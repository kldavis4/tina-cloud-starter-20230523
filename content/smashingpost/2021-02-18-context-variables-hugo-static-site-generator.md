---
title: 'Context And Variables In The Hugo Static Site Generator'
slug: context-variables-hugo-static-site-generator
author: kristian-lumme
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f0a7920-5d86-4efa-bbc0-cb554031617b/context-variables-hugo-static-site-generator.jpg
date: 2021-02-18T13:30:00.000Z
summary: >-
  In this article, we take a look at the topic of context and variables in Hugo, a popular static site generator. You’ll understand concepts such as the global context, flow control, and variables in Hugo templates, as well as data flow from content files through templates to partials and base templates.
description: >-
  In this article, we take a look at the topic of context and variables in Hugo, a popular static site generator. You’ll understand concepts such as the global context, flow control, and variables in Hugo templates, as well as data flow from content files through templates to partials and base templates.
categories:
  - Coding
  - Tools
  - Hugo
  - Generators
  - Guides
  - Static Generators
---

In this article, we’ll take a close look at how context works in the [Hugo static site generator](https://gohugo.io). We’ll examine how data flows from content to templates, how certain constructs change what data is available, and how we can pass on this data to partials and base templates.

This article is **not an introduction to Hugo**. You’ll probably get the most out of it if you have some experience with Hugo, as we won’t go over every concept from scratch, but rather focus on the main topic of context and variables. However, if you refer to the Hugo documentation throughout, you may well be able to follow along even without previous experience!

We’ll study various concepts by building up an example page. Not every single file required for the example site will be covered in detail, but the [complete project is available on GitHub](https://github.com/gittower/hugo-context-example). If you want to understand how the pieces fit together, that’s a good starting point. Please also note that we won’t cover how to *set up* a Hugo site or run the development server &mdash; instructions for running the example are in the repository.

### What Is A Static Site Generator?

If the concept of static site generators is new to you, here’s a quick introduction! Static site generators are perhaps best described by comparing them to dynamic sites. A dynamic site like a CMS generally assembles a page from scratch for each visit, perhaps fetching data from a database and combining various templates to do so. In practice, the use of caching means the page is not regenerated quite so often, but for the purpose of this comparison, we can think of it that way. A dynamic site is well suited to **dynamic content**: content that changes often, content that’s presented in a lot of different configurations depending on input, and content that can be manipulated by the site visitor.

In contrast, **many sites rarely change** and accept little input from visitors. A “help” section for an application, a list of articles or an eBook could be examples of such sites. In this case, it makes more sense to assemble the final pages _once_ when the content changes, thereafter serving the same pages to every visitor until the content changes again.

Dynamic sites have more flexibility, but place more demand on the server they’re running on. They can also be difficult to distribute geographically, especially if databases are involved. **Static site generators** can be hosted on any server capable of delivering static files, and are easy to distribute.

A common solution today, which mixes these approaches, is the [JAMstack](https://www.smashingmagazine.com/2020/02/headless-wordpress-site-jamstack/). “JAM” stands for JavaScript, APIs and markup and describes the building blocks of a JAMstack application: a static site generator generates **static files** for delivery to the client, but the stack has a dynamic component in the form of JavaScript running on the client &mdash; this client component can then use APIs to provide dynamic functionality to the user.

### Hugo

[Hugo](https://gohugo.io/) is a popular static site generator. It’s written in Go, and the fact that Go is a compiled programming language hints at some of Hugos benefits and drawbacks. For one, Hugo is **very fast**, meaning that it generates static sites very quickly. Of course, this has no bearing on how fast or slow the sites created using Hugo are for the end user, but for the developer, the fact that Hugo compiles even large sites in the blink of an eye is quite valuable.

However, as Hugo is written in a compiled language, **extending it is difficult**. Some other site generators allow you to insert your own code — in languages like Ruby, Python or JavaScript — into the compilation process. To extend Hugo, you would need to **add your code to Hugo itself and recompile it** &mdash; otherwise, you’re stuck with the template functions Hugo comes with out-of-the-box.

While it does provide a rich variety of functions, this fact can become limiting if the generation of your pages involves some complicated logic. As we found, having a site originally developed running on a dynamic platform, the cases where you’ve taken the ability to drop in your custom code for granted do tend to pile up.

Our team maintains a variety of web sites relating to our main product, [the Tower Git client](https://www.git-tower.com/), and we’ve recently looked at moving some of these over to a static site generator. One of our sites, [the “Learn” site](https://www.git-tower.com/learn/), looked like a particularly nice fit for a pilot project. This site contains a variety of free learning material including videos, eBooks and FAQs on Git, but also other tech topics.

Its content is largely of a static nature, and whatever interactive features there are (like newsletter sign-ups) were already powered by JavaScript. At the end of 2020, we **converted this site from our previous CMS to Hugo**, and today it runs as a static site. Naturally, we learned a lot about Hugo during this process. This article is a way of sharing some of the things we learned.

### Our Example

As this article grew out of our work on converting our pages to Hugo, it seems natural to put together a (very!) simplified hypothetical landing page as an example. Our main focus will be a reusable so-called “list” template.

In short, Hugo will use a list template for any page that contains subpages. [There’s more to Hugos template hierarchy](https://gohugo.io/templates/lookup-order/) than that, but you don’t have to implement every possible template. A single list template goes a long way. It will be used in any situation calling for a list template where no more specialized template is available.

Potential use cases include a home page, a blog index or a list of FAQs. Our reusable **list template** will reside in `layouts/_default/list.html` in our project. Again, the rest of the files needed to compile our example are [available on GitHub](https://github.com/gittower/hugo-context-example), where you can also get a better look at how the pieces fit together. The GitHub repository also comes with a `single.html` template &mdash; as the name suggests, this template is used for pages that do not have subpages, but act as single pieces of content in their own right.

Now that we’ve set the stage and explained what it is we’ll be doing, let’s get started!

{{% feature-panel %}}

## The Context Or “The Dot”

It all starts with the dot. In a Hugo template, the object `.` &mdash; “the dot” &mdash; refers to the current context. What does this mean? Every template rendered in Hugo has access to a set of data &mdash; **its context**. This is initially set to an [object representing the page](https://gohugo.io/templates/introduction/#variables) currently being rendered, including its content and some metadata. The context also includes site-wide variables like configuration options and information about the current environment. You’d access a field like the title of the current page using `.Title` and the version of Hugo being used through `.Hugo.Version` &mdash; in other words, you’re accessing _fields_ of the `.` structure.

<p class="c-pre-sidenote--left">Importantly, this context can change, making a reference like `.Title` above point at something else or even making it invalid. This happens, for example, as you loop over a collection of some kind using <code>range</code>, or as you <strong>split templates into partials and base templates</strong>. We’ll look at this in detail later!</p><p class="c-sidenote c-sidenote--right">Hugo uses the Go “templates” package, so when we refer to Hugo templates in this article, we’re really talking about Go templates. Hugo does add a lot template functions not available in standard Go templates.</p>

In my opinion, the context and the possibility to rebind it is one of Hugos best features. To me, it makes a lot of sense to always have “the dot” represent whatever object is the main focus of my template at a certain point, rebinding it as necessary as I go along. Of course, it’s possible to get yourself into a tangled mess as well, but I’ve been happy with it so far, to the extent that I quickly started missing it in any other static site generator I looked at.

With this, we’re ready to look out at the humble starting point of our example &mdash; the template below, residing in the location `layouts/_default/list.html` in our project:

<pre><code class="language-html">&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;{{ .Title }} | {{ .Site.Title }}&lt;/title&gt;
    &lt;link rel="stylesheet" href="/css/style.css"&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;nav&gt;
      &lt;a class="logo" href="{{ "/" | relURL }}"&gt;
        &lt;img src="/img/tower-logo.svg"&gt;
        &lt;img src="/img/tower-claim.svg"&gt;
      &lt;/a&gt;
      &lt;ul&gt;
        &lt;li&gt;&lt;a href="/"&gt;Home&lt;/a&gt;&lt;/li&gt;
      &lt;/ul&gt;
    &lt;/nav&gt;
    &lt;section class="content"&gt;
      &lt;div class="container"&gt;
        &lt;h1&gt;{{ .Title }}&lt;/h1&gt;
        {{ .Content }}
      &lt;/div&gt;
    &lt;/section&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

Most of the template consists of a bare-bones HTML structure, with a stylesheet link, a menu for navigation and some extra elements and classes used for styling. The interesting stuff is between the **curly braces**, which signal Hugo to step in and do its magic, replacing whatever is between the braces with the result of evaluating some expression and potentially manipulating the context as well.

As you may be able to guess, `{{ .Title }}` in the title tag refers to the title of the current page, while `{{ .Site.Title }}` refers to the title for the whole site, set in the Hugo configuration. A tag like `{{ .Title }}` simply tells Hugo to replace that tag with the contents of the field `Title` in the current context.

So, we’ve accessed some **data** belonging to the page in a template. Where does this data come from? That’s the topic of the following section.

## Content And Front Matter

Some of the variables available in the context are automatically provided by Hugo. Others are defined by us, mainly in **content files**. There are also other sources of data like configuration files, environment variables, data files and even APIs. In this article our focus will be on content files as the source of data.

In general, a single content file represents a single page. A typical content file includes the main content of that page but also metadata about the page, like its title or the date it was created. Hugo supports several formats both for [the main content](https://gohugo.io/content-management/formats/) and [the metadata](https://gohugo.io/content-management/front-matter/#front-matter-formats). In this article we’ll go with perhaps the most common combination: the content is provided as Markdown in a file containing the metadata as YAML front matter.

In practice, that means the content file starts with a section delimited by a line containing three dashes at each end. This section constitutes the **front matter**, and here metadata is defined using a `key: value` syntax (As we’ll see soon, YAML supports more elaborate data structures too). The front matter is followed by the actual content, specified using the Markdown markup language.

Let’s make things more concrete by looking at an example. Here’s a very simple content file with one front matter field and one paragraph of content:

<div class="break-out">

 <pre><code class="language-md">---
title: Home
---

Home page of the Tower Git client. Over 100,000 developers and designers use Tower to be more productive!
</code></pre>
</div>

(This file resides at `content/_index.md` in our project, with `_index.md` denoting the content file for a page that has subpages. Again, [the GitHub repository](https://github.com/gittower/hugo-context-example) makes it clear where which file is supposed to go.)

Rendered using the template from earlier, along with some styles and peripheral files (all found on GitHub), the result looks like this:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3726f71-c0f6-40ab-9ff5-d542a8643fed/1-start-context-variables-hugo-static-site-generator.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3726f71-c0f6-40ab-9ff5-d542a8643fed/1-start-context-variables-hugo-static-site-generator.png" width="800" height="301" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3726f71-c0f6-40ab-9ff5-d542a8643fed/1-start-context-variables-hugo-static-site-generator.png'>Large preview</a>)" alt="Home page of the Tower Git client" >}}

You may wonder whether the field names in the front matter of our content file are predetermined, or whether we can add any field we like. The answer is “both”. There is [a list of predefined fields](https://gohugo.io/content-management/front-matter/#predefined), but we can also add any other field we can come up with. However, these fields are accessed a bit differently in the template. While a predefined field like `title` is accessed simply as `.Title`, a custom field like `author` is accessed using `.Params.author`.

(For a quick reference on the predefined fields, along with things like functions, function parameters and page variables, see [our own Hugo cheat sheet](https://www.git-tower.com/learn/cheat-sheets/hugo/)!)

The `.Content` variable, used to access the main content from the content file in your template, is special. Hugo has a **“shortcode” feature** allowing you to use some extra tags in your Markdown content. You can also define your own. Unfortunately, these shortcodes will only work through the `.Content` variable &mdash; while you can run any other piece of data through a Markdown filter, this will not handle the shortcodes in the content.

A note here about undefined variables: accessing a predefined field like `.Date` always works, even though you haven’t set it &mdash; an empty value will be returned in this case. Accessing an undefined custom field, like `.Params.thisHasNotBeenSet`, also works, returning an empty value. However, accessing a non-predefined top-level field like `.thisDoesNotExist` will prevent the site from compiling.

As indicated by `.Params.author` as well as `.Hugo.version` and `.Site.title` earlier, chained invocations can be used to access a field nested in some other data structure. We can define such structures in our front matter. Let’s look at an example, where **we define a map**, or dictionary, specifying some properties for a banner on the page in our content file. Here is the updated `content/_index.md`:

<div class="break-out">

 <pre><code class="language-md">---
title: Home
banner:
  headline: Try Tower For Free!
  subline: Download our trial to try Tower for 30 days
---

Home page of the Tower Git client. Over 100,000 developers and designers use Tower to be more productive!
</code></pre>
</div>

Now, let’s add a banner to our template, referring to the banner data using `.Params` the way described above:

<pre><code class="language-html">&lt;html&gt;
  ...
  &lt;body&gt;
    ...
    &lt;aside&gt;
      &lt;h2&gt;{{ .Params.banner.headline }}&lt;/h2&gt;
      &lt;p&gt;{{ .Params.banner.subline}}&lt;/p&gt;
    &lt;/aside&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

Here’s what our site looks like now:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79ef32aa-305b-4739-899c-b85b872385cf/2-params-context-variables-hugo-static-site-generator.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79ef32aa-305b-4739-899c-b85b872385cf/2-params-context-variables-hugo-static-site-generator.png" width="800" height="467" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79ef32aa-305b-4739-899c-b85b872385cf/2-params-context-variables-hugo-static-site-generator.png'>Large preview</a>)" alt="Home page of the Tower Git client with a banner saying Try Tower For Free" >}}

Alright! At the moment, we’re accessing fields of the default context without any issues. However, as mentioned earlier, this context is not fixed, but can change.

Let’s take a look at how that might happen.

## Flow Control

Flow control statements are an important part of a templating language, allowing you do different things depending on the value of variables, loop through data and more. Hugo templates provide [the expected set of constructs](https://gohugo.io/templates/introduction/#logic), including `if/else` for conditional logic, and `range` for looping. Here, we will not cover flow control in Hugo in general (for more on this, see the [documentation](https://gohugo.io/documentation/)), but focus on how these statements affect the context. In this case, the most interesting statements are `with` and `range`.

Let’s start with `with`. This statement checks if some expression has a “non-empty” value, and, if it has, _rebinds the context to refer to the value of that expression_. An `end` tag indicates the point where the influence of the `with` statement stops, and the context is rebound to whatever it was before. The Hugo documentation [defines a non-empty value](https://gohugo.io/templates/introduction/#conditionals) as false, 0, and any zero-length array, slice, map or string.

Currently, our list template is not doing much listing at all. It might make sense for a list template to actually **feature some of its subpages** in some way. This gives us a perfect opportunity for examples of our flow control statements.

Perhaps we want to display some featured content at the top of our page. This could be any piece of content &mdash; a blog post, a help article or a recipe, for example. Right now, let’s say our Tower example site has some pages highlighting its features, use-cases, a help page, a blog page, and a “learning platform” page. These are all located in the `content/` directory. We configure which piece of content to feature by adding a field in the content file for our home page, `content/_index.md`. The page is referred to by its path, assuming the content directory as root, like so:

<div class="break-out">

 <pre><code class="language-md">---
title: Home
banner:
  headline: Try Tower For Free!
  subline: Download our trial to try Tower for 30 days without limitations
featured: /features.md
...
---
...
</code></pre>
</div>

Next, our list template has to be modified to display this piece of content. Hugo has a template function, `.GetPage`, which will allow us to refer to page objects other than the one we’re currently rendering. Recall how the context, `.`, was initially bound to an object representing the page being rendered? Using `.GetPage` and `with`, we can **temporarily rebind the context** to another page, referring to the fields of *that* page when displaying our featured content:

<pre><code class="language-html">&lt;nav&gt;
  ...
&lt;/nav&gt;
&lt;section class="featured"&gt;
  &lt;div class="container"&gt;
    {{ with .GetPage .Params.featured }}
      &lt;article&gt;
        &lt;h2&gt;{{ .Title }}&lt;/h2&gt;
        {{ .Summary }}
        &lt;p&gt;&lt;a href="{{ .Permalink }}"&gt;Read more →&lt;/a&gt;&lt;/p&gt;
      &lt;/article&gt;
    {{ end }}
  &lt;/div&gt;
&lt;/section&gt;
</code></pre>

Here, `{{ .Title }}`, `{{ .Summary }}` and `{{ .Permalink }}` between the `with` and the `end` tags refer to those fields *in the featured page*, and not the main one being rendered.

In addition to having a featured piece of content, let’s list a few more pieces of content further down. Just like the featured content, the listed pieces of content will be defined in `content/_index.md`, the content file for our home page. We’ll add a list of content paths to our front matter like this (in this case also specifying the section headline):

<pre><code class="language-markup">---
...
listing_headline: Featured Pages
listing:
  - /help.md
  - /use-cases.md
  - /blog/_index.md
  - /learn.md
---
</code></pre>

The reason that the blog page has its own directory and an `_index.md` file is that the blog will have subpages of its own &mdash; blog posts.

To display this list in our template, we’ll use `range`. Unsurprisingly, this statement will loop over a list, but it will also rebind the context to each element of the list in turn. This is very convenient for our content list.

Note that, from the perspective of Hugo, “listing” only contains some strings. For each iteration of the “range” loop, the **context will be bound to one of those strings**. To get access to the actual page object, we supply its path string (now the value of `.`) as an argument to `.GetPage`. Then, we’ll use the `with` statement again to rebind the context to the listed page object rather than its path string. Now, it’s easy to display the content of each listed page in turn:

<pre><code class="language-html">&lt;aside&gt;
  ...
&lt;/aside&gt;
&lt;section class="listing"&gt;
  &lt;div class="container"&gt;
    &lt;h1&gt;{{ .Params.listing_headline }}&lt;/h1&gt;
    &lt;div&gt;
      {{ range .Params.listing }}
        {{ with $.GetPage . }}
          &lt;article&gt;
            &lt;h2&gt;{{ .Title }}&lt;/h2&gt;
            {{ .Summary }}
            &lt;p&gt;&lt;a href="{{ .Permalink }}"&gt;Read more&nbsp;&rarr;&lt;/a&gt;&lt;/p&gt;
          &lt;/article&gt;
        {{ end }}
      {{ end }}
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/section&gt;
</code></pre>

Here’s what the site looks like at this point:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa7d5177-30d5-46a0-bf91-8789114e8129/3-flow-control-context-variables-hugo-static-site-generator.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa7d5177-30d5-46a0-bf91-8789114e8129/3-flow-control-context-variables-hugo-static-site-generator.png" width="800" height="1645" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa7d5177-30d5-46a0-bf91-8789114e8129/3-flow-control-context-variables-hugo-static-site-generator.png'>Large preview</a>)" alt="Home page of the Tower Git client showing four featured pages and banners" >}}

But hold on, there’s something weird in the template above &mdash; rather than calling `.GetPage`, we’re calling `$.GetPage`. Can you guess why `.GetPage` wouldn’t work?

The notation `.GetPage` indicates that the `GetPage` function is a method of the current context. Indeed, in the default context, there is such a method, but we’ve just gone ahead and **changed the context**! When we call `.GetPage`, the context is bound to a string, which does not have that method. The way we work around this is the topic of the next section.

{{% ad-panel-leaderboard %}}

## The Global Context

As seen above, there are situations where the context has been changed, but we’d still like to access the original context. Here, it’s because we want to call a method existing in the original context &mdash; another common situation is when we want to access some property of the main page being rendered. No problem, there’s an easy way to do this.

In a Hugo template, `$`, known as the **global context**, refers to the original value of the context &mdash; the context as it was when template processing started. In the previous section, it was used to call the `.GetPage` method even though we had rebound the context to a string. Now, we’ll also use it to access a field of the page being rendered.

At the beginning of this article, I mentioned that our list template is reusable. So far, we’ve only used it for the home page, rendering a content file located at `content/_index.md`. In the example repository, there is another content file which will be rendered using this template: `content/blog/_index.md`. This is an index page for the blog, and just like the home page it shows a featured piece of content and lists a few more &mdash; blog posts, in this case.

Now, let’s say we want to show listed content **slightly differently on the home page** &mdash; not enough to warrant a separate template, but something we can do with a conditional statement in the template itself. As an example, we’ll display the listed content in a two-column grid, as opposed to a single-column list, if we detect that we’re rendering the home page.

Hugo comes with a page method, `.IsHome`, which provides exactly the functionality we need. We’ll handle the actual change in presentation by adding a class to the individual pieces of content when we find we’re on the home page, allowing our CSS file do the rest.

We could, of course, add the class to the body element or some containing element instead, but that wouldn’t enable as good a demonstration of the global context. By the time we write the HTML for the listed piece of content, `.` **refers to the listed page**, but `IsHome` needs to be called on the main page being rendered. The global context comes to our rescue:

<pre><code class="language-html">&lt;section class="listing"&gt;
  &lt;div class="container"&gt;
    &lt;h1&gt;{{ .Params.listing_headline }}&lt;/h1&gt;
    &lt;div&gt;
      {{ range .Params.listing }}
        {{ with $.GetPage . }}
          &lt;article{{ if $.IsHome }} class="home"{{ end }}&gt;
            &lt;h2&gt;{{ .Title }}&lt;/h2&gt;
            {{ .Summary }}
            &lt;p&gt;&lt;a href="{{ .Permalink }}"&gt;Read more →&lt;/a&gt;&lt;/p&gt;
          &lt;/article&gt;
        {{ end }}
      {{ end }}
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/section&gt;
</code></pre>

The blog index looks just like our home page did, albeit with different content:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7def4339-f62b-4d2a-909b-297f3aa3d97e/4-global-context-1-context-variables-hugo-static-site-generator.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7def4339-f62b-4d2a-909b-297f3aa3d97e/4-global-context-1-context-variables-hugo-static-site-generator.png" width="800" height="1775" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7def4339-f62b-4d2a-909b-297f3aa3d97e/4-global-context-1-context-variables-hugo-static-site-generator.png'>Large preview</a>)" alt="Home page of the Tower Git client showing four featured pages and banners with different content" >}}

...but our home page now displays its featured content in a grid:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1533ba5a-1c05-4603-8eb6-856cd0d05800/4-global-context-2-context-variables-hugo-static-site-generator.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1533ba5a-1c05-4603-8eb6-856cd0d05800/4-global-context-2-context-variables-hugo-static-site-generator.png" width="800" height="1395" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1533ba5a-1c05-4603-8eb6-856cd0d05800/4-global-context-2-context-variables-hugo-static-site-generator.png'>Large preview</a>)" alt="Home page of the Tower Git client showing four featured pages in two rows by two columns and not all four on top of each other as before" >}}

## Partial Templates

When building up a real website, it quickly becomes useful to split your templates into parts. Perhaps you want to reuse some particular part of a template, or perhaps you just want to split a huge, unwieldy template into coherent pieces. For this purpose, Hugo’s partial templates are the way to go.

From a context perspective, the important thing here is that when we include a partial template, we **explicitly pass it the context** we want to make available to it. A common practice is to pass in the context as it is when the partial is included, like this: `{{ partial "my/partial.html" . }}`. If the dot here refers to the page being rendered, that’s what will be passed to the partial; if the context has been rebound to something else, that’s what’s passed down.

You can, of course, rebind the context in partial templates just like in normal ones. In this case, the global context, `$`, refers to the original context passed to the partial, not the main page being rendered (unless that’s what was passed in).

If we want a partial template to have access to some particular piece of data, we might run into problems if we pass only this to the partial. Recall our problem earlier with accessing page methods after rebinding the context? The same goes for **partials**, but in this case the global context can’t help us &mdash; if we’ve passed in, say, a string to a partial template, the global context in the partial will refer to that string, and we won’t be able to call methods defined on the page context.

The solution to this problem lies in **passing in more than one piece of data** when including the partial. However, we’re only allowed to provide one argument to the partial call. We can, however, make this argument a compund data type, commonly a map (known as a  dictionary or a hash in other programming languages).

In this map, we can, for example, have a `Page` key set to the current page object, along with other keys for any custom data to pass in. The page object will then be available as `.Page` in the partial, and the other values of the map are accessed similarly. A map is created using [the `dict` template function](https://gohugo.io/functions/dict/), which takes an even number of arguments, interpreted alternately as a key, its value, a key, its value and so on.

In our example template, let’s move the code for our featured and listed content into partials. For the featured content, it’s enough to pass in the featured page object. The listed content, however, needs access to the `.IsHome` method in addition to the particular listed content being rendered. As mentioned earlier, while `.IsHome` is available on the page object for the listed page as well, that won’t give us the correct answer &mdash; we want to know if the _main page_ being rendered is the home page.

We could instead pass in a boolean set to the result of calling `.IsHome`, but perhaps the partial will need access to other page methods in the future &mdash; let’s go with **passing in the main page object** as well as the listed page object. In our example, the main page is found in `$` and the listed page in `.`. So, in the map passed to the `listed` partial, the key `Page` gets the value `$` while the key “Listed” gets the value `.`. This is the updated main template:

<div class="break-out">

 <pre><code class="language-html">&lt;body&gt;
  &lt;nav&gt;
    &lt;a class="logo" href="{{ "/" | relURL }}"&gt;
      &lt;img src="/img/tower-logo.svg"&gt;
      &lt;img src="/img/tower-claim.svg"&gt;
    &lt;/a&gt;
    &lt;ul&gt;
      &lt;li&gt;&lt;a href="/"&gt;Home&lt;/a&gt;&lt;/li&gt;
      &lt;li&gt;&lt;a href="/blog/"&gt;Blog&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
  &lt;/nav&gt;
  &lt;section class="featured"&gt;
    &lt;div class="container"&gt;
      {{ with .GetPage .Params.featured }}
        {{ partial "partials/featured.html" . }}
      {{ end }}
    &lt;/div&gt;
  &lt;/section&gt;
  &lt;section class="content"&gt;
    &lt;div class="container"&gt;
      &lt;h1&gt;{{ .Title }}&lt;/h1&gt;
      {{ .Content }}
    &lt;/div&gt;
  &lt;/section&gt;
  &lt;aside&gt;
    &lt;h2&gt;{{ .Params.banner.headline }}&lt;/h2&gt;
    &lt;p&gt;{{ .Params.banner.subline}}&lt;/p&gt;
  &lt;/aside&gt;
  &lt;section class="listing"&gt;
    &lt;div class="container"&gt;
      &lt;h1&gt;{{ .Params.listing_headline }}&lt;/h1&gt;
      &lt;div&gt;
        {{ range .Params.listing }}
          {{ with $.GetPage . }}
            {{ partial "partials/listed.html" (dict "Page" $ "Listed" .) }}
          {{ end }}
        {{ end }}
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/section&gt;
&lt;/body&gt;
</code></pre>
</div>

The content of our “featured” partial does not change compared to when it was part of the list template:

<pre><code class="language-html">&lt;article&gt;
  &lt;h2&gt;{{ .Title }}&lt;/h2&gt;
  {{ .Summary }}
  &lt;p&gt;&lt;a href="{{ .Permalink }}"&gt;Read more →&lt;/a&gt;&lt;/p&gt;
&lt;/article&gt;
</code></pre>

Our partial for listed content, however, reflects the fact that the original page object is now found in `.Page` while the listed piece of content is found in `.Listed`:

<div class="break-out">

<pre><code class="language-html">&lt;article{{ if .Page.IsHome }} class="home"{{ end }}&gt;
  &lt;h2&gt;{{ .Listed.Title }}&lt;/h2&gt;
  {{ .Listed.Summary }}
  &lt;p&gt;&lt;a href="{{ .Listed.Permalink }}"&gt;Read more&nbsp;&rarr;&lt;/a&gt;&lt;/p&gt;
&lt;/article&gt;
</code></pre>
</div>

Hugo also provides [base template functionality](https://gohugo.io/templates/base/) which lets you **extend a common base template**, as opposed to including subtemplates. In this case, the context works similarly: when extending a base template, you provide the data that will constitute the original context in that template.

## Custom Variables

It is also possible to assign and reassign your own custom variables in a Hugo template. These will be available in the template where they’re declared, but won’t make their way into any partials or base templates unless we explicitly pass them on. A custom variable **declared inside a “block”** like the one specified by an `if` statement will only be available inside that block &mdash; if we want to refer to it outside the block, we need to declare it outside the block, then modify it inside the block as required.

Custom variables have names **prefixed** by a dollar sign (`$`). To declare a variable and give it a value at the same time, use the `:=` operator. Subsequent assignments to the variable use the `=` operator (without colon). A variable can’t be assigned to before being declared, and it can’t be declared without giving it a value.

One use case for custom variables is simplifying long function calls by assigning some intermediate result to an appropriately named variable. For example, we could assign the featured page object to a variable named `$featured` and then supply this variable to the `with` statement. We could also put the data to supply to the “listed” partial in a variable and give that to the partial call.

Here’s what our template would look like with those changes:

<div class="break-out">

<pre><code class="language-html">&lt;section class="featured">
  &lt;div class="container">
    {{ $featured := .GetPage .Params.featured }}
    {{ with $featured }}
      {{ partial "partials/featured.html" . }}
    {{ end }}
  &lt;/div>
&lt;/section>
&lt;section class="content">
  ...
&lt;/section>
&lt;aside>
  ...
&lt;/aside>
&lt;section class="listing">
  &lt;div class="container">
    &lt;h1>{{ .Params.listing_headline }}&lt;/h1>
    &lt;div>
      {{ range .Params.listing }}
        {{ with $.GetPage . }}
          {{ $context := (dict "Page" $ "Listed" .) }}
          {{ partial "partials/listed.html" $context }}
        {{ end }}
      {{ end }}
    &lt;/div>
  &lt;/div>
&lt;/section>
</code></pre>
</div>

Based on my experience with Hugo, I’d recommend **using custom variables liberally** as soon as you’re trying to implement some more involved logic in a template. While it’s natural to try to keep your code concise, this may easily make things less clear than they could be, confusing you and others.

Instead, use **descriptively named variables** for each step and don’t worry about using two lines (or three, or four, etc.) where one would do.

{{% ad-panel-leaderboard %}}

## .Scratch

Finally, let’s cover the `.Scratch` mechanism. In earlier versions of Hugo, custom variables could only be assigned to once; it was not possible to redefine a custom variable. Nowadays, custom variables can be redefined, which makes `.Scratch` less important, though it still has its uses.

In short, `.Scratch` is a scratch area allowing you to **set and modify your own variables**, like custom variables. Unlike custom variables, `.Scratch` belongs to the page context, so passing that context on to a partial, for example, will bring the scratch variables along with it automatically.

You can set and retrieve variables on `.Scratch` by calling its methods `Set` and `Get`. There are [more methods than these](https://gohugo.io/functions/scratch/), for example for setting and updating compound data types, but these two ones will suffice for our needs here. `Set` takes **two parameters**: the key and the value for the data you want to set. `Get` only takes one: the key for the data you want to retrieve.

Earlier, we used `dict` to create a map data structure to pass multiple pieces of data to a partial. This was done so that the partial for a listed page would have access to both the original page context and the particular listed page object. Using `.Scratch` is not necessarily a better or worse way to do this &mdash; whichever is preferrable may depend on the situation.

Let’s see what our list template would look like using `.Scratch` instead of `dict` to pass data to the partial. We call `$.Scratch.Get` (again using the global context) to set the scratch variable “listed” to `.` &mdash; in this case, the listed page object. Then we pass in just the page object, `$`, to the partial. The scratch variables will follow along automatically.

<pre><code class="language-html">&lt;section class="listing"&gt;
  &lt;div class="container"&gt;
    &lt;h1&gt;{{ .Params.listing_headline }}&lt;/h1&gt;
    &lt;div&gt;
      {{ range .Params.listing }}
        {{ with $.GetPage . }}
          {{ $.Scratch.Set "listed" . }}
          {{ partial "partials/listed.html" $ }}
        {{ end }}
      {{ end }}
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/section&gt;
</code></pre>

This would require some modification to the `listed.html` partial as well &mdash; the original page context is now available as “the dot” while the listed page is retrieved from the `.Scratch` object. We’ll use a custom variable to simplify access to the listed page:

<pre><code class="language-html">&lt;article{{ if .IsHome }} class="home"{{ end }}&gt;
  {{ $listed := .Scratch.Get "listed" }}
  &lt;h2&gt;{{ $listed.Title }}&lt;/h2&gt;
  {{ $listed.Summary }}
  &lt;p&gt;&lt;a href="{{ $listed.Permalink }}"&gt;Read more →&lt;/a&gt;&lt;/p&gt;
&lt;/article&gt;
</code></pre>

One argument for doing things this way is consistency. Using `.Scratch`, you can make it a habit to always pass in the current page object to any partial, adding any extra data as scratch variables. Then, whenever you write or edit your partials, you know that `.` is a page object. Of course, you can establish a convention for yourself using a passed-in map as well: always sending along the page object as `.Page`, for example.

## Conclusion

When it comes to context and data, a static site generator brings both benefits and limitations. On one hand, an operation that is too inefficient when run for every page visit may be perfectly good when run only once as the page is compiled. On the other hand, it may surprise you how often it would be useful to have access to some part of the network request even on a predominantly static site.

To **handle query string parameters**, for example, on a static site, you’d have to resort to JavaScript or some proprietary solution like [Netlify’s redirects](https://docs.netlify.com/routing/redirects/redirect-options/#query-parameters). The point here is that while the jump from a dynamic to a static site is simple in theory, it does take a shift in mindset. In the beginning, it’s easy to fall back on your old habits, but practice will make perfect.

With that, we conclude our look at data management in the Hugo static site generator. Even though we focused only on a narrow sector of its functionality, there are certainly things we didn’t cover that could have been included. Nevertheless, I hope this article gave you some added insight into how data flows from content files, to templates, to subtemplates and how it can be modified along the way.

**Note**: *If you already have some Hugo experience, we have a nice resource for you, quite appropriately residing on our aforementioned, Hugo-driven “Learn” site! When you just need to check the order of the arguments to the `replaceRE` function, how to retrieve the next page in a section, or what the “expiration date” front matter field is called, a cheat sheet comes in handy. We’ve put together just such a reference, so [download a Hugo cheat sheet](https://www.git-tower.com/learn/cheat-sheets/hugo/), in a package also featuring a host of other cheat sheets on everything from Git to the Visual Studio Code editor.*

### Further Reading

If you’re looking for more information on Hugo, here are some nice resources:

- [The official Hugo documentation](https://gohugo.io/documentation/) is always a good place to start!
- A great series of in-depth posts on Hugo on [Régis Philibert’s blog](https://regisphilibert.com/tags/hugo/).

{{< signature "vf, il" >}}

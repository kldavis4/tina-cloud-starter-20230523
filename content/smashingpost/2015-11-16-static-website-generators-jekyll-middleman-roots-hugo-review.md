---
title: 'Static Site Generators Reviewed: Jekyll, Middleman, Roots, Hugo'
slug: static-website-generators-jekyll-middleman-roots-hugo-review
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7687f63b-9e2d-4588-94d2-0a9cc6512035/middleman-opt.png'
date: 2015-11-16T15:01:38.000Z
author: mathiasbiilmannchristensen
summary: >-
  Static site generators are quickly becoming a big part of the professional website builder’s toolbox. A new static website generator seems to pop up every week. Figuring out which one to use can be like a walk in the jungle.
description: >-
  Static site generators are quickly becoming a big part of the professional website builder’s toolbox. A new static website generator seems to pop up every week. Figuring out which one to use can be like a walk in the jungle.
categories:
  - Coding
  - Tools
  - Generators
  - Static Generators
  - Jekyll
---
In my [previous article](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/), I looked at why static website generation is growing in popularity, and I gave a high-level overview of all of the components of a modern generator.

In this article, we’ll look at four popular static website generators &mdash; Jekyll, Middleman, Roots, Hugo &mdash; in far more detail. This should give you a great starting point for finding the right one for your project. A [lot of other ones](https://www.staticgen.com) are out there, and many of them could have made this list. The ones I chose for this article represent the different trends that dominate the landscape today.

Each generator takes a repository with plain-text files, runs one or more compilation phases, and spits out a folder with a static website that can be hosted anywhere. **No PHP or database needed**.

## Jekyll

No article today about static website generation can get by without mentioning Jekyll.

We might not be talking about the resurgence of static websites if GitHub’s founder, Tom Preston-Werner, hadn’t sat down in his San Francisco apartment in October 2008 with a glass of apple cider and the urge to write his own blogging engine.

{{% feature-panel %}}

The result was Jekyll, “a simple, blog-aware, static site generator.”

One of the brilliant ideas behind Jekyll is that <strong>it lets any normal static website be a valid Jekyll project</strong>. This makes it one of the easiest generators to get started with:

1.  Take a plain HTML mockup of a blog.
2.  Get rid of repeating headers, menus, footers and so on by working with layouts and includes.
3.  Turn pages and blog posts into Markdown, and pull the content into the templates.

Along the way, Jekyll <strong>can act as a local web server</strong> and keep watch over any files in your project, generating all of the HTML, CSS and JavaScript files from templates, Markdown, Sass or CoffeeScript files.

Jekyll was the first static generator to introduce the concept of “front matter,” a way of annotating templates or Markdown files with meta data. Front matter is a bit of YAML at the top of any text file, indicated by three leading and following hyphens (<code>---</code>):

<div class="break-out">

 <pre><code class="language-css">
title: A blog post
date: 2014-09-01
tags: ["meta", "yaml"]
---
# Blogpost with meta data

This is a short example of a Markdown document with meta data as front matter.
</code></pre>
</div>

### Templating Engine

Jekyll is built on Liquid, a templating engine that originated with Shopify. This is both a blessing and a curse. Liquid is a <strong>safe templating engine</strong> made to run untrusted templates for Shopify’s hosted platform. That means there is no custom code in the templates. Ever.

On the one hand, this can make templates simpler and more declarative, and Liquid has a good set of filters and helpers built in out of the box.

On the other hand, it does mean you have to start creating your own Liquid helpers from Jekyll plugins if you want to do anything that’s not baked in.

Liquid lets you use variables in your templates like this: <code>{{ some_variable }}</code>. And blog tags looks like this: <code>{% if some_variable %}Show this{% endif %}</code>. Jekyll adds a few tags to handle includes and links, plus some helpers for sorting, filtering and escaping content. One glaring omission is a simple <strong>way to handle default values for variables</strong>. At some point in the future, <code>{{ some_variable | default: 'Default Value' }}</code> should start working, but it’s not there yet. So, right now you’ll find a lot of clunky <code>if</code> and <code>else</code> statements in Jekyll websites that work around this.

### Content Model

Jekyll’s content model has evolved a lot since the tool was conceived as a simple blogging engine.

Today, content can be stored in several different forms and take on different behavior.

The simplest form is an individual document in either <strong>Markdown or HTML</strong>. This file gets converted into a corresponding HTML page when the page is built. The document can specify a layout that will be used when it is turned into an HTML page, as well as specify various meta data, which you can access from templates via the <code>{{page}}</code> variable.

Jekyll has special support for a folder named <code>&#95;posts</code> that contains Markdown files with a naming scheme of <code>yyyy-mm-dd-title-of-the-post.md</code>. Posts behave like you would typically expect from entries on a blog.

Since version 2.0, Jekyll supports <strong>collections</strong>. A collection is a folder with Markdown documents. You can access collections in templates through the special <code>{{site.collections}}</code> variable, and you can configure each document in the collection to have its own permalink. One big upcoming change in Jekyll 3.0 is that the distinction between <code>&#95;posts</code> and <code>collections</code> will be eliminated.

The last form of content is data files. These are stored in a special <code>&#95;data</code> folder, and they can be YAML, JSON or CSV files. From there, you can pull the data into any template file through the <code>{{site.data}}</code> variable.

{{% ad-panel-leaderboard %}}

### Asset Pipeline

Jekyll’s asset pipeline is extremely simple. Just as with the logic-less Liquid, this is both good and bad. There’s <strong>no built-in support for live reloading, minification or asset bundling</strong>; however, Sass and CoffeeScript are pretty straightforward to handle. Any <code>.sass</code>, <code>.scss</code> or <code>.coffee</code> file that starts with YAML front matter will be processed by Jekyll and turned into a corresponding <code>.css</code> or <code>.js</code> file in the final output for the static website.

This means a CoffeeScript file would have to look like this in order to get processed by Jekyll:

<pre><code class="language-javascript">
alert "Hello from CoffeeScript"
</code></pre>

Your editor’s syntax highlighter might not be super-excited about the leading hyphens.

If you look at the code for large Jekyll websites out there in the wild, you’ll see that many of them drop Jekyll’s built-in asset pipeline in favor of a combination of Grunt or Gulp with Jekyll to run their builds. For a large project, this is typically the way to go because you can take advantage of the large infrastructure around these projects and get BrowserSync or LiveReload to work.

### Putting It All Together

Let’s look at an actual Jekyll website to see how all of these parts fit together. What better source to learn from than the official <a href="https://jekyllrb.com/">Jekyll</a> website. We’ll be looking at the documentation section here. You can follow along in the GitHub repository.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/311d5900-5c2f-4954-ba4a-ca503c954b3a/01-jekyll-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21efaf31-0919-4eac-bc96-7e541181091d/01-jekyll-opt-preview.png" alt="static site generator" width="500" height="537" /></a><figcaption>How Jekyll’s documentation page works (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/311d5900-5c2f-4954-ba4a-ca503c954b3a/01-jekyll-opt.png">View large version</a>)</figcaption></figure>

Here, I’ve marked roughly where all of the parts of the page come from.

The main structure of the website is defined in <code>&#95;layouts/default.html</code>. There are two includes, <code>&#95;includes/header.html</code> and <code>&#95;includes/footer.html</code>. The header has a fairly hardcoded navigation menu. Jekyll doesn’t have a way to pull in a specific set of pages and iterate over them; so, typically, the main navigation of a website will end up being coded by hand.

Each page in the documentation section is a Markdown file in the <code>&#95;docs/</code> folder. The pages use a handy feature of Jekyll called nested layouts. The layout for the document section is set to <code>&#95;layouts/docs.html</code>, and that layout in turn uses <code>&#95;layouts/default.html</code>.

The navigation sidebar is generated from data in <code>&#95;data/docs.yml</code>, which arranges the different files in the documentation into different groups, each with its title.

### Extending Jekyll

Jekyll is quite simple to extend, and the <strong>ecosystem of plugins is fairly large</strong>. The simplest way to extend Jekyll is to add a Ruby file in the <code>&#95;plugins</code> folder. There are five types of plugins: generators, converters, commands, tags and filters.

As mentioned earlier, the Liquid templating engine is strict about not allowing any code in the templates. Tags and filters work around this by enabling you to add your own tags and filters.

Generators and converters let you hook into the build process of Jekyll and generate extra pages or support new file formats.

Commands let you add new features to Jekyll’s command-line interface.

### In Summary

Jekyll is widely used, and since version 2, the content model has grown rich enough to support websites with way more complexity than that of a simple blog. For a large project, you’ll probably quickly outgrow the limited asset pipeline and start relying on Gulp or Grunt. Liquid is battle-tested and a solid templating engine, but it can feel limiting. And as soon as you want to do complex filtering or querying on your content, you’ll need to write your own plugins.

{{% ad-panel-leaderboard %}}

## Middleman

Middleman is about the same age as Jekyll. While it never got the widespread adoption that Jekyll achieved from the latter’s default integration with GitHub pages, it has quietly become the backbone of websites for some of the web’s most design-savvy companies: The websites for MailChimp, Nest and Simple are all built with Middleman.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7687f63b-9e2d-4588-94d2-0a9cc6512035/middleman-opt.png" alt="Middleman" /><figcaption>The websites for MailChimp, Nest and Simple are all built with Middleman.</figcaption></figure>

It’s a thriving open-source project with more than a hundred contributors. The muscle behind it is Thomas Reynolds, technical director of Portland-based <a href="https://www.instrument.com/">Instrument</a>.

Whereas Jekyll was born of the desire for a simple, static blogging engine, Middleman was built as a <strong>framework for more advanced marketing and documentation websites</strong>. It’s a powerful tool and fast to pick up if you’re coming from the world of Rails.

### Templating Engine

A stated goal of its author is to make Middleman feel like Ruby on Rails for static websites. Just as in Rails, the default templating engine is Ruby’s standard embedded <strong>Ruby (ERB) templates</strong>, but swapping these out for Haml or Liquid is straightforward.

ERB is a straightforward templating engine that lets you use free-form Ruby in your templates, with no restrictions. This gives the engine a lot more power than Liquid, but obviously it also requires more discipline on your part because you can write as much code as you want right in your templates.

### Asset Pipeline

For years, the stable version of Middleman has been version 3. Now, version 4 is in beta and will bring some big changes to both the content model and the asset pipeline.

The core of Middleman’s content model is the <code>sitemap</code>. The site map is a list of all of the files that makes up your Middleman file, called “resources” in Middleman terminology.

Each resource has a <code>source_file</code> and a <code>destination_file</code> and gets fed through Middleman’s asset pipeline when the website is built.

A simple <code>source/about/index.html</code> source file would end up as a <code>build/about/index.html</code> destination file without any transformations. Just as when you use Rails’ asset pipeline, you can string together file extensions to specify what transformations to apply to your files.

A file named <code>source/about/index.html.erb</code> will get passed through the ERB templating engine and get transformed into <code>build/about/index.html</code>. A file named <code>source/js/app.js.coffee</code> would be compiled as CoffeeScript and end up as <code>build/js/app.js</code>.

The asset pipeline is built on <a href="https://github.com/sstephenson/sprockets">Sprockets</a>, just like Rails, which means you can use “magic” comments in your JavaScript and CSS files to include dependencies:

<pre><code class="language-bash">//= require 'includes/test.js'
</code></pre>

This makes it easy to <strong>split your front end into small modules</strong> and have Middleman resolve the dependencies at build time.

The upcoming version 4 introduces the concept of <strong>external pipelines</strong>. These let Middleman control external tools such as Ember CLI and Webpack during the build process and makes its asset pipeline even more powerful. This is really handy for getting Middleman to spin up a separate process running Ember CLI and then proxy the right requests through to the Ember.js server.

### Content Model

In your templates, you can access the site map and use Ruby to easily access, filter and sort the content.

The current stable version of Middleman (3) comes with a query interface in the site map that mimics Active Record (the object-relational mapping that powers Rails). That’s been stripped in the upcoming version 4, in favor of simple Ruby methods to query the data.

Let’s say you have a folder named <code>source/faq</code>. The FAQ entries are stored in Markdown files with a bit of front matter, and one looks something like this:

<div class="break-out">

 <pre><code class="language-markup">---
title: What is Middleman?
position: 1
---
Middleman is a [static website generator](https://www.staticgen.com) with all of the shortcuts and tools of modern web development.
</code></pre>
</div>

Suppose you want to pull all of these entries into an ERB template and order them by position. Our imaginary <code>source/faq.html.erb</code> would look something like this:

<pre><code class="language-markup">&lt;h1&gt;FAQ&lt;/h1&gt;
&lt;% sitemap.resources
   .select { |resource| resource.path =~ /^faq\// }
   .sort_by { |resource| resource.data.position }
   .each do |resource| %&gt;
   &lt;h2 class="question"&gt;&lt;%= resource.data.title %&gt;&lt;/h2&gt;
   &lt;div class="answer"&gt;&lt;%= resource.render(:layout =&gt; false) %&gt;&lt;/div&gt;
&lt;% end %&gt;
</code></pre>

Version 4 introduces the concept of <strong>collections</strong>, which let you turn those kinds of filters in the site map into a collection. When running in LiveReload mode, Middleman watches your file system and automatically update the collections (and rebuilds any file that depends on it) when something changes.

Once you get the hang of this, constructing any content architecture you might need for your website is pretty straightforward. If something can be built statically, Middleman can be made to build it for you.

There’s also support for data files (YAML and JSON files stored in a <code>data/</code> folder), just like in recent versions of Jekyll.

### Extending Middleman

Middleman allows extension authors to hook into different points through a <strong>powerful API</strong>. This is not needed nearly as often as it is in Jekyll, though, because the freedom to create ad-hoc helper functions, filtered collections and new pages, along with a templating engine that allows ERB, means you can do a lot out of the box that would require an extension in many other generators.

<strong>Authoring Middleman extensions is not very straightforward</strong> or well documented. To really get going, dig into some existing extensions and figure out how it’s all done.

Once you get going, however, Middleman offers hooks into both the CLI and the content model. The official <a href="https://directory.middlemanapp.com">directory of extensions</a> lists a wide selection.

## Roots

Like Middleman, Roots comes from an agency that needed a static website generator for its client work. <em>Carrot</em>, based in New York and now part of the Vice media group, sponsors the development of Roots. Jeff Escalante of Carrot is the mastermind behind it.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c528e4c-3f79-4536-9d89-6db01883bdd9/roots-opt.png" alt="Roots" /><figcaption>Roots is based on Node.js.</figcaption></figure>

Whereas Middleman is like a static version of Ruby on Rails, Roots clearly <strong>comes from the world of Node.js-based front-end tools</strong>.

Roots is a lot <strong>more opinionated</strong> than Middleman, and it has obviously been tailored to make building websites with Carrot’s standard toolchain highly efficient.

### Templating Engine

Roots comes with support for the <a href="https://jade-lang.com/">Jade</a> templating engine out of the box. Jade heavily abbreviates HTML’s syntax, cutting all of the cruft from HTML, and it makes embedding JavaScript snippets in templates clean and simple. It looks quite different from normal HTML, so copying and pasting HTML snippets from elsewhere is harder because they’ll need to be rewritten first.

You can switch the templating engine to EJS, and supporting other options wouldn’t be hard, but because Carrot has settled on Jade for its internal toolchain, all guides, examples and so on assume that you’re using Jade.

### Asset Pipeline

Roots comes with a <strong>built-in asset pipeline tuned for CoffeeScript and Stylus</strong>. As with Jade for templates, you can make Roots handle other formats, but these two are what Carrot has built the workflow around, and if you go with Roots, you’ll probably have an easier time adopting the same workflow.

That being said, Roots’ asset pipeline is <strong>easily extensible</strong>. One great extension adds support for <a href="https://browserify.org/">Browserify</a>, a tool that makes it trivial to use any library distributed with npm in your front-end JavaScript. Roots’ asset pipeline also support multipass compilation. If a file is named <code>myfile.jade.ejs</code>, then it would be compiled with EJS first and then with Jade.

As an asset pipeline, Roots obviously doesn’t have the ecosystem you’d find around more general build tools, such as Grunt, Gulp and Brunch. However, if you don’t try to fight Roots and you adopt a workflow similar to Carrot’s, then you’ll find that it is very simple to set up and get going with, while being just powerful enough to work for most projects.

### Content Model

Out of the box, Roots doesn’t really have any preference for content models. It simply takes templates in a <code>views/</code> folder and turns them into HTML documents in the <code>public/</code> folder. Jade makes it easy to embed Markdown, but that’s about it:

<div class="break-out">

 <pre><code class="language-bash">extends layout

block content
   :markdown
      ## This Is Markdown

      Everything in this block will be parsed as Markdown and inserted in the content
      block within the layout.jade template.

</code></pre>
</div>

### Extending Roots

Roots <strong>doesn’t have any content model</strong> as such because it relies completely on extensions for all content, and those extensions come in many flavors.

The <a href="https://roots.cx/extensions">official directory</a> doesn’t list as many extensions as what you’ll find for Middleman or Jekyll, but off the bat you’ll notice several for dealing with different kinds of content.

There is the <a href="https://github.com/carrot/roots-dynamic-content">Roots Dynamic Content</a> extension, which gives you something similar to Jekyll’s collections with front matter and a Jade body. There’s also my own <a href="https://github.com/netlify/roots-posts">Roots Posts</a> extension, which adds collections in Markdown plus front matter, just like Jekyll.

The <a href="https://github.com/carrot/roots-records">Records</a> and <a href="https://github.com/carrot/roots-yaml">YAML</a> extensions add support for data files that can be pulled into any template. The former will even fetch data from any URL and make it available from the templates.

A similar extension is <a href="https://github.com/carrot/roots-contentful">Roots Contentful</a>, which Carrot blogged about in its article “<a href="https://carrot.is/coding/static_cms">Building a Static CMS</a>.” The extension pulls in content from Contentful’s API and lets you filter and iterate over it.

Getting started with writing Roots extensions is very easy, and the documentation has a really good introduction to <a href="https://roots.cx/docs/extensions">how the different hooks and compilation passes work</a>. More thorough documentation on the inner workings of Roots wouldn’t hurt, though.

Fortunately, there is a very active <a href="https://gitter.im/jenius/roots">Gitter chat room</a>, where both Jeff Escalante and other Roots contributors readily answer questions.

## Hugo

Hugo is a much more recent addition to the world of static website generators, having started just two years ago. It’s certainly growing the fastest in popularity at the moment.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31efd336-0388-4549-a5ac-dc1bc0c19312/hugo-opt.jpg" alt="Hugo" /><figcaption>Hugo is growing the fastest in popularity at the moment.</figcaption></figure>

Hugo is <strong>written in Go</strong>, which makes it the only really popular generator written in a statically compiled language. Most of its big advantages, and largest drawback, come from this fact.

Let’s start with the good. <strong>Hugo is fast!</strong> Not just fast as in, “This is pretty cool.” Fast as in, “Whoa! This feels like more than 1G acceleration!”

A great benchmark on YouTube <a href="https://www.youtube.com/watch?v=CdiDYZ51a2o">shows Hugo building 5000 pages in about 6 seconds</a>, and PieCrust2’s author, Ludovic Chabant, has a blog post that <a href="https://ludovic.chabant.com/devblog/2015/07/12/multi-core-piecrust-2/">puts these numbers into context</a>, showing Hugo generating a sample website about 75 times faster than Middleman.

Hugo is also <strong>incredibly simple to install and update</strong>. Ruby and Node.js are fine if you’ve already set up a development environment; otherwise, you’re in for a lot of pain. Not so with Hugo: Just download the binary for your platform and run it — no runtime dependencies or installation process. Want to update Hugo? Just download a new binary and you’re set.

### Templating Engine

Hugo uses the <a href="https://golang.org/pkg/html/template/">package template</a> (<code>html/template</code>) from Go’s standard library, but it also supports two alternative Go-based template engines, <a href="https://github.com/eknkc/amber">Amber</a> and <a href="https://github.com/yosssi/ace">Ace</a>.

The package <strong>template engine is similar to Liquid</strong> in that it allows a limited amount of logic in your templates. As with Liquid, this is both a blessing and a curse. It will make your templates simpler and usually cleaner, but obviously it makes you far more dependent on whatever functions the templating language provides.

Fortunately, Hugo provides a really well-conceived set of helper methods that make it easy to do custom filtering, sorting and conditionals.

There’s <strong>no concept of layouts</strong> in the package template as we see in Jekyll, Roots and Middleman — just partials.

Variables and functions are inserted via curly braces:

<pre><code class="language-markup">&lt;h1&gt;{{ .Site.Title }}&lt;/h1&gt;
</code></pre>

One really interesting aspect of the package template engine is that <strong>variable insertion is context-aware</strong>, so the engine will always escape the output according to the context you’re in. So, the same output would be escaped differently according to whether you’re in an HTML block, within the quotes of an HTML attribute or in a <code>&lt;script&gt;</code> tag.

### Asset Pipeline

This is one of Hugo’s big weaknesses. You’d better want to work with plain CSS and JavaScript, or integrate an external asset pipeline with a tool like Gulp or Grunt, because Hugo doesn’t include any kind of asset pipeline.

When Hugo builds your website, it copies any files in the <code>static</code> folder to your build directory, but that’s it. Want Sass, EcmaScript6, CSS auto-prefixing and so on? You’ll have to set up an external build tool and make Hugo part of a build process (which negates many of the advantages of having just one static binary to install).

Hugo does come with LiveReload built in. If you can do with no-frills CSS and JavaScript, that might be all you need.

### Extensions

Because Go is a statically compiled binary and Hugo is distributed as a single compiled file, there is <strong>no easy way to add a plugin</strong> or extension engine to Hugo.

This means you’ll need to rely exclusively on the features built into Hugo, rather than roll your own. In this way, Hugo is almost the exact opposite of Roots, which is almost nothing on its own without plugins.

Fortunately, Hugo comes with batteries included and packs a big punch out of the box. <strong>Shortcodes, dynamic data sources</strong>, menus, syntax highlighting and tables of contents are all built into Hugo, and the templating language has enough options to sort and filter content. So, a lot of the cases for which you would otherwise want plugins or custom helpers are already taken care of.

The closest you’ll come to an extensions engine in Hugo are the <strong>external helpers</strong>, which currently add support for the AsciiDoc and reStructuredText formats, in addition to Markdown. But there’s no real way for these external helpers to interact with Hugo’s templating engine or content model.

### Content Model

With the bad parts behind us — no asset pipeline, no extensions — let’s get back to the good stuff.

Hugo <strong>has the most powerful content model out of the box</strong> of any of the static website generators.

Content is grouped into sections with entries. Sections can be nested as a tree:

<pre><code class="language-bash">└── content
   ├── post
   |  ├── firstpost.md   // &lt;- https://1.com/post/firstpost/
   |  ├── happy
   |  |   └── ness.md  // &lt;- https://1.com/post/happy/ness/
   |  └── secondpost.md  // &lt;- https://1.com/post/secondpost/
   └── quote
      ├── first.md       // &lt;- https://1.com/quote/first/
      └── second.md      // &lt;- https://1.com/quote/second/
</code></pre>

Here, <code>post</code>, <code>post/happy</code> and <code>quote</code> would be sections, and all of the Markdown files would be entries. As with most other static website generators, entries may have meta data encoded as front matter. Hugo lets you write front matter in YAML, JSON or TOML.

Content from different sections can easily be pulled into templates, filtered and sorted. And the command-line tool makes it easy to set up boilerplates for different content types, to make writing posts, quotes and so on easy.

Here’s a condensed version of a short real-life snippet from <a href="https://www.staticwebtech.com">Static Web-Tech</a> that pulls in the three most recent entries from the “Presentations” section:

<div class="break-out">

 <pre><code class="language-markup">&lt;ul class="link-list recent-posts"&gt;
   {{ range first 3 (where .Site.Pages.ByDate "Section" "presentations")}}
   &lt;li&gt;
      &lt;a href="{{ .Permalink }}"&gt;{{ .Title }}&lt;/a&gt;
      &lt;span class="date"&gt;{{ .Params.presenter }}&lt;/span&gt;
   &lt;/li&gt;
   {{ end }}
&lt;/ul&gt;
</code></pre>
</div>

The <code>range</code> and <code>where</code> syntax with various filters takes a little getting used to. But once it clicks, it’s very powerful.

The same could be said for Hugo’s taxonomy, which <strong>adds support for both tags and categories</strong> (with their own pages — so, you could list all posts in a category, list all entries with a particular tag, etc.) and helpers for showing counts, listing all tags and so on.

Apart from this, Hugo can also get content from data files and load data dynamically from URLs during the build process.

## Modern Static Website Technology

While static websites have been around since the beginning of the Internet, modern static website generation is just getting started.

All of the generators reviewed above are <strong>powerful modern tools</strong> that have already been used by large agencies to develop big, complex websites. They are all under active development and will only get more powerful and more flexible.

The whole ecosystem around modern static website technology is growing rapidly, with an emerging array of external services for hosting, search, e-commerce, commenting and similar functionality. The limit of what you can achieve with a static website keeps getting pushed.

If you’re a beginner, one tricky question is simply <strong>where to start</strong>. The answer will generally depend on what programming language you’re familiar with and whether you’re more of a designer or a developer:

- **Jekyll** is a safe choice as long as you’re familiar with the whole Ruby toolchain and you use Mac or Linux. (Ruby’s ecosystem is not very Windows-friendly.)
- **Middleman** has broad appeal to anyone coming from the world of Rails. It’s geared to people who are comfortable writing Ruby, and it is a better fit than Jekyll for large websites with a lot of sections and a complex content configuration.
- **Roots** is great for front-end developers who are comfortable with JavaScript (or CoffeeScript) and want to build custom-designed websites.
- **Hugo** is great for content-driven websites, because it is completely dependency-free and is easy to get going. What it lacks for in extensibility, it largely makes up for with a good content model and super-fast build times.

Use, share, improve, enjoy. Welcome to modern static website technology!

### <span class="rh">Further Reading</span> on SmashingMag:

- [Using A Static Site Generator At Scale: Lessons Learned](https://www.smashingmagazine.com/2016/08/using-a-static-site-generator-at-scale-lessons-learned/)
- [Build A Blog With Jekyll And GitHub Pages](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/)
- [Content Modeling With Jekyll](https://www.smashingmagazine.com/2016/02/content-modeling-with-jekyll/)
- [Creating Websites With Dropbox-Powered Hosting Tools](https://www.smashingmagazine.com/2016/09/creating-websites-with-dropbox-powered-hosting-tools/)

{{< signature "ml, al, jb" >}}

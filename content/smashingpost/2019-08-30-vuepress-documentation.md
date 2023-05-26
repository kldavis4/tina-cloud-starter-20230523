---
title: 'VuePress: Documentation Made Easy'
slug: vuepress-documentation
author: ben-hong
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67910108-f27f-4a4f-a3c1-02bc55a78a4e/4-vuepress-custom-containers.png
date: 2019-08-30T13:00:59+02:00
summary: >-
  One of the most overlooked aspects of creating and/or maintaining any software library is good documentation. Luckily for you, a new tool on the market is here to make  it easy for you to create great documentation for your projects.
description: >-
  One of the most overlooked aspects of creating and/or maintaining any software library is good documentation. Luckily for you, a new tool on the market is here to make  it easy for you to create great documentation for your projects.
categories:
  - Vue
  - Tools
  - Workflow
---
When it comes to any project that requires any user interaction (e.g., end users, maintainers, etc.), there is one critical factor that makes the difference between success and failure: good documentation. This holds true regardless of how small or large your project is. After all, short of providing one-on-one support for your project, documentation is the first line of defense for users who are trying to solve a problem. And whether you like it or not, you will never hear from users who give up after being unable to solve their problem due to inadequate documentation.

## The Challenges Of Creating Good Documentation

When it comes to writing good documentation, there are four recurring issues that teams often encounter:

<ol>
	<li><strong>Documentation is often out of date.</strong><br />While no documentation for a project can be a frustrating experience, it is arguably worse to have <em>outdated</em> documentation. After all, the purpose of having documentation is to provide users with an official body of knowledge that they can rely on. When it is out of date, users are wasting their time and ultimately losing trust in your product.<br /><br />The primary reason that documentation becomes outdated is that <em>documentation maintenance is separate from code changes</em>. Without investing significant time and energy, this can be difficult to solve because:<br />
	<ol>
		<li>Documentation usually lives in a third-party service like Confluence or a Wiki,</li>
		<li>Developers are typically more interested in writing code than documentation.</li>
	</ol>
	<li><strong>Users are unable to easily provide feedback.</strong><br />No matter how good you think your documentation is, it is ultimately meaningless without testing it with real users who can provide feedback. As mentioned earlier, a common bias when evaluating the effectiveness of things like documentation is failing to account for users who were unable to solve their problems and gave up. Since no team would ever be able to account for every scenario of how users might use your product, users must have an easy and reliable way to give feedback.</li>
	<li><strong>Documentation is often written for by power users for power users.</strong><br />The flaw with using standard tools like wikis or README files is that they often only cater to a specific set of users who often have a pre-existing knowledge of the library and/or technology stack. As a result, it is fairly simple for them to navigate the space and find what they need. However, new users lack this prior knowledge and thus often require a much more immersive experience to engage them.<br /><br />Examples of this include:<br />
		<ul>
			<li>A well-designed website,</li>
			<li>Search capability,</li>
			<li>Guided side navigation,</li>
			<li>Easily identifiable meta information (i.e., last updated date),</li>
			<li>Immersive content that extends beyond a wall of text that is difficult to easily comprehend.</li>
		</ul>
	</li>
	<li><strong>Poor infrastructure that makes documentation difficult to maintain.</strong><br />As if writing good documentation that users can understand is not difficult enough, the ease in which a developer can write and/or maintain documentation is critical to its long term viability. So, for every additional barrier that developers must deal with to write and/or maintain documentation, the more likely it is that it will ultimately fail. As a result, it is critical that the authoring experience and maintenance of any documentation be as seamless and engaging as possible.</li>
</li>
</ol>

If only there was a tool that could do all of these things for us...

{{% feature-panel %}}

## Enter VuePress

When first hearing of VuePress, one might be tempted to guess that it is an amalgamation of Vue.js and WordPress. Instead, you should think of VuePress as:

<blockquote>Vue.js + Printing Press</blockquote>

Because when all is said and done, VuePress is a static site generator!

Some of you might be thinking, “Wait. Another static site generator? What’s the big deal?”

While there are a number of tools that are static site generators, VuePress stands out from amongst the pack for a single reason: its primary directive is to make it easier for developers to create and maintain great documentation for their projects.

## Why Is VuePress So Powerful For Creating Documentation?

The answer is simple. It was designed with one goal in mind: to help developers create great documentation sites while maintaining a fun authoring experience. This means that it provides a framework for developers to:

- Create beautiful documentation sites,
- Come with pre-built features essential to all documentation sites,
- Optimize the authoring experience to make it as simple as updating a Markdown file.

### VuePress Can Co-Exist With Your Existing Codebase

This is one of the main reasons why I strongly recommend it. When it comes to maintaining documentation, one way to guarantee it will go out of date is to make it difficult for developers to update docs when writing code. If you make the authoring experience difficult by forcing developers to update things in two different places, this will cause a lot of friction and often results in documentation getting left to the wayside. This is commonly seen when developers have to maintain a third party tool like a wiki, in addition to the codebase itself.

Because it is a static site generator, this means that it can live in the same exact repo as your code.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c5dd5ad-3bf5-438a-8b33-5951ac864773/00-directory.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c286597-cbd6-4ad2-a5a8-c489958b6d35/00-vuepress-directory.png" sizes="100vw" caption="A sample application with VuePress docs existing next to a Vue CLI scaffolded app (<a href=''>Large preview</a>)" alt="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c5dd5ad-3bf5-438a-8b33-5951ac864773/00-directory.png" >}}

As you can see in this sample web app structure, your code would live in the `src` directory as normal, but you would simply have a `docs` directory to contain all of your documentation. This means you get the benefits of:

- All documentation is now version controlled;
- Pull requests can now contain both documentation and code changes;
- Creating separate scripts for running local instances of your code and docs at the same time;
- Utilize build pipelines to determine whether new documentation site deployments go in sync with code deployments or not.

### The Default Theme Comes With Standard Configuration

Writing documentation is hard enough as it is, so VuePress offloads a lot of the decisions that one normally has to make and has a bunch of built-in defaults to make your authoring experience easy:

- **Writing content is done primarily with Markdown.**  
This means that you can leverage your existing knowledge of Markdown syntax to style and format your text.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33ac9288-b973-47f8-865c-73fc52e48b82/01-markdown-example.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33ac9288-b973-47f8-865c-73fc52e48b82/01-markdown-example.png" sizes="100vw" caption="An example of how the Markdown is rendered in VuePress (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33ac9288-b973-47f8-865c-73fc52e48b82/01-markdown-example.png'>Large preview</a>)" alt="An example of how the Markdown is rendered in VuePress" >}}

- **Code syntax highlighting.**  
If you were building a site all on your own, you would need to wrestle with color syntax highlighting libraries. But you’re in luck because you can add code blocks in VuePress is so easy since everything is ready to go with zero configuration.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/271507da-9ebf-44fd-aed8-1bbbbbb73483/02-code-block-example.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/271507da-9ebf-44fd-aed8-1bbbbbb73483/02-code-block-example.png" sizes="100vw" caption="An example of how code block samples render in VuePress (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/271507da-9ebf-44fd-aed8-1bbbbbb73483/02-code-block-example.png'>Large preview</a>)" alt="An example of how code block samples render in VuePress" >}}

- **Front matter for defining page-level meta data.**  
Even though you’re authoring in a Markdown file, you can use front matter (like YAML, JSON, or TOML) to define metadata for your page to make it even easier to manage your content!

<pre><code class="language-yaml">---
title: Document Like a Pro
lang: en-US
description: Advice for best practices
tags:
  - documentation
  - best practices
---
</code></pre>

- **Custom Markdown containers.**  
In case you didn’t know, Markdown has extensions to add even more useful shortcuts to create beautiful UI components like custom containers. And since they are so useful in documentation, VuePress has already configured it so you can use it right out of the box:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d23c31b9-daec-4b01-a759-c6c76101a094/04-custom-containers.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d23c31b9-daec-4b01-a759-c6c76101a094/04-custom-containers.png" sizes="100vw" caption="A demonstration of custom containers rendered in VuePress (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d23c31b9-daec-4b01-a759-c6c76101a094/04-custom-containers.png'>Large preview</a>)" alt="A demonstration of custom containers rendered in VuePress" >}}

### Built-In Search Functionality

Let’s face it. No matter how much time we spend writing great documentation, it will ultimately amount to being useless if the users can’t find it. There are generally two approaches to this:

1. Wait for search engine robots to slowly crawl your site in hopes that one day your users will be able to find the right page on your site. Not a great solution.
2. Build your own search functionality, but this can be difficult to implement for static sites as there’s no server-side code running to create search indexes and perform the lookups. Not to mention this is taking development time away from the product itself. So this isn’t great either.

Luckily for us, VuePress is here to save the day once again!

{{% ad-panel-leaderboard %}}

VuePress comes with a built-in search functionality that generates its own “search engine” &mdash; you read that right. Without any additional database setup or configuration, VuePress is setup to scrape your entire docs to generate a simple search engine that will surface all of your h1s and h2s to your user. 

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/590f1e65-813d-41d8-9011-94450d66a2d4/05-basic-search.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c6baa3d-924f-4744-920e-2fcdcd06317f/05-basic-search-800w.gif" width="800" height="450" alt="An example of basic searching in VuePress’ default theme" /></a><figcaption>An example of basic searching in VuePress’ default theme (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/590f1e65-813d-41d8-9011-94450d66a2d4/05-basic-search.gif">Large preview</a>)</figcaption></figure>

Now, some of you may be thinking,

<blockquote>“What if I want something that will provide lower-level indexing for searching?”</blockquote>

Well, VuePress has got you covered there too because it is designed to easily integrate with [Algolia DocSearch](https://community.algolia.com/docsearch/) which can provide that functionality to you for free if you meet their requirements: 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ce36180-66d8-4945-b700-0b86c9c1f224/06-algolia.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ce36180-66d8-4945-b700-0b86c9c1f224/06-algolia.png" sizes="100vw" caption="An example of Algolia DocSearch in action (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ce36180-66d8-4945-b700-0b86c9c1f224/06-algolia.png'>Large preview</a>)" alt="An example of Algolia DocSearch in action" >}}

### Sidebar Navigation Is As Simple As Toggling The Feature On Or Off

For anyone who has ever been responsible for managing content, you know how complicated it can be to built a sidebar that has nested items and then track what position the reader is on while scrolling down. So, why spend the time on that when you could be writing better docs? With VuePress, the sidebar is as simple as toggling on the front matter for a page:

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c5c4e64-01ab-4249-9f77-c2d76a39bbb8/07-sidebar-nav.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f112a86-18d2-4e0c-819b-39b7f03337fd/07-sidebar-nav-800w.gif" width="800" height="450" alt="A demo of how the sidebar can be automatically generated through headings" /></a><figcaption>A demo of how the sidebar can be automatically generated through headings (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c5c4e64-01ab-4249-9f77-c2d76a39bbb8/07-sidebar-nav.gif">Large preview</a>)</figcaption></figure>

### Automatic Generation Of Important Meta-Data That’s Commonly Overlooked

One of the most frustrating things that a user can encounter is out-of-date documentation. When a user follows the steps and has trouble understanding why something doesn’t work, being able to easily find out the last updated date can be incredibly useful to both the user and maintainers of the project. 

With a simple configuration, VuePress can ensure automatically output the last updated date on the page so your users always know the last time it was updated.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95fcb15e-f225-4340-ac8a-85d26cd26aad/08-last-updated.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28aed3a8-8f0e-4c1e-b867-c4536f108f4b/08-last-updated-800w.gif" width="800" height="450" alt="A screenshot to show the ‘Last Updated’ metadata field" /></a><figcaption>A screenshot to show the ‘Last Updated’ metadata field (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95fcb15e-f225-4340-ac8a-85d26cd26aad/08-last-updated.gif">Large preview</a>)</figcaption></figure>

On top of that, with a little bit of configuration, VuePress also makes it incredibly easy for users to contribute to your docs by automatically generating a link at the bottom of every single page that allows users to easily create a pull request to your docs. 

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b694d0e-d725-4be5-ac1b-766cf571a078/09-edit-on-this-page.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca898a31-7d0c-4283-8793-78e6d69b5577/09-edit-on-this-page-800w.gif" width="800" height="450" alt="A demo of an automatically generated ‘Edit’ link which allows users to easily submit PRs to the docs" /></a><figcaption>A demo of an automatically generated ‘Edit’ link which allows users to easily submit PRs to the docs (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b694d0e-d725-4be5-ac1b-766cf571a078/09-edit-on-this-page.gif">Large preview</a>)</figcaption></figure>

It doesn’t get much easier than that for your users.

### Deployment On Any Static Hosting Site

Since VuePress is a static site generator at its core, this means that you can deploy it on any popular hosting platform such as:

- Netlify
- GitHub Pages
- GitLab Pages
- Heroku
- Now

All you need to do to build the site is run `vuepress build {{ docsDir }}` with where your directory lives and you’ll have everything you need to deploy it live on the web!

**Note**: *For more in-depth guides on how to do this, check out the [official deployment guides for VuePress](https://v1.vuepress.vuejs.org/guide/deploy.html#deploying).*

{{% ad-panel-leaderboard %}}

### Leveraging Vue Inside Your Markdown File

I know, I know. We can use Vue.js in our Markdown?! Yes, you read that right! While technically optional, this is probably one of the most exciting aspects of VuePress because it allows you to enhance your Markdown content like you’ve never been able to do before.

#### Define Repetitive Data In One Place And Have It Update Everywhere With Interpolation

In the example below, you’ll see a brief example of how you can leverage local variables (like the ones define in the frontmatter) as well as globally defined ones (like the site title):

<div class="break-out">

<pre><code class="language-javascript">---
title: My Page Title
author: Ben Hong
---

# {{ $page.title }}

Welcome to {{ $site.title }}! My name is {{ $page.author }} and I'll be your guide for today!
</code></pre>
</div>

#### Use Vue Components Within Markdown

I’ll give you a moment to collect yourself after reading this, but yes, live Vue components with a full Vue instance can be yours for the taking if you want! It will take a little bit more work to configure, but this is to be expected since you are creating custom content that will be running in your documentation. 

Here is a quick example of what a Counter component would look like in a Markdown file:

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79389e71-3949-40c3-8f2c-d2664fc9bc0b/10-counter.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b231d99a-e6cc-48be-90f8-c93d2d787c61/10-counter-800w.gif" width="800" height="450" alt="A demo of using Vue Components within Markdown" /></a><figcaption>A demo of using Vue Components within Markdown (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79389e71-3949-40c3-8f2c-d2664fc9bc0b/10-counter.gif">Large preview</a>)</figcaption></figure>

This is perhaps the most powerful part of customization available to documentation since it means you now have the freedom to create custom content extends far beyond the abilities of standard Markdown. So whether it’s providing a demo, or some interactive code, the ideas are endless!

## Next Steps

If you want to set up a beautiful documentation site for your users to learn how to use your product, it doesn’t get much easier than VuePress. And even though it might be easy to assume that VuePress should only be used by projects that use Vue.js, this could not be further from the truth. Here are just some examples of the different types of projects leveraging VuePress for their documentation sites:

- [Craft CMS](https://docs.craftcms.com/v3/)
- [UmiJS](https://umijs.org/) (which is built for React)
- [openHAB](https://www.openhab.org/docs/)
- [Peacock](https://papapeacockstorage.z13.web.core.windows.net/)

At the end of the day, regardless of whether you use VuePress or not, I hope this has helped to inspire you to create better documentation for your users. 

### Further Resources

There are many cool things that I did not cover here in this article (e.g. theming, blogging, and so on), but if you would like to learn more, check out these resources:

- [Official VuePress Docs](https://v1.vuepress.vuejs.org/)
- [A Curated List of VuePress Related Resources](https://github.com/ulivz/awesome-vuepress)
- [VuePress Gallery](https://vuepress.gallery/)
- [VuePress Blog Boilerplate](https://vuepress-blog-boilerplate.bencodezen.io/)

{{< signature "dm, yk, il" >}}

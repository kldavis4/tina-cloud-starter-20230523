---
title: 'Jamstack CMS: The Past, The Present and The Future'
slug: history-future-jamstack-cms
author: mikeneumegen
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2f37c71-d2c5-4634-b62c-2dc2eea127c1/history-future-jamstack-cms.jpg
date: 2021-08-20T08:00:00.000Z
summary: >-
  The story of Jamstack CMSs goes all the way back to the 90s. In this article, we take a trip down memory lane to see how we got to the modern Jamstack CMSs we have today, and where they’re heading in the next decade.
description: >-
  The story of Jamstack CMSs goes all the way back to the 90s. In this article, we take a trip down memory lane to see how we got to the modern Jamstack CMSs we have today, and where they’re heading in the next decade.
categories:
  - Jamstack
  - Headless
  - CMS
  - Static Generators
---

The world’s first website was made from static HTML files created in a text editor. While it looks unassuming, it laid the foundation for the web we have today. Fast-forward 30 years, and website technology has changed significantly &mdash; we have images, stylesheets, JavaScript, streaming video, AJAX, animation, WebSockets, WebGL, rounded corners in CSS — the list goes on.

Sir Tim Berners-Lee couldn’t have possibly imagined the weird and wonderful place the world wide web would become and how deeply it would become part of our everyday lives. Yet, for all these technological developments, it’s interesting that many of us are still serving sites in the same way Tim did with the very first website &mdash; a **web server serving static website files**.

Throughout the web’s history, static websites have always been a popular option due to their simplicity, scalability, and security. However, unlike the early days of the web, static sites are no longer limited to developers working in a code editor. Now there’s a massive range of Jamstack CMSs available, which bring all the advantages of static sites while allowing non-technical folk to update content.

Over the years, there have been many **different approaches and evolutions** of static and Jamstack CMSs. In this post, we’re taking a stroll down memory lane to look at the CMSs that gave rise to the Jamstack CMSs we have today and peek beyond the horizon of what’s next.

## The 90s

During the 90s, we saw two content management systems for static sites &mdash; Microsoft **FrontPage** in 1996 and Macromedia **Dreamweaver** in 1997. I vividly remember receiving a PC Magazine for my birthday with a trial of Dreamweaver. Piecing together a website using a WYSIWYG editor and seeing the code it generated was a fascinating and educational experience that sparked an initial interest in web design.

These desktop applications incremented the tooling an inch closer to the modern Jamstack content management systems of today. The idea of **drag’n’dropping website components** while still having control of the HTML was groundbreaking at the time.

Maintaining layouts became a particular pain point for static sites. For example, let’s say you had a website and wanted to change your navigation. You would need to make that change on every page. At this point, dynamically generated websites had already solved this problem with includes.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf2365a-7eb1-41f3-beda-ede559259e1d/3-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf2365a-7eb1-41f3-beda-ede559259e1d/3-history-future-jamstack-cms.png" width="800" height="451" sizes="100vw" caption="Table template in Dreamweaver 1.2 released 1998. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf2365a-7eb1-41f3-beda-ede559259e1d/3-history-future-jamstack-cms.png'>Large preview</a>)" alt="Table template in Dreamweaver 1.2 released 1998" >}}

Dreamweaver 4 introduced **editable regions**, which was the first foray into separating content from the layout on a static website. Now you could manage larger sites and even hand off content editing to someone else without worrying about them breaking the rest of the site.

The bridge between local development and deployment was also a pain point Dreamweaver began to address with **integrated FTP**. I remember the struggle of getting my FTP configuration exactly correct in Dreamweaver for the free, advertising-ridden hosting I’d found. But, when it worked, it was magical. I had my website with funny photos and links to favorite websites live on the internet, and better yet, I could edit directly on the server.

{{% feature-panel %}}

## The 00s

In the 2000s we had a showdown of two popular blog publishing platforms &mdash; **MovableType** in 2001 and **WordPress** in 2003. It was a battle of not only proprietary vs open source but also static vs dynamic. It’s safe to say WordPress, the platform now powering 40% of the internet, won that battle, but MovableType paved the way for Jamstack CMSs in the future.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/374e9c40-f1fd-4614-90eb-08f5a1db5ce5/8-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/374e9c40-f1fd-4614-90eb-08f5a1db5ce5/8-history-future-jamstack-cms.png" width="633" height="970" sizes="100vw" caption="Editing a blog post in MovableType 2.0 released 2002 (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/374e9c40-f1fd-4614-90eb-08f5a1db5ce5/8-history-future-jamstack-cms.png'>Large preview</a>)" alt="Editing a blog post in MovableType 2.0 released 2002." >}}

MovableType was one of the **first static site generators** on the market, although that term wouldn’t become popular until 2008. Ben and Mena Trott created MovableType because of a "Dissatisfacion with existing blog CMSes &mdash; performance, stability." To this day, these two points are common reasons for switching from a dynamic site to a static one.

What’s interesting is there was little mention of static sites in MoveableType’s documentation at all. Instead, they would talk about "rebuilding" the site after any changes. I imagine they wanted to avoid the limiting perception of the word 'static.' It’s the same problem that led the community to adopt the term 'Jamstack.'

Before MovableType, other personal blogging platforms were available such as **Geocities**, Blogger & Open Diary. However, MovableType was one of the first widely available platforms you could download for free and host yourself. In addition, they introduced a hosted version of MovableType in 2003 called TypePad to compete with other popular cloud platforms.

With MovableType, you had everything you needed to manage your blog. You could create and update blog posts, all content was straight HTML &mdash; open-source WYSIWYG editors weren’t available at the time, and Markdown didn’t come about until 2004.

We can see all the **bones of modern Jamstack CMSs** here. MovableType really was before its time.

In 2006, Denis Defreyne tried to set up a Ruby-based blog platform and ran into performance problems &mdash; "Having a VPS with only 96 MB of RAM, any Ruby-based CMS ran _extremely_ slowly." One year later, Denis launches [Nanoc](https://github.com/nanoc/nanoc), a static site generator that simplifies MovableType’s model. Nanoc removed the UI and is instead a program you run on the command line.

As far as I can tell, this is the **first modern static site generator**, although we’re still a year away from coining that term. At the time, Nanoc talked about compiling source files into HTML:

<blockquote>It operates on local files, and therefore does not run on the server. nanoc "compiles" the local source files into HTML by evaluating eRuby, Markdown, etc.</blockquote>

Nanoc had many static site generator (SSG) features we now take for granted:

* **Layouts**  
Create layout elements using Ruby’s ERB templating language.
* **Page Metadata**  
A separate YAML file for storing title and other metadata for a page. Front matter wasn’t a thing yet.
* **Markdown support**  
Write content in Markdown and transform it into HTML on build.
* **Templates**  
A feature similar to Hugo’s archetypes.
* **Plugins**  
Known as libs; extend the static site generator for your own needs.

By the end of 2008, Tom Preston-Werner announces [Jekyll](https://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html) &mdash; a simple, blog-aware, static site generator. It took ideas from Nanoc and pushed them even further with two significant innovations:

* **Front matter**  
Instead of metadata living in a separate file, now you can have a small YAML snippet at the top of a file.
* **Blog aware**  
Create posts with Markdown files. Jekyll builds these into an array you can iterate over and paginate to create a blog.

Both Nanoc and Jekyll **revolutionized the future of static site tooling** in their own way. First, Nanoc introduced having a site’s configuration, layouts, and content as static files. The benefit of doing this is the entire site’s source code can live in Git. Jekyll took this a step further by providing more structure around the content. Now you could use GitHub as your CMS. Adding a new blog post is as simple as creating a new Markdown file in GitHub, writing your content, and committing.

{{% ad-panel-leaderboard %}}

## The 10s

In 2012, Dave Cole published a post on [How we build CMS free websites](https://developmentseed.org/blog/2012-07-27-how-we-build-cms-free-websites). The post details how Development Seed moved their websites from Drupal to Jekyll and how they use[ Prose.io](https://Prose.io) to manage the content. Development Seed built[ Prose.io](https://Prose.io) to make it easier for content writers to contribute to Jekyll websites.

[Prose.io](https://Prose.io) **syncs with your GitHub repository** and provides a simple GUI for everyday content tasks such as updating front matter, writing Markdown, creating posts, and uploading files. In addition, content updates save back to GitHub, creating a tight workflow between developers and content writers.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f08d6861-401b-482c-8b78-c271c631854e/2-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba720076-8ac8-492f-9749-bd0d42ad6655/cms-preview.png" width="764" height="526" sizes="100vw" caption="Updating a blog post on Prose.io (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f08d6861-401b-482c-8b78-c271c631854e/2-history-future-jamstack-cms.png'>Large preview</a>)" alt="Updating a blog post on Prose.io" >}}

Prose turned Jekyll from a tool for developers to create blogs to a powerful **content publishing platform**. Moreover, it sparked a decade of companies pushing static site generator content publishing to the next level.

There are now [hundreds of modern Jamstack CMSs](https://jamstack.org/headless-cms/) to choose from, each with its own benefits and trade-offs. Jamstack CMSs typically take one of three approaches to manage content on a static website:

{{% ad-panel-leaderboard %}}

### SSG/CMS package

Hailing back to MovableType, these platforms manage content and render the static site themselves. Controlling the whole stack means these CMSs can provide a **tightly integrated experience**. Expect live previews, straightforward setup, and strong conventions.

The downside of the SSG/CMS package is they’re bundled together. You might love the editing experience but loathe the website generation portion. It’s worth noting that you can throw away the SSG portion on some of these platforms and only use it solely as a Content API.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c718cf5a-4a59-4e7f-be16-9c1efbc5b478/1-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c718cf5a-4a59-4e7f-be16-9c1efbc5b478/1-history-future-jamstack-cms.png" width="800" height="510" sizes="100vw" caption="Updating a rich content collection with Statmatic (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c718cf5a-4a59-4e7f-be16-9c1efbc5b478/1-history-future-jamstack-cms.png'>Large preview</a>)" alt="Updating a rich content collection with Statmatic" >}}

Examples: [Statamic](https://statamic.com/), [Publii](https://getpublii.com/), [WordPress](https://wordpress.org/) (with [Simply Static plugin](https://wordpress.org/plugins/simply-static/)).

### Content API

These platforms provide content as a service. They offer many different field types you can use to **piece together the content** for your pages. On top of that, Content API platforms provide sophisticated APIs to retrieve the content.

When you run an SSG build, you download the content from the content API and interact with it like you would a data file. The nice thing about content APIs is you can reuse content across many different digital experiences. In addition to that, you can manage massive amounts of content and have deep relationships between pieces of content.

The downside is your **content lives on a third party**, so you’re at their mercy for any downtime, API changes, or how you interact with your content. Finally, as the editing interface is abstract from the end use-case of the content, there can be a disconnect between the fields in the Content API vs what you see rendered on a web page.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/348cbb5d-5ffe-43f0-a2c8-0841ae47b2d9/9-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/348cbb5d-5ffe-43f0-a2c8-0841ae47b2d9/9-history-future-jamstack-cms.png" width="800" height="505" sizes="100vw" caption="Updating content with the entry editor on Contentful (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/348cbb5d-5ffe-43f0-a2c8-0841ae47b2d9/9-history-future-jamstack-cms.png'>Large preview</a>)" alt="Updating content with the entry editor on Contentful" >}}

Examples: [Contentful](https://www.contentful.com/), [Prismic](https://prismic.io/), [Strapi](https://strapi.io/).

### Git-Based CMS

These platforms take a similar approach to[ Prose.io](https://Prose.io). You connect your Git repository, they pull in your website files and create an editing interface around them. When you save changes, the files push back to your repository. The benefit of this approach is your Git repository holds your entire site and all its content.

Git based CMSs bring all the power of **Git workflows** to non-technical content writers. The downside is everything lives in your repository, so if you want to reuse content across multiple digital experiences, you would need to build JSON endpoints on your static site. Hosted repositories also have an upper limit of &#126;2GB, so you may need to use a 3rd party service for media if you have many assets.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/516c7909-33f7-4c57-9564-e6149081a248/4-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/516c7909-33f7-4c57-9564-e6149081a248/4-history-future-jamstack-cms.png" width="800" height="467" sizes="100vw" caption="Updating a blog post with the visual editor in CloudCannon. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/516c7909-33f7-4c57-9564-e6149081a248/4-history-future-jamstack-cms.png'>Large preview</a>)" alt="Updating a blog post with the visual editor in CloudCannon" >}}

Examples: [CloudCannon](https://cloudcannon.com/) (disclaimer: I’m the co-founder), [Netlify CMS](https://www.netlifycms.org/), [Tina](https://tina.io/)

## Where are Jamstack CMSs today?

SSGs were originally tools for developers to build personal blogs. It was a simple approach that gave developers complete control, but you needed a basic understanding of web development to contribute to the sites. Over the past decade, [the rapid evolution of Jamstack](https://www.smashingmagazine.com/2021/05/evolution-jamstack/) and the Jamstack CMS has helped propel Jamstack into **mainstream use cases**. These use cases include:

### Documentation

Developers expect a lot from documentation sites, and a good experience will help win them over. Jamstack puts you on the right track to creating documentation sites developers love:

1. **Development is rapid**, and there’s more time for polish. 
2. **Markdown** is an excellent format for Documentation made even easier with a good CMS.
3. The site will load in a snap.
4. The site content **lives in a repository** which allows the developer community to suggest improvements.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df9931c1-8261-4fe7-9419-77e47112d287/6-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df9931c1-8261-4fe7-9419-77e47112d287/6-history-future-jamstack-cms.png" width="800" height="500" sizes="100vw" caption="Twitch developer documentation hosted on AWS, edited on CloudCannon. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df9931c1-8261-4fe7-9419-77e47112d287/6-history-future-jamstack-cms.png'>Large preview</a>)" alt="Twitch developer documentation hosted on AWS, edited on CloudCannon." >}}

Companies including [Twitch](https://dev.twitch.tv/docs/), [Rackspace](https://docs.rackspace.com/docs), and [Linode](https://www.linode.com/docs/) are reaping the benefits of Jamstack for their documentation websites. 

### eCommerce

Visitors to an eCommerce site are on a path to paying money. Slow loading times or worse, downtime can make them look elsewhere. Platforms such as [Snipcart](https://snipcart.com/), [CommerceLayer](https://commercelayer.io/), [headless Shopify](https://www.shopify.com/plus/solutions/headless-commerce), and [Stripe](https://stripe.com/) enable you to manage products in a friendly UI while taking advantage of the benefits of Jamstack:

1. [Amazon’s famous study](https://www.gigaspaces.com/blog/amazon-found-every-100ms-of-latency-cost-them-1-in-sales) reported that for every 100ms in latency, they lose 1% of sales. Jamstack sites are typically among the fastest on the web.
2. When an eCommerce site has downtime, it can’t generate sales. There are far fewer moving parts in a Jamstack site, making them easier to keep online.
3. eCommerce sites are consistently iterating to improve conversion rates. Developer experience is at the heart of Jamstack, allowing developers to make and publish changes quickly.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebbdf580-cf11-4d5d-85b6-ffc7e66da064/12-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebbdf580-cf11-4d5d-85b6-ffc7e66da064/12-history-future-jamstack-cms.png" width="800" height="500" sizes="100vw" caption="Victoria Beckham Beauty powered by Shopify and Netlify. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebbdf580-cf11-4d5d-85b6-ffc7e66da064/12-history-future-jamstack-cms.png'>Large preview</a>)" alt="Victoria Beckham Beauty powered by Shopify and Netlify." >}}

[Victoria Beckham Beauty](https://www.victoriabeckhambeauty.com/), [Teespring](https://teespring.com/), and [Louis Vuitton](https://us.louisvuitton.com) are all using Jamstack to boost their eCommerce experience.

### Corporate websites

Corporate websites are the online front door to a company. Making a good impression with a fast-loading, well-constructed website can give an edge over competitors. Many of the Jamstack CMSs we’ve mentioned have the features and workflows growing enterprises require. These include translations, **publishing workflows**, and complex content modeling.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2fce8d8-cfa1-4d53-9685-05c64bf0c58a/11-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2fce8d8-cfa1-4d53-9685-05c64bf0c58a/11-history-future-jamstack-cms.png" width="800" height="500" sizes="100vw" caption="Peloton powered by Contentful and Netlify. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2fce8d8-cfa1-4d53-9685-05c64bf0c58a/11-history-future-jamstack-cms.png'>Large preview</a>)" alt="Peloton powered by Contentful and Netlify" >}}

[Netflix](https://devices.netflix.com/), [Peloton](https://www.onepeloton.com/), and [Intercom](https://www.intercom.com/) iterate faster on their corporate websites thanks to Jamstack and Jamstack CMSs.

### Large scale blogs

Static site generators often get pigeonholed as a solution for small websites. Thanks to the build speed of static site generators like Hugo and modern Jamstack CMSs designed to handle vast amounts of content, even prominent blogs like [Smashing Magazine](https://www.smashingmagazine.com/2020/01/migration-from-wordpress-to-jamstack/), [web.dev](https://web.dev), and [JFK International Air Terminal](https://www.jfkt4.nyc/) can take advantage of a Jamstack approach.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33338cdd-b725-4953-bf50-dfd14db9d529/5-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33338cdd-b725-4953-bf50-dfd14db9d529/5-history-future-jamstack-cms.png" width="800" height="500" sizes="100vw" caption="Smashing Magazine powered by Netlify. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33338cdd-b725-4953-bf50-dfd14db9d529/5-history-future-jamstack-cms.png'>Large preview</a>)" alt="Smashing Magazine powered by Netlify" >}}

### Government

What better way to promote online transparency in government than having a website where the content lives in a **public repository**? There’s a complete history of all changes, and citizens can suggest improvements. You really can have a government website by the people, for the people.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/066b8d63-00e2-4150-a02e-e1732c9eed1f/7-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/066b8d63-00e2-4150-a02e-e1732c9eed1f/7-history-future-jamstack-cms.png" width="800" height="500" sizes="100vw" caption="CIO.gov powered by The Federalist (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/066b8d63-00e2-4150-a02e-e1732c9eed1f/7-history-future-jamstack-cms.png'>Large preview</a>)" alt="CIO.gov powered by The Federalist" >}}

[digital.gov](https://digital.gov/), [Singapore Together](https://www.singaporetogether.gov.sg/), and [CIO.gov](https://www.cio.gov/) all have pubic repositories on GitHub, which you can browse through every change made or suggest a content update. 

### Client websites

Websites for clients need to be exceptionally simple to update. Jamstack CMSs with a visual editor like [Storyblok](https://www.storyblok.com/), [CloudCannon](https://cloudcannon.com/) and [Tina](https://tina.io/) make it intuitive for non-technical clients to manage content on their Jamstack website.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9151f98a-8ebc-4996-ac05-7f67876b7337/10-history-future-jamstack-cms.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9151f98a-8ebc-4996-ac05-7f67876b7337/10-history-future-jamstack-cms.png" width="800" height="500" sizes="100vw" caption="Down Thyme Restaurant & Cafe powered by CloudCannon. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9151f98a-8ebc-4996-ac05-7f67876b7337/10-history-future-jamstack-cms.png'>Large preview</a>)" alt="Down Thyme Restaurant & Cafe powered by CloudCannon." >}}

[Wilto Makes Food](https://wiltomakesfood.com), [Down Thyme](https://www.downthyme.nz/), [The Bottle Room Bar](https://thebottleroombar.com/) take advantage of the same Jamstack approach that world-leading companies are.

## How Does The Modern Jamstack CMS Stack Up Against Other Popular CMSs?

At a high level, there are two ways of getting a website online:

1. You select a template, customize it to your brand and enter your content.
2. You work with a designer and developer to create a bespoke website.

Of course the template approach is cheaper. For under $100, you can get a high-quality theme/template and get your website online in minutes. It’s an excellent way for an individual or small business to get a website online.

A quality bespoke website is going to start at $1k and can easily get to $100k+. A unique website with custom functionality helps you stand out against a sea of millions of websites, something many companies are willing to pay for.

### Squarespace, Wix And Weebly

**Website builder platforms** focus on the template approach. They’re going for the mass market, and provide a way for anyone to spin up a website without a developer. 

There’s no question Jamstack is a developer-focused technology. When we talk about static site generators, incremental regeneration, or instant cache invalidation, it’s enough to make the layman’s eyes glaze over. I struggle to see a future where the local flower shop needs a website and chooses a Jamstack approach without developer involvement. 

Even with the most intuitive content management system for Jamstack where you can select a template, drag & drop components, and inline edit content, the benefits of Jamstack for this audience over website builders are too technical. Sure, it’ll be fast, secure, and easy to edit; however, the end-user couldn’t care less whether it’s using Jekyll, Hugo, Gatsby, or a dynamic backend.

The benefits of a fast-loading website, automated DevOps, higher uptime, and faster development cycles are much more seductive to companies building bespoke web projects. In this sense **I don’t see a lot of overlap between website builders and Jamstack** use cases.

### WordPress

WordPress has captured both workflows. Someone completely non-technical can piece together a template with various plugins and have their website online within a day. WordPress also has **rich APIs** that developers use to create unique, bespoke web experiences. This broad range of use cases has helped grow WordPress to power almost 40% of the internet.

In most articles about Jamstack, you’ll find a section that throws WordPress under the bus. There’s frequently talk about how WordPress is slow, insecure, and complicated. I believe it’s a more fundamental conversation of approach. We’re often talking about static vs. dynamic and monolith vs. decoupled. WordPress is the most popular CMS, so it’s often the target.

**There is no Jamstack vs. WordPress**. The truth is you can enjoy the benefits of Jamstack while using WordPress as your CMS. Hosting platforms like [Shifter](https://www.getshifter.io/) and [Strattic](https://www.strattic.com/) turn your WordPress site into a static website. You can also use a [plugin](https://wordpress.org/plugins/simply-static/) to output a static site or use [WordPress as a headless CMS](https://www.gatsbyjs.com/docs/glossary/headless-wordpress/) to populate content into a static site generator. 

It’s also relatively straightforward to [migrate from WordPress to a Jamstack CMS](https://www.smashingmagazine.com/2020/01/migration-from-wordpress-to-jamstack/). For a Git CMS you’ll want to migrate the blog posts and assets to Markdown files which live with your static site generator of choice. Fortunately, many SSGs [have](https://gohugo.io/tools/migrations/#wordpress) [import](https://import.jekyllrb.com/docs/wordpress/) [tools](https://hexo.io/docs/migration.html#WordPress) that make this easy. For a Content API CMS, some of them have a data import tool otherwise, you can always write a script to pull data from WordPress and save it to your Content API.

### Webflow

Webflow is a curious one because it allows designers to create bespoke websites without developers, but it’s too technical to be considered a website builder. It’s a robust platform that certainly overlaps with some Jamstack use cases. Ultimately **it’s going to come down to control**.

If your requirements fit within Webflow’s capabilities, it might be a good solution for you. While it can do a lot, it has limitations that a developer can surpass. If you need a developer, taking a Jamstack approach is one of the most efficient ways to leverage your staffing resources.

### Drupal

Drupal is not just a CMS. It’s a **powerful framework** that can solve even the most complex use cases, gearing it more towards bespoke solutions for enterprise problems rather than much smaller informational sites.

Modern Jamstack CMSs have plenty of successful case studies of these smaller websites. For the more complex enterprise use cases, we have fewer examples. There are some limitations Jamstack needs to overcome to compete with a sizeable Drupal install:

#### Build time

Prebuilding a site using a static site generator takes time. For a small site, a build might take a few seconds. A site with 100k pages could take upwards of an hour to build. Waiting an hour for your site to build after each change isn’t a viable development workflow.

Static site generators have several strategies to **address long build times**, including build caching, incremental builds, dynamic persistent rendering, and website sharding. The choice of tooling also has a significant impact on build time. For example, using a Golang based static site generator like Hugo can rapidly build large sites, whereas using something Ruby-based like Jekyll might struggle. 

We don’t have a silver bullet for build time yet, but the implementations of these strategies are improving all the time, which opens up possibilities for more extensive use cases. 

#### Dynamic functionality

Large, complex websites typically have some form of dynamic behavior. Forms, commenting, search, and custom API endpoints are all bread-and-butter for Drupal. For many developers, it’s not obvious how to do these on a Jamstack site. 

There’s a [huge ecosystem of tools that support Jamstack websites](https://cloudcannon.com/community/jamstack-ecosystem/) for everything from commenting solutions, search, contact forms, to even eCommerce. 

Perhaps you don’t want to use a third party, and you need a bespoke solution. You still have options with Jamstack:

1. You could build a separate API your Jamstack site interacts with for any dynamic functionality.
2. [Netlify](https://www.netlify.com/products/functions/), [Vercel](https://vercel.com/docs/serverless-functions/introduction), [CloudFlare](https://workers.cloudflare.com/), and [AWS](https://aws.amazon.com/lambda/edge/) all have the concept of serverless functions run at edge nodes of a CDN.

#### Fine-grained permissions

Drupal has a **rich and extendable permission system**. Large sites have large teams of content editors, which require a deep permission system.

We haven’t seen the same level of deep permission systems in a Jamstack CMS as is possible with Drupal, but it’s only a matter of time. It’s a chicken-egg situation. Without large content sites with extensive content teams, we don’t need complex permission systems. When we see more large content site adoption in Jamstack, Jamstack CMSs will introduce deep permission systems to match Drupal. 

## 20s And Beyond

Jamstack CMSs are on an exciting trajectory. However, there’s still a long road ahead to become a mainstream way for businesses to build websites. So, what are the problems we need to solve to have a broader appeal for Jamstack?

### Intuitive Content Editing

Platforms like Squarespace and Webflow are known for highly intuitive content editing experiences. What could be easier than writing content directly on your website? No guesswork or previews are necessary.

Content management for the Jamstack website has drifted towards a **disconnected approach**. You update content on a set of abstract field components that don’t represent how that content will look on the rendered site. The advantage of this disconnection is content reuse, but you’re sacrificing the editing experience to have this flexibility. There’s no reason we can’t have an editing experience similar to Squarespace on a Jamstack website. When we do, you’ll no longer have to make editing trade-offs to reap the benefits of Jamstack.

### Less Reliance On Developers

While developers are an essential part of the Jamstack, they’re often heavily involved in the content publishing process. For Jamstack to grow, **we need content tools that reduce this reliance**. Editors should be able to create, manage and publish content without a developer. We’re getting close to editors becoming completely self-reliant once a site is set up, but there’s still work to do.

### Better Publishing Workflows

Most CMSs have basic staging/production content workflows, which work fine for simple websites. Yet, these workflows quickly become an issue as soon as you have multiple contributors. It’s the equivalent of having a team of developers trying to work on a single branch.

Git has revolutionized how developers collaborate on content. We now have workflows where independent developers from around the world can come together and build extremely high-quality software. **These workflows are game-changing**, so why can’t we do the same thing for content? Jamstack sites are static. They live in a repository. With the right interface, we can bring these workflows to an entirely new audience pushing content collaboration far beyond what any CMS is capable of today.

Developers review pull requests using a code diff which indicates what code has changed. In the review process, you can have conversations about particular lines of code and iterate until it’s in a good spot to merge into the main code base. In addition to this, it’s common to run a suite of status checks as part of a pull request. Status checks are small programs to lint, run tests, or anything else you’d like to measure. Code diffs and status checks are crucial tools to review source code and ensure it’s consistent and high quality. So how do we take these ideas and bring them to content management?

**We can’t put code diffs in front of content editors**. The whole point of a Jamstack CMS is to abstract technical concepts. We can, however, show content diffs to indicate what content changed rather than the underlying source code. Visual diffs are another option and give you a different angle. Platforms like [Percy](https://percy.io/) are already doing this and give you a pixel-perfect view of what has changed between two web page versions.

As for static checking on content, we already have many tools available. There’s everything from checking for broken links, missing alt tags, SEO checks, grammar checks, and accessibility checking. We need friendly interfaces on top of these tools to help non-technical editors identify and solve issues themselves. Integrating these tools and workflows into Jamstack CMSs will change the way we manage content on the web.

## The Next Frontier Of Content Management

While the bones of Jamstack CMS’s have been around since the early 90s, it’s only in the past five years we’ve seen significant funding and resources propel the approach. We’re still in the **early adoption of Jamstack**, but I believe we’re nearing a tipping point.

The number of large-scale deployments of Jamstack by world-leading companies is growing by the day. As the tooling and platforms improve, I can only see this trend growing. It will be hard to justify **not** using Jamstack for a bespoke corporate website or application in the next decade.

Where do you think Jamstack CMSs will be in 2030?

{{< signature "vf, il" >}}

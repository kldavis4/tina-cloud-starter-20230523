---
title: Jekyll For Wordpress Developers
slug: jekyll-wordpress-developers
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42bcab40-cb00-4194-ad97-8d1a65c92afd/jekyll-for-wp-developers-opt.png
date: 2017-04-21T16:45:30.000Z
author: mikeneumegen
description: >-
  Jekyll is gaining popularity as a lightweight alternative to WordPress. It
  often gets pigeonholed as a tool developers use to build their personal blog.
  That’s just the tip of the iceberg — it’s capable of so much more!

  In this article, we’ll take on the role of a web developer building a website
  for a fictional law firm. WordPress is an obvious choice for a website like
  this, but is it the only tool we should consider? Let’s look at a completely
  different way of building a website, using Jekyll.
categories:
  - WordPress
  - Tools
  - Generators
  - Static Generators
  - Jekyll
---
In this article, we’ll take on the role of a web developer building a [website for a fictional law firm](https://grey-grouse.cloudvent.net/). WordPress is an obvious choice for a website like this, but is it the only tool we should consider? Let’s look at a completely different way of building a website, using Jekyll.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42bcab40-cb00-4194-ad97-8d1a65c92afd/jekyll-for-wp-developers-opt.png" width="500" height="375" alt="Jekyll For Wordpress Developers" /></figure>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Build A Blog With Jekyll And GitHub Pages](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/)
*   [Content Modeling With Jekyll](https://www.smashingmagazine.com/2016/02/content-modeling-with-jekyll/)
*   [Static Site Generators Reviewed: Jekyll, Middleman, Roots, Hugo](https://www.smashingmagazine.com/2015/11/static-website-generators-jekyll-middleman-roots-hugo-review/)
*   [Why Static Site Generators Are The Next Big Thing](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/)

{{% feature-panel %}}

## What Is Jekyll?

[Jekyll](https://jekyllrb.com/) is a static website generator. Instead of software and a database being installed on our server, a Jekyll website is simply a directory of files on our computer. When we run Jekyll on that directory, it generates a static website, which we upload to a hosting provider.</p>

## Why Jekyll?

We need to consider a number of tradeoffs when deciding whether Jekyll is right for a project.</p>

### Advantages of Jekyll

*   **Less complexity**  
    A Jekyll website is essentially a static website with a templating language. It has fewer components to create and maintain. On the server, we only need a web server capable of serving files.
*   **Speed**  
    When visitors view pages on Jekyll sites, the server returns existing files _without any extra processing_. This is much faster than WordPress, which generates pages dynamically at request time. Note: WordPress Caching plugins can eliminate this performance gap.
*   **Stability**  
    WordPress has more components working together to generate pages for visitors. If a component fails, visitors may not be able to view the website. Much less can go wrong when a web server is serving only files.
*   **Security**  
    Wordpress does a lot to mitigate security risks such as CSRF, XSS, or SQL injection attacks however it relies on you always having the latest updates. Statics sites eliminate this problem because there's no dynamic data storage a hacker can exploit.
*   **Source-controlled**  
    A Jekyll website is a directory of files, so we can store the entire website in a Git repository. Working with a repository gives us [many benefits](https://www.atlassian.com/git/tutorials/why-git/git-for-developers) (although [VersionPress](https://versionpress.net/) is in development and enables this workflow for WordPress).</p>

### Disadvantages of Jekyll

*   **No GUI**  
    A client can sign up to WordPress.com, choose a theme and set up a basic website by themselves. Jekyll is a command-line tool, which overwhelms most non-technical users. There are third-party GUIs for Jekyll, including [CloudCannon](https://cloudcannon.com/) (disclaimer: I’m the cofounder), [Forestry](https://forestry.io/), [Jekyll Admin](https://github.com/jekyll/jekyll-admin), [Netlify CMS](https://github.com/netlify/netlify-cms), [Prose](https://prose.io/) and [Siteleaf](https://www.siteleaf.com/). However, these need to be set up by the developer before being handed off to the client.
*   **Build time**  
    In our situation, this isn’t a problem because the website will build in under a second. However, a larger website with 10,000 to 100,000 posts could take minutes to build. This is frustrating when we’re developing because we have to wait for the website to build before previewing it in the browser.
*   **Themes**  
    Jekyll has some themes available, but it’s nothing compared to the thousands of themes available for WordPress.
*   **Extensibility**  
    If we need to add custom functionality to our WordPress website, we can write our own PHP. We can create custom Ruby plugins for Jekyll, however, these run at build time rather than request time.
*   **Support**  
    WordPress has a huge community of experts and other resources to help. Jekyll has similar resources but on a smaller scale.

Jekyll is a great tool for largely informational websites, like this project. If the project is more of an application, we could add dynamic elements using JavaScript, but at some point we would probably need a back end like WordPress’.</p>

## Implementation

WordPress and Jekyll take different approaches to building a website yet share a lot of functionality. Let’s get started building our Jekyll website.</p>

### Installing

A typical development environment for WordPress requires installation of Apache or NGINX, PHP and MySQL. Then, we would install WordPress and configure the web server.

For Jekyll, we need to make sure we have Ruby installed (sometimes this is harder than it sounds). Then we install the Jekyll gem:

<pre><code>gem install jekyll</code></pre>

If you're on macOS make sure you have Xcode developer installed first.

<pre><code>xcode-select --install</code></pre>

### Running

Running a WordPress site usually consists of starting the database and web server.

In Jekyll, we navigate to our site files (an empty directory at this point) in the terminal and run:

<pre><code>jekyll serve</code></pre>

This starts a local web server on port `4000` and rebuilds the site whenever a file changes.</p>

### Pages

It’s time to create our first page. Let’s start with the home page. Pages are for standalone content without an associated date. WordPress stores page content in the database.

In Jekyll, pages are HTML files. We’ll start with pure HTML and then add Jekyll features as they’re needed. Here’s `index.html` in its current state:

<pre><code class="language-html">
&lt;html&gt;
  &lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;link rel="stylesheet" href="/css/main.css"&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;div class="container"&gt;
      &lt;h1&gt;&lt;a href="/"&gt;Justice&lt;/a&gt;&lt;/h1&gt;
      &lt;nav&gt;
        &lt;ul&gt;
          &lt;li&gt;&lt;a href="/about/"&gt;About&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href="/services/"&gt;Services&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href="/contact/"&gt;Contact&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href="/advice/"&gt;Advice&lt;/a&gt;&lt;/li&gt;
        &lt;/ul&gt;
      &lt;/nav&gt;
    &lt;/div&gt;

    &lt;section class="main"&gt;
      &lt;div class="container"&gt;
        &lt;p&gt;Justice Law is professional representation. Practicing for over 50 years, our team have the knowledge and skills to get you results.&lt;/p&gt;

        &lt;blockquote class="testimonial"&gt;
          &lt;p class="testimonial-message"&gt;Justice Law are the best of the best. Being local, they care about people and have strong ties to the community.&lt;/p&gt;
          &lt;p class="testimonial-author"&gt;
            &lt;img src="/images/peter.jpeg" alt="Photo of Peter Rottenburg"&gt; Peter Rottenburg
          &lt;/p&gt;
        &lt;/blockquote&gt;
      &lt;/div&gt;
    &lt;/section&gt;

    &lt;footer&gt;
      &lt;p class="copyright"&gt;
        &amp;copy; 2016
      &lt;/p&gt;
    &lt;/footer&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

### Liquid

In WordPress, we can write PHP to do almost anything. Jekyll takes a different approach. Instead of providing a full programming language, it uses a templating language named [Liquid](https://shopify.github.io/liquid/). (WordPress has templating languages, too, such as [Timber](https://upstatement.com/timber/).)

The footer of `index.html` contains a copyright notice with a year:

<pre><code class="language-html">
&lt;p class="copyright"&gt;
  &amp;copy; 2016
&lt;/p&gt;
</code></pre>

We’re unlikely to remember to update this every year, so let’s use Liquid to output the current year:

<pre><code class="language-html">
&lt;p class="copyright"&gt;
  &amp;copy; {{ site.time | date: "%Y" }}
&lt;/p&gt;
</code></pre>

We’re building a static website in Jekyll, so this date won’t change until we rebuild the website. If we wanted the date to change without having to rebuild the website, we could use JavaScript.</p>

### Includes

The bulk of the HTML in `index.html` is for setting up the overall layout and won’t change between pages. This repetition will lead to a lot of maintenance, so let’s reduce it.

Includes were one of the first things I learned in PHP. Using includes, we can put the header and footer content in different files, then include the same content on multiple pages.

Jekyll has exactly the same feature. Includes are stored in a folder named `_includes`. We use Liquid to include them in `index.html`:

<pre><code class="language-html">
{% include header.html %}
&lt;p&gt;Justice Law is professional representation. Practicing for over 50 years, our team have the knowledge and skills to get you results.&lt;/p&gt;

&lt;blockquote class="testimonial"&gt;
  &lt;p class="testimonial-message"&gt;Justice Law are the best of the best. Being local, they care about people and have strong ties to the community.&lt;/p&gt;
  &lt;p class="testimonial-author"&gt;
    &lt;img src="/images/peter.jpeg" alt="Photo of Peter Rottenburg"&gt; Peter Rottenburg
  &lt;/p&gt;
&lt;/blockquote&gt;
{% include footer.html %}
</code></pre>

### Layouts

Includes reduce some of the repetition, but we still have them on each page. WordPress solves this problem with template files that separate a website’s structure from its content.

The Jekyll equivalent to template files is layouts. Layouts are HTML files with a placeholder for content. They are stored in the `_layouts` directory. We’ll create `_layouts/default.html` to contain a basic HTML layout:

<pre><code class="language-html">
&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;link rel="stylesheet" href="/css/main.css"&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;div class="container"&gt;
      &lt;h1&gt;&lt;a href="/"&gt;Justice&lt;/a&gt;&lt;/h1&gt;
      &lt;nav&gt;
        &lt;ul&gt;
          &lt;li&gt;&lt;a href="/about/"&gt;About&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href="/services/"&gt;Services&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href="/contact/"&gt;Contact&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href="/advice/"&gt;Advice&lt;/a&gt;&lt;/li&gt;
        &lt;/ul&gt;
      &lt;/nav&gt;
    &lt;/div&gt;

    &lt;section class="main"&gt;
      &lt;div class="container"&gt;
        {{ content }}
      &lt;/div&gt;
    &lt;/section&gt;

    &lt;footer&gt;
      &lt;p class="copyright"&gt;
        &amp;copy; {{ site.time | date: "%Y-%m-%d" }}
      &lt;/p&gt;
    &lt;/footer&gt;
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

Then, replace the includes in `index.html` by specifying the layout. We specify the layout using front matter, which is a snippet of [YAML](https://en.wikipedia.org/wiki/YAML) that sits between two triple-dashed lines at the top of a file (more on this soon).

<pre><code class="language-html">
---
layout: default
---
&lt;blockquote class="testimonial"&gt;
  &lt;p class="testimonial-message"&gt;Justice Law are the best of the best. Being local, they care about people and have strong ties to the community.&lt;/p&gt;
  &lt;p class="testimonial-author"&gt;
    &lt;img src="/images/peter.jpeg" alt="Photo of Peter Rottenburg"&gt; Peter Rottenburg
  &lt;/p&gt;
&lt;/blockquote&gt;
</code></pre>

Now we can have the same layout on all of our pages.</p>

### Front Matter

In WordPress, custom fields allow us to set meta data on a post. We can use them to set SEO tags or to show and hide sections of a page for a particular post.

This concept is called [front matter](https://jekyllrb.com/docs/frontmatter/) in Jekyll. Earlier, we used front matter to set the layout for `index.html`. We can now set our own variables and access them using Liquid. This further reduces repetition on our website.

Let’s add multiple testimonials to `index.html`. We could copy and paste the HTML, but once again, that leads to increased maintenance. Instead, let’s add the testimonials in front matter and iterate over them with Liquid:

<pre><code class="language-html">
---
layout: default
testimonials:
  - message: We use Justice Law in all our endeavours. They offer an unparalleled service when it comes to running a business.
    image: "/images/joice.jpeg"
    name: Joice Carmold
  - message: Justice Law are the best of the best. Being local, they care about people and have strong ties to the community.
    image: "/images/peter.jpeg"
    name: Peter Rottenburg
  - message: Justice Law were everything we could have hoped for when buying our first home. Highly recommended to all.
    image: "/images/gibblesto.jpeg"
    name: D. and G. Gibbleston
---
&lt;div class="testimonials"&gt;
  {% for testimonial in page.testimonials %}
    &lt;blockquote class="testimonial"&gt;
      &lt;p class="testimonial-message"&gt;{{ testimonial.message }}&lt;/p&gt;
      &lt;p class="testimonial-author"&gt;
        &lt;img src="{{ testimonial.image }}" alt="Photo of {{ testimonial.name }}"&gt; {{ testimonial.name }}
      &lt;/p&gt;
    &lt;/blockquote&gt;
  {% endfor %}
&lt;/div&gt;
</code></pre>

### Posts

WordPress stores the HTML content, date and other meta data for posts in the database.

In Jekyll, each post is a static file stored in a `_posts` directory. The file name has the publication date and title for the post — for example, `_posts/2016-11-11-real-estate-flipping.md`. The source code for a blog post takes this structure:

<pre><code class="language-html">
---
layout: post
categories:
  - Property
---
![House](/images/house.jpeg)
</code></pre>

We can also use front matter to set categories and tags.

Below the front matter is the body of the post, written in [Markdown](https://en.wikipedia.org/wiki/Markdown). Markdown is a simpler alternative to HTML.

Jekyll allows us to create layouts that inherit from other layouts. You might have noticed this post has a layout of `post`. The `post` layout inherits from the default layout and adds a date and title:

<pre><code class="language-html">
---
layout: default
---
&lt;h3&gt;{{ page.title }}&lt;/h3&gt;
&lt;p&gt;{{ page.date | date: '%B %d, %Y' }}&lt;/p&gt;

{{ content }}
</code></pre>

Let’s create `blog.html` to iterate over the posts and link to them:

<pre><code class="language-html">
---
layout: default
---
&lt;ul&gt;
  {% for post in site.posts %}
    &lt;li&gt;&lt;a href="{{ post.url }}"&gt;{{ post.title }}&lt;/a&gt;&lt;/li&gt;
  {% endfor %}
&lt;/ul&gt;
</code></pre>

### Collections

In WordPress, custom post types are useful for managing groups of content. For example, you might use custom post types for testimonials, products or real-estate listings.

Jekyll has this feature and calls it [collections](https://jekyllrb.com/docs/collections/).

The `about.html` page shows profiles of staff members. We could define the meta data for the staff (name, image, phone number, bio) in the front matter, but then we could only reference it on that page. In the future, we want to use the same data to display information about authors on blog posts. A collection enables us to refer to staff members anywhere on the website.

Configuration of our website lives in `_config.yml`. Here, we set a new collection:

<pre><code class="language-html">
collections:
  staff_members:
    output: false
</code></pre>

Now we add our staff members. Each staff member is represented in a Markdown file stored in a folder with the collection name; for example, `_staff_members/jane-doe.md`.

We add the meta data in the front matter and the blurb in the body:

<pre><code class="language-html">
---
name: Jane Doe
image: "/images/jane.jpeg"
phone: "1234567"
---
Jane has 19 years of experience in law, and specialises in property and business.
</code></pre>

Similar to posts, we can iterate over the collection in `about.html` to display each staff member:

<pre><code class="language-html">
---
layout: default
---
&lt;ul&gt;
  {% for member in site.staff_members %}
    &lt;li&gt;
      &lt;div&gt;&lt;img src="{{ member.image }}" alt="Staff photo for {{ member.name }}"&gt;&lt;/div&gt;
      &lt;p&gt;{{ member.name }} - {{ member.phone }}&lt;/p&gt;
      &lt;p&gt;{{ member.content | markdownify }}&lt;/p&gt;
    &lt;/li&gt;
  {% endfor %}
&lt;/ul&gt;
</code></pre>

### Search

WordPress has powerful built-in search and even more powerful search plugins.

Jekyll doesn’t have search built in, but there are solutions:

*   client-side search using a JavaScript library such as [Lunr.js](https://lunrjs.com/) ([Jekyll.tips has a tutorial](https://jekyll.tips/jekyll-casts/jekyll-search-using-lunr-js/) on how to set this up);
*   third-party solutions, such as [Algolia](https://blog.algolia.com/instant-search-blog-documentation-jekyll-plugin/) for high-performance search;
*   drop-in solutions, such as [Google Custom Search](https://cse.google.com/).</p>

### Plugins

Plugins are an appealing part of WordPress. It’s easy to load in functionality to get WordPress to do almost anything.

On our Jekyll website, many popular WordPress plugins aren’t necessary:

*   [iThemes Security](https://wordpress.org/plugins/better-wp-security/)  
    Our Jekyll website is as secure as the web server it’s running on.
*   [Backup Guard](https://wordpress.org/plugins/backup/)  
    Our Jekyll website will live in a repository that gives us access to the entire history of changes.
*   [WP Super Cache](https://wordpress.org/plugins/wp-super-cache/)  
    Our Jekyll website is already static.

Other WordPress plugins have third-party equivalents that we can drop into the website:

*   Contact form plugins such as [Contact Form 7](https://wordpress.org/plugins/contact-form-7/) can be replaced with [Formspree](https://formspree.io/), [FormKeep](https://formkeep.com/) or [Wufoo](https://www.wufoo.com/).
*   For a simple store, [WP eCommerce](https://wpecommerce.org/) can be replaced with [Snipcart](https://snipcart.com/), [Gumroad](https://gumroad.com/) or [Stripe](https://stripe.com/).
*   Instead of WordPress comments with [Akismet](https://wordpress.org/plugins/akismet/), you could use [Disqus](https://disqus.com/), [Facebook Comments](https://developers.facebook.com/docs/plugins/comments) or [IntenseDebate](https://intensedebate.com/).

Some WordPress plugins can be emulated with core Jekyll. Here’s a photo gallery using front matter and Liquid:

<pre><code class="language-html">
---
layout: default
images:
  - image_path: /images/bill.jpg
    title: Bill
  - image_path: /images/burt.jpg
    title: Burt
  - image_path: /images/gary.jpg
    title: Gary
  - image_path: /images/tina.jpg
    title: Tina
  - image_path: /images/suzy.jpg
    title: Suzy
---
&lt;ul class="photo-gallery"&gt;
  {% for image in page.images %}
    &lt;li&gt;&lt;img src="{{ image.image_path }}" alt="{{ image.title }}"/&gt;&lt;/li&gt;
  {% endfor %}
&lt;/ul&gt;
</code></pre>

We just need to add our own JavaScript and CSS to complete it.

Jekyll plugins can emulate the functionality of other WordPress plugins. Keep in mind that Jekyll plugins only run while the website is being generated — they don’t add real-time functionality:

*   Instead of [One Click XML Sitemap](https://wordpress.org/plugins/one-click-xml-sitemap/), use [Jekyll Sitemap Generator Plugin](https://github.com/jekyll/jekyll-sitemap).
*   [Jekyll SEO Tag](https://github.com/jekyll/jekyll-seo-tag) gives you some of the functionality of [SEO Wizard](https://www.seowizard.org).
*   Instead of [WPGlobus](https://wordpress.org/plugins/wpglobus/) for a multilingual website, use [Jekyll Language Plugin](https://github.com/vwochnik/jekyll-language-plugin).</p>

### Version Control

One of the major benefits of using a static site generator like Jekyll is the entire site and content can live in Git. At a basic level, Git gives you a history of all the changes on the site. For teams, it opens up all sorts of workflows and approval processes.

GitHub has a fantastic [interactive tutorial](https://try.github.io/) for beginners learning Git.</p>

## Client Hand-Off

That covers the nuts and bolts of creating the website. If you’re curious to see how an entire Jekyll website fits together, have a look at the [Justice template](https://github.com/CloudCannon/justice-jekyll-template). It’s a free MIT-licensed template for Jekyll. The snippets above are based on this template.

The WordPress CMS is built into the platform, so we would need to set up an account for the client.

With our Jekyll website, we’d link our Git repository to one of the Jekyll GUIs mentioned earlier. One of the nice things about this workflow is that clients changes are committed back to the repository. As developers, we can continue to use local workflows even with non-developers updating the website.

Some Jekyll GUIs offer hosting, while others have a way to output to an Amazon S3 bucket or to [GitHub Pages](https://pages.github.com/).</p>

## Summary

At this point, our Jekyll website is live and editable by the client. If we need to make any changes to the website, we simply push to the repository and it will automatically deploy live.

&lt;div class="testimonials"&gt;
  {% for testimonial in page.testimonials %}
    &lt;blockquote class="testimonial"&gt;
      &lt;p class="testimonial-message"&gt;{{ testimonial.message }}&lt;/p&gt;
      &lt;p class="testimonial-author"&gt;
        &lt;img src="{{ testimonial.image }}" alt="Photo of {{ testimonial.name }}"&gt; {{ testimonial.name }}
      &lt;/p&gt;
    &lt;/blockquote&gt;
  {% endfor %}
&lt;/div&gt;
</code></pre>

### Posts

WordPress stores the HTML content, date and other meta data for posts in the database.

In Jekyll, each post is a static file stored in a `_posts` directory. The file name has the publication date and title for the post — for example, `_posts/2016-11-11-real-estate-flipping.md`. The source code for a blog post takes this structure:

<pre><code class="language-html">
---
layout: post
categories:
  - Property
---
![House](/images/house.jpeg)
</code></pre>

We can also use front matter to set categories and tags.

Below the front matter is the body of the post, written in [Markdown](https://en.wikipedia.org/wiki/Markdown). Markdown is a simpler alternative to HTML.

Jekyll allows us to create layouts that inherit from other layouts. You might have noticed this post has a layout of `post`. The `post` layout inherits from the default layout and adds a date and title:

<pre><code class="language-html">
---
layout: default
---
&lt;h3&gt;{{ page.title }}&lt;/h3&gt;
&lt;p&gt;{{ page.date | date: '%B %d, %Y' }}&lt;/p&gt;

{{ content }}
</code></pre>

Let’s create `blog.html` to iterate over the posts and link to them:

<pre><code class="language-html">
---
layout: default
---
&lt;ul&gt;
  {% for post in site.posts %}
    &lt;li&gt;&lt;a href="{{ post.url }}"&gt;{{ post.title }}&lt;/a&gt;&lt;/li&gt;
  {% endfor %}
&lt;/ul&gt;
</code></pre>

### Collections

In WordPress, custom post types are useful for managing groups of content. For example, you might use custom post types for testimonials, products or real-estate listings.

Jekyll has this feature and calls it [collections](https://jekyllrb.com/docs/collections/).

The `about.html` page shows profiles of staff members. We could define the meta data for the staff (name, image, phone number, bio) in the front matter, but then we could only reference it on that page. In the future, we want to use the same data to display information about authors on blog posts. A collection enables us to refer to staff members anywhere on the website.

Configuration of our website lives in `_config.yml`. Here, we set a new collection:

<pre><code class="language-html">
collections:
  staff_members:
    output: false
</code></pre>

Now we add our staff members. Each staff member is represented in a Markdown file stored in a folder with the collection name; for example, `_staff_members/jane-doe.md`.

We add the meta data in the front matter and the blurb in the body:

<pre><code class="language-html">
---
name: Jane Doe
image: "/images/jane.jpeg"
phone: "1234567"
---
Jane has 19 years of experience in law, and specialises in property and business.
</code></pre>

Similar to posts, we can iterate over the collection in `about.html` to display each staff member:

<pre><code class="language-html">
---
layout: default
---
&lt;ul&gt;
  {% for member in site.staff_members %}
    &lt;li&gt;
      &lt;div&gt;&lt;img src="{{ member.image }}" alt="Staff photo for {{ member.name }}"&gt;&lt;/div&gt;
      &lt;p&gt;{{ member.name }} - {{ member.phone }}&lt;/p&gt;
      &lt;p&gt;{{ member.content | markdownify }}&lt;/p&gt;
    &lt;/li&gt;
  {% endfor %}
&lt;/ul&gt;
</code></pre>

### Search

WordPress has powerful built-in search and even more powerful search plugins.

Jekyll doesn’t have search built in, but there are solutions:

*   client-side search using a JavaScript library such as [Lunr.js](https://lunrjs.com/) ([Jekyll.tips has a tutorial](https://jekyll.tips/jekyll-casts/jekyll-search-using-lunr-js/) on how to set this up);
*   third-party solutions, such as [Algolia](https://blog.algolia.com/instant-search-blog-documentation-jekyll-plugin/) for high-performance search;
*   drop-in solutions, such as [Google Custom Search](https://cse.google.com/).</p>

### Plugins

Plugins are an appealing part of WordPress. It’s easy to load in functionality to get WordPress to do almost anything.

On our Jekyll website, many popular WordPress plugins aren’t necessary:

*   [iThemes Security](https://wordpress.org/plugins/better-wp-security/)  
    Our Jekyll website is as secure as the web server it’s running on.
*   [Backup Guard](https://wordpress.org/plugins/backup/)  
    Our Jekyll website will live in a repository that gives us access to the entire history of changes.
*   [WP Super Cache](https://wordpress.org/plugins/wp-super-cache/)  
    Our Jekyll website is already static.

Other WordPress plugins have third-party equivalents that we can drop into the website:

*   Contact form plugins such as [Contact Form 7](https://wordpress.org/plugins/contact-form-7/) can be replaced with [Formspree](https://formspree.io/), [FormKeep](https://formkeep.com/) or [Wufoo](https://www.wufoo.com/).
*   For a simple store, [WP eCommerce](https://wpecommerce.org/) can be replaced with [Snipcart](https://snipcart.com/), [Gumroad](https://gumroad.com/) or [Stripe](https://stripe.com/).
*   Instead of WordPress comments with [Akismet](https://wordpress.org/plugins/akismet/), you could use [Disqus](https://disqus.com/), [Facebook Comments](https://developers.facebook.com/docs/plugins/comments) or [IntenseDebate](https://intensedebate.com/).

Some WordPress plugins can be emulated with core Jekyll. Here’s a photo gallery using front matter and Liquid:

<pre><code class="language-html">
---
layout: default
images:
  - image_path: /images/bill.jpg
    title: Bill
  - image_path: /images/burt.jpg
    title: Burt
  - image_path: /images/gary.jpg
    title: Gary
  - image_path: /images/tina.jpg
    title: Tina
  - image_path: /images/suzy.jpg
    title: Suzy
---
&lt;ul class="photo-gallery"&gt;
  {% for image in page.images %}
    &lt;li&gt;&lt;img src="{{ image.image_path }}" alt="{{ image.title }}"/&gt;&lt;/li&gt;
  {% endfor %}
&lt;/ul&gt;
</code></pre>

We just need to add our own JavaScript and CSS to complete it.

Jekyll plugins can emulate the functionality of other WordPress plugins. Keep in mind that Jekyll plugins only run while the website is being generated — they don’t add real-time functionality:

*   Instead of [One Click XML Sitemap](https://wordpress.org/plugins/one-click-xml-sitemap/), use [Jekyll Sitemap Generator Plugin](https://github.com/jekyll/jekyll-sitemap).
*   [Jekyll SEO Tag](https://github.com/jekyll/jekyll-seo-tag) gives you some of the functionality of [SEO Wizard](https://www.seowizard.org).
*   Instead of [WPGlobus](https://wordpress.org/plugins/wpglobus/) for a multilingual website, use [Jekyll Language Plugin](https://github.com/vwochnik/jekyll-language-plugin).</p>

### Version Control

One of the major benefits of using a static site generator like Jekyll is the entire site and content can live in Git. At a basic level, Git gives you a history of all the changes on the site. For teams, it opens up all sorts of workflows and approval processes.

GitHub has a fantastic [interactive tutorial](https://try.github.io/) for beginners learning Git.</p>

## Client Hand-Off

That covers the nuts and bolts of creating the website. If you’re curious to see how an entire Jekyll website fits together, have a look at the [Justice template](https://github.com/CloudCannon/justice-jekyll-template). It’s a free MIT-licensed template for Jekyll. The snippets above are based on this template.

The WordPress CMS is built into the platform, so we would need to set up an account for the client.

With our Jekyll website, we’d link our Git repository to one of the Jekyll GUIs mentioned earlier. One of the nice things about this workflow is that clients changes are committed back to the repository. As developers, we can continue to use local workflows even with non-developers updating the website.

Some Jekyll GUIs offer hosting, while others have a way to output to an Amazon S3 bucket or to [GitHub Pages](https://pages.github.com/).</p>

## Summary

At this point, our Jekyll website is live and editable by the client. If we need to make any changes to the website, we simply push to the repository and it will automatically deploy live.</p>

### Your First Jekyll Website

Now it’s your turn. Plenty of resources are available to help you build your first Jekyll website:

*   The [official Jekyll website](https://jekyllrb.com/) is a great place to start with in-depth documentation on all of Jekyll’s features.
*   [Jekyll.tips](https://jekyll.tips/) has a video tutorial series covering core Jekyll topics.
*   Have a look at Jekyll templates on GitHub to see how they’re put together: [Frisco](https://github.com/CloudCannon/frisco-jekyll-template) for marketing websites, [Scholar](https://github.com/CloudCannon/scholar-jekyll-template) for documentation and [Urban](https://github.com/CloudCannon/urban-jekyll-template) for digital agencies.

If you’re migrating, Jekyll has [tools to import posts](https://import.jekyllrb.com/) from WordPress and WordPress.com websites. After importing, you’ll need to manually migrate or create the layouts, pages, CSS, JavaScript and other assets for the website.</p>

### Wrapping Up

The beauty of Jekyll is in its simplicity. While WordPress can match many of the features of Jekyll, it often comes at the cost of complexity through extra plugins or infrastructure.

Ultimately, it’s about finding the tool that works best for you. I’ve found Jekyll to be a fast and efficient way to build websites. I encourage you to try it out and post your experience in the comments.

{{< signature "al" >}}


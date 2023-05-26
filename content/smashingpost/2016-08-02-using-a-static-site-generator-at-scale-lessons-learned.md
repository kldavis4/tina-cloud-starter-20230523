---
title: 'Using A Static Site Generator At Scale: Lessons Learned'
slug: using-a-static-site-generator-at-scale-lessons-learned
author: stefan-baumgartner
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5f45693-14c7-4e42-9f0f-bb3893e986f0/new-github-screenshot-opt.png
date: 2016-08-02T18:18:15.000Z
summary: >-
  Static site generators are wonderful, even though they have to deal with work for which they weren’t initially created for. Learn how to take care and provide aid wherever necessary for them to get going and become more productive than ever.
description: >-
  Static site generators are wonderful, even though they have to deal with work for which they weren’t initially created for. Learn how to provide aid wherever necessary for them to become more productive than ever.
categories:
  - Coding
  - Generators
  - Static Generators
---
Static site generators are pretty *en vogue* nowadays. It is as if developers around the world are suddenly realizing that, for most websites, a simple build process is easy enough to render the last 20 years of content management systems useless. All right, that’s a bit over the top. But for the average website without many moving parts, it’s pretty close!

However, does that hold true for websites bigger than your humble technology blog? How do static site generators behave when the number of pages exceeds the average portfolio website and runs up into the thousands? Or when development is a team effort? Or when people of different technical backgrounds are involved? This is the story of how we managed to bring roughly 2000 pages and 40 authors onto a technology stack made for hackers.

## The Reason For Static Sites And The Task At Hand

We used static site generators at our company's spin-off startup, where we had a reasonable amount of content to maintain: about 30 to 40 pages of product information, the occasional landing page and some company-related websites.

We have had good experiences with static site generators. For us front-end-heavy web developers, using a static site generator is as easy as templating, but with real data and actual content! And it enables us and our content providers to scale easily.

We started using the popular <a href="https://jekyllrb.com">Jekyll</a> static site generator. The usual page consisted of the following:

* **YAML front matter**.  
This is a delight for authors and editors, because they can put any meta information in it — even meta data that is not yet interpreted but might be interpreted in the future.
* **Markdown**.  
Markdown provides the basic structure for the content. It is easy to understand, it is easy to write, and a ton of editors out there give a good preview of the content at hand.
* **Liquid block elements**  
[Liquid is Shopify’s](https://help.shopify.com/themes/liquid) templating language, and it’s very powerful. It allows for advanced loops and conditionals and can be easily extended using plugins written in Ruby. Developers provide content editors with structural elements such as `{% section %}` and `{% column %}` to better organize the page.
* **And, of course, a lot of images**.  
Each page had about 5 to 15 images.

{{% feature-panel %}}

A typical page looked like this:

<pre><code class="lang-markup">---
title: Getting started with our product
layout: blue
headerImage: getting-started.svg
permalink: /getting-started/
---
{% section %}
# How to get started with our product
…
{% endsection %}
…
</code></pre>

In the end, writing content was as easy as scribbling down notes in an editor. Polish and beauty were added once the page ran through Jekyll.

In addition to the ease of using our preferred content editors, we loved the additional benefits that static site generators gave us as developers and “webmasters.” (You haven’t heard that term in quite some time, have you?)

* Security-wise, static websites are a fortress. Not having any database or any dynamic interpreter running on your servers reduces the risk of hacks tremendously.
* A static website is incredibly fast to serve. Put it on a CDN and let it be consumed worldwide in no time.
* Web developers love the flexibility. Changing the layout or adding a microsite to the content does not require you to go deep into the internals of the content management system, nor does it require any hacks. You can maintain these resources next to your usual content and “just deploy” them with it.
* Storing all of the technology parts as well as the content in a version-control system such as Git allows for a flexible publishing cycle. Preparing content in a branch, merging it on demand and putting it out on the servers entails just a few clicks on a Monday morning.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8785d4a4-84a2-4cde-b700-b39cc8be48a9/new-no-cms-intro.svg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8785d4a4-84a2-4cde-b700-b39cc8be48a9/new-no-cms-intro.svg" sizes="100vw" caption="Using Git as content store allows you to treat content like source code. Including pull requests, code reviews and versioning. This brings content authors to the same place as developers and designers. (Image credits: Stefan Baumgartner and Simon Ludwig) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8785d4a4-84a2-4cde-b700-b39cc8be48a9/new-no-cms-intro.svg'>Large preview</a>)" alt="Git as content store" >}}

Our five-person team was pretty pleased with the results. We took the idea from our marketing website over to our other web entities. Suddenly, next to our 40-page main brand website was a 50-page style guide. Then, 150 pages of documentation. Then, almost every web entity from our sibling company, counting up to 2000 pages of documentation. You wouldn’t believe it, but our tech stack was at the edge of exhaustion:

* The bigger your page, the longer your build. Static site generation is pro-active compilation of source code into HTML pages. It can take hours until your website is deployment ready.
* Choosing a static site generator is like betting on one Content Management System. A tool which speeds you up at first, but slows you down when it doesn't meet your needs.
* Even if most of your content is static and does not require any user input, there is the occasional case where you need dynamic data.
* Tech-savvy content editors love working with content that is actually source code. Not so tech-savvy editors ..., well, they don't.

Let's see how we tackle each one of those topics.

## More Content, More Build Time

One key factor of static site generation is the proactive approach to rendering. With a traditional content management system (CMS), each page you access gets rendered just for that one visit (obvious caching algorithms not included). With a static site generator, you create all of your pages at once. And even though the process is fast, it scales linearly with the amount of content. Especially when you have to auto-generate and auto-optimize <strong>responsive images</strong> of screenshots from 200 pixels up to full high definition in 200-pixel steps. Even with our initial setup of 40 pages and roughly 300 images, the build took about <strong>two hours</strong> from start to finish on our continuous delivery machines. That’s not time you want to wait for to see whether you fixed that typo in your headline or not. Anticipating our workload in the not-so-distant future, we had to make some important decisions.

{{% ad-panel-leaderboard %}}

### Divide And <del>Conquer</del> Build

Even if your technology stack can generate thousands of pages, it doesn’t necessarily need to. Not every item of content needs to know about every other item. A German-language website can be treated separately from an English-language version. And the documentation is a different content area than our main brand website.

Not only are the content elements discrete, but they also diverge in update frequency. Blogs are updated many times a day, the main brand website many times a week, and the documentation every two weeks to coincide with our product’s feature releases. And our Java performance book? Well, that’s once or twice a year.

This led us to split all of our websites into distinct <strong>content packages</strong> and <strong>tech repositories</strong>. The content packages were Git repositories that contained everything an author or editor could and should touch: Markdown files, images, additional data lists. For each entity, we created a content repository with the same structure.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d93bb144-16dc-47f3-946e-294543cc6a7c/new-conveyor-belt.svg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d93bb144-16dc-47f3-946e-294543cc6a7c/new-conveyor-belt.svg" sizes="100vw" caption="The tech repository can be regarded as a machine that converts several content repositories into full static websites. (Image credits: Stefan Baumgartner and Simon Ludwig) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d93bb144-16dc-47f3-946e-294543cc6a7c/new-conveyor-belt.svg'>Large preview</a>)" alt="One tech repo for various content packages" >}}

The tech repositories, on the other hand, contained everything meant for developers: front-end code, templates, content plugins, and the build process for our static site generation.

Our build servers were set up to listen for changes to each of those Git repositories. A change in a content repository triggered a build of that content package alone. A change in a tech repository triggered a build of only the corresponding content repository. Depending on how many content repositories you have, this can cut down the build time tremendously.

### Incremental Builds

Even more important than splitting the content files into separate packages was the method for dealing with images. The objective was to generate each screenshot of our product in various responsive-friendly sizes, down to 200 pixels wide. Also, each newly generated image would have to be optimized in <a href="https://github.com/sindresorhus/gulp-imagemin">gulp-imagemin</a>. Doing this for every build iteration took up a good chunk of the initial two-hour build time.

While the two hours of build time were necessary for the very first build, that was wasted time for each subsequent one. Not every image changed from iteration to iteration. Much of the work had already been done, so why do it over and over again? Incremental builds were the key to saving our build servers and ourselves from having to do a lot of work.

Our image processing was done in <a href="https://gulpjs.com">Gulp</a>. The <code>gulp-newer</code> plugin is exactly what we needed for our incremental builds. It compares the timestamp of each file with the timestamp of the file with the same name in the destination directory. If the timestamp is newer, the file is kept in the stream. Otherwise, it is discarded. Generating all of the responsive images, then, was a matter of chaining the right plugins in the right order:

<div class="break-out">

 <pre><code class="lang-javascript">const merge = require('merge2');
const rename = require('gulp-rename');
const newer = require('gulp-newer');
const imagemin = require('gulp-imagemin');
…

/*
The options in this case are an array of image widths. In our
case, we want responsive images from 200 pixels
up to 1600 pixels wide.
&#42;/
const options = [
  { width: 200 }, { width: 400 },
  { width: 600 }, { width: 800 },
  { width: 1000 }, { width: 1200 },
  { width: 1400 }, { width: 1600 }
];

gulp.task('images',() =&gt; {
  /&#42;
  We can map each element of this array to a Gulp stream.
  Each of those streams selects each of the original images
  and creates one variant.
  &#42;/
  const streams = options.map(el =&gt;  {
    return gulp.src(['./src/images/&#42;&#42;/&#42;'])
       /&#42;
       We follow a naming convention of adding a suffix to
       the file's base name. This suffix is the image's target
       width.
       &#42;/
      .pipe(rename(file =&gt; file.basename += '-' + el.width))
       /*
       This is where the "incremental" builds kick in.
       Before we run the heavy processing and resizing tasks,
       we filter elements that don't have any updates.
       This Gulp tasks checks whether the results in "images" are
       older than the source items.
       &#42;/
      .pipe(newer('dist/images'))
      .pipe(resize(el))
      .pipe(imagemin())
      .pipe(gulp.dest('dist/images'));
  });
  return merge(streams);
});
</code></pre>
</div>

In the absence of a good image-resizing plugin, we had to create our own. This was also the time to ensure that no unnecessary file was being processed. If an image couldn’t be resized because the target width was bigger than the original, then we discarded the image as well. The following snippet uses Node.js’ <a href="https://www.npmjs.com/package/gm">GraphicsMagick</a> bindings to complete the task.

<pre><code class="lang-javascript">const gm = require('gm');
const through = require('through2');

module.exports = el =&gt; {
  return through.obj((originalFile, enc, cb) =&gt; {
    var file = originalFile.clone({contents: false});

    if (file.isNull()) {
      return cb(null, file);
    }

    const gmfile = gm(file.contents, file.path);
    gmfile.size((err, size) =&gt; {
      if(el.width &lt; size.width) {
        gmfile
          .resize(el.width,
            (el.width / size.width) * size.height)
          .toBuffer((err, buffer) =&gt; {
             file.contents = buffer;
             /* add resized image to stream */
             cb(null, file);
           });
      } else {
        /* remove from stream */
        cb(null, null);
      }
    });
  });
};
</code></pre>

With all of this incremental adding of files, we couldn’t forget to get rid of files in the destination directory that had been deleted in the source. We didn’t want any leftovers from previous builds lying around, adding extra weight to the bundle to be deployed. Thankfully, Gulp's task system allows for <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Promise">promises</a>, so we had a lot of Promise-based plugins we could use for this task.

<div class="break-out">

 <pre><code class="lang-javascript">const globby = require('globby');
const del = require('del');
const path = require('path');
const globArray = [
  'images/**/*'
];

const widths = [200, 400, 600, 800, 1000, 1200, 1400, 1600];

/* This helper function adds the width suffix
   to the file name. &#42;/
const addSuffix = (name, w) =&gt; {
  const p = path.parse(name);
  p.name = `${p.name}-w`;
  return path.format(p);
}

gulp.task('diff', () =&gt; {
  return Promise.all([
    /* First, we select all files in the destination. &#42;/
    globby(globArray, { cwd: 'dist', nodir: true }),
    /* In parallel, we select all files in the source
       folder. Because they don't have the width suffix,
       we add them for every image width after selecting. &#42;/
    globby(globArray, { cwd: 'src', nodir: true })
      .then(files =&gt; files
         .map(el =&gt; […widths.map(w =&gt; addSuffix(el, w)])
  ])
  /* This is the diffing process. All file names that
     are in the destination directory but not in the source
     directory are kept in this array. Everything else is
     filtered. &#42;/
  .then(paths =&gt; paths[0]
    .filter(i =&gt; paths[i].indexOf(i) &lt; 0))
  /* The array now consists of files that are in "dest"
     but not in "src." They are leftovers and should be
     deleted. &#42;/
  .then(diffs =&gt; del(diffs));
);
</code></pre>
</div>

With all of these changes to the build process, the initial two hours for the images had been reduced to <strong>two to five</strong> minutes per build, depending on the number of images added. The extra time of doing all of the file-status checks passed pretty quickly, even with tens of thousands of images lying around.

## Avoiding Technology Lock-In

Jekyll is an amazing tool because it comes with a lot of features that go beyond merely creating HTML pages. The healthy plugin ecosystem makes Jekyll not just a static site generator, but a full-fledged build system. Out of the box, it’s possible to <a href="https://jekyllrb.com/docs/assets/">compile Sass and CoffeeScript</a> with Jekyll. The <a href="https://jekyll.github.io/jekyll-assets/">Jekyll asset pipeline</a> offers not only a ton of features for creating images, but also extra confidence because it checks every included asset for existence and integrity. This is gold if you’re dealing with a lot of assets.

However, these benefits come at a high cost, not only with performance and build time, but also with a certain level of technology lock-in. Instead of Jekyll being <em>in</em> your build system, it <em>becomes</em> your build system. Anything not included in Jekyll or one of the plugins has to be written and maintained by you in Ruby.

This bugged us in a several ways. Ruby was not our favorite language to begin with. While many on our team could work with Ruby, some of us couldn’t write a single line without referring to the language’s specification. Even worse is that we were trying to move away from a traditional CMS to gain more freedom and flexibility in the way we do things. By relying heavily on Jekyll’s ecosystem, we were trading one monolith for another. To avoid this form of technology lock-in, we took a few more steps.

{{% ad-panel-leaderboard %}}

### Separation of Concerns

First, we stripped away everything from Jekyll's duties that had nothing to do with the actual output of HTML. We still included the check for an asset’s existence. However, image generation and the compilation of JavaScript and style sheets would all be done by Gulp builds running beforehand.

This gave us a list of completely different benefits:

* Should we have a change of heart and switch Sass for something trendier, it would affect only a single part of our build file, not the entire static site generation. The same goes for the compilation of our other assets.
* We could decide whether even to build certain assets. The JavaScript might change, but the styles might not, so why compile the styles again? This cuts down even more on build time.
* We could even remove Jekyll at some point, and key parts of our build would still be intact and functioning.

Secondly, we removed any post-processing steps from Jekyll. The Jekyll asset pipeline allows you to create hashed URLs for JavaScript, style sheets and images. Stripping that away from the Jekyll process meant Jekyll had less to do, thus clarifying its purpose. Interestingly enough, we saw an improvement in speed by moving the revisiting process from Ruby to Node.js. The wonderful plugin <a href="https://github.com/sindresorhus/gulp-rev">gulp-rev</a> took care of this process.

<pre><code class="lang-javascript">const gulp       = require('gulp');
const rev        = require('gulp-rev');
const revReplace = require('gulp-rev-replace');
…
gulp.task('revision', () =&gt; {
  return gulp.src(['./**/*.js',
     './**/*.css', './images/**/*.*'])
    .pipe(rev())
    .pipe(gulp.dest(based))
    .pipe(rev.manifest())
    .pipe(gulp.dest('.'));
});

gulp.task('rev', ['revision'], () =&gt; {
  var manifest = gulp.src('rev-manifest.json');
  return gulp.src(['./**/*.html'])
    .pipe(revReplace({
      manifest: manifest
    }))
    .pipe(gulp.dest(based));
});
</code></pre>

From here on in, we made sure to know what is a part of Jekyll’s purpose and what isn’t. You can do amazing things with Jekyll and its ecosystem, but you also don’t want to rely too much on a tool that might not be the right one for tasks to come.

Jekyll’s responsibilities were reduced to converting Markdown and Liquid to HTML pages. With everything else being done by Gulp, you can easily spot the odd bird in the stack:

* The self-written plugins for custom sectioning elements were being done in Ruby (the only Ruby dependency still there).
* We were still using Liquid, a rather “exotic” templating language.

We also realized that Jekyll is not meant to be included in a build process. Jekyll was created to <em>be</em> the build process. Jekyll opens and analyzes every file during a build. Once you strip away everything from Jekyll that isn’t HTML creation, you have to take care of Jekyll's built-in features like incremental builds by yourself.

### Liquid Voodoo

While Jekyll is very popular, the underlying templating engine, Liquid, seems to be the odd one standing. It bears similarities to the PHP templating engine Twig and the JavaScript equivalent Swig, but it has a lot of features that are nowhere else to be seen. Liquid is powerful and allows for a lot of logic to find its way into the templates. This is not always a good thing, but it also isn’t Liquid’s fault. Take, for example, the creation of breadcrumbs based on a document’s permalink, done entirely in the templating language:

<div class="break-out">

 <pre><code class="lang-markup">{% assign coll = site.content %}
&lt;ul class="breadcrumbs"&gt;
  &lt;li&gt;&lt;a href="{{site.baseurl}}/"&gt;Home&lt;/a&gt;&lt;/li&gt;
  {% assign crumbs = page.url | split: '/' %}
  {% for crumb in crumbs offset: 1%}
  {% capture crumb_url %}{% assign crumb_limit = forloop.index | plus: 1 %}{% for crumb in crumbs limit: crumb_limit %}{{ crumb | append: '/' }}{% endfor %}{% endcapture %}
  {% capture site_name %}{% for p in coll %}{% if p.url == crumb_url %}{{ p.title }}{% endif %}{% endear %}{% end capture %}
  {% endunless %}
  {% unless site_name == '' %}
  &lt;li&gt;
  {% unless forloop.last %}
    &lt;a href="{{ site.baseurl }}{{ crumb_url | strip_newlines }}"&gt;{{site.name}}&lt;/a&gt;
  {% else %}
    &lt;span&gt;{{ site_name }}&lt;/span&gt;
  {% endunless %}
  &lt;/li&gt;
  {% endfor %}
&lt;/ul&gt;
</code></pre>
</div>

Let’s not go too deep into the abomination of code you see above. A mere glance should get the point across: The code above will output correctly, but it’s obviously not as readable as one would expect from a templating engine. On the contrary, the more features and logic you cram into this, the worse it’s going to be if you ever have to reconstruct what has happened. Moving away from this Liquid “voodoo” to Jekyll plugins would be a better idea:

* Restrict Liquid to content output (loops and simple conditionals).
* Create complex data beforehand. If it’s not available in Jekyll itself, then a plugin or a pregenerated YAML or JSON file is the way to go.

Looking at the breadcrumb generation again. A plugin that fills the relevant data set would be much more flexible and would not rely on string concatenation or splitting magic. Also, the Liquid templates that access the prefilled data would be much more readable and easier to understand:

<pre><code class="lang-markup">{% if page.breadcrumbs %}
&lt;ul class="breadcrumbs"&gt;
  &lt;li&gt;&lt;a href="{{site.baseurl}}/"&gt;Home&lt;/a&gt;&lt;/li&gt;
  {% for item in page.breadcrumbs %}
  &lt;li&gt;
    {% unless forloop.last %}
    &lt;a href="{{item.url}}"&gt;{{item.label}}&lt;/a&gt;
    {% else %}
    &lt;span&gt;{{item.label}}&lt;/span&gt;
  {% endunless %}
  &lt;/li&gt;
  {% endfor %}
&lt;/ul&gt;
{% endif %}
</code></pre>

This will keep your templates clean and tidy. Also, if you want to move from Liquid to another templating engine (in case you ever drop Jekyll), the templates will be a lot easier to convert.

## Serving More Than Static Websites

Deploying a static website sounds easy at first. You have a bundle of rendered HTML files and a lot of assets, and you just have to put them somewhere to be delivered to the World Wide Web. With free hosting services, static storage services and content delivery networks, the possibilities for getting your content out seem endless. You even can serve a page from a Dropbox folder!

If you are doing more than simply delivering content — perhaps you are in an ongoing migration process — then the requirements for the server might be a little more demanding.

The solution we have in place is based on nginx, which is great for serving static websites to begin with, but also makes for an easy setup when you’re not <em>just</em> serving a static website.

### Ongoing Migration From Old to New

With 2000 pages of content divided into different content packages, we had two strategies to choose from to go live:

* Convert all of the old content, wait for a big-bang release and fail miserably.
* Or start to release smaller content packages, and migrate over time.

With option one, the converted content would grow stale or would have to be maintained twice for a certain amount of time. And we wouldn’t get the benefits of static websites until long after everything is done. Of course, we opted for the latter. To make sure we could freely deploy new content created with the new technology stack without killing access to unmerged pages from the old CMS, we configured nginx to serve as a “fall-through” proxy.

{{< figure src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6257c5f7-92ad-4c88-90cc-21250e812352/visu-1.svg" alt="A proxy handling files from two different locations" caption="The proxy hits files from the static content folder first. Should the file not be available, the proxy falls through to the old CMS server. (Image: Stefan Baumgartner and Simon Ludwig)" >}}

* The idea was to first hit the deployed static website. This page and all of the assets had to be served should nginx hit a file.
* Instead of showing a 404 when a file is not available, nginx proxies the request through to the old server architecture.

This required us to run nginx on its own server, with the domain pointed towards it, and the IP of the old server serving as an upstream server.

<pre><code class="lang-bash"># An upstream server pointing to an IP address where the old
# CMS output is
upstream old-cms {
  server  192.168.77.22;
}

# This server fetches all requests and fetches the static
# documents. Should a document not be available, it falls
# back to the old CMS output.

server {
  listen 80;
  server_name your-domain.com;

  # the fallback route
  location @fallback {
    proxy_pass  https://old-cms;
  }

  # Either fetch the available document or go back to the
  # fallback route.
  location / {
    try_files   $uri $uri/ @fallback;
  }
}
</code></pre>

As the migration continued, more and more pages fell from the old CMS to the new static site server. Once everything was done, we could freely cut off the connection to the old server and have everything on the new one.

### The Need for Dynamic Content

Static websites exclude dynamic content, by definition. But even with the most static of websites, a dynamic element is needed once in a while. A lot of website features can be implemented with services that operate solely client side. Comments on blogs are often powered by services such as Facebook and Disqus. However, these features shouldn’t be critical to your website. Because JavaScript is the weakest link in the browser’s technology stack and could fail unexpectedly, it wouldn’t be wise to rely on it for key features of your website.

Other features require the server. For example, some parts of our static website are confidential and must be restricted to a certain user group. To gain access, a user needs to log in using the company’s single-sign-on service and must have the necessary permissions.

For such cases, we opened up a door to a small Node.js application using nginx upstreams.

{{< figure src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/772ceb89-60cd-49fe-a438-c907c2cfc0be/visu-2.svg" alt="A proxy handling files from two different locations" caption="Before hitting the static websites, the proxy directs a subset of URLs to the Node.js app, hiding possible static websites underneath. (Image: Stefan Baumgartner and Simon Ludwig)" >}}

<pre><code class="lang-bash"># This upstream points to a Node.js server running locally
# on port 3000.
upstream nodejs-backend {
  server   127.0.0.1:3000
}

# Later, we pointed dedicated routes to this Node.js back end
# when defining locations.
location /search/ {
  proxy_pass https://nodejs-backend;
}
</code></pre>

This application handles session IDs, calls to the single-sign-on service and a small website search feature implemented with <a href="https://lunrjs.com/">Lunr</a>. The important thing here is that we’re not modifying existing content, but rather providing additional content on top of it. If your content needs to have mostly dynamic features, then a static site generator is not right for you.

## Editing With A Static Site Generator

The biggest challenge in our journey to static sites was getting content editors to work with the new technology stack. You have to be hard as nails if you are willing to leave the comforts of your WYSIWYG editor — you know, those same comforts that drive web developers insane.

To get everyone, even the biggest skeptics, on board, we needed to take care of the following:

* Content editing on the new website had to be an improvement for the author, both in comfort and productivity. Providing actual content management and offering a good overview of what’s happening on the website justified the added complexity of dealing with files and source code.
* Authors had to see the benefit of being restricted in how they could edit content. Not being able to color text red would be a relief for developers and would make the website more consistent, but content creators might view it as an unnecessary restriction. Again, this is an issue of content management versus content design. Leveraging the possibilities of structuring content without giving much thought to the visual output lowers the barrier to entry with the new system. If content editors are enabled to do much more that is actually beneficial to the page, then they won’t miss features that they never needed in the first place.

On top of that, we had to support content editing for two different types of users: the professional, daily content editor and the occasional contributor.

### Pro Mode

We provided our main content editors with two ways to edit.

The first was to set up Node.js and Ruby on the content editor’s own machine, as well as to give them a crash course in Git and GitHub. Granted, this is not the easiest way to get started. It’s actually pretty hard, especially for someone who isn’t familiar with these technologies or isn’t even into software development at all. This elaborate setup was meant for people who needed a complete view of the whole page, or at least of their content package.

The advantage for these editors kicked in when they got to creating content. Writing in Markdown, as one might scribble notes, was incredibly fast. And copying and pasting content blocks between websites without the interference of a web-based interface made it even faster.

An editing tool such as Atom learns from everything you type and completes your code at times — another boost in productivity. Content becomes code, and all of the advantages of code editing emerge. Once the heavy lifting was done and the content authors were set up, editing happened in a breeze.

The other way, meant for quick fixes and updates to existing content, was to use GitHub’s web interface.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e3de206-f320-461a-be22-69aa11c4df79/new-github-screenshot-large-opt.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e3de206-f320-461a-be22-69aa11c4df79/new-github-screenshot-large-opt.png" sizes="100vw" caption="GitHub features a source editor that can stand in for a file-based Markdown CMS, including file uploading. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e3de206-f320-461a-be22-69aa11c4df79/new-github-screenshot-large-opt.png'>Large preview</a>)" alt="Github’s source editing interface is close to a Markdown CMS" >}}

Not only is GitHub good for storing and managing source code, but its in-place editing and file uploading make it a full-fledged CMS. It’s a bit rough if you want to do more than Markdown and actually want previews of your images, but everything that’s available for editing GitHub’s wiki pages was good enough for our own documentation.

One huge benefit we got from using Git and GitHub for data storage and the user interface was being able to work in content branches and doing pull requests. This was a delight for managing content, because we could prepare content in packages without interrupting the public website. This allowed professional content editors to create their own version of a page long beforehand and then push it live simply by clicking the “merge” button in GitHub.

Access to GitHub was, however, still a bit limited. There was a lot of clutter meant for source code, not for content, and a connection to the actual website couldn’t be provided. So, a whole lot of people were unable to create or maintain content.

### Not-So-Pro Mode

For those people, we decided to create our own content-editing interface, strongly inspired by the likes of <a href="https://ghost.org/">Ghost</a>. The most important thing was to be able to <strong>get an immediate preview</strong>. People who don’t spend every day creating content would be confused and put off if they couldn’t see the result of what they were typing — especially when the incorrect use of a custom plugin could result in a build error.

Constantly rendering the content at hand instilled confidence and supported the work of the content author. It was even fun to see simple commands outputted to advanced HTML.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dd182d0-2f7b-4863-b526-a1388964373b/ook-large-opt.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dd182d0-2f7b-4863-b526-a1388964373b/ook-large-opt.jpg" sizes="100vw" caption="The content preview editor allows for Markdown conversion and a lot of custom content blocks, giving authors a good feel for the result. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dd182d0-2f7b-4863-b526-a1388964373b/ook-large-opt.jpg'>Large preview</a>)" alt="A simple content preview editor that allows fast Markdown to HTML conversion" >}}

When working on the content-editing interface, we started dropping Jekyll completely. Jekyll is meant for websites, not for single pages in a single-page application. Requiring a manually started rendering process, which was rather slow to begin with, negated the benefit of immediacy. Jekyll was slowly replaced with <a href="https://metalsmith.io">Metalsmith</a>, a static site generation framework that had one huge benefit: various templating engines to choose from. This enabled us to run the same templating language on both the static site generator and our content-editing application, saving us a lot of development time and keeping the output consistent.

The content-editing application was not meant to be a full-fledged CMS. It was a way to get easy access to a technology that’s difficult, and to provide others who spend more time working on the content with prepared input.

Again, we saw an increase in productivity. The content providers usually wrote in Word and then pasted the text in various other content-editing interfaces. This had side effects: copy-and-paste errors and additional styling that was hard to get rid off. This time, the content they prepared was perfectly consumable by our static site generator and required minimal attention afterwards.

### API-Driven Content Management System

With the popularity of static site generators, we’ve also seen a shift in the CMS landscape. Instead of being all-powerful, all-in-one solutions, the new generation of CMS’ focuses on actual management again, dropping the rendering process in favor of structured output via an API. With our goal to make content management as convenient as possible for our authors and editors, we inspected these as well.

Commercial products such as <a href="https://contentful.com">Contentful</a> and open-source alternatives such as <a href="https://getcockpit.com">Cockpit</a> provide all of the conveniences of a traditional CMS without requiring you to spend much effort on the actual content-rendering part. Traditional old-school CMS’ such as Drupal have jumped on the bandwagon, with the <a href="https://groups.drupal.org/headless-drupal">Headless Drupal</a> initiative. Even WordPress allows you to access content directly with the <a href="https://wordpress.org/plugins/json-api">JSON API</a> plugin.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/033fa395-e3ef-4f0f-a649-d0d19c8a6d4a/contentful-large-opt.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/033fa395-e3ef-4f0f-a649-d0d19c8a6d4a/contentful-large-opt.jpg" sizes="100vw" caption="API-driven CMS’ such as Contentful have all of the conveniences of a traditional CMS, while keeping content management and content output completely separate. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/033fa395-e3ef-4f0f-a649-d0d19c8a6d4a/contentful-large-opt.jpg'>Large preview</a>)" alt="Contentful as an API-driven CMS" >}}

If you think of the static site generation pipeline as a combination of loosely coupled technologies, API-driven CMS’ still come with a certain kind of vendor or technology lock-in. The editing interface isn’t tightly coupled to the rendering process anymore; however, how and where your data is stored is still in the hands of the CMS.

One of our requirements was to preserve the content itself in a human-readable and easily accessible form. Storing content in structured Markdown files on GitHub was key to quickly moving forward, making quick updates and choosing combinations of technologies as we see fit. We didn’t want to go through another content migration process.

## Resources

In our journey from a simple startup website to the point where we were powering all of our company’s content with static site generators, we went through a lot of resources.

Phil Hawksworth has been talking about static site generators and their implications for developers and designers for the last two years. His <a href="https://www.youtube.com/watch?v=_cuZcnJIjls">constantly updated talk</a> is the definitive resource if you want to start with static site generation.

<a href="https://stackedit.io/">StackEdit</a> is a wonderful open-source browser-based Markdown editor. In addition to the lovely interface, it also features a lot of integration with data-storage platforms such as GitHub and Dropbox.

A ton of static site generators are out there. <a href="https://www.staticgen.com/">StaticGen</a> gives a good overview and might help you find the right tool for the job.

## Conclusion

Static site generators are wonderful, even though they have to deal with work for which they weren’t initially created for. To avoid trading one big monolith for another, **keep your tasks for the static site generator clear and manageable**. Splitting up tasks and keeping parts of the build process interchangeable will help you if one part doesn’t serve its purpose anymore.

In addition to the technical challenges, the human factor is also critical. People have to see the benefits of working in a rather unfamiliar environment. Take care and provide aid where necessary for them to get going and become more productive than ever.

### <span class="rh">Further Reading</span> on SmashingMag:

* [Content Modeling With Jekyll](https://www.smashingmagazine.com/2016/02/content-modeling-with-jekyll/)
* [Build A Blog With Jekyll And GitHub Pages](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/)
* [Why Static Website Generators Are The Next Big Thing](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/)
* [Static Website Generators Reviewed: Jekyll, Middleman, Roots, Hugo](https://www.smashingmagazine.com/2015/11/static-website-generators-jekyll-middleman-roots-hugo-review/)
* [Automating Style Guide-Driven Development](https://www.smashingmagazine.com/2015/03/automating-style-guide-driven-development/)

{{< signature "vf, il, al" >}}

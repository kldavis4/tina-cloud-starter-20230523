---
title: 'Django Highlights: Wrangling Static Assets And Media Files (Part 4)'
slug: django-highlights-wrangling-static-assets-media-files-part-4
author: philip-kiely
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bedd9e6f-8a44-45d6-9ed5-90501c3dd800/django-highlights-wrangling-static-assets-media-files-part-4.png
date: 2020-06-25T12:30:00.000Z
summary: >-
  Front-end developers and designers create amazing static assets for web applications. Today, we’re focusing on what happens after the style hotfix or beautiful graphic you just finished is pushed to master. We’ll also investigate handling files that users upload, called media files. Together, we’ll develop an intuition for the strategies available to Django developers for serving these files to users worldwide in a secure, performant, and cost-effective manner.
description: >-
  Front-end developers and designers create amazing static assets for web applications. In this article, we’re focusing on what happens after the style hotfix or beautiful graphic you just finished is pushed to master.
categories:
  - Performance
  - Tools
  - Django
---

Django websites involve a lot of files. It’s not just source code for the configuration, models, views, and templates, but also static assets: CSS and JavaScript, images, icons. As if that wasn’t enough already, sometimes users come along and want to upload their own files to your website. It’s enough to make any developer incredulous. Files everywhere!

Here’s where I wish I could say (without caveats): “Don’t worry, Django has your back!” But unfortunately, when dealing with static assets and media files, there are a *lot* of caveats to deal with.

Today, we’ll address storing and serving files for both single-server and scalable deployments while considering factors like compression, caching, and availability. We’ll also discuss the costs and benefits of CDNs and dedicated file storage solutions.

**Note**: *This is not a tutorial on how to deploy a Django site to any specific platform. Instead, like the other articles in the Django Highlights series (see below), it’s intended as a guide for front-end developers and designers to understand other parts of the process of creating a web application. Today, we’re focusing on what happens after the style hotfix or beautiful graphic you just finished is pushed to master. Together, we’ll develop an intuition for the strategies available to Django developers for serving these files to users worldwide in a secure, performant, and cost-effective manner.*

### <span class="rh">Previous Parts</span> In The Series:

- [Part 1](https://www.smashingmagazine.com/2020/02/django-highlights-user-models-authentication/): User Models And Authentication
- [Part 2](https://www.smashingmagazine.com/2020/04/django-highlights-templating-saves-lines/): Templating Saves Lines
- [Part 3](https://www.smashingmagazine.com/2020/04/django-highlights-models-admin-relational-database/): Models, Admin, And Harnessing The Relational Database

{{% feature-panel %}}

## Definitions

Most of these terms are pretty straightforward, but it’s worth taking a moment to establish a shared vocabulary for this discussion.

The three types of files in a live Django application are:

1. **Source Code**  
The Python and HTML files that are created with the Django framework. These files are the core of the application. Source code files are generally pretty small, measured in kilobytes.
2. **Static Files**  
Also called "static assets," these files include CSS and JavaScript, both written by the application developer and third-party libraries, as well as PDFs, software installers, images, music, videos, and icons. These files are only used client-side. Static files range from a few kilobytes of CSS to gigabytes of video.
3. **Media Files**  
Any file uploaded by a user, from profile pictures to personal documents, is called a media file. These files need to be securely and reliably stored and retrieved for the user. Media files can be of any size, the user might upload a couple of kilobytes of plaintext to a few gigabytes of video. If you’re on the latter end of this scale, you probably need more specialized advice than this article is prepared to give.

The two types of Django deployments are:

1. **Single-Server**  
A single-server Django deployment is exactly what it sounds like: everything lives on a single server. This strategy is very simple and closely resembles the development environment, but cannot handle large or inconsistent amounts of traffic effectively. The single-server approach is only applicable for learning or demonstration projects, not real-word applications that require reliable uptime.
2. **Scalable**  
There are lots of different ways to deploy a Django project that allows it to scale to meet user demand. These strategies often involve spinning up and down numerous servers and using tools like load balancers and managed databases. Fortunately, we can effectively lump everything more complex than a single-server deployment into this category for the purposes of this article.

## Option 1: Default Django

Small projects benefit from simple architecture. Django’s default handling of static assets and media files is just that: simple. For each, you have a root folder that stores the files and lives right next to the source code on the server. Simple. These root folders are generated and managed mostly through the *yourproject/settings.py* configuration.

### Static Assets

The most important thing to understand when working with static files in Django is the `python manage.py collectstatic` command. This command rifles through the *static* folder of each app in the Django project and copies all static assets to the root folder. Running this command is an important part of deploying a Django project. Consider the following directory structure:

<pre><code class="language-py">- project
  - project
    - settings.py
    - urls.py
    - ...
  - app1
    - static/
      - app1
        - style.css
        - script.js
        - img.jpg
    - templates/
    - views.py
    - ...
  - app2
    - static/
      - app2
        - style.css
        - image.png
    - templates/
    - views.py
    - ...</code></pre>

Also assume the following settings in *project/settings.py*:

<pre><code class="language-py">STATIC_URL = "/static/"
STATIC_ROOT = "/path/on/server/to/djangoproject/static"</code></pre>

Running the `python manage.py collectstatic` command will create the following folder on the server:

<pre><code class="language-py">- /path/on/server/to/djangoproject/static
  - app1
    - style.css
    - script.js
    - img.jpg
  - app2
    - style.css
    - image.png</code></pre>

Notice that within each static folder, there’s another folder with the app’s name. This is to prevent namespacing conflicts after the static files are collected; as you can see in the above file structure this keeps *app1/style.css* and *app2/style.css* distinct. From here, the application will look for static files in this structure at the `STATIC_ROOT` during production. As such, reference static files as follows in a template in *app1/templates/*:

<div class="break-out">

<pre><code class="language-css">{% load static %}
&lt;link rel="stylesheet" type="text/css" href="{% static "app1/style.css" %}"&gt;</code></pre>
</div>

Django automatically figures out where to get the static file from in development to model this behavior, you do not need to run `collectstatic` during development.

For more details, see [the Django documentation](https://docs.djangoproject.com/en/3.0/howto/static-files/).
 
### Media Files

Imagine a professional networking site with a database of users. Each of those users would have an associated profile, which might contain, among other things, an avatar image and a resume document. Here’s a short example model of that information:

<pre><code class="language-py">from django.db import models
from django.contrib.auth.models import User

def avatar_path(instance, filename):
    return "avatar_{}_{}".format(instance.user.id, filename)

class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    resume = models.FileField(upload_to="path/string")
    avatar = models.ImageField(upload_to=avatar_path)</code></pre>

For this to work, you need the following options in *project/settings.py*, like with static assets:

<pre><code class="language-py">MEDIA_URL = "/media/"
MEDIA_ROOT = "/path/on/server/to/media"</code></pre>

An `ImageField` inherits from `FileField`, so it shares the same parameters and capabilities. Both fields have an optional `upload_to` argument, which takes a string that is a path and appends it to the `MEDIA_ROOT` to store the file, which is then accessible by the same path on top of `MEDIA_URL`. The `upload_to` argument can also take a function that returns a string, as demonstrated with the `avatar_path` function.

Make sure to omit the media files directory and its contents from version control. Its contents may conflict when two developers test the same application on different machines, and it is, unlike static assets, not a part of the deployable Django application.

{{% ad-panel-leaderboard %}}

## Option 2: Django With Services

My guiding philosophy is to use tools for what they’re best at. Django is an amazing framework, and it provides great tooling out of the box for user authentication, server-side rendering, working with models and forms, administrative functions, and dozens of other essential aspects of building web applications. However, its tooling for handling static assets and media files is not, in my opinion, well-suited for production on scalable sites. The Django core developers recognize that many people choose alternate approaches to handling these files in production; the framework is very good at getting out of your way when you do. Most Django sites intended for general use will want to incorporate static assets and handle media files using these non-Django-specific approaches.

### Static Assets On A CDN

While small-to-medium projects can get away without one, a CDN (content delivery network) is easy to use and improves the performance of applications of any size. A CDN is a network of servers, generally worldwide, that distributes and serves web content, mostly static assets. Popular CDNs include [Cloudflare CDN](https://www.cloudflare.com/cdn/), [Amazon CloudFront](https://aws.amazon.com/cloudfront/), and [Fastly](https://www.fastly.com/products/cdn). To use a CDN, you upload your static files, then in your application reference them as follows:

<div class="break-out">

<pre><code class="language-py">&lt;link rel="stylesheet" type="text/css" href="https://cdn.example.com/path/to/your/files/app1/style.css"&gt;</code></pre>
</div>

This process is easy to integrate with your Django deployment scripts. After running the `python manage.py collectstatic` command, copy the generated directory to your CDN (a process that varies substantially based on the service you’re using), then remove the static assets from the Django deployment package.

In development, you’ll want to access different copies of your static assets than in production. This way, you can make changes locally without affecting the production site. You can either use local assets or run a second instance of the CDN to deliver the files. Configure *yourproject/settings.py* with some custom variable, like `CDN_URL`, and use that value in your templates to ensure you’re using the correct version of assets in development and production.

One final note is that many libraries for CSS and JavaScript have free CDNs that most websites can use. If you’re loading, say, Bootstrap 4 or underscore.js, you can skip the hassle of using your own copy in development and the expense of serving your own copies in production by using these public CDNs.

### Media Files with a Dedicated Filestore

No production Django site should store user files in a simple */media/* folder somewhere on the server that runs the site. Here are three of the many reasons why not to:

1. If you need to scale up the site by adding multiple servers, you need some way of copying and syncing the uploaded files across those servers.
2. If a server crashes, the source code is backed up in your version control system, but media files aren’t backed up by default, unless you configured your server to do so, but for that effort you’d be better off using a dedicated filestore.
3. In case of malicious activity, it’s somewhat better to keep user-uploaded files on a separate server from the one running the application, although this in no way removes the requirement to validate user-uploaded files.

Integrating a third party to store your user-uploaded files is really easy. You don’t need to change anything in your code, except maybe removing or modifying the `upload_to` value of `FileField`s in your models, and configuring a few settings. For example, if you were planning to store your files in AWS S3, you’d want to do the following, which is very similar to the process of storing files with Google Cloud, Azure, Backblaze, or similar competing services.

First, you’ll need to install the libraries `boto3` and `django-storages`. Then, you need to set up a bucket and IAM role on AWS, which is outside the scope of this article, but you can see [instructions for here](https://docs.aws.amazon.com/AmazonS3/latest/dev/walkthrough1.html). Once all of that is configured, you need to add three variables to your *project/settings.py*:

<div class="break-out">

<pre><code class="language-py">DEFAULT_FILE_STORAGE = "storages.backends.s3boto3.S3Boto3Storage"
AWS_STORAGE_BUCKET_NAME = "BUCKET_NAME"
AWS_S3_REGION_NAME = "us-east-2"</code></pre>
</div>

Additionally, you will need to set up credential access to your AWS bucket. Some tutorials will demonstrate adding an ID and secret key to your settings file or as environment variables, but these are insecure practices. Instead, use `django-storages` with the AWS CLI to configure the keys, as described [here](https://docs.aws.amazon.com/cli/latest/reference/configure/). You may also be interested in the `django-storages` [documentation](https://django-storages.readthedocs.io/en/latest/backends/amazon-S3.html).

You don’t want development or testing media files to get mixed up with uploads from actual users. Avoiding this is pretty simple: set up multiple buckets, one for development (or one for each developer), one for testing, and one for production. Then, all you need to change is the `AWS_STORAGE_BUCKET_NAME` setting per environment and you’re good to go.

{{% ad-panel-leaderboard %}}
 
## Performance And Availability

There are numerous factors that affect the performance and reliability of your website. Here are some important ones when considering static and media files that matter regardless of which approach you take to managing them.

### Cost

Serving files to a user costs money for two reasons: storage and bandwidth. You have to pay the hosting provider to store the files for you, but you also have to pay them to serve the files. Bandwidth is substantially more expensive than storage (for example, AWS S3 charges 2.3 cents per gigabyte for storage versus 9 cents per gigabyte of data transfer out to the Internet at the time of writing). The economics of a file store like S3 or a CDN are different than the economics of a generalized host like a Digital Ocean droplet. Take advantage of specialization and economies of scale by moving expensive files to services designed for them. Furthermore, many file stores and CDNs offer free plans so sites that might be small enough to get away without using them can instead do so and reap the benefits without any additional infrastructure costs.

### Compression and Transcoding

Most of the problems caused by static assets like photos and videos are because they are big files. Naturally, developers address this by trying to make these files smaller. There are a number of ways to do this using a mix of [compression](https://en.wikipedia.org/wiki/Data_compression) and [transcoding](https://en.wikipedia.org/wiki/Transcoding) in two general categories: lossless and lossy. Lossless compression retains the original quality of the assets but provides relatively modest decreases in file size. Lossy compression, or transcoding into a lossy format, allows for much smaller file sizes at the expense of losing some of the quality of the original artifact. An example of this is transcoding video to a lower bitrate. For details, check out [this article about optimizing video delivery](https://www.smashingmagazine.com/2018/10/video-playback-on-the-web-part-2/). When serving large files over the web, bandwidth speeds often demand that you serve highly compressed artifacts, requiring lossy compression.

Unless you’re YouTube, compression and transcoding doesn’t happen on the fly. Static assets should be appropriately formatted prior to deployment, and you can enforce basic file type and file size restrictions on user uploads to ensure sufficient compression and appropriate formatting in your users' media files.

### Minification

While files of JavaScript and CSS aren’t usually as large as images, they can often be compressed to squeeze into fewer bytes. This process is called [minification](https://en.wikipedia.org/wiki/Minification_(programming)). Minification does not change the encoding of the files, they’re still text, and a minified file still needs to be valid code for its original language. Minified files retain their original extensions.

The main thing removed in a minified file is unnecessary whitespace, and from the computer’s perspective almost all whitespace in CSS and JavaScript is unnecessary. Minification schemes also shorten variable names and remove comments.

Minification by default obfuscates code; as a developer, you should work exclusively with non-minified files. Some automatic step during the deployment process should minify the files before they are stored and served. If you’re using a library provided by a third-party CDN, make sure you’re using the minified version of that library if available. HTML files can be minified, but as Django uses server-side rendering, the processing cost of doing so on the fly would most likely outweigh the small decrease in page size.

### Global Availability

Just like it takes less time to send a letter to your neighbor than it does to send it across the country, so to does it take less time to transmit data nearby than across the world. One of the ways that a CDN improves page performance is by copying assets onto servers across the world. Then, when a client makes a request, they receive the static assets from the nearest server (often called an edge node), decreasing load times. One of the advantages to using a CDN with a Django site is decoupling the global distribution of your static assets from the global distribution of your code.

### Client-Side Caching

What’s better than having a static file on a server near your user? Having the static file already stored on your user’s device! Caching is the process of storing the results of a computation or request so that they can be accessed repeatedly more quickly. Just like a CSS stylesheet can be cached around the world in a CDN, it can be cached in the client’s browser the first time they load a page from your site. Then, the stylesheet is available on the device itself in subsequent requests, so the client is making fewer requests, improving page load time, and decreasing bandwidth use.

Browsers perform their own caching operations, but if your site enjoys substantial traffic, you can optimize your client-side caching behavior using [Django’s cache framework](https://docs.djangoproject.com/en/3.0/topics/cache/).

## In Conclusion

Again, my guiding philosophy is to use tools for what they’re best at. Single-server projects and small scalable deployments with only lightweight static assets can use Django’s built-in static asset management, but most applications should separate out assets to be served over a CDN.

If your project is intended for any kind of real-word use, do not store media files with Django’s default method, instead use a service. With enough traffic, where "enough traffic" is a relatively small number on the scale of the Internet, the additional complications to architecture, the development process, and deployment are more than worth it for the performance, reliability, and cost savings of using a separate CDN and file storage solution for static and media files, respectively.

### <span class="rh">Recommended Reading</span>

- [Part 1](https://www.smashingmagazine.com/2020/02/django-highlights-user-models-authentication/): User Models And Authentication
- [Part 2](https://www.smashingmagazine.com/2020/04/django-highlights-templating-saves-lines/): Templating Saves Lines
- [Part 3](https://www.smashingmagazine.com/2020/04/django-highlights-models-admin-relational-database/): Models, Admin, And Harnessing The Relational Database

{{< signature "dm, ra, yk, il" >}}

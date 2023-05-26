---
title: Varnish – Speed Up Your Mobile Website
slug: speed-up-your-mobile-website-with-varnish
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3736f520-5b1a-4e5b-91ea-b57b533ad46d/varnish-cache-opt1.png
date: 2013-12-04T13:44:44.000Z
author: rachel-andrew
description: >-
  Imagine that you have just written a post on your blog, tweeted about it and
  watched it get retweeted by some popular Twitter users, **sending hundreds of
  people to your blog at once**. Your excitement at seeing so many visitors talk
  about your post turns to dismay as they start to tweet that your website is
  down — a database connection error is shown.
categories:
  - Mobile
  - Performance
  - Responsive Design
  - Caching
  - Varnish
---
Imagine that you have just written a post on your blog, tweeted about it and watched it get retweeted by some popular Twitter users, sending hundreds of people to your blog at once. Your excitement at seeing so many visitors talk about your post turns to dismay as <strong>they start to tweet that your website is down</strong> — a database connection error is shown.

<img loading="lazy" decoding="async" title="Varnish – Speed Up Your Mobile Website" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bfc5358-a13a-4d0b-ab2d-df912a38ac43/varnish-cache-opt.png" alt="Varnish Magic" width="500" height="349" /><br>
<em>Keep calm and try Varnish to optimize mobile websites. (<a href="https://twitter.com/varnishcache">Image source</a>)</em>

Or perhaps you have been working hard to generate interest in your startup. One day, out of the blue, a celebrity tweets about how much they love your product. The person’s followers all seem to click at once, and many of them find that the domain isn’t responding, or when they try to sign up for the trial, the page times out. Despite your apologies on Twitter, many of the visitors move on with their day, and <strong>you lose much of the momentum of that initial tweet</strong>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Controlling The Cache: Using Edge Side Includes In Varnish](https://www.smashingmagazine.com/2015/02/using-edge-side-includes-in-varnish/)
*   [How To Speed Up Your WordPress Website](https://www.smashingmagazine.com/2014/06/how-to-speed-up-your-wordpress-website/)
*   [HTTPS Everywhere With Nginx, Varnish And Apache](https://www.smashingmagazine.com/2015/09/https-everywhere-with-nginx-varnish-apache/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)

{{% feature-panel %}}

These scenarios are fairly common, and I have noticed in my own work that when content becomes popular via social networks, the proportion of mobile devices that access that content is higher than usual, because many people use their mobile devices, rather than desktop applications, to access Twitter and other social networks. Many of these mobile users access the Web via slow data connections and crowded public Wi-Fi. So, anything you can do to ensure that your website loads quickly will benefit those users.

In this article, I’ll show you <a href="https://www.varnish-cache.org/">Varnish Web application accelerator</a>, a free and simple thing that makes a world of difference when a lot of people land on your website all at once.</p>

## Introducing The Magic Of Varnish

For the majority of websites, even those whose content is updated daily, <strong>a large number of visitors are served exactly the same content</strong>. Images, CSS and JavaScript, which we expect not to change very much — but also content stored in a database using a blogging platform or content management system (CMS) — are often served to visitors in exactly the same way every time.

Visitors coming to a blog from Twitter would likely not all be served exactly the same content — including not only images, JavaScript and CSS, but also content that is created with PHP and with queries to the database before being served as a page to the browser. Each request for that blog’s post would require not only the Web server that serves the file (for example, Apache), but also PHP scripts, a connection to the database, and queries run against database tables.

The number of database connections that can be made and the number of Apache processes that can run are always limited. The greater the number of visitors, the less memory available and the slower each request becomes. Ultimately, users will start to see database connection errors, or the website will just seem to hang, with pages not loading as the server struggles to keep up with demand.

This is where an HTTP cache like Varnish comes in. Instead of requests from browsers directly hitting your Web server, making the server create and serve the pages requested, <strong>requests would first hit the cache</strong>. If the requested page is in the cache, then it is served directly from memory, never touching Apache or the database. If the page is not in the cache, then the request is handed over to Apache as usual, whereupon Apache will create and serve the page, which is then stored in the cache, ready for the next request.

<strong>Serving a page from memory is a lot faster</strong> than serving it from disk via Apache. In addition, the page never needs to touch PHP or the database, leaving those processes free to handle traffic that does require a database connection or some processing. For example, in our second scenario of a startup being mentioned by a celebrity, the majority of people clicking through would check out only a few pages of the website — all of those pages could be in the cache and served from memory. The few who go on to sign up would find that the registration form works well, because the server-side code and database connection are not bogged down by people pouring in from Twitter.</p>

## How Does It Work?

The diagram below shows how a blog post might be served when all requests go to the Apache Web server. This example shows five browsers all requesting the same page, which uses PHP and MySQL.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bc40444-a685-4c9a-9660-5b5b444c098d/no-varnish-opt.png"><img loading="lazy" decoding="async" class="140102 size-full" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12e0dad4-e290-44e6-8f5c-81bb8e87f87d/no-varnish-500-opt.png" alt="When all requests go to the Apache Web server." width="500" height="360" /></a>

<strong>Every HTTP request is served by Apache</strong> — images, CSS, JavaScript and HTML files. If a file is PHP, then it is parsed by PHP. And if content is required from the database, then a database connection is made, SQL queries are run, and the page is assembled from the returned data before being served to the browser via Apache.

If we place Varnish in front of Apache, we would instead see the following:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec482754-41bc-46a1-b9ba-117551ba689b/with-varnish-opt.png"><img loading="lazy" decoding="async" class="140104" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f576aa51-d9f3-42e3-bf5b-65d7d1da5b16/with-varnish-500-opt.png" alt="If we place Varnish in front of Apache." width="500" height="449" /></a>

If the page and assets requested are already cached, then <strong>Varnish serves them from memory — Apache, PHP and MySQL would never be touched</strong>. If a browser requests something that is not cached, then Varnish hands it over to Apache so that it can do the job detailed above. The key point is that Apache needs to do that job only once, because the result is then stored in memory, and when a second request is made, Varnish can serve it.

The tool has other benefits. In Varnish terminology, when you configure Apache as your Web server, you are configuring a “back end.” Varnish allows you to configure multiple back ends. So, you might want to run two Web servers — for example, using Apache for PHP pages while serving static assets (such as CSS files) from nginx. You can set this up in Varnish, which will pass the request through to the correct server. In this tutorial, we will look at the simplest use case.</p>

## I’m Sold! How Do I Get Started?

Varnish is really easy to install and configure. You will need root, or <code>sudo</code>, access to your server to install things on it. Therefore, your website needs to be hosted on a virtual private server (VPS) or the like. You can get a VPS very inexpensively these days, and Varnish is a big reason to choose a VPS over [shared hosting](https://inmotion-hosting.evyy.net/c/1233229/260033/4222).

Some CMS’ have plugins that work with Varnish or that integrate it in the control panel — usually to make clearing the cache easier. But you can put Varnish in any CMS or any static website, without any particular integration with other systems.

I’ll walk you through installing Varnish, assuming that you already run Apache as a Web server on your system. I run Debian Linux, but packages for other distributions are available. (The paths to files on the system will vary with the Linux distribution.)

Before starting, <strong>check that Apache is serving your website as expected</strong>. If the server is brand new or you are trying out Varnish on a local virtual machine, make sure to configure a virtual host and that you can view a test page on the server using a browser.</p>

## Install Varnish

Installation instructions for various platforms are in <a href="https://www.varnish-cache.org/docs">Varnish’s documentation</a>. I am using Debian Wheezy; so, as root, I followed the <a href="https://www.varnish-cache.org/installation/debian">instructions for Debian</a>. Once Varnish is installed, you will see the following line in the terminal, telling you that it has started successfully.

<pre><code class="language-c">
[ ok ] Starting HTTP accelerator: varnishd.
</code></pre>

By default, Apache listens for requests on port <code>80</code>. This is where incoming HTTP requests go, because we want Varnish to essentially sit in front of Apache. We need to configure Varnish to listen on port <code>80</code> and change Apache to a different port — usually <code>8080</code>. We then tell Varnish where Apache is.</p>

## Reconfigure Apache

To change the port that Apache listens on, open the file <code>/etc/apache2/ports.conf</code> as root, and find the following lines:

<pre><code class="language-c">
NameVirtualHost *:80
Listen 80
</code></pre>

Change these lines to this:

<pre><code class="language-c">
NameVirtualHost *:8080
Listen 8080
</code></pre>

If you see the following lines, just change <code>80</code> to <code>8080</code> in the same way.

<pre><code class="language-c">
NameVirtualHost 127.0.0.1:80
Listen 80
</code></pre>

Save this file and open your default virtual host file, which should be in <code>/etc/apache2/sites-available</code>. In this file, find the following line:

<pre><code class="language-c">
&lt;VirtualHost *:80&gt;
</code></pre>

Change it to this:

<pre><code class="language-c">
&lt;VirtualHost *:8080&gt;
</code></pre>

You will also need to make this change to any other virtual hosts you have set up.

## Configure Varnish

Open the file <code>/etc/default/varnish</code>, and scroll down to the uncommented section that starts with <code>DAEMON_OPTS</code>. Edit this so that it looks like the following block, which will make Varnish listen on port <code>80</code>.

<pre><code class="language-c">
DAEMON_OPTS="-a :80
-T localhost:1234
-f /etc/varnish/default.vcl
-S /etc/varnish/secret
-s malloc,256m"
</code></pre>

Open the file <code>/etc/varnish/default.vcl</code>, and check that the default back end is set to port <code>8080</code>, because this is where Apache will be now.

<pre><code class="language-c">
backend default {
  .host = "127.0.0.1";
  .port = "8080";
}
</code></pre>

Restart Apache and Varnish as root with the following commands:

<pre><code class="language-bash">
service apache2 restart
service varnish restart
</code></pre>

Check that your test website is still available. If it is, then you’ll probably be wondering <strong>how to test that it is being served from Varnish</strong>. There are a few ways to do this. The simplest is to use cURL. In the command line, type the following:

<pre><code class="language-bash">
curl https://yoursite.com --head
</code></pre>

The response should be something like <code>Via: 1.1 varnish</code>.

You can also look at the statistics generated by Varnish. In the command line, type <code>varnishstat</code>, and watch the hit rate increase as you refresh your page in the browser. Varnish refers to something it can serve as a “hit” and something it passes to Apache or another back end as a “miss.”

Another useful tool is varnish-top. Type <code>varnishtop -i txurl</code> in the command line, and refresh your page in the browser. This tool shows you which files are being served by Varnish.</p>

## Purging The Cache

Now that pages are being cached, if you change an HTML or CSS file, you won’t see the changes immediately. This trips me up all of the time. I know that a cache is in front of Apache, yet every so often I still have that baffled moment of “Where are my changes?!” Type <code>varnishadm "ban.url ."</code> in the command line to clear the entire cache.

You can also control Varnish over HTTP. Plugins are available, such as <a href="https://wordpress.org/plugins/varnish-http-purge/">Varnish HTTP Purge</a> for WordPress, that you can configure to purge the cache directly from the administration area.</p>

## Some Simple Customizations

You’ll probably want to know a few things about how Varnish works by default in order to tweak it. Configuring it as described above should cause most basic assets and pages to be served from the cache, once those assets have been cached in memory.

Varnish <strong>will only cache things that are safe to do so</strong>, and it might not cache some common things that you think it would. A good example is cookies.

In its default configuration, Varnish will not cache content if a cookie is set. So, if your website serves different content to logged-in users, such as personalized content, you wouldn’t want to serve everyone content that is meant for one user. However, you’d probably want to ignore some cookies, such as for analytics. If the website does not serve any personalized content, then the only cookies you would probably care about are those set for your admin area — it would be inconvenient if Varnish cached the admin area and you couldn’t see changes.

Let’s edit <code>/etc/varnish/default.vcl</code>. Assuming your admin area is at <code>/admin</code>, you would add the following:

<pre><code class="language-c">
sub vcl_recv {
  if ( !( req.url ~ ^/admin/) ) {
    unset req.http.Cookie;
  }
}
</code></pre>

Some cookies might be important — for example, logged-in users should get uncached content. So, <strong>you don’t want to eliminate all cookies</strong>. A trip to the land of regular expressions is required to identify the cookies we’ll need. Many recipes for doing this can be found with a quick search online. For analytics cookies, you could add the following.

<pre><code class="language-c">
sub vcl_recv {
  // Remove has_js and Google Analytics __* cookies.
  set req.http.Cookie = regsuball(req.http.Cookie, "(^|;s*)(_[_a-z]+|has_js)=[^;]*", "");
  // Remove a ";" prefix, if present.
  set req.http.Cookie = regsub(req.http.Cookie, "^;s*", "");
}
</code></pre>

Varnish has a section in its documentation on “<a href="https://www.varnish-cache.org/docs/3.0/tutorial/cookies.html">Cookies</a>.”

In most cases, configuring Varnish as described above and removing analytics cookies will dramatically speed up your website. Once Varnish is up and running and you are familiar with the logs, you can start to tweak the configuration and get more performance from the cache.</p>

## Next Steps

To learn more, go through <a href="https://www.varnish-cache.org/docs/3.0/tutorial/index.html">Varnish’s documentation</a>. You should understand enough of Varnish’s basics by now to try some of the examples. The section on “<a href="https://www.varnish-cache.org/docs/3.0/tutorial/increasing_your_hitrate.html">Achieving a High Hit Rate</a>” is well worth a read for the simple tips on tweaking your configuration.

{{< signature "al, ea, il" >}}


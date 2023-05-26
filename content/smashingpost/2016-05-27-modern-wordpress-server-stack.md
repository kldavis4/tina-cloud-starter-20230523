---
title: A Look At The Modern WordPress Server Stack
slug: modern-wordpress-server-stack
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6e50b72-eee0-4936-af85-a18e0c243ccd/lamp-stack-preview-opt.png
date: 2016-05-27T15:46:03.000Z
author: carlalexander
description: >-
  **Editor's Note**: _Today marks a special day for WordPress. Powering many
  websites (and yes, Smashing Magazine is one of them), it celebrates its 13th
  birthday today. Happy birthday, dear WordPress! Here's to many more!_

  Do you remember when you could run a “fast” WordPress website with just an
  Apache server and PHP? Yeah, those were the days! Things were a lot less
  complicated back then.

  Now, everything has to load lightning-fast! Visitors don’t have the same
  expectations about loading times as they used to. A slow website can have
  serious implications for you or your client.
categories:
  - WordPress
  - Backend
  - Caching
  - Varnish
  - Nginx
---
Do you remember when you could run a “fast” WordPress website with just an Apache server and PHP? Yeah, those were the days! Things were a lot less complicated back then.

Now, everything has to load lightning-fast! Visitors don’t have the same expectations about loading times as they used to. A slow website can have serious implications for you or your client.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Proper WordPress Filesystem Permissions And Ownerships](https://www.smashingmagazine.com/2014/05/proper-wordpress-filesystem-permissions-ownerships/)
*   [Moving A WordPress Website Without Hassle](https://www.smashingmagazine.com/2013/04/moving-wordpress-website/)
*   [How To Develop WordPress Locally With MAMP](https://www.smashingmagazine.com/2011/09/developing-wordpress-locally-with-mamp/)
*   [<span class="headline">Do-It-Yourself Caching Methods With WordPress</span>](https://www.smashingmagazine.com/2012/06/diy-caching-methods-wordpress/)

Consequently, <strong>the WordPress server stack has had to evolve over the years</strong> to keep up with this need for speed. As part of this evolution, a few gears have had to be added to its engine. Some of the older gears have had to change as well.

{{% feature-panel %}}

The result is that the WordPress server stack looks quite different today than it did a few years ago. To better understand it, we’re going to explore this new stack in detail. You’ll see how the various pieces fit together to make a WordPress website fast.</p>

## Overview

Before diving in, let’s zoom out and look at the big picture. What does this new WordPress server stack look like? Well, here’s the answer:

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d5202eb-93d8-47dd-8bbc-2984bbfd5238/wordpress-server-stack-diagram.png"><img loading="lazy" decoding="async" class="alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d5202eb-93d8-47dd-8bbc-2984bbfd5238/wordpress-server-stack-diagram.png" alt="WordPress stack diagram" width="1598" height="211" /></a></figure>

The diagram above gives a good overview of what the modern WordPress server stack looks like. At a high level, we can divide what’s going on into three areas:

*   the request-response cycle between the browser and WordPress;
*   WordPress (which is a script that the PHP runtime executes);
*   the query-result cycle between WordPress and the MySQL database.

The role of the modern WordPress server stack is to optimize these three areas. These optimizations are what make everything load faster. And the best part is that there are several ways to do it. (Yay!)

In most cases, these optimizations involve installing new services on your server. Sometimes, these services will need the help of a plugin to interact with WordPress. There will also be times when you can get away with just installing a plugin. You’ll see a lot of different options throughout this article.</p>

## The Request-Response Cycle

Everything starts with the browser. Let’s say you want to view the home page of <code>modern.wordpress-stack.org</code>. Your browser will start by sending an <a href="https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_message">HTTP request</a> to the web server that hosts it. At the other end, the web server will take your request and turn it into an <a href="https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Response_message">HTTP response</a>.

This first response should always be the HTML content of the home page of <code>modern.wordpress-stack.org</code> (unless there’s an error). However, the job of your browser isn’t done. No, that home page still needs more files, the most common ones being CSS, JavaScript and images files.

So, the browser will send requests for those files. The web server will respond with the requested files (again, as long as there are no errors). This cycle will continue until the browser has enough information to render the home page. The faster this cycle happens, the faster the website will appear to load.

Now, this is an obvious simplification, but it’s how things work for the majority of WordPress websites.

## Optimizing The Request-Response Cycle

All right, this brings us to the obvious question, How do we make a web server perform this cycle faster? This is a great question and is part of the reason why the modern WordPress server stack exists.

The stack exists because you can’t just make a web server faster. A web server is also a dispatcher. It can receive a request and just forward it to other services.

These other services are often the bottleneck of this request-response cycle. With WordPress, this bottleneck is PHP, which is why optimizing the request-response cycle comes down to two things. We want the web server to:

*   receive as few requests as possible,
*   forward as few requests to PHP as possible.

The modern WordPress server stack focuses on this last one. It wants to forward as few requests to PHP as possible. That’ll be the main goal for optimizing the stack.

We focus on the second goal because the stack can’t do much about the first one; it has no direct impact on it. The second one is addressed either by the web server’s configuration or by modern development techniques.</p>

## Stack Elements For The Request-Response Cycle

So, what are the stack elements that will help us reduce the requests forwarded to PHP? Well, two stack elements in particular will help us achieve that goal: the web server and the HTTP cache.</p>

### Web Server

We’ve been speaking quite a bit about web servers already. There are three big players in the web server space:

*   [Apache](https://en.wikipedia.org/wiki/Apache_HTTP_Server)
*   [Internet Information Services](https://en.wikipedia.org/wiki/Internet_Information_Services) (IIS)
*   [nginx](https://en.wikipedia.org/wiki/Nginx)

Together, these make up more than 90% of the market share of web servers on the Internet. We’re going to focus on Apache and nginx. While IIS can be used to run WordPress, it’s not common because it’s available only for Windows, and most WordPress servers use Linux.

This leaves us with Apache and nginx. For all of WordPress’ life, Apache has been the recommended web server. We had the LAMP stack (Linux, Apache, MySQL and PHP), which ran WordPress on both the computer and the server.

But behind the scenes, things were changing. There was a new player in town, and its name was nginx. Automattic and WordPress.com have been using it since 2008. It’s the web server that runs the <a href="https://w3techs.com/blog/entry/25_percent_of_the_web_runs_nginx_including_46_6_percent_of_the_top_10000_sites">largest percentage of high-traffic websites</a> (a lot of which run WordPress). That’s why a lot of high-end hosting companies and top WordPress agencies use it as their web server.

It’s not that Apache is a bad web server. There are Apache experts who can make it run great under a lot of traffic. It just doesn’t do as well out of the box or with the standard WordPress configuration.

Meanwhile, nginx’s sole purpose is to handle a lot of traffic. That’s why <a href="https://en.wikipedia.org/wiki/Igor_Sysoev">Igor Sysoev</a> started the project when he was working at <a href="https://en.wikipedia.org/wiki/Rambler_(portal)">Rambler</a>.

One of the reasons why nginx handles more traffic better is that it uses <a href="https://en.wikipedia.org/wiki/FastCGI">FastCGI</a> to communicate with PHP. What is FastCGI? It’s a protocol that lets PHP run as a service separate from the web server.

Apache doesn’t do this by default. Each time the web server receives a request, it needs to start a PHP runtime process — even for images, JavaScript and CSS. This reduces the number of requests that the server can handle and how fast it can handle them.

This goes against one of the goals of the modern WordPress server stack, which we saw earlier. The stack needs to keep the request-response cycle time as low as possible. Loading PHP for every request, even when it doesn’t need it, goes against this goal. So, if you use Apache, look into FastCGI.

<a href="https://en.wikipedia.org/wiki/HTTP/2"><strong>HTTP/2</strong></a> is another important web server feature you should know about. It’s the next version of HTTP, the protocol that powers our entire request-response cycle.

Before the arrival of HTTP/2, a browser could have only six connections to the web server. And each connection could handle only one request at a time. So, in practice, a request-response cycle was capped at six requests per cycle.

That’s a real problem. Most websites have dozens of requests in their cycle. Developers and system administrators found clever ways to get around this limitation.

One of the better-known workarounds is the practice of combining CSS and JavaScript files. In an ideal scenario, this would bring down the total number of requests for CSS and JavaScript files to two: one for JavaScript and one for CSS.

This isn’t necessary with HTTP/2. HTTP/2 allows an unlimited number of requests per connection. This allows all extra requests after the initial HTML response to happen at the same time.

This has huge performance implications. A lot of the work of optimizing the server stack centers on the request-response cycle. By reducing the number of cycles to only a handful, HTTP/2 has done a tremendous amount of work for us.</p>

### HTTP Cache

The most important part of the modern WordPress server stack is the HTTP cache. In the WordPress world, we also call this page caching. The purpose of the HTTP cache is to cache responses to requests. What does this mean?

Well, let’s go back to our earlier example. The browser sends a request for the home page of <code>modern.wordpress-stack.org</code>, and the web server receives that request and forwards it to PHP.

The problem with this scenario is that the web server is dumb. It’ll always forward all requests it receives to PHP — regardless of whether most of the requests would generate the same response.

This is exactly what happens when visitors aren’t logged in. To the web server, they’re all different requests, but it doesn’t care. It will forward them all to PHP, which will generate the same response for all of them.

That’s terrible! As we saw earlier, PHP is the real bottleneck of our request-response cycle. Your browser can’t send its follow-up requests until it receives that initial home page response. We can’t have the web server forward everything to PHP by default.

That’s where the HTTP cache comes in. It sits between the web server and PHP. Its job is to check every request that the web server receives and look for a cached response. If there isn’t any, it’ll forward the request to PHP and then cache the response that PHP generates.

This drastically reduces the request-response cycle time, making the website load faster. It also lets the web server handle more simultaneous requests without blowing up.</p>

## The Different Flavors Of HTTP Cache

At this point, you should be wondering, “How can I get this baby on my server ASAP?!” The good news is that installing an HTTP cache on a WordPress server is quite easy. It’s the component with the widest range of options.</p>

### Install a Page-Caching Plugin

The easiest way is to install a page-caching plugin. You have a few options to pick from:

*   [Batcache](https://wordpress.org/plugins/batcache/)
*   [Hyper Cache](https://wordpress.org/plugins/hyper-cache/)
*   [Cache Enabler](https://wordpress.org/plugins/cache-enabler/)
*   [WP Rocket](https://wp-rocket.me/)
*   [WP Super Cache](https://wordpress.org/plugins/wp-super-cache/)
*   [W3 Total Cache](https://wordpress.org/plugins/w3-total-cache/)

All but WP Rocket are available as free plugins in the WordPress directory. So, you can install one and test it out right away. That being said, of the four plugins, the best one is WP Rocket. While it’s a paid plugin, it does a lot more than just create an HTTP cache. These other benefits magnify the work that the HTTP cache is doing.</p>

### How Does a Page-Caching Plugin Work?

All of these plugins leverage a drop-in that WordPress has made available for caching. This caching drop-in lets the plugins create an HTTP cache system inside of WordPress. The caching drop-in needs two things to work.

First, the <code>advanced-cache.php</code> drop-in file needs to be in the <code>wp-content</code> folder. That’s the actual file. But unlike most WordPress drop-ins, this one doesn’t kick in by default. WordPress also needs the <code>WP_CACHE</code> constant to be <code>true</code> in order to load the drop-in. In most cases, you would set that in <code>wp-config.php</code>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03f134ee-f2e6-4e20-aaf2-bbff662cd43b/plugin-http-cache-loading-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20e6d4a4-4c0c-4320-8bd9-e106885f5e7c/plugin-http-cache-loading-opt-1.png" alt="Plugin HTTP Cache (loading)" width="600" height="354" /></a></figure>

The diagram above shows what happens when you enable the drop-in with a caching plugin. WordPress loads the drop-in in <code>wp-settings.php</code> during its <a href="https://carlalexander.ca/wordpress-adventurous-loading/">loading process</a>. This is early enough in the process that WordPress hasn’t done anything time-consuming yet.

The caching plugin will then check whether it has already cached the response to the request. If it has, it will return that cached response. If it hasn’t, it will turn on <a href="https://php.net/manual/en/outcontrol.setup.php">PHP output buffering</a>, and WordPress will continue loading.

Now, output buffering is an interesting system. What it does is capture all the output from a PHP script in a string variable until one of two things happen:

*   you tell PHP to stop buffering its output using one of the built-in functions,
*   the PHP script finishes and needs to return a response to the browser.

The caching plugin is counting on the latter scenario. It wants WordPress to do its thing and then cache the whole output before PHP sends it back to the browser. You can see the process in the diagram below.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c65447b7-ff4d-44e4-9ae5-43c0ead32f88/plugin-http-cache-shutdown-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e9d060e-49f5-4737-a71a-368fe1178bb5/plugin-http-cache-shutdown-opt-1.png" alt="Plugin HTTP Cache (shutdown)" width="600" height="257" /></a></figure>

### Have the Web Server Do It

The next option is to add an HTTP cache at the web server level. The way it works is that the web server will cache all responses to requests that get forwarded to PHP. This solution is better than a caching plugin because it doesn’t need to touch PHP at all.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46a361c2-a11b-432f-9c71-13e1f0431b3a/web-server-http-cache-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31dc800f-0098-45cc-b42e-1a3eb520d8ae/web-server-http-cache-opt-1.png" alt="Web server HTTP cache" width="600" height="202" /><br>
</a></figure>

The diagram above gives an overview of what’s going in the web server. The web server receives a request and checks with the HTTP cache. If a response has been cached already, the HTTP cache will send that back.

Otherwise, it will forward the request to the PHP module (usually FastCGI). It will pass the request to WordPress so that it can generate a response. The HTTP cache module will then cache that response on the way back.

Both Apache and nginx come with the ability to add an HTTP cache system. The nginx one is built in. The Apache one is a separate <a href="https://httpd.apache.org/docs/2.4/mod/mod_cache.html">module</a> that you need to add to your Apache installation.

There isn’t a lot of information on how to use the Apache module with PHP or WordPress. That might be because it’s not popular with the Apache crowd, or maybe because it has some issues. There’s at least one <a href="https://bz.apache.org/bugzilla/show_bug.cgi?id=48364">long-standing issue</a> with it that is still open.

Meanwhile, the nginx HTTP cache system is robust and well documented. You can use it as a <a href="https://www.nginx.com/blog/nginx-caching-guide/">normal HTTP cache</a> or as a smaller yet effective <a href="https://www.nginx.com/blog/benefits-of-microcaching-nginx/">micro-cache</a>. It’s just one more reason why nginx is the preferred web server nowadays.</p>

### Add Varnish to the Stack

What is <a href="https://en.wikipedia.org/wiki/Varnish_(software)">Varnish</a>? It’s a dedicated HTTP cache server (or, as its developers like to call it, HTTP accelerator). Most high-traffic websites and premium hosting companies use it as their HTTP cache solution.

They use it because it’s powerful and offers the most flexibility. Varnish has its own configuration language, called VCL. It lets you control every element of the caching process. Varnish also comes with a lot of tools for analyzing what the cache is doing and how it’s performing.

These are the major differences between using it and just using the built-in web server HTTP cache. The built-in web server HTTP cache is super-performant but also pretty basic. You don’t have a lot of control beyond a few configuration options.

Nevertheless, this power and flexibility come at a price. Varnish is also the most complicated HTTP cache option. It does nothing but cache HTTP responses. It <a href="https://www.varnish-cache.org/docs/trunk/phk/ssl_again.html">doesn’t handle SSL termination</a>, which most WordPress developers want (or should want). This means that our modern WordPress server stack is going to be more complex when we use it.

<figure class="fwi"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b590d6c-eee4-4945-9514-af6d236c0c79/varnish-http-cache.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b590d6c-eee4-4945-9514-af6d236c0c79/varnish-http-cache.png" alt="Varnish HTTP cache" /></a></figure>

The diagram above illustrates this extra complexity. We now have two more components in our WordPress server stack: Varnish and a <a href="https://en.wikipedia.org/wiki/Reverse_proxy">reverse proxy</a>.

The reverse proxy is there to overcome the limitation that Varnish has with SSL. It sits in front of Varnish and decrypts the requests that our server receives. You can also call this type of reverse proxy an <a href="https://en.wikipedia.org/wiki/SSL_termination_proxy">SSL termination proxy</a>. The proxy then sends these decrypted requests to Varnish to process.

Once a request hits Varnish, the VCL configuration file(s) kick in. They’re Varnish’s brain. For example, they tell it how to:

*   analyze, clean up and modify incoming requests;
*   look for a cached response;
*   analyze, clean up and modify returning responses from WordPress;
*   cache these returning responses;
*   handle a request to remove one or more responses from the cache.

This last one is especially important. Left to itself, Varnish has no way to know when WordPress wants to remove a page from the cache. So, by default, if you make changes to a post and update it, visitors will keep seeing the same cached page. Luckily for us, a <a href="https://en-ca.wordpress.org/plugins/varnish-http-purge/">plugin exists</a> that removes pages from the Varnish cache.</p>

## WordPress

All right, our request for the home page of <code>modern.wordpress-stack.org</code> has hit WordPress. It went through the request-response cycle that we just covered. The HTTP cache did everything it could to find an HTTP response to send back.

But there was no cached HTTP response to send back to the browser. At that point, the HTTP cache had no other choice. It had to forward the HTTP request to WordPress.

It’s all in WordPress’ hands now. WordPress has to turn our HTTP request into an HTTP response and send it back to the HTTP cache. As we saw earlier, this is the main bottleneck of our whole modern WordPress server stack.

The cause of this bottleneck is two-fold. WordPress has a lot PHP code to execute. This is time-consuming, and the slower PHP is at doing it, the longer it takes.

The other bottleneck is the database queries that WordPress needs to perform. Database queries are expensive operations. The more there are, the slower WordPress gets. This will be the focus of the last section on the query-result cycle.</p>

## Optimizing The PHP Runtime

Let’s get back to PHP. At this moment, WordPress has a minimum requirement of PHP 5.2. This version of PHP is almost 10 years old! (The PHP team stopped supporting it in 2011.)

The PHP team hasn’t been sitting idle all those years. Numerous performance improvements have been made, especially over the last few years. Let’s look at what you can do to optimize it nowadays.</p>

### Use the Latest Version of PHP

The easiest thing you can do is upgrade your version of PHP. Versions 5.4, 5.5 and 5.6 all saw performance improvements. The largest improvement was from 5.3 to 5.4. Switching to it increased the performance of WordPress by a decent amount.</p>

### Install Opcode Caching

Opcode caching is another way to speed up PHP. As a <a href="https://en.wikipedia.org/wiki/Server-side_scripting">server-side scripting</a> language, PHP has a big flaw: It needs to compile a PHP script each time it executes it.

The solution to this problem is to cache the compiled PHP code. That way, PHP doesn’t have to compile it each time it executes it. This is the job of the <a href="https://php.net/manual/en/intro.opcache.php">opcode cache</a>.

Before PHP 5.5, PHP didn’t come bundled with an opcode cache. You had to install it yourself on the server. This is another reason why using a more recent version of PHP is better.</p>

### Switch to a Next-Generation Compiler

The last thing you can do is switch to one of the two next-generation compilers: either Facebook’s <a href="https://hhvm.com/">HHVM</a> or <a href="https://php7.zend.com/">PHP 7</a>, the latest version of PHP. (Why PHP 7? It’s a long story.)

Facebook and the PHP team built these two compilers from the ground up. They wanted to leverage more modern compilation strategies. HHVM uses <a href="https://en.wikipedia.org/wiki/Just-in-time_compilation">just-in-time compilation</a>, whereas PHP 7 uses <a href="https://en.wikipedia.org/wiki/Ahead-of-time_compilation">ahead-of-time compilation</a>. Both offer <a href="https://wpengine.com/blog/php-7-the-way-of-the-future/">incredible performance improvements</a> over good ol’ PHP 5.

HHVM was the first one to arrive on the scene a few years ago. A lot of top-tier hosts have had a lot of success with it, offering it as their primary PHP compiler.

It’s worth stressing, though, that HHVM isn’t an official PHP compiler. It’s not 100% compatible with PHP. The reason is that HHVM isn’t just designed to support PHP; it is also a compiler for Facebook’s <a href="https://en.wikipedia.org/wiki/Hack_(programming_language)">Hack</a> programming language.

PHP 7 is an official PHP compiler. It hasn’t been around for a long time. The PHP team released it in <a href="https://php.net/archive/2015.php#id2015-12-03-1">December of 2015</a>. This hasn’t prevented some WordPress hosting companies from supporting it already.

The good news is that WordPress itself is 100% compatible with both compilers! The bad news is that not all plugins and themes are, because the minimum PHP version for WordPress is still 5.2.

Nothing is forcing authors to make their plugins or themes work with these compilers. So, you can’t go all in with one of them. Your stack should always fall back to PHP 5.</p>

## Query-Result Cycle

At this point, the PHP runtime is going through all of the WordPress PHP files and executing them. However, these WordPress PHP files don’t contain any data. They only contain the WordPress code.

The problem is that WordPress stores all of its data in a MySQL database. So, to get to it, the PHP runtime needs to query that database. The MySQL server returns the result of that query, and the PHP runtime then continues to execute the WordPress PHP files… well, that is, until it needs data again.

This back and forth can happen from a few dozen times to a few hundred times. (You might want to speak with your developer if it’s the latter!) That’s why it’s a major bottleneck.</p>

## Optimizing The Query-Result Cycle

The optimization goal here is to speed up the execution time of WordPress files by PHP. This is where database queries are problematic. They tend to take more time than just running plain PHP code (unless your code is doing something outrageous).

The obvious way to fix this problem is to reduce the number of queries that WordPress needs to perform. And that’s always worthwhile! But it’s not something the modern WordPress server stack can help with.

We might not be able to reduce the number of queries that WordPress makes, but we aren’t out of options either. There are still two ways that the stack can help us optimize the query-result cycle. It can reduce the number of queries made to the database in the first place. And for those queries that make it to the database, it can decrease the time it takes to run them.

These two options are both meant to do the same thing: make PHP wait as little as possible for results from the database, which will make WordPress itself faster.</p>

## Stack Elements For The Query-Result Cycle

Let’s look at the different stack elements involved in the query-result cycle. This part of the stack is less complex. But it still involves more than one component — namely, the MySQL database server and the object cache.</p>

### MySQL Database Server

A few years ago, a MySQL database server would mean the same thing to everyone. It was a server with the <a href="https://en.wikipedia.org/wiki/MySQL">MySQL server</a> installed. But things have changed a lot in recent years.

Various groups weren’t happy with how <a href="https://en.wikipedia.org/wiki/Oracle_Corporation">Oracle</a> was managing the MySQL project. So, each group forked it and created its own version that you could “drop in” instead. The result is that there are now several MySQL database servers.

The new “official” MySQL server is the <a href="https://en.wikipedia.org/wiki/MariaDB">MariaDB server</a>. It’s the community-developed version of MySQL server. The community plans to maintain full compatibility with the MySQL server project.

Another popular alternative to MySQL is the <a href="https://en.wikipedia.org/wiki/Percona_Server">Percona server</a>. Unlike MariaDB, Percona is more of a branch of MySQL. Its developers aren’t against the MySQL project itself; they just want to focus on improving MySQL’s performance. The MariaDB team later merged some of these performance improvements into the MariaDB project.

At the end of the day, you can pick the one you prefer. There’s no difference in performance between a Percona server and a MariaDB server (for most of us anyhow). They both perform better than MySQL. Percona does, however, maintain closer compatibility with the Oracle project.

What does affect performance is the <a href="https://en.wikipedia.org/wiki/Database_engine"><strong>storage engine</strong></a> that the WordPress database uses. The storage engine controls how the database server manages the data it stores. You can also set a different storage engine per database table; you don’t have to use the same one for the entire database.

A database server has several storage engines. We’re not going to look at all of them. Only two interest us: <a href="https://en.wikipedia.org/wiki/InnoDB">InnoDB</a> and <a href="https://en.wikipedia.org/wiki/MyISAM">MyISAM</a>.

By default, WordPress uses the default MySQL database engine. Before MySQL 5.5, that engine was MyISAM. If you run a small WordPress website, then MyISAM is fine. MyISAM runs into performance issues once a website grows in size. At that point, InnoDB is the only choice for a database engine.

The only issue with InnoDB is that it requires some tuning to perform at its best. If you’re running a large database server, you might need to adjust things. Luckily for us, there’s a tool to help with that.

<a href="https://mysqltuner.com/">MySQLTuner</a> is a small script that analyzes your database server. It will generate a report and give you tuning recommendations.</p>

### Object Cache

The brunt of the work of optimizing the query-result cycle lies with the <a href="https://codex.wordpress.org/Class_Reference/WP_Object_Cache">object cache</a>. The job of the object cache is to store data that is time-consuming to get or generate. As you might guess, database queries are a perfect candidate.

WordPress uses the object cache a lot. Let’s say you use <a href="https://codex.wordpress.org/get_option"><code>get_option</code></a> to get an option from the database. WordPress will only query the database for that option once. It won’t query it again the next time someone needs it.

Instead, WordPress will fetch the query result from the object cache. This is a proactive step that WordPress takes to reduce the number of database queries that it needs to make. But it isn’t a foolproof solution.

While WordPress will do its best to leverage the object cache, a plugin or theme doesn’t have to. If a plugin or theme makes a lot of database queries and doesn’t cache the results, the stack can do nothing about it.

In such cases, most of the database queries will come from WordPress itself. So, you’ll get great mileage out of WordPress’s built-in use of the object cache. That’s why it’s an important element of the modern WordPress server stack.

Now, a problem with the object cache is that it doesn’t persist the data it stores by default. It just stores data in memory while PHP is executing all of the WordPress files. But once the PHP process terminates, all of the data that it stored in memory gets cleared.

This isn’t ideal at all. An object cache could stay valid for a long time, so you don’t want to limit it to a single request. The solution is to <strong>use a persistent object cache</strong>.

A persistent object cache often comes in the form of a plugin. That plugin would make use of the <code>object-cache.php</code> drop-in to do its job. This drop-in lets plugin authors change the default behavior of the object cache.

The plugins then connect the object cache to a persistent data store. They do that by replacing the fetch and save functionality of the default object cache. Instead of saving and fetching data to memory, the object cache does it from that store.</p>

## Persistent Object Cache Plugins

Nowadays, there are two popular data store options for persistent object caching:

*   [Memcached](https://en.wikipedia.org/wiki/Memcached) ([plugin](https://wordpress.org/plugins/memcached/))
*   [Redis](https://en.wikipedia.org/wiki/Redis) ([plugin](https://wordpress.org/plugins/redis-cache/))

Both of these data stores use <a href="https://en.wikipedia.org/wiki/Random-access_memory">RAM</a> for storage, which makes them lightning-fast. In fact, their performance is comparable to that of the default object cache.

The only problem is that they don’t come preinstalled on servers. And neither does their PHP extension (which is optional with Redis). You need to install one before you can use the corresponding WordPress plugin.

Which one should you install? In practice, there isn’t much of a difference between the two for object caching. In the past, the popular option was Memcached. This has changed over the last few years. Redis has added a lot of features that have made it the go-to option for object caching.</p>

## Getting Your Own Modern WordPress Server

So, how do you get your own server? The obvious way is to get one from a top-tier WordPress hosting companies. These companies want to stay at the forefront of the WordPress hosting business, which motivates them to adopt the latest breakthroughs and technologies.

But what if you want one without breaking the bank? A couple of tools are available to anyone who would rather do it themselves and pay less for hosting. Let’s look at them.</p>

### DebOps for WordPress

<a href="https://github.com/carlalexander/debops-wordpress">DebOps for WordPress</a> is a tool that I built to help anyone build a modern WordPress server. Its mission is to make the modern WordPress server stack <a href="https://carlalexander.ca/give-wordpress-an-apple-experience/">available to anyone in the community</a>. That’s why I’m trying to make it as easy to use as possible. You don’t need any system administration knowledge to use it.

DebOps for WordPress configures a server with the following:

*   HHVM (until PHP 7 makes it into an official Linux repository)
*   MariaDB
*   nginx
*   Redis
*   Varnish

The tool does more than just configure a server with the latest technologies. It also takes care of securing the server for you. This is something that people often overlook when managing their own server.</p>

### EasyEngine

<a href="https://easyengine.io/">EasyEngine</a> is a command-line tool designed to help you set up a WordPress website on a server. The great thing about EasyEngine is its flexibility: You can use it set up almost any combination of server technologies that we’ve looked at so far.

For example, it lets you set up a server with either HHVM or PHP 7. It lets you chose between Memcached and Redis for your persistent data store. And it lets you install administrator tools such as <a href="https://www.phpmyadmin.net/">phpMyAdmin</a>.

It also offers a large number of options when it creates a WordPress website. You can tell it to set up a website with an HTTP cache using a plugin or nginx. All of this flexibility is why EasyEngine is such a popular tool.</p>

### Trellis

<a href="https://roots.io/trellis/">Trellis</a> is a tool developed by <a href="https://roots.io/">Roots</a>. Like DebOps, it configures the server with a specific set of server technologies:

*   MariaDB
*   Memcached
*   nginx
*   nginx HTTP cache (optional)
*   PHP 7

One thing to know about Trellis is its relationship to <a href="https://roots.io/bedrock/">Bedrock</a>, another tool built by Roots. Bedrock is a boilerplate for structuring a WordPress website around the “<a href="https://12factor.net/">Twelve-Factor App</a>” principles.

The Roots team created Trellis to enable people to configure a server that uses Bedrock-structured WordPress website(s). You can’t use it with a normal WordPress installation, so keep that in mind.</p>

## Times Have Changed

As you can see, a WordPress server has a lot more moving parts today! But this doesn’t need to be a cause for despair. It’s not as bad as it looks because you don’t always need to use all of the parts.

That’s why so much of this article discusses how these parts work together. The point is to empower you to make your own decisions. Use this knowledge to decide which parts you need to use and when. In this way, you too will have a fast WordPress website.

{{< signature "ms, al, il" >}}

<em>This article has first been published on <a href="https://carlalexander.ca/modern-wordpress-server-stack/">Carl Alexander's blog</a>.</em>

<em>Front page image credits: <a href="https://pixabay.com/en/cupcakes-wordpress-sweets-sweet-525513/">Pixabay</a></em>


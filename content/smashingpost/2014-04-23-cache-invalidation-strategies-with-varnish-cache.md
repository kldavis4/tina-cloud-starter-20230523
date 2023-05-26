---
title: Cache Invalidation Strategies With Varnish Cache
slug: cache-invalidation-strategies-with-varnish-cache
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cc44cb1-cb34-4484-9020-bdd29adf7978/varnish-cache-500px-opt.png
date: 2014-04-23T18:00:07.000Z
author: per-buer
description: >-
  Phil Karlton once said, "There are only two hard things in Computer Science:
  cache invalidation and naming things." This article is about the harder of
  these two: cache invalidation. It’s directed at readers who already work with
  Varnish Cache. To learn more about it, you’ll find background information in
  “[Speed Up Your Mobile Website With
  Varnish](https://www.smashingmagazine.com/2013/12/04/speed-up-your-mobile-website-with-varnish/).”

  [![varnish-cache](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cc44cb1-cb34-4484-9020-bdd29adf7978/varnish-cache-500px-opt.png)](https://www.smashingmagazine.com/2014/04/23/cache-invalidation-strategies-with-varnish-cache/)

  10 microseconds (or 250 milliseconds): That’s the difference between
  delivering a cache hit and delivering a cache miss. How often you get the
  latter will depend on the efficiency of the cache — this is known as the “hit
  rate.” A cache miss depends on two factors: the volume of traffic and the
  average time to live (TTL), which is a number indicating how long the cache is
  allowed to keep an object. As system administrators and developers, **we can’t
  do much about the traffic, but we can influence the TTL**.
categories:
  - Coding
  - Techniques
  - Optimization
  - Performance
  - Varnish
---
Phil Karlton once said, "There are only two hard things in Computer Science: cache invalidation and naming things." This article is about the harder of these two: <strong>cache invalidation</strong>. It’s directed at readers who already work with Varnish Cache. To learn more about it, you’ll find background information in “<a href="https://www.smashingmagazine.com/2013/12/04/speed-up-your-mobile-website-with-varnish/">Speed Up Your Mobile Website With Varnish</a>.”

<em>10 microseconds (or 250 milliseconds)</em>: That’s the difference between delivering a cache hit and delivering a cache miss. How often you get the latter will depend on the efficiency of the cache — this is known as the “hit rate.” A cache miss depends on two factors: the volume of traffic and the average time to live (TTL), which is a number indicating how long the cache is allowed to keep an object. As system administrators and developers, <strong>we can’t do much about the traffic, but we can influence the TTL</strong>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Controlling The Cache: Using Edge Side Includes In Varnish](https://www.smashingmagazine.com/2015/02/using-edge-side-includes-in-varnish/)
*   [Speed Up Your Mobile Website With Varnish](https://www.smashingmagazine.com/2013/12/speed-up-your-mobile-website-with-varnish/)
*   [HTTPS Everywhere With Nginx, Varnish And Apache](https://www.smashingmagazine.com/2015/09/https-everywhere-with-nginx-varnish-apache/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)

However, to have a high TTL, we need to be able to invalidate objects from the cache so that we avoid serving stale content. With Varnish Cache, there are myriad ways to do this. We’ll explore the most common ways and how to deploy them.

{{% feature-panel %}}

Varnish does a whole lot of other stuff as well, but its caching services are most popular. <strong>Caches speed up Web services by serving cached static content</strong>. When Varnish Cache is delivering a cache hit, it usually just dumps a chunk of memory into a socket. Varnish Cache is so fast that, on modern hardware, we actually measure response time in microseconds!

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1cc44cb1-cb34-4484-9020-bdd29adf7978/varnish-cache-500px-opt.png" alt="Superhero bunny" width="500" height="260" /><br>
<em>Caching isn't always as simple as we think; a few gotchas and problems may take quite some of our time to master. (<a href="https://twitter.com/varnishcache">Image credits</a>)</em>

When using a cache, you need to know when to evict content from the cache. If you have no way to evict content, then you would rely on the cache to time-out the object after a predetermined amount of time. This is one method, but hardly the most optimal solution. The best way would be to let Varnish Cache keep the object in memory forever (mostly) and then tell the object when to refresh. Let’s go into detail on how to achieve this.</p>

## HTTP Purging

HTTP Purging is the most straightforward of these methods. Instead of sending a <code>GET /url</code> to Varnish, you would send <code>PURGE /url</code>. Varnish would then discard that object from the cache. Add an access control list to Varnish so that not just anyone can purge objects from your cache; other than that, though, you’re home free.

<pre><code class="language-c">
acl purge { 
	"localhost";
  	"192.168.55.0"/24; 
}

  sub vcl_recv { 
	# allow PURGE from localhost and 192.168.55...

  	if (req.request == "PURGE") {
 		if (!client.ip ~ purge) { 
			error 405 "Not allowed.";
  		}
 		return (lookup);
 	}
}

  sub vcl_hit { 
	if (req.request == "PURGE") {
 		purge;
 		error 200 "Purged."; 
	}
 }

  sub vcl_miss { 
	if (req.request == "PURGE") { 
		purge;
 		error 200 "Purged.";
 	}
 }
</code></pre>

### Shortcomings of Purging

HTTP purging falls short when a piece of content has a complex relationship to the URLs it appears on. A news article, for instance, might show up on a number of URLs. The article might have a desktop view and a mobile view, and it might show up on a section page and on the front page. Therefore, you would have to either get the content management system to keep track of all of these manifestations or let Varnish do it for you. To let Varnish do it, you would use bans, which we’ll get into now.</p>

## Bans

A ban is a feature specific to Varnish and one that is frequently misunderstood. It enables you to ban Varnish from serving certain content in memory, forcing Varnish to fetch new versions of these pages.

An interesting aspect is <strong>how you specify which pages to ban</strong>. Varnish has a language that provides quite a bit of flexibility. You could tell Varnish to ban by giving the ban command in the command-line interface, typically connecting to it with <code>varnishadm</code>. You could also do it through the Varnish configuration language (VCL), which provides a simple way to implement HTTP-based banning.

Let’s start with an example. Suppose we need to purge our website of all images.

<pre><code class="language-c">
&gt; ban obj.http.content-type ~ “^image/”
</code></pre>

The result of this is that, for all objects in memory, the HTTP response header <code>Content-Type</code> would match the regular expression <code>^image/</code>, which would invalidate immediately.

Here’s what happens in Varnish. First, the ban command puts the ban on the “ban list.” When this command is on the ban list, every cache hit that serves an object older than the ban itself will start to look at the ban list and compare the object to the bans on the list. If the object matches, then Varnish kills it and fetches a newer one. If the object doesn’t match, then Varnish will make a note of it so that it does not check again.

Let’s build on our example. Now, we’ll only ban images that are placed somewhere in the <code>/feature</code> URL. Note the logical “and” operator, <code>&amp;&amp;</code>.

<pre><code class="language-c">
&gt; ban obj.http.content-type ~ “^image/” &amp;&amp; req.url ~ “^/feature”
</code></pre>

You’ll notice that it says <code>obj.http.content-type</code> and <code>req.url</code>. In the first part of the ban, we refer to an attribute of an object stored in Varnish. In the latter, we refer to a part of a request for an object. This might be a bit unconventional, but you can actually use attributes on the request to invalidate objects in cache. Now, <code>req.url</code> isn’t normally stored in the object, so referring to the request is the only thing we can do here. <strong>You could use this to do crazy things</strong>, like ban everything being requested by a particular client’s IP address, or ban everything being requested by the Chromium browser. As these requests hit Varnish, objects are invalidated and refreshed from the originating server.

Issuing bans that depend on the request opens up some interesting possibilities. However, there is one downside to the process: A very long list of bans could slow down content delivery.

There is a worker thread assigned to the task of shortening the list of bans, “the ban lurker”. The ban lurker tries to match a ban against applicable objects. When a ban has been matched against all objects older than itself, it is discarded.

As the ban lurker iterates through the bans, it doesn’t have an HTTP request that it is trying to serve. So, any bans that rely on data from the request cannot be tested by the ban lurker. To keep ban performance up, then, we would recommend not using request data in the bans. If you need to ban something that is typically in the request, like the URL, you can copy the data from the request to the object in <code>vcl_fetch</code>, like this:

<pre><code class="language-c">
set beresp.http.x-url = req.url;
</code></pre>

Now, you’ll be able to use bans on <code>obj.http.x-url</code>. Remember that the <code>beresp</code> objects turn into <code>obj</code> as it gets stored in cache.

## Tagging Content For Bans

Bans are often a lot more effective when you give Varnish a bit of help. If the object has an <code>X-Article-id</code> header, then you don’t need to know all of the URLs that the object is presented as.

For pages that depend on several objects, you could have the content management system add an <code>X-depends-on</code> header. Here, you’d list the objects that should trigger an update of the current document. To take our news website again, you might use this to list all articles mentioned on the front page:

<pre><code class="language-c">
X-depends-on: 3483 4376 32095 28372
</code></pre>

Naturally, then, if one of the articles changes, you would issue a ban, like this:

<pre><code class="language-c">
ban obj.http.x-depends-on ~ “\D4376\D”
</code></pre>

This is potentially very powerful. Imagine making the database issue these invalidation requests through triggers, thus eliminating the need to change the middleware layer. Neat, eh?

## Graceful Cache Invalidations

Imagine purging something from Varnish and then the origin server that was supposed to replace the content suddenly crashes. You’ve just thrown away your only workable copy of the content. What have you done?! Turns out that quite a few content management systems crash on a regular basis.

Ideally, we would want to put the object in a third state — to invalidate it on the condition that we’re able to get some new content. This third state exists in Varnish: It is called “grace,” and it is used with TTL-based invalidations. After an object expires, it is kept in memory in case the back-end server crashes. If Varnish can’t talk to the back end, then it checks to see whether any graced objects match, and it serves those instead.

One Varnish module (or VMOD), named <code>softpurge</code>, allows you to invalidate an object by putting it into the grace state. Using it is simple. Just replace the <code>PURGE</code> VCL with the VCL that uses the <code>softpurge</code> VMOD.

<pre><code class="language-c">
import softpurge;
sub vcl_hit {
	if (req.method == "PURGE") { 
		softpurge.softpurge();
		error 200 “Successful softpurge”;
 	} 
}

sub vcl_miss { 
	if (req.method == "PURGE) {
 		softpurge.softpurge(); 
		error 200 "Successful softpurge";
 	} 
}
</code></pre>

## Distributing Cache Invalidations Events

All of the methods listed above describe the process of invalidating content on a single cache server. Most serious configurations would have more than one Varnish server. If you have two, which should give enough oomph for most websites, then you would want to issue one invalidation event for each server. However, if you have 20 or 30 Varnish servers, then you really wouldn’t want to bog down the application by having it loop through a huge list of servers.

Instead, you would want <strong>a single API end point to which you can send your purges</strong>, having it distribute the invalidation event to all of your Varnish servers. For reference, here is a very simple invalidation service written in shell script. It will listen on port 2000 and invalidate URLs to three different servers (<code>alfa</code>, <code>beta</code> and <code>gamma</code>) using cURL.

<pre><code class="language-c">
nc -l 2000 | while true
	do read url
	for srv in “alfa” “beta” “gamma”
		do curl -m 2 -x $srv -X PURGE $url
	done
done
</code></pre>

It might not be suitable for production because the error handling leaves something to be desired!

<strong>Cache invalidation</strong> is almost as important as caching. Therefore, having a sound strategy for invalidating the content is crucial to maintaining high performance and having a high cache-hit ratio. If you maintain a high hit rate, then you’ll need fewer servers and will have happier users and probably less downtime. With this, you’re hopefully more comfortable using tools like these to get stale content out of your cache.

{{< signature "al, ml, il" >}}


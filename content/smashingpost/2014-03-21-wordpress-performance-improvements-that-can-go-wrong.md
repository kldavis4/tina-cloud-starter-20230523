---
title: WordPress Performance Improvements That Can Go Wrong
slug: wordpress-performance-improvements-that-can-go-wrong
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23da8f18-2329-4065-9de7-305431fd3f48/pagespeed-screenshot-opt.jpg
date: 2014-03-21T10:14:53.000Z
author: hristo-pandjarov
description: >-
  If you've searched recently for tips on optimizing WordPress’ performance,
  then you have definitely come across various techniques that people recommend.
categories:
  - WordPress
  - Plugins
  - Optimization
  - Maintenance
  - Techniques (WP)
  - Caching
---
If you've searched recently for tips on optimizing WordPress’ performance, then you have definitely come across various techniques that people recommend. These include all sorts of caching mechanisms, such as reverse proxies, object caching and cache plugins, CSS minification, using sprites for images, and so on. All of them are <strong>viable and effective ways to speed up a WordPress website’s performance</strong>. However, be careful when implementing any of these techniques, and always test their effect on your particular website.

In this article, we’ll cover some of the most common issues with various speed boosters that I have encountered and share solutions to help you fix those problems or find ways around them.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Speed Up Your WordPress Website](https://www.smashingmagazine.com/2014/06/how-to-speed-up-your-wordpress-website/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)
*   [Secrets Of High-Traffic WordPress Blogs](https://www.smashingmagazine.com/2012/09/secrets-high-traffic-wordpress-blogs/)
*   [Speeding Up Your Website’s Database](https://www.smashingmagazine.com/2011/03/speeding-up-your-websites-database/)
*   [<span class="headline">Do-It-Yourself Caching Methods With WordPress</span>](https://www.smashingmagazine.com/2012/06/diy-caching-methods-wordpress/)

## Possible Problems When Using Reverse Proxies Such As Varnish And Nginx

I will start with the reverse proxies because, when used correctly, they can give you the biggest speed boost and, when used improperly, can cause serious problems, such as making your website inaccessible or showing the wrong information to the wrong visitors.

{{% feature-panel %}}

### How Do Reverse Proxies Work?

Reverse proxies, like Varnish and Nginx, stand between your visitors and your Web server. When a request for one of your pages is made, your Web server usually has to execute the PHP service that makes calls to the database and then provides the page output and the static resources needed to visualize the page. With a reverse proxy enabled, this result is cached, and the next time someone requests that page, the ready output will be delivered by the reverse proxy, which is much faster and causes no load on your server.

This is great, but to operate correctly, the cache must be purged every time something on the page has changed. <strong>This is where things can go wrong</strong>, mostly because WordPress does not natively support reverse proxies and requires additional tweaks for the cache to be cleared correctly. Usually, such tweaks rely on WordPress’ default core hooks (think of them as events) to purge the cache when necessary — when a post is updated, when a comment is added, when a post is created, etc. However, if an important hook is missed in the implementation of the reverse proxy that you’re using, then you might have a problem. Additionally, numerous events — ones not a part of WordPress’ core hooks but rather performed through plugins — could change the content on your website.</p>

### Possible Problems During WordPress Updates

When updating, WordPress puts your website in maintenance mode, updates its files and then disables maintenance mode. The reverse proxy could possibly cache some of your pages while your website is in maintenance mode. This means that if the cache is not purged, then this maintenance page would continue being served to visitors, actively preventing them from reaching your website even when it is operational on the Web server.

<strong>When you update a plugin, WordPress disables it</strong>, deletes its entire folder and then adds the new files. During that time, the plugin does not actually work. If it’s a big plugin that adds a lot of functionality, such as a gallery or online store, then your reverse proxy could cache pages with errors on them, instead of the actual content.

When you update manually, the easy fix is either to disable the cache during the update or to purge the cache manually once you are ready with the update. However, when you use WordPress’ native automatic update, these solutions are not very practical. What a good reverse proxy should do instead is <strong>automatically purge the cache on each update event</strong>. Because both core and plugin updates have hooks in the core, this is easily achievable and should be done by you (if you are implementing the reverse proxy yourself) or by your hosting provider (if you rely on the host’s implementation).</p>

### Problems With Online Store Plugins for WordPress

No matter which WordPress plugin you use for your online store, you should be very, very careful when implementing reverse proxy caching.

For example, you could create a lovely mess with a shopping-cart widget that displays the products that a customer has selected to buy. If that content is cached by the reverse proxies, then all of your visitors would see the products that the first customer has selected for purchase. Things could get even worse if pages containing personal information, such as thank-you pages, are cached and displayed incorrectly to the wrong visitor. Needless to say, this should be avoided at all costs.

The safest way to avoid such problems is to <strong>exclude the entire e-commerce part of your website from the cache</strong>. Usually, reverse proxies implemented by hosting companies exclude the most common WordPress e-commerce plugins from the cache by default.

If excluding the whole e-commerce part of your website does not sound to you like an elegant solution — because you would obviously lose the speed benefits — then, theoretically, there is a more intricate way around: using Edge Side Includes (ESI) to specify that parts of your pages should not be cached. In theory, you would simply surround your HTML with ESI tags:

<pre><code class="language-markup">
&lt;esi:include&gt; Dynamic content &lt;esi:remove&gt;
</code></pre>

Then, the content between those tags would be dynamically retrieved every time this page is requested.

Unfortunately, implementing ESI with WordPress is not straightforward at all, due to WordPress’ lack of native support for reverse proxies. Thus, ESI is usually not a viable option with hosts that support reverse proxies. But it is worth considering if you have an online store built with WordPress and you are implementing the reverse proxy yourself.</p>

### Problems With Rating Plugins

When you use a rating plugin on a WordPress website that is cached by a reverse proxy, chances are that visitors will often see an incorrect cached rating, instead of the real up-to-date rating. The reason is that a visitor’s vote given through such a plugin is not part of WordPress’ default hooks and will not trigger a cache purge.

Similar to the e-commerce issues, you could either exclude pages that you collect rankings for from the cache or implement the ESI model for those pages, if feasible.</p>

## Issues With Full-Page Caching Plugins

In case your hosting provider doesn’t provide you with a reverse proxy caching service, you could rely on one of the so-called full-page caching plugins for WordPress. When a visitor requests a page, the plugin would save the actual HTML output in a physical file on your server. The next time someone requests that page, it would be served as a static HTML file, which is much slower than a reverse proxy but still faster than not caching at all.

Unfortunately, due to the caching technique being used, all of the possible problems I’ve explained for reverse proxies hold true for the full-page caching plugins, plus some new ones.

<strong>Be careful using such caching</strong> on a website with many posts or pages. When you create content on a WordPress website, more pages are automatically created than just the one you’re working on directly: category pages that list all posts in that category, tag pages, archives, author pages, pages for uploaded images, etc. All of these add up to a big number of URLs that your website serves. Now, imagine all of those URLs being turned into HTML files in some folder (usually the <code>uploads</code> folder) on your Web server. When thousands of files are in a single directory, even listing those files is difficult, and we’re talking about the Linux OS here. The result for a big website is usually a huge number of files, a heavy I/O load on the server and, eventually, a slower website and problems with the hosting provider.

There is no exact number of posts above which you should not incorporate this method, and it also depends on the particular way the plugin stores the cache — using multiple folders instead of one, for example, would be more efficient, but still might not be enough for a really large website. Just bear in mind that if you use such a caching technique and your website starts slowing down, then this might be the reason.</p>

## Object Caching (Memcached) And How To Break It

Object caching is great for a website that gets a lot of requests to its database, and it can really speed up some websites. Memcached stores the result of the most commonly executed queries to your database in the server’s RAM and serves the cached results instead of querying the MySQL server each time. Unfortunately, in some scenarios, you could actually decrease your website’s performance, and here is why.

Some WordPress plugins are coded (badly) to store a huge amount of data in the application database. The Memcached service has a limited amount of memory for caching. Imagine what happens when a plugin stores huge images in the database. Memcached will try to store the result of this query in its buffer but will run out of space. Then, it will start to delete previously cached content on a first-in, first-out basis. If the query’s results are big enough, then no actual content would be cached because it would be removed before being served a second time. <strong>In this case, your website would actually slow down</strong> because not only would you fail to spare this load on the MySQL service, but you would add another service in the process that requires its own computing time.

If you find your website is working more slowly after enabling Memcached, then unfortunately your only solution is either to disable all plugins that store a huge amount of data in the database or to disable the Memcached service itself.

## Sprites: Yes, You Can Go Wrong With Them, Too

I love sprites for the performance boost they give to a website when used correctly. This is why, when we redesigned <a href="https://www.siteground.com/">SiteGround</a> recently, we moved all navigation and UI elements and many other page elements to sprites. Our website became much faster, and we were quite happy with the result. Then, we continued adding elements to the sprite image, until at some point we noticed problems when some pages loaded on iOS devices.

This happened because we hit mobile Safari’s limit on the maximum number of decoded pixels that can be displayed. This limit is different for different devices. You could easily <strong>generate a sprite with a lot of pixels</strong>, and if it reaches the size limit, then the browser won’t load it, which will leave your website without all of the elements contained in that sprite. Of course, you don’t want this to happen.

A good man by the name of William Malone has crafted a <a href="https://www.williammalone.com/articles/html5-javascript-ios-maximum-sprite-frames/">nifty tool</a> to check whether a sprite image will display correctly on all iOS devices. Enter the dimensions of your sprite image in the calculator, and the answer will appear.

If your sprite is too big, a possible solution is to split it into two images. If you have to do this, my advice is to relegate only the newest elements to a new image; otherwise you would have to adjust all of the CSS code that uses the sprite, a task that you’d want to avoid if possible.</p>

## Risks With CSS And JavaScript Minification

CSS and JavaScript minification is another of the most common techniques for speeding up a website. Generally, minifying these files entails removing all unnecessary symbols (new lines, semicolons after the final CSS property, comments, etc.), thus reducing the size of the files. This technique applies not only to WordPress but to any page that uses CSS and JavaScript.

<strong>Many tools and plugins will automatically minify files.</strong> However, some minify more aggressively than simply removing empty symbols. Some tools will rearrange CSS selectors, for example, grouping them by property, etc. In some cases, this could break the entire logic of a CSS file and turn your website into something that merely resembles the original.

To avoid such problems, use basic non-aggressive minification tools that remove only unnecessary data from JavaScript and CSS files, without reordering properties. In addition, always keep a copy of your unminified files because, after minification, they will become practically unreadable, making any further changes much harder. I use either a plugin or the online <a href="https://www.freeformatter.com/">FreeFormatter</a>.</p>

## Gzip: Can’t Go Wrong Here, But We Can Do It Better

Enabling Gzip for WordPress will greatly improve loading speed. Gzip compresses a page’s output and transfers it to the visitor’s browser, like a regular ZIP file, whereupon the browser decompresses and renders it. It’s great because the time a browser takes to decompress archived content is many times less than the time needed to physically transfer the uncompressed content from the server to the browser.

<strong>Most WordPress users rely on plugins when they can</strong> — at least the ones who can’t or don’t want to code — including for Gzip. Unfortunately, Gzip plugins run through PHP, which, although fast, is not as fast as running directly from the Apache server. All you need to do is install mod_deflate (ask your hosting provider if it is available — it should be because it is pretty much an industry standard) and add a few lines to your <code>.htaccess</code> file:

<pre><code class="language-markup">
AddOutputFilterByType DEFLATE text/plain
AddOutputFilterByType DEFLATE text/html
AddOutputFilterByType DEFLATE text/xml
AddOutputFilterByType DEFLATE text/css
AddOutputFilterByType DEFLATE application/xml
AddOutputFilterByType DEFLATE application/xhtml+xml
AddOutputFilterByType DEFLATE application/rss+xml
AddOutputFilterByType DEFLATE application/javascript
AddOutputFilterByType DEFLATE application/x-javascript
</code></pre>

## Conclusion

Knowing all of the risks involved in optimizing the speed of your WordPress website should not stop you from experimenting. To achieve the best results, just follow few simple principles: don’t change too many things at once, benchmark your loading speeds, use staging copies when possible, and test the website’s functionality after applying each new technique. In doing so, you will speed up your website without breaking any functionality or causing problems for visitors.

{{< signature "dp, al, il" >}}


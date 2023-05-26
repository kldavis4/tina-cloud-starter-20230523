---
title: How To Speed Up WordPress
slug: how-to-speed-up-your-wordpress-website
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5605013-1b0d-4ca0-8310-cc3287e84ed7/wordpress-red-illu-icon.jpg
date: 2014-06-25T21:45:12.000Z
author: marcustaylor
description: >-
  A few months ago, I ran an experiment to see how much faster I could make one
  of my websites in less than two hours of work. After installing a handful of
  WordPress plugins and fixing a few simple errors, I had improved the website’s
  loading speed from 1.61 seconds to 583 milliseconds. That’s a 70.39%
  improvement, without having made any visual changes to the website.
categories:
  - WordPress
  - Tools
  - Techniques (WP)
---
A few months ago, I ran an experiment to see how much faster I could make one of my websites in less than two hours of work. After installing a handful of WordPress plugins and fixing a few simple errors, I had improved the website’s loading speed from 1.61 seconds to 583 milliseconds. That’s a 70.39% improvement, without having made any visual changes to the website. 
<strong></strong>

According to a <a href="https://www.akamai.com/us/en/about/news/press/2009-press/akamai-reveals-2-seconds-as-the-new-threshold-of-acceptability-for-ecommerce-web-page-response-times.jsp">2009 Akamai study</a>, 47% of visitors expect a page to load in under 2 seconds, and 57% of visitors will abandon a page that takes more than 3 seconds to load. Since this study, no shortage of case studies have confirmed that loading time affects sales.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [WordPress Performance Improvements That Can Go Wrong](https://www.smashingmagazine.com/2014/03/wordpress-performance-improvements-that-can-go-wrong/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)
*   [Secrets Of High-Traffic WordPress Blogs](https://www.smashingmagazine.com/2012/09/secrets-high-traffic-wordpress-blogs/)
*   [How We Increased Google Page Speed To 100](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)

In 2006, Amazon reported that a 100-millisecond increase in page speed translated to a 1% increase in its revenue. Just a few years later, Google <a href="https://googlewebmastercentral.blogspot.com.au/2010/04/using-site-speed-in-web-search-ranking.html">announced in a blog post</a> that its algorithm takes page speed into account when ranking websites.

{{% feature-panel %}}

<figure><img class="at alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5835251c-eb46-4c46-90b7-db52849fa425/speeding-up-wordpress-opt.jpg" alt="Speed Up WordPress" width="500" height="307" /><br>
<figcaption>So, how can you speed up your WordPress website?</figcaption></figure>

Below are twelve quick fixes that will dramatically improve your website’s loading time, including:

*   identifying which plugins are slowing down your website;
*   automatically compressing Web pages, images, JavaScript and CSS files;
*   keeping your website’s database clean;
*   setting up browser caching the right way.</p>

## Lay The Foundation

When your house is sinking into the ground, you don’t polish the windows — you fix the foundations. The same goes for your website. If it’s hosted on a sluggish server or has a bloated theme, quick fixes won’t help. You’ll need to fix the foundation.

So, let’s start with what makes for a good foundation and how to set ourselves up for a website that runs at lightening speed.</p>

### Choose A Good Host

Your Web hosting company and hosting package have a huge impact on the speed of your website, among many other important performance-related things. I used to be sucked in by the allure of free or cheap hosting, but with the wisdom of hindsight, I’ve learned that hosting isn’t an area to skimp on.

To put this into perspective, two of my clients have similar websites but very different hosting providers. One uses WPEngine (an excellent hosting company), and the other hosts their website on a cheap shared server.

The DNS response time (i.e. the time it takes for the browser to connect to the hosting server) of the client using WPEngine is 7 milliseconds. The client using the cheap shared hosting has a DNS response time of 250 milliseconds.

If you want your website to run quickly, <a href="https://www.smashingmagazine.com/2009/03/9-steps-to-a-happy-relationship-with-your-hosting-provider/">start with a good hosting company</a> and package.</p>

### Choose A Good Theme

Unfortunately, not all WordPress themes are created equal. While some are extremely fast and well coded, others are bloated with hundreds of bells and whistles under the pretence of being “versatile and customizable.”

A few years ago, Julian Fernandes of Synthesis ran an interesting case study in which he updated his theme from WordPress’ default to the Genesis framework, monitoring page speed. He noticed that just by changing the theme to Genesis, his loading time improved from 630 to 172 milliseconds.

When you choose a theme, check the page speed of the theme’s demo, using a tool such as Pingdom, to see how quickly it runs with nothing added to it. This should give you an idea of how well coded it is.

### Use A Content Delivery Network

I recently started using a content delivery network (CDN) for one of my websites and noticed a 55% reduction in bandwidth usage and a huge improvement in page-loading speed.

A CDN hosts your files across a huge network of servers around the world. If a user from Argentina visits your website, then they would download files from the server closest to them geographically. Because your bandwidth is spread across so many different servers, the load on any single server is reduced.

Setting up a CDN can take a few hours, but it’s usually one of the quickest ways to dramatically improve page-loading speed.</p>

## 12 Quick Fixes To Speed Up WordPress

Now that our foundation is solid, we can begin fine-tuning our website.

A good way to start speeding up a website is to look at what can be removed. More often than not, a website is slow not because of what it lacks but because of what it already has.</p>

### 1. Identify Plugins That Are Slowing You Down

<a href="https://wordpress.org/plugins/p3-profiler/">P3</a> is one of my favourite diagnostic plugins because it shows you the impact of your other plugins on page-loading time. This makes it easy to spot any plugins that are slowing down your website.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/658f4f93-d453-4cb1-8660-8ccb47005a7b/runtime-by-plugin-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95d1424b-a9a3-4c0f-8be1-aa1d62d7b712/runtime-by-plugin-preview-opt.jpg" alt="Runtime by plugin" width="500" height="297" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/658f4f93-d453-4cb1-8660-8ccb47005a7b/runtime-by-plugin-large-opt.jpg">Large preview</a>)</figcaption></figure>

A common culprit is social-sharing plugins, most of which bloat page-loading times and can easily be replaced by embedding social buttons into the theme’s source code.

Once you’re aware of which plugins are slowing down your website, you can make an informed decision about whether to keep them, replace them or remove them entirely.</p>

### 2. Compress Your Website

When you compress a file on your computer as a ZIP file, the total size of the file is reduced, making it both easier and faster to send to someone. Gzip works in exactly the same way but with your Web page files.

Once installed, Gzip automatically compresses your website’s files as ZIP files, saving bandwidth and speeding up page-loading times. When a user visits your website, their browser will automatically unzip the files and show their contents. This method of transmitting content from the server to the browser is far more efficient and saves a lot of time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/244f8d24-a775-45f5-aeda-9b6f425c1cf9/gzip-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec3bfbff-2374-4674-9403-6367c26588e1/gzip-preview-opt.jpg" alt="Gzip" width="500" height="297" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/244f8d24-a775-45f5-aeda-9b6f425c1cf9/gzip-large-opt.jpg">Large preview</a>)</figcaption></figure>

There is virtually no downside to installing Gzip, and the increase in speed can be quite dramatic. As we can see in the screenshot above, MusicLawContracts.com goes from 68 KB to only 13 KB with Gzip installed.

While some plugins will add Gzip to your website with the click of a button, installing it manually is actually very simple. Open your <code>.htaccess</code> file (found in the root directory on your server), and add the following code to it:

<pre><code class="language-php">
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

Once you’ve added this snippet of code to <code>.htaccess</code>, test whether Gzip is working on your website by running <a href="https://checkgzipcompression.com/">Check Gzip Compression</a>. If for whatever reason the code above doesn’t work, try one of the other methods that Patrick Sexton describes in his article “<a href="https://www.feedthebot.com/pagespeed/enable-compression.html">Enable Gzip</a>.”

### 3. Compress Images

Images take up the majority of bandwidth on most websites. <a href="https://wordpress.org/plugins/wp-smushit/">WP Smush.it</a> is another great plugin that automatically compresses images as you upload them to the media library. All compression is “lossless,” meaning that you won’t notice any difference in the quality of images.

One nice thing about WP Smush.it is that it works retroactively. If thousands of images are saved in your media library, you can run them all through the plugin, compressing them to a more manageable size.</p>

### 4. Leverage Browser Caching

Browser caching is a tricky issue. A handful of great caching plugins are available, but if set up incorrectly, they could cause <a href="https://www.smashingmagazine.com/2014/03/21/wordpress-performance-improvements-that-can-go-wrong/">more harm than good</a>.

Expires headers tell the browser whether to request a particular file from the server or from the browser’s cache. Of course, this only works if the user already has a version of your Web page stored in their cache; so, the technique will speed up the website only for those who have already visited your website.

Expires headers speed up a website in two ways. First, they reduce the need for returning visitors to download the same files from your server twice. Secondly, they reduce the number of HTTP requests made.

To do this with a plugin, I recommend using <a href="https://wordpress.org/plugins/wp-super-cache/">WP Super Cache</a>. However, following an <a href="https://www.wpbeginner.com/beginners-guide/how-to-install-and-setup-wp-super-cache-for-beginners/">installation guide</a> is strongly recommended to ensure that you set it up correctly. Alternatively, you could add expires headers by adding the following code to your <code>.htaccess</code> file.</p>

<pre><code class="language-php">#
# associate .js with “text/javascript” type (if not present in mime.conf)
#
AddType text/javascript .js

#
# configure mod_expires
#
# URL: https://httpd.apache.org/docs/2.2/mod/mod_expires.html
#

ExpiresActive On
ExpiresDefault “access plus 1 seconds”
ExpiresByType image/x-icon “access plus 2692000 seconds”
ExpiresByType image/jpeg “access plus 2692000 seconds”
ExpiresByType image/png “access plus 2692000 seconds”
ExpiresByType image/gif “access plus 2692000 seconds”
ExpiresByType application/x-shockwave-flash “access plus 2692000 seconds”
ExpiresByType text/css “access plus 2692000 seconds”
ExpiresByType text/javascript “access plus 2692000 seconds”
ExpiresByType application/x-javascript “access plus 2692000 seconds”
ExpiresByType text/html “access plus 600 seconds”
ExpiresByType application/xhtml+xml “access plus 600 seconds”

#
# configure mod_headers
#
# URL: https://httpd.apache.org/docs/2.2/mod/mod_headers.html
#

Header set Cache-Control “max-age=2692000, public”

Header set Cache-Control “max-age=600, private, must-revalidate”

Header unset ETag
Header unset Last-Modified
</code></pre>

### 5. Clean Up the Database

I’m a big fan of how often WordPress autosaves everything, but the disadvantage is that your database will get filled with thousands of post revisions, trackbacks, pingbacks, unapproved comments and trashed items pretty quickly.

The solution to this is a fantastic plugin called <a href="https://wordpress.org/plugins/wp-optimize/">WP-Optimize</a>, which routinely clears out your database’s trash, keeping the database efficient and filled only with what needs to be kept. Of course, when doing anything to your database, always back up first.</p>

### 6. Minify CSS and JavaScript Files

If you’ve installed more than a handful of plugins, chances are that your website links to 10 to 20 individual style sheets and JavaScript files on every page. This is not ideal. Putting all JavaScript into one JavaScript file and all CSS in one CSS file is considerably more efficient.

This is where minification comes in. Plugins such as <a href="https://wordpress.org/plugins/bwp-minify/">Better WordPress Minify</a> will combine all of your style sheets and JavaScript files into one, reducing the number of requests that the browser needs to make.

I prefer Better WordPress Minify because it’s less aggressive than some of the other plugins that do the same thing (some of which cause problems, as <a href="https://www.smashingmagazine.com/2014/03/21/wordpress-performance-improvements-that-can-go-wrong/">Hristo Pandjarov outlines</a>).</p>

### 7. Turn Off Pingbacks and Trackbacks

Pingbacks and trackbacks are methods used by WordPress to alert other blogs that your posts link to. While sometimes interesting, they can be a drain on page speed and are usually better turned off. You can turn them off under the “Discussion” tab in “Settings.”

### 8. Specify Image Dimensions and Character Sets

Before a visitor’s browser can display your Web page, it has to figure out how to lay out the content around the images. Without knowing the size of these images, the browser has to figure it out, causing it to work harder and take longer.

Specifying image dimensions saves the browser from having to go through this step, speeding things up.

For the same reason, specifying a character set in your HTTP response headers is useful, so that the browser doesn’t have to spend extra time working out which one you’re using. Simply add the character set to your website’s <code>head</code> section.</p>

### 9. Move CSS to the Top and JavaScript to the Bottom

Linking to your style sheets as close to the top of the page as possible is widely recommended because browsers won’t render a page before rendering the CSS file. JavaScript, on the other hand, should be as close to the bottom of the footer as possible because it prevents browsers from parsing anything after it until it has full loaded.

In the majority of cases, this simple fix will improve page-loading speed by forcing files to be downloaded in the optimal order. But it can cause issues on websites that rely heavily on JavaScript and that require JavaScript files to load before the user sees any of the page.</p>

### 10. Use CSS Sprites

A sprite is essentially one large image file that contains all of your individual images next to each other. Using CSS, you can hide everything in the image except for the section you need, by specifying a set of coordinates.

CSS sprites speed up a website because loading one big image is much faster than loading a lot of small images.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fedb5e3e-88f6-4353-acef-e17b473ab3ec/spriteme-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dea66b8-ef99-4c01-bb54-3f9aa9c3cf51/spriteme-preview-opt.jpg" alt="SpriteMe" width="500" height="297" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fedb5e3e-88f6-4353-acef-e17b473ab3ec/spriteme-large-opt.jpg">Large preview</a>)</figcaption></figure>

The easiest solution is <a href="https://spriteme.org/">SpriteMe</a>, a tool that turns all of your images into a CSS sprite.

Remember that Safari does not load large sprites, so use <a href="https://www.williammalone.com/articles/html5-javascript-ios-maximum-sprite-frames/">William Malone’s calculator</a> to identify whether your sprite is too large.</p>

### 11\. Enable Keep Alive

HTTP Keep Alive refers to the message that is sent between the client’s machine and the Web server asking for permission to download a file. Enabling Keep Alive allows the client’s machine to download multiple files without having to repeatedly ask for permission, thus saving bandwidth.

To enable Keep Alive, simply copy and paste the code below into your <code>.htaccess</code> file.</p>

<pre><code class="language-php">
Header set Connection keep-alive
</code></pre>

### 12\. Replace PHP With Static HTML Where Appropriate

PHP is great for making a website efficient and reducing the need to enter the same information multiple times. However, calling information through PHP uses up server resources and should be replaced with static HTML where it doesn’t save any time.</p>

## Conclusion - Speed Up WordPress

In the next 12 months, mobile Internet usage is expected to overtake desktop usage. This shift towards Internet-enabled mobile devices means that <strong>having a fast website has never been as important as it is today</strong>. Users now expect websites to be lightening fast, and developers who don’t comply will ultimately lose out to developers who invest in delivering a great experience.

{{< signature "al, il" >}}


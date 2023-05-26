---
title: 'Creating Better, Faster And More Optimized WordPress Websites'
slug: better-faster-optimized-wordpress-websites
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3513654-1ba9-4d90-8e8b-fd43d62f5226/wordpress-host-preview-opt.png
date: 2017-06-07T17:13:42.000Z
author: brianjackson
description: >-
  Consumers typically have their own experiences when it comes to web hosting
  and their own opinions. If you search Google for reviews for any web hosting
  provider you'll find dozens of results.

  Usually, there are a lot more negative reviews than there are positive ones. I
  thought I would flip that around and share some WordPress hosting challenges
  **from the perspective of the WordPress host** and how I frequently solve
  them.
categories:
  - WordPress
  - Performance
---
Consumers typically have their own experiences when it comes to web hosting and their own opinions. If you search Google for reviews for any web hosting provider you'll find dozens of results. Usually, there are a lot more negative reviews than there are positive ones. I thought I would flip that around and share some WordPress hosting challenges <strong>from the perspective of the WordPress host</strong> and how I frequently solve them.

I have compiled a list of bad web practices and recommendations on what not to do on your site, based on thousands of hours of customer interactions, support tickets, and troubleshooting I experience on a daily basis. Some of these range from beginner mistakes to more complex issues. A lot of these can be the difference between having a successful WordPress site and a failure. Picking the right web host is very important. But your decision also goes hand-in-hand with educating yourself on how to best optimize your WordPress site.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7df056e3-e07c-4af9-968b-afd33a203caa/wordpress-host-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca692992-145c-4acb-b049-f715e31d0345/wordpress-host-800w-opt.png" alt="Optimizing WordPress sites." width="800" height="497" /></a><figcaption>Optimizing WordPress sites. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7df056e3-e07c-4af9-968b-afd33a203caa/wordpress-host-large-opt.png">Large preview</a>)</figcaption></figure>

I often observe that even seasoned developers focus on what they are good at, which is building solutions and sometimes neglect or don't have time to learn the latest optimization practices. Whether you are a WordPress user just getting started or an experienced developer, the following tips will help you create better, faster and more optimized WordPress sites.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Free SSL For Any WordPress Website](https://www.smashingmagazine.com/2016/06/free-ssl-for-any-wordpress-website/)
*   [WordPress Responsive Images With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)
*   [Lessons Learned From WordPress Plugin Support](https://www.smashingmagazine.com/2016/06/lessons-learned-from-plugin-support/)
*   [How To Make WordPress Hard For Clients To Mess Up](https://www.smashingmagazine.com/2016/07/how-to-make-wordpress-hard-for-clients-to-mess-up/)

{{% feature-panel %}}

## 1\. Switching Hosts Isn't Always a Quick Fix

One of the most important things people need to realize is that switching hosts doesn't automatically fix certain problems. If your WordPress site is having code issues or compatibility problems with specific plugins, this is still going to occur no matter where you host your site.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f943ec1-3c61-4e96-b7d9-5084f1c9382a/code-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/692c0ed1-8f32-407b-9659-cdde234aec0a/code-800w-opt.png" alt="Code Issues." width="800" height="601" /></a><figcaption>Coding issues aren't magically fixed. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f943ec1-3c61-4e96-b7d9-5084f1c9382a/code-large-opt.png">Large preview</a>)</figcaption></figure>

A managed host will provide as much assistance as they can, but won't debug an issue with a bad plugin or code for you. It is not the WordPress host's responsibility to write PHP code, create or edit custom functions for plugins or themes, integrate or fix external services or performing website content updates. This is where you would <strong>need the assistance of a seasoned WordPress developer</strong> to dig into it and make a determination as to what the issue is. There are many places to find WordPress specific developers, such as <a href="https://codeable.io/">Codeable</a> or <a href="https://www.toptal.com/wordpress">toptal</a>.

Many hosts also have third-party agency partners and developers they can refer you to for solving these problems. If there is an issue with a specific plugin, you should also reach out to the developer yourself.</p>

## 2\. Live Sites are Not For Development Work

I could say this a thousand times. <strong>Never use production (live) sites for development work!</strong> Nearly all of the major managed WordPress hosts now have staging/development environments and this is certainly for good reason. It prevents critical downtime caused by users breaking things while testing on their live site. This is typically the scenario that causes what some call the <a href="https://codex.wordpress.org/Common_WordPress_Errors#The_White_Screen_of_Death">white screen of death</a>.

If you don't want to use a staging environment you can always test and <a href="https://developer.wordpress.org/themes/getting-started/setting-up-a-development-environment/">develop locally</a> using what some call a LAMP or LEMP stack. These stand for Linux, Apache/Nginx (sounds like Engine-X), MySQL, and PHP. Tools like WAMP and <a href="https://www.smashingmagazine.com/2011/09/28/developing-wordpress-locally-with-mamp/">MAMP</a> all make configurations for local development quite easy.

These tools have all improved and evolved over time, but there are also other challenges and problems that arise with local development, such as the environment not exactly mimicking your live site. First of all, you have to figure out how to push your changes from local back to production without overwriting existing data or breaking your site. Depending on your setup this process might even add another layer of complexity. Other complications could also include having to mess with conflicting ports or errors from a different version of MySQL are all things that could pop up.

To avoid some of these complications, I recommend using tools like <a href="https://serverpress.com/">DesktopServer</a> and <a href="https://local.getflywheel.com/">Local</a>, which are both built solely for the purpose of speeding up your workflow when working locally with WordPress. These include streamlined ways to push things back to production and even have additional tools and features such as WP-CLI and multisite support built right in. Having multisite support alone can be priceless as working with large local installations can sometimes be downright tricky.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90e67f90-bc54-458a-9058-8ad16eac4050/lemp-stack-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72833848-1ccd-4fbe-898b-940526f99edf/lemp-stack-800w-opt.png" alt="LEMP Stack" width="800" height="671" /></a><figcaption>LEMP stack. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90e67f90-bc54-458a-9058-8ad16eac4050/lemp-stack-large-opt.png">View large version</a>)</figcaption></figure>

Staging and local testing environments can help you find problems before they break your site.</p>

## 3\. Not A Developer? Don't Edit Your Code

People that are either unfamiliar with WordPress or don't know the basics of how code works should not be editing files. One of the most common reasons that WordPress sites go down (or see that "white screen of death") is someone editing a PHP file directly from the appearance editor in the dashboard. Also, you shouldn't be editing your live site to begin with as we mentioned earlier.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a51c9a9-1c11-49a0-be49-27738642436b/wordpress-appearance-editor-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efacd262-eb87-4756-b9a4-8ff6ac3d4e22/wordpress-appearance-editor-800w-opt.png" alt="WordPress appearance editor." width="800" height="546" /></a><figcaption>Editing code in the WordPress Appearance editor. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a51c9a9-1c11-49a0-be49-27738642436b/wordpress-appearance-editor-large-opt.png">View large version</a>)</figcaption></figure>

A good administrative recommendation is to place the following code in your wp-config.php file, removing the <code>edit_themes</code>, <code>edit_plugins</code>, and <code>edit_files</code> capabilities for all users. This can help prevent users from breaking the site by hacking away at the code.</p>

<pre><code class="language-php">define('DISALLOW_FILE_EDIT', true);</code></pre>

Taking this process one step further, remove the functionality for clients to update themes or install plugins. Place the following code in your wp-config.php file to restrict these capabilities.</p>

<pre><code class="language-php">define('DISALLOW_FILE_MODS', true);</code></pre>

**Note**: _The above code will also disable the plugin and theme file editor, so you don't need both if you want to disable everything mentioned above. See [WordPress Codex](https://codex.wordpress.org/Editing_wp-config.php#Disable_Plugin_and_Theme_Update_and_Installation) for more information._

## 4\. Don't Cut Corners on Your Themes and Plugins

It's understandable that you are trying to save a few bucks or cut corners, but don't do it with your themes and plugins. WordPress might be the foundation of your site, but the themes and plugins are the glue that holds it all together. Try to <strong>stick with reputable developers</strong> when choosing plugins and look through the ratings and reviews beforehand. Look for a history of the developer providing good product support. With over 50,000 plugins in the <a href="https://wordpress.org/plugins/">repository</a>, this can sometimes be an overwhelming task, so do your research beforehand.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d53e200-5de4-4ba1-81b0-389d6bed3e6a/wordpress-plugin-repository-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6769913c-4a91-44c8-bebe-33b506dcff5c/wordpress-plugin-repository-800w-opt.jpg" alt="WordPress plugin repository." width="800" height="652" /></a><figcaption>Finding a plugin in the WordPress repository. (Image credit: <a href="https://wordpress.org/plugins/">WordPress.org</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d53e200-5de4-4ba1-81b0-389d6bed3e6a/wordpress-plugin-repository-large-opt.jpg">View large version</a>)</figcaption></figure>

It is very common for outdated and bad themes/plugins to more easily get infected with malware, inject bad links on your site, pharma, etc. According to recently published <a href="https://wploop.com/old-outdated-wordpress-plugins/">research by WP Loop</a>, nearly 50% of the plugins in the repository haven't been updated in over 2 years. That is both shocking and frightening!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c194956d-5a4b-4d28-933a-d2ea048ce4ac/wordpress-plugins-not-updated-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e7c13f-d4f3-4e77-b526-1da89708760e/wordpress-plugins-not-updated-800w-opt.png" alt="Out of date plugins." width="800" height="384" /></a><figcaption>Statistics on plugins that haven't been updated. (Image credit: <a href="https://wordpress.org/plugins/">WP Loop</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c194956d-5a4b-4d28-933a-d2ea048ce4ac/wordpress-plugins-not-updated-large-opt.png">View large version</a>)</figcaption></figure>

Another thing to be on the lookout for is a third-party source that is bundling up premium plugins into one low bundled price. If you purchase these, first off, you aren't supporting the developer, so shame on you. Second, you are relying on the 3rd party to grab the latest updates for you which is not good.

Relying on updates for a bundled plugin is actually a huge problem for WordPress users who purchase things via online marketplaces such as ThemeForest. Many theme developers bundle additional plugins like Revolution Slider or Visual Composer. The problem is that when <a href="https://www.themepunch.com/products/old-revolution-slider-pre-4-2-vulnerabilty-explained/">vulnerabilities are discovered</a>, the consumer is left waiting for an update from the theme developer, even though the plugin might have been patched the next day. This leaves a lot of sites wide open for hackers and site owners extremely vulnerable.

## 5\. Watch Your Admin AJAX Calls

Watch out for multiple <a href="https://kinsta.com/blog/admin-ajax/">Admin AJAX</a> calls from your WordPress site and plugins that may utilize AJAX. For example, the WordPress Heartbeat API uses <code>/wp-admin/admin-ajax.php</code> to run AJAX calls from the web-browser. A lot of times these are un-cachable requests. High usage of this file sometimes occurs during traffic spikes, CPU load, and can bring your site to a crawl. It is almost like you are launching a distributed denial-of-service (DDoS) attack against yourself!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df0e5abc-88fc-4717-8b37-75752736cd03/high-admin-ajax-usage-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fe823f6-0983-4c75-ad84-ae7ed824e50d/high-admin-ajax-usage-800w-opt.png" alt="Admin AJAX calls" width="800" height="256" /></a><figcaption>High admin-ajax.php usage. (Image credit: <a href="https://tools.pingdom.com/">Pingdom</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df0e5abc-88fc-4717-8b37-75752736cd03/high-admin-ajax-usage-large-opt.png">View large version</a>)</figcaption></figure>

If there are 3rd party plugins that utilize admin-ajax.php, make certain they are doing it in the correct way. You can usually <strong>look at the HTTP POST request action</strong> and quickly determine, based on the name, what plugin might be causing it. For example, one I have seen is, <code>get_shares_count</code>. Which turned out to be a popular social media sharing plugin which was hammering admin-ajax.php. These simply multiply on high-traffic sites.

However, AJAX does load after the page loads. So just because you see this in a speed test, doesn't necessarily always mean it is a bad thing. It is also an interesting comparison to note the <a href="https://deliciousbrains.com/comparing-wordpress-rest-api-performance-admin-ajax-php/">performance differences</a> between admin-ajax.php and the WordPress REST API.</p>

## 6\. Be Smart With Ad Networks and Limit External Services

Most high-traffic websites rely on advertising for their income. Removing 3rd party advertisements altogether is not an option. However, it is important to keep the number of 3rd party networks to a minimum and realize just how much load some of these tack onto your website.

Here's a quick comparison of how ad networks can affect your WordPress site.

Test Parameters: I added three 300x250 Google Adsense ads on a development/staging site running the default twenty sixteen theme and tested the speed before and after.</p>

### Before AdSense ([test results](https://www.webpagetest.org/result/161207_A5_98FR/))

*   First view: 1.372s load time
*   Repeat view: 1.013s load time

Here is the content breakdown by connections:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7ec41d6-7e06-40c0-8159-49655b90ea3d/content-breakdown-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ac7f344-304c-44a3-a195-d198aa4287e4/content-breakdown-800w-opt.jpg" alt="Before AdSense." width="800" height="217" /></a><figcaption>Content breakdown before running Google AdSense. (Image credit: <a href="https://www.webpagetest.org/result/161207_A5_98FR/">WebPageTest</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7ec41d6-7e06-40c0-8159-49655b90ea3d/content-breakdown-large-opt.jpg">View large version</a>)</figcaption></figure>

### After AdSense ([test results](https://www.webpagetest.org/result/161207_VG_9B59/))

*   First view: 4.103s load time
*   Repeat view: 3.712s load time

Here is the content breakdown by connections:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40f3e920-b2e6-491a-b69c-a82d64ef690b/ad-network-content-breakdown-2-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/264a348b-2848-4b79-a498-6b5488eafd05/ad-network-content-breakdown-2-800w-opt.jpg" alt="After AdSense." width="800" height="305" /></a><figcaption>Content breakdown after adding Google AdSense. (Image credit: <a href="https://www.webpagetest.org/result/161207_VG_9B59/">WebPageTest</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40f3e920-b2e6-491a-b69c-a82d64ef690b/ad-network-content-breakdown-2-large-opt.jpg">View large version</a>)</figcaption></figure>

By simply adding 3 Google AdSense ads, 6 additional connections were instantly added. <strong>The WordPress site with ads is 2.7x slower than the one without.</strong> This is mainly due to extra DNS lookup times and much heavier use of JavaScript on the page. This gives you a small picture of what can happen when large-scale sites simply embeds 10 ads on a single page. No matter how fast your WordPress host is, it won't fix delays from 3rd party ad network connections.

Here is another example below taken from New Relic monitoring on a site with a massive amount of HTTP requests to external ad networks, causing a heavy load on the WordPress site.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d657b81f-2fad-4a7c-9401-140f27f24220/external-ad-network-1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b724923f-9ccf-4dae-a618-6974b52503c2/external-ad-network-1-800w-opt.png" alt="Ad Heavy." width="800" height="170" /></a><figcaption>Heavy load due to advertising network. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d657b81f-2fad-4a7c-9401-140f27f24220/external-ad-network-1-large-opt.png">View large version</a>)</figcaption></figure>

There were so many requests that the app server failed to load at all. The site was simply unavailable trying to load all the external requests.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffb1030d-d22a-46a3-82d8-3fb72fff993c/external-ad-network-2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaf9347e-e5a0-4458-917a-f80b62209f77/external-ad-network-2-800w-opt.png" alt="App Server." width="800" height="411" /></a><figcaption>Web transactions time on app server. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffb1030d-d22a-46a3-82d8-3fb72fff993c/external-ad-network-2-large-opt.png">View large version</a>)</figcaption></figure>

Another good example of this is with <a href="https://www.huffingtonpost.com/">Huffington Post's</a> website. If you run a speed test on their website you will see massive amounts of HTTP requests to ad networks. This graph shows what I saw in a quick test. (<a href="https://www.webpagetest.org/result/161208_H7_61C7/">speed test</a>). They had a load time of over 13 seconds!

*   First view: 15.908s load time / Total HTTP requests: 221
*   Repeat view: 13.957s load time / Total HTTP requests: 66

However, simply removing advertisements might not be a realistic solution. Many sites rely on them for their income and livelihood. In this case, it's important to dive deeper into your scripts and ensure they are loading in the most optimal way. You can use <a href="https://www.keycdn.com/support/prefer-async-resources/">async</a> or defer on your scripts to help prevent them from interrupting the rendering of your page loads. When it comes to performance there is always a balancing act of <a href="https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/">perceived performance</a> vs. that of actual performance.</p>

### Async JavaScript example:

<pre><code class="language-javascript">src="example.js" async</code></pre>

### Defer JavaScript example:

<pre><code class="language-javascript">src="example.js" defer</code></pre>

Patrick Sexton also has another popular method for <a href="https://varvy.com/pagespeed/defer-loading-javascript.html">deferring JavaScript</a>. WordPress version 4.1 and higher has a <a href="https://matthewhorne.me/defer-async-wordpress-scripts/">filter</a> in which you can more easily add async and defer attributes to your scripts.

As a general rule, if you are relying on external services you will also want to cache the responses. Why? Because issues like the white screen of death can occur if you don't. Every external service you add to your WordPress site should be from a trusted and reliable source. After all, if they go down, it is then affecting your entire site or business operations. If you use vanity URLs generated from your WordPress site and use them in social networks, those will cease to function as well.</p>

## 7\. Over Optimizing Can Hurt Your Performance

There are thousands of articles around the web that give "tips" on how to speed up and optimize your WordPress site. But an even <strong>worse scenario is when users over optimize their websites.</strong> Yes, this happens a lot more frequently than you might think. It is common for WordPress site owners to think that by adding more of something it will double their speed.

Below I've listed a few problem scenarios that I see on a regular basis:

### Trying to Cache the Cache

Unlike typical VPS or standalone servers, a lot of managed WordPress host providers have their own caching, which is done at a server-level (like Redis or Memcache). Most providers do not allow caching plugins because this can cause all types of issues, most commonly 502 gateway errors. Trying to "cache the cache" as I call it is never a good idea.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abedf756-8fb0-481c-bd46-07664052ac85/facepalm-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b178e262-8553-4f4f-9dfe-2e0ed99299ed/facepalm-800w-opt.png" alt="Bad optimizations." width="800" height="800" /></a><figcaption>Bad optimizations which makes things worse. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abedf756-8fb0-481c-bd46-07664052ac85/facepalm-large-opt.png">View large version</a>)</figcaption></figure>

Plugins like WP Rocket and Cache Enabler are great, but they are designed for servers which need additional assistance speeding up your site. Read more about <a href="https://www.scalewp.io/object-caching/">object caching</a>, which is a popular form of server-level caching used by many today.</p>

### Adding 2 CDNs = is 2x the Speed, Right?

<a href="https://www.incapsula.com/cdn-guide/what-is-cdn-how-it-works.html">Content Delivery Networks</a> (CDN) have been shown to greatly decrease load times and latency when serving up content across different geographical regions, but only when setup correctly. One of the most popular providers is Cloudflare. Cloudflare is technically a fully proxy service and is slightly different than a normal CDN provider as you are pointing your entire DNS over to them, not just your assets.

Typically I see users add CloudFlare, and then they go add KeyCDN or MaxCDN along with it. This is usually because they read blog posts from someone recommending that they should go install this new service right away, and they simply go do it. They don't think about their existing setup. While this combination can work in certain scenarios, typically this ends up in a giant mess. In most cases it is better to either use CloudFlare or use a 3rd party CDN provider, each of which have their own advantages and disadvantages.</p>

### More SEO Plugins Doesn't Mean You Will Dominate SERPs

You want to dominate search engine ranking positions (SERPs) right? Well, adding 3 SEO plugins won't help you accomplish that goal. In fact, there are a lot of compatibility issues that popup when trying to run All In One SEO, Yoast, and other SEO plugins together. Such as outputting <a href="https://wordpress.org/support/topic/can-one-use-both-all-in-one-seo-and-yoast-plugin-at-the-same-time/">duplicate meta tags</a>. Adding more plugins doesn't mean it will improve your current SEO situation.</p>

## 8\. Common Performance Issues are Easy to Diagnose

Even if you aren't an advanced WordPress expert, common performance issues are fairly easy to diagnose. I recommend using <a href="https://www.webpagetest.org/">WebPageTest</a> for seasoned WordPress users as it supports the latest protocols such as HTTP/2. However, for those that aren't as webperf savvy, then <a href="https://tools.pingdom.com/">Pingdom</a> does a good job. A simple <a href="https://kinsta.com/blog/pingdom-speed-test/">waterfall analysis</a> can tell you quite a bit, such as learning if you have unnecessary redirects, missing files, too many DNS lookups or if a certain script or 3rd party ad network is bogging your site down.

Take a quick glance at the performance insights and response codes and you can see where to start addressing these performance issues on your WordPress site.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2643fb64-c857-4fc3-8755-c01c4dfcaaa1/pingdom-insights-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1388a70b-fc07-4b2e-8893-e8a22f308248/pingdom-insights-800w-opt.jpg" alt="Pingdom Insights." width="800" height="694" /></a><figcaption>Pingdom performance insights. (Image credit: <a href="https://tools.pingdom.com/">Pingdom</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2643fb64-c857-4fc3-8755-c01c4dfcaaa1/pingdom-insights-large-opt.jpg">View large version</a>)</figcaption></figure>

## 9\. Modifying WordPress Core is Bad

Plain and simple, modifying WordPress core files to make some of your code work is <a href="https://websynthesis.com/dont-hack-wordpress-core/">simply a bad idea</a>, especially on a live production site. Doing this can open up your WordPress site to security vulnerabilities. Unless you have an active update procedure in place (which many don't) you will lose your modifications with each new version of WordPress that is released. Instead, you should take advantage of WordPress tools and features such as well-developed 3rd party plugins, child themes, custom post types and hooks.</p>

## 10\. Ensure PHP 7/HHVM Compatibility Before Jumping on Board

PHP 7 and HHVM have been shown to be incredibly fast when it comes to <a href="https://make.wordpress.org/core/2015/09/10/wordpress-and-php7/">boosting WordPress performance</a>. And of course it's always satisfying to be using the latest and greatest, but first you need to make sure your site is compatible before simply hopping on the bandwagon. For example, If you are upgrading from PHP 5.6 to 7, you should test all functionalities of your WordPress site in a staging environment or locally to ensure there aren't any compatibility issues. One out of date plugin you rely on that doesn't work with PHP 7 could mean that you should wait before moving.</p>

## 11\. Large Sites Should Optimize Their Database

One of the easiest ways for a large WordPress site to slow down is when the database hasn't been optimized. Simple tasks like cleaning up old WordPress revisions or cleaning up unused tables, can help prevent some of this slowdown. However, I've found that a lot of older sites are still using the MyISAM storage engine in their database. Recently InnoDB has shown to <a href="https://dimitrik.free.fr/blog/archives/2015/12/mysql-performance-revisiting-innodb-vs-myisam-with-mysql-57.html">perform better</a> and be more reliable. A big reason is to use InnoDB over MyISAM is the lack of table locking. This allows your queries to process faster.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/956f99a7-fa58-4681-8cb1-eaf484a0cb05/database-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d08c102-2a4d-402d-8eab-9036528be550/database-800w-opt.png" alt="Database performance." width="800" height="883" /></a><figcaption>Database performance. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/956f99a7-fa58-4681-8cb1-eaf484a0cb05/database-large-opt.png">View large version</a>)</figcaption></figure>

You can convert your tables with just a few simple steps. Ensure you are running MySQL 5.6.4 or higher and that you always take a backup as a precautionary measure before making changes to your database. This example is using the <code>wp_comments</code> table. Simply run the ALTER command to convert it to InnoDB storage engine.</p>

<pre><code class="language-php">ALTER TABLE wp_comments ENGINE=InnoDB;</code></pre>

If you are running on a newer version of phpMyAdmin you can also click on a table, click into the "Operations" tab and change the storage engine manually.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d201985-c545-470c-a2b2-a9a976d9e9b4/innodb-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad2c110-127b-4f88-a5d8-369b802870f5/innodb-800w-opt.png" alt="InnoDB." width="800" height="628" /></a><figcaption>Changing from MyISAM to InnoDB. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d201985-c545-470c-a2b2-a9a976d9e9b4/innodb-large-opt.png">View large version</a>)</figcaption></figure>

Another easy optimization technique is to <strong>disable or modify the number of revisions</strong> you keep in your database. You can add the following to your wp-config.php to disable them completely.</p>

<pre><code class="language-php">define('WP_POST_REVISIONS', false );</code></pre>

Or simply modify the number of revisions that are kept per post/page:

<pre><code class="language-php">define('WP_POST_REVISIONS', 3);</code></pre>

I've seen many sites with over 200 revisions per post, which adds up very fast across large sites. Unless your host has an internal optimization in place, the default in WordPress is to store unlimited revisions. This is why it's so important to check and verify the settings with your own eyes.

If your current site has a lot of revisions already, you can run the following query in phpMyAdmin to clean them up:

<pre><code class="language-php">DELETE FROM wp_posts WHERE post_type = "revision";</code></pre>

If you aren't comfortable running a query, use plugins such as WP-Optimize to help you cleanup the revisions.</p>

## 12\. Do You Really Need a Multipurpose Theme?

There is a huge problem I see within the WordPress community. People go out and buy a multipurpose theme and then only utilize 1% of the theme's features or none at all. Many see fancy sliders and attractive portfolio pages on the demos that entices them to make the purchase. But in reality, these might be things they never actually use. They could have purchased a more minimal theme and saved a ton of time on digging through confusing options and their site would be a lot faster from the onset. Many of these additional features add load time.

I'm not saying all multipurpose themes are bad, in fact with a lot of customization they can sometimes run fast. Here is an example of an Avada theme that clocks in under 700ms. (<a href="https://tools.pingdom.com/#!/eaL5Ny/https://arizonamri.com">speed test</a>)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecc89517-5c6d-4410-b31c-edaaa9b462c3/avada-theme-fast-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/075e64c5-1467-4e5e-8d41-dd43562ce2c1/avada-theme-fast-800w-opt.jpg" alt="Fast WordPress theme after optimization." width="800" height="202" /></a><figcaption>Optimized multipurpose WordPress theme. (Image credit: <a href="https://tools.pingdom.com/#!/eaL5Ny/https://arizonamri.com">Pingdom</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ecc89517-5c6d-4410-b31c-edaaa9b462c3/avada-theme-fast-large-opt.jpg">View large version</a>)</figcaption></figure>

However, that requires a lot of knowledge and time to optimize the existing theme. For basic WordPress users, if they aren't utilizing a lot of features a more minimal theme is the way to go. Don't let all the shiny bells and whistles fool you. In most scenarios, fancy sliders and visual editors just slow your site down.</p>

## 13\. Error Log Is Your Friend

If you know your way around your WordPress files and the wp-config.php file, then the error log is your friend. By checking it on a regular basis you can save yourself a lot of headaches and probably learn a thing too. Not many users even bother checking this before reaching out to their host for help. With a few simple tweaks in your wp-config.php file you can enable logging, which by default is saved to /wp-content/debug.log.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88b70fc7-c23d-4b33-a7c2-152f49e8e743/log-file-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c543631-7943-4dcb-975e-a4bb050c5590/log-file-800w-opt.png" alt="Log file." width="800" height="801" /></a><figcaption>Error log is your friend. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88b70fc7-c23d-4b33-a7c2-152f49e8e743/log-file-large-opt.png">View large version</a>)</figcaption></figure>

### Enable Logging

<pre><code class="language-php">define( 'WP_DEBUG_LOG', true );</code></pre>

### Output Logging on Page

<pre><code class="language-php">define( 'WP_DEBUG_DISPLAY', true );</code></pre>

See more information in the <a href="https://codex.wordpress.org/Debugging_in_WordPress">WP_DEBUG codex.</a>

## 14\. Google is Here for a Reason

You would think this is common sense by now, but Google is here for a reason folks. Don't be afraid to Google your answer. The internet is full of solutions and tips. Within a few minutes of searching you can easily solve a majority of your issues. Typically questions like "how to change your GoDaddy DNS" or "how to use SFTP" are things that can be easily found on Google.

There are great resources available online such as <a href="https://wordpress.stackexchange.com/">https://wordpress.stackexchange.com/</a> and the <a href="https://codex.wordpress.org/">WordPress Codex</a>. Not to mention the hundreds of blogs with tutorials on just about any WordPress scenario that exists.

But not all of this is squarely on the shoulders of the user either. A responsible WordPress host should have an in-depth knowledge base with a good UI. Not only to cut down on their own support tickets but to help the user as well.</p>

## 15\. 123456 Is No Longer Acceptable

SpashData compiles a list of the most widely used leaked passwords (over 2 million) every year. Not surprisingly, in 2015 the <a href="https://www.teamsid.com/worst-passwords-2015/">most popular password</a> still being used was "123456 (the same as 2014)." This can be very frustrating for web hosting providers, as the bad practice of using easy to guess passwords puts the client's WordPress site in a state of "always one step away from being hacked." While storing passwords locally in a tool like KeePass is probably one of the safest routes, encouraging users to use services like LastPass or Passpack will at least help harden their passwords, even if they are stored in the cloud. A hashed and secured password in the cloud is always much more secure than using "123456."

## 16\. Scripts Don't Always Need to Load Sitewide

Unfortunately, unlike a static website which you have more control over, when it comes to WordPress many are at the mercy of the plugin and theme developers. Let's be honest, not all developers care about performance. There are a lot of plugins that simply load their scripts on all pages even though it might only be used on one. If you multiply this by 35+ plugins you can end up with a lot of unnecessary bloat that slows down your site.

One example of this can be seen with the popular Contact Form 7 WordPress plugin. As shown below, it is loading it's CSS file on the homepage of our dev site, as well as it's JavaScript file. Even though I'm not utilizing any contact form.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d79b6569-a208-4ef5-95b5-3b7acf3ceeb5/contact-form-7-loading-sitewide-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a912420f-f318-4610-8c4f-be600803e452/contact-form-7-loading-sitewide-800w-opt.png" alt="Script loading sitewide." width="800" height="626" /></a><figcaption>Script loading sitewide. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d79b6569-a208-4ef5-95b5-3b7acf3ceeb5/contact-form-7-loading-sitewide-large-opt.png">View large version</a>)</figcaption></figure>

There are a few easy ways to get around this. The first is to utilize a function which was introduced in WordPress 3.1 called <a href="https://codex.wordpress.org/Function_Reference/wp_dequeue_script">wp_dequeue_script()</a>. This allows you to remove an enqueued script from your site. Here is an example of <a href="https://orbitingweb.com/blog/prevent-cf7-from-loading-css-js/">how to utilize the function</a> with Contact Form 7. The Contact Form 7 developer also has some documentation on how to <a href="https://contactform7.com/loading-javascript-and-stylesheet-only-when-it-is-necessary/">load the JavaScript and CSS only when necessary</a>.

Another easy way to prevent certain scripts from loading on specific pages and posts is to utilize a WordPress plugin like <a href="https://tomasz-dobrzynski.com/wordpress-gonzales">Gonzalez</a> or <a href="https://wordpress.org/plugins/plugin-organizer/">Plugin Organizer</a>. Here is an example below on our dev site with the Gonzalez plugin. There are easy one-click options to disable the Contact Form 7 CSS and JavaScript files sitewide, per page/post, or only enable in a specific place. Generally, only loading Contact Form 7 on your "Contact Us" page would be the best for performance.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35dc67ce-bee6-4bb9-ad7d-c4e9243de319/disable-scripts-per-page-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0df80bd-eda6-478f-8693-a5e33ba9d4db/disable-scripts-per-page-800w-opt.png" alt="Disable scripts per page." width="800" height="310" /></a><figcaption>Disable scripts per page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35dc67ce-bee6-4bb9-ad7d-c4e9243de319/disable-scripts-per-page-large-opt.png">View large version</a>)</figcaption></figure>

## Conclusion

There is a reason why WordPress is used by over <a href="https://w3techs.com/technologies/details/cm-wordpress/all/all">28% of all websites</a> on the internet. And that is because it's a very robust, easy to use and feature rich content management system (CMS). Everyone from stay at home bloggers to fortune 500 companies rely on it every day. Just like with most platforms, if it isn't properly used or optimized it can turn into a big headache very quickly.

By correcting some of the common issues and mistakes I've seen from WordPress users above you can ensure happier visitors, better conversion rates, lower bounce rate and even improved search engine rankings. It is important for the WordPress community as a whole to <strong>help educate each other on better performance and development practices</strong> as the web continues to evolve.

{{< signature "mc, vf, ms, il" >}}


---
title: 'Don’t Get Crushed By The Load: Optimization Techniques And Strategies'
slug: dont-get-crushed-load-optimization-performance-techniques-strategies
image: null
date: 2013-08-16T16:05:37.000Z
author: bobby-pearson
description: >-
  Despite improvements in broadband and wireless
  Internet, load is in many ways more of an issue now than it was five years ago. The proliferation of mobile devices, [increased user
  expectations](https://www.nytimes.com/2012/03/01/technology/impatient-web-users-flee-slow-loading-sites.html),
  and the very real risks of [losing customers
  and dropping in search result rankings](https://www.smashingmagazine.com/2010/01/page-performance-what-to-know-and-what-you-can-do/)
  have laid a heavy burden on developers to optimize loading time at all costs.
categories:
  - Mobile
  - Techniques
  - Optimization
  - Performance
---
In building websites primarily for the desktop environment, the Web development community previously didn’t spend much time concerning itself with load issues. Selecting the proper image formats and saving our JPEGs for the Web was about as far as many of us would go. On the whole, our hardware and software tools are forgiving enough to accommodate sloppy code. Our production environments can handle thousands of visitors per day, and our clients tend to have predictably manageable traffic.

For all of these reasons and more, Web developers aren’t conditioned to think very hard about the unique load requirements of their clients’ websites. Predictability and complacency can leave our websites vulnerable to traffic spikes, glacial page loading and even downtime. We need to include a specification for load requirements as a regular checklist item when bidding and planning Web work.

{{% feature-panel %}}

## Learn To Love The Content Delivery Network

Content delivery networks (CDNs) are everywhere. And they are our friends. A CDN is a network of servers arrayed across the Internet. These servers work in tandem to serve website content scripts, images, fonts, audio, video and other files — in a distributed fashion. Using a CDN to serve content, your website’s files are pushed out to the edges of the network, several hops and several hundred milliseconds closer to your users.

I highly recommend storing your website’s graphic elements on a CDN. Delivering that 300 KB background image and <a href="https://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/css-sprite-sheets-best-practices-tools-and-helpful-applications/">multi-image sprite</a> on a CDN will dramatically improve your page’s speed and decrease the load on your server. When my company started its website’s mobile-optimized redesign, we ran Google’s <a href="https://developers.google.com/speed/pagespeed/insights">PageSpeed Insights</a> tool and found numerous problems — the scores ranged from 70/100 down to 50/100.

One of the best decisions we made was to combine more than 40 of our images into a single sprite and serve that sprite over our hosting provider’s cloud files system. Rather than loading 40+ individual image files as needed, we have the user load one 275 KB file that is not set to expire for 10 years. Unless we manually update and purge the file on our CDN, users will be able to load a cached version of it from our CDN’s edge nodes (or from their own browser cache) until 2023. Hopefully, bandwidth won’t be as big of an issue by then!

By using the <a href="https://www.smashingmagazine.com/2009/04/27/the-mystery-of-css-sprites-techniques-tools-and-tutorials/">CSS <code>background-position</code> property</a> to display most images as sprites from a master image, we’ve limited the number of HTTP requests. Each <code>div</code> that contains a sprite has a defined height and width in the CSS; so, until the master image is loaded, the user is presented with a blank box.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78de874f-42d2-46ce-aade-72425fab45f7/sprite.png"><img loading="lazy" decoding="async" class="136722" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ddc1d18-e7f7-4010-9656-9bed830cd4e5/sprite-300x300.png" alt="40-image sprite for The Ivy Group" width="500" height="500" /></a><br>
<em>The 40-image sprite used by <a href="https://ivygroup.com/">The Ivy Group</a>.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2e828d8-41a3-4084-9d35-a4690cc310f1/sprite-expiration-date-500.png"><img loading="lazy" decoding="async" class="136723" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2e828d8-41a3-4084-9d35-a4690cc310f1/sprite-expiration-date-500.png" alt="Ivy Group's sprite expires 28 January 2023, 10 years from now" width="508" height="319" /></a><br>
<em>The expiration header for our sprite is set for almost 10 years in the future, ensuring long-term caching on browsers and CDN edge nodes.</em>

Find out from your hosting provider whether it offers CDN services with its hosting packages. Alternatively, providers such as <a href="https://www.rackspace.com/cloud/files">Rackspace</a>, <a href="https://www.bitgravity.com/">BitGravity</a> and <a href="https://www.edgecast.com/">EdgeCast</a> are CDN specialists and can serve as an auxiliary service for your existing hosting solution. Rackspace and BitGravity are both resellers of the Akamai CDN, while EdgeCast runs its own network. Be sure to ask how the CDN will bill you. When I was pricing CDNs for a large file-delivery project, I found some companies will charge you only for downloads from the core of their network, not from the edge nodes, while others charge you for all downloads, regardless of which level of the network responds to each user request.

To host your website’s resource files on a CDN, first obtain an API user name and key from your provider. Use a cloud-file browser such as <a href="https://cyberduck.ch/">Cyberduck</a> to create a CDN “container” (essentially, a directory) for each project or client, and upload the files just as you would with an FTP connection.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7e372b6-08ce-474f-a515-f490e7327e80/cyberduck.jpg"><img loading="lazy" decoding="async" class="136724" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7e372b6-08ce-474f-a515-f490e7327e80/cyberduck.jpg" alt="A collection of files in the ivygroup CDN container, as viewed in Cyberduck" width="500" height="500" /></a><br>
<em>A collection of files in the <code>ivygroup</code> CDN container, as viewed in Cyberduck.</em>

Then, copy the container’s public HTTP or HTTPS path to your clipboard.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b840715-0ad5-48e5-8f94-eb20ff91fdaa/cdn-public-links-78x53.png"><img loading="lazy" decoding="async" class="136725" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b840715-0ad5-48e5-8f94-eb20ff91fdaa/cdn-public-links-78x53.png" alt="The HTTP, HTTPS, Streaming, and iOS Streaming public links to the ivygroup CDN container" width="500" height="339" /></a><br>
<em>The HTTP, HTTPS, Streaming and iOS Streaming public links to the <code>ivygroup</code> CDN container.</em>

Then, simply edit your HTML or CSS code, changing the file paths to reflect the public CDN links. Below is a sample block of CSS showing the HTTP public links to browser-specific style sheets:

<pre><code class="language-markup css">
&lt;!--[if !(IE)]&gt;&lt;!--&gt; &lt;link href="<strong>https://bc0b1dd616f981a9b16b-cd16ce5fde498683e20aaecc086aa721.r81.cf2.rackcdn.com</strong>/style.min.css?v=1.31" rel="stylesheet" /&gt;&lt;!--&lt;![endif]--&gt;
&lt;!--[if gte IE 9]&gt;
&lt;link rel="stylesheet" href="<strong>https://bc0b1dd616f981a9b16b-cd16ce5fde498683e20aaecc086aa721.r81.cf2.rackcdn.com</strong>/style.min.css?v=1.31"&gt;
&lt;![endif]--&gt;
&lt;!--[if lt IE 9]&gt;
&lt;link rel="stylesheet" type="text/css" media="all" href="<strong>https://bc0b1dd616f981a9b16b-cd16ce5fde498683e20aaecc086aa721.r81.cf2.rackcdn.com</strong>/style-ie.css?v=1.10"/&gt;
&lt;![endif]--&gt;
</code></pre>

And here is a sample block of CSS showing how to style a Twitter button (with a hover effect) using a sprite hosted on a CDN:

<pre><code class="language-markup css">
.social-media-block a {
   background: url("<strong>https://bc0b1dd616f981a9b16b-cd16ce5fde498683e20aaecc086aa721.r81.cf2.rackcdn.com</strong>/sprite.png") no-repeat transparent;
   float: left;
   height: 32px;
   margin:0 7px 7px 0;
   padding: 0;
   width: 32px;
}

.social-media-block a#twitter {
   background-position: 252px 667px;
}

.social-media-block a#twitter:hover {
   background-position: 252px 742px;
}
</code></pre>

## Single Vs. Multiple Resource Domains

Linking to resource files on a CDN brings up an interesting optimization issue. Web browsers <a href="https://gtmetrix.com/parallelize-downloads-across-hostnames-implementation-guide.html">limit the number of files</a> that may be loaded in parallel from a single host. You’d think, then, that dispersing all of your resource files across many different host servers would be optimal (for example, <code>content1.mydomain.com</code>, <code>content2.mydomain.com</code>, etc.) — this is known as <a href="https://gtmetrix.com/parallelize-downloads-across-hostnames.html">domain sharding</a>. However, there is a tradeoff, because each host name requires a new DNS lookup to find the host’s IP address, which imposes a cost in loading time. Mobile browsers that connect via the cellular network tend to experience longer lookup times than browsers that connect via traditional cable and DSL modems. It’s a good idea to evaluate your website once all content and resource files are in place and to experiment with multiple domains.

Mobify conducted a test last year that indicated that domain sharding was “<a href="https://www.mobify.com/blog/domain-sharding-bad-news-mobile-performance/">at best neutral and, in most cases, detrimental</a>” to mobile browsers, but feel free to conduct your own testing. At the very least, minimize the total number of files loaded per page, avoid linking to URLs that serve only as redirects to other domains, and use a standard host name convention (i.e. either <code>www.mydomain.com/file.jpg</code> or <code>mydomain.com/file.jpg</code>, not both).</p>

## Identify And Anticipate High-Traffic Periods

Suppose you develop a website for a high-profile event or for an organization whose business is concentrated around a few dates every year. Systems that work fine during the slow periods need to be tested with load in mind.

This is particularly important to administrators who use [shared hosting](https://inmotion-hosting.evyy.net/c/1233229/260033/4222) and have to impose traffic caps on their clients’ websites to protect the server. You might set a traffic cap during the slow period that shuts down the website during a natural high-volume spike, such as one towards the end of a registration period for an event. Be sure to set a generously high traffic cap on any website for which you expect seasonal or irregular traffic patterns, or, better yet, host in a cloud environment that is scalable to meet any traffic demand.

I still burn with shame when remembering how I mistakenly set a hard, rather than a soft, traffic cap on a charity fundraiser website during the “off-season,” only to have the website shut down on the weekend of the event itself. The website had been bouncing along at a stable traffic rate (about half a gigabyte per month) for months, so I set the cap to 2 GB per month and billed the client accordingly (admittedly a low figure, but our hosting model is based on customization and technical support and not on unlimited, unsupported space on a server farm). The website drew almost 2 GB of traffic on the Saturday of the event alone and went down at the worst possible time.

Don’t let this happen to you! My company learned its lesson: We now use only soft traffic caps as notifications of abnormal activity and investigate any notifications on the same day. Speak with your hosting provider to determine its preferred means of managing traffic spikes (see the following section on elasticity and load balancing), and make sure that you can stand behind whatever package of products and services you offer to clients.

## Scalable, Elastic Architecture On The Cloud

Beyond server- and client-side software, there is a wealth of options for how to structure and optimize your website’s hardware infrastructure. Two concepts here are scalability and elasticity, covered in an <a href="https://blog.evolveip.net/index.php/2012/05/24/cloud-elasticity-and-cloud-scalability-are-not-the-same-thing-2/">educational article</a> by Cloud IQ’s Guy Fardone. Scalability is the capacity to increase the load that your website will normally expect: the number of users supported by the system, the maximum size of all uploaded files, etc. A scalable solution is able to be multiplied by a factor of X (for example, “Create three fresh new copies of the system for three new clients,” or “The client has expanded their user base to include all employees beyond the 10-user pilot group; create 1,000 new user accounts each with a 1 GB file store”). Elasticity is the capacity of the website’s infrastructure to expand on demand during load spikes.

Many high-profile websites have implemented a multi-server solution with load balancing. A single load balancer accepts all client traffic and directs each client to one of N available Web servers, which in turn are able to share state information through either a centralized or asynchronous state-management scheme. MSDN has a helpful article about <a href="https://msdn.microsoft.com/en-us/library/ff648960.aspx">load-balancing concepts</a> that is good for beginners (scroll down to figures 2 and 3). Speak with your cloud hosting provider to see what it can provide you, and please share your experiences (good and bad) in the comments below.</p>

## Plan For Load Testing

Last year, my company finished the front-end work for a digitized collection of documents related to the founding fathers of the United States, overseen and funded by the US National Archives. Our client, the University of Virginia’s University Press, wisely budgeted several months to load-test the database and document-delivery system in conjunction with the National Archives’ technical team.

This made us realize that small Web development businesses and freelancers, too, often take load testing for granted. If a page loads within a few seconds while we’re developing, what’s the problem? By disregarding loading issues, the developer, first, misses the opportunity to add value to the delivered product and, secondly, allows a potential risk to go unmanaged.

Several load-testing services are out there: <a href="https://loadimpact.com/">Load Impact</a> and <a href="https://blitz.io/">Blitz</a> offer free trials and are worth investigating. If you have the technical ability and permission level, you could also try installing a server-side open-source load-testing tool such as <a href="https://jmeter.apache.org/">JMeter</a> or <a href="https://httpd.apache.org/docs/2.2/programs/ab.html">ab</a> from Apache. JMeter can test a wide variety of server and service types, while ab specializes in HTTP benchmarking. A reliable load tester that you would be comfortable operating and in whose results you can be confident would make a useful addition to your toolbox.

Below is a screenshot of a Blitz load test on my company website’s news page. Although the page has a very high page-speed score of 95 — due to optimized images, browser caching, minified CSS and JavaScript files, deferred loading and a few other tricks (more on those later!) — it could use some database and memory optimization. A single user will start to see formatted content displayed on their browser within 0.2 seconds, and the full page will load within 1.2 seconds. However, the page runs the risk of throwing errors and timeouts when the number of concurrent users hits 34.</p>

### Pre-Optimization: 6 Errors, 16 Timeouts, Max 3.0-Second Response Time

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51e4cb54-0d68-4d49-8999-3efb5ff26ca3/ivygroup-blitz-1.png"><img loading="lazy" decoding="async" class="136726" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51e4cb54-0d68-4d49-8999-3efb5ff26ca3/ivygroup-blitz-1.png" alt="Ivy Group page under load test throws 6 errors, 16 timeouts" width="500" height="208" /></a><br>
<em>As the number of simultaneous users increases from 0 to 50 over a 30-second period, the response time climbs from 600 milliseconds to just over 3 seconds.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b75ba0d-3d59-47db-ab5f-f86e8a2a0f66/ivygroup-blitz-1b.png"><img loading="lazy" decoding="async" class="136727" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b75ba0d-3d59-47db-ab5f-f86e8a2a0f66/ivygroup-blitz-1b.png" alt="Ivy Group page under load throws errors and timeouts at the 25-second mark" width="500" height="162" /></a><br>
<em>Green denotes hits; red, errors; and orange, timeouts. The website maxes out at 9 users per second around the 18-second mark. At 25 seconds, 3 users per second are experiencing timeouts. At 30 seconds, over 1 user per second is receiving an error message.</em>

I took steps to remedy this by increasing the MySQL connection pool and by implementing in-memory caching via memcached. (Note that these are advanced server-administration tasks and should not be attempted without expert assistance.) Increasing our maximum number of allowed MySQL connections from 100 to 200 failed to change our load-testing results — your mileage may vary. However, I did have success when I decided to…

## Use Memory Caching

Memcached is a fantastic extension that can be used to selectively store and retrieve query results from memory and to avoid making repetitive database calls, file-read operations and other server-side calculations. Other memory caching extensions are available that are worth comparing, but they all have some sort of key-value pair architecture for quick read/write access in memory and a fixed time-to-live so that data won’t cache persistently and result in an overflow.

Script Tutorials has two sets of sample code that demonstrate “<a href="https://www.script-tutorials.com/how-to-use-apc-caching-with-php/">How to Use APC Caching</a>” and “<a href="https://www.script-tutorials.com/how-to-use-memcache-with-php/">How to Use Memcache in PHP</a>.” I selected memcached and successfully improved our website’s performance — adding a single <code>memcache()</code> call in one of my most-used database functions decreased our total errors during a 30-second rush from 6 to 1 and our total timeouts from 16 to 7.</p>

### Post-Optimization: 1 Errors, 7 Timeouts, Max 2.5-Second Response Time

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4bab9e6-64b9-48f9-b465-f78ca62a2079/ivygroup-blitz-2.png"><img loading="lazy" decoding="async" class="136728" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4bab9e6-64b9-48f9-b465-f78ca62a2079/ivygroup-blitz-2.png" alt="Ivy Group page under load has improved response time with memcached" width="500" height="208" /></a><br>
<em>After applying memcached to one database function, the maximum response time at peak load fell from 3 to 2.5 seconds. The website performs measurably better during the 0- to 20-second period (between 1 and 35 simultaneous users). Note that the y-axis scale is not equal to the y-axis of the previous “Response Time” graph.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b89393b-f3c8-43d0-9f56-0a92ccc77654/ivygroup-blitz-2b.png"><img loading="lazy" decoding="async" class="136729" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b89393b-f3c8-43d0-9f56-0a92ccc77654/ivygroup-blitz-2b.png" alt="Ivy Group page under load experiences far fewer errors and timeouts after implementing memcached" width="500" height="164" /></a><br>
<em>Green denotes hits; red, errors; and orange, timeouts. After applying memcached to one database function, the website experienced a marked decrease in errors and timeouts during high usage. Further use of memcached is recommended. Note that the y-axis scale is not equal to the y-axis of the previous “Hit Rate” graph.</em>

### MySQL Query Cache

Memcached isn’t the only caching tool at your disposal. MySQL enables you to access query results directly from memory using <a href="https://www.docplanet.org/mysql/mysql-query-cache-in-depth/">Query Cache</a>. It has both advantages and disadvantages when compared to memcached; the two should not be treated as interchangeable. MySQL Query Cache is ideal for caching data that is seldom changed, <a href="https://www.rackspace.com/blog/memcached-more-cache-less-cash/">as Rackspace explains</a>. Rackspace’s key takeaway is this:
<blockquote>When you use a MySQL database, each time you INSERT, UPDATE, or DELETE a row from the MySQL database, <strong>the entire query cache for that table is invalidated</strong>. That means that the next request for every single session will be a cache miss, and must access the data from disk on the database server.</blockquote>

Memcached treats every SQL query and result as a unique key-value pair, so an entire table’s worth of <code>SELECT</code> queries will never be invalidated all at once if anything is changed. MySQL Query Cache recognizes that any change to any row in a table might affect any further queries on that table. It’s up to you, with your knowledge of your application, to determine whether one or both of these tools are worth implementing.

Test different values of the <code>query_cache_size</code> parameter in MySQL Query Cache and of both the cache size and timeout limit in memcached. There is no “correct” value for any of these parameters. It’s all based on your hosting environment, application structure and expected load.

Memcached and MySQL caching are relatively advanced techniques that require some fine-tuning to really be of any use. So, what about the low-hanging fruit? Fortunately, some other techniques are quicker and easier to implement, starting with…

## Compressing Resources

Apache has a built-in way to selectively <a href="https://httpd.apache.org/docs/2.2/mod/mod_deflate.html">compress files on request</a>. In your <code>.htaccess</code> or, preferably, <code>httpd.conf</code> file, specify which content types should be compressed, like so:

<pre><code class="language-markup text">
&lt;ifmodule mod_deflate.c&gt;
         AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css application/x-javascript application/javascript text/text
 &lt;/ifmodule&gt;
</code></pre>

This specifies that the server should compress all files recognized as being HTML, XML, CSS, JavaScript and plain-text content types. Your server might not recognize other content types that should be compressed, such as OpenType, EOF and TrueType font files. If that is the case, you can specifically add those types using <code>mod_mime</code>:

<pre><code class="language-markup text">
&lt;ifmodule mod_deflate.c&gt;
         &lt;ifmodule mod_mime.c&gt;
                 Addtype font/opentype .otf
                 Addtype font/eot .eot
                 Addtype font/truetype .ttf
         &lt;/ifmodule&gt;
         AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css application/x-javascript application/javascript text/text font/opentype font/truetype font/eot
 &lt;/ifmodule&gt;
</code></pre>

For additional compression steps and methods, check out <a href="https://viralpatel.net/blogs/compress-php-css-js-javascript-optimize-website-performance/">Viral Patel’s adventures</a> with Gzip, Deflate and PHP output buffering.</p>

## Concatenate Files

Besides compressing resource files, you can also concatenate them in a variety of ways. Rob Flaherty documents a way to <a href="https://www.ravelrumba.com/blog/css-js-concatenation-versioning-php/">concatenate all JavaScript files using PHP code</a>. Apache Ant enables you to configure a website build to <a href="https://ant.apache.org/manual/Tasks/concat.html">concatenate files</a> without modifying the website’s code. Note that this won’t work if you deliver your resource files over the CDN! They are mutually exclusive techniques.</p>

## Optimize JavaScript Loading

One of the simplest things you can do to accelerate your website’s loading time is to move any <code>&lt;script&gt;</code> tags from the <code>&lt;head&gt;</code> to the end of the HTML. As <a href="https://developers.google.com/speed/docs/best-practices/payload#DeferLoadingJS">Google Developers explains</a>, any JavaScript that defines user interaction or modifies loaded HTML content (such as <code>onClick</code> and <code>onLoad</code> events) can be deferred until all other HTML has loaded. By moving JavaScript references out of the <code>&lt;head&gt;</code> tag, you cut down the time it takes for a user’s browser to start loading the <code>&lt;body&gt;</code> and to actually display the content. The quicker you load the <code>&lt;head&gt;</code> tag and start displaying content, the better. Letting the user know that <em>something</em> is happening is preferable to showing a blank white screen for a second or two while all of those resource files load.</p>

## Assign Load Testing: DIY Or Outsourced?

For large-scale national clients and enterprise applications, it’s probably more efficient for a small development firm to outsource load testing to a specialist. The National Archives client outsourced this work to IBM, which acquired Rational Machines back in 2003 and is an industry leader in the full range of software testing — load, unit and accessibility testing, etc.

Take this opportunity to <a href="https://www.webperformance.com/load-testing/blog/2010/03/should-we-outsource-load-testing-or-do-it-ourselves/">decide on your business’ core competencies</a>. Ask yourself, how deep into the bytes will you venture? On the other hand, if your firm has decided to outsource load testing, please let us know in the comments section.</p>

## Bill Accordingly

As your firm increases its core competencies to include load-time optimization, CDN content delivery and load testing, remember to account for the extra value that you add to your clients in the bottom line. Whether these services are line items in your standard contract or not, you’d be selling yourself short by failing to highlight them and citing them to justify your rates.

Slow page-loading times translate into <a href="https://blog.kissmetrics.com/loading-time/">frustrated users</a> and <a href="https://blog.tagman.com/2012/03/just-one-second-delay-in-page-load-can-cause-7-loss-in-customer-conversions/">lost opportunities</a>: in sales, interaction, page visits, advertising impressions, etc. Most clients will glaze over if you go into too much technical detail, so keep your conversations focused on results.  Discuss metrics with your client to figure out what they want out of the project: few clients will come to you asking to decrease their average page-loading time by 25%, but many will tell you they want to increase sales, receive more user feedback or attract eyeballs.

Your expertise is worth it.

{{< signature "al" >}}


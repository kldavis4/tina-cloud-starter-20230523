---
title: Secrets Of High-Traffic WordPress Blogs
slug: secrets-high-traffic-wordpress-blogs
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0e5a98b-9428-4cce-82e4-ccab34f89931/wordpress-blue-illu.jpg
date: 2012-09-12T12:42:25.000Z
author: siobhan-mckeown
description: >-
  We all know that WordPress is awesome - but being awesome isn't always enough.
  Does it perform well under pressure? Can it deal with traffic from millions of
  visitors every month? There's no question that WordPress can be used for your
  or my blog, but what about multi-authored blogs with thousands of comments?
  How do developers make it scale and perform?
categories:
  - WordPress
  - Plugins
  - Optimization
  - Techniques (WP)
---
We all know that WordPress is awesome — but being awesome isn’t always enough. Does it perform well under pressure? Can it deal with traffic from millions of visitors every month? There’s no question that WordPress can be used for your or my blog, but what about multi-author blogs with thousands of comments? How do developers make it scale and perform?

I spoke with the developers behind some of the biggest WordPress blogs on the planet and asked them to tell me their secrets. Now I get to share them with you.</p>

## The Blogs

<table class="article-table three-columns"><br>
<tbody>
<tr>
<td><strong>Website</strong></td>
<td><strong>Monthly uniques</strong></td>
<td><strong>Monthly page views</strong></td>
</tr>
<tr>
<td><a href="https://www.digitaltrends.com/">Digital Trends</a></td>
<td>10 – 12 million</td>
<td>33 million</td>
</tr>
<tr>
<td><a href="https://www.iphoneclub.nl/">iPhoneclub.nl</a></td>
<td>2.5 million</td>
<td>5.4 million</td>
</tr>
<tr>
<td><a href="https://thenextweb.com/">The Next Web</a></td>
<td>4 million</td>
<td>8 million</td>
</tr>
<tr>
<td><a href="https://www.neatorama.com/">Neatorama</a></td>
<td>2.5 million</td>
<td>4.5 million</td>
</tr>
<tr>
<td><a href="https://www.slashgear.com/">Slashgear</a></td>
<td>6 million</td>
<td>10 million</td>
</tr>
<tr>
<td><a href="https://hotair.com/">Hot Air</a></td>
<td>2 – 3 million</td>
<td>35 – 45 million</td>
</tr>
<tr>
<td><a href="https://laughingsquid.com/">Laughing Squid</a></td>
<td>Undisclosed</td>
<td>Undisclosed</td>
</tr>
</tbody>
</table>

## In The Beginning

The first thing I asked the developers was whether they prepared for the heavy traffic that now flows through their website. In almost all cases, the answer was a resounding no. From The Next Web, CTO Arjen Schat and lead developer Pablo Roman said they had planned for growth but didn’t expect growth to happen on such a large scale. “There were few large WordPress sites at the time, so we learned as we went along.”

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Navigation For Mega-Sites](https://www.smashingmagazine.com/2013/03/navigation-mega-sites/)
*   [The Ultimate Guide To Choosing A WordPress Host](https://www.smashingmagazine.com/2014/09/the-ultimate-guide-to-choosing-a-wordpress-host/)
*   [Speeding Up Your Website’s Database](https://www.smashingmagazine.com/2011/03/speeding-up-your-websites-database/)
*   [Are You Loosing Traffic By Poor Website Performance?](https://www.smashingmagazine.com/2010/01/page-performance-what-to-know-and-what-you-can-do/)

Neatorama started out in late 2005 on <strong>cheap shared hosting until it got kicked out</strong>. It moved to a VPS and got kicked out again. In 2007, it moved to a dedicated server with a CDN, which eventually was insufficient, until finally it moved onto load-balanced servers with a CDN. Similar stories are echoed by iPhoneClub.nl and Laughing Squid.

Hot Air’s developer, Mark Jaquith, also a lead developer at WordPress, had to migrate the website to a new server within 48 hours of launching. Only SlashGear planned for a 30% increase in traffic per year.

<figure><a href="https://www.digitaltrends.com/"><img loading="lazy" decoding="async" title="Digital Trends" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3b258de-3994-4925-a7d3-45db81664590/digitaltrends.jpg" alt="Digital Trends" /></a></figure>

Digital Trends started out with around a million uniques a month and has since risen to 10 to 12 million uniques. Tom Willmot, of <a href="https://hmn.md">Human Made</a>, the development shop behind Digital Trends, said this of starting out:
<blockquote>When I started work on the website, there were some pretty big performance sinks in the code base that needed ironing out. A clean code base takes you only so far, however. I don’t think it’s something that should be too heavily focused on at the outset as you don’t know what specific features will need performance considerations. Coding well plus some persistent object caching are enough to begin with.</blockquote>

## Server Shred And Burn

High-traffic blogs have to deal with things that regular bloggers only dream of: loads and loads of visitors, eager to read all of the latest news. Neatorama held up when it was featured on the front page of Digg, but was shredded within a few minutes of being featured on Yahoo’s front page — over 2 million visits in the space of a few hours. To deal with that, it had to make a static page on a CDN and redirect traffic there.

Other blogs face challenges related to major events. Visitors flock to their websites to follow what’s happening and hear the news. iPhoneClub.nl and SlashGear are particularly affected during Apple’s live broadcasts. SlashGear experiences traffic of more than 4 million uniques within the two hours of a broadcast’s duration; to deal with this, it adds Amazon EC2 to its normal infrastructure.

<figure><a href="https://www.iphoneclub.nl/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cd434d2-53bf-4986-80a0-ec5aa1203895/iphoneclub1.jpg" alt="iPhoneclub.nl" /></a></figure>

Jean-Paul Horn, whose iPhoneclub.nl started out on WordPress 2.0.5, had to learn to deal with these problems on the fly:
<blockquote>We used to run a standard LAMP stack with WP Super-Cache, since the site was already growing rapidly when the iPhone started to get really popular. Our main problem was that the server ran perfectly fine on normal news days, but almost literally burned whenever Apple had a keynote or another big iPhone-related announcement. We tried preparing for these short avalanches by temporarily adding more cores and RAM, but it was never really enough, and I wasn’t really keen on investing in a big-ass server just for two to three days of insane amounts of Web traffic a year.</blockquote>

While moving to a Web server and database server with MySQL stored on a separate server helped in its continuing growth, it was still dealing with the same issues when Apple held a press conference. Enter Frederick Townes of <a href="https://www.w3-edge.com/">W3 Total Cache</a> and Mashable fame. Jean-Paul met Frederick at WordCamp Netherlands, and Frederick went on to help them set up their current configuration:

*   The app server hosts the Varnish front end.
*   They use two nginx Web servers: one with PHP-FPM, the other with static content, like a CDN.
*   The database server runs a highly tuned MySQL server, in which some of the WordPress tables, such as `wp_posts`, have been transitioned from MyISAM to InnoDB. Because InnoDEV doesn’t have full text search, Sphinx Search was implemented.
*   A performance analysis was carried out using the cachegrind files that xdebug generates to easily identify execution time optimization opportunities that preventing the servers from running cool and addressing cache misses quickly.

Jean-Paul has been using this configuration since November 2011 and has survived two major Apple events without any of the previous load issues or other performance troubles. They’ve also been able to accommodate more traffic and have beaten all of their previous traffic records.</p>

## Dealing With Growth

### Hot Air

<figure><a href="https://hotair.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94853d10-be49-4b2f-b0c7-bd58f1cd2a39/hotair.jpg" alt="Hot Air" /></a></figure>

US political blog Hot Air has gone through some major performance and scaling sprints, particularly in advance of US election years. An election guarantees a larger than average flurry of activity around politics. Given that politics is already one of the most popular topics on the Internet, this means some hardcore scaling. Mark Jaquith explained to me the steps he has taken to cope with scaling:

*   Deliver all static assets through a CDN.
*   Set up a load balancer, with multiple Web back-ends behind it.
*   Cache the front page proactively
*   Cache page fragments (such as sidebars) proactively, so that they can be loaded statically.
*   Cache recent posts proactively (mostly the ones displayed on the home page). Every time a post is updated or a comment is left, a back-end process generates a new static snapshot of the page and distributes it to the Web machines.
*   Eliminate the cache differentiation between logged-in and anonymous viewers. Most caching plugins don’t cache pages for logged-in users, or if they do, they cache a different version for each viewer. Hot Air’s templates are modified so that there is no difference in the HTML generated for logged-in and anonymous users, so there can be one shared cache pool.
*   Use Batcache (with a Memcached object cache back end) to cache views of old content.</p>

### The Next Web

<figure><a href="https://thenextweb.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32a431b0-207c-4247-a62e-83630ba3e640/tnwlogo.png" alt="The Next Web" /></a></figure>

As with most of these other blogs, scaling was forced upon The Next Web. The founders did plan for growth, but not on the scale they encountered. Arjen and Pablo went into detail on how they dealt with it.

The team’s essential tools are:

*   [Varnish](https://www.varnish-cache.org/) as a reverse proxy and for ESI (Edge Side Includes);
*   [Memcached](https://memcached.org/) to store the results of heavy queries, such as popular stories;
*   [Munin](https://munin-monitoring.org/) for monitoring.

Setting this up wasn’t enough, though. All of this had to be tuned, and poorly performing plugins and code had to be identified. To do this, they did the following:

*   **Use MySQL slow query log with `no-index` enabled.** Keeping your MySQL slow logs empty is essential. Your key cache suddenly might not be sufficient anymore if your data is growing.
*   **Use XHprof for code path analyses.**
*   **Keep Apache logs clean.**.  External referrers will link to pages on your website that don’t exist anymore. If a WordPress 404 page is loaded every time, then you’re doing work that can be avoided. Generating a 404 page can be heavy, so it needs to be cacheable in Varnish as well.

The team at The Next Web also uses additional tools with Varnish to improve cache hit rate. These include:

*   `varnishtop` Lets you look into Varnish.
*   `varnishtop -i txurl` This shows you all of the requests that make it into Apache that aren’t cached by Varnish. This helps you to identify different cases:
    *   Whether the back end sends a header that Varnish can’t cache;
    *   Whether the back end starts a session that isn’t needed;
    *   Partially malformed links to your website, such as `https://thenextweb.com/apple/https://referrer.com/my/cool/article`;
    *   Small variations of a normal request that you can normalize in Varnish, so that you can serve the standard page, such as `https://thenextweb.com/correct/article/link?utm=campaign`.
*   `[WP-VCL](https://github.com/thenextweb/wp-vcl)` Their basic VCL, which normalizes many different request into the standard versions.

An essential step for The Next Web was developing the ability to serve cached content to logged-in users. To do this, it pulls in all of the user-specific parts of the page and loads these through an AJAX call. This means that content doesn’t need to load all of WordPress. The developers have duplicated all of the code that is needed to handle logging in and basic user-profile stuff in WordPress into its own tiny login class. The class takes 1 millisecond to load, instead of 100 to 200 milliseconds to load through the whole WordPress stack. This prevents WordPress from loading for a trivial request, which can degrade the overall performance of your website by eating CPU cycles that should be used to render pages that are not cached. An added benefit is that WordPress can render all pages in non-logged-in mode.

This is used simultaneously as a feature of Varnish called ESI, which lets the team cache different sections of a page separately with different expiration times. This lets them show fresh content in the sidebar widgets even if the main content has a long expiration time.

## Essential Plugins

*   [W3 Total Cache](https://wordpress.org/extend/plugins/w3-total-cache/): iPhoneClub.nl, The Next Web, Digital Trends
*   [WP Super Cache](https://wordpress.org/extend/plugins/wp-super-cache/): Laughing Squid
*   WP Widget Cache: iPhoneClub.nl
*   [Plugin Output Cache](https://wordpress.org/extend/plugins/plugin-output-cache/) in conjunction with [Similar Posts](https://wordpress.org/extend/plugins/similar-posts/), [Recent Posts](https://wordpress.org/extend/plugins/recent-posts-plugin/) and [Recent Comments](https://wordpress.org/extend/plugins/recent-comments-plugin/): iPhoneClub.nl
*   [Clean Options](https://wordpress.org/extend/plugins/clean-options/): iPhoneClub.nl To keep WordPress’ easily bloated options table tidy.
*   [WordPress Sphinx search plugin](https://wordpress.org/extend/plugins/wordpress-sphinx-plugin/): iPhoneClub.nl To connect WordPress with the open-source Sphinx search project.
*   [WPVarnish](https://github.com/pkhamre/wp-varnish): The Next Web or cache busting.
*   [Term Management Tools by Scribu](https://wordpress.org/extend/plugins/term-management-tools/): Hot Air Useful for merging duplicate tags.
*   [Memcached Object Cache Plugin](https://wordpress.org/extend/plugins/memcached/): Digital Trends Lets you run a persistent object cache outside of PHP-APC. This is important if you’re running multiple servers.
*   [Varnish](https://www.varnish-cache.org/): Digital Trends

## Essential Tools And Services

*   [VaultPress](https://vaultpress.com/): Hot Air Real-time back-ups.
*   WordPress.com stats: Hot Air
*   [Google Analytics](https://www.google.com/analytics/): Hot Air
*   [Chartbeat](https://chartbeat.com/) and [Newsbeat](https://chartbeat.com/publishing/): Hot Air
*   A CDN: everyone
*   [SoftLayer](https://www.softlayer.com/): Slashgear A dedicated hosting company that Slashgear has been with for seven years.
*   [Cloudflare](https://www.cloudflare.com): Laughing Squid Provides Web performance and scalability services.
*   [Disqus](https://disqus.com/): Slashgear Helps to socialize engagement and offset comment loads from its servers.
*   [Solr](https://lucene.apache.org/solr/): The Next Web For search.</p>

## Challenges

### High Levels of Caching

All of the blog owners I spoke with have high levels of caching. Digital Trends deals with this by using Akamai Distributed, Varnish and Memcached. When this is combined with user log-ins and registrations, it can be difficult to make sure that everyone is seeing what they should be seeing while caching as many things as possible.</p>

### Mobile

iPhonclub.nl has to deal with a relatively high number of mobile visitors. In the past, it used WPTouch for iPhone visitors (along with its native app). The server team had to do major work with Varnish, nginx, and W3TC to keep the caches for desktop and mobile visitors separate, thus making user configuration more complex. However, later this year iPhoneclub.nl will merge with <a href="https://www.ipadclub.nl/">iPadclub.nl</a> to become <a href="https://iCulture.nl">iCulture.nl</a>. In addition to the merge, they are moving to a responsive design, which will better suit the new website and solve the issue of dealing with mobile visitors.</p>

### Built to Work, Not to Perform

A challenge raised by The Next Web is the actual architecture of WordPress. While using all of the options and all of the plugins is easy, they are built to work, not to perform. With every code change, you have to make sure it doesn’t cripple performance.</p>

### Security

Security is a big issue for every WordPress user, particularly for high-visibility websites. As Neatorama points out, keeping WordPress up to date isn’t always enough. You also have to keep your server’s operating system up to date as well.

<figure><a href="https://www.flickr.com/photos/66841393@N00/100490646/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fa5bf34-79fa-4814-aed9-56623d223404/server.jpeg" alt="Huge Servers" /></a><figcaption>Some websites need a huge server. (Image: <a href="https://www.flickr.com/photos/66841393@N00/100490646/">Skimaniac</a>)</figcaption></figure>

### Scalability

Slashgear has found it challenging to scale WordPress without chucking more hardware at it. It uses a caching system, but WordPress is built to be dynamic, and caching in a dynamic environment does not always work smoothly. The developers have overcome this by modifying their plugins to use AJAX to pull live data on statically cached generated pages.</p>

### Comments

A website like Hot Air can receive hundreds or even thousands of comments for a single post. There are dozens of posts every day, and the website has been live for six years. “With that many comments,” says Mark, “you really have to look at database optimization. We have a few custom plugins that intercept comments queries and rewrite them to be simpler. And you want to limit the number of queries you make against that table. For instance, I killed the ‘Right Now’ and ‘Recent Comments’ sections of the Dashboard.”

### Events

As discussed regarding iPhoneclub.nl and SlashGear, Hot Air has to deal with its own major events. When a big political event is happening, just a few minutes of downtime can do damage. Mark has warning systems and automated responses in place. In the event of an problem, he can set up something to automatically fix it if it recurs or to notify him when something indicates that a performance issue is imminent.</p>

## Would You Say Goodbye To WordPress?

I asked all of the blogs whether they’ve ever conceived of a situation in which they would have to move beyond WordPress. Here’s what they had to say.</p>

### Tom Willmot, Digital Trends

<blockquote>I really don’t like the whole “WordPress is slow” rhetoric. It’s just PHP plus MySQL — so is Facebook. It is possible to move beyond certain things that WordPress does (for example, perhaps you replace the rewrite engine with something more efficient), but to decide fundamentally that WordPress is somehow slow and needs to be gotten rid of is probably avoiding the specific issue that is the problem. Sure, there are aspects of WordPress that can be slow if you don’t do anything about them, but this is far outweighed by everything that you do get.

Writers love the WordPress back end; <a href="https://wordpress.com">WordPress.com</a> runs some of the largest websites in the world. Digital Trends servers 33 million pages a month for a website that is hugely more complicated (from a technical point) than a blog.</blockquote>

### Jean-Paul Horn, iPhoneclub.nl

<blockquote>I can’t for the life of me think why I would want to do this. I have been using WordPress since early 2.0. My wife started iPhoneclub.nl in December 2006 on WordPress 2.0.5 and we haven’t looked back since. I had some previous experiences with PHP-Nuke and Joomla, but WordPress has really grown on me for its simplicity and <strong>huge</strong> developer community.

For almost every missing piece of functionality in core, a plugin is available or so easy to patch that you could write your own theme-specific function. I evaluated both Drupal and ExpressionEngine (then called pMachine) when we faced our performance issues, but stuck with WordPress because of its extensibility and there was already a clear vision laid out for WordPress becoming more of a full-featured CMS.</blockquote>

### The Next Web

<blockquote>I don’t see a situation where you need to move beyond WordPress, as long as you don’t fall into the trap of thinking you can do everything with a plugin.</blockquote>

### Laughing Squid

<blockquote>WordPress continues to evolve along with us and is still the best platform out there for blogging. There is every indication that it will continue to be so in the future.</blockquote>

### SlashGear

<blockquote>[We would leave] when WordPress becomes too bloated. As you can see, each major WordPress version comes with more hooks (WordPress 3.0 had a little over 750 hooks, and 3.4 has over 1500 hooks). At this point, we prefer scalability and platform robustness over features that are not commonly used.</blockquote>

### Mark Jaquith, Hot Air

<blockquote>No way. Comments are the hardest thing to scale, and there are solutions for that, such as using an external service or even sharding comments between multiple tables. I haven’t yet come across a problem that I didn’t think could be solved, and the flexibility and extensibility of WordPress have proved invaluable.</blockquote>

## Saying Goodbye

Why would anyone ever want to leave WordPress? One of the blog owners I spoke with was in the process of doing just that. Neatorama’s e-commerce operation, <a href="https://www.neatoshop.com/">NeatoShop</a>, has grown, and it has decided to integrate the blog and the shop into one platform. This makes it possible for it to tailor its publishing process to fit its particular needs, such as scheduling and queueing multiple posts, maintaining multiple blogs with a single dashboard, cross-posting and having an inline commenting system. For Neatorama, the problem wasn’t WordPress itself, but that they couldn’t implement large-scale e-commerce.

<figure><a href="https://www.neatoshop.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b9df83f-d794-43c4-ab28-4e73d3501130/neatoshop.jpg" alt="Neatoshop" /></a></figure>

I asked Alex Santoso of Neatorama why he hadn’t considered using a WordPress e-commerce plugin such as WooCommerce or WP E-Commerce. Here’s what he had to say:
<blockquote>Because e-commerce isn’t just a shopping cart — there’s a whole other logistics fulfilment and shipping back end to it. We grew NeatoShop from selling just 12 t-shirts to over 5,000 items today, and we had to write our own software to enable us to process (i.e. ship) orders efficiently.

I’m doubtful that you can do large-scale e-commerce with plugins. Selling a dozen items or so should be no problem, but keeping track of thousands of items in inventory, minimizing fraud, automating, and the logistics would be.</blockquote>

It’s interesting that Neatorama feels that plugins aren’t sufficient to carry out large-scale e-commerce. But how does Alex feel about WordPress as a publishing platform?
<blockquote>We’re not moving away from WordPress because it’s failing us as a blogging platform. Rather, our business evolved from being a pure publisher into a side-by-side e-commerce and blogging operation. WordPress and its vibrant community continue to be a great choice for most publishers big and small.</blockquote>

## Learning From The Pros

It’s great to hear about what all of these websites are doing, but what advice can they offer you?

### Servers

Learn how to deal with servers, or get someone who does. You should know how to configure nginx and PHP-FPM, MySQL slaved with HyperDB, Varnish VCLs, and NFS. “If you don’t know how to deal with the stuff in between a browser sending the request and your code running,” warns Tom Willmot, “it will seriously limit you in terms of how things can be improved and also debugging issues. Server issues can be extremely frustrating; if you don’t have a handle on it, it will come back to bite you.”

### Read and Learn

Jean Paul Horn advises that you should keep up with the latest performance recommendations, and he particularly recommends the following:

*   [Steve Souders](https://stevesouders.com),
*   [Web Performance Today](https://webperformancetoday.com),
*   Articles about performance right here on Smashing Magazine,
*   A saved Twitter search with the [#webperf](https://twitter.com/search/?q=%23webperf) hash tag.</p>

### Ask for Help

“Don’t be afraid to ask for help,” says Jean Paul. “The community out there is exceptional and truly supportive.” Spend money hiring WordPress performance experts. This provides an excellent return on investment. If your website goes down or is unreachable, potential readers could end up with the competition. Trying to visit a website that is constantly down is frustrating for the visitor, and they won’t stick around.</p>

### Shop Around

Alex Santoso suggests that you “Shop around for hosting costs. Similar hardware configurations can have vastly different pricing from different hosting companies.”

### Trail and Error

SlashGear suggests that you use trial and error to get your configuration right. Decide whether a plugin is really necessary. Many plugins use many resources for a simple function that could be hard-coded into the theme. “Adding new hardware and server resources isn’t always the solution,” said Ewdison Then, “but sometimes it’s the only solution.”

### Optimize What Matters

Mark Jaquith recommends that you don’t optimize blindly. “Find out what the biggest bottlenecks are and eliminate them. Rinse and repeat.”

## WordPress Performance Resources

If you feel inspired to start scaling, here are some resources to check out:

*   “[Scaling, Servers and Deploys, Oh My!](https://wordpress.tv/2011/08/20/mark-jaquith-scaling-servers-and-deploys-oh-my/)” (video), Mark Jaquith
*   “[High Performance WordPress](https://themesforge.com/theme-news/high-performance-wordpress-part-1/)” Themes Forge A three-part series.
*   “[WordPress Performance Server: Debian ‘squeeze’ with Nginx, APC and PHP from the Dotdeb repos](https://c3mdigital.com/wordpress-performance-server/),” Chris Olbekson, C3M Digital
*   “[Do-It-Yourself Caching Methods With WordPress](https://www.smashingmagazine.com/2012/06/26/diy-caching-methods-wordpress/),” Milan Petrović, Smashing Magazine
*   “[Performance Optimization for Websites](https://www.smashingmagazine.com/smashing-book-1/performance-optimization-for-websites/),” Rene Schmidt, The Smashing Book
*   "[Scaling WordPress](https://scalingwp.wordpress.com/)" WordPress experts share advice on scaling

Many thanks to all of the people who contributed their knowledge to this post:

*   Tom Willmot ([Human Made](https://hmn.md/)) for [Digital Trends](https://www.digitaltrends.com/);
*   [Jean-Paul Horn](https://www.textopus.nl/) for [iPhoneclub.nl](https://www.iphoneclub.nl/);
*   Zee M Kane, Pablo Román and Arjen Schat for [The Next Web](https://thenextweb.com/);
*   Alex Santoso for [Neatorama](https://www.neatorama.com/);
*   [Ewdison Then](https://www.ewdisonthen.com/) for [Slashgear](https://www.slashgear.com/);
*   [Mark Jaquith](https://markjaquith.com/) ([Covered Web Services](https://coveredwebservices.com/)) for [Hot Air](https://hotair.com/);
*   Scott Beale for [Laughing Squid](https://laughingsquid.com/);
*   And thanks to [Simon Wheatley](https://simonwheatley.co.uk/) ([Code for the People](https://codeforthepeople.com/)) for a final sanity check.</p>

### Optimize What Matters

Mark Jaquith recommends that you don’t optimize blindly. “Find out what the biggest bottlenecks are and eliminate them. Rinse and repeat.”

## WordPress Performance Resources

If you feel inspired to start scaling, here are some resources to check out:

*   “[Scaling, Servers and Deploys, Oh My!](https://wordpress.tv/2011/08/20/mark-jaquith-scaling-servers-and-deploys-oh-my/)” (video), Mark Jaquith
*   “[High Performance WordPress](https://themesforge.com/theme-news/high-performance-wordpress-part-1/)” Themes Forge A three-part series.
*   “[WordPress Performance Server: Debian ‘squeeze’ with Nginx, APC and PHP from the Dotdeb repos](https://c3mdigital.com/wordpress-performance-server/),” Chris Olbekson, C3M Digital
*   “[Do-It-Yourself Caching Methods With WordPress](https://www.smashingmagazine.com/2012/06/26/diy-caching-methods-wordpress/),” Milan Petrović, Smashing Magazine
*   “[Performance Optimization for Websites](https://www.smashingmagazine.com/smashing-book-1/performance-optimization-for-websites/),” Rene Schmidt, The Smashing Book
*   "[Scaling WordPress](https://scalingwp.wordpress.com/)" WordPress experts share advice on scaling

Many thanks to all of the people who contributed their knowledge to this post:

*   Tom Willmot ([Human Made](https://hmn.md/)) for [Digital Trends](https://www.digitaltrends.com/);
*   [Jean-Paul Horn](https://www.textopus.nl/) for [iPhoneclub.nl](https://www.iphoneclub.nl/);
*   Zee M Kane, Pablo Román and Arjen Schat for [The Next Web](https://thenextweb.com/);
*   Alex Santoso for [Neatorama](https://www.neatorama.com/);
*   [Ewdison Then](https://www.ewdisonthen.com/) for [Slashgear](https://www.slashgear.com/);
*   [Mark Jaquith](https://markjaquith.com/) ([Covered Web Services](https://coveredwebservices.com/)) for [Hot Air](https://hotair.com/);
*   Scott Beale for [Laughing Squid](https://laughingsquid.com/);
*   And thanks to [Simon Wheatley](https://simonwheatley.co.uk/) ([Code for the People](https://codeforthepeople.com/)) for a final sanity check.

{{< signature "al" >}}


---
title: 'Struggling To Get A Handle On Traffic Surges'
slug: struggling-handle-traffic-surges
author: suzanne-scacca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c230b58-ae4b-4c1c-a688-1f2093009d81/struggling-handle-traffic-surges.png
date: 2019-12-10T10:00:00.000Z
summary: >-
  “If you build it, they will come.” That’s certainly true when you put a lot of time and effort into building websites and PWAs for clients. But what happens when “they will come” becomes “too many of them came all at once and now the site’s gone down”? Traffic surges do happen. But rather than let your website become victim to them, this guide will show you how you can set it up to be the victor.
description: >-
  Traffic surges happen, but rather than let your website become victim to them, this guide will show you how you can set it up to be the victor.
categories:
  - Workflow
  - SEO
disable_ads: true
disable_panels: true
---
<p>(This is a sponsored article.) When a traffic spike hits, you want your website to be able to ride the wave instead of drown beneath it.</p>

<p>But how do you do that without constantly overspending on server resources in anticipation of a traffic surge that may or may not happen?</p>

<p>Part of it comes down to knowing how to read your data really well so that you can predict upcoming upticks (or slumps) in traffic. Even then, the ebbs and flows of your data don’t always accurately predict when a traffic surge will hit, how big it will be or how long it will last.</p>

<p>So, what you need to do is make sure your clients’ websites are prepared to take the hit and then sustain the traffic. What we’re going to do today is help you create a system of tools, monitoring, and testing that will enable your websites to do this.</p>

## How To Prepare Your Website For A Traffic Surge

<p>To properly prepare your website for traffic surges, you need to set up a system that’s both proactive and reactive. Here’s what it should include:</p>

### 1. Move Your Website to a Scalable Cloud Solution

<p>The reason why traffic surges are able to wreak havoc on websites is because the hosting servers and resources are unprepared to handle them. Pure and simple.</p>

<p>That said, if you can’t predict when a surge will happen, how do you ensure your hosting has the capacity to handle the increased traffic load? Do you simply throw more money into an oversized hosting plan <em>just in case</em>?</p>

<p>Obviously, that’s not a cost-efficient way to deal with a potential traffic surge. Instead, you should look for a hosting solution that will scale to your needs.</p>

#### Leverage DigitalOcean Hosting Technology

<p>One such provider that can help with this is <a href="https://www.digitalocean.com/">DigitalOcean</a>, a developer of scalable cloud solutions.</p>

<p>What’s nice about this option is that DigitalOcean gives you optimized “droplets” to choose from. There’s no need to guess which plan is right for you &mdash; everything is clearly spelled out in DigitalOcean’s very useful use case recommendations:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5b0cfde-a5f4-47ab-8acf-c8ad88fefeaf/1-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5b0cfde-a5f4-47ab-8acf-c8ad88fefeaf/1-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="DigitalOcean sells virtual CPUs that are optimized for specific use cases. (Source: <a href='https://www.digitalocean.com/'>DigitalOcean</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5b0cfde-a5f4-47ab-8acf-c8ad88fefeaf/1-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="Digital Ocean vCPU droplets" >}}

<p>As you can see, Droplets are easy-to-configure virtual machines built for different kinds of websites and applications. What’s more, they’re configured for speed and security right out of the box with KVM hypervisors, SSD storage and 40GbE connectivity.</p>

<p>What’s more, as your website’s traffic grows, it’s easy to upgrade the amount of storage and bandwidth within your Droplet. And if you can figure out the rhyme or reason for traffic surges later on, you can quickly scale your resources up and down to accommodate the changes in traffic.</p>

<p>That said, a scalable cloud hosting solution isn’t enough to deal with traffic surges. There are a couple more things you’ll need.</p> 

#### Use Load Balancers for Surges

<p>If you’re unfamiliar with <a href="https://www.digitalocean.com/community/tutorials/what-is-load-balancing">load balancing</a> technology, let’s take a look at the difference between a website with and without it.</p>

<p>This is what happens when someone visits your website without a load balancer:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2ea64c0-deed-49c8-b82f-f2d15f6c5e6a/8-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2ea64c0-deed-49c8-b82f-f2d15f6c5e6a/8-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="A graphic from DigitalOcean on how visitors access a website without load balancing. (Source: <a href='https://www.digitalocean.com/'>DigitalOcean</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2ea64c0-deed-49c8-b82f-f2d15f6c5e6a/8-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="DigitalOcean - No Load Balancing graphic" >}}

<p>They log onto the Internet, enter your URL in their web browser or click on a link to it and then your server is supposed to deliver your website to their screen.</p>

<p>But if the amount of traffic requesting access to your site suddenly surges, this lone server may not be able to efficiently handle the load. This is why excessively high traffic surges can lead to painfully slow websites or no access to websites altogether.</p>

<p>With a load balancer, however, this is what happens to your web traffic:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e686e38-5d09-45be-93c6-135b1c384a90/5-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e686e38-5d09-45be-93c6-135b1c384a90/5-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="A graphic from DigitalOcean on how visitors access a website when load balancing is implemented. (Source: <a href='https://www.digitalocean.com/'>DigitalOcean</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e686e38-5d09-45be-93c6-135b1c384a90/5-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="DigitalOcean - Load Balancing graphic" >}}

<p>A load balancer serves as a sort of proxy for your server. This way, when traffic peaks, your server doesn’t have to struggle to handle the demand. Instead, the load balancer leverages multiple servers to balance out the growing volume of HTTP requests.</p>

<p>It’s kind of like distributing your workload amongst your team. Rather than continue to pile on the requests for team members who are already overloaded, you share the work with those who have the capacity for it.</p>

<p>Unlike real-world work distribution, however, load balancers do all of this behind the scenes and don’t need you to coordinate anything as it’s fully managed.</p>

#### Take Advantage of Performance Monitoring and Backups

<p>So long as you have the right amount of bandwidth and storage configured in your droplet, and load balancing activated, your website will be in good shape. It won’t be impervious to traffic surges, but it’ll be as close to it as you can get.</p>

<p>Just keep in mind that for all of the fortifying you do at the server level, it’s still important to have a contingency plan in place.</p>

<p>Your business (website) continuity plan should include all of the things you need to do to get your website back to normal, including how to:</p>

<ul>
  <li>Restore the website,</li>
  <li>Investigate the event that led to it,</li>
<li>And reach out to visitors and customers who were impacted.</lI>
</ul>

<p>That said, there are some parts of your continuity plan that DigitalOcean can help with.</p>

<p>Automated backups are essential for any website, but they’re absolutely critical if you know that your website will be susceptible to traffic surges. 24/7 support is another must and is something DigitalOcean offers as well.</p>

<p>Another thing to look for is built-in performance monitoring &mdash; something I’m going to touch on further down in this post.</p>

### 2. Optimize Your Assets

<p>With a solid cloud hosting solution in place, you can certainly give your website the help it needs to survive a huge traffic surge. However, it can’t all fall on your host. You need to do your part to make your website “light” enough to serve over and over again to the onslaught of visitors.</p>

<p>Here are some things you can do to optimize your website and its assets for greater performance:</p>

#### Enable Caching and Other File Optimizations

<p>Want your digital assets to be easier to handle? Then, you’ll need the following optimizations configured:</p>

<p><strong>Caching</strong></p>

<p>There are a variety of ways to implement caching and speed up how quickly your website gets delivered to visitors’ browsers. You can do this at the server, page, browser database levels.</p>

<p>Your web host can help you configure server caching.</p>

<p>If you’ve built your website with a content management system like WordPress, you can install a caching plugin to take care of the website and database baching for you. (It’ll also do things like file minification, Gzip compression combine CSS and JavaScript files.)</p>

<p>You can always enable caching manually. You’ll <a href="https://developers.google.com/web/fundamentals/performance/get-started/httpcaching-6">use your cache headers</a> and two mechanisms in particular &mdash; Cache-control and Expires &mdash; to configure how your content is cached.</p>

<p><strong>Image Optimization</strong></p>

<p>Don’t forget about your media. Image and video files can take up a lot of room on your server as well as impede how quickly your server works during a traffic surge. To optimize these assets, you should use file compression and resizing.</p>

<p>To compress images in bulk, I’ll use an online tool like <a href="https://tinypng.com/">TinyPNG</a> or TinyJPG to handle it for me.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5f4a933-1090-4019-90eb-2a6f488dc2dd/10-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5f4a933-1090-4019-90eb-2a6f488dc2dd/10-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="TinyPNG offers a quick and easy way to bulk-compress image assets. (Source: <a href='https://tinypng.com/'>TinyPNG</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5f4a933-1090-4019-90eb-2a6f488dc2dd/10-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="TinyPNG image compression" >}}

<p>On average, I can usually cut my file sizes by about 75% with this one tool.</p>

<p>To further shrink the heft of your images, you should be resizing them. There’s no reason to upload full-sized assets to a website if the maximum width you’re going to use is 1280 pixels or thereabouts.</p>

<p>For this, I’ll either use my file software to do it all in one go or I’ll use an online service like <a href="https://www.bulkresizephotos.com/en">Bulk Resize Photos</a>.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e1de0a5-657a-47e0-9292-bc6f9f19ef33/4-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e1de0a5-657a-47e0-9292-bc6f9f19ef33/4-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="Bulk Resize Photos offers an easy way to bulk-resize image assets using a variety of resizing methods. (Source: <a href='https://www.bulkresizephotos.com/en'>Bulk Resize Photos</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e1de0a5-657a-47e0-9292-bc6f9f19ef33/4-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="Bulk Resize Photos image resizing tool" >}}

<p>There’s a lot of flexibility here in how images are resized, but I find that setting a max width usually works best.</p>

#### Use Managed Databases

<p>In addition to optimizing the assets you put into a website, you should take some care to optimize your databases. That said, it’s often easier said than done.</p>

<p>While I’m familiar with database cleanup and optimization plugins you can use with WordPress to keep things running more smoothly, that’s not going to help much when it comes to a traffic surge. You need something that will help your database continue to process incoming data requests even at a higher rate.</p>

<p>For that, you’d be best off with <a href="https://www.digitalocean.com/community/tutorials/understanding-managed-databases">a managed database solution</a> &mdash; something you can provision from DigitalOcean.</p>

<p>When a traffic surge is detected, managed database services simplify what needs to be done in order to scale your resources accordingly. There are no calculations needed; simply log into your account and add more resources as needed.</p>

<p>Another reason why managed services are ideal in these kinds of situations is because of their built-in high availability. And this isn’t just some blanket promise of 99.9% uptime. If you take a look at your host’s SLA, you’ll find that it will go to great lengths to prevent egregious amounts of downtime.</p>

#### Add a CDN

<p>There’s another layer of optimization to add to your site when traffic surges are a common occurrence: a CDN.</p>

<p>Content delivery networks are useful for a whole host of reasons. They’re great for serving websites to global visitors. They’re definitely handy for e-commerce websites that want to provide a faster checkout experience. And they provide additional speed, security, and failover for websites that occasionally encounter high upticks in traffic.</p>

<p>If you’re planning on using DigitalOcean to host your website, look to its <a href="https://www.digitalocean.com/products/spaces/">Spaces</a> product (with built-in CDN integration) for more efficient storage and delivery of your assets.</p>

### 3. Analyze Your Traffic Reports

<p>In general, it’s really important to be diligent about collecting data from your website. That’s especially so when battling traffic surges. Here’s why:</p>

<p>If there are predictable highs and lows in your website traffic, you’ll know when and how exactly to plan for them. This not only means optimizing your website and server to handle the traffic but having the right amount of staff on to monitor and manage it.</p>

<p>To do this, use <a href="https://analytics.google.com/">Google Analytics</a> to keep tabs on everything.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37e90724-a40e-44ef-8506-9676c8271011/2-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37e90724-a40e-44ef-8506-9676c8271011/2-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="A sample traffic and pageviews chart from Google Analytics. (Source: <a href='https://analytics.google.com/'>Google Analytics</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37e90724-a40e-44ef-8506-9676c8271011/2-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="Google Analytics - charting out pageviews" >}}

<p>This example is a 12-month data pull that shows how many page views occurred every day (more or less). You can do this with other metrics like the number of users or sessions as well. The main goal, however, is to identify any sources of stress throughout the year, and excessive pageviews (or e-commerce conversions, if relevant) may be a more effective way to measure this.</p>

<p>You can see here that there were a number of high-highs and low-lows that took place:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2801ee0-81de-48f0-a4c2-eb4764dcfdaf/11-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2801ee0-81de-48f0-a4c2-eb4764dcfdaf/11-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="An example of how Google Analytics users would look for traffic surges in their data. (Source: <a href='https://analytics.google.com/'>Google Analytics</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2801ee0-81de-48f0-a4c2-eb4764dcfdaf/11-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="Google Analytics - traffic surge searching" >}}

<p>Rather than take them at face value, cross-reference them against other data points to ensure that what you’re looking at was a traffic surge you can learn from.</p>

#### Rule Out Web Development

<p>For example, was there any on-site development going on on those days? If someone were repairing a bug or designing a new page, that could cause the pageview numbers to increase greatly.</p>

<p>If this happens a lot, it would be a good idea to automatically strip this data out of your reports at the Google Analytics level. You can do this from the Admin menu.</p>

<p>Go to View > Filters > Add Filter:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b9b70cd-ad87-48ee-bbef-a242eabde3b1/7-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b9b70cd-ad87-48ee-bbef-a242eabde3b1/7-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="Google Analytics users can remove their personal visit and pageview metrics from results. (Source: <a href='https://analytics.google.com/'>Google Analytics</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b9b70cd-ad87-48ee-bbef-a242eabde3b1/7-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="Google Analytics filters" >}}

<p>By filtering out data for your IP address as well as anyone else who may preview the site frequently for testing or content creation purposes, you’ll give yourself a more accurate view of your traffic levels.</p>

<p>Let’s say that the spikes in traffic weren’t from your internal team. Next, you’ll want to see if these traffic surges (or drops) occur at predictable intervals.</p>

#### Look for Predictable Surges

<p>If your website has been live for more than a year, you can use Google Analytics to see if there’s a correlation. Simply set your dates to compare against the same timeframe from the previous year:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee1b1f63-6f9b-4d35-a2bc-1ce82aa06b2d/9-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee1b1f63-6f9b-4d35-a2bc-1ce82aa06b2d/9-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="Google Analytics allows users to compare two date ranges side-by-side. (Source: <a href='https://analytics.google.com/'>Google Analytics</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee1b1f63-6f9b-4d35-a2bc-1ce82aa06b2d/9-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="Google Analytics date range comparison" >}}

<p>Then, look for overlaps in traffic surges:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fd086a0-cbeb-4275-bf05-e2bb61c569b2/3-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fd086a0-cbeb-4275-bf05-e2bb61c569b2/3-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="Google Analytics users can simultaneously review two date ranges for traffic surge predictability. (Source: <a href='https://analytics.google.com/'>Google Analytics</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fd086a0-cbeb-4275-bf05-e2bb61c569b2/3-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="Google Analytics date range comparison data" >}}

<p>In this case, there’s maybe only one or two notable spikes that occurred in both years. The first was in early April and the other was around mid-November.</p>

<p>If these were excessively large surges in both years &mdash; like at least five times more than the usual amount of traffic &mdash; I’d say they’d be worth investigating. In this example, however, it’s probably just a coincidence and they can be ruled out.</p>

#### Check the Calendar

<p>If you have identified a notable traffic surge in your data, the last thing to do is check it against your calendar.</p>

<p>What you’re looking for are events that could have caused the surge. Things like:</p>

<ul>
<li>Holiday sales that generated a bunch of buzz.</li>
<li>Press releases that got picked up on major news wires.</li>
<li>Viral blog posts or email offers you sent out.</li>
</ul>

<p>I’d also suggest looking at the traffic during the days or weeks following the traffic surge.</p>

<p>How did it taper off? Was it suddenly or a slow burn? Was the website able to improve its daily traffic numbers &mdash; even slightly &mdash; thanks to the surge?</p>

<p>Also, look at how the organization was impacted. This is especially important for e-commerce websites that provide customer support and product returns. Was there an uptick in post-sale activity after the surge? When did it hit? How long did it last for?</p>

<p>If you can figure out why the traffic surge happened (i.e. what event triggered it) and what the fallout was, you can actually use this to your advantage in the future. For example, if you know that a sale or viral post caused the surge, you can plan your server and staffing resources ahead of the next one.</p>

<p>Regardless of what you find looking at old reports, this needs to become part of your ongoing process. Set up Google Analytics to generate traffic reports and email them to you on a regular basis. This way, as traffic levels change &mdash; for good or bad &mdash; you’ll always be in the know with what’s going on and can adapt your strategy accordingly.</p>

### 4. Real-time Performance Monitoring

<p>Google Analytics will help you figure out what happened in the past and prepare more effectively for future traffic surges. Real-time performance monitoring, on the other hand, will allow you to react to traffic surges and other performance changes in the heat of the moment.</p>

<p>There are various tools you can use for real-time monitoring. Here’s just a sample of them:</p> 

#### Frontend Performance Monitoring

<p>When page speed suddenly begins to deteriorate or your website goes down, there’s no time to waste. That said, it shouldn’t be up to you to regularly log into your website to make sure everything’s running fine.</p>

<p>Instead, you can use an uptime and speed monitoring service like <a href="https://www.pingdom.com/">Pingdom</a>:</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733bb170-5183-4e8b-b4d5-9eb14bdf46ac/6-struggling-to-get-handle-on-traffic-surges.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733bb170-5183-4e8b-b4d5-9eb14bdf46ac/6-struggling-to-get-handle-on-traffic-surges.png" sizes="100vw" caption="Users can automate uptime, user and speed monitoring with Pingdom. (Source: <a href='https://www.pingdom.com/'>Pingdom</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/733bb170-5183-4e8b-b4d5-9eb14bdf46ac/6-struggling-to-get-handle-on-traffic-surges.png'>Large preview</a>)" alt="Pingdom monitoring and alerting services" >}}

<p>It handles the tedious job of monitoring your website for upticks in traffic,  problems with speed or uptime as well as issues detected at checkout. It will also serve you real-time notices so you can take care of issues caused by traffic surges before they get too bad.</p>

<p>This way, you’ll only need to give your website the attention and care it needs when a traffic surge has a negative impact on performance instead of constantly worrying about it.</p>

#### Backend Performance Monitoring

<p>While it’s great to have a frontend monitoring service to tell you when traffic’s out of whack, it’s not enough. You need to know what’s going on on the backend as well.</p>

<p>Of course, with a managed hosting solution, you’ll get some help from your provider. However, it’s a good idea to familiarize yourself with your server metrics so you can be proactive about fighting off the devastating effects of surges.</p>

<p>Here are some of the metrics to keep an eye on:</p>

<ul>
  <li>Hosting resources (like memory and disk space),</li>
  <li>Your application performance (like error rates and resource usage),</li>
  <li>Connectivity (like latency and bandwidth utilization).</li>
</ul>

<p>Become acquainted with these key metrics so you’re never scrambling to figure out what’s going on with your website or how to fix it.</p>

<p>Now, with DigitalOcean, you won’t just get access to these handy metrics. It will set you up with <a href="https://www.digitalocean.com/community/tutorials/an-introduction-to-metrics-monitoring-and-alerting">real-time monitoring and alerts</a>, too. And that’s not all.</p>

<p>The problem with many monitoring systems is that they’re just that: they look for outages, errors, and instability, but it’s still up to you to take action. With DigitalOcean, though, you can automate certain actions to take place when specific scenarios are detected.</p> 

<p>For example, let’s say your website is receiving a much larger rush of traffic than you had anticipated for the holiday sale. Your resources are depleting too fast, which would normally put a website in risk of slowing to a crawl or crashing altogether. But in this case, the monitoring mechanism has noted the issue and your auto-scaling action has been triggered.</p>

<p>Imagine how useful it would be to automate your server’s response to certain events. You could spend less time worrying about how to restore your website and instead focus on how to keep optimizing your server assets to sustain the high levels of traffic.</p>

## Wrapping Up

<p>If your clients’ websites or PWAs aren’t ready for a traffic surge, it could spell major trouble for their businesses once the dust settles. And it’s not just downtime or slow-loading pages that will cost them (or you).</p>

<p>Having all of those extra visitors see a website that’s in ill shape &mdash; from broken checkouts or forms to malware infections &mdash; will hurt your business, too.</p>

<p>Rather than cross your fingers or tell yourself that your website isn’t big enough or popular enough to experience one of those traffic surges, be prepared. By starting with a practical cloud hosting solution from DigitalOcean and then optimizing your server, assets and processes surrounding them, you’ll improve your website’s chances of not only surviving a surge intact but greatly profiting from it.</p> 

{{< signature "ra, yk, il" >}}

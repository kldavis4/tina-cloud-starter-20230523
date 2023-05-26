---
title: 5 Simple Steps To Test Your Varnish Cache Deployment Using Varnishtest
slug: five-simple-steps-test-varnish-cache-deployment-varnishtest
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d14a0f87-f8b5-4450-b78c-549337c1c80f/varnish-caching-varnishtest-preview-opt.png
date: 2016-05-18T18:41:53.000Z
author: ariannaaondio
description: >-
  Varnish Cache is an open source HTTP accelerator that is used for speeding up
  the content delivery of the world’s top content-heavy dynamic websites.
  However, the performance or speed a newcomer to Varnish Cache can expect from
  its deployment can be quite nebulous.

  This is true for users at both extremes of the spectrum: from those who play
  with its source code to create more complex features to those who set up
  Varnish Cache using the default settings.
categories:
  - Coding
  - Performance
  - Caching
  - Varnish
  - Sponsored Content
---
Varnish Cache is an open-source HTTP accelerator that is used to speed up content delivery on some of the world’s top content-heavy dynamic websites. However, the performance or speed that a newcomer to Varnish Cache can expect from its deployment can be quite nebulous.

This is true for users at both extremes of the spectrum: from those who play with its source code to create more complex features, to those who set up Varnish Cache using the default settings.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d14a0f87-f8b5-4450-b78c-549337c1c80f/varnish-caching-varnishtest-preview-opt.png" title="5 Simple Steps To Your Varnish Test Cache Deployment Using Varnishtest" alt="varnish test" width="500" height="318" /><br>
<figcaption>Caching isn't always as simple as we think. A few gotchas and problems could take quite some time to master. (Image: <a href="https://twitter.com/varnishcache">Varnish Cache</a>)</figcaption></figure>

Imagine you have deployed Varnish Cache according to the default settings to deliver web and application content quickly, reliably and at scale. Suddenly, it stops behaving as it should. Either it’s not caching or, worse, because of bad caching or incorrect cookie policies, cached personal content is delivered to the wrong client.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2015/02/using-edge-side-includes-in-varnish/#further-reading-on-smashingmag)

*   [Speed Up Your Mobile Website With Varnish](https://www.smashingmagazine.com/2013/12/speed-up-your-mobile-website-with-varnish/)
*   [HTTPS Everywhere With Nginx, Varnish And Apache](https://www.smashingmagazine.com/2015/09/https-everywhere-with-nginx-varnish-apache/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)
*   [Secrets Of High-Traffic WordPress Blogs](https://www.smashingmagazine.com/2012/09/secrets-high-traffic-wordpress-blogs/)

{{% feature-panel %}}

In another scenario, TTL (time to live) limits might have been set incorrectly. Set the TTL limit too short and you’ll get too many unwanted back-end fetches, which will slow down the website. Set it too long and objects will stay in cache until the TTL expires, using far more storage than necessary.

Getting the best performance from Varnish Cache is about using it not only for caching, but also for invalidation. A previous article here on Smashing Magazine explains the different ways to do <a href="https://www.smashingmagazine.com/2014/04/cache-invalidation-strategies-with-varnish-cache/">cache invalidation</a> with Varnish Cache. Not every method works well for every website. You might find that a piece of content you’ve removed from your website is still delivered to mobile users.

We can easily avoid all of these mistakes by running tests. A little-known fact about Varnish Cache is that it comes with its own testing tool, called Varnishtest. Varnishtest is a script-driven program that can be used to create client mockups, to simulate transactions, to fetch content from mockups or real back ends, to interact with the actual Varnish Cache configuration, and to assert expected behaviors.

To ensure optimal performance from a Varnish Cache deployment, one should integrate Varnishtest into the design. Varnishtest can be used by system administrators in two scenarios: (1) when configuring a Varnish Cache installation, and (2) when writing complex caching policies in the Varnish Configuration Language (VCL) or when tuning Varnish Cache.

Code tinkerers who work on extensions written for Varnish Cache (called VMODs) can use Varnishtest to define and test their modules. The same goes for web developers who write applications that take full advantage of Varnish Cache. As mentioned, Varnishtest can be used to test a cache invalidation method or to reproduce bugs when filing a bug report.</p>

## The Varnish Test Case Language

Note that Varnishtest does not follow the unit-testing framework (<code>setUp</code>, <code>test</code>, <code>assert</code>, <code>tearDown</code>), nor does it follow behavior-driven development (“given,” “when,” “then”). Varnishtest has its own language: Varnish Test Case (VTC).

VTC files follow a naming convention. Files starting with <code>b</code> (for example, <code>b00001.vtc</code>) contain basic functionality tests. (The <a href="https://raw.githubusercontent.com/varnish/Varnish-Cache/master/bin/varnishtest/tests/README">full naming scheme for test scripts</a> is available on GitHub.)

<pre><code class="language-bash">
varnishtest "Varnish as Proxy" 

server s1 {
  rxreq
  txresp
} -start

varnish v1 -arg "-b ${s1_addr}:${s1_port}" -start

client c1 {
 txreq
 rxresp

 expect resp.http.via ~ "varnish"
} -run
</code></pre>

## 1\. Name The Test

All VTC programs start by naming the test:

<pre><code class="language-bash">
varnishtest "Varnish as Proxy"
</code></pre>

You need to define three components to run a Varnishtest: a server, a Varnish Cache instance and a client.</p>

## 2\. Declare The Origin Server

<pre><code class="language-bash">
server s1 {
  rxreq
  txresp
} -start
</code></pre>

All server declarations must start with <code>s</code>. In the code above, <code>server s1</code> receives a request (<code>rxreq</code>) and transmits a response (<code>txresp</code>). The commands <code>rxreq</code> and <code>txresp</code> describe the behavior of the server; <code>rxreq</code> means the server will accept an incoming request, and <code>txresp</code> means the request will be responded to.

The command <code>-start</code> boots server s1 and makes available the macros <code>${s1_addr}</code> and <code>${s1_port}</code>, with the IP address and port of the simulated back end.</p>

## 3\. Declare The Varnish Cache Instance

<pre><code class="language-bash">
varnish v1 -arg "-b ${s1_addr}:${s1_port}" -start
</code></pre>

Here, <code>varnish v1</code> declares an instance of our real Varnish server, (i.e. <code>varnishd</code>). The names of Varnish servers must start with <code>v</code>. This instance is controlled by the manager process, and <code>-start</code> forks a child, which is the actual cacher process.

There are many ways to configure <code>varnishd</code>. One way is to pass arguments with <code>-arg</code>, as in <code>-arg -b ${s1_addr}:${s1_port}</code>. Here, <code>-b</code> is a <code>varnishd</code> option to define the back end. In this case, the IP address and port of the simulated back end s1 are used. However, using a real back end is also possible, thus making it possible to use Varnishtest as an integration tool when testing the real back end.</p>

## 4\. Simulate The Client

<pre><code class="language-bash">
client c1 {
  txreq
  rxresp

  expect resp.http.via ~ "varnish"
} -run
</code></pre>

Simulated clients in Varnishtest start with <code>c</code>. In this example, <code>c1</code> transmits one request and receives one response. Because Varnish is a proxy, the response should be received from the back end via Varnish Cache. Therefore, <code>c1</code> expects <code>varnish</code> in the <code>via</code> HTTP header field. The tilde (<code>~</code>) is used as a match operator of regular expressions, because the exact text in <code>resp.http.via</code> depends on the Varnish version installed. Finally, the client <code>c1</code> is started with the <code>-run</code> command. (Note that Varnish servers are typically started with the <code>-start</code> command, and clients with the <code>-run</code> command.)

## 5\. Run The Test

<pre><code class="language-bash">
$varnishtest b00001.vtc
#  top TEST b00001.vtc passed (1.458)
</code></pre>

To run the test, simply issue the command above. By default, Varnishtest outputs a summary of passed tests, and a verbose output for failed tests only. A passed test means that a most basic Varnish Cache configuration is correct.</p>

### Easy Tests for Top Performance

The performance problems mentioned at the beginning of this article could have been prevented if we had used Varnishtest before going live. Here are two simple test examples I wrote to help you test your cache invalidation method and cookie policies:

*   [Test cache invalidation method](https://github.com/aondio/varnish-testcases/blob/master/purge.vtc) Ensure your TTL limits are set correctly. This test checks that you are able to purge objects from the cache, thus ensuring that not too much memory is used.
*   [Test cookies configuration](https://github.com/aondio/varnish-testcases/blob/master/cache_with_cookie.vtc) Because cookies are used to identify unique users and may contain personal information, by default Varnish does not cache a page if it contains a `Cookie` or `Set-Cookie` header. This case represents a scenario for testing cache objects with a cookie header to ensure that each of three defined clients gets the correct object.

However, there are many <a href="https://github.com/varnishcache/varnish-cache/tree/master/bin/varnishtest/tests">more documented test examples</a> for different scenarios.

The best way to learn how to create tests is by running the examples linked to above in Varnish Cache, and then write your own tests based on these.

Ultimately, these tests will help you understand in advance what will happen if Varnish Cache is put into production, ensuring optimal performance of your web architecture and helping you avoid the pitfalls described at the beginning of this article.

Web performance is business-critical across industries, and you can easily take the guesswork out of performance by baking Varnishtest into your design and following these five easy steps to incorporate testing into the configuration of your Varnish instances.

{{< signature "rb, ms, al, il" >}}


---
title: 'Analyzing Network Characteristics Using JavaScript And The DOM, Part 2'
slug: analyzing-network-characteristics-using-javascript-and-the-dom-part-2
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6addfe8e-759e-4ce6-a062-416caf61ad57/illu-dom.jpg'
date: 2013-08-27T08:34:02.000Z
author: philip-tellis
description: >-
  In [Part
  1](https://www.smashingmagazine.com/2011/11/14/analyzing-network-characteristics-using-javascript-and-the-dom-part-1/)
  of this series, we had a look at how the underlying protocols of the Web work,
  and how we can use JavaScript to estimate their performance characteristics.
  In this second part, we’ll look at DNS, IPv6 and the new W3C specification for
  the NavigationTiming API.
categories:
  - Coding
  - JavaScript
  - Performance
---
In <a href="https://www.smashingmagazine.com/2011/11/14/analyzing-network-characteristics-using-javascript-and-the-dom-part-1/">Part 1</a> of this series, we had a look at how the underlying protocols of the Web work, and how we can use JavaScript to estimate their performance characteristics. In this second part, we'll look at DNS, IPv6 and the new W3C specification for the <a href="https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming/Overview.html">NavigationTiming</a> API.</p>

## DNS Explained

Every device attached to the Internet is identified by a numeric address known as an IP address. The two forms of IP addresses seen on the open Internet are IPv4, which is a 32-bit number often represented as a series of four decimal numbers separated by dots, e.g. <code>80.72.139.101</code>, and IPv6 which is a 128-bit number represented as a series of multiple hexadecimal numbers separated by colons, e.g. <code>2607:f298:1:103::c8c:a407</code>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Website Performance: What To Know and What You Can Do](https://www.smashingmagazine.com/2010/01/page-performance-what-to-know-and-what-you-can-do/)
*   [Data-Driven Design In The Real World](https://www.smashingmagazine.com/2013/09/data-driven-design-in-the-real-world/)
*   [A Roadmap To Becoming An A/B Testing Expert](https://www.smashingmagazine.com/2014/07/roadmap-to-becoming-an-a-b-testing-expert/)
*   [Multivariate Testing 101: A Scientific Method Of Optimizing Design](https://www.smashingmagazine.com/2011/04/multivariate-testing-101-a-scientific-method-of-optimizing-design/)

{{% feature-panel %}}

These addresses are good for computers to understand; they take up a fixed number of bytes and can easily be processed, but they're hard for humans to remember. They're also not very good for branding, and are often tied to a geographic location or an infrastructure service provider (like an ISP or a hosting provider).

To get around these shortcomings, the "<strong>Domain Name System</strong>" was invented. At its simplest form, DNS creates a mapping between a human readable name, like "<code>www.smashingmagazine.com</code>" and its machine readable address (<code>80.72.139.101</code>). DNS can hold much more information, but this is all that's important for this article.

For now, we'll focus on DNS latency, and how we can measure it using JavaScript from the browser. DNS latency is important because the <strong>browser needs to do a DNS lookup for every unique hostname</strong> that it needs to download resources from — even if multiple hostnames map to the same IP address.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d99289eb-0f3d-409b-9791-944eb2ad46e7/smashing-dns-waterfall-large-mini.png"><img title="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6703075e-25a2-4ffb-a8a8-21ba3c471198/smashing-dns-waterfall-mini.png" alt="" width="500" height="143" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d99289eb-0f3d-409b-9791-944eb2ad46e7/smashing-dns-waterfall-large-mini.png">Larger view</a></em>

## Measuring DNS Lookup Times

The simple way to measure DNS lookup time from JavaScript would be to first measure the latency to a host using its IP address, and then measure it again using its hostname. The difference between the two should give us DNS lookup time. We use the methods developed in <a href="https://www.smashingmagazine.com/2011/11/14/analyzing-network-characteristics-using-javascript-and-the-dom-part-1/">Part 1</a> to measure latency.

The problem with this approach is that if the browser has already done a DNS lookup on this hostname, then that lookup will be cached, and we won't really get a difference. What we need, is a <a href="https://en.wikipedia.org/wiki/Wildcard_DNS_record">wildcard DNS record</a>, and a Web server listening on it. Carlos Bueno did a great write-up about this on the YDN blog a few years ago, and built the code that boomerang uses.

Before we look at the code, <strong>let's take a quick look at how DNS lookups work</strong> with the following (simplified) diagram:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f381c120-c2a5-43e8-9d2c-a63ef388f27e/dns-lookup-mini.png"><img title="DNS Lookup path from Client to Authoritative Server" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f381c120-c2a5-43e8-9d2c-a63ef388f27e/dns-lookup-mini.png" alt="DNS Lookup path from Client to Authoritative Server" width="411" height="300" /></a><br>
<em>From left to right: The client here is the browser, the DNS server is (typically) the user's ISP, the Root name server knows where to look for most domains (or who to ask if it doesn't know about them), and finally the authoritative server which is the DNS server of the website owner.</em>

Each of these layers has their own cache, and that cache generally sticks around for as long as the authoritative server's TTL (known as "Time To Live") says it should; but not all servers follow the spec (and that's a complete topic for itself).

Now, let's look at the code:

<pre><code class="language-javascript">var dns_time;

function start() {
    var gen_url, img,
        t_start, t_dns, t_http,
        random = Math.floor(Math.random()*(2147483647)).toString(36);

    // 1. Create a random hostname within our domain
    gen_url = "https://*.foo.com".replace(/*/, random);

    var A_loaded = function() {
        t_dns = new Date().getTime() - t_start;

        // 3. Load another image from the same host (see step 2 below)
        img = new Image();
        img.onload = B_loaded;

        t_start = new Date().getTime();
        img.src = gen_url + "image-l.gif?t=" + (new Date().getTime()) + Math.random();
    };

    var B_loaded = function() {
        t_http = new Date().getTime() - t_start;

        img = null;

        // 4. DNS time is the time to load the image with uncached DNS
        //    minus the time to load the image with cached DNS

        dns_time = t_dns - t_http;
    };

    // 2. Load an image from the random hostname
    img = new Image();
    img.onload = A_loaded;

    t_start = new Date().getTime();
    img.src = gen_url + "image-l.gif?t=" + (new Date().getTime()) + Math.random();

}</code></pre>

Let's step through the code quickly. <strong>What we've done here is the following:</strong>

1.  Create a random hostname prefixed to our wildcard domain. This makes sure that the hostname lookup isn't cached by anyone.
2.  Load an image from this host and measure the time it takes for it to load.
3.  Load another image from the same host and measure the time it takes to load.
4.  Calculate the difference between the two measured times.

The first measured time period includes DNS lookup time, TCP handshake time and network latency. The second time measured includes network latency.

There are two downsides to this approach though. First, it measures the worst case DNS lookup time, i.e. the time it takes to do a DNS lookup if your hostname isn't cached by any intermediate DNS server. In practice, this isn't always the case. There isn't an easy way to get around that without the help of browsers, and we'll get to that later at the end of this article.

Also, what probably makes it hard for most people to implement is setting up a wildcard DNS record. This isn't always possible if you don't control your DNS servers. Many [shared hosting](https://inmotion-hosting.evyy.net/c/1233229/260033/4222) providers won't let you set up a wildcard DNS record. The only thing you can do in this case is to move hosting providers, or at least DNS providers.

## Measuring IPv6 Support And Latency

Technically, measuring IPv6 shouldn't really be a separate topic, however, even a decade after its introduction, IPv6 adoption is still fairly low. ISPs have been holding back because not too many websites offer IPv6 support, and website owners have been holding back because not too many of their users have IPv6 support, and they're not sure how it will impact performance or user experience.

The IPv6 test in boomerang helps you determine if your users have IPv6 support and how their IPv6 latency compares to IPv4 latency. It doesn't check to see if their IPv6 support is broken or not (but see <a href="https://ipv6test.google.com/">Google's IPv6 test page</a> if you'd like to know that).

<strong>There are two parts to the IPv6 test:</strong>

1.  First, we check to see if we can connect to a host using its IPv6 address, and if we can, we measure how long it takes.
2.  Next, we try to connect to a hostname that only resolves to an IPv6 address.

The first test tells us if the user's network can make IPv6 connections. The second tells us if their DNS server can lookup AAAA records. We need to run the test in this order because we'd be unable to correctly test DNS if connections at the IP level fail.

The code is very similar to the DNS test, except we don't need a wildcard DNS record:

<pre><code class="language-javascript">var ipv6_url = "https://[2600:1234::d155]/image-l.gif",
    host_url = "https://ipv6.foo.com/image-l.gif",
    timeout: 1200,

    ipv6_latency='NA', dnsv6_latency='NA',

    timers: {
        ipv6: { start: null, end: null },
        host: { start: null, end: null }
    };

var img,
    rnd = "?t=" + (new Date().getTime()) + Math.random(),
    timer=0, error = null;

img = new Image();

function HOST_loaded() {
    // 4. When image loads, record its time
    timers['host'].end = new Date().getTime();
    clearTimeout(timer);
    img.onload = img.onerror = null;
    img = null;

    // 5. Calculate latency
    done();
}

function error(which) {
    // 6. If any image fails to load or times out, terminate the test immediately
    timers[which].supported = false;
    clearTimeout(timer);
    img.onload = img.onerror = null;
    img = null;

    done();
}

function done() {
    if(timers['ipv6'].end !== null) {
        ipv6_latency = timers.ipv6.end - timers.ipv6.start;
    }
    if(timers['host'].end !== null) {
        dnsv6_latency = timers.host.end - timers.host.start;
    }
}

img.onload = function() {
    // 2. When image loads, record its time
    timers['ipv6'].end = new Date().getTime();
    clearTimeout(timer);

    // 3. Then load image with hostname that only resolves to ipv6 address
    img = new Image();
    img.onload = HOST_loaded;
    img.onerror = function() { error('host') };

    timer = setTimeout(function() { error('host') }, timeout);

    timers['host].start = new Date().getTime();
    img.src = host_url + rnd;
};

img.onerror = function() { error('ipv6') };
timer = setTimeout(function() { error('ipv6') }, timeout);
this.timers['ipv6'].start = new Date().getTime();
// 1. Load image with ipv6 address
img.src = ipv6_url + rnd;</code></pre>

Yes, this code can be refactored to make it smaller, but that would make it harder to explain. This is what we do:

1.  We **first load an image from a host using its IPv6 address**. This checks to see that we can make a network connection to an IPv6 address. If your network, browser or OS don't support IPv6, this will fail and the onerror event fires.
2.  If the image loads up, we know that IPv6 connections are supported. We record the time that we'll use to measure latency later.
3.  Then we try to load up an image using a hostname that only resolves to an IPv6 address. It's important that this hostname does not resolve to an IPv4 address or this test might pass even if the DNS server cannot handle IPv6.
4.  If this succeeds, we know that our DNS server can look up and return AAAA (the IPv6 equivalent of A) records. We record the time.
5.  And then go ahead and calculate the latency. We can compare this with our IPv4 latency and DNS latency. This would also be an appropriate place to call any callback function to say that the test has completed.
6.  If any of the image loads fired an onerror event or if they timed out, we terminate the test immediately. In that case, any tests that haven't run have their corresponding variable (`ipv6_latency` or `dnsv6_latency`) set to "NA", indicating no support.

There are other ways to test IPv6 support with help from the server side, for example, have your server set a cookie stating whether it was loaded via IPv4 or IPv6. This only works well if your testing page and your image page are on the same domain.</p>

## The NavigationTiming API

The <a href="https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming/Overview.html">NavigationTiming API</a> is an interface provided by many modern browsers that gives JavaScript developers detailed information about the time the browser spent in the various states of downloading a page. The specification is still in a draft state, but as of the date of this article, Internet Explorer, Chrome and Firefox support it. Safari and Opera do not currently support the API.

JavaScript developers get access to the NavigationTiming object through <code>window.performance.timing</code>. Try this now. If you're using Chrome, IE 9+ or Firefox 8+, open a Web console and inspect the contents of <code>window.performance.timing</code>.

The diagram below explains the order of events whose time shows up in the object. Let's look at a few of them:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/533b09f5-7c54-4b5a-8b5c-8e2bc0d02bb2/timing-overview-large-mini.png"><img title="Navigation Timing Overview diagram from the W3C" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a01e7d2-67cd-4e22-b25b-43c94fc75421/timing-overview-mini.png" alt="Navigation Timing Overview diagram from the W3C" width="500" height="304" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/533b09f5-7c54-4b5a-8b5c-8e2bc0d02bb2/timing-overview-large-mini.png">Larger view</a> | <a href="https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming/Overview.html">Image source</a></em>

Now the items we've been interested in measuring are:

1.  **Page Load Time** We get the full page load time by taking the difference between `loadEventEnd` and `navigationStart`. The latter tells us when the user initiated the page load, either by clicking a link, or entering it into their browser's URL bar. The latter tells us when the `onload` event finished. If we're not interested in the execution time of the `onload` event, we could use `loadEventStart` instead.
2.  **Network/Application Latency** Network latency is the time from the browser initiating download to the time the first byte showed up. Now, part of this latency could be attributed to the application doing something before sending out bytes, but there's no way to know that from the client side. We use the difference between `requestStart` and `responseStart`.
3.  **TCP Connect Time** TCP connect time is the difference between `connectStart` and `connectEnd`, however, if the connection is over SSL, then this includes the time to negotiate an SSL handshake. You'd need to take that into account, and use `secureConnectionStart` instead of `connectEnd` if it exists, and if you care about the difference.
4.  **DNS Latency** DNS latency is the difference between `domainLookupStart` and `domainLookupEnd`.

<blockquote><strong>Important</strong>: We use a combination of times from <code>window.performance.timing</code> to determine each one of these.</blockquote>

While this looks good for the most part, and really tells you what your users experience, there are a <strong>few caveats to be aware of</strong>. If DNS is already cached, then DNS latency will be <code>0</code>. Similarly, if the browser uses a persistent TCP connection, then TCP connect time will be <code>0</code>. If the document is read out of cache, then network latency will be <code>0</code>. Keep these points in mind and use them to determine what fraction of your users makes effective use of available application caches.

The Navigation Timing interface provides us with many more timers, but several of them are restricted by the browser's same origin policy. These include details about redirects and unloading of the previous page. Other timers related to the DOM already have equivalent JavaScript events, namely the <code>readystatechange</code>, <code>DOMComplete</code> and <code>load</code> events.</p>

## The Network Information API

Another interesting network related API is the <a href="https://www.w3.org/TR/netinfo-api/">Network Information API</a>. While not strictly performance related, it does help make guesses at expected network performance. This API is currently only supported by Android devices, and is exposed via the <code>navigator.connection.type</code> object. In particular, it tells you whether the device is currently using Ethernet, Wi-Fi, 2G or 3G.

An article I highly recommend reading would be David Calhoun's piece that shows some good examples on <a href="https://davidbcalhoun.com/2010/using-navigator-connection-android">Optimizing Based On Connection Speed</a>. Both the article and the comments are useful reading.</p>

## Summary

While the Navigation Timing API provides easy access to accurate page timing information, it is still insufficient to draw a complete picture. There is still some benefit to estimating various performance characteristics using the techniques mentioned earlier in this series.

Whether we need to support browsers that do not currently implement the Navigation Timing or get information about resources not included in the current page, be sure to find out more about the user's network bandwidth or whether their support for IPv6 is better or worse than their support for IPv4 — a combination of methods gives us the best all-round picture.

All of the techniques presented here were developed while writing <a href="https://github.com/yahoo/boomerang">Boomerang</a> though not all of them made it into the code yet.</p>

### References

The following links helped in writing this article and may be referred to for more information on specific topics:

*   [The Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System): WikiPedia article explaining what DNS is and how it works.
*   [RFC 1035: DNS Specification](https://tools.ietf.org/html/rfc1035): One of the RFCs about DNS, this one details the specification and implementation.
*   [Wildcard DNS records](https://en.wikipedia.org/wiki/Wildcard_DNS_record): WikiPedia article explaining Wildcard DNS.
*   [IPv4](https://en.wikipedia.org/wiki/IPv4): WikiPedia article about revision 4 of the IP addressing protocol.
*   [IPv6](https://en.wikipedia.org/wiki/IPv6): WikiPedia article about revision 6 of the IP addressing protocol.
*   [Google's IPv6 test page](https://ipv6test.google.com/): Tells you if your browser, OS and network provider support IPv6 and whether that support works correctly or not.
*   [Hurricane Electric's IPv6 tunnels](https://tunnelbroker.net/): Create an IPv6 tunnel over your IPv4 network to give yourself IPv6 support (most useful for testing) before your ISP does.
*   [The NavTiming Specification](https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming/Overview.html): W3C draft specification for the browser NavTiming API.
*   [Network Information API](https://www.w3.org/TR/netinfo-api/): W3C draft specification for the Network Information API.
*   "[Using navigator.connection on Android](https://davidbcalhoun.com/2010/using-navigator-connection-android)" written by David Calhoun.

<em>(Credits of image on frontpage: <a href="https://www.flickr.com/photos/vlastula/300102949">Vlasta Juricek</a>)</em>

<em>(il) (ea)</em>


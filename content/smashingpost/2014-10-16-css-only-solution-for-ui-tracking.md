---
title: CSS-Only Solution For UI Tracking
slug: css-only-solution-for-ui-tracking
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f5b0544-dfa1-40b3-9ef5-51fc42f97a00/google-analytics-screenshot-500-opt.png
date: 2014-10-16T19:55:37.000Z
author: krasimirtsonev
description: >-
  The web is growing up. We are building applications that work entirely in the
  browser. They are responsive; they have tons of features and work under many
  devices. We enjoy providing high-quality code that is well structured and
  tested.

  But what matters in the end is the impact for clients. Are they getting more
  products sold or are there more visitors for their campaign sites? The final
  results usually show if our project is successful. And we rely on statistics
  as a measuring tool. We all use instruments like [Google
  Analytics](https://www.google.com/analytics/). It is a powerful way to collect
  data. In this article, we will see a CSS-only approach for tracking UI
  interactions using Google Analytics.
categories:
  - Coding
  - Tools
  - CSS
  - Techniques
  - Data Visualization
  - Analytics
---
The web is growing up. We are building applications that work entirely in the browser. They are responsive; they have tons of features and work under many devices. We enjoy providing high-quality code that is well structured and tested.

But what matters in the end is the impact for clients. Are they getting more products sold or are there more visitors for their campaign sites? The final results usually show if our project is successful. And we rely on statistics as a measuring tool. We all use instruments like <a href="https://www.google.com/analytics/">Google Analytics</a>. It is a powerful way to collect data. In this article, we will see a CSS-only approach for tracking UI interactions using Google Analytics.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Guide To Google Analytics And Useful Tools](https://www.smashingmagazine.com/2009/07/a-guide-to-google-analytics-and-useful-tools/)
*   [Finding Better Mobile Analytics](https://www.smashingmagazine.com/2016/10/finding-better-mobile-analytics/)
*   [Keep Your Analytics Data Safe And Clean](https://www.smashingmagazine.com/2012/04/keep-your-analytics-data-safe-and-clean/)
*   [Enabling Multiscreen Tracking With Google Analytics](https://www.smashingmagazine.com/2014/11/enabling-multiscreen-tracking-with-google-analytics/)
*   [How To Use Analytics To Build A Smarter Mobile Website](https://www.smashingmagazine.com/2014/03/how-to-use-analytics-to-build-a-smarter-mobile-website/)

## The Problem

We developed an application that had to work on various devices. We were not able to test on most of them and decided that we had to make everything simple. So simple that there wasn't a chance to produce buggy code. The design was clean, minimalistic, and there wasn't any complex business logic.

{{% feature-panel %}}

It was a website displaying information about one of the client's products. One of our tasks was to track user visits and interactions. For most cases, we used Google Analytics. All we had to do was to place code like the example below at the bottom of the pages:

<pre><code class="language-css">
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','//www.google-analytics.com/analytics.js','ga');

ga('create', '......', '......');
ga('send', 'pageview');
</code></pre>

This snippet was enough for tracking page views, traffic, sessions, etc. Moreover, we placed JavaScript where the user interacts with the page. For example, clicking on a link, filling an input field, or checking option boxes.</p>

<pre><code class="language-css">
ga('send', 'event', 'ui-interaction', 'click', 'link clicked', 1);
</code></pre>

The guys from Google handled these events nicely, and we were able to see them in our account. However, at some point the client reported that there were devices that have bad or no JavaScript support. They represented roughly 2% of all the devices that visited the site. We started searching for a solution that did not involve JavaScript. We were ready to admit that we could not collect statistics under these circumstances.

It was not that bad, but the client shared another issue. Our little application was going to be part of a private network. The computers there had JavaScript turned off for security reasons. Also, this private network was important for the client. So, he insisted that we still get stats in those cases. We had to provide a proper solution, but the problem was that we had only CSS and HTML available as tools.</p>

## The Solution

While searching for a solution, I was monitoring the <em>Network</em> tab in Chrome's developer tools when I noticed the following:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a826723a-dea4-4b59-936a-565ac1791f8e/1-google-analytics-large-preview-opt.png"><img title="Tracking UI with CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d3698bf-8877-4851-a012-f56ab24bd624/1-google-analytics-preview-opt.png" alt="Tracking UI with CSS" width="500" height="52" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a826723a-dea4-4b59-936a-565ac1791f8e/1-google-analytics-large-preview-opt.png">View large version</a>)</figcaption></figure>

In the beginning, I thought that there was nothing unusual. Google Analytics's code made few HTTP requests for its tracking processes. However, the fourth column shows the <code>Content-type</code> header of the response. It is an image. Not JSON or HTML, but an image. Then I started reading the documentation and landed on this <a href="https://developers.google.com/analytics/resources/concepts/gaConceptsTrackingOverview">Tracking Code Overview</a>. The most interesting part was:
<blockquote>When all this information is collected, it is sent to the Analytics servers in the form of a long list of parameters attached to a single-pixel GIF image request.</blockquote>

So, Google indeed made the HTTP request but not the trivial Ajax call. It simply appends all the parameters to an image's URL. After that it performs a request for a GIF file. There is even a name for such requests: <a href="https://www.phpied.com/beacon-performance/">beacon</a>. I wondered why GA uses this approach. Then I realized that there are some benefits:

*   It is simple. We initialize a new `Image` object and apply a value to its `src` attribute:

        new Image().src = '/stats.gif?' + parameters

*   It works everywhere. There is no need to add workarounds for different browsers as we do for Ajax requests.
*   Tiny response. As [Stoyan Stefanov said](https://www.phpied.com/beacon-performance/), the 1×1px GIF image could be only 42 bytes.

I made few clicks and sent events to Google Analytics. Knowing the request parameters, I was able to construct my own image URLs. The only thing to do in the end was to load an image on the page. And yes, this was possible with pure CSS.</p>

<pre><code class="language-css">
background-image: url('https://www.google-analytics.com/collect?v=1&amp;_v=j23&amp;a=...');
</code></pre>

Setting the <code>background-image</code> CSS property forces the browser to load an image. Finally, we successfully used this technique to track user actions.</p>

## Tracking User Actions

There are several ways to change styles based on user input. The first thing we thought about was the <code>:active</code> pseudo class. This class matches when an element is activated by the user. It is the time between the moment the user presses the mouse button and releases it. In our case, this was perfect for tracking clicks:

<pre><code class="language-css">
input[type="button"]:active {
    background-image: url('https://www.google-analytics.com/collect?v=1&amp;_v=j23&amp;a=...');
}
</code></pre>

Another useful pseudo class is <code>:focus</code>. We recorded how many times users started typing in the contact form. It was interesting to find out that in about 10% of cases users did not actually submit the form.</p>

<pre><code class="language-css">
input[name="message"]:focus {
    background-image: url('https://www.google-analytics.com/collect?v=1&amp;_v=j23&amp;a=...');
}
</code></pre>

On one page, we had a step-by-step questionnaire. At the end, the user was asked to agree with some terms and conditions. Some of the visitors did not complete that last step. In the first version of the site, we were not able to determine what these users had selected in the questionnaire because the results would have been sent after completion. However, because all the steps were just radio buttons, we used the <code>:checked</code> pseudo class and successfully tracked the selections:

<pre><code class="language-css">
input[value="female"]:checked {
    background-image: url('https://www.google-analytics.com/collect?v=1&amp;_v=j23&amp;a=...');
}
</code></pre>

One of the most important statistics we had to deliver was about the diversity of screen resolutions. Thanks to media queries this was possible:

<pre><code class="language-css">
@media all and (max-width: 640px) {
    body {
        background-image: url('https://www.google-analytics.com/collect?v=1&amp;_v=j23&amp;a=...');
    }
}
</code></pre>

In fact, there are <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Media_queries">quite a few logical operators</a> that we can use. We can track screens with a specific aspect ratio; devices in landscape orientation; or those with a resolution of 300dpi.

## Drawbacks

The problem with this kind of CSS UI tracking is that we get only the first occurrence of the event. For example, take the <code>:active</code> pseudo class example. The request for the background image is fired only once. If we need to capture every click then, we have to change the URL, which is not possible without JavaScript.

We used the <code>background-image</code> property to make the HTTP requests. However, sometimes we might need to set a real image as a background because of the application's design. In such cases we could use the <code>content</code> property. It is usually used for adding text or icons but the property also accepts an image. For example:

<pre><code class="language-css">
input[value="female"]:checked {
    content: url('https://www.google-analytics.com/collect?v=1&amp;_v=j23&amp;a=...');
}
</code></pre>

Because we are requesting an image, we should make sure that the browser is not caching the file. The statistics server should process the request each time. We could achieve this by providing the correct headers. Check out the image below. It shows the response headers sent by Google:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91ae96f7-2430-4e7b-9211-9ab89446ecce/2-google-analytics-large-preview-opt.png"><img title="Tracking UI with CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/258b7e5c-6367-43bd-8492-1009d350f99c/2-google-analytics-preview-opt.png" alt="Tracking UI with CSS" width="500" height="239" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91ae96f7-2430-4e7b-9211-9ab89446ecce/2-google-analytics-large-preview-opt.png">View large version</a>)</figcaption></figure>

Sending the following headers guarantees that the browser will not cache the image:

<pre><code class="language-css">
Cache-Control: no-cache, no-store, must-revalidate
Pragma: no-cache
Expires: 0
</code></pre>

In some cases, we may decide to write our own statistics server. This is an important note that we must consider during development. Here is a simple Node.js-based implementation. We used that for testing purposes:

<pre><code class="language-css">
var fs = require('fs'),
    http = require('http'),
    url = require('url'),
    img = fs.readFileSync(__dirname + '/stat.png'),
    stats = {};

var collectStats = function(type) {
    console.log('collectStats type=' + type);
    if(!stats[type]) stats[type] = 0;
    stats[type]++;
}

http.createServer(function(req, res){
    var request = url.parse(req.url, true);
    var action = request.pathname;
    if (action == '/stat.png') {
        collectStats(request.query.type);
        res.writeHead(200, {'Content-Type': 'image/gif', 'Cache-Control': 'no-cache' });
        res.end(img, 'binary');
    } else {
        res.writeHead(200, {'Content-Type': 'text/html' });
        res.end('Stats server:&lt;pre&gt;' + JSON.stringify(stats) + '&lt;/pre&gt;\n');
    }
}).listen(8000, '127.0.0.1');
console.log('Server is running at https://127.0.0.1:8000');
</code></pre>

If we save the code to a file called <i>server.js</i> and execute <code>node server.js</code> we will get a server listening on port 8000. There are two possible URLs for querying:

<pre><code class="language-css">
* https://127.0.0.1:8000/ - shows the collected statistics
* https://127.0.0.1:8000/stat.png?type=something - collecting statistics.
</code></pre>

By requesting the PNG in the second URL, we are incrementing values. The following piece of code shows the HTML and CSS that we have to place in the browser:

<pre><code class="language-css">
&lt;input type="button" value="click me"/&gt;

input[type="button"]:active {
    background-image: url('https://127.0.0.1:8000/stat.png?type=form-submitted');
}
</code></pre>

Finally, as a last drawback we have to mention that some antivirus software or browser settings may remove 1×1px beacons. So we have to be careful when choosing this technique and make sure that we provide workarounds.</p>

## Summary

CSS is usually considered a language for applying styles to webpages. However, in this article we saw that it is more than that. It is also a handy tool for collecting statistics.

{{< signature "ds, il, og" >}}


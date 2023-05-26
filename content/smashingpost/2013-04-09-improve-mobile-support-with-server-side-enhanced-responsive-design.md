---
title: Improve Mobile Support With Server-Side-Enhanced Responsive Design
slug: improve-mobile-support-with-server-side-enhanced-responsive-design
image: >-
  https://www.smashingmagazine.com/wp-content/uploads/2013/04/Server-Side-Enhanced-Responsive-Design.png
date: 2013-04-09T13:58:48.000Z
author: jon-arne
description: >-
  In many ways, responsive Web design deserves a big share of the honor for
  making the Web more usable on non-desktop devices. This trend of letting the
  browser determine more about how a Web page should be displayed makes sense,
  especially now that mobile browsers are slightly more trustworthy than in the
  old days of mobile.
categories:
  - Mobile
  - Techniques
  - Performance
  - Responsive Design
---
In many ways, responsive Web design deserves a big share of the honor for making the Web more usable on non-desktop devices. This trend of letting the browser determine more about how a Web page should be displayed makes sense, especially now that mobile browsers are slightly more trustworthy than in the old days of mobile.

However, <strong>a responsive website is not automatically a mobile-friendly website</strong>. Amid the buzz of trendy Web development techniques, the good ol’ Web server doesn’t get the spotlight it deserves. Modern Web development should be about finding the right balance between server-side and client-side implementation.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5842f9d5-0254-4e80-a2a7-f9838bc9b24b/serverclient.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b143570-6b21-4680-8e64-a8161b1ea4c8/serverclient-500.png" alt="Serverside or client side" width="500" height="386" /></a><br>
<em>Find the right mix of client-side and server-side logic for adaptive Web design.</em>

There is no one right answer to what should be done on the server and what should be done on the client side. That depends on the website in question. It is clear, however, that <strong>an either/or approach would fail to meet expectations</strong>. I will use a real-life project that my company is working on, with real requirements and pain points, as a reference. We are taking a pragmatic approach to the Web, starting with a blank sheet of paper to find the best solutions for both the technical and business requirements.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Server-Side Device Detection With JavaScript](https://www.smashingmagazine.com/2014/07/server-side-device-detection-with-javascript/)
*   [<span class="headline">Building A Better Responsive Website</span>](https://www.smashingmagazine.com/2013/03/building-a-better-responsive-website/)
*   [Responsible Considerations For Responsive Web Design](https://www.smashingmagazine.com/2013/03/responsible-web-design/)
*   [Losing Users If Responsive Web Design Is Your Only Strategy](https://www.smashingmagazine.com/2014/07/responsive-web-design-should-not-be-your-only-mobile-strategy/)
*   [<span class="headline">How To Provide The Greatest Mobile User Experience Possible</span>](https://www.smashingmagazine.com/2013/05/providing-the-best-mobile-user-experience-possible/)

{{% feature-panel %}}

## The Starting Point

Our client in this project is a large global news provider. Mobile is obviously crucial to it, because a large proportion of its audience doesn’t have access to a desktop device. Nevertheless, desktop access is just as important, and the solution needs to account for both.

Like many “forward-leaning” Web projects today, a general requirement was to consider <a href="https://www.lukew.com/ff/entry.asp?933">mobile first</a>, from both a technical and business perspective. That means HTML5 and RWD (in its broadest sense), for starters. At the same time, because the client was a global content distributor, having tools that could handle less-capable browsers and devices (ones that don’t support the principles of RWD and HTML5) well was essential.

The real challenge in this project was to make the most of RWD techniques, but also to address some of the challenges of RWD from a mobile perspective. This is where the server-side part comes into the picture. <strong>Doing as much optimization on the server side as possible</strong> makes sense, to relieve the client of data transferring and the execution of logic in the browser.

The main reason for doing this is performance. Most of the <a href="https://www.webperformancetoday.com/2011/04/20/desktop-vs-mobile-web-page-load-speed/">time taken by a page to load</a> is caused by the browser trying to make sense of the data being received. <a href="https://www.slideshare.net/stubbornella/designing-fast-websites-presentation">Being slow has a cost</a>, and every millisecond counts, regardless of the business model. Especially for big websites like our client’s, the cost of poor performance adds up to significant numbers. Even if you have many great <a href="https://en.wikipedia.org/wiki/Polyfill">polyfills</a> that provide shims, with fallbacks for missing functionality in browsers, favoring speed, performance and maintainability over polyfills makes sense.

Another point in favor of server-side device detection is its support of different business models and other business requirements. Advertising and other third-party content is one example that is much discussed, but other requirements need to be met, such as <a href="https://www.lukew.com/ff/entry.asp?1509">customized experiences</a> for specific devices, like the iPad.

With these considerations in mind, here are some of the requirements identified in our reference project:

*   No black box magic. The client needed to be able to control the full value chain.
*   Effortlessly integrated into the editorial process and CMS. Mobile had to be a part of the daily routine.
*   Fast page loading, to minimize data transfer and rendering time.
*   Easy for Web developers to use, regardless of the technology, to enable innovation and free thinking.
*   Support of business requirements, such as targeted business models and advertising and customized experiences for specific devices.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23b6b26b-7618-4ff4-b8da-0bf384aa296e/smg-req.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23b6b26b-7618-4ff4-b8da-0bf384aa296e/smg-req.png" alt="general requirements" width="500" height="248" /></a><br>
<em>A summary of our requirements, which I believe are pretty standard for most current mobile-oriented Web projects. (Image: <a href="https://wpzoom.com">WPZOOM</a>)</em>

## The Approach

The logical way to approach this is to find a way to combine the best of RWD and client-side techniques with server-side functionality based on device detection. This is sometimes called <a href="https://www.lukew.com/ff/entry.asp?1392">RESS</a> (responsive Web design with server-side components). The purpose of RESS is to do the heavy lifting on the server, making work easier for the browser, but also providing enough flexibility to meet any business requirements as described above. However, both RWD and RESS are parts of a bigger picture, sometimes referred to as <a href="https://bradfrostweb.com/blog/mobile/beyond-media-queries-anatomy-of-an-adaptive-web-design/">adaptive design</a>.

<strong>Making the design adaptive</strong>, throughout the value chain, is our goal. Presenting content in a browser is only a part of the story. A lot of stuff happens to the content before it reaches the browser.

From a developer’s perspective, there are no real best practices or dedicated tools for these kinds of requirements. The wheel has to be invented — or at least developers have to be helped to decide which wheel to use when, and how to mount it to different vehicles.

We decided to address the lack of tools. Even if there are some emerging best practices for RWD and good ol’ device-detection software, there are no good tools for combining the two to address the current needs when developing for the ubiquitous Web.

During our project, <strong>we identified five areas where the server’s side could be put to work</strong> to enhance client-side techniques.</p>

## 1\. Use Your CMS

But first, the obvious. The most important server-side component is the content management system (CMS).

If you look back a couple of years, mobile Web development was done by mobile specialists who performed their magic. This is not the case anymore. Web design and development is now driven by Web developers, usually working within, or at least connected to, the client’s organization. This is important to note, because this rules out the traditional approach to mobile Web design, whereby a magic mobile-platform proxy black box produces the mobile website. These platforms are usually based on some sort of proprietary XML format, screen scraping or other custom stuff that has to be learned.

<strong>We’re going mobile, but we are not replacing our CMS</strong>.

Another reason why a mobile publishing platform is not an option is that it would interfere with the editorial process. Being in control of the content and its behavior is important. So, the CMS is key. Managing all online entities, mobile, desktop, TV and so on from the current CMS makes sense, but going mobile must not require the content owner to change their CMS.

A side effect of making mobile an integral part of content publishing, which was important for this project, is that the Web developers, those working with the presentation of content, are able to effortlessly account for mobile. Mobile becomes a natural part of their work.

The best way to utilize the presentation layer in the CMS and to power-charge it is to tackle a range of devices, operating systems, browsers and interaction models. This is what’s so great about RWD. You can apply the technique on top of any CMS. <strong>RWD should be the default baseline of all Web projects.</strong> RWD restores fluidity to the Web. For websites that display mostly text and little fancy stuff, it might even be enough to serve the purpose alone.

Because the CMS might be just as important as the browser in creating an adaptive website, the server-side components must also be capable of enhancing the CMS. This happens to be true of the next four server-side techniques we’ll look at.</p>

## 2\. Use A Device-Description Repository

In my own experience, avoiding the need for some sort of server-side device detection has proven difficult. A few tools are available for device detection. The WURFL-powered device-detection repository (DDR) provided by <a href="https://www.scientiamobile.com/">ScientiaMobile</a> has been around the longest and is the basis for much of the server-side optimization in our project. However, even though ScientiaMobile provides an API to the WURFL database, we needed more flexibility and, so, built a <a href="https://en.wikipedia.org/wiki/Representational_state_transfer">RESTful</a> API on top of it.

The device database can then be queried like this:

<pre><code class="language-javascript">GET https://example.com/ddr/c/&lt;WURFL capability here&gt;</code></pre>

And the answer is returned in JSON format (asking for the device model):

<pre><code class="language-javascript">HTTP/1.1 200 OK
Content-Type: application/json

{"model_name":"iPhone"}</code></pre>

With this simple API, device detection can easily be used directly from the browser, using AJAX, or from the server-side programming language. Moreover, it can easily be used with popular feature-detection frameworks such as <a href="https://modernizr.com/">Modernizr</a>.

The nice thing about doing this server side is that <strong>the same information is available both client side and server side</strong> (including the CMS). Furthermore, it also provides a way to store “<a href="https://en.wikipedia.org/wiki/Tacit_knowledge">tacit knowledge</a>,” defining how the client should tackle certain aspects of the website. Tacit knowledge can be stored as custom capabilities and accessed the same way as any standard WURFL capability. The service is accompanied by a JavaScript library that appends additional client-side detected data. This helps the service make sense of a request when traditional analysis of the HTTP header is insufficient.

Today, the type of markup is not important, and most of the adaptation has moved into the CSS, JavaScript and images. In general, there is no need to serve any markup other than plain HTML5. The only exception is certain markets around the world in which feature phones, rather than smart devices, are dominant. In these cases, we need enough flexibility to handle these devices by serving a particular markup such as <a href="https://en.wikipedia.org/wiki/XHTML_Mobile_Profile">XHTML MP</a>. The device-detection service will provide that.</p>

### A Note on Caching and CDNs

As traffic from mobile devices increases rapidly, caching and content delivery networks (<abbr title="Content Delivery Network">CDN</abbr>) become keys part of the value chain. Adapting the markup to each device type or user agent would lead to “cache pollution,” which basically means that the cache is too big to make any difference. <strong>Keeping the markup of a page as static as possible across devices</strong> is key. As mentioned, most optimization in modern browsers happens in CSS and JavaScript. Cache pollution is a relevant issue for those resources, too, but less critical because CSS and JavaScript are easier to cache in the browser and are also typically generic to the website (i.e. the whole website uses the same CSS, so the file needs to be cached only once to be served to all pages on the website).</p>

## 3\. Execute CSS Media Queries Server-Side

Media queries in CSS are one of the key parts of RWD. They are also one of the page resources with the most overhead when it comes to <a href="https://scottjehl.github.com/CSS-Download-Tests/">excess data downloaded</a>. A mobile phone will download and process styles meant for desktop devices, which can have a detrimental impact on speed and user experience. Of course, well-designed CSS will minimize the issue, but more can be done to reduce CSS overhead.

For this project, we decided to do two things:

1.  Execute media queries server side, based on what we know about the client, using the DDR.
2.  Take it a step further by turning the device’s capabilities into media features.

To illustrate the first point, styles in the following media query would not be served to an iPhone because the viewport would never be as wide as 1200 pixels.

<pre><code class="language-css">@media screen and (min-width: 1200px) {
    /* styles here */
}</code></pre>

This requires a slightly different way of thinking and must, of course, be used with caution because <strong>breakpoints might never reach the client</strong>. Hence, CSS architecture is important.

The second illustrates the more powerful side of this, where device capabilities become media features:

<pre><code class="language-css">@media screen and (pointing-method: touchscreen) {
    .button{
        padding:1em;
    }
}</code></pre>

The above adds some extra padding to buttons to make them easily touchable on touchscreens. Another, perhaps more useful, example is the handling of fonts in CSS:

<pre><code class="language-css">@media screen and (font-face: true) {
    @font-face {
      font-family: 'Rambla';
      font-style: normal;
      font-weight: 400;
      src: local('Rambla'), local('Rambla-Regular'), url(https://themes.googleusercontent.com/static/fonts/rambla/v1/4oKK3Z-EimNu4ISiv21vMuvvDin1pK8aKteLpeZ5c0A.woff) format('woff');
    }
}</code></pre>

Thus, all <a href="https://scientiamobile.com/wurflCapability/tree">capabilities defined in WURFL</a> are available for querying. Custom capabilities can also be added to the system to be made available as media features, too. Again, it’s a different way of thinking about styling. But it’s very powerful, especially for handling browser bugs, “undetectables” and “false positives” from feature detection (which are pretty annoying when they happen), and third-party content. Tests we performed indicated that up to two thirds of the data could be saved using this technique.

To comply with the requirements of the project, we decided to implement it in the markup like this:

<pre><code class="language-markup">&lt;link
href="https://example1.com/css/https://example2.com/path/style.css"
rel="stylesheet"
type="text/css" /&gt;</code></pre>

In this snippet, the service executing the media queries lives at <code>https://example1.com/css/</code>, and proxies the CSS located at <code>https://example2.com/path/style.css</code>, and then executes, caches and returns the CSS needed by the client.</p>

### 4. Optimizing Images

<a href="https://www.alistapart.com/articles/responsive-images-how-they-almost-worked-and-what-we-need/">Image optimization</a> has been a hot potato lately. Until standards and support are established, and given that polyfills are not an option, <strong>the best way to optimize images is still to resize and prepare them server side</strong>.

The principle of image resizing is similar to CSS and has been proven to work with TinySrc (now <a href="https://www.sencha.com/products/io/">Sencha.io</a>):

<pre><code class="language-markup">&lt;img src="https://example.com/img/https://farm9.staticflickr.com/8154/7705240114_fdc69e5882_k_d.jpg" alt="Butterfly" /&gt;</code></pre>

In this example, the service will download and resize the image according to the screen size of the requesting device, and then cache and serve it to the client.

Being able to specify a size is also handy:

<pre><code class="language-markup">&lt;img src="https://example.com/img/px_320/https://farm9.staticflickr.com/8154/7705240114_fdc69e5882_k_d.jpg" alt="Butterfly" /&gt;</code></pre>

But this is not very responsive. This is one of those times when we need to combine client-side feature detection with server-side logic.

<strong>Below is an example of a JavaScript add-on defining different breakpoints</strong> and communicating this to the server through a cookie.

<pre><code class="language-javascript">if (vpw &gt;= 1024) {
    vpw = 1024; //viewport
    bp = "w"; //breakpoint for current viewport
} else if (vpw &gt;= 768) {
    bp = "m";
} else {
    bp = "n";
}</code></pre>

Then, we instruct the resizing service to behave differently according to the current breakpoint. In the image URL in our markup, we state that for breakpoint <code>w</code>, we want an image scaled to 80% of the viewport’s width. For breakpoints <code>m</code> and <code>n</code>, the values are 60 and 40%, respectively.

<pre><code class="language-markup">&lt;img src="https://example1.com/img/vpw_768/bp_m/pc/w_80/m_60/n_40/https://farm9.staticflickr.com/8154/7705240114_fdc69e5882_k_d.jpg" alt="Butterfly" /&gt;</code></pre>

High-DPI screens are also supported through the <code>@</code> notation:

<pre><code class="language-markup">&lt;img src="https://example.com/img/px_300/@_2/https://farm9.staticflickr.com/8154/7705240114_fdc69e5882_k_d.jpg" alt="Butterfly"/&gt;</code></pre>

<a href="https://blog.netvlies.nl/design-interactie/retina-revolution/">As noted by Daan Jobsis</a>, a high-resolution image does not necessarily entail a ton of data, because the image could be compressed much more than a low-resolution image without a visible loss in quality.</p>

### 5. Pre-Processing and Intelligent Caching

When addressing these issues, <strong>we noted that some tasks are “compile time” and others are “runtime.”</strong> Runtime tasks typically perform device detection on the server side to optimize something for a particular device or browser’s capability. Compile-time optimization handles the preprocessing of images, the minification of JavaScript, the preprocessing of Sass and LESS and so on. This can easily be implemented as <a href="https://git-scm.com/book/en/Customizing-Git-Git-Hooks">Git hooks</a>. It enables an alternative workflow for Web developers, which might be more relevant for some, depending on the server’s configuration and architecture.

By using Git, the CSS, JavaScript and images (and even the page itself) can be pushed to a host (e.g. <code>static.example.com</code>) where static content would be served from. The static resources would, of course, be optimized runtime as well to enable the server-side media queries and image resizing. This way, the extra roundtrip for fetching the resource, as described above, is avoided, too.

This approach might seem to be a trivial detail at first, but if you think of it like a CDN or a cache for static content, it becomes very powerful. Suddenly, the cache becomes intelligent. You can perform tasks when pushing to the cache (compile time) and also do runtime optimization for the device or browser.</p>

## The Findings

To illustrate the findings, I have made a demo based on one of the examples that comes with <a href="https://twitter.github.com/bootstrap/">Twitter Bootstrap</a> and that puts the server-side components to work. The demo is very simple, and much more adaption of Bootstrap should be done, but it illustrates the findings well.

The diagram below shows the distribution of different content types tested in a desktop browser and on an iPhone with Safari. The most obvious difference is the savings we get when optimizing images.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d4d8cdc-4d1e-47c8-8fbf-fb3aa2ad4d0c/stats-dtvsip.png"><img class="133626" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d4d8cdc-4d1e-47c8-8fbf-fb3aa2ad4d0c/stats-dtvsip.png" alt="weight of content types" width="450" height="193" /></a><br>
<em>Distribution of content types</em>

### Faster and Leaner

The overall result is that we can definitely save time and money by letting the server help the client with adapting the content and presentation:
<table class="table-overview"><br>
<tbody>
<tr>
<th></th>
<th><strong>Desktop</strong></th>
<th><strong>iPhone</strong></th>
</tr>
<tr>
<td>Page size</td>
<td> 927.1 KB</td>
<td> 338.8 KB</td>
</tr>
<tr>
<td>Rendering time (onload)</td>
<td> 6.6 seconds</td>
<td> 4.64 seconds</td>
</tr>
</tbody>
</table>

The page for an iPhone is only 37% of the total page weight of a desktop client. The page also loads faster on the iPhone. It is not the fastest page to begin with, but <strong>a 30% increase in speed is a good start</strong>.

Yes, many factors come into play that can influence the tests’ results, but the tests prove that knowing who you are talking to at the other end <a href="https://www.slideshare.net/stubbornella/designing-fast-websites-presentation">pays off</a>.

With this approach, we think we have been successful in designing a system that solves the current issues involved in getting the Web to work on different devices as well as in providing Web developers with useful tools to support their goals. <strong>The server can definitely improve the performance of RWD and other client-side techniques</strong> on mobile devices!

As standards emerge and as devices and networks improve, some issues will disappear, but new ones will pop up as the Web becomes more diverse. Handling diversity is a question not so much of whether to do things server side or client side, but of how to make the whole value chain as intelligent and adaptable as possible to prepare for the unknown — all the way from creating the content to caching to rendering in the browser.

During the project, we became so excited by the results and possibilites that we decided to make the tools available to Web developers out there. Because the project is still ongoing, we haven’t launched yet, but if you think the approach described here is worth a try, you can sign up at WhateverWeb to get early access. (It’s free, but we’d just like you to tell us what you think.)

<em>(al) (ea)</em>


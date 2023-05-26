---
title: 'S(GH)PA: The Single-Page App Hack For GitHub Pages'
slug: sghpa-single-page-app-hack-github-pages
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73f9f9c1-91bd-47d9-97b5-a84857e29f7e/mystery-80-1-big-opt.jpg'
date: 2016-08-16T18:01:23.000Z
author: danielbuchner
summary: >-
  lorem ipsum
description: >-
  lorem ipsum
categories:
  - Git
  - Apps
  - Coding
  - Static Generators
disable_ads: true
---
For some time now, I’ve wanted the ability to route paths for a GitHub Pages website to its index.html for handling as a single-page app (SPA). This is table-stakes because such apps require all requests to be routed to one HTML file, unless you want to copy the same file across all of your routes every time you make a change to the project. Currently, GitHub Pages doesn’t offer a route-handling solution; the Pages system is intended to be a flat, simple mechanism for serving basic project content.

In case you weren’t aware, GitHub does provide one morsel of customization for your project website: the ability to add a <code>404.html</code> file and have it served as your custom error page. I took a first stab at an SPA hack simply by duplicating my <code>index.html</code> file and renaming the copy to <code>404.html</code>. Turns out that many folks have <a href="https://twitter.com/csuwildcat/status/730558238458937344">experienced the same issue</a> with GitHub Pages and liked the general idea. However, the problem that some folks on Twitter correctly raised was that the <code>404.html</code> page is still served with a status code of 404, which is not good for search engine crawlers. The gauntlet had been thrown down, and I decided to answer — and answer with vigor!

## One More Time, With Feeling

After sleeping on it, I thought to myself, “Self, we’re deep in dirty hack territory, so why don’t I make this hack even dirtier?!” To that end, I developed an even better hack that provides the same functionality and simplicity, while also preserving your website’s crawler juice — and you don’t even need to waste time duplicating your <code>index.html</code> file and renaming it to <code>404.html</code> anymore! The following solution should work in all modern desktop and mobile browsers (Edge, Chrome, Firefox, Safari) and in Internet Explorer 10+.

<strong>Template and Demo</strong>: <em>If you want to skip the explanation and get the goods, here’s a <a href="https://github.com/csuwildcat/sghpa">template repo</a>, and a test URL to see it in action.</em>

{{% feature-panel %}}

## That’s So Meta

The first thing I did was investigate other options for getting the browser to redirect to the <code>index.html</code> page. That part was pretty straightforward. You basically have three options: a server config, a JavaScript <code>location</code> manipulation, or a <code>refresh</code> meta tag. The first one is obviously a no-go for GitHub pages. And JavaScript is basically the same as a refresh, but arguably worse for crawler indexing. That leaves us with the meta tag. A meta tag with a refresh value of <code>0</code> <a href="https://sebastians-pamphlets.com/google-and-yahoo-treat-undelayed-meta-refresh-as-301-redirect/">appears to be treated as a 301 redirect</a> by search engines, which works out well for this use case.

You’ll need to start by adding a <code>404.html</code> file to a <code>gh-pages</code> repository that contains an empty HTML document inside it. That document <em>must</em> total more than 512 bytes (explained below). Next, put the following markup in your <code>404.html</code> page’s <code>head</code> element:

<pre><code class="language-js">&lt;script&gt;
  sessionStorage.redirect = location.href;
&lt;/script&gt;
&lt;meta http-equiv="refresh" content="0;URL='/REPO_NAME_HERE'"&gt;</code></pre>

This code sets the attempted entrance URL to a variable on the standard sessionStorage object and immediately redirects to your project’s <code>index.html</code> page using a meta refresh tag. If you’re doing a Github Organization site, don’t put a repo name in the content attribute replacer text, just do this: <code>content="0;URL='/'"</code>

### Customizing Route Handling

If you want more elaborate route handling, just include some additional JavaScript logic in the <code>script</code> tag shown above. You can tweak several things: the composition of the <code>href</code> that you pass to the <code>index.html</code> page; which pages should remain on the 404 page (via dynamic removal of the meta tag); and any other logic you want to put in place to dictate what content is shown based on the inbound route.

### 512 Magical Bytes

This is, hands down, one of the strangest quirks I have ever encountered in web development. You must ensure that the total size of your <code>404.html</code> page is greater than 512 bytes, because if it isn’t, Internet Explorer will disregard it and show a generic browser 404 page instead. When I finally figured this out, I had to crack open a beer to cope with the amount of time it took.

## Let’s Make History

To capture and restore the URL that the user initially navigated to, you’ll need to add the following <code>script</code> tag to the <code>head</code> of your <code>index.html</code> page <em>before</em> any other JavaScript acts on the page’s current state:

<pre><code class="language-js">&lt;script&gt;
  (function(){
    var redirect = sessionStorage.redirect;
    delete sessionStorage.redirect;
    if (redirect &amp;&amp; redirect != location.href) {
      history.replaceState(null, null, redirect);
    }
  })();
&lt;/script&gt;</code></pre>

This bit of JavaScript retrieves the URL that we cached in <code>sessionStorage</code> over on the <code>404.html</code> page and replaces the current <code>history</code> entry with it. How you choose to handle things from here is up to you, but I’d use <code>popstate</code> and <code>hashchange</code> if I were you.

Well, folks, that’s it. Now go celebrate by writing some single-page apps on GitHub Pages!
<blockquote>This article is part of a web development series from Microsoft tech evangelists and engineers on practical JavaScript learning, open-source projects and interoperability best practices, including <a href="https://blogs.windows.com/msedgedev/2015/05/06/a-break-from-the-past-part-2-saying-goodbye-to-activex-vbscript-attachevent/?wt.mc_id=DX_873182">Microsoft Edge</a> browser.

We encourage you to test across browsers and devices (including Microsoft Edge — the default browser for Windows 10) with free tools on <a href="https://dev.windows.com/en-us/?wt.mc_id=DX_873182">dev.microsoftedge.com</a>, including the <a href="https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/f12-devtools-guide/?wt.mc_id=DX_873182">F12 developer tools</a>: seven distinct, fully documented tools to help you debug, test and speed up your web pages. Also, visit the <a href="https://blogs.windows.com/msedgedev/?wt.mc_id=DX_873182">Edge blog</a> to stay informed by Microsoft developers and experts.</blockquote>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)
*   [Creating A Complete Web App In Foundation For Apps](https://www.smashingmagazine.com/2015/04/creating-web-app-in-foundation-for-apps/)
*   [Build A Blog With Jekyll And GitHub Pages](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/)

{{< signature "al, il" >}}

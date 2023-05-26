---
title: 'Searchable Dynamic Content With AJAX Crawling'
slug: searchable-dynamic-content-with-ajax-crawling
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea75c388-0c4e-423a-a4ff-fdf8a170669a/crawlerserverdiagram-front-page1.jpg
date: 2011-09-27T10:30:29.000Z
author: zack-grossbart
summary: >-
  Google needs a way to let you serve AJAX content to browsers while serving simple HTML to crawlers. In other words, you need the same content in multiple formats. Find out more in this article.
description: >-
  Google needs a way to let you serve AJAX content to browsers while serving simple HTML to crawlers. In other words, you need the same content in multiple formats. Find out more in this article.
categories:
  - Coding
  - SEO
  - AJAX
  - JavaScript
  - Techniques
---

Google Search likes simple, easy-to-crawl websites. You like dynamic websites that show off your work and that really pop. But search engines can’t run your JavaScript. That cool AJAX routine that loads your content is hurting your SEO.

Google’s robots parse HTML with ease; they can pull apart Word documents, PDFs and even images from the far corners of your website. But as far as they’re concerned, AJAX content is invisible.

{{% feature-panel %}}

## The Problem With AJAX

AJAX has revolutionized the Web, but it has also hidden its content. If you have a Twitter account, try viewing the source of your profile page. There are no tweets there &mdash; just code! Almost everything on a Twitter page is built dynamically through JavaScript, and the crawlers can’t see any of it. That’s why Google developed AJAX crawling.

Because Google can’t get dynamic content from HTML, you will need to provide it another way. But there are two big problems: Google won’t run your JavaScript, and it doesn’t trust you.

Google indexes the entire Web, but it doesn’t run JavaScript. Modern websites are little applications that run in the browser, but running those applications as they index is just too slow for Google and everyone else.

The trust problem is trickier. Every website wants to come out first in search results; your website competes with everyone else’s for the top position. Google can’t just give you an API to return your content because some websites use dirty tricks like <a href="https://en.wikipedia.org/wiki/Cloaking">cloaking</a> to try to rank higher. Search engines can’t trust that you’ll do the right thing.

Google needs a way to let you serve AJAX content to browsers while serving simple HTML to crawlers. In other words, you need the same content in multiple formats.

## Two URLs For The Same Content

Let’s start with a simple example. I’m part of an open-source project called Spiffy UI. It’s a <a href="https://code.google.com/webtoolkit/">Google Web Toolkit</a> (GWT) framework for REST and rapid development. We wanted to show off our framework, so we made <a href="https://www.spiffyui.org">SpiffyUI.org</a> using GWT.

GWT is a dynamic framework that puts all of our content in JavaScript. Our <code>index.html</code> file looks like this:

<pre><code class="language-markup tmp-html">&lt;body&gt;
   &lt;script type="text/javascript" language="javascript"
   src="org.spiffyui.spsample.index.nocache.js"&gt;&lt;/script&gt;
&lt;/body&gt;</code></pre>

Everything is added to the page with JavaScript, and we control our content with <a href="https://en.wikipedia.org/wiki/Hashtag#Hashtags">hash tags</a> (I’ll explain why a little later). Every time you move to another page in our application, you get a new hash tag. Click on the “CSS” link and you’ll end up here:

<pre><code class="language-markup tmp-html">https://www.spiffyui.org#css</code></pre>

The URL in the address bar will look like this in most browsers:

<pre><code class="language-markup tmp-html">https://www.spiffyui.org/?css</code></pre>

We’ve fixed it up with HTML5. I’ll show you how later in this article.

This simple hash works well for our application and makes it bookmarkable, but it isn’t crawlable. Google doesn’t know what a hash tag means or how to get the content from it, but it does provide an alternate method for a website to return content. So, we let Google know that our hash is really JavaScript code instead of just an anchor on the page by adding an exclamation point (a “bang”), like this:

<pre><code class="language-markup tmp-html">https://www.spiffyui.org#!css</code></pre>

This hash bang is the secret sauce in the whole AJAX crawling scheme. When Google sees these two characters together, it knows that more content is hidden by JavaScript. It gives us a chance to return the full content by making a second request to a special URL:

<pre><code class="language-markup tmp-html">https://www.spiffyui.org?_escaped_fragment_=css</code></pre>

The new URL has replaced the <code>#!</code> with <code>?_escaped_fragment_=</code>. Using a URL parameter instead of a hash tag is important, because parameters are sent to the server, whereas hash tags are available only to the browser.

That new URL lets us return the same content in HTML format when Google’s crawler requests it. Confused? Let’s look at how it works, step by step.

## Snippets Of HTML

The whole page is rendered in JavaScript. We needed to get that content into HTML so that it is accessible to Google. The first step was to separate SpiffyUI.org into snippets of HTML.

Google still thinks of a website as a set of pages, so we needed to serve our content that way. This was pretty easy with our application, because we have a set of pages, and each one is a separate logical section. The first step was to make the pages bookmarkable.

### Bookmarking

Most of the time, JavaScript just changes something *within* the page: when you click that button or pop up that panel, the URL of the page does not change. That’s fine for simple pages, but when you’re serving content through JavaScript, you want give users unique URLs so that they can bookmark certain areas of your application.

JavaScript applications can change the URL of the current page, so they usually support bookmarking via the addition of hash tags. Hash tags work better than any other URL mechanism because they’re not sent to the server; they’re the only part of the URL that can be changed without having to refresh the page.

The hash tag is essentially a value that makes sense in the context of your application. Choose a tag that is logical for the area of your application that it represents, and add it to the hash like this:

<pre><code class="language-markup tmp-html">https://www.spiffyui.org#css</code></pre>

When a user accesses this URL again, we use JavaScript to read the hash tag and send the user to the page that contains the CSS.

You can choose anything you want for your hash tag, but try to keep it readable, because users will be looking at it. We give our hashes tags like <code>css</code>, <code>rest</code> and <code>security</code>.

Because you can name the hash tag anything you want, adding the extra bang for Google is easy. Just slide it between the hash and the tag, like this:

<pre><code class="language-markup tmp-html">https://www.spiffyui.org#!css</code></pre>

You can manage all of your hash tags manually, but most JavaScript history frameworks will do it for you. All of the plug-ins that support HTML4 use hash tags, and many of them have options for making URLs bookmarkable. We use <a href="https://github.com/balupton/history.js">History.js</a> by <a href="https://balupton.com/">Ben Lupton</a>. It’s easy to use, it’s open source, and it has excellent support for HTML5 history integration. We’ll talk more about that shortly.

### Serving Up Snippets

The hash tag makes an application bookmarkable, and the bang makes it crawlable. Now Google can ask for special escaped-fragment URLs like so:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ebed8c2-88c6-46af-a140-2fc3987cafd4/crawlerserverdiagram3.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea75c388-0c4e-423a-a4ff-fdf8a170669a/crawlerserverdiagram-front-page1.jpg" alt="screenshot" width="500" height="346" /></a></figure>

When the crawler accesses our ugly URL, we need to return simple HTML. We can’t handle that in JavaScript because the crawler doesn’t run JavaScript in the crawler. So, it all has to come from the server.

You can implement your server in PHP, Ruby or any other language, as long as it delivers HTML. SpiffyUI.org is a Java application, so we deliver our content with a <a href="https://en.wikipedia.org/wiki/Java_Servlet">Java servlet</a>.

The escaped fragment tells us what to serve, and the servlet gives us a place to serve it from. Now we need the actual content.

Getting the content to serve is tricky. Most applications mix the content in with the code; but we don’t want to parse the readable text out of the JavaScript. Luckily, Spiffy UI has an HTML-templating mechanism. The templates are embedded in the JavaScript but also included on the server. When the escaped fragment looks for the ID <code>css</code>, we just have to serve <code>CSSPanel.html</code>.

The template without any styling looks very plain, but Google just needs the content. Users see our page with all of the styles and dynamic features:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2136f445-51f5-4851-9133-d9799a53e48f/css-page-normal.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14fcf8fa-cb75-4842-b64c-6279bf78473d/specific-styles-500.jpg" alt="screenshot" width="500" height="438" /></a></figure>

Google gets only the unstyled version:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e2bd909-34cd-40af-b924-9ddbd23891b6/css-page-escaped1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bddc877b-73ea-42b8-87b0-f306c1b52562/google-specific-sytles.jpg" alt="screenshot" width="500" height="446" /></a></figure>

You can see all of the source code for our <code>SiteMapServlet.java</code> servlet. This servlet is mostly just a look-up table that takes an ID and serves the associated content from somewhere on our server. It’s called <code>SiteMapServlet.java</code> because this class also handles the generation of our site map.

{{% ad-panel-leaderboard %}}

## Tying It All Together With A Site Map

<a href="https://www.spiffyui.org/sitemap.xml">Our site map</a> tells the crawler what’s available in our application. Every website should have a site map; AJAX crawling doesn’t work without one.

Site maps are simple XML documents that list the URLs in an application. They can also include data about the priority and update frequency of the app’s pages. Normal entries for site maps look like this:

<pre><code class="language-markup tmp-html">&lt;url&gt;
   &lt;loc&gt;https://www.spiffyui.org/&lt;/loc&gt;
   &lt;lastmod&gt;2011-07-26&lt;/lastmod&gt;
   &lt;changefreq&gt;daily&lt;/changefreq&gt;
   &lt;priority&gt;1.0&lt;/priority&gt;
&lt;/url&gt;</code></pre>

Our AJAX-crawlable entries look like this:

<pre><code class="language-markup tmp-xml">&lt;url&gt;
   &lt;loc&gt;https://www.spiffyui.org/#!css&lt;/loc&gt;
   &lt;lastmod&gt;2011-07-26&lt;/lastmod&gt;
   &lt;changefreq&gt;daily&lt;/changefreq&gt;
   &lt;priority&gt;0.8&lt;/priority&gt;
&lt;/url&gt;</code></pre>

The hash bang tells Google that this is an escaped fragment, and the rest works like any other page. You can mix and match AJAX URLs and regular URLs, and you can use only one site map for everything.

You could write your site map by hand, but there are tools that will save you a lot of time. The key is to format the site map well and submit it to Google Webmaster Tools.

## Google Webmaster Tools

<a href="https://www.google.com/webmasters/tools">Google Webmaster Tools</a> gives you the chance to tell Google about your website. Log in with your Google ID, or create a new account, and then verify your website.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64029821-4985-482c-b6c6-68de1b427a6f/google-wmt-verification.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec45bbd6-06f0-44b7-adc1-6dacc03cf76f/google.wemaster-central" alt="screenshot" width="500" height="485" /></a></figure>

Once you’ve verified, you can submit your site map and then Google will start indexing your URLs.

And then you wait. This part is maddening. It took about two weeks for SpiffyUI.org to show up properly in Google Search. I posted to the help forums half a dozen times, thinking it was broken.

There’s no easy way to make sure everything is working, but there are a few tools to help you see what’s going on. The best one is <a href="https://www.google.com/support/webmasters/bin/answer.py?hl=en&amp;answer=158587">Fetch as Googlebot</a>, which shows you exactly what Google sees when it crawls your website. You can access it in your dashboard in Google Webmaster Tools under “Diagnostics.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da682b13-e9ff-4566-b947-2b367f003198/googlebot-fetch.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5471e284-443b-4be1-a174-08e3b35e8cc7/webmastertools-2.jpg" alt="screenshot" width="500" height="476" /></a></figure>

Enter a hash bang URL from your website, and click “Fetch.” Google will tell you whether the fetch has succeeded and, if it has, will show you the content it sees.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92b9845d-563c-4674-acf1-3785030aea82/googlebot-results.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5213a8ad-eff6-4977-8081-ba49e7b5c5fa/webastertools-3.jpg" alt="screenshot" width="500" height="494" /></a></figure>

If Fetch as Googlebot works as expected, then you’re returning the escaped URLs correctly. But you should check a few more things:

*   [Validate your site map](https://www.validome.org/google/validate).
*   Manually try the URLs in your site map. Make sure to try the hash-bang and escaped versions.
*   Check the Google result for your website by searching for `site:www.yoursite.com`.

## Making Pretty URLs With HTML5

Twitter leaves the hash bang visible in its URLs, like this:

<pre><code class="language-markup tmp-html">https://twitter.com/#!/ZackGrossbart</code></pre>

This works well for AJAX crawling, but again, it’s slightly ugly. You can make your URLs prettier by integrating HTML5 history.

Spiffy UI uses HTML5 history integration to turn a hash-bang URL like this…

<pre><code class="language-markup tmp-html">https://www.spiffyui.org#!css</code></pre>

… into a pretty URL like this:

<pre><code class="language-markup tmp-html">https://www.spiffyui.org?css</code></pre>

HTML5 history makes it possible to change this URL parameter, because the hash tag is the only part of the URL that you can change in HTML4. If you change anything else, the entire page reloads. HTML5 history changes the entire URL without refreshing the page, and we can make the URL look any way we want.

This nicer URL works in our application, but we still list the hash-bang version on our site map. And when browsers access the hash-bang URL, we change it to the nicer one with a little JavaScript.

## Cloaking

Earlier, I mentioned cloaking. It is the practice of trying to boost a website’s ranking in search results by showing one set of pages to Google and another to regular browsers. Google doesn’t like cloaking and may <a href="https://www.google.com/support/webmasters/bin/answer.py?answer=66355">remove offending websites from its search index</a>.

AJAX-crawling applications always show different results to Google than to regular browsers, but it isn’t cloaking if the HTML snippets contain the same content that the user would see in the browser. The real mystery is how Google can tell whether a website is cloaking or not; crawlers can’t compare content programmatically because they don’t run JavaScript. It’s all part of Google’s Googley power.

Regardless of how it’s detected, cloaking is a bad idea. You might not get caught, but if you do, you’ll be removed from the search index.

## Hash Bang Is A Little Ugly, But It Works

I’m an engineer, and my first response to this scheme is “Yuck!” It just feels wrong; we’re warping the purpose of URLs and relying on magic strings. But I understand where Google is coming from; the problem is extremely difficult. Search engines need to get useful information from inherently untrustworthy sources: us.

Hash bangs shouldn’t replace every URL on the Web. Some websites have had <a href="https://www.webmonkey.com/2011/02/gawker-learns-the-hard-way-why-hash-bang-urls-are-evil/">serious problems</a> with hash-bang URLs because they rely on JavaScript to serve content. Simple pages don’t need hash bangs, but AJAX pages do. The URLs do look a bit ugly, but you can fix that with HTML5.

### Other Resources

We’ve covered a lot in this article. Supporting AJAX crawling means that you need to change your client’s code and your server’s code. Here are some links to find out more:

*   “[Making AJAX Applications Crawlable](https://code.google.com/web/ajaxcrawling/),” Google Code
*   [sitemaps.org](https://www.sitemaps.org/)
*   [Google Webmaster Tools](https://www.google.com/webmasters/tools)
*   [Spiffy UI source code](https://code.google.com/p/spiffyui/source/checkout), with a complete example of AJAX crawling.

*Thanks to Kristen Riley for help with some of the images in this article.*

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Learning JavaScript: Essentials And Guidelines](https://www.smashingmagazine.com/learning-javascript-essentials-guidelines-tutorials/)
*   [Why AJAX Isn’t Enough](https://www.smashingmagazine.com/2015/01/why-ajax-isnt-enough/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [A Beginner’s Guide To jQuery-Based JSON API Clients](https://www.smashingmagazine.com/2012/02/beginners-guide-jquery-based-json-api-clients/)

{{< signature "al, mrn" >}}

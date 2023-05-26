---
title: The Website Launch Checklist – 15 Essential Checks Before You Go Live
slug: 15-essential-checks-before-launching-your-website
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e00cf1d-110d-416d-b1c1-a0bbe759c6c7/checklist.jpg
date: 2009-04-07T20:29:49.000Z
author: lee-munroe
description: >-
  Your website is designed, the CMS works, content has been added and the client
  is happy. It’s time to take the website live. Or is it? When launching a
  website, you can often forget a number of things in your eagerness to make it
  live, so it’s useful to have a checklist to look through as you make your
  final touches and before you announce your website to the world.
categories:
  - Design
  - Web Design
  - Checklists
  - Launch
  - Validation
---
Your website is designed, the CMS works, content has been added and the client is happy. It’s time to take the website live. Or is it? When launching a website, you can often forget a number of things in your eagerness to make it live, so it’s useful to have a checklist to look through as you make your final touches and before you announce your website to the world.

This article <strong>reviews some important and necessary checks that web-sites should be checked against before the official launch</strong> — little details are often forgotten or ignored, but – if done in time – may sum up to an overall greater user experience and avoid unnecessary costs after the official site release. Here is your website launch checklist:

## <span class="rh">Further Reading</span> on SmashingMag:

*   [What Is The Last Thing You Do Before You Launch A Website?](https://www.smashingmagazine.com/2010/07/what-is-the-last-thing-you-do-before-you-launch-a-website/)
*   [Building An Effective ‘Coming Soon’ Page For Your Product](https://www.smashingmagazine.com/2011/05/building-an-effective-coming-soon-page-for-your-product/)
*   [Elements Of A Viral Launch Page](https://www.smashingmagazine.com/2011/09/elements-of-a-viral-launch-page/)
*   [How To Launch Anything](https://www.smashingmagazine.com/2013/06/how-to-launch-anything/)

### Favicon

A favicon brands the tab or window in which your website is open in the user’s browser. It is also saved with the bookmark so that users can easily identify pages from your website. Some browsers pick up the favicon if you save it in your root directory as favicon.ico, but to be sure it’s picked up all the time, include the following in your head.

{{% feature-panel %}}

<pre><code class="language-markup tmp-xml">&lt;link rel="icon" type="image/x-icon" href="/favicon.ico" /&gt;</code></pre>

And if you have an iPhone favicon:

<pre><code class="language-markup tmp-xml">&lt;link rel="apple-touch-icon" href="/favicon.png" /&gt;</code></pre>

<figure><img loading="lazy" decoding="async" class="alignnone wp-image-1136 size-full" title="Description" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3738f3dc-8a6d-4a4a-84ef-e701e3479824/9rules.jpg" alt="website launch checklist" width="593" height="283" /></figure>

### Titles And Meta Data

Your page title is the most important element for SEO and is also important so that users know what’s on the page. Make sure it changes on every page and relates to that page’s content.

<pre><code class="language-markup tmp-xml">&lt;title&gt;10 Things To Consider When Choosing The Perfect CMS | How-To | Smashing Magazine&lt;/title&gt;</code></pre>

Meta description and keyword tags aren’t as important for SEO (at least for the major search engines anyway), but it’s still a good idea to include them. Change the description on each page to make it relate to that page’s content, because this is often what Google displays in its search result description.

<pre><code class="language-markup tmp-xml">&lt;meta name="description" content="By Paul Boag Choosing a content management system can be tricky. Without a clearly defined set of requirements, you will be seduced by fancy functionality that you will never use. What then should you look" /&gt;</code></pre>

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="1136" title="Description" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc85555f-67c5-40c2-a1b0-64e2a53d5b87/b-desc.jpg" alt="Description" /></figure>

### Cross-Browser Checks

Just when you think your design looks great, pixel perfect, you check it in IE and see that everything is broken. It’s important that your website works across browsers. It doesn’t have to be pixel perfect, but everything should work, and the user shouldn’t see any problems. The most popular browsers to check are Internet Explorer 6, 7 and 8, Firefox 3, Safari 3, Chrome, Opera and the iPhone.

<figure><img loading="lazy" decoding="async" class="alignnone wp-image-1136 size-full" title="Description" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d837abbd-a2bb-4a18-a025-0f6e9e7ffa9d/checks.jpg" alt="website launch checklist" width="544" height="295" /></figure>

*   [7 fresh and simple ways to test cross-browser compatibility](https://freelancefolder.com/7-fresh-and-simple-ways-to-test-cross-browser-compatibility/)

### Proofread

Read everything. Even if you’ve already read it, read it again. Get someone else to read it. There’s always something you’ll pick up on and have to change. See if you can reduce the amount of text by keeping it specific. Break up large text blocks into shorter paragraphs. Add clear headings throughout, and use lists so that users can scan easily. Don’t forget about dynamic text too, such as alert boxes.

*   [Writing for the web](https://www.useit.com/alertbox/9703b.html)

### Links

Don’t just assume all your links work. Click on them. You may often forget to add “https://” to links to external websites. Make sure your logo links to the home page, a common convention.

Also, think about how your links work. Is it obvious to new users that they are links? They should stand out from the other text on the page. Don’t underline text that isn’t a link because it will confuse users. And what happens to visited links?

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="1137" title="Links" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/550d8633-4a0a-4823-b592-cf870bdb4e14/b-links.jpg" alt="Links" /></figure>

*   [W3C Link Checker](https://validator.w3.org/checklink)

### Functionality Check

Test everything thoroughly. If you have a contact form, test it and copy yourself so that you can see what comes through. Get others to test your website, and not just family and friends but the website’s target market. Sit back and watch how a user uses the website. It’s amazing what you’ll pick up on when others use your website differently than how you assume they’d use it. Common things to check for are contact forms, search functions, shopping baskets and log-in areas.</p>

### Graceful Degradation

Your website should work with JavaScript turned off. Users often have JavaScript turned off for security, so you should be prepared for this. You can easily turn off JavaScript in Firefox. Test your forms to make sure they still perform server-side validation checks, and test any cool AJAX stuff you have going on.

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="1139" title="Javascript" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dbd11f4-ddc3-4fce-a692-50e309710836/b-js.jpg" alt="Javascript" /></figure>

### Validation

You should aim for a 100% valid website. That said, <a href="https://www.leemunroe.com/how-important-is-valid-html-web-standards/">it isn’t the end of the world if your website doesn’t validate</a>, but it’s important to know the reasons why it doesn’t so that you can fix any nasty errors. Common gotchas include no “alt” tags, no closing tags and using “&amp;” instead of “&amp;amp;” for ampersands.

<figure><a href="https://www.webstandardistas.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="1140" title="Valid" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ac4837b-1f29-4387-b66a-3f035b1a0855/b-valid.jpg" alt="Valid" /></a></figure>

*   [10 reasons your code won’t validate (and how to fix it)](https://net.tutsplus.com/articles/web-roundups/10-reasons-why-your-code-wont-validate-and-how-to-fix-it/)
*   [W3C validator](https://validator.w3.org/)

### RSS Link

If your website has a blog or newsreel, you should have an RSS feed that users can subscribe to. Users should be able to easily find your RSS feed: the common convention is to put a small RSS icon in the browser’s address bar.

Put this code between your &lt;head&gt; tags.

<pre><code class="language-markup tmp-xml">&lt;link rel="alternate" type="application/rss+xml" title="Site or RSS title" href="link-to-feed" /&gt;</code></pre>

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="1141" title="RSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9984546-f8ea-4bc7-8fb1-4ad23b58c7eb/b-rss.jpg" alt="RSS" /></figure>

### Analytics

Installing some sort of analytics tool is important for measuring statistics to see how your website performs and how successful your conversion rates are. Track daily unique hits, monthly page views and browser statistics, all useful data to start tracking from day 1. <a href="https://www.google.com/analytics/">Google Analytics</a> is a free favorite among website owners. Others to consider are <a href="https://getclicky.com/">Clicky</a>, <a href="https://kissmetrics.com/">Kissmetrics</a>, <a href="https://haveamint.com/">Mint</a> and <a href="https://statcounter.com/">StatCounter</a>.

<figure><a href="https://getclicky.com/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="1142" title="Clicky" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4610ea7-5706-4d17-aaac-7708841fd7c9/clicky.gif" alt="Analytics" width="598" height="481" /></a></figure>

### Sitemap

Adding a sitemap.xml file to your root directory allows the major search engines to easily index your website. The file points crawlers to all the pages on your website. <a href="https://www.xml-sitemaps.com/">XML-Sitemaps</a> automatically creates a sitemap.xml file for you. After creating the file, upload it to your root directory so that its location is www.mydomain.com/sitemap.xml.

If you use WordPress, install the <a href="https://www.arnebrachhold.de/projects/wordpress-plugins/google-xml-sitemaps-generator/">Google XML Sitemaps plug-in</a>, which automatically updates the sitemap when you write new posts. Also, add your website and sitemap to <a href="https://www.google.com/webmasters/tools">Google Search Console</a>. This tells Google that you have a sitemap, and the service provides useful statistics on how and when your website was last indexed.

<figure><a href="https://www.arnebrachhold.de/projects/wordpress-plugins/google-xml-sitemaps-generator/"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="1142" title="Clicky" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4389fe54-815c-44d6-abc7-3804bc54d99f/xml.gif" alt="Analytics" width="523" height="209" /></a></figure>

### Defensive Design

The most commonly overlooked defensive design element is the 404 page. If a user requests a page that doesn’t exist, your <strong>404 page</strong> is displayed. This may happen for a variety of reasons, including another website linking to a page that doesn’t exist. Get your users back on track by providing a useful 404 page that directs them to the home page or suggests other pages they may be interested in.

Another defensive design technique is <strong>checking your forms for validation</strong>. Try submitting unusual information in your form fields (e.g. lots of characters, letters in number fields, etc.) and make sure that if there is an error, the user is provided with enough feedback to be able to fix it.

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="1143" title="404" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19fb9724-22f7-46b4-90ac-845ff4310a00/b-404.jpg" alt="404" /></figure>

*   [404 error pages reloaded](https://www.smashingmagazine.com/2007/08/17/404-error-pages-reloaded/)

### Optimize

You’ll want to configure your website for <strong>optimal performance</strong>. You should do this on an ongoing basis after launch, but you can take a few simple steps before launch, too. Reducing HTTP requests, using CSS sprites wherever possible, optimizing images for the Web, compressing JavaScript and CSS files and so on can all help load your pages more quickly and use less server resources.

Besides, depending on the publishing engine that you are using, you may need to consider taking more specific measures – for instance, if you are using WordPress, you may need to consider <a href="https://www.arnebrachhold.de/2007/02/16/four-plus-one-ways-to-speed-up-the-performance-of-wordpress-with-caching/">useful caching techniques to speed up the performance</a>.

<figure><a href="https://developer.yahoo.com/performance/rules.html"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="1143" title="404" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04fb10ae-7734-4013-a09d-8f1b850adc41/yahoo.gif" alt="Yahoo Best Practices" width="480" height="400" /></a></figure>

*   [Best practices for speeding up your website](https://developer.yahoo.com/performance/rules.html)
*   [Web page analyzer](https://www.websiteoptimization.com/services/analyze/)

### Back Up

If your website runs off a database, you need a back-up strategy. Or else, the day will come when you regret not having one. If you use WordPress, install <a href="https://wordpress.org/extend/plugins/wp-db-backup/">Wordpress Database Backup</a>, which you can set up to automatically email you backups.</p>

### Print Style Sheet

If a user wants to print a page from your website, chances are she or he wants only the main content and not the navigation or extra design elements. That’s why it is a good idea to create a print-specific style sheet. Also, certain CSS elements, such as floats, don’t come out well when printed.

To point to a special CSS style sheet that computers automatically use when users print a page, simply include the following code between your &lt;head&gt; tags.

<pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet" type="text/css" href="print.css" media="print" /&gt;</code></pre>

*   [Printing The Web: Solutions and Techniques](https://www.smashingmagazine.com/2007/02/21/printing-the-web-solutions-and-techniques/)
*   [A List Apart: Going to print](https://www.alistapart.com/articles/goingtoprint/)

## Download the Ultimate Website Launch Checklist!

Just recently Dan Zambonini has published a very detailed checklist that covers both the pre-launch and the post-launch phase of the web site life cycle. Among other things his <a href="https://www.boxuk.com/blog/the-ultimate-website-launch-checklist">Ultimate Launch Checklist</a> contains checks related to content and style, standards and validation, search engine visibility, functional testing, security/risk, performance and marketing.

<figure><img loading="lazy" decoding="async" title="Ultimate Check List" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41a1acb8-f546-48ef-b003-bb02e940cc8a/ultimate.gif" alt="Ultimate Check List" width="544" height="306" /></figure>

The checklist is a very useful reference that may help you in your daily projects and will help you to prevent errors and mistake once the site is released.

You may also want to consider the <a href="https://www.uxbooth.com/blog/quick-usability-checklist/">Quick Usability Check List</a> by David Leggett that highlight some of the more common problems designers should address on their own sites in a Usability checklist of sorts. Not all of these items will apply to every website, these are just suggested things to look for in your own site design.

<figure><a href="https://www.uxbooth.com/blog/quick-usability-checklist/"><img loading="lazy" decoding="async" title="Ultimate Check List" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6a87904-a31a-4ed6-a5f0-1ded70dcc422/usab.jpg" alt="Quick Usability Check List" width="549" height="337" /></a></figure>

## What other checks would you list?

Make yourself a to-do list and keep it handy to check over before making any website live. Are there any other points you would add? Share them in the comments!

{{< signature "al" >}}


---
title: Technical SEO – Fundamental Principles
slug: technical-seo-2015-wiring-websites-organic-search
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7de070b2-6d09-42cb-9e1d-614e1aaf59f5/01-site-architecture-opt-small.png
date: 2015-11-25T19:49:00.000Z
author: tombennet
description: >-
  Ask ten people what SEO is, and you’re likely to **get ten different
  answers**. Given the industry’s unsavoury past, this is hardly surprising.
  Keyword stuffing, gateway pages, and comment spam earned the first _search
  engine optimisers_ a deservedly poor reputation within the web community.

  Snake oil salesmen continue to peddle these harmful techniques to unsuspecting
  website owners today, perpetuating the myth that optimising your website for
  Google or Bing is an inherently nefarious practise. Needless to say, **this is
  not true**.
categories:
  - Coding
  - SEO
  - Optimization
---
Ask ten people what SEO is, and you’re <strong>likely to get ten different answers</strong>. Given the industry’s unsavoury past, this is hardly surprising. Keyword stuffing, gateway pages, and comment spam earned the first <em style="line-height: 1em;">search engine optimizers</em> a deservedly poor reputation within the web community. Snake oil salesmen continue to peddle these harmful techniques to unsuspecting website owners today, perpetuating the myth that optimizing your website for Google or Bing is an inherently nefarious practice.
<img loading="lazy" decoding="async" title="Technical SEO – Fundamental Principles" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7de070b2-6d09-42cb-9e1d-614e1aaf59f5/01-site-architecture-opt-small.png" alt="Technical SEO – Fundamental Principles" width="500" height="246" />

Needless to say, <strong>this is not true</strong>.

Broadly speaking, today’s SEO industry is split into two related fields: content marketing and technical optimisation. The ability to create content that resonates with audiences and communicates a brand identity is <em>vital</em> to the success of any website, and articles exploring every intricacy of this art can be found on the web with relative ease.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [SEO For Responsive Websites](https://www.smashingmagazine.com/2013/11/seo-for-responsive-websites/)
*   [What The Heck Is SEO? A Rebuttal](https://www.smashingmagazine.com/2012/12/what-heck-seo-rebuttal/)
*   [How Content Creators Benefit From The New SEO](https://www.smashingmagazine.com/2012/06/content-creators-benefit-from-new-seo/)
*   [The Importance Of HTML5 Sectioning Elements](https://www.smashingmagazine.com/2013/01/the-importance-of-sections/)

{{% feature-panel %}}

When it comes to the latter field, however - technical optimization - the <strong>waters are often muddied by misinformation</strong>. This extraordinarily rich discipline is the key to realizing the organic search potential of your content, and despite being listed as a skill on many developers’ resumés, it is also one of the most frequently misunderstood areas of modern web development.

Today we’ll be exploring <strong>three of the fundamental principles of technical SEO</strong>. By the end, you’ll be armed with a wealth of techniques for organic search optimization that are applicable to almost all established websites. Let’s get started.</p>

## Crawl Accessibility

Search engines use automated bots commonly known as spiders to find and crawl content on the web. Google’s spider (‘Googlebot’) discovers URLs by following links and by reading sitemaps provided by webmasters. It interprets the content, adds these pages to Google’s index, and ranks them for search queries to which it deems them relevant.</p>

<strong>If Googlebot cannot efficiently crawl your website, it will not perform well in organic search.</strong> Regardless of your website’s size, history, and popularity, severe issues with crawl accessibility will cripple your performance and impact your ability to rank organically. Google assign a resource ‘budget’ to each domain based on its authority (more on this later), which is reflected in the regularity and depth of Googlebot’s crawl. Therefore, our primary goal is to maximize the efficiency of Googlebot’s visits.</p>

### Architecture & Sitemaps

This process begins with the basic architecture of your site. Disregard hackneyed advice telling you to make all information accessible within three clicks, and instead focus on building a website in accordance with Information Architecture (IA) best practices. Peter Morville’s <em>Information Architecture for the World Wide Web</em> is required reading (the <a href="https://shop.oreilly.com/product/0636920034674.do">fourth edition</a> is available since September 2015), and you can find a good introduction to the basic principles of IA as they relate to SEO <a href="https://moz.com/blog/information-architecture-for-seo-whiteboard-friday">over at Moz.com</a>.

Site structure should be crafted following extensive keyword research into search behavior and user intent. This is an art in itself, and we’ll not be covering it here; as a general rule, however, you’ll want a logical, roughly symmetrical, pyramid-shaped hierarchy with your high-value category pages near the top and your more-specific pages closer to the bottom. Click-depth should be a consideration, but not your foremost concern.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a232d15e-6ede-4460-b132-ef661a9ae63e/01-site-architecture-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7de070b2-6d09-42cb-9e1d-614e1aaf59f5/01-site-architecture-opt-small.png" alt="technical seo" width="500" height="246" /></a><figcaption>A diagram of the ideal site architecture, with the top dot representing the homepage. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a232d15e-6ede-4460-b132-ef661a9ae63e/01-site-architecture-opt.png">View large version</a>)</figcaption></figure>

This architecture should be reflected with <strong>a static and human-readable URL structure</strong>, free of dynamic parameters where possible, and which uses hyphens rather than underscores as word separators (see Google’s guidelines on <a href="https://support.google.com/webmasters/answer/76329">URL structure</a>). Maintain a consistent internal linking pattern, and avoid creating outlying, orphaned pages. Remember that search crawlers cannot use search forms, and so all content should be accessible via direct links.

Search engines can be told about the structure and content of a website by using <a href="https://www.sitemaps.org/protocol.html">XML Sitemaps</a>. These are particularly useful for large websites and those with a significant quantity of rich media, as they can be used to indicate content types, change frequency, and page priority to search crawlers. They are <em>not</em>, however, a good fix for fundamental architectural issues such as orphaned content. Take a look through <a href="https://support.google.com/webmasters/answer/156184">Google’s documentation</a> to learn more about how sitemaps are interpreted.

Your sitemap - which can be broken up into multiple smaller sitemaps and a sitemap index file, if necessary - can be submitted to Google by using <a href="https://www.google.com/webmasters/tools/home">Search Console</a> (formerly Webmaster Tools). In the spirit of search engine agnosticism, it’s also advisable to declare your sitemap’s location in a manner accessible to other crawlers. This can be done using <code>robots.txt</code>, <a href="https://en.wikipedia.org/wiki/Robots_exclusion_standard#Sitemap">a plaintext file</a> that sits in the top-level directory of your web server, with the following declaration:

<pre><code>Sitemap: https://yourdomain.com/sitemap-index-file.xml</code></pre>

XML Sitemaps can be generated automatically using a variety of free tools, such as the <a href="https://wordpress.org/plugins/wordpress-seo/">Yoast SEO Plugin</a> for websites running on WordPress (the relevant documentation is <a href="https://kb.yoast.com/article/96-enable-xml-sitemaps-in-the-wordpress-seo-plugin">available here</a>). If your sitemaps are being generated manually, be sure to keep them up-to-date. Avoid sending search crawlers to URLs that are blocked in your <code>robots.txt</code> file (see the next section), return <code>404</code> errors, are non-canonical, or result in redirects, since all of these will waste your site’s crawl budget.

We’ll explore these principles in greater depth and look at ways of diagnosing and fixing related issues in <a href="#crawl-efficiency">Section 2 of this article</a>.</p>

### Blocked Content

At times, you may wish to prevent search engines from discovering certain content on your website. Common examples include customer account areas, heavily personalised pages with little value to organic search, and staging sites under active development. Our goals here are twofold: to prevent these URLs from showing up in organic search results, and to ensure they are not absorbing our site’s crawl budget unnecessarily.

Robots <code>meta</code> tags are a part of the <a href="https://en.wikipedia.org/wiki/Robots_exclusion_standard">Robots Exclusion Protocol (REP)</a>, and can be used to instruct search engines <strong>not to list a URL in their results pages</strong>. Placed within the page <code>head</code>, the syntax is very simple:

<pre><code class="language-markup">&lt;meta name="robots" content="noindex,nofollow"&gt;
</code></pre>

The tag accepts <a href="https://yoast.com/articles/robots-meta-tags/">dozens of values</a>, and <code>noindex</code> and <code>nofollow</code> are two of the best supported. Together they prevent spiders from indexing the page or following any of its links. These directives can also be applied via an HTTP header called <code>X-Robots-Tag</code>; this is often a more practical means of deployment, especially on larger sites. On Apache with <code>mod_headers</code> enabled, the following would prevent PDF documents from being indexed or having their links followed by spiders:

<pre><code class="language-http">&lt;FilesMatch ".pdf$"&gt;
   Header set X-Robots-Tag "noindex, nofollow"
&lt;/FilesMatch&gt;
</code></pre>

Finally there’s <code>robots.txt</code>. Contrary to popular opinion, this file <strong>does not provide a means of preventing URLs from appearing in search results</strong>, nor does it provide any kind of security or privacy protection. It is publicly-viewable and discourages specific spiders from crawling certain pages or site sections. Each subdomain on a root domain will use a separate <code>robots.txt</code> file.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a58fbf-cbcb-4032-a240-65660bbfb376/02-blocked-by-robots-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b9df1c2-db5d-4818-aa22-b3875aac5ddc/02-blocked-by-robots-opt-small.png" alt="Blocked by robots.txt message in Google search results" /></a><figcaption>As you can see, pages blocked by <code>robots.txt</code> will still appear in search results. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a58fbf-cbcb-4032-a240-65660bbfb376/02-blocked-by-robots-opt.png">View large version</a>)</figcaption></figure>

A basic <code>robots.txt</code> file specifies a User Agent followed by one or more <code>Disallow</code> rules; these are relative URL paths from which you wish to block crawlers. Overrides can be configured by supplementing these with <code>Allow</code> rules. Pattern matching can be used to construct more complex rules, thanks to Google and Bing’s support for two regular expressions: end of string (<code>$</code>) and a wildcard (<code>*</code>). A simple example is given below:

<pre><code>User-agent: *
Disallow: /blocked-directory/
Allow: /blocked-directory/allowed-file.pdf$
</code></pre>

Google offers <a href="https://support.google.com/webmasters/answer/6062596">detailed guidelines</a> on writing rules for <code>robots.txt</code>, and provides an interactive testing environment as part of <a href="https://www.google.com/webmasters/tools/home">Search Console</a>.

Note that adding an on-page <code>noindex</code> directive to a page blocked in <code>robots.txt</code> will <em>not</em> cause it to stop appearing in search results. Crawlers that respect the disallow directives <strong>will not be able to see the tag</strong>, since they are prevented from accessing the page. You’ll need to unblock the page, then serve the <code>noindex</code> directive via an HTTP header or <code>meta</code> tag.

Another common mistake is to block crawlers from accessing CSS and JavaScript files that are required for page render. Google has been placing a renewed emphasis on this issue of late, and recently sent out <a href="https://www.seroundtable.com/google-warning-googlebot-css-js-20665.html">a fresh round of warnings</a> via Search Console.

Historically, Googlebot has been likened to a text-only browser such as Lynx, but today it is <strong>capable of rendering pages in a manner similar to modern web browsers</strong>. <a href="https://searchengineland.com/tested-googlebot-crawls-javascript-heres-learned-220157">This includes executing scripts</a>. As such, preventing crawlers from accessing these resources can impair organic performance. You can check for blocked resources and view an approximation of what Googlebot ‘sees’ by utilizing the <em>Blocked Resources</em> and <em>Fetch &amp; Render</em> tools in <a href="https://www.google.com/webmasters/tools/home">Search Console</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9f45473-2709-4031-a904-0fe58ad55fb2/03-fetch-render-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb403490-145e-4c24-a2ad-1e0de9280d9a/03-fetch-render-opt-small.png" alt="The Fetch and Render tool in Google Search Console" /></a><figcaption>The <em>Fetch and Render</em> tool in Google Search Console. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9f45473-2709-4031-a904-0fe58ad55fb2/03-fetch-render-opt.png">View large version</a>)</figcaption></figure>

Remember that you can quickly view a snapshot of how a page ‘looks’ to Googlebot by entering <code>cache:example.com/page</code> into Chrome’s address bar and selecting <em>Text-only version</em>.</p>

### Unparsable Content

Despite advances in Googlebot’s rendering capabilities, it remains true that websites making heavy use of AJAX and client-side JavaScript frameworks such as AngularJS are at a <strong>fundamental disadvantage when it comes to SEO</strong>.

The problem arises as a result of their reliance on hash fragment (<code>#</code>) URLs. Fragment identifiers are not sent as part of an HTTP request, and are often used to jump from one part of a page to another. Client-side JavaScript frameworks watch for changes in this hash fragment, dynamically manipulating the page without the need to make additional round trips to the server. In other words the <em>client</em> does the heavy lifting.

Heavy lifting is not Googlebot’s strong suit. Workarounds do exist, but they require additional development time and should ideally be baked into your workflow from the start.

The <a href="https://developers.google.com/webmasters/ajax-crawling/docs/getting-started">solution proposed by Google</a> back in 2010 involves replacing the hash (<code>#</code>) with a so-called hashbang (<code>#!</code>). Upon detecting that your site adheres to this scheme, Googlebot will modify each URL as follows:

<pre><code>Original: yourdomain.com/#!content
Modified: yourdomain.com/?_escaped_fragment_=content
</code></pre>

Everything after the hashbang is passed to the server in a special URL parameter called <code>_escaped_fragment_</code>. Your server must be configured to respond to these kinds of requests with a static HTML snapshot of the dynamic content.</p>

<a href="https://danwebb.net/2011/5/28/it-is-about-the-hashbangs">The flaws of this approach are numerous</a>. Hashbangs are an unofficial standard which do nothing to advance accessibility, and are arguably destructive to the nature of the web. In short, it’s an SEO kludge which <em>fails to fix the root cause of the problem</em>.</p>

<strong>HTML5 offers us a better solution</strong> in the form of the History API, a full introduction to which is available in <a href="https://diveintohtml5.info/history.html">Dive Into HTML5</a>. The <code>pushState</code> method allows us to manipulate browser history by changing the URL that appears in the address bar without making additional requests to the server. As a result, we reap the benefits of rich, JavaScript-powered interactivity <em>and</em> a traditional, clean URL structure.</p>

<pre><code>Original: yourdomain.com/#content
Modified: yourdomain.com/content
</code></pre>

This solution is not a magic bullet. Our server must be configured to respond to requests for these clean URLs with HTML rendered server-side, something that’s increasingly being achieved with <a href="https://www.smashingmagazine.com/2015/04/react-to-the-future-with-isomorphic-apps/">isomorphic JavaScript</a>. With good implementation, it’s possible to build a rich, JavaScript-powered web application which is accessible to search crawlers and adheres to the principles of <strong>progressive enhancement</strong>. Browser support for <code>pushState</code> is good, with <a href="https://caniuse.com/#search=pushstate">all modern browsers plus IE10</a> supporting the History API.

Finally, be wary of content that is inaccessible to robots. Flash files, Java applets, and other plugin-reliant content are all generally ignored or devalued by search engines, and should be avoided if you’re aiming for the content to be indexed.</p>

### Page Speed & Mobile

Search engine algorithms are becoming increasingly sensitive to <strong>usability</strong>, with <a href="https://developers.google.com/speed/">page speed</a> and <a href="https://developers.google.com/webmasters/mobile-sites/mobile-seo/">mobile-friendliness</a> being two of the most prominent examples. Thankfully, readers of Smashing Magazine should already be aware of the importance of these issues. Since it would be impossible to do these enormous subjects justice in the context of this article, we will limit ourselves to the basic principles of each.

Search engines support a variety of mobile configurations, including separate URLs for mobile users (via an <code>m.</code> subdomain, for example) and dynamic serving using the <code>Vary</code> HTTP header. Today, however, Google’s preferred approach to mobile is <strong>responsive web design</strong>. If you’re unfamiliar with modern front-end development, or have simply been living under a very large rock for the past five years, you could do worse than checking out <a href="https://www.smashingmagazine.com/2015/03/real-life-responsive-web-design-smashing-book-5/">Smashing Book 5</a> for a primer on modern RWD workflows.

Page speed, too, should be one of your foremost concerns. This is not simply because a longer load time results in a higher bounce rate; Google <a href="https://googlewebmastercentral.blogspot.co.uk/2010/04/using-site-speed-in-web-search-ranking.html">has indicated</a> that <strong>page speed itself factors into the ranking algorithm</strong>.

There are dozens of tools available to help you identify issues that could be slowing down your website. One good option is <a href="https://gtmetrix.com">GTmetrix</a>; it has both free and paid options, conducts analysis based on both Google PageSpeed and Yahoo YSlow rulesets, and provides many helpful visualizations and simulations.

Good first steps include:

*   Implementation of gzip compression on your server
*   Minification of assets like stylesheets and scripts
*   Leveraging browser caching with the `Expires` header
*   Minimising the number of HTTP requests _(although this recommendation in particular will make less sense as HTTP/2 adoption grows)_

Perhaps the <strong>best introduction to performance and page speed currently available</strong> is Lara Hogan’s <a href="https://designingforperformance.com/">Designing For Performance</a>. It’s a very practical guide to approaching projects with speed in mind, and it includes a great lesson on <em>how</em> browsers request and render content. It’s available for free online, but the sales proceeds go to charities focused on getting women and girls into coding, so you should definitely buy it.

Finally, be aware that search algorithms’ sensitivity to usability issues will only increase going forward. Even security is now a ranking factor; Google announced in late 2014 that sites using <a href="https://googlewebmastercentral.blogspot.co.uk/2014/08/https-as-ranking-signal.html">HTTPS encryption</a> would now see a slight advantage over sites that don’t.</p>

## Crawl Efficiency & Indexation

With the site sections we want to appear in organic search now accessible to crawlers, it is time to assess <em>how</em> your content is being interpreted and indexed.

We’ll begin by exploring one of the key principles of SEO-friendly site design: <em>duplicate content</em>. Contrary to popular belief, this phrase does not refer solely to literal carbon-copies of pages within your own site. As always in SEO, we must consider our site from the perspective of a robot. Therefore, when we refer to <em>duplicate</em> or <em>thin</em> content, we’re simply referring to URLs that meet the following criteria:

*   Return a `200 OK` [HTTP response status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), indicating that the requested resource exists
*   Return content that is available via other URLs (duplicate), or that offers no value to users (thin)

To help demonstrate the scope of these criteria, two examples from a prominent online UK retailer are provided below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ef13e93-2e26-4418-94b5-6793f1046a71/04-argos-duplicate-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd7473b4-2faf-47ea-a2cb-bae25656e78b/04-argos-duplicate-opt-small.png" alt="Argos duplicate category page" /></a><figcaption>Example 1, <a href="https://www.argos.co.uk/static/Browse/ID72/33012103/c_1/1|category_root|Baby+and+Nursery|33005732/c_2/2|33005732|Travel|33008428/c_3/3|cat_33008428|SEO+is+Dead|33012103.htm">Argos.co.uk</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ef13e93-2e26-4418-94b5-6793f1046a71/04-argos-duplicate-opt.png">View large version</a>)</figcaption></figure>

Here, each product category is accessible via an infinite number of nonsensical subcategories. This is an example of <strong>duplicate content</strong>; these URLs are being crawled and indexed by search engines, which constitutes a severe waste of the site’s crawl budget.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/039e863f-3b17-43a8-a213-af13e9b73971/05-argos-search-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/825b84ba-985c-4b6b-89d2-898ab19d1edf/05-argos-search-opt-small.png" alt="Argos search results for SEO is Dead" /></a><figcaption>Example 2, <a href="https://www.argos.co.uk/static/Search/searchTerm/seo+is+dead.htm">Argos.co.uk</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/039e863f-3b17-43a8-a213-af13e9b73971/05-argos-search-opt.png">View large version</a>)</figcaption></figure>

In this instance, search results pages - even those which turn up no product matches - lack any indexation directives and are completely open to search crawlers. This is a good example of <strong>thin content</strong> - these mostly-blank pages offer no value to users, and yet over <a href="https://www.google.co.uk/search?q=site%3Ahttp%3A%2F%2Fwww.argos.co.uk%2Fstatic%2FSearch%2FsearchTerm%2F+%22Hmmm%2C+no+search+results+for%22">22,000 have been indexed</a> at the time of writing.

It is well-known that Google’s algorithm penalizes sites for large-scale duplication of this kind, with <a href="https://googlewebmastercentral.blogspot.co.uk/2014/02/faceted-navigation-best-and-5-of-worst.html">faceted navigation systems</a> being particularly problematic in this regard. However, even the smallest of issues can become exacerbated over time. Behavioral quirks in your CMS or server configuration problems can lead to serious crawl budget waste and dilution of so-called <em>link equity</em> (the SEO ’value’ of external links to your pages - more on this in <a href="#link-profile">Section 3</a>). All-too-often, these issues go completely undetected by webmasters.

Our primary goal is to <strong>consolidate</strong> any duplicate, thin, or legacy content. One article could not begin to scratch the surface in terms of all the possible scenarios you might encounter, nor the approaches to their mitigation. Instead, we’ll be looking to arm ourselves with the tools to diagnose these issues when they occur.</p>

### Diagnostics

You can learn a remarkable amount about how your content is being indexed by using <a href="https://support.google.com/websearch/answer/2466433">advanced search operators</a>.

Entering <code>site:yourdomain.com</code> into Google will return a sample of URLs on your domain that have been indexed. Heading straight for the last of these paginated results - those Google deems least relevant - will often yield clues as to any duplication problems that are affecting your site. If you’re presented with a prompt to repeat the search with with “omitted results included” (see below), click it; the resulting unfiltered view is often a great way to uncover any particularly egregious problems.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20cd838c-7a71-4bfe-b661-67b3cfc16276/06-results-omitted-opt-small-84x84.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a19d152a-fc7d-4f6b-b1d0-70d29f0a525f/06-results-omitted-opt-small.png" alt="Always opt to see the unfiltered view in Google Search to diagnose problems" /></a><figcaption>Always opt to see the unfiltered view to diagnose problems. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20cd838c-7a71-4bfe-b661-67b3cfc16276/06-results-omitted-opt-small-84x84.png">View large version</a>)</figcaption></figure>

The <code>site:</code> operator can be made yet more powerful when combined with the <code>inurl</code>, <code>intitle</code>, exact (<code>"..."</code>), and negative (<code>-</code>) operators. By using these and other advanced operators as part of your investigation, it’s possible to diagnose certain major issues fairly quickly:

*   Check for accidentally-indexed subdomains and staging sites. If your website is supposed to sit on a `www`, for example, check for URLs missing that part of the URL.

        site:yourdomain.com -inurl:www

*   Check for multiple versions of your homepage by searching `<title>` tags. It’s common to see both the root domain and document name indexed separately: `yourdomain.com` and `yourdomain.com/index.html`, for example.

        site:yourdomain.com intitle:"Your Homepage Title"

*   Check for URLs appended with parameters that do not change page content, optionally within a particular directory. Session IDs and affiliate trackers are particularly common on large e-commerce platforms and can easily result in thousands of duplicated pages.

        site:yourdomain.com/directory/ inurl:trackingid=

Google’s <a href="https://www.google.com/webmasters/tools/home">Search Console</a> provides an excellent platform to monitor the overall health of your website. The <em>HTML Improvements</em> panel under <em>Search Appearance</em> is a good way of spotting duplicate content. Pay particular attention to the lists of identical <code>&lt;title&gt;</code> tags and meta descriptions, both of which help to diagnose issues with duplicate content and poorly marked-up pages.

Navigating to <em>Index Status</em> under <em>Google Index</em> will provide a historic view of your site’s indexation. Hit ‘Advanced’ to overlay this information with data on the number of URLs you’re blocking via your <code>robots.txt</code> file.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53f7dd6f-7d7c-4030-8da2-3f8a1dbc237f/07-index-status-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/402a1d90-144e-4448-b886-f373bd17db0d/07-index-status-opt-small.png" alt="A historic view of your site’s indexation in Search Console, including URLs blocked in robots.txt" /></a><figcaption>A historic view of your site’s indexation in Search Console, including URLs blocked in <code>robots.txt</code>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53f7dd6f-7d7c-4030-8da2-3f8a1dbc237f/07-index-status-opt.png">View large version</a>)</figcaption></figure>

Be sure to also check for <a href="https://support.google.com/webmasters/answer/181708">Soft 404 errors</a> under <em>Crawl</em> - <em>Crawl Errors</em>. These are instances where a non-existent page is failing to return the appropriate <code>404</code> status code. Remember, from the perspective of a robot, page content is unrelated to the HTTP response returned by the server. Users may be shown a “Page Not Found” message, but with improper error handling your server may be telling robots that the page exists and should be indexed.

Finally, take a look at the <em>Sitemaps</em> section under <em>Crawl</em>. As well as allowing you to test individual sitemaps, it can provide valuable insight into how Google and other search engines are interpreting your site structure. Pay close attention to the ratio of URLs indexed to URLs submitted; a significant discrepancy can be indicative of a problem with duplicate or ’thin’ content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/000685c9-a517-4a3d-9265-ea3addf3d2fc/08-sitemaps-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c634424-5147-470b-920d-6d3fc1883472/08-sitemaps-opt-small.png" alt="Submitted URLs versus indexed URLs in the Sitemaps section of Search Console" /></a><figcaption>Submitted URLs versus indexed URLs in the Sitemaps section of Search Console. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/000685c9-a517-4a3d-9265-ea3addf3d2fc/08-sitemaps-opt.png">View large version</a>)</figcaption></figure>

### Redirects & Rewrites

In situations where your duplicate or legacy content has an obvious ‘new’ URL - an old page which has been superseded, for example - the best course of action is generally to implement <strong>server side redirection</strong>. Human visitors will seamlessly arrive at the preferred URL, and search crawlers will understand that the original page has been moved.

Be sure to always return a code <code>301</code> (permanent) HTTP status response and not the Apache default, a code <code>302</code> (temporary). While humans won’t be able to tell the difference, robots interpret the two very differently. In contrast to a temporary redirect, a permanent redirect will:

*   Cause the old URL to eventually drop out of the search engine’s index
*   Pass on the _link equity_ of the old page to the new page, a concept we will be exploring in more depth in [Section 3](#link-profile)

Implementation will obviously vary depending on your server setup, but we’ll demonstrate some simple examples in Apache using the <code>.htaccess</code> configuration file. Particularly complex redirect mapping will generally require use of the <code>mod_rewrite</code> module, but don’t underestimate how much you can achieve with the <code>Redirect</code> and <code>RedirectMatch</code> directives in the simpler <code>mod_alias</code>. The following lines would redirect a single file, and an entire directory plus its contents, to their new locations via a code <code>301</code> redirect:

<pre><code>Redirect 301 /old-file.html https://www.yourdomain.com/new-file.html
RedirectMatch 301 ^/old-directory/ https://www.yourdomain.com/new-directory/
</code></pre>

Check the <a href="https://httpd.apache.org/docs/2.4/mod/mod_alias.html#redirect">Apache documentation</a> for more detailed guidance on implementing these directives.

In circumstances where we’re looking to address duplication of a more structural nature - the missing <code>www</code> issue mentioned above, for instance - we can use <strong>URL rewrite rules</strong>.

Our goal here is to ensure that our website is accessible only via our chosen hostname (<code>www.yourdomain.com</code>). Note that either is a valid choice, as long as we enforce it consistently. Requests for URLs which omit the <code>www</code> prefix should result in code <code>301</code> redirection to the corresponding canonical version. Users will seamlessly arrive on the correct page, and search crawlers understand which set of URLs should be indexed. We will achieve this with the following <code>mod_rewrite</code> directives:

<pre><code>RewriteEngine on
RewriteCond %{HTTP_HOST} ^yourdomain.com [NC]
RewriteRule ^(.*)$ https://www.yourdomain.com/$1 [L,R=301]
</code></pre>

Once again, consult the <a href="https://httpd.apache.org/docs/2.4/rewrite/remapping.html">Apache documentation</a> for more detailed guidelines. There is also documentation available for the corresponding modules in <a href="https://nginx.org/en/docs/http/ngx_http_rewrite_module.html">Nginx</a> and <a href="https://www.iis.net/learn/extensions/url-rewrite-module/using-the-url-rewrite-module">IIS</a>.

The relevance of URL rewrites to SEO goes beyond simple fixes. Crucially, it allows us to make resources available over HTTP at URLs which <strong>do not necessarily correspond to their locations in the file system</strong>. This allows us to implement a static, human-readable URL structure which reflects our logical, IA-compliant site architecture.

*   Original: `https://www.yourdomain.com/content/catID/43/prod.html?p=XjqG`
*   Rewritten: `https://www.yourdomain.com/category/product/`

The benefits of a clean URL structure in SEO cannot be overstated. In addition to providing an increase in crawl efficiency, a good implementation offers a huge usability advantage. Remember that the URL is one of the most prominent elements considered by searchers when deciding on which URL to click.

Given the sheer number of possible tech stacks, the methodology can vary greatly, but you can find a general summary of <a href="https://support.google.com/webmasters/answer/76329">URL best practices at Google</a>, and a helpful introduction to advanced rewrite conditions <a href="https://www.linode.com/docs/websites/apache-tips-and-tricks/rewrite-urls-with-modrewrite-and-apache/">at Linode.com</a>.

One final word on redirects: avoid chains where at all possible. Not only are they inefficient from a crawl efficiency standpoint, the amount of ‘value’ passed by a <code>301</code> (permanent) redirect diminishes with each sequential hop. Your goal should be to direct all variants and retired pages to the correct URL with a single permanent redirect. See <a href="#link-profile">Section 3</a> for more information on the concept of link value preservation.</p>

### The Canonical Tag

In situations where server-side redirection is impossible or inappropriate, there is another fix available to us: the <code>rel="canonical"</code> link element.</p>

<a href="https://googlewebmastercentral.blogspot.co.uk/2009/02/specify-your-canonical.html">First introduced in 2009</a> as part of a collaborative effort by Google, Bing, and Yahoo, the tag allows us to indicate to search engines the preferred URL for a page. Usage is simple: add a <code>link</code> element with the <code>rel="canonical"</code> attribute to the <code>head</code> section of the ‘true’ page and all its variants.

To use a simple homepage example:

*   `https://www.yourdomain.com`
*   `https://www.yourdomain.com/index.html`
*   `https://www.yourdomain.com?sessionid=1988`

Marking <strong>each</strong> of these with the following tag would indicate to search engines which version to show users:

<pre><code class="language-markup">&lt;link rel="canonical" href="https://www.yourdomain.com"&gt;
</code></pre>

Unlike a redirect, the canonical tag does not affect the URL shown in the user’s address bar. Instead, it is simply a hint to search engines to treat particular variants as a single page. <strong>Be sure that the URLs in your canonical tags are correct</strong>; canonicalizing your entire site to a single page or implementing canonicals that point at <code>404</code> errors can be disastrous.

Note that in <em>most</em> instances server-side redirection is a more robust and user-friendly way of addressing major duplication problems. If you are in a position to control a site’s architecture, it’s generally possible to avoid many of the scenarios that require canonical tags as a fix.

That being said, there are advantages to including self-referencing canonical tags on every page. When implemented correctly, they make a good first line of defence against unforeseen problems. If your site uses parameters to identify specific user comments (<code>…?comment=13</code>, for example), the canonical tag can ensure that links to these URLs do not lead to the indexation of duplicate pages.

When dealing with duplicate content, you should always look to address the <strong>root cause of the problem</strong> rather than using a proprietary solution. For this reason, disabling a problematic parameter and handling its function via a cookie is often a preferable solution to <a href="https://googlewebmastercentral.blogspot.co.uk/2011/07/improved-handling-of-urls-with.html">blocking the parameter</a> in a vendor-specific program like Google Search Console or Bing Webmaster Central. For a more detailed look into duplicate content and the approaches to tackling it, take a read of <a href="https://moz.com/blog/duplicate-content-in-a-post-panda-world">Dr. Pete Meyers’ article on Moz.com</a>.</p>

### Multi-regional & Multilingual

Websites that target more than one language or country can be particularly challenging from a search standpoint, given that such sites inherantly require multiplication of content. International SEO is an <em>extremely</em> broad subject that warrants an entire article to itself, and for this reason we will touch only on the basic principles here.

The structure of a multi-regional or multilingual website is worthy of careful consideration. Google’s own <a href="https://support.google.com/webmasters/answer/182192">guidelines on internationalisation</a> are a good starting point. There are dozens of factors to consider before opting for separate ccTLDs, subdomains, or subdirectories, and it is essential to consider the future of your site and plan implementation as thoroughly as possible before deployment.

Whichever route you choose, the <code>rel="alternate" hreflang="x"</code> attributes should be used to indicate to search engines the appropriate page to return to users searching in a particular language. These attributes are a <em>signal</em>, not a directive, and so other factors (server IP address or geotargeting settings in Search Console, for example) can override them.

Your <code>hreflang</code> annotations can be served via an HTTP header, by <a href="https://support.google.com/webmasters/answer/2620865">marking up your sitemaps</a>, or by using <code>link</code> elements in the <code>head</code> of your pages. The syntax for the latter implementation is as follows:

<pre><code class="language-markup">
&lt;link rel="alternate" href="https://yourdomain.com/en" hreflang="en"&gt;
&lt;link rel="alternate" href="https://yourdomain.com/de" hreflang="de"&gt;
&lt;link rel="alternate" href="https://yourdomain.com/fr" hreflang="fr"&gt;
&lt;link rel="alternate" href="https://yourdomain.com/fr-ca" hreflang="fr-ca"&gt;</code></pre>

The value of the <code>hreflang</code> attribute specifies the language in <a href="https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes">ISO 639-1</a> format, and (optionally) the region in <a href="https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2">ISO 3166-1 Alpha 2</a> format. In the example above, four versions of our homepage are specified: English, German, French (all non-region-specific), and finally French content localized for users in Canada. Each version of a page <strong>must identify every translated version, including itself</strong>. In other words, the above code block would be repeated on all four versions of our homepage. Finally, note that Google recommends <em>not</em> canonicalizing across different international page versions; instead, use the <code>canonical</code> tag only within the same version.

Internationalization can be notoriously complex, and as such it’s worth experimenting with tools such as Aleyda Solis’s <a href="https://www.internationalseomap.com/hreflang-tags-generator/">Hreflang Tags Generator Tool</a> and reading <a href="https://support.google.com/webmasters/answer/189077">Google’s documentation</a> in its entirety before even considering making changes to your website.

Finally, while we’re on the subject of region-specific content, it’s worth noting that SEO for local businesses carries with it a raft of additional opportunities. <a href="https://searchengineland.com/local-seo-rank-local-business-218906">Matthew Barby’s primer</a> on the subject for Search Engine Land is a good place to start.</p>

### Maintenance & Best Practices

In this section, we’ll be covering general best practices and housekeeping for SEO. This includes auditing your <strong>on-page meta data</strong> - titles, descriptions, headings, and so forth - and also checking for <strong>common internal issues</strong> which are easily overlooked.

In tandem with <a href="https://www.google.com/webmasters/tools/home">Google Search Console</a> or <a href="https://www.bing.com/toolbox/webmaster">Bing Webmaster Central</a>, the most useful tool available for everyday on-site SEO is a <em>simulated</em> search crawler. This is a piece of software that can be used to crawl your website in a manner similar to that of a search robot. The <a href="https://home.snafu.de/tilman/xenulink.html">Xenu Link Sleuth</a> is a good freeware option, but for serious work you cannot beat the <a href="https://www.screamingfrog.co.uk/seo-spider/">Screaming Frog SEO Spider</a>.

‘The Frog’, as it is affectionately dubbed, is fully configurable in terms of user agent, speed, crawl directory &amp; depth (including by regex patterns), and adherence to <code>nofollow</code> / <code>canonical</code> / <code>robots.txt</code> directives. The resulting data can be filtered and exported to CSV or Excel format, opening up countless avenues for exploration.

As a simple example, we’ll audit our on-page meta data. Actual content aside, a page’s <code>title</code> tag and <code>meta</code> description are <a href="https://support.google.com/webmasters/answer/35624">the two most important on-page factors</a> for modern SEO, so we’ll be looking to review these at scale.

Under <em>Configuration - Spider</em>, uncheck <em>Images, CSS, JavaScript, SWF</em>, and <em>External Links</em>. Then check <em>Crawl All Subdomains</em> to ensure that your entire domain is covered, and hit <em>OK</em>. Enter your domain in the <em>URL to spider</em> field, and hit <em>Start</em>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/857e51e8-0667-48b8-9475-0cf81e97f46a/09-screaming-frog-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/368abfa3-afca-49c4-982b-5e2529ffcee3/09-screaming-frog-opt-small.png" alt="The Screaming Frog SEO Spider crawling all URLs on a domain" /></a><figcaption>The Screaming Frog SEO Spider crawling all URLs on a domain. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/857e51e8-0667-48b8-9475-0cf81e97f46a/09-screaming-frog-opt.png">View large version</a>)</figcaption></figure>

The <em>Page Titles</em> and <em>Meta Descriptions</em> tabs will allow you to filter the crawl data by issue; in the case of <code>title</code> tags, these are categorised as missing, duplicate, too short, or overly-long. Hit <em>Export</em> to save the data to a spreadsheet for manual review later.

If you’ve never before run a crawl on your website, it’s almost a <em>guarantee</em> that something in the crawl results will surprise you. It could be an unexpected duplication problem, a legacy site section you’ve forgotten about, or a high priority page with no meta data whatsoever. This is why tools such as Screaming Frog can be so valuable - they provide insight into <em>how</em> crawlers are likely interacting with your website.

The <a href="https://www.screamingfrog.co.uk/seo-spider/user-guide/">official documentation</a> is very comprehensive, and Aichlee Bushnell wrote a great guide to advanced uses of the program for <a href="https://www.seerinteractive.com/blog/screaming-frog-guide/">Seer Interactive</a>.

A quick list of things to check for, most of which are inefficient from a crawl efficiency standpoint:

*   Temporary (code `302`) redirects, which do not pass value
*   Chained redirects - use the [redirect chains report](https://www.screamingfrog.co.uk/seo-spider/user-guide/general/#9) function
*   `404` error pages which are linked-to internally
*   Inconsistent internal linking - links to non-canonical URLs, for instance
*   Use of deprecated tags like `meta` keywords - these serve only to betray to competitors the keywords you are targeting!

## Link Profile Maintenance

Google’s rise to power in the late 1990s is partly attributable to its use of external links as a ranking factor.

Company co-founder Larry Page invented a technology called <em>PageRank</em>, a way of measuring a page’s quality based on the number of other websites - and, crucially, the <strong>authority</strong> of those other websites - linking to it. In practical terms, this means that a link to your website from the <a href="https://www.bbc.co.uk/">BBC</a> will have far more of an impact on your search rankings than a link from just about anywhere else.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6856322-a041-4a6a-9f9e-6658b56836fd/10-pagerank-example-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47ba0e9a-ad0c-44c3-a6fa-47a225359bc5/10-pagerank-example-opt-small.png" alt="A visualization of the PageRank algorithm" /></a><figcaption>A visualization of the PageRank algorithm. (Image credit: <a href="https://commons.wikimedia.org/wiki/File:PageRanks-Example.svg">Wikimedia Commons</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6856322-a041-4a6a-9f9e-6658b56836fd/10-pagerank-example-opt.png">View large version</a>)</figcaption></figure>

Google’s algorithm has evolved considerably in the years since its introduction, and today it incorporates dozens of metrics when determining how to rank a page. Nevertheless, <strong>external links remain the single most important factor for search rankings.</strong>

This has led to the messy saga of <a href="https://support.google.com/webmasters/answer/2604824">link spam and manual penalties</a>, in which unscrupulous SEO practitioners discover a link building tactic which they can abuse at scale before Google’s inevitable clampdown. The series of so-called ‘Penguin’ updates are essentially Google’s major offensives in this ongoing war of attrition, penalizing websites that benefit from paid links, link spam, and other breaches of Google’s guidelines.

As a result, SEO link audits will typically focus on <em>risks</em> - evidence of previous attempts to manipulate PageRank - rather than on <em>opportunities</em>. It is true that webmasters in certain highly-competitive industries such as gambling and pharmaceuticals <strong>need</strong> to be aware of the possible effects of link spam and negative SEO on their site’s rankings; in some cases, regular and proactive use of Google’s <a href="https://support.google.com/webmasters/answer/2648487">Disavow Tool</a> may even be necessary. These are extreme cases, however.

Link targeting, on the other hand, is relevant to <strong>all</strong> sites. By evaluating the health of a site’s link profile, it is possible to retain and reclaim <em>link equity</em> (the value which Google assigns to links) in a wide variety of ways.</p>

### Equity Loss

Think of <em>link equity</em> as a valuable liquid, and the links to your website as the pipes through which it is transported. A series of tubes, if you will. A normal link that points directly at a URL returning a <code>200 OK</code> HTTP response code - a live page - transfers this value to your website perfectly. A link to a dead page that returns a <code>404</code> or <code>503</code> error sends this value down the drain, and your site <strong>does not benefit at all.</strong>

A single code <code>301</code> redirect is like a funnel, in that it catches <em>most</em> of the equity from a link and diverts it on to the new destination. It does the job, but it’s an inherently leaky process and by avoiding redirect chains you can prevent the losses from compounding.

A code <code>302</code> redirect is like a sieve. Although humans clicking on the link are caught and sent safely on to the correct destination, all the valuable equity is wasted. Links (or redirects) to pages blocked in your <code>robots.txt</code> file are similarly inefficient; humans won’t notice, but the equity is prevented from reaching your site. We’ll avoid stretching the analogy further, but you should also avoid redirect loops and soft <code>404</code> pages.

There are a handful of other factors to consider before we start fixing leaks. First of all, <strong>each subdomain has its own reserves of link equity</strong>. Despite some claims to the contrary, search engines still view <code>forum.yourdomain.com</code> and <code>www.yourdomain.com</code> as different websites, and links to one <em>will not benefit the other</em>. This is why blogs hosted on an external service such as Tumblr (<code>yourblog.tumblr.com</code>) do not inherit the authority of their root domain. For this reason, it is almost always worth the effort to install site components (forums, blogs, and so forth) in subfolders on your main domain.

Furthermore, it is possible to prevent equity from flowing through specific links by using the <a href="https://support.google.com/webmasters/answer/96569">nofollow attribute</a>. This can be applied at a page level by using the robots <code>meta</code> tag we <a href="#blocked-content">discussed in Section 1.2</a>, which instructs spiders not to crawl the page’s links or to attribute value to them. It is also possible to apply this property to a specific link by setting <code>nofollow</code> as the value for the <code>rel</code> attribute: <code>&lt;a href="/" rel="nofollow"&gt;</code>.

Finally, the impact of the problems described above will be much worse for <em>old websites</em> and <em>big websites</em>. The side effects of historic migrations, rebrands, URL restructures, and internationalisation can become compounded over time. Thankfully, the cost to implement the necessary fixes stays relatively low, while the rewards in organic performance can often be remarkable.</p>

### Fixing Leaks

To identify and fix these problems we’ll need a list of <strong>all links to our website.</strong> There are a number of services that attempt to provide this, with two of the best being <a href="https://majestic.com/">Majestic</a> and <a href="https://ahrefs.com/">Ahrefs</a>. For the purposes of this guide, we’ll focus on the latter.

We’ll need to generate a raw export of our root domain’s link profile. Having entered the domain into the Ahrefs Site Explorer, hit <em>Export</em> - <em>CSV</em>. Download a <em>Backlinks/Ref pages</em> report in the encoding format of your choice (UTF–8 for Libre Office Calc, UTF–16 for Microsoft Excel).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fdd1cf3-a0eb-4d01-a0ed-586403cb734d/11-ahrefs-export-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b23ae9-9423-4dfc-975e-bb79a1bd9335/11-ahrefs-export-opt-small.png" alt="Ahrefs Raw Export" /></a><figcaption>The Ahrefs Raw Export function, <a href="https://ahrefs.com/">Ahrefs.com</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fdd1cf3-a0eb-4d01-a0ed-586403cb734d/11-ahrefs-export-opt.png">View large version</a>)</figcaption></figure>

Use a spider such as <a href="https://www.screamingfrog.co.uk/seo-spider/">Screaming Frog</a> or the free <a href="https://seotoolsforexcel.com/">SEO Tools for Excel</a> to crawl the target URLs of your links. If you’re using Screaming Frog, make sure that your spider is configured to always follow redirects (no matter how long the chain!), and to ignore <code>robots.txt</code> disallow rules. Make use of the <a href="https://www.screamingfrog.co.uk/seo-spider/user-guide/general/#9">redirect chains report</a> to export the full crawl path for each URL.

With the required data to hand, what exactly are we looking for? <a href="https://ohgm.co.uk/">Oliver Mason</a> wrote an excellent guide <a href="https://builtvisible.com/link-equity-and-crawl-efficiency-maintenance/">for Builtvisible</a> on this very subject:
<blockquote>“What we are trying to do is ensure that Googlebot can crawl unhindered from external link to canonical page in as few steps as possible. To do this, we look for anything that interrupts crawl or link equity.

Think about general guidelines for migrations and URL structures – they tend towards ‘make sure current structure is redirected to the new structure in a single hop’. This is fine in isolation, but every time new recommendations are put in place without consideration of past migrations, you’re guaranteeing link equity loss. Very often you’ll find that a number of structural changes have happened in the past without being handled quite correctly, leading to an abundance of inefficiencies.”</blockquote>

If you’ve made it this far, you should be able to guess the necessary fixes. Excluding the possibility of manual realignment (i.e. asking webmasters to update their outbound links to your website), you should look to address specific issues as follows:

*   To reclaim the value of links to `404` or `503` pages, implement permanent redirects to the most closely related live pages.
*   Update code `302` temporary redirects to code `301` permanent redirects.
*   If resources blocked in `robots.txt` have accrued links, either create an `Allow` exception or redirect the URLs to an unblocked page.
*   Remove all intermediate steps from redirect chains, ensuring that the path from external link to canonical page consists of no more than **one permanent redirect**.

If you’re dealing with a large website and have limited development resource, you can prioritise problematic URLs by the number of linking root domains pointing at them. Remember too that fixing instances of complete equity waste (e.g. redirecting a once-popular URL which is now returning a <code>404</code>) will likely have bigger impact than fixing minor inefficiencies.</p>

### Harnessing Your History

Finally, consider the domain history of your website. If it has ever undergone a major migration or rebrand which involved changing root domain - moving from a <code>.co.uk</code> to a <code>.com</code>, for example - it’s worth checking that the process was carried out properly. Consult the <a href="https://support.google.com/webmasters/answer/6033049">Google Support guidelines</a> on proper execution of a site move.

You’ll need to repeat the steps above for each domain property associated with your brand in order to ensure that each old page is properly redirecting to its corresponding new version. You’ll also want to submit a <a href="https://support.google.com/webmasters/answer/83106"><em>Change of Address</em> request</a> through Google Search Console.

Note that this needs to be done <em>after</em> redirects have been implemented, and will require you to verify ownership of both the old and the new domains. For particularly old properties, this will probably have to be done using a <a href="https://support.google.com/webmasters/answer/176792">DNS TXT record</a>. This may seem like an inordinate amount of effort, but the potential gain in organic performance is considerable.</p>

<strong>Preservation and reclamation of link value</strong> is key to the reason why any kind of migration or restructure must be overseen by an experienced [technical SEO consultant](https://www.derekiwasiuk.com/technical-seo-audit/). This is especially true for e-commerce websites that rely to any degree on organic acquisition for their revenue stream. Careful planning and comprehensive redirect mapping must be carried out in advance to ensure that organic rankings remain as stable as possible.</p>

## The Tip of the Technical SEO Iceberg

As this article has hopefully demonstrated, technical SEO is an extraordinarily rich discipline.

The principles and techniques we’ve explored are a good set of best practices, but - as with all areas of web development - there are exceptions to every rule. Tackling a migration for a huge e-commerce website running on an idiosyncratic CMS with a million pages, a separate mobile site, a faceted navigation system, and a colourful history of architectural changes and rebrands requires a different level of understanding.

For readers wishing to dive into advanced technical SEO, <strong>log file analysis</strong> is a great place to start. For particularly complex websites, adherence to guidelines can only take you so far; true organic optimisation requires an understanding of precisely <em>how</em> Googlebot and Bingbot are interacting with your site. By exporting raw server logs for analysis, it’s possible to ‘see’ each and every request made by search engine robots. This data allows us to determine the frequency, depth, and breadth of crawl behaviour, and reveals obstructions which may go unnoticed by even the most experienced SEO experts. I would strongly recommend <a href="https://builtvisible.com/log-file-analysis/">Daniel Butler’s guide</a> to anyone wishing to explore the possibilities of log file analysis.

What we’ve explored today is just the <strong>tip of the iceberg</strong>. Even websites that are technically well-optimised stand to benefit from a greater consideration of the possibilities of organic search.</p>

<pre><code>RewriteEngine on
RewriteCond %{HTTP_HOST} ^yourdomain.com [NC]
RewriteRule ^(.*)$ https://www.yourdomain.com/$1 [L,R=301]
</code></pre>

Once again, consult the <a href="https://httpd.apache.org/docs/2.4/rewrite/remapping.html">Apache documentation</a> for more detailed guidelines. There is also documentation available for the corresponding modules in <a href="https://nginx.org/en/docs/http/ngx_http_rewrite_module.html">Nginx</a> and <a href="https://www.iis.net/learn/extensions/url-rewrite-module/using-the-url-rewrite-module">IIS</a>.

The relevance of URL rewrites to SEO goes beyond simple fixes. Crucially, it allows us to make resources available over HTTP at URLs which <strong>do not necessarily correspond to their locations in the file system</strong>. This allows us to implement a static, human-readable URL structure which reflects our logical, IA-compliant site architecture.

*   Original: `https://www.yourdomain.com/content/catID/43/prod.html?p=XjqG`
*   Rewritten: `https://www.yourdomain.com/category/product/`

The benefits of a clean URL structure in SEO cannot be overstated. In addition to providing an increase in crawl efficiency, a good implementation offers a huge usability advantage. Remember that the URL is one of the most prominent elements considered by searchers when deciding on which URL to click.

Given the sheer number of possible tech stacks, the methodology can vary greatly, but you can find a general summary of <a href="https://support.google.com/webmasters/answer/76329">URL best practices at Google</a>, and a helpful introduction to advanced rewrite conditions <a href="https://www.linode.com/docs/websites/apache-tips-and-tricks/rewrite-urls-with-modrewrite-and-apache/">at Linode.com</a>.

One final word on redirects: avoid chains where at all possible. Not only are they inefficient from a crawl efficiency standpoint, the amount of ‘value’ passed by a <code>301</code> (permanent) redirect diminishes with each sequential hop. Your goal should be to direct all variants and retired pages to the correct URL with a single permanent redirect. See <a href="#link-profile">Section 3</a> for more information on the concept of link value preservation.</p>

### The Canonical Tag

In situations where server-side redirection is impossible or inappropriate, there is another fix available to us: the <code>rel="canonical"</code> link element.</p>

<a href="https://googlewebmastercentral.blogspot.co.uk/2009/02/specify-your-canonical.html">First introduced in 2009</a> as part of a collaborative effort by Google, Bing, and Yahoo, the tag allows us to indicate to search engines the preferred URL for a page. Usage is simple: add a <code>link</code> element with the <code>rel="canonical"</code> attribute to the <code>head</code> section of the ‘true’ page and all its variants.

To use a simple homepage example:

*   `https://www.yourdomain.com`
*   `https://www.yourdomain.com/index.html`
*   `https://www.yourdomain.com?sessionid=1988`

Marking <strong>each</strong> of these with the following tag would indicate to search engines which version to show users:

<pre><code class="language-markup">&lt;link rel="canonical" href="https://www.yourdomain.com"&gt;
</code></pre>

Unlike a redirect, the canonical tag does not affect the URL shown in the user’s address bar. Instead, it is simply a hint to search engines to treat particular variants as a single page. <strong>Be sure that the URLs in your canonical tags are correct</strong>; canonicalizing your entire site to a single page or implementing canonicals that point at <code>404</code> errors can be disastrous.

Note that in <em>most</em> instances server-side redirection is a more robust and user-friendly way of addressing major duplication problems. If you are in a position to control a site’s architecture, it’s generally possible to avoid many of the scenarios that require canonical tags as a fix.

That being said, there are advantages to including self-referencing canonical tags on every page. When implemented correctly, they make a good first line of defence against unforeseen problems. If your site uses parameters to identify specific user comments (<code>…?comment=13</code>, for example), the canonical tag can ensure that links to these URLs do not lead to the indexation of duplicate pages.

When dealing with duplicate content, you should always look to address the <strong>root cause of the problem</strong> rather than using a proprietary solution. For this reason, disabling a problematic parameter and handling its function via a cookie is often a preferable solution to <a href="https://googlewebmastercentral.blogspot.co.uk/2011/07/improved-handling-of-urls-with.html">blocking the parameter</a> in a vendor-specific program like Google Search Console or Bing Webmaster Central. For a more detailed look into duplicate content and the approaches to tackling it, take a read of <a href="https://moz.com/blog/duplicate-content-in-a-post-panda-world">Dr. Pete Meyers’ article on Moz.com</a>.</p>

### Multi-regional & Multilingual

Websites that target more than one language or country can be particularly challenging from a search standpoint, given that such sites inherantly require multiplication of content. International SEO is an <em>extremely</em> broad subject that warrants an entire article to itself, and for this reason we will touch only on the basic principles here.

The structure of a multi-regional or multilingual website is worthy of careful consideration. Google’s own <a href="https://support.google.com/webmasters/answer/182192">guidelines on internationalisation</a> are a good starting point. There are dozens of factors to consider before opting for separate ccTLDs, subdomains, or subdirectories, and it is essential to consider the future of your site and plan implementation as thoroughly as possible before deployment.

Whichever route you choose, the <code>rel="alternate" hreflang="x"</code> attributes should be used to indicate to search engines the appropriate page to return to users searching in a particular language. These attributes are a <em>signal</em>, not a directive, and so other factors (server IP address or geotargeting settings in Search Console, for example) can override them.

Your <code>hreflang</code> annotations can be served via an HTTP header, by <a href="https://support.google.com/webmasters/answer/2620865">marking up your sitemaps</a>, or by using <code>link</code> elements in the <code>head</code> of your pages. The syntax for the latter implementation is as follows:

<pre><code class="language-markup">
&lt;link rel="alternate" href="https://yourdomain.com/en" hreflang="en"&gt;
&lt;link rel="alternate" href="https://yourdomain.com/de" hreflang="de"&gt;
&lt;link rel="alternate" href="https://yourdomain.com/fr" hreflang="fr"&gt;
&lt;link rel="alternate" href="https://yourdomain.com/fr-ca" hreflang="fr-ca"&gt;</code></pre>

The value of the <code>hreflang</code> attribute specifies the language in <a href="https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes">ISO 639-1</a> format, and (optionally) the region in <a href="https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2">ISO 3166-1 Alpha 2</a> format. In the example above, four versions of our homepage are specified: English, German, French (all non-region-specific), and finally French content localized for users in Canada. Each version of a page <strong>must identify every translated version, including itself</strong>. In other words, the above code block would be repeated on all four versions of our homepage. Finally, note that Google recommends <em>not</em> canonicalizing across different international page versions; instead, use the <code>canonical</code> tag only within the same version.

Internationalization can be notoriously complex, and as such it’s worth experimenting with tools such as Aleyda Solis’s <a href="https://www.internationalseomap.com/hreflang-tags-generator/">Hreflang Tags Generator Tool</a> and reading <a href="https://support.google.com/webmasters/answer/189077">Google’s documentation</a> in its entirety before even considering making changes to your website.

Finally, while we’re on the subject of region-specific content, it’s worth noting that SEO for local businesses carries with it a raft of additional opportunities. <a href="https://searchengineland.com/local-seo-rank-local-business-218906">Matthew Barby’s primer</a> on the subject for Search Engine Land is a good place to start.</p>

### Maintenance & Best Practices

In this section, we’ll be covering general best practices and housekeeping for SEO. This includes auditing your <strong>on-page meta data</strong> - titles, descriptions, headings, and so forth - and also checking for <strong>common internal issues</strong> which are easily overlooked.

In tandem with <a href="https://www.google.com/webmasters/tools/home">Google Search Console</a> or <a href="https://www.bing.com/toolbox/webmaster">Bing Webmaster Central</a>, the most useful tool available for everyday on-site SEO is a <em>simulated</em> search crawler. This is a piece of software that can be used to crawl your website in a manner similar to that of a search robot. The <a href="https://home.snafu.de/tilman/xenulink.html">Xenu Link Sleuth</a> is a good freeware option, but for serious work you cannot beat the <a href="https://www.screamingfrog.co.uk/seo-spider/">Screaming Frog SEO Spider</a>.

‘The Frog’, as it is affectionately dubbed, is fully configurable in terms of user agent, speed, crawl directory &amp; depth (including by regex patterns), and adherence to <code>nofollow</code> / <code>canonical</code> / <code>robots.txt</code> directives. The resulting data can be filtered and exported to CSV or Excel format, opening up countless avenues for exploration.

As a simple example, we’ll audit our on-page meta data. Actual content aside, a page’s <code>title</code> tag and <code>meta</code> description are <a href="https://support.google.com/webmasters/answer/35624">the two most important on-page factors</a> for modern SEO, so we’ll be looking to review these at scale.

Under <em>Configuration - Spider</em>, uncheck <em>Images, CSS, JavaScript, SWF</em>, and <em>External Links</em>. Then check <em>Crawl All Subdomains</em> to ensure that your entire domain is covered, and hit <em>OK</em>. Enter your domain in the <em>URL to spider</em> field, and hit <em>Start</em>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/857e51e8-0667-48b8-9475-0cf81e97f46a/09-screaming-frog-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/368abfa3-afca-49c4-982b-5e2529ffcee3/09-screaming-frog-opt-small.png" alt="The Screaming Frog SEO Spider crawling all URLs on a domain" /></a><figcaption>The Screaming Frog SEO Spider crawling all URLs on a domain. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/857e51e8-0667-48b8-9475-0cf81e97f46a/09-screaming-frog-opt.png">View large version</a>)</figcaption></figure>

The <em>Page Titles</em> and <em>Meta Descriptions</em> tabs will allow you to filter the crawl data by issue; in the case of <code>title</code> tags, these are categorised as missing, duplicate, too short, or overly-long. Hit <em>Export</em> to save the data to a spreadsheet for manual review later.

If you’ve never before run a crawl on your website, it’s almost a <em>guarantee</em> that something in the crawl results will surprise you. It could be an unexpected duplication problem, a legacy site section you’ve forgotten about, or a high priority page with no meta data whatsoever. This is why tools such as Screaming Frog can be so valuable - they provide insight into <em>how</em> crawlers are likely interacting with your website.

The <a href="https://www.screamingfrog.co.uk/seo-spider/user-guide/">official documentation</a> is very comprehensive, and Aichlee Bushnell wrote a great guide to advanced uses of the program for <a href="https://www.seerinteractive.com/blog/screaming-frog-guide/">Seer Interactive</a>.

A quick list of things to check for, most of which are inefficient from a crawl efficiency standpoint:

*   Temporary (code `302`) redirects, which do not pass value
*   Chained redirects - use the [redirect chains report](https://www.screamingfrog.co.uk/seo-spider/user-guide/general/#9) function
*   `404` error pages which are linked-to internally
*   Inconsistent internal linking - links to non-canonical URLs, for instance
*   Use of deprecated tags like `meta` keywords - these serve only to betray to competitors the keywords you are targeting!

## Link Profile Maintenance

Google’s rise to power in the late 1990s is partly attributable to its use of external links as a ranking factor.

Company co-founder Larry Page invented a technology called <em>PageRank</em>, a way of measuring a page’s quality based on the number of other websites - and, crucially, the <strong>authority</strong> of those other websites - linking to it. In practical terms, this means that a link to your website from the <a href="https://www.bbc.co.uk/">BBC</a> will have far more of an impact on your search rankings than a link from just about anywhere else.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6856322-a041-4a6a-9f9e-6658b56836fd/10-pagerank-example-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47ba0e9a-ad0c-44c3-a6fa-47a225359bc5/10-pagerank-example-opt-small.png" alt="A visualization of the PageRank algorithm" /></a><figcaption>A visualization of the PageRank algorithm. (Image credit: <a href="https://commons.wikimedia.org/wiki/File:PageRanks-Example.svg">Wikimedia Commons</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6856322-a041-4a6a-9f9e-6658b56836fd/10-pagerank-example-opt.png">View large version</a>)</figcaption></figure>

Google’s algorithm has evolved considerably in the years since its introduction, and today it incorporates dozens of metrics when determining how to rank a page. Nevertheless, <strong>external links remain the single most important factor for search rankings.</strong>

This has led to the messy saga of <a href="https://support.google.com/webmasters/answer/2604824">link spam and manual penalties</a>, in which unscrupulous SEO practitioners discover a link building tactic which they can abuse at scale before Google’s inevitable clampdown. The series of so-called ‘Penguin’ updates are essentially Google’s major offensives in this ongoing war of attrition, penalizing websites that benefit from paid links, link spam, and other breaches of Google’s guidelines.

As a result, SEO link audits will typically focus on <em>risks</em> - evidence of previous attempts to manipulate PageRank - rather than on <em>opportunities</em>. It is true that webmasters in certain highly-competitive industries such as gambling and pharmaceuticals <strong>need</strong> to be aware of the possible effects of link spam and negative SEO on their site’s rankings; in some cases, regular and proactive use of Google’s <a href="https://support.google.com/webmasters/answer/2648487">Disavow Tool</a> may even be necessary. These are extreme cases, however.

Link targeting, on the other hand, is relevant to <strong>all</strong> sites. By evaluating the health of a site’s link profile, it is possible to retain and reclaim <em>link equity</em> (the value which Google assigns to links) in a wide variety of ways.</p>

### Equity Loss

Think of <em>link equity</em> as a valuable liquid, and the links to your website as the pipes through which it is transported. A series of tubes, if you will. A normal link that points directly at a URL returning a <code>200 OK</code> HTTP response code - a live page - transfers this value to your website perfectly. A link to a dead page that returns a <code>404</code> or <code>503</code> error sends this value down the drain, and your site <strong>does not benefit at all.</strong>

A single code <code>301</code> redirect is like a funnel, in that it catches <em>most</em> of the equity from a link and diverts it on to the new destination. It does the job, but it’s an inherently leaky process and by avoiding redirect chains you can prevent the losses from compounding.

A code <code>302</code> redirect is like a sieve. Although humans clicking on the link are caught and sent safely on to the correct destination, all the valuable equity is wasted. Links (or redirects) to pages blocked in your <code>robots.txt</code> file are similarly inefficient; humans won’t notice, but the equity is prevented from reaching your site. We’ll avoid stretching the analogy further, but you should also avoid redirect loops and soft <code>404</code> pages.

There are a handful of other factors to consider before we start fixing leaks. First of all, <strong>each subdomain has its own reserves of link equity</strong>. Despite some claims to the contrary, search engines still view <code>forum.yourdomain.com</code> and <code>www.yourdomain.com</code> as different websites, and links to one <em>will not benefit the other</em>. This is why blogs hosted on an external service such as Tumblr (<code>yourblog.tumblr.com</code>) do not inherit the authority of their root domain. For this reason, it is almost always worth the effort to install site components (forums, blogs, and so forth) in subfolders on your main domain.

Furthermore, it is possible to prevent equity from flowing through specific links by using the <a href="https://support.google.com/webmasters/answer/96569">nofollow attribute</a>. This can be applied at a page level by using the robots <code>meta</code> tag we <a href="#blocked-content">discussed in Section 1.2</a>, which instructs spiders not to crawl the page’s links or to attribute value to them. It is also possible to apply this property to a specific link by setting <code>nofollow</code> as the value for the <code>rel</code> attribute: <code>&lt;a href="/" rel="nofollow"&gt;</code>.

Finally, the impact of the problems described above will be much worse for <em>old websites</em> and <em>big websites</em>. The side effects of historic migrations, rebrands, URL restructures, and internationalisation can become compounded over time. Thankfully, the cost to implement the necessary fixes stays relatively low, while the rewards in organic performance can often be remarkable.</p>

### Fixing Leaks

To identify and fix these problems we’ll need a list of <strong>all links to our website.</strong> There are a number of services that attempt to provide this, with two of the best being <a href="https://majestic.com/">Majestic</a> and <a href="https://ahrefs.com/">Ahrefs</a>. For the purposes of this guide, we’ll focus on the latter.

We’ll need to generate a raw export of our root domain’s link profile. Having entered the domain into the Ahrefs Site Explorer, hit <em>Export</em> - <em>CSV</em>. Download a <em>Backlinks/Ref pages</em> report in the encoding format of your choice (UTF–8 for Libre Office Calc, UTF–16 for Microsoft Excel).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fdd1cf3-a0eb-4d01-a0ed-586403cb734d/11-ahrefs-export-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60b23ae9-9423-4dfc-975e-bb79a1bd9335/11-ahrefs-export-opt-small.png" alt="Ahrefs Raw Export" /></a><figcaption>The Ahrefs Raw Export function, <a href="https://ahrefs.com/">Ahrefs.com</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fdd1cf3-a0eb-4d01-a0ed-586403cb734d/11-ahrefs-export-opt.png">View large version</a>)</figcaption></figure>

Use a spider such as <a href="https://www.screamingfrog.co.uk/seo-spider/">Screaming Frog</a> or the free <a href="https://seotoolsforexcel.com/">SEO Tools for Excel</a> to crawl the target URLs of your links. If you’re using Screaming Frog, make sure that your spider is configured to always follow redirects (no matter how long the chain!), and to ignore <code>robots.txt</code> disallow rules. Make use of the <a href="https://www.screamingfrog.co.uk/seo-spider/user-guide/general/#9">redirect chains report</a> to export the full crawl path for each URL.

With the required data to hand, what exactly are we looking for? <a href="https://ohgm.co.uk/">Oliver Mason</a> wrote an excellent guide <a href="https://builtvisible.com/link-equity-and-crawl-efficiency-maintenance/">for Builtvisible</a> on this very subject:
<blockquote>“What we are trying to do is ensure that Googlebot can crawl unhindered from external link to canonical page in as few steps as possible. To do this, we look for anything that interrupts crawl or link equity.

Think about general guidelines for migrations and URL structures – they tend towards ‘make sure current structure is redirected to the new structure in a single hop’. This is fine in isolation, but every time new recommendations are put in place without consideration of past migrations, you’re guaranteeing link equity loss. Very often you’ll find that a number of structural changes have happened in the past without being handled quite correctly, leading to an abundance of inefficiencies.”</blockquote>

If you’ve made it this far, you should be able to guess the necessary fixes. Excluding the possibility of manual realignment (i.e. asking webmasters to update their outbound links to your website), you should look to address specific issues as follows:

*   To reclaim the value of links to `404` or `503` pages, implement permanent redirects to the most closely related live pages.
*   Update code `302` temporary redirects to code `301` permanent redirects.
*   If resources blocked in `robots.txt` have accrued links, either create an `Allow` exception or redirect the URLs to an unblocked page.
*   Remove all intermediate steps from redirect chains, ensuring that the path from external link to canonical page consists of no more than **one permanent redirect**.

If you’re dealing with a large website and have limited development resource, you can prioritise problematic URLs by the number of linking root domains pointing at them. Remember too that fixing instances of complete equity waste (e.g. redirecting a once-popular URL which is now returning a <code>404</code>) will likely have bigger impact than fixing minor inefficiencies.</p>

### Harnessing Your History

Finally, consider the domain history of your website. If it has ever undergone a major migration or rebrand which involved changing root domain - moving from a <code>.co.uk</code> to a <code>.com</code>, for example - it’s worth checking that the process was carried out properly. Consult the <a href="https://support.google.com/webmasters/answer/6033049">Google Support guidelines</a> on proper execution of a site move.

You’ll need to repeat the steps above for each domain property associated with your brand in order to ensure that each old page is properly redirecting to its corresponding new version. You’ll also want to submit a <a href="https://support.google.com/webmasters/answer/83106"><em>Change of Address</em> request</a> through Google Search Console.

Note that this needs to be done <em>after</em> redirects have been implemented, and will require you to verify ownership of both the old and the new domains. For particularly old properties, this will probably have to be done using a <a href="https://support.google.com/webmasters/answer/176792">DNS TXT record</a>. This may seem like an inordinate amount of effort, but the potential gain in organic performance is considerable.</p>

<strong>Preservation and reclamation of link value</strong> is key to the reason why any kind of migration or restructure must be overseen by an experienced technical SEO consultant. This is especially true for e-commerce websites that rely to any degree on organic acquisition for their revenue stream. Careful planning and comprehensive redirect mapping must be carried out in advance to ensure that organic rankings remain as stable as possible.</p>

## The Tip of the Technical SEO Iceberg

As this article has hopefully demonstrated, technical SEO is an extraordinarily rich discipline.

The principles and techniques we’ve explored are a good set of best practices, but - as with all areas of web development - there are exceptions to every rule. Tackling a migration for a huge e-commerce website running on an idiosyncratic CMS with a million pages, a separate mobile site, a faceted navigation system, and a colourful history of architectural changes and rebrands requires a different level of understanding.

For readers wishing to dive into advanced technical SEO, <strong>log file analysis</strong> is a great place to start. For particularly complex websites, adherence to guidelines can only take you so far; true organic optimisation requires an understanding of precisely <em>how</em> Googlebot and Bingbot are interacting with your site. By exporting raw server logs for analysis, it’s possible to ‘see’ each and every request made by search engine robots. This data allows us to determine the frequency, depth, and breadth of crawl behaviour, and reveals obstructions which may go unnoticed by even the most experienced SEO experts. I would strongly recommend <a href="https://builtvisible.com/log-file-analysis/">Daniel Butler’s guide</a> to anyone wishing to explore the possibilities of log file analysis.

What we’ve explored today is just the <strong>tip of the iceberg</strong>. Even websites that are technically well-optimised stand to benefit from a greater consideration of the possibilities of organic search.

Much as <a href="https://moz.com/blog/meta-data-templates-123">social media meta tags</a> can enrich the potential of your content on Facebook, Twitter, and Pinterest, <a href="https://developers.google.com/structured-data/">structured data markup</a> allows us to annotate our content for machine interpretation and enables search engines like Google and Bing to generate so-called <em>rich-snippets</em>. The <a href="https://schema.org/">Schema.org</a> vocabulary and JSON-LD format are opening up a whole new frontier of possibilities, and allow an increasingly complex array of <em>actions</em> to be invoked directly from the search results themselves. This will have to wait for another day.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/112ccaf2-e0cd-4dc5-9339-bb2805ada546/12-rich-serp-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/193e00da-7c84-4e4e-96e8-21c10d98a126/12-rich-serp-opt-small.png" alt="Rich Snippets, a great opportunity to stand out in organic search" /></a><figcaption>“Rich Snippets” - A great opportunity to stand out in organic search. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/112ccaf2-e0cd-4dc5-9339-bb2805ada546/12-rich-serp-opt.png">View large version</a>)</figcaption></figure>

My primary goal in writing this article was to introduce fellow web developers to the principles of modern <em>search engine optimisation</em>. If I’ve succeeded in dispelling any of the myths that surround this subject, even better.</p>

<strong>SEO is not a dark art, nor is it dying</strong>; much like site speed and mobile-friendliness, it is simply one of the many ways in which we will make a better, richer, and more discoverable web.</p>

<em>Special thanks to <a href="https://ohgm.co.uk/">Oliver Mason</a> for his invaluable suggestions and advice while this article was being written.</em>

{{< signature "ml, rb, al, jb" >}}


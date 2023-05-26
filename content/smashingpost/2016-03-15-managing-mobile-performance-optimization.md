---
title: How To Optimize Mobile Performance
slug: managing-mobile-performance-optimization
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/951dd491-9069-4bc9-8453-12e7928b3209/01-cdmobile-500-opt.jpg
date: 2016-03-15T17:33:40.000Z
author: danny-bluestone
summary: >-
  You can’t underestimate the importance of consistent, high-quality web design across devices of all shapes and sizes. Responsive web design is the way forward &mdash; but it’s often linked to performance issues. This is critical when 64% of smartphone users unforgivingly expect websites to load in <a href="https://www.businesswire.com/news/home/20120806005374/en/Smartphone-Tablet-Users-Frustrated-Slooow-Mobile-Web#.VQMa_YGsXuV">under four seconds</a>, yet <a href="https://www.sitepoint.com/average-page-weight-increases-15-2014/">average page weights</a> continue to rise.
description: >-
  You can’t underestimate the importance of consistent, high-quality web design across devices of all shapes and sizes. Responsive web design is the way forward &mdash; but it’s often linked to performance issues. This is critical when 64% of smartphone users unforgivingly expect websites to load in <a href="https://www.businesswire.com/news/home/20120806005374/en/Smartphone-Tablet-Users-Frustrated-Slooow-Mobile-Web#.VQMa_YGsXuV">under four seconds</a>, yet <a href="https://www.sitepoint.com/average-page-weight-increases-15-2014/">average page weights</a> continue to rise.
categories:
  - Mobile
  - Optimization
  - Performance
---

The best designs balance aesthetics and performance by working with mobile in mind from the start. From setting strict performance budgets to implementing client- and server-side optimization techniques, I’ll share the current mobile performance optimization processes we use at <em>Cyber-Duck</em>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b31f8dc6-f9b2-44e9-9a84-dc6cae55b742/01-cdmobile-opt.jpg"><img loading="lazy" decoding="async" title="Cyber-Duck website on mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/951dd491-9069-4bc9-8453-12e7928b3209/01-cdmobile-500-opt.jpg" alt="Mobile Performance " width="500" height="332" /></a><figcaption>Designing with mobile in mind from the start helps balance website aesthetics and performance across devices. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b31f8dc6-f9b2-44e9-9a84-dc6cae55b742/01-cdmobile-opt.jpg">Large preview</a>)</figcaption></figure>

## Become Mobile-Minded

Performance is a key part of the user experience, so it can’t be an afterthought at the end of the development process. It’s preferable to <strong>manage projects through a mobile-minded structure</strong>, with designers and developers collaborating from the start.

### Collaborative Review

For each project, review the design and development scope with the internal team, and define key performance indicator (KPI) goals. These are the milestone metrics that indicate project success, based on business objectives. Given their importance, performance-related goals should appear here.

Don’t sign off significant project milestones (like the art direction and wireframes) with stakeholders until the entire internal team has reviewed the output. Otherwise, we’ve found developers can request design adjustments (to reduce page size) during implementation. With designs already signed off, changes at this stage can create complications, opening further rounds of client approvals. When developers are involved from the outset, they can estimate the size and programming power required for interfaces, and avoid this.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae7b3bb4-ce99-4fca-920c-7ccadadecd3c/02-cdmeeting-opt.jpg"><img title="Cyber-Duck team meeting" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9f7e0b7-a301-4f66-9892-8fd4d99750ab/02-cdmeeting-500-opt.jpg" alt="Cyber-Duck team meeting" /></a><figcaption>Designers and developers should review key milestones together, evaluating potential performance before sending for approval. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae7b3bb4-ce99-4fca-920c-7ccadadecd3c/02-cdmeeting-opt.jpg">Large preview</a>)</figcaption></figure>

### Performance Budgets

The best way to get into the mobile mind-set is <strong>setting and adhering to a strict performance budget</strong>: establishing a target for the final website’s speed and size. When the team is working towards a clear high-performance goal, they must choose whether to implement expensive features like carousels.

Specific business goals and user requirements determine whether we set figure-based performance budgets. For instance, <a href="https://www.smashingmagazine.com/2013/06/18/adapting-to-a-responsive-design-case-study/"> our own website revamp</a> aimed to dramatically improve load times across devices, and drive up mobile conversions. We set strict limits of no more than 40 HTTP requests or 500KB of data for mobile. Google Analytics data can inform which goals to select during revamps, as historical interactions indicate the behavior of your target audience.

Generally we define targets for page size, with a 500KB limit for mobile homepages. Server requests are more difficult to predict, so we’re less likely to set exact figures. These rough guidelines suit our needs for client projects. But <a href="https://danielmall.com/articles/how-to-make-a-performance-budget/">Daniel Mall</a> has a great practical guide for adding detail to budgets: from allocating weight for HTML and CSS, to JavaScript, images and web fonts.

{{% feature-panel %}}

## Optimization Techniques

On mobile, website loading speed is driven by client- and server-side factors. Using targeted optimization techniques that address both of these factors can help you meet the performance budgets set for your project.

## Client-Side Optimization

With a varied mobile landscape – <a href="https://www.thedrum.com/news/2014/11/25/consumers-using-over-5000-unique-devices-access-web-netbiscuits-finds">over 5,000 unique smartphone devices</a> in 2014 - developers have significantly less control over individual device performance than server-side factors. So, client-side optimization is crucial. The following techniques aim to reduce the processing time and power required from mobile devices to load websites.

### Optimize Code

Many developers fall into the trap of writing in jQuery to power a website. But there is no such thing. In fact, you are writing in JavaScript, while using a library of helpful shortcuts and functions. Although this speeds up development – useful, when you need to get a product to market quickly – there can be a performance cost. The jQuery library adds weight, and the flexibility of plugins (and functions) means they can often be bloated.

Here’s an example, with JavaScript and jQuery used for the same function. Writing in plain JavaScript avoids pulling another external library into your application, and will save another precious HTTP request.

<pre><code class="language-javascript">// jQuery
var con = $('#my_container');
con.css('width','75%');

// Plain JavaScript
var con = document.getElementById('my_container');
el.style.width = '75%';</code></pre>

You can optimize CSS and JS files further by using systems like <a href="https://gruntjs.com/">Grunt</a> or <a href="https://gulpjs.com/">Gulp</a>, or with front-end compiler apps like <a href="https://prepros.io/">Prepos</a>, <a href="https://incident57.com/codekit/">Codekit</a> or <a href="https://hammerformac.com/">Hammer</a>. These reduce HTTP requests and file size by performing a variety of tasks: concatenating files, compiling Sass, Less or <a href="https://coffeescript.org/">CoffeeScript</a>, <a href="https://github.com/mishoo/UglifyJS">Uglify JS</a> (compresses JavaScript), and minify/compressing files for production use.

### Prioritize Above The Fold

<a href="https://developers.google.com/speed/docs/insights/PrioritizeVisibleContent#structure">Google Pagespeed Insights</a> (and similar tools) recommends prioritizing the loading size and speed of content above the fold. Separate the CSS used to render the visible part of the page (above the fold) first; defer the rest of the styles to load after the page has been rendered.

Adding the top CSS directly into the page header can do this. But, bear in mind this will not be cached like the rest of the CSS file, so must be restricted to key content. A variety of tools can help you determine the CSS to separate, including Scott Jehl’s <a href="https://gist.github.com/scottjehl/b6129da04733e4e0f9a4">Critical CSS</a> and Paul Kinlam’s <a href="https://gist.github.com/PaulKinlan/6284142">Bookmarklet</a> tool.

### Optimize Images

Considering the current preference for rich design, it’s unfortunate that images are often the culprit of heavy page size. But image-led design is still possible if each is optimized and compressed before and after export to the right format. Always ensure you use the appropriate image type. Heavy colored photos work better as JPEG files, whereas flat color graphics should be in PNG8. Gradients and more complex icons work best as PNG24/32 with alpha transparency, or SVGs.

<a href="https://www.photoshop.com/">Photoshop</a> and <a href="https://creative.adobe.com/products/fireworks">Fireworks</a> can help you customize the levels of optimization across different areas of the image. This means the main subject can remain high quality, while the rest is optimized to increase performance. Lossless image compression tools like <a href="https://imageoptim.com/">ImageOptim</a> and <a href="https://tinypng.com/">TinyPNG</a> can squeeze the most out of file size, without losing image quality.

You could also make use of the new HTML5 <code>&lt;picture&gt;</code> element and <code>srcset</code> and <code>size</code> attributes for images. These two additions to the language help you define responsive images directly in the HTML, so the browser will only download the image that matches the given condition.

<pre><code class="language-markup">&lt;picture&gt;
  &lt;source media="(min-width: 960px)" srcset="picture-large.png"&gt;
  &lt;source media="(min-width: 465px)" srcset="picture-small.png"&gt;
  &lt;img src="images/picture.png" alt="Picture alt"&gt;
&lt;/picture&gt;</code></pre>

However, this technique should be used carefully. Only a few browsers support it: some modern browsers (like Safari), Android browsers and IE10/11 (and older) do not. Polyfill alternatives can make this method work across older browsers, but these are external JavaScript libraries that have to be loaded separately, and may not be worth it given that other techniques are available. It’s worth considering your target audience, and what technologies they will be using, to see if the extra weight of the polyfill is required.

Data URLs are a final option. Instead of linking to an external image file, image data can be converted into a base64 (or ASCII) encoded string and embedded directly into the CSS or HTML file. <a href="https://dataurl.net/#about">A simple online conversion tool is available</a>. Data URLs are helpful, as they save HTTP requests and can transfer small files more quickly. But, as demonstrated below, the embedded code size is larger than linking to external images. The added length can make HTML and CSS documents more difficult to maintain, and image changes will have to be reencoded and embedded each time.

<pre><code class="language-markup">&lt;img width="32" height="32" alt="Camera" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAYZJREFUeNrsVsttwzAMtYUAvfrck0fIBukIyQAF5AkaTxB0gowQAR3AWcEbdASfeva1p5YEmIAgZEmWZKeHEhD8k2Ty8fFRZZFg3x/PL3DpYFSOac3T65eZ+qiKNLt4fo52Bker7A7AphoudcBU/PlxCQROM+a+TaGgFo7ei4JaIXonCmqF6J0oqJWiv6MgX5QU1R7LJTKyGBtgtKAP15J+3hWPsYOiyB9lZ7Ui7DarN5aXnzDeGeG2nk1GGKj1Pd3fGL+DoX1SjRz4kXlBcjByuvhhiEzjRMlWlGI9tcEmAT5nl0MjxxpwpKfGFYRASAoMbN7MFLCLDQkbAlsP7BhVKzaXOnKvczYN1+wlJ2KU0PCcM57wasL7jr7xdJgcUtzLWnbVuWdtlAOjYLlLR+qptbmOZMkW40Al8jp4mo51bYoDO/HcOua2nrVRDmh+sqFSO4hoB66ojC9BOhCSAmR3I5y4+jpfrhTcUNAzj3E6VIpniVJqM0p1YJF2/Od14N+BrPYrwAAH54zsDNHtwgAAAABJRU5ErkJggg==" /&gt;
</code></pre>

### Automate CMS Media Optimization

Applying the asset optimization techniques from the previous section meant we could choose a classic, image-led design for <a href="https://www.bam.co.uk/">BAM</a>, enabling them to showcase new construction project photography.

But we also needed to give BAM the freedom to update content without needing us to optimize each image. Of course, no solution would be as effective as optimization by hand but we did manage to achieve a reasonable degree of automated optimization. We reconfigured their existing <a href="https://www.sitefinity.com/">Sitefinity</a> CMS to create flexibility. Standard options were used to resize (and optimize) the images automatically, fitting the context of each web page:

<pre><code class="language-markup">&lt;thumbnailResizeSettings
    compositingQuality="HighQuality"
    interpolationMode="HighQualityBicubic"
    smoothingMode="HighQuality"&gt;
&lt;/thumbnailResizeSettings&gt;
</code></pre>

Sitefinity can also resize images from the URL by using URL parameters, and even faster rendering can be achieved by caching the resized image, using the following option:

<pre><code class="language-bash">/images/image-opt.jpg?size=480
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddfd6fa9-35dc-4c48-b6e9-1dca9d309149/03-bammobile-opt.jpg"><img title="BAM website on mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62380835-412f-4998-9748-51a2932a3fc6/03-bammobile-500-opt.jpg" alt="BAM website on mobile" /></a><figcaption>The homepage of the BAM website relies on regular project photography updates, so we implemented automated image optimization. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddfd6fa9-35dc-4c48-b6e9-1dca9d309149/03-bammobile-opt.jpg">Large preview</a>)</figcaption></figure>

<strong>Most CMS systems allow some degree of media optimization.</strong> For instance, you can define media settings to ensure future users only add images that fit the website templates. Here’s a quick example from <a href="https://wordpress.com/">WordPress</a>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6110378-a2b9-4b98-bab4-9de409a3ff23/04-mediasettings-500-opt.jpg"><img title="Wordpress media settings" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6110378-a2b9-4b98-bab4-9de409a3ff23/04-mediasettings-500-opt.jpg" alt="Wordpress media settings" /></a><figcaption>In WordPress, implement media settings like these to ensure future image uploads fit website templates.</figcaption></figure>

<pre><code class="language-markup">// Wordpress example
&lt;div class="avatar"&gt;
    &lt;?php the_thumbnail( 'thumbnail' ); ?&gt;
&lt;/div&gt;
</code></pre>

### Streamline Fonts And Icons

Fonts are an important part of the user experience and branding of a website or application, but might not be the first priority for the user. For this reason, web fonts can be another factor to optimize.

By deferring font loading, the browser will display copy in whatever font it has available to begin with. This means the user will always get the content first. Deferring font loading can be achieved by separating the part of the CSS that links to the font files, and loading it after the rest of the page has been rendered. Note, however, that the text may briefly flash to change when the web font is loaded.

Similarly, icons are another area to optimize, as they are small files that need to be loaded frequently. You could consider also using font files for icons. Use a service like <a href="https://fontello.com/">Fontello</a> to choose a variety of icons, and generate a font file limited to your selection. This technique can create high-quality vector icons for all screen resolutions, with a light performance impact.

Alternatively, image sprites are a well-known option. They combine images into one file (that uses only one request to load) and display just the part required for design by using the background position. <a href="https://paulstamatiou.com/how-to-optimize-your-site-with-image-sprites/">Paul Stamatiou describes how this is done</a> and outlines a few limitations.

{{% ad-panel-leaderboard %}}

### Loading Technologies

The following techniques avoid sending a website’s entire content to mobile browsers. Instead, <strong>only the precise data needed is downloaded</strong>, by optimizing for each breakpoint. Mobile loading speed was a key consideration for <a href="https://www.velocitydrive.com/">Velocity Drive's website</a>, which provides trailer technologies. JavaScript libraries must load at all breakpoints, to test for browser capabilities and avoid glitches. But we optimized assets carefully for each breakpoint: the homepage load size is only 323KB on mobile, rising to 828KB on large desktops.

Take this further with <strong>conditional lazy loading techniques</strong> to raise the perceived page speed. They load visible sections in stages, with key content placed above the fold. Expensive items (like images) found towards the end of pages aren’t loaded, unless the user chooses to scroll through the content. This technique was key for the 'Insights' section of the <a href="https://www.niu-solutions.com">Niu Solutions website</a>, covering their IT innovations. We used a small jQuery plugin called <a href="https://jscroll.com/">jScroll</a> to load further articles as the user scrolls down. Here’s a sample of how we would set up this plugin, which simply requires the link to more content:

<pre><code class="language-markup">&lt;a href="articles.php" class="more"&gt;Load more&lt;/a&gt;</code></pre>

<pre><code class="language-javascript">  // Insights javascript
  $('.insights-container).jscroll({
      nextSelector: '.more',
      loadingHtml: '&lt;p&gt;Loading...&lt;/p&gt;'
  });
</code></pre>

Preloading technologies present further opportunities. They can anticipate and prepare for the user’s next move by loading the page they are likely to view next before they do so, to provide a faster experience. However, discovering the typical traffic structure is easier when revamping an existing website, as you can study the behavior flow funnels on Google Analytics.

### Enhance From A Core Experience

The <a href="https://responsivenews.co.uk/post/18948466399/cutting-the-mustard">BBC's Responsive News</a> refers to the idea of giving the user the core experience they request, then <strong>evaluating the user’s environment and enhancing the experience accordingly</strong>. A simple example of this is loading low-resolution images initially, and then showing high-resolution depending on the bandwidth the user has.

This idea is part of progressive enhancement, where web technologies are layered to provide the best experience across environments. Progressive enhancement can be based on a number of different factors. These include the technology a user has access to, like their browser, operating system, and environment (such as internet speed). Here, define a basic set of features that must work on the least capable browsers, and only add further complexity after testing whether browsers can handle it.

Detecting whether the browser can support HTML5 and CSS features helps us write conditional code to cover all eventualities: enhancing and adding features when supported, while staying safe and simple for devices and browsers that do not.

### Reduce Feature Testing

Incorporating feature-testing libraries like <a href="https://modernizr.com/">Modernizr</a> or <a href="https://github.com/phiggins42/has.js/">has.js</a> is a common, recommended practice. But too many developers implement the entire library; they test for all capabilities, even though only a small number of results are needed to determine whether to add features.

<a href="https://timkadlec.com/2014/09/js-parse-and-execution-time/">Tim Kadlec reports</a> the parsing and execution time of the same library (minimized jQuery 2.1.1) across a range of devices. This demonstrates there’s often a larger mobile performance cost (even between old and new devices) for implementing these libraries, in comparison with desktop. We tend to <strong>tailor the library, testing relevant website features only</strong>. This will save time and precious mobile processing power.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78cd6677-0e7d-4e69-a5a6-62d52c34c4a8/05-modernizr-opt.jpg"><img title="Reducing the size of the Modernizr testing library" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/361f357e-c387-4c45-b767-eddfa99a6198/05-modernizr-500-opt.jpg" alt="Reducing the size of the Modernizr testing library" /></a><figcaption>Tailoring testing libraries is crucial. This image compares the size of implementing the entire library (top), with limiting tests to just what we needed (bottom). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78cd6677-0e7d-4e69-a5a6-62d52c34c4a8/05-modernizr-opt.jpg">Large preview</a>)</figcaption></figure>

## Server-Side Optimization

Server response time is a key factor in website speed: many aim for <a href="https://developers.google.com/speed/docs/insights/Server">less than 200ms</a>. But network latency (the delay as data moves between the server and device) is the real bottleneck for mobile performance, leaving mobile users with a slower experience.

This is influenced by network speed. <a href="https://media.ofcom.org.uk/news/2014/3g-4g-bb-speeds/">According to Ofcom</a>, the average download speeds on popular 3G and 4G networks were 6.1Mbps and 15.1Mbps in the UK. Some interpret this as a clear limit on maximum website size. But the reality is more complex, as the speed varies depending on the coverage and environmental context. Users often connect to slow Edge (E) and GPRS when out of range.

There are a variety of techniques available to improve server-side website performance.

### Caching, Prerendering, And Static Content

Dynamic web pages require multiple database queries, taking valuable time to process output and format data, then render to browser-legible HTML. <strong>It’s recommended to cache content previously rendered for that device.</strong> For returning visitors, instead of processing from scratch, it will check the cache, and only send updates.

Many also choose JavaScript template libraries like <a href="https://developers.google.com/speed/docs/insights/Server">Handlebars</a> and <a href="https://mustache.github.io/">Mustache</a> to handle web content. But parsing and executing JavaScript is power- and time-consuming. Mobile devices can’t process these template libraries as fast as desktop computers, and drain their processing resources. Rendering pages completely on the server is much faster. Twitter opted for this approach as early as 2012, and <a href="https://blog.twitter.com/2012/improving-performance-on-twittercom">explained the value on their blog</a>.

Recently, our senior front-end developer pushed the boundaries of this technique for his <a href="https://ramonlapenta.com/">personal portfolio</a>. It was built with the file-based Statamic CMS, which just added html_cache support. When implemented, this feature reduced the average load time of all pages from roughly 1.8 seconds to 225 milliseconds.

### Browser Caching

Granular optimization can streamline website loading by preventing regular transfer of files you know aren’t updated often. <strong>Use a server handler (like an <i>.htaccess</i> file) to instruct the browser</strong> on which type of content to store, and how long they should keep copies. Here’s how you can implement browser caching on the Apache server:

<div class="break-out">

 <pre><code class="language-bash">
&lt;IfModule mod_expires.c&gt;
    ExpiresActive on
    ExpiresDefault                          "access plus 1 month"
  # CSS
    ExpiresByType text/css                  "access plus 1 year"
  # Data interchange
    ExpiresByType application/json          "access plus 0 seconds"
    ExpiresByType application/ld+json       "access plus 0 seconds"
    ExpiresByType application/xml           "access plus 0 seconds"
    ExpiresByType text/xml                  "access plus 0 seconds"
  # Favicon and cursor images
    ExpiresByType image/x-icon              "access plus 1 week"
  # HTML components (HTCs)
    ExpiresByType text/x-component          "access plus 1 month"
  # HTML
    ExpiresByType text/html                 "access plus 0 seconds"

  # JavaScript
    ExpiresByType application/javascript    "access plus 1 year"

  # Manifest files
    ExpiresByType application/x-web-app-manifest+json   "access plus 0 seconds"
    ExpiresByType text/cache-manifest       "access plus 0 seconds"
  # Media
    ExpiresByType audio/ogg                 "access plus 1 month"
    ExpiresByType image/gif                 "access plus 1 month"
    ExpiresByType image/jpeg                "access plus 1 month"
    ExpiresByType image/png                 "access plus 1 month"
    ExpiresByType video/mp4                 "access plus 1 month"
    ExpiresByType video/ogg                 "access plus 1 month"
    ExpiresByType video/webm                "access plus 1 month"
  # Web feeds
    ExpiresByType application/atom+xml      "access plus 1 hour"
    ExpiresByType application/rss+xml       "access plus 1 hour"
  # Web fonts
    ExpiresByType application/font-woff     "access plus 1 month"
    ExpiresByType application/vnd.ms-fontobject  "access plus 1 month"
    ExpiresByType application/x-font-ttf    "access plus 1 month"
    ExpiresByType font/opentype             "access plus 1 month"
    ExpiresByType image/svg+xml             "access plus 1 month"
&lt;/IfModule&gt;
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

### Content Delivery Networks (CDNs)

You can improve asset loading by using a CDN like <a href="https://www.cloudflare.com/">CloudFlare</a> alongside your usual hosting service. Here, static content (like images, fonts and CSS) is stored on a network of global servers. Every time a user requests this content, the CDN detects their location and delivers assets from the nearest server, which reduces latency. It increases speed by allowing the main server to focus on delivering the application instead of serving static files.

Although it adds expense, <strong>use a dedicated CDN to improve the loading speed of asset-heavy websites</strong>. Aside from initial setup, CloudFlare doesn’t require manual configuration; the cache is built and updated for you, based on historical traffic and which assets are best to serve. But implement this with future independent content management in mind: ensure all assets uploaded from a CMS are also transparently served through the CDN.

A CDN was the best choice for our <a href="https://www.eurofighter.com/">Eurofighter Typhoon</a> website, as striking high-res photography of defense aircraft was a crucial feature to showcase their ability. In the last 30 days, reports indicate CloudFlare saved 76% of requests and 48% of bandwidth, increasing the speed of the image-heavy website.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd207bbb-69a0-495b-9873-fb5aba4e6dbc/06-eurofightermobile-opt.jpg"><img title="Eurofighter website on mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/658bcc6d-9003-4a2d-b7aa-b6ebcdab0836/06-eurofightermobile-500-opt.jpg" alt="Eurofighter website on mobile" /></a><figcaption>We implemented a CDN for Eurofighter Typhoon’s website, to speed up the loading of the high-res photography. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd207bbb-69a0-495b-9873-fb5aba4e6dbc/06-eurofightermobile-opt.jpg">Large preview</a>)</figcaption></figure>

## Testing

There’s no replacement for testing throughout production. <strong>Aim to use various tools to test work in progress</strong> by simulating the mobile experience and diagnosing potential performance issues.

As production progresses, always keep an eye on the numbers: from ensuring design assets are properly generated and exported, to checking the page file size and amount of HTTP requests via the developer tools on your browser. Here, the Network tab gives you a complete overview of the resources loaded, total file size and rendering time:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d33c208b-e182-4010-b8c5-436984f27f67/07-devtools-opt.png"><img title="Developer Tools - Cyber-Duck Website" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11eb86d1-db5b-457f-8b78-1b58256fea3f/07-devtools-500-opt.png" alt="Developer Tools - Cyber-Duck Website" /></a><figcaption>Developer Tools gives us a complete overview of the performance metrics of the Cyber-Duck website. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d33c208b-e182-4010-b8c5-436984f27f67/07-devtools-opt.png">Large preview</a>)</figcaption></figure>

Note the blue and red vertical lines at the right of the timeline in Chrome Inspector above. These represent DOM Ready and Page Load events respectively. At the bottom of the window, it displays the amount of HTTP requests and total file size loaded at the current breakpoint.

Other tools include:

*   [WebPagetest](https://www.webpagetest.org/) offers a wide variety of options for testing live URLs: from choosing any location around the world, to shaping specific 3G and 4G connection speeds and latency. You can even experience how the website loads for these users, through the filmstrip view and video.
*   [Google's Pagespeed Insights](https://developers.google.com/speed/pagespeed/insights/) is a more visual, introductory tool for analyzing page speed. It splits results into desktop or mobile, and suggests techniques to improve targeted areas of your site: indicating resources to cache or images to optimize.

### Test On Real Devices

But don’t rely on simulators alone. We also test projects throughout production on a variety of real mobile devices.

Create your own device lab or use <a href="https://opendevicelab.com/">OpenDeviceLabs</a>. Ideally, get a sense of the real user experience by avoiding the powerful office Wi-Fi. Create a test site in a web server (ideally the same as the live server) that you can access from outside the office network. Then, test while on the move in typical environments like a crowded coffee shop or hotel, on a network connection.

## Mobile Performance Summary

Above all, aim to create a website that can balance aesthetics and performance on mobile, and achieve real conversion metrics. A collaborative, iterative performance optimization process will help you achieve this.

Right from the start of the project, encourage the internal team to work together under a mobile mindset by <strong>setting a strict performance budget</strong>. Build an understanding of the client and server-side factors that determine website performance on mobile. Then you can meet the goal set by implementing a mixture of the targeted optimization techniques I have described. Of course, there’s still a trade-off between having a striking design, high performance and security in some cases; a collaborative design and development team can decide what’s best for the business, checking with relevant project managers and stakeholders.

Our optimization project for a global technology consultancy demonstrates how these techniques can combine to improve loading speed and size significantly. The project involved caching templates and pages, optimizing assets and fonts, and reducing feature testing, among other techniques. So far, <a href="https://tools.pingdom.com/fpt/">tests demonstrate</a> the rendering and total load time has been cut to less than 1.4 seconds, from almost 4 seconds before we began work; similarly, the file size has been reduced to 1MB from over 3MB.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Front-End Performance Checklist 2017](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Everything You Need To Know About AMP](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
*   [The (Not So) Secret Powers Of The Mobile Browser](https://www.smashingmagazine.com/2016/12/the-not-so-secret-powers-of-the-mobile-browser/)

{{< signature "da, ml, jb, og, il" >}}

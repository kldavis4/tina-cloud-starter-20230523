---
title: Quick Wins For Improving Performance And Security Of Your Website
slug: improving-performance-security
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8996478f-40c6-4693-85cf-9f29885b6f75/chrome-dev-tools-500w-opt.png
date: 2017-10-26T20:31:21.000Z
author: jonaskrummenacher
description: >-
  When it comes to building and maintaining a website, one has to take a ton of things into consideration. All webmasters should strive for a) improving the performance of their website, and b) increasing their website's security.
summary: >-
  When it comes to building and maintaining a website, one has to take a ton of
  things into consideration. All webmasters should strive for a) improving the performance of their website, and b) increasing their website's security.
categories:
  - Performance
  - Security
---
*   Improving the performance of their website,
*   Increasing their website's security.

Both of these goals are vital in order to run a successful website.

So, we've put together a list of five technologies you should consider implementing to **improve both the performance and security of your website**. Here's a quick overview of the topics we'll cover:

*   **Let's Encrypt (SSL)**<br/>A free way to obtain an SSL certificate for improved security and better performance.
*   **HTTP/2**  The successor to the HTTP 1.1 protocol, which introduces many performance enhancements.
*   **Brotli compression**.<br/>A compression method that outperforms Gzip, resulting in smaller file sizes.
*   **WebP images**.<br/>An image format that renders images smaller than a typical JPEG or PNG, resulting in faster loading times.
*   **Content delivery network**.<br/>A collection of servers spread out across the globe, with the aim of caching and delivering your website's assets faster.

{{% feature-panel %}}

If you aren't aware of the benefits of improving your website's performance and security, consider the fact that Google loves speed and, since 2010, has been using [website speed as a ranking factor](https://webmasters.googleblog.com/2010/04/using-site-speed-in-web-search-ranking.html). Furthermore, if you run an e-commerce shop or a simple blog with an opt-in form, a faster website will increase your conversions. According to a [study by Mobify](https://www.bizreport.com/2016/08/mobify-report-reveals-impact-of-mobile-website-speed.html), for every 100-millisecond decrease in home-page loading speed, Mobify saw a 1.11% lift in session-based conversions for its customer base, amounting to an average annual revenue increase of $376,789.

The web is also quickly moving towards SSL to provide users with better security and improved overall performance. In fact, for a couple of the technologies mentioned in this article, having an SSL-enabled website is a prerequisite.

Before jumping in, note that even if you can't (or decide not to) apply each and every one of the suggestions mentioned here, your website would still benefit from implementing any number of the methods outlined. Therefore, try to determine which aspects of your website could use improvement and apply the suggestions below accordingly.</p>

## Let's Encrypt (SSL)

If your website is still being delivered over HTTP, it's time to migrate now. Google already takes HTTPS into consideration as a ranking signal and according to [Google's Security blog](https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html), all non-secure web pages will eventually display a dominant "Not Secure" message within the Chrome browser.

That's why, to start off this list, we'll go over how you can complete the migration process with a free SSL certificate, via Let's Encrypt. Let's Encrypt is a free and automated way to obtain an SSL certificate. Before Let's Encrypt, you were required to purchase a valid certificate from a certificate-issuing authority if you wanted to deliver your website over HTTPS. Due to the additional cost, many web developers opted not to purchase the certificate and, therefore, continued serving their website over HTTP.

However, since Let's Encrypt's public beta launched in late 2015, millions of free SSL certificates have been issued. In fact, Let's Encrypt stated that, as of late June 2017, over [100 million certificates](https://letsencrypt.org/2017/06/28/hundred-million-certs.html) have been issued. Before Let's Encrypt launched, fewer than 40% of web pages were delivered over HTTPS. A little over a year and a half after the launch of Let's Encrypt, that number has risen to 58%.

If you haven't already moved to HTTPS, do so as soon as possible. Here are a few reasons why moving to HTTPS is beneficial:

*   increased security (because everything is encrypted),
*   HTTPS is required in order for HTTP/2 and Brotli to work,
*   HTTPS is a [ranking signal](https://webmasters.googleblog.com/2014/08/https-as-ranking-signal.html),
*   SSL-secured websites build visitor trust.</p>

### How to Obtain a Let's Encrypt Certificate

You can obtain an SSL certificate in a few ways. Although the SSL certificates that Let's Encrypt provides satisfy most use cases, there are certain things to be aware of:

*   There is currently no option for wildcard certificates. However, this is planned to be supported in [January 2018](https://letsencrypt.org/2017/07/06/wildcard-certificates-coming-jan-2018.html).
*   Let's Encrypt certificates are valid for a period of 90 days. You must either renew them manually before they expire or set up a process to renew them automatically.

Of course, if one or both of these points are a deal-breaker, then acquiring a custom SSL certificate from a certificate authority is your next best bet. Regardless of which provider you choose, having an HTTPS-enabled website should be your top priority.

To obtain a Let's Encrypt certificate, you have two methods to choose from:

*   With shell access: Run the installation and obtain a certificate yourself.
*   Without shell access: Obtain a certificate through your hosting or CDN provider.

The second option is pretty straightforward. If your web host or CDN provider offers Let's Encrypt support, you basically just need to enable it in order to start delivering assets over HTTPS.

However, if you have shell access and want or need to configure Let's Encrypt yourself, then you'll need to determine which web server and operating system you're using. Next, go to [Certbot](https://certbot.eff.org) and select your software and system from the dropdown menus to find your specific installation instructions. Although the instructions for each combination of software and OS are different, Certbot provides simple setup instructions for a wide variety of systems.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ceda785-e852-4ff4-b80c-6376ba8b6bf9/certbot-homepage-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8651b36-a6c5-47d6-b537-88f3a6280699/certbot-homepage-800w-opt.png" alt="Let's Encrypt Certbot home page" width="800" height="549" /></a><figcaption>Certbot home page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ceda785-e852-4ff4-b80c-6376ba8b6bf9/certbot-homepage-preview-opt.png">View large version</a>)</figcaption></figure>

## HTTP/2

Thanks to Let's Encrypt (or any other SSL certificate authority), your website should now be running over HTTPS. This means you can now take advantage of the next two technologies we'll discuss, which would otherwise be incompatible if your website was delivered over HTTP. The second technology we'll cover is HTTP/2.

HTTP 1.1 was released more than 15 years ago, and since then some major improvements have occurred. One of the most welcome improvements of HTTP/2 is that it allows browsers to parallelize multiple downloads using only one connection. With HTTP 1.1, most browsers were able to handle only six concurrent downloads on average. HTTP/2 now renders methods such as domain-sharding obsolete.

Apart from requiring only one connection per origin and allowing multiple requests at the same time (multiplexing), HTTP/2 offers other benefits:

*   **Server push**.  Pushes additional resources that it thinks the client will require in the future.
*   **Header compression**.  Reduces the size of headers by using HPACK header compression.
*   **Binary**.  Unlike in HTTP 1.1, which was textual, binary reduces the time required to translate text to binary and makes it easier for a server to parse.
*   **Prioritization**.  Priority levels are associated with requests, thereby allowing resources of higher importance to be delivered first.</p>

### Enabling HTTP/2

Regardless of how you're delivering the majority of your content, whether from your origin server or a CDN, most providers now support HTTP/2\. Determining whether a provider supports HTTP/2 should be fairly easy by going to its features page and checking around. As for CDN providers, [Is TLS Fast Yet?](https://istlsfastyet.com/#cdn-paas) provides a comprehensive list of CDN services and marks whether they support HTTP/2.

If you want to check for yourself whether your website currently uses HTTP/2, then you'll need to get the latest version of [cURL](https://curl.haxx.se/) and run the following command:

<pre><code class="language-markup">curl --http2 https://yourwebsite.com</code></pre>

Alternatively, if you're not comfortable using the command line, you can open up Chrome's Developer Tools and navigate to the "Network" tab. Under the "Protocol" column, you should see the value `h2`.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb1f7b5b-3735-44ff-90f9-da95f68f45ef/chrome-dev-tools-h2-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc70befa-7a30-4089-b999-adffaff54b11/chrome-dev-tools-h2-800w-opt.png" alt="Chrome's Developer Tools "Network" tab, showing the h2 protocol" width="800" height="331" /></a><figcaption>Chrome's Developer Tools <code>h2</code> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb1f7b5b-3735-44ff-90f9-da95f68f45ef/chrome-dev-tools-h2-preview-opt.png">View large version</a>)</figcaption></figure>

### Enabling HTTP/2 on nginx

If you're running your own server and are using an outdated software version, then you'll need to upgrade it to a version that supports HTTP/2\. For nginx users, the process is pretty straightforward. Simply ensure that you're running nginx **version 1.9.5** or higher, and add the following `listen` directive within the server block of your configuration file:

<pre><code class="language-markup">listen 443 ssl http2;</code></pre>

### Enabling HTTP/2 on Apache

For Apache users, the process involves a few more steps. Apache users must update their system to version **2.4.17** or higher in order to make use of HTTP/2\. They'll also need to build HTTPS with the [mod_http2](https://httpd.apache.org/docs/2.4/mod/mod_http2.html) Apache module, load the module, and then define the proper server configuration. An outline of how to configure HTTP/2 on an Apache server can be found in the [Apache HTTP/2 guide](https://httpd.apache.org/docs/2.4/howto/http2.html).

No matter which web server you're using, your website will need to be running on HTTPS in order to take advantage of the benefits of HTTP/2.</p>

### HTTP/2 Vs. HTTP 1.1: Performance Test

You can test the performance of HTTP/2 compared to HTTP 1.1 manually by running an online speed test before and after enabling HTTP/2 or by checking your browser's development console.

Based on the structure and number of assets that your website loads, you might experience different levels of improvement. For instance, a website with a large number of resources will require multiple connections over HTTP 1.1 (thus increasing the number of round trips required), whereas on HTTP/2 it will require only one.

The results below are the findings for a default WordPress installation using the 2017 theme and loading 18 image assets. Each setup was tested three times on a 100 Mbps connection, and the average overall loading time was used as the final result. Firefox was used to examine the waterfall structure of these tests.

The first test below shows the results over HTTP 1.1\. In total, the entire page took an average of 1.73 seconds to fully load, and various lengths of blocked time were incurred (as seen by the red bars).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f75be0e2-c56d-44a9-bb8b-078452b74f49/firefox-http1.1-preview-opt"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a23138bf-25b6-4bca-a850-4dd653b8ac3d/firefox-http1.1-800w-opt" alt="HTTP 1.1 speed test results" width="800" height="261" /></a><figcaption>HTTP 1.1 loading time and waterfall (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f75be0e2-c56d-44a9-bb8b-078452b74f49/firefox-http1.1-preview-opt">View large version</a>)</figcaption></figure>

When testing the exact same website, only this time over HTTP/2, the results were quite different. Using HTTP/2, the average loading time of the entire page took 1.40 seconds, and the amount of blocked time incurred was negligible.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0c69c7a-a2d9-4008-96f4-97b038a495af/firefox-http2.0-preview-opt"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a999af02-e4d0-4156-b487-be43abd2684c/firefox-http2.0-800w-opt" alt="HTTP/2 speed test results" width="800" height="260" /></a><figcaption>HTTP/2 loading time and waterfall (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0c69c7a-a2d9-4008-96f4-97b038a495af/firefox-http2.0-preview-opt">View large version</a>)</figcaption></figure>

Just by switching to HTTP/2, the average savings in loading time ended up being 330 milliseconds. That being said, the more resources your website loads, the more connections must be made. So, if your website loads a lot of resources, then implementing HTTP/2 is a must.</p>

## 3\. Brotli Compression

The third technology is Brotli, a compression algorithm developed by Google back in 2015\. Brotli continues to grow in popularity, and currently all popular web browsers support it (with the exception of Internet Explorer). Compared to Gzip, Brotli still has some catching up to do in global availability (i.e. in CMS plugins, server support, CDN support, etc.).

However, Brotli has shown some impressive compression results compared to other methods. For instance, according to [Google's algorithm study](https://www.gstatic.com/b/brotlidocs/brotli-2015-09-22.pdf), Brotli outperformed Zopfli (another modern compression method) by **20 to 26%** in compression ratio.</p>

### Enabling Brotli

Depending on which web server you're running, implementation of Brotli will be different. You'll need to use the method appropriate to your setup. If you're using nginx, Apache or Microsoft IIS, then the following modules are available to enable Brotli.

*   [ngx_brotli](https://github.com/google/ngx_brotli), nginx module
*   [mod_brotli](https://httpd.apache.org/docs/trunk/mod/mod_brotli.html), Apache module
*   [IIS Brotli](https://www.iis.net/downloads/community/2016/03/iis-brotli), Microsoft IIS community-contributed extension

Once you've finished downloading and installing one of the modules above, you'll need to configure the directives to your liking. When doing this, pay attention to three things:

*   **File type**.  The types of files that can be compressed with Brotli include CSS, JavaScript, XML and HTML.
*   **Compression quality**.  The quality of compression will depend on the amount of compression you want to achieve in exchange for time. The higher the compression level, the more time and resources will be required, but the greater the savings in size. Brotli's compression value can be defined anywhere from 1 to 11.
*   **Static versus dynamic compression**.  The stage at which you would like Brotli compression to take place will determine whether to implement static or dynamic compression:
    *   **Static** compression pre-compresses assets ahead of time — before the user actually makes a request. Therefore, once the request is made, there is no need for Brotli to compress the asset — it will already have been compressed and, hence, can be served immediately. This feature comes built-in with the nginx Brotli module, whereas implementing [static compression with Apache](https://css-tricks.com/brotli-static-compression/) requires some configuration.
    *   **Dynamic** compression occurs on the fly. In other words, once a visitor makes a request for a Brotli-compressible asset, the asset is compressed on the spot and subsequently delivered. This is useful for dynamic content that needs to be compressed upon each request, the downside being that the user must wait for the asset to be compressed before it is delivered.

A Brotli configuration for nginx users might look similar to the snippet below. This example sets compression to occur dynamically (on the fly), defines a quality level of 5 and specifies various file types.</p>

<pre><code class="language-markup break-out">brotli on;
brotli_comp_level 5;
brotli_types text/plain text/css application/json application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript;</code></pre>

To verify that Brotli is enabled on your server, you can open up Chrome's Developer Tools, navigate to the "Network" tab, select an asset, and check the `Content-Encoding` header. This should now be `br`. Note that Brotli requires HTTPS, so if you've correctly gone through the installation and configuration process but still don't see the `br` value, then you'll need to migrate to HTTPS.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d0d653e-e454-4fb2-b9a8-cb93fe88d12a/chrome-dev-tools-br-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcdce546-a0a2-471e-83dd-3656cebd6173/chrome-dev-tools-br-800w-opt.png" alt="Chrome Developer Tools Network tab showing the br encoding" width="800" height="236" /></a><figcaption>Chrome's Developer Tools <code>br</code> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d0d653e-e454-4fb2-b9a8-cb93fe88d12a/chrome-dev-tools-br-preview-opt.png">View large version</a>)</figcaption></figure>

Otherwise, you can run a simple cURL command, such as:

<pre><code class="language-markup break-out">curl -I https://yourwebsite.com/path/to/your/asset.js</code></pre>

<p>This will return a list of response headers, where you can also check for the <code>Content-Encoding</code> header value. If you're using WordPress and want to take things a step further by delivering a Brotli-compressed HTML document, check out my <a href="https://www.sitepoint.com/brotli-compression-wordpress/">WordPress guide to Brotli</a> to learn how.</p>

### Brotli Vs. Gzip: Performance Test

<p>To compare Brotli and Gzip compression, we'll take three compressible web assets and compare them in size and loading speed. Both compression methods were defined with a level 5 compression value.</p>

<p>Having tested the assets three times and taking the average loading speed of each, the results were as follows:</p>

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist">Asset name</th>
<th>Gzip size</th>
<th>Gzip loading time</th>
<th>Brotli size</th>
<th>Brotli loading time</th>
</tr>
</thead>
<tbody>
<tr>
<td>jquery.js</td>
<td>33.4 KB</td>
<td>308 ms</td>
<td>32.3 KB</td>
<td>273 ms</td>
</tr>
<tr>
<td>dashicons.min.css</td>
<td>28.1 KB</td>
<td>148 ms</td>
<td>27.9 KB</td>
<td>132 ms</td>
</tr>
<tr>
<td>style.css</td>
<td>15.7 KB</td>
<td>305 ms</td>
<td>14.5 KB</td>
<td>271 ms</td>
</tr>
</tbody>
</table>

<p>Overall, the Gzipped assets were 77.2 KB in total size, while the Brotli assets were 74.7 KB. That's a 3.3% reduction in overall page size just from using Brotli compression on three assets. As for loading time, the Gzip assets had a combined total time of 761 milliseconds, while the Brotli assets took 676 milliseconds to load — an improvement of 12.6%.</p>

## 4. WebP Images

<p>Our fourth suggestion is to use the image format that goes by the name of WebP. Like Brotli, WebP was developed by Google for the purpose of making images smaller. Like JPEG and PNG, WebP is an image format. The primary advantage of serving WebP images is that they are much smaller in size than JPEGs and PNGs. Typically, savings of up to 80% can be achieved after converting a JPEG or PNG to WebP.</p>

<p>The downside of the WebP image format is that not all browsers support it. At the time of writing, only Chrome and Opera do. However, with proper configuration, you can deliver WebP images to supporting browsers, while delivering a fallback image format (such as JPEG) to non-supporting browsers.</p>

<p>WebP still has a way to go before becoming as widespread as JPEG and PNG. However, thanks to its impressive savings in size, it stands a good chance of continued growth. Overall, WebP reduces total page size, speeds up website loading and saves bandwidth.</p>

### How to Convert to and Deliver WebP

A few options are available to convert images to [WebP format](https://www.smashingmagazine.com/2018/07/webp-manual/). If you use a popular CMS such as WordPress, Joomla or Magento, Plugins are available that enable you to convert images directly within the CMS' dashboard.</p>

<p>On the other hand, if you want to take a manual approach, online <a href="https://webp-converter.com/">WebP image converters</a> are available, and certain image-processing apps even come with a WebP format option that you can export to, thereby saving you from having to convert anything at all.</p>

<p>Lastly, if you prefer a more integrated approach, certain image-processing services provide an API that you can use to integrate directly in your web project, enabling you to <a href="https://images.guide/">convert images automatically</a>.</p>

<p>As mentioned, not all browsers currently support WebP images. Therefore, if you serve an image on your website with only a <code>.webp</code> extension, non-supporting browsers will return a broken image. That's why a fallback is important. Let's go over three ways to achieve this.</p>

### 1. Use the <code>picture</code> Element

<p>This method allows you to define the path of a WebP image, as well as the path of the original JPEG within the website's HTML. With this method, supporting browsers will display the WebP images, while all other browsers will display the default image defined in the last nested child tag within the <code>picture</code> block. Consider the following example:</p>

<pre><code class="language-markup break-out">&lt;picture&gt;
	&lt;source srcset="images/my-webp-image.webp" type="image/webp"&gt;
	&lt;img src="images/my-jpg-image.jpg" alt="My image"&gt;
&lt;/picture&gt;</code></pre>

<p>This method implements WebP functionality most widely, while ensuring that a fallback mechanism is in place. However, it might require a lot of modification to the HTML, depending on how large your application is.</p>

### 2. Modify the Server's Config File

<p>This method uses rewrite rules defined in the server's config file to fall back to a supported image format if the browser doesn't support WebP. Use the appropriate snippet for Apache or nginx according to your web server, and adjust the <code>path/images</code> directory accordingly.</p>

<p>For <strong>Apache</strong>:</p>

<pre><code class="language-php break-out">RewriteEngine On
RewriteCond %{HTTP_ACCEPT} image/webp
RewriteCond %{DOCUMENT_ROOT}/$1.webp -f
RewriteRule ^(path/images.+)\.(jpe?g|png)$ $1.webp [T=image/webp,E=accept:1]

Header append Vary Accept env=REDIRECT_accept
AddType image/webp .webp</code></pre>

<p>For <strong>nginx</strong>:</p>

<pre><code class="language-php"># http config block
map $http_accept $webp_ext {
	default "";
	"~*webp" ".webp";
}

# server config block
location ~* ^(path/images.+)\.(png|jpg)$ {
	add_header Vary Accept;
	try_files $1$webp_ext $uri =404;
}</code></pre>

<p>The downside of this method is that it is not recommended if you are going to be using WebP images in conjunction with a CDN. The reason is that the CDN will cache a WebP image if a WebP-supported browser is the first one to request the asset. Therefore, any subsequent requests will return the WebP image, whether the browser supports it or not.</p>

### 3. Use a WordPress Caching Plugin

<p>If you're a WordPress user and need a solution that will deliver WebP images to supporting browsers while falling back to JPEGs and PNGs for others, all the while being compatible with a CDN, then you can use a caching plugin such as <a href="https://wordpress.org/plugins/cache-enabler/">Cache Enabler</a>. If you define within the plugin that you want to create an additional cached version for WebP, then the plugin will deliver a WebP-cached version to supporting browsers, while falling back to HTML or HTML Gzip for other browsers.</p>

### WebP Vs. JPEG: Performance Tests

<p>To demonstrate the difference in size between a WebP and JPEG image, we'll take three JPEG images, convert them to WebP, and compare the output to the originals. The three images are shown below and carry a size of 2.1 MB, 4.3 MB and 3.3 MB, respectively.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bbb5376-c2dd-4bbd-a7d3-71803ad3d22d/test-jpg-1-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a8ca17-1d4a-468d-a04c-afa8739062f9/test-jpg-1-800w-opt.jpg" alt="JPEG test image 1" width="800" height="577" /></a><figcaption>Test JPEG image 1 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bbb5376-c2dd-4bbd-a7d3-71803ad3d22d/test-jpg-1-preview-opt.jpg">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb8d239-b7e2-449d-ba77-d0237983fbba/test-jpg-2-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd3da10e-f02e-4298-acdb-9521ea27d603/test-jpg-2-800w-opt.jpg" alt="JPEG test image 2" width="800" height="531" /></a><figcaption>Test JPEG image 2 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb8d239-b7e2-449d-ba77-d0237983fbba/test-jpg-2-preview-opt.jpg">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed3e5b78-8349-43bd-9097-9aa5a580671c/test-jpg-3-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e0024c8-62ae-421f-ae7f-b03eba42c25c/test-jpg-3-800w-opt.jpg" alt="JPEG test image 3" width="800" height="526" /></a><figcaption>Test JPEG image 3 (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed3e5b78-8349-43bd-9097-9aa5a580671c/test-jpg-3-preview-opt.jpg">View large version</a>)</figcaption></figure>

When converted to WebP format, each image reduced significantly in size. The table below outlines the sizes of the original images, the sizes of the WebP versions, and how much smaller the WebP images are than the JPEGs. The images were converted to WebP using lossy compression, with a quality level of 80.</p>

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist">Image name</th>
<th>JPEG size</th>
<th>WebP size</th>
<th>Percentage smaller</th>
</tr>
</thead>
<tbody>
<tr>
<td>test-jpg-1</td>
<td>2.1 MB</td>
<td>1.1 MB</td>
<td>48%</td>
</tr>
<tr>
<td>test-jpg-2</td>
<td>4.3 MB</td>
<td>1 MB</td>
<td>77%</td>
</tr>
<tr>
<td>test-jpg-3</td>
<td>3.3 MB</td>
<td>447 KB</td>
<td>85.9%</td>
</tr>
</tbody>
</table>

<p>You can compress WebP images using either a lossless (i.e. no quality loss) or lossy (i.e. some quality loss) method. The tradeoff for quality is a smaller image size. If you want to implement lossy compression for additional savings in size, doing so with WebP will render a better quality picture at a smaller size, as opposed to a lossy JPEG at the same level of quality. <a href="https://davidwalsh.name/webp-images-performance">David Walsh has written</a> a comprehensive post outlining the size and quality differences between WebP, JPEG and PNG.</p>

## 5. Content Delivery Network

<p>The last suggestion is to use a <a href="https://www.keycdn.com/what-is-a-cdn">content delivery network</a> (CDN). A CDN accelerates web assets globally by caching them across a cluster of servers. When a website uses a CDN, it essentially offloads the majority of its traffic to the CDN's edge servers and routes its visitors to the nearest CDN server.</p>

<p>CDNs store a website's resources for a predefined period of time thanks to caching. With caching, a CDN's server creates a copy of the origin server's web asset and store it on its own server. This process makes web requests much more efficient, given that visitors will be accessing your website from multiple geographic regions.</p>

<p>If no CDN has been configured, then all of your visitors' requests will go to the origin server's location, wherever that may be. This creates additional latency, especially for visitors who are requesting assets from a location far away from the origin server. However, with a CDN configured, visitors will be routed to the CDN provider's nearest edge server to obtain the requested resources, thus minimizing request and response times.</p>

### Setting up a CDN

<p>The process for setting up a CDN will vary according to the CMS or framework you're using. However, at a high level, the process is more or less the same:</p>

<ol>
<li>Create a CDN zone that points to your origin URL (https://yourwebsite.com).</li>
<li>Create a CNAME record to point a custom CDN URL (cdn.yourwebsite.com) to the URL provided by your CDN service.</li>
<li>Use your custom CDN URL to integrate the CDN with your website (make sure to follow the guide appropriate to your website's setup).</li>
<li>Check your website's HTML to verify that the static assets are being called using the CDN's URL that you defined and not the origin URL.</li>
</ol>

<p>Once this is complete, you'll be delivering your website's static assets from the CDN's edge servers instead of your own. This will not only improve website speed, but will also enhance security, reduce the load on your origin server and increase redundancy.</p>

### Before and After Using a CDN: Performance Test

<p>Because a CDN, by nature, has multiple server locations, performance tests will vary according to where you are requesting an asset from and where the CDN's closest server is. Therefore, for the sake of simplicity, we'll choose three locations from which to perform our tests:</p>

<ul>
<li>Frankfurt, Germany</li>
<li>New York, United States</li>
<li>Toronto, Canada.</li>
</ul>

<p>As for the assets to be tested, we chose to measure the loading times of an image, a CSS file and a JavaScript file. The results of each test, both with and without a CDN enabled, are outlined in the table below:</p>

<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist"></th>
<th>Frankfurt, Germany</th>
<th>New York, United States</th>
<th>Toronto, Canada</th>
</tr>
</thead>
<tbody>
<tr>
<td>Image, no CDN</td>
<td>222 ms</td>
<td>757 ms</td>
<td>764 ms</td>
</tr>
<tr>
<td>Image, with CDN</td>
<td>32 ms</td>
<td>81 ms</td>
<td>236 ms</td>
</tr>
<tr>
<td>JavaScript file, no CDN</td>
<td>90 ms</td>
<td>441 ms</td>
<td>560 ms</td>
</tr>
<tr>
<td>JavaScript file, with CDN</td>
<td>30 ms</td>
<td>68 ms</td>
<td>171 ms</td>
</tr>
<tr>
<td>CSS file, no CDN</td>
<td>96 ms</td>
<td>481 ms</td>
<td>553 ms</td>
</tr>
<tr>
<td>CSS file, with CDN</td>
<td>31 ms</td>
<td>77 ms</td>
<td>148 ms</td>
</tr>
</tbody>
</table>

<p>In all cases, the loading times for assets loaded through a CDN were faster than without a CDN. Results will vary according to the location of the CDN and your visitors; however, in general, performance should be boosted.</p>

## Conclusion

<p>If you're looking for ways to increase your website's performance and security, these five methods are all great options. Not only are they all relatively easy to implement, but they'll also modernize your overall stack.</p>

<p>Some of these technologies are still in the process of being globally adopted (in terms of browser support, plugin support, etc.); however, as demand increases, so will compatibility. Thankfully, there are ways to implement some of the technologies (such as Brotli and WebP images) for browsers that support them, while falling back to older methods for browsers that do not.</p>

<p>As a final note, if you haven't already migrated your website to HTTPS, do so as soon as possible. HTTPS is now the standard and is required in order to use certain technologies, such as HTTP/2 and Brotli. Your website will be more secure overall, will perform faster (thanks to HTTP/2) and will look better in the eyes of Google.</p>

{{< signature "rb, vf, yk, al, il" >}}


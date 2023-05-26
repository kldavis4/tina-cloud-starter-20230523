---
title: Free SSL For Any WordPress Website
slug: free-ssl-for-any-wordpress-website
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4265358a-69bd-4db2-8723-aff0c95cf9bf/03-dashboard-preview-opt.png
date: 2016-06-21T16:06:25.000Z
author: emersonloustau
description: >-
  If you have an e-commerce website, then SSL is mandatory for safely processing
  credit cards. But even if you aren’t processing payments, you should still
  seriously consider secure HTTP (or HTTPS), especially now that I’m going to
  show you how to set it up quickly, for free. Let’s get started.

  In short, SSL is the "S" in HTTPS. It adds a layer of encryption to HTTP that
  ensures that the recipient is actually who they claim to be and that only
  authorized recipients can decrypt the message to see its contents.
categories:
  - WordPress
  - Security
  - HTTPS
---
If you have an e-commerce website, then SSL is mandatory for safely processing credit cards. But even if you aren’t processing payments, you should still seriously consider secure HTTP (or HTTPS), especially now that I’m going to show you how to set it up quickly, for free. Let’s get started.</p>

## What Is SSL And Why Should I Care?

In short, SSL is the "S" in HTTPS. It adds a layer of encryption to HTTP that ensures that the recipient is actually who they claim to be and that only authorized recipients can decrypt the message to see its contents.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [HTTPS Everywhere With Nginx, Varnish And Apache](https://www.smashingmagazine.com/2015/09/https-everywhere-with-nginx-varnish-apache/)
*   [How To Issue A New SSL Certificate With An Old SSL Key](https://www.smashingmagazine.com/how-to-issue-a-new-ssl-certificate-with-an-old-ssl-key/)
*   [Getting Ready For HTTP/2: A Guide For Web Designers](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)

Sensitive information such as credit-card numbers — basically, anything private — should <em>always</em> be served via HTTPS. However, there is an increasing trend towards serving all content via HTTPS, as we’re seeing on news website, blogs, search engines and the websites of most mainstream brands. So, even if your website isn’t processing payments, there are good reasons to consider HTTPS, a few of which are listed here:

{{% feature-panel %}}

*   **Credibility**.  Even non-technical audiences associate the little green padlock in the browser’s address bar with trust and reliability.
*   **Password protection**.  Perhaps your website only hosts kitten videos. But if users are logging into your website via Wi-Fi with a password that they also use for online banking, then you are potentially facilitating a serious security breach by broadcasting those credentials publicly.
*   **Future-proofing**.  Many websites are still served via HTTP, but there is an undeniable trend towards HTTPS, and this will only increase as users become increasingly educated about web security. Be on the right side of history.
*   **SEO**.  Google officially announced that [HTTPS is used as a ranking signal](https://googlewebmastercentral.blogspot.co.id/2014/08/https-as-ranking-signal.html). In other words, Google is rewarding HTTPS websites by boosting their rankings in search results.

A common argument against HTTPS is that it reduces performance. True, the process of encrypting and decrypting does cost additional milliseconds, but in most situations it is negligible, as evidenced by the fact that performance-conscious companies such as Google and Facebook serve all of their content via HTTPS. And, true, HTTPS can exacerbate existing performance problems, like many CSS files being served individually, but this is mitigated by following basic best practices for performance. And with the adoption of HTTP/2, the performance cost of HTTPS is even lower. The bottom line is that the reduction in performance is a meaningful deterrent only if your website is either hyperoptimized or so underperforming that every millisecond matters.</p>

## How To Set Up HTTPS For Free

The first step to setting up HTTPS for free is to sign up for a cloud DNS service. If you have no idea what DNS is, I recommend that you take a minute to learn before proceeding. The delightful <a href="https://howdns.works/">How DNS Works</a> does a great job of breaking it down into a quippy cartoon. Otherwise, simply know that DNS is the system whereby domain names like <code>example.com</code> (which humans understand) get linked to IP addresses like <code>104.28.2.167</code> (which computers understand). You have many options, but I’m a fan of CloudFlare because it’s really fast to set up, the dashboard is intuitive, and a free plan is available with many powerful features.</p>

### Setting Up CloudFlare

After registering for a CloudFlare account, you’ll be walked through an easy wizard to configure your first website, which will conclude with instructions on how to log into your domain registrar and point the nameservers to CloudFlare. The change will take some time to propagate, but when it’s complete, CloudFlare will be hosting your website’s DNS records. Next, turn on CloudFlare’s "flexible SSL" feature.</p>

<figure><a href="/wp-content/uploads/2016/01/01-flex-ssl-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a47e66d-de8a-4658-99dc-0d25b09da103/01-flex-ssl-preview-opt.png" alt="CloudFlare dashboard" /></a><figcaption>CloudFlare dashboard with SSL setting (<a href="/wp-content/uploads/2016/01/01-flex-ssl-opt.png">View large version</a>)</figcaption></figure>

Choosing the "flexible SSL" setting is important because it doesn’t require you to buy and install your own SSL certificate on your website’s server. Here’s a diagram of what’s happening.</p>

<figure><a href="/wp-content/uploads/2016/01/02-security-illustration-ssl-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab992754-246a-4815-9c39-fce0f7e753c0/02-security-illustration-ssl-preview-opt.png" alt="CloudFlare flexible SSL diagram" /></a><figcaption>CloudFlare flexible SSL diagram (<a href="/wp-content/uploads/2016/01/02-security-illustration-ssl-opt.png">View large version</a>)</figcaption></figure>

As you can see, CloudFlare is acting as the middleman to secure traffic between your website and the client. If this were a static HTML website, you would now be able to connect to it via HTTPS (<code>https://yourdomain.com</code>). WordPress, however, requires additional configuration in order to work with the modified protocol.</p>

## Reconfiguring WordPress From HTTP To HTTPS

You will first need to update the "WordPress Address" and "Site Address" settings in the dashboard, under "Settings" → "General." When you do this, you will have to log into the dashboard again.</p>

<figure><a href="/wp-content/uploads/2016/01/03-dashboard-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4265358a-69bd-4db2-8723-aff0c95cf9bf/03-dashboard-preview-opt.png" alt="WordPress dashboard" /></a><figcaption>WordPress dashboard with URL settings (<a href="/wp-content/uploads/2016/01/03-dashboard-opt.png">View large version</a>)</figcaption></figure>

Proceed cautiously. If you update these settings prematurely, you risk locking yourself out. For example, if the website isn’t yet properly configured for HTTPS and the settings are updated, you could cause a redirect loop that breaks the website and prevents you from accessing the dashboard.

At this point, you should be able to visit the home page of the website via HTTPS. However, page links will still point to the HTTP URLs. WordPress stores links to pages and images as absoute URLs, meaning that the full URL, including the protocol, is saved in the database. To ensure that the entire website is consistently served via HTTPS (without spitting up warnings about mixed content), you will need to update your legacy content.</p>

### Updating Legacy Content

On a small website with only a few pages, the quickest option might be simply to manually update the URLs by editing existing pages in the admin interface. If the website is large or has a highly active blog, then manual editing likely isn’t practical. If your host provides phpMyAdmin or some other interface to run MySQL queries, you could do this pretty easily with a few MySQL queries in the SQL tab. Alternatively, you could follow <a href="https://thecustomizewindows.com/2014/09/mysql-queries-change-wordpress-http-https/">The Customize Windows’ instructions</a> to do it from the command line.

At the risk of stating the obvious, <strong>replace <code>yourdomain.com</code> in the following queries with your actual domain</strong>. Also, if you’ve customized WordPress’ table prefix, replace <code>wp_</code> with the relevant prefix.</p>

<span style="text-decoration: line-through">First, update the URLs of the posts and pages.</span>

<pre><code class="language-sql">UPDATE wp_posts SET guid = replace(guid, 'https://yourdomain.com','https://yourdomain.com');
</code></pre>

&nbsp;

[UPDATE: As discussed in the comments, <a href="https://codex.wordpress.org/Changing_The_Site_URL#Important_GUID_Note">the guid field should not be edited</a>.]

Update the <code>wp_postmeta</code> table, too.</p>

<pre><code class="language-sql">UPDATE wp_postmeta SET meta_value = replace(meta_value,'https://yourdomain.com','https://yourdomain.com');</code></pre>

Finally, update the actual contents of posts or pages. This will update any backlinks to HTTPS.</p>

<pre><code class="language-sql">UPDATE wp_posts SET post_content = REPLACE(post_content, 'https://yourdomain.com', 'https://yourdomain.com');</code></pre>

After running these queries, you will want to refresh your permalinks by going to "Settings" → "Permalinks." Simply change the setting back to the default, and then set it back to whatever setting you were originally using.

Now, you should be able to click the menus and links throughout the website, and the protocol should remain HTTPS.

## Troubleshooting Mixed-Content Warnings

Depending on the theme and plugins in use, you might get a warning in the address bar stating that certain resources are not being served securely. If the errors are associated with assets added by your own custom theme or plugin, make sure to properly <a href="https://codex.wordpress.org/Function_Reference/wp_enqueue_script">enqueue JavaScript</a> and <a href="https://codex.wordpress.org/Function_Reference/wp_enqueue_style">CSS files</a> and not to hardcode URLs that begin with <code>HTTP</code>. Most browsers will let you expand the warning to show the specific requests that are causing the error. You could also try a free plugin such as <a href="https://wordpress.org/plugins/ssl-insecure-content-fixer/">SSL Insecure Content Fixer</a>, which will attempt to correct third-party plugins that have failed to do this.

By this point, you should see the green padlock in the URL bar when visiting your website. If you aren’t using an e-commerce plugin such as WooCommerce or WP eCommerce, you’re done! If you are, there is an important last step.</p>

## Getting Flexible SSL To Work With E-Commerce Plugins

WordPress has a core function named <a href="https://codex.wordpress.org/Function_Reference/is_ssl"><code>is_SSL()</code></a> that plugins rely on to determine whether traffic is encrypted with SSL. With the method above alone, this function will return <code>false</code> because the encryption is only between CloudFlare and the client. The traffic that PHP interacts with is unencrypted, so the super global that that function checks (i.e. <code>$_SERVER['HTTPS']</code>) would not be useful. For our purpose, the relevant variable is <code>$_SERVER['HTTP_X_FORWARDED_PROTO']</code>, which, at the time of writing, WordPress does not recognize. The <a href="https://wordpress.org/support/topic/request-modify-is_ssl-function-to-check-for-http_x_forwarded_proto">request to change this</a> is long-standing, but it is yet to be resolved.</p>

<span id="freeplugin">Fortunately</span>, a free plugin will fix this for you immediately, <a href="https://wordpress.org/plugins/cloudflare-flexible-ssl/">CloudFlare Flexible SSL</a>. Simply install the plugin and activate it. Remember that this technique <strong>does not add any more security</strong>. Traffic between CloudFlare and your website’s server is still unencrypted and, therefore, still vulnerable to sniffing.</p>

## Flexible SSL Is Not Full SSL

CloudFlare’s "Universal SSL" initiative is an interesting attempt to make the Internet more secure, but it is not without controversy. The primary concern is that flexible SSL does not encrypt the second half of the traffic’s journey (to your server), yet the browser currently still shows the same green padlock that we have come to associate with <em>complete</em> SSL. <a href="https://blog.cloudflare.com/introducing-universal-ssl/">CloudFlare offers the following justification</a> on its blog:
<blockquote>Having cutting-edge encryption may not seem important to a small blog, but it is critical to advancing the encrypted-by-default future of the Internet. Every byte, however seemingly mundane, that flows encrypted across the Internet makes it more difficult for those who wish to intercept, throttle, or censor the web. In other words, ensuring your personal blog is available over HTTPS makes it more likely that a human rights organization or social media service or independent journalist will be accessible around the world. Together we can do great things.</blockquote>

For better or worse, flexible SSL is here, and the Internet will have to adapt. In the meantime, the burden is on website owners to be educated and to make responsible decisions.</p>

## Redirecting HTTP Requests To HTTPS

Enabling a website to run on HTTPS does not ensure that requests will actually use the protocol. If your website has been around for a while, users might have already bookmarked it with HTTP. You can redirect all HTTP requests to the new protocol by adding the following snippet to the top of the <code>.htaccess</code> file in the root of your website. If the file does not exist, you can safely add it.</p>

<pre><code class="language-http">&lt;IfModule mod_rewrite.c&gt;
    RewriteEngine On
    RewriteCond %{HTTP:X-Forwarded-Proto} !https
    RewriteRule (.*) https://yourdomain.com/$1 [R=301,L]
&lt;/IfModule&gt;</code></pre>

If an <code>.htaccess</code> file already exists, be careful not to change anything between the <code># BEGIN WordPress</code> and <code># END WordPress</code> lines in that file. Those lines are managed by WordPress, and whenever the permalinks get refreshed, the contents in that section get overwritten.</p>

## Congratulations

By upgrading your website to HTTPS, you have improved your website, protected users and participated in the advancement of the Internet. And it didn’t cost you anything!

{{< signature "dp, al, il" >}}


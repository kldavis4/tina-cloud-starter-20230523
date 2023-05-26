---
title: A Comprehensive WordPress Checklist To Creating The Perfect Website
slug: 15-step-checklist-creating-perfect-wordpress-website
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dc06153-10c7-4f21-81fc-f40b665364e8/wordpress-files-illu101.jpg
date: 2011-12-14T15:52:07.000Z
author: danny-cooper
description: >-
  There is no doubt that WordPress is the best content management system (CMS)
  for your website. Sure, countless CMS’ are available, ranging from open-source
  to paid, and you’ll hear evangelists on all sides swearing that their choice
  is the best. But Drupal, Joomla or any other CMS doesn’t hold a candle to
  WordPress for its ease of use, security and reliability.
categories:
  - WordPress
  - Themes
  - Tutorials
  - Techniques (WP)
---
There is no doubt that WordPress <em>is</em> the best content management system (CMS) for your website. Sure, countless CMS’ are available, ranging from open-source to paid, and you’ll hear evangelists on all sides swearing that their choice is the best. But Drupal, Joomla or any other CMS doesn’t hold a candle to WordPress for its ease of use, security and reliability.

![wordpress checklist](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87852184-123f-4cd8-9d81-382ad2242521/wp-config.jpg "A Comprehensive WordPress Checklist To Creating The Perfect WordPress Website")

It’s no wonder that Web developers have built over 50 million websites on its sturdy back, or that so many designers would never dream of using anything else. For the sake of this article, let’s agree that WordPress is the way to go, no looking back. With that established, let’s lay out a 15-step checklist to help you create the perfect WordPress website.</p>

## Choose A Domain

Without a domain, users wouldn’t be able to find or share your website. In case you’re unsure, <code>facebook.com</code> is a domain, as is <code>https://www.google.com</code>. The <code>https://</code> and <code>www.</code> are optional. Websites will work whether or not you type in the prefix. We’re referring to the rest when discussing domain selection.

{{% feature-panel %}}

There are four key elements to a domain: top-level domain, root domain, subdomain and subfolder:

### Top-Level Domain

The top-level domain, or TLD, is the end of the domain. The most ubiquitous TLD and the one you will be most familiar with is <code>.com</code>. Because <code>.com</code> is the first TLD that comes to mind, it is sought after the most by far, which is why most great <code>.com</code> domains are already owned.

There are many different TLDs, some created exclusively for organizations (<code>.gov</code>, <code>.edu</code>), some specific to countries (<code>.co.uk</code>, <code>.us</code>, <code>.es</code>) and some used most often as an alternative to <code>.com</code> (<code>.net</code>, <code>.org</code> <code>.info</code>).</p>

### Root Domain

Unlike the TLD, you have full control over your root domain; <code><strong>example</strong>.com</code> is a root domain. We have tremendous freedom in choosing root domains. The only two restrictions when registering a domain are that it be unique (i.e. it isn’t currently registered) and that it consist only of letters, numbers and hyphens.

Purchasing domains that have already been registered is also possible, but they usually command much higher prices. A good domain should be concise, memorable, unique, easy to spell and easy to pronounce.</p>

### Subdomains

A subdomain is the domain that appears before the root domain; <code><strong>sub</strong>.example.com</code>, for example. Once you own a root domain, you can create subdomains at no additional cost.</p>

### Subfolders

Subfolders are listed after the TLD; for example, <code>domain.com/<strong>subfolder</strong></code>. SEOmoz has an <a href="https://www.seomoz.org/blog/understanding-root-domains-subdomains-vs-subfolders-microsites">in-depth article on the intricacies of domains</a> relative to search engine optimization.

<strong>Articles on choosing a domain:</strong>

*   [The Effective Strategy for Choosing the Right Domain Names](https://www.smashingmagazine.com/2009/05/02/the-effective-strategy-for-choosing-right-domain-names/)

<strong>Where to buy a domain:</strong>

*   [iWantMyName](https://iwantmyname.com/)
*   [GoDaddy](https://www.godaddy.com/)
*   [Sedo](https://sedo.co.uk/)

## Choose A Hosting Package

Choosing the right host and package is extremely important. Get it wrong and your website will suffer. A host should empower you, never limit you. For example, some hosting packages allow only a single domain, so if you plan on having multiple websites (which many people do), these wouldn’t work.

When choosing a host, look for three key elements:

<strong>Limitations</strong>:

*   Does the host support WordPress?
*   How many domains can you host?
*   How much bandwidth and storage are you allocated?
*   What up-time percentage are you guaranteed?

<strong>Company:</strong>

*   How long has the company been in business?
*   Does it have positive reviews by users?
*   What kind of support does it offer?

<strong>Pricing:</strong>

*   How much is the package you need?
*   Are upgrades available if required?
*   Are there any additional costs (IP addresses, software, etc.)?
*   Is there a trial period?

The best hosting recommendations will come from friends and colleagues, because they will have first-hand experience to share. Here are some reputable hosting providers, in case you don’t know anyone with experience:

*   [Media Temple](https://mediatemple.net),
*   [FireHost](https://firehost.com),
*   VPS.net.

There are also high-quality WordPress-specific hosting companies that can take care of everything for you. Rather than simply host your website, they install and configure WordPress and support you every step of the way.

<strong>WordPress-specific hosting providers:</strong>

*   [Page.ly](https://page.ly/)
*   [WP Engine](https://wpengine.com/)
*   [ZippyKid](https://zippykid.com/)
*   [outstandingSETUP](https://outstandingsetup.com/)

<strong>Articles on hosting providers</strong>

*   [9 Steps to a Happy Relationship With Your Hosting Provider](https://www.smashingmagazine.com/2009/03/29/9-steps-to-a-happy-relationship-with-your-hosting-provider/)

## Configure The Nameservers

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd47a3f5-2df5-4ea6-9eee-f849d46e5d30/nameservers.jpg" alt="nameservers" width="550" height="300" /></figure>

(If your domain came with your hosting package, this step is not required.)

Once you have both a domain and hosting account, you will need to point the domain to your host’s nameservers, to connect the domain name to the server. When you signed up, your hosting provider should have sent you the names of the nameservers. They look something like <code>ns1.nameserver.com</code> and <code>ns2.nameserver.com</code>.

Navigate to your domain’s control panel, and search for something along the lines of “change nameservers.” This is where you will enter the nameservers. Once this step is completed, you will have to wait up to 24 hours for the change to propagate. You will know that it’s working if your domain shows your host’s landing page when you enter the URL in a browser.

If you can’t locate where to change the nameservers, do not hesitate to contact your domain registrar. It would be happy to point you in the right direction.</p>

## Upload WordPress

Download and unzip the <a href="https://wordpress.org/">latest version of WordPress</a>, and then upload it to your hosting account using FTP. FTP stands for “file transfer protocol”; it is a method of transferring files between a computer and hosting server.

To upload files using FTP, you must first download and install an FTP client program, such as <a href="https://filezilla-project.org/">FileZilla</a> (the one I use). FileZilla will ask for your FTP credentials (host name, user name and password). Your host will already have given you these; if not, request them.

Once you have connected to your server via FTP, you will be presented with a list of folders. Search for one named <code>public_html</code> or the name of your domain. This is where you will upload WordPress.

If you want your website to be on the root domain, upload it directly. If you want to install WordPress in a subfolder, you must first create the folder and then upload the files there. Many people install WordPress in a subfolder (such as <code>example.com/blog</code>), but this is not required.

<strong>Articles on uploading WordPress:</strong>

*   [Uploading WordPress to a Remote Host](https://codex.wordpress.org/Uploading_WordPress_to_a_remote_host)

## Create A Database

A database is where all your WordPress data is stored, including your content (i.e. posts, pages and comments), configurations and user data. Each time a page loads, WordPress queries the database for all of the required information, such as title, content, categories, tags and published date.

Using your host’s control panel, create a database and a database user name and password for WordPress to connect with. If you are unsure how to complete this step, your host will be able to assist you.

<strong>Articles on creating a database:</strong>

*   “[Creating a MySQL Database in cPanel](https://youtube.com/watch?v=nfM0xNwkAMA)”

## Modify wp-config-sample.php

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87852184-123f-4cd8-9d81-382ad2242521/wp-config.jpg" alt="wp-config" width="550" height="204" /></figure>

Once you have set up the database and its user name and password, it’s time to use the FTP client to edit the <code>wp-config-sample.php</code> file.

First, rename the file to <code>wp-config.php</code> (i.e. remove <code>sample</code>). Then, using a text editor, open the file.

<pre><code class="language-php">/** The name of the database for WordPress */

define('DB_NAME', <strong>'database_name_here'</strong>);

/** MySQL database username */

define('DB_USER', <strong>'username_here'</strong>);

/** MySQL database password */

define('DB_PASSWORD', <strong>'password_here'</strong>);</code></pre>

Find these lines, and replace the placeholders with your credentials. Then save your edited file to the server.</p>

## Install WordPress

Head to your domain. WordPress will request some basic information to complete the installation and create your account. The process is short and self-explanatory.

<strong>Security tip:</strong> Do not use the user name <code>admin</code> because it is too easily guessed by hackers.

Once you have submitted this information, you will be able to log into the admin panel at <code>yourdomain.com/wp-admin</code>. You will also receive a confirmation email.</p>

## Choose A Theme

Your WordPress theme is the design foundation for your website. Literally thousands of free and premium themes are available, or you could have one custom designed, although this option is substantially more expensive.

Whether your website is about design, food, real estate or pretty much anything else, you’ll find themes tailored to your needs. But finding the perfect one can feel like a never-ending quest.

Here are the absolute minimum requirements for the perfect theme:

*   Great design,
*   Valid HTML and CSS,
*   Rock-solid code,
*   Strong readability,
*   Compatibility with the latest version of WordPress,
*   Compatibility with the most popular plugins,
*   Extensive support and documentation.

With the space being so competitive, all reputable theme providers will offer these features as standard.

With your foundation in place, ask yourself a few questions to ensure the theme is ideal:

*   Does this theme meet all of my requirements?
*   Can it be customized?
*   How quickly will I outgrow this theme?
*   Do any of its color schemes match my brand?

A website should focus more on what your customers like and what they will respond to than on your personal preference. People get lost in their own personal style all too often. If your blog is personal, that’s fine. But if it’s for business, then you <em>must</em> put customers first.

<strong>Places to buy WordPress themes:</strong>

*   [ThemeForest](https://themeforest.net)
*   [WooThemes](https://www.woothemes.com/)
*   [StudioPress](https://www.studiopress.com/)

<strong>Articles about WordPress themes</strong>

*   [A Review of Customer Service and Support Models of Premium WordPress Shops](https://www.smashingmagazine.com/2011/06/15/a-review-of-customer-service-and-support-models-of-premium-wordpress-shops/)

## Configure The Basics

Once you have installed WordPress and picked out a few potential themes, you should make a few basic configurations that will dramatically improve the website.

*   **Activate Akismet**.  Akismet is the number one tool for detecting spam comments. Fortunately, it comes built into WordPress. You will need to [activate it and generate an API key](https://akismet.com/). If you don’t plan to allow comments on your articles, this step isn’t required.
*   **Disable comments**.  If you don’t want to allow comments, navigate to Settings → Discussion, and uncheck “Allow people to post comments on new articles.” This setting can be overridden in each post.
*   **Configure permalinks**.  By default, WordPress URLs look like `example.com?p=232`. By enabling the custom permalink structure (Settings → Permalinks) and pasting in `%postname%`, your URLs will be much friendlier to search engines and RSS readers. For example, for a page titled “WordPress checklist,” the URL would be `example.com/wordpress-checklist`. You can customize the URL of each post even after having customized the permalink structure.
*   **Add Gravatar**.  A Gravatar is an image associated with and linked to your email address. Comments are a perfect example of Gravatars in use. Some themes also have author boxes that feature Gravatars. The great thing about a Gravatar is that you need to [set it up only once](https://en.gravatar.com/), and then your image will load wherever your email address appears in a Gravatar-enabled location.

<strong>Articles about WordPress basics:</strong>

*   “WordPress: The Complete Post-Install Checklist” [Offline]

## Secure WordPress

WordPress is relatively secure out of the box, and its few weaknesses can be ironed out with little effort. Note, however, that no website is 100% secure. Your aim is simply to make it as hard as possible for someone to exploit the website.

No matter how much you invest in security, as long as your website is live, there is a chance it will be exploited, which is just one reason why backing up is so important. Also, the points we’ll cover here relate only to WordPress security, whereas hackers can attack from all angles; there have been cases of hosting providers being exploited, leaving their customers vulnerable.

*   **Keep WordPress up to date.**.  Many WordPress updates contain functional upgrades as well as security fixes. Do not leave yourself exposed to old exploits.
*   **Do not use `wp_` as the database table’s prefix.** Many WordPress users leave the database table’s prefix as the default, `wp_`, allowing malicious hackers to search for that specifically in their exploits. By changing the prefix to something unique, you make the database less vulnerable.
*   **Remove the WordPress version from the website’s header.** By telling malicious users which version of WordPress you are running, you might be inadvertently telling them how to exploit your website, especially if the version is outdated.
*   **Remove admin user name.**.  Malicious users know that a large percentage of users will have the user name `admin`. This means that they need to discover only a single piece of data: your password. By using a unique user name, they would have to guess twice as much data.

The above tweaks need not be done manually. The <a href="https://wordpress.org/extend/plugins/wp-security-scan/">WP Security Scan</a> plugin does some of these things automatically and can assist you with completing the others.

One final recommendation is to make your file permissions as strict as possible without preventing you from performing essential tasks such as uploading media from within the admin area. In my experience, setting all directories as <code>755</code> and all files as <code>644</code> is best, although you might need to set <code>wp-content/uploads</code> to <code>777</code> in order to allow uploads from within the admin area.

<strong>Articles about securing WordPress:</strong>

*   “[10 Steps to Securing Your WordPress Installation](https://wp.tutsplus.com/tutorials/10-steps-to-securing-your-wordpress-installation/)”
*   “[Hardening WordPress](https://codex.wordpress.org/Hardening_WordPress)”

## Create Essential Pages

When someone stumbles on your blog, you want them to be able to find everything they need as quickly as possible. You want to make it <strong>easy</strong>. That means having a few basic pages that will help you help them <strong>quickly</strong>.

*   **Home page**.  The is the landing page for your website. It can be either a static page that explains a little about you or your business, or a dynamic page that updates with each new blog post. By default, WordPress displays a list of your latest blog posts. If you would like a static page to be shown instead, first create that page, and then navigate to Settings → Reading and enable the static page.
*   **About page**.  If you’re not using the home page as a static landing page, then the “About” page is an ideal place to discuss you and your company. Present yourself in the best possible light by saying who are you, where you come from and why that should matter to visitors. Make the copy on this page informative and, if possible, a bit intriguing.
*   **Contact page**.  Visitors to your website might want to reach you and would expect to be able to do so with the ease of a click, which is the exact purpose of the contact page. Whether you use a form plugin or simply display an email address, the contact page makes it dead simple for people to connect with you.
*   **Products, services or “hire me” page** You probably aren’t building the website for fun. Whether you’re selling a service or have a full-blown e-commerce website with merchandise ready to ship, the product page is essential to your revenue. Make it easy to see your offerings and as simple and quick as possible for users to find exactly what they’re looking for.</p>

## Optimize For Search Engines

Search engine optimization (SEO) is essential to ensuring that your copy draws as much targeted traffic as possible. Some themes come with built-in SEO features, and while this is great, I prefer to use a plugin so that my settings are uniform across all of my websites, regardless of the theme. The best SEO plugin available at the moment is <a href="https://wordpress.org/extend/plugins/wordpress-seo/">WordPress SEO by Yoast</a>.

Here are its most important features:

*   **Generation of XML site map**.  A site map is a search engine-friendly map of all of your pages. No theme has this functionality built in, and most SEO plugins don’t include it either.
*   **Site-wide and post-level control of meta data**.  Being able to control the title and meta description of each page is essential to optimizing for search engines, because they are shown in the results when someone performs a search on Google.
*   **Control of `noindex` and `nofollow`** Being able to control which pages search engines index helps to avoid problems with duplicate content, and it also keeps the wrong pages from showing up in results.

<strong>Articles about WordPress SEO:</strong>

*   “[WordPress SEO: The Definitive Guide to Higher Rankings for Your Blog](https://yoast.com/articles/wordpress-seo/)”
*   “[WordPress SEO: The Only Guide You Need](https://www.viperchill.com/wordpress-seo/)”

## Set Up Analytics

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd4add55-ca9b-4a48-8e7c-c4e7db48e86e/analytics.jpg" alt="analytics" width="550" height="204" /></figure>

Analytics enables you to track visitors, with a ton of useful data on their browsing, such as:

*   How they landed on your website,
*   How long they stayed,
*   How many pages they viewed,
*   Which pages they viewed.

The most popular analytics software is <a href="https://www.google.com/analytics/">Google Analytics</a>, because it has pretty much everything you’ll need and is entirely free to use, no matter how big or small the website. Installing it is also extremely simple. All you have to do is create a Google Analytics account, and then place the JavaScript code you are given just before the <code>&lt;/body&gt;</code> tag in your theme’s footer file (usually <code>footer.php</code>).

<strong>Articles about analytics:</strong>

*   [A Guide to Google Analytics and Useful Tools](https://www.smashingmagazine.com/2009/07/16/a-guide-to-google-analytics-and-useful-tools/)

## Back Up

Backing up is undoubtedly the most important item on this list. If something goes wrong and you haven’t set up a back-up system, you could lose all of your online assets. Fortunately, there are multiple fantastic solutions. The most vital thing is to back up both the database and your files, not just one or the other.

*   [VaultPress](https://vaultpress.com) Owned by Automattic (the creator of WordPress), VaultPress is certainly the most reputable back-up solution. Plans start at $15 per month.
*   BackupBuddy This back-up solution has been around longer than VaultPress and allows you to back up content to your server, Amazon S3 or an email address. It also has a one-time cost, starting at $75 for two websites.
*   [WP-DB-Backup](https://wordpress.org/extend/plugins/wp-db-backup/) This plugin backs up only your database and then emails it to you. The problem with backing up only the database is that while your content will be saved, you will lose your themes, plugins and modifications. WP-DB-Backup is free.

<strong>Articles about backing up:</strong>

*   “5 Great Backup Plugins For WordPress”

## Set Up Caching

Every time a page is loaded by a user, WordPress processes that page on your server. This involves retrieving the title and content from the database and executing other processes. But if multiple people are viewing the exact same page, why not display a static version rather than process the page for every instance?

That is exactly what the <a href="https://wordpress.org/extend/plugins/w3-total-cache/">W3 Total Cache</a> plugin does.

The plugin also offers features such as minification, which strips all white space from your HTML, CSS and JavaScript files. Minification also combines CSS and JavaScript files; so, instead of making many calls, the browser makes just one for CSS and another for JavaScript. In short, minification makes your files smaller and, therefore, faster to load.

Simply by activating W3 Total Cache and leaving the default configuration, you could double or triple your blog’s speed while reducing server load.

<strong>Articles about caching:</strong>

*   “[WordPress Caching: What’s the best Caching Plugin?](https://www.tutorial9.net/tutorials/web-tutorials/wordpress-caching-whats-the-best-caching-plugin/)”

## Summary

In helping you choose a domain and hosting provider, install WordPress, select a theme, optimize the website for search engines, and install analytics to monitor traffic, this 15-point checklist is your bulletproof guide to building a quality website without wasting time.

It gives you everything you need to get a high-quality WordPress website up and running in very little time. Of course, if you want someone else to take care of everything for you, there are companies that offer high-quality and affordable solutions.

Don’t forget to bookmark this page in case you need it later. And best of luck with your new WordPress website!

<em>(al) (il) (vf)</em>


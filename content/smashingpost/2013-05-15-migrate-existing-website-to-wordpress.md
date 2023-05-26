---
title: Migrating A Website To WordPress Is Easier Than You Think
slug: migrate-existing-website-to-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/470fc769-711e-4c5c-9f27-bdc4f3c24ff6/wp-12.jpg
date: 2013-05-15T07:28:25.000Z
author: jonathan-wold
description: >-
  Now powering over 17% of the Web, WordPress is increasingly becoming the content management system (CMS) of choice for the average user. But what about websites built with an outdated CMS or without a CMS at all? Does moving to WordPress mean starting over and losing all the time, energy and money put into the current website? Nope!
categories:
  - WordPress
  - Themes
  - Techniques (WP)
---
Now powering over 17% of the Web, WordPress is increasingly becoming the content management system (CMS) of choice for the average user. But what about websites built with an outdated CMS or without a CMS at all? Does moving to WordPress mean starting over and losing all the time, energy and money put into the current website? Nope!

Migrating a website (including the design) over to WordPress is actually easier than you might think. In this guide, we’ll outline the migration process and work through the steps with a sample project. We’ll also cover some of the challenges you might encounter and review the solutions.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Moving A WordPress Website Without Hassle](https://www.smashingmagazine.com/2013/04/moving-wordpress-website/)
*   [Getting Ready For HTTP/2: A Guide For Web Designers And Developers](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)
*   [Free SSL For Any WordPress Website](https://www.smashingmagazine.com/2016/06/free-ssl-for-any-wordpress-website/)

{{% feature-panel %}}

## About This Guide

Before we get to work, let’s establish some context. First, this guide was written primarily with <strong>beginners</strong> in mind and will be most helpful for <strong>basic</strong> websites. Some of you will likely encounter advanced aspects of WordPress migration, but they are beyond the scope of this guide. If you’re tackling an advanced migration and get stuck, feel free to share your difficulty in the comments below.</p>

### Objectives

The objective of this guide is to help you with the following:

*   Plan an effective migration to WordPress.
*   Walk through the technical steps involved in migrating.
*   Get ideas and resources to solve common migration challenges.</p>

### Assumptions

I assume you have basic familiarity with WordPress. Previous development experience with WordPress would be helpful, but not necessary. I also assume you have an existing website and design that you want to migrate to WordPress.</p>

### Basic Steps

Here are the basic steps that I recommend you follow for a typical WordPress migration:

1.  **Evaluate website.** Work carefully through the pages on your existing website, identifying all of the types of content (standard pages, photo galleries, resource pages, etc.) and noting any areas that need special attention.
2.  **Set up environment.** Set up WordPress and get ready to import.
3.  **Import content.** Bring over and organize your content, whether via an importing tool, manual entry (for a small amount, when no tool is available) or a custom importing process.
4.  **Migrate design.** Incorporate your existing design into a custom WordPress theme.
5.  **Review website, go live.** Carefully review the import, making adjustments where needed, set up any URL redirects, and then go live.

With this outline in mind, let’s work through each step in detail.</p>

## Start With A Plan

The key to a successful migration is to carefully evaluate your current website. You need to figure out how to import and structure the content in WordPress before carrying over the design.

While the principles are the same across migration projects, <strong>the details often vary</strong>. So, below are two lists of questions to ask as you work out a plan.</p>

### Imported Content

*   How much content needs to be imported (number of pages, number of images, etc.)?
*   Is the volume low enough to be imported manually, or do you need a tool?
*   If you need a tool, does one already exist?
*   Can the content be categorized into the standard “posts” and “pages,” or does it call for custom post types?
*   Does extra content need to be stored for certain pages (custom fields, taxonomies, etc.)?
*   Will the URL structure change? If so, will the old URLs need to be redirected?

### Existing Functionality

*   Does the website integrate any third-party services (data collection, reservations, etc.)?
*   Do any forms need to be migrated (contact forms, application forms, etc.)?
*   Is access to any content restricted (such as members-only content)?
*   Does the website sell products (digital or physical)?
*   Do any administrative tools need to be carried over (such as custom CMS functionality)?

### A Working Example

My brother, Joshua Wold, has volunteered a website to serve as an example; it’s for a side project of his in which he sells posters and postcards of a <a href="https://www.veganfoodpyramid.com/">Vegan Food Pyramid</a>. He built the website in plain HTML, with some basic PHP includes for the header and footer. Below is a screencast of me evaluating the website to give you a sense of how the process will work. Enjoy!

## Set Up WordPress

Before importing the content, we need to get WordPress ready to go. If you’re just experimenting or if you prefer offline development, start with a <a href="https://codex.wordpress.org/Installing_WordPress#Local_Installation_Instructions">local installation of WordPress</a>. Otherwise, the next step is to install WordPress with your current hosting provider; or you could use the migration process as a great opportunity to move to a new host.

Once WordPress is up and running, you’re ready for action!

<img loading="lazy" decoding="async" class="108882" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0789379d-e3ef-47b3-b48f-e4c6e028d4be/image-3-compressed.png" alt="Setting Up WordPress" width="500" height="350" />

For our example, we’ve installed WordPress with the same host, setting it up in a <code>/wp</code> directory for the duration of the migration process.</p>

### Settings and Plugins

With WordPress installed, we’ll make a few minor adjustments:

*   **Update permalinks.**.  Go to `Settings → Permalinks` to make changes. In most cases, I’ll switch to “postname”-style permalinks.
*   **Update users.**.  I create an admin-level account for myself and any admin or editor accounts that are needed for clients and collaborators. I also remove the default “admin” user name if it exists (a basic but wise step for WordPress security).

Depending on the needs of the project, we might have to preinstall plugins. Here are the major categories of plugins:

*   **Form management**.  Migrating a form “as is” is usually a mess; simply recreating it using a forms plugin is usually easier. My current favorite is [Gravity Forms](https://www.gravityforms.com/) ($39+ per license). Other options are [Formidable](https://wordpress.org/extend/plugins/formidable/) (with free and pro versions) and [Contact Form 7](https://wordpress.org/extend/plugins/contact-form-7/) (entirely free).
*   **SEO management**.  Search engine optimization (SEO) is a touchy subject. My philosophy is to build content for people, not for search engines. That being said, there is a common-sense approach to SEO that is solidly supported by the WordPress plugin ecosystem. And if your old website includes custom meta descriptions, giving them a new home during the importing process is important. I recommend [WordPress SEO](https://wordpress.org/extend/plugins/wordpress-seo/) (free).
*   **Multiple languages**.  If your old website supports multiple languages, WordPress has you covered. My plugin of choice is [WPML](https://wpml.org/) ($79 per license, free for non-profits). Another option is [MultilingualPress](https://wordpress.org/plugins/multilingual-press/) (free).
*   **Security**.  WordPress security is a topic near and dear to me. The increasing popularity of WordPress has made it a target for security attacks. WordPress itself is rarely the problem; a poorly secured hosting environment or an outdated or poorly developed plugin usually is. I use managed WordPress hosting for the majority of my projects, which offers a good foundation for solid WordPress security. Options include [WPEngine](https://wpengine.com/), [ZippyKid](https://pressable.com/), [Pagely](https://page.ly/) and [Synthesis](https://websynthesis.com/). In addition to managed hosting (and especially if you opt for a non-managed host), consider installing a security plugin, such as [Better WP Security](https://wordpress.org/extend/plugins/better-wp-security/) (free) or [Wordfence](https://wordpress.org/extend/plugins/wordfence/) (also free). Last but not least, review the “[Hardening WordPress](https://codex.wordpress.org/Hardening_WordPress)” guide in the Codex.
*   **Backups**.  If you opt for managed hosting, backups are usually included (make sure, though). If you’re managing backups yourself or you want an extra layer of data protection, great options are available, including [VaultPress](https://vaultpress.com/) ($15+ a month), [CodeGuard](https://www.codeguard.com/) ($5+ a month), [BackupBuddy](https://ithemes.com/purchase/backupbuddy/) ($75+ per license) and [BackWPup](https://wordpress.org/extend/plugins/backwpup/) (free).

## Import Content

With WordPress up and running, it’s time to bring over all of your content.

If your old website has a CMS, an importing tool might be available. Start by viewing the list of <a href="https://codex.wordpress.org/Importing_Content">content-importing scripts</a> in the Codex. If there’s a match, great! Follow the instructions and get to work. If all goes well, you’ll have migrated the content over without any trouble.

If your old CMS is not in the list or you don’t have a CMS at all and you’ve got fewer than 100 pages, then manual migration is probably the way to go. Copy and paste the contents, noting the old URLs as you go (tracking the migration in a spreadsheet is a good idea).

<img loading="lazy" decoding="async" class="108883" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db45c275-f16f-4de5-8513-37da5bfef617/image-4-compressed.png" alt="4" width="500" height="350" />

If you’ve got a custom CMS or a database of records without an importing tool and a high volume of content, then you might want to <strong>bring in a specialist to move the content</strong> over before continuing. The higher the volume of content, the higher the chance of human error and the more important automating it becomes.

For our project, I’ve migrated the content manually and replaced the existing navigation with a WordPress menu. You can watch the process in this next screencast:

## Bring Over The Design

With our content in WordPress, it’s time to bring over the design. Incidentally, if you’re considering a new design, then now is a great time to look at the many excellent WordPress themes out there, both in the <a href="https://wordpress.org/extend/themes/">official repository</a> and in third-party marketplaces such as <a href="https://themeforest.net/category/wordpress">ThemeForest</a> and <a href="https://creativemarket.com/themes/wordpress/">Creative Market</a>. For our purpose, I’ll assume that you’re happy with your design.</p>

### Evaluating A Design

Evaluate the source code of a prospective design as best you can before tackling the migration. If the code is table-based or more complex than you’re comfortable with, then migrating the design might not be worth the effort. While anything is possible (I’ve migrated some complex table-based designs in my time), <strong>not everything is practical.</strong>

### Working With Source Code

In my experience, the easiest way to migrate is to work directly with the source code in the browser. While having access to the original hosting environment can be helpful (especially when working with a lot of images and downloadable files), the ways that websites are built vary so widely that you’ll often have to reverse-engineer the original architecture in order to derive anything useful.

<img loading="lazy" decoding="async" class="108884" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c280c630-b317-4f9c-aa0d-7e38f48ac5fe/image-5-compressed.png" alt="5" width="500" height="350" />

Going directly to the source code in your browser of choice will save a lot of time and, barring any important “behind the scenes” functionality, give you everything you need. <a href="https://www.google.com/chrome/">Google Chrome</a> is currently my browser of choice, and I’ve pulled our source-code samples directly from the browser. (In Chrome, go to <code>Menu → Tools → View Source</code>, or just right-click to bring up the contextual menu.)

## Create A Custom Theme

If you’re new to them, <a href="https://codex.wordpress.org/Using_Themes">learn about using themes</a> in the Codex. For the migration process, you can either build a new WordPress theme from the ground up or modify an existing theme to meet your needs. I recommend the latter.

Most of my migration projects have started with the latest version of WordPress’ default theme (currently <a href="https://wordpress.org/extend/themes/twentytwelve">Twenty Twelve</a>). Recently, I stripped down the default theme to create my own migration starter theme, which I’ll use in our example and which <a href="https://github.com/sirjonathan/migration-theme/">you’re welcome to use yourself</a>. (Feel free to suggest improvements!) Let’s get to work.

<a href="https://github.com/sirjonathan/migration-theme/archive/master.zip">Download a copy</a> (ZIP) of the migration starter theme or follow along in your own theme of choice as we work through the relevant theme files.</p>

## 1\. Style Sheet

Our first step is to bring over the styles from the old website. In most cases, this is as simple as searching the source code for references to <code>.css</code> and then copying and pasting the contents from those style sheet(s) into our own <code>style.css</code>. Let’s get to it.

1.  Open up `style.css`.
2.  Replace the details of the theme (“Name,” “URI,” “Description,” etc.) with your own.
3.  Paste in the styles from the old website.</p>

### A Note About Images

As you migrate the style sheet(s), search for and update any references to images. In general, I like to keep all images in an <code>/images/</code> folder within the theme’s directory. More often than not, changing the locations of images referenced in the original CSS is necessary, and I make sure to update all references in the style sheet and templates accordingly.</p>

## 2\. Header

The next step is to create the header for our new theme. Our objective here is to merge the structure of the current code base with WordPress’ templates. Here’s what we’re going to do:

*   Replicate the HTML structure of the old website.
*   Replace the static menu with a WordPress-powered menu.
*   Use WordPress’ `title` tag and leave the `wp_head` hook in place.
*   Merge any other relevant tags from the old header.

Let’s get into the code!

### Original HTML

<pre><code class="language-markup html">
&lt;!DOCTYPE HTML&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Vegan Food Pyramid posters, postcards and wallpapers&lt;/title&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8" /&gt;
&lt;meta name="google-site-verification" content="PO3bWDpUEh4O6XXwnmfyfxrKRDf8JsRrNIcGdzv3POs" /&gt;
&lt;link rel="stylesheet" type="text/css" href="style.css" media="screen" /&gt;
&lt;link rel="shortcut icon" href="https://www.veganfoodpyramid.com/favicon.ico?v=2" /&gt;
&lt;script type="text/javascript" src="//use.typekit.net/tty6xpj.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;try{Typekit.load();}catch(e){}&lt;/script&gt;

&lt;/head&gt;
&lt;body&gt;
&lt;a href="https://veganfoodpyramid.com"&gt;&lt;h1 id="logo"&gt;Vegan Food Pyramid&lt;/h1&gt;&lt;/a&gt;
&lt;ul class="menu"&gt;
   &lt;li&gt;&lt;a class="active" href="https://veganfoodpyramid.com"&gt;Products&lt;/a&gt;&lt;/li&gt;
   &lt;li&gt;&lt;a href="https://veganfoodpyramid.com/wallpaper.php"&gt;Wallpaper&lt;/a&gt;&lt;/li&gt;
   &lt;li&gt;&lt;a href="https://veganfoodpyramid.com/about.php"&gt;About&lt;/a&gt;&lt;/li&gt;
   &lt;li&gt;&lt;a href="https://veganfoodpyramid.com/contact.php"&gt;Contact&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

### Merged Header (header.php)

<pre><code class="language-markup php">
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
   &lt;title&gt;&lt;?php wp_title( '|', true, 'right' ); ?&gt;&lt;/title&gt;
   &lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8" /&gt;
   &lt;meta name="google-site-verification" content="PO3bWDpUEh4O6XXwnmfyfxrKRDf8JsRrNIcGdzv3POs" /&gt;
   &lt;link rel="shortcut icon" href="https://www.veganfoodpyramid.com/favicon.ico?v=2" /&gt;
   &lt;script type="text/javascript" src="//use.typekit.net/tty6xpj.js"&gt;&lt;/script&gt;
   &lt;script type="text/javascript"&gt;try{Typekit.load();}catch(e){}&lt;/script&gt;
   &lt;?php wp_head(); ?&gt;
&lt;/head&gt;

&lt;body &lt;?php body_class(); ?&gt;&gt;

   &lt;header&gt;
      &lt;a href="https://veganfoodpyramid.com"&gt;&lt;h1 id="logo"&gt;Vegan Food Pyramid&lt;/h1&gt;&lt;/a&gt;
      &lt;?php wp_nav_menu( array(
            'theme_location' =&gt; 'primary',
            'container' =&gt; false,
            'menu_class' =&gt; 'menu'
      ) ); ?&gt;
   &lt;/header&gt;
</code></pre>

### Explanation

One of the challenges of migration is deciding whether to improve code as you go along. Our project has a few areas that could be improved, but Joshua and I agreed to leave them as is. Most of you will be tackling the migration of a design that hasn’t been coded to current best practices (although, in fairness to the original coder, they may have been best practices at the time).

<img loading="lazy" decoding="async" class="108885" title="Website Review" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e909d6b-aaa8-4641-b878-0a323d671d70/image-6-compressed.png" alt="Website Review" width="500" height="350" />

<strong>If time and opportunity allow, I encourage you to improve on the code.</strong> Otherwise, take comfort in the fact that, with the website now on WordPress, improvements will be a whole lot easier down the road.

Let’s work through the changes we’ve made!

*   **Doctype**.  Make sure to carry over the same doctype. In this case, the original HTML already has an HTML5 doctype (a relatively rare occurrence on old websites). Using a modern doctype in a code base written for an older specification (such as XHTML or HTML4) could break the layout (especially in old browsers).
*   **Meta tags**.  I usually bring over the majority of meta tags as is, replacing them in WordPress. The exception in our case is the reference to the style sheet, which is being inserted automatically via [`wp_enqueue_style`](https://codex.wordpress.org/Function_Reference/wp_enqueue_style) in the `functions.php` file.
*   **Scripts**.  Scripts can be tricky. If a script belongs on every page (such as a tracking script or font script), then putting it directly in the header (or footer) file is fine. If it needs to appear only on certain pages, then a [conditional tag](https://codex.wordpress.org/Conditional_Tags) will do the trick. As a best practice, register all scripts and add them to the header (or footer) via [`wp_enqueue_script`](https://codex.wordpress.org/Function_Reference/wp_enqueue_script). If you’re up for the challenge, I recommend doing it this way. (Check out a [tutorial on enqueuing TypeKit](https://wptheming.com/2013/02/typekit-code-snippet/) the right way.)
*   **wp_head**.  Leave `<?php wp_head(); ?>` at the bottom of the `</head>` tag in the merged header file. WordPress uses [`wp_head`](https://codex.wordpress.org/Plugin_API/Action_Reference/wp_head), among other things, to enqueue scripts and style sheets that are referenced in the theme (usually in `functions.php`) and in plugins that you’ve installed. Without `wp_head` in place, most front-end plugins won’t work.
*   **body_class**.  Notice our use of the `<?php body_class(); ?>` tag. WordPress uses this to provide a series of helpful classes to the `<body>` tag depending on the page being viewed. In our example, the `<body>` classes weren’t being used. Yours might have unique IDs or classes on each page, in which case you can create a custom function using conditional tags to add the appropriate classes to the corresponding pages. [Have a look at the Codex](https://codex.wordpress.org/Function_Reference/body_class) for some examples.
*   **WordPress menus**.  Switching to a WordPress-powered menu is one of the more complex tasks in most basic migrations. It will be fairly straightforward for us. We have a menu with simple markup that uses an `active` class (generated via PHP) to indicate which page the visitor is viewing. The [`wp_nav_menu`](https://codex.wordpress.org/Function_Reference/wp_nav_menu) function is highly flexible and offers built-in functionality to handle the current state of an element in the menu. I’ve updated the references in the style sheet to the `active` class and changed them to use the equivalent generated by `wp_nav_menu`, which is `current-menu-item`. Watch the screencast on importing content to see how I’ve set up the menu for our example.

And that’s a wrap! Let’s move on to the next piece.</p>

## 3\. Footer

The footer is usually the most uneventful template in the migration process. As with the header, our objective is to merge the relevant parts of the original source code. Let’s get to it!

### Original HTML

<pre><code class="language-markup html">
&lt;div id="footer"&gt;&lt;p&gt;© 2013 VeganFoodPyramid.com&lt;/p&gt;&lt;/div&gt;

&lt;script type="text/javascript"&gt;
var gaJsHost = (("https:" == document.location.protocol) ? "https://ssl." : "https://www.");
document.write(unescape("%3Cscript src='" + gaJsHost + "google-analytics.com/ga.js' type='text/javascript'%3E%3C/script%3E"));
&lt;/script&gt;
&lt;script type="text/javascript"&gt;
try {
var pageTracker = _gat._getTracker("UA-6992755-1");
pageTracker._trackPageview();
} catch(err) {}&lt;/script&gt;

&lt;/body&gt;
&lt;/html&gt;
</code></pre>

### Merged Footer (footer.php)

<pre><code class="language-markup php">
&lt;div id="footer"&gt;&lt;p&gt;© &lt;?php echo date('Y'); ?&gt; VeganFoodPyramid.com&lt;/p&gt;&lt;/div&gt;

&lt;script type="text/javascript"&gt;
var gaJsHost = (("https:" == document.location.protocol) ? "https://ssl." : "https://www.");
document.write(unescape("%3Cscript src='" + gaJsHost + "google-analytics.com/ga.js' type='text/javascript'%3E%3C/script%3E"));
&lt;/script&gt;
&lt;script type="text/javascript"&gt;
try {
var pageTracker = _gat._getTracker("UA-6992755-1");
pageTracker._trackPageview();
} catch(err) {}&lt;/script&gt;

&lt;?php wp_footer(); ?&gt;

&lt;/body&gt;
&lt;/html&gt;
</code></pre>

### Explanation

Some footers are hard to migrate (such as ones with complex menus and widgets), but most are simple. In this case, we’ve merged the HTML with our footer template, making sure to preserve our reference to the <a href="https://codex.wordpress.org/Function_Reference/wp_footer"><code>wp_footer</code></a> hook. We’ve also changed the date reference to use PHP, ensuring that it updates with each year.</p>

## 4\. Home Page

One of the challenges of a migration is that there are so many different ways to get the job done. The home page is a good illustration of this because it tends to be the most different from the rest of the website. Adopting the simplest method is usually best. I’ve opted to put all of the home page’s content directly in the template. Changes will be rare and can easily be made by editing the template.

Let’s look at the code, excluding the header and footer, which we’ve already covered.</p>

### Original HTML

<pre><code class="language-markup html">
&lt;div id="content"&gt;

&lt;div id="poster"&gt;
&lt;a href="https://veganfoodpyramid.com/images/Vegan-Food-Pyramid-New.jpg"&gt;&lt;img class="product-img" src="https://veganfoodpyramid.com/images/Vegan-Food-Pyramid-New.jpg" /&gt;&lt;/a&gt;
&lt;div class="description"&gt;
&lt;h2&gt;Poster&lt;/h2&gt;
&lt;p&gt;A 30×20-inch poster illustrating over 125 vegan food items as an alternative to the traditional food pyramid. This poster will catch people’s attention and serve as a suggestion for food ideas.&lt;/p&gt;
&lt;h3&gt;$30 each&lt;/h3&gt;
&lt;p&gt;Includes free shipping worldwide&lt;/p&gt;
&lt;a class="button" href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&amp;hosted_button_id=2FKQT879CXYYG"&gt;Buy&lt;/a&gt;
&lt;/div&gt;
&lt;/div&gt;

&lt;div id="postcard"&gt;
&lt;a href="https://veganfoodpyramid.com/images/Vegan-Food-Pyramid-New.jpg"&gt;&lt;img class="product-img" src="https://veganfoodpyramid.com/images/postcard-splash.jpg" alt="Postcard Splash" /&gt;&lt;/a&gt;
&lt;div class="description"&gt;
&lt;h2&gt;Postcards&lt;/h2&gt;
&lt;p&gt;Beautiful 4×6 postcards that can be mailed and shared with friends and family. Hand them out at events. Post them on walls. Share the vegan love!&lt;/p&gt;
&lt;h3&gt;$50 for 50&lt;/h3&gt;
&lt;p&gt;Includes free shipping worldwide&lt;/p&gt;
&lt;a class="button" href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&amp;hosted_button_id=EN387WHNSSFMW"&gt;Buy&lt;/a&gt;
&lt;/div&gt;
&lt;/div&gt;

&lt;/div&gt; &lt;!-- end content --&gt;
</code></pre>

### Merged Home Page (/page-templates/front-page.php)

<pre><code class="language-markup php">
&lt;?php
/**
 * Template Name: Front Page Template
 */

get_header(); ?&gt;

&lt;div id="content"&gt;

   &lt;div id="poster"&gt;
      &lt;a href="&lt;?php echo get_stylesheet_directory_uri(); ?&gt;/images/Vegan-Food-Pyramid-New.jpg"&gt;&lt;img class="product-img" src="&lt;?php echo get_stylesheet_directory_uri(); ?&gt;/images/Vegan-Food-Pyramid-New.jpg" /&gt;&lt;/a&gt;
      &lt;div class="description"&gt;
         &lt;h2&gt;Poster&lt;/h2&gt;
         &lt;p&gt;A 30×20-inch poster illustrating over 125 vegan food items as an alternative to the traditional food pyramid. This poster will catch people’s attention and serve as a suggestion for food ideas.&lt;/p&gt;
         &lt;h3&gt;$30 each&lt;/h3&gt;
         &lt;p&gt;Includes free shipping worldwide&lt;/p&gt;
         &lt;a class="button" href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&amp;hosted_button_id=2FKQT879CXYYG"&gt;Buy&lt;/a&gt;
      &lt;/div&gt;
   &lt;/div&gt;

   &lt;div id="postcard"&gt;
      &lt;a href="&lt;?php echo get_stylesheet_directory_uri(); ?&gt;/images/Vegan-Food-Pyramid-New.jpg"&gt;&lt;img class="product-img" src="&lt;?php echo get_stylesheet_directory_uri(); ?&gt;/images/postcard-splash.jpg" alt="Postcard Splash" /&gt;&lt;/a&gt;
      &lt;div class="description"&gt;
         &lt;h2&gt;Postcards&lt;/h2&gt;
         &lt;p&gt;Beautiful 4×6 postcards that can be mailed and shared with friends and family. Hand them out at events. Post them on walls. Share the vegan love!&lt;/p&gt;
         &lt;h3&gt;$50 for 50&lt;/h3&gt;
         &lt;p&gt;Includes free shipping worldwide&lt;/p&gt;
         &lt;a class="button" href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&amp;hosted_button_id=EN387WHNSSFMW"&gt;Buy&lt;/a&gt;
      &lt;/div&gt;
   &lt;/div&gt;

&lt;/div&gt; &lt;!-- end #content --&gt;

&lt;?php get_footer(); ?&gt;
</code></pre>

### Explanation

The <code>front-page.php</code> template begins and ends with a reference to the header and footer that we’ve just prepared. In between, we’ll merge the rest of the HTML, and we’ll use the <a href="https://codex.wordpress.org/Function_Reference/get_stylesheet_directory_uri"><code>get_stylesheet_directory_uri</code></a> function, which will dynamically generate references to the images folder in our new theme.</p>

## 5\. Standard Page Template

With the header and footer done, the standard templates are usually quite easy. For brevity’s sake, we’ll go directly to the merged templates.</p>

### Merged Template (page.php)

<pre><code class="language-markup php">
&lt;?php
/**
 * The template for displaying all pages.
 */

get_header(); ?&gt;

&lt;div id="content"&gt;

   &lt;?php while ( have_posts() ) : the_post(); ?&gt;

      &lt;?php get_template_part( 'content', 'page' ); ?&gt;

   &lt;?php endwhile; ?&gt;

&lt;/div&gt;

&lt;?php get_footer(); ?&gt;
</code></pre>

### Content Template (content-page.php)

<pre><code class="language-markup php">
&lt;?php
/**
 * The template used for displaying page content in page.php
 */
?&gt;

   &lt;article &lt;?php post_class(); ?&gt;&gt;
      &lt;?php the_content(); ?&gt;
   &lt;/article&gt;

</code></pre>

### Explanation

There are several items to point out here:

*   **The loop**.  If you’re new to WordPress or programming in general, this piece of code in the `#content` container might look intimidating. The “loop” is code used by WordPress to display a post’s content. You can [learn more about the loop](https://codex.wordpress.org/The_Loop) in the Codex. Meanwhile, just make sure that it’s in there, or else the content you save in WordPress won’t show up.
*   **get_template_part**.  Our page template here employs the handy [`get_template_part`](https://codex.wordpress.org/Function_Reference/get_template_part) function, which is a great way to keep content organized, especially in complex projects. Our website is simple enough not to warrant it, but I left it in just to show you.
*   **post_class**.  I also added a reference to `<article>` (with the corresponding [`post_class`](https://codex.wordpress.org/Function_Reference/post_class) function) to make further customization of the design easier.</p>

## 5\. Full-Width Template (full-width.php)

Although not illustrated in the screencast, the design includes a full-width template for use on the “Wallpaper” page, while the standard page template is changed to a narrow width.

Let’s have a look.</p>

### Merged Template (templates/full-width.php)

<pre><code class="language-markup php">
&lt;?php
/**
 * Template Name: Full-Width Template
 */

get_header(); ?&gt;

&lt;div id="content" class="full-width"&gt;

   &lt;?php while ( have_posts() ) : the_post(); ?&gt;

      &lt;?php get_template_part( 'content', 'page' ); ?&gt;

   &lt;?php endwhile; ?&gt;

&lt;/div&gt;

&lt;?php get_footer(); ?&gt;
</code></pre>

### Explanation

With the template created, all that remains is to assign it to a page. From the “Edit Page” interface, find the “Page Attributes” box (usually right below the “Publish” box) and select “Full-Width Template” from the “Templates” dropdown menu.</p>

## 6\. Extras

Now let’s tackle some of the “extras” that sometimes come up as challenges during a WordPress migration.

*   **Breadcrumbs**.  Breadcrumbs are relatively common on websites. The easiest way to reproduce them is with a plugin. My current favorite is [Breadcrumb NavXT](https://wordpress.org/extend/plugins/breadcrumb-navxt/) (free). [WordPress SEO](https://wordpress.org/extend/plugins/wordpress-seo/) also offers built-in breadcrumbs.
*   **Widgets**.  If the design you’re migrating has a sidebar, you could either reproduce it as is (the migration theme has a sample sidebar in place) or integrate WordPress widgets to allow for a dynamically managed sidebar. The folks at Automattic have prepared a handy [guide to widgetizing themes](https://automattic.com/code/widgets/themes/). Start there.
*   **Restricted content**.  In case some content needs to be restricted, WordPress offers [basic password protection](https://codex.wordpress.org/Using_Password_Protection) by default. If you want more control, use a plugin. For basic role management and content permissions, I recommend [Members](https://wordpress.org/extend/plugins/members/) (free). For more advanced control (especially if payment is involved), consider [Membership](https://wordpress.org/extend/plugins/membership/) (which has basic and premium versions), [s2Member](https://wordpress.org/extend/plugins/s2member/) (also free and premium) and [WP-Members](https://wordpress.org/extend/plugins/wp-members/) (free).
*   **Custom Post Types**.  Some migrations, especially ones with a lot of different types of content, call for “custom post types.” You can learn about [custom post types in the Codex](https://codex.wordpress.org/Post_Types). To set them up, I recommend using a plugin. Two good choices are [Custom Post Type UI](https://wordpress.org/extend/plugins/custom-post-type-ui/) and [Types](https://wordpress.org/extend/plugins/types/) (both free).</p>

## Review Website

Now that we’ve wrapped up work on the theme, it’s time for a review. Work carefully through the pages on the migrated website. For a large website, focus on the different templates. As you review, here are some things to watch out for:

1.  **Broken links** Make sure all links work as they should. If you have only a few pages, you can check manually. For an automated check, use [Integrity](https://peacockmedia.co.uk/integrity/) (free, for Mac) or [Xenu’s Link Sleuth](https://home.snafu.de/tilman/xenulink.html) (free, for Windows).
2.  **Broken styles** Occasionally, for one reason or another, a design element of your website might have broken during the migration. Carefully compare the old HTML to the new to make sure you haven’t missed any important code and that the corresponding style sheet rules have been carried over. If all else fails, a quick rebuild of the design element on the new website might be in order.
3.  **Broken functionality** Test any functionality that you’ve migrated over, such as “Buy now” buttons, contact forms, newsletter opt-ins, “members-only” content, embedded maps, media players, etc.
4.  **Temporary links** Depending on how you’ve carried out the migration, temporary links to a subfolder or testing domain might appear in your content or theme. You’ll want to update these before going live. Use the [Search and Replace](https://wordpress.org/plugins/better-search-replace/) plugin (free) to check for and update links in your content.</p>

### Setting Up Redirects

If your link structure has changed (and it usually will, even if only slightly), make sure that visitors are redirected from the old pages to the new. For small amounts of content, one of the easiest ways to set up redirects is by adding them to the <code>.htaccess</code> file.

Open the <code>.htaccess</code> file in the WordPress directory. If you don’t see it, set your FTP client to show hidden files. Now, create redirect rules for each of the old pages. Be sure to put these rules <em>after</em> WordPress’ block of rules.

Here are the rewrite rules for our links:

<pre><code class="language-markup">
Redirect 301 /wallpaper.php https://veganfoodpyramid.com/wallpaper/
Redirect 301 /about.php https://veganfoodpyramid.com/about/
Redirect 301 /contact.php https://veganfoodpyramid.com/contact/
Redirect 301 /contactthanks.php https://veganfoodpyramid.com/contact/thanks/
</code></pre>

If editing your <code>.htaccess</code> file is not an option or if you’re dealing with a lot of redirects, then have a look at <a href="https://wordpress.org/extend/plugins/redirection/">Redirection</a> (free).

<strong>Advanced tip:</strong> If the volume of redirects is very high (which is likely with a large-scale migration and a custom importing process), then consider building a function that hooks into <a href="https://codex.wordpress.org/Plugin_API/Action_Reference/template_redirect"><code>template_redirect</code></a>, compares a generated list of cases, and then uses the <a href="https://codex.wordpress.org/Function_Reference/wp_redirect"><code>wp_redirect</code></a> function to redirect any matches.</p>

## Going Live

Going live with a website usually involves one of two tasks:

1.  Relocate WordPress from the development folder to the root directory.
2.  Point the domain name from the old server to the new WordPress server.

<img loading="lazy" decoding="async" class="108886" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbffc05d-d796-4c0f-8e63-b69c8e7ba7fe/image-7-compressed.png" alt="Going Live!" width="500" height="350" />

### Relocating WordPress

If you set up WordPress in a subfolder (as we did), then going live involves a few simple steps. Follow the guide to <a href="https://codex.wordpress.org/Giving_WordPress_Its_Own_Directory#Using_a_pre-existing_subdirectory_install">using a pre-existing subdirectory installation</a>.

Once you’ve made the change, check immediately for any broken links that you may have missed in the final review.</p>

### Pointing to a New Server

If you set up WordPress on a new server, then you probably used a temporary domain. Accordingly, remove references to the temporary domain before pointing the domain to the new server.

Also, if you’re planning to update the name servers for your domain, then first resolve any dependencies in the current DNS records (such as hosted email and third-party services). I usually go live with a domain by updating the A records, leaving the name servers in place.</p>

## Conclusion

And there you have it! <strong>A successful WordPress migration is all about the details</strong>, and while this guide is by no means comprehensive, you now have a good outline of the process and a sense of some of the challenges you’ll encounter, along with ideas for solving them. If you run into challenges along the way, share them in the comments below. Now get migrating!

{{< signature "al" >}}


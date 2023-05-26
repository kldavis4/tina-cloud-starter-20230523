---
title: 10 Useful WordPress Security Tweaks
slug: 10-useful-wordpress-security-tweaks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0b3e89c-bca6-4bdd-94e1-8a6dde50c877/child-playing-airplane.jpg
date: 2010-07-01T13:14:31.000Z
author: jean-baptiste-jung
description: >-
  Security has always been a hot topic. Offline, people buy wired homes, car
  alarms and gadgets to bring their security to the max. Online, security is
  important, too, especially for people who make a living from websites and
  blogs. In this article, we'll show you **some useful tweaks to protect your
  WordPress-powered blog**.

  When you fail to log into a WordPress blog, the CMS displays some info telling
  you what went wrong. This is good if you've forgotten your password, but it
  might also be good for people who want to hack your blog. So, why not prevent
  WordPress from displaying error messages on failed log-ins?
categories:
  - WordPress
  - Security
  - Techniques (WP)
---
Security has always been a hot topic. Offline, people buy wired homes, car alarms and gadgets to bring their security to the max. Online, security is important, too, especially for people who make a living from websites and blogs. In this article, we'll show you some useful tweaks to protect your WordPress-powered blog.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Securing Your WordPress Website](https://www.smashingmagazine.com/2011/11/securing-your-wordpress-website/)
*   [<span class="headline">Common WordPress Malware Infections</span>](https://www.smashingmagazine.com/2012/10/four-malware-infections-wordpress/)
*   [A Comprehensive Checklist To Creating The Perfect WordPress Website](https://www.smashingmagazine.com/2011/12/15-step-checklist-creating-perfect-wordpress-website/)
*   [Learning WordPress: Most Useful Tips and Tutorials](https://www.smashingmagazine.com/learning-wordpress-useful-wordpress-tips-tutorials/)

## 1\. Prevent Unnecessary Info From Being Displayed

<strong>The problem</strong>
When you fail to log into a WordPress blog, the CMS displays some info telling you what went wrong. This is good if you've forgotten your password, but it might also be good for people who want to hack your blog. So, why not prevent WordPress from displaying error messages on failed log-ins?

{{% feature-panel %}}

<strong>The solution</strong>
To remove log-in error messages, simply open your theme's <em>functions.php</em> file, and paste the following code:

<pre><code class="language-php">add_filter('login_errors',create_function('$a', "return null;"));</code></pre>

Save the file, and see for yourself: no more messages are displayed if you fail to log in.

Please note that there are several <em>functions.php</em> files. Be sure to change the one in your <em>wp-content</em> directory.

<strong>Code explanation</strong>
With this code, we've added a simple hook to overwrite the <code>login_errors()</code> function. Because the custom function that we created returns only <code>null</code>, the message displayed will be a blank string.

<strong>Source</strong>

*   [Tips for Securing WordPress](https://themeplayground.com/2009/tutorials/for-wordpress-users/security-tips/)
*   [WordPress Security: Hide Log-In Error Messages](https://www.wprecipes.com/wordpress-security-hide-login-error-messages)

## 2\. Force SSL Usage

<strong>The problem</strong>
If you worry about your data being intercepted, then you could definitely use SSL. In case you don't know what it is, SSL is a cryptographic protocol that secures communications over networks such as the Internet.

Did you know that forcing WordPress to use SSL is possible? Not all hosting services allow you to use SSL, but if you're hosted on Wp WebHost or HostGator, then SSL is enabled.

<strong>The solution</strong>
Once you've checked that your Web server can handle SSL, simply open your <em>wp-config.php</em> file (located at the root of your WordPress installation), and paste the following:

<pre><code class="language-php">define('FORCE_SSL_ADMIN', true);</code></pre>

Save the file, and you're done!

<strong>Code explanation</strong>
Nothing hard here. WordPress uses a lot of constants to configure the software. In this case, we have simply defined the <code>FORCE_SSL_ADMIN</code> constant and set its value to <code>true</code>. This results in WordPress using SSL.

<strong>Source</strong>

*   [How To: Force Using SSL on wp-admin Directory](https://www.wprecipes.com/how-to-force-using-ssl-on-wp-admin-directory)

## 3\. Use .htaccess To Protect The wp-config File

<strong>The problem</strong>
As a WordPress user, you probably know how important the <em>wp-config.php</em> file is. This file contains all of the information required to access your precious database: username, password, server name and so on. Protecting the <em>wp-config.php</em> file is critical, so how about exploiting the power of Apache to this end?

<strong>The solution</strong>
The <em>.htaccess</em> file is located at the root your WordPress installation. After creating a back-up of it (it's such a critical file that we should always have a safe copy), open it up, and paste the following code:

<pre><code class="language-php">&lt;files wp-config.php&gt;
order allow,deny
deny from all
&lt;/files&gt;</code></pre>

<strong>Code explanation</strong><br>
<em>.htaccess</em> files are powerful and one of the best tools to prevent unwanted access to your files. In this code, we have simply created a rule that prevents any access to the <em>wp-admin.php</em> file, thus ensuring that no evil bots can access it.

<strong>Source</strong>

*   [10 Easy Ways to Secure Your WordPress Blog](https://www.catswhocode.com/blog/10-easy-ways-to-secure-your-wordpress-blog)

## 4\. Blacklist Undesired Users And Bots

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42f10558-114b-4826-8be4-49d383435a56/sm4.jpg" alt="Screenshot" />

<strong>The problem</strong>
This is as true online as it is in real life: someone who pesters you today will probably pester you again tomorrow. Have you noticed how many spam bots return to your blog 10 times a day to post their annoying comments? The solution to this problem is quite simple: forbid them access to your blog.

<strong>The solution</strong>
Paste the following code in your <em>.htaccess</em> file, located at the root of your WordPress installation. As I said, <strong>always back up the <em>.htaccess</em> file</strong> before editing it. Also, don't forget to change <code>123.456.789</code> to the IP address you want to ban.

<pre><code class="language-php">&lt;Limit GET POST PUT&gt;
order allow,deny
allow from all
deny from 123.456.789
&lt;/LIMIT&gt;</code></pre>

<strong>Code explanation</strong>
Apache is powerful and can easily be used to ban undesirable people and bots from your website. With this code, we're telling Apache that everyone is allowed to visit our blog except the person with the IP address <code>123.456.789</code>.

To ban more people, simply repeat line 4 of this code on a new line, using another IP address, as shown below:

<pre><code class="language-php">&lt;Limit GET POST PUT&gt;
order allow,deny
allow from all
deny from 123.456.789
deny from 93.121.788
deny from 223.956.789
deny from 128.456.780
&lt;/LIMIT&gt;</code></pre>

<strong>Source</strong>

*   [Over 150 of the Worst Spammers, Scrapers and Crackers from 2007](https://perishablepress.com/press/2008/02/24/over-150-of-the-worst-spammers-scrapers-and-crackers-from-2007/)

## 5\. Protect Your WordPress Blog From Script Injections

<strong>The problem</strong>
Protecting dynamic websites is especially important. Most developers always protect their <code>GET</code> and <code>POST</code> requests, but sometimes this is not enough. We should also protect our blog against script injections and any attempt to modify the PHP <code>GLOBALS</code> and <code>_REQUEST</code> variables.

<strong>The solution</strong>
The following code blocks script injections and any attempts to modify the PHP <code>GLOBALS</code> and <code>_REQUEST</code> variables. Paste it in your <em>.htaccess</em> file (located in the root of your WordPress installation). <strong>Make sure to always back up the <em>.htaccess</em> file</strong> before modifying it.

<pre><code class="language-php">Options +FollowSymLinks
RewriteEngine On
RewriteCond %{QUERY_STRING} (&lt;|%3C).*script.*(&gt;|%3E) [NC,OR]
RewriteCond %{QUERY_STRING} GLOBALS(=|[|%[0-9A-Z]{0,2}) [OR]
RewriteCond %{QUERY_STRING} _REQUEST(=|[|%[0-9A-Z]{0,2})
RewriteRule ^(.*)$ index.php [F,L]</code></pre>

<strong>Code explanation</strong>
Using the power of the <em>.htaccess</em> file, we can check requests. What we've done here is check whether the request contains a &lt;script&gt; and whether it has tried to modify the value of the PHP <code>GLOBALS</code> or <code>_REQUEST</code> variables. If any of these conditions are met, the request is blocked and a 403 error is returned to the client's browser.

<strong>Sources</strong>

*   [Protéger Son Site Avec Un Fichier .htaccess](https://blog.galerie-cesar.com/proteger-son-site-avec-fichier-htaccess/)
*   [Protect Your WordPress Blog Using .htaccess](https://www.wprecipes.com/protect-your-wordpress-blog-using-htaccess)

## 6\. Fight Back Against Content Scrapers

<strong>The problem</strong>
If your blog is the least bit known, people will no doubt try to use your content on their own websites without your consent. One of the biggest problems is hot-linking to your images, which saps your server's bandwidth.

<strong>The solution</strong>
To protect your website against hot-linking and content scrapers, simply paste the following code in your <em>.htaccess</em> file. As always, don't forget to back up when modifying the <em>.htaccess</em> file.

<pre><code class="language-php">RewriteEngine On
#Replace ?mysite.com/ with your blog url
RewriteCond %{HTTP_REFERER} !^https://(.+.)?mysite.com/ [NC]
RewriteCond %{HTTP_REFERER} !^$
#Replace /images/nohotlink.jpg with your "don't hotlink" image url
RewriteRule .*.(jpe?g|gif|bmp|png)$ /images/nohotlink.jpg [L]</code></pre>

Once you've saved the file, only your website will be able to link to your images, or, to be more correct, no one <em>would link</em> to your images, because it would be way too complicated and time-consuming. Other websites will automatically display the <em>nohotlink.jpg</em> image. Note that you can also specify a non-existent image, so websites that try to hot-link to you would display a blank space.

<strong>Code explanation</strong>
With this code, the first thing we've done is check the referrer to see that it matches our blog's URL and it is not empty. If it doesn't, and the file has a JPG, GIF, BMP or PNG extension, then the nohotlink image is displayed instead.

<strong>Source</strong>

*   [How to Protect Your Blog from Content Thieves](https://www.catswhoblog.com/how-to-protect-your-blog-from-content-thieves)

## 7\. Create A Plug-In To Protect Your Blog From Malicious URL Requests

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10c4de34-1fa4-4ab7-af65-935ca03756d5/sm7.jpg" alt="Screenshot" />

<strong>The problem</strong>
Hackers and evil-doers often use malicious queries to find and attack a blog's weak spots. WordPress has good default protection, but enhancing it is possible.

<strong>The solution</strong>
Paste the following code in a text file, and save it as <em>blockbadqueries.php</em>. Once you've done that, upload it to your <code>wp-content/plugins</code> directory and activate it as you would any other plug-in. Now your blog is protected against malicious queries.

<pre><code class="language-php">&lt;?php
/*
Plugin Name: Block Bad Queries
Plugin URI: https://perishablepress.com/press/2009/12/22/protect-wordpress-against-malicious-url-requests/
description: >-
  Protect WordPress Against Malicious URL Requests
Author URI: https://perishablepress.com/
Author: Perishable Press
Version: 1.0
*/

global $user_ID;

if($user_ID) {
  if(!current_user_can('level_10')) {
    if (strlen($_SERVER['REQUEST_URI']) &gt; 255 ||
      strpos($_SERVER['REQUEST_URI'], "eval(") ||
      strpos($_SERVER['REQUEST_URI'], "CONCAT") ||
      strpos($_SERVER['REQUEST_URI'], "UNION+SELECT") ||
      strpos($_SERVER['REQUEST_URI'], "base64")) {
        @header("HTTP/1.1 414 Request-URI Too Long");
  @header("Status: 414 Request-URI Too Long");
  @header("Connection: Close");
  @exit;
    }
  }
}
?&gt;</code></pre>

<strong>Code explanation</strong>
What this code does is pretty simple. It checks for excessively long request strings (more than 255 characters) and for the presence of either the <code>eval</code> or <code>base64</code> PHP functions in the URI. If one of these conditions is met, then the plug-in sends a 414 error to the client's browser.

<strong>Source</strong>

*   [Protect WordPress Against Malicious URL Requests/](https://perishablepress.com/press/2009/12/22/protect-wordpress-against-malicious-url-requests/)

## 8\. Remove Your WordPress Version Number… Seriously!

<strong>The problem</strong>
As you may know, WordPress automatically displays the version you are using in the head of your blog files. This is pretty harmless if your blog is always up to date with the latest version (which is certainly what you should be doing anyway). But if for some reason your blog isn't up to date, WordPress still displays it, and hackers will learn this vital piece of information.

<strong>The solution</strong>
Paste the following line of code in the <em>functions.php</em> file of your theme. Save it, refresh your blog, and voila: no more WordPress version number in the header.

<pre><code class="language-php">remove_action('wp_head', 'wp_generator');</code></pre>

<strong>Code explanation</strong>
To execute certain actions, WordPress uses a mechanism called "hooks," which allow you to hook one function to another. The <code>wp_generator</code> function, which displays the WordPress version, is hooked. We can remove this hook and prevent it from executing by using the <code>remove_action()</code> function.

<strong>Source</strong>

*   [How to Remove the WordPress Version Number (the Right Way)](https://digwp.com/2009/07/remove-wordpress-version-number/)

## 9\. Change The Default "Admin" Username

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f77258d-306d-4e4d-925c-9287b467143a/sm9.jpg" alt="Screenshot" />

<strong>The problem</strong>
Brute force is one of the easiest ways to break a password. The method is simple: try as many different passwords as possible until the right one is found. Users of the brute force method use dictionaries, which give them a lot of password combinations.

But knowing your username certainly makes it easier for them to guess the right combination. This is why you should always change the default "admin" username to something harder to guess.

Note that WordPress 3.0 let you choose your desired username by default. Therefore, this tip is still usefull if you still use the old "admin" account from older WordPress versions.

<strong>The solution</strong>
If you haven't changed the "admin" username yet, simply run the following SQL query to your database to change it for good. Don't forget to specify your desired username.

<pre><code class="language-markup tmp-sql">UPDATE wp_users SET user_login = 'Your New Username' WHERE user_login = 'Admin';</code></pre>

<strong>Code explanation</strong>
Usernames are stored in the database. To change one, a simple <code>UPDATE</code> query is enough. Note that this query will not transfer posts written by "admin" to your new username; the source post below shows you how to easily do that.

<strong>Source</strong>

*   [13 Useful WordPress SQL Queries You Wish You Knew Earlier/](https://www.onextrapixel.com/2010/01/30/13-useful-wordpress-sql-queries-you-wish-you-knew-earlier/)

## 10\. Prevent Directory Browsing

<strong>The problem</strong>
By default, most hosts allow directory listing. So, if you type <code>www.yourblog.com/wp-includes</code> in the browser's address bar, you'll see all of the files in that directory. This is definitely a security risk, because a hacker could see the last time that files were modified and access them.

<strong>The solution (Updated)</strong>
Just add the following to the Apache configuration or your .htaccess file:

<pre><code class="language-php">Options -Indexes</code></pre>

<strong>Code explanation</strong>
Please note that it's not enough to update the blog's <em>robots.txt</em> file with <code>Disallow: /wp*</code>. This would prevent the wp-directory from being indexed, but will not prevent users from seeing it.

<strong>Source</strong>

*   [18 WordPress Security Plug-ins and Tips to Secure Your Blog](https://www.makeuseof.com/tag/18-useful-plugins-and-hacks-to-protect-your-wordpress-blog/)

{{< signature "al" >}}


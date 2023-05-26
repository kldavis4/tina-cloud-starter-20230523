---
title: 10 Steps To Protect The Admin Area In WordPress
slug: 10-steps-to-protect-the-admin-area-in-wordpress
image: null
date: 2009-01-27T06:08:25.000Z
author: afrison
description: >-
  The administration area of a Web application is a favorite target of hackers
  and thus particularly well protected. The same goes for WordPress: when
  creating a blog, the system creates an administrative user with a perfectly
  secure password and blocks public access to the settings area with a log-in
  page. This is the cornerstone of its protection.
categories:
  - WordPress
  - Security
---
The administration area of a Web application is a favorite target of hackers and thus particularly well protected. The same goes for WordPress: when creating a blog, the system creates an administrative user with a perfectly secure password and blocks public access to the settings area with a log-in page. This is the cornerstone of its protection. Let’s dig deeper!

<strong>This article focuses on defending the administration area of WordPress</strong>, meaning all those pages in the <em>wp-admin</em> folder (or https://www.yourblog.com/wp-admin/) that are displayed <strong>after a user a verified</strong>. We highlighted the phrase “after a user is verified” deliberately: it should be explicitly understood that only a simple query stands in the way of an evil hacker and the powerful admin area of your whole blog. The latter is only as strong as the passwords that are generated. 

You might be interested in the following related posts:

*   [<span class="headline">How To Become A Top WordPress Developer</span>](https://www.smashingmagazine.com/2012/08/how-to-become-a-top-wordpress-developer/)
*   [<span class="headline">A Beginner’s Guide To Creating A WordPress Website</span>](https://www.smashingmagazine.com/2016/02/beginners-guide-creating-wordpress-website/)
*   [How To Speed Up Your WordPress Website](https://www.smashingmagazine.com/2014/06/how-to-speed-up-your-wordpress-website/)

To make an attack more difficult, you should perform the following actions manually. These solutions do not guarantee 100% security, but you can create effective stumbling blocks on a hacker’s way to the administration area.

{{% feature-panel %}}

## 1\. Rename and Upload the wordpress Folder

Since version 2.6, it has been possible to change the path of the <em>wp-content</em> directory. Unfortunately, this is still not possible for the <em>wp-admin</em> directory. Security-minded bloggers will just have to accept this fact and hope that this protection of their blog will be made possible in future versions. Until then, the following recipe is a comparable alternative. Upon extracting the zipped WordPress files, you’ll see a folder named Wordpress. This folder should be renamed (ideally to something cryptic), and, after also adjusting the <em>wp-config.php</em> file, uploaded to the root directory of the domain.

What does this change accomplish?

*   First, the files will no longer be loose in the main directory, thus increasing the clarity of the root level. Other files and folders will be found quicker.
*   Secondly, many WordPress instances can now be created and can be put parallel to each other without interfering with other system files and settings, making it perfect for testing and development.
*   The third advantage actually speaks to security: the admin area (and the blog itself) is no longer in the root domain and must first be found by robots. It won’t be easy to find the path of this relocated log-in page, at least for a human. Until then, this change will protect your blog.

<strong>Note</strong>: If the system files of a WordPress blog are no longer in the main directory, and the name of the installation’s main folder has been changed (as recommended above), the blog can still be accessed from <em>https://example.com</em>. How? In the <em>WordPress address (URL)</em> field under the general settings, include the path of the renamed folder. For example, if the unzipped Wordpress folder is renamed to <em>wordpress_live_Ts6K</em>, enter the path as <em>https://example.com/wordpress_live_Ts6K.</em>

Your blog address will remain beautiful and not distracting.</p>

## 2\. Extend the file wp-config.php

The WordPress configuration file <em>wp-config.php</em> contains settings and access data for the database. But security-related values can also be found in the file. The following definitions must be in the <em>wp-config.php</em> file (but may not be) and should be added or modified:

*   **Security keys**: Since WordPress 2.7, WordPress has had four kinds of security keys, which must be set up properly. WordPress saves you from having to come up the strings yourself by [generating](https://api.wordpress.org/secret-key/1.1/) the lines of security keys automatically. You just have to implement these security keys in your configuration file. These keys are essential to the safety of your installed blog.
*   **The table prefix** of a newly created WordPress installation should not be the standard _wp__. The more cryptic the word, the less likely an intrusion into the MySQL database tables will occur. Bad: _$table_prefix = ‘wp_’;_. Much better: _$table_prefix = ‘wp4FZ52Y_’;_. This value is assigned only once and you don’t have to remember it because it has an internal function.
*   If the server has **SSL encryption** available, it is recommended to encrypt the administration area. This can be done by adding the following command to the _wp-config.php_ file: _define(’FORCE_SSL_ADMIN’, true);_
*   In addition, you can adjust other system settings in the configuration file. A clear and comprehensive list of settings for greater safety and performance can be found in the [WordPress Codex](https://codex.wordpress.org/Editing_wp-config.php).</p>

## 3\. Move the wp-config.php file

Also since version 2.6, WordPress allows you to move the <em>wp-config.php</em> file to a higher level. Because this system file contains by far more sensitive information than any other, and because it is difficult to access the parent file server level, it certainly makes sense to store it outside of the actual installation. WordPress automatically looks at the highest underlying index for the configuration settings file. Any attempt by users to adjust the path is thus useless.</p>

## 4\. Protect the wp-config.php file

Not all ISPs, though, allow you to transfer data to a higher level than the main directory. Administrators cannot always execute the previous step if they do not have this privilege. In this case, external access to the <em>wp-config.php</em> file can be excluded via the <em>.htaccess</em> file.

It is important to make sure that the <em>.htaccess</em> file, with this built-in protection, shares the same directory as the <em>wp-config.php</em> file. Incidentally, this technique would also be useful if you use multiple WordPress installations but are not allowed to relocate the relevant configuration files.

## 5\. Delete the _admin_ User Account

When WordPress is installed, an administrator acount with the username <em>admin</em> is automatically created, without any options set. This is a well-intended gesture by WordPress, but a default user with administrative rights and an assigned ID of #1 is an easy target for hackers. In an attack, only the password of this user would have to be broken. Hence our advice:

1.  Create another administrator in the admin area.
2.  Log out of the back end.
3.  Log in as the new user.
4.  Delete the old _admin_ from the user list.

A second user gives greater security: that name will be displayed in all future published articles and commentaries, and the name of the actual administrator will never be displayed on blog pages and therefore never communicated to the outside world.</p>

## 6\. Choose strong passwords

The probability and frequency of attack increases in proportion to the popularity of the blog. And when the back end of a WordPress blog is skillfully attacked, you have to be sure there are no weak links in the chain of security.

More often than not, passwords are the weakest link in this chain. The reason? The way that passwords are usually handled or chosen is too reckless. Numerous studies show that miserably vast numbers of passwords contain too few characters and are too easily guessed.

WordPress responded to this problem with an intuitive indicator, based on a traffic-light visual, that displays the strength of a user’s desired password. Inexplicably, though, this tool is only available for existing profiles (found under Settings &gt; Users &gt; Your profile). If the administrator creates new users, then password strength is not communicated visually.

Our recommendation for a secure WordPress password is that it be at least seven characters long and include uppercase and lowercase characters, numbers and symbols such as <em>! ” ? $ % ^ &amp; )</em>.</p>

## 7\. Protect the wp-admin Directory

Adhering to the motto “Two are better than one,” the administration area is equipped with additional password protection. The query (in WordPress otherwise responsible for Permalinks) is handled by <em>.htaccess</em>, which is stored in the <em>wp-admin</em> folder along with <em>.htpasswd</em>. After making this change, the browser will ask for the data stored in <em>.htaccess</em>. This can be different for each blog author or the same for everyone.

Note: the Htaccess and Htpasswd generator helps to create the necessary files with desired values.</p>

## 8\. Suppress Error Feedback on the Log-In Page

The log-in page of a WordPress installation is the door to the administration area. The administration area is only accessible upon error-free verification. Until successfully logging in, visitors — whether good or bad — have countless attempts to enter the correct data in the log-in fields. In case of a failed attempt, WordPress communicates to the user what the problem might be.

When troubleshooting, WordPress is really fussy and provides a unique, meaningful message for each error. So if a user name is typed incorrectly, that will be communicated. If the password is wrong, that will be also communicated. This is a comfort for the user and a blessing for the thief. Unintentionally, WordPress provides valuable feedback to the bad boys who are trying to access your data. It’s just a matter of time until they gain access to the back end.

A simple one-liner solves this problem cleverly: The output of the error on the log-in page is simply blocked to looters. This code goes in the <em>functions.php</em> file of your theme:

<code>add_filter('login_errors',create_function('$a', "return null;"));</code>

## 9\. Restrict Erroneous Log-In Attempts

WordPress keeps no record of failed attempts to log in, much to the detriment of the blog administrator, who doesn’t see the insidious attack coming and so can’t gather the tools to combat the threat. Is there a way out of this dilemma?

Two solutions exist: <a href="https://www.bad-neighborhood.com/login-lockdown.html">Login LockDown</a> and Limit Login Attempts. Upon being installed, they record all log-in attempts. Furthermore, both extensions can lock out visitors for a specified time after a certain number of failed attempts. Thus, robots and hackers are limited in the scale of their attack.

The extensions are free and compatible with WordPress 2.7.</p>

## 10\. Keep Software Up to Date

Finally, the following should be stated: WordPress developers are very fast and react immediately to vulnerabilities in WordPress. Keep your installations up to date. Since version 2.7, available updates are just a click away. The same goes for plug-ins!

And remember: less is more. As an administrator, you should ensure that only the extensions that are necessary are active in your installation. Every plug-in is a potential risk and should be inactive or, better yet, removed if it is not needed.

{{< signature "al" >}}


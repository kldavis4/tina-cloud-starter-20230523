---
title: A Guide To PHP Error Messages For Designers
slug: a-guide-to-php-error-messages-for-designers
image: null
date: 2011-11-30T11:00:20.000Z
author: rachel-andrew
description: >-
  PHP is widely available with inexpensive hosting plans, which makes it a popular choice for developers who write software for the Web. From big platforms, such as WordPress, down to small scripts, such as ones to display image galleries or to send forms to email, thousands of script and products are out there written in PHP that can be installed and used even if you don’t know much about PHP yourself "A Guide To PHP Error Messages For Designers").
categories:
  - Coding
  - PHP
  - Errors
---
I have been a PHP developer for 10 years, and my company has developed a content management system, written in PHP, that is intended to be very simple to install and get started with. So, I spend a lot of time working with designers who are installing a PHP script for the first time. If you are installing a script and something goes wrong, PHP can be incredibly infuriating. Until you know what they mean, PHP errors can be baffling. My favorite message is:

<pre><code class="language-php tmp-none">Parse error: syntax error, unexpected T_PAAMAYIM_NEKUDOTAYIM</code></pre>

Paamayim Nekudotayim means “double colon” in Hebrew! But <code>double colon</code> is a lot easier to debug than <code>T_PAAMAYIM_NEKUDOTAYIM</code>.

This article is aimed at designers who are not PHP developers but need to install PHP scripts from time to time. Thus, the problems and error messages we will look at here are those you are most likely to encounter when installing scripts, rather than when writing PHP. The tips should help you work through other error messages and should at least help you give clear information to the script’s developer if you need to ask them for assistance.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [PHP: What You Need To Know To Play With The Web](https://www.smashingmagazine.com/2010/04/php-what-you-need-to-know-to-play-with-the-web/)
*   [10 Advanced PHP Tips](https://www.smashingmagazine.com/2009/03/10-useful-php-tips-revisited/)
*   [50 Extremely Useful PHP Tools](https://www.smashingmagazine.com/2009/01/50-extremely-useful-php-tools/)

## All I Get Is A Blank Page!

Before we can diagnose PHP errors, we need to <em>see</em> some PHP errors. Ideally, you would first be installing the script locally, perhaps using MAMP on a Mac or XAMPP, both of which allow you to turn on error messages easily. You can get PHP to just spit the errors out directly on the screen or log them to a file for viewing.

If, however, you are installing a script directly in your hosting account, the host will likely have disabled the display of all PHP error messages. This is sensible for security, because an error message could give away important information about the server or database, but it isn’t so useful if you are trying to configure a script. If error displays have been turned off, then a fatal error before any output is made to the page would result in a blank page. An error that happens after some HTML has been outputted would result in the markup being “cut off” (stopping at the point where the error occurred). If you “View source” and see a completely blank page or half a page or are getting a “500 internal server error,” then a PHP error is probably the culprit.</p>

### Locate the Error Log

On a live server, you should have access to the PHP error log. This is different than the Web server error log, which shows things such as 404 errors when a page or image is not found. The PHP log gives information on errors and warnings in PHP itself. The host should have configured PHP to send errors to a log rather than write them to the screen.

If no error log can be found, then you might be able to configure PHP to maintain one in a location that you specify. To do this, create a directory on your website named <code>errors</code>. Make this directory writable. Then add the code below to the <em>.htaccess</em> file at the root of your website. If you do not have an <em>.htaccess</em> file, create one.

<pre><code class="language-php tmp-none">php_flag  log_errors on
php_flag display_errors off
php_value error_log  /your/path/public_html/errors/php_error.log</code></pre>

Then, protect the <code>errors</code> directory so that the file cannot be downloaded from the Web. You might be able to do this in the control panel or just by creating a new <em>.htaccess</em> file, this time in the <code>errors</code> directory.

<pre><code class="language-php tmp-none">Order allow,deny
Deny from all</code></pre>

If you now run the script that caused the error, the error message should get added to the <em>php_error.log</em> file. If it doesn’t work, try creating the file yourself first in the <code>errors</code> directory and making it writable.

If you have no luck creating an error log, then open a support ticket with your hosting provider, explaining what you are trying to achieve and inquiring how to do it.

## Errors, Notices And Warnings

PHP classifies the messages that go to the error log as either errors, notices or warnings. These have different levels of severity. An error is something broken in your code. It needs fixing and will cause PHP to stop executing.

A warning is essentially PHP saying, “What you’re doing will likely cause a problem, but I’ll try to continue.”

A notice alerts you to something that needs attention in your script. It could be that the version of PHP on your server is newer than the one supported by the script. Things in PHP are deprecated in the same way that elements in the HTML specification get deprecated. When something is deprecated, it means that it will be removed in the future, so the notice lets you know this.

Errors in a purchased or open-source script are most likely an issue with your installation, assuming that your version of PHP meets the requirement. If a script is throwing out warnings that you cannot fix, then you should probably raise them with technical support. You can usually ignore notices, although you should check that the latest version of the script is installed. If a lot of notices are being thrown out, it could indicate a poor-quality script.

If the trick above for turning on error logging worked for you, you can set the level of error reporting in the <em>.htaccess</em> file, too:

<pre><code class="language-php tmp-none">php_flag  log_errors on
php_flag display_errors off
php_value error_log  /your/path/public_html/errors/php_error.log
php_value error_reporting 1</code></pre>

The above will add only errors to the <code>error_log</code>.

<pre><code class="language-php tmp-none">php_flag  log_errors on
php_flag display_errors off
php_value error_log  /your/path/public_html/errors/php_error.log
php_value error_reporting -1</code></pre>

Setting <code>error_reporting</code> to <code>-1</code> will log all errors, warnings and notices. If you do this, then you’ll definitely want to set <code>php_flag display_errors</code> to <code>off</code>, so that notices do not get outputted to your website’s pages.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/030f41cb-d661-4b46-a5d7-6198f49b1bb4/htaccess.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119381" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/030f41cb-d661-4b46-a5d7-6198f49b1bb4/htaccess.png" alt="screenshot" width="500" height="115" /></a>

### The First Error Is The Important One

If you are displaying errors to the page and hit a PHP error, you could run into a terrifying page full of errors. If you are reviewing errors in a log, refresh the page that is generating the error and then check the log. You might find a long set of errors for the same page; they should all have the same time code, helping you to identify them as a set. This usually happens when the first error is a warning; the script tries to continue running but hits more problems related to the initial warning. Fix the initial warning, and you might find that all of the other issues go away.

## Database-Related Errors

Many of the errors people encounter when installing a script have to do with the connection to the database. Usually, when a script needs to make a database connection, you will be asked for four bits of information: the database’s user name and password, the server’s address (which is often, but not always, <code>localhost</code>) and the database’s name. If any of these are incorrect, you won’t be able to connect. Depending on the script, either you will see an ugly string of error messages or, if the developer has handled this gracefully, you will be told that the script was unable to connect to the database.

The database connection issues that I commonly see when providing technical support are as follows:

*   **The user has entered `localhost` instead of an IP address or URL for the database server.** Localhost means that the database is on the same server as your website. Some hosts have different servers for MySQL and so will give you an address for the server that you need to use when configuring the script.
*   **An incorrect user name has been entered.**.  One thing to watch is that cPanel prefixes user names that you create with the account’s name. If your account’s name is `fred` and you create a user named `website`, then the user name to enter when configuring a script would be `fred_website`.
*   **An incorrect database name has been entered.**.  As with user names, cPanel prefixes the database’s name with the account’s name. Check that you are using the prefixed version in your configuration.</p>

### Database Permission Problems

Another possible cause of database-related trouble is when all of the connection details are correct, but the database user doesn’t have the permissions needed to do things that the script needs to do. For example, the script might need to create database tables and so would require the database user to have <code>create</code> permissions.

If you created the database user in cPanel, you would also need to select the database and join the user to it, giving the user enough permissions to run the script. For example, if you were installing WordPress, your database user would need to have <code>All Privileges</code> for the database it is attached to.

In cPanel, you can set these in the section named “Add user to database.” Select the user and database, and then on the next screen, click the “All Privileges” checkbox before submitting the form.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09a62738-44a5-4172-99a9-0666c7868871/privs.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119387" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09a62738-44a5-4172-99a9-0666c7868871/privs.png" alt="screenshot" width="500" height="304" /></a>

## PHP Errors

The next set of errors are those generated by PHP because of some problem with the script that you’re installing or because of something that was introduced while you were installing or configuring it.</p>

### Fatal Error: Call to Undefined Function

<pre><code class="language-php tmp-none">Fatal error: Call to undefined function my_function() in /home/mysite/public_html/test.php on line 2</code></pre>

This means that a PHP function that the current page needs cannot be found. The function might be part of the script itself or built right into PHP. You might see this error when installing a third-party script for the following reasons:

*   If you’re installing a new script, you might not have uploaded all of the files. In my experience, people who use Dreamweaver’s FTP client encounter this issue a lot.
*   If you’re upgrading, you might not have replaced all of the required files. So, an old version that doesn’t contain the function is being used.
*   You might not have added a required PHP include or specified a correct path in a configuration file.
*   A script might be calling a PHP function that is not available on this server. For example, it might be calling `imagecreatefromjpeg()` when the GD image libraries haven’t been installed.

To solve the error, check carefully that all of the files have been uploaded or replaced and that you have followed the installation instructions. If you cannot resolve it, then contact the script’s developer, explaining what you have done and what you have checked and copying the error message.

If the issue is that something is missing in your PHP installation, then you might need to contact your hosting provider.</p>

### Fatal Error: Cannot Redeclare

<pre><code class="language-php tmp-none">Fatal error: Cannot redeclare my_function() (previously declared in /home/mysite/public_html/runtime.php:14) in /home/mysite/public_html/runtime.php on line 26</code></pre>

This usually means that you have included a file twice. Check everywhere you have edited and check included files to make sure you haven’t duplicated an include.</p>

### Fatal Error: Allowed Memory Size Exhausted

<pre><code class="language-php tmp-none">Fatal error: Allowed memory size of 67108864 bytes exhausted (tried to allocate 17472 bytes) in /home/mysite/public_html/lib/Image.class.php on line 198</code></pre>

You will typically see this error when trying to upload and process an image, although you might see it for any script that requires a lot of memory to run. The amount of memory that your scripts are allowed to use is set by the hosting provider. On cheap [shared hosting](https://inmotion-hosting.evyy.net/c/1233229/260033/4222) plans, these limits are often set very low. If you need to use a script to process large images, contact your provider to see whether you can move to a plan with higher limits.</p>

## Permission Errors

<pre><code class="language-php tmp-none">Warning: move_uploaded_file(/home/mysite/public_html/upload/my_cat.jpg) [function.move-uploaded-file]: failed to open stream: Permission denied in /home/mysite/public_html/upload.php on line 49</code></pre>

This warning is an example of a permissions error. The script is trying to upload a file to a directory, but the directory doesn’t have enough permissions for the file to be moved to it. The permissions that PHP needs in order to write to a file or directory depend on how the server is configured and whether you are using a Unix or Windows host. The section on “<a href="https://codex.wordpress.org/Changing_File_Permissions#Permission_Scheme_for_WordPress">Permission Scheme</a>” in the WordPress Codex is relevant even if you are not using WordPress. However, if you get any kind of “Permission denied” error or warning and can’t fix it simply by changing the permissions for the folder, speak with your hosting provider rather than the developer of the script, because your provider will be able to tell you how to do this.</p>

## PHP Warning: Include

<pre><code class="language-php tmp-none">PHP Warning:  include(foo.php): failed to open stream: No such file or directory in /home/mysite/public_html/test.php on line 2</code></pre>

This warning tells you that an include file (included using PHP’s <code>include</code> syntax) was not found. It is a warning rather than an error, because PHP will continue trying to load the page if it cannot find an include.

In PHP, you can include files using <code>include()</code> or <code>require()</code>. If you use <code>require()</code>, then you are telling PHP that this script is vital to running the website, and so PHP will spit out an error if the file is not found, rather than try to continue.

If you get a warning or error message that a file could not be opened, then check that the file referred to in the error message is there and that your path to it is correct. For example, if you have the file <code>/inc/navigation.php</code>, and the page calling this file is in the directory <code>/about</code>, then you would need to include <code>navigation.php</code> with the following include:

<pre><code class="language-php tmp-none">&lt;?php include(../inc/navigation.php); ?&gt;</code></pre>

Omitting the <code>../</code> would result in a warning because PHP would not be able to find the file.</p>

## In Summary

PHP errors can seem very confusing if you are not a PHP developer, but if you read the error message carefully, you will usually find something that leads you to the root of the problem. Most of the errors I see in technical support have to do with incorrect database connections, missing files or permissions. These are all things that someone with no PHP knowledge can identify and fix themselves, just by learning how to access error messages and becoming familiar with what PHP is saying in them. Being able to debug these kinds of problems will save you a lot of frustration and will free you from having to wait for tech support to get back to you.

If you run into an error when installing a script, remember the following:

1.  Learn how to access PHP errors on your server.
2.  Look at the error log to see what the error actually is.
3.  See if you can identify the source of the problem by looking at the initial error message or warning for the script.
4.  If the error seems to involve permissions or an incorrect database configuration, open a ticket with your hosting provider.
5.  If the script is the problem, then open a ticket with the developer, explaining what you have done and copying information from the error log. You will bring joy to their heart if you provide the actual error message rather than say you saw a blank page!

### Further Reading

*   “[Advanced PHP Error Handling Via .htaccess](https://perishablepress.com/press/2008/01/14/advanced-php-error-handling-via-htaccess/),” Jeff Starr, Perishable Press
*   “[Configure Error Log](https://codex.wordpress.org/Editing_wp-config.php#Configure_Error_Log),” WordPress CodexWordPress-specific information on configuring the error log.
*   “[3 Ways to Monitor PHP Errors](https://digwp.com/2009/07/monitor-php-errors-wordpress/),” Jeff Starr, Digging Into WordPressIncludes some other methods of logging errors.

Have you come across a particularly baffling error when installing a script? Have you come across a hosting provider that requires a different method to get error logs working? Add your suggestions in the comments section.

<em>Image source on front page: <a href="https://www.flickr.com/photos/34120957@N04/4199675334/">Alex E. Proimos</a></em>

{{< signature "al" >}}


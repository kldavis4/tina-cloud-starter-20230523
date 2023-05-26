---
title: 'WordPress Local Development For Beginners: From Setup To Deployment'
slug: wordpress-local-development-beginners-setup-deployment
author: nickschaeferhoff
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e352fd7-ab3d-4f5d-b999-4f57bead8bda/02-wordpress-local-development-for-beginners-800w.jpg
date: 2018-04-27T14:00:29+02:00
summary: >-
  Is there a better way to make direct changes to your WordPress website? Yes, there is! Learn how to build a local WordPress environment with XAMPP and how to get your website online once it’s ready to see the light of day.
description: >-
  Is there a better way to make direct changes to your WordPress website? Yes, there is! Learn how to build a local WordPress environment with XAMPP and how to get your website online once it’s ready to see the light of day.
categories:
  - WordPress
---
<p>When first starting out with WordPress, it’s very common to make any changes directly on your live site. After all, where else would you do it? You only have that one site, so when something needs changing, you do it there.</p>

<p>However, this practice has several drawbacks. Most of all that it’s very public. So, when something goes seriously wrong, it’s quite noticeable for people on your site.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Preventing Common Mistakes</h4>
<p>When creating free or premium WordPress themes, you’re bound to make mistakes. Find out how you can avoid them in order to save yourself time and focus on actually creating themes people will enjoy using.  <a href="https://www.smashingmagazine.com/2018/03/prevent-common-wordpress-theme-mistakes/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

<p>It’s ok, don’t feel bad. Most WordPress beginners have done this at one point or another. However, in this article, we want to show you a better way: <strong>local WordPress development</strong>.</p>

<p>What that means is setting up a copy of your website on your local hard drive. Doing so is incredibly useful. So, below we will talk about the benefits of building a local WordPress development environment, how to set one up and how to move your local site to the web when it’s ready.</p>

<p>This is important, so stay tuned!</p>

## The Benefits Of Local WordPress Development

<p>Before diving into the <em>how</em>, let’s have a look at the <em>why</em>. Using a local development version of WordPress offers many benefits.</p>

{{% feature-panel %}}

<p>We already mentioned that you no longer have to make changes to your live site with all the risks involved with that. However, there is more:</p>

<ul>
<li><strong>Test themes and plugins</strong><br />With a local copy of your site, you can try out as many themes and plugin combinations as you want without risking taking your live site out due to incompatibilities.</li>
<li><strong>Update safely</strong><br />Another time when things are prone to go wrong are updates. With a local environment, you can update WordPress core and components to see if there are any problems before applying the updates to your live site.</li>
<li><strong>Independent of an online connection</strong> <br />With your WordPress site on your computer, you can work on it without being connected to the Internet. Thus, you can get work done even if there is no wifi.</li>
<li><strong>High performance/low cost</strong><br />Because site performance is not limited by an online connection, local sites usually run much faster. This makes for a better workflow. Also, as you will see, you can set it all up with free software, eliminating the need for a paid staging area.</li>
</ul>

<p>Sounds good? Then let’s see how to make it happen.</p>

## How To Set Up A Local Development Environment For WordPress

<p>In this next part, we will show you how to set up your own local WordPress environment. First, we will go over what you need to do and then how to get it right.</p>

### Tools You’ll Need

<p>In order to run, WordPress needs a server. That’s true for an online site as well as a local installation. So, we need to find a way to set one up on our computer.</p>

<p>That server also needs some software WordPress requires to work. Namely, that’s PHP (the platform’s main programming language) and MySQL for the database. Plus, it’s nice to have a MySQL user interface like <a href="https://www.phpmyadmin.net">phpMyAdmin</a> to make handling the database more convenient.</p>

<p>In addition to that, need your favorite code editor or IDE (<a href="https://en.wikipedia.org/wiki/Integrated_development_environment">integrated development environment</a>) for the coding part. My choice is <a href="https://notepad-plus-plus.org/&sa=D&ust=1515115581629000&usg=AFQjCNEN0VTbppcuZuo1LJsCm94h88UvGA">Notepad++</a> but you might have your own preferences.</p>

<p>Finally, it’s useful to have some developer tools to analyze and debug your site, for example, to look at HTML and CSS. The easiest way is to use Chrome or Firefox (read <a href="https://www.smashingmagazine.com/2015/12/revisiting-firefox-devtools/&sa=D&ust=1515115581629000&usg=AFQjCNEBaIBIrWQbtsMeqGx7y_VVSGuwAg">our article on Firefox's DevTools</a>), which have extensive functionality like that built in.</p>

### Available Software

<p>We have several options at our disposal to set up local server environments. Some of the most well known are <a href="https://serverpress.com">DesktopServer</a>, <a href="https://www.vagrantup.com">Vagrant</a>, <a href="https://local.getflywheel.com">Local by Flywheel</a>, and <a href="https://www.smashingmagazine.com/2021/06/multiple-wordpress-sites-locally-devkinsta/">DevKinsta</a>. All of these contain the necessary components to set up a local server that WordPress can run on.</p>

<p>For this tutorial we will use <a href="https://www.apachefriends.org/index.html">XAMPP</a>. The name is an acronym and stands for “cross platform, Apache, MySQL, PHP, Perl”. If you have been paying attention, you will notice that we earlier noted MySQL and PHP as essential to running a WordPress website. In addition, Apache is an open source solution for creating servers. So, the software contains everything we need in one neat package. Plus, as “cross platform” suggests, XAMPP is available for both Windows, Mac and Linux computers.</p>

<p>To continue, if you haven’t done so already, head over to <a href="https://www.apachefriends.org/index.html">the official XAMPP website</a> and download a copy.</p>

### How To Use XAMPP

<p>Installing XAMPP pretty much works like every other piece of software.</p>

<p>On Windows:</p>

<ol>
<li>Run the installer (note that you might get a warning about running unknown software, allow to continue).</li>
<li>When asked which components to install, make sure that Apache, MySQL, PHP, and phpMyAdmin are active. The rest is usually unnecessary, deactivate it unless you have good reason not to.</li>
<li>Choose the location to install. Make sure it’s easy to reach as that’s where your sites will be saved and you will probably access them often.</li>
<li>You can disregard the information about Bitnami.</li>
<li>Choose to start the control panel right away at the end.</li>
</ol>

<p>On Mac:</p>

<ol>
<li>Open the .dmg file</li>
<li>Double click on the XAMPP icon or drag it to applications folder</li>
<li>That’s it, well done!</li>
</ol>

<p>After the installation is complete, the control panel starts. Should your operating system ask for Firewall permissions, make sure to allow XAMPP for private networks, otherwise, it won’t work.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf5a4c39-1599-4513-befe-77ff975228bd/08-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf5a4c39-1599-4513-befe-77ff975228bd/08-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>From the panel, you can start Apache and MySQL by clicking the <code>Start</code> buttons on the respective rows. If you run into problems with programs that use the same ports as XAMPP, quit those programs and try to restart the XAMPP processes. If the problem is with Skype, there is a permanent solution by disabling the ports under <code>Tools</code>&nbsp;&rarr;&nbsp;<code>Options</code>&nbsp;&rarr;&nbsp;<code>Advanced</code>&nbsp;&rarr;&nbsp;<code>Connections</code>.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fe39b43-041a-4333-9c53-ff121c241939/04-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fe39b43-041a-4333-9c53-ff121c241939/04-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>Under <code>Config</code>, you can also enable automatic start for the components you need.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/948de10b-9d4b-4c99-a37b-19b91b6f862b/09-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/948de10b-9d4b-4c99-a37b-19b91b6f862b/09-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>After that, it’s time to test your local server. For that, open your browser, and go to <code>https://localhost</code>.</p>

<p>If you see the following screen, everything works as it should. Well done!</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/904e73d5-b228-4b1f-9e4e-1a20dfc6cc31/13-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/904e73d5-b228-4b1f-9e4e-1a20dfc6cc31/13-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

### Installing WordPress Locally

<p>Now that you have a local server, you can install WordPress in the same way that you do on a web server. The only difference: everything is done on your hard drive, not an FTP server or inside a hosting provider’s admin panel.</p>

<p>That means, to create a database for WordPress, you can simply go to <code>https://localhost/phpmyadmin</code>. Here, you find the same options as in the online version and can <a href="https://codex.wordpress.org/Installing_WordPress%23Using_phpMyAdmin&sa=D&ust=1515115581640000&usg=AFQjCNH3rSK4UbV8xEIaM1dljQBLws-5cg">create a database, user and password for WordPress</a>.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71515eed-1c79-4679-973a-b982e763fbab/12-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71515eed-1c79-4679-973a-b982e763fbab/12-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>Once that is done and you want to install WordPress, you can do so via the <code>htdocs</code> folder inside your installation of XAMPP. There, simply create a new directory, download <a href="https://wordpress.org/latest.zip">the latest version of WordPress</a>, unpack the files and copy them into the new folder. After that, you can start the installation by going to <code>https://localhost/newdirectoryname</code>.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c49d899e-13f3-4bb6-8f44-5c32084ee860/01-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c49d899e-13f3-4bb6-8f44-5c32084ee860/01-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>That’s basically it. Now that you have a running copy of WordPress on your website, you can install themes and plugins, <a href="https://www.smashingmagazine.com/2016/01/create-customize-wordpress-child-theme/&sa=D&ust=1515115581642000&usg=AFQjCNFL2cAnqRYIkUGPS-RHJnio9PBSzg">set up a child theme</a>, change styles, <a href="https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/&sa=D&ust=1515115581643000&usg=AFQjCNFXUp0Byb1NFqpe11VErK7KEEkR_A">create custom page templates</a> and do whatever your heart desires.</p>

<p>When you are satisfied, you can then move the website from a local installation to live environment. That’s what we will talk about next.</p>

## How To Deploy Your Site With A Plugin

<p>Alright, once your local site is up to your liking, it’s time to get it online. Just a quick note: if you want to get a copy of your existing live site to your hard drive, you can use the same process as described below only in reverse. The overall principles stay the same.</p>

<p>Either way, we can <a href="https://www.smashingmagazine.com/2013/04/moving-wordpress-website/&sa=D&ust=1515115581644000&usg=AFQjCNHffat6-FHejgiPDdPd570-xVpd7g">do this manually</a> or via plugin and there are several solutions available. For this tutorial, we will use <a href="https://wordpress.org/plugins/duplicator/&sa=D&ust=1515115581644000&usg=AFQjCNFDZDm0iLZ9c8rX5ArHpJJEKO9DmQ">Duplicator</a>. I found it to be one of the most convenient free solutions and, as you will see, it makes things really easy.</p>

### 1. Install Duplicator

<p>Like every other WordPress plugin, you first need to install Duplicator in order to use it. For that, simply go to <code>Plugins</code>&nbsp;&rarr;&nbsp;<code>Add New</code>. In the search box, input the plugin name and hit enter, it should be the first search result.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f17f7da8-b800-405a-8834-ef8b8c7b7c0a/05-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f17f7da8-b800-405a-8834-ef8b8c7b7c0a/05-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>Click <code>Install Now</code> and activate once it’s done.</p>

### 2. Export Site

<p>When Duplicator is active on your site, it adds a new menu item in the WordPress dashboard. Clicking it gets you to this screen.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26d61da4-d53a-4e96-a764-1f2378e0cabe/14-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26d61da4-d53a-4e96-a764-1f2378e0cabe/14-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>Here, you can create a so-called package. In Duplicator that means a zipped up version of your site, database, and an installation file. To get started, simply click on <code>Create New</code>.</p>

<p>In the next step, you can enter a name for your package. However, it’s not really necessary unless you have a specific reason.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/648cc3d6-34ac-4e8c-a55d-c4d0b75c1fc6/10-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/648cc3d6-34ac-4e8c-a55d-c4d0b75c1fc6/10-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>Under <code>Storage</code>, <code>Archive</code>, and <code>Installer</code> are options to determine where to save the archive (works for the Pro version only), exclude files or database tables from the migration and input the updated database credentials and new URL.</p>

<p>In most cases you can just leave everything as is, especially because Duplicator will attempt to fill in the new credentials automatically later. So, for now just hit <code>Next</code>.</p>

<p>After that, Duplicator will run a test to see if there are any problems.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e347651-30dd-421a-add9-87e61a1079a5/07-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e347651-30dd-421a-add9-87e61a1079a5/07-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>Unless something major pops up, just click on <code>Build</code> to begin building the package. This will start the backup process.</p>

<p>At the end of it, you get the option to download the zip file and installer with the click on the respective buttons or with the help of the <code>One-Click Download</code>.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5f2d0fc-2ef2-443b-aff5-063ccc4eb7f1/02-wordpress-local-development-for-beginners-800w.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5f2d0fc-2ef2-443b-aff5-063ccc4eb7f1/02-wordpress-local-development-for-beginners-800w.jpg'>Large preview</a>" alt="" >}}

<p>Do so and you are done with this part of the process.</p>

### 3. Upload And Deploy Files On Your Server

<p>If all of this has gone down without a hitch, it’s now time to upload the generated files to their new home. For that, log into your FTP server and browse to your new site’s home directory. Then, start uploading the files we generated in the last step.</p>

<p>Once done, you can start the installation process by inputting <code>https://yoursite.com/installer.php</code> into the browser bar.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3734fa20-6b01-441f-bf23-faa79b34cb6e/11-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3734fa20-6b01-441f-bf23-faa79b34cb6e/11-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>In the first step, the plugin checks the archive’s integrity and whether it can deploy the site in the current environment. You also get some advanced options that you are welcome to ignore at the moment. However, make sure to check the box where it says “I have read and accept all terms and notices,” before clicking <code>Next</code>.</p>

<p>Your site is now being unpacked. After that, you get to the screen where it’s time to input the database information.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/656b14d8-a681-417c-9bfe-1023c51ee813/03-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/656b14d8-a681-417c-9bfe-1023c51ee813/03-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>The plugin can either create a new database (if your host allows it) or use an existing one. For the latter option, you need to set up the database manually beforehand. Either way, you need to input the database name, username, and password to continue. Duplicator will also use this information to update the <code>wp-config.php</code> file of your site so that it can talk to the new database. Click <code>Test Database</code> to see if the connection works. Hit <code>Next</code> to start the installation of the database.</p>

<p>Once Duplicator is done with that, the final step is to confirm the details of your old and new site.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0778e278-426c-4d04-ab95-26036d53f55a/16-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0778e278-426c-4d04-ab95-26036d53f55a/16-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>That way, Duplicator is able to replace all mentions of your old URL in the database with the new one. If you don’t, your site won’t work properly. If everything is fine, click the button that says <code>Next</code>.</p>

### 4. Finishing Up

<p>Now, there are just a few more things to do before you are finished. The first one is to check the last page of the setup for any problems encountered in the deployment.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce355de3-ea88-484f-bb05-8c9be6012120/06-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce355de3-ea88-484f-bb05-8c9be6012120/06-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>The second is to log into your new site (you can do so via the button). Doing so will land you in the Duplicator menu.</p>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbdffc60-0943-4a6f-bfdf-8cb75b81d7b5/15-wordpress-local-development-for-beginners.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbdffc60-0943-4a6f-bfdf-8cb75b81d7b5/15-wordpress-local-development-for-beginners.jpg'>Large preview</a>" alt="" >}}

<p>Here, be sure to click on <code>Remove Installation Files Now!</code> at the top. This is important for security reasons.</p>

<p>And that’s it, your site should now be successfully migrated. Well done! You have just mastered the basics of local WordPress development.</p>

### Quick Note: Updating Your Database Information Manually

<p>Should the Duplicator plugin for some reason be unable to update <code>wp-config.php</code> with the new database information, your site won’t work and you will see a warning that says “unable to establish database connection”.</p>

<p>In that case, you need to change the information manually. Do this by finding <code>wp-config.php</code> in your WordPress installation’s main folder. You can access it via FTP or a hosting backend like cPanel. Ask your provider for help if you find yourself unable to locate it on your own.</p>

<p>Edit the file (this might mean downloading, editing and re-uploading it) and find the following lines:</p>

<pre><code class="language-bash">/** The name of the database for WordPress */
define('DB_NAME', 'database_name_here');

/** MySQL database username */
define('DB_USER', 'username_here');

/** MySQL database password */
define('DB_PASSWORD', 'password_here');

/** MySQL hostname */
define('DB_HOST', 'localhost');</code></pre>

<p>Update the information here with that of your new host (by replacing the info between the ' '), save the file and move it back to your site’s main directory. Now everything should be fine.</p>

## WordPress Local Development In A Nutshell

<p>Learning how to install WordPress locally is super useful. It enables you to make site changes, run updates, test themes and plugins and more in a risk-free environment. In addition to that, it’s free thanks to open source software.</p>

<p>Above, you have learned how to build a local WordPress environment with XAMPP. We have led you through the installation process and explained how to use the local server with WordPress. We have also covered how to get your local site online once it’s ready to see the light of day.</p>

<p>Hopefully, your takeaway is that all of this is pretty easy. It might feel overwhelming as a beginner at first, however, using WordPress locally will become second nature quickly. Plus, the benefits clearly outweigh the learning process and will help you take your WordPress skills to the next level.</p>

<p>What are your thoughts on local WordPress development? Any comments, software or tips to share? Please do so in the comments section below!</p>

{{< signature "mc, ra, yk, il" >}}


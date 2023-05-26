---
title: 'A Complete Guide To WordPress Multisite'
slug: complete-guide-wordpress-multisite
author: manish-dudharejia
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9479baa1-e1a5-47fa-811d-c92f69aa91e4/complete-guide-wordpress-multisite.png
date: 2020-01-23T13:00:00.000Z
summary: >-
  WordPress Multisite allows you to run multiple websites on your server using the same WordPress installation. From setting up Wordpress Multisite to optimizing its various features, this article will help you understand every facet of this unique WordPress tool. Read on to find out more.
description: >-
  WordPress Multisite allows you to run multiple websites on your server using the same WordPress installation. This article will help you understand every facet of this unique WordPress tool.
categories:
  - WordPress
  - Techniques (WP)
---
<p>WordPress Multisite is a popular feature of WordPress, which enables you to create and run multiple websites using the same WordPress installation on your server. In other words, you can manage several different WordPress websites from a single dashboard.</p>
 
<p>However, people are sometimes unsure of how to use this feature. This guide will help to clear up questions related to what WordPress Multisite is, who needs it, and how to install it.</p>
 
<p>Let's start with the basics.</p>

## 1. What Is WordPress Multisite?

<p>WordPress Multisite is a feature that allows you to create and run multiple WordPress websites from a single WordPress dashboard. It was previously called WordPress Multi-User or WPMU. WordPress Multisite is not a new feature. It is an advanced feature on the WordPress platform that has been around since the launch of WordPress 3.0. You can use it for a variety of purposes, such as updating all of your websites with a single click or charging your subscribers to create a website on your Multisite network.</p>

{{% feature-panel %}}

## 2. Key Features Of WordPress Multisite

<p>WordPress Multisite comes with various unique features. For starters, you can run a network of blogs and websites from a single WordPress installation. It enables you to create a network of subdomains, like <code>https://john.example.com</code>, or directories, like <code>https://www.example.com/john/</code>. Alternatively, you can also have a separate domain for each website on the network. It is also easier to replicate functionality across a network of websites.</p>

<p>In WordPress Multisite, you can control the entire network as a Super Admin. As a regular website admin, you can control only one website on the network. As a Super Admin, you control the accessibility of users who want to create an account and set up WordPress blogs or websites of their own.</p>

<p>A Super Admin can install new themes and plugins, make them available to the websites on the network, and also customize the themes for all websites. Another feature is the ability to create websites and online shops intended for specific languages, regions, and currencies.</p> 

<p>Both the Super Admin and the website admin can control content. While this control extends over the entire network for a Super Admin, the website admin has the right to choose which content from the main domain gets displayed on their respective website. Plugins are also under the control of a Super Admin. However, a website admin can activate and deactivate plugins on their website if required.</p>

## 3. Who Should And Shouldn’t Use WordPress Multisite?

<p>Although WordPress Multisite offers several features, it is not always the right choice. The main concern is that the websites on a Multisite network would share the same database. In other words, you can’t back up only a single website. That’s why all of the websites on a network must belong to the same principal domain.</p>

<p>Let me explain with an example. A university could use WordPress Multisite to build different websites for each department, for student and faculty member blogs, and for forums. Because the websites would share their database with the university's main domain, they would be easier to manage on a Multisite network.</p>

<p>Likewise, banks and financial institutions with a national or global network of branches, digital publications with multiple content sections, government offices with multiple departments, hotel chains, stores with multiple outlets, e-commerce companies, and website design companies such as Wix could also use a Multisite network to their advantage.</p>

<p>However, a web designer couldn’t use Multisite to manage several unrelated client projects. If one of the clients decided to move their website elsewhere, it would be a problem because the website would be sharing its database with others on the network. Multisite makes it difficult to back up an individual website on the network. You would be better off using a single installation in this case.</p>

## 4. Pros And Cons Of WordPress Multisite

<p>Now that we know who should and shouldn’t use WordPress Multisite, let's look at the technical pros and cons. You’ll need to weigh them carefully before making a decision.</p>

### Pros

<ul>
<li>The main advantage is the ability to manage multiple websites from a single dashboard. This is useful if you are running multiple websites managed by different teams under one parent domain, such as an e-commerce store with different country-specific sub-sites.</li>
<li>However, you can also assign a different admin to each website on your network.</li>
<li>With a single download, you can install and activate plugins and themes for all of the websites on your network.</li>
<li>You can also manage updates with a single master installation for all of the websites on your network.</li>
</ul>

### Cons

<ul>
<li>Because all of the websites share the same network resources, they will all go down if the network goes down.</li>
<li>A sudden increase in traffic to one website will affect all others on the network. Unfortunately, beginners often find it difficult to manage traffic and server resources on a Multisite network.</li>
<li>Similarly, if one website gets hacked, the entire network will get compromised.</li>
<li>Not all WordPress plugins support a Multisite network.</li>
<li>Likewise, not all web hosting providers have the tools necessary to support a Multisite network.</li>
<li>If your hosting provider lacks the server requirements, you won't be able to use the Multisite feature. For example, some hosting providers might not allow you to add a domain to the same hosting server. In that case, you might need to change or upgrade your hosting plan or change providers.</li>
</ul>

## 5. Requirements For WordPress Multisite

<p>Knowing the technical pros and cons, you must have decided whether Multisite is the right option for you. If you are going to use it, you will need to meet a few technical requirements first.</p>

<p>One of the first things you will need is a web hosting service provider that can handle multiple domains in a single web hosting plan. Although you could use shared hosting for a couple of websites with low traffic, you should use VPS hosting or a dedicated server, owing to the nature of the WordPress Multisite network.</p>

<p>You will also need to have the fundamental knowledge of how to install WordPress. It would be an added advantage if you already have a WordPress installation. However, you will need to back it up. You will also need to deactivate all of the plugins.</p>

<p>Make sure you have FTP access. You will need to know the basics of editing files using FTP as well. Finally, you will need to activate pretty permalinks. In other words, your URLs should look not like <code>https://example.com/?p=2345</code>, but like <code>https://example.com/my-page</code>.</p>

## 6. Multisite Domain Mapping
 
<p>By default, you can create additional websites on your Multisite network as subdomains or subfolders of the main website. They look like this:</p>
 
<p><code>subsite.network.com</code></p>

<p>or like this:</p>

<p><code>network.com/subsite</code></p>
 
<p>However, you might not always want this, because you will be required to create a unique domain name for each website. That's where domain mapping comes to the rescue. You can use this feature within the Multisite network to map additional websites to show as <code>domain.com</code>. Using domain mapping, this is what you will see:</p>
 
<p><code>subsite.network.com = domain.com</code></p>

<p>or:</p>

<p><code>network.com/subsite = domain.com</code></p>
 
<p>Prior to WordPress 4.5, you had to use a domain mapping plugin to map the additional websites. However, in version 4.5+, domain mapping is a native feature.</p>

## 7. Multisite Hosting And SSL

<p>As you probably know, Secure Sockets Layer (SSL) enables you to transport data over the internet securely. The data remains undecipherable to malicious users, bots, and hackers.</p>

<p>However, some hosting providers offer free SSL certification for the main domain only. You might need to buy it separately for each subdomain. If one of the websites on your multisite network lacks SSL certification, it will compromise the security of all the other websites.  Thus, ensure that all websites on your WordPress Multisite network have SSL certificates.</p>

{{% ad-panel-leaderboard %}}

## 8. Installing And Setting Up WordPress Multisite For New And Existing Websites
 
<p>First, you will need to install WordPress. Once it’s installed, you will need to enable the Multisite feature. You can also enable it on your existing WordPress website. Before doing so, however, back up your website.</p>

<ul>
<li>Use an FTP client or the cPanel file manager to connect with your website, and open the <code>wp-config.php</code> file for editing.</li>
<li>Add the following code to your <code>wp-config.php</code> file just before the <code>/*</code>:</li>

<pre><code class="language-php">/* Multisite */
define( 'WP_ALLOW_MULTISITE', true );</code></pre>
 
<li>Now, save and upload your <code>wp-config.php</code> file back to the server.</li>
<li>That’s all!</li>
</ul>

<p>Next, you will need to set up the Multisite network. If you are already logged into your WordPress dashboard, refresh the page to continue with the next steps. If not, you will need to log in again.</p>
 
<ul>
<li>When setting up the Multisite network on your existing website, you will need to deactivate all plugins. Go to the “Plugins” » “Installed Plugins” page, and select all plugins. Select the “Deactivate” option from the “Bulk Actions” dropdown menu, and click “Apply”.</li>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/225d59b7-6a33-4674-b7d9-d428a2e82b0a/guide-to-wordpress-multisite-deactivate-plugin.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/225d59b7-6a33-4674-b7d9-d428a2e82b0a/guide-to-wordpress-multisite-deactivate-plugin.png" sizes="100vw" caption="Deactivate Plugin. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/225d59b7-6a33-4674-b7d9-d428a2e82b0a/guide-to-wordpress-multisite-deactivate-plugin.png'>Large preview</a>)" alt="How to Deactivate Plugin" >}}

<li>Now, go to “Tools” » “Network Setup”. If you see a notice that you need Apache’s <code>mod_rewrite</code> module installed on your server, don't be alarmed. All leading WordPress hosting providers keep this module enabled.</li>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/983607fa-3b0a-4b9c-89c8-92d1dd90c787/guide-to-wordpress-multisite-network-setup.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/983607fa-3b0a-4b9c-89c8-92d1dd90c787/guide-to-wordpress-multisite-network-setup.png" sizes="100vw" caption="Network Setup. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/983607fa-3b0a-4b9c-89c8-92d1dd90c787/guide-to-wordpress-multisite-network-setup.png'>Large preview</a>)" alt="How to Create a Network of WordPress Sites" >}}

<li>Choose the domain structure for websites on your network, either subdomains or subdirectories.</li>
<li>Add a title for your network.</li>
<li>Make sure that the email address for the network admin is correct.</li>
<li>Click the “Install” button.</li>
<li>You will see some code that you have to add to the <code>wp-config.php</code> and <code>.htaccess</code> files, respectively. Use an FTP client or the file manager in cPanel to copy and paste the code.</li>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bd1505a-8046-49c3-8631-c89c8ba99fd3/guide-to-wordpress-multisite-complete-setup.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bd1505a-8046-49c3-8631-c89c8ba99fd3/guide-to-wordpress-multisite-complete-setup.png" sizes="100vw" caption="Complete Setup. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bd1505a-8046-49c3-8631-c89c8ba99fd3/guide-to-wordpress-multisite-complete-setup.png'>Large preview</a>)" alt="Add code to wp-config.php and .htaccess file" >}}
</ul>

<p>The set-up is complete. You will need to log in again to access your Multisite network.</p>

## 9. WordPress Multisite Configuration And Other Settings

<p>Hold on! You still need to configure the network settings, for which you will need to switch to the Multisite network dashboard.</p>
 
<ul>
<li>Open the “My Sites” menu in the admin toolbar. Click the “Network Admin” option, and then click the “Dashboard” option to go to the Multisite network dashboard.</li>
<li>Click the “Settings” option in the admin sidebar. You will see your website’s title and the admin’s email address. Make sure they are correct before moving on to a few essential configuration settings.</li>
</ul>
</ul>

### A. Registration Settings
 
<p>This setting enables you to open your website to user registration and allows existing users to create new websites on your network. Check the appropriate box.</p>
 
<p>If you check the “Registration Notification” box, you will receive an email notification whenever a new user or website gets registered. Check the “Add New Users” option to enable individual website administrators to add new users to their own websites.</p>
 
<p>Use the “Limited Email Registration” option to restrict registration to a specific domain. For example, allow only users from your company to register with your website. Likewise, you can also prevent some domains from being registered.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13c31a40-5d6d-4fa1-bd4c-6bc90c214a65/guide-to-wordpress-multisite-registration-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13c31a40-5d6d-4fa1-bd4c-6bc90c214a65/guide-to-wordpress-multisite-registration-settings.png" sizes="100vw" caption="Registration Settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13c31a40-5d6d-4fa1-bd4c-6bc90c214a65/guide-to-wordpress-multisite-registration-settings.png'>Large preview</a>)" alt="How to Register New Sites" >}}

### B. New Website’s Settings
 
<p>Here, you can configure the default options, such as welcome emails and the contents of the first default post, page, and comment, for every new website built on your Multisite network. You can update these settings anytime.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d78d8851-e31c-49ab-b3e0-36ee663e10f6/guide-to-wordpress-multisite-new-site-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d78d8851-e31c-49ab-b3e0-36ee663e10f6/guide-to-wordpress-multisite-new-site-settings.png" sizes="100vw" caption="New Site Settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d78d8851-e31c-49ab-b3e0-36ee663e10f6/guide-to-wordpress-multisite-new-site-settings.png'>Large preview</a>)" alt="Make Settings For New site" >}}

### C. Upload Settings

<p>You can limit the total amount of space each website on your network can use for uploads. This will help you to delegate server resources judiciously. The default value is 100 MB. You can also set the type of files that users can add to their websites, such as images, .doc, .docx, and .odt files, audio and video files, and PDFs. You can also set a size limit for individual files.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfd378cc-1277-4110-ba33-3c8ebad447c7/guide-to-wordpress-multisite-upload-settings.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfd378cc-1277-4110-ba33-3c8ebad447c7/guide-to-wordpress-multisite-upload-settings.png" sizes="100vw" caption="Upload Settings. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfd378cc-1277-4110-ba33-3c8ebad447c7/guide-to-wordpress-multisite-upload-settings.png'>Large preview</a>)" alt="Assign space for uploads of each site on your network" >}}

### D. Menu Settings
 
<p>This setting enables the administrative menu for the plugins section of your network’s websites. Once you enable this setting, users will be able to activate and deactivate plugins, but won’t be able to add new ones. Click “Save Changes” to apply the changes you have made.</p>

## 10. Resources: Setting Up Themes And Plugins
 
<p>Because individual website administrators can’t install themes and plugins on their own, you will need them to set up on the network.</p>
 
### A. Themes
 
<p>Go to “My Sites” » “Network Admin” » “Themes”.</p>
 
<p>On this page, you will see a list of the themes currently installed. Use the following settings to make your desired changes.</p>

<ul>
<li><strong>“Network Enable”</strong>: Make the theme available to website administrators.</li>
<li><strong>“Network Disable”</strong>: Disable a theme that you have previously made available.</li>
<li><strong>“Add New”</strong>: Install a new theme on your network.</li>
</ul>

### Change a Default Theme

<p>Add the following code to your <code>wp-config.php</code> file to change the default theme for new websites (replacing <code>your-theme</code> with the name of the theme’s folder):</p>
 

<pre><code class="language-php">// Setting default theme for new sites
define( 'WP_DEFAULT_THEME', 'your-theme' );</code></pre>

### B. Plugins
 
<p>Go to “My Sites” » “Network Admin” » “Plugins”.</p>
 
<p>Click the “Network Activate” option below each plugin to add it to your network. Remember that if you have already enabled the “Plugins Menu” option for website administrators in the “Network Settings”, then admins will not be able to delete or install new plugins. However, they will be able to activate and deactivate existing plugins.</p>
 
## 11. How To Add A New Website To The Multisite Dashboard
 
<p>Go to “My Sites” » “Network Admin” » “Sites”.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3a4fe6a-65f4-47be-8906-946f73384ef8/guide-to-wordpress-multisite-add-sites.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3a4fe6a-65f4-47be-8906-946f73384ef8/guide-to-wordpress-multisite-add-sites.png" sizes="100vw" caption="Add Sites. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3a4fe6a-65f4-47be-8906-946f73384ef8/guide-to-wordpress-multisite-add-sites.png'>Large preview</a>)" alt="How to to enable Administrative Menu for Plugins Section" >}}

<p>Click the “Add New” button.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8792909b-54b4-4905-89e6-b95e813d125b/guide-to-wordpress-multisite-add-new-sites.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8792909b-54b4-4905-89e6-b95e813d125b/guide-to-wordpress-multisite-add-new-sites.png" sizes="100vw" caption="Add New Sites. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8792909b-54b4-4905-89e6-b95e813d125b/guide-to-wordpress-multisite-add-new-sites.png'>Large preview</a>)" alt="How to Add New Site to the Multisite Dashboard" >}}

<p>Fill in the following fields.</p>

<ul>
<li>Add the address (URL) for your new website.</li>
<li>Enter your “Site Title”.</li>
<li>Enter the email address of the new website’s administrator.</li>
</ul>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5fcf52c-6f52-43cd-9833-fd55f7fe5bc9/guide-to-wordpress-multisite-add-site-button.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5fcf52c-6f52-43cd-9833-fd55f7fe5bc9/guide-to-wordpress-multisite-add-site-button.png" sizes="100vw" caption="Add Site Button. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5fcf52c-6f52-43cd-9833-fd55f7fe5bc9/guide-to-wordpress-multisite-add-site-button.png'>Large preview</a>)" alt="Add New Site Button" >}}

<p>Click the “Add Site” button to finish the process.</p>

## 12. Google Analytics On WordPress Multisite
 
<p>You can also generate Google Analytics code for all pages on all of the websites on your Multisite network. If you haven't already done so, create a Google Analytics account, and sign into it.</p>
 
<ul>
<li>Start by creating a property to set up a Google Analytics ID. You will need this ID to install your global site tag (<code>gtag.js</code>).</li>
<li>Next, find your Google Analytics ID in the “Property” column of the relevant account in the “Admin” section of your Analytics account.</li>
<li>Now, you can copy and paste the global site tag on the relevant web pages. Add the <code>gtag.js</code> tag right after the opening <code>&lt;head&gt;</code> tag. You can have different analytics code for each website on the network, and the Super Admin can manage all of them if needed.</li>
</ul>
 
{{% ad-panel-leaderboard %}}

## 13. Setting Up On Local Host

<p>You can use any WAMP or LAMP software to set up WordPress Multisite on a local system. You’ll need to follow the same steps you did to host a website. However, take care with the domain mapping. You can easily set up a subdirectory website in the local system, but to set up a subdomain or a different domain, you’ll need to set up virtual host on the WAMP or LAMP server.</p>

## 14. Useful Plugins For WordPress Multisite And How They Work

<p>You can use a variety of plugins to ensure the smooth operation of your Multisite network.</p>
 
<p><strong>A. <a href="https://wordpress.org/plugins/wordpress-mu-domain-mapping/">Domain Mapping</a></strong><br />
This plugin enables you to offer each website on your network its own domain name.</p>
 
<p><strong>B. <a href="https://wpforms.com/">WPForms</a></strong><br />
Create different forms using a simple drag-and-drop tool.</p>
 
<p><strong>C. <a href="https://yoast.com/wordpress/plugins/seo/">Yoast SEO</a></strong><br />
Optimize the websites on your network for better search engine results. Yoast is a well-known name in the SEO world.</p>
 
<p><strong>D. <a href="https://wpmupremium.com/wordpress/pro-sites-plugin/">Pro Sites</a></strong><br />
Offer paid upgrades, advertising, and more, thereby monetizing your Multisite network. You can restrict the features of the free website, encouraging users to upgrade.</p>

<p><strong>E. <a href="https://www.seedprod.com/">SeedProd</a></strong><br />
Add customized “Coming soon” and “maintenance mode” landing pages. This will jazz up the network while administrators work on their websites.</p>

<p><strong>F. <a href="https://wordpress.org/plugins/wp-mail-smtp/">WP Mail SMTP</a></strong><br />
Fix the “WordPress is not sending email” issue with this plugin. It allows you to use an SMTP server to send crucial Multisite registration and notification emails.</p>
 
<p><strong>G. <a href="https://wordpress.org/plugins/user-switching/">User Switching</a></strong><br />
Using this plugin, you can switch user accounts as network admin to see what your users are experiencing when working on their websites. It can help you to troubleshoot some functionality issues.</p>

## 15. Troubleshooting And FAQs
 
### A. Troubleshooting

<p>When setting up a Multisite network, you might encounter a few common problems. Let's see how to troubleshoot these issues.</p>
 
#### I. Login Issues

<p>You might encounter a <code>wp-admin</code> login issue If you are using WordPress Multisite with subdirectories, rather than subdomains. If you are not able to log into the WordPress back end for individual websites with subdirectories, you can try replacing the <code>define ('SUBDOMAIN_INSTALL', true);</code> line in <code>wp-config.php</code> file with <code>define ('SUBDOMAIN_INSTALL', 'false');</code>.</p>

#### II. Find Unconfirmed Users

<p>Sometimes, you might not be able to find registered users who haven’t received an activation email. Usually, poorly configured mail settings are responsible for this problem. You can use SMTP (Simple Mail Transfer Protocol) to send activation emails. The PHP Mail function might send emails to the junk folder due to unauthorized email sending. Instead, you can use SMTP with proper domain authentication to get emails delivered to the inbox. Use any SMTP service provider, such as MailGun or Gmail.</p>

### B. FAQs
 
#### 1. Can I install plugin “X” in my WordPress Multisite?

Yes, you can install any plugin in Multisite. However, not all plugins support Multisite. Check the plugin’s support before installing it.
 
#### 2. Can I share user logins and roles across a Multisite network?

Yes, you can share user logins and roles across multiple websites. This comes in handy if you want website admins to manage the content on their own websites in your Multisite network.
 
#### 3. Is it possible to display the main website’s posts on all websites on the network?

Yes, you can show your main website’s posts across the network.
 
#### 4. If I am a Super Admin, can I log into all network websites with a single ID?

Yes, Super Admins can use the same credentials to sign into all network websites.

#### 5. As a Super Admin, can I log into another network’s websites?

No, you can't sign into networks other than your own.
 
#### 6. Can I add more websites to my network later?

Yes, you can add as many websites as you want, anytime you want.
 
#### 7. Can I use different plugins for each website, such as Yoast for one and All in One SEO for another?

Yes, you can use different plugins with similar functionality for different websites. However, you must set the plugin for the specific website you want. If you activate it for the entire Multisite network, it will work on all websites automatically.
 
#### 8. Can I install a plugin on an individual website?

No, you cannot install a plugin directly on an individual website. You have to install it on the network. However, you can activate or deactivate it for a specific website.
 
#### 9. Can I create a theme and apply it to a specific website?

Yes, you can create as many themes as you like. You can also activate or deactivate themes as a website’s admin.

## 16. WordPress Multisite Examples

<p>Here are a few well-known brands using a WordPress Multisite network.</p>
 
<ul>
	<li><a href="https://openviewpartners.com/">OpenView Venture Partners</a><br />OpenView Venture Partners is a venture capital firm. The company uses a Multisite installation to run three different websites, including the corporate website, the corporate blog, and a multi-author blog called Labs. The company runs the last two websites under the subdomains blog.openviewpartners.com and labs.openviewpartners.com. Each website has a centralized theme that works perfectly.</li>
	<li><a href="https://blogs.ubc.ca/">The University of British Columbia Blogs</a><br />The University of British Columbia (UBC) also uses WordPress Multisite. The purpose here is to enable professors to create course websites, build blogs with multiple contributors, and create portfolios for students as well as staff members. The WordPress Multisite installation gives teachers complete control over their online communities. They can add as many students as they like and take teaching beyond the walls of the classroom.</li>
	<li><a href="https://www.cheapflights.com/">Cheap Flights</a><br />Cheapflights is a travel website, offering flight tickets, hotel bookings, and vacation packages. The website uses WordPress Multisite to power its Travel Tips section. The section covers the latest travel news, tips on flying, information on the best places to travel to, and more.</li>
</ul>
 
## Wrapping Up
 
<p>As you can see, WordPress Multisite comes with several advantages. You can control and manage several websites from a single dashboard. It can certainly reduce your legwork and make your website monitoring hassle-free. Hopefully, you now have enough knowledge on installing, troubleshooting, and working with applications on a Multisite network to take the plunge.</p>

<p>Have you ever used WordPress Multisite? Will you consider using it for future projects? Let us know in the comments section below.</p>

{{< signature "dm, yk, al, il" >}}

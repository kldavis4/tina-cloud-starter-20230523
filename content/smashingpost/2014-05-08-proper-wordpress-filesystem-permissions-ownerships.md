---
title: WordPress Permissions – How To Set Up Proper Filesystems And Ownerships
slug: proper-wordpress-filesystem-permissions-ownerships
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7757dd71-b3dd-4bff-8f47-dd2f31aa5de5/illu-permission.jpg
date: 2014-05-08T17:47:02.000Z
author: benjamin-intal
description: >-
  When people talk about WordPress security, file permissions and ownership are
  usually the last thing on their minds. **Installing security plugins is a good
  practice** and a must for every WordPress website. However, if your
  file-system permissions aren’t set up correctly, most of your security
  measures could be easily bypassed by intruders.
categories:
  - WordPress
  - Backend
  - Security
  - Techniques (WP)
---
When people talk about WordPress security, file permissions and ownership are usually the last thing on their minds. <strong>Installing security plugins is a good practice</strong> and a must for every WordPress website. However, if your file-system permissions aren’t set up correctly, most of your security measures could be easily bypassed by intruders.

![wordpress permissions](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5172712-40f7-41f2-b669-f2183848e27d/permission-intro.jpg "WordPress Permissions – Proper Filesystems And Ownerships")

Permissions and ownership are quite important in WordPress installations. Setting these up properly on your Web server should be the first thing you do after installing WordPress. Having the wrong set of permissions could cause fatal errors that stop your website dead. Wrong permissions can also compromise your website and make it prone to attacks.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [What To Do When Your Website Goes Down](https://www.smashingmagazine.com/2010/12/what-to-do-when-your-website-goes-down/)
*   [How To Keep Your Coding Workflow Organized](https://www.smashingmagazine.com/2011/01/cleaning-up-the-mess-how-to-keep-your-coding-workflow-organized/)
*   [<span class="headline">How to find out why your website stopped working</span>](https://www.smashingmagazine.com/2013/07/how-to-find-out-why-your-website-stopped-working/)
*   [9 Steps To A Happy Relationship With Your Hosting Provider](https://www.smashingmagazine.com/2009/03/9-steps-to-a-happy-relationship-with-your-hosting-provider/)

{{% feature-panel %}}

Aside from the security concerns, a number of other issues can stem from having the wrong set of permissions and ownership. Have you ever encountered a blank white screen when trying to load your website for the first time? Or have you ever received error messages when trying to upload images in the media uploader? Correcting permissions and ownership of your files and folders will often fix these types of problems.

In this article, we will teach you all about WordPress filesystem permissions and ownership: what they are, why they are important and how to set them up. You will learn a few basic principles that I follow to keep my file system intact. We will also cover the two most common WordPress server configurations. We’ll explain how they differ and, more importantly, how to set the proper permissions and ownership for each.</p>

## Terminal Vs. FTP Client

During the course of this article, we will be using the terminal to change permissions and ownership. Why not use an FTP client instead? The reason is that FTP is a bit limited for our needs. FTP can be used to transfer files and change file and folder permissions, but it cannot be used to change ownership settings.

To perform the commands listed in this article, you will have to be logged into your server using the <code>SSH</code> command. If you are not familiar with the terminal and <code>SSH</code>, you can learn about them in the article “<a href="https://www.smashingmagazine.com/2012/01/23/introduction-to-linux-commands/">Introduction to Linux Commands</a>.”

## Users And Groups

Before anything else, we need to quickly talk about what users and groups are, because these go hand in hand when defining permissions.

To put it simply, a user is an account that has access to the computer, and a group just is an identifier for a certain set of users. This means that every time you transfer files using FTP, you are using a user account on your server. And depending on how your host has set up your account, you (the user) might belong to one or more groups. <strong>Users and groups are like users and roles in WordPress</strong>. Both are conceptually the same, except that the former is used on your server.

Users and groups are important because they help to identify privileges for all of our files and folders. Owners of a file normally would have full privileges on it; other users who belong to the same group would have fewer privileges on it; while everyone else might have no privileges on it. These privileges are what we call permissions.</p>

## What Are File Permissions?

Permissions dictate what users can do with a file. A permission is represented by a set of numbers, such as <code>644</code> or <code>777</code>, referred to as a <strong>permission mode</strong>. If you have used plugins in WordPress before, then you’ve most likely been asked by some of them to change the permissions of a file or directory because the plugin can’t write to it. By changing the file’s permissions, you are allowing the Web server to gain access to that file or folder.

Think of a permission mode as a set of “who can do what” statements, in which each digit corresponds to the “who” part of the statement:

*   **First digit**.  What the user of the account that owns the file can do
*   **Second digit**.  What other user accounts in the owner’s group can do
*   **Third digit**.  What the user accounts of everyone else (including website visitors) can do

Next, the number corresponds to the “what” part of the statement and is a sum of a combination of any these digits:

*   `4` **Read** a file, or read the names of the files in a folder
*   `2` **Write** or modify a file, or modify the contents of a folder
*   `1` **Execute** or run a file, or access the files in a folder

These digits are the privileges that are assigned to the “who” in the permission mode. Note in the list above that privileges mean something different for files and folders.

<strong>Using the correct permission mode is quite important</strong>. To better illustrate this, think again of users and roles in WordPress. On a WordPress website, contributors and administrators have different sets of capabilities. Contributors may create new blog posts, but they may not add plugins. Administrators, on the other hand, may add plugins and also create blog posts. Administrators may even change the look of the website if they want to. A clear line separates what users in different roles can do. This is the same with permission modes, except that instead of dealing with blog posts and theme options, we are dealing with files and folders on the server.</p>

## Changing Permission Modes

FTP clients usually provide an interface where you can conveniently change the permission mode of your files and folders. Here’s a screenshot of the interface in my FTP client:

<img loading="lazy" decoding="async" title="Example of a permission mode interface." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95f56075-06c6-4cb1-867b-015590fa11a2/permission-mode.png" alt="Example of a permission mode interface." width="291" height="107" /><br>
<em>Example of a permission mode interface.</em>

If you have access to your server’s terminal, you can also use the <code>chmod</code> command to change the permission mode of a file or folder:

<pre><code class="language-bash">
sudo chmod 644 &lt;file&gt;
</code></pre>

To change the permission modes of all files or folders, use <code>chmod</code> in tandem with the <code>find</code> command. For example, you can use this to change all files to <code>644</code>:

<pre><code class="language-bash">
sudo find . -type f -exec chmod 644 {} +
</code></pre>

Or use this to change all of your folders to <code>755</code>:

<pre><code class="language-bash">
sudo find . -type d -exec chmod 755 {} +
</code></pre>

Refer to “<a href="https://codex.wordpress.org/Changing_File_Permissions">Changing File Permissions in the WordPress Codex</a>” for a guide to changing permission modes.

## The Difference Between 644 And 777

Let’s look at some permission modes and how they affect our website.

What would a PHP script with a permission mode of <code>644</code> mean? Following the explanation above of how permission modes work, we can decipher what this mode allows users to do with our script:

*   The owner’s privileges are “read” (4) + “write” (2) = `6`
*   The owner’s group privileges are “read” (4) = `4`
*   Everyone else’s privileges are “read” (4) = `4`

In plain language, this means that:

*   if we own the script, we may read and modify it;
*   everyone else may only read it.

As we can see, <code>644</code> is a good permission mode for our PHP script. We can make changes to it, and our Web server can read it.

Now let’s look at folders. What if we owned a folder that had a permission mode of <code>777</code>? This permission mode can be broken down as follows:

*   The owner’s privileges are “read” (4) + “write” (2) + “execute” (1) = `7`
*   The owner’s group privileges are “read” (4) + “write” (2) + “execute” (1) = `7`
*   Everyone else’s privileges are “read” (4) + “write” (2) + “execute” (1) = `7`

This means that

*   anyone may get a list of file names in our folder;
*   anyone may create, modify and delete any file in our folder;
*   anyone may access the files in our folder.

It is obvious that <code>777</code> is a bad permission mode for anything on our WordPress website because any visitor would be able to add files to our directory or even delete scripts. Worse, anyone would be able to put in malicious code and compromise our website.</p>

## WordPress Server Configurations

Now we know about permissions and how to read them. But before proceeding to change all of our permissions, we need to understand how our server is set up. Because permissions deal with user accounts and groups, we need to know how our WordPress website runs.

A lot of different server configurations are out there. Different configurations need different sets of permission modes for WordPress to work correctly and securely. We’ll talk about just the two most common configurations and the proper permissions for them:

*   **Standard server configuration:**
    *   You have a user account.
    *   Your Web server runs as another user account.
*   **Shared server configuration or `suEXEC` configuration:**
    *   You have a user account.
    *   Other people who use the server have user accounts and might share the same group with your user account.
    *   Your Web server runs as the owner of your WordPress files.

The main difference between these two is in how the Web server runs.</p>

## Permissions For A Standard WordPress Server Configuration

Standard WordPress configurations require a bit more work than shared server configurations because the Web server has no relationship to our user account.</p>

### File and Folder Ownership for WordPress

First, we need to adjust the file and folder ownerships of our WordPress files. We’ll have to make sure of the following:

*   that your user account is the owner of all WordPress files and folders,
*   that your user account and the Web server’s user account belong to the same group.

To find out the groups that your user account belongs to, you can use this command in your server’s terminal:

<pre><code class="language-bash">
groups
</code></pre>

Then, to find out the groups that your Web server belongs to, you can temporarily insert this PHP snippet in one of your WordPress scripts:

<pre><code class="language-bash">
echo exec( 'groups' );
</code></pre>

If your user and the Web server don’t belong to the same group, you can use the following command in the terminal to add your user to one of your Web server’s groups:

<pre><code class="language-bash">
sudo usermod -a -G &lt;a-common-group-name&gt; myuser
</code></pre>

Lastly, to ensure that everything in our WordPress folder belongs to our user account and has the shared group that we just added, perform this command in your WordPress folder:

<pre><code class="language-bash">
sudo find . -exec chown myuser:a-common-group-name {} +
</code></pre>

### Permissions for WordPress

All of our files and folders should now have the correct ownership. Now it’s time to adjust the permission modes. To make things simpler, you’ll only need to remember the following:

*   All files should be `664`.
*   All folders should be `775`.
*   `wp-config.php` should be `660`.

Here’s what we’re trying to achieve with this set of permission modes:

*   Our user account may read and modify our files.
*   WordPress (via our Web server) may read and modify our scripts.
*   WordPress may create, modify or delete files and folders.
*   Other people may not see our database credentials in `wp-config.php`.

You might be thinking that allowing WordPress full privileges with our folders is not secure. Don’t worry — we’re doing this because WordPress needs certain features to create and modify files. WordPress allows us to upload and remove themes and plugins and even edit scripts and styles from the administrative back end. Without this type of permission, we would have to manually upload themes and plugins every time using FTP.

You can use your FTP client to change the permission modes, or you can use the following commands in your WordPress directory to quickly adjust the permissions of all of your files and folders:

<pre><code class="language-bash">
sudo find . -type f -exec chmod 664 {} +
sudo find . -type d -exec chmod 775 {} +
sudo chmod 660 wp-config.php
</code></pre>

Note that some Web servers are stricter than others. If yours is strict, then setting your <code>wp-config.php</code> to <code>660</code> might stop your website from working. In this case, just leave it as <code>664</code>.</p>

## Permissions For A Shared Server Configuration Or `SuEXEC` Configuration

Permissions for shared server configurations are easier to implement. We won’t dwell on ownership because the Web server runs as the owner of our files and folders. Because our user account and the Web server share the same permissions (both are owners), we can dive right into modifying the permission modes:

*   All files should be `644`.
*   All folders should be `755`.
*   `wp-config.php` should be `600`.

Similar to the previous set of permission modes, these break down as follows:

*   Our user account may read and modify our files.
*   WordPress (via our Web server and as the account owner) may read and modify our scripts.
*   WordPress may create, modify or delete files or folders.
*   Other people may not see our database credentials in `wp-config.php`.

Again, you can use an FTP client to change the permission modes, or you can use the following commands in your WordPress directory to quickly adjust the permissions of all of your files and folders:

<pre><code class="language-bash">
sudo find . -type f -exec chmod 644 {} +
sudo find . -type d -exec chmod 755 {} +
sudo chmod 600 wp-config.php
</code></pre>

Similar to the standard WordPress server configuration, your server might be stricter than others and might not allow <code>wp-config.php</code> to be <code>600</code>. In this case, you can adjust it to a more lenient <code>640</code>; if that still doesn’t work, then use <code>644</code>.

Always follow these guidelines and your WordPress files should be kept safe from intruders.</p>

## Common Pitfalls

A common mistake people make is to set the <code>uploads</code> folder to <code>777</code>. Some do this because they get an error when trying to upload an image to their website, and <code>777</code> quickly fixes this problem. But <strong>never give unlimited access to everyone</strong>, or else you’ll make the Web server vulnerable to attack. If you follow the guidelines covered in this article, then you should have no problems uploading files to your website.

At times, though, a plugin will request that you set a file to <code>777</code>. On these occasions, you can temporarily set it to <code>777</code>, but make sure to set it back to its original permission mode when you’re done.</p>

## Conclusion

We’ve learned now about the proper permissions and file ownership of a WordPress website. We’ve also learned to avoid a permission mode of <code>777</code> because of how it endangers the Web server.

Hopefully, you can implement these tips to keep your WordPress website safe and secure. If you have any additional tips regarding permissions and security, please share them in the comments below.

Excerpt image credit: <a href="https://www.flickr.com/photos/64060016@N03/5964629989/in/photostream/">Christopher Ross</a>

{{< signature "al, ml" >}}


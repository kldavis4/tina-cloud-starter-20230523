---
title: 'Wordpress Migration: How To Move A Site Without Hassle'
slug: moving-wordpress-website
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/586dcd8f-1ab0-451a-90ec-e55efa828926/wp-11.jpg
date: 2013-04-08T14:48:19.000Z
author: rachel-mccollin-2
description: >-
  Moving WordPress is a task that many people find daunting. The advice on the
  Codex, while comprehensive, gives you a myriad of options and doesn’t describe
  the process simply and in one place.
categories:
  - WordPress
  - Techniques (WP)
---
Moving WordPress is a task that many people find daunting. The advice on the Codex, while comprehensive, gives you a myriad of options and doesn't describe the process simply and in one place.

When I had to move a WordPress installation for the first time, I spent hours searching online for information on the various aspects of the process, and eventually <strong>wrote myself a checklist</strong> — which I still use.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Migrating A Website To WordPress Is Easier Than You Think](https://www.smashingmagazine.com/2013/05/migrate-existing-website-to-wordpress/)
*   [<span class="headline">A Beginner’s Guide To Creating A WordPress Website</span>](https://www.smashingmagazine.com/2016/02/beginners-guide-creating-wordpress-website/)
*   [How To Speed Up Your WordPress Website](https://www.smashingmagazine.com/2014/06/how-to-speed-up-your-wordpress-website/)
*   [Free SSL For Any WordPress Website](https://www.smashingmagazine.com/2016/06/free-ssl-for-any-wordpress-website/)

So to save you the hassle, here's a step-by-step guide to moving a WordPress website. I'll cover three different scenarios, which in my experience are the most common:

{{% feature-panel %}}

*   Moving a website from a subdirectory of a domain to the root directory (for example, if you've been using a subdirectory for development while not affecting an existing website that's in the root);
*   Moving a website from a local installation to a remote installation; and
*   Moving a website between domains or hosts.</p>

## Before You Start

Before you start any of these methods, make a backup of your website:

*   Your theme files;
*   Your uploads;
*   The plugins you've used, so you won't have to spend time downloading them again if things go wrong; and
*   Your database.

You can back up the database using one of a number of tools:

*   [phpMyAdmin](https://www.phpmyadmin.net/home_page/index.php);
*   [Sequel Pro](https://www.sequelpro.com) for OS X;
*   Terminal commands;
*   A MySQL desktop client; or
*   A backup plugin such as [WP-DB-Backup](https://wordpress.org/extend/plugins/wp-db-backup/), which will provide you a copy of your database by email or download.

In this article I'll show you <strong>how to back up your database using phpMyAdmin</strong>, as this is provided by most hosting providers and has a relatively easy-to-use interface.

If I'm going to be editing the database (which needs to be done when uploading a website or moving it between hosts or servers), I start by making a duplicate of the database and adding "old" to its name. This is the backup, and I'll be editing the original database.</p>

## Moving A Website From A Subdirectory To The Root

This is by far the simplest of the three moves I'm going to cover, because you don't actually have to move anything — or nearly anything. This method will work on a standard installation of WordPress, and will work with most frameworks, or if you're using a parent and child theme structure.

<em>Beware! This method will not work for multisite installations, just for </em><i>standard single-site installations.</i>

The great thing about this method is that it only takes from three to ten minutes depending on your setup — no time at all in the scheme of things.</p>

### 1. Remove the Existing Website

If there is an existing website in the root directory, remove it. It may be another WordPress installation or it may be a static website.

If it's a WordPress website, make a backup as detailed above, and then delete all of the WordPress files in the root.

*   If you have access to [Softaculous](https://www.softaculous.com/) or another installation service via your hosting control panel, use that to uninstall WordPress.
*   If not, use phpMyAdmin to drop (delete) the database from the existing website. See the next section for details of how to do this.
*   After dropping the database, remove all WordPress files. This normally means any files or folders beginning with `wp-`.
*   **Beware — don't remove the existing site until you have made a backup!**

### 2. Turn Off Permalinks

Turn off pretty permalinks in the "Permalinks" screen, which you'll find in the "Settings" menu. Do this by selecting the "Default" option and clicking "Save Changes."

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fe6e88a-63ad-453e-a30e-c406437f4519/1-permalinks.png"><img loading="lazy" decoding="async" title="Permalink Settings screen." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6c0ac53-e5a8-4eb1-b01b-0ad0ee67d92f/1-permalinks.jpg" alt="wordpress migration" width="500" height="340" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fe6e88a-63ad-453e-a30e-c406437f4519/1-permalinks.png">Larger version</a>.</em>

### 3. Change Your Website Address

In "Settings" → "General," change the address of your website but not the address of WordPress. For example if you've been working on the website at <code>example.com/development</code>, change the settings as follows:

*   WordPress address (URL): `https://example.com/development`
*   Site Address (URL): `https://example.com`

Save by clicking on the "Save Changes" button and move on to the next steps before trying to access your website.</p>

### 4. Copy and Edit Two Files

Using FTP/SFTP or cPanel file manager, copy (don't move) the following files from your WordPress directory to the root directory:

*   `index.php`
*   `.htaccess`, if you have one. If there isn't an `.htaccess` file (and turning off pretty permalinks means you're less likely to have one), don't worry about creating one.

Edit the <code>index.php</code> file that you've moved. You could do this by:

*   Editing it in situ after the move, by using FTP/SFTP or cPanel file manager;
*   Downloading it from the subdirectory, editing it and then uploading it to the root directory — instead of making a copy.

The edit you need to make is very simple, to one line at the end of the file. <strong>You simply change this:</strong>

<pre><code class="language-php">require ('./wp-blog-header.php)</code></pre>

..to this:

<pre><code class="language-php">require ('./subdirectoryname/wp-blog-header.php)</code></pre>

So if you've been developing in <code>example.com/development</code>, just change the line to:

<pre><code class="language-php">require ('./development/wp-blog-header.php)</code></pre>

Save the new <code>index.php</code> file.</p>

### 5. Turn Permalinks Back On and Test

Back in the WordPress admin, turn pretty permalinks on again, with whatever setting you need for your website.

Visit the root domain of your website in the browser and it will display the website that's stored in the subdirectory, but the URL will show the root URL rather than the subdirectory URL. And that's it!

## Uploading A WordPress Website From A Local To A Remote Installation

This is one of the most common instances of moving WordPress. If you're working on a local website for development and need to upload it either to go live or because you need to show a client or other team members your work, you're going to need to upload your WordPress website. This is more complicated than moving from a subdirectory to the root directory, and involves moving three things:

*   WordPress itself — you'll need to install this in the new location;
*   The database — which you can move using phpMyAdmin;
*   Your theme files, uploads and plugins.</p>

### 1. Turn Off Permalinks

Turn off pretty permalinks in the "Permalinks" screen, which you'll find in the "Settings" menu. Do this by selecting the "Default" option and clicking "Save Changes."

### 2. Backup the Database

Make a copy of the database and give it a new name (for example, by adding "old" to its name).</p>

### 3. Install WordPress In the New Location and Upload Content

Using your preferred method, install WordPress on the server you want to move your website to.

Using FTP or SFTP, copy the files from your local "wp-content" directory to the remote "wp-content" directory, using the same folder structure as in your local install.

Go and have a cup of coffee. These files could take a while to upload.</p>

### 4. Edit the Database

Don't just open the original database file from your local installation and edit it. DB ata stored serialized will break if edited directly in a text editor. You are better off with a serialize-aware tool like <a href="https://github.com/interconnectit/Search-Replace-DB">Search-Replace-DB</a> (<em>thanks, Andrey Savchenko!</em>). Replace the old, local URL for the website with the new, remote URL.

So for example, if your local URL is <code>https://localhost/example</code>, you would change it to <code>https://example.com</code>.

Using the "replace" command will speed this up — there could be thousands of instances. Save your new database.</p>

### 5. Drop the Existing Remote Database

<strong>Note</strong>: This step only applies if you've used a script such as Softaculous or Fantastico to install WordPress, as they automatically create a new database. If you've installed WordPress manually, you can ignore this bit.

In phpMyAdmin, drop (delete) the database that was installed in the remote website when you installed WordPress:

*   Select the database you're working with.
*   Click on the "Structure" tab.
*   Below the list of tables, click "Check All."
*   In the drop-down menu which says "With selected," select "Drop":[![Dropping a database in phpMyAdmin.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a47ed71-014a-4179-850e-8917978f2cd8/2-phpmyadmin-drop-tables.jpg "Dropping a database in phpMyAdmin.")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9616d820-0fea-464f-8269-a0cc5b24a4e3/2-phpmyadmin-drop-tables.jpg) _[Larger version](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9616d820-0fea-464f-8269-a0cc5b24a4e3/2-phpmyadmin-drop-tables.jpg)._
*   You will see a warning message checking that you want to drop all tables. Click "Yes."
*   Finally you will see a message telling you that your query has been implemented:[![Confirmation message after dropping a database.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/775eb1c5-9735-491b-bd08-f5a1533e2b9e/3-phpmyadmin-drop-success.jpg "Confirmation message after dropping a database.")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b40226b5-b29b-4b20-890b-fe59d18d3d48/3-phpmyadmin-drop-success.png) _[Larger version](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b40226b5-b29b-4b20-890b-fe59d18d3d48/3-phpmyadmin-drop-success.png)._

### 6. Upload the New Database

While you are still in phpMyAdmin, upload the database you've edited:

*   Click the "Import" tab.
*   Click the "Choose file" button.
*   Select the database you saved in step 4 and click "Choose" or "OK."
*   Click the "Go" button.
*   After a while (depending on the size of your database), you will see a message telling you the upload has successfully finished:[![Confirmation message after importing a database.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3bdeb50-4008-401b-976c-e035e47809e2/4-phpmyadmin-import-success.jpg "Confirmation message after importing a database.")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3bdeb50-4008-401b-976c-e035e47809e2/4-phpmyadmin-import-success.jpg)

### 7. Clear Your Browser's Cache

This avoids any problems you may have if the browser has cached content from the old version of the remote database.</p>

### 8. Log Into the WordPress Admin For the Remote Website and Update Permalinks

Your log-in details will be the same as for your local website. If you specified different log-in details when installing remotely, these will have been overridden by the imported database.

Visit the "Permalinks" screen and turn pretty permalinks back on.

You're done!

## Moving A WordPress Website Between Hosts

This process is almost exactly the same as that for uploading a website from a local installation. The only difference is that you need to download the files and database from the existing website.

Follow the above process, with changes to step 2:

### 2. Download and Backup the Old Database and Files

In phpMyAdmin for the old website, select the correct database and click on the "Export" tab. Download the database by clicking the "Go" button. The database will download to your machine.

Move the database out of your downloads folder to somewhere useful and make a copy of it. You'll be working with this database in Step 4.

Using FTP or SFTP, download the contents of <code>wp-content</code> from your old website. You will upload this to the new website in step 3.

Now return to the original process.</p>

## Summary

Moving WordPress doesn't need to be complicated. As long as you follow the steps above in the right order, your data will be safe and your website will work in its new location. Important points to remember are:

*   Always back up your website before you start.
*   If moving WordPress within a domain, you don't need to move the whole thing, just make some changes to the settings and move and edit the `index.php` file.
*   When uploading your database to a new location, make sure you upload the version that you've edited with the new URL, not the backup version with the old URL. Otherwise, at the very least, internal links will break and it's possible you'll see the white screen of death when you try to install your website.

If at any stage you go wrong, undo what you've done and start again with your backup. You did make a backup, right?

## Resources

The WordPress Codex includes resources that will help you apply this method whatever your hosting setup:

*   [Moving WordPress](https://codex.wordpress.org/Moving_WordPress)
*   [Giving WordPress Its Own Directory](https://codex.wordpress.org/Giving_WordPress_Its_Own_Directory)
*   [Installing WordPress](https://codex.wordpress.org/Installing_WordPress)

For help with phpMyAdmin, see <a href="https://www.phpmyadmin.net/documentation/">phpMyAdmin’s documentation</a>.

There are also plugins which will help you move WordPress if you don't want to do it all manually. I haven't tested all of these, so I can't vouch for their reliability or ease of use. If you do use one, do so with care.

*   [WordPress Move](https://wordpress.org/extend/plugins/wordpress-move/)
*   [Backup and Move Plugin](https://wordpress.org/extend/plugins/backup-and-move/)
*   [WP-DB-Backup](https://wordpress.org/extend/plugins/wp-db-backup/)

{{< signature "cp" >}}


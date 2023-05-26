---
title: 'How To Streamline WordPress Multisite Migrations With MU-Migration'
author: nicholas-andre
slug: wordpress-multisite-migrations
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96936ae2-0840-457b-92a3-0ac17db3ba6f/nicholas-oliveira-profile-pic.jpg
date: 2018-02-14T13:30:38+01:00
summary: >-
  Introducing the MU-Migration tool, a WP-CLI command that helps developers migrate sites to or between multisite instances. Multisite migrations have various technical complexities, and this tool can help alleviate them.
description: >-
  Introducing the MU-Migration tool, a WP-CLI command that helps developers migrate sites to or between multisite instances. Multisite migrations have various technical complexities, and this tool can help alleviate them.
categories:
  - Wordpress
---
Migrating a standalone WordPress site to a site network (or "multisite") environment is a tedious and tricky endeavor, the opposite is also true. The [WordPress Importer](https://wordpress.org/plugins/wordpress-importer/) works reasonably well for smaller, simpler sites, but leaves room for improvement. It exports content, but not site configuration data such as Widget and Customizer configurations, plugins, and site settings. The Importer also struggles to handle a large amount of content. In this article, you’ll learn how to streamline this type of migration by using [MU-Migration](https://github.com/10up/MU-Migration), a WP-CLI plugin. 

## Understanding Multisite

A WordPress multisite lets you run multiple websites within the same WordPress installation. It is often referred to as "Multisite Network." [WordPress.com](wordpress.com) is probably the biggest example of a multisite network, running thousands of sites within the same WordPress instance. 

A WordPress multisite can be a perfect fit for several use cases, some of them includes:

- Your client might have multiple properties, and it might make sense to consolidate all of its sites into a unique WordPress installation, sharing a single domain, but not limited to it.

- Once you have it set up, it is a simple and straightforward process to spin up new sites and leverage themes and plugin already available in the network

A deep understanding of how multisite works is beyond the scope of this article, but you can check out the following links:

- "[Create A Network](https://codex.wordpress.org/Create_A_Network)," Codex, WordPress.org

- "[WordPress Multisite: Practical Functions And Methods](https://www.smashingmagazine.com/2011/11/wordpress-multisite-practical-functions-methods/)," Kevin Leary, Smashing Magazine

{{% feature-panel %}}

## Understanding The Challenges

The differences between the structure of a single site and a WordPress multisite are quite reasonable. With multisite, each subsite gets its own set of database tables, with the exception of the user's table (`wp_user`) that is shared across all sites. The way this works in WordPress is that each subsite set of tables have the ID of the site added to each table name (`wp_X_posts`, `wp_X_postmeta`, `wp_X_options`). 

This database structure itself already introduces some complexities. For example, how would you migrate a subsite from multisite to a single install? Obviously, you can’t just export and import the database into the single installation &mdash; the table names are different! You would need to either rename the tables in the exported `.sql` file or use an `ALTER TABLE SQL` query to rename the tables after importing them. The same is true for the opposite way: If you’re importing a single site into multisite, table prefixes will have to be updated as well. Sounds like too much work, right?

The user's table in multisite is global, which means that you can’t just import the user's table from your single site since it would completely override the multisite global user's table. If you’re doing the inverse, extracting a subsite from WordPress and importing into a single site, you would be carrying over all users of the network, even those that do not belong to the subsite being migrated. Additionally, If migrating a subsite from one multisite to another, exporting the user's table is completely off the table. 

The best solution is to export the users separately, but it introduces another problem: when the users are imported they’ll get different IDs. To solve this problem, it is necessary to keep track of the new user's ids, create a mapping table and use the mapping table to update all references to users IDs in WordPress! Again, too much work, right?

These are just two examples of the challenges that one can face when dealing with migrations like this. There are a bunch of other minor things that also need to be taken care of, like moving the uploads folder to the proper location, migrating the records in the database that reference the site ID, etc.

## Meet MU-Migration

[MU-Migration](https://github.com/10up/MU-Migration) is a WP-CLI plugin which I created while working on several client migrations and later open-sourced by 10up. It was conceived to streamline the process of moving sites from single WordPress sites to a multisite instance (or vice-versa). It essentially exports everything into a ZIP package which can then be used to import the site in the desired WordPress installation.

It works by exporting the site’s content and optionally theme, plugins and uploads folders into a zip package that can be easily imported into another WordPress installation. When using MU-Migration, you do not need to worry about the underlying technical details of the migration. It will simply take care of all of that for you so you can focus on what is important: delivering a successful migration to your clients.

### Installing WP-CLI And MU-Migration

In order to use MU-Migration, you first need to [install](https://wp-cli.org/#installing) [WP-CLI](https://wp-cli.org/), the official WordPress command line tool. Installing WP-CLI is as simple as running the commands below on your server:

<div class="break-out">

<pre><code class="language-bash">$ curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
$ chmod +x wp-cli.phar
$ sudo mv wp-cli.phar /usr/local/bin/wp
</code></pre></div>

After running these steps, you’ll be able to execute WP-CLI by typing just `wp` from any WordPress installation, as long as you’re inside the WordPress root directory. 

For example, on your WordPress installation folder, try running the following command:

<pre><code class="language-bash">$ wp theme status
</code></pre>

It is a simple command and will list all themes available, highlighting which one is currently active.

Lastly, to install MU-Migration, you can leverage the `package install` command. Use the following command to download and install MU-Migration as a WP-CLI plugin. 

<pre><code class="language-bash">$ wp package install 10up/mu-migration
</code></pre>

### Running A Simple Migration

The usage of MU-Migration is quite simple. For our first scenario, we’re going to move a single WordPress site into a WordPress multisite installation.

**Exporting The Single Site**

We’ll start off by exporting the single site. To do so, we need to use *export all* command:

<div class="break-out">

<pre><code class="language-bash">$ wp mu-migration export all single-site.zip --themes --plugins --uploads
</code></pre></div>

The command above will export the whole site into a ZIP package, the flags `--themes`, `--plugins`, and `--uploads` are optional and will include the current theme, all plugins, and the uploads folder, respectively, in the export. Depending on the size of your site, it can take some time to finish the process, but for most sites, the export process shouldn’t take more than a couple of minutes.

Once it finishes, it will create a file called `single-site.zip` containing all the site’s data, themes, and plugins as well as the uploads directory. The next step is to move it to the server where the WordPress multisite lives. You can use your preferred SFTP client or a more robust solution like <code><a href="https://rsync.samba.org/">rsync</a></code>.

**Importing The Single Site Into Multisite**

With the exported file in your multisite server, all you need to do is use the import command from the WordPress multisite directory; needless to say, both WP-CLI and MU-Migration needs to be installed on the destination server as well.

<div class="break-out">

<pre><code class="language-bash">$ wp mu-migration import all /path/to/single-site.zip --new_url=example.com/single-site
</code></pre></div>

The command above will take the `single-site.zip` file, extract it and import everything into multisite. It will create a new subsite in your network. The `--new_url` parameter is optional; it will instruct MU-Migration to perform a search, and replace in order to replace all occurrences of the site URL of the exported site with the specified one. This parameter is handy when the migration includes a change of URL or if you’re importing locally, or even in a staging environment.

The import process usually takes longer and depends on the size of the site you’re importing, but don’t fear, MU-Migration will keep you updated as the migration runs. When the process finishes, MU-Migration will inform you the final URL of your imported site. **It is strongly recommended to flush all cache layers** that run on your server, specially Memcache or Redis. 

### Re-Running A Migration

When doing migrations, it is fairly common to do a dry-run first with the purpose of testing things out before running the final migration, which usually means taking another export and re-importing in the destination multisite installation. However, note that in our first migration example, MU-Migration created a new subsite within the network in order to import the single site on top of it. Running the exact same command again would lead to the creation of another subsite, which is not exactly what we would expect for.

Fortunately, it is possible to specify a `blog_id`,  which tells MU-Migration to override the subsite with the specified `blog_id`. For example, let’s assume that the previous import command created a subsite with `2` as the ID and you want to re-run the migration. You could do the following:

<div class="break-out">

<pre><code class="language-bash">$ wp mu-migration import all /path/to/single-site.zip --new_url=example.com/single-site --blog_id=2
</code></pre></div>

If you don’t know the `blog_id`, you can get it through Network Admin Settings or by running  `$ wp site list`.

### Extracting A Subsite From A Multisite Installation

MU-Migration also supports extracting subsites from multisite installations and importing it either into another multisite or in a single site.

For these two scenarios, we’d run the export command from a multisite installation and not from a single site; this means that we need a way to specify which subsite we want to export. In order to do that we just need to pass the `--blog_id` parameter to the export command:

<div class="break-out">

<pre><code class="language-bash">$ wp mu-migration export all subsite-3.zip --themes --plugins --uploads --blog_id=3
</code></pre></div>

In this example, we’re exporting a subsite with ID equals to 3; this will create a ZIP file that is ready to be imported into another multisite or in a single site. The command for importing into a single site and multisite is exactly the same, MU-Migration will detect if it is running on multisite or not and will adjust itself to that automatically. On a side note, when importing into another multisite instance, you can also specify the `--blog_id` parameter to override an existing subsite.

<div class="break-out">

<pre><code class="language-bash">$ wp mu-migration import all /path/to/subsite-3.zip [--new_url=<newurl.com>] [--blog_id=<ID>]
</code></pre></div>

## Tips For Running Large Migrations

While the previous examples work very well for small to medium size migrations, migrating large sites to or from multisite can take a reasonable amount time. In this section, I’ll share some lessons learned while doing several enterprise-like migrations.

**Create A Migration Plan**

Data migrations are often necessary, but it’s a neglected part of many projects. Migrations can be cumbersome and complex, but when planned appropriately it can be painless. Creating a migration plan should be the first step of any migration project. 

A typical migration plan includes things like:

- The impact of the migration on any production editorial processes (i.e., content freezes, differential migration requirements).

- How long is the migration expected to run?

- How will backups be restored? How will a failed migration be handled?

- How will the export process affect the site’s performance? Many sites cannot afford a database export during peak times.

As a general rule of thumb, migrations should be as seamless as possible, and ideally, at the day of launch, all the heavy lifting would have been completed already, and only the steps that are strictly necessary should be performed. This means that you should migrate everything you can before the actual launch date as it will give you room for fixing mistakes and QAing. If it’s a new site build and you’re migrating data, you can often benefit from a content freeze window and get your content moved ahead of time. You can also use strategies to progressively move your content if possible. Check out the next section for an example of this technique.

Although neglected many times, a proper migration plan can avoid a wide variety of issues on a migration. Don’t let unexpected circumstances cause your migration to fail, plan ahead! For a more in-depth discussion about planning a migration, I encourage you to check out the migration section of [10up’s best practices.](https://10up.github.io/Engineering-Best-Practices/migrations/)

**Use Rsync To Progressively Copy The Uploads**

The uploads folder of large sites can be extremely big, and compressing it into a ZIP file for later extraction isn’t always the best and fastest solution. There are several other ways of copying the uploads folder to the destination server. A commonly used tool for enterprise-like migration is <code><a href="https://rsync.samba.org/">rsync</a></code>, which can transfer files between servers faster than using a standard SFTP solution, and as a plus, it can pause and restore transfers. It keeps tracks of what have been transferred already, meaning that we can progressively sync our files. For example, you can start syncing the files a couple of days before the actual migration to buy you some time. Then, on the day of migration, all you need to do is sync the files to make sure that everything that has been added since the last sync is transferred over to the destination server.

The only caveat of this approach is that you’ll need to manually move the uploads’ subdirectories to the right place since multisite has a slightly different structure for the uploads folder: each site gets its own subfolder where its name is the ID of the site.

As a final example, let’s see how we could migrate a large single site into a multisite instance. We’ll start off by exporting the single site into a ZIP package and running a dry-run test on the destination server. At that point, the site would not be accessible to anyone since the domain is still pointing to the old server, meaning that you can safely point your host's file to the new server in order to test the migration. You can also enable a plugin like [Restrict Site Access ](https://wordpress.org/plugins/restricted-site-access/) on the destination site to ensure that it is not publicly accessible in any way. 

For our dry-run test, we’d export the site a few days or weeks before the planned migration date to test and get a sense of how long the process will take. Note that the uploads folder is *not* included.

**Do A Dry-Run First**

Always do a dry-run first. Ideally, a dry-run should happen on the actual server or in a staging environment with a similar server stack.

**Consider Using The `--mysql-single-transaction` Flag**

The import command also supports a `--mysql-single-transaction` flag that will wrap the SQL export into a single transaction to commit all changes from the import at once, preventing the write from overwhelming the database server, especially in clustered MySQL environments.

<pre><code class="language-bash">$ cd /path/to/wordpress
$ wp mu-migration export all site.zip --themes --plugins
</code></pre>

With `rsync`, we can easily transfer the generated exported file:

<pre><code class="language-bash">$ rsync -aP site.zip root@172.99.99.99:/var/www/multisite/
</code></pre>

Then we run the import command on the destination server:

<pre><code class="language-bash">$ ssh root@172.99.99.99
$ cd /var/www/multisite
$ wp mu-migration import all site.zip
</code></pre>

Now we need to know what the `blog_id` of the newly created subsite is; we can get that info by running:

<table class="table-overview tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
	<thead>
	<tr>
		<th data-tablesaw-priority="persist">$ wp site list</th>
		<th></th>
		<th></th>
		<th></th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>blog_id</td>
		<td>url</td>
		<td>last_updated</td>
		<td>registered</td>
	</tr>
	<tr>
		<td>1</td>
		<td>https://multisite.com/ </td>
		<td>2017-09-09 20:59:31</td>
		<td>2016-11-23 21:59:34</td>
	</tr>
	<tr>
		<td>2</td>
		<td>https://siglesite.com/</td>
		<td>2017-06-21 18:30:09</td>
		<td>2017-04-25 13:07:46</td>
	</tr>
</tbody>
</table>

From the output of the above command we know that our site has been imported with the ID 2. We’ll need that to properly move the uploads folder using `rsync`. From the single site server, we’d run the following:

<div class="break-out">

<pre><code class="language-bash">$ rsync -azP wp-content/uploads/ root@172.99.99.99:/var/www/multisite/wp-content/uploads/sites/2/
</code></pre></div>

The above command will copy the whole uploads folder to the right place on a multisite install, which is under the sites folder and inside a folder where its name is just the ID of the site (in this case, 2). At this point, we can now edit the host's file to point the single site domain to the multisite server; then we can do some testing to ensure that the migration worked as expected.

For the final migration, everything would be the same, with the exception that we’d be passing `--blog_id=2` to the import command:

<pre><code class="language-bash">$ wp mu-migration import all site.zip --blog_id=2
</code></pre>

And as a benefit, the uploads sync will happen way faster since `rsync` will only transfer the files that have been changed or added since the last sync.

## Conclusion

Migrating to or from multisite is hard and the tool introduced in this article simplifies the whole migration process by reducing the endeavor to a couple of CLI commands. MU-Migration has been actively used in production for more than a year and is a completely open-source project. The plugin is developed on [Github](https://github.com/10up/MU-Migration) and pull requests are welcome!

{{< signature "mc, ra, hjc, il" >}}


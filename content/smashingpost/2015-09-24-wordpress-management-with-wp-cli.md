---
title: WP-CLI – Advanced WordPress Management
slug: wordpress-management-with-wp-cli
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/148c563a-c32c-4f78-8adb-147f8ee84415/typing-opt.jpg'
date: 2015-09-24T21:57:00.000Z
author: konstantinos-kouratoras
description: >-
  The command-line interface has always been popular in the world of developers,
  because it provides tools that **boost productivity and speed up the
  development** process. At first sight, it might seem hard to believe that
  using the command line to perform certain tasks is getting easier than using a
  graphical interface. The purpose of this article is to clear up your doubts
  about that, at least concerning WordPress tasks.

  WordPress provides a graphical user interface for every administrative task,
  and this has helped to make it the most popular content management system on
  the web. But in terms of productivity, **working with the command line**
  enables you to accomplish many such tasks more efficiently and quickly.
categories:
  - WordPress
  - Workflow
  - Techniques (WP)
---
The command-line interface (CLI) has always been popular in the world of developers, because it provides tools that <strong>boost productivity and speed up the development</strong> process. At first sight, it might seem hard to believe that using the command line to perform certain tasks is getting easier than using a graphical interface. The purpose of this article is to clear up your doubts about that, at least concerning WordPress tasks.</p>

<figure><figcaption><img loading="lazy" decoding="async" class="292270 size-full" title="The command-line interface (CLI)" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a6d7b8c-57a0-4f62-a1d3-8b58ee617800/wp-cli.png" alt="wp-cli" width="300" height="300" /></figcaption></figure>

WordPress provides a graphical user interface for every administrative task, and this has helped to make it the most popular content management system on the web. But in terms of productivity, <strong>working with the command line</strong> enables you to accomplish many such tasks more efficiently and quickly.

WP-CLI is a set of command-line tools that provide such functionality for managing WordPress websites.

In this tutorial, I’ll describe the benefits of using and extending WP-CLI, and I’ll present several advanced commands to make your life easier when working with WordPress.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Meet ImageOptim-CLI, A Batch Compression Tool](https://www.smashingmagazine.com/2013/12/imageoptim-cli-batch-compression-tool/)
*   [Powerful Command Line Tools For Developers](https://www.smashingmagazine.com/2012/10/powerful-command-line-tools-developers/)
*   [Proper WordPress Filesystem Permissions And Ownerships](https://www.smashingmagazine.com/2014/05/proper-wordpress-filesystem-permissions-ownerships/)

## Installation

<strong>Note:</strong> The following steps require a UNIX-like environment (OS X, Linux or FreeBSD). If you are a Windows user, you will need a command-line tool such as <a href="https://www.cygwin.com/">Cygwin</a> or a virtual machine.

Installation of WP-CLI is simple. The basic idea is to download a PHP file and put it somewhere in order to be able to run it from anywhere. You can download the WP-CLI script from GitHub repository:

<pre><code class="language-php">curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar</code></pre>

Then, you need to make the file executable:

<pre><code class="language-php">chmod +x wp-cli.phar</code></pre>

The final step is to move the file to a folder, so that you can execute it from anywhere. Renaming the file to something easy to remember and type is also a good idea; this is the reason why <code>wp</code> is the most commonly used name:

<pre><code class="language-php">sudo mv wp-cli.phar /usr/local/bin/wp</code></pre>

Installation is now over, and you should be able to type WP-CLI commands. You can check whether this process was completed successfully with the following command:

<pre><code class="language-php">wp --info</code></pre>

If everything went fine, you should get an output similar to this:

<pre><code class="language-php">PHP binary: /usr/bin/php
PHP version: 5.5.24
php.ini used: /etc/php.ini
WP-CLI root dir:  phar://wp-cli.phar
WP-CLI global config: /Users/kouratoras/.wp-cli/config.yml
WP-CLI project config:
WP-CLI version: 0.19.2</code></pre>

## Common Tasks

This article is focused on more advanced usage of WP-CLI, but we can start with some ordinary tasks that can be performed on the command line.</p>

### Install a WordPress Website

A basic WP-CLI command is <code>core</code>, which offers a set of powerful tools for managing WordPress installations. The first step in setting up a new WordPress website is to download the package. Navigate to the desired directory and type:

<pre><code class="language-php">wp core download</code></pre>

This will download the latest version of WordPress in English (<code>en_US</code>). If you want to download another version or language, use the <code>--version</code> and <code>--locale</code> parameters. For example, to use the Greek localization and 4.2.2 version, you would type:

<pre><code class="language-php">wp core download --version=4.2.2 --locale=el_GR</code></pre>

Once the download is completed, you can create the <code>wp-config.php</code> file using the <code>core config</code> command:

<pre><code class="language-php">wp core config --dbname=databasename --dbuser=databaseuser --dbpass=databasepassword --dbhost=localhost --dbprefix=prfx_</code></pre>

This command will use the arguments and create a <code>wp-config.php</code> file. Finally, to install WordPress, use the <code>core install</code> command:

<pre><code class="language-php">wp core install --url=example.com  --title="WordPress Website Title" --admin_user=admin_user --admin_password=admin_password --admin_email="admin@example.com"</code></pre>

### Update Core

If your WordPress installation needs to be updated, use the <code>wp core update</code> and <code>wp core update-db</code> subcommands to update the core files and the database (if the database needs to be updated).

WordPress updates, especially security fixes, are important. To make them happen more quickly, use the <code>core update</code> command and (if needed) the <code>core update-db</code> command:

<pre><code class="language-php">wp core update
wp core update-db</code></pre>

You can always check the current version of your installation using <code>core version</code>:

<pre><code class="language-php">wp core version</code></pre>

Initially, updating in the command line might not seem more efficient than doing it from the dashboard, but if you’re maintaining multiple WordPress installations, it can save a lot of time and clicks. You can create a script and update them all at once:

<pre><code class="language-php">#!/bin/bash
declare -a sites=('/var/www/wp1' '/var/www/wp2' '/var/www/wp3')
for site in "${sites[@]}";
do
    wp --path=$site core update
done</code></pre>

In any case, <strong>backing up your database</strong> before any update process is recommended:

<pre><code class="language-php">wp db export backup.sql</code></pre>

### Manage Plugins

Similarly, managing plugins is a matter of a single command. For example, <code>plugin status</code> returns information about installed plugins and their status — <code>A</code> means active, <code>I</code> means inactive and <code>UA</code> means update available — outputting like this:

<pre><code class="language-php">5 installed plugins:
 UA smooth-scroll-up        0.8.9
  I wordpress-beta-tester   1.0
  A wordpress-importer      0.6.1
  A wpcli-commands          1.0
</code></pre>

Other plugin-related subcommands are <code>install</code>, <code>activate</code>, <code>deactivate</code>, <code>update</code>, <code>delete</code> and <code>search</code>, which can be used like in the following example:

<pre><code class="language-php">wp plugin install wordpress-importer --activate
wp plugin deactivate wordpress-importer
wp plugin delete wordpress-importer
wp plugin update --all
wp plugin search import</code></pre>

### Manage Themes

Generally, the same commands can be used to handle a website's theme just by replacing <code>plugin</code> with <code>theme</code>, so there is no point going deeper into this. One noteworthy command is <code>scaffold</code>, which creates an empty child theme, making that process much shorter:

<pre><code class="language-php">wp scaffold child-theme my-child-theme --parent_theme=twentyfifteen --theme_name='My Child Theme' --author='Konstantinos Kouratoras' --author_uri=https://www.kouratoras.gr --theme_uri=https://wp.kouratoras.gr --activate</code></pre>

## Manipulate Data

Apart from simple commands like <code>post create</code>, <code>post edit</code> and <code>post delete</code>, WP-CLI provides tools to manage posts. If you need a lot of posts to test your code in a plugin or theme, you can use the <code>post generate</code> command:

<pre><code class="language-php">wp post generate --count=1000</code></pre>

You can also export your current content and migrate it to another WordPress installation. To do so, you need to install the Importer plugin:

<pre><code class="language-php">wp plugin install wordpress-importer --activate</code></pre>

And then you would use the <code>export</code> and <code>import</code> commands to complete the transfer:

<pre><code class="language-php">wp export
wp import test.xml --authors=create</code></pre>

### Manage Post Revisions

By default, WordPress <strong>stores every revision of a post</strong> in the database. This means that eventually you will have a huge amount of information in the posts table of your website.

To handle this issue, you can use the <a href="https://github.com/trepmal/wp-revisions-cli">wp-revisions-cli</a> plugin, which is an extension of WP-CLI that adds functionality for managing post revisions. This can be installed as a common WordPress plugin, and it offers a set of commands such as <code>clean</code>, <code>list</code> and <code>status</code>. For example, using <code>wp wp revisions list</code>, you can get a list of revisions to current posts:

<pre><code class="language-php">+--------------+-------------+-----+
| post_title   | post_parent | ID  |
+--------------+-------------+-----+
| Hello world! | 1           | 894 |
+--------------+-------------+-----+</code></pre>

## Media

Some administrative tasks that are hard to perform relate to images and media in general. WP-CLI provide some tools to save you time here.</p>

### Bulk Import Images

It's not unusual for a client to provide a set of images and ask you to import them into their website. Doing that through the administrator's panel is painful. Instead, using the media tool of WP-CLI, you can complete this task in a single command:

<pre><code class="language-php">wp media import images_folder/*</code></pre>

### Regenerate Media

You need to regenerate thumbnails when you create new image sizes during the development process. Of course, you could use a third-party plugin or custom PHP code to achieve this, but both ways require significantly more time than a WP-CLI command:

<pre><code class="language-php">wp media regenerate</code></pre>

There are infinite possibilites, because you can combine several commands to specify the target images to edit. For example, to regenerate the featured images for posts of a particular category, you can use the following command:

<pre><code class="language-php">wp media regenerate $(wp eval 'foreach( get_posts(array("category" =&gt; 2,"fields" =&gt; "ids")) as $id ) { echo get_post_thumbnail_id($id). " "; }')</code></pre>

## Database Operations

When we talk about advanced WordPress management using the command line, database operations always come in mind. WP-CLI provides tools for these kinds of tasks. You can run simple queries:

<pre><code class="language-php">wp db query "SELECT id FROM wp_users;"</code></pre>

And you can handle database operations such as importing, exporting and optimizing:

<pre><code class="language-php">wp db export
wp db import backup.sql
wp db optimize</code></pre>

The export command can be also <strong>used in a script or a cron job</strong> to handle and schedule database backups.</p>

## Search And Replace

Developing a website on a local or development server and then moving to another server when everything is ready is a common practice. Copying the files and migrating the database are the easy steps. <strong>Replacing the old URLs with the new ones in the database</strong> records is a trickier part of this procedure, because URLs also exist in serialized data, for which a simple search and replace will not work.

WP-CLI helps you perform this task. The <code>search-replace</code> command replaces the old URL with the new one in all database entries, <strong>including those that contain serialized data</strong>.</p>

<pre><code class="language-php">wp search-replace 'dev.example.com' 'www.example.com'</code></pre>

In this case, WP-CLI unpacks JSON data, executes the replace action and packs the data again into the database entry.

If you want to see how many instances of this search action are in your database without performing the replace command, you can run the previous command using the <code>--dry-run</code>:

<pre><code class="language-php">wp search-replace --dry-run 'dev.example.com' 'www.example.com'</code></pre>

The resulting output will be something like the following:

<pre><code class="language-php">+---------------------+-----------------------+--------------+------+
| Table               | Column                | Replacements | Type |
+---------------------+-----------------------+--------------+------+
| wpcli_options       | option_value          | 2            | PHP  |
| wpcli_posts         | post_content          | 1            | SQL  |
| wpcli_posts         | guid                  | 28           | SQL  |
+---------------------+-----------------------+--------------+------+</code></pre>

## Working With WordPress Multisite

A huge advantage of WP-CLI and the command line in general is the ability to automate repetitive tasks using scripts. This also applies to WordPress Multisite networks. Instead of visiting each website's dashboard to perform a task, you can simplify the process using some lines of code. For example, you can use the following script to install WordPress’ Importer plugin:

<pre><code class="language-php">#!/bin/bash
for site in $(wp site list --field=url)
do
	wp plugin install wordpress-importer --url=$site --activate
done</code></pre>

If you want to avoid the additional steps of creating and running a script file, you can execute the previous example using a single command:

<pre><code class="language-php">for site in $(wp site list --field=url); do wp plugin install wordpress-importer --url=$site --activate; done</code></pre>

## Using WP-CLI Remotely With SSH

If you have already installed WP-CLI on your remote server or if your hosting provider supports this, then you can connect via an SSH terminal and use WP-CLI commands. The only things you’ll need are an SSH client and your host credentials to connect to your server.

Linux and Mac OS X users do not need any additional software, because this can be done using the Terminal application. For Windows users, there are third-party tools, <a href="https://www.chiark.greenend.org.uk/~sgtatham/putty/download.html">Putty</a> being the most popular one. Using any of the tools mentioned above, you can connect to your server using this command:

<pre><code class="language-php">ssh username@host</code></pre>

You will be prompted for your password and, if you connect successfully, you will have a command-line interface to use WP-CLI tools for your websites with this host. In case WP-CLI is not available, you can follow the steps described on the <a href="https://wp-cli.org/">official website</a> to install it. At the end of the process, you can verify that it was successfully installed by typing the following command:

<pre><code class="language-php">wp cli version</code></pre>

If everything went fine, you will get the current version.</p>

### Run Commands Seamlessly

Connecting to a server and navigating to the right path in order to execute WP-CLI commands is a bit boring. Instead, you can use <a href="https://github.com/xwp/wp-cli-ssh">WP-CLI SSH</a>, which is a package that allows you to <strong>invoke WP-CLI from your local shell</strong>, without having to log into your remote host.

Before moving to the installation steps of WP-CLI SSH, you need to set up WP-CLI’s package index in the <code>~/.wp-cli</code> folder. (If it does not exists, create this directory.)

<pre><code class="language-php">cd ~/.wp-cli</code></pre>

You’ll have to install Composer, if you have not done so before:

<pre><code class="language-php">curl -sS 'https://getcomposer.org/installer' | php</code></pre>

Create (or use the existing) <code>composer.json</code> file:

<pre><code class="language-php">php composer.phar init --stability dev --no-interaction
php composer.phar config bin-dir bin
php composer.phar config vendor-dir vendor</code></pre>

Add the WP-CLI package index:

<pre><code class="language-php">php composer.phar config repositories.wp-cli composer 'https://wp-cli.org/package-index/'</code></pre>

Create (or use the existing) <code>config.yml</code> file, and put these lines inside it:

<pre><code class="language-php">require:
	- vendor/autoload.php</code></pre>

Everything should now be ready for you to install the WP-CLI SSH package:

<pre><code class="language-php">php composer.phar global require x-team/wp-cli-ssh dev-master</code></pre>

It's time to create the configuration file and set up the hosts. Create a <code>wp-cli.yml</code> file and insert the following settings:

<pre><code class="language-php">ssh:

  production:
    # The %pseudotty% placeholder gets replaced with -t or -T depending on whether you're piping output
    # The %cmd% placeholder is replaced with the originally invoked WP-CLI command
    cmd: ssh %pseudotty% production.example.com %cmd%

    # Passed to WP-CLI on the remote server via --url
    url: production.example.com

    # We cd to this path on the remote server before running WP-CLI
    path: /var/www/production

    # WP-CLI over SSH will stop if one of these is provided
    disabled_commands:
      - db drop
      - db reset</code></pre>

In the previous example, replace <code>production.example.com</code> with your server’s URL and <code>/var/www/production</code> with the path to your WordPress installation. In the <code>disabled commands</code> section, you can set WP-CLI commands that will not be allowed on the remote server. You can create as many hosts as you wish, using different names for each one.

If everything has been set up correctly, you will be able to run commands using the <code>ssh</code> subcommand and providing the host argument:

<pre><code class="language-php">wp ssh plugin status --host=production</code></pre>

In case you’ll be working mainly on the remote server, there is also the option to create an alias in your <code>~/.bash_profile</code> file, so that the <code>wp</code> command will <strong>use this host by default</strong>:

<pre><code class="language-php">alias wp="wp ssh --host=production"</code></pre>

## Unit Tests

Unit tests can be very beneficial to plugin developers. They can reveal bugs very quickly and ensure that a new version of your software will not break anything. However, creating tests is a complicated process because you have to set up PHPUnit, set up WordPress’ testing library and test configuration files. For the last two tasks, WP-CLI can make your life easier and generate the required files automatically.

First things first. You need to install PHPUnit; follow the guide on the <a href="https://github.com/sebastianbergmann/phpunit#installation">official website</a>. After this, WP-CLI will take action and help you to create the files needed to run PHPUnit tests with a single command:

<pre><code class="language-php">wp scaffold plugin-tests my-plugin</code></pre>

If you navigate to your plugin's directory, you will see some new folders and files:

<pre><code class="language-php">.travis.yml
bin/
phpunit.xml
tests/</code></pre>

You can use the <code>install-wp-tests.sh</code> file in the <code>bin</code> folder to initialize the testing environment:

<pre><code class="language-php">bash bin/install-wp-tests.sh test_database user 'pass' localhost latest</code></pre>

The parameters used are:

*   `test_database` the database that will be used to insert test data
*   `user` MySQL database user
*   `pass` MySQL database password
*   `localhost` MySQL host
*   `latest` the WordPress version you are using

The previous command would set up an example unit test that actually does nothing, but it can be used as a starter file to create your own test. The file is <code>tests/test-sample.php</code> and contains the following source code:

<pre><code class="language-php">class SampleTest extends WP_UnitTestCase {

	function test_sample() {
		// replace this with some actual testing code
		$this-&gt;assertTrue( true );
	}
}</code></pre>

Everything is now ready, and you can run your plugin's unit test:

<pre><code class="language-php">phpunit</code></pre>

We won’t go any further into unit tests because they’re beyond the scope of this article, but you can find a ton of resources on <a href="https://phpunit.de/documentation.html">PHPUnit’s official website</a> and around the web.</p>

## Extending WP-CLI

If you have gotten to this point, you might be convinced that WP-CLI is a powerful tool in the hands of a developer. But this is not the end of the story, because you can also <strong>extend built-in functionality using your code</strong>. There are two ways to do that. You can either load and execute PHP code from a file or build your own plugin that creates a custom command.</p>

### Execute PHP File

If you want to test a PHP snippet, there is no need to include it in a WordPress file. WP-CLI provides the <code>eval-file</code> command, which executes common PHP files, having loaded WordPress before. For example, if you want to print the title from a random WordPress post, the source code for this action would be something like this:

<pre><code class="language-php">global $wpdb;
$random_post = $wpdb-&gt;get_var(
	"SELECT post_title
	FROM $wpdb-&gt;posts
	WHERE post_type = 'post'
		AND post_status = 'publish'
	ORDER BY rand()
	LIMIT 1"
);
echo "Random post: $random_post";</code></pre>

Save it in a file named <code>script.php</code> and check the output, typing this command:

<pre><code class="language-php">wp eval-file ./script.php</code></pre>

### Create Custom Commands Using Plugin

Moving one step further, you can create custom WordPress plugins to extend WP-CLI’s built-in functionality and create your own commands. Your plugin file should have a class for each command and public methods for each subcommand.

Let's see it in action. Let’s assume you want to create a command that contains three subcommands:

*   `hello` takes a name as a positional argument and says `hello`
*   `bye` takes a name as an associative argument and says `bye`
*   `random` prints the title of a random WordPress post

We’d create a class, named <code>My_Commands</code>, that contains three public functions: <code>hello</code>, <code>bye</code> and <code>random</code>. These functions take two arguments: <code>$args</code>, which contains the positional arguments, and <code>$assoc_args</code>, which contains the associative arguments.

In our example, the first subcommand would have a <code>name</code> positional argument, which would take as input to print the <code>hello</code>:

<pre><code class="language-php">function hello( $args, $assoc_args ) {
        list( $name ) = $args;
        WP_CLI::success( "Hello, $name!" );
}</code></pre>

The second subcommand would have a <code>name</code> associative argument, which would be extracted from the <code>$assoc_args</code> array:

<pre><code class="language-php">function bye( $args, $assoc_args ) {
        $name = 'name';
        if( $assoc_args[ 'name' ] ) {
                $name = $assoc_args[ 'name' ];
        }
        WP_CLI::success( "Bye, $name!" );
}</code></pre>

The third subcommand would take no arguments. It would just execute a database query, fetch a random post and print the title:

<pre><code class="language-php">function random ( $args, $assoc_args ) {
        global $wpdb;
        $random_post = $wpdb-&gt;get_var(
        	"SELECT post_title
        	FROM $wpdb-&gt;posts
        	WHERE post_type = 'post'
        		AND post_status = 'publish'
    		ORDER BY rand() LIMIT 1"
    	);
        WP_CLI::success( "Random post: $random_post" );
}</code></pre>

Finally, you would have to register your class as a WP-CLI command, using an <code>add_command</code> call. This function takes as arguments the name of the command and the name of the class:

<pre><code class="language-php">WP_CLI::add_command( 'mycommands', 'My_Commands' );</code></pre>

Wrapping the whole code in a WordPress plugin, you would end up with the following file:

<pre><code class="language-php">/*
Plugin Name: WP-CLI Commands
Version: 1.0
description: >-
  Extending WP-CLI with custom commands
Author: Konstantinos Kouratoras
Author URI: https://www.kouratoras.gr
*/

if( defined( 'WP_CLI' ) &amp;&amp; WP_CLI ) {

        class My_Commands {

                function hello( $args, $assoc_args ) {

                        list( $name ) = $args;

                        WP_CLI::success( "Hello, $name!" );
                }

                function bye( $args, $assoc_args ) {

                        $name = 'name';

                        if( $assoc_args[ 'name' ] ) {
                                $name = $assoc_args[ 'name' ];
                        }

                        WP_CLI::success( "Bye, $name!" );
                }

                function random ( $args, $assoc_args ) {

                        global $wpdb;

                        $random_post = $wpdb-&gt;get_var("SELECT post_title FROM $wpdb-&gt;posts WHERE post_type = 'post' AND post_status = 'publish' ORDER BY rand() LIMIT 1");

                        WP_CLI::success( "Random post: $random_post" );
                }
        }

        WP_CLI::add_command( 'mycommands', 'My_Commands' );
}</code></pre>

You can confirm that your command has been registered successfully by typing the following:

<pre><code class="language-php">wp mycommands</code></pre>

This outputs the list of all available commands:

<pre><code class="language-php">usage: wp mycommands bye --name=name
   or: wp mycommands hello name
   or: wp mycommands random</code></pre>

Everything is ready to execute your first WP-CLI custom commands:

<pre><code class="language-php">wp mycommands hello world
wp mycommands bye --name="Joe"
wp mycommands random</code></pre>

Respectively, the output would be:

<pre><code class="language-php">Success: Hello, world!
Success: Bye, Joe!
Success: Random post: This is a title of a post</code></pre>

## Conclusion

You now have a good idea of the possibilities of WP-CLI. These possibilities are becoming endless, if you consider that you can extend core functionality and create your own commands. Of course, many more built-in tools were not mentioned in this article. You can find more about them on the <a href="https://wp-cli.org/">official website</a>.

In case you want to see WP-CLI in action and integrate it in your daily workflow, you will find some resources below to get started.</p>

### Resources From Around the Web

*   [WP-CLI](https://wp-cli.org/) (official website)
*   [WP-CLI](https://github.com/wp-cli/wp-cli), GitHub
*   [WP-CLI wiki](https://github.com/wp-cli/wp-cli/wiki)
*   [WP-CLI](https://codex.wordpress.org/wp-cli), WordPress Codex
*   [WP-CLI](https://wordpress.stackexchange.com/questions/tagged/wp-cli), StackExchange (questions)
*   [WP-CLI Commits](https://groups.google.com/forum/?fromgroups=#!forum/wp-cli-commits), Google Groups (mailing list)

{{< signature "dp, ml, al" >}}


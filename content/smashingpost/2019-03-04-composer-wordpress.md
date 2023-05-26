---
title: 'Using Composer With WordPress'
slug: composer-wordpress
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f333d7c1-4fd6-4616-8b70-3dd59200c839/composer-wordpress-leo-losoviz.png
date: 2019-03-04T14:00:33+01:00
summary: >-
  WordPress is modernizing, allowing us to rethink how to make the most out of newer tools and technologies. In this article, Leonardo Losoviz explains how you can integrate WordPress with Composer, Packagist, and WPackagist in order to produce better code.
description: >-
  WordPress is modernizing, allowing us to rethink how to make the most out of newer tools and technologies. In this article, Leonardo Losoviz explains how you can integrate WordPress with Composer, Packagist, and WPackagist in order to produce better code.
categories:
  - WordPress
  - JavaScript
  - PHP
---
WordPress is getting modernized. The recent inclusion of JavaScript-based Gutenberg as part of the core has added modern capabilities for building sites on the frontend, and the [upcoming bump of PHP’s minimum version](https://make.wordpress.org/core/2018/12/08/updating-the-minimum-php-version/), from the current 5.2.4 to 5.6 in April 2019 and 7.0 in December 2019, will make available a myriad of new features to build powerful sites.

In my previous article on Smashing in which I identified [the PHP features newly available to WordPress](https://www.smashingmagazine.com/2019/02/wordpress-modern-php/), I argued that the time is ripe to make components the basic unit for building functionalities in WordPress. On one side, Gutenberg already makes the block (which is a high-level component) the basic unit to build the webpage on the frontend; on the other side, by bumping up the required minimum version of PHP, the WordPress backend has access to the whole collection of PHP’s Object-Oriented Programming features (such as classes and objects, interfaces, traits and namespaces), which are all part of the toolset to think/code in components.

So, **why components?** What’s so great about them? A "component" is not an implementation (such as a React component), but instead, it's a concept: It represents the act of encapsulating properties inside objects, and grouping objects together into a package which solves a specific problem. Components can be implemented for both the frontend (like those coded through JavaScript libraries such as React or Vue, or CSS component libraries such as Bootstrap) and the backend.

We can use already-created components and customize them for our projects, so we will **boost our productivity by not having to reinvent the wheel each single time**, and because of their focus on solving a specific issue and being naturally decoupled from the application, they can be tested and bug-fixed very easily, thus making the application more maintainable in the long term. 

The concept of components can be employed for different uses, so we need to make sure we are talking about the same use case. In a previous article, I described how to [componentize a website](https://www.smashingmagazine.com/2019/01/introducing-component-based-api/#building-a-site-through-components); the goal was to transform the webpage into a series of components, wrapping each other from a single topmost component all the way down to the most basic components (to render the layout). In that case, the use case for the component is for rendering &mdash; similar to a React component but coded in the backend. In this article, though, the use case for components is importing and managing functionality into the application.

{{% feature-panel %}}

## Introduction To Composer And Packagist

To import and manage own and third-party components into our PHP projects, we can rely on the PHP-dependency manager [Composer](https://getcomposer.org/) which by default retrieves packages from the PHP package repository [Packagist](https://packagist.org/) (where a package is essentially a directory containing PHP code). With their ease of use and exceptional features, Composer + Packagist have become key tools for establishing the foundations of PHP-based applications. 

Composer allows to declare the libraries the project depends on and it will manage (install/update) them. **It works recursively**: libraries depended-upon by dependencies will be imported to the project and managed too. Composer has a mechanism to resolve conflicts: If two different libraries depend on a different version of a same library, Composer will try to find a version that is compatible with both requirements, or raise an error if not possible. 

To use Composer, the project [simply needs a *composer.json* file](https://getcomposer.org/doc/01-basic-usage.md#composer-json-project-setup) in its root folder. This file defines the dependencies of the project (each for a specific version constraint based on [semantic versioning](https://semver.org/)) and may contain other metadata as well. For instance, the following *composer.json* file makes a project require `nesbot/carbon`, a library providing an extension for DateTime, for the latest patch of its version 2.12:

<pre><code class="language-json">{
    "require": {
        "nesbot/carbon": "2.12.*"
    }
}
</code></pre>

We can edit this file manually, or it can be created/updated through commands. For the case above, we simply open a terminal window, head to the project’s root directory, and type:

<pre><code class="language-bash">composer require "nesbot/carbon"
</code></pre>

This command will search for the required library in Packagist (which is found [here](https://packagist.org/packages/nesbot/carbon)) and add its latest version as a dependency on the existing *composer.json* file. (If this file doesn’t yet exist, it will first create it.) Then, we can import the dependencies into the project, which are by default added under the `vendor/` folder, by simply executing:

<pre><code class="language-bash">composer install
</code></pre>

Whenever a dependency is updated, for instance `nesbot/carbon` released version 2.12.1 and the currently installed one is 2.12.0, then Composer will take care of importing the corresponding library by executing:

<pre><code class="language-bash">composer update
</code></pre>

If we are using Git, we only have to specify the `vendor/` folder on the *.gitignore* file to not commit the project dependencies under version control, making it a breeze to keep our project’s code thoroughly decoupled from external libraries.

<p id="wrike">Composer offers plenty of additional features, which are properly described in the <a href="https://getcomposer.org/doc/00-intro.md"> documentation</a>. However, already in its most basic use, Composer gives developers unlimited power for managing the project’s dependencies.</p>

{{% ad-panel-leaderboard %}}

## Introduction To WPackagist

Similar to Packagist, [WPackagist](https://wpackagist.org/) is a PHP package repository. However, it comes with one particularity: It contains all the themes and plugins hosted on the WordPress [plugin](https://wordpress.org/plugins/) and [theme](https://wordpress.org/themes/) directories, making them available to be managed through Composer.

To use WPackagist, our *composer.json* file must include the following information:

<pre><code class="language-json">{
    "repositories":[
        {
            "type":"composer",
            "url":"https://wpackagist.org"
        }
    ]
}
</code></pre>

Then, any theme and plugin can be imported to the project by using `"wpackagist-theme"` and `"wpackagist-plugin"` respectively as the vendor name, and the slug of the theme or plugin under the WordPress directory (such as `"akismet"` in https://wordpress.org/plugins/akismet/) as the package name. Because themes do not have a trunk version, then the theme’s version constraint is recommended to be “&#42;”:

<pre><code class="language-json">{
    "require": {
        "wpackagist-plugin/akismet":"^4.1",
        "wpackagist-plugin/bbpress":">=2.5.12",
        "wpackagist-theme/twentynineteen":"*"
    }
}
</code></pre>

Packages available in WPackagist have been given the [type](https://getcomposer.org/doc/04-schema.md#type) "wordpress-plugin" or "wordpress-theme". As a consequence, after running `composer update`, instead of installing the corresponding themes and plugins under the default folder `vendor/`, these will be installed where WordPress expects them: under folders `wp-content/themes/` and  `wp-content/plugins/` respectively.

## Possibilities And Limitations Of Using WordPress And Composer Together

So far, so good: Composer makes it a breeze to manage a PHP project’s dependencies. However, WordPress’ core hasn’t adopted it as its dependency management tool of choice, primarily because [WordPress is a legacy application that was never designed to be used with Composer](https://core.trac.wordpress.org/ticket/23912#comment:57), and the community can’t agree if WordPress [should be considered the site or a site’s dependency](https://core.trac.wordpress.org/ticket/23912#comment:78), and integrating these approaches requires hacks.

In this concern, WordPress is outperformed by newer frameworks which could incorporate Composer as part of their architecture. For instance, [Laravel](https://laravel.com/) underwent a major rewriting in 2013 to [establish Composer as an application-level package manager](https://en.wikipedia.org/wiki/Laravel#History). As a consequence, WordPress’ core still does not include the *composer.json* file required to manage WordPress as a Composer dependency. 

Knowing that WordPress can’t be natively managed through Composer, let’s explore the ways such [support can be added](https://composer.rarst.net/), and what roadblocks we encounter in each case.

There are [three basic ways in which WordPress and Composer can work together](https://torquemag.io/2014/09/improving-wordpress-development-workflow-composer/):

1. Manage dependencies when developing a theme or a plugin;
2. Manage themes and plugins on a site;
3. Manage the site completely (including its themes, plugins and WordPress’ core).

And there are two basic situations concerning who will have access to the software (a theme or plugin, or the site):

1. The developer can have absolute control of how the software will be updated, e.g. by managing the site for the client, or providing training on how to do it;
2. The developer doesn’t have absolute control of the admin user experience, e.g. by releasing themes or plugins through the WordPress directory, which will be used by an unknown party.

From the combination of these variables, we will have more or less freedom in how deep we can integrate WordPress and Composer together.

From a philosophical aspect concerning the objective and target group of each tool, while Composer empowers developers, WordPress focuses primarily on the needs of the end users first, and only then on the needs of the developers. This situation is not self-contradictory: For instance, a developer can create and launch the website using Composer, and then hand the site over to the end user who (from that moment on) will **use the standard procedures for installing themes and plugins** &mdash; bypassing Composer. However, then the site and its *composer.json* file fall out of sync, and the project can’t be managed reliably through Composer any longer: Manually deleting all plugins from the `wp-content/plugins/` folder and executing `composer update` will not re-download those plugins added by the end user. 

The alternative to keeping the project in sync would be to ask the user to install themes and plugins through Composer. However, this approach goes against [WordPress’ philosophy](https://wordpress.org/about/philosophy/): Asking the end user to execute a command such as `composer install` to install the dependencies from a theme or plugin adds friction, and [WordPress can’t expect every user to be able to execute this task](https://wptavern.com/i-love-composer-i-love-wordpress-but-i-object-to-a-marriage), as simple as it may be. So this approach can’t be the default; instead, it can be used only if we have absolute control of the user experience under `wp-admin/`, such as when building a site for our own client and providing training on how to update the site.

The default approach, which handles the case when the party using the software is unknown, is to release themes and plugins with all of their dependencies bundled in. This implies that the dependencies must also be uploaded to WordPress' [plugin](https://plugins.svn.wordpress.org/) and [theme](https://themes.svn.wordpress.org/) subversion repositories, defeating the purpose of Composer. Following this approach, developers are still able to use Composer for development, however, not for releasing the software.

This approach is not failsafe either: If two different plugins bundle different versions of a same library which are incompatible with each other, and these two plugins are installed on the same site, it could [cause the site to malfunction](https://deliciousbrains.com/wp-offload-s3-1-6-released/#why). A solution to this issue is to modify the dependencies' namespace to some custom namespace, which ensures that different versions of the same library, by having different namespaces, are treated as different libraries. This can be achieved through [a custom script](https://deliciousbrains.com/wp-offload-s3-1-6-released/#how) or through [Mozart](https://github.com/coenjacobs/mozart), a library which composes all dependencies as a package inside a WordPress plugin.

For managing the site completely, Composer must install WordPress under a subdirectory as to be able to install and update WordPress’ core without affecting other libraries, hence the setup must consider WordPress as a site’s dependency and not the site itself. (Composer doesn’t take a stance: This decision is for the practical purpose of being able to use the tool; from a theoretical perspective, we can still consider WordPress to be the site.) Because WordPress can be [installed in a subdirectory](https://codex.wordpress.org/Giving_WordPress_Its_Own_Directory), this doesn’t represent a technical issue. However, WordPress is by default installed on the root folder, and installing it in a subdirectory involves a conscious decision taken by the user. 

To make it easier to completely manage WordPress with Composer, several projects have taken the stance of installing WordPress in a subfolder and providing an opinionated *composer.json* file with a setup that works well: core contributor [John P. Bloch](https://profiles.wordpress.org/johnpbloch/) provides a [mirror of WordPress’ core](https://github.com/johnpbloch/wordpress-core), and [Roots](https://roots.io/) provides a WordPress boilerplate called [Bedrock](https://roots.io/bedrock/). I will describe how to use each of these two projects in the sections below.

{{% ad-panel-leaderboard %}}

## Managing The Whole WordPress Site Through John P. Bloch’s Mirror Of WordPress Core

I have followed Andrey “Rarst” Savchenko’s recipe for [creating the whole site’s Composer package](https://composer.rarst.net/recipe/site-stack/), which makes use of John P. Bloch’s mirror of WordPress’ core. Following, I will reproduce his method, adding some extra information and mentioning the gotchas I found along the way.

First, create a *composer.json* file with the following content in the root folder of your project:

<pre><code class="language-json">{
    "type": "project",
    "config": {
        "vendor-dir": "content/vendor"
    },
    "extra": {
        "wordpress-install-dir": "wp"
    },
    "require": {
        "johnpbloch/wordpress": ">=5.1"
    }
}
</code></pre>

Through this configuration, Composer will install WordPress 5.1 under folder `"wp"`, and dependencies will be installed under folder `"content/vendor"`. Then head to the project’s root folder in terminal and execute the following command for Composer to do its magic and install all dependencies, including WordPress:

<pre><code class="language-bash">composer install --prefer-dist
</code></pre>

Let’s next add a couple of plugins and the theme, for which we must also add WPackagist as a repository, and let’s configure these to be installed under `"content/plugins"` and `"content/themes"` respectively. Because these are not the default locations expected by WordPress, we will later on need to tell WordPress where to find them through constant `WP_CONTENT_DIR`.

**Note**: *WordPress’ core includes by default a few themes and plugins under folders* `"wp/wp-content/themes"` *and* `"wp/wp-content/plugins"`*, however, these will not be accessed.*

Add the following content to `composer.json`, in addition to the previous one:

<pre><code class="language-json">{
    "repositories": [
        {
            "type": "composer",
            "url" : "https://wpackagist.org"
        }
    ],
    "require": {
        "wpackagist-plugin/wp-super-cache": "1.6.*",
        "wpackagist-plugin/bbpress": "2.5.*",
        "wpackagist-theme/twentynineteen": "*"
    },
    "extra": {
        "installer-paths": {
            "content/plugins/{$name}/": ["type:wordpress-plugin"],
            "content/themes/{$name}/": ["type:wordpress-theme"]
        }
    }
}
</code></pre>

And then execute in terminal: 

<pre><code class="language-bash">composer update --prefer-dist
</code></pre>

*Hallelujah!* The theme and plugins have been installed! Since all dependencies are distributed across folders `wp`, `content/vendors`, `content/plugins` and `content/themes`, we can easily ignore these when committing our project under version control through Git. For this, create a *.gitignore* file with this content:

<pre><code class="language-git">wp/
content/vendor/
content/themes/
content/plugins/
</code></pre>

**Note**: *We could also directly ignore folder* `content/`*, which will already ignore all media files under* `content/uploads/` *and files generated by plugins, which most likely must not go under version control.*

There are a few things left to do before we can access the site. First, duplicate the *wp/wp-config-sample.php* file into *wp-config.php* (and add a line with *wp-config.php* to the *.gitignore* file to avoid committing it, since this file contains environment information), and edit it with the usual information required by WordPress (database information and secret keys and salts). Then, add the following lines at the top of *wp-config.php*, which will load Composer’s autoloader and will set constant `WP_CONTENT_DIR` to folder `content/`:

<pre><code class="language-php">// Load Composer’s autoloader
require_once (__DIR__.'/content/vendor/autoload.php');

// Move the location of the content dir
define('WP_CONTENT_DIR', dirname(__FILE__).'/content');
</code></pre>

By default, WordPress sets constant `WP_CONSTANT_URL` with value `get_option('siteurl').'/wp-content'`. Because we have changed the content directory from the default `"wp-content"` to `"content"`, we must also set the new value for `WP_CONSTANT_URL`. To do this, we can’t reference function `get_option` since it hasn’t been defined yet, so we must either hardcode the domain or, possibly better, we can retrieve it from `$_SERVER` like this:

<div class="break-out">

 <pre><code class="language-php">$s = empty($_SERVER["HTTPS"]) ? '' : ($_SERVER["HTTPS"] == "on") ? "s" : "";
$sp = strtolower($_SERVER["SERVER_PROTOCOL"]);
$protocol = substr($sp, 0, strpos($sp, "/")) . $s;
$port = ($_SERVER["SERVER_PORT"] == "80") ? "" : (":".$_SERVER["SERVER_PORT"]);
define('WP_CONTENT_URL', $protocol."://".$_SERVER[’SERVER_NAME'].$port.'/content');
</code></pre>
</div>

We can now access the site on the browser under `domain.com/wp/`, and proceed to install WordPress. Once the installation is complete, we log into the Dashboard and activate the theme and plugins. 

Finally, because WordPress was installed under subdirectory `wp`, the URL will contain path “`/wp`” when accessing the site. Let’s remove that (not for the admin side though, which by being accessed under `/wp/wp-admin/` adds an extra level of security to the site).

The documentation proposes two methods to do this: [with](https://codex.wordpress.org/Giving_WordPress_Its_Own_Directory#Method_II_.28With_URL_change.29) or [without](https://codex.wordpress.org/Giving_WordPress_Its_Own_Directory#Method_I_.28Without_URL_change.29) URL change. I followed both of them, and found the without URL change a bit unsatisfying because it requires specifying the domain in the *.htaccess* file, thus mixing application code and configuration information together. Hence, I’ll describe the method with URL change.

First, head to “General Settings” which you’ll find under `domain.com/wp/wp-admin/options-general.php` and remove the “`/wp`” bit from the "Site Address (URL)" value and save. After doing so, the site will be momentarily broken: browsing the homepage will list the contents of the directory, and browsing a blog post will return a 404. However, don’t panic, this will be fixed in the next step.

Next, we copy the *index.php* file to the root folder, and edit this new file, adding “`wp/`” to the path of the required file, like this:

<pre><code class="language-php">/** Loads the WordPress Environment and Template */
require( dirname( __FILE__ ) . '/wp/wp-blog-header.php' );
</code></pre>

We are done! We can now access our site in the browser under `domain.com`:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8863b544-53f2-4ba4-b589-655c9d1d62c0/wpcomposer-johnpblock-site.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8863b544-53f2-4ba4-b589-655c9d1d62c0/wpcomposer-johnpblock-site.jpg" sizes="100vw" caption="WordPress site successfully installed through Composer (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8863b544-53f2-4ba4-b589-655c9d1d62c0/wpcomposer-johnpblock-site.jpg'>Large preview</a>)" alt="WordPress site" >}}

Even though it has downloaded the whole WordPress core codebase and several libraries, **our project itself involves only six files** from which only five need to be committed to Git:

1. *.gitignore*
2. *composer.json*
3. *composer.lock*  
This file is generated automatically by Composer, containing the versions of all installed dependencies.
4. *index.php*  
This file is created manually.
5. *.htaccess*  
This file is automatically created by WordPress, so we could avoid committing it, however, we may soon customize it for the application, in which case it requires committing.

The remaining sixth file is *wp-config.php* which **must not be committed** since it contains environment information.

Not bad!

The process went pretty smoothly, however, it could be improved if the following issues are dealt better:

1. **Some application code is not committed under version control.**  
Since it contains environment information, the *wp-config.php* file must not be committed to Git, instead requiring to maintain a different version of this file for each environment. However, we also added a line of code to load Composer’s autoloader in this file, which will need to be replicated for all versions of this file across all environments.
2. **The installation process is not fully automated.**  
After installing the dependencies through Composer, we must still install WordPress through its standard procedure, log-in to the Dashboard and change the site URL to not contain “`wp/`”. Hence, the installation process is slightly fragmented, involving both a script and a human operator.

Let’s see next how Bedrock fares for the same task.

## Managing The Whole WordPress Site Through Bedrock

[Bedrock](https://roots.io/bedrock/) is a WordPress boilerplate with an improved folder structure, which looks like this:

<pre><code class="language-php">├── composer.json
├── config
│   ├── application.php
│   └── environments
│       ├── development.php
│       ├── staging.php
│       └── production.php
├── vendor
└── web
    ├── app
    │   ├── mu-plugins
    │   ├── plugins
    │   ├── themes
    │   └── uploads
    ├── wp-config.php
    ├── index.php
    └── wp
</code></pre>

The people behind Roots chose this folder structure in order to make WordPress embrace the [Twelve Factor App](https://12factor.net/), and they elaborate how this is accomplished through [a series of blog posts](https://roots.io/twelve-factor-wordpress/). This folder structure can be considered an improvement over the standard WordPress one on the following accounts:

- It adds support for Composer by moving WordPress’ core out of the root folder and into folder `web/wp`;
- It enhances security, because the configuration files containing the database information are not stored within folder `web`, which is set as the web server’s document root (the security threat is that, if the web server goes down, there would be [no protection to block access to the configuration files](https://wordpress.stackexchange.com/questions/58391/is-moving-wp-config-outside-the-web-root-really-beneficial#74972));
- The folder `wp-content` has been renamed as “`app`”, which is a more standard name since it is used by other frameworks such as Symfony and Rails, and to better reflect the contents of this folder.

Bedrock also introduces different config files for different environments (development, staging, production), and it cleanly decouples the configuration information from code through library [PHP dotenv](https://github.com/vlucas/phpdotenv), which loads environment variables from a *.env* file which looks like this:

<div class="break-out">

 <pre><code class="language-json">DB_NAME=database_name
DB_USER=database_user
DB_PASSWORD=database_password

# Optionally, you can use a data source name (DSN)
# When using a DSN, you can remove the DB_NAME, DB_USER, DB_PASSWORD, and DB_HOST variables
# DATABASE_URL=mysql://database_user:database_password@database_host:database_port/database_name

# Optional variables
# DB_HOST=localhost
# DB_PREFIX=wp_

WP_ENV=development
WP_HOME=https://example.com
WP_SITEURL=${WP_HOME}/wp

# Generate your keys here: https://roots.io/salts.html
AUTH_KEY='generateme'
SECURE_AUTH_KEY='generateme'
LOGGED_IN_KEY='generateme'
NONCE_KEY='generateme'
AUTH_SALT='generateme'
SECURE_AUTH_SALT='generateme'
LOGGED_IN_SALT='generateme'
NONCE_SALT='generateme'
</code></pre>
</div>

Let’s proceed to install Bedrock, following [their instructions](https://roots.io/bedrock/docs/installing-bedrock/). First create a project like this:

<pre><code class="language-bash">composer create-project "roots/bedrock"
</code></pre>

This command will bootstrap the Bedrock project into a new folder "bedrock", setting up the folder structure, installing all the initial dependencies, and creating an *.env* file in the root folder which must contain the site’s configuration. We must then edit the *.env* file to add the database configuration and secret keys and salts, as would normally be required in *wp-config.php* file, and also to indicate which is the environment (development, staging, production) and the site’s domain.

Next, we can already add themes and plugins. Bedrock comes with themes twentyten to twentynineteen shipped by default under folder `web/wp/wp-content/themes`, but when adding more themes through Composer these are installed under `web/app/themes`. This is not a problem, because WordPress can register more than one directory to store themes through function [`register_theme_directory`](https://codex.wordpress.org/Function_Reference/register_theme_directory).

Bedrock includes the WPackagist information in the *composer.json* file, so we can already install themes and plugins from this repository. To do so, simply step on the root folder of the project and execute the `composer require` command for each theme and plugin to install (this command already installs the dependency, so there is no need to execute `composer update`):

<pre><code class="language-bash">cd bedroot
composer require "wpackagist-theme/zakra"
composer require "wpackagist-plugin/akismet":"^4.1"
composer require "wpackagist-plugin/bbpress":">=2.5.12"
</code></pre>

The last step is to configure the web server, setting the document root to the full path for the `web` folder. After this is done, heading to `domain.com` in the browser we are happily greeted by WordPress installation screen. Once the installation is complete, we can access the WordPress admin under `domain.com/wp/wp-admin` and activate the installed theme and plugins, and the site is accessible under `domain.com`. Success!

Installing Bedrock was pretty smooth. In addition, Bedrock does a better job at not mixing the application code with environment information in the same file, so the issue concerning application code not being committed under version control that we got with the previous method doesn’t happen here.

## Conclusion

With the launch of Gutenberg and the upcoming bumping up of PHP’s minimum required version, WordPress has entered an era of modernization which provides a wonderful opportunity to rethink how we build WordPress sites to make the most out of newer tools and technologies. Composer, Packagist, and WPackagist are such tools which can help us produce better WordPress code, with an emphasis on reusable components to produce modular applications which are easy to test and bugfix.

First released in 2012, Composer is not precisely what we would call "new" software, however, it has not been incorporated to WordPress’ core due to a few incompatibilities between WordPress' architecture and Composer’s requirements. This issue has been an ongoing source of frustration for many members of the WordPress development community, who assert that the integration of Composer into WordPress will enhance creating and releasing software for WordPress. Fortunately, we don’t need to wait until this issue is resolved since several actors took the matter into their own hands to provide a solution. 

In this article, we reviewed two projects which provide an integration between WordPress and Composer: manually setting our *composer.json* file depending on John P. Bloch’s mirror of WordPress’ core, and Bedrock by Roots. We saw how these two alternatives, which offer a different amount of freedom to shape the project’s folder structure, and which are more or less smooth during the installation process, can succeed at fulfilling our requirement of completely managing a WordPress site, including the installation of the core, themes, and plugins.

If you have any experience using WordPress and Composer together, either through any of the described two projects or any other one, I would love to see your opinion in the comments below.

*I would like to thank Andrey “Rarst” Savchenko, who reviewed this article and provided invaluable feedback.*

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
    <li><a title="Read 'Improving WordPress Code With Modern PHP'" href="https://www.smashingmagazine.com/2019/02/wordpress-modern-php/" rel="bookmark">Improving WordPress Code With Modern PHP</a></li>
    <li><a title="Read 'Caching Smartly In The Age Of Gutenberg'" href="https://www.smashingmagazine.com/2018/12/caching-smartly-gutenberg/" rel="bookmark">Caching Smartly In The Age Of Gutenberg</a></li>
    <li><a title="Read 'Implications Of Thinking In Blocks Instead Of Blobs'" href="https://www.smashingmagazine.com/2018/11/implications-blocks-blobs/" rel="bookmark">Implications Of Thinking In Blocks Instead Of Blobs</a></li>
    <li><a title="Read 'What Can Be Learned From The Gutenberg Accessibility Situation?'" href="https://www.smashingmagazine.com/2018/12/gutenberg-accessibility-situation/" rel="bookmark">What Can Be Learned From The Gutenberg Accessibility Situation?</a></li>
</ul>

{{< signature "rb, ra, il" >}}

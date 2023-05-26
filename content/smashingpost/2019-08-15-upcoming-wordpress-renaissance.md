---
title: 'The (Upcoming) WordPress Renaissance'
slug: upcoming-wordpress-renaissance
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c4ff8e-18a1-4f9e-ba78-27734b820766/upcoming-wordpress-renaissance-sharing-card.png
date: 2019-08-15T13:00:59+02:00
summary: >-
  Since its release 8 months ago, Gutenberg has been greatly improved, offering a user experience much richer than anything that was possible in WordPress. Let's take a look at its latest developments, and where it is heading to.
description: >-
  Since its release 8 months ago, Gutenberg has been greatly improved, offering a user experience much richer than anything that was possible in WordPress. Let's take a look at its latest developments, and where it is heading to.
categories:
  - WordPress
  - Plugins
  - Tools
---
It has been 8 months since [Gutenberg](https://wordpress.org/gutenberg/) was launched as the default content editor in WordPress. Depending who you ask, you may hear that Gutenberg is the worst or the best thing that has happened to WordPress (or anything in between). But something that most people seem to agree with, is that Gutenberg has been steadily improving. At the current pace of development, it's only a matter of time until its most outstanding issues have been dealt with and the user experience becomes truly pleasant. 

Gutenberg is an ongoing work in progress. While using it, I experience maddening nuisances, such as floating options that I can't click on because the block placed below gets selected instead,  unintuitive grouping of blocks, columns with so much gap that make them useless, and the "+" element calling for my attention all over the page. However, the problems I encounter are still relatively manageable (which is an improvement from the previous versions) and, moreover, Gutenberg has started making its potential benefits become a reality: Many of its most pressing bugs have been ironed out, its accessibility issues are being solved, and new and exciting features are continuously being made available. What we have so far is pretty decent, and it will only get better and better.

Let's review the new developments which have taken place since Gutenberg's launch, and where it is heading to. 

**Note:** *For more information about this topic, I recommend watching [WordPress founder Matt Mullenweg's talk](https://wordpress.tv/2019/07/04/matt-mullenweg-matt-on-wordpress/) during the recent [WordCamp Europe 2019](https://2019.europe.wordcamp.org/).*

{{% feature-panel %}}

## Why Gutenberg Was Needed

Gutenberg arrived just in time to kick-start the rejuvenation of WordPress, to attempt to make WordPress appealing to developers once again (and reverse its current status of being [the most dreaded platform](https://insights.stackoverflow.com/survey/2019#technology-_-most-loved-dreaded-and-wanted-platforms)). WordPress had stopped looking attractive because of its focus on not breaking backwards compatibility, which prevented WordPress from incorporating modern code, making it look pale in comparison with newer, shinier frameworks.

Many people argue that WordPress was in no peril of dying (after all, it powers more than 1/3rd of the web), so that Gutenberg was not really needed, and they may be right. However, even if WordPress was in no immediate danger, by being disconnected from modern development trends it was headed towards obsolescence, possibly not in the short-term but certainly in the mid to long-term. Let's review how Gutenberg improves the experience for different WordPress stakeholders: developers, website admins, and website users. 

**Developers** have recently embraced building websites through JavaScript libraries Vue and React because (among other reasons) of the power and convenience of components, which translates into a satisfying developer-experience. By jumping into the bandwagon and adopting this technique, Gutenberg enables WordPress to attract developers once again, allowing them to code in a manner they find gratifying.

**Website admins** can manage their content more easily, improve their productivity, and achieve things that couldn't be done before. For instance, placing a Youtube video through a block is easier than through the TinyMCE Textarea, blocks can serve optimal images (compressed, resized according to the device, converted to a different format, and so on) removing the need to do it manually, and the WYSIWYG (**W**hat **Yo**u **S**ee **I**s **W**hat **Y**ou **G**et) capabilities are decent enough to provide a real-time preview of how the content will look like in the website.

By giving them access to powerful functionality, **website users** will have a higher satisfaction when browsing our sites, as experienced when using highly-dynamic, user-friendly web applications such as Facebook or Twitter.

In addition, Gutenberg is slowly but surely modernizing the whole process of creating the website. While currently it can be used only as the content editor, some time in the future it will become a full-fledged site builder, allowing to place components (called blocks) anywhere on a page, including the header, footer, sidebar, etc. (Automattic, the company behind [WordPress.com](https://wordpress.com), has already started work on a [plugin adding full site editing capabilities](https://wordpress.org/plugins/full-site-editing/) for its commercial site, from which it could be adapted for the open-source WordPress software.) Through the site-building feature, non-techy users will be able to add very powerful functionality to their sites very easily, so WordPress will keep welcoming the greater community of people working on the web (and not just developers).

{{% ad-panel-leaderboard %}}

## Fast Pace Of Development

One of the reasons why Gutenberg has seen such a fast pace of development is because it is [hosted on GitHub](https://github.com/WordPress/gutenberg), which simplifies the management of code, issues and communication as compared to Trac (which [handles WordPress core](https://core.trac.wordpress.org/)), and which makes it easy for first-time contributors to become involved since they may already have experience working with Git.

Being decoupled from WordPress core, Gutenberg can benefit from rapid iteration. Even though a new version of WordPress is released every 3 months or so, Gutenberg is also available as a [standalone plugin](https://wordpress.org/plugins/gutenberg), which sees a new release every two weeks (while the latest release of WordPress contains Gutenberg version 5.5, the latest plugin version is 6.2). Having access to powerful new functionality for our sites every two weeks is very impressive indeed, and it enables to unlock further functionality from the broader ecosystem (for instance, the [AMP plugin](https://wordpress.org/plugins/amp/) requires Gutenberg 5.8+ for several features).

## Headless WordPress To Power Multiple Stacks

One of the side effects of Gutenberg is that WordPress has increasingly become "headless", further decoupling the rendering of the application from the management of the content. This is because Gutenberg is a front-end client that interacts with the WordPress back-end through APIs (the WP REST API), and the development of Gutenberg has demanded a consistent expansion of the available APIs. These APIs are not restricted to Gutenberg; they can be used together with any client-side framework, to render the site using any stack. 

An example of a stack we can leverage for our WordPress application is the [JAMstack](https://jamstack.org/), which champions an architecture based on static sites augmented through 3rd party services (APIs) to become dynamic (indeed, Smashing Magazine is a JAMstack site!). This way, we can host our content in WordPress (leveraging it as a Content Management System, which is what it is truly good at), build an application that accesses the content through APIs, generate a static site, and deploy it on a Content Delivery Network, providing for lower costs and greater access speed. 

## New Functionality

Let's play with Gutenberg (the plugin, not the one included in WordPress core, which is available [here](https://wordpress.org/plugins/gutenberg/)) and see what functionality has been added in the last few months. 

### Block Manager

Through the block manager, we can decide what blocks will be available on the content editor; all others will be disabled. Removing access to unwanted blocks can be useful in several situations, such as:

- Many plugins are bundles of blocks; when installing such a plugin, all their blocks will be added to the content editor, even if we need only one
- As many as 40 embed providers are implemented in WordPress core, yet we may need just a few of them for the application, such as Vimeo and Youtube
- Having a large amount of blocks available can overwhelm us, impairing our workflow by adding extra layers that the user needs to navigate, leading to suboptimal use of the time; hence, temporarily disabling unneeded blocks can help us be more effective
- Similarly, having only the blocks we need avoids potential errors caused by using the wrong blocks; in particular, establishing which blocks are needed can be done in a top-down manner, with the website admin analyzing all available blocks and deciding which ones to use, and imposing the decision on the content managers, who are then relieved from this task and can concentrate on their own duties.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c32a1e5-e4dd-4cbb-ba78-e5109ac4d945/upcoming-wordpress-renaissance-block-manager.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c32a1e5-e4dd-4cbb-ba78-e5109ac4d945/upcoming-wordpress-renaissance-block-manager.png" sizes="100vw" caption="Enabling/disabling blocks through the manager (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c32a1e5-e4dd-4cbb-ba78-e5109ac4d945/upcoming-wordpress-renaissance-block-manager.png'>Large preview</a>)" alt="Block manager" >}}

### Cover Block With Nesting Elements

The cover block (which allows us to add a title over a background image, generally useful for creating hero headers) now defines its inner elements (i.e. the heading and buttons, which can be added for creating a call to action) as nested elements, allowing us to modify its properties in a uniform way across blocks (for instance, we can make the heading bold and add a link to it, place one or more buttons and change their background color, and others).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a444826a-a8e0-4f77-a28f-f7df1dfc3286/upcoming-wordpress-renaissance-cover-block.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a444826a-a8e0-4f77-a28f-f7df1dfc3286/upcoming-wordpress-renaissance-cover-block.jpg" sizes="100vw" caption="The cover block accepts nested elements (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a444826a-a8e0-4f77-a28f-f7df1dfc3286/upcoming-wordpress-renaissance-cover-block.jpg'>Large preview</a>)" alt="Cover block" >}}

### Block Grouping And Nesting

Please beware: These features are still buggy! However, plenty of time and energy is being devoted to them, so we can expect them to work smoothly soon. 

Block grouping allows to group several blocks together, so when moving them up or down on the page, all of them move together. Block nesting means placing a block inside of a block, and there is no limit to the nesting depth, so we can have blocks inside of blocks inside of blocks inside of... (you've got me by now). Block nesting is especially useful for adding columns on the layout, through a column block, and then each column can contain inside any kind of block, such as images, text, videos, etc.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d109ded5-2d34-4592-a666-39bcce8a2431/upcoming-wordpress-renaissance-group-and-nesting.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d109ded5-2d34-4592-a666-39bcce8a2431/upcoming-wordpress-renaissance-group-and-nesting.jpg" sizes="100vw" caption="Blocks can be grouped together, and nested inside each other (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d109ded5-2d34-4592-a666-39bcce8a2431/upcoming-wordpress-renaissance-group-and-nesting.jpg'>Large preview</a>)" alt="Block grouping and nesting" >}}

### Migration Of Pre-Existing Widgets

Whereas in the past there were several methods for adding content on the page (TinyMCE content, shortcodes, widgets, menus, etc.), the blocks attempt to unify all of them into a single method. Currently, newly-considered legacy code, such as widgets, is being migrated to the block format. 

Recently, the "Latest Posts" widget has been re-implemented as a block, supporting real-time preview of how the layout looks when configuring it (changing the number of words to display, showing an excerpt or the full post, displaying the date or not, etc).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78cd3c29-31fa-4dc2-9d37-597d4b9a33e7/upcoming-wordpress-renaissance-latest-posts-widget.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78cd3c29-31fa-4dc2-9d37-597d4b9a33e7/upcoming-wordpress-renaissance-latest-posts-widget.jpg" sizes="100vw" caption="The “Latest posts” widget includes several options to customize its appearance (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78cd3c29-31fa-4dc2-9d37-597d4b9a33e7/upcoming-wordpress-renaissance-latest-posts-widget.jpg'>Large preview</a>)" alt="Latest posts widget" >}}

### Motion Animation

Moving blocks up or down the page used to involve an abrupt transition, sometimes making it difficult to understand how blocks were re-ordered. Since Gutenberg 6.1, a new feature of motion animation solves this problem by adding a realistic movement to block changes, such as when creating, removing or reordering a block, giving a greatly improved visual cue of the actions taken to re-order blocks. In addition, the overall concept of motion animation can be applied throughout Gutenberg to express change and thus improve the user experience and provide better accessibility support.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5145649e-eb93-4a68-bec2-a73bca55c839/upcoming-wordpress-renaissance-motion-animation.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5145649e-eb93-4a68-bec2-a73bca55c839/upcoming-wordpress-renaissance-motion-animation.gif" width="600" alt="Motion animation" /></a><figcaption>Blocks have a smooth effect when being re-ordered. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5145649e-eb93-4a68-bec2-a73bca55c839/upcoming-wordpress-renaissance-motion-animation.gif">Large preview</a>)</figcaption></figure>

## Functionality (Hopefully) Coming Soon

According to WordPress founder Matt Mullenweg, only 10% of Gutenberg's complete roadmap has been implemented by now, so there is plenty of exciting new stuff in store for us. Work on the new features listed below has either already started, or the team is currently experimenting with them.

- **Block directory**  
A new top-level item in wp-admin which will provide block discovery. This way, blocks can be independently installed, without having to ship them through a plugin.
- **Navigation blocks**  
Currently, navigation menus must be created through their own interface. However, soon we will be able to create these through blocks and place them anywhere on the page.
- **Inline installation of blocks**  
Being able to discover blocks, the next logical step is to be able to install a new block on-the-fly, where is needed the most: On the post editor. We will be able to install a block while writing a post, use the new block to generate its HTML, save its output on the post, and remove the block, all without ever browsing to a different admin page.
- **Snap to grid when resizing images**  
When we place several images on our post, resizing them to the same width or height can prove to be a painful process of trying and failing repeatedly until getting it right, which is far from ideal. Soon, it will be possible to snap the image to a virtual grid layer which appears on the background as the image is being resized.

{{% ad-panel-leaderboard %}}

## WordPress Is Becoming Attractive (Once Again)

Several reasons support the idea that WordPress will soon become an attractive platform to code for, as it used to be once upon a time. Let's see a couple of them.

### PHP Modernization

WordPress's quest to modernize does not end with incorporating modern JavaScript libraries and tooling (React, webpack, Babel): It also extends to the server-side language: PHP. WordPress's minimum version of PHP was [recently bumped up](https://make.wordpress.org/core/2018/12/08/updating-the-minimum-php-version/) to 5.6, and should be bumped to version 7.0 as early as December 2019. PHP 7 offers remarkable advantages over PHP 5, most notably it more than [doubles its speed](https://kinsta.com/blog/php-benchmarks/#wordpress-5-benchmarks), and later versions of PHP (7.1, 7.2 and 7.3) have each become even faster.

Even though there seems to be no official plans to further upgrade from PHP 7.0 to its later versions, once the momentum is there it is easier to keep it going. And PHP is itself being improved relentlessly too. The upcoming PHP 7.4, to be released in November 2019, will include plenty of [new improvements](https://kinsta.com/blog/php-7-4/), including arrow functions and the spread operator inside of arrays (as used for modern JavaScript), and a mechanism to preload libraries and frameworks into the OPCache to further boost performance, among several other exciting features.

### Reusability Of Code Across Platforms

A great side effect of Gutenberg being decoupled from WordPress is that it can be integrated with other frameworks too. And that is exactly what has happened! Gutenberg is now [available for Drupal](https://www.drupal.org/project/gutenberg), and [Laraberg](https://github.com/VanOns/laraberg) (for [Laravel](https://laravel.com/)) will soon be officially released  (currently testing the release candidate). The beauty of this phenomenon is that, through Gutenberg, all these different frameworks can now share/reuse code!

## Conclusion

There has never been a better time to be a web developer. The pace of development for all concerned languages and technologies (JavaScript, CSS, image optimization, variable fonts, cloud services, etc) is staggering. Until recently, WordPress was looking at this development trend from the outside, and developers may have felt that they were missing the modernization train. But now, through Gutenberg, WordPress is riding the train too, and keeping up with its history of steering the web in a positive direction. 

Gutenberg may not be fully functional yet, since it has plenty of issues to resolve, and it may still be some time until it truly delivers on its promises. However, so far it is looking good, and it looks better and better with each new release: Gutenberg is steadily bringing new possibilities to WordPress. As such, this is a great time to reconsider giving Gutenberg a try (that is, if you haven't done so yet). Anyone somehow dealing with WordPress (website admins, developers, content managers, website users) can benefit from this new normal. I’d say this is something to be excited about, wouldn’t you?

{{< signature "dm, il" >}}

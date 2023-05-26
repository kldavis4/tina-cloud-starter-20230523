---
title: Power Tips For WordPress Template Developers
slug: power-tips-for-wordpress-template-developers
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b60e8c6-9068-48e1-a82b-76af0568fe48/wpmanyillus45.jpg
date: 2009-07-02T15:03:04.000Z
author: jacob-goldman
description: >-
  With its latest releases, WordPress has extended its potential well beyond
  blogging, moving toward an advanced, robust and very powerful content
  management solution. By default, WordPress delivers a very lightweight,
  minimal system that offers only basic functionalities. But where the WordPress
  core falls short, there are a wealth of plug-ins that extend its limitations.

  Plug-ins often offer simple solutions, but they are not always elegant
  solutions: in particular, they can add a noticable overhead, e.g. if they
  offer more functionality than needed. In fact, some general and frequently
  needed WordPress-functionalities can be added to the engine without bloated
  plugins, using the software itself.

  [![](https://www.smashingmagazine.com/images/wordpress-custom-fields/sm7.jpg)](https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/)

  This article presents **8 tips for WordPress template developers that address
  common CMS implementation challenges**, with little to no plug-in dependence.
  These examples are written for WordPress 2.7+ and should also work in the
  latest WordPress-version.
categories:
  - WordPress
  - PHP
  - Templates
  - Techniques (WP)
---
With its latest releases, WordPress has extended its potential well beyond blogging, moving toward an advanced, robust and very powerful content management solution. By default, WordPress delivers a very lightweight, minimal system that offers only basic functionalities. But where the WordPress core falls short, there are a wealth of plug-ins that extend its limitations.

Plug-ins often offer simple solutions, but they are not always elegant solutions: in particular, they can add a noticable overhead, e.g. if they offer more functionality than needed. In fact, some general and frequently needed WordPress-functionalities can be added to the engine without bloated plugins, using the software itself.

This article presents <strong>8 tips for WordPress template developers that address common CMS implementation challenges</strong>, with little to no plug-in dependence. These examples are written for WordPress 2.7+ and should also work in the latest WordPress-version.

You may be interested in the following related posts:

*   [10 Useful WordPress Loop Hacks](https://www.smashingmagazine.com/2009/06/10/10-useful-wordpress-loop-hacks/)
*   [Custom Field Hacks For WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/)
*   [15 Useful Twitter Hacks and Plugins For WordPress](https://www.smashingmagazine.com/2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [Mastering WordPress Shortcuts](https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/)
*   [100 Amazing Free WordPress Themes For 2009](https://www.smashingmagazine.com/2009/05/18/100-amazing-free-wordpress-themes-for-2009/)

{{% feature-panel %}}

## 1\. Associating pages with post categories

WordPress enables administrators to identify any page as the <em>posts page</em>: this is ideal for CMS implementations featuring a single news or blog feed. However, <strong>WordPress provides no simple, out-of-the-box mechanism to configure a site with multiple, independent feeds</strong>.

Here's a common use case: a company wants a simple and casual blog, and a seperate and more formal feed for press releases <em>inside</em> their "About Us" section. Let's list a few requirements mandated by a sample client seeking just that:

*   At no point should these two feeds be displayed as one.
*   Links to these feeds need to appear in page navigation.
*   The Press Release page needs to have static, maintainable content above its feed.
*   For SEO purposes, these feeds should have a page-like permalink structure: in other words, "mysite.com/_category_/press-releases" is unacceptable; the goal is "mysite.com/about-us/press-releases".

![The proposed sitemap](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c782e3d-9005-41f2-9abe-3bee57c24218/goalsitemap.gif)

As is often the case, there are several approaches one can take. Major considerations used to guage the best approach include the number of standalone feed pages (one, in this case: Press Releases) and the necessity for a "primary" feed requiring multiple category support. For this example, let us assume that "Our Blog" <em>does</em> need to behave like a full featured blog with categories.</p>

### Preparing the site

This approach to <strong>"pages with single feeds" is built upon an association created between a <em>page</em> and a <em>post category</em></strong>. The "primary" blog will simply be the "posts page" with a few template adjustments that will exclude posts from the "Press Releases" feed. To meet the SEO requirement for a logical and consistent URL structure, we will need to carefully configure and set permalinks.

*   In the "Reading" settings, ensure that the "Front page displays" option is set to "A static page", and that the "Posts page" is set to "Our Blog".
*   In the "Permalinks" settings for WordPress, ensure that "Custom Structure" is selected. The structure should be: **/%category%/%postname%/**.
*   In the page list, identify the the permalink (or slug) for the "About Us" page (using our example sitemap: let's say "about-us"). Identify the slug for the Press Releases page ("press-releases").
*   Two corresponding categories must be added: an "About Us" category with a matching permalink ("about-us"), and a "Press Releases" category with a matching permalink ("press-releases") and its parent category set to "About Us".
*   Create a post in the "Press Releases" category for testing purposes.

![The proposed sitemap](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81071056-5827-46bc-861c-067220b9b92b/wp-cat-config.gif)

### Excluding a category from the blog page

To exclude a category from the main blog page (which shows all posts across categories), the post query used for the <a title="WordPress Blog Home Template" href="https://codex.wordpress.org/Template_Hierarchy#Home_Page_display">blog page template</a> must be modified.

The WordPress codex <a title="Exclude Category form Blog Page" href="https://codex.wordpress.org/Template_Tags/query_posts#Exclude_Categories_From_Your_Home_Page">outlines the solution</a>. Simply identify the category ID for the "Press Releases" category (hovering the mouse over the category name in the admin panel and looking at the URL in the status bar is an easy way to find the ID - let's use 5 for the example), and insert the following code above the post loop:

<pre><code class="language-php">query_posts("cat=-5");</code></pre>

Note that many templates also include a list of categories in the sidebar, recent post lists, and other components that may not exclude posts from the "press releases" category. These will also need to be modified to exclude the category; this is easily supported by most WordPress calls.</p>

### Enabling the individual feed page

The feed page will require a <a title="WordPress custom page templates" href="https://codex.wordpress.org/Pages#Creating_Your_Own_Page_Templates">custom page template</a>. For this example, we named the template "Press Release Feed", and used the generic "page.php" template as a starting point (copying it and renaming it "page_press.php").

Since the requirements mandate static, editable page content above the feed, the first post loop - that drops in the page content - will be left as is. <strong>Below the code for page content output, another post query and loop will be executed</strong>. Once completed, the query should be reset using "wp_reset_query" so that items appearing after the loop - such as side navigation - can correctly reference information stored it the original page query.

The general framework for the code is below. The <a title="WordPress Post Query" href="https://codex.wordpress.org/Template_Tags/query_posts">query posts documentation on the WordPress codex</a> provides insight into great customization.

<pre><code class="language-php">query_posts('category_name=Press Releases');
if ( have_posts() ) : while ( have_posts() ) : the_post();
  //post output goes here... index.php typically provides a good template
endwhile; endif;
wp_reset_query();</code></pre>

Of course, be certain to assign the "Press Releases" page the new template, in the page editor.</p>

### The devil is in the details

Depending on the characteristics of the individual site, many additional template customizations - beyond those outlined above - will probably be necessary. In particular, this "power tip" does not cover specific strategies for handling individual post views within these isolated feeds. At the high level, using conditional <a title="WordPress in category function" href="https://codex.wordpress.org/Function_Reference/in_category">in_category</a> checks within the "single.php" template (used for output of individual posts) should provide the foundation for customizing post views based on their category. If you are interested, a more detailed article may explore these strategies in greater detail (please let us know in the comments!).</p>

### Alternative Scenarios

Creating individual page templates for each standalone feed is an efficient solution for a site with only a couple of such feeds. There are, however, WordPress-powered sites like <a href="https://www.m62.net">m62 visual communications</a> that extend the idea of category and even <em>tag</em> association with pages much more deeply. m62 features dozens of pages associated with individual blog categories, parent categories, and tags, seamlessly mixed in with standard, "feed-less" pages. In these instances, a smarter solution would involve specialized templates that <strong>match tag and category permalinks against page permalinks to dynamically create associations</strong>.

This approach can also facilitate sites that require more than one "primary" (multi-category) blog, through the use of hierarchical categories / parent categories.

Again, if there is interest, a future article can discuss these methods in detail.

## 2\. "Friendly" member only pages

Out-of-the-box, WordPress includes an option to designate any page or post as private. By default, these items do not show up in page or post lists (including navigation) and generate 404 errors when visited directly - unless the visitor is logged in. While utilitarian, more often than not, this is not ideal for usability.

Often times, sites intentionally make public visitors aware of pages or posts whose full content is only visible to members. A friendly message alerting visitors that they have reached a members-only page, with a prompt to log in, may be a better solution. Content-centric websites may tease the public with "above the fold" - or abbreviated - content for the entire audience, while enticing the visitor to log in or sign up to read the entire article.

![Linedata's blog upsells with member exclusive content](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54e04d3a-28b1-44dc-b7d7-2b3018c237b4/wp-member-example.gif)

This example offers a framework for these "hybrid" member / public pages using the latter scenario as an example. <strong>Content featured "above the fold" - or above the "more" seperator - will be visible to the general public. Content below the fold will only be available to members.</strong> In place of content below the fold, public visitors will be prompted to log in.

This approach to "hybrid" pages is built upon public, published pages with a custom field used to identify the page content as "member exclusive".

1.  Create a page or post.
2.  Start with a paragraph or two visible to the general public.
3.  Insert the "more tag" at the end of the public content.
4.  Enter content visible only to logged in members below the more tag.
5.  Add a custom field named "member_content". Set its value to 1.
6.  Publish the page with public visibility (the default).

![Hybrid public / member content](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee04dcb-1816-4963-a29b-f81df14cd070/wp-member-content.gif)

The next step involves editing the applicable template files. Typically, this will be "page.php" (pages) and "single.php" (posts). Note that if these hybrid views will only apply to pages, a developer can create a "member content" page template as an alternative to using a custom field. Doing so will eliminate the need for the custom field check and alternative outputs inside the same template.

For this example, we shall assume that we created a post (not page) with member exclusive content. Therefore, we will need to edit "single.php". Inside the template, find the <em>the_content</em> call used to drop in page and post content. Here's what this often looks like before the changes:

<pre><code class="language-php">the_content();</code></pre>

Here is the new code with the alternative "public" view:

<pre><code class="language-php">if(!get_post_meta($post-&gt;ID, 'member_content', true) || is_user_logged_in()) {
    the_content('&lt;p class="serif"&gt;Read the rest of this entry »&lt;/p&gt;');
} else {
    global $more; // Declare global $more (before the loop).
    $more = 0;  // Set (inside the loop) to display content above the more tag.
    the_content(""); //pass empty string to avoid showing "more" link
    echo "&lt;p&gt;&lt;em&gt;The complete article is only available to members. Please log in to read the article in its entirely.&lt;/em&gt;&lt;/p&gt;";
}</code></pre>

Combine this with the next tip to include a login form that sends members right back to the current page or post.</p>

## 3\. Embedding a log-in form that returns to the current location

Sometimes, sending members to the standard WordPress login form is not ideal. It may, for instance, not be consistent with the look and feel a client is seeking. There may also be instances where embedding a login form in a page - as in tip 7 - offers superior usability compared to clicking a link for the login page.

[![Museums in the Park, powered by WordPress, has a custom log-in form for members.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43d51d92-56b8-450a-af54-00c20b71be5e/mip-login.gif)](https://www.museumsinthepark.org/staff-area/)

<strong>The code below drops the WordPress login form into the template, <em>and</em> sends the user back to the page they logged in from</strong>.

<pre><code class="language-markup tmp-xml">&lt;?php if(!is_user_logged_in()) { ?&gt;
  &lt;form action="&lt;?php echo wp_login_url(get_permalink()); ?&gt;" method="post"&gt;
    &lt;label for="log"&gt;&lt;input type="text" name="log" id="log" value="&lt;?php echo wp_specialchars(stripslashes($user_login), 1) ?&gt;" size="22" /&gt; User&lt;/label&gt;&lt;br /&gt;
    &lt;label for="pwd"&gt;&lt;input type="password" name="pwd" id="pwd" size="22" /&gt; Password&lt;/label&gt;&lt;br /&gt;
    &lt;input type="submit" name="submit" value="Send" class="button" /&gt;
    &lt;label for="rememberme"&gt;&lt;input name="rememberme" id="rememberme" type="checkbox" checked="checked" value="forever" /&gt; Remember me&lt;/label&gt;
  &lt;/form&gt;
&lt;?php } ?&gt;</code></pre>

Be aware of a pitfall of this easy-to-implement power tip: if the user fails to login with the proper credentials, the log-in error will appear on the standard WordPress login form. The visitor will, however, still be redirected back to the original page upon successful log-in.</p>

## 4\. Identifying the Top Level Page

The "top level page" is the highest level page within the current branch of the sitemap. For example, if you consider the page below, you'll find that "Support &amp; Resources", "Finding Support", and "Support for Patients" all share the top level page "Support &amp; Resources".

![The top level page is Support and Resources](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a5f8e2c-c630-497f-a51c-19439e212137/identify-top-level.jpg)

There are some relatively new plug-ins that make "section", or "top level page" WordPress navigation a cinch, such as <a title="WordPress CMS Navigation" href="https://www.cmurrayconsulting.com/software/wordpress-simple-section-navigation/">Simple Section Navigation</a>. However, there are plenty of instances (outside of navigation) where the template may need to be aware of the current top level page.

For instance, you many want to be able to style certain design elements, such as the navigation bar's background image, depending on the currently chosen section.  This can be achieved by checking the page ID of the top level page inside the header, and dropping in additional styles when the IDs for those top level pages were found.

[![Top level navigation changes its background image depending on the top level page](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e45abdb-60db-40d1-b48a-c096db71bb61/nav-changes-top-level.jpg)](https://www.sge-corp.com)

Here is how it works. Although WordPress offers no built in call to determine the <strong>top level page, it can be found with a single line of code</strong> in the template:

<pre><code class="language-php">$top_level = ($post-&gt;post_parent) ? end(get_post_ancestors($post)) : $post-&gt;ID;</code></pre>

Using a <a href="https://www.addedbytes.com/php/ternary-conditionals/">ternary conditional</a>, this line of code checks the value of <em>$post-&gt;post_parent</em>, which returns the current page's parent page ID, if one exists. If the conditional is evaluated as "true" (as any positive integer will), than the current page has some "ancestory"; in other words, it is inside of a page hierarchy or branch in the sitemap. If the conditional fails, the page is either a top level page, or not in any page ancestory (i.e. a <em>post</em> on a site without a blog "page" assigned).

If the current page has ancestory, an array containing the hierarchy "above" the page (parents, grandparents, etc) can be retrieved using the <em>get_post_ancestors</em> function. The last value in the array that function returns is always the ID of the top level page. Jump right to the last value using PHP's <em>end</em> function. If the conditional fails (no ancestory), the code simply grabs the current page ID.

Keep in mind that, in many instances, this information is only useful when WordPress is working with an actual page (as opposed to a post, 404 page, etc). Therefore, this function and code that uses the top_level variable, may need to be wrapped inside a check that confirms that WordPress is loading a <em>page</em>: see the <a href="https://codex.wordpress.org/Function_Reference/is_page"><em>is_page()</em> function</a>.</p>

## 5\. Breadcrumb Navigation - without a plug-in

![Example of a WordPress site with breadcrumb navigation](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbb5bf3c-ec8d-416c-a7ac-ef3e81518140/breadcrumbs.jpg)

There are plenty of WordPress extensions that generate <a href="https://www.smashingmagazine.com/2009/03/17/breadcrumbs-in-web-design-examples-and-best-practices-2/">breadcrumb navigation</a>. But you can actually <strong>create custom breadcrumb navigation with only a handful of lines of code</strong> in the template, opening up greater control and, potentially, less overhead. This approach to breadcrumbs builds on the <em>get_post_ancestors</em> function discussed in tip #4.

This tip won't review formatting of breadcrumbs; for this example, the breadcrumbs will be dropped in an unordered bullet list. As it happens, lists of links tend to be a good format for search engines, and you can format them almost any way you like.

To start with, here is a basic implemenation of breadcrumbs that only deals with <em>pages</em> and includes a breadcrumb for “home” (the front page of the site) at the beginning of the list. Depending on the design of a particular template, some checks may need to placed around this code. In this example, it will be assumed that this code will be placed in the <em>header.php</em> template file, that the crumbs should appear only on pages, and that it should not show up on the front page. The current page and front page link will also be assigned special CSS classes for styling purposes.

<pre><code class="language-php">if (is_page() &amp;&amp; !is_front_page()) {
   echo '&lt;ul id="breadcrumbs"&gt;';
   echo '&lt;li class="front_page"&gt;&lt;a href="'.get_bloginfo('url').'"&gt;Home&lt;/a&gt;&lt;/li&gt;';
   $post_ancestors = get_post_ancestors($post);
   if ($post_ancestors) {
      $post_ancestors = array_reverse($post_ancestors);
      foreach ($post_ancestors as $crumb)
          echo '&lt;li&gt;&lt;a href="'.get_permalink($crumb).'"&gt;'.get_the_title($crumb).'&lt;/a&gt;&lt;/li&gt;';
   }
   echo '&lt;li class="current"&gt;&lt;a href="'.get_permalink().'"&gt;'.get_the_title().'&lt;/a&gt;&lt;/li&gt;';
   echo '&lt;/ul&gt;';
}</code></pre>

If the WordPress implementation has a static front page and has been assigned a "blog" page, one might want to show the breadcrumb path to the blog page. This can be accomplished by adding <code>is_home()</code> to the conditional check at the top:

<pre><code class="language-php">if ((is_page() &amp;&amp; !is_front_page()) || is_home()) {
   ...</code></pre>

The next evolution of this code involves the inclusion of breadcrumbs for individual category archives as well as individual posts. Note that WordPress allows posts to be assigned to multiple categories; to avoid making our breadcrumb trail unweildly, the script will simply grab the <em>first</em> category assigned to the post. For the sake of simplicity, the example will be assumed that hierarchical categories are not in play.

<pre><code class="language-php">if ((is_page() &amp;&amp; !is_front_page()) || is_home() || is_category() || is_single()) {
   echo '&lt;ul id="breadcrumbs"&gt;';
   echo '&lt;li class="front_page"&gt;&lt;a href="'.get_bloginfo('url').'"&gt;Home&lt;/a&gt;&lt;/li&gt;';
   $post_ancestors = get_post_ancestors($post);
   if ($post_ancestors) {
      $post_ancestors = array_reverse($post_ancestors);
      foreach ($post_ancestors as $crumb)
          echo '&lt;li&gt;&lt;a href="'.get_permalink($crumb).'"&gt;'.get_the_title($crumb).'&lt;/a&gt;&lt;/li&gt;';
   }
   if (is_category() || is_single()) {
      $category = get_the_category();
      echo '&lt;li&gt;&lt;a href="'.get_category_link($category[0]-&gt;cat_ID).'"&gt;'.$category[0]-&gt;cat_name.'&lt;/a&gt;&lt;/li&gt;';
   }
   if (!is_category())
      echo '&lt;li class="current"&gt;&lt;a href="'.get_permalink().'"&gt;'.get_the_title().'&lt;/a&gt;&lt;/li&gt;';
   echo '&lt;/ul&gt;';
}</code></pre>

There are many ways to extend the breadcrumb navigation further. For instance, a developer might want breadcrumbs for different types of archives (tags, months, etc), or may incorporate hierarchical categories. While this article won’t walk through every possible implementation, the samples above should provide you with a solid framework to work with.</p>

## 6\. Creating sidebar content elements

Many websites feature distinct sidebars with common elements represented throughout the site, such as section navigation, contact information, and special badges (i.e. “Follow us on Twitter”). It is also common for sites to <strong>feature more basic HTML blocks in the sidebar that are associated with a single page, or several pages</strong> that may or may not be tied together in any logical way.

Some content management systems enable the idea of multiple content blocks out of the box. For instance, <a href="https://www.citysoft.com">CitySoft Community Enterprise</a> allows the editor to select from a variety of page layouts, some of which include multiple blocks of content that can be edited independently. This is convenient for some, though it does have some limitations: (1) it can be hard to integrate the prefabbed layout blocks into unusual areas in the overall site template, and (2), reusing some of these content blocks for multiple pages is not possible (without some additional, complicated custom development).

Here's how to <strong>implement reusable "sidebar elements" in WordPress</strong>. For the sake of simplicity, this example assumes that only one sidebar element can be assigned to a page.

Fundamentally, these sidebar elements will simply be pages. Although non-essential, it can be a good organizational practice to create a page called "sidebars" that will contain all of the sidebar pages. Be careful to exclude this page in top level navigation and any other page lists or sitemaps. Sidebar elements are then constructed as "private" pages (so they cannot be searched or viewed independently by general visitors), with the "sidebar" container page set as the parent page. The title of the sidebar page will be used for the title of the sidebar element.

![Editing a sidebar on the left; on the front end on the right](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2527351a-beba-4f23-8946-a85c65e9ad76/sidebars.jpg)

Once the sidebar has been created, the editor will need the ID of the sidebar page. The easiest way to find this is by rolling over the page title in the admin page list, and looking for the “id” in the URL (typically in the statusbar).

To assign the sidebar to a page, a new <a href="https://codex.wordpress.org/Using_Custom_Fields">custom field</a> is assigned to the page that will hold the sidebar called "sidebar". The value for this field is the page ID of the sidebar page.

Now, in the sidebar template file (or wherever the sidebar element should appear), some code is included that checks for the custom field, and - if found - drops in the referenced page. To make the process of dropping the sidebar page content a bit more simple, the example will use the light weight plug-in, <a href="https://www.vtardia.com/improved-include-page/">Improved Include Page</a>. Here's the code, which also drops "h2" tags around the page title:

<pre><code class="language-php">$sidebar_pg = get_post_meta($post-&gt;ID,'sidebar', true);
if (function_exists('iinclude_page') &amp;&amp; $sidebar_pg) {
   include_page($sidebar_pg,'displayTitle=true&amp;titleBefore=&lt;h2&gt;&amp;titleAfter=&lt;/h2&gt;

      &amp;displayStyle=DT_FULL_CONTENT&amp;allowStatus=publish,private');
}</code></pre>

## 7\. Feature selected posts on the front page

Many CMS implementations feature some selected items from the blog feed on the home page, or even throughout the site in a sidebar or footer element. Content editors are, wisely, selective about what merits a front page mention. Here’s how to <strong>implement a selective blog feed</strong> that can be placed on a front page template or anywhere else in the design.

[![Featured news feed on front page](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d37b9a57-bd74-42e6-a3f1-3a3c7525eddd/featurednews-sge.jpg)](https://www.sge-corp.com)

A special category is needed to classify posts as "Featured"; a category named "Featured" or "Front Page" is a good convention. For the content editor, marking a post as "featured" is as simple as adding it to this category (remember: posts can have multiple categories). On the template side, the ID of the "featured" category will be needed. The easiest way to find the category ID is by rolling over the category "edit link" inside WordPress administration and noting the ID in the URL (typically in the status bar).

Using this ID ("4" in the example), and the number of posts to feature on the home page (let's say three), the following code will list the featured posts beginning with the recent ones.

<pre><code class="language-php">echo "&lt;h3&gt;Featured Blog Posts&lt;/h3&gt;";
echo "&lt;ul&gt;";
$feat_posts = get_posts('numberposts=4&amp;category=71');
foreach ($feat_posts as $feat) {
   echo '&lt;li&gt;&lt;a href="'.get_permalink($feat-&gt;ID).'"&gt;'.$feat-&gt;post_title.'&lt;/a&gt;&lt;/li&gt;';
}
echo "&lt;/ul&gt;";</code></pre>

As with the other examples, this code can be extended in a number of ways. For example, the <a href="https://www.sge-corp.com">SGE Corporation</a> front page features the excerpt for the most recent item. The excerpt can be manually entered in the "excerpt" field or pulled automatically (if none is provided) by grabbing a certain number of characters from the beginning of the post's content.</p>

## 8\. Highlight current post's category

WordPress page lists assign special classes to each item, including classes that indicate whether a page is the current page, a parent page, an ancestor page, and so forth. Category lists do assign a special class (<code>current-cat</code>) to appropriate list items when the user is browsing a category's archive. Unfortunately, <strong>categories do not, by default, get this special class assigned to them when the user is on a post inside the category</strong>. However, one can override this default limitation by grabbing the current category ID and passing it to the <em>wp_list_categories</em> function.

<pre><code class="language-php">$category = get_the_category();
wp_list_categories('current_category='.$category[0]-&gt;cat_ID);</code></pre>

Note that there is one significant downside to this approach – only some category can be passed to the list categories function. So if a post is assigned to multiple categories, only the first category will be highlighted. However, if a site has distinct categories (say a news feed and an editorial feed), this can help a template developer treat the category more like a page navigation item.</p>

## Related posts

You may be interested in the following related posts:

*   [10 Useful WordPress Loop Hacks](https://www.smashingmagazine.com/2009/06/10/10-useful-wordpress-loop-hacks/)
*   [Custom Field Hacks For WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/)
*   [15 Useful Twitter Hacks and Plugins For WordPress](https://www.smashingmagazine.com/2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [Mastering WordPress Shortcuts](https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/)
*   [100 Amazing Free WordPress Themes For 2009](https://www.smashingmagazine.com/2009/05/18/100-amazing-free-wordpress-themes-for-2009/)


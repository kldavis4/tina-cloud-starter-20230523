---
title: 'New WordPress Power Tips For Template Developers And Consultants'
slug: new-wordpress-power-tips-for-template-developers-and-consultants
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/051e202c-b4b8-4d8b-abe1-6759d577fd2c/body-neat-stuff.jpg
date: 2011-05-10T07:41:02.000Z
author: jacob-goldman
summary: >-
  Jacob Goldman reviews some of WordPress’s new tips that can help template developers and consultants up their game even further. Learn about adding excerpts to pages, removing the “Links” menu item, and more.
description: >-
  Jacob Goldman reviews some of WordPress’s new tips that can help template developers and consultants up their game even further. Learn about adding excerpts to pages, removing the “Links” menu item, and more.
categories:
  - WordPress
  - PHP
  - Templates
  - Techniques (WP)
---

It has been a big year for WordPress. If there were still some lingering doubts about its potency as a full-fledged content management system, then the full support for <a href="https://wordpress.org/support/article/taxonomies/">custom taxonomies</a> and <a href="https://wordpress.org/support/article/post-types/">custom post types</a> in WordPress 3.0 core should have put them to rest. WordPress 3.1 took those leaps one step further, polishing custom taxonomies with <a href="https://www.wpmods.com/query-multiple-taxonomies-in-wp-3-1">multi-taxonomy query support</a>, polishing custom post types with <a href="https://core.trac.wordpress.org/ticket/13818">native template support for archives and feeds</a>, and introducing features (like the “admin bar”) that make it easier to quickly edit and add content from the front end.

In the broader community, we’ve seen incredible plug-in suites such as <a href="https://www.buddypress.org">BuddyPress</a> mature, and even the emergence of independent WordPress-dedicated hosting services, such as <a href="https://page.ly">page.ly</a>. To celebrate WordPress’s progress, let’s review some new tips that can help template developers and consultants up their game even further.

{{% feature-panel %}}

### Foreword for New Developers: What is a “Hook”?

Most of these tips take advantage of core WordPress “hooks.” Hooks are points in the code that **allow any number of outside functions to “hook in” and intercept the code** in order to add to or modify behavior at a particular point. Hooks are the fundamental concept that enables virtually all plug-ins. WordPress has two kinds of hooks: actions and filters.

**Action hooks** are intended to allow developers to intercept certain activities and execute some additional functionality. For instance, when a new post is published, the developer may want to add some extra functionality, such as posting the title and a link to Twitter.

**Filter hooks** allow the developer to intercept and *modify* data that is being processed by WordPress for display or saving. For instance, the developer may want to inject an advertisement into the content before displaying the post on the screen.

Learn more about hooks on the <a href="https://codex.wordpress.org/Plugin_API">official WordPress codex</a>.

### The Underused Pagination Function

Many great plug-ins are in the official WordPress repository. But using fancy plug-ins to add fairly basic functionality to your theme is often like driving a tractor trailer to go around the block. There’s usually a lighter, smarter way: a bike or even a car. And while plug-ins are a fine solution for consultants who are staging a complete roll-out, they’re awkward solutions for theme developers who want to sell standalone templates.

<a href="https://wordpress.org/extend/plugins/wp-pagenavi/">WP-PageNavi</a> is one of the most popular WordPress plug-ins; and no doubt it is well developed. It is ideal for those who are uncomfortable digging into WordPress code. But did you know that WordPress has a function built right into core that (with a bit of savvy about its parameters) can generate pagination links for everything from comments to post archives to post pages?

The function in question is <a href="https://developer.wordpress.org/reference/functions/paginate_links/"> <code>paginate_links()</code></a>. (For those who like to fish around in the source, it’s on line 1954 of *general-template.php* in the *wp-includes* folder as of WordPress 3.1.) Believe it or not, this underused function has been around since 2.1. Another function, <a href="hhttps://developer.wordpress.org/reference/functions/paginate_comments_links/"><code>paginate_comment_links()</code></a>, is actually a wrapper for this function that is designed specifically for paging comments, and it has been around since 2.7.

The function takes an array of parameters that make it versatile enough to use for any kind of paging:

*   `base` This is the path for the page number links, not including the pagination-specific part of the URL. The characters `%_%` will be substituted in that URL for the page-specific part of the URL.
*   `format` This is the “page” part of the URL. `%#%` is substituted for the page number. For example, `page/%#%` or `?page=%#%`.
*   `total` The total number of pages available.
*   `current` The current page number.
*   `show_all` Lists all page links, instead of limiting it to a certain number of links to the left and right of the current page.
*   `prev_next` Includes the “Previous” and “Next” links (if applicable), just as you might normally do with the `previous_posts_link()` function.
*   `prev_text` and `next_text` Text to put inside the “Previous” and “Next” links.
*   `end_size` The number of page links to show at the end. Defaults to `1` (e.g. 1 2 3 … 10).
*   `mid_size` The number of pages to show on either side of the current page. Defaults to `2` (example: 1 … 3 4 5 6 7 … 10).
*   `type` Allows you to specify an output style. The default is “plain,” which is just a string of links. Can also be set to list (i.e. `ul` and `li` representation of links) and array (i.e. returns an array of page links to be potentially outputted any way you like in code).
*   You can also add query arguments and fragments.

Because the function takes all of the information needed to generate page links, you can use it for pretty much any pagination list, as long as you have some key information, such as the number of pages and the current page. Let’s use this function to generate pagination links for an article archive such as a category or main post index:

<pre><code class="language-php">// get total number of pages
global $wp_query;
$total = $wp_query-&gt;max_num_pages;
// only bother with the rest if we have more than 1 page!
if ( $total &gt; 1 )  {
     // get the current page
     if ( !$current_page = get_query_var('paged') )
          $current_page = 1;
     // structure of “format” depends on whether we’re using pretty permalinks
     $format = empty( get_option('permalink_structure') ) ? '&amp;page=%#%' : 'page/%#%/';
     echo paginate_links(array(
          'base' =&gt; get_pagenum_link(1) . '%_%',
          'format' =&gt; $format,
          'current' =&gt; $current_page,
          'total' =&gt; $total,
          'mid_size' =&gt; 4,
          'type' =&gt; 'list'
     ));
}</code></pre>

Here's the HTML generated by that code on the first of 10 posts pages:

<pre><code class="language-php">&lt;ul class='page-numbers'&gt;
     &lt;li&gt;&lt;span class='page-numbers current'&gt;1&lt;/span&gt;&lt;/li&gt;
     &lt;li&gt;&lt;a class='page-numbers' href='https://mysite.com/page/2/'&gt;2&lt;/a&gt;&lt;/li&gt;
     &lt;li&gt;&lt;a class='page-numbers' href='https://mysite.com/page/3/'&gt;3&lt;/a&gt;&lt;/li&gt;
     &lt;li&gt;&lt;a class='page-numbers' href='https://mysite.com/page/4/'&gt;4&lt;/a&gt;&lt;/li&gt; 
     &lt;li&gt;&lt;a class='page-numbers' href='https://mysite.com/page/5/'&gt;5&lt;/a&gt;&lt;/li&gt;
     &lt;li&gt;&lt;span class='page-numbers dots'&gt;...&lt;/span&gt;&lt;/li&gt;
     &lt;li&gt;&lt;a class='page-numbers' href='https://mysite.com/page/10/'&gt;10&lt;/a&gt;&lt;/li&gt;
     &lt;li&gt;&lt;a class='next page-numbers' href='https://mysite.com/page/2/'&gt;Next &amp;raquo;&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;</code></pre>

Here’s a screenshot of the pagination on m62 visualcommunications, built using the <code>em&gt;paginate_links</code> function.

<figure><a href="https://www.m62.net"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="97983" title="m62 pagination" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66479780-e574-4009-ae52-03da963d51e2/m62-pages.jpg" alt="" width="500" height="97" /></a><figcaption>Screenshot of the pagination on m62 visualcommunications.</figcaption></figure>

### “I Wish Posts Were Called Articles For My Client.”

Have you ever wished you could change the wording of a built-in menu item or notification? If you’re a bit WordPress-savvy, you may have considered generating your own translations file. But you might not know that you can actually “hook” the translation functions in WordPress, capturing their input and modifying their output.

Be careful with this one. The code you put in this hook will run every time WordPress runs a string through its translation filters. Complex cases and conditionals could add a considerable amount of overhead, especially when loading pages filled with translation strings, such as the administrative pages. But if you just want to rename one thing that confuses your client (for example, maybe changing “Posts” to “Articles” for that corporate client who doesn’t “blog” yet), then these hooks can be very handy.

<pre><code class="language-php">// hook the translation filters
add_filter( 'gettext', 'change_post_to_article' );
add_filter( 'ngettext', 'change_post_to_article' );

function change_post_to_article( $translated ) {
$translated = str_ireplace( 'Post', 'Article', $translated ); // ireplace is PHP5 only
return $translated;
}</code></pre>

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="97984" title="Change &quot;Posts&quot; to &quot;Articles&quot;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a725a21-8eca-40e4-8ab9-b047feae440a/translations.jpg" alt="" width="500" height="115" /><figcaption>Changing “Posts” to “Articles”.</figcaption></figure>

{{% ad-panel-leaderboard %}}

### Redirect Failed Log-Ins

Adding a log-in form to the front end of WordPress is pretty easy. WordPress 3.0 gave us the flexible <a href="https://developer.wordpress.org/reference/functions/wp_login_form/">wp_login_form()</a> function, which displays a log-in form that can be customized with a number of arguments. By default, it will redirect the user back to the current page upon successful authentication, but we can also customize the redirect location.

<pre><code class="language-php">wp_login_form(array( 'redirect' =&gt; site_url() )); // will redirect back to the website’s home page</code></pre>

There’s just one problem: it will only redirect upon successful authentication! If your idea was to hide the default WordPress log-in screen, then sending users who fail at a log-in attempt back to the default log-in screen probably isn’t ideal. Here’s a hook and some code that you can put in your *functions.php* file that will redirect failed log=ins to any location of your choosing.

<pre><code class="language-php">add_action( 'wp_login_failed', 'my_front_end_login_fail' );  // hook failed login

function my_front_end_login_fail( $username ) {
     $referrer = $_SERVER['HTTP_REFERER'];  // where did the post submission come from?
     // if there's a valid referrer, and it's not the default log-in screen
     if ( !empty($referrer) &amp;&amp; !strstr($referrer,'wp-login') &amp;&amp; !strstr($referrer,'wp-admin') ) {
          wp_redirect( $referrer . '?login=failed' );  // let's append some information (login=failed) to the URL for the theme to use
          exit;
     }
}</code></pre>

### Adding Excerpts to Pages

With the addition of support for custom post types, content types (including the built-in Post and Page types) are more like abstract objects. Each content type can support any number of core features, such as the HTML editor, titles, featured images and so forth. One of these core features is the “excerpt.” By default, Pages do not support excerpts. Did you know that adding excerpt support to the built-in Page type is as simple as adding a single line of code?

<pre><code class="language-php">add_action( 'init', 'my_add_excerpts_to_pages' );
function my_add_excerpts_to_pages() {
 add_post_type_support( 'page', 'excerpt' );
}</code></pre>

Technically, that was a couple of lines of code, but many themes already hook <code>init</code>, so the hook might not be necessary.

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="97986" title="Page Excerpt" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a38a4f2-35f6-4dd2-b48a-959c719506df/page-excerpt.jpg" alt="" width="500" height="449" /><figcaption>Adding excerpts to Pages.</figcaption></figure>

### Add Body Classes Based on Special Conditions

If a theme is well constructed, then it would use the <a href="https://codex.wordpress.org/Function_Reference/body_class">body_class()</a> function to automatically generate classes for the <code>body</code> tag based on the properties of the page being viewed, like <code>category</code>, <code>category-3</code>, and <code>logged-in</code>.

Some websites may have sections that should share some styling but aren’t unified by any of the default classes generated by <code>body_class</code>. Say we want page ID <code>7</code>, category ID <code>5</code> and the archive for the tag <code>neat</code> to share the body class <code>neat-stuff</code>, so that we can add a number of styling properties to them all without cluttering the style sheet.

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="97988" title="New body class" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/051e202c-b4b8-4d8b-abe1-6759d577fd2c/body-neat-stuff.jpg" alt="" width="500" height="199" /><figcaption>Adding body class.</figcaption></figure>

Luckily, we can hook the <code>body_class()</code> output!

<pre><code class="language-php">add_filter( 'body_class', 'my_neat_body_class');
function my_neat_body_class( $classes ) {
     if ( is_page(7) || is_category(5) || is_tag('neat') )
          $classes[] = 'neat-stuff';

     return $classes;
}</code></pre>

### “You Can Have Settings Access, But Don’t Say We Didn’t Warn You!”

Clients often expect full administrative access (and rightly so), including access to settings pages. Let’s look at how we can hook admin “notices” (those warning boxes generated by some plug-ins) to send some warnings to administrative users when they are on settings pages.

<pre><code class="language-php">add_action( 'admin_notices', 'my_admin_notice' );
function my_admin_notice(){
     global $current_screen;&lt;/div&gt;
     if ( $current_screen-&gt;parent_base == 'options-general' )
          echo '&lt;div&gt;&lt;p&gt;Warning - changing settings on these pages may cause problems with your website’s design!&lt;/p&gt;&lt;/div&gt;';
}</code></pre>

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="97990" title="Warnings on settings pages" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0a640ba-038c-41b9-9f18-0c0cb3d3b72d/warning-settings.jpg" alt="" width="500" height="85" /><figcaption>Warnings on setting pages.</figcaption></figure>

### Remove the “Links” Menu Item

With WordPress increasingly being used for full website implementations, the blog roll and links feature is being used less and less. Thankfully, a new, <a href="https://developer.wordpress.org/reference/functions/remove_menu_page/">little-known function</a> added in WordPress 3.1 makes it very easy to remove unwanted menu items such as “Links.”

<pre><code class="language-php">add_action( 'admin_menu', 'my_admin_menu' );

function my_admin_menu() {
     remove_menu_page('link-manager.php');
}</code></pre>

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="97992" title="WordPress - remove links from the menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/204d5d47-3d9f-4813-8297-0fb551cfe3db/no-links.jpg" alt="" width="154" height="126" /><figcaption>Remove unwanted menu items.</figcaption></figure>

### Take Out the Dashboard News Feeds… and Add a New One of Your Own

If you build WordPress websites for clients, then the number of WordPress news feeds loaded by default in the dashboard might be an annoyance. If you’re clever, you might just inject some of your own client’s news.

<pre><code class="language-php">add_action('wp_dashboard_setup', 'my_dashboard_widgets');
function my_dashboard_widgets() {
     global $wp_meta_boxes;
     // remove unnecessary widgets
     // var_dump( $wp_meta_boxes['dashboard'] ); // use to get all the widget IDs
     unset(
          $wp_meta_boxes['dashboard']['normal']['core']['dashboard_plugins'],
          $wp_meta_boxes['dashboard']['side']['core']['dashboard_secondary'],
          $wp_meta_boxes['dashboard']['side']['core']['dashboard_primary']
     );
     // add a custom dashboard widget
     wp_add_dashboard_widget( 'dashboard_custom_feed', 'News from 10up', 'dashboard_custom_feed_output' ); //add new RSS feed output
}
function dashboard_custom_feed_output() {
     echo '&lt;div class="rss-widget"&gt;';
     wp_widget_rss_output(array(
          'url' =&gt; 'https://www.get10up.com/feed',
          'title' =&gt; 'What's up at 10up',
          'items' =&gt; 2,
          'show_summary' =&gt; 1,
          'show_author' =&gt; 0,
          'show_date' =&gt; 1
     ));
     echo "&lt;/div&gt;";
}</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82724e56-c1ed-40a4-886f-28721a90794c/10up-news.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="97994" title="Consultant's news feed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82724e56-c1ed-40a4-886f-28721a90794c/10up-news.jpg" alt="" width="500" height="220" /></a><figcaption>Inject some of your own client’s news in the dashboard.</figcaption></figure>

### Add Your Own Credits to the Administrative Footer

If you build WordPress websites for clients, then you should certainly make sure that WordPress gets its due. It wouldn’t hurt to sneak in a little credit to your agency either.

<pre><code class="language-php">add_filter( 'admin_footer_text', 'my_admin_footer_text' );
function my_admin_footer_text( $default_text ) {
     return '&lt;span id="footer-thankyou"&gt;Website managed by &lt;a href="https://www.get10up.com"&gt;10up&lt;/a&gt;&lt;span&gt; | Powered by &lt;a href="https://www.wordpress.org"&gt;WordPress&lt;/a&gt;';
}</code></pre>

<figure><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="97997" title="Customized administrative footer" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ccda11b-7e7e-4047-a6d2-e82a8c080582/admin-footer.jpg" alt="" width="500" height="66" /><figcaption>Add your own credits.</figcaption></figure>

{{% ad-panel-leaderboard %}}

### Other Resources

Here are more tips for developers who build websites for clients:

*   [Customizing WordPress Administration with Twenty-Ten Child Theme](https://www.get10up.com/blog/2011/03/customizing-wordpress-admin/)
*   [10 Techniques for Customizing the WordPress Admin Panel](https://sixrevisions.com/wordpress/10-techniques-for-customizing-the-wordpress-admin-panel/)

More WordPress power tips from Smashing Magazine:

*   [Advanced Power Tips for WordPress Template Developers: Reloaded](https://www.smashingmagazine.com/2009/12/14/advanced-power-tips-for-wordpress-template-developers-reloaded/)
*   [Advanced Power Tips for WordPress Template Developers](https://www.smashingmagazine.com/2009/11/25/advanced-power-tips-for-wordpress-template-developers/)
*   [Power Tips for WordPress Template Developers](https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/)

### Further Reading

- [10 Useful WordPress loop hacks](https://www.smashingmagazine.com/2009/06/10-useful-wordpress-loop-hacks/)
- [The Modern Way To Create And Host A WordPress Site](https://www.smashingmagazine.com/2022/05/elementor-modern-way-create-host-wordpress-site/)
- [Building Gatsby Themes For WordPress-Powered Websites](https://www.smashingmagazine.com/2021/12/building-gatsby-themes-wordpress-powered-websites/)
- [Automatically Transforming And Optimizing Images And Videos On Your WordPress Website](https://www.smashingmagazine.com/2021/11/transforming-optimizing-images-videos-wordpress-website/)

{{< signature "al, il, mrn" >}}

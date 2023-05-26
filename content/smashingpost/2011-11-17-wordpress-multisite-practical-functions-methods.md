---
title: 'WordPress Multisite: Practical Functions And Methods'
slug: wordpress-multisite-practical-functions-methods
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d09fcde-2d46-45f1-9ff2-cb3c3c2b61e4/wordpress-grudge.jpg
date: 2011-11-17T16:16:39.000Z
author: kevin-leary
description: >-
  Multisite is a powerful new feature that arrived with the release of WordPress 3.0\. It allows website managers to host multiple independent websites with a single installation of WordPress.
categories:
  - WordPress
  - PHP
  - Essentials
  - Functions
---
Although each “website” in a network is independent, there are many ways to share settings, code and content throughout the entire network.

Since the beginning of the year, I’ve been developing themes and plugins for a WordPress Multisite-powered content network. During that time I’ve learned many powerful tips and tricks unique to Multisite. This guide will introduce you to a few Multisite-specific functions, along with real-world programming examples that you can begin using today. Hopefully, it will open your eyes to a few of the new possibilities available in Multisite.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Advanced WordPress Management With WP-CLI](https://www.smashingmagazine.com/2015/09/wordpress-management-with-wp-cli/)
*   [How To Develop WordPress Locally With MAMP](https://www.smashingmagazine.com/2011/09/developing-wordpress-locally-with-mamp/)
*   [Useful WordPress Tools, Themes And Plugins](https://www.smashingmagazine.com/2012/03/useful-wordpress-tools-themes-plugins/)
*   [Improve And Refine Your WordPress Theme Development](https://www.smashingmagazine.com/2013/02/wp-theme-development-process/)

{{% feature-panel %}}

## Why Use Multisite?

Multisite is a great option for freelancers, businesses and organizations that manage multiple WordPress websites. Whether you’re a freelancer who wants to provide hosting and maintenance to clients, a college organization looking to centralize the management of your websites, or a large news publisher trying to isolate silos for different departments, Multisite is the answer.

Managing multiple websites with a single installation of WordPress enables you to easily upgrade the core, plugins and themes for every website in a network. You can share functionality across multiple websites with network plugins, as well as standardize design elements across multiple websites using a parent theme.</p>

### Overview of Benefits

*   Users are able to easily access and manage multiple websites with a single user account and profile.
*   Users can access a particular website or every website using the same account.
*   Information from one website can be completely isolated from others.
*   Information from one website can be easily shared with others.
*   Theme functionality can be shared across multiple websites using a [parent-child theme relationship](https://www.wpbeginner.com/wp-themes/how-to-create-a-wordpress-child-theme-video/) or a [functionality plugin](https://wpcandy.com/teaches/how-to-create-a-functionality-plugin).
*   Updates and upgrades can be rolled out across multiple websites in less time, reducing overhead and maintenance costs.
*   Customizations to WordPress can be efficiently distributed in a centralized, cascading method using network-wide plugins.

I won’t explain how to <a href="https://codex.wordpress.org/Create_A_Network">install and configure Multisite</a>. If you need help, plenty of great articles are available in the <a href="https://codex.wordpress.org/">WordPress Codex</a>.</p>

## Working With Multisite Functions

Multisite-enabled WordPress installations contain additional functions and features that theme developers can use to improve the experience of a website. If you find yourself developing themes and plugins for WordPress Multisite, consider the following tips to customize and improve the connectivity of the network.</p>

### Displaying Information About a Network

You might find yourself in a situation where you would like to display the number of websites or users in your network. Providing a link to the network’s primary website would also be nice, so that visitors can learn more about your organization.

Multisite stores global options in the <code>wp_sitemeta</code> database table, such as the <strong>network’s name</strong> (<code>site_name</code>), the <strong>administrator’s email address</strong> (<code>admin_email</code>) and the <strong>primary website’s URL</strong> (<code>siteurl</code>). To access these options, you can use the <code>get_site_option()</code> function.

In this example, I’ve used the <code>get_site_option()</code> function along with <code>get_blog_count()</code> and <code>get_user_count()</code> to display a sentence with details about a network.

<pre><code class="language-php">&lt;?php if( is_multisite() ): ?&gt;

   The <a href="&lt;?php echo esc_url( get_site_option( 'siteurl' ) ); ?&gt;">&lt;?php echo esc_html( get_site_option( 'site_name' ) ); ?&gt; network</a> currently powers <strong>&lt;?php echo get_blog_count(); ?&gt;</strong> websites and <strong>&lt;?php echo get_user_count(); ?&gt;</strong> users.

&lt;?php endif; ?&gt;</code></pre>

This small snippet of code will display the following HTML:

<pre><code class="language-php">The <a href="https://www.smashingmagazine.com">Smashing Magazine network</a> currently powers <strong>52</strong> websites and <strong>262</strong> users.</code></pre>

Many useful Multisite functions can be found in the <a href="https://core.trac.wordpress.org/browser/tags/3.2.1/wp-includes/ms-functions.php"><code>/wp-includes/ms-functions.php</code></a> file. I highly suggest browsing the <a href="https://core.trac.wordpress.org/browser/tags/3.2.1/">Trac project</a> yourself. It’s a great way to find new functions and to become familiar with <a href="https://codex.wordpress.org/WordPress_Coding_Standards">WordPress coding standards</a>.</p>

### Build a Network Navigation Menu

Many networks have consistent dynamic navigation that appears on all websites, making it easy for visitors to browse the network. Using the <a href="https://codex.wordpress.org/Class_Reference/wpdb"><code>$wpdb</code> database class</a>, along with the <code>get_site_url()</code>, <code>home_url()</code>, <code>get_current_blog_id()</code>, <code>switch_to_blog()</code> and <code>restore_current_blog()</code> functions, we can create a fully dynamic network menu, including a class (<code>.current-site-item</code>) to highlight the current website.

The SQL query we’ve created in this example has the potential to become very large, possibly causing performance issues. For this reason, we’ll use the <a href="https://codex.wordpress.org/Transients_API">Transients API</a>, which enables us to temporarily store a cached version of the results as network website “transients” in the <code>sitemeta</code> table using the <code>set_site_transient()</code> and <code>get_site_transient()</code> functions.

Transients provide a simple and standardized way to store cached data in the database for a set period of time, after which the data expires and is deleted. It’s very similar to storing information with the <a href="https://codex.wordpress.org/Options_API">Options API</a>, except that it has the added value of an expiration time. Transients are also sped up by caching plugins, whereas normal options aren’t. Due to the nature of the expiration process, never assume that a transient is in the database when writing code.

The SQL query will run every two hours, and the actual data will be returned from the transient, making things much more efficient. I’ve included two parameters, <code>$size</code> and <code>$expires</code>, allowing you to control the number of posts returned and the expiration time for the transient.

One of the most powerful elements of this example is the use of <code>switch_to_blog()</code> and <code>restore_current_blog()</code>. These two Multisite functions enable us to temporarily switch to another website (by ID), gather information or content, and then switch back to the original website.

Add the following to your theme’s <em>functions.php</em> file:

<pre><code class="language-php">/**
 * Build a list of all websites in a network
 */
function wp_list_sites( $expires = 7200 ) {
   if( !is_multisite() ) return false;

   // Because the get_blog_list() function is currently flagged as deprecated 
   // due to the potential for high consumption of resources, we'll use
   // $wpdb to roll out our own SQL query instead. Because the query can be
   // memory-intensive, we'll store the results using the Transients API
   if ( false === ( $site_list = get_transient( 'multisite_site_list' ) ) ) {
      global $wpdb;
      $site_list = $wpdb-&gt;get_results( $wpdb-&gt;prepare('SELECT * FROM wp_blogs ORDER BY blog_id') );
      // Set the Transient cache to expire every two hours
      set_site_transient( 'multisite_site_list', $site_list, $expires );
   }

   $current_site_url = get_site_url( get_current_blog_id() );

   $html = 'blog_id . '"' . $class . '>[' . get_bloginfo('name') . '](' . home_url() . ')

           ' . "n"; restore_current_blog(); } $html .= '

           ' . "nn"; return $html; }</code></pre>

(<strong>Please note:</strong> The <code>get_blog_list()</code> function is currently <strong>deprecated</strong> due to the potential for a high consumption of resources if a network contains more than 1000 websites. Currently, there is no replacement function, which is why I have used a custom <code>$wpdb</code> query in its place. In future, WordPress developers will probably release a better alternative. I suggest <a href="https://codex.wordpress.org/WPMU_Functions/get_blog_list">checking for a replacement</a> before implementing this example on an actual network.)

This function first verifies that Multisite is enabled and, if it’s not, returns <code>false</code>. First, we gather a list of IDs of all websites in the network, sorting them in ascending order using our custom <code>$wpdb</code> query. Next, we iterate through each website in the list, using <code>switch_to_blog()</code> to check whether it is the current website, and adding the <code>.current-site-item</code> class if it is. Then, we use the name and link for that website to create a list item for our menu, returning to the original website using <code>restore_current_blog()</code>. When the loop is complete, we return the complete unordered list to be outputted in our theme. It’s that simple.

To use this in your theme, call the <code>wp_list_sites()</code> function where you want the network menu to be displayed. Because the function first checks for a Multisite-enabled installation, you should verify that the returned value is not <code>false</code> before displaying the corresponding HTML.

<pre><code class="language-php">&lt;?php
// Multisite Network Menu
$network_menu = wp_list_sites();
if( $network_menu ): 
?&gt;</code></pre>

<div>&lt;?php echo $network_menu; ?&gt;</div>
 &lt;?php endif; ?&gt;

### List Recent Posts Across an Entire Network

If the websites in your network share similar topics, you may want to create a list of the most recent posts across all websites. Unfortunately, WordPress does not have a built-in function to do this, but with a little help from the <a href="https://codex.wordpress.org/Class_Reference/wpdb"><code>$wpdb</code> database class</a>, you can create a custom database query of the latest posts across your network.

This SQL query also has the potential to become very large. For this reason, we’ll use the <a href="https://codex.wordpress.org/Transients_API">Transients API</a> again in a method very similar to what is used in the <code>wp_list_sites()</code> function.

Start by adding the <code>wp_recent_across_network()</code> function to your theme’s <em>functions.php</em> file.

<pre><code class="language-php">/**
 * List recent posts across a Multisite network
 *
 * @uses get_blog_list(), get_blog_permalink()
 *
 * @param int $size The number of results to retrieve
 * @param int $expires Seconds until the transient cache expires
 * @return object Contains the blog_id, post_id, post_date and post_title
 */
function wp_recent_across_network( $size = 10, $expires = 7200 ) {
   if( !is_multisite() ) return false;

   // Cache the results with the WordPress Transients API
   // Get any existing copy of our transient data
   if ( ( $recent_across_network = get_site_transient( 'recent_across_network' ) ) === false ) {

      // No transient found, regenerate the data and save a new transient
      // Prepare the SQL query with $wpdb
      global $wpdb;

      $base_prefix = $wpdb-&gt;get_blog_prefix(0);
      $base_prefix = str_replace( '1_', ’ , $base_prefix );

      // Because the get_blog_list() function is currently flagged as deprecated 
      // due to the potential for high consumption of resources, we'll use
      // $wpdb to roll out our own SQL query instead. Because the query can be
      // memory-intensive, we'll store the results using the Transients API
      if ( false === ( $site_list = get_site_transient( 'multisite_site_list' ) ) ) {
         global $wpdb;
         $site_list = $wpdb-&gt;get_results( $wpdb-&gt;prepare('SELECT * FROM wp_blogs ORDER BY blog_id') );
         set_site_transient( 'multisite_site_list', $site_list, $expires );
      }

      $limit = absint($size);

      // Merge the wp_posts results from all Multisite websites into a single result with MySQL "UNION"
      foreach ( $site_list as $site ) {
         if( $site == $site_list[0] ) {
            $posts_table = $base_prefix . "posts";
         } else {
            $posts_table = $base_prefix . $site-&gt;blog_id . "_posts";
         }

         $posts_table = esc_sql( $posts_table );
         $blogs_table = esc_sql( $base_prefix . 'blogs' );

         $query .= "(SELECT $posts_table.ID, $posts_table.post_title, $posts_table.post_date, $blogs_table.blog_id FROM $posts_table, $blogs_tablen";
         $query .= "tWHERE $posts_table.post_type = 'post'n";
         $query .= "tAND $posts_table.post_status = 'publish'n";
         $query .= "tAND $blogs_table.blog_id = {$site-&gt;blog_id})n";

         if( $site !== end($site_list) ) 
            $query .= "UNIONn";
         else
            $query .= "ORDER BY post_date DESC LIMIT 0, $limit";
      }

      // Sanitize and run the query
      $query = $wpdb-&gt;prepare($query);
      $recent_across_network = $wpdb-&gt;get_results( $query );

      // Set the Transients cache to expire every two hours
      set_site_transient( 'recent_across_network', $recent_across_network, 60*60*2 );
   }

   // Format the HTML output
   $html = '</code></pre>

*   <a>blog_id, $post->ID ) . '">' . $post->post_title . '</a>

'; } $html .= '

'; return $html; }

Using this function in your theme is simple. Be certain to check the <code>return</code> value before outputting HTML to avoid conflicts with non-Multisite installations.

<pre><code class="language-php">&lt;?php
// Display recent posts across the entire network
$recent_network_posts = wp_recent_across_network();
if( $recent_network_posts ):
?&gt;

<div class="recent-accross-network">&lt;?php echo $recent_network_posts; ?&gt;</div>
&lt;?php endif; ?&gt;</code></pre>

### Retrieve a Single Post from Another Website in the Network

In certain situations, you may find it useful to refer to a single page, post or post type from another website in your network. The <code>get_blog_post()</code> function makes this process simple.

For example, you may want to display <code>the_content()</code> from an “About” page on the primary website in your network.

<pre><code class="language-php">&lt;?php
// Display "About" page content from the network's primary website
$about_page = get_blog_post( 1, 317 );
if( $about_page ): 
?&gt;

</code></pre>

<div class="network-about entry">&lt;?php echo $about_page-&gt;post_content; ?&gt;</div>
&lt;?php endif; ?&gt;

Did you notice that the entire <code>$post</code> object is returned? In this example, we’ve used only <code>the_content()</code>, but far more information is available for other circumstances.</p>

### Set Up Global Variables Across a Network

Starting any WordPress project in a <a href="https://www.smashingmagazine.com/2011/09/28/developing-wordpress-locally-with-mamp/">solid local development environment</a> is always important. You might find it handy to have a global variable that determines whether a website is “live” or “staging.” In Multisite, you can achieve this using a network-activated plugin that contains the following handy function, assuming that your local host contains <code>localhost</code> in the URL:

<pre><code class="language-php">/**
 * Define network globals
 */
function ms_define_globals() {
   global $blog_id;
   $GLOBALS['staging'] = ( strstr( $_SERVER['SERVER_NAME'], 'localhost' ) ) ? true : false;
}
add_action( 'init', 'ms_define_globals', 1 );</code></pre>

When would you use this <code>$staging</code> variable? I use it to display development-related messages, notifications and information to improve my workflow.</p>

### Display the Page Request Information in a Local Environment

I use the <code>$staging</code> global variable to display the number of queries and page-request speed for every page across a network in my local environment.

<pre><code class="language-php">/**
 * Display page request info
 *
 * @requires $staging
 */
function wp_page_request_info() {
   global $staging;
   if ( $staging ): ?&gt;
      &lt;?php echo get_num_queries(); ?&gt; queries in &lt;?php timer_stop(1); ?&gt; seconds.
   &lt;?php endif;
}
add_action( 'wp_footer', 'wp_page_request_info', 1000 );</code></pre>

This is only one of many ways you can use the <code>ms_define_globals()</code> function. I’ve used it to define, find and replace URLs in the content delivery network, to detect mobile devices and user agents, and to filter local attachment URLs.</p>

## Conclusion

There is tremendous value in the simplicity of managing multiple websites in a single installation of WordPress. Leveraging WordPress Multisite is quickly becoming a requisite skill among WordPress developers. These techniques should provide a solid foundation for you to build on, so that you can be the next WordPress Multisite theme rock star!

### Other Resources

*   [Mastering WordPress Multisite](https://wpcandy.com/series-on/mastering-wordpress-multisite) series, WPCandy
*   “[Create a [Multisite] Network](https://codex.wordpress.org/Create_A_Network),” WordPress Codex
*   “[WordPress MultiSite Subdomains on MAMP](https://perishablepress.com/wordpress-multisite-subdomains-mamp/),” Perishable Press
*   “[Migrating Multiple Blogs Into WordPress 3.0 Multisite](https://codex.wordpress.org/Migrating_Multiple_Blogs_into_WordPress_3.0_Multisite),” WordPress Codex
*   [OpenView Venture Partners](https://openviewpartners.com/), a live example of a WordPress Multisite network
*   “[Transients, Caching and the Complexities of Multisite](https://www.slideshare.net/andrewnacin/wordpress-transients-caching-and-the-complexities-of-multisite),” The Otto and Nacin Show, WordCamp San Francisco 2011

{{< signature "al" >}}


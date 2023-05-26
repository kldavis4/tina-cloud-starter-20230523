---
title: How To Create A Custom Taxonomy In WordPress
slug: create-custom-taxonomies-wordpress
image: >-
  https://www.smashingmagazine.com/general/2013/11/26/176703-revision-287/attachment/wordpress-taxonomy-graphic/
date: 2012-01-04T15:51:55.000Z
author: kevin-leary
description: >-
  WordPress 3 introduced custom taxonomies as a core feature. The following release of 3.1 included many features to enhance the support for custom taxonomies.
categories:
  - WordPress
  - Tutorials
---
Better import and export handling, advanced queries with <code>tax_query</code>, hierarchical support, body classes and a bunch of wonderful functions to play with were all part of the package.

Let’s take an in-depth look at how to create your own custom taxonomies in WordPress, including a few advanced development examples that you can begin using in your WordPress themes and plugins today.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Customizing WordPress Archives For Categories, Tags And Other](https://www.smashingmagazine.com/2014/08/customizing-wordpress-archives-categories-terms-taxonomies/)
*   [Building An Advanced WordPress Search With WP_Query](https://www.smashingmagazine.com/2016/03/advanced-wordpress-search-with-wp_query/)
*   [Introducing Term Meta Data In WordPress And How To Use Them](https://www.smashingmagazine.com/2015/12/how-to-use-term-meta-data-in-wordpress/)
*   [<span class="headline">The Complete Guide To Custom Post Types</span>](https://www.smashingmagazine.com/2012/11/complete-guide-custom-post-types/)

## The Custom Taxonomy In WordPress

WordPress’ custom taxonomies make it possible to structure large amounts of content in a logical, well-organized way. In WordPress, <strong>categories</strong> are set up as a hierarchal taxonomy, and <strong>tags</strong> are set up as a multifaceted taxonomy.

{{% feature-panel %}}

Taxonomy content can be displayed in a theme using <a href="https://codex.wordpress.org/Template_Hierarchy#Custom_Taxonomies_display">taxonomy templates</a>. Within a template, there are ample ways to display your data with <a href="https://codex.wordpress.org/Function_Reference#Category.2C_Tag_and_Taxonomy_Functions">built-in taxonomy functions</a>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01d359a1-ec26-4ddf-804d-0021ce06fc95/wordpress-taxonomy-graphic.jpg" alt="custom taxonomy wordpress" width="550" height="300" />

### Built-In Taxonomies

WordPress offers four built-in taxonomies out of the box:

1.  Categories (hierarchal),
2.  Tags (multifaceted),
3.  Links (multifaceted),
4.  Navigation menu (hierarchal).</p>

### Custom Taxonomies

WordPress provides a new method of grouping content by allowing you to create your own custom taxonomies. The core developers have created the <code>register_taxonomy()</code> function to handle the heavy lifting for us. All you have to do is understand how to configure all of the settings to suit your needs.</p>

## A Practical Example: Content By Location

A business that operates in multiple locations could benefit from organizing its content by location to allow visitors to browse news in their locality. A large news organization could organize its content by world region (Africa, Asia, Europe, Latin America, Middle East, US &amp; Canada), as the <a href="https://www.bbc.co.uk/news/world/">BBC</a> does in its “World” section.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/513b64a8-d82c-442a-ba31-e417db4df540/bbc-location-taxonomy.jpg" alt="How the BBC uses a location taxonomy" width="550" height="270" />

### Create a Custom Taxonomy

In WordPress, you can create (or “register”) a new taxonomy by using the <code>register_taxonomy()</code> function. Each taxonomy option is <a href="https://codex.wordpress.org/Function_Reference/register_taxonomy">documented in detail in the WordPress Codex</a>.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a92231-ab47-4b46-987d-96045cf34a1b/wordpress-locations-post-taxonomy.jpg" alt="WordPress custom taxonomy: Posts by location" width="550" height="212" />

<pre><code class="language-php">/**
 * Add custom taxonomies
 *
 * Additional custom taxonomies can be defined here
 * https://codex.wordpress.org/Function_Reference/register_taxonomy
 */
function add_custom_taxonomies() {
  // Add new "Locations" taxonomy to Posts
  register_taxonomy('location', 'post', array(
    // Hierarchical taxonomy (like categories)
    'hierarchical' =&gt; true,
    // This array of options controls the labels displayed in the WordPress Admin UI
    'labels' =&gt; array(
      'name' =&gt; _x( 'Locations', 'taxonomy general name' ),
      'singular_name' =&gt; _x( 'Location', 'taxonomy singular name' ),
      'search_items' =&gt;  __( 'Search Locations' ),
      'all_items' =&gt; __( 'All Locations' ),
      'parent_item' =&gt; __( 'Parent Location' ),
      'parent_item_colon' =&gt; __( 'Parent Location:' ),
      'edit_item' =&gt; __( 'Edit Location' ),
      'update_item' =&gt; __( 'Update Location' ),
      'add_new_item' =&gt; __( 'Add New Location' ),
      'new_item_name' =&gt; __( 'New Location Name' ),
      'menu_name' =&gt; __( 'Locations' ),
    ),
    // Control the slugs used for this taxonomy
    'rewrite' =&gt; array(
      'slug' =&gt; 'locations', // This controls the base slug that will display before each term
      'with_front' =&gt; false, // Don't display the category base before "/locations/"
      'hierarchical' =&gt; true // This will allow URL's like "/locations/boston/cambridge/"
    ),
  ));
}
add_action( 'init', 'add_custom_taxonomies', 0 );</code></pre>

After adding this to your theme’s <code>functions.php</code> file, you should see a new taxonomy under the “Posts” menu in the admin sidebar. It works just like categories but is separate and independent.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a92983d3-706e-4041-9c59-a327cdfd37fb/wordpress-admin-locations-taxonomy-post-view.jpg" alt="WordPress custom taxonomy: Posts by location" width="550" height="176" />

After adding a few terms to your new taxonomy, you can begin to organize the content in your posts by location. A new “Locations” box will appear to the right of your posts in the WordPress admin area. Use this the way you would categories.

Let’s use this “location” taxonomy as a jumping-off point to learn more about working with taxonomy functions and content.</p>

### Create a Taxonomy Template for Your Theme

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e0d1a62-de2b-4f1a-bf3a-a6dbf8a28881/wordpress-taxonomy-theme-template-example.jpg" alt="Taxonomies: Bringing order to chaos in WordPress" width="419" height="348" />

When you add a custom taxonomy to a WordPress theme, you can display its content using one of <a href="https://codex.wordpress.org/Template_Hierarchy#Custom_Taxonomies_display">WordPress’ taxonomy theme templates</a>.

*   `taxonomy-{taxonomy}-{slug}.php` We could use this to create a theme template for a particular location, such as `taxonomy-location-boston.php` for the term “boston.”
*   `taxonomy-{taxonomy}.php` If the taxonomy were `location`, WordPress would look for `taxonomy-location.php`.
*   `taxonomy.php` This template is used for all custom taxonomies.
*   `archive.php` If no taxonomy-specific template is found, then the taxonomy that lists pages will use the archive template.
*   `index.php` If no other template is found, then this will be used.

Let’s use <code>taxonomy-location.php</code> to display our content. The template file could look something like this:

<pre><code class="language-php">&lt;?php
/**
 * Locations taxonomy archive
 */
get_header();
$term = get_term_by( 'slug', get_query_var( 'term' ), get_query_var( 'taxonomy' ) );
?&gt;
&lt;div class="wrapper"&gt;
  &lt;div class="primary-content"&gt;
    &lt;h1 class="archive-title"&gt;&lt;?php echo apply_filters( 'the_title', $term-&gt;name ); ?&gt; News&lt;/h1&gt;

    &lt;?php if ( !empty( $term-&gt;description ) ): ?&gt;
    &lt;div class="archive-description"&gt;
      &lt;?php echo esc_html($term-&gt;description); ?&gt;
    &lt;/div&gt;
    &lt;?php endif; ?&gt;

    &lt;?php if ( have_posts() ): while ( have_posts() ): the_post(); ?&gt;

    &lt;div id="post-&lt;?php the_ID(); ?&gt;" &lt;?php post_class('post clearfix'); ?&gt;&gt;
      &lt;h2 class="post-title"&gt;&lt;a href="&lt;?php the_permalink(); ?&gt;" rel="bookmark"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/h2&gt;
      &lt;div class="content clearfix"&gt;
        &lt;div class="post-info"&gt;
          &lt;p&gt;&lt;?php the_time(get_option('date_format')); ?&gt; by &lt;?php the_author_posts_link(); ?&gt;&lt;/p&gt;
        &lt;/div&gt;&lt;!--// end .post-info --&gt;
        &lt;div class="entry"&gt;
          &lt;?php the_content( __('Full story…') ); ?&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;&lt;!--// end #post-XX --&gt;

    &lt;?php endwhile; ?&gt;

    &lt;div class="navigation clearfix"&gt;
      &lt;div class="alignleft"&gt;&lt;?php next_posts_link('« Previous Entries') ?&gt;&lt;/div&gt;
      &lt;div class="alignright"&gt;&lt;?php previous_posts_link('Next Entries »') ?&gt;&lt;/div&gt;
    &lt;/div&gt;

    &lt;?php else: ?&gt;

    &lt;h2 class="post-title"&gt;No News in &lt;?php echo apply_filters( 'the_title', $term-&gt;name ); ?&gt;&lt;/h2&gt;
    &lt;div class="content clearfix"&gt;
      &lt;div class="entry"&gt;
        &lt;p&gt;It seems there isn't anything happening in &lt;strong&gt;&lt;?php echo apply_filters( 'the_title', $term-&gt;name ); ?&gt;&lt;/strong&gt; right now. Check back later, something is bound to happen soon.&lt;/p&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;?php endif; ?&gt;
  &lt;/div&gt;&lt;!--// end .primary-content --&gt;

  &lt;div class="secondary-content"&gt;
    &lt;?php get_sidebar(); ?&gt;
  &lt;/div&gt;&lt;!--// end .secondary-content --&gt;

&lt;?php get_footer(); ?&gt;</code></pre>

(Normally, we would <a href="https://codex.wordpress.org/Function_Reference/get_template_part">load a template part for the loop</a>, but for the sake of simplicity, I’ve skipped that step. As an alternative to <code>get_term_by()</code>, we could use <a href="https://codex.wordpress.org/Function_Reference/single_term_title"><code>single_term_title()</code></a> and <a href="https://codex.wordpress.org/Function_Reference/term_description"><code>term_description()</code></a> on this taxonomy archive template to display or retrieve the title and description of the taxonomy term.)

In this example, we’ve used a function called <code>get_term_by()</code> to retrieve all of the data associated with a taxonomy term in the form of an object. The object returned by the <a href="https://codex.wordpress.org/Function_Reference/get_term_by"><code>get_term_by()</code></a> function contains the following details about the term:

*   `ID` 325
*   `name` Boston
*   `slug` boston
*   `group` 0
*   `taxonomy` location
*   `taxonomy ID` 325
*   `description` If you need to know the latest news in Boston, then look no further.
*   `parent` 0 (or the ID)
*   `count` 1 (i.e. the number of posts with this term selected)

We’ve used this object, then, to display information about the current term <code>name</code> and <code>description</code> in the <code>taxonomy-location.php</code> template.</p>

### Using Taxonomy Conditionals

Conditional tags can be used in WordPress to determine what content is displayed on a particular page depending on the conditions met by the page. Taxonomy templates have their own set of conditionals:

*   `is_tax()` When any taxonomy archive page is being displayed.
*   `is_tax( 'location' )` When a taxonomy archive page for the “location” taxonomy is being displayed.
*   `is_tax( 'location', 'boston')` When the archive page for the “location” taxonomy with the slug of “boston” is being displayed.
*   `is_tax( 'location', array( 'boston', 'new-york', 'philadelphia' ) )` Returns `true` when the “location” taxonomy archive being displayed has a slug of either “boston,” “new-york” or “philadelphia.”
*   `taxonomy_exists()` When a particular taxonomy is registered via `register_taxonomy()`.</p>

## Working With Taxonomy Functions

Many functions for working with taxonomies are available in WordPress. Let’s go through a few commons examples of how to use them in practice.</p>

### Display a List of Taxonomy Terms

Most navigation systems begin with an unordered list. You can generate an unordered list of links to taxonomy archive pages using the <code>wp_list_categories()</code> function. This function is <a href="https://codex.wordpress.org/Template_Tags/wp_list_categories">very customizable</a> and can handle most of the scenarios that you’ll encounter as a theme developer.

<pre><code class="language-php">/**
 * Create an unordered list of links to active location archives
 */
$locations_list = wp_list_categories( array(
  'taxonomy' =&gt; 'location',
  'orderby' =&gt; 'name',
  'show_count' =&gt; 0,
  'pad_counts' =&gt; 0,
  'hierarchical' =&gt; 1,
  'echo' =&gt; 0,
  'title_li' =&gt; 'Locations'
) );

// Make sure there are terms with articles
if ( $locations_list )
  echo '&lt;ul class="locations-list"&gt;' . $locations_list . '&lt;/ul&gt;';</code></pre>

If you encounter a situation that requires a custom structure, I would recommend exploring the <a href="https://codex.wordpress.org/Function_Reference/Walker_Class">Walker class</a> or the <code>wp_get_object_terms()</code> function.</p>

### Create a Taxonomy Tag Cloud

A tag cloud provides a great way for users to browse content. The <code>wp_tag_cloud()</code> function makes creating a tag cloud with a custom taxonomy easy.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b99d5154-d8e1-4d0e-80a3-c97119fcd969/wordpress-taxonomy-term-cloud-example.jpg" alt="WordPress taxonomy term cloud example" width="347" height="189" />

Let’s use it to display a tag cloud of our location terms:

<pre><code class="language-php">// Locations tag cloud
&lt;?php
$locations_cloud = wp_tag_cloud( array(
  'taxonomy' =&gt; 'location',
  'echo' =&gt; 0
) );

// Make sure there are terms with articles
if ( $locations_cloud ): ?&gt;
&lt;h2&gt;News by Location&lt;/h2&gt;
&lt;div class="locations-cloud"&gt;
  &lt;?php echo $locations_cloud; ?&gt;
&lt;/div&gt;
&lt;?php endif; ?&gt;</code></pre>

### Get All Terms in a Taxonomy

You will often need to work with a full list of terms in a taxonomy, and the <code>get_terms()</code> function can be quite handy for this. Let’s use it to show off the number of locations to which we’re providing news:

<pre><code class="language-php">&lt;?php
// Get a list of all terms in a taxonomy
$terms = get_terms( "location", array(
  'hide_empty' =&gt; 0,
) );
$locations = array();
if ( count($terms) &gt; 0 ):
  foreach ( $terms as $term )
    $locations[] = $term-&gt;name;

  $locations_str = implode(', ', $locations);
?&gt;
&lt;h2&gt;Nationwide Coverage&lt;/h2&gt;
&lt;p&gt;We cover stories around the country in places like &lt;?php echo $locations_str; ?&gt; and more. If we're not the best source for the latest news in your area, let us know!&lt;/p&gt;
&lt;?php endif; ?&gt;</code></pre>

This will output the following HTML:

<pre><code class="language-php">&lt;h2&gt;Nationwide Coverage&lt;/h2&gt;
&lt;p&gt;We cover stories around the country in places like Boston, London, New York, San Francisco and more. If we're not the best source for the latest news in your area, let us know!&lt;/p&gt;</code></pre>

This simple approach may not show it, but the <a href="https://codex.wordpress.org/Function_Reference/get_terms"><code>get_terms()</code></a> function is incredibly powerful. It allows you to get terms from multiple taxonomies at once by passing an array that contains the names of your taxonomies as the first parameter.</p>

### Working With WP_Query and tax_query

The <a href="https://codex.wordpress.org/Class_Reference/WP_Query"><code>WP_Query</code> class</a> enables you to create a custom loop. WordPress 3.1 introduced a new parameter for the class called <a href="https://codex.wordpress.org/Class_Reference/WP_Query#Taxonomy_Parameters"><code>tax_query</code></a>, which allows you to display content from a taxonomy in many unique ways.

Let’s use it to create a list of the most recent news posts in Boston.

<pre><code class="language-php">&lt;?php
/**
 * Display a list of the most recent news in Boston
 *
 * @class WP_Query https://codex.wordpress.org/Class_Reference/WP_Query
 */
$locations_query = new WP_Query( array(
  'post_type' =&gt; 'post',
  'posts_per_page' =&gt; 10,
  'tax_query' =&gt; array(
    array(
      'taxonomy' =&gt; 'location',
      'field' =&gt; 'slug',
      'terms' =&gt; 'boston'
    )
  )
) );
// Display the custom loop
if ( $locations_query-&gt;have_posts() ): ?&gt;
&lt;h2&gt;Latest News in Boston&lt;/h2&gt;
&lt;ul class="postlist"&gt;
  &lt;?php while ( $locations_query-&gt;have_posts() ) : $locations_query-&gt;the_post(); ?&gt;
  &lt;li&gt;&lt;span class="date"&gt;&lt;?php the_time(get_option('date_format')); ?&gt;&lt;/span&gt; – &lt;a href="&lt;?php the_permalink(); ?&gt;" rel="bookmark"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/li&gt;
  &lt;?php endwhile; wp_reset_postdata(); ?&gt;
&lt;/ul&gt;&lt;!--// end .postlist --&gt;
&lt;?php endif; ?&gt;</code></pre>

We could easily make this set-up dynamic by using the <code>get_term_by()</code> or <code>get_terms()</code> functions that we discussed earlier.</p>

## Attaching Additional Data to a Taxonomy

Each taxonomy term has specific data associated with it. Out of the box, WordPress allows you to store the following information for each taxonomy term:

*   Name,
*   Slug,
*   Parent,
*   Description.

But what if you need to store more information, such as an image for the taxonomy term or a title and description for search engines, or maybe even attach the term to a particular author the way a traditional news column does? Since WordPress 2.9, developers have been able to attach additional meta data to posts, pages, custom post types, comments and users using the <code>add_metadata()</code>, <code>update_metadata()</code> and <code>get_metadata()</code> functions. But this does not include taxonomies such as tags and categories.

With the help of the <a href="https://wordpress.org/extend/plugins/taxonomy-metadata/">Taxonomy Metadata</a> plugin, we can attach meta data to taxonomy terms for both built-in and custom taxonomies. This enables us to create additional taxonomy fields that will be stored in a new <code>taxonomymeta</code> database table.

<strong>Note to Multisite developers:</strong> I’ve encountered issues using the Taxonomy Metadata plugin on a WordPress Multisite installation. Activating the plugin network-wide results in data not being saved. Instead, activate the plugin individually for each website, and it will work properly.

(Knowing the story behind this technique and what it might mean for future WordPress upgrades is important. Currently, there is a <a href="https://core.trac.wordpress.org/ticket/10142">debate on the WordPress Trac project</a> about the best method for this. The method I’ll show you is one suggested by various WordPress core developers. But I strongly urge you to review the Trac project and the Codex. A standard approach could very well be built into WordPress in the future, which would therefore be more practical than what I am about to show you.)

The <strong>prerequisite</strong> to all of the examples below is to install and activate the <a href="https://wordpress.org/extend/plugins/taxonomy-metadata/">Taxonomy Metadata</a> plugin.</p>

### Add Search Engine Title and Description Fields to Categories and Tags

We will use action hooks to gracefully attach additional fields to our taxonomies without editing WordPress’ core. If you’ve made it this far, then you probably have a working knowledge of WordPress filters and actions. To learn about working with hooks, I highly suggest <a href="https://www.smashingmagazine.com/2011/10/07/definitive-guide-wordpress-hooks/">Daniel Pataki’s article</a> on the subject.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3196ae56-9e9d-4cc5-8637-d2c202c043df/wordpress-taxonomy-custom-fields-example.jpg" alt="WordPress taxonomy meta data: Search engine title and description fields added to categories and tags" width="549" height="952" />

Let’s start by adding a text <code>input</code> and a <code>textarea</code> field to the “Add New” and “Edit” term pages on the <a href="https://codex.wordpress.org/Administration_Screens">WordPress admin screen</a>. We do this by placing the following functions in our theme or plugin.

<strong>The <code>taxonomy_metadata_add()</code> function attaches the fields to the <code>/wp-admin/edit-tags.php?taxonomy=%taxonomy%</code> page.</strong>
The <code>%taxonomy%</code> item in the URL above will change depending on the term you are editing.

<pre><code class="language-php">/**
 * Add additional fields to the taxonomy add view
 * e.g. /wp-admin/edit-tags.php?taxonomy=category
 */
function taxonomy_metadata_add( $tag ) {
  // Only allow users with capability to publish content if ( current_user_can( 'publish_posts' ) ): ?&gt;
  &lt;div class="form-field"&gt;
    &lt;label for="meta_title"&gt;&lt;?php _e('Search Engine Title'); ?&gt;&lt;/label&gt;
    &lt;input name="meta_title" id="meta_title" type="text" value="" size="40" /&gt;
    &lt;p class="description"&gt;&lt;?php _e('Title display in search engines is limited to 70 chars'); ?&gt;&lt;/p&gt;
  &lt;/div&gt;

  &lt;div class="form-field"&gt;
    &lt;label for="meta_description"&gt;&lt;?php _e('Search Engine Description'); ?&gt;&lt;/label&gt;
    &lt;textarea name="meta_description" id="meta_description" rows="5" cols="40"&gt;&lt;/textarea&gt;
    &lt;p class="description"&gt;&lt;?php _e('The meta description will be limited to 156 chars by search engines.'); ?&gt;&lt;/p&gt;
  &lt;/div&gt;
  &lt;?php endif;
}</code></pre>

<strong>The <code>taxonomy_metadata_edit()</code> function attaches the fields to the <code>/wp-admin/edit-tags.php?action=edit&amp;taxonomy=%taxonomy%&amp;tag_ID=%id%&amp;post_type=%post_type%</code> page.</strong>
The <code>%taxonomy%</code>, <code>%id%</code> and <code>%post_type%</code> items in the URL above will change depending on the term you are editing.

We’ll use the <code>get_metadata</code> function here to display any saved data that exists in the form.

<pre><code class="language-php">/**
 * Add additional fields to the taxonomy edit view
 * e.g. /wp-admin/edit-tags.php?action=edit&amp;taxonomy=category&amp;tag_ID=27&amp;post_type=post
 */
function taxonomy_metadata_edit( $tag ) {
  // Only allow users with capability to publish content if ( current_user_can( 'publish_posts' ) ): ?&gt;
  &lt;tr class="form-field"&gt;
    &lt;th scope="row" valign="top"&gt;
      &lt;label for="meta_title"&gt;&lt;?php _e('Search Engine Title'); ?&gt;&lt;/label&gt;
    &lt;/th&gt;
    &lt;td&gt;
      &lt;input name="meta_title" id="meta_title" type="text" value="&lt;?php echo get_term_meta($tag-&gt;term_id, 'meta_title', true); ?&gt;" size="40" /&gt;
      &lt;p class="description"&gt;&lt;?php _e('Title display in search engines is limited to 70 chars'); ?&gt;&lt;/p&gt;
    &lt;/td&gt;
  &lt;/tr&gt;

  &lt;tr class="form-field"&gt;
    &lt;th scope="row" valign="top"&gt;
      &lt;label for="meta_description"&gt;&lt;?php _e('Search Engine Description'); ?&gt;&lt;/label&gt;
    &lt;/th&gt;
    &lt;td&gt;
      &lt;textarea name="meta_description" id="meta_description" rows="5" cols="40"&gt;&lt;?php echo get_term_meta($tag-&gt;term_id, 'meta_description', true); ?&gt;&lt;/textarea&gt;
      &lt;p class="description"&gt;&lt;?php _e('Title display in search engines is limited to 70 chars'); ?&gt;&lt;/p&gt;
    &lt;/td&gt;
  &lt;/tr&gt;
  &lt;?php endif;
}</code></pre>

These two functions control the output of the form fields. I’ve used HTML that follows WordPress’ <a href="https://codex.wordpress.org/User:TECannon/UI_Pattern_and_Style_Guide">UI patterns and styles guidelines</a> for the admin area.

<strong>Saving the form’s data to the <code>taxonomymeta</code> database table</strong>
Now that we’ve added the form fields, we’ll need to process and save the data with the <code>update_term_meta</code> function that is provided by the plugin.

<pre><code class="language-php">/**
 * Save taxonomy metadata
 *
 * Currently the Taxonomy Metadata plugin is needed to add a few features to the WordPress core
 * that allow us to store this information into a new database table
 *
 *  https://wordpress.org/extend/plugins/taxonomy-metadata/
 */
function save_taxonomy_metadata( $term_id ) {
  if ( isset($_POST['meta_title']) )
    update_term_meta( $term_id, 'meta_title', esc_attr($_POST['meta_title']) );

  if ( isset($_POST['meta_description']) )
    update_term_meta( $term_id, 'meta_description', esc_attr($_POST['meta_description']) );
}</code></pre>

<strong>Add the new taxonomy fields</strong>
Now that everything is in place, we’ll use action hooks to load our new functions in all the right places. By hooking the following function into the <code>admin_init</code> action, we ensure that it runs only on the admin side of WordPress. First, we need to make sure that the functions added by the Taxonomy Metadata plugin are available. Next, we use the <code>get_taxonomies()</code> function to attach the new taxonomy fields to every public taxonomy, including the built-in tags and categories.

<pre><code class="language-php">/**
 * Add additional taxonomy fields to all public taxonomies
 */
function taxonomy_metadata_init() {
  // Require the Taxonomy Metadata plugin if( !function_exists('update_term_meta') || !function_exists('get_term_meta') ) return false;

  // Get a list of all public custom taxonomies
  $taxonomies = get_taxonomies( array(
    'public'   =&gt; true,
    '_builtin' =&gt; true
  ), 'names', 'and');

  // Attach additional fields onto all custom, public taxonomies if ( $taxonomies ) {
    foreach ( $taxonomies  as $taxonomy ) {
      // Add fields to "add" and "edit" term pages
      add_action("{$taxonomy}_add_form_fields", 'taxonomy_metadata_add', 10, 1);
      add_action("{$taxonomy}_edit_form_fields", 'taxonomy_metadata_edit', 10, 1);
      // Process and save the data
      add_action("created_{$taxonomy}", 'save_taxonomy_metadata', 10, 1);
      add_action("edited_{$taxonomy}", 'save_taxonomy_metadata', 10, 1);
    }
  }
}
add_action('admin_init', 'taxonomy_metadata_init');</code></pre>

That’s it. We’re done!

You should now see two additional fields in your tags, categories and public custom taxonomies. As mentioned at the beginning of this section, the technique can be used to handle many different scenarios. This basic framework for storing and retrieving information associated with a taxonomy should have you well on your way to mastering the management of taxonomy content.</p>

## In Conclusion

I hope you better understand how to organize WordPress content with the help of taxonomies. Whether hierarchal or multifaceted, a well-implemented taxonomy will simplify the way content is organized and displayed on a website. WordPress has all of the tools you need to create custom taxonomies and to group your content in new and exciting ways. How you use them is up to you!

### Additional Resources

*   [Custom taxonomy theme templates in WordPress](https://codex.wordpress.org/Template_Hierarchy#Custom_Taxonomies_display)
*   “[Custom Taxonomies in WordPress 2.8](https://justintadlock.com/archives/2009/05/06/custom-taxonomies-in-wordpress-28)”
*   “[A Refresher on Custom Taxonomies](https://justintadlock.com/archives/2010/06/10/a-refresher-on-custom-taxonomies)”
*   [Official documentation on `register_taxonomy()`](https://codex.wordpress.org/Function_Reference/register_taxonomy)
*   “[Introducing WordPress 3 Custom Taxonomies](https://net.tutsplus.com/tutorials/wordpress/introducing-wordpress-3-custom-taxonomies/)”
*   “[Adding Meta Data to Taxonomy Terms](https://www.wpmods.com/adding-metadata-taxonomy-terms/)”

{{< signature "al" >}}


---
title: 'Advanced Power Tips for WordPress Template Developers: Reloaded'
slug: advanced-power-tips-for-wordpress-template-developers-reloaded
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a810f00-691f-4fdf-a0e3-ffc4b40d76bb/tick-box-illu88.jpg
date: 2009-12-14T15:23:12.000Z
author: jacob-goldman
description: >-
  Two weeks ago we published the [first part of this
  article](https://www.smashingmagazine.com/2009/11/25/advanced-power-tips-for-wordpress-template-developers/),
  covering multiple column content techniques and associating pages with post
  content; we discussed how to use the "More"-tag, hide standalone categories
  from the category list and retain the page layout for post views within a
  category page. This article presents the second part of the article; it covers
  customizing basic content administration and adding features to the post and
  page editor in WordPress. You would like to see more similar articles in the
  future? Let us know in the comments to this post!
categories:
  - WordPress
  - PHP
  - Templates
  - Techniques (WP)
---
Two weeks ago we published the <a title="Advanced Power Tips For WordPress Template Developers" href="https://www.smashingmagazine.com/2009/11/25/advanced-power-tips-for-wordpress-template-developers/">first part of this article</a>, covering multiple column content techniques and associating pages with post content; we discussed how to use the "More"-tag, hide standalone categories from the category list and retain the page layout for post views within a category page. This article presents the second part of the article; it covers customizing basic content administration and adding features to the post and page editor in WordPress. You would like to see more similar articles in the future? Let us know in the comments to this post!

You may be interested in the following related posts:

*   [Custom Field Hacks for WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/)
*   [15 Useful Twitter Hacks and Plugins For WordPress](https://www.smashingmagazine.com/2009/11/2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [100 Amazing Free WordPress Themes For 2009](https://www.smashingmagazine.com/2009/11/2009/05/18/100-amazing-free-wordpress-themes-for-2009/)

## Customizing Basic Content Administration

Many template developers have learned the art of making beautiful, highly customized front end templates for WordPress. But the real wizards know how to tailor the WordPress administrative console to create a tailored, customized experience for content managers.

{{% feature-panel %}}

### Customizing the Dashboard Widgets

The dashboard is the first screen presented to registered visitors when they visit WordPress administration (/wp-admin). <strong>Tailoring the dashboard to a client can be the difference between a great first impression and a confused one</strong>, particularly if the theme customizes the administrative experience.

The dashboard is comprised of a number of widgets that can be repositioned and toggled using the “screen options” tab. WordPress has a hook – <em>wp_dashboard_setup</em> – that can be used to customize the dashboard widgets, as well as a function – <em>wp_add_dashboard_widget</em> – that allows developers to easily add new widgets.

The WordPress codex <a href="https://codex.wordpress.org/Dashboard_Widgets_API">documents the process of adding and removing widgets</a>.

Here is a practical use case based on that documentation: let’s remove all of the default widgets that don’t pertain to managing a typical site, and add one simple widget that welcomes the administrator and reminds them how to contact the developer for support.

<pre><code class="language-php">add_action('wp_dashboard_setup', 'my_custom_dashboard_widgets');

function my_custom_dashboard_widgets() {
   global $wp_meta_boxes;

   unset($wp_meta_boxes['dashboard']['normal']['core']['dashboard_plugins']);
   unset($wp_meta_boxes['dashboard']['side']['core']['dashboard_primary']);
   unset($wp_meta_boxes['dashboard']['side']['core']['dashboard_secondary']);

   wp_add_dashboard_widget('custom_help_widget', 'Help and Support', 'custom_dashboard_help');
}

function custom_dashboard_help() {
   echo '&lt;p&gt;Welcome to your custom theme! Need help? Contact the developer &lt;a href="https://mytemplates.com"&gt;here&lt;/a&gt;.&lt;/p&gt;';
}</code></pre>

<img loading="lazy" decoding="async" class="19154" title="Customized WordPress admin dashboard" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69126e49-9c15-4023-b9be-4419c2f2a906/wp-custom-dash.gif" alt="Customized WordPress admin dashboard" width="500" height="306" />

### Customizing the Contextual Help Dropdown

Throughout its administrative panel, WordPress has a small "Help" tab just below the administrative header. Clicking this tab rolls down contextual help for the current administrative page.

<img loading="lazy" decoding="async" class="19155" title="WordPress contextual administrative help" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8517b05-ca96-4c04-a150-2d251bbabf6e/wp-default-context-help.gif" alt="WordPress contextual administrative help" width="500" height="261" />

If your theme has some special functionality that might not be intuitive, it's a good practice to add some additional contextual help. For example purposes, let's assume that the theme has been customized to use the "more divider" to separate content into two columns, as described in the first tip. That’s probably not an obvious feature for your average content editor. To accomplish this, hook the contextual help text when on the "new page" and "edit page" administrative pages, and add a note about that feature.

<pre><code class="language-php">//hook loading of new page and edit page screens
add_action('load-page-new.php','add_custom_help_page');
add_action('load-page.php','add_custom_help_page');

function add_custom_help_page() {
   //the contextual help filter
   add_filter('contextual_help','custom_page_help');
}

function custom_page_help($help) {
   //keep the existing help copy
   echo $help;
   //add some new copy
   echo "&lt;h5&gt;Custom Features&lt;/h5&gt;";
   echo "&lt;p&gt;Content placed above the more divider will appear in column 1. Content placed below the divider will appear in column 2.&lt;/p&gt;";
}</code></pre>

<img loading="lazy" decoding="async" class="19156" title="Customized WordPress contextual administrative help" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/593c4333-627d-4ca4-9147-4ab6731e849a/wp-custom-context-help.gif" alt="Customized WordPress contextual administrative help" width="500" height="289" />

### Dropping in Your Own Logo

Providing the client some administrative branding can be quick and easy. Here's <strong>how to replace the default WordPress "W" logo in the administrative header with a custom alternative</strong>.

First, create an image that fits the allocated space. As of WordPress 2.8, the logo is a 30 pixels wide and 31 pixels tall transparent GIF. When using a transparent GIF or 8-bit PNG, ensure that the image matte matches the header background color: hex value 464646.

A logo named "custom_logo.gif" inside the template directory's image subfolder can substitute the default WordPress logo with the following code inside the theme's "functions.php" file.

<pre><code class="language-php">//hook the administrative header output
add_action('admin_head', 'my_custom_logo');

function my_custom_logo() {
   echo '
      &lt;style type="text/css"&gt;
         #header-logo { background-image: url('.get_bloginfo('template_directory').'/images/custom-logo.gif) !important; }
      &lt;/style&gt;
   ';
}</code></pre>

<img loading="lazy" decoding="async" class="19158" title="Customized logo in WordPress administration" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2d3bbb7-b776-4ab9-a7c9-41a25c8047b4/wp-custom-logo.gif" alt="Customized logo in WordPress administration" width="500" height="227" />

### Hiding Fields Based on User Role

Basic contributors might be confused or distracted by some of the boxes that surround the page or post editor, particularly if there are a handful of plug-ins that have added their own meta boxes. Alternatively, the content editor might simply want to keep author and contributor hands off of some special fields or features.

Let's say the content editor wants to keep authors and contributors way from the "custom fields" box. We can use the "remove_meta_box" function – regardless of user role – to remove that from all post editing screens like so:

<pre><code class="language-php">//hook the admin init
add_action('admin_init','customize_meta_boxes');

function customize_meta_boxes() {
     remove_meta_box('postcustom','post','normal');
}</code></pre>

The "remove_meta_box" function takes three parameters. The first is the ID of the box. The easiest way to discover the ID of the meta box is to look for the ID attribute of the corresponding DIV "postbox" in the source code. The second parameter determines which the context the function applies to: page, post, or link. Finally, the context attribute determines the position within its context: normal, or advanced (in most cases, just setting this to "normal" will work fine).

<img loading="lazy" decoding="async" class="19159" title="Finding a meta box ID using Firebug" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68592a3b-adc3-4584-aaa5-5d09a51204f9/wp-find-meta-id.gif" alt="Finding a meta box ID using Firebug" width="500" height="371" />

The next step is to extend the "customize_meta_boxes" function so that the "custom fields" box – ID "postcustom" – is only hidden from users with author role or lower. We’ll use <a href="https://codex.wordpress.org/Function_Reference/get_currentuserinfo"><em>get_currentuserinfo</em></a> to retrieve the user level. According to the WordPress codex, <a href="https://codex.wordpress.org/Roles_and_Capabilities#Author">authors represent level 2</a>.

<pre><code class="language-php">//hook the admin init
add_action('admin_init','customize_meta_boxes');

function customize_meta_boxes() {
     //retrieve current user info
     global $current_user;
     get_currentuserinfo();

     //if current user level is less than 3, remove the postcustom meta box
     if ($current_user-&gt;user_level &lt; 3)
          remove_meta_box('postcustom','post','normal');
}</code></pre>

## Adding Features to the Post & Page Editor

WordPress provides a "custom fields" box that makes it quick and easy to start adding new metadata to your pages and posts. For a tech-savvy client or low budget customization, this is a great, inexpensive method to start <a href="https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/">adding some unique fields for a custom implementation</a>.

<img loading="lazy" decoding="async" class="19114" title="Custom field with sidebar_content key" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36df9981-03d9-4812-93d8-6b1d248b9dfb/sidebar-custom-field.gif" alt="Custom field with sidebar_content key" width="500" height="236" />

But there are plenty of times when something more specialized than a generic "custom fields" box may be appropriate. A less savvy client may be confused by the generic fields that lack any documentation. A checkbox for a Boolean field may be more intuitive for a client than instructions to choose the custom field name from a drop down and type in “1” or “true” under the value. column Or maybe the field should be limited, in select box like fashion, to a few different choices.

<strong>The WordPress API can be used to add custom meta boxes to pages and / or posts. And with WordPress 2.8, adding new, tag-like taxonomies is a cinch.</strong>

### Adding a Custom Meta Box

Let's say a hyper-local journalist has hired us to build a news blog that covers politics in New York City. The journalist has a few writers on her team, none of whom are particularly tech-savvy, but they will all be set up as authors and posting their reports directly in WordPress. Our imaginary client wants each article associated with a single <a href="https://en.wikipedia.org/wiki/Borough_%28New_York_City%29">borough</a>, in addition to a "city-wide" option. Articles will never be associated with 2 boroughs, and the staff is prone to typos.

A developer accustomed to basic WordPress administrative customization would probably go to "categories" first. Make a "city-wide" category, with sub-categories for each borough. However, categories are multi-select, and there's no obvious way to prevent authors from selecting several. Furthermore, the client wants the borough named at the beginning of the article, and if categories are used in other ways (like news topics), extracting the borough name would be a bit tricky.

So how about a "custom field" for "borough"? The authors never remember to look in that generic custom fields box, and in their rush to meet deadlines, occassionally spell the borough wrong, breaking the “filter by borough” feature on the front end.

The right answer is a new custom "meta box," with a drop down "Borough" field. The WordPress Codex <a href="https://codex.wordpress.org/Function_Reference/add_meta_box">documents the "add_meta_box" function</a> in detail.

Let's apply the code discussed in the codex to this use case, assuming we want the "Borough" field to only appear on posts (not pages), and be shown on the top-right of the post editor page.

<pre><code class="language-php">/* Use the admin_menu action to define the custom boxes */
add_action('admin_menu', 'nyc_boroughs_add_custom_box');

/* Adds a custom section to the "side" of the post edit screen */
function nyc_boroughs_add_custom_box() {
     add_meta_box('nyc_boroughs', 'Applicable Borough', 'nyc_boroughs_custom_box', 'post', 'side', 'high');
}

/* prints the custom field in the new custom post section */
function nyc_boroughs_custom_box() {
     //get post meta value
     global $post;
     $custom = get_post_meta($post-&gt;ID,'_nyc_borough',true);

     // use nonce for verification
     echo '&lt;input type="hidden" name="nyc_boroughs_noncename" id="nyc_boroughs_noncename" value="'.wp_create_nonce('nyc-boroughs').'" /&gt;';

     // The actual fields for data entry
     echo '&lt;label for="nyc_borough"&gt;Borough&lt;/label&gt;';
     echo '&lt;select name="nyc_borough" id="nyc_borough" size="1"&gt;';

      //lets create an array of boroughs to loop through
      $boroughs = array('Manhattan','Brooklyn','Queens','The Bronx','Staten Island');
      foreach ($boroughs as $borough) {
            echo '&lt;option value="'.$borough.'"';
            if ($custom == $borough) echo ' selected="selected"';
            echo '&gt;'.$borough.'&lt;/option&gt;';
      }

     echo "&lt;/select&gt;";
}

/* use save_post action to handle data entered */
add_action('save_post', 'nyc_boroughs_save_postdata');

/* when the post is saved, save the custom data */
function nyc_boroughs_save_postdata($post_id) {
     // verify this with nonce because save_post can be triggered at other times
     if (!wp_verify_nonce($_POST['nyc_boroughs_noncename'], 'nyc-boroughs')) return $post_id;

     // do not save if this is an auto save routine
     if (defined('DOING_AUTOSAVE') &amp;&amp; DOING_AUTOSAVE) return $post_id;

     $nyc_borough = $_POST['nyc_borough'];
     update_post_meta($post_id, '_nyc_borough', $nyc_borough);
}</code></pre>

Take another look at the second to last line in that code block, where the post metadata is updated (update_post_meta will also add the meta if it does not exist). That function stores the field key and value (second and third parameters), assigned to the designated post (first parameter) in the same generic "way" that custom fields are stored. Notice that the field key name was prefaced with an underscore: "_nyc_borough". <strong>Meta fields with keys beginning with an underscore are not shown in the generic "custom fields" box.</strong> All other meta fields are shown in that box.

<img loading="lazy" decoding="async" class="19163" title="New borough custom field added to WordPress post editor screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73ebe8ea-b053-434f-94a2-2a85b1f6bf50/wp-borough-custom.gif" alt="New borough custom field added to WordPress post editor screen" width="500" height="217" />

We can use this field value in our template just as we would embed generic custom fields.

<pre><code class="language-php">echo get_post_meta($post-&gt;ID, '_nyc_borough', true);</code></pre>

If we want to do a post query that only includes posts in the “Queens” borough, we can execute the query with the following code:

<pre><code class="language-php">query_posts('meta_key=_nyc_borough&amp;meta_value=Queens');</code></pre>

### Adding Custom Taxonomies

A taxonomy, generically defined, is a "classification." Post tags and categories in WordPress are both types of taxonomies, one of which – categories – has a "hierarchical" proprietary: categories can have child and parent categories. The ability to define new taxonomies has actually been around in some basic form since WordPress 2.3 – but WordPress 2.8 ups the ante, making it incredibly easy for template developers to add and manage tag-like taxonomies.

At the core API level, taxonomies may be hierarchical (or not, a la “tags”) , associated with pages <em>or </em>posts, and have a few other more esoteric properties related to allowing post queries and permalink structures. The potential for custom taxonomies is considerable – posts could easily have two types of categories, pages could have multiple tags, and sites could have multiple tag clouds based on groupings more specific that a generic "tag."

While the architecture for all of this is all there, the real magic of custom taxonomies – introduced in 2.8 – has only been enabled for posts and non-hierarchical types. But if those qualifications aren't a show stopper, a developer can get a lot of value out of just a few lines of code: a new tag-like meta box added to posts, a new "posts menu" option for managing those values, and the ability to easily output clouds, filter by taxonomies, design taxonomy templates, and do just about anything one could do with generic "tags" on the front end.

The WordPress Codex outlines the <a href="https://codex.wordpress.org/Function_Reference/register_taxonomy">"register_taxonomy" function</a>.

Let's go back to that hyper-local New York City politics blog. Say the editor wants authors to be able to "tag" articles with a distinct "people" taxonomy, but still wants to retain generic tagging. The new "people" taxonomy will highlight the names of political leaders mentioned in articles. On the front end the editor envisions a "tag cloud" that will help the most active politicians get recognized (for better or worse!). Clicking on a leader’s name in the cloud should bring up a list of articles "tagged" with the given politician.

The following few lines of code will add the new "people" meta box to posts and add a new option to the "posts" menu where the taxonomy values can be managed.

<pre><code class="language-php">//hook into the init action to add the taxonomy
add_action( 'init', 'create_nyc_people_taxonomy');

//create nyc people taxonomy
function create_nyc_people_taxonomy() {
     register_taxonomy('people', 'post', array('hierarchical' =&gt; false, 'label' =&gt; 'people'));
}</code></pre>

<img loading="lazy" decoding="async" class="19166" title="New custom post taxonomy in WordPress - people" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cac9cb44-23f5-4e05-bb09-948c3881d37c/wp-people-taxonomy.gif" alt="New custom post taxonomy in WordPress - people" width="500" height="281" />

To output a cloud for this custom taxonomy highlighting the 40 most-tagged politicians, the generic "<a href="https://codex.wordpress.org/Template_Tags/wp_tag_cloud">wp_tag_cloud</a>" function can be used with a few parameters.

<pre><code class="language-php">wp_tag_cloud(array('taxonomy' =&gt; 'people', 'number' =&gt; 40));</code></pre>

To list the highlighted leaders in a single post:

<pre><code class="language-php">echo get_the_term_list($post-&gt;ID, 'people', 'People: ', ', ');</code></pre>

Clicking on a person's name will automatically take the visitor to an archive for that taxonomy. Custom template files can also be built for the custom taxonomy. A "taxonomy.php" template file in the theme folder can be used for all custom taxonomies. A "taxonomy-people.php" template file could be used for the “people” taxonomy in the example. As with all archives, if no taxonomy-specific template files are available, WordPress will fall back to the generic "archive" and "index" template files.</p>

### Further Reading on Custom Meta Boxes and Taxonomies

*   [Justin Tadlock on Custom Taxonomies in WordPress 2.8](https://justintadlock.com/archives/2009/05/06/custom-taxonomies-in-wordpress-28)
*   [Shiba combines meta box and custom taxonomy capabilities in a tutorial](https://www.shibashake.com/wordpress-theme/wordpress-custom-taxonomy-input-panels)


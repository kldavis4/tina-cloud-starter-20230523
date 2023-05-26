---
title: How To Use Custom Post Types To Organize Online Marketing Campaigns
slug: how-to-use-custom-post-types-to-organize-online-marketing-campaigns
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff4d6c29-2a0b-4f4a-accf-da6149e6c725/writing-code-illu22.jpg
date: 2012-02-03T14:59:01.000Z
author: joshua-dodson
description: >-
  [Custom post types](https://www.smashingmagazine.com/2012/11/complete-guide-custom-post-types/) add a level of flexibility to WordPress that makes this open-source Web development platform more useful on many levels. Whenever I have been faced with a Web-based task, especially one that involves organizing information, the first thing I do is examine WordPress to determine if it can handle the job. It usually can.
categories:
  - WordPress
  - Techniques
  - Plugins
---
As an Internet marketer and analyst, I need to be able to organize online marketing campaigns in a way that is trackable in Google Analytics. This is the perfect task for WordPress custom post types.

In this article, we’ll explain how to create a WordPress plugin that enables you to organize Internet marketing campaigns using trackable URLs, shortened versions of those URLs, and trackable QR codes that you can also use for offline marketing activities.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Extending WordPress With Custom Content Types](https://www.smashingmagazine.com/2015/04/extending-wordpress-custom-content-types/)
*   [A Detailed Guide To WordPress Custom Page Templates](https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/)
*   [Customizing WordPress Archives For Categories, Tags](https://www.smashingmagazine.com/2014/08/customizing-wordpress-archives-categories-terms-taxonomies/)
*   [Building A Custom Archive Page For WordPress](https://www.smashingmagazine.com/2015/04/building-custom-wordpress-archive-page/)

{{% feature-panel %}}

We’ll show you how to create this plugin in a way that maximizes ease of use and functionality. If you have other methods that you have found useful, please share them in the comments. Also, let’s remember that we are standing on the shoulders of WordPress developers who have laid the foundation for easier coding.

Here are the criteria for our custom post type plugin:

*   It must provide a form in which users can specify a landing page to be tracked, the anchor text or content, the term (if this link is a PPC ad), and any additional information about this link.
*   It must provide three custom taxonomy types, so that users can select the URL variables for source, medium and campaign name. This is a taxonomy type because they will be reusable across campaigns and posts.
*   It must be organizable in the admin area and be displayed in the user interface.
*   The output must include a Google Analytics campaign-trackable URL, the information about the URL in human-readable format, a shortened version of the URL using a URL shortener, and a QR code of the shortened URL.</p>

## The File Structure

This plugin will use three files. To set up the structure, create a plugin folder named <code>campaign-tracker</code>. Inside the <code>campaign-tracker</code> folder, create the following three PHP files:

*   `campaign-tracker.php`
*   `ga-functions.php`
*   `campaign-template.php`

After you have created the files, we are ready to start adding the code.</p>

## The Plugin File

The main plugin file will be <code>campaign-tracker.php</code>. The content of this file will begin the standard way, by providing WordPress with the information that it needs to recognize it is as plugin. We then dive into setting up the <code>CampaignTracker10</code> class and functions. We will set up our campaign custom post type and register the taxonomies that we will need. We will also initiate our admin interface.

<pre><code class="language-php">&lt;?php
   /*
   Plugin Name: Campaign Tracking 1.0
   Plugin URI: https://www.convergeconsulting.org
   description: >-
   Google Analytics Campaign Tracking system for WordPress 3.0 and above.
   Author: Joshua Dodson
   Version: 1.0
   Author URI: https://www.convergeconsulting.org
   */

   // Include the ga-functions.php helper functions
   include_once('ga-functions.php');

   if(!class_exists('CampaignTracker10'))
   {

      class CampaignTracker10 {

         var $meta_fields = array("gaca10-gaurl","gaca10-gaterm","gaca10-gacontent","gaca10-gadescription");

         // This function will create the custom post type. Thanks to Konstantin Kovshenin's example for additional examples of how to construct custom post types (https://kovshenin.com/2010/03/custom-post-types-in-wordpress-3-0-2089/), which inspired much of this.
         function __construct(){
            // Register custom post types
            register_post_type('campaign', array(
            'label' =&gt; _x('Campaigns','campaigns label'), // We're labeling the custom posts as Campaigns and also accounting for <a title="Disambiguation by context" href="https://codex.wordpress.org/I18n_for_WordPress_Developers#Disambiguation_by_context">gettext</a> appropriately
            'singular_label' =&gt; _x('Campaign','campaign singular label'), // Each post will be called a Campaign
            'public' =&gt; true, // These will be public
            'show_ui' =&gt; true, // Show the UI in admin panel
            '_builtin' =&gt; false, // This is a custom post type, not a built in post type
            '_edit_link' =&gt; 'post.php?post=%d',
            'capability_type' =&gt; 'post',
            'hierarchical' =&gt; false,
            'rewrite' =&gt; array("slug" =&gt; "campaign"), // This is for the permalinks
            'query_var' =&gt; "campaign", // This goes to the WP_Query schema
            'supports' =&gt; array('title'/* We only need the default title field, but we could use others such as 'author', 'excerpt', 'editor' ,'custom-fields'*/)
            ));

            add_filter("manage_edit-campaign_columns", array(&amp;$this, "edit_columns"));
            add_action("manage_posts_custom_column", array(&amp;$this, "custom_columns"));

            // Register custom taxonomies gasource (for the Campaign Source), gamedium (for the Campaign Medium), and ganame (for Campaign Name)
            // Campaign Source
            register_taxonomy("gasource", array("campaign"), array("hierarchical" =&gt; true, "label" =&gt; _x( 'Campaign Sources', 'campaign sources taxonomy label' ), "singular_label" =&gt; "Campaign Source", "rewrite" =&gt; true));
            // Campaign Medium
            register_taxonomy("gamedium", array("campaign"), array("hierarchical" =&gt; true, "label" =&gt; _x( 'Campaign Mediums', 'campaign mediums taxonomy label' ), "singular_label" =&gt; "Campaign Medium", "rewrite" =&gt; true));
            // Campaign Name
            register_taxonomy("ganame", array("campaign"), array("hierarchical" =&gt; true, "label" =&gt; _x( 'Campaign Names', 'campaign names taxonomy label' ), "singular_label" =&gt; "Campaign Name", "rewrite" =&gt; true));

            add_action("admin_init", array(&amp;$this, "admin_init"));
            add_action("template_redirect", array(&amp;$this, 'template_redirect'));

            add_action("wp_insert_post", array(&amp;$this, "wp_insert_post"), 10, 2);

         }</code></pre>

Let’s give the columns on the admin screen some headings:

<pre><code class="language-php">function edit_columns($columns)
   {
      $columns = array(
      'cb' =&gt; '&lt;input type="checkbox" /&gt;',
      'title' =&gt; _x('Campaign Title','campaign title label for edit columns'),
      'gaca10_ganame' =&gt; _x('Campaign Name','campaign name label for edit columns'),
      'gaca10_gasources' =&gt; _x('Campaign Source','campaign source label for edit columns'),
      'gaca10_gasmedium' =&gt; _x('Campaign Medium','campaign medium label for edit columns'),
      );
      return $columns;
   }</code></pre>

Let’s specify which columns we would like to show up on the admin screen for this custom post type. We’ll have columns for campaign source, medium and name, in addition to the post’s title.

<pre><code class="language-php">function custom_columns($column)
   {
      global $post;
      switch ($column)
      {
         // The campaign source
         case "gaca10_gasources":
         $gasources = get_the_terms(0, "gasource");
         if ( $gasources &amp;&amp; ! is_wp_error( $gasources ) ) :
         $gasources_html = array();
         foreach ($gasources as $gasource)
         array_push($gasources_html, '&lt;a href="' . get_term_link($gasource-&gt;slug, "gasource") . '"&gt;' . $gasource-&gt;name . '&lt;/a&gt;');

         echo implode($gasources_html, ", ");
         endif;
         break;

         // The campaign medium
         case "gaca10_gasmedium":
         $gamediums = get_the_terms(0, "gamedium");
         if ( $gamediums &amp;&amp; ! is_wp_error( $gamediums ) ) :
         $gamediums_html = array();
         foreach ($gamediums as $gamedium)
         array_push($gamediums_html, '&lt;a href="' . get_term_link($gamedium-&gt;slug, "gamedium") . '"&gt;' . $gamedium-&gt;name . '&lt;/a&gt;');

         echo implode($gamediums_html, ", ");
         endif;
         break;

         // The campaign name
         case "gaca10_ganame":
         $ganames = get_the_terms(0, "ganame");
         if ( $ganames &amp;&amp; ! is_wp_error( $ganames ) ) :
         $ganames_html = array();
         foreach ($ganames as $ganame)
         array_push($ganames_html, '&lt;a href="' . get_term_link($ganame-&gt;slug, "ganame") . '"&gt;' . $ganame-&gt;name . '&lt;/a&gt;');

         echo implode($ganames_html, ", ");
         endif;
         break;
      }
   }</code></pre>

Once our columns are set up appropriately, we should see the following columns (note that this example is with one campaign already added):

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03370c5b-277b-4ef7-a4b9-34e9216fcc1d/campaigns-in-columns.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/304d6182-9d9b-44f7-8d8f-458b0856ac2f/campaigns-in-columns-500.jpg" alt="Campaigns in columns" width="500" height="213" /></a>

The next section enables us to specify which template we would like to use to display this custom post type. We will be using the <code>campaign-template.php</code> template:

<pre><code class="language-php">function template_redirect()
   {
      global $wp;

      // If the post type is set and is campaign…
      if (isset($wp-&gt;query_vars["post_type"])) {
         if ($wp-&gt;query_vars["post_type"] == "campaign")
         {
            // Then use the campaign-template.php file from this plugin directory
            include WP_PLUGIN_DIR.'/campaign-tracker/campaign-template.php';
            die();
         }
      }
   }</code></pre>

If a post is inserted or updated, then loop through the array and update or add the post’s meta data.

<pre><code class="language-php">function wp_insert_post($post_id, $post = null)
   {
      if ($post-&gt;post_type == "campaign")
      {
         foreach ($this-&gt;meta_fields as $key)
         {
            $value = $_POST[$key];
            if (empty($value))
            {
               delete_post_meta($post_id, $key);
               continue;
            }

            if (!is_array($value))
            {
               if (!update_post_meta($post_id, $key, $value))
               {
                  add_post_meta($post_id, $key, $value);
               }
            }
            else
            {
               delete_post_meta($post_id, $key);

               foreach ($value as $entry){
                  add_post_meta($post_id, $key, $entry);
               }
            }
         }
      }
   }</code></pre>

With the following function, we can add custom meta boxes for the admin screen where we edit the campaign:

<pre><code class="language-php">function admin_init()
   {
      // Add custom meta boxes for the edit campaign screen
      add_meta_box("gaca10-meta", "Campaign Information", array(&amp;$this, "meta_options"), "campaign", "normal", "core");
   }</code></pre>

The following function is for the admin post meta contents. This lets us create the form in which we specify some of the variables for our trackable URL (except for the taxonomies). It also provides a read-only field that shows the shortened URL after the URL variables have been saved.

<pre><code class="language-php">function meta_options()
   {
      global $post;
      $custom = get_post_custom($post-&gt;ID);
      if($custom["gaca10-gaurl"][0]){
         $gaurl = $custom["gaca10-gaurl"][0];
      }
      else{ $gaurl = ’; }
      if($custom["gaca10-gaterm"][0]) {
         $gaterm = $custom["gaca10-gaterm"][0];
      }
      else { $gaterm = ’; }
      if ($custom["gaca10-gacontent"][0]) {
         $gacontent = $custom["gaca10-gacontent"][0];
      }
      else { $gacontent = ’; }
      if ($custom["gaca10-gadescription"][0]) {
         $gadescription = $custom["gaca10-gadescription"][0];
      }
      else { $gadescription = ’; }

      $url = trackable_url();
      if ($custom["campaign_tinyurl"][0]) {
         if($gaurl == ’) { $shortenedurl = ’; }
         else{ $shortenedurl = create_tiny_url($url); }
      }

      ?&gt;
      &lt;label&gt;&lt;?php _ex('Website URL:','website url label'); ?&gt;&lt;/label&gt;&lt;input name="gaca10-gaurl" value="&lt;?php echo $gaurl; ?&gt;" /&gt;&lt;br /&gt;
      &lt;em&gt;&lt;?php _ex('(e.g., https://www.google.com)','website url example'); ?&gt;&lt;/em&gt;&lt;br /&gt;&lt;br /&gt;

      &lt;label&gt;&lt;?php _ex('Campaign Term:','campaign term label'); ?&gt;&lt;/label&gt;&lt;input name="gaca10-gaterm" value="&lt;?php echo $gaterm; ?&gt;" /&gt;&lt;br /&gt;
      &lt;em&gt;&lt;?php _ex('(identify the paid keywords)','campaign term information'); ?&gt;&lt;/em&gt;&lt;br /&gt;&lt;br /&gt;
      &lt;label&gt;&lt;?php _ex('Campaign Content:','campaign content label'); ?&gt;&lt;/label&gt;&lt;input name="gaca10-gacontent" value="&lt;?php echo $gacontent; ?&gt;" /&gt;&lt;br /&gt;
      &lt;em&gt;&lt;?php _ex('(use to differentiate ads)','campaign content information'); ?&gt;&lt;/em&gt;&lt;br /&gt;&lt;br /&gt;

      &lt;label&gt;&lt;?php _ex('Campaign Description:','campaign description label'); ?&gt;&lt;/label&gt;&lt;input name="gaca10-gadescription" value="&lt;?php echo $gadescription; ?&gt;" /&gt;&lt;br /&gt;
      &lt;em&gt;&lt;?php _ex('(use to remind yourself about this specific link)','campaign description information'); ?&gt;&lt;/em&gt;&lt;br /&gt;&lt;br /&gt;

      &lt;label&gt;&lt;?php _ex('Shortened URL:','shortened URL label'); ?&gt;&lt;/label&gt;&lt;input name="gaca10-gashortened-url" value="&lt;?php echo $shortenedurl; ?&gt;" readonly="readonly" /&gt;&lt;br /&gt;

      &lt;?php
   }
}

}</code></pre>

Here is how the “Add/Edit Campaign” screen will appear:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b965c8d-7494-45ce-b15a-71aa8e35ba7c/add-new-post.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99a3eb12-e42f-4922-b676-85b60c09c714/add-new-post-500.jpg" alt="Add new post" width="500" height="263" /></a>

If <code>CampaignTracker10</code> exists, then we initiate the plugin:

<pre><code class="language-php">if(class_exists('CampaignTracker10')){

      // Initiate the plugin
      add_action("init", "CampaignTracker10Init");

      function CampaignTracker10Init() {
         global $gaca10;
         $gaca10 = new CampaignTracker10();

      }
   }</code></pre>

Combine these functions into the <code>campaign-tracker.php</code> file.

The following taxonomy examples should also be on the “Add/Edit Campaign” screen after everything has been added. Here is the “Campaign Names” taxonomy:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb294624-dcb1-4f32-8935-35a59765adb2/campaign-names.png" alt="Campaign Names" width="291" />

Here is the “Campaign Mediums” taxonomy:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7871ffba-036f-43ac-8030-157ddd1ad357/campaign-mediums.png" alt="Campaign Mediums" width="287" />

Here is the “Campaign Sources” taxonomy:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a2f93a3-b3ed-4ae1-9859-e6e7c542d140/campaign-sources.png" alt="Campaign Sources" width="288" />

Similar to how traditional post categories are set up, you can create new categories or select previous categories.

<strong>A note on usage:</strong> When you begin to use the system, try to select only one category each from name, source and medium. One category per taxonomy type will prove to be most useful in your actual analysis in Google Analytics. So, as a general rule: one name, one source and one medium per URL.

## The Helpful Display Functions

Each of the functions in this section is part of the <code>ga-functions.php</code> file. The functions have been separated from the other functions in order to keep the display functions together.

Our file will begin with the <code>formatted_utm_taxonomy_terms</code> function, which will display a URL-friendly version of the taxonomy terms:

<pre><code class="language-php">&lt;?php
   /* Some Helpful Display Functions */

   function formatted_utm_taxonomy_terms($the_term) {
      global $post;
      $post_terms = get_the_terms( $post-&gt;ID, $the_term );
      if ( $post_terms &amp;&amp; ! is_wp_error( $post_terms ) ) :
      $encoded_terms = array();
      foreach ($post_terms as $term ) {
         if(!$encoded_terms[] = $term-&gt;slug){
            $encoded_terms[] = urlencode($term-&gt;name);
         }
      }
      $return_terms = implode('+',$encoded_terms);
      return $return_terms;
      endif;
   }</code></pre>

The <code>trackable_url</code> function generates the trackable URL from the fields on the admin screen as well as the taxonomies. This appends the appropriate tracking criteria to the URL so that Google Analytics can use the variables and provide information based on these specific variables. To do this, we will use the <a title="add_query_arg" href="https://codex.wordpress.org/Function_Reference/add_query_arg"><code>add_query_arg</code></a> WordPress function.

<pre><code class="language-php">function trackable_url() {
      global $post;
      $custom = get_post_custom($post-&gt;ID);

      // the url
      if ($custom["gaca10-gaurl"][0]) {
         $gaurl = $custom["gaca10-gaurl"][0];
      }
      else { $gaurl = ’; }

      // the term(s)
      if ($gaterm = $custom["gaca10-gaterm"][0]) {
         $gaterm = $custom["gaca10-gaterm"][0];
         $gaterm = urlencode($gaterm);
      }
      else { $gaterm = ’; }

      // the content(s)
      if ($custom["gaca10-gacontent"][0]) {
         $gacontent = $custom["gaca10-gacontent"][0];
         $gacontent = urlencode($gacontent);
      }
      else { $gacontent = ’; }
      $arr_params = array ( 'utm_campaign' =&gt; formatted_utm_taxonomy_terms('ganame'), 'utm_source' =&gt; formatted_utm_taxonomy_terms('gasource'), 'utm_medium' =&gt; formatted_utm_taxonomy_terms('gamedium'), 'utm_term' =&gt; $gaterm, 'utm_content' =&gt; $gacontent);
      return add_query_arg( $arr_params, $gaurl );

   }</code></pre>

The following functions take the campaign-trackable URL and <a href="https://www.richardcastera.com/blog/creating-a-tinyurl-with-tinyurl-api">shortens it with TinyURL</a>. This method uses <a title="wp_remote_get" href="https://codex.wordpress.org/Function_API/wp_remote_get"><code>wp_remote_get</code></a> to generate the shortened URL. It then saves the shortened URL to the post’s meta data when a post is saved. The <code>trackable_url_tiny</code> function enables us to retrieve the shortened URL in the template.

<pre><code class="language-php">// Save the shortened trackable URL to the post meta
   function save_shortened_meta($post_ID) {
      $url = trackable_url();
      $shortened_url = create_tiny_url($url);
      update_post_meta($post_ID, "campaign_tinyurl", $shortened_url);
      return $post_ID;
   }

   // Add an action to save it when the post is saved.
   add_action('save_post', 'save_shortened_meta');

   // Retrieve the shortened URL from post meta
   function trackable_url_tiny($url = null, $post_ID) {
      global $post;
      $custom_fields = get_post_custom($post-&gt;ID);
      $campaign_tinyurl = $custom_fields['campaign_tinyurl'][0];
      return $campaign_tinyurl;

      return $post_ID;
   }

   // Create shortened trackable URL through the wp_remote_get function
   function create_tiny_url($strURL) {
      $tinyurl = wp_remote_get( 'https://tinyurl.com/api-create.php?url='.$strURL );
      if( is_wp_error( $response ) ) {
         return 'Something went wrong!';
      } else {
         return $tinyurl['body'];

      }
   }</code></pre>

The <code>trackable_url_report</code> function is what provides the human-readable version of the variables. These are broken out by each section. The landing page, campaign name, source, medium, terms and content are all separated and displayed individually if they exist.

<pre><code class="language-php">function trackable_url_report() {
      global $post;
      $custom = get_post_custom($post-&gt;ID);

      // get the url
      if ($custom["gaca10-gaurl"][0]) {
         $gaurl = $custom["gaca10-gaurl"][0];
      }
      else { $gaurl = ’; }
      // get the term(s)
      if ($gaterm = $custom["gaca10-gaterm"][0]) {
         $gaterm = $custom["gaca10-gaterm"][0];
      }
      else { $gaterm = ’; }

      // get the content(s)
      if ($custom["gaca10-gacontent"][0]) {
         $gacontent = $custom["gaca10-gacontent"][0];
      }
      else { $gacontent = ’; }

      // The Landing page
      $url_info =’;
      $url_info.= "&lt;strong&gt;". _x( 'Landing Page:','landing page label') . "&lt;/strong&gt; ";
      $url_info.= $gaurl;
      $url_info.= "&lt;br /&gt;";

      // The campaign name
      $url_info.= "&lt;strong&gt;". _x( 'Campaign:','campaign label') . "&lt;/strong&gt; ";
      $url_info.= formatted_utm_taxonomy_terms('ganame');
      $url_info.= "&lt;br /&gt;";

      // The Source
      $url_info.= "&lt;strong&gt;". _x( 'Source:','source label') . "&lt;/strong&gt; ";
      $url_info.= formatted_utm_taxonomy_terms('gasource');
      $url_info.= "&lt;br /&gt;";

      // The medium
      $url_info.= "&lt;strong&gt;". _x( 'Medium:','medium label') . "&lt;/strong&gt; ";
      $url_info.= formatted_utm_taxonomy_terms('gamedium');
      $url_info.= "&lt;br /&gt;";

      // The term
      $url_info.= "&lt;strong&gt;". _x( 'Term:','term label') . "&lt;/strong&gt; ";
      $url_info.= $gaterm;
      $url_info.= "&lt;br /&gt;";

      // The content
      $url_info.= "&lt;strong&gt;". _x( 'Content:','content label') . "&lt;/strong&gt; ";
      $url_info.= $gacontent;
      $url_info.= "&lt;br /&gt;";

      return $url_info;
   }</code></pre>

The <code>display_description</code> function displays the description of the URL. We’ve broken this part out here in order to keep all of the pieces that are specific to the URL together. This is also the last function in the <code>ga-functions.php</code> file.

      &lt;label&gt;&lt;?php _ex('Campaign Description:','campaign description label'); ?&gt;&lt;/label&gt;&lt;input name="gaca10-gadescription" value="&lt;?php echo $gadescription; ?&gt;" /&gt;&lt;br /&gt;
      &lt;em&gt;&lt;?php _ex('(use to remind yourself about this specific link)','campaign description information'); ?&gt;&lt;/em&gt;&lt;br /&gt;&lt;br /&gt;

      &lt;label&gt;&lt;?php _ex('Shortened URL:','shortened URL label'); ?&gt;&lt;/label&gt;&lt;input name="gaca10-gashortened-url" value="&lt;?php echo $shortenedurl; ?&gt;" readonly="readonly" /&gt;&lt;br /&gt;

      &lt;?php
   }
}

}</code></pre>

Here is how the “Add/Edit Campaign” screen will appear:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b965c8d-7494-45ce-b15a-71aa8e35ba7c/add-new-post.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99a3eb12-e42f-4922-b676-85b60c09c714/add-new-post-500.jpg" alt="Add new post" width="500" height="263" /></a>

If <code>CampaignTracker10</code> exists, then we initiate the plugin:

<pre><code class="language-php">if(class_exists('CampaignTracker10')){

      // Initiate the plugin
      add_action("init", "CampaignTracker10Init");

      function CampaignTracker10Init() {
         global $gaca10;
         $gaca10 = new CampaignTracker10();

      }
   }</code></pre>

Combine these functions into the <code>campaign-tracker.php</code> file.

The following taxonomy examples should also be on the “Add/Edit Campaign” screen after everything has been added. Here is the “Campaign Names” taxonomy:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb294624-dcb1-4f32-8935-35a59765adb2/campaign-names.png" alt="Campaign Names" width="291" />

Here is the “Campaign Mediums” taxonomy:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7871ffba-036f-43ac-8030-157ddd1ad357/campaign-mediums.png" alt="Campaign Mediums" width="287" />

Here is the “Campaign Sources” taxonomy:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a2f93a3-b3ed-4ae1-9859-e6e7c542d140/campaign-sources.png" alt="Campaign Sources" width="288" />

Similar to how traditional post categories are set up, you can create new categories or select previous categories.

<strong>A note on usage:</strong> When you begin to use the system, try to select only one category each from name, source and medium. One category per taxonomy type will prove to be most useful in your actual analysis in Google Analytics. So, as a general rule: one name, one source and one medium per URL.</p>

## The Helpful Display Functions

Each of the functions in this section is part of the <code>ga-functions.php</code> file. The functions have been separated from the other functions in order to keep the display functions together.

Our file will begin with the <code>formatted_utm_taxonomy_terms</code> function, which will display a URL-friendly version of the taxonomy terms:

<pre><code class="language-php">&lt;?php
   /* Some Helpful Display Functions */

   function formatted_utm_taxonomy_terms($the_term) {
      global $post;
      $post_terms = get_the_terms( $post-&gt;ID, $the_term );
      if ( $post_terms &amp;&amp; ! is_wp_error( $post_terms ) ) :
      $encoded_terms = array();
      foreach ($post_terms as $term ) {
         if(!$encoded_terms[] = $term-&gt;slug){
            $encoded_terms[] = urlencode($term-&gt;name);
         }
      }
      $return_terms = implode('+',$encoded_terms);
      return $return_terms;
      endif;
   }</code></pre>

The <code>trackable_url</code> function generates the trackable URL from the fields on the admin screen as well as the taxonomies. This appends the appropriate tracking criteria to the URL so that Google Analytics can use the variables and provide information based on these specific variables. To do this, we will use the <a title="add_query_arg" href="https://codex.wordpress.org/Function_Reference/add_query_arg"><code>add_query_arg</code></a> WordPress function.

<pre><code class="language-php">function trackable_url() {
      global $post;
      $custom = get_post_custom($post-&gt;ID);

      // the url
      if ($custom["gaca10-gaurl"][0]) {
         $gaurl = $custom["gaca10-gaurl"][0];
      }
      else { $gaurl = ’; }

      // the term(s)
      if ($gaterm = $custom["gaca10-gaterm"][0]) {
         $gaterm = $custom["gaca10-gaterm"][0];
         $gaterm = urlencode($gaterm);
      }
      else { $gaterm = ’; }

      // the content(s)
      if ($custom["gaca10-gacontent"][0]) {
         $gacontent = $custom["gaca10-gacontent"][0];
         $gacontent = urlencode($gacontent);
      }
      else { $gacontent = ’; }
      $arr_params = array ( 'utm_campaign' =&gt; formatted_utm_taxonomy_terms('ganame'), 'utm_source' =&gt; formatted_utm_taxonomy_terms('gasource'), 'utm_medium' =&gt; formatted_utm_taxonomy_terms('gamedium'), 'utm_term' =&gt; $gaterm, 'utm_content' =&gt; $gacontent);
      return add_query_arg( $arr_params, $gaurl );

   }</code></pre>

The following functions take the campaign-trackable URL and <a href="https://www.richardcastera.com/blog/creating-a-tinyurl-with-tinyurl-api">shortens it with TinyURL</a>. This method uses <a title="wp_remote_get" href="https://codex.wordpress.org/Function_API/wp_remote_get"><code>wp_remote_get</code></a> to generate the shortened URL. It then saves the shortened URL to the post’s meta data when a post is saved. The <code>trackable_url_tiny</code> function enables us to retrieve the shortened URL in the template.

<pre><code class="language-php">// Save the shortened trackable URL to the post meta
   function save_shortened_meta($post_ID) {
      $url = trackable_url();
      $shortened_url = create_tiny_url($url);
      update_post_meta($post_ID, "campaign_tinyurl", $shortened_url);
      return $post_ID;
   }

   // Add an action to save it when the post is saved.
   add_action('save_post', 'save_shortened_meta');

   // Retrieve the shortened URL from post meta
   function trackable_url_tiny($url = null, $post_ID) {
      global $post;
      $custom_fields = get_post_custom($post-&gt;ID);
      $campaign_tinyurl = $custom_fields['campaign_tinyurl'][0];
      return $campaign_tinyurl;

      return $post_ID;
   }

   // Create shortened trackable URL through the wp_remote_get function
   function create_tiny_url($strURL) {
      $tinyurl = wp_remote_get( 'https://tinyurl.com/api-create.php?url='.$strURL );
      if( is_wp_error( $response ) ) {
         return 'Something went wrong!';
      } else {
         return $tinyurl['body'];

      }
   }</code></pre>

The <code>trackable_url_report</code> function is what provides the human-readable version of the variables. These are broken out by each section. The landing page, campaign name, source, medium, terms and content are all separated and displayed individually if they exist.

<pre><code class="language-php">function trackable_url_report() {
      global $post;
      $custom = get_post_custom($post-&gt;ID);

      // get the url
      if ($custom["gaca10-gaurl"][0]) {
         $gaurl = $custom["gaca10-gaurl"][0];
      }
      else { $gaurl = ’; }
      // get the term(s)
      if ($gaterm = $custom["gaca10-gaterm"][0]) {
         $gaterm = $custom["gaca10-gaterm"][0];
      }
      else { $gaterm = ’; }

      // get the content(s)
      if ($custom["gaca10-gacontent"][0]) {
         $gacontent = $custom["gaca10-gacontent"][0];
      }
      else { $gacontent = ’; }

      // The Landing page
      $url_info =’;
      $url_info.= "&lt;strong&gt;". _x( 'Landing Page:','landing page label') . "&lt;/strong&gt; ";
      $url_info.= $gaurl;
      $url_info.= "&lt;br /&gt;";

      // The campaign name
      $url_info.= "&lt;strong&gt;". _x( 'Campaign:','campaign label') . "&lt;/strong&gt; ";
      $url_info.= formatted_utm_taxonomy_terms('ganame');
      $url_info.= "&lt;br /&gt;";

      // The Source
      $url_info.= "&lt;strong&gt;". _x( 'Source:','source label') . "&lt;/strong&gt; ";
      $url_info.= formatted_utm_taxonomy_terms('gasource');
      $url_info.= "&lt;br /&gt;";

      // The medium
      $url_info.= "&lt;strong&gt;". _x( 'Medium:','medium label') . "&lt;/strong&gt; ";
      $url_info.= formatted_utm_taxonomy_terms('gamedium');
      $url_info.= "&lt;br /&gt;";

      // The term
      $url_info.= "&lt;strong&gt;". _x( 'Term:','term label') . "&lt;/strong&gt; ";
      $url_info.= $gaterm;
      $url_info.= "&lt;br /&gt;";

      // The content
      $url_info.= "&lt;strong&gt;". _x( 'Content:','content label') . "&lt;/strong&gt; ";
      $url_info.= $gacontent;
      $url_info.= "&lt;br /&gt;";

      return $url_info;
   }</code></pre>

The <code>display_description</code> function displays the description of the URL. We’ve broken this part out here in order to keep all of the pieces that are specific to the URL together. This is also the last function in the <code>ga-functions.php</code> file.

<pre><code class="language-php">function display_description(){
      global $post;
      $custom = get_post_custom($post-&gt;ID);
      $description = $custom["gaca10-gadescription"][0];
      return $description;
   }

   ?&gt;</code></pre>

Combine these functions into the <code>ga-functions.php</code> file, and then we can move onto creating the template file.</p>

## The Template File

The final file that we will use to generate the view of the trackable URL is <code>campaign-template.php</code>. You will remember from the <code>campaign-tracker.php</code> file that we have a call in the <code>template_redirect()</code> function to redirect users to this template when viewing the custom post type of campaigns.

For display purposes, we will use the <code>single.php</code> file from the current default WordPress theme, TwentyEleven. You can, of course, use another theme and different styles.

First, we include the <code>ga-functions.php</code> file so that we can use some of our display functions. The campaign template also uses the Google Charts API to <a href="https://code.google.com/apis/chart/infographics/docs/overview.html">generate the QR code</a>.

The following code will do all of the heavy lifting to display our campaign-trackable URL, the information about the URL, the shortened URL and the QR code. It will also allow us to edit the post if we need to change a variable. Simply drop this code into <a href="https://codex.wordpress.org/The_Loop">the loop</a>.

<pre><code class="language-php">&lt;h1 class="entry-title"&gt;&lt;?php the_title() ?&gt;&lt;/h1&gt;&lt;br /&gt;

   &lt;?php
   echo "&lt;strong&gt;". _x( 'Description:','description label') . "&lt;/strong&gt; ";
   echo display_description();
   echo "&lt;br /&gt;";
   echo trackable_url_report();
   echo "&lt;br /&gt;";
   echo "&lt;strong&gt;". _x('Trackable URL:','trackable URL label') . "&lt;/strong&gt; ";
   echo "&lt;a href=".trackable_url()." target='_blank'&gt;".trackable_url()."&lt;/a&gt;&lt;br /&gt;";

   echo "&lt;strong&gt;" . _x('Shortened Trackable URL:','shortened trackable URL label') . "&lt;/strong&gt; ";
   echo "&lt;a href=".trackable_url_tiny()." target='_blank'&gt;".trackable_url_tiny()."&lt;/a&gt;&lt;br /&gt;";
   ?&gt;

   &lt;br /&gt;
   &lt;img src="https://chart.googleapis.com/chart?chs=150x150&amp;amp;cht=qr&amp;amp;chl=&lt;?php trackable_url_tiny(); ?&gt;" /&gt;&lt;br /&gt;
   &lt;?php edit_post_link( __( 'Edit', 'twentyeleven' ), '&lt;span class="edit-link"&gt;', '&lt;/span&gt;' ); ?&gt;</code></pre>

When we combine the code, the campaign template will be as follows:

<pre><code class="language-php">&lt;?php
   /**
   * The Template for displaying all single posts.
   *
   * @package WordPress
   * @subpackage Twenty_Eleven
   * @since Twenty Eleven 1.0
   */

   // Include the ga-functions.php file so that we can easily display the results
   include_once('ga-functions.php');

   get_header(); ?&gt;

   &lt;div id="primary"&gt;
   &lt;div id="content" role="main"&gt;

   &lt;?php while ( have_posts() ) : the_post(); ?&gt;

   &lt;nav id="nav-single"&gt;
   &lt;h3 class="assistive-text"&gt;&lt;?php _e( 'Post navigation', 'twentyeleven' ); ?&gt;&lt;/h3&gt;
   &lt;span class="nav-previous"&gt;&lt;?php previous_post_link( '%link', __( '&lt;span class="meta-nav"&gt;&amp;larr;&lt;/span&gt; Previous', 'twentyeleven' ) ); ?&gt;&lt;/span&gt;
   &lt;span class="nav-next"&gt;&lt;?php next_post_link( '%link', __( 'Next &lt;span class="meta-nav"&gt;&amp;rarr;&lt;/span&gt;', 'twentyeleven' ) ); ?&gt;&lt;/span&gt;
   &lt;/nav&gt;&lt;!-- #nav-single --&gt;

   &lt;h1 class="entry-title"&gt;&lt;?php the_title() ?&gt;&lt;/h1&gt;&lt;br /&gt;

   &lt;?php
   echo "&lt;strong&gt;". _x( 'Description:','description label') . "&lt;/strong&gt; ";
   echo display_description();
   echo "&lt;br /&gt;";
   echo trackable_url_report();
   echo "&lt;br /&gt;";
   echo "&lt;strong&gt;". _x('Trackable URL:','trackable URL label') . "&lt;/strong&gt; ";
   echo "&lt;a href=".trackable_url()." target='_blank'&gt;".trackable_url()."&lt;/a&gt;&lt;br /&gt;";

   echo "&lt;strong&gt;" . _x('Shortened Trackable URL:','shortened trackable URL label') . "&lt;/strong&gt; ";
   echo "&lt;a href=".trackable_url_tiny()." target='_blank'&gt;".trackable_url_tiny()."&lt;/a&gt;&lt;br /&gt;";
   ?&gt;

   &lt;br /&gt;
   &lt;img src="https://chart.googleapis.com/chart?chs=150x150&amp;amp;cht=qr&amp;amp;chl=&lt;?php trackable_url_tiny(); ?&gt;" /&gt;&lt;br /&gt;
   &lt;?php edit_post_link( __( 'Edit', 'twentyeleven' ), '&lt;span class="edit-link"&gt;', '&lt;/span&gt;' ); ?&gt;

   &lt;?php comments_template( ’, true ); ?&gt;

   &lt;?php endwhile; // end of the loop. ?&gt;

   &lt;/div&gt;&lt;!-- #content --&gt;
   &lt;/div&gt;&lt;!-- #primary --&gt;

   &lt;?php get_footer(); ?&gt;</code></pre>

When the template is set up and a campaign has been added, then it should display the following page:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2926274b-4bd7-4470-a22c-f7cf81cab90c/display-information.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e3c5e05-53d0-472e-930d-08ad6a437be2/display-information-500.jpg" alt="Display information" width="500" /></a>

## In Conclusion

By using WordPress custom post types in the method described, it is possible to organize marketing campaigns with the relevant Google Analytics campaign-tracking URL, shortened URL and QR code. This makes organizing marketing campaigns much simpler and more effective.

Custom post types make it very easy to set up a system by which to organize content. And we can get creative in how we use custom post types. They can be very useful when organizing content outside of the normal structure of WordPress and other content management systems (i.e. posts, pages, etc.).

Other possible uses of custom post types include the following:

*   Manage client contacts,
*   Create an employee directory,
*   Keep an inventory of items,
*   Organize other data.</p>

### Resources

You may be interested in the following resources and articles:

*   “Custom Post Types in WordPress 3.0,” Konstantin Kovshenin
*   “[Custom Post Types in WordPress](https://justintadlock.com/archives/2010/04/29/custom-post-types-in-wordpress),” Justin Tadlock
*   “[Creating a TinyURL With TinyURL’s API](https://www.richardcastera.com/blog/creating-a-tinyurl-with-tinyurl-api),” Richard Castera
*   “[Getting Started With Infographics](https://code.google.com/apis/chart/infographics/docs/overview.html)” (QR Codes with the Google Charts API), Google Code
*   “[Post Types](https://codex.wordpress.org/Post_Types),” WordPress Codex
*   [URL Builder tool](https://ga-dev-tools.appspot.com/campaign-url-builder/) Google Analytics
*   “[IQ Lessons](https://support.google.com/conversionuniversity/bin/request.py?hl=en&contact_type=indexSplash&rd=1),” Google Analytics

{{< signature "al" >}}


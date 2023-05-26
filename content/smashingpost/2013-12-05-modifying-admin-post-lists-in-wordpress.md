---
title: How To Modify Admin Post Lists In WordPress
slug: modifying-admin-post-lists-in-wordpress
image: >-
  https://www.smashingmagazine.com/inspiration/2014/04/11/get-excited-about-emotional-branding/attachment/why-you-should-get-excited-about-emotional-branding-layouts-jpg/attachment/events_final/
date: 2013-12-05T09:24:37.000Z
author: daniel-pataki
description: >-
  Have you ever created a custom post type and then found that **only the titles
  and dates of your posts are displayed** in the admin lists? While WordPress
  will add taxonomies for you, that’s the most it can do. Adding relevant
  at-a-glance information is easy; in this article, we’ll look how to modify
  admin post lists with WordPress.
categories:
  - WordPress
  - Tools
  - Admin
  - Techniques (WP)
---
Have you ever created a custom post type and then found that <strong>only the titles and dates of your posts are displayed</strong> in the admin lists? While WordPress will add taxonomies for you, that’s the most it can do. Adding relevant at-a-glance information is easy; in this article, we’ll look how to modify admin post lists with WordPress.

To make sure we’re on the same page, an admin list is the table of posts shown in the admin section when you click on “Posts,” “Pages” or another custom post type. Before we delve in, it is worth noting that admin tables are created using the <code>WP_List_Table</code> class. Jeremy Desvaux de Marigny has written a <a href="https://www.smashingmagazine.com/2011/11/03/native-admin-tables-wordpress/">great article on native admin tables</a> that explains how to make these from scratch.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">The Complete Guide To Custom Post Types</span>](https://www.smashingmagazine.com/2012/11/complete-guide-custom-post-types/)
*   [How To Create Native Admin Tables In WordPress The Right Way](https://www.smashingmagazine.com/2011/11/native-admin-tables-wordpress/)
*   [WordPress Shortcodes: A Complete Guide](https://www.smashingmagazine.com/2012/05/wordpress-shortcodes-complete-guide/)

We’ll focus in this article on how to extend existing tables. We’ll do this using an example from a theme that we recently built, named <a href="https://themeforest.net/item/rock-band-awesome-music-template/5581920">Rock Band</a>. Rock Band includes event management, which means that we needed some custom event-specific interface elements and details to make the admin section more useful!

{{% feature-panel %}}

## Creating A Custom Post Type

This process is fairly straightforward and is documented well in “<a href="https://www.smashingmagazine.com/2012/11/08/complete-guide-custom-post-types/">The Complete Guide to Custom Post Types</a>.” All we need is a definition of the labels that we’re going to use and a few settings. Open up your <code>functions.php</code> file and drop the following into it.

<pre><code class="language-php">add_action( 'init', 'bs_post_types' );
function bs_post_types() {

  $labels = array(
    'name'                =&gt; __( 'Events', THEMENAME ),
    'singular_name'       =&gt; __( 'Event', THEMENAME ),
    'add_new'             =&gt; __( 'Add New', THEMENAME ),
    'add_new_item'        =&gt; __( 'Add New Event', THEMENAME ),
    'edit_item'           =&gt; __( 'Edit Event', THEMENAME ),
    'new_item'            =&gt; __( 'New Event', THEMENAME ),
    'all_items'           =&gt; __( 'All Event', THEMENAME ),
    'view_item'           =&gt; __( 'View Event', THEMENAME ),
    'search_items'        =&gt; __( 'Search Events', THEMENAME ),
    'not_found'           =&gt; __( 'No events found', THEMENAME ),
    'not_found_in_trash'  =&gt; __( 'No events found in Trash', THEMENAME ),
    'menu_name'           =&gt; __( 'Events', THEMENAME ),
  );

  $supports = array( 'title', 'editor' );

  $slug = get_theme_mod( 'event_permalink' );
  $slug = ( empty( $slug ) ) ? 'event' : $slug;

  $args = array(
    'labels'              =&gt; $labels,
    'public'              =&gt; true,
    'publicly_queryable'  =&gt; true,
    'show_ui'             =&gt; true,
    'show_in_menu'        =&gt; true,
    'query_var'           =&gt; true,
    'rewrite'             =&gt; array( 'slug' =&gt; $slug ),
    'capability_type'     =&gt; 'post',
    'has_archive'         =&gt; true,
    'hierarchical'        =&gt; false,
    'menu_position'       =&gt; null,
    'supports'            =&gt; $supports,
  );

  register_post_type( 'event', $args );

}</code></pre>

### Quick Tip

By pulling the permalink from the theme settings, you can make sure that users of your theme are able to set their own permalinks. This is important for multilingual websites, on which administrators might want to make sure that URLs are readable by their users.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2770ae69-556f-49f3-8356-1073398e3815/events-original.png"><img loading="lazy" decoding="async" class="109716" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2770ae69-556f-49f3-8356-1073398e3815/events-original.png" alt="events_original" width="1033" height="966" /></a>

What we get is the post list above. It’s better than nothing, but it has no at-a-glance information at all. Event venue, start time and ticket status would be great additions, so let’s get cracking!

## Adding Custom Table Headers

Throughout this whole process, we will never have to touch the <code>WP_Lists_Table</code> class directly. This is wonderful news! Because we’ll be doing everything with hooks, our code will be nice and modular, easily customizable.

Adding the header is as simple as modifying the value of an array. This sounds like a job for a filter!

<pre><code class="language-php">add_filter('manage_event_posts_columns', 'bs_event_table_head');
function bs_event_table_head( $defaults ) {
    $defaults['event_date']  = 'Event Date';
    $defaults['ticket_status']    = 'Ticket Status';
    $defaults['venue']   = 'Venue';
    $defaults['author'] = 'Added By';
    return $defaults;
}</code></pre>

Note the name of the filter: It corresponds to the name of the post type we have created. This means you can modify the table of any post type, not only your custom ones. Just use <code>manage_post_posts_columns</code> to modify the columns for the table of regular posts.

Once this code has been placed in our functions file, you should see the four new table headers. The fields don’t have any content yet; it is for us to decide what goes in them.</p>

## Fill ’er Up!

Adding data for each column is about as “complex” as it was to create the columns.

<pre><code class="language-php">add_action( 'manage_event_posts_custom_column', 'bs_event_table_content', 10, 2 );

function bs_event_table_content( $column_name, $post_id ) {
    if ($column_name == 'event_date') {
    $event_date = get_post_meta( $post_id, '_bs_meta_event_date', true );
      echo  date( _x( 'F d, Y', 'Event date format', 'textdomain' ), strtotime( $event_date ) );
    }
    if ($column_name == 'ticket_status') {
    $status = get_post_meta( $post_id, '_bs_meta_event_ticket_status', true );
    echo $status;
    }

    if ($column_name == 'venue') {
    echo get_post_meta( $post_id, '_bs_meta_event_venue', true );
    }

}</code></pre>

As is obvious from the structure of this function, it gets called separately for each column. Because of this, we need to check which column is currently being displayed and then spit out the corresponding data.

The data we need for this is stored in the <code>postmeta</code> table. Here’s how to do it:

*   The event’s date is stored using the `_bs_meta_event_date` key.
*   The ticket’s status uses the `_bs_meta_event_ticket_status` key.
*   The venue is stored using the `_bs_meta_event_venue` meta key.

Because these are all <code>postmeta</code> values, we just need to use the <code>get_post_meta()</code> function to retrieve them. With the exception of the date, we can echo these values right away.

This brings us to an important point. You are not restricted to showing individual snippets of data or showing links. Whatever you output will be shown. With sufficient time, you could attach a calendar to the dates, which would be shown on hover. You could create flyout menus that open up on click, and so on.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e6eca8a-f388-406d-a8d0-51ce6fbd2e95/events-data.png"><img loading="lazy" decoding="async" class="109717" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e6eca8a-f388-406d-a8d0-51ce6fbd2e95/events-data.png" alt="events_data" width="1019" height="964" /></a>

As you can see, this is much better. The event’s date, ticket status, venue and author can be seen, which makes this table actually informative, rather than just a way to get to edit pages. However, we can do more.

## Ordering Columns

Enabling column ordering takes two steps but is fairly straightforward. First, use a filter to specify which of your columns should be sortable by adding it to an array. Then, create a filter for each column to modify the query when a user clicks to sorts the column.

<pre><code class="language-php">add_filter( 'manage_edit-event_sortable_columns', 'bs_event_table_sorting' );
function bs_event_table_sorting( $columns ) {
  $columns['event_date'] = 'event_date';
  $columns['ticket_status'] = 'ticket_status';
  $columns['venue'] = 'venue';
  return $columns;
}

add_filter( 'request', 'bs_event_date_column_orderby' );
function bs_event_date_column_orderby( $vars ) {
    if ( isset( $vars['orderby'] ) &amp;&amp; 'event_date' == $vars['orderby'] ) {
        $vars = array_merge( $vars, array(
            'meta_key' =&gt; '_bs_meta_event_date',
            'orderby' =&gt; 'meta_value'
        ) );
    }

    return $vars;
}

add_filter( 'request', 'bs_ticket_status_column_orderby' );
function bs_ticket_status_column_orderby( $vars ) {
    if ( isset( $vars['orderby'] ) &amp;&amp; 'ticket_status' == $vars['orderby'] ) {
        $vars = array_merge( $vars, array(
            'meta_key' =&gt; '_bs_meta_event_ticket_status',
            'orderby' =&gt; 'meta_value'
        ) );
    }

    return $vars;
}

add_filter( 'request', 'bs_venue_column_orderby' );
function bs_venue_column_orderby( $vars ) {
    if ( isset( $vars['orderby'] ) &amp;&amp; 'venue' == $vars['orderby'] ) {
        $vars = array_merge( $vars, array(
            'meta_key' =&gt; '_bs_meta_event_venue',
            'orderby' =&gt; 'meta_value'
        ) );
    }

    return $vars;
}</code></pre>

Here is what’s happening in each of these cases. Whenever posts are listed, an array of arguments is passed that determines what is shown — things like how many to show per page, which post type to display, and so on. WordPress knows how to construct the array of arguments for each of its built-in features.

When we say, “order by venue,” WordPress doesn’t know what this means. Results are ordered before they are displayed, not after the fact. Therefore, WordPress needs to know what order to pull posts in before it actually retrieves them. Thus, we tell WordPress which <code>meta_key</code> to filter by and how to treat the values (<code>meta_value</code> for strings, <code>meta_value_num</code> for integers).

As with displaying data, you can go nuts here. You can use all of the arguments that <code>WP_Query</code> takes to perform taxonomy filtering, meta field queries and so on.

By adding the code above, we can now click to order based on date, status and venue. We’re almost there. One more thing would help out a lot, especially when dealing with hundreds of events.</p>

## Data Filtering

Setting up the filters is analogous to setting up ordering. First, we tell WordPress which controls we want to use. Then, we need to make sure those controls actually do something. Let’s get started.

<pre><code class="language-php">add_action( 'restrict_manage_posts', 'bs_event_table_filtering' );
function bs_event_table_filtering() {
  global $wpdb;
  if ( $screen-&gt;post_type == 'event' ) {

    $dates = $wpdb-&gt;get_results( "SELECT EXTRACT(YEAR FROM meta_value) as year,  EXTRACT( MONTH FROM meta_value ) as month FROM $wpdb-&gt;postmeta WHERE meta_key = '_bs_meta_event_date' AND post_id IN ( SELECT ID FROM $wpdb-&gt;posts WHERE post_type = 'event' AND post_status != 'trash' ) GROUP BY year, month " ) ;

    echo ’;
      echo ’ . __( 'Show all event dates', 'textdomain' ) . ’;
    foreach( $dates as $date ) {
      $month = ( strlen( $date-&gt;month ) == 1 ) ? 0 . $date-&gt;month : $date-&gt;month;
      $value = $date-&gt;year . '-' . $month . '-' . '01 00:00:00';
      $name = date( 'F Y', strtotime( $value ) );

      $selected = ( !empty( $_GET['event_date'] ) AND $_GET['event_date'] == $value ) ? 'selected="select"' : ’;
      echo ’ . $name . ’;
    }
    echo ’;

    $ticket_statuses = get_ticket_statuses();
    echo ’;
      echo ’ . __( 'Show all ticket statuses', 'textdomain' ) . ’;
    foreach( $ticket_statuses as $value =&gt; $name ) {
      $selected = ( !empty( $_GET['ticket_status'] ) AND $_GET['ticket_status'] == $value ) ? 'selected="selected"' : ’;
      echo ’ . $name . ’;
    }
    echo ’;

  }
}</code></pre>

I know, this is a bit scarier! Initially, all we are doing is making sure that we add filters to the right page. As you can see from the hook, this is not specific to the post’s type, so we need to check manually.

Once we’re sure that we’re on the events page, we add two controls: a selector for event dates and a selector for ticket statuses.

We have one custom function in there, <code>get_ticket_statuses()</code>, which is used to retrieve a list of ticket statuses. These are all defined by the user, so describing how it works would be overkill. Suffice it to say that it contains an array with the key-value pairs that we need for the selector.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b7d44b5-739b-43d6-8436-df747f7ff946/events-final.png"><img loading="lazy" decoding="async" class="109715" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b7d44b5-739b-43d6-8436-df747f7ff946/events-final.png" alt="events_final" width="1026" height="984" /></a>

Once this is done, the table will reach its final form. We now have our filters along the top, but they don’t work yet. Let’s fix that, shall we?

Filtering data is simply a matter of adding arguments to the query again. This time, instead of ordering our data, we’ll add parameters to narrow down or broaden our returned list of posts.

<pre><code class="language-php">add_filter( 'parse_query','bs_event_table_filter' );
function bs_event_table_filter( $query ) {
  if( is_admin() AND $query-&gt;query['post_type'] == 'event' ) {
    $qv = &amp;$query-&gt;query_vars;
    $qv['meta_query'] = array();

    if( !empty( $_GET['event_date'] ) ) {
      $start_time = strtotime( $_GET['event_date'] );
      $end_time = mktime( 0, 0, 0, date( 'n', $start_time ) + 1, date( 'j', $start_time ), date( 'Y', $start_time ) );
      $end_date = date( 'Y-m-d H:i:s', $end_time );
      $qv['meta_query'][] = array(
        'field' =&gt; '_bs_meta_event_date',
        'value' =&gt; array( $_GET['event_date'], $end_date ),
        'compare' =&gt; 'BETWEEN',
        'type' =&gt; 'DATETIME'
      );

    }

    if( !empty( $_GET['ticket_status'] ) ) {
      $qv['meta_query'][] = array(
        'field' =&gt; '_bs_meta_event_ticket_status',
        'value' =&gt; $_GET['ticket_status'],
        'compare' =&gt; '=',
        'type' =&gt; 'CHAR'
      );
    }

    if( !empty( $_GET['orderby'] ) AND $_GET['orderby'] == 'event_date' ) {
      $qv['orderby'] = 'meta_value';
      $qv['meta_key'] = '_bs_meta_event_date';
      $qv['order'] = strtoupper( $_GET['order'] );
    }

  }
}</code></pre>

For each filter, we need to add rules to the query. When we’re filtering for events, we need to add a <a href="https://codex.wordpress.org/Class_Reference/WP_Query#Custom_Field_Parameters">meta_query</a>. This will return only results for which the custom field key is <code>_bs_meta_event_ticket_status</code> and the value is the given ticket’s status.

Once this final piece of the puzzle is added, we will have a customized WordPress admin list, complete with filtering, ordering and custom data. Well done!

## Overview

Adding custom data to a table is a great way to draw information to the attention of users. Plugin developers can hook their functionality into posts without touching any other functionality, and theme authors can add advanced information about custom post types and other things to relevant places.

<strong>Showing the right information in the right place</strong> can make a <em>huge</em> difference in the salability and likability of any product. That being said, don’t overexploit your newfound power. Don’t add fields just because you can, especially to WordPress’ main tables.

Don’t forget that others know about this, too, and many developers of SEO plugins and similar products already add their own columns to posts. If you’re going to add things to the default post types, I suggest including settings to enable and disable them.

If you’ve used these techniques in one of your products or are wondering how to show some tidbit of information in a table, let us know in the comments!

{{< signature "al, il" >}}


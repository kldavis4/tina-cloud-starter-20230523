---
title: Introducing Term Meta Data In WordPress And How To Use Them
slug: how-to-use-term-meta-data-in-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/244abde5-f03e-4312-acf0-ee232a7ce7d4/excerpt-wordpress-opt.jpg
date: 2015-12-09T23:39:21.000Z
author: thomasmaier
description: >-
  WordPress 4.4 introduced **term meta data** which allows you to save meta
  values for terms in a similar way to post meta data. This is a highly
  anticipated and logical addition to the WordPress system.

  So far, the post and comment meta systems allowed us to add arbitrary data to
  posts and comments. This can be used to add ratings to comments, indicate your
  mood while you were writing a post, attach prices to product posts, and
  various other information you think is relevant to your content. As of the
  newest version of WordPress, **meta data can now be added to terms** which
  allows us to create features like default category thumbnails in a
  standardized way. This tutorial will show you how you can edit, update and
  retrieve these meta data for terms.
categories:
  - WordPress
  - Techniques (WP)
---
WordPress 4.4 introduced <strong>term meta data</strong> which allows you to save meta values for terms in a similar way to post meta data. This is a highly anticipated and logical addition to the WordPress system.

So far, the post and comment meta systems allowed us to add arbitrary data to posts and comments. This can be used to add ratings to comments, indicate your mood while you were writing a post, attach prices to product posts, and various other information you think is relevant to your content. As of the newest version of WordPress, meta data can now be added to terms which allows us to create features like default category thumbnails in a standardized way. This tutorial will show you how you can edit, update and retrieve these meta data for terms.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Extending WordPress With Custom Content Types](https://www.smashingmagazine.com/2015/04/extending-wordpress-custom-content-types/)
*   [How To Add Custom Fields In A WordPress Comment Form](https://www.smashingmagazine.com/2012/05/adding-custom-fields-in-wordpress-comment-form/)
*   [RICG Responsive Images For WordPress](https://www.smashingmagazine.com/2015/02/ricg-responsive-images-for-wordpress/)
*   [Everything You Need To Know About Accelerated Mobile Pages](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)

## Under The Hood Of Term Meta Data

The logic behind term meta data is not new, already being used for posts, comments and users.

{{% feature-panel %}}

To enable meta data for terms, the new <code>termmeta</code> table was introduced. It saves the combination of the <code>term_id</code>, <code>meta_key</code> and <code>meta_value</code>, plus an incrementing <code>meta_id</code>.</p>

## Meta Data Functions

Four new functions were introduced to handle create, read, update and delete (CRUD) operations for term meta data:

*   `add_term_meta()`: adds the meta data
*   `update_term_meta()`: updates existing meta data
*   `delete_term_meta()`: deletes meta data
*   `get_term_meta()`: retrieves the meta data

Under the hood, these functions use the same code that the corresponding functions for post meta data use as well.</p>

## How To Use Term Meta Data

In a recent project, I had to assign additional attributes to non-hierarchical terms, which was a great chance to test the new meta data feature.

The project used a custom post type to represent houses. The features of a house (e.g. TV, sofa, etc.) were terms in a custom taxonomy. The editor of the house information wanted to list the features based on a group that should not be a feature by itself. Hence, I decided to add this group using term meta data.

The taxonomy I used was <code>house_feature</code>, but you can also use the existing <code>category</code> or <code>post_tag</code> taxonomies if you want to use term meta data with post categories or tags.

First, I created my feature taxonomy:

<pre><code class="language-php">add_action('init', 'register_feature_taxonomy');

function register_feature_taxonomy() {
    $labels = array(
        'name' =&gt; _x( 'Features', 'taxonomy general name', 'my_plugin' ),
        'singular_name' =&gt; _x('Features', 'taxonomy singular name', 'my_plugin'),
        'search_items' =&gt; __('Search Feature', 'my_plugin'),
        'popular_items' =&gt; __('Common Features', 'my_plugin'),
        'all_items' =&gt; __('All Features', 'my_plugin'),
        'edit_item' =&gt; __('Edit Feature', 'my_plugin'),
        'update_item' =&gt; __('Update Feature', 'my_plugin'),
        'add_new_item' =&gt; __('Add new Feature', 'my_plugin'),
        'new_item_name' =&gt; __('New Feature:', 'my_plugin'),
        'add_or_remove_items' =&gt; __('Remove Feature', 'my_plugin'),
        'choose_from_most_used' =&gt; __('Choose from common Feature', 'my_plugin'),
        'not_found' =&gt; __('No Feature found.', 'my_plugin'),
        'menu_name' =&gt; __('Features', 'my_plugin'),
    );

    $args = array(
        'hierarchical' =&gt; false,
        'labels' =&gt; $labels,
        'show_ui' =&gt; true,
    );

    register_taxonomy('house_feature', array('houses'), $args);
}</code></pre>

You should change the <code>houses</code> post type in the last line to the one you are using, or just to <code>post</code> if you want to take the new taxonomy out for a test run on default posts.

If you use the code from this article in your theme’s <i>functions.php</i> file or within a plugin, make sure that the text domain <code>my_plugin</code> matches the text domain of your theme or plugin. The <code>my_plugin</code> text domain would work in a plugin with a <code>my_plugin</code> slug.

The groups I assigned the house features to were managed through settings. It can also be a simple array. For the sake of a short, but useful introduction into term meta, I am using the following global array to hold the available groups:

<pre><code class="language-php">$feature_groups = array(
    'bedroom' =&gt; __('Bedroom', 'my_plugin'),
    'living' =&gt; __('Living room', 'my_plugin'),
    'kitchen' =&gt; __('Kitchen', 'my_plugin')
);</code></pre>

## Extending The Term Form

To assign meta data to terms, we need to extend the term edit form. The complicated part is that the hooks we need from now on are built dynamically.</p>

### Adding Meta Data With A New Term

In order to extend the form to add a term, we make use of the <code>{$taxonomy}_add_form_fields</code> hook. For our <code>house_feature</code> taxonomy it resolves into <code>house_feature_add_form_fields</code>.</p>

<pre><code class="language-php">add_action( 'house_feature_add_form_fields', 'add_feature_group_field', 10, 2 );
function add_feature_group_field($taxonomy) {
    global $feature_groups;
    ?&gt;&lt;div class="form-field term-group"&gt;
        &lt;label for="featuret-group"&gt;&lt;?php _e('Feature Group', 'my_plugin'); ?&gt;&lt;/label&gt;
        &lt;select class="postform" id="equipment-group" name="feature-group"&gt;
            &lt;option value="-1"&gt;&lt;?php _e('none', 'my_plugin'); ?&gt;&lt;/option&gt;&lt;?php foreach ($feature_groups as $_group_key =&gt; $_group) : ?&gt;
                &lt;option value="&lt;?php echo $_group_key; ?&gt;" class=""&gt;&lt;?php echo $_group; ?&gt;&lt;/option&gt;
            &lt;?php endforeach; ?&gt;
        &lt;/select&gt;
    &lt;/div&gt;&lt;?php
}</code></pre>

This adds a select form right between the original form fields and the submit button.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac9f4050-0f73-423b-b5f3-421a0e14a88c/feature-field-create-form-opt.png"><img title="term form with meta data field" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/402c3e6f-5696-44eb-90c2-7c229d3f5b24/feature-field-create-form-500px-opt.png" alt="create term form with meta data field" /></a><figcaption>The form to create a new term in the custom taxonomy should now look like this. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac9f4050-0f73-423b-b5f3-421a0e14a88c/feature-field-create-form-opt.png">View large version</a>)</figcaption></figure>

To save the term meta we need to hook into the action, which is fired when the new term is being saved. This time we use the <code>created_{$taxonomy}</code> hook.</p>

<pre><code class="language-php">add_action( 'created_house_feature', 'save_feature_meta', 10, 2 );

function save_feature_meta( $term_id, $tt_id ){
    if( isset( $_POST['feature-group'] ) &amp;&amp; ’ !== $_POST['feature-group'] ){
        $group = sanitize_title( $_POST['feature-group'] );
        add_term_meta( $term_id, 'feature-group', $group, true );
    }
}</code></pre>

We get the term data from the <code>$_POST</code> array sent with the form and save it using the new <code>add_term_meta()</code> function. Like <code>add_post_meta()</code>, it takes four arguments:

*   `$term_id`: the id of the term,
*   `$meta_key`: the meta key,
*   `$meta_value`: the value,
*   `$unique`: whether the key can only be used once; defaults to `false`.

I am setting <code>$unique</code> to true, because I want each feature of the house to be listed in only one group.

## Updating A Term With Meta Data

Even though they share similar features, adding a new term and updating an existing one is technically different in WordPress. Therefore, we need to add an update routine too.

We make use of the <code>{$taxonomy}_edit_form_fields</code> hook to get the field for the group into the edit form.</p>

<pre><code class="language-php">add_action( 'house_feature_edit_form_fields', 'edit_feature_group_field', 10, 2 );

function edit_feature_group_field( $term, $taxonomy ){

    global $feature_groups;

    // get current group
    $feature_group = get_term_meta( $term-&gt;term_id, 'feature-group', true );

    ?&gt;&lt;tr class="form-field term-group-wrap"&gt;
        &lt;th scope="row"&gt;&lt;label for="feature-group"&gt;&lt;?php _e( 'Feature Group', 'my_plugin' ); ?&gt;&lt;/label&gt;&lt;/th&gt;
        &lt;td&gt;&lt;select class="postform" id="feature-group" name="feature-group"&gt;
            &lt;option value="-1"&gt;&lt;?php _e( 'none', 'my_plugin' ); ?&gt;&lt;/option&gt;
            &lt;?php foreach( $feature_groups as $_group_key =&gt; $_group ) : ?&gt;
                &lt;option value="&lt;?php echo $_group_key; ?&gt;" &lt;?php selected( $feature_group, $_group_key ); ?&gt;&gt;&lt;?php echo $_group; ?&gt;&lt;/option&gt;
            &lt;?php endforeach; ?&gt;
        &lt;/select&gt;&lt;/td&gt;
    &lt;/tr&gt;&lt;?php
}</code></pre>

In addition to the add form, we need to retrieve the existing term data using <code>get_term_meta()</code> and pre-select it. This function has three arguments:

*   `$term_id`: the id of the term,
*   `$key`: the key of the meta data,
*   `$single`: whether to return a single result; defaults to `false` which would return an array.

Since I am expecting only one value to be returned, I set <code>$single</code> to <code>true</code>.

We now need to hook into <code>edited_{$taxonomy}</code> to save the data.</p>

<pre><code class="language-php">add_action( 'edited_house_feature', 'update_feature_meta', 10, 2 );

function update_feature_meta( $term_id, $tt_id ){

    if( isset( $_POST['feature-group'] ) &amp;&amp; ’ !== $_POST['feature-group'] ){
        $group = sanitize_title( $_POST['feature-group'] );
        update_term_meta( $term_id, 'feature-group', $group );
    }
}</code></pre>

We use <code>update_term_meta()</code> to overwrite the existing value instead of adding a new set of meta data.</p>

## Displaying The Term Meta Data In The Term List

The meta data is saved now. Let’s display it in a new column in the term list table. First, let’s add the column and header to the table. Finding the correct hook to extend a table in the WordPress dashboard is again a bit tricky because of so many flexible hook names.

The pattern you can use here is <code>manage_edit-{$taxonomy}_columns</code>, even though this is not exactly how the hook is defined.</p>

<pre><code class="language-php">add_filter('manage_edit-house_feature_columns', 'add_feature_group_column' );

function add_feature_group_column( $columns ){
    $columns['feature_group'] = __( 'Group', 'my_plugin' );
    return $columns;
}</code></pre>

To add the content into the column fields, you can use the hook pattern <code>manage_{$taxonomy}_custom_column</code>.</p>

<pre><code class="language-php">add_filter('manage_house_feature_custom_column', 'add_feature_group_column_content', 10, 3 );

function add_feature_group_column_content( $content, $column_name, $term_id ){
    global $feature_groups;

    if( $column_name !== 'feature_group' ){
        return $content;
    }

    $term_id = absint( $term_id );
    $feature_group = get_term_meta( $term_id, 'feature-group', true );

    if( !empty( $feature_group ) ){
        $content .= esc_attr( $feature_groups[ $feature_group ] );
    }

    return $content;
}</code></pre>

Again, we use <code>get_term_meta()</code> to retrieve the value and then simply attach it to the existing content. This would allow other developers to attach something else here as well.

It was in the nature of my project, that many terms shared the same value, so let’s make the group column sortable. We only need to add it to the sortable columns.</p>

<pre><code class="language-php">add_filter( 'manage_edit-house_feature_sortable_columns', 'add_feature_group_column_sortable' );

function add_feature_group_column_sortable( $sortable ){
    $sortable[ 'feature_group' ] = 'feature_group';
    return $sortable;
}</code></pre>

This is how the term list might look like with an extra column for term data:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b2fdde9-114b-4f95-8844-25ff92b2a896/feature-list-with-meta-opt.png"><img title="term list with meta data" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eec6b4f7-3707-40e2-84c4-79b8d3579c6a/feature-list-with-meta-500px-opt.png" alt="term list with meta data" /></a><figcaption>Term list with meta data table. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b2fdde9-114b-4f95-8844-25ff92b2a896/feature-list-with-meta-opt.png">View large version</a>)</figcaption></figure>

## Deleting Term Meta Data

If you remove a term, the corresponding meta data will also be removed, so you don’t need to clean up after yourself.

However, if you find yourself needing to remove term meta data, you can use the <code>delete_term_meta()</code> function. It takes up to three arguments:

*   `$term_id`: the id of the term
*   `$meta_key`: the meta key
*   `$meta_value`: the previous value

You only need to provide <code>$meta_value</code> if you want to remove meta data with a specific value.</p>

## Retrieving Terms By Meta Value

Like with posts, you can also retrieve terms using the meta values. Set the <code>meta_query</code> parameter when using <code>get_terms()</code> or <code>wp_get_object_terms()</code>.

With the following query I would retrieve all features in the <code>kitchen</code> group.</p>

<pre><code class="language-php">$args = array(
    'hide_empty' =&gt; false, // also retrieve terms which are not used yet
    'meta_query' =&gt; array(
        array(
           'key'       =&gt; 'feature-group',
           'value'     =&gt; 'kitchen',
           'compare'   =&gt; 'LIKE'
        )
    )
);

$terms = get_terms( 'house_feature', $args );</code></pre>

The syntax of <code>meta_query</code> is the same as in <a href="https://codex.wordpress.org/Class_Reference/WP_Query#Custom_Field_Parameters"><code>WP_Query</code></a>, which allows you to make use of different operators for <code>compare</code>, like <code>NOT LIKE</code>, <code>EXISTS</code>, or <code>BETWEEN</code>.

Since I use meta data to group my terms, getting the result back ordered by the meta value would be really helpful. However, unlike with <code>WP_Query</code>, you can’t use <code>orderby =&gt; meta_value</code> yet and must sort the results after you retrieve them.

To display our terms and meta data, we iterate through the results and make use of <code>get_term_meta()</code> again.</p>

<pre><code class="language-php">if ( ! empty( $terms ) &amp;&amp; ! is_wp_error( $terms ) ){
    echo '&lt;ul&gt;';
    foreach ( $terms as $term ) {
        echo '&lt;li&gt;' . $term-&gt;name . ' (' . get_term_meta( $term-&gt;term_id, 'feature-group', true ) . ')' . '&lt;/li&gt;';
    }
    echo '&lt;/ul&gt;';
}</code></pre>

## Conclusion

I know many projects that already save meta information for custom taxonomies. A lot of them are probably going to update and use the new meta data logic once WordPress 4.4 is widely used.

The last thing I am missing now in the taxonomy roadmap is to be able to set meta data for a specific term–object relationship. Let me know if you can relate to that in the comments.</p>

### Resources

*   [`get_terms` in the WordPress Codex](https://codex.wordpress.org/Function_Reference/get_terms)
*   [Taxonomy roundup](https://make.wordpress.org/core/2015/10/23/4-4-taxonomy-roundup/) on make.wordpress.org

<em>Excerpt image: <a href="https://www.flickr.com/photos/nbachiyski/2536017020/">Nikolay Bachiyski</a></em>

{{< signature "dp, jb, ml, og" >}}


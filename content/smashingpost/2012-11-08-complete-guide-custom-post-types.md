---
title: The Complete Guide To WordPress Custom Post Types
slug: complete-guide-custom-post-types
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dea6029-b8cf-44d6-bdef-7362d6906367/wp-6.jpg
date: 2012-11-08T13:05:45.000Z
author: daniel-pataki
description: >-
  WordPress has been gaining a foothold in the general CMS game for a few years
  now but the real breakthrough was the custom post type mechanism which allows
  for the creation of a wide variety of content. Let's take a look at how this
  came to be and all the options that this great functionality offers.
categories:
  - WordPress
  - Techniques
---
WordPress has been gaining a foothold in the general content management system (CMS) game for a few years now, but the real breakthrough was the custom post type mechanism which allows for the creation of a wide variety of content. Let's take a look at how this came to be and all the options that this great functionality offers.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/355ea6cc-032a-4378-9f4e-5162e539dcb2/customposttypes.jpg"><img loading="lazy" decoding="async" class="alignnone" title="Some Of The custom Post Types You Can Create In WordPress" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/355ea6cc-032a-4378-9f4e-5162e539dcb2/customposttypes.jpg" alt="wordpress custom post type" width="592" height="400" /></a><br>
<em>Some of the custom post types you can create in WordPress.</em></figure>

## What It Used To Be Like

In practice, custom post types have been around for a long time, more specifically since February 17, 2005, when WordPress 1.5 added support for static pages, creating the <code>post_type</code> database field.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Extending WordPress With Custom Content Types](https://www.smashingmagazine.com/2015/04/extending-wordpress-custom-content-types/)
*   [A Detailed Guide To WordPress Custom Page Templates](https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/)
*   [Customizing WordPress Archives For Categories, Tags](https://www.smashingmagazine.com/2014/08/customizing-wordpress-archives-categories-terms-taxonomies/)
*   [Building A Custom Archive Page For WordPress](https://www.smashingmagazine.com/2015/04/building-custom-wordpress-archive-page/)

{{% feature-panel %}}

The <code>wp_insert_post()</code> function has been around since WordPress 1.0, so when the <code>post_type</code> field was implemented in 1.5, you could simply set the <code>post_type</code> value when inserting a post. Of course, creating and managing custom post types required much more than that, but the amount of coding needed became less and less as WordPress functions became more and more flexible.

By version 2.8, the <code>register_post_type()</code> function and some other helpful things were added to the nightly builds, and when 2.9 came out, the functions became available to everyone. At this point, extensive coding and hacks were not needed to make WordPress a full blown CMS; you could use plenty of great built-in functions to make WordPress do your bidding.</p>

## What WordPress Can Do For You Now

A custom post type is nothing more than a regular post with a different <code>post_type</code> value in the database. The post type of regular posts is <code>post</code>, pages use <code>page</code>, attachments use <code>attachment</code> and so on. You can now create your own to indicate the type of content created. You could create custom post types for books, movies, reviews, products and so on.

If created correctly, you can achieve the following with a few lines of code:

*   The custom post type will show up in the back end as a separate menu item with its own post list and “add new” page
*   Navigating to `https://mysite.com/customposttype/` will take you to the archive page for the post type. This is akin to visiting the front page for latest posts from the “post” post type.
*   Categories and tags can be made available to the custom post type, or you can create custom taxonomies.

Apart from these, you can modify countless options, such as where the custom post type should be placed in the menu, should it be searchable, which user level can access it, should it be hierarchical, custom rewrite rules, etc.

Different types of content have different data requirements. For regular posts, you'll want to specify the author, category, date and so on. For a “book” custom post type, ideally you'd like to have the option to specify the book's author, the page count, genre, publisher and other book-specific data. Using custom meta boxes, this is easily achieved and managed as well.

Custom <a href="https://www.smashingmagazine.com/2011/10/create-custom-post-meta-boxes-wordpress/">meta boxes</a> enable you to add additional boxes to the edit screen of a post. They usually use custom fields, so you could just use custom fields as well, but by separating out some custom fields as meta boxes, you can create a much smoother and usable admin.</p>

## Working With Custom Post Types

To effectively create and use custom post types, you'll need to be familiar with the following:

*   Creating custom post types,
*   Creating custom taxonomies,
*   Creating custom meta boxes.

## Creating Custom Post Types

First on our agenda is creating the post type itself. Ideally you should <a href="https://www.smashingmagazine.com/2011/09/30/how-to-create-a-wordpress-plugin/">create a plugin</a> when working with custom post types, but if you don't know how, or just need a quick test, you can use the <code>functions.php</code> file in your theme.</p>

<pre><code class="language-php">function my_custom_post_product() {
  $args = array();
  register_post_type( 'product', $args ); 
}
add_action( 'init', 'my_custom_post_product' );</code></pre>

In its simplest form, it will create a post type which has almost no customization. It won't be public, it won't show up in the admin, interaction messages will be the same as posts (“post saved,” “post updated,” etc.) and so on. To tailor our new post type to our needs, I'll go through some of the more frequently-used options and add them to the previously empty <code>$args</code> array.</p>

<pre><code class="language-php">function my_custom_post_product() {
  $labels = array(
    'name'               =&gt; _x( 'Products', 'post type general name' ),
    'singular_name'      =&gt; _x( 'Product', 'post type singular name' ),
    'add_new'            =&gt; _x( 'Add New', 'book' ),
    'add_new_item'       =&gt; __( 'Add New Product' ),
    'edit_item'          =&gt; __( 'Edit Product' ),
    'new_item'           =&gt; __( 'New Product' ),
    'all_items'          =&gt; __( 'All Products' ),
    'view_item'          =&gt; __( 'View Product' ),
    'search_items'       =&gt; __( 'Search Products' ),
    'not_found'          =&gt; __( 'No products found' ),
    'not_found_in_trash' =&gt; __( 'No products found in the Trash' ), 
    'parent_item_colon'  =&gt; ’,
    'menu_name'          =&gt; 'Products'
  );
  $args = array(
    'labels'        =&gt; $labels,
    'description'   =&gt; 'Holds our products and product specific data',
    'public'        =&gt; true,
    'menu_position' =&gt; 5,
    'supports'      =&gt; array( 'title', 'editor', 'thumbnail', 'excerpt', 'comments' ),
    'has_archive'   =&gt; true,
  );
  register_post_type( 'product', $args ); 
}
add_action( 'init', 'my_custom_post_product' );</code></pre>

*   **`labels`** The `labels` option should be an array defining the different labels that a custom post type can have. I have separated this out above just to make the arguments for registering a post type clearer.
*   **`description`** A short explanation of our custom post type; what it does and why we're using it.
*   **`public`** This option controls a bunch of things in one go. Setting this to true will set a bunch of other options (all to do with visibility) to true. For example, it is possible to have the custom post type visible but not queryable. More on this later.
*   **`menu_position`** Defines the position of the custom post type menu in the back end. Setting it to “5” places it below the “posts” menu; the higher you set it, the lower the menu will be placed.
*   **`supports`** This option sets up the default WordPress controls that are available in the edit screen for the custom post type. By default, only the title field and editor are shown. If you want to add support for comments, revisions, post formats and such you will need to specify them here. For a full list take a look at the [arguments section](https://codex.wordpress.org/Function_Reference/register_post_type#Arguments) in the Codex.
*   **`has_archive`** If set to true, rewrite rules will be created for you, enabling a post type archive at `https://mysite.com/posttype/` (by default)

<figure><img loading="lazy" decoding="async" title="A Custom Post Type In The Menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e64adc8-7cbd-4201-a0a2-8b92e9c5f555/custom-post-type.png" alt="A custom post type in the menu." width="443" height="349" /><figcaption>A custom post type in the menu.</figcaption></figure>

After setting this up, you should see the menu entry for the custom post type. You should be able to add posts, view the post list in the admin and also visit the published posts on the website.

As I mentioned there are a lot of things you can modify when creating a post type. I suggest looking at the arguments list in the Codex for a full description of each option and the possible values.</p>

### Custom Interaction Messages

WordPress generates a number of messages triggered by user actions. Updating, publishing, searching, etc., in the back end all lead to messages which — by default — are tailored to regular posts. You can change the text of these messages easily by using the <code>post_updated_messages</code> hook.</p>

<pre><code class="language-php">function my_updated_messages( $messages ) {
  global $post, $post_ID;
  $messages['product'] = array(
    0 =&gt; ’, 
    1 =&gt; sprintf( __('Product updated. &lt;a href="%s"&gt;View product&lt;/a&gt;'), esc_url( get_permalink($post_ID) ) ),
    2 =&gt; __('Custom field updated.'),
    3 =&gt; __('Custom field deleted.'),
    4 =&gt; __('Product updated.'),
    5 =&gt; isset($_GET['revision']) ? sprintf( __('Product restored to revision from %s'), wp_post_revision_title( (int) $_GET['revision'], false ) ) : false,
    6 =&gt; sprintf( __('Product published. &lt;a href="%s"&gt;View product&lt;/a&gt;'), esc_url( get_permalink($post_ID) ) ),
    7 =&gt; __('Product saved.'),
    8 =&gt; sprintf( __('Product submitted. &lt;a target="_blank" href="%s"&gt;Preview product&lt;/a&gt;'), esc_url( add_query_arg( 'preview', 'true', get_permalink($post_ID) ) ) ),
    9 =&gt; sprintf( __('Product scheduled for: &lt;strong&gt;%1$s&lt;/strong&gt;. &lt;a target="_blank" href="%2$s"&gt;Preview product&lt;/a&gt;'), date_i18n( __( 'M j, Y @ G:i' ), strtotime( $post-&gt;post_date ) ), esc_url( get_permalink($post_ID) ) ),
    10 =&gt; sprintf( __('Product draft updated. &lt;a target="_blank" href="%s"&gt;Preview product&lt;/a&gt;'), esc_url( add_query_arg( 'preview', 'true', get_permalink($post_ID) ) ) ),
  );
  return $messages;
}
add_filter( 'post_updated_messages', 'my_updated_messages' );</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/126e9a0f-8306-42d1-be95-b02de2913589/custommessage.png"><img loading="lazy" decoding="async" title="A Custom Message After Saving A Product" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/126e9a0f-8306-42d1-be95-b02de2913589/custommessage.png" alt="A custom message after saving a product." width="346" height="52" /></a><figcaption>A custom message after saving a product.</figcaption></figure>

As you can see, this is not the most user-friendly method of managing messages. An associative array would be far better; we could see what each message is for without having to read the actual message.

Notice that you can change the messages for all custom post types using this single function. The <code>$messages</code> array holds the messages for all post types, so you can modify them all here. I personally create a function for each post type just so I can group the post type creation and the custom messages together easily.</p>

### Contextual Help

A feature I rarely see implemented is the customized contextual help. As a user, I've never actually used this feature myself, but I'm sure that many people do; in any case, it's nice to provide some hand-holding for less experienced users.

The contextual help feature is a descending tab which can be seen in the top right of pages where available. Let's take a look at how the contents can be changed.</p>

<pre><code class="language-php">function my_contextual_help( $contextual_help, $screen_id, $screen ) { 
  if ( 'product' == $screen-&gt;id ) {

    $contextual_help = '&lt;h2&gt;Products&lt;/h2&gt;
    &lt;p&gt;Products show the details of the items that we sell on the website. You can see a list of them on this page in reverse chronological order - the latest one we added is first.&lt;/p&gt; 
    &lt;p&gt;You can view/edit the details of each product by clicking on its name, or you can perform bulk actions using the dropdown menu and selecting multiple items.&lt;/p&gt;';

  } elseif ( 'edit-product' == $screen-&gt;id ) {

    $contextual_help = '&lt;h2&gt;Editing products&lt;/h2&gt;
    &lt;p&gt;This page allows you to view/modify product details. Please make sure to fill out the available boxes with the appropriate details (product image, price, brand) and &lt;strong&gt;not&lt;/strong&gt; add these details to the product description.&lt;/p&gt;';

  }
  return $contextual_help;
}
add_action( 'contextual_help', 'my_contextual_help', 10, 3 );</code></pre>

This is also a bit difficult because you have to know the ID of the screen you are on. If you print out the contents of the <code>$screen</code> variable, you should be able to determine the ID easily. This is also a function you can use to modify the contextual help of all custom post types at once, but I personally recommend grouping this together with the previous two blocks and only using it for one custom post type at a time.</p>

### Overview

To quickly recap, we used three functions to create a “complete” custom post type. We used <code>register_post_type()</code> to create the post type itself and two hooks — <code>contextual_help</code> and <code>post_updated_messages</code> — to create helpful guidance and relevant messages respectively.</p>

## Custom Taxonomies

Your regular blog posts use categories and tags to create an organization structure. However, the same organization doesn't necessarily make sense for custom post types. Your blog posts could be about your “Life,” your “Thoughts” or your “Dreams.” These are obviously not appropriate for products.

This is the problem that drove developers to create custom taxonomies. You can create a separate taxonomy named “Product Categories” to house categories you only use for products. Kevin Leary wrote a great article about <a href="https://www.smashingmagazine.com/2012/01/04/create-custom-taxonomies-wordpress/">custom taxonomies in WordPress</a> which I highly recommend, so I will only go into minor detail here.</p>

<pre><code class="language-php">function my_taxonomies_product() {
  $args = array();
  register_taxonomy( 'product_category', 'product' $args );
}

add_action( 'init', 'my_taxonomies_product', 0 );</code></pre>

Similarly to custom post types, you can create a taxonomy very easily, but you need to work at it a bit to tailor it to your needs. Custom taxonomies behave a bit better out of the box as they are public by default, so the above is actually enough to tie this taxonomy to the product posts. Let's look at a customized example.</p>

<pre><code class="language-php">function my_taxonomies_product() {
  $labels = array(
    'name'              =&gt; _x( 'Product Categories', 'taxonomy general name' ),
    'singular_name'     =&gt; _x( 'Product Category', 'taxonomy singular name' ),
    'search_items'      =&gt; __( 'Search Product Categories' ),
    'all_items'         =&gt; __( 'All Product Categories' ),
    'parent_item'       =&gt; __( 'Parent Product Category' ),
    'parent_item_colon' =&gt; __( 'Parent Product Category:' ),
    'edit_item'         =&gt; __( 'Edit Product Category' ), 
    'update_item'       =&gt; __( 'Update Product Category' ),
    'add_new_item'      =&gt; __( 'Add New Product Category' ),
    'new_item_name'     =&gt; __( 'New Product Category' ),
    'menu_name'         =&gt; __( 'Product Categories' ),
  );
  $args = array(
    'labels' =&gt; $labels,
    'hierarchical' =&gt; true,
  );
  register_taxonomy( 'product_category', 'product', $args );
}
add_action( 'init', 'my_taxonomies_product', 0 );</code></pre>

As you can see, not much has changed. We added some labels and set the hierarchical option to true. This enables “category style” taxonomies. When set to false (this is the default), your taxonomy will be like the default tags.

There are a few other power options available which you can read about in Leary's article, or you can go to the <a href="https://codex.wordpress.org/Function_Reference/register_taxonomy">Codex entry on <code>register_taxonomy()</code></a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3999e7f-02e2-4510-b824-e34fadd32a1f/productcategories.jpg"><img loading="lazy" decoding="async" title="The Product Categories Custom Taxonomy" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3999e7f-02e2-4510-b824-e34fadd32a1f/productcategories.jpg" alt="The Product Categories custom taxonomy." width="808" height="496" /></a><figcaption>The Product Categories custom taxonomy.</figcaption></figure>

## Post Meta Boxes

Meta boxes are the draggable boxes you see in the WordPress edit screen for a post. There are numerous built-in meta boxes like the publishing controls, the taxonomies, the author box, etc., but you can create some for yourself.

Meta boxes tend to be used to manage custom field data in a much more user-friendly way than the built-in custom fields box does. Since you put the controls in place, you can add client-side error checking and many other fancy things.

Justin Tadlock wrote the all-encompassing <a href="https://www.smashingmagazine.com/2011/10/04/create-custom-post-meta-boxes-wordpress/">custom meta box article</a> here on Smashing Magazine, which is a great in-depth article on the subject. I recommend reading it for the full picture, but I'll get you started here.

Creating a meta box requires three steps:

*   Define the box itself,
*   Define the content of the meta box,
*   Define how the data from the box is handled.</p>

### Defining the Meta Box

<pre><code class="language-php">add_action( 'add_meta_boxes', 'product_price_box' );
function product_price_box() {
    add_meta_box( 
        'product_price_box',
        __( 'Product Price', 'myplugin_textdomain' ),
        'product_price_box_content',
        'product',
        'side',
        'high'
    );
}</code></pre>

The code above creates the meta box with the following parameters (in the order given):

*   The unique identifier for the meta box (it does not have to match the function name),
*   The title of the meta box (visible to users),
*   The function which will display the contents of the box,
*   The post type the meta box belongs to,
*   The placement of the meta box,
*   The priority of the meta box (determines “how high” it is placed).</p>

### Defining the Content of the Meta Box

<pre><code class="language-php">function product_price_box_content( $post ) {
  wp_nonce_field( plugin_basename( __FILE__ ), 'product_price_box_content_nonce' );
  echo '&lt;label for="product_price"&gt;&lt;/label&gt;';
  echo '&lt;input type="text" id="product_price" name="product_price" placeholder="enter a price" /&gt;';
}</code></pre>

This is a simple box which only contains the price, so we have created a label and an input to manage it. A <a href="https://codex.wordpress.org/WordPress_Nonces">nonce</a> field is also present, which adds security to the data submission.</p>

### Handling Submitted Data

In most cases, you will want to save the data as a custom field, but you are by no means restricted to this method. You could use the input to make a third party API call, to generate an XML file or whatever you like. The most common use is saving custom post data, so let's take a look at how that is done.</p>

<pre><code class="language-php">add_action( 'save_post', 'product_price_box_save' );
function product_price_box_save( $post_id ) {

  if ( defined( 'DOING_AUTOSAVE' ) &amp;&amp; DOING_AUTOSAVE ) 
  return;

  if ( !wp_verify_nonce( $_POST['product_price_box_content_nonce'], plugin_basename( __FILE__ ) ) )
  return;

  if ( 'page' == $_POST['post_type'] ) {
    if ( !current_user_can( 'edit_page', $post_id ) )
    return;
  } else {
    if ( !current_user_can( 'edit_post', $post_id ) )
    return;
  }
  $product_price = $_POST['product_price'];
  update_post_meta( $post_id, 'product_price', $product_price );
}</code></pre>

The biggest part of this function is all about safety. First of all, if an autosave is being performed, nothing happens because the user hasn't actually submitted the form. Then the nonce is checked, followed by permission checking. If these are all passed, we take our data and add it to the post using the <code>update_post_meta()</code> function.</p>

<figure><img loading="lazy" decoding="async" title="An Example Of A Meta Box For An Apartment Post Type" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/384ac3d4-bf9c-493f-ad36-4b63efd51b74/metabox.png" alt="An example of a meta box for an apartment post type." width="296" height="288" /><figcaption>An example of a meta box for an apartment post type.</figcaption></figure>

## Displaying Your Content

While there a plenty of nuances to all of the above, you should be familiar with the basics. All that is left is to actually use the data we now have and show things to the user. This involves showing posts — perhaps from various custom post types and taxonomies — and using our post metadata.</p>

### Displaying Posts

If you've created a post type with the <code>has_archive</code> parameter set to “true,” WordPress will list your posts on the post type's archive page. If your post type is called “books,” you can simply go to <code>https://mysite.com/books/</code> and you'll see your post list.

This page uses <code>archive-[post_type].php</code> for the display if it exists (<code>archive-books.php</code> in our case). If it doesn't exist, it will use <code>archive.php</code> and if that doesn't exist it will use <code>index.php</code>.

Another way to display custom post type content is to use a custom query with the <code>WP_Query</code> class. To display posts from a certain post type and custom taxonomy, you could do something like this:

<pre><code class="language-php">&lt;?php
    $args = array(
      'post_type' =&gt; 'product',
      'tax_query' =&gt; array(
        array(
          'taxonomy' =&gt; 'product_category',
          'field' =&gt; 'slug',
          'terms' =&gt; 'boardgames'
        )
      )
    );
    $products = new WP_Query( $args );
    if( $products-&gt;have_posts() ) {
      while( $products-&gt;have_posts() ) {
        $products-&gt;the_post();
        ?&gt;
          &lt;h1&gt;&lt;?php the_title() ?&gt;&lt;/h1&gt;
          &lt;div class='content'&gt;
            &lt;?php the_content() ?&gt;
          &lt;/div&gt;
        &lt;?php
      }
    }
    else {
      echo 'Oh ohm no products!';
    }
  ?&gt;</code></pre>

### Displaying Metadata

Metadata can be retrieved easily using the <code>get_post_meta()</code> function. In our example above, we saved a post meta field named <code>product_price</code>. We can retrieve the value of this field for a given post using the following code:

<pre><code class="language-php">&lt;?php
  // If we are in a loop we can get the post ID easily
  $price = get_post_meta( get_the_ID(), 'product_price', true );

  // To get the price of a random product we will need to know the ID
  $price = get_post_meta( $product_id, 'product_price', true );
?&gt;</code></pre>

## Final Words

As you can see, creating a CMS is pretty easy due to the modular nature of WordPress controls and functions. The methods outlined here can be used extremely well to create customized admins for nearly anything you can think of.

Since defining the content of <a href="https://www.smashingmagazine.com/2011/10/create-custom-post-meta-boxes-wordpress/">meta boxes</a> is completely up to you, you have the power to create additional features for your controls, making you or your clients very happy.

You can take this one step further with custom admin pages and completely custom content, but that's a story for another day.</p>

<em><a href="https://alittlecode.com/wordpress-custom-post-types-and-custom-taxonomies-a-roundup/">Image source</a> of picture on front page.</em>

{{< signature "cp" >}}


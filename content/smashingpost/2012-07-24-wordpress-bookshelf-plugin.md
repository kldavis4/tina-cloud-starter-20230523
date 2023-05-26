---
title: Create A WordPress Bookshelf Plugin
slug: wordpress-bookshelf-plugin
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85520dc1-ead1-4baa-b8b5-9f4496a6fa70/smbookthumb.jpg
date: 2012-07-24T08:47:57.000Z
author: kailan-wyatt
description: >-
  This tutorial explains how to create a WordPress bookshelf plugin that displays books on a shelf like [Smashing Magazine’s](https://www.smashingmagazine.com/ebooks/) eBook page.
categories:
  - WordPress
  - Techniques (WP)
---
Some key WordPress functionality will be showcased throughout the tutorial that could benefit your own project.

The article covers how to create post types, shortcodes and meta fields using WordPress’ functionality and how to combine them to make a fully configurable plugin. To begin, we’ll explain how to register the plugin, develop the back-end functionality and then create the front-end display using shortcodes.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3f5d54f-0c34-4ce7-a694-26232a62d075/sm-book-thumb.jpg"><img loading="lazy" decoding="async" class="106213" title="sm_book_thumb" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3f5d54f-0c34-4ce7-a694-26232a62d075/sm-book-thumb.jpg" alt="" width="500" height="300" /></a>

## Setting Up The Plugin

The standard method of registering a plugin in WordPress is to add some information to the header of the file. Create a file named <code>sm_books.php</code>, and add the information below to it. Note that the information being registered is “Plugin Name,” “Author,” “Version,” etc. This information will be used to tell WordPress about the plugin so that the plugin can be activated and displayed in the plugin management screen.

{{% feature-panel %}}

<pre><code class="language-php">&lt;?php
/*
Plugin Name: SM Books
Plugin URI: https://b4ucode.com
Description: Displays Books and books
Author: B4uCode
Version: 1.0.0
Author URI: https://b4ucode.com
*/</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4835c35f-f2ae-4cfb-9c11-191450a21fad/sm-book-registered.jpg"><img loading="lazy" decoding="async" class="106212" title="sm_book_registered" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4835c35f-f2ae-4cfb-9c11-191450a21fad/sm-book-registered.jpg" alt="Book Plugin" width="630" height="202" /></a>

To learn more about creating a plugin, check out “<a href="https://www.smashingmagazine.com/2011/09/30/how-to-create-a-wordpress-plugin/">WordPress Essentials: How to Create a WordPress Plugin</a>.”

## Register The Post’s Type

In order to add the new book system, we will register a new custom post type using the <code>register_post_type</code> function. To access this function, we will trigger it using the <code>add_action</code> function. Add the following to the <code>sm_books.php</code> file:

<pre><code class="language-php">//Register Book Post Type
add_action( 'init', 'create_sm_book_type' );
function create_sm_book_type() {
   register_post_type( 'sm_books',
      array(
         'labels' =&gt; array(
            'name' =&gt; __( 'Books' ),
            'singular_name' =&gt; __( 'Book' )
         ),
      'public' =&gt; true,
      'has_archive' =&gt; true,
      'supports' =&gt; array('title','editor','thumbnail')
      )
   );
}</code></pre>

This snippet is a basic way to create a post type. The <code>register_post_type( $post_type, $args )</code> function takes two parameters: <code>$post_type</code> and <code>$args</code>. The first parameter is a 20-character string that will be used for the name of the new type. The default post types in WordPress are “Post,” “Page,” “Attachment,” “Revisions” and “Navigation Menus.” These default names cannot be used when creating a custom type, so we will use <code>sm_books</code>. The second parameter is an optional array that stores a multitude of options for the post type. The array accepts “labels” that will be used and seen while using <code>sm_books</code>, as well as options available for the post type, such as <code>exclude_from_search</code>, <code>show_ui</code> and much more.</p>

## Add Books Category

For this tutorial, we will add a custom set of categories for the books. This set is referred to as a “taxonomy,” and we will create it with the <code>register_taxonomy</code> function, which we will call <code>sm_book_category</code>. The categories enable us to assign our entries to different categories for displaying on the screen. Just as with our previous snippet in the file, we will use <code>add_action</code> to trigger our function. Also, <code>register_taxonomy($taxonomy, $object_type, $args)</code> is very similar to the <code>register_post_type</code> function, with its three parameters:

1.  `$taxonomy` A string with no capital letters or spaces.
2.  `$object_type` Defines the post type that this new taxonomy will be attached to.
3.  `$args` An optional array that holds options and labels similar to what we see in the `register_post_type` function.

<pre><code class="language-php">//Add Book Categories
add_action( 'init', 'sm_book_taxonomies', 0 );
function sm_book_taxonomies(){
   register_taxonomy('sm_book_category', 'sm_books', array(
      'hierarchical'=&gt;true,
      'label'=&gt;'Categories'
      )
   );
}</code></pre>

## Add Meta Fields

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bb74166-ac84-4322-b093-9203945411ba/sm-book-information.jpg"><img loading="lazy" decoding="async" class="106211" title="sm_book_information" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bb74166-ac84-4322-b093-9203945411ba/sm-book-information.jpg" alt="Meta Data Fields" width="506" height="244" /></a>

As you may have noticed, each book has different attributes, consisting of prices and links. We will add these attributes as custom meta data fields using the <code>add_meta_boxes</code> action in WordPress. At the moment, we will also add the <code>save_post</code> action to save these fields. Once we’ve triggered our function, the <code>add_meta_box( $id, $title, $callback, $post_type, $context, $priority, $callback_args )</code> function will establish the “ID,” “Name” and “Description” of the meta box area. The other <code>$post_type</code> parameter determines what post types the meta box should appear in; and for the <code>$callback</code>, we will use the <code>sm_bk_info_box</code> function, which will render the HTML output of form fields.

<pre><code class="language-php">add_action( 'add_meta_boxes', 'sm_book_extra_box' );
add_action( 'save_post', 'sm_books_save_postdata' );

function sm_book_extra_box() {
   add_meta_box(
      'sm_bk_info_box',
      __( 'Book Information', 'sm_bk_info_box' ),
      'sm_bk_info_box',
      'sm_books',
      'side'
   );
}

/* Prints the box content */
function sm_bk_info_box( $post ) {

   $price = get_post_meta( $post-&gt;ID, 'price', true );
   $sale_price =  get_post_meta( $post-&gt;ID, 'sale_price', true );
   $link_amazon =  get_post_meta( $post-&gt;ID, 'link_amazon', true );
   $link_google =  get_post_meta( $post-&gt;ID, 'link_google', true );
   $link_apple =  get_post_meta( $post-&gt;ID, 'link_apple', true );

   // Use nonce for verification
   wp_nonce_field( plugin_basename( __FILE__ ), 'sm_book_noncename' );
?&gt;

&lt;p&gt;
  &lt;label for="price"&gt;Price
  &lt;input type="text" name="price"
   id="price" size="10" value="&lt;?php echo $price; ?&gt;" /&gt;
  &lt;/label&gt;
&lt;/p&gt;
&lt;p&gt;
  &lt;label for="sale_price"&gt;Sale Price
  &lt;input type="text" name="sale_price"
   id="sale_price" size="10" value="&lt;?php echo $sale_price; ?&gt;" /&gt;
  &lt;/label&gt;
&lt;/p&gt;
&lt;p&gt;
  &lt;label for="link_amazon"&gt;Amazon Link
  &lt;input type="text" name="link_amazon"
   id="link_amazon" size="25" value="&lt;?php echo $link_amazon; ?&gt;" /&gt;
  &lt;/label&gt;
&lt;/p&gt;
&lt;p&gt;
  &lt;label for="link_google"&gt;Google Link
  &lt;input type="text" name="link_google"
   id="link_google" size="25" value="&lt;?php echo $link_google; ?&gt;" /&gt;
  &lt;/label for="myplugin_new_field"&gt;
&lt;/p&gt;
&lt;p&gt;
  &lt;label for="link_apple"&gt;Apple Link
  &lt;input type="text" name="link_apple"
   id="link_apple" size="25" value="&lt;?php echo $link_apple; ?&gt;" /&gt;
  &lt;/label&gt;
&lt;/p&gt;
&lt;?php
}</code></pre>

To save the meta data fields that we created previously, we will create the <code>sm_books_save_postdata</code> function that we defined in our <code>save_post</code> action. Within this function, we will check for submitted post data and update the post meta data using the <code>update_post_meta</code> function. Add the following snippet to the <code>sm_books.php</code> file to give the plugin an update-able set of custom fields:

<pre><code class="language-php">function sm_books_save_postdata($post_id){
if ( defined( 'DOING_AUTOSAVE' ) &amp;&amp; DOING_AUTOSAVE )
   return;

   if ( !wp_verify_nonce( $_POST['sm_book_noncename'],
   plugin_basename( __FILE__ ) ) )
    return;

    if ( !current_user_can( 'edit_post', $post_id ) )
    return;

    if( isset( $_POST['price'] ) ){
      update_post_meta( $post_id,'price',
      esc_attr( $_POST['price'] ) );
   }
     if( isset( $_POST['sale_price'] ) ){
      update_post_meta( $post_id,'sale_price',
           esc_attr( $_POST['sale_price'] ) );
   }
   if( isset( $_POST['link_amazon'] ) ){
      update_post_meta( $post_id,'link_amazon',
           esc_attr( $_POST['link_amazon'] ) );
   }
   if( isset( $_POST['link_google'] ) ){
      update_post_meta( $post_id,'link_google',
           esc_attr( $_POST['link_google'] ) );
   }
   if( isset( $_POST['link_apple'] ) ){
      update_post_meta( $post_id,'link_apple',
           esc_attr( $_POST['link_apple'] ) );
   }
}</code></pre>

The <code>update_post_meta</code> takes the post’s ID as the first argument, the key to update as the second argument and the value to be saved as the third argument.

## Add Featured Post

For our custom book system, we will add an option for a thumbnail, which will be used to show the book cover on our shelf. We will use the featured post’s thumbnail to accomplish this, and we’ll set the image size that we intend to use with the <code>add_image_size</code> function.

<pre><code class="language-php">//Enable Thumbnail
if ( function_exists( 'add_theme_support' ) ) {
   add_theme_support( 'post-thumbnails' );
      set_post_thumbnail_size( 150, 150 );
      add_image_size( 'book-thumb', 84, 107, true );
}</code></pre>

The name of the thumb that we will be referencing is <code>book-thumb</code>, and the size that we will try to resize to is 84 × 107 pixels. These are optional, but based on what we’re going for, the numbers suit our needs.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">A Beginner’s Guide To Creating A WordPress Website</span>](https://www.smashingmagazine.com/2016/02/beginners-guide-creating-wordpress-website/)
*   [How To Create Tabs On WordPress Settings Pages](https://www.smashingmagazine.com/2011/10/create-tabs-wordpress-settings-pages/)
*   [How To Contribute To WordPress](https://www.smashingmagazine.com/2013/05/contributing-to-wordpress/)
*   [Diary Of A WordCamp](https://www.smashingmagazine.com/2012/05/diary-of-a-wordcamp/)

## Add Shortcode

Now that we’ve created the administrative side of the plugin, we will create the front-end design. For this tutorial, we will use a WordPress shortcode to add our book listing to the page. Our shortcode will look like the following on any page:

<pre><code class="language-php">[sm_books category="coding"]</code></pre>

The shortcode above will be used to display the list of books in the category of “coding.” Note that “coding” is the slug of the custom taxonomy that we created. In the end, the plugin will be able to list all of the books if we leave out the <code>category</code> attribute of the shortcode.

Now, let’s move on to making the shortcode work. Add the following code to the <code>sm_books.php</code> file:

<pre><code class="language-php">function sm_display($atts) {
   extract( shortcode_atts( array('category' =&gt; ’), $atts ) );
   $args = array('post_type'=&gt;'sm_books', 'sm_book_category'=&gt;$category);
   $posts = new WP_Query( $args );
   $html = '&lt;div class="sm_holder"&gt;&lt;div class="shelf"&gt;&lt;div class="innerDiv" id="sm_book_1"&gt;';

   // Book Loop
   if ( $posts-&gt;have_posts() ) : while ( $posts-&gt;have_posts() ) : $posts-&gt;the_post();
      $book_cover = get_the_post_thumbnail(
         get_the_ID(),'book-thumb',
         $attr=array("alt"=&gt;get_the_title())
      );
   $html .= '&lt;a href="'.get_permalink().'" class="books"&gt;'.$book_cover.'&lt;/a&gt;';
   endwhile; endif;

   $html.='&lt;/div&gt;&lt;/div&gt;&lt;table class="sm_book_tbl" cellspacing="0" cellpadding="0"&gt;';

   // The Loop
   if ( $posts-&gt;have_posts() ) : while ( $posts-&gt;have_posts() ) : $posts-&gt;the_post();

      $price =  get_post_meta( get_the_ID(), 'price', true );
      $sale_price = get_post_meta( get_the_ID(), 'sale_price', true );
      $link_amazon = get_post_meta( get_the_ID(), 'link_amazon', true );
      $link_google = get_post_meta( get_the_ID(), 'link_google', true );
      $link_apple = get_post_meta( get_the_ID(), 'link_apple', true );
      $html.='&lt;tr&gt;&lt;td class="title"&gt;&lt;a href="'.get_permalink().'"&gt;'.get_the_title().'&lt;/a&gt;&lt;br&gt;';
      if ($link_amazon):
         $html .= '&lt;small&gt;&lt;a style="color:#999" href="'.$link_amazon.'"&gt;Amazon&lt;/a&gt;';
      if ($link_google || link_apple):
         $html .=' | ';
      endif;
      endif;
      if($link_google):
         $html .='&lt;a style="color:#999" href="'.$link_google.'"&gt;Google&lt;/a&gt;&lt;/small&gt;';
      if($link_apple):
         $html .=' | ';
      endif;
      endif;
      if($link_apple):
         $html .='&lt;a style="color:#999" href="'.$link_apple.'"&gt;Apple&lt;/a&gt;&lt;/small&gt;';
      endif;
      $html .= '&lt;/td&gt;&lt;td&gt;';

      if ($sale_price &amp;&amp; $price) {
         $html .= $sale_price.'&lt;br /&gt;';
         $html .= '&lt;span class="old_price"&gt;'.$price.'&lt;/span&gt;';
      } elseif ($price) {
         $html .= $price;
      } else {
         $html .= ’;
      }
      $html .= '&lt;/td&gt;
      &lt;td class="cart"&gt;
         &lt;a style="margin:0px" class="sm_cart_button" href="'.get_permalink().'"&gt;Add to Cart&lt;/a&gt;
      &lt;/td&gt;
      &lt;/tr&gt;';

   endwhile; endif;

   $html .= '&lt;/table&gt;';
   $html .= '&lt;/div&gt;';
   return $html;
}</code></pre>

In the snippet above, we have created a couple of loops that will be rendered when the shortcode is entered. By instantiating the <code>WP_Query</code> class, we are creating a couple of loops to display the books. The arguments that we will use are <code>post_type</code> of <code>sm_books</code>; then, we will use the argument of <code>sm_book_category</code>, which is querying a taxonomy. The value we add will be derived from the shortcode.

The first loop renders the book’s cover in a div where the shelf image will be displayed. The second loop places a set of rows below the shelf and outputs some information about each book. The template tags are used as follows:

*   `get_permalink()` Fetches the permalink.
*   `get_the_ID()` Fetches the post’s ID, which is combined with `get_post_meta` to get the meta fields.
*   `get_the_title()` Fetches the title.

The final bit for the shortcode is the action that actually registers the shortcode. The first argument is the string that will be written to call the shortcode. The second is the function that will be executed. Add the following below your function:

<pre><code class="language-php">add_shortcode( 'sm_books', 'sm_display' );</code></pre>

## Styling Our Listing

Looking at what we have so far, you can imagine how out of place everything looks. Therefore, at this stage, we will add some CSS to style our output. Create a folder named <code>sm_books</code>. Then, create a file named <code>style.css</code>, and add the following code:

<pre><code class="language-css">.sm_holder {
   padding: 0px;
   border-bottom: 5px solid #41B7D8;
   width: 630px;
}
div.shelf {
   background-image: url(shelf_bg.jpg);
   display: block;
}
.shelf div.innerDiv {
   padding: 0px 34px;
   width: 100%;
}
.shelf .books img {
   margin-right: 10px;
   padding-top: 15px;
   margin-bottom: 11px;
}
span.old_price {
   color: #E53B2C;
   text-decoration: line-through;
}
.sm_book_tbl {
   margin: 0px 20px 0px 0px !important;
   width: 100%;
   background-color: #f3f3f3;
   border: 1px solid #e5e5e5
}
.sm_book_tbl td.title {
   height: 60px;
   width: 70%;
   padding-left: 20px;
   padding-right: 20px;
   color: #999
}
.sm_book_tbl td.cart {
   padding: 10px 20px;
   color: #999;
}</code></pre>

In our style sheet, we have added a background image to our <code>shelf</code> div, as seen in the declaration for the <code>div.shelf</code> class. This image will be located in the <code>sm_books</code> folder. Attached to this tutorial is the source file; add the <code>shelf_bg.jpg</code> file to that folder.

Once completed, we will attach the style sheet to our plugin. Add the following snippet to the bottom of the <code>sm_books.php</code> file. Using some WordPress functions, we will register the style sheet from our folder with the WordPress system.

<pre><code class="language-php">function sm_add_styles() {
   wp_register_style( 'sm_add_styles',
   plugins_url('sm_books/style.css', __FILE__) );
   wp_enqueue_style( 'sm_add_styles' );
}
add_action( 'wp_enqueue_scripts', 'sm_add_styles' );</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/184f01a0-cff6-4a32-935a-59aa810d4a39/sm-book-preview.jpg"><img loading="lazy" decoding="async" class="106210" title="sm_book_preview" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/184f01a0-cff6-4a32-935a-59aa810d4a39/sm-book-preview.jpg" alt="Book Preview" width="630" height="439" /></a>

### Download the plugin

You can download the <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/407a78e3-1004-4aa0-99b4-54a3c21b4e4e/b4ucode-smashing-bookshelf.1">B4uCode Smashing Books plugin</a>, which contains everything covered in this tutorial.</p>

## Conclusion

Having done this tutorial, you should be able to create a nice shelving plugin for your books. The plugin might serve your needs if you need an online book archive or library. The options aren’t limited to books either; you could create a similar system for CDs, DVDs and records, and you could tweak it to show videos. The possibilities are endless.</p>

### Resources From the WordPress Codex

*   “[ShortCode API](https://codex.wordpress.org/Shortcode_API)”
*   “[Writing a Plugin](https://codex.wordpress.org/Writing_a_Plugin)”
*   “[Function Reference/register taxonomy](https://codex.wordpress.org/Function_Reference/register_taxonomy)”
*   “[Function Reference/add meta box](https://codex.wordpress.org/Function_Reference/add_meta_box)”
*   “[Post Types](https://codex.wordpress.org/Post_Types)”

{{< signature "al" >}}


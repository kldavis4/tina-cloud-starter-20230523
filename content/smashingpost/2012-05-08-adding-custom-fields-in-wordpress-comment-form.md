---
title: How To Add Custom Fields In A WordPress Comment Form
slug: adding-custom-fields-in-wordpress-comment-form
image: >-
  https://www.smashingmagazine.com/general/2013/12/06/175489-revision-195/attachment/comment-wordpress-plugin-500/
date: 2012-05-08T13:56:07.000Z
author: pritam
description: >-
  If you have created websites or blogs, then you need no introduction to WordPress, one of the most popular content management systems (CMS). WordPress powers millions of websites, for individuals as well as big companies. Why is it so successful?
categories:
  - WordPress
  - Comments
  - Custom Fields
---
Apart from its ease of use and the availability of themes and plugins, WordPress can be easily modified to include custom features and functions. Hooks and filters are built into the CMS that allow you to add functionality or strip out something that is not required. You can customize the way WordPress handles content as well as comments. For example, you could require readers to leave their phone number and/or address when leaving a comment.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [3 Approaches To Adding Configurable Fields To Your WordPress Plugin](https://www.smashingmagazine.com/2016/04/three-approaches-to-adding-configurable-fields-to-your-plugin/)
*   [Introducing Term Meta Data In WordPress And How To Use Them](https://www.smashingmagazine.com/2015/12/how-to-use-term-meta-data-in-wordpress/)
*   [Building An Advanced Notification System For WordPress](https://www.smashingmagazine.com/2015/05/building-wordpress-notification-system/)
*   [<span class="headline">Common WordPress Malware Infections</span>](https://www.smashingmagazine.com/2012/10/four-malware-infections-wordpress/)

You might want them to say whether they liked your blog post. You could have any one of thousands of reasons for adding input fields to the comment form on your WordPress website. So, how do you extend the WordPress comment form with a custom input field?

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b2aeec0-c189-47e6-a765-f688f1f80ff1/comment-wordpress-plugin.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4453481b-7125-4cfb-b8cc-90c538f277f6/comment-wordpress-plugin-500.jpg" alt="Add custom fields in WordPress comment form" width="500" height="327" /></a><br>
<em>Flickr/<a href="https://www.flickr.com/photos/31878512@N06/4704140020/">Neal</a></em>

In this article, we will add three input fields to the comment form of a WordPress website: two text-input fields (for a phone number and comment title) and a radio option for rating the current article. We will use the <a href="https://codex.wordpress.org/Function_Reference/add_comment_meta"><code>add_comment_meta</code></a> function to add a meta data field to comments. In the process, we will also modify the comment form using the <a href="https://codex.wordpress.org/Function_Reference/comment_form"><code>comment_form_default_fields</code> filter</a> and the <code>comment_form_after_fields</code> and <code>comment_form_logged_in_after</code> actions. And we will use many more functions to achieve the desired result.

We can extend the comment form by editing the theme or by creating a theme that alters the behavior of the active theme to include the additional input fields. Modifying the theme is relatively easier to do, but it has an obvious limitation: all the effort that has gone into customization will be for nought if the theme is replaced. Using a plugin to customize the comment form frees us from this limitation. This way, the customized comment form will apply to all themes (except those that have non-standard methods for adding the comment form). Let’s take the plugin route, to avoid having to go through the entire coding process in case we switch themes. We will call our plugin “Extend Comment.”

Open your text editor of choice (Notepad, Notepad++, BlueFish, etc.), and create a new file, <code>extendcomment.php</code>. Make sure to save it in a folder of the same name, <code>ExtendComment,</code> to keep the organization of files simple. As the first step in our coding, let’s add the headers for our WordPress plugin. The headers are pretty much self-explanatory:

<pre><code class="language-php">&lt;?php
/*
Plugin Name: Extend Comment
Version: 1.0
Plugin URI: https://smartwebworker.com
description: >-
  A plugin to add fields to the comment form.
Author: Specky Geek
Author URI: https://www.speckygeek.com
*/</code></pre>

Now, we need to start actually adding the input fields. We’ll start by adding a text input field for a phone number. We will add it to the default fields of the comment form for collecting the author’s information. The default fields are for name, email address and website URL. This set of input fields is hidden if the user is logged in. In the code below, we have recalled the information of the logged-in user as well as the information on whether a field is required. We have modified all of the default fields and added a field for a phone number by creating an array with our settings and passing it through a filter.

<pre><code class="language-php">// Add custom meta (ratings) fields to the default comment form
// Default comment form includes name, email address and website URL
// Default comment form elements are hidden when user is logged in

add_filter('comment_form_default_fields', 'custom_fields');
function custom_fields($fields) {

    $commenter = wp_get_current_commenter();
    $req = get_option( 'require_name_email' );
    $aria_req = ( $req ? " aria-required='true'" : ’ );

    $fields[ 'author' ] = '&lt;p class="comment-form-author"&gt;'.
      '&lt;label for="author"&gt;' . __( 'Name' ) . '&lt;/label&gt;'.
      ( $req ? '&lt;span class="required"&gt;*&lt;/span&gt;' : ’ ).
      '&lt;input id="author" name="author" type="text" value="'. esc_attr( $commenter['comment_author'] ) .
      '" size="30" tabindex="1"' . $aria_req . ' /&gt;&lt;/p&gt;';

    $fields[ 'email' ] = '&lt;p class="comment-form-email"&gt;'.
      '&lt;label for="email"&gt;' . __( 'Email' ) . '&lt;/label&gt;'.
      ( $req ? '&lt;span class="required"&gt;*&lt;/span&gt;' : ’ ).
      '&lt;input id="email" name="email" type="text" value="'. esc_attr( $commenter['comment_author_email'] ) .
      '" size="30"  tabindex="2"' . $aria_req . ' /&gt;&lt;/p&gt;';

    $fields[ 'url' ] = '&lt;p class="comment-form-url"&gt;'.
      '&lt;label for="url"&gt;' . __( 'Website' ) . '&lt;/label&gt;'.
      '&lt;input id="url" name="url" type="text" value="'. esc_attr( $commenter['comment_author_url'] ) .
      '" size="30"  tabindex="3" /&gt;&lt;/p&gt;';

    $fields[ 'phone' ] = '&lt;p class="comment-form-phone"&gt;'.
      '&lt;label for="phone"&gt;' . __( 'Phone' ) . '&lt;/label&gt;'.
      '&lt;input id="phone" name="phone" type="text" size="30"  tabindex="4" /&gt;&lt;/p&gt;';

  return $fields;
}</code></pre>

In the next step, we have to add a text field for the comment’s title and a radio list for rating the article. These fields cannot be added to the default fields for the author’s information above because even logged-in users will need to input these. This time we have not filtered any default function, but we have added new actions altogether. The <code>comment_form_logged_in_after</code> action adds the input fields below the status message that is displayed to logged-in users, just above the comment input box. It will not be activated for users who are not logged in. To show the input fields to non-logged-in users, we have added the <code>comment_form_after_fields</code> action, which displays the fields below the default fields for the author’s information. We have marked the rating field as <code>required</code>, which we’ll take care of later. Instead of using plain HTML for the radio input boxes, we have used simple code that runs a loop and renders the input boxes with the relevant values until there are five of them.

<pre><code class="language-php">// Add fields after default fields above the comment box, always visible

add_action( 'comment_form_logged_in_after', 'additional_fields' );
add_action( 'comment_form_after_fields', 'additional_fields' );

function additional_fields () {
  echo '&lt;p class="comment-form-title"&gt;'.
  '&lt;label for="title"&gt;' . __( 'Comment Title' ) . '&lt;/label&gt;'.
  '&lt;input id="title" name="title" type="text" size="30"  tabindex="5" /&gt;&lt;/p&gt;';

  echo '&lt;p class="comment-form-rating"&gt;'.
  '&lt;label for="rating"&gt;'. __('Rating') . '&lt;span class="required"&gt;*&lt;/span&gt;&lt;/label&gt;
  &lt;span class="commentratingbox"&gt;';

    //Current rating scale is 1 to 5. If you want the scale to be 1 to 10, then set the value of $i to 10.
    for( $i=1; $i &lt;= 5; $i++ )
    echo '&lt;span class="commentrating"&gt;&lt;input type="radio" name="rating" id="rating" value="'. $i .'"/&gt;'. $i .'&lt;/span&gt;';

  echo'&lt;/span&gt;&lt;/p&gt;';

}</code></pre>

Our comment form has the input fields, but they are useless until we have a system for saving the data inputted by users. By adding an action to the <code>comment_post</code> hook, we devise a method for saving the values of meta data if these are not blank. We should make sure not to save blank meta data fields in order to keep the database table from being cluttered with empty rows. We’re also sanitizing the inputted data using the <code>wp_filter_nohtml_kses</code> filter.

Here is the default usage of the <code>add_comment_meta</code> function:

<pre><code class="language-php">add_comment_meta($comment_id, $meta_key, $meta_value, $unique = false)</code></pre>

In the code, <code>$comment_id</code> is the comment’s default ID set by WordPress. It will be left as is to allow for processing of all comments. The <code>$meta_key</code> stands for the names of the fields as set by us. In this case, the meta keys are the phone number, comment title and rating. Here is how we implement the function in our plugin:

<pre><code class="language-php">// Save the comment meta data along with comment

add_action( 'comment_post', 'save_comment_meta_data' );
function save_comment_meta_data( $comment_id ) {
  if ( ( isset( $_POST['phone'] ) ) &amp;&amp; ( $_POST['phone'] != ’) )
  $phone = wp_filter_nohtml_kses($_POST['phone']);
  add_comment_meta( $comment_id, 'phone', $phone );

  if ( ( isset( $_POST['title'] ) ) &amp;&amp; ( $_POST['title'] != ’) )
  $title = wp_filter_nohtml_kses($_POST['title']);
  add_comment_meta( $comment_id, 'title', $title );

  if ( ( isset( $_POST['rating'] ) ) &amp;&amp; ( $_POST['rating'] != ’) )
  $rating = wp_filter_nohtml_kses($_POST['rating']);
  add_comment_meta( $comment_id, 'rating', $rating );
}</code></pre>

Remember marking the ratings field as <code>required</code>? Let’s tell WordPress to refuse comments without a rating. We’ll add a function to the <code>preprocess_comment</code> filter that will be applied to the comment data before it is saved. We’re checking whether the ratings field is empty and then displaying an error message if it is.

<pre><code class="language-php">// Add the filter to check whether the comment meta data has been filled

add_filter( 'preprocess_comment', 'verify_comment_meta_data' );
function verify_comment_meta_data( $commentdata ) {
  if ( ! isset( $_POST['rating'] ) )
  wp_die( __( 'Error: You did not add a rating. Hit the Back button on your Web browser and resubmit your comment with a rating.' ) );
  return $commentdata;
}</code></pre>

Now we have our additional input fields in the comment form. We will use the following function to retrieve the comment’s meta data:

<pre><code class="language-php">get_comment_meta( $comment_id, $meta_key, $single = false )</code></pre>

If we had been working with a theme, then all of the codes above would have gone into the <code>functions.php</code> file, and the code below would have been included in the comment template. Because we are creating a plugin, we will modify the comment’s output and inject our meta data into it. To do this, we’ll make use of the <code>comment_text</code> filter. In the code below, we first retrieve the URL of the plugin’s folder, which is required only because we will be using images saved in that folder (if we were using the codes in a theme, it would have been the URL of the style sheet’s directory or the theme’s directory).

Depending on whether the comment data is set, we might have to retrieve the comment data and text and then add them to the comment section, with the desired formatting. In the code below, the comment’s title is appended to the beginning of the comment’s text, while the rating images and value are added at the end.

<pre><code class="language-php">// Add the comment meta (saved earlier) to the comment text
// You can also output the comment meta values directly to the comments template  

add_filter( 'comment_text', 'modify_comment');
function modify_comment( $text ){

  $plugin_url_path = WP_PLUGIN_URL;

  if( $commenttitle = get_comment_meta( get_comment_ID(), 'title', true ) ) {
    $commenttitle = '&lt;strong&gt;' . esc_attr( $commenttitle ) . '&lt;/strong&gt;&lt;br/&gt;';
    $text = $commenttitle . $text;
  } 

  if( $commentrating = get_comment_meta( get_comment_ID(), 'rating', true ) ) {
    $commentrating = '&lt;p class="comment-rating"&gt;  &lt;img src="'. $plugin_url_path .
    '/ExtendComment/images/'. $commentrating . 'star.gif"/&gt;&lt;br/&gt;Rating: &lt;strong&gt;'. $commentrating .' / 5&lt;/strong&gt;&lt;/p&gt;';
    $text = $text . $commentrating;
    return $text;
  } else {
    return $text;
  }
}</code></pre>

Now, our plugin is ready for us to add the desired input fields in the comment form and to display the meta data with comments. We could stop here, but we won’t. WordPress allows us to edit comments, and we want the option to edit the information entered in these meta fields as well. Therefore, we will continue coding our plugin and add an option to edit these meta fields from the comment editing screen.

We’ll add a meta box on the comment editing page using the <code>add_meta_boxes_comment</code> hook, which tells WordPress to add the reference meta box to the comment editing page. In the function, we’ll add a meta box using the <code>add_meta_box</code> function, the details of which you can check in the <a href="https://codex.wordpress.org/Function_Reference/add_meta_box">WordPress Codex</a>.

<pre><code class="language-php">add_meta_box( $id, $title, $callback, $post_type, $context, $priority, $callback_args );</code></pre>

We’re using the meta boxes to add the form fields, along with a <code>wp_nonce_field</code> for security. In the callback function, we retrieve the meta data before proceeding. We then recreate the same set of input fields as were added in the comment form; the only difference is that here, we also show the value. For the rating radio field, we have again used a simple loop; this time checking whether the radio should be checked comes in handy. Using the resulting input fields, we can now modify the meta data added to comments.

<pre><code class="language-php">// Add an edit option to comment editing screen  

add_action( 'add_meta_boxes_comment', 'extend_comment_add_meta_box' );
function extend_comment_add_meta_box() {
    add_meta_box( 'title', __( 'Comment Metadata - Extend Comment' ), 'extend_comment_meta_box', 'comment', 'normal', 'high' );
}

function extend_comment_meta_box ( $comment ) {
    $phone = get_comment_meta( $comment-&gt;comment_ID, 'phone', true );
    $title = get_comment_meta( $comment-&gt;comment_ID, 'title', true );
    $rating = get_comment_meta( $comment-&gt;comment_ID, 'rating', true );
    wp_nonce_field( 'extend_comment_update', 'extend_comment_update', false );
    ?&gt;
    &lt;p&gt;
        &lt;label for="phone"&gt;&lt;?php _e( 'Phone' ); ?&gt;&lt;/label&gt;
        &lt;input type="text" name="phone" value="&lt;?php echo esc_attr( $phone ); ?&gt;" class="widefat" /&gt;
    &lt;/p&gt;
    &lt;p&gt;
        &lt;label for="title"&gt;&lt;?php _e( 'Comment Title' ); ?&gt;&lt;/label&gt;
        &lt;input type="text" name="title" value="&lt;?php echo esc_attr( $title ); ?&gt;" class="widefat" /&gt;
    &lt;/p&gt;
    &lt;p&gt;
        &lt;label for="rating"&gt;&lt;?php _e( 'Rating: ' ); ?&gt;&lt;/label&gt;
      &lt;span class="commentratingbox"&gt;
      &lt;?php for( $i=1; $i &lt;= 5; $i++ ) {
        echo '&lt;span class="commentrating"&gt;&lt;input type="radio" name="rating" id="rating" value="'. $i .'"';
        if ( $rating == $i ) echo ' checked="checked"';
        echo ' /&gt;'. $i .' &lt;/span&gt;';
        }
      ?&gt;
      &lt;/span&gt;
    &lt;/p&gt;
    &lt;?php
}</code></pre>

As our last step, we need to devise a mechanism for saving the modified data from the editing screen. This is quite similar to the process for saving the meta data from a comment form. Here, we use the <code>edit_comment</code> function to verify the nonce key, and then we update or delete the comment meta field.

<pre><code class="language-php">// Update comment meta data from comment editing screen 

add_action( 'edit_comment', 'extend_comment_edit_metafields' );

function extend_comment_edit_metafields( $comment_id ) {
    if( ! isset( $_POST['extend_comment_update'] ) || ! wp_verify_nonce( $_POST['extend_comment_update'], 'extend_comment_update' ) ) return;

  if ( ( isset( $_POST['phone'] ) ) &amp;&amp; ( $_POST['phone'] != ’) ) :
  $phone = wp_filter_nohtml_kses($_POST['phone']);
  update_comment_meta( $comment_id, 'phone', $phone );
  else :
  delete_comment_meta( $comment_id, 'phone');
  endif;

  if ( ( isset( $_POST['title'] ) ) &amp;&amp; ( $_POST['title'] != ’) ):
  $title = wp_filter_nohtml_kses($_POST['title']);
  update_comment_meta( $comment_id, 'title', $title );
  else :
  delete_comment_meta( $comment_id, 'title');
  endif;

  if ( ( isset( $_POST['rating'] ) ) &amp;&amp; ( $_POST['rating'] != ’) ):
  $rating = wp_filter_nohtml_kses($_POST['rating']);
  update_comment_meta( $comment_id, 'rating', $rating );
  else :
  delete_comment_meta( $comment_id, 'rating');
  endif;

}</code></pre>

Our plugin is still missing one critical thing: the ability to automatically delete the meta data for comments should we need to remove the plugin. We can easily instruct WordPress to delete all of the custom comment meta data with a small snippet of code. We just need to create a new file, <code>uninstall.php</code>, in the same folder as our plugin’s file and add the code below to it. This code will first check whether the plugin’s uninstall command is set to <code>true</code>. If so, it retrieves all of the comments and runs a <code>foreach</code> loop to delete the three meta fields. The uninstall command is initiated only when you delete the plugin through WordPress’ dashboard.

<pre><code class="language-php">&lt;?php
if( !defined( 'ABSPATH') &amp;&amp; !defined('WP_UNINSTALL_PLUGIN') )
    exit();

  $comments = get_comments();
  foreach($comments as $comment) {
    delete_comment_meta($comment-&gt;comment_ID, 'phone');
    delete_comment_meta($comment-&gt;comment_ID, 'title');
    delete_comment_meta($comment-&gt;comment_ID, 'rating');
  }</code></pre>

<a title="8KB ZIP File" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/285b85d7-52ee-47d3-b116-30542a0cf8ca/extendcomment.zip">Download the Extend Comment WordPress Plugin</a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40b4d09f-2253-49fc-a44f-cc299b1ff36d/comment-plugin-example.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40b4d09f-2253-49fc-a44f-cc299b1ff36d/comment-plugin-example.jpg" alt="comment-plugin-example" width="500" height="226" /></a><br>
<em>Screenshot of the Extend Comment plugin installed on the default WordPress theme</em>

## Conclusion

You can find a rating system implemented in the comments area of hosting review pages on <a href="https://webhostingrock.com/reviews/">Web Hosting Rock</a>. It was added directly to the theme to allow for some flexibility and control over the ratings in user comments. We’ve now learned how to use custom meta fields to modify and extend the comment forms in WordPress posts, pages and custom posts. We’ve made use of conditional tags for greater control and customization. And we can restrict these custom fields to certain post types by forcing the functions that add custom input fields to be executed only if the “post type” conditions are met. Now, your comment forms need not be so boring. Add this extra element of fun and interactivity.

{{< signature "al" >}}


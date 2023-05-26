---
title: Powerful WordPress Tips And Tricks
slug: powerful-wordpress-tips-and-tricks
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f087cd46-e188-459b-8568-890811f418e8/illu-wp.jpg'
date: 2013-09-26T08:24:03.000Z
author: daniel-pataki
description: >-
  I’ve been working with WordPress since the dawn of time, and even though I
  peek at the source code regularly, I still discover new tips and tricks. I’ve
  compiled my own list of 21 techniques that are handy, clever, fun or best
  practices rarely followed. I hope everyone finds something new in the list!
categories:
  - WordPress
  - Workflow
  - Techniques
---
I’ve been working with WordPress since the dawn of time, and even though I peek at the source code regularly, I still discover new tips and tricks. I’ve compiled my own list of 21 techniques that are handy, clever, fun or best practices rarely followed. I hope everyone finds something new in the list!

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12554cdf-c22c-4944-b502-dc507b77d8a9/21tips-mini.jpg"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-107026" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07879f14-90c8-496f-ba9b-60b903331a58/21tips-mini-opt.png" alt="21 tips" width="500" height="312" /></a>

## 1\. WordPress Has A Ton Of Built-In Scripts

Using the great <code>wp_enqueue_script()</code> and <code>wp_enqueue_style()</code>, you can include styles and scripts easily with dependency management. But did you know that WordPress has a lot of scripts already built in? jQuery, many elements of jQuery UI, jQuery Form, SWF Object, Tiny MCE, Jcrop and Thickbox are just some the better known ones. The whole list can be <a title="A list of scripts included in WordPress" href="https://codex.wordpress.org/Function_Reference/wp_enqueue_script#Default_scripts_included_with_WordPress">found in the WordPress Codex</a>. If you’re interested in learning how to use the enqueue functions effectively, I recommend “<a title="Script and style management in WordPress" href="https://www.smashingmagazine.com/2011/10/12/developers-guide-conflict-free-javascript-css-wordpress/">The Developer’s Guide to Conflict-Free JavaScript and CSS in WordPress</a>” right here on Smashing Magazine!

## <span class="rh">Further Reading</span> on SmashingMag:

*   <span>[How To Get The Most Out Of A Premium WordPress Theme](https://www.smashingmagazine.com/2013/02/get-the-best-out-of-premium-wordpress-theme/)</span>
*   <span>[Moving A WordPress Website Without Hassle](https://www.smashingmagazine.com/2013/04/moving-wordpress-website/)</span>
*   <span>[WordPress Functions To Make Blogging Easier](https://www.smashingmagazine.com/2013/06/five-wordpress-functions-blogging-easier/)</span>
*   <span>[How To Improve The Deployment Of WordPress Websites](https://www.smashingmagazine.com/2013/04/wordpress-deployment-survey/)</span>

{{% feature-panel %}}

## 2\. Replace Built-In Scripts By Deregistering Them

If you live on the bleeding edge, you can use versions of scripts other than the built-in ones. Using a newer jQuery version is common (though not necessarily good) practice, which can be done in the following way.

<pre><code class="language-php">function my_scripts_method() {
   wp_deregister_script( 'jquery' );
   wp_register_script( 'jquery', get_template_directory_uri() . '/js/jquery-new.js');
   wp_enqueue_script( 'jquery' );
}
add_action('wp_enqueue_scripts', 'my_scripts_method');</code></pre>

But do <em>not</em> do this just to brag about using latest stuff. WordPress includes the version of jQuery that it does to ensure maximum compatibility.

Use another version of jQuery only when encountering compatibility issues, such a plugin that specifically requires it.</p>

## 3\. Force Perfect JPG Images

This is a classic example of why working on a team is beneficial. My good friend Lars told me that WordPress doesn’t use 100% quality for images served on the website, to conserve space and bandwidth. He also showed me a solution, of course:

<pre><code class="language-php">add_filter( 'jpeg_quality', 'smashing_jpeg_quality' );
function smashing_jpeg_quality() {
   return 100;
}</code></pre>

Wordpress uses a default quality of 90%. This is fine in most cases; I doubt many people can see the difference. But if top-notch image quality is a must on your website (for a portfolio, photography, etc.), modifying the value might be best.</p>

## 4\. FeedBurner Redirection

FeedBurner is used on almost every blog that I’ve worked on, and yet I never know how exactly to set it up by heart. Thanks to Elio for writing “<a title="WordPress Optimization Tips" href="https://www.smashingmagazine.com/2011/12/07/10-tips-optimize-wordpress-theme/">10 Tips to Optimize Your WordPress Theme</a>,” which contains this snippet:

<pre><code class="language-php">add_action( 'template_redirect' , 'smashing_rss_redirect');
function smashing_rss_redirect() {
   if ( is_feed() AND !preg_match( '/feedburner|feedvalidator/i', $_SERVER['HTTP_USER_AGENT'] ) ){
      header( 'Location: https://feeds.feedburner.com/my_smashing_feed' );
      header( 'HTTP/1.1 302 Temporary Redirect' );
   }
}</code></pre>

## 5\. Using General Taxonomy Functions

A number of taxonomy functions can handle your custom taxonomies as well as the built-in tags and categories. The Codex’s <a title="WordPress Taxonomy Functions" href="https://codex.wordpress.org/Function_Reference#Category.2C_Tag_and_Taxonomy_Functions">reference of functions</a> contains the full list of taxonomy functions. I particularly like using <code>get_term()</code>, <code>get_terms()</code> and <code>wp_get_object_terms()</code>. To make things more modular, I use these functions as much as I can, even for tags and categories.</p>

## 6\. Setting Up Sessions In WordPress

Sessions are great for storing information between pages and are widely used on websites. WordPress doesn’t use them at all internally, so the session is never set. Using the following method, you can start a session on all pages before any output.

<pre><code class="language-php">add_action( 'init', 'smashing_session_start' );
function smashing_session_start() {
   if ( !session_id() ) {
      session_start();
   }
}</code></pre>

Note that, while sessions are generally pretty safe, implement IP checking or added nonce protection just to be on the safe side. As long as you’re transmitting non-sensitive data, though, you’ll fine. Check out Mark Jaquith’s great <a href="https://markjaquith.wordpress.com/2006/06/02/wordpress-203-nonces/">article on nonces</a> for more info.</p>

## 7\. List All Hooked Functions

I started writing a function to do this. When I did a quick Google search, it turned out that <a title="Listing all hooked functions" href="https://www.wprecipes.com/list-all-hooked-wordpress-functions">WP Recipes had exactly</a> what I needed.

<pre><code class="language-php">function list_hooked_functions($tag=false){
   global $wp_filter;
   if ($tag) {
      $hook[$tag]=$wp_filter[$tag];
      if (!is_array($hook[$tag])) {
         trigger_error("Nothing found for '$tag' hook", E_USER_WARNING);
         return;
      }
   }
   else {
      $hook=$wp_filter;
      ksort($hook);
   }

   echo '&lt;pre&gt;';

   foreach($hook as $tag =&gt; $priority){
      echo "&lt;br /&gt;&amp;gt;&amp;gt;&amp;gt;&amp;gt;&amp;gt;t&lt;strong&gt;$tag&lt;/strong&gt;&lt;br /&gt;";
      ksort($priority);
      foreach($priority as $priority =&gt; $function){
         echo $priority;
         foreach($function as $name =&gt; $properties) {
            echo "t$name&lt;br /&gt;";
         }
      }
   }
   echo '&lt;/pre&gt;';
   return;
}</code></pre>

Used without an argument, you’ll get a nice list of all hooked functions. This will be a bit long, so you can specify a hook to narrow the list a bit. This is particularly useful when debugging or fiddling around with hook priorities. Knowing what’s hooked into <code>wp_head()</code> in what order is important, and this function is a great asset!

## 8\. Automatically Add Paragraph Tags To Anything

WordPress does this automatically to the content and the excerpt, but there’s no reason not to use it elsewhere. The function responsible for turning double line breaks into paragraphs is <a title="Automatic paragraph tags in WordPress" href="https://codex.wordpress.org/Function_Reference/wpautop"><code>wpautop()</code></a>.

<pre><code class="language-php">$my_text = 'Welcome!
Smashing Magazine is a great place to learn new things.
I hope you’re having a nice time!';

echo wpautop( $my_text );</code></pre>

Sometimes you’ll want to disable this filter by default, which you can do by removing it from the content and excerpt, like so:

<pre><code class="language-php">remove_filter( 'the_content', 'wpautop' );
remove_filter( 'the_excerpt', 'wpautop' );</code></pre>

## 9\. Send Emails Using WordPress

A little while back, I wrote a long article on “<a title="Using the WordPress mail function" href="https://www.smashingmagazine.com/2011/10/25/create-perfect-emails-wordpress-website/">Creating Perfect Emails for Your WordPress Website</a>,” a part of which has to do with using the <code>wp_mail()</code> functions. These functions let you use built-in WordPress awesomeness to send emails to users.

<pre><code class="language-php">$message = 'Hello, thanks for reading my post! I hope to see you back soon.';
wp_mail( 'someonesemail@example.com', 'Thanks for reading my post!', $message);</code></pre>

You can also send HTML content by using a filter:

<pre><code class="language-php">add_filter ("wp_mail_content_type", "smashing_mail_content_type");
function smashing_mail_content_type() {
   return "text/html";
}</code></pre>

## 10\. Native Pagination Links

It came as a surprise to me about six months ago that you don’t need any plugins to pull off proper paging (i.e. not just “Previous” and “Next” links); you can do it with a native function. The <code>paginate_links()</code> function is a handy little thing that lets you show pagination for any type of content, not just a WordPress loop.

<pre><code class="language-php">// Pagination for a WordPress loop
$list = new WP_Query( $query_args );
$pagination = array(
   'base'       =&gt; str_replace( 99999, '%#%', get_pagenum_link( 99999 ) ),
   'format'     =&gt; '?paged=%#%',
   'current'    =&gt; max( 1, get_query_var( 'paged' ) ),
   'total'      =&gt; $list-&gt;max_num_pages,
   'next_text'  =&gt; 'next',
   'prev_text'  =&gt; 'previous'
);
echo '&lt;div class="pagination primary-links"&gt;' . paginate_links( $pagination ) . '&lt;/div&gt;';

// Pagination for anything
$list = range(1, 100);
$items_per_page = 12;
$pagination = array(
   'base'       =&gt; get_bloginfo( 'url' ) . '/mypage/%_%',
   'format'     =&gt; '?paged=%#%',
   'current'    =&gt; $_GET['current_page'],
   'total'      =&gt; ceil( max($list) / $items_per_page ),
   'next_text'  =&gt; 'go forth',
   'prev_text'  =&gt; 'go back'
);
echo '&lt;div class="pagination primary-links"&gt;' . paginate_links( $pagination ) . '&lt;/div&gt;';</code></pre>

## 11\. Upload Files With Ease

WordPress has a bunch of great uploading functions for everything from checking the file type to finding the uploads directory. A more obscure function is <a title="WordPress upload function" href="https://codex.wordpress.org/Function_Reference/wp_upload_bits"><code>wp_upload_bits()</code></a>, which you can use to upload a file to the uploads directory.

<pre><code class="language-php">$upload = wp_upload_bits( $_FILES['myfile']['name'], null, file_get_contents( $_FILES['myfile']['tmp_name'] ) );
echo 'Well uploaded! The path to this file is ' . $upload['file'] . ' and the url to this file is ' . $upload['url'];</code></pre>

## 12\. Twitter-Like Time Display

This was another shock to me a while back, especially since it has been in WordPress since version 1.5! If you’d like to show viewers a relative date in a human-readable format, like “5 minutes ago” or “one month ago,” try the <a title="Human Time difference function in WordPress" href="https://codex.wordpress.org/Function_Reference/human_time_diff"><code>human_timed_diff()</code></a> function.

<pre><code class="language-php">$diff = human_time_diff( '2012-05-05 12:05:00', '2012-05-05 12:10:00' );
echo 'This comment was submitted ' . $diff . 'ago';

// Output: This comment was submitted 5 minutes ago</code></pre>

## 13\. Log In As Any User

If you’re building a complex website with many roles, being able to switch between them quickly and easily would be useful. The <a title="Log in a user based on ID in WordPress" href="https://codex.wordpress.org/Function_Reference/wp_set_auth_cookie"><code>wp_set_auth_cookie()</code></a> lets you log the current user in based on ID.

<pre><code class="language-php">$user_id = 4;
   wp_set_auth_cookie( $user_id );</code></pre>

Take great care when using this function; left unchecked, it could log every user in as user number 4. Even while testing, I target it specifically to my IP, and maybe even to a special URL string just to be sure. That said, with proper safety, it can be used as part of a custom log-in script.</p>

## 14\. Add Custom Profile Fields In The Admin Area

I can’t say that WordPress offers much in the way of profile customization in the administration area. Especially nowadays, when you want to show the Twitter and other social accounts of authors, this is a shortcoming. It can be fixed easily, though. Have a look here:

<pre><code class="language-php">&lt;?php
add_action( 'show_user_profile', 'smashing_profile_fields' );
add_action( 'edit_user_profile', 'smashing_profile_fields' );

function smashing_profile_fields( $user ) { 
?&gt;

   &lt;h3&gt;Social Sites&lt;/h3&gt;

   &lt;table class="form-table"&gt;

      &lt;tr&gt;
         &lt;th&gt;&lt;label for="twitter"&gt;Twitter&lt;/label&gt;&lt;/th&gt;

         &lt;td&gt;
            &lt;input type="text" name="twitter" id="twitter" value="&lt;?php echo esc_attr( get_the_author_meta( 'twitter', $user-&gt;ID ) ); ?&gt;" /&gt;&lt;br /&gt;
            &lt;span class="description"&gt;Your Twitter Username&lt;/span&gt;
         &lt;/td&gt;
      &lt;/tr&gt;

      &lt;tr&gt;
         &lt;th&gt;&lt;label for="twitter"&gt;Facebook&lt;/label&gt;&lt;/th&gt;

         &lt;td&gt;
            &lt;input type="text" name="facebook" id="facebook" value="&lt;?php echo esc_attr( get_the_author_meta( 'facebook', $user-&gt;ID ) ); ?&gt;" /&gt;&lt;br /&gt;
            &lt;span class="description"&gt;Your Facebook Profile URL&lt;/span&gt;
         &lt;/td&gt;
      &lt;/tr&gt;

      &lt;tr&gt;
         &lt;th&gt;&lt;label for="twitter"&gt;Linkedin&lt;/label&gt;&lt;/th&gt;

         &lt;td&gt;
            &lt;input type="text" name="linkedin" id="linkedin" value="&lt;?php echo esc_attr( get_the_author_meta( 'linkedin', $user-&gt;ID ) ); ?&gt;" /&gt;&lt;br /&gt;
            &lt;span class="description"&gt;Your Linkedin Profile URL&lt;/span&gt;
         &lt;/td&gt;
      &lt;/tr&gt;

   &lt;/table&gt;

&lt;?php
}
add_action( 'personal_options_update', 'smashing_save_profile_fields' );
add_action( 'edit_user_profile_update', 'smashing_save_profile_fields' );

function smashing_save_profile_fields( $user_id ) {
   if ( !current_user_can( 'edit_user', $user_id ) )
      return false;

   update_user_meta( $user_id, 'twitter', $_POST['twitter'] );
   update_user_meta( $user_id, 'facebook', $_POST['facebook'] );
   update_user_meta( $user_id, 'linkedin', $_POST['linkedin'] );
}</code></pre>

## 15\. Sanitize URLs With Ease

When working with URLs, always make sure they are properly formed and don’t contain any invalid or dangerous characters. The <a title="Esacaping URLs in WordPress" href="https://codex.wordpress.org/Function_Reference/esc_url">esc_url()</a> function lets you do just that.

<pre><code class="language-php">$my_url = 'https://mypage.com/?awesome=true';
   $url = esc_url( $my_url );</code></pre>

Be sure to check out all of the other escape functions. You can find a list of them at the bottom of the page that I linked to in the related section.</p>

## 16\. Empower Text Widgets

To make text widgets so much better, you can enable the use of shortcodes in them. This is a great tool for theme developers because it makes your product much more flexible for the user.

<pre><code class="language-php">add_filter( 'widget_text', 'do_shortcode' );</code></pre>

## 17\. Add Custom Post Types To The RSS Feed

Not being able to do this easily from the admin area is a big issue. Many website owners separate their content into custom posts, and they also want all of their items to show up in the feeds. Never fear — a function is here!

<pre><code class="language-php">add_filter('request', 'smashing_custom_feed');
function smashing_custom_feed( $vars ) {
   if ( isset( $vars['feed'] ) ) {
      $vars['post_type'] = get_post_types();
   }
   return $vars;
}</code></pre>

While this is great, it forces all of your post types into the feed. If you’d like to add just some of your custom post types to the feed, you can list them separately.

<pre><code class="language-php">add_filter('request', 'smashing_custom_feed');

$post_type_list = array( 'post', 'products' );
function smashing_custom_feed( $vars ) {
   if ( isset( $vars['feed'] ) AND !isset( $vars['post_type'] ) ) {
      $vars['post_type'] = $post_type_list;
   }
   return $vars;
}</code></pre>

## 18\. Don’t Break WordPress Loops

Multiple loops are great but can wreak havoc if not used correctly. To make sure your loop runs smoothly and you can still use all of the functions that rely on globals, store the original query in a temporary variable.

<pre><code class="language-php">$tmp_query = $wp_query;
query_posts('cat=5&amp;order=ASC');
while( have_posts() ) : the_post() 
?&gt;
   &lt;a href="&lt;?php the_permalink() ?&gt;'&gt;&lt;?php the_title() ?&gt;&lt;/a&gt;&lt;br /&gt;
&lt;?php
$wp_query = $tmp_query;</code></pre>

## 19\. Custom Database Queries

If you need something more than what the default WordPress functions give you, you can use <a title="The WordPress Database Class" href="https://codex.wordpress.org/Class_Reference/wpdb"><code>$wpdb</code></a>, the WordPress database class to query the database directly.

<pre><code class="language-php">$recent_users = $wpdb-&gt;get_results( "SELECT display_name, user_registered FROM $wpdb-&gt;users ORDER BY user_registered DESC LIMIT 0,10" );</code></pre>

This class has great features and functions. Take a look at “<a title="How to query the WordPress Database" href="https://www.smashingmagazine.com/2011/09/21/interacting-with-the-wordpress-database/">Interacting With the WordPress Database</a>” for an in-depth tutorial.</p>

## 20\. Customize WordPress Post Revisions

The post revisions feature in WordPress is great, but the majority of users don’t use it. Database entries are created for revisions, even if they are not used. While they’re not a huge hit on your server’s performance, if you don’t use revisions, you can disable them by placing the following code in your <code>wp-config.php</code> file.

<pre><code class="language-php">// To remove revisions
define( 'WP_POST_REVISIONS', FALSE );

// To limit them
define( 'WP_POST_REVISIONS', 5 );</code></pre>

## 20\. Styling Author Comments

If you’d like author comments to jump out, simply use the <code>bypostauthor</code> class in your CSS.

<pre><code class="language-css">li.bypostauthor {
   background:#fafafa;
   color:#555;
}</code></pre>

## 21\. Storing Your Whole Page In A Variable

In some cases, storing your whole output in a variable can be very helpful. This allows you to make global changes, compress or obfuscate code and more very easily. All we need is PHP output buffering and two hooks.

<pre><code class="language-php">add_action('wp_head', 'smashing_buffer_start');
add_action('wp_footer', 'smashing_buffer_end');

function smashing_buffer_start() {
   ob_start( 'smashing_callback' );
}

function buffer_end() {
   ob_end_flush();
}

function smashing_callback( $content ) {
   // Feel free to do things to the content here
   $content = str_replace( 'great', 'awesome', $content );
   echo $content;
}</code></pre>

## And The List Goes On

Do you have any favorite WordPress tips and tricks or best practices that you wish were followed more? Please do share in the comments so that we can all learn something new!

<em>(al) (ea)</em>


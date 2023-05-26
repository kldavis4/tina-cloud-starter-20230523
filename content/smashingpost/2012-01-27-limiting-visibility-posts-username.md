---
title: Limiting The Visibility Of Posts In WordPress Via Usernames
slug: limiting-visibility-posts-username
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1831c77-31cd-41ee-9de0-2a3867a7940c/wordpress-11.png
date: 2012-01-27T13:45:50.000Z
author: chris-ellison
description: >-
  Controlling who is able to view a post is a simple task once the system is established. Limiting access to certain users has several advantages, ranging from a design studio distributing artwork among various clients, or a small school arranging to have its students' homework posted online through a cheap and easy solution.
categories:
  - WordPress
  - Custom Fields
  - Functions
---
The easiest method to get this system working is to make the recipients of the information “subscribers” (since they need not be able to post) and the distributors of information “authors” (since they should only be able to edit their own posts). This system eliminates several headaches for the website owner by <strong>managing who has access to particular posts</strong>. The username would be used to identify who is allowed to view certain posts, since it is unique and, for the most part, constant.</p>

## The Basics

### What Will You Need?

*   WordPress 3.1 or later
*   Members of various roles
*   The ability to modify your theme's files
*   Basic knowledge of PHP and MySQL

{{% feature-panel %}}

### What Is a Username?

In general, a username is a means by which to identify and verify a user. It is not the only way to identify a user, but remembering a username is easier for the person logging in than having to remember a random user ID. A username can be made unique to an individual, unlike a person's name or email address (family members may share the same name, or even the same email address). This ease of use and uniqueness is why usernames are used on most websites that require people to sign up in order to access the website or certain of its features.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Utilizing User Roles In WordPress](https://www.smashingmagazine.com/2012/10/utilizing-user-roles-wordpress/)
*   <span>[How To Become A Top WordPress Professional](https://www.smashingmagazine.com/2012/12/become-top-wordpress-professional/)</span>
*   <span>[Useful WordPress Tools, Themes And Plugins](https://www.smashingmagazine.com/2012/03/useful-wordpress-tools-themes-plugins/)</span>
*   [Creating Mobile-Optimized Websites Using WordPress](https://www.smashingmagazine.com/2012/05/creating-mobile-optimized-websites-using-wordpress/)

To WordPress, a username is means of identifying a user. Paired with a password, a username enables someone to access their profile and, depending on their permissions within WordPress, to access to the administrative pages of the website. A username can be used for many functions in the operation and management of a website, such as karma, prestige, user roles and expulsion.

A WordPress username is unique and impossible for the average user to change. Thus, the system is a potentially reliable means of identifying individuals. This reliability is important for a system in which a post must be visible to only a few people. The permissions of a post should not alter merely because someone has changed their name or email address.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04d049c6-6438-4333-876d-e89f9d35a5e0/lpvuau-1-full1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70879bf0-c33b-4b03-aad1-b57b8cf84520/lpvuau-1-screenshot.jpg" alt="Screenshot of a WordPress single user page" width="500" height="39" /></a><br>
<em>The user page in a WordPress installation. Note that “Usernames cannot be changed.”</em>

## Setting Up The Back End

In order for an author to be able to set permissions for visibility, a method of selecting users must be set up on the post editing page. We could accomplish this by one of several methods, one of the easiest and most efficient of which is to create a meta box (or widget) in the post editing page that allows the author to add custom information, as required by a theme or plugin. This information enables us to tell the theme which members should have viewing rights to particular posts.</p>

### A Basic Custom Meta Box

Justin Tadlock’s article “<a title="How To Create Custom Post Meta Boxes In WordPress" href="https://www.smashingmagazine.com/2011/10/04/create-custom-post-meta-boxes-wordpress/">How to Create Custom Post Meta Boxes in WordPress</a>” explains how to create meta boxes, and we’ll reuse that code here.

Let’s assume we’re dealing with a website for a music school named “Smashing Magazine’s Fancy Flautists.” We will use the name <code>smashing_flautist_access</code> in the code for the back end to distinguish it from other custom functions. Justin's code is a great starting point for this project, but it needs a little customization for our purpose. Place the following code in your theme's <code>functions.php</code>, and modify the various labels according to your project.

<pre><code class="language-php">/* Fire our meta box setup function on the post editor screen. */
add_action( 'load-post.php', 'smashing_post_meta_boxes_setup' );
add_action( 'load-post-new.php', 'smashing_post_meta_boxes_setup' );

/* Meta box setup function. */
function smashing_post_meta_boxes_setup() {

   /* Add meta boxes on the 'add_meta_boxes' hook. */
   add_action( 'add_meta_boxes', 'smashing_add_post_meta_boxes' );

   /* Save post meta on the 'save_post' hook. */
   add_action( 'save_post', 'smashing_flautist_access_save_meta', 10, 2 );
}

/* Create one or more meta boxes to be displayed on the post editor screen. */
function smashing_add_post_meta_boxes() {

   add_meta_box(
      'smashing-flautist-access',         // Unique ID
      esc_html__( 'Post Viewing Permission', 'smashing_flautist' ),     // Title
      'smashing_flautist_access_meta_box',      // Callback function
      'post',              // Admin page (or post type)
      'normal',               // Context
      'default'               // Priority
   );
}

/* Display the post meta box. */
function smashing_flautist_access_meta_box( $object, $box ) { ?&gt;

   &lt;?php wp_nonce_field( basename( __FILE__ ), 'smashing_flautist_access_nonce' ); ?&gt;

   &lt;p&gt;
      &lt;label for="smashing-flautist-access"&gt;&lt;?php _e( "Enter the username of the subscriber that you want to view this content.", 'smashing_flautist' ); ?&gt;&lt;/label&gt;
      &lt;br /&gt;
      &lt;input class="widefat" type="text" name="smashing-flautist-access" id="smashing-flautist-access" value="&lt;?php echo esc_attr( get_post_meta( $object-&gt;ID, 'smashing_flautist_access', true ) ); ?&gt;" size="30" /&gt;
   &lt;/p&gt;
&lt;?php }</code></pre>

With Justin’s code, modified for this project, we should have a custom meta box that looks like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1fdb4a6-e304-423d-9ccf-55de45c20495/lpvuau-2-full1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f136b424-0e6b-4b7d-a57d-b89e62d63df3/lpvuau-2-screenshot.jpg" alt="Screenshot of a basic meta box" width="500" height="58" /></a><br>
<em>A basic meta box positioned below the post editing box.</em>

### Adding Ease to the Selection

This box can be used as is, and the author would simply input the members who they want to allow to view a post. This would work well if each author had very few usernames to remember; but if the author has long list of usernames to choose from, then a list of members would have to be displayed, and there would have to be a system that allows the authors to choose members from the list. Add the following code to the area just below the original box, just after the closing paragraph tag, to display a list of users with their names, along with radio buttons to grant one of the users access to the current post.

<pre><code class="language-php">&lt;table class="smashing-flautist-access"&gt;
&lt;tr align="left"&gt;
&lt;th&gt;Username&lt;/th&gt;
&lt;th&gt;    &lt;/th&gt;
&lt;th&gt;Visiblity&lt;/th&gt;
&lt;th&gt;    &lt;/th&gt;
&lt;th&gt;Name&lt;/th&gt;
&lt;/tr&gt;
&lt;?php
global $post;
   $users = get_users('role=subscriber');
   foreach ($users as $user) {
         $user_info = get_userdata( $user-&gt;ID );
         if(get_post_meta( $object-&gt;ID, 'smashing_flautist_access', true ) == $user-&gt;user_login) $ifchecked = 'checked="checked" ';
         echo "&lt;tr&gt;";
         echo "&lt;td&gt;$user-&gt;user_login&lt;/td&gt;&lt;td&gt;    &lt;/td&gt;";
         echo "&lt;td align="center"&gt;&lt;input type="radio" name="smashing-flautist-access" id="smashing-flautist-access" value="$user-&gt;user_login" " . $ifchecked ."/&gt;&lt;/td&gt;&lt;td&gt;    &lt;/td&gt;";
         echo "&lt;td&gt;$user_info-&gt;last_name, $user_info-&gt;first_name&lt;/td&gt;&lt;td&gt;    &lt;/td&gt;";
         echo "&lt;/tr&gt;";
         unset($ifchecked);

   } ?&gt;&lt;/table&gt;</code></pre>

If everything goes well, you should end up with a box underneath the post editor that looks similar to the image below. The form containing the radio buttons gets a list of users that are listed as subscribers and makes the selection of the student with viewing permissions easy, all without the post's author having to remember any usernames.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4456bd27-c812-4b89-b510-41da58790765/lpvuau-3-full1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e973ed9-d8e1-4ed0-82c4-cb2ebd13c127/lpvuau-3-screenshot.jpg" alt="Screenshot of a meta box with user information" width="500" height="214" /></a><br>
<em>A meta box that contains a method to select the particular name and information of each user.</em>

### Saving the List

Now that we have generated a list that makes it easy for the authors to pick which members they want to be able to view particular posts, we have to create a system to add the list to WordPress’ MySQL database so that we can retrieve it later. We also need a way to tell WordPress to update this list of usernames in case the author decides later to add or remove someone from a particular post's list of authorized viewers. The code provided by Justin does excellent work; place his code below in your theme's <code>functions.php</code>, just after the function that sets up the custom meta box.

<pre><code class="language-php">/* Save post meta on the 'save_post' hook. */
add_action( 'save_post', 'smashing_flautist_access_save_meta', 10, 2 );

/* Save the meta box's post metadata. */
function smashing_flautist_access_save_meta( $post_id, $post ) {

   /* Make all $wpdb references within this function refer to this variable */
   global $wpdb;

   /* Verify the nonce before proceeding. */
   if ( !isset( $_POST['smashing_flautist_access_nonce'] ) || !wp_verify_nonce( $_POST['smashing_flautist_access_nonce'], basename( __FILE__ ) ) )
      return $post_id;

   /* Get the post type object. */
   $post_type = get_post_type_object( $post-&gt;post_type );

   /* Check if the current user has permission to edit the post. */
   if ( !current_user_can( $post_type-&gt;cap-&gt;edit_post, $post_id ) )
      return $post_id;

   /* Get the posted data and sanitize it for use as an HTML class. */
   $new_meta_value = ( isset( $_POST['smashing-flautist-access'] ) ? sanitize_html_class( $_POST['smashing-flautist-access'] ) : ’ );

   /* Get the meta key. */
   $meta_key = 'smashing_flautist_access';

   /* Get the meta value of the custom field key. */
   $meta_value = get_post_meta( $post_id, $meta_key, true );

   /* If a new meta value was added and there was no previous value, add it. */
   if ( $new_meta_value &amp;&amp; ’ == $meta_value )
      {
      add_post_meta( $post_id, $meta_key, $new_meta_value, true );
      $wpdb-&gt;query($wpdb-&gt;prepare("UPDATE $wpdb-&gt;posts SET post_status = 'private' WHERE ID = ".$post_id." AND post_type ='post'"));
      }
   /* If the new meta value does not match the old value, update it. */
   elseif ( $new_meta_value &amp;&amp; $new_meta_value != $meta_value )
      {
      update_post_meta( $post_id, $meta_key, $new_meta_value );
      $wpdb-&gt;query($wpdb-&gt;prepare("UPDATE $wpdb-&gt;posts SET post_status = 'private' WHERE ID = ".$post_id." AND post_type ='post'"));
      }
   /* If there is no new meta value but an old value exists, delete it. */
   elseif ( ’ == $new_meta_value &amp;&amp; $meta_value )
      {
      delete_post_meta( $post_id, $meta_key, $meta_value );
      $wpdb-&gt;query($wpdb-&gt;prepare("UPDATE $wpdb-&gt;posts SET post_status = 'public' WHERE ID = ".$post_id." AND post_type ='post'"));
      }
}</code></pre>

The three MySQL queries are in place to prevent unauthorized users from viewing protected posts and to hide the posts from the RSS feeds. The first query runs only when new data populates the previously empty custom field, while the second query runs only when the data in the custom field has changed. The third query runs only if the custom field is emptied, and it sets the post’s visibility back to “Public.” All three are protected from SQL injection attacks by using <code>$wpdb-&gt;prepare()</code> to validate the data entered into the username form field.

If you don’t like that WordPress precedes the post’s title with the word “Private,” then add the following code to your theme's <code>functions.php</code> file. This custom function is called when your theme would display a post's title; it finds any instance of the words “Protected” or “Private” at the beginning of the title and removes them. In the core of WordPress’ programming, the function <code>get_the_title()</code> adds those words if a post's visibility is restricted and the person viewing is not an administrator. What the following code does is send a message to the action that <code>get_the_title()</code> hooks into, telling it to remove the terms “Protected: ” and “Private: ” from the title. So, you can set a post's title to begin with either term, and the title will not be altered; this code only affects WordPress' ability to add to your title.

<pre><code class="language-php">function smashing_title_trim($title) {
   $title = attribute_escape($title);
   $needles = array(__('Protected: '),__('Private: '));
   $title = str_replace($needles,’,$title);
   return $title;
}
add_filter('protected_title_format','smashing_title_trim');
add_filter('private_title_format','smashing_title_trim');</code></pre>

To allow users at the subscriber level to see private posts, you have to give them that capability. As it happens, some of the code we’ll be using later frees us from having to worry about users at the subscriber level seeing the posts of others.

<pre><code class="language-php">$subRole = get_role( 'subscriber' );
$subRole-&gt;add_cap( 'read_private_posts' );</code></pre>

You can also grant users at the subscriber level permission to view private pages, in case you want a dedicated page of information that subscribers should know.

<pre><code class="language-php">$subRole-&gt;add_cap( 'read_private_pages' );</code></pre>

## Setting Up The Front End

Now that we have a way to add members to the list of people who can view a particular post, we have to modify our theme to use this data, and to actually control the visibility of each post based on this list. First, we need a way to get the username of the person who can view a post. Secondly, we would compare the username of the member with viewing permissions to the user who is currently logged in. Finally, we would make the theme display either the post in the loop or an error message (or perhaps nothing at all).

Place this code just after <a title="The Loop" href="https://codex.wordpress.org/The_Loop">The Loop</a> starts. It goes in <code>single.php</code>, <code>category.php</code> and <code>index.php</code> if you will be displaying posts on the home page.

<pre><code class="language-php">&lt;?php
/* Get the post's acceptable viewer. */
      $flautist_access = get_post_meta($post-&gt;ID, 'smashing_flautist_access', true );
/* Get the post's current viewer, if he or she is logged in. */
      if(is_user_logged_in()) {$current_flautist = $current_user-&gt;user_login;}
/* See if the acceptable viewer and the current viewer are the same */
      if($flautist_access == $current_flautist || current_user_can('author') || current_user_can('editor') || current_user_can('administrator'))
         {echo ’; ?&gt;</code></pre>

Place this code just before the loop ends. Here is where you can show an error message telling the user that they may not view this post. Or you could leave this code as is to make it appear as though the current visitor is not missing anything.

<pre><code class="language-php">&lt;?php } else { echo ’; } ?&gt;</code></pre>

This is what a hidden post looks like to the public or to a user who is not logged in. They would see what appears to be an error message and are redirected away from the post.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c78d941-36d5-4fb5-8be7-4a9fbffcd098/lpvuau-4-full.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3ea6b82-cfed-423f-aa71-cb61b46936ad/lpvuau-4-screenshot.jpg" alt="What the public sees when trying to view a protected post" width="500" /></a><br>
<em>If a person is not logged in and tries to view a restricted post, they would get an error message.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a71aebe2-fea1-405d-b00d-b1f551611d54/lpvuau-5-full.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b2138d5-e82b-465b-b608-29b45b2c87f1/lpvuau-5-screenshot.jpg" alt="What an unauthorized user sees when trying to view a protected post" width="500" /></a><br>
<em>If a user is logged in but not allowed to view a restricted post, they would see either nothing or an error message specific to members.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8979829-e8c5-45b1-a425-04abad3ea552/lpvuau-6-full.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a57ba83b-f2c6-4644-b9dc-21f1f27ff01e/lpvuau-6-screenshot.jpg" alt="What an authorized user sees when trying to view a protected post" width="500" /></a><br>
<em>If a member is logged in and authorized to view a protected post, then they would see the post itself.</em>

## Conclusion

Being able to control who can view individual posts is a useful feature with a wide variety of applications. Third-party software can natively do this, but WordPress is widely supported and documented, which means that any security holes that might allow unauthorized users to view restricted posts would be shut in a future update. Plus, it allows you to run an actual blog next to posts with limited visibility. This system could be used by administrators to distribute personalized content, by professionals to send files to clients, or by bloggers to restrict the visibility of certain posts to certain members.

Enabling an author to control who can view their posts can help them tailor the blog's content to the needs or tastes of certain users. Ultimately, you will have to factor in the <strong>purpose and content of your website when deciding whether to use this method</strong>. It’s not for everyone, but it suit the needs of owners of small websites who want to deliver certain content to certain people.</p>

### Resources

*   “[Function Reference/add meta box](https://codex.wordpress.org/Function_Reference/add_meta_box),” WordPress Codex
*   “[Function Reference/get users](https://codex.wordpress.org/Function_Reference/get_users),” WordPress Codex
*   “[Roles and Capabilities](https://codex.wordpress.org/Roles_and_Capabilities),” WordPress Codex
*   “[Class Reference/wpdb](https://codex.wordpress.org/Class_Reference/wpdb#Protect_Queries_Against_SQL_Injection_Attacks),” WordPress Codex
*   “[How To Create Custom Post Meta Boxes In WordPress](https://www.smashingmagazine.com/2011/10/04/create-custom-post-meta-boxes-wordpress/),” Justin Tadlock

{{< signature "al" >}}


---
title: Utilizing User Roles In WordPress
slug: utilizing-user-roles-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32cfb9b6-0951-454f-a4b7-b5395102747e/red-user.jpg
date: 2012-10-25T19:00:43.000Z
author: daniel-pataki
description: >-
  Roles have been an integral part of WordPress for quite some time now — many
  functions associated with managing them have been in place since version
  2.0.0\. Despite this longevity, they are rarely utilized which is a shame
  since they allow for the easy setup of custom user types (and also have the
  ability to micro-manage them). In this article, you'll learn everything you
  need to utilize user roles in WordPress and make the most of this incredible
  built-in functionality.
categories:
  - WordPress
  - Admin
  - Techniques (WP)
---
Roles have been an integral part of WordPress for quite some time now — many functions associated with managing them have been in place since version 2.0.0. Despite this longevity, they are rarely utilized which is a shame since they allow for the easy setup of custom user types (and also have the ability to micro-manage them). In this article, you'll learn everything you need to utilize user roles in WordPress and make the most of this incredible built-in functionality.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec660abe-c543-4a12-b44b-313ddd49e5a3/rolemananagement.jpg"><img class="aligncenter size-full wp-image-106577" title="Role Mananagement" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec660abe-c543-4a12-b44b-313ddd49e5a3/rolemananagement.jpg" alt="" width="753" height="400" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec660abe-c543-4a12-b44b-313ddd49e5a3/rolemananagement.jpg">Large view</a>.</em>

## Terminology

The main terms to know are "role" and "capability". <strong>Capabilities</strong> are the core of the system, they represent the <em>things you can do</em>. An example of a capability is <code>switch_themes</code>. A user who has this capability is able to change the look of the website using the Appearances section in the admin. Those who do not have this capability will not be able to do so.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   <span>[Manage Events Like A Pro With WordPress](https://www.smashingmagazine.com/2012/04/manage-events-like-pro-with-wordpress/)</span>
*   <span>[Writing Effective Documentation For WordPress End Users](https://www.smashingmagazine.com/2012/07/writing-effective-wordpress-documentation/)</span>
*   [Random Redirection In WordPress](https://www.smashingmagazine.com/2012/04/random-redirection-in-wordpress/)
*   <span>[Do-It-Yourself Caching Methods With WordPress](https://www.smashingmagazine.com/2012/06/diy-caching-methods-wordpress/)</span>

{{% feature-panel %}}

<strong>Roles</strong> are simply a named set of capabilities. Imagine you have capabilities like <code>edit_post</code>, <code>add_user</code> and so on. Instead of listing all 50 of them for each and every user who you'd like to be an admin, simply assign each user the "admin" role and then assign all the capabilities to that role.</p>

## The Default Setup

By default, WordPress has six roles and about 57 capabilities. Each role has a different combination of capabilities which endow the user with the appropriate rights and privileges.

For example, a contributor can edit and delete his own posts, but cannot control when these posts are published (and cannot delete those posts once they are published). This is because they have the <code>edit_posts</code> and <code>delete_posts</code> capabilities, but they do <strong>not</strong> have the <code>publish_post</code> and <code>delete_published_post</code> capabilities.

The <a href="https://codex.wordpress.org/Roles_and_Capabilities#Roles">default setup</a> offered by WordPress is very well thought out and should not be modified, only added to. If it is changed, you could face difficult problems later on — like a contributor being able to remove posts from your website, or an admin not being able to change the theme.</p>

## When New Roles And Capabilities Are Needed

New roles usually come hand-in-hand with new capabilities. Usually, we first create a set of new capabilities, which are held by the admin (and a new role, as well). Let's look at an example.

If you have a large website, chances are you have a marketing team. This team doesn't need to be able to edit and publish posts, but they do need access to advertising stats, trending search topics, etc. Perhaps it would also be beneficial to <strong>allow them to manage categories and comments</strong> for SEO purposes and customer satisfaction, respectively.

Our first order of business is to look at the advertising stats and trending searches. This is not something WordPress offers by default, so let's presume it has been built as a plugin. Let's create a capability called <code>view_stats</code>. This will be given to the marketing people and of course to the admin. Other users — like editors and authors — do not need to see the stats (which, in many case, is sensitive data) so they will not receive this capability.

Our second task is to decide what other capabilities our marketing people need. Based on our assumptions above, they will need the <code>read</code>, <code>manage_links</code>, <code>manage_categories</code> and <code>moderate_comments</code> capabilities.

Lastly, we would use some coding chops to create a new role named “Marketing”, and assign the above-mentioned capabilities to it. Once that has been done, we are able to appoint the “Marketing” role to any user within the “Add User” and “Edit Profile” page.</p>

## Basic WordPress Functions

To manage roles and capabilities effectively, all you need is five very straightforward functions:

*   `add_role()` — Enables you to add a custom role
*   `remove_role()` — Enables you to remove a custom role
*   `add_cap()` — Enables you to add a custom capability to a role
*   `remove_cap()` — Enables you to remove a custom capability from a role
*   `get_role()` — Gets information about a role as well as associated capabilities

If you would like to view the documentation for these functions, you can take a look at the <a href="https://codex.wordpress.org/Roles_and_Capabilities#Resources">Roles and Capabilities</a> section in the Codex.</p>

## Implementing New Roles And Capabilities

The full implementation of roles and capabilities requires more than just the five functions I mentioned. We'll also need to use functions for checking capabilities, we'll need features which are only available to certain roles, and so on.</p>

### Adding the Roles and Capabilities

<pre><code class="language-php">
$marketing = add_role( 'marketing', 'Marketing', array(
    'read' =&gt; true,
    'manage_links', 
    'manage_categories', 
    'moderate_comments',
    'view-stats'
));

$role = get_role( 'administrator' );
$role-&gt;add_cap( 'view-stats' );  
</code></pre>

The function above will add our new "Marketing" role. It adds four capabilities which are already included in WordPress and a fifth one which is a custom capability. As you can see, no special coding is required to add custom caps — just include them in the array when adding the role. Once we add the new role, we make sure to add our new capability to the admin role as well.

Note that the <code>add_role()</code> fuction returns a <code>WP_Role</code> object on success or <code>NULL</code> if the role already exists.

Since the above code will be used in a plugin, the best way to use it is to utilize hooks, and to add the capabilities to the administrator only when we first create the role.

<pre></pre>

add_action( 'admin_init', 'add_custom_role' );

function add_custom_role() {
$marketing = add_role( 'marketing', 'Marketing', array(
'read' =&gt; true,
'manage_links',
'manage_categories',
'moderate_comments',
'view-stats'
));

if( null !== $marketing ) {
$role = get_role( 'administrator' );
$role-&gt;add_cap( 'view-stats' );
}
}

### Checking for Capabilities and Roles

Once we have our system in place we can check for capabilities and roles. This allows us to make sure that only users with the right capabilities can do certain things.

<pre><code class="language-php">
add_action('admin_menu', 'register_stats_Page');

function register_stats_Page() {
    add_menu_page( 'Marketing Info', 'Marketing Info', 'view_stats', 'marketing-info', 'show_marketing_info' );
}

function show_marketing_info(){
   if( ! current_user_can( 'view-stats' ) ) {
      die( 'You are not allowed to view this page' );
   }
   echo "
This is the marketing stats page
"; 
}  
</code></pre>

The code above will add a top level menu to the admin area for our marketing stats page. The <code>add_menu_page()</code> function allows you to specify a capability (the third argument) which determines whether or not the menu is shown.

Note that even though the <code>add_menu_page()</code> function itself takes the capability as an argument, we still need to check for it in the function which displays the content of the page.

This leads us into our next two functions nicely: <code>current_user_can()</code> and <code>user_can()</code>.

If you want to check whether or not the currently logged-in user has a specific capability, simply use the following format:

<pre><code class="language-php">
if( current_user_can( 'any_capability' ) ) {
    // The user has the capability
}
else {
    // The user does not have the capability
}  
</code></pre>

If you would like to check whether or not an arbitrary user has a specific capability, use the <code>user_can()</code> function:

<pre><code class="language-php">
if( user_can( 45, 'any_capability' ) ) {
    // The user with the ID of 45 has the capability
}
else {
    // The user with the ID of 45 does not have the capability
}  
</code></pre>

In addition to capabilities, both functions can check for <strong>roles</strong> as well:

<pre><code class="language-php">
if( current_user_can( 'marketing' ) ) {
    // The current user is a marketing person
}
else {
    // The current user is not a marketing person
}  
</code></pre>

## Creating User Types

While not an official term, I call different roles "user types" when they require many different front-end changes. Say you're building a theme marketplace, for example. Apart from the administrator who oversees all (and the authors who would write in the company blog) you also have buyers and sellers. These are both registered users of your website but would require somewhat differing front-ends.

The profile page of a buyer would most likely show the number of things he's bought, how frequently he buys stuff and when logged in, he would see a list of downloads.

A seller's profile would be a portfolio of his work, his most popular items, and so on. When logged in he should probably see sales statistics.</p>

### Figuring Out Roles and Permissions

To make things simple, users either buy or sell, and cannot do both. Let's create the two roles with a set of capabilities (off the top of my head...):

<pre><code class="language-php">
add_action( 'admin_init', 'add_custom_roles' );

function add_custom_roles() {
    $seller = add_role( 'seller', 'Seller', array(
        'read' =&gt; true,
        'delete_posts' =&gt; true,
        'edit_posts' =&gt; true,
        'delete_published_posts' =&gt; true,
        'publish_posts' =&gt; true,
        'upload_files' =&gt; true,
        'edit_published_posts' =&gt; true,
        'view_sales' =&gt; true,
        'moderate_comments' =&gt; true
    ));

    $role = get_role( 'administrator' );

    if( null !== $seller ) {
        $role-&gt;add_cap( 'view_sales' );
        $role-&gt;add_cap( 'view_others_sales' );
   }

    $buyer = add_role( 'buyer', 'Buyer', array(
        'read' =&gt; true,
        'add_payment' =&gt; true,
        'download_resources' =&gt; true
    ));

    if( null !== $buyer ) {
        $role-&gt;add_cap( 'add_payment' );
        $role-&gt;add_cap( 'add_others_payment' );
        $role-&gt;add_cap( 'download_resources' );
        $role-&gt;add_cap( 'download_others_resources' );
   }

}  
</code></pre>

The idea here is that sellers are like authors, who will store sellable items as posts. Therefore, they receive the capabilities of an author. In addition, they can also view sales stats for their own items.

In addition to viewing items, buyers can also add payments and download files related to items that they buy.

Admins receive all these permissions, but in addition, they may view the statistics of any other user, add payments to any account, and may download resources for any item.</p>

### Frontend Implementation

From here on out it's a matter of using our role and capability checking functions to determine who sees what. Let's take a look at a couple of examples:

### Listing Users

If we list all the users on the website, we could show the items bought for the buyers and the items sold for the sellers. Here's how:

<pre><code class="language-markup">
&lt;!-- 
  User Data comes from a WordPress user object stored in the $user variable 
--&gt; 

&lt;div class='user'&gt;
  &lt;div class='row'&gt;
    &lt;div class='threecol'&gt;
      &lt;?php echo get_avatar( $user-&gt;ID, 120 ) ?&gt;
    &lt;/div&gt;
    &lt;div class='sixcol'&gt;
      &lt;h1&gt;&lt;?php echo $user-&gt;display_name ?&gt;&lt;/h1&gt;
      &lt;?php echo $user-&gt;description ?&gt;
    &lt;/div&gt;
    &lt;div class='threecol last'&gt;
      &lt;?php if( user_can( $user-&gt;ID, 'buyer' ) ) : ?&gt;  
        &lt;div class='counter'&gt;
          &lt;span class='number'&gt;&lt;?php get_purchases_count( $user-&gt;ID ) ?&gt;&lt;/span&gt;
          &lt;span class='text'&gt;purchases&lt;/span&gt;
        &lt;/div&gt;
      &lt;?php else ?&gt;
        &lt;div class='counter'&gt;
          &lt;span class='number'&gt;&lt;?php get_sales_count( $user-&gt;ID ) ?&gt;&lt;/span&gt;
          &lt;span class='text'&gt;sales&lt;/span&gt;
        &lt;/div&gt;      
      &lt;?php endif ?&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;  
</code></pre>

Most of this is plain old HTML, but the important thing to take away is how the counter is created. Note that the <code>get_purchases_count()</code> and <code>get_sales_count()</code> functions are fictitious (they are not part of WordPress, of course).

Of course, in a real world example we would need to make sure that only buyers and sellers are listed, and we might need to create a separate template for them completely (if the differences are numerous enough).

<pre><code class="language-php">
foreach( $users as $user_id ) {
    $user = get_userdata( $user_id );
    if( user_can( $user-&gt;ID, 'buyer' ) ) {
        get_template_part( 'userlist', 'buyer' );
    }
    else {
        get_template_part( 'userlist', 'seller' );
    }
}  
</code></pre>

When looping through our users above, either <code>userlist-buyer.php</code> or <code>userlist-seller.php</code> will be used, depending on the user's role.</p>

## Conclusion

User roles and capabilities are extremely powerful tools in WordPress. Whenever you build a plugin which requires the implementation of special user-based functions, you should consider using them.

Apart from making your life easier (and more manageable) it will make the processes on your websites easier to follow and easier to backtrack any problems.

<em>(jvb) (il) (jc) (js)</em>


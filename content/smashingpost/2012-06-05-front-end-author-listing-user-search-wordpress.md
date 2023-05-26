---
title: Front-End Author Listing And User Search For WordPress
slug: front-end-author-listing-user-search-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dbbfa3b-f11e-4982-9ebe-61fceb75d988/abstract-wallpapers-noupe.jpg
date: 2012-06-05T13:55:36.000Z
author: cristian-antohe
description: >-
  This article will guide you through the process of creating a front-end page in WordPress that lists your authors. We’ll discuss why you would want to do this, we’ll introduce the `WP_User_Query` class, and then we’ll put it it all together
categories:
  - WordPress
  - Plugins
  - Shortcodes
---
At its core, WordPress is a rock-solid publishing platform. With a beautiful and easy to use interface, and support for custom post types and post formats, publishers have the flexibility to do what they do best: <strong>write content</strong>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Modifying Admin Post Lists In WordPress](https://www.smashingmagazine.com/2013/12/modifying-admin-post-lists-in-wordpress/)
*   [Useful Free Admin Plugins For WordPress](https://www.smashingmagazine.com/2012/03/useful-free-admin-plugins-wordpress/)
*   [Ten Things Every WordPress Plugin Developer Should Know](https://www.smashingmagazine.com/2011/03/ten-things-every-wordpress-plugin-developer-should-know/)
*   [Inside The WordPress Toolbar](https://www.smashingmagazine.com/2012/03/inside-the-wordpress-toolbar/)

{{% feature-panel %}}

However, WordPress is lacking in social interaction between content authors and readers. BuddyPress is trying to solve this, but I believe it’s going in the wrong direction by trying to be a full-fledged social network.

A big phrase in the publishing world is “user engagement.” This is about getting readers to spend more time on the website, actively searching for content and even generating their own. While one could write a few books on the subject, here are a few things a WordPress publisher can do:

*   Create a daily or weekly newsletter, with top stories from selected categories;
*   Provide an editorial-driven open forum in which editors propose themes, stories and questions and readers comment on them;
*   Continue the discussion of articles on social platforms;
*   Encourage users to submit articles and images for contests;
*   **Highlight your authors.**

### Listing Authors, And Why It’s A Good Thing

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d927ebe6-b445-4438-8098-de05dc869acc/user-listing1.jpg"><img loading="lazy" decoding="async" class="105831" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d927ebe6-b445-4438-8098-de05dc869acc/user-listing1.jpg" alt="user-listing" width="500" height="327" /></a>

If you’re a publisher, your authors are your biggest asset. They are the content creators. Their writing gets consumed by millions of people all over the world.

Showcasing them exposes them for what they really are: authorities. Your authors will thank you for acknowledging them, and readers will get to see the human face behind the technology.</p>

## Coding The Perfect Author Listing

Here are the things we want to achieve with our page:

*   Build it as a WordPress plugin so that we can reuse it more easily;
*   Display the name, biography, number of posts and latest published post of all authors;
*   Paginate the listing if we have many authors;
*   Make the listing searchable.</p>

### Introducing WP_User_Query And get_users

The <a href="https://codex.wordpress.org/Class_Reference/WP_User_Query"><code>WP_User_Query</code></a> class allows us to query the user database.

Besides returning an array of users, <code>WP_User_Query</code> returns general information about the query and, most importantly, the total number of users (for pagination).

One can use <code>WP_User_Query</code> by passing a series of arguments and listing the output.

<pre><code class="language-php">$my_authors = new WP_User_Query(
  array(
    'blog_id' =&gt; $GLOBALS['blog_id'],
    'role' =&gt; ’,
    'meta_key' =&gt; ’,
    'meta_value' =&gt; ’,
    'meta_compare' =&gt; ’,
    'include' =&gt; array(),
    'exclude' =&gt; array(),
    'search' =&gt; ’,
    'orderby' =&gt; 'login',
    'order' =&gt; 'ASC',
    'offset' =&gt; ’,
    'number' =&gt; ’,
    'count_total' =&gt; true,
    'fields' =&gt; 'all',
    'who' =&gt; ’
));</code></pre>

We’ll focus on only a few arguments, rather than go through all of them:

*   `role` This is the user’s role. In our example, we’ll query for `author`.
*   `offset` The first `n` users to be skipped in the returned array.
*   `number` Limit the total number of users returned.

We also have the <a href="https://codex.wordpress.org/Function_Reference/get_users"><code>get_users</code></a> class, which (like <code>WP_User_Query</code>) returns a number of users based on the parameters set.

The important difference between the two is that <code>get_users</code> only returns an array of users and their meta data, whereas <code>WP_User_Query</code> returns extra information such as the <strong>total number of users</strong> (which is useful when it comes time to paginate).</p>

### Simple User Listing Using get_users()

Before moving on with the full user listing, including pagination and search, let’s see <code>get_users</code> in action.

If all you need is a simple list of authors, then you could just use <a href="https://codex.wordpress.org/Function_Reference/wp_list_authors"><code>wp_list_authors</code></a>, like so:

<pre><code class="language-php">wp_list_authors('show_fullname=1&amp;optioncount=1&amp;orderby=post_count&amp;order=DESC&amp;number=3');</code></pre>

## Creating A Plugin And Shortcode With A Bit More Functionality

A simple and straightforward way to build our user listing would be to create a shortcode that we could include on any page we like. Housing this type of functionality in a plugin is ideal, so that we don’t have to worry about migrating it when we change the theme.

Let’s keep it simple. Our entire plugin will consist of just one file: <code>simple-user-listing.php</code>.

<pre><code class="language-php">&lt;?php
/*
Plugin Name: Simple User Listing
Plugin URI: https://cozmoslabs.com
description: >-
  Create a simple shortcode to list our WordPress users.
Author: Cristian Antohe
Version: 0.1
Author URI: https://cozmoslabs.com
*/

function sul_user_listing($atts, $content = null) {
  global $post;

  extract(shortcode_atts(array(
    "role" =&gt; ’,
    "number" =&gt; '10'
  ), $atts));

  $role = sanitize_text_field($role);
  $number = sanitize_text_field($number);

  // We're outputting a lot of HTML, and the easiest way
  // to do it is with output buffering from PHP.
  ob_start();

  // Get the Search Term
  $search = ( isset($_GET["as"]) ) ? sanitize_text_field($_GET["as"]) : false ;

  // Get Query Var for pagination. This already exists in WordPress
  $page = (get_query_var('paged')) ? get_query_var('paged') : 1;

  // Calculate the offset (i.e. how many users we should skip)
  $offset = ($page - 1) * $number;

  if ($search){
    // Generate the query based on search field
    $my_users = new WP_User_Query(
      array(
        'role' =&gt; $role,
        'search' =&gt; '*' . $search . '*'
      ));
  } else {
    // Generate the query
    $my_users = new WP_User_Query(
      array(
        'role' =&gt; 'author',
        'offset' =&gt; $offset ,
        'number' =&gt; $number
      ));
  }

  // Get the total number of authors. Based on this, offset and number
  // per page, we'll generate our pagination.

  $total_authors = $my_users-&gt;total_users;

  // Calculate the total number of pages for the pagination
  $total_pages = intval($total_authors / $number) + 1;

  // The authors object.

  $authors = $my_users-&gt;get_results();
?&gt;

  &lt;div class="author-search"&gt;
  &lt;h2&gt;Search authors by name&lt;/h2&gt;
    &lt;form method="get" id="sul-searchform" action="&lt;?php the_permalink() ?&gt;"&gt;
      &lt;label for="as" class="assistive-text"&gt;Search&lt;/label&gt;
      &lt;input type="text" class="field" name="as" id="sul-s" placeholder="Search Authors" /&gt;
      &lt;input type="submit" class="submit" name="submit" id="sul-searchsubmit" value="Search Authors" /&gt;
    &lt;/form&gt;
  &lt;?php
  if($search){ ?&gt;
    &lt;h2 &gt;Search Results for: &lt;em&gt;&lt;?php echo $search; ?&gt;&lt;/em&gt;&lt;/h2&gt;
    &lt;a href="&lt;?php the_permalink(); ?&gt;"&gt;Back To Author Listing&lt;/a&gt;
  &lt;?php } ?&gt;

  &lt;/div&gt;&lt;!-- .author-search --&gt;

&lt;?php if (!empty($authors))   { ?&gt;
  &lt;ul class="author-list"&gt;
&lt;?php
  // loop through each author foreach($authors as $author){
    $author_info = get_userdata($author-&gt;ID);
    ?&gt;
    &lt;li&gt;
      &lt;?php echo get_avatar( $author-&gt;ID, 90 ); ?&gt;
      &lt;h2&gt;&lt;a href="&lt;?php echo get_author_posts_url($author-&gt;ID); ?&gt;"&gt;&lt;?php echo $author_info-&gt;display_name; ?&gt;&lt;/a&gt; - &lt;?php echo count_user_posts( $author-&gt;ID ); ?&gt; posts&lt;/h2&gt;
      &lt;p&gt;&lt;?php echo $author_info-&gt;description; ?&gt;&lt;/p&gt;
      &lt;?php $latest_post = new WP_Query( "author=$author-&gt;ID&amp;post_count=1" );
      if (!empty($latest_post-&gt;post)){ ?&gt;
      &lt;p&gt;&lt;strong&gt;Latest Article:&lt;/strong&gt;
      &lt;a href="&lt;?php echo get_permalink($latest_post-&gt;post-&gt;ID) ?&gt;"&gt;
        &lt;?php echo get_the_title($latest_post-&gt;post-&gt;ID) ;?&gt;
      &lt;/a&gt;&lt;/p&gt;
      &lt;?php } //endif ?&gt;
      &lt;p&gt;&lt;a href="&lt;?php echo get_author_posts_url($author-&gt;ID); ?&gt; "&gt;Read &lt;?php echo $author_info-&gt;display_name; ?&gt; posts&lt;/a&gt;&lt;/p&gt;
    &lt;/li&gt;
    &lt;?php
  }
?&gt;
  &lt;/ul&gt; &lt;!-- .author-list --&gt;
&lt;?php } else { ?&gt;
  &lt;h2&gt;No authors found&lt;/h2&gt;
&lt;? } //endif ?&gt;

  &lt;nav id="nav-single" style="clear:both; float:none; margin-top:20px;"&gt;
    &lt;h3 class="assistive-text"&gt;Post navigation&lt;/h3&gt;
    &lt;?php if ($page != 1) { ?&gt;
      &lt;span class="nav-previous"&gt;&lt;a rel="prev" href="&lt;?php the_permalink() ?&gt;page/&lt;?php echo $page - 1; ?&gt;/"&gt;&lt;span class="meta-nav"&gt;←&lt;/span&gt; Previous&lt;/a&gt;&lt;/span&gt;
    &lt;?php } ?&gt;

    &lt;?php if ($page &lt; $total_pages ) { ?&gt;
      &lt;span class="nav-next"&gt;&lt;a rel="next" href="&lt;?php the_permalink() ?&gt;page/&lt;?php echo $page + 1; ?&gt;/"&gt;Next &lt;span class="meta-nav"&gt;→&lt;/span&gt;&lt;/a&gt;&lt;/span&gt;
    &lt;?php } ?&gt;
  &lt;/nav&gt;

  &lt;?php
  // Output the content.
  $output = ob_get_contents();
  ob_end_clean();

  // Return only if we're inside a page. This won't list anything on a post or archive page.

  if (is_page()) return  $output;

}

// Add the shortcode to WordPress.
add_shortcode('userlisting', 'sul_user_listing');
?&gt;</code></pre>

## Breaking Down The Code

The top of our plugin’s main PHP file must contain the standard header of information. This header tells WordPress that our plugin exists, and it adds it to the plugin management screen so that it can be activated, loaded and run.

<pre><code class="language-php">/*
Plugin Name: Simple User Listing
Plugin URI: https://cozmoslabs.com
description: >-
  Create a simple shortcode to list our WordPress users.
Author: Cristian Antohe
Version: 0.1
Author URI: https://cozmoslabs.com
*/</code></pre>

### Creating a Shortcode

Adding a new shortcode in WordPress is rather easy. We find the function that returns the desired output (in our case, <code>sul_user_listing</code>), and then we add it using the <code>add_shortcode</code> WordPress function.

<pre><code class="language-php">function sul_user_listing($atts, $content = null) {
// return our output
}
add_shortcode('userlisting', 'sul_user_listing');</code></pre>

### Extracting Our Shortcode Arguments

We want to be able to list users based on their roles and to control how many users are displayed on the page. We do this through shortcode arguments. We’ll add the shortcode to our theme in this way: <code>[userlisting role="author" number="15"]</code>. This will allow us to reuse the plugin to list our subscribers as well.

To do this, we need to use shortcode arguments:

<pre><code class="language-php">extract(shortcode_atts(array(
  "role" =&gt; ’,
  "number" =&gt; '10'
), $atts));</code></pre>

The <code>extract</code> function imports variables into our function from an array. The WordPress function <code>shortcode_atts</code> basically returns an array with our arguments; and we’ll set up some defaults in case none are found.

Note that the <strong><code>role</code> default is an empty string</strong>, which would list all users regardless of their role.</p>

### Shortcodes Should Never Echo Stuff Out

The return value of a shortcode handler function gets inserted into the post content’s output in place of the shortcode. You should use <code>return</code> and not <code>echo</code>; anything that is echoed will be outputted to the browser but will probably appear above everything else. You would also probably get “headers already sent” type of errors.

For simplicity, we’re buffering the output through <code>ob_start()</code>, so we put everything into an object and return it once we’re done.</p>

### Setting Up Our Variables

Now we can start building our listing of authors. First, we need to set up a few variables:

*   `$search` This takes the `GET` parameter `as` if it exists.
*   `$page` The `get_query_var` for the pagination. This already exists in WordPress.
*   `$offset` Calculate the offset (i.e. how many users to skip when paginating).
*   `$total_authors` Get the total number of authors.
*   `$total_pages` Calculate the total number of pages for the pagination.</p>

### The Query

We actually have two queries: the default listing and the search results.

<pre><code class="language-php">if ($search){
  // Generate the query based on search field
  $my_users = new WP_User_Query(
    array(
      'role' =&gt; $role,
      'search' =&gt; '*' . $search . '*'
    ));
} else {
  // Generate the query
  $my_users = new WP_User_Query(
    array(
      'role' =&gt; 'author',
      'offset' =&gt; $offset ,
      'number' =&gt; $number
    ));
}</code></pre>

### WP_User_Query->total_users and WP_User_Query->get_results

WP_User_Query provides us with two useful functions, among others:

*   `total_users` Returns the total number of authors. This, the offset and the number of users per page will generate our pagination.
*   `get_results` Returns an object with the authors alone. This is similar to what `get_users()` returns.</p>

### The Search Form

For the search, we’re using a simple form. There’s nothing complex here.

<pre><code class="language-php">&lt;div class="author-search"&gt;
&lt;h2&gt;Search authors by name&lt;/h2&gt;
  &lt;form method="get" id="sul-searchform" action="&lt;?php the_permalink() ?&gt;"&gt;
    &lt;label for="as" class="assistive-text"&gt;Search&lt;/label&gt;
    &lt;input type="text" class="field" name="as" id="s" placeholder="Search Authors" /&gt;
    &lt;input type="submit" class="submit" name="submit" id="searchsubmit" value="Search Authors" /&gt;
  &lt;/form&gt;
&lt;?php
if($search){ ?&gt;
  &lt;h2 &gt;Search Results for: &lt;em&gt;&lt;?php echo $search; ?&gt;&lt;/em&gt;&lt;/h2&gt;
  &lt;a href="&lt;?php the_permalink(); ?&gt;"&gt;Back To Author Listing&lt;/a&gt;
&lt;?php } ?&gt;

&lt;/div&gt;&lt;!-- .author-search --&gt;</code></pre>

### User Data and Listing the Authors

Looping through our results is fairly simple. However, getting information about users is a bit confusing in WordPress. You see, there are a lot of ways to get user data. We could get it directly from the returned query; we could use general functions such as <code>get_userdata</code>, <code>get_user_meta</code>, <code>the_author_meta</code> and <code>get_the_author_meta</code>; or we could even use dedicated functions such as <code>the_author_link</code> and <code>the_author_posts</code>.

We’ll just use <code>get_userdata</code> plus two other functions: <code>get_author_posts_url</code> and <code>get_avatar</code>.

<pre><code class="language-php">&lt;?php if (!empty($authors))   { ?&gt;
  &lt;ul class="author-list"&gt;
&lt;?php
  // loop through each author foreach($authors as $author){
    $author_info = get_userdata($author-&gt;ID);
    ?&gt;
    &lt;li&gt;
      &lt;?php echo get_avatar( $author-&gt;ID, 90 ); ?&gt;
      &lt;h2&gt;&lt;a href="&lt;?php echo get_author_posts_url($author-&gt;ID); ?&gt;"&gt;&lt;?php echo $author_info-&gt;display_name; ?&gt;&lt;/a&gt; - &lt;?php echo count_user_posts( $author-&gt;ID ); ?&gt; posts&lt;/h2&gt;
      &lt;p&gt;&lt;?php echo $author_info-&gt;description; ?&gt;&lt;/p&gt;
      &lt;?php $latest_post = new WP_Query( "author=$author-&gt;ID&amp;post_count=1" );
      if (!empty($latest_post-&gt;post)){ ?&gt;
      &lt;p&gt;&lt;strong&gt;Latest Article:&lt;/strong&gt;
      &lt;a href="&lt;?php echo get_permalink($latest_post-&gt;post-&gt;ID) ?&gt;"&gt;
        &lt;?php echo get_the_title($latest_post-&gt;post-&gt;ID) ;?&gt;
      &lt;/a&gt;&lt;/p&gt;
      &lt;?php } //endif ?&gt;
      &lt;p&gt;&lt;a href="&lt;?php echo get_author_posts_url($author-&gt;ID); ?&gt; "&gt;Read &lt;?php echo $author_info-&gt;display_name; ?&gt; posts&lt;/a&gt;&lt;/p&gt;
    &lt;/li&gt;
    &lt;?php
  }
?&gt;
  &lt;/ul&gt; &lt;!-- .author-list --&gt;
&lt;?php } else { ?&gt;
  &lt;h2&gt;No authors found&lt;/h2&gt;
&lt;? } //endif ?&gt;</code></pre>

### Pagination

We need pagination because each listing will generate two extra queries. So, if we were listing 100 people, we would end up with 200 extra queries per page. That’s a bit much, so pagination is really needed. Otherwise, for websites with many authors, the load could get so heavy that it brings down the website.

<pre><code class="language-php">&lt;nav id="nav-single" style="clear:both; float:none; margin-top:20px;"&gt;
  &lt;h3 class="assistive-text"&gt;Post navigation&lt;/h3&gt;
  &lt;?php if ($page != 1) { ?&gt;
    &lt;span class="nav-previous"&gt;&lt;a rel="prev" href="&lt;?php the_permalink() ?&gt;page/&lt;?php echo $page - 1; ?&gt;/"&gt;&lt;span class="meta-nav"&gt;←&lt;/span&gt; Previous&lt;/a&gt;&lt;/span&gt;
  &lt;?php } ?&gt;

  &lt;?php if ($page &lt; $total_pages ) { ?&gt;
    &lt;span class="nav-next"&gt;&lt;a rel="next" href="&lt;?php the_permalink() ?&gt;page/&lt;?php echo $page + 1; ?&gt;/"&gt;Next &lt;span class="meta-nav"&gt;→&lt;/span&gt;&lt;/a&gt;&lt;/span&gt;
  &lt;?php } ?&gt;
&lt;/nav&gt;</code></pre>

## Final Thoughts

We’ve discussed the code for an authors listing, but it has so many more uses:

*   List your company’s employees;
*   Showcase users who have won a competition (by listing users with the role of “winners”);
*   Present your company’s departments, each with its respective team (based on user roles).

If you allow users to register on your website, you could use more or less the same code to generate any listing of users based on your needs. If you require users to log in in order to comment (an effective way to stop automated spam), then listing users and their number of comments could increase engagement.

Have you used something similar for a project? If so, let us know in the comments!

{{< signature "al" >}}


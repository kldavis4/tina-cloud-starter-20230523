---
title: 10 Useful WordPress Coding Techniques
slug: 10-useful-wordpress-hacks-for-advanced-themes
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c57fc6-2db3-4e93-a398-e4351c8cef26/writing-css-illu.jpg
date: 2009-10-20T13:22:28.000Z
author: jean-baptiste-jung
summary: >-
  Since last year, the WordPress themes market has grown incredibly. The reason? Great designs, of course, but also a lot of amazing new functionality. Top WordPress developers are always looking to get the most out of WordPress and use all of their knowledge to find ways to make their favorite blogging engine even more powerful.
description: >-
  In this article, we have compiled ten useful WordPress code snippets, hacks and tips to help you create a WordPress theme that stands out from the crowd.
categories:
  - WordPress
  - Techniques (WP)
---
In this article, we have compiled ten useful WordPress code snippets, hacks and tips to help you create a WordPress theme that stands out from the crowd.

## 1. Style Posts Individually

**The problem**.  
Your blog has a lot of posts, but the posts aren't all of the same type. To give special styling to one or more of your posts, you can take advantage of both the `post_class()` function and the post ID.

**The solution**.  
To apply this trick, just open your _single.php_ file, find the loop and replace it with the following:

<pre><code class="language-php">&lt;?php if (have_posts()) : ?&gt;
&lt;?php while (have_posts()) : the_post(); ?&gt;
&lt;div &lt;?php post_class() ?&gt; id=&quot;post-&lt;?php the_ID(); ?&gt;&quot;&gt;
&lt;h3&gt;&lt;a href=&quot;&lt;?php the_permalink() ?&gt;&quot;&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/h3&gt;
&lt;?php the_content(); ?&gt;
&lt;/div&gt;
&lt;?php endwhile; else: ?&gt;
&lt;?php _e('Sorry, no posts matched your criteria.'); ?&gt;
&lt;?php endif; ?&gt;</code></pre>

**Code explanation**.  
The important part is mostly in line 3\. Here, we have added the PHP `post_class()` function. Introduced in WordPress 2.8, this function adds CSS classes to the post. For example, it can add:

*   .hentry
*   .sticky
*   .category-tutorials
*   .tag-wordpress

With these CSS classes now added, you can now give a custom style to all posts that have the `sticky` tag or those that belong to the `tutorials` category.

The other important piece of this code is `id="post-<?php the_ID(); ?>"`. By displaying the ID of the post here, we're able to style a particular post. As an example:

<pre><code class="language-php">#post-876{
  background:#ccc;
}</code></pre>

**Source:**

 *   [Take advantage of the new post class](https://justagirlintheworld.com/take-advantage-of-the-new-sticky-post-feature-in-wordpress-27/)

{{% feature-panel %}}

## 2. Display Related Posts... With Thumbnails!

**The problem**.  
After they have read your latest post, what do your readers do? That's easy: most of them simply leave. A great way to keep them interested is to display a list of related posts. Many plug-ins can do that, but for those who like to know how things works, here is some nice code to get related posts and their thumbnails.

**The solution**.  
Simply paste this code after the `the_content()` function in your _single.php_ file:

<div class="break-out">

 <pre><code class="language-php">&lt;?php
$original_post = $post;
$tags = wp_get_post_tags($post-&gt;ID);
if ($tags) {
  echo '&lt;h2&gt;Related Posts&lt;/h2&gt;';
  $first_tag = $tags[0]-&gt;term_id;
  $args=array(
    'tag__in' =&gt; array($first_tag),
    'post__not_in' =&gt; array($post-&gt;ID),
    'showposts'=&gt;4,
    'caller_get_posts'=&gt;1
   );
  $my_query = new WP_Query($args);
  if( $my_query-&gt;have_posts() ) {
    echo &quot;&lt;ul&gt;&quot;;
    while ($my_query-&gt;have_posts()) : $my_query-&gt;the_post(); ?&gt;
      &lt;li&gt;&lt;img src=&quot;&lt;?php bloginfo('template_directory'); ?&gt;/timthumb/timthumb.php?src=&lt;?php echo get_post_meta($post-&gt;ID, &quot;post-img&quot;, true); ?&gt;&amp;h=40&amp;w=40&amp;zc=1&quot; alt=&quot;&quot; /&gt;&lt;a href=&quot;&lt;?php the_permalink() ?&gt;&quot; rel=&quot;bookmark&quot; title=&quot;Permanent Link to &lt;?php the_title_attribute(); ?&gt;&quot;&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;?php endwhile;
    echo &quot;&lt;/ul&gt;&quot;;
  }
}
$post = $original_post;
wp_reset_query();
?&gt;</code></pre>
</div>

**Code explanation**.  
First, this code makes use of TimbThumb, a PHP image-resizing script. We have used it to automatically resize images to 40 by 40 pixels.

Once this code is pasted in your theme, it uses the first tag of the post to fetch related posts. In this example, four related posts are displayed. You can change this number on line 10.

Also, notice that I have cloned the `$post` variable at the beginning of the script and restored it at the end. This prevents problems that may occur with the loop, such as comments being assigned to the wrong post.

**Source:**

 *   [How to: Show related posts without a plug-in](https://www.wprecipes.com/how-to-show-related-posts-without-a-plugin)

## 3. Alternate Post Styling On Your Home Page

**The problem**.  
Many new WordPress themes have an amazing way of displaying posts on the home page. For example, we can display the first three posts bigger than the rest, with images and extended text, with the remaining posts shown more simply.

I have seen many themes in which developers use two distinct loops to achieve this, which isn't necessary and can cause further problems. Let's use a much simpler method.

**The solution**.  
Here is a custom loop that displays the first three posts different than the rest. You can replace the existing loop in your _index.php_ file with this code.

<div class="break-out">

 <pre><code class="language-php">&lt;?php
$postnum = 0;
while (have_posts()) : the_post(); ?&gt;

&lt;?php if ($postnum &lt;= 3){ ?&gt;
&lt;div &lt;?php post_class() ?&gt; id=&quot;post-&lt;?php the_ID(); ?&gt;&quot;&gt;
  &lt;div class=&quot;date&quot;&gt;&lt;span&gt;&lt;?php the_time('M j') ?&gt;&lt;/span&gt;&lt;/div&gt;
    &lt;h2&gt;(&lt;?php echo $postnum;?&gt;)&lt;a href=&quot;&lt;?php the_permalink() ?&gt;&quot;&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/h2&gt;
  &lt;div class=&quot;post-image&quot; style=&quot;text-align:center;&quot;&gt;
    &lt;a href=&quot;&lt;?php the_permalink() ?&gt;&quot;&gt;&lt;img src=&quot;&lt;?php bloginfo('template_directory' ); ?&gt;/timthumb.php?src=&lt;?php  echo catch_that_image(); ?&gt;&amp;amp;w=500&amp;amp;h=200&amp;amp;zc=1&quot; alt=&quot;&lt;?php the_title(); ?&gt;&quot; /&gt;&lt;/a&gt;
  &lt;/div&gt;
  &lt;p&gt;&lt;?php the_content('Read the rest of this entry &amp;raquo;'); ?&gt;&lt;/p&gt;
  &lt;p class=&quot;more&quot;&gt;&lt;a href=&quot;#&quot;&gt;Read More&lt;/a&gt;&lt;/p&gt;
  &lt;/div&gt;
&lt;/div&gt;

&lt;?php } else {
&lt;div &lt;?php post_class( 'single ' . $end ); ?&gt; id=&quot;post-&lt;?php the_ID(); ?&gt;&quot;&gt;
  &lt;div class=&quot;post-content&quot;&gt;
    &lt;h3&gt;&lt;a href=&quot;&lt;?php the_permalink() ?&gt;&quot;&gt;(&lt;?php echo $postnum; ?&gt;)&lt;?php the_title(); ?&gt;&lt;/a&gt; &lt;?php edit_post_link('&#95;', ’, ’); ?&gt;&lt;/h3&gt;
    &lt;p&gt;&lt;?php the_excerpt( ’ ); ?&gt;&lt;/p&gt;
    &lt;p class=&quot;more&quot;&gt;&lt;a href=&quot;#&quot;&gt;Read More ?&lt;/a&gt;&lt;/p&gt;
  &lt;/div&gt;
&lt;/div&gt;&lt;!-- End post --&gt;

&lt;?php }
  endwhile;
  ?&gt;</code></pre>
</div>

**Code explanation**.  
Nothing hard here! We just created a PHP variable, named `$postnum`, which is invoked at the end of the loop. If `$postnum` is less than or equal to 3, the post is displayed in full. Otherwise, it is displayed in its more compact form.</p>

## 4. Using Multiple Loops

**The problem**.  
When coding complex WordPress pages with more than one loop, it can happen that one of the loops doesn't behave as expected: for example, unwanted offset, repeated posts, etc. Happily, with a bit of knowledge and a very useful function, we can avoid this.

**The solution**.  
The following example features two distinct loops. Notice the `rewind_posts()` function on line 8\. This example can be used on any WordPress file as is: _index.php_, _single.php_, etc.

<pre><code class="language-php">// First loop (get the last 3 posts in the "featured" category)
&lt;?php query_posts('category_name=featured&amp;showposts=3'); ?&gt;
&lt;?php while (have_posts()) : the_post(); ?&gt;
  &lt;!-- Do stuff... --&gt;
&lt;?php endwhile;?&gt;

//loop reset
&lt;?php rewind_posts(); ?&gt;

//Second loop (Get all posts)
&lt;?php while (have_posts()) : the_post(); ?&gt;
  &lt;!-- Do stuff... --&gt;
&lt;?php endwhile; ?&gt;</code></pre>

**Code explanation**.  
This piece of code doesn't use any hacks; `rewind_posts()` is a standard WordPress function.

The purpose of `rewind_posts()` is to "clear" a loop that has been previously used (like the first loop in our example above), allowing you to use a second loop that isn't affected by the first loop's results.

**Source:**

 *   [Multiple WordPress Loops Explained](https://www.catswhocode.com/blog/multiple-wordpress-loops)

{{% ad-panel-leaderboard %}}

## 5. Overwrite Post Titles Easily

**The problem**.  
`the_title()` is a basic but very useful WordPress function: it displays the post or page's title. No more, no less. But hey, have you ever wished you were able to display the full title in your listing of posts and a custom title on the actual post's page? If so, find out how right here.

**The solution**.  
In your _single.php_ file, find the call to the `the_title()` function and replace it with the following code:

<pre><code class="language-php">&lt;?php $title = get_post_meta($post-&gt;ID, &quot;custom-title&quot;, true);
if ($title != &quot;&quot;) {
  echo &quot;&lt;h1&gt;&quot;.$title.&quot;&lt;/h1&gt;&quot;;
} else { ?&gt;
  &lt;h1&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
&lt;?php } ?&gt;</code></pre>

Once that's done, you can rewrite the post's title by creating a field named `custom-title`. Its value will be your custom title for this post.

**Code explanation**.  
When this code loads, it retrieves the meta field named `custom-title`. If this meta field exists and isn't blank, it is displayed as the post's title. Otherwise, the `the_title()` function is called, and the post's regular title is displayed.

**Source:**

 *   [Allow title overwrite on your WordPress blog](https://www.wprecipes.com/allow-title-overwrite-on-your-wordpress-blog)

## 6. Add Multiple Sidebars

**The problem**.  
Sidebars are great because they allow you to display a lot of useful info, such as related posts, author info, a blog roll, 125x125-pixel ad spaces and so on. But sidebars can quickly become very busy, and readers may be hard-pressed to find what they're looking for. So, what about having different sidebars available and displaying the most appropriate one for the post?

**The solution**.  
To apply this hack, duplicate your _sidebar.php_ file and fill it with whatever information you would like to appear. Save the file as _sidebar-whatever.php_.

Once that's done, open your single.php_<sup>&#42;</sup> file and find the call to the `get_sidebar()` function:

<pre><code class="language-php">&lt;?php get_sidebar(); ?&gt;</code></pre>

Replace it with:

<pre><code class="language-php">&lt;?php $sidebar = get_post_meta($post->ID, "sidebar", true);
get_sidebar($sidebar);
?&gt;</code></pre>

Now when you write a post, create a custom field named `sidebar`. Set its value as the name of the sidebar that you want to include. For example, if its value is _right_, WordPress will automatically include _sidebar-right.php_ as a sidebar.  
If no custom _sidebar_ field is found, WordPress automatically includes the default sidebar.

_*The same can be done with page.php._

**Code explanation**.  
This trick is quite simple. The first thing we did was look for a custom field named _sidebar_ and get its value as a variable. Then, the variable is used as a parameter for the WordPress function `get_sidebar()`, which allows us to specify a particular file to use as a sidebar.

**Source:**

 *   [WordPress hack: Choose the sidebar to use, post by post](https://www.wprecipes.com/wordpress-hack-choose-the-sidebar-to-use-post-by-post)

## 7. Display Content Only To Registered Users

**The problem**.  
As you probably know, WordPress lets you decide whether to allow readers to create accounts and sign in to your blog. If you want to increase your blog's registered readers or would just like to reward existing readers, why not keep some content private, just for them?

**The solution**.  
To achieve this hack, we'll use a shortcode. The first step is to create it. Open your _functions.php_ file and paste the following code:

<div class="break-out">

 <pre><code class="language-php">function member_check_shortcode($atts, $content = null) {
  if (is_user_logged_in() &#038;&amp; !is_null($content) &#038;&amp; !is_feed()) {
    return $content;
  } else {
    return 'Sorry, this part is only available to our members. Click here to become a member!';
}

add_shortcode('member', 'member_check_shortcode');
</code></pre>
</div>

Once that's done, you can add the following to your posts to create a section or text (or any other content) that will be displayed only to registered users:

<pre><code class="language-php">[member]
This text will be displayed only to registered users.
[/member]</code></pre>

That's it. Registered users will see the text contained in the shortcode, while unregistered users will see a message asking them to register.

**Code explanation**.  
The first thing we've done is create a function named `member_check_shortcode`, which checks whether the current user is logged in. If they are, then the text contained in the `[member]` shortcode is displayed. Otherwise, the message on line 5 is shown.

If you'd like to know more about WordPress shortcodes, you should definitely have a look at our [Mastering WordPress Shortcodes](https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/) post.

**Source:**

 *   [Using shortcodes to show members-only content](https://justintadlock.com/archives/2009/05/09/using-shortcodes-to-show-members-only-content)
*   [WordPress shortcode: Display content to registered users only](https://www.wprecipes.com/wordpress-shortcode-display-content-to-registered-users-only)

{{% ad-panel-leaderboard %}}

## 8. Display Your Most Popular Content In The Sidebar

**The problem**.  
If you want to feature your best content and help readers discover more articles from your blog, you might want to display a list of your most popular posts, based on the number of comments they've received, in your sidebar.

**The solution**.  
This code is really easy to implement. Just paste it wherever you'd like your popular posts to appear. To get more or less than five posts, just change the value of the SQL `limit` clause on line 3.

<div class="break-out">

 <pre><code class="language-php">&lt;h2&gt;Popular Posts&lt;/h2&gt;
&lt;ul&gt;
&lt;?php $result = $wpdb-&gt;get_results(&quot;SELECT comment_count,ID,post_title FROM $wpdb-&gt;posts ORDER BY comment_count DESC LIMIT 0 , 5&quot;);
foreach ($result as $post) {
setup_postdata($post);
$postid = $post-&gt;ID;
$title = $post-&gt;post_title;
$commentcount = $post-&gt;comment_count;
if ($commentcount != 0) { ?&gt;
&lt;li&gt;&lt;a href=&quot;&lt;?php echo get_permalink($postid); ?&gt;&quot; title=&quot;&lt;?php echo $title ?&gt;&quot;&gt;

&lt;?php echo $title ?&gt;&lt;/a&gt; {&lt;?php echo $commentcount ?&gt;}&lt;/li&gt;
&lt;?php } } ?&gt;
&lt;/ul&gt;
</code></pre>
</div>

**Code explanation**.  
In this code, we use the `$wpdb` object to send a custom SQL query to the WordPress database. Then we verify that the results aren't empty (i.e. that no posts are without comments), and finally we display the list of posts.

**Sources**

 *   [Create your own "Popular Posts" page](https://www.problogdesign.com/wordpress/create-your-own-popular-posts-page/)
*   [How to: Display your most popular content in your blog sidebar](https://www.wprecipes.com/how-to-display-your-most-popular-content-in-your-blog-sidebar)

## 9. Create A Drop-Down Menu For Easy Tag Navigation

**The problem**.  
Tags are cool because they allow you to categorize content using precise terms. But displaying tag clouds is a problem: they are ugly, not easy to use and can be extremely big.

So, what's the solution? Simply create a drop-down menu for your tags. That way, they don't get in the way, but people still have easy access to them.

**The solution**.  
To create our drop-down menu of tags, we first have to paste the two functions below into the _functions.php_ file of our WordPress theme:

<div class="break-out">

 <pre><code class="language-php">&lt;?php
function dropdown_tag_cloud( $args = ’ ) {
  $defaults = array(
    'smallest' =&gt; 8, 'largest' =&gt; 22, 'unit' =&gt; 'pt', 'number' =&gt; 45,
    'format' =&gt; 'flat', 'orderby' =&gt; 'name', 'order' =&gt; 'ASC',
    'exclude' =&gt; ’, 'include' =&gt; ’
  );
  $args = wp_parse_args( $args, $defaults );

  $tags = get_tags( array_merge($args, array('orderby' =&gt; 'count', 'order' =&gt; 'DESC')) ); // Always query top tags

  if ( empty($tags) )
    return;

  $return = dropdown_generate_tag_cloud( $tags, $args ); // Here's where those top tags get sorted according to $args if ( is_wp_error( $return ) )
    return false;
  else
    echo apply_filters( 'dropdown_tag_cloud', $return, $args );
}

function dropdown_generate_tag_cloud( $tags, $args = ’ ) {
  global $wp_rewrite;
  $defaults = array(
    'smallest' =&gt; 8, 'largest' =&gt; 22, 'unit' =&gt; 'pt', 'number' =&gt; 45,
    'format' =&gt; 'flat', 'orderby' =&gt; 'name', 'order' =&gt; 'ASC'
  );
  $args = wp_parse_args( $args, $defaults );
  extract($args);

  if ( !$tags )
    return;
  $counts = $tag_links = array();
  foreach ( (array) $tags as $tag ) {
    $counts[$tag-&gt;name] = $tag-&gt;count;
    $tag_links[$tag-&gt;name] = get_tag_link( $tag-&gt;term_id );
    if ( is_wp_error( $tag_links[$tag-&gt;name] ) )
      return $tag_links[$tag-&gt;name];
    $tag_ids[$tag-&gt;name] = $tag-&gt;term_id;
  }

  $min_count = min($counts);
  $spread = max($counts) - $min_count;
  if ( $spread &lt;= 0 )
    $spread = 1;
  $font_spread = $largest - $smallest;
  if ( $font_spread &lt;= 0 )
    $font_spread = 1;
  $font_step = $font_spread / $spread;

  // SQL cannot save you; this is a second (potentially different) sort on a subset of data.
  if ( 'name' == $orderby )
    uksort($counts, 'strnatcasecmp');
  else
    asort($counts);

  if ( 'DESC' == $order )
    $counts = array_reverse( $counts, true );

  $a = array();

  $rel = ( is_object($wp_rewrite) &amp;&amp; $wp_rewrite-&gt;using_permalinks() ) ? ' rel="tag"' : ’;

  foreach ( $counts as $tag =&gt; $count ) {
    $tag_id = $tag_ids[$tag];
    $tag_link = clean_url($tag_links[$tag]);
    $tag = str_replace(' ', '&amp;nbsp;', wp_specialchars( $tag ));
    $a[] = "t&lt;option value='$tag_link'&gt;$tag ($count)&lt;/option&gt;";
  }

    switch ( $format ) :
  case 'array' :
    $return =&amp; $a;
    break;
  case 'list' :
    $return = "&lt;ul class='wp-tag-cloud'&gt;nt&lt;li&gt;";
    $return .= join("&lt;/li&gt;nt&lt;li&gt;", $a);
    $return .= "&lt;/li&gt;n&lt;/ul&gt;n";
    break;
  default :
    $return = join("n", $a);
    break;
  endswitch;

  return apply_filters( 'dropdown_generate_tag_cloud', $return, $tags, $args );
}
?&gt;
</code></pre>
</div>

Once you've pasted this function in your _functions.php_ file, you can use it to create your drop-down menu of tags. Just open the file where you want the list to be displayed and paste the following code:

<pre><code class="language-php">&lt;select name="tag-dropdown" onchange="document.location.href=this.options[this.selectedIndex].value;"&gt;
  &lt;option value="#"&gt;Liste d'auteurs&lt;/option&gt;
  &lt;?php dropdown_tag_cloud('number=0&amp;order=asc'); ?&gt;

&lt;/select&gt;</code></pre>

**Code explanation**.  
To achieve this hack, we take the `wp_tag_cloud()` WordPress function and rewrite it to make it display tags in an HTML "Select" element.

Then, we just call the newly created `dropdown_tag_cloud()` in our theme to display the drop-down menu items.

**Source:**

 *   [Top 10 WordPress hacks from June '09](https://www.catswhocode.com/blog/top-10-wordpress-hacks-from-june-09)

## 10. Auto-Resize Images Using TimThumb And WordPress Shortcodes

**The problem**.  
A good blog post needs images, whether screenshots or simple eye-candy. Readers always prefer articles with nice pictures to plain boring text.

But images can be a pain to deal with, especially because of their various sizes. So how about we create a WordPress shortcode that uses Timthumb to automatically resize images?

**The solution**.  
The first thing to do is create the shortcode. Paste the following code in your _functions.php_ file:

<pre><code class="language-php">function imageresizer( $atts, $content = null ) {
  return '&lt;img src="https://www.smashingmagazine.com/wp-content/uploads/2009/10//timthumb/timthumb.php?src='.$content.'&amp;w=590" alt="" /&gt;';
}

add_shortcode('img', 'imageresizer');</code></pre>

Now, you can use the following syntax to add an automatically resized image to your blog post:

<pre><code class="language-php">[img]https://www.yoursite.com/yourimage.jpg[/img]</code></pre>

**Code explanation**.  
You have probably already noticed how cool WordPress shortcodes are and how they make your blogging life easier. This code simply creates a shortcode that takes a single parameter: the image's URL. Please notice that **it's not a good idea to resize large images this way** as it unnecessarily increases the server load – in such cases it's better to create and upload smaller images instead.

TimThumb resizes the image to 590 pixels wide, as specified on line 2 `(w=590)`. Of course, you can change this value or add a height parameter (e.g. `h=60`).

### Related Posts

You may be interested in the following related posts:

*   [10 Handy WordPress Comments Hacks](https://www.smashingmagazine.com/2009/07/23/10-wordpress-comments-hacks/)
*   [Power Tips For WordPress Template Developers](https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/)
*   [10 Useful WordPress Loop Hacks](https://www.smashingmagazine.com/2009/06/10/10-useful-wordpress-loop-hacks/)
*   [Custom Field Hacks For WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/)
*   [15 Useful Twitter Hacks and Plugins For WordPress](https://www.smashingmagazine.com/2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [Mastering WordPress Shortcuts](https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/)

{{< signature "al, il" >}}

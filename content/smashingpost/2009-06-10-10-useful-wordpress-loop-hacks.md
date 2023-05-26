---
title: 10 Useful WordPress Loop Hacks
slug: 10-useful-wordpress-loop-hacks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2da9cc6-52ad-4b5d-bae2-ba3a66a8bf75/illusearch11.jpg
date: 2009-06-10T07:28:33.000Z
author: jean-baptiste-jung
description: >-
  The loop is a very important aspect of WordPress blogs. In fact, the loop is what allows you to get posts from your WordPress database and print them on the screen. A set of useful and user-friendly functions, the loop is incredibly powerful. With it, you can get a single post, a list of posts ordered by date, title or category, a list of posts written by a specific author and much more.
categories:
  - WordPress
  - Hacks
  - Techniques (WP)
---
The loop is a very important aspect of WordPress blogs. In fact, the loop is what allows you to get posts from your WordPress database and print them on the screen. A set of useful and user-friendly functions, the loop is incredibly powerful. With it, you can get a single post, a list of posts ordered by date, title or category, a list of posts written by a specific author and much more.

In this article, we'll show you <strong>10 useful things you can do with the WordPress loop</strong> to make your blog even more powerful than it is right now.

## 1\. Get Posts Published Between Two Dates

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11f26ac7-7cef-4824-807b-d21f8b4c5dac/time.jpg" alt="Screenshot" width="400" height="265" /><br>
<em>Image source: Shutterstock</em>

{{% feature-panel %}}

<strong>The problem</strong>.
The loop and the <code>query_posts()</code> WordPress function allow you to easily retrieve a list of posts published in a specific week or month. Unfortunately, getting posts published between, for example, March 17 and May 3 isn't that easy. Let's solve this problem.

<strong>The solution</strong>.
Simply paste the following code wherever in your theme you'd like to display the list of posts published between two dates. Don't forget to replace the dates in the example with yours.

<pre><code class="language-php">&lt;?php function filter_where($where = ’) {
        $where .= " AND post_date &gt;= '2009-03-17' AND post_date &lt;= '2009-05-03'";
    return $where;
  }
add_filter('posts_where', 'filter_where');
query_posts($query_string);
while (have_posts()) :
      the_post();
      the_content();
endwhile;

?&gt;</code></pre>

<strong>Code explanation</strong>.
To achieve this hack, I first create a function named <code>filter_where()</code>, which contains an SQL "<code>WHERE</code>" condition. Then, before starting the loop, the <code>filter_where()</code> function is hooked into WordPress' <code>post_where()</code> function.

As a result, the "<code>WHERE</code>" clause contained in the <code>filter_where()</code> function is added to the end of the SQL query contained in the <code>post_where()</code> function, which means that the loop will return posts published only between the two dates specified in the <code>filter_where()</code> function.

### Source

*   [WordPress loop: Get posts published between two particular dates](https://www.wprecipes.com/wordpress-loop-get-posts-published-between-two-particular-dates)

## 2\. Use More Than One Loop On A Page, Without Printing Duplicate Posts

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2c1f016-b8b4-485b-9d1e-e0a14328d2ae/sm4.jpg" alt="Screenshot" />

<strong>The problem</strong>.
Most modern themes and all "magazine" themes display at least two loops on the blog's home page; these can be used, for example, for a "featured posts" section. While using two loops is very easy to do, preventing duplicate posts from displaying is not... until, that is, you learn this easy method of preventing them.

<strong>The solution</strong>.

1.  Let’s start with the first loop. Nothing hard here: we’re just going to get the eight most recent posts using the `showposts` parameter. Open the _index.php_ file, and paste the following code to output your “featured” posts:

        <?php
        query_posts('showposts=8');
        $ids = array();
        while (have_posts()) : the_post();
        $ids[] = get_the_ID();
        the_title();
        the_content();
        endwhile;
        ?>

2.  Once that's done, it’s time to apply our second loop and get all posts, excepted the ones we have already outputted in the first loop:

        <?php
        query_posts(array('post__not_in' => $ids));
        while (have_posts()) : the_post();
        the_title();
        the_content();
        endwhile;
        ?>

3.  Save your _index.php_ file and admire the results!

<strong>Code explanation</strong>.
The <strong>first loop</strong> starts with the very useful <code>query_posts()</code> function, which allows you to specify a wide range of parameters to be used by the loop. The <code>showposts</code> parameter allows you to get the specified number of posts. Just before the loop starts, I create a PHP array named <code>$ids</code>, which will receive all IDs of the posts returned by this loop.

Like the first one, the <strong>second loop</strong> uses the <code>query_posts()</code> function with the <code>post__not_in</code> parameter. This parameter allows you to specify a list of posts that you don't want to be displayed, in the form of a PHP array. As you probably saw, I passed the <code>$ids</code> array to this parameter so that any posts returned by the first loop would be returned again by the second loop.

## 3\. Insert Ads After The First Post

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d660d61e-57f5-4fa1-92fb-e72c1044158c/sm1.jpg" alt="Screenshot" />

<strong>The problem</strong>.
Advertising is a good way to monetize your blog. But to get advertisers, your ads must receive clicks by your visitors. Many bloggers display ads on the blog sidebar, footer or header, which isn't always great with click-through rates. To obtain more clicks on your ads and make your advertisers happy, inserting them after the first post is a good idea. Let's see how to do this in the WordPress loop.

<strong>The solution</strong>.
Simply use the following loop instead of your current loop. Don't forget to insert your ad code on line 6:

<pre><code class="language-php">&lt;?php if (have_posts()) : ?&gt;
&lt;?php $count = 0; ?&gt;
&lt;?php while (have_posts()) : the_post(); ?&gt;
&lt;?php $count++; ?&gt;
  &lt;?php if ($count == 2) : ?&gt;
          //Paste your ad code here
          &lt;h2&gt;&lt;a href="&lt;?php the_permalink(); ?&gt;"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/h2&gt;
          &lt;?php the_excerpt(); ?&gt;
   &lt;?php else : ?&gt;
          &lt;h2&gt;&lt;a href="&lt;?php the_permalink(); ?&gt;"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/h2&gt;
          &lt;?php the_excerpt(); ?&gt;
  &lt;?php endif; ?&gt;
&lt;?php endwhile; ?&gt;
&lt;?php endif; ?&gt;</code></pre>

<strong>Code explanation</strong>.
Since the early days of programming, integer variables have been a common operation to use as a counter. This is exactly what I've done here: just before the loop starts, a <code>$count</code> variable is created. This variable increases by an increment of 1 with each result returned by the loop.

Then, you just have to add an <code>if</code> structure (line 5) and see if <code>$count</code> is equal to 2. If it is, it means that the first post has already been returned and we can display the ads.</p>

### Source

*   [How to: Insert AdSense after the first post](https://www.wprecipes.com/how-to-insert-adsense-after-the-first-post)

## 4\. Get Posts With A Specific Custom Field And Specific Value

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c144129-9ad8-422e-b9b1-33babed7ff8b/sm3.png" alt="Screenshot" />

<strong>The problem</strong>.
Because of the popularity of <a href="https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/">WordPress' custom fields</a>, you will often want to be able to output a list of posts with a specific custom field and specific value. While so simple for advanced WordPress users, beginners continue to ask me about this on my blogs. So, here's the correct and easy way to achieve this.

<strong>The solution</strong>.
Not hard at all. We only have to use the <code>query_posts()</code> function with the <code>meta_key</code> and <code>meta_value</code> parameters:

<pre><code class="language-php">&lt;?php query_posts('meta_key=review_type&amp;meta_value=movie');  ?&gt;
&lt;?php if (have_posts()) : ?&gt;
&lt;?php while (have_posts()) : the_post(); ?&gt;</code></pre>

<strong>Code explanation</strong>.
Definitely nothing hard here. To get only posts with a specific custom field and specific value, you have to use the <code>query_posts()</code> function with the <code>meta_key</code> and <code>meta_value</code> parameters. The <code>meta_key</code> value is the name of the desired custom field, and <code>meta_value</code> is the desired value.</p>

### Source

*   How to Only Show Posts With a Specific Custom Field
*   [Easily get posts with a specific custom field/value on your WordPress blog](https://www.wprecipes.com/easily-get-posts-with-a-specific-custom-fieldvalue-on-your-wordpress-blog)

## 5\. List Upcoming Posts

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa1c3ccd-a839-4a18-b06f-a56d2978596a/sm5.jpg" alt="Screenshot" />

<strong>The problem</strong>.
Thanks to the "schedule post" option, our favorite blogging platform allows us to write a post and schedule it to be published later. To make sure your readers come back to your blog or subscribe to your RSS feed, listing your upcoming posts is a good idea.

<strong>The solution</strong>.

<pre><code class="language-php">&lt;?php query_posts('showposts=10&amp;post_status=future'); ?&gt;
&lt;?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?&gt;
    &lt;h2&gt;&lt;?php the_title(); ?&gt;&lt;/h2&gt;
    &lt;span class="datetime"&gt;&lt;?php the_time('j. F Y'); ?&gt;&lt;/span&gt;&lt;/p&gt;
&lt;?php endwhile;
else: ?&gt;&lt;p&gt;No future events scheduled.&lt;/p&gt;
&lt;?php endif; ?&gt;</code></pre>

<strong>Code explanation</strong>.
To achieve this, I used the <code>query_posts()</code> function with an interesting parameter called <code>post_status</code>. The <code>post_status</code> parameter allows you to get posts according to their published status ("published," "draft" or, like in this example, "future"). Because I also added the <code>showposts=10</code> parameter, this code will not return more than 10 upcoming posts.</p>

### Source

*   [How to: List future posts](https://www.wprecipes.com/how-to-list-future-posts)
*   [Image credit](https://wphackr.com/)

## 6\. Display Posts Published One Year Ago

<strong>The problem</strong>.
Many blogs have so much content and some very good older posts that should not be ignored. But most visitors end up seeing only the freshest content.

<strong>The solution</strong>.
If your blog is relatively old, why not showcase posts that were published over a year ago? Doing this is simple. Just insert the following code in your blog sidebar or <em>single.php</em> file.

<pre><code class="language-php">&lt;?php
$current_day = date('j');
$last_year = date('Y')-1;
query_posts('day='.$current_day.'&amp;year='.$last_year);
if (have_posts()):
    while (have_posts()) : the_post();
       the_title();
       the_excerpt();
    endwhile;
endif;
?&gt;</code></pre>

<strong>Code explanation</strong>.
The first thing was to get today's number, which we did on line 2, using the PHP <code>date()</code> function. Then, we had to get last year's number, which we easily did by taking <code>date('Y')</code> (which returns the current year) and subtracting 1, giving us last year's number.

Once that's done, we only have to pass the <code>$current_day</code> and <code>$last_year</code> variables to the <code>day</code> and <code>year</code> parameters of the <code>query_posts</code> WordPress function.

As an aside, if for some reason you want only today's posts, just delete line 3 and replace line 4 with the following:

<pre><code class="language-php">query_posts('day='.$current_day);</code></pre>

### Source

*   [How to: Get posts published exactly one year ago](https://www.wprecipes.com/how-to-get-posts-published-exactly-one-year-ago)

## 7\. Use The Loop To Create An "Archive" Page Template

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5ea31c5-80ae-4ac1-ae05-3ce9337543bd/sm7.png" alt="Screenshot" />

<strong>The problem</strong>.
As noted in the previous hack, a common problem on blogs is that it is hard for readers to find content published a while ago.

To help my readers finding what they're looking for, I created a WordPress page template that displays a list of all posts ever published on my blog. You can see a live demo of this hack on <a href="https://www.wprecipes.com/archives">WpRecipes</a>.

<strong>The solution</strong>.
If you don't know what a page template is or how to use one on your blog, you should first read this quick post to get started.

<pre><code class="language-php">&lt;?php
/*
Template Name: Archives
*/
?&gt;

&lt;?php get_header(); ?&gt;

  &lt;h2&gt;&lt;?php $numposts = $wpdb-&gt;get_var("SELECT COUNT(*) FROM $wpdb-&gt;posts WHERE post_status = 'publish'");
if (0 &lt; $numposts) $numposts = number_format($numposts); ?&gt;
&lt;h2&gt;&lt;?php echo $numposts.' recipes published since October 06, 2008'; ?&gt;
  &lt;/h2&gt;

  &lt;ul id="archive-list"&gt;
    &lt;?php
    $myposts = get_posts('numberposts=-1&amp;');
    foreach($myposts as $post) : ?&gt;
      &lt;li&gt;&lt;?php the_time('m/d/y') ?&gt;: &lt;a href="&lt;?php the_permalink(); ?&gt;"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;?php endforeach; ?&gt;
  &lt;/ul&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>

<strong>Code explanation</strong>.
The first thing to do is create a "page template." A page template is created by adding the following lines to the top of the file:

<pre><code class="language-php">&lt;?php
/*
Template Name: Archives
*/
?&gt;</code></pre>

An <strong>interesting part</strong> of this code is the post counter (line 8). This is done by creating a PHP variable named <code>$numposts</code> and using the <code>$wpdb</code> object to get the result from the SQL query sent to WordPress database.

Once that's done, we simply have to display the <code>$numposts</code> variable, and the total number of posts on your blog will be printed on the screen.

Now, let's have a closer look at the loop used in this code. As you probably saw, this code doesn't use the classic loop but rather uses the <code>get_posts()</code> function. <code>get_posts()</code> is a simple tag for creating multiple loops. We first take all posts from the engine and for each of these posts we present the date, the link and the title of the post. Simple and effective.</p>

### Source

*   [fahirsch asked: “How to list ALL posts on a page?”](https://www.wprecipes.com/fahirsch-asked-how-to-list-all-posts-on-a-page)

## 8\. Create Your Own WordPress Loops Using The WP_Query Object

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/504d76d3-159a-473d-bc44-299fd30ec47b/sm8.png" alt="Screenshot" />

<strong>The problem</strong>.
The classic WordPress loop, which is used in most hacks in this post, is both useful and user-friendly. However, particularly when using a lot of custom loops (for example, in complex "magazine" layouts), you risk problems with resetting, offsetting, invalid conditional tags and other annoyances.

<strong>The solution</strong>.
The solution is to use the <code>WP_Query</code> object and create your very own loop:

<pre><code class="language-php">&lt;?php
$myPosts = new WP_Query();
$myPosts-&gt;query('showposts=5');

while ($myPosts-&gt;have_posts()) : $myPosts-&gt;the_post(); ?&gt;
   the_title();
   the_content();
endwhile;

?&gt;</code></pre>

<strong>Code explanation</strong>.
The code above displays your five most recent posts. Here is what this code does in detail:

*   On line 2, I created a new `WP_Query` object, named `$myPosts`.
*   On line 3, I executed a query using the `showposts` parameter to get only the five most recent posts.
*   On line 5, our custom loop starts.
*   On line 6 and 7, we simply print some basic post information (title and post content)
*   On line 8, our custom loop ends.

If you want to display more or less than five posts, simply change the value of the <code>showposts</code> parameter on line 3.</p>

### Source

*   [Define Your Own WordPress Loop Using WP_Query](https://weblogtoolscollection.com/archives/2008/04/13/define-your-own-wordpress-loop-using-wp_query/)

## 9\. Get Only The Latest Sticky Posts

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddef18f4-640d-4bda-9a7d-cea2c2b06495/sm9.png" alt="Screenshot" />

<strong>The problem</strong>.
Introduced in WordPress 2.7, sticky posts are a very cool feature of our favorite blogging platform. A lot of WordPress users ask how to get only sticky posts in the loop.

<strong>The solution</strong>.
To display your five most recent sticky posts, just paste the following code anywhere in your theme files. If you want to display more or less sticky posts, just change the 5 to the desired value on line 4.

<pre><code class="language-php">&lt;?php
$sticky = get_option('sticky_posts');
rsort( $sticky );
$sticky = array_slice( $sticky, 0, 5);
query_posts( array( 'post__in' =&gt; $sticky, 'caller_get_posts' =&gt; 1 ) );

if (have_posts()) :
    while (have_posts()) : the_post();
        the_title();
        the_excerpt();
    endwhile;
endif;

?&gt;</code></pre>

<strong>Code explanation</strong>.
The first thing was to get all sticky posts (line 2). Then, we re-ordered them, displaying the most recent ones at the top, using the PHP <code>rsort()</code> function (line 3). On line 4, we got the five most recent sticky posts. As mentioned, you can change the amount of posts retrieved by changing 5 to any other value.

Once that's done, we use the <code>query_posts()</code> function to control the WordPress loop. Using the <code>post__in</code> parameter, we can make sure that the retrieved posts are contained in an array of values. This array is indeed our <code>$sticky</code> variable. Then, we just set up a basic loop and display the desired information from the post on the screen.</p>

### Sources

*   [Get the latest sticky posts in WordPress](https://justintadlock.com/archives/2009/03/28/get-the-latest-sticky-posts-in-wordpress)
*   [How to: Get latest sticky posts](https://www.wprecipes.com/how-to-get-latest-sticky-posts)
*   [Image credit](https://www.flickr.com/photos/aleksiaaltonen/)

## 10\. Create A Loop Of Images

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/581acd31-731a-4d5c-b6f7-a138974e4b2b/sm10.jpg" alt="Screenshot" />

<strong>The problem</strong>.
Nowadays, most blogs display post excerpts on the home page along with an image. How about being even more original and providing readers with a nice "gallery" page, listing however many of your recent posts, and displaying each post's lead image? Of course, we can easily achieve this with custom fields; but believe it or not, custom fields aren't necessary.

<strong>The solution</strong>.
To create our loop of images, we first need a PHP function that can grab the first image from each post and return its URL. To do this, paste the following function in your <em>functions.php</em> file. Don't forget to define a default image on line 10.

<pre><code class="language-php">function catch_that_image() {
  global $post, $posts;
  $first_img = ’;
  ob_start();
  ob_end_clean();
  $output = preg_match_all('/&lt;img.+src=['"]([^'"]+)['"].*&gt;/i', $post-&gt;post_content, $matches);
  $first_img = $matches [1] [0];

  if(empty($first_img)){ //Defines a default image
    $first_img = "/images/default.jpg";
  }
  return $first_img;
}</code></pre>

Once you've saved the <em>functions.php</em> file, you are now ready to display your image loop.

<pre><code class="language-php">&lt;?php
if (have_posts()) :
    while (have_posts()) : the_post(); ?&gt;
        &lt;a href="&lt;?php the_permalink();?&gt;" title="&lt;?php the_title(); ?&gt;" class="img-loop"&gt;
        &lt;img src="https://www.smashingmagazine.com/wp-content/uploads/images/wordpress-loop-hacks/&lt;?php echo catch_that_image() ?&gt;" alt="&lt;?php the_title(); ?&gt;" /&gt;
        &lt;/a&gt;
    endwhile;
endif;
?&gt;</code></pre>

<strong>Code explanation</strong>.
The first part of this code is the <code>catch_that_image()</code> function that we inclued in our <em>functions.php</em> file. Basically, this function parses the post's content using the <code>$post</code> and <code>$posts</code> global variables as well as a PHP regular expression. If no image is found (i.e. the post doesn't have one), the default image URL is returned. Otherwise, the function returns the URL of the first image in the post.

The second part of the code is the loop itself, and there's absolutely nothing hard about it. In fact, it is just a basic loop with no text content is displayed. Instead, the first image from the post is displayed, using the <code>catch_that_image()</code> function.</p>

### Sources

*   <span class="removed_link" title="https://wordpress.org/support/topic/246893">Retreive First Image From Post</span>
*   [How to: Get the first image from the post and display it](https://www.wprecipes.com/how-to-get-the-first-image-from-the-post-and-display-it)

## Related posts

You may be interested in the following related posts:

*   [100 Amazing Free WordPress Themes For 2009](https://www.smashingmagazine.com/2009/05/18/100-amazing-free-wordpress-themes-for-2009/)
*   [Custom Field Hacks For WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/)
*   [10 Exceptional WordPress Hacks](https://www.smashingmagazine.com/2009/04/15/10-exceptional-wordpress-hacks/)
*   [15 Useful Twitter Hacks and Plugins For WordPress](https://www.smashingmagazine.com/2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [Mastering WordPress Shortcuts](https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/)

{{< signature "al" >}}


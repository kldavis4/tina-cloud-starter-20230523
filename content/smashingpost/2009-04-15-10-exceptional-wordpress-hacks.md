---
title: 10 Exceptional WordPress Hacks
slug: 10-exceptional-wordpress-hacks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b60e8c6-9068-48e1-a82b-76af0568fe48/wpmanyillus45.jpg
date: 2009-04-15T11:37:29.000Z
author: jean-baptiste-jung
description: >-
  One of the reasons people love **WordPress** so much is its great flexibility. You can change the software's appearance with themes. You can enhance its functionality with plug-ins. And, last but not least, you can totally unleash WordPress' power with hacks.
categories:
  - WordPress
  - Hacks
  - Techniques (WP)
---
Today, let's do it again with <strong>10 new and totally killer WordPress hacks</strong> to make your blog stand out from the crowd. As usual, we won't just list the hacks alone. In each entry, you'll find an explanation of the code as well as the kinds of problems that the hack solves.

## 1\. Create TinyURLs On The Fly

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5451e3a-d2bb-4eba-ac1c-d38f9279dc35/sm1.jpg" alt="Screenshot" width="500" height="202" />

{{% feature-panel %}}

<strong>The problem</strong>. Because Twitter has become a social media revolution, many bloggers and Twitter users enjoy sharing blog posts they have found and liked on Twitter. However, manually creating a TinyURL before tweeting can get a little tedious. As you probably know, Twitter can bring a lot of traffic to your blog, so it is in your interest to consistently provide short URLs to your readers.

<strong>The solution</strong>. To use this recipe, follow the simple steps below:

1.  Open your _functions.php_ file.
2.  Paste the following code in the file:

        function getTinyUrl($url) {
            $tinyurl = file_get_contents("https://tinyurl.com/api-create.php?url=".$url);
            return $tinyurl;
        }

3.  Open your _single.php_ file and paste the following in the loop:

        <?php
        $turl = getTinyUrl(get_permalink($post->ID));
        echo 'Tiny Url for this post: <a href="'.$turl.'">'.$turl.'</a>'
        ?>

4.  That's all you need. Each of your posts now has its own TinyURL, ready for tweeting!

<strong>Code explanation</strong>. The popular URL shortening service TinyURL provides a quick API that creates TinyURLs on the fly. When you pass a URL to <em>https://tinyurl.com/api-create.php</em>, the API immediately prints the related TinyURL on the screen.

Using the PHP function file_get_contents(), we can get it and assign it to the $tinyurl variable. The last part of the code retrieves the post's permalink and passes it as a parameter to the getTinyUrl() function previously created.

Source:

*   [How to: Automatically provide TinyURLs for your WordPress blog posts](https://www.wprecipes.com/how-to-automatically-provide-tinyurls-for-your-wordpress-blog-posts)

## 2\. List Upcoming Posts

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f68415-190b-4a78-aeea-4358f7bf5b7c/sm8.jpg" alt="Screenshot" width="500" height="217" />

<strong>The problem</strong>. If you often schedule posts to be published, how about displaying them in a list? This will make your readers look forward to what you're going to publish in a few days and can help you reach new RSS subscribers. Implementing this functionality on your WordPress blog isn't hard at all.

<strong>The solution</strong>. Nothing hard here. Just copy this code and paste it anywhere in your theme files.

<pre><code class="language-php">&lt;div id="zukunft"&gt;
  &lt;div id="zukunft_header"&gt;&lt;p&gt;Future events&lt;/p&gt;&lt;/div&gt;

  &lt;?php query_posts('showposts=10&amp;post_status=future'); ?&gt;
  &lt;?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?&gt;
    &lt;div &gt;
      &lt;p class&gt;&lt;b&gt;&lt;?php the_title(); ?&gt;&lt;/b&gt;&lt;?php edit_post_link('e',' (',')'); ?&gt;&lt;br /&gt;

      &lt;span class="datetime"&gt;&lt;?php the_time('j. F Y'); ?&gt;&lt;/span&gt;&lt;/p&gt;
    &lt;/div&gt;
  &lt;?php endwhile; else: ?&gt;&lt;p&gt;No future events scheduled.&lt;/p&gt;&lt;?php endif; ?&gt;

&lt;/div&gt;</code></pre>

Once you've saved the file, your upcoming posts will be displayed on your blog.

<strong>Code explanation</strong>. This code use the super-powerful <em>query_posts()</em> WordPress function, which allows you to take control of the WordPress loop.

The parameter used is post_status, which allows you to get posts according to their status (published, draft, pending or future). The showposts parameter is also used to define how many items you'd like to get. You can change the value of this parameter on line 4 to retrieve more or less than ten posts.

Source:

*   [How to: List future posts](https://www.wprecipes.com/how-to-list-future-posts)

## 3\. Create A "Send To Facebook" Button

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a917a06-62fb-4f59-b77e-705491946a52/sm2.jpg" alt="Screenshot" width="500" height="227" />

<strong>The problem</strong>. In the first hack, we noted that Twitter can bring a lot traffic to your blog. Another website that can boost your traffic stats easily is Facebook. In this hack, let's see how we can create a "Send to Facebook" button for your WordPress blog.

<strong>The solution</strong>.

1.  Open the _single.php_ file in your theme.
2.  Paste the following code in the loop:

        <a href="https://www.facebook.com/sharer.php?u=<?php the_permalink();?>&t=<?php the_title(); ?>" target="blank">Share on Facebook</a>

3.  Alternatively, you could use the getTinyUrl() function to send a short URL to Facebook:

        <?php $turl = getTinyUrl(get_permalink($post->ID)); ?>
        <a href="https://www.facebook.com/sharer.php?u=<?php echo $turl;?>&t=<?php the_title(); ?>" target="blank">Share on Facebook</a>

4.  That's all. Your readers will now be able to share your blog post on Facebook with their friends!

<strong>Code explanation</strong>. This useful hack is very easy to understand: the only thing we do here is retrieve the post's permalink and title and send them as parameters to <em>https://www.facebook.com/sharer.php</em>.

In the alternative method, we used the getTinyUrl() function (created in the previous hack) to send a short URL instead of the post's permalink.

Source:

*   [How to: Add a “Share on Facebook” link to your WordPress blog](https://www.wprecipes.com/how-to-add-a-share-on-facebook-link-to-your-wordpress-blog)

## 4\. Create A Maintenance Page For Your WordPress Blog

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b970472-5147-4584-9539-17de3df223de/sm3.jpg" alt="Screenshot" width="500" height="222" />

<strong>The problem</strong>. One thing I really like about Drupal is the option to temporarily redirect visitors to a maintenance page. Sadly, WordPress doesn't have this feature. When you upgrade your blog, switch themes or make design changes, you may not want your visitors to see your blog as it is being tweaked, especially if it has design or code problems or, even worse, security gaps.

<strong>The solution</strong>. To solve this problem, we use the power of the <em>.htaccess</em> file. Just follow the steps below to get started.

1.  Create your maintenance page. A simple WordPress page is generally sufficient.
2.  Find your _.htaccess_ file (located at the root of your WordPress installation) and **create a back-up**.
3.  Open your _.htaccess_ file for editing.
4.  Paste the following code:

        RewriteEngine on
        RewriteCond %{REQUEST_URI} !/maintenance.html$
        RewriteCond %{REMOTE_ADDR} !^123.123.123.123
        RewriteRule $ /maintenance.html [R=302,L]

5.  Replace 123.123.123.123 on line 3 with your IP address ([Don't know it?](https://www.ip-adress.com/)). Make sure to use the same syntax.
6.  Now, all visitors except you will be redirected to your maintenance page.
7.  Once you're done tweaking, upgrading, theme switching or whatever, re-open your _.htaccess_ file and remove (or comment out) the redirection code.

<strong>Code explanation</strong>. The <em>.htaccess</em> file, which controls the Apache Web server, is very useful for these kinds of tasks.

In this example, we state that any visitor who has an IP different from 123.123.123.123 (which doesn't request <em>maintenance.html</em>) should be redirected to <em>maintenance.html</em>.

By replacing 123.123.123.123 with your own IP address, you make sure you're still allowed to browse your blog normally, while others are redirected to <em>maintenance.html</em>.

Source:

*   [10 awesome .htaccess hacks for WordPress](https://www.catswhocode.com/blog/10-awesome-htaccess-hacks-for-wordpress)

## 5\. Display Related Posts Without A Plug-In

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eabfb242-9996-47be-ae84-9758cc0d1cbe/sm4.jpg" alt="Screenshot" width="500" height="203" />

<strong>The problem</strong>. One well-known way of keeping visitors on your blog longer and helping them discover news posts is to display, usually at the end of the article, a list of related content.

Many plug-ins will do this job, but why not super-charge your theme by integrating this functionality by default?

<strong>The solution</strong>.

1.  Open the _single.php_ file in your theme.
2.  Paste the following code in the loop:

        <?php
        //for use in the loop, list 5 post titles related to first tag on current post
        $tags = wp_get_post_tags($post->ID);
        if ($tags) {
          echo 'Related Posts';
          $first_tag = $tags[0]->term_id;
          $args=array(
            'tag__in' => array($first_tag),
            'post__not_in' => array($post->ID),
            'showposts'=>5,
            'caller_get_posts'=>1
           );
          $my_query = new WP_Query($args);
          if( $my_query->have_posts() ) {
            while ($my_query->have_posts()) : $my_query->the_post(); ?>
              <p><a href="<?php the_permalink() ?>" rel="bookmark" title="Permanent Link to <?php the_title_attribute(); ?>"><?php the_title(); ?></a></p>
              <?php
            endwhile;
          }
        }
        ?>

3.  Save the file, and then have a look at your blog: related posts are automatically displayed!

<strong>Code explanation</strong>. This hack uses tags to retrieve related posts. The first thing it does is get the post's tags. If a post has tags, the first one is extracted and used in a query that retrieves posts with the same tag.

By default, this code displays up to five related posts. To change this number, simply edit line 9 of the code.

Source:

*   [How to: Show related posts without a plug-in](https://www.wprecipes.com/how-to-show-related-posts-without-a-plugin)

## 6\. Automatically Retrieve The First Image From Posts On Your Home Page

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0f11937-7a17-4cfc-9773-fbf2b14efea0/sm5.jpg" alt="Screenshot" width="500" height="230" />

<strong>The problem</strong>. Many WordPress users use custom fields to display a thumbnail on their blog home page. Of course, this is a nice solution, but how about automatically retrieving the first image from a post and using it as a thumbnail?

<strong>The solution</strong>. This hack is quite easy to implement:

1.  Open the _functions.php_ file in your theme.
2.  Paste this code in. Don't forget to specify a default image on line 10 (in case a post of yours does not have an image).

        function catch_that_image() {
          global $post, $posts;
          $first_img = ’;
          ob_start();
          ob_end_clean();
          $output = preg_match_all('/<img.+src=['"]([^'"]+)['"].*>/i', $post->post_content, $matches);
          $first_img = $matches [1] [0];

          if(empty($first_img)){ //Defines a default image
            $first_img = "/images/default.jpg";
          }
          return $first_img;
        }

3.  Save the _functions.php_ file.
4.  On your blog home page (_index.php_), call the function this way to get the URL of the first image from the post:

        <?php echo catch_that_image() ?>

<strong>Code explanation</strong>. The function uses the global variable $post to parse the post's content with a regular expression. If an image is found, its URL is returned by the function. If not, the default image URL is returned.

Source:

*   [How to: Get the first image from the post and display it](https://www.wprecipes.com/how-to-get-the-first-image-from-the-post-and-display-it)
*   <span class="removed_link" title="https://wordpress.org/support/topic/246893">Retreive first image from post</span>

## 7\. Resize Images On The Fly

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78b809c3-3466-4405-9088-9e21176b301f/sm6.jpg" alt="Screenshot" width="500" height="161" />

<strong>The problem</strong>. When you use thumbnails on your blog's home page or even images in posts, having to manually resize them is boring and wastes a lot of time. So, why not use the power of PHP to do it?

<strong>The solution</strong>. To achieve this hack, just follow these simple steps:

1.  Get this script and save it on your computer (I'll assume you've named it _timthumb.php_).
2.  Use an FTP program to connect to your server and create a new directory called _scripts_. Upload the _timthumb.php_ file to it.
3.  Once done, you can display images like so:

        <img loading="lazy" decoding="async" src="/scripts/timthumb.php?src=/images/whatever.jpg&h=150&w=150&zc=1" alt="Screenshot" />

    In other words, you just call the _timthumb.php_ file and pass your image as a parameter. The same goes for your desired width and height.

<strong>Code explanation</strong>. The <em>timthumb.php</em> script use the PHP GD library, which allows you to manipulate images dynamically with PHP. GD is installed by default on all servers running PHP5. If you're not running PHP5, you'll have to check if GD is installed before using this script.

The <em>timthumb.php</em> file gets the parameters you've passed to it (image URL, width and height) and uses it to create a new image with your stated dimensions. Once that's done, the image is returned to you.

Source:

*   TimThumb PHP script released
*   [How to: Resize images on the fly](https://www.wprecipes.com/how-to-resize-images-on-the-fly)

## 8\. Get Your Most Popular Posts Without A Plug-In

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67501522-e003-453d-86f5-b62a5f50a9d1/sm7.jpg" alt="Screenshot" width="500" height="196" />

<strong>The problem</strong>. Displaying your most popular posts is a good way to make visitors stay longer on your blog, as is displaying related posts. Many great plug-ins can list your most popular posts, but again, why use a plug-in when you can simply hack your WordPress theme to do it automatically?

<strong>The solution</strong>. Just paste the following code anywhere in your theme files (for example, in <em>sidebar.php</em>). To change the number of displayed posts, simply change the "5" on line 3 to your desired number.

<pre><code class="language-php">&lt;h2&gt;Popular Posts&lt;/h2&gt;
&lt;ul&gt;
&lt;?php $result = $wpdb-&gt;get_results("SELECT comment_count,ID,post_title FROM $wpdb-&gt;posts ORDER BY comment_count DESC LIMIT 0 , 5");
foreach ($result as $post) {
setup_postdata($post);
$postid = $post-&gt;ID;
$title = $post-&gt;post_title;
$commentcount = $post-&gt;comment_count;
if ($commentcount != 0) { ?&gt;

&lt;li&gt;&lt;a href="&lt;?php echo get_permalink($postid); ?&gt;" title="&lt;?php echo $title ?&gt;"&gt;
&lt;?php echo $title ?&gt;&lt;/a&gt; {&lt;?php echo $commentcount ?&gt;}&lt;/li&gt;
&lt;?php } } ?&gt;

&lt;/ul&gt;</code></pre>

<strong>Code explanation</strong>. This code executes an SQL query to the WordPress database, using the $wpdb object, to get a list of the five posts with the most comments. The results are then wrapped in an unordered HTML list and displayed on screen.

Source:

*   [Create your own popular posts page](https://www.problogdesign.com/wordpress/create-your-own-popular-posts-page/)

## 9\. Highlight Searched Text In Search Results

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55b88918-d2c1-473f-84ff-3defad1b3e66/sm9.jpg" alt="Screenshot" width="500" height="93" />

<strong>The problem</strong>. The WordPress search engine system is often criticized for not being powerful enough. One of its weakest points in my opinion is that searched text is not easily distinguishable from the rest of the text. Let's solve that!

<strong>The solution</strong>.

1.  Open your _search.php_ file and find the the_title() function.
2.  Replace it with the following:

        echo $title;

3.  Now, just before the modified line, add this code:

        <?php
          $title  = get_the_title();
          $keys= explode(" ",$s);
          $title  = preg_replace('/('.implode('|', $keys) .')/iu',
            '<strong class="search-excerpt"></strong>',
            $title);
        ?>

4.  Save the _search.php_ file and open _style.css_. Add the following line to it:

        strong.search-excerpt { background: yellow; }

That's all. Better, isn't it?

<strong>Code explanation</strong>. Once again, regular expressions are a lifesaver. The regexp parses the $s content ($s is the variable containing the searched text) and automatically adds a <em>&lt;strong class="search-excerpt"&gt;</em> element around any occurrences of $s.

Then, you simply modify your <em>style.css</em> file to give searched text a special style and make it more visible to your readers.

Sources:

*   [Make WordPress' search function suck less.](https://yoast.com/wordpress-search/)
*   [How to: Highlight searched text in search results](https://www.wprecipes.com/how-to-enlight-searched-text-in-search-results)

## 10\. Disable Widgetized Areas Without Editing Theme Files

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f56331c5-4904-4906-b199-d6612cd7558b/sm10.jpg" alt="Screenshot" width="500" height="255" />

<strong>The problem</strong>. Widgets are very useful, but sometimes you don't need them on a particular page or post. Sure, you can create a page template for a particular page or even remove the widgetized zone from the code, but a much better and more elegant solution exists.

<strong>The solution</strong>. To do this, simply add the following code to your <em>functions.php</em> file:

<pre><code class="language-php">&lt;?php
add_filter( 'sidebars_widgets', 'disable_all_widgets' );

function disable_all_widgets( $sidebars_widgets ) {
  if ( is_home() )
    $sidebars_widgets = array( false );
  return $sidebars_widgets;
}
?&gt;</code></pre>

<strong>Code explanation</strong>. This code first adds a filter to the sidebars_widgets WordPress function. Now every time WordPress tries to execute this function, it will execute the disable_all_widgets function we just created.

The disable_all_widgets function uses WordPress conditional tags (in this example, is_home(), but you can use any conditional tag) to disable all widgets if a visitor is on a particular page or post.

Source:

        function catch_that_image() {
          global $post, $posts;
          $first_img = ’;
          ob_start();
          ob_end_clean();
          $output = preg_match_all('/<img.+src=['"]([^'"]+)['"].*>/i', $post->post_content, $matches);
          $first_img = $matches [1] [0];

          if(empty($first_img)){ //Defines a default image
            $first_img = "/images/default.jpg";
          }
          return $first_img;
        }

3.  Save the _functions.php_ file.
4.  On your blog home page (_index.php_), call the function this way to get the URL of the first image from the post:

        <?php echo catch_that_image() ?>

<strong>Code explanation</strong>. The function uses the global variable $post to parse the post's content with a regular expression. If an image is found, its URL is returned by the function. If not, the default image URL is returned.

Source:

*   [How to: Get the first image from the post and display it](https://www.wprecipes.com/how-to-get-the-first-image-from-the-post-and-display-it)
*   <span class="removed_link" title="https://wordpress.org/support/topic/246893">Retreive first image from post</span>

## 7\. Resize Images On The Fly

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78b809c3-3466-4405-9088-9e21176b301f/sm6.jpg" alt="Screenshot" width="500" height="161" />

<strong>The problem</strong>. When you use thumbnails on your blog's home page or even images in posts, having to manually resize them is boring and wastes a lot of time. So, why not use the power of PHP to do it?

<strong>The solution</strong>. To achieve this hack, just follow these simple steps:

1.  Get this script and save it on your computer (I'll assume you've named it _timthumb.php_).
2.  Use an FTP program to connect to your server and create a new directory called _scripts_. Upload the _timthumb.php_ file to it.
3.  Once done, you can display images like so:

        <img loading="lazy" decoding="async" src="/scripts/timthumb.php?src=/images/whatever.jpg&h=150&w=150&zc=1" alt="Screenshot" />

    In other words, you just call the _timthumb.php_ file and pass your image as a parameter. The same goes for your desired width and height.

<strong>Code explanation</strong>. The <em>timthumb.php</em> script use the PHP GD library, which allows you to manipulate images dynamically with PHP. GD is installed by default on all servers running PHP5. If you're not running PHP5, you'll have to check if GD is installed before using this script.

The <em>timthumb.php</em> file gets the parameters you've passed to it (image URL, width and height) and uses it to create a new image with your stated dimensions. Once that's done, the image is returned to you.

Source:

*   TimThumb PHP script released
*   [How to: Resize images on the fly](https://www.wprecipes.com/how-to-resize-images-on-the-fly)

## 8\. Get Your Most Popular Posts Without A Plug-In

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67501522-e003-453d-86f5-b62a5f50a9d1/sm7.jpg" alt="Screenshot" width="500" height="196" />

<strong>The problem</strong>. Displaying your most popular posts is a good way to make visitors stay longer on your blog, as is displaying related posts. Many great plug-ins can list your most popular posts, but again, why use a plug-in when you can simply hack your WordPress theme to do it automatically?

<strong>The solution</strong>. Just paste the following code anywhere in your theme files (for example, in <em>sidebar.php</em>). To change the number of displayed posts, simply change the "5" on line 3 to your desired number.

<pre><code class="language-php">&lt;h2&gt;Popular Posts&lt;/h2&gt;
&lt;ul&gt;
&lt;?php $result = $wpdb-&gt;get_results("SELECT comment_count,ID,post_title FROM $wpdb-&gt;posts ORDER BY comment_count DESC LIMIT 0 , 5");
foreach ($result as $post) {
setup_postdata($post);
$postid = $post-&gt;ID;
$title = $post-&gt;post_title;
$commentcount = $post-&gt;comment_count;
if ($commentcount != 0) { ?&gt;

&lt;li&gt;&lt;a href="&lt;?php echo get_permalink($postid); ?&gt;" title="&lt;?php echo $title ?&gt;"&gt;
&lt;?php echo $title ?&gt;&lt;/a&gt; {&lt;?php echo $commentcount ?&gt;}&lt;/li&gt;
&lt;?php } } ?&gt;

&lt;/ul&gt;</code></pre>

<strong>Code explanation</strong>. This code executes an SQL query to the WordPress database, using the $wpdb object, to get a list of the five posts with the most comments. The results are then wrapped in an unordered HTML list and displayed on screen.

Source:

*   [Create your own popular posts page](https://www.problogdesign.com/wordpress/create-your-own-popular-posts-page/)

## 9\. Highlight Searched Text In Search Results

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55b88918-d2c1-473f-84ff-3defad1b3e66/sm9.jpg" alt="Screenshot" width="500" height="93" />

<strong>The problem</strong>. The WordPress search engine system is often criticized for not being powerful enough. One of its weakest points in my opinion is that searched text is not easily distinguishable from the rest of the text. Let's solve that!

<strong>The solution</strong>.

1.  Open your _search.php_ file and find the the_title() function.
2.  Replace it with the following:

        echo $title;

3.  Now, just before the modified line, add this code:

        <?php
          $title  = get_the_title();
          $keys= explode(" ",$s);
          $title  = preg_replace('/('.implode('|', $keys) .')/iu',
            '<strong class="search-excerpt"></strong>',
            $title);
        ?>

4.  Save the _search.php_ file and open _style.css_. Add the following line to it:

        strong.search-excerpt { background: yellow; }

That's all. Better, isn't it?

<strong>Code explanation</strong>. Once again, regular expressions are a lifesaver. The regexp parses the $s content ($s is the variable containing the searched text) and automatically adds a <em>&lt;strong class="search-excerpt"&gt;</em> element around any occurrences of $s.

Then, you simply modify your <em>style.css</em> file to give searched text a special style and make it more visible to your readers.

Sources:

*   [Make WordPress' search function suck less.](https://yoast.com/wordpress-search/)
*   [How to: Highlight searched text in search results](https://www.wprecipes.com/how-to-enlight-searched-text-in-search-results)

## 10\. Disable Widgetized Areas Without Editing Theme Files

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f56331c5-4904-4906-b199-d6612cd7558b/sm10.jpg" alt="Screenshot" width="500" height="255" />

<strong>The problem</strong>. Widgets are very useful, but sometimes you don't need them on a particular page or post. Sure, you can create a page template for a particular page or even remove the widgetized zone from the code, but a much better and more elegant solution exists.

<strong>The solution</strong>. To do this, simply add the following code to your <em>functions.php</em> file:

<pre><code class="language-php">&lt;?php
add_filter( 'sidebars_widgets', 'disable_all_widgets' );

function disable_all_widgets( $sidebars_widgets ) {
  if ( is_home() )
    $sidebars_widgets = array( false );
  return $sidebars_widgets;
}
?&gt;</code></pre>

<strong>Code explanation</strong>. This code first adds a filter to the sidebars_widgets WordPress function. Now every time WordPress tries to execute this function, it will execute the disable_all_widgets function we just created.

The disable_all_widgets function uses WordPress conditional tags (in this example, is_home(), but you can use any conditional tag) to disable all widgets if a visitor is on a particular page or post.

Source:

*   [Disable widget areas (sidebars) without touching theme templates](https://justintadlock.com/archives/2009/03/06/disable-widget-areas-without-touching-theme-templates)

## Related posts

You may be interested in the following related posts:

*   [15 Useful Twitter Hacks and Plug-Ins For WordPress](https://www.smashingmagazine.com/2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [Mastering WordPress Shortcodes](https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/)
*   [10 Steps To Protect The Admin Area In WordPress](https://www.smashingmagazine.com/2009/01/26/10-steps-to-protect-the-admin-area-in-wordpress/)
*   [8 Useful WordPress SQL Hacks](https://www.smashingmagazine.com/2008/12/18/8-useful-wordpress-sql-hacks/)
*   [10 Useful RSS-Tricks and Hacks For WordPress](https://www.smashingmagazine.com/2008/12/02/10-useful-rss-hacks-for-wordpress/)

{{< signature "al" >}}


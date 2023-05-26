---
title: 10 Handy WordPress Comments Hacks
slug: 10-wordpress-comments-hacks
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2c0d559-96ad-40da-acf5-42dc84abbe78/alfred-extension-illu.jpg
date: 2009-07-23T07:31:18.000Z
author: jean-baptiste-jung
description: >-
  Comments sections are neglected on many blogs. That is definitely a bad thing,
  because comments represent interaction between you and your readers. In this article, we'll have a look at 10 great tips and hacks to enhance your blog's comments section and give it the quality it deserves.
categories:
  - WordPress
  - Hacks
  - Comments
  - Techniques (WP)
---
Comments sections are neglected on many blogs. That is definitely a bad thing, because comments represent interaction between you and your readers. In this article, we'll have a look at 10 great tips and hacks to enhance your blog's comments section and give it the quality it deserves.

## 1\. Add Action Links To Comments

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e613acf9-a835-4c62-86fb-eb2a579fee6c/sm1.png" alt="Screenshot" width="500" height="140" />

{{% feature-panel %}}

<strong>The problem</strong>.
Whether or not you allow readers to add comments without having to be approved, you will often need to edit, delete or mark certain comments as spam. By default, WordPress shows the "Edit" link on comments (using the <code>edit_comment_link()</code> function) but not "Delete" or "Spam" links. Let's add them.

<strong>The solution</strong>.
First, we have to create a function. Paste the code below in your <em>functions.php</em> file:

<pre><code class="language-php">function delete_comment_link($id) {
  if (current_user_can('edit_post')) {
    echo '| &lt;a href="'.admin_url("comment.php?action=cdc&amp;c=$id").'"&gt;del&lt;/a&gt; ';
    echo '| &lt;a href="'.admin_url("comment.php?action=cdc&amp;dt=spam&amp;c=$id").'"&gt;spam&lt;/a&gt;';
  }
}</code></pre>

Once you have saved <em>functions.php</em>, open up your <em>comments.php</em> file, and add the following code where you want the "Delete" and "Spam" links to appear. They must go in the comment loop. In most themes, you'll find an <code>edit_comment_link()</code> declaration. Add the code in just after that.

<pre><code class="language-php">delete_comment_link(get_comment_ID());</code></pre>

<strong>Code explanation</strong>.
The first thing we did, of course, was to make sure the current user has permission to edit comments. If so, links to delete and mark a comment as spam are displayed. Note the use of the <code>admin_url()</code> function, which allows you to retrieve your blog admin's URL.

<strong>Source:</strong>

*   [How to: Add "Delete" and "Spam" buttons to your comments.](https://www.wprecipes.com/how-to-add-del-and-spam-buttons-to-your-comments)

## 2\. Separate TrackBacks From Comments

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92363a6f-a10b-4601-aad6-07baefd9052d/sm2.png" alt="Screenshot" width="500" height="177" />

<strong>The problem</strong>.
Do your posts have a lot of TrackBacks? Mine do. Trackbacks are cool because they allow your readers to see which articles from other blogs relate to yours. But the more TrackBacks you have, the harder the discussion is to follow. Separating comments from TrackBacks, then, is definitely something to consider, especially if you do not use the "Reply" capabilities introduced in WordPress 2.7.

<strong>The solution</strong>.
Open and edit the <em>comments.php</em> file in your theme. Find the comment loop, which looks like the following:

<pre><code class="language-php">foreach ($comments as $comment) : ?&gt;
    // Comments are displayed here
endforeach;</code></pre>

Once you have that, replace it with the code below:

<pre><code class="language-php">&lt;ul class="commentlist"&gt;
    &lt;?php //Displays comments only foreach ($comments as $comment) : ?&gt;
        &lt;?php $comment_type = get_comment_type(); ?&gt;
        &lt;?php if($comment_type == 'comment') { ?&gt;
      &lt;li&gt;//Comment code goes here&lt;/li&gt;
  &lt;?php }
    endforeach;
&lt;/ul&gt;

&lt;ul&gt;
    &lt;?php //Displays trackbacks only foreach ($comments as $comment) : ?&gt;
        &lt;?php $comment_type = get_comment_type(); ?&gt;
        &lt;?php if($comment_type != 'comment') { ?&gt;
      &lt;li&gt;&lt;?php comment_author_link() ?&gt;&lt;/li&gt;
  &lt;?php }
    endforeach;

&lt;/ul&gt;</code></pre>

<strong>Code explanation</strong>.
Nothing hard about this code. The <code>get_comment_type()</code> function tells you if something is a regular comment or a TrackBack. We simply have to create two HTML lists, filling the first with regular comments and the second with TrackBacks.

<strong>Source:</strong>

*   [Jamie asks: How do I display comments and TrackBacks separately?](https://www.wprecipes.com/jamie-asked-how-can-i-display-comments-and-trackbacks-separately)

## 3\. Get Rid Of HTML Links In Comments

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/734fadc2-0643-415f-8de0-901016f46b76/sm3.png" alt="Screenshot" width="500" height="137" />

<strong>The problem</strong>.
Bloggers are always looking to promote their blogs, and spammers are everywhere. One thing that totally annoys me on my blogs is the incredible amount of links left in comments, which are usually irrelevant. By default, WordPress transforms URLs in comments to links. Thankfully, if you're as tired of comment links as I am, this can be overwritten.

<strong>The solution</strong>.
Simply open your <em>function.php</em> file and paste in this code:

<pre><code class="language-php">function plc_comment_post( $incoming_comment ) {
  $incoming_comment['comment_content'] = htmlspecialchars($incoming_comment['comment_content']);
  $incoming_comment['comment_content'] = str_replace( "'", '&amp;apos;', $incoming_comment['comment_content'] );
  return( $incoming_comment );
}

function plc_comment_display( $comment_to_display ) {
  $comment_to_display = str_replace( '&amp;apos;', "'", $comment_to_display );
  return $comment_to_display;
}

add_filter('preprocess_comment', 'plc_comment_post', ’, 1);
add_filter('comment_text', 'plc_comment_display', ’, 1);
add_filter('comment_text_rss', 'plc_comment_display', ’, 1);
add_filter('comment_excerpt', 'plc_comment_display', ’, 1);</code></pre>

Once you have saved the file, say goodbye to links and other undesirable HTML in your comments.

<strong>Code explanation</strong>.
The first thing we did was create two functions that replace HTML characters with HTML entities. Then, using the powerful <code>add_filter()</code> WordPress function, we hooked the standard WordPress comments processing functions to the two functions we just created. This makes sure that any comments added will have their HTML filtered out.

<strong>Sources:</strong>

*   [How to: get rid of links in your comments](https://www.wprecipes.com/how-to-get-rid-of-links-in-your-comments)
*   [How to disable HTML in WordPress comments](https://www.theblog.ca/literal-comments)

## 4\. Use Twitter Avatars In Comments

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/938bb221-3692-46db-9e1c-f3356e9dd5d1/sm4.png" alt="Screenshot" width="500" height="246" />

<strong>The problem</strong>.
Bloggers find Twitter very useful because it allows them to promote their blog and stay connected to other bloggers and their own audience. Because of Twitter's popularity, why not illustrate comments with Twitter avatars instead of the normal gravatars?

<strong>The solution</strong>.

1.  The first thing to do is get the functions file [here](https://www.smashingmagazine.com/2009/01/08/twitter-avatars-in-comments-wordpress-plugin/).
2.  Once you have that, unzip the archive to your hard drive, and then open the _twittar.php_ file.
3.  Select all of its content and paste it to your blog's _functions.php_ file.
4.  The last thing to do is open your _comments.php_ file and find the comments loop.
5.  Paste the following line in the comments loop:

        <?php twittar('45', 'default.png', '#e9e9e9', 'twitavatars', 1, 'G'); ?>

<strong>Code explanation</strong>.
Some months ago here at Smashing Magazine, an awesome plug-in named <em>Twittar</em> was released. Its purpose is to allow you to use Twitter avatars on your WordPress blog. Because of the number of requests I received from WpRecipes.com readers, I decided to turn the plug-in into a hack, for people who prefer hacks to plug-ins.

Of course, you could simply <strong>install the plug-in</strong> rather than insert its content into your <em>function.php</em> file. It's up to you.

<strong>Sources:</strong>

*   [Twitter avatars in comments](https://www.smashingmagazine.com/2009/01/08/twitter-avatars-in-comments-wordpress-plugin/)
*   [How to: Use Twitter avatars in comments](https://www.wprecipes.com/ho-to-use-twitter-avatars-in-comments)

## 5\. Set Apart Author Comments With Style

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/918b85c3-478f-4fc3-bb76-44e36cf1289e/sm5.jpg" alt="Screenshot" width="500" height="175" />

<strong>The problem</strong>.
For blog posts that have a lot of comments, finding the author's comments and responses to reader questions is not always easy, especially if the blog don't have WordPress 2.7's threaded comments feature. Happily, it is possible to give author comments a different style so that readers can always quickly find your answers.

<strong>The solution</strong>.

1.  Open the _comments.php_ file and find the comment loop:

        <?php foreach comment as $comment) { ?>

2.  After that line, paste in the following:

        <?php
        $isByAuthor = false;
        if($comment->comment_author_email == get_the_author_email()) {
        $isByAuthor = true;
        }
        ?>

3.  Once that's done, find the line of code that represents comments (it may vary depending on your theme):

        <li class="<?php echo $oddcomment; ?>" id="comment-<?php comment_ID() ?>">

4.  Now we have to output the `authorcomment` class if the comment was made by the author:

        <li class="<?php echo $oddcomment; ?> <?php if($isByAuthor ) {
         echo 'authorcomment';} ?>" id="comment-<?php comment_ID() ?>">

5.  The last thing we do is create a CSS class for author comments. Open the _style.css_ file and insert the code. Replace the example colors with your colors of choice.

        .authorcomment{
          color:#fff;
          font-weight:bold;
          background:#068;
        }

<strong>Code explanation</strong>.
Basically, this code compares each email address left by a commentator to the author's email address. If they match, the <code>$isByAuthor</code> is set to <code>true</code>. When comments are displayed on screen, the value of <code>$isByAuthor</code> is checked. If it returns <code>true</code>, then the <code>authorcomment</code> class is added to the container.

It can be done more easily on Wordpress 2.7+ by just adding `comment_class();` to the comment’s DIV, which automatically adds the class `bypostauthor` when you’re commenting on your own post (_Thanks, Nima!_).

<strong>Source:</strong>

*   [Highlight Author Comments in WordPress](https://aonach.com/chatter/highlight-author-comments-in-wordpress/)

## 6\. Display Total Number Of Comments And Average Number Of Comments Per Post

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4d1baac-0051-4147-9a1f-571f1d782927/sm6.png" alt="Screenshot" width="500" height="310" />

<strong>The problem</strong>.
On your blog's dashboard, WordPress tells you how many total comments your blog has received. Unfortunately, there's no function for displaying this information publicly. Displaying the total number of comments on your blog and average number of comments per post can be very helpful, especially if you have a page for advertising opportunities.

<strong>The solution</strong>.

<pre><code class="language-php">&lt;?php
$count_posts = wp_count_posts();
$posts = $count_posts-&gt;publish;

$count_comments = get_comment_count();
$comments  = $count_comments['approved'];

echo "There's a total of ".$comments." comments on my blog, with an average ".round($comments/$posts)." comments per post.";
?&gt;</code></pre>

<strong>Code explanation</strong>.
Introduced in version 2.5, the <code>wp_count_posts()</code> and <code>get_comment_count()</code> functions allow you to easily retrieve the total number of posts and comments, respectively, on your WordPress blog. To derive the average number of comments per post, we have to do a bit of simple math, using the PHP <code>round()</code> function to make sure we end up with an integer.

<strong>Source:</strong>

*   [How to: Display your average number of comments per posts](https://www.wprecipes.com/how-to-display-your-average-comments-per-posts)

## 7\. Display X Number Of Most Recent Comments

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df054176-e022-4771-b4b9-f3d703f748e4/sm7.jpg" alt="Screenshot" width="544" height="289" />

<strong>The problem</strong>.
By default, WordPress provides a widget that outputs a list of however many of the most recent comments. This is great, but sometimes you want this functionality without a widget.

<strong>The solution</strong>.
This hack is very simple: just paste this code wherever you need a certain number of the most recent comments to be displayed. Don't forget to specify the actual number on line 3 (after the <code>LIMIT</code> SQL clause).

<pre><code class="language-php">&lt;?php
  $pre_HTML ="";
  $post_HTML ="";
  global $wpdb;
  $sql = "SELECT DISTINCT ID, post_title, post_password, comment_ID, comment_post_ID, comment_author, comment_date_gmt, comment_approved, comment_type,comment_author_url, SUBSTRING(comment_content,1,30) AS com_excerpt FROM $wpdb-&gt;comments LEFT OUTER JOIN $wpdb-&gt;posts ON ($wpdb-&gt;comments.comment_post_ID = $wpdb-&gt;posts.ID) WHERE comment_approved = '1' AND comment_type = ’ AND post_password = ’ ORDER BY comment_date_gmt DESC LIMIT 10";

  $comments = $wpdb-&gt;get_results($sql);
  $output = $pre_HTML;
  $output .= "n&lt;ul&gt;";
  foreach ($comments as $comment) {
    $output .= "n&lt;li&gt;".strip_tags($comment-&gt;comment_author) .":" . "&lt;a href="" . get_permalink($comment-&gt;ID)."#comment-" . $comment-&gt;comment_ID . "" title="on ".$comment-&gt;post_title . ""&gt;" . strip_tags($comment-&gt;com_excerpt)."&lt;/a&gt;&lt;/li&gt;";
  }
  $output .= "n&lt;/ul&gt;";
  $output .= $post_HTML;
  echo $output;
?&gt;</code></pre>

<strong>Code explanation</strong>.
As in the last hack, we use the <code>$wpdb</code> object here, too, this time with the <code>get_results()</code> method. Once the comments have been retrieved by the WordPress database, we simply use a <code>for</code> loop to concatenate the comments into an HTML unordered list. The <code>$pre_HTML</code> and <code>$post_HTML</code> variables, initialized at the top of this code, allow you to define which content should go before and after the comments list.

<strong>Sources:</strong>

*   [How to: List most recent comments](https://www.wprecipes.com/how-to-list-most-recent-comments)
*   Huge Compilation of WordPress Code

## 8\. Easily Prevent Comment Spam

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4d12e9f-56af-4782-88d9-71bd25dd3b08/sm8.jpg" alt="Screenshot" width="500" height="279" />

<strong>The problem</strong>.
Comment spam is such a pain for everyone. Akismet is a good solution, but why not block spammers outright instead of just marking their comments as suspected spam? This code looks for the HTTP referrer (the page where the request comes from) and automatically blocks the comment if the referrer is incorrect or not defined.

<strong>The solution</strong>.
Paste the following code in your <em>functions.php</em> file:

<pre><code class="language-php">function check_referrer() {
    if (!isset($_SERVER['HTTP_REFERER']) || $_SERVER['HTTP_REFERER'] == “”) {
        wp_die( __('Please enable referrers in your browser, or, if you're a spammer, bugger off!') );
    }
}

add_action('check_comment_flood', 'check_referrer');</code></pre>

That's all. Once you've saved the file, your blog will have a new level of protection against spam.

<strong>Code explanation</strong>.
This code automatically rejects any request for comment posting coming from a browser (or, more commonly, a bot) that has no referrer in the request. Checking is done with the PHP <code>$_SERVER[]</code> array. If the referrer is not defined or is incorrect, the <code>wp_die</code> function is called and the script stops its execution.

This function is hooked to WordPress' <code>check_comment_flood()</code> function. This way, we can be sure that our <code>check_referrer()</code> function is called each time a comment is posted.

<strong>Source:</strong>

*   [Yoast.com](https://yoast.com/)

## 9\. Keep WordPress Backwards Compatible With Versions Older Than 2.7

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba14c589-ff79-439a-820f-f07809291b4b/sm9.jpg" alt="Screenshot" width="500" height="230" />

<strong>The problem</strong>.
Released some months ago, WordPress 2.7 introduced a totally new commenting system, allowing you to thread comments and display them on separate pages. Although this is great, keep in mind if you are creating a theme for a client or for online distribution that many users still haven't upgraded their installation to version 2.8 or even 2.7. This code allows 2.7+ users to benefit from the new commenting system, while keeping the old system functional for people with older versions.

<strong>The solution</strong>.
You'll need two files for this recipe: the first is a WordPress 2.7 compatible comments file called <em>comments.php</em>. The second is a comment template for older WordPress versions called <em>legacy.comments.php</em>. Both of these files go in your theme directory.

Paste this code in your <em>functions.php</em> file.

<pre><code class="language-php">&lt;?php
add_filter('comments_template', 'legacy_comments');

function legacy_comments($file) {
  if(!function_exists('wp_list_comments')) : // WP 2.7-only check
    $file = TEMPLATEPATH.'/legacy.comments.php';
  endif;
  return $file;
}
?&gt;</code></pre>

<strong>Code explanation</strong>.
This code creates a function called <code>legacy_comments()</code>, which is hooked to WordPress <code>comments_template</code> function. Each time WordPress calls <code>comments_template()</code>, our <code>legacy_comments()</code> function is executed. If the <code>wp_list_comments()</code> function doesn't exist, the code automatically loads <em>legacy.comments.php</em> instead of <em>comments.php</em>.

<strong>Sources:</strong>

*   [Making your theme’s comments compatible with WordPress 2.7 and earlier versions](https://justintadlock.com/archives/2008/11/01/making-your-themes-comments-compatible-with-wordpress-27-and-earlier-versions)
*   [How to: make your comments template compatible with WordPress 2.7 and older versions](https://www.wprecipes.com/how-to-make-your-comments-template-compatible-with-wordpress-27-and-older-versions)

## 10\. Display Most Commented Posts From A Certain Period

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c5eab39-6350-426c-9207-e7eb74c36c15/sm10.png" alt="Screenshot" width="500" height="293" />

<strong>The problem</strong>.
Number of comments is a good way to measure a blog post's popularity and is a good filter for displaying a list of your most popular posts. Another great idea is to restrict a list of your most popular posts to a particular period, like "Last month's most popular posts," for example.

<strong>The solution</strong>.
Simply paste the following code where you'd like your most commented posts to be displayed. Don't forget to change the dates values on line 3 according to your needs.

<pre><code class="language-php">&lt;ul&gt;
&lt;?php
$result = $wpdb-&gt;get_results("SELECT comment_count,ID,post_title, post_date FROM $wpdb-&gt;posts WHERE post_date BETWEEN '2009-06-01' AND '2009-07-01' ORDER BY comment_count DESC LIMIT 0 , 10");

foreach ($result as $topten) {
    $postid = $topten-&gt;ID;
    $title = $topten-&gt;post_title;
    $commentcount = $topten-&gt;comment_count;
    if ($commentcount != 0) {
    ?&gt;
         &lt;li&gt;&lt;a href="&lt;?php echo get_permalink($postid); ?&gt;"&gt;&lt;?php echo $title ?&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;?php }
}
?&gt;
&lt;/ul&gt;</code></pre>

<strong>Code explanation</strong>.
The first thing we did was send out an SQL query to the WordPress database using the <code>$wpdb</code> object. Once we got the results, we used a simple PHP <code>foreach</code> statement to display the most popular posts from a certain period in an HTML unordered list.

<strong>Source:</strong>

*   [How to: Display the most commented posts of 2008](https://www.wprecipes.com/how-to-display-the-most-commented-posts-of-2008)

## Related posts

You may be interested in the following related posts:

*   [5 Useful And Creative Ways To Use WordPress Widgets](https://www.smashingmagazine.com/2009/07/14/5-useful-and-creative-ways-to-use-wordpress-widgets/)
*   [Power Tips For WordPress Template Developers](https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/)
*   [10 Useful WordPress Loop Hacks](https://www.smashingmagazine.com/2009/06/10/10-useful-wordpress-loop-hacks/)
*   [Custom Field Hacks For WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/)
*   [15 Useful Twitter Hacks and Plugins For WordPress](https://www.smashingmagazine.com/2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [Mastering WordPress Shortcuts](https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/)
*   [100 Amazing Free WordPress Themes For 2009](https://www.smashingmagazine.com/2009/05/18/100-amazing-free-wordpress-themes-for-2009/)

{{< signature "al" >}}


---
title: 10 Useful RSS-Tricks and Hacks For WordPress
slug: 10-useful-rss-hacks-for-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9a6f349-759e-4235-b9a1-66fa37307030/crossbrowser-testing.jpg
date: 2008-12-02T18:48:33.000Z
author: jean-baptiste-jung
description: >-
  **RSS** is one of those technologies that are extremely simple yet extremely
  powerful. Currently, RSS is the _de facto_ standard for blog syndication, and
  it is used widely in both personal and corporate settings; for example, in
  blogs. And because a large percentage of these blogs run on WordPress, we'll
  cover in this post some (hopefully) relatively unknown but useful RSS-related
  tricks and hacks that will help you use RSS in a more effective way — and
  without unnecessary and chunky WordPress plug-ins.
categories:
  - WordPress
  - RSS
  - Hacks
  - Techniques (WP)
---
<strong>RSS</strong> is one of those technologies that are extremely simple yet extremely powerful. Currently, RSS is the <em>de facto</em> standard for blog syndication, and it is used widely in both personal and corporate settings; for example, in blogs. And because a large percentage of these blogs run on WordPress, we'll cover in this post some (hopefully) relatively unknown but useful RSS-related tricks and hacks that will help you use RSS in a more effective way — and without unnecessary and chunky WordPress plug-ins. <strong>This article has been reviewed and updated on Nov. 24th, 2016</strong>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Easily Customize WordPress’ Default Functionality](https://www.smashingmagazine.com/2012/06/customize-wordpress-default-functionality/)
*   [10 Tips To Optimize Your WordPress Theme](https://www.smashingmagazine.com/2011/12/10-tips-optimize-wordpress-theme/)
*   [Guide To WordPress Coding Standards](https://www.smashingmagazine.com/2012/07/guide-wordpress-coding-standards/)
*   [Writing Unit Tests For WordPress Plugins](https://www.smashingmagazine.com/2012/03/writing-unit-tests-for-wordpress-plugins/)

Let's take a look at <strong>10 useful, yet rather unknown RSS-tricks for WordPress</strong>. Each section of the article presents a problem, suggests a solution and provides you with an explanation of the solution, so that you can not just solve some of your RSS-related problems but also understand what you are actually doing. Thus, you can make sure your WordPress theme remains under your control and is not bloated with some obscure source code.</p>

## 1\. Control When Your Posts are Available via RSS

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1c741e5-5da2-47c8-9191-d9510e8b6b14/sm8.jpg" alt="Screenshot" />

{{% feature-panel %}}

<strong>The problem</strong>. Have you ever published an article and then immediately noticed an error? Sure, you can edit it, but there’s another problem: the article has already been published in your RSS feed. To avoid this kind of problem, use this recipe to create a delay between the publication of a post and its availability in your RSS feed.

<strong>The solution</strong>. To apply this hack, simply paste the following code into your theme’s function.php file. If your theme doesn’t have this file, just create it.

<pre><code class="language-php">function publish_later_on_feed($where) {
  global $wpdb;

  if ( is_feed() ) {
    // timestamp in WP-format
    $now = gmdate('Y-m-d H:i:s');

    // value for wait; + device
    $wait = '5'; // integer

    // https://dev.mysql.com/doc/refman/5.0/en/date-and-time-functions.html#function_timestampdiff
    $device = 'MINUTE'; //MINUTE, HOUR, DAY, WEEK, MONTH, YEAR

    // add SQL-sytax to default $where
    $where .= " AND TIMESTAMPDIFF($device, $wpdb-&gt;posts.post_date_gmt, '$now') &gt; $wait ";
  }
  return $where;
}

add_filter('posts_where', 'publish_later_on_feed');</code></pre>

<strong>Code explanation</strong>. The above code will add a 5-minute delay to the time between when your post is published on your blog and when it appears in your RSS feed. To change the length of the delay, change the value of the <em>$wait</em> variable on line 9.</p>

### Sources

*   [Publish your feed later](https://wpengineer.com/publish-the-feed-later/)

## 2\. Redirecting WordPress Feeds to FeedBurner Feeds

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5569a9a8-8322-40f6-8f55-9f00081cac54/sm1.png" alt="Screenshot" width="500" height="160" />

<strong>The problem</strong>. Beginner bloggers usually start to use FeedBurner only after they have seen it used on many other blogs and realize how useful and cool this tool is. They sign up and start to use it, but their early readers are already subscribed to their default WordPress feed.

Another problem: do you often change your theme? If so, you must be bored having to edit each call to <em>bloginfo(’rss2_url’)</em> and replace it with your FeedBurner feed’s URL.

<strong>The solution</strong>. The solution to both problems described above is simple: use server redirections.

1.  Create a backup of your .htaccess file, located in the root of your Web server.
2.  Edit the .htaccess file and add the following code. Don’t forget to modify the feed’s URL with your own feed’s URL.

        # temp redirect wordpress content feeds to feedburner
        <IfModule mod_rewrite.c>
         RewriteEngine on
         RewriteCond %{HTTP_USER_AGENT} !FeedBurner    [NC]
         RewriteCond %{HTTP_USER_AGENT} !FeedValidator [NC]
         RewriteRule ^feed/?([_0-9a-z-]+)?/?$ https://feeds.feedburner.com/wprecipes [R=302,NC,L]
        </IfModule>

3.  Save the file. You’re done!

<strong>Code explanation</strong>. Each time someone clicks on a link to <em>https://www.yourblog.com/feed</em>, he or she will be redirected to <em>https://feeds.feedburner.com/yourblog</em>. This way, you will have never lost an RSS subscriber, and even if you change your theme twice a day, you’ll never have to manually edit your RSS feed links again.</p>

### Sources

*   [Redirect WordPress feeds to FeedBurner via htaccess (Redux)](https://perishablepress.com/press/2008/03/25/redirect-wordpress-feeds-to-feedburner-via-htaccess-redux/)
*   [How to: redirect WordPress RSS feeds to FeedBurner with .htaccess](https://www.wprecipes.com/how-to-redirect-wordpress-rss-feeds-to-feedburner-with-htaccess)

## 3\. Insert Ads (or Anything Else) in Your RSS Feed

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19285264-baa2-464f-bafa-75a14781e80f/sm2.png" alt="Screenshot" width="500" height="231" />

<strong>The problem</strong>. Monetizing RSS feeds is currently becoming a common practice, and many blog owners do it to maximize their income. FeedBurner can insert AdSense ads into your feed items, but you need at least 500 subscribers to qualify, and you can’t use any ads other than the AdSense ads provided by FeedBurner.

<strong>The solution</strong>. It is possible, though, to insert other kinds of ads into your RSS feed. You can, for example, use a link to a free WordPress theme only for your RSS subscribers.

Follow these simple steps to perform this hack:

1.  Edit the functions.php file of your theme. If your theme doesn’t have a functions.php file, simply create one.
2.  Paste the following code into your functions.php file:

        <?php
        function insertAds($content) {
            $content = $content.'<hr /><a href="https://www.wprecipes.com">Have you visited WpRecipes today?</a><hr />';
            return $content;
        }
        add_filter('the_excerpt_rss', 'insertAds');
        add_filter('the_content_rss', 'insertAds');
        ?>

3.  Save the file. You’re now displaying your ads in your RSS feed!

<strong>Code explanation</strong>. I have seen many similar hacks on the Web, but all of them require you to edit WordPress core files to achieve the same result. Of course, editing WordPress core files is a very bad idea because then you would have to re-edit the files each time you upgrade your blog. Instead, this hack uses the <em>add_filter()</em> WordPress function to insert content into your RSS feed without editing any core files.</p>

### Sources

*   [How to: insert ads in your RSS feed](https://www.wprecipes.com/how-to-insert-ads-on-your-rss-feed)

## 4\. Format Your Images for Feed Readers

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/676232bb-8aaa-4e25-874e-4d945b584880/sm6.jpg" alt="Screenshot" />

<strong>The problem</strong>. You took a lot of time to write and format your post and add beautiful screenshots. It looks so good on your blog. Sadly, when the post is displayed in Google Reader or any other RSS reader, it doesn’t look so great.

<strong>The solution</strong>. This is due to the fact that most feed readers display images inline with text:
<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fa14f91-98e6-418c-9310-ee6e0815be04/inline-image.jpg" alt="inline image" />
To avoid this problem, add a CSS class to display the image as a block. WordPress provides the built-in class “<em>center</em>“:

<pre><code class="language-php">&lt;img src="https://www.smashingmagazine.com/images/wordpress-rss-hacks/myimage.jpg" alt="This is my image" class="center"/&gt;</code></pre>

### Sources

*   [How to format images for feed readers](https://www.pearsonified.com/2007/06/how-to-format-images-for-feed-readers.php)

## 5\. Provide Your Readers with a Feed for Each Post

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/593b6daa-d9ed-4505-bcb1-545a7320191a/sm9.png" alt="Screenshot" /><br>
<strong>The problem.</strong> When a post has lots and lots of comments, it can be hard for readers to follow the conversation. Most WordPress users don’t know this, but our favorite blogging engine has a built-in function for providing an RSS feed for the comments in each post.

<strong>The solution.</strong> Well, this recipe isn’t really a hack or anything: to provide an RSS feed for the comments in a particular post, just call the <em>comment_rss_link()</em> function:

<pre><code class="language-php">&lt;?php comments_rss_link('&amp;raquo; Comments RSS Feed'); ?&gt;</code></pre>

Update: the <em>comment_rss_link()</em> function has been deprecated. Use the <em>post_comments_feed_link()</em> function instead.

<pre><code class="language-php">&lt;?php post_comments_feed_link('&amp;raquo; Comments RSS Feed'); ?&gt;</code></pre>

### Sources

*   [WordPress how to: provide an RSS feed for the comments in each post](https://www.wprecipes.com/wordpress-how-to-provide-rss-feed-for-each-post-comments)

## 6\. Exclude Categories from Your RSS Feed

<strong>The problem</strong>. Do you use one of your blog categories to let readers know about your website’s news, or does your blog feature a category that has nothing to do with the rest of your content? If so, it is generally not a good idea to include it in your RSS feed.

<strong>The solution</strong>. Here’s how to get rid of one of the categories in your RSS feed:

1.  First, get the numeric ID of the category you want to exclude. If you don’t know how to get the ID of a particular category, you can learn how [here](https://www.wprecipes.com/how-to-find-wordpress-category-id).
2.  Once you have the ID of the category you want to exclude from your RSS feed, edit the functions.php file in your theme. Create the file if it doesn’t exist.
3.  Paste the following code in it:

        function myFilter($query) {
            if ($query->is_feed) {
                $query->set('cat','-5'); //Don't forget to change the category ID =^o^=
            }
        return $query;
        }

        add_filter('pre_get_posts','myFilter');

4.  Save the file, and you’re done!

<strong>Code explanation</strong>. This hack works exactly the same way as the previous one: create a custom function to exclude the category that you don’t want to appear in your RSS feed, and then use the super-useful <em>add_filter()</em> function to apply it to the <em>pre_get_posts()</em> WordPress core function. The minus is important before the numeric ID. Without the minus, only this category will be used.</p>

## 7\. Display Any RSS Feed on Your WordPress Blog

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cefc5b0-b134-4f3f-8d02-e99483e61b80/sm5.png" alt="Screenshot" />

<strong>The problem</strong>. Do you have more than one blog, or do you manage a forum? If so, you may want to be able to display any RSS feed on your WordPress blog.

<strong>The solution</strong>. Many plug-ins can do the job, but they’re not necessary at all. WordPress has a built-in RSS reader that is used, for example, to display news on your dashboard. All you have to do is use it in your theme.

1.  Paste the following code anywhere in your theme (personally, I’d put it in the sidebar, the footer or, even better, the page template):

        <?php include_once(ABSPATH.WPINC.'/rss.php');
        wp_rss('https://feeds.feedburner.com/wprecipes', 3); ?>

2.  Save it and you’re done. It’s as easy as that!

<strong>Code explanation</strong>. The first thing we have done is include the rss.php file from WordPress core. This file allows us to use the <em>wp_rss()</em> function, which takes two parameters: the first is the RSS feed’s URL, and the second is the number of RSS entries to be displayed.</p>

### Sources

*   [How to: Display any RSS feed on your WordPress blog](https://www.wprecipes.com/how-to-display-any-rss-feed-on-your-wordpress-blog)

## 8\. Use Category-Specific RSS Feeds

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97b2e8a5-d680-4bbb-8e81-465cca859272/rss-categ.gif" alt="Screenshot" width="502" height="306" />

<strong>The problem</strong>. Many blogs talk about a lot of different topics: design, programming, blogging tips, etc. Have you ever come across a blog in which you have enjoyed only one category of posts? If so, you should definitely consider offering one feed per category to your own readers.

<strong>The solution</strong>. Let’s say you’d like to be able to subscribe only to <a href="https://www.thegridsystem.org/categories/tools/">TheGridSystem's tools section</a>. The category URL is:

<pre><code class="language-php">https://www.thegridsystem.org/categories/tools/</code></pre>

To get an RSS feed for this category, you simply have to add <em>/feed</em> to the end of the URL:

<pre><code class="language-php">https://www.thegridsystem.org/categories/tools/feed</code></pre>

Pretty easy, isn’t it? But pretty useful, too, in my opinion.</p>

## 9\. List RSS Feeds by Category

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb3c3c1e-9a1b-4228-904b-c996c7232601/sm3.gif" alt="Screenshot" />

<strong>The problem</strong>. If you like the previous hack, you will probably also want to be able to display the names of all your category feeds in a list to your readers.

<strong>The solution</strong>.

1.  Edit any of your theme files, where you want to list your categories and their accompanying feeds.
2.  Paste the following code:

        <?php wp_list_categories('feed_image=https://www.myblog.com/image.gif&feed=XML Feed&optioncount=1&children=0'); ?>

3.  Save the file. You categories will now be displayed, along with their RSS feeds!

<strong>Code explanation</strong>. This hack uses only the good old <em>wp_list_categories()</em> function, with two parameters. The first is feed_image, which allows us to specify the URL to be displayed as a feed image. The second parameter is feed, which is used to specify the feed format.</p>

## 10\. Get Rid of RSS Feeds the Clean Way

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c51f2008-8366-4f5f-9a1e-8108abbba87d/sm7.png" alt="Screenshot" />

<strong>The problem</strong>. Let’s say you’re using WordPress as a CMS to manage your online portfolio or your company’s website. In such cases, the RSS feed isn’t that useful, and some people would probably want to remove it.

<strong>The solution</strong>. I have seen many “hacks” on the Web where people say you just have to remove the <em>include</em> on the wp-settings.php core file. I don’t think you should ever edit a core file. Instead, the following hack will do the job. Simply paste this code in the functions.php file of your theme:

<pre><code class="language-php">function fb_disable_feed() {
  wp_die( __('No feed available,please visit our &lt;a href="'. get_bloginfo('url') .'"&gt;homepage&lt;/a&gt;!') );
}

add_action('do_feed', 'fb_disable_feed', 1);
add_action('do_feed_rdf', 'fb_disable_feed', 1);
add_action('do_feed_rss', 'fb_disable_feed', 1);
add_action('do_feed_rss2', 'fb_disable_feed', 1);
add_action('do_feed_atom', 'fb_disable_feed', 1);</code></pre>

### Sources

*   [Disable WordPress feed](https://wpengineer.com/disable-wordpress-feed/)

{{< signature "al" >}}


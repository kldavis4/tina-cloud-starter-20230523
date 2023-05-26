---
title: Mastering WordPress Shortcodes
slug: mastering-wordpress-shortcodes
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63509dd6-130f-4fa5-985a-953b71890d96/organized-office-illu.jpg
date: 2009-02-03T04:00:31.000Z
author: jean-baptiste-jung
description: >-
  Introduced in WordPress 2.5, shortcodes are powerful but still yet quite unknown WordPress functions. Imagine you could just type "adsense" to display an AdSense ad or "post_count" to instantly find out the number of posts on your blog.
categories:
  - WordPress
  - Essentials
  - Shortcodes
  - Techniques (WP)
---
WordPress shortcodes can do this and more and will definitely make your blogging life easier. In this article, we'll show you how to create and use shortcodes, as well as provide killer <strong>ready-to-use WordPress shortcodes</strong> that will enhance your blogging experience. 

You may also want to take a look at the following related posts:

*   [WordPress Shortcodes: A Complete Guide](https://www.smashingmagazine.com/2012/05/wordpress-shortcodes-complete-guide/)
*   [<span class="headline">Inserting Widgets With Shortcodes</span>](https://www.smashingmagazine.com/2012/12/inserting-widgets-with-shortcodes/)
*   [10 Useful WordPress Loop Hacks](https://www.smashingmagazine.com/2009/06/10-useful-wordpress-loop-hacks/)

## What Are Shortcodes?

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89451025-9263-47fa-8547-ea04387a684e/sm1.png" alt="" />

{{% feature-panel %}}

Using shortcodes is very easy. To use one, create a new post (or edit an existing one), switch the editor to HTML mode and type a shortcode in brackets, such as:

<pre><code class="language-php">[showcase]</code></pre>

It is also possible to use attributes with shortcodes. A shortcode with attributes would look something like this:

<pre><code class="language-php">[showcase id="5"]</code></pre>

Shortcodes can also embed content, as shown here:

<pre><code class="language-php">[url href="https://www.smashingmagazine.com"]Smashing Magazine[/url]</code></pre>

Shortcodes are handled by a set of functions introduced in WordPress 2.5 called the Shortcode API. When a post is saved, its content is parsed, and the shortcode API automatically transforms the shortcodes to perform the function they're intended to perform.</p>

## Creating a Simple Shortcode

The thing to remember with shortcodes is that they're very easy to create. If you know how to write <a title="PHP: What You Need To Know To Play With The Web" href="https://www.smashingmagazine.com/2010/04/php-what-you-need-to-know-to-play-with-the-web/">a basic PHP function</a>, then you already know how to create a WordPress shortcode. For our first one, let's create the well-known "Hello, World" message.

1.  Open the _functions.php_ file in your theme. If the file doesn't exists, create it.
2.  First, we have to create a function to return the "Hello World" string. Paste this in your _functions.php_ file:

        function hello() {
            return 'Hello, World!';
        }

3.  Now that we have a function, we have to turn it into a shortcode. Thanks to the `add_shortcode()` function, this is very easy to do. Paste this line after our `hello()` function, then save and close the _functions.php_ file:

        add_shortcode('hw', 'hello');

    The first parameter is the shortcode name, and the second is the function to be called.
4.  Now that the shortcode is created, we can use it in blog posts and on pages. To use it, simply switch the editor to HTML mode and type the following:

        [hw]

    You're done! Of course, this is a very basic shortcode, but it is a good example of how easy it is to create one.</p>

## Creating Advanced Shortcodes

As mentioned, shortcodes can be used with attributes, which are very useful, for example, for passing arguments to functions. In this example, we'll show you how to create a shortcode to display a URL, just as you would with the BBCodes that one uses on forums such as VBulletin and PHPBB.

1.  Open your _functions.php_ file. Paste the following function in it:

        function myUrl($atts, $content = null) {
          extract(shortcode_atts(array(
            "href" => 'https://'
          ), $atts));
          return '<a href="'.$href.'">'.$content.'</a>';
        }

2.  Let's turn the function into a shortcode:

        add_shortcode("url", "myUrl");

3.  The shortcode is now created. You can use it on your posts and pages:

        [url href="https://www.wprecipes.com"]WordPress recipes[/url]

    When you save a post, the shortcode will display a link titled "WordPress recipes" and pointing to [https://www.wprecipes.com](https://www.wprecipes.com).

<strong>Code explanation</strong>. To work properly, our shortcode function must handle two parameters: <code>$atts</code> and <code>$content</code>. <code>$atts</code> is the shortcode attribute(s). In this example, the attribute is called <code>href</code> and contains a link to a URL. <code>$content</code> is the content of the shortcode, embedded between the domain and sub-directory (i.e. between "www.example.com" and "/subdirectory"). As you can see from the code, we've given default values to <code>$content and <code>$atts</code>.</code>

Now that we know how to create and use shortcodes, let's look at some killer <strong>ready-to-use</strong> shortcodes!

## 1\. Create a "Send to Twitter" Shortcode

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ede805e8-73b4-475a-8f51-d0b4d34a9029/sm4.png" alt="" />

<strong>The problem</strong>. Seems that a lot of you enjoyed my "Send to Twitter" hack. I also really enjoyed that hack, but it has a drawback: if you paste the code to your <em>single.php</em> file, the "Send to Twitter" link will be visible on every post, which you may not want. It would be better to control this hack and be able to specify when to add it to a post. The solution is simple: a shortcode!

<strong>The solution</strong>. This shortcode is simple to create. Basically, we just get the code from the "Send to Twitter" hack and turn it into a PHP function. Paste the following code in the <em>functions.php</em> file in your theme:

<pre><code class="language-php">function twitt() {
  return '&lt;div id="twitit"&gt;&lt;a href="https://twitter.com/home?status=Currently reading '.get_permalink($post-&gt;ID).'" title="Click to send this page to Twitter!" target="_blank"&gt;Share on Twitter&lt;/a&gt;&lt;/div&gt;';
}

add_shortcode('twitter', 'twitt');</code></pre>

To use this shortcode, simply switch the editor to HTML mode and then type:

<pre><code class="language-php">[twitter]</code></pre>

and a "Send to Twitter" link will appear where you placed the shortcode.</p>

### Source and related plug-ins:

*   [How to: Create a “send this to twitter” button](https://www.wprecipes.com/how-to-create-a-send-this-to-twitter-button)
*   [Twitter tools](https://alexking.org/blog/2007/05/07/twitter-tools-10)

## 2\. Create a "Subscribe to RSS" Shortcode

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c469f24-91d6-4067-a615-51b210f5feba/sm5.png" alt="" />

<strong>The problem</strong>. You already know that a very good way to gain RSS subscribers is to display a nice-looking box that says something like "Subscribe to the RSS feed." But once again, we don't really want to hard-code something into our theme and lose control of the way it appears. In this hack, we'll create a "Subscribe to RSS" shortcode. Display it in some places and not others, in posts or on pages, above or below the main content, it's all up to you.

<strong>The solution</strong>. As usual, we create a function and then turn it into a shortcode. This code goes into your <em>functions.php</em> file. Don't forget to replace the example feed URL with your own!

<pre><code class="language-php">function subscribeRss() {
    return '&lt;div class="rss-box"&gt;&lt;a href="https://feeds.feedburner.com/wprecipes"&gt;Enjoyed this post? Subscribe to my RSS feeds!&lt;/a&gt;&lt;/div&gt;';
}

add_shortcode('subscribe', 'subscribeRss');</code></pre>

<strong>Styling the box</strong>. You probably noticed the <code>rss-box</code> class that was added to the div element containing the link. This allows you to style the box the way you like. Here's an example of some CSS styles you can apply to your "Subscribe to RSS" box. Simply paste it into the <em>style.css</em> file in your theme:

<pre><code class="language-php">.rss-box{
  background:#F2F8F2;
  border:2px #D5E9D5 solid;
  font-weight:bold;
  padding:10px;
}</code></pre>

## 3\. Insert Google AdSense Anywhere

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/744f83e8-9629-43cf-8e52-15b09cccf7c2/sm3.png" alt="" />

<strong>The problem</strong>. Most bloggers use Google AdSense. It is very easy to include AdSense code in a theme file such as <em>sidebar.php</em>. But successful online marketers know that people click more on ads that are embedded in the content itself.

<strong>The solution</strong>. To embed AdSense anywhere in your posts or pages, create a shortcode:

1.  Open the _functions.php_ file in your theme and paste the following code. Don't forget to modify the JavaScript code with your own AdSense code!

        function showads() {
            return '<div id="adsense"><script type="text/javascript"><!--
          google_ad_client = "pub-XXXXXXXXXXXXXX";
          google_ad_slot = "4668915978";
          google_ad_width = 468;
          google_ad_height = 60;
          //-->
        </script>

        <script type="text/javascript"
        src="https://pagead2.googlesyndication.com/pagead/show_ads.js">
        </script></div>';
        }

        add_shortcode('adsense', 'showads');

2.  Once you have saved _functions.php_, you can use the following shortcode to display AdSense anywhere on your posts and pages:

        [adsense]

    Note that our AdSense code is wrapped with an `adsense` div element, we can style it the way we want in our _style.css_ file.

<strong>Code explanation</strong>. The above code is used simply to display AdSense ads. When the shortcode is inserted in a post, it returns an AdSense ad. It is pretty easy but also, you'll agree, a real time-saver!

### Sources:

*   [How to: Embed AdSense anywhere on your posts](https://www.wprecipes.com/how-to-embed-adsense-anywhere-on-your-posts)

## 4\. Embed an RSS Reader

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a5e070f-f191-40fd-9b87-98697ddccad1/sm6.png" alt="" />

<strong>The problem</strong>. Many readers also seemed to enjoy the "<a href="https://www.smashingmagazine.com/2008/12/02/10-useful-rss-hacks-for-wordpress/">8 RSS Hacks for WordPress</a>" post published on Smashing Magazine recently. Now, let's use our knowledge of both RSS and shortcodes to embed an RSS reader right in our posts and pages.

<strong>The solution</strong>. As usual, to apply this hack, simply paste the following code in your theme's <em>function.php</em> file.

<pre><code class="language-php">//This file is needed to be able to use the wp_rss() function.
include_once(ABSPATH.WPINC.'/rss.php');

function readRss($atts) {
    extract(shortcode_atts(array(
  "feed" =&gt; 'https://',
      "num" =&gt; '1',
    ), $atts));

    return wp_rss($feed, $num);
}

add_shortcode('rss', 'readRss');</code></pre>

To use the shortcode, type in:

<pre><code class="language-php">[rss feed="https://feeds.feedburner.com/wprecipes" num="5"]</code></pre>

The <code>feed</code> attribute is the feed URL to embed, and <code>num</code> is the number of items to display.</p>

## 5\. Get posts from WordPress Database with a Shortcode

<strong>The problem</strong>. Ever wished you could call a list of related posts directly in the WordPress editor? Sure, the "Related posts" plug-in can retrieve related posts for you, but with a shortcode you can easily get a list of any number of posts from a particular category.

<strong>The solution</strong>. As usual, paste this code in your <em>functions.php</em> file.

<pre><code class="language-php">function sc_liste($atts, $content = null) {
        extract(shortcode_atts(array(
                "num" =&gt; '5',
                "cat" =&gt; ’
        ), $atts));
        global $post;
        $myposts = get_posts('numberposts='.$num.'&amp;order=DESC&amp;orderby=post_date&amp;category='.$cat);
        $retour='&lt;ul&gt;';
        foreach($myposts as $post) :
                setup_postdata($post);
             $retour.='&lt;li&gt;&lt;a href="'.get_permalink().'"&gt;'.the_title("","",false).'&lt;/a&gt;&lt;/li&gt;';
        endforeach;
        $retour.='&lt;/ul&gt; ';
        return $retour;
}
add_shortcode("list", "sc_liste");</code></pre>

To use it, simply paste the following in the WordPress editor, after switching to HTML mode:

<pre><code class="language-php">[liste num="3" cat="1"]</code></pre>

This will display a list of three posts from the category with an ID of 1. If you don't know how to get the ID of a specific category, an easy way is explained <a href="https://www.wprecipes.com/how-to-find-wordpress-category-id">here</a>.

<strong>Code explanation</strong>. After it has extracted the arguments and created the global variable <code>$posts</code>, the <code>sc_liste()</code> function uses the <code>get_posts()</code> function with the <code>numberposts</code>, <code>order</code>, <code>orderby</code> and <code>category</code> parameters to get the X most recent posts from category Y. Once done, posts are embedded in an unordered HTML list and returned to you.</p>

### Source:

1.  WordPress: Création de shortcode avancé

## 6\. Get the Last Image Attached to a Post

<strong>The problem</strong>. In WordPress, images are quite easy to manipulate. But why not make it even easier? Let's look at a more complex shortcode, one that automatically gets the latest image attached to a post.

<strong>The solution</strong>. Open the <em>functions.php</em> file and paste the following code:

<pre><code class="language-php">function sc_postimage($atts, $content = null) {
  extract(shortcode_atts(array(
    "size" =&gt; 'thumbnail',
    "float" =&gt; 'none'
  ), $atts));
  $images =&amp; get_children( 'post_type=attachment&amp;post_mime_type=image&amp;post_parent=' . get_the_id() );
  foreach( $images as $imageID =&gt; $imagePost )
  $fullimage = wp_get_attachment_image($imageID, $size, false);
  $imagedata = wp_get_attachment_image_src($imageID, $size, false);
  $width = ($imagedata[1]+2);
  $height = ($imagedata[2]+2);
  return '&lt;div class="postimage" style="width: '.$width.'px; height: '.$height.'px; float: '.$float.';"&gt;'.$fullimage.'&lt;/div&gt;';
}
add_shortcode("postimage", "sc_postimage");</code></pre>

To use the shortcode, simply type the following in the editor, when in HTML mode:

<pre><code class="language-php">[postimage size="" float="left"]</code></pre>

<strong>Code explanation</strong>. The <code>sc_postimage()</code> function first extracts the shortcode attributes. Then, it retrieves the image by using the <code>get_children()</code>, <code>wp_get_attachment_image()</code> and <code>wp_get_attachment_image_src()</code> WordPress functions. Once done, the image is returned and inserted in the post content.</p>

### Sources:

1.  [WordPress Shortcode: easily display the last image attached to post](https://www.wprecipes.com/wordpress-shortcode-easily-display-the-last-image-attached-to-post)

## 7\. Adding Shortcodes to Sidebar Widgets

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80344b9d-b716-485d-8cca-b1807ad5d92f/sm8.png" alt="" />

<strong>The problem</strong>. Even if you enjoyed this article, you may have felt a bit frustrated because, by default, WordPress doesn't allow shortcode to be inserted into sidebar widgets. Thankfully, here's a little trick to enhance WordPress functionality and allow shortcodes to be used in sidebar widgets.

<strong>The solution</strong>. One more piece of code to paste in your <em>functions.php</em> file:

<pre><code class="language-php">add_filter('widget_text', 'do_shortcode');</code></pre>

That's all you need to allow shortcodes in sidebar widgets!

<strong>Code explanation</strong>. What we did here is quite simple: we added a filter on the <code>widget_text()</code> function to execute the <code>do_shortcode()</code> function, which uses the API to execute the shortcode. Thus, shortcodes are now enabled in sidebar widgets.

{{< signature "al" >}}


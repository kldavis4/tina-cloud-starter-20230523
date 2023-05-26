---
title: 15 Useful Twitter Hacks and Plug-Ins For WordPress
slug: 15-useful-twitter-plugins-and-hacks-for-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f64b89a8-1266-463b-a9a5-949c5dad0544/twitter-birds-design-illu.jpg
date: 2009-03-04T16:00:45.000Z
author: jean-baptiste-jung
description: >-
  Since its launch in 2006, **Twitter** has grown to create what most people
  would call a social media revolution. By the very nature of the short messages
  it hosts, Twitter is a wonderful marketing and promotion tool that no serious
  blogger can ignore.

  In this article, we have compiled **15 most useful Twitter plug-ins, hacks and
  tips for WordPress** to help you get the most out of Twitter in your WordPress
  blog.

  WordPress plug-ins are good, but if you have 50 different plug-ins active on
  your blog, you should obviously expect longer loading times and even some
  inconvenience. This is why we love hacks! First let’s dive deep into WordPress
  and see what hacks can do to enhance our blogging experience. In the second
  part of this article, we will also show you some useful Twitter plug-ins for
  your WordPress blog.

  You may want to take a look at the following related posts:

  *   [50 Twitter Tools and Tutorials For Designers and
  Developers](https://www.smashingmagazine.com/2009/03/02/twitter-web-designer-and-developer-toolbox-api-and-tutorials/)

  *   [8 Useful Tips To Become Successful With
  Twitter](https://www.smashingmagazine.com/2009/02/03/8-useful-tips-to-become-successul-with-twitter/)
categories:
  - WordPress
  - Twitter
  - Plugins
  - Hacks
  - Social Media
---
Since its launch in 2006, <strong>Twitter</strong> has grown to create what most people would call a social media revolution. By the very nature of the short messages it hosts, Twitter is a wonderful marketing and promotion tool that no serious blogger can ignore.

In this article, we have compiled <strong>15 most useful Twitter plug-ins, hacks and tips for WordPress</strong> to help you get the most out of Twitter in your WordPress blog.

You may want to take a look at the following related posts:

*   [50 Twitter Tools and Tutorials For Designers and Developers](https://www.smashingmagazine.com/2009/03/02/twitter-web-designer-and-developer-toolbox-api-and-tutorials/)
*   [8 Useful Tips To Become Successful With Twitter](https://www.smashingmagazine.com/2009/02/03/8-useful-tips-to-become-successul-with-twitter/)
*   [Twitter Icons: Cute Tweeters & Birdies](https://www.smashingmagazine.com/2009/01/friday-freebies-flavours-icon-set-and-cute-tweeters-icon-set/)

## 1\. WordPress Hacks For Twitter

WordPress plug-ins are good, but if you have 50 different plug-ins active on your blog, you should obviously expect longer loading times and even some inconvenience. This is why we love hacks! First let’s dive deep into WordPress and see what hacks can do to enhance our blogging experience. In the second part of this article, we will also show you some useful Twitter plug-ins for your WordPress blog.

{{% feature-panel %}}

### Automatically create TinyUrls for your blog posts

<img style="border: 1px #aaa solid; padding: 3px;" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b2699a7-bed9-4196-8933-a2195670d26b/9.png" alt="" />

Because of the restriction on character numbers in Twitter, you have to use a URL shortener when tweeting URLs. So, to help your readers tweet about your posts, you should definitely provide short URLs for all of your posts.

Here’s how to automate that task:

Open your functions.php file and paste the following code:

<pre><code class="language-php">function getTinyUrl($url) {
    $tinyurl = file_get_contents("https://tinyurl.com/api-create.php?url=".$url);
    return $tinyurl;
}</code></pre>

Once done, paste this in your <em>single.php</em> file, within the loop:

<pre><code class="language-php">&lt;?php
$turl = getTinyUrl(get_permalink($post-&gt;ID));
echo 'Tiny Url for this post: &lt;a href="'.$turl.'"&gt;'.$turl.'&lt;/a&gt;'
?&gt;</code></pre>

To see this in action, visit my website, WpVote, and look at any post.

<strong>Source: <a href="https://www.wprecipes.com/how-to-automatically-provide-tinyurls-for-your-wordpress-blog-posts">How to: Automatically provide TinyUrls for your WordPress blog posts</a></strong>

### Display your latest tweet without a plug-in

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acee3917-3dcb-4780-a7c0-080841dfc0d6/8.png" alt="" />

If people like your blog, they would probably also enjoy your tweets. Displaying your latest tweets on your WordPress blog is a good way to gain new subscribers. A plug-in can do that, but for such a simple task, I prefer a hack. This one grabs your latest tweet and displays it on your blog.

This ready-to-use code can be pasted anywhere in your theme files. Just don’t forget to change the value of the $username on line 4. The $prefix and $suffix variable can be used to insert a title, and the div element can be used for further CSS styling.

<pre><code class="language-php">&lt;?php

// Your twitter username.
$username = "TwitterUsername";

// Prefix - some text you want displayed before your latest tweet.
// (HTML is OK, but be sure to escape quotes with backslashes: for example href="link.html")
$prefix = "&lt;h2&gt;My last Tweet&lt;/h2&gt;";

// Suffix - some text you want display after your latest tweet. (Same rules as the prefix.)
$suffix = "";

$feed = "https://search.twitter.com/search.atom?q=from:" . $username . "&amp;rpp=1";

function parse_feed($feed) {
    $stepOne = explode("&lt;content type="html"&gt;", $feed);
    $stepTwo = explode("&lt;/content&gt;", $stepOne[1]);
    $tweet = $stepTwo[0];
    $tweet = str_replace("&amp;lt;", "&lt;", $tweet);
    $tweet = str_replace("&amp;gt;", "&gt;", $tweet);
    return $tweet;
}

$twitterFeed = file_get_contents($feed);
echo stripslashes($prefix) . parse_feed($twitterFeed) . stripslashes($suffix);
?&gt;</code></pre>

Save the file, and your latest tweet is displayed on your blog. Nice, huh?

<strong>Sources:</strong>

*   [How to: Display your latest twitter entry on your WP blog](https://www.wprecipes.com/how-to-display-your-latest-twitter-entry-on-your-wp-blog)
*   [Latest Twitter Update With PHP](https://scriptplayground.com/tutorials/php/Latest-Twitter-Update-With-PHP/)

### Display your latest tweet as an image

Because of Twitter’s success, a lot of third-parties have started promoting additional Twitter services. TwitSig is one of them. This website is very ugly but also very cool because it allows you to get an auto-updating image that displays your latest Twitter entry.

While using this image as a signature in forums would be good enough, integrating it in your WordPress blog, under your posts for example, would also be great.

1.  Go to Twitsig.com. You don’t have to register: very nice!
2.  Simply enter your Twitter username in the text field.
3.  And your Twitter image is ready, displaying your latest tweet. The image is automatically updated when you update your Twitter status.
4.  Open any of your WordPress theme files and paste the following code (make sure to replace my username with yours!):

        <a href="https://twitter.com/catswhocode"><img loading="lazy" decoding="async" src="https://twitsig.com/catswhocode.jpg"></a>

### Create a “Tweet this” button

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35bd8f66-07f1-411b-8353-1a6cad056c65/10.png" alt="" />

Twitter is definitely a great way to gain exposure on the Web. This is why I created a fancy “Send to Twitter” button and implemented it on my blogs (see links at the bottom of the article). Go here if you’d like to see this hack in action.

1.  Open the single.php file in your theme.
2.  Paste the following code where you’d like your Twitter button to appear:

        <a href="https://twitter.com/home?status=Currently reading <?php the_permalink(); ?>" title="Click to send this page to Twitter!"><img loading="lazy" decoding="async" src="send-to-twitter.png" alt="" /></a>

Some time ago, in my “<a href="https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/">Mastering WordPress shortcodes</a>” article here on Smashing Magazine, I showed you how to create a “Send to Twitter” WordPress shortcode. I also wrote an article on Pro Blog Design about creating a “Send to Twitter” WordPress widget. You can read that tutorial <a href="https://www.problogdesign.com/wordpress/how-to-create-your-own-twitter-widget/">here</a>!

### Detect a visitor from Twitter

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eb4f8fc-2f01-48a7-9076-81c9e5642a2c/11.png" alt="" />

Visitors coming to my blogs from Twitter now represent something like 10% of all my traffic, which is quite a lot. Because many Twitter users re-tweet blog posts that they like, it may be a very good idea to detect Twitter visitors, welcome them and, of course, remind them that their re-tweets are appreciated.

To do this, open your <em>single.php</em> file and paste these lines where you’d like your “Welcome Twitter user” message to be displayed.

<pre><code class="language-php">&lt;?php
if (strpos("twitter.com",$_SERVER[HTTP_REFERER])==0) {
    echo "Welcome, Twitter visitor! If you enjoy this post, don't hesitate to retweet!";
}
?&gt;</code></pre>

This code will detect readers coming from Twitter and display the message only to them.</p>

### Create a Twitter page on your WordPress blog

We already showed you how to display your latest tweet on your blog, in your sidebar for example. Another good way to introduce readers to your Twitter updates is to create a dedicated page for displaying your tweets, using the powerful “Page template” WordPress option.

To perform this hack, you need to know how to create and use page templates. If you’re not familiar with this, this article will tell you all you need to know.

Here’s the code to create a Twitter page template. Paste it in a new file, name the file something like <em>twitter-page.php</em>, for example, and then add it to your blog.

<pre><code class="language-php">&lt;?php

/*
Template Name: Twitter page
*/

get_header();

include_once(ABSPATH.WPINC.'/rss.php');
wp_rss('https://twitter.com/statuses/user_timeline/15985955.rss', 20);

get_sidebar();
get_footer();
?&gt;</code></pre>

This code uses the <em>wp_rss()</em> function from WordPress core, which is an RSS reader. In the first argument I pass my Twitter RSS feed, and in the second argument I determine the number of entries to display.</p>

### Using Twitter avatars in comments without plug-ins

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d562b1c-0959-4be0-8707-15b8313c4788/12.gif" alt="" />

I was pretty interested in the Twittar plug-in when it was first released and decided to look at the source to see how it works. Being a die-hard WordPress hack fanatic, I decided to create a hack using the Twittar code.

Follow these simple instructions to use Twitter avatars in your blog comments without a plug-in:

1.  The first thing is to get the functions file [here](https://www.smashingmagazine.com/2009/01/08/twitter-avatars-in-comments-wordpress-plugin/).
2.  Once you have it, unzip the archive and open the twittar.php file. Select all of its contents and paste it in the functions.php file in your theme.
3.  Now, open your comments.php file and find the comments loop. Then, just paste the following line where you’d like the Twitter avatars to be displayed:

        <?php twittar('45', 'default.png', '#e9e9e9', 'twitavatars', 1, 'G'); ?>

<strong>Source</strong>: <a href="https://www.wprecipes.com/ho-to-use-twitter-avatars-in-comments">How to: Use Twitter avatars in comments</a>

## 2\. WordPress Plug-Ins For Twitter

Twitter Updater
Are you using Twitter to notify readers about your new blog posts, or even old ones that you’ve updated? If so, then Twitter Updated is definitely something to consider. The plug-in automatically sends an update status request to Twitter when you create or modify a post. Text is customizable, and the plug-in provides many options.

<a href="https://twitthis.com/">Twit this</a>
The Twit This plug-in makes it easy for readers to tweet about your blog posts by creating a “Share on Twitter” link on your blog. When someone clicks on it, your blog post’s URL is automatically sent to Twitter, and the visitor can enters a description before sending the tweet to his or her friends.

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c248e0c-be7d-4b09-8c54-11fb7a8e56a8/2.png)

Twit it up
Twit it up is a simple AJAX-powered WordPress plug-in that basically does the same thing as Twit this: allows readers to tweet one of your posts directly from your blog by clicking a simple link.

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7dbdba41-e74f-4d3e-8c56-fa8748eb6ea6/3.png)

<a href="https://deanjrobinson.com/projects/twitt-twoo/">Twit-Twoo</a>
Twit-Twoo is a very useful for bloggers because it allows you to tweet friends directly from your WordPress dashboard. Particularly great if you spend a lot of time on your WordPress dashboard!

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/751f04e7-9851-4a6b-b5d4-03b935835b3b/4.gif)

<a href="https://alexking.org/projects/wordpress/readme?project=twitter-tools">Twitter Tools</a>
Twitter Tools, created by Alex King, is one of the most popular Twitter plug-ins for WordPress. It completely integrates Twitter in your WordPress blog, allowing you to archive your tweets, create a blog post from each of your tweets and post tweets from your admin dashboard or sidebar. It also allows you to create a daily digest of tweets; very nice if you tweet a lot!

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b92dd3cb-580f-4df5-9a0c-cb6c9d8ba745/5.png)

<a href="https://www.smashingmagazine.com/2009/01/08/twitter-avatars-in-comments-wordpress-plugin/">Twittar</a>
Twittar was <a href="https://www.smashingmagazine.com/2009/01/08/twitter-avatars-in-comments-wordpress-plugin/">released here on Smashing Magazine back in January</a>. Remember it? This plug-in integrates Twitter avatars in the comment template of your WordPress blog. Definitely a plug-in to consider if you and your readership often use Twitter! And don’t worry if any of your readers don’t use Twitter (yet), Twittar automatically displays gravatars if no Twitter avatar is available.

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c347cef-0f13-4faa-8c0b-35a891b4933e/6.png)

<a href="https://www.smashingmagazine.com/2009/01/09/tweetbacks-plugin-for-wordpress/">Tweetbacks</a>
Since its release only one month ago, the Tweetbacks plug-in has created a mini-revolution in the blogging world. While your WordPress blog can automatically notify you when bloggers discuss your posts on their own blogs, via Trackbacks, it can’t notify you when people discuss your posts on Twitter. That’s why Tweetbacks is so great: it automatically imports tweets about your posts and lets you display them either as comments or separately.

![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f22d68e-027e-4f74-984c-880c79d0fc0f/7.png)

## Related Posts

You may want to take a look at the following related posts:

*   [50 Twitter Tools and Tutorials For Designers and Developers](https://www.smashingmagazine.com/2009/03/02/twitter-web-designer-and-developer-toolbox-api-and-tutorials/)
*   [8 Useful Tips To Become Successful With Twitter](https://www.smashingmagazine.com/2009/02/03/8-useful-tips-to-become-successul-with-twitter/)

{{< signature "al" >}}


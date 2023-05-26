---
title: 'How To Integrate Facebook, Twitter And Google+ In WordPress'
slug: facebook-twitter-google-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aab11dee-69f7-4cd1-a096-a24e8424eb34/wordpress-arrow-illu.jpg
date: 2012-01-19T16:01:28.000Z
author: kevin-muldoon
description: >-
  Integrating social media services in your website design is vital if you want
  to make it easy for readers to share your content. While some users are happy
  with the social media buttons that come built into their design template, the
  majority of WordPress users install a plugin to automatically embed sharing
  links on their pages. Many of you will find that a plugin does exactly what
  you need; others not so much.
categories:
  - WordPress
  - Social Media
  - Techniques (WP)
---
Integrating social media services in your website design is vital if you want to make it easy for readers to share your content. While some users are happy with the social media buttons that come built into their design template, the majority of WordPress users install a plugin to automatically embed sharing links on their pages. Many of you will find that a plugin does exactly what you need; others not so much. Some are poorly coded, and most include services that you just don’t need. And while some great social media plugins are out there, they don’t integrate with every WordPress design.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [8 Useful Tips To Become Successful With Twitter](https://www.smashingmagazine.com/2009/02/8-useful-tips-to-become-successul-with-twitter/)
*   [Twitter Icons: Cute Tweeters & Birdies](https://www.smashingmagazine.com/2009/01/friday-freebies-flavours-icon-set-and-cute-tweeters-icon-set/)
*   [15 Useful Twitter Hacks and Plug-Ins For WordPress](https://www.smashingmagazine.com/2009/03/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [Create A Responsive, Mobile-First WordPress Theme](https://www.smashingmagazine.com/2012/06/create-responsive-mobile-first-wordpress-theme/)

If you aren’t comfortable editing your WordPress templates, a plugin is probably the best solution. If you are comfortable making a few edits to your theme, then consider manually integrating social media so that you have more control over what services appear on your website.

<a href="https://www.smashingmagazine.com/2012/01/19/facebook-twitter-google-wordpress/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b6cb4519-f27b-4311-a50d-85cf03b3f29d/social-media-icons.jpg" alt="The Big Three: Twitter, Facebook, and Google+" width="550" /></a>

{{% feature-panel %}}

Today, we’ll show you how to manually integrate the three most popular social media services on your website: Twitter, Facebook and Google+. First, you’ll learn how to integrate Facebook comments on your WordPress website, to make it easier for readers to discuss your posts. Then, we’ll show you the most common ways to display your latest tweets in the sidebar, which should encourage more people to follow you on Twitter. Finally, we’ll show you how to add sharing buttons for all three social media services to your home page, posts and pages.

Please make sure to back up all of your template files before making any changes, so that you can revert back if something goes wrong. Testing your changes in a non-production area first would also be prudent.</p>

## Integrate Facebook Comments On Your Website

Because most people are signed into Facebook when they browse the Web, enabling Facebook comments on your website is a great way to encourage people to leave comments. It also curbs spam. While many solutions purport to reduce spam comments on WordPress, most are either ineffective or frustrate visitors by blocking legitimate comments.

Feature-rich commenting solutions such as <a title="IntenseDebate" href="https://intensedebate.com/">IntenseDebate</a> and <a title="Disqus" href="https://disqus.com">Disqus</a> have benefits, of course, because they allow users to comment using Facebook and a number of other services; but before visitors can comment, they have to grant access to the application, an additional step that discourages some from commenting. By comparison, integrating Facebook comments directly enables visitors to comment with no fuss. Also, this commenting system allows users to comment by signing into Facebook, Yahoo, AOL or Hotmail.

Before <a title="Integrated Facebook Comments On WordPress Mods" href="https://www.wpmods.com/facebook-comments-added-to-wpmods/">integrating Facebook on WordPress Mods</a> at the end of September, I looked at a few solutions. I followed a <a title="Add Facebook Comments To Your WordPress Theme" href="https://wp.tutsplus.com/tutorials/add-facebook-comments-to-your-wordpress-theme/">great tutorial by Joseph Badow</a> and tried a few plugins, such as <a title="Facebook Comments For WordPress" href="https://wordpress.org/extend/plugins/facebook-comments-for-wordpress/">Facebook Comments For WordPress</a>. The reality, though, is that the <a title="official Facebook comment plugin" href="https://developers.facebook.com/docs/reference/plugins/comments/">official Facebook comment plugin</a> is the quickest and easiest way to add Facebook comments to your website.

Simply follow the steps below to get up and running.</p>

### 1. Create a Facebook Application

To use Facebook comments on your website, create a new comment application for your website on the <a title="Facebook Applications" href="https://developers.facebook.com/apps">Facebook Application</a> page. This step is required, whether you add Facebook comments manually using a third-party plugin or with the official Facebook plugin.

Simply click on the “+ Create New App” button on the Facebook Application page, and enter a unique name for your application in the “App Display Name” field. The “App Namespace” field doesn’t have to be filled in for Facebook comments (it’s used with the <a title="Facebook Open Graph Protocol" href="https://developers.facebook.com/docs/opengraph/">Facebook Open Graph Protocol</a>).

<a href="https://developers.facebook.com/apps"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ed7058f-289f-45cf-8349-f27bce024a09/create-facebook-app.png" alt="Create Facebook App" width="550" /></a>

You will then be provided with an “App ID/API key” and an “App secret key.” You don’t need to remember these numbers because the <a title="official Facebook comment plugin" href="https://developers.facebook.com/docs/reference/plugins/comments/">official Facebook comments plugin</a> automatically inserts them into the code that you need to add to your website.

<a href="https://developers.facebook.com/apps"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5a4f560-34ce-4cd9-8d5b-448ec5184c0b/create-facebook-app-2.png" alt="Create Facebook Application" width="550" /></a>

### 2. Add the Code to Your Website

Next, go back to the <a title="Facebook Comments Plugin" href="https://developers.facebook.com/docs/reference/plugins/comments/">Facebook Comments plugin</a> page and get the code for your website. The box allows you to change the URL on which comments will be placed, the number of comments to be shown, the width of the box and the color scheme (light or dark).

<a href="https://developers.facebook.com/docs/reference/plugins/comments/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03e586da-cbe2-4b0e-8f11-7d2793f1be7c/customise-facebook-app.png" alt="Customise Facebook" width="241" /></a>

You don’t have to worry about what you enter in the box because all of the attributes can be modified manually. And it doesn’t matter what URL you enter because we will be replacing it later with the WordPress permalink:

*   `href` The URL for this Comments plugin. News feed stories on Facebook will link to this URL.
*   `width` The width of the plugin in pixels. The minimum recommended width is 400 pixels.
*   `colorscheme` The color scheme for the plugin (either light or dark).
*   `num_posts` The number of comments to show by default. The default is 10, and the minimum is 1.
*   `mobile` (beta) Whether to show the mobile version. The default is `false`.

When you click on the “Get Code” button, a box will appear with your plugin code (choose the HTML5 option, because FBML is being deprecated). Make sure to select the application that you set up earlier for your comments so that the correct application ID is added to the code.

<a href="https://developers.facebook.com/docs/reference/plugins/comments/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cef89a9-155b-4786-9021-f7a7f6cdfe21/get-facebook-app-code.png" alt="Get Facebook Application Code" width="550" /></a>

Insert the first piece of code directly after the <code>&lt;body&gt;</code> tag in your <code>header.php</code> template:

<pre><code class="language-php">&lt;div id="fb-root"&gt;&lt;/div&gt;
&lt;script&gt;(function(d, s, id) {
var js, fjs = d.getElementsByTagName(s)[0];
if (d.getElementById(id)) return;
js = d.createElement(s); js.id = id;
js.src = "//connect.facebook.net/en_GB/all.js#xfbml=1&amp;appId=YOURAPPLICATIONID";
fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));&lt;/script&gt;</code></pre>

Put the second line of code where you want to show the comments. Make sure the static URL is replaced with the WordPress permalink (<code>&lt;?php the_permalink(); ?&gt;</code>) so that comments show correctly on every page of your website.

<pre><code class="language-php">&lt;div class="fb-comments" data-href="&lt;?php the_permalink(); ?&gt;" data-num-posts="15" data-width="500"&gt;&lt;/div&gt;</code></pre>

To put Facebook comments above WordPress comments, add the above code just below the line that reads <code>&lt;!-- You can start editing here. --&gt;</code> in the <code>comments.php</code> template. To put Facebook comments below WordPress comments, add the above code below the <code>&lt;/form&gt;</code> tag (again in the <code>comments.php</code> template).

If you plan to completely replace your WordPress comments with Facebook comments, simply replace the call to your <code>comments.php</code> template with the call to your Facebook comments. For example, to replace comments in posts, simply add the code to the <code>single.php</code> template. Similarly, edit the <code>page.php</code> template to show Facebook comments on pages.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b549e4a7-f9d9-4f64-b597-21c7d8f2a166/facebook-comments.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b549e4a7-f9d9-4f64-b597-21c7d8f2a166/facebook-comments.png" alt="Facebook Comments" width="550" /></a>

Your should now see the Facebook comments box displayed on your website. To get an update whenever someone leaves a comment using Facebook, add yourself as a moderator to your application on the <a title="Comment moderation tool" href="https://developers.facebook.com/tools/comments">Comment Moderation tool</a> page.

## Show Your Latest Tweets In The Sidebar

Displaying your latest tweets is a good way to encourage people to follow you on Twitter. The most common place to display tweets is in the sidebar, although you can add them to any area of the website.</p>

### Display Your Latest Tweets Manually

I have tried a few manual solutions for showing tweets on my websites, and my favorite comes from Chris Coyier of <a title="CSS Tricks" href="https://css-tricks.com/snippets/wordpress/display-rss-in-wordpress/">CSS-Tricks</a>. His <a title="Show Your Favorite Tweets with WordPress" href="https://css-tricks.com/snippets/wordpress/display-rss-in-wordpress/">RSS fetching snippet</a> is a quick and effective way to show the latest tweets from your account. The <a title="Here is How to Find Your Twitter RSS Feed and Your Twitter Favorites RSS Feed" href="https://seo-alien.com/tips-and-tricks/find-twitter-rss-feed/">RSS address of your Twitter</a> account is <code>https://api.twitter.com/1/statuses/user_timeline.rss?screen_name=xxxxx</code> (where <code>xxxxx</code> is your Twitter user name). For the tweets that you favorite, use <code>https://twitter.com/favorites/xxxxx.rss</code>. For example, the RSS for the latest tweets from Smashing Magazine is <code>https://api.twitter.com/1/statuses/user_timeline.rss?screen_name=smashingmag</code>; and to display only the favorites, <code>https://twitter.com/favorites/smashingmag.rss</code>. Once you’ve got your Twitter RSS address, simply add it to Chris’ PHP snippet.

<pre><code class="language-php">&lt;?php
include_once(ABSPATH . WPINC . '/feed.php');
$rss = fetch_feed('https://api.twitter.com/1/statuses/user_timeline.rss?screen_name=smashingmag');
$maxitems = $rss-&gt;get_item_quantity(3);
$rss_items = $rss-&gt;get_items(0, $maxitems);
?&gt;

&lt;ul&gt;
&lt;?php if ($maxitems == 0) echo '&lt;li&gt;No items.&lt;/li&gt;';
else
// Loop through each feed item and display each item as a hyperlink.
foreach ( $rss_items as $item ) : ?&gt;
&lt;li&gt;
&lt;a href='&lt;?php echo $item-&gt;get_permalink(); ?&gt;'&gt;
&lt;?php echo $item-&gt;get_title(); ?&gt;
&lt;/a&gt;
&lt;/li&gt;
&lt;?php endforeach; ?&gt;
&lt;/ul&gt;</code></pre>

For a more stylish way to display tweets manually, check out Martin Angelov’s tutorial “<a title="Display your Favorite Tweets using PHP and jQuery" href="https://tutorialzine.com/2011/08/display-favorite-tweets-php-css/">Display Your Favorite Tweets Using PHP and jQuery</a>,” or Sea of Cloud’s “Javascript Plugin Solution.”

### Display Your Latest Tweets Using the Official Twitter Widget

The official Twitter profile widget looks great and is easy to customize. You can define the number of tweets to display and whether the box should expand to show all tweets or provide a scroll bar.

The dimensions can be adjusted manually, or you can use an auto-width option. The color scheme can easily be changed in the settings area, too. Once the widget is the way you want it, simply grab the code and add it to the appropriate WordPress template.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a90cff1-d63d-45bb-80a1-db2d560d6ff6/twitter-widget.png" alt="Official Twitter Profile Widget" width="550" />

### Display Your Latest Tweets Using a WordPress Plugin

If you don’t want to code things manually or use the official Twitter profile widget, you could try one of the many plugins available:

*   [Cardoza Twitter Box](https://wordpress.org/extend/plugins/cardoza-twitter-box/ "Cardoza Twitter Box")
*   [Floating Tweets](https://wordpress.org/extend/plugins/floating-tweets/ "Floating Tweets")
*   Latest Twitter Sidebar Widget
*   [My Twitter Ticker](https://wordpress.org/extend/plugins/my-twitter-ticker/ "My Twitter Ticker")
*   [Tweet Blender](https://wordpress.org/extend/plugins/tweet-blender/ "Tweet Blender")
*   Twitter Plugin for WordPress
*   [Twitter Widget Pro](https://wordpress.org/extend/plugins/twitter-widget-pro/ "Twitter Widget Pro")

## Add Social-Media Sharing Buttons To Your WordPress Website

Adding social-media sharing and voting buttons is very straightforward and enables readers to share your content on the Web. Simply get the code directly from the following pages:

*   [Facebook](https://developers.facebook.com/docs/reference/plugins/like/ "Facebook"),
*   [Google+](https://www.google.com/webmasters/+1/button/ "Google+"),
*   [Twitter](https://twitter.com/about/resources/buttons "Twitter").

The buttons you get from the above links work well when added directly to posts (<code>single.php</code>) and pages (<code>page.php</code>). But they don’t work correctly on the home page (<code>index.php</code>) or the archive (<code>archive.php</code>) by default, because we want to show the number of likes, pluses and retweets for each individual article, rather than the page that lists the article. That is, if you simply add the default code to <code>index.php</code>, every button will show the number of shares for your home page, not for each article.

To resolve this, simply make sure that each button uses the article permalink, rather than the URL of the page it is on. To add sharing buttons only to posts, simply choose the button you want from the links above and copy the code to <code>single.php</code>; to add the buttons only to pages, just add the code to <code>page.php</code>.

To show the number of likes, pluses and retweets that an article has on the home page and in the archives, follow the steps noted below for Facebook, Google+ and Twitter below (the code for showing a sharing button on the index page will work for posts and pages, too). You can see an example of sharing buttons integrated in post excerpts on my own website <a title="WordPress Mods" href="https://www.wpmods.com">WordPress Mods</a> and on popular blogs such as <a title="Mashable" href="https://www.mashable.com">Mashable</a>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58ed1ca5-3796-4ac9-86c9-a805ad39c427/social-media-index.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58ed1ca5-3796-4ac9-86c9-a805ad39c427/social-media-index.png" alt="Social Media Sharing Buttons Example" width="500" /></a>

### Facebook

<a title="Facebook" href="https://developers.facebook.com/docs/reference/plugins/like/">Facebook’s Like button</a> comes with a lot of options. Choose from three layouts: standard, button count and box count. An email button (labelled “Send”) can be added, and you can set the width of the box, too. You can also show profile pictures below the button, choose between the labels “Like” and “Recommend,” choose between a light and dark color scheme, and set the font.

<a href="https://www.google.com/webmasters/+1/button/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3eddc94-51d8-4037-a318-03f7bca99b56/facebook-customise.png" alt="Customise Facebook" width="313" /></a>

You need to add two pieces of code to your website. First, add the JavaScript SDK code directly after the <code>&lt;body&gt;</code> tag (in the <code>header.php</code> template). This code has to be added only once (i.e. if you’ve already added the code to show Facebook comments on your website, you don’t need to add it again).

Put the second piece of code where you want to show the Like button. To ensure that the correct page is referenced, add <code>href="&lt;?php echo get_permalink($post-&gt;ID); ?&gt;"</code> to the second piece of code. It should look something like this:

<pre><code class="language-php">&lt;div class="fb-like" data-href="https://www.facebook.com/smashmag" href="&lt;?php echo get_permalink($post-&gt;ID); ?&gt;" data-send="false" data-layout="box_count" data-width="450" data-show-faces="true" data-font="arial"&gt;&lt;/div&gt;</code></pre>

More information on how to customize the Like button can be found on the <a title="Facebook Like Button" href="https://developers.facebook.com/docs/reference/plugins/like/">Facebook Like Button page</a>.</p>

### Google+

<a title="Google+" href="https://www.google.com/webmasters/+1/button/">Google+</a> offers four sizes of sharing buttons: small, medium, standard and tall. The number of votes that a page has received can be shown inline, shown in a bubble or removed altogether.

<a href="https://www.google.com/webmasters/+1/button/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7861ac52-b2ef-44b2-90b6-b0287b1f7200/googleplus-customise.png" alt="Customise Google+" width="528" /></a>

Linking to your article’s permalink is very easy. Just append <code>href="&lt;?php the_permalink(); ?&gt;"</code> to the <code>g:plusone</code> tag. For example, to show a tall inline Google+ button, you would use the following code:

<pre><code class="language-php">&lt;!-- Place this tag where you want the +1 button to render --&gt;
&lt;g:plusone size="tall" annotation="inline" href="&lt;?php the_permalink(); ?&gt;"&gt;&lt;/g:plusone&gt;

&lt;!-- Place this render call where appropriate --&gt;
&lt;script type="text/javascript"&gt;
(function() {
var po = document.createElement('script'); po.type = 'text/javascript'; po.async = true;
po.src = 'https://apis.google.com/js/plusone.js';
var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(po, s);
})();
&lt;/script&gt;</code></pre>

For more tips on customizing the Google+ button, please view the <a title="official Google+ button documentation page" href="https://developers.google.com/+/plugins/+1button/">official Google+ button documentation page</a>.</p>

### Twitter

<a title="Twitter" href="https://twitter.com/about/resources/buttons">Twitter</a> offers four types of buttons: one for sharing links, one for inviting people to follow you, a hash tag button for tweeting stories, and another for mentions (used for contacting others via Twitter). The button you need to show the number of shares that an article has gotten is called “Share a link.”

On the button customization page, you can choose whether to show the number of retweets and can append “Via,” “Recommend” and “Hashtag” mentions to the shared link.

<a href="https://twitter.com/about/resources/buttons"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60ce85e2-0a5b-4535-ae9b-f47b750783a9/twitter-customise.png" alt="Customise Twitter" width="550" /></a>

To make sure Twitter uses the title of your article and the correct URL, simply add <code>data-text="&lt;?php the_title(); ?&gt;"</code> and <code>data-url="&lt;?php the_permalink(); ?&gt;"</code> to your link. For example, if you were using the small button, you would use:

<pre><code class="language-php">&lt;a href="https://twitter.com/share" class="twitter-share-button" data-via="smashingmag" data-text="&lt;?php the_title(); ?&gt;" data-url="&lt;?php the_permalink(); ?&gt;"&gt;Tweet&lt;/a&gt;
&lt;script&gt;!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0];
if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src="//platform.twitter.com/widgets.js";
fjs.parentNode.insertBefore(js,fjs);}}(document,"script","twitter-wjs");&lt;/script&gt;</code></pre>

To show the larger button instead, simply append <code>data-size="large"</code> to the link. To show the popular vertical button (shown below) instead of the default horizontal button, append <code>data-count="vertical"</code> to the link.

<a href="https://twitter.com/about/resources/buttons"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dfcb5f2-9f68-472e-bb8d-b237650a1fb3/twitter-vertical.png" alt="Twitter Vertical Button" width="60" /></a>

For more tips on customizing the Twitter button, please view the <a title="official Twitter button documentation page" href="https://dev.twitter.com/docs/tweet-button">official Twitter button documentation page</a>.</p>

## Summary

Many WordPress users continue to use plugins to integrate social-media sharing buttons and activity on their websites. As we’ve seen, though, integrating social-media services manually is straightforward and, for many users, a better solution than simply installing a plugin and making do with whatever features it offers.

Integrating Facebook comments on your website takes only a few minutes and is much less complicated than any of the available plugins. While good tutorials are available that show you how to manually add Twitter to your website, the official widget from Twitter is the best all-around solution for most websites.

Some fantastic plugins exist for WordPress to automatically insert social-media voting buttons in your design. Installing and setting them up takes only a few minutes, although manually adding the buttons enables you to give them maximum visibility.

Remember, play it safe and make any changes in a test area first before applying the changes to the live website. I also recommend backing up all of your template files before changing anything (and your database if required). A few minutes of preparation could save you hours of troubleshooting, so try not to skip this step.

Hopefully, you’ve found this useful. If you are unsure of any aspect of this tutorial, please let us know and we’ll do our best to clarify the step or help you with it. Also, subscribe to Smashing Magazine via <a title="Subscribe to Smashing Magazine via RSS" href="https://rss1.smashingmagazine.com/feed/">RSS</a>, <a title="Subscribe to Smashing Magazine via Twitter" href="https://twitter.com/smashingmag">Twitter</a>, <a title="Subscribe to Smashing Magazine via Facebook" href="https://www.facebook.com/smashmag">Facebook</a> or <a title="Subscribe to Smashing Magazine via Google+" href="https://plus.google.com/116812091267698107544">Google+</a> to get the latest articles delivered directly to you.

{{< signature "al" >}}


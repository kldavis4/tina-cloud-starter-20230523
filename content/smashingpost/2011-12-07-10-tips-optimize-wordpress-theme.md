---
title: 10 Tips To Optimize Your WordPress Theme
slug: 10-tips-optimize-wordpress-theme
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1831c77-31cd-41ee-9de0-2a3867a7940c/wordpress-11.png
date: 2011-12-07T15:54:23.000Z
author: elio-rivero
description: >-
  The beauty of WordPress is in how easy it is to adapt for different tasks. One can extend it with just a couple of lines of code. In this post, we’ll review
  10 shortcode snippets that will tweak and optimize your WordPress theme. You can add all of these code snippets to the `functions.php` file in your WordPress theme.
categories:
  - WordPress
  - Themes
  - Optimization
  - Techniques (WP)
---

## Limit The Excerpt’s Word Count

One thing that can go wrong in WordPress magazine themes is when users include too many words before the <code>more</code> tag. Sure, they could handcraft the excerpt in the dedicated field, but on a website that has hundreds of posts and on which the text above the <code>more</code> tag has always been used as the excerpt, going back to create excerpts for all of those posts by hand would be cumbersome. In this case, we can limit the number of words shown in the excerpt by using this code:

{{% feature-panel %}}

<pre><code class="language-php">add_filter('excerpt_length', 'ilc_excerpt_length');
function ilc_excerpt_length( $length ){
  return 10;
}</code></pre>

Here, we’re using a WordPress filter hook, which is a function that parses and (usually) modifies data before it gets stored in the database or displayed on a page. In this case, we’re setting the number of words shown in the excerpt to 10.</p>

## Add A Favicon Using A WordPress Hook

Hooks allow us to insert custom code without touching the template. This gives us a lot of flexibility, because now, whenever we need to change something, we only have to change the function that’s plugged into a certain hook. For example, you can add a favicon to your website without touching the <code>header.php</code> file, just by plugging a function into the <code>wp_head</code> hook:

<pre><code class="language-php">add_action( 'wp_head', 'ilc_favicon');
function ilc_favicon(){
  echo "&lt;link rel='shortcut icon' href='" . get_stylesheet_directory_uri() . "/favicon.ico' /&gt;" . "n";
}</code></pre>

The <code>favicon.ico</code> file should be located at the root of your theme. We’re now using an action hook, which is a function that is triggered at specific points during an execution by WordPress’ core. In this case, the hook triggers any function that’s attached to it when a page is launched in the browser. But other hooks can be triggered when saving a post, registering a user and so on. Some themes even have their own action hooks, which, like WordPress’ core action hooks, can be used to launch functions at specific points of an execution.</p>

## Detect Safari On iOS

Nowadays, websites serve mobile versions using different techniques. WordPress offers a safe way to check for the mobile Safari browser so that you know when a visitor is using an iPhone or iPad.

WordPress sets the <code>$is_phone</code> variable internally, and you can use it to embed an alternative style sheet, show alternative content or display a different video format. In the following example, the <code>$is_iphone</code> variable is run, and different style sheets are applied depending on the value returned:

<pre><code class="language-php">add_action('wp_print_styles', 'ilc_enqueue_styles');
function ilc_enqueue_styles(){
  global $is_iphone;
  if( $is_iphone ){
    wp_enqueue_style('iphone-css', get_stylesheet_directory_uri() . '/iphone.css' );
  }
  else{
    wp_enqueue_style('common-css', get_stylesheet_directory_uri() . '/common.css' );
  }
}</code></pre>

In this case, we’re using the standard WordPress function <a title="wp_enqueue_style in WordPress Codex" href="https://codex.wordpress.org/Function_Reference/wp_enqueue_style"><code>wp_enqueue_style</code></a> to add styles to the <code>head</code> element of the Web page. The action that we’re attaching our function to is <code>wp_print_styles</code>; so, we’re basically telling WordPress to output the relevant style sheet when it prints all of the other required style sheets.</p>

## Remove Elements From The Header

WordPress outputs several things in the <code>head</code> section. In particular, the <code>generator</code> meta tag, the <abbr title="Really Simple Discovery">RSD</abbr> link and the <code>wlwmanifest</code> link won’t be of much use to many users:

<pre><code class="language-markup tmp-html">&lt;meta name="generator" content="WordPress 3.2.1"&gt;
&lt;link rel="EditURI" type="application/rsd+xml" title="RSD" href="https://example.com/xmlrpc.php?rsd"&gt;
&lt;link rel="wlwmanifest" type="application/wlwmanifest+xml" href="https://example.com/wp-includes/wlwmanifest.xml"&gt;</code></pre>

Some bloggers say you should get rid of the <code>generator</code> meta tag so that no one can tell which version of WordPress you’re using. But remember, you should always be using the latest version anyway.

If you don’t need XML-RPC functionality, you can remove the RSD link (the second line in the snippet above). The same goes for if you don’t use Windows Live Writer: you can safely remove the third element.

In this case, you can add this code:

<pre><code class="language-php">add_filter('the_generator', create_function(’, 'return "";'));
remove_action('wp_head', 'rsd_link');
remove_action('wp_head', 'wlwmanifest_link');</code></pre>

These lines will remove the corresponding elements in the snippet above.</p>

## Redirect WordPress Feeds To FeedBurner

It’s great that WordPress offers feeds out of the box. But if you want statistics about your subscribers, you’ll have to use FeedBurner or a similar service. To redirect your feed to one of these, use the following snippet. Thus, if you try to go to <a href="https://www.smashingmagazine.com/feed"><code>https://www.smashingmagazine.com/feed</code></a>, you’ll be redirected to <a href="https://feeds.feedburner.com/smashingmagazine">FeedBurner’s feeds for Smashing Magazine</a>.

<pre><code class="language-php">add_action('template_redirect', 'ilc_rss_redirect');
function ilc_rss_redirect() {
  if ( is_feed() &amp;&amp; !preg_match('/feedburner|feedvalidator/i', $_SERVER['HTTP_USER_AGENT'])){
    header('Location: https://feeds.feedburner.com/smashingmagazine');
    header('HTTP/1.1 302 Temporary Redirect');
  }
}</code></pre>

Replace <code>https://feeds.feedburner.com/smashingmagazine</code> with the URL for your own feed from FeedBurner.</p>

## Show Featured Images In Feed

To encourage subscribers to visit your website, rather than letting them just consume content through your RSS feed, you might want to display only the excerpt and featured image of posts. But WordPress doesn’t display the featured image in the RSS feed by default. Use the following code to do so. You can even add HTML to it.

<pre><code class="language-php">add_filter('the_content_feed', 'rss_post_thumbnail');
function rss_post_thumbnail($content) {
  global $post;
  if( has_post_thumbnail($post-&gt;ID) )
    $content = '&lt;p&gt;' . get_the_post_thumbnail($post-&gt;ID, 'thumbnail') . '&lt;/p&gt;' . $content;
  return $content;
}</code></pre>

## Show Content Only To RSS Subscribers

To increase subscribers to your RSS feed, you could offer a gift available only to them. The code below creates a new <a href="https://codex.wordpress.org/Shortcode_API">shortcode</a> with which to wrap content in order to hide it from regular visitors but not from RSS subscribers.

<pre><code class="language-php">add_shortcode( 'feedonly', 'ilc_feedonly' );
function ilc_feedonly( $atts, $content = null ) {
  if( is_feed() ) return '&lt;p&gt;' . $content . '&lt;/p&gt;';
  else return;
}</code></pre>

## Show Content Only To Logged-In Users

In the same vein, you could show content only to registered users of your website. The code below creates a new <a href="https://codex.wordpress.org/Shortcode_API">shortcode</a> with which to wrap content in order to hide it from casual visitors but not logged-in users.

<pre><code class="language-php">add_shortcode( 'loggedin', 'ilc_loggedin' );
function ilc_loggedin( $atts, $content = null ) {
  if( is_user_logged_in() ) return '&lt;p&gt;' . $content . '&lt;/p&gt;';
  else return;
}</code></pre>

## Display Links For Sharing Posts On Social Networks

If, for some reason, you don’t want to use the standard Facebook, Twitter and other social-networking buttons for sharing posts, you can add your own links with the code below, perhaps using it in conjunction with one of Smashing Magazine’s icon sets, such as <a title="Flavours Icon Set on Smashing Magazine" href="https://www.smashingmagazine.com/2009/01/23/friday-freebies-flavours-icon-set-and-cute-tweeters-icon-set/">Flavours</a>.

Here, we’ll be filtering the content using the <code>the_content</code> function. But, unlike what we did when we adjusted the excerpt’s length or removed the <code>generator</code> meta tag, we don’t want to overwrite it, but rather to append our links to it. So, this filter returns the post’s original content, concatenating our social-networking links right after it.

<pre><code class="language-php">add_filter( 'the_content', 'ilc_share' );
function ilc_share( $content ) {
  global $post;
  $postlink  = get_permalink($post-&gt;ID);
  $posttitle = get_the_title($post-&gt;ID);
  $html = '&lt;ul class="share-entry"&gt;';
  // Twitter
  $html .= '&lt;li&gt;&lt;a class="share-twitter" title="Share on Twitter" rel="external" href="https://twitter.com/share?text='.$posttitle.'&amp;url='.$postlink.'"&gt;Share on Twitter&lt;/a&gt;&lt;/li&gt;';
  // Facebook
  $html .= '&lt;li&gt;&lt;a class="share-facebook" title="Share on Facebook" rel="external" href="https://www.facebook.com/share.php?u=' . $postlink . '"&gt;Share on Facebook&lt;/a&gt;&lt;/li&gt;';
  // LinkedIn
  $html .= '&lt;li&gt;&lt;a class="share-linkedin" title="Share on LinkedIn" rel="external" href="https://www.linkedin.com/shareArticle?mini=true&amp;url=' . $postlink . '&amp;title=' . $posttitle . '"&gt;Share on LinkedIn&lt;/a&gt;&lt;/li&gt;';
  // Digg
  $html .= '&lt;li&gt;&lt;a class="share-digg" title="Share on Digg" rel="external" href="https://digg.com/submit?url=' . $postlink . '"&gt;Share on Digg&lt;/a&gt;&lt;/li&gt;';
  // StumbleUpon
  $html .= '&lt;li&gt;&lt;a class="share-stumbleupon" title="Share on StumbleUpon" rel="external" href="https://www.stumbleupon.com/submit?url=' . $postlink . '&amp;title=' . $posttitle . '"&gt;Share on StumbleUpon&lt;/a&gt;&lt;/li&gt;';
  // Google+
  $html .= '&lt;li&gt;&lt;a class="share-googleplus" title="Share on Google+" rel="external" href="https://plusone.google.com/_/+1/confirm?url=' . $postlink . '"&gt;Share on Google+&lt;/a&gt;&lt;/li&gt;';
  $html .= '&lt;/ul&gt;';
  return $content . $html;
}</code></pre>

This code will add the links both in the full view for posts and on the archive pages (such as the category and tag pages). If you want them to appear only in the full view for posts, then add the following right before <code>global $post;</code>:

<pre><code class="language-php">if( !is_singular() ) return $content;</code></pre>

This way, the links will be appended only when the user visits the full post or the page for an image.</p>

## Add Logo To The Log-In Page

To add your logo to the log-in page for administrators, use the <code>login_head</code> action hook, which executes all functions that are attached to it in the log-in page’s <code>head</code> element. We’re doing two things here: changing the logo, and changing the link that it points to.

<pre><code class="language-php">add_action( 'login_head', 'ilc_custom_login');
function ilc_custom_login() {
  echo '&lt;style type="text/css"&gt;
  h1 a { background-image:url('. get_stylesheet_directory_uri() . '/images/login-logo.png' . ') !important; margin-bottom: 10px; }
  padding: 20px;}
  &lt;/style&gt;
  &lt;script type="text/javascript"&gt;window.onload = function(){document.getElementById("login").getElementsByTagName("a")[0].href = "'. home_url() . '";document.getElementById("login").getElementsByTagName("a")[0].title = "Go to site";}&lt;/script&gt;';
}</code></pre>

The CSS code will replace the WordPress logo with your own. You can adjust the path to the image in the fourth line of the code above to suit your theme.

In addition, the JavaScript changes the logo’s URL, so that you jump not to <code>wordpress.org</code> but to your own home page.</p>

## Closing Thoughts

We’ve seen how to customize WordPress’ social-network links and icons, how to show content only to logged-in users, how to customize the RSS feed and more. But the most important thing to take away is that you can build on this in endless ways. For example, you could add social-network links only in your feed, or add your logo to the bottom of the feed, or customize the log-in page using CSS, to name just a few possibilities.

Action hooks and filters are effective tools for tweaking the output of a theme, whether written to the database or run in the visitor’s browser. You can read more about <a title="WordPress Action Hooks" href="https://codex.wordpress.org/Plugin_API/Action_Reference">actions</a> and <a title="WordPress Filter Hooks" href="https://codex.wordpress.org/Plugin_API/Filter_Reference">filters</a> in the WordPress Codex.

{{< signature "al" >}}


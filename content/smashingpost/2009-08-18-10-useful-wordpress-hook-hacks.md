---
title: 10 Useful WordPress Hook Hacks
slug: 10-useful-wordpress-hook-hacks
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a13dbbb2-6e5c-4a3e-9ef9-629e01b73763/sm6.jpg'
date: 2009-08-18T14:21:00.000Z
author: jean-baptiste-jung
description: >-
  Hooks are very useful in WordPress. They allow you to "hook" a custom function to an existing function, which allows you to modify WordPress' functionality without editing core files. In this article, we have compiled **10 extremely useful ready-to-use WordPress hooks**, along with examples and coding explanations.
categories:
  - WordPress
  - Hacks
  - Hooks
  - Techniques (WP)
---

## What Is A Hook?

To achieve a particular effect on a WordPress blog, you have to modify how WordPress works. Some of these modifications are made to what WordPress developers call "core files," files required by WordPress to work properly.

{{% feature-panel %}}

But modifying core files is always a bad idea. It may create a security loophole. Also, you will have lost the modification when you upgrade your WordPress installation.

Still, developers need to overwrite some of WordPress' functionality, which is why WordPress provides the <a href="https://codex.wordpress.org/Plugin_API">Plugin API</a>.

Hooks are one of the main building blocks of WordPress plug-ins. Almost every plug-in uses a hook to overwrite WordPress' core functionality.</p>

### How to Use Hooks on Your WordPress Blog

Unless you're writing a plug-in, you would write hooks in the <em>functions.php</em> file. This file is located in the <em>wp-content/themes/yourtheme</em> directory.

A hook, as you would expect, "hooks" one function to another. For example, you could write a custom function and attach it to one of WordPress' core functions:

<pre><code class="language-php">add_action ( 'publish_post', 'myCustomFunction' );</code></pre>

In this example, we hook our own custom function to WordPress' <code>publish-post</code> function, which means that every time WordPress executes the <code>publish-post</code> function, it will also execute this hooked function.

Of course, we can also remove hooks using the <code>remove_action()</code> function:

<pre><code class="language-php">remove_action ( 'publish_post', 'myCustomFunction' );</code></pre>

<strong>Hooks resources:</strong>

*   [WordPress plugin API Codex page](https://codex.wordpress.org/Plugin_API)
*   [Adam Brown's hook database](https://adambrown.info/p/wp_hooks)
*   [Hooks from WpRecipes](https://www.wprecipes.com/?s=hook)

## 1\. Disable WordPress' Automatic Formatting

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68bb059b-476d-4c27-a4de-9d8ee1f8a3e7/sm1.png" alt="Screenshot" />

<strong>The problem</strong>.
You have probably noticed that, by default, WordPress converts normal quotes to "curly" quotes, and makes other little formatting changes when a post is displayed.

This is very cool for people who publish normal content, but anyone who uses their blog to discuss code will be annoyed because, when pasted in a text editor, code with curly quotes returns syntax errors.

<strong>The solution</strong>.
Simply paste the following code in your <em>functions.php</em> file:

<pre><code class="language-php">function my_formatter($content) {
  $new_content = ’;
  $pattern_full = '{([raw].*?[/raw])}is';
  $pattern_contents = '{[raw](.*?)[/raw]}is';
  $pieces = preg_split($pattern_full, $content, -1, PREG_SPLIT_DELIM_CAPTURE);

  foreach ($pieces as $piece) {
    if (preg_match($pattern_contents, $piece, $matches)) {
      $new_content .= $matches[1];
    } else {
      $new_content .= wptexturize(wpautop($piece));
    }
  }

  return $new_content;
}

remove_filter('the_content', 'wpautop');
remove_filter('the_content', 'wptexturize');

add_filter('the_content', 'my_formatter', 99);</code></pre>

Once that's done, you can use the <code>[raw]</code> shortcode in your posts:

<pre><code class="language-php">[raw]This text will not be automatically formatted.[/raw]</code></pre>

<strong>Code explanation</strong>.
Our first step here was to create a function that uses a regular expression to find the <code>[raw]</code> shortcode in your posts' content.

Then we hook our <code>my_formatter()</code> function to WordPress' <code>the_content()</code> function, which means that <code>my_formatter()</code> will now be automatically called every time <code>the_content()</code> is called.

To remove the automatic formatting, we use the <code>remove_filter()</code> function, which lets you delete a hook on a specific function.

<strong>Source:</strong>

*   [Disable WordPress automatic formatting on posts using a shortcode](https://www.wprecipes.com/disable-wordpress-automatic-formatting-on-posts-using-a-shortcode)

## 2\. Detect The Visitor's Browser Using A Hook

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70557fd8-3f48-456d-bee1-40f97d050818/sm2.jpg" alt="Screenshot" />

<strong>The problem</strong>.
Cross-browser compatibility is probably the most common problem in Web development. You will save yourself a lot of headaches if you are able to detect the browsers that people use to visit your website and then create a custom class wrapped in the <code>body</code> tag. Few people are aware of it, but WordPress can already detect browsers, and a few global variables are available for us to use.

<strong>The solution</strong>.
Nothing hard here: just paste the code below in your <em>functions.php</em> file, then save the file and you're done!

<pre><code class="language-php">&lt;?php
add_filter('body_class','browser_body_class');
function browser_body_class($classes) {
  global $is_lynx, $is_gecko, $is_IE, $is_opera, $is_NS4, $is_safari, $is_chrome, $is_iphone;

  if($is_lynx) $classes[] = 'lynx';
  elseif($is_gecko) $classes[] = 'gecko';
  elseif($is_opera) $classes[] = 'opera';
  elseif($is_NS4) $classes[] = 'ns4';
  elseif($is_safari) $classes[] = 'safari';
  elseif($is_chrome) $classes[] = 'chrome';
  elseif($is_IE) $classes[] = 'ie';
  else $classes[] = 'unknown';

  if($is_iphone) $classes[] = 'iphone';
  return $classes;
}
?&gt;</code></pre>

Once you have saved the file, the function will automatically add a CSS class to the <code>body</code> tag, as shown in the example below:

<pre><code class="language-php">&lt;body class="home blog logged-in safari"&gt;</code></pre>

<strong>Code explanation</strong>.
WordPress has global variables that return <code>true</code> if a visitor is using a particular browser. If the visitor's browser is Google Chrome, the <code>$is_chrome</code> variable will return <code>true</code>. This is why we create the <code>browser_body_class()</code> function, which returns the name of the visitor's browser. Once that's done, we just hook the function to WordPress' <code>body_class()</code> function.

<strong>Sources:</strong>

*   [Browser Detection and the body_class() Function](https://www.nathanrice.net/blog/browser-detection-and-the-body_class-function/)
*   [How to detect the visitor's browser within WordPress](https://www.wprecipes.com/how-to-detect-the-visitor-browser-within-wordpress)

## 3\. Define Default Text In TinyMCE

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d16fb2a2-22fe-499f-be8a-f1a4020f5485/sm3.png" alt="Screenshot" />

<strong>The problem</strong>.
Many bloggers almost always use the same layout for their blog posts. Posts on my own blog WpRecipes.com are always displayed the same way: some text, some code and then some more text.

What about saving time by forcing tinyMCE (WordPress' visual editor) to display default text?

<strong>The solution</strong>.
Once again, hooks are the solution. Just open your <em>functions.php</em> file, paste the code and let the hooks work their magic!

<pre><code class="language-php">&lt;?php
add_filter('default_content', 'my_editor_content');

function my_editor_content( $content ) {
  $content = "If you enjoyed this post, make sure to subscribe to my rss feed.";
  return $content;
}
?&gt;</code></pre>

<strong>Code explanation</strong>.
This code is powerful, and yet the method is so simple. Just create a function that returns the desired text (in this example, we have defined some simple text that asks readers to subscribe to the blog's RSS feed), and hook the function to WordPress' <code>default_content()</code> function. That's it.

<strong>Sources:</strong>

*   [How to preset text in the WordPress post editor](https://justintadlock.com/archives/2009/04/05/how-to-preset-text-in-the-wordpress-post-editor)
*   [How to: Automatically insert text in WordPress editor](https://www.wprecipes.com/how-to-automatically-insert-text-in-wordpress-editor)

## 4\. Insert Content Automatically After Each Post

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3206540b-13ac-44c2-9432-0d8cf6cb4b12/sm4.jpg" alt="Screenshot" />

<strong>The problem</strong>.
Most blogs use the <em>single.php</em> template to insert some text, images or ads just after a post. Sure, this can be done by opening <em>single.php</em> and pasting the desired text after the <code>the_content()</code> function. But the text won't show up in your RSS feed? Hooks and the technique described below solve this problem.

<strong>The solution</strong>.
One again, simply paste the code below in the <em>functions.php</em> file of your theme. That's it.

<pre><code class="language-php">function insertFootNote($content) {
        if(!is_feed() &amp;&amp; !is_home()) {
                $content.= "&lt;div class='subscribe'&gt;";
                $content.= "&lt;h4&gt;Enjoyed this article?&lt;/h4&gt;";
                $content.= "&lt;p&gt;Subscribe to our  &lt;a href='https://feeds2.feedburner.com/WpRecipes'&gt;RSS feed&lt;/a&gt; and never miss a recipe!&lt;/p&gt;";
                $content.= "&lt;/div&gt;";
        }
        return $content;
}
add_filter ('the_content', 'insertFootNote');</code></pre>

<strong>Code explanation</strong>.
The purpose of the <code>insertFootNote()</code> function is pretty simple: it simply concatenates text of your choice to the <code>$content</code> variable, which contains your post's content.

Then, our <code>insertFootNote()</code> function is hooked to the <code>the_content()</code> function, and it is automatically called every time the <code>the_content</code> is called. Using this function is basically the same as typing in the text at the end of each post.

Notice the <code>(!is_feed)</code> condition on line 2, which prevents the text from being inserted in the RSS feed. If you want the text to appear in your RSS feed, replace line 2 with the following:

<pre><code class="language-php">if (!is_home()) {</code></pre>

<strong>Sources:</strong>

*   [How to: Automatically insert content after each post](https://www.wprecipes.com/how-to-automatically-insert-content-after-each-post)

## 5\. Disable The "Please Update Now" Message On WordPress Dashboard

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/967d531e-56b6-4d31-9ec9-e5f8d225eb5f/sm5.png" alt="Screenshot" />

<strong>The problem</strong>.
Your dashboard automatically lets you know when a new version of WordPress is released by inserting a message at the top of admin pages. This is definitely a good thing, because updating gives your blog the latest functions and security fixes. But if the blog is a client project, letting the client control updates may not be a good idea.

<strong>The solution</strong>.
Just paste these four lines of code in your <em>functions.php</em> file:

<pre><code class="language-php">if (!current_user_can('edit_users')) {
  add_action( 'init', create_function( '$a', "remove_action( 'init', 'wp_version_check' );" ), 2 );
  add_filter( 'pre_option_update_core', create_function( '$a', "return null;" ) );
}</code></pre>

Once you save <em>functions.php</em>, you won't see the message on the dashboard.

<strong>Code explanation</strong>.
The first thing we do here is make sure the current user has sufficient administrative rights to update WordPress. Once we do that, we just create two hooks to overwrite the automatic check for updates and message display.

<strong>Sources:</strong>

*   [How to: Disable the "Please update now" message on WP dashboard](https://www.wprecipes.com/how-to-disable-the-please-update-now-message-in-wp-dashboard)

## 6\. Disable WordPress From Auto-Saving Posts

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc3a8e5e-9941-48be-a812-c81ad9ab7bf0/sm6.jpg" alt="Screenshot" /><br>
<em>Photo by <a href="https://www.flickr.com/photos/thatcanadiangirl/">thatcanadiangirl</a></em>

<strong>The problem</strong>.
As you type a post in the dashboard, WordPress periodically saves the content. This is a useful feature, but sometimes you may want to disable it.

<strong>The solution</strong>.
To disable WordPress' auto-saving functionality, simply open the <em>functions.php</em> file and paste the following function:

<pre><code class="language-php">function disableAutoSave(){
    wp_deregister_script('autosave');
}
add_action( 'wp_print_scripts', 'disableAutoSave' );</code></pre>

<strong>Code explanation</strong>.
Again, nothing hard about this code. We simply create an action (on line 4) and hook the <code>disableAutoSave()</code> function that we created on line 1 to WordPress' <code>wp_print_scripts()</code>.

The result is that our <code>disableAutoSave()</code> function is called every time WordPress executes <code>wp_print_scripts()</code>. This way, we make sure the auto-save functionality is disabled.

<strong>Sources:</strong>

*   [WordPress hook: Disable posts auto-saving](https://www.wprecipes.com/wordpress-hook-disable-posts-auto-saving)

## 7\. Prevent Duplicate Content On Comment Pages

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20e860ad-542b-4e93-936a-c8b8cbbbbc15/sm7.jpg" alt="Screenshot" />

<strong>The problem</strong>.
Duplicate content is an SEO problem for many websites. It can also be a problem for your WordPress blog if you don't apply a few tricks.

Introduced in version 2.7, paged comments is a great addition to WordPress because it lets bloggers split comments into multiple pages. The only problem, again, is the risk of duplicate content.

Let's use the new <code>rel="canonical"</code> attribute to prevent duplicate content in paged comments.

<strong>The solution</strong>.
Simply paste the following code in your <em>function.php</em> file:

<pre><code class="language-php">function canonical_for_comments() {
  global $cpage, $post;
  if ( $cpage &gt; 1 ) :
    echo "n";
      echo "&lt;link rel='canonical' href='";
      echo get_permalink( $post-&gt;ID );
      echo "' /&gt;n";
   endif;
}

add_action( 'wp_head', 'canonical_for_comments' );</code></pre>

<strong>Code explanation</strong>.
First, we create a function to add the <code>rel="canonical"</code> attribute to comment pages, except page 1. Then we hook this function to WordPress' <code>wp_head()</code> function. As simple as that!

<strong>Sources:</strong>

*   [WordPress hack: Canonical links for comments](https://www.wprecipes.com/wordpress-hack-canonical-links-for-comments)

## 8\. Get Entire Post Or Page In A PHP Variable

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bce242b7-1343-4887-8d45-6bae955575de/sm8.jpg" alt="Screenshot" />

<strong>The problem</strong>.
Being able to get the entire current post or page as a PHP variable is definitely a good thing. You could, for example, replace parts of the content using the <code>str_replace()</code> PHP function, and much more.

<strong>The solution</strong>.
Once again, nothing hard. Just paste the following in your <em>function.php</em> file.

<pre><code class="language-php">function callback($buffer) {
  // modify buffer here, and then return the updated code return $buffer;
}

function buffer_start() {
  ob_start("callback");
}

function buffer_end() {
  ob_end_flush();
}

add_action('wp_head', 'buffer_start');
add_action('wp_footer', 'buffer_end');</code></pre>

<strong>Code explanation</strong>.
To achieve this hack, we need three functions:

*   `callback()`: this function returns the whole page as a variable called `$buffer`. You can modify it before returning it by using regular expressions, for example.
*   `buffer_start()`: this function simply starts the buffer. It is hooked to WordPress' `wp_head()` function.
*   `buffer_end()`: this function clears the buffer. It is hooked to WordPress' `wp_footer()` function.

Once we have our function, we just hook it to existing WordPress functions.

<strong>Sources:</strong>

*   [WordPress Hook for Entire Page Using Output Buffering](https://www.dagondesign.com/articles/wordpress-hook-for-entire-page-using-output-buffering/)

## 9\. Use Hooks And Cron To Schedule Events

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f8f152e-6126-445b-9011-a9a103ad5966/sm9.jpg" alt="Screenshot" />

<strong>The problem</strong>.
You probably already know that WordPress can schedule events. For example, it can publish posts at preset dates and times. Using hooks and <code>wp-cron</code>, we can easily schedule our own events. In this example, we will get our WordPress blog to send us an email once hourly.

<strong>The solution</strong>.
Paste the following code block in the <em>functions.php</em> file of your theme.

<pre><code class="language-php">if (!wp_next_scheduled('my_task_hook')) {
  wp_schedule_event( time(), 'hourly', 'my_task_hook' );
}

add_action( 'my_task_hook', 'my_task_function' );

function my_task_function() {
  wp_mail('you@yoursite.com', 'Automatic email', 'Hello, this is an automatically scheduled email from WordPress.');
}</code></pre>

<strong>Code explanation</strong>.
The first thing we did, of course, was create a function that performs the desired action. In this example, the function is called <code>my_task_function()</code> and it just sends an email to the specified email address.

To schedule an event, we have to use the <code>wp_schedule_event()</code> function. The last argument has to be a hook, which is why we hook our <code>my_task_function()</code> function to <code>my_task_hook</code>.

<strong>Sources:</strong>

*   Timing is everything: scheduling in WordPress

## 10\. List All Hooked Functions

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89ae5b0b-f432-4082-91f1-eefd1b089199/sm10.png" alt="Screenshot" />

<strong>The problem</strong>.
When things go wrong, listing all hooked functions can be very useful for debugging.

<strong>The solution</strong>.
As with the others, this code has to be pasted in your <em>functions.php</em> file. When you have finished debugging, don't forget to remove the code from <em>functions.php</em>, or else the debugging message will continue to appear.

<pre><code class="language-php">function list_hooked_functions($tag=false){
 global $wp_filter;
 if ($tag) {
  $hook[$tag]=$wp_filter[$tag];
  if (!is_array($hook[$tag])) {
  trigger_error("Nothing found for '$tag' hook", E_USER_WARNING);
  return;
  }
 }
 else {
  $hook=$wp_filter;
  ksort($hook);
 }
 echo '&lt;pre&gt;';
 foreach($hook as $tag =&gt; $priority){
  echo "&lt;br /&gt;&amp;gt;&amp;gt;&amp;gt;&amp;gt;&amp;gt;t&lt;strong&gt;$tag&lt;/strong&gt;&lt;br /&gt;";
  ksort($priority);
  foreach($priority as $priority =&gt; $function){
  echo $priority;
  foreach($function as $name =&gt; $properties) echo "t$name&lt;br /&gt;";
  }
 }
 echo '&lt;/pre&gt;';
 return;
}</code></pre>

*   [How to: Disable the "Please update now" message on WP dashboard](https://www.wprecipes.com/how-to-disable-the-please-update-now-message-in-wp-dashboard)

## 6\. Disable WordPress From Auto-Saving Posts

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc3a8e5e-9941-48be-a812-c81ad9ab7bf0/sm6.jpg" alt="Screenshot" /><br>
<em>Photo by <a href="https://www.flickr.com/photos/thatcanadiangirl/">thatcanadiangirl</a></em>

<strong>The problem</strong>.
As you type a post in the dashboard, WordPress periodically saves the content. This is a useful feature, but sometimes you may want to disable it.

<strong>The solution</strong>.
To disable WordPress' auto-saving functionality, simply open the <em>functions.php</em> file and paste the following function:

<pre><code class="language-php">function disableAutoSave(){
    wp_deregister_script('autosave');
}
add_action( 'wp_print_scripts', 'disableAutoSave' );</code></pre>

<strong>Code explanation</strong>.
Again, nothing hard about this code. We simply create an action (on line 4) and hook the <code>disableAutoSave()</code> function that we created on line 1 to WordPress' <code>wp_print_scripts()</code>.

The result is that our <code>disableAutoSave()</code> function is called every time WordPress executes <code>wp_print_scripts()</code>. This way, we make sure the auto-save functionality is disabled.

<strong>Sources:</strong>

*   [WordPress hook: Disable posts auto-saving](https://www.wprecipes.com/wordpress-hook-disable-posts-auto-saving)

## 7\. Prevent Duplicate Content On Comment Pages

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20e860ad-542b-4e93-936a-c8b8cbbbbc15/sm7.jpg" alt="Screenshot" />

<strong>The problem</strong>.
Duplicate content is an SEO problem for many websites. It can also be a problem for your WordPress blog if you don't apply a few tricks.

Introduced in version 2.7, paged comments is a great addition to WordPress because it lets bloggers split comments into multiple pages. The only problem, again, is the risk of duplicate content.

Let's use the new <code>rel="canonical"</code> attribute to prevent duplicate content in paged comments.

<strong>The solution</strong>.
Simply paste the following code in your <em>function.php</em> file:

<pre><code class="language-php">function canonical_for_comments() {
  global $cpage, $post;
  if ( $cpage &gt; 1 ) :
    echo "n";
      echo "&lt;link rel='canonical' href='";
      echo get_permalink( $post-&gt;ID );
      echo "' /&gt;n";
   endif;
}

add_action( 'wp_head', 'canonical_for_comments' );</code></pre>

<strong>Code explanation</strong>.
First, we create a function to add the <code>rel="canonical"</code> attribute to comment pages, except page 1. Then we hook this function to WordPress' <code>wp_head()</code> function. As simple as that!

<strong>Sources:</strong>

*   [WordPress hack: Canonical links for comments](https://www.wprecipes.com/wordpress-hack-canonical-links-for-comments)

## 8\. Get Entire Post Or Page In A PHP Variable

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bce242b7-1343-4887-8d45-6bae955575de/sm8.jpg" alt="Screenshot" />

<strong>The problem</strong>.
Being able to get the entire current post or page as a PHP variable is definitely a good thing. You could, for example, replace parts of the content using the <code>str_replace()</code> PHP function, and much more.

<strong>The solution</strong>.
Once again, nothing hard. Just paste the following in your <em>function.php</em> file.

<pre><code class="language-php">function callback($buffer) {
  // modify buffer here, and then return the updated code return $buffer;
}

function buffer_start() {
  ob_start("callback");
}

function buffer_end() {
  ob_end_flush();
}

add_action('wp_head', 'buffer_start');
add_action('wp_footer', 'buffer_end');</code></pre>

<strong>Code explanation</strong>.
To achieve this hack, we need three functions:

*   `callback()`: this function returns the whole page as a variable called `$buffer`. You can modify it before returning it by using regular expressions, for example.
*   `buffer_start()`: this function simply starts the buffer. It is hooked to WordPress' `wp_head()` function.
*   `buffer_end()`: this function clears the buffer. It is hooked to WordPress' `wp_footer()` function.

Once we have our function, we just hook it to existing WordPress functions.

<strong>Sources:</strong>

*   [WordPress Hook for Entire Page Using Output Buffering](https://www.dagondesign.com/articles/wordpress-hook-for-entire-page-using-output-buffering/)

## 9\. Use Hooks And Cron To Schedule Events

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f8f152e-6126-445b-9011-a9a103ad5966/sm9.jpg" alt="Screenshot" />

<strong>The problem</strong>.
You probably already know that WordPress can schedule events. For example, it can publish posts at preset dates and times. Using hooks and <code>wp-cron</code>, we can easily schedule our own events. In this example, we will get our WordPress blog to send us an email once hourly.

<strong>The solution</strong>.
Paste the following code block in the <em>functions.php</em> file of your theme.

<pre><code class="language-php">if (!wp_next_scheduled('my_task_hook')) {
  wp_schedule_event( time(), 'hourly', 'my_task_hook' );
}

add_action( 'my_task_hook', 'my_task_function' );

function my_task_function() {
  wp_mail('you@yoursite.com', 'Automatic email', 'Hello, this is an automatically scheduled email from WordPress.');
}</code></pre>

<strong>Code explanation</strong>.
The first thing we did, of course, was create a function that performs the desired action. In this example, the function is called <code>my_task_function()</code> and it just sends an email to the specified email address.

To schedule an event, we have to use the <code>wp_schedule_event()</code> function. The last argument has to be a hook, which is why we hook our <code>my_task_function()</code> function to <code>my_task_hook</code>.

<strong>Sources:</strong>

*   Timing is everything: scheduling in WordPress

## 10\. List All Hooked Functions

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89ae5b0b-f432-4082-91f1-eefd1b089199/sm10.png" alt="Screenshot" />

<strong>The problem</strong>.
When things go wrong, listing all hooked functions can be very useful for debugging.

<strong>The solution</strong>.
As with the others, this code has to be pasted in your <em>functions.php</em> file. When you have finished debugging, don't forget to remove the code from <em>functions.php</em>, or else the debugging message will continue to appear.

<pre><code class="language-php">function list_hooked_functions($tag=false){
 global $wp_filter;
 if ($tag) {
  $hook[$tag]=$wp_filter[$tag];
  if (!is_array($hook[$tag])) {
  trigger_error("Nothing found for '$tag' hook", E_USER_WARNING);
  return;
  }
 }
 else {
  $hook=$wp_filter;
  ksort($hook);
 }
 echo '&lt;pre&gt;';
 foreach($hook as $tag =&gt; $priority){
  echo "&lt;br /&gt;&amp;gt;&amp;gt;&amp;gt;&amp;gt;&amp;gt;t&lt;strong&gt;$tag&lt;/strong&gt;&lt;br /&gt;";
  ksort($priority);
  foreach($priority as $priority =&gt; $function){
  echo $priority;
  foreach($function as $name =&gt; $properties) echo "t$name&lt;br /&gt;";
  }
 }
 echo '&lt;/pre&gt;';
 return;
}</code></pre>

Once that's done, simply call the <code>list_hooked_functions()</code> function, as shown below, to print all hooked WordPress functions on your screen.

<pre><code class="language-php">list_hooked_functions();</code></pre>

<strong>Code explanation</strong>.
If no hook name is provided to the function as an argument, then hooks are printed to the screen using the global variable <code>$wp_filter</code>. Alternatively, you can list one particular hook by passing its name as an attribute:

<pre><code class="language-php">list_hooked_functions('wp_head');</code></pre>

## Related posts

You may be interested in the following related posts:

*   [10 Handy WordPress Comments Hacks](https://www.smashingmagazine.com/2009/07/23/10-wordpress-comments-hacks/)
*   [Power Tips For WordPress Template Developers](https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/)
*   [10 Useful WordPress Loop Hacks](https://www.smashingmagazine.com/2009/06/10/10-useful-wordpress-loop-hacks/)
*   [Custom Field Hacks For WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/)
*   [15 Useful Twitter Hacks and Plugins For WordPress](https://www.smashingmagazine.com/2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [Mastering WordPress Shortcuts](https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/)

{{< signature "al" >}}


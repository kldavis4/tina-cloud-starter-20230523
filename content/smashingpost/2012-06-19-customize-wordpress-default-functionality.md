---
title: Easily Customize WordPress’ Default Functionality
slug: customize-wordpress-default-functionality
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aecccd29-a723-43f3-9a2f-7a87a4ccfcb2/wordpress-money-green.jpg
date: 2012-06-19T08:27:08.000Z
author: joseph-casabona
description: >-
  The absolute best thing about WordPress is how flexible it is. Don't like it?
  Change the theme. Need added functionality? There is probably a plugin you can download or buy. If not, built it yourself! You can change pretty much everything about WordPress. In this article I'm going to go over some easy ways to customize WordPress that you may not know about.
categories:
  - WordPress
  - Themes
  - Tutorials
---
## Change The Default Source Of jQuery

Another great thing about WordPress is that it comes locked and loaded with all kinds of JavaScript libraries, including jQuery. It also gives you the power to change the source of those libraries according to your needs.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How Commercial Plugin Developers Are Using The Repository](https://www.smashingmagazine.com/2012/01/commercial-plugin-developers-wordpress-repository/)
*   [WordPress Essentials: How To Create A WordPress Plugin](https://www.smashingmagazine.com/2011/09/how-to-create-a-wordpress-plugin/)
*   [Guide To WordPress Coding Standards](https://www.smashingmagazine.com/2012/07/guide-wordpress-coding-standards/)
*   [Writing Unit Tests For WordPress Plugins](https://www.smashingmagazine.com/2012/03/writing-unit-tests-for-wordpress-plugins/)

{{% feature-panel %}}

Let’s say we want to relieve our server of some stress by switching WordPress’ version of jQuery for a hosted solution (or <abbr title="Content Delivery Network">CDN</abbr> version). We can very easily change the source of jQuery with this function:

<pre><code class="language-php">function add_scripts() {
    wp_deregister_script( 'jquery' );
    wp_register_script( 'jquery', 'https://code.jquery.com/jquery-1.7.1.min.js');
    wp_enqueue_script( 'jquery' );
}

add_action('wp_enqueue_scripts', 'add_scripts');</code></pre>

Three things are going on here. First, we’re using <code>wp_deregister_script()</code> to tell WordPress to forget about the version of jQuery currently being used. We then use <code>wp_register_script()</code> to re-register jQuery (as the script name), using jQuery’s own CDN version. Finally, we use <code>wp_enqueue_script()</code> to add jQuery to our theme or plugin.

One thing to note here is that we’re using <code>add_action()</code>, not <code>add_filter()</code>, to add our scripts. Because we’re not making any changes to the content, but instead relying on WordPress to do something in order for our scripts to load, we use an action hook, not a filter hook. Read about both <a href="https://codex.wordpress.org/Plugin_API">in the WordPress Codex</a>.</p>

## Add Image Sizes

We know that WordPress sets a few different sizes for the images we upload. Did you know you can also (relatively easily) set your own image sizes? And all with two simple functions. If we have a custom header image for our posts with dimensions of 760 × 300 pixels, we could make our images upload to that size with this:

<pre><code class="language-php">add_theme_support( 'post-thumbnails' );
add_image_size( 'post-header', 760, 300, true );</code></pre>

The first function, <code>add_theme_support()</code>, tells WordPress to allow not just for thumbnails, but for featured images and images of new sizes. The second line, <code><a href="https://codex.wordpress.org/Function_Reference/add_image_size">add_image_size()</a></code>, is where we add our new size. This function accepts four arguments: name, width, height and whether to crop the image. WordPress also advises strongly against using certain reserved names (read: <strong>do not use them</strong>): <code>thumb</code>, <code>thumbnail</code>, <code>medium</code>, <code>large</code> and <code>post-thumbnail</code>.

Once our new size is created, we can add it to the post’s loop to display it to users, like so:

<pre><code class="language-php">if ( has_post_thumbnail() ){
  the_post_thumbnail( 'post-header' );
}</code></pre>

This checks to see whether you’ve uploaded an image and made it the post’s featured image. If so, WordPress displays it. You can also get fancy and add a default fallback image.

<pre><code class="language-php">if ( has_post_thumbnail() ){
  the_post_thumbnail( 'post-header' );
}else{
  &lt;img src="'. IMAGES .'/default.jpg" alt="Post Header Image" /&gt;
}</code></pre>

In this case, if the post has no thumbnail, it falls back to the default image. Hooray, continuity!

## Change the Sidebar’s Markup

Registering a sidebar doesn’t take much. All you really need is a name and an ID to make it clear in the admin area:

<pre><code class="language-php">register_sidebar( array (
  'name' =&gt; __( 'Sidebar', 'main-sidebar' ),
  'id' =&gt; 'primary-widget-area'
));</code></pre>

WordPress will apply the default markup for us, which we can style as we want. However, we can also add our own markup and style it as we want. I prefer to use divs for sidebar widgets because they are more semantically correct than list items. I also prefer <code>h3</code> for widget headings because I usually reserve <code>h2</code> for the blog post’s title. So, with that in mind:

<pre><code class="language-php">register_sidebar( array (
  'name' =&gt; __( 'Sidebar', 'main-sidebar' ),
  'id' =&gt; 'primary-widget-area',
  'description' =&gt; __( 'The primary widget area', 'wpbp' ),
  'before_widget' =&gt; '&lt;div class="widget"&gt;',
  'after_widget' =&gt; "&lt;/div&gt;",
  'before_title' =&gt; '&lt;h3 class="widget-title"&gt;',
  'after_title' =&gt; '&lt;/h3&gt;',
) );</code></pre>

This produces a sidebar that looks like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f3d4eb6-45e7-49de-b44e-7f29c086bfc8/sidebar-markup.jpg"><img title="The sidebar with markup. Isn't the Web Developer Toolbar great?" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f3d4eb6-45e7-49de-b44e-7f29c086bfc8/sidebar-markup.jpg" alt="" width="299" height="405" /></a><br>
<em>The sidebar with markup. Isn’t the Web Developer Toolbar great? (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f3d4eb6-45e7-49de-b44e-7f29c086bfc8/sidebar-markup.jpg">View image</a>.)</em>

## Alter The RSS Widget’s Refresh Rate

WordPress’ built-in RSS widget is fantastic, but sometimes it doesn’t update often enough. Luckily, there is a fairly simple solution for that. Just add this code to your <code>functions.php</code> file:

<pre><code class="language-php">add_filter( 'wp_feed_cache_transient_lifetime',
   create_function('$a', 'return 600;') );</code></pre>

As you can see, we are using WordPress’ <code><a href="https://codex.wordpress.org/Function_Reference/add_filter">add_filter()</a></code> function, which accepts a <a href="https://codex.wordpress.org/Plugin_API/Filter_Reference">filter hook</a>, callback function and (optional) priority. The <code>wp_feed_cache_transient_lifetime</code> hook handles the feed’s refresh rates. We’re creating our callback function on the fly using PHP’s <a href="https://us2.php.net/manual/en/function.create-function.php"><code>create_function()</code></a> function. It is one line, which returns the refresh rate in seconds. Our refresh rate is set to 10 minutes.

## Add Content To The RSS Feed

WordPress’ ability to add targeted content to an RSS feed (i.e. content that only your subscribers can see) is especially cool. This could be anything such as ads, a hidden message or value-added content. In the following example, we’ll add a hidden message.

<pre><code class="language-php">function add_to_feed($content){
   $content .= "&lt;p&gt;Thanks for Subscribing! You're the best ever!&lt;/p&gt;";
   return $content;
}

add_filter( "the_content_feed", "add_to_feed" );</code></pre>

Using the filter <code>the_content_feed</code>, which is called only when the feed is created, we use a callback function to append new information to the post’s content. If we looked at our website’s feed in Google Reader, we’d see this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ee42aea-1b65-45ef-9eb8-cf2f1ff36fc6/extra-feed.jpg"><img class="105895" style="border: 1px solid #ddd" title="extra-feed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ee42aea-1b65-45ef-9eb8-cf2f1ff36fc6/extra-feed.jpg" alt="Here's our super-secret message to all subscribers." width="492" height="186" /></a><br>
<em>Here’s our super-secret message to all subscribers. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ee42aea-1b65-45ef-9eb8-cf2f1ff36fc6/extra-feed.jpg">View image</a>.)</em>

## Highlight The Author’s Comments

One fairly common practice is to set off the author’s comments from the comments of readers. I do it on my blog:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7318b301-8385-4fdb-9a59-781c7f4d529f/comments.jpg"><img class="105893" title="comments" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7318b301-8385-4fdb-9a59-781c7f4d529f/comments.jpg" alt="My blog hasn't seen a whole lot of activity lately." width="495" height="439" /></a><br>
<em>My blog hasn’t seen a whole lot of activity lately. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7318b301-8385-4fdb-9a59-781c7f4d529f/comments.jpg">View image</a>.)</em>

So, how do we accomplish this? I’m glad you asked! See, in a pre-2.7 world, some custom coding was required to determine whether the author’s ID matches the commenter’s. On my blog, I just used to check whether the commenter’s ID was 1, which was the ID of the admin. Not very good I know, but I was young and naive (as well as the blog’s only author).

Version 2.7+ has a fancy little function named <code><a href="https://codex.wordpress.org/Template_Tags/wp_list_comments">wp_list_comments</a></code>, which prints a post’s comments for us. Even better, it applies the class <code>.bypostauthor</code> to any comments by — you guessed it — the post’s author. Now, to style the author’s comments differently, all we need to do is this:

<pre><code class="language-css">.comment { /* Reader comments */
   background: #FFFFFF;
   color: #666666;
}

.bypostauthor { /* Author comments */
   background: #880000;
   color: #FFFFFF;
}</code></pre>

Done! Easy, right?

<strong>Tip:</strong> If you don’t like that WordPress tells you what markup to use in the comments section, you can tell it to use your own print function:

<pre><code class="language-php">&lt;ul class="commentlist"&gt;
  &lt;?php wp_list_comments('type=comment&amp;callback=my_comment_display'); ?&gt;
&lt;/ul&gt;</code></pre>

Then, you create a function named <code>my_comment_display()</code>, which prints your comments as you see fit. More information on that <a href="https://codex.wordpress.org/Template_Tags/wp_list_comments#Comments_Only_With_A_Custom_Comment_Display">in the Codex</a>.</p>

## Modify Published Content

Just as we modified the feed’s content earlier, we can do the same thing with our website’s content using the <code>the_content</code> filter. What we’ll do here is append the author’s signature to the end of the content:

<pre><code class="language-php">function sig_to_content($content){
   $content .= '&lt;p&gt;&lt;img src="'. IMAGES .'/sig.png" alt="Joseph L. Casabona" /&gt;&lt;/p&gt;';
   return $content;
}

add_filter( "the_content", "sig_to_content" );</code></pre>

By now you’re getting the hang of the <code>add_filter()</code> and callback functions. In this case, our filter is <code>the_content</code>. This will add a signature to the end of both posts and pages. To filter out pages, we simply add this condition:

<pre><code class="language-php">function sig_to_content($content){
   if(is_single()){
      $content .= '&lt;p&gt;&lt;img src="'. IMAGES .'/sig.png" alt="Joseph L. Casabona" /&gt;&lt;/p&gt;';
      return $content;
   }
}</code></pre>

This function, <code>is_single()</code>, checks to see whether we’re viewing a single post (as opposed to the content’s relationship status).</p>

## Create A Custom Template For A Taxonomy

I started using WordPress way back in 2004, before pages, plugins or rich editing were introduced. Thinking about its evolution into an amazingly flexible platform, I remember doing custom stuff with certain categories and tags using <code>if</code> statements in the <code>single.php</code> template file. It’s much easier now.

WordPress has an incredibly sophisticated <a href="https://codex.wordpress.org/Template_Hierarchy">template hierarchy</a>. Everything falls back to <code>index.php</code>, while templates such as <code>page.php</code> and <code>single.php</code> display various types of content differently. But you could get specific with <code>category.php</code> and even <code>home.php</code>. As you can imagine, <code>home.php</code> would be your home page, and <code>category.php</code> would display relevant posts when the visitor is viewing a category page. What you might not know is that you can get category-specific. By creating a template page named <code>category-[slug].php</code> or <code>category-[id].php</code> (that is, for example, <code>category-news.php</code> or <code>category-6.php</code>), you are telling WordPress, “Use this template specifically for this category.” I usually copy <code>index.php</code> or <code>category.php</code> and modify them.</p>

## Customize The Search Bar

On the same note, you can customize the search bar by creating a template page named <code>searchform.php</code>, which will include <strong>only the search form</strong>. By default (i.e. when there is no <code>searchform.php</code>), here’s what we’re looking at:

<pre><code class="language-php">&lt;form role="search" method="get" id="searchform" action="&lt;?php echo home_url( '/' ); ?&gt;"&gt;
    &lt;div&gt;&lt;label class="screen-reader-text" for="s"&gt;Search for:&lt;/label&gt;
        &lt;input type="text" value="" name="s" id="s" /&gt;
        &lt;input type="submit" id="searchsubmit" value="Search" /&gt;
    &lt;/div&gt;
&lt;/form&gt;</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6972faa7-4154-45ff-b6e3-41266c2d2984/search.jpg"><img class="105898" title="search" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6972faa7-4154-45ff-b6e3-41266c2d2984/search.jpg" alt="The default search bar" width="342" height="46" /></a><br>
<em>The default search bar. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6972faa7-4154-45ff-b6e3-41266c2d2984/search.jpg">View image</a>.)</em>

I like to eliminate the button and label and instruct the user to hit “Enter” to search. We can do that simply by creating a <code>searchform.php</code> template file and adding the code. Here’s the file in its entirety:

<pre><code class="language-php">&lt;!--BEGIN #searchform--&gt;
&lt;form class="searchform" method="get" action="&lt;?php bloginfo( 'url' ); ?&gt;"&gt;
  &lt;input class="search" name="s" onclick="this.value=’" type="text" value="Enter your search" tabindex="1" /&gt;
&lt;!--END #searchform--&gt;
&lt;/form&gt;</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0f47c79-c273-4d49-a6e2-a9a4b8946609/new-search.jpg"><img class="105897" title="new-search" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0f47c79-c273-4d49-a6e2-a9a4b8946609/new-search.jpg" alt="Our new search bar after some CSS magic" width="185" height="53" /></a><br>
<em>Our new search bar after some CSS magic. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0f47c79-c273-4d49-a6e2-a9a4b8946609/new-search.jpg">View image</a>.)</em>

## Customize WordPress’ Log-In Screen

There are several ways to do this, mostly involving plugins. First, let’s look at a way to customize the log-in logo (and logo URL) through our own theme. Customizing the logo’s URL is easy. Just add this code to your <code>functions.php</code> file:

<pre><code class="language-php">add_filter('login_headerurl',
  create_function(false,"return 'https://casabona.org';"));</code></pre>

Much like with the refresh rate for our RSS widget, we are combining <code>add_filter()</code> and <code>create_function()</code> to return a different URL (in this case, my home page) when the <code>login_headerurl</code> hook is called. Changing the logo image is theoretically the same but does require a little extra work:

<pre><code class="language-php">add_action("login_head", "custom_login_logo");

function custom_login_logo() {
  echo "
  &lt;style&gt;
  body.login #login h1 a {
    background: url('".get_bloginfo('template_url')."/images/custom-logo.png') no-repeat scroll center top transparent;
    height: 313px;
    width: 313px;
  }
  &lt;/style&gt;
  ";
}</code></pre>

You can see we have a hook (<code>login_head</code>) and a callback function (<code>custom_login_logo()</code>), but instead of <code>add_filter()</code>, we’re using <code>add_action()</code>. The difference between the two is that, while <code>add_filter()</code> replaces some text or default value, <code>add_action()</code> is meant to execute some code at a particular point while WordPress is loading.

In our callback function, we are overwriting the default CSS for the logo (<code>body.login #login h1 a</code>) with an image that we’ve uploaded to our theme’s directory. Be sure to adjust the height and width as needed. We get something like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d40b2ca-0942-45e7-b67f-80ff6bbb5c33/new-login.png"><img class="105896" title="new-login" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a81faa58-8264-4300-b6ef-9b9bd87a5fbd/new-login-500.jpg" alt="That is one handsome sketch." width="500" height="569" /></a><br>
<em>That is one handsome sketch. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d40b2ca-0942-45e7-b67f-80ff6bbb5c33/new-login.png">View image</a>.)</em>

You could also go the plugin route and find a bunch that will help you modify the log-in page right from the WordPress admin area. I’m familiar with <a href="https://wordpress.org/extend/plugins/custom-login/">Custom Login</a>, but go ahead and <a href="https://wordpress.org/extend/plugins/search.php?q=custom+login">try a few out</a>!

## Bonus: Make A Splash Page Part Of Your Theme

While this isn’t exactly modifying WordPress’ default functionality, a lot of designers add completely separate splash pages, and WordPress makes this easy to do. Follow these steps:

1.  Create a new file in your theme directory named `page-splash.php` (although the name doesn’t matter).
2.  Add your HTML and CSS markup and anything else you might use. The idea here is that the markup, CSS and layout for the splash page will probably be different from the rest of the website.
3.  At the top of `page-splash.php`, add the following, which tells WordPress that this is a page template: `<php /* Template Name: Splash */ ?>`
4.  Add the two tags that will make your page a WordPress-ready page. Somewhere in the head (ideally, close to `</head>`), add `<?php wp_head(); ?>`. Right before the `</body>` tag, add `<?php wp_footer(); ?>`. Save it!
5.  Go into the WordPress admin panel and create a page using that template: [![default template](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d980fcb9-7de8-433b-9c8a-9a4063510c8a/page-temp.png "page-temp")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d980fcb9-7de8-433b-9c8a-9a4063510c8a/page-temp.png)
6.  Once you have saved the page, go to `Settings → Reading`, and under “Front page displays” choose the radio button “A static page.” Make the front page the splash page you created! [![splash screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fab275dd-08ab-4985-8ead-61e9835a469c/splash1.png "splash")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fab275dd-08ab-4985-8ead-61e9835a469c/splash1.png)

## Conclusion

There you have it! Over 10 modifications you can make to WordPress through hooks, functions and template pages, oh my! These are ones I use frequently, but there is a whole host of hooks to do everything from adding body classes to modifying the title before it’s printed. Flexibility and not having to modify the core are what makes WordPress such a great platform! What are your favorite tips? Let us know in the comments.</p>

### Other Resources

Everything we’ve talked about in this article comes from the WordPress Codex. Here are some pages I find particularly helpful:

*   “[Plugin API](https://codex.wordpress.org/Plugin_API)” An in-depth description of actions and filters, as well as a list of hooks.
*   “[Template Tags](https://codex.wordpress.org/Template_Tags/)” Everything you can use in the loop.
*   “[Template Hierarchy](https://codex.wordpress.org/Template_Hierarchy)” How your theme drills down.

{{< signature "al" >}}


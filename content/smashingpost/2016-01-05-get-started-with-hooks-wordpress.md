---
title: 'Useful Tips To Get Started With WordPress Hooks'
slug: get-started-with-hooks-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/537f6ea1-2b75-4ee0-86ab-fd414ae97871/wordpress-hooks-500px-opt.png
date: 2016-01-05T21:24:50.000Z
author: thomasmaier
summary: >-
  Whenever you want to change existing or create new functionality in WordPress theme and development, you will have to turn to hooks. Learning hooks is like studying law: you don’t need to know all of the statements and paragraphs, but simply where to find them. In this article you will find all you need to setup Hook Routines and get ready to have a better experience developing for Wordpress.
description: >-
  With these Wordpress Hooks detailed tips, you can understand code snippets with hooks, extend WordPress, plugins and themes, avoiding common problems and allowing others to easily extend your code.
categories:
  - WordPress
  - Hooks
  - Techniques
---

Even though hooks in WordPress are amazing and everyone uses them knowingly or unknowingly, I get the impression that some advanced users and especially front&ndash;end developers still seem to avoid them. If you feel like you’ve been holding back on hooks, too, then this article will get you started. I am also going to **reveal some interesting details to anyone who thinks they are familiar enough with hooks**.

You’ll want to read this article especially if you’d like to:

- understand code snippets with hooks such as those found in forums;
- extend WordPress, plugins and themes without breaking updates;
- **learn how to avoid common problems**;
- allow others to extend your code.

My examples are taken from WordPress’ core and from my work as a freelance developer and author of the Advanced Ads plugin.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/537f6ea1-2b75-4ee0-86ab-fd414ae97871/wordpress-hooks-500px-opt.png"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/537f6ea1-2b75-4ee0-86ab-fd414ae97871/wordpress-hooks-500px-opt.png" width="500" height="274" alt="Screen showing Hooks in WordPress" /></a><figcaption>Hooks in WordPress are useful and widely used, but not straightforward. But you can extend plugins and themes without breaking them and avoid common maintenance issues along the way.</figcaption></figure>

## What Are Hooks?

Whenever you want to **do something** or **customize something** in WordPress, then there is very likely a hook you can use.

The **“do” hook** is called an “action”. Wherever an action is defined, you can execute your own code. Here are some examples:

- send an email to the author once a post is published;
- load a custom script file in the footer of the page;
- add instructions above the login form.

The most important thing about action hooks is the position. There are action hooks all over WordPress core that allow you to do your thing.

The **“customize” hook** is called a “filter.” A filter allows you to change or customize a value and return it in a new form. Some examples are:

- capitalizing a post’s title,
- attaching links to related posts after the main content,
- changing an option that is retrieved from the database.

Not only is the position important for a filter, but the given and returned values matter, too. As with actions, you can assume that **WordPress has a filter for almost every value it processes**.

## Elements Of A Hook Routine

The hook alone is just a position. Nothing happens here by default. To make it work, you need at least three basic functions, which, combined, I’d like to call a “hook routine.”

Let’s use the `wp_head` hook as an example for actions and `the_content` for filters.

### Hook (Noun)

The hook itself is when and where the magic happens. Imagine this as the kind of hook a climber would put into a mountain face. It has a specific position and if they or other climbers want to move along, they can use it.

Action hooks are placed with `do_action()`, as in the following:

<pre><code class="language-php">
do_action( 'wp_head' );
</code></pre>

Filter hooks use `apply_filters()`, as follows:

<pre><code class="language-php">
$content = apply_filters( 'the_content', $content );
</code></pre>

As you can see, we need to catch the filter’s output, too.

### Action and Filter

The next element in a hook routine is the **action or the filter**. This is at least one function that you define to do or filter something. This would be the actual climber who is ready to use any hook to get a bit higher.

An action that is triggered in `wp_head` is `noindex()`.

<pre><code class="language-php">
function noindex() {
// If the blog is not public, tell robots to go away.
if ( '0' == get_option('blog_public') )
wp_no_robots();
}
</code></pre>

This simply checks whether you have disabled the setting for search engine visibility. If so, `wp_no_robots()` adds the robots meta tag telling search engines not to index your website.

An example of a filter on `the_content` is `wpautop()`. It is responsible for wrapping your paragraphs in `&lt;p&gt;` tags and using `&lt;br /&gt;` for line breaks. The important part of the plugin is this:

<pre><code class="language-php">
function wpautop( $pee, $br = true ) {
// …
return $pee;
}
</code></pre>

Other than an action, a filter function needs at least one argument. This argument is to be returned again later.

{{% feature-panel %}}

### Hook (Verb)

While our real&ndash;life climber knows what they can do with a hook, in a WordPress hook routine **we would need to tell them that this very specific hook is meant for them to use**. This means, we have to hook (verb) our function into the hook (noun).

This is done using a function that is often also incorrectly referred to as a “hook” (noun). When I’m explaining a hook routine, this is expressed as a verb, but if I need to use a noun, then I would call it a “connection.”

For the `wp_head` hook and the `noindex()` action, the connection is made with this line:

<pre><code class="language-php">
add_action( 'wp_head', 'noindex', 1 );
</code></pre>

The third parameter is a priority, which we will be covering below.

Hooking `wpautop()` into `the_content` is done with this line:

<pre><code class="language-php">
add_filter( 'the_content', 'wpautop' );
</code></pre>

These are the basics of a hook routine. We will cover more of them in the following sections.

## You’re Already Using These Hooks

Actions and filter are hidden deep in the core, but you are just interested in changing your theme, so why should you bother with them?

The truth is that, even if you “just” code themes or occasionally put something in your theme’s `functions.php`, you are probably already using actions and filters.

### Wp_head

Let’s look at the `head` section of the Twenty Fifteen theme, which can be found in `wp-content/themes/twentyfifteen/header.php`.

<pre><code class="language-php">
&lt;!DOCTYPE html&gt;
&lt;html &lt;?php language_attributes(); ?&gt; class="no-js"&gt;
&lt;head&gt;
&lt;meta charset="&lt;?php bloginfo( 'charset' ); ?&gt;"&gt;
&lt;meta name="viewport" content="width=device-width"&gt;
&lt;link rel="profile" href="https://gmpg.org/xfn/11"&gt;
&lt;link rel="pingback" href="&lt;?php bloginfo( 'pingback_url' ); ?&gt;"&gt;
&lt;!--[if lt IE 9]&gt;
&lt;script src="&lt;?php echo esc_url( get_template_directory_uri() ); ?&gt;/js/html5.js"&gt;&lt;/script&gt;
&lt;![endif]--&gt;
&lt;?php wp_head(); ?&gt;
&lt;/head&gt;
</code></pre>

There is not really a lot between the starting and closing `&lt;head&gt;` tags, so take a look at the source code in your browser. You will see all kinds of meta elements, including a `&lt;title&gt;` tag.

The elements you might find missing in the `header.php` file are added with the `wp_head()` function. If you have your IDE open (i.e. the software you write code with), and it allows you to jump to the definition of a function, then you should really use that now and check out the contents of `wp_head()`.

<pre><code class="language-php">
/\*\*

- Fire the wp_head action
-
- @since 1.2.0
  \*/
  function wp_head() {
  /\*\*
- Print scripts or data in the head tag on the front end.
-
- @since 1.5.0
  \*/
  do_action( 'wp_head' );
  }
</code></pre>

If you were to remove the comments, then you’d see that the only thing `wp_head()` is doing is placing the `wp_head` hook.

Practically, this means that your theme could also just use `do_action( 'wp_head' );`, instead of `wp_head();`.

This hook is used by the core already. Here are some connections that WordPress defines by default:

<pre><code class="language-php">
add_action( 'wp_head','\_wp_render_title_tag', 1);
add_action( 'wp_head','wp_enqueue_scripts', 1);
add_action( 'wp_head','feed_links', 2);
add_action( 'wp_head','feed_links_extra', 3);
add_action( 'wp_head','rsd_link');
add_action( 'wp_head','wlwmanifest_link');
add_action( 'wp_head','adjacent_posts_rel_link_wp_head', 10, 0 );
add_action( 'wp_head','locale_stylesheet');
add_action( 'wp_head','noindex', 1);
add_action( 'wp_head','print_emoji_detection_script', 7);
add_action( 'wp_head','wp_print_styles', 8);
add_action( 'wp_head','wp_print_head_scripts', 9);
add_action( 'wp_head','wp_generator');
add_action( 'wp_head','rel_canonical');
add_action( 'wp_head','wp_shortlink_wp_head', 10, 0 );
add_action( 'wp_head','wp_site_icon', 99);
</code></pre>

Among them is our `noindex()` action, as well as (since WordPress 4.1) the call to `\_wp_render_title_tag()`, which generates the `title` tag.

### The_content

An example of a filter hook that you’ve used multiple times without knowing it is `the_content`.

It is hidden behind the `the_content()` function, which is used to output the contents of a post or page. It also contains the call to the `the_content` hook.

<pre><code class="language-php">
function the_content( $more_link_text = null, $strip_teaser = false) {
$content = get_the_content( $more_link_text, $strip_teaser );

// …
$content = apply_filters( 'the_content', $content );
$content = str_replace( ']]&gt;', ']]&amp;gt;', $content );
echo $content;
}
</code></pre>

When calling `the_content()` in a clean WordPress installation, a few filters are already hooked to `the_content`.

<pre><code class="language-php">
add_filter( 'the_content', 'wptexturize' );
add_filter( 'the_content', 'convert_smilies' );
add_filter( 'the_content', 'convert_chars' );
add_filter( 'the_content', 'wpautop' );
add_filter( 'the_content', 'shortcode_unautop' );
add_filter( 'the_content', 'prepend_attachment' );
</code></pre>

The default filters take care of the format and some special signs in your text. It is also widely used by many plugins to attach elements such as social&ndash;sharing icons or related posts to the end of a post’s main content.

### Lessons From Using the_content

Even if you do not knowingly use this hook, it is good to learn a bit about it in order to understand common issues. Here are two stories in which incorrect usage prevents features from working properly.

As you can see in `the_content()`, there is also a call to `get_the_content()`. I have seen the latter used instead of the former in a couple of themes. This, however, bypasses the hook, and many features, including the post’s default formatting, would not work.

If you hook into `the_content`, then also be aware that it **is used not only on content pages, but also on list pages**, such as the archive and home page. I still remember a client contacting me about his front page, which was slow due to a popular plugin that injected a social&ndash;sharing widget below each post’s teaser, each of which called back home simultaneously. There was no “off” switch for such behavior.

## Parameters In A Hook Routine

The most common parameters you’ll need to know about when building or debugging a hook routine are the name of the hook, the name of the function, the priority and the arguments you give to the function.

Needless to say, the devil is in the details.

For your reference, this is what a basic call to `add_filter()` looks like, including all parameters:

<pre><code class="language-php">
add_filter( $tag, $function, $priority, $accepted_args );
</code></pre>

### Naming Hooks ($tag)

You cannot do anything about the name of a hook that is used in WordPress’ core or in plugins or themes, but keep in mind a few things when creating your own names.

A rule of thumb I follow is that **actions should contain the moment of their call, and filters should contain the moment and value** that is going to be changed.

`wp_head` and `wp_footer` are good examples of actions called according to a position. It is also common to use a prefix or suffix such as `before`, `pre`, `begin` and `after` and `end`.

The function `wp_delete_post()`, which is obviously responsible for deleting a post, includes the following hooks:

- `before_delete_post`
- `delete_post`
- `deleted_post`
- `after_delete_post`

When I write a filter, I try to include the filtered value, too. `the_content` serves as a good example of this.

### Hook Name Prefix

Besides the position and the value, you should give your hook a prefix that identifies it as your own. Follow these examples:

- `wpseo_` from Yoast SEO,
- `genesis_` from the Genesis framework,
- `advanced_ads_` from my Advanced Ads plugin.

This serves two purposes.

First, it prevent conflicts with hooks in other plugins or themes.

Secondly, if someone uses your hook in a theme or plugin, then third parties will more easily understand where exactly the hook originates.

### Dynamic Hook Names

Imagine you have a lot of options in your plugin and you want others to be able to use a filter on each of them. You could either call `apply_filters()` for every option or use the idea of a dynamic hook name, as WordPress core does in the `get_options()` function.

It contains the following hooks:

- `'pre_option_' . $option`
- `'default_option_' . $option`
- `'option_' . $option`

Knowing this, you could hook into `option_blogname` or `option_blogdescription` to change the name or description of the blog dynamically.

This might also be a reason why you can’t find a hook you’ve read about in the source code without shortening the dynamic part.

### The Magical “all”

The special `all` tag can be used as a hook name when calling `add_action()` and `add_filter()`. It will cause the hooked function to be used for every hook (both actions and filters).

The only time I have ever needed this is when debugging a hook’s whole environment.

### Function Names

When calling a plain function, add a prefix. This will prevent conflicts with other function helpers that identify it.

In forums, you will often find function names starting with `my\_`. Change that to something that can later be identified as yours.

<pre><code class="language-php">
add_filter( 'the_content', 'bestpluginever_capitalize_all_words' );
</code></pre>

Hooking a static function in a class is possible, too:

<pre><code class="language-php">
add_filter( 'the_content', array( 'bestpluginever', 'capitalize_all_words' ) );
</code></pre>

Calling it in an instance of this class would be as follows:

<pre><code class="language-php">
add_filter( 'the_content', array( $bestpluginever, 'capitalize_all_words' ) );
</code></pre>

You can also call a method in the instance of the same class, like so:

<pre><code class="language-php">
add_filter( 'the_content', array( $this, 'capitalize_all_words' ) );
</code></pre>

Make sure that the functions are public as well.

{{% ad-panel-leaderboard %}}

### Use Default PHP Functions, Too

Sometimes, creating your own function is not needed.

This hook routine capitalizes the first letter of each word in the post’s title:

The default filters take care of the format and some special signs in your text. It is also widely used by many plugins to attach elements such as social&ndash;sharing icons or related posts to the end of a post’s main content.

### Lessons From Using the_content

Even if you do not knowingly use this hook, it is good to learn a bit about it in order to understand common issues. Here are two stories in which incorrect usage prevents features from working properly.

As you can see in `the_content()`, there is also a call to `get_the_content()`. I have seen the latter used instead of the former in a couple of themes. This, however, bypasses the hook, and many features, including the post’s default formatting, would not work.

If you hook into `the_content`, then also be aware that it **is used not only on content pages, but also on list pages**, such as the archive and home page. I still remember a client contacting me about his front page, which was slow due to a popular plugin that injected a social&ndash;sharing widget below each post’s teaser, each of which called back home simultaneously. There was no “off” switch for such behavior.

## Parameters In A Hook Routine

The most common parameters you’ll need to know about when building or debugging a hook routine are the name of the hook, the name of the function, the priority and the arguments you give to the function.

Needless to say, the devil is in the details.

For your reference, this is what a basic call to `add_filter()` looks like, including all parameters:

<pre><code class="language-php">
add_filter( $tag, $function, $priority, $accepted_args );
</code></pre>

### Naming Hooks ($tag)

You cannot do anything about the name of a hook that is used in WordPress’ core or in plugins or themes, but keep in mind a few things when creating your own names.

A rule of thumb I follow is that **actions should contain the moment of their call, and filters should contain the moment and value** that is going to be changed.

`wp_head` and `wp_footer` are good examples of actions called according to a position. It is also common to use a prefix or suffix such as `before`, `pre`, `begin` and `after` and `end`.

The function `wp_delete_post()`, which is obviously responsible for deleting a post, includes the following hooks:

- `before_delete_post`
- `delete_post`
- `deleted_post`
- `after_delete_post`

When I write a filter, I try to include the filtered value, too. `the_content` serves as a good example of this.

### Hook Name Prefix

Besides the position and the value, you should give your hook a prefix that identifies it as your own. Follow these examples:

- `wpseo_` from Yoast SEO,
- `genesis_` from the Genesis framework,
- `advanced_ads_` from my Advanced Ads plugin.

This serves two purposes.

First, it prevent conflicts with hooks in other plugins or themes.

Secondly, if someone uses your hook in a theme or plugin, then third parties will more easily understand where exactly the hook originates.

### Dynamic Hook Names

Imagine you have a lot of options in your plugin and you want others to be able to use a filter on each of them. You could either call `apply_filters()` for every option or use the idea of a dynamic hook name, as WordPress core does in the `get_options()` function.

It contains the following hooks:

- `'pre_option_' . $option`
- `'default_option_' . $option`
- `'option_' . $option`

Knowing this, you could hook into `option_blogname` or `option_blogdescription` to change the name or description of the blog dynamically.

This might also be a reason why you can’t find a hook you’ve read about in the source code without shortening the dynamic part.

### The Magical “all”

The special `all` tag can be used as a hook name when calling `add_action()` and `add_filter()`. It will cause the hooked function to be used for every hook (both actions and filters).

The only time I have ever needed this is when debugging a hook’s whole environment.

### Function Names

When calling a plain function, add a prefix. This will prevent conflicts with other function helpers that identify it.

In forums, you will often find function names starting with `my\_`. Change that to something that can later be identified as yours.

<pre><code class="language-php">
add_filter( 'the_content', 'bestpluginever_capitalize_all_words' );
</code></pre>

Hooking a static function in a class is possible, too:

<pre><code class="language-php">
add_filter( 'the_content', array( 'bestpluginever', 'capitalize_all_words' ) );
</code></pre>

Calling it in an instance of this class would be as follows:

<pre><code class="language-php">
add_filter( 'the_content', array( $bestpluginever, 'capitalize_all_words' ) );
</code></pre>

You can also call a method in the instance of the same class, like so:

<pre><code class="language-php">
add_filter( 'the_content', array( $this, 'capitalize_all_words' ) );
</code></pre>

Make sure that the functions are public as well.

### Use Default PHP Functions, Too

Sometimes, creating your own function is not needed.

This hook routine capitalizes the first letter of each word in the post’s title:

<pre><code class="language-php">
function bestpluginever_capitalize_title( $title ){
return ucwords( $title );
}
add_filter( 'the_title', 'bestpluginever_capitalize_title' );
</code></pre>

Because `ucwords()` is a normal PHP function that receives and returns a value like any other filter function, you can also shorten the four lines to this:

<pre><code class="language-php">
add_filter( 'the_title', 'ucwords' );
</code></pre>

### Priority

The third parameter in `add_action()` and `add_filter()` is the priority. It sets the order in which multiple hooked functions are called.

This parameter is optional and will default to `10` if undefined. Multiple functions with the same priority will be called in the order in which they were registered to the hook.

The priority parameter has cost me a lot of nerves. Advanced Ads uses `the_content` when injecting ads before or after the content. As I mentioned, a lot of other plugins do the same to insert content such as recent or similar posts.

The parameter determines whether the ad or the other content is attached first. To cut down on support requests about the “wrong” order of elements, which has in fact a very specific definition, I ended up letting the user select the priority of the filter as an option.

### Making Sure That An Action Has Already Happened

To check whether a specific action has already run through, you can use `did_action()`.

You might remember that `\_wp_render_title_tag` was hooked into `wp_head`. This is an example on how core makes sure that the `title` tag is really only created there.

<pre><code class="language-php">
function \_wp_render_title_tag() {
if ( ! current_theme_supports( 'title-tag' ) ) {
return;
}

// This can only work internally on wp_head.
if ( ! did_action( 'wp_head' ) &amp;&amp; ! doing_action( 'wp_head' ) ) {
return;
}

echo '&lt;title&gt;' . wp_title( '|', false, 'right' ) . "&lt;/title&gt;\n";
}
</code></pre>

`did_action( $hook )` returns the number of times an action has fired, including the current call. It would return `1` if `\_wp_render_title_tag()` is currently being triggered in `wp_head`. `doing_action( 'wp_head' )` makes sure that we are in the `wp_head` action right now. Practically, the code above is a double-check, which might also be the reason why it will be removed in WordPress 4.4.0.

`doing_action()` only checks whether an action is currently happening, but the logic behind it is a topic for a whole other article.

{{% ad-panel-leaderboard %}}

### Check Whether a Filter Was Already Used

There is no alias for `did_action()` and `doing_action()` for filters.

You’ll need to make use of `has_filter( $hook, $function )` instead. If only `$hook` is specified, then it will return `true` if any function is registered for the hook, or `false` if not.

If `$function`is given, it will return the priority of this function, or `false` if that function is not hooked into the hook.

When injecting ads after a particular paragraph, my Advanced Ads plugin needs to make sure that `wpautop()` is called before my own filter function is applied.

<pre><code class="language-php">
$wpautop_priority = has_filter( 'the_content', 'wpautop');
if ( $wpautop_priority &amp;&amp; $advads_content_injection_priority() &lt; $wpautop_priority ) {
$content = wpautop( $content );
}
</code></pre>

In this snippet, I check whether the priority of `wpautop()` is higher than the ad injection’s priority. This would mean that the paragraphs are not set yet, and it forces the plugin to create them first.

## Arguments

While filter hooks need at least one argument (the value that is filtered), actions don’t need any. However, this doesn’t mean that both can’t have more.

Let’s look at the `delete_term` hook, which is fired after a term is deleted from the database.

<pre><code class="language-php">
do_action( 'delete_term', $term, $tt_id, $taxonomy, $deleted_term );
</code></pre>

When using the `add_action()` or `add_filter()` function, the fourth parameter is the number of arguments that your action or filter function is expecting.

In our case, a hooked function can make use of these four arguments, but it doesn’t have to, as you can see from this connection made in core:

<pre><code class="language-php">
add_action( 'delete_term', '\_wp_delete_tax_menu_item', 10, 3 );
</code></pre>

The action is only interested in the first three arguments and not in `$deleted_term`.

<pre><code class="language-php">
function \_wp_delete_tax_menu_item( $object_id = 0, $tt_id, $taxonomy ) {
// …
}
</code></pre>

### The Number-of-Arguments Trap

The stated number of arguments has to match the arguments that the function uses, but it can be left out if it is empty or `1`.

I constantly run into the same problem with this argument, because it is not completely optional. If your function needs more arguments, then you’ll have to set them, or else you will get an error message. If you do set them, then you also need to set the priority, which is, in many cases, actually optional.

### Start With Return

Another tip I want to give you concerns filter functions. If you write complex filters with many conditions, then it might happen that you forget to return a value, which would practically remove it. It has happened more than once in development that my post’s content was empty, until I figured out the reason.

For a while now, I have been starting my filters with the `return $value` statement at the end, which has reduced problems like this to a minimum.

## Removing Actions And Filters

Removing an action or a filter from a hook is not uncommon. A popular example was the removal of emojis from WordPress 4.2.

The whole [Disable Emojis](https://wordpress.org/plugins/disable-emojis/) plugin can be boiled down to this code:

<pre><code class="language-php">
function disable_emojis() {
remove_action( 'wp_head', 'print_emoji_detection_script', 7 );
remove_action( 'admin_print_scripts', 'print_emoji_detection_script' );
remove_action( 'wp_print_styles', 'print_emoji_styles' );
remove_action( 'admin_print_styles', 'print_emoji_styles' );
remove_filter( 'the_content_feed', 'wp_staticize_emoji' );
remove_filter( 'comment_text_rss', 'wp_staticize_emoji' );
remove_filter( 'wp_mail', 'wp_staticize_emoji_for_email' );
}
add_action( 'init', 'disable_emojis' );
</code></pre>

And there are also plugins that disable the `wpautop()` function, which could be just one line in your theme’s `functions.php`.

<pre><code class="language-php">
remove_filter( 'the_content', 'wpautop' );
</code></pre>

As you might have guessed from these examples, `remove_action()` and `remove_filter()` accept three arguments:

- hook,
- function,
- priority.

They all need to match the values from `add_action()` and `add_filter()`. The tricky part here is that the connection will only be removed if it has already been added.

## How To Find Hooks?

It might be scary to think of the 1957(!) hooks that WordPress currently has, according to [Adam Brown’s hook database](https://adambrown.info/p/wp_hooks), but you don’t have to learn them. You only need to know that, whatever you’d like to change or add, there is probably a hook for it.

To get started, you could just explore the functions that you already use in your existing code, like I did above with `wp_head()` and `the_content()`.

Another resource is the page for the [plugin API](https://codex.wordpress.org/Plugin_API), which lists the important functions and their details.

## Debugging Hooks

To extensively debug hooks, you could create a list of all hooked actions and filters, as [shown by Jean&ndash;Baptiste Jung](/2009/08/10-useful-wordpress-hook-hacks/#10-list-all-hooked-functions).

### Using error_log()

For debugging filters especially in live environments, I like to use `error_log()` in combination with [DEBUG_LOG](https://codex.wordpress.org/Debugging_in_WordPress) turned on. This will write my output to a `debug.log` file but not display it in the front end.

<pre><code class="language-php">
function example_content_filter( $content ){
$option = get_option( 'add_haha' );

error_log( $option );

if( $option === true ){
$content .= 'HAHA&lt;br/&gt;' . $content;
}
return $content;
}
add_filter( 'the_content', 'example_content_filter' );
</code></pre>

In the scenario above, I’ve prepended the string `HAHA` to the content, but only if my option returns `true`. If this doesn’t work for some reason, I can use `error_log( $option );` to debug the option’s value, writing it to the log to check out later, without breaking the content that is visible to visitors in the front end.

### Using the Hook API

Another way to debug hooks is by using one of the functions mentioned above, like `doing_action()` or `did_action()`.

One is missing from that list: `current_filter()` (or `current_action()`). You can use it to display the name of the current hook, as in this example taken from the Codex:

<pre><code class="language-php">
function my_filter() {
echo current_filter(); // 'the_content'
}
add_filter( 'the_content', 'my_filter' );
</code></pre>

If you want to see somewhere that core uses this, then check out [capital_P_dangit()](https://core.trac.wordpress.org/browser/trunk/src/wp-includes/formatting.php#L4304). I’ll bet that most of you didn’t know such a filter exists.

### Using a Plugin

There are also countless plugins for debugging out there, allowing you to see a list of all hooks and hooked functions in the front end. I’ve personally settled on [Debug Objects](https://wordpress.org/plugins/debug-objects/).

## Get Started

Learning hooks is like studying law: You don’t need to know all of the statements and paragraphs, just where to find them. You will also never need all of them, but I hope you now understand the solutions posted in forums a bit better. Or you can get started by taking a closer look at any function that you are already using.

Let me know in the comments about your “hook” experience.

### Further Reading on Smashing Magazine

- “[Extending WordPress With Custom Content Types](https://www.smashingmagazine.com/2015/04/extending-wordpress-custom-content-types/),” Brian Onorio
- “[A Detailed Guide To WordPress Custom Page Templates](https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/),” Nick Schäferhoff
- “[Customizing WordPress Archives For Categories, Tags](https://www.smashingmagazine.com/2014/08/customizing-wordpress-archives-categories-terms-taxonomies/),” Josh Pollock
- “[Building A Custom Archive Page For WordPress](https://www.smashingmagazine.com/2015/04/building-custom-wordpress-archive-page/),” Karol K

{{< signature "dp, jb, ml, al, nl" >}}

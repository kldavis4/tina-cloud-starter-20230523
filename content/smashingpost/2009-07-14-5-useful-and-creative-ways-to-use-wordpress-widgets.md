---
title: 5 Useful And Creative Ways To Use WordPress Widgets
slug: 5-useful-and-creative-ways-to-use-wordpress-widgets
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30bbc75e-d2f7-4fb0-8b21-63a12d58a298/illusearch7.jpg
date: 2009-07-14T22:12:31.000Z
author: leland
description: >-
  If you've been reading some of the previous WordPress-related articles here on
  Smashing Magazine, you'll know that WordPress is much more than a blogging
  platform. It can be used as a CMS, too. And WordPress widgets are a powerful
  tool in your **WordPress development arsenal**.

  When you think of **WordPress widgets**, you may think they're just a way to
  rearrange various items in your blog's sidebar without touching any code.
  Sure, that's nice and all, but that's really just the tip of the iceberg of
  all the things WordPress widgets can do.
categories:
  - WordPress
  - Techniques
  - Widgets
---
If you've been reading some of the previous WordPress-related articles here on Smashing Magazine, you'll know that WordPress is much more than a blogging platform. It can be used as a CMS, too. And WordPress widgets are a powerful tool in your <strong>WordPress development arsenal</strong>.

When you think of <strong>WordPress widgets</strong>, you may think they're just a way to rearrange various items in your blog's sidebar without touching any code. Sure, that's nice and all, but that's really just the tip of the iceberg of all the things WordPress widgets can do.

You may be interested in the following related posts:

*   [Power Tips For WordPress Template Developers](https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/)
*   [10 Useful WordPress Loop Hacks](https://www.smashingmagazine.com/2009/06/10/10-useful-wordpress-loop-hacks/)
*   [Custom Field Hacks For WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/)
*   [15 Useful Twitter Hacks and Plugins For WordPress](https://www.smashingmagazine.com/2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [Mastering WordPress Shortcuts](https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/)
*   [100 Amazing Free WordPress Themes For 2009](https://www.smashingmagazine.com/2009/05/18/100-amazing-free-wordpress-themes-for-2009/)

## 1\. Multiple Widget-Ready Areas

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/wordpress-widgets/2(1).jpg" alt="Screenshot" width="357" height="250" />

{{% feature-panel %}}

A widgetized theme has come to be expected by theme users and developers alike. Nowadays, however, just one widgetized area doesn't cut it. The first step to using widgets on your WordPress website is to <strong>widgetize your theme</strong>, and that's really not that hard if you have the right code in place.</p>

### Register the Widget Areas

To have multiple widget-ready areas, the first thing to do is register the widget areas in the <em>functions.php</em> file of your WordPress theme. Let's say you have a three-column theme, and you want to have two different sidebars on the left and right side:

<pre><code class="language-php">&lt;?php
  register_sidebar( array(
    'name' =&gt; 'left-sidebar',
    'id' =&gt; 'left-sidebar',
    'before_widget' =&gt; '&lt;div id="%1$s" class="%2$s widget"&gt;',
    'after_widget' =&gt; '&lt;/div&gt;',
    'before_title' =&gt; '&lt;h3 class="widget-title"&gt;',
    'after_title' =&gt; '&lt;/h3&gt;'
  ) );
  register_sidebar( array(
    'name' =&gt; 'right-sidebar',
    'id' =&gt; 'right-sidebar',
    'before_widget' =&gt; '&lt;div id="%1$s" class="%2$s widget"&gt;',
    'after_widget' =&gt; '&lt;/div&gt;',
    'before_title' =&gt; '&lt;h3 class="widget-title"&gt;',
    'after_title' =&gt; '&lt;/h3&gt;'
  ) );
?&gt;</code></pre>

### Activate the Widget Areas

The next step is to put the dynamic sidebar code in the actual sidebar files. Depending on your theme, this could be located in a <em>sidebar.php</em> file, or elsewhere.  Here's the code to use:

<pre><code class="language-php">&lt;?php if (!dynamic_sidebar("left-sidebar") ) : ?&gt;
Default left sidebar stuff here…
&lt;?php endif; ?&gt;</code></pre>

<pre><code class="language-php">&lt;?php if (!dynamic_sidebar("right-sidebar") ) : ?&gt;
Default right sidebar stuff here…
&lt;?php endif; ?&gt;</code></pre>

The code between the PHP tags will be displayed if no widgets are currently used in the relevant widget area. For example, if no widgets are used in the "left-sidebar" widget, then "Default left sidebar stuff here…" would be displayed instead.

<strong>Sources:</strong>

*   [See How Easy It Is To Widgetize WordPress Themes](https://www.themelab.com/2008/04/18/see-how-easy-it-is-to-widgetize-wordpress-themes/)
*   [Widgetizing WordPress Themes](https://automattic.com/code/widgets/themes/) (Automattic)

## 2\. Widget Logic

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7666448e-b0a5-4888-a7ba-394cd12a1e5c/cal.jpg" alt="Screenshot" width="357" height="250" />

Sometimes you may not want the same widgets to appear the same way on every single page of your blog.  This is where the <a href="https://wordpress.org/extend/plugins/widget-logic/">Widget Logic</a> plug-in comes in handy.

After the plug-in is installed, a new "Widget Logic" input box is displayed in the options box of every widget you use.  In this box, you can type a series of <strong>WordPress conditional tags</strong> to control where exactly the widget is displayed.

In the screenshot above, the Calendar widget is set to display only on the page called "Evil." You can use many more conditional tags as well.</p>

### Examples

*   Display only on the home page: `is_home()`
*   Display only on individual posts: `is_single()`
*   Display only on pages: `is_page()`
*   Display on archive pages (category, tag, etc.): `is_archive()`
*   Display on search results pages: `is_search()`
*   Display on all pages _except_ the home page: `!is_home()`
*   Display on "Advertise" or "Contact" page: `is_page('advertise') || is_page('contact')`

Simply type something similar in your own Widget Logic boxes, depending on where you want the widgets to display.

<strong>Sources:</strong>

*   [The Ultimate Guide to WordPress Conditional Tags](https://www.themelab.com/2008/04/14/the-ultimate-guide-to-wordpress-conditional-tags/)
*   [WordPress Conditional Tags](https://codex.wordpress.org/Conditional_Tags) (WordPress Codex)

## 3\. Query Posts

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dc88d84-d83d-4cf5-a8b0-6886fe644fb8/que.jpg" alt="Screenshot" width="357" height="250" />

For those who don't know, the <code><strong>query_posts</strong></code> template tag is a powerful WordPress function that you can use to control how different posts and pages show up in the loop.

However, if you'd rather not mess around with more PHP code than is necessary but still want to take advantage of the <code>query_posts</code> tag, you can use the <a href="https://wordpress.org/extend/plugins/query-posts/">Query Posts</a> widget to display WordPress content in almost any way you can think of.

After installing and activating the plug-in, you will have a new "Query Posts" widget available in the WordPress widgets menu.</p>

### What It Can Do

*   Display posts by tag, category, author, time/date or custom field keys/values,
*   Display however many number of posts you want,
*   Order posts by date published, title or ID in either ascending or descending order,
*   Display posts with full content, as excerpts or in a list,
*   Show WordPress pages.

<strong>Source:</strong>

*   [Query Posts Widget: WordPress Plug-In](https://justintadlock.com/archives/2009/03/15/query-posts-widget-wordpress-plugin)

## 4\. 404 Templates

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/wordpress-widgets/2_2(1).jpg" alt="Screenshot" width="357" height="250" />

A lot of WordPress themes out there, including the default WordPress theme, don't offer anything useful in their 404 templates. For example, if you land on a 404 page of a WordPress website that uses the default theme, you'll be greeted with a message that says "Error 404 - Not Found," and that's it.

There are plenty of WordPress widgets you can use to spice up your 404 page and make it more useful to visitors who are trying to find content. The widgets "Recent Posts," "Categories" and "Archives" come to mind.</p>

### The Code

The first step is to register the widget area in WordPress. To do this, open up your theme's <em>functions.php</em> file, and put the following code in it:

<pre><code class="language-php">&lt;?php
  register_sidebar( array(
    'name' =&gt; '404',
    'id' =&gt; '404',
    'before_widget' =&gt; '&lt;div id="%1$s" class="%2$s widget"&gt;',
    'after_widget' =&gt; '&lt;/div&gt;',
    'before_title' =&gt; '&lt;h3 class="widget-title"&gt;',
    'after_title' =&gt; '&lt;/h3&gt;'
  ) );
?&gt;</code></pre>

Now that the widget is registered, you'll have to edit your theme's <em>404.php</em> file and add the following code:

<pre><code class="language-php">&lt;?php dynamic_sidebar( '404' ); ?&gt;</code></pre>

That's it. You can now place any widgets you'd like in your "404" widget, and they will be displayed every time a visitor lands on a 404 page. Load it up with things like a search box, recent posts, category listings or maybe a few Query Post lists.

<strong>Source:</strong>

*   [Customize your 404 page from the WordPress Admin](https://justintadlock.com/archives/2009/05/13/customize-your-404-page-from-the-wordpress-admin)

## 5\. Insert Ads Between Posts

<img loading="lazy" decoding="async" src="https://www.smashingmagazine.com/images/wordpress-widgets/3(2).jpg" alt="Screenshot" width="357" height="250" />

You can code your theme to insert a widget in between a certain number of posts. Some people use this to insert advertising, but the sky is the limit when it comes to widgets.</p>

### The Code

As we did when widgetizing the 404 template, the first step to setting this up is to register the widget area for the index insert. Open up your <em>functions.php</em> file again and insert this similar code:

<pre><code class="language-php">&lt;?php
  register_sidebar( array(
    'name' =&gt; 'index-insert',
    'id' =&gt; 'index-insert',
    'before_widget' =&gt; '&lt;div id="%1$s" class="%2$s widget"&gt;',
    'after_widget' =&gt; '&lt;/div&gt;',
    'before_title' =&gt; '&lt;h3 class="widget-title"&gt;',
    'after_title' =&gt; '&lt;/h3&gt;'
  ) );
?&gt;</code></pre>

To set it up on your main index page, you'll need to open up the <em>index.php</em> file of your theme, locate the "endwhile" near the end and put the following code directly above it, so that it looks like this.

<pre><code class="language-php">&lt;?php if ($count==2) { ?&gt;
&lt;?php dynamic_sidebar('index-insert') ?&gt;
&lt;?php } ?&gt;
&lt;?php $count = $count + 1; ?&gt;
&lt;?php endwhile; ?&gt;</code></pre>

The above code will insert the "index-insert" widget area right after the second post. You can change the <code>$count==2</code> number to something else, according to the post you'd like the widget area to be displayed after.

If you want ads to show up in between your archive listings, such as on category or tag pages, you may have to insert the above code in other files, including <em>archive.php</em>, <em>category.php</em> and <em>tag.php</em>. You can even control which ads are displayed on which pages by using conditional tags, such as <code>is_archive()</code>, <code>is_category()</code> and <code>is_tag()</code>, in the Widget Logic plug-in.

<strong>Source:</strong>

*   [Thematic WordPress Theme](https://themeshaper.com/thematic/)

## More Widget Resources

*   [Add a Widgetized Footer to Your WordPress Theme](https://www.themelab.com/2009/04/25/add-a-widgetized-footer-to-your-wordpress-theme/) A tutorial that teaches you how to code your own widgetized footer, including the HTML, CSS and WordPress code needed.
*   [List of WordPress Widgets](https://codex.wordpress.org/Plugins/WordPress_Widgets) A list of WordPress widgets from the Codex, as well as several other widget-related resources.</p>

## Related posts

You may be interested in the following related posts:

*   [Power Tips For WordPress Template Developers](https://www.smashingmagazine.com/2009/07/02/power-tips-for-wordpress-template-developers/)
*   [10 Useful WordPress Loop Hacks](https://www.smashingmagazine.com/2009/06/10/10-useful-wordpress-loop-hacks/)
*   [Custom Field Hacks For WordPress](https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/)
*   [15 Useful Twitter Hacks and Plugins For WordPress](https://www.smashingmagazine.com/2009/03/04/15-useful-twitter-plugins-and-hacks-for-wordpress/)
*   [Mastering WordPress Shortcuts](https://www.smashingmagazine.com/2009/02/02/mastering-wordpress-shortcodes/)
*   [100 Amazing Free WordPress Themes For 2009](https://www.smashingmagazine.com/2009/05/18/100-amazing-free-wordpress-themes-for-2009/)

{{< signature "al" >}}


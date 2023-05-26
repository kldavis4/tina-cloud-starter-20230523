---
title: How To Build A Custom WordPress Archive Page
slug: building-custom-wordpress-archive-page
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69efe617-9ccd-4748-979b-511d260de0cf/archivepage-excerpt.jpg
date: 2015-04-16T21:04:36.000Z
author: karol
description: >-
  If I were to ask you what the least used default page type in WordPress is, chances are you’d say the archive template. Or, more likely, you’d probably not even think of the archive template at all — that’s how unpopular it is. The reason is simple. As great as WordPress is, the standard way in which it approaches the archive is far from user-friendly.
categories:
  - WordPress
  - Themes
  - Techniques (WP)
---
If I were to ask you what the least used default page type in WordPress is, chances are you’d say the archive template. Or, more likely, you’d probably not even think of the archive template at all — that’s how unpopular it is. The reason is simple. As great as WordPress is, the standard way in which it approaches the archive is far from user-friendly.

Let’s fix that today! Let’s build an archive page for WordPress that’s actually useful. The best part is that you will be able to use it with any modern WordPress theme installed on your website at the moment.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Create And Customize A WordPress Child Theme](https://www.smashingmagazine.com/2016/01/create-customize-wordpress-child-theme/)
*   [A Detailed Guide To WordPress Custom Page Templates](https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/)
*   [Customizing WordPress Archives For Categories, Tags And Other](https://www.smashingmagazine.com/2014/08/customizing-wordpress-archives-categories-terms-taxonomies/)
*   [Responsive Images In WordPress With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)

But first, what do we mean by “archive page” exactly?

{{% feature-panel %}}

## The Story Of WordPress Archives

In WordPress, you get to work with a range of different page templates and structures in the standard configuration. Looking at the directory listing of the default theme at the time of writing, Twenty Fifteen, we find the following:

*   404 error page,
*   archive page (our hero today),
*   image attachments page,
*   index page (the main page),
*   default page template (for pages),
*   search results page,
*   single post and attachment pages.

Despite their different purposes, all of these pages are really similar in structure, and they usually only differ in a couple of places and several lines of code. In fact, the only visible difference between the index page and the archive page is the additional header at the top, which changes according to the particular page being viewed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14bc31b4-fa88-4b28-8da4-5661a9fc531e/arch-scr-large-preview-opt.png"><img loading="lazy" decoding="async" title="Standard archive page" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67e2ca98-36e4-438a-9857-0965a4eda8c3/arch-scr-preview-opt.png" alt="wordpress archive page" width="500" height="84" /></a><figcaption>Standard archive page in Twenty Fifteen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14bc31b4-fa88-4b28-8da4-5661a9fc531e/arch-scr-large-preview-opt.png">View large version</a>)</figcaption></figure>

The idea behind such an archive structure is to provide the blog administrator with a way to showcase the archive based on various criteria, but to do so in a simplified form. At the end of the day, these various archive pages are just versions of the index page that filter content published during a specific time period or by a particular author or with particular categories or tags.

While this sounds like a good idea from a programmer’s perspective, it doesn’t make much sense from the user’s point of view. Or, more accurately, one layer is missing here — a layer that would come between the user’s intent to find content and the individual items in the archive themselves.

Here’s what I mean. Right now, the only built-in way to showcase the archive links on a WordPress website is with a widget. So, if you want to allow visitors to dig into the archive in any clear way, you’d probably have to devote a whole sidebar just to the archive (just to be able to capture different types of organization, such as a date-based archive, a category archive, a tag archive, an author archive and so on).

So, what we really need here is a <strong>middleman</strong>, a page that welcomes the visitor, explains that they’re in the archive and then points them to the exact piece of content they are interested in or suggests some popular content.

That is why we’re going to create a custom archive page.</p>

## How To Build A Custom Archives Page In WordPress

Here’s what we’re going to do in a nutshell. Our custom archive page will be based on a <a href="https://codex.wordpress.org/Page_Templates">custom page template</a>. This template will allow us to do the following:

*   include a custom welcome message (may contain text, images, an opt-in form, etc. — standard WordPress stuff);
*   list the 15 latest posts (configurable);
*   display links to the author archive;
*   display links to the monthly archive;
*   add additional widget areas (to display things like the most popular content, categories, tags).

Lastly, the page will be responsive and will not depend on the current theme of the website it’s being used on.

That being said, we do have to start by using <em>some</em> theme as the base of our work here. I’ll use <a href="https://wordpress.org/themes/minimalzerif/">Zerif Lite</a>. I admit, I may be a bit biased here because it is one of our own themes (at ThemeIsle). Nonetheless, it was one of the 10 most popular themes released last year in WordPress’ theme directory, so I hope you’ll let this one slide.

And, hey, if you don’t like the theme, no hard feelings. You can use the approach presented here with any other theme.</p>

## Getting Started With The Main File

The best model on which to build your archive page is the <code>page.php</code> file of your current theme, for a couple of reasons:

*   Its structure is already optimized to display custom content within the main content block.
*   It’s probably one of the simplest page templates in your theme’s structure.

Therefore, starting with the <code>page.php</code> file of the Zerif Lite theme, I’m going to make a copy and call it <code>tmpl_archives.php</code>.

(Make sure not to call your page something like <code>page-archives.php</code>. All file names starting with <code>page-</code> will be treated as new page templates within the main file <a href="https://www.codeinwp.com/blog/wordpress-theme-heirarchy/">hierarchy of WordPress themes</a>. That’s why we’re using the prefix <code>tmpl_</code> here.)

Next, all I’m going to do is change one single line in that file:

<pre><code class="language-php">
&lt;?php get_template_part( 'content', 'page' ); ?&gt;
</code></pre>

We’ll change that to this:

<pre><code class="language-php">
&lt;?php get_template_part( 'content', 'tmpl_archives' ); ?&gt;
</code></pre>

All this does is fetch the right content file for our archive page.

If you want, you could remove other elements that seem inessential to your archive page (like comments), but make sure to leave in all of the elements that make up the HTML structure. And in general, don’t be afraid to experiment. After all, if something stops working, you can easily bring back the previous code and debug from there.

Also, don’t forget about the standard custom template declaration comment, which you need to place at the very beginning of your new file (in this case, <code>tmpl_archives.php</code>):

<pre><code class="language-php">
&lt;?php
/* Template Name: Archive Page Custom */
?&gt;
</code></pre>

After that, what we’re left with is the following file structure (with some elements removed for readability):

<pre><code class="language-php">
&lt;?php
/* Template Name: Archive Page Custom */
get_header(); ?&gt;

&lt;div class="clear"&gt;&lt;/div&gt;
&lt;/header&gt; &lt;!-- / END HOME SECTION --&gt;

&lt;div id="content" class="site-content"&gt;

&lt;div class="container"&gt;

  &lt;div class="content-left-wrap col-md-9"&gt;
    &lt;div id="primary" class="content-area"&gt;
      &lt;main id="main" class="site-main" role="main"&gt;

        &lt;?php while ( have_posts() ) : the_post(); // standard WordPress loop. ?&gt;

          &lt;?php get_template_part( 'content', 'tmpl_archives' ); // loading our custom file. ?&gt;

        &lt;?php endwhile; // end of the loop. ?&gt;

      &lt;/main&gt;&lt;!-- #main --&gt;
    &lt;/div&gt;&lt;!-- #primary --&gt;
  &lt;/div&gt;
  &lt;div class="sidebar-wrap col-md-3 content-left-wrap"&gt;
    &lt;?php get_sidebar(); ?&gt;
  &lt;/div&gt;

&lt;/div&gt;&lt;!-- .container --&gt;

&lt;?php get_footer(); ?&gt;
</code></pre>

Next, let’s create the other piece of the puzzle — a custom content file. We’ll start with the <code>content-page.php</code> file by making a copy and renaming it to <code>content-tmpl_archives.php</code>.

In this file, we’re going to remove anything that’s not essential, keeping only the structural elements, plus the basic WordPress function calls:

<pre><code class="language-php">
&lt;?php
/**
* The template used to display archive content
*/
?&gt;

&lt;article id="post-&lt;?php the_ID(); ?&gt;" &lt;?php post_class(); ?&gt;&gt;

  &lt;header class="entry-header"&gt;
    &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
  &lt;/header&gt;&lt;!-- .entry-header --&gt;

  &lt;div class="entry-content"&gt;
    &lt;?php the_content(); ?&gt;

    &lt;!-- THIS IS WHERE THE FUN PART GOES --&gt;

  &lt;/div&gt;&lt;!-- .entry-content --&gt;

&lt;/article&gt;&lt;!-- #post-## --&gt;
</code></pre>

The placeholder comment visible in the middle is where we’re going to start including our custom elements.</p>

### Adding a Custom Welcome Message

This one’s actually already taken care of by WordPress. The following line does the magic:

<pre><code class="language-php">
&lt;?php the_content(); ?&gt;
</code></pre>

### Adding New Widget Areas

Let’s start this part by setting up new widget areas in WordPress using the standard process. However, let’s do it through an additional functions file, just to keep things reusable from theme to theme.

So, we begin by creating a new file, <code>archives-page-functions.php</code>, placing it in the theme’s main directory, and registering the two new widget areas in it:

<pre><code class="language-php">
if(!function_exists('archives_page_widgets_init')) :
function archives_page_widgets_init() {
  /* First archive page widget, displayed to the LEFT. */
  register_sidebar(array(
    'name' =&gt; __('Archives page widget LEFT', 'zerif-lite'),
    'description' =&gt; __('This widget will be shown on the left side of your archive page.', 'zerif-lite'),
    'id' =&gt; 'archives-left',
    'before_widget' =&gt; '&lt;div class="archives-widget-left"&gt;',
    'after_widget' =&gt; '&lt;/div&gt;',
    'before_title' =&gt; '&lt;h1 class="widget-title"&gt;',
    'after_title' =&gt; '&lt;/h1&gt;',
  ));

  /* Second archive page widget, displayed to the RIGHT. */
  register_sidebar(array(
    'name' =&gt; __('Archives page widget RIGHT', 'zerif-lite'),
    'description' =&gt; __('This widget will be shown on the right side of your archive page.', 'zerif-lite'),
    'id' =&gt; 'archives-right',
    'before_widget' =&gt; '&lt;div class="archives-widget-right"&gt;',
    'after_widget' =&gt; '&lt;/div&gt;',
    'before_title' =&gt; '&lt;h1 class="widget-title"&gt;',
    'after_title' =&gt; '&lt;/h1&gt;',
  ));
}
endif;
add_action('widgets_init', 'archives_page_widgets_init');
</code></pre>

Next, we’ll need some custom styling for the archive page, so let’s also “enqueue” a new CSS file:

<pre><code class="language-php">
if(!function_exists('archives_page_styles')) :
function archives_page_styles() {
  if(is_page_template('tmpl_archives.php')) {
    wp_enqueue_style('archives-page-style', get_template_directory_uri() . '/archives-page-style.css'); // standard way of adding style sheets in WP.
  }
}
endif;
add_action('wp_enqueue_scripts', 'archives_page_styles');
</code></pre>

This is a conditional enqueue operation. It will run only if the visitor is browsing the archive page.

Also, let’s not forget to enable this new <code>archives-page-functions.php</code> file by adding this line at the very end of the current theme’s <code>functions.php</code> file:

<pre><code class="language-php">
require get_template_directory() . '/archives-page-functions.php';
</code></pre>

Finally, the new block that we’ll use in our main <code>content-tmpl_archives.php</code> file is quite simple. Just place the following right below the call to <code>the_content();</code>:

<pre><code class="language-php">
&lt;?php /* Enabling the widget areas for the archive page. */ ?&gt;
&lt;?php if(is_active_sidebar('archives-left')) dynamic_sidebar('archives-left'); ?&gt;
&lt;?php if(is_active_sidebar('archives-right')) dynamic_sidebar('archives-right'); ?&gt;
&lt;div style="clear: both; margin-bottom: 30px;"&gt;&lt;/div&gt;&lt;!-- clears the floating --&gt;
</code></pre>

All that’s left now is to take care of the only missing file, <code>archives-page-style.css</code>. But let’s leave it for later because we’ll be using it as a place to store all of the styles of our custom archive page, not just those for widgets.</p>

### Listing the 15 Latest Posts

For this, we’ll do some manual PHP coding. Even though displaying this could be achieved through various widgets, let’s keep things diverse and get our hands a bit dirty just to show more possibilities.

You’re probably asking why the arbitrary number of 15 posts? Well, I don’t have a good reason, so let’s actually make this configurable through custom fields.

Here’s how we’re going to do it:

*   Setting the number of posts will be possible through the custom field `archived-posts-no`.
*   If the number given is not correct, the template will default to displaying the 15 latest posts.

Below is the code that does this. Place it right below the previous section in the <code>content-tmpl_archives.php</code> file, the one that handles the new widget areas.</p>

<pre><code class="language-php">
&lt;?php
$how_many_last_posts = intval(get_post_meta($post-&gt;ID, 'archived-posts-no', true));

/* Here, we're making sure that the number fetched is reasonable. In case it's higher than 200 or lower than 2, we're just resetting it to the default value of 15. */
if($how_many_last_posts &gt; 200 || $how_many_last_posts &lt; 2) $how_many_last_posts = 15;

$my_query = new WP_Query('post_type=post&amp;nopaging=1');
if($my_query-&gt;have_posts()) {
  echo '&lt;h1 class="widget-title"&gt;Last '.$how_many_last_posts.' Posts &lt;i class="fa fa-bullhorn" style="vertical-align: baseline;"&gt;&lt;/i&gt;&lt;/h1&gt;&amp;nbsp;';
  echo '&lt;div class="archives-latest-section"&gt;&lt;ol&gt;';
  $counter = 1;
  while($my_query-&gt;have_posts() &amp;&amp; $counter &lt;= $how_many_last_posts) {
    $my_query-&gt;the_post(); 
    ?&gt;
    &lt;li&gt;&lt;a href="&lt;?php the_permalink() ?&gt;" rel="bookmark" title="Permanent Link to &lt;?php the_title_attribute(); ?&gt;"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/li&gt;
    &lt;?php
    $counter++;
  }
  echo '&lt;/ol&gt;&lt;/div&gt;';
  wp_reset_postdata();
}
?&gt;
</code></pre>

Basically, all this does is look at the custom field’s value, set the number of posts to display and then fetch those posts from the database using <code>WP_Query();</code>. I’m also using some Font Awesome icons to add some flare to this block.</p>

### Displaying Links to the Author Archives

(This section is only useful if you’re dealing with a multi-author blog. Skip it if you are the sole author.)

This functionality can be achieved with a really simple block of code placed right in our main <code>content-tmpl_archives.php</code> file (below the previous block):

<pre><code class="language-php">
&lt;h1 class="widget-title"&gt;Our Authors &lt;i class="fa fa-user" style="vertical-align: baseline;"&gt;&lt;/i&gt;&lt;/h1&gt;&amp;nbsp;
&lt;div class="archives-authors-section"&gt;
  &lt;ul&gt;
    &lt;?php wp_list_authors('exclude_admin=0&amp;optioncount=1'); ?&gt;
  &lt;/ul&gt;
&lt;/div&gt;
</code></pre>

We’ll discuss the styles in just a minute. Right now, please note that everything is done through a <code class="language-php">wp_list_authors()</code> function call.</p>

### Displaying Links to the Monthly Archives

I’m including this element at the end because it’s not the most useful one from a reader’s perspective. Still, having it on your archive page is nice just so that you don’t have to use widgets for the monthly archive elsewhere.

Here’s what it looks like in the <code>content-tmpl_archives.php</code> file:

<pre><code class="language-php">
&lt;h1 class="widget-title"&gt;By Month &lt;i class="fa fa-calendar" style="vertical-align: baseline;"&gt;&lt;/i&gt;&lt;/h1&gt;&amp;nbsp;
&lt;div class="archives-by-month-section"&gt;
  &lt;p&gt;&lt;?php wp_get_archives('type=monthly&amp;format=custom&amp;after= |'); ?&gt;&lt;/p&gt;
&lt;/div&gt;
</code></pre>

This time, we’re displaying this as a single paragraph, with entries separated by a pipe (|).

(Smashing Magazine already has a really good tutorial on how to <a href="https://www.smashingmagazine.com/2014/08/27/customizing-wordpress-archives-categories-terms-taxonomies/">customize individual archive pages</a> for categories, tags and other taxonomies in WordPress.)

### The Complete Archive Page Template

OK, just for clarity, let’s look at our complete <code>content-tmpl_archives.php</code> file, which is the main file that takes care of displaying our custom archive:

<pre><code class="language-php">
&lt;?php
/**
* The template used to display archive content
*/
?&gt;

&lt;article id="post-&lt;?php the_ID(); ?&gt;" &lt;?php post_class(); ?&gt;&gt;

&lt;header class="entry-header"&gt;
  &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
&lt;/header&gt;&lt;!-- .entry-header --&gt;

&lt;div class="entry-content"&gt;
  &lt;?php the_content(); ?&gt;

  &lt;?php if(is_active_sidebar('archives-left')) dynamic_sidebar('archives-left'); ?&gt;
  &lt;?php if(is_active_sidebar('archives-right')) dynamic_sidebar('archives-right'); ?&gt;
  &lt;div style="clear: both; margin-bottom: 30px;"&gt;&lt;/div&gt;&lt;!-- clears the floating --&gt;

  &lt;?php
  $how_many_last_posts = intval(get_post_meta($post-&gt;ID, 'archived-posts-no', true));
  if($how_many_last_posts &gt; 200 || $how_many_last_posts &lt; 2) $how_many_last_posts = 15;

  $my_query = new WP_Query('post_type=post&amp;nopaging=1');
  if($my_query-&gt;have_posts()) {
    echo '&lt;h1 class="widget-title"&gt;Last '.$how_many_last_posts.' Posts &lt;i class="fa fa-bullhorn" style="vertical-align: baseline;"&gt;&lt;/i&gt;&lt;/h1&gt;&amp;nbsp;';
    echo '&lt;div class="archives-latest-section"&gt;&lt;ol&gt;';
    $counter = 1;
    while($my_query-&gt;have_posts() &amp;&amp; $counter &lt;= $how_many_last_posts) {
      $my_query-&gt;the_post();
      ?&gt;
      &lt;li&gt;&lt;a href="&lt;?php the_permalink() ?&gt;" rel="bookmark" title="Permanent Link to &lt;?php the_title_attribute(); ?&gt;"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/li&gt;
      &lt;?php
      $counter++;
    }
    echo '&lt;/ol&gt;&lt;/div&gt;';
    wp_reset_postdata();
  }
  ?&gt;

  &lt;h1 class="widget-title"&gt;Our Authors &lt;i class="fa fa-user" style="vertical-align: baseline;"&gt;&lt;/i&gt;&lt;/h1&gt;&amp;nbsp;
  &lt;div class="archives-authors-section"&gt;
    &lt;ul&gt;
      &lt;?php wp_list_authors('exclude_admin=0&amp;optioncount=1'); ?&gt;
    &lt;/ul&gt;
  &lt;/div&gt;

  &lt;h1 class="widget-title"&gt;By Month &lt;i class="fa fa-calendar" style="vertical-align: baseline;"&gt;&lt;/i&gt;&lt;/h1&gt;&amp;nbsp;
  &lt;div class="archives-by-month-section"&gt;
    &lt;p&gt;&lt;?php wp_get_archives('type=monthly&amp;format=custom&amp;after= |'); ?&gt;&lt;/p&gt;
  &lt;/div&gt;

&lt;/div&gt;&lt;!-- .entry-content --&gt;

&lt;/article&gt;&lt;!-- #post-## --&gt;
</code></pre>

### The Style Sheet

Lastly, let’s look at the style sheet and, most importantly, the effect it gives us.

Here’s the <code>archives-page-style.css</code> file:

<pre><code class="language-css">
.archives-widget-left {
  float: left;
  width: 50%;
}

.archives-widget-right {
  float: left;
  padding-left: 4%;
  width: 46%;
}

.archives-latest-section { }
.archives-latest-section ol {
  font-style: italic;
  font-size: 20px;
  padding: 10px 0;
}
.archives-latest-section ol li {
  padding-left: 8px;
}

.archives-authors-section { }
.archives-authors-section ul {
  list-style: none;
  text-align: center;
  border-top: 1px dotted #888;
  border-bottom: 1px dotted #888;
  padding: 10px 0;
  font-size: 20px;
  margin: 0 0 20px 0;
}
.archives-authors-section ul li {
  display: inline;
  padding: 0 10px;
}
.archives-authors-section ul li a {
  text-decoration:none;
}

.archives-by-month-section {
   ext-align: center;
  word-spacing: 5px;
}
.archives-by-month-section p {
  border-top: 1px dotted #888;
  border-bottom: 1px dotted #888;
  padding: 15px 0;
}
.archives-by-month-section p a {
  text-decoration:none;
}

@media only screen and (max-width: 600px) {
  .archives-widget-left {
    width: 100%;
  }

  .archives-widget-right {
    width: 100%;
  }
}
</code></pre>

This is mostly typography and not a lot of structural elements, except for the couple of <code>float</code> alignments, plus the responsive design block at the end.

OK, let’s see the result! Here’s what it looks like on a website that already has quite a bit of content in the archive:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70ccf7bc-451f-4b47-bf3c-14391ee6bae8/zerif-example-large-preview-opt.jpg"><img title="Archives page on Zerif Lite." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe5c8dcd-fac5-42de-80e6-d43e443497ec/zerif-example-preview-opt.jpg" alt="Archive page on Zerif Lite" width="500" height="1074" /></a><figcaption>Our custom archive page in the Zerif Lite theme. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70ccf7bc-451f-4b47-bf3c-14391ee6bae8/zerif-example-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

## How To Integrate This Template With Any Theme

The custom archive page we are building here is for the Zerif Lite theme, in the official WordPress directory. However, like I said, it can be used with any theme. Here’s how to do that:

1.  Take the `archives-page-style.css` file and the `archives-page-functions.php` file that we built here and put them in your theme’s main directory.
2.  Edit the `functions.php` file of your theme and add this line at the very end: `require get_template_directory() . '/archives-page-functions.php';`.
3.  Take the `page.php` file of your theme, make a copy, rename it, change the `get_template_part()` function call to `get_template_part( 'content', 'tmpl_archives' );`, and then add the main declaration comment at the very beginning: `/* Template Name: Archive Page Custom */`.
4.  Take the `content-page.php` file of your theme, make a copy, rename it to `content-tmpl_archives.php`, and include all of the custom blocks that we created in this guide right below the `the_content();` function call.
5.  Test and enjoy.

Here’s what it looks like in the default Twenty Fifteen theme:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94b597c3-9962-43be-997b-9fc25f86fb30/tf-example-large-preview-opt.jpg"><img title="Archive page in Twenty Fifteen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3c2f102-7cbb-4a42-bf1e-9d516655bf7c/tf-example-preview-opt.jpg" alt="Archive page in Twenty Fifteen" width="500" height="927" /></a><figcaption>Our custom archive page in the Twenty Fifteen theme. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94b597c3-9962-43be-997b-9fc25f86fb30/tf-example-large-preview-opt.jpg">View large version</a>)</figcaption></figure>

## What’s Next?

We’ve covered a lot of ground in this guide, but a lot can still be done with our archive page. We could widgetize the whole thing and erase all of the custom code elements. We could add more visual blocks for things like the latest content, and so on.

The possibilities are truly endless. So, what would you like to see as an interesting addition to this template? Feel free to share.

{{< signature "dp, al, ml" >}}


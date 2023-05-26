---
title: A Detailed Guide To A Custom WordPress Page Templates
slug: wordpress-custom-page-templates
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9315729-7ed1-4428-aebe-86942c0bbc1b/excerpt-templates.jpg
date: 2015-06-19T21:15:19.000Z
author: nickschaeferhoff
description: >-
  I like to think of **WordPress** as the gateway drug of web development. Many
  people who get started using the platform are initially merely looking for a
  comfortable (and free) way to create a simple website. Some Googling and
  consultation of the WordPress Codex later, it's done and that should be it.
  Kind of like "I'm just going to try it once.
categories:
  - WordPress
  - Techniques (WP)
---
I like to think of <strong>WordPress</strong> as the gateway drug of web development. Many people who get started using the platform are initially merely looking for a comfortable (and free) way to create a simple website, often with the help of a <a href="https://www.000webhost.com/blog/wordpress-page-builders">WordPress page builder plugin</a>. Kind of like “I’m just going to try it once.” 

However, a good chunk of users don't stop there. Instead, they get hooked. Come up with more ideas. Experiment. Try out new plugins. Discover <a href="https://addons.mozilla.org/en-us/firefox/addon/firebug/">Firebug</a>. Boom. Soon there is no turning back. Does that sound like your story? As a WordPress user it is only natural to want more and more control over your website. To crave custom design, custom functionality, custom everything.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Create And Customize A WordPress Child Theme](https://www.smashingmagazine.com/2016/01/create-customize-wordpress-child-theme/)
*   [Building A Custom Archive Page For WordPress](https://www.smashingmagazine.com/2015/04/building-custom-wordpress-archive-page/)
*   [Customizing WordPress Archives](https://www.smashingmagazine.com/2014/08/customizing-wordpress-archives-categories-terms-taxonomies/)

Luckily, WordPress is built for exactly that. Its flexible structure and compartmentalized architecture allows anyone to change practically anything on their site.

{{% feature-panel %}}

Among the most important tools in the quest for complete website control are page templates. They allow users to <strong>dramatically alter their website's design</strong> and functionality. Want a customized header for your front page? Done. An additional sidebar only for your blog page? No problem. <a href="https://www.smashingmagazine.com/2014/08/a-better-404-page/">A unique 404 error page</a>? Be. My. Guest.

If you want to know how <strong>WordPress page templates</strong> can help you achieve that, read on. But first, a little background information.</p>

## Template Files In WordPress

What are we talking about when we speak of templates in the context of WordPress? The short version is that templates are files which tell WordPress how to display different types of content.

The slightly longer version: every time someone sends a request to view part of your website, the WordPress platform will figure out what content they want to see and how that specific part of your website should be rendered.

For the latter, WordPress will attempt to use the most appropriate template file found within your theme. Which one is decided on the basis of a set order, the <a href="https://codex.wordpress.org/Template_Hierarchy#The_Template_Hierarchy_In_Detail">WordPress template hierarchy</a>. You can see what this looks like in the screenshot below or in this <a href="https://wphierarchy.com/">interactive version</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36c0b05f-5bc0-46ef-aafd-ebf3f58512b8/01-wp-template-hierarchy-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38f7ea0f-8f81-4f08-9fae-d10e1b8943dc/01-wp-template-hierarchy-opt-small.jpg" alt="custom wordpress" width="500" height="307" /></a><figcaption>The WordPress template hierarchy. (Image credit: <a href="https://codex.wordpress.org/">WordPress Codex</a>)(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36c0b05f-5bc0-46ef-aafd-ebf3f58512b8/01-wp-template-hierarchy-opt.jpg">View large version</a>)</figcaption></figure>

The template hierarchy is a list of template files WordPress is familiar with that are ranked to determine which file takes precedence over another.

You can think of it as a decision tree. When WordPress tries to decide how to display a given page, it <strong>works its way down the template hierarchy</strong> until it finds the first template file that fits the requested page. For example, if somebody attempted to access the address <em>https://yoursite.com/category/news</em>, WordPress would look for the correct template file in this order:

1.  _category-{slug}.php_: in this case _category-news.php_
2.  _category-{id}.php_>: if the category ID were 5, WordPress would try to find a file named _category-5.php_
3.  _category.php_
4.  _archive.php_
5.  _index.php_

At the bottom of the hierarchy is <em>index.php</em>. It will be used to display any content which does not have a more specific template file attached to its name. If a template file ranks higher in the hierarchy, WordPress will automatically use that file in order to display the content in question.</p>

### Page Templates And Their Use

For pages, the standard template is usually the aptly named <em>page.php</em>. Unless there is a more specific template file available (such as <em>archive.php</em> for an archive page), WordPress will use <em>page.php</em> to render the content of all pages on your website.

However, in many cases it might be necessary to change the design, look, feel or functionality of individual parts of your website. This is where page templates come into play. Customized page templates allow you to <strong>individualize any part</strong> of your WordPress site without affecting the rest of it.

You might have already seen this at work. For example, many WordPress themes today come with an option to change your page to full width, add a second sidebar or switch the sidebar's location. If that is the case for yours, it was probably done through template files. There are several ways to accomplish this and we'll go over them later.

First, however, a word of caution: since working with templates involves editing and changing files in your active theme, it's always a <strong>good idea to go with a child theme</strong> when making these kinds of customizations. That way you don't run the danger of having your changes overwritten when your parent theme gets updated.</p>

## How To Customize Any Page In WordPress

There are three basic ways to use custom page templates in WordPress: adding conditional statements to an existing template; creating specific page templates which rank higher in the hierarchy; and directly assigning templates to specific pages. We will take a look at each of these in turn.</p>

### Using Conditional Tags In Default Templates

An easy way to make page-specific changes is to add <a href="https://codex.wordpress.org/Conditional_Tags">WordPress's many conditional tags</a> to a template already in use. As the name suggests, these tags are used to create functions which are only executed if a certain condition is met. In the context of page templates, this would be something along the line of <em>"Only perform action X on page Y."</em>

Typically, you would add conditional tags to your theme's <em>page.php</em> file (unless, of course, you want to customize a different part of your website). They enable you to make changes limited to the homepage, front page, blog page or any other page of your site.

Here are some frequently used conditional tags:

1.  `is_page()`: to target a specific page. Can be used with the page's ID, title, or URL/name.
2.  `is_home()`: applies to the home page.
3.  `is_front_page()`: targets the front page of your site as set under Settings → Reading
4.  `is _category()`: condition for a category page. Can use ID, title or URL/name like `is_page()` tag.
5.  `is_single()`: for single posts or attachments
6.  `is_archive()`: conditions for archive pages
7.  `is_404()`: applies only to 404 error pages

For example, when added to your <em>page.php</em> in place of the standard <code>get_header();</code> tag, the following code will load a custom header file named <em>header-shop.php</em> when displaying the page <em>https://yoursite.com/products</em>.</p>

<pre><code class="language-php">if ( is_page('products') ) {
  get_header( 'shop' );
} else {
  get_header();
}</code></pre>

A good use case for this would be if you have a shop on your site and you need to display a different header image or customized menu on the shop page. You could then add these customization in <em>header-shop.php</em> and it would show up in the appropriate place.

However, conditional tags are not limited to one page. You can make several statements in a row like so:

<pre><code class="language-php">if ( is_page('products') ) {
  get_header( 'shop' );
} elseif ( is_page( 42 ) ) {
  get_header( 'about' );
} else {
  get_header();
}</code></pre>

In this second example, two conditions will change the behavior of different pages on your site. Besides loading the aforementioned shop-specific header file, it would now also load a <em>header-about.php</em> on a page with the ID of 42. For all other pages the standard header file applies.

To learn more about the use of conditional tags, the following resources are highly recommended:

*   [WordPress Codex: Conditional Tags](https://codex.wordpress.org/Conditional_Tags)
*   [ThemeLab: The Ultimate Guide to WordPress Conditional Tags](https://www.themelab.com/ultimate-guide-wordpress-conditional-tags/)

### Creating Page-Specific Files In The WordPress Hierarchy

Conditional tags are a great way to introduce smaller changes to your page templates. Of course, you can also <strong>create larger customizations by using many conditional statements</strong> one after the other. I find this a very cumbersome solution, however, and would opt for designated template files instead.

One way to do this is to exploit the WordPress template hierarchy. As we have seen, the hierarchy will traverse a list of possible template files and choose the first one it can find that fits. For pages, the hierarchy looks like this:

*   Custom page template
*   _page-{slug}.php_
*   _page-{id}.php_
*   _page.php_
*   _index.php_

In first place are custom page templates which have been directly assigned to a particular page. If one of those exists, WordPress will use it no matter which other template files are present. We will talk more about custom page templates in a bit.

After that, WordPress will look for a page template that includes the slug of the page in question. For example, if you include a file named <em>page-about.php</em> in your theme files, WordPress will use this file to display your 'About' page or whichever page can be found under <em>https://www.yoursite.com/about</em>.

Alternatively, you can achieve the same by targeting your page's ID. So if that same page has an ID of 5, WordPress will use the template file <em>page-5.php</em> before <em>page.php</em> if it exists; that is, only if there isn't a higher-ranking page template available.

(BTW, you can find out the ID for every page by hovering over its title under 'All Pages' in your WordPress back-end. The ID will show up in the link displayed by your browser.)

### Assigning Custom Page Templates

Besides providing templates in a form that WordPress will use automatically, it is also possible to manually assign custom templates to specific pages. As you can see from the template hierarchy, these will <strong>trump any other template file</strong> present in the theme folder.

Just like creating page-specific templates for the WordPress hierarchy, this requires you to provide a template file and then link it to whichever page you want to use it for. The latter can be done in two different ways you might already be familiar with. Just in case you aren't, here is how to do it.

#### 1. Assigning Custom Page Templates From The WordPress Editor

In the WordPress editor, you find an option field called 'Page Attributes' with a drop-down menu under 'Template'.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/414ee5d4-e152-4966-bce3-26f30ad49ad9/02-page-attributes-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1fb86798-80e2-4837-947d-d1eab88cf58f/02-page-attributes-opt-small.jpg" alt="Page Attributes in the WordPress editor." /></a><figcaption>Page Attributes in the WordPress editor. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/414ee5d4-e152-4966-bce3-26f30ad49ad9/02-page-attributes-opt.jpg">View large version</a>)</figcaption></figure>

Clicking on it will give you a list of available page templates on your WordPress website. Choose the one you desire, save or update your page and you are done.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa7cbb12-1c03-4733-ad45-5791cf5b89af/03-choose-page-template-manually-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c35f36e1-cfcf-4cbb-9cda-62f92c8cbdb2/03-choose-page-template-manually-opt-small.jpg" alt="Available templates under Page Attributes." /></a><figcaption>Available templates under Page Attributes. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa7cbb12-1c03-4733-ad45-5791cf5b89af/03-choose-page-template-manually-opt.jpg">View large version</a>)</figcaption></figure>

#### 2. Setting A Custom Template Via Quick Edit

The same can also be achieved without entering the WordPress editor. Go to 'All Pages' and hover over any item in the list there. A menu will become visible that includes the 'Quick Edit' item.

Click on it to edit the page settings directly from the list. You will see the same drop-down menu for choosing a different page template. Pick one, update the page and you are done.

Not so hard after all, is it? But what if you don't have a custom page template yet? How do you create it so that your website looks exactly the way you want it? Don't worry, that's what the next part is all about.</p>

## A Step-By-Step Guide To Creating Custom Page Templates

Putting together customized template files for your pages is not that hard but here are a few details you have to pay attention to. Therefore, let's go over the process bit-by-bit.</p>

### 1. Find The Default Template

A good way is to start by copying the template which is currently used by the page you want to modify. It's easier to modify existing code than to <a href="https://www.smashingmagazine.com/2012/06/create-responsive-mobile-first-wordpress-theme/">write an entire page from scratch</a>. In most cases this will be the <em>page.php</em> file.

(If you don't know how to find out which template file is being used on the page you want to edit, the plugin <a href="https://wordpress.org/plugins/what-the-file/">What The File</a> will prove useful.)

I will be using the Twenty Twelve theme for demonstration. Here is what its standard page template looks like:

<pre><code class="language-php">
&lt;?php
/**
 * The template for displaying all pages
 *
 * This is the template that displays all pages by default.
 * Please note that this is the WordPress construct of pages
 * and that other 'pages' on your WordPress site will use a
 * different template.
 *
 * @package WordPress
 * @subpackage Twenty_Twelve
 * @since Twenty Twelve 1.0
 */
get_header(); ?&gt;

  &lt;div id="primary" class="site-content"&gt;
    &lt;div id="content" role="main"&gt;

      &lt;?php while ( have_posts() ) : the_post(); ?&gt;
        &lt;?php get_template_part( 'content', 'page' ); ?&gt;
        &lt;?php comments_template( ’, true ); ?&gt;
      &lt;?php endwhile; // end of the loop. ?&gt;

    &lt;/div&gt;&lt;!-- #content --&gt;
  &lt;/div&gt;&lt;!-- #primary --&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;
</code></pre>

As you can see, nothing too fancy here: the usual calls for the header and footer, and the loop in the middle. The page in question looks like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/defb1edb-4204-4075-b90b-390f6d35ed43/04-default-template-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30678c07-3eee-4876-8dc4-a1b0d3a85b67/04-default-template-opt-small.jpg" alt="The default page template in the Twenty Twelve theme." /></a><figcaption>The default page template in the Twenty Twelve theme. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/defb1edb-4204-4075-b90b-390f6d35ed43/04-default-template-opt.jpg">View large version</a>)</figcaption></figure>

### 2. Copy And Rename The Template File

After identifying the default template file, it's time to make a copy. We will use the duplicated file in order to make the desired changes to our page. For that we will also have to rename it. Can't have two files of the same name, that's just confusing for everyone.

You are free to give the file any name you like as long as it doesn't start with any of the <a href="https://codex.wordpress.org/Theme_Development#Template_Files_List">reserved theme filenames</a>. So don't be naming it <em>page-something.php</em> or anything else that would make WordPress think it is a dedicated template file.

It makes sense to use a name which easily identifies what this template file is used for, such as <em>my-custom-template.php</em>. In my case I will go with <em>custom-full-width.php</em>.</p>

### 3. Customize The Template File Header

Next we have to tell WordPress that this new file is a custom page template. For that, we will have to adjust the file header in the following way:

<pre><code class="language-php">
&lt;?php
/*
 * Template Name: Custom Full Width
 * description: >-
  Page template without sidebar
 */

// Additional code goes here...
</code></pre>

The name under 'Template Name' is what will be displayed under 'Page Attributes' in the WordPress editor. Make sure to adjust it to your template name.</p>

### 4. Customize The Code

Now it's time to get to the meat and potatoes of the page template: the code. In my example, I merely want to remove the sidebar from my demo page.

This is relatively easy, as all I have to do is remove <code>&lt;?php get_sidebar(); ?&gt;</code> from my page template since that's what is calling the sidebar. As a consequence, my custom template ends up looking like this:

<pre><code class="language-php">&lt;?php
/*
 * Template Name: Custom Full Width
 * description: >-
  Page template without sidebar
 */

get_header(); ?&gt;

&lt;div id="primary" class="site-content"&gt;
  &lt;div id="content" role="main"&gt;

    &lt;?php while ( have_posts() ) : the_post(); ?&gt;
      &lt;?php get_template_part( 'content', 'page' ); ?&gt;
      &lt;?php comments_template( ’, true ); ?&gt;
    &lt;?php endwhile; // end of the loop. ?&gt;

  &lt;/div&gt;&lt;!-- #content --&gt;
&lt;/div&gt;&lt;!-- #primary --&gt;

&lt;?php get_footer(); ?&gt;
</code></pre>

### 5. Upload The Page Template

After saving my customized file, it is now time to upload it to my website. Custom page templates can be saved in several places to be recognized by WordPress:

*   Your active (child) theme's folder
*   The folder of your main parent theme
*   A subfolder within either of these

I personally like to create a folder named <em>page_templates</em> in my child theme and place any customized templates in there. I find this easiest to retain an overview over my files and customizations.</p>

### 6. Activate The Template

As a last step, you need to activate the page template. As mentioned earlier, this is done under Page Attributes → Templates in the WordPress editor. Save, view the page and voilà! Here is my customized page without a sidebar:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fc7a808-2c91-4d39-b034-ac419bb37bb5/05-custom-wp-page-template-without-sidebar-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02580fc0-2dca-466f-a109-e5758d202533/05-custom-wp-page-template-without-sidebar-opt-small.jpg" alt="Customized page template without the sidebar." /></a><figcaption>Customized page template without the sidebar. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fc7a808-2c91-4d39-b034-ac419bb37bb5/05-custom-wp-page-template-without-sidebar-opt.jpg">View large version</a>)</figcaption></figure>

Not so hard, is it? Don't worry, you will quickly get the hang of it. To give you a better impression of what to use these page templates for, I will demonstrate additional use cases (including the code) for the remainder of the article.</p>

## Five Different Ways To Use Page Templates

As already mentioned, page templates can be employed for many different purposes. You can customize pretty much anything on any page with their help. Only your imagination (and coding abilities) stand in your way.</p>

### 1. Full-Width Page Template

The first case we will look at is an advanced version of the demo template we created above. Up there, we already removed the sidebar by deleting <code>&lt;?php get_sidebar(); ?&gt;</code> from the code. However, as you have seen from the screenshot this does not actually result in a full-width layout since the content section stays on the left.

To address this, we need to deal with the CSS, in particular this part:

<pre><code class="language-css">.site-content {
  float: left;
  width: 65.1042%;
}</code></pre>

The <code>width</code> attribute limits the element which holds our content to 65.1042% of the available space. We want to increase this.

If we just change it to 100%, however, this will affect all other pages on our site, which is far from what we want. Therefore, the first order here is to change the primary <code>div</code>'s class in our custom template to something else, like <code>class="site-content-fullwidth"</code>. The result:

<pre><code class="language-php">
&lt;?php
/*
 * Template Name: Custom Full Width
 * description: >-
  Page template without sidebar
 */

get_header(); ?&gt;

&lt;div id="primary" class="site-content-fullwidth"&gt;
  &lt;div id="content" role="main"&gt;

    &lt;?php while ( have_posts() ) : the_post(); ?&gt;
      &lt;?php get_template_part( 'content', 'page' ); ?&gt;
      &lt;?php comments_template( ’, true ); ?&gt;
    &lt;?php endwhile; // end of the loop. ?&gt;

  &lt;/div&gt;&lt;!-- #content --&gt;
&lt;/div&gt;&lt;!-- #primary --&gt;

&lt;?php get_footer(); ?&gt;
</code></pre>

Now we can adjust the CSS for our new custom class:

<pre><code class="language-css">.site-content-fullwidth {
  float: left;
  width: 100%;
}</code></pre>

As a result, the content now stretches all the way across the screen.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9c60ab6-500a-42a0-8e47-32ffebed0d2d/06-custom-full-width-wp-page-template-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f527548-e1a8-46de-9148-98c4740620d0/06-custom-full-width-wp-page-template-opt-small.jpg" alt="The custom page template at full width." /></a><figcaption>The custom page template at full width. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9c60ab6-500a-42a0-8e47-32ffebed0d2d/06-custom-full-width-wp-page-template-opt.jpg">View large version</a>)</figcaption></figure>

### 2. Dynamic 404 Error Page With Widget Areas

The 404 error page is where every person lands who tries to access a page on your website that doesn't exist, be it through a typo, a faulty link or because the page's permalink has changed.

Despite the fact that getting a 404 is disliked by everyone on the Internet, if you are running a website the 404 error page is of no little importance. Its content can be the decisive factor on whether someone immediately abandons your site or sticks around and checks out your other content.

Coding a customized error page from scratch is cumbersome, especially if you are not confident in your abilities. <strong>A better way is to build widget areas into your template</strong> so you can flexibly change what is displayed there by drag and drop.

For this we will grab and edit the <em>404.php</em> file that ships with Twenty Twelve (template hierarchy, remember?). However, before we change anything on there, we will first create a new widget by inserting the following code into our <em>functions.php</em> file:

<pre><code class="language-php">
register_sidebar( array(
  'name' =&gt; '404 Page',
  'id' =&gt; '404',
  'description'  =&gt; __( 'Content for your 404 error page goes here.' ),
  'before_widget' =&gt; '&lt;div id="error-box"&gt;',
  'after_widget' =&gt; '&lt;/div&gt;',
  'before_title' =&gt; '&lt;h3 class="widget-title"&gt;',
  'after_title' =&gt; '&lt;/h3&gt;'
) );
</code></pre>

This should display the newly created widget in your WordPress back-end. To make sure that it actually pops up on the site, you need to add the following line of code to your 404 page in the appropriate place:

<pre><code class="language-php">&lt;?php dynamic_sidebar( '404' ); ?&gt;</code></pre>

In my case, I want to replace the search form (<code>&lt;?php get_search_form(); ?&gt;</code>) inside the template with my new widget, making for the following code:

<pre><code class="language-php">
&lt;?php
/**
 * The template for displaying 404 pages (Not Found)
 *
 * @package WordPress
 * @subpackage Twenty_Twelve
 * @since Twenty Twelve 1.0
 */

get_header(); ?&gt;

&lt;div id="primary" class="site-content"&gt;
  &lt;div id="content" role="main"&gt;

    &lt;article id="post-0" class="post error404 no-results not-found"&gt;
      &lt;header class="entry-header"&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php _e( 'This is somewhat embarrassing, isn&amp;amp;rsquo;t it?', 'twentytwelve' ); ?&gt;&lt;/h1&gt;
      &lt;/header&gt;

      &lt;div class="entry-content"&gt;
        &lt;?php dynamic_sidebar( '404' ); ?&gt;
      &lt;/div&gt;&lt;!-- .entry-content --&gt;
    &lt;/article&gt;&lt;!-- #post-0 --&gt;

  &lt;/div&gt;&lt;!-- #content --&gt;
&lt;/div&gt;&lt;!-- #primary --&gt;

&lt;?php get_footer(); ?&gt;
</code></pre>

After uploading the template to my site, it's time to populate my new widget area:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a2e635d-37e5-4422-8760-050d6c3e3026/07-404-page-template-widgets-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9bb14ae-70cc-40b0-b0ca-c6985b9f19d6/07-404-page-template-widgets-opt-small.jpg" alt="404 page template widget." /></a><figcaption>404 page template widget. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a2e635d-37e5-4422-8760-050d6c3e3026/07-404-page-template-widgets-opt.jpg">View large version</a>)</figcaption></figure>

If I now take a look at the 404 error page, my newly created widgets show up there:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fac08e93-e18d-48cf-bb37-aa4f9f6e4c75/08-customized-404-error-page-via-template-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ab51106-bdca-4e51-9e81-7edb45a7efc3/08-customized-404-error-page-via-template-opt-small.jpg" alt="Customized 404 page." /></a><figcaption>Customized 404 page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fac08e93-e18d-48cf-bb37-aa4f9f6e4c75/08-customized-404-error-page-via-template-opt.jpg">View large version</a>)</figcaption></figure>

### 3. Page Template For Displaying Custom Post Types

Custom post types are a great way to introduce content that has its own set of data points, design and other customizations. A favorite use case for these post types are review items such as books and movies. In our case we want to build a page template that shows portfolio items.

We first need to create our custom post type (CPT). This can be done manually or via plugin. One plugin option I can wholeheartedly recommend is <a href="https://wordpress.org/plugins/types/">Types</a>. It lets you easily create custom post types and custom fields.

Install and activate Types, add a custom post, make sure its slug is 'portfolio', customize any fields you need (such as adding a featured image), adjust any other options, and save.

Now, that we have our portfolio post type, we want it to show up on our site. The first thing we'll do is create the page in question. Be aware that if you chose 'portfolio' as the slug of your CPT, the page can not have the same slug. I went with my <code>clients-portfolio</code> and also added some example text.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/738ba7ff-64a7-4c73-9b01-ea15b4c42326/09-portfolio-page-without-custom-page-template-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb5c94ba-cfb7-4561-8abe-6b7041308c2a/09-portfolio-page-without-custom-page-template-opt-small.jpg" alt="Portfolio page without a custom page template." /></a><figcaption>Portfolio page without a custom page template. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/738ba7ff-64a7-4c73-9b01-ea15b4c42326/09-portfolio-page-without-custom-page-template-opt.jpg">View large version</a>)</figcaption></figure>

After adding a few items in the 'portfolio' post type section, we want them to show up on our page right underneath the page content.

To achieve this we will again use a derivative of the <em>page.php</em> file. Copy it, call it <em>portfolio-template.php</em> and change the header to this:

<pre><code class="language-php">
&lt;?php
/*
 * Template Name: Portfolio Template
 * description: >-
  Page template to display portfolio custom post types 
 * underneath the page content
 */
 </code></pre>

However, in this case we will have to make a few changes to the original template. When you take a look at the code of <em>page.php</em>, you will see that it calls another template file in the middle, named <em>content-page.php</em> (where it says <code>&lt;?php get_template_part( 'content', 'page' ); ?&gt;</code>). In that file we find the following code:

<pre><code class="language-php">
&lt;article id="post-&lt;?php the_ID(); ?&gt;" &lt;?php post_class(); ?&gt;&gt;
  &lt;header class="entry-header"&gt;
    &lt;?php if ( ! is_page_template( 'page-templates/front-page.php' ) ) : ?&gt;
    &lt;?php the_post_thumbnail(); ?&gt;
    &lt;?php endif; ?&gt;
    &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
  &lt;/header&gt;

  &lt;div class="entry-content"&gt;
    &lt;?php the_content(); ?&gt;
    &lt;?php wp_link_pages( array( 'before' =&gt; '&lt;div class="page-links"&gt;' . __( 'Pages:', 'twentytwelve' ), 'after' =&gt; '&lt;/div&gt;' ) ); ?&gt;
  &lt;/div&gt;&lt;!-- .entry-content --&gt;
  &lt;footer class="entry-meta"&gt;
    &lt;?php edit_post_link( __( 'Edit', 'twentytwelve' ), '&lt;span class="edit-link"&gt;', '&lt;/span&gt;' ); ?&gt;
  &lt;/footer&gt;&lt;!-- .entry-meta --&gt;
&lt;/article&gt;&lt;!-- #post --&gt;
</code></pre>

As you can see, it is here that the page title and content are called. Since we definitely want those on our portfolio site, we will need to copy the necessary parts of this template to our <em>page.php</em> file. The result looks like this:

<pre><code class="language-php">get_header(); ?&gt;

&lt;div id="primary" class="site-content"&gt;
  &lt;div id="content" role="main"&gt;

    &lt;?php while ( have_posts() ) : the_post(); ?&gt;
      &lt;header class="entry-header"&gt;
        &lt;?php the_post_thumbnail(); ?&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
      &lt;/header&gt;

      &lt;div class="entry-content"&gt;
        &lt;?php the_content(); ?&gt;
      &lt;/div&gt;&lt;!-- .entry-content --&gt;

      &lt;?php comments_template( ’, true ); ?&gt;
    &lt;?php endwhile; // end of the loop. ?&gt;

  &lt;/div&gt;&lt;!-- #content --&gt;
&lt;/div&gt;&lt;!-- #primary --&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;
</code></pre>

To get the portfolio items onto our page, we will add the following code right beneath the <code>the_content()</code> call.</p>

<pre><code class="language-php">
&lt;?php
  $args = array(
    'post_type' =&gt; 'portfolio', // enter custom post type
    'orderby' =&gt; 'date',
    'order' =&gt; 'DESC',
  );

  $loop = new WP_Query( $args );
  if( $loop-&gt;have_posts() ):
  while( $loop-&gt;have_posts() ): $loop-&gt;the_post(); global $post;
    echo '&lt;div class="portfolio"&gt;';
    echo '&lt;h3&gt;' . get_the_title() . '&lt;/h3&gt;';
    echo '&lt;div class="portfolio-image"&gt;'. get_the_post_thumbnail( $id ).'&lt;/div&gt;';
    echo '&lt;div class="portfolio-work"&gt;'. get_the_content().'&lt;/div&gt;';
    echo '&lt;/div&gt;';
  endwhile;
  endif;
?&gt;
</code></pre>

This will make the CPT show up on the page:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/562767a8-545b-4197-b95c-3b1662ae2f46/10-custom-portfolio-template-without-styling-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c4796e5-f415-4d43-87f0-74037d957258/10-custom-portfolio-template-without-styling-opt-small.jpg" alt="The custom portfolio template." /></a><figcaption>The custom portfolio template. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/562767a8-545b-4197-b95c-3b1662ae2f46/10-custom-portfolio-template-without-styling-opt.jpg">View large version</a>)</figcaption></figure>

I'm sure we all agree that it looks less than stellar, so some styling is in order.</p>

<pre><code class="language-css">
/* Portfolio posts */

.portfolio {
  -webkit-box-shadow: 0px 2px 2px 0px rgba(50, 50, 50, 0.75);
  -moz-box-shadow:    0px 2px 2px 0px rgba(50, 50, 50, 0.75);
  box-shadow:         0px 2px 2px 0px rgba(50, 50, 50, 0.75);
  margin: 0 0 20px;
  padding: 30px;
}
.portfolio-image {
  display: block;
  float: left;
  margin: 0 10px 0 0;
  max-width: 20%;
}
.portfolio-image img {
  border-radius: 0;
}
.portfolio-work {
  display: inline-block;
  max-width: 80%;
}
.portfolio h3{
  border-bottom: 1px solid #999;
  font-size: 1.57143rem;
  font-weight: normal;
  margin: 0 0 15px;
  padding-bottom: 15px;
}
</code></pre>

Much better, don't you think?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/615356ff-f8ab-4280-87a0-a8bbefbbafd3/11-custom-portfolio-template-including-styling-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d6a1dca-14de-4c09-828d-6ecb9cd5b1c2/11-custom-portfolio-template-including-styling-opt-small.jpg" alt="The custom portfolio template with styling." /></a><figcaption>The custom portfolio template with styling. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/615356ff-f8ab-4280-87a0-a8bbefbbafd3/11-custom-portfolio-template-including-styling-opt.jpg">View large version</a>)</figcaption></figure>

And here is the entire code for the portfolio page template:

<pre><code class="language-php">
&lt;?php
/*
 * Template Name: Portfolio Template
 * description: >-
  Page template to display portfolio custom post types 
 * underneath the page content
 */

get_header(); ?&gt;

&lt;div id="primary" class="site-content"&gt;
  &lt;div id="content" role="main"&gt;

    &lt;?php while ( have_posts() ) : the_post(); ?&gt;

      &lt;header class="entry-header"&gt;
        &lt;?php the_post_thumbnail(); ?&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
      &lt;/header&gt;

      &lt;div class="entry-content"&gt;
        &lt;?php the_content(); ?&gt;
        &lt;?php
          $args = array(
            'post_type' =&gt; 'portfolio', // enter custom post type
            'orderby' =&gt; 'date',
            'order' =&gt; 'DESC',
          );

          $loop = new WP_Query( $args );
          if( $loop-&gt;have_posts() ):
          while( $loop-&gt;have_posts() ): $loop-&gt;the_post(); global $post;
            echo '&lt;div class="portfolio"&gt;';
            echo '&lt;h3&gt;' . get_the_title() . '&lt;/h3&gt;';
            echo '&lt;div class="portfolio-image"&gt;'. get_the_post_thumbnail( $id ).'&lt;/div&gt;';
            echo '&lt;div class="portfolio-work"&gt;'. get_the_content().'&lt;/div&gt;';
            echo '&lt;/div&gt;';
          endwhile;
          endif;
        ?&gt;
      &lt;/div&gt;&lt;!-- #entry-content --&gt;
      &lt;?php comments_template( ’, true ); ?&gt;               
    &lt;?php endwhile; // end of the loop. ?&gt;                
  &lt;/div&gt;&lt;!-- #content --&gt;
&lt;/div&gt;&lt;!-- #primary --&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;
</code></pre>

### 4. Contributor Page With Avatar images

Next up in our page template use cases is a contributor page. We want to set up a list of authors on our website, including their images and the number of posts they have published under their name. The end result will look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e302793f-6944-4a60-adb6-1cec393a22bb/12-custom-contributor-page-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4312d905-242b-455b-96ff-79773fd0cb13/12-custom-contributor-page-opt-small.jpg" alt="The completed custom contributors page." /></a><figcaption>The completed custom contributors page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e302793f-6944-4a60-adb6-1cec393a22bb/12-custom-contributor-page-opt.jpg">View large version</a>)</figcaption></figure>

We will again start out with our hybrid file from before and add the code for the contributor list to it. But what if you don't know how to create such a thing? No worries, you can get by with intelligent stealing.

You see, the Twenty Fourteen default theme comes with a contributor page by default. You can find its template in the <em>page-templates</em> folder with the name <em>contributors.php</em>.

When looking into the file, however, you will only find the following call in there: <code>twentyfourteen_list_authors();</code>. Luckily, as an avid WordPress user you now conclude that this probably refers to a function in Twenty Fourteen's <em>function.php</em> file and you would be right.

From what we find in there, the part that interests us is this:

<pre><code class="language-php">
&lt;?php
// Output the authors list.
$contributor_ids = get_users( array(
  'fields'  =&gt; 'ID',
  'orderby' =&gt; 'post_count',
  'order'   =&gt; 'DESC',
  'who'     =&gt; 'authors',
));

foreach ( $contributor_ids as $contributor_id ) :
$post_count = count_user_posts( $contributor_id );
  // Move on if user has not published a post (yet).
  if ( ! $post_count ) {
    continue;
  }
?&gt;

&lt;div class="contributor"&gt;
  &lt;div class="contributor-info"&gt;
    &lt;div class="contributor-avatar"&gt;&lt;?php echo get_avatar( $contributor_id, 132 ); ?&gt;&lt;/div&gt;
    &lt;div class="contributor-summary"&gt;
      &lt;h2 class="contributor-name"&gt;&lt;?php echo get_the_author_meta( 'display_name', $contributor_id ); ?&gt;&lt;/h2&gt;
      &lt;p class="contributor-bio"&gt;
        &lt;?php echo get_the_author_meta( 'description', $contributor_id ); ?&gt;
      &lt;/p&gt;
      &lt;a class="button contributor-posts-link" href="&lt;?php echo esc_url( get_author_posts_url( $contributor_id ) ); ?&gt;"&gt;
        &lt;?php printf( _n( '%d Article', '%d Articles', $post_count, 'twentyfourteen' ), $post_count ); ?&gt;
      &lt;/a&gt;
    &lt;/div&gt;&lt;!-- .contributor-summary --&gt;
  &lt;/div&gt;&lt;!-- .contributor-info --&gt;
&lt;/div&gt;&lt;!-- .contributor --&gt;

&lt;?php
endforeach;
?&gt;
</code></pre>

We will again add it below the call for <code>the_content()</code> with the following result:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8376169f-58d7-42b5-8d9e-4e2557790114/13-custom-contributor-page-without-styling-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa6738f8-f6a2-445c-abc2-23eec7c07097/13-custom-contributor-page-without-styling-opt-small.jpg" alt="The unstyled custom contributors page." /></a><figcaption>The unstyled custom contributors page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8376169f-58d7-42b5-8d9e-4e2557790114/13-custom-contributor-page-without-styling-opt.jpg">View large version</a>)</figcaption></figure>

Now for a little bit of styling:

<pre><code class="language-css">
/* Contributor page */

.contributor {
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing:      border-box;
  display: inline-block;
  padding: 48px 10px;
}
.contributor p {
  margin-bottom: 1rem;
}
.contributor-info {
  margin: 0 auto 0 168px;
}
.contributor-avatar {
  border: 1px solid rgba(0, 0, 0, 0.1);
  float: left;
  line-height: 0;
  margin: 0 30px 0 -168px;
  padding: 2px;
}
.contributor-avatar img{
  border-radius: 0;
}
.contributor-summary {
  float: left;
}
.contributor-name{
  font-weight: normal;
  margin: 0 !important;
}
.contributor-posts-link {
  background-color: #24890d;
  border: 0 none;
  border-radius: 0;
  color: #fff;
  display: inline-block;
  font-size: 12px;
  font-weight: 700;
  line-height: normal;
  padding: 10px 30px 11px;
  text-transform: uppercase;
  vertical-align: bottom;
}
.contributor-posts-link:hover {
  color: #000;
  text-decoration: none;
}</code></pre>

And that should be it. Thanks Twenty Fourteen!

### 5. Customized Archive Page

Twenty Twelve comes with its own template for archive pages. It will jump into action, for example, when you attempt to view all past posts from a certain category.

However, I want something a little more like what <a href="https://www.problogger.net/archives/">Problogger</a> has done: a page that lets people discover additional content on my site in several different ways. That, again, is done with a page template.

Staying with our mixed template from before, we will add the following below the <code>the_content()</code> call:

<pre><code class="language-php">
&lt;div class="archive-search-form"&gt;&lt;?php get_search_form(); ?&gt;&lt;/div&gt;

&lt;h2&gt;Archives by Year:&lt;/h2&gt;
&lt;ul&gt;&lt;?php wp_get_archives('type=yearly'); ?&gt;&lt;/ul&gt;

&lt;h2&gt;Archives by Month:&lt;/h2&gt;
&lt;ul&gt;&lt;?php wp_get_archives('type=monthly'); ?&gt;&lt;/ul&gt;

&lt;h2&gt;Archives by Subject:&lt;/h2&gt;
&lt;ul&gt; &lt;?php wp_list_categories('title_li='); ?&gt;&lt;/ul&gt;
</code></pre>

Plus, a little bit of styling for the search bar:

<pre><code class="language-css">
.archive-search-form {
  padding: 10px 0;
  text-align: center;
}
</code></pre>

And the result should look a little bit like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/486ba4bc-0fb2-4441-9beb-ee9af975ff4c/14-custom-archive-page-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce07d9a6-51b3-418d-81cc-c8752bfd71e6/14-custom-archive-page-opt-small.jpg" alt="The custom archive page." /></a><figcaption>The custom archive page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/486ba4bc-0fb2-4441-9beb-ee9af975ff4c/14-custom-archive-page-opt.jpg">View large version</a>)</figcaption></figure>

For completion's sake, here is the entire file:

<pre><code class="language-php">
&lt;?php
/**
 * Template Name: Custom archive template
 *
 */

get_header(); ?&gt;

&lt;div id="primary" class="site-content"&gt;
  &lt;div id="content" role="main"&gt;

    &lt;?php while ( have_posts() ) : the_post(); ?&gt;

      &lt;header class="entry-header"&gt;
        &lt;?php the_post_thumbnail(); ?&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
      &lt;/header&gt;

      &lt;div class="entry-content"&gt;
        &lt;?php the_content(); ?&gt;

        &lt;div class="archive-search-form"&gt;&lt;?php get_search_form(); ?&gt;&lt;/div&gt;

        &lt;h2&gt;Archives by Year:&lt;/h2&gt;
        &lt;ul&gt;&lt;?php wp_get_archives('type=yearly'); ?&gt;&lt;/ul&gt;

        &lt;h2&gt;Archives by Month:&lt;/h2&gt;
        &lt;ul&gt;&lt;?php wp_get_archives('type=monthly'); ?&gt;&lt;/ul&gt;

        &lt;h2&gt;Archives by Subject:&lt;/h2&gt;
        &lt;ul&gt;&lt;?php wp_list_categories('title_li='); ?&gt;&lt;/ul&gt;
      &lt;/div&gt;&lt;!-- #entry-content --&gt;

      &lt;?php comments_template( ’, true ); ?&gt;               
    &lt;?php endwhile; // end of the loop. ?&gt;             
  &lt;/div&gt;&lt;!-- #content --&gt;
&lt;/div&gt;&lt;!-- #primary --&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;
</code></pre>

Don't forget to assign it to a page!

## WordPress Page Templates In A Nutshell

On your way to mastering WordPress, learning to use page templates is an important step. They can make customizing your website very, very easy and allow you to assign unique functionality and design to as many or few pages as you wish. From adding widget areas to showing custom post types to displaying a list of your website's contributors — the possibilities are practically endless.

Whether you use conditional tags, exploit the WordPress template hierarchy, or create page-specific template files is entirely up to you and what you are trying to achieve. <strong>Start off small and work your way up to more complicated things</strong>. It won't be long before every part of your WordPress website will answer to your every call.</p>

<em>Do you have experience using page templates in WordPress? What other use cases can you add to the list? Any important details to add? Please tell us about it in the comments.</em>

<em>Image credit: <a href="https://pixabay.com/en/users/kpgolfpro-27707/">Kevin Phillips</a></em>

{{< signature "og, ml" >}}


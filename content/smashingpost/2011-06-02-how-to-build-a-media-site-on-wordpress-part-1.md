---
title: 'How To Build A Media Site On WordPress'
slug: how-to-build-a-media-site-on-wordpress-part-1
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/278956f7-956a-4bfc-b852-f26748ca01d0/wordpress-17.gif
date: 2011-06-02T14:04:15.000Z
author: jonathan-wold
summary: >-
  With the introduction of WordPress 3.1, several new features were added that make using WordPress to manage media even more practical. In this article, Jonathan Wold shows you how to setup custom post types and custom taxonomies, without plugins.
description: >-
  With the introduction of WordPress 3.1, several new features were added that make using WordPress to manage media even more practical. Jonathan Wold shows you how to setup custom post types and custom taxonomies, without plugins.
categories:
  - WordPress
  - PHP
  - Social Media
---

WordPress is amazing. With its growing popularity and continual development, it is becoming the tool of choice for many designers and developers. WordPress projects, though, are pushing well beyond the confines of mere “posts” and “pages”. How do you go about adding and organizing media and all its complexities? With the introduction of WordPress 3.1, several new features were added that make using WordPress to manage media even more practical and in this tutorial, we’re going to dive in and show you how.

In part one, we’re going to setup custom post types and custom taxonomies, without plugins. After that, we’ll build a template to check for and display media attached to custom posts. Then, in part two, we’ll use custom taxonomy templates to organize and relate media (and other types of content).

As we focus on building a media centric site, I also want you to see that the principles taught in this series offer you a set of tools and experience to build interfaces for and organize many different types of content. Examples include:

{{% feature-panel %}}

*   A “Media” center, of any type, added to an existing WordPress site
*   A repository of videos, third party hosted (e.g. Vimeo, YouTube, etc), organized by topics and presenters
*   A music site, with streaming and song downloads, organized by bands and associated by albums
*   An author-driven Q&A site, with user submitted questions organized by topics and geographical location
*   A recipe site with videos and visitor ratings, organized by category and shared ingredients

In a future tutorial, we will focus on customizing the WordPress backend (with clients especially in mind) to manage a media site and in another tutorial we will use the foundation laid to build a dynamic filtering interface that allows visitors to quickly sort their way through hundreds or even thousands of custom posts.

### Requirements

*   **WordPress 3.1** - With the release of 3.1, several new features related to the use of custom post types and taxonomies were introduced that are essential to the techniques taught in this series.
*   **Basic Familiarity with PHP** (or “No Fear”) - To move beyond copying and pasting the examples I’ve given will require a basic familiarity with PHP or, at least, a willingness to experiment. If the code samples below are intimidating to you and you have the desire to learn, then I encourage you to tackle it and give it your best. If you have questions, ask in the comments.

### Working Example

In April, 2011 we (Sabramedia, of which I am a co-founder) worked with an organization in Southern California to develop a resource center on WordPress to showcase their paid and free media products. On the front-end, we built a jQuery powered filtering interface to allow visitors to filter through media on-page. We’ll cover the ins and outs of building a similar interface in part three.

<figure><img loading="lazy" decoding="async" class="98667" title="ARISE Resource Center" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f17e8986-984e-47c5-947a-e64de3d979df/screenshot-arise-illu.jpg" alt="ARISE Resource Center" width="500" /><figcaption>The “Resource Center” on ARISE, with a custom taxonomy filter (“David Asscherick”) pre-selected.</figcaption></figure>

## Working With Custom Post Types

By default, WordPress offers two different types of posts for content. First, you have the traditional “post”, used most often for what WordPress is known best for - blogging. Second, you have “pages”. Each of these, as far as WordPress is concerned, is a type of “post”. A *custom* post type is a type of post that you define.
<blockquote><strong>Note:</strong> You can learn more about <a href="https://wordpress.org/support/article/post-types/">post types</a> on the WordPress Codex.</blockquote>

In this series, we are going to use custom post types to build a media based resource center. I will be defining and customizing a post type of “resource”.

### Setting Up Your Custom Post Type

You can setup your custom post types by code or by plugin. In these examples, I will be setting up the post type by code, storing and applying the code directly in the functions file on the default WordPress theme, <a href="https://wordpress.org/extend/themes/twentyten">Twenty Ten</a>. You can follow along by using a plugin to setup the post types for you or by copying the code samples into the bottom of your theme’s custom functions file (functions.php).
<blockquote><strong>Note: </strong>As a best practice, unless you use an existing plugin to create the post types, you may want to consider <a href="https://justintadlock.com/archives/2011/02/02/creating-a-custom-functions-plugin-for-end-users">creating your own WordPress plugin</a>. Setting up custom post types and taxonomies separate from your theme becomes important if and when you want to make major changes to your theme or try a new theme out. Want to save some typing? Use the <a href="https://themergency.com/generators/wordpress-custom-post-types/">custom post code generator</a>.</blockquote>

Alright, let’s setup our custom post type. Paste the following code into your theme’s functions.php:

<pre><code class="language-php">add_action('init', 'register_rc', 1); // Set priority to avoid plugin conflicts

function register_rc() { // A unique name for our function
  $labels = array( // Used in the WordPress admin
    'name' =&gt; _x('Resources', 'post type general name'),
    'singular_name' =&gt; _x('Resource', 'post type singular name'),
    'add_new' =&gt; _x('Add New', 'Resource'),
    'add_new_item' =&gt; __('Add New Resource'),
    'edit_item' =&gt; __('Edit Resource'),
    'new_item' =&gt; __('New Resource'),
    'view_item' =&gt; __('View Resource '),
    'search_items' =&gt; __('Search Resources'),
    'not_found' =&gt;  __('Nothing found'),
    'not_found_in_trash' =&gt; __('Nothing found in Trash')
  );
  $args = array(
    'labels' =&gt; $labels, // Set above
    'public' =&gt; true, // Make it publicly accessible
    'hierarchical' =&gt; false, // No parents and children here
    'menu_position' =&gt; 5, // Appear right below "Posts"
    'has_archive' =&gt; 'resources', // Activate the archive
    'supports' =&gt; array('title','editor','comments','thumbnail','custom-fields'),
  );
  register_post_type( 'resource', $args ); // Create the post type, use options above
}</code></pre>

The code above tells WordPress to “register” a post type called “resource”. Then, we pass in our options, letting WordPress know that we want to use our own labels, that we want our post type to be publicly accessible, non-hierarchal, and that we want it to show up right below “posts” in our admin menu. Then, we activate the “archive” feature, new in WordPress 3.1. Finally, we add in “supports”: the default title field, the WordPress editor, comments, featured thumbnail, and custom fields (I’ll explain that later).
<blockquote><strong>Note:</strong> For more information on setting up the post type and for details on all the options you have (there are quite a few available), refer to the <a href="https://developer.wordpress.org/reference/functions/register_post_type/">register_post_type function reference</a> on the WordPress Codex.</blockquote>

If the code above was successful, you will see a new custom post type, appearing below “Posts” in the WordPress admin menu. It will look something like this:

<figure><img class="98884 " title="WordPress Admin, after adding a custom post" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f93d73c-a1f9-40a9-b73a-fbb744cbdd9f/wordpress-screenshot-admin.jpg" alt="Screenshot" width="550" height="225" /><figcaption>A view of the WordPress Admin, after adding a custom post type.</figcaption></figure>

We’re in good shape! Next, let’s setup our custom taxonomies.

## Working With Custom Taxonomies

A “taxonomy” is a way of organizing and relating information. WordPress offers two default taxonomies, categories and tags. Categories are hierarchal (they can have sub-categories) and are often used to organize content on a more broad basis. Tags, are non-hierarchal (no sub-tags) and are often used to organize content across categories.

A “term” is an entry within a taxonomy. For a custom taxonomy of “Presenters”, “John Smith” would be a term within that taxonomy.

In this series, we will be creating two different custom taxonomies to organize the content within our resource center.

*   Presenters - Each media item in our resource center will have one or more presenters. For each presenter, we want to know their name and we want to include a short description. Presenters will be non-hierarchal.
*   Topics - Our resource center will offer media organized by topics. Topics will be hierarchal, allowing for multiple sub-topics and even sub-sub-topics.

<blockquote><strong>Note:</strong> Interested in working with more than the title and short description? Take a look at <a href="https://sabramedia.com/blog/how-to-add-custom-fields-to-custom-taxonomies">How To Add Custom Fields To Custom Taxonomies</a> on the Sabramedia blog.</blockquote>

### Setting Up Presenters

Our goal with presenters is to create a presenter profile, referenced on the respective media pages, that will give more information about the presenter and cross-reference other resources that they are associated with.

Add the following code to your theme’s functions.php file:

<pre><code class="language-php">$labels_presenter = array(
  'name' =&gt; _x( 'Presenters', 'taxonomy general name' ),
  'singular_name' =&gt; _x( 'Presenter', 'taxonomy singular name' ),
  'search_items' =&gt;  __( 'Search Presenters' ),
  'popular_items' =&gt; __( 'Popular Presenters' ),
  'all_items' =&gt; __( 'All Presenters' ),
  'edit_item' =&gt; __( 'Edit Presenter' ),
  'update_item' =&gt; __( 'Update Presenter' ),
  'add_new_item' =&gt; __( 'Add New Presenter' ),
  'new_item_name' =&gt; __( 'New Presenter Name' ),
  'separate_items_with_commas' =&gt; __( 'Separate presenters with commas' ),
  'add_or_remove_items' =&gt; __( 'Add or remove presenters' ),
  'choose_from_most_used' =&gt; __( 'Choose from the most used presenters' )
);

register_taxonomy(
  'presenters', // The name of the custom taxonomy array( 'resource' ), // Associate it with our custom post type array(
    'rewrite' =&gt; array( // Use "presenter" instead of "presenters" in the permalink
      'slug' =&gt; 'presenter'
      ),
    'labels' =&gt; $labels_presenter
    )
  );</code></pre>

Let’s break that down. First, we setup the labels to be used when we “register” our taxonomy. Then, we give it a name, in this case “presenters”, and assign it to the post type of “resource”. If you had multiple post types, you would add them in with a comma, like this:

<code>array( 'resource', 'other-type' ), // Associate it with our custom post types</code>

After that, we change the URL (or “permalink”) to satisfy our desire for grammatical excellence. Rather than being “/presenters/presenter-name” we update the “slug” (<a href="https://wordpress.org/support/article/glossary/">what is a slug?</a>) to remove the “s” so that the permalink will read “/presenter/presenter-name”.

In our example, you should now notice a new menu option labeled “Presenters” under “Resources” in the admin sidebar. When you go to create a new resource you should also notice a meta box on the right side that looks like this:

<figure><img class="98885 " title="WordPress Admin, showing &quot;Presenters&quot; taxonomy" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70a192a0-4d01-4c24-a687-c8b1f5110918/meta-box-wp-admin1.jpg" alt="Screenshot" width="549" /><figcaption>My custom taxonomy of “Presenters” now shows up between the “Publish” box and “Featured Image”.</figcaption></figure>

<blockquote><strong>Note:</strong> To learn more about setting up custom taxonomies and the options available, take a look at the <a href="https://developer.wordpress.org/reference/functions/register_taxonomy/">register_taxonomy function reference</a> on the WordPress Codex.</blockquote>

### Setting Up Topics

Our goal with topics is to allow for a hierarchal set of topics and sub-topics, each with their own page, showing the resources that are associated with each respective topic.

Add the following code to your theme’s functions.php file:

<pre><code class="language-php">$labels_topics = array(
  'name' =&gt; _x( 'Topics', 'taxonomy general name' ),
  'singular_name' =&gt; _x( 'Topic', 'taxonomy singular name' ),
  'search_items' =&gt;  __( 'Search Topics' ),
  'all_items' =&gt; __( 'All Topics' ),
  'parent_item' =&gt; __( 'Parent Topic' ),
  'parent_item_colon' =&gt; __( 'Parent Topic:' ),
  'edit_item' =&gt; __( 'Edit Topic' ),
  'update_item' =&gt; __( 'Update Topic' ),
  'add_new_item' =&gt; __( 'Add New Topic' ),
  'new_item_name' =&gt; __( 'New Topic Name' ),
);

register_taxonomy(
  'topics', // The name of the custom taxonomy array( 'resource' ), // Associate it with our custom post type array(
    'hierarchical' =&gt; true,
    'rewrite' =&gt; array(
      'slug' =&gt; 'topic', // Use "topic" instead of "topics" in permalinks
      'hierarchical' =&gt; true // Allows sub-topics to appear in permalinks
      ),
    'labels' =&gt; $labels_topics
    )
  );</code></pre>

That was easy enough! The code above is similar to setting up presenters, except this time we are using a few different labels, specific to hierarchal taxonomies. We set hierarchal to true (it’s set to “false” by default), we update the slug to be singular instead of plural, then, just before referencing our labels, we set the rewriting to be hierarchal. A hierarchal rewrite allows permalinks that look like this: /topic/topic-name/sub-topic-name.

With the above code implemented, you should notice another option below “Resources” in the WordPress admin and a new meta box that looks like this:

<figure><img class="98888 " title="WordPress Admin with &quot;Topics&quot; added in" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16859878-4f82-4b31-a0ad-26ae753c22ed/tutorial-admin-4.png" alt="Screenshot" width="550" height="265" /><figcaption>My custom taxonomy of “Topics” now shows up, albeit a bit empty looking, below “Presenters”.</figcaption></figure>

## Adding Custom Fields To Custom Post Types

In many cases, the “title” and “editor” (the default content editor in WordPress) aren’t going to be enough. What if you want to store extra information about a particular custom post? Examples might include:

*   Duration of a media file - HH:MM:SS format, useful to pre-populate your media player with the duration on page load.
*   Original recording date - Stored as a specific date with day, month, and year.

We call this “meta” information and it is a set of details that are *specific* to the individual item and usually make the most sense to store as meta data, as opposed to terms within a custom taxonomy. While you could put all these details in the “editor” field, it gives you very little flexibility with how this is displayed within your template.

So, let’s **setup some custom fields**. Use the custom fields interface at the bottom of an individual custom post to add some extra details about your custom post.

For our example, we’re going to add two fields. For each field, I will list the name, then an example value:

*   **recording_length** - Example: 00:02:34
*   **recording_date** - Example: March 16, 2011

Here’s how that looks after adding two custom fields:

<figure><img class="98892" title="WordPress Admin, with two custom fields added" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/371ba827-6f2a-4a7f-bb1c-74b498b817f4/tutorial-admin-5.png" alt="Screenshot" width="550" height="289" /><figcaption>An example of the custom fields interface after adding two “keys” and their respective “values”.</figcaption></figure>

<blockquote><strong>Note:</strong> The default custom fields interface can be a bit limiting. If you’d like to make use of a plugin, try More Fields. The functionality is the same (just be mindful of what you name your custom fields) - a plugin typically offers you a better interface. If you want to build your own interface, take a look at <a href="https://www.farinspace.com/wpalchemy-metabox/">WP Alchemy</a>. To learn more about using custom fields, take a look at <a href="https://wordpress.org/support/article/custom-fields/">using custom fields</a> on the WordPress Codex.</blockquote>

{{% ad-panel-leaderboard %}}

### Custom Taxonomies vs. Custom Fields

At this point, you may run into a situation where you’re uncertain whether a particular piece of information should be stored as a custom taxonomy or as a custom field. Let’s use the recording date as an example. If we were to log the complete date, then it would probably make the most sense to store it within a custom field on the individual item. If we were to just use the year, though, we could store it as a term within a custom taxonomy (we’d probably call it “year”) and use it to show other resources recorded that same year.

The question is whether or not you want to relate content (in our case, “resources”) by the information you’re considering. If you don’t see any need to relate content (and don’t have plans to) then a custom field is the way to go. If you have a need to relate content or see a potential need down the road, then a custom taxonomy is the way to go.

## Media Storage - WordPress vs. Third Party

Now that we have our custom post type and custom taxonomies in place, it’s time to upload some media. Our goal is to make this as simple a process for the end-user as possible. There are two ways that we can manage the media, either directly within WordPress or via third party.

*   **WordPress Managed** - WordPress has a media management system built-in. You can upload media directly from your post type interface or from the “media” section in the WordPress admin. If storage or bandwidth becomes an issue, you can use a plugin (such as [WP Super Cache](https://wordpress.org/extend/plugins/wp-super-cache/)) to offload the storage of the media to a third party content delivery network (CDN) to optimize delivery speed and save on bandwidth.
*   **Third Party** - Going this route, you can use a media hosting service like [YouTube](https://youtube.com), [Vimeo](https://vimeo.com), [Scribd](https://scribd.com) (PDFs), [Issuu](https://issuu.com) (ebooks), or any media hosting service that offers you an embed option.

Going the internal route, the media is stored inside of WordPress and associated with the individual custom post. We then access it as an attachment within the template. Going the third party route, we get the embed code (or the media ID) and store it inside of WordPress within a custom field. We’ll look at examples of both options further on.
<blockquote><strong>Note:</strong> Working with images? Take a look at a recent Smashing article that covers <a href="https://www.smashingmagazine.com/2011/05/26/better-image-management-practices-with-wordpress/">better image management with WordPress</a>.</blockquote>

## Preparing The Stage - Adding New Media

We’re about to start working with the templates. Before we do that, though, we need to have some media to work with within our new custom post type. Before proceeding, make sure you’ve done the following:

*   Create a new “resource” post (or whatever your post type may be) and give it a title and a description in the main content editor.
*   Associate your resource with a non-hierarchical custom taxonomy you’ve created (e.g. A presenter named “Jonathan Wold”).
*   Associate your resource with a hierarchical custom taxonomy you’ve created (e.g. A topic of “Family” and a sub-topic of “Children”)
*   Add one or more custom fields with a unique “key” and “value” (e.g. a key of “recording_duration” and a value of “00:02:34”).
*   Upload a video file to your custom post using the WordPress media manager (click the “video” icon just below the title field and right above the editor).

<blockquote><strong>Note: </strong>If you’re hosting your videos via third party, create a custom field to hold either the entire embed code or the ID of the video. I’ll give you an example using Vimeo a bit later that will use the video ID.</blockquote>

<blockquote><strong>Note #2:</strong> Depending on your hosting provider, you may run into trouble with a default upload limit, often 2MB or 8MB. Check out how to <a href="https://www.wordimpressed.com/coding/how-to-increase-wordpress-file-upload-size-correctly/">increase the WordPress upload limit</a>.</blockquote>

After you’ve created a new post, previewing it should show you a screen, depending on your theme, will look something like this:

<figure><img class="101163" title="Twenty Ten, default front end" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76fa5449-b085-428f-9c24-859e29955b74/tutorial-frontend-1.png" alt="Screenshot" width="550" height="192" /><figcaption>A preview of my custom post, displaying title and description, on the Twenty Ten theme.</figcaption></figure>

<blockquote><strong>Note: </strong>If you preview your post and get a “404" error, you may need to update your Permalinks. From the WordPress Admin, Go to “Settings", then “Permalinks", and click “Save Changes". Refresh and you should be good to go.</blockquote>

## Displaying Our Media - Working With Custom Post Templates

If you previewed your custom post, you probably saw something similar to what I showed in my example - not much. Where are the custom taxonomy terms, custom fields, and videos? Missing - but not for long! In the following steps, we’re going to create a custom template that tells WordPress what data to display and how to display it.

### Creating A Custom Post Type Template

The WordPress template engine has a hierarchy that it follows when deciding what theme template it uses to display data associated with a post. In the case of our “resource” post type, the WordPress hierarchy (as of 3.1) is as follows:

*   **single-resource.php** - WordPress will check the theme folder for a file named single-resource.php, if it exists, it will use that file to display the content. For different post types, simple replace “resource” with the name of your custom post type.
*   **single.php** - If no post type specific template is found, the default single.php is used. This is what you probably saw if you did an early preview.
*   **index.php** - If no single template is found, WordPress defaults to the old standby - the index.

I’ll be using minimal examples for each of the templates, modified to work with Twenty Ten. Each example will replace and build on the previous example. Expand to your heart’s content or copy the essentials into your own theme.

To get started with our example, create a file called **single-resource.php** and upload it to your theme folder. Add the following code:

<pre><code class="language-php">&lt;?php get_header(); ?&gt;

  &lt;div id="container"&gt;
    &lt;div id="content"&gt;
    &lt;?php if ( have_posts() ) while ( have_posts() ) : the_post(); ?&gt;

      &lt;div class="resource"&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
        &lt;div class="entry-content"&gt;
          &lt;?php the_content();?&gt;
        &lt;/div&gt;
      &lt;/div&gt;

    &lt;?php endwhile; ?&gt;
    &lt;/div&gt;
  &lt;/div&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>

The code above will give you a rather unexciting, but working template that will display the title and content (drawn directly from the main editor). What about our custom fields? Let’s add them in next.

Replace the code in single-resource.php with the following:

<pre><code class="language-php">&lt;?php get_header(); ?&gt;

&lt;?php // Let's get the data we need
  $recording_date = get_post_meta( $post-&gt;ID, 'recording_date', true );
  $recording_length = get_post_meta( $post-&gt;ID, 'recording_length', true );
?&gt;

  &lt;div id="container"&gt;
    &lt;div id="content"&gt;
    &lt;?php if ( have_posts() ) while ( have_posts() ) : the_post(); ?&gt;

      &lt;div class="resource"&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
        &lt;div class="entry-meta"&gt;
          &lt;span&gt;Recorded: &lt;?php echo $recording_date ?&gt; | &lt;/span&gt;
          &lt;span&gt;Duration: &lt;?php echo $recording_length ?&gt; &lt;/span&gt;
        &lt;/div&gt;
        &lt;div class="entry-content"&gt;
          &lt;?php the_content();?&gt;
        &lt;/div&gt;
      &lt;/div&gt;

    &lt;?php endwhile; ?&gt;
    &lt;/div&gt;
  &lt;/div&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>

We’re making progress! Now, using the examples above, you should see the date your resource was published and the duration of the media file.

Let’s take a look at how that works. In WordPress, data stored in custom fields can be accessed several ways. Here, we are using a function called <a href="https://codex.wordpress.org/Function_Reference/get_post_meta">get_post_meta</a>. This function requires two parameters, the unique ID of the post you want to get the data from and the name of the field (its “key”) whose data you’re after. Here’s the code again:

<code>$recording_date = get_post_meta( $post-&gt;ID, 'recording_date', true );</code>

First, we set a variable with PHP - we name it “$recording_date”. Then, we use the “get_post_meta” function. Remember, it needs two parameters, ID and the “key” of the field we want. “$post-&gt;ID” tells WordPress to use the ID of the post it is currently displaying. If we wanted to target a specific post, we'd put its ID instead:

<code>$recording_date = get_post_meta( 35, 'recording_date', true ); // Get the date from post 35</code>

The next parameter is the “key”, or “name” of our custom field. Be sure you get that right. The last parameter tells the function to return the result as a single “string” - something that we can use as text in our template below. To display our data in the template, we write:

<code>&lt;?php echo $recording_date ?&gt;</code>

Ok, let’s keep going and get our custom taxonomies showing up.

Replace the code in single-resource.php with the following:

<pre><code class="language-php">&lt;?php get_header(); ?&gt;

&lt;?php // Let's get the data we need
  $recording_date = get_post_meta( $post-&gt;ID, 'recording_date', true );
  $recording_length = get_post_meta( $post-&gt;ID, 'recording_length', true );
  $resource_presenters = get_the_term_list( $post-&gt;ID, 'presenters', ’, ', ', ’ );
  $resource_topics = get_the_term_list( $post-&gt;ID, 'topics', ’, ', ', ’ );
?&gt;

  &lt;div id="container"&gt;
    &lt;div id="content"&gt;
    &lt;?php if ( have_posts() ) while ( have_posts() ) : the_post(); ?&gt;

      &lt;div class="resource"&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
        &lt;div class="entry-meta"&gt;
          &lt;span&gt;Recorded: &lt;?php echo $recording_date ?&gt; | &lt;/span&gt;
          &lt;span&gt;Duration: &lt;?php echo $recording_length ?&gt; | &lt;/span&gt;
          &lt;span&gt;Presenters: &lt;?php echo $resource_presenters ?&gt; | &lt;/span&gt;
          &lt;span&gt;Topics: &lt;?php echo $resource_topics ?&gt;&lt;/span&gt;
        &lt;/div&gt;
        &lt;div class="entry-content"&gt;
          &lt;?php the_content();?&gt;
        &lt;/div&gt;
      &lt;/div&gt;

    &lt;?php endwhile; ?&gt;
    &lt;/div&gt;
  &lt;/div&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>

Now we’re starting to get more dynamic. You should see your custom fields and, assuming that your custom post has “presenters” and “topics” associated with it, you should see a list of one or more custom taxonomy terms as links. If you clicked the link, you probably saw a page that didn’t look quite what you expected - we’ll get to that soon. Check out <a href="https://developer.wordpress.org/reference/functions/get_the_term_list/">get_the_term_list on the WordPress Codex</a> to learn more about how it works.

## Adding A Media Player

Now that we have some basic data in place, it’s time to add our media player. In this example, we will be working with the <a href="https://www.jwplayer.com/?hsLang=en">JW Media Player</a>, a highly customizable open-source solution.

### Installing JW Media Player

You can access basic installation instructions <a href="https://www.longtailvideo.com/support/jw-player/jw-player-for-flash-v5/12/install-the-jw-player-for-flash-v5">here</a>. I recommend the following steps:

1.  [Download the player](https://www.longtailvideo.com/players/jw-flv-player/) from the Longtail Video website.
2.  Create a folder within your theme to hold the player files - In this case, I’ve named the folder “jw”.
3.  Upload **jwplayer.js** and **player.swf** to the JW Player folder within your theme.

JW Player is now installed and ready to be referenced.

Now, replace the code in single-resource.php with the following:

<pre><code class="language-php">&lt;?php get_header(); ?&gt;

&lt;?php // Let's get the data we need
  $recording_date = get_post_meta( $post-&gt;ID, 'recording_date', true );
  $recording_length = get_post_meta( $post-&gt;ID, 'recording_length', true );
  $resource_presenters = get_the_term_list( $post-&gt;ID, 'presenters', ’, ', ', ’ );
  $resource_topics = get_the_term_list( $post-&gt;ID, 'topics', ’, ', ', ’ );

  $resource_video = new WP_Query( // Start a new query for our videos array(
    'post_parent' =&gt; $post-&gt;ID, // Get data from the current post
    'post_type' =&gt; 'attachment', // Only bring back attachments
    'post_mime_type' =&gt; 'video', // Only bring back attachments that are videos
    'posts_per_page' =&gt; '1', // Show us the first result
    'post_status' =&gt; 'inherit', // Attachments require "inherit" or "all"
    )
  );
?&gt;

  &lt;div id="container"&gt;
    &lt;div id="content"&gt;
    &lt;?php if ( have_posts() ) while ( have_posts() ) : the_post(); ?&gt;

      &lt;div class="resource"&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
        &lt;div class="entry-meta"&gt;
          &lt;span&gt;Recorded: &lt;?php echo $recording_date ?&gt; | &lt;/span&gt;
          &lt;span&gt;Duration: &lt;?php echo $recording_length ?&gt; | &lt;/span&gt;
          &lt;span&gt;Presenters: &lt;?php echo $resource_presenters ?&gt;&lt;/span&gt;
        &lt;/div&gt;
        &lt;div class="entry-content"&gt;
          &lt;?php while ( $resource_video-&gt;have_posts() ) : $resource_video-&gt;the_post(); ?&gt;
            &lt;p&gt;Video URL: &lt;?php echo $post-&gt;guid; ?&gt;&lt;/p&gt;
          &lt;?php endwhile; ?&gt;

          &lt;?php wp_reset_postdata(); // Reset the loop ?&gt;

          &lt;?php the_content(); ?&gt;
        &lt;/div&gt;
      &lt;/div&gt;

    &lt;?php endwhile; ?&gt;
    &lt;/div&gt;
  &lt;/div&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>

<blockquote><strong>Note: </strong>You may notice the somewhat mysterious reference to “wp_reset_postdata”. We are creating a loop within a loop and, to prevent strange behavior with template tags like “the_content” (try removing “wp_reset_postdata” to see what happens), we need to run a reset after any new loops we add within the main loop. <a href="https://codex.wordpress.org/The_Loop">Learn more about the loop</a> on the WordPress Codex.</blockquote>

Now we’re getting somewhere! If everything went as expected, you should see a direct, plain text URL to your video. That’s not very exciting (yet), but we want to make sure we are getting *that* far before we add in the next step - the player.

If you’re having trouble at this point, check back through your code and look for any mistakes that may have been made. If you are trying to vary widely from this example, simplify your variations and start as close to this example as you can - get that to work *first* then branch back out.

With the URL to our video available, we are ready to add in the player. Let’s go!

Replace the code in single-resource.php with the following:

<pre><code class="language-php">&lt;?php get_header(); ?&gt;

&lt;?php // Let's get the data we need
  $recording_date = get_post_meta( $post-&gt;ID, 'recording_date', true );
  $recording_length = get_post_meta( $post-&gt;ID, 'recording_length', true );
  $resource_presenters = get_the_term_list( $post-&gt;ID, 'presenters', ’, ', ', ’ );
  $resource_topics = get_the_term_list( $post-&gt;ID, 'topics', ’, ', ', ’ );

  $resource_video = new WP_Query( // Start a new query for our videos array(
    'post_parent' =&gt; $post-&gt;ID, // Get data from the current post
    'post_type' =&gt; 'attachment', // Only bring back attachments
    'post_mime_type' =&gt; 'video', // Only bring back attachments that are videos
    'posts_per_page' =&gt; '1', // Show us the first result
    'post_status' =&gt; 'inherit', // Attachments require "inherit" or "all"
    )
  );
?&gt;

  &lt;div id="container"&gt;
    &lt;div id="content"&gt;
    &lt;?php if ( have_posts() ) while ( have_posts() ) : the_post(); ?&gt;

      &lt;div class="resource"&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
        &lt;div class="entry-meta"&gt;
          &lt;span&gt;Recorded: &lt;?php echo $recording_date ?&gt; | &lt;/span&gt;
          &lt;span&gt;Duration: &lt;?php echo $recording_length ?&gt; | &lt;/span&gt;
          &lt;span&gt;Presenters: &lt;?php echo $resource_presenters ?&gt; | &lt;/span&gt;
          &lt;span&gt;Topics: &lt;?php echo $resource_topics ?&gt;&lt;/span&gt;
        &lt;/div&gt;

        &lt;div class="entry-content"&gt;
        &lt;?php while ( $resource_video-&gt;have_posts() ) : $resource_video-&gt;the_post(); // Check for our video ?&gt;
          &lt;div id="player"&gt;
            &lt;script type="text/javascript" src="&lt;?php bloginfo('stylesheet_directory'); ?&gt;/jw/jwplayer.js"&gt;&lt;/script&gt;
            &lt;div id="mediaspace"&gt;Video player loads here.&lt;/div&gt;
            &lt;script type="text/javascript"&gt;
                jwplayer("mediaspace").setup({
                    flashplayer: '&lt;?php bloginfo( 'stylesheet_directory' ); ?&gt;/jw/player.swf',
                    file: '&lt;?php echo $post-&gt;guid; ?&gt;',
                    width: 640,
                    height: 360
                });
            &lt;/script&gt;
          &lt;/div&gt;
        &lt;?php endwhile; ?&gt;

        &lt;?php wp_reset_postdata(); // Reset the loop ?&gt;

        &lt;?php the_content(); ?&gt;
        &lt;/div&gt;
      &lt;/div&gt;

    &lt;?php endwhile; ?&gt;
    &lt;/div&gt;
  &lt;/div&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>

Note carefully the assumptions I’m making in the code above. First, I am assuming that you are storing the JW player files in a folder called “jw” inside the WordPress theme folder of the currently activated theme. If you load the page and the player is *not* working (and you *did* have the video URL displaying in the previous step), view the source code on your page, copy the URLs that WordPress is generating to your respective JW player files (jwplayer.js and player.swf) and try accessing them in your browser to make sure each is valid. If there is a problem, update your references accordingly.

Otherwise, there you have it! Your video details and the video itself is now displaying on the page and you should see something like this:

<figure><img class="101171" title="Twenty Ten, front end" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6af8b2f3-53b3-42bf-ad10-70405a85279e/tutorial-frontend-complete-e1305143493456.png" alt="Screenshot" width="550" height="412" /><figcaption>A view of the player, complete with title, description, custom field values and custom taxonomies terms.</figcaption></figure>
<blockquote><strong>Note: </strong>There is a <em>lot </em>that you can do to customize the appearance and behavior of the JW Player. A good place to start is the <a href="https://www.longtailvideo.com/support/jw-player-setup-wizard">JW Player Setup Wizard</a>. Customize the player to your liking, then implement the code changes in your template accordingly.</blockquote>

### Using Vimeo Instead

Let’s say you wanted to use Vimeo, instead of uploading the videos into WordPress. First, you need to add a custom field to store the ID of your Vimeo video. Assuming you’ve done that, and assuming that you’ve entered a valid Vimeo ID in your custom field (we named the field “vimeo_id” in our example), the following code will work:

<pre><code class="language-php">&lt;?php get_header(); ?&gt;

&lt;?php // Let's get the data we need
  $recording_date = get_post_meta( $post-&gt;ID, 'recording_date', true );
  $recording_length = get_post_meta( $post-&gt;ID, 'recording_length', true );
  $resource_presenters = get_the_term_list( $post-&gt;ID, 'presenters', ’, ', ', ’ );
  $resource_topics = get_the_term_list( $post-&gt;ID, 'topics', ’, ', ', ’ );

  $vimeo_id = get_post_meta( $post-&gt;ID, 'vimeo_id', true );
?&gt;

  &lt;div id="container"&gt;
    &lt;div id="content"&gt;
    &lt;?php if ( have_posts() ) while ( have_posts() ) : the_post(); ?&gt;

      &lt;div class="resource"&gt;
        &lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
        &lt;div class="entry-meta"&gt;
          &lt;span&gt;Recorded &lt;?php echo $recording_date ?&gt; | &lt;/span&gt;
          &lt;span&gt;Duration: &lt;?php echo $recording_length ?&gt; | &lt;/span&gt;
          &lt;span&gt;Presenters: &lt;?php echo $resource_presenters ?&gt; | &lt;/span&gt;
          &lt;span&gt;Topics: &lt;?php echo $resource_topics ?&gt;&lt;/span&gt;
        &lt;/div&gt;

        &lt;div class="entry-content"&gt;
          &lt;?php if ($vimeo_id) { // Check for a video ?&gt;
            &lt;iframe src="https://player.vimeo.com/video/&lt;?php echo $vimeo_id; ?&gt;?byline=0&amp;title=0&amp;portrait=0" width="640" height="360" frameborder="0" class="vimeo"&gt;&lt;/iframe&gt;
          &lt;?php } ?&gt;

          &lt;?php the_content(); ?&gt;
        &lt;/div&gt;
      &lt;/div&gt;

    &lt;?php endwhile; ?&gt;
    &lt;/div&gt;
  &lt;/div&gt;

&lt;?php get_sidebar(); ?&gt;
&lt;?php get_footer(); ?&gt;</code></pre>

We use “$vimeo_id” to retrieve and store the ID from our custom field (named “vimeo_id”, in this case) and then, in the code below, we first check to make sure the $vimeo_id field has data in it, then we use Vimeo’s iframe code (<a href="https://vimeo.com/blog:334">details here</a>) to load the video.

<figure><img class="98880" title="Example of Vimeo ID" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f44cabc-840e-4edb-be86-933065ebf7c6/tutorial-vimeo-id.png" alt="Screenshot" width="550" height="32" /><figcaption>In Vimeo’s case, the ID is a series of numbers (notice the selected text) after “vimeo.com/”.</figcaption></figure>

## Conclusion

And that concludes part one! You’ve learned how to setup custom post types and custom taxonomies *without* using plugins. You’ve also learned how to setup custom fields and display their data, along with a video player and custom taxonomy terms, within a custom post template. <a href="https://www.smashingmagazine.com/2011/06/08/how-to-build-a-media-site-on-wordpress-part-2/">In part two</a>, we’ll look at how to customize the custom taxonomy templates and make them a whole lot more useful.

{{% ad-panel-leaderboard %}}

## Credits

Though this article keeps things basic, the conclusions in part two and a lot of the techniques developed in conjunction with the projects that inspired this series would have been much more difficult without the help of the <a href="https://wordpress.stackexchange.com">WordPress Stack Exchange</a> community. If you have a question directly related to this post, ask it here. If you have anything else WordPress related, though, WPSE is the place to go. Also, a big thank you to <a href="https://joshuawold.com">Joshua</a>, <a href="https://nickjohnson.com">Nick</a>, <a href="https://claydoss.com">CJ</a>, and <a href="https://mattgeri.com">Matt</a> for their many hours spent reviewing, testing code samples, and providing feedback while I worked on this series.

### Further Reading

*   [Creating Mobile-Optimized Websites Using WordPress](https://www.smashingmagazine.com/2012/05/creating-mobile-optimized-websites-using-wordpress/)
*   [A Beginner’s Guide To Creating A WordPress Website](https://www.smashingmagazine.com/2016/02/beginners-guide-creating-wordpress-website/)
*   [My (Simple) Workflow To Design And Develop A Portfolio Website](https://www.smashingmagazine.com/2013/06/workflow-design-develop-modern-portfolio-website/)
*   [A Comprehensive Checklist To Creating The Perfect WP Website](https://www.smashingmagazine.com/2011/12/15-step-checklist-creating-perfect-wordpress-website/)

{{< signature "mrn" >}}

---
title: Extend WordPress With Custom Fields
slug: extend-wordpress-with-custom-fields
image: null
date: 2010-04-29T13:29:18.000Z
author: alex-denning
description: >-
  WordPress' popularity has grown exponentially as of late. This rise in popularity is due in part to WordPress' custom fields. Custom fields allow you to add little bits of data to posts. They have changed the way people look at WordPress. A couple of years ago, WordPress was a blogging platform — a good one, but a blogging platform nonetheless. Now it's widely considered to be an excellent simple content management system. How did it evolve so quickly? **Custom fields,** that's how.
categories:
  - WordPress
  - Custom Fields
  - Functions
---
How exactly did these bits of data transform WordPress? The fields could initially include the weather — as the codex points out — the temperature and various other not-particularly-useful things. And that was the story for a while. Then people started to realize that they could use the custom fields to store URLs of images. They could then pull these images to the home page to create magazine-style layouts. These magazine themes, as they became known, evolved, and eventually you were able to pull images automatically from posts. You can draw a direct line from WordPress' popularity to the magazine themes to custom fields.

You may also want to check out the following Smashing Magazine articles:

*   [Custom Fields Hacks For WordPress](https://www.smashingmagazine.com/2009/05/10-custom-fields-hacks-for-wordpress/)
*   [How To Create Custom Post Meta Boxes In WordPress](https://www.smashingmagazine.com/2011/10/create-custom-post-meta-boxes-wordpress/)
*   [Extending Advanced Custom Fields With Your Own Controls](https://www.smashingmagazine.com/2015/09/extending-advanced-custom-fields-with-your-own-controls/)
*   [<span class="headline">The Complete Guide To Custom Post Types</span>](https://www.smashingmagazine.com/2012/11/complete-guide-custom-post-types/)

## The Custom Field Syntax

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ae0def-ea40-4863-b559-d4fc05f29340/custom-fields.jpg"><img loading="lazy" decoding="async" class="30759" title="custom-fields" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ae0def-ea40-4863-b559-d4fc05f29340/custom-fields.jpg" alt="custom-fields" width="500" height="144" /></a>

{{% feature-panel %}}

In order to do more complicated things, you'll need to understand the syntax. Creating a custom field is easy: it requires a name and a value. The name is constant, but the value can change with each post.

A real-world example: let's say you run a blog about cameras. You have categories set up for each type of post ("Review," "New," etc.), and you tag the post with the manufacturer's name. But you want to display the price and specifications of the camera. This is as easy as creating a new custom field with the name <code>Camera_Specs</code> and then typing the info into the value box. Click the "Add" button and you will have added the custom field to the post.

Displaying the field on the page is simple, too. In the <em>single.php</em> file, add the following code:

<pre><code class="language-php">&lt;?php echo get_post_meta($post-&gt;ID, "Camera_Specs", true); ?&gt;</code></pre>

(You might want to wrap this in a paragraph, ordered list or the like. You can use HTML in the value of the field.)

<strong>Custom fields can be conditional</strong>, too. We can display a camera's specs or, if that isn't available, some generic text.

<pre><code class="language-php">&lt;?php $camera_specs = get_post_meta($post-&gt;ID, 'Camera_Specs', true);
if ($camera_specs) {
?&gt;
&lt;?php echo $camera_specs; ?&gt;

&lt;?php } else { ?&gt;

&lt;p&gt;No specification available.&lt;/p&gt;

&lt;?php } ?&gt;</code></pre>

That's the general syntax, and now <strong>the only limit is your imagination</strong>!

## Spicing Up Post Titles

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dc9d8db-263e-4000-8435-1a2b53b2f5d1/custom-fields-title.jpg"><img loading="lazy" decoding="async" class="30762" title="custom-fields-title" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6dc9d8db-263e-4000-8435-1a2b53b2f5d1/custom-fields-title.jpg" alt="custom-fields-title" width="500" height="167" /></a>

Post titles are usually fairly boring. You're limited to text. Links aren't possible, nor is HTML. Well, not anymore. Custom fields to the rescue!

Using a conditional statement and custom fields, adding any HTML to your posts' titles is now possible. (This won't work with RSS feeds or the like, but it works great for any titles on the blog itself.) We'll use the custom field <code>Post-Title</code>:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acc07f2d-db8a-48bb-9193-50b38004dbb8/custom-fields-post-title.jpg"><img loading="lazy" decoding="async" class="30761" title="custom-fields-post-title" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acc07f2d-db8a-48bb-9193-50b38004dbb8/custom-fields-post-title.jpg" alt="custom-fields-post-title" width="500" height="169" /></a>

<strong>You can add any HTML you like to your posts' titles.</strong> Implementing it on your blog is easy, too. You'll have to use the following code on all pages on which titles are displayed: the home page, archives, current posts, etc. The following snippet looks for the custom field and falls back on <code>the_title</code>:

<pre><code class="language-php">&lt;?php $post_title = get_post_meta($post-&gt;ID, 'Post-Title', true);
if ($post_title) {
?&gt;
&lt;h2&gt;&lt;?php echo $post_title; ?&gt;&lt;/h2&gt;

&lt;?php } else { ?&gt;

&lt;h2&gt;&lt;?php the_title(); ?&gt;&lt;/h2&gt;

&lt;?php } ?&gt;</code></pre>

An easy yet effective way to improve your website.</p>

## Only Display Posts With A Specific Custom Field

WordPress displays posts through something called a loop. Another WordPress function, <code>query_posts</code>, allows you to choose exactly which posts are displayed in your loop. One parameter lets you display <strong>only posts that have a custom field</strong> and/or that have a specific custom field value. Going back to our camera website, we could display only posts that have the custom field <code>Camera_Specs</code>:

<pre><code class="language-php">query_posts('meta_key=Camera_Specs');</code></pre>

If we wanted to display only cameras that had 10 megapixels (and if all posts had the custom field <code>Camera_Specs_Pixels</code> that specified the value of the number of megapixels), we could do so with the following:

<pre><code class="language-php">query_posts('meta_key=Camera_Specs_Pixels&amp;meta_value=10');</code></pre>

You may want to do this on a custom page template. If so, just add the following to the top of the file and name it appropriately (e.g. <em>camera-specs-pixels.php</em>):

<pre><code class="language-php">&lt;?php /*Template Name: Camera Specs Pixels */?&gt;</code></pre>

To make your new page template show up, create a new page, and then in the drop-down on the right, choose the page template you've just created. Publish the post, and you're done!

## Using Custom Fields To Create A Unique Design

WordPress 2.7 introduced the <code>post_class</code> function. This allows you to <strong>apply specific CSS classes to posts</strong> (thus giving them unique designs). Guess what? You can use custom fields to apply particular classes!

This one is a bit more involved. First, open your <em>functions.php</em> file and add the following code:

<pre><code class="language-php">function shiftnews_post_class($classes) {
   global $post;
   $sn_post_class_array = array (
      get_the_author_meta('display_name'),
      get_post_meta($post-&gt;ID, 'post-class', true)
   );
   $classes[] = implode(" ", $sn_post_class_array);
   return $classes;
}</code></pre>

You'll then need to edit your <em>single.php</em> file, adding <code>&lt;?php post_class(shiftnews_post_class()); ?&gt;</code> to a DIV that wraps your content. Using the custom field <code>post-class</code>, you can then type in CSS classes (e.g. <code>flower-bg</code> or <code>blue-content</code>, which would apply the classes <code>.flower-bg</code> or <code>.blue-content</code>), thus adding them to the post.

The possibilities here are inspiring, and this is quite <strong>possibly the best way to create a unique post design for WordPress</strong>.</p>

### Set a different background for each post with custom fields

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08228069-3a5f-4c52-ac72-e9f5e4a87d38/editorial.jpg" alt="Screenshot" width="509" height="300" />

You could take this even further by allowing users to choose a background image through custom fields. Of course, you could just resize the image to 1920x1200, upload it and copy the URL into a custom field, 'background' and then put the following code in your header:

<pre><code class="language-php">&lt;?php if (is_page() || is_single()) {

&lt;?php $background = get_post_meta($post-&gt;ID, 'background', true);
if ($background) {
?&gt;
&lt;style type="text/css"&gt;body{ url(&lt;?php echo $background; ?&gt;) no-repeat fixed; }&lt;/style&gt;

&lt;?php }
}?&gt;</code></pre>

But that would be a pain to do every single time you just wanted to change the background image. There is an easy way to do it: upload an image, copy the URL into a custom field and then use a script to resize the image and set it as the background.

First thing to do is to upload an image. We're going to be resizing it to 1920px (although depending on your audience you may want to use a higher/lower resolution) so anything that's 1200px wide or above should look fine.

Copy the relative URL of the image (ie /wp-content/... , not https://yoursite.com/wp-content/) into a custom field called 'background' and click 'add custom field'. Next, we need something to resize the images with. We'll be using <a href="https://code.google.com/p/timthumb">timthumb</a>. Upload it to /yourtheme/timthumb/ and we're ready to go!

Open up your header once again and add (below your theme's stylesheet) the following:

<pre><code class="language-php">&lt;?php if (is_page() || is_single()) {

&lt;?php $background = get_post_meta($post-&gt;ID, 'background', true);
if ($background) {
?&gt;
&lt;style type="text/css"&gt;background: url(&lt;?php bloginfo('template_url'); ?&gt;/timthumb/timthumb.php?w=1920&amp;zc=1&amp;src=&lt;?php echo $background; ?&gt;) fixed no-repeat;&lt;/style&gt;

&lt;?php }
}?&gt;</code></pre>

What that does is takes the image from the custom field and then runs it through timthumb so it gets resized to fill the entire screen, even on large monitors (the image then gets cached, so it is only generated once). The resized image is then displayed as the background of the post.

If you're having problems, make sure you've got the relative URL and not the absolute URL of the image, it is hosted on your server (you're not hotlinking!) and that you have the file permissions set correctly (as shown in the timthumb wiki). This is one of my favourite things to do with custom fields as not only is it easy to do, but it's also very effective in differentiating different blog posts; this technique is used to great effect on Nometet.com.</p>

## Search Engine Optimization With Custom Fields

The "All in One SEO Pack" is consistently one of the most popular plug-ins for WordPress. It allows you to do things like specify your own title tag or meta description. It is powered by custom fields, meaning <strong>you can recreate it</strong> in your theme.

Start by adding the following code to your theme's <code>title</code> tag:

<pre><code class="language-php">&lt;?php if ( is_single() || is_page() ) { ?&gt;&lt;?php $title = get_post_meta($post-&gt;ID, 'Title', true);  if ($title) { ?&gt;
&lt;?php echo $title; ?&gt; | &lt;?php bloginfo('name'); ?&gt;
&lt;?php } else { ?&gt;
&lt;?php wp_title(’); ?&gt; | &lt;?php bloginfo('name'); ?&gt;
&lt;?php } ?&gt;
&lt;?php } ?&gt;</code></pre>

Now, when a page or post is displayed, WordPress will look for the custom field <code>Title</code>. If it exists, its contents will be displayed; if it doesn't, then the post's title will be displayed. To use this new-found power, create the custom field <code>Title</code> and make its value what you want to be displayed in the <code>title</code> tag (note that <code>| [Blog name]</code> will be added).

You can apply the same idea to other elements, such as the <code>description</code> tag:

<pre><code class="language-php">&lt;?php if (is_single() || is_page() ) : if ( have_posts() ) : while ( have_posts() ) : the_post(); ?&gt;
&lt;meta name="description" content="&lt;?php $description = get_post_meta($post-&gt;ID, 'Description', true);  if ($description) { ?&gt;&lt;?php echo get_post_meta($post-&gt;ID, "Description", true); ?&gt;
&lt;?php } else { ?&gt;&lt;?php the_excerpt_rss(); ?&gt;&lt;?php } ?&gt;" /&gt;
&lt;?php endwhile; endif; elseif(is_home()) : ?&gt;
&lt;meta name="description" content="&lt;?php bloginfo('description'); ?&gt;" /&gt;
&lt;?php endif; ?&gt;</code></pre>

The code above should replace the entire <code>description</code> tag and allow you to use the custom field <code>Description</code> to display the contents of the description tag. If the custom field does not exist, then the excerpt is used on posts and pages, and the blog's description (which you set when you installed WordPress) is used on the home page.

Read more on the topic in the article <a href="https://yoast.com/articles/wordpress-seo/">WordPress SEO: The Definitive Guide To Higher Rankings For Your Blog</a>.</p>

## Custom This, Custom That!

Custom fields are very powerful, and <strong>the only limit is your imagination</strong>! As we've seen in this post, you can do some really awesome things with WordPress' custom fields. They can <strong>improve both your blog and its ranking</strong> in search engines. Enjoy!

If you'd like to do some further reading:

*   [10 Awesome Things to Do With WordPress' Custom Fields](https://wpshout.com/10-awesome-things-to-do-with-wordpress-custom-fields/)
*   WordPress Custom Field Tutorial, [Part 1](https://perishablepress.com/press/2008/12/17/wordpress-custom-fields-tutorial/) and [Part 2](https://perishablepress.com/press/2008/12/22/wordpress-custom-fields-tips-tricks/)
*   [Custom "Read More" Links](https://www.wprecipes.com/create-custom-read-more-links-on-your-wordpress-blog)

The possibilities for this are inspiring, and this is quite possibly the best way to create a unique post design for WordPress.

Of course, the other option is to use custom fields to include a style sheet that is specific to the post or even just to use inline styling.

You can add a style sheet to a post with a custom field value quite easily. First, add the following code to the <em>header.php</em> file, after your theme's style sheet loads:

<pre><code class="language-php">&lt;?php if (is_page() || is_single()) {

&lt;?php $stylesheet = get_post_meta($post-&gt;ID, 'Stylesheet', true);
if ($stylesheet) {
?&gt;
&lt;link rel="stylesheet" href="&lt;?php bloginfo('template_url'); ?&gt;&lt;?php echo $stylesheet; ?&gt;.css" type="text/css" media="screen,projection,tv" /&gt;&lt;/h2&gt;

&lt;?php }
}?&gt;</code></pre>

This tells WordPress to look for the custom field <code>Stylesheet</code> on posts and pages. All you've got to do is enter the name of the style sheet (so if it's <em>blue.css</em>, just enter the value <code>blue</code>) and upload it to your theme's directory.

A whole new style sheet might be overkill in some cases, though. If you're changing just one or two styles, then inline styling might be the way to go. This is just as easy: paste the following code into your <em>header.php</em> file, again after your theme's style sheet loads:

<pre><code class="language-php">&lt;?php if (is_page() || is_single()) {

&lt;?php $styles = get_post_meta($post-&gt;ID, 'Styles', true);
if ($styles) {
?&gt;
&lt;style type="text/css"&gt;&lt;?php echo $styles; ?&gt;&lt;/style&gt;

&lt;?php }
}?&gt;</code></pre>

This piece of code looks for the custom field <code>Styles</code>; put in it any styling you want to apply only to that post. For example:

<pre><code class="language-css">body{
    color:#000;
    background:#fff;
}</code></pre>

There's something for everyone here, so you can start to quickly create unique post designs however you prefer! You might want to look at Smashing Magazine's <a href="https://www.smashingmagazine.com/2009/05/13/10-custom-fields-hacks-for-wordpress/">previous post about custom fields</a> as well.

{{< signature "al" >}}


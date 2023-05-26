---
title: Random Redirection In WordPress
slug: random-redirection-in-wordpress
image: null
date: 2012-04-19T13:57:12.000Z
author: goce-mitevski
description: >-
  If you run an online magazine, most of your readers will never go through your archive, even if you design a neat archive page. It’s not you; it’s just that going through archives is not very popular these days. So, how do you actually make readers dig in without forcing them? How do you invite them to (re)read in a way that’s not boring?
categories:
  - WordPress
  - Techniques
  - Admin
---
How do you make your WordPress magazine more interactive?
Have you tried random redirection?

Call it recycling if you like, but random redirection doesn’t have to be about retreading familiar territory. Through random redirection, you <strong>offer readers a chance to hop randomly through your posts</strong> and discover content that they somehow missed.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   <span>[A Process For Professional WordPress Development](https://www.smashingmagazine.com/2012/03/process-professional-wordpress-development/)</span>
*   [Writing Effective Documentation For WordPress End Users](https://www.smashingmagazine.com/2012/07/writing-effective-wordpress-documentation/)
*   [Random Redirection In WordPress](https://www.smashingmagazine.com/2012/04/random-redirection-in-wordpress/)
*   <span>[Do’s And Don’ts For WordPress Startups](https://www.smashingmagazine.com/2012/06/dos-donts-wordpress-startups/)</span>

The concept really is simple. All you have to do is create a hyperlink — named, say, “Random article” — that when clicked will redirect the reader to a randomly pulled article.

{{% feature-panel %}}

WordPress supports random redirection out of the box, but it’s not very obvious. All of the required functions are in the core, but they’re not bound in any common workflow. For instance, generating a “Random article” link in the main menu simply by checking a box in the administration section is not possible.

To implement random redirection in WordPress, you will usually need to work with the following three things:

*   A page to process the redirection,
*   A query to pick a post from the database,
*   Some sort of mechanism to initiate the redirection.

Of course, many of you might want to use a plugin. That’s absolutely fine, as long as you don’t need any more features than what it offers.

You would probably come across Matt Mullenweg’s <a href="https://wordpress.org/extend/plugins/random-redirect/">Random Redirect</a> plugin first. Then you would probably try <a href="https://wordpress.org/extend/plugins/random-redirect-2/">Random Redirect 2</a>, which expands on that.

Instead, today I’ll guide you through a custom implementation that I use. It’s not the “right” way to implement random redirection; it’s just one plugin-less solution to start with and build on.

We’ll be working with the three things mentioned in the list further up. Let’s go into the concept in detail.</p>

## The Simple Solution

We’ll be implementing random redirection through a WordPress page, which we’ll simply call “Random.” Creating this new page in the admin section will be the last step we take, though. Why? Because we don’t want to make the redirection page accessible before it’s been fully implemented.

According to the <a href="https://codex.wordpress.org/Template_Hierarchy#Page_display">WordPress template hierarchy</a>, if you create a page template file named <code>page-random.php</code>, whenever a user loads the page assigned to the slug <code>random</code>, it will load through the <code>page-random.php</code> template. This is a well-known benefit of WordPress and is also useful for our random redirection.

The <code>page-random.php</code> page template will not include the usual calls for loading the header, sidebar and footer templates, because our “Random” page won’t generate any visible output for the user; it will simply jump (that is, redirect) to a randomly chosen article. Because we need to make only one request from the database (to select one random article to redirect to), we will make only one call to the <code>get_posts()</code> function in the template, and we’ll use a <code>foreach</code> loop to process the output.

The <code>get_posts()</code> function receives only two arguments as its input, with which we’re specifying that we want to fetch only one post randomly. <strong>The <code>orderby</code> argument set to <code>rand</code> is what enables randomization in WordPress.</strong> We don’t need to specify the <code>post_type</code> because it’s already set to <code>post</code> by default for <code>get_posts()</code>. We also don’t need to specify the <code>post_status</code> because it defaults to <code>publish</code>, which is exactly what we need.

<pre><code class="language-php">// source code from page-random.php

// Random Redirection Page Template

// set arguments for get_posts()
$args = array(
    'numberposts' =&gt; 1,
    'orderby' =&gt; 'rand'
);

// get a random post from the database
$my_random_post = get_posts ( $args );

// process the database request through a foreach loop
foreach ( $my_random_post as $post ) {
  // redirect the user to the random post wp_redirect ( get_permalink ( $post-&gt;ID ) );
  exit;
}</code></pre>

So, we first save the data from <code>get_posts()</code> into a variable and then process it through the <code>foreach</code> loop. The magic happens in the <code>foreach</code> loop, when the redirection is initiated through the <a href="https://codex.wordpress.org/Function_Reference/wp_redirect"><code>wp_redirect()</code></a> function, which has the post’s permalink as its input.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae9e77f-b566-4aa9-b874-4cd56f842301/random-redirection-wordpress-01.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="129671" title="random-redirection-wordpress-add-random-page" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dae9e77f-b566-4aa9-b874-4cd56f842301/random-redirection-wordpress-01.png" alt="random-redirection-wordpress-add-random-page" width="728" height="512" /></a><br>
<em>Creating a “Random” page through WordPress’ administration interface</em>

Now the only thing we need to do is go to WordPress’s administration section, create a blank new page with the slug <code>random</code>, and publish it. Then, when you visit <code>https://www.mywebsite.com/random/</code>, you will be automatically redirected to a random article.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f46c7c0-1a95-4e23-9d12-4bd4e725cd1f/random-redirection-wordpress-02.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="129672" title="random-redirection-wordpress-add-random-page-main-menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f46c7c0-1a95-4e23-9d12-4bd4e725cd1f/random-redirection-wordpress-02.png" alt="random-redirection-wordpress-add-random-page-main-menu" width="637" height="308" /></a><br>
<em>Adding a link to the “Random” page in the main menu.</em>

We can now add a link in the main menu to make the page easily accessible.</p>

## Using WP_Query Instead

The implementation above can easily be adapted to directly use the <a href="https://codex.wordpress.org/Function_Reference/WP_Query"><code>WP_Query</code></a> class, instead of the <code>get_posts()</code> function.

<pre><code class="language-php">// source code from page-random.php implemented through WP_Query

// Random Redirection Page Template

// set arguments for WP_Query()
$args = array(
    'posts_per_page' =&gt; 1,
    'orderby' =&gt; 'rand'
);

// get a random post from the database
$my_random_post = new WP_Query ( $args );

// process the database request through WP_Query
while ( $my_random_post-&gt;have_posts () ) {
  $my_random_post-&gt;the_post ();
  // redirect the user to the random post wp_redirect ( get_permalink () );
  exit;
}</code></pre>

The main benefit of using <code>WP_Query</code> is that it can accept more arguments than the <code>get_posts()</code> function, thus offering more flexibility when you’re building specific queries.</p>

### A Few More Examples

With both <code>get_posts()</code> and <code>WP_Query</code>, we can be very specific and implement random redirection for posts of custom types or posts that belong to particular categories.

For example, we could make WordPress redirect to articles published only in the “Travel” category:

<pre><code class="language-php">// set arguments for WP_Query()
$args = array(
    'category_name' =&gt; 'travel', // remember, we are using category slug here
    'posts_per_page' =&gt; 1,
    'orderby' =&gt; 'rand'
);

// get a random post from the database
$my_random_post = new WP_Query ( $args );

// process the database request through WP_Query
while ( $my_random_post-&gt;have_posts () ) {
  $my_random_post-&gt;the_post ();
  // redirect the user to the random post wp_redirect ( get_permalink () );
  exit;
}</code></pre>

Or we could redirect to posts from all categories except “Uncategorized”:

<pre><code class="language-php">// set arguments for WP_Query()
$args = array(
    'category__not_in' =&gt; array(1), // id of the category to be excluded
    'posts_per_page' =&gt; 1,
    'orderby' =&gt; 'rand'
);

// get a random post from the database
$my_random_post = new WP_Query ( $args );

// process the database request through WP_Query
while ( $my_random_post-&gt;have_posts () ) {
  $my_random_post-&gt;the_post ();
  // redirect the user to the random post wp_redirect ( get_permalink () );
  exit;
}</code></pre>

How about limiting randomization to posts published in 2011?

<pre><code class="language-php">// set arguments for WP_Query()
$args = array(
    'posts_per_page' =&gt; 1,
    'year' =&gt; '2011',
    'orderby' =&gt; 'rand'
);

// get a random post from the database
$my_random_post = new WP_Query ( $args );

// process the database request through WP_Query
while ( $my_random_post-&gt;have_posts () ) {
  $my_random_post-&gt;the_post ();
  // redirect the user to the random post wp_redirect ( get_permalink () );
  exit;
}</code></pre>

Maybe even add filtering by custom field? Let’s limit random redirection to posts that have a custom field with the value <code>strawberry</code> assigned.

<pre><code class="language-php">// set arguments for WP_Query()
$args = array(
    'posts_per_page' =&gt; 1,
    'meta_value' =&gt; 'strawberry',
    'orderby' =&gt; 'rand'
);

// get a random post from the database
$my_random_post = new WP_Query ( $args );

// process the database request through WP_Query
while ( $my_random_post-&gt;have_posts () ) {
  $my_random_post-&gt;the_post ();
  // redirect the user to the random post wp_redirect ( get_permalink () );
  exit;
}</code></pre>

The example above could easily be transformed to limit random redirection to posts that have the custom field <code>long_description</code> assigned. Remember, our only condition here is for the post to have the custom field assigned. It doesn’t matter what the value of the <code>long_description</code> custom field is.

<pre><code class="language-php">// set arguments for WP_Query()
$args = array(
    'posts_per_page' =&gt; 1,
    'meta_key' =&gt; 'long_description',
    'orderby' =&gt; 'rand'
);

// get a random post from the database
$my_random_post = new WP_Query ( $args );

// process the database request through WP_Query
while ( $my_random_post-&gt;have_posts () ) {
  $my_random_post-&gt;the_post ();
  // redirect the user to the random post wp_redirect ( get_permalink () );
  exit;
}</code></pre>

Instead of posts, we could also implement random redirection for pages:

<pre><code class="language-php">// set arguments for WP_Query()
$args = array(
    'post_type' =&gt; 'page',
    'posts_per_page' =&gt; 1,
    'orderby' =&gt; 'rand'
);

// get a random post from the database
$my_random_post = new WP_Query ( $args );

// process the database request through WP_Query
while ( $my_random_post-&gt;have_posts () ) {
  $my_random_post-&gt;the_post ();
  // redirect the user to the random post wp_redirect ( get_permalink () );
  exit;
}</code></pre>

We could even create random redirection for custom post types:

<pre><code class="language-php">// set arguments for WP_Query()
$args = array(
    'post_type' =&gt; 'my-custom-post-type',
    'posts_per_page' =&gt; 1,
    'orderby' =&gt; 'rand'
);

// get a random post from the database
$my_random_post = new WP_Query ( $args );

// process the database request through WP_Query
while ( $my_random_post-&gt;have_posts () ) {
  $my_random_post-&gt;the_post ();
  // redirect the user to the random post wp_redirect ( get_permalink () );
  exit;
}</code></pre>

As you can see from these examples, we can add a random redirection link to a WordPress website with just a few lines of code. Nothing complicated, nothing too advanced.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e870fc-b003-48cb-bad8-99b504b1be09/random-redirection-wordpress-03.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="129673" title="random-redirection-wordpress-wikipedia-wikihow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9e870fc-b003-48cb-bad8-99b504b1be09/random-redirection-wordpress-03.png" alt="random-redirection-wordpress-wikipedia-wikihow" width="918" height="486" /></a>

If random redirection still doesn’t make sense to you, hop on over to <a href="https://en.wikipedia.org/">Wikipedia</a> and <a href="https://www.wikihow.com/">WikiHow</a> and see how their links to random articles work.</p>

## Play The Randomization Game!

Now that you know how easy implementing a random redirection page in WordPress is, you can start planning for your own random output.

All in all, it’s a great feature. Every online magazine should have it. It requires only a single click per request; it’s unpredictable, it’s fun, and it will be useful to your readers.</p>

### Further Reading

*   “[How to Redirect Users to a Random Post in WordPress](https://www.wpbeginner.com/wp-tutorials/how-to-redirect-users-to-a-random-post-in-wordpress/),” WPBeginner
*   “How to Make a ‘Random Post’ Button,” Wessley Roche
*   “[Random Post Snippet](https://ottopress.com/2011/random-post-snippet/),” Otto on WordPress
*   “[Redirect Home Page to a Random Blog Post](https://wpsnipp.com/index.php/loop/redirect-home-page-to-a-random-blog-post/),” WordPress Code Snippets
*   “[Template Tags/get_posts()](https://codex.wordpress.org/Template_Tags/get_posts),” WordPress Codex
*   “[Class Reference/WP_Query](https://codex.wordpress.org/Class_Reference/WP_Query),” WordPress Codex

{{< signature "al" >}}


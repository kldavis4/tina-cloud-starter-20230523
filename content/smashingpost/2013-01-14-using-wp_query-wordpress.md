---
title: How To Use WP_Query In WordPress
slug: using-wp_query-wordpress
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20c6a95f-29a3-4ce8-a22a-fdd3422f08ce/wp-query-1-1.png'
date: 2013-01-14T15:41:26.000Z
author: daniel-pataki
description: >-
  If you've been around WordPress for a while you know how difficult it used to
  be to create post lists based on complex criteria while also conforming to
  WordPress standards. Over the course of a few years the platform has come a
  long way. By utilising the power of the `WP_Query` class, we can lists posts
  in any way we want.
categories:
  - WordPress
  - Themes
  - Techniques (WP)
---
If you’ve been around WordPress for a while, you’ll know how difficult it used to be to create lists of posts based on complex criteria while also conforming to WordPress’ standards. Over the course of a few years, the platform has come a long way. By using the power of the <code>WP_Query</code> class, we can lists posts in any way we want.

<img loading="lazy" decoding="async" class="108029" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cb00b45-db76-4967-ab6f-a956491f22ce/wp-query-1.png" alt="wp_query" title="How To Use WP_Query In WordPress" width="500" height="325" />

## What Is WP_Query?

The <code>WP_Query</code> class is one of the most important parts of the WordPress codebase. Among other things, it determines the query you need on any given page and pulls posts accordingly. It also saves a lot of information about the requests it makes, which helps a great deal when optimizing pages (and troubleshooting them).

The other role of <code>WP_Query</code> is to enable us to perform complex database queries in a safe, simple and modular manner.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Powerful WordPress Tips And Tricks](https://www.smashingmagazine.com/2013/09/powerful-wordpress-tips-and-tricks/)
*   [Building An Advanced WordPress Search With WP_Query](https://www.smashingmagazine.com/2016/03/advanced-wordpress-search-with-wp_query/)
*   [10 Useful WordPress Loop Hacks](https://www.smashingmagazine.com/2009/06/10-useful-wordpress-loop-hacks/)
*   [<span class="headline">Do-It-Yourself Caching Methods With WordPress</span>](https://www.smashingmagazine.com/2012/06/diy-caching-methods-wordpress/)

### Safety

Throughout our interactions with this object, we are supplying parameters and using functions to reach our goal. The object’s internals take care of many annoyances, such as protecting against SQL injection attacks and making sure that proper data types are used.</p>

### Simplicity

The object abstracts much of the query complexity away so that we don’t have to muck about with the specifics of our database. Because we are using an array to supply our criteria, everything is more self-explanatory. No manual database joins or nested queries are needed — just create an arguments array and instantiate the class!

### Modularity

My favorite of all is modularity. When making raw queries, it is hard to manage those frequently used bits because they are just fragments of SQL code. <code>WP_Query</code> does away with this by using an associative array as an argument. A plethora of goodness ensues: you can merge arguments from different places, run array functions to your heart’s content and manipulate it in ingenious ways.</p>

## Getting Started

### The “Regular” WordPress Loop

Let’s look at a regular loop first, and then create the same loop using <code>WP_Query</code>. Let’s assume that we’re coding in the <code>category.php</code> file.

<pre><code class="language-php">&lt;?php
   if(have_posts()) :
      while(have_posts()) :
         the_post();
?&gt;

         &lt;h1&gt;&lt;?php the_title() ?&gt;&lt;/h1&gt;
         &lt;div class='post-content'&gt;&lt;?php the_content() ?&gt;&lt;/div&gt;

&lt;?php
      endwhile;
   else :
?&gt;

      Oops, there are no posts.

&lt;?php
   endif;
?&gt;</code></pre>

### The Same Loop Using WP_Query

<pre><code class="language-php">&lt;?php

   $args = array('cat' =&gt; 4);
   $category_posts = new WP_Query($args);

   if($category_posts-&gt;have_posts()) :
      while($category_posts-&gt;have_posts()) :
         $category_posts-&gt;the_post();
?&gt;

         &lt;h1&gt;&lt;?php the_title() ?&gt;&lt;/h1&gt;
         &lt;div class='post-content'&gt;&lt;?php the_content() ?&gt;&lt;/div&gt;

&lt;?php
      endwhile;
   else:
?&gt;

      Oops, there are no posts.

&lt;?php
   endif;
?&gt;</code></pre>

As you can see, there is not much difference at all! Let’s break it down:

1.  **Constructing a query** On a category page, WordPress already knows that you want to list posts from that category. Because we are constructing a query from scratch using `WP_Query`, we need to specify this ourselves. We’ll delve a bit deeper into this in a bit.
2.  **Instantiating the class and querying for posts** By instantiating a class with the constructed argument array, `WP_Query` will try to pull the posts specified and a load of other details.
3.  **Creating a loop** You can use all of the usual functions; just be sure to use them as the methods of your object:
    *   Instead of `have_posts()`, use `$category_posts->have_posts()`.
    *   Instead of `the_post()`, use `$category_posts->the_post()`.
4.  **Resume business as usual** Once you’ve done the above, you can use all of the template tags you’ve come to know and love.

If you look at this in detail, you will find that the global <code>$post</code> object is also available. This means that if you use a custom loop like this within another loop, things can go wrong. Be sure to store the original value of the <code>$post</code> object and restore it after the loop.

<pre><code class="language-php">&lt;?php
   $temp_post = $post; // Storing the object temporarily
   $my_query = new WP_Query();
   while($my_query-&gt;have_posts()) {
      // Loop in here
   }
   $post = $temp_post; // Restore the value of $post to the original
?&gt;</code></pre>

## Digging Deeper

### The Power of a Good Argument

The ease with which we can create loops is obvious, but what about actually querying for posts? Let me show you a common technique I use when creating sliders for commercial themes.

In many cases, users of your theme will want a great-looking slider, but they might be a bit lazy in creating content. Many users will also want to show future content. Let’s query for upcoming (i.e. unpublished) posts that have an attached featured image.

<pre><code class="language-php">&lt;?php
   $args = array(
      'post_status' =&gt; 'future',
      'meta_query' =&gt; array(
         array(
            'key' =&gt; '_thumbnail_id',
            'value' =&gt; ’,
            'compare' =&gt; '!='
         )
      )
   );
   $slider_posts = new WP_Query($args);
?&gt;

&lt;?php if($slider_posts-&gt;have_posts()) : ?&gt;

&lt;div class='slider'&gt;
   &lt;?php while($slider_posts-&gt;have_posts()) : $slider_posts-&gt;the_post() ?&gt;
      &lt;div class='slide'&gt;
         &lt;?php the_post_thumbnail() ?&gt;
      &lt;/div&gt;
   &lt;?php endwhile ?&gt;
&lt;/div&gt;

&lt;?php endif ?&gt;</code></pre>

Short, sweet and utterly understandable — just beautiful. And we’ve just scraped the surface.</p>

### Know Your Defaults

You may have noticed that I didn’t specify a number of things in my queries. What about how many posts to list? What about the post’s status in the first query we made?

Default values are supplied for many of the most common arguments. Here are a few that you don’t have to specify, unless you want to change them:

*   `posts_per_page` Defaults to the value specified in the reading settings for the number of posts to list.
*   `post_type` Defaults to `post`.
*   `post_status` Defaults to `publish`.

You can find the complete list of parameters <a href="https://codex.wordpress.org/Class_Reference/WP_Query#Parameters">in the Codex</a>, of course!

### Arrays Are Awesome

In many cases, you will want to specify a number of values that an argument can take. Where it would seem logical, <code>WP_Query</code> usually allows you to use arrays to make your life easier. Here are a few examples:

*   You can use an array for `post_status` to pull posts from a number of different statuses. Note that you can use the string `any` to get posts from all statuses.
*   If you use custom post types, you’ll be happy to hear that you can use an array for the value of the `post_type` parameter as well.
*   For the taxonomy type parameters `category__in`, `tag__in` and so on, you can use an array to indicate a multitude of values.</p>

### Handling Taxonomies

<code>WP_Query</code> is nice enough to offer a simple way to make advanced taxonomy queries as well. This is especially useful for websites with complex set-ups and for commercial themes with large feature sets. The mechanism used is called <code>tax_query</code>. Let’s look at an example.

Say you have a website all about movies. You store movies in a custom “movie” post type; you have a custom taxonomy for genre, a custom taxonomy for actors, and you use the regular ol’ category to indicate how good a movie is. Let’s find all “Action” movies starring “Bruce Willis” that aren’t “Bad”:

<pre><code class="language-php">&lt;?php
   $args = array(
      'post_type' =&gt; 'movie',
      'tax_query' =&gt; array(
         'relation' =&gt; 'AND',
         array(
            'taxonomy' =&gt; 'category',
            'field' =&gt; 'slug',
            'terms' =&gt; array('bad')
            'operator' =&gt; 'NOT IN'
         ),
         array(
            'taxonomy' =&gt; 'genre',
            'field' =&gt; 'slug',
            'terms' =&gt; array('action')
         ),
         array(
            'taxonomy' =&gt; 'actor',
            'field' =&gt; 'slug',
            'terms' =&gt; array('Bruce Willis'),
         )
      )
   );
?&gt;</code></pre>

While this hardcoded example would be useful only to people who love Die Hard, it’s not hard to see how an advanced filter can be built that lets users filter through your content in any which way they want.

Learn more about all of the awesome things you can do with the <a href="https://codex.wordpress.org/Class_Reference/WP_Query#Taxonomy_Parameters">taxonomy parameters in the Codex</a>.</p>

### Having Fun With Meta Data

You’ve already seen that <code>WP_Query</code> is great at handling meta data — we used a <code>meta_query</code> in the second example to build a slider from posts that have featured images. Just as with the taxonomy queries, a lot of flexibility is built in here.

We’re currently building a WordPress theme to be used to create a Web page for apartment(s) for rent. We store apartments as a custom post type and use meta data to store the details. With a meta query, we can easily pull in all apartments that can house four or more people, that have a balcony and that are non-smoking.

<pre><code class="language-php">&lt;?php
   $args = array(
      'post_type' =&gt; 'apartment',
       'meta_query' =&gt; array(
         'relation' =&gt; 'AND',
          array(
             'key' =&gt; 'persons',
             'value' =&gt; '4',
             'compare' =&gt; '&gt;=',
             'type' =&gt; 'NUMERIC'
          ),
          array(
             'key' =&gt; 'balcony',
             'value' =&gt; '1',
             'type' =&gt; 'BINARY',
             'compare' =&gt; '='
          ),
          array(
             'key' =&gt; 'smoking',
             'value' =&gt; '0',
             'type' =&gt; 'BINARY',
             'compare' =&gt; '='
          )
       )
   );
?&gt;</code></pre>

Again, this is very modular, very understandable. To learn more about the parameters you can use, just visit the “<a href="https://codex.wordpress.org/Class_Reference/WP_Query#Custom_Field_Parameters">Custom Field Parameters</a>” section in the <code>WP_Query</code> documentation.</p>

## Methods And Properties

Once you’ve made a query, you can coax a lot of information out of your object. You can find a full list of “<a href="https://codex.wordpress.org/Class_Reference/WP_Query#Methods_and_Properties">Methods and Properties</a>” in the Codex. Here are the ones I tend to use most:

*   `$query`
Shows you the query string passed to the `$wp_query` object. This is quite helpful for troubleshooting in some advanced cases.
*   `$query_vars`
Shows an associative array of the arguments you’ve passed. If you do plenty of mixing and matching before passing arguments, this tool could be helpful indeed to check that all is well.
*   `$posts`
Holds the requested posts from the database. I rarely use this property, but it’s good to know that this is where your items come from.
*   `$found_posts`
A handy little thing that shows the total number of found items (without the limit imposed by the `posts_per_page` argument).</p>

## With Great Power Comes Great Responsibility

While <code>WP_Query</code> gives you plenty to play around with, it does have its drawbacks. Many people (my past self included) go nuts when they realize how easy it is to bang out queries all over the place.

Keep in mind that more queries mean more server load. I’ve found that on hosted systems, complex queries can be especially naughty because they eat at your RAM, which is probably your scarcest resource.

Make sure to check out what the default query holds on each page. What’s the sense in creating a new query for the latest posts on the front page if it’s there by default? Use what you can more than once, cache results, and so on.

{{< signature "al" >}}


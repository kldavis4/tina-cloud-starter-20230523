---
title: 'Building An Advanced WordPress Search With WP_Query'
slug: advanced-wordpress-search-with-wp_query
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9606e07d-0f3f-4116-913c-6a20452efe9d/01-super-preview-opt.png
date: 2016-03-29T15:46:51.000Z
author: carlodaniele
summary: >-
  This article will show you how to provide your WordPress installation with an advanced search system allowing the user to search and retrieve content from a specific custom post type, filtering results by custom taxonomy terms and multiple custom field values. It will cover both a theoretical introduction to handling user requests and a concrete application of that theory, particularly, building an advanced search system.
description: >-
  This article covers both a theoretical introduction to handling user requests and a concrete application of that theory, particularly, building an advanced search system.
categories:
  - WordPress
  - Search
  - Techniques (WP)
---
Many WordPress superpowers come from its flexible data architecture that allows developers to widely customize their installations with custom post types, taxonomies and fields. However, when it comes down to its search, WordPress provides us with only one-field form that often appears inadequate and leads site admins to adopt external search systems, like Google Custom Search, or third-party plugins.

In this article I’ll show you how to provide your WordPress installation with an advanced search system allowing the user to **search and retrieve content from a specific custom post type**, filtering results by custom taxonomy terms and multiple custom field values.

The article has two parts. First, I will present a theoretical introduction to handling user requests, starting from the URL transmission, passing through the query execution, and ending with the output production. The second part of the article is a concrete application of what we’re going to learn in the first part, and there we will build our advanced search system.

So, let’s start learning some key concepts.

## User Requests

When a user clicks on a link or types a URL pointing to a page of the website, WordPress performs a series of operations described well in the WP Query Code Reference [Query Overview](https://codex.wordpress.org/Query_Overview). Briefly, this is what happens:

1.  WordPress parses the requested URL into a set of query parameters (called query specification).
2.  All the `is_` variables related to the query are set.
3.  The query specification is converted into a MySQL query, which is executed against the database.
4.  The retrieved dataset is stored in the `$wp_query` object.
5.  WordPress then handles 404 errors.
6.  WordPress sends blog HTTP headers.
7.  The Loop variables are initialized.
8.  The template file is selected according to the template hierarchy rules.
9.  WordPress runs the Loop.

URL parsing comes first, so let’s dive into query strings and variables.

### WP Query Vars: Defaults And Custom Variables

The WP Query Code Reference states at [WordPress Query Vars](https://codex.wordpress.org/WordPress_Query_Vars):

<blockquote>“An array of query vars are available for WordPress users or developers to utilise in order to query for particular types of content or to aid in theme and/or plugin design and functionality.”<br /><br />— <a href='https://developer.wordpress.org/reference/classes/wp_query'>WP Query Code Reference</a></blockquote>

In other words, WordPress query vars are those variables in a query string that determine (or affect) results in a query performed against the database. By default, WordPress provides public and private query vars, and the WP Query Code Reference defines them as follows:

<blockquote>“Public query vars are those available and usable via a direct URL query in the form of <code>example.net/?var1=value1&amp;var2=value2</code>. Private query vars cannot be used in the URL, although WordPress will accept a query string with private query vars, the values will not be passed into the query and should be placed directly into the query. An example is given below.<br /><br /><code>`query_posts('privatevar=myvalue');</code>”<br /><br />— <a href='https://developer.wordpress.org/reference/classes/wp_query'>WP Query Code Reference</a></blockquote>

As a consequence, it’s not possible to send via a query string private vars like `category__in`, `category__not_in`, `category__end`, etc. Check the WP Query Code Reference for a comprehensive list of the [built-in query vars](https://codex.wordpress.org/WordPress_Query_Vars#Query_variables).

With the public variables at our disposal (as users as well as developers), we can assemble a great number of queries with no need to develop a plugin or edit the theme’s functions file. We just need to build a URL, add to the query string one or more of the available parameters, and WordPress will show the requested results to the user.

As an example, we can query for a specific post type by adding the `post_type` parameter to the query string; or we can request a custom taxonomy, appending to the query string the pair `taxonomy-name=taxonomy-term`. For instance, we can build the following URL:

<pre><code class="language-markup">mywebsite.com/?post_type=movie&amp;genre=thriller</code></pre>

WordPress will query the database and retrieve all `movie` post types belonging to the `thriller` genre, where `genre` is a custom taxonomy.

It’s awesome, but that’s not all. What we have said so far, in fact, concerns just the built-in functionalities of query vars. WordPress allows us to go further and create our own custom query variables.

### Register Custom Query Vars

Before we can use them, the custom query vars should be registered. We can accomplish this task thanks to the `query_vars` filter. So, let’s open the main file of a plugin (or a theme’s *functions.php* file) and write the following code:

<div class="break-out">

<pre><code class="language-php">/**
 * Register custom query vars
 *
 * @link https://codex.wordpress.org/Plugin_API/Filter_Reference/query_vars
 */
function myplugin_register_query_vars( $vars ) {
	$vars[] = 'author';
	$vars[] = 'editor';
	return $vars;
}
add_filter( 'query_vars', 'myplugin_register_query_vars' );
</code></pre>
</div>

The callback function keeps an array of variables as an argument, and must return the same array when new variables have been added.

Now we can include the new variables in the parameters that will affect the query. These parameters will be available in our scripts thanks to the `get_query_var()` template tag, as we’ll see later. Now it’s time to introduce the class that manages the queries in WordPress.

### Her Majesty The `WP_Query`

Querying a database is not an easy task. It’s not only a matter of building an efficient query, but it’s a problem that requires security issues to be carefully taken into account. Thanks to [`WP_Query` Class](https://codex.wordpress.org/Class_Reference/WP_Query), WordPress gives us access to the database quickly (no need to get our hands dirty with SQL) and securely (`WP_Query` builds safe queries behind the scenes).

The retrieved dataset will be available for use in the [Loop](https://codex.wordpress.org/The_Loop), thanks to the many methods and properties of the class.

Let’s take a generic Loop as an example:

<pre><code class="language-php">&lt;?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?&gt;
	&lt;!-- code here --&gt;
&lt;?php endwhile; else : ?&gt;
	&lt;!-- code here --&gt;
&lt;?php endif; ?&gt;
</code></pre>

If you are new to WordPress development, you may ask: “Hey, buddy! Where’s the Query?”

In fact, you don’t need to create a new instance of the `WP_Query` object. The class itself establishes the query to be executed according to the requested page. So, if the site viewer requires a category archive, WordPress will run a query retrieving all posts belonging to that specific category, and the Loop will show them.

But this is just a vary basic example of a main query. We can do a lot of more, and filter the returning result set granularly, just by passing an array of parameters to a new instance of the `WP_Query` class, as we’ll do in the following example:

<pre><code class="language-php">// An array of arguments
$args = array( 'arg_1' =&gt; 'val_1', 'arg_2' =&gt; 'val_2' );

// The Query
$the_query = new WP_Query( $args );

// The Loop
if ( $the_query-&gt;have_posts() ) {

	while ( $the_query-&gt;have_posts() ) : $the_query-&gt;the_post(); 
		// Your code here
	endwhile;

} else {
        // no posts found
}
/* Restore original Post Data */
wp_reset_postdata();
</code></pre>

Things look a bit more complicated, don’t they? But if we look closely, they’re not.

The new instance of `WP_Query` keeps an array of arguments that will affect data retrieved from the database. The WP Query Code Reference provides the [full list of parameters](https://codex.wordpress.org/Class_Reference/WP_Query#Parameters), grouping them in seventeen categories. So, for instance, we have [Author Params](https://developer.wordpress.org/reference/classes/wp_query/#author-parameters), [Category Params](https://developer.wordpress.org/reference/classes/wp_query/#category-parameters), just one [Search parameter](https://developer.wordpress.org/reference/classes/wp_query/#search-parameters) (`s`), [Custom Field params](https://developer.wordpress.org/reference/classes/wp_query/#custom-field-post-meta-parameters), and so on (we’ll get back to `WP_Query` params in a moment).

Now that we have instantiated the `$query` object, we can access all its [properties and methods](https://developer.wordpress.org/reference/classes/wp_query/#properties-and-methods). `have_posts` checks whether any post remains to be printed, while `the_post` moves the Loop forward to the succeeding post and updates the `$post` global variable.

Outside the Loop, when using a custom query, we should always make a call to `wp_reset_postdata()`. This function restores the `$post` global variable after the execution of a custom query, and is necessary because any new query overwrites `$post`. From the WP Query Code Reference:  

<blockquote>“Note: If you use `the_post()` with your query, you need to run `wp_reset_postdata()` afterwards to have Template Tags use the main query’s current post again.”<br /><br />— <a href='https://developer.wordpress.org/reference/classes/wp_query'>WP Query Code Reference</a></blockquote>

Now let’s get back to the query args.

{{% feature-panel %}}

### `WP_Query` Arguments

We said that the `WP_Query` class keeps an array of [parameters](https://developer.wordpress.org/reference/classes/wp_query/#parameters) that allow developers to select granularly the results from the database.

The first group, the Author Parameters, includes those arguments that allow us to build queries based on the author(s) of the posts (pages and post types). They include:

*   `author`
*   `author_name`
*   `author__in`
*   `author__not_in`

If you want to retrieve all the posts from `carlo`, you just need to set the following query:

<pre><code class="language-php">$query = new WP_Query( array( 'author_name' =&gt; 'carlo' ) );</code></pre>

The second group includes the Category Parameters, i.e. all those arguments that allow us to query for (or exclude) posts assigned to one or more categories:

*   `cat`
*   `category_name`
*   `category__and`
*   `category__in`
*   `category__not_in`

If we needed all posts assigned to the `webdesign` category, we just have to set the `category_name` argument, as we’ll do in the following example:

<pre><code class="language-php">$query = new WP_Query( array( 'category_name' =&gt; 'webdesign' ) );</code></pre>

The following query searches for posts from more than one category, the comma standing in for `OR</code>:

<div class="break-out">

<pre><code class="language-php">$query = new WP_Query( array( 'category_name' =&gt; 'webdesign,webdev' ) );</code></pre>
</div>

We can also ask for posts belonging to both `webdesign` and `webdev` categories, with plus (`+</code>) meaning `AND</code>:

<div class="break-out">

<pre><code class="language-php">$query = new WP_Query( array( 'category_name' =&gt; 'webdesign+webdev' ) );</code></pre>
</div>

And we can also pass an array of IDs, as in the next examples:

<pre><code class="language-php">$query = new WP_Query( array( 'category__in' =&gt; array( 4, 9 ) ) );
$query = new WP_Query( array( 'category__and' =&gt; array( 4, 9 ) ) );
</code></pre>

And so on with tags and taxonomies, search keywords, posts, pages and post types. Refer to the WP Query Code Reference for a [more detailed walk-through](https://developer.wordpress.org/reference/classes/wp_query/#parameters) of query arguments.

As we said before, we can also set more than one argument and retrieve, for instance, all posts in a specific category `AND` written by a certain author:

<div class="break-out">

<pre><code class="language-php">$query = new WP_Query( array( 'author_name' =&gt; 'carlo', 'category_name' =&gt; 'webdesign' ) );</code></pre>
</div>

When the data architecture get more complex &mdash; and that occurs when we add custom fields and taxonomies to post types &mdash; then it could become necessary to set one or more [Custom Field parameters](https://developer.wordpress.org/reference/classes/wp_query/#custom-field-post-meta-parameters) allowing us to retrieve all posts (or custom post types) labeled with specific custom field values. Shortly, we’ll need to execute a meta query against the database.

### WordPress Meta Queries

The WP Query Code Reference informs us that when dealing with a meta query, `WP_Query` uses the [`WP_Meta_Query` class](https://developer.wordpress.org/reference/classes/wp_meta_query/). This class, introduced in WordPress 3.2, builds the SQL code of the queries based on custom fields.

To build a query based on a single custom field, we just need one or more of the following arguments:

*   `meta_key`
*   `meta_value`
*   `meta_value_num`
*   `meta_compare`

Suppose a custom post type is named `accommodation`. Let’s assign to each `accommodation` a custom field named `city`, which stores the name of a geographical location. With a meta query we can retrieve from the database all accommodations located in the specified city, simply passing the right arguments to the query, as you can see below:

<pre><code class="language-php">$args = array( 
	'post_type'		=&gt; 'accommodation', 
	'meta_key'		=&gt; 'city', 
	'meta_value'		=&gt; 'Freiburg', 
	'meta_compare'	=&gt; 'LIKE' );
</code></pre>

Once we’ve set the arguments, we can build the query the same way as before:

<pre><code class="language-php">// The Query
$the_query = new WP_Query( $args );

// The Loop
if ( $the_query-&gt;have_posts() ) {

	while ( $the_query-&gt;have_posts() ) : $the_query-&gt;the_post(); 
		// Your code here
	endwhile;

} else {
        // no posts found
}
/* Restore original Post Data */
wp_reset_postdata();
</code></pre>

Copy and paste the code above in a template file and you’ll get an archive of all accommodations available in Freiburg.

This is the case for a single custom field. But what if we needed to build a query based on multiple custom fields?

### The `meta_query` Argument

For this kind of query, the `WP_Meta_Query` class (and the `WP_Query` class as well) provides the `meta_query` parameter. This has to be an array of arrays, as shown in the following example:

<pre><code class="language-php">$args = array(
	'post_type'  =&gt; 'accommodation',
	'meta_query' =&gt; array(
		array(
			'key'     =&gt; 'city',
			'value'   =&gt; 'Freiburg',
			'compare' =&gt; 'LIKE',
		),
	)
);
</code></pre>

The `meta_query` element is a bidimensional array whose items are single meta queries with the following arguments:

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th>Argument</th>
			<th>Type</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>key</code></td>
			<td><em>string</em></td>
			<td>Identifies the custom field.</td>
		</tr>
		<tr>
			<td><code>value</code></td>
			<td><em>string|array</em></td>
			<td>Can be an array just when the <code>compare</code> value is <code>'IN'</code>, <code>'NOT IN'</code>, <code>'BETWEEN'</code>, or <code>'NOT BEETWEEN'</code>.</td>
		</tr>
		<tr>
			<td><code>compare</code></td>
			<td><em>string</em></td>
			<td>A comparison operator. Accepted values are <code>'='</code>, <code>'!='</code>, <code>'&gt;'</code>, <code>'&gt;='</code>, <code>'&lt;'</code>, <code>'&lt;='</code>, <code>'LIKE'</code>, <code>'NOT LIKE'</code>, <code>'IN'</code>, <code>'NOT IN'</code>, <code>'BETWEEN'</code>, <code>'NOT BETWEEN'</code>, <code>'EXISTS'</code>, <code>'NOT EXISTS'</code>, <code>'REGEXP'</code>, <code>'NOT REGEXP'<code> and <code>'RLIKE'</code>. It defaults to <code>'='</code>.</td>
		</tr>
		<tr>
			<td><code>type</code></td>
			<td><em>string</em></td>
			<td>The custom field type. Possible values are <code>'NUMERIC'</code>, <code>'BINARY'</code>, <code>'CHAR'</code>, <code>'DATE'</code>, <code>'DATETIME'</code>, <code>'DECIMAL'</code>, <code>'SIGNED'</code>, <code>'TIME'</code>, <code>'UNSIGNED'</code>. It defaults to <code>'CHAR'</code>.</td>
		</tr>
	</tbody>
</table>

If we set more than one custom field, we also have to assign the `relation` argument to the `meta_query` element.

Now we can build a more advanced query. Let’s begin by setting the arguments and creating a new instance of `WP_Query`:

<div class="break-out">

<pre><code class="language-php">$args = array(
	'post_type'	=&gt; 'accommodation',
	'meta_query'	=&gt; array(
		array( 'key' =&gt; 'city', 'value' =&gt; 'Paris', 'compare' =&gt; 'LIKE' ),
		array( 'key' =&gt; 'type', 'value' =&gt; 'room', 'compare' =&gt; 'LIKE' ),
		'relation' =&gt; 'AND'
	)
);
$the_query = new WP_Query( $args );
</code></pre>
</div>

Here, the `meta_query` argument holds two meta query arrays and a third parameter setting the relation between the meta queries. The query searches the *wp_posts* table for all `accommodation` post types where the custom fields `city` and `type` store respectively the values `Paris` and `room`.

Let’s copy and paste the code into a template file named *archive-accommodation.php*. When requested, WordPress will execute the query searching the *wp_posts* table, and the Loop will show the results, if available.

At this point we’re still writing the code in a template file. This means that our script is static and each time the Loop runs, it will produce the same output. But we need to allow site users to make custom requests, and to accomplish this task we need to dynamically build custom queries.

### The `pre_get_posts` Filter

The [`pre_get_posts` action hook](https://developer.wordpress.org/reference/hooks/pre_get_posts/) is fired after the `$query` object creation, but before its execution. To modify the query, we’ll have to hook a custom callback to `pre_get_posts`.

In an earlier example, we queried the database to retrieve all posts in the `webdesign` category from a certain author. In the following example we’re passing the same arguments to the `$query` object, but we won’t do the job with a template file, as we’ve done before, but we’ll use the main file of a plugin (or a theme’s *functions.php*), instead. Let’s write the following block of code:

<pre><code class="language-php">function myplugin_pre_get_posts( $query ) {
	// check if the user is requesting an admin page 
	// or current query is not the main query
	if ( is_admin() || ! $query-&gt;is_main_query() ){
		return;
	}
	$query-&gt;set( 'author_name', 'carlo' );
	$query-&gt;set( 'category_name', 'webdesign' );
}
add_action( 'pre_get_posts', 'myplugin_pre_get_posts', 1 );
</code></pre>

The `$query` object is passed to the callback function by reference, not by value, and this means that any changes made to the query directly affect the original `$query` object. The WP Query Code Reference says:

<blockquote>“The <code>pre_get_posts</code> action gives developers access to the <code>$query</code> object by reference (any changes you make to <code>$query</code> are made directly to the original object &mdash; no return value is necessary).”<br /><br />— <a href='https://developer.wordpress.org/reference/classes/wp_query'>WP Query Code Reference</a></blockquote>

As we’re manipulating the original `$query` object, we have to pay attention to which query we’re working on. The `is_main_query` method checks if the current `$query` object is… (yes!) the main query. The WP Query Code Reference also informs us that the `pre_get_posts` filter can affect the admin panel as well as the front-end pages. For this reason, it’s more than appropriate to check the requested page with the `is_admin` conditional tag as well.

The `pre_get_posts` action hook is well documented and it’s well worth reading the WP Query Code Reference for [a more detailed description and several examples of use](https://developer.wordpress.org/reference/hooks/pre_get_posts/).

We can now end our introduction to the the main tools available to handle WordPress queries. Now it’s time to present a concrete example of their use, building an advanced search system of the site content. Our case study is provided by a real estate website.

{{% ad-panel-leaderboard %}}

## From Theory To Code: Building The Search System

We will follow these steps:

1.  Define the data structure.
2.  Register the custom query vars.
3.  Get the query var values and use them to build a custom query.
4.  Build a form programmatically generating the field values.

### 1. Define The Data Structure

The purpose of the custom post types is to add contents that logically can be included neither in blog posts nor in static pages. Custom post types are particularly appropriate to present events, products, books, movies, catalogue items, and so on. Here we’re going to build an archive of real estate ads with the following structure:

*   **custom post type**: `accommodation`
*   **custom taxonomy**: `typology` (B&B, homestay, hotel, etc.)
*   **custom field**: `_sm_accommodation_type` (entire house, private room, shared room)
*   **custom field**: `_sm_accommodation_city`
*   **other custom fields.**

We have to register the post type, the custom taxonomy and custom fields and meta boxes, as shown in the figure below.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c98853a4-a031-4cca-9e70-d9f4246544d1/02-new-accommodation-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3aace401-a3ba-4c77-b1c6-ab8cd4d10452/02-new-accommodation-preview-opt.png" width="800" height="927" alt="Accommodation edit page" /></a><figcaption>The edit accommodation page shows all custom meta boxes and fields. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3aace401-a3ba-4c77-b1c6-ab8cd4d10452/02-new-accommodation-preview-opt.png">View large version</a>)</figcaption></figure>

The image shows how the **Edit Accommodation** page will appear once three custom meta boxes containing the *Typology* custom taxonomy and several custom fields have been registered.

It’s not our goal to analyze WordPress data architecture, as this topic has already been covered here on Smashing Magazine by [Daniel](https://www.smashingmagazine.com/2012/11/complete-guide-custom-post-types/), [Brian](https://www.smashingmagazine.com/2015/04/extending-wordpress-custom-content-types/), [Kevin](https://www.smashingmagazine.com/2012/01/create-custom-taxonomies-wordpress/), [Josh](https://www.smashingmagazine.com/2014/08/customizing-wordpress-archives-categories-terms-taxonomies/) and [Justin](https://www.smashingmagazine.com/2011/10/create-custom-post-meta-boxes-wordpress/). Read their articles if you need a refresher, and come back as soon as you’re ready.

Once we’ve defined the data architecture, it’s time to register the query vars.

### 2. Register The Query Variables

Earlier we defined query vars as `key=value` pairs following a question mark in a URL. But before we can handle these pairs in our scripts, we have to register them in a plugin or functions file. For our purposes, we need just two variables that will enable the execution of a query based on the values of the corresponding custom fields:

<div class="break-out">

<pre><code class="language-php">/**
 * Register custom query vars
 *
 * @link https://codex.wordpress.org/Plugin_API/Filter_Reference/query_vars
 */
function sm_register_query_vars( $vars ) {
	$vars[] = 'type';
	$vars[] = 'city';
	return $vars;
} 
add_filter( 'query_vars', 'sm_register_query_vars' );</code></pre>
</div>

That’s it! We have added two more parameters to query the database. Now it would make sense to build a URL like this one:

<pre><code class="language-http">https://example.com/?type=XXX&amp;city=YYY</code></pre>

### 3. Manipulate The Query

Now let’s add a new block of code to our script:

<div class="break-out">

<pre><code class="language-php">/**
 * Build a custom query based on several conditions
 * The pre_get_posts action gives developers access to the $query object by reference
 * any changes you make to $query are made directly to the original object. No return value is requested
 *
 * @link https://codex.wordpress.org/Plugin_API/Action_Reference/pre_get_posts
 *
 */
function sm_pre_get_posts( $query ) {
	// check if the user is requesting an admin page 
	// or current query is not the main query
	if ( is_admin() || ! $query-&gt;is_main_query() ){
		return;
	}

	// edit the query only when post type is 'accommodation'
	// if it isn't, return
	if ( !is_post_type_archive( 'accommodation' ) ){
		return;
	}

	$meta_query = array();

	// add meta_query elements
	if( !empty( get_query_var( 'city' ) ) ){
		$meta_query[] = array( 'key' =&gt; '_sm_accommodation_city', 'value' =&gt; get_query_var( 'city' ), 'compare' =&gt; 'LIKE' );
	}

	if( !empty( get_query_var( 'type' ) ) ){
		$meta_query[] = array( 'key' =&gt; '_sm_accommodation_type', 'value' =&gt; get_query_var( 'type' ), 'compare' =&gt; 'LIKE' );
	}

	if( count( $meta_query ) &gt; 1 ){
		$meta_query['relation'] = 'AND';
	}

	if( count( $meta_query ) &gt; 0 ){
		$query-&gt;set( 'meta_query', $meta_query );
	}
}
add_action( 'pre_get_posts', 'sm_pre_get_posts', 1 );
</code></pre>
</div>

This code is the sum of all we covered in the first part of the article. The callback function quits if the user is in the admin panel, if the current query is not the main query, and if the post type is not `accommodation`.

Later, the function checks if any of the query vars we’ve registered before are available. This task is accomplished thanks to the `get_query_var` function, which retrieves a public query variable from an HTTP request. Read more about `get_query_var` [in the WP Query Code Reference](https://developer.wordpress.org/reference/functions/get_query_var/). If the variable exists, then the callback defines one array for each meta query and pushes it into the multi-dimensional `$meta_query` array.

Finally, if at least two meta queries are available, then the `relation` argument is pushed into `$meta_query` and its value is set to `'AND'`. Once done, the `set` method saves `$query` for its subsequent execution.

You don’t need to worry about data sanitization here, because the `WP_Query` and `WP_Meta_Query` classes do the job for us &mdash; check [the `WP_Query`](https://core.trac.wordpress.org/browser/tags/4.4.1/src/wp-includes/query.php) and [`WP_Meta_Query` source code](https://core.trac.wordpress.org/browser/tags/4.4.1/src/wp-includes/class-wp-meta-query.php).

### 4. Build The Search Form

The form data are submitted with the `GET` method. This means that the `name` and `value` attributes of the form fields are sent as URL variables (i.e. as query vars). So we’re going to give the `name` attributes of the form fields the same values as the previously registered query vars (`city` and `type`), while the field values could be assigned programmatically, retrieving data from the database, or filled in by the user.

First we will create a shortcode that will allow the site admin to include a search form in posts and pages of the website. Our shortcode will be hooked to the `init` action:

<pre><code class="language-php">function sm_setup() {
	add_shortcode( 'sm_search_form', 'sm_search_form' );
}
add_action( 'init', 'sm_setup' );
</code></pre>

Next we will define the callback function that will produce the HTML of a form containing three select fields, corresponding to a custom taxonomy and two custom fields.

<pre><code class="language-php">function sm_search_form( $args ){
	// our code here
}
</code></pre>

`$args` is an array of the shortcode attributes. Inside the function we’ll add the following code:

<div class="break-out">

<pre><code class="language-php">// The Query
// meta_query expects nested arrays even if you only have one query
$sm&#95;query = new WP&#95;Query( array( 'post_type' =&gt; 'accommodation', 'posts&#95;per&#95;page' =&gt; '-1', 'meta&#95;query' =&gt; array( array( 'key' =&gt; '&#95;sm&#95;accommodation&#95;city' ) ) ) );

// The Loop
if ( $sm&#95;query-&gt;have&#95;posts() ) {
	$cities = array();
	while ( $sm_query-&gt;have_posts() ) {
		$sm_query-&gt;the_post();
		$city = get_post_meta( get&#95;the&#95;ID(), '&#95;sm&#95;accommodation&#95;city', true );

		// populate an array of all occurrences (non duplicated)
		if( !in_array( $city, $cities ) ){
			$cities[] = $city;    
		}
	}
}
} else{
       echo 'No accommodations yet!';
       return;
}

/* Restore original Post Data &#42;/
wp&#95;reset&#95;postdata();

if( count($cities) == 0){
	return;
}

asort($cities);

$select_city = '&lt;select name="city" style="width: 100%"&gt;';
$select_city .= '&lt;option value="" selected="selected"&gt;' . &#95;&#95;( 'Select city', 'smashing_plugin' ) . '&lt;/option&gt;';
foreach ($cities as $city ) {
	$select&#95;city .= '&lt;option value="' . $city . '"&gt;' . $city . '&lt;/option&gt;';
}
$select&#95;city .= '&lt;/select&gt;' . "\n";

reset($cities);</code></pre>
</div>

We’ve built a query that will retrieve all `accommodation` post types having set a custom field named `&#95;sm&#95;accommodation&#95;city` (the underscore preceding the name represents a hidden custom field).

The Loop won’t show any accommodation, but will add elements to the `$cities` array from the corresponding custom field value. The condition will skip duplicates. If no accommodations are available, the execution is interrupted; otherwise the array elements are sorted and used to print the values of the first group of `option` elements.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a6203b1-c3e4-471b-b3b9-11b845e8cc40/03-select-city-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a6203b1-c3e4-471b-b3b9-11b845e8cc40/03-select-city-preview-opt.png" width="500" height="175" alt="Select box" /></a><figcaption>All available cities are shown as options in a select box.</figcaption></figure>

The second form field is still a select button, and it corresponds to the `typology` custom taxonomy. The values of the second group of `option` elements are provided by [the `get_terms` template tag](https://developer.wordpress.org/reference/functions/get_terms/). Here follows the second block of code, generating a new `select` field corresponding to the `typology` taxonomy:

<div class="break-out">

<pre><code class="language-php">$args = array( 'hide_empty' =&gt; false );
$typology_terms = get_terms( 'typology', $args );
if( is_array( $typology_terms ) ){
	$select_typology = '&lt;select name="typology" style="width: 100%"&gt;';
	$select_typology .= '&lt;option value="" selected="selected"&gt;' . __( 'Select typology', 'smashing_plugin' ) . '&lt;/option&gt;';
	foreach ( $typology_terms as $term ) {
		$select_typology .= '&lt;option value="' . $term-&gt;slug . '"&gt;' . $term-&gt;name . '&lt;/option&gt;';
	}
	$select_typology .= '&lt;/select&gt;' . "\n";
}</code></pre>
</div>

`get_terms` returns an array of all terms of the taxonomy set as first argument, or a `WP_Error` object if the taxonomy does not exist. Now again a `foreach` cycle prints out the option elements.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d315c13a-509d-4430-afa9-e50cc89030c6/04-select-typology-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d315c13a-509d-4430-afa9-e50cc89030c6/04-select-typology-preview-opt.png" width="500" height="236" alt="Select box" /></a><figcaption>The options of the second select box.</figcaption></figure>

Then we build the last `select` element, corresponding to the `type` custom field. Here is the code:

<div class="break-out">

<pre><code class="language-php">$select_type = '&lt;select name="type" style="width: 100%"&gt;';
$select_type .= '&lt;option value="" selected="selected"&gt;' . __( 'Select room type', 'smashing_plugin' ) . '&lt;/option&gt;';
$select_type .= '&lt;option value="entire"&gt;' . __( 'Entire house', 'smashing_plugin' ) . '&lt;/option&gt;';
$select_type .= '&lt;option value="private"&gt;' . __( 'Private room', 'smashing_plugin' ) . '&lt;/option&gt;';
$select_type .= '&lt;option value="shared"&gt;' . __( 'Shared room', 'smashing_plugin' ) . '&lt;/option&gt;';
$select_type .= '&lt;/select&gt;' . "\n";
</code></pre>
</div>

As you can see, in this case we have manually set the option values.

Finally, we can print out the form:

<div class="break-out">

<pre><code class="language-php">$output = '&lt;form action="' . esc_url( home_url() ) . '" method="GET" role="search"&gt;';
$output .= '&lt;div class="smselectbox"&gt;' . esc_html( $select_city ) . '&lt;/div&gt;';
$output .= '&lt;div class="smselectbox"&gt;' . esc_html( $select_typology ) . '&lt;/div&gt;';
$output .= '&lt;div class="smselectbox"&gt;' . esc_html( $select_type ) . '&lt;/div&gt;';
$output .= '&lt;input type="hidden" name="post_type" value="accommodation" /&gt;';
$output .= '&lt;p&gt;&lt;input type="submit" value="Go!" class="button" /&gt;&lt;/p&gt;&lt;/form&gt;';

return $output;</code></pre>
</div>

We’ve set a hidden input field for the `post_type` public query var. When the user submits the form, WordPress gets the `post_type` value, and loads the *archive.php* template file, or, if available, the *archive-{post_type}.php* file. With this kind of form, if you’re going to customize the HTML structure of the resulting page, you’ll need to provide the most appropriate template file.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71b07677-32dc-404f-9042-6f3ad63c066d/05-wordpress-advanced-search-form-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71b07677-32dc-404f-9042-6f3ad63c066d/05-wordpress-advanced-search-form-preview-opt.png" width="500" height="359" alt="Advanced search form" /></a><figcaption>The image shows the advanced search form we’ve been building through this article.</figcaption></figure>

{{% ad-panel-leaderboard %}}

### A Free Text Search

The form we’ve built so far allows the user to set up three filters from a number of predetermined options. We’re now going to improve the search system including a text field in the form, so that users can search accommodation by custom keywords. We can do that thanks to the `s` [query argument](https://codex.wordpress.org/Class_Reference/WP_Query#Search_Parameter). So, let’s change the form as follows:

<div class="break-out">

<pre><code class="language-php">$output = '&lt;form id="smform" action="' . esc_url( home_url() ) . '" method="GET" role="search"&gt;';
$output .= '&lt;div class="smtextfield"&gt;&lt;input type="text" name="s" placeholder="Search key..." value="' . get_search_query() . '" /&gt;&lt;/div&gt;';
$output .= '&lt;div class="smselectbox"&gt;' . esc_html( $select_city ) . '&lt;/div&gt;';
$output .= '&lt;div class="smselectbox"&gt;' . esc_html( $select_typology ) . '&lt;/div&gt;';
$output .= '&lt;div class="smselectbox"&gt;' . esc_html( $select_type ) . '&lt;/div&gt;';
$output .= '&lt;input type="hidden" name="post_type" value="accommodation" /&gt;';
$output .= '&lt;p&gt;&lt;input type="submit" value="Go!" class="button" /&gt;&lt;/p&gt;&lt;/form&gt;';</code></pre>
</div>

Thanks to the text field, we can pass `WP_Query` a new *key/value* pair, where the key is the `s` parameter, and the value is the user input or the `get_search_query()` returning value. Read [“Get Search Query” in the WP Query Code Reference](https://codex.wordpress.org/Template_Tags/get_search_query) for more details.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5c39160-e30b-4122-b25d-2f33ad225d85/06-wordpress-advanced-search-form-2-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5c39160-e30b-4122-b25d-2f33ad225d85/06-wordpress-advanced-search-form-2-preview-opt.png" width="500" height="381" alt="Advanced search form" /></a><figcaption>A more advanced search form.</figcaption></figure>

A final note: in our preceding example, we’ve seen WordPress loading an archive template file to show the results of the query. That’s because we did not set the search argument. When the query string contains the `s` param, WordPress automatically loads the search template file, as shown in the last image of this post.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa404464-acb4-416a-b1aa-d2891e1000ab/07-ocean-preview-opt.png"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa404464-acb4-416a-b1aa-d2891e1000ab/07-ocean-preview-opt.png" width="500" height="496" alt="Advanced search form" /></a><figcaption>The image shows the search page in Twenty Fifteen.</figcaption></figure>

## Conclusion

The examples of this article are intended to demonstrate what can be achieved with the tools provided by WordPress. Sure, the form can be improved by adding new fields allowing more granular customization. Nevertheless, I hope I’ve provided a quite detailed view of the functionalities that make it possible to build a search system overcoming the limits of the built-in search system with no need of external services and plugins.

Now it’s time to code!

### Resources

*   [Query Overview](https://codex.wordpress.org/Query_Overview)
*   [WP_Query](https://developer.wordpress.org/reference/classes/wp_query/)
*   [WP_Meta_Query](https://developer.wordpress.org/reference/classes/wp_meta_query/)
*   [Custom Queries](https://codex.wordpress.org/Custom_Queries)
*   [WordPress Query Vars](https://codex.wordpress.org/WordPress_Query_Vars)

### Further Reading On Smashing Magazine:

- “[Front-End Author Listing And User Search For WordPress](https://www.smashingmagazine.com/2012/06/front-end-author-listing-user-search-wordpress/),” Cristian Antohe
- “[A Detailed Guide To WordPress Custom Page Templates](https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/),” Nick Schäferhoff
- “[Building An Advanced Notification System For WordPress](https://www.smashingmagazine.com/2015/05/building-wordpress-notification-system/),” Carlo Daniele
- “[How To Create Perfect Emails For Your WordPress Website](https://www.smashingmagazine.com/2011/10/create-perfect-emails-wordpress-website/),” Daniel Pataki

{{< signature "og, yk, il, nl" >}}

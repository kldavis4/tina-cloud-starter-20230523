---
title: Do-It-Yourself Caching Methods With WordPress
slug: diy-caching-methods-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/278956f7-956a-4bfc-b852-f26748ca01d0/wordpress-17.gif
date: 2012-06-26T08:34:09.000Z
author: milan-petrovic
description: >-
  There are different ways to make your website faster: specialized plugins to cache entire rendered HTML pages, plugins to cache all SQL queries and data objects, plugins to minimize JavaScript and CSS files and even some server-side solutions.
categories:
  - WordPress
  - Techniques
---
But even if you use such plugins, using internal caching methods for objects and database results is a good development practice, so that your plugin doesn't depend on which cache plugins the end user has. Your plugin needs to be fast on its own, not depending on other plugins to do the dirty work. And if you think you need to write your own cache handling code, you are wrong. WordPress comes with everything you need to quickly implement varying degrees of data caching. Just identify the parts of your code to benefit from optimization, and choose a type of caching.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Modifying Admin Post Lists In WordPress](https://www.smashingmagazine.com/2013/12/modifying-admin-post-lists-in-wordpress/)
*   [Useful Free Admin Plugins For WordPress](https://www.smashingmagazine.com/2012/03/useful-free-admin-plugins-wordpress/)
*   [Ten Things Every WordPress Plugin Developer Should Know](https://www.smashingmagazine.com/2011/03/ten-things-every-wordpress-plugin-developer-should-know/)
*   [Inside The WordPress Toolbar](https://www.smashingmagazine.com/2012/03/inside-the-wordpress-toolbar/)

WordPress implements two different caching methods:

{{% feature-panel %}}

1.  **Non-persistent** The data remains in the cache during the loading of the page. (WordPress uses this to cache most database query results.)
2.  **Persistent** This depends on the database to work, and cached data can auto-expire after some time. (WordPress uses this to cache RSS feeds, update checks, etc.)

## Non-Persistent Cache

When you use functions such as <code>get_posts()</code> or <code>get_post_meta()</code>, WordPress first checks to see whether the data you require is cached. If it is, then you will get data from the cache; if not, then a database query is run to get the data. Once the data is retrieved, it is also cached. A non-persistent cache is recommended for database results that might be reused during the creation of a page.

The code for WordPress’ internal non-persistent cache is located in the <code>cache.php</code> file in the <code>wp-includes</code> directory, and it is handled by the <code>WP_Object_Cache</code> class. We need to use two basic functions: <code>wp_cache_set()</code> and <code>wp_cache_get()</code>, along with the additional functions <code>wp_cache_add()</code>, <code>wp_cache_replace()</code>, <code>wp_cache_flush()</code> and <code>wp_cache_delete()</code>. Cached storage is organized into groups, and each entry needs its own unique key. To avoid mixing with WordPress’ default data, using your own unique group names is best.</p>

### Example

For this example, we will a create function named <code>d4p_get_all_post_meta()</code>, which will retrieve all meta data associated with a post. This first version doesn't involve caching.

<pre><code class="language-php">function d4p_get_all_post_meta($post_id) {
    global $wpdb;

    $data = array();
    $raw = $wpdb-&gt;get_results( "SELECT meta_key, meta_value FROM $wpdb-&gt;postmeta WHERE post_id = $post_id", ARRAY_A );

    foreach ( $raw as $row ) {
        $data[$row['meta_key']][] = $row['meta_value'];
    }

    return $data;
}</code></pre>

Every time you call this function for the same post ID, an SQL query will be executed. Here is the modified function that uses WordPress’ non-persistent cache:

<pre><code class="language-php">function d4p_get_all_post_meta($post_id) {
    global $wpdb;

    if ( ! $data = wp_cache_get( $post_id, 'd4p_post_meta' ) ) {
        $data = array();
        $raw = $wpdb-&gt;get_results( "SELECT meta_key, meta_value FROM $wpdb-&gt;postmeta WHERE post_id = $post_id", ARRAY_A );

        foreach ( $raw as $row ) {
            $data[$row['meta_key']][] = $row['meta_value'];
        }

        wp_cache_add( $post_id, $data, 'd4p_post_meta' );
    }

    return $data;
}</code></pre>

Here, we are using a cache group named <code>d4p_post_meta</code>, and <code>post_id</code> is the key. With this function, we first check to see whether we need any data from the cache (line 4). If not, we run the normal code to get the data and then add it to the cache in line 13. So, if you call this function more than once, only the first one will run SQL queries; all other calls will get data from the cache. We are using the <code>wp_cache_add</code> function here, so if the key-group combination already exists in the store, it will not be replaced. Compare this with <code>wp_cache_set</code>, which will always overwrite an existing value without checking.

As you can see, we’ve made just a small change to the existing code but potentially saved a lot of repeated database calls during the page’s loading.</p>

### Important Notes

1.  Non-persistent cache is available only during the loading of the current page; once the next page loads, it will be blank once again.
2.  The storage size is limited by the total available memory for PHP on the server. Do not store large data sets, or you might end up with an “Out of memory” message.
3.  Using this type of cache makes sense only for operations repeated more than once in the creation of a page.
4.  It works with WordPress since version 2.0.</p>

## Database-Driven Temporarily Persistent Cache

This type of cache relies on a feature built into WordPress called the Transient API. Transients are stored in the database (similar to most WordPress settings, in the <code>wp_options</code> table). Transients need two records in the database: one to store the expiration time and one to store the data. When cached data is requested, WordPress checks the timestamp and does one of two things. If the expiration time has passed, WordPress removes the data and returns <code>false</code> as a result. If the data has not expired, another query is run to retrieve it. The good thing about this method is that the cache persists even after the page has loaded, and it can be used for other pages for as long as the transient’s expiration time has not passed.

If your database queries are complex and/or produce results that might not change often, then storing them in the transient cache is a good idea. This is an excellent solution for most widgets, menus and other page elements.</p>

### Example

Let's say we wanted an SQL query to retrieve 20 posts from the previous month, along with some basic author data such as name, email address and URL. But we want posts from only the top 10 authors (sorted by their total number of posts in that month). The results will be displayed in a widget.

When tested on my local machine, this SQL query took 0.1710 seconds to run. If we had 1000 page views per day, this one query would take 171 seconds every 24 hours, or 5130 seconds per month. Relatively speaking, that is not much time, but we could do much better by using the transient cache to store these results with an expiration time of 30 days. Because the results of this query will not change during the month, the transient cache is a great way to optimize resources.

Returning to my local machine, the improved SQL query to get data from the transient cache is now only 0.0006 seconds, or 18 seconds per month. The advantage of this method is obvious in this case: we’ve saved 85 minutes each month with this one widget. Not bad at all. There are cases in which you could save much, much more (such as with very complex menus). More complex SQL queries or operations would further optimize resources.

Let's look at the actual code, both before and after implementing the transient cache. Below is the normal function to get the data. In this example, the SQL query is empty (because it is long and would take too much space here), but the entire widget is linked to at the end of this article.

<pre><code class="language-php">function d4p_get_query_results() {
    global $wpdb;

    $data = $wpdb-&gt;get_results(' // SQL query // ');

    return $data;
}</code></pre>

And here is the function using the transient cache, with a few extra lines to check whether the data is cached.

<pre><code class="language-php">function d4p_get_query_results() {
    global $wpdb;

    $data = get_transient('my_transient_key');

    if ($data === false) {
        $data = $wpdb-&gt;get_results(' // SQL query // ');
        set_transient('my_transient_key', $data, 3600 * 24);
    }

    return $data;
}</code></pre>

The function <code>get_transient</code> (or <code>get_site_transient</code> for a network) needs a name for the transient record key. If the key is not found or the record has expired, then the function will return <code>false</code>. To add a new transient cache record, you will need the record key, the object with the data and the expiration time (in seconds), and you will need to use the <code>set_transient</code> function (or <code>set_site_transient</code> for a network).

If your data changes, you can remove it from the cache. You will need the record key and the <code>delete_transient</code> function (or <code>delete_site_transient</code> for a network). In this example, if the post in the cache is deleted or changed in some way, you could delete the cache record with this:

<pre><code class="language-php">delete_transient('my_transient_key');</code></pre>

### Important Notes

1.  The theoretical maximum size of data you can store in this way is 4 GB. But usually you would keep much smaller amounts of data in transient (up to couple of MB).
2.  Use this method only for data (or operations) that do not change often, and set the expiration time to match the cycle of data changes.
3.  In effect, you are using it to render results that are generated through a series of database queries and storing the resulting HTML in the cache.
4.  The name of the transient record may not be longer than 45 characters, or 40 characters for “site transients” (used with multi-sites to store data at the network level).
5.  It works with WordPress since version 3.0.</p>

## Widget Example: Using Both Types Of Cache

Based on our SQL query, we can create a widget that relies on both caching methods. These are two approaches to the problem, and the two widgets will produce essentially the same output, but using different methods for data retrieval and results caching. As the administrator, you can set a title for the widget and the number of days to keep the results in the cache.

Both versions are simple and can be improved further (such as by selecting the post’s type or by formatting the output), but for this article they are enough.</p>

### Raw Widget

The “raw” widget version stores an object with the SQL query results in the transient cache. In this case, the SQL query would return all columns from the <code>wp_posts</code> table and some columns from the <code>wp_users</code> table, along with information about the authors. Every time the widget loads, each post from our results set would get stored in the non-persistent cache object in the standard <code>posts</code> group, which is the same one used to store posts for normal WordPress operations. Because of this, functions such as <code>get_permalink()</code> can use the cached object to generate a URL to post. Information about the authors from the <code>wp_users</code> table is used to generate the URL for the archive of authors’ posts.

This widget is located in the <code>method_raw.php</code> file in the <code>d4p_sa_method_raw</code> class. The function <code>get_data()</code> is the most important part of the widget. It attempts to get data from the transient cache (on line 52). If that fails, <code>get_data_real()</code> is called to run the SQL query and return the data. This data is now saved into the transient cache (line 56). After we have the data, we store each post from the set into the non-persistent cache. The <code>render</code> function is simple; it displays the results as an unordered list.</p>

### Rendered Widget

The previous method works well, but it could have one problem. What if your permalink depends on categories (or other taxonomies) or you are running a query for a post type in a hierarchy? If that is the case, then generating a permalink for each post would require additional SQL queries. For example, to display 20 posts, you might need another 20 or more SQL queries. To fix the problem, we’ll change how we get the data and what is stored in the transient cache.

The second widget is located in the <code>method_rendered.php</code> file in the <code>d4p_sa_method_rendered</code> class. Within, the names of class methods are the same, so you can easily see now the difference between the two widgets. In this case, the transient cache is used in the <code>render()</code> method. We’re checking for cached data, and if that fails we use <code>get_data()</code> to get the data set and generate a rendered list of results. Now, we are caching the rendered HTML output! No matter how many extra SQL queries are needed to generate the HTML (for permalinks or whatever else you might need in the widget), they are run only once, and the complete HTML is cached. Until the cache expires, we are always displaying HTML rendered without the need for any additional SQL queries or processing.</p>

### Download the Widget

You can <a title="Download the Plugin" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cceadca-fc2e-4d88-956f-1d8688bbd488/d4p-smashing-authors.1">download this D4P Smashing Authors plugin</a>, which contains both widgets.</p>

## Conclusion

As you can see, implementing one or both caching methods is easy and could significantly improve the performance of your plugin. If a user of your plugin decides to use a specialized caching plugin, all the better, but make sure that your code is optimized.

{{< signature "al" >}}


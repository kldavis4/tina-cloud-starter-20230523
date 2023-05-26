---
title: 'How To Interact With The WordPress Database'
slug: interacting-with-the-wordpress-database
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dc06153-10c7-4f21-81fc-f40b665364e8/wordpress-files-illu101.jpg
date: 2011-09-21T19:32:23.000Z
author: daniel-pataki
summary: >-
   In this article, Daniel Pataki will explain how to get started with the <code>&#36;wpdb</code> class, how to retrieve data from your WordPress database and how to run more advanced queries which are tailored to your particular needs, in order to update or delete something in the database, and generally make your website more efficient.
description: >-
  In this article, Daniel Pataki will explain how to get started with the <code>&#36;wpdb</code> class, how to retrieve data from your WordPress database and how to run more advanced queries which are tailored to your particular needs, in order to update or delete something in the database, and generally make your website more efficient.
categories:
  - WordPress
  - PHP
  - Essentials
  - SQL
---

While you already use many functions in WordPress to communicate with the database, there is an easy and safe way to do this directly, using the <code>$wpdb</code> class. Built on the great <a href="https://justinvincent.com/ezsql">ezSQL class</a> by Justin Vincent, <code>$wpdb</code> enables you to address queries to any table in your database, and it also helps you handle the returned data.

Because this functionality is built into WordPress, there is no need to open a separate database connection (in which case, you would be duplicating code), and there is no need to perform hacks such as modifying a result set after it has been queried.

In this article, I will show you how to get started with the <code>$wpdb</code> class, how to retrieve data from your WordPress database and how to run more advanced queries that update or delete something in the database. The techniques here will remove some of the constraints that you run into with functions such as <code>get_posts()</code> and <code>wp_list_categories()</code>, allowing you to tailor queries to your particular needs. This method can also make your website more efficient by getting only the data that you need &mdash; nothing more, nothing less.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01716b7a-c9fa-4e9c-ba54-fbf1b9a33312/wpdboverview.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aaa11d21-ee76-46eb-9b00-0c84fb24a8ac/wpdboverview-frontpage.jpg" alt="wordpress database" width="500" height="237" /></a><figcaption>The <code>$wpdb</code> class modularizes and automates a lot of database-related tasks.</figcaption></figure>

{{% feature-panel %}}

## Getting Started

If you know how MySQL or similar languages work, then you will be right at home with this class, and you will need to keep only a small number of function names in mind. The basic usage of this class can be best understood through an example, so let’s query our database for the IDs and titles of the four most recent posts, ordered by comment count (in descending order).

<div class="break-out">

<pre><code class="language-php">&lt;?php
   $posts = $wpdb-&gt;get_results("SELECT ID, post_title FROM $wpdb-&gt;posts WHERE post_status = 'publish'
   AND post_type='post' ORDER BY comment_count DESC LIMIT 0,4")
?&gt;</code></pre>
</div>

As you can see, this is a basic SQL query, with some PHP wrapped around it. The <code>$wpdb</code> class contains a method (a method is a special name for functions that are inside classes), named <code>get_results()</code>, which will not only fetch your results but put them in a convenient object. You might have noticed that, instead of using <code>wp_posts</code> for the table’s name, I have used <code>$wpdb-&gt;posts</code>, which is a helper to access your core WordPress tables. More on why to use these later.

The <code>$results</code> object now contains your data in the following format:

<div class="break-out">

<pre><code class="language-php">Array
(
   [0] =&gt; stdClass Object
      (
         [ID] =&gt; 6
         [post_title] =&gt; The Male Angler Fish Gets Completely Screwed
      )

   [1] =&gt; stdClass Object
      (
         [ID] =&gt; 25
         [post_title] =&gt; 10 Truly Amazing Icon Sets From Germany
      )

   [2] =&gt; stdClass Object
      (
         [ID] =&gt; 37
         [post_title] =&gt; Elderberry Is Awesome
      )

   [3] =&gt; stdClass Object
      (
         [ID] =&gt; 60
         [post_title] =&gt; Gathering Resources and Inspiration With Evernote
      )

)</code></pre>
</div>

{{% feature-panel %}}

## Retrieving Results From The Database

If you want to retrieve some information from the database, you can use one of four helper functions to structure the data.

### get_results()

This is the function that we looked at earlier. It is best for when you need two-dimensional data (multiple rows and columns). It converts the data into an array that contains separate objects for each row.

<div class="break-out">

<pre><code class="language-php">&lt;?php
   $posts = $wpdb-&gt;get_results("SELECT ID, post_title FROM wp_posts WHERE post_status = 'future'
   AND post_type='post' ORDER BY post_date ASC LIMIT 0,4")

   // Echo the title of the first scheduled post
   echo $posts[0]-&gt;post_title;
?&gt;</code></pre>
</div>

### get_row

When you need to find only one particular row in the database (for example, the post with the most comments), you can use <code>get_row()</code>. It pulls the data into a one-dimensional object.

<div class="break-out">

<pre><code class="language-php">&lt;?php
   $posts = $wpdb-&gt;get_row("SELECT ID, post_title FROM wp_posts WHERE post_status = 'publish'
   AND post_type='post' ORDER BY comment_count DESC LIMIT 0,1")

   // Echo the title of the most commented post
   echo $posts-&gt;post_title;
?&gt;</code></pre>
</div>

### get_col

This method is much the same as <code>get_row()</code>, but instead of grabbing a single row of results, it gets a single column. This is helpful if you would like to retrieve the IDs of only the top 10 most commented posts. Like <code>get_row()</code>, it stores your results in a one-dimensional object.

<div class="break-out">

<pre><code class="language-php">&lt;?php
   $posts = $wpdb-&gt;get_col("SELECT ID FROM wp_posts WHERE post_status = 'publish'
   AND post_type='post' ORDER BY comment_count DESC LIMIT 0,10")

   // Echo the ID of the 4th most commented post
   echo $posts[3]-&gt;ID;
?&gt;</code></pre>
</div>

### get_var

In many cases, you will need only one value from the database; for example, the email address of one of your users. In this case, you can use <code>get_var</code> to retrieve it as a simple value. The value’s data type will be the same as its type in the database (i.e. integers will be integers, strings will be strings).

<div class="break-out">

<pre><code class="language-php">&lt;?php
   $email = $wpdb-&gt;get_var("SELECT user_email FROM wp_users WHERE user_login = 'danielpataki' ")

   // Echo the user's email address
   echo $email;
?&gt;</code></pre>
</div>

## Inserting Into The Database

To perform an insert, we can use the insert method:

<pre><code class="language-php">$wpdb-&gt;insert( $table, $data, $format);</code></pre>

This method takes three arguments. The first specifies the name of the table into which you are inserting the data. The second argument is an array that contains the columns and their respective values, as key-value pairs. The third parameter specifies the data type of your values, in the order you have given them. Here’s an example:

<div class="break-out">

<pre><code class="language-php">&lt;?php
   $wpdb-&gt;insert($wpdb-&gt;usermeta, array("user_id" =&gt; 1, "meta_key" =&gt; "awesome_factor", "meta_value" =&gt; 10), array("%d", %s", "%d"));

   // Equivalent to:
   // INSERT INTO wp_usermeta (user_id, meta_key, meta_value) VALUES (1, "awesome_factor", 10);
?&gt;</code></pre>
</div>

If you’re used to writing out your inserts, this may seem unwieldy at first, but it actually gives you a lot of flexibility because it uses arrays as inputs.

Specifying the format is optional; all values are treated as strings by default, but including this in the method is a good practice. The three values you can use are <code>%s</code> for strings, <code>%d</code> for decimal numbers and <code>%f</code> for floats.

{{% ad-panel-leaderboard %}}

## Updating Your Data

By now, you won’t be surprised to hear that we also have a helper method to update our data &mdash; shockingly, called <code>update()</code>. Its use resembles what we saw above; but to handle the <code>where</code> clause of our update, it needs two extra parameters.

<div class="break-out">

<pre><code class="language-php">$wpdb-&gt;update( $table, $data, $where, $format = null, $where_format = null );</code></pre>
</div>

The <code>$table</code>, <code>$data</code> and <code>$format</code> parameters should be familiar to you; they are the same as before. Using the <code>$where</code> parameter, we can specify the conditions of the update. It should be an array in the form of column-value pairs. If you specify multiple parameters, then they will be joined with <code>AND</code> logic. The <code>$where_format</code> is just like <code>$format</code>: it specifies the format of the values in the <code>$where</code> parameter.

<div class="break-out">

<pre><code class="language-php">$wpdb-&gt;update( $wpdb-&gt;posts, array("post_title" =&gt; "Modified Post Title"), array("ID" =&gt; 5), array("%s"), array("%d") );</code></pre>
</div>

## Other Queries

While the helpers above are great, sometimes performing different or more complex queries than the helpers allow is necessary. If you need to perform an update with a complex <code>where</code> clause containing multiple <code>AND</code>/<code>OR</code> logic, then you won’t be able to use the <code>update()</code> method. If you wanted to do something like delete a row or set a connection character set, then you would need to use the “general” <code>query()</code> method, which let’s you perform any sort of query.

<div class="break-out">

<pre><code class="language-php">$wpdb-&gt;query("DELETE FROM wp_usermeta WHERE meta_key = 'first_login' OR meta_key = 'security_key' ");</code></pre>
</div>

## Protection And Validation

I hope I don’t have to tell you how important it is to make sure that your data is safe and that your database can’t be tampered with! Data validation is a bit beyond the scope of this article, but do take a look at what the WordPress Codex has to say about “<a href="https://codex.wordpress.org/Data_Validation">Data Validation</a>” at some point.

In addition to validating, you will need to escape all queries. Even if you are not familiar with <a href="https://en.wikipedia.org/wiki/SQL_injection">SQL injection</a> attacks, still use this method and then read up on it later, because it is critical.

If you use the <code>query()</code> method or any other function where you write raw SQL (like <code>get_var()</code>), you will need to escape manually, using the <code>prepare()</code> method.

<div class="break-out">

<pre><code class="language-php">$sql = $wpdb-&gt;prepare( 'query' [, value_parameter, value_parameter ... ] );</code></pre>
</div>

To make this a bit more digestible, let’s rewrite this basic format a bit.

<div class="break-out">

<pre><code class="language-php">$sql = $wpdb-&gt;prepare( "INSERT INTO $wpdb-&gt;postmeta (post_id, meta_key, meta_value ) VALUES ( %d, %s, %d )", 3342, 'post_views', 2290 )
$wpdb-&gt;query($sql);</code></pre>
</div>

As you can see, this is not that scary. Instead of adding the actual values where you usually would, you enter the type of data, and then you add the actual data as subsequent parameters.

## Class Variables And Other Methods

Apart from these excellent methods, there are quite a few other functions and variables to make your life easier. I’ll show you some of the most common ones, but please do look at the WordPress Codex page linked to above for a full list of everything that <code>$wpdb</code> has to offer.

### insert_id()

Whenever you insert something into a table, you will very likely have an auto-incrementing ID in there. To find the value of the most recent insert performed by your script, you can use <code>$wpdb-&gt;insert_id</code>.

<div class="break-out">

<pre><code class="language-php">$sql = $wpdb-&gt;prepare( "INSERT INTO $wpdb-&gt;postmeta (post_id, meta_key, meta_value ) VALUES ( %d, %s, %d )", 3342, 'post_views', 2290 )
   $wpdb-&gt;query($sql);

   $meta_id = $wpdb-&gt;insert_id;</code></pre>
</div>

### num_rows()

If you’ve performed a query in your script, then this variable will return the number of results of your last query. This is great for post counts, comment counts and so on.

### Table Names

All the core table names are stored in variables whose names are exactly the same as their core table equivalent. The name of your posts table (probably <code>wp_posts</code>) would be stored in the <code>$posts</code> variable, so you could output it by using <code>$wpdb-&gt;posts</code>.

We use this because we are allowed to choose a prefix for our WordPress tables. While most people use the default <code>wp</code>, some users want or need a custom one. For the sake of flexibility, this prefix is not hardcoded, so if you are writing a plug-in and use <code>wp_postmeta</code> in a query instead of <code>$wpdb-&gt;postmeta</code>, your code will not work on some websites.

If you want to get data from a non-core WordPress table, no special variable will be available for it. In this case, you can just write the table’s name as usual.

### Error Handling

By calling the <code>show_errors()</code> or <code>hide_errors()</code> methods, you can turn error-reporting on or off (it’s off by default) to get some more info about what’s going on. Either way, you can also use the <code>print_error()</code> method to print the errors for the latest query.

<div class="break-out">

<pre><code class="language-php">$wpdb-&gt;show_errors();
   $wpdb-&gt;query("DELETE FROM wp_posts WHERE post_id = 554 ");

   // When run, because show_errors() is set, the error message will tell you that the "post_id" field is an unknown
   // field in this table (since the correct field is ID)</code></pre>
</div>

## Building Some Basic Tracking With Our New $wpdb Knowledge

If you’re new to all of this, you probably get what I’m going on about but may be finding it hard to implement. So, let’s take the example of a simple WordPress tracking plug-in that I made for a website.

For simplicity’s sake, I won’t describe every detail of the plug-in. I’ll just show the database’s structure and some queries.

### Our Table’s Structure

To keep track of ad clicks and impressions, I created a table; let’s call it “tracking.” This table records user actions in real time. Each impression and click is recorded in its own row in the following structure:

*   `ID` The auto-incremented ID.
*   `time` The date and time that the action occurred.
*   `deal_id` The ID of the deal that is connected to the action (i.e. the ad that was clicked or viewed).
*   `action` The type of action (i.e. click or impression).
*   `action_url` The page on which the action was initiated.
*   `user_id` If the user is logged in, their ID.
*   `user_ip` The IP of the user, used to weed out any naughty business.

This table will get pretty big pretty fast, so it is aggregated into daily statistics and flushed periodically. But let’s just work with this one table for now.

## Inserting Data Into Our Tables

When a user clicks an ad, it is detected, and the information that we need is sent to our script in the form of a <code>$&#95;POST</code> array, with the following data:

<pre><code class="language-php">Array
(
   [deal_id] =&gt; 643
   [action] =&gt; click
   [action_url] =&gt; https://thisiswhereitwasclicked.com/about/
   [user_id] =&gt; 223
   [user_ip] = 123.234.223.12
)</code></pre>

We can then insert this data into the database using our helper method, like so:

<div class="break-out">

<pre><code class="language-php">$wpdb-&gt;insert('tracking', array("deal_id" =&gt; 643, "action" =&gt; "click", "action_url" =&gt; "https://thisiswhereitwasclicked.com/about/",
"user_id" =&gt; 223, "user_ip" =&gt; "123.234.223.12"), array("%d", %s", "%s", "%d", "%s"));</code></pre>
</div>

At the risk of going on a tangent, I’ll address some questions you might have about this particular example. You may be thinking, what about data validation? The click could have come from a website administrator, or a user could have clicked twice by mistake, or a bunch of other things might have happened.

We decided that because we don’t need real-time stats (daily stats is enough), there is no point to check the data at every insert. Data is aggregated into a new table every day around midnight, a low traffic time. Before aggregating the data, we take care to clean it up, taking out duplicates and so on. The data is, of course, escaped before being inserted into the table, because we are using a helper function; so, we are safe there.

Just deleting in bulk all at once the ones that are made by administrators is easier than checking at every insert. This takes a considerable amount of processing off our server’s shoulders.

### Deleting Actions From A Blacklisted IP

If we find that the IP address <code>168.211.23.43</code> is being naughty-naughty, we could blacklist it. In this case, when we aggregate the daily data, we would need to delete all of the entries by this IP.

<div class="break-out">

<pre><code class="language-php">$sql = $wpdb-&gt;prepare("DELETE FROM tracking WHERE user_ip = %s ", '168.211.23.43');
   $wpdb-&gt;query($sql);</code></pre>
</div>

You have probably noticed that I am still escaping the data, even though the IP was received from a secure source. I would suggest escaping your data no matter what. First of all, proper hackers are good at what they do, because they are excellent programmers and can outsmart you in ways that you wouldn’t think of. Also, I personally have done more to hurt my own websites than hackers have, so I do these things as a safety precaution against myself as well.

### Updating Totals

We store our ads as custom post types; and to make statistical reporting easier, we store the total amount of clicks that an ad receives separately as well. We could just add up all of the clicks in our tracking database for the given deal as well, so let’s look at that first.

<pre><code class="language-php">$total = $wpdb-&gt;get_var("SELECT COUNT(ID) WHERE deal_id = 125 ");</code></pre>

Because getting a single variable is easier than always burdening ourselves with a more complex query, whenever we aggregate our data, we would store the current total separately. Our ads are stored as posts with a custom post type, so a logical place to store this total is in the <code>postmeta</code> table. Let’s use the <code>total_clicks</code> meta key to store this data.

<div class="break-out">

<pre><code class="language-php">$wpdb-&gt;update( $wpdb-&gt;postmeta, array("meta_value" =&gt; $total), array("ID" =&gt; 125), array("%d"), array("%d") );

   // note that this should be done with update_post_meta(), I just did it the way I did for example's sake</code></pre>
</div>

## Final Thoughts And Tips

I hope you have gained a better understanding of the WordPress <code>$wpdb</code> class and that you will be able to use it to make your projects better. To wrap up, here are some final tips and tricks for using this class effectively.

*   I urge you to be cautious: with great power comes great responsibility. Make sure to escape your data and to validate it, because improper use of this class is probably a leading cause of hacked websites!
*   Ask only for the data that you need. If you will only be displaying an article’s title, there is no need to retrieve all of the data from each row. In this case, just ask for the title and the ID: `SELECT title, ID FROM wp_posts ORDER BY post_date DESC LIMIT 0,5`.
*   While you can use the `query()` method for any query, using the helper methods (`insert`, `update`, `get_row`, etc.) is better if possible. They are more modular and safer, because they escape your data automatically.
*   Take care when deleting records from a WordPress (or any other) database. When WordPress deletes a comment, a bunch of other actions also take place: the comment count in the `wp_posts` table needs to be reduced by one, all of the data in the `comment_meta` table needs to be deleted as well, and so on. Make sure to clean up properly after yourself, especially when deleting things.
*   Look at all of the [class variables](https://codex.wordpress.org/Class_Reference/wpdb#Class_Variables) and other bits of information in the official documentation. These will help you use the class to its full potential. I also recommend looking at the [ezSQL](https://justinvincent.com/ezsql) class for general use in your non-WordPress projects; I use it almost exclusively for everything I do.

### Other Resources

*   [WordPress DB basics and schema](https://codex.wordpress.org/Database_Description), WordPress Codex
*   [Documentation on $wpdb](https://codex.wordpress.org/Class_Reference/wpdb), WordPress Codex
*   “[Data validation](https://codex.wordpress.org/Data_Validation),” WordPress Codex
*   “[SQL Injection](https://en.wikipedia.org/wiki/SQL_injection),” Wikipedia
*   “[SQL Injection Attacks by Example](https://www.unixwiz.net/techtips/sql-injection.html),” Steve Friedl

{{% ad-panel-leaderboard %}}

### Further Reading

- [Speeding Up Your Website’s Database](https://www.smashingmagazine.com/2011/03/speeding-up-your-websites-database/)
- [MySQL Admin and Development Tools Round-Up](https://www.smashingmagazine.com/2009/03/mysql-admin-and-development-tools-round-up/)
- [A Look At The Modern WordPress Server Stack](https://www.smashingmagazine.com/2016/05/modern-wordpress-server-stack/)
- [Advanced WordPress Management With WP-CLI](https://www.smashingmagazine.com/2015/09/wordpress-management-with-wp-cli/)

{{< signature "al, yk, il, mrn" >}}

---
title: Speeding Up Your Website’s Database
slug: speeding-up-your-websites-database
image: null
date: 2011-03-23T08:05:09.000Z
author: paul-tero
description: >-
  Website speed has always been a big issue, and it has become even more important since April 2010, when Google decided to use it in search rankings.
categories:
  - Coding
  - Performance
  - Speed
---
However, the focus of the discussion is generally on minimizing file sizes, improving server settings and optimizing CSS and Javascript.

The discussion glosses over another important factor: the speed with which your pages are actually put together on your server. Most big modern websites store their information in a database and use a language such as PHP or ASP to extract it, turn it into HTML and send it to the Web browser.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Advanced WordPress Management With WP-CLI](https://www.smashingmagazine.com/2015/09/wordpress-management-with-wp-cli/)
*   [Why Static Website Generators Are The Next Big Thing](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/)
*   [WordPress Performance Improvements That Can Go Wrong](https://www.smashingmagazine.com/2014/03/wordpress-performance-improvements-that-can-go-wrong/)
*   [Speed Up Your Mobile Website With Varnish](https://www.smashingmagazine.com/2013/12/speed-up-your-mobile-website-with-varnish/)

So, even if you get your home page down to 1.5 seconds (Google’s threshold for being considered a “fast” website), you can still frustrate customers if your search page takes too much time to respond, or if the product pages load quickly but the “Customer reviews” delay for several seconds.

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8f09765-d0f6-4c3a-944a-5ccb1c3e4c4b/site-performance-full.png"><img loading="lazy" decoding="async" class="88572" title="Google Site Performance" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c9e0176-c96a-4196-90e6-365f78b47808/performance.gif" alt="Google Site Performance" width="501" height="371" /></a><br>
<em>Google’s threshold for a fast-loading website is about 1.5 seconds. This screenshot comes from Google Webmaster Tools (go to [domain name] → Diagnostics → Site Performance).</em>

This article looks at these sorts of issues and describes some simple ways to speed up your website by optimizing your database. It starts with common knowledge but includes more complex techniques at the end, with links to further reading throughout. The article is intended for fearless database beginners and designers who have been thrown in at the deep end.</p>

## What Is A Database? What Is SQL?

A database is basically a collection of tables of information, such as a list of customers and their orders. It could be a filing cabinet, a bunch of spreadsheets, a Microsoft Access file or Amazon’s 40 terabytes of book and customer data.

A typical database for a blog has tables for users, categories, posts and comments. WordPress includes <a href="https://codex.wordpress.org/Database_Description">these and a few other</a> starter tables. A typical database for an e-commerce website has tables for customers, products, categories, orders and order items (for the contents of shopping baskets). The open-source e-commerce software Magento includes <a href="https://www.magentocommerce.com/wiki/2_-_magento_concepts_and_architecture/magento_database_diagram">these and many others</a>. Databases have many other uses — such as for content management, customer relations, accounts and invoicing, and events — but these two common types (i.e. for a blog and an e-commerce website) will be referenced throughout this article.

Some tables in a database are connected to other tables. For example, a blog post can have many comments, and a customer can make multiple orders (these are <em>one-to-many</em> relationships). The most complicated type of database relationship is a <em>many-to-many</em> relationship. One relationship is at the core of all e-commerce databases: an order can contain many products, and a single product can be added to many different orders. This is where the “order items” table comes in: it sits between the products and the orders, and it records every time a product is added to an order. This will be relevant later on in the article, when we look at why some database queries are slow.

The word <em>database</em> also refers to the software that contains all this data, as in “My database crashed while I was having breakfast,” or “I really need to upgrade my database.” Popular database software include Microsoft Access 2010, Microsoft SQL Server, MySQL, PostgreSQL and Oracle Database 11g.

The acronym SQL comes up a lot when dealing with databases. It stands for “structured query language” and is pronounced “sequel” or “es-cue-el.” It’s the language used to ask and tell a database things — exciting things like <code>SELECT lastname FROM customers WHERE city='Brighton'</code>. This is called a <em>database query</em> because it queries the database for data. There are other types of database statements: <code>INSERT</code> for putting in new data, <code>UPDATE</code> for updating existing data, <code>DELETE</code> for deleting things, <code>CREATE TABLE</code> for creating tables, <code>ALTER TABLE</code> and many more.</p>

## How Can A Database Slow Down A Website?

A brand new empty website will run very fast, but as it grows and ages, you may notice some sluggishness on certain pages, particularly pages with complicated bits of functionality. Suppose you wanted to show “Customers who bought this product also bought…” at the bottom of a page of products. To extract this information from the database, you would need to do the following:

1.  Start with the current product,
2.  See how many times the product has recently been added to anyone’s shopping basket (the “order items” table from above),
3.  Look at the orders related to those shopping baskets (for completed orders only),
4.  Find the customers who made those orders,
5.  Look at other orders made by those customers,
6.  Look at the contents of those orders’ baskets (the “order items” again),
7.  Look up the details of those products,
8.  Identify the products that appear the most often and display them.

You could, in fact, do all of that in one massive database query, or you could split it up over several different queries. Either way, it might run very quickly when your database has 20 products, 12 customers, 18 orders and 67 order items (i.e. items in shopping baskets). But if it is not written and programmed efficiently, then it will be a lot slower with 500 products, 10,000 customers, 14,000 orders and 100,000 order items, and it will slow down the page.

This is a very complicated example, but it shows what kind of stuff goes on behind the scenes and why a seemingly innocuous bit of functionality can grind a website to a halt.

A website could slow down for many other reasons: the server running low on memory or disc space; another website on the same server consuming resources; the server sending out a lot of emails or churning away at some other task; a software, hardware or network fault; a misconfiguration. Or it may have suddenly become a popular website. The next two sections, therefore, will look at speed in more detail.</p>

## Is It My Database?

There are now several ways to analyze your website’s speed, including the <a href="https://getfirebug.com/">Firebug plug-in</a> for Firefox, the developer tools in Google Chrome (press Shift + Control + I, and then go to Resources → Enable Resource Tracking) and <a href="https://developer.yahoo.com/yslow/">Yahoo YSlow</a>. There are also websites such as <a href="https://www.webpagetest.org">WebPagetest</a>, where you can enter a URL, and it will time it from your chosen location.

All of these tools will show you a diagram of all of the different resources (HTML, images, CSS and JavaScript files) used by your page, along with how long each took to load. They will also break down the time taken to perform a DNS lookup (i.e. to convert your domain name into an IP address), the time taken to connect to your server, the time spent waiting for your server to reply (aka “time to first byte”), and the time spent receiving (i.e. downloading) the data.

Many Web pages are constructed in their entirety by the Web server, including by PHP that accesses the database, and then sent to the browser all at once, so any database delays would lead to a long waiting time, and the receiving/downloading time would be proportional to the amount of data sent. So, if your 20 kB HTML page has a quick connection, a waiting time of 5 seconds and a download time of 0.05 seconds, then the delay would occur on the server, as the page is being built.

Not all Web pages are like this, though. The PHP <code>flush</code> function forces the server to send the HTML that it has already built to the browser right away. Any further delays would then be in the receiving time, rather than the waiting time.

Either way, you can <strong>compare the waiting/receiving time</strong> for your suspected slow and complicated Web page to the waiting time for a similarly sized HTML page (or image or other static resource) on the same server at the same time. This would rule out the possibility of a slow Internet connection or an overloaded server (both of which would cause delays) and allow you to compare the times taken to construct the pages. This is not an exact science, but it should give you some indication of where things are being held up.

The screenshots below show the analysis provide by Google Chrome’s Developer Tools of a 20 kB Web page versus a 20 kB image. The Web page waited 130 milliseconds (ms) and downloaded for 22 ms. The image waited for 51 ms and downloaded for 11 ms. The download/receiving times are about the same, as expected, but the server is spending about 80 ms extra on processing and constructing the Web page, which entails executing the PHP and calling the database.

When performing these tests, analyze the static resource by itself and click “Refresh,” so that you are not getting a quick cached version. Also, run each a few times to ensure that you’re not looking at a statistical anomaly. The third screenshot below shows that WebPagetest indicates almost double the time of Google for the same page at the same time, demonstrating that using the same environment for all tests is important.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35402c26-7fe4-4c55-8a74-08bd2f987c20/google-chrome-image-full.png"><img loading="lazy" decoding="async" class="85683" title="Page speed in Google Chrome" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11dac2be-b289-4a4e-adb5-af52b73b2ecd/google-chrome-web-page-snapshot.png" alt="Screenshot" width="500" height="188" /></a><br>
<em>Resource analysis using Google Chrome’s Developer Tools, showing a 130-ms wait time for a Web page.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35402c26-7fe4-4c55-8a74-08bd2f987c20/google-chrome-image-full.png"><img loading="lazy" decoding="async" class="88532" title="Waiting and receiving time for an image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f43e0b3e-03d5-4388-ae6a-4620b2728ef2/google-chrome-image-snapshot.png" alt="Waiting and receiving time for an image" width="500" height="186" /></a><br>
<em>The same tool, showing a 51-ms wait time for an image of about the same size.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93a0a1ba-c02f-4cea-86c8-50c004feefd3/web-page-test-full1.png"><img loading="lazy" decoding="async" class="85679" title="Analyzing page speed" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4763f9-ac56-4ef8-8760-f8a9c2d8de45/web-page-test-thumb.png" alt="Screenshot" width="500" height="133" /></a><br>
<em>Resource analysis of the same page from WebPagetest, with a 296-ms wait time and a 417-ms total time.</em>

## How To Time A Database Query In PHP And MySQL

The approach above was general; we can now get very specific. If you suspect that your database might be slowing down your website, then you need to figure out where the delay is coming from. I will define a couple of timing functions, and then use them to time every single database query that is run by a page. The code below is specific to PHP and MySQL, but the method could be used on any database-driven website:

<pre><code class="language-php">function StartTimer ($what=’) {
 global $MYTIMER; $MYTIMER=0; //global variable to store time
 //if ($_SERVER['REMOTE_ADDR'] != '127.0.0.1') return; //only show for my IP address

 echo '&lt;p style="border:1px solid black; color: black; background: yellow;"&gt;';
 echo "About to run &lt;i&gt;$what&lt;/i&gt;. "; flush(); //output this to the browser
 //$MYTIMER = microtime (true); //in PHP5 you need only this line to get the time

 list ($usec, $sec) = explode (' ', microtime());
 $MYTIMER = ((float) $usec + (float) $sec); //set the timer
}
function StopTimer() {
 global $MYTIMER; if (!$MYTIMER) return; //no timer has been started
 list ($usec, $sec) = explode (' ', microtime()); //get the current time
 $MYTIMER = ((float) $usec + (float) $sec) - $MYTIMER; //the time taken in milliseconds
 echo 'Took ' . number_format ($MYTIMER, 4) . ' seconds.&lt;/p&gt;'; flush();
}</code></pre>

<code>StartTimer</code> starts the timer and also prints whatever you are trying to time. The second line is a check of your IP address. This is very useful if you are doing this (temporarily) on a live website and don’t want everyone in the world to see the timing messages. Uncomment the line by removing the initial <code>//</code>, and replace the <code>127.0.0.1</code> with <a href="https://whatismyipaddress.com/">your IP address</a>. <code>StopTimer</code> stops the timer and displays the time taken.

Most modern websites (especially well-programmed open-source ones) have a lot of PHP files but query the database in only a handful of places. Search through all of the PHP files for your website for <code>mysql_db_query</code> or <code>mysql_query</code>. Many software development packages such as BBEdit have functions to perform searches like this; or, if you are familiar with the Linux command line, try this:
<code>grep mysql_query `find . -name *php`</code>

You may find something like this:

<pre><code class="language-php">mysql_query ($sql);</code></pre>

For WordPress 3.0.4, this is on line 1112 of the file <em>wp-includes/wp-db.php</em>. You can copy and paste the functions above into the top of this file (or into any PHP file that is included by every page), and then add the timer before and after the <code>mysql_query</code> line. It will look like this:

<pre><code class="language-php">StartTimer ($query);
$this-&gt;result = @mysql_query( $query, $dbh );
StopTimer();</code></pre>

Below is a partial screenshot of this being done on a brand new WordPress installation. It is running about 15 database queries in total, each taking about 0.0003 seconds (0.3 ms); so, less than 5 ms in total, which is to be expected for an empty database.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/480ee08a-2293-4621-b770-2820c2094c23/wordpress-timed-full.png"><img loading="lazy" decoding="async" class="85645" title="Showing all the database queries WordPress runs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/163f386f-4acc-420c-8f0a-ef7e0ca44559/hello-world.gif" alt="Screenshot" width="540" height="570" /></a><br>
<em>This shows and times all of the database queries that WordPress runs.</em>

If you have found this line in other commonly used systems, please share this information by adding to the comments for this article.

You can also do other interesting things with it: you can see how fast your computer is compared to mine. Counting to 10 million takes my computer 2.9420 seconds. My Web server is a bit faster at 2.0726 seconds:

<pre><code class="language-php">StartTimer ('counting to 10000000');
for ($i=0; $i&lt;10000000; $i++); //count to a high number
StopTimer();</code></pre>

### Notes on the Results

This technique gives you only comparative results. If your server was very busy at that moment, then all of the queries would be slower than normal. But you should have at least been able to determine how long a fast query takes on your server (maybe 1 to 5 ms), and therefore identify the slow-ish ones (200+ ms) and the really slow ones (1+ second). You can run the test a few times over the course of an hour or day (but not immediately after — see the section below about the database cache) to make sure you’re not getting a fluke.

This will also most likely severely mess up the graphical presentation of the page. It may also give you PHP warnings like “Cannot modify header information. Headers already sent by…" This is because the timing messages are interfering with cookie and session headers. As long as the page still displays below the warnings, you can ignore them. If the page does not display at all, then you may need to put the <code>StartTimer</code> and <code>StopTimer</code> around specific blocks of code, rather than around <code>mysql_query</code>.

This technique is essentially a quick hack to show some rough results. It should not be left on a live website.</p>

### What Else Could It Be?

If your database queries are not particularly slow, but the construction of your Web page is, then you might just have poorly written code. You can put the timer statements above around bigger and bigger blocks of code to see if and where the delay is occurring. It could be that you are looping through 10,000 full rows of product information, even if you are displaying only 20 product names.</p>

### Profiling

If you are still baffled and/or want more complete and accurate information about what’s happening in your code, you could try a debugging and profiling tool such as <a href="https://www.xdebug.org/">Xdebug</a>, which analyzes a local copy of your website. It can even visually show where bottlenecks are occurring.</p>

## Indexing Database Tables

The experiment above may have surprised you by showing just how many database queries a page on your website is running, and hopefully, it has helped you identify particularly slow queries.

Let’s look now at some <strong>simple improvements to speed things up</strong>. To do this, you’ll need a way to run database queries on your database. Many server administration packages (like cPanel or Plesk) provide phpMyAdmin for this task. Alternatively, you could upload something like <a href="https://phpminiadmin.sourceforge.net/">phpMiniAdmin</a> to your website; this single PHP file enables you to look at your database and run queries. You’ll need to enter your database name, user name and password. If you don’t know these, you can usually find them in your website’s configuration file, if it has one (in WordPress, it’s <em>wp-config.php</em>).

Among the database queries that your page runs, you probably saw a few <code>WHERE</code> conditions. This is SQL’s way of filtering out results. For instance, if you are looking at an "Account history" type of page on your website, there is probably a query like this to look up all of the orders someone has placed. Something like this:

<pre><code class="language-markup tmp-sql">SELECT * FROM orders WHERE customerid = 2;</code></pre>

This retrieves all orders placed by the customer with the database ID 2. On my computer, with 100,000 orders in the database, running this took 0.2158 seconds.

Columns like <code>customerid</code> — which deal with a lot of <code>WHERE</code> conditions with <code>=</code> or <code>&lt;</code> or <code>&gt;</code> and have many possible values, should be indexed. This is like the index at the back of a book: it helps the database quickly retrieve indexed data. This is one of the quickest ways to speed up database queries.</p>

### What to Index

In order to know which columns to index, you need to understand a bit about how your database is being used. For example, if your website is often used to look up categories by name or events by date, then these columns should be indexed.

<pre><code class="language-markup tmp-sql">SELECT * FROM categories WHERE name = 'Books';
SELECT * FROM events WHERE startdate &gt;= '2011-02-07';</code></pre>

Each of your database tables should already have an ID column (often called <code>id</code>, but sometimes <code>ID</code> or <code>articleid</code> or the like) that is listed as a <code>PRIMARY KEY</code>, as in the <code>wp_posts</code> screenshot below. These <code>PRIMARY KEY</code>s are automatically indexed. But you should also index any columns that refer to ID numbers in other tables, such as <code>customerid</code> in the example above. These are sometimes referred to as <code>FOREIGN KEY</code>s.

<pre><code class="language-markup tmp-sql">SELECT * FROM orders WHERE customerid = 2;
SELECT * FROM orderitems WHERE orderid = 231;</code></pre>

If a lot of text searches are being done, perhaps for descriptions of products or article content, then you can add another type of index called a <a href="https://www.devarticles.com/c/a/MySQL/Getting-Started-With-MySQLs-Full-Text-Search-Capabilities/1/">FULL TEXT index</a>. Queries using a <code>FULL TEXT</code> index can be done over multiple columns and are initially configured to work only with words of four or more letters. They also exclude certain <a href="https://dev.mysql.com/doc/refman/5.0/en/fulltext-stopwords.html">common words</a> like <em>about</em> and words that appear in more than 50% of the rows being searched. However, to use this type of index, you will need to change your SQL queries. Here is a typical text search, the first without and the second with a <code>FULL TEXT</code> index:

<pre><code class="language-markup tmp-sql">SELECT * FROM products WHERE name LIKE '%shoe%' OR description LIKE '%shoe%';
SELECT * FROM products WHERE MATCH(name,description) AGAINST ('shoe');</code></pre>

It may seem that you should go ahead and index everything. However, while indexing speeds up <code>SELECT</code>s, it slows down <code>INSERT</code>s, <code>UPDATE</code>s and <code>DELETE</code>s. So, if you have a products table that hardly ever changes, you can be more liberal with your indexing. But your orders and order items tables are probably being modified constantly, so you should be more sparing with them.

There are also cases where <a href="https://www.mysqlperformanceblog.com/2007/08/28/do-you-always-need-index-on-where-column/">indexing may not help</a>; for example, if most of the entries in a column have the same value. If you have a <code>stock_status</code> column that stores a value of <code>1</code> for “in stock,” and 95% of your products are in stock, then an index wouldn’t help someone search for in-stock products. Imagine if the word <em>the</em> was indexed at the back of a reference book: the index would list almost every page in the book.

<pre><code class="language-markup tmp-sql">SELECT * FROM products WHERE stock_status = 1;</code></pre>

### How to Index

Using phpMyAdmin or phpMiniAdmin, you can look at the structure of each database table and see whether the relevant columns are already indexed. In phpMyAdmin, click the name of the table and browse to the bottom where it lists “Indexes.” In phpMiniAdmin, click “Show tables” at the top, and then “sct” for the table in question; this will show the database query needed to recreate the table, which will include any indices at the bottom — something like <code>KEY 'orderidindex' ('orderid')</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f2e3018-cf4d-4d65-a421-67354d558cda/show-create-table-full.png"><img loading="lazy" decoding="async" class="85649" title="Checking for indices using phpminiadmin" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5f66827-e29a-482a-9092-6fcbfbc1cf6c/show-create-table-snapshot1.png" alt="Screenshot" width="500" height="388" /></a><br>
<em>Using phpMiniAdmin to check for indices in the WordPress <code>wp_posts</code> table.</em>

If the index does not exist, then you can add it. In phpMyAdmin, below the index, it says “Create an index on 1 columns”; click “Go” here, enter a useful name for the index (like <code>customeridindex</code>), choose the column on the next page, and press “Save,” as seen in this screenshot:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76dc631b-5d3a-4957-9043-9eb0ef78afa6/adding-index-full.png"><img loading="lazy" decoding="async" class="85648" title="Indexing a column using phpMyAdmin" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc857187-9459-4d14-9bf1-e2fa14351062/adding-index-snapshot1.png" alt="Screenshot" width="500" height="302" /></a><br>
<em>Indexing a column using phpMyAdmin.</em>

In phpMiniAdmin, you’ll have to run the following database statement directly in the large SQL query box at the top:

<pre><code class="language-markup tmp-sql">ALTER TABLE orders ADD INDEX customeridindex (customerid);</code></pre>

Running the query again after indexing takes only 0.0019 seconds on my computer, 113 times faster.

Adding a <code>FULL TEXT</code> index is a similar process. When you run searches against this index, you must list the same columns:

<pre><code class="language-markup tmp-sql">ALTER TABLE articles ADD FULLTEXT(title,author,articletext);
SELECT * FROM articles WHERE MATCH(title,author,articletext) AGAINST ('mysql');</code></pre>

### Back-Ups and Security

Before altering your database tables in any way, make a back-up of the whole database. You can do this using phpMyAdmin or phpMiniAdmin by clicking “Export.” Especially if your database contains customer information, keep the back-ups in a safe place. You can also use the command <code>mysqldump</code> to back up a database via SSH:

<pre><code class="language-markup tmp-sql">mysqldump --user=myuser --password=mypassword
--single-transaction --add-drop-table mydatabase
&gt; backup`date +%Y%e%d`.sql</code></pre>

These scripts also represent a security risk, because they make it much easier for someone to steal all of your data. While phpMyAdmin is often provided securely though your server management software, phpMiniAdmin is a single file that is very easy to upload and forget about. So, you may want to password-protect it or remove it after usage.</p>

## Optimizing Tables

MySQL and other kinds of database software have built-in tools for optimizing their data. If your tables get modified a lot, then you can <strong>run the tools regularly</strong> to make the database tables smaller and more efficient. But they take some time to run (from a few seconds to a few minutes or more, depending on the size of the tables), and they can block other queries from running on the table during optimization, so doing this at a non-busy time is best. There’s also <a href="https://www.xaprb.com/blog/2010/02/07/how-often-should-you-use-optimize-table/">some debate</a> about how often to optimize, with opinions ranging from never to once in a while to weekly.

To optimize a table, run database statements such as the following in phpMyAdmin or phpMiniAdmin:

<pre><code class="language-markup tmp-sql">OPTIMIZE TABLE orders;</code></pre>

For example, before I optimized my orders table with 100,000 orders, it was 31.2 MB in size and took 0.2676 seconds to run <code>SELECT * FROM orders</code>. After its first ever optimization, it shrunk to 30.8 MB and took only 0.0595 seconds.

The PHP function below will optimize all of the tables in your database:

<pre><code class="language-php">function OptimizeAllTables() {
 $tables = mysql_query ('SHOW TABLES'); //get all the tables
 while ($table = mysql_fetch_array ($tables))
 mysql_query ('OPTIMIZE TABLE ' . $table[0]); //optimize them
}</code></pre>

Before calling this function, you have to connect to your database. Most modern websites will connect for you, so you don’t need to worry about it, but the relevant MySQL calls are shown here for the sake of completeness:

<pre><code class="language-php">mysql_connect (DB_HOST, DB_USER, DB_PASSWORD);
mysql_select_db (DB_NAME);
OptimizeAllTables();</code></pre>

## Making Sure To Use The Cache

Just as a Web browser caches copies of pages you visit, database software caches popular queries. As above, the query below took 0.0019 seconds when I ran it the first time with an index:

<pre><code class="language-markup tmp-sql">SELECT * FROM orders WHERE customerid=2;</code></pre>

Running the same query again right away takes only 0.0004 seconds. This is because MySQL has remembered the results and can return them a second time without looking them up again.

However, many news websites and blogs might have queries like the following to ensure that articles are displayed only after their published date:

<pre><code class="language-markup tmp-sql">SELECT * FROM posts WHERE publisheddate &lt;= CURDATE();
SELECT * FROM articles WHERE publisheddate &lt;= NOW();</code></pre>

These queries cannot be cached because they depend on the current time or date. In a table with 100,000 rows, a query like the one above would take about 0.38 seconds every time I run it against an unindexed column on my computer.

If these queries are run on every page of your website, thousands of times per minute, it would speed things up considerably if they were cacheable. You can force queries to use the cache by replacing <code>NOW</code> or <code>CURDATE</code> with an actual time, like so:

<pre><code class="language-markup tmp-sql">SELECT * FROM articles WHERE publisheddate &lt;= '2011-01-17 17:00';</code></pre>

You can use PHP to make sure the time changes every five minutes or so:

<pre><code class="language-php">$time = time();
$currenttime = date ('Y-m-d H:i', $time - ($time % 300));
mysql_query (“SELECT * FROM articles WHERE publisheddate &lt;= '$currenttime'”);</code></pre>

The percentage sign is the modulus operator. <code>% 300</code> rounds the time down to the last 300 seconds or 5 minutes.

There are other <a href="https://dev.mysql.com/doc/refman/5.0/en/query-cache-operation.html">uncacheable MySQL functions</a>, too, like RAND.</p>

### Outgrowing Your Cache

Outgrowing your MySQL cache can also make your website appear to slow down. The more posts, pages, categories, products, articles and so on that you have on your website, the more related queries there will be. Take a look at this example:

<pre><code class="language-markup tmp-sql">SELECT * FROM articles WHERE publisheddate &lt;= '2011-01-17 17:00' AND categoryid=12</code></pre>

It could be that when your website had 500 categories, queries like this one all fit in the cache together and all returned in milliseconds. But with 1000 regularly visited categories, they keep knocking each other out of the cache and returning much slower. In this case, increasing the size of the cache might help. But giving more server RAM to your cache means spending less on other tasks, so consider this carefully. Plenty of advice is available about <a href="https://www.databasejournal.com/features/mysql/article.php/3808841/Optimizing-the-MySQL-Query-Cache.htm">turning on and improving the efficiency of your cache</a> by setting server variables.</p>

### When Caching Doesn’t Help

A cache is invalidated whenever a table changes. When a row is inserted, updated or deleted, all queries relying on that table are effectively cleared from the cache. So, if your articles table is updated every time someone views an article (perhaps to count the number of views), then the improvement suggested above might not help much.

In such cases, you may want to investigate an application-level cacher, such as <a href="https://memcached.org/">Memcached</a>, or read the next section for ideas on making your own ad-hoc cache. Both require much bigger programming changes than discussed up to now.</p>

## Making Your Own Cache

If a particularly viscous database query takes ages but the results don’t change often, you can cache the results yourself.

Let's say you want to show the 20 most popular articles on your website in the last week, using an advanced formula that takes into account searches, views, saves and “Send to a friend” hits. And you want to show these on your home page in an unordered (<code>&lt;ul&gt;</code>) HTML list.

It might be easiest to use PHP to run the database query once an hour or once a day and save the full list to a file somewhere, which you can then include on your home page.

Once you have written the PHP to create the include file, you could take one of a couple approaches to scheduling it. You could use your server’s scheduler (in Plesk 8, go to Server → Scheduled Tasks) to call a PHP page every hour, with a command like this:

<pre><code class="language-php">wget -O /dev/null -q https://www.mywebsite.co.uk/runhourly.php</code></pre>

Alternatively, you could get PHP to check whether the file is at least an hour old before running the query — something like this, where 3600 is the number of seconds in an hour:

<pre><code class="language-php">$filestat = stat ('includes/complicatedfile.html');
//look up information about the file
if ($filestat['mtime'] &lt; time()-3600) RecreateComplicatedIncludeFile();
//over 1 hour
readfile ('includes/complicatedfile.html');
//include the file into the page</code></pre>

Returning to the involved example above for “Customers who bought this product also bought…,” you could also cache items in a new database column (or table). Once a week or so, you could run that long set of queries for each and every product, to figure out which other products customers are buying. You could then store the resulting product ID numbers in a new database column as a comma-separated list. Then, when you want to select the other products bought by customers who bought the product with the ID 12, you can run this query:

<pre><code class="language-markup tmp-sql">SELECT * FROM products WHERE FIND_IN_SET(12,otherproductids);</code></pre>

## Reducing The Number Of Queries By Using JOINs

Somewhere in the management and control area of your e-commerce website is probably a list of your orders with the names of the customers who made them.

This page might have a query like the following to find all completed orders (with a status value indicating whether an order has been completed):

<pre><code class="language-markup tmp-sql">SELECT * FROM orders WHERE status&gt;1;</code></pre>

And for each order it comes across, it might look up the customer’s details:

<pre><code class="language-markup tmp-sql">SELECT * FROM customers WHERE id=1;
SELECT * FROM customers WHERE id=2;
SELECT * FROM customers WHERE id=3;
etc</code></pre>

If this page shows 100 orders at a time, then it has to run 101 queries. And if each of those customers looks up their delivery address in a different table, or looks for the total charge for all of their orders, then the time delay will start to add up. You can make it much faster by combining the queries into one using a <code>JOIN</code>. Here’s what a <code>JOIN</code> looks like for the queries above:

<pre><code class="language-markup tmp-sql">SELECT * FROM orders INNER JOIN customers
ON orders.customerid = customers.id WHERE orders.status&gt;=1;</code></pre>

Here is another way to write this, without the word <code>JOIN</code>:

<pre><code class="language-markup tmp-sql">SELECT * FROM orders, customers
WHERE orders.customerid = customers.id AND orders.status&gt;=1;</code></pre>

Restructuring queries to use <code>JOIN</code>s can get complicated because it involves changing the accompanying PHP code. But if your slow page runs thousands of database statements, then it may be worth a look. For further information, Wikipedia offers a <a href="https://en.wikipedia.org/wiki/Join_%28SQL%29">good explanation of JOINs</a>. The columns with which you use a <code>JOIN</code> (<code>customerid</code> in this case) are also prime candidates for being <code>INDEX</code>ed.

You could also ask MySQL to <a href="https://dev.mysql.com/doc/refman/5.0/en/explain.html">EXPLAIN</a> a database query. This tells you which tables it will use and provides an “execution plan.” Below is a screenshot showing the <code>EXPLAIN</code> statement being used on one of the more complex WordPress queries from above:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f2291e8-dea5-4fbc-9803-d180d1b7faa9/mysql-explain-full.png"><img loading="lazy" decoding="async" class="85673" title="Explaining a SELECT query" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3e790bc-18b2-4c9b-96b1-2e9760fab1c9/mysql-explain-snapshot.png" alt="Screenshot" width="500" height="460" /></a><br>
<em>Using the <code>EXPLAIN</code> statement to explain how MySQL plans to deal with a complex query.</em>

The screenshot shows which tables and indices are being used, the <code>JOIN</code> types, the number of rows analyzed, and a lot more information. A comprehensive page on the MySQL website <a href="https://dev.mysql.com/doc/refman/5.5/en/explain-output.html">explains what the EXPLAIN explains</a>, and another much shorter page goes over how to use that information to <a href="https://dev.mysql.com/doc/refman/5.5/en/using-explain.html">optimize your queries</a> (by adding indices, for instance).</p>

## …Or Just Cheat

Finally, returning again to the advanced example above for “Customers who bought this product also bought…,” you could also simply change the functionality to be something less complicated for starters. You could call it “Recommended products” and just return a few other products from the same category or return some hand-picked recommendation.</p>

## Conclusion

This article has shown a number of techniques for improving database performance, ranging from simple to quite complex. While all well-built websites should already incorporate most of these techniques (particularly the database indices and <code>JOIN</code>s), the techniques do get overlooked.

There is also a lot of debate on forums around the Web about the effectiveness and reliability of some of these techniques (i.e. measuring speed, indexing, optimization, how best to use the cache, etc.), so the advice here is not definitive, but hopefully it gives you an overview of what’s available.

If your website starts to mysteriously slow down after a few months or years, you will at least have a starting point for figuring out what’s wrong.

{{< signature "al" >}}


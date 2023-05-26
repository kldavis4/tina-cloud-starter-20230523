---
title: How To Create Native Admin Tables In WordPress The Right Way
slug: native-admin-tables-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/685f4963-b432-4318-8646-b95c889bc40a/wordpress-blue-illu.jpg
date: 2011-11-03T14:00:26.000Z
author: jeremy-desvaux-de-marigny
description: >-
  WordPress list tables are a very common element of the WordPress admin interface but creating one of those tables is not really an intuitive thing to do when you haven’t done it before. In this article, we’ll see how to generate some native admin tables the right way.
categories:
  - WordPress
  - Tutorials
  - Admin
  - Techniques (WP)
---
List tables are a common element in WordPress’ administration interface. They are used on nearly all default admin pages with lists, and developers often integrate them into their plugins. But creating one of these tables is not really intuitive if you haven’t done it before, and I’ve seen people try to replicate it by using WordPress CSS classes in custom markup and even by replicating the CSS from scratch.

In this article, we’ll see how WordPress provides functionality that can be used to generate native admin tables. We’ll look at a typical WordPress table and its different components and show how to implement it the right way.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Customize The WordPress Admin Easily](https://www.smashingmagazine.com/2012/05/customize-wordpress-admin-easily/)
*   [Modifying Admin Post Lists In WordPress](https://www.smashingmagazine.com/2013/12/modifying-admin-post-lists-in-wordpress/)
*   [10 Steps To Protect The Admin Area In WordPress](https://www.smashingmagazine.com/2009/01/10-steps-to-protect-the-admin-area-in-wordpress/)

{{% feature-panel %}}

## Presentation Of A WordPress Table

To better understand the various elements we’ll be talking about, let’s take the default link manager that you see when you click “Links” in the admin menu. Here’s what you see:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c902e69-5fa8-40f3-af65-32b7faa0198b/sm-wplt1.jpg"><img loading="lazy" decoding="async" class="103872" title="The default page for managing links in WordPress 3.2." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c902e69-5fa8-40f3-af65-32b7faa0198b/sm-wplt1.jpg" alt="The default page for managing links in WordPress 3.2." width="500" height="246" /></a><br>
<em>The default page for managing links in WordPress 3.2.</em>

As you can see, a few different elements precede the table that enable you to perform actions on the table. Then we have the table’s header, the rows, the table’s footer and, finally, some more actions.</p>

### Before and After the Table

WordPress’ admin interface is consistent, so you’ll get used to finding elements in certain places as you navigate.

Before and after the admin tables, for example, are where you would usually find options to take action on the table. These include bulk actions, which enable you to edit and delete multiple posts and to filter the list based on a certain criteria.

We’ll see in the second part of this article how to interact with these two areas and how to display options there.</p>

### Header and Footer

Speaking of consistency, every admin table in WordPress has a header and footer.

Following the same logic, they display the the same information: the titles of the columns. Some of the titles are simple and some are linked (meaning that the table can be ordered according to that column).</p>

### The Content

Obviously, the reason you would create a table is to put some content in it. This content would go in the rows between the header and footer.

## How Is This Done In WordPress?

As we’ve just seen, a WordPress table has three families of elements. Let’s see how to achieve this, using a concrete example.</p>

### Our Example Table

Most of the time, the data we want to display will be in the form of a SQL table. We’ll use the default links table in WordPress as our example, but the concepts apply to any database table and could easily be adapted to your needs. Our table will have the following structure:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7dbdf409-cd95-42f3-919d-15a515db500d/sm-wplt2.jpg"><img loading="lazy" decoding="async" class="103875" title="Structure of the links table" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7dbdf409-cd95-42f3-919d-15a515db500d/sm-wplt2.jpg" alt="Structure of the links table" width="500" height="185" /></a>

This table contains some default data that will be perfect for testing.</p>

### Using the List Table Class

To create an HTML table in WordPress, we don’t have to write a lot of HTML. Instead, we can rely on the precious work of the <code>WP_List_Table</code> class. As <a href="https://codex.wordpress.org/Function_Reference/WP_List_Table">explained by the WordPress Codex</a>, this class is a powerful tool for generating tables.

It is tailored for back-end developers, so we can concentrate on the most essential task (the treatment of the data), leaving the other tasks (such as HTML rendering) to WordPress.

The <code>WP_List_Table</code> class is essentially a little framework whose functionality we can rely on to prepare our table. This is an object-oriented approach, because we’ll be creating an object that extends <code>WP_List_Table</code> and using that, instead of using <code>WP_List_Table</code> directly.

Let’s create a class <code>Link_List_Table</code> with a simple constructor:

<pre><code class="language-php">class Link_List_Table extends WP_List_Table {

   /**
    * Constructor, we override the parent to pass our own arguments
    * We usually focus on three parameters: singular and plural labels, as well as whether the class supports AJAX.
    */
    function __construct() {
       parent::__construct( array(
      'singular'=&gt; 'wp_list_text_link', //Singular label
      'plural' =&gt; 'wp_list_test_links', //plural label, also this well be one of the table css class
      'ajax'   =&gt; false //We won't support Ajax for this table
      ) );
    }

}</code></pre>

This is the starting point of our table. We now have an object that has access to the properties and methods of its parent, and we’ll customize it to suit our needs.

Keeping in mind the three types of elements we saw earlier, let’s see now what to add to our class to get the same result.</p>

### How to Add Elements Before and After the Table

To display content before or after the table, we need to add a method named <code>extra_tablenav</code> to our class. This method can be implemented as follows:

<pre><code class="language-php">/**
 * Add extra markup in the toolbars before or after the list
 * @param string $which, helps you decide if you add the markup after (bottom) or before (top) the list
 */
function extra_tablenav( $which ) {
   if ( $which == "top" ){
      //The code that goes before the table is here
      echo"Hello, I'm before the table";
   }
   if ( $which == "bottom" ){
      //The code that goes after the table is there
      echo"Hi, I'm after the table";
   }
}</code></pre>

The interesting thing here is that the <code>extra_tablenav</code> method takes one parameter, named <code>$which</code>, and this function is called twice by <code>Link_List_Table</code>, (once before the table and once after). When it’s called before, the value of the <code>$which</code> parameter is <code>top</code>, and when it’s called a second time, after the table, its value is <code>bottom</code>.

You can then use this to position the various elements that you’d like to appear before and after the table.

This function exists in the parent <code>WP_List_Table</code> class in WordPress, but it doesn’t return anything, so if you don’t override it, nothing bad will happen; the table just won’t have any markup before or after it.</p>

### How to Prepare the Table’s Header and Footer

In the header and footer, we have the column’s headers, and some of them are sortable.

We’ll add to our class a method named <code>get_columns</code> that is used to <strong>define the columns</strong>:

<pre><code class="language-php">/**
 * Define the columns that are going to be used in the table
 * @return array $columns, the array of columns to use with the table
 */
function get_columns() {
   return $columns= array(
      'col_link_id'=&gt;__('ID'),
      'col_link_name'=&gt;__('Name'),
      'col_link_url'=&gt;__('Url'),
      'col_link_description'=&gt;__('Description'),
      'col_link_visible'=&gt;__('Visible')
   );
}</code></pre>

The code above will build an array in the form of <code>'column_name'=&gt;'column_title'</code>. This array would then be used by your class to display the columns in the header and footer, in the order you’ve written them, so defining that is pretty straightforward.

Plenty of fields are in the links table, but not all of them interest us. With our <code>get_columns</code> method, we’ve chosen to display only a few of them: the ID, the name, the URL, the description of the link, as well as whether the link is visible.

Unlike the <code>extra_tablenav</code> method, the <code>get_columns</code> is a parent method that <em>must</em> be overridden in order to work. This makes sense, because if you don’t declare any columns, the table will break.

To specify the columns to which to add <strong>sorting functionality</strong>, we’ll add the <code>get_sortable</code> columns method to our class:

<pre><code class="language-php">/**
 * Decide which columns to activate the sorting functionality on
 * @return array $sortable, the array of columns that can be sorted by the user
 */
public function get_sortable_columns() {
   return $sortable = array(
      'col_link_id'=&gt;'link_id',
      'col_link_name'=&gt;'link_name',
      'col_link_visible'=&gt;'link_visible'
   );
}</code></pre>

Here again, we’ve built a PHP array. The model for this one is <code>'column_name'=&gt;'corresponding_database_field'</code>. In other words, the <code>column_name</code> must be the same as the column name defined in the <code>get_columns</code> method, and the <code>corresponding_database_field</code> must be the same as the name of the corresponding field in the database table.

The code we have just written specifies that we would like to add sorting functionality to three columns (“ID,” “Name” and “Visible”). If you don’t want the user to be able to sort any columns or if you just don’t want to implement this method, WordPress will just assume that no columns are sortable.

At this point, our class is ready to handle quite a few things. Let’s look now at how to display the data.</p>

### How to Display the Table’s Rows

The first steps in preparing the list table are very quick. We just have to tackle a few more things in the treatment of data.

To make the list table display your data, you’ll need to prepare your items and assign them to the table. This is handled by the <code>prepare_items</code> method:

<pre><code class="language-php">/**
 * Prepare the table with different parameters, pagination, columns and table elements
 */
function prepare_items() {
   global $wpdb, $_wp_column_headers;
   $screen = get_current_screen();

   /* -- Preparing your query -- */
        $query = "SELECT * FROM $wpdb-&gt;links";

   /* -- Ordering parameters -- */
       //Parameters that are going to be used to order the result
       $orderby = !empty($_GET["orderby"]) ? mysql_real_escape_string($_GET["orderby"]) : 'ASC';
       $order = !empty($_GET["order"]) ? mysql_real_escape_string($_GET["order"]) : ’;
       if(!empty($orderby) &amp; !empty($order)){ $query.=' ORDER BY '.$orderby.' '.$order; }

   /* -- Pagination parameters -- */
        //Number of elements in your table?
        $totalitems = $wpdb-&gt;query($query); //return the total number of affected rows
        //How many to display per page?
        $perpage = 5;
        //Which page is this?
        $paged = !empty($_GET["paged"]) ? mysql_real_escape_string($_GET["paged"]) : ’;
        //Page Number
        if(empty($paged) || !is_numeric($paged) || $paged&lt;=0 ){ $paged=1; } //How many pages do we have in total? $totalpages = ceil($totalitems/$perpage); //adjust the query to take pagination into account if(!empty($paged) &amp;&amp; !empty($perpage)){ $offset=($paged-1)*$perpage; $query.=' LIMIT '.(int)$offset.','.(int)$perpage; } /* -- Register the pagination -- */ $this-&gt;set_pagination_args( array(
         "total_items" =&gt; $totalitems,
         "total_pages" =&gt; $totalpages,
         "per_page" =&gt; $perpage,
      ) );
      //The pagination links are automatically built according to those parameters

   /* -- Register the Columns -- */
      $columns = $this-&gt;get_columns();
      $_wp_column_headers[$screen-&gt;id]=$columns;

   /* -- Fetch the items -- */
      $this-&gt;items = $wpdb-&gt;get_results($query);
}</code></pre>

As you can see, this method is a bit more complex than the previous ones we added to our class. So, let’s see what is actually happening here:

1.  **Preparing the query** The first thing to do is specify the general query that will return the data. Here, it’s a generic `SELECT` on the links table.
2.  **Ordering parameters** The second section is for the ordering parameters, because we have specified that our table can be sorted by certain fields. In this section, we are getting the field (if any) by which to order our record (`$_GET['order']`) and the order itself (`$_GET['orderby']`). We then adjust our query to take those into account by appending an `ORDER BY` clause.
3.  **Pagination parameters** The third section deals with pagination. We specify how many items are in our database table and how many to show per page. We then get the current page number (`$_GET['paged']`) and then adapt the SQL query to get the correct results based on those pagination parameters.
4.  **Registration** This part of the function takes all of the parameters we have prepared and assigns them to our table.
5.  **Ready to go** Our list table is now set with all of the information it needs to display our data. It knows what query to execute to get the records from the database; it knows how many records will be returned; and all the pagination parameters are ready. This is an essential method of your list table class. If you don’t implement it properly, WordPress won’t be able to retrieve your data. If the method is missing in your class, WordPress will return an error telling you that the `prepare_items` method must be overridden.
6.  **Displaying the rows** This is it! Finally, we get to the method responsible for displaying the records of data. It is named `display_rows` and is implemented as follows.

<pre><code class="language-php">/**
 * Display the rows of records in the table
 * @return string, echo the markup of the rows
 */
function display_rows() {

   //Get the records registered in the prepare_items method
   $records = $this-&gt;items;

   //Get the columns registered in the get_columns and get_sortable_columns methods
   list( $columns, $hidden ) = $this-&gt;get_column_info();

   //Loop for each record
   if(!empty($records)){foreach($records as $rec){

      //Open the line
        echo '&lt; tr id="record_'.$rec-&gt;link_id.'"&gt;';
      foreach ( $columns as $column_name =&gt; $column_display_name ) {

         //Style attributes for each col
         $class = "class='$column_name column-$column_name'";
         $style = "";
         if ( in_array( $column_name, $hidden ) ) $style = ' style="display:none;"';
         $attributes = $class . $style;

         //edit link
         $editlink  = '/wp-admin/link.php?action=edit&amp;link_id='.(int)$rec-&gt;link_id;

         //Display the cell
         switch ( $column_name ) {
            case "col_link_id":  echo '&lt; td '.$attributes.'&gt;'.stripslashes($rec-&gt;link_id).'&lt; /td&gt;';   break;
            case "col_link_name": echo '&lt; td '.$attributes.'&gt;<strong><a title="Edit" href="'.$editlink.'">'.stripslashes($rec-&gt;link_name).'</a></strong>&lt; /td&gt;'; break;
            case "col_link_url": echo '&lt; td '.$attributes.'&gt;'.stripslashes($rec-&gt;link_url).'&lt; /td&gt;'; break;
            case "col_link_description": echo '&lt; td '.$attributes.'&gt;'.$rec-&gt;link_description.'&lt; /td&gt;'; break;
            case "col_link_visible": echo '&lt; td '.$attributes.'&gt;'.$rec-&gt;link_visible.'&lt; /td&gt;'; break;
         }
      }

      //Close the line
      echo'&lt; /tr&gt;';
   }}
}</code></pre>

This function gets the data prepared by the <code>prepare_items</code> method and loops through the different records to build the markup of the corresponding table row.

With this method, you have great control over how to display the data. If you do not wish to add this method to your class, then the class will use the parent’s method to render the data in WordPress’ default style.

Your list table class is now finished and ready to be used on one of your pages.

All of the methods we’ve added to our class already exist in the parent <code>WP_List_Table</code> class. But for your child class to work, you must override at least two of them: <code>get_columns</code> and <code>prepare_items</code>.</p>

## Implementation

Now that our list table class is ready, let’s see how we can use it on a page of our choice.</p>

### Where Do We Write It?

The code that we’ll cover in this section has to be written on the page where you want to display the admin table.

We’ll create a very simple demonstration plugin, named “Test WP List Table.” Basically, this plugin will add a link in the WordPress “Plugins” sub-menu. Our code will, therefore, be written in the plugin file.</p>

### Before We Begin

<strong>Important:</strong> the <code>WP_List_Table</code> class is <em>not</em> available in plugins by default. You can use the following snippet to check that it is there:

<pre><code class="language-php">//Our class extends the WP_List_Table class, so we need to make sure that it's there
if(!class_exists('WP_List_Table')){
   require_once( ABSPATH . 'wp-admin/includes/class-wp-list-table.php' );
}</code></pre>

Also, if you have created your <code>Links_List_Table</code> class in an external file, make sure to include it before you start instantiating.</p>

### Instantiate the Table

The first step is to create an instance of our list table class, then call the <code>prepare_items</code> method to fetch the data to your table:

<pre><code class="language-php">//Prepare Table of elements
$wp_list_table = new Links_List_Table();
$wp_list_table-&gt;prepare_items();</code></pre>

### Display It

The <code>$wp_list_table</code> object is now ready to display the table wherever you want.

Build your page’s markup, and wherever you decide to display the table, make a call to the <code>display()</code> method:

<pre><code class="language-php">//Table of elements
$wp_list_table-&gt;display();</code></pre>

Calling the <code>display()</code> method will generate the full markup of the list table, from the before-and-after area to the table’s content, and including the table’s header and footer. It also automatically generates all pagination links for you, so the result should look like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc6d6eeb-6369-4195-8ca5-95e75feaf558/sm-wplt3.jpg"><img loading="lazy" decoding="async" class="103877" title="sm_wplt3_" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc6d6eeb-6369-4195-8ca5-95e75feaf558/sm-wplt3.jpg" alt="" width="500" height="161" /></a>

In the download accompanying this article, you’ll find the complete PHP file containing the class definition and the example of its implementation. It is named <em>testWPListTable.php</em>, and it is written in the form of a simple plugin that you can put in your WordPress plugin folder and activate if you want to see what it does.</p>

## Conclusion

Creating a PHP class merely to display a table of data might seem like overkill. But this class is very easy to create and customize. And once it’s done, you’ll be happy that the parts of tables that are difficult to implement, such as pagination and reordering, are now taken care of.

Also, because the generated markup is exactly what WordPress supports, if an update is released one day, your tables will remain in good shape.

The PHP code we’ve used is clean and easy to understand. And mastering the default functionality won’t take a long time.

What we’ve seen today is the basic implementation of a WordPress list table, but you can add other supported methods to the class for extra functionality.

For more information, read the Codex page dedicated to <a href="https://codex.wordpress.org/Function_Reference/WP_List_Table">WordPress list tables</a>, and have a look at another <a href="https://wordpress.org/extend/plugins/custom-list-table-example">custom list table example</a>.

I hope you’ve found this article useful, and I wish you good luck with list tables!

{{< signature "al" >}}


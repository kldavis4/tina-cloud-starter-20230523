---
title: Customizing Tree-Like Data Structures In WordPress With The Walker Class
slug: customize-tree-like-data-structures-wordpress-walker-class
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94a0528d-4364-49a0-9113-55cfae016afd/01-wpcommentsstructure-opt-small.png
date: 2015-10-14T22:25:14.000Z
author: carlodaniele
description: >-
  In WordPress, a **navigation menu**, a list of categories or pages, and a list
  of comments all share one common characteristic: They are the **visual
  representation of tree-like data structures**. This means that a relationship
  of superordination and subordination exists among the elements of each data
  tree.

  There will be elements that are parents of other elements and, conversely,
  elements that are children of other elements. A reply to a comment depends
  logically on its parent, in the same way that a submenu item depends logically
  on the root element of the tree (or subtree).
categories:
  - WordPress
  - Tutorials
  - Techniques (WP)
---
In WordPress, a <strong>navigation menu</strong>, a list of categories or pages, and a list of comments all share one common characteristic: They are the <strong>visual representation of tree-like data structures</strong>. This means that a relationship of superordination and subordination exists among the elements of each data tree.

There will be elements that are parents of other elements and, conversely, elements that are children of other elements. A reply to a comment depends logically on its parent, in the same way that a submenu item depends logically on the root element of the tree (or subtree).</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Rapid Front-End Prototyping With WordPress](https://www.smashingmagazine.com/2015/06/rapid-front-end-prototyping-with-wordpress/)
*   [How To Create And Customize A WordPress Child Theme](https://www.smashingmagazine.com/2016/01/create-customize-wordpress-child-theme/)
*   [Create A Responsive, Mobile-First WordPress Theme](https://www.smashingmagazine.com/2012/06/create-responsive-mobile-first-wordpress-theme/)
*   [Creating A Complete Web App In Foundation For Apps](https://www.smashingmagazine.com/2015/04/creating-web-app-in-foundation-for-apps/)

Starting with version 2.1, WordPress provides the <a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/class-wp-walker.php"><code>Walker</code> abstract class</a>, with the specific function of traversing these tree-like data structures. But an abstract class does not produce any output by itself. It has to be extended with a concrete child class that builds the HTML bricks for specific lists of items. With this precise function, WordPress provides the <code>Walker_Category</code> class to produce a nested list of categories, the <a href="https://codex.wordpress.org/Class_Reference/Walker_Page"><code>Walker_Page</code> class</a>, which builds a list of pages, and several other <code>Walker</code> concrete child classes.

{{% feature-panel %}}

But when we build a WordPress theme, we might need to customize the HTML list’s default structure to fit our particular needs. We may want to add a description to a menu item, add custom class names or perhaps redefine the HTML structure of a list of categories or comments.

Before we begin, let’s look at the most important concept in this article.</p>

## Tree-Like Data Structures

<a href="https://en.wikipedia.org/wiki/Tree_(data_structure)">Wikipedia defines a tree</a> as a hierarchical organization of data:
<blockquote>“A tree data structure can be defined recursively (locally) as a collection of nodes (starting at a root node), where each node is a data structure consisting of a value, together with a list of references to nodes (the ‘children’), with the constraints that no reference is duplicated, and none points to the root.”</blockquote>

So, the structure is characterized by a root element (at the first level), parent elements (which are directly referenced to subordered elements, named children), siblings (which are elements placed at the same hierarchical level) and descendant and ancestor elements (which are connected by more than one parent-child relation).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d5aed4-b295-4f81-b8a3-cc5808ef0a65/01-wpcommentsstructure-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94a0528d-4364-49a0-9113-55cfae016afd/01-wpcommentsstructure-opt-small.png" alt="The wp_comments table structure" /></a><figcaption>Each element in the <code>wp_comments</code> is referenced to its parent by the value of the <code>comment_parent</code> field. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d5aed4-b295-4f81-b8a3-cc5808ef0a65/01-wpcommentsstructure-opt.png">View large version</a>)</figcaption></figure>

As an example of this kind of structure, let's take the <code>wp_comments</code> table from the WordPress database. The <code>comment_parent</code> field stores the parent ID of each element in the structure, making it possible to create the reference from the child node to its parent.</p>

## What We’ll Be Doing

Before moving forward, I'll show you a simple example of a concrete child class producing the HTML markup of a category list.

The category list in WordPress is printed out by the <code>wp_list_categories</code> template tag. When we call this function, it executes the <code>Walker_Category</code> class, which actually builds the HTML structure, producing something like the following code:

<pre><code class="language-markup">&lt;li class="categories"&gt;Categories
   &lt;ul&gt;  
      &lt;li class="cat-item cat-item-10"&gt;
         &lt;a href="https://example.com/wordpress/category/coding/"&gt;Coding&lt;/a&gt;
         &lt;ul class="children"&gt;
            &lt;li class="cat-item cat-item-39"&gt;
               &lt;a href="https://example.com/wordpress/category/coding/php/"&gt;PHP&lt;/a&gt;
            &lt;/li&gt;
         &lt;/ul&gt;
      &lt;/li&gt;
      &lt;li class="cat-item cat-item-11"&gt;
         &lt;a href="https://example.com/wordpress/category/design/"&gt;Design&lt;/a&gt;
      &lt;/li&gt;
   &lt;/ul&gt;
&lt;/li&gt;
</code></pre>

<code>wp_list_categories</code> will print the output produced by the <code>Walker_Category</code> concrete class. It will be a wrapper list item holding a nested list of categories.

Now, suppose you don't like this kind of list, and you want to print custom HTML code. You can do this trick by defining your own <code>Walker</code> extention. In your theme’s <code>functions.php</code> file, add the following code:

<pre><code class="language-php">class My_Custom_Walker extends Walker
{
   public $tree_type = 'category';

   public $db_fields = array ('parent' =&gt; 'parent', 'id' =&gt; 'term_id');

   public function start_lvl( &amp;$output, $depth = 0, $args = array() ) {
      $output .= "&lt;ul class='children'&gt;\n";
   }

   public function end_lvl( &amp;$output, $depth = 0, $args = array() ) {
      $output .= "&lt;/ul&gt;\n";
   }

   public function start_el( &amp;$output, $category, $depth = 0, $args = array(), $current_object_id = 0 ) {
      $output .= "&lt;li&gt;" . $category-&gt;name . "\n";
   }

   public function end_el( &amp;$output, $category, $depth = 0, $args = array() ) {
      $output .= "&lt;/li&gt;\n";
   }
}
</code></pre>

Even if you don’t know a lot about <a href="https://php.net/manual/en/language.oop5.basic.php">PHP classes</a>, the code is quite descriptive. The <code>start_lvl()</code> method prints the <code>start</code> tag for each level of the tree (usually a <code>&lt;ul&gt;</code> tag), while <code>end_lvl()</code> prints the end of each level. In the same way, the <code>start_el</code> and <code>end_el</code> methods open and close each item in the list.

This is just a basic example, and we won't dive deep into the <code>Walker</code> properties and methods for now. I'll just say that the concrete child class <code>My_Custom_Walker</code> extends the abstract class <code>Walker</code>, redefining some of its properties and methods.

As I wrote above, the category list is printed out by the <code>wp_list_categories</code> template tag, but the HTML structure is built by the <code>Walker_Category</code> class. WordPress allows us to pass a custom <code>walker</code> class to the <code>template</code> tag. The new <code>walker</code> will build a custom HTML structure that will be printed on the screen by <code>wp_list_categories</code>.

As a first example, let's create a shortcode that will print new markup for the lists of categories. In your <code>functions.php</code> file, add the following code:

<pre><code class="language-php">function my_init() {
   add_shortcode( 'list', 'my_list' );
}
add_action('init', 'my_init');

function my_list( $atts ){
   $list = wp_list_categories( array( 'echo' =&gt; 0, 'walker' =&gt; new My_Custom_Walker() ) );
   return $list;
}
</code></pre>

We are passing the function an array of two arguments: <code>echo</code> keeps the result in a variable, and <code>walker</code> sets a custom <code>Walker</code> (or <code>Walker_Category</code>) child class.

Finally, the shortcode <code>[list]</code> will print the resulting HTML code:

<pre><code class="language-markup">&lt;ul&gt;
   &lt;li class="categories"&gt;Categories
      &lt;ul&gt;
         &lt;li&gt;Coding
            &lt;ul class="children"&gt;
            &lt;li&gt;PHP&lt;/li&gt;
            &lt;/ul&gt;
         &lt;/li&gt;
         &lt;li&gt;Design&lt;/li&gt;
      &lt;/ul&gt;
   &lt;/li&gt;
&lt;/ul&gt;
</code></pre>

As you can see, the example is very basic but should give you an idea of our goals.

## The `Walker` Class And Its Extensions

The <a href="https://codex.wordpress.org/Class_Reference/Walker"><code>Walker</code> class</a> is defined in <a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/class-wp-walker.php"><code>wp-includes/class-wp-walker.php</code></a> as “a class for displaying various tree-like structures.”

As I mentioned before, it's an <a href="https://php.net/manual/en/language.oop5.abstract.php">abstract class</a> and does not produce any output by itself; rather, it has to be extended by defining one or more concrete child classes. Only these concrete child classes will produce the HTML markup. WordPress provides several extensions of the <code>Walker</code> class, each one producing a hierarchical HTML structure.

Look at the table below:
<table class="article-table three-columns"><br>
<tbody>
<tr>
<th>Class name</th>
<th>Defined in</th>
<th>Extends</th>
</tr>
<tr>
<td><code>Walker_Page</code></td>
<td><a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/post-template.php#L1325">post-template.php</a></td>
<td><code>Walker</code></td>
</tr>
<tr>
<td><code>Walker_PageDropdown</code></td>
<td><a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/post-template.php#L1471">post-template.php</a></td>
<td><code>Walker</code></td>
</tr>
<tr>
<td><code>Walker_Category</code></td>
<td><a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/category-template.php#L962">category-template.php</a></td>
<td><code>Walker</code></td>
</tr>
<tr>
<td><code>Walker_CategoryDropdown</code></td>
<td><a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/category-template.php#L1163">category-template.php</a></td>
<td><code>Walker</code></td>
</tr>
<tr>
<td><code>Walker_Category_Checklist</code></td>
<td><a href="https://core.trac.wordpress.org/browser/tags/4.2.2/src/wp-admin/includes/template.php#L24">template.php</a></td>
<td><code>Walker</code></td>
</tr>
<tr>
<td><code>Walker_Comment</code></td>
<td><a href="https://core.trac.wordpress.org/browser/tags/4.2.2/src/wp-includes/comment-template.php#L1662">comment-template.php</a></td>
<td><code>Walker</code></td>
</tr>
<tr>
<td><code>Walker_Nav_Menu</code></td>
<td><a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/nav-menu-template.php#L16">nav-menu-template.php</a></td>
<td><code>Walker</code></td>
</tr>
<tr>
<td><code>Walker_Nav_Menu_Checklist</code></td>
<td><a href="https://core.trac.wordpress.org/browser/tags/4.2.2/src/wp-admin/includes/nav-menu.php#L237">nav-menu.php</a></td>
<td><code>Walker_Nav_Menu</code></td>
</tr>
<tr>
<td><code>Walker_Nav_Menu_Edit</code></td>
<td><a href="https://core.trac.wordpress.org/browser/tags/4.2.2/src/wp-admin/includes/nav-menu.php#L10">nav-menu.php</a></td>
<td><code>Walker_Nav_Menu</code></td>
</tr>
</tbody>
</table>

This table shows the built-in <code>Walker</code> child classes, the template files they are defined in, and the corresponding parent class.

The goal of this article is to put the <code>Walker</code> class to work, so we need to dive into its structure.</p>

## The `Walker` Class’ Structure

<code>Walker</code> is defined in <a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/class-wp-walker.php"><code>wp-includes/class-wp-walker.php</code></a>. It declares four properties and six main methods, most of which are left empty and should be redefined by the concrete child classes.

The properties are:

*   `$tree_type`
*   `$db_fields`
*   `$max_pages`
*   `$has_children`

### `$tree_type`

This is a string or an array of the data handled by the <code>Walker</code> class and its extentions.</p>

<pre><code class="language-php">public $tree_type;</code></pre>

The <code>Walker</code> class declares the property but does not set its value. To be used, it has to be redeclared by the concrete child class. For example, the <code>Walker_Page</code> class declares the following <code>$tree_type</code> property:

<pre><code class="language-php">public $tree_type = 'page';</code></pre>

Whereas <code>Walker_Nav_menu</code> declares the following <code>$tree_type</code>:

<pre><code class="language-php">public $tree_type = array( 'post_type', 'taxonomy', 'custom' );</code></pre>

### `$db_fields`

Just like $<code>tree_type</code>, <code>$db_fields</code> is declared with no value assigned. In the <code>Walker</code> class’ documentation, it just says that its value is an array:

<pre><code class="language-php">public $db_fields;</code></pre>

The elements of the array should set the database fields providing the ID and the parent ID for each item of the traversed data set.

The <code>Walker_Nav_Menu</code> class redeclares <code>$db_fields</code> as follows:

<pre><code class="language-php">public $db_fields = array( 'parent' =&gt; 'menu_item_parent', 'id' =&gt; 'db_id' );</code></pre>

<code>$db_fields['parent']</code> and <code>$db_fields['id']</code> will be used by the <code>display_element</code> method.</p>

### `$max_pages`

This keeps in memory the maximum number of pages traversed by the <code>paged_walker</code> method. Its initial value is set to <code>1</code>.</p>

<pre><code class="language-php">public $max_pages = 1;</code></pre>

### `$has_children`

This boolean is set to <code>true</code> if the current element has children.</p>

<pre><code class="language-php">public $has_children;</code></pre>

After the properties, the methods are:

*   `start_lvl`
*   `end_lvl`
*   `start_el`
*   `end_el`
*   `display_element`
*   `walk`

### `start_lvl`

This method is executed when the <code>Walker</code> class reaches the root level of a new subtree. Usually, it is the container for subtree elements.</p>

<pre><code class="language-php">public function start_lvl( &amp;$output, $depth = 0, $args = array() ) {}</code></pre>

<code>start_lvl()</code> takes three arguments:
<table class="article-table three-columns"><br>
<tbody>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Description</th>
</tr>
<tr>
<td><code>$output</code></td>
<td>string</td>
<td>passed by reference; used to append additional content</td>
</tr>
<tr>
<td><code>$depth</code></td>
<td>int</td>
<td>depth of the item</td>
</tr>
<tr>
<td><code>$args</code></td>
<td>array</td>
<td>an array of additional arguments</td>
</tr>
</tbody>
</table>

Because it produces HTML output, <code>start_lvl</code> should be redefined when extending the <code>Walker</code> class. For instance, the <code>start_lvl</code> method of the <code>Walker_Nav_Menu</code> class will output a <code>ul</code> element and is defined as follows:

<pre><code class="language-php">public function start_lvl( &amp;$output, $depth = 0, $args = array() ) {
   $indent = str_repeat("\t", $depth);
   $output .= "\n$indent&lt;ul class=\"sub-menu\"&gt;\n";
}
</code></pre>

### `end_lvl`

The second method of the <code>Walker</code> class closes the tag previously opened by <code>start_lvl</code>.</p>

<pre><code class="language-php">public function end_lvl( &amp;$output, $depth = 0, $args = array() ) {}</code></pre>

The <code>end_lvl</code> method of <code>Walker_Nav_Menu</code> closes the unordered list:

<pre><code class="language-php">public function end_lvl( &amp;$output, $depth = 0, $args = array() ) {
   $indent = str_repeat("\t", $depth);
   $output .= "$indent&lt;/ul&gt;\n";
}
</code></pre>

### `start_el`

This method opens the tag corresponding to each element of the tree. Obviously, if <code>start_lvl</code> opens a <code>ul</code> element, then <code>start_el</code> must open an <code>li</code> element. The <code>Walker</code> class defines <code>start_el</code> as follows:

<pre><code class="language-php">public function start_el( &amp;$output, $object, $depth = 0, $args = array(), $id = 0 ) {}</code></pre>

<table class="article-table three-columns">
<tbody>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Description</th>
</tr>
<tr>
<td><code>$output</code></td>
<td>string</td>
<td>passed by reference; used to append additional content</td>
</tr>
<tr>
<td><code>$object</code></td>
<td>object</td>
<td>the data object</td>
</tr>
<tr>
<td><code>$depth</code></td>
<td>int</td>
<td>depth of the item</td>
</tr>
<tr>
<td><code>$args</code></td>
<td>array</td>
<td>an array of additional arguments</td>
</tr>
<tr>
<td><code>$id</code></td>
<td>int</td>
<td>current item ID</td>
</tr>
</tbody>
</table>

### `end_el`

It closes the tag opened by <code>start_el</code>.</p>

<pre><code class="language-php">public function end_el( &amp;$output, $object, $depth = 0, $args = array() ) {}</code></pre>

Finally, we've reached the core of the <code>Walker</code> class. The following two methods are used to iterare over the elements of the arrays of objects retrieved from the database.</p>

### `display_element`

I won't show the full code here, because you can find it in the <a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/class-wp-walker.php#L112">WordPress Trac</a>. I'll just say that this method displays the elements of the tree.</p>

<pre><code class="language-php">public function display_element( $element, &amp;$children_elements, $max_depth, $depth, $args, &amp;$output ) {}
</code></pre>

<code>display_element</code> takes the following arguments:
<table class="article-table three-columns"><br>
<tbody>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Description</th>
</tr>
<tr>
<td><code>$element</code></td>
<td>object</td>
<td>the data object</td>
</tr>
<tr>
<td><code>$children_elements</code></td>
<td>array</td>
<td>list of elements to continue traversing</td>
</tr>
<tr>
<td><code>$max_depth</code></td>
<td>int</td>
<td>maximum depth to traverse</td>
</tr>
<tr>
<td><code>$depth</code></td>
<td>int</td>
<td>depth of current element</td>
</tr>
<tr>
<td><code>$args</code></td>
<td>array</td>
<td>an array of arguments</td>
</tr>
<tr>
<td><code>$output</code></td>
<td>string</td>
<td>passed by reference; used to append additional content</td>
</tr>
</tbody>
</table>

This method does not output HTML on its own. The markup will be built by a call to each of the previously described methods: <code>start_lvl</code>, <code>end_lvl</code>, <code>start_el</code> and <code>end_el</code>.</p>

### `walk`

<code>walk</code> is the core of the <code>Walker</code> class. It iterates over the elements of the tree depending on the value of <code>$max_depth</code> argument (see the Trac for the <a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/class-wp-walker.php#L175">full code</a>).</p>

<pre><code class="language-php">public function walk( $elements, $max_depth ) {}</code></pre>

<code>walk</code> takes two arguments.
<table class="article-table three-columns"><br>
<tbody>
<tr>
<th>Argument</th>
<th>Type</th>
<th>Description</th>
</tr>
<tr>
<td><code>$elements</code></td>
<td>array</td>
<td>an array of elements</td>
</tr>
<tr>
<td><code>$max_depth</code></td>
<td>int</td>
<td>maximum depth to traverse</td>
</tr>
</tbody>
</table>

Other methods are used for more specific pourposes.</p>

### `paged_walk`

This builds a page of nested elements. The method establishes which elements of the data tree should belong to a page, and then it builds the markup by calling <code>display_element</code> and outputs the result.</p>

<pre><code class="language-php">public function paged_walk( $elements, $max_depth, $page_num, $per_page ) {}</code></pre>

### `get_number_of_root_elements`

This gets the number of first-level elements.</p>

<pre><code class="language-php">public function get_number_of_root_elements( $elements ){}</code></pre>

### `unset_children`

This last method unsets the array of child elements for a given root element.</p>

<pre><code class="language-php">public function unset_children( $e, &amp;$children_elements ){}</code></pre>

Now that we've introduced the <code>Walker</code> properties and methods, we can explore one of its possible applications: changing the HTML structure of the navigation menu. The default markup for navigation menus is produced by the <code>Walker_Nav_Menu</code> concrete class. For this reason, we'll create a new concrete <code>Walker</code> child class based on <code>Walker_Nav_Menu</code>, and we'll pass it to <code>wp_nav_menu</code> to replace the output.

But is extending the <code>Walker_Nav_Menu</code> class always necessary when rebuilding a menu? Of course not!

Most of the time, a call to the <code>wp_nav_menu</code> template tag will suffice.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca42f8bf-e3b4-4470-ad0a-7c7d63b30d38/02-themelocation-opt.png" alt="Menus admin page" /><figcaption>In the “Menus” editing page, setting theme locations for each custom menu is possible.</figcaption></figure>

## Basic Customization Of The Navigation Menu: The `wp_nav_menu` Template Tag

The navigation menu can be included in the theme’s template files with a call to the <code>wp_nav_menu()</code> template tag. This function takes just one argument, an array of parameters that is well described <a href="https://codex.wordpress.org/Function_Reference/wp_nav_menu">in the Codex</a>.</p>

<code>wp_nav_menu()</code> can be included in your templates as follows:

<pre><code class="language-php">$defaults = array(
   'theme_location'     =&gt; ’,
   'menu'            =&gt; ’,
   'container'       =&gt; 'div',
   'container_class' =&gt; ’,
   'container_id'    =&gt; ’,
   'menu_class'         =&gt; 'menu',
   'menu_id'         =&gt; ’,
   'echo'            =&gt; true,
   'fallback_cb'     =&gt; 'wp_page_menu',
   'before'          =&gt; ’,
   'after'           =&gt; ’,
   'link_before'     =&gt; ’,
   'link_after'         =&gt; ’,
   'items_wrap'         =&gt; '&lt;ul id="%1$s" class="%2$s"&gt;%3$s&lt;/ul&gt;',
   'depth'           =&gt; 0,
   'walker'          =&gt; ’
);

wp_nav_menu( $defaults );
</code></pre>

WordPress provides many parameters to configure the navigation menu. We can change the menu’s container (it defaults to a <code>div</code>), the container's CSS class and ID, as well as the text strings and markup to be included before and after the anchor element and before and after the item’s title. Furthermore, we can change the root element’s structure (<code>items_wrap</code>) and the depht of the tree.

So, we don't need to extend the <code>Walker</code> (or the <code>Walker_Nav_Menu</code>) class each time we want to make changes to the menu’s structure — only when we have to produce more advanced structural customizations. This happens when we have to assign CSS classes to the menu elements when a specific condition occurs, or when we have to add data or HTML code to the menu items.

This can be done by setting a value for the <code>walker</code> parameter, which will be nothing but an instance of a custom concrete class. So, from now on, we'll dive more and more deeply into WordPress menus, from changing the menu structure to adding custom fields to the menu items' editing boxes. As I said, we'll do this job by extending the <code>Walker_Nav_Menu</code>, so it's time to get acquainted with it.</p>

## The `Walker_Nav_Menu` Class

The <code>Walker_Nav_Menu</code> class is defined in <a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/nav-menu-template.php"><code>wp-includes/nav-menu-template.php</code></a>. This is the class used by WordPress to build the navigation menu’s structure. Each time you want to make relevant changes to the menu’s default structure, you can extend <code>Walker_Nav_Menu</code>.

The concrete class redeclares the <code>$tree_type</code> and <code>$db_fields</code> properties and the <code>start_lvl</code>, <code>end_lvl</code>, <code>start_el</code> and <code>end_el</code> methods.</p>

<pre><code class="language-php">class Walker_Nav_Menu extends Walker {

   public $tree_type = array( 'post_type', 'taxonomy', 'custom' );

   public $db_fields = array( 'parent' =&gt; 'menu_item_parent', 'id' =&gt; 'db_id' );

   public function start_lvl( &amp;$output, $depth = 0, $args = array() ) {
      $indent = str_repeat("\t", $depth);
      $output .= "\n$indent&lt;ul class=\"sub-menu\"&gt;\n";
   }

   public function end_lvl( &amp;$output, $depth = 0, $args = array() ) {
      $indent = str_repeat("\t", $depth);
      $output .= "$indent&lt;/ul&gt;\n";
   }

   public function start_el( &amp;$output, $item, $depth = 0, $args = array(), $id = 0 ) {
      // code below
   }

   public function end_el( &amp;$output, $item, $depth = 0, $args = array() ) {
      $output .= "&lt;/li&gt;\n";
   }

} // Walker_Nav_Menu
</code></pre>

The <code>start_el</code> public method builds the HTML markup of the opening <code>li</code> tag for each menu item. It is defined as follows:

<pre><code class="language-php">public function start_el( &amp;$output, $item, $depth = 0, $args = array(), $id = 0 ) {
   $indent = ( $depth ) ? str_repeat( "\t", $depth ) : ’;

   $classes = empty( $item-&gt;classes ) ? array() : (array) $item-&gt;classes;
   $classes[] = 'menu-item-' . $item-&gt;ID;

   $class_names = join( ' ', apply_filters( 'nav_menu_css_class', array_filter( $classes ), $item, $args, $depth ) );
   $class_names = $class_names ? ' class="' . esc_attr( $class_names ) . '"' : ’;

   $id = apply_filters( 'nav_menu_item_id', 'menu-item-'. $item-&gt;ID, $item, $args, $depth );
   $id = $id ? ' id="' . esc_attr( $id ) . '"' : ’;

   $output .= $indent . '&lt;li' . $id . $class_names .'&gt;';

   $atts = array();
   $atts['title']  = ! empty( $item-&gt;attr_title ) ? $item-&gt;attr_title : ’;
   $atts['target'] = ! empty( $item-&gt;target )     ? $item-&gt;target     : ’;
   $atts['rel']    = ! empty( $item-&gt;xfn )        ? $item-&gt;xfn        : ’;
   $atts['href']   = ! empty( $item-&gt;url )        ? $item-&gt;url        : ’;

   $atts = apply_filters( 'nav_menu_link_attributes', $atts, $item, $args, $depth );

   $attributes = ’;
   foreach ( $atts as $attr =&gt; $value ) {
      if ( ! empty( $value ) ) {
         $value = ( 'href' === $attr ) ? esc_url( $value ) : esc_attr( $value );
         $attributes .= ' ' . $attr . '="' . $value . '"';
      }
   }

   $item_output = $args-&gt;before;
   $item_output .= '&lt;a'. $attributes .'&gt;';

   $item_output .= $args-&gt;link_before . apply_filters( 'the_title', $item-&gt;title, $item-&gt;ID ) . $args-&gt;link_after;
   $item_output .= '&lt;/a&gt;';
   $item_output .= $args-&gt;after;

   $output .= apply_filters( 'walker_nav_menu_start_el', $item_output, $item, $depth, $args );
}
</code></pre>

The code is quite self-explanatory:

*   `$indent` stores a number of `'/t'` strings corresponding to `$depth`’s value;
*   `$classes` is an array of the CSS classes assigned to the list item;
*   `$id` records the element's ID, composed by the prefix `'menu-item-'` and the item’s ID retrieved from the database;
*   `$atts` is an array of the element's attributes;
*   `$item_output` keeps track of the HTML code before it is assigned to `$output`;
*   `$output` stores the HTML markup.</p>

## Extending The `Walker_Nav_Menu` Class

When building your custom navigation menu markup, you might decide to extend the <code>Walker</code> class itself or its concrete child class <code>Walker_Nav_Menu</code>. If you opt to extend the <code>Walker</code> class, you'll need to define all necessary properties and methods. Otherwise, if you choose to extend the concrete child class, you'll just need to define those methods whose output has to be changed.

The following example describes a real-life situation in which the default menu’s structure has to be changed in order to integrate a WordPress theme with the Foundation 5 framework.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a597b7fc-be27-4901-8b00-2a35332fcdef/03-foundationhomepage-opt.png" alt="Foundation 5 home page" /><figcaption>Foundation 5’s home page.</figcaption></figure>

## A Working Example: The Foundation Top Bar As WordPress Navigation Menu

<a href="https://foundation.zurb.com/">Foundation 5</a> comes with a flexible grid system and with plugins and components that make it easy to develop solid and responsive websites. So, chances are that you'll decide to enrich your theme with all of this great stuff.

First, you need to include all necessary scripts and style sheets in your theme. This isn’t our topic, so we won't dive deep into the configuration, but you can pull out all necessary information directly from <a href="https://foundation.zurb.com/docs/javascript.html">Foundation’s documentation</a> and the <a href="https://codex.wordpress.org/Function_Reference/wp_enqueue_script">WordPress Codex</a>.

Here, we'll see how to force WordPress to display <a href="https://foundation.zurb.com/docs/components/topbar.html">Foundation Top Bar</a> as a navigation menu.

WordPress should print something like the following HTML:

<pre><code class="language-markup">&lt;nav class="top-bar" data-topbar role="navigation"&gt;
   &lt;ul class="title-area"&gt;
   &lt;li class="name"&gt;
      &lt;h1&gt;&lt;a href="#"&gt;My Site&lt;/a&gt;&lt;/h1&gt;
   &lt;/li&gt;
   &lt;!-- Remove the class "menu-icon" to get rid of menu icon. Take out "Menu" to just have icon alone --&gt;
   &lt;li class="toggle-topbar menu-icon"&gt;&lt;a href="#"&gt;&lt;span&gt;Menu&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
   &lt;/ul&gt;

   &lt;div class="top-bar-section"&gt;
      &lt;!-- Left Nav Section --&gt;
      &lt;ul class="left"&gt;
         &lt;li class="active"&gt;&lt;a href="#"&gt;Right Button Active&lt;/a&gt;&lt;/li&gt;
         &lt;li class="has-dropdown"&gt;
            &lt;a href="#"&gt;Left Button Dropdown&lt;/a&gt;
            &lt;ul class="dropdown"&gt;
               &lt;li&gt;&lt;a href="#"&gt;First link in dropdown&lt;/a&gt;&lt;/li&gt;
               &lt;li class="active"&gt;&lt;a href="#"&gt;Active link in dropdown&lt;/a&gt;&lt;/li&gt;
            &lt;/ul&gt;
         &lt;/li&gt;
      &lt;/ul&gt;
   &lt;/div&gt;
&lt;/nav&gt;
</code></pre>

To achieve our goal, add the following code to your <code>header.php</code> file or to whichever template file contains the navigation menu:

<pre><code class="language-markup">&lt;nav class="top-bar" data-topbar role="navigation"&gt;
   &lt;ul class="title-area"&gt;
      &lt;li class="name"&gt;
         &lt;h1&gt;&lt;a href="#"&gt;&lt;?php echo get_bloginfo(); ?&gt;&lt;/a&gt;&lt;/h1&gt;
      &lt;/li&gt;
      &lt;li class="toggle-topbar menu-icon"&gt;&lt;a href="#"&gt;&lt;span&gt;&lt;!--&lt;?php echo get_bloginfo(); ?&gt;--&gt;&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;
   &lt;/ul&gt;
   &lt;?php wp_nav_menu( array(
      'theme_location'     =&gt; 'primary',
      'container_class'    =&gt; 'top-bar-section',
      'menu_class'         =&gt; 'left',
      'walker'             =&gt; new Custom_Foundation_Nav_Menu()) ); ?&gt;
&lt;/nav&gt;
</code></pre>

We have set the Foundation CSS class <code>top-bar-section</code>, along with a custom <code>Walker</code> class, on the navigation menu’s container, location and alignment. Now, we can define <code>Custom_Foundation_Nav_Menu</code>:

<pre><code class="language-php">class Custom_Foundation_Nav_Menu extends Walker_Nav_Menu {
   public function start_lvl( &amp;$output, $depth = 0, $args = array() ) {
      $indent = str_repeat("\t", $depth);

      // add the dropdown CSS class
      $output .= "\n$indent&lt;ul class=\"sub-menu dropdown\"&gt;\n";
   }
   public function display_element( $element, &amp;$children_elements, $max_depth, $depth = 0, $args, &amp;$output ) {

      // add 'not-click' class to the list item
      $element-&gt;classes[] = 'not-click';

      // if element is current or is an ancestor of the current element, add 'active' class to the list item
      $element-&gt;classes[] = ( $element-&gt;current || $element-&gt;current_item_ancestor ) ? 'active' : ’;

      // if it is a root element and the menu is not flat, add 'has-dropdown' class 
      // from https://core.trac.wordpress.org/browser/trunk/src/wp-includes/class-wp-walker.php#L140
      $element-&gt;has_children = ! empty( $children_elements[ $element-&gt;ID ] );
      $element-&gt;classes[] = ( $element-&gt;has_children &amp;&amp; 1 !== $max_depth ) ? 'has-dropdown' : ’;

      // call parent method
      parent::display_element( $element, $children_elements, $max_depth, $depth, $args, $output );
   }
}
</code></pre>

As you can see, we've redefined the <code>start_lvl</code> and <code>display_element</code> methods. The first one generates the markup of the opening <code>ul</code> tag and assigns the <code>dropdown</code> CSS class.

The second method, <code>display_element</code>, is <a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/class-wp-walker.php#L112">described in the Trac</a>: It’s a method to “traverse elements to create a list from elements,” so it is a good place to make changes to the menu items.

Here we've accessed the <code>has_children</code>, <code>classes</code>, <code>current</code> and <code>current_item_ancestor</code> properties and passed the updated <code>$element object</code> to the parent <code>display_element</code> method. That's enough to achieve our goal, but we could do much more on the menu items. If you call <code>var_dump</code> on the <code>$element</code> object, you'll see all of the available properties at your disposal to build more advanced navigation menus.

And, as we'll see in a moment, we can add new properties to the object.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de8bc55c-7981-4153-9f81-dc283a9442b8/04-foundationmenu-opt.png" alt="The Foundation Top Bar on a WordPress website" /><figcaption>The Foundation Top Bar on a WordPress website.</figcaption></figure>

The menu is up and running, but we may want deeper customization. In the next example, we'll get more from our navigation menu, allowing the website administrator to prepend icons to the items’s titles the easy way: directly from the administration panel. In our example, we'll use <a href="https://zurb.com/playground/foundation-icon-fonts-3">Foundation Icon Fonts 3</a>.</p>

## Adding Fields To The WordPress Menu Items’ Editing Box

Before we start coding, let's open the menu editing page and make sure that all of the advanced menu properties in the “Screen Options” tab are checked.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3406fb38-b32d-4763-b811-fde680f4d963/05-screenoptions-opt-small.png" alt="Screen Options Tab" /><figcaption>WordPress’ “Screen Options” tab on the administration page for menus.</figcaption></figure>

Each checkbox enables or disables certain fields in the menu item’s editing box:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c0ba74e-bbd7-420e-a1b5-880864c75645/06-menueditbox-opt.png" alt="Menu item edit box" /><figcaption>The menu items’ editing box.</figcaption></figure>

But we can do more than add or change field values. The menu items are considered specific post types, and the values of the menu items’ fields are stored in the database as hidden custom fields. So we can add a new menu item’s field exactly as we do with regular posts’ custom fields.

Any kind of form field is allowed: inputs, checkboxes, textboxes and so on.

In the following example, I will show you how to add a simple text field that enables the website administrator to add a new property to the <code>$item</code> object. It will be stored as a custom field and will be used to show data in the website’s front end.

To do that, we will:

1.  register a custom field for the navigation menu item,
2.  save the new custom field’s value,
3.  set up a new `Walker` class for the edit menu tree.</p>

### Step 1: Register A Custom Field For The Nav Menu Item

First, we'll have to register a new custom field for the navigation menu item in the <code>functions.php</code> file:

<pre><code class="language-php">/**
 * Add a property to a menu item
 *
 * @param object $item The menu item object.
 */
function custom_nav_menu_item( $item ) {
   $item-&gt;icon = get_post_meta( $item-&gt;ID, '_menu_item_icon', true );
   return $item;
}
add_filter( 'wp_setup_nav_menu_item', 'custom_nav_menu_item' );
</code></pre>

<code>wp_setup_nav_menu_item</code> filters the navigation menu’s <code>$item</code> object, allowing us to add the <code>icon</code> property.</p>

### Step 2: Save The User’s Input

When the user submits the form from the menu’s administration page, the following callback will store the fields' values in the database:

<pre><code class="language-php">/**
 * Save menu item custom fields' values
 * 
 * @link https://codex.wordpress.org/Function_Reference/sanitize_html_class
 */
function custom_update_nav_menu_item( $menu_id, $menu_item_db_id, $menu_item_args ){
   if ( is_array( $_POST['menu-item-icon'] ) ) {
      $menu_item_args['menu-item-icon'] = $_POST['menu-item-icon'][$menu_item_db_id];
      update_post_meta( $menu_item_db_id, '_menu_item_icon', sanitize_html_class( $menu_item_args['menu-item-icon'] ) );
   }
}
add_action( 'wp_update_nav_menu_item', 'custom_update_nav_menu_item', 10, 3 );
</code></pre>

When updating the menu items, this action calls <code>custom_update_nav_menu_item()</code>, which will sanitize and update the value of the <code>_menu_item_icon</code> meta field.

Now we have to print the custom field's markup.</p>

### Step 3: Set Up A New Walker For The Edit Menu Tree

The structure of the menu’s administration page is built by the <code>Walker_Nav_Menu_Edit</code> class, which is an extension of <code>Walker_Nav_Menu</code>. To customize the menu items’ editing boxes, we'll need a new custom <code>Walker_Nav_Menu</code> child class based on the <code>Walker_Nav_Menu_Edit</code> class.

To set a custom <code>Walker</code>, this time we'll need the following filter:

<pre><code class="language-php">add_filter( 'wp_edit_nav_menu_walker', function( $class ){ return 'Custom_Walker_Nav_Menu_Edit'; } );</code></pre>

When fired, this filter executes an <a href="https://php.net/manual/en/functions.anonymous.php">anonymous function</a> that sets a custom class that will build the list of menu items.

Finally, the new <code>Walker</code> can be declared. We won't reproduce the full code here. Just copy and paste the full <code>Walker_Nav_Menu_Edit</code> code <a href="https://core.trac.wordpress.org/browser/tags/4.2.4/src/wp-admin/includes/nav-menu.php">from the Trac</a> into your custom class and add the custom field markup as shown below:

<pre><code class="language-php">class Custom_Walker_Nav_Menu_Edit extends Walker_Nav_Menu {
   public function start_lvl( &amp;$output, $depth = 0, $args = array() ) {}
   public function end_lvl( &amp;$output, $depth = 0, $args = array() ) {}
   public function start_el( &amp;$output, $item, $depth = 0, $args = array(), $id = 0 ) {
   ...

      &lt;p class="field-xfn description description-thin"&gt;
         &lt;label for="edit-menu-item-xfn-&lt;?php echo $item_id; ?&gt;"&gt;
            &lt;?php _e( 'Link Relationship (XFN)' ); ?&gt;&lt;br /&gt;
            &lt;input type="text" id="edit-menu-item-xfn-&lt;?php echo $item_id; ?&gt;" class="widefat code edit-menu-item-xfn" name="menu-item-xfn[&lt;?php echo $item_id; ?&gt;]" value="&lt;?php echo esc_attr( $item-&gt;xfn ); ?&gt;" /&gt;
         &lt;/label&gt;
      &lt;/p&gt;
      &lt;p class="field-custom description description-thin"&gt;
         &lt;label for="edit-menu-item-icon-&lt;?php echo $item_id; ?&gt;"&gt;
            &lt;?php _e( 'Foundation Icon' ); ?&gt;&lt;br /&gt;
            &lt;input type="text" id="edit-menu-item-icon-&lt;?php echo $item_id; ?&gt;" class="widefat code edit-menu-item-icon" name="menu-item-icon[&lt;?php echo $item_id; ?&gt;]" value="&lt;?php echo esc_attr( $item-&gt;icon ); ?&gt;" /&gt;
         &lt;/label&gt;
      &lt;/p&gt;
   ...
   }
}
</code></pre>

Now, with the new input field in place, the website administrator will be able to add the new icon property to the menu <code>$item</code> object.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52e001ac-9de8-4f40-90cc-00b23ac19679/07-menueditboxcustom-opt.png" alt="Custom menu item edit box" /><figcaption>A customized version of the menu items’ editing box.</figcaption></figure>

At this time, the <code>Walker_Nav_Menu</code> class won't be able to access the new property value; so, the value of <code>$item-&gt;icon</code> would not be available to build the menu structure. To make it accessible, in the <code>Custom_Foundation_Nav_Menu</code> class of our previous example, we will redefine the <code>start_el</code> method. The easiest way to proceed is to copy the code from <a href="https://core.trac.wordpress.org/browser/trunk/src/wp-includes/nav-menu-template.php">the <code>Walker_Nav_Menu</code> class</a> and paste it in our custom class, editing it where necessary.

So, paste the code and jump to the bottom of the new <code>start_el</code> method and make the following edits:

<pre><code class="language-php">public function start_el( &amp;$output, $item, $depth = 0, $args = array(), $id = 0 ) {

   ...

   $item_output = $args-&gt;before;
   $item_output .= '&lt;a'. $attributes .'&gt;';

   if( !empty( $item-&gt;icon ) )
      $item_output .= '&lt;i class="fi-' . $item-&gt;icon . '" style="margin-right: .4em"&gt;&lt;/i&gt;';

   $item_output .= $args-&gt;link_before . apply_filters( 'the_title', $item-&gt;title, $item-&gt;ID ) . $args-&gt;link_after;
   $item_output .= '&lt;/a&gt;';
   $item_output .= $args-&gt;after;

   $output .= apply_filters( 'walker_nav_menu_start_el', $item_output, $item, $depth, $args );
}
</code></pre>

No other changes are being done here except the condition that checks the value of the <code>$item-&gt;icon</code> property. If a value has been set, a new <code>i</code> element is attached to <code>$item_output</code> and assigned to the proper CSS class.

Finally, the following markup shows the new HTML menu structure.</p>

<pre><code class="language-markup">&lt;div class="top-bar-section"&gt;
   &lt;ul id="menu-nav-menu" class="left"&gt;
      &lt;li id="menu-item-46" class="menu-item menu-item-type-custom menu-item-object-custom current-menu-item current_page_item menu-item-home not-click active menu-item-46"&gt;
         &lt;a href="https://localhost:8888/wordpress/"&gt;
            &lt;i class="fi-social-smashing-mag"&gt;&lt;/i&gt;
            &lt;span&gt;Home&lt;/span&gt;
         &lt;/a&gt;
      &lt;/li&gt;
   &lt;/ul&gt;
&lt;/div&gt;
</code></pre>

The image below shows the final result on the desktop.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0baeae3d-7a91-43ed-b061-73b276db1021/08-icontopbardesktopzoomed-opt.png" alt="Foundation 5 Topbar in WordPress" /><figcaption>The custom Foundation 5 Top Bar integrated in a WordPress theme, enriched with icon fonts from Foundation Icon Font 3.</figcaption></figure>

## Final Notes

In this article, we've explored some of the most common uses of the <code>Walker</code> class. Note, however, that our examples do not cover all possible applications and alternative ways to take advantage of the class. But you'll discover more just by making use of your imagination and your skills as a programmer.

And never lose sight of the official documentation:

*   [Class Reference/`Walker`](https://codex.wordpress.org/Class_Reference/Walker)
*   [Function Reference/`wp_nav_menu`](https://codex.wordpress.org/Function_Reference/wp_nav_menu)

{{< signature "ml, dp, jb, al, jb" >}}


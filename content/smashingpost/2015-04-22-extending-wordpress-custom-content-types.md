---
title: Extending WordPress With Custom Content Types
slug: extending-wordpress-custom-content-types
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a1d16af-2d70-4b29-be0b-163d6f0f1406/wordpress-custom-post-type-menu-preview-opt.png
date: 2015-04-22T21:04:41.000Z
author: brianonorio
description: >-
  WordPress does some pretty amazing things out of the box. It handles content
  management as well as any other open-source solution out there — and better
  than many commercial solutions. One of the best attributes of WordPress is its
  ease of use. It’s easy because there’s not a significant amount of bloat with
  endless bells and whistles that steepen the learning curve.

  On the flip side, some might find WordPress a little… well, light. It does a
  lot, but not quite enough. If you find yourself hacking WordPress to do the
  things you wish it would do, then the chances are high that this article is
  for you. WordPress can be easily extended to fit the requirements of a custom
  data architecture. We’re going to explore the **process of registering new
  data types** in a fully compliant manner.
categories:
  - WordPress
  - Techniques (WP)
---
WordPress does some pretty amazing things out of the box. It handles content management as well as any other open-source solution out there — and better than many commercial solutions. One of the best attributes of WordPress is its ease of use. It’s easy because there’s not a significant amount of bloat with endless bells and whistles that steepen the learning curve.

On the flip side, some might find WordPress a little… well, light. It does a lot, but not quite enough. If you find yourself hacking WordPress to do the things you wish it would do, then the chances are high that this article is for you.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Detailed Guide To WordPress Custom Page Templates](https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/)
*   [Building A Custom Archive Page For WordPress](https://www.smashingmagazine.com/2015/04/building-custom-wordpress-archive-page/)
*   [<span class="headline">The Complete Guide To Custom Post Types</span>](https://www.smashingmagazine.com/2012/11/complete-guide-custom-post-types/)
*   [How To Create Custom Post Meta Boxes In WordPress](https://www.smashingmagazine.com/2011/10/create-custom-post-meta-boxes-wordpress/)

WordPress can be easily extended to fit the requirements of a custom data architecture. We’re going to explore the process of registering new data types in a fully compliant manner.

{{% feature-panel %}}

If you want to follow along at home, we’ve provided the <a href="https://smashingmagazine.com/provide/full-source-code.txt">full source code</a> (TXT, 5.0 KB).</p>

## Custom Post Types

WordPress gives you a very simple and straightforward way to extend the standard two data types (Posts and Pages) into an endless array for your custom needs. A digital agency or freelancer would need a “Project” post type. A mall would need a “Location” post type.

Quick point. Spinning off custom post types is a great idea for content that is intrinsically different than either Posts or Pages. There could be a case where you would want press releases to live in their own type. But more often than not, the press releases would be a Post and categorized as a press release. Or you may want to create a post type for landing pages. It may very well belong as a custom type, but it likely could also exist as a Page.

For the sake of this article, we’re going to follow a real-world scenario of creating a Project post type to store samples of work. We’ll register the post type, add some meta data to it, include additional information in WordPress’ administration screens, and create custom taxonomies to supplement.</p>

## Registering The Post Type

To get started, we’ll need some code to register the post type. We’re going to go with an object-oriented approach because we’ll be spinning off this post type later with some added functionality that would be done much more efficiently with an object model. To start, let’s create the function that registers the post type.</p>

<pre><code class="language-php">
function create_post_type() {
  $labels = array(
    'name'               =&gt; 'Projects',
    'singular_name'      =&gt; 'Project',
    'menu_name'          =&gt; 'Projects',
    'name_admin_bar'     =&gt; 'Project',
    'add_new'            =&gt; 'Add New',
    'add_new_item'       =&gt; 'Add New Project',
    'new_item'           =&gt; 'New Project',
    'edit_item'          =&gt; 'Edit Project',
    'view_item'          =&gt; 'View Project',
    'all_items'          =&gt; 'All Projects',
    'search_items'       =&gt; 'Search Projects',
    'parent_item_colon'  =&gt; 'Parent Project',
    'not_found'          =&gt; 'No Projects Found',
    'not_found_in_trash' =&gt; 'No Projects Found in Trash'
  );

  $args = array(
    'labels'              =&gt; $labels,
    'public'              =&gt; true,
    'exclude_from_search' =&gt; false,
    'publicly_queryable'  =&gt; true,
    'show_ui'             =&gt; true,
    'show_in_nav_menus'   =&gt; true,
    'show_in_menu'        =&gt; true,
    'show_in_admin_bar'   =&gt; true,
    'menu_position'       =&gt; 5,
    'menu_icon'           =&gt; 'dashicons-admin-appearance',
    'capability_type'     =&gt; 'post',
    'hierarchical'        =&gt; false,
    'supports'            =&gt; array( 'title', 'editor', 'author', 'thumbnail', 'excerpt', 'comments' ),
    'has_archive'         =&gt; true,
    'rewrite'             =&gt; array( 'slug' =&gt; 'projects' ),
    'query_var'           =&gt; true
  );

  register_post_type( 'sm_project', $args );
}
</code></pre>

Not much mysterious here. We’re calling the <code>create_post_type</code> function, which registers our post type. We’re giving the type some labels for back-end identification and giving it a list of specifications in what it can do. For a full list of reference for each of these variables, take a <a title="Register Post Type on the WordPress Codex" href="https://codex.wordpress.org/Function_Reference/register_post_type">look at the WordPress Codex</a>, but we’ll hit on a few key items.</p>

### labels

For brevity, we’ve created a <code>labels</code> array and simply passed it to the <code>arguments</code> array. WordPress enables us to identify a slew of labels for singular, plural and other purposes.</p>

### public

This setting is a parent of sorts for a few of the other settings that appear later in the list. The default value for the public attribute is <code>false</code>. The value of <code>public</code> is passed to the following other attributes when they are not explicitly defined: <code>exclude_from_search</code>, <code>publicly_queryable</code>, <code>show_in_nav_menus</code> and <code>show_ui</code>.</p>

### exclude_from_search

The default setting here is the <em>opposite</em> of the <code>public</code> attribute. If your post type is <code>public</code>, then it will be included in the website’s search results. Note that this has no implication for SEO and only restricts or allows searches based on WordPress’ native search protocol. There’s a chance you would want the post type to be public but not appear in these search results. If that’s the case, set this attribute to <code>true</code>.</p>

### publicly_queryable

This attribute is exclusively for front-end queries and has no real back-end implications. The default value is the same as the <code>public</code> attribute. Note that when it’s set to <code>false</code>, you will not be able to view or preview the post type in the front end. For example, if you wanted to create a post type that populates a personnel page with a list of everyone’s name, title and bio but didn’t want them to have their own URL on the website, then you would set <code>publicly_queryable</code> to <code>false</code>.</p>

### show_ui

Most of the time, you’ll want to set <code>show_ui</code> to <code>true</code>. The default value pulls from the <code>public</code> attribute but can be overridden. When it’s set to <code>false</code>, then a UI element on WordPress’ administration screen won’t be available to you. A practical reason why you would want this set to <code>false</code> is if you had a post type that merely managed data. For example, you may want an Events post type that has a recurring attribute. When you save an event, new posts of a different type would be created to handle each event occurrence. You would want the UI to show only the primary Events post type and not the event occurrence’s meta data.</p>

### show_in_nav_menus

Pretty simple and straightforward. If you don’t want this post type to appear in WordPress’ default menu functionality, set this to <code>false</code>. It takes the value of <code>public</code> as default.</p>

### show_in_menu

You can modify the position of the post type in the back end. When set to <code>true</code>, the post type defaults as a top-level menu (on the same hierarchical level as Posts and Pages). If <code>false</code>, it won’t show at all. You can use a string value here to explicitly nest the post type into a top level’s submenu. The type of string you would provide is <code>tools.php</code>, which would place the post type as a nested element under “Tools.” It derives its default value from <code>show_ui</code>. Note that <code>show_ui</code> must be set to <code>true</code> in order for you to be able to control this attribute.</p>

### show_in_admin_bar

Pretty self-explanatory. If you want UI elements added to WordPress’ administration bar, set this to <code>true</code>.</p>

### menu_position

The default value of <code>null</code> will place the menu (at the top level and if not overridden using <code>show_in_menu</code>) below “Comments” in the back end. You can control this further by specifying an integer value corresponding to WordPress’ default menu placements. A value of <code>5</code> will place the post type under “Posts,” <code>10</code> under “Media,” <code>15</code> under “Links,” and 20 under “Pages.” For a full list of values, <a title="register_post_type on the WordPress Codex" href="https://codex.wordpress.org/Function_Reference/register_post_type">check out the WordPress Codex</a>.</p>

### menu_icon

You can pass a URL to this attribute, but you could also simply use the name of an icon from Dashicons for a quick solution. Supplying the attribute <code>dashicons-admin-appearance</code> would give you a <a title="WordPress Paint Brush Icon" href="https://developer.wordpress.org/resource/dashicons/#admin-appearance">paint brush</a>. A <a title="WordPress Dashicons" href="https://developer.wordpress.org/resource/dashicons/">full list of Dashicons is available</a> as a handy resource. The default is the thumbtack icon used for Posts.</p>

### capability_type

This attribute quickly gets into some advanced user-role segmenting concepts. Essentially, assigning <code>post</code> to this attribute generates a capability structure that exactly mimics how access to Posts works. Using this value, subscribers would not be able to access this post type, whereas Authors, Editors and Administrators would. Using <code>page</code> here would limit access to just Editors and Administrators. You can define a more granular structure using <code>capability_type</code> and <code>capabilities</code> attributes in the arguments list. Note that we did not use the <code>capabilities</code> attribute in this example because we’re not explicitly defining a custom capability structure to be used with this post type. This is an advanced concept and one for a completely different article.</p>

### hierarchical

This is basically the difference between a Post and a Page. When set to <code>true</code>, a parent post can be identified on a per-post basis (basically, Pages). When <code>false</code>, it behaves as a Post.</p>

### supports

A whole bunch of default functionality is attached to each new post type. This array tells WordPress which one of those to include by default. There may be an instance when you don’t want the editor on your post type. Removing that from the array will remove the editor box on the post’s editing screen. Eligible items for the array include the following:

*   `title`
*   `editor`
*   `author`
*   `thumbnail`
*   `excerpt`
*   `trackbacks`
*   `custom-fields`
*   `comments`
*   `revisions`
*   `page-attributes`
*   `post-formats`

### has_archive

When this is set to <code>true</code>, WordPress creates a hierarchical structure for the post type. So, accessing <code>/projects/</code> would give us the standard <code>archive.php</code> view of the data. You can template out a variant of <code>archive.php</code> for this particular archive by creating a new file in your theme system named <code>archive-sm_project.php</code>. You can control the default behavior at a more granular level by spinning it off from your primary <code>archive.php</code>.</p>

### rewrite

The <code>rewrite</code> option allows you to form a URL structure for the post type. In this instance, our URL would be <code>https://www.example.com/projects/{slug}/</code>, where the slug is the portion assigned by each post when it’s created (normally, based on the title of the post). A second variable can be assigned inside the <code>rewrite</code> array. If you add <code>with_front =&gt; false</code> (it defaults to <code>true</code>), it will not use the identified front half of the URL, which is set in “Settings” → “Permalinks.” For example, if your default WordPress permalink structure is <code>/blog/%postname%/</code>, then your custom post type would automatically be <code>/blog/projects/%postname%/</code>. That’s not a good outcome, so set <code>with_front</code> to <code>false</code>.</p>

### query_var

This attribute controls where you can use a PHP query variable to retrieve the post type. The default is <code>true</code> and renders with the permalink structure (when set). You can use a string instead of a variable and control the key portion of the query variable with the string’s value.</p>

## Extending The Post Type With A Taxonomy (Or Two)

Out of the box, WordPress Posts have categories and tags attached to them that enable you to appropriately place content in these buckets. By default, new post types don’t have any taxonomies attached to them. You may not want to categorize or tag your post type, but if you do, you’d need to register some new ones. There are two variants of taxonomies, one that behaves like categories (the checklist to the right of the posts) and one like tags, which have no hierarchical structure. They behave in the back end pretty much in the same way (the only discernable difference being that categories can have children, whereas tags cannot), but how they’re presented on the administration screen varies quite wildly. We’ll register two taxonomies to give us one of each type.</p>

<pre><code class="language-php">
function create_taxonomies() {

  // Add a taxonomy like categories
  $labels = array(
    'name'              =&gt; 'Types',
    'singular_name'     =&gt; 'Type',
    'search_items'      =&gt; 'Search Types',
    'all_items'         =&gt; 'All Types',
    'parent_item'       =&gt; 'Parent Type',
    'parent_item_colon' =&gt; 'Parent Type:',
    'edit_item'         =&gt; 'Edit Type',
    'update_item'       =&gt; 'Update Type',
    'add_new_item'      =&gt; 'Add New Type',
    'new_item_name'     =&gt; 'New Type Name',
    'menu_name'         =&gt; 'Types',
  );

  $args = array(
    'hierarchical'      =&gt; true,
    'labels'            =&gt; $labels,
    'show_ui'           =&gt; true,
    'show_admin_column' =&gt; true,
    'query_var'         =&gt; true,
    'rewrite'           =&gt; array( 'slug' =&gt; 'type' ),
  );

  register_taxonomy('sm_project_type',array('sm_project'),$args);

  // Add a taxonomy like tags
  $labels = array(
    'name'                       =&gt; 'Attributes',
    'singular_name'              =&gt; 'Attribute',
    'search_items'               =&gt; 'Attributes',
    'popular_items'              =&gt; 'Popular Attributes',
    'all_items'                  =&gt; 'All Attributes',
    'parent_item'                =&gt; null,
    'parent_item_colon'          =&gt; null,
    'edit_item'                  =&gt; 'Edit Attribute',
    'update_item'                =&gt; 'Update Attribute',
    'add_new_item'               =&gt; 'Add New Attribute',
    'new_item_name'              =&gt; 'New Attribute Name',
    'separate_items_with_commas' =&gt; 'Separate Attributes with commas',
    'add_or_remove_items'        =&gt; 'Add or remove Attributes',
    'choose_from_most_used'      =&gt; 'Choose from most used Attributes',
    'not_found'                  =&gt; 'No Attributes found',
    'menu_name'                  =&gt; 'Attributes',
  );

  $args = array(
    'hierarchical'          =&gt; false,
    'labels'                =&gt; $labels,
    'show_ui'               =&gt; true,
    'show_admin_column'     =&gt; true,
    'update_count_callback' =&gt; '_update_post_term_count',
    'query_var'             =&gt; true,
    'rewrite'               =&gt; array( 'slug' =&gt; 'attribute' ),
  );

  register_taxonomy('sm_project_attribute','sm_project',$args);
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c88b6bfc-073b-41fa-a8e3-c722399a80a4/wordpress-custom-post-type-menu-large-preview-opt.png"><img loading="lazy" decoding="async" title="The WordPress Custom Post Type Menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a1d16af-2d70-4b29-be0b-163d6f0f1406/wordpress-custom-post-type-menu-preview-opt.png" alt="When registering a post type, a new menu will appear in the dashboard." /></a><figcaption>After you register the new post type and taxonomies, you’ll be greeted with a handy menu in the back end. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c88b6bfc-073b-41fa-a8e3-c722399a80a4/wordpress-custom-post-type-menu-large-preview-opt.png">View large version</a>)</figcaption></figure>

All right, now we have two new taxonomies attached to the new post type. The <code>register_taxonomy</code> function takes three arguments. The first is the taxonomy’s name, the second is an array or string of post types, and the third is the arguments defined above.

A quick note on our prefixing. Our post type and taxonomies are all prefixed with <code>sm_</code>. This is by design. We don’t want future plugins to interrupt our infrastructure, so we simply prefix. The name of the prefix is completely up to you.

So, we’ve got a new post type and two new taxonomies attached to it. This essentially replicates the default Posts behavior of WordPress. This is all good stuff, but let’s dig a little deeper to make it more integrated.</p>

## Enhancing The Experience With Meta Data

Creating additional fields available to the author in WordPress’ administration screen can be a bit tricky — but abundantly useful. Where WordPress underperforms its competitors is precisely in this area. There’s no user interface where you can define additional pieces of information on a per-post basis. Make no mistake, WordPress fully <em>supports</em> this behavior, but it’s more of a developer tool than an out-of-the-box tool, which makes sense. One might need an endless number of combinations of additional fields. Even if WordPress provided a slick back-end interface to allow a non-technical user to define these fields, there’s no real seamless way to display that information in the front end without a developer putting their hands on it and making it so.

This is where <a title="Advanced Custom Fields" href="https://www.advancedcustomfields.com/">Advanced Custom Fields</a> comes in. ACF is a wonderful plugin that gives developers this interface and a full array of templating functions to pull the data in the front end. This article doesn’t detail how to do that, but ACF gives ample <a title="ACF Documentation" href="https://www.advancedcustomfields.com/resources/">documentation</a> to get you started and working in the ACF environment.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65d2556b-cff2-4ada-b22a-aa007fac9878/acf-ui-large-preview-opt.png"><img loading="lazy" decoding="async" title="The ACF UI" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e0a4911-0e99-4c4a-9c79-844fa9838c00/acf-ui-preview-opt.png" alt="A preview of the ACF UI for creating custom metadata." /></a><figcaption>ACF makes creating meta data and conditionally attaching to custom post types a snap. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65d2556b-cff2-4ada-b22a-aa007fac9878/acf-ui-large-preview-opt.png">View large version</a>)</figcaption></figure>

Using ACF, you can define new fields and conditionally attach them to content throughout the website. For example, we could create a timeframe meta field that collects how long a particular project has taken. We could add additional fields for awards won or create fields to represent a list of references for any given project.

Using ACF really opens up the hood for what’s possible in WordPress.</p>

## Adding Columns To The Administration Screen

Viewing a list of your posts on the administration screen will give you the checkbox, the title and the date published. When registering taxonomies to the post type, you’ll get an additional column for each additional taxonomy. For the majority of cases, this is sufficient. But there may be an additional case or two where you need to provide a little more information. For example, referencing pieces of meta data in the administration grid might be useful. Maybe you want a quick reference for the timeframe or the awards field we defined above. We’ll need two functions attached to some WordPress hooks.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f6ae62e-9800-4c75-83d7-840e2168f437/custom-post-type-administration-screen-before-large-preview-opt.png"><img loading="lazy" decoding="async" title="The WordPress Custom Post Type Administration Screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/755a67db-5fd6-4a61-8c02-c7df1f648389/custom-post-type-administration-screen-before-preview-opt.png" alt="WordPress will give you a standard UI that will closely mirror the Post UI." /></a><figcaption>WordPress gives you a standard administration screen out of the box that closely mirrors the built-in Post post type. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f6ae62e-9800-4c75-83d7-840e2168f437/custom-post-type-administration-screen-before-large-preview-opt.png">View large version</a>)</figcaption></figure>

Let’s look at the code:

<pre><code class="language-php">
function columns($columns) {
  unset($columns['date']);
  unset($columns['taxonomy-sm_project_attribute']);
  unset($columns['comments']);
  unset($columns['author']);
  return array_merge(
    $columns,
    array(
      'sm_awards' =&gt; 'Awards',
      'sm_timeframe' =&gt; 'Timeframe'
    ));
}
</code></pre>

The first line unsets the date column. You can unset any of the default columns that you wish. The second line unsets the custom taxonomy we registered (the tag-like one, not category). This could be useful for keeping the admin screen neat and tidy. As you may have noticed, we also unset the comments and author — information we didn’t think was necessary on the screen.

Then, we’re simply defining the new columns and merging them with the array that was passed in the function. We created two new columns, one for <code>awards</code> and one for <code>timeline</code>. The array keys are completely arbitrary. They could be anything, but we’ll need to reference them again when it comes time to pull data into those columns… which is what we’re going to do next.</p>

<pre><code class="language-php">
function column_data($column,$post_id) {
  switch($column) {
  case 'sm_awards' :
    echo get_post_meta($post_id,'awards',1);
    break;
  case 'sm_timeframe' :
    echo get_post_meta($post_id,'timeframe',1);
    break;
}
</code></pre>

All right, we’ve fetched the meta data and conditionally outputted it based on what column we’re on. This is where we’re referencing the array key from above. So, as long as they’re both the same, we could use any arbitrary string we want. Note that we’re pulling the meta fields over using WordPress’ native <code>get_post_meta</code> function.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/096b56de-50d7-4c46-9408-091940e4eedf/custom-post-type-administration-screen-after-large-preview-opt.png"><img loading="lazy" decoding="async" title="The WordPress Custom Post Type Administration Screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f567ac5a-99aa-4141-adbd-156df4316a31/custom-post-type-administration-screen-after-preview-opt.png" alt="Removing a few built-in columns and adding some of our own enhances the UI." /></a><figcaption>Removing some built-in columns and adding a few of our own enhances the UI and streamlines the information displayed. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/096b56de-50d7-4c46-9408-091940e4eedf/custom-post-type-administration-screen-after-large-preview-opt.png">View large version</a>)</figcaption></figure>

## Sorting

Ah, sorting. As you probably know, WordPress sorts Pages by menu order and then alphabetically by title and Posts by date published. Let’s get fancy and sort our new post type by the number of awards won. The use case here is easy to see. You want your most award-winning work at the top of the list at all times. If we use standard WordPress queries, the order we’re about to establish will be honored – universally across the website. We will need a function to join the <code>wp_posts</code> and <code>wp_postmeta</code> tables and another to revise how the data is sorted.</p>

<pre><code class="language-php">
function join($wp_join) {
  global $wpdb;
  if(get_query_var('post_type') == 'sm_project') {
    $wp_join .= " LEFT JOIN (
      SELECT post_id, meta_value as awards
      FROM $wpdb-&gt;postmeta
      WHERE meta_key =  'awards' ) AS meta
      ON $wpdb-&gt;posts.ID = meta.post_id ";
  }
  return ($wp_join);
}
</code></pre>

This function does the joining for us. We won’t get into why that <code>select</code> statement works (that’s for another article altogether). Pay attention to the <code>if</code> statement here. We’re determining the post type and then conditionally running the <code>join</code> if it meets the <code>sm_project</code> condition. Absent this <code>if</code> statement, you would be doing this <code>join</code> regardless of type, which is not likely something you want.

There could also be a case where you just want to sort the administration screens and not the front end. Fortunately, we can use WordPress’ built-in conditional statements to do that job. Just wrap your statement with another conditional and check against <code>is_admin</code>.</p>

<pre><code class="language-php">
function set_default_sort($orderby,&amp;$query) {
  global $wpdb;
  if(get_query_var('post_type') == 'sm_project') {
    return "meta.awards DESC";
  }
  return $orderby;
}
</code></pre>

Once again, we’re verifying our post type and then returning an amended <code>order</code> statement. Now we’re telling WordPress to order by the value from the <code>wp_postmeta</code> table descending. So, we’ll get a list of our awards from the most won per project to the least won per project.</p>

## Putting It All Together

None of these functions will do anything until they’re called and attached to WordPress hooks. We’ll do this and keep it neat by creating an object around the post type and using the constructor to attach each function to the appropriate hook. For brevity, we’re not going to repeat the code already referenced above.</p>

<pre><code class="language-php">
class sm_project {

  function __construct() {
    add_action('init',array($this,'create_post_type'));
    add_action('init',array($this,'create_taxonomies'));
    add_action('manage_sm_project_posts_columns',array($this,'columns'),10,2);
    add_action('manage_sm_project_posts_custom_column',array($this,'column_data'),11,2);
    add_filter('posts_join',array($this,'join'),10,1);
    add_filter('posts_orderby',array($this,'set_default_sort'),20,2);
  }

  function create_post_type() {
    …
  }

  function create_taxonomies() {
    …
  }

  function columns($columns) {
    …
  }

  function column_data($column,$post_id) {
    …
  }

  function join($wp_join) {
    …
  }

  function set_default_sort($orderby,&amp;$query) {
    …
  }
}

new sm_project();
</code></pre>

Voila! Everything has come together quite nicely. In our constructor, we referenced the appropriate actions and filters. We’re performing these functions in a particular order — and this must be followed. The post type has to be created first, the taxonomies attached second, then any sort of custom sorting. Keep that in mind as you’re creating your data type.</p>

## Summing Up

Once you get the hang of it and you create a few of these, it’ll start to come naturally. I’ve got a bunch of these clips saved up in my toolbelt. I rarely create these from scratch anymore. Although this article is long and in-depth, it really is about a 10-minute process from concept to conclusion once you fully understand what’s going on.</p>

### References

*   “[register_post_type](https://codex.wordpress.org/Function_Reference/register_post_type "WordPress Codex: register_post_type"),” WordPress Codex
*   “[register_taxonomy](https://codex.wordpress.org/Function_Reference/register_taxonomy "WordPress Codex: register_taxonomy"),” WordPress Codex
*   “[Metadata API](https://codex.wordpress.org/Metadata_API "WordPress Codex: Metadata API"),” WordPress Codex
*   “[get_post_meta](https://codex.wordpress.org/Function_Reference/get_post_meta "WordPress Codex: get_post_meta"),” WordPress Codex
*   “[get_fields](https://www.advancedcustomfields.com/resources/get_fields/ "ACF: get_fields"),” ACF Documentation
*   “[Template Hierarchy](https://codex.wordpress.org/Template_Hierarchy "WordPress Codex: Template Hierarchy"),” WordPress Codex
*   “[Action Reference](https://codex.wordpress.org/Plugin_API/Action_Reference "WordPress Codex: Action Reference"),” WordPress Codex
*   “[Filter Reference](https://codex.wordpress.org/Plugin_API/Filter_Reference "WordPress Codex: Filter Reference"),” WordPress Codex

{{< signature "dp, al" >}}


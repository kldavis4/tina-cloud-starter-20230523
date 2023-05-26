---
title: Customizing Admin Columns In WordPress
slug: customizing-admin-columns-wordpress
author: david-mosterd-jesper-van-engelen
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f83844c-a317-4401-bf56-36f2d3a675a4/2-result-final-large-opt.png
date: 2017-12-01T17:46:00+01:00
summary: >-
  How do you get insight into all of your content at a glance? WordPress’ admin
  area does not show you much about your pages, posts, users and comments. We
  will demonstrate some simple custom solutions and a ready-to-deploy plugin to
  overcome this problem.
description: >-
  How do you get insight into all of your content at a glance? WordPress’ admin
  area does not show you much about your pages, posts, users and comments. We
  will demonstrate some simple custom solutions and a ready-to-deploy plugin to
  overcome this problem.
categories:
  - WordPress
  - Plugins
---
<p>(<em>This is a sponsored article.</em>) If you manage a WordPress website, you've probably faced a common problem. How do you get insight into all of your content at a glance? WordPress' admin area does not show you much about your pages, posts, users and comments. That can make it hard to find the right page, to check if all associated fields are properly filled, or simply to get a general sense of your website's content. Does this sound familiar to you? Read on because we will demonstrate some simple custom solutions and a ready-to-deploy plugin to overcome this problem.</p>

<p>A modern WordPress website usually consists of much richer content than simply titles and chunks of text. Plugins such as Advanced Custom Fields and WooCommerce introduce custom fields that store specific pieces of content, such as prices, additional images, subtitles and so forth. Those functions on their own are great, but <strong>how do you keep track of all of that content</strong> when you can still only see the title, date and author in your admin screens? The answer is, you can't.</p>

<p>In this tutorial, we'll tackle this problem by showing you some easy-to-implement custom code. For those of you who don't want to code, we'll show you how to configure the Admin Columns plugin to do the job for you.</p>

<p>Also, you will learn how to:</p>

<ul>
<li>add new columns to the posts overview,</li>
<li>sort your posts by these columns,</li>
<li>create a filtering form to find your content,</li>
<li>use Admin Columns to edit your content inline (without having to navigate to the individual post).</li>
</ul>

{{% feature-panel %}}

## A Motivating Use Case

<p>Imagine that you're tasked with building or managing a website containing a real-estate agency's portfolio. On the website, you display pictures, house addresses, locations, number of rooms and other attributes. On the admin screen, you manage the portfolio, adding, removing and editing existing real estate. The columns WordPress shows by default (title, author, publication date, number of comments) are hardly relevant for your real-estate website, and you'd be more interested in seeing the existing pictures and information about the real-estate listings as a whole.</p>

<p>Let's look at a standard admin overview screen for custom post types:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b1824c3-4898-4a36-a9a5-9badf7d4b08a/1-default-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8393f075-cfd9-4d3f-8153-19f2105ebc69/1-default-800w-opt.png" width="800" height="444" alt="admin overview screen for custom post types" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b1824c3-4898-4a36-a9a5-9badf7d4b08a/1-default-large-opt.png">View large version</a>)</figcaption></figure>

This would be pretty useful if this were our website's blog posts or news items, right? But for our real-estate portfolio, this gives us no information at all. The same goes for web shops, car dealerships, creative portfolios and so forth. Luckily, there's a solution. We'll work towards a far more pleasing overview of our real-estate portfolio, which will look like this:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c29d1c48-b75b-4289-beae-746eefc6f324/2-result-final-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/010c3e74-dd78-447b-8ee7-5e9a9a9b18a4/2-result-final-800w-opt.png" width="800" height="444" alt="overview real-estate portfolio" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c29d1c48-b75b-4289-beae-746eefc6f324/2-result-final-large-opt.png">View large version</a>)</figcaption></figure>

As you can see, this gives us a lot of insight into our real-estate portfolio. It's now much easier to find, validate and, as you'll see, edit the content.</p>

<p>We'll provide a step-by-step guide to adding custom columns to your WordPress admin screens, sorting them and adding custom filters. We'll also show you how to do this with the Admin Columns plugin. (If you don't want to code, you can just <a href="#managing-columns">skip to that part</a> right away.)</p>

## Managing Columns With Code

<p class="c-cheshire-cat">First up is the management of columns for admin screens: adding columns that are specific to your content type, removing columns that are obsolete, and reordering columns. For this goal, WordPress offers the Columns API. It's available for users and taxonomies as well, but we'll focus on the posts screen.</p>

<p>Changing the existing columns can be accomplished using two WordPress hooks: <code>manage_[post_type]_posts_columns</code>, which allows you to remove, reorder and add columns, and <code>manage_[post_type]_posts_custom_column</code>. In place of <code>[post_type]</code>, enter the post type you wish to target. For pages, for example, you would use <code>manage_page_posts_columns</code> and <code>manage_page_posts_custom_column</code>, respectively.</p>

<p>If you haven't heard about WordPress hooks, we encourage you to move on to the "Managing Columns With the Admin Columns Plugin" section. It explains how you can manage your columns without touching any code. But if you feel like learning, then <a href="https://www.smashingmagazine.com/2016/01/get-started-with-hooks-wordpress/">read more about WordPress hooks (filters and actions)</a>.</p>

### "Where Do I Place My Code?"

<div class="c-cheshire-cat c-cheshire-cat--fat">
  <p>To add all of this custom functionality, we need a place to run our code. This is best done in a plugin. In this tutorial, for example, we're creating a custom plugin to run all of this code in. If you don't know how to create a plugin, you can <a href="https://www.smashingmagazine.com/2011/09/how-to-create-a-wordpress-plugin/">learn how</a>.</p>

  <p>All of the code snippets we'll provide will go in our custom plugin. It is advisable to place such code in a plugin, not in your theme.</p>
</div>

### Adding, Removing and Reordering Columns

<p>The first hook for managing columns (<code>manage_posts_columns</code>) is a filter that handles the array of columns. The standard array of filters for the posts overview is this:</p>

<pre><code class="language-php">
[
  [cb]          =&gt; &lt;input type="checkbox" /&gt;
  [title]       =&gt; Title
  [author]      =&gt; Author
  [categories]  =&gt; Categories
  [tags]        =&gt; Tags
  [comments]    =&gt; [..] Comments [..]
  [date]        =&gt; Date
]
</code></pre>

<p>We're going to remove a few columns from this list and add a few. To do so, we'll add a callback to the <code>manage_posts_columns</code> filter and append our custom columns to the columns array. Note that we're using the <code>manage_realestate_posts_columns</code> hook. Here, <code>realestate</code> is the name of our post type, passed as the first argument to the <code>register_post_type</code> function for registering custom post types. We use it in place of <code>[post_type]</code> in the <code>manage_[post_type]_posts_columns</code> filter.</p>

<div class="break-out">

<pre><code class="language-php">
add_filter( 'manage_realestate_posts_columns', 'smashing_filter_posts_columns' );
function smashing_filter_posts_columns( $columns ) {
  $columns['image'] = __( 'Image' );
  $columns['price'] = __( 'Price', 'smashing' );
  $columns['area'] = __( 'Area', 'smashing' );
  return $columns;
}
</code></pre></div>

<p>The first line adds our function <code>smashing_filter_posts_columns</code> as a callback to the filter that handles the columns that are displayed. The second line defines the callback function. Lines 2 to 4 add our custom columns to the list of columns. Finally, line 6 returns the resulting columns list.</p>

<p><strong>Note</strong>: The <code>smashing_</code> part before our functions is just a best practice to make sure that our function name is unique in WordPress. The <code>__</code> function is used for <a href="https://codex.wordpress.org/I18n_for_WordPress_Developers">translating the string</a> to the user's preferred language. Notice that for both "Price" and "Area," we use <code>smashing</code> as the text domain, which WordPress uses to determine what source should be used to translate the string. We can omit this for translating "Image" because WordPress already includes translations of this word itself. You can read <a href="https://codex.wordpress.org/I18n_for_WordPress_Developers#Text_Domains">more about text domains</a> in the WordPress Codex.</p>

<p>We've added columns to display an image, the price and the area, and the array with the new columns has been returned. The resulting real-estate list looks like this:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42fe09ba-77e5-4aec-8eb3-fb070515d138/3-step1a-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87256894-c678-4dec-9a0d-1cb130b5891a/3-step1a-800w-opt.png" width="800" height="338" alt="resulting real-estate list" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42fe09ba-77e5-4aec-8eb3-fb070515d138/3-step1a-large-opt.png">View large version</a>)

</figcaption></figure>

We still have to do two things:</p>

<ul>

<li>Remove the "Author," "Date" and "Comments" columns, which are irrelevant to our real-estate content.</li>

<li>Reorder the columns so that "Image" is first.</li>

</ul>

<p>We'll modify our function to accomplish this. Note that we do not explicitly remove the three columns mentioned above, but simply construct an entire new array of columns precisely as we need them. The modified lines are highlighted.</p>

<div class="break-out">

<pre>
  <code class="language-php">
add_filter( 'manage_realestate_posts_columns', 'smashing_realestate_columns' );
function smashing_realestate_columns( $columns ) {
  </code>
  <code class="language-php" style="background-color: #fffbd7">
    $columns = array(
      'cb' =&gt; $columns['cb'],
      'image' =&gt; __( 'Image' ),
      'title' =&gt; __( 'Title' ),
      'price' =&gt; __( 'Price', 'smashing' ),
      'area' =&gt; __( 'Area', 'smashing' ),
    );
  </code>
  <code class="language-php">
  return $columns;
}
  </code>
</pre></div>

<p>Our new real-estate overview screen is starting to take shape: Irrelevant columns have been removed, and new ones have been added in the right positions.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eedaeae6-62e4-4448-8334-e21870dfcf34/4-step1b-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f311ae0-35a6-4738-b61e-51f07b955899/4-step1b-800w-opt.png" width="800" height="339" alt="real-estate overview screen" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eedaeae6-62e4-4448-8334-e21870dfcf34/4-step1b-large-opt.png">View large version</a>)</figcaption></figure>

### Populating Columns

<p>Next up is populating our columns. Again, WordPress provides a pretty simple hook to do so: the <code>manage_[post_type]_posts_custom_column</code> action. Unlike the previously discussed hook, this is <strong>not a filter</strong>, so it only allows us to <strong>add</strong> content, not to <strong>change</strong> it. Thus, in the callback for this action, we're simply going to <code>echo</code> the column content that we want to display.</p>

<p>Let's start by adding the "Image" column.</p>

<div class="break-out">

<pre>
  <code class="language-php">
add_action( 'manage_realestate_posts_custom_column', 'smashing_realestate_column', 10, 2);
function smashing_realestate_column( $column, $post_id ) {
  // Image column
  if ( 'image' === $column ) {
    echo get_the_post_thumbnail( $post_id, array(80, 80) );
  }
}
  </code>
</pre></div>

<p>We added a callback function, <code>smashing_realestate_column</code>, to the action <code>'manage_realestate_posts_custom_column'</code>, taking two parameters: the column name and the post ID. This is indicated by the fourth parameter, <code>add_action</code>: It specifies the number of arguments expected by the callback function. The third parameter, called the priority of the hook, determines in what order the callback functions registered to the hook should be executed. We'll leave it at the default, which is 10. This callback function populates a single post's "Image" column.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7db456d8-44fe-419b-8c47-9bfe76cd3a7c/5-step2a-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28377fd3-a224-4fbb-a2c8-6bf53bd631dc/5-step2a-800w-opt.png" width="800" height="339" alt="image column" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7db456d8-44fe-419b-8c47-9bfe76cd3a7c/5-step2a-large-opt.png">View large version</a>)</figcaption></figure>

The remaining two columns, "Price" and "Area," are stored as custom fields with the keys <code>price_per_month</code> and <code>area</code>, respectively. We'll display these in the same way as we did with the image, displaying "n/a" when a price or surface area value is not available. The implementation is very similar for both columns. Starting with the price column, the changed lines in our <code>smashing_realestate_column</code> function are highlighted in the code block below.</p>

<div class="break-out">

<pre>
  <code class="language-php">
add_action( 'manage_realestate_posts_custom_column', 'smashing_realestate_column', 10, 2);
function smashing_realestate_column( $column, $post_id ) {
  // Image column
  if ( $column == 'image' ) {
    echo get_the_post_thumbnail( $post_id, array( 80, 80 ) );
  }

  </code>
  <code class="language-php" style="background-color: #fffbd7">
  // Monthly price column
  if ( 'price' === $column ) {
    $price = get_post_meta( $post_id, 'price_per_month', true );

    if ( ! $price ) {
      _e( 'n/a' );  
    } else {
      echo '$ ' . number_format( $price, 0, '.', ',' ) . ' p/m';
    }
  }
  </code>
  <code class="language-php">
}
  </code>
</pre></div>

<p>Next up is the <code>area</code> column. Except for the unit (square meters, m<sup>2</sup>, instead of dollars), the code is pretty much the same:</p>

<div class="break-out">

<pre>
  <code class="language-php">
add_action( 'manage_realestate_posts_custom_column', 'smashing_realestate_column', 10, 2 );
function smashing_realestate_column( $column, $post_id ) {
  [...]

  </code>
  <code class="language-php" style="background-color: #fffbd7">
  // Surface area column
  if ( 'area' === $column ) {
    $area = get_post_meta( $post_id, 'area', true );

    if ( ! $area ) {
      _e( 'n/a' );
    } else {
      echo number_format( $area, 0, '.', ',' ) . ' m<sup>2</sup>';
    }
  }
  </code>
  <code class="language-php">
}
</code></pre></div>

<p>That's it! Our real-estate overview page now contains all relevant information that we want to display:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a704dd36-5c89-4702-986d-430130ea5a9c/6-step2b-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5908287d-bec0-40e4-bc3f-43980beb29b1/6-step2b-800w-opt.png" width="800" height="339" alt="real-estate overview page" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a704dd36-5c89-4702-986d-430130ea5a9c/6-step2b-large-opt.png">View large version</a>)</figcaption></figure>

Let's move on to some of the more funky stuff. Let's add some sorting functionality to our columns!</p>

## Making Columns Sortable

<p>Making columns sortable is relatively easy in WordPress, yet it's rarely implemented for custom columns. Sorting helps you organize content and enables you to find content quickly. For example, we could sort our real-estate overview by price and then find our cheapest and most expensive pieces of property.</p>

<p>We'll start by adding our "price" column to the list of sortable columns:</p>

<div class="break-out">

<pre><code class="language-php">
add_filter( 'manage_edit-realestate_sortable_columns', 'smashing_realestate_sortable_columns');
function smashing_realestate_sortable_columns( $columns ) {
  $columns['price'] = 'price_per_month';
  return $columns;
}
</code></pre></div>

<p>This code hooks into the <code>manage_edit-realestate_sortable_columns</code> filter and adds <code>smashing_realestate_sortable_columns</code> as a callback function (line 1). The "price" column is made sortable by adding it to the list of sortable columns in line 3. Note that the array key, <code>price</code>, is the name we've given our column before. The array value is used to tell WordPress what it should sort by. We could, for example, use WordPress' native sorting strategies to sort by title, date or comment count.</p>

<p>In our case, however, we want to sort by a custom field. This requires us to create another function, which needs to alter the posts query if we're trying to sort by price. We're going to use the <code>pre_get_posts</code> action. It allows us to change the <code>WP_Query</code> object (the object that WordPress uses to query posts) and fires before posts are queried. We check whether to sort by price and, if so, change the query accordingly:</p>

<div class="break-out">

<pre><code class="language-php">
add_action( 'pre_get_posts', 'smashing_posts_orderby' );
function smashing_posts_orderby( $query ) {
  if( ! is_admin() || ! $query-&gt;is_main_query() ) {
    return;
  }

  if ( 'price_per_month' === $query-&gt;get( 'orderby') ) {
    $query-&gt;set( 'orderby', 'meta_value' );
    $query-&gt;set( 'meta_key', 'price_per_month' );
    $query-&gt;set( 'meta_type', 'numeric' );
  }
}
</code></pre></div>

<p>Lines 1 and 2 add the callback function to the action and start the definition of the callback function, respectively. Line 3 then checks whether we're in the admin panel and whether the query is the main posts query (<a href="https://codex.wordpress.org/Function_Reference/is_main_query">see the Codex</a> for more information). If not, we don't change the query. Then, we check whether the current sorting strategy is by price. If it is, we adjust the query accordingly: We set the <code>meta_key</code> value to <code>price_per_month</code>, telling WordPress to retrieve this custom field for all real estate, and we set the <code>orderby</code> key to <code>meta_value</code>, which tells WordPress to sort by the value belonging to the specified meta key. Finally, we tell WordPress to sort numerically instead of alphabetically, because "price" is a numerical column.</p>

<p><strong>Note</strong>: You might have noticed that the filter we hook into is named <code>manage_edit-realestate_sortable_columns</code>, whereas you might have expected it to be <code>manage_realestate_sortable_columns</code> (without the <code>edit-</code>). This is simply an inconsistency in filter naming in WordPress.</p>

<p>The result is a sortable price column:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/771c4798-4aec-4dfe-8895-b6b46b84a11c/code-sorting.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/771c4798-4aec-4dfe-8895-b6b46b84a11c/code-sorting.gif" width="600" height="332" alt="code sorting" /></a></figure>

<p>The same procedure can be repeated for the "area" column. For textual columns, which should be sorted alphabetically, be sure to leave out the <code>$query-&gt;set( 'meta_type', 'numeric' )</code> part.</p>

## Managing Columns With The Admin Columns Plugin

<p>Now that we've covered the programming part of this tutorial, it's time to move on to the much simpler method: using the <a href="https://wordpress.org/plugins/codepress-admin-columns/">Admin Columns</a> plugin. Without touching any code and using a simple drag-and-drop interface, you can manage columns with just a few clicks. More than 150 column types exist. It comes with optional fields that let you customize how a column is named and behaves. In this last part of the tutorial, we're going to show you how to set up Admin Columns to create the exact same overview as before. On top of that, we will show you how you can then filter and edit content directly from the content-overview screens.</p>

<p>First off, install Admin Columns as you would install any plugin, and activate it. It's ready for use right away, so let's start to manage our columns by going to the "Column Settings" page.</p>

<p>Admin Columns lets you control the columns per content type (for example, posts, pages, users or comments) using the dropdown box highlighted in the image above. In our case, we will select the post type "Real Estate." You will see the screen immediately showing the columns that are currently active for this post type.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab5a3cd5-3fd3-42ea-80dd-afa2f104a6e7/7-ac-listscreens-dropdown-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8151b76f-e2b2-49e5-9d4b-bbc40e8916ce/7-ac-listscreens-dropdown-800w-opt.png" width="800" height="465" alt="controlling the columns per content type" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab5a3cd5-3fd3-42ea-80dd-afa2f104a6e7/7-ac-listscreens-dropdown-large-opt.png">View large version</a>)</figcaption></figure>

### Adding, Removing and Reordering Columns

<p>Let's clean up a bit by removing columns we don't need for our real-estate overview:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95f63a66-d458-4fa7-9033-b29bd3935af1/ac-remove-columns.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95f63a66-d458-4fa7-9033-b29bd3935af1/ac-remove-columns.gif" width="600" height="377" alt="" /></a></figure>

<p>Wasn't that easy? We will continue by adding our first relevant column: the featured image that shows a picture of the property. To do so, simply click the "Add Column" button, choose the "Featured Image" column type from the dropdown, and fill in the appropriate settings:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e046fce9-1f9c-41cc-a73a-63c2328ea93f/ac-add-column.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e046fce9-1f9c-41cc-a73a-63c2328ea93f/ac-add-column.gif" width="600" height="377" alt="adding columns" /></a></figure>

<p>As you can see, Admin Columns shows relevant display options for your columns to give you full control over their appearance. Here, you're asked to specify the dimensions of the image to display. Later, we will see that Admin Columns shows the appropriate options when you select a different column type. For these options, Admin Columns tries to present sensible defaults, to minimize the time required to add new columns.</p>

<p>The last part showed us how to drag the column to the first position. Admin Columns lets you reorder columns simply by dragging them around. Our real-estate screen now looks like this:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c6bf6a6-79a0-41e6-b2c0-f23c0559a95c/8-ac-step1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d212916-b69e-4f7d-a98e-9a8b0a0e00ce/8-ac-step1-800w-opt.png" width="800" height="337" alt="eal-estate screen updated" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c6bf6a6-79a0-41e6-b2c0-f23c0559a95c/8-ac-step1-large-opt.png">View large version</a>)</figcaption></figure>

We're now going to add the two columns to display the property's living area and monthly rent. Because we've added these custom fields using the <a href="https://wordpress.org/plugins/advanced-custom-fields/">Advanced Custom Fields</a> plugin, we will use Admin Columns' ACF integration plugin for this task. However, the "Custom Field" column would have also sufficed for this purpose.</p>

<p>The animation below shows the process of adding the "Area" and "Price" columns:</p>

<figure><a
href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9549c72c-9777-4ab3-a3ae-4a072c77e349/ac-add-area-price-columns.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9549c72c-9777-4ab3-a3ae-4a072c77e349/ac-add-area-price-columns.gif" width="600" height="377" alt="adding area and price columns"/></a></figure>

<p><strong>Note</strong>: Admin Columns offers integration add-ons for quite a few other plugins, including WooCommerce, Ninja Forms and Yoast SEO.</p>

<p>For those who followed the code examples and paid close attention, we did not add the "City" column. It's a little trickier to do that with code, but with Admin Columns it's a breeze. We simply select the "Taxonomy" column and pick the "City" taxonomy, and voilà! Our result is there. Didn't we tell you? It's a breeze!</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/160cdf50-3157-40ac-a3ae-b7b23ff597ee/9-ac-final-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9edce3ce-ef99-4442-bb55-9cfd6307735a/9-ac-final-800w-opt.png" width="800" height="337" alt="city taxonomy column" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/160cdf50-3157-40ac-a3ae-b7b23ff597ee/9-ac-final-large-opt.png">View large version</a>)</figcaption></figure>

Depending on your mouse-handling speed, we've achieved this result, from top to bottom, in somewhere between two and three minutes!</p>

### Sorting and Filtering With Admin Columns

<p>Most of what you've seen so far is part of the free version of Admin Columns, which can be <a href="https://wordpress.org/plugins/codepress-admin-columns/">downloaded from WordPress.org</a>. However, there is also Admin Columns Pro, which offers additional features. We'll discuss the most prominent features for this use case: sorting, filtering and editing. These features will help you to quickly find and update your content right from the overview screen.</p>

<p>Although the features might be pretty self-explanatory, I'll explain them really quickly in the context of Admin Columns.</p>

<p>Sorting will display your content in a particular order based on the value of a column. It's great for getting insight into your content very quickly. For example, it enables you see which pages have a page template and to order them alphabetically. For a regular blog, you could quickly find out which users have authored the highest number of posts by sorting users according to their post count.</p>

<p>Filtering helps you to find content faster. You can filter columns that have a specific value, or a value within some range (for numeric columns) or without any value set at all. For instance, you could find e-commerce products within a price range, or posts missing a featured image or custom field. You could even use multiple filters together to target content more precisely.</p>

<p>Let's get back to our use case and consider a simple example: We want to find houses with the largest surface areas. This will take us only a few seconds because we can simply make the "Area" column sortable and sort by that column in the real-estate overview screen:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d8c0bd0-4e7f-42a7-8730-14cdbc5ea0aa/ac-sorting.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d8c0bd0-4e7f-42a7-8730-14cdbc5ea0aa/ac-sorting.gif" width="600" height="405" alt="sorting" /></a></figure>

<p>Now, let's take it a step further by adding a filter: We want to find the top 10 houses with the largest surface areas, but only those with a monthly rental price between $300 and $500. Again, a few clicks are enough:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16c1b210-8624-4a99-9e1e-e65475121d64/ac-filtering.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16c1b210-8624-4a99-9e1e-e65475121d64/ac-filtering.gif" width="600" height="405" alt="filtering" /></a></figure>

<p>There are, of course, many other ways to sort and filter. Combined, the features are a powerful tool to gain insight into your content.</p>

### Editing With Admin Columns

<p>The real-estate overview screen now shows all relevant information and allows you to find the content you need. However, one thing is lacking: To edit our content, we have to go to the editing page, find the fields we want to change, update them, click "Update," and go back to our overview screen.</p>

<p>What if we could do the same process in just three simple steps: click, edit, save? With Admin Columns Pro, we can.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc5e335-fc93-4465-b1d6-1e5a1d7da135/ac-editing.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc5e335-fc93-4465-b1d6-1e5a1d7da135/ac-editing.gif" width="600" height="405" alt="editing" /></a></figure>

<p>The screenshot above shows "direct editing" mode for the property title, and it's available for almost all custom columns. In Admin Columns Pro, inline editing can be toggled from the columns settings screen. It automatically detects your content type and adds editability accordingly. With images, for instance, the media gallery will pop up.</p>

<p>In this example, we've used the <a href="https://www.admincolumns.com/advanced-custom-fields-columns/">Advanced Custom Fields</a> add-on for Admin Columns, which comes with all business and developer licenses. It detects your ACF fields and adds them as possible columns. They are automatically sortable, filterable and editable &mdash; just toggle the corresponding icon.</p>

<p>The result is pretty neat: Our real-estate overview screen adds editing icons to all cells, and just by clicking, editing and saving, we can update our content. Let's see that in practice: We've enabled direct editing for all of our custom columns, and we're going to use that functionality to quickly update our content:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9ebb236-04b9-459f-9abf-32b765f6825a/ac-editing-all.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9ebb236-04b9-459f-9abf-32b765f6825a/ac-editing-all.gif" width="600" height="405" alt="editing all" /></a></figure>

<p>The changes are instantly saved. Should anything go wrong, undo and redo buttons are available to quickly revert.</p>

<p>Direct editing is supported for almost all columns. With the Advanced Custom Fields and WooCommerce add-ons, Admin Columns gives you a native editing experience as if you were editing from the details page.</p>

## Wrapping Up

<p>Admin Columns can do much more cool stuff, but there's just not enough room in this article. Why not <a href="https://www.admincolumns.com">take a look</a> and check out some of the awesome features for yourself? We hope to see you there!</p>

{{< signature "mc, ra, al, yk, il" >}}


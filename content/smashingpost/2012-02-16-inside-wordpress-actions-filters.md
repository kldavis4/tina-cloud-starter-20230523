---
title: Inside WordPress Actions And Filters
slug: inside-wordpress-actions-filters
image: >-
  https://www.smashingmagazine.com/general/2013/11/29/174458-revision-127/attachment/header_image_550px/
date: 2012-02-16T15:56:55.000Z
author: gennady-kovshenin
description: >-
  Gone are the days when WordPress developers, wanting to extend the functionality, had to alter and hack the WordPress core source code directly,
  resulting in headaches when upgrading and sharing modifications.
categories:
  - WordPress
  - Techniques (WP)
---
When WordPress 1.2 rolled out back in 2004, a new plugin architecture was introduced that is now commonly referred to as actions and filters, hooks, and the Plugin API.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/213758c8-9f8d-4bc0-b5f4-143ef91574cf/header-image-550px.png" alt="WordPress Actions and Filters" width="550" />

WordPress’ core has been carefully sprinkled with actions and filters that external code (in the form of themes and plugins) can hook into, injecting new functionality into the standard flow. The <a href="https://www.smashingmagazine.com/2011/09/how-to-create-a-wordpress-plugin/">Wordpress Plugin API</a> provides a neat interface to work with actions and filters. This article gathers insight into the inner workings, elegance and beauty of the Plugin API. It will help WordPress plugin and theme developers gain a more profound understanding of what happens behind the scenes, why some things will work and others won’t, and where to look when they unexpectedly don’t.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Utilizing User Roles In WordPress](https://www.smashingmagazine.com/2012/10/utilizing-user-roles-wordpress/)
*   [How To Become A Top WordPress Professional](https://www.smashingmagazine.com/2012/12/become-top-wordpress-professional/)
*   [Useful WordPress Tools, Themes And Plugins](https://www.smashingmagazine.com/2012/03/useful-wordpress-tools-themes-plugins/)
*   <span>[Writing Effective Documentation For WordPress End Users](https://www.smashingmagazine.com/2012/07/writing-effective-wordpress-documentation/)</span>

{{% feature-panel %}}

### Warning

This is a detailed walkthrough of some of WordPress’ core source code. To get the most understanding, insight and fun from it, you will need basic knowledge of PHP and WordPress functions, as well as the <a href="https://wordpress.org/latest.zip">source code for WordPress 3+</a> (which can be viewed <a href="https://core.trac.wordpress.org/browser/trunk">online</a>) and the courage to dig in and get your hands dirty.</p>

## The Plugin API

The functions that theme and plugin developers most commonly use are these:

*   [`add_action()`](https://codex.wordpress.org/Function_Reference/add_action)
*   [`add_filter()`](https://codex.wordpress.org/Function_Reference/add_filter)
*   [`do_action()`](https://codex.wordpress.org/Function_Reference/do_action)
*   [`apply_filters()`](https://codex.wordpress.org/Function_Reference/apply_filters)

These functions are well-known, well-documented, and used abundantly in a majority of themes and plugins. The <a href="https://codex.wordpress.org/Plugin_API">Codex Plugin API</a> page provides some basic examples of WordPress hooks in action. The Plugin API’s source code has made itself at home in the <code>/wp-includes/plugin.php</code> file. Feel free to open it in your favorite text editor or <a href="https://core.trac.wordpress.org/browser/trunk/wp-includes/plugin.php">view it online</a> to follow along.

The API is quite compact, around only 350 lines of code (the rest are comments). It exposes 22 functions, 14 of which work directly with actions and filters, while the rest are helper functions and utility functions that pertain to plugin path resolution, activation and deactivation.

The Plugin API is made available in the earliest stages of the WordPress boot-up process, and the earliest action one can hook into is <code>muplugins_loaded</code>, which is fired off after all “<a href="https://codex.wordpress.org/Must_Use_Plugins">must use</a>” and <a href="https://codex.wordpress.org/Create_A_Network#WordPress_Plugins">network-wide</a> plugins are included — rather useless if your plugin is neither of those. The <code>plugins_loaded</code> action is fired off immediately after all valid plugin files are included in the scope. Finally, <code>after_setup_theme</code> is fired off once the active template <code>functions.php</code> has been included.

The <a href="https://codex.wordpress.org/Plugin_API/Action_Reference">Actions Reference</a> and the <a href="https://codex.wordpress.org/Plugin_API/Filter_Reference">Filter Reference</a> contain descriptions for many of the Actions and Filters available during typical request scenarios.</p>

## $wp_filter

The Plugin API provides functions that act on the <code>$wp_filter</code> global, which is a simple associative array with a particular structure. All of the action and filter functions read from and write to this globally shared associative array, which makes the API completely decoupled from WordPress’ core code. You can actually include the Plugin API’s <code>plugin.php</code> file in any other PHP project or framework and use all of the action and filter functions (<code>do</code>/<code>apply</code>, <code>add</code>, <code>remove</code>, <code>has</code>, <code>current</code>) without any modification whatsoever. In fact, an almost unchanged file is shipped with <a href="https://backpress.org/">BackPress</a>, a collection of standalone libraries that grew out of WordPress. The secret to this lies in the high flexibility of the API and the simplicity of its concept.

The <code>$wp_filter</code> global starts out in WordPress as an undefined variable, completely void of any data. Data is written to it once an action or filter is added via <code>add_action()</code> or <code>add_filter()</code>. So, this will be our starting point. The two functions have an identical prototype in terms of function arguments:

<pre><code class="language-php">function add_filter($tag, $function_to_add, $priority = 10, $accepted_args = 1)</code></pre>

This function is <a href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/plugin.php#L46">defined on line 65</a>. It's very simple. Notice how it returns <code>true</code> quite regardless of what happens inside. The <code>add_action()</code> (on line 331) function invokes the <code>add_filter()</code> function without any modification. This means that <code>$wp_filter</code> does not distinguish between filters and actions when queuing them. The data structure of <code>$wp_filter</code> is quite simple and can be represented by the following diagram:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8fc630e-f41c-430a-9e2b-42d273ffb62d/wp-filter-structure.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6c1ddb3-2d26-42e0-b2e8-37bc4f5f37cf/wp-filter-structure-550px.png" alt="WordPress filter structure" width="550" /></a><br>
<em>The data structure of <code>$wp_filter</code>.</em>

A “function” array (i.e. an array containing a function callback and the number of arguments it accepts) is identified by the <code>_wp_filter_build_unique_id()</code> (<a href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/plugin.php#L721">line 750</a>) helper function, which returns a unique <code>idx</code> for a callback, ordered by “priority” and attached to a “tag” (which is the name of the filter or action). This results in a list of actions with unique callbacks that will be invoked only once, regardless of how many times the same callback is added (the unique ID ensures this).</p>

## Come Get Some Action!

Actions are usually fired off via the <code>do_action()</code> function, which has the following prototype:

<pre><code class="language-php">function do_action($tag, $arg = ’, ...)</code></pre>

The definition of the function is on <a href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/plugin.php#L336">line 359</a>, you're more than welcome to read the bits of code there and return for a step-by-step explanation.

First of all, the <code>$wp_actions</code> global keeps track of how times a particular action has been triggered. It’s a simple associative array, with the action tag or name as its keys. The <code>did_action()</code> function (<a href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/plugin.php#L412">line 423</a>) returns the number of times that an action has been triggered by accessing this <code>$wp_actions</code> array. Next, the <code>all</code> action is triggered by the <code>_wp_call_all_hook()</code> function. This function simply pulls on all of the registered or added hooks in the <code>$wp_filter['all']</code> array using the PHP <a href="https://www.php.net/manual/en/function.call-user-func-array.php"><code>call_user_func_array()</code></a> function (we will look at a great application of the <code>all</code> action a bit later). This is followed by a simple “check and return if action does not exist.”

Next, you’ll notice that the action tag is pushed into the global <code>$wp_current_filter</code> array. The <code>current_filter()</code> function (<a href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/plugin.php#L297">line 306</a>) returns the last value stored in this global array. Action and filter callbacks can pull on more actions and filters, invoking other callbacks, resulting in long chains. One can trace the chain of hooks by looking into the global <code>$wp_current_filter</code> array during the execution of a callback. However, these chains do not usually get any longer than a couple of links, unless you do this:

<pre><code class="language-php">add_action( 'my_action', 'my_function' );
add_action( 'my_action_2', 'my_function_2' );
add_action( 'my_action_3', 'my_function_3' );
add_action( 'my_action_4', 'my_function_4' );
function my_function() { do_action( 'my_action_2'); }
function my_function_2() { do_action( 'my_action_3'); }
function my_function_3() { do_action( 'my_action_4'); }
function my_function_4() { var_dump( $GLOBALS['wp_current_filter']); }

do_action( 'my_action' );

/* array(4) {
[0]=&gt; string(9) "my_action"
[1]=&gt; string(11) "my_action_2"
[2]=&gt; string(11) "my_action_3"
[3]=&gt; string(11) "my_action_4"
} */</code></pre>

Why would anyone do this? The previous is an evident example, however consider the following piece of code involving the <code>get_{$meta_type}_metadata</code> where I want to augment a specific key:

<pre><code class="language-php">add_filter( 'get_post_metadata', 'augment_post_meta_by_key', 999, 4 );
function augment_post_meta_by_key( $null, $object_id, $meta_key, $single ) {
  if ( $meta_key != 'my_key' ) return $null; /* Ignore everything else */
  /* Get the value */
  $value = get_post_meta( $object_id, 'my_key', true );
  if ( $value == '12345' ) return '54321'; /* Simple augmentation of a meta value */
}</code></pre>

Do you see the pitfall? Correct, this is an infinite loop. The filter will fire off inside of <code>augment_post_meta_by_key</code> because we're doing more meta requests. So the <code>$current_filter</code> chain will be quite long if you look at it. A solution would be to remove the filter before getting the value and re-adding it afterwards.

Back on track: look at <a href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/plugin.php#L359">line 386</a>. All of the callback arguments are assembled into the local <code>$args</code> variable, through the use of PHP’s <a href="https://www.php.net/manual/en/function.func-get-arg.php"><code>func_get_arg()</code></a>. If you’re curious about the unusual <code>// array(&amp;this)</code> business around line 387, check <a href="https://core.trac.wordpress.org/ticket/17111">Ticket #17111</a>.

Right after the callback arguments are taken care of, the <code>$wp_filter</code> global has its data for the current tag sorted by priority. When actions and filters are added to the tags in <code>$wp_filter</code>, priority arrays that contain the callbacks are created and pushed into the tag array in an unsorted order. In other words, adding four actions with priorities of 10, 1, 15, 3 would result in the tag containing priorities 10, 1, 15, 3 in the exact same order; thus, sorting by priority is required. Sorting is done by a simple <a href="https://php.net/manual/en/function.ksort.php"><code>ksort()</code></a>, and the global <code>$merged_filters</code> array keeps track of whether a tag’s priorities are sorted or not. The usage of <code>ksort()</code> shows that <strong>priorities can be strings and negative numbers</strong>, which is perfectly valid, and that no action callback is ever guaranteed to run first. When an action or filter is added, <a href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/plugin.php#L65">this line of code</a> - <code>unset( $merged_filters[$tag] );</code> makes sure that the priorities are sorted, even if they’ve been sorted once before.

Next, each <code>$wp_filter[$tag]</code> callback is invoked by the <a href="https://php.net/manual/en/function.call-user-func-array.php"><code>call_user_func_array()</code></a> function, with the second argument (i.e. the array of arguments to call the actions with) truncated to the number of accepted arguments (<code>$accepted_args</code>).

Finally, the current action gets unset from <code>$wp_current_filter</code>.

## Filters

The <code>apply_filters()</code> function (<a href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/plugin.php#L112">line 134</a>) goes through practically the same process as the <code>do_action()</code> function, with some minor differences in code implementation and a major difference in the fact that the <code>apply_filters()</code> function returns a value.

If you’ve been reading the source code, you may have noticed by now that <code>has_action()</code> is wrapped around <code>has_filter()</code>; that <code>remove_action()</code> and <code>remove_all_actions()</code> are wrapped around <code>remove_filter()</code> and <code>remove_all_filters()</code>; and that <code>add_action()</code> is wrapped around <code>add_filter()</code>…

### So, Why Bother!?

Although both will call your functions the same way, and you actually could — <strong>but never should!</strong> — apply <code>add_action()</code> to lists of filters and vice versa, or use <code>apply_filters()</code> instead of <code>do_action()</code> or even <code>do_action()</code> instead of <code>apply_filters()</code>, keeping them functionally and semantically separate is absolutely critical. As Samuel Wood says in “<a href="https://ottopress.com/2011/actions-and-filters-are-not-the-same-thing/">Actions and Filters Are Not the Same Thing</a>”:
<blockquote>Filters filter things. Actions do not. And this is critically important when you’re writing a filter. A filter function should never, ever, have unexpected side effects.</blockquote>

## ref_array

A quick note about <code>do_action_ref_array()</code> (line 197) and <code>apply_filters_ref_array()</code> (<a href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/plugin.php#L432">line 448</a>). These functions contain the same code as their non-<code>ref_array</code> counterparts, and they accept an array of arguments instead of a list of arguments:

<pre><code class="language-php">do_action( 'my_action', 'a string', array( 1, 2, 3 ), false, 2 );
$my_action_arguments = array(
'a string',
array( 1, 2, 3 ),
false,
2
);
do_action_ref_array( 'my_action', $my_action_arguments );</code></pre>

The two behave the same. The array version is convenient to use when your arguments have been building up in an array, because you won’t have to unpack it.</p>

## Debugging

### Dumping

A clean installation of WordPress will contain around 200 actions and filters and twice as many registered callbacks when the <code>wp</code> action fires off. You probably dumped the global <code>$wp_filter</code> array at the beginning of this article to see its structure, and perhaps noticed that interpreting it is quite difficult due to the massive amount of data and the <code>var_dump</code> presentation. Now that you’re comfortable with the structure of <code>$wp_filter</code>, the array can be custom <a href="https://en.wikipedia.org/wiki/Prettyprint">pretty-printed</a> with something more or less as simple as the following:

<pre><code class="language-php">echo '&lt;ul&gt;;
/* Each [tag] */
foreach ( $GLOBALS['wp_filter'] as $tag =&gt; $priority_sets ) {
  echo '&lt;li&gt;&lt;strong&gt; . $tag . '&lt;/strong&gt;&lt;ul&gt;;

  /* Each [priority] */
  foreach ( $priority_sets as $priority =&gt; $idxs ) {
    echo '&lt;li&gt; . $priority . '&lt;ul&gt;;

    /* Each [callback] */
    foreach ( $idxs as $idx =&gt; $callback ) {
      if ( gettype($callback['function']) == 'object' ) $function = '{ closure }';
      else if ( is_array( $callback['function'] ) ) {
        $function = print_r( $callback['function'][0], true );
        $function .= ':: '.print_r( $callback['function'][1], true );
      }
      else $function = $callback['function'];
      echo '&lt;li&gt; . $function . '&lt;i&gt;(' . $callback['accepted_args'] . ' arguments)&lt;/i&gt;&lt;/li&gt;;
    }
    echo '&lt;/ul&gt;&lt;/li&gt;;
  }
  echo '&lt;/ul&gt;&lt;/li&gt;;
}
echo '&lt;/ul&gt;;</code></pre>

The result is a more compact and friendlier report. Of course, when debugging, you’ll probably know what you’re looking for, so there would be no need to dump the whole <code>$wp_filter</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6896fbb0-3e06-4985-b781-49b7aadea97a/dump-wp-filter.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4bfac06-751d-42fb-92a2-f60278a00897/dump-wp-filter-550px.png" alt="A custom pretty print of the $wp_filter global vs. a var_dump" width="550" /></a><br>
<em>A custom pretty-print of the <code>$wp_filter</code> global (left) compared to a <code>var_dump</code> (right).</em>

### Tracing via the “all” Hook

Remember the <code>all</code> hook (<a href="https://core.trac.wordpress.org/browser/branches/3.3/wp-includes/plugin.php#L134">line 140</a>)? It fires off every time the <code>apply_filters()</code> or <code>do_action()</code> function is called. This means that tracing the execution of filters and actions is possible and quite useful for debugging.

<pre><code class="language-php">/* Hook to the 'all' action */
add_action( 'all', 'backtrace_filters_and_actions');
function backtrace_filters_and_actions() {
  /* The arguments are not truncated, so we get everything */
  $arguments = func_get_args();
  $tag = array_shift( $arguments ); /* Shift the tag */

  /* Get the hook type by backtracing */
  $backtrace = debug_backtrace();
  $hook_type = $backtrace[3]['function'];

  echo "&lt;pre&gt;";
  echo "&lt;i&gt;$hook_type&lt;/i&gt; &lt;b&gt;$tag&lt;/b&gt;n";
  foreach ( $arguments as $argument )
    echo "tt" . htmlentities(var_export( $argument, true )) . "n";

    echo "n";
    echo "&lt;/pre&gt;";
}</code></pre>

The little code snippet can be improved by adding timestamps for profiling, along with <code>$wp_filter</code> dumping to show more information about what has been called, and so much more useful stuff.</p>

## Final Thoughts

WordPress has evolved a lot since the early versions, and it is one of the best examples of how to write a CMS in PHP and other programming and scripting languages. WordPress’ core architecture has become very robust, and software engineers could learn a lot from the platform’s source code. The inner workings, elegance and beauty of WordPress’ actions and filters has given me (and hopefully you, too) tremendous insight, inspiration and motivation to keep digging.</p>

### More Resources

Don’t stop here! Your journey has just begun. Check these out:

*   “[WordPress Hooks Database](https://adambrown.info/p/wp_hooks),” Adam Brown An overview of all actions and filters that are present in WordPress, with source-code locations and much more.
*   “[Debug WordPress Hooks](https://www.rarst.net/script/debug-wordpress-hooks/),” Andrey Savchenko More advanced hook-dumping snippets for WordPress.

{{< signature "al" >}}


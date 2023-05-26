---
title: 'How To Make A WordPress Plugin Extensible'
slug: making-wordpress-plugin-extensible
author: benjamin-intal
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a111bfc-d5c1-4866-9cab-936952f9c2a9/wordpress-plugins.png
date: 2018-03-14T13:40:28+01:00
summary: >-
  Just when you thought you've finally found a plugin that does everything you need, there's still that one tiny important thing it can't do. Find out how to make your plugin extensible and reduce headache.
description: >-
  Just when you thought you've finally found a plugin that does everything you need, there's still that one tiny important thing it can't do. Find out how to make your plugin extensible and reduce headache.
categories:
  - WordPress
  - Plugins
---
<p>Have you ever used a plugin and wished it did something a bit differently? Perhaps you needed something unique that was beyond the scope of the settings page of the plugin.</p>

<p>I have personally encountered this, and I'm betting you have, too. If you're a WordPress plugin developer, most likely some of your users have also encountered this while using your plugin.</p>

<p>Here's a typical scenario: You've finally found that plugin that does everything you need &mdash; except for one tiny important thing. There is no setting or option to enable that tiny thing, so you browse the documentation and find that you can't do anything about it. You request the feature in the WordPress plugin's support forum &mdash; but no dice. In the end, you uninstall it and continue your search.</p>

<p>Imagine if you were the developer of this plugin. What would you do if a user asked for some particular functionality?</p>

<p>The ideal thing would be to implement it. But if the feature was for a very special use case, then adding it would be impractical. It wouldn't be good to have a plugin setting that only 0.1% of your users would have a use for.</p>

<p>You'd only want to implement features that affect the majority of your users. In reality, 80% of users use 20% of the features (the 80/20 rule). So, make sure that any new feature is highly requested, and that 80% of your users would benefit from it, before implementing it. If you created a setting for every feature that is requested, then your plugin would become complicated and bloated &mdash; and nobody wants that.</p>

<p>Your best bet is to make the plugin extensible, code-wise, so that other people can enhance or modify it for their own needs.</p>

<p>In this article, you'll learn about why making your plugin extensible is a good idea. I'll also share a few tips of how I've learned to do this.</p>

{{% feature-panel %}}

## What Makes A Plugin Extensible?

<p>In a nutshell, an extensible plugin means that it adheres to the "O" part of the SOLID principles of object-oriented programming &mdash; namely, the open/closed principle.</p>

<p>If you're unfamiliar with the open/closed principle, it basically means that <strong>other people shouldn't have to edit your code in order to modify something</strong>.</p>

<p>Applying this principle to a WordPress plugin, it would mean that a plugin is extensible if it has provisions in it that enable other people to modify its behavior. It's just like how WordPress allows people to "hook" into different areas of WordPress, but at the level of the plugin.</p>

## A Typical Example Of A Plugin

<p>Let's see how we can create an extensible plugin, starting with a sample plugin that isn't.</p>

<p>Suppose we have a plugin that generates a sidebar widget that displays the titles of the three latest posts. At the heart of the plugin is a function that simply wraps the titles of those three posts in list tags:</p>

<pre><code class="language-javascript">
function get_some_post_titles() {
  $args = array(
      'posts_per_page' =&gt; 3,
  );

  $posts = get_posts( $args );

  $output = '<ul>';
  foreach ( $posts as $post ) {
      $output .= '<li>' . $post-&gt;post_title . '</li>';
  }
  $output .= '</ul>';

  return $output;
}
</code></pre>

<p>While this code works and gets the job done, it isn't quite extensible.</p>

<p>Why? Because the function is set in its own ways, there's no way to change its behavior without modifying the code directly.</p>

<p>What if a user wanted to display more than three posts, or perhaps include links with the posts' titles? There's no way to do that with the code above. The user is stuck with how the plugin works and can nothing to change it.</p>

## Including A Hundred Settings Isn't The Answer

<p>There are a number of ways to enhance the plugin above to allow users to customize it.</p>

<p>One such way would be to add a lot of options in the settings, but even that might not satisfy all of the possibilities users would want from the plugin.</p>

<p>What if the user wanted to do any of the following (scenarios we'll revisit later):</p>

<ul>
<li>display WooCommerce products or posts from a particular category;</li>
<li>display the items in a carousel provided by another plugin, instead of as a simple list;</li>
<li>perform a custom database query, and then use those query's posts in the list.</li>
</ul>

<p>If we added a hundred settings to our widget, then we would be able to cover the use cases above. But what if one of these scenarios changes, and now the user wants to display only WooCommerce products that are currently in stock? The widget would need even more settings to accommodate this. Pretty soon, we'd have a gazillion settings.</p>

<p>Also, a plugin with a huge list of settings isn't exactly user-friendly. Steer away from this route if possible.</p>

<p>So, how would we go about solving this problem? We'd make the plugin extensible.</p>

## Adding Our Own Hooks To Make It Extensible

<p>By studying the plugin's code above, we see a few operations that the main function performs:</p>

<ul>
<li>It gets posts using <code>get_posts</code>.</li>
<li>It generates a list of post titles.</li>
<li>It returns the generated list.</li>
</ul>

<p>If other people were to modify this plugin's behavior, their work would mostly likely involve these three operations. To make our plugin extensible, we would have to add hooks around these to open them up for other developers.</p>

<p>In general, these are good areas to add hooks to a plugin:</p>

<ul>
<li>around and within the major processes,</li>
<li>when building output HTML,</li>
<li>for altering post or database queries,</li>
<li>before returning values from a function.</li>
</ul>

## A Typical Example Of An Extensible Plugin

<p>Taking these rules of thumb, we can add the following filters to make our plugin extensible:</p>

<ul>
<li>add <code>myplugin_get_posts_args</code> for modifying the arguments of <code>get_posts</code>,</li>
<li>add <code>myplugin_get_posts</code> for overriding the results of <code>get_posts</code>,</li>
<li>add <code>myplugin_list_item</code> for customizing the generation of a list entry,</li>
<li>add <code>myplugin_get_some_post_titles</code> for overriding the returned generated list.</li>
</ul>

<p>Here's the code again with all of the hooks added in:</p>

<pre><code class="language-javascript">
function get_some_post_titles() {
  $args = array(
      'posts_per_page' =&gt; 3,
  );

  // Let other people modify the arguments.
  $posts = get_posts( apply_filters( 'myplugin_get_posts_args', $args ) );

  // Let other people modify the post array, which will be used for display.
  $posts = apply_filters( 'myplugin_get_posts', $posts, $args );

  $output = '<ul>';
  foreach ( $posts as $post ) {

      // Let other people modify the list entry.
      $output .= '<li>' . apply_filters( 'myplugin_list_item', $post-&gt;post_title, $post ) . '</li>';
  }
  $output .= '</ul>';

  // Let other people modify our output list.
  return apply_filters( 'myplugin_get_some_post_titles', $output, $args );
}
</code></pre>

<p>You can also get the code above in the <a href="https://github.com/bfintal/How-to-Make-Your-WordPress-Plugin-Extensible">GitHub archive</a>.</p>

<p>I'm adding a lot of hooks here, which might seem impractical because the sample code is quite simple and small, but it illustrates my point: By adding just four hooks, other developers can now customize the plugin's behavior in all sorts of ways.</p>

## Namespacing And Context For Hooks

<p>Before proceeding, note two important things about the hooks we've implemented:</p>

<ul>
<li><strong>We're namespacing the hooks with <code>myplugin_</code>.</strong><br>
This ensures that the hook's name doesn't conflict with some other plugin's hook. This is just good practice, because if another hook with the same name is called, it could lead to unwanted effects.</li>

<li><strong>We're also passing a reference to <code>$args</code> in all of the hooks for context.</strong><br>
I do this so that if others use this filter to change something in the flow of the code, they can use that <code>$args</code> parameter as a reference to get an idea of why the hook was called, so that they can perform their adjustments accordingly.</li>
</ul>

## The Effects Of Our Hooks

<p>Remember the unique scenarios I talked about earlier? Let's revisit those and see how our hooks have made them possible:</p>

<ul>
<li>If the user wants to <strong>display WooCommerce products or posts from a particular category</strong>, then either they can use the filter <code>myplugin_get_posts_args</code> to add their own arguments for when the plugin queries posts, or they can use <code>myplugin_get_posts</code> to completely override the posts with their own list.</li>

<li>If the user wants to <strong>display the items in a carousel provided by another plugin</strong>, instead of as a simple list, then they can override the entire output of the function with <code>myplugin_get_some_post_titles</code>, and instead output a carousel from there.</li>

<li>If the user wants to <strong>perform a custom database query</strong> and then use that query's posts in the list, then, similar to the first scenario, they can use <code>myplugin_get_posts</code> to use their own database query and change the post array.</li>
</ul>

<p>Much better!</p>

## A Quick Example Of How To Use Our Filters

<p>Developers can use <code>add_filter</code> to hook into our filters above (or use <code>add_action</code> for actions).</p>

<p>Taking our first scenario above, a developer can just do the following to display WooCommerce products using the <code>myplugin_get_posts_args</code> filter that we created:</p>

<div class="break-out">

<pre><code class="language-javascript">add_filter( 'myplugin_get_posts_args', 'show_only_woocommerce_products' );
function show_only_woocommerce_products( $args ) {
   $args['post_type'] = 'product';
   return $args;
}
</code></pre></div>

## We Can Also Use Action Hooks

<p>Aside from using <code>apply_filters</code>, we can also use <code>do_action</code> to make our code extensible. The difference between the two is that the first allows others to change a variable, while the latter allows others to execute additional functionality in various parts of our code.</p>

<p>When using actions, we're essentially exposing the plugin's flow to other developers and letting them perform other things in tandem.</p>

<p>It might not be useful in our example (because we are only displaying a shortcode), but it would be helpful in others. For example, given an extensible backup plugin, we could create a plugin that also uploads the backup file to a third-party service such as Dropbox.</p>

## "Great! But Why Should I Care About Making My Plugin Extensible?"

<p>Well, if you're still not sold on the idea, here are a few thoughts on why allowing other people to modify your plugin's behavior is a good idea.</p>

### It Opens Up the Plugin to More Customization Possibilities

<p>Everyone has different needs. And there's a big chance your plugin won't satisfy all of them, nor can you anticipate them. Opening up your plugin to allow for modifications to key areas of your plugin's behavior can do wonders.</p>

### It Allows People to Introduce Modifications Without Touching the Plugin's Code

<p>Other developers won't be forced to change your plugin's files directly. This is a huge benefit because directly modifying a plugin's file is generally bad practice. If the plugin gets updated, then all of your modifications will be wiped.</p>

<p>If we add our own hooks for other people to use, then the plugin's modifications can be put in an external location &mdash; say, in another plugin. Done this way, the original plugin won't be touched at all, and it can be freely updated without breaking anything, and all of the modifications in the other plugin would remain intact.</p>

## Conclusion

<p>Extensible plugins are really awesome and give us room for a lot of customization possibilities. If you make your plugin extensible, your users and other developers will love you for it.</p>

<p>Take a look at plugins such as WooCommerce, Easy Digital Downloads and ACF. These plugins are extensible, and you can easily tell because numerous other plugins in WordPress' plugins directory add functionality to them. They also provide a wide array of action and filter hooks that modify various aspects of the plugins. The rules of thumb I've enumerated above have come up in my study of them.</p>

<p>Here are a few takeaways to make your plugin extensible:</p>

<ul>
<li>Follow the open/closed principle. Other people shouldn't have to edit your code in order to modify something.</li>

<li>
  <p>
    To make your plugin extensible, add hooks in these places:

    <ul>
    <li>around and within major processes,</li>
    <li>when building the output HTML,</li>
    <li>for altering post or database queries,</li>
    <li>before returning values from a function.</li>
    </ul>
  </p>
</li>

<li>Namespace your hooks' names with the name of your plugin to prevent naming conflicts.</li>

<li>Try passing other variables that are related to the hook, so that other people get some context of what's happening in the hook.</li>

<li>Don't forget to document your plugin's hooks, so that other people can learn of them.</li>
</ul>

### Further Reading

<p>Here are some resources if you want to learn more about extending plugins:</p>

<ul>
<li><a href="https://github.com/bfintal/How-to-Make-Your-WordPress-Plugin-Extensible">How to Make Your WordPress Plugin Extensible</a>, GitHub<br>
All of the sample code in this article.</li>

<li>"<a href="https://www.smashingmagazine.com/2016/01/get-started-with-hooks-wordpress/">Useful Tips to Get Started With WordPress Hooks</a>," Thomas Maier, Smashing Magazine</li>

<li>"<a href="https://www.smashingmagazine.com/2011/09/how-to-create-a-wordpress-plugin/">How to Create a WordPress Plugin</a>," Daniel Pataki, Smashing Magazine</li>

<li>"<a href="https://developer.wordpress.org/plugins/hooks/">Hooks</a>," Plugin Handbook, WordPress.org</li>
</ul>

{{< signature "mc, ra, al, yk, il" >}}


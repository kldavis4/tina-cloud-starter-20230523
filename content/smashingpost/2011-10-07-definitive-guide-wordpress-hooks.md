---
title: The Definitive Guide To WordPress Hooks
slug: definitive-guide-wordpress-hooks
image: >-
  https://www.smashingmagazine.com/general/2013/11/21/174458-revision-66/attachment/wp-hooks-guide/
date: 2011-10-07T14:28:24.000Z
author: daniel-pataki
description: >-
  If you’re into WordPress development, you can’t ignore hooks for long before
  you have to delve into them head on. Modifying WordPress core files is a big
  no-no, so whenever you want to change existing functionality or create new
  functionality, you will have to turn to hooks.

  [![wp-hooks-guide](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49da5405-9205-4b87-9933-135775a7cdce/wp-hooks-guide.jpg)](https://www.smashingmagazine.com/2011/10/07/definitive-guide-wordpress-hooks/)

  In this article, I would like to dispel some of the confusion around hooks,
  because not only are they _the_ way to code in WordPress, but they also teach
  us a great design pattern for development in general. Explaining this in depth
  will take a bit of time, but bear with me: by the end, you’ll be able to
  jumble hooks around like a pro.
categories:
  - WordPress
  - Hooks
  - Essentials
  - Functions
---
If you’re into WordPress development, you can’t ignore hooks for long before you have to delve into them head on. Modifying WordPress core files is a big no-no, so whenever you want to change existing functionality or create new functionality, you will have to turn to hooks.

<a href="https://www.smashingmagazine.com/2011/10/07/definitive-guide-wordpress-hooks/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49da5405-9205-4b87-9933-135775a7cdce/wp-hooks-guide.jpg" alt="wp-hooks-guide" width="500" height="300" /></a>

In this article, I would like to dispel some of the confusion around hooks, because not only are they <em>the</em> way to code in WordPress, but they also teach us a great design pattern for development in general. Explaining this in depth will take a bit of time, but bear with me: by the end, you’ll be able to jumble hooks around like a pro.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Useful Tips To Get Started With WordPress Hooks](https://www.smashingmagazine.com/2016/01/get-started-with-hooks-wordpress/)
*   [10 Useful WordPress Hook Hacks](https://www.smashingmagazine.com/2009/08/10-useful-wordpress-hook-hacks/)
*   [10 Exceptional WordPress Hacks](https://www.smashingmagazine.com/2009/04/10-exceptional-wordpress-hacks/)

{{% feature-panel %}}

## Why Hooks Exist

I think the most important step in grasping hooks is to understand the need for them. Let’s create a version of a WordPress function that already exists, and then evolve it a bit using the “hooks mindset.”

<pre><code class="language-php">function get_excerpt($text, $length = 150) {
      $excerpt = substr($text,$length)
      return $excerpt;
   }</code></pre>

This function takes two parameters: a string and the length at which we want to cut it. What happens if the user wants a 200-character excerpt instead of a 150-character one? They just modify the parameter when they use the function. No problem there.

If you use this function a lot, you will notice that the parameter for the text is usually the post’s content, and that you usually use 200 characters instead of the default 150. Wouldn’t it be nice if you could set up new defaults, so that you didn’t have to add the same parameters over and over again? Also, what happens if you want to add some more custom text to the end of the excerpt?

These are the kinds of problems that hooks solve. Let’s take a quick look at how.

<pre><code class="language-php">function get_excerpt($text, $length = 150) {

      $length = apply_filters("excerpt_length", $length);

      $excerpt = substr($text,$length)
      return $excerpt;
   }</code></pre>

As you can see, the default excerpt length is still 150, but we’ve also applied some filters to it. A filter allows you to write a function that modifies the value of something — in this case, the excerpt’s length. The name (or tag) of this filter is <code>excerpt_length</code>, and if no functions are attached to it, then its value will remain 150. Let’s see how we can now use this to modify the default value.

<pre><code class="language-php">function get_excerpt($text, $length = 150) {

      $length = apply_filters("excerpt_length", $length );

      $excerpt = substr($text,$length)
      return $excerpt;
   }

   function modify_excerpt_length() {
      return 200;
   }

   add_filter("excerpt_length", "modify_excerpt_length");</code></pre>

First, we have defined a function that does nothing but return a number. At this point, nothing is using the function, so let’s tell WordPress that we want to hook this into the <code>excerpt_length</code> filter.

We’ve successfully changed the default excerpt length in WordPress, without touching the original function and without even having to write a custom excerpt function. This will be extremely useful, because if you always want excerpts that are 200 characters long, just add this as a filter and then you won’t have to specify it every time.

Suppose you want to tack on some more text, like “Read on,” to the end of the excerpt. We could modify our original function to work with a hook and then tie a function to that hook, like so:

<pre><code class="language-php">function get_excerpt($text, $length = 150) {

      $length = apply_filters("excerpt_length", $length );

      $excerpt = substr($text,$length)
      return apply_filters("excerpt_content", $excerpt);
   }

   function modify_excerpt_content($excerpt) {
      return $excerpt . "Read on…";
   }
   add_filter("excerpt_content", "modify_excerpt_content");</code></pre>

This hook is placed at the end of the function and allows us to modify its end result. This time, we’ve also passed the output that the function would normally produce as a parameter to our hook. The function that we tie to this hook will receive this parameter.

All we are doing in our function is taking the original contents of <code>$excerpt</code> and appending our “Read on” text to the end. But if we choose, we could also return the text “Click the title to read this article,” which would replace the whole excerpt.

While our example is a bit redundant, since WordPress already has a better function, hopefully you’ve gotten to grips with the thinking behind hooks. Let’s look more in depth at what goes on with filters, actions, priorities, arguments and the other yummy options available.</p>

## Filters And Actions

Filters and actions are two types of hooks. As you saw in the previous section, a filter modifies the value of something. An action, rather than modifying something, calls another function to run beside it.

A commonly used action hook is <code>wp_head</code>. Let’s see how this works. You may have noticed a function at the bottom of your website’s <code>head</code> section named <code>wp_head()</code>. Diving into the code of this function, you can see that it contains a call to <code>do_action()</code>. This is similar to <code>apply_filters()</code>; it means to run all of the functions that are tied to the <code>wp_head</code> tag.

Let’s put a copyright meta tag on top of each post’s page to test how this works.

<pre><code class="language-php">add_action("wp_head", "my_copyright_meta");

   function my_copyright_meta() {
      if(is_singular()){
         echo "";
      }
   }</code></pre>

## The Workflow Of Using Hooks

While hooks are better documented nowadays, they have been neglected a bit until recently, understandably so. You can find some good pointers in the Codex, but the best thing to use is <a href="https://adambrown.info/p/wp_hooks">Adam Brown’s hook reference</a>, and/or look at the <a href="https://core.trac.wordpress.org/browser/tags/">source code</a>.

Say you want to add functionality to your blog that notifies authors when their work is published. To do this, you would need to do something when a post is published. So, let’s try to find a hook related to publishing.

Can we tell whether we need an action or a filter? Sure we can! When a post is published, do we want to modify its data or do a completely separate action? The answer is the latter, so we’ll need an action. Let’s go to the <a href="https://adambrown.info/p/wp_hooks/hook/actions">action reference</a> on Adam Brown’s website, and search for “Publish.”

The first thing you’ll find is <code>app_publish_post</code>. Sounds good; let’s click on it. The details page doesn’t give us a lot of info (sometimes it does), so click on the “View hook in source” link next to your version of WordPress (preferably the most recent version) in the table. This website shows only a snippet of the file, and unfortunately the beginning of the documentation is cut off, so it’s difficult to tell if this is what we need. Click on “View complete file in SVN” to go to the complete file so that we can search for our hook.

In the file I am viewing, the hook can be found in the <code>_publish_post_hook()</code> function, which — according to the documentation above it — is a “hook to schedule pings and enclosures when a post is published,” so this is not really what we need.

With some more research in the action list, you’ll find the <code>publish_post</code> hook, and this is what we need. The first thing to do is write the function that sends your email. This function will receive the post’s ID as an argument, so you can use that to pull some information into the email. The second task is to hook this function into the action. Look at the finished code below for the details.

<pre><code class="language-php">function authorNotification($post_id) {
      global $wpdb;
      $post = get_post($post_id);
      $author = get_userdata($post-&gt;post_author);

      $message = "
         Hi ".$author-&gt;display_name.",
         Your post, ".$post-&gt;post_title." has just been published. Well done! 
      ";
      wp_mail($author-&gt;user_email, "Your article is online", $message);
   }
   add_action('publish_post', 'authorNotification');</code></pre>

Notice that the function we wrote is usable in its own right. It has a very specific function, but it isn’t only usable together with hooks; you could use it in your code any time. In case you’re wondering, <code>wp_mail()</code> is an awesome mailer function — have a look at the <a href="https://codex.wordpress.org/Function_Reference/wp_mail">WordPress Codex</a> for more information.

This process might seem a bit complicated at first, and, to be totally honest, it does require browsing a bit of documentation and source code at first, but as you become more comfortable with this system, your time spent researching what to use and when to use it will be reduced to nearly nothing.</p>

## Priorities

The third parameter when adding your actions and filters is the priority. This basically designates the order in which attached hooks should run. We haven’t covered this so far, but attaching multiple functions to a hook is, of course, possible. If you want an email to be sent to an author when their post is published and to also automatically tweet the post, these would be written in two separate functions, each tied to the same tag (<code>publish_post</code>).

Priorities designate which hooked function should run first. The default value is 10, but this can be changed as needed. Priorities usually don’t make a huge difference, though. Whether the email is sent to the author before the article is tweeted or vice versa won’t make a huge difference.

In rarer cases, assigning a priority could be important. You might want to overwrite the actions of other plugins (be careful, in this case), or you might want to enforce a specific order. I recently had to overwrite functionality when I was asked to optimize a website. The website had three to four plugins, with about nine JavaScript files in total. Instead of disabling these plugins, I made my own plugin that overwrote some of the JavaScript-outputting functionality of those plugins. My plugin then added the minified JavaScript code in one file. This way, if my plugin was deactivated, all of the other plugins would work as expected.</p>

## Specifying Arguments

The fourth argument when adding filters and actions specifies how many arguments the hooked function takes. This is usually dictated by the hook itself, and you will need to look at the source to find this information.

As you know from before, your functions are run when they are called by <code>apply_filters()</code> or <code>do_action()</code>. These functions will have the tag as their first argument (i.e. the name of the hook you are plugging into) and then passed arguments as subsequent arguments.

For example, the filter <code>default_excerpt</code> receives two parameters, as seen in <em>includes/post.php</em>.

<pre><code class="language-php">$post-&gt;post_excerpt = apply_filters( 'default_excerpt', $post_excerpt, $post );</code></pre>

The arguments are well named — <code>$post_excerpt</code> and <code>$post</code> — so it’s easy to guess that the first is the excerpt text and the second is the post’s object. If you are unsure, it is usually easiest either to look further up in the source or to output them using a test function (make sure you aren’t in a production environment).

<pre><code class="language-php">function my_filter_test($post_excerpt, $post) {
      echo "&lt;pre&gt;";
         print_r($post_excerpt);
         print_r($post);
      echo "&lt;/pre&gt;";
   }
   add_filter("default_excerpt", "my_filter_test");</code></pre>

## Variable Hook Names

Remember when we looked at the <code>publish_post</code> action? In fact, this is not used anymore; it was renamed in version 2.3 to <code>{$new_status}_{$post-&gt;post_type}</code>. With the advent of custom post types, it was important to make the system flexible enough for them. This new hook now takes an arbitrary status and post type (they must exist for it to work, obviously).

As a result, <code>publish_post</code> is the correct tag to use, but in reality, you will be using <code>{$new_status}_{$post-&gt;post_type}</code>. A few of these are around; the naming usually suggests what you will need to name the action.</p>

## Who Is Hooked On Who?

To find out which function hooks into what, you can use the neat script below, <a href="https://www.wprecipes.com/list-all-hooked-wordpress-functions">courtesy of WP Recipes</a>. Use this function without arguments to get a massive list of everything, or add a tag to get functions that are hooked to that one tag. This is a great one to keep in your debugging tool belt!

<pre><code class="language-php">function list_hooked_functions($tag=false){
 global $wp_filter;
 if ($tag) {
  $hook[$tag]=$wp_filter[$tag];
  if (!is_array($hook[$tag])) {
  trigger_error("Nothing found for '$tag' hook", E_USER_WARNING);
  return;
  }
 }
 else {
  $hook=$wp_filter;
  ksort($hook);
 }
 echo '&lt;pre&gt;';
 foreach($hook as $tag =&gt; $priority){
  echo "&lt;br /&gt;&lt;strong&gt;$tag&lt;/strong&gt;&lt;br /&gt;";
  ksort($priority);
  foreach($priority as $priority =&gt; $function){
  echo $priority;
  foreach($function as $name =&gt; $properties) echo "t$name&lt;br /&gt;";
  }
 }
 echo '&lt;/pre&gt;';
 return;
}</code></pre>

## Creating Your Own Hooks

A ton of hooks are built into WordPress, but nothing is stopping you from creating your own using the functions we’ve looked at so far. This may be beneficial if you are building a complex plugin intended for wide release; it will make your and other developers’ jobs a lot easier!

In the example below, I have assumed we are building functionality for users to post short blurbs on your website’s wall. We’ll write a function to check for profanity and hook it to the function that adds the blurbs to the wall.

Look at the full code below. The explanation ensues.

<pre><code class="language-php">function post_blurb($user_id, $text) {

      $text = apply_filters("blurb_text", $text);

      if(!empty($text)) {
         $wpdb-&gt;insert('my_wall', array("user_id" =&gt; $user_id, "date" =&gt; date("Y-m-d H:i:s"), "text" =&gt; $text), array("%d", %s", "%s"));   
      }
   }

   function profanity_filter($text) {
      $text_elements = explode(" ", $text);
      $profanity = array("badword", "naughtyword", "inappropriatelanguage");

      if(array_intersect($profanity, $text_elements)) {
         return false;
      }
      else {
         return $text;
      }      
   }

   add_filter("blurb_text", "profanity_filter");</code></pre>

The first thing in the code is the designation of the function that adds the blurb. Notice that I included the <code>apply_filters()</code> function, which we will use to add our profanity check.

Next up is our profanity-checking function. This checks the text as its argument against an array of known naughty words. By using <code>array_intersect()</code>, we look for array elements that are in both arrays — these would be the profane words. If there are any, then <code>return false</code>; otherwise, return the original text.

The last part actually hooks this function into our blurb-adding script.

Now other developers can hook their own functions into our script. They could build a spam filter or a better profanity filter. All they would need to do is hook it in.</p>

## Mixing And Matching

The beauty of this system is that it uses functions for everything. If you want, you can use the same profanity filter for other purposes, even outside of WordPress, because it is just a simple function. Already have a profanity-filter function? Copy and paste it in; all you’ll need to do is add the one line that actually hooks it in. This makes functions easily reusable in various situations, giving you more flexibility and saving you some time as well.</p>

## That’s All

Hopefully, you now fully understand how the hooks system works in WordPress. It contains an important pattern that many of us could use even outside of WordPress.

This is one aspect of WordPress that does take some time getting used to if you’re coming to it without any previous knowledge. The biggest problem is usually that people get lost in all of the filters available or in finding their arguments and so on, but with some patience this can be overcome easily. Just start using them, and you’ll be a master in no time!

{{< signature "al" >}}


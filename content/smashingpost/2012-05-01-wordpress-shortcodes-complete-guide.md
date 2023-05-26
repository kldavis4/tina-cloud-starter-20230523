---
title: 'WordPress Shortcodes: A Complete Guide'
slug: wordpress-shortcodes-complete-guide
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/001fd659-fa3c-40c9-8fce-77c680833db2/shortcodeswp.jpg
date: 2012-05-01T13:55:28.000Z
author: konstantinos-kouratoras
description: >-
  WordPress shortcodes were introduced in version 2.5 and since then have proved to be one of the most useful features. The average user acting as editor has the ability to publish dynamic content using macros, without the need for programming skills.
categories:
  - WordPress
  - PHP
  - Shortcodes
  - Functions
---
When a shortcode is inserted in a WordPress post or page, it is replaced with some other content. In other words, we instruct WordPress to find the macro that is in square brackets (<code>[]</code>) and replace it with the appropriate dynamic content, which is produced by a PHP function.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [WordPress Functions To Make Blogging Easier](https://www.smashingmagazine.com/2013/06/five-wordpress-functions-blogging-easier/)
*   [Mastering WordPress Shortcodes](https://www.smashingmagazine.com/2009/02/mastering-wordpress-shortcodes/)
*   [Making A WordPress Plugin That Uses Service APIs](https://www.smashingmagazine.com/2016/03/making-a-wordpress-plugin-that-uses-service-apis/)
*   [Responsive Images Now Landed In WordPress Core](https://www.smashingmagazine.com/2015/12/responsive-images-in-wordpress-core/)

<a href="/wp-content/uploads/2012/04/shortcodes.jpg"><img loading="lazy" decoding="async" class="105422 size-full" title="Shortcodes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/875e19b3-8ce2-442c-910b-a05d00327e9f/shortcodes.jpg" alt="wordpress shortcode" width="879" height="434" /></a>

{{% feature-panel %}}

The usage is pretty simple. Let's say we want to show the most recent posts in a given post. We could use something like this:

<pre><code class="language-php">[recent-posts]</code></pre>

For a more advanced shortcode, we could set the number of posts to display by setting a parameter:

<pre><code class="language-php">[recent-posts posts="5"]</code></pre>

Going one step further, we could set a heading for the list of recent posts:

<pre><code class="language-php">[recent-posts posts="5"]Posts Heading[/recent-posts]</code></pre>

## Simple Shortcode

In the first part of this tutorial, we will create the code for this simple shortcode:

<pre><code class="language-php">[recent-posts]</code></pre>

The creation process is simple and does not require any advanced PHP knowledge. The basic steps are:

1.  Create the function, which will be called by WordPress when it finds a shortcode.
2.  Register the shortcode by setting a unique name.
3.  Tie the registration function to a WordPress action.

All codes in this tutorial can be placed in <code>functions.php</code> or in a seperate PHP file that will be included in <code>functions.php</code>.</p>

### Create the Callback Function

When a shortcode is found, it is replaced by some piece of code, which is the callback function. So, let's create a function that fetches recent posts from the database.

<pre><code class="language-php">function recent_posts_function() {
   query_posts(array('orderby' =&gt; 'date', 'order' =&gt; 'DESC' , 'showposts' =&gt; 1));
   if (have_posts()) :
      while (have_posts()) : the_post();
         $return_string = '&lt;a href="'.get_permalink().'"&gt;'.get_the_title().'&lt;/a&gt;';
      endwhile;
   endif;
   wp_reset_query();
   return $return_string;
}</code></pre>

As shown, we're querying the database to get the latest post and return a string with a link to it. Ιt is worth noting that the callback function does not print anything, but rather returns a string.</p>

### Register the Shortcode

Now, we tell WordPress that this function is a shortcode:

<pre><code class="language-php">function register_shortcodes(){
   add_shortcode('recent-posts', 'recent_posts_function');
}</code></pre>

Ιf a shortcode of <code>[recent-posts]</code> is found in a post's content, then <code>recent_posts_function()</code> is called automatically. We should ensure that the shortocode's name is unique in order to avoid conflicts.</p>

### Hook Into WordPress

In order to execute our <code>register_shortcodes()</code> function, we will tie it to WordPress' initialization action:

<pre><code class="language-php">add_action( 'init', 'register_shortcodes');</code></pre>

### Test the Shortcode

Our simple shortcode is ready, and the next step is testing that it operates properly. Let's create a new post (or open an existing one) and put the following line somewhere in the content:

<pre><code class="language-php">[recent-posts]</code></pre>

Publish the post, and viewing it in a browser, you should see a link to the most recent post on your blog, as shown in this screenshot:

<figure><a href="/wp-content/uploads/2012/04/shortcodes01.png"><img class="105423" title="Simple shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9a8a5ed-51cf-4e88-b2c4-9591b5497a81/shortcodes01.png" alt="" width="935" height="511" /></a></figure>

<em>Simple shortcode</em>

## Advanced Shortcode

### Shortcode Parameters

Shortcodes are flexible because they allow us to add parameteres in order to make them more functional. Let's say we want to display a certain number of recent posts. To do this, we need to add an extra option to our shortcode that specifies how many recent posts to show.

We have to use two functions. The first one is WordPress' built-in <code>shortcode_atts()</code> function, which combines user shortcode attributes with native attributes and fills in the defaults where needed. The second function is the <code>extract()</code> PHP function, which does what its name suggests: it extracts the shortcode attributes.

Extending our callback function, we add an argument, which is an array of attributes from which we extract the parameter for the number of posts. Then we query the database to get the desired number of posts and create an HTML list to show them.

<pre><code class="language-php">function recent_posts_function($atts){
   extract(shortcode_atts(array(
      'posts' =&gt; 1,
   ), $atts));

   $return_string = '&lt;ul&gt;';
   query_posts(array('orderby' =&gt; 'date', 'order' =&gt; 'DESC' , 'showposts' =&gt; $posts));
   if (have_posts()) :
      while (have_posts()) : the_post();
         $return_string .= '&lt;li&gt;&lt;a href="'.get_permalink().'"&gt;'.get_the_title().'&lt;/a&gt;&lt;/li&gt;';
      endwhile;
   endif;
   $return_string .= '&lt;/ul&gt;';

   wp_reset_query();
   return $return_string;
}</code></pre>

If the user skips the option, <code>1</code> is the default value. In the same way, we can add more attributes, enabling the shortcodes to accept multiple parameteres. Thanks to this enhanced function, we can set how many posts to show:

<pre><code class="language-php">[recent-posts posts="5"]</code></pre>

When viewing it in the browser, you should see links to the five most recent posts in the content:

<figure><a href="/wp-content/uploads/2012/04/shortcodes02.png"><img class="105424" title="Advanced shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70eed573-19f0-454c-a612-00c412e98e7c/shortcodes02.png" alt="" width="937" height="629" /></a></figure>

<em>Advanced shortcode</em>

### Content in Shortcode

We can take our shortcode one step further and add the ability to pass some content as an argument, which in this case will be a heading for the list of recent posts. To do this, we use a second parameter, <code>$content</code>, in the callback function and add it as an <code>h3</code> heading before the list. The new function is as follows:

<pre><code class="language-php">function recent_posts_function($atts, $content = null) {
   extract(shortcode_atts(array(
      'posts' =&gt; 1,
   ), $atts));

   $return_string = '&lt;h3&gt;'.$content.'&lt;/h3&gt;';
   $return_string .= '&lt;ul&gt;';
   query_posts(array('orderby' =&gt; 'date', 'order' =&gt; 'DESC' , 'showposts' =&gt; $posts));
   if (have_posts()) :
      while (have_posts()) : the_post();
         $return_string .= '&lt;li&gt;&lt;a href="'.get_permalink().'"&gt;'.get_the_title().'&lt;/a&gt;&lt;/li&gt;';
      endwhile;
   endif;
   $return_string .= '&lt;/ul&gt;';

   wp_reset_query();
   return $return_string;
}</code></pre>

This kind of shortcode is similar to an HTML tag. We enclose the content in an opening and closing shortcode:

<pre><code class="language-php">[recent-posts posts="5"]This is the list heading[/recent-posts]</code></pre>

The result is the same as the previous example, except for the new heading for the list of posts:

<figure><a href="/wp-content/uploads/2012/04/shortcodes03.png"><img class="105425" title="Content in shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/031c3f5a-2214-426b-a981-12193d543862/shortcodes03.png" alt="" width="934" height="644" /></a></figure>

<em>Content in shortcode</em>

## Shortcodes Anywhere, Anytime!

### Enabling Shortcodes in Widgets

By default, shortcodes are ignored in WordPress sidebar widgets. Take the following as an example:

<pre><code class="language-php">[recent-posts posts="5"]</code></pre>

If you type this shortcode into a widget, it would look something like this:

<figure><a href="/wp-content/uploads/2012/04/shortcodes04.png"><img class="105426" title="Shortcode in widget before enabling them" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afb7dbea-3c31-4d41-a79a-90cf0d1efb15/shortcodes04.png" alt="" width="938" height="647" /></a></figure>

<em>A shortcode in a widget before enabling the functionality</em>

With WordPress, we can enable this functionality with a single line of code. To be able to add shortcodes in widgets, add the following:

<pre><code class="language-php">add_filter('widget_text', 'do_shortcode');</code></pre>

Now, without having to change anything else, the shortcode will display properly in widgets:

<figure><a href="/wp-content/uploads/2012/04/shortcodes05.png"><img class="105427" title="Shortcode in widget after enabling them" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c921b391-e896-4360-9ccb-195cdf9be355/shortcodes05.png" alt="" width="942" height="641" /></a></figure>

<em>A shortcode in a widget after enabling the functionality</em>

Similarly, we can enable shortcodes in comments:

<pre><code class="language-php">add_filter( 'comment_text', 'do_shortcode' );</code></pre>

And excerpts:

<pre><code class="language-php">add_filter( 'the_excerpt', 'do_shortcode');</code></pre>

## Shortcode TinyMCE Editor Button

While shortcodes are a handy way to add dynamic content to posts, the might be a bit confusing for the average user, especially when they get complicated, with multiple parameteres. Most users are not familiar with HTML-like syntax; and yet they have to remember the exact syntax and all available attributes of shortcodes, because even a minor syntax error could cause an undesirable result.

To resovle this, we can add a button to the TinyMCE editor`s interface, enabling the user to create a shortcode with a simple click. There are two basic steps to creating this button:

1.  Create the JavaScript file for the button.
2.  Register the button and the JavaScript file.</p>

### JavaScript File for the Button

The JavaScript file is used to register the TinyMCE plugin through the <a title="" href="https://www.tinymce.com/wiki.php/API3:tinymce.api.3.x">TinyMCE API</a>. We create a new file named <code>recent-posts.js</code> in the <code>js</code> directory of our theme, and then we type the following piece of code:

<pre><code class="language-php">(function() {
   tinymce.create('tinymce.plugins.recentposts', {
      init : function(ed, url) {
         ed.addButton('recentposts', {
            title : 'Recent posts',
            image : url+'/recentpostsbutton.png',
            onclick : function() {
               var posts = prompt("Number of posts", "1");
               var text = prompt("List Heading", "This is the heading text");

               if (text != null &amp;&amp; text != ’){
                  if (posts != null &amp;&amp; posts != ’)
                     ed.execCommand('mceInsertContent', false, '[recent-posts posts="'+posts+'"]'+text+'[/recent-posts]');
                  else
                     ed.execCommand('mceInsertContent', false, '[recent-posts]'+text+'[/recent-posts]');
               }
               else{
                  if (posts != null &amp;&amp; posts != ’)
                     ed.execCommand('mceInsertContent', false, '[recent-posts posts="'+posts+'"]');
                  else
                     ed.execCommand('mceInsertContent', false, '[recent-posts]');
               }
            }
         });
      },
      createControl : function(n, cm) {
         return null;
      },
      getInfo : function() {
         return {
            longname : "Recent Posts",
            author : 'Konstantinos Kouratoras',
            authorurl : 'https://www.kouratoras.gr',
            infourl : ’,
            version : "1.0"
         };
      }
   });
   tinymce.PluginManager.add('recentposts', tinymce.plugins.recentposts);
})();</code></pre>

As shown below, we create a new plugin, calling the <code>tinymce.create()</code> method, passing in the plugin’s name and the attributes. The most important part of this code is the <code>init()</code> function, where we define a name, an icon file and an event handler for the button using the <code>onclick()</code>function.

In the first two lines of the <code>onclick()</code> function, the user is prompted to input the parameters for the number of posts and list heading of the shortcode. Then, depending on the values of these parameters, the appropriate shortcode form is inserted in the editor.

Finally, our TinyMCE plugin is added to the PluginManager using the <code>add()</code> function. Now we’ve successfully integrated the <code>[recent-posts]</code> shortcode into a WordPress theme.</p>

### Registering the Button and TinyMCE Plugin

After creating the JavaScript file, we need to register it and the shortcode button. So, we create two functions and tie them to the corresponding WordPress filters.

The first function is named <code>register_button()</code> and pushes the shortcode into the array of buttons, adding a divider between the new button and the existing ones:

<pre><code class="language-php">function register_button( $buttons ) {
   array_push( $buttons, "|", "recentposts" );
   return $buttons;
}</code></pre>

The second function, <code>add_plugin()</code>, points to the path and name of the JavaScript file:

<pre><code class="language-php">function add_plugin( $plugin_array ) {
   $plugin_array['recentposts'] = get_template_directory_uri() . '/js/recent-posts.js';
   return $plugin_array;
}</code></pre>

The next step is to add a filter with the previous functions. The <code>register_button()</code> function is tied to the <code>mce_buttons</code> filter, which is executed when the editor loads the plugins, and <code>add_plugin()</code> is tied to <code>mce_external_plugins</code> filter, which is executed when the buttons are about to be loaded:

<pre><code class="language-php">function my_recent_posts_button() {

   if ( ! current_user_can('edit_posts') &amp;&amp; ! current_user_can('edit_pages') ) {
      return;
   }

   if ( get_user_option('rich_editing') == 'true' ) {
      add_filter( 'mce_external_plugins', 'add_plugin' );
      add_filter( 'mce_buttons', 'register_button' );
   }

}</code></pre>

The previous function takes no action if the user does not have permission to edit posts or pages or if the user is not in visual editor mode.

Finally, we hook the function into WordPress' initialization action to execute this when a page loads:

<pre><code class="language-php">add_action('init', 'my_recent_posts_button');</code></pre>

### Button Usage

To check that the shortcode button functions properly, let's create a new post or edit an existing one. A new button, with the icon that we set before, should have been added to the left of the first line of the TinyMCE buttons, as in this screenshot:

<figure><a href="/wp-content/uploads/2012/04/shortcodes06.png"><img class="105428" title="Shortcode TinyMCE Editor button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bc8d3ad-a9a3-4255-a841-7e0c2e12f73d/shortcodes06.png" alt="" width="1203" height="591" /></a></figure>

<em>Shortcode TinyMCE editor button</em>

When we press the shortcode button, a dialog appears that prompts us to type the shortcode parameter for the number of posts:

<figure><a href="/wp-content/uploads/2012/04/shortcodes07.png"><img class="105429" title="Shortcode TinyMCE Editor button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71ff45ce-bc3d-4d76-9909-a10b9cafa3ed/shortcodes07.png" alt="" width="1202" height="587" /></a></figure>

<em>Shortcode TinyMCE editor button</em>

After inserting the number of posts, a second dialog appears, prompting us to type in the heading of the list:

<figure><a href="/wp-content/uploads/2012/04/shortcodes08.png"><img class="105430" title="Shortcode TinyMCE Editor button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c36781-aa9d-4375-aaaa-66b21e5d4f54/shortcodes08.png" alt="" width="1206" height="588" /></a></figure>

<em>Shortcode TinyMCE editor button</em>

If any parameter is left blank, it will not be included in the final shortcode.

Finally, the shortcode appears in the editor:

<figure><a href="/wp-content/uploads/2012/04/shortcodes09.png"><img class="105431" title="Shortcode TinyMCE Editor button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa837aeb-4a2c-435a-904e-529efce615d3/shortcodes09.png" alt="" width="1200" height="592" /></a></figure>

<em>Shortcode TinyMCE editor button</em>

## Some Useful Shortcodes

This part of the tutorial provides the source code for some userful WordPress shortcodes that will take your blog one step up.</p>

### Link Button

One simple example is the link button shortcode:

<pre><code class="language-php">function linkbutton_function( $atts, $content = null ) {
   return '&lt;button type="button"&gt;'.do_shortcode($content).'&lt;/button&gt;';
}
add_shortcode('linkbutton', 'linkbutton_function');</code></pre>

Use this shortcode as follows:

<pre><code class="language-php">[linkbutton]Click Me![/linkbutton]</code></pre>

Something like this should appear:

<figure><a href="/wp-content/uploads/2012/04/shortcodes10.png"><img class="105432" title="Link button shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/177936f3-687b-48ce-849e-8552a042f36c/shortcodes10.png" alt="" width="664" height="67" /></a></figure>

<em>Link button shortcode</em>

### WordPress Menu

Let's move on to a more complex shortcode, one that grabs a WordPress menu:

<pre><code class="language-php">function menu_function($atts, $content = null) {
   extract(
      shortcode_atts(
         array( 'name' =&gt; null, ),
         $atts
      )
   );
   return wp_nav_menu(
      array(
          'menu' =&gt; $name,
          'echo' =&gt; false
          )
   );
}
add_shortcode('menu', 'menu_function');</code></pre>

When calling this shortcode, pass in the name of the menu you want to show:

<pre><code class="language-php">[menu name="main-menu"]</code></pre>

The menu will appear in your content:

<figure><a href="/wp-content/uploads/2012/04/shortcodes14.png"><img class="105436" title="Menu shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5add006b-22ca-4da1-ba44-d593dd8e8c2f/shortcodes14.png" alt="" width="667" height="364" /></a></figure>

<em>Menu shortcode</em>

### Google Maps

A Google Maps shortcode is really useful, because we can insert a map into our content without needing to edit the source code.

<pre><code class="language-php">function googlemap_function($atts, $content = null) {
   extract(shortcode_atts(array(
      "width" =&gt; '640',
      "height" =&gt; '480',
      "src" =&gt; ’
   ), $atts));
   return '&lt;iframe width="'.$width.'" height="'.$height.'" src="'.$src.'&amp;output=embed" &gt;&lt;/iframe&gt;';
}
add_shortcode("googlemap", "googlemap_function");</code></pre>

When typing the shortcode, pass in the width and height and the link from Google Maps as parameters:

<pre><code class="language-php">[googlemap width="600" height="300" src="https://maps.google.com/maps?q=Heraklion,+Greece&amp;hl=en&amp;ll=35.327451,25.140495&amp;spn=0.233326,0.445976&amp; sll=37.0625,-95.677068&amp;sspn=57.161276,114.169922&amp; oq=Heraklion&amp;hnear=Heraklion,+Greece&amp;t=h&amp;z=12"]</code></pre>

The result is the following:

<figure><a href="/wp-content/uploads/2012/04/shortcodes11.png"><img class="105433" title="Google Maps shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63717672-d716-4d8e-8f45-a12b2bd4eb5e/shortcodes11.png" alt="" width="617" height="316" /></a></figure>

<em>Google Maps shortcode</em>

### Google Charts

Another useful service is Google Charts, because it is very customizable. Here is a shortcode example with multiple attributes:

<pre><code class="language-php">function chart_function( $atts ) {
   extract(shortcode_atts(array(
       'data' =&gt; ’,
       'chart_type' =&gt; 'pie',
       'title' =&gt; 'Chart',
       'labels' =&gt; ’,
       'size' =&gt; '640x480',
       'background_color' =&gt; 'FFFFFF',
       'colors' =&gt; ’,
   ), $atts));

   switch ($chart_type) {
      case 'line' :
         $chart_type = 'lc';
         break;
      case 'pie' :
         $chart_type = 'p3';
         break;
      default :
         break;
   }

   $attributes = ’;
   $attributes .= '&amp;chd=t:'.$data.’;
   $attributes .= '&amp;chtt='.$title.’;
   $attributes .= '&amp;chl='.$labels.’;
   $attributes .= '&amp;chs='.$size.’;
   $attributes .= '&amp;chf='.$background_color.’;
   $attributes .= '&amp;chco='.$colors.’;

   return '&lt;img title="'.$title.'" src="https://chart.apis.google.com/chart?cht='.$chart_type.’.$attributes.'" alt="'.$title.'" /&gt;';
}
add_shortcode('chart', 'chart_function');</code></pre>

To create a pie chart with four types of data, we insert the following line:

<pre><code class="language-php">[chart type="pie" title="Example Pie Chart" data="41.12,32.35,21.52,5.01" labels="First+Label|Second+Label|Third+Label|Fourth+Label" background_color="FFFFFF" colors="D73030,329E4A,415FB4,DFD32F" size="450x180"]</code></pre>

The result is a pie like the following:

<figure><a href="/wp-content/uploads/2012/04/shortcodes12.png"><img class="105434" title="Google Charts shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ce09035-b468-47c5-989e-5631b820cd91/shortcodes12.png" alt="" width="457" height="230" /></a></figure>

<em>Google Charts shortcode</em>

### PDF embedding

We can use the Google Docs PDF viewer to embed a PDF on your website. Here is the shortcode to do this:

<pre><code class="language-php">function pdf_function($attr, $url) {
   extract(shortcode_atts(array(
       'width' =&gt; '640',
       'height' =&gt; '480'
   ), $attr));
   return '&lt;iframe src="https://docs.google.com/viewer?url=' . $url . '&amp;embedded=true" style="width:' .$width. '; height:' .$height. ';"&gt;Your browser does not support iframes&lt;/iframe&gt;';
}
add_shortcode('pdf', 'pdf_function');</code></pre>

To embed a PDF, type the shortcode <code>[pdf]</code>, and pass in the URL as the content argument:

<pre><code class="language-php">[pdf width="520px" height="700px"]https://static.fsf.org/common/what-is-fs-new.pdf[/pdf]</code></pre>

When viewing the page, the visitor will see a viewer with the PDF:

<figure><a href="/wp-content/uploads/2012/04/shortcodes13.png"><img class="105435" title="PDF embed shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81c09168-c9e1-45d0-87c0-c7e42d0654d9/shortcodes13.png" alt="" width="530" height="716" /></a></figure>

<em>PDF embedding shortcode</em>

## Shortcodes WordPress Plugins

Thanks to WordPress plugins, adding shortcode functionality to a website requires no source-code editing at all. If you look at the <a title="WordPress Plugins Directory" href="https://wordpress.org/extend/plugins/">WordPress plugins directory</a>, you'll see a large number of such plugins with which to style posts and pages. In this section, we'll recommend some of the best shortcode plugins (favoring the free ones) to satisfy your every need.</p>

### Shortcodes Ultimate

Without a doubt, this is the best shortcode plugin out there. It enables you to easily create buttons, tabs, boxes, sliders, tooltips and many more elements.

<figure><a href="/wp-content/uploads/2012/04/shortcodes15.png"><img class="105437" title="Shortcodes Ultimate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf0cb518-b7df-4dbe-9501-556715a8e2b4/shortcodes15.png" alt="" width="530" height="941" /></a></figure>

<a title="Shortcodes Ultimate" href="https://wordpress.org/extend/plugins/shortcodes-ultimate/">Shortcodes Ultimate</a>

### J Shortcodes

The J Shortcodes plugin is similar to Shortcodes Ultimate, offering a collection of useful elements to style a website, including buttons, boxes, tabs and accordions. J Shortcodes lets you set custom attributes on elements, such as color, size and shape, and define custom column layouts on any page or post.

<figure><a href="/wp-content/uploads/2012/04/shortcodes16.png"><img class="105438" title="J Shortcodes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/766b9630-d3b8-4a6b-9913-3192d25cc546/shortcodes16.png" alt="" width="1021" height="793" /></a></figure>

<a title="J Shortcodes" href="https://wordpress.org/extend/plugins/j-shortcodes/">J Shortcodes</a>

<figure><a href="/wp-content/uploads/2012/04/shortcodes18.png"><img class="105440" title="Shortcode Exec PHP" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cec91eb7-5c74-41f0-b531-479e55029131/shortcodes18.png" alt="" width="500" height="581" /></a></figure>

## Resources From Around the Web

<pre><code class="language-php">function register_button( $buttons ) {
   array_push( $buttons, "|", "recentposts" );
   return $buttons;
}</code></pre>

The second function, <code>add_plugin()</code>, points to the path and name of the JavaScript file:

<pre><code class="language-php">function add_plugin( $plugin_array ) {
   $plugin_array['recentposts'] = get_template_directory_uri() . '/js/recent-posts.js';
   return $plugin_array;
}</code></pre>

The next step is to add a filter with the previous functions. The <code>register_button()</code> function is tied to the <code>mce_buttons</code> filter, which is executed when the editor loads the plugins, and <code>add_plugin()</code> is tied to <code>mce_external_plugins</code> filter, which is executed when the buttons are about to be loaded:

<pre><code class="language-php">function my_recent_posts_button() {

   if ( ! current_user_can('edit_posts') &amp;&amp; ! current_user_can('edit_pages') ) {
      return;
   }

   if ( get_user_option('rich_editing') == 'true' ) {
      add_filter( 'mce_external_plugins', 'add_plugin' );
      add_filter( 'mce_buttons', 'register_button' );
   }

}</code></pre>

The previous function takes no action if the user does not have permission to edit posts or pages or if the user is not in visual editor mode.

Finally, we hook the function into WordPress' initialization action to execute this when a page loads:

<pre><code class="language-php">add_action('init', 'my_recent_posts_button');</code></pre>

### Button Usage

To check that the shortcode button functions properly, let's create a new post or edit an existing one. A new button, with the icon that we set before, should have been added to the left of the first line of the TinyMCE buttons, as in this screenshot:

<figure><a href="/wp-content/uploads/2012/04/shortcodes06.png"><img class="105428" title="Shortcode TinyMCE Editor button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bc8d3ad-a9a3-4255-a841-7e0c2e12f73d/shortcodes06.png" alt="" width="1203" height="591" /></a></figure>

<em>Shortcode TinyMCE editor button</em>

When we press the shortcode button, a dialog appears that prompts us to type the shortcode parameter for the number of posts:

<figure><a href="/wp-content/uploads/2012/04/shortcodes07.png"><img class="105429" title="Shortcode TinyMCE Editor button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71ff45ce-bc3d-4d76-9909-a10b9cafa3ed/shortcodes07.png" alt="" width="1202" height="587" /></a></figure>

<em>Shortcode TinyMCE editor button</em>

After inserting the number of posts, a second dialog appears, prompting us to type in the heading of the list:

<figure><a href="/wp-content/uploads/2012/04/shortcodes08.png"><img class="105430" title="Shortcode TinyMCE Editor button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c36781-aa9d-4375-aaaa-66b21e5d4f54/shortcodes08.png" alt="" width="1206" height="588" /></a></figure>

<em>Shortcode TinyMCE editor button</em>

If any parameter is left blank, it will not be included in the final shortcode.

Finally, the shortcode appears in the editor:

<figure><a href="/wp-content/uploads/2012/04/shortcodes09.png"><img class="105431" title="Shortcode TinyMCE Editor button" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa837aeb-4a2c-435a-904e-529efce615d3/shortcodes09.png" alt="" width="1200" height="592" /></a></figure>

<em>Shortcode TinyMCE editor button</em>

## Some Useful Shortcodes

This part of the tutorial provides the source code for some userful WordPress shortcodes that will take your blog one step up.</p>

### Link Button

One simple example is the link button shortcode:

<pre><code class="language-php">function linkbutton_function( $atts, $content = null ) {
   return '&lt;button type="button"&gt;'.do_shortcode($content).'&lt;/button&gt;';
}
add_shortcode('linkbutton', 'linkbutton_function');</code></pre>

Use this shortcode as follows:

<pre><code class="language-php">[linkbutton]Click Me![/linkbutton]</code></pre>

Something like this should appear:

<figure><a href="/wp-content/uploads/2012/04/shortcodes10.png"><img class="105432" title="Link button shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/177936f3-687b-48ce-849e-8552a042f36c/shortcodes10.png" alt="" width="664" height="67" /></a></figure>

<em>Link button shortcode</em>

### WordPress Menu

Let's move on to a more complex shortcode, one that grabs a WordPress menu:

<pre><code class="language-php">function menu_function($atts, $content = null) {
   extract(
      shortcode_atts(
         array( 'name' =&gt; null, ),
         $atts
      )
   );
   return wp_nav_menu(
      array(
          'menu' =&gt; $name,
          'echo' =&gt; false
          )
   );
}
add_shortcode('menu', 'menu_function');</code></pre>

When calling this shortcode, pass in the name of the menu you want to show:

<pre><code class="language-php">[menu name="main-menu"]</code></pre>

The menu will appear in your content:

<figure><a href="/wp-content/uploads/2012/04/shortcodes14.png"><img class="105436" title="Menu shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5add006b-22ca-4da1-ba44-d593dd8e8c2f/shortcodes14.png" alt="" width="667" height="364" /></a></figure>

<em>Menu shortcode</em>

### Google Maps

A Google Maps shortcode is really useful, because we can insert a map into our content without needing to edit the source code.

<pre><code class="language-php">function googlemap_function($atts, $content = null) {
   extract(shortcode_atts(array(
      "width" =&gt; '640',
      "height" =&gt; '480',
      "src" =&gt; ’
   ), $atts));
   return '&lt;iframe width="'.$width.'" height="'.$height.'" src="'.$src.'&amp;output=embed" &gt;&lt;/iframe&gt;';
}
add_shortcode("googlemap", "googlemap_function");</code></pre>

When typing the shortcode, pass in the width and height and the link from Google Maps as parameters:

<pre><code class="language-php">[googlemap width="600" height="300" src="https://maps.google.com/maps?q=Heraklion,+Greece&amp;hl=en&amp;ll=35.327451,25.140495&amp;spn=0.233326,0.445976&amp; sll=37.0625,-95.677068&amp;sspn=57.161276,114.169922&amp; oq=Heraklion&amp;hnear=Heraklion,+Greece&amp;t=h&amp;z=12"]</code></pre>

The result is the following:

<figure><a href="/wp-content/uploads/2012/04/shortcodes11.png"><img class="105433" title="Google Maps shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63717672-d716-4d8e-8f45-a12b2bd4eb5e/shortcodes11.png" alt="" width="617" height="316" /></a></figure>

<em>Google Maps shortcode</em>

### Google Charts

Another useful service is Google Charts, because it is very customizable. Here is a shortcode example with multiple attributes:

<pre><code class="language-php">function chart_function( $atts ) {
   extract(shortcode_atts(array(
       'data' =&gt; ’,
       'chart_type' =&gt; 'pie',
       'title' =&gt; 'Chart',
       'labels' =&gt; ’,
       'size' =&gt; '640x480',
       'background_color' =&gt; 'FFFFFF',
       'colors' =&gt; ’,
   ), $atts));

   switch ($chart_type) {
      case 'line' :
         $chart_type = 'lc';
         break;
      case 'pie' :
         $chart_type = 'p3';
         break;
      default :
         break;
   }

   $attributes = ’;
   $attributes .= '&amp;chd=t:'.$data.’;
   $attributes .= '&amp;chtt='.$title.’;
   $attributes .= '&amp;chl='.$labels.’;
   $attributes .= '&amp;chs='.$size.’;
   $attributes .= '&amp;chf='.$background_color.’;
   $attributes .= '&amp;chco='.$colors.’;

   return '&lt;img title="'.$title.'" src="https://chart.apis.google.com/chart?cht='.$chart_type.’.$attributes.'" alt="'.$title.'" /&gt;';
}
add_shortcode('chart', 'chart_function');</code></pre>

To create a pie chart with four types of data, we insert the following line:

<pre><code class="language-php">[chart type="pie" title="Example Pie Chart" data="41.12,32.35,21.52,5.01" labels="First+Label|Second+Label|Third+Label|Fourth+Label" background_color="FFFFFF" colors="D73030,329E4A,415FB4,DFD32F" size="450x180"]</code></pre>

The result is a pie like the following:

<figure><a href="/wp-content/uploads/2012/04/shortcodes12.png"><img class="105434" title="Google Charts shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ce09035-b468-47c5-989e-5631b820cd91/shortcodes12.png" alt="" width="457" height="230" /></a></figure>

<em>Google Charts shortcode</em>

### PDF embedding

We can use the Google Docs PDF viewer to embed a PDF on your website. Here is the shortcode to do this:

<pre><code class="language-php">function pdf_function($attr, $url) {
   extract(shortcode_atts(array(
       'width' =&gt; '640',
       'height' =&gt; '480'
   ), $attr));
   return '&lt;iframe src="https://docs.google.com/viewer?url=' . $url . '&amp;embedded=true" style="width:' .$width. '; height:' .$height. ';"&gt;Your browser does not support iframes&lt;/iframe&gt;';
}
add_shortcode('pdf', 'pdf_function');</code></pre>

To embed a PDF, type the shortcode <code>[pdf]</code>, and pass in the URL as the content argument:

<pre><code class="language-php">[pdf width="520px" height="700px"]https://static.fsf.org/common/what-is-fs-new.pdf[/pdf]</code></pre>

When viewing the page, the visitor will see a viewer with the PDF:

<figure><a href="/wp-content/uploads/2012/04/shortcodes13.png"><img class="105435" title="PDF embed shortcode" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81c09168-c9e1-45d0-87c0-c7e42d0654d9/shortcodes13.png" alt="" width="530" height="716" /></a></figure>

<em>PDF embedding shortcode</em>

## Shortcodes WordPress Plugins

Thanks to WordPress plugins, adding shortcode functionality to a website requires no source-code editing at all. If you look at the <a title="WordPress Plugins Directory" href="https://wordpress.org/extend/plugins/">WordPress plugins directory</a>, you'll see a large number of such plugins with which to style posts and pages. In this section, we'll recommend some of the best shortcode plugins (favoring the free ones) to satisfy your every need.</p>

### Shortcodes Ultimate

Without a doubt, this is the best shortcode plugin out there. It enables you to easily create buttons, tabs, boxes, sliders, tooltips and many more elements.

<figure><a href="/wp-content/uploads/2012/04/shortcodes15.png"><img class="105437" title="Shortcodes Ultimate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf0cb518-b7df-4dbe-9501-556715a8e2b4/shortcodes15.png" alt="" width="530" height="941" /></a></figure>

<a title="Shortcodes Ultimate" href="https://wordpress.org/extend/plugins/shortcodes-ultimate/">Shortcodes Ultimate</a>

### J Shortcodes

The J Shortcodes plugin is similar to Shortcodes Ultimate, offering a collection of useful elements to style a website, including buttons, boxes, tabs and accordions. J Shortcodes lets you set custom attributes on elements, such as color, size and shape, and define custom column layouts on any page or post.

<figure><a href="/wp-content/uploads/2012/04/shortcodes16.png"><img class="105438" title="J Shortcodes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/766b9630-d3b8-4a6b-9913-3192d25cc546/shortcodes16.png" alt="" width="1021" height="793" /></a></figure>

<a title="J Shortcodes" href="https://wordpress.org/extend/plugins/j-shortcodes/">J Shortcodes</a>

<figure><a href="/wp-content/uploads/2012/04/shortcodes18.png"><img class="105440" title="Shortcode Exec PHP" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cec91eb7-5c74-41f0-b531-479e55029131/shortcodes18.png" alt="" width="500" height="581" /></a></figure>

## Resources From Around the Web

Last but not least, here are some articles you might find useful.

*   "[Mastering WordPress Shortcodes](/2009/02/02/mastering-wordpress-shortcodes/ "Mastering WordPress Shortcodes")," Smashing Magazine A great article that shows how to create and use shortcodes, providing some ready-to-use WordPress shortcodes.
*   "[Getting Started with WordPress Shortcodes (+Examples)](https://speckyboy.com/2011/07/18/getting-started-with-wordpress-shortcodes-examples/ "Getting Started with WordPress Shortcodes (+Examples)")," SpeckyBoy This tutorial is a good place to start messing with shortcodes.
*   "[Getting Started With WordPress Shortcodes](https://wp.tutsplus.com/tutorials/getting-started-with-wordpress-shortcodes/ "Getting Started With WordPress Shortcodes")," Tuts+ This gives a detailed explanation of the WordPress shortcode API, showing some useful examples of more advanced shortcodes.
*   "[Shortcode API](https://codex.wordpress.org/Shortcode_API "WordPress Codex - Shortcode API")," WordPress Codex The official page of the API in the WordPress Codex.
*   "[Shortcodes](https://en.support.wordpress.com/shortcodes/ "WordPress Support - Shortcodes")," WordPress Support Lists some useful built-in shorcodes.

{{< signature "al" >}}


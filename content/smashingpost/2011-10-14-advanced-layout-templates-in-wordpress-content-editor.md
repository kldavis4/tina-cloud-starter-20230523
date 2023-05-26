---
title: Advanced Layout Templates In WordPress' Content Editor
slug: advanced-layout-templates-in-wordpress-content-editor
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ac44f6f-52af-4405-94e7-f575de488908/multi-col-layout-featured-5501.png
date: 2011-10-14T14:04:47.000Z
author: david-hansen
description: >-
  As a Web designer, I often find myself building WordPress-based websites that
  will ultimately be updated and maintained by clients who have little to no
  experience working with HTML. While the TinyMCE rich-text editor is great for
  giving Web content managers of any skill level the tools they need to easily
  style and publish their posts to a degree, creating anything beyond a single
  column of text with a few floated images generally requires at least a basic
  understanding of HTML.
categories:
  - WordPress
  - Techniques
  - Templates
---
As a Web designer, I often find myself building WordPress-based websites that will ultimately be updated and maintained by clients who have little to no experience working with HTML. While the TinyMCE rich-text editor is great for giving Web content managers of any skill level the tools they need to easily style and publish their posts to a degree, creating anything beyond a single column of text with a few floated images generally requires at least a basic understanding of HTML.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/358e0a5c-ef2b-481c-97ba-228d7cf4b6f1/multi-col-layout-featured-550.png" alt="multi-col-layout-featured" width="550" height="315" />

This article shows you an easy-to-implement trick that enables even the least tech-savvy of clients to manage multi-column content layouts within the comfort of the WYSIWIG editor. And for you advanced users, it’s still a great way to standardize and streamline your content entry.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Power Tips For WordPress Template Developers](https://www.smashingmagazine.com/2009/07/power-tips-for-wordpress-template-developers/)
*   [A Detailed Guide To WordPress Custom Page Templates](https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/)
*   [How To Create And Customize A WordPress Child Theme](https://www.smashingmagazine.com/2016/01/create-customize-wordpress-child-theme/)
*   [How To Make WordPress Hard For Clients To Mess Up](https://www.smashingmagazine.com/2016/07/how-to-make-wordpress-hard-for-clients-to-mess-up/)

{{% feature-panel %}}

## Creating A Custom Layout

All we’re really going to do here is inject a few HTML elements into the editing window and style them. WordPress’ <code>default_content</code> filter allows us to insert set content into any post as soon as it’s created so that our clients don’t have to. This filter is also great for adding boilerplate text to posts.</p>

### The Back End

By adding the following to <em>functions.php</em>, each new post we create will come pre-stocked with two divs, classed <code>content-col-main</code> and <code>content-col-side</code>, respectively. I should note now that this code has been tested only in WordPress version 3.0 and up:

<pre><code class="language-php">&lt;?php
   add_filter( 'default_content', 'custom_editor_content' );
   function custom_editor_content( $content ) {
   $content = '
      &lt;div class="content-col-main"&gt;

      This is your main page content

      &amp;nbsp;

      &lt;/div&gt;
      &lt;div class="content-col-side"&gt;

      This is your sidebar content

       &amp;nbsp;

      &lt;/div&gt;    
   ';
   return $content;
   }
?&gt;</code></pre>

A couple of things to note:

*   The `default_content` filter is fired only when a new post is created; any posts or pages that existed before you added this code will not receive this content.
*   The line spacing and additional `&nbsp;` are not essential, but I’ve found them to be useful for preventing a few of TinyMCE’s little quirks.

Now we just need to give it some style. Add the following to <em>functions.php</em>:

<pre><code class="language-php">&lt;?php
   add_editor_style( 'editor-style.css' );
?&gt;</code></pre>

The <code>add_editor_style()</code> function looks for the specified style sheet and applies any CSS it contains to the content in our TinyMCE editing window. If you don’t specify the name of a style sheet, it will look for <em>editor-style.css</em> by default, but for the purpose of this article, I’ve written it out. Create a style sheet named <em>editor-style.css</em>, and place it in the theme folder, with the following styles:

<pre><code class="language-css">body {
   background: #f5f5f5;
}

.content-col-main {
   float:left;
   width:66%;
   padding:1%;
   border: 1px dotted #ccc;
   background: #fff;
}

.content-col-side {
   float:right;
   width:29%;
   padding:1%;
   border: 1px dotted #ccc;
   background: #fff;
}

img { /* Makes sure your images stay within their columns */
   max-width: 100%;
   width: auto;
   height: auto;
}</code></pre>

Now, when you create a new post, you will see two columns that you can type or paste your content into:

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="103849" title="multi-col-layout-01" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de368537-c760-4836-a9c8-d46b8c3f0823/multi-col-layout-01.png" alt="Example of a multi-column template in WordPress’ TinyMCE editor" width="550" height="294" /><br>
<em>This basic multi-column template will now appear any time you create a new page or post.</em>

And there you have it: a simple multi-column template in your content editor. You can go back and edit the <code>default_content</code> and <em>editor-styles.css</em> to adapt the content layout to your needs:

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="103850" title="multi-col-layout-02" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5ea8d89-9349-4418-8fcf-44bebd7b127f/multi-col-layout-02.png" alt="Example of an advanced multi-column template in WordPress’ TinyMCE editor" width="550" height="575" /><br>
<em>Use this technique to create your own layout templates, customized to your content.</em>

### The Front End

When your post is displayed on the front end of the website, the content will still appear in a single column, as before. The styles you wrote out in <em>editor-style.css</em> do not get passed to the front end of the website. However, by viewing the page source, you’ll see that the divs we created with our <code>custom_editor_content()</code> function have been passed through and are wrapping the different sections of the content. Simply open <em>style.css</em> (or whatever style sheet you’re using for your theme) and style to your heart’s desire.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="103851" title="multi-col-layout-03" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/976c613d-63e5-4279-a0b7-5e13869823d9/multi-col-layout-03.png" alt="Example of a WordPress post designed with a customized multi-column layout" width="550" height="417" /><br>
<em>This technique applies not only to the visual layout of content. Use JavaScript to target specific containers to make on-the-fly slideshows and other dynamic effects.</em>

### Get More From Your Templates

Beyond just opening up new styling possibilities, this technique can also be used to create objects to target later with JavaScript.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="103852" title="multi-col-layout-04" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01ba7790-c884-441d-83d9-1a4641091c42/multi-col-layout-04.png" alt="Example of a WordPress advanced layout post using different sections for Javascript-enabled tabs" width="550" height="507" />

In the example above, we were able to turn a series of content areas into more easily digestible tabbed sections for the user, while still allowing the administrator to update all of the information on one page. These are just a few of the many ways you can take your WordPress templates further.</p>

## Templates For Templates

The code above will simply apply the same layout and styling to all of your posts, pages, custom posts… anywhere the TinyMCE editor appears. This is probably not ideal. By adding conditional statements to the <code>custom_editor_content()</code> function above, you can serve a different default layout template to each of your post types:

<pre><code class="language-php">&lt;?php
   add_filter( 'default_content', 'custom_editor_content' );
      function custom_editor_content( $content ) {
         global $current_screen;
         if ( $current_screen-&gt;post_type == 'page') {
            $content = '

               // TEMPLATE FOR YOUR PAGES

            ';
         }
         elseif ( $current_screen-&gt;post_type == 'POSTTYPE') {
            $content = '

                // TEMPLATE FOR YOUR CUSTOM POST TYPE

            ';
         }
         else {
            $content = '

               // TEMPLATE FOR EVERYTHING ELSE

            ';
         }
         return $content;
       }
?&gt;</code></pre>

You can style all of your default content elements in the <em>editor-style.css</em> file, but if you’d like to use a different style sheet entirely for each post type, you can do so with this snippet <a href="https://wpstorm.net/2010/04/editor-styles-custom-post-types-wordpress-3-0/">from WPStorm</a>:

<pre><code class="language-php">&lt;?php
   function custom_editor_style() {
      global $current_screen;
      switch ($current_screen-&gt;post_type) {
         case 'post':
         add_editor_style('editor-style-post.css');
         break;
         case 'page':
         add_editor_style('editor-style-page.css');
         break;
         case '[POSTTYPE]':
         add_editor_style('editor-style-[POSTTYPE].css');
         break;
      }
   }
   add_action( 'admin_head', 'custom_editor_style' );
?&gt;</code></pre>

Add the above to your <em>functions.php</em> file, and then create the <em>editor-style-[POSTTYPE].css</em> files to use different style sheets for the corresponding post types. Just replace <em>[POSTTYPE]</em> with the name of your custom post type. Extend the code above by adding new cases for each additional post type.

Alternatively, you could use the following code to automatically look for a style sheet named <em>editor-style-</em> followed by the name of the post type that you’re currently editing. Again, just make sure that the suffix of the new style sheet you create matches exactly the name of the post type.

<pre><code class="language-php">&lt;?php
 function custom_editor_style() {
   global $current_screen;
   add_editor_style(
   array(
      'editor-style.css',
      'editor-style-'.$current_screen-&gt;post_type.'.css'
    )
   );
 }

 add_action( 'admin_head', 'custom_editor_style' );
?&gt;</code></pre>

(In this snippet, <em>editor-style.css</em> will also be included on <em>all</em> post-editing pages, in addition to the style sheet that is specific to that post type, which will be named <em>editor-style-[POSTTYPE].css</em>.)

## Conclusion

While this method does have its drawbacks — it assumes you already know the layout that your client wants to give their content, and the layout structures cannot be easily edited by the client themselves — it does enable you to create more interesting sandboxes for your client to play in, while encouraging a standardized format for the content.

If the client decides they don’t want to use a pre-defined container for a particular post, they can simply click inside the container and hit Backspace until all the content is gone, and then hit Backspace once more, and TinyMCE will delete the div wrapper, leaving a clean slate for them to work with.

I hope you’ve found this little technique useful. I’m excited to see all of the ways you guys will customize and improve it for more dynamic layouts.</p>

### Additional Resources

*   “[Editor Styles for Custom Post Types in WordPress 3.0](https://wpstorm.net/2010/04/editor-styles-custom-post-types-wordpress-3-0/),” WPStorm
*   “[Killer Hacks to Enhance WordPress Editor](https://www.catswhocode.com/blog/killer-hacks-to-enhance-wordpress-editor)” Jean-Baptiste Jung
*   “[Custom Post Types in WordPress](https://justintadlock.com/archives/2010/04/29/custom-post-types-in-wordpress),” Justin Tadlock
*   “[New WordPress Power Tips for Template Developers and Consultants](https://www.smashingmagazine.com/2011/05/10/new-wordpress-power-tips-for-template-developers-and-consultants/),” Jacob Goldman

{{< signature "al" >}}


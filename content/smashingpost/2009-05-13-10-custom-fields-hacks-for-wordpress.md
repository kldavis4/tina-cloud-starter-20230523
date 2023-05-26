---
title: Custom Fields Hacks For WordPress
slug: 10-custom-fields-hacks-for-wordpress
image: null
date: 2009-05-13T08:22:00.000Z
author: jean-baptiste-jung
description: >-
  In our previous articles on WordPress hacks, we discussed the incredible flexibility of WordPress, which is one of the biggest reasons for its popularity among bloggers worldwide. **Custom fields** in particular, which let users create variables and add custom values to them, are one of the reasons for WordPress' flexibility.
categories:
  - WordPress
  - Hacks
  - Custom Fields
  - Techniques (WP)
---
In this article, we've compiled a list of <strong>10 useful things that you can do with custom fields in WordPress</strong>. Among them are setting expiration time for posts, defining how blog posts are displayed on the front page, displaying your mood or music, embedding custom CSS styles, disabling search engine indexing for individual posts, inserting a “Digg this” button only when you need it and, of course, displaying thumbnails next to your posts

## 1\. Set An Expiration Time For Posts

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00a9a85a-4ac6-4a6d-a50d-b4cd2082fc28/sm2.jpg" alt="Screenshot" /><br>
<em>Image source: <a href="https://www.ludimaginary.net/photograph-219.html">Richard Vantielcke</a></em>

{{% feature-panel %}}

<strong>The problem.</strong> Sometimes (for example, if you're running a contest), you want to be able to publish a post and then automatically stop displaying it after a certain date. This may seem quite hard to do but in fact is not, using the power of custom fields.

<strong>The solution.</strong> Edit your theme and replace your current WordPress loop with this "hacked" loop:

<pre><code class="language-php">&lt;?php
if (have_posts()) :
     while (have_posts()) : the_post(); ?&gt;
         $expirationtime = get_post_custom_values('expiration');
         if (is_array($expirationtime)) {
             $expirestring = implode($expirationtime);
         }

         $secondsbetween = strtotime($expirestring)-time();
         if ( $secondsbetween &gt; 0 ) {
             // For example...
             the_title();
             the_excerpt();
         }
     endwhile;
endif;
?&gt;</code></pre>

To create a post set to expire at a certain date and time, just create a custom field. Specify <em>expiration</em> as a key and your date and time as a value (with the format <strong>mm/dd/yyyy 00:00:00</strong>). The post will not show up after the time on that stamp.

<strong>Code explanation.</strong> This code is simply a custom WordPress loop that automatically looks to see if a custom field called <em>expiration</em> is present. If one is, its value is compared to the current date and time.

If the current date and time is equal to or earlier than the value of the custom <em>expiration</em> field, then the post is not displayed.

Note that this code does not remove or unpublish your post, but just prevents it from being displayed in the loop.

<strong>Source:</strong>

*   [How to: Set a post's expiration date and time on your WordPress blog](https://www.wprecipes.com/how-to-set-post-expiration-datetime-on-your-wordpress-blog)

## 2\. Define How Blog Posts Are Displayed On The Home Page

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a68763f5-0344-427e-892d-f4d103b226ef/sm3.jpg" alt="Screenshot" />

<strong>The problem.</strong> I've always wondered why 95% of bloggers displays <em>all</em> of their posts the same way on their home page. Sure, WordPress has no built-in option to let you define how a post is displayed. But wait: with custom fields, we can do it easily.

<strong>The solution.</strong> The following hack lets you define how a post is displayed on your home page. Two values are possible:

*   Full post
*   Post excerpt only

Once more, we'll use a custom WordPress loop. Find the loop in your <em>index.php</em> file and replace it with the following code:

<pre><code class="language-php">&lt;?php if (have_posts()) :
    while (have_posts()) : the_post();
         $customField = get_post_custom_values("full");
         if (isset($customField[0])) {
              //Custom field is set, display a full post
              the_title();
              the_content();
         } else {
              // No custom field set, let's display an excerpt
              the_title();
              the_excerpt();
    endwhile;
endif;
?&gt;</code></pre>

In this code, excerpts are displayed by default. To show full posts on your home page, simply edit the post and create a custom field called <em>full</em> and give it any value.

<strong>Code explanation.</strong> This code is rather simple. The first thing it does is look for a custom field called <em>full</em>. If this custom field is set, full posts are displayed. Otherwise, only excerpts are shown.

<strong>Source:</strong>

*   [How to: Manually define whether to show full posts or excerpts on your home page](https://www.wprecipes.com/how-to-manually-define-to-show-full-post-or-excerpt-on-your-homepage)

## 3\. Display Your Mood Or The Music You're Listening To

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/158c93cf-eb69-4a41-9f76-7e6f0850644b/sm4.jpg" alt="Screenshot" />

<strong>The problem.</strong> About five or six years ago, I was blogging on a platform called LiveJournal. Of course it wasn't great as WordPress, but it had nice features that WordPress doesn't have. For example, it allowed users to display their current mood and the music they were listening to while blogging.

Even though I wouldn't use this feature on my blog, I figure many bloggers would be interested in knowing how to do this in WordPress.

<strong>The solution.</strong> Open your <em>single.php</em> file (or modify your <em>index.php</em> file), and paste the following code anywhere within the loop:

<pre><code class="language-php">$customField = get_post_custom_values("mood");
if (isset($customField[0])) {
    echo "Mood: ".$customField[0];
}</code></pre>

Save the file. Now, when you write a new post, just create a custom field called <em>mood</em>, and type in your current mood as the value.

<strong>Code explanation.</strong> This is a very basic use of custom fields, not all that different from the well-known hack for displaying thumbnails beside your posts' excerpts on the home page. It looks for a custom field called <em>mood</em>. If the field is found, its value is displayed.

<strong>Source:</strong>

*   [How to: Display your current mood on your posts](https://www.wprecipes.com/how-to-display-your-current-mood-on-your-posts)

## 4\. Add Meta Descriptions To Your Posts

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff56b353-1996-4df8-8bfd-e74277b87d5d/sm5.png" alt="Screenshot" />

<strong>The problem.</strong> WordPress, surprisingly, does not use meta description tags by default.

Sure, for SEO, meta tags are not as important as they used to be. Yet still, they can enhance your blog's search engine ranking nevertheless.

How about using custom fields to create meta description tags for individual posts?

<strong>The solution.</strong> Open your <em>header.php</em> file. Paste the following code anywhere within the &lt;head&gt; and &lt;/head&gt; tags:

<pre><code class="language-php">&lt;meta name="description" content="
&lt;?php if ( (is_home()) || (is_front_page()) ) {
    echo ('Your main description goes here');
} elseif(is_category()) {
    echo category_description();
} elseif(is_tag()) {
    echo '-tag archive page for this blog' . single_tag_title();
} elseif(is_month()) {
    echo 'archive page for this blog' . the_time('F, Y');
} else {
    echo get_post_meta($post-&gt;ID, "Metadescription", true);
}?&gt;"&gt;</code></pre>

<strong>Code explanation.</strong> To generate meta descriptions, this hack makes extensive use of WordPress conditional tags to determine which page the user is on.

For category pages, tag pages, archives and the home page, a static meta description is used. Edit lines 3, 7 and 9 to define your own. For posts, the code looks for a custom field called <em>Metadescription</em> and use its value for the meta description.

<strong>Sources:</strong>

*   [Unique meta description and meta keyword tags in your WordPress themes](https://www.malcolmcoles.co.uk/blog/unique-meta-description-and-meta-keywords-in-your-wordpress-themes/)
*   [How to: Create a meta description function for your WordPress blog](https://www.wprecipes.com/how-to-create-a-meta-description-function-for-your-wordpress-blog)

## 5\. Link To External Resources

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/533c7f9d-fd35-412c-8cf7-e52ee14cb4b5/sm6.jpg" alt="Screenshot" />

<strong>The problem.</strong> Many bloggers have asked me the following question: "How can I link directly to an external source, rather than creating a post just to tell visitors to visit another website?"

The solution to this problem is to use custom fields. Let's see how we can do that.

<strong>The solution.</strong> The first thing to do is open your <em>functions.php</em> file and paste in the following code:

<pre><code class="language-php">function print_post_title() {
  global $post;
  $thePostID = $post-&gt;ID;
  $post_id = get_post($thePostID);
  $title = $post_id-&gt;post_title;
  $perm  = get_permalink($post_id);
  $post_keys = array(); $post_val  = array();
  $post_keys = get_post_custom_keys($thePostID);

  if (!empty($post_keys)) {
      foreach ($post_keys as $pkey) {
          if ($pkey=='url1' || $pkey=='title_url' || $pkey=='url_title') {
              $post_val = get_post_custom_values($pkey);
          }
      }
      if (empty($post_val)) {
          $link = $perm;
      } else {
          $link = $post_val[0];
      }
  } else {
      $link = $perm;
  }
  echo '&lt;h2&gt;&lt;a href="'.$link.'" rel="bookmark" title="'.$title.'"&gt;'.$title.'&lt;/a&gt;&lt;/h2&gt;';
}</code></pre>

Once that's done, open your <em>index.php</em> file and replace the standard code for printing titles...

<pre><code class="language-php">&lt;h2&gt;&lt;a href="&lt;?php the_permalink() ?&gt;" rel="bookmark" title="Permanent Link to &lt;?php the_title(); ?&gt;"&gt;&lt;?php the_title(); ?&gt;&lt;/a&gt;&lt;/h2&gt;</code></pre>

... with a call to our newly created <em>print_post_title()</em> function:

<pre><code class="language-php">&lt;?php print_post_title() ?&gt;</code></pre>

Now, whenever you feel like pointing one of your posts' titles somewhere other than your own blog, just scroll down in your post editor and create or select a custom key called <em>url1</em> or <em>title_url</em> or <em>url_title</em> and put the external URL in the value box.

<strong>Code explanation.</strong> This is a nice custom replacement function for the <em>the_title()</em> WordPress function.

Basically, this function does the same thing as the good old <em>the_title()</em> function, but also looks for a custom field. If a custom field called <em>url1</em> or <em>title_url</em> or <em>url_title</em> is found, then the title link will lead to the external website rather than the blog post. If the custom field isn't found, the function simply displays a link to the post itself.

<strong>Sources:</strong>

*   [Hacking WordPress theme: external URL for post title](https://www.istudioweb.com/hacking-wordpress-theme-external-url-for-post-title-2008-01-12/)
*   [How to: Link to an external resource in the post's title](https://www.wprecipes.com/how-to-link-to-some-external-ressource-in-post-title)

## 6\. Embed Custom CSS Styles

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86dcc341-48f4-4858-ad1f-9b3ef1fe5186/sm7.jpg" alt="Screenshot" />

<strong>The problem.</strong> Certain posts sometimes require additional CSS styling. Sure, you can switch WordPress' editor to HTML mode and add inline styling to your post's content. But even when inline styling is useful, it isn't always the cleanest solution.

With custom fields, we can easily create new CSS classes for individual posts and make WordPress automatically add them to the blog's header.

<strong>The solution.</strong> First, open your <em>header.php</em> file and insert the following code between the <em>&lt;head&gt;</em> and <em>&lt;/head&gt;</em> HTML tags:

<pre><code class="language-php">&lt;?php if (is_single()) {
    $css = get_post_meta($post-&gt;ID, 'css', true);
    if (!empty($css)) { ?&gt;
        &lt;style type="text/css"&gt;
        &lt;?php echo $css; ?&gt;
        &lt;style&gt;
    &lt;?php }
} ?&gt;</code></pre>

Now, when you write a post or page that requires custom CSS styling, just create a custom field called <em>css</em> and paste in your custom CSS styling as the value. As simple as that!

<strong>Code explanation.</strong> First, the code above makes sure we're on an actual post's page by using WordPress' conditional tag <em>is_single()</em>. Then, it looks for a custom field called <em>css</em>. If one is found, its value is displayed between <em>&lt;style&gt;</em> and <em>&lt;/style&gt;</em> tags.

<strong>Source:</strong>

*   [How to: Embed CSS in your posts with a custom field](https://www.wprecipes.com/how-to-embed-css-in-your-posts-with-a-custom-field)

## 7\. Re-Define The <title> Tag

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4126cab-71b7-4e2a-974e-a269e58e5ea4/sm1.jpg" alt="Screenshot" />

<strong>The problem.</strong> On blogs, as on every other type of website, content is king. And SEO is very important for achieving your goals with traffic. By default, most WordPress themes don't have an optimized &lt;title&gt; tag.

Some plug-ins, such as the well-known "All in One SEO Pack," override this, but you can also do it with a custom field.

<strong>The solution.</strong> Open your <em>header.php</em> file for editing. Find the &lt;title&gt; tag and replace it with the following code:

<pre><code class="language-php">&lt;title&gt;

&lt;?php if (is_home () ) {
    bloginfo('name');
} elseif ( is_category() ) {
    single_cat_title(); echo ' - ' ; bloginfo('name');
} elseif (is_single() ) {
    $customField = get_post_custom_values("title");
    if (isset($customField[0])) {
        echo $customField[0];
    } else {
        single_post_title();
    }
} elseif (is_page() ) {
    bloginfo('name'); echo ': '; single_post_title();
} else {
    wp_title(’,true);
} ?&gt;
&lt;/title&gt;</code></pre>

Then, if you want to define a custom title tag, simply create a custom field called <em>title</em>, and enter your custom title as a value.

<strong>Code explanation.</strong> With this code, I have used lots of template tags to generate a custom &lt;title&gt; tag for each kind of post: home page, page, category page and individual posts.

If the active post is an individual post, the code looks for a custom field called <em>title</em>. If one is found, its value is displayed as the title. Otherwise, the code uses the standard <em>single_post_title()</em> function to generate the post's title.

<strong>Source:</strong>

*   [How to: Redefine the title tag with a custom field](https://www.wprecipes.com/how-to-redifine-title-tag-with-a-custom-field)

## 8\. Disable Search Engine Indexing For Individual Posts

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5584df58-1c22-42ad-b7ce-25b2cbb7c3c4/sm8.jpg" alt="Screenshot" />

<strong>The problem.</strong> Have you ever wanted to create semi-private posts, accessible to your regular readers but not to search engines? If so, one easy solution is to... you guessed it! Use a custom field.

<strong>The solution.</strong> First, get the ID of the post that you'd not like to be indexed by search engines. We'll use a post ID of 17 for this example.

Open your <em>header.php</em> file and paste the following code between the &lt;head&gt; and &lt;/head&gt; tags:

<pre><code class="language-php">&lt;?php $cf = get_post_meta($post-&gt;ID, 'noindex', true);
    if (!empty($cf)) {
    echo '&lt;meta name="robots" content="noindex"/&gt;';
}
?&gt;</code></pre>

That's all. Pretty useful if you want certain info to be inaccessible to search engines!

<strong>Code explanation.</strong> In this example, we used the <em>get_post_meta()</em> function to retrieve the value of a custom field called <em>noindex</em>. If the custom field is set, then a <em>&lt;meta name="robots" content="noindex"/&gt;</em> tag is added.

<strong>Source:</strong>

*   [How to: disable search engine indexing of a single post](https://www.wprecipes.com/how-to-disable-search-engine-indexing-on-a-single-post)

## 9\. Get Or Print Any Custom Field Value Easily With A Custom Function

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a1ec189-d97e-4b88-b57f-28a56d185710/sm9.jpg" alt="Screenshot" />

<strong>The problem.</strong> Now that we've shown you lot of great things you can do with custom fields, how about an automated function for easily getting custom fields values?

Getting custom field values isn't hard for developers or those familiar with PHP, but can be such a pain for non-developers. With this hack, getting any custom field value has never been easier.

<strong>The solution.</strong> Here's the function. Paste it into your theme's <em>functions.php</em> file. If your theme doesn't have this file, create it.

<pre><code class="language-php">function get_custom_field_value($szKey, $bPrint = false) {
  global $post;
  $szValue = get_post_meta($post-&gt;ID, $szKey, true);
  if ( $bPrint == false ) return $szValue; else echo $szValue;
}</code></pre>

Now, to call the function and get your custom field value, use the following code:

<pre><code class="language-php">&lt;?php if ( function_exists('get_custom_field_value') ){
        get_custom_field_value('featured_image', true);
} ?&gt;</code></pre>

<strong>Code explanation.</strong> First, we use the PHP <em>function_exists()</em> function to make sure the <em>get_custom_field_value</em> function is defined in our theme. If it is, we use it. The first argument is the custom field name (here, <em>featured_image</em>), and the second lets you echo the value (true) or call it for further PHP use (false).

<strong>Sources:</strong>

*   <span class="removed_link" title="https://www.mattvarone.com/wordpress/useful-functions-for-wordpress/">Useful custom functions for WordPress</span>
*   [How to: Easily get the value of a custom field](https://www.wprecipes.com/how-to-easily-get-the-value-of-a-custom-field)

## 10\. Insert A "Digg This" Button Only When You Need It

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d496e761-3e4b-478d-a191-d5bf61773aec/sm10.png" alt="Screenshot" />

<strong>The problem.</strong> To get traffic from well-known Digg.com, a good idea is to integrate its "Digg this" button into your posts so that readers can contribute to the posts' success.

But do <em>all</em> of your posts need this button? Definitely not. For example, if you write an announcement telling readers about improvements to your website, submitting the post to Digg serves absolutely no value.

<strong>The solution.</strong> Custom fields to the rescue once again. Just follow these steps to get started:

1.  Open your _single.php_ file and paste these lines where you want your "Digg this" button to be displayed:

        <?php $cf = get_post_meta($post->ID, 'digg', true);
          if (!emptyempty($cf)) {
          echo 'https://digg.com/tools/diggthis.js" type="text/javascript">'} ?>

2.  Once you've saved the _single.php_ file, you can create a custom field called _digg_ and give it any value. If set, a Digg button will appear in the post.

<strong>Code explanation.</strong> This code is very simple. Upon finding a custom field called <em>digg</em>, the code displays the "Digg this" button. The JavaScript used to display the "Digg this" button is provided by Digg itself.</p>

## Bonus: Display Thumbnails Next To Your Posts

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b2471dd-5978-4d80-aad3-49af82785d3c/sm11.png" alt="Screenshot" />

<strong>The problem</strong> Most people knows this trick and have implemented it successfully on their WordPress-powered blogs. But I figure some people still may not know how to display nice thumbnails right next to the posts on their home page.

To view examples of this well-known trick, visit my blogs <a href="https://www.wprecipes.com">WpRecipes</a> and <a href="https://www.catswhocode.com">Cats Who Code</a>.

<strong>The solution.</strong>

1.  Start by creating a default image in Photoshop or Gimp. The size in my example is 200x200 pixels but is of course up to you. Name the image _default.gif_.
2.  Upload your _default.gif_ image to the _image_ directory in your theme.
3.  Open the _index.php_ file and paste in the following code where you'd like the thumbnails to be displayed:

        <?php $postimageurl = get_post_meta($post->ID, 'post-img', true);
        if ($postimageurl) {
        ?>
              <a href="<?php the_permalink(); ?>" rel="bookmark"><img loading="lazy" decoding="async" src="<?php echo $postimageurl; ?>" alt="Post Pic" width="200" height="200" /></a>
        <?php } else { ?>
              <a href="<?php the_permalink(); ?>" rel="bookmark"><img loading="lazy" decoding="async" src="<?php bloginfo('template_url'); ?>/images/wprecipes.gif" alt="Screenshot" width="200" height="200" /></a>
        <?php } ?>

4.  Save the file.
5.  In each of your posts, create a custom field called _post-img_. Set its value as the URL of the image you'd like to display as a thumbnail.

<strong>Code explanation</strong> The code looks for a custom field called <em>post-img</em>. If found, its value is used to display a custom thumbnail.

In case a <em>post-img</em> custom field is not found, the default image is used, so you'll never have any posts without thumbnails.</p>

## More Custom Field Resources

You may also be interested in the following related posts:

*   [Custom Fields Hacks For WordPress](https://www.smashingmagazine.com/2009/05/10-custom-fields-hacks-for-wordpress)
*   [10 Useful WordPress Loop Hacks](https://www.smashingmagazine.com/2009/06/10-useful-wordpress-loop-hacks/)
*   [10 Useful WordPress Hook Hacks](https://www.smashingmagazine.com/2009/08/10-useful-wordpress-hook-hacks/)
*   [10 Exceptional WordPress Hacks](https://www.smashingmagazine.com/2009/04/10-exceptional-wordpress-hacks/)

{{< signature "al" >}}


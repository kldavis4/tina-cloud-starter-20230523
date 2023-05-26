---
title: RICG Responsive Images For WordPress
slug: ricg-responsive-images-for-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dece646d-e997-4a06-92b1-e71cc3ea8492/ricg-wp-preview-image.png
date: 2015-02-25T02:37:46.000Z
author: timevko
description: >-
  I recently teamed up with Mat Marquis of the Responsive Images Community Group
  to help integrate responsive images into the WordPress platform. We decided to
  refactor a plugin that I had built several months ago, hoping that it would
  lead to a more useable and performant solution.
categories:
  - WordPress
  - Plugins
  - Responsive Design
  - Techniques (WP)
---
I recently teamed up with Mat Marquis of the Responsive Images Community Group to help integrate responsive images into the WordPress platform. We decided to refactor a plugin that I had built several months ago, hoping that it would lead to a more useable and performant solution.

After months of pull requests, conversations on Slack and help from WordPress’ core team, we’re finally ready to share what we’ve been working on. You can download and install <a href="https://wordpress.org/plugins/ricg-responsive-images/">RICG Responsive Images</a> from WordPress’ plugin directory, while keeping track of our <a href="https://github.com/ResponsiveImagesCG/wp-tevko-responsive-images">development progress on GitHub</a>.

<img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dece646d-e997-4a06-92b1-e71cc3ea8492/ricg-wp-preview-image.png" />

## What Does The Plugin Do?

WordPress hasn’t changed the way it outputs the <code>img</code> tag in quite some time. And although there are plenty of ways to hook into WordPress’ native functions and alter the <code>img</code> snippet, doing so can be overwhelming for beginners and non-theme developers alike. Compound that with the complexity of Picturefill and of the <code>srcset</code> specification, and WordPress users have had few options for implementing a clean and properly functioning responsive images solution.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Images Now Landed In WordPress Core](https://www.smashingmagazine.com/2015/12/responsive-images-in-wordpress-core/)
*   [Automating Art Direction With The Responsive Image Breakpoints Generator](https://www.smashingmagazine.com/2016/09/automating-art-direction-with-the-responsive-image-breakpoints-generator/)
*   [Introducing The Responsive Image Breakpoints Generator](https://www.smashingmagazine.com/2016/01/responsive-image-breakpoints-generation/)
*   [Responsive Images Done Right: A Guide To <picture>And srcset</picture>](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/)
*   [Responsive Images In WordPress With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)

To solve this problem, we set out to build a plugin that gives users responsive images as soon as the plugin is installed, with no extra effort needed. No admin setting, media uploading configuration or coding is required. The plugin <a href="https://scottjehl.github.io/picturefill/">comes with one dependency</a>, a polyfill for browsers that don’t yet support native responsive images. Removing this file is completely optional and will not affect the functionality of the plugin, as long as the user has a modern browser.

As soon as an image is uploaded through the media interface, WordPress automatically creates three variations of the image at different sizes. When the plugin is activated, adding “Featured” and content images to a post will return WordPress’ standard image markup, with an <a href="https://www.smashingmagazine.com/2013/08/21/webkit-implements-srcset-and-why-its-a-good-thing/">added <code>srcset</code> attribute</a>. We’re using the <code>srcset</code> attribute because it’s the easiest attribute for both developers and users to add. While the <code>picture</code> element provides the user with a <a href="https://alistapart.com/article/responsive-images-in-practice#section4">richer set of options</a>, we felt that the <code>srcset</code> attribute makes the most sense as an out-of-the-box solution. It’s also best to use when you’re focusing on <a href="https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/">resolution-switching more than art direction</a> (more on that later in the article).

<pre><code class="language-markup">
&lt;a href="https://ricg.dev/wp-content/uploads/2015/01/image.jpg"&gt;&lt;img loading="lazy" decoding="async" class="6" src="https://ricg.dev/wp-content/uploads/2015/01/image.jpg" srcset="https://ricg.dev/wp-content/uploads/2015/01/image-150x150.jpg 150w, https://ricg.dev/wp-content/uploads/2015/01/image-300x300.jpg 300w, https://ricg.dev/wp-content/uploads/2015/01/image-1024x1024.jpg 1024w, https://ricg.dev/wp-content/uploads/2015/01/image.jpg 1800w" alt="a cool responsive image" width="1800" height="1800"&gt;&lt;/a&gt;
</code></pre>

The plugin is designed to be backwards-compatible, meaning that images added before the plugin was installed will be responsive when added to a post or “Featured Image” section. This is because it uses the image sizes previously defined by WordPress and the active theme’s <code>functions.php</code> file. The image ratio will be maintained throughout the <code>srcset</code> array, meaning that images differing from the aspect ratio of the initial uploaded image will be left out.

Theme developers can use the plugin to place responsive images wherever they’d like by using the <code>tevkori_get_srcset_string()</code> function, which takes an image’s ID and size as parameters.

<pre><code class="language-markup">
&lt;img src="myimg.png" &lt;?php echo tevkori_get_srcset_string( 11, 'medium' ); ?&gt; /&gt;
</code></pre>

There’s also a <code>tevkori_get_srcset_array()</code> function that takes the same parameters and returns an array of <code>srcset</code> values for the specified image.</p>

## How Does The Plugin Work?

Most of the functionality happens when an image is dropped into WordPress’ WYSIWYG editor. Because all of the resized images will have been created during the uploading process, the only thing left to do is create an array containing the URLs of the available images in various sizes, as well as their dimensions. This array is then filtered to remove the image sizes with aspect ratios that don’t match the ratio of the full-sized image.

The array is created by calling the <code>wp_get_attachment_image_src()</code> function and storing the results. At the same time, we use <code>wp_get_attachment_metadata()</code> to retrieve the same results but for every possible variation of the image. Next, the ratio is calculated by multiplying each image’s width by the result of the initial image’s height divided by the initial image’s width. If that result matches the initial image’s height, then the image will be pushed into the final array, to be returned by the <code>tevkori_get_srcset_array()</code> function.

The <code>tevkori_get_srcset_string()</code> function calls <code>tevkori_get_srcset_array()</code> and places the result inside of the <code>srcset</code> attribute. A filter is applied to the <code>image_send_to_editor</code> function, where a regular expression is used to place the result of the <code>tevkori_get_srcset_string()</code> function directly after the <code>src</code> attribute in the image. The same process occurs for featured images, with a filter being applied to the <code>post_thumbnail_html</code> function.

If the image size is changed in the post’s editor, then the plugin will detect the change and update the <code>srcset</code> value accordingly. This ensures that the correct image ratio is always maintained. To enable this functionality, we’re using JavaScript to hook into the <a href="https://codex.wordpress.org/Javascript_Reference/wp.media"><code>wp.media</code> object</a> and recalculating the <code>srcset</code> attribute by running the same image-ratio calculations defined in <code>tevkori_get_srcset_array()</code>. Before starting on this project, I was unaware of the <code>wp.media</code> object and its useful functionality. Because not much documentation for it exists, explaining in detail how we’re using it might be helpful. As it turns out, you can listen for an <code>image-update</code> event in the post’s editor by adding an event listener to the <code>wp.media</code> object.

<pre><code class="language-javascript">
wp.media.events.on( 'editor:image-update', function( args ) {
  var image = args.image;
  //more function logic
});
</code></pre>

With this function, a theme developer can access every image as soon as it has been updated in the post’s editor. You can also take advantage of <a href="https://underscorejs.org/">Underscore</a>, which is used as a dependency by the media uploader to edit image data on the fly. In the case of our plugin, we’re using a helpful Underscore utility to get our image-size ratios once the <code>editor:image-update</code> event has been fired.

<pre><code class="language-javascript">
// Grab all of the sizes that match our target ratio and add them to our srcset array.
_.each(sizes, function(size){
  var softHeight = Math.round( size.width * metadata.height / metadata.width );

  // If the height is within 1 integer of the expected height, let it pass.
  if ( size.height &gt;= softHeight - 1 &amp;&amp; size.height &lt;= softHeight + 1  ) {
    srcsetGroup.push(size.url + ' ' + size.width + 'w');
  }
});
</code></pre>

To learn more about how we hook into the <code>wp.media</code> object, be sure to look at the code in <code>wp-tevko-responsive-images.js</code>.</p>

## The sizes Attribute

Currently, this plugin doesn’t add a <a href="https://ericportis.com/posts/2014/srcset-sizes/#part-2"><code>sizes</code> attribute</a> to complement the <code>srcset</code> attribute. The reason is that we initially recognized that we could never predict what those sizes would need to be, because they depend on how the user’s theme is styled. While we are working on a solution to this issue, we’re encouraging all users to include a <code>sizes</code> attribute on their own, either manually or via another WordPress plugin, such as <a href="https://github.com/aFarkas/wp-lazysizes">wp-lazysizes</a>. One thing to note is that the responsive images specification has recently changed, and use of the <code>w</code> descriptor must now be followed by a <code>sizes</code> attribute. Omitting the <code>sizes</code> attribute will render the markup technically invalid, while still falling back to a default size of <code>100vh</code>.</p>

## What About Features X, Y And Z?

While much more can be done with responsive images, you’ve probably noticed a few use cases that this plugin doesn’t cover. The first thing that we’re usually asked about is a feature for art direction. Art direction refers to loading differently styled images at different breakpoints — whether that means entirely new images or the same image cropped or focused differently. This feature would require use of the <code>picture</code> element, which in turn would mean a lot more markup to generate the final image.

Adding this feature to WordPress would be impossible without the addition of a fairly complicated interface in WordPress’ media uploader, because the user would need to be able to define all breakpoints and then select images to be loaded in when those breakpoints are reached. Our goal for this plugin is to <strong>allow for a basic implementation of responsive images</strong>, with absolutely no configuration needed by the user. So, we’ve decided to omit this feature. We will, however, do our best to allow art direction to work side by side with our plugin as we expand the API for theme developers.

Lazy-loading and image compression are two other features that we have no plans to implement, simply because they fall beyond the scope of a more or less “default” solution for responsive images. Again, we aim to make the addition of these features possible for theme developers who use our plugin via a feature-rich API.</p>

## What’s Next?

While the plugin is available for everyone to download and install, we’re actively working to make it better. So, users can expect frequent updates, resolved issues and an all-around better functioning plugin as time goes on. We’re planning to add more features, such as the <code>sizes</code> attribute and hooks that allow theme developers to further customize the plugin.

Another feature we have yet to consider is ratio descriptors like <code>2x</code> and <code>3x</code> for “Retina” use cases. Better documentation and support are coming soon as well. Eventually, we’d like to see this plugin become a part of WordPress’ core, which means that it will stay minimalist, admin-less and easy to use.

{{< signature "il, al, ml" >}}


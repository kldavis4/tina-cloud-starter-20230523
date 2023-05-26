---
title: 'Better Image Management With WordPress'
slug: better-image-management-practices-with-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/278956f7-956a-4bfc-b852-f26748ca01d0/wordpress-17.gif
date: 2011-05-26T12:36:45.000Z
author: daniel-pataki
summary: >-
  Making sure the content of images is rich in meta information before publishing them is important. That’s why, Daniel Pataki brings you some ways to enrich your blog using some common sense, best practices, and the power of WordPress.
description: >-
  Making sure the content of images is rich in meta information before publishing them is important. That’s why, Daniel Pataki brings you some ways to enrich your blog using some common sense, best practices, and the power of WordPress.
categories:
  - WordPress
  - Tutorials
  - Responsive Images
---

With the advent of sophisticated and user-friendly content management systems like WordPress, textual content has become increasingly easier to manage. The architecture of these systems aims to deliver a well-formed code foundation; this means that if you are a good writer, then your content will be just as awesome as the structure and quality of the code that runs it.

However, media handling is, by nature, not the greatest. In many cases, images are used merely to make the website look good, not to supplement the content. Little care is usually taken to make these elements as useful as their textual counterparts. They are often tacked on as an afterthought; the owner thinks, “If all of my posts have an image, surely I should find something quickly for this next one as well.”

{{% feature-panel %}}

Because **the content of images cannot be parsed by search engines**, making sure they are rich in meta information before publishing them is important. Here are a few ways to enrich your blog using some common sense, best practices and the power of WordPress.

## Understanding And Using Images

To get the most out of your graphic content, you’ll need to be familiar with how they work in HTML. To put an image on a page, you would add an image tag, with the appropriate attributes, like so:

<pre><code class="language-markup tmp-html">&lt;img title="A duck" src="https://myimages.com/theimage.jpg" alt="A mallard duck landing in the water" &gt;</code></pre>

As you can see, the tag has three attributes that contain information about the image:

*   `src` is the URL source of the image file;
*   `alt`, or alternative, text is shown when an image can’t load (whether because of a loading error, text-only browser, etc.);
*   `title` is the title attribute, where you can add a short description of the image, which will pop up after hovering over the image for a second.

The <code>src</code> and <code>alt</code> attributes are both required; the HTML is invalid without them. However, HTML is not a strict language. Your post will still render just fine if you leave out the <code>alt</code> text, which is one of the *negative* aspect of loose languages: it doesn’t force best practices.

### Why Use Alt and Title Attributes?

The most useful aspect of <code>alt</code> and <code>title</code> is that they allow you to add text-based information to an element on your website that would otherwise be invisible to search engines. If you sell umbrellas, Google won’t see that one particular image on your page is of the coolest umbrella it’s ever seen. You’ll have to add that information yourself.

Also, <code>alt</code> attribute can be a huge help to the disabled, because this is how they know what is in an image. So, **use the <code>title</code> attribute to write something snappy about the image, and use the <code>alt</code> attribute to describe it**. Sticking with our umbrella example, the incorrect way to do this would be:

<pre><code class="language-markup tmp-html">&lt;img title="Awesome umbrella" src="awesomeumbrella.jpg" alt="The most awesome umbrella ever" &gt;</code></pre>

And the correct way would be:

<pre><code class="language-markup tmp-html">&lt;img title="Awesome umbrella" src="awesomeubrella.jpg" alt="A matte black cane umbrella with a spruce handle and a chrome tip" &gt;</code></pre>

Remember, the <code>alt</code> attribute is descriptive not only for the visually impaired, but for Google as well. Your website might even rank better if it’s image-heavy.

While not as critical, it is probably worth optimizing the file name as well. The name *o290rjf.jpg* won’t get in the way showing the image, but *super-sleek-umbrella.jpg* is a parsable bit of text, and there is a chance that some search engines would take it into account. Also, if someone downloads the image from your website, they will be able to find it more easily in their “Downloads” folder. And user satisfaction translates into more visits.

### Adding Images Properly With WordPress

WordPress allows you to attach media to posts very easily through the “Add media” modal window, which you can access by clicking one of the icons over the editing toolbar in a post. You can select multiple images and upload them to the post with a click. Because this is so easy, adding the meta attributes is often overlooked and regarded as a hassle.

When uploading images, make sure to fill out the form which is displayed. Add the <code>title</code> and <code>alt</code> attribute at a bare minimum, but also consider filling in the caption and description fields. If you want a short, nicely formatted caption to appear under the image (which is a good idea), type one in. We’ll look later at harnessing the description field, so writing a paragraph or so about the image might be a good idea.

Once done, all you need to do is insert the image, and the correct HTML tag will be plopped in by WordPress automatically. By taking an extra minute, you will have added a sizable bit of text to your image, making it SEO-friendly and in turn making your website that much more informative. If this is all you have time for, then you have done the most important step. But let’s look at some more advanced image-handling techniques.

## Managing Image Sizes

If you display an image at a size of 450&times;300 pixels, then having an image file of roughly the same size is a good idea. If the source file is 2250&times;1500 pixels, the image will show up just fine, but instead of loading a 50 KB image, you would be loading a 500 KB image, while achieving the same effect.

WordPress is super-smart, though, taking care of this for you by churning out different sizes for each image you upload. See the dimensions it creates by going to the media settings in the back end. You can modify these once you have the final layout, which I would advise.

For an image-centric website, you might want to add a couple of more sizes, to make sure you never serve an image that is bigger than needed. By putting the following code in your theme’s *functions.php* file, you create two extra sizes:

<pre><code class="language-php">add_image_size( 'large_thumb', 75, 75, true );
add_image_size( 'wider_image', 200, 150 );</code></pre>

The first line defines an image that is cropped to exactly 75×75 pixels, and the second line defines an image whose maximum dimension is 200×150, while maintaining the aspect ratio. Note the name given in the first argument of the function, because you will be referring to it when retrieving the images, which you can do like so:

<pre><code class="language-php">wp_get_attachment_image_src( 325, 'wider_image');</code></pre>

The first argument is the ID of the attachment that we want to show. The second argument is the size of the image.

### Rebuilding Your Thumbnails

If you have been blogging for a while now, you probably have a ton of images. Adding an image size now will *not* create new thumbnails of your existing images. If you specify an image size&mdash;for example, our *wider_image* format&mdash;WordPress will fetch a resolution that is close to it, but it won’t create a thumbnail especially for this size.

Using a plug-in, however, you can go back and regenerate the thumbnails to make sure that all of the images are optimized, thus **minimizing server load**. I can personally vouch for <a href="https://wordpress.org/extend/plugins/ajax-thumbnail-rebuild/">AJAX Thumbnail Rebuild</a>, which goes through all of your images and regenerates the selected sizes for you.

## Using Featured Images

A featured image can capture the message of a post. Featured images have many uses: for adding flare in a magazine-style layout, underlining a point made in an article, or substituting for an article’s title (in the sidebar, for example).

Featured images have been built into WordPress since version 2.9, so you don’t need any special plug-ins. If you are using the new default WordPress theme, then featured images are already enabled. Otherwise, you might need to switch them on manually. To enable them, just open your theme’s *functions.php* file, paste in the code below, and voila!

<pre><code class="language-php">add_theme_support( 'post-thumbnails' );
set_post_thumbnail_size( 115, 115 )</code></pre>

The first line of code tells WordPress to enable featured images, while the second sets the default size for featured thumbnails. The <code>set_post_thumbnail_size()</code> bit works just like the <code>add_image_size()</code> function we looked at above. You can give it a width, a height and, optionally, a third boolean parameter (<code>true</code> or <code>false</code>) to indicate whether it should be an exact crop.

Once that’s done, go into the back end and edit a post. You should see a featured image widget in the right sidebar; click it to add an image. Or navigate to the media section of the post, view an image’s details, and click the “Use as featured image” link.

The only thing left to do is make these featured images show up! You will need to edit the code for the loop in your theme’s files, which is usually found in *index.php* or in some cases in *loop.php*. Look for something like this:

<pre><code class="language-php">&lt;?php while ( have_posts() ) : the_post(); ?&gt;
The code to display a post is inside here, it can be quite long
&lt;?php endwhile; ?&gt;</code></pre>

Wherever you want to show the images, add the following in the loop:

<pre><code class="language-php">&lt;?php the_post_thumbnail(); ?&gt;</code></pre>

In some cases, you may want to show the featured image at a size different than the default. If so, you can pass the desired size as an argument, like so:

<pre><code class="language-php">&lt;?php the_post_thumbnail("wider_image"); ?&gt;</code></pre>

You can name a size that you have previously created using <code>add_image_size()</code>, as I have done above, or you can use an array to specify a size on the fly: <code>array(225, 166)</code>.

## Creating Galleries

The easiest way to show multiple images in a post is to upload the images to the post and then use the gallery shortcode to display them all.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcaf2d0f-2152-4bc8-8d73-21ed625fae06/gallery-settings.jpg"><img class="87578 alignnone" title="Gallery settings" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcaf2d0f-2152-4bc8-8d73-21ed625fae06/gallery-settings.jpg" alt="The settings pane for creating a gallery in WordPress" width="469" height="280" /></a><figcaption>Show multiple images.</figcaption></figure>

Simply open the “Upload/insert” media screen, click on “Galleries,” and scroll down to the gallery settings. Make sure the links point to the attachment pages (more on this later), and then insert the gallery. Now, thumbnails of all the images you have uploaded to that post will be displayed, each linked to its attachment page.

### Including and Excluding Images

You can easily include images from other posts or exclude certain images from the current post by modifying the gallery shortcode. If you switch the editor to the HTML view, you should see <code>[ gallery ]</code> where the gallery would show up. You can add options to it using the following format: <code>[ gallery option_1="value" option_2="value" ]</code>.

To include a specific image, you will need to know its attachment ID. You can find that by going to the “Media” section of the WordPress admin area, finding the image you need, hovering over it, and reading the target from the URL or status bar. It should be something like <code>`https://webtastique.net/wp-admin/media.php?attachment_id=92&amp;action=edit`</code>. The number after <code>attachment_id</code> is what you need.

You can include multiple items like so: <code>[ gallery include="23,39,45" ]</code>. And exclude items the same way: <code>[ gallery exclude="87,11"]</code>.

{{% ad-panel-leaderboard %}}

### Excluding the Featured Image

Sometimes you will want to use all of the images attached to a post *except* the featured one. You could find the ID of the image and enter it in the exclude options of the gallery shortcode every time, but that would be a hassle (especially if you change the featured image later). Let’s automate this.

Regrettably, the only way to do this is by replacing a core function in WordPress with our own, using the <code>remove_shortcode()</code> and <code>add_shortcode()</code> functions. The large chunk of code below may be off-putting, but implementing it is as easy as copying, pasting and adding two lines of code. The reason we need to add all this is that we can’t just go around editing a WordPress core file; we need to replace core functions with built-in functions.

First, open your theme’s *functions.php* file (if it doesn’t exist, simply create it), and add the following code to it:

<pre><code class="language-php">// remove the  WordPress function
remove_shortcode('gallery', 'gallery_shortcode');
// add our own replacement function
add_shortcode('gallery', 'myown_gallery_shortcode');</code></pre>

This removes the <code>gallery_shortcode()</code> function that WordPress uses to display galleries and replaces it with our own function, called <code>myown_gallery_shortcode()</code>.

The code below is almost exactly the same as the default, but we are adding a line to exclude our featured image. Paste the code below into the *functions.php* file, and then read the explanation further down:

<pre><code class="language-php">function myown_gallery_shortcode($attr) {
  global $post, $wp_locale;

  static $instance = 0;
  $instance++;

  // Allow plugins/themes to override the default gallery template.
  $output = apply_filters('post_gallery', ’, $attr);
  if ( $output != ’ )
    return $output;

  // We’re trusting author input, so let’s at least make sure it looks like a valid orderby statement if ( isset( $attr['orderby'] ) ) {
    $attr['orderby'] = sanitize_sql_orderby( $attr['orderby'] );
    if ( !$attr['orderby'] )
      unset( $attr['orderby'] );
  }
  extract(shortcode_atts(array(
    'order'      =&gt; 'ASC',
    'orderby'    =&gt; 'menu_order ID',
    'id'         =&gt; $post-&gt;ID,
    'itemtag'    =&gt; 'dl',
    'icontag'    =&gt; 'dt',
    'captiontag' =&gt; 'dd',
    'columns'    =&gt; 3,
    'size'       =&gt; 'thumbnail',
    'include'    =&gt; ’,
    'exclude'    =&gt; $default_exclude
  ), $attr));

  $default_exclude = get_post_thumbnail_id($post-&gt;ID);
  $exclude .= ",".$default_exclude;

  $id = intval($id);
  if ( 'RAND' == $order )
    $orderby = 'none';

  if ( !empty($include) ) {
    $include = preg_replace( '/[^0-9,]+/', ’, $include );
    $_attachments = get_posts( array('include' =&gt; $include, 'post_status' =&gt; 'inherit', 'post_type' =&gt; 'attachment', 'post_mime_type' =&gt; 'image', 'order' =&gt; $order, 'orderby' =&gt; $orderby) );

    $attachments = array();
    foreach ( $_attachments as $key =&gt; $val ) {
      $attachments[$val-&gt;ID] = $_attachments[$key];
    }
  } elseif ( !empty($exclude) ) {
    $exclude = preg_replace( '/[^0-9,]+/', ’, $exclude );
    $attachments = get_children( array('post_parent' =&gt; $id, 'exclude' =&gt; $exclude, 'post_status' =&gt; 'inherit', 'post_type' =&gt; 'attachment', 'post_mime_type' =&gt; 'image', 'order' =&gt; $order, 'orderby' =&gt; $orderby) );
  } else {
    $attachments = get_children( array('post_parent' =&gt; $id, 'post_status' =&gt; 'inherit', 'post_type' =&gt; 'attachment', 'post_mime_type' =&gt; 'image', 'order' =&gt; $order, 'orderby' =&gt; $orderby) );
  }

  if ( empty($attachments) )
    return ’;

  if ( is_feed() ) {
    $output = "n";
    foreach ( $attachments as $att_id =&gt; $attachment )
      $output .= wp_get_attachment_link($att_id, $size, true) . "n";
    return $output;
  }

  $itemtag = tag_escape($itemtag);
  $captiontag = tag_escape($captiontag);
  $columns = intval($columns);
  $itemwidth = $columns &gt; 0 ? floor(100/$columns) : 100;
  $float = is_rtl() ? 'right' : 'left';

  $selector = "gallery-{$instance}";

  $output = apply_filters('gallery_style', "


 "); $i = 0; foreach ( $attachments as $id =&gt; $attachment ) { $link = isset($attr['link']) &amp;&amp; 'file' == $attr['link'] ? wp_get_attachment_link($id, $size, false, false) : wp_get_attachment_link($id, $size, true, false); $output .= "&lt;{$itemtag} class='gallery-item'&gt;"; $output .= " &lt;{$icontag} class='gallery-icon'&gt; $link "; if ( $captiontag &amp;&amp; trim($attachment-&gt;post_excerpt) ) { $output .= " &lt;{$captiontag} class='gallery-caption'&gt; " . wptexturize($attachment-&gt;post_excerpt) . " "; } $output .= ""; if ( $columns &gt; 0 &amp;&amp; ++$i % $columns == 0 ) $output .= ''; } $output .= "

 n"; 

 return $output; 

 }</code></pre>

In lines 18 through 29, WordPress is determining the default attributes. By default, nothing is excluded; so under this bit of code, we add two more lines, and that’s it:

<pre><code class="language-php">$default_exclude = get_post_thumbnail_id($post-&gt;ID);
$exclude .= ",".$default_exclude;</code></pre>

The first line here finds the featured image of the post in question, while the second appends it to the exclude list. The rest of the code is the same as the default.

## Using Attachment Pages

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af34bdef-a557-4a43-8809-ffbceffc7e0a/colorblocks.jpg"><img class="aligncenter size-full wp-image-83902" title="A nicely formatted attachment page" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af34bdef-a557-4a43-8809-ffbceffc7e0a/colorblocks.jpg" alt="A WordPress attachment page with an image, a description and some meta data" width="524" height="440" /></a><figcaption>WordPress attachment page with an image, a description and some meta data.</figcaption></figure>

In my opinion, attachment pages are the single best tool for creating richer, more informative image-driven websites. They enable you to create separate pages for each and every media item you have, affording you considerably more power in managing them.

Attachment pages exist in WordPress by default, but people seem to rarely link to them. Linking thumbnails directly to their full-sized versions (i.e. without the website framework) is much more common. I am not a huge fan of this because it throws the user into a completely new environment without prior warning. Attachment pages allow you to show the user a wealth of information about the image; and for those who need a bigger version, you can display download links for different sizes.

### Enabling Attachment Pages

As stated, you don’t need to do anything to enable attachment pages. Just make sure to link your images to them instead of to the original files. For galleries, link to the attachment page using the radio buttons before inserting them. When inserting a single image, point the link’s URL field to the “Post URL” by clicking the relevant button below it.

### Styling Attachment Pages

If your theme doesn’t have an *attachment.php* file, then *single.php* will handle the display of attachment pages by default. If you have a decent theme, chances are this will work fine without your needing to touch any code. When clicking on an image, you should arrive on a page that shows the title and description of the image and the image itself.

To add additional information to this page, you will need an *attachment.php* file. I suggest duplicating *single.php* and going from there, because in most cases it will have most of what you need.

## Adding Image Data

To make the attachment pages more informative, add a bunch of meta data to your images. To help with this, I have created a plug-in especially for Smashing Magazine readers, which you can download from the <a href="https://wordpress.org/plugins/advanced-custom-fields/">WordPress Plugins</a> page, or just search for “advanced custom fields” in WordPress’ back end where you “Add new” plug-ins.

This plug-in lets you create your own custom fields, like the photographer’s name, coordinates, color palette, etc. What you add is up to you. You can easily manage all of the information on the plug-in’s admin page.

In the video below, I’ll walk you through how I did this on my own blog. You’ll learn about basic usage and see an example.
*“<a href="https://vimeo.com/18757227">Better Media Management With WordPress Using the Media Custom Fields Plugin</a>,” by <a href="https://vimeo.com/webtastique">Daniel Pataki</a>.*

## Creative Attachment Page Uses

### Download Links for Image Sizes

Using the <code>add_image_size()</code> function mentioned above, you could create five or six image sizes and show Flickr-style download options that allow users to **choose the dimensions** of their preference. This is helpful when showcasing desktop backgrounds and large photographs. So, let’s do that:

<pre><code class="language-php">// If we are on an attachment page, the $post object will be available and the $post-&gt;ID variable will contain the ID of the image in question.

// Find the meta data field from the postmeta table, which contains the sizes for a given image. This is the '_wp_attachment_metadata' field, which contains a serialized array. Take care, because if you use 'true' as the third parameter, the function will unserialize the string for you, so that you don’t need to do it.
$image_meta = get_post_meta( $post-&gt;ID, '_wp_attachment_metadata', true);

// Put all the image sizes and file names into an array for ease of use
$image_sizes = $image_meta['sizes'];
$image_sizes['original']['width']  =  $image_meta['width'];
$image_sizes['original']['height'] =  $image_meta['height'];
$image_sizes['original']['file']      =  $image_meta['file'];

// Display a list of links for these images
echo '
&lt;h3&gt;This image is available in the following formats&lt;/h3&gt;
';
echo '

'; foreach ( $image_sizes as $size_name => $size ) { $url = wp_get_attachment_image_src( $post->ID, $size_name ); $anchortext = $size['width'] . 'x' . $size['height']; echo "

".$anchortext."9
"; } echo '
';</code></pre>

## Adding Color Palettes

By adding some creativity to the mix, you can come up with some nifty features. The screencast above and the code below shows you how to display color blocks of the dominant colors in each of your photos.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f8b86f8-7e89-44a3-aa35-a778299d210d/screen-shot-2011-02-11-at-1.21"><img class="aligncenter size-full wp-image-89436" title="Example of a color palette" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f8b86f8-7e89-44a3-aa35-a778299d210d/screen-shot-2011-02-11-at-1.21" alt="" width="550" height="90" /></a><figcaption>Adding color blocks.</figcaption></figure>

To accomplish this, you will first need to create a custom field using the Media Custom Fields plug-in and name it something like “Color Palette.” Remember to look at the field name that the system generates; it is displayed in parentheses next to the title you chose. It should be something like *tqmcf_color-palette*.

Once that’s done, edit the image you’d like, and add the following in the custom field: <code>color_1,color_2,color_3</code>, where <code>colors_x</code> should be hex values. In my case, I entered the following string: <code>f0e9bf,e4dc99,000000</code>.

Open up the *attachment.php* file in a code editor. Wherever you want to display the colors, you’ll need to add something like this:

<pre><code class="language-php">// Retrieve the field value from the database
$color_palette = get_post_meta( $post-&gt;ID, 'tqmfc_color-palette', true );

// Turn the string into an array of values, where each value is one of the colors
$colors = explode( ',', $color_palette );

echo '
&lt;h2&gt;Logo Colors&lt;/h2&gt;
';

// Loop through all the colors and create the color blocks, which will actually be links pointing the the color's page on Colourlovers.com
foreach ($colors as $color) {
    $link = 'https://www.colourlovers.com/color/'.$color.'/';
    echo ’;
}</code></pre>

You will also need to style the link element so that it shows up. Because anchors are inline elements by default, if they have no content, they won’t show up. Here’s the CSS I used, but you’ll need to change it to match your website:

<pre><code class="language-php">.color-block {
    display: block;
    float: left;
    height: 20px;
    margin-right: 3px;
    width: 30px;
}</code></pre>

## Conclusion

As you can see, even with minimal effort, you can create a much more robust system for storing and showing images. And with some copying and pasting, you can take it one step further.

The first and most important step is to add meta data like <code>alt</code> text to images, give them meaningful file names and so on. By doing so, you lay a foundation for any media management system. You can easily add other meta data to your files by using the <a title="Custom fields plugin for WordPress media" href="https://wordpress.org/plugins/advanced-custom-fields/">Advanced Custom Fields</a> plug-in for WordPress.

With this foundation in place and a few simple code tweaks, you can show images based on any of the custom fields you wish, displaying relevant and interesting information about them. Creating download buttons for multiple sizes and creating multiple color palettes are only the tip of the iceberg. The techniques showcased here can be used for so much more!

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Web Image Effects Performance Showdown](https://www.smashingmagazine.com/2016/05/web-image-effects-performance-showdown/)
*   [Efficient Image Resizing With ImageMagick](https://www.smashingmagazine.com/2015/06/efficient-image-resizing-with-imagemagick/)
*   [One Solution To Responsive Images](https://www.smashingmagazine.com/2014/02/one-solution-to-responsive-images/)
*   [Clever JPEG Optimization Techniques](https://www.smashingmagazine.com/2009/07/clever-jpeg-optimization-techniques/)

{{< signature "al, mrn" >}}

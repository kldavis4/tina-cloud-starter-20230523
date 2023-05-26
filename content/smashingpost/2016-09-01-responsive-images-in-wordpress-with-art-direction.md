---
title: WordPress Responsive Images With Art Direction
slug: responsive-images-in-wordpress-with-art-direction
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ec1045f-ee3c-4297-834c-9f4be2e61155/car-large-500-opt.jpg
date: 2016-09-01T18:14:22.000Z
author: laurielaforest
description: >-
  Support for responsive images was added to WordPress core in version 4.4 to
  address the use case for viewport-based image selection, where the browser
  requests the image size that best fits the layout for its particular viewport.
categories:
  - WordPress
  - Optimization
  - Performance
  - Responsive Design
  - Techniques (WP)
---
<a href="https://www.smashingmagazine.com/2015/12/responsive-images-in-wordpress-core/">Support for responsive images</a> was added to WordPress core in version 4.4 to address the use case for <a href="https://usecases.responsiveimages.org/#viewport-based-selection">viewport-based image selection</a>, where the browser requests the image size that best fits the layout for its particular viewport.

Images that are inserted within the text of a post automatically get the responsive treatment, while images that are handled by the theme or plugins — like featured images and image galleries — can be coded by developers using the new responsive image functions and filters. With a few additions, WordPress websites can accommodate another responsive image use case known as <a href="https://usecases.responsiveimages.org/#art-direction">art direction</a>. Art direction gives us the ability to design with images whose crop or composition changes at certain breakpoints.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Responsive Image Breakpoints Generator](https://www.smashingmagazine.com/2016/09/automating-art-direction-with-the-responsive-image-breakpoints-generator/)
*   [Introducing The Responsive Image Breakpoints Generator](https://www.smashingmagazine.com/2016/01/responsive-image-breakpoints-generation/)
*   [Responsive Images Done Right: A Guide To <picture>And srcset</picture>](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/)
*   [Responsive Images Now Landed In WordPress Core](https://www.smashingmagazine.com/2015/12/responsive-images-in-wordpress-core/)

In this article, I’ll show you how to set up a WordPress website for art direction by going through three progressive examples:

{{% feature-panel %}}

*   [WordPress’ automatic support for responsive images within posts](#wordpress-automatic-support-for-responsive-images-within-posts)
*   [a variable-width banner image in a page template](#a-variable-width-banner-image-in-a-page-template)
*   [an art-directed hero image in a page template](#an-art-directed-hero-image-in-a-page-template)

In the art direction example, we’ll be adding some PHP, a polyfill and a cropping plugin to the website.</p>

## Automatic Support For WordPress Responsive Images Within Posts

Support for responsive images is all about options: We provide a well-described array of image files to the browser, and the browser applies its knowledge of the width and pixel density of the viewport to request the file with the most appropriate resolution. The workhorse here is the <code>srcset</code> attribute, which can be used with <code>img</code> and <code>source</code> tags. Similar to, but more informative than, its older cousin, the <code>src</code> attribute, <code>srcset</code> is essentially a “set of sources” — that is, a list of image files available for downloading. For detailed background on the <code>srcset</code> attribute, I recommend Eric Portis’ <a href="https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/">article on responsive images</a>.

Since version 4.4, WordPress automatically adds a <code>srcset</code> attribute to any image that is run through <code>the_content</code> filter. In other words, when WordPress is creating the HTML for your web page, it scans the post or page’s text for <code>img</code> tags and adds a <code>srcset</code> attribute to any tags that don’t already contain one. You won’t see the <code>srcset</code> in the post editor (unless you explicitly add one, although you should generally let WordPress take care of it), but it will be present in the page’s HTML source.

To offer multiple image sizes in the <code>srcset</code>, WordPress leverages its standard behavior of automatically creating several smaller versions of your image files when you upload them to the “Media Library.” You can find these sizes listed on the “Media Settings” screen (under the “Settings” menu in the WordPress administration interface), along with their default values; not listed is the <a href="https://make.wordpress.org/core/2015/11/10/responsive-images-in-wordpress-4-4/">new “medium_large” image size</a> (768 pixels wide, with no height limit), the size of which can be changed by a theme or plugin but not through the administration interface.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c146584d-d843-4aad-b62d-3e6cd15fdeab/media-settings-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/858d682b-63b8-46ea-8d4c-58a3cf070308/media-settings-500-opt.jpg" alt="wordpress responsive images" width="500" height="343" /></a><figcaption>The default maximum sizes shown on WordPress’ “Media Settings” screen are 1024 × 1024 pixels for the “large” size, 300 × 300 pixels for the “medium” size, and 150 × 150 pixels for the “thumbnail” size. The 768 pixel “medium_large” size cannot be changed here. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c146584d-d843-4aad-b62d-3e6cd15fdeab/media-settings-large-opt.jpg">View large version</a>)</figcaption></figure>

By default, the autogenerated “medium,” “medium_large” and “large” image sizes are <strong>soft-cropped</strong> — that is, they maintain the same aspect ratio as the original file. (I refer to these as “scaled” versions.) In these cases, the width given on the “Media Settings” screen is the constraining parameter. In contrast, the “thumbnail” size is <strong>hard-cropped</strong> to a 150 pixel square, so it most likely has a different aspect ratio than its bigger brothers. WordPress relies on aspect ratio to determine which image sizes should be included in a <code>srcset</code>, and we’ll be seeing this play out in each of our examples.

Let’s say that you upload a 1400 × 952-pixel image to the WordPress media library and keep the image sizes at their default values. Behind the scenes, WordPress creates the following versions of the original image:
<table class="article-table five-columns"><caption>Image generation in WordPress based on a 1400 × 952-pixel image</caption><br>
<tbody>
<tr>
<th>Size</th>
<th>Width (px)</th>
<th>Height (px)</th>
<th>Cropping</th>
<th>Aspect ratio (w/h)</th>
</tr>
<tr>
<td><strong>full</strong> (original)</td>
<td>1400</td>
<td>952</td>
<td>soft</td>
<td>1.47</td>
</tr>
<tr>
<td><strong>large</strong></td>
<td>1024</td>
<td>696</td>
<td>soft</td>
<td>1.47</td>
</tr>
<tr>
<td><strong>medium_large</strong></td>
<td>768</td>
<td>522</td>
<td>soft</td>
<td>1.47</td>
</tr>
<tr>
<td><strong>medium</strong></td>
<td>300</td>
<td>204</td>
<td>soft</td>
<td>1.47</td>
</tr>
<tr>
<td><strong>thumbnail</strong></td>
<td>150</td>
<td>150</td>
<td>hard</td>
<td>1</td>
</tr>
</tbody>
</table>

If you then insert the “large” (1024 pixels wide) version into a post and view the HTML source for the published web page, you’d see something like this:

<pre><code class="language-markup">
&lt;img src="sample-1024x696.jpg" width="1024" height="696" 
	class="alignnone size-large" 
	srcset="sample-300x204.jpg 300w, 
		sample-768x522.jpg 768w, 
		sample-1024x696.jpg 1024w" 
	sizes="(max-width: 1024px) 100vw, 1024px"
	alt="A meaningful sample image"&gt;
</code></pre>

WordPress has generated a <code>srcset</code> for us using the “medium,” “medium_large” and “large” sizes because these images all share the same aspect ratio. The “thumbnail” version wasn’t included, which makes sense because we want those images to look the same in every viewport.

Two other bits of information are also included in the HTML above. First, the <code>w</code> descriptors within the <code>srcset</code> tell the browser the actual pixel widths of the files; without these, the browser would need download the images to find out their dimensions. Secondly, WordPress’ default value for the <code>sizes</code> attribute tells the browser how wide the image is intended to be in this particular layout. Here, for viewports narrower than 1024 pixels, the image should fill and scale with the size of the viewport; otherwise, the image should be displayed at its default width of 1024 pixels and not any wider. With these final pieces to the puzzle, the browser can now make an intelligent image request, whether it be to display a high-resolution file on a “Retina” display or a low-resolution file on a small phone.</p>

## A Variable-Width Banner Image In A Page Template

Now that we understand how WordPress leverages the standard image sizes to build a <code>srcset</code>, it’s time to get acquainted with WordPress core’s new <a href="https://make.wordpress.org/core/2015/11/10/responsive-images-in-wordpress-4-4/">responsive image functions</a> by applying viewport-based image selection to a theme. For this example, we’ll look at a full-width banner image that appears on a static front page.

Let’s assume that we have an existing website using the current version of WordPress and that <a href="https://codex.wordpress.org/Post_Thumbnails#Enabling_Support_for_Post_Thumbnails">support for post thumbnails is enabled</a> in our theme. (Support for post thumbnails allows us to add featured images to posts and pages.) Let’s also assume that the banner image is pulled from the featured image for the front page. If our front page template uses WordPress’ <code>the_post_thumbnail()</code> template tag to generate the HTML for the banner, then we are all set: This function already outputs an <code>img</code> tag that includes <code>srcset</code> and <code>sizes</code> attributes. That’s one reason why it is good to use WordPress template functions when they are available!

Maybe, though, our page template builds the HTML for the banner image piece by piece, as you might need to do if your banner is actually part of a third-party carousel. To make this image responsive, we ask WordPress explicitly for <code>srcset</code> and <code>sizes</code> attributes, using the <code>wp_get_attachment_image_srcset()</code> and <code>wp_get_attachment_image_sizes()</code> functions, respectively:

<pre><code class="language-php">
&lt;?php if ( has_post_thumbnail() ) : ?&gt;

	$id = get_post_thumbnail_id();
	$src = wp_get_attachment_image_src( $id, 'full' );
	$srcset = wp_get_attachment_image_srcset( $id, 'full' );
	$sizes = wp_get_attachment_image_sizes( $id, 'full' );
	$alt = get_post_meta( $id, '_wp_attachment_image_alt', true);

  	&lt;img src="&lt;?php echo esc_attr( $src );?&gt;"
  		srcset="&lt;?php echo esc_attr( $srcset ); ?&gt;"
		sizes="&lt;?php echo esc_attr( $sizes );?&gt;"
		alt="&lt;?php echo esc_attr( $alt );?&gt;" /&gt;

&lt;?php endif; ?&gt;
</code></pre>

Here, we’ve based <code>srcset</code> and <code>sizes</code> on the original image size by passing the <code>full</code> keyword to our functions. If that image is 1280 × 384 pixels, and if we keep the standard image sizes at their default values, then the HTML output would look like this:

<pre><code class="language-markup">
&lt;img src="banner.jpg" 
	srcset="banner.jpg 1280w,
	banner-300x90.jpg 300w,
	banner-768x231.jpg 768w,
	banner-1024x308.jpg 1024w" 
	sizes="(max-width: 1280px) 100vw, 1280px"
	alt="Front page banner alt text"&gt;
</code></pre>

In this case, as in the last, the value that WordPress gives us for the <code>sizes</code> attribute is acceptable for our hypothetical layout. In general, WordPress’ default value for <code>sizes</code> works fine for full-width images, but for any other layout, you are going to need to write the value yourself. Some layouts are more complicated than others: The <code>sizes</code> attribute for a responsive image grid (see <a href="https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/#the-fluid-and-variable-sized-image-use-cases">Eric Portis’ example</a>) is pretty straightforward, but layouts that change at different breakpoints, such as pages with a sidebar column, require more thought. For the latter case, Tim Evko uses the Twenty Sixteen theme as an <a href="https://www.smashingmagazine.com/2015/12/responsive-images-in-wordpress-core/">example of applying the <code>wp_calculate_image_sizes</code> filter</a> to make the <code>sizes</code> value match the layout’s CSS breakpoints.</p>

## An Art-Directed Hero Image In A Page Template

Let’s momentarily revisit the HTML in the banner example and take note of the size of the smallest image in <code>srcset</code>: It’s only 90 pixels tall and probably difficult to discern. The aspect ratio is fixed by the original image, so, realistically, we’ll be looking at a 96-pixel stripe across a 320-pixel phone.

Themes currently get around the “banner stripe” problem by displaying the banner image as the CSS background of a flexible <code>div</code> and adjusting its <code>height</code> and <code>background-size</code> in media queries. This solution is responsive in terms of appearance, however, it is not a true responsive image solution. Enter art direction, the ability to provide different image sources at different viewport widths directly in HTML. With this technique, we can avoid the banner stripe problem by resetting the proportions of an image below a breakpoint to give the smallest resizes better dimensions; we can also use art direction to emphasize a particular area of an image at different sizes or orientations.

In our art direction example, we will use the 1400 × 952-pixel image from our first example to create a responsive hero image. On large viewports, the hero image will look like this (albeit much larger):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65b8f7e6-9fd7-4ce2-899f-58b3d576bf1d/car-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ec1045f-ee3c-4297-834c-9f4be2e61155/car-large-500-opt.jpg" alt="Large hero image example" width="500" height="340" /></a><figcaption>Full-sized hero image, 1400 × 952 pixels (Image: <a href="https://unsplash.com/">Josh Felise</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/65b8f7e6-9fd7-4ce2-899f-58b3d576bf1d/car-large-opt.jpg">View large version</a>)</figcaption></figure>

But for smaller viewports, we will crop the image within WordPress so that it looks like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd63852f-fee4-41c1-b6a0-2183c08ef40e/car-small-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd63852f-fee4-41c1-b6a0-2183c08ef40e/car-small-opt.jpg" alt="Cropped hero image example" width="500" height="300" /></a><figcaption>Cropped hero image with a 5:3 aspect ratio</figcaption></figure>

This approach gives us two images for the price of one — a full-sized and a cropped — each with its own <code>srcset</code>.

Setting up our WordPress environment for art direction takes four steps. As in the previous example, the hero image will be the featured image for the website’s home page, and we’ll be editing the front-page template. I assume that you are making changes to an existing theme and, thus, have created a <a href="https://codex.wordpress.org/Child_Themes">child theme</a> to work in.</p>

### 1. Include the PictureFill Script

We are going to code our hero image by wrapping it in <a href="https://responsiveimages.org">HTML5’s <code>picture</code> element</a>. The <code>picture</code> element allows us to provide multiple sources for an image, along with media queries to determine when a source will be used. As of this writing, <code>picture</code> is <a href="https://caniuse.com/#feat=picture">supported globally by 62% of browsers</a>, so we will need to rely on the <a href="https://scottjehl.github.io/picturefill/">Picturefill polyfill</a> to implement this element in non-supporting browsers. The Picturefill project is maintained by the Filament Group, and the Picturefill JavaScript file can be <a href="https://github.com/scottjehl/picturefill">downloaded from GitHub</a>.

To include the PictureFill script in the <code>head</code> of our pages, we’ll place the script file in our child theme directory and add the following code to our child theme’s <code>functions.php</code> file:

<pre><code class="language-php">
// adds Picturefill to 'js' subdirectory inside child theme

function theme_add_javascripts() {
    wp_enqueue_script( 'picturefill-js', get_stylesheet_directory_uri() .
    	'/js/picturefill.min.js', '', '', false );
}

add_action( 'wp_enqueue_scripts', 'theme_add_javascripts' );
</code></pre>

### 2. Plan the Breakpoint and Configure the Image Sizes

To plan our <code>srcset</code>s, we need to decide on three things:

*   the breakpoint at which we will switch from the cropped to the full-sized hero image,
*   the aspect ratio of the cropped hero.
*   one or more scaled-down sizes for the cropped image in small viewports.

Let’s deal with each in turn:

<strong>The breakpoint</strong>

For our example, let’s say that the couple in the rearview mirror become hard to recognize in images narrower than 768 pixels; perhaps some overlaid text that we are using with this image no longer fits beneath the mirror at this point as well. We’ll set our breakpoint at 768 pixels, which means that we’ll also be able to keep the “medium_large” and “large” image sizes at their default values.</p>

<strong>The aspect ratio</strong>

This simple implementation of art direction in WordPress doesn’t require us to upload multiple featured images or to type in a value for the breakpoint. Still, we need a way to keep the <code>srcset</code> for the full-sized image from overlapping with the <code>srcset</code> of the cropped image, and for this we will rely on the fact that the <code>wp_get_attachment_image_srcset()</code> function only selects image files with the same aspect ratio as the size we pass to it. We’ll pick a 5:3 (1.67) aspect ratio for the cropped hero image, which differs from the 1.47 aspect ratio of the original.</p>

<strong>The image sizes</strong>

Based on our breakpoint and aspect ratio, the size of the cropped hero image will be 767 × 460 pixels. The cropped hero won’t be completely responsive, however, unless we define additional image sizes to crop along with it. Applying a <a href="https://blog.cloudfour.com/sensible-jumps-in-responsive-image-file-sizes/">performance budget approach</a> to our hypothetical theme, we’ll create custom sizes that are 560 and 360 pixels wide, giving us a roughly 20 KB difference in file size between the three cropped versions. (Because the file size of a compressed image depends its color variation and level of detail, I established this size relationship empirically with WordPress’ default 90% JPEG compression.) The custom image sizes will be created by adding the following code to our child theme’s <code>functions.php</code> file:

<pre><code class="language-php">
// cropped hero
add_image_size( 'mytheme-hero-cropped', 767, 460, true );

// scaled-down cropped hero 1
add_image_size( 'mytheme-hero-cropped-smaller', 560, 336, true );

// scaled-down cropped hero 2
add_image_size( 'mytheme-hero-cropped-smallest', 360, 216, true );
</code></pre>

The fourth parameter in the <code>add_image_size</code> function specifies whether the image version can be hard-cropped, which we set to be <code>true</code>; many cropping plugins (which we’ll look at in step 3) will not let us hard-crop an image unless this is set.

Overall, we’ll have the following image versions available to work with:
<table class="article-table four-columns"><caption>The standard and custom image sizes generated for the hero image in our example</caption><br>
<tbody>
<tr>
<th>Size</th>
<th>Width (px)</th>
<th>Height (px)</th>
<th>Aspect ratio (w/h)</th>
</tr>
<tr>
<td>Full-sized hero:</td>
</tr>
<tr>
<td><strong>full</strong> (original)</td>
<td>1400</td>
<td>952</td>
<td>1.47</td>
</tr>
<tr>
<td><strong>large</strong></td>
<td>1024</td>
<td>696</td>
<td>1.47</td>
</tr>
<tr>
<td><strong>medium_large</strong></td>
<td>768</td>
<td>522</td>
<td>1.47</td>
</tr>
<tr>
<td><strong>medium</strong> (not needed)</td>
<td>300</td>
<td>204</td>
<td>1.47</td>
</tr>
<tr>
<td colspan="4">Cropped hero:</td>
</tr>
<tr>
<td><strong>mytheme-hero-cropped</strong></td>
<td>767</td>
<td>460</td>
<td>1.67</td>
</tr>
<tr>
<td><strong>mytheme-hero-cropped-smaller</strong></td>
<td>560</td>
<td>336</td>
<td>1.67</td>
</tr>
<tr>
<td><strong>mytheme-hero-cropped-smallest</strong></td>
<td>360</td>
<td>216</td>
<td>1.67</td>
</tr>
<tr>
<td colspan="4">Thumbnail:</td>
</tr>
<tr>
<td><strong>thumbnail</strong> (not needed)</td>
<td>150</td>
<td>150</td>
<td>1</td>
</tr>
</tbody>
</table>

### 3. Install a Third-Party Image-Cropping Plugin and Crop the Images

WordPress’ built-in image editor does allow us to hard-crop an image, but the change is applied to all image sizes (or just to the “thumbnail”), whereas we need to crop only three. For greater control, we’ll install a third-party cropping plugin from the WordPress directory.

While any cropping plugin should work with our art direction scheme, the ideal plugin would be able to crop multiple versions of an image at the same time, provided that they all had the same aspect ratio. I came across two plugins that are able to do this: <a href="https://wordpress.org/plugins/crop-thumbnails/">Crop-Thumbnails</a> and <a href="https://wordpress.org/plugins/post-thumbnail-editor/">Post Thumbnail Editor</a>. Testing both of these plugins with our custom image sizes, I found that the Crop-Thumbnails plugin (version 0.10.8) recognized only two of the three sizes as having the 5:3 aspect ratio, meaning that I would need to go through the cropping process two times. (The “mytheme-hero-cropped” size was left out because of a rounding issue: An exact 5:3 aspect ratio would require the width to be 460.2 pixels, instead of 460.) The Post Thumbnail Editor plugin (version 2.4.8) allowed me to crop all three sizes at once.</p>

### 4. Code the Hero Image Using the <picture> Element

Now that our images are ready, we can add the code for the hero image to a copy of the front-page template in our child theme. HTML5’s <code>picture</code> element can hold an <code>img</code> tag and one or more <code>source</code> tags. For our example, the single <code>source</code> element will contain the <code>media</code> query and <code>srcset</code> for the full-sized image, and the <code>img</code> tag will contain the <code>srcset</code> for the cropped image; the cropped image will serve as the default image when the breakpoint condition is not met.</p>

<pre><code class="language-php">
&lt;?php if ( has_post_thumbnail() ) : ?&gt;

	$id = get_post_thumbnail_id();
	$alt = get_post_meta( $id, '_wp_attachment_image_alt', true);

	/* get the width of the largest cropped image to 
	   calculate the breakpoint */
	$hero_cropped_info = 
		wp_get_attachment_image_src( $id, 'mytheme-hero-cropped' );
	$breakpoint = absint( $hero_cropped_info[1] ) + 1;

	// pass the full image size to these functions
	$hero_full_srcset = 
		wp_get_attachment_image_srcset( $id, 'full' );
	$hero_full_sizes = 
		wp_get_attachment_image_sizes( $id, 'full' );

	// pass the cropped image size to these functions
	$hero_cropped_srcset = 
		wp_get_attachment_image_srcset( $id, 'mytheme-hero-cropped' );
	$hero_cropped_sizes = 
		wp_get_attachment_image_sizes( $id, 'mytheme-hero-cropped' );

  &lt;picture&gt;
  	&lt;source
  		media="(min-width: &lt;?php echo $breakpoint; ?&gt;px)"
  		srcset="&lt;?php echo esc_attr( $hero_full_srcset ); ?&gt;"
		sizes="&lt;?php echo esc_attr( $hero_full_sizes ); ?&gt;" /&gt;
  	&lt;img srcset="&lt;?php echo esc_attr( $hero_cropped_srcset ); ?&gt;"
		alt="&lt;?php echo esc_attr( $alt );?&gt;"
		sizes="&lt;?php echo esc_attr( $hero_cropped_sizes ); ?&gt;" /&gt;
  &lt;/picture&gt;
&lt;?php endif; ?&gt;
</code></pre>

There are two additional points of interest in this code. First, notice that we are not hardcoding the breakpoint width, even though we know that it should be 768 pixels in this case. Because we calculate the breakpoint using the width of the largest cropped image, we can now change the image sizes in future without needing to go back to edit the template. Secondly, in contrast to the banner image example, the <code>img</code> tag here does not get a <code>src</code> attribute. This is an artifact of using a polyfill to support the <code>picture</code> element: A non-supporting browser would preload the file given in the <code>src</code> attribute, resulting in a double download for this image.

The HTML that we get is shown below:

<pre><code class="language-markup">
&lt;picture&gt;
  	&lt;source media="(min-width: 768px)" srcset="hero.jpg 1400w,
  		hero-300x204.jpg 300w, hero-768x522.jpg 768w, 
  		hero-1024x696.jpg 1024w" 
  		sizes="(max-width: 1400px) 100vw, 1400px"&gt;
  	&lt;img srcset="hero-767x460.jpg 767w, hero-560x336.jpg 560w, 
  		hero-360x216.jpg 360w" 
  		alt="Front page hero alt text"
  		sizes="(max-width: 767px) 100vw, 767px"&gt;
&lt;/picture&gt;
</code></pre>

We could finish here, but we could make one refinement to our HTML output. Notice that the 300-pixel-wide “medium” image has been included in the <code>srcset</code> for the full-sized image. This image file will never be used, so we can add a <code>wp_calculate_image_srcset</code> filter to remove it from the <code>srcset</code>. The following code, which goes in the child theme’s <code>functions.php</code> file, looks only at the potential <code>srcset</code> (the <code>$sources</code> array) for the full-sized hero image; it loops through the images and removes those with widths narrower than the breakpoint.</p>

<pre><code class="language-php">
add_filter( 'wp_calculate_image_srcset', 
	'mytheme_remove_images_below_breakpoint', 10, 5 );

function mytheme_remove_images_below_breakpoint( $sources, $size_array, 
	$image_src, $image_meta, $attachment_id ) {

	if ( is_front_page() &amp;&amp; has_post_thumbnail() ) {

		// check if we're filtering the featured image
		if ( $attachment_id === get_post_thumbnail_id() )  {

			// get cutoff as width of the largest cropped image size
			// (in HTML, breakpoint = cutoff + 1 )
			$cutoff = 
				$image_meta['sizes']['mytheme-hero-cropped']['width'];

			// check if our version is the full-sized version by 
			// comparing its width to the cutoff
			if ( $cutoff &lt; $size_array[0] ) { // for each element in tentative srcset foreach ( $sources as $key =&gt; $value ) {

					// if image width is at or below cutoff,
					// we don't need it
					if ( $cutoff &gt;= $key ) {
						unset( $sources[ $key ] );
					}
				}
			}
		}
	}

	return $sources;

}
</code></pre>

## Final Thoughts

We have just set up a WordPress theme to support art direction in a simple manner. This method relies on WordPress’ standard administration interface as much as possible, and it requires only a single image to be uploaded. Simplicity comes at a cost, however, and this method has its limitations: The sizes for the cropped hero images are hardcoded in the theme, only one breakpoint is assumed, and the aspect ratios of the full-sized and cropped heros must be different.

Programmatically, it is entirely possible to give a website’s content creator complete control over all aspects of art direction, because the <code>wp_calculate_image_srcset</code> filter can process images by width, size keyword or any other bit of meta data that a theme or plugin wants to save. Multiple images could even be selected from the media library and incorporated in the art-directed version. The challenge lies in making the administration interface — the theme customizer or the plugin settings page — simple to use for content creators who may want no options, a few options or the kitchen sink.

Finally, we can’t end an article on responsive images in 2016 without mentioning browser support. While we do have a very effective polyfill for the <code>picture</code> element, if a browser that does not natively support the <code>srcset</code> attribute has JavaScript turned off (or encounters a JavaScript error), a visitor will only see our hero image’s <code>alt</code> text. Global support for the <code>picture</code> element did increase earlier this year when new versions of Safari for Mac and iOS were released, but we are still waiting for the <code>picture</code> element to come to UC Browser and for older browsers — namely, Internet Explorer 11 — to die out.

{{< signature "vf, al, il" >}}


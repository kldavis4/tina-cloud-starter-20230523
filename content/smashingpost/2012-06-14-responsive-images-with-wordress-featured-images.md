---
title: Responsive Images With WordPress' Featured Images
slug: responsive-images-with-wordress-featured-images
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab27f371-28b4-4561-9283-26ab96cd02f2/responsive-main.jpg
date: 2012-06-14T11:00:46.000Z
author: rachel-mccollin-2
description: >-
  It’s been a couple of years now since the concept of responsive design took the Web design world by storm, and more and more websites are going responsive. But there are still some barriers and potential problems, not the least of these being the challenge of reducing the size of files that you’re sending to mobile devices.
categories:
  - WordPress
  - Mobile
  - Responsive Design
  - Media Queries
---
In this article, we’ll look at how to use WordPress’ built-in featured images capability to deliver different-sized image files to different devices. “Featured images,” sometimes referred to as thumbnails, is a feature of WordPress that has been vastly improved since version 3. It enables you to specify a featured image for each post and display it with the post’s content.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Choosing A Responsive Image Solution](https://www.smashingmagazine.com/2013/07/choosing-a-responsive-image-solution/)
*   [Responsive Images Now Landed In WordPress Core](https://www.smashingmagazine.com/2015/12/responsive-images-in-wordpress-core/)
*   [Responsive Images In WordPress With Art Direction](https://www.smashingmagazine.com/2016/09/responsive-images-in-wordpress-with-art-direction/)
*   [Introducing The Responsive Image Breakpoints Generator](https://www.smashingmagazine.com/2016/01/responsive-image-breakpoints-generation/)

The fact that the image is stored in the post’s meta data, rather than embedded in the post’s content, means we can use it more flexibly, as we shall see.

{{% feature-panel %}}

## Why Worry About Image Size?

OK, so a lot of people <em>do</em> use their mobile devices to surf the Web while sitting on the sofa, hooked up to their Wi-Fi, one eye on the phone and one on the TV. And many browse for information sparked by a conversation with the people around them. This type of website visitor is becoming more and more common. You might even be reading this article in this way right now.

But there are and will always be people who use the Web from a mobile device while out and about, possibly using 3G in an area with a dodgy signal or on an expensive data plan. We Web designers and developers tend to invest in data plans with all the bells and whistles; but, believe it or not, plenty of people out there don’t use the Internet as much as we do and so choose a limited plan.

These people won’t thank you for using up their data by sending huge image files to their devices. They may well abandon your website before looking at it if the image downloads are slowing everything down. Moreover, mobile visitors might only check your website quickly in the middle of doing something else, <em>and</em> a slow website could harm your search engine rankings. Taking all this into account, surely reducing file sizes for mobile devices is a no-brainer.</p>

## Responsive Images: What’s It All About?

By now, you probably know what responsive design is: it uses a combination of a fluid layout and media queries to define breakpoints at which a website’s layout or content changes to fit a particular screen size. Most responsive websites use media queries to target phones; some target tablets such as iPads as well.

In the early days of responsive design, making your images responsive meant using CSS to ensure they stayed nicely inside their containing element, with this code:

<pre><code class="language-css">img {
   max-width: 100%;
}</code></pre>

This technique makes the images look tidy, but all it really does is shrink the same large image to fit the layout. It does nothing to alter the actual size of the file, which could lead to huge image files sneaking onto your mobile design and seriously slowing down the website. Displaying large images that have been shrunk with CSS is discouraged by the W3C, and it uses processing power and data, so it’s a particularly bad idea on mobile devices.

When we do responsive design now, we generally include some way of making the image’s actual size smaller, using one of a variety of established techniques.</p>

## More Than One Way To Skin This Cat

If you’ve taken an interest in responsive design, you’ll have noticed that quite a few methods of delivering truly responsive images have emerged. Here are some of those methods:

*   Replace images in the markup with background images, using images of different sizes depending on the device. This method has serious accessibility and SEO drawbacks because the images don’t have `alt` tags for screen readers to read or search engines to index.
*   Use a smaller image in the markup and a larger image as the background of the containing element in the desktop version of the website, and then use CSS to hide the smaller image on larger screens. This method, described in detail by [Harry Roberts on CSS Wizardry](https://csswizardry.com/2011/07/responsive-images-right-now/), is better than the first one, but it does require that you manually create two images and then, in the style sheet, define the background image for every single image on the website. I don’t know about you, but I certainly don’t have the time or patience for that!
*   Use a JavaScript-based solution that employs URL parameters or data attributes. This avoids the repetitive work above, but it involves more processing and [can slow the website down](https://24ways.org/2011/adaptive-images-for-responsive-designs "Matt Wilcox on javascript-based resposnive images in 24 Ways")—the opposite of what you intended.
*   Use a solution such as Matt Wilcox’s [Adaptive Images](https://adaptive-images.com/ "Adapative images website"), which does the work for you. This is the smoothest option I’ve seen, but it requires that you separate the images that you want to be resized from those that you don’t—a potential problem when handing over a CMS-based website to a client or editor who isn’t technologically savvy.

The fact that Adaptive Images uses PHP got me thinking about how this could fit WordPress, which, after all, is written in PHP. Is there a way to use WordPress’ built-in functionality to deliver responsive images in a way that the client would not be able to break?

The answer is yes… with the addition of just one free plugin.</p>

## WordPress Responsive Images: Making It Work

I’ll demonstrate this technique using a website that I recently developed for a client, <a href="https://whatsamayorfor.org.uk">What’s a Mayor For?</a>. This website is responsive and gets a significant portion of visits from mobile devices. At the moment, it uses <code>max-width</code> to resize images, but it doesn’t send different image files to mobile devices.

This is what the website looks like in desktop and mobile browsers:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e7a8c37-f06a-4c72-b35c-de523f24874a/wpresponsiveimages-image1.png"><img class="alignleft size-medium wp-image-111749" title="whatsamayorfor-desktop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4024e1c8-7be6-4fb3-a2b6-c935a34b1085/wpresponsiveimages-image1-300x203.png" alt="The whatsamayorfor site on desktop browsers" width="300" height="203" /></a><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1143bf03-eaff-4142-9068-b367e5469ab0/wpresponsiveimages-image2.png"><img class="size-medium wp-image-111750 alignnone" title="whatsamayorfor-mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/435a911f-c946-4b65-817e-4e2a62295b4e/wpresponsiveimages-image2-109x300.png" alt="The whatsamayorfor site on mobile devices" width="109" height="300" /></a><br>
<em>Click on the images for a large preview.</em>

As you can see, the images scale to fit the layout. But what you can’t see is that the image’s actual size stays the same. We need to change that.

The solution we’ll follow here uses the following elements:

1.  A free plugin called Mobble, which detects devices and provides conditional PHP functions that you can use to deliver different content to different devices in your theme’s files;
2.  The `single.php` and `page.php` files, which we’ll edit to display the post or page’s featured image, but altering the image’s size according to the type of device;
3.  The featured image functionality in WordPress’ dashboard, which we’ll use to define the image used for each post and page.

Let’s get started!

### Download the Mobble Plugin

First, download the <a href="https://wordpress.org/extend/plugins/mobble/">Mobble</a> plugin. This will check the browser’s user-agent string to determine which device the user is on. These checks are wrapped in WordPress-style conditional functions, such as <code>is_mobile()</code>, which is the one we’ll be using. Purists will balk at this approach, but in my experience it’s very reliable, and the plugin does get a high rating in WordPress’ repository.

Download and activate the plugin.</p>

### Edit the single.php and page.php Files to Call the Post’s Thumbnail

Using a text editor or WordPress’ editor, open the <code>single.php</code> file. Find the following code or something like it:

<pre><code class="language-css">&lt;article id="post-&lt;?php the_ID(); ?&gt;" &lt;?php post_class(); ?&gt;&gt;
&lt;h1 class="entry-title"&gt;&lt;?php the_title(); ?&gt;&lt;/h1&gt;
&lt;section class="entry-content"&gt;</code></pre>

In our example, the image needs to be displayed immediately after the heading and before the content, so our code needs to be inserted between the <code>h1</code> and <code>section</code> tags. If your website’s theme doesn’t use HTML5, you may put a <code>div</code> there instead of <code>section</code>.

Here is the code that displays the featured image for a given post:

<pre><code class="language-css">&lt;?php the_post_thumbnail(); ?&gt;</code></pre>

The function has some parameters that we can use, the most relevant being image size. You can use any of the sizes defined by WordPress:

*   `thumbnail` Thumbnail: by default, a maximum of 150 × 150 pixels
*   `medium` Medium resolution: by default a maximum of 300 × 300 pixels
*   `large` Large resolution: by default, a maximum of 640 × 640 pixels
*   `full` Full resolution: the original uploaded size

This is where our conditional function plays with the image’s size. Here is the full code we’ll need:

<pre><code class="language-css">&lt;?php
   if (is_mobile()) {
   the_post_thumbnail('medium');
   } else {
   the_post_thumbnail('large');
} ?&gt;</code></pre>

This code does the following:

1.  Checks whether the website is being viewed on a mobile device: `if (is mobile())`;
2.  If so, outputs the medium resolution of the post’s thumbnail (or featured image): `{the_post_thumbnail('medium')}`;
3.  If not (i.e. `else`), outputs the large resolution: `{the_post_thumbnail(large)}`.

Having set up the <code>single.php</code> file, let’s do the same for <code>page.php</code>. Then, we need to change any embedded images to featured images via the WordPress dashboard.</p>

### Use WordPress’ Featured Image Functionality to Display the Images Correctly

Adding featured images in WordPress has been very simple since the functionality was incorporated in the user interface in version 3.0. Just follow these three steps:

1.  In the WordPress dashboard, open the editing screen for each post and page.
2.  Delete the existing image (it will remain in the gallery for that post or page, which will be helpful in a moment).
3.  Click “Set featured image” in the bottom right of the screen.
4.  In the “Set featured image” pop-up, click the “Gallery” tab. The image you just deleted will be displayed. All you need to do now is click “Use as featured image,” and then click the little cross in the top right of the window. Don’t insert the image into the post or else the image will be displayed twice.[![The WordPress featured image uploader](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da51e035-ce99-4d4a-bda3-d93fc3e359dd/wpresponsiveimages-image3-300x203.png "wordpress-featured-image-uploader")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13106e4e-2024-4b11-b18e-84046949693a/wpresponsiveimages-image3.png) _[Large preview](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13106e4e-2024-4b11-b18e-84046949693a/wpresponsiveimages-image3.png)._
5.  Finally, click the “Update” button to save the changes that you’ve made to the post, and test it.</p>

## Summary

As you can see, using WordPress’ featured images functionality to make responsive websites faster on mobile devices is a fairly simple process. All it takes is three steps:

1.  Install the Mobble plugin.
2.  Add conditional tags to the `single.php` and `page.php` files to call different versions of the image depending on the device.
3.  Replace images in the body of the content with the featured images.

Of course, this method isn’t perfect for all situations. It only works if the image should appear above (or below) the rest of the content, and it does require that anyone who adds a post or page use the featured image functionality instead of just inserting an image in the body of the content. All you need to do now is educate the editors of your website to use featured images instead of images within the content. But how you do that is for another day!

{{< signature "al" >}}


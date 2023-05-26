---
title: 'The Mystery Of CSS Sprites: Techniques, Tools And Tutorials'
slug: the-mystery-of-css-sprites-techniques-tools-and-tutorials
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ad690ce-d7cb-4271-bf44-8b2fe40b041a/add-ons-illus.jpg
date: 2009-04-28T02:21:07.000Z
author: sven-lennartz
description: >-
  **CSS Sprites** are not new. In fact, they are a rather well-established technique and have managed to become common practice in Web development. Of course, CSS sprites are not always necessary, but in some situation they can bring significant advantages and improvements – particularly if you want to reduce your server load. 
categories:
  - Coding
  - CSS
  - Techniques
  - Essentials
---
And if you haven't heard of CSS sprites before, now is probably a good time to learn what they are, how they work and what tools can help you create and use the technique in your projects.

## What Are CSS Sprites?

The term "sprite" (similar to "spirit," "goblin," or "elf") has its origins in computer graphics, in which it described a graphic object blended with a 2-D or 3-D scene through graphics hardware. Because the complexity of video games has continually increased, there was a need for smart techniques that could deal with detailed graphic objects while keeping game-play flowing. One of the techniques developed saw sprites being plugged into a master grid (see the image below), then later pulled out as needed by code that mapped the position of each individual graphic and selectively painted it on the screen.

Sprites were displayed over a static or dynamic background image, and the positioning of the sprite was controlled simply by the hardware controllers. The term was coined because the sprites seemed to "haunt" the display and didn't really exist in the graphic memory.
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e036165-6189-49ad-82ea-1c604fe95719/pokemon.gif" border="0" alt="Screenshot" width="450" height="299" /><br>
<em>The Pokemon Sprite Sheet, consisting of over 1000 graphic objects. Found <a href="https://gmc.yoyogames.com/">here</a>. You can click on the image for the larger version (<em>thanks, Ryan!</em>).</em>

Time passed, and at the beginning of the 2000s, when progressive Web designers started to seek alternatives to JavaScript-based rollover menus (with onMouseOver and onMouseOut effects), sprites saw a renaissance in Web development. With CSS, the simple implementation of sprites was possible, and it was much easier and clearer than its JavaScript-based predecessor.

{{% feature-panel %}}

In 2004, Dave Shea <a href="https://www.alistapart.com/articles/sprites">suggested</a> a simple CSS-based approach to CSS sprites based on the practice established by those legendary video games. In this case, multiple images used throughout a website would be combined into the so-called "master image." To display a single image from the master image, one would use the <strong>background-position</strong> property in CSS, defining the exact position of the image to be displayed. Any hover, active or focus effects would be implemented using the simple definition of the background-position property for the displayed element.

When the page is loaded, it would not load single images one by one (nor hover-state images per request), but would rather <strong>load the whole master image at once</strong>. It may not sound like a significant improvement, but it actually was: the main disadvantage of the onMouse effects is that JavaScript-based hover effects require two HTTP requests for each image, which takes time and creates that unpleasant "flickering" of images. Because the master image is loaded with the whole page only once with CSS sprites, no additional HTTP requests are needed for hover, active or focus effects (because the image is already loaded), and no "flickering" effect occurs.

Consequence: CSS sprites reduce HTTP requests and the loading time of pages. This is the main reason why CSS sprites are often used on websites with heavy traffic, where millions of page impressions would need "only" a tiny fraction of what could otherwise be 30,000,000. Hence, CSS sprites are commonly used, particularly for navigation (such as for hover effects), icons and buttons.
## Where Are CSS Sprites Used?

CSS sprites can be used in various settings. Large websites can combine multiple single images in a meaningful manner, creating clearly separated "chunks" of the master images &ndash; the purpose being to keep the design maintainable and easy to update. The large empty space between the images is often used to make sure that the text resizing in browser doesn't cause side effects such the display of multiple images in the background. In fact, sprites usually work well in a pixel-based design, but they are hard to use in elastic (em-based) designs due to the restricted background-position-property. Essentially, the structure that sprites take depends on the trade-off between maintainability and reduced server load; thus, it varies depending on the project you are working on.

Here are some inspiring (and not so inspiring) examples:

<a href="https://www.xing.de">Xing</a>
Xing uses various icons and buttons, as well as its logo, in the sprite.
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a1854f7-94b2-485b-ba9a-5635180a3fa2/xing.png" border="0" alt="Screenshot" width="463" height="106" /></p>

<a href="https://www.amazon.com">Amazon</a>
Large, shiny and compact CSS sprites on Amazon.
<p class="showcase"><a href="https://www.flickr.com/photos/mezzoblue/3217540317/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8098a66e-ad94-4d2a-a729-da5dc80707d7/amazon.png" border="0" alt="Screenshot" width="605" height="540" /></a></p>

<a href="https://www.apple.com/">Apple</a>
Apple uses CSS sprites for various states of its main navigation menu.
<p class="showcase"><a href="https://images.apple.com/global/nav/images/globalnavbg.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1cf1f27-4c7b-41b8-b2d7-51d4615afbfc/apple.jpg" border="0" alt="Screenshot" width="590" height="152" /></a></p>

<a href="https://youtube.com/">YouTube</a>
YouTube takes a vertical approach to its buttons and icons. The whole sprite is 2800 pixels in height!
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9280c4f1-a1d2-4606-ac09-b13ca3c5f4ff/youtube.gif" border="0" alt="Screenshot" width="152" height="450" /></p>

<a href="https://www.cnn.com/">CNN</a>
CNN uses a modest CSS sprite with its social icons.
<p class="showcase"><a href="https://i.cdn.turner.com/cnn/.element/img/2.0/global/icons/share_sprite.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ea3c385-32f3-489c-9cf2-3e6958c604fc/cnn.gif" border="0" alt="Screenshot" width="20" height="200" /></a></p>

<a href="https://www.digg.com/">Digg</a>
Digg has quite an esoteric sprite, with small arrows and brackets. The large empty space between the images is used to make sure that text resizing doesn't display multiple images as the background image. You can explicitely define width and height in pixels, so that this problem does not occur &ndash; however, in this case the resized text will never break out of the defined box, thus possibly making the text unreadable. Consequently, you must be cautious when using spriting for buttons with variable text labels. For those buttons, you should define font size in pixels also. Or just use the large empty space in the sprite (<em>thanks, daftie!</em>).

<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99f005ea-7307-4075-a1b0-0089cc749b31/digg.gif" border="0" alt="Screenshot" width="211" height="508" /></p>

<a href="https://www.yahoo.com/">Yahoo</a>
Yahoo has nice icons in its sprite, spread out equidistant from each other.
<p class="showcase"><a href="https://l.yimg.com/a/i/ca/sp/purple/fp_spt_icons_0.0.2.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9280c4f1-a1d2-4606-ac09-b13ca3c5f4ff/youtube.gif" border="0" alt="Screenshot" width="335" height="435" /></a></p>

<a href="https://www.google.com/">Google</a>
Google sticks to its minimalist design principle with its minimalist CSS sprite.
<p class="showcase"><a href="https://www.google.ca/images/nav_logo3.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bd1361a-5dd5-48b4-8488-ca1e5635a06b/google.png" border="0" alt="Screenshot" width="150" height="105" /></a></p>

<a href="https://dragoninteractive.com/">Dragon Interactive</a>
A design agency with a colorful, vivid CSS sprite for the navigation menu.
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b100531b-0b24-4224-a605-4ee2ad76a624/dragon.jpg" border="0" alt="Screenshot" width="556" height="350" /></p>

<a href="https://tv1.rtp.pt/noticias/index.php">TV1.rtp.pt</a><br />A huge colorful and qute chaotic CSS sprite on a site of a Portugiese TV-channel (<em>thank you, António Manuel Cardoso!</em>).
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74319f47-9816-47a2-b0d4-a8557d56acd8/noti.jpg" border="0" alt="Screenshot" width="500" height="600" /></p>

CSS Sprites are used to combine many frequently used graphic elements, such as navigation elements, logos, lines, RSS icons, buttons, etc. Conversely, they are not used for any kind content that is likely to change frequently upon release.
## Articles About CSS Sprites

<a href="https://www.alistapart.com/articles/sprites">CSS Sprites: Image Slicing’s Kiss of Death</a>
The legendary introductory article about CSS sprites on A List Apart.
<p class="showcase"><a href="https://www.alistapart.com/articles/sprites"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3a24f84-a77c-4d68-8187-e0e1bd95574c/sprites.gif" border="0" alt="Screenshot" width="175" height="112" /></a></p>

<a title="What They Are, Why They’re Cool, and How To Use Them" rel="bookmark" href="https://css-tricks.com/css-sprites/">CSS Sprites: What They Are, Why They’re Cool And How To Use Them</a>
An illustrated article about CSS sprites by Smashing Magazine author Chris Coyier and a blogger from Turkey, Volkan Görgülü.
<p class="showcase"><a href="https://css-tricks.com/css-sprites/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d10aaa7-7861-4bfb-8dbe-123dc0513aa8/example1before.png" border="0" alt="Screenshot" width="450" height="294" /></a></p>

<a href="https://www.websiteoptimization.com/speed/tweak/css-sprites/">How Yahoo.com and AOL.com Improve Web Performance With CSS Sprites</a>
Some of the busiest websites on the Web use CSS sprites to save on HTTP requests. This article shows how Yahoo! and AOL use sprites to improve performance. Note: some devices (the iPhone being the most notable) apply sprites in a memory-intensive way, which slows the device to a crawl.

<a href="https://www.peachpit.com/articles/article.aspx?p=447210">What Are CSS Sprites?</a>
An introduction by Jason Cranford Teague.
<p class="showcase"><a href="https://www.peachpit.com/articles/article.aspx?p=447210"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ca4f2ad-baea-4bcd-8ba3-cd9fb72d25f6/fig02.jpg" border="0" alt="Screenshot" width="377" height="542" /></a></p>

<a title="Permanent link for this article" href="https://mezzoblue.com/archives/2009/01/27/sprite_optim/">Sprite Optimization</a>
Dave Shea ponders whether it actually makes sense to create large CSS sprites, combining all elements into a single image and then displaying them with the <code>background-position</code> property in CSS. Answer: No, do not over-complicate things. Instead, find a good compromise between quick loading time and maintainability.

<a title="Permanent link for this article" href="https://mezzoblue.com/archives/2009/01/27/sprite_optim/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b8e61a1-3568-4408-b4f9-6578b018f97c/various.gif" alt="CSS Sprites" width="514" height="157" /></a>

Creating Easy and Useful CSS Sprites
A detailed introduction to CSS Sprites by Ignacio Ricci. All files can be downloaded as well.
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24dd76df-1afa-4a09-b2f5-4ea44141799a/background-position.png" border="0" alt="Screenshot" width="635" height="268" /></p>

<a href="https://wellstyled.com/css-nopreload-rollovers.html">Fast Rollovers Without Preload</a>
A practical example of implementing fast rollovers.
<p class="showcase"><a href="https://wellstyled.com/css-nopreload-rollovers.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da8132f4-18c2-4133-9dbd-0b1b83313015/button.gif" border="0" alt="Screenshot" width="471" height="27" /></a></p>

CSS Sprites + Rounded corners
Another example from practice, this one explaining how to display rounded corners using CSS Sprites.
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b912a27-db33-438e-94ff-4fdfcc6e4f06/creating-your-rounded-box-sprite-part2.gif" border="0" alt="Screenshot" width="479" height="105" /></p>

<a href="https://websitetips.com/articles/css/sprites/">CSS Image Sprites</a>
An extensive tutorial with examples, tips, suggestions and best practices.

Optimize Your Website Using CSS Image Sprites
This very detailed tutorial by Andrew Johnson explains what CSS sprites are, why they are important, how they work and how to implement them.
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55f9af0e-79f4-467d-81d2-7289b0936cbd/4-910d73c375024baa89.gif" border="0" alt="Screenshot" width="401" height="401" /></p>

Animated GIF For CSS Sprites
This article discusses one of the more bizarre uses of CSS sprites: as an animated GIF.
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d257186c-6836-47ab-a520-520ac7c47c08/event-ani-only-sprite.gif" border="0" alt="Screenshot" width="220" height="21" /></p>

<span class="removed_link" title="https://stylemeltdown.com/2007/10/22/image-sprite-navigation-with-css/">Image Sprite Navigation With CSS</span>
Learn how to create a simple menu with the hover effect.
<p class="showcase"><span class="removed_link" title="https://stylemeltdown.com/2007/10/22/image-sprite-navigation-with-css/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4afbf6e-8a76-499f-9cb7-c9f46158aa20/nav-final.jpg" border="0" alt="Screenshot" width="490" height="80" /></span></p>

<a href="https://www.webdesignerwall.com/tutorials/advanced-css-menu/">Advanced CSS Menu</a>
Implement the hover effect with CSS sprites.
<p class="showcase"><a href="https://www.webdesignerwall.com/tutorials/advanced-css-menu/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a063195-57ff-471a-b1d7-8143eadffda6/css-menu5.gif" border="0" alt="Screenshot" width="400" height="220" /></a></p>

<a href="https://davidwalsh.name/css-sprites">Creating and Using CSS Sprites</a>
A very basic tutorial about CSS sprites by David Walsh.
<p class="showcase"><a href="https://davidwalsh.name/css-sprites"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e0f7b60-731f-4596-95f3-a46cd181ee6f/walsh.gif" alt="CSS Sprites Screenshot" width="383" height="150" /></a></p>

## Screencasts about CSS Sprites

How to Use CSS Sprites
David Perel explains the basics of CSS sprites and how to use them in your website design. 10 minutes.

Creating Rounded Buttons With CSS Sprites
Continuing the above sprites tutorial, David shows how to create dynamic rounded-corner buttons with CSS.

<a href="https://nettuts.com/videos/screencasts/exactly-how-to-use-css-sprites/">Exactly How to Use CSS Sprites</a>
In this screencast, Andres Fernandez shows how to use CSS sprites to improve loading time and decrease HTTP requests.

<a href="https://css-tricks.com/video-screencasts/43-how-to-use-css-sprites/">How To Use CSS Sprites</a>
This screencast, Smashing Magazine author Chris Coyier shows how to use CSS sprites in practice, by taking what would have been eight different images and combining them into one. As an added bonus, he then expands on the idea with jQuery by building a little accordion widget.

<a href="https://borkweb.com/story/faster-page-loads-with-image-concatenation">Faster Page Loads With Image Concatenation</a>
For complex web apps, the quantity and resulting latency of icons and images used can greatly affect page load times. And developers usually try to reduce, rather than increase, page load times for their sweet Web apps.

<a href="https://www.csslessons.com/">CSS Image Sprites In 10 Minutes</a>
Another screencast that explains how to use CSS sprites for a navigation menu.

<a href="https://www.sitepoint.com/blogs/2007/07/05/css-using-percentages-in-background-image/">CSS: Using Percentages in Background-Image</a>
This article explains the <code>background-position</code> property, which is essential to implementing CSS sprites.
## CSS Image Maps With CSS Sprites

With CSS Sprites, the hover effect doesn't have to be applied to the whole element. Using a negative <code>background-position</code> value, you can create pure CSS-based image maps. Below, you'll find some techniques in which CSS sprites are used for this purpose.

CSS Image Maps Using Sprites
A basic example of a CSS-based image map with a negative <code>background-position</code> value. Try hovering over the image. Compare this with the <a href="https://www.cssplay.co.uk/menu/imap.html">classic example without CSS sprites</a>.
<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48703ed9-79ce-41ee-a4e6-fe49bbfc58f5/apple-sprite.jpg" alt="Screenshot" width="517" height="202" /></p>

<a href="https://www.alistapart.com/d/sprites/ala-image3.html">City Guide Map Using Sprites</a>
Another example, with horizontally positioned hover areas.
<p class="showcase"><a href="https://www.alistapart.com/d/sprites/ala-image3.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c54ed34-71b7-44e3-acee-c7191a84f31f/maps.jpg" alt="Screenshot" width="403" height="402" /></a></p>

<a href="https://www.frankmanno.com/ideas/css-imagemap/">Advanced Map Using Sprites</a>
A more advanced technique by Frank Manno.
<p class="showcase"><a href="https://www.frankmanno.com/ideas/css-imagemap/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d54431a-c969-40eb-ac6f-50323244098b/advanced.jpg" alt="Screenshot" width="366" height="267" /></a></p>

## CSS Sprites Techniques

<a href="https://alistapart.com/articles/sprites2">CSS Sprites 2</a>
Dave Shea expands on the classic CSS sprites technique with jQuery. His technique allows for animation between link states, while still being fully degradable for visitors who do not have JavaScript enabled.

<a href="https://www.newmediacampaigns.com/page/css-sprites2-refactored-building-an-unobtrusive-jquery-plugin">CSS Sprites2 Refactored: Building an Unobtrusive jQuery Plug-In</a>
Joel Sutherland describes his jQuery plug-in, which cleans up Dave Shea's function and allows for more control over the animation with less initial configuration.
<p class="showcase"><a href="https://www.newmediacampaigns.com/page/css-sprites2-refactored-building-an-unobtrusive-jquery-plugin"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a9308ed-b43a-41a4-8397-13dac745c2db/sprites2.gif" alt="CSS Sprites Screenshot" width="401" height="195" /></a></p>

<a href="https://www.phpied.com/background-repeat-and-css-sprites/">Background Repeat and CSS Sprites</a>
CSS sprites are a great way to improve the loading speed of your pages. One of the problems you might face with sprites is how to deal with cases where the background repeats. The rule is pretty simple: if you want the background to repeat vertically (top to bottom), place the images in the sprite horizontally (left to right) and make sure the individual images in the sprite have the same height. For the opposite case, when you want to repeat horizontally, sprite vertically.

<a href="https://www.interactivellama.com/blog/archives/photoshop-script-combine-two-images-css-hover-css-sprite/">CSS Sprite: Photoshop Script Combines Two Images for CSS Hover</a>
This article presents a simple JSX Photoshop script for creating image sprites, and you can also assign a keyboard shortcut to it.
<p class="showcase"><a href="https://www.interactivellama.com/blog/archives/photoshop-script-combine-two-images-css-hover-css-sprite/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f299632-c641-44b4-80cf-86a7ca09055e/liama.jpg" alt="CSS Sprites Screenshot" width="316" height="280" /></a></p>

<a href="https://www.jennifersemtner.com/css/101/extending-css-spriting/">Extending CSS Spriting</a>
Jennifer Semtner extends the classic CSS sprites technique to non-background images and discusses what to consider when using CSS Sprites for the design.

<a href="https://www.fiftyfoureleven.com/weblog/web-development/css/doors-meet-sprites">Sliding Doors Meets CSS Sprites</a>
Combining the ideas behind Dave Shea's CSS sprites and Douglas Bowman's sliding doors technique, this post assumes you have a good understanding of Bowman's article "<a href="https://www.alistapart.com/articles/slidingdoors/">Sliding Doors of CSS</a>."

<a href="https://trevordavis.net/blog/tutorial/how-to-preload-images-when-you-cant-use-css-sprites/">How to Preload Images When You Can’t Use CSS Sprites</a>
This article addresses the problem that occurs with CSS sprites when the user resizes text. The idea is to combine the images into two images, rather than one. Then you place the image being shown on hover as the background image of another element (preferably a containing element), positioned just off screen.

<a href="https://www.sitepoint.com/blogs/2007/07/20/javascript-sprite-animation-using-jquery/">JavaScript Sprite Animation Using jQuery</a>
Alex Walker combines visual jQuery effects with CSS sprites to achieve the "page turn" effect.
<p class="showcase"><a href="https://www.sitepoint.com/blogs/2007/07/20/javascript-sprite-animation-using-jquery/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baee058b-cc12-446d-acb1-301e9b97396a/turner.gif" alt="CSS Sprites Screenshot" width="348" height="255" /></a></p>

<a href="https://www.julienlecomte.net/blog/2007/07/4/">IE6, CSS Sprites and Alpha Transparency</a>
Julien Lecomte shows how to combine CSS sprites, PNG transparency and Internet Explorer 6 compatibility using the AlphaImageLoader hack.
## CSS Sprite Generators
<a href="https://duris.ru/lang/en/">Data URI Sprites</a>
DURIS (Data URI [CSS] Sprites) is a new method to manage website's background images. It's aimed to replace classical CSS Sprites. The new technique allows you to apply any corrections to your make-up, allows you to minimize number of requests for design-related data that is used on the webpage and uses text (non graphic) format of image data presentation. It also solves all problems with scaling for background images and combines images of different types and axes of repetition.
<p class="showcase"><a href="https://duris.ru/lang/en/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b93d763-0195-4c5a-8359-9936c0b90f11/data.gif" border="0" alt="Screenshot" width="497" height="303" /></a></p>

<a href="https://printf.ru/spritr/">Spritr</a>
This simple tool lets you upload multiple images and generates CSS code for the sprite.

<a href="https://www.floweringmind.com/sprite-creator/index.php">Sprite Creator 1.0</a>
This tool allows you to upload an image and create the CSS code for selected areas of the sprite.

<a href="https://drupal.org/project/sprites">CSS Sprite Generator</a>
A Drupal module for building CSS sprites.

<a href="https://www.csssprites.com/">CSS Sprites Generator</a>
This tool allows you to upload multiple files and generate a sprite out of them. It also gives you the CSS code (the <code>background-position</code> value) for each image in the sprite.

<a href="https://spritegen.website-performance.org/">Projekt Fondue CSS Sprite Generator</a>
This generator lets you ignore duplicate images, resize source images, define horizontal and vertical offset, define background and transparency color, assign CSS class prefixes and various other things. It also supports many languages. The source code is available for downloading and is covered by a BSD license. Want to run a local copy? Well, you can do that, too.
<p class="showcase"><a href="https://spritegen.website-performance.org/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bafe1c3d-2f88-4b3f-ad31-9631b6e2800e/spritegen.gif" border="0" alt="Screenshot" width="511" height="492" /></a></p>

<a href="https://smartsprites.osinski.name/">SmartSprites</a>
A Java-based desktop application that parses special directives that you can insert into your original CSS to mark individual images to be turned into sprites. It then builds sprite images from the collected images and automatically inserts the required CSS properties into your style sheet, so that the sprites are used instead of the individual images.

You can work with your CSS and original images as usual and have SmartSprites automatically transform them to the sprite-powered version when necessary. A <a href="https://www.tanila.de/smartsprite/index.php">PHP version</a> is available as well. Open-source. Check also <a href="https://tanila.de/smartsprite/index.php">Chris Brainard's Sprite Creator 1.0</a>.
## Bonus: How Does The background-position Property Work?

The <code>background-position</code> property, together with <a href="https://www.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/">CSS specificity</a> and <a href="https://www.smashingmagazine.com/2007/05/01/css-float-theory-things-you-should-know/">CSS floats</a>, is probably one of the most confusing and counter-intuitive of CSS properties.

According to CSS specifications, the <code>background-position</code> takes two (optional) arguments: <code>horizontal</code> position and <code>vertical</code> position. For example:

<pre><code class="language-css">.introduction {
    background-image: url(bg.gif);
    background-position: [horizontal position] [vertical position];
    }</code></pre>

Using this property, you can define the exact position of the background image for the block-level element (list item <code>li</code>). You can use either <code>%</code> or <code>px</code> units (or mix both) to define the starting position (i.e. the upper-left corner) of the displayed part of the master image. Alternatively, you could use the following keywords: top left, top center, top right, center left, center center, center right, bottom left, bottom center, bottom right.

Hence, in <code>background-position: x% y%</code>, the first value is the horizontal position, and the second value is the vertical position. The top-left corner is <code>0% 0%</code>. The bottom-right corner is <code>100% 100%</code>. <strong>If you specify only one value, the other value will be 50%</strong>.

For instance, if you use,

<pre><code class="language-css">ul li {
    background-image: url(bg.gif);
    background-position: 19px 85px;
    },</code></pre>

... then the <strong><code>background-image</code> will be positioned</strong> 19 pixels from the left and 85 pixels from the top of the list item element.

As <a href="https://reference.sitepoint.com/css/background-position">SitePoint's reference article explains</a>: "a <code>background-image</code> with <code>background-position</code> values of <code>50% 50%</code> will place the point of the image that’s located at 50% of the image’s width and 50% of the image’s height at a corresponding position within the element that contains the image. In the above case, this causes the image to be perfectly centered. This is an important point to grasp -- using background-position isn’t the same as placing an element with absolute position using percentages where the top-left corner of the element is placed at the position specified."

You can find a detailed explanation of the property in the article "<a href="https://reference.sitepoint.com/css/background-position">background-position (CSS property)</a>" on SitePoint.
## Related posts

You may want to take a look at the following related posts:
<ul>
  <li><a href="https://www.smashingmagazine.com/2007/01/19/53-css-techniques-you-couldnt-live-without/">53 CSS-Techniques You Couldn't Live Without</a></li>
  <li><a href="https://www.smashingmagazine.com/2008/02/21/powerful-css-techniques-for-effective-coding/">Powerful CSS-Techniques For Effective Coding</a></li>
  <li><a href="https://www.smashingmagazine.com/2008/12/09/50-really-useful-css-tools/">50 Extremely Useful and Powerful CSS Tools</a></li>
  <li><a href="https://www.smashingmagazine.com/2007/05/01/css-float-theory-things-you-should-know/">CSS Float Theory</a></li>
  <li><a href="https://www.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/">CSS Specificity</a></li>
</ul>

{{< signature "al" >}}


---
title: 'Fixed Elements And Overlays In XD: Incredibly Easy And Fun Methods For Your Prototypes'
slug: >-
  fixed-elements-overlays-methods-prototypes
author: manuelalangella
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fb7cd135-6996-49b0-a683-e227776bdfa2/18-fixed-elements-and-overlays-in-xd.png
date: 2018-09-18T12:30:32+02:00
summary: >-
  Over the summer, Adobe XD released two great prototyping features: fixed elements and overlays. When you work with prototypes and want them to be more interactive, functions like these will be very helpful.
description: >-
  Over the summer, Adobe XD released two great prototyping features: fixed elements and overlays. When you work with prototypes and want them to be more interactive, functions like these will be very helpful.
categories:
  - Illustrator
  - Wireframing
  - Prototyping
disable_panels: true
disable_ads: true
---
<p>(This article is kindly sponsored by Adobe.) A fixed element is an object you set to a fixed position on the artboard, allowing other items to scroll underneath. This way, you get a realistic simulation of scrolling on desktop and mobile. With the new overlay feature, you can simulate interactions such as lightbox effects and submenus.</p>

<p>How do famous brands use fixed elements and overlays? Well, let’s take a look at some examples to get some inspiration first.</p>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acfd8276-131c-4969-905d-0ea7a2ab82bb/grid-examples-of-fixed-elements-and-overlays.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acfd8276-131c-4969-905d-0ea7a2ab82bb/grid-examples-of-fixed-elements-and-overlays.jpg" sizes="100vw" caption="From left to right: 1) McDonald’s mobile home 2) A submenu slides up when you click on the hamburger menu. This is an example of an overlay. 3) Netflix’s Italian mobile website home screen. 4) Netflix sets its call to action as a fixed element. When you scroll down, the button stays fixed to the bottom of the screen. 5) Adobe mobile home 6) By clicking on the menu symbol, a submenu comes out as an overlay. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acfd8276-131c-4969-905d-0ea7a2ab82bb/grid-examples-of-fixed-elements-and-overlays.jpg'>Large preview</a>)" alt="Examples of brands using fixed elements and overlays" >}}

<p>In this tutorial, we will learn how to set a menu bar as a fixed element and how to apply an overlay transition in a prototype, to simulate a menu opening from the click of a button. Both examples will be done in a mobile template, so that we can see our simulation in action directly on our mobile device. I’ve also included an Illustrator file with icons, which you can use to set up your examples quickly.</p>

<p>Let’s get started.</p>

## Preparing The Mobile Template

<p>Open Adobe Xd, and choose the “iPhone 6/7/8 Plus” template. Then, go to <code>File &rarr; Save As</code> and choose a name to save your file (mine is <code>mobile.xd</code>).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36c98261-a74a-4b8e-8801-0135d7d17f97/1-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36c98261-a74a-4b8e-8801-0135d7d17f97/1-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36c98261-a74a-4b8e-8801-0135d7d17f97/1-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Let’s create a restaurant app in which people can select what to order from a list of food.</p>

<p>We will create two home layouts. The first one will be a long page, which we will use to see how fixed navigation works. The second will have a full-screen image, and the user will be able to click and open a menu bar that overlays the home screen.</p>

<p>To get started, click on the artboard icon on the left side, and click to the right of your current artboard. This will create a second identical artboard, near the first one.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6d1e983-9ca5-41e6-9783-995b3befb160/2-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6d1e983-9ca5-41e6-9783-995b3befb160/2-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6d1e983-9ca5-41e6-9783-995b3befb160/2-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Let’s begin to design our elements, starting with the navigation bar. Click on the Rectangle tool (R) and draw a shape 414 pixels wide and 48 pixels tall. Set its color as <code>#DE4F4F</code>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13e22a87-f23f-4901-8df8-37b457e445d1/3-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13e22a87-f23f-4901-8df8-37b457e445d1/3-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13e22a87-f23f-4901-8df8-37b457e445d1/3-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>I’ve prepared some icons in Illustrator to use in our layout. Just open the <a href="https://smashingmagazine.com/provide/fixed-elements-overlays-methods-prototypes-icons.ai">Illustrator file I’ve provided</a>, and drag and drop the icons in your library, as shown below:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147654fe-b40d-4b65-af1f-7241f0525f96/3a-fixed-elements-and-overlays-in-xd.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b2ab19c-f2dc-4a1e-a426-2d88f02577aa/3a-fixed-elements-and-overlays-in-xd-800w.gif" width="800" height="" alt="" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/147654fe-b40d-4b65-af1f-7241f0525f96/3a-fixed-elements-and-overlays-in-xd.gif">Large preview</a></figcaption></figure>

<p>In doing so, your icons will be automatically uploaded to your Adobe XD library, too.</p>

<p>To learn more about how to use libraries in different apps, read <a href="https://www.smashingmagazine.com/2018/02/user-interfaces-icons-visual-elements-screen-design/">my earlier article</a>, in which I go over some examples of how to add icons and elements to a library (in Illustrator, for instance) and then access them by opening that library in other apps (XD, in this case).</p>

<p>Once you have added the icons, open your XD library. You should see the icons in place:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a8c8e16-e4d8-4a53-b88c-ce54874d8d72/4-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a8c8e16-e4d8-4a53-b88c-ce54874d8d72/4-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a8c8e16-e4d8-4a53-b88c-ce54874d8d72/4-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Drag and drop the icons on your artboard, as shown below. Position them, and make sure they are all about 25 pixels wide.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cdb3f69-26bf-4949-abc2-44c3ddd101a6/5-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cdb3f69-26bf-4949-abc2-44c3ddd101a6/5-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cdb3f69-26bf-4949-abc2-44c3ddd101a6/5-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Because we need our icons to be white, we have to modify these. We can directly modify them in the library, as demonstrated <a href="https://www.smashingmagazine.com/2018/06/wireframing-process-photoshop-xd/">in my previous tutorial</a>. With that done, we’ll see them updated in XD directly, without having to drag them from the library again.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1fb3336-089d-419b-8eee-863cf253cb5f/6-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1fb3336-089d-419b-8eee-863cf253cb5f/6-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1fb3336-089d-419b-8eee-863cf253cb5f/6-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Now that the icons we want are in place, let’s create a logo. Let’s call this app “Gusto”. We’ll simply use the Text tool to add it. (I’m using the <a href="https://fonts.google.com/specimen/Leckerli+One">Leckerli One</a> font here, but feel free to use whichever you like.) Align the logo to the middle of the navigation bar by clicking “Align center (horizontally)” in the right sidebar.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c26ab93a-9756-4171-97f2-dbc89dc1481e/7-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c26ab93a-9756-4171-97f2-dbc89dc1481e/7-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c26ab93a-9756-4171-97f2-dbc89dc1481e/7-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Group all of the navigation elements together, and call the group “Menu”. To do this, select all elements in the left panel, right-click and choose “Group”.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df851ae9-bfe3-42c3-8d42-0939ae6dc324/8-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df851ae9-bfe3-42c3-8d42-0939ae6dc324/8-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df851ae9-bfe3-42c3-8d42-0939ae6dc324/8-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/297fa632-3a2f-4f0a-9c8f-6dabb4399eac/9-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/297fa632-3a2f-4f0a-9c8f-6dabb4399eac/9-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/297fa632-3a2f-4f0a-9c8f-6dabb4399eac/9-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Let’s add a beautiful hero image. I selected <a href="https://www.pexels.com/photo/food-salad-restaurant-person-5317/">one from Pexels</a>. Drag it on your artboard, and resize its height to 380 pixels.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e2a3eaa-4c17-4ca9-9c88-6fdfe39eb72a/10-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e2a3eaa-4c17-4ca9-9c88-6fdfe39eb72a/10-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e2a3eaa-4c17-4ca9-9c88-6fdfe39eb72a/10-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Now, click on Rectangle tool (R), and draw a rectangle the same size as the hero image, and place it on the image. Set a gradient for the rectangle’s color, using the values shown in the image below.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40209403-7ece-411d-b6c7-4e8a95aea414/11-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40209403-7ece-411d-b6c7-4e8a95aea414/11-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40209403-7ece-411d-b6c7-4e8a95aea414/11-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>(If you’d like more information about gradients, feel free to see <a href="https://www.smashingmagazine.com/2018/01/gradients-user-experience-design/">my previous tutorial</a> on how to apply them in XD.)</p>

<p>Insert some white text on the hero image and a circle for a button. Place a little circle with a number on the cart icon as well; we will need it later.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f1ce70d-7c09-4908-bfc1-890f0d6a68fa/12-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f1ce70d-7c09-4908-bfc1-890f0d6a68fa/12-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f1ce70d-7c09-4908-bfc1-890f0d6a68fa/12-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Next, let’s increase the artboard’s height. We have to do that in order to insert new elements and to create the scrolling simulation.</p>

<p>After double-clicking on the artboard, set its height to 1265 pixels. Be sure that “Scrolling” is set to “Vertical” and that the “Viewport Height” is set to 736 pixels. A little blue marker will allow you to set the scrolling boundary towards the bottom of the artboard, as seen below:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ecd16be-4fae-4ea7-90f0-16436e630ad8/13-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ecd16be-4fae-4ea7-90f0-16436e630ad8/13-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ecd16be-4fae-4ea7-90f0-16436e630ad8/13-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Let’s add in our content: Gusto’s mouthwatering menu. Click on the Rectangle tool (R) to create a rectangle for the picture that we will add.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66a6970d-ecd9-491e-a28b-dbf7798fafcd/13b-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66a6970d-ecd9-491e-a28b-dbf7798fafcd/13b-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66a6970d-ecd9-491e-a28b-dbf7798fafcd/13b-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Drag and drop a picture directly into the box we just created; the image will automatically fit in it. Click on it once, and drag the little white circle from an angle inwards, in order to round all of the angles. Their values should be around 25, as shown in the picture below. Get rid of the border by unchecking the border value in the right sidebar.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04b97e7f-fe0f-47e0-baf4-d07493ec7af1/13c-fixed-elements-and-overlays-in-xd.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52457f79-1730-4524-80f0-ca01621c1d0d/13c-fixed-elements-and-overlays-in-xd-800w.gif" width="800" height="" alt="" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04b97e7f-fe0f-47e0-baf4-d07493ec7af1/13c-fixed-elements-and-overlays-in-xd.gif">Large preview</a></figcaption></figure>

<p>Click on the Text tool (T), and write a title on the right side of the image. I chose Lato as the font, at 14 pixels. Feel free to use another font, but maintain the 14-pixel size.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a82e629-4a84-4f52-ade0-f12b24956fc5/13d-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a82e629-4a84-4f52-ade0-f12b24956fc5/13d-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a82e629-4a84-4f52-ade0-f12b24956fc5/13d-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Grab the Text tool (T) again, and write some lines for the description (Lato, 10 pixels) and for the price (Lato, 16 pixels).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/302ce9af-3eb5-4229-80a3-5a837f905a4e/13e-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/302ce9af-3eb5-4229-80a3-5a837f905a4e/13e-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/302ce9af-3eb5-4229-80a3-5a837f905a4e/13e-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Take the Rectangle tool (R) and draw a rectangle of 100 by 30 pixels. Color it with the same orange we used on the button for the hero image; add the text “Add to Cart” with the Text tool (T); and add the cart icon from the library. All of these steps are covered in the short video below:</p>

<div class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/287799821" width="640" height="369" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

<p>Finally, click on “Repeat Grid” to create a grid for this section. Once that’s done, we can change images and text easily, as shown in the video below:</p>

<div class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/287971103" width="640" height="369" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

<p>If you want to learn more about how to create grids, follow <a href="https://www.smashingmagazine.com/2018/03/prototyping-photoshop-adobexd-apps-design/">my tutorial</a>.</p>

<p>I used the following pictures from Pexels:</p>

<ul>
<li>https://www.pexels.com/photo/close-up-of-food-247685/</li>
<li>https://www.pexels.com/photo/food-dinner-pasta-spaghetti-8500/</li>
<li>https://www.pexels.com/photo/selective-focus-photography-of-beef-steak-with-sauce-675951/</li>
<li>https://www.pexels.com/photo/food-plate-chocolate-dessert-132694/</li>
<li>https://www.pexels.com/photo/bread-food-sandwich-wood-62097/</li>
</ul>

<p>Add some titles, descriptions and buttons.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69d7a528-e949-4022-92eb-84362ddfa529/14-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69d7a528-e949-4022-92eb-84362ddfa529/14-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69d7a528-e949-4022-92eb-84362ddfa529/14-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Finally, let’s add a rectangle for the footer, with the text “Gusto” in the center. Set the rectangle’s fill color to <code>#211919</code>.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8071b30e-7ab4-480d-b1e7-86aa07ffd105/15-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8071b30e-7ab4-480d-b1e7-86aa07ffd105/15-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8071b30e-7ab4-480d-b1e7-86aa07ffd105/15-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Yes! We’ve completed the first template design. Let’s set up our second template before we begin prototyping.</p>

<p>For our second mobile layout, just copy and paste the navigation and hero section from the first layout, and size the hero image to be full screen. Then, add a “Try Now” button to it.</p>

<p>In the short video below, I show you how to copy and paste elements into the second artboard, create a new button with the Rectangle tool (R) and write text on it with the Text tool (T).</p>

<div class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/287794968" width="640" height="369" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43c2e2a0-6d04-4c61-818d-1474886eb350/16-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43c2e2a0-6d04-4c61-818d-1474886eb350/16-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43c2e2a0-6d04-4c61-818d-1474886eb350/16-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Excellent! Let’s move on and create our prototypes.</p>

## Setting Fixed Elements

<p>We want to make the top navigation of our layout fixed, making it stick to its position as we scroll the artboard.</p>

<p>Click on your “Menu” group to select it, and select “Fixed Position” in the right sidebar.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c72bffe9-c666-4385-8db8-4896cc314ad0/17-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c72bffe9-c666-4385-8db8-4896cc314ad0/17-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c72bffe9-c666-4385-8db8-4896cc314ad0/17-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p><strong>Important:</strong> In order for all elements to scroll under the menu, the menu should be on top of all other elements. Simply place the menu folder at the top, in the left sidebar.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a361a63d-6f09-4eb4-b169-0e7fb390a85e/18-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a361a63d-6f09-4eb4-b169-0e7fb390a85e/18-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a361a63d-6f09-4eb4-b169-0e7fb390a85e/18-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Now, to see your fixed navigation in action, simply click on the “Desktop Preview” button and try scrolling. You should see this:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fedd99a-1568-4efb-aa46-b694731484ea/19-fixed-elements-and-overlays-in-xd.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fc00886-33c4-4595-98e2-153094b49870/19-fixed-elements-and-overlays-in-xd-800w.gif" width="800" height="" alt="" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fedd99a-1568-4efb-aa46-b694731484ea/19-fixed-elements-and-overlays-in-xd.gif">Large preview</a></figcaption></figure>

<p>Tremendously simple, isn’t it?</p>

## Setting Overlay Elements

<p>To see how overlays work in XD, we first need to create the elements that will be overlaid. When you click an item in the menu, what would you expect to happen? Exactly: A submenu should appear.</p>

<p>Let’s create three different submenus, like the ones in the image below, using the Rectangle tool (R). I chose a rectangle because the menu will overlay the screen, so it will cover not the whole artboard but just a part of it.</p>

<p>Follow the video below to see how I created the three overlay menus. You will see that I  used the Rectangle tool (R), Line tool (L) and Text tool (T). We’re using rectangles to create the menu backgrounds because we need an object to overlay the screen. I’ve included the icons in the Adobe Illustrator file which you can directly download over <a href="https://smashingmagazine.com/provide/fixed-elements-overlays-methods-prototypes-icons.ai">here</a>.</p>

<p>Below, you’ll see how I use “Repeat Grid” and how I modify elements inside of it.</p>

<div class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/287796096" width="640" height="369" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

<div class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/287796351" width="640" height="369" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

<div class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/287796590" width="640" height="369" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

<p>Here is the final result:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffb7a14-53cf-421f-81b6-fcaf0534cf61/20-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffb7a14-53cf-421f-81b6-fcaf0534cf61/20-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffb7a14-53cf-421f-81b6-fcaf0534cf61/20-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>We will work on the second home layout at this point.</p>

<p>Set the visual mode to “Prototype”, selecting it from the top left of the screen.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec982cfa-bb3d-49ad-a4e5-d69a502f55da/21-fixed-elements-and-overlays-in-xd.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec982cfa-bb3d-49ad-a4e5-d69a502f55da/21-fixed-elements-and-overlays-in-xd.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec982cfa-bb3d-49ad-a4e5-d69a502f55da/21-fixed-elements-and-overlays-in-xd.png'>Large preview</a>)" alt="" >}}

<p>Next, double-click on the little hamburger menu icon, and drag and drop the little blue arrow onto the “Overlay 1” artboard. When the popup window appears, choose “Overlay” and “Slide right”. Then, click the “Desktop Preview” button to see it in action.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a88a71f-6761-4011-94b5-8dd00d0d40ec/22-fixed-elements-and-overlays-in-xd.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/503e1144-01c7-4f02-9847-5ba669635874/22-fixed-elements-and-overlays-in-xd-800w.gif" width="800" height="" alt="" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a88a71f-6761-4011-94b5-8dd00d0d40ec/22-fixed-elements-and-overlays-in-xd.gif">Large preview</a></figcaption></figure>

<p>Let’s do the same thing with the user icon and cart icon. Double-click on the user icon in Prototype mode, and drag and drop the little blue arrow onto the “Overlay 2” artboard. When the popup window appears, choose “Overlay” and “Slide left”. Then, click the “Desktop Preview” button to see it in action.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfd03820-3899-4266-a7c7-55a2ab934a48/23-fixed-elements-and-overlays-in-xd.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80285195-905e-4406-8089-1d141c093fe2/23-fixed-elements-and-overlays-in-xd-800w.gif" width="800" height="" alt="" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfd03820-3899-4266-a7c7-55a2ab934a48/23-fixed-elements-and-overlays-in-xd.gif">Large preview</a></figcaption></figure>

<p>Now, double-click on the cart icon in Prototype mode, and drag and drop the little blue arrow onto the “Overlay 3” artboard. When the popup windows appears, choose “Overlay” and “Slide left”. Click the “Desktop Preview” button again to see it work.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f24b2b7-050c-45b9-a7c8-f03b0897a704/24-fixed-elements-and-overlays-in-xd.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6c755a3-ac8a-4a11-81f7-9b64d5bcdab9/24-fixed-elements-and-overlays-in-xd-800w.gif" width="800" height="" alt="" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f24b2b7-050c-45b9-a7c8-f03b0897a704/24-fixed-elements-and-overlays-in-xd.gif">Large preview</a></figcaption></figure>

<p>We’re done! These great new features are super-easy to learn, and they’ll add a new level of interactivity simulation to your prototypes.</p>

<p><strong>Quick tip:</strong> Want to preview the layout on your phone? Just upload your XD file to Creative Cloud, <a href="https://www.adobe.com/products/xd.html#mobile">download the XD app</a> for mobile, and open your document.</p>

<p>Here’s what we have learned in this tutorial:</p>

<ul>
<li>set and create mobile layouts and elements,</li>
<li>set fixed elements,</li>
<li>use overlays to simulate a click-to-open submenu.</li>
</ul>

<p>Where would you use fixed elements or overlays? Feel free to share your examples in the comments below!</p>

<p><em>This article is part of the UX design series sponsored by Adobe. Adobe XD is made for a <a href="https://adobe.ly/2IkzKMF">fast and fluid UX design process</a>, as it lets you go from idea to prototype faster. Design, prototype and share — all in one app. You can check out more inspiring projects created with <a href="https://www.behance.net/galleries/adobe/5/XD">Adobe XD on Behance</a>, and also <a href="https://adobe.ly/2yKueO8">sign up for the Adobe experience design newsletter</a> to stay updated and informed on the latest trends and insights for UX/UI design.</em></p>

{{< signature "il, yk" >}}
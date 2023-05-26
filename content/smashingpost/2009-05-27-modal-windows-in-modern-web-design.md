---
title: Modal Windows In Modern Web Design
slug: modal-windows-in-modern-web-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/311cb243-fd8f-4190-9e1a-ed8dcefe4042/modal-window.jpg
date: 2009-05-27T22:40:13.000Z
author: matt-cronin
description: >-
  Web design is essentially the organization of information into a readable,
  usable, functional and accessible format. Good organization of content is
  crucial, and you need a strong layout that you can build a website upon. You
  can use numerous interface elements and structures to organize content, such
  as jQuery-based content sliders and **modal windows**, which are basically
  windows that float above the page.

  The modal window has many advantages. For example, when a modal window
  contains a smaller element, the user doesn't need to load an entirely new page
  just to access it (another way to achieve the same effect is e.g. by using
  AJAX-based tabs). By providing modal windows, you improve the usability of
  your website. Having to load pages over and over will annoy most users, so
  avoiding that is definitely a good thing. Modal windows also allow you to save
  space by getting rid of large elements that don't need to be on the main page.
  For example, rather than putting a full video on a page, you can just provide
  a link, thumbnail or button of some sort.

  In this article, we'll go over **best practices and trends for working with
  and building modal windows**. We'll also provide numerous examples of
  well-constructed modal windows and a few scripts to get you started with
  building them.
categories:
  - Inspiration
  - Showcases
  - User Interaction
---
Web design is essentially the organization of information into a readable, usable, functional and accessible format. Good organization of content is crucial, and you need a strong layout that you can build a website upon. You can use numerous interface elements and structures to organize content, such as jQuery-based content sliders and <strong>modal windows</strong>, which are basically windows that float above the page.

The modal window has many advantages. For example, when a modal window contains a smaller element, the user doesn't need to load an entirely new page just to access it (another way to achieve the same effect is e.g. by using AJAX-based tabs). By providing modal windows, you improve the usability of your website. Having to load pages over and over will annoy most users, so avoiding that is definitely a good thing. Modal windows also allow you to save space by getting rid of large elements that don't need to be on the main page. For example, rather than putting a full video on a page, you can just provide a link, thumbnail or button of some sort.

In this article, we'll go over <strong>best practices and trends for working with and building modal windows</strong>. We'll also provide numerous examples of well-constructed modal windows and a few scripts to get you started with building them.

You may be interested in the following related posts:

*   [30 Scripts For Galleries, Slideshows and Lightboxes](https://www.smashingmagazine.com/2007/05/18/30-best-solutions-for-image-galleries-slideshows-lightboxes/)
*   [How To Use Help Elements To Improve Your Designs](https://www.smashingmagazine.com/2009/04/23/help-elements-design-showcase/)
*   [8 Layout Solutions To Improve Your Designs](https://www.smashingmagazine.com/2009/05/19/8-layout-solutions-to-improve-your-designs/)
*   [Designing Drop-Down-Menus: Examples and Best Practices](https://www.smashingmagazine.com/2009/03/24/designing-drop-down-menus-examples-and-best-practices/)
*   [Breadcrumbs in Web Design](https://www.smashingmagazine.com/2009/03/17/breadcrumbs-in-web-design-examples-and-best-practices-2/)

{{% feature-panel %}}

## When to Use Modal Windows

Modal windows are an excellent structural element, but they don't work for every type of content or media. Here are few elements for which you <em>should</em> consider using modal windows.</p>

### Lightbox for Images/Videos

The most obvious use of modal windows is for the lightbox, which showcases images and video in a clean and usable fashion. By using a lightbox for images, users don't have to load a new page just to view a single image or video. Modal windows also save space in the content layout by allowing you to show only the thumbnail of an image or video, which opens the modal window when clicked. By using a thumbnail instead of the entire element, you take up much less space and the layout looks more organized.

Furthermore, you would usually blur or fade out the background behind a modal window, putting the focus on the image or video itself, thus creating an excellent environment in which site visitors can view the media. For details on fading and blurring out the background of a modal window, see the styling practices outlined below.

When using a lightbox for an image gallery, be sure to link every image to the same lightbox, providing "Next" and "Previous" buttons to allow users to navigate the image set with ease. The user then does not have to close and re-open the modal window to view each image in the gallery.</p>

### Contact Forms

One often sees contact forms contained in modal windows. Modal windows work well for this purpose because you don't have to create a full page for the function. In terms of usability, it is important for contact forms to be immediately available and easy to find. By using a floating window, contact forms are easily accessible on each and every page. Contact forms are generally small, so they will fit quite nicely in these windows.

<a href="https://wpcoder.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f097a8be-0317-427b-8f57-a5d3d780fe23/wpcoder.jpg" alt="" /></a>

### Sign-Up/Log-In Forms

Instead of creating a separate page for users to log in to and sign up for your website, you can use a modal window, which is actually often used for this purpose. This approach makes the form available on each page for easier access. You can include a link to the log-in window in the header of the website.</p>

### Alerts/Notices

When you want to alert users of a critical function or an action taking place, the best way to do so is through a modal window. When a modal window opens on a page, the user cannot ignore it because it will appear directly in the middle of the screen, right where the user is looking. Furthermore, the rest of the content will be faded out and disabled, so the user can't do anything else until they look at the window and click to close it. In the screenshot below, you can see a modal window being used to alert users to a download. 

<a href="https://www.versionsapp.com/#"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29ec58d9-29e6-4a75-88cb-39407526aee7/versions.jpg" alt="" /></a>

Please notice that you should not use modal window as an alternative pop-up-approach. Please make sure to alert your visitors only in case something cruical to the current browsing session has taken place. In many situations, a simple faded block in the layout would work better than a modal window.</p>

### Help Elements/Tips

Additional help elements and tips aren't essential to the functionality and navigation of a website, so you don't want them to take up space and get in the way of content. Not all users want to use them anyway. However, they need to be conveniently located for those who do want to use them, so it seems reasonable to show help elements and tips in modal windows. Users can easily open and close them, without them getting in the way of content and functionality.

Here below is a good example of a help element in a floating window. This window is much smaller than the other ones we've seen; but it contains similar functions. For example, a semi-transparent border for visual separation and an "exit" (close-) button in the top-right corner.

<a href="https://www.footnote.com/search.php?query=john%20hancock"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61962e48-5601-4a04-91d3-1579d6694d10/footnote.jpg" alt="" /></a>

### Search Boxes

This is a less common practice, but you will occasionally see modal windows containing search boxes. Advanced search functionality can take up quite a bit of room, so to prevent a large search box from taking space away from the content, you can put it in a floating window. You can see this in practice in the screenshot below.

<a href="https://collabfinder.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9efba7c3-3398-4637-a2a4-be8905e7ec6d/collabfinder.jpg" alt="" /></a>

### Embedding PDFs

Sometimes you need to embed files on your website, such as a PDF of your résumé. Instead of providing a link that users can click on to download the PDF to their computer or embedding the PDF some other way, you can use a modal window for the same purpose. This way, the PDF can be easily viewed without disrupting the user's experience of the website. By blurring the background, you also bring focus to the PDF, which improves usability.</p>

## Usability and Styling Practices

The following is a list of usability and styling practices and trends to keep in mind when building your modal windows.</p>

### Blur and Fade Out Background of Window

Foremost in importance for usability and styling is fading out the page behind a floating window. You will see this practiced nearly everywhere, most often with lightboxes for media. By fading out the page, you bring all of the user's attention to the floating window. If the background doesn't fade, the user may not even realize right away that the window is "floating" above the page and is not a part of the main layout. The appearance of a window physically floating above the page also gives your website dimension. It looks cleaner and eliminates confusion. Overall, the fading provides much needed separation between the window and the page, improving functionality and usability.

Make sure the fade is heavy, but leave a slight opacity, so that the user knows the page hasn't disappeared. For example, a black fade with about 75% opacity would work well. But for websites with a white background, fade the page with white with a slight opacity, and use a drop-shadow.

Sometimes you will see a modal window that doesn't fade out the entire page but instead has a strong drop-shadow below it to add dimension. This creates the same effect and provides a similar visual separation. You can see this technique used perfectly in the screenshot below.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b0c07ff-39cc-4d84-b028-24ee7c18d6db/rapidweaver.jpg" alt="" />

### Exit Strategy: Button, Click Outside Window, Escape Key

To improve functionality, always provide an exit button in an upper corner of the window. It is standard practice to use a simple circular button with an "x" graphic, which is clean and quite obvious for the user. In the lightbox shown below, you can clearly see the exit button.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b350e266-9fe4-478e-8080-5ea4216ebb82/wdw.jpg" alt="" />

Other methods of allowing users to close modal windows is to let them click outside the window on the page behind, to click on the displayed element in the modal window or to hit the Escape key once.</p>

### <del>Disable All Other Page Functions</del>

<del>Disable all functionality of the page behind the window. It should be focused out, and no buttons should be able to be clicked when the modal window is open. The floating window should be separated from the rest of the content, so disabling the page below creates a better separation. Keeping page scrolling functionality is a good idea, though, so that users have at least some freedom to refer back to the page if needed.</del>

### Using Transition Effects

Transition effects are small details that look very nice if done correctly. One good transition effect for modal windows is fading in and out. But don't overdo it to the point of annoying users. Keep the fade brief but slightly noticeable.

In the example below, the blurred gray backdrop fades in and out, creating a great effect.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e25055f-5837-4988-8ecd-5ed08b5f0728/fontcase.jpg" alt="" />

## Scripts, Tools and Plug-Ins For Lightboxes and Modal Windows

When you start the process of integrating modal windows, you'll probably want something to build off of. Here are 11 excellent jQuery scripts and plug-ins on which to base your modal windows. Each has its own unique features and functions, so check them all out.

<a href="https://fancy.klade.lv/home">Fancy Lightbox</a>
This is one of the better lightbox jQuery plug-ins. It's well styled and very functional. It has clean styling, labeling features and website integration, and it works with AJAX.

<a href="https://fancy.klade.lv/home"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40ec9a25-5f26-40fa-b4fa-bd44097e8eb4/fancylightbox.jpg" alt="" /></a>

<a href="https://www.lokeshdhakar.com/projects/lightbox2/">Lightbox 2</a>
This is the original lightbox script, built only for images. It's simply styled and supports image set viewing.

<a href="https://www.lokeshdhakar.com/projects/lightbox2/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22d9984f-2bf8-4b33-8d55-41e035bab3c5/lightbox2.jpg" alt="" /></a>

<a href="https://www.dynamicdrive.com/dynamicindex4/facebox/index.htm">Facebook Image/Content Viewer</a>
Here is an excellent script, based on Facebook's floating window. This one supports images and content and is styled similar to Facebook's well-known window.

<a href="https://www.dynamicdrive.com/dynamicindex4/facebox/index.htm"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f7874da-28dd-4017-9b01-c24836297e84/facebookmodal.jpg" alt="" /></a>

<span class="removed_link" title="https://woork.blogspot.com/2008/01/lightbox-using-mootools-and-pathfusion.html">Woork Mootools Lightbox</span>
This excellent tutorial from Woork shows you how to create a simple lightbox script. The script includes image set functions and label features.

<span class="removed_link" title="https://woork.blogspot.com/2008/01/lightbox-using-mootools-and-pathfusion.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a199b579-2e46-4b62-9427-ea4c2dbdaa1a/woorklightbox.jpg" alt="" /></span>

<a href="https://nyromodal.nyrodev.com/">nyroModal jQuery Plug-In</a>
This simple window plug-in supports all types of media and file scripts, including AJAX. It also has some great show/hide effects.

<a href="https://nyromodal.nyrodev.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2ed6787-bb2a-4437-b12d-92a0ecf2504f/nyromodal.jpg" alt="" /></a>

<a href="https://nyromodal.nyrodev.com/">jQuery Alert Dialog</a>
This jQuery plug-in is for alert and dialog boxes. It has numerous functions and works very nicely for sending messages to users.

<a href="https://nyromodal.nyrodev.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93f2c0f9-d728-44d4-b4fa-2121286621b6/alertbox.jpg" alt="" /></a>

LightWindow
Here is a comprehensive lightbox script with many features, such as PDF embedding, multiple image gallery support, SWF implementation and more.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17afba4d-99c6-454c-82aa-78f5948c61a5/grooveshark.jpg" alt="" />

<a href="https://prototype-window.xilinus.com/">Prototype Window Class</a>
Another in-depth set of scripts with different functions, such as dialog boxes, log-in windows, AJAX content windows, image lightboxes and more.

<a href="https://prototype-window.xilinus.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64b2ec05-9f2e-4844-9752-25e2c619af68/windowclass.jpg" alt="" /></a>

<a href="https://prototype-window.xilinus.com/">ThickBox 3.1</a>
One of the more popular lightbox tools, ThickBox. It works with images, inline content and AJAX.

<a href="https://prototype-window.xilinus.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5de7407c-7884-479f-b3d0-40e6b8b893b5/thickbox.jpg" alt="" /></a>

<a href="https://www.no-margin-for-errors.com/projects/prettyPhoto-jquery-lightbox-clone/">prettyPhoto</a>
A well-styled image lightbox that works nicely with image sets.

<a href="https://www.no-margin-for-errors.com/projects/prettyPhoto-jquery-lightbox-clone/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d1826d0-d95d-4794-87d0-ee0bd6b5379f/prettyphoto.jpg" alt="" /></a>

jQuery Expose
This is a little different than a modal window script. This one exposes selected HTML elements. When you click a specific element, the rest of the page fades out. This is an excellent alternative to the modal window: it still fades out the page to bring focus to an element.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79264af7-d6fa-4d32-8ac4-428f8531d902/expose.jpg" alt="" />

## Showcase of Modal Windows

Grooveshark
Grooveshark is a well-constructed and well-styled application, and the modal windows are no exception. A modal window, with the page faded out, is used for the log-in and sign-up functions.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17afba4d-99c6-454c-82aa-78f5948c61a5/grooveshark.jpg" alt="" />

<a href="https://digg.com/">Digg</a>
Digg is another user-generated website with log-in and sign-up functions in a floating window. The log-in link is in the header of the website. Notice that a semi-transparent border is used instead of a fade and drop-shadow. The border provides more visual separation.

<a href="https://digg.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca95c607-a69e-4105-b792-a6ba32fb88dc/digg.jpg" alt="" /></a>

<a href="https://www.apple.com/trailers/universal/fastandfurious/">Apple Movie Trailers</a>
Apple uses modal windows in many places. Here you can see a window used for viewing movie trailers. The window is built just right so that large video files don't impact the performance of the window.

<a href="https://www.apple.com/trailers/universal/fastandfurious/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4009295-cac2-48c9-81cc-af8feb29f955/appletrailers.jpg" alt="" /></a>

Apple iMac: Design Gallery
Another example of modal windows on Apple's website. These have a clean, simple style with a strong drop-shadow for visual separation.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42140756-a64e-4a96-a044-0f787c705847/applemac.jpg" alt="" />

<a href="https://www.taoeffect.com/espionage/">Espionage</a>
Another good example of an image lightbox. In this one, the image extends to the edge of the window, and the exit button is overlaid directly on the image. No border is necessary here because of the strong color contrast.

<a href="https://www.taoeffect.com/espionage/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2adce4a-45e2-4063-ab78-dc21f90ad1a7/espionage.jpg" alt="" /></a>

<a href="https://marketcircle.com/daylite/index.html#">Daylite 3</a>
A good example of a window with the background faded out. Multiple pages of content are integrated here in a single modal window.

<a href="https://marketcircle.com/daylite/index.html#"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06d13052-9203-44c7-991d-c4dcf5dc2aa1/daylite.jpg" alt="" /></a>

<a href="https://www.behance.net/Gallery/Positive-Hype/55599">Behance</a>
Another contact form, this one with the familiar "Send to a friend" element, which is usually put in a modal window. Because the website has a mostly dark background, a light semi-transparent border is used for separation.

<a href="https://www.behance.net/Gallery/Positive-Hype/55599"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4f03fa6-ca0a-4773-8591-07697cff52a3/behance.jpg" alt="" /></a>

<a href="https://www.facebook.com/">Facebook</a>
Facebook's very recognizable modal window. This one contains information linked to a help element in the sign-up form. Again, a strong semi-transparent border.

<a href="https://www.facebook.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b999b668-79b3-49a9-ab93-89d645f8d155/facebook.jpg" alt="" /></a>

<a href="https://www.kissmetrics.com/">KISSmetrics</a>
Here is an excellent log-in form in a modal window. The form is well styled and contains help elements to improve usability: just because the log-in function is in a modal window doesn't mean you can neglect usability.

<a href="https://www.kissmetrics.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/871acd53-1551-43e6-8f23-073fa76e621c/kissmetrics.jpg" alt="" /></a>

Nasi Briyani Lounge
Another log-in form, this one a little different. Instead of a full modal window, this is just a simple pop-up window with a small form.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf85bee1-3252-4fcf-8c86-7f0d4ccec917/nasi.jpg" alt="" />

<a href="https://www.pixelightcreative.com/">Pixelight Creative</a>
A lightbox on a freelancer's portfolio website. When you click one of the portfolio items, a larger view opens in a lightbox.

<a href="https://www.pixelightcreative.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec1bbb29-9047-4ddf-88c6-1761ebdb218f/pixelight.jpg" alt="" /></a>

<a href="https://supermegaultragroovy.com/products/Capo/">Capo</a>
Another well-styled window, this one a video featuring a tour of the software, which is a common practice. This one also contains a simple border with a slight drop-shadow.

<a href="https://supermegaultragroovy.com/products/Capo/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35051d2b-f4e9-468a-b63f-f2bc2be2ac04/capo.jpg" alt="" /></a>

Accept-Ideas
This floating window is attached to the search box. When you type a query, the results show up in the modal window itself. The window has basic functionality, including an exit button and border.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d291686-6698-4749-a3c4-5404f81972dc/acceptideas.jpg" alt="" />

<a href="https://typedeskref.com/">The Typographic Desk Reference</a>
A very simple modal window with a strong shadow that adds a lot of depth.

<a href="https://typedeskref.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8a9009d-c161-44c9-bc8d-f97a192a564e/tdr.jpg" alt="" /></a>

<a href="https://www.evernote.com/">Evernote Web Application</a>
This screenshot shows an alert that you get when you open Evernote's Web application. Notice how the page fades out strongly, which puts all of the focus on the window's content.

<a href="https://www.evernote.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c24d679c-afe8-450a-9a61-19ebaff47bfc/evernote.jpg" alt="" /></a>

Iceberg
Another sign-up form in a floating window. This one doesn't have a fade or shadow but does have a border for separation.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d354e92-2b1d-470c-b258-2d4287ebe8d5/iceberg.jpg" alt="" />

<a href="https://corp.viewzi.com/">Viewzi Corporate</a>
A beautifully styled modal window. Notice the large clean exit button in the upper corner, the generous padding in the window and the semi-transparent background.

<a href="https://corp.viewzi.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92b4c907-264a-4f5b-a101-682ca4b4b773/viewzi.jpg" alt="" /></a>

<a href="https://www.mailchimp.com/">Mail Chimp</a>
This lightbox has a semi-transparent border, and the page fades out.

<a href="https://www.mailchimp.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82437873-13df-4a54-80a4-b7f260e04103/mailchimp.jpg" alt="" /></a>

The Resumator
Notice in this one how strongly the background of the image contrasts with the page background. A label is used here but not attached to the window, creating a very nice look.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6705d706-81f9-4e8a-8088-22615e6c1fea/resumator.jpg" alt="" />

<a href="https://www.checkoutapp.com/">Checkout App</a>
A well-styled image modal window. This window has a slight drop-shadow to add depth and a solid border to provide more separation and frame the image.

<a href="https://www.checkoutapp.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6e34d9c-321e-46a4-a33a-d86dc4d66b15/checkout.jpg" alt="" /></a>

<a href="https://www.pixelmator.com/">Pixelmator</a>
Another example of a nice download alert. This alert pops up immediately once the download starts. Notice the excellent styling, such as the slight opacity of the window.

<a href="https://www.pixelmator.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/415590d1-220a-4e7d-9a06-41dbd52d1ce0/pixelmator.jpg" alt="" /></a>

<a href="https://www.getballpark.com/">Ballpark</a>
Here is a modal window for a video, common for corporate and software websites such as this one. You most often see QuickTime and SWF videos in modals, but this one embeds a video from Vimeo. A great fade in and out transition, too.

<a href="https://www.getballpark.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4c0f799-9d9f-40e2-aeb7-a1b82ad05e37/ballpark.jpg" alt="" /></a>

<a href="https://www.backpackit.com/?source=37signals+home#/">Backpack</a>
Another window with a video. Notice again how the page fades to a lighter rather than darker color.

<a href="https://www.backpackit.com/?source=37signals+home#/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aafa7895-4651-4629-b6c7-69d21f797c0a/backpack.jpg" alt="" /></a>

<a href="https://blog.guifx.com/category/downloads/">Guifx</a>
An image lightbox for a portfolio, always a great idea if you want to include larger images to show details of your work.

<a href="https://blog.guifx.com/category/downloads/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ad8bd78-7d37-4d3d-b14d-0031466cdd69/guifx.jpg" alt="" /></a>

## Further Resources

You may be interested in the following related posts:

*   [30 Scripts For Galleries, Slideshows and Lightboxes](https://www.smashingmagazine.com/2007/05/18/30-best-solutions-for-image-galleries-slideshows-lightboxes/)
*   [How To Use Help Elements To Improve Your Designs](https://www.smashingmagazine.com/2009/04/23/help-elements-design-showcase/)
*   [8 Layout Solutions To Improve Your Designs](https://www.smashingmagazine.com/2009/05/19/8-layout-solutions-to-improve-your-designs/)
*   [Designing Drop-Down-Menus: Examples and Best Practices](https://www.smashingmagazine.com/2009/03/24/designing-drop-down-menus-examples-and-best-practices/)
*   [Breadcrumbs in Web Design](https://www.smashingmagazine.com/2009/03/17/breadcrumbs-in-web-design-examples-and-best-practices-2/)

{{< signature "al" >}}


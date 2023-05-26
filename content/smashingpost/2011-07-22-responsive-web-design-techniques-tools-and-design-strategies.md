---
title: 'Responsive Web Design Techniques, Tools and Design Strategies'
slug: responsive-web-design-techniques-tools-and-design-strategies
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef9a215c-23ad-44d3-9dcb-8e4661f62cd0/image1.png
date: 2011-07-22T10:16:22.000Z
author: vitaly-friedman
summary: >-
  A round-up of resources for creating responsive website designs. Tutorials, techniques, articles, tools and more you need to create your own responsive designs.
description: >-
 A round-up of resources for creating responsive website designs. Tutorials, techniques, articles, tools and more you need to create your own responsive designs.
categories:
  - Mobile
  - Techniques
  - Responsive Design
  - Strategy
---

Back in January, we published an article on responsive design, “[Responsive Web Design: What It Is and How to Use It](https://www.smashingmagazine.com/2011/01/12/guidelines-for-responsive-web-design/).”

Responsive design continues to get a lot of attention, but considering how different it is from the “traditional” way of designing websites, it can be a bit overwhelming for those designers who have yet to try it.

To that end, we’ve compiled this round-up of resources for creating responsive website designs. Included are tutorials, techniques, articles, tools and more, all geared toward giving you the specific knowledge you need to create your own responsive designs.

{{% feature-panel %}}

## Responsive Design Techniques

<a href="https://elliotjaystocks.com/blog/css-transitions-media-queries/">CSS Transitions and Media Queries</a>  
Elliot Jay Stocks provides insight into the combination of CSS media queries and CSS transitions. The basic premise is this: you use media queries to design responsive websites that adapt in layout according to browser width, and you constantly resize your browser to see how the website performs, but every time a query kicks in, there’s a harsh jump between the first style and the second. Why not use some simple CSS transitions to smooth the jump by animating the resize? A nice case study.

<figure><a href="https://elliotjaystocks.com/blog/css-transitions-media-queries/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/820c08d9-4086-451d-b3de-e97c65481d66/responsive-design-116.jpg" alt="CSS Transitions and Media Queries" width="500" height="300" /></a></figure>

<a href="https://css-tricks.com/responsive-data-table-roundup/">Responsive Data Tables</a>  
Chris Coyier and Scott Jehl are experimenting with responsive design techniques for displaying data tables. By default, data tables can be quite wide, and necessarily so. You could zoom out and see the whole table, but then the text size would be too small to read. You could zoom in to make it readable, but then you’d have to scroll both vertically and horizontally (sad face) to browse the table. One solution is to reformat the table for better readability. Another is to display a pie graph from the data. Yet another is to adapt the table into a mini-graphic for narrow screens (rather than interfering much with the content when the full table is displayed).

<figure><a href="https://css-tricks.com/responsive-data-table-roundup/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d0724c8-9896-4788-8f65-71dbaca2eca0/responsive-design-105.jpg" alt="Responsive Data Tables" width="500" height="300" /></a></figure>

<a href="https://css-tricks.com/convert-menu-to-dropdown/">Responsive Navigation Menus: Convert a Menu to a Dropdown for Small Screens</a>  
Chris Coyier describes another technique for converting a regular row of links into a dropdown menu when the browser window is narrow. When the user is on a small screen and clicks the dropdown, they’ll get an interface to select an option that is nice and big and easy to choose. Obviously much better than displaying a tiny link.

<figure><a href="https://css-tricks.com/convert-menu-to-dropdown/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c409564-f80c-4c26-8cd3-a5dfa9ed1279/responsive-design-131.jpg" alt="Convert a Menu to a Dropdown for Small Screens" width="500" height="300" /></a></figure>

<a href="https://css-tricks.com/css-media-queries/">CSS Media Queries and Using Available Space</a>  
A tutorial from CSS-Tricks that discusses how to make subtle changes with media queries and how to use media queries in a single style sheet. For instance, if you have a fluid-width design in which the sidebar is 35% of the width of the page, depending on the width of the browser window, you could say, “If the browser is really narrow, do this. If it’s wider, do this. If it’s really wide, do this.” In the article, you’ll learn how to modify a list of links according to the browser’s viewport.

<figure><a href="https://css-tricks.com/css-media-queries/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e637d71d-dc25-499c-b8e6-2cbc9e686522/mediaq.jpg" width="500" height="300" /></a></figure>

### Responsive Images, Responsive Videos

<a href="https://unstoppablerobotninja.com/entry/fluid-images/">Fluid Images</a>  
Fluid images are a central aspect of a responsive design. This article by Ethan Marcotte gives a thorough overview on creating them using the classic <code>img { max-width: 100%; }</code> code snippet, as well as details to get you started.

<figure><a href="https://unstoppablerobotninja.com/entry/fluid-images/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00d8dbbe-90fa-45ed-9d5c-976a9308b541/fluidimages.jpg" width="500" /></a></figure>

<a href="https://filamentgroup.com/lab/responsive_images_experimenting_with_context_aware_image_sizing/">Responsive Image: Experimenting With Context-Aware Image Sizing</a>  
An alternative approach to fluid images by Filament Group. This technique allows designers to create responsive layouts that serve different image sizes at different resolutions. Effectively, it allows designers to create mobile-optimized images for smaller screens, and then serve higher-resolution versions to larger screens. Filament Group has developed this technique that uses .htaccess files and JavaScript to serve up different sized images based on the screen width. An alternative solution is to use tools like <a href="https://tinysrc.net/">TinySrc</a> which allows you to merely prefix all large images in your source code with a TinySrc URL, and the tool does the rest.

<figure><a href="https://filamentgroup.com/lab/responsive_images_experimenting_with_context_aware_image_sizing/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c1957a5-51c3-4076-94de-abe8fc717e0e/filament1.jpg" width="500" height="300" /></a></figure>

<a href="https://www.craig-russell.co.uk/responsive-images-and-context-aware-image-sizing/">Responsive Images and Context-Aware Image Sizing</a>  
Craig Russell has developed a technique that uses a server-side script (in PHP) to serve up images of several different resolutions. The idea is that within the PHP script, a nested array is used that lists image files and their relative percentage scales. In HTML, the image’s <code>src</code> attribute would be set to get the requested image’s id, but with no scale specified. A JavaScript calculates the percentage width of the image relative to the maximum width of the container, and this figure is then appended to the end of the <code>src</code> attribute as the scale parameter. The comments in the article contain some nice ideas and suggestions on how the technique could be improved.

<figure><a href="https://www.craig-russell.co.uk/responsive-images-and-context-aware-image-sizing/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef32f71b-3297-40a7-aef8-23e9553a1d75/responsive-design-101.jpg" alt="» Responsive Images and Context Aware Image Sizing Craig Russell Web Developer" width="500" height="300" /></a></figure>

<a href="https://csswizardry.com/2011/07/responsive-images-right-now/">Responsive Images Right Now</a>  
Harry Roberts’ idea is to use the <code>img</code> element for the smaller of the two images, the image that you want mobile users to download. You would also have a containing <code>div</code> to which you apply the large version of the image as a background through CSS. You then hide the <code>img</code> from desktop users, and show them the large CSS background, and hide the background image from mobile users and just serve them the smaller inline image.

<figure><a href="https://csswizardry.com/2011/07/responsive-images-right-now/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/393f2730-0620-4513-96bf-357cf74a99cc/responsive-design-110.jpg" alt="Responsive images right now — CSS Wizardry—CSS, Web Standards, Typography, and Grids by Harry Roberts" width="500" height="300" /></a></figure>

<a href="https://nicolasgallagher.com/responsive-images-using-css3/">Responsive Images Using CSS3</a>  Nicolas Gallagher’s method relies on the use of <code>@media</code> queries, CSS3-generated content and the CSS3 extension to the <code>attr()</code> function. By combining the content property with the CSS3 extension to <code>attr()</code>, you are able to specify that an attribute’s value should be interpreted as the URL part of a <code>url()</code> expression. In this case, it means you will be able to replace an image’s content with the image found at the destination URL, stored in a custom HTML <code>data-\*</code> attribute.

<figure><a href="https://nicolasgallagher.com/responsive-images-using-css3/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/204115db-ad2a-40d5-918d-15b874f230a7/responsive-102.gif" alt="Responsive images using CSS3" width="500" height="300" /></a></figure>

<a href="https://blog.keithclark.co.uk/responsive-images-using-cookies/">Responsive Images Using Cookies</a>  
Keith Clark suggests using cookies to serve smaller images to mobile users. Whenever a browser requests a file from a server, it automatically forwards any cookie data along with the request. If we use JavaScript to populate a cookie with the current screen’s dimensions, all subsequent requests made by the browser will pass this data to the server. In other words, the server would know the screen size of the device that is asking for the file.

<figure><a href="https://blog.keithclark.co.uk/responsive-images-using-cookies/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99626b22-b9e4-4fbf-8182-54575965e1e1/responsive-103.gif" alt="Responsive images using CSS3" width="500" height="300" /></a></figure>

<a href="https://www.johnfaulds.com.au/journal/responsive-images-with-expressionengine/">Responsive Images With ExpressionEngine</a>  
John Faulds presents a technique for responsive images that is different from the techniques presented above. It involves querying the device’s user agent string to determine whether it is mobile, and then setting a global variable that can then be used in templates to modify the size of the image output. Basically, only one image gets sent to the browser, but that image is different depending on whether you’re viewing the page on a mobile or desktop device.

<figure><a href="https://www.johnfaulds.com.au/journal/responsive-images-with-expressionengine/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9497a374-0e6b-47d6-bbb6-85243f4c01c2/responsive-design-118.jpg" alt="Responsive images with ExpressionEngine — John Faulds" width="500" height="300" /></a></figure>

<a href="https://webdesignerwall.com/tutorials/css-elastic-videos">CSS: Elastic Videos</a>  
Nick La applies the <code>max-width: 100%;</code> snippet to videos and presents techniques that make HTML5 videos and object- and iFrame-embedded videos responsive. For the latter, the trick is very simple. Just wrap the embedding code in a <code>div</code> container, and specify a 50% to 60% <code>padding-bottom</code>. Then, specify the child elements (iFrame, object embed) and a 100% width and 100% height, with absolute positioning. This will force the embedded elements to expand full width automatically. Initially discovered by <a href="https://www.tjkdesign.com/articles/how-to-resize-videos-on-the-fly.asp">Thierry Koblentz</a>.

<figure><a href="https://webdesignerwall.com/tutorials/css-elastic-videos"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e8ba9e9-7e7f-4e00-b470-a07646058cfa/responsive-design-107.jpg" alt="CSS: Elastic Videos" width="500" height="300" /></a></figure>

<a href="https://css-tricks.com/resizeable-images-at-full-resolution/">Resizeable Images (At Full Resolution!)</a>  
A quick tutorial from CSS-Tricks on resizing images while maintaining resolution.

<figure><a href="https://css-tricks.com/resizeable-images-at-full-resolution/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8813d983-70ba-40cb-ada4-df119d9bd2fb/resizeableimages.jpg" width="500" /></a></figure>

### Responsive Email Newsletters

<a href="https://www.campaignmonitor.com/blog/post/3163/optimizing-your-emails-for-mobile-devices-with-media/">Optimizing Your Email for Mobile Devices With the Media Query</a>  
Wide emails often require horizontal scrolling, especially when there’s a large image. This case study by Campaign Monitor explains how emails can be optimized for mobile devices using media queries and offers a couple of useful techniques and snippets to be used right away.

<figure><a href="https://www.campaignmonitor.com/blog/post/3163/optimizing-your-emails-for-mobile-devices-with-media/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8fd19cf-0ac1-480b-b90b-622787773689/responsive-104.gif" alt="Optimizing your email for mobile devices with the @media query - Blog - Campaign Monitor" width="500" height="300" /></a></figure>

<a href="https://wildbit.com/blog/2011/06/30/design-for-the-largest-mobile-audience-email-clients/">Responsive Design for Email, the Largest Mobile Audience</a>  
Another interesting case study that shows how the development team behind Beanstalk applied screen-size-specific media queries to target styles, and what design decisions were made to make the mobile email experience better.

<figure><a href="https://wildbit.com/blog/2011/06/30/design-for-the-largest-mobile-audience-email-clients/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ad1f454-34d5-48a8-a34f-dcec748d59e0/responsive-design-133.jpg" alt="Wildbit » Responsive design for email – the largest mobile audience - Thoughts on building web apps, businesses, and virtual teams" width="500" height="300" /></a></figure>

<a href="https://www.emailonacid.com/blog/details/C6/media_queries_in_html_emails">Media Queries in HTML Emails</a>  
This article covers using media queries to target specific mobile email clients.

<figure><a href="https://www.emailonacid.com/blog/details/C6/media_queries_in_html_emails"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac451959-1742-4f5c-874b-91ab087dcec7/emailmediaqueries.jpg" width="500" /></a></figure>

<a href="https://www.campaignmonitor.com/css/">Guide to CSS Support in Email</a>  
Designing an HTML email that renders consistently across major email clients can be time-consuming. Support for even simple CSS varies considerably between clients, and even different versions of the same client. Campaign Monitor has put together a guide to save you the time and frustration of figuring it out for yourself. With 24 different email clients tested, it covers all of the popular applications across desktop, Web and mobile email.

<figure><a href="https://www.campaignmonitor.com/css/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a94574e6-8fd4-481a-b919-0814f121ebd7/responsive-design-137.jpg" alt="Guide to CSS support in email - Articles &amp; Tips - Campaign Monitor" width="500" height="300" /></a></figure>

{{% ad-panel-leaderboard %}}

## Responsive Design Tools

You can build a responsive design from scratch, or you can use some of the tools listed below to speed up and smooth out the process.

<a href="https://blog.fogcreek.com/webputty-css-editing-goes-boink/">WebPutty: Scientific Progress CSS Editing</a>  
This tool is a Web-based CSS editor with auto-save feature and a real-time preview of your website. WebPutty also has CSS selector highlighting and SCSS support (for Sass and LESS), as well as Compass support. To use the tool, just embed a link tag at the end of your website’s <code>head</code> tag.

<figure><a href="https://blog.fogcreek.com/webputty-css-editing-goes-boink/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8f00d29-1a2a-4add-ac9c-db687acfd5ee/webputty.gif" alt="WebPutty: scientific progress CSS editing goes “boink” - Fog Creek Blog" width="500" height="300" /></a></figure>

<a href="https://www.johanbrook.com/writings/debugging-css-media-queries/">Debugging CSS Media Queries</a>  
In responsive Web design, we’re working with different states, widths and viewport sizes. Johan Brook shares a quick tip for indicating (with pure CSS) which media query has kicked in. The article also provides a mixin for developers using Sass. A demo is available as well.

<figure><a href="https://www.johanbrook.com/writings/debugging-css-media-queries/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1ece629-6034-4499-b623-80c0ca4e9850/responsive-105.gif" alt="Debugging CSS Media Queries · Johan Brook" width="500" height="300" /></a></figure>

<a href="https://mattkersley.com/responsive/">Responsive Design Testing</a>  
This tool is for everyone who needs a quick and easy way to test their website design in multiple screen widths. Change the defaultURL variable at the top of the responsive.js file to your own site and navigate your website from within the frames.

<figure><a href="https://mattkersley.com/responsive/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55272658-d008-4c6d-b427-57fed77cdc80/image2.png" width="500" /></a></figure>

<a href="https://resizemybrowser.com/">Resize My Browser</a>  
If you need your browser to display content in a certain window size this is what you have been looking for. Just click on the size you need and check out what your size looks like. Does not work in Chrome and Opera due to issues with the “ResizeTo” event.

<figure><a href="https://resizemybrowser.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d76fba10-47d2-4307-827f-b8e607f2d1ba/resize.gif" width="500" height="300" /></a></figure>

<a href="https://seesparkbox.com/foundry/media_query_bookmarklet">Media Query Bookmarklet</a>  
A handy tool that shows you exactly what size the viewport has and which media query just fired. Drag it to your bookmarks bar and have it ready when needed.

<figure><a href="https://seesparkbox.com/foundry/media_query_bookmarklet"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74a79671-37ca-48dc-916b-62d0d885c340/responsive-109.jpg" width="500" height="300" /></a></figure>

<a href="https://responsivepx.com/">Responsivepx</a>  
Use the information this little gadget provides in your media queries to create responsive designs.

<figure><a href="https://responsivepx.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef9a215c-23ad-44d3-9dcb-8e4661f62cd0/image1.png" width="500" /></a></figure>

<a href="https://protofluid.com/">ProtoFluid</a>  
A tool for rapid prototyping of responsive design. You can prototype CSS on a variety of popular device sizes, orientations and browsers, be they phones (BlackBerry Torch, Google Nexus One, iPhone, Motorola Droid), tablets (BlackBerry Playbook, iPad, Samsung Galaxy Tab, Dell Streak), monitors or televisions (720p, 1080p). You can preview designs right in the browser and use your development tools like Firebug. You might want to check an alternative tool <a href="https://quirktools.com/screenfly/">ScreenFly</a> as well.

<figure><a href="https://protofluid.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae92724f-cd8e-4917-80ca-d958c65acee8/protofluid2.jpg" width="500" /></a></figure>

<a href="https://csswizardry.com/2011/06/fluid-grid-calculator/">Fluid Grid Calculator</a>  
Harry Roberts has developed a calculator and generator of fluid grids for your responsive designs. Just provide the number of columns, the width of one column and the width of the gutters, and the tool will generate a fluid grid system in CSS for you. Handy!

<figure><a href="https://csswizardry.com/2011/06/fluid-grid-calculator/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef4c0cd3-cede-4f21-babc-3221a6ef3dcd/responsive-design-102.jpg" alt="Fluid Grids—a fluid grid calculator by Harry Roberts" width="500" height="300" /></a></figure>

<a href="/2011/06/07/free-html5-css3-wordpress-3-1-theme-with-responsive-layout-yoko/">Free HTML5/CSS3 WordPress 3.1+ Theme With Responsive Layout: Yoko</a>  
Yoko is a modern and flexible WordPress theme. With the responsive layout based on **CSS3 media queries**, the theme adjusts to different screen sizes. The design is optimized for big desktop screens, tablets and small smartphone screens. To make your blog more individual, you can use the new post formats (like gallery, aside or quote), choose your own logo and header image, customize the background and link color.

<figure><a title="Visit the demo" href="/2011/06/07/free-html5-css3-wordpress-3-1-theme-with-responsive-layout-yoko/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f8fc01c-cbee-412c-a79c-d7304133edb0/release.png" width="500" height="400" /></a></figure>

<a href="https://wordpress.org/extend/themes/scherzo">Scherzo, a Responsive WordPress Theme</a>  
This WordPress theme is a fine example of responsive design, displaying nicely on almost all devices and screens.

## Responsive Design Templates

<a href="https://stuffandnonsense.co.uk/projects/320andup/">320 and Up</a>  
320 and Up works on the “tiny screen first” principle, whereby designs are created for mobile screens first, and then expanded for tablets, desktops, and large screens. It works well as an extension to HTML5 Boilerplate and as a standalone kit.

<figure><a href="https://stuffandnonsense.co.uk/projects/320andup/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86cb4844-21b8-4be1-bcf4-e1045ca838e0/320andup.jpg" width="500" /></a></figure>

<a href="https://www.stuffandnonsense.co.uk/blog/about/hardboiled_css3_media_queries/">Media Queries for Standard Devices</a>  
Here is a useful template for media queries for standard devices: empty placeholders for targeting devices and attributes that you might be interested in when making responsive designs.

<figure><a href="https://www.stuffandnonsense.co.uk/blog/about/hardboiled_css3_media_queries/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/252323c8-6f91-4663-a304-19c42220de32/responsive-design-120.jpg" alt="Media Queries for Standard Devices" width="500" height="300" /></a></figure>

<a href="https://html5boilerplate.com/mobile/">Mobile Boilerplate</a>  
Here is a customizable template for creating rich, high-performance mobile Web apps. You’ll get cross-browser consistency among A-grade smartphones, and fallback support for legacy BlackBerry, Symbian and IE Mobile. You’ll also get offline caching for free, fast button clicks, a media query polyfill and many common mobile Webkit optimizations.

<figure><a href="https://html5boilerplate.com/mobile/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f15fe5c-28c6-4288-9bf2-72ea1a69adcf/boiler.gif" alt="New-css-112 in Powerful New CSS Techniques and Tools" width="500" height="300" /></a></figure>

<a href="https://www.getskeleton.com/">Skeleton: Beautiful Boilerplate for Responsive, Mobile-Friendly Development</a>  
Skeleton is a small collection of CSS and JavaScript files that can help you rapidly develop websites that look beautiful at any size, be it a 17-inch laptop or an iPhone. Skeleton is a grid that is responsive right down to mobile. It is well organized and well structured and provides most basic styles as a foundation.

<figure><a href="https://www.getskeleton.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78a394e3-8fd1-489b-904c-cc29df2eed36/responsive-design-128.jpg" alt="Skeleton: Beautiful Boilerplate for Responsive, Mobile-Friendly Development" width="500" height="300" /></a></figure>

## Responsive Design Frameworks

<a href="https://github.com/inuitcss">inuit.css</a>  
This CSS framework is built to provide a solid foundation for designs on smaller screens (such as tablets) and tiny screens (such as phones) straight out of the box with minimal effort. It also has a custom grid system builder for creating fluid grid systems.

<figure><a href="https://github.com/inuitcss"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3aa841db-c9df-48dc-a443-a33e545ebadc/responsive-1241.jpg" alt="inuit.css" width="500" height="300" /></a></figure>

<a href="https://kflorence.github.com/flurid/">Flurid</a>  
Flurid is a liquid grid layout with up to 16 columns.

<figure><a href="https://kflorence.github.com/flurid/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa9031c7-16a3-447f-bef5-d9bce7f22632/flurid.jpg" alt="Flurid in Responsive Web Design Techniques, Tools and Tutorials" width="500" /></a></figure>

<a href="https://fluidgrids.com/">FluidGrids</a>  
FluidGrids is a fluid grid framework that creates layouts based on 6, 7, 8, 9, 10, 12 or 16 columns.

<figure><a href="https://fluidgrids.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b95edde-fa5e-465b-8c4e-d7e8d40ff787/fluidgrids.jpg" width="500" /></a></figure>

<a href="https://lessframework.com/">Less Framework 4</a>  
A CSS grid system for creating adaptive layouts. It includes four basic layouts (including tablet, mobile and wide mobile), with three sets of typography presets.

<figure><a href="https://lessframework.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76008f2a-ce6b-44cd-be4a-77102fb333b9/lessframework4.jpg" width="500" /></a></figure>

<a href="https://fluid.newgoldleaf.com/">Fluid Grid System</a>  
This fluid grid framework includes a typographic grid and baseline grid.

<figure><a href="https://fluid.newgoldleaf.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1fc3ffb-c45d-421c-bbc7-dac593bed094/fluidgridsystem.jpg" /></a></figure>

<a href="https://www.tinyfluidgrid.com/">Tiny Fluid Grid</a>  
Tiny Fluid Grid helps you generate your own fluid grid with 12, 16 or 24 columns, minimum and maximum widths, and percentage-based gutters.

<figure><a href="https://www.tinyfluidgrid.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/041f13bf-4840-4f7e-97d6-d0f4e1568583/tinyfluidgrid.jpg" /></a></figure>

## Responsive Design Workflow and Strategies

<a href="https://www.lukew.com/ff/entry.asp?1353">The Responsive Designer’s Workflow</a>  
Luke Wroblewski’s conference notes on Ethan Marcotte’s presentation about applying responsive Web design principles and workflows to the redesign of a major newspaper website. Among other things, Ethan explains how he approaches the responsive design methodology, what the design process looks like and how prototyping is done in the context of responsive design.

<figure><a href="https://www.lukew.com/ff/entry.asp?1353"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e139d90-831a-4906-a30e-0335278b0428/responsive-design-104.jpg" alt="LukeW" width="500" height="300" /></a></figure>

<a href="https://www.goldilocksapproach.com/">The Goldilocks Approach to Responsive Web Design</a>  
The Goldilocks Approach stresses device-independent layouts that look perfect regardless of the device they’re viewed on.

<figure><a href="https://www.goldilocksapproach.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b3a9eb6-44fd-433c-b990-8e7d812266fe/goldilocks.gif" width="500" /></a></figure>

<a href="https://trentwalton.com/2011/07/14/content-choreography/">Content Choreography</a>  
Read up on how to properly plan your site to live up to todays standards. Begin to choreograph content proportional to size to serve the best possible experience at any width.

<figure><a href="https://trentwalton.com/2011/07/14/content-choreography/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22198853-8458-4ec3-9d0e-e2340da41bcb/trentwalton1.gif" width="500" height="350" /></a></figure>

<a href="https://www.slideshare.net/stephenhay/structured-content-first">Structured Content First</a>  
In this presentation, Stephen Hay discusses a couple of troubles you might run into when structuring your content and argues that properly structured content is portable to future platforms. Stephen suggests that we think about creating and designing structured content first that caters to the lowest common layout denominator, whether this be a small screen or a text browser. This content should be able to go anywhere.

<a href="https://artequalswork.com/posts/target-first.php">Design for a Target Experience First</a>  
Another interesting perspective on a responsive designer’s workflow; Nathan C. Ford focuses on experience of its users first and then derives user scenarios and media queries from it. “There are goals for sites that reach beyond simple readability, where a lack of features can actually diminish the experience. I am working on such a project now. Our approach has been to peruse the research and tailor an optimal experience for the most likely user scenarios. Working out from there, we judicially edit and hone for each media query.”

<figure><a href="https://artequalswork.com/posts/target-first.php"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8decac80-7ce3-4a99-b38d-17544912bb8c/responsive-115.jpg" width="500" height="300" /></a></figure>

<a href="https://www.lukew.com/ff/entry.asp?1304">Breaking Development</a>  
Luke Wroblewski took notes at the Breaking Development Conference while Stephen Hay talked about the realities of designing for different device experiences.

<figure><a href="https://www.lukew.com/ff/entry.asp?1304"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8d4a4a9-e479-47cb-94ae-dff7ac5f16e6/entry.png" width="500" /></a></figure>

<a href="https://www.slideshare.net/preciousforever/patterns-for-multiscreen-strategies">Patterns for Multiscreen Strategies</a>  
Have a look at this simple but effective slideshow to get an idea of which core factors play a role in multiscreen concepts.

<figure><a href="https://www.slideshare.net/preciousforever/patterns-for-multiscreen-strategies"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffcd8c4e-3d3c-4d30-80da-b73c661e20f0/patterns.jpg" width="500" height="300" /></a></figure>

<a href="https://warpspire.com/talks/responsive/">Responsive Web Design from the Future</a>  
According to Kyle Neath, responsive web design is about a lot more than the size of your screen. This talk is about about how GitHub handles links, the url bar, partial page updates, and explains why Kyle thinks the HTML5 history API is the most important thing to happen to front end development since Firebug. An inspiring presentation.

<figure><a href="https://warpspire.com/talks/responsive/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/168bb69e-d805-4ea5-a128-69ff43cf97a5/responsive-1131.jpg" width="500" height="300" /></a></figure>

<a href="https://www.slideshare.net/dmolsenwvu/developing-a-progressive-mobile-strategy">Developing a Progressive Mobile Strategy</a>  
In this presentation, Dave Olsen presents a progressive mobile strategy that consists of audience strategy, content strategy and platform strategy. Dave argues that to develop a sustainable and scalable mobile strategy, you need to answer the questions, “What value will the targeted audiences get from this content?” and “How do we develop solutions to handle both mobile and native now, as well as the devices of the future?” An interesting presentation.

<figure><a href="https://www.slideshare.net/dmolsenwvu/developing-a-progressive-mobile-strategy"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a86b9d3f-b950-4ac3-b626-69ad151431c6/responsive-design-112.jpg" alt="Developing a Progressive Mobile Strategy" width="500" height="300" /></a></figure>

<a href="/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/">How to Use CSS3 Media Queries to Create a Mobile Version of Your Website</a>  
In this Smashing Magazine article, Rachel Andrew explains how, with a few CSS rules, you can create an iPhone version of your website using CSS3 &mdash; one that will work now. You’ll see a very simple example and learn the process of adding a small device style sheet to a website to show how easily we can add mobile-specific style sheets to existing websites. You may want to consider reading Aaron Gustafson’s article “<a href="https://www.netmagazine.com/tutorials/adaptive-layouts-media-queries">Adaptive Layouts With Media Queries</a>” and Emily Lewis’ piece "<a href="https://msdn.microsoft.com/en-us/scriptjunkie/gg619395.aspx">Respond to Different Devices With CSS3 Media Queries</a>" as well.

<figure><a href="/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24d0497f-3b0c-4279-9494-3a857b898697/responsive-design-126.jpg" alt="How To Use CSS3 Media Queries To Create a Mobile Version of Your Website - Smashing Magazine" width="500" height="300" /></a></figure>

## Discussions And Points Of View On Responsive Design

While not tutorials per se, the articles here give you valuable insight into why you should use responsive design techniques (and when you maybe shouldn’t use them).

<a href="http://globalmoxie.com/blog/mobile-web-responsive-design.shtml"> Responsive Web Design or Separate Mobile Site? Eh, It Depends</a>  
An interesting article discussing the pros and cons of responsive designs vs. dedicated mobile websites.

<figure><a href="https://globalmoxie.com/blog/mobile-web-responsive-design.shtml"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57bea6f4-8f5b-4592-9396-cc4baf666840/ehitdepends.jpg" width="500" /></a></figure>

<a href="https://adactio.com/journal/1696/">A Responsive Mind</a>  
A discussion on Jeremy Keith’s blog about the necessary parts of a responsive design and how to effectively create different layouts based on different screen sizes. Examples are included.

<a href="https://adactio.com/journal/1700/">Responsive Enhancement</a>  
An excellent introduction to responsive design as a way of thinking rather than as a tool or technique. Jeremy Keith argues that responsive Web design can’t be tacked on to the end of an existing workflow. Instead of pixel perfection, we should be thinking of proportion perfection. An inspiring read.

<a href="https://bradfrostweb.com/blog/web/mobile-first-responsive-web-design/">Mobile-First Responsive Web Design</a>  
Mobile First Responsive Web Design is a combination of philosophies and strategies with the aim to achieve a wider application of best practices in the area.

## Further Resources

Here are some additional resources for creating responsive designs that don’t fit neatly into the categories above.

<a href="https://mediaqueri.es/">Media Queries</a>  
A growing collection of websites that use media queries.

<figure><a href="https://mediaqueri.es/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee7c8d3d-400a-490a-96a9-5e0110b832b0/mediaqueries.jpg" /></a></figure>

<a href="https://www.abookapart.com/products/responsive-web-design">Responsive Web Design</a>, by Ethan Marcotte  
This book, written by Ethan Marcotte and published by A Book Apart, is a fantastic resource for learning how to design responsive websites. It covers the basics of the responsive Web, flexible grid systems, flexible images and media queries, and it gives insight into how to create responsive designs.

<figure><a href="https://www.abookapart.com/products/responsive-web-design"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07343ef2-1aba-4c4e-a50a-03983c977edc/responsive-120.jpg" width="500" height="300" /></a></figure>

<a href="https://5by5.tv/bigwebshow/9">The Big Web Show Episode #9: Responsive Web Design</a>  
Jeffrey Zeldman and Dan Benjamin sit down with Ethan Marcotte for episode 9 of The Big Web Show to discuss responsive design, among other topics.

{{% ad-panel-leaderboard %}}

## Last Click

<a href="https://html5-demos.appspot.com/static/html5-whats-new/template/index.html#1">The Latest in HTML5</a>  
This slideshow covers some techniques and lesser-known HTML5 gems that could get implemented in browsers in the near future: among other things, server-side media queries with JavaScript and form-factor detection.

<figure><a href="https://html5-demos.appspot.com/static/html5-whats-new/template/index.html#1"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b62fbe0b-7a6b-43a2-8bf4-475d6ba7d14c/matchmedia.gif" alt="The Latest in HTML5" width="500" height="288" /></a></figure>

### Further Reading

*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Responsible Considerations For Responsive Web Design](https://www.smashingmagazine.com/2013/03/responsible-web-design/)
*   [Photoshop Etiquette For Responsive Web Design](https://www.smashingmagazine.com/2016/08/photoshop-etiquette-for-responsive-web-design/)

{{< signature "al, mrn" >}}

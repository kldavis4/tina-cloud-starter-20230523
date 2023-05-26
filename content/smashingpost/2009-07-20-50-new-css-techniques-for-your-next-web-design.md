---
title: 50 New CSS Techniques For Your Next Web Design
slug: 50-new-css-techniques-for-your-next-web-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aefa8a1a-04dd-490b-90a7-7db5557fdf79/04-duplicate-opt-small.png
date: 2009-07-20T07:43:22.000Z
author: cameron-chapman
description: >-
  CSS is almost certainly one of the best developments in web design since the first graphical web browsers were adopted on a wide scale. Where tables created clunky, slow-loading pages, CSS created much more streamlined and usable web pages. Plus, CSS has allowed designers to achieve a number of different styles that used to only be possible with images.
categories:
  - Coding
  - CSS
  - Techniques
  - Resources
---
One of the best parts of CSS is that it's so simple once you know the basics. Where tables used to make incredibly complex and sometimes impossible-to-decipher code, CSS keeps things clean and simple. Add a few comments to keep everything organized and it becomes an absolute dream to work with.

Below are 50 fresh CSS tricks, techniques and tutorials that will help you to improve the quality of your next web design. Be sure to check out our previous articles:

*   [Powerful CSS-Techniques For Effective Coding](https://www.smashingmagazine.com/2008/02/powerful-css-techniques-for-effective-coding/)
*   [50 New Useful CSS Techniques, Tutorials and Tools](https://www.smashingmagazine.com/2010/10/50-new-useful-css-techniques-tutorials-and-tools/)
*   [53 CSS-Techniques You Couldn't Live Without](https://www.smashingmagazine.com/2007/01/19/53-css-techniques-you-couldnt-live-without/)
*   [Responsive Web Design Techniques, Tools and Design Strategies](https://www.smashingmagazine.com/2011/07/responsive-web-design-techniques-tools-and-design-strategies/)

## 1\. Security and Performance

While CSS is often thought of as merely a styling language, there are ways you can use it to add security to your site. There are also ways you can optimize your CSS to improve page load times. Both are discussed below.

{{% feature-panel %}}

### Make your pages load faster by combining and compressing javascript and css files

<a href="https://rakaz.nl/item/make_your_pages_load_faster_by_combining_and_compressing_javascript_and_css_files">This tutorial</a> shows you how to create a PHP script to compress and combine multiple CSS and/or JavaScript files with gzip when they're called for by a browser. It speeds up the page load times while making it possible to still edit the individual CSS or JavaScript files without having to combine and re-compress everything each times.

Informal testing showed that a group of JavaScript files were reduced from 168Kb (and 1905 ms to transfer) to 37Kb (and 400 ms). There wasn't any data available for the effect it had on CSS files, but I'd guess it's probably pretty similar.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7605a77f-ea0a-4d2a-8f41-955609330ccb/makeyourpagesloadfaster.jpg)](https://rakaz.nl/item/make_your_pages_load_faster_by_combining_and_compressing_javascript_and_css_files)

### The Definitive Post on Gzipping Your CSS

This <a href="https://www.fiftyfoureleven.com/weblog/web-development/css/the-definitive-css-gzip-method">post</a> covers the best and most recent methods for using GZIP to compress your CSS. It currently covers two different methods, both equally effective. One involves adding a bit of PHP to your CSS file (and renaming the file with a PHP extension instead of CSS) while the other method involves using the same PHP code with some additions but in a separate file.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79f0b729-ad80-442b-b616-a33f0f6ed0f7/definitivecssgzipmethod.jpg)](https://www.fiftyfoureleven.com/weblog/web-development/css/the-definitive-css-gzip-method)

### Clickjane.css: A CSS User Style Sheet to Help Detect and Avoid Clickjacking Attacks

This <a href="https://maymay.net/blog/2008/12/29/clickjanecss-a-css-user-style-sheet-to-help-detect-and-avoid-clickjacking-attacks/">post</a> covers how to use clickjane.css to prevent clickjacking, a class of security vulnerabilities kind of like phishing scams and more formally referred to as <em>user interface redressing</em>. It's cross-browser compatible but, admittedly, probably only covers a small range of potential clickjacking vulnerabilities. It's still a good place to start, though.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7ada774-e297-40b0-aa35-36f9b8e4f662/clickjanecsshelpdetectandav.jpg)](https://maymay.net/blog/2008/12/29/clickjanecss-a-css-user-style-sheet-to-help-detect-and-avoid-clickjacking-attacks/)

### 5 Step Style Sheet Weight Loss Program

This post shows five different ways to trim the size of your style sheets. Techniques range from learning how to group selectors to using CSS shorthand. Each technique is thoroughly explained and includes related resources.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0306eb2-c4eb-4c0b-b6cd-3962cb4e6724/5stepcssweightlossprogram.jpg)

## 2\. Page Layout

This is what CSS was built for. The options are almost endless, especially as CSS3 becomes the new standard.</p>

### Aligning Inline Images with the Vertical-Align Property

The default vertical alignment for inline images in text sometimes looks not-so-great. This <a href="https://www.maxdesign.com.au/2008/10/05/vertical-align/">tutorial</a> shows you how to better align inline images with your site's type. It goes over the different types of vertical alignment and what they mean in relation to type.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a559ab7e-b20f-45ee-be65-da868d63f27d/aligningimageswithverticala.jpg)](https://www.maxdesign.com.au/2008/10/05/vertical-align/)

### CSS Centering

This <a href="https://www.maxdesign.com.au/presentation/center/">post</a> includes instructions for centering liquid layouts with CSS. It's very simple and straight-forward and works in virtually all browsers. Basically, it just uses left and right margins combined with some additional code to make it cross-browser compatible.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49c0cc91-0970-4b15-b545-5385e9a850e9/csscentering.jpg)](https://www.maxdesign.com.au/presentation/center/)

### Making Your Footer Stay Put with CSS

Keeping footers at the bottom of your pages can be a real hassle with CSS, depending on how the rest of your page is set up. This <a href="https://fortysevenmedia.com/blog/archives/making_your_footer_stay_put_with_css/">tutorial</a> shows exactly how to keep your footer where it should be&amp;mdash;below the rest of your content! It's a very thorough post, with complete, step-by-step instructions.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db399a7e-c92d-4333-938e-7dd6441c587e/makingyourfooterstayputwith.jpg)](https://fortysevenmedia.com/blog/archives/making_your_footer_stay_put_with_css/)

### Vertical Centering with CSS

This post covers five excellent ways to center your content vertically. It includes the good and bad for each method along with complete instructions for implementing them. The methods range from using divs that act like tables to using absolute positions.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a49a64cb-4a8b-4da5-9453-46f1a0db3b3f/verticalcenteringwithcss.jpg)

### Handy Tips for Creating a Print CSS Stylesheet

This <a href="https://line25.com/tutorials/handy-tips-for-creating-a-print-css-stylesheet">post</a> is filled with great tips for creating better print stylesheets. It includes instructions for everything from including link destinations after the link text to splitting comments onto a new page. Pick and choose from the techniques offered or copy the whole stylesheet.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b6c0355-8a45-494f-ac60-86c097f02693/handytipsforcreatingaprintc.jpg)](https://line25.com/tutorials/handy-tips-for-creating-a-print-css-stylesheet)

### Fluid Images

Fluid layouts are great. They generally look and function just fine until you start introducing fixed-width elements within them&amp;mdash;like images. This <a href="https://unstoppablerobotninja.com/entry/fluid-images/">post</a> shows how to make your images fluid, too. And it works for most embedded video. And while the basic technique includes just one CSS property, there is a workaround necessary to make it work on Windows machines.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c94f675-bde0-4509-8570-9191d238f029/fluidimages.jpg)](https://unstoppablerobotninja.com/entry/fluid-images/)

### Flexible Equal Height Columns

This <a href="https://www.socialgeek.be/blog/read/flexible-equal-height-columns">tutorial</a> shows how to create completely versatile equal height columns using valid and semantic markup. It's cross-browser compatible and works with both fixed, fluid, and even elastic designs. It's a very complete tutorial but not at all complicated.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/780989c4-0035-4bbe-b15e-4e50683b717d/flexibleequalheightcolumns.jpg)](https://www.socialgeek.be/blog/read/flexible-equal-height-columns)

### CSS Columns with Borders

This is a <a href="https://www.onderhond.com/blog/onderhond/css-columns-with-borders">technique</a> for creating equal-height columns with CSS that have borders. It uses a series of nested divs to achieve the effect instead of images. The end result is fantastic.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81b134f8-8fa0-4f1b-a107-783262801c51/csscolumnswithborders.jpg)](https://www.onderhond.com/blog/onderhond/css-columns-with-borders)

### Creating a Polaroid Photo Viewer with CSS3 and jQuery

The photo gallery created with this <a href="https://www.marcofolio.net/webdesign/creating_a_polaroid_photo_viewer_with_css3_and_jquery.html">technique</a> is absolutely awesome. The HTML and CSS aren't super-complicated, and everything is explained really well. While CSS3 isn't supported by every browser, this does appear to degrade gracefully, making it perfectly fine to use as long as you don't mind some visitors not getting the full effect.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36a493bc-0bf1-454f-832f-6bf3944d9f2d/polaroidphotoviewer.jpg)](https://www.marcofolio.net/webdesign/creating_a_polaroid_photo_viewer_with_css3_and_jquery.html)

### A Killer Collection of Global CSS Reset Styles

An incredibly complete <a href="https://perishablepress.com/press/2007/10/23/a-killer-collection-of-global-css-reset-styles/">collection</a> of global resets, this post covers pretty much every reset you could possibly need. Some are short and sweet, consisting of only a couple of properties, while others are very complete and reset everything you might consider resetting.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e832365f-3ea9-4407-a073-13f2188dab59/akillercollectionofglobalcs.jpg)](https://perishablepress.com/press/2007/10/23/a-killer-collection-of-global-css-reset-styles/)

### Making Module Layout Systems

This <a href="https://24ways.org/2008/making-modular-layout-systems">tutorial</a> gives complete instructions for creating modular layout systems using CSS. This makes it practical to use different grid-based divs as needed for individual content elements. The end result provides tons of flexibility for dealing with everything from images to text while keeping everything uniform and balanced.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b729f25-15bf-4f63-af6f-15963d2d98bb/makingmodularlayoutsystems.jpg)](https://24ways.org/2008/making-modular-layout-systems)

### Multiple Backgrounds (CSS3)

This tutorial shows how to implement multiple backgrounds using CSS3. It's currently only supported by Safari, but the tutorial includes tricks to make it work in non-supported browsers. Currently, it doesn't validate, but once the CSS3 standard is completed it's likely it will.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c7306df-38f2-4289-9691-ea468bdaceb3/multiplebackgroundscss3.jpg)

### CSS3 Multiple Columns

Here's a tutorial for creating multi-column layouts with CSS3. The CSS is pretty simple and straight-forward, much easier than most current solutions to multi-column layouts. Unfortunately, this only works with Firefox, Safari and Chrome at the moment.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62d00e80-7d36-4b4f-85a9-82654aa0cbf0/css3multiplecolumns.jpg)

### Smart Columns with CSS and jQuery

This tutorial shows how to create smart columns inside liquid layouts using a combination of CSS and jQuery. Basically, it fits as many columns into the base column size as possible and then distributes any leftover white space among the columns there. A very elegant solution if you want to allow for a variable number of columns without ending up with a bunch of leftover white space in your design.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/307dcb09-ddf7-421b-b6fb-590077633975/smartcolumnswithcssjquery.jpg)

### CSS Hack for Chrome, Safari and Internet Explorer

This <a href="https://www.giantisland.com/Resources/LitePacificHackforSafariAndIE7.aspx">tutorial</a> shows how to apply different style sheets based on the browser your visitors are using (at least in IE5-8, Google Chrome, and Safari 1-4). A very valuable technique if you want to use styles only supported in certain browsers without making your site look bad in unsupported browsers.</p>

## 3\. Menu and Navigation Customizations

Menu and navigation styles can really set your site apart if done well. Just remember, menus need to remain usable and functional no matter how they look.</p>

### Overlap That Menu!

Have you ever wanted to create menu items that overlap? <span class="removed_link" title="https://www.cssbake.com/cookbook/overlap-that-menu/">This relatively-simple tutorial</span> shows you how to do just that using unique classes for your menu items. It also tells how to reorder the navigation items using the z-index. It's a nice effect that isn't difficult to achieve.

<span class="removed_link" title="https://www.cssbake.com/cookbook/overlap-that-menu/">![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dcf8be9-af36-438a-8677-4d679c79ef43/overlapthatmenu.jpg)</span>

### Super Awesome Buttons with CSS3 and RGBA

With a little CSS3 magic, you can created a <a href="https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba">scalable set of sexy buttons</a> with nearly half the CSS it would have taken with hex colors. Give it a go in your next project and see how it can help add that extra polish you want without huge impact on your code.

[![ Super Awesome Buttons with CSS3 and RGBA](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5429bc73-7543-4e08-ab4b-6f4af53ba660/56.gif)](https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba)

### Custom Buttons 3.0

<a href="https://stopdesign.com/eg/buttons/3.0/code.html">This page</a> shows a variety of rounded-corner (1px radius) buttons that don't use images (other than for the optional background gradient). Just look at the source code for the page to see how it's done.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c621dd01-7a6d-408f-980f-e3a9ae8d0853/custombuttons30.jpg)](https://stopdesign.com/eg/buttons/3.0/code.html)

### Centered Tabs with CSS

<a href="https://24ways.org/2005/centered-tabs-with-css">This tutorial</a> provides an alternative to the sliding doors method of creating tabs in CSS that allows tabs to be centered instead of only right- or left-aligned. It's a multi-step tutorial but isn't complicated.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48774745-221c-4b7b-9be8-adab94e2471e/changinghtmlimagesonhover.jpg)](https://24ways.org/2005/centered-tabs-with-css)

### Styling the Button Element with CSS Sliding Doors

An updated tutorial on sliding doors buttons that now includes creating them with CSS image sprites. It's also been simplified to work with a single block of CSS in all the major browsers (including IE 6-8). The markup is simple and straight-forward and the end result is perfect.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b5443ac-f67e-4e9f-9783-650a519997e0/stylingbuttonelementsliding.jpg)

### Styling Buttons to Look Like Links

Sometimes you have to use a button (like with forms), but realize your design would look so much better with just a simple text link. This tutorial gives a complete overview of how to make your buttons look like text links using CSS.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04c31d5a-7a35-44a8-a6b9-51f93799cc3a/stylingbuttonsaslinks.jpg)

### Simple, Scalable CSS Based Breadcrumbs

Breadcrumbs can be a great addition to your site's navigation and can really improve your site's usability. This <a href="https://veerle.duoh.com/blog/comments/simple_scalable_css_based_breadcrumbs/">tutorial</a> shows you how to create breadcrumbs with CSS. The code used is simple (the HTML portion is just an unordered list) and there are only six CSS styles defined.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82d6c660-2c99-44b2-b79a-f75c7cec9d7c/simplescalablecssbreadcrumb.jpg)](https://veerle.duoh.com/blog/comments/simple_scalable_css_based_breadcrumbs/)

### Recreating the Button

This <a href="https://stopdesign.com/archive/2009/02/04/recreating-the-button.html">article</a> covers how to make a button that look very similar to regular HTML input buttons but can handle multiple types of interaction (like dropdowns or toggle functions). These buttons were originally developed at Google and are skinnable with just a few lines of CSS. The buttons created are entirely CSS-based, including the gradient background.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffff9761-a5f7-4078-b660-81db55262d0a/recreatingthebutton.jpg)](https://stopdesign.com/archive/2009/02/04/recreating-the-button.html)

### List of 10+ Usability-Conscious Link Styles

This page offers a good overview of different effects you can use for links, including color and underline, backgrounds, and animations. It's a good starting place if you're trying to figure out exactly how your links should look and act to make them more user-friendly.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea7671dd-1f14-4d55-b432-f4e3cdea4c5d/listof10usabilityconsciousl.jpg)

### Create Vimeo-Like Top Navigation

Here's a <a href="https://www.jankoatwarpspeed.com/post/2009/01/19/Create-Vimeo-like-top-navigation.aspx">tutorial</a> to create a drop-down top navigation bar similar to the one <a href="https://www.vimeo.com">Vimeo.com</a> uses. It's all done with images, CSS and HTML and isn't particularly difficult, though it is a bit complex. It's explained really well, with images illustrating the structure and very well-written CSS.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f16047ed-ab89-48a6-b879-326ced5d3728/createvimeoliketopnav.jpg)](https://www.jankoatwarpspeed.com/post/2009/01/19/Create-Vimeo-like-top-navigation.aspx)

### Beautifully Horizontal Centered Menus/Tabs/List

This <a href="https://matthewjamestaylor.com/blog/beautiful-css-centered-menus-no-hacks-full-cross-browser-support">tutorial</a> explains how to create cross-browser compatible, centered menus or other items in CSS with no hacks and no JavaScript It's compatible with liquid layouts, too. Not only does it give the code to achieve the effect, but it also fully explains exactly how and why it works.</p>

## 4\. Typography

Here's a tutorial for creating multi-column layouts with CSS3. The CSS is pretty simple and straight-forward, much easier than most current solutions to multi-column layouts. Unfortunately, this only works with Firefox, Safari and Chrome at the moment.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62d00e80-7d36-4b4f-85a9-82654aa0cbf0/css3multiplecolumns.jpg)

### Smart Columns with CSS and jQuery

This tutorial shows how to create smart columns inside liquid layouts using a combination of CSS and jQuery. Basically, it fits as many columns into the base column size as possible and then distributes any leftover white space among the columns there. A very elegant solution if you want to allow for a variable number of columns without ending up with a bunch of leftover white space in your design.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/307dcb09-ddf7-421b-b6fb-590077633975/smartcolumnswithcssjquery.jpg)

### CSS Hack for Chrome, Safari and Internet Explorer

This <a href="https://www.giantisland.com/Resources/LitePacificHackforSafariAndIE7.aspx">tutorial</a> shows how to apply different style sheets based on the browser your visitors are using (at least in IE5-8, Google Chrome, and Safari 1-4). A very valuable technique if you want to use styles only supported in certain browsers without making your site look bad in unsupported browsers.</p>

## 3\. Menu and Navigation Customizations

Menu and navigation styles can really set your site apart if done well. Just remember, menus need to remain usable and functional no matter how they look.</p>

### Overlap That Menu!

Have you ever wanted to create menu items that overlap? <span class="removed_link" title="https://www.cssbake.com/cookbook/overlap-that-menu/">This relatively-simple tutorial</span> shows you how to do just that using unique classes for your menu items. It also tells how to reorder the navigation items using the z-index. It's a nice effect that isn't difficult to achieve.

<span class="removed_link" title="https://www.cssbake.com/cookbook/overlap-that-menu/">![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dcf8be9-af36-438a-8677-4d679c79ef43/overlapthatmenu.jpg)</span>

### Super Awesome Buttons with CSS3 and RGBA

With a little CSS3 magic, you can created a <a href="https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba">scalable set of sexy buttons</a> with nearly half the CSS it would have taken with hex colors. Give it a go in your next project and see how it can help add that extra polish you want without huge impact on your code.

[![ Super Awesome Buttons with CSS3 and RGBA](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5429bc73-7543-4e08-ab4b-6f4af53ba660/56.gif)](https://www.zurb.com/article/266/super-awesome-buttons-with-css3-and-rgba)

### Custom Buttons 3.0

<a href="https://stopdesign.com/eg/buttons/3.0/code.html">This page</a> shows a variety of rounded-corner (1px radius) buttons that don't use images (other than for the optional background gradient). Just look at the source code for the page to see how it's done.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c621dd01-7a6d-408f-980f-e3a9ae8d0853/custombuttons30.jpg)](https://stopdesign.com/eg/buttons/3.0/code.html)

### Centered Tabs with CSS

<a href="https://24ways.org/2005/centered-tabs-with-css">This tutorial</a> provides an alternative to the sliding doors method of creating tabs in CSS that allows tabs to be centered instead of only right- or left-aligned. It's a multi-step tutorial but isn't complicated.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48774745-221c-4b7b-9be8-adab94e2471e/changinghtmlimagesonhover.jpg)](https://24ways.org/2005/centered-tabs-with-css)

### Styling the Button Element with CSS Sliding Doors

An updated tutorial on sliding doors buttons that now includes creating them with CSS image sprites. It's also been simplified to work with a single block of CSS in all the major browsers (including IE 6-8). The markup is simple and straight-forward and the end result is perfect.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b5443ac-f67e-4e9f-9783-650a519997e0/stylingbuttonelementsliding.jpg)

### Styling Buttons to Look Like Links

Sometimes you have to use a button (like with forms), but realize your design would look so much better with just a simple text link. This tutorial gives a complete overview of how to make your buttons look like text links using CSS.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04c31d5a-7a35-44a8-a6b9-51f93799cc3a/stylingbuttonsaslinks.jpg)

### Simple, Scalable CSS Based Breadcrumbs

Breadcrumbs can be a great addition to your site's navigation and can really improve your site's usability. This <a href="https://veerle.duoh.com/blog/comments/simple_scalable_css_based_breadcrumbs/">tutorial</a> shows you how to create breadcrumbs with CSS. The code used is simple (the HTML portion is just an unordered list) and there are only six CSS styles defined.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82d6c660-2c99-44b2-b79a-f75c7cec9d7c/simplescalablecssbreadcrumb.jpg)](https://veerle.duoh.com/blog/comments/simple_scalable_css_based_breadcrumbs/)

### Recreating the Button

This <a href="https://stopdesign.com/archive/2009/02/04/recreating-the-button.html">article</a> covers how to make a button that look very similar to regular HTML input buttons but can handle multiple types of interaction (like dropdowns or toggle functions). These buttons were originally developed at Google and are skinnable with just a few lines of CSS. The buttons created are entirely CSS-based, including the gradient background.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffff9761-a5f7-4078-b660-81db55262d0a/recreatingthebutton.jpg)](https://stopdesign.com/archive/2009/02/04/recreating-the-button.html)

### List of 10+ Usability-Conscious Link Styles

This page offers a good overview of different effects you can use for links, including color and underline, backgrounds, and animations. It's a good starting place if you're trying to figure out exactly how your links should look and act to make them more user-friendly.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea7671dd-1f14-4d55-b432-f4e3cdea4c5d/listof10usabilityconsciousl.jpg)

### Create Vimeo-Like Top Navigation

Here's a <a href="https://www.jankoatwarpspeed.com/post/2009/01/19/Create-Vimeo-like-top-navigation.aspx">tutorial</a> to create a drop-down top navigation bar similar to the one <a href="https://www.vimeo.com">Vimeo.com</a> uses. It's all done with images, CSS and HTML and isn't particularly difficult, though it is a bit complex. It's explained really well, with images illustrating the structure and very well-written CSS.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f16047ed-ab89-48a6-b879-326ced5d3728/createvimeoliketopnav.jpg)](https://www.jankoatwarpspeed.com/post/2009/01/19/Create-Vimeo-like-top-navigation.aspx)

### Beautifully Horizontal Centered Menus/Tabs/List

This <a href="https://matthewjamestaylor.com/blog/beautiful-css-centered-menus-no-hacks-full-cross-browser-support">tutorial</a> explains how to create cross-browser compatible, centered menus or other items in CSS with no hacks and no JavaScript It's compatible with liquid layouts, too. Not only does it give the code to achieve the effect, but it also fully explains exactly how and why it works.</p>

## 4\. Typography

Here are a few tutorials and tricks for creating advanced typographic styles using CSS. There's everything from line-wrap functions to faux anti-aliasing to adding gradients and shadows.</p>

### Wrapping Text Inside Pre Tags

<a href="https://www.longren.org/2006/09/27/wrapping-text-inside-pre-tags/">This tutorial</a> shows how to wrap text within pre html tags. It's useful for displaying code on your site, especially when lines of code are quite long and end up breaking your site's layout (especially in IE). It's a relatively simple and there are a few different options presented.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be3b41b9-eeb5-4bb4-9423-de9f36856d55/wrappingtextinpretags.jpg)](https://www.longren.org/2006/09/27/wrapping-text-inside-pre-tags/)

### Make Cool and Clever Text Effects with CSS Text-Shadow

Creating text effects without the use of images is a big advantage in terms of both file size and the time required for maintenance. This <a href="https://www.kremalicious.com/2008/04/make-cool-and-clever-text-effects-with-css-text-shadow/">tutorial</a> shows how to take advantage of the text-shadow property in CSS to style your text. While this effect doesn't work in IE, it does in most other browsers. And it looks incredibly cool if done well (I'm a big fan of the "milky text" example).

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9636c300-6d5e-4ab3-ba11-ee3c20a541ec/coolandclevertexteffectscss.jpg)](https://www.kremalicious.com/2008/04/make-cool-and-clever-text-effects-with-css-text-shadow/)

### Safari's Text-Shadowing Anti-Aliasing CSS Hack

This <a href="https://sam.brown.tc/entry/348/safaris-text-shadow-anti-aliasing-css-hack">tutorial</a> shows how to use the text-shadow CSS property to create an anti-aliasing effect on your text. It only works in browsers that support text-shadow (so not IE), but the look is pretty awesome. It can definitely make text more readable, just don't overdo it or you end up with text that's blurry.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6cc078b4-d18b-4c33-a223-1ee04dd24699/safaristextshadowantialiasi.jpg)](https://sam.brown.tc/entry/348/safaris-text-shadow-anti-aliasing-css-hack)

### Safari's Text-Shadowing Anti-Aliasing CSS Hack Revision

This is a revised version of the technique above to create a slightly different anti-aliasing effect, especially useful for light text on dark backgrounds. It uses an extremely transparent black background to force Safari to render the text more legibly.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52c0d6af-05e1-4c9b-baf0-971fbb49d96b/safaritextshadowantialiasin.jpg)

### Snazzy Pullquotes for Your Blog

If you have a blog or other site that's text-heavy, using pull quotes to highlight important bits can look really awesome while also making your content more scannable. This <a href="https://www.pearsonified.com/2006/09/snazzy_pullquotes_for_your_blo.php">tutorial</a> shows how to format those pull quotes with CSS. It shows how to create both left and right aligned pull quotes while also preserving your regular blockquote style.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2a09041-d583-4042-b478-f081856f9587/snazzypullquotesforyourblog.jpg)](https://www.pearsonified.com/2006/09/snazzy_pullquotes_for_your_blo.php)

### Codename Rainbows

Here's a technique for creating two-color gradients for text using a combination of JavaScript and CSS. It also works to apply shadows and highlights to text. The possibilities for the use of this technique are pretty endless. Of course, this is also one of those things where a little bit goes a long way (ie, limit gradients to your headers, titles, and other text you want to stand out&amp;mdash;not your site's body copy).

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea15b3b2-e348-47cd-9ea9-01e8bb8c4693/codenamerainbows.jpg)

### Build Better CSS Font Stacks

This article gives some great guidelines for creating better CSS font stacks. It includes information on the most common font stacks currently used and then goes on to cover Tuck's Definitive Font Stacks and Ford's Better Font Stacks. It's a great resource when you're determining a site's typography, with the information presented in a very scannable, well-organized format.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed87b6b0-e222-41ff-b419-ae552642a0f1/buildbettercssfontstacks.jpg)

### CSS3 Embedding a Font Face

Here's a great tutorial on how to embed fonts using CSS3. While it's still not widely supported, this technique makes it much easier to embed special fonts into a site without having to resort to images.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bfc96ae-1448-4b3f-a5cf-f7b62be8e24b/css3embedafontface.jpg)

### CSS Gradient Text Effect

This little <a href="https://www.webdesignerwall.com/tutorials/css-gradient-text-effect/">trick</a> makes it easy to create gradient text by applying a 1 pixel gradient PNG to it. It's a quick and easy way to create gradient text pretty much anywhere on your site. There's even a fix to make it work in IE6 included.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b022834-03c2-4831-8e69-47bd2b10c4cb/cssgradienttexteffect.jpg)](https://www.webdesignerwall.com/tutorials/css-gradient-text-effect/)

## 5\. Other Cool Techniques, Tips, and Tricks

Below are a ton of other techniques and tricks you can use to really make your CSS stand out.</p>

### 3D Cube Using CSS Transformations

This is probably one of the coolest CSS techniques I've seen. <a href="https://www.fofronline.com/2009-04/3d-cube-using-css-transformations/">This tutorial</a> shows how to build a 3D cube with text or other content on each side of the cube. It does it entirely with CSS; there's no canvas, SVG, imagery, or JavaScript. There's even instructions for creating multiple shaded cubes on a single page. The only real drawback is that it's only supported in recent WebKit and Gecko browsers.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9d7c8a1-be9e-4308-be33-47b8e705fb18/3dcubeusingcsstransformatio.jpg)](https://www.fofronline.com/2009-04/3d-cube-using-css-transformations/)

### Nine Ways to Obfuscate E-mail addresses compared

This <a href="https://techblog.tilllate.com/2008/07/20/ten-methods-to-obfuscate-e-mail-addresses-compared/">article</a> gives two different methods for obfuscating email addresses with CSS. One involves using the display:none attribute while the other involves reversing the code. Both supposedly cut the amount of spam received to zero.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ff14e0c-023e-44fa-b183-295bfabfa1d0/waystoobfuscateemailaddress.jpg)](https://techblog.tilllate.com/2008/07/20/ten-methods-to-obfuscate-e-mail-addresses-compared/)

### Forms Markup and CSS - Revisited

Here is a CSS template for form styling. The markup of the form is based on the Accessible Forms Markup from Derek Featherstone. The template is semantically correct, flexible and accessible.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ad5c1a4-cdc2-471e-a888-b2cf4dc43d89/csshackforchromesafariinter.jpg)

### iPhone CSS

A very short and simple <a href="https://squaregirl.com/blog/2009/6/1/iphone-css.html">tutorial</a> on how to make certain elements of you CSS render differently on the iPhone. It's surprisingly simple and easy to implement.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bd17e48-bd3a-4f5d-9c90-105abd2fb273/iphonecss.jpg)](https://squaregirl.com/blog/2009/6/1/iphone-css.html)

### Improving Your Process: Faster Front End Development

While this post offers plenty of information on things other than CSS, it also offers some great advice for improving your efficiency with CSS: mainly, write your CSS in blocks. This technique is usually done progressively as you get used to coding in this manner. The steps are simple, though, and it's sure to make you a much faster designer.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8210da83-35ab-423c-a158-63c9dfed92a6/improvingyourprocessfasterf.jpg)

### Image-Free CSS Tooltip Pointers - A Use for Polygonal CSS?

This tutorial explains how to create triangles (to be used for pointers) using CSS, without the need for any images. The end result is great, though it only works for single-color images. The CSS used is incredibly simple while still being really versatile. You can create a triangle of almost any size using just a single div.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43870a8a-e99c-4ac6-b16f-4b91cc1f5544/imagefreecsstooltippointers.jpg)

### How I Implemented My Cookie-Based Switcher

While not strictly a CSS trick, this post shows how to create a cookie-based CSS theme switcher for WordPress. It allows users to choose to use a different theme when they visit the blog while allowing new users to see a nice, simple, easy-to-read theme that puts the primary focus on the content.

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e251bc-1e2d-4338-81c5-d80a4cdb008f/howiimplementedmycookiebase.jpg)

### CSS Swap Hover Effect

This great technique will replace any image with another image when you hover over it. The tutorial shows it applied to a portfolio site, but the possibilities are endless. It's very slick and cross-browser compatible (though IE6 does require a bit of a workaround, as usual).

![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2b6c4c8-d43b-40ad-9542-cb47e066072a/cssswaphovereffect.jpg)

### CSS Stacked Bar Graphs

Here's a <span class="removed_link" title="https://www.thewojogroup.com/2008/12/css-stacked-bar-graphs/">tutorial</span> for creating stacked bar graphs using CSS and some images. It's a pretty in-depth process, but the result looks fantastic.

<span class="removed_link" title="https://www.thewojogroup.com/2008/12/css-stacked-bar-graphs/">![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff0f39ad-ce74-45ad-8b32-254e9607e182/cssstackedbargraphs.jpg)</span>

### Changing HTML Images on Hover / A Quick CSS Trick

Here's a quick and easy CSS <a href="https://www.onderhond.com/blog/work/changing-html-images-on-hover">technique</a> for swapping out images on hover. It's pure CSS, no JavaScript required. The biggest issue this technique solves is that when the page is printed, the base image is the only one that shows up.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48774745-221c-4b7b-9be8-adab94e2471e/changinghtmlimagesonhover.jpg)](https://www.onderhond.com/blog/work/changing-html-images-on-hover)

### 10 Properties that Were Impossible to Implement in IE6

This <a href="https://www.productivedreams.com/properties-that-were-impossible-to-implement-in-ie6/">collection</a> of CSS tricks shows how to implement a number of styles that were supposedly impossible in Internet Explorer 6. It includes tricks for opacity, fixed positions, and text shadow, among others.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bcdd76f-626a-48b6-8bef-5f0e7c552e5d/propertiesimpossibletoimple.jpg)](https://www.productivedreams.com/properties-that-were-impossible-to-implement-in-ie6/)

### 10 Challenging But Awesome CSS Techniques

Sometimes the coolest things just take a bit more effort. This collection of <a href="https://net.tutsplus.com/tutorials/html-css-techniques/10-challenging-but-awesome-css-techniques/">tutorials</a> covers ten different CSS techniques that aren't exactly easy to achieve, but the end results are well worth the extra effort. Techniques include pull quotes, dynamic variables, and style changes based on the time of day or even the weather, among other awesome examples.

[![Screenshot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a642026-27cf-4ec3-b008-f477d7d74443/10challengingbutawesomecsst.jpg)](https://net.tutsplus.com/tutorials/html-css-techniques/10-challenging-but-awesome-css-techniques/)


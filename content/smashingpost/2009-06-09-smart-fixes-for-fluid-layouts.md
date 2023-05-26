---
title: 'Adaptive CSS-Layouts: New Era In Fluid Layouts?'
slug: smart-fixes-for-fluid-layouts
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/679065ef-6fb6-4363-a490-78c4fe55d214/development.gif
date: 2009-06-09T14:07:28.000Z
author: newsletter-team
description: >-
  **Fluid web designs** have many benefits, but only if implemented correctly. With proper technique, a design can be seen correctly on large screens, small screens and even tiny PDA screens. With bad coding structure, however, a fluid layout can be disastrous. Because of this, we need to find ways to work around most, if not all, of the cons of fluid design.
categories:
  - Coding
  - Layouts
  - CSS
---
If you as a designer are going to go through all the extra work of creating a functional fluid layout, why not go a bit further and make it compatible with all resolutions, instead of just most? You can use a few techniques to create an incredibly versatile, adaptive layout that will stay perfectly functional with the constantly changing screen sizes.

In this article, we'll discuss **effective techniques to create 100%-functional adaptive CSS-layouts**, and provide details on other tutorials and practices.

Also consider our previous articles:

*   [Fixed vs. Fluid vs. Elastic Layout: What’s The Right One For You?](https://www.smashingmagazine.com/2009/06/02/fixed-vs-fluid-vs-elastic-layout-whats-the-right-one-for-you/)  
    This article discusses the pros and cons of each type of layout. Either one can be used to make a successful website layout, as long as you keep usability in mind.
*   [Flexible Layouts: Challenge For The Future](https://www.smashingmagazine.com/2008/06/26/flexible-layouts-challenge-for-the-future/ "Flexible Layouts: Challenge For The Future")  
    Discusses the challenges of flexible layouts for the future.
*   <span class="removed_link" title="https://www.smashingmagazine.com/2007/11/23/screen-resolutions-and-better-user-experience">Screen Resolutions and Better User Experience</span>  
    Introduces the issue of screen resolutions, then considers the average user's profile.

{{% feature-panel %}}

## 1\. Fluid Layout Using A Grid

Most of us have heard of the [960 Grid System](https://960.gs) for designing fixed-width Web pages. Using 960 often makes fixed-width design preferable to fluid layouts. However, there is a way to create a grid-based **elastic layout**. Elastic layouts are, technically, different than fluid layouts in their coding structure, but they provide almost identical results for the user.</p>

### What Is a Fluid Grid?

A fluid grid can be created through a smart use of DIV layers, percentages and very simple math. The idea comes from [Ethan Marcotte](https://www.alistapart.com/articles/fluidgrids), who realized that the "em" unit could go further than font size. We'll go over the basics here, but for a complete and detailed overview of the method, read the article [Fluid Grids](https://www.alistapart.com/articles/fluidgrids) by Ethan Marcotte, which is a complete walk-through and tutorial on creating a grid-based elastic layout.

The idea here is to use relative units, a combination of percentages and em's, and to use simple division to find the equivalents of pixel widths that would normally be used for fixed-width design.</p>

### The Benefits

*   This method allows you to have a grid layout, which once only seemed possible with fixed-width layouts.
*   The user can view the entire layout using their preset text size, and everything will stay in proportion.
*   The layout style uses concepts that are cross-browser compatible.
*   Once understood, the concept is a fairly easy fix for most problems with fluid design.</p>

### How to Create a Fluid Grid Layout

The first step in creating this fluid layout is to create a mock-up of the preferred fixed-width layout. This way, the designer can still see the proportions and can apply Divine Proportion, balance and appropriate spacing techniques.

![Fixed-width version of our final result](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/084dd6b4-d020-491a-b593-b0b7fd9f11a3/fixed-mockup.jpg)

From the simple layout above, we can see how we would code this in CSS. 960 pixels would be our fixed width, and we would force a horizontal scroll bar for any resolution narrower than this. All of our content is in a wrapper that is 880 pixels wide. We have 40-pixel margins on both the left and right side, and 20 pixels of spacing between all of our elements.

Everything’s fine until we start thinking about usability. This type of layout would probably work well for many users; but not for everyone. So, let’s transfer this to a fluid layout. If we want this layout to maintain its proportions at any screen resolution, we’ll have to change our 960-pixel width to 100%, and then find the percentage equivalents of 880 pixels, 640 pixels and 220 pixels.

This just requires some rational thinking. In our fixed-width mock-up, our entire wrapper was 880 pixels, within the 960-pixel-wide design. If we want the equivalent in a percentage, all we have to do is divide:

880 pixels ÷ 960 pixels = 0.91666667

Take that decimal number, turn it into a percentage and you get 91.666667%. Now, because **browsers handle percentages differently, it would not be wise to put all those decimals places straight into the layout.** Browsers either round up or down, so to know exactly what we’re working with, we should round it to a whole number ourselves. Since it’s closer to 92%, we’ll round up. If we need to round it down later because of extra spacing issues, that’s easily done.

<pre><code class="language-css">name="code">
wrapper {
	width: 92%;
}</code></pre>

For the content and sidebar areas, we need to do the same thing, but in the right proportion. Because these two areas are within the 880-pixel-wide wrapper DIV, we need to find the percentages of these relative to this DIV:

640 pixels ÷ 880 pixels = 0.727272 → 73%

220 pixels ÷ 880 pixels = 0.25 → 25%

<pre><code class="language-css">name="code">
content {
	width: 73%;
}

sidebar {
	width: 25%
}</code></pre>

Let’s actually round the content area down to 72%, so that our layout doesn’t break. Because it has to be positioned next to the navigation bar, we don’t want it to be too wide.

![Our fixed-width layout mock-up with percentage equivalents.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89ac9c5a-413c-427f-b537-69974817710f/percentage-equivilant.jpg)

This is a very easy concept and a much more efficient way to handle proportions in fluid design. With this technique, a designer doesn’t have the excuse that proportions cannot be maintained and ruin the aesthetic appeal of their layouts.</p>

### A Note About Margins

Designers will determine the length of the margins in different ways. One way is to calculate the percentages of the margins (in this case, 20 pixels ÷ 880 pixels). Another is to set fixed margins or, as in our example, hard-code them in as 20 pixels.

Each method has its pros and cons. With percentage margins, the designer risks the margins being too wide in very large screen resolutions but probably achieves better proportion. Fixed margins may cause slight imperfections in the proportions but guarantees that the spacing will look right no matter what the screen size.</p>

## 2\. Adaptive Content

Another common problem with fluid designs is that even though they adapt to many screen resolutions, if the resolution gets too small (such as on a phone or PDA) or incredibly large, things start to look a bit funny. For example, a three-column layout would look very cluttered on a PDA screen whose resolution is only 240-pixels wide.

To address this problem, we can use a technique that involves adapting content to a specific ranges of screen resolutions. Fortunately, we can still use the technique outlined above to retain our proportions, and then we can add this technique for even better usability.</p>

### Fluid Layout with Adaptive Content

Most fluid layouts look great in screen resolutions of 800x600 pixels up to 1280-pixels wide and larger. However, it would be even better if we could break it up a bit more and create slightly different custom-made layouts for resolutions that are 800 to 1024 pixels, 1024 to 1280 pixels and 1280 pixels and up. Likewise, custom adjustments could be made for screen resolutions that are 640 to 800 pixels, 320 to 640 pixels, 240 to 320 pixels, and 240 pixels and below.

An example of this technique is used on [The Man in Blue](https://themaninblue.com):

![A layout for a screen resolution of 800 pixels and wider.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d69f547f-8f8f-4a22-8152-9093ce89af4d/800orabove.jpg)

![A layout for a screen resolution of 800 pixels and narrower.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02c7c3a4-eaa2-41dc-a885-e074106d43b6/800orbelow.jpg)

The example above has only two separate style sheets: one for resolutions wider than 800 pixels and one resolutions narrower than 800 pixels. A better implementation of this technique would have several layout styles to more accurately accommodate different screen resolutions. [Marc Van Den Dobblesteen's layout example, Switchy McLayout](https://www.alistapart.com/d/switchymclayout/transition_layout_tab.html), provides a perfect example of using these alternative style sheets.</p>

### The Benefits

*   The designer is able to see with greater accuracy what a design will look like in different resolutions.
*   Better adherence to design principles of spacing and balance, no matter what platform the design is viewed on.
*   The tiniest and largest resolutions are handled with perfection.</p>

### Create a Fluid Layout with Adaptive Content

To create this type of layout, we need two things: separate style sheets for every range of screen resolutions, and a way of determining a user's screen resolution. A popular walk-through of this is the article [Dynamic Resolution-Dependent Layout Technique](https://particletree.com/features/dynamic-resolution-dependent-layouts) by Kevin Hale.

The first step is to create a set of alternative layout files. For example, one could be called _narrow.css_ and would be tailored to very narrow resolutions. Another could be _normal.css_ and would apply to conventional computer screen resolutions, and a third could be _wide.css_ and would handle unusually large resolutions.

We can then use JavaScript to make some simple alterations depending on the preset style sheets. [Dynamic Resolution Dependent Layouts](https://particletree.com/features/dynamic-resolution-dependent-layouts/) offers some sample JavaScript in the demo explains how it is being used. Declarations of all the style sheets and the JavaScript file are then put in the header, just like any other type of layout.

<pre><code class="language-markup tmp-xml"><b>&lt;!-- Narrow style sheet --></b>
&lt;link rel="alternate stylesheet" type="text/css" href="css/narrow.css"
title="narrow"/>

<b>&lt;!-- Default style sheet --></b>
&lt;link rel="stylesheet" type="text/css" href="css/normal.css" title="default"/>

<b>&lt;!-- Wide style sheet --></b>
&lt;link rel="alternate stylesheet" type="text/css" href="css/wide.css" 
title="wide"/>

<b>&lt;!-- Included JavaScript to switch style sheets --></b>
&lt;script src="scripts/dynamiclayout.js" type="text/javascript">&lt;/script></code></pre>

Notice the **title attribute** in all three links to the style sheets: "narrow," "default" and "wide." Taking a closer look at the `DynamicLayout()` function in the JavaScript source, we can see that it is quite easy to customize which style sheet is called according to each title attribute. We can also see how to change the pixel widths accordingly.

<pre class="js" name="code">
function dynamicLayout(){
    var browserWidth = getBrowserWidth();

    <b>// Narrow CSS rules</b>
    if (browserWidth < 640){
        changeLayout("narrow");
    }
    <b>// Normal (default) CSS rules</b>
    if ((browserWidth >= 640) && (browserWidth <= 960)){
        changeLayout("default");
    }
    <b>// Wide CSS rules</b>
    if (browserWidth > 960){
        changeLayout("wide");
    }
}
</pre>

This technique is very easy to implement and works great with other techniques for creating more usable fluid layouts. Take a closer look at the JavaScript to see in more detail how things work.</p>

### Similar Techniques

	For a similar technique, look over [Dynamic layouts with adaptive columns](https://www.brandspankingnew.net/archive/2005/12/dynamic_layouts_with_css_javascript.html) over at [Brand Spanking New](https://www.brandspankingnew.net). It features generally the same code, although slightly different. There are fortunately many options and script examples for getting the same adaptive content technique to work.

  [![An adaptive layout.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7422c969-970a-40ec-aace-05c80f2e0ace/adaptivelayout1.jpg)](https://www.brandspankingnew.net/specials/adaptLayout/adaptive_columns_01.html)

	[![An adaptive layout.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/056542d3-3a40-400e-916e-864ef37f1bbf/adaptivelayout2.jpg)](https://www.brandspankingnew.net/specials/adaptLayout/adaptive_columns_01.html)

	To download the script for this version of adaptive content, go to [Dynamic layouts with adaptive columns](https://www.brandspankingnew.net/archive/2005/12/dynamic_layouts_with_css_javascript.html).

	The concept isn't difficult, and many developers have made their own version of this technique. A great source to find even more examples of adaptive content layouts and scripts is Clagnut.com's blog post, "[Variable fixed width layout](https://clagnut.com/blog/1663)". There is even one such technique featured on this post that requires no JavaScript whatsoever: [CSS Drop Column Layout](https://muffinresearch.co.uk/archives/2006/02/07/css-drop-column-layout).</p>

## 3\. Images In A Fluid Layout

One major concern among developers of fluid layouts is dealing with images and other content that requires a set width. In most cases, we'd all like our images to be as large as possible, or at least to prevent any awkward white space if they're too small. In a fixed-width layout, adjustments can be made manually, but quite easily, to overcome these issues. However, in a fluid layout, in which the width of the area where images appear is constantly changing, these problems can come up all over again.</p>

### Automatic Magazine Layout

One solution requires some smart algebra and PHP. The full explanation (including the math) and the downloadable source code is available in the article [Automatic Magazine Layout](https://www.alistapart.com/articles/magazinelayout) by Harvey Kane. The title derives from how images are displayed in magazines: **organized and always perfectly aligned**. Of course, a magazine designer has to go through a certain process to achieve this look, involving resizing and manual placement.

There is now a technique that achieves this effect for us, too. Below is the first example of what the script can do:

![Example 1 from the Automatic Magazine Layout by Harvey Kane](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f382e8dd-e400-420b-af3f-7ba0c39bed59/automatic-ex1.jpg)

As you can see, things are definitely prettier. But how does it make things more usable with a fluid design? Harvey Kane gives the PHP script that we need to use:

<pre><code class="language-php"># include the class file
require_once('magazinelayout.class.php');

<b># Define the width for the output area (pixels)
$width = 600;</b>

# Define padding around each image; this *must* be included 
#in your style sheet (pixels)
$padding = 3;

# Define your template for outputting images
# (Don't forget to escape the &)
$template = '&lt;img src="image.php?size=[size]&amp;file=[image]" alt="" /&gt;';

# create a new instance of the class
$mag = new magazinelayout($width,$padding,$template);

# Add the images in any order
$mag->addImage( 'landscape1.jpg' );
$mag->addImage( 'portrait1.jpg' );
$mag->addImage( 'landscape2.jpg' );

# display the output

echo $mag->getHtml();</code></pre>

We can predefine the width that we'd like our entire magazine-inspired image layout to render as. So, if we can find out what the user's browser width is, we can determine how wide our image layout should be. This is easy enough, because we've already done it with our second technique: fluid layouts with adaptive content. In his script, Kevin Hale uses a **method called `getBrowserWidth()`**. You can get a more in-depth look at the code for this method in his article.

If we can use this method to retrieve the browser's width as a number, then we can use this number to find the pixel width of our content area (or whatever area these images are going to be placed in). Let's say we'd like to put the images in our content area, which is set to 70% width. Using simple math, we just need to find out how many pixels is 70% of the browser's width.

<pre><code class="language-php">Pixel width = Percentage of Content Area x Browser Width
$width = 0.70 x getBrowserWidth();</code></pre>

This is, of course, pretty basic math, and a pretty basic solution for dealing with images in fluid layouts, once the initial PHP script is set up. Adjust the PHP script to automatically find the pixel width of the images, and you've got a great way of dealing with images, or any other content that has a set width, in a fluid layout.</p>

## 4\. jQuery Masonry

	There are enough problems in CSS without thinking about constantly changing screen resolution. There is one common problem, though, that many designers may face more than others — multiple content boxes. When working with many floated elements, some awkward extra whitespace may show up between sections of varying heights. An example of this is below.

	![Awkward, uneven space with floated divs.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e442f00e-a279-4c5c-8d19-3ed0bc24f151/jquerymasonry1.jpg)

	If we want to use divs in this way in a fixed-width layout, the fix is easy: just manually adjust the divs until everything is in place. Dealing with divs in this fashion in a fluid layout almost seems impossible. Every time the layout is adjusted, we get weird whitespace in a new spot, and in different amounts.

	![Extra whitespace caused by the layout colapsing into two columns.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0f63c27-f166-4d50-8750-ade75a7e69ff/jquerymasonry2.jpg)

	Viewing the same layout in a thinner resolution causes the layout to collapse into a 2-column layout, as it should. However, when this happens, we get a different whitespace issue. Any designer can see this is a very ugly problem for layouts, and often times layouts like these are forced into fixed width because there seems to be no way around the problem.

	Fortunately, it's not an impossible fix, but rather an incredibly easy one — thanks to David DeSandro's jQuery Plugin: jQuery Masonry.</p>

### What is jQuery Masonry?

	jQuery Masonry is a very easy to use jQuery plugin. In the words of David DeSandro himself, "Think of Masonry as the flip side of CSS floats. Where as floats arrange elements horizontally then vertically, Masonry arranges them vertically then horizontally. The result leaves no vertical gaps between elements of varying height, just like a mason fitting stones in a wall."

### How to Use the jQuery Masonry Plugin

	In the example above, all of the boxes are placed in paragraphs with an ID of "item". This item ID has a set width of 30%, and floats to the left. All of these 'item' paragraphs are then placed inside of a very basic wrapper with its own fluid width of 90%. Once the paragraphs reach the end of the wrapper width, they'll go to the next available line — whether it causes too much whitespace or not.

	Fixing it is as easy as downloading the jQuery Masonry plugin, and applying the .masonry() method to our wrapper ID.

	<pre class="js" name="code">$('#wrapper').masonry();</pre>

	The two images below show the power of this plugin. First is the layout on a large screen resolution, second is the same layout on a lower screen resolution when collapsed to two columns.

	![Fixed full-width layout.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee831284-63ae-47b5-842c-f7ebde208093/jquerymasonry3.jpg)

	![Fixed collapsed layout.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c375366e-84a6-4f1e-8370-ac5c62b1915c/jquerymasonry4.jpg)

### One Bug to this Plugin, and One Fix

	To download the script for this version of adaptive content, go to [Dynamic layouts with adaptive columns](https://www.brandspankingnew.net/archive/2005/12/dynamic_layouts_with_css_javascript.html).

	The concept isn't difficult, and many developers have made their own version of this technique. A great source to find even more examples of adaptive content layouts and scripts is Clagnut.com's blog post, "[Variable fixed width layout](https://clagnut.com/blog/1663)". There is even one such technique featured on this post that requires no JavaScript whatsoever: [CSS Drop Column Layout](https://muffinresearch.co.uk/archives/2006/02/07/css-drop-column-layout).</p>

## 3\. Images In A Fluid Layout

One major concern among developers of fluid layouts is dealing with images and other content that requires a set width. In most cases, we'd all like our images to be as large as possible, or at least to prevent any awkward white space if they're too small. In a fixed-width layout, adjustments can be made manually, but quite easily, to overcome these issues. However, in a fluid layout, in which the width of the area where images appear is constantly changing, these problems can come up all over again.</p>

### Automatic Magazine Layout

One solution requires some smart algebra and PHP. The full explanation (including the math) and the downloadable source code is available in the article [Automatic Magazine Layout](https://www.alistapart.com/articles/magazinelayout) by Harvey Kane. The title derives from how images are displayed in magazines: **organized and always perfectly aligned**. Of course, a magazine designer has to go through a certain process to achieve this look, involving resizing and manual placement.

There is now a technique that achieves this effect for us, too. Below is the first example of what the script can do:

![Example 1 from the Automatic Magazine Layout by Harvey Kane](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f382e8dd-e400-420b-af3f-7ba0c39bed59/automatic-ex1.jpg)

As you can see, things are definitely prettier. But how does it make things more usable with a fluid design? Harvey Kane gives the PHP script that we need to use:

<pre><code class="language-php"># include the class file
require_once('magazinelayout.class.php');

<b># Define the width for the output area (pixels)
$width = 600;</b>

# Define padding around each image; this *must* be included 
#in your style sheet (pixels)
$padding = 3;

# Define your template for outputting images
# (Don't forget to escape the &)
$template = '&lt;img src="image.php?size=[size]&amp;file=[image]" alt="" /&gt;';

# create a new instance of the class
$mag = new magazinelayout($width,$padding,$template);

# Add the images in any order
$mag->addImage( 'landscape1.jpg' );
$mag->addImage( 'portrait1.jpg' );
$mag->addImage( 'landscape2.jpg' );

# display the output

echo $mag->getHtml();</code></pre>

We can predefine the width that we'd like our entire magazine-inspired image layout to render as. So, if we can find out what the user's browser width is, we can determine how wide our image layout should be. This is easy enough, because we've already done it with our second technique: fluid layouts with adaptive content. In his script, Kevin Hale uses a **method called `getBrowserWidth()`**. You can get a more in-depth look at the code for this method in his article.

If we can use this method to retrieve the browser's width as a number, then we can use this number to find the pixel width of our content area (or whatever area these images are going to be placed in). Let's say we'd like to put the images in our content area, which is set to 70% width. Using simple math, we just need to find out how many pixels is 70% of the browser's width.

<pre><code class="language-php">Pixel width = Percentage of Content Area x Browser Width
$width = 0.70 x getBrowserWidth();</code></pre>

This is, of course, pretty basic math, and a pretty basic solution for dealing with images in fluid layouts, once the initial PHP script is set up. Adjust the PHP script to automatically find the pixel width of the images, and you've got a great way of dealing with images, or any other content that has a set width, in a fluid layout.</p>

## 4\. jQuery Masonry

	There are enough problems in CSS without thinking about constantly changing screen resolution. There is one common problem, though, that many designers may face more than others — multiple content boxes. When working with many floated elements, some awkward extra whitespace may show up between sections of varying heights. An example of this is below.

	![Awkward, uneven space with floated divs.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e442f00e-a279-4c5c-8d19-3ed0bc24f151/jquerymasonry1.jpg)

	If we want to use divs in this way in a fixed-width layout, the fix is easy: just manually adjust the divs until everything is in place. Dealing with divs in this fashion in a fluid layout almost seems impossible. Every time the layout is adjusted, we get weird whitespace in a new spot, and in different amounts.

	![Extra whitespace caused by the layout colapsing into two columns.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c0f63c27-f166-4d50-8750-ade75a7e69ff/jquerymasonry2.jpg)

	Viewing the same layout in a thinner resolution causes the layout to collapse into a 2-column layout, as it should. However, when this happens, we get a different whitespace issue. Any designer can see this is a very ugly problem for layouts, and often times layouts like these are forced into fixed width because there seems to be no way around the problem.

	Fortunately, it's not an impossible fix, but rather an incredibly easy one — thanks to David DeSandro's jQuery Plugin: jQuery Masonry.</p>

### What is jQuery Masonry?

	jQuery Masonry is a very easy to use jQuery plugin. In the words of David DeSandro himself, "Think of Masonry as the flip side of CSS floats. Where as floats arrange elements horizontally then vertically, Masonry arranges them vertically then horizontally. The result leaves no vertical gaps between elements of varying height, just like a mason fitting stones in a wall."

### How to Use the jQuery Masonry Plugin

	In the example above, all of the boxes are placed in paragraphs with an ID of "item". This item ID has a set width of 30%, and floats to the left. All of these 'item' paragraphs are then placed inside of a very basic wrapper with its own fluid width of 90%. Once the paragraphs reach the end of the wrapper width, they'll go to the next available line — whether it causes too much whitespace or not.

	Fixing it is as easy as downloading the jQuery Masonry plugin, and applying the .masonry() method to our wrapper ID.

	<pre class="js" name="code">$('#wrapper').masonry();</pre>

	The two images below show the power of this plugin. First is the layout on a large screen resolution, second is the same layout on a lower screen resolution when collapsed to two columns.

	![Fixed full-width layout.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee831284-63ae-47b5-842c-f7ebde208093/jquerymasonry3.jpg)

	![Fixed collapsed layout.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c375366e-84a6-4f1e-8370-ac5c62b1915c/jquerymasonry4.jpg)

### One Bug to this Plugin, and One Fix

	When using this plugin, one will notice that the div layers stay in the same spot if a user were to resize their browser. Upon refresh, the layout is fixed and works appropriately again. However, the user will not know they need to refresh to fix the problem, so changing the HTML code below will correct this bug quite easily.

	<pre class="js" name="code">&lt;body onresize="window.location=window.location;"></pre>

	Now, every time the user changes their browser size, the browser will autmoatically refresh and reload the entire script.</p>

## 5\. Smart Columns with jQuery & CSS

	The jQuery fix above solves problems with divs of varying height, but for a layout intended to have even div heights, it might not be the best solution. Soh Tanaka of SohTanaka.com has come up with a jQuery script and a smart use of CSS to make columns in fluid layouts collapse and expand elegantly. For an example, check out the demo: Smart Columns w/ CSS & jQuery.</p>

### What are Smart Columns with jQuery & CSS?

	Smart Columns are a script that can alter the width of the divs for the best viewing quality, and also determine how may columns can be viewed across that page for the browsers current size. It is also perfect for users who resize their browsers, rather than just accomodating browser size on entry to the website.

	![Smart Columns with jQuery and CSS](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5577a446-0dc6-4ffd-9f6e-a5c8c910b3d3/smartwidth1.jpg)

	![Smart Columns with jQuery and CSS](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f73ec44a-da34-4935-b51e-a42e84073c58/smartwidth2.jpg)

	The script takes the remaining whitespace off of the end of a row of columns, which may be caused by varying browser widths, and then places them evenly throughout the columns using jQuery.</p>

### How to Get Smart Columns

	The code is all laid out in Soh Tanakas blog post: Smart Columns w/ CSS and jQuery. It can be set up using a list, with each block item as a <li> element.

<pre class="js" name="code">&lt;ul class="column">
	&lt;li>
		&lt;div class="block">
		Block 1
		&lt;/div>
	&lt;/li>

	&lt;li>
		&lt;div class="block">
		Block 2
		&lt;/div>
	&lt;/li>

	&lt;li>
		&lt;div class="block">
		Block 3
		&lt;/div>
	&lt;/li>
&lt;/ul></pre>

	Then, by intserting the CSS and jQuery code into the page (Soh Tanaka has easily laid this out in the above post), the smart columns will work. Customizing the code is easy, and only requires editing the CSS in terms of width, height, and margins.</p>

## 6\. Text Zooming

	Another common problem among fluid layouts is the concern that the text either gets so stretched or squished that the layout loses readability. The image below shows this problem, both for an incredibly wide screen, and then for a very thin screen. The very thin screen seems to host the biggest problem by causing big gaps in the text, but both instances can frustrate the user equally.

	![Readibility can be an issue with fluid layouts.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b81f4b8a-eee9-466a-97ed-1aaf25688bd8/textzooming1.jpg)

	<p>One method to combat this is to use min-width and max-width, although that has two problems:
<ol><br>
<li>Min-width and max-width are not supported in all browsers,</li>
<li>the layout is then just resorting to a partially fixed-width layout, and we lose overall flexibility again.</li>
</ol>

	<p>Luckily, James over at <a href="https://tinnedfruit.com">Tinned Fruit</a> has created a script that does something to fight this problem.</p>

	<h4>What is Text Zooming?</h4>	
	<p>Text Zooming, as he calls it, is a JavaScript that automatically resizes text based on the width of the user's screen. As the screen gets wider, the text gets larger. Likewise, as the screen gets thinner the text gets smaller. In addition to this basic functionality, a designer can set a max and min text size so the user never sees any oddly sized text.</p>

	<p>For a live demo, go to his Text Zooming page. As one can see, the script degrades nicely, and the larger text is easy to read on a wide resolution, just as the smaller text is to read on a thinner resolution. Better yet, the header and navigation don't change in size, so a designer can choose which elements should use the text zoom.</p>

	<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ef0e871-558a-454d-868e-0410ab919486/tz.gif" alt="Text Zooming in action." width="450" height="370" /></p>
	<p>Above is a portion of the maximized page (large width) that is displaying larger text.</p>
	<p class="showcase"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/141890e9-8a3a-41e7-b564-3a9d782e3743/tz2.gif" width="450" height="380" alt="Text Zooming in action." /></p>
	<p>Above is the same page, only minimized to about 700px in width. The text is resized along with the browser.</p>

	<h4>How to Get Text Zooming</h4>
	<p>Text zooming is a basic JavaScript that one can include to a web page externally. To download the JS file and read further instructions, head on over to the demo page: Text Zooming.</p>

	<p>Below the external script line, it's as easy as intserting the following code and changing it as necessary.</p>

<pre class="js" name="code">
&lt;script type="text/javascript">
  var contentZoom = new TextZoom(
    "Content", // Reference element
    "Content", // Target element
    0.22, // Zoom ratio
    70, // Minimum font size (%)
    130); // Maximum font size (%)
  addLoadEvent(textZoomInit);
&lt;/script>
</pre>

## Conclusion

<p>All of these techniques can be implemented in one design to create a <strong>very user-friendly fluid layout</strong>. A smart use of the fluid grid can create an adaptable layout whose proportions remain faithful to the Rule of Thirds, balance and other design principles. The adaptive content technique can handle unusually small and large screen resolutions with a bit of customization, so the designer is sure to get the perfect look for all users. And the third technique is a good one for making sure that images and other pieces of content with set widths aren't too large for the screen.</p>
<p>jQuery Masonry leaves no vertical gaps between elements of varying height, just like a mason fitting stones in a wall; thet "Smart Columns techniques" makes columns in fluid layouts collapse and expand elegantly and Text Zooming
provides a JavaScript that automatically resizes text based on the width of the user's screen.</p>

<p>Hopefully, <strong>advanced fluid layout techniques will signal a new era in layout design</strong>. With the growing variety of screen widths, it's only a matter of time before these techniques become essential.</p>

## Further Resources

<p>You may also be interested in these additional resources:</p>

- [Responsively Retrofitting An Existing Site With RWD Retrofit](https://www.smashingmagazine.com/2013/03/18/retrofit-a-website-to-be-responsive-with-rwd-retrofit/)
- [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
- [Responsive Web Design Techniques, Tools and Strategies](https://www.smashingmagazine.com/2011/07/responsive-web-design-techniques-tools-and-design-strategies/)
- [The State Of Responsive Web Design](https://www.smashingmagazine.com/2013/05/the-state-of-responsive-web-design/)
- [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)

{{< signature "al" >}}


---
title: 'Styling HTML Lists with CSS: Techniques and Resources'
slug: styling-html-lists-with-css-techniques-and-resources
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1206652f-18d7-440e-a752-ef7e4adcbc02/css-lists.jpg
date: 2009-12-11T11:27:15.000Z
author: louis-lazaris
description: >-
  In an online world now dominated by CSS layouts, CSS-styled HTML lists have become invaluable tools in a CSS developer's toolbox, due to the HTML lists versatile and graphically flexible nature. All this despite some of the obvious browser inconsistencies that can affect the styling of the different types of lists available in HTML coding.
categories:
  - Coding
  - CSS
  - Techniques
  - Essentials
---
If you're new to CSS, this article should provide a good overview of the different types of lists available, as well as some of the browser quirks that occur in relation to HTML lists, with some helpful advice that should prevent those quirks from becoming major road blocks to good design.

You might be interested in the following related posts:

*   [Mastering CSS Coding: Getting Started](https://www.smashingmagazine.com/2009/10/mastering-css-coding-getting-started/)
*   [CSS3 Flexible Box Layout Explained](https://www.smashingmagazine.com/2011/09/css3-flexible-box-layout-explained/)
*   [Challenging CSS Best Practices](https://www.smashingmagazine.com/2013/10/challenging-css-best-practices-atomic-approach/)
*   [The Mystery Of The CSS Float Property](https://www.smashingmagazine.com/2009/10/the-mystery-of-css-float-property/)

In addition, we'll look at a <strong>showcase of various uses, techniques, and tutorials that utilize HTML lists</strong>. All of this should put strong emphasis on the importance of using lists in modern web design, reminding even experienced coders how HTML lists can improve the flexibility and maintainability of a website.

{{% feature-panel %}}

## Available List Options

### Unordered Lists: <ul>

Unordered lists are the most commonly used lists. Here is an image showing what an unstyled unordered list looks like in different browsers:

<figure><img title="Unordered lists in multiple browsers" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e54778e-4c48-4b13-a72d-8b9d025556e0/lists-browsers.jpg" alt="Unordered lists in multiple browsers" width="500" height="340" /></figure>

As you can see above, the default settings for unordered lists are somewhat different across various browsers. Of course, <strong>nowadays it is rare to see a naked unordered list</strong> on any website. Also, a good <a href="https://meyerweb.com/eric/tools/css/reset/" rel="nofollow">CSS reset</a> will normalize those differences, bringing the list down to bare text with no bullets and no margins or padding.

CSS properties that are specific to unordered lists include <code>list-style-type</code>, <code>list-style-position</code>, and <code>list-style-image.</code> These properties set the type of marker (or bullet), the position of the marker, and an image to replace the marker. These three properties can be combined using the shorthand <code>list-style</code> property.

The <code>list-style-type</code> property can be set to a number of different values, some of which are shown in the chart below:

<figure><img title="Unordered list markers" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7db7b396-48da-4e19-9df5-ed21d9de5d39/list-markers.jpg" alt="Unordered list markers" width="500" height="181" /></figure>

Depending on the user's browser and system, certain values for <code>list-style-item</code> may not appear correctly, often defaulting to <code>decimal</code>. Using an incrementing value for an unordered list is not recommended since that would take away the semantic value of the <strong>unordered</strong> list.

The <code>list-style-position</code> property specifies the position of the list marker, and can be set to either <code>outside</code> (the default) or <code>inside</code>. This property would also set the position of an image, if the <code>list-style-image</code> property is set.

The <code>list-style-image</code> property can be used to give the unordered list a custom look with unique "bullets". Unfortunately, <strong>this method of adding a bullet to an unordered list is buggy in Internet Explorer</strong>, and is rarely used. A much better solution is to add a background image to the <code>&lt;li&gt;</code> elements on the list, adjusting the position of the background image accordingly, and setting it to <code>no-repeat</code>. This solution is explained through a series of steps at <a href="https://css.maxdesign.com.au/listutorial/introduction.htm" rel="nofollow">maxdesign.com</a>, and works nicely in all browsers.</p>

### Ordered Lists: <ol>

Ordered lists are used when a list of items requires a visible incrementing value before each item. The value for the marker on an ordered list can be set to any of the values also available for an unordered list, as discussed above. In most cases, an ordered list would either have an incrementing marker on the list items, or no marker at all. So, it would be unlikely that you would change the marker from an incrementing one to a non-incrementing one on an <strong>ordered list</strong>, since that would remove the semantic value of the items.</p>

### Definition Lists: <dl>

Definition lists are used to mark up lists of items that have definitions. They consist of definition terms (<code>&lt;dt&gt;</code>) along with definitions (<code>&lt;dd&gt;</code>). The pairings for definition list items do not have to be exactly paired up. The following is perfectly valid in XHTML Strict:

<pre><code class="language-markup tmp-xml">&lt;dl&gt;
  &lt;dt&gt;calculator&lt;/dt&gt;
  &lt;dt&gt;abacus&lt;/dt&gt;
  &lt;dd&gt;A machine used for making numerical calculations.&lt;/dd&gt;
&lt;/dl&gt;</code></pre>

Thus, you could have more than one <code>&lt;dt&gt;</code> with a single <code>&lt;dd&gt;</code>, or even have multiple <code>&lt;dd&gt;</code> tags and only one <code>&lt;dt&gt;</code>.

The visual display of a definition list, by default, is virtually the same across all browsers, as shown in the image below:

<figure><img title="A definition list" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/831400be-13c1-4b61-8a3d-7be597f5c2aa/definition-list.jpg" alt="A definition list" width="500" height="128" /></figure>

### Deprecated Lists: <menu> & <dir>

The &lt;menu&gt; and &lt;dir&gt; elements also, technically, qualify as "HTML lists", but they are deprecated in XHTML, so I won't discuss those in detail here.</p>

### Lists in HTML5

In HTML5, the unordered list has basically remained the same, although now it seems to be referred to simply as a "list". The new <code>&lt;nav&gt;</code> element will be used to wrap a list that is used for navigation.

The <code>&lt;ol&gt;</code> element has slightly changed, gaining two new attributes: <code>reversed</code>, which is a Boolean that indicates if the list should be ascending or descending, and <code>start</code>, which is an integer that declares the starting point of the ordered list items.

Also, the <code>&lt;figure&gt;</code> and <code>&lt;details&gt;</code> elements have been added. Those new tags will have children that include <code>&lt;dt&gt;</code> and <code>&lt;dd&gt;</code> elements.

For further information on <strong>lists in HTML5</strong>, see the HTML5 Draft Standard.

## Browser Differences

There are some notable differences across the most commonly-used browsers when certain styles are applied to ordered or unordered lists. Let's take a look at some of these differences. Of course, this assumes there are no other styles associated with the elements, including those in a CSS reset.</p>

### Adding "display: block" to List Items

In Internet Explorer 8, Opera 9, Chrome, Firefox 2 &amp; 3, and Safari, adding <code>display: block</code> to the <code>&lt;li&gt;</code> elements in an ordered or unordered list will make the bullets or numbers disappear.

<figure><img title="display: block in IE8 and Other Browsers" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3291ce08-7b28-4b2c-bd73-6dabee357739/display-block.jpg" alt="display: block in IE8 and Other Browsers" width="500" height="126" /></figure>

In IE6 and IE7 the bullets and numbers will still be visible, even with <code>display: block</code> applied to the list items.

<figure><img title="display: block in IE6 &amp; IE7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58e7ec01-dcb6-4111-ab71-14868649dc0a/display-block-2.jpg" alt="display: block in IE6 &amp; IE7" width="500" height="126" /></figure>

### Adding "float: left" to List Items

In Internet Explorer 6 and 7, adding <code>float: left</code> to the list items (with no other styles present) will align the list items horizontally and the list bullets (or list numbers) will disappear. In IE8 and all other browsers, the list items will align horizontally, but the list bullets (or list numbers) will still be visible.

Another factor to keep in mind when the list items are floated is that the list container (the <code>&lt;ul&gt;</code> element) will collapse when it contains only floated elements. This occurs the same way in all browsers. Adding <code>overflow: hidden</code> to the <code>&lt;ul&gt;</code> or <code>&lt;ol&gt;</code> element is one way to resolve this issue.

To achieve virtually the same effect as <code>float: left</code> in all browsers, <strong>the best solution is to use <code>display: inline</code></strong>.</p>

### Ordered List Items That Have "Layout" in IE

In IE6 &amp; IE7, if the list items in an ordered list have "Layout", the numbers in the ordered list will not increment, and will all show as "1", as shown in the image below:

<figure><img title="Non-Incrementing Numbers in IE6 &amp; IE7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7183743-82b4-42ad-8dcb-6a303215024f/non-increment.jpg" alt="Non-Incrementing Numbers in IE6 &amp; IE7" width="500" height="200" /></figure>

The <code>hasLayout</code> property cannot be set directly, but it can be changed if an element is given an explicit width or height, or the element is floated or absolutely positioned, among other things. For a thorough discussion of the <code>hasLayout</code> property, <a href="https://reference.sitepoint.com/css/haslayout" rel="nofollow">see this article</a>.</p>

### Padding & Margins in IE 6/7

In most browsers, in order to remove the bullets or numbers from a list and push the list flush to the left, the left padding needs to be set to zero. But this has no effect in IE6 and IE7. Instead, the left margin needs to be set to zero for this to be achieved in those browsers.

<figure><img title="padding-left set to zero in IE6 &amp; IE7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a16e3227-f945-41e0-9a38-f827a3b0bb13/padding-left.jpg" alt="padding-left set to zero in IE6 &amp; IE7" width="500" height="126" /></figure>

### Achieving Consistent List-Styling in all Browsers

To avoid the issues that arise in the handling of list styles in the different browsers, the best method is to <strong>use a CSS reset</strong>. A CSS reset will set virtually all default browser settings to the bare minimum, and will allow you to work from a common ground in all browsers. There will still be differences after certain styles are applied, but they will not be as difficult to deal with after a reset is put in place.

Also, as mentioned earlier, it is best to completely avoid using the <code>list-style-image</code> property, and to instead set a background on the <code>&lt;li&gt;</code> elements. This will provide a cross-browser, easy-to-maintain solution for achieving custom bullets on an unordered list.</p>

## Showcase of Trends, Examples, & Tutorials

Now that we've reviewed the basics of HTML lists, as well as some browser inconsistencies, let's look at a number of <strong>different examples and tutorials</strong> that display practical examples and uses for HTML lists.</p>

### Navigation Bars

By far the most common use for the unordered list is the navigation bar, whether vertical or horizontal. Ever since table-based layouts became obsolete, the unordered list has been widely implemented as a basis for navigation elements for a number of reasons, listed below.

*   An unordered list is a block-level element, and so does not need to be wrapped in an extra `<div>` to apply a background or other graphical enhancement
*   When styles are disabled, a styled list will degrade gracefully, ensuring the navigation items appear distinct from the rest of the page's content
*   Although an unordered list might add more markup than just a plain list of `<a>` tags, having the extra `<li>` elements allows the navigation bar to be graphically flexible
*   Navigation divided into lists and/or sub-lists allows users with assistive technology (such as screen readers) to easily skip entire navigation sections

<a href="https://www.jampmark.com/html+css-techniques/pure-css-fish-eye-menu.html" rel="nofollow">Pure CSS Fish Eye Menu</a>
This vertical navigation menu that mimics the Apple "fisheye" effect on rollover is done with pure CSS and utilizes an unordered list to display the icons.

<figure><a href="https://www.jampmark.com/html+css-techniques/pure-css-fish-eye-menu.html" rel="nofollow"><img title="Pure CSS Fish Eye Menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54cb68be-8497-4c80-aa53-6b30932a9010/fisheye.jpg" alt="Pure CSS Fish Eye Menu" width="500" height="150" /></a></figure>

<a href="https://www.fiftyfoureleven.com/weblog/web-development/css/doors-meet-sprites" rel="nofollow">Sliding Doors Meets CSS Sprites</a>
An HTML list can also provide the foundation for a tabbed navigation bar using the famous <a href="https://www.alistapart.com/articles/slidingdoors/" rel="nofollow">sliding doors</a> technique, as demonstrated in this example.

<figure><a href="https://www.fiftyfoureleven.com/weblog/web-development/css/doors-meet-sprites" rel="nofollow"><img title="Sliding Doors Meets CSS Sprites" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f407484-087f-40d7-bb4f-96b56b5b4545/tabbed-nav.jpg" alt="Sliding Doors Meets CSS Sprites" width="500" height="271" /></a></figure>

<a href="https://www.gmarwaha.com/blog/2007/08/23/lavalamp-for-jquery-lovers/" rel="nofollow">LavaLamp for jQuery Lovers</a>
A "Lava Lamp" hover animation effect on a list-based navigation bar, written for jQuery.

<figure><a href="https://www.gmarwaha.com/blog/2007/08/23/lavalamp-for-jquery-lovers/" rel="nofollow"><img title="LavaLamp for jQuery Lovers" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a65325-3eed-4176-80af-c6bff55ac071/lavalamp.jpg" alt="LavaLamp for jQuery Lovers" width="500" height="208" /></a></figure>

<a href="https://webmuch.com/animated-navigation-bar-using-jquery/" rel="nofollow">Animated Navigation Bar Using jQuery</a>
This tutorial on WebMunch uses list-based navigation to create an animated navigation bar powered by jQuery. The demo page displays four different variations of the animated effect.

<figure><a href="https://webmuch.com/animated-navigation-bar-using-jquery/" rel="nofollow"><img title="Animated Navigation Bar Using jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50dac7c3-3510-40d3-9c1e-d03165df11fb/animated-bar.jpg" alt="Animated Navigation Bar Using jQuery" width="500" height="400" /></a></figure>

Apple's Navigation bar using only CSS
This tutorial describes how to recreate Apple's navigation bar, based on a list, with some CSS3 enhancements that degrade gracefully in IE and older browsers. The final result also includes an animated hover effect that works in Safari.

<figure><img title="Apple's Navigation bar using only CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2164091f-0d52-43a2-81c2-c816f8b5c992/apple.jpg" alt="Apple's Navigation bar using only CSS" width="500" height="61" /></figure>

### Drop-Down Menus

Older drop-down menus, like Brainjar's <a href="https://www.brainjar.com/dhtml/menubar/" rel="nofollow">Revenge of the Menu Bar</a> used <code>&lt;div&gt;</code> elements to divide sections of anchor tags, implementing JavaScript to show and hide menus. Later, drop-down menus were developed that were more semantic, and more dependent on CSS.

<a href="https://www.alistapart.com/articles/dropdowns" rel="nofollow">Suckerfish Dropdowns</a>
The classic Suckerfish dropdowns by Patrick Griffiths and Dan Webb were one of the earliest drop-down (or fly-out) menus to be based on nested lists.

<figure><a href="https://www.alistapart.com/articles/dropdowns" rel="nofollow"><img title="Suckerfish Dropdowns" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f830f952-1aa1-4de7-9a49-39328da14b9b/suckerfish.jpg" alt="Suckerfish Dropdowns" width="500" height="317" /></a></figure>

<a href="https://www.stunicholls.com/menu/pro_dropdown_2.html" rel="nofollow">Professional Drop-Down</a>
Stu Nicholls provides another list-based solution for drop-downs.

<figure><a href="https://www.stunicholls.com/menu/pro_dropdown_2.html" rel="nofollow"><img title="Professional Drop-Down by Stu Nicholls" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9b9981a-6f24-4a5b-a038-b39416e2c89b/dropdowns.jpg" alt="Professional Drop-Down by Stu Nicholls" width="500" height="289" /></a></figure>

Animated Drop Down Menu with jQuery
This tutorial demonstrates how to create a simple, single animated drop-down menu based on an unordered list, with jQuery.

<figure><img title="Animated Drop Down Menu with jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/244f6289-eead-48bd-9530-fbd9bc98e614/dropdown-animated.jpg" alt="Animated Drop Down Menu with jQuery" width="500" height="302" /></figure>

<a href="https://www.jankoatwarpspeed.com/post/2009/06/20/Create-dropdown-menus-with-CSS-only.aspx" rel="nofollow">Create Dropdown Menus with CSS Only</a>
This simple technique creates list-based drop-down menus without JavaScript.

<figure><a href="https://www.jankoatwarpspeed.com/post/2009/06/20/Create-dropdown-menus-with-CSS-only.aspx" rel="nofollow"><img title="Create Dropdown Menus with CSS Only" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf1b11ba-b016-44b5-b1e2-4c73beee12d8/css-dropdowns.jpg" alt="Create Dropdown Menus with CSS Only" width="500" height="231" /></a></figure>

<a href="https://sandbox.scriptiny.com/sorter/" rel="nofollow">JavaScript Dropdown Menu with Multi Levels</a>
These multi-level, cross-browser, list-based drop-down menus include an animated slide and fade effect.

<figure><a href="https://sandbox.scriptiny.com/sorter/" rel="nofollow"><img title="JavaScript Dropdown Menu with Multi Levels" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6fd7402-cdef-455a-b677-29ad9358b5c4/multi-fade.jpg" alt="JavaScript Dropdown Menu with Multi Levels" width="500" height="278" /></a></figure>

### Photo Displays

HTML lists serve as an effective way to <strong>display a list of photos</strong>, for many of the same reasons that were mentioned above for navigation bars. Below are some examples of photo galleries and other photo-based widgets that are styled with HTML lists.

<a href="https://sorgalla.com/jcarousel/" rel="nofollow">jCarousel</a>
The jCarousel photo carousel jQuery plugin applies customizable jQuery functionality to an unordered list that can display the carousel in a number of different ways.

<figure><a href="https://sorgalla.com/jcarousel/" rel="nofollow"><img title="jCarousel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e893ebb-47ff-48ba-a364-9f6c98763b21/jcarousel.jpg" alt="jCarousel" width="500" height="305" /></a></figure>

<a href="https://medienfreunde.com/lab/innerfade/" rel="nofollow">InnerFade with JQuery</a>
This plugin allows an unordered list of images to serve as the basis for a fading image rotator that displays one image at a time. The screen grab below displays two of the images in mid-transition.

<figure><a href="https://medienfreunde.com/lab/innerfade/" rel="nofollow"><img title="InnerFade with JQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f4b349d-3201-4ff9-a381-cda9835b7b00/innerfade.jpg" alt="InnerFade with JQuery" width="500" height="355" /></a></figure>

CSS Photo Gallery Template
This is a free photo gallery template that displays a caption on hover. This simple gallery uses an unordered list with <strong>floated list items</strong>.

<figure><img title="CSS Photo Gallery Template" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cb55d36-7d32-4c50-9951-0c7e2001386c/gallery.jpg" alt="CSS Photo Gallery Template" width="500" height="349" /></figure>

Definition Lists for Image Gallery
This demonstration on Max Design shows how to transform a definition list into an image gallery.

<figure><img title="Definition Lists for Image Gallery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f51a8d9-83a3-4aeb-bac9-e35fe674f0b6/def-photos.jpg" alt="Definition Lists for Image Gallery" width="500" height="207" /></figure>

### Styling and Dividing Other Types of Content

In addition to displaying images, lists also come in handy for display of content in sometimes atypical fashion, as demonstrated by the examples below.

<a href="https://www.alistapart.com/articles/multicolumnlists/" rel="nofollow">Multi-Column Lists</a>
A few years back, A List Apart demonstrated how to convert a single unordered list into a <strong>multi-columned display</strong>, without the need to divide the items into multiple lists.

<figure><a href="https://www.alistapart.com/articles/multicolumnlists/" rel="nofollow"><img title="Multi-Column Lists" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e09a9e56-87a3-4d30-8e3b-46dd1bf7a64f/multicolumn.jpg" alt="Multi-Column Lists" width="500" height="256" /></a></figure>

<a href="https://css-tricks.com/style-a-list-with-one-pixel/" rel="nofollow">Style a List with One Pixel</a>
Chris Coyier demonstrates a neat CSS trick -- how to create a "depth-chart looking unordered list" using just a 1-pixel GIF.

<figure><a href="https://css-tricks.com/style-a-list-with-one-pixel/" rel="nofollow"><img title="Style a List with One Pixel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b70e0349-4412-401e-82cf-c618654ff2e6/1pixel.jpg" alt="Style a List with One Pixel" width="500" height="298" /></a></figure>

Accessible HTML Forms using Definition Lists
Andrew Sellick steps through the styling of a lengthy form with the help of <strong>definition lists</strong> to group sets of text boxes, radio buttons, and checkboxes.

<figure><img title="Accessible HTML Forms using Definition Lists" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/514e496c-af65-4379-a6e9-942aaa6cd6e2/form-def.jpg" alt="Accessible HTML Forms using Definition Lists" width="500" height="305" /></figure>

<a href="https://www.drunkenfist.com/304/2007/11/29/a-three-column-css-layout-using-just-an-unordered-list/" rel="nofollow">A Three Column CSS Layout Using Just an Unordered List</a>
Rob Larsen of DrunkenFist.com demonstrates how to create a <strong>3-column page layout</strong> using an unordered list in place of the usual <code>&lt;div&gt;</code> elements.

<figure><a href="https://www.drunkenfist.com/304/2007/11/29/a-three-column-css-layout-using-just-an-unordered-list/" rel="nofollow"><img title="A Three Column CSS Layout Using Just an Unordered List" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edbe5fd1-524d-4da4-b2e2-d91e78552db9/ul-layout.jpg" alt="A Three Column CSS Layout Using Just an Unordered List" width="500" height="247" /></a></figure>

<span class="removed_link" title="https://www.gayadesign.com/diy/animated-tabbed-content-with-jquery/">Animated Tabbed Content with jQuery</span>
This tutorial on Gaya Design demonstrates how to create an animated tabbed content box with jQuery. The content is structured using unordered lists.

<figure><span class="removed_link" title="https://www.gayadesign.com/diy/animated-tabbed-content-with-jquery/"><img title="Animated Tabbed Content with jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6e56fc3-d8aa-4381-90a3-1ae566c6c2be/tabbed-content.jpg" alt="Animated Tabbed Content with jQuery" width="500" height="436" /></span></figure>

<a href="https://www.queness.com/post/741/a-simple-and-beautiful-jquery-accordion-tutorial" rel="nofollow">A Simple and Beautiful jQuery Accordion Tutorial</a>
This is a simple tutorial that uses nested unordered lists as a basis for a jQuery animated accordion menu.

<figure><a href="https://www.queness.com/post/741/a-simple-and-beautiful-jquery-accordion-tutorial" rel="nofollow"><img title="A Simple and Beautiful jQuery Accordion Tutorial" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e5e6430-5150-4fee-9df4-2e2b9178fd01/accordion.jpg" alt="A Simple and Beautiful jQuery Accordion Tutorial" width="500" height="244" /></a></figure>

### Code Highlighters

Many blogs and tutorial sites include JavaScript-driven code highlighters that convert <code>&lt;pre&gt;</code> elements into ordered lists, as shown in the screen capture below. One such code highlighter is <a href="https://code.google.com/p/syntaxhighlighter/" rel="nofollow">Alex Gorbatchev's SyntaxHighlighter</a>

<figure><a href="https://code.google.com/p/syntaxhighlighter/" rel="nofollow"><img title="Code Highlighter" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97f3d169-940d-412e-b2d8-8a2fd5092265/code-hilite.jpg" alt="Code Highlighter" width="500" height="344" /></a></figure>

### Blog Comments

Blog comments, including those on WordPress-driven sites, are structured with ordered lists, providing very flexible options for styling, and laying a foundation for nested comments. Nested, or "threaded" comments are now built into WordPress.</p>

### Fancy Styles and Techniques with Lists

jQuery Sortable Lists With Drag Drop Handle
Will Linssen demonstrates, with jQuery, how to create an ordered or unordered list that allows the user to manually sort the list items.

<figure><img title="jQuery Sortable Lists With Drag Drop Handle" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94ba860c-c0ad-493f-b9bf-bed0f478fdd6/drag-drop.jpg" alt="jQuery Sortable Lists With Drag Drop Handle" width="500" height="285" /></figure>

Sexy Ordered Lists with CSS
Soh Tanaka shows users how to add some fancy styling to an ordered list.

<figure><img title="Sexy Ordered Lists with CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fce80638-0e49-42f7-ac14-049d29a1dae4/soh-lists.jpg" alt="Sexy Ordered Lists with CSS" width="500" height="472" /></figure>

<a href="https://veerle.duoh.com/" rel="nofollow">Veerle's Block Hover Effect on List Items</a>
In the "Approved" section in the footer of her home page, Veerle Pieters implements a cross-browser block-hover effect on an unordered list. Each list item contains a number of separate elements, but the hover effect works on the entire list item, and even works in IE6. The same effect is discussed in tutorials on <a href="https://www.smileycat.com/miaow/archives/000230.php" rel="nofollow">Smiley Cat</a> and <a href="https://randsco.com/index.php/2009/05/21/beautify_a_resource_list" rel="nofollow">randsco.com</a>.

<figure><a href="https://veerle.duoh.com/" rel="nofollow"><img title="Veerle's Block Hover Effect on List Items" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf0d944-b669-41c7-a022-6203fa9dbdb0/veerle-list.jpg" alt="Veerle's Block Hover Effect on List Items" width="500" height="472" /></a></figure>

<a href="https://www.cssplay.co.uk/menu/barchart.html" rel="nofollow">A Definition List Bar Chart</a>
The ever-creative Stu Nicholls shows us how to display a bar chart (with very old browser stats!) with a styled definition list.

<figure><a href="https://www.cssplay.co.uk/menu/barchart.html" rel="nofollow"><img title="A Definition List Bar Chart" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e5ed87e-550e-4ee1-bfba-ac49e6995651/bar-chart.jpg" alt="A Definition List Bar Charts" width="500" height="201" /></a></figure>

<a href="https://www.webdesignerwall.com/tutorials/jquery-sequential-list/" rel="nofollow">jQuery Sequential List</a>
This tutorial on Web Designer Wall will show you how to use jQuery to add sequential CSS classes to list items to create a graphical list.

<figure><a href="https://www.webdesignerwall.com/tutorials/jquery-sequential-list/" rel="nofollow"><img title="jQuery Sequential List" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d5c1b4b-1839-44d8-9d61-642dc3884ded/sequential.jpg" alt="jQuery Sequential List" width="500" height="437" /></a></figure>

<span class="removed_link" title="https://www.stevenyork.com/tutorial/creating_accessible_tag_cloud_in_php_css_mysql">Creating an Accessible Tag Cloud in PHP and CSS</span>
This tutorial describes how to create an accessible, standards compliant tag cloud with simple code. The resulting HTML output is a simple unordered list.

<figure><span class="removed_link" title="https://www.stevenyork.com/tutorial/creating_accessible_tag_cloud_in_php_css_mysql"><img title="Creating an Accessible Tag Cloud in PHP and CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54f5aaaf-e802-4484-898c-3b7bf3d7e87f/tagcloud.jpg" alt="Creating an Accessible Tag Cloud in PHP and CSS" width="500" height="143" /></span></figure>

<a href="https://veerle.duoh.com/blog/comments/simple_scalable_css_based_breadcrumbs" rel="nofollow">Simple Scalable CSS Based Breadcrumbs</a>
Veerle Pieters describes how to create a breadcrumb navigation section using an unordered list.

<figure><a href="https://veerle.duoh.com/blog/comments/simple_scalable_css_based_breadcrumbs" rel="nofollow"><img title="Simple Scalable CSS Based Breadcrumbs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdcdc50a-44c7-484d-984e-9001df69e5f9/breadcrumbs.jpg" alt="Simple Scalable CSS Based Breadcrumbs" width="500" height="295" /></a></figure>

<a href="https://codylindley.com/CSS/325/css-step-menu" rel="nofollow">CSS Step Menu</a>
A demonstration of a "step menu" that's based on unordered lists.

<figure><a href="https://codylindley.com/CSS/325/css-step-menu" rel="nofollow"><img title="CSS Step Menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c8f96b0-0778-4ff7-b273-d7f6d5a78955/stepmenu.jpg" alt="CSS Step Menu" width="500" height="442" /></a></figure>

Overlap That Menu!
A tutorial that describes how to create overlapping menu items using a styled unordered list.

<figure><span class="removed_link" title="https://www.cssbake.com/cookbook/overlap-that-menu/"><img title="Overlap That Menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03a72801-2625-4cf4-b17b-6d7b779139d4/overlap.jpg" alt="Overlap That Menu" width="500" height="290" /></span></figure>

In most browsers, in order to remove the bullets or numbers from a list and push the list flush to the left, the left padding needs to be set to zero. But this has no effect in IE6 and IE7. Instead, the left margin needs to be set to zero for this to be achieved in those browsers.

<figure><img title="padding-left set to zero in IE6 &amp; IE7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a16e3227-f945-41e0-9a38-f827a3b0bb13/padding-left.jpg" alt="padding-left set to zero in IE6 &amp; IE7" width="500" height="126" /></figure>

### Achieving Consistent List-Styling in all Browsers

To avoid the issues that arise in the handling of list styles in the different browsers, the best method is to <strong>use a CSS reset</strong>. A CSS reset will set virtually all default browser settings to the bare minimum, and will allow you to work from a common ground in all browsers. There will still be differences after certain styles are applied, but they will not be as difficult to deal with after a reset is put in place.

Also, as mentioned earlier, it is best to completely avoid using the <code>list-style-image</code> property, and to instead set a background on the <code>&lt;li&gt;</code> elements. This will provide a cross-browser, easy-to-maintain solution for achieving custom bullets on an unordered list.</p>

## Showcase of Trends, Examples, & Tutorials

Now that we've reviewed the basics of HTML lists, as well as some browser inconsistencies, let's look at a number of <strong>different examples and tutorials</strong> that display practical examples and uses for HTML lists.</p>

### Navigation Bars

By far the most common use for the unordered list is the navigation bar, whether vertical or horizontal. Ever since table-based layouts became obsolete, the unordered list has been widely implemented as a basis for navigation elements for a number of reasons, listed below.

*   An unordered list is a block-level element, and so does not need to be wrapped in an extra `<div>` to apply a background or other graphical enhancement
*   When styles are disabled, a styled list will degrade gracefully, ensuring the navigation items appear distinct from the rest of the page's content
*   Although an unordered list might add more markup than just a plain list of `<a>` tags, having the extra `<li>` elements allows the navigation bar to be graphically flexible
*   Navigation divided into lists and/or sub-lists allows users with assistive technology (such as screen readers) to easily skip entire navigation sections

<a href="https://www.jampmark.com/html+css-techniques/pure-css-fish-eye-menu.html" rel="nofollow">Pure CSS Fish Eye Menu</a>
This vertical navigation menu that mimics the Apple "fisheye" effect on rollover is done with pure CSS and utilizes an unordered list to display the icons.

<figure><a href="https://www.jampmark.com/html+css-techniques/pure-css-fish-eye-menu.html" rel="nofollow"><img title="Pure CSS Fish Eye Menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54cb68be-8497-4c80-aa53-6b30932a9010/fisheye.jpg" alt="Pure CSS Fish Eye Menu" width="500" height="150" /></a></figure>

<a href="https://www.fiftyfoureleven.com/weblog/web-development/css/doors-meet-sprites" rel="nofollow">Sliding Doors Meets CSS Sprites</a>
An HTML list can also provide the foundation for a tabbed navigation bar using the famous <a href="https://www.alistapart.com/articles/slidingdoors/" rel="nofollow">sliding doors</a> technique, as demonstrated in this example.

<figure><a href="https://www.fiftyfoureleven.com/weblog/web-development/css/doors-meet-sprites" rel="nofollow"><img title="Sliding Doors Meets CSS Sprites" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f407484-087f-40d7-bb4f-96b56b5b4545/tabbed-nav.jpg" alt="Sliding Doors Meets CSS Sprites" width="500" height="271" /></a></figure>

<a href="https://www.gmarwaha.com/blog/2007/08/23/lavalamp-for-jquery-lovers/" rel="nofollow">LavaLamp for jQuery Lovers</a>
A "Lava Lamp" hover animation effect on a list-based navigation bar, written for jQuery.

<figure><a href="https://www.gmarwaha.com/blog/2007/08/23/lavalamp-for-jquery-lovers/" rel="nofollow"><img title="LavaLamp for jQuery Lovers" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02a65325-3eed-4176-80af-c6bff55ac071/lavalamp.jpg" alt="LavaLamp for jQuery Lovers" width="500" height="208" /></a></figure>

<a href="https://webmuch.com/animated-navigation-bar-using-jquery/" rel="nofollow">Animated Navigation Bar Using jQuery</a>
This tutorial on WebMunch uses list-based navigation to create an animated navigation bar powered by jQuery. The demo page displays four different variations of the animated effect.

<figure><a href="https://webmuch.com/animated-navigation-bar-using-jquery/" rel="nofollow"><img title="Animated Navigation Bar Using jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50dac7c3-3510-40d3-9c1e-d03165df11fb/animated-bar.jpg" alt="Animated Navigation Bar Using jQuery" width="500" height="400" /></a></figure>

Apple's Navigation bar using only CSS
This tutorial describes how to recreate Apple's navigation bar, based on a list, with some CSS3 enhancements that degrade gracefully in IE and older browsers. The final result also includes an animated hover effect that works in Safari.

<figure><img title="Apple's Navigation bar using only CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2164091f-0d52-43a2-81c2-c816f8b5c992/apple.jpg" alt="Apple's Navigation bar using only CSS" width="500" height="61" /></figure>

### Drop-Down Menus

Older drop-down menus, like Brainjar's <a href="https://www.brainjar.com/dhtml/menubar/" rel="nofollow">Revenge of the Menu Bar</a> used <code>&lt;div&gt;</code> elements to divide sections of anchor tags, implementing JavaScript to show and hide menus. Later, drop-down menus were developed that were more semantic, and more dependent on CSS.

<a href="https://www.alistapart.com/articles/dropdowns" rel="nofollow">Suckerfish Dropdowns</a>
The classic Suckerfish dropdowns by Patrick Griffiths and Dan Webb were one of the earliest drop-down (or fly-out) menus to be based on nested lists.

<figure><a href="https://www.alistapart.com/articles/dropdowns" rel="nofollow"><img title="Suckerfish Dropdowns" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f830f952-1aa1-4de7-9a49-39328da14b9b/suckerfish.jpg" alt="Suckerfish Dropdowns" width="500" height="317" /></a></figure>

<a href="https://www.stunicholls.com/menu/pro_dropdown_2.html" rel="nofollow">Professional Drop-Down</a>
Stu Nicholls provides another list-based solution for drop-downs.

<figure><a href="https://www.stunicholls.com/menu/pro_dropdown_2.html" rel="nofollow"><img title="Professional Drop-Down by Stu Nicholls" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9b9981a-6f24-4a5b-a038-b39416e2c89b/dropdowns.jpg" alt="Professional Drop-Down by Stu Nicholls" width="500" height="289" /></a></figure>

Animated Drop Down Menu with jQuery
This tutorial demonstrates how to create a simple, single animated drop-down menu based on an unordered list, with jQuery.

<figure><img title="Animated Drop Down Menu with jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/244f6289-eead-48bd-9530-fbd9bc98e614/dropdown-animated.jpg" alt="Animated Drop Down Menu with jQuery" width="500" height="302" /></figure>

<a href="https://www.jankoatwarpspeed.com/post/2009/06/20/Create-dropdown-menus-with-CSS-only.aspx" rel="nofollow">Create Dropdown Menus with CSS Only</a>
This simple technique creates list-based drop-down menus without JavaScript.

<figure><a href="https://www.jankoatwarpspeed.com/post/2009/06/20/Create-dropdown-menus-with-CSS-only.aspx" rel="nofollow"><img title="Create Dropdown Menus with CSS Only" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf1b11ba-b016-44b5-b1e2-4c73beee12d8/css-dropdowns.jpg" alt="Create Dropdown Menus with CSS Only" width="500" height="231" /></a></figure>

<a href="https://sandbox.scriptiny.com/sorter/" rel="nofollow">JavaScript Dropdown Menu with Multi Levels</a>
These multi-level, cross-browser, list-based drop-down menus include an animated slide and fade effect.

<figure><a href="https://sandbox.scriptiny.com/sorter/" rel="nofollow"><img title="JavaScript Dropdown Menu with Multi Levels" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6fd7402-cdef-455a-b677-29ad9358b5c4/multi-fade.jpg" alt="JavaScript Dropdown Menu with Multi Levels" width="500" height="278" /></a></figure>

### Photo Displays

HTML lists serve as an effective way to <strong>display a list of photos</strong>, for many of the same reasons that were mentioned above for navigation bars. Below are some examples of photo galleries and other photo-based widgets that are styled with HTML lists.

<a href="https://sorgalla.com/jcarousel/" rel="nofollow">jCarousel</a>
The jCarousel photo carousel jQuery plugin applies customizable jQuery functionality to an unordered list that can display the carousel in a number of different ways.

<figure><a href="https://sorgalla.com/jcarousel/" rel="nofollow"><img title="jCarousel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e893ebb-47ff-48ba-a364-9f6c98763b21/jcarousel.jpg" alt="jCarousel" width="500" height="305" /></a></figure>

<a href="https://medienfreunde.com/lab/innerfade/" rel="nofollow">InnerFade with JQuery</a>
This plugin allows an unordered list of images to serve as the basis for a fading image rotator that displays one image at a time. The screen grab below displays two of the images in mid-transition.

<figure><a href="https://medienfreunde.com/lab/innerfade/" rel="nofollow"><img title="InnerFade with JQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f4b349d-3201-4ff9-a381-cda9835b7b00/innerfade.jpg" alt="InnerFade with JQuery" width="500" height="355" /></a></figure>

CSS Photo Gallery Template
This is a free photo gallery template that displays a caption on hover. This simple gallery uses an unordered list with <strong>floated list items</strong>.

<figure><img title="CSS Photo Gallery Template" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cb55d36-7d32-4c50-9951-0c7e2001386c/gallery.jpg" alt="CSS Photo Gallery Template" width="500" height="349" /></figure>

Definition Lists for Image Gallery
This demonstration on Max Design shows how to transform a definition list into an image gallery.

<figure><img title="Definition Lists for Image Gallery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f51a8d9-83a3-4aeb-bac9-e35fe674f0b6/def-photos.jpg" alt="Definition Lists for Image Gallery" width="500" height="207" /></figure>

### Styling and Dividing Other Types of Content

In addition to displaying images, lists also come in handy for display of content in sometimes atypical fashion, as demonstrated by the examples below.

<a href="https://www.alistapart.com/articles/multicolumnlists/" rel="nofollow">Multi-Column Lists</a>
A few years back, A List Apart demonstrated how to convert a single unordered list into a <strong>multi-columned display</strong>, without the need to divide the items into multiple lists.

<figure><a href="https://www.alistapart.com/articles/multicolumnlists/" rel="nofollow"><img title="Multi-Column Lists" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e09a9e56-87a3-4d30-8e3b-46dd1bf7a64f/multicolumn.jpg" alt="Multi-Column Lists" width="500" height="256" /></a></figure>

<a href="https://css-tricks.com/style-a-list-with-one-pixel/" rel="nofollow">Style a List with One Pixel</a>
Chris Coyier demonstrates a neat CSS trick -- how to create a "depth-chart looking unordered list" using just a 1-pixel GIF.

<figure><a href="https://css-tricks.com/style-a-list-with-one-pixel/" rel="nofollow"><img title="Style a List with One Pixel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b70e0349-4412-401e-82cf-c618654ff2e6/1pixel.jpg" alt="Style a List with One Pixel" width="500" height="298" /></a></figure>

Accessible HTML Forms using Definition Lists
Andrew Sellick steps through the styling of a lengthy form with the help of <strong>definition lists</strong> to group sets of text boxes, radio buttons, and checkboxes.

<figure><img title="Accessible HTML Forms using Definition Lists" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/514e496c-af65-4379-a6e9-942aaa6cd6e2/form-def.jpg" alt="Accessible HTML Forms using Definition Lists" width="500" height="305" /></figure>

<a href="https://www.drunkenfist.com/304/2007/11/29/a-three-column-css-layout-using-just-an-unordered-list/" rel="nofollow">A Three Column CSS Layout Using Just an Unordered List</a>
Rob Larsen of DrunkenFist.com demonstrates how to create a <strong>3-column page layout</strong> using an unordered list in place of the usual <code>&lt;div&gt;</code> elements.

<figure><a href="https://www.drunkenfist.com/304/2007/11/29/a-three-column-css-layout-using-just-an-unordered-list/" rel="nofollow"><img title="A Three Column CSS Layout Using Just an Unordered List" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edbe5fd1-524d-4da4-b2e2-d91e78552db9/ul-layout.jpg" alt="A Three Column CSS Layout Using Just an Unordered List" width="500" height="247" /></a></figure>

<span class="removed_link" title="https://www.gayadesign.com/diy/animated-tabbed-content-with-jquery/">Animated Tabbed Content with jQuery</span>
This tutorial on Gaya Design demonstrates how to create an animated tabbed content box with jQuery. The content is structured using unordered lists.

<figure><span class="removed_link" title="https://www.gayadesign.com/diy/animated-tabbed-content-with-jquery/"><img title="Animated Tabbed Content with jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6e56fc3-d8aa-4381-90a3-1ae566c6c2be/tabbed-content.jpg" alt="Animated Tabbed Content with jQuery" width="500" height="436" /></span></figure>

<a href="https://www.queness.com/post/741/a-simple-and-beautiful-jquery-accordion-tutorial" rel="nofollow">A Simple and Beautiful jQuery Accordion Tutorial</a>
This is a simple tutorial that uses nested unordered lists as a basis for a jQuery animated accordion menu.

<figure><a href="https://www.queness.com/post/741/a-simple-and-beautiful-jquery-accordion-tutorial" rel="nofollow"><img title="A Simple and Beautiful jQuery Accordion Tutorial" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e5e6430-5150-4fee-9df4-2e2b9178fd01/accordion.jpg" alt="A Simple and Beautiful jQuery Accordion Tutorial" width="500" height="244" /></a></figure>

### Code Highlighters

Many blogs and tutorial sites include JavaScript-driven code highlighters that convert <code>&lt;pre&gt;</code> elements into ordered lists, as shown in the screen capture below. One such code highlighter is <a href="https://code.google.com/p/syntaxhighlighter/" rel="nofollow">Alex Gorbatchev's SyntaxHighlighter</a>

<figure><a href="https://code.google.com/p/syntaxhighlighter/" rel="nofollow"><img title="Code Highlighter" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97f3d169-940d-412e-b2d8-8a2fd5092265/code-hilite.jpg" alt="Code Highlighter" width="500" height="344" /></a></figure>

### Blog Comments

Blog comments, including those on WordPress-driven sites, are structured with ordered lists, providing very flexible options for styling, and laying a foundation for nested comments. Nested, or "threaded" comments are now built into WordPress.</p>

### Fancy Styles and Techniques with Lists

jQuery Sortable Lists With Drag Drop Handle
Will Linssen demonstrates, with jQuery, how to create an ordered or unordered list that allows the user to manually sort the list items.

<figure><img title="jQuery Sortable Lists With Drag Drop Handle" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94ba860c-c0ad-493f-b9bf-bed0f478fdd6/drag-drop.jpg" alt="jQuery Sortable Lists With Drag Drop Handle" width="500" height="285" /></figure>

Sexy Ordered Lists with CSS
Soh Tanaka shows users how to add some fancy styling to an ordered list.

<figure><img title="Sexy Ordered Lists with CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fce80638-0e49-42f7-ac14-049d29a1dae4/soh-lists.jpg" alt="Sexy Ordered Lists with CSS" width="500" height="472" /></figure>

<a href="https://veerle.duoh.com/" rel="nofollow">Veerle's Block Hover Effect on List Items</a>
In the "Approved" section in the footer of her home page, Veerle Pieters implements a cross-browser block-hover effect on an unordered list. Each list item contains a number of separate elements, but the hover effect works on the entire list item, and even works in IE6. The same effect is discussed in tutorials on <a href="https://www.smileycat.com/miaow/archives/000230.php" rel="nofollow">Smiley Cat</a> and <a href="https://randsco.com/index.php/2009/05/21/beautify_a_resource_list" rel="nofollow">randsco.com</a>.

<figure><a href="https://veerle.duoh.com/" rel="nofollow"><img title="Veerle's Block Hover Effect on List Items" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3bf0d944-b669-41c7-a022-6203fa9dbdb0/veerle-list.jpg" alt="Veerle's Block Hover Effect on List Items" width="500" height="472" /></a></figure>

<a href="https://www.cssplay.co.uk/menu/barchart.html" rel="nofollow">A Definition List Bar Chart</a>
The ever-creative Stu Nicholls shows us how to display a bar chart (with very old browser stats!) with a styled definition list.

<figure><a href="https://www.cssplay.co.uk/menu/barchart.html" rel="nofollow"><img title="A Definition List Bar Chart" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e5ed87e-550e-4ee1-bfba-ac49e6995651/bar-chart.jpg" alt="A Definition List Bar Charts" width="500" height="201" /></a></figure>

<a href="https://www.webdesignerwall.com/tutorials/jquery-sequential-list/" rel="nofollow">jQuery Sequential List</a>
This tutorial on Web Designer Wall will show you how to use jQuery to add sequential CSS classes to list items to create a graphical list.

<figure><a href="https://www.webdesignerwall.com/tutorials/jquery-sequential-list/" rel="nofollow"><img title="jQuery Sequential List" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d5c1b4b-1839-44d8-9d61-642dc3884ded/sequential.jpg" alt="jQuery Sequential List" width="500" height="437" /></a></figure>

<span class="removed_link" title="https://www.stevenyork.com/tutorial/creating_accessible_tag_cloud_in_php_css_mysql">Creating an Accessible Tag Cloud in PHP and CSS</span>
This tutorial describes how to create an accessible, standards compliant tag cloud with simple code. The resulting HTML output is a simple unordered list.

<figure><span class="removed_link" title="https://www.stevenyork.com/tutorial/creating_accessible_tag_cloud_in_php_css_mysql"><img title="Creating an Accessible Tag Cloud in PHP and CSS" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54f5aaaf-e802-4484-898c-3b7bf3d7e87f/tagcloud.jpg" alt="Creating an Accessible Tag Cloud in PHP and CSS" width="500" height="143" /></span></figure>

<a href="https://veerle.duoh.com/blog/comments/simple_scalable_css_based_breadcrumbs" rel="nofollow">Simple Scalable CSS Based Breadcrumbs</a>
Veerle Pieters describes how to create a breadcrumb navigation section using an unordered list.

<figure><a href="https://veerle.duoh.com/blog/comments/simple_scalable_css_based_breadcrumbs" rel="nofollow"><img title="Simple Scalable CSS Based Breadcrumbs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdcdc50a-44c7-484d-984e-9001df69e5f9/breadcrumbs.jpg" alt="Simple Scalable CSS Based Breadcrumbs" width="500" height="295" /></a></figure>

<a href="https://codylindley.com/CSS/325/css-step-menu" rel="nofollow">CSS Step Menu</a>
A demonstration of a "step menu" that's based on unordered lists.

<figure><a href="https://codylindley.com/CSS/325/css-step-menu" rel="nofollow"><img title="CSS Step Menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c8f96b0-0778-4ff7-b273-d7f6d5a78955/stepmenu.jpg" alt="CSS Step Menu" width="500" height="442" /></a></figure>

Overlap That Menu!
A tutorial that describes how to create overlapping menu items using a styled unordered list.

<figure><span class="removed_link" title="https://www.cssbake.com/cookbook/overlap-that-menu/"><img title="Overlap That Menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03a72801-2625-4cf4-b17b-6d7b779139d4/overlap.jpg" alt="Overlap That Menu" width="500" height="290" /></span></figure>

<span class="removed_link" title="https://www.thewojogroup.com/2008/12/css-stacked-bar-graphs/">CSS Stacked Bar Graphs</span>
A fancy stacked bar graph in CSS that uses an unordered list and a definition list.

<figure><span class="removed_link" title="https://www.thewojogroup.com/2008/12/css-stacked-bar-graphs/"><img title="CSS Stacked Bar Graphs" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bec7f872-9d8b-47ed-8d5b-661565ce0395/bargraph.jpg" alt="CSS Stacked Bar Graphs" width="500" height="426" /></span></figure>

<a href="https://www.dynamicdrive.com/style/csslibrary/item/nested_side_bar_menu/" rel="nofollow">Nested Side Bar Menu</a>
Using the same principle as drop-down menus, this demonstration shows a cross-browser vertical menu with fly-outs, based on nested unordered lists.

<figure><a href="https://www.dynamicdrive.com/style/csslibrary/item/nested_side_bar_menu/" rel="nofollow"><img title="Nested Side Bar Menu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91a75dfe-edc8-4a3d-a707-7b927e3b33b0/flyouts.jpg" alt="Nested Side Bar Menu" width="500" height="231" /></a></figure>

<a href="https://www.ogilvydurham.com/allTags.php" rel="nofollow">OMG Durham's Tag Popularity Graph</a>
OMG Durham's website displays popular tags using a bar graph that is based on an unordered list.

<figure><a href="https://www.ogilvydurham.com/allTags.php" rel="nofollow"><img title="OMG Durham's Tag Popularity Graph" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/855893d0-8cd8-4995-9dde-d54a376b4cec/tag-graph.jpg" alt="OMG Durham's Tag Popularity Graph" width="500" height="141" /></a></figure>

## Conclusion

A beautiful, CSS-styled, cross-browser HTML list has the power to resolve thousands of potential layout or design challenges. Although dozens more uses and techniques could be discussed in this article, the above material should be enough to give a thorough overview of HTML lists, demonstrating how powerful and flexible they are in the hands of an experienced coder.</p>

## Further Resources

*   [The Listamatic](https://css.maxdesign.com.au/listamatic/)
*   [CSS Design: Taming Lists](https://www.alistapart.com/articles/taminglists/)
*   [Definition lists - misused or misunderstood?](https://www.maxdesign.com.au/presentation/definition/)
*   [List Elements on Sitepoint's HTML Reference](https://reference.sitepoint.com/html/elements-list)


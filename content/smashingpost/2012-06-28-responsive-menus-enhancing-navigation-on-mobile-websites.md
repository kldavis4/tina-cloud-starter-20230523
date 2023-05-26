---
title: 'Responsive Menus: Enhancing Navigation On Mobile Websites'
slug: responsive-menus-enhancing-navigation-on-mobile-websites
image: >-
  https://www.smashingmagazine.com/wordpress/2012/04/05/manage-events-like-pro-with-wordpress/attachment/events-planner-pro-time500/attachment/compassdesign-ipad/
date: 2012-06-28T13:32:32.000Z
author: rachel-mccollin-2
description: >-
  Most of us are pretty familiar with responsive Web design by now. Basically,
  it uses a combination of a fluid layout and media queries to alter the design
  and layout of a website to fit different screen sizes. There are other
  considerations, too. For example, a lot of work has been done on responsive
  images, ensuring not only that images fit in a small-screen layout, but that
  the files downloaded to mobile devices are smaller, too.
categories:
  - Mobile
  - CSS
  - Navigation
  - Responsive Design
---
Most of us are pretty familiar with responsive Web design by now. Basically, it uses a combination of a fluid layout and media queries to alter the design and layout of a website to fit different screen sizes. There are other considerations, too. For example, a lot of work has been done on responsive images, ensuring not only that images fit in a small-screen layout, but that the files downloaded to mobile devices are smaller, too.

But mobile design isn’t just about layout and speed: it’s also about user experience. In this article, we’ll focus on one aspect of the user experience — navigation menus — and detail a few approaches to making them work better on mobile devices.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Navigation On Complex Websites](https://www.smashingmagazine.com/2013/09/responsive-navigation-on-complex-websites/)
*   [<span class="headline">Sticky Menus Are Quicker To Navigate</span>](https://www.smashingmagazine.com/2012/09/sticky-menus-are-quicker-to-navigate/)
*   [<span class="headline">A Simple JavaScript Plugin For Responsive Navigation</span>](https://www.smashingmagazine.com/2013/04/javascript-plugin-for-responsive-navigation/)
*   [Progressive And Responsive Navigation](https://www.smashingmagazine.com/2012/02/progressive-and-responsive-navigation/)

## What Are Responsive Menus?

By responsive menus, we mean quite simply <strong>navigation menus whose presentation or behavior is altered on different devices and screen widths</strong>.There are various approaches to achieving this, whether by using CSS or other languages such as PHP. In this article, we’ll look at what can be done with CSS media queries.

{{% feature-panel %}}

There are a few ways in which a menu could change on different devices:

*   It could have different styling, fitting differently in the browser window, or possibly looking like a menu from an app.
*   It could have different content, with the links adapting to the device they’re being viewed on.
*   They could appear in a different location on the page or screen.</p>

## Why Use Responsive Menus?

For visitors using a small screen, the user experience requirements for navigation will be different.

The first and most obvious reason for this is the size of the screen itself; the navigation will need to fit in that space without dominating the page (unless you want it to). Another factor is that navigation on most mobile devices has to be tapped on. The thumb is larger and less precise than a computer mouse, so your navigation links might need to be larger. This holds true even on large tablets such as the iPad, whose screen size is comparable to that of a desktop monitor but is still being tapped with a finger rather than clicked with a mouse.

Responsive menus have a number of benefits:

*   **Design**The navigation is integral to the design, so it might not look right with a different layout. The simplest adjustment to a responsive menu would be just to enhance its appearance.
*   **Ergonomics**Navigation links on a mobile website need to be large and clear enough to be able to be used with “one thumb and one eye,” as Luke Wroblewski asserts in his book _Mobile First_. In its “[User Experience Guidelines](https://developer.apple.com/library/ios/#documentation/UserExperience/Conceptual/MobileHIG/UEBestPractices/UEBestPractices.html#//apple_ref/doc/uid/TP40006556-CH20-SW20),” Apple advises making anything tappable the size of a fingertip, which it defines as 44 points square, or approximately 57 pixels square. This is a lot bigger than a link in a text-based menu, which might be only 14 pixels high. Thus, the clickable area of a link on a mobile website should encompass not only the text but the area around the text, and ideally this would be apparent to the user.
*   **User experience**Users might interact with your menu differently on a mobile device. In addition to the content of the menu and the size of the links, consider how the position of the menu will affect user experience. For example, a user who has scrolled to the end of a long blog post will not be inclined to scroll all the way back up to interact with the menu. Some designers fix the menu at the top or bottom of the screen to get around this, or they move the navigation to the bottom of the page and add a “Menu” link to the top. Some designers partially hide the menu until the user taps on it, to reduce the amount of screen space that it takes up — particularly important with fixed-position menus, which will hide all of the content if you’re not careful!

## Some Approaches To Responsive Menus

So, those were some of the benefits of responsive menus. Obviously, <strong>they will vary according to the website’s content, layout and functionality</strong>. Your approach will also depend on the time and budget available; some of these approaches aren’t a quick fix and could take some time to get right. Let’s look at some approaches that can make navigation work better on small screens, working our way from the quickest and simplest up to the most complex.</p>

### 1. Adjusting the Visual Design of the Menu

We could first do simple design tweaks to make the menu look better on narrower screens, focusing on landscape and portrait modes (i.e. screens narrower than 480 pixels).

The screenshot below is of the desktop design for <a href="https://121interviewcoaching.co.uk/">One to One Interview Coaching</a>, which has fairly simple one-level navigation.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea92c09d-eadc-4de7-9c90-83b04125bd05/121interviewcoaching-desktop.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111931" title="121interviewcoaching-desktop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b6b9498-f692-4d2b-bcef-895d1290f4d4/121interviewcoaching-desktop-300x258.png" alt="121interviewcoaching - desktop site" width="300" height="258" /></a><br>
<em>Click for larger view.</em>

The website has a responsive design, with straightforward changes to the layout depending on the screen’s size. On phones in portrait mode, it currently looks like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb00dcb0-c5c2-4cc3-87c0-02e395933201/121interviewcoaching-mobile.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111932" title="121interviewcoaching-mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/013281db-385a-424a-847d-6bbc81041f40/121interviewcoaching-mobile-200x300.png" alt="121interviewcoaching - mobile site" width="200" height="300" /></a><br>
<em>Click for larger view.</em>

The most important tappable area on this website is the button above the menu, which has been resized to make it easier to tap on small screens. But the left-aligned menu below looks a bit scruffy and would look better centered.

To do this, we add some CSS in the relevant media query. The menu items are currently in an unordered list, each set to float left with padding on the right. We can change this with the following code:

<pre><code class="language-css">.menu {
   text-align: center;
   margin-top: 10px;
}

.menu a {
   display: inline;
}

.menu li {
   float: none;
   display: inline;
}</code></pre>

This code centers the text of the menu as a whole; removes the floats from the list items and links; and displays the list items inline rather than as blocks. If all we did was center the text, then each link would appear as a centered list one above the other.

Having made this change, the website now looks like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cee7f433-a72e-4a04-bb1f-1b4ed87633d8/121interviewcoaching-mobile2.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111933" title="121interviewcoaching-mobile2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f4db6a8-062f-4c04-8a73-ab10d4679455/121interviewcoaching-mobile2-200x300.png" alt="121interviewcoaching - mobile site after tweaks" width="200" height="300" /></a><br>
<em>Click for larger view.</em>

The links are now nicely centered. We just had to slightly edit the menu text, shortening “Areas covered” to “Areas” to make that link span one line instead of two.

Obviously, this hasn’t improved the ergonomics or functionality of the menu much, but it has improved the design, and it took just moments. Making the links larger would be another usability improvement here. But instead <strong>let’s look at the size of navigation links on a website that needs more radical changes</strong>.</p>

### 2. Enhancing the Ergonomics: Make Menus Easier to Tap

Accurately tapping the links in the average navigation bar is not as easy as it should be on a small touchscreen device. We can help this both by making the tappable areas larger and by making the links look more like buttons, which sends a very clear signal to users of where to tap.

Tappability is an issue not only for phones, but for larger touch devices, such as tablets.</p>

### Improving the Navigation for Tablets

My own website, <a href="https://compass-design.co.uk/">Compass Design</a>, is responsive but not yet optimized for touch interfaces. Its layout on the iPad and other large tablets is similar to its layout on desktops, which might look fine, but the navigation links are too small for the user to tap comfortably. On narrower screens (such as when in portrait mode), the navigation drops to a second line, which looks messy.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d077cce1-39a5-431a-a3e8-18fed2ce3429/compassdesign-ipad.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111934" title="compassdesign-ipad" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8916e1f0-a988-48e8-96f7-2ecbd39b6fc5/compassdesign-ipad-260x300.png" alt="Compass Design - site on iPad" width="260" height="300" /></a><br>
<em>Click for larger view.</em>

We can fix these issues by making each link the same width, with text spanning two (or more) lines if need be. This would make each link larger without adding to the overall screen space taken up by the menu.<strong> The only downside is that this approach only works if you know how many links are in the menu</strong> — if you add more, then the CSS will need to be tweaked.

This effect is done with the following code:

<pre><code class="language-css">@media screen and (max-width: 780px) {
   .menu li {
   width: 10%;
   padding: 1%;
   margin: 0;
   border-left: 1px solid #fff;
   border-right: 1px solid #333;
   }
}

.menu li:first-child {
   border-left: none;
}

.menu li:last-child {
   border-right: none;
}

.menu li a {
   margin: 0;
   padding: 0 0 0.2em 0;
   line-height: 1.1em;
   text-align: center;
   height: 3.8em;
}</code></pre>

This code does the following:

*   Sets the width of each menu item to 10% of the width of the full menu, and adds some padding;
*   Removes margins that were previously set to the right of each menu item for spacing;
*   Adds a double border, making each link look a little more like a button, and removes this border from the first and last elements, as needed;
*   Reduces the line height of the link in each menu item (previously set to 3 em for spacing);
*   Sets a manual height for each link, and centers the text.

Here is the result:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8aca3b05-bfa5-4ef6-87ca-f8dc9578537f/compassdesign-ipad2.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111935" title="compassdesign-ipad2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60f7d13d-bae8-43ee-8c4c-b49a7311f4f2/compassdesign-ipad2-300x77.png" alt="Compass Design - site on iPad after menu tweaks" width="300" height="77" /></a><br>
<em>Click for larger view.</em>

It’s an improvement. The menu items all line up horizontally, and the links are easy to tap with a thumb. But aligning the text to the top looks untidy, so let’s fix this using CSS tables:

<pre><code class="language-css">.menu li {
   display: table;
}

.menu li a {
   display: table-cell;
   vertical-align: middle;
}</code></pre>

This makes the link in each menu item behave like a table cell, and it enables us to center the text vertically, a technique <a href="https://css-tricks.com/vertically-center-multi-lined-text/">documented on CSS-Tricks</a>.

Let’s see what that looks like:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d389b1a0-460d-4b6e-bfde-3c279243c791/compassdesign-ipad3.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111937" title="compassdesign-ipad3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b948601-78e5-4db3-9bef-947b79b69623/compassdesign-ipad3-300x74.png" alt="Compass Design site - final iPad version" width="300" height="74" /></a><br>
<em>Click for larger view.</em>

The navigation links are now large enough to tap with a thumb; they look more like buttons; and the layout is much neater. <strong>This is a good solution for when the horizontal navigation is too wide to fit on the screen without the text wrapping.</strong> We’ve achieved some improvements in both design and UX, with just a few lines of CSS.</p>

### Improving Navigation for Phones

As you can imagine, this layout would look terrible and be nigh-on impossible to use on very narrow screens, such as phones. To fix this, we’ll make each navigation link stretch the full width of the screen and make it large enough to tap.

Here’s the code:

<pre><code class="language-css">@media screen and (max-width: 480px) {
   .menu {
      background: #666;
   }
}

.menu li li {
   width: 100%;
   border: none;
   border-top: 1px solid #fff;
   border-bottom: 1px solid #333;
   background: -moz-linear-gradient(top, #ffffff 0%, #666666 100%); /* FF3.6+ */
   background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#ffffff), color-stop(100%,#666666)); /* Chrome,Safari4+ */
   background: -webkit-linear-gradient(top, #ffffff 0%,#666666 100%); /* Chrome10+,Safari5.1+ */
   background: -o-linear-gradient(top, #ffffff 0%,#666666 100%); /* Opera 11.10+ */
   background: -ms-linear-gradient(top, #ffffff 0%,#666666 100%); /* IE10+ */
   background: linear-gradient(top, #ffffff 0%,#666666 100%); /* W3C */
}

.menu li:first-child {
   border-top: none;
}

.menu li:last-child {
   border-bottom: none;
}

.menu li a {
   padding: 0;
   font-size: 1.2em;
   line-height: 1em;
   height: 2.8em;
}</code></pre>

This code does the following:

*   Replaces the CSS gradient in the menu with a mid-gray block;
*   Makes each item in the menu take up 100% of the screen’s width;
*   Adds our gradient to each menu item;
*   Removes the borders for tablets and adds new top and bottom borders, again removing them for the first and last children as needed;
*   Removes the padding previously set on the links;
*   Alters the height of each link and the text size, which makes the link button-like, with text that almost fills it and that is clearly legible on a small screen.

How does this look?

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dc1a15a-457a-4fbd-9047-19dc86cf4311/compassdesign-iphone1.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111938" title="compassdesign-iphone1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b3c2914-b8c2-4c01-a7ab-042775f4f215/compassdesign-iphone1-150x300.png" alt="Compass Design - menu on iPhone" width="150" height="300" /></a><br>
<em>Click for larger view.</em>

The tappability has improved, but the menu now dominates the screen and pushes the content below the fold. This needs to be fixed. Which brings us to the next aspect of responsive menus: their position.</p>

### 3. Positioning: Relocating the Navigation on Very Small Screens

On tablets and desktops, keeping the menu at or near the top of the screen makes sense, because this is where users would expect to find it, and it doesn’t take up too much of the screen there. But what about small screens such as phones?

In his book <em>Mobile First</em>, Luke Wroblewski advocates for moving navigation to the bottom of the page on smartphones. This way, when the user has scrolled to the bottom of a page and has finished reading the content, they have somewhere to go. Let’s try that for this menu.

We want to move the menu below the page’s content but above the footer, without having to create a new menu or make any changes to the markup. <strong>This can be done using a combination of absolute positioning and margins.</strong> We’ll have to make sure that the height of the menu is fixed, so our first change will be to switch the height of each menu link from ems to pixels:

<pre><code class="language-css">#access li a {
   padding: 0;
   margin: 0;
   font-size: 16px;
   height: 57px;
}</code></pre>

I haven’t worried about calculating the height of each link. I’ve just set it to the recommended 57 pixels, which is close to what its height was in ems.

Having done this, we can calculate the height of the menu as 57 pixels plus 2 pixels (i.e. the borders), multiplied by the number of menu items (nine), minus 2 pixels (to account for the borders that we removed from the top and bottom links). This works out to 529 pixels. We then use absolute positioning to move the menu to the position we need it in, with padding to give it some breathing room:

<pre><code class="language-css">.container {
   padding-bottom: 549px;
   position: relative;
}

.nav-strip {
   position: absolute;
   bottom: 0;
}</code></pre>

This moves the navigation to the bottom of the page, between the main content and the footer. I must own up that I did make one change to the markup — I needed a containing element for the menu, which ends before the footer, so I added an empty <code>div</code> with a <code>container</code> class. The <code>div</code> opens at the very top of the <code>body</code> element and closes just before the footer. <strong>Without that container, the menu would have moved below the footer to the very bottom of the page.</strong>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25c54e4e-de22-44e6-a000-86d87f2754e5/compassdesign-iphone2.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111939" title="compassdesign-iphone2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7ff0006-f91c-4a0a-81b2-49dc9ebcb20e/compassdesign-iphone2-142x300.png" alt="Compass Design - iPhone menu after tweaks" width="142" height="300" /></a><br>
<em>Click for larger view.</em>

The menu is now less obtrusive when the users first arrives on the website, but it still takes up a lot of room. A possible solution would be to convert it into a select menu, using the <a title="Responsive Select menu - WordPres plugin" href="https://wordpress.org/extend/plugins/responsive-select-menu/">Responsive Select Menu</a> plugin. This would probably be the best approach for very long menus, multi-level menus and menus that are likely to have links added or taken away.

For this website, however, I’ll stick with the CSS styled menu.

But there is still one problem. A new visitor who lands on the website’s home page on a phone and wants to navigate around will be presented with content and no menu, unless they think to scroll down — and we certainly couldn’t expect users to know that they need to do that.

This is a broader issue, and it also relates to where to deliver the menu on different devices. Let’s deal with that next.</p>

### 4. Different Menus for Different Devices

There are a number of methods for delivering a different menu to each kind of device. If your website uses a CMS, then plugins or conditional code would likely achieve this. Here we’ll look at a way to achieve this purely with CSS.

The downside to this method is that it’s based on screen size, not on device, so it assumes that a visitor on a small screen would need a different menu (or at least would benefit from one). It also includes two blocks of markup for two menus, which are delivered to all devices but one of which is hidden using CSS. However, if your menus are just text, they shouldn’t put too much of a strain on the website’s loading times.

<strong>While I’m not an advocate of hiding content from mobile visitors, and I get really frustrated by websites that do, I do think that restructuring the navigation for mobile devices is sometimes helpful.</strong> For example, customers who are checking a business’ bookings, times and locations on their phone need to be able to get at this information quickly and easily via the navigation. For some websites, this would necessitate radical alterations to the navigation on small screens, creating a more app-like menu, while — importantly — including access to the other areas of the website elsewhere on every page. For other websites this would simply require a menu with a different structure, or possibly one with fewer top-level links that fits better on a small screen.

In this case, we just need to add a single link that appears on mobile devices only. What we want to do is create a link to the navigation menu near the top of the page that redirects visitors to the menu.

We can do this by placing a link to the menu immediately above the content. And we use CSS to hide it on desktops and tablets. We’ll add this just above the content:

<pre><code class="language-markup tmp-html">&lt;a class="menu-link" href="#menu"&gt;Menu&lt;/a&gt;</code></pre>

And we’ll add this just above the menu itself:

<pre><code class="language-markup tmp-html">&lt;a class="menu-anchor" name="menu"&gt;</code></pre>

The CSS to hide this link on large screens is simple and goes in the main section of the style sheet:

<pre><code class="language-css">a.menu-link,
a.menu-anchor {
   display: none;
}</code></pre>

The CSS in our media query displays the link and anchor, styles the link and gives the anchor a height of <code>0</code> so that it doesn’t affect the page’s layout:

<pre><code class="language-css">a.menu-link,
a.menu-anchor {
   display: block;
}

a.menu-anchor {
   height:0;
}</code></pre>

The styles for the <code>.menu-link</code> element are the same as for the navigation links, which we styled earlier.

The website now has a prominent link that appears on small screens, taking the visitor to the navigation menu, while making better use of the screen’s real estate. This link is styled to look like the navigation menu itself:

### 4. Different Menus for Different Devices

There are a number of methods for delivering a different menu to each kind of device. If your website uses a CMS, then plugins or conditional code would likely achieve this. Here we’ll look at a way to achieve this purely with CSS.

The downside to this method is that it’s based on screen size, not on device, so it assumes that a visitor on a small screen would need a different menu (or at least would benefit from one). It also includes two blocks of markup for two menus, which are delivered to all devices but one of which is hidden using CSS. However, if your menus are just text, they shouldn’t put too much of a strain on the website’s loading times.

<strong>While I’m not an advocate of hiding content from mobile visitors, and I get really frustrated by websites that do, I do think that restructuring the navigation for mobile devices is sometimes helpful.</strong> For example, customers who are checking a business’ bookings, times and locations on their phone need to be able to get at this information quickly and easily via the navigation. For some websites, this would necessitate radical alterations to the navigation on small screens, creating a more app-like menu, while — importantly — including access to the other areas of the website elsewhere on every page. For other websites this would simply require a menu with a different structure, or possibly one with fewer top-level links that fits better on a small screen.

In this case, we just need to add a single link that appears on mobile devices only. What we want to do is create a link to the navigation menu near the top of the page that redirects visitors to the menu.

We can do this by placing a link to the menu immediately above the content. And we use CSS to hide it on desktops and tablets. We’ll add this just above the content:

<pre><code class="language-markup tmp-html">&lt;a class="menu-link" href="#menu"&gt;Menu&lt;/a&gt;</code></pre>

And we’ll add this just above the menu itself:

<pre><code class="language-markup tmp-html">&lt;a class="menu-anchor" name="menu"&gt;</code></pre>

The CSS to hide this link on large screens is simple and goes in the main section of the style sheet:

<pre><code class="language-css">a.menu-link,
a.menu-anchor {
   display: none;
}</code></pre>

The CSS in our media query displays the link and anchor, styles the link and gives the anchor a height of <code>0</code> so that it doesn’t affect the page’s layout:

<pre><code class="language-css">a.menu-link,
a.menu-anchor {
   display: block;
}

a.menu-anchor {
   height:0;
}</code></pre>

The styles for the <code>.menu-link</code> element are the same as for the navigation links, which we styled earlier.

The website now has a prominent link that appears on small screens, taking the visitor to the navigation menu, while making better use of the screen’s real estate. This link is styled to look like the navigation menu itself:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd849c8c-813f-496f-b116-b3dad9008a15/compassdesign-iphone31.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111941" title="compassdesign-iphone3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff69bf0-66fd-49d7-a981-0d720118d3e4/compassdesign-iphone31-191x300.png" alt="Compass Design site - link to navigation on iPhone" width="191" height="300" /></a><br>
<em>Click for larger view.</em>

We know how to hide links on large screens using CSS, but what about hiding an entire navigation menu?

To do this, we use the exact same technique. I developed a website for <a href="https://centenarylounge.com">Centenary Lounge</a>, a coffee shop in Birmingham’s Moor Street station, and the client wanted not only a responsive website but an optimized menu for mobile devices. The desktop navigation was large, with links to a lot of historical information on the coffee shop and its history, however, mobile users needed to be able to find out where Centenary Lounge was and when it would be open.

Our solution was to create two menus and alternately hide one or the other on small or large screens, using classes to identify which menu was which. Here is the code from the main part of the style sheet, aimed at desktops:

<pre><code class="language-css">menu.mobile {
   display: none;
}</code></pre>

This hides the menu and removes it from the flow of the page.

Here is the CSS inside the media query for screens narrower than 480 pixels (i.e. phones in landscape and portrait mode):

<pre><code class="language-css">menu.mobile {
   display: block;
}

menu.desktop {
   display: none;
}</code></pre>

This reverses the earlier code for the mobile menu, making it visible, and hides the desktop menu. It doesn’t specify that the desktop menu needs to be displayed for desktops because that is the default anyway.

This code resulted in a website with smaller, more focused navigation for mobile devices:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80a4338a-23f3-4410-a47b-d43f1e3ab505/centenarylounge-desktop.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111942" title="centenarylounge-desktop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92a712c7-2613-4e5b-8130-18c821612bae/centenarylounge-desktop-300x235.png" alt="Centenary Lounge website on desktop" width="300" height="235" /></a>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1acc0ec-a9ba-42c0-9c3a-e1063dc3a4ee/centenarylounge-mobile.png"><img loading="lazy" decoding="async" class="size-medium wp-image-111943" title="centenarylounge-mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b315b708-814a-458b-a073-9b0d6abd8da9/centenarylounge-mobile-199x300.png" alt="Centenary Lounge site on mobile" width="199" height="300" /></a><br>
<em>Click for larger view.</em>

Access to the full content of the website is still there via the “Discover” link, but reducing the number of top-level links has made better use of the space and made the most commonly used links more prominent. As with all mobile design projects, the question begs to be asked whether a similar change would benefit the UX on the desktop!

## Summary

As you can see, the subject of responsive menus has a lot of potential and a number of solutions and considerations. We’ve looked at some of the main issues to consider when designing navigation for mobile devices and worked through some solutions to these. Here are some of them:

1.  Make quick tweaks to the visual design of the menu to make it better fit a mobile layout.
2.  Enhance the tappability of navigation links by ensuring they are at least 44 pixels square and that they look like obvious links in a mobile context (mobile users might be more used to tapping on buttons than text).
3.  Consider the best location for navigation, and move the menu to the bottom of the page, using only CSS.
4.  Use CSS to display a different menu depending on the device being used.

<strong>The solutions you adopt will depend on a number of factors, including the needs of the website, the nature of the menus and the expectations of users.</strong> Not to mention, for websites using a CMS, delivering different content to different devices without CSS and without sending unnecessary markup to each device is often possible. However, for text-based menus, using CSS to reposition, hide and restyle mobile navigation is a fairly straightforward and flexible approach that is definitely worth considering.

{{< signature "al" >}}


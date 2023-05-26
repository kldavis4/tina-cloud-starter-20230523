---
title: Creating Mobile-Optimized Websites Using WordPress
slug: creating-mobile-optimized-websites-using-wordpress
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cad66cb0-80b2-4eb6-a07e-66a42baf56db/twenty-eleven-desktop.jpg
date: 2012-05-24T08:30:21.000Z
author: rachel-mccollin-2
description: >-
  “Mobile Web design.” Unless you’ve been hiding under a bush for the last 18
  months, you’ll know that it’s one of the hottest topics in the industry at the
  moment. Barely a week goes by without new tips being unveiled to help us hone
  our skills in making websites work as well — and as fast — as possible on
  mobile devices.
categories:
  - WordPress
  - Mobile
  - Responsive Design
---
“Mobile Web design.” Unless you’ve been hiding under a bush for the last 18 months, you’ll know that it’s one of the hottest topics in the industry at the moment. Barely a week goes by without new tips being unveiled to help us hone our skills in making websites work as well — and as fast — as possible on mobile devices.

If you own or have designed a WordPress website for the desktop and are considering going mobile, the process can be fairly daunting. You probably know of <a title="responsive design - smashing magazine article" href="https://www.smashingmagazine.com/responsive-web-design-guidelines-tutorials/">responsive design</a> and might have heard of the mobile-first approach <a title="Luke Wroblewski on mobile first" href="https://www.lukew.com/ff/entry.asp?933">developed by Luke Wroblewski</a>, which entails planning the content and design for mobile devices first and then desktops second, rather than the other way round.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   <span>[Creating Mobile-Optimized Websites Using WordPress](https://www.smashingmagazine.com/2012/05/creating-mobile-optimized-websites-using-wordpress/)</span>
*   [How To Become A Top WordPress Professional](https://www.smashingmagazine.com/2012/12/become-top-wordpress-professional/)
*   [Useful WordPress Tools, Themes And Plugins](https://www.smashingmagazine.com/2012/03/useful-wordpress-tools-themes-plugins/)
*   <span>[Writing Effective Documentation For WordPress End Users](https://www.smashingmagazine.com/2012/07/writing-effective-wordpress-documentation/)</span>

But if your WordPress website has a desktop theme in which everything is set in pixels, then the thought of adopting a responsive design might have you running for the hills.

{{% feature-panel %}}

It doesn’t have to be that way.

Here are four ways to make your WordPress blog or website mobile-friendly, ranging from the quick and dirty to the complex but potentially very beautiful. As well as outlining the pros and cons of these methods, we’ll include information on plugins that will help without actually doing all the work for you, and we’ll provide some code that you can use for a responsive design.</p>

## Plugins: The Quick Way To Make Your Content Mobile-Friendly

Designing for content is increasingly becoming more common than squeezing content into a pixel-perfect design, as <a title="Content strategy within the design process" href="https://www.smashingmagazine.com/2011/12/02/content-strategy-within-design-process/">documented here on Smashing Magazine</a>.

If your website is more about content than design (say you run a blog that is content-heavy and designed for reading), then you won’t be too fussed about what your website looks like on mobile devices. You just want people to be able to read it without having to zoom in, move the viewport around or generally tie themselves up in knots until they decide to leave.

If this is the case, then a simple plugin might do the trick. Below are some plugins to consider.</p>

### WPtouch

<a title="WP-Touch" href="https://www.wptouch.com/">WPtouch</a>, which comes in free and premium versions, strips out your existing theme and displays your content and not much else, but the result is user-friendly, robust and easy to read.

WPtouch is widely used on websites, including <a title="Stephen Fry's blog" href="https://www.stephenfry.com/">Stephen Fry’s blog</a> and <a title="Social Media Examiner" href="https://www.socialmediaexaminer.com/">Social Media Examiner</a>. You can see below how the plugin renders those two websites. The premium version has options to modify the colors and some styles, including a bespoke menu at the bottom of the screen, as seen on Social Media Examiner.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22781bf0-5ea2-438f-b411-8c66ea73df11/socialmediaexaminer-desktop-original1.png"><img loading="lazy" decoding="async"  class="size-medium wp-image-111786" title="socialmediaexaminer-desktop-original" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dce7f4cc-3d65-4a0a-a921-af4251534465/socialmediaexaminer-desktop-original1-300x203.png" alt="Social Media Examiner - desktop site" width="300" height="203" /></a><br>
<em>Social Media Examiner desktop design</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/473a640b-d76f-4273-aeba-de100808193a/socialmediaexaminer-mobile-original1.png"><img loading="lazy" decoding="async"  class="size-medium wp-image-111787" title="socialmediaexaminer-mobile-original" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d51fedc-2055-4677-94b5-426477e3de73/socialmediaexaminer-mobile-original1-200x300.png" alt="The Social Media Examiner mobile site - minimal styling" width="200" height="300" /></a><br>
<em>Social Media Examiner mobile design, using WPtouch</em>

### WordPress Mobile Pack

The <a title="WordPress mobile pack" href="https://wordpress.org/extend/plugins/wordpress-mobile-pack/">WordPress Mobile Pack</a> has some color options and can be used as a mobile switcher if you want a completely different theme for mobile devices. It also has a mobile interface for editing posts, although this has been superseded to some extent by the WordPress apps for <a title="WordPress iOs apps" href="https://ios.wordpress.org/">iOS</a> and <a title="WordPress Android app" href="https://android.wordpress.org/">Android</a>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89ddf913-b928-4cfc-83d0-85dc8f6f5894/wp-mobile-pack-original.png"><img loading="lazy" decoding="async"  class="111597" title="wp-mobile-pack" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e54cd83d-ef9b-40c9-b20b-215f413da87c/wp-mobile-pack.png" alt="WordPress mobile pack gives a mobile interface with one or two colours and simple posts listing." width="500" height="456" /></a><br>
<em>WordPress Mobile Pack screenshots</em>

### BuddyPress Mobile

If your website runs BuddyPress, then you’ll need a plugin to ensure that none of its functionality is lost on mobile devices. BuddyPress Mobile has theming options, and you can edit the style sheet to make the mobile design your own.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6e5b365-996b-440c-ad11-92fe8363595e/buddypress-mobile-original.png"><img loading="lazy" decoding="async"  class="111580" title="buddypress-mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/689f12c9-f35e-4afb-a377-bf6c4317cede/buddypress-mobile.png" alt="BuddyPress mobile displays member information such as profile picture and updates." width="336" height="600" /></a><br>
<em>BuddyPress Mobile</em>

## Mobile Themes: The Next Level Up

If you want a consistent design across desktop and mobile, but you don’t yet have a theme or you want to develop one, then a mobile theme might be the answer.

More and more mobile themes have sprung up over the last year. In particular, <a title="WordPress twenty eleven" href="https://wordpress.org/extend/themes/twentyeleven)">Twenty Eleven</a>, WordPress’ default theme since version 3.0, is responsive enough for many websites.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b31a06f-d9b8-4b6f-8544-0de6fb639493/twenty-eleven-desktop-original.png"><img loading="lazy" decoding="async"  class="111595" title="twenty-eleven-desktop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e72c230e-d8ea-45ad-a36b-7937048c548e/twenty-eleven-desktop.png" alt="The twenty eleven desktop version includes a full width header image and standard sidebar to the right." width="500" height="339" /></a><br>
<em>Twenty Eleven on the desktop</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/016c8714-1ca9-4a70-a54e-2f761d652051/twenty-eleven-mobile-original.png"><img loading="lazy" decoding="async"  class="111596" title="twenty-eleven-mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d93d92e0-bff4-42e3-b217-c9977e620f99/twenty-eleven-mobile.png" alt="The mobile version of twenty eleven displays a narrower header image and moves the sidebar below the main content." width="400" height="600" /></a><br>
<em>Twenty Eleven on mobile</em>

Below are some other themes that include a mobile or responsive style sheet.</p>

### Carrington

The <a title="Carrington theme" href="https://carringtontheme.com">Carrington</a> family of themes can be used as parent themes. You can edit the CSS and functions to suit your needs, and it has a mobile version.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/480715ef-0ab6-40aa-b6a8-58804f2dda81/carrington-desktop-original.png"><img loading="lazy" decoding="async"  class="111583" title="carrington-desktop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0eaec1b0-b451-4826-8ae9-e702ed13dc1a/carrington-desktop.png" alt="The desktop version of Carrington includes two sidebars to the right and some use of colour and graphics." width="500" height="339" /></a><br>
<em>Carrington on desktop</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7644446-6b82-4d63-965b-98642cd7a9dc/carrington-mobile-original.png"><img loading="lazy" decoding="async"  class="111584" title="carrington-mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa1930c8-0b66-445d-8620-162fa4229e37/carrington-mobile.png" alt="On mobile, Carrington has only one font, moves sidebars below the content and uses default colours for links." width="393" height="600" /></a><br>
<em>Carrington on mobile</em>

### Scherzo

Scherzo is clean and minimalist and would be great to use as a parent theme. It uses a mobile-first responsive design.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04d1bd0c-aae3-4004-95f0-7feb3b183b6f/scherzo-desktop-original.png"><img loading="lazy" decoding="async"  class="111589" title="scherzo-desktop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20df5483-132a-4f2b-a34a-7ad161a52b40/scherzo-desktop.png" alt="Scherzo on the desktop has a white background and dark grey text with blue headings, and a sidebar to the right." width="500" height="339" /></a><br>
<em>Scherzo on desktop</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6c66bb4-08fc-4ab0-b208-2c0d8e0c2998/scherzo-mobile-original.png"><img loading="lazy" decoding="async"  class="111590" title="scherzo-mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90c13553-1687-44db-9fc7-8215034db540/scherzo-mobile.png" alt="Scherzo on mobile uses the same font styles as the desktop version with a white background and moves the sidebar below the main content. It has less white space than the desktop version." width="371" height="600" /></a><br>
<em>Scherzo on mobile</em>

### Jigoshop

E-commerce websites are trickier to make mobile-friendly, but <a title="Jigoshop theme/plugin" href="https://jigoshop.com/">Jigoshop</a> can help. It’s a full e-commerce plugin and theme, with a responsive layout that can be tweaked to suit your design.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32c10404-9dc8-4cf0-b1d4-f8bac1cba982/jigoshop-desktop-original.png"><img loading="lazy" decoding="async"  class="111587" title="jigoshop-desktop" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/056d4e31-9bc6-44fb-9684-6da866d1156c/jigoshop-desktop.png" alt="Jigoshop on the desktop uses a white background with dark grey text, green details, product images in a grid and a sidebar to the right." width="500" height="339" /></a><br>
<em>Jigoshop on desktop</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ad7c58b-7117-452d-87ec-774ee5723e28/jigoshop-mobile-original.png"><img loading="lazy" decoding="async"  class="111588" title="jigoshop-mobile" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e64d5786-d0d5-4848-844d-f8a42a93666f/jigoshop-mobile.png" alt="Jigoshop on mobile uses the same colours and font styling as the desktop version with a simplified menu banner, a narrower grid for product images and the sidebar below the main content." width="408" height="600" /></a><br>
<em>Jigoshop on mobile</em>

## A Different Theme For Mobile Devices

In the days before responsive design gained traction, websites commonly had two versions: desktop and mobile. The mobile version might have been on an <code>m.</code> subdomain or have a <code>.mobi</code> extension. Some websites out there still do this, mainly huge news websites that serve different content depending on the device.

Fewer WordPress administrators are choosing to do this now, but if you do want to go down this route, then serving two versions of your website from the same database is possible, by using a mobile switcher.

Here are two plugins that make this possible:

*   [WordPress Mobile Pack](https://wordpress.org/extend/plugins/wordpress-mobile-pack/ "WordPress mobile pack") This tool, already mentioned above as a theme that makes your website mobile-friendly, can also be used as a mobile switcher, detecting mobile devices and using a separate theme of your choice.
*   [WPtap Mobile Detector](https://wordpress.org/extend/plugins/wptap-mobile-detector/ "WPtap mobile detector") This targets mobile devices and enables the theme of your choice.

Using one of these plugins enables you to develop a completely separate theme for mobile devices, with its own layout, navigation and content structure.</p>

## Or, Finally, Make Your Current Theme Responsive

If you don’t want to throw out your existing theme, then the best way to give mobile users an experience that is at least visually similar to the desktop version is to build responsiveness into your theme.

A responsive theme contains media queries in the theme’s style sheet to define CSS that applies only to devices of a specified maximum or minimum width. A truly responsive theme has a fluid layout that adapts to mobile devices and larger screens to some extent already, but with some extra styling to make the layout optimal for mobile devices.</p>

### 1. Defining the Media Queries

To get started, you will need to define media queries in the style sheet. Most of the styles already in your style sheet apply to desktop and mobile, so you only need to add CSS that is different for mobile devices. This will go at the end of your theme’s style sheet.

Start by defining the screen width you are developing for. There are two main approaches to this:

1.  Start with the narrowest screen width you are targeting (which will usually be mobile phones in portrait orientation); add all of the CSS needed for this screen width; and then add successive media queries for wider screens. This is known as the mobile-first approach, and it has the benefit of making websites faster on mobile devices because only the CSS needed for those devices is loaded.
2.  Start with the widest screen width (usually desktop monitors) and work down, adding CSS that applies to each screen width in turn. While this might slow down loading on mobile devices, it has the advantage of working in IE 8 and below, which doesn’t understand media queries. At the moment, most websites are developed this way because they involve making an existing desktop design responsive, so this is the approach we’ll cover here.

A media query consists of three main parts:

1.  The `@media` rule;
2.  The media type (the most common being `print` and `screen` — we’ll use `screen`);
3.  The maximum width of the screen you are targeting.

You could have a media query to target mobile phones (and other small devices such as the iPod Touch) in portrait orientation that have a width of 320 pixels:

<pre><code class="language-css">@media screen and (max-width: 320px) {

}</code></pre>

The CSS to be applied to that screen width and any screen narrower than it would be written between the braces.

An alternative to the <code>@media</code> rule would be to create a linked style sheet with the CSS for each screen width. But I don’t do that because it adds another server request with the potential to slow the website down; and managing all of the styles becomes harder if they’re in more than one place.

Here are other media queries for commonly targeted screen sizes:

*   `(max-width: 480px)` Works for mobile devices in either portrait or landscape mode, because they are 480 pixels wide in landscape orientation but are still narrower than this maximum width in portrait.
*   `(max-width: 780px)` Works for iPads and other large tablets in portrait mode and any screens narrower than them.
*   `(max-width: 1024px)` Works for iPads in both orientations, as well as for small desktop browsers.

You can run one media query after another so that each change you make applies to the screen size you’re querying, plus any widths queried further down in the style sheet. In this case, you would work with wider screens first. For example:

<pre><code class="language-css">@media screen and (max-width: 480px) {

}</code></pre>

If you are ignoring tablets, you would include this media query first and add any CSS for mobile phones in both portrait and landscape modes (for example, any changes to graphics or text size). You would then follow it with this:

<pre><code class="language-css">@media screen and (max-width: 320px) {

}</code></pre>

Here, we’re adding any styles that apply only to phones in portrait mode (such as layout changes). You don’t need to repeat the CSS that applies to both landscape and portrait modes because this will still apply. In the same way, you don’t need to repeat any styles that will stay the same for desktop views because they will cascade down from the earlier parts of the style sheet.</p>

### 2. Making the Layout Responsive

Phew! So, now we’ve defined media queries, and we’re ready to roll with some mobile-friendly CSS. Below are the main things you will need to work on for a standard WordPress website. Let’s assume your website’s markup is similar to that of the Twenty Eleven theme (i.e. <code>html</code> → <code>body</code> → <code>header</code> (or div <code>#header</code>) → <code>#main</code> → <code>#content</code> → <code>#primary</code> → <code>#secondary</code> → <code>footer</code> (or div <code>#footer</code>). You might need to substitute your own elements and IDs for the ones in the examples below.

<strong>Overall width of website</strong>
You’ll need to change this so that it displays correctly. Add the following code between the braces of your first media query:

<pre><code class="language-css">body {
width: 100%;
float: none;
}</code></pre>

This ensures that the website’s <code>body</code> fills the width of the device and removes any floats. At this point, you might also want to change the background image if there is one (more on that shortly).

You will now have the following code at the bottom of your style sheet:

<pre><code class="language-css">@media screen and (max-width: 480px) {
   body {
   width: 100%;
   float: none;
   }
}</code></pre>

<strong>Width of content and sidebar</strong>
In portrait mode in particular, there isn’t room for a sidebar to the right of the main content. Add the following code to the media query relating to devices with a maximum width of 320 pixels:

<pre><code class="language-css">#content, #primary, #secondary {
width: 100%;
float: none;
margin: 10px 0;
}</code></pre>

<strong>Footer content, especially widgets</strong>
If your footer has widget areas or other elements with floats applied, you will need to override them for mobile devices in portrait mode.

If you want the footer widgets to be full width in both landscape and portrait modes, then simply add <code>footer.widget-area</code> to the CSS for the sidebars and content.

However, you might want the widget areas to be laid out side by side in landscape mode, depending on how many you have. In that case, you’ll need to do the following:

1.  Work out the percentages for the widths, padding and margins (some box-model maths for you!);
2.  Add the relevant code to your media query for devices with a maximum width of 480 pixels;
3.  Add a separate query for devices with a maximum width of 320 pixels after the one you’re working on, with the following code:

<pre><code class="language-css">footer .widget-area {
width: 100%;
float: none;
margin: 10px 0;
}</code></pre>

You might also need to adjust the text alignment and borders and padding, depending on your existing theme. Margins should be set to 0 on the left and right; suit them to your theme at the top and bottom, but generally they should be smaller than in the desktop version.

<strong>Image sizes</strong>
The images in your design might still break the layout or break out of their containing elements, making your website shrink when viewed on a mobile device. There is an easy fix for this:

<pre><code class="language-css">body img {
max-width: 100%;
}</code></pre>

This will ensure that images are never wider than their containing element. You might need to tweak the CSS if images sized further up in the style sheet have greater specificity.

However, this solution isn’t ideal. The images might look smaller, but mobile devices will still have to download their full sizes, which will slow down response times and possibly lose visitors, as well as annoy users on expensive data plans (more of them are out there than you might think). There a number of solutions to this, some of which you will find in this <a title="Smashing magazine on responsive images" href="https://www.smashingmagazine.com/2011/07/22/responsive-web-design-techniques-tools-and-design-strategies/">roundup of articles on responsive images</a>. You may recall the mobile-first approach mentioned earlier; one benefit of this approach is that it serves different-sized image files to devices based on screen width.

<strong>Text size</strong>
So, our layout is working, and everything displays nicely. But now that the website is narrower, the text might appear huge. We’ll need to adjust the text’s size with the following code:

<pre><code class="language-css">body {
font-size: 60%;
line-height: 1.4em;
}</code></pre>

This sets the font size as a percentage of the size set for it further up in the style sheet.</p>

### 4. Changing the Navigation Menus and Creating an App-Like Interface

Sometimes mobile users will want to access specific content; for example, visitors to a store’s website will want to find the store’s location easily, and visitors to an e-commerce website will want to shop with a minimum of clicks (or taps). Sometimes you might want to adjust the navigation to make the website look more like an app.

Here are some methods you can follow to do this:

*   Use CSS to turn menu items that are visible on the desktop into drop-down menus, using code similar to what you would use to create a second-level drop-down menu on a desktop website.
*   Use conditional PHP or a plugin such as [Mobble](https://wordpress.org/extend/plugins/mobble/ "Mobble plugin") to display a different menu depending on the device, as seen on the website that I developed for [Centenary Lounge](https://centenarylounge.com "Centenary Lounge website"): [![The centenary lounge desktop site includes a large logo and full width slideshow, using shades of brown for text and the background.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d24bb77f-03e9-449c-b81b-71ce3400a122/centenarylounge-desktop.png "centenarylounge-desktop")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f55680c4-3db1-4423-865e-85fb3e375cd6/centenarylounge-desktop-original.png) _Centenary Lounge desktop website_ [![The Centenary Lounge mobile site includes the same colours and design but replaces the slideshow with a smaller image, and the full width navigation menu with a shorter menu focusing on pages that visitors from mobiles are more likely to need.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7db7e649-90ac-42a3-88f7-87d6a74c8d02/centenarylounge-mobile.png "centenarylounge-mobile")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2d879de-dd9d-4cdb-ac5a-60b09397f04a/centenarylounge-mobile-original.png) _Centenary Lounge mobile website_
*   Use CSS to display menu items as a vertical list of buttons to give the website an app-like look, such as on Cafe Blend: [![The Cafe Blend desktop site has a vertical navigation menu to the left of the main content, all contained within a balck box.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12213708-ec41-4100-a215-5eac5525b7c1/cafeblend-desktop.png "cafeblend-desktop")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/394e916c-ce70-48f2-9b1e-f2832726234d/cafeblend-desktop-original.png) _Cafe Blend desktop website_ [![The Cafe Blend mobile site has a full-width navigation menu with each menu item in a horizontal box resembling a button, with the content below the menu.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbeb1f4f-0786-4479-bb43-c91c43473e17/cafeblend-mobile.png "cafeblend-mobile")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/899f3c3c-fbbb-4121-ac7b-28ce7a42d4da/cafeblend-mobile-original.png) _Cafe Blend mobile website_
*   Use a plugin such as [Dropdown Menus](https://wordpress.org/extend/plugins/dropdown-menus/ "Dropdown menus plugin") to display menu items as a drop-down walker, freeing up screen real estate.
*   Use background images combined with media queries and floats, to create a grid of visual buttons for your navigation, giving the home page an app-like feel.
*   Use fixed positioning to fix the navigation to the bottom of the screen, minimizing the need for scrolling, as seen earlier on Social Media Examiner.

The possibilities are limited only by your imagination and creativity!

### 5. A Problem!

You’ve added the media queries above, but your smartphone still displays the desktop version. Don’t worry! This is because many smartphones use a virtual viewport that is equal to the width of a small desktop, which prevents desktop-designed websites from breaking when rendered in the browser. This can be easily fixed by placing the following code in the <code>head</code> of each page. Because yours is a WordPress website, you need to add it only once, to the <code>header.php</code> theme file:

<pre><code class="language-markup tmp-html">&lt;meta name="viewport" content="width=device-width"&gt;</code></pre>

What this does is tell the phone to treat the size of the screen as its actual size, not the virtual size… if that makes sense.</p>

## Summary

Here’s what we’ve looked at in this article:

*   Four different ways to make a WordPress website mobile-friendly: with a plugin, with a prebuilt responsive theme, with a separate mobile theme, and by making the existing theme responsive;
*   Media queries for responsive design and how they target different device widths;
*   Some common styles to make a WordPress website responsive in its layout, images and text.

As you can see, no one option is necessarily the best; it will depend on the website, on the budget and on the time and capability of those involved. Over time, most mobile-friendly WordPress websites will have responsiveness built into them, instead of using a separate theme, mobile website or plugin.

Hopefully this article has given you a starting point to make your WordPress website mobile-friendly. This is just the beginning of the possibilities. To further develop your mobile website, you might want to consider a mobile content strategy; a mobile-first design; APIs and native device functionality to create an even more app-like experience; and more.

Enjoy!

{{< signature "al" >}}


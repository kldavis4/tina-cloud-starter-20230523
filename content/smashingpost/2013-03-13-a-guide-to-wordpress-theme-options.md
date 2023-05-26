---
title: A Guide To The Options For WordPress Theme Development
slug: a-guide-to-wordpress-theme-options
image: >-
  https://www.smashingmagazine.com/mobile/2014/02/06/applying-xsl-transformations-to-responsive-web-design/attachment/transforms-6-wireframe-responsive-delivery/attachment/wordpress_theme_customizer-2/
date: 2013-03-13T12:16:55.000Z
author: rachel-mccollin-2
description: >-
  At the recent [WordCamp Edinburgh](https://2012.edinburgh.wordcamp.org/), I
  took part in a panel discussion about WordPress theme development and the
  options available to developers when building themes. The overriding
  conclusion from the session was that **there isn’t a one-size-fits-all
  answer** and that the best method depends on the needs of the website and the
  capabilities of the developer.
categories:
  - WordPress
  - Techniques (WP)
---
At the recent <a href="https://2012.edinburgh.wordcamp.org/">WordCamp Edinburgh</a>, I took part in a panel discussion about WordPress theme development and the options available to developers when building themes. The overriding conclusion from the session was that <strong>there isn’t a one-size-fits-all answer</strong> and that the best method depends on the needs of the website and the capabilities of the developer.

But if you’re starting out building WordPress themes or want to develop a system for building them more efficiently or robustly, how do you decide which approach to take? In this article, we’ll briefly describe how WordPress themes work and then look at some of the different approaches to developing them, with tips on which approach might be most suitable for your website and circumstances.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Migrating A Website To WordPress Is Easier Than You Think](https://www.smashingmagazine.com/2013/05/migrate-existing-website-to-wordpress/)
*   [Using WP_Query In WordPress](https://www.smashingmagazine.com/2013/01/using-wp_query-wordpress/)
*   [Schedule Events Using WordPress Cron](https://www.smashingmagazine.com/2013/10/schedule-events-using-wordpress-cron/)
*   [How To Improve The Deployment Of WordPress Websites](https://www.smashingmagazine.com/2013/04/wordpress-deployment-survey/)

## How Does A WordPress Theme Work?

In WordPress, themes drive a website and determine what it contains, how it behaves and what it looks like. The theme is separate from the content, which is held in the database. This means you can use the same theme on more than one website, regardless of the content of the websites — which you might already be doing if you’ve downloaded themes from <a href="https://wordpress.org/extend/themes/">WordPress’ theme repository</a>.

{{% feature-panel %}}

A theme consists of a number of template files, all stored in the theme folder, which you’ll find in <code>wp-content/themes</code> in your WordPress installation. Every WordPress theme has to include <strong>at least two files</strong>: <code>index.php</code> and <code>style.css</code>. The index file defines what content is displayed by the theme, and the style sheet (you guessed it) styles it, as well as contains meta information about the theme that WordPress uses to make the theme work correctly.

Actually, most themes have a few additional files:

*   `header.php` Contains the `<head>` section of each page, plus the header of the website’s design.
*   `sidebar.php` Contains the sidebar, including any widget areas.
*   `footer.php` Contains the footer, which may or may not have widget areas.
*   `functions.php` Contains any functions that are specific to your theme. You can find out about the functions file [in the WordPress Codex](https://codex.wordpress.org/Theme_Development#Functions_File).
*   Files that contain the [loop](https://codex.wordpress.org/The_Loop), which call the content from the database. Depending on which part of the website you’re working in, this could be one of a number of files:
    *   `page.php` For static pages
    *   `single.php` For individual posts (blog posts, for example)
    *   `index.php`, `archive.php`, `category.php`, etc. For pages that list a number of posts

Yoast has written a great <a href="https://yoast.com/wordpress-theme-anatomy">visual representation of how theme files work</a>, and the <a href="https://codex.wordpress.org/Theme_Development">WordPress Codex</a> includes a detailed description of themes, including details on the various files and when they are called.

I would argue that the style sheet, however, is the most important file and the one you are likely to begin with, because a “child theme” (more of that shortly) needs a style sheet even if it contains nothing else. The style sheet contains important meta information about the theme itself, which is commented out before all of the styles. Below are the opening comments for WordPress’ current default theme, <a href="https://wordpress.org/extend/themes/twentyeleven">Twenty Eleven</a>:

<pre><code class="language-css">/*
   Theme Name: Twenty Eleven
   Theme URI: https://wordpress.org/extend/themes/twentyeleven
   Author: the WordPress team
   Author URI: https://wordpress.org/
   Description: The 2011 theme for WordPress is sophisticated, lightweight, and adaptable. …
   Version: 1.3
   License: GNU General Public License
   License URI: license.txt
   Tags: dark, light, white, black, …
*/</code></pre>

This information is commented out so that it isn’t read by browsers, but it is read by WordPress, and it provides information to anyone using your theme. We’ll come back to this shortly when we look at how to create a child theme.

Now that you know how themes work, the next step is to figure out how to go about building your own. Before starting, it would be worth considering some points that will help you make that decision.</p>

## What To Consider When Developing A WordPress Theme?

Before deciding which approach to take to develop your theme, identify your constraints. These likely include the following:

*   **Time**.  How much time do you have to develop your theme, or to learn how to do it?
*   **Budget**.  This is related to time but also has to do with whether you can afford to pay for a premium theme or a theme framework.
*   **Capability**.  How familiar are you with theme development, with CSS and PHP and with how themes work? If you’re not familiar, how much do you want to learn?
*   **Future-proofing**.  Will your theme need to be updated in future? Will other developers be working on it in addition to you? If so, then your approach will need to be as robust as possible.
*   **Repetition**.  Do you see yourself developing a number of similar themes in future? If so, your approach will have to allow for code to be reused.

We’ll revisit these considerations at the end of the article and identify which development options are most suitable for various situations.</p>

## Theme Development: Your Options

A few options are available for developing your theme or themes, and investigating them before you roll your sleeves up and start coding would be worthwhile. Picking the right approach will result in a better theme, with more robust code, and it will minimize the amount of revisions you’ll have to do later. It will also help you to build the theme more efficiently.

The options we’ll look at here are:

*   Build a theme from scratch,
*   Edit (or “hack,” some might say) an existing theme,
*   Use the theme customizer to tweak an existing theme,
*   Create a child theme to make changes to an existing theme,
*   Create your own parent theme (using one of the approaches above) and child themes,
*   Use a theme framework.</p>

### 1. Build A Theme From Scratch

This approach is the most difficult if you’re inexperienced. But if you’re a seasoned WordPress developer, it will give you the <strong>most control</strong>. It might be the most appropriate method if you’re importing HTML from an existing static website that is being upgraded to WordPress with no other changes.

However, when transferring a website to WordPress, conducting a review of it as part of the process, rather than simply copying the code across, is a good idea. If you are copying a static website, you’ll need to keep a close eye on your code to ensure that it’s clean, efficient and valid.</p>

### 2. Edit (or Hack) an Existing Theme

This is how most people start with WordPress theme development: in working on a theme that they’ve downloaded, they see that some styling isn’t quite right, so they delve into the style sheet and make some edits. Starting like this is tempting because it feels like a quick and easy way to achieve the effect you want. But <strong>there are some dangers</strong>:

*   If you ever switch themes, that update will override any changes you’ve made.
*   It’s easy to add repetitive code by adding new styles lower down in the style sheet that override styles higher up, rather than removing what you don’t need.
*   The website could end up with a lot more code than it needs.
*   If the theme isn’t well coded or commented to begin with, you could get yourself into a bigger mess and find that you have to make a lot of fixes.

However, hacking a theme can work if you <strong>go into it with your eyes open</strong>. It may be an option if the following are true:

*   The theme you're using is well written, valid and commented (e.g., the default WP theme, Twenty Eleven);
*   The changes you’re making are so drastic that you wouldn’t need to update the original theme;
*   You understand the PHP and CSS contained in the theme and are comfortable editing, adding to and removing it without breaking the theme.

If you do decide to go down this route, keeping a backup of the original theme and commenting your code thoroughly are important. I would also advise commenting out any code that you don’t want and then testing to see what happens before deleting anything.</p>

### 3. Use the Theme Customizer to Tweak an Existing Theme

The theme customizer was released with WordPress 3.4. It gives you the option to customize a theme without writing any code, simply by using a WYSIWYG interface. Depending on how well the customizer is written into the theme itself, you can use it to change images, titles, colors and even the layout. Expect to see more themes with the customizer integrated into them.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04cd631e-2000-4f06-8eae-e6aeed29ba39/wordpress-theme-customizer.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04cd631e-2000-4f06-8eae-e6aeed29ba39/wordpress-theme-customizer.jpg" alt="Using the WordPress theme customizer with the Twenty Ten theme." width="500" height="300" /></a><figcaption>Using the WordPress theme customizer with the Twenty Ten theme.</figcaption></figure>

The theme customizer stores your changes in a separate file, not in the theme’s style sheet, so there will be repetitive code.

For more information, take a look at Otto on WordPress’ <a href="https://youtube.com/watch?v=vD8v6u3noPg">video tutorial</a> or <a href="https://ottopress.com/2012/how-to-leverage-the-theme-customizer-in-your-own-themes/">guide to integrating the theme customizer into your own themes</a>.</p>

### 4. Create a Child Theme to Make Changes to an Existing Theme

This approach is similar to editing an existing theme, but safer. It consists of creating a brand new theme that is defined as a child of the existing theme. Where your child theme doesn’t have a particular file but the parent theme does, it will use that. Where the child theme does have a file, that file will override the equivalent in the parent. Let’s look at an example:

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th>Parent theme files</th>
<th>Child theme files</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<ul>
 	<li><code>style.css</code></li>
 	<li><code>page.php</code></li>
 	<li><code>single.php</code></li>
 	<li><code>archive.php</code></li>
 	<li><code>header.php</code></li>
 	<li><code>sidebar.php</code></li>
 	<li><code>footer.php</code></li>
</ul>
</td>
<td>
<ul>
 	<li><code>style.css</code></li>
 	<li><code>page.php</code></li>
 	<li><code>header.php</code></li>
</ul>
</td>
</tr>
</tbody>
</table>

In the example above, WordPress would use the following files to deliver content:

*   `style.css` from the child theme,
*   `page.php` from the child theme,
*   `single.php` from the parent theme,
*   `archive.php` from the parent theme,
*   `header.php` from the child theme,
*   `sidebar.php` from the parent theme,
*   `footer.php` from the parent theme.

You can see how this would be useful if you wanted to use most of the parent theme’s markup but change the content of the header (adding, say, your logo and address details) and any static pages (maybe changing the way that meta data is displayed).

The one <strong>file that every child theme must have</strong> in order to work is the style sheet, because it contains the information that WordPress needs to make the child theme function correctly. To do this, add some extra code to the style sheet’s comments:

<pre><code class="language-css">/*
  Theme Name: Twenty Eleven Child Theme
  Theme URI: https://example.com
  Author: you!
  Author URI: https://example.com/
  Description:  Child theme based on Twenty Eleven.
  Template: twentyeleven
  Version: 1.0
  Tags: your tags (optional)
 */
@import url("../twentyeleven/style.css");</code></pre>

<strong>Can you spot the extra lines?</strong> The first one is:

<pre><code class="language-css">Template: twentyeleven</code></pre>

This line tells WordPress that the theme is a child theme and that Twenty Eleven is its parent. You would add the name of the parent theme’s directory, not its full name.

And the second one:

<pre><code class="language-css">@import url("../twentyeleven/style.css");</code></pre>

This line tells the browser to load the parent theme’s style sheet before rendering any of the styles in the current style sheet. This frees you from having to duplicate any styles in the parent theme that you want to use.

So, that’s how child themes work. But when is this <strong>the best approach?</strong> I would suggest using it in the following cases:

*   You already have a theme (to be used as the parent) that contains most of what you need for your theme;
*   You want to be able to update your parent theme (for example, when theme updates are released following a WordPress update);
*   You don’t want to get tied up in knots from hacking an existing theme;
*   You want the option to revert to the parent theme or to develop another similar theme in future (which would be a new child theme);
*   You’re developing a number of similar websites with some minor stylistic or content differences (I did this when building similar websites for a client that owned multiple companies);
*   The difference between your child and parent themes is not so huge that you need to start from scratch, or not so huge that your child theme’s code will override anything affected by updates to the parent theme.</p>

### 5. Create Your Own Parent Theme (Using One of the Approaches Above) and Child Themes

The situation I just alluded to, of building a set of websites for a client with multiple companies, is an occasion when you might create a parent theme and then set up child themes for individual websites. You might also want to do this in the following cases:

*   You plan to develop a lot of websites with similar content and markup in future (not just for one client);
*   You manage a lot of websites and have to dip into each of them regularly, and you want the code to be very similar;
*   You’re comfortable creating your own parent theme, editing the code to create a robust parent that will work well with child themes.

If you decide to adopt this approach, you could either build your parent theme from scratch or hack an existing theme. For most of the websites I build, I use a parent theme that I developed by hacking the Twenty Ten theme, the former default theme for WordPress. I made so many changes that I no longer needed to activate updates to the original theme. I was also comfortable with the code in the theme and wanted to make significant changes to it, reducing the code, restructuring it to <strong>fit the way I work</strong> and removing code that I knew I wouldn’t need.

You could also create a child theme based on an existing theme and then create child themes for that — effectively, grandchildren of the original theme. The advantage of this is that you will not overwrite the code in the original theme, while having the flexibility to make modifications to the child theme that will be passed down to the grandchild themes. A word of warning here, though: with three themes in use, it’s easy to get confused about what’s happening, and you could end up with a lot of unnecessary code.</p>

### 6. Use a Theme Framework

The final option is one used by thousands of WordPress users and developers. A number of theme frameworks exist that you can use as a kind of parent theme, but with much more functionality, and in some cases with the option to make quite fancy layout and style changes without writing a line of code. Some frameworks are free, while others are premium. They have been <a href="https://www.smashingmagazine.com/2009/05/27/wordpress-theme-development-frameworks/">reviewed in detail already on Smashing Magazine</a>, but the main ones are listed below.</p>

<strong>Free WordPress frameworks:</strong>

*   [Theme Hybrid](https://themehybrid.com/) includes a myriad of hooks and widget areas to help you customize your themes. It also has some child themes available. The framework and child themes are all free, but if you want support, you’ll have to pay for it by registering on Theme Hybrid’s website. Working with it can be quite complex unless you understand PHP or use one of the child themes.
*   [Wonderflux](https://wonderflux.com/) is based on a flexible grid system. It has options for adjusting layout and styles without having to write code, and it includes a lot of hooks and widget areas. It’s free to use and supported via the WordPress forums.
*   [Carrington](https://carringtontheme.com/) is the most established of the free frameworks, and it has a number of child themes.
*   [Thematic](https://themeshaper.com/thematic/) is developed by Automattic, which develops WordPress itself. It includes a number of hooks, filters and widget areas.

#### Premium WordPress frameworks:

*   Its developers describe [Genesis](https://www.studiopress.com/) as “the industry standard.” It comes with a wide variety of child themes, options to customize without writing code, and SEO features.
*   [Thesis](https://diythemes.com/) is the other big premium framework, and it also gives you the option to customize child themes without writing code.</p>

## Summary: Choosing An Approach

Chances are that, having read this, you’ve got an idea of which approach to go with. But in case you’re still scratching your head, here’s a summary of when each method is appropriate:
<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th>Approach</th>
<th>Time</th>
<th>Cost</th>
<th>Capability</th>
<th>Future-proofing</th>
<th>Repetition</th>
</tr>
</thead>
<tbody>
<tr>
<td>Build from scratch</td>
<td>High</td>
<td>Low</td>
<td>High</td>
<td>Low</td>
<td>Low</td>
</tr>
<tr>
<td>Hack existing theme</td>
<td>Low</td>
<td>Low</td>
<td>Medium</td>
<td>Low</td>
<td>Low</td>
</tr>
<tr>
<td>Use theme customizer</td>
<td>Low</td>
<td>Low</td>
<td>Low</td>
<td>Low</td>
<td>Low</td>
</tr>
<tr>
<td>Create child theme based on existing parent</td>
<td>Medium</td>
<td>Low</td>
<td>Medium</td>
<td>High</td>
<td>High</td>
</tr>
<tr>
<td>Create parent theme</td>
<td>High</td>
<td>Low</td>
<td>High</td>
<td>High</td>
<td>High</td>
</tr>
<tr>
<td>Theme framework (free)</td>
<td>Medium</td>
<td>Low</td>
<td>Medium</td>
<td>High</td>
<td>High</td>
</tr>
<tr>
<td>Theme framework (premium)</td>
<td>Medium</td>
<td>High</td>
<td>Low to medium</td>
<td>High</td>
<td>High</td>
</tr>
</tbody>
</table>

All in all, each approach has its place; it just depends on the website and on you. The important thing is to <strong>choose an approach after having weighed the pros and cons</strong> — not just to dive in and have a go, only to discover that you’ve broken a theme or that you’ve created a lot of rework for yourself.

And as always, whatever you decide, don’t forget to keep backups!

{{< signature "al" >}}


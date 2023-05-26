---
title: 'How To Create And Customize A WordPress Child Theme'
slug: create-customize-wordpress-child-theme
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fb58d35-b018-47c8-8b80-c1c89cb5201e/wordpress-logo-stacked-rgb-opt.png
date: 2016-01-21T20:02:17.000Z
author: nickschaeferhoff
summary: >-
  WordPress does make it really easily to completely customize a website. Unfortunately, any modifications made to a theme will be lost once the theme is updated by the developer &mdash; which is also bad for security. A much better idea is to use a child theme. This allows you to make any number of changes to a website without touching any of the original theme files. In this article we will take a detailed look at what WordPress child themes are, how to create them and how to use them to customize your website &mdash; the right way.
description: >-
  Child themes modifies or adds to the files of an existing theme in WrodPress and these customizations wont be lost if the parent theme changes. Learn here how to easily set up a child theme.
categories:
  - WordPress
  - Techniques (WP)
---

The WordPress platform is a magnet for those who want to take matters into their own hands, who want complete control over their websites and want to be independent in running them. WordPress does make it really easily to completely customize a website. If you have a bit of knowledge of HTMl, CSS and/or PHP, **there is nothing you can’t change**.

I mean, just compare the default themes, [Twenty Fifteen](https://wordpress.org/themes/twentyfifteen/) and [Twenty Fourteen](https://wordpress.org/themes/twentyfourteen/). Hard to believe they are running on the same platform, isn’t it? Therefore, it is only natural for you to want to adapt the look of your website to fit your vision. I doubt there are many WordPress users out there who don’t constantly think about what to implement next. However, a problem arises.

The biggest disadvantage is that **any modifications made to the theme in this way will be lost** once the theme is updated by the developer. As a consequence, users either won’t be able to keep their theme up to date (which is bad for security) or will find all of their customizations gone when they do.

Either way, the situation is far from an ideal.

A much better idea is to use a child theme. This allows you to make any number of changes to a website without touching any of the original theme files.

Sound good? Great, because in this article we will take a detailed look at what WordPress child themes are, how to create them and how to use them to customize your website &mdash; the right way.

I know! I’m as excited as you are!

{{% feature-panel %}}

## What Are Child Themes And Why Use Them?

When talking about child themes, we first have to talk about **parent themes**. A theme only becomes a parent theme when someone builds a child theme for it. Until then, it is just a theme, such as the ones you find in the [WordPress directory](https://wordpress.org/themes). Every theme that includes all of the files required in order to be considered complete can be a parent theme.

Yet, while any such theme _can_ be a parent theme, some are better suited to this purpose than others. For example, frameworks such as [Genesis by StudioPress](https://my.studiopress.com/themes/genesis/) are specifically made to be customized by child themes.

What is a child theme, then? Well, from the WordPress back end, a child theme doesn’t behave any differently. You can find and activate it under “Appearance” &nbsp;&rarr; “Themes,” just like you would with any other theme.

The big difference is that a **child theme depends completely on its parent in order to work**. Without its parent theme present, it will not do a thing and cannot even be activated.

That’s because a child theme isn’t a standalone entity, but instead modifies or adds to the files of an existing theme. It uses everything present in the parent theme and changes only those parts that you want to be different.

This allows you to alter styles, functions, layout, templates and more. In fact, you can customize the parent theme beyond recognition. However, without it being present, none of it will work.

## Advantages Of Child Themes

There are numerous advantages to going the child theme route:

- Instead of having to create a complete theme from scratch, you can **build on something that already exists**, thus speeding up development time.
- You can take advantage of the functionality of sophisticated frameworks and parent themes, while customizing the design to your needs.
- You can upgrade the parent theme without losing your customizations.
- If you aren’t satisfied with your customizations, just disable the child theme and everything will be as it was before.
- It’s a great way to start learning about how themes work.

A child theme can contain image folders, JavaScript, CSS, template files and many other things. The beautiful thing, though, is that they don’t have to. You can include as much or as little customization as you want.

In fact, a child theme really only needs three things: a folder, a style sheet and a `functions.php` file. That’s it. And the two files can even pretty much be empty.

### When to Use a Child Theme

So, should you always build a child theme whenever you want to make any changes to a WordPress website? No, it really depends.

If you plan to make only **minor modifications**, such as color changes or a different font, then a [custom CSS plugin](https://wordpress.org/plugins/wp-add-custom-css/) might be all you need (other options are [Jetpack](https://jetpack.me/support/custom-css/) and [SiteOrigin CSS](https://wordpress.org/plugins/so-css/)). Many themes nowadays also offer the option to add custom code natively.

However, if you plan to introduce **larger changes**, such as a complete design overhaul, multiple template changes or anything else of that magnitude, then a child theme is definitely the way to go.

{{% ad-panel-leaderboard %}}

## Set Up A Basic Child Theme

All right, now that we know how awesome child themes are and what they can do for us, let’s go over how to create one step by step. For our example, we will use [Twenty Fifteen](https://wordpress.org/themes/twentyfifteen/), the latest default theme for WordPress. Don’t worry, it’s really easy and you will get it in no time.

**Side note:** The steps below can be performed directly on your server via an FTP client. However, I recommend that you first set up everything locally, then zip your child theme folder and install it like a normal theme via the “Theme” menu. This will make the whole thing much easier.

### Create a Folder in `wp-content/themes`

As mentioned, a child theme needs three things: its own folder, a style sheet and a `functions.php` file. We will start with the folder.

Like any theme, child themes are located in `wp-content/themes` in your WordPress installation. So, navigate there now and create a new folder for your child theme.

A best practice is to give your theme’s folder the same name as the parent theme and append it with `-child`. Because we are using the Twenty Fifteen theme, we will call our folder `twentyfifteen-child`.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2eebc87-ae57-43ca-9f17-8c6dbe4cbe56/01-create-theme-folder-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/321839fb-8679-4461-ade6-703201c5b0f3/01-create-theme-folder-opt-small.jpg" width="436" height="114" alt="Screen with a list of 3 folders and a index.php file" /></a><figcaption>Creating a folder for our WordPress child theme.</figcaption></figure>

You are free to use any name you want to; just make sure not to include any spaces because that might cause errors.

### Create a Style Sheet

Now that we have our folder, we will need a style sheet. In case you are not aware, a style sheet contains the code that determines the design of a website. Themes can have multiple style sheets, but we will be content with one for the moment.

Making a style sheet is easy: Simply create a new text file and call it `style.css`. Done! However, in order for it to actually work, we will have to paste the following code, the so&mdash;called “style sheet header,” right at the beginning of the file (code courtesy of the [WordPress Codex](https://codex.wordpress.org/Child_Themes)):

<pre><code class="language-php">/*
Theme Name: Twenty Fifteen Child
Theme URI: https://example.com/twenty-fifteen-child/
description: >-
  Twenty Fifteen Child Theme
Author: John Doe
Author URI: https://example.com
Template: twentyfifteen
Version: 1.0.0
License: GNU General Public License v2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html
Tags: light, dark, two-columns, right-sidebar, responsive-layout, accessibility-ready
Text Domain: twenty-fifteen-child
*/
</code></pre>

Here is what each line means:

- **Theme name**. This is the name that will show up for your theme in the WordPress back end.
- **Theme URI**. This points to the website or demonstration page of the theme at hand. This or the author’s URI must be present in order for the theme to be accepted into the WordPress directory.
- **Description**. This description of your theme will show up in the theme menu when you click on “Theme Details.”
- **Author**. This is the author’s name &mdash; that’s you, in this case.
- **Author URI**. You can put your website’s address here if you want.
- **Template**. This part is crucial. Here goes the name of the parent theme, meaning its folder name. Be aware that it is case&ndash;sensitive, and if you don’t put in the right information, you will receive an error message, so double&ndash;check!
- **Version**. This displays the version of your child theme. Usually, you would start with 1.0.
- **License**. This is the license of your child theme. WordPress themes in the directory are usually released under a GPL license; you should stick with the same license as your parent theme.
- **License URI**. This is the address where your theme’s license is explained. Again, stick with what your parent theme says.
- **Tags**. The tags help others find your theme in the WordPress directory. Thus, if you include some, make sure they are relevant.
- **Text domain**. This part is used for internationalization and to make themes translatable. This should fit the “slug” of your theme.

If you feel a bit overwhelmed (already?), you might be happy to know that not all of this information is actually required. In fact, all you really need is the theme name and template.

The rest is important only if you plan to publish your theme, which I am not. For this reason, my child theme’s header looks like what’s shown below. Feel free to copy it and make your own adjustments.

<pre><code class="language-php">/*
 Theme Name:   Twenty Fifteen Child Theme
 description: >-
   A child theme of the Twenty Fifteen default WordPress theme
 Author:       Nick Schäferhoff
 Template:     twentyfifteen
 Version:      1.0.0
*/
</code></pre>

### Activate Child Theme

Once your folder and style sheet are present, go to “Appearance” &nbsp;&rarr; “Themes” in the WordPress back end and find your child theme there. When you click on “Theme Details” now, you will see the contents of the style sheet header. That’s what that info is for.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e5601b6-13ed-441b-b2ae-eabee74c2593/02-wordpress-child-theme-header-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2ba75a9-cab3-4b72-95d2-5385fabcd500/02-wordpress-child-theme-header-opt-small.jpg" width="800" height="439" alt="The WordPress child theme header" /></a><figcaption>The WordPress child theme’s header. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e5601b6-13ed-441b-b2ae-eabee74c2593/02-wordpress-child-theme-header-opt.jpg">Large preview</a>)</figcaption></figure>

All right, now click on the button that says “Activate.” Good job! Your theme is now activated. However, if you look at your website, it should look something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cae19ec3-48b5-4a68-8269-c127c869bcc2/03-wordpress-child-theme-without-stylesheet-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2022135a-06bd-4f0b-95ca-208336306261/03-wordpress-child-theme-without-stylesheet-opt-small.jpg" width="800" height="641" alt="WordPress child theme without style sheet" /></a><figcaption>WordPress child theme without style sheet. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cae19ec3-48b5-4a68-8269-c127c869bcc2/03-wordpress-child-theme-without-stylesheet-opt.jpg">Large preview</a>)</figcaption></figure>

Don’t worry, everything is fine. You haven’t screwed up. Get your face out of the paper bag. The reason why your website is empty is because it doesn’t have any styles yet. No styles means you get treated to an all&mdash;text experience.

I just wanted to show you that, in theory, having a style sheet and a folder is enough to create a child theme. And if it worked for you, then you’ve already done it! I’ll be the first to admit, though, that it could look a little better. Let’s get to that now.

### Create functions.php

Next up is the `functions.php` file. You have probably heard of this file before, but let’s quickly go over what it is for.

The `functions.php` file allows you to change and add functionality and features to a WordPress website. It may contain both PHP and native WordPress functions. Plus, you are free to create your own functions.

In short, `functions.php` contains code that **fundamentally changes** how a website looks and behaves. Got it? Nice, I knew I could count on you.

Creating the file is as easy as creating a style sheet, if not more so. All you need is a text file named `functions.php`, and then paste in the following code:

<pre><code class="language-php">&lt;?php
//* Code goes here
</code></pre>

Seriously, that’s it. Just add that opening `php` tag and you are good to go. Of course, you could get all fancy and write some information in the header (don’t forget to comment it out so that WordPress doesn’t try to execute it), but this will do for our purpose. Add it to your theme’s folder as well.

Now, let me say this: You don’t _need_ `functions.php`. If you don’t plan to use PHP to modify your theme, then you can completely do without it. A style sheet and other files might be enough for you.

However, I wanted to include this part, first, so that you would know about this important file and, secondly, because of the next step.

### Inherit Parent Styles

So, you are probably aware that your website is still mostly text. It’s time to change that. How? I’ll show you.

Because you are using a parent theme, you probably have a good idea of how your website is supposed to look. For our example, Twenty Fifteen, we want to get to this point:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea6f2139-6919-4a3c-a25f-ef7435991cd7/04-twenty-fifteen-wordpress-default-theme-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2488821-00a3-46b2-8eeb-bdf8c01a397c/04-twenty-fifteen-wordpress-default-theme-opt-small.jpg" width="800" height="417" alt="WordPress default Twenty Fifteen theme" /></a><figcaption>WordPress’ default Twenty Fifteen theme. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea6f2139-6919-4a3c-a25f-ef7435991cd7/04-twenty-fifteen-wordpress-default-theme-opt.jpg">Large preview</a>)</figcaption></figure>

To get here, you will need to inherit the information in your parent theme’s style sheet. There are two ways to do this.

One is via CSS and the `@import` rule. By copying the code below into your `style.css` file, you are telling your child theme to use the info contained in your parent theme’s style sheet to present your content.

<pre><code class="language-css">@import url("../twentyfifteen/style.css");
</code></pre>

Be aware, however, that this is the **old way** of inheriting parent styles and is no longer recommended. The reason for that is performance.

If you need to import several style sheets (which is not unheard of), then using `@import` will cause them to download **consecutively**. This can slow down the page’s loading time by several seconds (which, I probably don’t have to tell you, isn’t a good thing).

The second, recommended way to load the parent’s style sheet &mdash; and the reason why we created `functions.php` earlier &mdash; is to use `wp_enqueue_style()`. [This WordPress function](https://codex.wordpress.org/Function_Reference/wp_enqueue_style) safely adds style sheet files to a WordPress theme.

In our case, the corresponding code looks a little something like this:

<pre><code class="language-php">add_action( 'wp_enqueue_scripts', 'enqueue_parent_styles' );

function enqueue_parent_styles() {
   wp_enqueue_style( 'parent-style', get_template_directory_uri().'/style.css' );
}
</code></pre>

Be sure to paste this at the beginning of your `functions.php` file, and save it (remember to upload the file if you are using an FTP connection). Now check your front end; it should look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd264e1c-0c48-4ced-82dc-17df37925009/05-wordpress-child-theme-successfully-activated-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b512049-0cd2-41ce-ad32-4ae42f05bbbd/05-wordpress-child-theme-successfully-activated-opt-small.jpg" width="800" height="1070" alt="WordPress child theme successfully activated" /></a><figcaption>WordPress child theme successfully activated. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd264e1c-0c48-4ced-82dc-17df37925009/05-wordpress-child-theme-successfully-activated-opt.jpg">Large preview</a>)</figcaption></figure>

Pretty, right? Congratulations, you did it! You created your very first WordPress child theme. If I were there, I’d pat you on the shoulder.

However, you might object, rightly, that it looks exactly like the parent theme. So, what’s the point of going with a child theme?

Don’t worry. Next you will learn how to customize the child theme to look exactly the way you want.

### Extra Points: Add Theme Image

If you want to get all fancy, you could add a theme image. This image will show up in the theme menu in WordPress.

All you need to do is create a PNG file, named `screenshot.png`, and place it in your theme’s folder (in our case, `twentyfifteen-child`. Make sure to put it in the top&mdash;level directory and not in a subdirectory such as `images`.

The recommended size is **880&times;660** pixels, although it will be shown as 387&times;290. The larger dimensions ensure that the image will show up well on high&mdash;resolution screens.

Other image formats such as JPEG and GIF would also work, but PNG is recommended. You can do this now for extra props or wait until you are done customizing the theme, because the image is usually a screenshot of the theme’s design.

## Customizing Your WordPress Child Theme

If you have done everything correctly, then your child theme should now be activated and look exactly like its parent. This is where the fun begins.

Now we can start customizing our theme and change things around to get the result we are looking for. Customizations can be done in many different ways, and we will go over a whole lot of them.

### Implementing Custom Styles

One of the easiest ways to make changes to your theme is via CSS. This allows you to customize colors, dimensions, fonts and other fundamental design elements.

If you are proficient in CSS, you could actually change the entire layout of your website. However, introducing such drastic changes is usually done differently. We will get to that.

For now, all you need to know is that, with `style.css` in place, you can override any styles in the parent theme by adding code to the child theme’s style sheet.

Important: If you’ve called the parent theme’s styles in your `style.css` file, then be sure to add any custom styles **below** the `@import` statement, as in the following snippet. (Although you do know you’re supposed to use `functions.php`, right?)

<pre><code class="language-css">/*
 Theme Name:   Twenty Fifteen Child Theme
 description: >-
   A child theme of the Twenty Fifteen default WordPress theme
 Author:       Nick Schäferhoff
 Template:     twentyfifteen
 Version:      1.0.0
*/

// Custom styles go here
</code></pre>

Twenty Fifteen is a beautifully designed theme. I really like the generous white space, which lets the content breathe and is soothing to the eye.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5ea2409-96b7-4387-9eb0-e8bb72e17321/06-twenty-fifteen-content-layout-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3bc714b-c343-4a83-a449-876d242185cb/06-twenty-fifteen-content-layout-opt-small.jpg" width="800" height="589" alt="Twenty Fifteen layout" /></a><figcaption>Twenty Fifteen’s layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5ea2409-96b7-4387-9eb0-e8bb72e17321/06-twenty-fifteen-content-layout-opt.jpg">Large preview</a>)</figcaption></figure>

However, let’s say you are not a fan and want to cram a few more words into each line. No harm in that. In that case, you would use a tool like [Firebug](https://addons.mozilla.org/en-US/firefox/addon/firebug/) to figure out which styles need to be modified. Your search would turn up the following:

<pre><code class="language-css">.entry-header {
   padding: 0 10%;
}</code></pre>

<pre><code class="language-css">.entry-title, .widecolumn h2 {
   font-size: 3.9rem;
   line-height: 1.2308;
   margin-bottom: 1.2308em;
}</code></pre>

<pre><code class="language-css">.entry-content, .entry-summary {
   padding: 0 10% 10%;
}</code></pre>

We would make a few adjustments that achieve what we have in mind and copy them to the `style.css` file of our child theme.

<pre><code class="language-css">.entry-header {
   padding: 0 5%;
}
.entry-title, .widecolumn h2 {
   margin-bottom: 0.5em;
}
.entry-content, .entry-summary {
   padding: 0 5% 10%;
}</code></pre>

Voilá! Here is the result:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad9fe0d8-9ee3-49d6-b0e5-86cd9cd72516/07-child-theme-custom-styles-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ae3999e-0745-452e-9e50-4844d5be434d/07-child-theme-custom-styles-opt-small.jpg" width="800" height="589" alt="WordPress child theme with custom styles" /></a><figcaption>WordPress child theme with custom styles. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad9fe0d8-9ee3-49d6-b0e5-86cd9cd72516/07-child-theme-custom-styles-opt.jpg">Large preview</a>)</figcaption></figure>

Whether that is better than before is another question, but you get the idea: Adding custom styles to a child theme will override styles in the parent theme.

### Overriding Parent Theme Files

You can not only target individual style declarations via the style sheet, but also override entire components of the parent theme.

For every theme file present in the parent directory, WordPress will check whether a corresponding file is present in the child theme and, if so, use that one instead. This means that a `header.php` file in the child theme will override its equivalent in the parent folder.

So, if you don’t like something about a page’s layout, just copy the respective file, implement your changes, and upload it to the child theme’s folder. The modifications will then appear in the child theme, while the original file will remain untouched.

For example, if we take `content.php` from the Twenty Fifteen theme’s folder and open it with an editor, among others things, we will find the following code:

<pre><code class="language-php">&lt;?php
   // Post thumbnail.
   twentyfifteen_post_thumbnail();
?&gt;

&lt;header class="entry-header"&gt;
   &lt;?php
   if ( is_single() ) :
      the_title( '&lt;h1 class="entry-title"&gt;', '&lt;/h1&gt;' );
   else :
      the_title( sprintf( '&lt;h2 class="entry-title"&gt;&lt;a href="%s" rel="bookmark"&gt;', esc_url( get_permalink() ) ), '&lt;/a&gt;&lt;/h2&gt;' );
   endif;
   ?&gt;
&lt;/header&gt;&lt;!-- .entry-header --&gt;
</code></pre>

Let’s see what happens when we reverse the order of these two, like this:

<pre><code class="language-php">&lt;header class="entry-header"&gt;
   &lt;?php
      if ( is_single() ) :
         the_title( '&lt;h1 class="entry-title"&gt;', '&lt;/h1&gt;' );
      else :
         the_title( sprintf( '&lt;h2 class="entry-title"&gt;&lt;a href="%s" rel="bookmark"&gt;', esc_url( get_permalink() ) ), '&lt;/a&gt;&lt;/h2&gt;' );
      endif;
   ?&gt;
&lt;/header&gt;&lt;!-- .entry-header --&gt;

&lt;?php
   // Post thumbnail.
   twentyfifteen_post_thumbnail();
?&gt;
</code></pre>

As you can see below, after saving and uploading the file to the child theme’s folder, the featured image of each blog post will now appear underneath the post’s title.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40dc864c-5bc3-46aa-8ed9-39038ad232cd/08-wordpress-child-theme-override-parent-theme-files-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dba4ff9-eff6-49bd-8344-af54974107fe/08-wordpress-child-theme-override-parent-theme-files-opt-small.jpg" width="800" height="417" alt="Override parent theme files with the child theme" /></a><figcaption>Override parent theme files with the child theme. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40dc864c-5bc3-46aa-8ed9-39038ad232cd/08-wordpress-child-theme-override-parent-theme-files-opt.jpg">Large preview</a>)</figcaption></figure>

Granted, it could use some styling, but you get the idea. You can use this method to make all kinds of changes to your website. Just remember to give the child theme the same folder tree structure as the parent. For example, if a file you want to modify is found in a folder named `page-templates` in the parent theme, then you would create a folder of the same name in your child theme’s directory and place the file there.

### Working With Template Files

We’ve learned that we can overwrite any file in the parent theme by placing a copy in the child theme’s folder and customizing it. However, using files that **exist only in the child theme** is also possible. Template files are a good example of this.

Let’s say we want to build a full&ndash;width page template for our child theme. I’ll be the first to admit that the Twenty Fifteen theme does not lend itself to full&mdash;screen presentation, but let’s do it anyway for demonstration purposes, shall we?

To create a full&ndash;width page in Twenty Fifteen, we need to do four things: create a custom page template, a custom header and a footer file, and then add some customized CSS. Let’s start with the page template.

For our custom page template, we simply copy `page.php` from the parent theme, rename it to `custom-full-width.php` and place it in a folder named `page-templates` in our child theme.

Now, let’s introduce a couple of changes to the code so that it looks like this:

<pre><code class="language-php">&lt;?php
/*
 * Template Name: Custom Full Width
 * description: >-
  Page template without sidebar
 */

get_header('custom'); ?&gt;

   &lt;div id="primary" class="content-area"&gt;
   &lt;main id="main" class="site-main" role="main"&gt;

   &lt;?php
   // Start the loop.
   while ( have_posts() ) : the_post();

   // Include the page content template.
   get_template_part( 'content', 'page' );

   // If comments are open or we have at least one comment, load up the comment template.
   if ( comments_open() || get_comments_number() ) :
      comments_template();
   endif;

   // End the loop.
   endwhile;
   ?&gt;

   &lt;/main&gt;&lt;!-- .site-main --&gt;
   &lt;/div&gt;&lt;!-- .content-area --&gt;

&lt;?php get_footer('custom'); ?&gt;
</code></pre>

The only thing we’ve done here is introduce a header that tells WordPress that this is a page template, and we’ve changed the `get_header` and `get_footer` calls so that they will include two files named `header-custom.php` and `footer-custom.php`.

Let’s go to the page that we want to see in full width and, under “Page Attributes,” change the page template to our newly created “Custom Full Width” template.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5a392ae-2b0c-45f3-ab61-aa4a521f23b8/09-activate-page-template-in-wordpress-child-theme-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5a392ae-2b0c-45f3-ab61-aa4a521f23b8/09-activate-page-template-in-wordpress-child-theme-opt.jpg" width="313" height="351" alt="How to activate a WordPress page template" /></a><figcaption>How to activate a WordPress page template.</figcaption></figure>

Now it’s time to create our custom header and footer theme files. First, go to the parent theme, copy both `header.php` and `footer.php` to our child theme’s folder, and rename them to `header-custom.php` and `footer-custom.php`, respectively.

So far, our page looks the same as before. It’s time for some customization. Let’s start with our custom header.

<pre><code class="language-php">&lt;?php
/**
 * The template for displaying the header
 *
 * Displays all of the head element and everything up until the "site-content" div.
 *
 * @package WordPress
 * @subpackage Twenty_Fifteen
 * @since Twenty Fifteen 1.0
 */
?&gt;&lt;!DOCTYPE html&gt;
&lt;html &lt;?php language_attributes(); ?&gt; class="no-js"&gt;
&lt;head&gt;
   &lt;meta charset="&lt;?php bloginfo( 'charset' ); ?&gt;"&gt;
   &lt;meta name="viewport" content="width=device-width"&gt;
   &lt;link rel="profile" href="https://gmpg.org/xfn/11"&gt;
   &lt;link rel="pingback" href="&lt;?php bloginfo( 'pingback_url' ); ?&gt;"&gt;
   &lt;!--[if lt IE 9]&gt;
   &lt;script src="&lt;?php echo esc_url( get_template_directory_uri() ); ?&gt;/js/html5.js"&gt;&lt;/script&gt;
   &lt;![endif]--&gt;
   &lt;?php wp_head(); ?&gt;
&lt;/head&gt;

&lt;body class="full-width-body" &lt;?php body_class(); ?&gt;&gt;
&lt;div id="page" class="hfeed site"&gt;
   &lt;a class="skip-link screen-reader-text" href="#content"&gt;&lt;?php _e( 'Skip to content', 'twentyfifteen' ); ?&gt;&lt;/a&gt;

   &lt;header id="masthead" class="site-header full-width" role="banner"&gt;
   &lt;div class="site-branding full-width"&gt;
   &lt;?php
      if ( is_front_page() &amp;&amp; is_home() ) : ?&gt;
         &lt;h1 class="site-title"&gt;&lt;a href="&lt;?php echo esc_url( home_url( '/' ) ); ?&gt;" rel="home"&gt;&lt;?php bloginfo( 'name' ); ?&gt;&lt;/a&gt;&lt;/h1&gt;
         &lt;?php else : ?&gt;
         &lt;p class="site-title"&gt;&lt;a href="&lt;?php echo esc_url( home_url( '/' ) ); ?&gt;" rel="home"&gt;&lt;?php bloginfo( 'name' ); ?&gt;&lt;/a&gt;&lt;/p&gt;
         &lt;?php endif;

      $description = get_bloginfo( 'description', 'display' );
      if ( $description || is_customize_preview() ) : ?&gt;
         &lt;p class="site-description"&gt;&lt;?php echo $description; ?&gt;&lt;/p&gt;
      &lt;?php endif;
   ?&gt;
   &lt;button class="secondary-toggle"&gt;&lt;?php _e( 'Menu and widgets', 'twentyfifteen' ); ?&gt;&lt;/button&gt;
   &lt;/div&gt;&lt;!-- .site-branding --&gt;
   &lt;/header&gt;&lt;!-- .site-header --&gt;

   &lt;div id="content" class="site-content full-width"&gt;
</code></pre>

We’ve done a number of things here. We have given the `&lt;body&gt;` element a custom class, named `full-width-body`. We have also added a `full-width` class to `site-header`, `site-branding` and `site-content`, so that we can assign them custom CSS.

As a last step, we have gotten rid of all sidebar elements (both the `sidebar` div and the call to `get_sidebar`), because we don’t want them on our full-width page.

The only change we’ve made in `footer-custom.php` is to add the `full-width` class to the `footer` element, like so:

<pre><code class="language-html">&lt;footer id="colophon" class="site-footer full-width" role="contentinfo"&gt;</code></pre>

All that’s left to do is input some code in our style sheet:

<pre><code class="language-css">.full-width-body::before {
   display: none;
}

.site-content.full-width {
   float: none;
   margin: 0 auto;
}

.site-header.full-width {
   background-color: #fff;
   box-shadow: 0 1px 0 rgba(0, 0, 0, 0.15);
   margin: 0;
   padding: 2% 0;
}

.site-branding.full-width {
   margin: 0 auto;
   width: 58.8235%;
}

.site-footer.full-width {
   float: none;
   margin: 0 auto;
}
</code></pre>

Ta-da! And here is our full-width page:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5266c984-8298-478b-b283-617475b230b7/10-twenty-fifteen-custom-full-width-template-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3f07b2b-23c3-4e27-b323-41d5cef2769b/10-twenty-fifteen-custom-full-width-template-opt-small.jpg" width="800" height="1207" alt="Custom full-width page template for Twenty Fifteen theme" /></a><figcaption>Custom full-width page template for Twenty Fifteen theme. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5266c984-8298-478b-b283-617475b230b7/10-twenty-fifteen-custom-full-width-template-opt.jpg">Large preview</a>)</figcaption></figure>

It could use some polishing, but let’s be satisfied for the moment. For more shenanigans with page templates, check out my previous article on Smashing Magazine: [How To Create And Customize A WordPress Child Theme](https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/).

### Using functions.php

We’ve touched on `functions.php`. Use this file to include PHP and native WordPress functions in your theme. This will give you a lot of options for customization.

**Note:** The child theme’s `functions.php` file is loaded **in addition** to the file of the same name in the parent theme. In fact, it is executed **right before** the parent theme’s `function.php` &mdash; unlike `style.css`, which replaces the original file. Consequently, do not copy the full contents of your parent theme’s `functions.php` file to the file in your child theme. Rather, use the latter to modify functions in the parent theme.

Back to customizing our child theme. In this example, I want to add a widget area to the footer of the website. To do that, we first need to register a widget in our `functions.php` file.

<pre><code class="language-php">&lt;?php

register_sidebar( array(
   'name'          =&gt; 'Footer Widget',
   'id'            =&gt; 'footer-widget',
   'before_widget' =&gt; '&lt;div class="footer-widget"&gt;',
   'after_widget'  =&gt; '&lt;/div&gt;'
) );
</code></pre>

**Note:** The opening `&lt;?php` tag is the beginning of the `functions.php` file. Don’t include it if one is already there!

This will make the newly created widget area show up in our back end. However, for it to be usable on the website, we need to add the following code to `footer.php`:

<pre><code class="language-php">&lt;?php if ( is_active_sidebar( 'footer-widget' ) ) :
      dynamic_sidebar( 'footer-widget' );
   endif;
?&gt;
</code></pre>

Once more, we will copy `footer.php` from the Twenty Fifteen parent theme and paste it in our child theme. This time, however, we will leave its name as is.

After that, we need to add the call to our new footer widget so that it looks like this:

<pre><code class="language-php">&lt;?php
/**
 * The template for displaying the footer
 *
 * Contains the closing of the "site-content" div and all content after.
 *
 * @package WordPress
 * @subpackage Twenty_Fifteen
 * @since Twenty Fifteen 1.0
 */
?&gt;

   &lt;/div&gt;&lt;!-- .site-content --&gt;

   &lt;footer id="colophon" class="site-footer" role="contentinfo"&gt;
      &lt;div class="site-info"&gt;
      &lt;?php if ( is_active_sidebar( 'footer-widget' ) ) :
            dynamic_sidebar( 'footer-widget' );
         endif;
      ?&gt;
         &lt;?php
            /**
             * Fires before the Twenty Fifteen footer text for footer customization.
             *
             * @since Twenty Fifteen 1.0
             */
            do_action( 'twentyfifteen_credits' );
         ?&gt;
         &lt;a href="&lt;?php echo esc_url( __( 'https://wordpress.org/', 'twentyfifteen' ) ); ?&gt;"&gt;&lt;?php printf( __( 'Proudly powered by %s', 'twentyfifteen' ), 'WordPress' ); ?&gt;&lt;/a&gt;
      &lt;/div&gt;&lt;!-- .site-info --&gt;
   &lt;/footer&gt;&lt;!-- .site-footer --&gt;

&lt;/div&gt;&lt;!-- .site --&gt;

&lt;?php wp_footer(); ?&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

Minimal styling is needed in `style.css</code>:

<pre><code class="language-css">.footer-widget {
   margin: 2% 0;
}</code></pre>

Now, when we add a search widget to our new widget area, the front page will look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc27465e-5969-4956-aaf0-ad25b5f1a56d/11-wordpress-child-theme-custom-footer-widget-opt.jpg"><img  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef2fd3a0-6d71-4272-aea3-728840aaba9c/11-wordpress-child-theme-custom-footer-widget-opt-small.jpg" width="800" height="417" alt="Twenty Fifteen child theme custom footer widget" /></a><figcaption>Twenty Fifteen child theme custom footer widget. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc27465e-5969-4956-aaf0-ad25b5f1a56d/11-wordpress-child-theme-custom-footer-widget-opt.jpg">Large preview</a>)</figcaption></figure>

Not so hard, was it?

### Using Theme Hooks

A better way to modify a child theme via `functions.php` is to use hooks. If you have never heard of theme hooks before, think of them as little anchors in a theme’s files that allow you to add content, functions and other stuff right there, without having to edit the core files themselves.

There are two types of hooks: **action** hooks and **filter** hooks. Action hooks allow you to add custom functionality to existing functions. Filter hooks are a way to modify the functions present in the hook’s location.

Let’s go over an example to make it clearer. We will be using an action hook. Let’s go back to our last example, where we added a widget area to our theme’s footer. Instead of modifying the `footer.php` file in our child theme, we can achieve the same by using an action hook.

Let’s write a little function:

<pre><code class="language-php">function custom_footer_widget() {
   if ( is_active_sidebar( 'footer-widget' ) ) :
      dynamic_sidebar( 'footer-widget' );
   endif;
}</code></pre>

You will notice that this is essentially the same code that we pasted in `footer.php` earlier, only this time wrapped in a function (and without the opening and closing `php` tags around it, since we are pasting this in `functions.php`).

The advantage of this is that we can now add the entire function to a hook in our parent theme’s core files, without having to edit the file itself. In this case, we are targeting `twentyfifteen_credits` in the parent theme’s file. It is responsible for the footer credits (“Proudly powered by WordPress”) in the Twenty Fifteen theme, and it appears in `footer.php` like this:

<pre><code class="language-php">do_action( 'twentyfifteen_credits' );
</code></pre>

All it takes to add our new function for the widget area to this hook is one more line in the `functions.php` of our child theme:

<pre><code class="language-php">add_action( 'twentyfifteen_credits', 'custom_footer_widget' );
</code></pre>

Boom! Now, the widget area will show up in the exact same spot where we had it before, without our having to copy or add any code to the theme’s footer file. Neat, huh?

**Note:** If you are following along and are going the `functions.php` route, don’t forget to delete the modified `footer.php` file from your child theme; otherwise, the widget area will show up twice.

A lot more can be done with hooks in child themes. Some theme frameworks provide loads of hooks so that you can modify anything directly from `functions.php`.

However, that topic is beyond the scope of this article. If you are interested in learning more, some excellent resources can be found online. A good starting point is Daniel Pataki’s [A Quick and In-Depth Guide to WordPress Hooks](https://www.smashingmagazine.com/2011/10/definitive-guide-wordpress-hooks/).

{{% ad-panel-leaderboard %}}

## Summing Up

As you have hopefully seen, building a child theme in WordPress is not very complicated. All it takes is a folder plus two files.

Yet, despite its simplicity, a child theme is quite powerful. It allows us to **completely and safely customize a website** without editing any core files.

The benefits of this are numerous: You can build on top of an existing theme or framework without having to write a theme from scratch; your changes are safe from theme updates; and, if things go awry, you will always have a functioning theme to fall back on.

Plus, you are getting a top&ndash;notch education in building WordPress themes on the side. Not too bad, right?

For this reason, learning about child themes is an important step in the career of any WordPress designer or developer and for those who want more control over their WordPress websites. I hope this article helps you get started.

**What is your experience with building child themes for WordPress?** Do you have anything to add? Anything you’d do differently? Please share it in the comments.

## Customizing WordPress: You Might Be Doing It Wrong

When trying to make changes to a website, a staggering number of people opt to edit their theme directly. This means they are changing or adding files in their current theme’s folder. This creates a number of problems.

### Further Reading on Smashing Magazine:

- “[A Detailed Guide To WordPress Custom Page Templates](https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/),” Nick Schäferhoff
- “[Building A Custom Archive Page For WordPress](https://www.smashingmagazine.com/2015/04/building-custom-wordpress-archive-page/),” Karol K
- “[Extending WordPress With Custom Content Types](https://www.smashingmagazine.com/2015/04/extending-wordpress-custom-content-types/),” Brian Onorio
- “[Customizing WordPress Archives For Categories, Tags And Other Taxonomies](https://www.smashingmagazine.com/2014/08/customizing-wordpress-archives-categories-terms-taxonomies/),” Josh Pollock

{{< signature "ml, dp, al, jb, nl" >}}
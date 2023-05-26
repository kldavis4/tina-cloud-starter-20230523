---
title: 'WordPress Full-Site Editing: A Deep Dive Into The New Feature'
slug: wordpress-full-site-editing
author: nickschaeferhoff
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e92a7c2c-7748-4eb9-8ab8-6a534ad201e0/wordpress-full-site-editing.jpg
date: 2022-10-17T12:00:00.000Z
summary: >-
  In this article, Nick Schäferhoff will take a deep dive into WordPress Full-Site Editing, examine the tools it provides for theme development, and provide a tutorial on how to use it to make changes to your site.
description: >-
  In this article, Nick Schäferhoff will take a deep dive into WordPress Full-Site Editing, examine the tools it provides for theme development, and provide a tutorial on how to use it to make changes to your site.
categories:
  - WordPress
  - Tools
  - Techniques
---

Full-Site Editing is one of the main improvements added to the WordPress platform with [version 5.9](https://wordpress.org/support/wordpress-version/version-5-9/). It allows users to make sweeping changes to their website design and layout via a graphic interface, thus moving WordPress closer to the experience of a page builder. In addition, it offers new ways to create and customize themes.

These drastic changes have great consequences not only for the WordPress user experience but also for large parts of the platform’s ecosphere. For that reason, in this post, I am planning to take a deep dive into **WordPress Full-Site Editing** (or **FSE** for short, there are also [discussions about changing the name](https://make.wordpress.org/core/2022/07/27/giving-fse-a-more-user-friendly-name/) because it’s a bit of a mouthful).

In the following, I will first talk about what Full-Site Editing is and provide a tutorial on how to use it to make changes to your site. I will also examine the tools it provides for theme development and close with a discussion of how the arrival of this feature will impact developers, theme authors, and existing page-builder plugins.

**Table of Contents**

- [What Is WordPress Full-Site Editing?](#what-is-wordpress-full-site-editing)
- [How To Use Full-Site Editing To Customize WordPress](#how-to-use-full-site-editing-to-customize-wordpress)
- [Full-Site Editing for Developers And Designers](#full-site-editing-for-developers-and-designers)
- [Consequences Of Full-Site Editing For The WordPress Ecosphere](#consequences-of-full-site-editing-for-the-wordpress-ecosphere)
- [Further Resources](#full-site-editing-further-resources)
- [Final Thoughts](#final-thoughts-on-wordpress-full-site-editing)

Let’s get started.

**Quick note**: *While FSE was first added to WordPress in version 5.9, it has since been further enhanced by [WordPress 6.0](https://wordpress.org/support/wordpress-version/version-6-0/). This post includes the latest changes.*

## What Is WordPress Full-Site Editing?

In a nutshell, Full-Site Editing means that WordPress now offers the ability to create and edit page templates and elements like headers and footers in a block-based graphic user interface.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4909b291-8632-444c-a4ee-903d1445ea36/58-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4909b291-8632-444c-a4ee-903d1445ea36/58-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4909b291-8632-444c-a4ee-903d1445ea36/58-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing" >}}

This is part of phase two of the Gutenberg project and the preliminary culmination of a development that saw its beginning with the introduction of the [WordPress block editor](https://www.smashingmagazine.com/2018/08/complete-anatomy-gutenberg-wordpress-editor/) in WordPress 5.0. Since its initial release, the block workflow has branched out to other parts of the WordPress user interface. For example, you can now also use it for widget management.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57eb0d7b-ba93-4909-a4af-91eef8e1b63f/23-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57eb0d7b-ba93-4909-a4af-91eef8e1b63f/23-wordpress-full-site-editing.jpg" width="800" height="449" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57eb0d7b-ba93-4909-a4af-91eef8e1b63f/23-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of widgets page" >}}

One of the main goals of Full-Site Editing is to provide users with a singular workflow for making changes to their WordPress sites. In the past, you often needed to know several different systems to create a new menu, compose a page or post content, populate the sidebar, or adjust the color scheme. Even more complex changes required you to know [how to edit page template files](https://www.smashingmagazine.com/2015/06/wordpress-custom-page-templates/) or write CSS. With Full-Site Editing, you can now make changes to everything in pretty much the same way (even if much of it still happens in different menus).

For everyday users, the benefit is reduced dependence on front-end developers. Site owners can now do a lot by themselves that, in the past, would require technical chops or professional help, such as making changes to page templates. Plus, those changes are now visible in the editor right away instead of having to go back and forth between the front end and back end of your site or even a code file.

At the same time, Full-Site Editing makes it easier for theme developers and designers to create markup and allows for quicker templating.

### Main Features

Here are the main building blocks that Full-Site Editing consists of:

- **Page templates and template parts**  
The central attractions are two new editor interfaces that allow you to customize page layouts similar to the normal content editor. You can move page elements around, change their design (colors, fonts, alignment, and so on), and add or remove them at will. The same is also possible for single template parts such as headers and footers. It’s even possible to edit them separately. Plus, you can export your templates to use and distribute them as themes.
- **Global styles and `theme.json`**  
A common feature in WordPress page builder plugins, Full-Site Editing allows you to define global styling for your entire site, such as colors and typography, in a central place. In the past, you would have to change the styling in different locations (e.g., the Customizer and block editor). FSE also introduces the `theme.json` file, which acts as a nexus for different APIs and contains the majority of styling information in block-based themes.
- **Template blocks and block patterns**  
Full-Site Editing adds new block types to WordPress and the WordPress editor. These include static blocks like the site logo but also dynamic elements such as blocks for navigation, post titles, and featured images. These change according to settings in other places. There is even a full-fledged query block that’s basically the WordPress PHP loop. It lets you display a list of posts anywhere on the page. Each block also comes with its own design and configuration options.

Sounds exciting? Then let’s dive into how to use this new WordPress feature practically.

{{% feature-panel %}}

## How To Use Full-Site Editing To Customize WordPress

In the following, I will first go over how to take advantage of Full-Site Editing as a user. Later, we will also examine what makes this a useful feature for developers and theme designers.

### Prerequisites For Using FSE

In order to take advantage of Full-Site Editing, the most important thing is that you have a WordPress site running at least version 5.9. You can also use a lower version, but then you need to have the [Gutenberg plugin](https://wordpress.org/plugins/gutenberg/) installed and up to date.

The second thing you require is a block theme. That’s a theme that can take advantage of the new feature. We will go over how these are different from classic themes later. For now, a good option is [Twenty Twenty-Two](https://wordpress.org/themes/twentytwentytwo/), which also came out with WordPress 5.9. I will be using it for this Full-Site Editing tutorial. Refer to the resources section at the end for other options.

Finally, if you are giving WordPress Full-Site Editing a spin for the first time, I recommend using a staging site or [local development environment](https://www.smashingmagazine.com/2018/04/wordpress-local-development-beginners-setup-deployment/) for it. That way, you can make all the mistakes you want without anyone knowing.

### Overview Of The User Interface

When you are logged into your test site, you can access Full-Site Editing via ***Appearance > Editor*** (also notice that the widget and Customizer options are missing).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c63ccdd-06d2-4758-b177-c4a4e96e2b00/44-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c63ccdd-06d2-4758-b177-c4a4e96e2b00/44-wordpress-full-site-editing.jpg" width="800" height="239" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c63ccdd-06d2-4758-b177-c4a4e96e2b00/44-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of Full-Site Editing user interface" >}}

An alternative way to get there is via the ***Edit Site*** link in the WordPress admin taskbar on the front end. Either will land you on the main editor interface. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6200923d-09cf-4ff1-a1c8-07b58bf02bd7/60-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6200923d-09cf-4ff1-a1c8-07b58bf02bd7/60-wordpress-full-site-editing.jpg" width="800" height="414" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6200923d-09cf-4ff1-a1c8-07b58bf02bd7/60-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="The main editor interface" >}}

Let’s walk through all the options available here:

1. **Top left corner:** Let’s start here because it’s easy to overlook. A click on the WordPress logo opens up a menu to edit templates and template parts. It also has a link to return to the WordPress dashboard.
2. **Top bar:** This should look familiar to anyone who has used the Gutenberg editor before. It contains the option to add blocks and block patterns, toggle between editing and selecting blocks, and undo/redo buttons. You can also open a list view of the current page, select different template parts, and jump directly to them.
3. **Top right corner:** Contains the buttons to save changes and preview the design on different screen sizes. The gear icon opens up settings for templates as a whole and individual blocks. Besides, that is the option to customize Global Styles. The three-dot icon contains display options for the editor, the ability to export templates and template parts, and access to the welcome guide.
4. **Center:** In the middle is the main editing screen. Here is where you will make changes to page templates and work with blocks. It is also an accurate representation of what your design will look like and contains some controls to add blocks and other elements to the page.

Most of these are togglable, so you can only have those options open that you really need and want.

### Global Style Presets

As mentioned above, you can access this menu by clicking the half-black, half-white circle in the top right corner. It offers two types of styling options: for the entire website and for individual blocks. What exactly is available here depends on your theme.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41971280-0ee3-458c-a785-6bdcd504c6a4/6-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41971280-0ee3-458c-a785-6bdcd504c6a4/6-wordpress-full-site-editing.png" width="800" height="539" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41971280-0ee3-458c-a785-6bdcd504c6a4/6-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing menu" >}}

For Twenty Twenty-Two, you have options for typography, colors, and layout. We will get to those below. For now, let’s turn to the most exciting part of the Global Styles menu &mdash; the preset color themes. You can find them when you click on ***Browse styles***.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d31581b2-88ca-4442-ac1c-19961e273ed6/19-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d31581b2-88ca-4442-ac1c-19961e273ed6/19-wordpress-full-site-editing.png" width="800" height="535" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d31581b2-88ca-4442-ac1c-19961e273ed6/19-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing color themes" >}}

In this menu, developers have the possibility to offer styling presets for the entire theme. Hover over one of the options to see a preview of its color and font scheme, and then adopt the look for your entire theme with a single click.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c861bfc7-9610-46e9-8b33-0c99f9b35576/64-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c861bfc7-9610-46e9-8b33-0c99f9b35576/64-wordpress-full-site-editing.jpg" width="800" height="419" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c861bfc7-9610-46e9-8b33-0c99f9b35576/64-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing color themes preview" >}}

I really like this feature as it offers users different versions of the same theme that they can easily use as jump-off points for their own creations. It’s a bit like themes shipping together with a number of their own [child themes](https://www.smashingmagazine.com/2016/01/create-customize-wordpress-child-theme/). You can also go back to the previous state by clicking the three dots at the top and choosing ***Reset to defaults***.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/997dfd9d-15a7-4737-8379-a0a2fc9967e2/54-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/997dfd9d-15a7-4737-8379-a0a2fc9967e2/54-wordpress-full-site-editing.png" width="800" height="538" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/997dfd9d-15a7-4737-8379-a0a2fc9967e2/54-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing color themes" >}}

### Global Styles: Typography

When you click on ***Typography***, you get to a submenu where you can choose whether to customize the styling for general text or links.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ee1f896-eb04-491b-a573-aec0e9146193/43-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ee1f896-eb04-491b-a573-aec0e9146193/43-wordpress-full-site-editing.png" width="800" height="538" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ee1f896-eb04-491b-a573-aec0e9146193/43-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing typography" >}}

Another click gets you to a subsection where you can make the actual changes.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8714915f-e8d7-436c-b5a6-d80c40c184a2/55-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8714915f-e8d7-436c-b5a6-d80c40c184a2/55-wordpress-full-site-editing.png" width="800" height="550" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8714915f-e8d7-436c-b5a6-d80c40c184a2/55-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing typography" >}}

As you can see, it’s possible to customize the font family, size, line height, and appearance, meaning font-weight and slant. Options here depend on the theme as well. For example, under ***Font family***, you can only choose ***System Font*** and ***Source Serif Pro*** as these are the only options Twenty Twenty-Two ships with.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/518d8982-a6f8-49dc-b0ee-87413de23659/16-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/518d8982-a6f8-49dc-b0ee-87413de23659/16-wordpress-full-site-editing.png" width="800" height="557" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/518d8982-a6f8-49dc-b0ee-87413de23659/16-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing typography" >}}

However, this is also due to the fact that full support for (local) web fonts only became available in WordPress 6.0, and this theme came out before that.

Likewise, the numbers under ***Size*** represent defaults set by the theme authors. You also have the option to click on the little icon in the upper right corner to set a custom value.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8493b12a-23d9-45a0-a2a3-b0f55712769f/7-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8493b12a-23d9-45a0-a2a3-b0f55712769f/7-wordpress-full-site-editing.png" width="800" height="548" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8493b12a-23d9-45a0-a2a3-b0f55712769f/7-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing typography" >}}

***Line height*** should be self-explanatory. The ***Appearance*** drop-down menu lets you choose font variations from a list.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99a9ed3e-ef5d-4c77-8806-bac8baeb4232/48-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99a9ed3e-ef5d-4c77-8806-bac8baeb4232/48-wordpress-full-site-editing.png" width="800" height="554" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99a9ed3e-ef5d-4c77-8806-bac8baeb4232/48-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing typography" >}}

If you pick any of these options, changes will automatically become visible on the editing screen.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf204293-1392-487e-a6ea-cb2781daf0f0/45-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf204293-1392-487e-a6ea-cb2781daf0f0/45-wordpress-full-site-editing.jpg" width="800" height="459" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf204293-1392-487e-a6ea-cb2781daf0f0/45-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing typography" >}}

If you don’t like the modifications you have made, you can always reset to defaults, as mentioned above.

### Global Colors And Layout

Under ***Colors***, you can change the hue of different elements (duh!).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6940e4d3-5cd4-4f0e-bd6d-da7f63039230/10-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6940e4d3-5cd4-4f0e-bd6d-da7f63039230/10-wordpress-full-site-editing.png" width="800" height="562" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6940e4d3-5cd4-4f0e-bd6d-da7f63039230/10-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing color palette" >}}

What’s interesting here is the ***Palette*** option, where the theme can provide its own color palette, including gradients. This is besides the default options Gutenberg offers and custom colors that users can create.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05f70897-f972-4e98-990c-20b6065d33ab/3-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05f70897-f972-4e98-990c-20b6065d33ab/3-wordpress-full-site-editing.png" width="800" height="567" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05f70897-f972-4e98-990c-20b6065d33ab/3-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing color palette" >}}

Besides that, just like for typography, the theme provides different options for elements for which you can change colors. In Twenty Twenty-Two, that’s ***Background***, ***Text***, and ***Links***.

After choosing any of these, you get to a screen where you can easily pick a color or gradient from available options or create your own. When you do, your pick automatically translates to what you see on the editing screen.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b4130d-de51-447d-8a4b-9c444b5cc63e/63-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b4130d-de51-447d-8a4b-9c444b5cc63e/63-wordpress-full-site-editing.jpg" width="800" height="459" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b4130d-de51-447d-8a4b-9c444b5cc63e/63-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing background color" >}}

There is even a color picker that lets you set custom hues or enter color codes in RGB, HSL, or HEX format.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52a1ea42-5a43-47d2-b525-fc84228e4d0c/62-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52a1ea42-5a43-47d2-b525-fc84228e4d0c/62-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52a1ea42-5a43-47d2-b525-fc84228e4d0c/62-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing background color" >}}

Finally, in this theme, the ***Layout*** option only allows you to add padding around the homepage.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1372202-d0ab-4628-a92d-0bd23bb16218/25-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1372202-d0ab-4628-a92d-0bd23bb16218/25-wordpress-full-site-editing.jpg" width="800" height="459" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1372202-d0ab-4628-a92d-0bd23bb16218/25-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of WordPress Full-Site Editing layout option" >}}

### Changing Styles For Individual Blocks

Styling defaults are not only available for the website as a whole, but you can also set them for individual blocks. For that, you find an option in Global Styles at the bottom where it says ***Blocks***.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8792f474-3a02-43e9-923e-ec260e555fe6/14-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8792f474-3a02-43e9-923e-ec260e555fe6/14-wordpress-full-site-editing.png" width="800" height="535" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8792f474-3a02-43e9-923e-ec260e555fe6/14-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of styling blocks option in WordPress Full-Site Editing" >}}

When you click it, you find a list of all the WordPress default blocks.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e37aace-e0d1-479c-931e-c13255aa2327/35-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e37aace-e0d1-479c-931e-c13255aa2327/35-wordpress-full-site-editing.png" width="800" height="541" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e37aace-e0d1-479c-931e-c13255aa2327/35-wordpress-full-site-editing.png'>Large preview</a>)" alt="A list of all the WordPress default blocks" >}}

Click those in turn to find similar options to customize their design on a per-block basis. For example, below, I have set the link color globally to blue but set the color for the ***Post Title*** block (which is also a link) to orange. As a consequence, orange overwrites the initial value, and the title comes out in that color.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2af2285d-c09a-4f2c-bfc7-8a68a86bcf34/37-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2af2285d-c09a-4f2c-bfc7-8a68a86bcf34/37-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2af2285d-c09a-4f2c-bfc7-8a68a86bcf34/37-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of different links color options" >}}

If you have ever worked with CSS, this principle should be very familiar. Set some site-wide standards at the top of the style sheet and then overwrite them with customizations further down in the [cascade](https://www.smashingmagazine.com/2022/01/introduction-css-cascade-layers/). It’s the same thing here.

### Moving Blocks Around

Making layout changes works the same way as in the main WordPress block editor. Everything you see on the screen is made up of blocks. Some may be combined as groups or block patterns, but they are blocks nevertheless.

As such, you can move and customize them however you want. For example, the main part of the homepage is the ***Query Loop*** block, whose function is to serve up the latest blog posts. However, it, too, is made up of different blocks, namely ***Post Title***, ***Post Featured Image***, ***Post Excerpt***, ***Post Date***, ***Spacer***, and ***Pagination***.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33eef055-92e6-4185-95fc-ff5da40bb52d/38-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33eef055-92e6-4185-95fc-ff5da40bb52d/38-wordpress-full-site-editing.jpg" width="800" height="446" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33eef055-92e6-4185-95fc-ff5da40bb52d/38-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the Query Loop block" >}}

If you want to change something about the way it looks, you can very easily do so. For example, you may click on the ***Post Featured Image*** block and then use the arrows in the toolbar to move it below or above the post title.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73b828d0-3e64-4c33-b8be-bf9c2caad832/46-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73b828d0-3e64-4c33-b8be-bf9c2caad832/46-wordpress-full-site-editing.jpg" width="800" height="446" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73b828d0-3e64-4c33-b8be-bf9c2caad832/46-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the Post Featured Image block" >}}

Alternatively, hover over the block and then use the <kbd>Drag</kbd> button (which looks like six dots) to move it to another position. If you hit <kbd>Save</kbd> after this, it will translate to the design on your site.

### Using Block Options

In addition to the ability to move them around, every block also comes with its own settings. Like in the Gutenberg content editor, you can access those via the gear icon in the upper right corner. When a block is selected, you will see its customization options there.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d07c2e-8013-4f7c-bf06-33cf30aa5918/30-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d07c2e-8013-4f7c-bf06-33cf30aa5918/30-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30d07c2e-8013-4f7c-bf06-33cf30aa5918/30-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of block settings" >}}

What’s available in this place depends on the block you are working with. For example:

- **Post Featured Image**: Has options to add the margin, padding, and configure image dimensions.
- **Pagination**: Control the justification and orientation of its elements, wrapping, colors, and whether to show arrows, chevrons, or nothing as indicators.
- **Post Title**: Besides setting colors, you can decide if the title should be a link, open in a new tab, or have a `rel=` attribute. You can also control colors and typography (including the ability to use ***Title Case***) and add a margin.

You get the gist. Be aware that there are often more settings hidden that you can access via a plus or three-dot icon within the sections.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05d03f1f-99f3-40fe-a8a1-218fd4ad8aae/42-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05d03f1f-99f3-40fe-a8a1-218fd4ad8aae/42-wordpress-full-site-editing.png" width="800" height="536" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05d03f1f-99f3-40fe-a8a1-218fd4ad8aae/42-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of hidden block settings" >}}

In addition, there are settings in the toolbar atop blocks when they are selected. You should not forget those as they can be decisive. For example, in the case of the ***Post Title*** block, it’s where you determine what order of heading (h1-h6) it takes, an important factor for [SEO](https://www.smashingmagazine.com/smashing-guide-search-engine-optimization/).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1520811-c801-48fc-ae90-b92a7890cc23/18-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1520811-c801-48fc-ae90-b92a7890cc23/18-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1520811-c801-48fc-ae90-b92a7890cc23/18-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of block settings in the toolbar" >}}

### Adding And Removing Blocks

Of course, you can not just customize the available blocks, but you are also able to add your own. This works the same way as in the content editor and comes with different options:

1. Hover over an empty space in the template until a plus button appears, and click it. Then search or choose what you want from a list of blocks.
2. Click existing blocks and use the options button in the top bar to pick ***Insert before*** and ***Insert after***.
3. Use the plus button in the upper left corner to see and search the full list of available blocks, then drag and drop them where you want.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb248392-5941-4973-a976-12754cadaccc/47-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb248392-5941-4973-a976-12754cadaccc/47-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb248392-5941-4973-a976-12754cadaccc/47-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="Adding and removing blocks option" >}}

In some places and existing blocks, you will also find icons to add more blocks. Plus, you have the ability to add block patterns, but we will talk about this further below.

Leaves the question, how is any of this helpful?

Well, it means you can easily add both static and dynamic content to the homepage. An example would be a heading and paragraph above the ***Query Loop*** block as an introduction to your blog.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cae44414-06bb-490c-a884-21f23c777962/34-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cae44414-06bb-490c-a884-21f23c777962/34-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cae44414-06bb-490c-a884-21f23c777962/34-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of a heading and paragraph above the Query Loop block" >}}

Naturally, you can also remove blocks you don’t want just as easily. Simply select one and hit the <kbd>Del</kbd> or <kbd>backspace</kbd> button on your keyboard, or remove it via the block options.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8035323-7def-4f02-ba5f-9dc7a2226a37/5-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8035323-7def-4f02-ba5f-9dc7a2226a37/5-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8035323-7def-4f02-ba5f-9dc7a2226a37/5-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the remove blocks option" >}}

You also have the ability to open a list view at the top (the icon with three staggered lines) and navigate to blocks from there or choose to delete them right away.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4a382fa-065d-4658-88ce-bf8d8e125667/4-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4a382fa-065d-4658-88ce-bf8d8e125667/4-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4a382fa-065d-4658-88ce-bf8d8e125667/4-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of how to delete blocks" >}}

This option also gives you a great overview of the block structure of whatever part of the site you are currently editing.

### Exchanging And Editing Template Parts

Template parts are entire sections inside templates that you can exchange as a whole and modify separately. In the case of Twenty Twenty-Two, that is the header and footer. You can see this in the template options on the right or when you click the arrow in the top bar.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/515f77d2-b3c0-4775-8b38-df8f2c70951c/27-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/515f77d2-b3c0-4775-8b38-df8f2c70951c/27-wordpress-full-site-editing.jpg" width="800" height="307" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/515f77d2-b3c0-4775-8b38-df8f2c70951c/27-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of template parts" >}}

Template parts are just groups of blocks on the page, so you can edit them as described above. However, what’s special about them is that themes can offer variations that allow you to change the entire part with one click.

For example, when you select the header in the example, it will show a ***Replace*** option in the settings bar at the bottom.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3c92ade-7566-43b3-8e5f-7a988ab2c828/33-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3c92ade-7566-43b3-8e5f-7a988ab2c828/33-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3c92ade-7566-43b3-8e5f-7a988ab2c828/33-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of a Replace option" >}}

When you click it, you can see the variations the theme offers for this template part, as well as fitting block patterns.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f8db23-1200-4e14-b645-2913f4a67ce3/53-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f8db23-1200-4e14-b645-2913f4a67ce3/53-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f8db23-1200-4e14-b645-2913f4a67ce3/53-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the theme offers for the template part" >}}

Twenty Twenty-Two has several default options to choose from. Click any of them, and Full-Site Editing will automatically replace the entire header with the new option.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2300801f-dde4-4cf8-82d8-6c3aed0ffe76/21-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2300801f-dde4-4cf8-82d8-6c3aed0ffe76/21-wordpress-full-site-editing.jpg" width="800" height="569" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2300801f-dde4-4cf8-82d8-6c3aed0ffe76/21-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of templates for headers" >}}

The same works for the footer, of which Twenty Twenty-Two also has a few to offer.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20842738-183d-40f6-a90d-cd99753d5791/17-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20842738-183d-40f6-a90d-cd99753d5791/17-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20842738-183d-40f6-a90d-cd99753d5791/17-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of templates for footers" >}}

### Customizing And Creating Template Parts

To edit template parts separately, click on the WordPress logo in the upper left corner to open the following menu.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82bbaf4b-3cc1-4f19-9a77-50529d31a3a8/13-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82bbaf4b-3cc1-4f19-9a77-50529d31a3a8/13-wordpress-full-site-editing.jpg" width="800" height="461" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82bbaf4b-3cc1-4f19-9a77-50529d31a3a8/13-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of how to edit template parts separately" >}}

At the bottom, you will find a menu item called ***Template Parts***. Click it to see a list of all available template parts on your site.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5aebea1-6e4e-46bb-b25a-aab9811ff2ac/15-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5aebea1-6e4e-46bb-b25a-aab9811ff2ac/15-wordpress-full-site-editing.jpg" width="800" height="461" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5aebea1-6e4e-46bb-b25a-aab9811ff2ac/15-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of available template parts" >}}

Alternatively, you can also select a template part and choose to edit it from its options.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d4a7094-8932-4b7f-9fd8-e494822ac855/26-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d4a7094-8932-4b7f-9fd8-e494822ac855/26-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d4a7094-8932-4b7f-9fd8-e494822ac855/26-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of how to edit a template part" >}}

In the ***Template Parts*** menu, click ***Add New*** in the upper right corner to create additional ones. This is useful if you want to make another version of the footer, for example. The cool thing is when you click it, besides asking for a name, WordPress automatically gives you templates for both header and footer, so you don't have to start from scratch (unless you want to).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fcc71ff-d844-42e2-b8b7-3d68af957755/40-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fcc71ff-d844-42e2-b8b7-3d68af957755/40-wordpress-full-site-editing.jpg" width="800" height="480" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fcc71ff-d844-42e2-b8b7-3d68af957755/40-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of how to create a new template part" >}}

Besides that, you may also just click on existing parts in the list to edit them. This works the same way as in the main editor. The only thing that is different for template parts is that you have handles on the left and right that you can use to shrink and expand the size in order to check its behavior on smaller screens, i.e., mobile devices.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e8ed588-8e71-422d-bda3-229684243527/39-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e8ed588-8e71-422d-bda3-229684243527/39-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e8ed588-8e71-422d-bda3-229684243527/39-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of how to edit template parts" >}}

Just like a template file, anything you change and save here will translate to all pages and templates that use this part.

Finally, if you have set up a group of blocks on the main screen, you can turn them into a template part as well. Click the options in the main screen or in the list view and pick ***Make template part***.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f6656e-1408-4409-8307-fff8fa91e301/51-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f6656e-1408-4409-8307-fff8fa91e301/51-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8f6656e-1408-4409-8307-fff8fa91e301/51-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of how to make a template part" >}}

You need to give it a name and choose what area it belongs to. When you then save it, it is available as a template part.

### Editing Page Templates

In the WordPress logo menu, there is also an item called ***Templates***. Unsurprisingly, it contains a list of all page templates available on your site, from the 404-page over archives and single pages to single posts.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d08f215-4cbe-465c-9ec5-a92c2463877d/49-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d08f215-4cbe-465c-9ec5-a92c2463877d/49-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d08f215-4cbe-465c-9ec5-a92c2463877d/49-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of templates item on the WordPress logo menu" >}}

Page templates are usually files that control the basic layout of different types of content. If you change the template, all content of that type changes, too. With Full-Site Editing, you can edit existing templates and create your own in the user interface instead of a code editor.

Note, however, that FSE only lets you create standard page templates via ***Add New***. More on that soon.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/229c6e85-3aa2-48a1-960e-849163e99c5d/24-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/229c6e85-3aa2-48a1-960e-849163e99c5d/24-wordpress-full-site-editing.png" width="800" height="536" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/229c6e85-3aa2-48a1-960e-849163e99c5d/24-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of how to create a new page template" >}}

Something that comes especially handy here (and also for template parts) is block patterns. These are predesigned layouts consisting of several blocks you can add to website pages to instantly create entire sections. Examples include newsletter sign-up forms, pricing tables, and event lists, but also simple things like a styled divider or an image with a quote or caption.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1691d53-95e5-463d-bdae-711b00b4b941/57-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1691d53-95e5-463d-bdae-711b00b4b941/57-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1691d53-95e5-463d-bdae-711b00b4b941/57-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of a block pattern example" >}}

Patterns allow you to put together entire designs quickly. They are easy to use, too! When editing a template, simply click the plus symbol in the upper left and go to the ***Patterns*** tab.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be39afa1-e279-47a6-8cf4-60a2bda5ca74/41-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be39afa1-e279-47a6-8cf4-60a2bda5ca74/41-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be39afa1-e279-47a6-8cf4-60a2bda5ca74/41-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of patterns tab for templates" >}}

Filter the patterns via the drop-down menu at the top, e.g., by featured patterns, footers, pages, or buttons. If you find something you like, simply drag and drop it on the page. You can also search for something specific, like a “header” at the top, which will even show blocks from the [WordPress block directory](https://wordpress.org/support/article/block-directory/).

For a better overview, it helps to click on ***Explore*** to access the block pattern explorer.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1be62dac-758e-43a7-8562-ad7dbbb098d8/52-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1be62dac-758e-43a7-8562-ad7dbbb098d8/52-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1be62dac-758e-43a7-8562-ad7dbbb098d8/52-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of featured patterns" >}}

This shows the block patterns in a larger window with the ability to search and filter them on the left. A click on a pattern you like automatically adds it to the template editor, where you can position and customize it as usual.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6dd1947-d6c5-415c-ac17-2db2685e5458/22-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6dd1947-d6c5-415c-ac17-2db2685e5458/22-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6dd1947-d6c5-415c-ac17-2db2685e5458/22-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the template editor" >}}

By the way, you can clear all customizations you have made for individual templates by clicking the three-dot icon in the ***Template*** menu and choosing so.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/985fa90e-5948-47de-9dbe-f7f3ed9b259c/2-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/985fa90e-5948-47de-9dbe-f7f3ed9b259c/2-wordpress-full-site-editing.jpg" width="800" height="320" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/985fa90e-5948-47de-9dbe-f7f3ed9b259c/2-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of how to clear customizations" >}}

### Adding New Block Patterns

Besides using what’s available, you also can add external block patterns from the [pattern directory](https://wordpress.org/patterns/). 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9580619-f362-4b41-a68d-ede4426609f0/31-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9580619-f362-4b41-a68d-ede4426609f0/31-wordpress-full-site-editing.jpg" width="800" height="666" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9580619-f362-4b41-a68d-ede4426609f0/31-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the pattern directory" >}}

Search and filter to your needs. If you find something you like, simply use the <kbd>Copy Pattern</kbd> button on the pattern page to get it on your site.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/768ec223-89e2-47ed-aa32-ec58376269d6/20-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/768ec223-89e2-47ed-aa32-ec58376269d6/20-wordpress-full-site-editing.jpg" width="800" height="638" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/768ec223-89e2-47ed-aa32-ec58376269d6/20-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of a Copy Pattern button on the pattern page" >}}

After that, go back to the Full-Site Editing editor and paste it. The pattern will then show up there.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48a6ca6-b880-42ce-98d6-39216d52571e/32-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48a6ca6-b880-42ce-98d6-39216d52571e/32-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c48a6ca6-b880-42ce-98d6-39216d52571e/32-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of a new pattern in the Full-Site Editing editor" >}}

If you like it and likely want to use it again, click the three dots in the options bar and choose ***Add to Reusable blocks***.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32a6744c-0dde-4b9b-8afd-521212b701fa/56-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32a6744c-0dde-4b9b-8afd-521212b701fa/56-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32a6744c-0dde-4b9b-8afd-521212b701fa/56-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the 'Add to Reusable blocks' option" >}}

That way, it will, from now on, be available in the block menu under ***Reusable***.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40582956-ae89-4e1f-a659-480033930e31/9-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40582956-ae89-4e1f-a659-480033930e31/9-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40582956-ae89-4e1f-a659-480033930e31/9-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the 'reusable' item in the block menu" >}}

### Using The Standalone Templates Editor

There is a second way to edit and create page templates, which happens in the normal Gutenberg content editor. It offers less complexity than the site editor interface (e.g., no access to other templates) but works similarly.

Simply create a new post or page, then, in the document settings sidebar, locate the ***Template*** panel below ***Status & visibility***.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c517526f-5b69-4f63-bf8a-f30c50645c47/1-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c517526f-5b69-4f63-bf8a-f30c50645c47/1-wordpress-full-site-editing.jpg" width="800" height="431" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c517526f-5b69-4f63-bf8a-f30c50645c47/1-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the standalone templates editor" >}}

Here, it lists your current template and makes other options available in the drop-down menu. You can edit what’s already there via the ***Edit*** button or create a new template by selecting ***New***. Each opens the more limited template editing experience.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23e920c0-a48c-4be4-b33b-4a643eec8bee/11-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23e920c0-a48c-4be4-b33b-4a643eec8bee/11-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23e920c0-a48c-4be4-b33b-4a643eec8bee/11-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the drop-down menu for editing or adding new templates" >}}

Edit and save the template in the same way as in the site editor. Anything you create this way will also show up in the list of templates in the Full-Site Editing editor.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5549ef0-e1d2-404e-b629-17afb0d21280/65-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5549ef0-e1d2-404e-b629-17afb0d21280/65-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5549ef0-e1d2-404e-b629-17afb0d21280/65-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the list of templates in the Full-Site Editing editor" >}}

### Available Blocks For Templating

To make templating in FSE possible, the developers have added a number of dynamic blocks that can pull content from the database depending on the following:

- Site title, tagline, and logo;
- Post title, featured image, content, excerpt, author, avatar, author biography, date, tags, categories, next and previous post, read more;
- Post comments, single comment, comments query loop, author, date, content, count, comment form, and link;
- Archive title and term description;
- Query loop, post list, post template, pagination;
- Template part.

These are also available in the normal WordPress editor. There are more to come in future versions, and you can get early access to them via the Gutenberg plugin.

### Preview And Save Changes

When you have made all the changes you want, you have the option to preview them in different screen sizes by clicking ***Preview*** in the upper right corner.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f0013de-7ae8-4081-b66e-94b33c49fd91/8-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f0013de-7ae8-4081-b66e-94b33c49fd91/8-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f0013de-7ae8-4081-b66e-94b33c49fd91/8-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the Preview option" >}}

If you are satisfied, a click on <kbd>Save</kbd> will make the modifications permanent. WordPress will also list which templates and template parts your changes will affect.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce0fb1f4-2830-4001-a15d-6dec239d44f3/36-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce0fb1f4-2830-4001-a15d-6dec239d44f3/36-wordpress-full-site-editing.png" width="800" height="539" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce0fb1f4-2830-4001-a15d-6dec239d44f3/36-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of the Save button for saving changes in templates and template parts" >}}

That way, if you want to discard them in one place but keep them elsewhere, you can do so. Simply uncheck those components where you don’t want to save your changes. Click <kbd>Save</kbd> again, and your choices will translate to the front end of your site.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4562e844-9196-4be3-98cc-cf7885cf9680/61-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4562e844-9196-4be3-98cc-cf7885cf9680/61-wordpress-full-site-editing.png" width="800" height="531" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4562e844-9196-4be3-98cc-cf7885cf9680/61-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of a template" >}}

{{% ad-panel-leaderboard %}}

## Full-Site Editing For Developers And Designers

Full-Site Editing is also a useful tool for developers. You can use the interface to create templates and then export them as files to add to and publish as themes.

### A Quick Primer On Block Theme Architecture

To take advantage of this, you need to be aware that FSE-ready block themes have a different architecture than classic WordPress themes. For one, the template and template-part files for Full-Site Editing no longer contain PHP but are HTML files with block markup.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a51ac91c-0739-4544-bb05-797fd4d457cc/28-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a51ac91c-0739-4544-bb05-797fd4d457cc/28-wordpress-full-site-editing.jpg" width="800" height="429" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a51ac91c-0739-4544-bb05-797fd4d457cc/28-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of Block Theme Architecture" >}}

Instead of `style.css`, styling is mostly taken over by `theme.json`. Here is where you set up styles for the block editor and individual blocks, styling presets, as well as CSS defaults (both for the front-end and backend editor). In fact, `theme.json` is so powerful that, by modifying it, you can change the style of an entire website. 

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Last week I created a quick demo of how the visual aesthetic of Twenty Twenty-Two can be drastically changed through its theme.json settings. This example swaps the default json file for one with different font, color, duotone, and spacing values. <a href="https://t.co/ab9tyGwLOS">pic.twitter.com/ab9tyGwLOS</a></p>&mdash; kjellr (@kjellr) <a href="https://twitter.com/kjellr/status/1451536195616395272?ref_src=twsrc%5Etfw">October 22, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This also allows you to switch between different sets of global styles (i.e., `theme.json` files) in the same theme. It’s a feature that only arrived in WordPress 6.0.

Relying mostly on `theme.json` greatly reduces CSS in other places. For example, Twenty Twenty-Two’s `style.css` is only 148 lines long. For comparison, its predecessor Twenty Twenty-One has almost 6,000 lines in its style sheet.

In addition, `theme.json` uses a whole different kind of markup. Yet, you could write an entire article just on this one file, so you are better served to start with the [documentation](https://developer.wordpress.org/block-editor/how-to-guides/themes/theme-json/) for details. 

The minimum requirements for a block theme are to have an `index.php`, `style.css`, and an `index.html` file in a ***templates*** folder. The latter is what marks the theme as a block theme to WordPress.

If you want to add template parts, you will place those in a ***parts*** folder. Having a `functions.php` and `theme.json` files is optional. Finally, you can also include a ***styles*** folder for global style presets. For example, this can include different color schemes for the theme.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/939b4152-5f64-4942-b7fc-8d29991fd802/29-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/939b4152-5f64-4942-b7fc-8d29991fd802/29-wordpress-full-site-editing.png" width="800" height="517" sizes="100vw" caption="Source: <a href='https://developer.wordpress.org/themes/block-themes/block-theme-setup/'>developer.wordpress.org</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/939b4152-5f64-4942-b7fc-8d29991fd802/29-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of the Block theme setup" >}}

Besides the changed structure, you also have different ways of creating template files when using a block theme. While you can still do it manually, using the new WordPress interface is also possible.

### Using FSE Or The Template Editor To Create Theme Files

If you want to use the page editors to create templates, the first step is to simply set up your templates as described in the first part of this article. One important option here is to know that you can use the ***Advanced*** settings for template-part blocks to change their type of HTML element.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5020bdd0-26ff-413b-9e1e-488b9ea6b9c3/59-wordpress-full-site-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5020bdd0-26ff-413b-9e1e-488b9ea6b9c3/59-wordpress-full-site-editing.png" width="800" height="534" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5020bdd0-26ff-413b-9e1e-488b9ea6b9c3/59-wordpress-full-site-editing.png'>Large preview</a>)" alt="A screenshot of how to change the type of HTML element for template-part blocks" >}}

When satisfied, you can download all your theme files at once. The option for that is available in the ***More tools & options*** menu, which you access by clicking the three dots in the upper right corner of the Full-Site Editing screen.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f407e26b-a352-4265-b476-74e0655763d8/50-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f407e26b-a352-4265-b476-74e0655763d8/50-wordpress-full-site-editing.jpg" width="800" height="413" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f407e26b-a352-4265-b476-74e0655763d8/50-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the export option to download theme files" >}}

Here, locate the ***Export*** option. It will automatically download all template and template part files as a zip. Simply unpack them, and you can use them for your theme.

### Manually Creating Block Theme Templates

Of course, it’s also possible to create template files by hand. For that, you just need to be familiar with block markup.

For the most part, these are just HTML comments that contain the name of a block prepended with `wp:`. Some of them are self-containing. For example, here’s how to add a site-title block to the template:

<pre><code class="language-html">&lt;!-- wp:site-title /--&gt;
</code></pre>

Others, like paragraphs, function like brackets:

<pre><code class="language-html">&lt;!-- wp:paragraph --&gt;
&lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipiscing elit.&lt;/p&gt;
&lt;!-- /wp:paragraph --&gt;
</code></pre>

You can also call template parts by stating the file name via `slug`. Here’s how to call `footer.html`:

<pre><code class="language-html">&lt;!-- wp:template-part {"slug":"footer"} /--&gt;
</code></pre>

You can even customize the HTML tag (default: `div`) via the `tagName` attribute:

<pre><code class="language-html">&lt;!-- wp:group {"tagName":"main"} --&gt;

&lt;!-- /wp:group --&gt;
</code></pre>

Here, too, it’s possible to use one of the editors above to create blocks and then simply copy the markup over if you are not sure. Plus, if you save a file and then add it to the respective location in the theme directory, it will also show up in the FSE editor.

For more details, refer to the resource list below.

## Consequences Of Full-Site Editing For The WordPress Ecosphere

Besides providing a tutorial on how to use Full-Site Editing, I also want to talk about what its arrival means for the WordPress environment and those working there.

### Job Opportunities For Developers And Designers

As is to be expected, an important question is whether this kind of feature will eliminate the need for professional developers and designers. Are they still needed when users can seemingly do everything themselves?

The short answer is “yes.”

Neither the emergence of WordPress itself nor page builders or page builder plugins, or any other technology that makes it easier for laypeople to build their own websites have eradicated the need for professional help. And it won’t happen this time, either.

While these days, users don’t need help for every little thing (like changing colors or fonts), there are still lots of tasks that non-technical site owners simply can not do with the available tools and where they need someone to do it for them. Plus, if you want a unique design and not rely on a template that hundreds or thousands of other people might also be using, you still need a designer and/or developer.

Plus, with great power also comes a great opportunity to screw things up (to loosely quote Spiderman). Just because everyone has the tools at their disposal to make a well-designed website, that doesn’t mean everyone can. Design is more than mere technical ability.

What’s more, not everyone actually wants to do the work. They’d rather hire someone with the skills than acquire them from scratch. Finally, there is so much more to a successful website than “just” design, such as SEO, performance, security, and maintenance.

So, even if there are fewer obstacles to building websites, there is no need to think that designers and developers are a dying breed. In contrast, the switch to new tools offers plenty of opportunities to build services and products around them.

### What Does FSE Mean For The Theme Market And Theme Designers?

So what about theme creators? Does everyone have to switch to block themes now?

Here, it’s first important to keep in mind that many themes have not yet switched to the Gutenberg block editor and that there are still many users on the Classic Editor. The latter will also continue to work for a while as the plugin will still be supported until [at least the end of 2022](https://wptavern.com/wordpress-classic-editor-support-extended-for-at-least-another-year).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f494e0a4-4b48-4287-b93c-5c23f96c5d31/12-wordpress-full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f494e0a4-4b48-4287-b93c-5c23f96c5d31/12-wordpress-full-site-editing.jpg" width="800" height="419" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f494e0a4-4b48-4287-b93c-5c23f96c5d31/12-wordpress-full-site-editing.jpg'>Large preview</a>)" alt="A screenshot of the article with the title 'WordPress classic editor support extended for at least another year'" >}}

Also, all of the features described above are optional, not mandatory. Therefore, the switch does not have to be immediate. You can even build hybrid themes that are not complete block themes but are able to use block templates. This option exists by default unless you specifically [switch it off](https://developer.wordpress.org/block-editor/how-to-guides/themes/block-theme-overview/#classic-themes).

Nevertheless, in the long run, it’s probably a good idea to move your existing themes over to FSE capabilities. It’s something that WordPress users will likely grow to expect as it gives them more flexibility and power to customize themes on their own.

At the same time, as described above, you can also use Full-Site Editing to create themes with less coding, which can speed up development time. Plus, it offers new economic opportunities. Besides themes, theme authors can now offer extensions like blocks and block patterns, opening up whole new business models and opportunities.

### Full-Site Editing vs. Page Builder Plugins

The existing page builder plugins are probably one of the biggest question marks. Will the likes of Divi, Elementor, and Co survive when WordPress can do a lot of what they were created to provide?

First of all, it’s unlikely that everyone will immediately switch away from the tools they are used to working with, so page builder plugins will likely stay around for a while. Also, many of them are currently more powerful than what Full-Site Editing is capable of in its present form. Another reason to stay with what you have.

Overall, these types of plugins have become very established over the last years, to the point that they sometimes ship packaged with themes. For that reason, it’s improbable that they will suddenly lose all their market share. Despite that, Full-Site Editing will likely eat into it over time, especially with new users who get to know it as a normal part of WordPress.

Just like everyone else, page builder plugins will have to evolve so that they offer things that FSE doesn’t to stay competitive. One way would be to offer kind of hybrid plugins that extend WordPress’ native page editor. Similar things already exist for Gutenberg and for the Classic Editor.

### Full-Site Editing: Further Resources

If you want to get even deeper into the topic of WordPress Full-Site Editing, I recommend you start with these resources:

- [Block Editor Handbook](https://developer.wordpress.org/block-editor/)  
The Block Editor Handbook is generally a good place to start for anything related to the Gutenberg editor and project. Don’t miss the primer on block themes, how they work, and how to create them in the [Theme Developer Handbook](https://developer.wordpress.org/themes/block-themes/).
- [Fullsiteediting.com](https://fullsiteediting.com/)  
A dedicated resource site and free online course for FSE created by [Carolina Nymark](https://twitter.com/carolinapoena). It has chapters on every part of Full-Site Editing, from basics over how to use `theme.json` to even a [starter block theme generator](https://fullsiteediting.com/block-theme-generator/). Plus, it has a list of [available block themes](https://fullsiteediting.com/themes/).
- [WordPress Theme Directory: Block Themes](https://wordpress.org/themes/tags/full-site-editing/)  
Speaking of block themes, the official WordPress directory now has a tag for themes compatible with Full-Site Editing. This way, you can easily find some to give the feature a spin. More are being added all the time.

{{% ad-panel-leaderboard %}}

## Final Thoughts On WordPress Full-Site Editing

Full-Site Editing is an exciting new chapter in the evolution of WordPress. It makes the design process easier and more uniform across the entire platform, offering new opportunities for content creators and users to customize their pages.

At the same time, FSE comes with interesting challenges for developers and theme designers. It changes the architecture of themes as well as introduces new markups and workflows. However, the feature also offers rewards in terms of new opportunities and a faster way for prototyping and creating themes that require less coding.

Above, we have gone over everything FSE has to offer in detail. My personal impression is that it is a well-thought-out feature, and I am impressed by how much it can already do. I’d definitely recommend adding it to your [WordPress skill set](https://nickschaeferhoff.com/wordpress-skills/).

Sure, there is room for improvement. For example, I could not find an option to change the hover or active color for links and other elements. Also, it is not as powerful as existing page builder plugins though I am sure that new features will close the gap in the future. Yet, I really like its modularity and the ability to customize different theme parts in different ways. I’ll surely consider using it more in the future. How about you?

*What are your thoughts on WordPress Full-Site Editing? How do you think it will impact users, developers, and the WordPress sphere as a whole? Please share your opinion in the comments!*

{{< signature "il, vf, yk" >}}

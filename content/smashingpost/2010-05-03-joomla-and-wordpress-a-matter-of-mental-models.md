---
title: 'Joomla And WordPress: A Matter Of Mental Models'
slug: joomla-and-wordpress-a-matter-of-mental-models
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d455b61b-bbbd-48f6-98c8-8fcee0499814/magic-wand-yellow-illu.jpg
date: 2010-05-03T12:52:50.000Z
author: marco-solazzi
description: >-
  Open-source content management systems (CMS) are a large family of Web
  applications, but if we're looking for stability, performance and average
  technical requirements, we'll come up with a handful of options. In the past,
  choosing the "right" CMS was a matter of the project's requirements, but now
  this is not completely valid because the paradigm of extensibility had driven
  the development of major CMS' towards a model of core features that are
  extensible with plug-ins that fill virtually any requirement.
categories:
  - WordPress
  - CMS
  - Joomla
---
Open-source content management systems (CMS) are a large family of Web applications, but if we're looking for stability, performance and average technical requirements, we'll come up with a handful of options. In the past, choosing the "right" CMS was a matter of the project's requirements, but now this is not completely valid because the paradigm of extensibility had driven the development of major CMS' towards a model of core features that are extensible with plug-ins that fill virtually any requirement.

Picking the right CMS is then a matter of "mental models": choosing the one that best fits our vision of how a Web application should work and what it should provide to users and administrators. In this article, <strong>we'll explore the main difference in the mental models</strong>: of WordPress and Joomla for theming and extending their core.</p>

## Background Thoughts

<img loading="lazy" decoding="async" title="Joomla and WordPress" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/388a981f-d1a2-4e1a-b118-57103067a631/joomla-wp-logos.png" alt="Joomla and WordPress" width="426" height="229" />

WordPress and Joomla are two of the most popular open-source CMS' around. They offer large and active developer communities and excellent documentation.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How WordPress Took The CMS Crown From Drupal And Joomla](https://www.smashingmagazine.com/2011/11/wordpress-cms-crown-drupal-joomla/)
*   [How To Modify A Default Joomla 1.5 Template](https://www.smashingmagazine.com/2011/07/how-to-modify-a-default-joomla-1-5-template/)
*   [Why Static Website Generators Are The Next Big Thing](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/)

WordPress is the first choice among the designer community mostly because of its well-designed back end and wide availability of excellent themes.

Joomla, meanwhile, suffers from Mambo's legacy, which was notorious for low performance and semantically incorrect output (such as nested tables for layout). But since the release of version 1.5, Joomla has a completely rewritten core, with improved extensibility and better HTML output.

One difference between WordPress and Joomla is their theming model. A website developer migrating from Joomla to WordPress might feel that the latter requires too much theme coding, while a developer moving the other way might feel that Joomla is less flexible and customizable. The reason for this is the different models on which the themes of these CMS' are based.</p>

## WordPress' Theming Model

<img loading="lazy" decoding="async" title="WordPress Theme" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fce4639-d7ad-46ff-a80a-f42606f12bbd/wp-theme.jpg" alt="WordPress Theme" width="499" height="220" />

WordPress' theming model is based on a per-view structure. This means that in each theme, you could have individual view files for the post list, the single post and the archive pages. These files are independent of each other, allowing the developer to customize each view but requiring them to duplicate many parts of the code. The only common parts in a theme are the header and footer, which can be coded directly in the individual view anyway.

The main drawback of this model is that different views will not always require a different presentation (for example, the archive, category list and tag list are just lists). To overcome this problem, a theme is organized in a hierarchical structure, in which more generic views are used as fallbacks for specific ones. The common fallback for a WordPress theme is the <em>index.php</em> file, which is actually the only required file (along with a style sheet) in a theme. A complete reference and visual diagram of the hierarchical structure of a WordPress theme are available <a title="WordPress Template File Hierarchy" href="https://codex.wordpress.org/Template_Hierarchy#Visual_Overview">here</a>.</p>

### The Loop and Template Tags

To better understand how a WordPress theme works, we need to look more closely at the "loop" and template tags.

All data for a post or a list of posts is extracted through a loop. A loop is basically a <code>while</code> construct that begins with this declaration:

<pre><code class="language-php">&lt;?php if (have_posts()) : while (have_posts()) : the_post(); ?&gt; 

// post output here 

&lt;?php endif; endwhile; ?&gt;</code></pre>

The most important part of this code is <code>the_post()</code>, which initializes a global <code>$post</code> PHP object containing all of the page data. The loop construct is also required for single post view, because all functions for presentation of data rely on the presence of the <code>$post</code> object. These functions are called template tags, and their main purpose is to output formatted data. Usually, they do not output HTML tags so that they can be used in different scenarios.

A complete guide to theme development is available <a title="WordPress Theme Development" href="https://codex.wordpress.org/Theme_Development">here</a>.</p>

## Joomla's Content-Based Model

<img loading="lazy" decoding="async" title="Joomla Template Configuration File" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3162942b-0d91-4cd5-bd58-ab5186b138eb/joomla-theme.png" alt="Joomla Template Configuration File" width="488" height="220" />

Joomla has a completely different theming approach. Joomla's templates are built on a common structure defined in an <em>index.php</em> file.

This file contains both static content (i.e. content that is common throughout the website) and template tags, which serve as content place-holders and are replaced by HTML output during the page-rendering phase.

A common form for a template tag is:

<pre><code class="language-php">&lt;jdoc:include type="modules" name="right" style="xhtml" /&gt;</code></pre>

Template tags differ in the type of content they provide: component, message, module, head.

This structural backbone implies that each view in the CMS outputs not a complete page but just what's needed to present content. At first glance, a developer used to the theming model of WordPress might think that there's no way to customize this content block. In fact, Joomla relies on the <a title="MVC Architectural patterns" href="https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller">MVC architectural pattern</a>, meaning that data extraction and presentation are separated, the latter being rendered by the view part of the application.</p>

### Template Customization

To customize the default view, Joomla has a pattern called template override, through which the system scans the template folder for a custom view file to use in place of the default one. The image below shows the folder structure and naming convention of a default view and its override.

<img loading="lazy" decoding="async" title="Joomla Template override" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83a9206e-d200-4c58-86ea-493f010df6e7/joomla-overrides.png" alt="Joomla Template override" width="503" height="313" /><br>
<em>An example of the folder and file structure of a Joomla template override (from the "ja_purity" template).</em>

Joomla overrides are an excellent way to customize a website template without hacks. Still, they are often overlooked, and Joomla's support of legacy extensions make this pattern unusable, even for popular packages such as <a href="https://virtuemart.net/">Virtuemart</a> (which uses its built-in template system).

A complete reference for Joomla's template system is available <a title="Joomla! 1.5 Template Tutorials Project" href="https://docs.joomla.org/Joomla!_1.5_Template_Tutorials_Project">here</a>.

## Beyond Core

<img loading="lazy" decoding="async" title="Modular System" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83625970-8d6e-4c8d-91b3-b1d7ca2f9c26/puzzle-modules.jpg" alt="Modular System" width="500" height="220" /><br>
<em>(Image by <a href="https://www.flickr.com/photos/generated/501445202/">jared</a>)</em>

In the last few years, plug-ins have made a big difference in the software industry, one of the most notable examples being Mozilla Firefox.

As we noted, modern CMS' are developed to be extensible, allowing us to use the core as a backbone and build specialized parts on top of it. This resulting modular design is an effective development model for many reasons:

*   Better maintainability Developers don't need to modify the core in order to add or customize functionality.
*   Lightweight and safer Only features that are needed are included, resulting in less memory consumption, a smaller code base and fewer vulnerabilities.
*   Separate development cycles for core and features By offering an extensions API, third-party developers can add new features while the core team focuses on the reliability and performance of the system.

With open-source projects, this last point is both a blessing and a curse. It benefits from shared development effort but leads to unverified work and a less organized workflow.

Joomla and WordPress have tried to overcome this curse by providing coding guidelines. Still, little effort is spent documenting the back-end and front-end UI design.

Aside from their different naming conventions, the extensions models of WordPress and Joomla differ in how third-party code interacts with the core by mean of the extensions API.

The key point to understand is that while Joomla is based on MVC pattern, WordPress relies on an event-like system to which extensions can be hooked. Let's look at some details.</p>

## WordPress' Hook Method

WordPress' extensions model is based on the execution of a set of functions attached to the system flow by mean of "hooks."

Hooks contain a list of functions that are triggered at various points as WordPress is running. They manipulate (in the case of filter hooks) and output (in the case of action hooks) database data and can be accessed from within the theme itself and from a specialized plug-in package.

WordPress lacks comprehensive documentation for hooks, but a list of hooks is available <a title="Plugin API/Action Reference" href="https://codex.wordpress.org/Plugin_API/Action_Reference">here</a>.

To understand the mental model behind WordPress' hook system, we can compare it to the sequence of actions in baking a cake. In the beginning, we have an idea of what kind of cake we want to bake, so we get our ingredients. We cannot just throw everything together and bake it. So, we execute an ordered list of actions, such as "filtering" egg shells and mixing the eggs in with flour and sugar. As we're doing that, we might want to customize the recipe. So, we "plug in" some chocolate and perhaps reduce the quantity of another ingredient by half. The result is a proper cake, created from discrete ingredients and a touch of creativity.

WordPress bakes its pages the same way.</p>

### Sidebars and Widgets

While plug-ins are broadly related to hooks, a widget is a special type of plug-in. It provides a means of showing information in a theme's sidebar. The main advantage of widgets is that they are configurable in the back-end interface, allowing quick customization even for novice users.

<img loading="lazy" decoding="async" title="WordPress Widgets Page" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3861bc69-a014-4449-ba3d-97394bde8e46/wp-widgets.png" alt="WordPress Widgets Page" width="440" height="276" /><br>
<em>All available widgets are listed in an administration panel.</em>

In terms of theme development, the sidebar is similar in its mental model to Joomla's template tags. It is a placeholder for something. The misleading bit is that a sidebar doesn't have to be placed in the actual sidebar of a layout. It could go in the footer, navigation, header or elsewhere.

To learn more about the new API for widget development, have a look at the <a title="WordPress Widgets API" href="https://codex.wordpress.org/Widgets_API">official documentation</a>.</p>

### Adding Functionality

Until now, the problem with WordPress' extension API was that it gave you no simple way to add complex functionality, such as e-commerce carts and event listings. Most developers excused this shortcoming by pointing out that WordPress is a blog engine. This will hopefully be resolved with the release of WordPress 3.0 and its system for "post types," which makes it possible to use the "post" and "page" interfaces for different types of content.

As for other popular CMS' (such as <a href="https://drupal.org/">Drupal</a>), post types function as a kind of "Content Construction Kit," giving you the ability to smartly add, manage and present specialized content. If you're interested in trying this new feature, here is a good <a href="https://kovshenin.com/archives/extending-custom-post-types-in-wordpress-3-0/">tutorial</a>.

Other than post types (and until major plug-ins update support for this feature), the only feasible way to add complex functionality is to use already existing pages as containers, placing in the body a place-holder (called a "<a href="https://codex.wordpress.org/Shortcode_API">shortcode</a>") that is replaced with HTML output by specific filter hooks.

This approach is used by plug-ins such as <a href="https://buddypress.org/">Buddypress</a> and <a href="https://www.instinct.co.nz/e-commerce/">WP e-Commerce</a>, which extend the blog engine with social network and shopping-cart capabilities.

Another great example of shortcode implementation is <a title="Contact Form 7" href="https://contactform7.com/">Contact Form 7</a>, a fully featured contact-form management plug-in.</p>

## Extending Joomla

An often overlooked aspect of Joomla is that it is built on the solid MVC framework. So, extending its core is really much like working with products such as Zend Framework and CodeIgniter, which give you an already designed back-end interface upon which to integrate your own extensions. This approach also gives designers the ability to use template overrides, even for third-party extensions.

<img loading="lazy" decoding="async" title="Joomla! MVC Diagram" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0faaef8-7d82-42b3-902a-a1063e00b64c/mvc-diagram.png" alt="Joomla! MVC Diagram" width="350" height="350" /><br>
<em>A diagram depicting Joomla's Model View Controller system flow.</em>

To better understand MVC and how it works in Joomla, here is a <a href="https://docs.joomla.org/Developing_a_Model-View-Controller_Component_-_Part_1#Introduction_to_Model-View-Controller">complete reference</a>.</p>

### Joomla's Extension Types

Joomla's extension model comes in three flavors, each with different tasks: components, modules and plug-ins.

Components extend the core by adding specific functionality, such as e-commerce carts, event listings and forums. From the user's point of view, we can think of components as discrete sections of a website, not connected to other content. A popular example is <a title="JEvents" href="https://www.jevents.net/">JEvents</a>, an events calendar.

In the theme system, a component's output replaces the <code>component</code> placeholder in the template's <em>index.php</em> file:

<pre><code class="language-php">&lt;jdoc:include type="component" /&gt;</code></pre>

Modules are like widgets in WordPress: they show a component's information, which is extracted from the database. They are "attachable" to module positions and can be put on every page of a website.

Modules are primarily intended to be teaser blocks, but they can incorporate full text and image galleries, which makes them handy for static parts of a layout, such as footer notes. They are also useful for showing related content on a page. For example, you could highlight interesting products for Web developers as they're browsing a list of barcamp events.

The template tag, which serves as module place-holder, looks like this:

<pre><code class="language-php">&lt;jdoc:include type="modules" name="right" style="xhtml" /&gt;</code></pre>

Plug-ins work similar to WordPress' hook system, because they bind to specific system events to format, manipulate and replace HTML output. Possible fields of action range from content for articles (such as video embedding tools—<a href="https://www.joomlaworks.gr/content/view/16/42/">AllVideos</a> is a popular one) to HTML filtering and user-profile extension. Commonly used Joomla plug-ins include URL rewriting filters, which come bundled with administrative components such as <span class="removed_link" title="https://dev.anything-digital.com/sh404SEF/">Sh404SEF</span>.</p>

### Compatibility Issues

One thing every developer should be aware of is that, despite efforts to provide a great extension API, Joomla 1.5 still suffers in its support of legacy extensions (built for v1.0), which do not have an MVC structure and which are sometimes hardly customizable. Furthermore, they break the API mental model.

The Joomla extensions library has a clear mark for 1.0 or 1.5 native extensions. But faking 1.5 native compatibility is easy, which would leave developers with nothing but legacy code. This method is followed even by big well-known projects like <a href="https://virtuemart.net/">Virtuemart</a>.

Hopefully, once Joomla 1.6 is released and legacy support is dropped, every developer will rework their code to fit the CMS' specifications.</p>

## What's Next

While the best way to choose a CMS is by trying it out on a real project, understanding its underlying mental model can make developers feel less lost in code and more aware of the design patterns they need to follow.

If you want to develop themes and extensions for Joomla and WordPress, here are some resources.

WordPress:

*   [How to Create a WordPress Theme from Scratch](https://net.tutsplus.com/tutorials/wordpress/how-to-create-a-wordpress-theme-from-scratch/https://net.tutsplus.com/tutorials/wordpress/how-to-create-a-wordpress-theme-from-scratch/)
*   [How to Write a WordPress Plugin](https://www.devlounge.net/extras/how-to-write-a-wordpress-plugin): a complete reference on WordPress plugins development.
*   [Top 10 Most Common Coding Mistakes in WordPress Plugins](https://planetozh.com/blog/2009/09/top-10-most-common-coding-mistakes-in-wordpress-plugins/): a must read for WordPress developers.
*   [WordPress 3.0 new features](https://wpshout.com/looking-forward-to-wordpress-3-0/)
*   [8 Useful Code Snippets To Get Started With WordPress 3.0](https://www.catswhocode.com/blog/8-useful-code-snippets-to-get-started-with-wordpress-3-0)

Joomla:

*   [Joomla Developer’s Toolbox](https://www.smashingmagazine.com/2009/01/05/joomla-developers-toolbox/): a collection of resources for Joomla users and developers by Smashing Magazine.
*   Creating a Basic Joomla! Template
*   [Developing a Model-View-Controller Component](https://docs.joomla.org/Developing_a_Model-View-Controller_Component_-_Part_1): a step-by-step tutorial on components development in Joomla.
*   Creating a Hello World Module for Joomla 1.5: official documentation on Joomla modules development.
*   [Joomla Component Creator](https://www.notwebdesign.com/joomla-component-creator/): a smart wizard for creating a "starter" component structure.
*   [Joomla 1.6 Updates](https://community.joomla.org/blogs/community/1118-joomla-16-update-february-2010.html): this article explains the primary objectives of the upcoming Joomla 1.6.

{{< signature "al" >}}


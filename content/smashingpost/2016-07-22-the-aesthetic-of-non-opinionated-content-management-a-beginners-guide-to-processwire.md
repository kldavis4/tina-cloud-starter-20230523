---
title: ProcessWire CMS – A Beginner’s Guide
slug: >-
  the-aesthetic-of-non-opinionated-content-management-a-beginners-guide-to-processwire
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ac9700b-c812-499b-83fe-61d1b1af7fa6/10-screenshot-image-cropping-preview-opt.png
date: 2016-07-22T16:05:53.000Z
author: francescoschwarz
description: >-
  Systems for managing content are more often than not rather opinionated. For
  example, most of them expect a certain rigid content structure for inputting
  data and then have a specific engraved way of accessing and outputting that
  data, whether or not it makes sense. Additionally, they rarely offer effective
  tools to break out of the predefined trails if a case requires it.
categories:
  - WordPress
  - CMS
  - Techniques (WP)
---
<a href="https://processwire.com/">ProcessWire</a> is a content management system (CMS) distributed under the Mozilla Public License version 2.0 (MPL) and MIT License. It is designed from the ground up to tackle the issues caused by exactly this kind of opinionatedness (which, inevitably, results in frustrated developers and users) by being — you guessed it — non-opinionated. At its heart, it is based on a few simple core concepts and offers an exceptionally easy-to-use and powerful API to handle content of any kind. Let’s get right into it!

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Designing for Content Management Systems](https://www.smashingmagazine.com/2010/11/designing-for-content-management-systems/)
*   [Why Static Website Generators Are The Next Big Thing](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/)
*   [Content Management System (CMS) Icon Set (12 Free Icons)](https://www.smashingmagazine.com/2010/07/content-management-system-cms-icon-set-12-free-icons/)
*   [Getting Started With Content Management Systems](https://www.smashingmagazine.com/2009/11/getting-started-with-content-management-systems/)

## The Admin GUI

After <a href="https://processwire.com/about/requirements/">installing</a> ProcessWire (which requires PHP 5.3.8+, MySQL 5.0.15+ and Apache), you will see the home page of the default admin GUI:

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19d8a125-c0d0-4fa8-9ff2-0fe9a35ab34c/02-screenshot-processwire-admin-gui-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19d8a125-c0d0-4fa8-9ff2-0fe9a35ab34c/02-screenshot-processwire-admin-gui-preview-opt.png" alt="ProcessWire admin GUI." title="A Beginner’s Guide To ProcessWire" /></a><figcaption>The admin GUI has a pretty simple structure. It’s also fully responsive, so it will look slightly different on big screens.</figcaption></figure>

<strong>Note:</strong> The pages you see in the hierarchical page tree (more on that later) are there because I chose the “Default (Beginner Edition)” website profile during the installation process. This is totally optional. You could also start with a blank website profile, which lets you build everything from scratch.

You can actually <a href="https://modules.processwire.com/categories/admin-theme/">choose from</a> many admin themes, although for ProcessWire 2.6+ the default theme or Reno theme is recommended. Because Reno comes prepackaged with every ProcessWire installation, switching to it is pretty easy: Just install it and select it in your user profile.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4d6744b-0337-4797-ae43-da7509ed9476/03-changing-default-theme-to-reno-theme.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46fd1a6c-d197-4fb2-ba79-5deeb3a3540f/03-screenshot-reno-theme-preview-opt.png" alt="Screenshot of “Reno” theme." /></a><figcaption>Installing a new theme for the admin GUI is easy. This one is called Reno. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4d6744b-0337-4797-ae43-da7509ed9476/03-changing-default-theme-to-reno-theme.gif">View animated GIF version</a>)</figcaption></figure>

Let’s have a quick look at the main back-end navigation:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01d8435c-509c-48f0-b9a6-904dc2084fc8/04-screenshot-main-navigation-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01d8435c-509c-48f0-b9a6-904dc2084fc8/04-screenshot-main-navigation-preview-opt.png" alt="Screenshot of the main navigation in the back-end." /></a></figure>

*   “Pages” This is the entry point of the admin GUI. It features the hierarchical page tree and, thus, all of your website’s content in the back end.
*   “Setup” This is the place to set up the general data model architecture of your installation through templates and fields (more on that later). This is also where ProcessWire modules often add an entry for their specific functionality and user interface — for example, visualizing log messages right in the admin GUI or managing all of the different languages when dealing with multi-language content.
*   “Modules” This is where you manage all of your website’s modules. Think of ProcessWire modules as WordPress plugins: They extend and customize the system.
*   “Access” Here is where you manage users, user roles and user permissions.</p>

## Three Simple Core Concepts

The core concepts that form the overall data model architecture of ProcessWire are exactly three: <strong>pages, fields and templates</strong>. Let’s look at each one by one.</p>

### Everything Is a Page: Or, One Page Tree to Rule Them All

A page in ProcessWire can generate a regular page in the front end of your website, ready to be visited by your users (like “Home” and “About” in the screenshot above). But a page can also exist solely in the back end, with no front-end counterpart — for example, a hidden settings page where you store the global slogan, logo and copyright notice of your website. When I say “everything is a page” in ProcessWire, I mean it. Heck, even the main navigation links in the admin GUI are made out of hidden pages in the hierarchical page tree!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba616e0f-61c6-4d55-bc69-e6f706af379d/05-screenshot-everything-is-a-page-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba616e0f-61c6-4d55-bc69-e6f706af379d/05-screenshot-everything-is-a-page-preview-opt.png" alt="Screenshot that shows that even the back-end navigation is made out of pages." /></a><figcaption>In ProcessWire, everything is a page. Even the main navigation and sub-navigation are made out of pages from the hierarchical page tree.</figcaption></figure>

This is so meta that I’m reminded of a <a href="https://knowyourmeme.com/memes/xzibit-yo-dawg">certain Xzibit meme</a>. But let’s leave it at that.

The concept of a page being visible only in the back end is pretty powerful because it opens up a whole world of possibilities on how to structure and access data through other pages (your imagination being the only limit). You could build a massive product catalog, or an intranet application with hundreds of thousands of items based on a complex page hierarchy, or just a simple blog with the usual blog categories and tags (every category and tag being a page in the page tree).</p>

<a href="https://twitter.com/joss_sanglier">Joss Sanglier</a>, a distinguished member in the ProcessWire community, breaks down the concept of pages <a href="https://processwire.com/talk/topic/2296-confused-by-pages/#entry21426">to this</a>:
<blockquote>[I]n ProcessWire pages are […] not great gulps of information, but tiny little things, nothing more than a link to the more interesting world of fields and templates; just a little blip of data in your huge fascinating database.

Pages in ProcessWire are used for all kinds of things. They can be used as a marker in your pages list. They can be used as a group parent for other pages. They can be used as categories, tags or lists or users. And they can even be used for simple drop-down selects — just to supply a label and value.</blockquote>

Let’s interact with the hierarchical page tree a little bit:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1130eb36-b71d-4077-ad3b-8d928a7702b9/06-interacting-with-page-tree.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faab9355-f98b-405a-a95e-9bcbbaf25f11/06-screenshot-drag-and-drop-page-tree-preview-opt.png" alt="Screenshot of drag and drop in the page tree." /></a><figcaption>You can move pages in the hierarchical page tree by dragging and dropping. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1130eb36-b71d-4077-ad3b-8d928a7702b9/06-interacting-with-page-tree.gif">View animated GIF version</a>)</figcaption></figure>

As you can see, pages can be edited, moved around or trashed, and they can have an infinite number of children and grandchildren.

Let’s open up the “Home” page:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52c26b9e-5540-43ef-b2fc-e4e934cb292d/07-screenshot-home-page-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52c26b9e-5540-43ef-b2fc-e4e934cb292d/07-screenshot-home-page-preview-opt.png" alt="Screenshot of the opened Home page" /></a><figcaption>The “Home” page of the “Default (Beginner Edition)” website profile features a few simple fields, which are all optional.</figcaption></figure>

This brings us to the next core concept of ProcessWire, fields.</p>

### Fields Are The Containers Into Which You Put Data

Fields are basically the containers into which you put data. At this point, it’s important to realize that ProcessWire doesn’t have the concept of custom fields, like WordPress does, because <strong>every field in ProcessWire is a custom field</strong>. When you create a field, you can give it a label, a description and some additional notes that will appear underneath it.

Let’s edit the “Title” field and add a description and a note to it:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4b88fec-d5ba-423a-81c7-b40abdb62e5e/08-change-description-and-note-of-title.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02201ab2-4290-4979-a633-7bd81e16eac7/08-screenshot-title-with-description-and-note-preview-opt.png" alt="Screenshot of the title field with custom description and note." /></a><figcaption>Every field can be given a custom description and a note. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4b88fec-d5ba-423a-81c7-b40abdb62e5e/08-change-description-and-note-of-title.gif">View animated GIF version</a>)</figcaption></figure>

The preinstalled field types cover most basic data-input needs. For example, you can create things like check boxes, date-pickers, field sets (a field that groups other fields into visually logical units), file and image uploaders and, of course, text and textarea fields (the default WYSIWYG editor being <a href="https://ckeditor.com">CKEditor</a>).

There are also a lot of prepackaged and <a href="https://modules.processwire.com/categories/fieldtype/">third-party</a> field types to choose from. A useful core module, which is not installed by default, is the <strong>repeater field</strong>. It lets you dynamically create rows of data sets.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3830b830-743f-44ec-a587-e0fdb0aaa805/09-repeater-in-action.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90f95810-2506-4e9a-b25b-1d837faa7f39/09-screenshot-repeater-preview-opt.png" alt="Screenshot of the repeater." /></a><figcaption>Repeaters are a neat and easy way to create rows of data of the same kind. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3830b830-743f-44ec-a587-e0fdb0aaa805/09-repeater-in-action.gif">View animated GIF version</a>)</figcaption></figure>

ProcessWire is also a good fit for handling <strong>images</strong>. For example, you can decide which image variants ProcessWire should automatically create of an image after uploading it (which enables nice use cases for responsive images). And choosing a thumbnail for an image is a breeze.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acf9b4cd-d52d-4515-882c-fbd4954a018d/10-image-editing-in-action.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ac9700b-c812-499b-83fe-61d1b1af7fa6/10-screenshot-image-cropping-preview-opt.png" alt="Screenshot of cropping an image." /></a><figcaption>ProcessWire is a good fit for working with images. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acf9b4cd-d52d-4515-882c-fbd4954a018d/10-image-editing-in-action.gif">View animated GIF version</a>)</figcaption></figure>

Another useful field type is the <strong>page field type</strong>. You can link other pages with the page you are currently editing and, thus, create a relationship between them. In the field’s settings, you can decide how the input’s appearance and interaction with the field should be — for example, whether a single page or multiple pages should be selectable, or whether only the child pages of a particular parent page should be selectable. If you were to write, say, a blog post, you could choose to allow only blog post categories to autocomplete.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f779abc1-6cea-4aec-a30d-33e1d78cc2cb/11-page-field-autocomplete.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9294944-6d85-4604-8be0-89f622f23bf4/11-screenshot-page-field-autocomplete-preview-opt.png" alt="Screenshot of the autocomplete page field." /></a><figcaption>A page field can have very different manifestations. Here is one: The autocomplete functionality lets you choose already existing pages (in the dropdown menu) but also create new pages right within the field. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f779abc1-6cea-4aec-a30d-33e1d78cc2cb/11-page-field-autocomplete.gif">View animated GIF version</a>)</figcaption></figure>

A neat feature you can switch on in the settings of a field is the ability to <strong>edit the field’s content in the front end of your website</strong>. Once a user has logged into ProcessWire’s back end, they can switch to the website’s front end and edit and save the content right where it will eventually get rendered.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e63f12a5-39e7-4138-bda9-15c084fd47c7/12-front-end-editing.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8760bad2-5d8e-4d76-8512-a1ff25f0e50e/12-screenshot-front-end-editing-preview-opt.png" alt="Screenshot of editing content on your website’s front-end." /></a><figcaption>Are you a fan of front-end editing of content? ProcessWire has you covered. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e63f12a5-39e7-4138-bda9-15c084fd47c7/12-front-end-editing.gif">View animated GIF version</a>)</figcaption></figure>

After looking at pages and fields in ProcessWire, you may ask yourself: How does a page know which fields it has? And where can I define how the fields are ordered and rendered on a page? So, let’s move on to the last core concept, templates.</p>

### Templates Are the Blueprints of Pages

Every time you create a page in the hierarchical page tree, ProcessWire needs to know which template is associated with it. That’s because a page needs to know which fields it has to render, and that information is always a part of the respective template.

Long story short: Templates contain all of the information the page needs to know about its contents (what fields it has, how those fields are rendered and how they behave).

Let’s open the “Home” template from our sample installation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f151426-016b-4e13-b56e-3cadb7ba47bf/13-screenshot-template-settings-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8fa7471-56b9-4897-a11e-459883dad777/13-screenshot-template-settings-preview-opt.png" alt="Screenshot of the template settings" /></a><figcaption>Templates in ProcessWire are very flexible and are one of the reasons why ProcessWire feels more like a framework than a CMS. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f151426-016b-4e13-b56e-3cadb7ba47bf/13-screenshot-template-settings-opt.png">View large version</a>)</figcaption></figure>

The main thing to notice is the number of settings. There’s really a lot to discover here. For example, you can limit access to the pages created with this template to specific user roles. Or you can decide whether pages created with this template should be cached for a specific amount of time (to enhance performance), plus the conditions under which the cache must be cleared.

Another powerful setting is hidden in the “Family” tab. Here, you can define whether pages created with this template can have children pages and which templates are allowed for the parent page or its children pages. This allows you to create exactly the type of template family hierarchy that you want. It’s a flexible and handy way (and actually one of the most powerful ways) to structure your data, and it’s one of the many ways that ProcessWire shows its flexibility.

Let’s turn our attention to the <strong>list of fields</strong> in a template. Looking at the screenshot above, you can see that the order of the fields resembles the order in which the fields will get rendered on the home page. You can simply drag and drop fields to change the order in the list, thus changing the order of appearance when editing the home page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c122aecf-4b45-4234-b920-e035f6b33559/14-changing-field-order.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32fa4339-7e01-4d44-9805-429c7e46d6c9/14-screenshot-change-of-field-order-preview-opt.png" alt="Left screenshot half: drag and drop fields in template settings. Right screenshot half: changed field order on “Home” page." /></a><figcaption>Changing the order of fields in the template settings (left) affects the order in which the fields are rendered on the page (right). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c122aecf-4b45-4234-b920-e035f6b33559/14-changing-field-order.gif">View animated GIF version</a>)</figcaption></figure>

You can also change the width of a field on the page. Just click on a field and change it. Let’s put the “Title” and “Headline” fields side by side.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32c37336-a284-486f-860f-f88d8aa1a4db/15-changing-width-of-fields.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a23ec022-1595-4958-bc19-fd7c20c7a8a5/15-screenshot-of-fields-side-by-side-preview-opt.png" alt="Screenshot of fields rendered side by side" /></a><figcaption>You are in total control of how fields are rendered on the page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32c37336-a284-486f-860f-f88d8aa1a4db/15-changing-width-of-fields.gif">View animated GIF version</a>)</figcaption></figure>

Another example of how you can customize and tailor the user interface of a page and its fields are <a href="https://processwire.com/api/selectors/inputfield-dependencies/">inputfield dependencies</a>. These enable you to specify the conditions under which a particular field in the page editor is shown or required. Let’s make the “Headline” field visible in the UI only if the user enters something in the “Title” field, and let’s mark the “Summary” field as required only if the user enters something in the “Headline” field:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38778221-7531-4dd2-838f-2fb79979bff7/16-inputfield-dependencies.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6cf6a92-3a78-4011-922a-371b48e0d276/16-screenshot-inputfield-dependencies-preview-opt.png" alt="Screenshot of settings for inputfield dependencies" /></a><figcaption>The “Headline” field will be shown on the page only once the user has entered something in the “Title” field. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38778221-7531-4dd2-838f-2fb79979bff7/16-inputfield-dependencies.gif">View animated GIF version</a>)</figcaption></figure>

Here’s a video that shows you how inputfield dependencies can be used to enhance the user’s experience while working with ProcessWire:
<figure class="video-container"><iframe loading="lazy" width="500" height="280" src="https://www.youtube.com/watch?v=hqLs9YNYKMM" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

<figcaption>How inputfield dependencies can be used to enhance the user’s experience while working with ProcessWire</figcaption></figure>

The number, order and appearance of fields on a page are totally under your control. You can put just one field in a template, none at all (not very useful) or more than 50 fields, 100 or even more. You can order them in any way you want, specify which are required or visible and which aren’t, and specify under what circumstances they should be required or visible. Here is where ProcessWire’s non-opinionated approach shines.</p>

### Roundup: Pages, Fields, Templates

Let’s recap the technical relationship between pages, fields and templates: You add fields to templates, and you select a template when creating a new page. The fields you see when editing a page are the fields you’ve added to the selected template.

Another way to look at this would be through an analogy from the programming world:

*   Templates are like classes.
*   Fields are like the properties of classes.
*   Pages are instances of classes.

Once you internalize these concepts, you’ll be equipped with everything you need to know to develop in ProcessWire. And the reason for this is that ProcessWire’s <a href="https://processwire.com/about/why/">philosophy</a> is based solely on these three concepts. Pretty cool, right?

## Template Files And The API: A Couple Meant To Be Together

The place where you retrieve the data inputted in ProcessWire’s back end and output it in the front end is, of course, the file system — more specifically, the <code>/site/templates/</code> folder of your ProcessWire installation. A template can have a physical PHP file of the same name associated with it; so, the <code>home</code> template would have a <code>home.php</code> file in the <code>/site/templates/</code> folder.</p>

<strong>Note:</strong> How you develop your template files is totally up to you. If you are familiar with the WordPress style of developing things, you can continue just as you are used to. Or, if you have a pretty complex and big set-up and want to create a more sophisticated architecture, you could use an MVC-inspired approach, which would work just as well. Ryan Cramer has a pretty good introductory tutorial, titled “<a href="https://processwire.com/docs/tutorials/how-to-structure-your-template-files/">How to Structure Your Template Files</a>,” in which you can learn different approaches to template file development in ProcessWire.

The code you write in a template file will mostly consist of basic PHP constructs (<code>if</code> conditions, <code>foreach</code> loops, <code>echo</code> statements), HTML markup and <a href="https://processwire.com/api/concept/">ProcessWire’s API</a>. The API is heavily inspired by jQuery — so, it’s really kind of like iterating and traversing the content you’ve inputted in the back end via methods, selectors and chaining (fluent interface) capabilities. It’s easy to use and very expressive, just like jQuery.

Let’s start by looking at some simple examples to get you going with the API. But before we start, remember to bookmark the <a href="https://cheatsheet.processwire.com/">ProcessWire API cheat sheet</a>, a helpful reference with an overview of all available API methods.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5388655a-9a10-4696-ab59-afb4a533c3f2/17-processwire-cheatsheet-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5388655a-9a10-4696-ab59-afb4a533c3f2/17-processwire-cheatsheet-preview-opt.png" alt="Screenshot of the ProcessWire Cheatsheet" /></a><figcaption>The <a href="https://cheatsheet.processwire.com/">API cheat sheet</a> will serve you as a good companion.</figcaption></figure>

The thing we want to do first is access and output the content of a page’s field. The API exposes a variable for us to deal with this: <code>$page</code>.</p>

### Getting the Current Page With the `$page` Variable

The <code>$page</code> variable contains all of the fields of a single page. This includes <a href="https://cheatsheet.processwire.com/page/built-in-fields-reference">built-in fields</a> (like the name of a page’s template), as well as the fields you, as the developer, have added to the page’s template.

Let’s open <code>home.php</code>, which is the template file of the <code>home</code> template, and add this line to it:

<pre><code class="language-php">echo $page-&gt;title;
</code></pre>

This tells ProcessWire to grab the “Title” field of the page we are currently on (“Home”) and output it. Let’s say we also have a “Headline” field on the page, which we want to use instead of the “Title” field but only if the user has entered something in it.</p>

<pre><code class="language-php">echo $page-&gt;get("headline|title");
</code></pre>

We used the <code>get</code> method to access a page’s field (so, <code>$page-&gt;get("title")</code> is basically equivalent to the first code example above), and we wrote <code>"headline|title"</code> in the <code>get</code> method. This tells ProcessWire to first check the “Headline” field and output the headline’s content. But if the “Headline” field is empty, then the “Title” field is used as the fallback.

Using API variables in PHP strings is also possible. The following two <code>echo</code> statements for outputting the number of children of a page are equivalent:

<pre><code class="language-php">echo "This page has " . $page-&gt;numChildren . " children pages.";
echo "This page has {$page-&gt;numChildren} children pages.";
</code></pre>

Let’s get the children of our root page (remember, we are still in <code>home.php</code>) and output them as a list of links:

<pre><code class="language-php">echo "&lt;ul&gt;";
foreach ($page-&gt;children as $child) {
	echo "&lt;li&gt;&lt;a href='{$child-&gt;url}'&gt;{$child-&gt;title}&lt;/a&gt;&lt;/li&gt;";
}
echo "&lt;/ul&gt;";
</code></pre>

Another example of a built-in field (like <code>children</code> and <code>url</code> in the example above) is iterating through all parents of a page and creating breadcrumb navigation:

<pre><code class="language-php">echo "&lt;ul&gt;";
foreach ($page-&gt;parents as $parent) {
	echo "&lt;li&gt;&lt;a href='{$parent-&gt;url}'&gt;{$parent-&gt;title}&lt;/a&gt;&lt;/li&gt;";
}
// output the page itself at the end
echo "&lt;li&gt;{$page-&gt;title}&lt;/li&gt;";
echo "&lt;/ul&gt;";
</code></pre>

On the root page (“Home”), this would just output its title, because <code>$page-&gt;parents</code> would be empty.

Earlier, I showed you how to create image thumbnails in the admin GUI. Creating thumbnails can also be done programmatically with the help of the API. Let’s iterate through all images uploaded in the “Images” field, create a large image variant at 600 pixel wide with a proportional height, and a 150 × 150-pixel thumbnail, with specific options like crop settings and image quality. In the end, we want to link the thumbnail image to the large image. Sounds complicated? It isn’t.</p>

<pre><code class="language-php">$options = array(
	"quality" =&gt; 90,
	"cropping" =&gt; "northwest"
);

foreach ($page-&gt;images as $image) {
	$large = $image-&gt;width(600);
	$thumbnail = $image-&gt;size(150, 150, $options);
	echo "&lt;a href='{$large-&gt;url}'&gt;&lt;img src='{$thumbnail-&gt;url}' alt=’&gt;&lt;/a&gt;";
}
</code></pre>

ProcessWire is pretty smart in this regard because it creates images at any sizes on the fly and keeps a cache of them, so that it has to create the versions just once.

Here is one last <code>$page</code> example to show you that the API feels a lot like you’re interacting with the DOM when using jQuery. Let’s get the last child of the parent page we are currently on.</p>

<pre><code class="language-php">$wantedPage = $page-&gt;parent-&gt;children()-&gt;last();</code></pre>

Besides the <code>$page</code> variable, the API exposes another important one: <code>$pages</code>.</p>

### Getting All Pages With the `$pages` Variable

With <code>$pages</code>, you have access to all pages in your ProcessWire installation. In other words, it gives you <strong>access to all of your content from anywhere</strong>.

For example, you could have a hidden (meaning, not accessible in the front end) settings page in your ProcessWire installation; you could add global settings, like the title and description of your website; and you could access and output these content blobs from any template file you want.</p>

<pre><code class="language-php">$settings = $pages-&gt;get("template=settings");
echo "&lt;h1&gt;{$settings-&gt;global_title}&lt;/h1&gt;";
echo "&lt;p&gt;{$settings-&gt;global_description}&lt;/p&gt;";
</code></pre>

One common use case for a single topic page of a blog is to show all blog posts in which the topic is referenced. Just write this in the template file of the topic:

<pre><code class="language-php">$pages-&gt;find("template=blog-post, topics=$page");</code></pre>

<strong>Note:</strong> <code>topics</code> is a field in the <code>blog-post</code> template where you would add all topic categories that are specific to the blog post.

Another powerful setting is hidden in the “Family” tab. Here, you can define whether pages created with this template can have children pages and which templates are allowed for the parent page or its children pages. This allows you to create exactly the type of template family hierarchy that you want. It’s a flexible and handy way (and actually one of the most powerful ways) to structure your data, and it’s one of the many ways that ProcessWire shows its flexibility.

Let’s turn our attention to the <strong>list of fields</strong> in a template. Looking at the screenshot above, you can see that the order of the fields resembles the order in which the fields will get rendered on the home page. You can simply drag and drop fields to change the order in the list, thus changing the order of appearance when editing the home page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c122aecf-4b45-4234-b920-e035f6b33559/14-changing-field-order.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32fa4339-7e01-4d44-9805-429c7e46d6c9/14-screenshot-change-of-field-order-preview-opt.png" alt="Left screenshot half: drag and drop fields in template settings. Right screenshot half: changed field order on “Home” page." /></a><figcaption>Changing the order of fields in the template settings (left) affects the order in which the fields are rendered on the page (right). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c122aecf-4b45-4234-b920-e035f6b33559/14-changing-field-order.gif">View animated GIF version</a>)</figcaption></figure>

You can also change the width of a field on the page. Just click on a field and change it. Let’s put the “Title” and “Headline” fields side by side.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32c37336-a284-486f-860f-f88d8aa1a4db/15-changing-width-of-fields.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a23ec022-1595-4958-bc19-fd7c20c7a8a5/15-screenshot-of-fields-side-by-side-preview-opt.png" alt="Screenshot of fields rendered side by side" /></a><figcaption>You are in total control of how fields are rendered on the page. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32c37336-a284-486f-860f-f88d8aa1a4db/15-changing-width-of-fields.gif">View animated GIF version</a>)</figcaption></figure>

Another example of how you can customize and tailor the user interface of a page and its fields are <a href="https://processwire.com/api/selectors/inputfield-dependencies/">inputfield dependencies</a>. These enable you to specify the conditions under which a particular field in the page editor is shown or required. Let’s make the “Headline” field visible in the UI only if the user enters something in the “Title” field, and let’s mark the “Summary” field as required only if the user enters something in the “Headline” field:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38778221-7531-4dd2-838f-2fb79979bff7/16-inputfield-dependencies.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6cf6a92-3a78-4011-922a-371b48e0d276/16-screenshot-inputfield-dependencies-preview-opt.png" alt="Screenshot of settings for inputfield dependencies" /></a><figcaption>The “Headline” field will be shown on the page only once the user has entered something in the “Title” field. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38778221-7531-4dd2-838f-2fb79979bff7/16-inputfield-dependencies.gif">View animated GIF version</a>)</figcaption></figure>

Here’s a video that shows you how inputfield dependencies can be used to enhance the user’s experience while working with ProcessWire:
<figure class="video-container"><iframe loading="lazy" width="500" height="280" src="https://www.youtube.com/watch?v=hqLs9YNYKMM" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></figure>

<figcaption>How inputfield dependencies can be used to enhance the user’s experience while working with ProcessWire</figcaption></figure>

The number, order and appearance of fields on a page are totally under your control. You can put just one field in a template, none at all (not very useful) or more than 50 fields, 100 or even more. You can order them in any way you want, specify which are required or visible and which aren’t, and specify under what circumstances they should be required or visible. Here is where ProcessWire’s non-opinionated approach shines.</p>

### Roundup: Pages, Fields, Templates

Let’s recap the technical relationship between pages, fields and templates: You add fields to templates, and you select a template when creating a new page. The fields you see when editing a page are the fields you’ve added to the selected template.

Another way to look at this would be through an analogy from the programming world:

*   Templates are like classes.
*   Fields are like the properties of classes.
*   Pages are instances of classes.

Once you internalize these concepts, you’ll be equipped with everything you need to know to develop in ProcessWire. And the reason for this is that ProcessWire’s <a href="https://processwire.com/about/why/">philosophy</a> is based solely on these three concepts. Pretty cool, right?

## Template Files And The API: A Couple Meant To Be Together

The place where you retrieve the data inputted in ProcessWire’s back end and output it in the front end is, of course, the file system — more specifically, the <code>/site/templates/</code> folder of your ProcessWire installation. A template can have a physical PHP file of the same name associated with it; so, the <code>home</code> template would have a <code>home.php</code> file in the <code>/site/templates/</code> folder.</p>

<strong>Note:</strong> How you develop your template files is totally up to you. If you are familiar with the WordPress style of developing things, you can continue just as you are used to. Or, if you have a pretty complex and big set-up and want to create a more sophisticated architecture, you could use an MVC-inspired approach, which would work just as well. Ryan Cramer has a pretty good introductory tutorial, titled “<a href="https://processwire.com/docs/tutorials/how-to-structure-your-template-files/">How to Structure Your Template Files</a>,” in which you can learn different approaches to template file development in ProcessWire.

The code you write in a template file will mostly consist of basic PHP constructs (<code>if</code> conditions, <code>foreach</code> loops, <code>echo</code> statements), HTML markup and <a href="https://processwire.com/api/concept/">ProcessWire’s API</a>. The API is heavily inspired by jQuery — so, it’s really kind of like iterating and traversing the content you’ve inputted in the back end via methods, selectors and chaining (fluent interface) capabilities. It’s easy to use and very expressive, just like jQuery.

Let’s start by looking at some simple examples to get you going with the API. But before we start, remember to bookmark the <a href="https://cheatsheet.processwire.com/">ProcessWire API cheat sheet</a>, a helpful reference with an overview of all available API methods.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5388655a-9a10-4696-ab59-afb4a533c3f2/17-processwire-cheatsheet-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5388655a-9a10-4696-ab59-afb4a533c3f2/17-processwire-cheatsheet-preview-opt.png" alt="Screenshot of the ProcessWire Cheatsheet" /></a><figcaption>The <a href="https://cheatsheet.processwire.com/">API cheat sheet</a> will serve you as a good companion.</figcaption></figure>

The thing we want to do first is access and output the content of a page’s field. The API exposes a variable for us to deal with this: <code>$page</code>.</p>

### Getting the Current Page With the `$page` Variable

The <code>$page</code> variable contains all of the fields of a single page. This includes <a href="https://cheatsheet.processwire.com/page/built-in-fields-reference">built-in fields</a> (like the name of a page’s template), as well as the fields you, as the developer, have added to the page’s template.

Let’s open <code>home.php</code>, which is the template file of the <code>home</code> template, and add this line to it:

<pre><code class="language-php">echo $page-&gt;title;
</code></pre>

This tells ProcessWire to grab the “Title” field of the page we are currently on (“Home”) and output it. Let’s say we also have a “Headline” field on the page, which we want to use instead of the “Title” field but only if the user has entered something in it.</p>

<pre><code class="language-php">echo $page-&gt;get("headline|title");
</code></pre>

We used the <code>get</code> method to access a page’s field (so, <code>$page-&gt;get("title")</code> is basically equivalent to the first code example above), and we wrote <code>"headline|title"</code> in the <code>get</code> method. This tells ProcessWire to first check the “Headline” field and output the headline’s content. But if the “Headline” field is empty, then the “Title” field is used as the fallback.

Using API variables in PHP strings is also possible. The following two <code>echo</code> statements for outputting the number of children of a page are equivalent:

<pre><code class="language-php">echo "This page has " . $page-&gt;numChildren . " children pages.";
echo "This page has {$page-&gt;numChildren} children pages.";
</code></pre>

Let’s get the children of our root page (remember, we are still in <code>home.php</code>) and output them as a list of links:

<pre><code class="language-php">echo "&lt;ul&gt;";
foreach ($page-&gt;children as $child) {
	echo "&lt;li&gt;&lt;a href='{$child-&gt;url}'&gt;{$child-&gt;title}&lt;/a&gt;&lt;/li&gt;";
}
echo "&lt;/ul&gt;";
</code></pre>

Another example of a built-in field (like <code>children</code> and <code>url</code> in the example above) is iterating through all parents of a page and creating breadcrumb navigation:

<pre><code class="language-php">echo "&lt;ul&gt;";
foreach ($page-&gt;parents as $parent) {
	echo "&lt;li&gt;&lt;a href='{$parent-&gt;url}'&gt;{$parent-&gt;title}&lt;/a&gt;&lt;/li&gt;";
}
// output the page itself at the end
echo "&lt;li&gt;{$page-&gt;title}&lt;/li&gt;";
echo "&lt;/ul&gt;";
</code></pre>

On the root page (“Home”), this would just output its title, because <code>$page-&gt;parents</code> would be empty.

Earlier, I showed you how to create image thumbnails in the admin GUI. Creating thumbnails can also be done programmatically with the help of the API. Let’s iterate through all images uploaded in the “Images” field, create a large image variant at 600 pixel wide with a proportional height, and a 150 × 150-pixel thumbnail, with specific options like crop settings and image quality. In the end, we want to link the thumbnail image to the large image. Sounds complicated? It isn’t.</p>

<pre><code class="language-php">$options = array(
	"quality" =&gt; 90,
	"cropping" =&gt; "northwest"
);

foreach ($page-&gt;images as $image) {
	$large = $image-&gt;width(600);
	$thumbnail = $image-&gt;size(150, 150, $options);
	echo "&lt;a href='{$large-&gt;url}'&gt;&lt;img src='{$thumbnail-&gt;url}' alt=’&gt;&lt;/a&gt;";
}
</code></pre>

ProcessWire is pretty smart in this regard because it creates images at any sizes on the fly and keeps a cache of them, so that it has to create the versions just once.

Here is one last <code>$page</code> example to show you that the API feels a lot like you’re interacting with the DOM when using jQuery. Let’s get the last child of the parent page we are currently on.</p>

<pre><code class="language-php">$wantedPage = $page-&gt;parent-&gt;children()-&gt;last();</code></pre>

Besides the <code>$page</code> variable, the API exposes another important one: <code>$pages</code>.</p>

### Getting All Pages With the `$pages` Variable

With <code>$pages</code>, you have access to all pages in your ProcessWire installation. In other words, it gives you <strong>access to all of your content from anywhere</strong>.

For example, you could have a hidden (meaning, not accessible in the front end) settings page in your ProcessWire installation; you could add global settings, like the title and description of your website; and you could access and output these content blobs from any template file you want.</p>

<pre><code class="language-php">$settings = $pages-&gt;get("template=settings");
echo "&lt;h1&gt;{$settings-&gt;global_title}&lt;/h1&gt;";
echo "&lt;p&gt;{$settings-&gt;global_description}&lt;/p&gt;";
</code></pre>

One common use case for a single topic page of a blog is to show all blog posts in which the topic is referenced. Just write this in the template file of the topic:

<pre><code class="language-php">$pages-&gt;find("template=blog-post, topics=$page");</code></pre>

<strong>Note:</strong> <code>topics</code> is a field in the <code>blog-post</code> template where you would add all topic categories that are specific to the blog post.

Let’s work a little more with <a href="https://processwire.com/api/selectors/">ProcessWire’s selector engine</a>. Let me show you some examples by referring you to <a href="https://processwire.com/demo/">ProcessWire’s demo website</a>, a directory of US skyscrapers. The demo website contains many pages and has an interesting data model architecture (i.e. things like architects, cities, buildings and locations referencing each other), and it’s a good use case to show what you can do with selectors.

This example finds all skyscrapers that mention the phrase “empire state building” in their body copy:

<pre><code class="language-php">$pages-&gt;get("template=cities")-&gt;find("template=skyscraper, body*=empire state building");</code></pre>

<strong>Note:</strong> First we get the page with the template <code>cities</code>; then, we get all pages with the template <code>skyscraper</code>. The reason why we can chain the methods in this way is because all skyscraper pages are sub-children of the “Cities” page.

Let’s find all skyscrapers by the architects Adrian Smith, Eric Kuhne or William Pereira and sort the results by height in ascending order:

<pre><code class="language-php">$adrian = $pages-&gt;get("template=architect, name=adrian-smith");
$eric = $pages-&gt;get("template=architect, name=eric-kuhne");
$william = $pages-&gt;get("template=architect, name=william-pereira");

$skyscrapers = $pages-&gt;find("template=skyscraper, architects=$adrian|$eric|$william, sort=height");
</code></pre>

You could optimize the code by finding all requested architects in a single step, instead of three:

<pre><code class="language-php">$architects = $pages-&gt;find("template=architect, name=adrian-smith|eric-kuhne|william-pereira");
$skyscrapers = $pages-&gt;find("template=skyscraper, architects=$architects, sort=height");
</code></pre>

<strong>Note:</strong> The <code>get</code> method potentially always returns one page; the <code>find</code> method potentially always returns multiple pages.

You can further revise the code by using <a href="https://processwire.com/api/selectors/#sub-selectors">sub-selectors</a> (yes, you can have selectors inside of selectors):

<pre><code class="language-php">$skyscrapers = $pages-&gt;find("template=skyscraper, architects=[name=adrian-smith|eric-kuhne|william-pereira], sort=height");
</code></pre>

### Other API Variables

<code>$page</code> and <code>$pages</code> are not the only API variables you can work with. There are a <a href="https://processwire.com/api/variables/">whole lot of other ones</a>, such as <code>$session</code> (to log users in and out and to redirect to other pages), <code>$user</code> (to establish a connection to the user currently viewing the page) and <code>$config</code> (which are for settings specific to your ProcessWire installation). Let’s look at two examples.

First, let’s redirect the user to the home page:

<pre><code class="language-php">$session-&gt;redirect($pages-&gt;get("template=home")-&gt;url);</code></pre>

And let’s do something if the current user is logged in:

<pre><code class="language-php">if ($user-&gt;isLoggedin()) { /* do something */ }</code></pre>

## Extending ProcessWire’s Functionality With Modules

ProcessWire is built on a <a href="https://processwire.com/api/modules/">modular and easily extendable architecture</a>, and it shows: Every installation consists of ProcessWire’s core (the essence of ProcessWire, which enables the basic functionality) and a set of prepackaged modules (so-called core modules) that sit on top of the core and extend it.</p>

### Core Modules

Some of these prepackaged modules are installed and activated by default, and <a href="https://processwire.com/blog/posts/processwire-2.6.19-plus-guide-to-optional-core-modules/#a-guide-to-optional-uninstalled-core-modules">others are uninstalled</a> by default. For example, ProcessWire’s <strong>built-in comment system</strong> is a module you can switch on or off at any time. Also, things like the <strong>repeater field</strong> we talked about earlier and the <strong>multi-language support</strong> for content are basically just modules you can install if you need them in your project.

Other examples of neat little core modules are <strong>Page Names</strong>, which validates text input when you’re typing a page name (automatically transforming, say, umlauts like <em>ä</em> to <em>ae</em>), and <strong>Page Path History</strong>, which keeps track of past URLs where pages have lived and automatically redirects to the new location whenever an old URL is accessed.</p>

### Finding and Installing Modules

The official <a href="https://modules.processwire.com/">modules repository</a> is the main spot where you can find and download ProcessWire modules. On a module’s page, you will find the description and purpose of the module and links to the respective GitHub repository and support forum. Module authors are highly encouraged to post their modules in the official repository because it has the highest visibility and is the place people think of first when they want to find a ProcessWire module.

Installing a module is as easy as dragging the module’s files to the <code>/site/modules/</code> directory and installing it in the admin GUI. There are other ways to install a module, such as by installing the <a href="https://modules.processwire.com/modules/modules-manager/">Modules Manager</a>, which enables you to browse (and install) modules without leaving the admin GUI.</p>

### Commercial Modules

While most modules are free, there are a few commercial ones, too. The ones being promoted in <a href="https://processwire.com/talk/store/">ProcessWire’s store</a> are by the lead developer, Ryan Cramer. There you will find the following modules:

*   [ProDrafts](https://processwire.com/api/modules/prodrafts/) enables you to maintain separate draft and live versions of any page. It also provides a comparison and diff tool, as well as automatic saving capabilities.
*   [ProFields](https://processwire.com/talk/store/product/10-profields/) are a group of ProcessWire modules that help you manage more data with fewer fields, saving you time and energy.
*   [ProCache](https://processwire.com/talk/store/product/6-procache-single/) (among other things) provides an impressive performance boost for your website by completely bypassing PHP and MySQL and enabling your web server to deliver pages of your ProcessWire website as if they were static HTML files.

Don’t miss the screenshots and videos on the module pages to get a first impression. This is finely executed software.

There are also commercial modules outside of the official website, such as <a href="https://www.padloper.pw/">Padloper</a>, an e-commerce platform built on top of ProcessWire. To be fair, what is definitely missing in the ProcessWire cosmos is a way for module authors to easily publish their commercial modules in a centralized spot.</p>

### How Do ProcessWire Modules Generally Compare to WordPress Plugins?

The reason why ProcessWire has so fewer modules than WordPress (approximately 400 versus more than 40,000) is not so much because it is <strong>less popular</strong> (an understatement, of course), but more because the core itself is <strong>already so feature-rich</strong> that adding a ton of modules to extend it is simply not necessary. For example, you don’t need a module to create a gallery slideshow or to get the first child of something or to generate thumbnails. All of that (and much more) is already covered out of the box.

So, whereas in WordPress your typical method of solving a problem would be to search for a plugin, in ProcessWire you would first look to the tools available in core; in 90% of cases, that would provide you with the solution.</p>

## What You Can Build With ProcessWire

Because ProcessWire behaves more like a framework than a CMS (the core is actually a framework, and the CMS is an application built on top of it), the use cases for building things with ProcessWire are pretty broad. You may want to check out some <a href="https://processwire.com/about/sites/">websites powered by ProcessWire</a> (especially the <a href="https://processwire.com/about/sites/sort--likes">most liked websites</a>).

ProcessWire is a good fit if you want to develop a JSON REST API, an image-resizing app for employees, a front end for managing millions of products (scalability is pretty impressive — you can have literally <a href="https://processwire.com/talk/topic/9491-site-with-millions-of-%E2%80%9Epages%E2%80%9D/">millions of pages</a> on a single installation), a web application for displaying the financial results of companies, a simple blog, a website for a big university, or just a simple one-page informational website.</p>

## Where To Go From Here: There’s A Lot To Discover

Naturally, a beginner’s guide can’t talk about everything the tool has to offer. So, here is a short list of other ProcessWire features, facts, links and tools worth mentioning:

*   Check out [ProcessWire Weekly](https://weekly.pw/) and [ProcessWire’s blog](https://processwire.com/blog/) to stay up to date on the latest news.
*   ProcessWire has built-in caching mechanisms (for example, a [template and markup cache](https://www.flamingruby.com/blog/processwire-caching-explained/)).
*   [Wireshell](https://wireshell.pw/) is a command-line interface for ProcessWire based on the Symphony Console component.
*   [Security](https://processwire.com/docs/security/) is a top priority for ProcessWire.
*   Visit [grab.pw](https://grab.pw/) (isn’t that the coolest domain name ever?) to download the latest stable version of ProcessWire (ZIP file, 10MB).
*   ProcessWire has a small and friendly community. The [discussion board](https://processwire.com/talk/) is the central place to discuss any questions and problems.
*   ProcessWire has good [multi-language support](https://processwire.com/api/multi-language-support/). The multi-language modules are part of the prepackaged core modules.
*   ProcessWire has a [transparent roadmap](https://processwire.com/about/roadmap/), and development is [very active](https://github.com/ryancramerdesign/ProcessWire/commits/devns). There is a new minor release nearly every week.
*   See what others have to say about ProcessWire in the [reviews section](https://processwire.com/about/processwire-reviews/) and on [alternativeTo](https://alternativeto.net/software/processwire/reviews/). There’s also an interesting Quora thread titled “[How does ProcessWire compare to WordPress](https://www.quora.com/How-does-Processwire-compare-to-Wordpress).”
*   [ProcessWire.tv](https://processwire.tv/) is a searchable collection of ProcessWire tutorial videos.</p>

## Summary

<blockquote>ProcessWire is a system that rewards you [for] being curious. We aim to show you how to fish so that you can catch the big fish.</blockquote>

<a href="https://processwire.com/talk/topic/7565-making-pw-more-userfriendly/page-8#entry73748">This statement</a> by Ryan Cramer, the creator of ProcessWire, encapsulates what ProcessWire is all about.

I think what resonates with a lot of people is that ProcessWire is a system that goes from simple to complex, not the other way around. It doesn’t assume what you want to build, but instead lays a strong, non-opinionated foundation by offering you effective, powerful tools and leaving the rest to you. That conceptual aesthetic has, to me, a certain appeal to it.

{{< signature "dp, al, il" >}}


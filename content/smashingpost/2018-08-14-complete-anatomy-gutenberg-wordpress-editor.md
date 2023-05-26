---
title: 'The Complete Anatomy Of The Gutenberg WordPress Editor'
slug: complete-anatomy-gutenberg-wordpress-editor
author: manish-dudharejia
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0565c7b5-a9fd-4809-9813-c393073bd60c/understanding-the-gutenberg-wordpress-editor-ghxszz.png
date: 2018-08-14T14:00:22+02:00
summary: >-
  An in-depth analysis of the new Gutenberg Editor and its impact on the WordPress web development. In this article, you’ll learn a few hands-on tricks that will prove useful especially if you are using Gutenberg for the first time.
description: >-
  An in-depth analysis of the new Gutenberg Editor and its impact on the WordPress web development. In this article, you’ll learn a few hands-on tricks that will prove useful especially if you are using Gutenberg for the first time.
categories:
  - WordPress
  - Plugins
---
It seems that Gutenberg has been a term of controversy in the world of WordPress lately. Hailed as the most significant change to [WordPress 5.0](https://make.wordpress.org/core/5-0/) this year, the Gutenberg editor has received a mixed response from web developers and regular folk alike. All of this chaos is making it difficult to see Gutenberg for what it really is. So, I’ll try to put some of the confusion to rest once and for all.

In this article, I will cover the following:

1. [What is Gutenberg?](#what-is-gutenberg)
2. [More Than Just An Editor](#more-than-just-an-editor)
3. [What Does Gutenberg Change In WordPress?](#what-does-gutenberg-change-in-wordpress)
4. [Installing Gutenberg](#installing-gutenberg)
5. [Exploring Gutenberg At Length](#exploring-gutenberg-at-length)
6. [Pros And Cons](#pros-and-cons)
7. [Understanding Compatibility Issues](#understanding-compatibility-issues)
8. [Gutenberg Is The Future](#gutenberg-is-the-future)
9. [Latest News And Further Resources](#latest-news-and-further-resources)

## 1. What Is Gutenberg? <a name="what-is-gutenberg"></a>

Named after Johannes Gutenberg, who invented the mechanical printing press, Gutenberg was introduced to the world by Matt Mullenweg at [WordCamp Europe in 2017](https://wordpress.tv/2017/07/01/interview-and-qanda-with-matt-mullenweg/). In essence, Gutenberg is a new WordPress editor, with dozens of cutting-edge features. It simplifies website creation and editing for the average non-technical user.

It has earned several accolades, from "WordPress’s new publishing experience" to “the future of website creation”. Some skeptics think it is the nail in the coffin for WordPress. All this babble aside, Gutenberg is going to be way more than just an editor for WordPress (which I will discuss next).

It allows website creators to build a website using blocks, which are small drag-and-drop units. Thus, it replaces the current inconsistent and distracting customization process. It also enables HTML tags such as `section` and `figure`, outputting solid HTML. At the time of writing, Gutenberg is still a plugin. However, the community is planning to merge it with WordPress 5.0 this year.

{{% feature-panel %}}

## 2. More Than Just An Editor <a name="more-than-just-an-editor"></a>

Gutenberg is more than just an editor because it allows you to handle website content in customizable chunks or blocks. You don’t need to be fluent in HTML or write shortcodes. You can control a website’s entire layout (both back end and front end) from a single console.

This new editor attempts to combine the best features from both page-builder plugins such as [Divi](https://www.elegantthemes.com/gallery/divi/) and [Visual Composer](https://visualcomposer.io/), as well as do-it-yourself platforms such as Medium, Wix and Squarespace. So, just like those page-builder plugins, you can handle multi-column layouts through a single interface.

Does this spell the end of plugins such as Divi and Beaver Builder? That’s a topic for another post, but the short answer is no. Gutenberg is unlikely to replace those plugins completely. You can continue to use them even once Gutenberg becomes the default editor.

## 3. What Does Gutenberg Change In WordPress? <a name="what-does-gutenberg-change-in-wordpress"></a>

The sole purpose of the Gutenberg editor is to provide an alternative to the current open text editor, not to mention the difficult-to-remember shortcodes, with an agile and visual user interface (UI). So, unlike the current WordPress editor, you don’t have to:

- import images, multimedia and approved files from the media library or add HTML shortcodes;
- copy and paste links for embeds;
- write shortcodes for specialized assets of different plugins;
- create featured images to be added at the top of a post or page;
- add excerpts for subheads;
- add widgets for content on the side of a page.

In short, Gutenberg doesn’t change how WordPress functions. It does, however, change the way website owners (or creators) interact with it. Instead of a whole lot of shortcodes and meta boxes, you will be using simple blocks.

#### What Are Blocks?

Consider a block as the most basic (therefore, smallest) unit of the new editor. They will be the building blocks of WordPress 5.0. In other words, everything—including content, images, quotes, galleries, cover images, audio, video, headings, embeds, custom codes, paragraphs, separators and buttons—will turn into distinct blocks. Because you can drag and drop each block, identifying these items and placing them on the page becomes a lot easier.

## 4. Installing Gutenberg <a name="installing-gutenberg"></a>

You can download the latest version of Gutenberg directly from the [WordPress repository](https://wordpress.org/plugins/gutenberg/). You can also search for it under "Add New" plugins in your WordPress dashboard. I would recommend installing it in your staging environment. However, you’ll need the latest version of WordPress ([version 4.8](https://codex.wordpress.org/Version_4.8) or later) to install the Gutenberg editor.

1. Sign into your WordPress admin dashboard.
2. Go to the Plugins menu on the left side of the dashboard.
3. Click "Plugins" to open the “Add New” menu.
4. Type "Gutenberg" in the search box, located in the top-left corner.
5. You will see the Gutenberg plugin in the results.
6. Click the "Install Now" button.
7. Click the "Activate" button to initiate the plugin.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12eab485-3be4-4bad-ba20-f1af3238d74d/gutenberg-editor-install-gutenberg.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12eab485-3be4-4bad-ba20-f1af3238d74d/gutenberg-editor-install-gutenberg.gif" width="1920" height="917" alt="Installing Gutenberg" /></a><figcaption>Gutenberg Installation Steps (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12eab485-3be4-4bad-ba20-f1af3238d74d/gutenberg-editor-install-gutenberg.gif">Large preview</a>)</figcaption></figure>

## 5. Exploring Gutenberg At Length <a name="exploring-gutenberg-at-length"></a>

Once installed and activated, Gutenberg will show an icon in the left menu bar. When you launch it for the first time, you will see a new sample post, titled "Gutenberg Demo." You can practice on the demo post before creating your own.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f1463c-c6b8-4e1e-82b2-12f49d0c9631/gutenberg-editor-gutenberg-demo.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f1463c-c6b8-4e1e-82b2-12f49d0c9631/gutenberg-editor-gutenberg-demo.jpg" sizes="100vw" caption="Gutenberg Sample Post (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92f1463c-c6b8-4e1e-82b2-12f49d0c9631/gutenberg-editor-gutenberg-demo.jpg'>Large preview</a>)" alt="Gutenberg Demo" >}}

### A. Add New

Go to "Posts" in the left menu bar of your WordPress dashboard. The new post will launch in Gutenberg first. You can later edit it in both the classic editor and Gutenberg.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d57febcc-ddc1-4309-bec0-a39b1b41105d/gutenberg-editor-add-new-post.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d57febcc-ddc1-4309-bec0-a39b1b41105d/gutenberg-editor-add-new-post.gif" width="1903" height="939" alt="Adding a new post in Gutenberg" /></a><figcaption>Adding a new post in Gutenberg (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d57febcc-ddc1-4309-bec0-a39b1b41105d/gutenberg-editor-add-new-post.gif">Large preview</a>)</figcaption></figure>

### B. Edit

Go to the "Posts" menu, and hover the mouse over a saved post to see the option to choose between the two editors. Although the classic editor option is available for the time being, it will most likely be removed with the launch of WordPress 5.0.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10f2be0a-f68d-4d3a-81ff-4f09244a0902/gutenberg-editor-edit-post.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10f2be0a-f68d-4d3a-81ff-4f09244a0902/gutenberg-editor-edit-post.gif" width="1903" height="939" alt="Editing a post in Gutenberg" /></a><figcaption>Editing a post in Gutenberg (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10f2be0a-f68d-4d3a-81ff-4f09244a0902/gutenberg-editor-edit-post.gif">Large preview</a>)</figcaption></figure>

### C. Switch Between Editors

You can also switch between the two editors when editing a post. Click on the dropdown menu in the upper-right corner to toggle between the visual editor mode and the text editor (i.e. code). Alternatively, you can also use the shortcut <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>M</kbd> to switch between editors.

Text editor:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242af93b-0b8e-4acd-bbbd-b4bdf8cbaf24/gutenberg-editor-code-editor.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242af93b-0b8e-4acd-bbbd-b4bdf8cbaf24/gutenberg-editor-code-editor.jpg" sizes="100vw" caption="The text editor in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/242af93b-0b8e-4acd-bbbd-b4bdf8cbaf24/gutenberg-editor-code-editor.jpg'>Large preview</a>)" alt="The text editor in Gutenberg" >}}

Visual editor:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abd80a2a-d19b-42bb-9569-b5cf7121df5f/gutenberg-editor-visual-editor.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abd80a2a-d19b-42bb-9569-b5cf7121df5f/gutenberg-editor-visual-editor.jpg" sizes="100vw" caption="The visual editor in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abd80a2a-d19b-42bb-9569-b5cf7121df5f/gutenberg-editor-visual-editor.jpg'>Large preview</a>)" alt="The visual editor in Gutenberg" >}}

### D. Copy All Content

This feature allows you to copy all content in the HTML version with just one click. You can open this feature in both editors by clicking on the dropdown menu in the upper-right corner of the dashboard.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0290178-b853-4496-b928-c30d372b22c0/gutenberg-editor-copy-all-content.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0290178-b853-4496-b928-c30d372b22c0/gutenberg-editor-copy-all-content.gif" width="1903" height="939" alt="The ‘Copy All Content’ tool in Gutenberg" /></a><figcaption>“ The ‘Copy All Content’ tool in Gutenberg (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0290178-b853-4496-b928-c30d372b22c0/gutenberg-editor-copy-all-content.gif">Large preview</a>)</figcaption></figure>

### E. Content Structures

This feature allows you to count the number of words in an entire post. You can also see the number of headings, paragraphs and blocks with just a click. Click the information icon (i) in the upper-left area.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64b9fe7a-6b6f-4be0-a57e-d6792ad1dd5d/gutenberg-editor-content-structures.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64b9fe7a-6b6f-4be0-a57e-d6792ad1dd5d/gutenberg-editor-content-structures.jpg" sizes="100vw" caption="Content information in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64b9fe7a-6b6f-4be0-a57e-d6792ad1dd5d/gutenberg-editor-content-structures.jpg'>Large preview</a>)" alt="Content Structures" >}}

### F. Redo and Undo

You can find these options next to the information icon (i). They allow you to undo or redo the last command.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/978348a9-0ba3-489d-bbd3-3f9820230d29/gutenberg-editor-undo-redo.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/978348a9-0ba3-489d-bbd3-3f9820230d29/gutenberg-editor-undo-redo.jpg" sizes="100vw" caption="Undo&#47;Redo Command (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/978348a9-0ba3-489d-bbd3-3f9820230d29/gutenberg-editor-undo-redo.jpg'>Large preview</a>)" alt="Undo and Redo command" >}}

### G. Page and Document Settings

This allows you to change various page and document settings. You can find it in the right menu bar. You can make the following adjustments:

- Make a post public or private.
- Change the publishing date.
- Select a post’s format.
- Add or edit categories and tags.
- Upload featured images.
- Write an excerpt.
- Enable and disable comments, pingbacks and trackbacks.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e17825da-447e-4209-827e-f6e3c6374baf/gutenberg-editor-page-document-settings.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e17825da-447e-4209-827e-f6e3c6374baf/gutenberg-editor-page-document-settings.jpg" sizes="100vw" caption="Page&#47;Document Settings (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e17825da-447e-4209-827e-f6e3c6374baf/gutenberg-editor-page-document-settings.jpg'>Large preview</a>)" alt="Page and Document Settings" >}}

### H. Stick to Front Page

This feature will come handy if you’re running a blog. When you turn this on in the document settings, that particular post will always appear on the front page of your blog. And just turn it off to remove it from the front page.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41bb418f-98ba-4059-80c7-1e6da025dcb9/gutenberg-editor-stick-to-front-page.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41bb418f-98ba-4059-80c7-1e6da025dcb9/gutenberg-editor-stick-to-front-page.gif" width="1903" height="939" alt="Making your post stick to the front page" /></a><figcaption>Making your post stick to the front page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41bb418f-98ba-4059-80c7-1e6da025dcb9/gutenberg-editor-stick-to-front-page.gif">Large preview</a>)</figcaption></figure>

### I. Using Blocks

As mentioned, blocks are the fundamental unit of the new Gutenberg editor. To use Gutenberg efficiently, you need to understand how to use these blocks. I will cover the main blocks one by one. Click the plus (+) button next to the redo/undo option to open the blocks menu.

#### Common Blocks

Common blocks allow you to add the elements required to create a rich UI.

- **Paragraph**  
The paragraph block comes with a few excellent features, such as custom font sizes, drop caps, background colors and text colors, among others. You are also able to add more CSS classes here.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c818f2ac-170e-433f-89cf-485ca20dc311/gutenberg-text-editor-options.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c818f2ac-170e-433f-89cf-485ca20dc311/gutenberg-text-editor-options.jpg" sizes="100vw" caption="Gutenberg Text Editor Options (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c818f2ac-170e-433f-89cf-485ca20dc311/gutenberg-text-editor-options.jpg'>Large preview</a>)" alt="Gutenberg Text Editor Options" >}}

- **Image**  
This element comes with a new feature that allows you to toggle between gallery and image layouts. You also get more control over images because you can set particular size dimensions, percentage size ratios, and an alternative text description for each image.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c7f3656-81e9-4f5b-8465-b8e1823663de/gutenberg-editor-image-settings.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c7f3656-81e9-4f5b-8465-b8e1823663de/gutenberg-editor-image-settings.jpg" sizes="100vw" caption="Image Settings in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c7f3656-81e9-4f5b-8465-b8e1823663de/gutenberg-editor-image-settings.jpg'>Large preview</a>)" alt="Image Settings in Gutenberg" >}}

- **Other elements include**:
	- quotes,
	- galleries,
	- cover images,
	- headings,
	- lists,
	- audio,
	- files,
	- subheadings,
	- video.

{{% ad-panel-leaderboard %}}

#### Formatting

As the name suggests, these blocks comprise all of the formatting tools.

- **Table**  
Adding a table using custom HTML code was a tedious job. With the table block, however, the task is a lot easier. You are able to add and remove rows and columns of a table without coding.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c962ec4-f25c-413b-a93f-a0021db19fef/gutenberg-editor-table-format.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c962ec4-f25c-413b-a93f-a0021db19fef/gutenberg-editor-table-format.jpg" sizes="100vw" caption="Table Block in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c962ec4-f25c-413b-a93f-a0021db19fef/gutenberg-editor-table-format.jpg'>Large preview</a>)" alt="Table Block in Gutenberg" >}}

- **Custom HTML**  
You can use a custom HTML code in Gutenberg. And the nice part is that you can insert your code and see a preview in the block itself.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4282b849-089a-491d-ab14-01a9a7bfa855/gutenberg-editor-custom-html.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4282b849-089a-491d-ab14-01a9a7bfa855/gutenberg-editor-custom-html.gif" width="1903" height="939" alt="Custom HTML in Gutenberg" /></a><figcaption>Custom HTML in Gutenberg (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4282b849-089a-491d-ab14-01a9a7bfa855/gutenberg-editor-custom-html.gif">Large preview</a>)</figcaption></figure>

- **Other elements include**:  
	- code,
	- classic,
	- preformatted,
	- pull quote,
	- verse.

#### Layout

Use your imagination to create a stunning layout using this block. Each element in this block comes with excellent features.

- **Button**  
You can add buttons such as "Subscribe now" and “Buy now” using this block. It has different options, including alignment and font styles. You can also set the background color and shape of the button.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38e979be-78e0-4fea-829f-ce3c9ac9da3f/gutenberg-editor-button-layout.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38e979be-78e0-4fea-829f-ce3c9ac9da3f/gutenberg-editor-button-layout.jpg" sizes="100vw" caption="Button Layout in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38e979be-78e0-4fea-829f-ce3c9ac9da3f/gutenberg-editor-button-layout.jpg'>Large preview</a>)" alt="Button Layout in Gutenberg" >}}

- **Columns (beta)**  
Creating columns in the code-based editor is time-consuming and laborious. This block allows you to add text columns. You are able to add one to six columns in a single row.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86072526-97af-4f7e-9e12-6f0209b27657/gutenberg-editor-column-layout.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86072526-97af-4f7e-9e12-6f0209b27657/gutenberg-editor-column-layout.jpg" sizes="100vw" caption="Column Layout in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86072526-97af-4f7e-9e12-6f0209b27657/gutenberg-editor-column-layout.jpg'>Large preview</a>)" alt="Column Layout in Gutenberg" >}}

- **Other elements include**:  
	- read more,
	- page break,
	- separator,
	- spacer.

#### Widgets

These blocks allow you to add an archive, categories, the latest posts and the latest comments with just a click anywhere on the page. You are also able to adjust these elements without any coding.

- **Latest Post**  
With this block element, you can show posts in a grid view or list view, organize them in categories, and order them alphabetically or according to publication date. You can also choose to display the publication date.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5180c984-286b-428b-8a59-a21a585e091c/gutenberg-editor-latest-posts.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5180c984-286b-428b-8a59-a21a585e091c/gutenberg-editor-latest-posts.jpg" sizes="100vw" caption="Latest Posts Setting in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5180c984-286b-428b-8a59-a21a585e091c/gutenberg-editor-latest-posts.jpg'>Large preview</a>)" alt="Latest Posts Setting in Gutenberg" >}}

#### Embeds

You can easily access any embeds using these blocks. Whether you want to add a YouTube or Twitter link, it’s super-easy and quick. All you need to do is paste the URL in the given blank space, and Gutenberg will embed the code for you. Here is an example of inserting a YouTube link:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09fce3e7-ff57-4d9d-bf2f-168439ff1c45/gutenberg-editor-embeds.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09fce3e7-ff57-4d9d-bf2f-168439ff1c45/gutenberg-editor-embeds.gif" width="1903" height="939" alt="Embed Youtube Link in Gutenberg" /></a><figcaption>Embed Youtube Link in Gutenberg (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09fce3e7-ff57-4d9d-bf2f-168439ff1c45/gutenberg-editor-embeds.gif">Large preview</a>)</figcaption></figure>

#### Reusable Blocks

Reusable blocks give developers improved usability. You can convert any block into a reusable block so that you can use it in a different location. You can edit the same and save it as a new reusable block again.

You can also see a preview of a reusable block. All reusable blocks are available under the "Shared Block" options. Most importantly, you can turn one back into a regular block anytime.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44e3c1e4-9a59-4c01-9919-b7a00f072354/gutenberg-editor-reusable-blocks.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44e3c1e4-9a59-4c01-9919-b7a00f072354/gutenberg-editor-reusable-blocks.gif" width="1903" height="939" alt="Reusable Blocks in Gutenberg" /></a><figcaption>Reusable Blocks in Gutenberg (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44e3c1e4-9a59-4c01-9919-b7a00f072354/gutenberg-editor-reusable-blocks.gif">Large preview</a>)</figcaption></figure>

#### Most Used

Under this option, you will see the most used blocks, for quick access. Alternatively, you can use the search box to find a block by name.

#### J. Edit Block

To edit any block, open the dropdown menu by clicking in the upper-right corner of the block. You will see different options, including to edit as HTML, duplicate and add to the reusable blocks.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4eec69a-a4dc-4302-80fb-cdea8f738685/gutenberg-editor-edit-block.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4eec69a-a4dc-4302-80fb-cdea8f738685/gutenberg-editor-edit-block.jpg" sizes="100vw" caption="Edit Block in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4eec69a-a4dc-4302-80fb-cdea8f738685/gutenberg-editor-edit-block.jpg'>Large preview</a>)" alt="Edit Block in Gutenberg" >}}

#### K. Insert Blocks

Using this feature, you can insert a new block anytime. When you bring your mouse over a block, you will see a plus icon (+). Click it to insert a new block.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57bc414e-1993-47e5-96c5-bcd6374f3e1f/gutenberg-editor-insert-block.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57bc414e-1993-47e5-96c5-bcd6374f3e1f/gutenberg-editor-insert-block.jpg" sizes="100vw" caption="Inserting a block in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57bc414e-1993-47e5-96c5-bcd6374f3e1f/gutenberg-editor-insert-block.jpg'>Large preview</a>)" alt="Insert Block in Gutenberg" >}}

#### L. Slash Autocomplete

The Slash Autocomplete feature is available in Gutenberg 1.1.0 and later versions. Chances are you are already familiar with the similar feature in Slack. It was added to reduce the amount of pointing and clicking required to create new blocks.

When you open a new block, just press <kbd>/</kbd> (slash key) on your keyboard to select any of the autocomplete options. It works in the default paragraph block only, but it might become a part of other types of blocks in the future.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fe2e765-6714-4b3b-8f58-c457849ce458/gutenberg-editor-slash-autocomplete.gif"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fe2e765-6714-4b3b-8f58-c457849ce458/gutenberg-editor-slash-autocomplete.gif" width="1903" height="939" alt="Slash Autocomplete in Gutenberg" /></a><figcaption>Slash Autocomplete in Gutenberg (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fe2e765-6714-4b3b-8f58-c457849ce458/gutenberg-editor-slash-autocomplete.gif">Large preview</a>)</figcaption></figure>

#### M. Move Blocks

Gutenberg enables you to move each block up and down. You can use the arrows (on the left side of each block) to move them vertically.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/571acb8a-0066-4214-aa10-fc156108bd24/gutenberg-editor-move-block.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/571acb8a-0066-4214-aa10-fc156108bd24/gutenberg-editor-move-block.jpg" sizes="100vw" caption="Moving a block in Gutenberg (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/571acb8a-0066-4214-aa10-fc156108bd24/gutenberg-editor-move-block.jpg'>Large preview</a>)" alt="Move Block in Gutenberg" >}}

## 6. Gutenberg Pros And Cons <a name="pros-and-cons"></a>

### Pros

- No technical skill is required to make a custom layout for a blog post or website. It works like [Medium](https://medium.com/), so people looking for that kind of style and user-friendly editing experience will love it.
- It allows you to create a consistent and advanced design without relying much on [TinyMCE](https://www.tiny.cloud/).
- Furthermore, blocks are an excellent concept. They allow non-developers to intuitively craft complex layouts. If you are new to WordPress or have no knowledge of it whatsoever, you are still going to love it.
- The Gutenberg editor itself works well on mobile (it’s responsive). Unlike its predecessor, it allows you to make quick edits on the go. In fact, mobile-savvy developers can manage to do more than just a few quick edits.
- The increased screen space is proving to be a less distracting user experience for many developers.
- Hardcore developers can still create customized reusable blocks using HTML5. So, it seems like a win-win for both geeks and non-technical users.

### Cons

- For the time being, there is no Markdown support in the beta version of the WordPress editor.
- It still doesn’t support responsive columns. You will need to do some custom coding to make this feature responsive. So, using this feature on mobile isn’t an option right now.
- The design layout options are inadequate at the moment.
- Compatibility issues could be a significant concern for some WordPress users.
- You get only partial support for meta boxes, however, developers are working hard to extend meta box support.
- [Backward compatibility](https://en.wikipedia.org/wiki/Backward_compatibility) is going to be a primary concern for most developers. It will destroy current plugins and themes, especially ones that require integration with TinyMCE.

{{% ad-panel-leaderboard %}}

## 7. Understanding Compatibility Issues <a name="understanding-compatibility-issues"></a>

Despite its simplicity and agility, Gutenberg might not be everyone’s cup of tea. Most WordPress developers might find it difficult to work with, especially in the beginning. They will need to retrain their reflexes to get used to the new UX.

- Owing to the backward-compatibility issue, you will need to update many plugins and themes to ensure they are fully compatible with the new editor.
- For the time being, blocks are more focused on content. As a result, Gutenberg lacks precision and control over the layout of custom websites.
- Shortcodes are replaced by shortcode blocks. However, you will still be able to add shortcodes from the widget block.
- Meta boxes will be available under a new name and a new UI. Conflicting meta boxes are likely to lead to the classic editor, instead of Gutenberg, with an alert. While this system might prove helpful, some meta boxes will not be supported in Gutenberg.
- Custom post types are supported and remain backward-compatible in Gutenberg.
- You won’t be able to turn off Gutenberg once it is integrated in WordPress core. However, you can disable it using the [official plugin](https://wordpress.org/plugins/classic-editor/) anytime.

## 8. Gutenberg Is The Future <a name="gutenberg-is-the-future"></a>

Contrary to popular opinion, Gutenberg is not a replacement for the current text editor. It is a new way to build websites. I like to think of it as Facebook for WordPress.

You don’t need to be a computer geek to publish things on Facebook or any other social media platform. Gutenberg is just a way to bring this simplicity and flexibility to WordPress, so that people don’t need to code in order to create and publish websites. That’s why I think it is going to be the future, not only for WordPress, but for the web in general.

Granted, Gutenberg has a long way to go. People (including me) have had issues with its implementation, but soon we will have Gutenberg-ready themes, plugins and tools surfacing everywhere. Nevertheless, you have to start somewhere. So, you might as well be a part of this change from the beginning.

## 9. Latest News And Further Resources <a name="latest-news-and-further-resources"></a>

If you are interested in riding the Gutenberg train from the beginning, here are a few links to find the latest buzz. Keep in mind that none of these websites are officially endorsed by WordPress.

- [Gutenberg News](https://gutenberg.news/)
- [Gutenberg Hub](https://gutenberghub.com/)
- [Gutenberg Times](https://gutenbergtimes.com/)

For official updates and news, you can try the following:

- “[Gutenberg, Or The Ship Of Thesus](https://matiasventura.com/post/gutenberg-or-the-ship-of-theseus/),” Matías Ventura Bausero
- “[Editor Technical Overview](https://make.wordpress.org/core/2017/01/17/editor-technical-overview/),” Matías Ventura Bausero, WordPress.org
- “[Design Principles](https://wordpress.org/gutenberg/handbook/contributors/design/),” WordPress.org
- “[wp-post-grammar](https://github.com/Automattic/wp-post-grammar),” Dennis Snell
- “[#gutenberg (Dev Chat Summary: June 27th)](https://make.wordpress.org/core/tag/gutenberg/),” Jeffrey Paul
- “[Introduction To Gutenberg](https://wordpress.org/gutenberg/handbook/),” WordPress.org

## Wrapping Up

Whether you like it or not, Gutenberg is coming to WordPress 5.0. Do try to be a part of the ongoing discussion about it on the web. It will certainly help. In fact, while you’re at it, try to speed up the development process with your skills. Meanwhile, let me know if this post has shed some light on the topic. Drop your queries and suggestions in the comments section. I would love to keep the conversation going.

{{< signature "ra, il" >}}
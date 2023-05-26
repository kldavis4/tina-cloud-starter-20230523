---
title: 'Exploring New Ways To Manage Content In WordPress'
slug: exploring-new-ways-manage-content-wordpress
author: leonardolosoviz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e23f31fe-3894-4983-a0d5-6ff96e09b513/exploring-new-ways-manage-content-wordpress.png
date: 2019-11-07T11:30:59+02:00
summary: >-
  Gutenberg is reinventing the experience of creating content in WordPress, granting it new powers to create, edit and manage our content. Let’s see what these new powers are.
description: >-
  Gutenberg is reinventing the experience of creating content in WordPress, granting it new powers to create, edit and manage our content. Let’s see what these new powers are.
categories:
  - WordPress
  - Coding
---
<p>The combination of WordPress’ versatility for managing data (since its database model supports the creation of different content models, easily extensible through meta attributes) and <a href="https://www.smashingmagazine.com/2019/10/postmortem-gutenberg-launch-product/">Gutenberg</a>’s rich user interactions provide a powerful mechanism to create, edit and manage content.</p>

<p>In this article, I want to shine some light on these upgraded capabilities, exploring the new tools at our disposition and presenting several new ones to be released sometime in the future.</p>

## Existing Features

<p>The following features are already part of Gutenberg-powered WordPress.</p>

### Create Once, Publish Everywhere

<p>As I have described in my recent article <a href="https://www.smashingmagazine.com/2019/10/create-once-publish-everywhere-wordpress/">“Create Once, Publish Everywhere” with WordPress</a>, the block-based nature of Gutenberg enables it to enhance how content is organized/architected on the database, making it available on a granular basis (block by block) to any application running on any medium or platform (web, email, iOS/Android apps, VR/AR, home assistants, and so on). Content managed through Gutenberg can then become the single source of truth for all of our applications, allowing us to reduce the cost associated with re-formatting content to make it suitable for each required platform.</p>

### Copy/paste from Google Docs with (almost) perfect formatting

<p>Whenever we need to collaborate with other people to create content, we will quite likely use online tools such as <a href="https://docs.google.com">Google Docs</a>, <a href="https://paper.dropbox.com">Dropbox Paper</a>, <a href="https://coda.io">Coda</a> or others. These tools make it easy for different people to edit the content in a document concurrently and provide and incorporate feedback. If we are going to choose a Content Management System to store our content, we need to make sure that it works well with these tools.</p>

{{% feature-panel %}}

<p>Gutenberg does the job fairly well: When copying the content from a Google Doc and then pasting it into a Gutenberg blog post, the formatting is preserved, bullet lists are properly transformed to the list block, and images are inserted where they should. There may be a few inconsistencies (for instance different spacing across blocks and in the original document) however, for the most part, the process is fit for use.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28ea7e0b-0423-4309-977f-6870a3809c28/copy-paste-gdoc.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f58a80ad-d85c-4eea-86ac-9f50f51811a8/copy-paste-gdoc-800w.gif" width="800" height="" alt="Copy/pasting from GDoc to Gutenberg" /></a><figcaption>Copy/pasting from GDoc preserves the format of the document. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28ea7e0b-0423-4309-977f-6870a3809c28/copy-paste-gdoc.gif">Large preview</a>)</figcaption></figure>

### Crafting art direction

<p>Several Gutenberg blocks support creating distinctive and engaging layouts and assisting the <a href="https://www.smashingmagazine.com/2019/04/art-direction-for-the-web-using-css-shapes/">art direction</a> of the site, to give it more personality and emphasize its identity. This way, even though we may base the site on a standard, plain-looking WordPress theme, we can customize the content’s appearance to make it stick out from the sea of sameness out there on the web. Let’s explore some of these blocks.</p>

<p>The <a href="https://wordpress.org/plugins/coblocks/">Shape divider</a> block allows to insert dividers in between two blocks. We can choose one among several basic shapes and customize its width, proportions and colors and then, with a bit of resourcefulness, create more intrinsic patterns from it. For instance, the divider below was created by first creating and customizing a divider, then flipping it both vertically and horizontally to mirror itself, then grouping these 2 halves so we can use it as a single unit (the grouping functionality will be available in core through the <a href="https://wordpress.org/news/2019/11/wordpress-5-3-rc4/">release of WordPress 5.3</a> next week, and is currently available through the <a href="https://wordpress.org/plugins/gutenberg/">Gutenberg plugin</a>), and finally saving the grouped block as a reusable block so it can be used everywhere across the whole site:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49bf059f-5e4e-4b21-b907-6b1969a4783f/divider-block.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49bf059f-5e4e-4b21-b907-6b1969a4783f/divider-block.jpg" sizes="100vw" caption="The shape divider block connects, or breaks apart, components. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49bf059f-5e4e-4b21-b907-6b1969a4783f/divider-block.jpg'>Large preview</a>)" alt="Shape divider block" >}}

<p>The <a href="https://wordpress.org/plugins/ultimate-addons-for-gutenberg/">Advanced columns</a> and <a href="https://wordpress.org/plugins/kadence-blocks/">Row layout</a> blocks allow to create row-based layouts, inside of which we can place nested blocks (i.e. any other Gutenberg block). They are highly configurable: They offer to define how many columns the row must have, with what padding, margin and proportion of width for each column, setting an image or custom color in the background, and several other attributes.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abae37b2-5d3f-4b7b-8737-9d19ae6208e4/row-layout-block.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abae37b2-5d3f-4b7b-8737-9d19ae6208e4/row-layout-block.jpg" sizes="100vw" caption="The row layout block allows to easily configure the proportion of width among columns. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abae37b2-5d3f-4b7b-8737-9d19ae6208e4/row-layout-block.jpg'>Large preview</a>)" alt="Row layout block" >}}

<p>We can also create grid-based layouts with predefined content. For instance, through the <a href="https://wordpress.org/plugins/ultimate-addons-for-gutenberg/">Post grid, Post carousel and Post masonry</a> blocks we can display a list of posts in different ways, defining what attributes from each post to show (title, date, excerpt, author, and so on), and through the <a href="https://wordpress.org/plugins/kadence-blocks/">Advanced gallery</a> block we can create beautiful image galleries.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95cc313a-b4d1-49a7-aebf-6f636ba4101c/advanced-gallery-block.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95cc313a-b4d1-49a7-aebf-6f636ba4101c/advanced-gallery-block.jpg" sizes="100vw" caption="Masonry gallery created with Advanced gallery block. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95cc313a-b4d1-49a7-aebf-6f636ba4101c/advanced-gallery-block.jpg'>Large preview</a>)" alt="Advanced gallery block" >}}

<p>Some other blocks, such as <a href="https://wordpress.org/plugins/stackable-ultimate-gutenberg-blocks/">Feature grid</a>, allow to create grid layouts with predefined templates filled with custom content.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0ea8c1-abf7-4f55-be98-2058a22cba2e/feature-grid-block.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0ea8c1-abf7-4f55-be98-2058a22cba2e/feature-grid-block.jpg" sizes="100vw" caption="The feature grid block enables to add custom content inside of a grid layout. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0ea8c1-abf7-4f55-be98-2058a22cba2e/feature-grid-block.jpg'>Large preview</a>)" alt="Feature grid block" >}}

<p>These are just a sample of those blocks which can help us fill the content with visually attractive layouts and craft the art direction of our sites. To keep exploring possibilities, we can head to the <a href="https://wordpress.org/plugins/browse/blocks/">directory of plugins offering blocks</a> and check these out.</p>

### Assisting the user while editing content

<p>Gutenberg assists the user when creating content through the following features:</p>

#### Real-Time Preview

The Gutenberg editor gives a relatively accurate preview of how the content will look like in the website.</p>

#### Error Warnings

Gutenberg makes the content creator be aware of accessibility concerns. For instance, if our content structure jumps from an <code>&lt;h2&gt;</code> header to an <code>&lt;h4&gt;</code> one without adding an <code>&lt;h3&gt;</code> tag in between, Gutenberg provides a warning message about this potential error. Similarly, when setting up the color of some text against its background color, if the contrast between the two colors is not clear enough then Gutenberg provides a warning message and helps fix the problem.</p>

#### Suggesting/Executing Improvements

Blocks can connect to third-party services to analyze content and enhance it. For instance, a service could suggest how to improve the grammar of the content, provide alternative titles and tags for a better SEO, and even automatically translate the content to another language, as done by <a href="https://wordpress.org/plugins/wphindi/">this plugin</a> which automatically translates from English to Hindi as the user types.</p>

{{% ad-panel-leaderboard %}}

## New Features Under Implementation

<p>The following features will hopefully/eventually be coming to Gutenberg in the future.</p>

### Snap to grid when resizing images

<p>Contributors are already working on <a href="https://github.com/WordPress/gutenberg/issues/16271">adding a grid system to Gutenberg</a> which will, among other things, enable to resize images in an assisted manner by snapping it to the grid:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc665fd4-2c0c-4945-a0a6-1318d2fa8385/snap-to-grid.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc665fd4-2c0c-4945-a0a6-1318d2fa8385/snap-to-grid.gif" width="800" height="" alt="Installing a block from within Gutenberg" /></a><figcaption>Snapping an image to grid (image from the GitHub issue). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc665fd4-2c0c-4945-a0a6-1318d2fa8385/snap-to-grid.gif">Large preview</a>)</figcaption></figure>

### Inline installation of blocks

<p>Sometimes, while we are writing a blog post, we find out that we need some functionality that we don’t have yet installed. Hence, we need to switch to the Plugins screen, search and install the corresponding plugin, and then go back to the blog post. This process adds friction to our content-writing workflow.</p>

<p>Wouldn’t it be nicer if we could install the required functionality right from within the editor itself, whenever we need to use it? Well, this proposal is already being implemented through <a href="https://github.com/WordPress/gutenberg/pull/16524">this pull request</a> (it first depends on blocks being <a href="https://make.wordpress.org/meta/2019/03/08/the-block-directory-and-a-new-type-of-plugin/">installed on their own</a>, i.e. without depending on being shipped through a plugin). Once merged, our content-writing workflow will not be impaired anymore, as visible in the mockup below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/529698e8-a492-4af1-ab73-a99efe3a8a2b/install-block.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/529698e8-a492-4af1-ab73-a99efe3a8a2b/install-block.gif" width="800" height="" alt="Installing a block from within Gutenberg" /></a><figcaption>Installing a block from within Gutenberg (image from the GitHub pull request). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/529698e8-a492-4af1-ab73-a99efe3a8a2b/install-block.gif">Large preview</a>)</figcaption></figure>

<p>Installing blocks directly from the editor could lead to unintended bloat, from making it too easy for the user to install blocks. To address this issue, after installing and using it, the block could be removed! This was not possible before Gutenberg, because if the plugin providing a shortcode (which was the way to render dynamic content inside the blog post before Gutenberg) was disabled, then the invocation of the shortcode would be rendered in the blog post (instead of the shortcode’s output), messing up our content. However, Gutenberg works differently: Blocks only save HTML content inside of the blog post (including HTML comments to store configuration attributes), so, if the block is disabled, its intended HTML output is still part of the blog post’s content. (Even though there may be problems if the block needs to load CSS assets which are not loaded anymore once the block is disabled. I am not aware how this issue will be handled.)</p>

### Page/Site builder

<p>Currently Gutenberg can only be used for the creation of content inside a blog post or a page, however it will soon support the creation of any part of the website: <a href="https://make.wordpress.org/core/2019/09/05/defining-content-block-areas/">Content-block areas</a> can define the header, sidebars, footer or any section needed for our layouts. <a href="https://automattic.com">Automattic</a> (the company behind <a href="https://wordpress.com">WordPress.com</a>) is already working on a <a href="https://wordpress.org/plugins/full-site-editing/">plugin to add full site editing capabilities</a> to its WordPress.com product, which should eventually be extensible to the <a href="https://wordpress.org">open source WordPress software</a> too.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2d608d9-206d-45fc-9867-45365c37c279/full-site-editing.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2d608d9-206d-45fc-9867-45365c37c279/full-site-editing.jpg" sizes="100vw" caption="Creating a new page with full site editing allows to select a page template. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2d608d9-206d-45fc-9867-45365c37c279/full-site-editing.jpg'>Large preview</a>)" alt="Creating a new page with full site editing enabled" >}}

### Real-time collaboration

<p>Google Docs is incredibly useful to teams because it enables their members to work on the same document at the same time. Sometime in the future, Gutenberg will also incorporate a <a href="https://github.com/WordPress/gutenberg/issues/1930">mechanism for real-time collaboration</a>, allowing different people to work on the same blog post at the same time. This mechanism will (at least initially) be based on giving editing-locks to users on a block-by-block basis, as shown in the mockup image below.</p>

{{< rimg  href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/404ca96b-88be-4afc-81bc-435fd3256c5c/collaborative-editing.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/404ca96b-88be-4afc-81bc-435fd3256c5c/collaborative-editing.png" sizes="100vw" caption="Real-time collaboration through Gutenberg (image from the GitHub issue). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/404ca96b-88be-4afc-81bc-435fd3256c5c/collaborative-editing.png'>Large preview</a>)" alt="Real-time collaboration through Gutenberg" >}}

<p>This feature will be particularly useful to online magazines (such as the New York Times and the like) since they may already have teams collaborating on a story (for instance, designers dealing with images, journalists, proofreaders and editors dealing with content, and others). Having real-time collaboration tools will enable these magazines to speed up their content-creation workflows and publish their articles faster.</p>

{{% ad-panel-leaderboard %}}

### Translation

<p>WordPress core has never added support to translate content (it only supports translation of strings inside of core, plugin and theme files), but instead left this responsibility to plugins. Through Gutenberg, WordPress will finally add native support for this feature.</p>

<p>Translation is not a priority yet, so it has been targeted for Gutenberg phase 4, expected in the year 2020+. Since it is a long way off, there are yet no technical considerations of its implementation or mockups of its intended user experience. So we can only guess how it will be. Since it will be implemented after the real-time collaboration feature (described above), I would expect it will enable different people to translate the same blog post to different languages at the same time, block by block.</p>

### Inline media editing

<p>Through the Media Library, WordPress already provides some image editing capabilities: resizing, cropping, rotating and flipping. These capabilities are very basic, and they are applied on to the image on a different screen, which creates some friction to the process of fitting the image into the blog post.</p>

<p>Through Gutenberg, the media-editing experience could be greatly enhanced: One one side, it could support editing the image in more advanced ways, such as applying effects or filters, altering the contrast, replacing colors, adding text as watermark, adding transparent regions, converting it to different formats, and others (for instance, Cloudinary <a href="https://cloudycam.dev/awais">provides an API to apply many transformations to an image</a>, which could be perfectly accessed by a block). On the other side, the editing could happen inline, right where the image is placed inside the blog post. Then, for instance, if the image was added as an overlay against some background, and we add transparent regions to the image, we can visualize in real-time how the composite result looks like.</p>

<p>(I haven’t found any proposal to tackle this issue in <a href="https://github.com/WordPress/gutenberg/issues">Gutenberg’s GitHub repo</a>, but I learned about this idea talking to some core contributors, who expected to be able to work on it some time in the future.)</p>

## Conclusion

<p>Already being the most popular CMS (<a href="https://w3techs.com/technologies/history_overview/content_management/all">close to 35% of the web</a>), WordPress has also the chance to offer the most compelling tools to manipulate content. This is because Gutenberg offers an appealing mechanism to create, edit and manage content: A single interface, simple to use, fairly powerful and versatile. With its new content management capabilities, WordPress can become the single source of truth of all our content, to power all our applications (websites, newsletters, apps, and so on) through APIs. Kudos to that!</p>

{{< signature "yk, il" >}}

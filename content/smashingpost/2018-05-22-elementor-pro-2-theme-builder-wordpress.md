---
title: 'How To Reduce The Need To Hand-Code Theme Parts In Your WordPress Website'
slug: elementor-pro-2-theme-builder-wordpress
author: nickbabich
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58c5aafd-f71a-4eab-b40e-794659092b0d/17-elementor-pro-theme-builde-800w.png
date: 2018-05-22T11:45:05+02:00
summary: >-
  The process of content management should be as easy as possible for everyone involved. Introducing Elementor, a tool that offers flexibility to visually design an entire website.
description: >-
  The process of content management should be as easy as possible for everyone involved. Introducing Elementor, a tool that offers flexibility to visually design an entire website.
categories:
  - WordPress
  - Plugins
  - Themes
---
<p>(<em>This is a sponsored article</em>.) Good design leads to sales and conversions on your website, but crafting great design is no easy task. It takes a lot of time and effort to achieve excellent results.</p>

<p>Design is a constantly evolving discipline. Product teams iterate on design to deliver the best possible experience to their users. A lot of things might change during each iteration. Designers will introduce changes, and developers will dive into the code to adjust the design. While jumping into code to solve an exciting problem might be fun, doing it to resolve a minor issue is the exact opposite. It’s dull. Imagine that you, as a web developer, continually get requests from the design team like:</p>

<ul>
<li>Change the featured image.</li>
<li>Update the copy next to the logo in the header.</li>
<li>Add a custom header to the “About Us” page.</li>
</ul>

<p>These requests happen all the time in big projects. It’s a never-ending stream of boring requests. Want to have fun while creating websites, focus on more challenging tasks, and complete your projects much faster?</p>

<p><a href="https://elementor.com">Elementor</a> helps with just that. It reduces the need to hand-code the theme parts of your website and frees you up to work on more interesting and valuable parts of the design.</p>

## Elementor Page Builder

<p>For a long time, people dreamed that they would be able to put together a web page by dragging and dropping different elements together. That’s how page builders became popular. Page builders introduced a whole different experience of building a page &mdash; all actions involving content are done visually. They reduce the time required to produce a desirable structure.</p>

<p>What if we took the <a href="https://w3techs.com/technologies/overview/content_management/all">most popular CMS in the world</a> and develop the most advanced page builder for it? That’s how Elementor 1.0 for WordPress was created. Here are a few features of the tool worth mentioning:</p>

<ul>
<li><strong>Live editing</strong>. Elementor provides instant live editing &mdash; what you see is what you get!  The tool comes with a live drag-and-drop interface. This interface eliminates guesswork by allowing you to build your layout in real time.</li>
<li>Elementor comes with a ton of <strong>widgets</strong>, including for the most common website elements. Also, there are dozens of Elementor add-ons created by the community: <a href="https://wordpress.org/plugins/search/elementor/">https://wordpress.org/plugins/search/elementor/</a></li>
<li><strong>Responsive design</strong> out of the box. The content you create using Elementor will automatically adapt to mobile devices, ensuring that your website is mobile-friendly. Your design will look pixel-perfect on any device.</li>
<li><strong>Mobile-first design</strong>. The Elementor page builder lets you create truly a responsive website in a whole new visual way. Use different font sizes, padding and margins per device, or even reverse column ordering for users who are browsing your website using a mobile device.</li>
<li><strong>Revision history</strong>. Elementor has a history browser that allows you to roll forward and backward through your changes. It gives you the freedom to experiment with a layout without fear of losing your progress.</li>
<li><strong>Built-in custom CSS</strong> feature allow you to add your own styles. Elementor allows you to add custom CSS to every element, and to see it in action live in the editor.</li>
<li><strong>Theme-independence</strong>. With Elementor, you’re not tied to a single theme. You can change the theme whenever you like, and your content will come along with you. This gives you, as a WordPress user, maximum flexibility and freedom to work with your favorite theme, or to switch themes and not have to worry about making changes.</li>
<li><strong>Complete code reference</strong> and a lot of tutorials. Elementor is a developer-oriented product &mdash; it’s an open-source solution with a <a href="https://code.elementor.com/">complete code reference</a>. If you’re interested in creating your own solutions for Elementor, it’s worth checking the website <a href="https://developers.elementor.com/">https://developers.elementor.com</a>. The website contains a lot of helpful tutorials and explanations.</li>
</ul>

<p>There are two particular cases in which Elementor would be helpful to web developers:</p>

<ul>
<li>Web developers who need to <strong>create an interactive prototype really quickly</strong>. Elementor can help in situations where a team needs to provide an interactive solution but doesn’t have enough time to code it.</li>
<li>Web developers who <strong>don’t want to be involved in post-development activities</strong>. Elementor is perfect when a website is developed for a client who wants to make a lot of changes themselves without having to write a single line of code.</li>
</ul>

## Meet Elementor Pro 2.0 Theme Builder

<p>Despite all of the advantages Elementor 1.0 had, it also had two severe limitations:</p>

<ul>
<li>There were parts of a WordPress website that weren’t customizable. As a user, you were limited to a specific area of your website: the content that resides between the header and the footer. To modify other parts of the website (e.g. footer or header), you had to mess with the code.</li>
<li>It was impossible to create dynamic content. While this wouldn’t cause any problems if the website contained only static pages (such as an “About Us” page), it might be a roadblock if the website had a lot of dynamic content.</li>
</ul>

<p>In an attempt to solve these problems, the Elementor team released the Elementor 2.0 Theme Builder, with true theme-building functionality. Elementor Pro 2.0 introduces a new way to build and customize websites. With Theme Builder, you don't have to code menial theme jobs anymore and can instead focus on deeper website functionality. You are able to design the entire page in the page builder. No header, no footer, just Elementor.</p>

## How Does Theme Builder Work?

<p>The tool allows you to build a header, footer, single or archive templates, and other areas of a website using the same Elementor interface. To make that possible, Elementor 2.0 introduces the concept of global templates. Templates are design units.  They’re capable of customizing each and every area of your website.</p>

<p>The process of creating a template is simple:</p>

<ol>
<li>Choose a template type.</li>
<li>Build your page’s structure.</li>
<li>Set the conditions that define where to apply your template.</li>
</ol>

<p>Let’s explore each of these steps in more detail by creating a simple website. In the next section, we’ll build a company website that has a custom header and footer and dynamic content (a blog and archive). But before you start the process, make sure you have the latest version of WordPress, with the <a href="https://elementor.com/pro/">Elementor Pro</a> plugin installed and activated. It is also worth mentioning that you should have a theme for your website. Elementor doesn’t replace your theme; rather, it gives you visual design capabilities over every part of the theme.</p>

### Custom Header And Footer

<p>The header and footer are the backbone of every website. They are where users expect to see navigation options. Helping visitors navigate is a top priority for web designers.</p>

<p>Let’s start with creating a header. We’ll create a fairly standard header, with the company’s logo and main menu.</p>

<p>The process of creating a custom header starts with choosing a template. To create a new template, you’ll need to go to <strong>“Elementor” → “My Templates” → “Add New”.</strong></p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69ec1b53-4f57-4502-95fc-6626cb7fce11/15-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69ec1b53-4f57-4502-95fc-6626cb7fce11/15-elementor-pro-2-theme-builde.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69ec1b53-4f57-4502-95fc-6626cb7fce11/15-elementor-pro-2-theme-builde.png'>Large preview</a>" alt="" >}}

<p>You’ll see a dialog box, “Choose Template Type”. Select “Header” from the list of options.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0511f27c-84da-4052-987a-93dfea4a9c5f/10-elementor-pro-2-theme-builde.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0511f27c-84da-4052-987a-93dfea4a9c5f/10-elementor-pro-2-theme-builde.png" sizes="100vw" caption=" Choose the type of template you want to create. It can be a header, footer, single post page or archive page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0511f27c-84da-4052-987a-93dfea4a9c5f/10-elementor-pro-2-theme-builde.png'>Large preview</a>)" alt="" >}}

<p>Once you choose a type of template, Elementor will display a list of blocks that fit that type of content. Blocks are predesigned layouts provided by Elementor. They save you time by proving common design patterns that you can modify to your own needs. Alternatively, you can create a template from scratch.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffe4f652-9c1e-40bc-87d6-c167fd09a633/17-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffe4f652-9c1e-40bc-87d6-c167fd09a633/17-elementor-pro-2-theme-builde.png" sizes="100vw" caption="Choose either a predesigned block for your header, or build the entire menu from scratch. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffe4f652-9c1e-40bc-87d6-c167fd09a633/17-elementor-pro-2-theme-builde.png'>Large preview</a>)" alt="" >}}

<p>Let’s choose the first option from the list (“Metro”). You can see that the top area of the page layout has a new object &mdash; a newly created header.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2147fe70-7576-4b90-8327-916e1d8fe6c7/07-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2147fe70-7576-4b90-8327-916e1d8fe6c7/07-elementor-pro-2-theme-builde.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2147fe70-7576-4b90-8327-916e1d8fe6c7/07-elementor-pro-2-theme-builde.png'>Large preview</a>" alt="" >}}

<p>Now, you need to customize the header according to your needs. Let’s choose a logo and define a menu. Click on the placeholder “Choose Your Image”, and select the logo from the gallery. It’s worth mentioning that the template embeds your website’s logo. This is good because if you ever change that logo at the website level, the header will automatically be updated on all pages. Next, click on the menu placeholder and select the website’s main menu.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0110faec-d489-4583-bd09-cf3556a35011/05-elementor-pro-2-theme-builde.jpg" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0110faec-d489-4583-bd09-cf3556a35011/05-elementor-pro-2-theme-builde.jpg" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0110faec-d489-4583-bd09-cf3556a35011/05-elementor-pro-2-theme-builde.jpg'>Large preview</a>" alt="" >}}

<p>When the process of customization is finished, you need to implement the revised header on your website. Click the “Publish” button. The “Display Conditions” window will ask you to choose where to apply your template.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19b2eb51-b944-4fff-ac11-bc0b332011ad/08-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19b2eb51-b944-4fff-ac11-bc0b332011ad/08-elementor-pro-2-theme-builde.png" sizes="100vw" caption="Every template contains the display conditions that define where it’s placed. Choose where the header will be shown. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19b2eb51-b944-4fff-ac11-bc0b332011ad/08-elementor-pro-2-theme-builde.png'>Large preview</a>)" alt="" >}}

<p>The conditions define which pages your template will be applied to. It’s possible to show the header on all pages, to show it only on certain pages or to exclude some pages from showing the header. The latter case is helpful if you don’t want to show the header on particular pages.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/019fe9bb-e0f4-4b06-98e8-91c7c9541404/11-elementor-pro-2-theme-builde.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/019fe9bb-e0f4-4b06-98e8-91c7c9541404/11-elementor-pro-2-theme-builde.png" sizes="100vw" caption="Choose where you want to show the header. Want one header for the home page and another for the services page? Get it done in minutes. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/019fe9bb-e0f4-4b06-98e8-91c7c9541404/11-elementor-pro-2-theme-builde.png'>Large preview</a>)" alt="" >}}

<p>As soon as you publish your template, Elementor will recognize it as a header and will use it on your website.</p>

<p>Now it’s time to create the footer for your website. The process is similar; the only difference is that this time you’ll need to choose the template named “Footer” and select the footer layout from the list of available blocks. Let’s pick the first option from the list (the one that says “Stay in Touch” on the dark background).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2bf156a-8778-4bb0-bc61-5cd015a58cf8/01-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2bf156a-8778-4bb0-bc61-5cd015a58cf8/01-elementor-pro-2-theme-builde.png" sizes="100vw" caption="Choosing a block for a footer. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2bf156a-8778-4bb0-bc61-5cd015a58cf8/01-elementor-pro-2-theme-builde.png'>Large preview</a>)" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cea3199-7113-4caa-9c82-1877c4f8af33/16-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cea3199-7113-4caa-9c82-1877c4f8af33/16-elementor-pro-2-theme-builde.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2cea3199-7113-4caa-9c82-1877c4f8af33/16-elementor-pro-2-theme-builde.png'>Large preview</a>" alt="" >}}

<p>Next, we need to customize the footer. Change the color of the footer and the text label under the words “Stay in Touch”. Let’s reuse the color of the header for the footer. This will make the design more visually consistent.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52e41214-2428-4a4b-b14c-3e56a82217a3/18-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52e41214-2428-4a4b-b14c-3e56a82217a3/18-elementor-pro-2-theme-builde.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52e41214-2428-4a4b-b14c-3e56a82217a3/18-elementor-pro-2-theme-builde.png'>Large preview</a>" alt="" >}}

<p>Finally, we need to choose display conditions. Similar to the header, we’ll choose to display the footer for the entire website.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd237bf6-99da-4677-bbf2-860912d4ad1e/14-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd237bf6-99da-4677-bbf2-860912d4ad1e/14-elementor-pro-2-theme-builde.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd237bf6-99da-4677-bbf2-860912d4ad1e/14-elementor-pro-2-theme-builde.png'>Large preview</a>" alt="" >}}

<p>That’s all! You just built a brand new header and footer for your website without writing a single line of code. The other great news is that you don’t have to worry about how your design will look on mobile. Elementor does that for you. UI elements such as the top-level menu will automatically become a hamburger for mobile users.</p>

### Single Post for Blog

<p>Let’s design a blog page. Unlike static pages, such as “About us”, the blog has dynamic content. Elementor 2.0 allows you to build a framework for your content. So, each time you write a new blog post, your content will automatically be added to this design framework.</p>

<p>The process of creating a blog page starts with selecting a template. For a single blog post, choose the template type named “Single.” We have two options of blocks to choose from. Let’s choose the first one.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7ac32a0-fba8-41ec-b4b1-b5c396027c1b/13-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7ac32a0-fba8-41ec-b4b1-b5c396027c1b/13-elementor-pro-2-theme-builde.png" sizes="100vw" caption="Choosing a block for a single post. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7ac32a0-fba8-41ec-b4b1-b5c396027c1b/13-elementor-pro-2-theme-builde.png'>Large preview</a>)" alt="" >}}

<p>The block you selected has all of the required widgets, so you don’t need to change anything. But it’s relatively easy to adjust the template if needed. A single post is made of dynamic widgets such as the post title, post content, featured image, meta data and so on. Unlike static widgets that display content that you enter manually, dynamic widgets draw content from the current pages where they’re applied. These widgets are in the “Elements” panel, under the category “Theme Elements”.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20961e92-a5b3-4de3-80e2-8dbb5e5d087d/03-elementor-pro-2-theme-builde.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20961e92-a5b3-4de3-80e2-8dbb5e5d087d/03-elementor-pro-2-theme-builde.png" sizes="50vw" caption="List of dynamic elements. A dynamic widget changes according to the page it’s used on. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20961e92-a5b3-4de3-80e2-8dbb5e5d087d/03-elementor-pro-2-theme-builde.png'>Large preview</a>)" alt="" >}}

<p>When you work on dynamic content like a single post, you’ll want to see how it looks on different posts. Elementor gives you a preview mode so you can know exactly what your blog will look like.</p>

<p>To go into preview mode, you need to click on the Preview icon (the eye icon in the bottom-left part of the layout), and then “Settings”.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca892d61-6b2e-4c49-ad7e-662fb70cee35/19-elementor-pro-2-theme-builde.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca892d61-6b2e-4c49-ad7e-662fb70cee35/19-elementor-pro-2-theme-builde.png" sizes="100vw" caption="Never again work on the back end and guess what the front end will look like. Use preview mode to see how your templates will work for your content. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca892d61-6b2e-4c49-ad7e-662fb70cee35/19-elementor-pro-2-theme-builde.png'>Large preview</a>)" alt="" >}}

<p>To see what your page will look like when it’s be filled with content, simply choose a source of content (e.g. a post from the “News” category).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcb85f74-9109-4239-b2d8-37e93eddf3f0/09-elementor-pro-2-theme-builde.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcb85f74-9109-4239-b2d8-37e93eddf3f0/09-elementor-pro-2-theme-builde.png" sizes="50vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dcb85f74-9109-4239-b2d8-37e93eddf3f0/09-elementor-pro-2-theme-builde.png'>Large preview</a>" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68610492-04d9-4dc0-b562-655f3c11abf2/02-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68610492-04d9-4dc0-b562-655f3c11abf2/02-elementor-pro-2-theme-builde.png" sizes="100vw" caption="Fill your template with content from your actual website to see what the result will look like. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68610492-04d9-4dc0-b562-655f3c11abf2/02-elementor-pro-2-theme-builde.png'>Large preview</a>)" alt="" >}}

<p>Once you’ve finished creating dynamic content, you’ll need to choose when the template will be applied. Click on “Publish” button, and you’ll see a dialog that allows you to define conditions.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdc18dc9-77e4-421b-93ad-4f68de74be51/12-elementor-pro-2-theme-builde.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdc18dc9-77e4-421b-93ad-4f68de74be51/12-elementor-pro-2-theme-builde.png" sizes="100vw" caption="Choosing conditions for a single post template. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fdc18dc9-77e4-421b-93ad-4f68de74be51/12-elementor-pro-2-theme-builde.png'>Large preview</a>)" alt="" >}}

### Archive

<p>The archive page is a page that shows an assortment of posts. Your archive page makes it easy for readers to see all of your content and to dive deeper into the website. It’s also a common place to show search results.</p> 

<p>The Theme Builder enables you to build your own archive using a custom taxonomy. To create an archive page, you need to go through the usual steps: create a new template, and choose a block for it. For now, Elementor provides only one type of block for this type of template (you can see it in the image below).</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc6d6c4-4c5d-4499-b7b5-2fab028c23ed/06-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc6d6c4-4c5d-4499-b7b5-2fab028c23ed/06-elementor-pro-2-theme-builde.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dc6d6c4-4c5d-4499-b7b5-2fab028c23ed/06-elementor-pro-2-theme-builde.png'>Large preview</a>" alt="" >}}

<p>After selecting this block, all you need to do is either set a source for your data or stick to the default selection. By default, the archive page shows all available blog posts. Let’s leave it as is.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10d6e17f-2da0-40a0-bc07-2502a498ffc6/04-elementor-pro-2-theme-builde.png" breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10d6e17f-2da0-40a0-bc07-2502a498ffc6/04-elementor-pro-2-theme-builde.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10d6e17f-2da0-40a0-bc07-2502a498ffc6/04-elementor-pro-2-theme-builde.png'>Large preview</a>" alt="" >}}

<p>As you can see, we’ve successfully customized the website’s header, footer, single post and archive page, without any roadblocks of coding.</p>

## What To Expect In The Near Future

<p>Elementor is being actively developed, with new features and exciting enhancements released all the time. This means that the theme builder is only going to get better. The Elementor team plans to add integration for plugins such as WooCommerce, Advanced Custom Fields (ACF), and Toolset. The team also welcomes feedback from developers. So, if you have a feature that you would like to have in Elementor, feel free to reach out to the Elementor team and <a href="https://github.com/pojome/elementor/issues">suggest it</a>.</p>

## Conclusion

<p>When WordPress was released 15 years ago, the idea behind it was to save valuable time for developers and to make the process of content management as easy as possible. Today, it is widely regarded as a developer-friendly tool. Elementor is no different. The tool now offers never-before-seen flexibility to visually design an entire website. Don’t believe me? Try it for yourself! Explore <a href="https://elementor.com/pro/">Elementor Pro</a> today.</p>

{{< signature "ms, ra, il, al, yk" >}}


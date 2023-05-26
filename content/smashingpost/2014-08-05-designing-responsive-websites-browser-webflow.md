---
title: Design Responsive Websites In The Browser With Webflow
slug: designing-responsive-websites-browser-webflow
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/323ab405-bd1b-4e16-855e-b67191c6da18/wf-bodysection-500-opt.jpg
date: 2014-08-05T19:54:04.000Z
author: richard-knight
description: >-
  _This article is the first part of a series of articles on emerging responsive
  design tools. Today, Richard Knight explores the advantages of Webflow and how
  you can use it today to build responsive websites — perhaps a bit faster than
  you would build them otherwise. – Ed._

  New tools have emerged to address the challenges of responsive web design —
  tools such as _Adobe Reflow_ and the recently released _Macaw_. Today, we’ll
  look at one that I have tested extensively in the last few months. Though not
  perfect, it’s been a leap forward in productivity for the team that I work
  with. Its name is _Webflow_, and it could be the solution to the problems you
  face with static design comps produced in Photoshop and Fireworks.

  This article will take you step by step through the process of creating a
  responsive website layout for a real project. As we go along, we’ll also
  identify Webflow’s advantages and where it comes up short.
categories:
  - Mobile
  - Design
  - Techniques
  - Responsive Design
---
<em>This article is the first part of a series of articles on emerging responsive design tools. Today, Richard Knight explores the advantages of Webflow and how you can use it today to build responsive websites — perhaps a bit faster than you would build them otherwise. – Ed.</em>

New tools have emerged to address the challenges of responsive web design — tools such as <a href="https://html.adobe.com/edge/reflow/">Adobe Reflow</a> and the recently released <a href="https://macaw.co/">Macaw</a>. Today, we’ll look at one that I have tested extensively in the last few months. Though not perfect, it’s been a leap forward in productivity for the team that I work with. Its name is <a href="https://webflow.com/">Webflow</a>, and it could be the solution to the problems you face with static design comps produced in Photoshop and Fireworks.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3c65c83-6a1a-4045-885b-cd59ab183440/1-intro-e1394001063518.jpg" alt="1-introducing-webflow" width="500" height="294" /></figure>

This article will take you step by step through the process of creating a responsive website layout for a real project. As we go along, we’ll also identify Webflow’s advantages and where it comes up short.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Design Process In The Responsive Age](https://www.smashingmagazine.com/2012/05/design-process-responsive-age/)
*   [Device-Agnostic Approach To Responsive Web Design](https://www.smashingmagazine.com/2012/03/device-agnostic-approach-to-responsive-web-design/)
*   [12 Factors In Selecting A Mobile Prototyping Tool](https://www.smashingmagazine.com/2016/04/factors-selecting-mobile-prototyping-tool/)

{{% feature-panel %}}

## Getting Started

Getting started in Webflow is a relatively simple. Head over to <a href="https://webflow.com/">the website</a>, create an account, and give the free trial a go. Make sure to open the interface in the latest version of Google Chrome because it is currently the only browser that is fully supported.

Before beginning a design, decide whether to start it from scratch or to work with one of the many templates. For this tutorial, we’ll choose the blank website template.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/443f0c67-af44-4617-970f-34e97bab9386/2-templates1-e1394009624163.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b6f9e46-b6b1-4323-b7e2-8f84e25f88b5/2-templates-e1394001363940.jpg" alt="2-introducing-webflow" width="500" height="347" /></a></figure>

Take a minute to mouse over the tooltips in Webflow’s interface to become familiar. There are no shape tools or layers in the traditional sense. There are also no filters or effects or even brushes. Webflow keeps everything focused on what the browser can do; so, knowing the basics of HTML and CSS is enough to get up and running.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d77eef2-ff97-42b4-b6fe-a34bedd55a99/wf-toolbars.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93ee65af-4814-4fcb-83d6-d6a2b17eff76/wf-toolbars-500.png" alt="wf_toolbars_500" width="500" height="318" /></a></figure>

### Toolbar Overview

The left toolbar handles various functions, such as publishing your website to be shared with a live link and switching between device views (using the laptop and phone icons). You’ll use this toolbar mostly for the latter and for entering preview mode, which hides Webflow’s interface and shows what your website will look like when published.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f93d3cd-ca93-44d2-b06d-613a8fd91faa/3-blank-canvas3-e1394177800453.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e295522f-bcd5-4766-9546-0eb2b1a8c974/3-blank-canvas2-e1394177671515.png" alt="webflow-left-bar-500" width="251" height="498" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f93d3cd-ca93-44d2-b06d-613a8fd91faa/3-blank-canvas3-e1394177800453.png">View the entire toolbar</a>)</figcaption></figure>

The right toolbar (shown below) consists of six tabs. The first tab (“+”) lets you add structure and HTML content elements to the page. Each item you add to the body of the page comes with default styles that you may overwrite. Whenever you need to add content, you’ll come back here. I always start with a section, a container and columns because they all have predefined behavior that changes according to the breakpoint.

A section is a div set to the full width of the viewport. A container sits centered within a section and constrains the widths of elements such as headings and paragraphs, while columns divide containers evenly in percentages.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbc375c0-97b5-4825-8960-124951c6092c/wf-layout-full.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ac8055a-c6e0-4581-812b-dfb2bd7b9bf4/wf-layout.png" alt="wf_layout" width="237" height="370" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbc375c0-97b5-4825-8960-124951c6092c/wf-layout-full.png">View the large version</a>)</figcaption></figure>

Next is the CSS tab, where we’ll spend most of our time. Here, we can assign classes to the element that is currently selected and then style it as we see fit. All of the CSS that you would normally write by hand is shown here. As soon as you change a class, the CSS will update immediately without your having to refresh. Be sure to examine the advanced toggles, which allow for control of other things such as positioning and the behavior of background images in their div.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75046d52-678a-4f0c-941f-43778a2391a2/wf-css-full.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2dc9a75-1e22-41f3-96dc-35943940b4d0/wf-css-preview.png" alt="wf_css_preview" width="238" height="417" /></a><figcaption>CSS options (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75046d52-678a-4f0c-941f-43778a2391a2/wf-css-full.png">View large version</a>)</figcaption></figure>

The third tab is for settings of the element that you select. Here, you can control things like the visibility of content at certain screen sizes, and you can add link elements to other pages in your project. This panel has to do mainly with non-style-related aspects and is especially handy when you’re working on complicated elements, such as the navigation menu.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17f6cf9b-9e8c-4f18-a2de-462bd52cc19f/wf-settings.png" alt="wf_settings" width="237" height="434" /><figcaption>Control visibility and even add links.</figcaption></figure>

Fourth from the left is a useful structure navigator that visually displays the contents of your website in a folder-like tree. If you need a heading to sit in a different div or container, just click and drag it to where you want it to be. I often refer to this panel as I go to make sure that certain items are in the right divs and that my styles cascade appropriately. It’s also useful for selecting content that might be hard to click with the mouse because it is behind other elements.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0382b7e7-bd59-4744-a336-7dad4a5d878b/wf-structure.png" alt="wf_structure" width="236" height="488" /><figcaption>These elements will be represented by the class names that you assign to them, so give everything a straightforward name.</figcaption></figure>

Next up is the class manager, which shows all of your CSS classes at once. You can use it to edit a particular class (see the small wrench icon) and to quickly remove any class that isn’t being used. It’s handy, but you will usually just use it to clean up classes that you’ve discarded or to quickly change a class that’s used multiple times in different places.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de17604e-758f-43bd-820c-501db21e0383/wf-css-classes.png" alt="wf_css_classes" width="238" height="504" /><figcaption>A quick view of all of your CSS classes.</figcaption></figure>

Last is the symbol library. Complex items, such as the primary navigation and the footer, can be created as symbols, which can be reused on other pages in your Webflow website. This is a great time-saver, but know that symbols are usable only in the project they were created in.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/604d07ca-bdc8-4de6-95ca-43b02f368248/symbol-library.png" alt="symbol_library" width="237" height="264" /></figure>

### Regarding Web Fonts

Before we begin with the project, it’s worth mentioning that Webflow supports web fonts to a certain extent. All of the usual standbys, including Arial and Verdana, are available, and you can use any font in Google’s library, as well as any you have in TypeKit. However, any font not provided by either Google or Typekit cannot be integrated in Webflow’s design view (an obstacle that my team faced).

Applying your own font using Webflow’s custom code area is possible. Do this by linking to it in the head of your website and then using a style tag to specify where to use it. However, the font will appear only after you’ve published the website, making it frustrating to refine your typography for different breakpoints.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b86d9612-7b36-4084-a5ab-a6e4c198a6a0/custom-code.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dadc7b6-916d-4b10-86e7-4361ee163d9f/wf-custom-code-500.png" alt="wf_custom_code_500" width="500" height="246" /></a><figcaption>An example of how to apply your own hosted web font.</figcaption></figure>

## Designing In The Browser

For this tutorial, we’ll work from the desktop view down to mobile. This is deliberate: In Webflow, every style that you create in the desktop view will cascade down. It’s weird at first, but you do get used it. The rationale is that when you change a style in the tablet view, it will change for everything below. This saves time when something is broken in one media query because it will often be broken in the narrower views.

We’ll find what we need to begin in the “+” icon (the tab to add elements). First, add a section, and then drag and drop a “navbar” into that section. Then, select the image element under “Media,” and drag it over to the logo area of the navbar. Once it’s highlighted, let go of the mouse, and Webflow will drop in a placeholder image. I’ve replaced the default image with my company’s logo. Essentially, what we’re doing here is <strong>using divs and HTML pieces that have a predefined behavior in Webflow</strong>; while empty and lacking any notable styles, they will form the basic structure of the website.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b3cd0e0e-f70c-4005-a1da-264b389d882b/wf-navbar.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56e72f64-cbe3-413d-92e4-3336873aefb7/wf-navbar-500.png" alt="wf_navbar_500" width="500" height="316" /></a></figure>

Now, let’s add the rest of the navigation, give it a background color, and change the fonts. My company uses a standard gray for the background of its navigation. Add a background color easily by selecting the navbar section with your mouse and then going down to the background area in the style tab. Once you’ve chosen a color, click “OK” to confirm.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/078ad132-abe8-4c5e-adf9-e2f46629d2a5/wf-navbar-styles.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/078ad132-abe8-4c5e-adf9-e2f46629d2a5/wf-navbar-styles.png" alt="wf_navbar_styles" width="1363" height="806" /></a></figure>

Next, we need to add a section that sits above the navbar. This will have a link and some copy. Click and drag the section so that it sits above the navbar, and then add a container so that our new content stays centered in the browser window, like the navigation below it.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a99393cb-9011-45f4-bda1-f5e99ec78981/wf-votenow.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8547e24-6029-4469-bd6a-f4865fb0a14f/wf-votenow-500.png" alt="wf_votenow_500" width="500" height="283" /></a></figure>

Above, I’ve added a plain-text block for the deadline copy, as well as a text link for our call to action. Both are assigned separate classes, set to display as <code>inline-block</code> and with the text aligned right. I’ve also adjusted the padding by dragging with the mouse on the arrows under “Position,” so that they both appear vertically centered. Finally, I’ve given this new section a background gradient.

Notice under “Position” how the padding values are blue. This lets us know that we’ve changed the default styling of <code>0</code>. If it were a yellow number or a label, this would mean that the selected element’s style is inherited.</p>

<figure><img loading="lazy" decoding="async" class="142682" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b06e506-bddc-4b6e-8765-794901009241/wf-inherited-fonts.png" alt="wf_inherited_fonts" width="240" height="161" /><figcaption>The font and line-height fields have yellow labels, letting you know that their styles are inherited.</figcaption></figure>

With the styling done for the header, let’s set the structure of the main body. Our website needs copy on the left and an image on the right for tablet and desktop views. Again, add a section and a container, and define a grid by adding the column element to that container. By default, we’re given two columns. You can change this to a different number at any time by tweaking the column’s setting.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89f2bb60-52b9-4e7c-844d-d0b7ea50b578/wf-bodysection.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4464790-2cb4-41f5-8a75-e3302cc20d5a/wf-bodysection-500.png" alt="wf_bodysection_500" width="500" height="297" /></a></figure>

I’ve gone ahead and added a large placeholder image to the right column and paragraph copy to the left. I’ve also added two buttons. Working with long copy in Webflow gets tedious because each paragraph has to be added as its own element. It would be nice just to work with one text-box element, in which you can paste all of the copy at once and proceed to style it, as in Macaw.

For now, let’s adjust the paragraph’s line height, add style to the buttons and add the remaining content.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/199f73bc-0f6d-4ef1-8e07-e9b738bdab90/wf-body.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0dc677a-17d6-4e39-9737-174bcb115dee/wf-body-500.png" alt="wf_bodysection_500" width="500" height="297" /></a></figure>

Last, we’ll add the footer by adding a section to the bottom of the page. We’ll apply a background color and throw in one last container to house our new text links and copyright. Another annoyance is that Webflow doesn’t yet allow for descendant selectors. I’d much a prefer a visual way to target links in the footer section with styles akin to the following:

<pre><code class="language-css">
.footer a {
   text-decoration: none;
   font-size: 12px; }
</code></pre>

&nbsp;

Webflow currently requires everything to be assigned a class, even if it’s already in a div that has a class that you could reference. While not a deal-breaker, a little more finesse would be nice.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90fe0248-2b57-4f95-9d12-fe3e9d986958/wf-footer.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a11e9092-af8e-48ed-8408-d5bd3eaa9a80/wf-footer-500.png" alt="wf_footer_500" width="500" height="103" /></a><figcaption>Every styled element requires its own class in Webflow.</figcaption></figure>

With the footer done, our desktop layout is in pretty good shape. Now it’s time to tackle any presentation issues that we find at the other breakpoints.</p>

## Fixing Breakpoints In Webflow’s Responsive Views

One of the main differences between Webflow and its competition is that you cannot define your own breakpoints. Webflow is a custom framework based heavily on Bootstrap, so a lot of the <strong>automatic behavior for content elements</strong> derives from that. You could view this as a hindrance or an advantage, depending on your situation and your project’s needs. Our current e-commerce website leverages Bootstrap, so using Webflow to prototype makes sense for us. If your website requires unique breakpoints or you already use another framework, such as Foundation, then you might have to try something else.

Let’s look at the tablet view first. Nothing completely breaks, as you can see below, although we might want to add more space between the footer and the rest of the page.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f93655b0-10a1-4acc-b0b2-bf45b203737b/wf-tabletview.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e79b0a64-aa0e-4606-b501-4284d2ce5c81/wf-tabletview-500.png" alt="wf_tabletview_500" width="500" height="272" /></a><figcaption>Webflow’s custom Bootstrap framework does most of the work to resize our content.</figcaption></figure>

Next up is the phone view in landscape mode or, as I like to think of it, a very wide phone breakpoint. As you can see in the first screenshot below, things are getting messy. Our image in “Column 2” collides with our callout box. Also, that image is pretty large for mobile phones, so let’s shrink it by changing its width to <code>40%</code>, leaving the height set to <code>auto</code>. For our last change, I’d prefer that our buttons appear on small screens as block elements, with widths of <code>100%</code>. Check out the before and after:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7cef4db-14aa-4305-9dbe-d5b245772d6e/wf-phone-landscape-500.png" alt="wf_phone_landscape_500" width="500" height="478" /><figcaption>Webflow makes it easy to fix a broken layout.</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/814377a9-145d-40df-befc-3e43ea7daa8f/wf-phone-landscape-fixed-500.png" alt="wf_phone_landscape_fixed_500" width="500" height="697" /><figcaption>The same breakpoint with our changes applied.</figcaption></figure>

That’s a bit better. As you become familiar with Webflow, you might decide to abandon columns altogether in certain instances because they dictate the order of your page. Suppose we wanted the image to be the first visible item below the primary navigation on phones. Because we’ve used columns and thrown the image into the righthand column, we cannot reorder it on mobile; the left column will always be stacked on top.

If we used our own divs with our own CSS rules, we could easily circumvent this order with some floats. So, even though columns are easy to work with and they come with predefined padding and their widths switch to 100% at low breakpoints, they can also be limiting.

Before moving on, let’s look at the <strong>default styles for the navigation menu when expanded</strong>. We get there by selecting the navbar and going to the settings tab. Once you’re in settings, click “Open Menu,” and you should see something like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96bed533-0cf8-4aac-a2d2-a269ab92abc3/wf-menu-expanded.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c78c10b-c6c6-43bf-8643-4c915dc0cf59/wf-menu-expanded-500.png" alt="wf_menu_expanded_500" width="500" height="298" /></a><figcaption>Menu before</figcaption></figure>

That’s a lot of dark gray, with no indication of the boundary between menu items for users of touch devices. Select a link and proceed to change the style. Let’s also separate the links with a bottom border. Other options are available to play with animation, but I’m happy with the defaults for now.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e1b6c9a-1c54-4d07-ba51-fd843587b1bc/wf-menu-expanded-fixed.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fe4f882-f469-4521-80dd-af81456bb426/wf-menu-expanded-fixed-500.png" alt="wf_menu_expanded_fixed_500" width="500" height="256" /></a><figcaption>Menu after</figcaption></figure>

Much better. I’ve inverted the colors somewhat to make the menu items stand out more, and I’ve added a box shadow to give a sense of depth in case it overlaps with elements like buttons. Of course, you can refine it further, specifying hover states and pressed states, but for now let’s look at the smallest breakpoint and see how our changes cascade down.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/567f4ec2-ee14-416e-8911-b7adea43450c/wf-phone-portrait-500.png" alt="wf_phone_portrait_500" width="500" height="789" /></figure>

Not bad but the header takes up a lot of space. Considering that browser chrome will take up space, too, let’s shrink it a bit.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c20af974-89b7-439b-927c-3e105208cc7e/wf-phone-portrait-fixed-500.png" alt="wf_phone_portrait_fixed_500" width="500" height="503" /></figure>

There we go. You can view the result on the demo page. If you’re on a desktop machine, resize your browser to see how the layout changes. One of the last items we’ll look at is Webflow’s code-exporting feature.</p>

## Exporting The Code

In the left toolbar is an icon that allows you to export your work as a full ZIP file, with the HTML, CSS and all images that you’ve used. At this time, there are no options to tweak how your website gets exported. Having the option to choose between LESS files and one master style sheet would be nice in future, as would an option to point to the paths where images are publicly hosted.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdae5b9d-c58f-4e88-a604-f037a252b169/wf-code-export.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28ad5d69-6629-4199-9c9f-9ebdf29e0797/wf-code-export-500.png" alt="wf_code_export_500" width="500" height="369" /></a></figure>

Webflow’s code is relatively clear and straightforward enough. Being design-focused, it does throw just about anything it can into a div, and you’ll see a lot of custom classes that look akin to Bootstrap 3. It also includes a separate style sheet for various fixes, so your website should work in most browsers. Your mileage with the exported code may vary, depending on what you need to do with it. The developers on our team found it easier just to replicate my interactive mockup in Bootstrap 3, rather than try to build on top of the code.

We did this for two reasons. First, our website is a Backbone application that needs functionality such as timed user sessions, Google Analytics and an administrative back end. Secondly, Webflow’s code does not support Internet Explorer 8, which is a requirement for our user base, unfortunately.</p>

## Conclusion: A New Tool For Designers

Webflow is a tool targeted at designers who are looking for an alternative to Photoshop and Fireworks for responsive web design. It’s not an all-encompassing solution for creating websites — at least not yet — but by enabling me to <strong>focus on layout, interaction and content behavior without having to code</strong>, it sped up our team’s design phase immensely.

And while we didn’t use the code that Webflow generated, we still found it to be more collaborative, allowing the developers who I work with to see the work I was doing on their actual phone, tablet and desktop browsers. They could ask questions any time, and I was able to iterate on the fly. Sitting down to actually build the website was easier because we had an interactive prototype to refer to.

I still use Photoshop as I believe it was intended — to crop and retouch images — but when I’m asked to make a new page or a new website, I’ll start working in Webflow. And I’ll continue to refine and expand the visual prototype until we feel we’ve taken it as far as we need to. Then, we’ll move into development, still using Webflow to prototype or test ideas if needed.</p>

<strong>On today’s responsive web, a static comp raises more questions than it answers.</strong> Sure, you’ll be able to convey the look and feel, but so many questions remain that both designers and developers can get frustrated. As designers, we try to resolve these questions by creating accompanying documentation, such as a web style guide or even sometimes by building a basic page ourselves.

Developers who receive static comps to build from either have to infer missing details or go back to the designer. How does the navigation adjust? What are we envisioning for hover states or for pressed states for buttons? How will the typography change to accommodate different screens? How do we denote an active page? The list goes on and on.

Webflow fills this gap. Details can be inferred because they’ve been realized and are <strong>viewable in the browser</strong>. It enables you as the designer to experiment and prototype interactive ideas on the fly. How the tool fits in your process will depend on you and the needs of the project. However, I strongly recommend giving it a shot. It might surprise you.</p>

### Other Resources

*   “[Video Tutorials](https://tutorials.webflow.com/),” Webflow Help This free series of videos walks you through the UI and how to build websites in Webflow.
*   “[Forums](https://forum.webflow.com/)” Webflow Community An active and knowledgeable community of people already use Webflow.</p>

<em>Many thanks to Shawna Jones, Jeffrey Love, Shawn O’Neill and David Belangér for supporting my use and testing of Webflow throughout our projects.</em>

{{< signature "al, il" >}}


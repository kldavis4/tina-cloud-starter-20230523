---
title: The 10 Commandments Of Efficient Design In Axure
slug: ten-commandments-of-efficient-design-in-axure
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09b0e8e8-1588-4847-9784-b36fa83a71c4/axure-design-illu.png
date: 2013-10-04T16:14:34.000Z
author: david-morgan
description: >-
  Axure is a powerful tool for creating software prototypes quickly. Getting
  started with it is really easy; however, therein lies a danger. The tool is so
  intuitive that many users can be productive without undergoing any formal
  training. What they might not be aware of is that they probably aren’t using
  Axure optimally.
categories:
  - UX
  - Tools
  - Usability
  - Ideation
---
Axure is a powerful tool for creating software prototypes quickly. Getting started with it is really easy; however, therein lies a danger. The tool is so intuitive that many users can be productive without undergoing any formal training. What they might not be aware of is that they probably aren’t using Axure optimally.

In my experience as a UX designer, I seldom draw a page and get it right the first time. Most of the time, I go through five to ten iterations. When your UX design is used as the blueprint of an agile project, you might need to keep the entire project up to date with the scope of development. Sometimes these changes will affect a dozen or more other pages. It is at these times when some of the less evident features of Axure can become huge time-savers.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Deep Dive Into Axure 8: A Comprehensive Review](https://www.smashingmagazine.com/2016/07/a-deep-dive-into-axure-8-a-comprehensive-review/)
*   [Creating Responsive Prototypes With Adaptive Views In Axure RP 7](https://www.smashingmagazine.com/2014/02/creating-responsive-prototypes-with-adaptive-views-in-axure-rp-7/)
*   [How To Integrate Motion Design In The UX Workflow](https://www.smashingmagazine.com/2016/03/integrate-motion-design-animation-ux-workflow/)
*   [Mobile Prototyping With Axure RP](https://www.smashingmagazine.com/2012/08/mobile-prototyping-axure-rp/)

I generally work in teams to create wireframes and prototypes. To do this, I make use of Axure’s “shared projects” functionality (“team” projects in Axure 7). Multiple people being able to work on a design project at the same time remains my favorite feature of Axure, but it does demand a tidy and structured way of working. You will undoubtedly find someone else working on a page that you’ve designed or yourself working on another’s page. I’ve written these commandments with Axure in mind, because that is the tool I presently work with, but I’m certain many of the principles apply to other tools.

{{% feature-panel %}}

This <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b19128f-d330-4bf2-89c5-ac39f1e6f131/5-auto-capitalization-78x53.png">list of 10 commandments</a> is what I've found to be crucial techniques to save time in the long run. This way of working does not always provide the quickest results in the short term, but it does allow for optimal flexibility further down the line.</p>

## I) Thou Shalt Never Use Two Widgets When One Will Do.

The most common time-consuming behavior that I see with beginner and advanced Axure users is the use of unnecessary widgets. I still catch myself making this mistake and have to remind myself constantly of this first commandment. Each widget that you add to your project will require a bit more work when you need to make changes in the future. All of these little bits of work start to add up after ten iterations. Below is a simple example of how two visually identical objects can be built up in different ways.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1edcfeb-0fa8-4ab8-bff5-c29b4e5728c2/axure-rp-pro-7.0-BetaScreenSnapz015_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119312" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c138f529-127f-45dc-a1c2-75b45e58ec93/axure-rp-pro-7.0-BetaScreenSnapz015_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz015_500_mini" width="500" height="296" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1edcfeb-0fa8-4ab8-bff5-c29b4e5728c2/axure-rp-pro-7.0-BetaScreenSnapz015_mini">Larger view</a></em>

Both examples show a situation in which someone uses a separate widget for the text and the button. When this person then wants to add <code>onClick</code> behavior to the entire object, they have two options. The first option is to add a hotspot over the group, which results in three widgets to maintain. The second option is to create the <code>onClick</code> interaction for both elements, which results in two behaviors to maintain.

Both of these options will cost unnecessary time when changes need to be made. A much leaner way is to create this object by adding text to a box widget.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e0e1e0d-447f-42ff-8bcb-f22a62320e83/axure-rp-pro-7.0-BetaScreenSnapz016_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119313" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31c88076-79f9-47f8-ab39-bb7a4543cf9c/axure-rp-pro-7.0-BetaScreenSnapz016_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz016_500_mini" width="500" height="176" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e0e1e0d-447f-42ff-8bcb-f22a62320e83/axure-rp-pro-7.0-BetaScreenSnapz016_mini">Larger view</a></em>

Your text can then be positioned using the “alignment and padding” tools. You will now have only one widget to maintain and will need to connect only one behavior to it.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca10a412-5e95-41df-9c9d-f902ee1d8416/axure-rp-pro-7.0-BetaScreenSnapz002_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119324" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c90571f-29a0-49d5-8c97-49f3e1b2da96/axure-rp-pro-7.0-BetaScreenSnapz002_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz002_500_mini" width="500" height="238" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca10a412-5e95-41df-9c9d-f902ee1d8416/axure-rp-pro-7.0-BetaScreenSnapz002_mini">Larger view</a></em>

## II) Thou Shalt Not Duplicate, But Rather Make The Object A Master.

When I find myself in a late stage of a design and realize that we need to change the main navigation on every single page, I experience tremendous joy. Not because I enjoy a big pile of repetitive work, but because all I need to do is edit my single master object and — presto — the whole project has been updated.

Using a master for the main navigation would seem to be quite obvious, but it pays to create a master for anything you use more than once. Whenever you find yourself copying and pasting a group of widgets, always remember that creating a master is probably better.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d21eed6e-0ff8-49a7-ab5f-cb965ba49ecf/axure-rp-pro-7.0-BetaScreenSnapz004_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119325" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9334693-f09c-4254-a46c-1809ef8c492d/axure-rp-pro-7.0-BetaScreenSnapz004_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz004_500_mini" width="500" height="691" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d21eed6e-0ff8-49a7-ab5f-cb965ba49ecf/axure-rp-pro-7.0-BetaScreenSnapz004_mini">Larger view</a></em>

After creating a master, such as the product tile above, if you decide to change the button’s label to “Buy now,” you will need to edit it only once to see the change in every instance of the master.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09852b54-fede-4a08-a0b7-d60b6e04743b/axure-rp-pro-7.0-BetaScreenSnapz019_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119314" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0223f5cb-a5f9-49a3-abb7-6d3aa4a9dfb5/axure-rp-pro-7.0-BetaScreenSnapz019_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz019_500_mini" width="500" height="303" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09852b54-fede-4a08-a0b7-d60b6e04743b/axure-rp-pro-7.0-BetaScreenSnapz019_mini">Larger view</a></em>

Remember not to turn overly large groups into masters. The larger a group of objects, the higher the chance you will need a variation of that master at some point. Combining masters into another master is often better. This can be convenient when you need some variations of one master, with certain elements always included and other elements varying, as below:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/514851b1-81af-49f3-bc3f-9ad3b1f5fa9b/axure-rp-pro-7.0-BetaScreenSnapz020_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119315" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0e00c98-6031-465f-8473-3962dffe6f28/axure-rp-pro-7.0-BetaScreenSnapz020_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz020_500_mini" width="500" height="365" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/514851b1-81af-49f3-bc3f-9ad3b1f5fa9b/axure-rp-pro-7.0-BetaScreenSnapz020_mini">Larger view</a></em>

This base master has no pricing information included, but it can be combined with one of the other masters to create new masters for full product tiles.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae8eab7b-2829-4a20-98a3-3f6fc7390408/axure-rp-pro-7.0-BetaScreenSnapz021_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119316" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fb53d36-cb30-42c9-a87a-c70a9641fd47/axure-rp-pro-7.0-BetaScreenSnapz021_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz021_500_mini" width="500" height="341" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae8eab7b-2829-4a20-98a3-3f6fc7390408/axure-rp-pro-7.0-BetaScreenSnapz021_mini">Larger view</a></em>

## III) Thou Shalt Place Styles Before Masters.

Masters are great for creating reusable elements, but they do not allow for variations. Each instance of a master will be exactly the same as the others. This is where styles come in. Suppose you have a button design that needs to be replicated on multiple pages, but the labels on the button need to vary. Styles can help you achieve this easily. Every property of a button can be managed through styles; all you need to do is change the label.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af34591d-3217-47a6-bd09-fb83927f2018/axure-rp-pro-7.0-BetaScreenSnapz007_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119326" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a164f0c8-ba0c-4d38-943f-f6e183ddc014/axure-rp-pro-7.0-BetaScreenSnapz007_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz007_500_mini" width="500" height="474" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af34591d-3217-47a6-bd09-fb83927f2018/axure-rp-pro-7.0-BetaScreenSnapz007_mini">Larger view</a></em>

The affordance of buttons is often enhanced with <code>mouseOver</code> and related behaviors. These behaviors are often created in Axure by using dynamic panels. The different states are then placed in different panel states and selected with scripts. With this method, however, you would need to go into each of the panel states to change the copy of the button.

A much faster way of dealing with button behavior is to use the “Interaction Styles” dialog box. With this feature, simply set different styles for each behavior state, and then you would need to set the copy and size of your button only once.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44c59ae0-dacb-4dcc-a018-665b932bace7/axure-rp-pro-7.0-BetaScreenSnapz009_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119328" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a3da720-0abb-403a-8df4-91729d538622/axure-rp-pro-7.0-BetaScreenSnapz009_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz009_500_mini" width="500" height="509" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44c59ae0-dacb-4dcc-a018-665b932bace7/axure-rp-pro-7.0-BetaScreenSnapz009_mini">Larger view</a></em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c055106-44b4-4015-a66d-b7ff0b94bdb4/axure-rp-pro-7.0-BetaScreenSnapz010_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119329" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b65aabd-76ee-4846-a330-d8ffe6dd6219/axure-rp-pro-7.0-BetaScreenSnapz010_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz010_500_mini" width="500" height="636" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c055106-44b4-4015-a66d-b7ff0b94bdb4/axure-rp-pro-7.0-BetaScreenSnapz010_mini">Larger view</a></em>

<em><strong>Tip:</strong> Use the “Auto fit width” function, introduced in Axure 7, on your buttons. If you set up the left and right padding in your style, all you will need to change is the button text, and then the size of the button will automatically adapt.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c521476-b011-4095-9148-7fcbbf1e6788/axure-rp-pro-7.0-BetaScreenSnapz008_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119327" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99562597-7e27-45f5-89d8-d5de3314aa0c/axure-rp-pro-7.0-BetaScreenSnapz008_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz008_500_mini" width="500" height="372" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c521476-b011-4095-9148-7fcbbf1e6788/axure-rp-pro-7.0-BetaScreenSnapz008_mini">Larger view</a></em>

## IV) Thou Shalt Keep Thy Project Organized And Shalt Name Clearly.

Axure provides many options for keeping things organized. Every element that you place on a page can be given a unique name. Pages may be named and organized in a tree structure. Masters may be given names and sorted in folders and so on. But why go through the effort of giving everything a clear name?

*   **Keep things organized for yourself.**.  When you have an elaborate page and you want to create an interaction with a dynamic panel, you will have to sift through a long list of elements to find the one you are looking for. You can use the search field — but only if you have thoughtfully named your items.
*   **Allow for team members to step in.**.  If, like me, you work in teams on your projects, unexpected things will always happen. You or your colleague could become ill or unexpectedly have to work on another project. It is critical, then, that the project be so clearly set up that the other can just step in and take over. Interactivity built by another can be particularly complicated to step into.
*   **You will be sharing with third parties.**.  In the average project that I work on, my wireframes get shared with at least 10 people. Some people will sit at a table with me and can be carefully guided through. Others, I will never meet and will have no idea of their understanding of wireframes. Ideally, a prototype should be viewable autonomously.

Several things I do to achieve this are the following.</p>

### Create a Landing Page

You could set up the home page of your prototype as a starting page that explains what people are looking at and how they can use it. Additionally, you could provide your contact information or links to flowcharts.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/925e5320-fc93-46ff-8b81-4d0b88785a1f/google-chromescreensnapz007-mini.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119320" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b92ebdc6-def9-40de-8bce-32bba9880ba4/google-chromescreensnapz007-500-mini.png" alt="Google-ChromeScreenSnapz007_500_mini" width="500" height="313" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/925e5320-fc93-46ff-8b81-4d0b88785a1f/google-chromescreensnapz007-mini.png">Larger view</a></em>

### Give the Pages Unique and Self-Explanatory Names

The prototype will be easier to understand if the page names are clear and explain what the pages are. People will also use these names in future communication. If, for example, a graphic designer works on a comp based on your design, they will likely use the same names for the pages as you did. If a page’s name is not unique, then different names for the page will appear.</p>

### Create a Flowchart of the Most Common User Flows

Most people don’t think of a design as a tree of pages; they think in terms of a flow of activity. You can create flowcharts in Axure to reflect the important user flows and to link the nodes to the relevant pages. You would then provide an extra way to navigate the prototype. (The names in the flowchart would be based on those in the site map. Thus, it would become evident whether you are naming clearly.)

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4eaa0db-c5b0-4dde-81b8-7554639bb25d/axure-rp-pro-7.0-BetaScreenSnapz023_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119317" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30597e8d-ff5d-4d28-b331-31fc529e1a0d/axure-rp-pro-7.0-BetaScreenSnapz023_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz023_500_mini" width="500" height="296" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4eaa0db-c5b0-4dde-81b8-7554639bb25d/axure-rp-pro-7.0-BetaScreenSnapz023_mini">Larger view</a></em>

## V) Useth Always Global Guides And A Grid.

Axure allows users to create two kinds of guides: local guides, which exist only on one page, and global guides, which are visible on all pages. The guides can be set up using the “Create Guides” dialog box. If you set up guides in, for instance, a default 960 grid, then consistently positioning elements over the different pages becomes a lot easier. Also, your team members will see these global guides in a shared project.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1e6cc8d-847a-49c0-bc27-45d5abb2a800/axure-rp-pro-7.0-BetaScreenSnapz011_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119330" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b74790b-f556-4543-b2fc-49da1eb48eea/axure-rp-pro-7.0-BetaScreenSnapz011_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz011_500_mini" width="500" height="134" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1e6cc8d-847a-49c0-bc27-45d5abb2a800/axure-rp-pro-7.0-BetaScreenSnapz011_mini">Larger view</a></em>

Using a grid can help you keep your designs clean and structured. I usually set my grid to 10 × 10 pixels and create all of my objects with dimensions of multiples of 10; for example, a button of 60 × 20 pixels, and not 55 × 18 pixels. When you place these objects on the grid, everything becomes easier to align and will satisfy any obsessive-compulsiveness you may have. Of course, allow yourself to stray from the grid for special objects that need different dimensions.

<em><strong>Tip:</strong> In Axure 7, you are able to set up different sets of global guides for mobile and desktop pages. Here’s an example of a mobile grid I like to use:</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4451d632-acfa-420b-9879-0b0c691bd223/axure-rp-pro-7.0-BetaScreenSnapz012_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119331" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b15bb836-a329-44e4-bac9-d1da662ac89f/axure-rp-pro-7.0-BetaScreenSnapz012_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz012_500_mini" width="500" height="833" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4451d632-acfa-420b-9879-0b0c691bd223/axure-rp-pro-7.0-BetaScreenSnapz012_mini">Larger view</a></em>

## VI) Forgeteth Not The Import Tool.

In most projects, people create elements that are useful in other projects. Instead of reinventing the wheel for each project, reuse things that have worked in the past. Many of the basics will remain the same throughout projects, such as styles, guides and certain masters. Although copying and pasting objects from one <code>.rp</code> file to another is possible, not all information would be carried over. When you paste a button that has a particular style, that style will not be pasted along with it.

The best way to reuse elements is by using the powerful import function. This enables you to import pages and masters, but also styles and guides.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd647eba-705e-4f3f-bf5e-89ae9689666d/axure-rp-pro-7.0-BetaScreenSnapz013_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119332" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e0c34e4-72e1-4e47-9e1a-2232137f0724/axure-rp-pro-7.0-BetaScreenSnapz013_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz013_500_mini" width="500" height="385" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd647eba-705e-4f3f-bf5e-89ae9689666d/axure-rp-pro-7.0-BetaScreenSnapz013_mini">Larger view</a></em>

<em><strong>Tip:</strong> Create a “mother” <code>.rp</code> file, in which you keep all of your standard masters, to import for new projects.</em>

## VII) Thou Shalt Keep Old Versions Of Pages.

I often find that I need to go back to an old version of a project. In the “good” old days (I won’t bore you with the reasons why “good” is in quotation marks), when I was often required to create wireframes in Visio, managing projects with many pages was difficult, so I would end up taking out the legacy pages. I would also save a new file every few days with an incremental number, so that I had some sort of history of the project. In other words, I ended up with a folder of hundreds of pretty large files, wasting space.

In Axure, keeping track of old versions is easy. Simply create a folder (or a page in Axure 6.5 and earlier) named <code>Bin</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94c7d371-7085-4d30-9249-6310d9645db7/axure-rp-pro-7.0-BetaScreenSnapz014_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119311" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb253b3c-232d-4480-9ac4-63570804c9f5/axure-rp-pro-7.0-BetaScreenSnapz014_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz014_500_mini" width="500" height="167" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94c7d371-7085-4d30-9249-6310d9645db7/axure-rp-pro-7.0-BetaScreenSnapz014_mini">Larger view</a></em>

Place old versions of pages in there, so that you can easily refer to them when you need to go back in time. When exporting, simply use the option to not export all pages. This way, you can share a clean version with clients and still have old versions be directly accessible.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1063ffeb-b592-4e3b-a227-5dbebea32c56/axure-rp-pro-7.0-BetaScreenSnapz024_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119318" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f59d156-ea35-4f8d-8751-547ced7b2d59/axure-rp-pro-7.0-BetaScreenSnapz024_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz024_500_mini" width="500" height="493" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1063ffeb-b592-4e3b-a227-5dbebea32c56/axure-rp-pro-7.0-BetaScreenSnapz024_mini">Larger view</a></em>

## VIII) Thou Shalt Not Make Unnecessary Interactions.

First-time users of Axure are often impressed by the ease with which interactivity can be added to a prototype. When I started out, I couldn’t resist creating every possible interaction on my pages. However, in many cases, my designs could be clearly communicated without any interactivity — simply as still images. I now add interactivity only if the answer to one of the following questions is yes.</p>

### 1. “Do I Need Interactivity to Communicate My Design Unambiguously?”

Could your design be interpreted incorrectly if you supplied only still images, instead of an interactive element? This might be the case for an interaction that relies on certain animations to be understood.</p>

### 2. “Will This Interactivity Save Time in the Long Run?”

Would making an element interactive be quicker than showing different states on different pages? For example, creating and maintaining an interactive page with tabs would be easier than creating multiple pages for each tab.</p>

### 3. “Do I Need to Convince Someone of a Concept for an Interactive Element?”

When I come up with what I believe to be the best solution for a problem, but I know it will be heavy to develop, then I need people to support the idea. I have found that making something interactive can help sell the idea.

But if the answer to all of these questions is no, then I prefer to create multiple versions of a page that simply show different states of an interactive element.</p>

## IX) Useth Font Icons Instead Of Images.

Another simple but often overlooked way to keep Axure projects manageable is by minimizing the number of images. To change the color of an icon image in a prototype, you would have to go through several steps. You would need to open an image editor, make the changes to the icon, export to a new bitmap, and finally import into your Axure project.

Another option would be to use an icon font. With one, you can change color and scale within Axure. A great source of basic icon fonts is <a href="https://copypastecharacter.com/">CopyPasteCharacter</a>, whose fonts work right out of the box on most platforms.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b90bec-c761-4168-b6ca-b3a25dc970e8/safariscreensnapz011-mini.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119322" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ab1ae24-eb2f-4cde-b253-eb4a552a541b/safariscreensnapz011-500-mini.png" alt="SafariScreenSnapz011_500_mini" width="500" height="271" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33b90bec-c761-4168-b6ca-b3a25dc970e8/safariscreensnapz011-mini.png">Larger view</a></em>

With an icon font, you can add a graphic to a button and still obey the first commandment.</p>

## X) Previeweth Thy Prototype In The Browser Or On A Device.

Designers get frustrated upon learning that their prototype doesn’t look the same in the browser as it does in Axure. In particular, text spacing and positioning look off. What’s more, there are even differences between browsers. To avoid surprises, constantly preview your prototype in a browser or on a device if you are designing for mobile.

Even though you will never be able to eliminate all differences between Axure and the browser, there are some ways to limit them.</p>

### Text Wrapping

Here is how Axure wraps text:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8f3709b-2c38-4dba-9fd2-00a4cf9b8f98/axure-rp-pro-7.0-BetaScreenSnapz025_mini"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119319" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7d8f58-36a2-412a-aea6-0608910c8cd2/axure-rp-pro-7.0-BetaScreenSnapz025_500_mini" alt="Axure-RP-Pro-7.0-BetaScreenSnapz025_500_mini" width="500" height="261" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8f3709b-2c38-4dba-9fd2-00a4cf9b8f98/axure-rp-pro-7.0-BetaScreenSnapz025_mini">Larger view</a></em>

And here is how a browser wraps text:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2553d27a-f9bb-47ac-aef4-1b88b8d712fd/safariscreensnapz010-mini.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119321" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/358784b9-eefa-4621-b60a-fa1dcee48c50/safariscreensnapz010-500-mini.png" alt="SafariScreenSnapz010_500_mini" width="500" height="246" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2553d27a-f9bb-47ac-aef4-1b88b8d712fd/safariscreensnapz010-mini.png">Larger view</a></em>

To prevent text from wrapping to the next line, make sure your text boxes have sufficient breathing space. The safest bet is to always give text the maximum amount of space that it might need. Thus, if you need to edit your text in the future, you won’t need to resize the text box; it will wrap the way text should.</p>

### Vertical Spacing

Vertical spacing can look significantly different between a browser and Axure. You can tweak the spacing in Axure until you find the setting at which the text will look good in the browser, but this is quite an effort with an uncertain outcome. The only way to be certain of the positioning of text is either to break up the copy into chunks or to convert the text to an image. The first option breaks the first commandment, unfortunately, although it is sometimes unavoidable.</p>

## Summary

A few of these commandments bring results in the short term, but most yield benefit in the long run. All will save time and, perhaps more importantly, keep your work pleasurable.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b19128f-d330-4bf2-89c5-ac39f1e6f131/5-auto-capitalization-78x53.png"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="119323" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8c0c952-9c0d-4d9d-a20f-87de1b6dc2ad/10-commandments-500-mini.png" alt="10-commandments_500_mini" width="500" height="707" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b19128f-d330-4bf2-89c5-ac39f1e6f131/5-auto-capitalization-78x53.png">Larger view</a></em>

I hope these commandments become as useful to you as they are to me. I’m certain that other people think other rules are more important, and it would be interesting for us all to hear about them, so post your ideas in the comments.

If you haven’t yet, try out the beta version of Axure 7. Some of the changes really help to keep one’s work organized.

<strong>One last point</strong>: These rules, like any others, are made to be broken. Never let them hinder your work. As smart designers, we need to know when to break the rules.

*   [Sample RP file](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1437c305-7619-450d-909f-7cb4c43bb8bf/ten-rules-axure-examples.rp_) (ZIP)

{{< signature "al, il" >}}


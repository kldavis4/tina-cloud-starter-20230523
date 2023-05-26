---
title: 'Webflow: The Web Development Platform Of The Future'
slug: webflow-the-future-of-web-development
author: nickbabich
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23803c93-a0a8-4adb-bd02-b955e9e7dbe6/webflow-platform-futureimage28.png
date: 2019-09-10T12:30:59+02:00
summary: >-
  The market is filled with site builders that promise to be universal solutions for any design challenge, but when it comes to practice, they fall short on both the design and development side. Only a few tools actually keep their promises. In this article, Nick reviews Webflow &mdash; the next-generation tool for building a sophisticated web experience that allows users to design, build, and launch websites visually.
description: >-
  In this article, Nick reviews the Webflow &mdash; the next-generation tool for building a sophisticated web experience that allows users to design, build, and launch websites visually.
categories:
  - Tools
  - Prototyping
disable_ads: true
disable_panels: true
---
(This is a sponsored article.) Time-to-market plays a crucial role in modern web design. Most product teams want to minimize the time required to go from the idea to a ready-to-use product without sacrificing the quality of the design along the way. 

When it comes to creating a website, teams often use a few different tools: one tool for graphics and visual design, another for prototyping, and another for coding. [Webflow](https://webflow.com/?utm_medium=external&utm_source=smag) attempts to simplify the process of web design by enabling you to design and develop at the same time.

## Typical Problems That Web Designers Face

It’s important to start with understanding what challenges web design teams face when they create websites:

- **A disconnection between visual design and coding.**  
Visual designers create mocks/prototypes in a visual tool (like Sketch) and hand them off to developers who need to code them. It creates an extra round of back-and-forth since developers have to go through an extra iteration of coding. 
- **It’s hard to code complex interactions (especially animated transitions).**  
Designers can introduce beautiful effects in hi-fi prototypes, but developers will have a hard time reproducing the same layout or effect in code.
- **Optimizing designs for various screens.**  
Your designs should be responsive right from the start. 

## What Is Webflow?

[Webflow](https://webflow.com/?utm_medium=external&utm_source=smag) is an in-browser design tool that gives you the power to design, build, and launch responsive websites visually. It’s basically an all-in-one design platform that you can use to go from the initial idea to ready-to-use product. 

Here are a few things that make Webflow different:

- **The visual design and code are not separated.**  
What you create in the visual editor is powered by HTML, CSS, and JavaScript.
- **It allows you to reuse CSS classes.**  
Once defined, you can use a class for any elements that should have the same styling or use it as a starting point for a variation (base class). 
- **It is a platform and as such, it offers hosting plans.**  
For $12 per month, it allows you to connect a custom domain and host your HTML site. And for an additional $4 per month, you can use the Webflow CMS.

## Building A One-Page Website Using Webflow

The best way to understand what the tool is capable of is to build a real product with it. For this review, I will use Webflow to create a simple landing page for a fictional smart speaker device.

### Define The Structure Of The Future Page

While it's possible to use Webflow to create a structure of your layout, it’s better to use another tool for that. Why? Because you need to experiment and try various approaches before finding the one that you think is the best. It’s better to use a sheet of paper or any prototyping tool to define the bones of your page. 

It’s also crucial to have a clear understanding of what you’re trying to achieve. Find an example of what you want and sketch it on paper or in your favorite design tool.

**Tip:** You don’t need to create a high-fidelity design all of the time. In many cases, it’s possible to use lo-fi wireframes. The idea is to use a sketch/prototype as a reference when you work on your website.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd3fa75f-9fd1-40e3-b6c2-970700be1faa/webflow-platform-futureimage21.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd3fa75f-9fd1-40e3-b6c2-970700be1faa/webflow-platform-futureimage21.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd3fa75f-9fd1-40e3-b6c2-970700be1faa/webflow-platform-futureimage21.png'>Large preview</a>)" alt="" >}}

For our website, we will need the following structure:

- A hero section with a large product image, copy, and a call-to-action button. 
- A section with the benefits of using our product. We will use a zig-zag layout (this layout pairs images with text sections).
- A section with quick voice commands which will provide a better sense of how to interact with a device. 
- A section with contact information. To make contact inquiries easier for visitors, we’ll provide a contact form instead of a regular email address. 

### Create A New Project In Webflow

When you open the Webflow dashboard for the first time, you immediately notice a funny illustration with a short but helpful line of text. It is an excellent example of an empty state that is used to guide users and create the right mood from the start. It’s hard to resist the temptation to click “New Project.”

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e78c1594-236b-4483-96e1-0ac38e210dea/webflow-platform-futureimage10.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e78c1594-236b-4483-96e1-0ac38e210dea/webflow-platform-futureimage10.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e78c1594-236b-4483-96e1-0ac38e210dea/webflow-platform-futureimage10.png'>Large preview</a>)" alt="" >}}

When you click “New Project,” Webflow will offer you a few options to start with: a blank site, three common presets, and an impressive list of ready-to-use templates. Some of the templates that you find on this page are integrated with the CMS which means that  you can create CMS-based content in Webflow.  

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3908282e-8ba3-4b05-a9d7-9e58c59364b4/webflow-platform-futureimage27.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3908282e-8ba3-4b05-a9d7-9e58c59364b4/webflow-platform-futureimage27.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3908282e-8ba3-4b05-a9d7-9e58c59364b4/webflow-platform-futureimage27.png'>Large preview</a>)" alt="" >}}

Templates are great when you want to get up and running very quickly, but since our goal is to learn how to create the design ourselves, we will choose “Blank Site.”

As soon as you create a new project, we will see Webflow’s front-end design interface. Webflow provides a series of quick how-to videos. They are handy for anyone who’s using Webflow for the first time.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/046c1f65-ed01-4880-a233-479069f30715/webflow-platform-futureimage9.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/046c1f65-ed01-4880-a233-479069f30715/webflow-platform-futureimage9.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/046c1f65-ed01-4880-a233-479069f30715/webflow-platform-futureimage9.png'>Large preview</a>)" alt="" >}}

Once you’ve finished going through the introduction videos, you will see a blank canvas with menus on both sides of the canvas. The left panel contains elements that will help you define your layout’s structure and add functional elements. The right panel contains styling settings for the elements.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c0c58b-0df7-47d0-8e53-afb4aa121dec/webflow-platform-futureimage26.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c0c58b-0df7-47d0-8e53-afb4aa121dec/webflow-platform-futureimage26.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c0c58b-0df7-47d0-8e53-afb4aa121dec/webflow-platform-futureimage26.png'>Large preview</a>)" alt="" >}}

Let’s define the structure of our page first. The top left button with a plus (`+`) sign is used to add elements or symbols to the canvas. All we have to do to introduce an element/visual block is to drag the proper item to the canvas.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1fa1aa0-214f-4afb-bf16-72758f7e675a/webflow-platform-futureimage24.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1fa1aa0-214f-4afb-bf16-72758f7e675a/webflow-platform-futureimage24.gif" width="600" alt="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1fa1aa0-214f-4afb-bf16-72758f7e675a/webflow-platform-futureimage24.gif">Large preview</a>)</figcaption></figure>

While elements should be familiar for anyone who builds websites, Symbols can still be a new concept for many people. Symbols are analogous to features of other popular design tools, like the components in Figma and XD. Symbols turn any element (including its children) into a reusable component. Anytime you change one instance of a Symbol, the other instances will update too. Symbols are great if you have something like a navigation menu that you want to reuse constantly through the site. 

Webflow provides a few elements that allow us to define the structure of the layout:

- **Sections**. Sections divide up distinct parts of your page. When we design a page, we usually tend to think in terms of sections. For instance, you can use Sections for a  hero area, for a body area, and a footer area.
- Grid, columns, div block, and containers are used to divide the areas within Sections.
- **Components**. Some elements (e.g. navigation bar) are provided in ready-to-use components. 

Let’s add a top menu using the premade component Navbar which contains three navigation options and placeholders for the site’s logo:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a3e53d8-6ea1-45b4-89f6-2eae2c3ccf49/webflow-platform-futureimage12.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a3e53d8-6ea1-45b4-89f6-2eae2c3ccf49/webflow-platform-futureimage12.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a3e53d8-6ea1-45b4-89f6-2eae2c3ccf49/webflow-platform-futureimage12.png'>Large preview</a>)" alt="" >}}

Let’s create a Symbol for our navigation menu so we can reuse it. We can do that by going to “Symbols” and clicking “Create New Symbol.” We will give it the name “Navigation.” 

Notice that the section color turned to green. We also see how many times it’s used in a project (1 instance). Now when we need a menu on a newly created page, we can go to the Symbols panel and select a ready-to-use “Navigation.” If we decide to introduce a change to the Symbol (i.e., rename a menu option), all instances will have this change automatically.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7ad000-f05f-45ac-8180-dffa40060c5c/webflow-platform-futureimage1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7ad000-f05f-45ac-8180-dffa40060c5c/webflow-platform-futureimage1.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc7ad000-f05f-45ac-8180-dffa40060c5c/webflow-platform-futureimage1.png'>Large preview</a>)" alt="" >}}

Next, we need to define the structure of our hero section. Let’s use Grid for that. Webflow has a very powerful Grid editor that simplifies the process of creating the right grid &mdash; you can customize the number of columns and rows, as well as a gap between every cell. Webflow also supports nested grid structure, i.e. one grid inside the other. We will use a nested grid for a hero section: a parent grid will define the image, while the child grid will be used for the Heading, text paragraph, and call-to-action button.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba3729d1-ec92-4fe3-af22-9c7d6232bb86/webflow-platform-futureimage5.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba3729d1-ec92-4fe3-af22-9c7d6232bb86/webflow-platform-futureimage5.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba3729d1-ec92-4fe3-af22-9c7d6232bb86/webflow-platform-futureimage5.png'>Large preview</a>)" alt="" >}}

Now let’s place the elements in the cells. We need to use _Heading_, _Paragraph_, _Button_, and _Image_ elements. By default, the elements will automatically fill out the available cells as you drag and drop them into the grid.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73d3c6c4-ad68-4c6e-8ec2-441107e63ce5/webflow-platform-futureimage3.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73d3c6c4-ad68-4c6e-8ec2-441107e63ce5/webflow-platform-futureimage3.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73d3c6c4-ad68-4c6e-8ec2-441107e63ce5/webflow-platform-futureimage3.png'>Large preview</a>)" alt="" >}}

While it’s possible to customize the styling for text and images and add real content instead of dummy placeholders, we will skip this step and move to the other parts of the layout: the zig-zag layout.

For this layout, we will use a 2×3 grid (2 columns × 3 rows) in which every cell that contains text will be divided into 3 rows. We can easily create the first cell with a 3-row grid, but when it comes to using the same structure for the third cell of the master grid, we have a problem. Since Webflow automatically fills the empty cells with a new element, it will try to apply the 3-row child grid to the third element. To change this behavior, we need to use Manual. After setting the grid selection to Manual, we will be able to create the correct layout. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/706ae45b-fe64-48ea-aebe-519fd0bb278e/webflow-platform-futureimage25.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/706ae45b-fe64-48ea-aebe-519fd0bb278e/webflow-platform-futureimage25.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/706ae45b-fe64-48ea-aebe-519fd0bb278e/webflow-platform-futureimage25.png'>Large preview</a>)" alt="" >}}

Similar to the hero section, we will add the dummy context to the grid sections. We will change the data after we finish with the visual layout.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3a6a97f-35a8-4701-8687-2d4fb421d0d4/webflow-platform-futureimage13.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3a6a97f-35a8-4701-8687-2d4fb421d0d4/webflow-platform-futureimage13.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c3a6a97f-35a8-4701-8687-2d4fb421d0d4/webflow-platform-futureimage13.png'>Large preview</a>)" alt="" >}}

Now we need to define a section with voice commands. To save space, we will use a carousel. Webflow has a special element for that purpose: _Slider_.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c8c9ae6-e5a9-4e96-a239-b14c763f1b51/webflow-platform-futureimage22.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c8c9ae6-e5a9-4e96-a239-b14c763f1b51/webflow-platform-futureimage22.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c8c9ae6-e5a9-4e96-a239-b14c763f1b51/webflow-platform-futureimage22.png'>Large preview</a>)" alt="" >}}

Once we have all the required elements in place, we can create a vertical rhythm by adjusting the position of every item that we use. First, we need to adjust the spacing of elements in grids. Change the margin and paddings and _Align self_ for the image in order to place it in the center of the cell. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec5acab3-8a9c-43aa-9da4-dfea34387d5f/webflow-platform-futureimage15.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec5acab3-8a9c-43aa-9da4-dfea34387d5f/webflow-platform-futureimage15.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec5acab3-8a9c-43aa-9da4-dfea34387d5f/webflow-platform-futureimage15.png'>Large preview</a>)" alt="" >}}

Now it’s time to replace the dummy content with real content. To start adding images, we’ll need to click on the gear icon for the Image element and select the image of our choice.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ab0af14-4096-4ffc-87ef-9ec0b47133dc/webflow-platform-futureimage14.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ab0af14-4096-4ffc-87ef-9ec0b47133dc/webflow-platform-futureimage14.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ab0af14-4096-4ffc-87ef-9ec0b47133dc/webflow-platform-futureimage14.png'>Large preview</a>)" alt="" >}}

Notice that Webflow stores all images in a special area called _Assets_. Any media we add, whether it’s a video or image, goes straight to that area.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4a7afff-46e8-4e2c-8bf4-7a06cc13643e/webflow-platform-futureimage17.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4a7afff-46e8-4e2c-8bf4-7a06cc13643e/webflow-platform-futureimage17.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4a7afff-46e8-4e2c-8bf4-7a06cc13643e/webflow-platform-futureimage17.png'>Large preview</a>)" alt="" >}}

After we introduce an image to the layout, we need to modify the Heading and Text sections.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b7ef06a-319f-45dc-84f8-e12476232742/webflow-platform-futureimage11.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b7ef06a-319f-45dc-84f8-e12476232742/webflow-platform-futureimage11.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b7ef06a-319f-45dc-84f8-e12476232742/webflow-platform-futureimage11.png'>Large preview</a>)" alt="" >}}

Webflow provides a visual style for every element we use in our design. Let’s take a Heading section as an example: It’s possible to play with font color, font, weight, spacing, shadows, and other visual properties of this object. Here is what we will have when adding real copy and playing with font color.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab5e96e1-9efb-4095-b98c-859f7f554c86/webflow-platform-futureimage2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab5e96e1-9efb-4095-b98c-859f7f554c86/webflow-platform-futureimage2.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab5e96e1-9efb-4095-b98c-859f7f554c86/webflow-platform-futureimage2.png'>Large preview</a>)" alt="" >}}

Once we have a nice and clean hero section, we can add content to our zig-zag layout.

Notice that every time we style something, we give it a _Selector_ (a class), so Webflow will know that the style should be applied specifically for this element. We can use the same class to style other elements. In our case, we need the same style for images, headings, descriptions, and links that we have in the zig-zag layout. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dde40b1-2b44-42d3-ad44-fb0c12d8205b/webflow-platform-futureimage16.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dde40b1-2b44-42d3-ad44-fb0c12d8205b/webflow-platform-futureimage16.png" sizes="100vw" caption="Applying the same “benefit” style for all images in the zig-zag section. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dde40b1-2b44-42d3-ad44-fb0c12d8205b/webflow-platform-futureimage16.png'>Large preview</a>)" alt="" >}}

Webflow also allows creating combo classes &mdash; when one class is used as a base class, and another class is used to override the styling options of the base class. In the example below, we override the default font color of the Heading using the class “Zig-Heading-Second.” Combo classes can save you a lot of time because you won’t need to create a style from scratch. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39587592-726b-4836-8665-d8459b64f6c8/webflow-platform-futureimage18.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39587592-726b-4836-8665-d8459b64f6c8/webflow-platform-futureimage18.png" sizes="100vw" caption="Using a combo class for the Heading. The orange indicator is used to highlight the properties that were inherited from the base class. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/39587592-726b-4836-8665-d8459b64f6c8/webflow-platform-futureimage18.png'>Large preview</a>)" alt="" >}}

Here is how our layout will look like after the changes:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55fde3e2-cbde-4367-9bca-c87b2d4ae12d/webflow-platform-futureimage8.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55fde3e2-cbde-4367-9bca-c87b2d4ae12d/webflow-platform-futureimage8.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55fde3e2-cbde-4367-9bca-c87b2d4ae12d/webflow-platform-futureimage8.png'>Large preview</a>)" alt="" >}}

Webflow provides a very helpful feature for aligning content named “guide overlay” which can be located in the left menu panel. When you enable the guide, you will see the elements that are breaking the grid.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23803c93-a0a8-4adb-bd02-b955e9e7dbe6/webflow-platform-futureimage28.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23803c93-a0a8-4adb-bd02-b955e9e7dbe6/webflow-platform-futureimage28.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23803c93-a0a8-4adb-bd02-b955e9e7dbe6/webflow-platform-futureimage28.png'>Large preview</a>)" alt="" >}}

After finishing with a zig-zag layout, we need to add information on voice commands in the Slider. Add a Heading section in a relevant slide and change the visual styling options of this object.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc4681bd-6b8a-4c17-9dac-ea6f25cac8ad/webflow-platform-futureimage23.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc4681bd-6b8a-4c17-9dac-ea6f25cac8ad/webflow-platform-futureimage23.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc4681bd-6b8a-4c17-9dac-ea6f25cac8ad/webflow-platform-futureimage23.png'>Large preview</a>)" alt="" >}}

It’s that simple!

Last but not least, we need to add a contact form to our website. Let’s add a section right underneath of Slider. 

There are two ways we can add a form to the page. First, Webflow has a special element for web forms called _Form Block_. A form created using Form Block has three elements: Name, Email Address, and a Submit button. For our form, we will need a Message field. We can easily create one by duplicating the element Email Address and renaming it. By default, the Form Block has 100% width alignment, meaning it will take the entire width of the container. We will use the Grid settings to adjust the form width. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e677999d-33d6-4447-a6af-43a4413631ae/webflow-platform-futureimage19.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e677999d-33d6-4447-a6af-43a4413631ae/webflow-platform-futureimage19.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e677999d-33d6-4447-a6af-43a4413631ae/webflow-platform-futureimage19.png'>Large preview</a>)" alt="" >}}

Secondly, Webflow allows integrating custom code right in the page. It means that we can create a form in a tool like Typeform, copy the embed code it provides and place it to the component called _Embed_ that we placed to the section. Note that embeds will only appear once the site has been published or exported &mdash; not while you're designing the site.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5aae962-c6c1-407a-a6a8-c25ae280b806/webflow-platform-futureimage7.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25bae10e-2e58-427e-86e8-c2e15a5cd439/7-webflow-platform-futureimage.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5aae962-c6c1-407a-a6a8-c25ae280b806/webflow-platform-futureimage7.png'>Large preview</a>)" alt="" >}}

Once all elements are in place, we need to optimize our design for mobile. Almost [half of the users](https://www.statista.com/statistics/277125/share-of-website-traffic-coming-from-mobile-devices/) (globally) access websites on mobile. What you can do within Webflow is to resize the browser window so that you can see how your design looks like with different breakpoints.

Let’s change our view to Mobile by clicking on the _Mobile - Portrait_ icon.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a63f743f-4a52-432d-ad38-8488efb60ee3/webflow-platform-futureimage4.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a63f743f-4a52-432d-ad38-8488efb60ee3/webflow-platform-futureimage4.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a63f743f-4a52-432d-ad38-8488efb60ee3/webflow-platform-futureimage4.png'>Large preview</a>)" alt="" >}}

As you can see, the design looks bad on mobile. But it’s relatively easy to optimize the design using Webflow: It allows you to change the order of elements, the spacing between elements, as well as other visual settings to make the design look great on mobile.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc3888b2-5a41-4788-b0db-3a78d071c286/webflow-platform-futureimage20.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc3888b2-5a41-4788-b0db-3a78d071c286/webflow-platform-futureimage20.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc3888b2-5a41-4788-b0db-3a78d071c286/webflow-platform-futureimage20.png'>Large preview</a>)" alt="" >}}

After we’re done making changes to our design, we have two options: we can export the design and use it on our own web hosting (i.e., integrate it into your existing CMS) or we can use Webflow’s own hosting provided. If we decide to use the second option, we need to click the _Publish_ button and select the relevant publishing options, i.e. either publish it on the webflow.io domain or on a custom domain.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a29d2cd-5f84-42a9-9b68-4b16114a2b0b/webflow-platform-futureimage6.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a29d2cd-5f84-42a9-9b68-4b16114a2b0b/webflow-platform-futureimage6.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a29d2cd-5f84-42a9-9b68-4b16114a2b0b/webflow-platform-futureimage6.png'>Large preview</a>)" alt="" >}}

If you decide to export the code, Webflow will prepare a full zip with HTML, CSS, and all the assets you’ve used to create your design. The exported code will help you build a solid foundation for your product. 

## Conclusion

Webflow is an excellent tool for building high-fidelity prototypes and inviting feedback from team members and stakeholders. People who will review your prototype won’t need to imagine how the finished product will behave and look &mdash; they can _experience_ it instead!

The tool simplifies the transition from a prototype into a fully finished UI because you’re designing products with real code, as opposed to creating clickable mocks in Sketch or any other prototyping tool. You won’t waste time by using one piece of software to build prototypes and another to turning those prototypes into real products. [Webflow](https://webflow.com/?utm_medium=external&utm_source=smag) solves this problem for you.

{{< signature "ms, ra, il" >}}

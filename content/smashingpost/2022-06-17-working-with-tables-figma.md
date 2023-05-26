---
title: 'How To Easily Build And Support Tables In Figma'
slug: easy-build-support-tables-figma
author: andrii-zhdan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47932465-87b0-41aa-97c3-4a2690860dd8/easy-build-support-tables-figma.jpg
date: 2022-06-17T09:00:00.000Z
summary: >-
  User interface designers work with tables on a daily basis. The table is often a complex combination of text components, lines, rectangles, and icons which could be very difficult to work with, especially if you also need to support different screen resolutions, change the order of columns, and use real-life content. In this article, Andrii shares his approach to managing tables in Figma with a bit less pain.
description: >-
  In this article, Andrii shares his approach to managing tables in Figma in an easier, more streamlined way when there is a need to support different screen resolutions, change the order of columns, and use real-life content.
categories:
  - UI
  - Figma
  - Guides
  - Workflow
---

The table is one of the most painful components designers have to deal with in their daily design lives. The table element is often a complex combination of text components, lines, rectangles, icons, and more. It soon may become a nightmare to work with, especially if you also want to support different screen resolutions, change the order of columns, and use real-life content.

In my projects, approximately half of the user interface designs I am working on are **tables**. This is why in this article, I’d like to share my approach to managing tables in Figma in an easier, more streamlined way. 

I’m not a fan of long reads with too many unnecessary details, so I’ll “jump” into the subject right away. My guide consists of several parts; thus, you can stop reading at any point when you understand that what you have learned so far covers your needs at the moment, and you can go back/or jump forward to any section when you want to refresh your memory or learn about the more complex workflows. Let’s go!

**Table of Contents**

- [Cells and Table Structure](#cells-and-table-structure)
- [Real Data and Column Size Corrections](#real-data-and-column-size-corrections)
- [Responsive Tables](#responsive-tables)
- [Basic Table Kit and States](#basic-table-kit-and-states)
- [Figma Design file](#figma-design-file)
- [Conclusion](#conclusion)

**Note:** *This article is aimed at people with some experience using Figma Design. If you are an absolute beginner in the Figma field, I would suggest first checking some basic Figma tutorials. To make things easier for you, near the end of the article (check* [***Figma Design File***](#figma-design-file) section)*, I have provided my Figma Design which you can use for deconstruction and learning purposes.*

## Cells And Table Structure

I often use the [Ant Design System](https://ant.design/) in my projects. Let’s take their table components as an example.

To start, we need to make only **two** simple components in Figma:

- a head cell,
- a row cell.

Use `Left` and `Center` in `Constraints` to align the text.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b67cf31-0f93-45e1-b865-b0788751b01d/1-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b67cf31-0f93-45e1-b865-b0788751b01d/1-how-build-support-tables-figma.png" width="800" height="311" sizes="100vw" caption="Create two components: a <strong>head</strong> cell, and a <strong>row</strong> cell. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b67cf31-0f93-45e1-b865-b0788751b01d/1-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot of two components in Figma: a head cell, and a row cell" >}}

<blockquote><strong>Aside on keyboard shortcuts:</strong><br /><br /><span style="font-style: normal"><kbd>Ctrl</kbd>/<kbd>Cmd</kbd> &mdash; Win/Mac<br /><kbd>Alt</kbd>/<kbd>Option</kbd> &mdash; Win/Mac<br /><kbd>Shift</kbd> &mdash; Win and Mac<br /><br />Figma is a tool that works on both Windows and Mac. For example, the following keyboard shortcut combo <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>D</kbd> means, “Press <kbd>Ctrl</kbd> + <kbd>D</kbd> on Windows, or press <kbd>Cmd</kbd> + <kbd>D</kbd> on Mac.”</span></blockquote>

Then we need to copy the components for our future table:

- hold <kbd>Alt</kbd>/<kbd>Option</kbd> + <kbd>Shift</kbd> + left mouse button for copying
- and <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>D</kbd> to repeat the last action in Figma.

{{< vimeo id="720634901" caption="Let’s copy the components for our future table." breakout="true" >}}

Now we have to set the space between the cells and create the components: <kbd>Alt</kbd>/<kbd>Option</kbd> + <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>K</kbd>. 

**Useful tip:** *I have used zero spacing in the example below, but if you need vertical lines, use 1 `px`.*

{{< vimeo id="720636315" caption="Create the table head and the table row components." breakout="true" >}}

**Useful tip:** *I recommend naming the components on every level. Organise everything early, organise everything thoroughly!*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fef7d90-888e-496b-884a-4e8cca16e250/4-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fef7d90-888e-496b-884a-4e8cca16e250/4-how-build-support-tables-figma.png" width="800" height="302" sizes="100vw" caption="Naming the components. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fef7d90-888e-496b-884a-4e8cca16e250/4-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot showing the naming of the components." >}}

How to create the table lines? Start here:

- press and hold <kbd>Alt</kbd>/<kbd>Option</kbd> + <kbd>Shift</kbd> + mouse left for copying,
- and <kbd>Ctrl</kbd>/<kbd>Cmd</kbd>+ <kbd>D</kbd> to repeat the last action in Figma.

{{< vimeo id="720640927" caption="Copying and arranging the table rows." breakout="true" >}}

And now, let’s say that we need a table with the following parameters:

- horizontal lines between the rows: 1 `px`, blue color;
- green colored stroke (table border);
- corner radius: 15 `px`.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27da4225-7ba9-4ff9-8d1e-ee5ab122e4c3/6-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27da4225-7ba9-4ff9-8d1e-ee5ab122e4c3/6-how-build-support-tables-figma.png" width="800" height="561" sizes="100vw" caption="Styling the table border, the row lines, and the table corner radius. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27da4225-7ba9-4ff9-8d1e-ee5ab122e4c3/6-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot showing the process of styling the table border, the row lines, and setting the table corner radius" >}}

How did I do it? Here are the steps:

1. group the table row elements into a single frame;
2. set corners’ radius to 15 `px`;
3. set outline stroke to 1 `px`, `#49E36B`;
4. set frame fill color to `#278EEE`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ca485b-c3c1-4929-8665-8fed4e4ed39b/7-how-build-support-tables-figma.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ca485b-c3c1-4929-8665-8fed4e4ed39b/7-how-build-support-tables-figma.jpeg" width="800" height="480" sizes="100vw" caption="Group the table row elements into a single frame and adjust the parameters. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ca485b-c3c1-4929-8665-8fed4e4ed39b/7-how-build-support-tables-figma.jpeg'>Large preview</a>)" alt="A screenshot showing how to group the table row elements into a single frame and then adjust the parameters." >}}

To help you better imagine how it works, here is a quick illustration that I made:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03bbb5f6-56ae-432a-b74d-26cbb4e77516/8-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03bbb5f6-56ae-432a-b74d-26cbb4e77516/8-how-build-support-tables-figma.png" width="800" height="537" sizes="100vw" caption="The table elements. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03bbb5f6-56ae-432a-b74d-26cbb4e77516/8-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot showing the table elements, highlighted in different colors" >}}

The frame is for coloring the table lines between the rows and the table stroke (the outside table border). And you will need to add “crop frame content” and “corner radius” to shape the table.

If you add “Auto layout,” it would work like this:

{{< vimeo id="720644043" caption="Add “Auto layout.”" breakout="true" >}}

Use <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>C</kbd> and <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>V</kbd> to add lines, and <kbd>Delete</kbd> to remove some of them.

{{% feature-panel %}}

## Real Data And Column Size Corrections

Now let’s fill the table with some data. Hold <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> to highlight text layers in the frame. 

I use the [Content reel](https://www.figma.com/community/plugin/731627216655469013/Content-Reel) plugin for this purpose. 

{{< vimeo id="720646239" caption="Using the Content Reel plugin for adding data to our table." breakout="true" >}}

You can use “Auto layout” to change the columns’ order and size:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ef3d701-0596-45ac-a051-fe5174a0ec66/11-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ef3d701-0596-45ac-a051-fe5174a0ec66/11-how-build-support-tables-figma.png" width="800" height="239" sizes="100vw" caption="Frame → Horizontal → Fixed (for the row). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ef3d701-0596-45ac-a051-fe5174a0ec66/11-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot showing how to set the Frame to Fixed size (for the row)" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f299511-298c-4a71-ab58-0409572335e2/12-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f299511-298c-4a71-ab58-0409572335e2/12-how-build-support-tables-figma.png" width="800" height="284" sizes="100vw" caption="Frame → Horizontal → Fill (for the cell). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f299511-298c-4a71-ab58-0409572335e2/12-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot showing how to set the Frame to Fill option (for the cell)" >}}

As a result, you would get this behavior. Hold <kbd>Shift</kbd> and double-click to highlight it, then resize the column.

{{< vimeo id="720648603" caption="How to change the columns’ order and size." breakout="true" >}}

## Responsive Tables

Now I want to make this table **responsive** for different screens. 

The expected results:

- head cell (140): fixed 140 `px` size,
- row cell (140): fixed 140 `px` size,
- head cell (&#126;): responsive,
- row cell (&#126;): responsive.

For this, we need `Auto layout` and to use a horizontal frame `Fixed` size option for the rows:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8231abeb-46e2-44cf-96f9-4a474456af06/14-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8231abeb-46e2-44cf-96f9-4a474456af06/14-how-build-support-tables-figma.png" width="800" height="229" sizes="100vw" caption="Frame → Horizontal → <code>Fixed</code> (for the rows). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8231abeb-46e2-44cf-96f9-4a474456af06/14-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot showing how to set the Frame to Fixed size (for the rows)" >}}

For fixed-size cells, we apply `Fixed` horizontally:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e8459e-f303-47b9-a249-9aed5ff68cee/15-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e8459e-f303-47b9-a249-9aed5ff68cee/15-how-build-support-tables-figma.png" width="800" height="242" sizes="100vw" caption="Frame → Horizontal → <code>Fixed</code> (for the fixed-size cells). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e8459e-f303-47b9-a249-9aed5ff68cee/15-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot showing how to set the Frame to Fixed size (for the fixed size cells)" >}}

For the responsive cells, we need to set `Fill` horizontally:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69cdcfd2-621c-43d3-b8ae-269c13ad5ca6/16-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69cdcfd2-621c-43d3-b8ae-269c13ad5ca6/16-how-build-support-tables-figma.png" width="800" height="241" sizes="100vw" caption="Frame → Horizontal → <code>Fill</code> (for the responsive cells). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69cdcfd2-621c-43d3-b8ae-269c13ad5ca6/16-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot showing how to set the Frame to Fill option (for the responsive cells)" >}}

Then we turn this table into a `Frame`, and every row inside the `Frame` should have horizontal `Constraints` set as `Left and right`:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46fb80a2-2971-4f4c-9fb6-1f20350e5442/17-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46fb80a2-2971-4f4c-9fb6-1f20350e5442/17-how-build-support-tables-figma.png" width="800" height="300" sizes="100vw" caption="Constrains → Horizontal → <code>Left and right</code> (for all rows in the table). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46fb80a2-2971-4f4c-9fb6-1f20350e5442/17-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot showing how to set Constraints (Horizontal) to Left and right (for all rows)." >}}

Voilà, we’re fully responsive now!

{{< vimeo id="720674193" caption="The table is responsive now!" breakout="true" >}}

{{% ad-panel-leaderboard %}}

## Basic Table Kit And States

Even for a simple project, you need more states.

Let’s build a basic kit for a table and link new combinations to the two primary components as `variants`.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ae461fe-06d2-4b4c-a7aa-6d73294c3b30/19-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ae461fe-06d2-4b4c-a7aa-6d73294c3b30/19-how-build-support-tables-figma.png" width="800" height="480" sizes="100vw" caption="Building a basic table kit. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ae461fe-06d2-4b4c-a7aa-6d73294c3b30/19-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot of building a basic table kit in Figma" >}}

**The kit structure:**

- icons we use in the table,
- basic header states,
- basic cell states.

### Icons

Using any icon library, you can have a few hundred icons. As a result, this can push you to inconsistency (using different icons for the same goals, for example), especially if you have more than one designer on your team. Table icons as a separate library will help you manage and support consistency on big projects.

### Combinations

There are a few main combinations we have: 

- just text in a cell,
- just an icon or a set of icons in a cell,
- a variety of text, icons, and other objects (checkbox, toggle, action, select, and so on) in a different order within a cell.

Avoid hidden layers! You will know that you used them while building a design system, and you will certainly forget about them later. In addition, people who will use your design system may not know about these hidden layers at all.

You will have an idea of how to create them based on the illustration above (**Building a basic table kit**), but I’ll specify a few more complex components for beginner designers.

{{< vimeo id="720677473" caption="An example of components’ behavior that we need." breakout="true" >}}

The first one is simple:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e838ae84-9967-41a6-a37b-b3568216811a/21-how-build-support-tables-figma.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e838ae84-9967-41a6-a37b-b3568216811a/21-how-build-support-tables-figma.jpg" width="800" height="285" sizes="100vw" caption="Set the following constraints options. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e838ae84-9967-41a6-a37b-b3568216811a/21-how-build-support-tables-figma.jpg'>Large preview</a>)" alt="A screenshot showing specific constraints options" >}}

And we use `Auto layout` with the following parameters in the second component example:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cb2ab41-9de7-4a12-b3ce-d222ad42036a/22-how-build-support-tables-figma.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cb2ab41-9de7-4a12-b3ce-d222ad42036a/22-how-build-support-tables-figma.jpg" width="800" height="535" sizes="100vw" caption="The text can change the Frame size, and the icon should always be on the right side. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cb2ab41-9de7-4a12-b3ce-d222ad42036a/22-how-build-support-tables-figma.jpg'>Large preview</a>)" alt="A screenshot which shows how the text can change the Frame size, and where the icon should always be on the right side" >}}

So, remember the table that we built using only two components? It’s time to update it!

{{< vimeo id="720681115" caption="Applying the new cell types to the initial table created from two components." breakout="true" >}}

The main idea of this article was to learn how to be more flexible with tables in Figma. And as I have demonstrated, in the beginning, you need to create only two simple components, then do some wire-framing, and finally, when you need to breathe more “life” into your table, just add more states. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b324946-e254-43fb-b579-5e7193e305a0/24-how-build-support-tables-figma.jpeg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b324946-e254-43fb-b579-5e7193e305a0/24-how-build-support-tables-figma.jpeg" width="799" height="394" sizes="100vw" caption="The basic table kit that we made in Figma. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b324946-e254-43fb-b579-5e7193e305a0/24-how-build-support-tables-figma.jpeg'>Large preview</a>)" alt="A screenshot showing the table kit that we made in Figma" >}}

Also, you can use “Figma Properties” to make it compact. All the instructions you can find in the following tutorial video created by the Figma team during [Figma Config 2022](https://www.figma.com/blog/config-2022-thinking-big-and-acting-with-urgency/): “Jumping into component properties.”

{{< youtube id="hobK6JqADio" breakout="true" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f761a45b-8829-4f7f-ba69-906dc63dd2a6/25-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f761a45b-8829-4f7f-ba69-906dc63dd2a6/25-how-build-support-tables-figma.png" width="800" height="535" sizes="100vw" caption="Example of the structure using ‘Figma Properties’. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f761a45b-8829-4f7f-ba69-906dc63dd2a6/25-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot showing an example of the structure using Figma Properties" >}}

It’s only one example of how I structured the basic table kit in this article. You can use a similar workflow or create your own. In my projects, kits are much more complex, so I’ll leave this choice to you. 

### Figma Design File

I have prepared a [**Figma Design file**](https://www.figma.com/file/UTy6ZCJ7MAnFz5udAZp2gB/SM?node-id=0%3A1) that may help you go through some of the steps of my tutorial. If you have questions or need help, do post your questions in the comments section at the end of the article.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ea18d2c-e663-40d2-9774-8b8a5f4d1415/26-how-build-support-tables-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ea18d2c-e663-40d2-9774-8b8a5f4d1415/26-how-build-support-tables-figma.png" width="800" height="419" sizes="100vw" caption="The table that I have created (<a href='https://www.figma.com/file/UTy6ZCJ7MAnFz5udAZp2gB/SM?node-id=0%3A1'>Figma Design file</a>) for the purposes of this tutorial. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ea18d2c-e663-40d2-9774-8b8a5f4d1415/26-how-build-support-tables-figma.png'>Large preview</a>)" alt="A screenshot of the table that I have created in Figma Design for the purposes of this tutorial" >}}

{{% ad-panel-leaderboard %}}

## Conclusion

The way I am working with tables in Figma is not as black and white. The approach mainly depends on the product you’re designing and, of course, there are a few possible ways you could achieve the same goals.

Here are a few general recommendations I can make from my own practice:

- Keeping the line components on the design system side provides a chance to update tables for the whole project from one place. But every time you want to make an update, you will need to publish changes on the **design system-level**.
- If you keep tasks in different documents, don’t forget to **disconnect that file from the design system**. This would help avoid uncontrolled updates that you will miss.
- At first, using resizable components seems too tempting… until you need to begin supporting different styles in every size. If you have tables with varying line heights, **it’s better to create individual components for each one of them.**
- There is an approach that consists of using *as few components* as possible. But most of the time, you don’t look at your components &mdash; instead, you use “variants” to switch between them. So, it’s **better to have enough separate components and, as a result, “variants”** than to use hidden layers, the “Auto layout” option, and components inside other components that would be hard to manage later on.
- Check that all table cells support **at least** two lines of text. You can use 16 `px` line spacing to make it happen.  
- I recommend using the **minimum width for parent components** (minimum width for each column). But these default minimum sizes have to be discussed with the front-end developers as they may sometimes have their own limitations. Therefore you need to ensure that everything in the design can be implemented in the later development stages.
- **Create a color palette in your Design System for the tables**, so you would be able to control all the colors from one place. Of course, you can use shared colors from the palette, but once you need to change text color in the tables, background, or something else, you will get into trouble. 
- **Create different text styles for the tables.** For example, we use smaller line spacing in tables than in news feeds or articles. Having separate text settings would help you avoid future conflicts.

Thank you for following me along! As I already said, tables are a complex component, and I can talk about this topic for days. But maybe better to stop here and give you a chance to try this approach for yourself. Then, if you have questions, I’d be happy to reply and help! Or I could write another article: “Working With Tables in Figma: The Pro Level.” ;-)

### Further Reading

I have collected a few links to resources (tutorials, plugins, discussions, etc.) related to working with tables in Figma:

- “[Creating Tables In Figma](https://www.smashingmagazine.com/2019/09/creating-tables-in-figma/),” Sasha Belichenko  
*A guide about one possible way of working with tables in Figma: how to create a table using components and Atomic Design methodology, and then how to integrate the table into your design system.*
- “[Create a Figma Prototype with Data from Google Sheets](https://spin.atomicobject.com/2022/02/15/google-sheets-sync/),” Bryan Elkus  
*The article covers in detail a plugin for Figma called* ***Google Sheets Sync.*** *It allows a user to pull in content directly from Google Sheets which is super-useful if you want to use this to populate your designs with more realistic data.*
- “[Creating Tables in Figma with Auto Layout](https://www.figma.com/community/file/809752704119681183)”, Gavin McFarland  
*In this tutorial, Gavin explains how to modify tables in Figma which are completely fluid (with the Auto Layout feature). You can inspect the components in Figma Design to see how they were created.*

#### Tweets

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I spend my whole Figma life designing tables. I imagine other designers too. <a href="https://twitter.com/figma?ref_src=twsrc%5Etfw">@figma</a> can you please give us more features, like draggable horizontal rows AND vertical columns? Moving data around should be super easy, like Google Sheets.</p>&mdash; Joshua Sortino (@sortino) <a href="https://twitter.com/sortino/status/1513577995407179784?ref_src=twsrc%5Etfw">April 11, 2022</a></blockquote> 

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I have a love/hate relationship with tables, so here&#39;s how I set up my design system to make things easier. Rows vs. columns, cell variants, and a &quot;module&quot; component with a variable toolbar and variable pagination.<a href="https://t.co/0MbCROJAmp">https://t.co/0MbCROJAmp</a> <a href="https://t.co/xztjdwoVeL">pic.twitter.com/xztjdwoVeL</a></p>&mdash; Jon Moore (@TheJMoore) <a href="https://twitter.com/TheJMoore/status/1513844779431387151?ref_src=twsrc%5Etfw">April 12, 2022</a></blockquote> 

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">We hear tables in <a href="https://twitter.com/figma?ref_src=twsrc%5Etfw">@figma</a> are hard, and we agree.<br><br>Here&#39;s how we leveraged our internal design tools to create a more seamless workflow for designers across the <a href="https://twitter.com/DesigningUber?ref_src=twsrc%5Etfw">@DesigningUber</a> team ➡️ <a href="https://t.co/R8PwiYdebK">pic.twitter.com/R8PwiYdebK</a></p>&mdash; Vincent van der Meulen (@vincentmvdm) <a href="https://twitter.com/vincentmvdm/status/1513630608274051074?ref_src=twsrc%5Etfw">April 11, 2022</a></blockquote> 

*A short Twitter thread on this topic, also mentioning the Configurator plugin that Vincent’s team made.*

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I found a pretty reliable way to create flexible, responsive custom tables in Figma. I’ll do a video walkthrough at some point, but if you want to play… <a href="https://t.co/cibZI3Uk4g">https://t.co/cibZI3Uk4g</a></p>&mdash; Buzz Usborne (@buzzusborne) <a href="https://twitter.com/buzzusborne/status/1511604883748622343?ref_src=twsrc%5Etfw">April 6, 2022</a></blockquote> 

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Did I make a full video about building tables in Figma? Yes. Do I regret going down this rabbit hole? Also yes. 📺🕳️ <a href="https://t.co/JCyLxEBktG">https://t.co/JCyLxEBktG</a></p>&mdash; Buzz Usborne (@buzzusborne) <a href="https://twitter.com/buzzusborne/status/1514098048796065798?ref_src=twsrc%5Etfw">April 13, 2022</a></blockquote> 

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Tips time!<br><br>Using component props, we can create &quot;infinite tables&quot;<br><br>So we can toggle on however many columns / rows we need in designs<br><br>This prevents us maintaining large variant sets for every permutation of table 🍽<br><br>Community file to play with: <a href="https://t.co/WqNM5SMjSE">https://t.co/WqNM5SMjSE</a> <a href="https://t.co/yhefqrNImC">pic.twitter.com/yhefqrNImC</a></p>&mdash; luis. (@disco_lu) <a href="https://twitter.com/disco_lu/status/1531278254723567616?ref_src=twsrc%5Etfw">May 30, 2022</a></blockquote>

*Note: This technique is interesting if you have just a few tables in the product design. Otherwise it would be a problem to scale the system.*

As you can see, dealing with tables is a “hot topic” 🔥 in the Figma design community! I hope that you could find something useful here, too.

<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

{{< signature "mb, yk, il" >}}

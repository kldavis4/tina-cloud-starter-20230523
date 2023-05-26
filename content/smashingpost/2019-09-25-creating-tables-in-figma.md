---
title: 'Creating Tables In Figma'
slug: creating-tables-in-figma
author: sasha-belichenko
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d08b37a-9f74-4ec9-9cd9-acfdc924a4e8/tables-in-figma-mockup.png
date: 2019-09-25T12:30:59+02:00
summary: >-
  This is a detailed guide for those who are struggling with tables in Figma. We’ll create a table using components, so that later on you could save a lot of time on scalability and edits. Moreover, you’ll be able to easily integrate the table into your design system.
description: >-
  This is a detailed guide for those who are struggling with tables in Figma. We’ll create a table using components, so that later on you could save a lot of time on scalability and edits. Moreover, you’ll be able to easily integrate the table into your design system.
categories:
  - UX
  - UI
  - Figma
  - Workflow
---
In this tutorial, we will talk about how tables can be created in Figma by using components and Atomic Design methodology. We will also take a look at the basic elements of the table layout and how components can be included in the component library so that they can become part of the design system you are using. 

To make it easy for you, I’ve prepared a <a href="#figma-table-mockup-download">mockup example</a> that uses all of the components we need for this tutorial.

To follow along, you will need to have at least some understanding of the basic Figma concepts, its interface, and how to work with Figma components. However, if you’re new to Figma and working with table data, I recommend watching the “[Getting Started](https://www.youtube.com/watch?v=T0kRCTOX0zY)” video to help you better understand Figma end-to-end, as well as the article “[How To Architect A Complex Web Table](https://www.smashingmagazine.com/2019/02/complex-web-tables/)” that was published not too long ago here on Smashing Magazine.

To simplify the scope of this tutorial, let’s assume that the colors, fonts, and effects already exist as styles in the Figma project you’re about to begin. In terms of Atomic Design, they are **atoms**. (To learn more, the folks at *littleBits* wrote [a great article on the topic](https://blog.prototypr.io/creating-atomic-components-in-figma-90c6128d6cbe).)

The target audience for this tutorial are designers (UX, UI) who have either already adopted Figma into their workflows or are planning to try Figma in their next design projects but aren’t sure how to get started.

So, without further ado, let’s dig in!

**Quick Note**: *While writing this article, [Figma introduced plugins](https://www.figma.com/blog/introducing-figma-plugins/). At the time of publishing, there weren’t any good ones for working with tables, but things might change fast. Who knows, maybe this article will actually help an aspiring Figma plugin developer to create a really neat Figma Tables plugin, or at least, I hope it will.* 😉

{{% feature-panel %}}

## Introduction

Imagine the table as an organism. The table cell is then a molecule which is comprised of individual atoms. In design terms, they’re **cell properties**. 

So, let’s start with the cell. It has three properties:

<ol>
	<li><a href="#background">Background</a></li>
	<li><a href="#border">Border</a></li>
	<li><a href="#content">Content</a></li>
</ol>

Now we’ll take a closer look at each one of them. 

## Background

The background will be a separate component in Figma. The size doesn’t really matter since we can stretch the component as we need, but let’s begin with setting the size to 100&times;36 pixels.

In this component, add a rectangle of the same size as the component itself. It will be the only object inside the component. We need to attach the rectangle’s borders to the component’s borders by using constraints (set constraints to “Left & Right” and “Top & Bottom” at the right panel in the *Constraints* section), so that the rectangle stretches automatically to the size of the component.

*If you’d like to see this in action, [watch this tutorial](https://www.youtube.com/watch?v=rRQAQ1d9q9w) on how the constraints work in Figma.*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d9f3aff-354f-4617-baa1-d7bc36380613/1-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d9f3aff-354f-4617-baa1-d7bc36380613/1-tables-in-figma.png" sizes="100vw" caption="The Background Component (the ‘atom’) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d9f3aff-354f-4617-baa1-d7bc36380613/1-tables-in-figma.png'>Large preview</a>)" alt="The Background Component" >}}

The fill color of the rectangle will determine the background color of the cell. Let’s pick the white color for it. I recommend choosing that color from the color styles that are configured at the beginning of the project.  

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2308ca98-afed-435b-8e82-8cbba004eee9/samplebg.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59a371cc-8aa0-4278-a220-785319f141c5/sample-bg-800w.gif" width="800" height="" alt="Background color" /></a><figcaption>Changing the background color (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2308ca98-afed-435b-8e82-8cbba004eee9/samplebg.gif">Large preview</a>)</figcaption></figure>

## Border

This one is a bit trickier than the background. You can’t just create one rectangle with a stroke. We may need different kinds of borders: one for the separate cells (with borders around), one for the whole row of cells with only top and bottom borders, or one for the table header that we might want to separate from the rest with a wider line. There are many options. 

Border properties:

- Border line (left, right, top, bottom, or absence of any of them)
- Line width 
- Line color 
- Line style

Each line within the cell border might havea  different width, color, and style. For example, the left one could be a continuous red line, and the top one a dotted grey line. 

Let’s create a component with a size of 100&times;36 pixels (the same as we did before). Inside the component, we need to add 4 lines for each border. Now pay attention to how we are going to do this.

1. Add a line for the **bottom border** with the length of the component width;
2. Set its position to the bottom border and constraints to stretch horizontally and stick to the bottom border;
3. For the **top border**, duplicate the line for the bottom border, rotate it by 180 degrees and stick to the top of the component. (Don’t forget to change its constraints to stick to the top and stretch horizontally.);
4. Next, for the **left border**, simply rotate by -90 degrees and set its position and constraints to be at the left side sticking to the left border and stretching vertically;
5. Last but not least, you can create the **right border** by rotating it by 90 degrees and setting its position and constraints. Set stroke color and stroke width for each line to gray (select from the color styles) and 1 pixel respectively.
 
**Note**: *You may be asking yourself why we rotated the line for the bottom border. Well, when you change the stroke width for a line in Figma, it will rise. So we had to set this “rise” direction to the center of the component. Changing the line’s stroke width (in our case it is the border size) won’t expand outside the component (cell).*

{{% ad-panel-leaderboard %}}

Now we can hide or customize the styles separately for every border in the cell.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54b7d486-ca47-47a4-bdc4-a088de0b3539/3-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54b7d486-ca47-47a4-bdc4-a088de0b3539/3-tables-in-figma.png" sizes="100vw" caption="A border component with 1px stroke (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54b7d486-ca47-47a4-bdc4-a088de0b3539/3-tables-in-figma.png'>Large preview</a>)" alt="The Border Component" >}}

If your project has several styles for table borders (a few border examples shown below), you should create a separate component for each style. Simply create a new master component as we did before and customize it the way you need.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ca426bd-c59a-4376-b627-d3f80b6b4e5e/2-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ca426bd-c59a-4376-b627-d3f80b6b4e5e/2-tables-in-figma.png" sizes="100vw" caption="A few extra examples of border styles. Note that the white background is not included in the component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ca426bd-c59a-4376-b627-d3f80b6b4e5e/2-tables-in-figma.png'>Large preview</a>)" alt="Border Styles" >}}

The separate stroke component will save up lots of your time and add *scalability*. If you change the stroke color inside the master component, the whole table will adjust. Same as with the background color above, each individual cell can have its own stroke parameters. 

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbda009b-fa59-4c9f-af9e-3337707ee54c/sampleborder.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d455ecc1-fe02-4f43-9b02-ff3c6c698f1d/sampleborder-800w.gif" width="800" height="" alt="Border’s width and color" /></a><figcaption>Changing border’s width and color (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbda009b-fa59-4c9f-af9e-3337707ee54c/sampleborder.gif">Large preview</a>)</figcaption></figure>

## Content

This is the most complex component of all.

We need to create all possible variations of the table content in the project: plain text, a text with an icon (left or right, different alignment), checkboxes, switches, and any other content that a cell may possibly contain. To simplify this tutorial, please check the components in the <a href="#figma-table-mockup-download">mockup file</a>. How to create and organize components in Figma is a topic for another article.

However, there are a few requirements for content components:

- Components should stretch easily both vertically and horizontally to fit inside a cell;
- The minimum size of the component should be less than the default cell size (especially height, keep in mind possible cell paddings);
- Avoid any margins, so the components can align properly inside a cell;
- Avoid unnecessary backgrounds because a cell itself has it already. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/410e6284-f976-4e1a-a6e6-98bd6745ff3e/4-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/410e6284-f976-4e1a-a6e6-98bd6745ff3e/4-tables-in-figma.png" sizes="100vw" caption="Examples of cell content in components. This is not a complete list; you can use most of the components of your design system inside a table. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/410e6284-f976-4e1a-a6e6-98bd6745ff3e/4-tables-in-figma.png'>Large preview</a>)" alt="Content components examples" >}}

Content components can be created gradually: start with the basic ones like text components and add new ones as the project grows in size. 

The reason we want the content to be in components is the same as with other elements &mdash; it saves uptime. To change the cell’s content, we just need to switch it in the component. 

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49b7a4e1-48c1-4a5f-a63b-f133462c09df/table-components.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb5cbc4a-fb8f-4a2e-b927-8f8cddaee391/table-components-800w.gif" width="800" height="" alt="Changing the component inside the cell" /></a><figcaption>Editing the table using cells components (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49b7a4e1-48c1-4a5f-a63b-f133462c09df/table-components.gif">Large preview</a>)</figcaption></figure>

## Creating A Cell Component

We created all the atoms we need: background, border, content. It’s time to create a cell component, i.e. the molecule made from atoms. Let’s gather all the components in a cell. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40f14761-70b7-40ba-85d0-5cfbcc963b5a/5-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40f14761-70b7-40ba-85d0-5cfbcc963b5a/5-tables-in-figma.png" sizes="100vw" caption="The cell component (the ‘molecule’) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40f14761-70b7-40ba-85d0-5cfbcc963b5a/5-tables-in-figma.png'>Large preview</a>)" alt="The cell component" >}}

Set the background component as the bottom layer and stretch it to the whole cell size (set constraints to “Left & Right” and “Top & Bottom”).

Add the border component with the same constraints as the background component. 

Now to the most complicated part &mdash; the **content content**. 

The cell has paddings, so you need to make a frame with the component’s content. That frame should be stretched to the whole cell size except for the paddings. The content component should also be stretched to the whole frame size. The content itself needs to be deprived of any margins, so all paddings will be set by the cell. 

At the end of the day, cell paddings are the only property in a component that we will set only once without an opportunity to change it later. In the example above, I made it 4px for all sides.

**Note**: *As a fix, you can create columns with empty cells (with no content and width of 16px for example) left and right to the column where extra margin is needed. Or if your table’s design allows, you can add horizontal paddings inside the cell component. For example, cells in Google Material Design have 16px paddings by default.*

Don’t forget to remove the “**Clip content**” option for the cell and frame (this can be done at the right-hand panel in the Properties section). The cell’s content can go out of its borders; for example, when a dropdown is inside your cell and you want to show its state with a popup. 

<p><strong>Note</strong>: <em>We’ll be using this cell style as the main one. Don’t worry if your table has additional styles &mdash; we’ll cover that in the <a href="#table-states">Table States</a> and <a href="#components-not-overrides">Components, Not Overrides</a> sections.</em></p>

## Cell Options For A Standard Table

This step could be optional but if your table needs states then you can’t go without it. And even more so if there is more than one border style in the table.

So let’s create additional cell components from which it’d be easier to build up a table. When working with a table, we will select the appropriate component depending on its position in the table (e.g. depending on the type of borders).

In order to do that, let’s take our cell component and create eight more masters from it. We also need to disable the appropriate layers responsible for borders. The result should look like the image below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d920eee-827a-4d44-954b-e98746099914/6-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d920eee-827a-4d44-954b-e98746099914/6-tables-in-figma.png" sizes="100vw" caption="The cell options we need to build a table. Note that there could be a few extra depending on your table borders styles. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d920eee-827a-4d44-954b-e98746099914/6-tables-in-figma.png'>Large preview</a>)" alt="Cell options" >}}

The top row is for the cells on top and in the middle of the table. The bottom row is only for the cells at the bottom. This way we’ll be able to put the cells one after another with no gaps and keep the same stroke width.  

A few examples: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f1d254-3322-4fdd-9611-9deeda2eaa6e/7-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f1d254-3322-4fdd-9611-9deeda2eaa6e/7-tables-in-figma.png" sizes="100vw" caption="If each cell in the table has a border, we’d only need cells 1, 4, 5 and 8. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f1d254-3322-4fdd-9611-9deeda2eaa6e/7-tables-in-figma.png'>Large preview</a>)" alt="The First example" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/152b96b5-3fd3-4160-9515-3fec6569e2a5/8-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/152b96b5-3fd3-4160-9515-3fec6569e2a5/8-tables-in-figma.png" sizes="100vw" caption="If there are merged cells or border absence, we must apply the rest 2 and 3 cells as well as 6 and 7 to the bottom row. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/152b96b5-3fd3-4160-9515-3fec6569e2a5/8-tables-in-figma.png'>Large preview</a>)" alt="The Second example" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19f7ea7d-8017-474b-87f6-14dab7d5e8f3/9-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19f7ea7d-8017-474b-87f6-14dab7d5e8f3/9-tables-in-figma.png" sizes="100vw" caption="If the table design considers the absence of vertical borders, cells 2 and 6 would be enough. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19f7ea7d-8017-474b-87f6-14dab7d5e8f3/9-tables-in-figma.png'>Large preview</a>)" alt="The Third example" >}}

**Note**: *For each border style created above, it’d be good to add master components like the ones described earlier.*

So we have excluded the necessity of overriding cell’s instances (disabling the appropriate layers, to be precise). Instead of that, we use various components. Now if, for example, a column uses a different style from the default (the fill color or border), you can choose this column and simply change the relative component. And everything will be alright. On the opposite side, changing a border of each cell manually (disabling the appropriate borders) is a pain you don’t want to bother with.

Now we are ready to create tables (in terms of Atomic Design &mdash; organisms) from the various cell components (molecules) we made.

{{% ad-panel-leaderboard %}}

## Customizing The Table 

Changing the row’s height in the whole table is relatively easy: highlight the table, change the element height (in this case, the cell’s height, H in the right-hand panel in the Properties section), and then change the vertical margin from the element to 0. That’s it: changing the line height took two clicks! 

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3391eda3-42c3-44c1-8b81-ec711788e8df/table-size.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba448d33-0336-41b1-8c4a-c75582d53cdf/table-size-800w.gif" width="800" height="" alt="Changing the row height" /></a><figcaption>Changing the row height for the whole table (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3391eda3-42c3-44c1-8b81-ec711788e8df/table-size.gif">Large preview</a>)</figcaption></figure>

Changing the column width: highlight the column and change the width size. After moving the rest of the table close up, select the whole table by using the *Tide Up* option in the *Alignment* panel as well as the first item in the dropdown list under the rightmost icon. 

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33c9658c-55f6-48db-849a-7890cc31b1e0/13-tables-in-figma.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e9eed10-3054-4a56-bb14-0f4449d74f1c/13-tables-figma-800w.gif" width="800" height="" alt="Changing the column width" /></a><figcaption>Changing the column width. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33c9658c-55f6-48db-849a-7890cc31b1e0/13-tables-in-figma.gif">Large preview</a>)</figcaption></figure>

**Note:** *I wouldn’t recommend grouping rows and columns. If you change the column size extending the elements, you’ll get fractional values for width and height. If you don’t group them and snap to the pixel grid, the cell size will remain an integer number.*

The background color, stroke type, and content data can be changed in the appropriate component or in one of the eight cells master components (cells that had different stroke styles). The only parameter that can’t be changed right away is the cell margins, e.g. **content paddings**. The rest are easily customizable. 

## Components, Not Overrides

Looking at what we got in the end, it might seem like overkill. And it is if there is only one table in your project. In this case, you can simply create one cell component and leave the background and stroke components off. Simply include them in the cell component, create the table and do the necessary customization for each separate cell.

But if components are included in a library that is used by a number of other files, here comes the most interesting stuff.

**Note**: *I do not recommend changing the background color and stroke in components' instances. Change them **only in the master**. By doing so, those instances with overrides won’t get updated. This means you would have to do that manually and that’s what we’re trying to avoid. So let’s stick to the master components.*

If we need to create an additional type of table cells (e.g. the table header), we add the necessary set of master components for cells with the appropriate styles (just like we did above with the eight cells that had different stroke styles), and use it. Yes, it takes longer than overriding components’ instances but this way you will avoid the case when changing the masters will apply those changes to all layouts.

## Table States

Let’s talk about the states of the table’s elements. A cell can have three states: default, hover, and selected. Same for columns and rows.

If your project is relatively small, all states can be set by overrides inside instances of your table components. But if it’s a big one, and you’d want to be able to change the look of the states in the future, you’ll have to create separate components for everything. 

You’ll need to add all eight cells with different stroke variants for each of the states (maybe less, depends on the stroke style). And yes, we’ll need separate components for the background color and the stroke for the states as well. 

In the end, it’ll look similar to this: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5360264b-077f-42c7-b8cc-a7ce88618e2a/10-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5360264b-077f-42c7-b8cc-a7ce88618e2a/10-tables-in-figma.png" sizes="100vw" caption="The cells’ states (hover and selected) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5360264b-077f-42c7-b8cc-a7ce88618e2a/10-tables-in-figma.png'>Large preview</a>)" alt="Hover and Selected" >}}

Here’s where a bit of trouble comes in. Unfortunately, if we do everything as described above (when changing the component’s state from one to another), there is a risk of losing the cell’s content. We’ll have to update it apart from the case when the content type is the same as in the master cell. At this point, we can’t do anything about it.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4b162f-c9ba-4e2d-9c04-839a3e13eb33/11-tables-in-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4b162f-c9ba-4e2d-9c04-839a3e13eb33/11-tables-in-figma.png" sizes="100vw" caption="Table with various rows’ states. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb4b162f-c9ba-4e2d-9c04-839a3e13eb33/11-tables-in-figma.png'>Large preview</a>)" alt="Table with rows’ states" >}}

I added tables in the <a href="#figma-table-mockup-download">mockup file</a> that were made in a few different ways: 

- Using this tutorial (separate components for cells’ styles);
- Using the cell component (components for borders, background, and content);
- Using the cell component that unites everything (with only content components in addition).

Try to play around and change the cell’s styles.

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aee8ffc8-8a0e-4e1f-9cda-360fa5ba9644/12-tables-in-figma.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/783ea21b-7d19-442b-945b-aa41e6bbe640/12-tables-in-figma-800w.gif" width="800" height="" alt="Changing the state" /></a><figcaption>Changing the state of the row. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aee8ffc8-8a0e-4e1f-9cda-360fa5ba9644/12-tables-in-figma.gif">Large preview</a>)</figcaption></figure>

## Conclusion

If you’re using the same components library in several projects and you’ve got a reasonable number of tables in each of them, you can create a local copy of components (cells components with stroke styles and, if needed, cells components with different states), customize them, and use them in the project. The cell content can be set based on local components. 

Also, if you’re using the table for one large project with different kinds of tables, all the above-mentioned components are easily scaled. The table components can be improved to infinity and beyond, like creating the cell states when hovering and other kinds of interactions.

Questions, feedback, thoughts? Leave a comment below, and I’ll do my best to help you!

### Figma Table Mockup Download

As promised, I created a complete version of the Figma table mockup that you’re welcome to use for learning purposes or anything else you like. Enjoy!

{{< rimg breakout="true" href="https://www.figma.com/file/PDmebscR4YRI42oMVjolz7j6/Table-(Article)?node-id=0%3A1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d08b37a-9f74-4ec9-9cd9-acfdc924a4e8/tables-in-figma-mockup.png" sizes="100vw" caption="Here’s a <a href='https://www.figma.com/file/PDmebscR4YRI42oMVjolz7j6/Table-(Article)?node-id=0%3A1'>Figma table mockup</a> that you can use for learning purposes &mdash; let the creativity begin!" alt="Tables in Figma mockup design" >}}

### Related Reading

- “[Atomic Design](https://atomicdesign.bradfrost.com/table-of-contents/),” Brad Frost
- “[How To Architect A Complex Web Table](https://www.smashingmagazine.com/2019/02/complex-web-tables/),” Slava Shestopalov, Smashing Magazine
- “[Creating Atomic Components In Figma](link),” Design & Engineering team, littleBits
- “[Figma Tables: Data Grid Design By A Single Cell-Component](https://setproduct.com/blog/figma-tables-data-grid-design),” Roman Kamushken, Setproduct

### Useful Resources

- [Figma YouTube Channel](https://www.youtube.com/channel/UCQsVmhSa4X-G3lHlUtejzLA/videos)  
*The official Figma channel on YouTube &mdash; it’s the first thing to watch if you are new to Figma.*
- [Google Sheets Sync](https://www.figma.com/c/plugin/735770583268406934/Google-Sheets-Sync)  
*A Figma plugin that helps you get data from Google Sheets into your Figma file. This should work fine with the techniques from this tutoria, but you’ll need to invest some time into renaming all the text layers for this to work properly.*

{{< signature "mb, yk, il" >}}

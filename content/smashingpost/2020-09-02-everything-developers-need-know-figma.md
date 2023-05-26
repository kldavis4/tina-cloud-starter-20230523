---
title: 'Everything Developers Need To Know About Figma'
slug: figma-developers-guide
author: jurn-van-wissen
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bdb95ed-a19e-4c9e-a619-06d040d59396/figma-developers-guide.png
date: 2020-09-02T11:00:00.000Z
summary: >-
  Figma is a design tool that is rapidly gaining popularity and becoming more common in companies around the world. Unlike most design software, Figma is free and browser-based so developers can easily access the full design files making the developer handoff process significantly smoother. This article teaches developers who have nothing but a basic understanding of design tools everything they need to know to work with Figma.
description: >-
  Unlike most design software, Figma is free and browser-based so developers can easily access the full design files making the developer handoff process significantly smoother. This article explains everything they need to know to work with Figma.
categories:
  - Design
  - Tools
  - Workflow
  - Figma
  - Guides
---

If you aren’t using it yet the name Figma is surely a name that you’ve heard more and more over the last few years. 

Figma is a relatively new design tool that is browser-based. This means you don’t need to install it locally or buy expensive licenses to give team members access to design files. This has made design more accessible than ever and that’s why many developers now find themselves needing to learn how to work with design tools.

Since many developers don’t have a lot of experience playing around in design tools we’ll cover all the basics developers need to know about so you can confidently navigate around Figma and extract any information you might need when working with the designs sent to you by a designer.

I’ll also cover some specific Figma features that make it easier for developers such as providing CSS information about elements used within the design.

### A Quick Note About Shortcuts

Most shortcuts are written for both Windows and Mac, where the <kbd>Ctrl</kbd> key on Windows corresponds to the <kbd>Cmd</kbd> key on the Mac, and <kbd>Alt</kbd> is used for both <kbd>Alt</kbd> (Windows) and <kbd>Option/Alt</kbd> (Mac).

For example, <kbd>Ctrl/Cmd + Alt + C</kbd> is <kbd>Ctrl + Alt + C</kbd> on Windows and <kbd>Cmd + Alt/Option + C</kbd> on the Mac.

## Developer Handoff

To understand the hype around Figma and why you suddenly find yourself needing to learn how design tools work as a developer, it’s helpful to look back on the developer handoff process before Figma was around as it has changed significantly.

Design teams used to send an email to the development team with dozens of attachments containing static images of the design, exported assets, and even word documents with the page copy. Developers usually didn’t have access to the full design files as licenses for design software were expensive and not strictly necessary. Communication and feedback were scattered across email, project management tools, and meeting notes. Everyone was struggling with keeping track of changes to the design; every time the design was updated, it needed to be sent to everyone involved &mdash; yet again.

As design tools modernized, this process got more streamlined. Designers would often use separate tools like Zeplin or Invision to handoff the designs to developers. Developers now had better access to the designs and had more tools available to extract information about typography, colors, and measurements. Although it was easier to find the latest version of a design for everyone, designers needed to work in separate tools and keep them in sync. A big improvement but still not perfect.

Figma is a design tool that is rapidly gaining in popularity and shakes up the design handoff process once again. Figma is browser-based so everyone can use it regardless of their operating system and without installing anything. It’s also completely cloud-based so everyone is always looking at the latest version of the design and has built-in collaboration tools making collaborating and communicating easier than ever. 

If you want to follow along with this article (or just play around with Figma), I’ll be using this file to explain everything in this tutorial:

- [Figma startup landing page dark](https://www.figma.com/community/file/827488004796756851) (download)

{{% feature-panel %}}

## The Basics

When you are added as a collaborator on a Figma design you can choose to open it in the browser or you can [download the desktop app](https://www.figma.com/downloads/) (available on Windows and macOS). The desktop app is not a native app but a cross-platform electron app like Slack and Visual Studio Code. The functionality of the browser and desktop versions is largely the same. The desktop app does have built-in support for using local fonts whereas the browser version requires installing the Figma Font Helper before you can use local fonts.

Figma’s interface is split into three major parts. In the middle, you’ll find a big canvas where all the designs are located. On the left side, there is a sidebar that contains the layers, assets, and pages of a file. The right toolbar contains all information about elements in the file.

A file can have multiple pages and every page has one canvas. Designers often use pages to separate and organize different parts of the file with separate pages for the design system, icons, or other file assets.

When opening up a new file for the first time, make sure to familiarize yourself with the different pages within the file. If the designer you are working with has made a separate page for all colors, typography, and icons it can save you time while building out the design.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc464a52-92e4-4e3d-a224-0c5f9f8626fc/figma-interface.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc464a52-92e4-4e3d-a224-0c5f9f8626fc/figma-interface.png" sizes="100vw" caption="Figma’s interface. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc464a52-92e4-4e3d-a224-0c5f9f8626fc/figma-interface.png'>Large preview</a>)" alt="Interface of Figma" >}}

## Navigating Figma

Before we get to the good stuff, it’s important that you can quickly navigate around in Figma so you can work more efficiently.

When you open a file you’ll start on the largest zoom level that fits all the frames in the visible area.

- You can zoom in or out by holding <kbd>Cmd ⌘</kbd> and scrolling up/down or by pressing the <kbd>+</kbd> and <kbd>-</kbd> keys.
- If you want to scroll horizontally on the canvas you hold the spacebar and drag with your mouse.
- You can zoom in quickly on a single frame or element by selecting it and pressing <kbd>Shift</kbd> + <kbd>2</kbd>.
- Quickly return to where all elements fit in the canvas by pressing <kbd>Shift</kbd> + <kbd>1</kbd>.

Don’t worry too much about remembering these shortcuts for now, just know that they are available and you can always view these and other available shortcuts by pressing <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>?</kbd>.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e91b57b7-dadf-4f5e-8cce-fdadd634a357/shortcuts-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e91b57b7-dadf-4f5e-8cce-fdadd634a357/shortcuts-figma.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e91b57b7-dadf-4f5e-8cce-fdadd634a357/shortcuts-figma.png'>Large preview</a>)" alt="available shortcuts in Figma" >}}

Once you have used a shortcut it will be colored blue so you can easily see which ones you still need to learn.

## Project Styles

When you’re opening a brand new project it’s helpful to set up all the basic styles first. Figma displays all the project styles in the right sidebar. Here you can easily find all the typography, colors, grids, and other styles used in the design.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/622087b6-9284-45c6-9fba-23488aad9c61/project-styles-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/622087b6-9284-45c6-9fba-23488aad9c61/project-styles-figma.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/622087b6-9284-45c6-9fba-23488aad9c61/project-styles-figma.png'>Large preview</a>)" alt="" >}}

Note that the project styles will only display if no element is selected. If you want to cancel your selection and view the project styles, simply click somewhere in the canvas or use the <kbd>Esc</kbd> key.

You can use this information to set up your layout, variables, and fonts in CSS. Simply click on the edit icon next to the style element to view all information about that style.

{{< vimeo id="450489725" caption="View and edit project styles." breakout="true" >}}

{{% ad-panel-leaderboard %}}

## Selecting Elements

Once you’ve set up the basics for your project it’s time to dive into the design. The most important thing in deconstructing a design is selecting elements and getting information about dimensions and styles from it.

Selecting a layer isn’t as simple as clicking on an element as most designs have multiple levels of nesting for elements. Clicking an element only selects the top-level element.

To select a specific layer you need to hold Command `⌘` while clicking or you can right-click an element to open a menu of all the nested layers and select the correct one.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4eee538-f084-42b5-83e8-4a4d6dbe13ce/select-layer-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4eee538-f084-42b5-83e8-4a4d6dbe13ce/select-layer-figma.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4eee538-f084-42b5-83e8-4a4d6dbe13ce/select-layer-figma.png'>Large preview</a>)" alt="Secondary menu to select a layer" >}}

If you double click an element, it will select one nesting level lower every time you double click. This is a great way to drill down into an element until you get to the desired selection.

*There are many more ways to select and navigate layers, this article just covers the basics that are used 80% of the time. Figma’s documentation teaches more ways [to select and navigate layers](https://help.figma.com/hc/en-us/articles/360040449873-Select-layers-and-objects).*

Once you select an element, you can click the **Code** tab in the right sidebar to display all the CSS information about that element.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1feae473-0c3c-42d4-abdf-a5a3b795588c/code-tab-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1feae473-0c3c-42d4-abdf-a5a3b795588c/code-tab-figma.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1feae473-0c3c-42d4-abdf-a5a3b795588c/code-tab-figma.png'>Large preview</a>)" alt="code tab showing CSS properties of selected element" >}}

It’s important to note that the CSS is automatically generated and is not perfect, especially for positioning elements. Don’t copy all CSS 1-to-1 to your project but instead use it as a guide and a quick way to get information about elements.

## Dimensions And Measuring

Whenever you want to measure spaces between elements, correctly position elements, or even set the right margin or padding, all you need to do is select the element that you want to measure from, then hold the <kbd>Alt</kbd> and hover your mouse over the element you’d like to measure the distance to.

{{< vimeo id="450492777" caption="Measuring distance between elements." breakout="true" >}}

Figma will mark the distance between elements with a red line and show the distance in pixels. If you want to measure the distance to a specific child element in another group or frame, you can hold the <kbd>Cmd ⌘</kbd> key just like you would when selecting an element to deep select it.

## Exporting Assets

In the past, designers would often be responsible for exporting all assets as most developers didn’t have design software installed on their system. In Figma, you now have full access to the designs and can export everything yourself.

### Prepare for Export

The first thing you need to do if you want to export an asset is that you have to mark it as exportable. You do this by selecting the element you want to export and clicking the plus icon in the right sidebar next to the **Export** heading.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c85f177-b4bf-4126-a6da-ecc64c30cd81/export-settings-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c85f177-b4bf-4126-a6da-ecc64c30cd81/export-settings-figma.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c85f177-b4bf-4126-a6da-ecc64c30cd81/export-settings-figma.png'>Large preview</a>)" alt="Setting export settings for selected layer" >}}

Depending on what type of file you are exporting there will be different export settings you can tweak. Images only have a scale multiplier and you can choose the file type (PNG, JPG, SVG or PDF). Figma will use the name of the layer as the file name but you can add a file name suffix. You can then export the selected element using the export button.

**Quick tip:** *You can also quickly export an asset by right-clicking it, hovering on Copy/paste and copying the image or SVG code. This is useful if you don’t need to have custom export settings and just need a quick copy of a single element.*

### Export all Assets

You can export each individual asset by selecting it and clicking the export button but you can also export all assets that are exportable at once.

If you want to export all the assets from the design in one go you can go to the main menu, and click **Export..** under the File menu. You can also use the keyboard shortcut <kbd>Shift</kbd> + <kbd>Cmd</kbd> + <kbd>E</kbd> on MacOS or <kbd>Shift</kbd> + <kbd>Ctrl</kbd> + <kbd>E</kbd> on Windows.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c56b4370-cfd0-4cf6-b000-308dc25bf018/export-all-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c56b4370-cfd0-4cf6-b000-308dc25bf018/export-all-figma.png" sizes="70vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c56b4370-cfd0-4cf6-b000-308dc25bf018/export-all-figma.png'>Large preview</a>)" alt="Setting export settings for selected layer" >}}

This will display a list of all the items in the file that are marked for export. You can then inspect the dimensions, file type and exclude any files before making the final export. If you hover over the thumbnail of the assets it will display the file name that the asset will have when it’s exported.

If you need to make adjustments, clicking on the thumbnail of an asset will select that element in the canvas where you can easily adjust the export settings.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e98d12f0-6a0f-48a8-b620-f74a61a24528/export-all-assets-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e98d12f0-6a0f-48a8-b620-f74a61a24528/export-all-assets-figma.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e98d12f0-6a0f-48a8-b620-f74a61a24528/export-all-assets-figma.png'>Large preview</a>)" alt="List of all exportable assets" >}}

If you have a lot of exportable assets in a single file, you can use a slash “/” in your layer name to mark it as a group of assets. Figma will then automatically create a folder for that group and export the assets within that group to the subfolder.

{{% ad-panel-leaderboard %}}

## User Flow And Animations

Figma also supports a [variety of animations](https://blog.jurn.io/figma-animation-examples/) for transition between states or pages, for opening modals or menus, for dragging and swiping actions on mobile and much more. You can preview these animations by clicking the play icon in the top right to open Presentation view.

To view the information about an animation, select the **Prototype** tab in the right sidebar and you’ll see the user flow displayed in blue arrows in the canvas. 

Clicking on the arrow shows you all the information about that specific animation. Each animation consists of a trigger, an action, and a transition.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/063a4696-1b9a-4cbb-8915-19024c627968/animation-tab-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/063a4696-1b9a-4cbb-8915-19024c627968/animation-tab-figma.png" sizes="100vw" caption="A simple hamburger menu animation (Source: <a href='https://www.figma.com/community/file/866532393298219995'>figma.com</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/063a4696-1b9a-4cbb-8915-19024c627968/animation-tab-figma.png'>Large preview</a>)" alt="Animation settings tab" >}}

This simple animation opens a hamburger menu. You can see that the hamburger icon has an **On Tap** trigger, once it is triggered it will **Navigate To** the screen where the mobile menu is in an opened state. The transition type is a **Smart Animate** transition which means Figma automatically interpolates between these two states. It does this using an **Ease Out** animation function with a duration of **300ms**.

This information is necessary to exactly replicate the animations in CSS but unlike all other element information, animations can not be found in the Code tab!

## Communication

If anything isn’t clear and you’d like to ask someone else on the project for clarification. All you have to do is click on the chat bubble icon in the top toolbar or hit the <kbd>C</kbd> key to switch to the Comment tool.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad26699d-eb3a-4d00-8ec3-61a58bd259af/comment-tool-figma.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad26699d-eb3a-4d00-8ec3-61a58bd259af/comment-tool-figma.png" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad26699d-eb3a-4d00-8ec3-61a58bd259af/comment-tool-figma.png'>Large preview</a>)" alt="Figma toolbar with comment tool highlighted" >}}

You can now click anywhere in the design and start typing a comment or question about that element. Once you’ve finished writing your comment, you can use the <kbd>V</kbd> key to return to the normal cursor.

Note that not everyone will automatically receive a notification that you left a comment. If you want to be sure someone sees your comment you should mention them using the @ symbol just like on Slack or Twitter.

Every comment is visible to everyone who has access to the design as there are no private comments/chats. Once the issue has been resolved it can be marked as such and the comment will gray out.

## Conclusion

We’ve covered a lot of ground so far in Figma and you should be able to navigate around and extract all the information you need from any Figma design file sent your way. Getting information about typography and colors, measuring margins, padding and position of elements, exporting assets and collaborating with other team members.

If you want to learn more about the tool, [Figma’s documentation](https://help.figma.com/hc/en-us) is a great place to start or search when you want to learn more about a specific feature.

{{< signature "ra, yk, il" >}}

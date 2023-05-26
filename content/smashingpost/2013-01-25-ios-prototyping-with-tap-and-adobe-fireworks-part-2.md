---
title: iOS Prototyping With TAP And Adobe Fireworks (Part 2)
slug: ios-prototyping-with-tap-and-adobe-fireworks-part-2
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/562f96e3-cbe2-436d-b2dd-9e3d00d6905b/fireworks-logo2.jpg
date: 2013-01-25T11:01:47.000Z
author: shlomo-goltz
summary: >-
  In the <a href="https://www.smashingmagazine.com/2013/01/11/ios-prototyping-adobe-fireworks-tap-part1/">previous article</a> in this series, Shlomo Goltz looked in detail at the four major stages that all of the projects at Cooper go through, as well as the approach to Fireworks PNG organization, and the main components of Fireworks (pages, shared layers, symbols and styles).
description: >-
  After following the steps in <a href="https://www.smashingmagazine.com/2013/01/11/ios-prototyping-adobe-fireworks-tap-part1/">Part 1</a>, we now have everything to start building the prototype. But first, Shlomo explains how to create a “live” iOS prototype.
categories:
  - Fireworks
  - Tutorials
  - Prototyping
  - iOS
---
After following the steps in <a href="https://www.smashingmagazine.com/2013/01/11/ios-prototyping-adobe-fireworks-tap-part1/">Part 1</a>, we now have everything to start building the prototype. But first, allow me try to sum it up quickly: to create a “live” iOS prototype, you only need to perform the following six steps:

1.  **Design** each page in Fireworks (each page representing one step of a walkthrough of the user’s actions).
2.  **Add hotspots** over the page to create buttons.
3.  **Customize** each hotspot:
    *   Which page will the hotspot link to?
    *   Which gesture will initiate the hotspot link?
    *   Which transition will animate once the correct gesture is used?
4.  **Export** your design as a prototype, and upload it to your server.
5.  **Download** [Touch Application Prototypes](https://unitid.nl/2011/03/touch-application-prototypes-tap-for-iphone-and-ipad-using-adobe-fireworks/) (TAP), a free Fireworks extension for prototyping on the iPhone and iPad.
6.  **Convert** (with the help of TAP) the exported prototype to an animated, gesture-based prototype that you can use on an iOS device.

We’ll cover steps one to three in this tutorial. Steps four through six (exporting the prototype from Fireworks and converting to an iOS prototype with TAP) will be covered in [part 3](https://www.smashingmagazine.com/2013/02/ios-prototyping-adobe-fireworks-tap-part3/) of this series.

So, where do we begin? We have already covered pages, shared layers, symbols and styles &mdash; a few of the major building blocks of our design in Fireworks. But now we need interactivity!

## The Basics Of Interactive Prototyping In Fireworks

We’ll assume you know the basics of designing pages, adding hotspots and linking pages, so we won’t cover them here in detail. The rest of the article focuses on how to use TAP together with Fireworks to take your wireframes to the next level.

If you need basic information about Fireworks before moving on to the rest of this article, please check out the following resources:

*   “[Understanding Fireworks](https://tv.adobe.com/watch/learn-fireworks-cs4/getting-started-01-understanding-fireworks/),” Jim Babbage, Adobe TV This video tutorial has general information about Adobe Fireworks.
*   “[Fireworks for Beginners](https://medialoot.com/blog/fireworks-for-beginners/ "Quick Overview of Unique and Useful Features in Fireworks"),” MediaLoot This tutorial provides a quick overview of the unique and useful features in Fireworks.
*   “[How to Create and Link Image Maps in Fireworks](https://www.dummies.com/how-to/content/how-to-create-and-link-image-maps-in-fireworks-cs5.html),” For Dummies This quick tutorial shows how to create hotspots in image maps.

Also, these two detailed articles, published recently on Smashing Magazine, will help you get started with interactive prototyping in Fireworks:

*   “[Create Interactive Prototypes With Adobe Fireworks](https://www.smashingmagazine.com/2012/06/25/create-interactive-prototypes-with-adobe-fireworks/),” André Reinegger
*   “[Interactive Prototypes and Time-Savers With Adobe Fireworks](https://www.smashingmagazine.com/2012/07/03/interactive-prototypes-timesavers-adobe-fireworks/),” Trevor Kay

{{% feature-panel %}}

## TAP: Customizing Hotspots And Using Gestures, Transitions And Timers

TAP allows you to specify whether the interactions in a prototype will be <strong>taps</strong> or <strong>gestures</strong>. The following gestures are supported:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24280664-8e3a-4867-a629-c0a297894055/gestures-list.png" alt="List of gestures supported by TAP." width="500" /><br>
<em><a href="https://unitid.nl/tap/TAP_cheatsheet_0046.pdf">List of gestures supported by TAP</a> (PDF)</em>

Once the user has interacted with a prototype by tapping or gesturing, you can specify which <strong>transition</strong> will be used to change the interface. The following transitions are supported:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2064836c-73eb-4e39-ab0b-645d4d5aa93e/transitions-list.png" alt="List of transitions supported by TAP." width="500" /><br>
<em><a href="https://unitid.nl/tap/TAP_cheatsheet_0046.pdf">List of transitions supported by TAP</a> (PDF)</em>

Although TAP supports transitions for both taps and gestures, we will use slightly different methods to define the interactions for each. We will place hotspots over the design and then assign interactions in the Properties panel.

Because a tap is the simplest interaction, a hotspot for a tap may have only one transition and one destination. However, a hotspot for a gesture may respond to multiple gestures and have multiple transitions and destinations.

### Customizing Hotspots for Taps

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f026ad0f-203b-4a99-a6eb-090f65f5def2/iconhotspot.png" alt="Hotspot icon" width="84" height="100" />

When setting up your Fireworks PNG file for use with TAP, keep in mind that you will be using the “Link,” “Alt” and “Target” fields <strong>differently</strong> than when you are using Fireworks on its own. Be sure to fill in the correct fields with the syntax required by the TAP extension. Also, the way you enter the properties into the “Link,” “Alt” and “Target” fields will vary depending on whether you are using a gesture or a tap (we’ll explain this in detail further below).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/868f85a7-397c-4df6-9059-74e2cc786c02/hotspot-showcase.png" alt="A hotspot in Fireworks" width="500" height="486" /><br>
<em>Hotspots are represented on the canvas as a translucent blue shape with crosshairs in the center. Hotspots exist on their own special Web layer, separate from the rest of the elements on the canvas.</em>

Each hotspot has three fields that can be customized in the Properties panel: “Link,” “Alt” and “Target.” Each property is used by TAP in the following ways when a tap (rather then a gesture) is made:

*   **Link**  
Link to another page (remember that links are case-sensitive!).
*   **Alt**  
The transition will animate in between pages.
*   **Target**  
This is a timeout, used to transition to another page after a set amount of time has passed. (This is a great feature for loading screens or step-by-step animations.)

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fbeeb03-0fd7-4c2d-bf7e-1ce2c446acf0/hotspotpropertypanel-tapformat.png" alt="Hotspot Property Panel - format for tap" width="500" height="183" /><br>
<em>Notice how the Properties panel changes when a hotspot is selected. The “Link,” “Alt” and “Target” fields are used by TAP as “Link,” “Transition” and “Timeout” fields.</em>

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7254d0ee-3510-4e45-a929-08f9a1f741b8/propertiesbarfilledoutexample1.png" alt="Properties panel (hotspot is selected) - filled out example" width="500" height="199" /><br>
<em>Here is the Properties panel again when a hotspot is selected, now with an example filled out; in this case, a tap that initiates a fade to another page.</em>

### Customizing Hotspots for Gestures

Four gestures are supported by TAP:

1.  Swipe left,
2.  Swipe right,
3.  Swipe up,
4.  Swipe down.

<strong>Note</strong>: Tapping (which is technically a fifth gesture) is also supported, and it is the default if no gesture is explicitly declared.

Gestures work only when there are hotspots, so the first step is to create a hotspot. If you swipe outside of a hotspot area, nothing will happen. However, if you create a hotspot that takes up the entire page, then the swipe will work <em>everywhere</em> on the page.

Each property is used by TAP in the following ways when a gesture (rather then a tap) is made:

*   **Link**.  The link field must contain a hash sign (#).
*   **Alt**.  When gestures are used, this field will be blank.
*   **Target**.  The gesture, the page linked to and the transition are all defined here when a gesture is used.

For hotspots that use a gesture, you do not specify which page the hotspot will link to in the “Link” field (the page linked to is defined in the “Target” field, as described below); rather, you would add a <code>#</code> (hash sign). The hash sign allows for a JavaScript call, which makes the gesture recognition work properly. Decide which gesture you will use, and then enter the programming code needed into the “Target” field. The amount of coding you need to know is minimal, and even with no experience, memorizing and mastering all of the options takes minutes.

{{% ad-panel-leaderboard %}}

You can also use a <a href="https://unitid.nl/tap/TAP_cheatsheet_0046.pdf">TAP cheat sheet</a> (PDF), which applies to TAP version 0.46 and later.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91c3e92b-c17e-4e15-89ba-9d81d269ca81/hotspotpropertypanel-gestureformat.png" alt="Properties panel (hotspot is selected) - format for gestures" width="500" height="179" /><br>
<em>The way the Properties panel is used is different when gestures are used than when only a tap is used. The “Link” and “Target” fields take on different functionality.</em>

The format for writing the statement is a combination of three phrases, separated by commas:

1.  Type of gesture,
2.  Page to link to,
3.  Transition type.

For example, the statement <code>swipeleft, page2, slideleft</code> actually says the following: “If you <em>swipe</em> this area with your finger from right to left, then <em>page 2</em> will appear with a <em>slide-left</em> transition.”

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c42cdfc-0d3c-4337-baac-752d48c551eb/hotspotpropertypanel-gestureexample1.png" alt="Properties panel (hotspot is selected) - gestures example" width="500" height="300" /><br>
<em>The Properties panel (with a hotspot selected); a filled-out TAP example.</em>

To also enable swiping in another direction, simply continue adding the three parameters to the “Target” field. (Remember that, according to TAP’s syntax, a “statement” is made up of a three-phrase group.)

The following code has three statements (each composed of three phrases, for a total of nine phrases in this declaration): <code>swipeleft,page2,slideleft, swiperight,page0,slideright, swipeup,page3,pushup</code>. With these commands, the user can <em>swipe left</em>, <em>swipe right</em> and <em>swipe up</em>, finding <em>page 2</em>, <em>page 0</em> and <em>page 3</em>, respectively.

### Transitions

Sixteen transitions are supported by TAP, falling into the following categories: slide, push, pop, fade, flip, swap and cube.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68e06e47-f73c-43ed-8fd4-35a61baaaec4/transitiontaxonomymatrix.png" alt="All the transitions available in TAP" width="500" height="358" /><br>
<em>All animations are CSS3 transitions supported natively by WebKit. (The Safari and Chrome browsers are both based on the WebKit engine.)</em>

To add a transition, select the hotspot you want to add a transition to. In the Property Inspector (PI) panel, enter the transition type in the “Alt” field. The proper syntax can be found in the <a href="https://unitid.nl/2011/03/touch-application-prototypes-tap-for-iphone-and-ipad-using-adobe-fireworks/">official TAP documentation</a>. If you have a bit of CSS3 knowledge, you can easily add your own transitions.

### Timers

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ea48223-b830-488d-bf21-a71f566a9de5/icontimers.png" alt="Timers icon" width="84" height="100" />

Sometimes you want to load a new page without the user having to interact at all. For example, you might want to show a loading screen that automatically goes to the start page of the application after a set amount of time.

To create a timed transition, draw a hotspot on the page that will be displayed for a limited amount of time. It is not really important where you place this hotspot, because it will be triggered automatically when the specified amount of time has passed.

In the “Target” field of your hotspot (where gestures are also handled), enter <code>timeout=</code>. The time of the delay before switching to another page is entered to the right of the <code>=</code> sign. Time is measured in milliseconds, so <code>timeout=500</code> is equal to half a second. Experiment with the number to get the result you are looking for. If desired, add a transition to the “Alt” field.

<strong>Note:</strong> If you don’t put a transition in the field, the default of “fast fade” will be used by TAP.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c10c345d-4ef5-469e-a77a-e66130eb5ebe/hotspotpropertypanel-timeoutexample.png" alt="Hotspot Property Panel Example - Timeout" width="500" height="190" /><br>
<em>The Properties panel with a hotspot selected and an example filled out: a 500-millisecond delay that initiates a fade to another page.</em>

### Change in Orientation

You can display a different page when the device detects a change in orientation, from landscape to portrait or vice versa. Providing a layout for each orientation will make your prototype feel more like a real app and will allow for more versatile usage.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81c6cb58-b22f-46fc-b8a2-2342b1f70d3f/ipadrotation1.png" alt="iPad Rotation - TAP supports both landscape and portrait orientations" width="500" height="320" /><br>
<em>TAP supports both landscape and portrait orientations through two versions with similar names. The landscape version is followed by an underscore and lowercase “L” (<code>&#95;l</code>).</em>

For TAP to be able to identify which screen design to use when the orientation changes, you must have two screens with similar names. You can name the portrait design anything you want (although it is recommended that you follow HTML naming conventions &mdash; that is, no spaces &mdash; so that your pages render properly when exported), and the corresponding landscape page must have the same name followed by an <code>&#95;l</code>. So, you would create a portrait page in Fireworks and name it, for example, <code>Page1</code>. Then, you would create another page, this one in landscape. Make sure the canvas is landscape-sized (you don’t need to design everything rotated by 90°), and name this page <code>Page1&#95;l</code>. The <code>&#95;l</code> extension is enough to trigger the prototype to switch between the portrait and landscape versions.

{{% ad-panel-leaderboard %}}

## Building An iOS Prototype With Adobe Fireworks And TAP

Now it’s time to put all of that theory into practice by creating an interactive iOS prototype.

### Tutorial Exercise Files

To help you with this tutorial, I have prepared three exercise files:

1.  [`CookbookBlank.fw_.png`](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56ac418c-e489-4716-a54d-ae7b9e353c73/cookbookblank.fw_)
2.  [`CookbookFinished.fw_.png`](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fc61a4a-c945-404e-8fb1-5a2ceb0fef42/cookbookfinished.fw_)
3.  [`CookbookPackage.zip`](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93857c3b-fa09-4069-8af6-5ba8a5cc1fc6/cookbookpackage.zip)

<strong>Note:</strong> A <a href="https://stackoverflow.com/questions/9302823/use-a-adobe-fireworks-file-extension-other-than-png-for-multi-layer-master-file">common convention</a> among designers is to add an <code>.fw</code> before the <code>.png</code> file extension, in order to easily differentiate between Fireworks editable PNG files and flattened (exported) PNG files. For some reason, Smashing Magazine’s uploader adds an underscore to the file extension, so the files linked to above were originally named <code>CookbookBlank.fw.png</code> and <code>CookbookFinished.fw.png</code>.

*   You’ll use `CookbookBlank.fw.png` to follow along with this tutorial.
*   `CookbookFinished.fw.png` is the completed version of the file that you would get by following this tutorial closely. Use this file if you get stuck, to check your progress, or if you want to jump ahead and see how everything works together in Fireworks.
*   The `CookbookPackage.zip` is a ZIP archive containing the exported designs and the TAP framework. You can quickly upload the folder (after unzipping it, of course) and see the working prototype on any server.

### Getting Acquainted With The Fireworks PNG File

Open the file <code>CookbookBlank.fw.png</code>. Note that six <strong>pages</strong> and one <strong>master page</strong> are in it (you can see them in the Pages panel in Fireworks). All page names are HTML-compliant (no special characters, no spaces), and the first page is named <code>index</code>, just like on a normal website.

## Creating And Customizing Hotspots

### Master Page

The master page in our exercise file is named <code>title-bar</code>, and it appears above all other pages in the Pages panel. Any objects on this page will appear on all the other pages. We want to create a universal link to the start page on the master page so that it can be produced only once and appear in the rest of the design automatically. When the user taps on the “Home” button, whatever is being displayed on the screen will slide down to reveal the start page.

1.  Create a hotspot covering the “Home” button:
    1.  Select the Rectangle Hotspot tool (found in the Tools panel, or press `J`). [![Rectangle Hotspot tool](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8add76be-0d7b-467f-a71a-d5c2a252f4ec/1-toolbar11-e1336442946966-150x75.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83d3e158-003d-49dd-99aa-6567a1e1e3f6/1-toolbar11.png "Rectangle Hotspot tool (view large)")
    2.  Click in the upper-left corner of the “Home” button and drag to the lower-right corner. A hotspot will be created.
2.  Customize the “Home” hotspot in the Properties panel:
    1.  Select the hotspot you have just created, and in the Properties panel select `start.html` in the “Link” drop-down menu.
    2.  In the “Alt” field, type `slidedown`.

<a title="The previous steps should result in a hotspot and hotspot properties as seen in this screenshot (view large)." href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff682622-b28f-4517-8508-a302b5ef3960/3-masterpage1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63a163f4-92ca-4b10-a402-e95bf599401e/3-masterpage1.500" alt="Master page" width="500" height="436" /></a><br>
<em>The preceding steps should result in a hotspot and the hotspot properties seen in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff682622-b28f-4517-8508-a302b5ef3960/3-masterpage1.png">Larger version</a>)</em>

### Page 1: The Loading Screen

The first page of our iOS prototype represents the loading screen.

Typically, a loading screen appears upon the launch of an app and stays for a couple seconds until the app loads. We’ll duplicate this functionality by creating a hotspot with a timeout (or timer) function.

1.  Select the first page (named `index`) in the Pages panel.
2.  Create a hotspot that covers the whole screen.
3.  Customize the hotspot in the Properties panel so that it automatically goes to the next page after a three-second delay:
    1.  Choose which page the hotspot will link to: in the “Link” drop-down menu, select `start.htm`.
    2.  Set up the timer: in the “Target” field, enter `timeout=3000` (which is in milliseconds and equal to 3 seconds).

<a title="The previous steps should result in a hotspot and hotspot properties as seen in this screenshot (view large)." href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fd0409a-a790-4b82-83aa-fd03d6b8134d/4-indextimer1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f6f140f-6a33-4f51-9868-220e21929a09/4-indextimer1.500" alt="Index page" width="500" height="437" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fd0409a-a790-4b82-83aa-fd03d6b8134d/4-indextimer1.png">Larger version</a>).</em>

### Page 2: The Start Screen

The start screen has a carousel in the middle of the page and three buttons at the bottom. To simplify some of the steps in this tutorial, we will make only the “All recipes” button functional:

1.  Select the second page (named `start`) in the Pages panel.
2.  Create a hotspot over the “All Recipes” button:
    *   Choose which page the hotspot will link to in the Properties panel: in the “Link” drop-down menu, select `all-recipes.htm`.
3.  Set up the transition to the next page: in the “Alt” field, type `slideup`.

<a title="The previous steps should result in a hotspot and hotspot properties as seen in this screenshot (view large)." href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89aae439-73ce-4e37-8f81-27cd2d9e670f/5-allrecipes1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1abbbdfd-c1df-4cad-9444-70ab36fc6942/5-allrecipes1.500" alt="All Recipes hotspot" width="500" height="439" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89aae439-73ce-4e37-8f81-27cd2d9e670f/5-allrecipes1.png">Larger version</a>).</em>

### Page 3: Recipe Selection Screen

We will now create a swipeable region at the top of the screen that (in addition to the “Home” button we’ve already created) allows the user to <strong>go back to the start page</strong>. While this functionality is not necessary, it gives the user another way to navigate the app, and it will teach you how to create a swipe in your prototype:

1.  In the Pages panel, select the third page, `all-recipes`.
2.  Create a hotspot that covers the entire width of the screen and the horizontal band across the title “Recipes” (see the illustration below).
3.  Customize the hotspot in the Properties panel:
    *   Initiate the swipe function: in the “Link” field, type `#` (a hash sign).

When a swipe is set, the transition, swipe and link are defined in the “Target” field:

1.  In the “Target” field, type `swipeleft,start,cubeleft` (i.e. when you _swipe_ left, go to the _start_ page, using the _cubeleft_ transition).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13ef48eb-0f1e-4b09-9d68-9a6fcb60253a/6-swipeback1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac73512f-7c50-4f2c-a562-b6a2ff69fa4e/6-swipeback1.500" alt="Swipe Back hotspot" width="500" height="437" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13ef48eb-0f1e-4b09-9d68-9a6fcb60253a/6-swipeback1.png">Larger version</a>)</em>

Next, let’s enable the user to <strong>choose a particular recipe</strong>:

1.  Over the Salisbury steak (located in the middle of the second row from the top), draw a hotspot.
2.  Customize the hotspot in the Properties panel:
    1.  Choose which page the hotspot will link to: in the “Link” field, select `chosen-recipe-intro-card.htm`.
    2.  Choose the transition: type `fade`.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9805036-7f11-4cdd-b36e-ec13889d5fea/7-foodhotspot1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81c8fb10-dcce-4b2a-af6c-1ca33754652d/7-foodhotspot1.500" alt="The preceding steps should result in a hotspot and hotspot properties." width="500" height="438" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9805036-7f11-4cdd-b36e-ec13889d5fea/7-foodhotspot1.png">Larger version</a>)</em>

### Page 4: Recipe Info Card

In the Pages panel, select the page <code>chosen-recipe-intro-card</code>.

<strong>Note:</strong> The design of page four is similar to the design of page three, in that page four is simply a lightbox laid over page three. This was achieved by sharing the wireframe layer of page three to page four. Sharing layers in Fireworks is an efficient way to maintain consistency in a project. The benefit of sharing layers between pages is that, if the design of page three is changed, those changes will be automatically reflected on page four.

1.  Create a hotspot over the “Cook This Recipe” button.
2.  Customize the hotspot in the Properties panel:
    1.  Choose which page the hotspot links to: in the “Link” drop-down menu, select `chosen-recipe-full.htm`.
    2.  Choose the transition: in the “Alt” field, type `flipright`.[![Recipe info card page](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6be4669a-3e67-4770-9635-7b6890ca2288/8-lighbtoxcookbutton1.500)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60c8c192-a06a-4b14-83b5-9945aa99f1e7/8-lighbtoxcookbutton1.png) _The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. ([Larger version](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60c8c192-a06a-4b14-83b5-9945aa99f1e7/8-lighbtoxcookbutton1.png))_
3.  Allow the user to close the lightbox:
    1.  Create four hotspots that completely surround the lightbox (one above, one below, one to the right and one to the left), and with the same attributes (i.e. the “Link” is `all-recipes.htm`, and “Alt” is `fade`).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6483dc03-bba9-459e-9a4b-dfb890ff8e78/9-lightboxexit1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef2efeb7-47a2-4c56-a400-8d4b29b78a07/9-lightboxexit1.500" alt="Closing the lightbox (hotspots)" width="500" height="438" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6483dc03-bba9-459e-9a4b-dfb890ff8e78/9-lightboxexit1.png">Larger version</a>)</em>

### Page 5: Recipe Detail Page

### Transitions

Sixteen transitions are supported by TAP, falling into the following categories: slide, push, pop, fade, flip, swap and cube.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68e06e47-f73c-43ed-8fd4-35a61baaaec4/transitiontaxonomymatrix.png" alt="All the transitions available in TAP" width="500" height="358" /><br>
<em>All animations are CSS3 transitions supported natively by WebKit. (The Safari and Chrome browsers are both based on the WebKit engine.)</em>

To add a transition, select the hotspot you want to add a transition to. In the Property Inspector (PI) panel, enter the transition type in the “Alt” field. The proper syntax can be found in the <a href="https://unitid.nl/2011/03/touch-application-prototypes-tap-for-iphone-and-ipad-using-adobe-fireworks/">official TAP documentation</a>. If you have a bit of CSS3 knowledge, you can easily add your own transitions.

### Timers

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ea48223-b830-488d-bf21-a71f566a9de5/icontimers.png" alt="Timers icon" width="84" height="100" />

Sometimes you want to load a new page without the user having to interact at all. For example, you might want to show a loading screen that automatically goes to the start page of the application after a set amount of time.

To create a timed transition, draw a hotspot on the page that will be displayed for a limited amount of time. It is not really important where you place this hotspot, because it will be triggered automatically when the specified amount of time has passed.

In the “Target” field of your hotspot (where gestures are also handled), enter <code>timeout=</code>. The time of the delay before switching to another page is entered to the right of the <code>=</code> sign. Time is measured in milliseconds, so <code>timeout=500</code> is equal to half a second. Experiment with the number to get the result you are looking for. If desired, add a transition to the “Alt” field.

<strong>Note:</strong> If you don’t put a transition in the field, the default of “fast fade” will be used by TAP.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c10c345d-4ef5-469e-a77a-e66130eb5ebe/hotspotpropertypanel-timeoutexample.png" alt="Hotspot Property Panel Example - Timeout" width="500" height="190" /><br>
<em>The Properties panel with a hotspot selected and an example filled out: a 500-millisecond delay that initiates a fade to another page.</em>

### Change in Orientation

You can display a different page when the device detects a change in orientation, from landscape to portrait or vice versa. Providing a layout for each orientation will make your prototype feel more like a real app and will allow for more versatile usage.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81c6cb58-b22f-46fc-b8a2-2342b1f70d3f/ipadrotation1.png" alt="iPad Rotation - TAP supports both landscape and portrait orientations" width="500" height="320" /><br>
<em>TAP supports both landscape and portrait orientations through two versions with similar names. The landscape version is followed by an underscore and lowercase “L” (<code>&#95;l</code>).</em>

For TAP to be able to identify which screen design to use when the orientation changes, you must have two screens with similar names. You can name the portrait design anything you want (although it is recommended that you follow HTML naming conventions &mdash; that is, no spaces &mdash; so that your pages render properly when exported), and the corresponding landscape page must have the same name followed by an <code>&#95;l</code>. So, you would create a portrait page in Fireworks and name it, for example, <code>Page1</code>. Then, you would create another page, this one in landscape. Make sure the canvas is landscape-sized (you don’t need to design everything rotated by 90°), and name this page <code>Page1&#95;l</code>. The <code>&#95;l</code> extension is enough to trigger the prototype to switch between the portrait and landscape versions.

## Building An iOS Prototype With Adobe Fireworks And TAP

Now it’s time to put all of that theory into practice by creating an interactive iOS prototype.

### Tutorial Exercise Files

To help you with this tutorial, I have prepared three exercise files:

1.  [`CookbookBlank.fw_.png`](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56ac418c-e489-4716-a54d-ae7b9e353c73/cookbookblank.fw_)
2.  [`CookbookFinished.fw_.png`](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fc61a4a-c945-404e-8fb1-5a2ceb0fef42/cookbookfinished.fw_)
3.  [`CookbookPackage.zip`](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93857c3b-fa09-4069-8af6-5ba8a5cc1fc6/cookbookpackage.zip)

<strong>Note:</strong> A <a href="https://stackoverflow.com/questions/9302823/use-a-adobe-fireworks-file-extension-other-than-png-for-multi-layer-master-file">common convention</a> among designers is to add an <code>.fw</code> before the <code>.png</code> file extension, in order to easily differentiate between Fireworks editable PNG files and flattened (exported) PNG files. For some reason, Smashing Magazine’s uploader adds an underscore to the file extension, so the files linked to above were originally named <code>CookbookBlank.fw.png</code> and <code>CookbookFinished.fw.png</code>.

*   You’ll use `CookbookBlank.fw.png` to follow along with this tutorial.
*   `CookbookFinished.fw.png` is the completed version of the file that you would get by following this tutorial closely. Use this file if you get stuck, to check your progress, or if you want to jump ahead and see how everything works together in Fireworks.
*   The `CookbookPackage.zip` is a ZIP archive containing the exported designs and the TAP framework. You can quickly upload the folder (after unzipping it, of course) and see the working prototype on any server.

### Getting Acquainted With The Fireworks PNG File

Open the file <code>CookbookBlank.fw.png</code>. Note that six <strong>pages</strong> and one <strong>master page</strong> are in it (you can see them in the Pages panel in Fireworks). All page names are HTML-compliant (no special characters, no spaces), and the first page is named <code>index</code>, just like on a normal website.

## Creating And Customizing Hotspots

### Master Page

The master page in our exercise file is named <code>title-bar</code>, and it appears above all other pages in the Pages panel. Any objects on this page will appear on all the other pages. We want to create a universal link to the start page on the master page so that it can be produced only once and appear in the rest of the design automatically. When the user taps on the “Home” button, whatever is being displayed on the screen will slide down to reveal the start page.

1.  Create a hotspot covering the “Home” button:
    1.  Select the Rectangle Hotspot tool (found in the Tools panel, or press `J`). [![Rectangle Hotspot tool](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8add76be-0d7b-467f-a71a-d5c2a252f4ec/1-toolbar11-e1336442946966-150x75.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83d3e158-003d-49dd-99aa-6567a1e1e3f6/1-toolbar11.png "Rectangle Hotspot tool (view large)")
    2.  Click in the upper-left corner of the “Home” button and drag to the lower-right corner. A hotspot will be created.
2.  Customize the “Home” hotspot in the Properties panel:
    1.  Select the hotspot you have just created, and in the Properties panel select `start.html` in the “Link” drop-down menu.
    2.  In the “Alt” field, type `slidedown`.

<a title="The previous steps should result in a hotspot and hotspot properties as seen in this screenshot (view large)." href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff682622-b28f-4517-8508-a302b5ef3960/3-masterpage1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63a163f4-92ca-4b10-a402-e95bf599401e/3-masterpage1.500" alt="Master page" width="500" height="436" /></a><br>
<em>The preceding steps should result in a hotspot and the hotspot properties seen in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff682622-b28f-4517-8508-a302b5ef3960/3-masterpage1.png">Larger version</a>)</em>

### Page 1: The Loading Screen

The first page of our iOS prototype represents the loading screen.

Typically, a loading screen appears upon the launch of an app and stays for a couple seconds until the app loads. We’ll duplicate this functionality by creating a hotspot with a timeout (or timer) function.

1.  Select the first page (named `index`) in the Pages panel.
2.  Create a hotspot that covers the whole screen.
3.  Customize the hotspot in the Properties panel so that it automatically goes to the next page after a three-second delay:
    1.  Choose which page the hotspot will link to: in the “Link” drop-down menu, select `start.htm`.
    2.  Set up the timer: in the “Target” field, enter `timeout=3000` (which is in milliseconds and equal to 3 seconds).

<a title="The previous steps should result in a hotspot and hotspot properties as seen in this screenshot (view large)." href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fd0409a-a790-4b82-83aa-fd03d6b8134d/4-indextimer1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f6f140f-6a33-4f51-9868-220e21929a09/4-indextimer1.500" alt="Index page" width="500" height="437" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fd0409a-a790-4b82-83aa-fd03d6b8134d/4-indextimer1.png">Larger version</a>).</em>

### Page 2: The Start Screen

The start screen has a carousel in the middle of the page and three buttons at the bottom. To simplify some of the steps in this tutorial, we will make only the “All recipes” button functional:

1.  Select the second page (named `start`) in the Pages panel.
2.  Create a hotspot over the “All Recipes” button:
    *   Choose which page the hotspot will link to in the Properties panel: in the “Link” drop-down menu, select `all-recipes.htm`.
3.  Set up the transition to the next page: in the “Alt” field, type `slideup`.

<a title="The previous steps should result in a hotspot and hotspot properties as seen in this screenshot (view large)." href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89aae439-73ce-4e37-8f81-27cd2d9e670f/5-allrecipes1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1abbbdfd-c1df-4cad-9444-70ab36fc6942/5-allrecipes1.500" alt="All Recipes hotspot" width="500" height="439" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89aae439-73ce-4e37-8f81-27cd2d9e670f/5-allrecipes1.png">Larger version</a>).</em>

### Page 3: Recipe Selection Screen

We will now create a swipeable region at the top of the screen that (in addition to the “Home” button we’ve already created) allows the user to <strong>go back to the start page</strong>. While this functionality is not necessary, it gives the user another way to navigate the app, and it will teach you how to create a swipe in your prototype:

1.  In the Pages panel, select the third page, `all-recipes`.
2.  Create a hotspot that covers the entire width of the screen and the horizontal band across the title “Recipes” (see the illustration below).
3.  Customize the hotspot in the Properties panel:
    *   Initiate the swipe function: in the “Link” field, type `#` (a hash sign).

When a swipe is set, the transition, swipe and link are defined in the “Target” field:

1.  In the “Target” field, type `swipeleft,start,cubeleft` (i.e. when you _swipe_ left, go to the _start_ page, using the _cubeleft_ transition).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13ef48eb-0f1e-4b09-9d68-9a6fcb60253a/6-swipeback1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac73512f-7c50-4f2c-a562-b6a2ff69fa4e/6-swipeback1.500" alt="Swipe Back hotspot" width="500" height="437" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13ef48eb-0f1e-4b09-9d68-9a6fcb60253a/6-swipeback1.png">Larger version</a>)</em>

Next, let’s enable the user to <strong>choose a particular recipe</strong>:

1.  Over the Salisbury steak (located in the middle of the second row from the top), draw a hotspot.
2.  Customize the hotspot in the Properties panel:
    1.  Choose which page the hotspot will link to: in the “Link” field, select `chosen-recipe-intro-card.htm`.
    2.  Choose the transition: type `fade`.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9805036-7f11-4cdd-b36e-ec13889d5fea/7-foodhotspot1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81c8fb10-dcce-4b2a-af6c-1ca33754652d/7-foodhotspot1.500" alt="The preceding steps should result in a hotspot and hotspot properties." width="500" height="438" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9805036-7f11-4cdd-b36e-ec13889d5fea/7-foodhotspot1.png">Larger version</a>)</em>

### Page 4: Recipe Info Card

In the Pages panel, select the page <code>chosen-recipe-intro-card</code>.

<strong>Note:</strong> The design of page four is similar to the design of page three, in that page four is simply a lightbox laid over page three. This was achieved by sharing the wireframe layer of page three to page four. Sharing layers in Fireworks is an efficient way to maintain consistency in a project. The benefit of sharing layers between pages is that, if the design of page three is changed, those changes will be automatically reflected on page four.

1.  Create a hotspot over the “Cook This Recipe” button.
2.  Customize the hotspot in the Properties panel:
    1.  Choose which page the hotspot links to: in the “Link” drop-down menu, select `chosen-recipe-full.htm`.
    2.  Choose the transition: in the “Alt” field, type `flipright`.[![Recipe info card page](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6be4669a-3e67-4770-9635-7b6890ca2288/8-lighbtoxcookbutton1.500)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60c8c192-a06a-4b14-83b5-9945aa99f1e7/8-lighbtoxcookbutton1.png) _The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. ([Larger version](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60c8c192-a06a-4b14-83b5-9945aa99f1e7/8-lighbtoxcookbutton1.png))_
3.  Allow the user to close the lightbox:
    1.  Create four hotspots that completely surround the lightbox (one above, one below, one to the right and one to the left), and with the same attributes (i.e. the “Link” is `all-recipes.htm`, and “Alt” is `fade`).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6483dc03-bba9-459e-9a4b-dfb890ff8e78/9-lightboxexit1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef2efeb7-47a2-4c56-a400-8d4b29b78a07/9-lightboxexit1.500" alt="Closing the lightbox (hotspots)" width="500" height="438" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6483dc03-bba9-459e-9a4b-dfb890ff8e78/9-lightboxexit1.png">Larger version</a>)</em>

### Page 5: Recipe Detail Page

We will now create a “Back” button from the recipe detail page:

1.  Select `chosen-recipe-full` in the Pages panel.
2.  Create a hotspot over the “Back” button in the upper-left part of the screen.
3.  Customize the hotspot in the Properties panel:
    1.  Choose which page the hotspot links to: in the “Link” drop-down menu, select `all-recipes.htm`.
    2.  Choose the transition: in the “Alt” field, type `slideright`.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce38c670-5fb8-4217-85c8-6672d38ebff0/10-fullrecipeback1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fe1739c-28b5-4fa3-bf94-904194a53a37/10-fullrecipeback1.500" alt="Full Recipe back hotspot" width="500" height="438" /></a><br>
<em>The preceding steps should result in a hotspot and hotspot properties as shown in this screenshot. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce38c670-5fb8-4217-85c8-6672d38ebff0/10-fullrecipeback1.png">Larger version</a>)</em>

### Page 6: Landscape of the Recipe Detail Page

<strong>Note:</strong> Page five and six have a special relationship: they have the same name, except for the latter’s suffix of <code>&#95;l</code>. Thus, when page five is being viewed and the iOS device is rotated to landscape mode, the view will switch to page six!

Unlike the first five pages, page six has a landscape orientation. This was achieved by creating a page, adding <code>&#95;l</code> to the page’s name, and modifying the size of the canvas (Modify → Canvas → Canvas Size):

*   Set the width to 1024 pixels and the height to 768 pixels;
*   Enable the “Current page only” option.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2284b37d-9ed6-48e4-8836-08643474e99a/12-canvassize1.500"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2284b37d-9ed6-48e4-8836-08643474e99a/12-canvassize1.500" alt="Change canvas size" width="500" height="355" /></a><br>
<em>Changing the size of the landscape canvas</em>

To design the landscape page, either draw the landscape version from scratch, or rearrange and resize the graphics and symbols from the portrait version to fit the wider format.

## Conclusion

Now that all of the pages are linked together with hotspots, and the TAP properties (transitions, gestures and timers) are correctly set, the prototype should be ready for exporting.

We’ll do this in the next and final part of this tutorial!

### Further Reading

*   [Introducing New iOS6 Features In Mobile Safari](https://www.smashingmagazine.com/2012/12/10/ios6-new-features-developers-mobile-safari/)
*   [Developing A Design Workflow In Adobe Fireworks](https://www.smashingmagazine.com/2012/06/11/developing-a-design-workflow-in-adobe-fireworks/)
*   [Transform A Tablet Into An Affordable Kiosk For Your Clients](https://www.smashingmagazine.com/2012/11/26/transform-tablet-affordable-kiosk-clients/)
*   [Developing A Design Workflow In Adobe Fireworks](https://www.smashingmagazine.com/2012/06/developing-a-design-workflow-in-adobe-fireworks/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

{{< signature "mb, al, il" >}}

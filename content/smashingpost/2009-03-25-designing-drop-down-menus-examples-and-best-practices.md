---
title: 'Designing Drop-Down Menus: Examples and Best Practices'
slug: designing-drop-down-menus-examples-and-best-practices
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b9592499-df58-41ce-bd63-ad8958b2c492/dropdown.jpg
date: 2009-03-25T02:34:13.000Z
author: matt-cronin
summary: >-
  As a general rule, most Web developers, especially usability enthusiasts, say it is bad practice to use drop-down menus because they are confusing, annoying and oftentimes dysfunctional. From a design standpoint, however, drop-down menus are an excellent feature because they help clean up a busy layout. If structured correctly, drop-down menus can be a great navigation tool, while still being a usable and attractive design feature. 
description: >-
  In this article, we take a closer look at the nature of drop-down navigation menus and analyze situations in which they should or should not be used.
categories:
  - Inspiration
  - Showcases
  - Web Design
  - Navigation
---

Yes, that’s right: <strong>drop-down navigation menus can be user-friendly</strong>. Just yesterday Jacob Nielsen the results of his recent <a href="https://www.useit.com/alertbox/mega-dropdown-menus.html" rel="nofollow">drop-down menus study</a>, in which he found out that big, two-dimensional drop-down panels that group navigation options help users to avoid scrolling and can precisely explain the user’s choices with effective use of typography, icons, and tooltips.

These panels appear temporarily and disappear on their own when users move the pointer to another top-level option or to a "regular" part of the screen.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/455d7955-0f8d-4ed1-9b8b-77b83e5d9c2f/food.jpg" alt="Screenshot" width="500" height="404" /><br>
<figcaption>Huge vertical drop-down panel from Foodnetwork; notice a close button (the "x" in the upper right corner).</figcaption></figure>

In this article, we take a closer look at the nature of drop-down navigation menus, analyze situations in which they should or should not be used, discuss various implementations and finally showcase a couple of bad and good examples of such menus. The article also includes various tips and suggestions to help you work with your drop-down menus.

{{% feature-panel %}}

## Where To Use Drop-Down Menus

You will often see many trends in which drop-down menus are used. Here are a few of the most common ones.

### Organize Pages In A Section

Most commonly, drop-down menus are used to pull all of the pages in a certain category together in one organized element. This is essentially sub-navigation. Take a look at the design below. A drop-down element contains all of the different categories for a certain section of the website.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/948af20d-7d29-492b-9365-94548f34d6cc/change.org" alt="Screenshot" width="450" height="350" /></figure>

### Organize Categories In A Blog

You will see many blogs use a drop-down menu to organize categories and tags. Why? Blogs are driven by a large amount of information, so the layout needs to be as clean as possible to hold that content. A drop-down menu ultimately helps pull together links, such as categories, out of layout elements, such as the sidebar.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49d0562a-8814-4205-8cd7-e758960749a8/gomediazine.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Show Products on an eCommerce Website

You will see many e-commerce websites use drop-down menus to show products or categories of products. The drop-down menu is a friendly feature that all consumers can easily figure out, so it is a perfect way to organize products. The Best Buy website, shown below, does just this.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/306b0c3d-9523-47be-a2af-b87410be3456/bestbuy.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Display Modules

A drop-down can be an excellent way to tuck away an obstructive menu, which the user can click on to reveal. Take the example below, for instance. The sign-in element is part of the navigation, then appears in the form of a drop-down. This is a great way to take this large element out of the layout without negatively impacting usability.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2daec435-5029-4fb8-9a23-4f6aa25ccf15/collabfinder.jpg" alt="Screenshot" width="450" height="350" /></figure>

{{% ad-panel-leaderboard %}}

## Best Practices

Drop-down menus do in fact organize content into small, uncluttered elements, but if not done correctly, they can be just as bad as a messy layout. Here are some ways to make this controversial element more usable.

### Avoid a Drop-Down with More than Two Levels

Overall, this is just about the worst mistake one could make with drop-down menus in terms of usability. If done with a hover menu structure, the user will lose focus of the menu whenever the mouse pointer moves away from it. If done with a clickable structure, it has too many buttons and doesn’t work nicely.

The website shown below makes this mistake. The menus are very difficult to use because if you even slightly lose focus of the menu with the mouse pointer, you have to start from the top. Notice the tooltip, which also gets in the way of the navigation.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68ec7a42-0d8e-469a-843f-edd1b8135824/brita.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Option 1: Hover Menu

Basically, there are two ways to approach the drop-down menu: with either a hover or a click to activate the menu. From a design and convenience standpoint, a hover menu is better.

### Option 2: Clickable Menu

On the other hand, many will argue that a clickable menu is better because it is much more usable. Reason? Because of the way a hover menu is constructed, the user has to have the pointer over the menu at all times. If the user loses focus of the hover menu, it closes. Therefore, it is better to go with a drop-down menu that is activated by clicking a button, then deactivated by clicking the button once more.

CSS-Tricks has a tutorial showing how to create a layout similar to that of Digg. It is a perfect drop-down menu with a click-to-activate/deactivate feature, so it’s certainly something you should take a look at.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eae95e8d-a1c7-434e-a13c-aa53fc0dbad6/csstricks.jpg" alt="Screenshot" width="450" height="350" /></figure>

Also, Google features a usable drop-down menu using the click on/off trick.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/156b0a56-f2cf-4bd6-a08a-70b38a0e4b2d/google.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Delay the Deactivation of a Hover

Avoiding a hover structure and many levels in a drop-down may be too much of a restriction for the navigation you are trying to create. There is a solution, though, that can improve the usability of a hover and multi-level menu. With most menus, the drop-down disappears immediately after the user moves the mouse pointer away from the menu. The solution is to delay its disappearance. Or, have a click function that requires users to click outside the menu area to close the drop-down, similar to how a Lightbox functions.

Take Dell, for example. It uses a multi-level drop-down menu, but it is still somewhat usable. This is the only exception to the use of multi-level drop-down menus.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f89efb2-bcd3-42a2-9f09-7cd65af5128e/dell.jpg" alt="Screenshot" width="450" height="350" /></figure>

Furthermore, the menu on the Porsche website has multiple levels. However, the menu has a very wide focus range. This means you have to move your pointer a certain distance away from the menu to close it.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/453a70fa-7346-4143-a650-5cf40c4fd60f/porsche.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Add a Hover Effect to Menu Options

The navigation itself actually affects the usability of the drop-down menu. One way to make the menu work better with the drop-down is to add a hover effect to the menu options. This shows exactly which button in the navigation the menu is extending from, which will certainly help users.

The example below, the MediaTemple home page, shows a strong hover effect on the navigation options, which helps to support the drop-down menu.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53a32b43-bffc-4ad4-a5e0-b1efdd906915/mt.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Seamless Transitions

When a drop-down menu appears, it should appear seamlessly and without interruption. The menu should load immediately. Many websites make the mistake of making the menu so “heavy” that it takes more than an instant to load upon the hover.

Transition effects are one more detail that can look really cool. Instead of the menu simply appearing, try throwing in a wipe down or fade in. Just be sure to make the transition quick and not disruptive.

You will notice that Microsoft doesn’t do a very good job of creating a seamless menu. Observe the image below closely. You will notice that outlines from adjacent menus are still visible when the main menu is loading. When you move from button to button in the navigation, the drop-down menus have a slight lag, which looks bad. Of course, this doesn’t occur in all browsers, but it shouldn’t occur in any.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47412b07-8d55-4aad-8dd9-d51d4f9f6d57/microsoft2.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Remove Tooltips

Of course, when designing drop-down menus, there are always little details that impact usability. One important practice you may overlook is the presence of tooltips, or the lack of tooltips. You should always remove tooltips from buttons with drop-down menus. Reason? Tooltips just get in the way and sometimes even block the first list item in the drop-down menu.

Yes, we will be picking on Microsoft once more. Microsoft makes this mistake on its corporate page. Notice how the tooltip blocks many of the list items, which makes navigation that much more difficult.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91ba0bff-1f66-4d0c-9667-7c3ac63ab78b/microsoft.jpg" alt="Screenshot" width="450" height="350" /></figure>

{{% ad-panel-leaderboard %}}

## Styling Techniques

Content backgrounds can be somewhat of a challenge, too. The background has to be subtle, or it will ruin the content. Here are a few ways to liven up content backgrounds without going over the top.

### Use a Clean List

Not only is the element styling important, but the content styling is important, too. Clean typography and a readable list are important. Use smart spacing between elements in the list, and add a border above and below list items.

The example below from Audi shows a very well-organized and readable list. The list items are separated, and there are even list item icons.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/156a99df-f498-4e48-aa44-a1793043f8ea/audi.jpg" alt="Screenshot" width="450" height="350" /></figure>

On the other hand, The Washington Post’s website has a very poor list in the drop-down menu. There is not enough spacing between list items, so the menu is very cluttered and difficult to use.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9ce7cf9-6ba6-489d-913b-b8f9f77747d8/washingtonpost.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Hover Effects on List Items

All buttons need some sort of hover effect to be more usable. In drop-down menu lists, apply subtle hover effects, perhaps just a text color or background change. The White House website uses only a background change on list items, but it still helps the user.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49649e63-0085-4d77-b4e4-ce349334823f/whitehouse.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Semi-Transparent Background

This won’t work for all designs, but you should consider a semi-transparent background for the menu. The website shown below has a transparency, so the user can still see through to the image background. The key to semi-transparent elements is to keep a strong and readable contrast.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f491998-7c01-441b-b313-43eb7dd1030d/august.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Keep Styling Consistent with Menu

You will hear everywhere that consistency in styling is a must, and it certainly is. For navigation and a drop-down menu to work together as one unit, as they should, the styling needs to be similar. Use the same fonts and a similar background.

In the example below, the drop-down menu looks as it should.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49f1202c-ad2e-489a-83d8-25276ad24540/macstorm.gif" alt="Screenshot" width="450" height="350" /></figure>

## Poorly Constructed Menus

Below are some examples of drop-down menus that fall short somewhere with styling and usability.

### Navigant Consulting

This menu is poorly styled and dysfunctional.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fee2931-3eba-4a69-9090-c4dbd27a1aff/navigant.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Panasonic

Although this menu is well-styled, it is difficult to use because of a bad hover effect.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/315c5e7b-4e36-4553-9809-44e186dc6f57/panasonic.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Toshiba

The Toshiba menu is too small and does not follow good styling practices.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb2d70cf-8245-438c-88a8-9a0fb5aa2fed/toshiba.jpg" alt="Screenshot" width="450" height="350" /></figure>

### LG

Like the Microsoft menu above, this one has a slight lag, which makes it hard to use.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b066ac5-e2cb-4dff-a307-29ff1b4f35c8/lg.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Chrysler

The Chrysler page uses a drop-down menu with very small text, which makes it difficult to read.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fa89808-e829-406e-87f2-9ad25d18e225/chrysler.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Sun

These drop-down menus are rather fidgety and hard to use. The tooltip gets in the way, too, and directly above the main navigation is another drop-down menu. All of this makes it very difficult to navigate.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9313a5b9-23f3-4a46-918f-2fdb3a8e86c6/sun.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Creative Labs

The menu below is cluttered and does not have a delayed hiding or similar technique, so it is not very usable.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4aa53651-e828-4f1c-9bfa-b02587a2df93/creative.jpg" alt="Screenshot" width="450" height="350" /></figure>

### HP

Another hover menu that lacks usable features.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67aa9d17-38fa-4532-993b-605bf035b13d/hp.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Alienware

The black menu on the black design makes this drop-down difficult to use.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/536d5289-e08f-4011-ba23-1914ac495824/alienware.jpg" alt="Screenshot" width="450" height="350" /></figure>

## Good Drop-Down Menus

Here are many drop-down menus that have good usability and styling features.

### Sony

A well-constructed hover menu with a good list.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53163202-2124-4f85-81e4-eadbacc1042d/sony.jpg" alt="Screenshot" width="450" height="350" /></figure>

### ActionEnvelope

A clean vertical drop-down panel with a lot of padding; notice, how the panel appear to be above other design elements. Simple and beautiful solution.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dea4585d-2465-4df9-bd80-e123d13e7af3/action.jpg" alt="Screenshot" width="500" height="221" /></figure>

### Helmy Bern

A beautifully styled menu, with a fade transition.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84946bdc-a37c-4cdd-b670-96d42f2b2400/bern.jpg" alt="Screenshot" width="450" height="350" /></figure>

### RedBrick

This menu is cleanly styled and very readable.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/215916aa-8bb2-4f83-833a-48fc0acad7f6/redbrick.jpg" alt="Screenshot" width="450" height="350" /></figure>

### REI

This drop-down is very wide, so it is easy to keep the mouse in focus.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3c103a21-d7a5-4d70-bf21-86182343cb1e/rei.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Philips

Philips has a large and usable drop-down module.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e386a7d8-6336-4ff2-9d27-9b96bf931287/philips.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Walmart

On the Walmart site, the user clicks on the area outside the menu to close it.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a3f69d7-908a-468a-b74a-76231fd3b1fb/walmart.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Samsung

The Samsung menu is usable because of its large size and styling.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76ef428d-42c5-4e7f-8454-053e518c3514/samsung.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Epson

Epson shows another usable drop-down menu.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15ce7e16-896a-4b7c-bf80-cb4ad8308cc5/epson.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Mini Cooper

This website uses a drop-down menu with delayed closing.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1d9673a-4b17-4752-89f4-7948eadcd401/mini.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Gateway

Here is another usable drop-down element.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78ba9b52-5c2a-4fd5-a81d-11bff89abb2b/gateway.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Asus Global

A well-styled menu that has delayed hiding.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddb73de8-abae-4fd2-95db-716caee555d3/asus.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Intel

A very clean drop-down menu.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f49d183-ddf3-486f-a713-ec828d2bef2b/intel.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Target

A well-organized menu that has delayed closing.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f3e35d1-1cca-40d5-a344-73194cb5af72/target.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Garmin

This drop-down menu is simple yet functional.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b117f06-4858-477a-b0d9-6fb21b9fee64/garmin.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Logitech

A drop-down with very nice styling that matches the menu.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f622816e-541c-45fd-9b3d-1f4e53b2ba4f/logitech.jpg" alt="Screenshot" width="450" height="350" /></figure>

### Incase
This menu is very basic but serves its purpose.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef4a7c55-8859-4b48-83c0-f20ca1e2c93b/incase.jpg" alt="Screenshot" width="450" height="350" /></figure>

### evelMerch
A small yet functional drop-down, with a graphic to show users that the button opens a menu.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79ee83d0-0993-4d86-9a29-9f64332175bb/evel.jpg" alt="Screenshot" width="450" height="350" /></figure>

### IBM
A multi-level drop-down is used here, but a slight delay makes this one easier to use.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f4bcb32-c96a-4512-8645-696b4b3ea4cd/ibm.jpg" alt="Screenshot" width="450" height="350" /></figure>

### EA
A very clean and well-organized drop-down element.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c30260f-6889-4327-aa7d-69d2b3c3466d/ea.jpg" alt="Screenshot" width="450" height="350" /></figure>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Showcase of Creative Navigation Menus: Good and Bad Examples](https://www.smashingmagazine.com/2011/04/showcase-of-creative-navigation-menus-good-and-bad-examples/)
*   [Planning And Implementing Website Navigation](https://www.smashingmagazine.com/2011/06/planning-and-implementing-website-navigation/)
*   [Breadcrumbs In Web Design: Examples And Best Practices](https://www.smashingmagazine.com/2009/03/breadcrumbs-in-web-design-examples-and-best-practices/)
*   [Web Design Navigation Menus – Articles And A Beautiful Showcase](https://www.smashingmagazine.com/2009/02/50-beautiful-and-user-friendly-navigation-menus/)

{{< signature "al, il" >}}

---
title: 'Efficiently Simplifying Navigation, Part 3: Interaction Design'
slug: efficiently-simplifying-navigation-interaction-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1628618e-9eb7-414c-82ba-d1b8c442a8c6/pad-tablet-illu.jpg
date: 2014-09-18T21:13:04.000Z
author: anastasios-karafillis
description: >-
  Having addressed the [information
  architecture](https://www.smashingmagazine.com/2013/12/03/efficiently-simplifying-navigation-information-architecture/)
  and the [various
  systems](https://www.smashingmagazine.com/2014/05/09/efficiently-simplifying-navigation-systems/)
  of navigation in the first two articles of this series, the last step is to
  efficiently simplify the navigation experience — specifically, by carefully
  designing interaction with the navigation menu.
categories:
  - UX
  - Techniques
  - Navigation
  - UX
---
Having addressed the <a href="https://www.smashingmagazine.com/2013/12/03/efficiently-simplifying-navigation-information-architecture/">information architecture</a> and the <a href="https://www.smashingmagazine.com/2014/05/09/efficiently-simplifying-navigation-systems/">various systems</a> of navigation in the first two articles of this series, the last step is to efficiently simplify the navigation experience — specifically, by carefully designing interaction with the navigation menu.

When designing interaction with any type of navigation menu, we have to consider the following six aspects:

*   symbols,
*   target areas,
*   interaction event,
*   layout,
*   levels,
*   functional context.

It is possible to design these aspects in different ways. Designers often <a title="Creative and innovative navigation designs" href="https://www.smashingmagazine.com/2013/07/11/innovative-navigation-designs/">experiment with new techniques</a> to create a more exciting navigation experience. And looking for new, more engaging solutions is a very good thing. However, most users just want to get to the content with as little fuss as possible. For those users, designing the aforementioned aspects to be as <strong>simple, predictable and comfortable</strong> as possible is important.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Elements Of Navigation + 6 Design Guidelines](https://www.smashingmagazine.com/2012/03/the-elements-of-navigation/)
*   [Responsive Menus: Enhancing Navigation On Mobile Websites](https://www.smashingmagazine.com/2012/06/responsive-menus-enhancing-navigation-on-mobile-websites/)
*   [Can User Experience Be Beautiful?](https://www.smashingmagazine.com/2012/03/an-analysis-navigation-portfolio-websites/)
*   [Sticky Menus Are Quicker To Navigate](https://www.smashingmagazine.com/2012/09/sticky-menus-are-quicker-to-navigate/)

{{% feature-panel %}}

## Symbols

Users often rely on small visual clues, such as icons and symbols, to guide them through a website’s interface. Creating a system of symbolic communication throughout the website that is <strong>unambiguous and consistent</strong> is important.

The first principle in designing a drop-down navigation menu is to make users aware that it exists in the first place.</p>

### The Triangle Symbol

A downward triangle next to the corresponding menu label is the most familiar way to indicate a drop-down menu and distinguish it from regular links.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c308450c-f0ef-4490-9010-86a356ddcb03/1-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c93583fd-58cb-43d8-9ea7-cced3f03e15d/1-preview-opt.jpg" alt="1-preview-opt" width="500" height="408" /></a><br>
<em>A downward triangle next to the menu label is the most reliable way to indicate a drop-down. (Source: <a href="https://www.cbs.com/shows/bad-teacher/">CBS</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c308450c-f0ef-4490-9010-86a356ddcb03/1-large-opt.jpg">View large version</a>)</em>

If a menu flies out, rather than drops down, then the triangle or arrow should point in the right direction. The website below is exemplary because it also takes into account the available margin and adjusts the direction in which the menu unfolds accordingly.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a853abfb-48b8-450e-a761-0e32b0e4b9e5/2-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cedab58-06da-410e-b4c1-9b70fbe6601e/2-preview-opt.jpg" alt="2-preview-opt" width="500" height="377" /></a><br>
<em>A triangle or arrow pointing in the right direction is the most reliable way to indicate a fly-out menu. (Source: <a href="https://www.currys.co.uk/gbuk/index.html">Currys</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a853abfb-48b8-450e-a761-0e32b0e4b9e5/2-large-opt.jpg">View large version</a>)</em>

### The Plus Symbol

Another symbol that is used for opening menus is the plus symbol (“+”). Notice that the website below mixes symbols: an arrow for the top navigation menu and a “+” for the dynamic navigation menu to the left (although an arrow is used to further expand the dynamic menu — for example, to show “More sports”).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b860fddb-e57a-490a-a449-0bd7406fd913/3-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eddc226f-5105-487c-96fd-a74012b9a594/3-preview-opt.jpg" alt="3-preview-opt" width="500" height="374" /></a><br>
<em>Some websites use a “+” to drop down or fly out menus. (Source: Nike) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b860fddb-e57a-490a-a449-0bd7406fd913/3-large-opt.jpg">View large version</a>)</em>

Mixing symbols can be problematic, as we’ll see below. So, if you ever add functionality that enables users to add something (such as an image, a cart or a playlist), then “+” would not be ideal for dropping down or flying out a menu because it typically represents adding something.

### The Three-Line Symbol

A third symbol often used to indicate a navigation menu, especially on responsive websites, is three horizontal lines.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc29502b-26ff-452c-b5ad-4fe591e8ae01/4-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de96cccf-009f-47e8-bc60-c43411bf0bfc/4-preview-opt.png" alt="4-preview-opt" width="500" height="48" /></a><br>
<em>Three horizontal lines is frequently used for responsive navigation menus. (Source: <a href="https://nokia.com">Nokia</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc29502b-26ff-452c-b5ad-4fe591e8ae01/4-large-opt.png">View large version</a>)</em>

Note a couple of things. First, three lines, like a <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de455e00-5289-46d5-beef-78060e409cc6/grid.jpg">grid</a> and a <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4e7c35a-47e4-4e40-aa94-d0ef29a5abb5/bullet-list.jpg">bullet list</a> icon, communicate a certain type of layout — specifically, a vertical stack of entries. The menu’s layout should be consistent with the layout that the icon implies. The website below, for example, lists items horizontally, thus contradicting the layout indicated by the menu symbol.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1287858-5f83-4293-a20f-ae4a4f8bd656/5-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4d4391d-2c98-47a0-9be3-307f88e8d3d9/5-preview-opt.jpg" alt="5-preview-opt" width="500" height="296" /></a><br>
<em>Three lines do not work well if the menu items are not stacked vertically. (Source: <a href="https://2012.dconstruct.org">dConstruct 2012</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1287858-5f83-4293-a20f-ae4a4f8bd656/5-large-opt.jpg">View large version</a>)</em>

The advantage of the more inclusive triangle symbol and the label “Menu” is that they suit any layout, allowing you to change the layout without having to change the icon.

Secondly, even though three lines are becoming more common, the symbol is still relatively new, and it is more ambiguous, possibly representing more than just a navigation menu. Therefore, a label would clarify its purpose for many users.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dce9d782-3f83-43d2-9bc6-4eeadec52db9/6-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9347723e-e534-4f9e-821f-0b5fb7481776/6-preview-opt.jpg" alt="6-preview-opt" width="500" height="58" /></a><br>
<em>An accompanying label would clarify the purpose of the three lines. (Source: <a href="https://kiwibank.co.nz/">Kiwibank</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dce9d782-3f83-43d2-9bc6-4eeadec52db9/6-large-opt.jpg">View large version</a>)</em>

### Consistent Use Of Symbols

While finding symbols that accurately represent an element or task is important, also carefully plan their usage throughout the website to create a consistent appearance and avoid confusion.

Notice the inconsistent use of symbols in the screenshot below. The three lines in the upper-right corner drop down the navigation menu. The three lines in the center indicate “View nutrition info.” The “Location” selector uses a downward triangle, while the “Drinks” and “Food” menus, which drop down as well, use a “+” symbol.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f570221-31b2-4d72-970b-c712a4ca586d/7-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69a82413-268d-405c-9a8f-915d9333ada1/7-preview-opt.png" alt="consistent_symbols" width="500" height="534" /></a><br>
<em>Inconsistent symbols lead to confusion. (Source: <a href="https://www.starbucks.com/menu/catalog/product?drink=bottled-drinks#view_control=product">Starbucks</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f570221-31b2-4d72-970b-c712a4ca586d/7-large-opt.png">View large version</a>)</em>

While using multiple symbols for a drop-down menu is inconsistent, using arrows for anything other than a drop-down menu causes problems, too. As seen below, all options load a new page, rather than fly out or drop down a menu.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47abd2a5-7e19-4065-8e98-40905ea24d49/8-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a37ea98-69b5-406f-b27f-f524ee6c3ba1/8-preview-opt.png" alt="arrow" width="500" height="401" /></a><br>
<em>Using a triangle or arrow for anything other than a drop-down or fly-out menu can cause confusion. (Source: <a href="https://www.baristaprima.ca/">Barista Prima</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47abd2a5-7e19-4065-8e98-40905ea24d49/8-large-opt.png">View large version</a>)</em>

This leads to a couple of problems. First, using arrows for regular links — whether to <a href="https://baymard.com/blog/ux-illusion-of-space">create the illusion of space</a> or for other reasons — puts pressure on you to consistently do the same for all links. Otherwise, users could be surprised, not knowing when to expect a link to load a simple menu or a new page altogether. Secondly, a single-level item, such as “Products”, could conceivably be expanded with subcategories in the future. A triangle could then be added to indicate this and distinguish it from single-level entries, such as the “About” item.

Users generally interpret an arrow to indicate a drop-down or fly-out menu. And they don’t have any problem following a link with no arrow, as long as it looks clickable. It is best not to mix these two concepts.

## Target Areas

A simple yet important rule is that links in a navigation menu should be <strong>easy to read, large and consistently located</strong>. The area in the interface that is assigned to and activates a link is typically referred to as the target area.</p>

### Legibility

Before clicking a target, a user will obviously want to read its label. Therefore, consider the font’s size and the legibility of the label and description accordingly. Notice below that the link labels in the center (“Laptops,” “Desktops,” etc.) are large and contrast with the background, enabling the user to comfortably read and distinguish between them, unlike the labels in the drop-down menu.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c8bb3c0-fbcc-4de2-b73e-bc3b4ec45608/9-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04d6f159-7e39-42a6-b16e-db3505325b7e/9-preview-opt.jpg" alt="target_areas" width="500" height="418" /></a><br>
<em>Links should be easy to read and allow for comfortable navigation. (Source: <a href="https://www.toshiba.com/tai/products_consumer.jsp">Toshiba</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c8bb3c0-fbcc-4de2-b73e-bc3b4ec45608/9-large-opt.jpg">View large version</a>)</em>

Also, consider how a font performs in dim lighting, which is especially an issue on mobile. While <a title="Typographic Design Patterns And Current Practices (2013 Edition)" href="https://www.smashingmagazine.com/2013/05/17/typographic-design-patterns-practices-case-study-2013/">many recommendations about font settings</a> can be followed, still test your settings because individual preferences will vary.</p>

### Size

The larger and closer a target is, the easier and faster it is to hit. This simple rule predates the digital era and is one that <a href="https://www.smpp.northwestern.edu/savedLiterature/FittsLawPapers/Information Capacity of Human Motor System Controlling Ampltude of Movement.Paul.Fitts.pdf">Paul Fitts tried to quantify</a> in human-computer interaction.

One common suggestion is to use every available pixel by extending the clickable area of a link to the entire space reserved for it. As a result, less precision will be required to click the link, which will speed up navigation. Below, notice how the target area on the left lets a few pixels go to waste. The target area on the right is larger and quicker to click because it occupies every pixel at its disposal.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45a423fd-227a-4599-9fc8-6e433430e27e/10-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7aa42e8c-613d-4035-a973-2a90a9209b09/fitts.jpg" alt="target areas" /></a><br>
<em>Fitts Law tells us to exploit every available pixel. (Source: left:<a href="https://philly.com">Philly</a>, right: <a href="https://apple.com">Apple</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45a423fd-227a-4599-9fc8-6e433430e27e/10-large-opt.jpg">View large version</a>)</em>

Similarly, make the images in mega-menus and separate pages into target areas as well, not only their labels.

The downside of large targets is that they can break the balance of an interface and quickly eat up screen space. However, even with plenty of space to spare, enlarging the target areas to be as big as possible is not necessary because there is not a one-to-one correlation between the size of a target and its usability.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf833a99-198d-4fd1-b0c1-cf479696abae/11-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e65776b-b1ee-423f-b649-4154e0c0c17e/non-linear-progression1.jpg" alt="usability progression" /></a><br>
<em>The relationship between the size and usability of a target is not linear. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf833a99-198d-4fd1-b0c1-cf479696abae/11-large-opt.png">View large version</a>)</em>

Thus, if a small target is made 10% larger, it will become much more usable, but if an already big target is made 10% larger, it will not gain much more in usability.</p>

### Consistency of Location

Apart from being large enough and easy to read, target areas should be consistently located. This builds muscle memory in the user, further facilitating navigation.

One type of multi-level navigation that creates inconsistent target areas is the nested menu. In a nested menu, a subcategory appears directly under its parent category, which constantly pushes the items below into new locations.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0854d42-f4b7-4837-89ee-623ad9b44dfb/nested-menus11.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14bb220f-1c5c-4617-afd2-5cee90ec9a6a/nested-menus1.jpg" alt="nested_menus" /></a><br>
<em>Nested menus create inconsistently positioned target areas. (Source: “<a href="https://webdesign.tutsplus.com/tutorials/big-menus-small-screens-responsive-multi-level-navigation--webdesign-8452">Big Menus, Small Screens: Responsive, Multi-Level Navigation</a>,” Tessa Thornton, Tuts+) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0854d42-f4b7-4837-89ee-623ad9b44dfb/nested-menus11.jpg">View large version</a>)</em>

A better way to display multiple levels is to fly out or slide to the submenus, as we’ll discuss in more detail below.

However, single-level navigation menus can have inconsistent target areas as well, especially when the user is trying to close the menu. When some menus are opened, the clickable area moves to a different location. Below, the “close” button is pushed down whenever a menu or submenu is opened.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15866ce5-db89-4ac3-a975-5e48c11b0f0d/13-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/928ea8e6-e18e-4d7f-8a58-9d451271db4d/13-preview-opt.png" alt="inconsistent_trigger" width="500" height="302" /></a><br>
<em>A repositioned button makes it more difficult to close the menu. (Source: <a href="https://elc-eu.org">ELC</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15866ce5-db89-4ac3-a975-5e48c11b0f0d/13-large-opt.png">View large version</a>)</em>

This requires the user to look for the “close” and then move their cursor or hand to the new spot. Reserving the same spot for opening and closing a menu is easier. In addition, the user should be able to click any non-linked spot outside of the menu to close it.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae13b0c1-a4f6-4f8b-8a8b-b46242e84787/14-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89eb5b75-8981-45f3-9350-23cd55d3f17f/14-preview-opt.png" alt="consistent_menu" width="500" height="346" /></a><br>
<em>Consistent clickable areas and generous targets make it easier to close the menu. (Source: <a href="https://starbucks.com">Starbucks</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae13b0c1-a4f6-4f8b-8a8b-b46242e84787/14-large-opt.png">View large version</a>)</em>

## Interaction Event

The interaction event describes the type of input that users have to perform to interact with an interface. The four most common interaction events in navigation menus are:

*   hovering,
*   clicking,
*   scrolling,
*   typing.</p>

### Hovering

Hovering (or mousing over) is the most common interaction event in navigation menus. The problem with hovering, however, is that accidentally moving the cursor just inside or outside the target area will immediately activate or close the menu. One workaround that is often suggested is to <a href="https://www.mackido.com/Interface/hysteresis.html">use a delay</a>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0284cba8-bb4f-4bb9-8f5a-9168f9419d67/15-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce070693-3eff-4c45-b6f1-6fb322d46ec2/15-preview-opt.png" alt="timeout_delay" width="500" height="250" /></a><br>
<em>A delay is often used to account for accidental hovering. (Source: <a href="https://zealousweb.co.uk">ZealousWeb</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0284cba8-bb4f-4bb9-8f5a-9168f9419d67/15-large-opt.png">View large version</a>)</em>

Of course, if the delay is too long, interaction will become sluggish and annoying. There is no “correct” value for the delay because proficiency in moving the cursor varies not only by individual, but by fatigue level and the user’ familiarity with the menu.

A second workaround is to create temporary invisible target areas based on predicted path of the cursor’s movement. The blue overlay in the screenshot below depicts such an invisible area, where users can access the contents of a submenu without accidentally opening another menu in the process.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb3bc04-f2a3-4763-955c-7a46df9941f6/16-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4f7d4a7-2610-4d4c-870e-f1f0104a5cc9/16-preview-opt.png" alt="cursor_path" width="500" height="385" /></a><br>
<em>Invisible target areas minimize mistakes and facilitate navigation based on predicted cursor paths. (Source: “<a href="https://bjk5.com/post/44698559168/breaking-down-amazons-mega-dropdown">Breaking Down Amazon’s Mega Dropdown</a>,” Ben Kamens) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb3bc04-f2a3-4763-955c-7a46df9941f6/16-large-opt.png">View large version</a>)</em>

However, this workaround has its own problems. Because the user has no way of knowing that the invisible areas exist in the first place, they will still try to carefully move the cursor along visible paths. Even if they do know, invisible areas invariably produce their own share of mistakes. Finally, because the areas are temporary, the issues related to variations in cursor movement speed still hold true.

Another problem is tooltips. Some authors suggest <a href="https://www.nngroup.com/articles/mega-menus-work-well/">using tooltips in navigation menus</a> to explain the options.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/643364a9-9206-4fec-8778-0831d44d37bf/17-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/854d0665-7273-4ab1-afac-dcd97333eb26/17-preview-opt.png" alt="tooltips" width="500" height="257" /></a><br>
<em>Tooltips do not work well in navigation menus. (Source: <a href="https://www.miniusa.com/content/miniusa/en.html">Mini</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/643364a9-9206-4fec-8778-0831d44d37bf/17-large-opt.png">View large version</a>)</em>

However, because tooltips require hovering, users encounter the following problems, in this order:

1.  Because tooltips appear on hover, users might not know that they exist and, thus, not discover them. If tooltips are important for explain the options, this is rather unfavorable.
2.  Tooltips could obstruct adjacent items.
3.  The delay problem strikes again. If the delay is too short, the tooltip will flicker. If it is too long, then getting the tooltip for each item will be slow and annoying.
4.  As a consequence, comparing items will be more difficult.
5.  Hovering does not work on touchscreens, thus inhibiting a consistent cross-device experience.

Note, however, that <a href="https://www.nngroup.com/articles/using-link-titles-to-help-users-predict-where-they-are-going/">link titles</a> that appear in the body of text are not bad at all because the context is different. A body of text is meant mainly for reading, not navigation, so many users will just want to read the article and won’t care much about the links. However, if they do care, the hypertext and its context are often sufficient clues about the link’s target. In case they are not, a link title can be indeed very useful, especially because it probably will not cover other hyperlinks in the article.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9137909-4c26-461e-9e69-9b9850acf83d/18-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3eb0431e-74da-4b36-aab3-693923ab0f90/18-preview-opt.png" alt="tooltip" width="500" height="350" /></a><br>
<em>Link titles can be useful additions to hyperlinks. (Source: <a href="https://sixrevisions.com/usability/data-visualization-gestalt-laws/">Six Revisions</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9137909-4c26-461e-9e69-9b9850acf83d/18-large-opt.png">View large version</a>)</em>

However, a navigation menu is a different story, as explained above. So, if descriptions are necessary to explain the options, then use regular text, rather than tooltips.

All in all, hovering is not a good technique for enabling interaction with menus, and the workarounds do not alleviate the problems.</p>

### Clicking

Clicking to open a drop-down menu and its submenus should become the standard, not hovering. This would yield the following benefits:

*   Individual proficiencies would be better accounted for. High-proficiency users would still be the fastest.
*   Mistakes would amount to virtually zero, thus reducing stress.
*   This would allow for multi-tasking. Users could pause navigation in any state, switch to another tab or application and then resume where they left off.
*   Hovering does not work on touchscreens. Clicking would make for a consistent, unified experience.

The increasing prevalence of clicking as the interaction pattern for navigation menus is a positive trend.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa3de90e-39f7-47e1-be5b-c58047c3a868/19-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c9485ff-adf4-4607-b2df-eb9aa242c0e4/19-preview-opt.jpg" width="500" height="374" /></a><br>
<em>Opening and closing menus should be done by clicking, not hovering. (Source: <a href="https://mediatemple.net/">Media Temple</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa3de90e-39f7-47e1-be5b-c58047c3a868/19-large-opt.jpg">View large version</a>)</em>

### Scrolling

While users do not mind a certain amount of scrolling, avoid excessive or unnecessary scrolling.

Having users scroll to see all options is sometimes inevitable, especially when you’re using a separate page for a navigation menu. However, reserve scrolling <strong>only for browsing categories</strong>, not for navigating between categories. Below, users have to scroll to the bottom of the page to see all categories.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/802237f0-25c4-4860-8419-93a543347c6b/20-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d418bd7e-e3ee-442b-8805-e0467a8a092c/20-preview-opt.jpg" width="500" height="298" /></a><br>
<em>Scrolling should be used to browse categories, not to navigate between categories. (Source: <a href="https://abc.go.com/shows">ABC</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/802237f0-25c4-4860-8419-93a543347c6b/20-large-opt.jpg">View large version</a>)</em>

The design above forces the user to scroll through a lot of undesired content to get to the category they want. A better solution would be to present the categories at the top of the page. This would allow users to skip unwanted sections. I’ve mocked this up to illustrate:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bdd3e70-5532-4b31-8576-410caab2a102/21-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24022a79-6e79-4046-8110-a52559d83c43/21-preview-opt.jpg" alt="mockup_levels" width="500" height="241" /></a><br>
<em>Linking to categories at the top of the page enables users to go directly to their desired categories. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bdd3e70-5532-4b31-8576-410caab2a102/21-large-opt.jpg">View large version</a>)</em>

Apart from that, be aware that including labels, images and descriptions is a better way to explain media content such as TV shows.</p>

### Typing

A fourth type of interaction event is typing. The two common techniques here are <strong>search and typing to filter</strong>. The difference between them is that search does not require a navigation menu. Whereas, when users type to filter, they have already navigated to a content category and are typing a term to dynamically narrow down a list of already visible entries. The app below shows the latter technique, although the designers labeled it "search". Still, this is unlikely to cause confusion as "search" and "filter" are, indeed, very similar concepts.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/291ac5d4-3d50-4d0d-85c2-ae675bbd7f29/22-large-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/291ac5d4-3d50-4d0d-85c2-ae675bbd7f29/22-large-preview-opt.jpg" alt="22-preview-500px-opt" width="500" height="526" /></a><br>
<em>Typing to filter is similar to search but is used to navigate within, rather than to, content categories. (Source: <a href="https://getpocket.com/">Pocket</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/291ac5d4-3d50-4d0d-85c2-ae675bbd7f29/22-large-preview-opt.jpg">View large version</a>)</em>

The purpose of typing to filter is to spare users from having to scroll through and read a long list. However, it does come with the same problems of uncertainty and the heavy cognitive load that we mentioned with search. However, it is somewhat alleviated by the fact that the user has already navigated to a content category. Therefore, if a list is very long, it is worth breaking down the content category into subcategories or offering dynamic filters, as the app shown below does.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/152ac83f-e075-4c67-821b-49e457d8bd0a/23-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a0fb6d7-2842-4006-86e8-599a91da998a/23-preview-opt.jpg" alt="23-preview-opt" width="500" height="328" /></a><br>
<em>Subcategories and dynamic filters help to break down long lists. (Source: <a href="https://getpocket.com/">Pocket</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8142a7b2-582f-4d94-9655-684b9480e037/23-large-opt.png">View large version</a>)</em>

Be aware, though, that typing to filter, like search, works better with large personal databases in applications, such as file managers and email clients, rather than for websites, because the user would more likely know the particular string they are looking for related to the item they want.</p>

## Levels

Designing a single-level navigation menu is hard enough as it is. Incorporating multiple levels complicates the matter, especially on small screens.</p>

### Removing Navigation Levels

To reduce the complexity of multiple levels, some authors suggest <a href="https://ux.stackexchange.com/questions/28825/how-to-solve-overly-deep-hierarchy-navigation-on-mobile-device">reducing the number of navigation levels, especially for mobile screens</a>. The rationale is to spare users from having to navigate many levels. However, removing levels could have an adverse effect. Below, the category “Products” consists of two levels.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c73440-006d-4a14-92eb-85f1b8214f84/24-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61c6f446-fb0e-4f2d-bdcf-0730542ac860/24-preview-opt.png" alt="levels" width="500" height="320" /></a><br>
<em>Some websites display more levels in their desktop view than in their mobile view. (Source: <a href="https://microsoft.com">Microsoft</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09c73440-006d-4a14-92eb-85f1b8214f84/24-large-opt.png">View large version</a>)</em>

In its menu for mobile screens, Microsoft removes the first level (“Windows”, “Office”, “Devices”, etc.). The result is a very long list that lacks structure and requires the user to work more to find and navigate to the product they are looking for.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59e896ae-1c97-44e9-8c8e-ab7543c7cf0a/25-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28776aa4-d146-4fb0-9248-f54e8302f1ec/25-preview-opt.png" alt="long_lists" width="500" height="328" /></a><br>
<em>Removing levels creates long lists and obscures entries. (Source: <a href="https://microsoft.com">Microsoft</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59e896ae-1c97-44e9-8c8e-ab7543c7cf0a/25-large-opt.png">View large version</a>)</em>

By contrast, keeping the additional level makes for shorter, more informative lists. I mocked up this solution to illustrate:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d444061-c6cf-4882-8454-9d4f00b69dff/26-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/918cc917-3eee-4c08-ac95-83284a9e2784/26-preview-opt.png" alt="levels_mockup" width="500" height="328" /></a><br>
<em>Subcategories make for lists that are shorter, more descriptive and easier to interact with. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d444061-c6cf-4882-8454-9d4f00b69dff/26-large-opt.png">View large version</a>)</em>

Of course, even with the right number of levels, multiple-level navigation remains a tricky affair and requires careful design and implementation — on all types of devices.</p>

### Levels And Mobiles

Large, wide screens offer space for fly-out submenus.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc392f65-947b-4cdb-a886-a61bbd331365/27-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d43a18a-9edc-49ee-a3f2-72bcb3aeb88e/27-preview-opt.jpg" alt="fly-out" width="500" height="250" /></a><br>
<em>Large screens can get fly-out submenus. (Source: <a href="https://www.intel.com/content/www/us/en/homepage.html">Intel</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc392f65-947b-4cdb-a886-a61bbd331365/27-large-opt.jpg">View large version</a>)</em>

Mobile devices are not wide enough for fly-out menus. There are two ways to deal with this limitation.

As soon as the user selects a menu option, you could slide them right to a separate screen that displays the content of the submenu.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78fc1c6a-e5fd-4fe6-b8ae-0382aca94136/28-large-opt.jpg"><img loading="lazy" decoding="async" class="203558" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41bce1bf-65e6-4d68-b896-0308971ebd89/28-preview-opt.jpg" alt="28-preview-opt" width="500" height="299" /></a><br>
<em>Sliding to submenus on a separate screen is the mobile equivalent of a fly-out submenu. (Source: <a href="https://www.sonypictures.com/movies/">Sony Pictures</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78fc1c6a-e5fd-4fe6-b8ae-0382aca94136/28-large-opt.jpg">View large version</a>)</em>

Above, the submenu’s title is displayed in a heading, along with a “&lt;” button that enables users to slide back to the parent category. Two things to note about sliding menus. First, the symbol should be relevant to the type of animation. Sony correctly uses the “&lt;” symbol to slide users to the left, but why it uses “+” to do the opposite is not clear. The sliding menu below uses symbols that are more in line with their animations.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5184a8b-3c26-45c2-b301-940187d39385/sliding-symbols1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07483742-cfe3-4774-9101-2bf30b993929/29-preview-opt.jpg" alt="sliding_symbols" width="500" /></a><br>
<em>Symbols should be relevant to the type of animation. (Source: <a href="https://asus.com/us">Asus</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5184a8b-3c26-45c2-b301-940187d39385/sliding-symbols1.jpg">View large version</a>)</em>

Secondly, consider the fold. I cropped the screenshot above to highlight this problem. The “Commercial” category actually has five entries, but users might miss the bottom one.

A second way to display multiple levels is to nest them. Nested menus are stacked, and the levels are visually distinguishable with the help of gradients or indentation.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ac0895-857c-40d1-9963-85764b709c62/nest1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b973115-1d95-44ce-9848-f51b8e3481dd/30-preview-opt.jpg" alt="nest" width="500" /></a><br>
<em>The levels of nested menus are stacked. (Source: “<a href="https://blog.medianotions.de/en/articles/2008/mootools-nested-accordion">MooTools: Nested Accordion</a>” (standard demo with MooTools 1.11), Media Notions Blog) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ac0895-857c-40d1-9963-85764b709c62/nest1.jpg">View large version</a>)</em>

However, because the items are stacked, not only are the target areas inconsistent, but they also take up vertical space, which can push entries out of the viewport and require users to scroll. Sliding menus are a simpler, more space-efficient way to navigate to a content category.</p>

### Levels And Mega-Menus

A mega-menu, which <a href="https://www.nngroup.com/articles/mega-menus-gone-wrong/">structures options into panels and subareas</a>, is another way to display multiple categories. Nonetheless, displaying the contents of no more than a single category at a time is recommended. The menu pictured below displays the contents of eight categories. Obviously, users will be interested in the contents of only one particular category at any time. Consequently, the space taken up by the other seven categories goes to waste, cluttering the menu as well.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/574937c7-d244-471b-a7d8-48a6be34b96b/31-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e47696c2-509d-48b1-96f1-d7d58872aee2/31-preview-opt.jpg" alt="31-preview-opt" width="500" height="271" /></a><br>
<em>Displaying the contents of multiple categories clutters the menu and is redundant. (Source: <a href="https://target.com">Target</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/574937c7-d244-471b-a7d8-48a6be34b96b/31-large-opt.jpg">View large version</a>)</em>

A better solution is to <strong>organize subcategories into tabs</strong>. Best Buy, pictured below, has to accommodate similar types and numbers of products. However, it has chosen to tab its menu. As a result, the user sees only the contents of the category that they have explicitly selected. Also, because the tabs reduce the number of items displayed, the menu looks much cleaner, allowing space for pictures and icons with the items.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/757e6ce3-ec91-468b-9253-5c289b282ac1/32-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94bfa724-ee2e-46a3-80bb-a76510b04a74/32-preview-opt.jpg" alt="32-preview-opt" width="500" height="295" /></a><br>
<em>A tabbed mega-menu reduces the number of items displayed and frees up space for pictures. (Source: <a href="https://www.bestbuy.ca/en-CA/home.aspx#">Best Buy</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/757e6ce3-ec91-468b-9253-5c289b282ac1/32-large-opt.jpg">View large version</a>)</em>

### Dynamic Filters

Websites with many items and, thus, many levels often employ a dynamic filter but, interestingly, always implement the dynamic filter on the same level.

Dynamic filters can be implemented in one of several ways. Below, the filters are implemented as nested menus. The problem with nested menus, however, is that just one or two open filters will likely push the other filters below out of the viewport, requiring users to scroll. Also, unless the user closes the nested menus after selecting the values they need, a lot of the menus will be cluttering the interface.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f08e567-b6a1-4577-ae9a-0e3e259d6563/33-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/387a770f-6da1-4aed-a823-7b590811e8df/33-preview-opt.jpg" alt="33-preview-opt" width="500" height="326" /></a><br>
<em>Nested menus can clutter the interface with unneeded options and require a lot of scrolling. (Source: <a href="https://www.sears.com/shoes-mens-shoes-mens-casual-shoes/b-1253483662">Sears</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f08e567-b6a1-4577-ae9a-0e3e259d6563/33-large-opt.jpg">View large version</a>)</em>

An alternative is to use drop-down menus, which keep the interface clean and the interaction consistent.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5338209-dd76-4614-add4-811d99682acc/34-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02321d90-e725-49a7-8f57-80be953e33b2/34-preview-opt.jpg" alt="34-preview-opt" width="500" height="385" /></a><br>
<em>Implementing dynamic filters as drop-down menus keeps the interface clean and the interaction consistent. (Source: <a href="https://www.omegawatches.com/watchfinder">Omega</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5338209-dd76-4614-add4-811d99682acc/34-large-opt.jpg">View large version</a>)</em>

The downside is that users have to open a drop-down menu each time to view and select its values.

If you go with drop-down menus for the filters, consider their placement carefully. Shown above, Omega places its filters <strong>above</strong> the products. On a tablet held in portrait orientation, this would be the best arrangement. However, on a wide screen, multiple lines of filters would take away space from the products and visually emphasize the filters, rather than the products.

Placing the filters <strong>beside</strong> the items, as mocked up below, has the opposite effect. It slightly transfers space and emphasis from the filters to the products.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af8e1b04-c9b2-49bb-8c00-8407b1e69d50/35-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d4942b3-2cee-417d-a901-36303408b237/35-preview-opt.jpg" alt="35-preview-opt" width="500" height="324" /></a><br>
<em>Placing the filters beside the products on a wide screen emphasizes the products rather than the filters. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af8e1b04-c9b2-49bb-8c00-8407b1e69d50/35-large-opt.jpg">View large version</a>)</em>

On mobile, the user almost necessarily has to toggle one screen to select and confirm the values and another to display the results, which is what the website shown below does.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed1d4aa6-82a3-4f4a-a1f2-2d6420034059/36-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75ef5577-bebc-459e-b998-0f9b4a81f83e/36-preview-opt.jpg" alt="36-preview-opt" width="500" height="377" /></a><br>
<em>Dynamic filters often require two screens on mobiles, one for the filters and another for the results. (Source: <a href="https://m.lowes.com/category?langId=-1&amp;storeId=10702&amp;catalogId=10051&amp;nValue=4294857973&amp;store=595">Lowes</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed1d4aa6-82a3-4f4a-a1f2-2d6420034059/36-large-opt.jpg">View large version</a>)</em>

Another possibility is to place the filters in a drop-down menu or overlay box.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cd33624-8b75-40ba-be4f-200fdf195067/37-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8028f91-830e-4088-82d7-35a20d4fa1a6/37-preview-opt.jpg" alt="37-preview-opt" width="500" height="277" /></a><br>
<em>Placing dynamic filters in a drop-down menu or overlay box keeps the context of the products page. (Source: <a href="https://m.zappos.com/women-shirts-tops/CKvXARDL1wHAAQHiAgMBGAI.zso">Zappos</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cd33624-8b75-40ba-be4f-200fdf195067/37-large-opt.jpg">View large version</a>)</em>

The benefit of the latter approach is that it keeps the context of the product page, rather than sending users to a separate screen. However, a separate screen remains the better choice if the filters do not fit on a single screen and users are, thus, required to scroll in order to interact with them.

After choosing a widget and positioning the filters, the next step is to visualize the values. A few simple rules will help with this:

*   If the filter values are **mutually exclusive**, then use **radio buttons** or tabs or display the values as plain entries in a drop-down menu.
*   If the values are **independent**, then display them along with a **checkbox**.
*   If the values **increment in consistent intervals** (weight, duration, price, distance, etc.), then use a **slider**, as shown below.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/282957da-f804-45b7-8617-85c6a4656ef2/gradual-sliders.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3c418e2-7f25-4f7e-8c31-d31f2dc20077/38-preview-opt.jpg" alt="filters" /></a><br>
<em>Consistently incrementing values are best represented by a slider. (Source: <a href="https://freetimeapp.com">Free Time</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/282957da-f804-45b7-8617-85c6a4656ef2/gradual-sliders.jpg">View large version</a>)</em>

Of course, being able to deselect values is also important. Radio buttons, for example, cannot be returned to their default state once a value has been selected. A reset button would, therefore, come in handy.

Finally, consider whether to implement a separate bar that displays the selected values. The website below lists selected values at the top of the page, along with a “close” button that enables users to remove the values again.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c186946-66bb-4501-9a90-2f160e4d53ab/39-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62ce34ea-5968-4d59-bff9-85cb7d836693/39-preview-opt.jpg" alt="39-preview-opt" width="500" height="341" /></a><br>
<em>In many interfaces with dynamic filters, a separate bar displays the selected values. (Source: Food) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c186946-66bb-4501-9a90-2f160e4d53ab/39-large-opt.jpg">View large version</a>)</em>

This separate bar provides feedback about the selected values. But it takes up space, which is especially an issue on small screens. Also, the dynamic filters already display the selected values, albeit not as elegantly. A separate bar would, therefore, require users to look at and work with two areas instead of one to basically do the same thing.

So, not repeating the values in a separate area should not be much of a usability issue.</p>

### Breadcrumbs

An interesting topic that often comes up in discussions on navigation systems with multiple levels is breadcrumbs. A breadcrumb trail visualizes the user’s current location in the website.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac4fec12-df09-498f-9e9b-0d1b914f1b39/40-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6d03051-179b-4b25-9d97-a2a8586b8aa4/40-preview-opt.jpg" alt="40-preview-opt" width="500" height="324" /></a><br>
<em>Breadcrumbs visualize the user’s current location relative to the website. (Source: <a href="https://www.homedepot.com/b/Appliances-Cooking-Microwaves-Built-In-Microwaves/N-c3q3Z5yc1v#./N-c3q3Z5yc1v?&amp;_suid=1385830414682015189466296192966">Home Depot</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac4fec12-df09-498f-9e9b-0d1b914f1b39/40-large-opt.jpg">View large version</a>)</em>

Users rarely interact with breadcrumbs. They occasionally access parent categories in the breadcrumb trail, but if they start navigating from the home page, they will usually only click their way from one category to the next. Likewise, if they land from an external link, then they would not need breadcrumbs. Nonetheless, breadcrumbs have <a href="https://usabilitygeek.com/12-effective-guidelines-for-breadcrumb-usability-and-seo/">many small benefits</a> that make them worth implementing, the most important one being that they impart a sense of structure and orientation.

Imagine that using a search engine is like <a href="https://www.nngroup.com/articles/breadcrumb-navigation-useful/">parachuting</a> into an unknown forest. If the user only wants some wood, that that would get the job done. But imagine a sign in the forest that says <code>Hoosier Forest &gt; in Monroe County &gt; in the state of Indiana &gt; in the US &gt; on the North American continent</code>. Immediately, users would gain a important sense of orientation.

This is also why breadcrumbs help users who are lost. The first step in knowing where to go is knowing where one is.

Even developers who opt not to use breadcrumbs still implicitly follow its logic by constructing their URLs as a breadcrumb trail, with the domain name as the starting point, followed by a common classification scheme, such as topic or date, and with the levels divided by a forward slash, <code>/</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81cf2c8d-5598-4b45-b3c9-2ec46ad886f9/41-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e15289f-049d-4778-84dc-0b464baf6b7b/41-preview-opt.jpg" alt="41-preview-opt" width="500" height="568" /></a><br>
<em>URLs are typically written as a breadcrumb trail. (Source: top: “<a href="https://www.uie.com/articles/breadcrumbs/">Design Cop-Out #2: Breadcrumbs</a>,” Jared Spool, User Interface Engineering, bottom: “<a href="https://derivadow.com/2010/02/18/the-problem-with-breadcrumb-trails/">The Problem With Breadcrumb Trails</a>,” Tom Scott) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81cf2c8d-5598-4b45-b3c9-2ec46ad886f9/41-large-opt.jpg">View large version</a>)</em>

The example below shows one problem with implementing breadcrumbs. On the desktop, you have enough space, and following <a href="https://www.smashingmagazine.com/2009/03/17/breadcrumbs-in-web-design-examples-and-best-practices-2/">best practices</a> is not too difficult. However, breadcrumbs sometimes duplicate the information in the URL bar. The website below has a meaningful and consistent URL architecture. However, because the breadcrumb trail is identical, it seems redundant.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36fefa21-0e6f-4c7e-8df8-3f495d2a99dc/42-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3203e20b-e599-450e-b18a-1ab0402f4428/42-preview-opt.jpg" alt="42-preview-opt" width="500" height="381" /></a><br>
<em>Breadcrumbs sometimes duplicate the information in the URL. (Source: <a href="https://www.area17.com/work/wythe-hotel-website">Area 17</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36fefa21-0e6f-4c7e-8df8-3f495d2a99dc/42-large-opt.jpg">View large version</a>)</em>

Nonetheless, many users expect a dedicated breadcrumb trail, not just a consistent URL architecture. If, however, your navigation system has no more than two levels, and especially if you have tabbed navigation, as below, then a breadcrumb trail is not necessary.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96676fb6-87eb-43c8-9296-681006a7b280/43-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69e1d5db-8d47-46f7-8a5d-483c387426f6/43-preview-opt.jpg" alt="43-preview-opt" width="500" height="383" /></a><br>
<em>Breadcrumbs are unnecessary in navigation systems with one or two levels. (Source: <a href="https://www.express.co.uk/entertainment/books">Express</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96676fb6-87eb-43c8-9296-681006a7b280/43-large-opt.jpg">View large version</a>)</em>

On mobile, the situation is even trickier. The website shown below demonstrates a good solution. Rather than implementing an entire breadcrumb trail, the designers display only the current category in the center and then show the parent category with a <code>&lt;</code> in the top-left corner.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08360177-a260-488a-a5ef-ac3af9478629/44-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d26f9ce-3869-4930-b25d-05ebb7f9a246/44-preview-opt.jpg" alt="44-preview-opt" width="500" height="374" /></a><br>
<em>On mobile, showing only the current and parent category in the path will suffice. (Source: <a href="https://m.lowes.com/category?langId=-1&amp;storeId=10702&amp;catalogId=10051&amp;nValue=4294857647&amp;store=595">Lowes</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08360177-a260-488a-a5ef-ac3af9478629/44-large-opt.jpg">View large version</a>)</em>

While this solution does not show the entire path, it will have to do on mobile. The only problem is that Lowes’ designers use up two lines, instead of one. Admittedly, placing both a long label for the parent category and a centered header on one line on a small screen is difficult, but with carefully planning, keeping the labels short, possibly abbreviating the parent category with an ellipses (<code>…</code>), it can be achieved.</p>

### Mega-Sites

Finally, a type of website that features many levels is the so-called mega-site.

Mega-sites typically belong to large organizations with many large sub-departments, such as universities, broadcast networks, media conglomerates and governments. The difference, however, is that each sub-department is considered not just the next level in the navigation menu, but a separate, independent mini-site, with its own, distinct audience and image.

First, be aware that mini-websites are not as independent as they may seem. If they were, they would have their own domain. It is not unlikely that users would want to explore other departments, especially if they like the mini-site.

One rule can help you achieve the goal of balancing a unique mini-site with easy-to-use navigation: While the <strong>visual design</strong> for individual departments can be as <strong>unique</strong> as you like, keep the <strong>interaction</strong> across departments as <strong>consistent</strong> as possible.

In the mega-site shown below, each department has its own visual style, but the interaction across departments is fairly consistent.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/341d33a0-a235-44a0-8261-283142241df5/45-large-preview.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a950d528-914f-4cc1-8e89-0a031281d396/45-preview-opt.jpg" alt="45-preview-opt" width="500" height="820" /></a><br>
<em>Consistency facilitates navigation in other departments. (Source: <a href="https://www.ard.de/home/ard/ARD_Startseite/21920/index.html">Ard</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/341d33a0-a235-44a0-8261-283142241df5/45-large-preview.jpg">View large version</a>)</em>

The mega-site pictured below has less consistent navigation, which makes it more difficult to explore departments.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff9d2818-1d78-4695-9cbe-8c7691aa7166/46-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe5a3049-6096-4c1f-b418-eed9cf572061/46-preview-opt.jpg" alt="46-preview-opt" width="500" height="892" /></a><br>
<em>Varying navigation can impede exploration of other departments. (Source: <a href="https://www.bbc.com/">BBC</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff9d2818-1d78-4695-9cbe-8c7691aa7166/46-large-opt.jpg">View large version</a>)</em>

The reason for distinguishing between visual and interaction design is simple. The user knows that a medical school will look different from a law school and so will expect a unique visual design. But there is no reason why the medical school should put its contact information in the bottom-left corner and the law school in the top-right corner.</p>

## Layout

Layout in web design refers to the arrangement of elements in a meaningful, aesthetically pleasing way. However, laying out elements for reading is different than layout out items in a navigation menu.

A piece of content can be complex and unique. Laying out its elements in a specific, sophisticated way might be necessary to explain it. Navigation is different. A menu is made up of categories and subcategories. The items in a category should all match the category’s description, as simple as that. Users do not expect anything else in a navigation menu. Thus, the goal of layout is not to explain items, but merely to <strong>sort</strong> them.</p>

### Sorting Items

Some people suggest <a href="https://www.nngroup.com/articles/alphabetical-sorting-must-mostly-die/">not sorting alphabetically</a>, but instead looking for other ways. Be aware, though, that alphabetical sorting is very logical in most cases. The menu pictured below does not use alphabetical sorting.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4938e620-d83a-44ca-9047-acfec338b70e/47-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a31882b-33cd-4472-8a8f-1773c3811622/47-preview-opt.jpg" alt="47-preview-opt" width="500" height="94" /></a><br>
<em>If the sorting logic is not immediately clear, then browsing and finding items can be difficult. (Source: <a href="https://verious.com">Verious</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4938e620-d83a-44ca-9047-acfec338b70e/47-large-opt.jpg">View large version</a>)</em>

The items seem to be arranged arbitrarily. But even if there is a sorting logic, it does not really matter. If users are not able to figure it out immediately, then browsing and finding items will be more difficult. The advantage of alphabetical sorting is that users will figure it out immediately. Also, if the user knows the name of the option they are looking for in that category, they will find it very quickly.

Nonetheless, a sorting logic other than alphabetical can be more helpful to users on occasion. Take the “News” category. The title itself is a clue to an alternative sorting logic. News items are best sorted by publication date, not alphabetically.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7342fa47-d572-4ecf-8683-bd3403626d20/48-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46003884-052b-4c9d-9bc1-b7cda2025fe5/48-preview-opt.jpg" alt="48-preview-opt" width="500" height="591" /></a><br>
<em>Sometimes, a sorting logic other than alphabetical is more appropriate. (Source: <a href="https://theweek.com/section/index/politics">The Week</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7342fa47-d572-4ecf-8683-bd3403626d20/48-large-opt.jpg">View large version</a>)</em>

Finally, some websites offer a widget that enables users to choose how to sort items in a navigation menu. A sorting widget is often added to interfaces with dynamic filters.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54bb1898-4cd0-4ace-9866-2cd1be8c651f/49-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d895e745-2619-4850-bcac-d219252ca7bc/49-preview-opt.jpg" alt="49-preview-opt" width="500" height="371" /></a><br>
<em>A sorting widget enables users to choose how to sort items in a navigation menu. (Source: <a href="https://www.costco.com/all-tvs.html">Costco</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54bb1898-4cd0-4ace-9866-2cd1be8c651f/49-large-opt.jpg">View large version</a>)</em>

Be aware that users use sorting widgets not so much to sort and then comprehensively browse results as they do to <a href="https://www.uxmatters.com/mt/archives/2009/07/the-mystery-of-filtering-by-sorting.php">filter out undesired items</a>. For example, if a user sorts items by rating, then they are obviously more interested in higher-rated items than lower-rated ones.

Nonetheless, a sorting widget can be a useful addition. Users will know immediately what it does and how to use it. Also, if implemented as a drop-down menu, it won’t take up too much space. However, as with the more powerful dynamic filters, a widget is only necessary if the menu has more than a few items and if breaking down a long list into subcategories is not called for.</p>

### How Users Scan Information

Correctly sorting items can be tricky. And laying out options in that order is not without pitfalls either.

The three most common layouts for a navigation menu are <strong>lists, columns and grids</strong>. There are additional, more sophisticated layouts, as we’ll see, but keep things as simple and familiar as possible. In the three aforementioned layouts, the user will scan through the items as shown below.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd682250-14fe-4382-a263-8ad6d23883a4/50-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/036c5231-6694-4a24-8d83-2c1d8505802c/50-preview-opt.jpg" alt="50-preview-opt" width="500" height="146" /></a><br>
<em>Users typically scan information according to the layout. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd682250-14fe-4382-a263-8ad6d23883a4/50-large-opt.jpg">View large version</a>)</em>

In addition, the navigation items should be left-aligned, not centered, which is more familiar and easier to read.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba2f6245-4b9f-43bd-82aa-06e06150da6f/51-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/860b4152-2a6e-40a5-a85f-c1a1bc3df390/51-preview-opt.jpg" alt="51-preview-opt" width="500" height="407" /></a><br>
<em>Items in the navigation menu should be left-aligned. (Source: <a href="https://aritzia.com/">Aritzia</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba2f6245-4b9f-43bd-82aa-06e06150da6f/51-large-opt.jpg">View large version</a>)</em>

Be aware, though, that the way users scan information is not written in stone, but culturally conditioned.</p>

### Choosing the Right Layout

The next question, of course, is when to use which layout. The type and amount of your content is a good guide:

*   **Labels only**.  In this case, a list or set of columns is the best choice. Whichever you choose will depend on the available screen space of the device.
*   **Labels and pictures**.  Here, a grid is the best choice.
*   **Labels, pictures and descriptions**.  In this case, anything but a list would not be feasible. Even if there is enough space for a grid, a list is still the best choice.

To better understand the subtleties of grids and lists, examine the website below, which enables users to switch between a list and grid. First, look at the grid view.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/323f6629-6bfa-4801-9341-875632c81c15/52-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2e21fba-27ca-4f3c-96ba-040fa9a9810c/52-preview-opt.jpg" alt="52-preview-opt" width="500" height="626" /></a><br>
<em>The grid mode is space-efficient and emphasizes the pictures, which helps users quickly spot items they want. (Source: <a href="https://usatoday.com/money">USA Today</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/323f6629-6bfa-4801-9341-875632c81c15/52-large-opt.jpg">View large version</a>)</em>

The main focus is the pictures, not the labels or, in this case, the titles. The labels could be displayed over top of the picture, which would slightly compromise the pictures, or above and beneath it, which would slightly compromise the space efficiency. A grid is still the most space-efficient view, as well as the best for quickly spotting items — that is, if pictures are sufficient for explaining the options. By contrast, consider the list view:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30b16d0e-d65e-4e3a-8b58-3e8e2b737a0f/53-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/481d16cc-e185-4389-a897-f798b4393f0a/53-preview-opt.jpg" alt="53-preview-opt" width="500" height="812" /></a><br>
<em>A list takes up more space and emphasizes descriptions. (Source: <a href="https://usatoday.com/money">USA Today</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30b16d0e-d65e-4e3a-8b58-3e8e2b737a0f/53-large-opt.jpg">View large version</a>)</em>

The focus is on the titles and descriptions, which are centered. The pictures take a supporting role. A list takes up more space than a grid; however, reading is more comfortable in a list.

For news, a list is best. Pictures are not sufficient to explain the options; titles and descriptions, which are missing in the grid view, are required. If the items were not news articles but clothes, paintings or cars, products whose point of interest can be conveyed by a picture, then a grid would be suitable.

These rules apply to all traditional navigation menus. Interestingly, with dynamic filters, the rules change.

First, consider what would be the best view in a regular menu for electronic products, such as mobile phones, computers or cameras. A grid view might seem to be the best choice. After all, users typically want a stylish product, and a grid emphasizes pictures. The pictures below are cropped to emphasize this.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c32b1c1f-c0e3-44bb-93ae-2f5dfed64e2e/54-large-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0398a8ed-9c4a-472d-a875-bc928ddadb01/54-preview-500px-opt.jpg" alt="54-preview-500px-opt" width="500" height="517" /></a><br>
<em>A grid view emphasizes pictures of products. (Source: <a href="https://www.pcrichard.com/Computers-Tablets/Computers-Notebooks/Laptop-Computers/703020.pcrc?view=grid&amp;trail=">P.C. Richard &amp; Son</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c32b1c1f-c0e3-44bb-93ae-2f5dfed64e2e/54-large-preview-opt.jpg">View large version</a>)</em>

However, users also look for certain features in electronic devices, be it number of pixels, wireless connectivity, CPU speed, etc. So, a list, which is better suited to displaying technical information, would work best for these type of items.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0420dc7f-3a7d-442b-bc84-10fec58715d9/55-large-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c21382e9-399c-4a45-b9b0-cce8beea01a3/55-preview-500px-opt.jpg" alt="55-preview-500px-opt" width="500" height="644" /></a><br>
<em>A list is best suited to displaying technical information. (Source: <a href="https://www.pcrichard.com/Computers-Tablets/Computers-Notebooks/Laptop-Computers/703020.pcrc?view=list&amp;trail=">P.C. Richard &amp; Son</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0420dc7f-3a7d-442b-bc84-10fec58715d9/55-large-preview-opt.jpg">View large version</a>)</em>

Dynamic filters change the equation. Their very purpose is to capture and display meta data. Therefore, displaying the same data in a list would be unnecessary. The better choice would be a grid that only displays the three elements that dynamic filters cannot properly show: the name of the product, a picture and the exact price. The screenshot below demonstrates this, showing the same menu as above but this time with dynamic filters.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d71d92cc-6c10-46dc-bb58-12e84be788f1/56-large-opt.jpg"><img loading="lazy" decoding="async" class="size-medium wp-image-203673" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b703d6be-ccfa-497c-8c55-8c129819b5ff/56-preview-opt.jpg" alt="56-preview-opt" width="500" height="538" /></a><br>
<em>A grid is best suited if dynamic filters can accommodate the desired meta data. (Source: <a href="https://www.pcrichard.com/Computers-Tablets/Computers-Notebooks/Laptop-Computers/703020.pcrc?pageNum=0&amp;view=grid&amp;trail=1135%3AApple|Asus|Samsung%3A1137%3A250.00-500.00|500.00-1000.00|1000.00-2500.00">P.C. Richard &amp; Son</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d71d92cc-6c10-46dc-bb58-12e84be788f1/56-large-opt.jpg">View large version</a>)</em>

Of course, if the dynamic filters cannot display the required information properly (for example, descriptions of articles), then a list remains the best view.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03d7f41f-a24b-4f71-822c-46419c03d4d8/57-large-opt.jpg"><img loading="lazy" decoding="async" class="size-medium wp-image-203675" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad8b0ccc-50a1-4668-bf42-fbf5ef3fecc3/57-preview-opt.jpg" alt="57-preview-opt" width="500" height="462" /></a><br>
<em>If dynamic filters cannot properly accommodate crucial information, then a list is the best choice. (Source: <a href="https://query.nytimes.com/search/sitesearch/#/U.S.+foreign+policy/">New York Times</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03d7f41f-a24b-4f71-822c-46419c03d4d8/57-large-opt.jpg">View large version</a>)</em>

### Home Pages

A fourth way to lay out items is often encountered on “Home” or “Featured Items” pages. First, notice that the “US” section in the screenshot below displays items in a simple, traditional list.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/043c7851-9910-4e96-b0b0-d3e4eb8eb4c6/58-large-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbc9e0de-dd2e-40ff-b866-e11fe2468234/58-preview-500px-opt.jpg" alt="58-preview-500px-opt" width="500" height="589" /></a><br>
<em>Subsections often have simple, traditional layouts. (Source: <a href="https://america.aljazeera.com/topics/topic/categories/us.html">Al Jazeera America</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/043c7851-9910-4e96-b0b0-d3e4eb8eb4c6/58-large-preview-opt.jpg">View large version</a>)</em>

All sections of Al Jazeera’s website have the same layout. However, the home page has a different, more sophisticated layout.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c69ef9ad-2fc3-4a7b-ba85-452c6f305ffa/59-large-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f454376-1d6a-4244-a4b8-ead2d073105d/59-preview-500px-opt.jpg" alt="59-preview-500px-opt" width="500" height="601" /></a><br>
<em>Home pages contain featured items that users would otherwise have to access by going to the corresponding subsections. (Source: <a href="https://america.aljazeera.com/">Al Jazeera America</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c69ef9ad-2fc3-4a7b-ba85-452c6f305ffa/59-large-preview-opt.jpg">View large version</a>)</em>

The latest news article is given center stage and the largest picture. Links to related articles are next to it. A bar underneath horizontally lists recent items from various subsections. And a vertical list further below shows past articles.

There are a few reasons why “Home” and “Featured Items” pages look the way they do, with their more complex layouts. Users can access featured articles by visiting the corresponding subsection, whereas the home page displays those featured articles from the subsections, making them directly visible and accessible. However, because the home page lacks the descriptive precision of subcategories, the designers highlighted and prioritized the articles through layout.

There are three things to note about the layout of the “Home” and “Featured Items” pages. First, as important as the home page is, users should be able to easily see and access subsections as well. Secondly, the home page is still essentially one big navigation menu, not a page for consumption per se, so the layout should be simple. Thirdly, many large websites have multiple big sections that are designed as “home” pages; keeping their layouts consistent will make it easier for users to find their way around.</p>

### Tag Clouds

Finally, a fifth type of layout for navigating to content is the tag cloud. A tag cloud uses gradients, font size and positioning to show the relative importance or recurrence of items in a category.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7690171-a8b0-4446-93cd-9c1610e260b7/60-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e7783e1-59ce-4ab6-ae2e-61fc31c23b54/60-preview-opt.jpg" alt="60-preview-opt" width="500" height="310" /></a><br>
<em>Tag clouds are a complex visualization of weighted navigation choices. (Source: <a href="https://www.professionalontheweb.com/">Professional on the Web</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7690171-a8b0-4446-93cd-9c1610e260b7/60-large-opt.jpg">View large version</a>)</em>

Interestingly, tag clouds enable users to visualize items both alphabetically and by importance at the same time. Nonetheless, sorting by name or frequency makes items easier to understand and faster to scan. Apart from that, a tag cloud hardly works with anything but labels.</p>

## Functional Context

Functional context refers to the function that a user performs in a particular situation — in this case, whether they are <strong>navigating to or consuming</strong> content. These functions, however, play different roles in the user’s experience. As mentioned, navigation is merely a means to consuming content, so users expect navigation and consumption to contrast with each other.</p>

### Duplicate Navigation Menus

The content of a website could be pictures, videos or statistical data. After adding the main content itself, many developers will add options for the content, such as additional data, a chart view or an option to darken the surrounding page while a video is playing. They do so to make the available content more appealing to consume. However, the situation is the opposite with navigation. While users might want to view the same set of data in different chart types, they need only one type of menu to navigate to the data.

One wrong solution that is all too common is that clicking a navigation link drops down a submenu first.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9291d59-d984-44d1-aa18-2577502d6186/61-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e31d03a3-2416-4272-a470-b5eb672df3b6/61-preview-opt.jpg" alt="61-preview-opt" width="500" height="269" /></a><br>
<em>Clicking a menu link often drops down a submenu. (Source: <a href="https://www.maplin.co.uk/">Maplin</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9291d59-d984-44d1-aa18-2577502d6186/61-large-opt.jpg">View large version</a>)</em>

However, clicking the same link twice takes users to a separate page, which is for the same content category.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a855d54-8f08-46c4-b832-f1354f1c44f4/62-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c55df8e2-e973-4622-bcb0-9cf52b66d533/62-preview-opt.jpg" alt="62-preview-opt" width="500" height="267" /></a><br>
<em>Clicking the same link again will often open a separate page for the same content category. (Source: <a href="https://www.maplin.co.uk/c/computing-and-office">Maplin</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a855d54-8f08-46c4-b832-f1354f1c44f4/62-large-opt.jpg">View large version</a>)</em>

In some cases, as with Maplin, two different navigation menus are even on the same page.

We’d be dealing with one of two scenarios:

*   The drop-down menu and the separate page contain the same items, with the separate page usually displaying the items in more detail and with additional information.
    *   Example: [Tiger Direct](https://tigerdirect.com)
    *   Counter-example: [Best Buy](https://bestbuy.ca)
*   The drop-down menu contains a few featured items, while the separate page contains the same featured items as well as all other items that match that category.
    *   Example: [Boston Globe](https://www.bostonglobe.com)
    *   Counter-example: [Time](https://time.com)

Unfortunately in both scenarios, effort is duplicated for both users and designers, yet without benefit.

In the first scenario, the user will probably compare the menus first. “Why are there two navigation menus? Do they offer different options? If so, which is better suited to my navigation needs?” What’s more, returning visitors might repeat the process when new content is added. This is time they could have spent navigating to and consuming content from a single menu.

The second scenario has additional problems. If the user does not like the featured items in the drop-down menu, they might be reluctant to see the other options, especially because that would entail loading a new page and finding their way around again.

Again, instead of offering two types of menus, a mega-menu and a separate page, that both navigate to content, ask yourself which would do a better job of it, and then put all your effort into properly designing that one.</p>

### Visual Design In Navigation Menus

Another factor in the balance of navigation and consumption of content is visual design.

Mega-menus and separate pages offer ample space for pictures, but <strong>pictures should be used merely to explain options</strong>, not to present users with a degree of detail that would make them stop and “consume” the menu itself. Below, the car is presented in great detail, both in the large impressive picture and in the information below it.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bbe1103-631a-4c30-9bcf-9cb6c6bd5371/63-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01ed05d7-1e83-4d0e-93d0-c9edb685680b/63-preview-opt.jpg" alt="63-preview-opt" width="500" height="376" /></a><br>
<em>Large pictures and detailed information can create problems in navigation menus. (Source: <a href="https://porsche.com/usa">Porsche</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bbe1103-631a-4c30-9bcf-9cb6c6bd5371/63-large-opt.jpg">View large version</a>)</em>

While the menu might look exciting at first, it actually creates a few problems in its interaction and efficiency of space.

First, the large picture and text take up so much space that only one item can be displayed. So, to compare their options, the user has to constantly move their cursor between the small submenu entries in the middle. Secondly, the content page shown below is rightly designed to put the product into the spotlight and to give the user a lot of information about it. However, because the navigation has a similar style, the effect of transitioning to the main content is not as impressive as it could be.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d03f9e7-3189-4fd9-a237-3561eb8c89b4/64-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ae5727d-0f98-48ba-9070-2b4a022fdfb3/64-preview-opt.jpg" alt="64-preview-opt" width="500" height="509" /></a><br>
<em>If the navigation is similar in design to the product page, then the latter will look less impressive. (Source: <a href="https://porsche.com/usa/models/boxster/boxster-s">Porsche</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d03f9e7-3189-4fd9-a237-3561eb8c89b4/64-large-opt.jpg">View large version</a>)</em>

By contrast, in the example below, the designs of the navigation and main content are distinct. The pictures in the menu are large and detailed enough for the user to be able to easily distinguish between models but small enough to be lined up horizontally. Also, the text is restricted to helping users decide which model to explore in detail.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac9509ee-2a26-40cc-b040-a09145b47c8a/65-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee31e548-ebc9-4e49-8562-97e7360af098/65-preview-opt.jpg" alt="65-preview-opt" width="500" height="331" /></a><br>
<em>Pictures in navigation menus are best used to explain options, not to present in detail. (Source: <a href="https://lexus.com">Lexus</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac9509ee-2a26-40cc-b040-a09145b47c8a/65-large-opt.jpg">View large version</a>)</em>

Then, once users pick a model, they are taken to a dedicated page that presents the product in as detailed and spectacular a fashion as possible.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9e7431c-c223-43dc-8e3c-6be503bdd082/66-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/216fc908-2a10-4e45-923a-37ed373e9f37/66-preview-opt.jpg" alt="66-preview-opt" width="500" height="357" /></a><br>
<em>The best way to present a product in detail is on a separate dedicated page. (Source: <a href="https://lexus.com/models/IS">Lexus</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9e7431c-c223-43dc-8e3c-6be503bdd082/66-large-opt.jpg">View large version</a>)</em>

### Animation And Navigation

Another reason to make navigation and content distinct has to do with animation.

Some responsive websites have advanced animation, such as <a href="https://www.smashingmagazine.com/2013/01/15/off-canvas-navigation-for-responsive-website/">off-canvas navigation</a> and <a href="https://filamentgroup.com/lab/responsive_design_approach_for_navigation/">flexible navigation</a>. In general, content is moved down or to the side to reveal the navigation. The website pictured below slides in the menu from the left, pushing content to the right.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9415f30-48bb-47f8-bf98-d54435ee40a5/offcanvas1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0c64ac1-567b-435b-8782-e89292b7221e/67-preview-opt.jpg" alt="offcanvas" width="500" height="362" /></a><br>
<em>Some websites animate content to reveal the navigation. (Source: <a href="https://mashable.com">Mashable</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9415f30-48bb-47f8-bf98-d54435ee40a5/offcanvas1.jpg">View large version</a>)</em>

Animation, if purposefully deployed, can be a useful way to explain transitions on the screen. Left and right sliding animations, for example, visualize the moving back and forth between navigation levels. However, sliding animation should be used only to explain navigation and nothing else.

With the techniques mentioned above, by contrast, both content and navigation are animated. While other developers might be impressed by the effect because they know how technically difficult it is to do, users might think different. Users might ask why the content is moving if they’ve only requested the menu. Building and maintaining such an effect take time and resources, yet the result could be perceived as confusing.

The traditional way to animate navigation is to slide it over top of the content, as mocked up below, which is a simpler, more efficient solution for both developers and users.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81ae804d-464a-473e-a5c0-e3265b8870a6/mockup-menu1.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbc527e5-8578-4a35-84ea-682b20683327/68-preview-opt.jpg" alt="mockupmenu" /></a><br>
<em>Sliding the navigation menu over top of the content is a simpler, more efficient way to present navigation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81ae804d-464a-473e-a5c0-e3265b8870a6/mockup-menu1.jpg">View large version</a>)</em>

### Immersing the User in the Functional Context

A final point concerns immersing the user in one function by fading out the other.

Many websites that have drop-down navigation also have media such as videos and slideshows that play either automatically or manually, the latter being favorable because it puts the user in control. In either case, be considerate and pause media in the background as soon as the menu is opened to allow the user to assess their navigation options without distraction.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10b5ef79-28ef-41d1-9457-4ccdf8812823/69-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/692fe38b-2bd0-466c-a6e0-c95ed8f7c667/69-preview-opt.jpg" alt="69-preview-opt" width="500" height="461" /></a><br>
<em>When the user opens the menu, pause carousels and other media to allow for undisturbed navigation. (Source: <span class="removed_link" title="https://www.forever21.com/shop/ca/en">Forever 21</span>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10b5ef79-28ef-41d1-9457-4ccdf8812823/69-large-opt.jpg">View large version</a>)</em>

## Summary

The recommendations in this article can be summed up as follows:

*   **Symbols**.  Indicate drop-down menus with a symbol; a text label with a triangle is the most reliable indicator. Consistent use of symbols throughout the website will minimize confusion.
*   **Target areas**.  Target areas in navigation should be large, easy to read and consistently positioned to make interaction comfortable.
*   **Interaction event**.  Interaction with navigation should be based on clicking, not hovering or typing. Scrolling should be allowed only for navigating within, not between, categories.
*   **Layout**.  Alphabetical sorting is good, but don’t overlook alternative sorting methods. Lists, columns and grids are the most familiar types of layouts for menus. If short text is sufficient to explain the options, then go for a list or columns. If pictures are best, then choose a grid. If longer descriptions are necessary, then a list is the best choice. If dynamic filters can accommodate crucial information, then use a grid; otherwise, a list.
*   **Levels**.  Display the content of no more than a single category at a time. Tabbed mega-menus and sliding menus are the most efficient solutions for mobile. Also, too few levels can complicate navigation by creating long lists that are hard to digest. If you have more than a couple of levels, consider a breadcrumb trail. On a mega-site, give each sub-department a unique visual design, but keep the interaction consistent across departments.
*   **Functional context**.  Use only one type of navigation for a website, and use pictures merely to explain the options, not to present in detail. Also, once users activate the menu, pause any distractions, such as video or slideshows.</p>

## Final Thoughts

The gist of designing a navigation system that is easy to use is to restrict and follow up the navigation options for your target audience as well as to keep the information in the menu to a minimum.

However, these two steps make up only half the story. Because the users have to interact with the navigation, two more steps are required — namely, to choose and then design the right type of navigation.

As for choosing the right type, the less information that is necessary to explain the options and the less it amounts to, the simpler the navigation will be. Finally, the menu should be designed to be as simple, predictable and comfortable as possible.

<strong>Simplicity</strong> means using only one type of navigation menu and displaying the contents of a single category at a time. <strong>Predictability</strong> comes from following consistent and familiar patterns. And <strong>comfort</strong> follows from reducing mistakes and stress by making the interaction forgiving and inclusive.

These four steps might sound like common sense, but mistakes that break or compromise the user’s experience often happen along the way. Hopefully, this series of articles has helped you avoid mistakes and improve your navigation for users as a result.</p>

### Further Reading

Here are some resources you might be interested in:

*   “[Guide to Website Navigation Design Patterns](https://sixrevisions.com/user-interface/navigation-design-patterns/)” Cameron Chapman, Six Revisions
*   [Welie: Patterns in Interaction Design](https://www.welie.com/)
*   “[Designing for Mobile, Part 2: Interaction Design](https://www.uxbooth.com/articles/designing-for-mobile-part-2-interaction-design/)” Elaine McVicar, UX Booth
*   “[Responsive Navigation Patterns](https://bradfrostweb.com/blog/web/responsive-nav-patterns/)” Brad Frost
*   “[Complex Navigation Patterns for Responsive Design](https://bradfrostweb.com/blog/web/complex-navigation-patterns-for-responsive-design/)” Brad Frost
*   “[Navigation Patterns for Mobile Optimized Retail Websites](https://www.slideshare.net/theresaneil/mobile-retail-navigation-patterns)” Theresa Neil, Slideshare

{{< signature "al, il" >}}


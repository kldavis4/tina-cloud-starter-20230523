---
title: 'Smart Responsive Design Patterns, Or When Off-Canvas Isn’t Good Enough'
slug: smart-responsive-design-patterns-or-when-off-canvas-isnt-good-enough
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec326e8a-cfc4-4cd0-b7fc-ae47c4f2b093/bmw-builder-500px-opt.png
date: 2016-05-30T18:15:16.000Z
summary: >-
  This article features some of the slightly more obscure design patterns, such
  as responsive car-builder interfaces, mega dropdown navigation, content grids,
  maps and charts, as well as responsive art direction.
description: >-
  This article features some of the slightly more obscure design patterns, such
  as responsive car-builder interfaces, mega dropdown navigation, content grids,
  maps and charts, as well as responsive art direction.
categories:
  - Coding
  - UX
  - Responsive Design
  - UI
  - Design Patterns
  - Web Design
  - Best Practices
---
Design patterns often have a bad reputation. They are often considered to be quick, lazy, off-the-shelf solutions that are applied blindly without consideration of the context of a problem. Solutions such as the almighty off-canvas navigation, the floating label pattern or carousels for featured products are some of the prominent ones.

This article isn’t about these patterns, though. This article features some of the slightly more **obscure design patterns**, such as responsive car-builder interfaces, mega dropdown navigation, content grids, maps and charts, as well as responsive art direction. Please note that this **article isn’t technical**; it explores interesting UX patterns out in the wild, rather than code samples. Beware: You will not be able to unsee what you are about to see, and that’s probably a good thing.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Taking Pattern Libraries To The Next Level](https://www.smashingmagazine.com/taking-pattern-libraries-next-level/)
*   [Smashing Conferences and Workshops](https://www.smashingmagazine.com/smashing-workshops/)
*   [An In-Depth Overview Of Living Style Guide Tools](https://www.smashingmagazine.com/2015/04/an-in-depth-overview-of-living-style-guide-tools/)
*   [Boost Your Mobile E-Commerce Sales With Mobile Design Patterns](https://www.smashingmagazine.com/2012/12/boost-your-mobile-e-commerce-sales-with-mobile-design-patterns/)

When we design responsive websites today, in practice it makes more sense to move away from designing standalone pages towards designing flexible and sophisticated design systems. So, we focus on the components first, and then combine them to build larger components that eventually make up a page. It’s easier to comprehend the complexity of multi-screen experiences this way. But even then, we tend to see responsive design merely as a collection of slightly differently sized rectangles, with a slightly different layout, sometimes with slightly different content poured into them.

{{% feature-panel %}}

## Responsive Complexity Graph

I think it’s more accurate to envision responsive design as a complicated graph with dozens of dimensions, including typography, layout, [accessibility](https://www.smashingmagazine.com/2016/06/inclusive-design-patterns/), navigation and [performance](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/) (to name just a few). So, every single time we make a design decision, we are trying to plot just the right dot in just the right place across all of these dimensions to ensure that we create a resilient system that can appropriately scale up and down according to the user’s settings — and according to our intent. From this perspective, crafting responsive websites appears to be a slightly more daunting and fragile exercise, doesn’t it?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/633cfb87-6bf3-40f8-8749-76e8d8178637/responsive-graph.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/633cfb87-6bf3-40f8-8749-76e8d8178637/responsive-graph.png" alt="responsive design patterns" title="Smart Responsive Design Patterns, Or When Off-Canvas Isn't Good Enough" /></a><figcaption>With this responsive complexity graph, every time we make a design decision, we try to plot just the right dot in just the right place across all of these dimensions to ensure that we create a resilient system. (Image: <a href="https://en.wikipedia.org/wiki/Hypercube#/media/File:11-cube.svg">Wikipedia</a>) </figcaption></figure>

Actually, it really is a more daunting and fragile exercise, and this is why we keep going back and forth reconsidering our design and development decisions, trying to find better matches across all of the dimensions on the graph. And it’s also why design patterns can be very helpful: They reroute our decisions when we reach dead ends and simply don’t know what to do next; they help us save time by enabling us to iterate on solutions that have already proved to be helpful. It doesn’t mean that we apply the same patterns one to one in every project, but we could take them, review them and build on top of them, depending on the context. That’s where design patterns can be immensely valuable.

In this article, we’ll take a **close look at five responsive design patterns**, ranging from a car configurator to maps and infographics. Fasten your seatbelt: it’s going to be quite a journey.</p>

## Responsive Car-Builder Interface

Let’s imagine you get a call from a respectable and sizeable company that has a respectable and sizeable task for its website. As it turns out, a new feature had to be rolled out, you know, yesterday, and a big new announcement is coming up in a few weeks. The timing works for you, and the budget isn’t too shabby either.

Now, what if that company was BMW and you had to build a responsive car configurator that would allow users to build and purchase a car of their choice? You’d need to build in a selection of the car line, the interior and exterior, gears, a 360-degree view of the car, as well as a comparison view — for example, if a user wants to compare two cars at the same time. Obviously, the interface has to be responsive, too. Time is running out, so how would you approach this task?

{{< vimeo id="166812578" >}}

Whenever we have a complex component to design and build, we try two strategies to find a solution that might work well in the context. One option is to look at the **essence of the component** — its core and purpose, and then to design cross-screen experiences outwards. This means focusing on the content and features, without thinking about the layout and structure at first. For a component like a car builder, the core function is to combine different parts of the car into one piece by following a series of steps and choices.

Essentially, in its bare form, it could be a one-page layout with a few sections, each having a few radio buttons or toggles. We could use accordions to group sections logically and allow users to jump between sections easily. We would also need some sort of navigation to allow users to remodel some of the parts they’ve already selected. Also, whenever the user decides on one of the components of the car, this change should appear immediately.

Once we know what we are designing, we can prototype each section and arrange modules in a meaningful way throughout the entire spectrum of screens. We might need to change the fidelity, appearance and even functionality of those modules along the way as well. In other words, we would try to break down a complex component into more manageable smaller components, and **“repackage” content appropriately** for screen size — focusing on mobile first, extending the screen, adding a breakpoint and then changing the layout when things either break or could be enhanced for a better experience. We know the drill.</p>

<figure><a href="https://www.bmw.com.tr/tr/ssl/configurator.html#/7E01/P0A90,S02WS,S07R3,S05AC,S04UR,S06WB,S0552,S0255,S06U8,S0688,S03DS,S0258,S0416,S02VB,S06S1,S04HA,S04NM,S0420,S05DP,S08S3,S04ND,S05A1,S04NB,S06AP,S0609,S05AT,S06AM,S06AK,S03AG,S06AE,S0502,S06NW,S0322,S06AC,S0650,S0323/config/RIMS/"><img loading="lazy" decoding="async" srcset="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec326e8a-cfc4-4cd0-b7fc-ae47c4f2b093/bmw-builder-500px-opt.png 500w, https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a91da67-b1db-45a6-9477-abc781655b25/bmw-builder-opt.png 830w" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec326e8a-cfc4-4cd0-b7fc-ae47c4f2b093/bmw-builder-500px-opt.png" alt="BMW Configurator" /></a><figcaption><a href="https://www.bmw.com.tr/tr/ssl/configurator.html#/7E01/P0A90,S02WS,S07R3,S05AC,S04UR,S06WB,S0552,S0255,S06U8,S0688,S03DS,S0258,S0416,S02VB,S06S1,S04HA,S04NM,S0420,S05DP,S08S3,S04ND,S05A1,S04NB,S06AP,S0609,S05AT,S06AM,S06AK,S03AG,S06AE,S0502,S06NW,S0322,S06AC,S0650,S0323/config/RIMS/">BMW Configurator</a> uses both horizontal and vertical media queries to adjust the layout to better display interface controls, like the wheel selection. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a91da67-b1db-45a6-9477-abc781655b25/bmw-builder-opt.png">Large view.</a></figcaption>
</figure>

If we look at [BMW’s car configurator](https://www.bmw.com.tr/tr/ssl/configurator.html#/2A31/S07R3,S0423,S0431,S0520,S0521,S08S3,S0205,S0845,S0563,S02VB,S0249,S06S1,S05A4,S03AG,S0507,S06AE,S06AC,S0473/modelFinder/), that’s exactly what we can identify if we abstract away from the layout of the page. On a narrow screen, customers can select a model in a dropdown menu or by choosing the photo of the car line. On mobile, thumbs drive over 75% of user interactions, so adding the navigation and “next” button at the bottom of the screen makes sense. To allow users to quickly jump between sections of the configurator, we could also use an “overview” icon that prompts a full-screen overview of all steps in the car builder.

Instead of all steps being contained on one page, each step has a dedicated page. For every step, if we can’t display all options at once — for example, all colors or all kinds of wheels — we can provide a slider for users to swipe left or right to find the option they prefer. Obviously, we need to put the focus on the components of the car in every step of the process, so we could remove all subsidiary features and hints and hide them (perhaps in another dropdown menu).</p>

<picture><a href="https://www.bmw.com.tr/tr/ssl/configurator.html#/7E01/P0A90,S02WS,S07R3,S05AC,S04UR,S06WB,S0552,S0255,S06U8,S0688,S03DS,S0258,S0416,S02VB,S06S1,S04HA,S04NM,S0420,S05DP,S08S3,S04ND,S05A1,S04NB,S06AP,S0609,S05AT,S06AM,S06AK,S03AG,S06AE,S0502,S06NW,S0322,S06AC,S0650,S0323/config/RIMS/"><img loading="lazy" decoding="async" srcset="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac2835fd-df74-42bd-8f90-33154d7d9702/bmw-large-500px-opt.png 500w, https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ca91872-2717-4982-a9a2-27be8121bea4/bmw-large-opt.png 1500w" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac2835fd-df74-42bd-8f90-33154d7d9702/bmw-large-500px-opt.png" /></a><br /><em><a href="https://www.bmw.com.tr/tr/ssl/configurator.html#/7E01/P0A90,S02WS,S07R3,S05AC,S04UR,S06WB,S0552,S0255,S06U8,S0688,S03DS,S0258,S0416,S02VB,S06S1,S04HA,S04NM,S0420,S05DP,S08S3,S04ND,S05A1,S04NB,S06AP,S0609,S05AT,S06AM,S06AK,S03AG,S06AE,S0502,S06NW,S0322,S06AC,S0650,S0323/config/RIMS/">BMW Configurator</a> uses the available space to highlight the car; the wheel selection has shifted to the sidebar, compared to a narrower view above. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ca91872-2717-4982-a9a2-27be8121bea4/bmw-large-opt.png">Large view.</a></em></picture>

Once we get to larger screens, we can make better use of the available space. Instead of showing only the current step in the navigation at the bottom, we could display as many completed steps as possible and enhance the experience by adding more interface controls to make it easier to switch back to previous and next steps. The same goes for the slider panes for the color and wheels selection. With more space, we can line them out horizontally in a bigger size, without a slider at all.

On even larger screens, again, we can utilize the space by displaying the steps of the builder in a sidebar, and by flipping the horizontal panes into a vertical sidebar, so that the car itself gets more focus. This is where the designers of the BMW car builder decided to introduce a 360-degree view, as well as a feature to save the model for future reference. These features would be as beneficial for phone and tablet users, though.

An interesting but totally unrelated feature is the “Quick view” dropdown menu, which is displayed in addition to the regular menu in the top navigation bar. Displaying the most critical tasks separately yet prominently, in addition to the main navigation, might be a good idea. The website features many little highlights like this one, and in general it demonstrates good attention to detail in a responsive setting.

In the end, the car configurator isn’t as complicated as it would appear initially. [More](https://www.volvocars.com/intl/buy/shopping-tools/car-configurator#/packages/137/812-6SEVCC-90-x-en-52489519-EUR-207569358-x-1208937796-1207569382-1207569383-1207569423-0207569415-1207569422-0208946504-1207569369-1207569390-1207569430-1207569433-1208945154) [examples](https://rules.config.jaguar.com/jdx/en_gb/cj_jscwl01b/) are [out there](https://www.configurator.maserati.com/configurator/v2/?modelName=GHIBLI_330&currentCountry=78&lang=de&version=00), but only few of them are responsive, although [Ferrari’s car builder](https://car-configurator.ferrari.com/488gtb#config/1|c0023||20b0000|57000000|804||2a0000|60000000||4e000||||4001000|3f900) stands out from the crowd because of its features; for example, you can switch between a daylight and night view, as well as design two versions of a car at the same time and see the comparison live.</p>

{{< vimeo id="166812595" >}}

When it comes to a multi-step process, we can always break it down by displaying one section at a time, with the navigation conveniently placed at the bottom of the screen. We can use slider panes in case we can’t display all available options, and use extra navigation dropdown menus for extra details. We can then repackage these modules to better fill the available screen, from smaller to larger viewports. The result is a flexible, responsive car builder without bells and whistles, but with a straightforward and well-organized interface.</p>

## Responsive Mega DropDown Navigation

In one of his essays, Jason Fried, the creative mind behind Basecamp, [stated](https://signalvnoise.com/posts/3047-the-obvious-the-easy-and-the-possible) that “much of the tension in product development and interface design comes from trying to balance the obvious, the easy, and the possible.” It might sound like a very general observation, but in practice, it proves to be consistently valuable. In fact, whenever we attempt to [organize and design navigation](https://www.smashingmagazine.com/2014/09/efficiently-simplifying-navigation-interaction-design/), we try to group navigation items into exactly these three buckets. The way you group them defines how the navigation will be displayed throughout the website. Now, what do they stand for?

*   The **obvious** is all about features and navigation items that should always be within reach of the user. It reflects the essence of the website, and it is expensive because it requires pixels on the screen. Think about the most important sections or features of your website; if they belong to the obvious group, they should always remain visible.
*   The **easy** is all about features and sections used frequently but not all of the time. This is where we, as designers, have to balance the critical and non-critical, and these items are often hard to define. Usually, they are candidates for primary navigation items that are accessible with a click of a button or a dropdown menu toggle.
*   The **possible** is all about parts of the website that are sometimes or rarely used and usually do not require a spotlight. They should be accessible but not front and center, and probably hidden. These items usually work well in secondary navigation.

Now, what if we apply this separation of concerns to navigation? In simple cases, we could heavily prioritize the “obvious” (for example, search and the most trafficked sections of the website) and display it in all resolutions; we could reveal the “easy” navigation options with progressive disclosure (for example, with a “Menu” button or toggle); and we could provide access to the “possible” on a separate page, once users click on one of the subsections in “Menu,” rather than right in the navigation bar. More often than not, displaying the possible within the main navigation isn’t necessary or helpful. However, the decision for or against it would have to depend on hard data: metrics and usability tests.

[World Wildlife Fund](https://www.worldwildlife.org/) chose exactly this approach. Instead of displaying the same depth of navigation in all views, it chose to **prioritize the important ones** and show the rest only when required. In a large view, the upper navigation bar features seven sub-dropdown menus. On a small screen, you’d see only two links (“Donate” and “About”) displayed prominently, with a hamburger icon concealing a list with the main-level navigation areas, but not the links that are displayed on a large screen on hover. These areas are still accessible when the user drills down to the section page, but not right away.</p>

{{< vimeo id="166812605" >}}

In this case, the obvious could be “Donate” and “Adopt”; the easy could be the main categories in the hamburger menu; and the possible could be the areas accessible in each separate section.

You could ask yourself, Why do we hide these sections in the navigation menu if we could just display them with a set of accordions? Wouldn’t it be better if the user could jump to the section of their choice right away, with a few clicks right in the navigation? After all, if the navigation items are hidden, then we would expect lower engagement and traffic for them. That’s true, but with more focused navigation, we should expect higher engagement and traffic for the navigation items that are immediately visible. Besides, do you always want to present the rich content of a section as a list of plain links?

Still, in some situations, making such items immediately visible is useful, especially if many users return often to the website, or even to specific sections of the website. The data should dictate whether such items should go in the easy or possible bucket. Indeed, that’s where going back and forth usually is unavoidable.

This strategy could be applied to regular navigation as well as to **mega dropdown menus**. The latter are a common choice for any large website with dozens of sections, and it’s a good way to display a wide variety of products and sections at a glance. Well, it works well on the desktop at least, where there is enough space, but the view is quite narrow on mobile. What can we do there? We have a few options.

[The Guardian](https://www.theguardian.com/us) uses a combination of the mega dropdown menu and the “priority+” pattern to display as many items as possible in any given viewport, and then those items are put in a dropdown menu whenever they don’t fit anymore. On narrow screens, the layout is made linear, with all navigation options presented in a long list, the current selection being displayed at the very top.</p>

{{< vimeo id="166812599" >}}

The [Financial Times](https://next.ft.com/fastft) chose to transform its large detailed view into a tabbed menu. Instead of displaying all items in an almost endless list of links, each group acts as a tab, so sub-navigation is revealed upon tap or click.</p>

{{< vimeo id="166812597" >}}

The [Institute for Faith, Work & Economics](https://tifwe.org/about/) uses a similar technique for simpler navigation. It displays secondary navigation on hover on wide screens and uses the available space to display secondary navigation on the right side of the navigation panel on narrow screens. To indicate the secondary navigation, an arrow points to the right. That arrow [might need to be larger](https://www.viget.com/articles/testing-accordion-menu-designs-iconography), though.</p>

{{< vimeo id="166812603" >}}

[Food & Company](https://store.foodandcompany.co.jp/) rearranges the list of items based on the viewport. On large screens, images prominently drive users to the point of interest. On narrow screens, the images are replaced with text, and items are organized in a slightly more compact way.</p>

{{< vimeo id="166812598" >}}

[EuroVision](https://www.eurovision.tv/page/timeline) has a consistent grouping of navigation items and lets flexbox take care of filling in the space intelligently and automatically. The result isn’t always perfect, but it’s quite straightforward, without much hassle for the layout.</p>

{{< vimeo id="166812594" >}}

The simplest way to arrange a mega dropdown menu is by stacking the sections on top of each other in a simple linear view. However, users might benefit from a more compact view with grouped items and a tabbed view.

Adding nested accordions to reveal more than three sublevels of navigation at once usually could be a warning sign that something isn’t quite right and that perhaps the navigation could be simplified. Next time, start with a minimal amount of navigation, test usability with real users, and then add levels of navigation only when absolutely necessary. Not every off-canvas drawer has to be a collection of archived items that nobody really needs.

## Responsive Content Mosaics

Sometimes navigation takes slightly different forms, though. What if you want to build a prominent “feature” area that has to be displayed in a more appealing and interesting way on a landing page? Usually, you would want to stay away from perfect ol’ square boxes or circles, perfectly aligned in your perfect grid. How can we break the grid with an unusual arrangement an items, and how do we keep the items responsive?

An ordinary way of making, well, _anything_ responsive is by turning it into a vertical stack of sections. Indeed, [Sapporo](https://www.support-sapporo.or.jp/) does exactly that. Admittedly, the mosaic isn’t repeated multiple times throughout the page, so turning each section into a block seems to work well in this case.</p>

{{< vimeo id="166812602" >}}

This might not be the optimal solution for all websites, though. [Typekit](https://typekit.com/) features a complex content mosaic pattern, with blocks of content arranged in quite a unique shape. There are many blocks on the page, so lining them vertically would make for a very long page. Instead, Typekit designers chose to turn the content mosaic into a set of sliders in narrow views. Users can swipe to the left or right to explore the sections. It would have been helpful to add “previous” and “next” toggles in the upper-right corner of each slider, though, so that users can easily navigate between these sections.</p>

{{< vimeo id="166812604" >}}

Another way to solve the same problem would be to readjust the pattern to keep the metaphor but provide a slightly different view. The [FIFA World Football Museum](https://www.fifamuseum.com/) displays content blocks as spheres, inspired by the official ball used by FIFA. Each sphere is a hexagon, and the edges of the sphere are used as connectors between the blocks.</p>

{{< vimeo id="166812582" >}}

On large screens, the hexagons are larger and display content on hover. On narrow screens, the content is displayed right away, but not the entire content. With changes in the viewport, the hexagons are rearranged, but the metaphor remains.

[TPS Real Estate](https://www.tpsre.ru/en/) uses floating areas with masked videos to feature available properties. While the page is loading, the floor plans are used as [skeleton screens](https://www.lukew.com/ff/entry.asp?1797); as content becomes available, it gets populated into the areas, replacing the floor plans.</p>

{{< vimeo id="166812584" >}}

On larger screens, the content blocks grow on hover; on smaller screens, they turn into cards. Additionally, the user can choose between different views: the tiles view, the map view or the list view. Not all features are available on all screens, though: A 360-degree view doesn’t show up in narrow views but is displayed on wide screens (for obvious reasons — it requires Flash).

An obvious way to make a content mosaic responsive is by turning it into a list of block elements. Consider using a slider, or rearrange the tiles into different views, so that users can switch to the view of their preference.</p>

## Responsive Maps And Charts

In general, even advanced content mosaics aren’t as detailed as a large map or a non-trivial data visualization. In some scenarios, maps can be used as content filters — for example, to let users visually select a region of a city of their choice to buy a property. Obviously, an input field would make the input easier — but only if users know what they are looking for. What if you want to visually display a price range for the city areas using colors and text, so that the user can click on an area of interest and zoom into it?

The problem with a map is that, when scaled down, we often lose the almighty [44 × 44-pixel touch target](https://www.smashingmagazine.com/2012/02/finger-friendly-design-ideal-mobile-touchscreen-target-sizes/), which is required for comfortable and precise navigation. One idea would be to display a low-fidelity view of the map on narrow screens and progressively enhance it with more detail on larger screens.

Another option would be to accept less precise input and prompt users to specify input if it’s ambiguous. For example, the world map on the [Kremlin’s website](https://en.kremlin.ru) allows users to select multiple countries at once, and then prompts you with a data list asking for the country of interest. Additionally, traditional interface controls for zooming in and out are available as well, but selecting “Andorra” with them would be an exercise in patience, whereas selecting a region and choosing a country from a short list of options would be faster and easier. The website has a dozen other useful patterns, and we’ve featured them in a [case study on the Kremlin’s website](https://www.smashingmagazine.com/2015/08/from-russia-with-love-behind-the-scenes-of-the-kremlin-ru-responsive-redesign/) last year. Worth a read!

{{< vimeo id="166812596" >}}

This pattern can be useful for data visualization in general. Whenever a news website features elections, highlighting how the general public has voted in regions of a city, state or country, we could present a data list in both narrow and wide views, allowing users to select their area of interest.

Another interesting option to apply to maps would be to change the fidelity of the map entirely, moving away from a precise representation to a slightly more general one. That’s what CNN decided to do for its political “[Delegate Estimate](https://edition.cnn.com/election/primaries/candidates/hillary-clinton)” map. Instead of representing each state at an accurate size relative to others, CNN depicts each state with exactly the same width and height, with abbreviations and the delegates count represented in a state-by-state breakdown. It might not be precisely representative, but it does communicate the purpose of the map visually and works relatively well on mobile — probably better than a long tabular list of states aligned vertically would have.</p>

{{< vimeo id="166812581" >}}

## Responsive Art Direction

Changing the views and the fidelity of components for different screens is one of the cornerstones of responsive art direction. It’s common to assume that in web design, art direction is usually an exception for special pages, such as landing pages. That’s where we definitely want to ensure that a product is presented perfectly. So, changing the visuals to better match the screen is worth the effort.

Sometimes it’s not just preferable but necessary. [Emirates](https://www.emirates.com) airlines doesn’t have a responsive website; it uses a separate mobile website instead. But the content on both websites is remarkably similar, albeit quite different in terms of art direction.</p>

{{< vimeo id="166812592" >}}

The main images at the top of the screen differ depending on the language the user chooses to access the website. On an [international English version](https://www.emirates.com/lt/English/), the woman is looking from right to left, with a drink resembling a cocktail in her right hand. The metaphor is carried over to the mobile website as well.

In the [mobile Arabic version](https://mobile.emirates.com/qa/arabic/home.xhtml) of the website, the woman is looking from left to right, with a glass of orange juice in her left hand. The image is different altogether on the [desktop Arabic version](https://www.emirates.com/ae/arabic/).

Also interesting is that on the Emirates website, in a mobile view, critical items such as booking a flight and checking in aren’t highlighted with color or buttons, but are simply taller than other items — another little technique that could be applied in a variety of scenarios.

Another area where responsive art direction might be necessary is storytelling. As an integral part of its website, [Kobe Marathon QBB](https://kobe-marathon-qbb.com/) uses a series of cartoon strips to tell the story of a character running through Tokyo. The images change between narrow and wide screens, and so do the background images across the pages.</p>

{{< vimeo id="166812601" >}}

You could take the idea even further and allow users to zoom into a frame of a comic strip to view only one frame at a time, as [Al Jazeera](https://projects.aljazeera.com/2014/terms-of-service/#4) does. When the user taps on one of the frames in a mobile view, the frame gets larger and comes into focus, removing everything else. To move through the frames, users can then just swipe to the left or right.</p>

{{< vimeo id="166812576" >}}

Art direction is beneficial for landing pages, but it could be useful for multilingual projects or any website that involves some sort of storytelling.</p>

## Summary

Design patterns deserve more credit and attention than they usually receive. Looking into how our colleagues solve common problems helps us to avoid losing time and to get on the right track faster.

Complex interfaces can be broken down into simpler components and reshuffled to better fit various screens. Mega dropdown menus could be transformed into a set of tabs or into grouped navigation areas for narrow views. With complex content mosaics, we could turn content blocks into sliders and allow users to switch between views. For maps and complex infographics, users could select multiple countries at once and specify their selection in the second step. Responsive art direction isn’t easy, but it could dramatically improve landing pages and any project involving storytelling.

Next time, we’ll look into examples of more complex navigation, with filters, switchers between maps and list views, comparison tables, and responsive PDFs. Stay tuned, and if you happen to know of a responsive design pattern worth highlighting, please share it on Twitter or in the comments below. And if you're looking for a few more patterns to use, we've got a little [responsive design book](https://www.smashingmagazine.com/2015/03/real-life-responsive-web-design-smashing-book-5/) that you might find useful.

{{< signature "al" >}}


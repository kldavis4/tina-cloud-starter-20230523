---
title: 'Designing Navigation for Mobile: Design Patterns and Best Practices'
slug: navigation-design-mobile-ux
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4f71534-99d6-4c67-866b-808017f4c3a5/navigation-design-mobile-ux.jpg
date: 2022-11-02T14:00:00.000Z
summary: >-
  When designing navigation on mobile, we don’t have to rely on slide-in-menus or nested accordions. We can also use the curtain and billboard design patterns, and show multiple levels of navigation at once.
description: >-
  When designing navigation on mobile, we don’t have to rely on slide-in-menus or nested accordions. We can also use the curtain design pattern, and show multiple levels of navigation at once.
categories:
  - Navigation
  - Design Patterns
  - UX
---

When it comes to **complex navigation on mobile**, we often think about hamburger menus, full-page overlays, animated slide-in-menus, and a wide range of nested accordions. Not all of these options perform well, and there are some alternative design patterns that are worth exploring. Let’s dive in!

<style>.course-intro{--shadow-color:206deg 31% 60%;background-color:#eaf6ff;border:1px solid #ecf4ff;box-shadow:0 .5px .6px hsl(var(--shadow-color) / .36),0 1.7px 1.9px -.8px hsl(var(--shadow-color) / .36),0 4.2px 4.7px -1.7px hsl(var(--shadow-color) / .36),.1px 10.3px 11.6px -2.5px hsl(var(--shadow-color) / .36);border-radius:11px;padding:1.35rem 1.65rem}@media (prefers-color-scheme:dark){.course-intro{--shadow-color:199deg 63% 6%;border-color:var(--block-separator-color,#244654);background-color:var(--accent-box-color,#19313c)}}</style>
  
<p class="course-intro"><em>Pssst!</em> This article is <strong>part of our ongoing series</strong> on <a href="/category/design-patterns">design patterns</a>. It’s also a part of <a style="font-weight:700" href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>&nbsp;🍣 and is available in the <a href="https://smashingconf.com/online-workshops/workshops/interface-design-course-vitaly-friedman/">Live Interface Design Training</a>&nbsp;🍕 as well.</p>

## 1. Avoid Too Many Signposts In Your Navigation

One of the most common strategies for navigation on mobile is to use a good ol’ [accordion](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/). In fact, **accordions work very well** for multiple levels of navigation and are usually better than slide-in menus. However, since we open and collapse menus, we also need to indicate it with an icon. This often results in **too many signs** pulling user’s attention in too many directions.

{{< rimg href="https://www.vodafone.de" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35fd061c-5589-4045-8de4-d7c5bae0839a/15-vodafone.jpg" width="800" height="576" sizes="100vw" caption="" alt="Three different mobile views of Vodafone’s website using three examples of three icons being used to navigate the website" >}}

In the example above, [Vodafone](https://www.vodafone.de) uses **3 different icons**, pointing either to the bottom (accordion collapsed), to the top (accordion open), or to the right. The latter indicates that the selection is a *link*, driving users to a category page. This is, however, not immediately obvious.

{{< rimg href="https://www.vodafone.de"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd7383bf-d083-4362-98b2-350ddad75c8c/vodafone-mock-up.jpg" width="800" height="576" sizes="100vw" caption="" alt="Two mobile views of the Vodafone website showing underlined links within accordions" >}}

An alternative &mdash; and perhaps a slightly more obvious way &mdash; is by **adding a link underline** to links and removing the icons next to them altogether. As a side effect, if we eventually have to mix collapsible menus and links to categories, it’s perhaps a bit more obvious which is which.

{{< rimg breakout="true" href="https://www.swisscom.ch/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/212a87d1-425b-484a-ad43-3f57c868637f/11-swisscom.jpg" width="800" height="576" sizes="100vw" caption="" alt="Three different views of the Swisscom website shown on mobile" >}}

In general, pointing users in too many directions is often unnecessary. It’s quite likely that you’ll be able to achieve better results with **just two icons**, indicating whether an accordion is open or not. That’s how it’s done on [Swisscom](https://www.swisscom.ch/) (pictured above), for example.

{{< rimg breakout="true" href="https://posturinn.is/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d40221d-6c67-4728-b1b4-0ca5a4c78a95/01-posturinn.jpg" width="800" height="576" sizes="100vw" caption="" alt="Three views showing one icon being used on the website of the Icelandic Postal Service" >}}

Alternatively, [Icelandic Postal Service](https://posturinn.is) uses **just one single icon**, and to indicate expansion of the accordion, changes the color of the heading of the section. This seems to be working fairly well, too.

It’s a good idea to avoid too many icons guiding users in too many directions. If we can get away without them, it’s a good idea to test what happens if we do.

{{% feature-panel %}}

## 2. Don’t Overload Your Navigation With Multiple Actions

Sometimes navigation menus combine **two different functions** in one single navigation bar. For example, what if you have **categories** that you want to link to directly, but then you also want to allow for quick jumps into **sub-menu items**?

Usually, this means adding two different actions to the same navigation bar. A tap on the title of the category would lead to the category; a tap on the icon would open an accordion or prompt a separate view. And to make this difference a bit more obvious, we often add a **vertical separator**. Unfortunately, in practice, that doesn't work too well.

{{< rimg breakout="true" href="https://www.tivoli.dk/en/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10ccbebd-e482-4ccb-82bb-efa5f5852d01/tivoli-separator.png" width="800" height="576" sizes="100vw" caption="" alt="Tivoli overloads the navigation bar with multiple actions - too often it doesn’t work well" >}}

In the example above on [Tivoli Gardens Copenhagen](https://www.tivoli.dk/en/), each section title is linked to a standalone category page. A tap on the icon on the right, however, opens a separate sub-navigation. Indeed, a vertical separator does help to distinguish between the two actions, but it still **causes plenty of mistakes**.

Sometimes users want to just *assess* the navigation at a glance, and they aren’t yet committing to going to a dedicated page. Yet here they are, being **pushed towards a page** just when they aren’t ready to go there at all. And once they do, they then have to return back to the previous page and start all over again. Ideally, we’d avoid this problem altogether.

{{< rimg breakout="true" href="https://www.mammut.com/eu/en" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47e6eb93-5dbe-46ed-853f-33c41b95ddda/04-mammut.jpg" width="800" height="576" sizes="100vw" caption="" alt="Three screenshots of the Mammut website as seen on mobile" >}}

On [Mammut](https://www.mammut.com/eu/en), the **entire navigation bar** drives the user to the second level of navigation. Their users can move to discover all items within the category or jump into a sub-category. Problems solved. Rather than overloading the navigation bar with separators and separate actions, we can help users **move forward confidently and comfortably** and prevent mistakes altogether. The next action is always just a tap away.

Always consider adding a link to the category page within the expanded accordion or in a separate view, and assign only a singular function to the entire bar &mdash; opening that view. 

## 3. Use The Billboard Pattern For Top Tasks

Not every navigation item is equally important. Some items are more frequently used, and they might deserve a little bit more spotlight in your navigation. In fact, if some items are more important than others, we can use the **billboard pattern** and display them more prominently above the navigation.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c2e6130-e0be-4f69-af57-c54dbd70a981/billboard-pattern.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c2e6130-e0be-4f69-af57-c54dbd70a981/billboard-pattern.png" width="800" height="478" sizes="100vw" caption="" alt="Mobile views of three websites: Otto, Korea Post and Deutsche Post" >}}

In the examples above &mdash; [Otto](https://www.otto.de), [Korea Post](https://www.koreapost.go.kr/) and [Deutsche Post](https://deutschepost.de/) &mdash; we display the most important topics or features more prominently while the rest of the navigation is available, but gets a slightly less prominent presence.

{{< rimg breakout="true" href="https://www.otto.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21bcdebe-9d83-4ab5-aa4a-680381302cb2/otto-billboard-pattern.png" width="800" height="473" sizes="100vw" caption="" alt="Viewing the Otto.de website on mobile" >}}

## 4. Nested Accordions Work For Expert Users

Just like we might have too many icons, we might end up with too many nested levels of navigation, neatly packaged within **nested accordions**. For complex sites, it seems like one of the few options to present a huge amount of navigation available on the site. In fact, we could argue that by allowing users to jump from any page to any page on the 4th or even 5th level of navigation, we can **massively speed them** up in their journeys.

{{< rimg breakout="true" href="https://www.ecb.europa.eu/home/html/index.en.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52c77133-b31c-4574-add4-fa8c2f8e5b2b/08-european-central-bank.jpg" width="800" height="576" sizes="100vw" caption="" alt="Three mobile versions of the European Central Bank website" >}}

Surprisingly enough, this seems to be right. **Expert users** typically don’t have massive usability issues with multiple nested accordions. However, **infrequent users** often struggle to find the information that they need because they don’t understand how the information is organized.

In complex environments, navigation usually **mirrors the way the organization is structured internally**, and without that prior knowledge finding the right route to the right page is difficult at best. In that case, once a user is looking for something very specific, they seem to use search rather than traversing the navigation tree up and down. This becomes apparent especially when the contrast between levels isn’t obvious, such as on [WHO](https://www.who.int/), for example (pictured below).

{{< rimg breakout="true" href="https://www.who.int/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ff18c03-1a35-49b7-9fae-980c2c4d4ab3/07-wto.jpg" width="800" height="576" sizes="100vw" caption="" alt="Taking a closer look at the website of the World Trade Organization" >}}

If we need to include multiple levels of navigation within nested accordions, it’s a good idea to sparkle just a tiny bit of typographic and visual contrast to the menu so that **every level of navigation is clearly distinct**, and it’s also obvious when links to actual pages start appearing. Compare the quick mock-up below. 

{{< rimg breakout="true" href="https://www.who.int/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd2eadda-d19f-41fa-b48e-f501cee5e3fc/21-wto-optimized.jpg" width="800" height="576" sizes="100vw" caption="" alt="A mock-up of the World Trade Organization website" >}}

Another way to indicate multiple levels of nesting is by **adding different types of icons** to make it more obvious where users currently are. This is how it’s done on the [Stockholm University website](https://www.su.se/cmlink/stockholm-university). Personally, I wasn’t able to verify how well this design pattern works, but when combined with better typographic contrast, this might be performing better and is definitely worth testing.

{{< rimg breakout="true" href="https://www.su.se/cmlink/stockholm-university" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22bf791c-2ec4-42d2-b6e5-4bb5b0c3fd3a/18-stockholm-university.jpg" width="800" height="576" sizes="100vw" caption="" alt="Three mobile views of the Stockholm University website" >}}

[DOT](https://dinoffentligetransport.dk/), a public transportation website from Denmark, uses the `+` icon across multiple levels for their nested accordions. While the chevron is positioned on the left, the `+` are always positioned on the right. Thus, they display **four levels of navigation** with nested accordions. Perhaps it’s a bit too much navigation, but it seems to be working fairly well.

{{< rimg breakout="true" href="https://dinoffentligetransport.dk/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15569baf-1566-4344-b721-6c945f0bf4f8/dot-nested-accordions.png" width="800" height="478" sizes="100vw" caption="" alt="Mobile views of three websites: Otto, Korea Post and Deutsche Post" >}}


On the other hand, it might not be needed at all. [Allianz](https://allianz.de/) gets away with using a single icon (chevron up and down), but with **clearly different designs** for every navigation level. The first level is highlighted with white text on a blue background; the second level is designed in bold; and the third level is plain text (which could, of course, be links, too).

Plus, instead of showing all items at the same time, only **four most important ones** are displayed at first, and the others are available on a separate page. This a great example worth keeping in mind.

{{< rimg breakout="true" href="https://allianz.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb1b6ecc-c2be-4ca8-855c-d9a0e980d4d5/12-allianz.jpg" width="800" height="576" sizes="100vw" caption="" alt="Mobile view comparisons of the Allianz website" >}}

**Nested accordions** can work with enough contrast between each level. However, if you have more than three levels of navigation, making it work with a bit of indentation and various typographic styles will become quite difficult.

{{% feature-panel id="vitaly-friedman" %}}

## 5. Slide-In-Menus Don’t Perform Very Well

Admittedly, many navigation menus on mobile aren’t accordions. Because each navigation section might contain dozens and dozens of sub-navigation items, it’s common to see the so-called **slide-in menus**, with navigation items sliding in horizontally and presenting users with a comprehensive menu of all options available on that level.

With that pattern, **quick jumps** from one level to another are impossible, as users always have to go back to the previous level to move forward.

{{< rimg breakout="true" href="https://www.unilever.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a24c7fe-aa00-46c5-9260-ddcc40bf28a4/09-unilever.jpg" width="800" height="576" sizes="100vw" caption="" alt="Three mobile views of the Unilever website showing one level of navigation at a time" >}}

[Unilever](https://www.unilever.com) displays **only one level of navigation at a time**. As users navigate further down the rabbit hole, they are presented with only one level at a time. This does work well to fit all the items and all the levels that an organization might ever need. However, if a user isn’t quite sure where to go, the discovery of content tends to be slower. Also, it’s not necessarily clear where the “Back” button will go to.

{{< rimg breakout="true" href="https://deutschepost.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3992eeba-9fba-4b61-8b99-b624a01ba7f4/02-deutsche-post.jpg" width="800" height="576" sizes="100vw" caption="" alt="Screenshots of the navigation menu used on the Deutsche Post website" >}}

If we do use a slide-in menu, it’s a good idea to **replace a generic “Back” button** with a more contextual label, explaining to users where exactly they will be returning to. [Deutsche Post](https://deutschepost.de/) (pictured above) does just that. Also, notice that the main page of the menu features some of the top tasks on the site, in additionally to the slide-in menu.

{{< rimg breakout="true" href="https://www.nejm.org/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bef334f-2bfa-49b1-8060-51fda008060c/13-new-england-journal-of-medicine.jpg" width="800" height="576" sizes="100vw" caption="" alt="The New England Journal of Medicine" >}}

Additionally, [The New England Journal of Medicine](https://www.nejm.org/) adds some typographic contrast to each section, so it’s a bit more obvious right away what would open up another section and what is a link driving to a new page. In fact, we can go quite far by just **making links more obvious** yet again, as displayed in the example of [ADAC](https://www.adac.de/) below.

{{< rimg breakout="true" href="https://www.adac.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f96101c2-26fa-490d-bb40-162c15be8b36/22-adac-optimized.jpg" width="800" height="576" sizes="100vw" caption="" alt="Making links obvious and more visible on the ADAC website" >}}

It’s worth noting that **animated slide-ins can be quite disorienting**, distracting, and annoying for people who use the navigation a lot. Add to that the slow speed of content discovery, a few too many icons, and a bit too little contrast between the items, and you have a recipe for disaster.

A slide-in menu is an option but **rarely the best one**. It surely doesn’t perform as well as accordions where jumps between levels are faster and there is rarely a need to go back. However, accordions aren’t the only option we have &mdash; especially when we want to help users **navigate between levels faster**, not slower.

## 6. The Navigation Stack Works For Quick Jumps

As we move users from one level to another, we also need to provide a way for them to move back. But instead of just displaying a "Back" button, we can stack all the previous sections like a breadcrumb under each other. And so we get a **navigation stack**.

{{< rimg breakout="true" href="https://www.coolblue.nl/en/mobile-phones/smartphones" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b57180fa-595b-4857-b513-a345912f0201/cool-blue-stacking.png" width="800" height="473" sizes="100vw" caption="" alt="Viewing the Coolblue.nl website on mobile" >}}

On [Coolblue](https://www.coolblue.nl/en/mobile-phones/smartphones), a Dutch retailer, as users keep exploring deeper levels of navigation, they can always return all the way to the previous levels that they’ve been coming from. This allows for **faster jumps between levels**, and is definitely a good idea when driving users from one-page overlay to another.

## 7. Use Curtain Pattern To Show Multiple Levels of Navigation

It shouldn’t be a big revelation that the speed of navigation is at its maximum when we display navigation options right away. This is why we see **large buttons** appearing as large clickable cards, filters, and bottom sheets. However, how do we use it in our navigation menus which barely have any place anyway?

{{< rimg breakout="true" href="https://www.lcfc.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9748d90c-dfbf-4d0c-83c6-442240efccaa/01-lcfc-vertical-split-navigation.jpg" width="800" height="576" sizes="100vw" caption="<a href='https://www.lcfc.com/'>LCFC</a> split the page into two parts, one for each level of navigation." alt="LCFC split the page into two parts, one for each level of navigation" >}}

We could make better use of the available space. For example, what if **split the screen vertically**, showing one level of navigation on each? Very much like a curtain that we’d pull to one side of a window. That’s what <a href="https://www.lcfc.com/">LCFC</a> (pictured above) does. To move between levels, we don’t need to close any menus or return back at all &mdash; instead, we click on large areas, move forward, and explore.

And what if you **need slightly more space** for your lengthy navigation labels? Well, the labels could **wrap onto multiple lines**, or we could reduce the width by replacing text labels with icons (as long as they are unambiguous). It might not work for every project, but it seems to work for [Playstation](https://www.playstation.com/en-us/) (pictured below).

{{< rimg breakout="true" href="https://www.playstation.com/en-us/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00619f8d-ced5-4aa1-bd38-66ccf64f3fa9/02-curtain-split-navigation-playstation.jpg" width="800" height="576" sizes="100vw" caption="" alt="The Playstation website shows two levels of navigation at the same time" >}}

The entire first level of navigation collapses into <em>tabs</em>; yet moving from one level to the other doesn’t require any jumps back. You might be wondering what the three vertical lines represent &mdash; ideally, one could drag away the pane, but it doesn’t seem to be working as expected, unfortunately.

{{< rimg breakout="true" href="https://espn.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef2e3c73-80a0-410a-929a-4d28a4c7d4f6/espn-curtain-navigation.png" width="800" height="576" sizes="100vw" caption="" alt="The ESPN website shows two levels of navigation at the same time" >}}

[ESPN](https://espn.com/) uses a very similar approach but reduces the amount of space for the first level to the minimum. It could be a little bit larger to prevent mistaps, but the idea is pretty much the same: showing **two levels of navigation at the same time**.

We could use the same approach in other contexts, such as filtering. We display **all filter attributes on the left**, and allow users to choose the specific values for these filters in the second vertical pane. That’s what the filtering experience looks like on <a href="https://www.myntra.com">Myntra</a>, an Indian eCommerce retailer pictured below.

{{< rimg breakout="true" href="https://www.myntra.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b367d3d9-40ea-451c-b599-1bf08e62071c/03-myntra-filter-selection-triple-view.jpg" width="800" height="576" sizes="100vw" caption="" alt="No slide-in-navigation in sight on the Myntra website" >}}

If some filters don’t fit in the right pane, users can scroll to explore more or even **search for a specific filter** in the selection. Of course, the "Apply" button has to stay floating. It would be lovely to see the total number of results on that button, too.

We could take it even further, though. For example, sometimes users need to select filters that are relevant to them and define their values in the next step. In that case, we **group all filters into a few categories** (or even sub-categories), and then present all of the categories and filters as sub-categories side-by-side.

{{< rimg breakout="true" href="https://markets.ft.com/data/equities/results" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4b31635-2b04-4f21-b99f-0d15c5c90e66/04-ft-filter-constructor.jpg" width="800" height="576" sizes="100vw" caption="" alt="Showing the FT Screener website on mobile with two panes, i.e. one for groups and one for specific filters." >}}

With <a href="https://markets.ft.com/data/equities/results">FT Screener</a>, for example, users can add or change criteria by exploring multiple levels at the same time &mdash; both the labels for groups and the filters living within those groups. Once a filter has been chosen, it’s added to the overview on the top. That’s a **simple filter constructor** for sophisticated filtering on mobile.

The vertical split could be used to quickly select one important present or make a single choice. That would be the case for a language selector, for example. We could organize all supported countries and languages as cards or accordions, but they could also work as **vertical tabs**, as it’s done in the footer of <a href="https://www.oracle.com/">Oracle</a>.

{{< rimg breakout="true" href="https://www.oracle.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7240484-4a6b-419a-a8da-0718d1261197/05-oracle-country-selector.jpg" width="800" height="576" sizes="100vw" caption="" alt="The Oracle website has a vertical-split menu for the country/region selection in the footer" >}}

This way, we display **only options that are relevant to users**. They never have to go to irrelevant sections or pages since they get a preview and can navigate away from it quickly, should they wish to do so.

In general, the curtain pattern works well with a quite **flat content architecture**, but is difficult to manage with three or more levels. It shows its strengths when the speed of navigation matters and when users are likely to jump between sections a lot. 

It’s *way* faster than slide-in-menus but less flexible than accordions. Still, a great lil’ helper to keep in mind to **make better use of available space** on mobile.

## 8. You Might Not Need 3+ Levels of Navigation

The curtain pattern works well for two levels of navigation, but you might have many more levels than that. In that case, it might be a good idea to test if it actually has to be this way. What if you **show only two or three levels** via your menu drawer, but then the rest would be available on standalone pages?

{{< rimg breakout="true" href="https://uantwerpen.be/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf8a342c-d254-48e6-b5cc-cbe54bf848e3/16-antwerp-university.jpg" width="800" height="576" sizes="100vw" caption="" alt="The University of Antwerp" >}}

[The University of Antwerp](https://uantwerpen.be/) gets away with just one level of navigation on mobile. All the sub-section exist on standalone pages as cards. In fact, there are dozens of links on each page, but as long as the **navigation is obvious**, this might be just what you need.

{{< rimg breakout="true" href="https://www.gov.uk/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3483b7d-15f1-4296-a000-600107a5d1ca/17-gov-uk.jpg" width="800" height="576" sizes="100vw" caption="" alt="Gov.uk" >}}

[Gov.uk](https://www.gov.uk) isn’t a particularly small website, but it features **only two main sections** with plenty of subsections in its navigation on mobile. However, no third or fourth-level navigation is accessible from the menu drawer. Everything else is accessible via links and cards on separate pages.

{{< rimg breakout="true" href="https://www.koreapost.go.kr/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db36c09a-7d22-490e-ad5e-ffe8c32654f5/20-korean-post.jpg" width="800" height="576" sizes="100vw" caption="" alt="Korea Post" >}}

[Korea Post](https://www.koreapost.go.kr/) follows along with an interesting twist to that idea. On tap in the menu, it shows all items living on the second level, but also **automatically shows the options from the third level**, too. Additionally, breadcrumbs include drop-downs allowing users to jump quickly between the siblings of each level. You can find out more about that pattern (*sideways breadcrumbs*) in [Designing A Perfect Breadcrumbs UX](https://www.smashingmagazine.com/2022/04/breadcrumbs-ux-design/).

Do you need to display more than two levels of navigation? Perhaps it is indeed necessary, but chances are high that it isn’t. So perhaps it’s worth testing a design that features **only two levels**. Additionally, we can add another feature to it to make navigation even faster.

{{% feature-panel %}}

## 9. Query User’s Intent With Navigation Queries

In addition to search and navigation, we could study some of the most frequently visited pages or some of the most popular tasks, and show them directly, as we saw in the [Deutsche Post](https://deutschepost.de/) example earlier above.

We could also add [navigation queries](https://www.smashingmagazine.com/2022/04/designing-better-navigation-ux-queries/) to **ask users about their intent**, and allow them to choose a topic relevant to them. Think about it as a mini-search engine for your navigation, designed as a seamless autocomplete experience. This would give users guidance toward the goal and help them navigate more reliably.

{{< rimg href="https://www.cosmosdirekt.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1df9fbaa-2e19-4b04-878c-8848cd815c6b/task-cosmos-direk.png" width="800" height="576" sizes="100vw" caption="" alt="Examples of the navigation being used on the Cosmos Direkt website as seen on mobile" >}}

[Cosmos Direkt](https://www.cosmosdirekt.de/), a German insurance company, features a &lt;select&gt;-menu that allows users to select a particular task that they’d like to perform on the site. This type of navigation exists additionally to search and classic navigation menu, but **increases the speed to relevance** significantly.

## Wrapping Up

Just as a quick summary, here are a few things to keep in mind when dealing with complex multi-level navigation:

- **[Accordions](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/) work well**, and for expert users, they work even if they are nested.
- **Remove icons that you don’t need**. Avoid icons pointing in more than two directions.
- **Use the billboard pattern** to highlight top tasks that users want to complete on the site.
- For nested navigation levels, make sure that **each level is distinct** (indentation + type styles).
- Whenever possible, **make links obvious** by underlining them.
- Slide-in-menus **don’t perform very well**; they are slow and distracting. Accordions are likely to perform better.
- **Keep the navigation stack** of the levels that users browsed through to allow for quick jumps.
- **Curtain navigation** is fast! Consider using it when you have two, or at most three, levels of navigation.
- Perhaps we don’t need to show all levels of navigation and instead can bring users to the relevant page to navigate from there.

<!-- 
{{< rimg href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/299002ce-ea0b-479d-8ca9-b9dd77843b29/03-adac.jpg" width="800" height="576" sizes="100vw" caption="" alt="" >}}

{{< rimg href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47e6eb93-5dbe-46ed-853f-33c41b95ddda/04-mammut.jpg" width="800" height="576" sizes="100vw" caption="" alt="" >}}

{{< rimg href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a3e3568-ec14-4527-a015-094ca53f3dc6/05-frans-hals-musem.jpg" width="800" height="576" sizes="100vw" caption="" alt="" >}}

{{< rimg href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25c9ad03-f219-404c-817f-a76368bb5cc5/10-eda.jpg" width="800" height="576" sizes="100vw" caption="" alt="" >}}

{{< rimg href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e29c9cfe-3735-4945-b4d9-f78612b8eb0c/14-the-royal-institution.jpg" width="800" height="576" sizes="100vw" caption="" alt="" >}}

{{< rimg href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/650c7f5a-ced1-45ec-a1fd-99c60debbedf/19-austria-postal-service.jpg" width="800" height="576" sizes="100vw" caption="" alt="" >}} -->


## Meet “Smart Interface Design Patterns”

If you are interested in similar insights around UX, take a look at [**Smart Interface Design Patterns**](https://smart-interface-design-patterns.com/), our shiny new **9h-video course** with 100s of practical examples from real-life projects. Design patterns and guidelines on everything from mega-dropdowns to complex enterprise tables &mdash; with five new segments added every year. *Just sayin’!* [Check a free preview](https://www.youtube.com/watch?v=aSP5oR9g-ss).

<figure style="margin-bottom: 1rem"><a href="https://smart-interface-design-patterns.com/"><img style="border-radius: 11px" decoding="async" fetchpriority="low" width="950" height="492" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 400w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 800w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1200w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1600w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg" sizes="100vw" alt="Smart Interface Design Patterns"></a><figcaption class="op-vertical-bottom">Meet <a href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>, our new video course on interface design &amp; UX.</figcaption></figure>

<div class="btn--lined btn--lined--white-border" style="margin-top: 0.75em; margin-bottom: 0.75em"><a class="btn btn--large btn--green btn--text-shadow" href="https://smart-interface-design-patterns.com/">Jump to the video course&nbsp;&rarr;</a></div>

<p class="ticket-price__desc" style="font-size: .8em!important; text-align: center; line-height: 1.5; margin-top: 0; display: block;">100 design patterns &amp; real-life 
examples.<br>9h-video course + live UX training. <a href="https://www.youtube.com/watch?v=aSP5oR9g-ss">Free preview</a>.

## Related UX Articles

- [Designing Perfect Breadcrumbs UX](https://www.smashingmagazine.com/2022/04/breadcrumbs-ux-design/)
- [Boosting Navigation UX With Navigation Queries](https://www.smashingmagazine.com/2022/04/designing-better-navigation-ux-queries/)
- [Designing Better Error Messages UX](https://www.smashingmagazine.com/2022/08/error-messages-ux-design/)
- [Rethinking Authenticaiton UX](https://www.smashingmagazine.com/2022/08/authentication-ux-design-guidelines/)
- [Disabled Buttons UX](https://www.smashingmagazine.com/2021/08/frustrating-design-patterns-disabled-buttons/)
- [Designing A Perfect Infinite Scroll](https://www.smashingmagazine.com/2022/03/designing-better-infinite-scroll/)
- [Design Patterns and UX on SmashingMag](https://www.smashingmagazine.com/category/ux/)

{{< signature "vf, il" >}}

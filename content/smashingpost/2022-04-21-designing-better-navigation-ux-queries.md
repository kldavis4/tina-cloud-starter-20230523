---
title: 'Say Goodbye To Frustrating Navigation, With Navigation Queries'
slug: designing-better-navigation-ux-queries
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b9b874c-9208-47da-b69b-b46d90988b11/designing-better-navigation-ux-queries.jpg
date: 2022-04-21T10:00:00.000Z
summary: >-
  In UX, we can use navigation queries, evaluation journeys, A-Z index and tap-ahead autocomplete to help users get where they want to be, faster. Let’s find out how.
description: >-
  In UX, we can use navigation queries, evaluation journeys, A-Z index and tap-ahead autocomplete to help users get where they want to be, faster. Let’s find out how.
categories:
  - UX
  - Navigation
  - Design Patterns
---

When designing interfaces, we often focus on the usual suspects. How do we design better [mega-menus](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-mega-dropdown-hover-menus/) and [carousels](https://www.smashingmagazine.com/2022/04/designing-better-carousel-ux/)? How do we support users with better [breadcrumbs](https://www.smashingmagazine.com/2022/04/breadcrumbs-ux-design/)? How do we better display our sidebar navigation? And how do we provide a better search experience, along with decent filtering, sorting and search?

While all these features for navigation are absolutely important and useful, there are also a few other navigation patterns that are often forgotten or dismissed. We can think of them as **navigation shortcuts**, helping users get where they want to go, faster &mdash; without having to use traditional navigation at all.

As it turns out, sometimes they are **much more effective**, especially on large sites with thousands of pages, many of which have been gathering dust over the years.

<p style="background-color: #e8f5ff;
border: 1px solid #dbeaff; border-radius: 11px; padding: 1.35rem 1.65rem;">This article is part of our ongoing series on <a href="/category/design-patterns">design patterns</a>. It’s also a part of the upcoming <a style="font-weight: bold" href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-ux/">4-weeks live UX training</a>&nbsp;🍣 and will be in our recently released <a href="https://smart-interface-design-patterns.com/">video course</a> soon.</p>

## Designing For Exploration

Our typical experience on the web is somewhat unusual. We visit websites with all kinds of various intents, yet to address that intent, we usually have to translate it into a meaningful combination of keywords, clicks, taps and selections. We rarely get the answers we need immediately; instead, **we discover the answers** in a long-winded journey between pages and sub-navigation items.

{{< rimg href="https://twitter.com/marcinignac/status/1400806180797231104" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc3aedc3-44d4-4d05-8c93-909d6c417454/1-better-navigation-design-shortcuts.png" width="800" height="450" sizes="100vw" caption="How do you find stuff that is not in your top 10 results of mini snippets? According to <a href='https://twitter.com/marcinignac/status/1400806180797231104'>Marcin Ignac</a>, we need more explorative interfaces taking advantage of context and association. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc3aedc3-44d4-4d05-8c93-909d6c417454/1-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="An illustration of how searching is done versus exploring" >}}

Gerry McGovern once [rightfully suggested](https://gerrymcgovern.com/books/world-wide-waste/) that more people have been on top of Mount Everest than have been to the 10th page of Google’s search results. This is probably true, yet usually, our interfaces provide long lists of options and are **rarely designed for exploration**. We surface a multitude of options rather than taking advantage of context and association, as Marcin Ignac [has put it recently](https://twitter.com/marcinignac/status/1400806180797231104/photo/1).

In fact, we leave users on their own with a few signposts along the way. They need to survey the landscape, jump between menu items, iterate on search queries, and scout tags and footer links.

It works, but it’s slow. To minimize the **distance between intent and action**, we can query users about their intent and then assist users in their journey. That's when navigation queries come into play.

## Navigation Queries

The idea behind navigation queries is not new. We’ve seen all kinds of variations of Madlib pattern, [natural language forms](https://www.jroehm.com/2014/01/26/ui-pattern-natural-language-form/) and [chatbots](https://www.nngroup.com/articles/chatbots/), all of which present a human-friendly way to **specify intent** without having to use input fields or navigation menus. Usually, we’d see the entire form presented as a sentence in front of us, with a few drop-downs allowing us to specify what is it exactly what we are looking for. However, we can also apply this concept more dynamically.

{{< rimg href="https://twitter.com/marcinignac/status/1400806180797231104" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47a08e44-2c84-4800-ba33-e7c59a57b446/23-better-navigation-design-shortcuts.png" width="800" height="450" sizes="100vw" caption="<a href='https://www.ao.de/'>AO.de</a> provides a shortcut for users to jump from the homepage to a specific product of interest. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47a08e44-2c84-4800-ba33-e7c59a57b446/23-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A screenshot of the Commonbond.co website" >}}

The idea, then, is to create a **“query constructor”** for the user’s intent. In our interface, we could show options to choose from and based on one answer, provide further options, all the way to the point where we guide a user to the page of interest. And that’s what we would call a *navigation query*.


On [AO.de](https://www.ao.de/), the front page is dedicated to **query the type of device** that the customers are interested in. Once it’s selected, another selection appears, allowing users to specify one of the filters that could be applied to their query. And depending on that input, the third filter selection appears. Finally, a slider helps users to pick the right price range for the product.

In that example, customers don’t need to use the navigation or search at all to get relevant results. Obviously, it wouldn’t harm to replace a drop-down with a **smart autocomplete** to avoid dead-ends, but this works here, too.

{{< rimg href="https://commonbond.co/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb08c49c-0412-438b-97dc-22c977f66f22/24-better-navigation-design-shortcuts.png" width="800" height="506" sizes="100vw" caption="In the past, a navigation query pattern on <a href='https://commonbond.co/'>Commonbond.co</a> was providing a shortcut for users to jump to a relevant page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb08c49c-0412-438b-97dc-22c977f66f22/24-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A screenshot of the Commonbond.co website" >}}

On [Commonbond.co](https://commonbond.co/), you could define your intent using a navigation query pattern. In a dedicated area on the page, additionally to the primary navigation on the top, users are presented with a drop-down. They can specify what exactly they’d like to do on the website, or what they are looking for. Once one option is selected, another drop-down appears, allowing them to specify their intent even further. 

This experience mimics the **drill-down navigation** with multiple levels. Yet the difference is that users are making small decisions, one after another, without being confronted with the entire navigation at every step of the way.

Similar to [mega-menus](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-mega-dropdown-hover-menus/), there is no need to load a new page, and users can easily go between options without having to recalibrate their mouse pointer or finger in the menu. In fact, you could potentially also **select multiple options at once** and get only a selection of pages that are relevant to you.

{{< rimg href="https://corkchamber.ie/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee37f965-352a-438e-b259-c97b976fae99/3-better-navigation-design-shortcuts.png" width="800" height="503" sizes="100vw" caption="On <a href='https://corkchamber.ie/'>Cork Chamber</a>, you can choose what exactly you want to do and jump there immediately, from every page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee37f965-352a-438e-b259-c97b976fae99/3-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A screenshot of the Cork Chamber website" >}}

[Cork Chamber](https://corkchamber.ie/) uses a navigation query in addition to the rest of the navigation. ”I want to” is taking a **primary spot in the navigation**, driving users directly to the page of interest. Essentially it’s just a drop-down that provides users with a few options. But it could be extended with second and third-level selections. Notice how user-centric the navigation is though: “I want to” is focused on what the visitors of the page plan to do.

{{< rimg href="https://sbahn.berlin/tickets/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff2636d0-37c6-4a12-9a38-a6efb0dc1078/29-better-navigation-berlin.png" width="800" height="241" sizes="100vw" caption="Instead of using navigation, on <a href='https://sbahn.berlin/tickets/'>Sbahn.berlin</a> customers need to define a view that fits them best. The website then provides an answer for them. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff2636d0-37c6-4a12-9a38-a6efb0dc1078/29-better-navigation-berlin.png'>Large preview</a>)" alt="An example from the Sbahn.berlin website showing a dropdown menu" >}}

[Sbahn.berlin](https://sbahn.berlin/tickets/), a public transportation service in Berlin, allows users to **choose the view that fits them best** and brings them directly to a page that they might not be able to easily spot otherwise. By choosing one of the options, they jump directly to the 4th-level navigation, without having to interact with a hover or click the menu at all.

{{< rimg href="https://service.duesseldorf.de/home" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec86774f-eebf-4da6-a621-855f429d8c79/30-better-navigation-dusseldorf.png" width="800" height="233" sizes="100vw" caption="Tell the service what you want to do, and where you want to do it, and it provides an answer. Navigation shortcuts in use on <a href='https://service.duesseldorf.de/home'>City of Düsseldorf</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec86774f-eebf-4da6-a621-855f429d8c79/30-better-navigation-dusseldorf.png'>Large preview</a>)" alt="The City of Duesseldorf website uses shortcuts within the navigation at the top" >}}

Figuring out just the right page to book an appointment on [City of Düsseldorf](https://service.duesseldorf.de/home) might take quite a while when going through the global navigation or external search. However, two drop-downs in the central area allow citizens to **specify their intent and choose a location**. The result, then, is a link to the page where they can complete their task. No need to use the navigation or search at all.

{{< rimg breakout="true" href="https://monday.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/287f3ef2-9ba2-43cd-832b-3dd8daf9d3f4/8w5urfps.png" width="800" height="233" sizes="100vw" caption="On the homepage, <a href='https://monday.com/'>Monday.com</a> asks prospect customers to specify how they intend to use the product. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/287f3ef2-9ba2-43cd-832b-3dd8daf9d3f4/8w5urfps.png'>Large preview</a>)" alt="An example from the Monday.com website in which it asks users to specify their interests with the help of a dropdown menu" >}}

{{< rimg breakout="true" href="https://monday.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/125eced8-1a5b-4df2-b9b0-12e10b748341/yutxdxm4.png" width="800" height="233" sizes="100vw" caption="To maximize time to relevance, <a href='https://monday.com/'>Monday.com</a> asks prospect customers to specify their interests, and then drives them to an onboarding flow that fits their needs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/125eced8-1a5b-4df2-b9b0-12e10b748341/yutxdxm4.png'>Large preview</a>)" alt="An example from the Monday.com website in which it asks users to specify their interests with the help of a dropdown menu" >}}

[Monday.com](https://monday.com/) is using a similar pattern for their **onboarding flow**. On the homepage, prospect customers can first select what they’d like to manage using the Monday.com product. Based on that input, one of the onboarding flows is triggered, guiding users to relevant boards. A great way to bring people to relevant views is by **minimizing the distance between the intent and value**.

{{% feature-panel %}}

## Feature Comparison

Imagine that you’ve added a few headphones for comparison on an eCommerce retailer site. You probably don’t plan on purchasing all of them, but rather want to find the option that works best for you. What kind of experience are you expecting when **comparing these items**?

Most of the time, it will be a good ol’ [feature comparison table](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/), with multiple columns, one for each product, and hundreds of attributes to browse through. To navigate it, we’ll probably be using a [lown mower pattern](https://www.nngroup.com/articles/lawn-mower-pattern/), going through the tables **row by row**, from right to left and back again. Admittedly, that’s a quite tiring and time-consuming undertaking.

In fact, nobody wakes up in the morning hoping to finally compare products by features in a **comparison table matrix**. As customers, we actually want to find out what a better option is, yet we need to do quite a bit of work to get there. Even though we might have very specific attributes in mind that we care about most. To improve their experience, we can just ask our users what their intent is.

{{< rimg breakout="true" href="https://www.productchart.com/smartphones/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46531da5-e6fd-4d50-8939-f0ef3bd4e8d9/11-better-navigation-design-shortcuts.png" width="800" height="459" sizes="100vw" caption="On <a href='https://www.productchart.com/smartphones/'>Productchart.com</a>, customers compare without a feature comparison table. Customers compare by exploring a 2D-space, along with a few filters to reduce the range of options. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46531da5-e6fd-4d50-8939-f0ef3bd4e8d9/11-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A screenshot of the Product Chart website with examples and comparisons showing screen size and price" >}}

Not a typical feature comparison on [Productchart.com](https://www.productchart.com/smartphones/). Instead of using a feature comparison table, Productchart **maps all products in a two-dimensional space**. Customers can choose the attribute on each axis, and they can also use filters to reduce the overall number of options to a more manageable selection. They can also highlight products of interest and compare them side by side.

{{< rimg breakout="true" href="https://www.mediamarkt.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2c7e14e-1b7a-47d5-9437-a42754ad3804/12-13-14-better-navigation-design-shortcuts.png" width="800" height="526" sizes="100vw" caption="For comparison, <a href='https://www.mediamarkt.de/'>Media Markt</a> asks what attributes users are interested in first and shows only attributes that are relevant for them. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2c7e14e-1b7a-47d5-9437-a42754ad3804/12-13-14-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A comparison of the Media Markt website in German showing three mobile views how a user can find a product" >}}

On [Mediamarkt](https://www.mediamarkt.de/), feature comparison is happening without tables altogether. Instead, when users choose to compare products, they are asked **to choose relevant attributes first**. Potentially it could even be an autocomplete multi-combo-box, complemented with all available features grouped into accordions.

Each selection becomes a single step in the **evaluation journey**, where customers can vote up and vote down products based on the features that they have. Once it’s done, they are presented with the **winning option** &mdash; based on their interests and preferences. Additionally, there is an option to see the entire feature comparison matrix and even download it as a PDF for convenience.

## A-Z Index Pattern

Once a website keeps growing, it gets into **navigation decay**. New navigation items are added all over the place just because there don’t seem to be good existing categories under which they could live. So new categories get added, while older categories and partially outdated content **never get deleted or archived**. And because there are many different content managers involved, with many different content management systems, tags become inconsistent, categories are mislabeled and content is often duplicated &mdash; *just in case*.

The right way to address this issue is to [redesign the information architecture](https://www.smashingmagazine.com/2022/03/easy-information-architecture/) and established guidelines for publishing, categorizing, archiving and deleting. That’s the role of **governance**, of course, and as such, it might be years until any significant changes get implemented. Yet during that time visitors of the site can hardly find any information on the site, and had to rely on Google or Bing instead, often landing on competing websites altogether.

One way to address that is by using an **A-Z Index pattern**. We identify the [top tasks](https://alistapart.com/article/what-really-matters-focusing-on-top-tasks/) that users perform on the site. For each task, we define a set of keywords that they associate the task with. We run [tree testing](https://maze.co/guides/ux-research/tree-testing/) to ensure that they can find the pages that they are looking for. And then we surface the A-Z catalog of keywords on a single page.

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/869e5495-4f4a-4e4e-b470-bccaf62211c8/15-better-navigation-design-shortcuts.png" width="800" height="370" sizes="100vw" caption="Large websites are likely to be using A-Z pattern. Examples: <a href='https://www.service.nsw.gov.au/nswgovdirectory/atoz'>NSW Government</a>, <a href='https://www.nhs.uk/conditions/'>NHS.uk</a>, <a href='https://www.govt.nz/organisations/#main'>New Zealand Government</a>, <a href='https://www.usa.gov/federal-agencies'>USA.gov</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/869e5495-4f4a-4e4e-b470-bccaf62211c8/15-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A mobile view comparison of the four websites in question" >}}

In fact, that’s a very typical approach that many large websites, especially public service websites, will use &mdash; alongside search and global navigation. **Every keyword is of course a link**, driving users to the page of interest. 

Sometimes each letter is represented on a separate page, and sometimes vertical accordions are used. In usability tests, the best way to show an A-Z index appears to be by **listing all keywords on a single page** &mdash; mostly because users can use in-browser search to look something up quickly without having to go and explore multiple pages.

{{< rimg breakout="true" href="https://www.uantwerpen.be/en/study/programmes/all-programmes/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3f5d8d0-71ab-435c-8b5c-31aa8b508241/16-better-navigation-design-shortcuts.png" width="800" height="495" sizes="100vw" caption="A quite sophisticated A-Z index with a lot of detail, on <a href='https://www.uantwerpen.be/en/study/programmes/all-programmes/'>University of Antwerp</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3f5d8d0-71ab-435c-8b5c-31aa8b508241/16-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="An example from the website of the University of Antwerp showing filters in alphabetical order beginning with A" >}}

To take it one step further, we could also **expose relevant information** right in the A-Z index. Rather than driving users to a dedicated page, they could choose what information they want to learn &mdash; opening hours, location, booking appointment links, etc. &mdash; and study that information without ever heading to individual pages.

A good example of a similar idea is [University of Antwerp](https://www.uantwerpen.be/en/study/programmes/all-programmes/) which surfaces useful information directly on the A-Z index page. Of course, this information could also be accessible within an accordion, but then we’d also need a button to **open and collapse all accordions** at once.

{{< rimg breakout="true" href="https://international.au.dk/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/165324ed-cb63-4870-832d-b6cd776454d4/30-better-navigation-design-shortcuts.png" width="800" height="407" sizes="100vw" caption="Visitors can quickly jump from any page to any page on <a href='https://international.au.dk/'>Aarhus University</a>. A-Z index is permanently accessible in the header of each page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/165324ed-cb63-4870-832d-b6cd776454d4/30-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A screengrab of the Aarhus University website showing study portals in the navigation at the top" >}}

[Aarhus University](https://international.au.dk/) highlights the A-Z index as part of global navigation. Visitors can choose their role first, then choose a letter, and then explore the overview of all options available, jumping to a specific department or faculty. 

Most importantly, visitors can **quickly jump from any page to any other page**. In this case, the A-Z index is permanently accessible in the header of each page. That’s not something other navigation patterns provide out of the box.

The only caveat here is that keywords appearing in the A-Z index have to be **thoroughly tested** to ensure that users actually find what they need in the index. And sometimes the index is complemented with an in-index search, which is very similar to autocomplete.

{{% ad-panel-leaderboard %}}

## Tap-Ahead Autocomplete Pattern

We tend to use autocomplete to **highlight relevant keyword suggestions**. However, We could also drive users directly to relevant categories, specific products, brands, or even collections of items or records that we’ve prepared ahead of time. 

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b4e763a-951b-4624-905c-405f504bef76/18-better-navigation-design-shortcuts.png" width="800" height="480" sizes="100vw" caption="Autocomplete can provide much more than just keyword suggestions. We could show categories, products, prices and any other attributes immediately. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b4e763a-951b-4624-905c-405f504bef76/18-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A mobile view comparison of the three websites mentioned below" >}}

On [Prisma.fi](https://www.prisma.fi/fi/prisma), [Hema.nl](https://hema.nl/) and [Ikea.com](https://www.ikea.com/), autocomplete prompts **category suggestions**, products, frequent searches as well as products and information about each product, from their length to their prices. Rather than focusing on a list of keywords, the autocomplete actually provides an overview of items that the users might be looking for.

{{< rimg breakout="true" href="https://www.stat.ee/en" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b658dba-ca21-49a3-9c17-1aeca403f90c/19-better-navigation-design-shortcuts.png" width="800" height="477" sizes="100vw" caption="It’s not surprising to see statistical offices providing data in their autocomplete suggestions. Point in case: <a href='https://www.stat.ee/en'>Statistics Estonia 100</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b658dba-ca21-49a3-9c17-1aeca403f90c/19-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A search bar showing autocomplete suggestions on the Statistics Estonia 100 website" >}}

[Statistics Estonia 100](https://www.stat.ee/en) highlights an overview of articles but also the actual query results that a visitor might be looking for. Each type of data is marked, along with the recent statistics provided right in the autocomplete.

However, we could also take it to the next level entirely. We can provide users with helpful feedback on their query and guide them towards a **better keyword query** that would also bring them better results. And that’s exactly what the **tap-ahead autocomplete pattern** provides.

With tap-ahead autocomplete, we allow users to **construct a query based on autocomplete suggestions**. As users hit the autocomplete field or start typing a keyword, suggestions appear. Users can either jump directly to the keyword, or *append* frequently used keyword combinations to their query, hence “constructing” their query based on the suggestions.

{{< rimg href="https://www.mediamarkt.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2702bb78-e419-476f-9518-ea9e996a9370/20-better-navigation-design-shortcuts.png" width="800" height="482" sizes="100vw" caption="Have you ever clicked on such an arrow on the right hand side? That’s Tap-Ahead in action, on <a href='https://www.mediamarkt.de/'>Media Markt</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2702bb78-e419-476f-9518-ea9e996a9370/20-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="An example of tap-ahead from the Media Markt website in German" >}}

Some large websites are using the tap-ahead pattern extensively. On [Mediamarkt.de](https://www.mediamarkt.de/), users can click through to the keyword that matches the interest, or click on the arrow on the right-hand side. The user’s query is then **replaced with the selected query**, while still leaving the user within the search input. They can continue their iterations on search queries until they feel confident in specifying their intent well enough.

Tap-ahead **minimizes the amount of effort** needed for typing, but also drives customers to relevant results and gives them the confidence that they are actually on the right track.

{{< rimg href="https://stackoverflow.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c5aa37c-1226-48a6-be08-138916a09b49/21-better-navigation-design-shortcuts.png" width="800" height="484" sizes="100vw" caption="Users can construct advanced search queries on <a href='https://stackoverflow.com/'>Stackoverflow</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c5aa37c-1226-48a6-be08-138916a09b49/21-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A search bar next to Log In and Sign Up buttons showing search results below with the possibility to ask a question or search further help" >}}

If you are designing an interface for expert users, perhaps slightly more advanced ways to use search might be reasonable. [Stackoverflow](https://stackoverflow.com/) allows its users to **specify a filter right in the search box**, without having to rely on filters, tags, or any other modes of navigation. Only focus users receive hints about how to use search in a more advanced way &mdash; should they wish to do so.

{{< rimg breakout="true" href="https://stripe.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f3b9b90-c2a2-4f02-ad9a-aa0529c07904/22-better-navigation-design-shortcuts.png" width="800" height="418" sizes="100vw" caption="On <a href='https://stripe.com/'>Stripe</a>, you can not only construct your queries, but also explore results appearing as you type. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f3b9b90-c2a2-4f02-ad9a-aa0529c07904/22-better-navigation-design-shortcuts.png'>Large preview</a>)" alt="A screenshot of the Stripe website in which suggested filters show while typing in the search bar" >}}

[Stripe](https://stripe.com/) also allows customers to specify filters right in the search box. Users can focus on typing their query in the search input, and as they do, they also see the results immediately.

{{% ad-panel-leaderboard %}}

## Wrapping Up

When designing navigation, we often rely on predictable patterns. That’s a good thing as our outcome is usually predictable, familiar, and hence obvious to our customers.

However, sometimes navigation might be just a bit too tiring and time-consuming, and in such cases, we can use **navigation queries** to pick up our users whenever they are and gently guide them toward the page that is of interest to them. They are unlikely to help you resolve all IA issues on the site, but they could help users get where they want to be faster.

All the techniques mentioned above can help us get there. By no means do they replace established navigation patterns; they **complement and add to the experience**, especially on large and slightly outdated websites.

Next time you are working on navigation, consider designing more **explorative interfaces for navigation and search**; explore navigation queries, evaluation journeys, A-Z index, and tap-ahead autocomplete. They are unlikely to help you resolve all IA issues on the site, but they could help users get where they want to go be, faster. And sometimes that’s just what is needed at the current stage of the project.

## Meet Smart Interface Design Patterns

If you are interested in similar insights around UX, take a look at [**Smart Interface Design Patterns**](https://smart-interface-design-patterns.com/), our shiny new **9h-video course** with 100s of practical examples from real-life projects. Plenty of **design patterns and guidelines** on everything from accordions and dropdowns to complex tables and intricate web forms &mdash; with five new segments added every year. *Just sayin’!* [Check a free preview](https://www.youtube.com/watch?v=aSP5oR9g-ss).

<figure style="margin-bottom: 0"><a href="https://smart-interface-design-patterns.com/"><img style="border-radius: 11px" decoding="async" fetchpriority="low" width="950" height="492" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 400w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 800w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1200w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1600w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg" sizes="100vw" alt="Smart Interface Design Patterns"></a><figcaption class="op-vertical-bottom">Meet <a href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>, our new video course on interface design &amp; UX.</figcaption></figure>

<div class="btn--lined btn--lined--white-border" style="margin-top: 0.75em; margin-bottom: 0.75em"><a class="btn btn--large btn--green btn--text-shadow" href="https://smart-interface-design-patterns.com/">Jump to the video course&nbsp;&rarr;</a></div>

<p class="ticket-price__desc" style="font-size: .8em!important; text-align: center; line-height: 1.5; margin: 0; display: block;">100 design patterns &amp; real-life 
examples.<br>9h-video course + live UX training. <a href="https://www.youtube.com/watch?v=aSP5oR9g-ss">Free preview</a>.

## Related Articles

If you find this article useful, here’s an overview of similar articles we’ve published over the years &mdash; and a few more are coming your way.

- [Designing A Perfect Infinite Scroll](https://www.smashingmagazine.com/2022/03/designing-better-infinite-scroll/)
- [Designing Perfect Breadcrumbs](https://www.smashingmagazine.com/2022/04/breadcrumbs-ux-design/)
- [Designing A Perfect Carousels](https://www.smashingmagazine.com/2022/04/designing-better-carousel-ux/)
- [Designing A Perfect Accordion](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/)
- [Designing A Perfect Responsive Configurator](https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/)
- [Designing A Perfect Birthday Picker](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/)
- [Designing A Perfect Date and Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
- [Designing A Perfect Feature Comparison](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/)
- [Designing A Perfect Slider](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/)
- “[Form Design Patterns Book](https://www.smashingmagazine.com/printed-books/form-design-patterns/),” written by Adam Silver

{{< signature "il" >}}

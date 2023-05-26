---
title: 'Infinite Scroll UX Done Right: Guidelines and Best Practices'
slug: designing-better-infinite-scroll
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41704a7b-0bd6-4144-b13e-2b092a0ea3e1/designing-better-infinite-scroll.jpg
date: 2022-03-30T13:30:00.000Z
summary: >-
  Infinite scroll can be designed well. Best practices and guidelines to improve the UX of infinite scroll with bookmarks, footer reveal and pagination.
description: >-
  Infinite scroll can be designed well. Best practices and guidelines to improve the UX of infinite scroll with bookmarks, footer reveal and pagination.
disable_panels: true
categories:
  - UX
  - Design Patterns
---

We’ve all been there. You might have a long-winded list of search results, products, orders or data entries. Of course, you have all kinds of filters and sorting and search already in place. However, you also need to help customers **explore relevant entries**, and to do so, you need to support and speed up browsing through entries.

Your natural design instinct might tell you to stay true to good old-fashioned pagination at first. Yet before you know it, you might start wondering if **infinite scroll** might be a good option to consider, given the very unique use case that you have. So is infinite scroll actually a good idea? Well, we all have strong opinions about infinite scroll, and usually not very good ones. This has a number of good reasons.

<p style="background-color: #e8f5ff;
border: 1px solid #dbeaff; border-radius: 11px; padding: 1.35rem 1.65rem;">This article is part of our ongoing series on <a href="/category/design-patterns">design patterns</a>. It’s also a part of the upcoming <a style="font-weight: bold" href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-ux/">4-weeks live UX training</a>&nbsp;🍣 and will be in our recently released <a href="https://smart-interface-design-patterns.com/">video course</a> soon.</p>

## Problems With Infinite Scroll

The issues with infinite scroll are well-known. The most obvious one is the sheer amount of options on the page which is often **too overwhelming** and too difficult to manage. It really feels like [drowning in an information abyss](https://www.nngroup.com/articles/infinite-scrolling/) with no end in sight. No wonder that once the number of displayed options is beyond the [comfortable range](https://www.smashingmagazine.com/2021/07/frustrating-design-patterns-broken-frozen-filters/), a good number of users abandon the page altogether as a reaction to that.

Also, we don’t have any control over when and how many items appear on scroll. Just like there is no easy way to navigate between the **“old” and “new” segments** of the infinite scroll as they all fall into the same stream of items. Once you scroll up and down a few items, it’s hard to see immediately what we have seen already and what we haven’t seen yet &mdash; unless we meticulously scan through the last few items a couple of times.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e8341ca-f39b-44b3-88a5-5219aa193533/01-pagination-vs-infinite-scroll.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e8341ca-f39b-44b3-88a5-5219aa193533/01-pagination-vs-infinite-scroll.png" width="800" height="351" sizes="100vw" caption="Pagination vs. infinite scroll. An old discussion, without a clear winner. Image credit: Yogev Ahuvia (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e8341ca-f39b-44b3-88a5-5219aa193533/01-pagination-vs-infinite-scroll.png'>Large preview</a>)" alt="Pagination vs. infinite scroll. An old discussion, without a clear winner" >}}

Sometimes the **URL in the address bar** changes on scrolling, but more often it does not, leaving us out there starting all over again if we want to continue browsing later. And if we want to send the URL to ourselves or to our loved ones to explore a particular set of items at once, that’s usually painful as we can’t really **bookmark a location** in the list.

Should we want to **reach the footer**, every time we scroll, we need to scroll just a little bit faster to get a miraculous chance to reach the footer before the new stream of items comes in. Sometimes users find themselves taking on a scrolling challenge while hitting <kbd>Esc</kbd> at the same time &mdash; to *cancel* the infinite scroll just in time. (*Usually unsuccessfully.*)

On top of that, infinite scroll [breaks the scroll bar](https://www.nngroup.com/articles/infinite-scrolling/) as the user’s expectations of the page length have to be recalibrated with every scroll. The scrollbar is a *promise* of how lengthy the page actually is, but with newly loaded items, the promise is always faulty. Not to mention **accessibility issues** of announcing the newly loaded items properly to screen readers as well as **performance issues** on choppy connections.

All of the issues listed above are just **poor usability**. So it’s not surprising that we often disregard infinite scroll as a fashionable technique that produces more problems than solutions. And it’s not surprising that as designers, we tend to use other options instead: pagination and “load more” buttons.

{{% feature-panel %}}

## Pagination and “Load More”

We can avoid all infinite scroll issues by falling back to the usual suspect: **pagination**. And it has plenty of benefits. With it, the user always has a **clear beginning and a clear end**. As users finish a page and move to the next one, there is a very clear “cut” of what has and what hasn’t been seen yet, along with a sense of completion during that navigation.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ac115a2-67bb-4a97-9165-433d499c1ba4/pagination-patterns.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ac115a2-67bb-4a97-9165-433d499c1ba4/pagination-patterns.jpg" width="577" height="253" sizes="100vw" caption="Perhaps a bit old-fashioned, but very reliable: pagination on <a href='https://www.thinkific.com/'>Thinkific.com</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ac115a2-67bb-4a97-9165-433d499c1ba4/pagination-patterns.jpg'>Large preview</a>)" alt="Pagination as displayed on the Thinkific website" >}}

Plus, there is a **sense of control** how much data is being displayed on a given page (usually with controls to change the number of items per page), the URL is different for every page, the footer is easy to reach and the options appearing on pages are easier to manage.

Unfortunately, in usability tests, **sometimes pagination doesn’t perform well at all**. It’s much more predictable and easier to manage, but also much slower compared to infinite scroll, so users often browse significantly less and often feel “slowed down”. There seems to be more time spent on the first few pages, and filters and sorting are used more often in that time, but compared to infinite scroll, they view fewer items in total and are often less engaged.

If we want to keep the benefits of pagination but avoid overwhelming users with infinite scroll, we can use a **“Load more” pattern** instead. With it in place, as users start scrolling, eventually they can choose to load more items on tap or on click. In some implementations, as users start scrolling down, more items appear automatically at first, but then the “Load more” button appears, once a certain threshold is reached.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31aeb2f0-3f76-47f2-b8f2-be699e6d2d84/02-load-more-pattern.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31aeb2f0-3f76-47f2-b8f2-be699e6d2d84/02-load-more-pattern.png" width="577" height="264" sizes="100vw" caption="“Load more” pattern in use, on Crutchfield. On the first few scrolls, new items appear automatically. The “Load more” button starts appearing only when user reaches 58 items. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31aeb2f0-3f76-47f2-b8f2-be699e6d2d84/02-load-more-pattern.png'>Large preview</a>)" alt="A pair of on-ear headphones displayed on a product page" >}}

For example, we could display **10–30 products on the initial page load** (10 on mobile, 30 on desktop). When the user reaches the end of the listing, we can use automatically fetch the next 10–30 products. When the user reaches 30–70 items, we then switch to “Load more”. We also provide an option to go back with the “Back” button, so users always have a sense of control about where they navigate.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60c7780f-671b-461e-b7dd-779c9e2ce95d/03-continue-browsing-later.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60c7780f-671b-461e-b7dd-779c9e2ce95d/03-continue-browsing-later.png" width="577" height="339" sizes="100vw" caption="We could allow users to send a link to the current position in the list and continue browsing later. A mock-up, based on Crutchfield UI. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60c7780f-671b-461e-b7dd-779c9e2ce95d/03-continue-browsing-later.png'>Large preview</a>)" alt="A screenshot of a product page showing on-ear headphones to which you can send yourself or anyone else a link to an email address to continue at a different time or day" >}}

We could also provide an option to **continue browsing later** by allowing users to type in their email and get a link that later would bring them to the position in the list where they currently are. This solves the problem of not being able to continue browsing later, perhaps on another device, or at a different time.

[“Load more” works very well in eCommerce](https://www.smashingmagazine.com/2016/03/pagination-infinite-scrolling-load-more-buttons/) &mdash; users have control of what they see as all items appear on a single page and the footer is always in reach. Plus, if the URL is changed every time a user hits the “Load more” button, we bring together the **speed of infinite scroll with the comfort and security of pagination**. Users do seem to be browsing more and are more engaged. This makes this pattern a good option to consider for lengthy lists.

Does it mean that we can abandon infinite scroll altogether? Not necessarily. An important benefit of infinite scroll is the **speed of displaying results** &mdash; displaying new items just when users want to see more. As it turns out, there are a few techniques and strategies to make infinite scroll better. But it requires solving all of the issues we’ve outlined earlier.

{{% ad-panel-leaderboard %}}

## Bookmarking The Position In The List

The easiest way to improve infinite scroll is by marking the breaks between “new” and “old” items in the list. When a new batch comes in, we **separate the items visually** and allow users to mark the position in the list from which they want to continue browsing later. We could also allow them to see all products they’ve seen on a **separate page**, so they can separate viewed options from the infinite stream of all options. An example of this interaction is displayed below.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ff2d0e7-8df4-4e44-a64b-55cab096eca8/04-adding-whitespace.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ff2d0e7-8df4-4e44-a64b-55cab096eca8/04-adding-whitespace.png" width="577" height="549" sizes="100vw" caption="Adding enough whitespace between “new” and “old” segments in the list, and a button allowing users to continue browsing later. A mock-up, based on Crutchfield UI. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ff2d0e7-8df4-4e44-a64b-55cab096eca8/04-adding-whitespace.png'>Large preview</a>)" alt="An example of a product page showing two different pairs of cover-ear headphones" >}}

Once a user clicks on the “Continue here later”, we could either show a checkmark and store the position in the browser, or **display a modal** asking users for their email address.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08fee91f-e97a-4f51-82f2-45b66d1b1afd/05-pop-up.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08fee91f-e97a-4f51-82f2-45b66d1b1afd/05-pop-up.png" width="577" height="189" sizes="100vw" caption="A pop-up showing up when a user wants to continue browsing later. A mock-up, based on Crutchfield UI. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/08fee91f-e97a-4f51-82f2-45b66d1b1afd/05-pop-up.png'>Large preview</a>)" alt="A product image of over-ear headphones" >}}

Alternatively, we could display the newsletter box directly, allowing users to **copy a link to the current position** on the page as well. As a positive side effect, this also gives us an option to collect users’ emails to send them a reminder about new items later.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc5913c-1404-4d45-af06-0811e46fa2eb/06-changing-the-wording.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc5913c-1404-4d45-af06-0811e46fa2eb/06-changing-the-wording.png" width="577" height="470" sizes="100vw" caption="Changing the wording to 'Copy a link to this position in the list'. A mock-up, based on Crutchfield UI. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fcc5913c-1404-4d45-af06-0811e46fa2eb/06-changing-the-wording.png'>Large preview</a>)" alt="A product image of two pairs of over-ear headphones" >}}

## Footer Reveal

The solution above might solve the problem with the lack of understanding of where users are, but since items will be loaded in automatically, we still have some other issues &mdash; e.g. **reaching the footer**. This is quite easy to solve though.

Just like we are used to sticky headers, we could integrate a **footer reveal**: a little helper that would stay persistent at the bottom right bar, and display the footer if needed while the rest of the page uses infinite scroll. A good example of it in action is [Dahmakan](https://popmeals.com.my/food-delivery), a food delivery service from Kuala-Lumpur in Malaysia (no infinite scroll in use at the moment). It’s worth emphasizing that the footer should be **accessible via keyboard** navigation as well, rather than just opening on click or on tap.

<!-- {{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c57dfff-f500-452b-8d69-03f61175371f/07-dahmakan-sticky-footer.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c57dfff-f500-452b-8d69-03f61175371f/07-dahmakan-sticky-footer.png" width="800" height="" sizes="100vw" caption="Sticky footer Dahmakan, a food delivery service from Kuala-Lumpur in Malaysia. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c57dfff-f500-452b-8d69-03f61175371f/07-dahmakan-sticky-footer.png'>Large preview</a>)" alt="" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c26ba92-1460-409f-a0f2-c07bdd1124c6/08-dahmakan-open-footer.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c26ba92-1460-409f-a0f2-c07bdd1124c6/08-dahmakan-open-footer.png" width="800" height="" sizes="100vw" caption="Sticky footer Dahmakan, a food delivery service from Kuala-Lumpur in Malaysia (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c26ba92-1460-409f-a0f2-c07bdd1124c6/08-dahmakan-open-footer.png'>Large preview</a>)" alt="" >}} -->

{{< vimeo id="692843018" caption="Footer reveal, with a button showing and hiding footer when needed. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c57dfff-f500-452b-8d69-03f61175371f/07-dahmakan-sticky-footer.png'>Large preview</a>)" >}}

## Combine Pagination and Infinite Scroll

As users scroll down a page and items are loaded in, we can present it as **dynamic pagination** to users (see [Pepper.pl](https://www.pepper.pl/)). On scroll, the URL of the page changes, and the page number is updated in the sticky bottom bar. Users can also navigate to a specific page in a pagination drop-down. And of course, an accordion opens up a footer on tap or click as well. [Check the video example](https://vimeo.com/692842717).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e73f391-9065-4c37-9c77-acb2b3e49006/09-pepper-sticky-footer-scroll.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e73f391-9065-4c37-9c77-acb2b3e49006/09-pepper-sticky-footer-scroll.png" width="754" height="587" sizes="100vw" caption="Combining pagination and infinite scroll in one &mdash; along with a sticky footer at the bottom of the screen. Pepper.pl (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e73f391-9065-4c37-9c77-acb2b3e49006/09-pepper-sticky-footer-scroll.png'>Large preview</a>)" alt="A screenshot of three products displayed at the bottom of the site’s page" >}}

What do we do with the **“Back” button** though? For example, once a user has browsed through “pages” 1, 2 and 3 and now has landed on “page” 4, should a click on a “Back” button bring them from page 4 to page 3, or to the previous page that they visited before getting to the page 1 in the first place? In general, we probably don’t want to pollute users’ browsers' history by adding every step of the infinite scroll in there. So selecting a specific page with a drop-down is indeed a good idea. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/361311c8-e639-41c9-beb0-4ae887221089/10-pagination-infinite-scroll.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/361311c8-e639-41c9-beb0-4ae887221089/10-pagination-infinite-scroll.png" width="754" height="600" sizes="100vw" caption="Users can jump to specific pages, while using infinite scroll during browsing. Perhaps a drop-down chevron next to current page number would make it a bit more obvious. Pepper.pl (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/361311c8-e639-41c9-beb0-4ae887221089/10-pagination-infinite-scroll.png'>Large preview</a>)" alt="A screenshot of a product page with the page numbers displayed below" >}}

A great example of combining **pagination and infinite scroll** in one place; the only refinement could be slightly better focus styles and better navigation jumps for accessibility. Additionally, it would be fantastic to add some sort of a **drop-down chevron** next to the current page to make it obvious that one can actually jump to a specific page. The “Back” button, then, would bring the user back to the page from which they came to the list they have in front of them at the moment.

## Scrollbar Range Intervals

Another useful technique is suggested by [Baymard Institute](https://baymard.com/), a research company for testing eCommerce sites. The idea is to make scrollbars more helpful by adding **dynamic labels** that are spaced out vertically. These would indicate to users where they currently are and where they can jump to. As users keep scrolling down, the labels would be shifting as the scrollbar is growing. Could be used by any criteria a user has chosen to sort the items by.

{{< rimg href="https://baymard.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32978341-969b-4ff1-a97e-1d3a8657391c/11-scrollbar-range-intervals.png" width="578" height="554" sizes="100vw" caption="If users sort by price, we could display dynamic pricing labels next to the scrollbar. Image credit: <a href='https://baymard.com/'>Baymard Institute</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/32978341-969b-4ff1-a97e-1d3a8657391c/11-scrollbar-range-intervals.png'>Large preview</a>)" alt="An example of dynamic pricing labels shown on the product page" >}}

## Pinning Sections on a Mini-Map

We could make it even more useful by **allowing users to pin, or bookmark, areas of interest** in the list, so they can return to favorites faster. An interesting prototype of such an experience is [Minimap experiment](https://uiw.tf/minimap) (currently works only in Firefox), created by Rauno Freiberg, along with many other [wonderful experiments](https://uiw.tf/).


{{< rimg href="https://baymard.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa252212-27bf-4844-8629-fa045408ab89/minimaps.jpg" width="578" height="554" sizes="100vw" caption="A <a href='https://uiw.tf/minimap'>mini-map experiment</a>, allowing users to mark and pin some areas of the screen and jump to them faster. Currently works only in Firefox. <a href='https://vimeo.com/692844539'>Check the video example</a>." alt="A screenshot of text on screen where users can mark and pin particular parts of the text to jump to anytime" >}}

{{% ad-panel-leaderboard %}}

## Wrapping Up

With all of these techniques in place, **we solved many problems** that infinite scroll is known for. We now have better control of how many items appear on scroll, and can always stop browsing and continue later. We can easily spot “old” and “new” segments. The URL is being updated as the user scrolls down the page, and we allow them to copy the URL to the current position in the list as well.

Users **can always reach the footer**, and the scrollbar indicates where they currently are and where they can jump to. They can also jump to any specific page since we provide pagination as well. Additionally, we still need to implement infinite scroll in a way to ensure accessibility for the keyboard and announce new items. But: we make use of all the benefits that infinite scroll provides: especially the speed of browsing.

Now, all of this seems like **a lot of work** just to make infinite scroll better. The ultimate question of whether all the work is worth it has to be answered by the goals your users are supposed to achieve. [Infinite scroll is not for every website](https://www.nngroup.com/articles/infinite-scrolling/), and an endless list of options needs to be complemented with proper **filtering, sorting and search**. In general, if your users are more likely to compare options or find very specific content, infinite scroll probably won’t be very useful.

However, if your users often explore many options, and browsing is a very typical attribute on your site, especially when customers add multiple items in a shopping cart or operate on a large set of data entries at once, infinite scroll **might be very well worth it** &mdash; but only if accessibility and performance considerations are the very heart of its design.

The ideas highlighted in this article are just that &mdash; *ideas*. Some of them might fail miserably in your usability tests, while others might perform fairly well. But: if you absolutely need to **make infinite scroll work**, there are ways and workarounds to do so &mdash; it’s just not as straightforward as it might appear at first.

## Infinite Scroll Checklist

As usual, here’s a general checklist of a few **important guidelines to consider** when designing a better infinite scroll:

- If in doubt, always prefer **pagination**.
- With infinite scroll, always integrate a **footer reveal**.
- Consider separating “old” and “new” items visually.
- Provide an option to **continue browsing later**.
- Consider using “load more” + infinite scroll together.
- Consider using pagination + infinite scroll together.
- Change the URL as new items are loaded in and expose it to users.
- Allow users to jump to any page with a **pagination drop-down**.
- Consider using scrollbar range intervals.
- Consider allowing users to pin or bookmark items/areas of interest.
- Make sure **accessibility and performance** are major considerations in the implementation.

## Meet Smart Interface Design Patterns

If you are interested in similar insights around UX, take a look at [**Smart Interface Design Patterns**](https://smart-interface-design-patterns.com/), our shiny new **9h-video course** with 100s of practical examples from real-life projects. Design patterns and guidelines on everything from mega-dropdowns to complex enterprise tables &mdash; with 5 new segments added every year. *Just sayin’!* [Check a free preview](https://www.youtube.com/watch?v=aSP5oR9g-ss).

<figure style="margin-bottom: 0"><a href="https://smart-interface-design-patterns.com/"><img style="border-radius: 11px" decoding="async" fetchpriority="low" width="950" height="492" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 400w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 800w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1200w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1600w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg" sizes="100vw" alt="Smart Interface Design Patterns"></a><figcaption class="op-vertical-bottom">Meet <a href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>, our new video course on interface design &amp; UX.</figcaption></figure>

<div class="btn--lined btn--lined--white-border" style="margin-top: 0.75em; margin-bottom: 0.75em"><a class="btn btn--large btn--green btn--text-shadow" href="https://smart-interface-design-patterns.com/">Jump to the video course&nbsp;&rarr;</a></div>

<p class="ticket-price__desc" style="font-size: .8em!important; text-align: center; line-height: 1.5; margin: 0; display: block;">100 design patterns &amp; real-life 
examples.<br>9h-video course + live UX training. <a href="https://www.youtube.com/watch?v=aSP5oR9g-ss">Free preview</a>.

## Useful Resources

- “[Infinite Scrolling Is Not For Every Website](https://www.nngroup.com/articles/infinite-scrolling/),” Hoa Loranger, Nielsen Norman Group 
- “[UX: Infinite Scrolling vs. Pagination](https://uxplanet.org/ux-infinite-scrolling-vs-pagination-1030d29376f1),” Nick Babich, UX Planet
- “[Infinite Scroll: Let’s Get To The Bottom Of This](https://www.smashingmagazine.com/2013/05/infinite-scrolling-lets-get-to-the-bottom-of-this/),” Yogev Ahuvia, Smashing Magazine
- “[Infinite Scrolling, Pagination Or “Load More” Buttons? Usability Findings In eCommerce](https://www.smashingmagazine.com/2016/03/pagination-infinite-scrolling-load-more-buttons/),” Christian Holst, Smashing Magazine

If you find this article useful, here’s an overview of similar articles we’ve published over the years &mdash; and a few more are coming your way.

### Related Articles

- [Designing A Perfect Accordion](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/)
- [Designing A Perfect Responsive Configurator](https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/)
- [Designing A Perfect Birthday Picker](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/)
- [Designing A Perfect Date and Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
- [Designing A Perfect Feature Comparison](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/)
- [Designing A Perfect Slider](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/)
- “[Form Design Patterns Book](https://www.smashingmagazine.com/printed-books/form-design-patterns/),” written by Adam Silver

{{< signature "il" >}}

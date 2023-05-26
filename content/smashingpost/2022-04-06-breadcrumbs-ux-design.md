---
title: 'Designing Effective Breadcrumbs Navigation'
slug: breadcrumbs-ux-design
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83a5c72a-37d0-4c2c-9ce8-1ebc22b913f3/designing-better-breadcrumbs-navigation.jpg
date: 2022-04-06T14:20:00.000Z
summary: >-
  Breadcrumbs UX are often neglected, but they can be extremely helpful when designing a complex navigation. We can improve them with sideways navigation, clearer breadcrumbs paths and accordions on mobile.
description: >-
  Breadcrumbs UX are often neglected, but they can be extremely helpful when designing a complex navigation. We can improve them with sideways navigation, clearer breadcrumbs paths and accordions on mobile.
categories:
  - UX
  - Web Design
  - Usability
  - Navigation
---

Nobody gets particularly excited about **breadcrumbs navigation**. You know, those tiny little crumbles of pathways that illustrate where a user currently is in the intricate hierarchy of the website. Their design is seemingly obvious, so is their position on the page, and it doesn’t seem like much innovation is required for breadcrumbs to shine.

As it turns out, there are plenty of fine little details that can either make breadcrumbs confusing or infinitely more useful. In this article, we’ll take a closer look at some of them. We’ll explore **when we actually need breadcrumbs**, how people use them, and how to design them better to speed up users’ navigation on our websites.

Let’s start by exploring how people navigate websites in the first place, and how exactly breadcrumbs assist us in our journeys.

<p style="background-color: #e8f5ff;
border: 1px solid #dbeaff; border-radius: 11px; padding: 1.35rem 1.65rem;">This article is part of our ongoing series on <a href="/category/design-patterns">design patterns</a>. It’s also a part of the upcoming <a style="font-weight: bold" href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-ux/">4-weeks live UX training</a>&nbsp;🍣 and will be in our recently released <a href="https://smart-interface-design-patterns.com/">video course</a> soon.</p>
  
## Breadcrumbs UX: How Do People Navigate Websites?

Every usability test shows that there is no single, general and well-established way of exploring websites. Depending on the task at hand and the frequency of visits, users apply very **different modes of navigation**. It’s not uncommon to see that on some websites, search is barely used but main navigation gets a lot of attention. On others, categories hardly get any clicks but search queries go through the roof. And sometimes breadcrumbs happen to be the most popular navigation choice on the entire site.

{{< rimg breakout="true" href="https://auspost.com.au/id-and-document-services/licence-renewals-and-applications/sa-drivers-licence-renewals#tab1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ca97f3b-13cd-4070-a50d-c3b16aa418ae/64-economist-designing-better-breadcrumbs.png" width="800" height="426" sizes="100vw" caption="<a href='https://auspost.com.au/id-and-document-services/licence-renewals-and-applications/sa-drivers-licence-renewals#tab1'>Australia Post Service</a> combine plenty of navigation patterns on one page. They all serve different purposes, and work well." alt="" >}}

On [Australia Post](https://auspost.com.au/id-and-document-services/licence-renewals-and-applications/sa-drivers-licence-renewals#tab1), for example, various kinds of navigation need to work together. The global navigation bar, the primary navigation, the breadcrumbs, the sidebar and tabs. Users can jump between various levels, they can easily go backwards with breadcrumbs, move forward with horizontal navigation on the top, move sideways with the sidebar navigation and switch contexts within the sections of the page with tabs.

We **rarely browse through every section** one by one, and we rarely even notice all the navigation available on the site. For frequently visited websites, such as a news website, we’ll be using a **very limited set of pages** and features. In fact, we probably won’t be able to remember what features and sections we are clicking, but we probably *will* remember where they are located in the interface.

<!-- [Postal Service Iceland](https://posturinn.is/einstaklingar/posthus-postbox-og-pakkaport/aframsenda-i-postbox/) doesn’t include the current page in their breadcrumbs. Because the heading is located close to the breadcrumbs, it might be indeed unnecessary. Everything is perfectly clear here &mdash; except that each breadcrumb is a link, perhaps. The only issue is [performance](https://pagespeed.web.dev/report?url=https%3A%2F%2Fposturinn.is%2Feinstaklingar%2Fposthus-postbox-og-pakkaport%2F). -->

{{< rimg breakout="true" href="https://posturinn.is/einstaklingar/posthus-postbox-og-pakkaport/aframsenda-i-postbox/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a324d460-fcfa-44d6-8583-90bf6c3766c6/62-economist-designing-better-breadcrumbs.png" width="800" height="465" sizes="100vw" caption="Once you landed on the page, how would you make sense of where you are? Here, breadcrumbs help a lot. Example: <a href='https://posturinn.is/einstaklingar/posthus-postbox-og-pakkaport/aframsenda-i-postbox/'>Postal Service Iceland</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a324d460-fcfa-44d6-8583-90bf6c3766c6/62-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

When we land on a website we’ve never visited before, e.g. national opera website, we assess the breadth of options and features at first. This usually happens by **scrolling up and down** the page — first slowly, then faster — and getting familiar with the navigation menus. We click through sidebars, switch between tabs and open mega-drop-downs. We just wander around, trusting navigation signposts and our extremely unreliable hunches. We scan, identify patterns and trust our instincts.

And sometimes, if we don’t find what we are after, our journeys turn into **wild explorations** of pages and categories of all kinds — often intense, chaotic, time-consuming and frustrating. If anything doesn’t work as expected, we just don’t use it anymore because we don’t trust it anymore. And once we don’t really have any options left, we abandon altogether.

{{< rimg href="https://gds.blog.gov.uk/2019/12/19/making-gov-uk-more-than-a-website/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b33fea7a-4dd5-4f0a-8746-3a1210abd709/47-nejm-designing-better-breadcrumbs.png" width="800" height="797" sizes="100vw" caption="Sometimes, redesigned websites get a significant traffic drop. It’s not because something has gone wrong. On the contrary: we <a href='https://gds.blog.gov.uk/2019/12/19/making-gov-uk-more-than-a-website/'>meet users where they are</a>, displaying answers directly, so there is no need to visit the website. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b33fea7a-4dd5-4f0a-8746-3a1210abd709/47-nejm-designing-better-breadcrumbs.png'>Large preview</a>)" alt="OneBoxes" >}}

However, when navigation and search are barely used, it’s not necessarily because the website is poorly designed or built. On the contrary: the content might be so well-organized that people actually **find what they need** very quickly — perhaps even before visiting the website in the first place, just by exploring Google’s search results. And once they do, there isn’t really much reason to stay on the site.

While we often focus on **exit rates** and **bounce rates** and time spent on a page, these indicators rarely reveal the full story of what exactly users are doing on the site. The fact that somebody spends 4:30 minutes on a given page isn’t necessarily a good indicator; and the fact that somebody leaves within 30 seconds isn’t necessarily a bad thing.

To track how well users understand and use navigation (and search), we need to track how successful users are at a task at hand. You can think about it as **design KPIs** established and studied over a longer period of time. It’s worth gathering insights about user-focused metrics such as:

- **task completion rates**,
- task completion times,
- time to first share,
- customer support inquiries,
- ratio of negative reviews,
- accuracy of submitted data.

Our task, then, is to pave a path for users that’s obvious, clear and unambiguous to help them complete their tasks. And that usually means supporting **three directions of navigation**: forwards navigation, backwards navigation and sideways navigation.

{{< rimg breakout="true" href="https://www.craftscouncil.org.uk/business-skills/spring-back-talks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9e83131-2d25-429f-b095-8f26d0539c44/66-economist-designing-better-breadcrumbs.png" width="741" height="388" sizes="100vw" caption="For websites with a shallow navigation tree, breadcrumbs can be integrated into headings and titles. <a href='https://www.craftscouncil.org.uk/business-skills/spring-back-talks'>Crafts Council</a> does just that. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9e83131-2d25-429f-b095-8f26d0539c44/66-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

### Forwards Navigation

We come to websites for a reason, and on some websites, it can be as specific as checking a bank account or exploring a large data set. So once we end up on a homepage or on a dashboard, we move forwards in the hierarchy on the site, from very broad to very specific pages, in an attempt to complete that task that we’ve set out to achieve.

{{< rimg breakout="true" href="https://stripe.com/docs/billing/subscriptions/overview" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e8fdde9-2e76-4765-b0a5-667f183154a8/23-stripe-designing-better-breadcrumbs.png" width="800" height="484" sizes="100vw" caption="<a href='https://stripe.com/docs/billing/subscriptions/overview'>Stripe Docs</a> combines various directions of navigation at once &mdash; it’s easy to navigate forward, backwards and sideways with the main navigation, sidebar navigation, in-page navigation and breadcrumbs. All at once. (<a href=''>Large preview</a>)" alt="Stripe Docs" >}}

In navigation terms, we move from a homepage to a category to sub-categories to further in-page navigation to find that particular feature that we need to finally click on. And if we are lucky, we can skip the entire journey and reach that feature from a mega-drop-down or calls-to-action earlier. The better we, as designers, **reduce the distance between the intent and action**, the better the user experience will be.

### Backwards Navigation

It’s not always that we have exactly one particular task in mind though. More often than not, our **goals are multi-faceted**, and we change our minds, overlook things, make spontaneous decisions, and get distracted by blinking notifications. So our digital journeys are **rarely strictly linear**, and this holds true especially if the navigation on the site is somewhat convoluted.

In such cases, eventually, we end up moving *backwards.* In fact, we move back to reorient ourselves, pick a route to explore, and move forward in another direction. And then we do the same dance again, and yet again until we have fulfilled our intent. In many ways, this process is similar to writing an article like this one. There is a general idea that drives the article forward, but there are stumbling blocks and reconsiderations that pull you back.

On the web, this happens especially when we end up on a page that seems to be **leading nowhere**, has outdated content, doesn’t expose a much-needed feature, or when our search query is too ambiguous to provide accurate and relevant results.

{{< rimg href="https://www.deutsche-bank.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ced0d81b-78f5-476e-b49e-4bc85a9b6ce3/29-deutsche-bank-designing-better-breadcrumbs.png" width="800" height="491" sizes="100vw" caption="Deutsche Bank’s navigation doesn’t highlight where the user currently is. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ced0d81b-78f5-476e-b49e-4bc85a9b6ce3/29-deutsche-bank-designing-better-breadcrumbs.png'>Large preview</a>)" alt="Deutsche Bank" >}}

One simple test that we frequently use is to give a user an URL and ask them to explain in which section of the website they currently are, and also **locate similar**, or related sections. In the [Deutsche Bank](https://www.deutsche-bank.de/pk/sparen-und-anlegen/geldanlage-online/wertpapiersparplan.html) example above, it would be a little bit difficult since there are no highlights of the current page in the navigation.

{{< rimg href="https://www.deutsche-bank.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89557a2c-bd0b-4a90-b045-75fcfaa00198/30-deutsche-bank-2-designing-better-breadcrumbs.png" width="800" height="440" sizes="100vw" caption="The current level of navigation isn’t highlighted in the navigation bar by default. (<a href=''>Large preview</a>)" alt="Deutsche Bank" >}}

As it turns out, we are in the third level of navigation. Usually “Sparen and Anlegen” should be active and highlighted on the page, but it isn’t. It’s only when we open a hover menu that we can spot what the current page actually is (“Online Weltpapier Sparplan”). Navigating backwards is a little bit cumbersome on Deutsche Bank.

### Sideways Navigation

As if it wasn’t enough with all the going back and forth, sometimes we also move *sideways* &mdash; fiercely jumping up and down between various levels and sections and pages and sub-categories. This usually happens when we want to **explore similar topics** or related pages, or explore more information that’s in some way connected with the current page.

This also happens when we are browsing through available options and haven’t made up our minds yet. Basically, we explore, browse and click around trying to create a comprehensive picture of what we have in front of us.

<!-- On [Austrian Postal Service](https://www.post.at/en/p/c/customs-information-international-parcel), it’s not obvious that breadcrumbs are clickable, and they are slightly difficult to tap on, even if one discovered that they are indeed links. A bit of spacing and a bit of underlining would go a long way here. -->

{{< rimg breakout="true" href="https://www.post.at/en/p/c/customs-information-international-parcel" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/968e674d-efec-49a0-9363-3a996cf611fe/65-economist-designing-better-breadcrumbs.png" width="800" height="512" sizes="100vw" caption="<a href='https://www.post.at/en/p/c/customs-information-international-parcel'>Austrian Postal Service</a> supports sideways navigation with an Additional information sidebar on the right. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/968e674d-efec-49a0-9363-3a996cf611fe/65-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

And as we do, we need signposts that guide us in the right direction. In fact, given how much movement is happening, having a consistent and predictable **trace of how we navigate** is surely helpful. In fact, that’s exactly what breadcrumbs provide.

At the first glance, it might seem that **breadcrumbs** are helpful only for backward navigation, but often we use them to move back, find a better route and move forward again. In that way, they serve all directions of navigation, and they do it well.

## When Do We Need Breadcrumbs?

One might wonder at first if breadcrumbs are actually still necessary these days. We surely must have learned a thing or two about designing navigation menus over the decades, and search has become incredibly precise in pointing users to the right direction. Indeed, **smaller websites can be very effective** without having to rely on breadcrumbs at all.

This also holds true if a website has quite a few sections, but **doesn’t contain many nested levels**. Then, indicating what category a given page belongs to, or the tags associated with the page, is perfectly sufficient.

{{< rimg breakout="true" href="https://www.economist.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adf27936-48a7-41c5-a666-0b8957e6a404/48-economist-designing-better-breadcrumbs.png" width="800" height="275" sizes="100vw" caption="Because The Economist has a quite flat navigation, indicating what category a page belongs to might be enough. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adf27936-48a7-41c5-a666-0b8957e6a404/48-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="The Economist" >}}

That’s the case on [The Economist](https://www.economist.com/), for example. The website does contain a lot of topics to browse through, but it doesn’t contain multiple levels of navigation. In fact, the navigation structure is quite flat: much of the content comfortably sits on the same level. If we were to add breadcrumbs in this case, most breadcrumbs wouldn’t contain more than one section anyway. Instead, the designers of the site chose to **display the section prominently next to the title**. This is reasonable because it actually serves exactly the same purpose.

{{< rimg breakout="true" href="https://www.economist.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34b56469-2b0d-4074-b797-0b914299463e/02-the-economist-designing-better-breadcrumbs.png" width="741" height="565" sizes="100vw" caption="“The Economist” doesn’t use breadcrumbs but clearly indicates where the user currently is next to the title. One needs to learn that it’s actually a link though. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34b56469-2b0d-4074-b797-0b914299463e/02-the-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="The Economist" >}}

Not every website is like that though. As sites start to grow and gain **more levels of navigation**, eventually it becomes very difficult to gain a quick understanding of available options. For example, if a user has landed on the 4th level of navigation, but this isn’t clearly labeled on the page, they will have a quite hard time trying to explore similar items.

The bigger problem is that most complex sites have plenty of issues related to **content** as well. Often labels and headings are ambiguous. Or multiple sections have sub-sections with the same titles, so it’s not clear what exactly a particular page refers to. Or the content uses internal vocabulary that makes it difficult to understand if it’s intended for you. Or perhaps there are multiple points of entry to the website, but it’s impossible to easily find out which one you’re currently at, or which one is a better fit.

{{< rimg breakout="true" href="https://www.nejm.org/doi/full/10.1056/NEJMp2200422" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f78f1de-0a80-40ce-b935-e3f3a729d50a/01-nejm-designing-better-breadcrumbs.png" width="800" height="534" sizes="100vw" caption="It’s difficult to say where exactly one is in the hierarchy of the site. “Perspective” above the heading is a link, but it’s not obvious. Breadcrumbs might be helpful here. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f78f1de-0a80-40ce-b935-e3f3a729d50a/01-nejm-designing-better-breadcrumbs.png'>Large preview</a>)" alt="New England Journal of Medicine" >}}

At the first glance, it’s difficult to say where exactly one is on the [New England Journal of Medicine](https://www.nejm.org/doi/full/10.1056/NEJMp2200422). **There isn’t a clear label** for the current category that one would immediately understand. If you’d like to explore more related articles, how would you navigate there? As it turns out, “Perspective” above the heading is actually a category *and* a link to that category, but because it’s appearing in light grey, it doesn’t look like an interactive element. To explore more, we’d need to click there, yet it’s not necessarily obvious to everyone.

Many complex projects will have *some* sort of breadcrumbs. They are often added to support **users coming via search results**, news feeds, or personal messages, who don’t have any prior knowledge of the website and how it’s organized. In such cases, breadcrumbs help users quickly understand where they have landed. In fact, on informational websites, users often heavily rely on them to explore the site.

<!-- [Unilever](https://www.unilever.com/planet-and-society/raise-living-standards/strategy-and-goals/) drops one of the intermediate levels, keeping Home and the parent of the current page visible on mobile. This might create some confusion, as users might be expecting to find sections similar to “Raise living standards” in the primary navigation. It’s not there though: related sections are placed under “Planet and Society”.  -->

{{< rimg breakout="true" href="https://www.unilever.com/planet-and-society/raise-living-standards/strategy-and-goals/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e152a6c5-f2a7-4ad0-ba1d-9685055b22d8/67-economist-designing-better-breadcrumbs.png" width="741" height="455" sizes="100vw" caption="Larger websites like <a href='https://www.unilever.com/planet-and-society/raise-living-standards/strategy-and-goals/'>Unilever</a> will probably need breadcrumbs to allow jumpts between multiple levels of navigation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e152a6c5-f2a7-4ad0-ba1d-9685055b22d8/67-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}


In summary, as long as you have a relatively **shallow navigation tree**, you probably won’t need breadcrumbs. Neither will you need them when finding the right page on the site isn’t the priority for most users. If, for example, they explore data, filter tables, manage accounts or use search frequently, breadcrumbs won’t be of much help.

But if you have plenty of pages and sub-categories and nested navigation levels, or your navigation grows to **three, four or even more levels**, your users are likely to benefit from reliable signposts along their journey. That’s where breadcrumbs prove to be essential.

The question, then, is how to make them noticeable and helpful without being redundant and unnecessary? As it turns out, that’s an art and craft of its own.

{{% feature-panel id="vitaly-friedman" %}}

## A Short Story Of Confused Breadcrumbs

There doesn’t seem to be any other interface component that’s seemingly as consistent as breadcrumbs. After all, there are links to sections, and they are separated by some sort of a delimiter. And most of the time, that delimiter is an arrow or a chevron, which also indicates relationships.

But where should these icons **actually point to**? Should breadcrumbs indicate where each item lives (icon pointing to the left), or rather the path that a user has taken so far (icon pointing to the right)? After all, when using breadcrumbs, users will be navigating backward, not forward.
  
{{< rimg breakout="true" href="https://www.su.se/english/research/news-research/ai-finds-the-best-ideas-1.606746" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a221a5eb-100a-4eab-a81a-e9f78f815990/50-economist-designing-better-breadcrumbs.png" width="741" height="379" sizes="100vw" caption="<a href='https://www.su.se/english/research/news-research/ai-finds-the-best-ideas-1.606746'>Stockholm University</a> with chevrons pointing to the left. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a221a5eb-100a-4eab-a81a-e9f78f815990/50-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

On the [Stockholm University website](https://www.su.se/english/research/news-research/ai-finds-the-best-ideas-1.606746), chevrons reluctantly point to the left. Since breadcrumbs are usually explored right to left, the icons indicate where a particular section or page lives.

{{< rimg breakout="true" href="https://www.tvm.nl/verzekeringen/weg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be54869f-b733-483e-b88b-b14b360f43b3/59-tvm.png" width="741" height="504" sizes="100vw" caption="<a href='https://www.tvm.nl/verzekeringen/weg'>TVM</a>, with arrows pointing to the left in the breadcrumbs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be54869f-b733-483e-b88b-b14b360f43b3/59-tvm.png'>Large preview</a>)" alt="" >}}

On [TVM](https://www.tvm.nl/verzekeringen/weg), arrows indicate where a particular section or page belongs too. The last item in the breadcrumbs (*Huidige pagina*) means "Current page". It’s reasonable to assume that some users might think that the page it’s pointing towards is the current page.

{{< rimg breakout="true" href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8aadbab7-16e3-4d69-ad5e-31f53e1ce2cf/27-kbc-breadcrumbs-change-designing-better-breadcrumbs.png" width="741" height="514" sizes="100vw" caption="<a href='https://www.kbc.be/particulieren/nl/sparen/spaarrekeningen/spaarrekening.html?zone=topnav'>KBC</a>, with chevrons pointing to the right. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8aadbab7-16e3-4d69-ad5e-31f53e1ce2cf/27-kbc-breadcrumbs-change-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

On [KBC](https://www.kbc.be/particulieren/nl/sparen/spaarrekeningen/spaarrekening.html?zone=topnav), chevrons are pointing to the right are much more conventional and familiar to users. The delimiter could also be an arrow, and it’s only beneficial if all links in the breadcrumbs are actually underlined. This sets the right expectations early on. 

It’s reasonable to assume that users will find their way in both directions — left and right — but historically in left-to-right interfaces relationships are indicated with **icons pointing to the right**. The direction indicates that a category contains another page or category; and because we usually consider browsing through pages as a *horizontal* experience projected onto a timeline, we are usually moving from left to right. So it’s definitely safe to stay true to this approach: it’s just more familiar to users this way.

{{% ad-panel-leaderboard %}}

## Breadcrumbs Work Best Under Global Navigation

To help users understand where they are, **breadcrumbs need to be visible** to users. This seems to be quite obvious at first, yet in practice, breadcrumbs appear all over the map. Sometimes you can find them in under the main promo header, sometimes close to the top of the page, sometimes on images, and sometimes in the footer. So what’s the right position for breadcrumbs?

{{< rimg breakout="true" href="https://shop.deutschepost.de/shop/internetmarke/imConfiguration.jsp?_requestid=1496269#/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7854600-2e8a-4564-9536-5cc5b4d9a393/63-economist-designing-better-breadcrumbs.png" width="800" height="581" sizes="100vw" caption="<a href='https://shop.deutschepost.de/shop/internetmarke/imConfiguration.jsp?_requestid=1496269#/'>Deutsche Post</a>, with the breadcrumbs appearing under the main navigation bar. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7854600-2e8a-4564-9536-5cc5b4d9a393/63-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

It’s common to see breadcrumbs appearing **all the way on the top of the page**, and it’s a perfectly reasonable option to choose. [Deutsche Post](https://shop.deutschepost.de/shop/internetmarke/imConfiguration.jsp?_requestid=1496269#/), a German postal service (pictured above), is just an example of that. In fact, that’s where many users search for breadcrumbs first, because they associate them with navigation.

{{< rimg breakout="true" href="https://www.gothaer.de/privatkunden/tierversicherung/tierhalterhaftpflicht/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/456f30f4-1f73-4dd6-8d5e-309de43c2c39/14-gothaer-footer-designing-better-breadcrumbs.png" width="741" height="436" sizes="100vw" caption="<a href='https://www.gothaer.de/privatkunden/tierversicherung/tierhalterhaftpflicht/'>Gothaer</a>, with breadcrumbs appearing at the bottom of the page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/456f30f4-1f73-4dd6-8d5e-309de43c2c39/14-gothaer-footer-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

Not every website follows this pattern though. On many of its pages, [Gothaer](https://www.gothaer.de/privatkunden/tierversicherung/tierhalterhaftpflicht/) displays breadcrumbs **just above the footer**. It’s probably not the first spot where users would search for it though. The website does look wonderful, but the position of breadcrumbs might not be obvious and is probably suboptimal.

<!-- {{< rimg breakout="true" href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b12f2e1e-bbbb-4f41-bbf8-77a05cfc511e/12-banner-designing-better-breadcrumbs.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b12f2e1e-bbbb-4f41-bbf8-77a05cfc511e/12-banner-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

On [Independer.nl](https://www.independer.nl/autoverzekering/info/bereken-dagwaarde), even though the breadcrumbs are **disconnected from the title** of the page with a blue banner, they are easy to spot, and clearly marked as links. Still bringing them closer together might be worth considering. -->

{{< rimg breakout="true" href="https://www.dhl.de/en/privatkunden/pakete-versenden/deutschlandweit-versenden/preise-national.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b64539ba-57c9-4d58-ae85-7bd216966376/52-economist-designing-better-breadcrumbs.png" width="741" height="444" sizes="100vw" caption="On <a href='https://www.dhl.de/en/privatkunden/pakete-versenden/deutschlandweit-versenden/preise-national.html'>DHL</a>, one might skip the banner altogether due to advertising blindness. The image though isn’t an ad. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b64539ba-57c9-4d58-ae85-7bd216966376/52-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

[DHL](https://www.dhl.de/en/privatkunden/pakete-versenden/deutschlandweit-versenden/preise-national.html) displays the breadcrumbs **under its primary header image**. While it does fit the overall design of the page, users often dismiss banner-alike images instinctively, mostly because they don’t find anything useful there. “Standard shipping” does appear as some sort of title, yet it doesn’t show up in the breadcrumbs. 

The text on the banner is actually the title of the page. “Standard shipping”, on the other hand, is one of the sub-sections on the current page. The breadcrumbs above “Standard shipping” seem to **relate more to the banner**, rather than to the sub-section displayed under it. This might be confusing to some users.

{{< rimg breakout="true" href="https://www.allianz.de/auto/kfz-versicherung/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01159a29-f275-4e92-999c-2b45a10e9b0e/53-economist-designing-better-breadcrumbs.png" width="741" height="463" sizes="100vw" caption="<a href='https://www.allianz.de/auto/kfz-versicherung/'>Allianz.de</a>, with the breadcrumbs appearing in teh top area of the banner. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01159a29-f275-4e92-999c-2b45a10e9b0e/53-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

In contrast, on [Allianz.de](https://www.allianz.de/auto/kfz-versicherung/), breadcrumbs are positioned **on top of the header image**, easy to spot and easier to connect with that header. It appears to be just a bit more obvious this way. The only refinement could be subtle underlines to indicate that each breadcrumb is actually a link.

{{< rimg breakout="true" href="https://www.swisslife.de/pk/versicherungen/berufsunfaehigkeitsversicherung.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5231a212-45d0-45f7-968b-06eca087edb9/21-swisslife-designing-better-breadcrumbs.png" width="741" height="410" sizes="100vw" caption="<a href='https://www.swisslife.de/pk/versicherungen/berufsunfaehigkeitsversicherung.html'>SwissLife</a>, with breadcrumbs and benefits shown and displayed on the header banner. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5231a212-45d0-45f7-968b-06eca087edb9/21-swisslife-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

A similar website, a similar industry, but organized slightly differently: [SwissLife](https://www.swisslife.de/pk/versicherungen/berufsunfaehigkeitsversicherung.html). There are multiple levels of navigation on the top, with **breadcrumbs above the heading** and placed on top of the image. Unlike in the previous example, here the header is more useful — just also unfortunately much more difficult to read. The text could live on a darker background, for example. The overall design pattern though seems to be quite right, now with useful content appearing right in the header area.
 
{{< rimg breakout="true" href="https://www.sdu.dk/en/om_sdu/international_staff/living+in+denmark/insurance/health+insurance" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84fdc345-ca92-42fe-aa03-dda00ea3db6b/22-sdu-designing-better-breadcrumbs.png" width="741" height="395" sizes="100vw" caption="<a href='https://www.sdu.dk/en/om_sdu/international_staff/living+in+denmark/insurance/health+insurance'>SDU</a>, with a dedicated area for breadcrumbs. The chevrons pointing to the right. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84fdc345-ca92-42fe-aa03-dda00ea3db6b/22-sdu-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

On [SDU](https://www.sdu.dk/en/om_sdu/international_staff/living+in+denmark/insurance/health+insurance), breadcrumbs live under the main navigation and **just above the title of the page**, in a dedicated area, housing multiple levels of navigation if needed. All of them are links, except the last item which is a label, highlighted in bold.

When we land on an unknown page, we tend to first verify that they are on the right page. Obviously, we seek confirmation that they are still on the right path towards their goal. Naturally, we focus on the main heading of the page, and sometimes on tags and sidebar links to get the confirmation that we need.

If at any point we need to move backwards or sideways, we need to be able to find breadcrumbs immediately. Displaying breadcrumbs **just under the main navigation** or just above the main heading is the most obvious and familiar way to achieve just that.

## Breadcrumbs Should Be Visible Without Scrolling

Yet even if breadcrumbs live above the main heading, it doesn’t mean that they are easy to use. In fact, the further we move breadcrumbs away from the top of the page, the more difficult they are to spot. This might sound like quite an exaggeration, but if you look closely at the example below ([LVK.fi](https://www.lvk.fi/korvaukset/ilmoita-vahinko-ja-hae-korvausta-lvksta/luottamuksellisten-asiakirjojen-lahettaminen-suojatulla-sahkopostilla/)), can you actually spot where the breadcrumbs are hiding?

{{< rimg breakout="true" href="https://www.lvk.fi/en/compensation/claim-compensation-from-lvk/sending-confidential-documents-by-secure-email/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56386702-145d-47ef-9f08-cba59ce5a98f/11-lvk-designing-better-breadcrumbs.png" width="741" height="418" sizes="100vw" caption="On <a href='https://www.lvk.fi/en/compensation/claim-compensation-from-lvk/sending-confidential-documents-by-secure-email/'>LVK</a>, breadcrumbs are hiding somewhere. Where could they possibly be? (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/56386702-145d-47ef-9f08-cba59ce5a98f/11-lvk-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

Yes, it was indeed a bit of a tricky question. Of course, the breadcrumbs are hiding behind the sticky cookie consent prompt. With the global navigation and a sticky navigation bar, along with a large visual promo area on the top, we end up with almost **0% of the screen dedicated to the content** that the user has come to explore on the site. In fact, much of the site is polluted with navigation, not content.

This alone is a bit suboptimal, but it also has a negative side effect. While the composition of the page might be beautiful and visually pleasing, now every time a user wants to explore any page, they **need to scroll down one full page** to get to the first sentence of the actual information on the page.

{{< rimg breakout="true" href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6d05f0f-a41a-4cea-925f-473adfe2a6a3/11-lvk-3-designing-better-breadcrumbs.png" width="741" height="385" sizes="100vw" caption="Users have to scroll full page every time they want to read the content on the page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6d05f0f-a41a-4cea-925f-473adfe2a6a3/11-lvk-3-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

This problem is **slightly more critical** than it might appear at the first glance. Of course, users know how to scroll, and they do scroll vigorously. But if every time you move from one page to another, you need to scroll a full page to start reading that page, you might be less inclined to browse more, so we shouldn’t be expecting people to browse through a lot of pages and finding what they seek. And with people leaving the site, that extra scroll on every page can quickly become quite damaging and **quite expensive**.

{{< rimg breakout="true" href="https://www.gu.se/en/study-in-gothenburg/study-options/masters-programmes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8f211d6-f8c6-44a6-a7b4-6a71a135b85b/54-economist-designing-better-breadcrumbs.png" width="771" height="446" sizes="100vw" caption="<a href='https://www.gu.se/en/study-in-gothenburg/study-options/masters-programmes'>University of Gothenburg</a> reserves most of the screen estate to navigation. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8f211d6-f8c6-44a6-a7b4-6a71a135b85b/54-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

On the [University of Gothenburg](https://www.gu.se/en) website, much of the screen space is used for navigation menus and visuals. Every time a user wants to explore a page's content, they need to scroll the entire screen first. It might help to change the aspect ratio a little to help users focus on the content of the page.

{{< rimg breakout="true" href="https://www.ubs.com/ch/de/private/mortgages/guide/maintenance.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/498ce280-f9f8-47ee-8fbd-52bcf5915fb3/20-ubs-designing-better-breadcrumbs.png" width="741" height="415" sizes="100vw" caption="<a href='https://www.ubs.com/ch/de/private/mortgages/guide/maintenance.html'>UBS</a> doesn’t require any scrolling to display the content. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/498ce280-f9f8-47ee-8fbd-52bcf5915fb3/20-ubs-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

No need to scroll on [UBS](https://www.ubs.com/ch/de/private/mortgages/guide/maintenance.html). The sidebar navigation is **stable and consistent**, and users can explore the content immediately across many sections in the left sidebar. No breadcrumbs are needed here either.

It’s worth testing if **removing a promo banner** has any impact on the design KPIs outlined earlier in the article. Of course, sometimes we want to leave a lasting impression, but sometimes we want to communicate information, and a visual would just get in the way. Boring? Maybe. But effective.

{{< rimg breakout="true" href="https://www.signal-iduna.de/krankenzusatzversicherung/ambulante-zusatzversicherung.php" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d1a1833-8519-4726-b89b-2c60d78bc6fe/15-signal-iduna-designing-better-breadcrumbs.png" width="800" height="482" sizes="100vw" caption="<a href='https://www.signal-iduna.de/krankenzusatzversicherung/ambulante-zusatzversicherung.php'>Signal Iduna</a>, with the breadcrumbs appearing right under the top navigation: no scrolling required. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d1a1833-8519-4726-b89b-2c60d78bc6fe/15-signal-iduna-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

Also a little bit less exciting, but a little bit more predictable and easier to spot. On [Signal Iduna](https://www.signal-iduna.de/krankenzusatzversicherung/ambulante-zusatzversicherung.php) the breadcrumbs are displayed at the **very top of the page**, under the main navigation and above the call to action. A good reference example to keep in mind when designing breadcrumbs navigation for a corporate landing page.

{{< rimg breakout="true" href="https://www.bag.admin.ch/bag/de/home/versicherungen/krankenversicherung/krankenversicherung-das-wichtigste-in-kuerze.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86c3be6a-587e-49fe-b9eb-d947024763c7/16-bundesrat-designing-better-breadcrumbs.png" width="800" height="664" sizes="100vw" caption="Why not use two sets of breadcrumbs navigation? One for the family of websites, and one for the sections on a site. Example: <a href='https://www.bag.admin.ch/bag/de/home/versicherungen/krankenversicherung/krankenversicherung-das-wichtigste-in-kuerze.html'>BAG Switzerland</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86c3be6a-587e-49fe-b9eb-d947024763c7/16-bundesrat-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

One could of course go even further, and place the breadcrumbs all the way on the top of the page, **above primary navigation**, and above the logo — that’s exactly what the designers of [Bundesrat Switzerland](https://www.bag.admin.ch/bag/de/home/versicherungen/krankenversicherung/krankenversicherung-das-wichtigste-in-kuerze.html) have chosen to do.

In this particular case, breadcrumbs act as *global* type of breadcrumbs navigation allowing for jumps between a larger family of websites, not sections on a given website. This goes very much in line with Erik D. Kennedy’s [laws of locality](https://learnui.design/blog/the-3-laws-of-locality.html). Indeed, that’s exactly what the navigation is, and it’s not to be mistaken for a more common breadcrumbs navigation we’ve explored earlier.

In summary, a simple way to ensure that breadcrumbs are found and understood easily is to **always keep the breadcrumbs visible without scrolling**, and preferably close to the main heading of the page. That’s where users expect to find a confirmation and some clues about where they currently are.

{{% ad-panel-leaderboard %}}

## Avoid “Disabled” Breadcrumbs

If you take a closer look at the previous examples, do you see any inconsistencies in their designs? In some implementations breadcrumbs are merely a **text label** representing the structure of the site; in others, each breadcrumb is actually **a link** guiding to separate sections of a site.

And on some websites breadcrumbs are a sort of *choose-your-own-adventure* game. Some breadcrumbs are links, while others are *disabled*, merely representing the location of a given page in the overall hierarchy of the website.

{{< rimg breakout="true" href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba552d9-6ef6-465b-b0a4-c324b5e3d744/10-sparkasse-designing-better-breadcrumbs.png" width="800" height="621" sizes="100vw" caption="Some breadcrumbs are accessible, while others aren’t. Example: <a href='https://www.sparkasse.de/unsere-loesungen/privatkunden/karten.html'>Sparkasse</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ba552d9-6ef6-465b-b0a4-c324b5e3d744/10-sparkasse-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

In [Sparkasse](https://www.sparkasse.de/unsere-loesungen/privatkunden/karten.html)’s breadcrumbs, “Startseite” (Homepage) and “Karten” are actually links, but the sections in between are not. There might be very good reasons for this decision, but the general expectation is very clear: all breadcrumbs are links.

Removing *some* links from *some* breadcrumbs can be confusing, and is likely to cause a few hefty rage clicks. In fact, it wouldn’t be surprising to discover that these inaccessible breadcrumbs get quite a few **rage clicks**: even though they might look different, it doesn’t necessarily mean that they will not work. After all, they might appear different because these sections have been visited previously.

<!-- For the other breadcrumbs though, we want users to be able to navigate quickly, should it be desired. So it only makes sense to link all crumbs to corresponding sections if possible.  -->

{{< rimg href="https://www.bahn.de/angebot/bahncard/bahncard50" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63afa629-bc71-4864-a65f-e1dee44f7747/31-db.png" width="741" height="254" sizes="100vw" caption="Some people might assume that the last breadcrumb is a parent category of the current page on <a href='https://www.bahn.de/angebot/bahncard/bahncard50'>Deutsche Bahn</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63afa629-bc71-4864-a65f-e1dee44f7747/31-db.png'>Large preview</a>)" alt="" >}}

Do we know if the current page is a link or not? On [Deutsche Bahn](https://www.bahn.de/angebot/bahncard/bahncard50), the styles for text labels and links are identical &mdash; unless you start hovering or tabbing through the sections. Plain underlines would make it slightly more obvious.

In general, if a component in the interface behaves differently or serves an important or different purpose, we make it stand out by highlighting it in some way. In the case of breadcrumbs, there are **two different types of crumbs**: the current page (if we choose to display it), and the breadcrumbs on the path to that page.

{{< rimg href="https://www.bahn.de/angebot/bahncard/bahncard50" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/851944dd-abc4-4068-87ec-da75757a6047/32-db-underlined.png" width="741" height="254" sizes="100vw" caption="Just a bit of underline can go a long way. A mock-up based on <a href='https://www.bahn.de/angebot/bahncard/bahncard50'>Deutsche Bahn</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/851944dd-abc4-4068-87ec-da75757a6047/32-db-underlined.pngg'>Large preview</a>)" alt="" >}}

The current page shows where a user currently is, and there is no need to navigate there because the user is there already. However, if that page looks exactly like the rest of the breadcrumbs, it suggests that they all have a similar function, or that they all are links. 

This brings another problem along: depending on the title of that last breadcrumb, you can observe users assuming that the last appearing item **isn’t current page**, but a parent of the page. Consequently, willing to move back, they click on that last item, but indeed nothing happens. That’s confusing, too.

To avoid that conundrum altogether, we can either display the current page differently or avoid it altogether.

<!-- 
{{< rimg href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/499cc9f6-9662-4fbf-9f64-654e24d1f069/09-finanstylsynet-designing-better-breadcrumbs.png" width="800" height="523" sizes="100vw" caption="<a href='https://www.finanstilsynet.no/'>Finanstilsynet</a>: it doesn’t get more obvious than this. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/499cc9f6-9662-4fbf-9f64-654e24d1f069/09-finanstylsynet-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

[Finanstilsynet](https://www.finanstilsynet.no/) is infinitely less exciting, but very difficult to get wrong. There is a clear difference between links and a label, everything is easy to read and understand. Perhaps boring isn’t that bad after all. -->

{{< rimg breakout="true" href="https://www.gov.uk/apply-funding-community-project" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76cb7ee6-f1fe-4fdd-83d4-13a6f714e2f8/28-gov-uk-designing-better-breadcrumbs.png" width="800" height="566" sizes="100vw" caption="Breadcrumbs on <a href='https://www.gov.uk/apply-funding-community-project'>Gov.uk</a> don’t include the current page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76cb7ee6-f1fe-4fdd-83d4-13a6f714e2f8/28-gov-uk-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

In fact, it’s removing the current page altogether that [Gov.uk](https://www.gov.uk/apply-funding-community-project) has [opted in](https://design-system.service.gov.uk/components/breadcrumbs/). The current page isn’t displayed in the breadcrumbs. Every breadcrumb that is displayed is a link, with proper `:active` and `:focus` states for keyboard users. It seems to be working well though because the breadcrumbs are located right above the heading.

## That Question About That Last Item

As we saw in the previous section, one fine little detail where breadcrumb designs often differ is the **presence of the current page** in the breadcrumbs. After all, the current page is indicated through the heading right under the breadcrumbs, so is it necessary to duplicate it? On the images below, one example includes the current page in breadcrumbs ([DocuSign Developer](https://developers.docusign.com/docs/esign-rest-api/how-to/code-launchers/)), and on the other, it does not ([Stripe Docs](https://stripe.com/docs/payments/cards/overview)).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29eb5e1f-b878-4f27-a7c9-0df164fda885/73-economist-designing-better-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29eb5e1f-b878-4f27-a7c9-0df164fda885/73-economist-designing-better-breadcrumbs.png" width="741" height="711" sizes="100vw" caption="On the left: <a href='https://developers.docusign.com/docs/esign-rest-api/how-to/code-launchers/'>DocuSign Developer Docs</a>, on the right: <a href='https://stripe.com/docs/payments/cards/overview'>Stripe Documentation</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29eb5e1f-b878-4f27-a7c9-0df164fda885/73-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

It appears that **it doesn’t really matter that much** as long as breadcrumbs appear straight above headings. In that case, the last item can be dismissed as long as proper semantics is used to announce the heading to the screen reader. The further away breadcrumbs are from the heading, however, the more likely we are to include the current page in the breadcrumbs as well &mdash; just to provide more clarity.

{{< rimg breakout="true" href="https://www.kbc.be/particuliers/fr/produits/paiements/self-banking/sur-votre-smartphone.html?zone=topnav" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa910fb7-88d0-4723-867d-75b2e3fbdf46/55-economist-designing-better-breadcrumbs.png" width="800" height="317" sizes="100vw" caption="<a href='https://www.kbc.be/particuliers/fr/produits/paiements/self-banking/sur-votre-smartphone.html?zone=topnav'>KBC</a>, with the breadcrumbs appearing under the main banner. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa910fb7-88d0-4723-867d-75b2e3fbdf46/55-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

In the example above ([KBC](https://www.kbc.be/particuliers/fr/produits/paiements/self-banking/sur-votre-smartphone.html?zone=topnav)), the relationship between the heading and the breadcrumbs might not be as obvious as it is in the previous examples. Had we removed the current page from the breadcrumbs, users might be assuming that they are on a “Self Banking” page, which isn’t the case. Notice that the title appearing in breadcrumbs is the same as the heading of the page &mdash; this is helpful, but unfortunately isn’t always the case.

Another use case where keeping the current page in the breadcrumbs might make sense is if the **breadcrumbs navigation is sticky**. As users scroll down a potentially long page, they might be losing the context of what exactly they are looking at at this very moment. Keeping the current page in the breadcrumbs might serve as a good reference point in such a case.

Our ultimate goal with breadcrumbs is that users quickly understand what they are looking at and where they are. Both options provide that answer. As long as the breadcrumbs appear above headings, adding a current page to the breadcrumbs isn’t as necessary as one might think.

## Avoid Truncations and Use Accordions Instead

Websites with many levels of navigation often don’t have space to display the entire path with breadcrumbs. This is also true for pages that just happen to have very lengthy labels, especially in Finnish and German. One common way to deal with this problem is to **truncate** some intermediate steps in the breadcrumbs navigation.

{{< rimg breakout="true" href="https://www.tff.no/hoved/in-english/frontier-motor-insurance-in-norway/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/159a144c-86e9-4642-b534-d49c245cfb8b/17-frontier-designing-better-breadcrumbs.png" width="800" height="694" sizes="100vw" caption="Some items in the breadcrumbs are truncated on <a href='https://www.tff.no/hoved/in-english/frontier-motor-insurance-in-norway/'>TFF.no</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/159a144c-86e9-4642-b534-d49c245cfb8b/17-frontier-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

[Frontier Motor Insurance](https://www.tff.no/hoved/in-english/frontier-motor-insurance-in-norway/) **replaces some paths with an ellipsis**; the title is removed but the link is still there and can be explored. With this approach, we are cutting the breadcrumbs, making it more difficult for users to explore the full path.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa859a5b-04f4-458a-a0c4-1612a43fe747/69-economist-designing-better-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa859a5b-04f4-458a-a0c4-1612a43fe747/69-economist-designing-better-breadcrumbs.png" width="741" height="464" sizes="100vw" caption="Breadcrumbs wrapping onto mutiple lines. Usually taking up too much space that is limited already. <a href='https://www.dhl.de/en/privatkunden/pakete-versenden/deutschlandweit-versenden/preise-national.html'>DHL</a>, <a href='https://auspost.com.au/id-and-document-services/licence-renewals-and-applications/nt-driver-and-vehicle-services'>Australia Post</a>, <a href='https://www.scb.se/'>SCB.se</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa859a5b-04f4-458a-a0c4-1612a43fe747/69-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

One option is to display the entire breadcrumbs, **wrapped into multiple lines** (pictured above). Admittedly, this would take quite a bit of horizontal and vertical space on screens that don’t have much space anyway. Hence this can be quite problematic and is [often advised against](https://www.nngroup.com/articles/breadcrumbs/).


{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c72a1f89-68a4-4103-acd1-639a60358bf0/72-economist-designing-better-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c72a1f89-68a4-4103-acd1-639a60358bf0/72-economist-designing-better-breadcrumbs.png" width="741" height="452" sizes="100vw" caption="One item at a time on mobile on <a href='https://www.tvm.nl/verzekeringen/weg'>TVM</a>, <a href='https://www.uantwerpen.be/en/study/admission-and-enrolment/admission/academic-bachelor/'>University of Antwerp</a> and <a href='https://www.sdu.dk/da/om_sdu/international_staff/living+in+denmark/insurance/health+insurance'>Syddansk Universitat</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c72a1f89-68a4-4103-acd1-639a60358bf0/72-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

When there isn’t enough space to display full breadcrumbs, it’s common to see breadcrumbs displayed as only **one item at a time**. That’s reasonable but favors more jumps against faster interaction. The user has to go through multiple pages on mobile, and if they happen to be on a choppy connection, they might be better off using the navigation menu. Ideally, we could keep the breadcrumbs visible as much as necessary, without compromising the amount of displayed content on the page.

{{< rimg breakout="true" href="https://www.swisscom.ch/en/residential/plans-rates/inone-home/swisscom-blue-tv/offers.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/743dc7e2-7f9e-4cd0-a065-105aae039443/44-swisscom-desktop-designing-better-breadcrumbs.png" width="741" height="437" sizes="100vw" caption="Visible on desktop, <a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/61cafcd9-78fc-4ef5-a920-9204b7588097/43-swisscom-mobile-designing-better-breadcrumbs.png'>disappear on mobile</a>. On Swisscom, breadcrumbs aren’t accessible on mobile at all. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/743dc7e2-7f9e-4cd0-a065-105aae039443/44-swisscom-desktop-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

Other times breadcrumbs **disappear entirely**, like it currently is on [Swisscom](https://www.swisscom.ch/en/residential/plans-rates/inone-home/swisscom-blue-tv/offers.html). Then, users have to rely on global navigation every time they want to navigate, and often the current page has to be discovered through tiring drill-down navigation on a small screen.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd418a96-9e4c-42e5-a70b-342665573926/68-economist-designing-better-breadcrumbs.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd418a96-9e4c-42e5-a70b-342665573926/68-economist-designing-better-breadcrumbs.png" width="741" height="710" sizes="100vw" caption="Arrows everywhere! Designing a navigation within the parts of breadcrumbs can be a quite challenging task. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd418a96-9e4c-42e5-a70b-342665573926/68-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

Another option is to **add some sort of drop-down** to allow people to move between levels. In the [City of Düsseldorf](https://www.duesseldorf.de/einwohnerangelegenheiten/terminvereinbarung-in-den-duesseldorfer-buergerbueros.html) and [Federal Statistical Office Switzerland](https://www.bfs.admin.ch/bfs/en/home.html) that might be a little bit difficult to understand with a few too many arrows pointing to different directions.

<!-- {{< rimg breakout="true" href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edf3b8fe-af23-491e-ab3b-5f88ff535566/18-ausw-amt-designing-better-breadcrumbs.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/edf3b8fe-af23-491e-ab3b-5f88ff535566/18-ausw-amt-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}} -->

{{< rimg breakout="true" href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbe1868a-6509-4815-a94e-9a4d401658bf/70-economist-designing-better-breadcrumbs.png" width="741" height="461" sizes="100vw" caption="Displaying breadcrumbs without multi-line wrapping on mobile. This requires scrolling, but is compact and probably better than removing breadcrumbs altogether. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbe1868a-6509-4815-a94e-9a4d401658bf/70-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

A good compromise is to keep all breadcrumbs on the same line but **avoid multi-line wrapping**. [Deutschland Auswärtiges Amt](https://www.auswaertiges-amt.de/de/aussenpolitik/themen/humanitaere-hilfe/-/205110) displays the entire breadcrumb for lengthy titles, but if it doesn’t fit, it uses **fade-out** and encourages users to swipe left and right to explore the entire path. No breadcrumbs are truncated but require a bit of horizontal scrolling to be discovered.

The same pattern is being used on [ADAC](https://www.adac.de/rund-ums-fahrzeug/auto-kaufen-verkaufen/kauftipps/). An alternative option is to use a **swiper assistant** to move between levels predictably. [Süddeutsche Zeitung](https://www.sueddeutsche.de/politik/krieg-ukraine-russland-liveblog-sanktionen-un-sicherheitsrat-1.5559161) is using it for primary navigation, but it could be helpful for breadcrumbs as well.

{{< rimg breakout="true" href="https://ec.europa.eu/info/business-economy-euro/recovery-coronavirus/recovery-and-resilience-facility/finlands-recovery-and-resilience-plan_en#" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e23a2b80-f0ee-4d42-9e3a-997262315017/71-economist-designing-better-breadcrumbs.png" width="741" height="462" sizes="100vw" caption="<a href='https://ec.europa.eu/info/business-economy-euro/recovery-coronavirus/recovery-and-resilience-facility/finlands-recovery-and-resilience-plan_en#'>European Commission</a> with a breadcrumbs accordion. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e23a2b80-f0ee-4d42-9e3a-997262315017/71-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

On the [European Commission's website](https://ec.europa.eu/info/business-economy-euro/recovery-coronavirus/recovery-and-resilience-facility/finlands-recovery-and-resilience-plan_en#), the parent category of the current page is always displayed in full, but the parents of that section are truncated. However, when a user taps or activates the truncated area (which is a link), the entire breadcrumbs appear. Technically, it’s a **breadcrumbs accordion**. Also, notice the visual difference between the current page (text label) and breadcrumbs (links). That’s a great reference to keep in mind.

## Sideways Breadcrumbs

In all the examples above, breadcrumbs were mostly a static representation of the information architecture on the site. They support backward navigation, but moving forward or sideways always requires another click. There is an alternative way of helping users move forward faster. This requires a combination of breadcrumbs navigation and tap/click menus, also conveniently called **sideways breadcrumbs**.

At [ADAC](https://www.adac.de/produkte/versicherungen/autoversicherung/tarife-und-leistungen/) example below, breadcrumbs are sort of *extended* &mdash; with a drop-down that allows users to jump to other sections within the category quickly. That’s the notion of **sideways breadcrumbs** which provide quick access to the siblings of the current page.

{{< rimg breakout="true" href="https://www.adac.de/produkte/versicherungen/autoversicherung/tarife-und-leistungen/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99b98252-c838-4da1-9dc2-56e168c1b541/58-economist-designing-better-breadcrumbs.png" width="741" height="409" sizes="100vw" caption="<a href='https://www.adac.de/produkte/versicherungen/autoversicherung/tarife-und-leistungen/'>ADAC</a> uses sideways breadcrumbs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99b98252-c838-4da1-9dc2-56e168c1b541/58-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

The chevron in breadcrumbs might be missing to make it perfectly clear, but the design pattern per se is useful since it significantly **speeds up jumps between siblings**. We can think about it as an alternative approach to sidebar navigation which requires less vertical space and appears on demand. On mobile, breadcrumbs turn into a horizontal swiper with a drop-down that reveals all available options on tap or on enter.

{{< rimg breakout="true" href="https://www.duesseldorf.de/einwohnerangelegenheiten/terminvereinbarung-in-den-duesseldorfer-buergerbueros.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/459a3e45-620e-4068-a33c-47843ef6355f/60-economist-designing-better-breadcrumbs.png" width="741" height="393" sizes="100vw" caption="<a href='https://www.duesseldorf.de/einwohnerangelegenheiten/terminvereinbarung-in-den-duesseldorfer-buergerbueros.html'>City of Düsseldorf</a> with sideways breadcrumbs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/459a3e45-620e-4068-a33c-47843ef6355f/60-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

The [City of Düsseldorf](https://www.duesseldorf.de/einwohnerangelegenheiten/terminvereinbarung-in-den-duesseldorfer-buergerbueros.html) uses a similar pattern but rather than providing access to siblings of the current page, at first it seems to be providing quick jumps for siblings of the parent section. That’s not the case though. Surprisingly, the last item in the breadcrumb isn’t the current page but rather “other topics”, which also happens to be a drop-down. A bit surprising, but sideways breadcrumbs make their appearance here as well.

{{< rimg breakout="true" href="https://www.bfs.admin.ch/bfs/en/home.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea79fd0a-6a96-4163-b135-9e978b8e37ce/61-economist-designing-better-breadcrumbs.png" width="741" height="382" sizes="100vw" caption="<a href='https://www.bfs.admin.ch/bfs/en/home.html'>Federal Administration of Statistics</a> with a family of sideways breadcrumbs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea79fd0a-6a96-4163-b135-9e978b8e37ce/61-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

But of course, when we look into sideways breadcrumbs, we don’t have to use it only at the last level. [Federal Administration of Statistics in Switzerland](https://www.bfs.admin.ch/bfs/en/home.html) displays **global sideways breadcrumbs** that help users jump between different departments of the Federal Administration family of websites. The breadcrumbs are the first thing that users encounter on the site. Unfortunately, on mobile, breadcrumbs disappear entirely.

Like other navigation options, sideways breadcrumbs provide not only an overview of where a user currently is but also **relationships between sections**. Yet unlike other options, it doesn’t need much space to do that and often conveys a significant amount of information in a very small amount of space. As such, they can be very helpful and could be worth considering as a good extension of traditional breadcrumbs navigation.

## Breadcrumbs Alone Aren’t Enough

We’ve explored many examples of breadcrumbs so far, and in some way, they all support the navigation patterns that we explored early in the article. Admittedly, there are plenty of other solutions worth considering as well, and they don’t necessarily have to involve breadcrumbs. In fact, breadcrumbs alone aren’t sufficient to navigate the site easily &mdash; they **complement existing navigation patterns**, but can’t really replace them.

Let’s briefly explore how a combination of various options can help us resolve common issues around navigation.

### Horizontal Layering

One approach is to use **horizontal layering** &mdash; that is, displaying multiple navigation bars, one for each level of navigation. Thus, at any point, users can jump between levels, and they can see siblings of all sections in the hierarchy. [BBC](https://www.bbc.com/sport/rugby-union/60976996) is a great example of a large website using this very pattern at large (see image below).

{{< rimg breakout="true" href="https://www.bbc.com/sport/rugby-union/60976996" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abf5d51c-4536-4a02-be33-cfdf40e7b93d/49-economist-designing-better-breadcrumbs.png" width="800" height="455" sizes="100vw" caption="Horizontal layering on BBC: for each of the layers of navigation, we can jump between siblings, and we can locate our current position in the hierarchy (although “Rugby Union” might be highlighted as an active selection). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abf5d51c-4536-4a02-be33-cfdf40e7b93d/49-economist-designing-better-breadcrumbs.png'>Large preview</a>)" alt="BBC" >}}

### Sidebar Navigation

Another approach is to use a **sidebar navigation**. Rather than laying out navigation options horizontally, we can do so vertically. This gives us the flexibility to show more items on the page if needed, and easily open and close vertical accordions without ever covering some of the options (which would probably be the case with horizontal layering). That’s the pattern used consistently on [Statistics Sweden](https://www.scb.se/lamna-uppgifter/offentlig-sektor/regelverk-och-samrad/).

{{< rimg breakout="true" href="https://www.scb.se/lamna-uppgifter/offentlig-sektor/regelverk-och-samrad/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29d38084-9ccd-41a7-92e3-2844f57f3fae/06-scb-se-designing-better-breadcrumbs.png" width="800" height="470" sizes="100vw" caption="Sidebar navigation on the Statistics Sweden complements breadcrumbs and “See also” in the right sidebar. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29d38084-9ccd-41a7-92e3-2844f57f3fae/06-scb-se-designing-better-breadcrumbs.png'>Large preview</a>)" alt="Statistics Sweden" >}}

### Tags

With sidebar navigation, we indicate the relationships between subsections and allow users to jump between levels quickly. However, if we just want to indicate which category the page belongs to, we might be able to get away with using **tags** instead.

They don’t show the relationship of a current page within the hierarchy of the site, but it might be actually a better option if we have literally hundreds of “sections” on the page. Showing them in a horizontal or vertical bar just wouldn’t be possible.

{{< rimg breakout="true" href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d76e898-f015-4f2f-b63c-9d5dbfe2f7c6/05-the-economist-tags-designing-better-breadcrumbs.png" width="741" height="357" sizes="100vw" caption="<a href='https://www.nejm.org/'>Nejm</a> uses tags, but they appear only at the bottom of the article. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d76e898-f015-4f2f-b63c-9d5dbfe2f7c6/05-the-economist-tags-designing-better-breadcrumbs.png'>Large preview</a>)" alt="" >}}

Remember [The New England Journal of Medicine](https://www.nejm.org/)? As it turns out, it does use both tags and a sidebar navigation. Related items appear in the sidebar below the job board area, and the tags are displayed at the end of the page. While this might be working absolutely fine for frequent users of the site, it might be not as obvious to occasional users.

### Breadcrumbs

All the options listed above do provide a **sense of orientation**, but they also require quite a bit of horizontal or vertical space to do so. Throughout the entire user journey, they need to be visible to guide users moving from one page to the next. Should they disappear all of a sudden on one of the pages, users are very likely to get lost. Add to it a healthy dose of noise in the search results and a slightly cumbersome navigation, and we shouldn’t be too surprised that users have issues finding what they are looking for.

In contrast, **breadcrumbs** are concise, compact, focused, and do their job well. Rather than showing *all* levels of navigation, they indicate just where the page lives, along with quick access to all its parents, all the way to the homepage. And sometimes it’s exactly what is needed: not more, and not less.

<!-- <blockquote>When we start moving from one page to another, it’s easy to get lost in the myriad of pages without proper signposts all along the pathway. Because getting lost usually means high abandonment, often it’s a very expensive problem for businesses and organizations, small and large.</blockquote> -->


## Breadcrumbs Checklist

Not every breadcrumb navigation appears and works similarly.  We’ve seen a couple of very different patterns and fine little details in which breadcrumb design and implementation differ. 

As usual, here’s a general checklist of a few **important guidelines to consider** when designing better breadcrumbs:

- Breadcrumbs always need to complement main navigation.
- Breadcrumbs fit best **under global navigation**.
- They could also appear above main headings.
- The delimiter should be **pointing to the right** (in RTL interfaces).
- Breadcrumbs should be **visible without scrolling**.
- Avoid “disabled” breadcrumbs and turn all breadcrumbs into links.
- The current page can be dropped if breadcrumbs live above headings.
- Otherwise, include the current page in breadcrumbs for clarity.
- On mobile, use accordions to display a full path if needed.
- The parent of the current page should be visible at all times.
- **Sideways breadcrumbs** might be a quite surprising and useful discovery for your users.

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

- “[Breadcrumbs Guidelines for Mobile and Desktop](https://www.nngroup.com/articles/breadcrumbs/),” Hoa Loranger, Nielsen Norman Group
- “[Breadcrumbs in Web Design: Examples and Best Practices](https://www.smashingmagazine.com/2009/03/breadcrumbs-in-web-design-examples-and-best-practices/),” Jacob Gube, Smashing Magazine
- “[Effective Guidelines For Breadcrumb Usability And SEO](https://medium.com/usabilitygeek/12-effective-guidelines-for-breadcrumb-usability-and-seo-71de2202bdb9),” Justin Mifsud, Usability Geek

If you find this article useful, here’s an overview of similar articles we’ve published over the years &mdash; and a few more are coming your way.

### Related Articles

- [Designing A Perfect Accordion](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/)
- [Designing A Better Infinite Scroll](https://www.smashingmagazine.com/2022/03/designing-better-infinite-scroll/)
- [Designing A Perfect Responsive Configurator](https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/)
- [Designing A Perfect Birthday Picker](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/)
- [Designing A Perfect Date and Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
- [Designing A Perfect Feature Comparison](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/)
- [Designing A Perfect Slider](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/)

{{< signature "vf, il" >}}

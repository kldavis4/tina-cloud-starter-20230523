---
title: Navigation For Mega-Sites
slug: navigation-mega-sites
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c70093b9-c411-4b69-a093-64fceb20cc29/userinterfaces-11.png
date: 2013-03-27T20:40:30.000Z
author: paul-boag
description: >-
  For most websites, navigation is not particularly challenging. A primary
  navigation bar, supported by sub-navigation, is often enough. Typically,
  sub-navigation displays the parent, siblings and children of the current page.
categories:
  - Design
  - Web Design
  - Navigation
  - Content
  - UX
---
For most websites, navigation is not particularly challenging. A primary navigation bar, supported by sub-navigation, is often enough.

Typically, sub-navigation displays the parent, siblings and children of the current page. A persistent primary navigation bar shows top-level pages, allowing users to move between sections.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Navigation On Complex Websites](https://www.smashingmagazine.com/2013/09/responsive-navigation-on-complex-websites/)
*   [Breadcrumbs In Web Design: Examples And Best Practices](https://www.smashingmagazine.com/2009/03/breadcrumbs-in-web-design-examples-and-best-practices/)
*   [Responsive Upscaling: Large-Screen E-Commerce Design](https://www.smashingmagazine.com/2015/08/responsive-upscaling-large-screen-e-commerce-design/)
*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)

However, there is one class of website for which this traditional form of navigation falls short. It is what I refer to as a "mega-site".

{{% feature-panel %}}

## What Is A Mega-Site?

A mega-site is typically owned by a large organization that encompasses a broad range of services or products. The organization also often supports a diverse user base.

Organizations with mega-sites include institutions such as the <a href="https://bbc.co.uk">BBC</a>, companies with diverse portfolios such as <a href="https://www.microsoft.com">Microsoft</a>, government bodies, higher-education institutions and large charities that run many campaigns, such as the <a href="https://worldwildlife.org">World Wildlife Fund</a>.

These websites:

*   are extremely large,
*   are many levels deep,
*   are made up of many micro-websites and subsections,
*   cater to many audiences,
*   have multiple entry points.

Websites of this size and complexity bring some unique navigational challenges.</p>

## The Challenges Of Navigation On Mega-Sites

At our company, we do a lot of work on mega-sites, and they can prove to be particularly challenging, especially when trying to use traditional navigation.</p>

### Traditional Navigation Cannot Support Depth

The deeper the website, the more that traditional navigation struggles. Navigation can comfortably accommodate three levels; beyond that, one of two things happens. Either the navigation expands to the point where more screen real estate is dedicated to navigation than to content (a problem made worse by the sheer number of pages on a mega-site), or higher pages in the information architecture no longer appear in the navigation.

In the latter case, if the user is deep within the website, they <strong>will lose the context</strong> of where they are because they are not seeing where the current page fits in the website’s structure.

<a href="https://boagworld.com/wp-content/uploads/2013/02/unilever.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68537d2a-912c-4b89-a989-44d2f7dab37a/unilever-500.jpg" alt="Image showing navigation dominating page real estate" width="500" height="444" /></a><br>
<em>While traditional navigational approaches, combined with breadcrumbs, can scale to accommodate mega-sites, they do so at the cost of ever-increasing real estate. <a href="https://boagworld.com/wp-content/uploads/2013/02/unilever.jpg">Larger version</a>.</em>

The latter problem can be partially mitigated by well-implemented breadcrumbs. However, this is not the only issue with traditional navigation.

### Traditional Navigation Cannot Support Multiple Entry Points

Traditional navigation can confuse users who enter the website via a micro-site or subsection.

Take a student who is considering attending a university for post-graduate studies. This person is probably more interested in a particular faculty or school than in the institution as a whole. They could, therefore, very well enter the website at that level, rather than at the university’s home page.

Another example would be a single mother wanting to know about child benefits. They are more likely to arrive on the benefits subsite than on the government’s home page. In such situations, <strong>the user’s focus is on their current context</strong> (i.e. post-graduate studies or child benefits). They are not immediately interested in the broader mega-site.

Unfortunately, traditional primary and secondary navigation exposes the user to this broader context, whether they want it or not.

<a href="https://boagworld.com/wp-content/uploads/2013/03/uni-of-bath-670x508.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff476f9-3b38-4600-9741-b91bace47d11/uni-of-bath-670x508-500.jpg" alt="An example of a site with confusing navigational labels" width="500" height="379" /></a><br>
<em>Does a section labelled “Research” on a university’s page refer to the entire university or just the school being viewed? What about when the same label appears twice but goes to two separate places? <a href="https://boagworld.com/wp-content/uploads/2013/03/uni-of-bath-670x508.jpg">Larger version</a>.</em>

To make matters worse, the current context can actually alter the user’s perception of the navigation items. For example, would our post-graduate student think that a link labelled “About us” is about the school in question or about the larger institution. In some extreme cases, you can even find the same navigation labels being used for both the current context and the broader institution (for example, information about the university and about the school might both be labelled “About us” on the same page).

How, then, can we solve the navigation problems of mega-sites?

## Navigation Solutions

As with all things, there is no perfect solution. However, there are solutions that are a step forward from navigation better suited to small websites. The first of these solutions is the most radical.</p>

### Get Rid of Navigation Entirely

I first heard of this approach in <a href="https://www.r2.co.nz/20060525/russ.mp3">Russ Weakley’s talk about doing away with traditional navigation</a> back in 2006. It rejects the idea of imposing a navigational structure upon users, instead allowing them to find their own path through the website.

This is achieved by making each Web page a standalone document and tagging it with appropriate meta data. Users can then find pages through a combination of search and navigating by tags. Pulling in links to related documents based on the meta data associated with each page would also be possible.

This approach has <strong>several advantages</strong>:

*   It supports a website of limitless size.
*   It is ideally suited to users who come to the website from a deep link.
*   It allows for a much more dynamic relationship between pages and easily accommodates pages being added and removed.

Of course, it is not without its challenges. While individual sections of the website could still have a landing page (for example, <code>section.acme.com</code>), the business may well struggle with the idea of not having a specific website to manage. More importantly, this approach relies heavily on having well-tagged documents and powerful search functionality, both of which are hard to achieve with a mega-site.

That said, it is an option, and one that shouldn’t be quickly dismissed.</p>

### Split the Website Into Smaller Micro-Sites

Another approach is to break the mega-site into a number of smaller more manageable micro-sites. This is the approach adopted by the <a href="https://bbc.co.uk">BBC</a>.

Instead of treating its Web presence as a single entity, the BBC has broken it down into subsites, such as news, sports, TV, radio and so on. Each website has its own navigation and thus avoids the problems associated with mega-sites.

The way the BBC avoids a disjointed experience for users who move between micro-sites is to ensure consistency in top-level navigation and in the user interface.

<a href="https://boagworld.com/wp-content/uploads/2013/03/bbc-670x972.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50b6a311-b0f5-43a9-88bd-5272f0b54329/bbc-670x972-500.jpg" alt="BBC web presences" width="500" height="725" /></a><br>
<em>The BBC avoids being a mega-site by splitting its Web presence into a number of smaller websites, while maintaining consistency in navigation and design language. <a href="https://boagworld.com/wp-content/uploads/2013/03/bbc-670x972.jpg">Larger version</a>.</em>

Although the BBC’s micro-sites do vary in appearance, they make use of the same primary navigation, and also have a consistent design language for things like typography, layout and modules. This language, defined on the BBC’s <a href="https://www.bbc.co.uk/gel">Global Experience Language</a> (GEL) website, is consistent enough to ensure a stable user experience yet flexible enough to cater to different audiences and subject matter.

It is a fine line to walk. Make each micro-site too different and users will become confused by changes in the UI. Make them too similar and users will be thrown off upon finding that the website does not have a single navigational structure.</p>

### Use a Breadcrumb-Driven Approach

A third solution is the one adopted by <a href="https://gov.uk">Gov.uk</a>. It does away with dedicated areas for navigation, and instead uses the page’s content to link to its children. It then uses breadcrumbs to help the user identify where they are within the navigational hierarchy and to move back up the tree when needed.

<a href="https://boagworld.com/wp-content/uploads/2013/03/gov-uk-670x422.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d21a2a3c-81de-456b-96ed-954346bce2b8/gov-uk-670x422-500.jpg" alt="Gov.uk website" width="500" height="314" /></a><br>
<em>Gov.uk relies almost exclusively on breadcrumbs for navigation. <a href="https://boagworld.com/wp-content/uploads/2013/03/gov-uk-670x422.jpg">Larger version</a>.</em>

The approach has many advantages. For a start, it minimizes the space dedicated to navigation, while at the same time allowing for much more detailed descriptions of each child. In that sense, it is the simplest, cleanest and easiest to understand of the approaches.

It also translates well to mobile devices, which account for <a href="https://digital.cabinetoffice.gov.uk/2013/03/12/were-not-appy-not-appy-at-all/">45% of Gov.uk’s Web traffic</a>.

The prominent breadcrumbs make clear to the user where they are on the website, while in-page navigation to child pages makes the next step obvious. Most of all, the emphasis on content, rather than navigation, appeals to me the most.

<strong>Unfortunately, it does have its downsides</strong>.

By relying entirely on breadcrumbs and in-page links to children, the user has little context of their current position. They are unaware of the siblings of the current page and of the overall shape of the website (for example, they are unaware of the top-level sections).

This is not a problem if the user is trying to complete a specific task and the website has catered to that task by bringing all content related to it in a single place. However, when a user is in general research mode or when the content related to the task is spread across multiple pages, this approach can prove frustrating.

The frustration is caused by the breadcrumb navigation requiring the user to navigate up and down the website’s structure. There is no way to enable jumping between sections.

Fortunately, there is a hybrid approach, which uses breadcrumbs as the primary navigational tool, but augmented with more traditional navigation.</p>

## My Preferred Solution

My preferred solution is inspired by the navigational approach used by BBC Sports before GEL was introduced.

Instead of running them horizontally, the BBC flipped the traditional breadcrumbs vertically. At the end of each breadcrumb list, the current page also showed its children. When you reached the bottom of the tree, the navigation would continue to display the siblings of the current page, instead of its children.

<a href="https://boagworld.com/wp-content/uploads/2013/03/BBC-sports-old.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81bf78b4-0873-44e0-85c0-979e8e27f41d/bbc-sports-old-500.jpg" alt="Screenshot of the old BBC sports website" width="500" height="317" /></a><br>
<em>The old BBC Sports website used vertical breadcrumbs as the primary navigation tool. When the user entered a section, such as football, all other sports (i.e. the siblings) would be removed, focusing the user on the subject at hand. <a href="https://boagworld.com/wp-content/uploads/2013/03/BBC-sports-old.jpg">Larger version</a>.</em>

This approach grouped all navigation together in a single place, gave the user a clear sense of their location and reduced the space dedicated to navigation. Yet, it still suffered from the problems of Gov.uk.

When working on the <a href="https://brighton.ac.uk">University of Brighton</a>, we proposed BBC Sports’ approach, but added one important thing. We suggested keeping a consistent top-level navigation bar. While this adds more navigation to the page, it gives the user an instant overview of the structure of the website. This enables users who require information from multiple sections (say, a prospective student researching courses as well as accommodation) to jump quickly between those sections.

In many cases, this is enough to create a simple yet powerful user experience. However, it does not address the need to be able to see the siblings of the current page.</p>

## Showing Siblings While Using Breadcrumb Navigation

So far, I have considered two possible solutions to this issue.

One works on the assumption that siblings often have a relationship with each other; they are part of the same story, if you will. On that basis, the simple addition of “next” and “previous” buttons (such as you find on many blogs) might be enough of a solution. Users could then move between siblings with the single click of a button.

An alternative approach would be to make each level of the breadcrumb navigation a flyout menu, thereby exposing the siblings of that level. This would enable the user to jump to any sibling on any level of the website and potentially do away with the need for a separate primary navigation bar.

<a href="https://boagworld.com/wp-content/uploads/2013/03/vertical-breadcrumb-nav.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c114ff76-2dd5-4a4f-a6bc-6ed73dcab928/vertical-breadcrumb-nav-500.jpg" alt="An example of flyout breadcrumb navigation" width="500" height="314" /></a><br>
<em>By adding flyout menus to the vertical breadcrumb navigation, you give users quick access to any sibling on any level of the website. <a href="https://boagworld.com/wp-content/uploads/2013/03/vertical-breadcrumb-nav.jpg">Larger version</a>.</em>

This could work whether you use vertical breadcrumb navigation or traditional horizontal breadcrumbs.

That said, I haven’t tested this approach, and some will have concerns about touch devices.</p>

## More Ideas Needed

As you can see, the issue of navigation on mega-sites is a thorny one, and there does not seem to be a single obvious solution. One of the primary reasons for writing this post is to open a discussion on the subject and hopefully encourage the exploration of some alternative approaches.

As a result, I would really appreciate your thoughts in the comments section and any examples of alternative navigational approaches you have found.

{{< signature "al" >}}


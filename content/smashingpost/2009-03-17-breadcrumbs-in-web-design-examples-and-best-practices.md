---
title: 'Breadcrumbs In Web Design: Examples And Best Practices'
slug: breadcrumbs-in-web-design-examples-and-best-practices
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a871b3cd-b596-4cc6-9d6b-f2622912e2e7/breadcrumbs.jpg
date: 2009-03-17T19:22:19.000Z
author: jacob-gube
summary: >-
  On websites that have a lot of pages, breadcrumb navigation can greatly enhance the way users find their way around. In terms of usability, breadcrumbs reduce the number of actions a website visitor needs to take in order to get to a higher-level page, and they improve the <a href="https://en.wikipedia.org/wiki/Findability">findability</a> of website sections and pages.
description: >-
  On websites that have a lot of pages, breadcrumb navigation can greatly enhance the way users find their way around. In terms of usability, breadcrumbs reduce the number of actions a website visitor needs to take.
categories:
  - Inspiration
  - Showcases
  - Web Design
  - Navigation
---
A "breadcrumb" (or "breadcrumb trail") is a type of <strong>secondary navigation scheme</strong> that reveals the user's location in a website or Web application. The term comes from the <a href="https://en.wikipedia.org/wiki/Hansel_and_Gretel">Hansel and Gretel</a> fairy tale in which the two title children drop breadcrumbs to form a trail back to their home. Just like in the tale, breadcrumbs in real-world applications offer users a way to trace the path back to their original landing point.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e78e0a9a-1363-4b20-a762-8ed07ea989dd/interactive-delicious.jpg" alt="Breadcrumbs" width="243" height="99" /><figcaption>Breadcrumbs on Delicious.com</figcaption></figure>

You can usually find breadcrumbs in websites that have a large amount of content organized in a hierarchical manner. You also see them in Web applications that have more than one step, where they function similar to a progress bar. In their simplest form, breadcrumbs are horizontally arranged text links separated by the "greater than" symbol (&gt;); the symbol indicates the level of that page relative to the page links beside it.

In this article, we'll explore the use of breadcrumbs on websites and discuss some best practices for applying breadcrumb trails to your own website.

 We’ve also published a <a href="https://www.smashingmagazine.com/2022/04/breadcrumbs-ux-design/">recent article on designing better breadcrumbs UX</a>, with examples and guidelines.
 
 <p style="background-color:#e8f5ff;border:1px solid #dbeaff;border-radius:11px;padding:1.35rem 1.65rem">This article is part of our ongoing series on <a href="/category/design-patterns">design patterns</a>. It’s also a part of the upcoming <a style="font-weight:bold" href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-ux/">4-weeks live UX training</a>&nbsp;🍣 and will be in our recently released <a href="https://smart-interface-design-patterns.com/">video course</a> soon.</p>
 
## When Should You Use Breadcrumbs?

<strong>Use breadcrumb navigation</strong> for large websites and websites that have hierarchically arranged pages. An excellent scenario is e-commerce websites, in which a large variety of products is grouped into logical categories.

You <strong>shouldn't</strong> use breadcrumbs for single-level websites that have no logical hierarchy or grouping. A great way to determine if a website would benefit from breadcrumb navigation is to construct a site map or a diagram representing the website's navigation architecture, and then analyze whether breadcrumbs would improve the user's ability to navigate within and between categories.

Breadcrumb navigation should be regarded as an extra feature and shouldn't replace effective primary navigation menus. It's a convenience feature; a <strong>secondary navigation scheme</strong> that allows users to establish where they are; and an alternative way to navigate around your website.

{{% feature-panel id="vitaly-friedman" %}}

## There Are 3 Types Of Breadcrumbs

<strong>1. Location-based
</strong>Location-based breadcrumbs show the user where they are in the website's hierarchy. They are typically used for navigation schemes that have multiple levels (usually more than two levels). In the example below (from SitePoint), each text link is for a page that is one level higher than the one on its right.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/566bfbf4-cf2b-4b00-bd59-8577975a45ba/location-based-breadcrumb-example-sitepoint.jpg" alt="Breadcrumbs location-based" width="500" height="179" /></figure>

<strong>2. Attribute-based
</strong>Attribute-based breadcrumb trails display the attributes of a particular page. For example, in Newegg, breadcrumb trails show the attributes of the items displayed on a particular page:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8de010ce-eb9f-45ba-877d-4b5351d28797/newegg-attribute-based-navigation.jpg" alt="Example of attribute-based breadcrumbs." width="500" height="109" /></figure>

This page displays all computer cases that have the attributes of being manufactured by <em>Lian Li</em> and having a <em>MicroATX Mini Tower</em> form factor.

<strong>3. Path-based</strong>
Path-based breadcrumb trails show users the steps they've taken to arrive at a particular page. Path-based breadcrumbs are dynamic in that they display the pages the user has visited before arriving on the current page.

## Benefits Of Using Breadcrumbs

Here are just some of the benefits of using a breadcrumb trail.

<strong>Convenient for users</strong>
Breadcrumbs are used primarily to give users a secondary means of navigating a website. By offering a breadcrumb trail for all pages on a large multi-level website, users can navigate to higher-level categories more easily.

<strong>Reduces clicks or actions to return to higher-level pages</strong>
Instead of using the browser's "Back" button or the website's primary navigation to return to a higher-level page, users can now use the breadcrumbs with a fewer number of clicks.

<strong>Doesn't usually hog screen space</strong>
Because they're typically horizontally oriented and plainly styled, breadcrumb trails don't take up a lot of space on the page. The benefit is that they have little to no negative impact in terms of content overload, and they outweigh any negatives if used properly.

<strong>Reduces bounce rates</strong>
Breadcrumb trails can be a great way to entice first-time visitors to peruse a website after having viewed the landing page. For example, say a user arrives on a page through a Google search, seeing a breadcrumb trail may tempt that user to click to higher-level pages to view related topics of interests. This, in turn, reduces the overall website bounce rate.

## Mistakes In Breadcrumb Trail Implementation

Using breadcrumb trails is a fairly straightforward affair, and there are only a few guidelines to consider before deciding to implement them on a website. Let's take a look at some common mistakes to avoid.

<strong>Using breadcrumbs when you don't need to</strong>
A common mistake in implementing breadcrumbs is using them when there is no benefit.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9542c777-e988-4715-aa66-9088726ea3a5/simple-pie-mistake.jpg" alt="Using breadcrumbs when you do not need it." width="500" height="200" /></figure>

In the above example, Slicethepie risks overwhelming users with too many navigation options. The (1) primary navigation, (2) breadcrumb trail and (3) secondary navigation are very close together. The breadcrumb trail in this application offers users no added convenience because the secondary navigation for lower-level pages sits right below it. Additionally, clicking on the second-level link in the breadcrumb trail ("Music") takes you back to the first tab ("Listen"), which mistakenly suggests that the first tab is on a higher level than the other two ("Search" and "Artist hall of fame").

<strong>Using breadcrumb trails as primary navigation</strong>
As stated earlier, use breadcrumbs as an optional aid to navigation.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e00ca905-311f-4b7f-b96b-f74c2eee400f/mefeedia.jpg" alt="Using breadcrumbs as primary navigation" width="496" height="128" /></figure>

In the above example, mefeedia does not offer a primary navigation menu for viewing videos. Though there is text link navigation in the footer section, there's no navigation menu in the body of the pages, making it hard to navigate to other sections of the website.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b239473-6481-4404-b16b-e548229fc5fd/mefeedia-2-primary-nav.jpg" alt="Using breadcrumbs trails as primary navigation - example 2." width="500" height="381" /></figure>

If you arrive on a video page directly – say, for example, through a Google search result – the only navigation option you may have is the breadcrumb trail. Or if you've already been browsing a website's pages and reach a page that does not display the primary navigation menu, you will have to hit the "Back" button in your browser to access the main menu.

<strong>Using breadcrumbs when pages have multiple categories</strong>
Breadcrumb trails have a linear structure, so using them will be difficult if your pages can't be classified into neat categories. Deciding whether to use breadcrumbs largely depends on how you've designed your website hierarchy. When a lower-level page is (or can be put) in more than one parent category, breadcrumb trails are ineffective, inaccurate and confusing to the user.

## Breadcrumb Navigation Design Considerations

When designing a breadcrumb navigation scheme, keep several things in mind. Let's take a look at some questions that might arise when you're working with breadcrumbs.

<strong>What should be used to separate link items?</strong>
The commonly accepted and most recognizable symbol for separating hyperlinks in breadcrumb trails is the "greater than" symbol (&gt;). Typically, the &gt; sign is used to denote hierarchy, as in the format of <em>Parent category &gt; Child category</em>.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96b0be6e-7a9f-4110-81b4-b5482bfdb646/greater-than-symbol-google.jpg" alt="Example of greater than symbols separating the text links." width="433" height="136" /></figure>

Other symbols used are arrows pointing to the right, right angle quotation marks (») and slashes (/).

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/067bf939-0948-45c3-83e7-ea64df16f3d8/forward-slashes-uxmatters.jpg" alt="Example of alternative hierarchy separators." width="438" height="100" /></figure>

The choice depends on the aesthetics of the website and the type of breadcrumb used. For example, for path-based breadcrumbs in which the links do not necessarily have a hierarchical relationship to each other, using a "greater than" symbol may not convey their relationship accurately.

<strong>How big should it be?</strong>
You don't want your breadcrumbs to dominate the page. A breadcrumb trail functions merely as an aid to users (a convenience); its size should convey this to users and thus should at least be smaller, or less prominent, than the primary navigation menu.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b0b28276-3dbc-4f0d-8507-78f4e01be31d/size-of-breadcrumb-campaign-monitor.jpg" alt="An example of a good-sized breadcrumb trail." width="499" height="318" /></figure>

A good rule of thumb to follow when sizing your breadcrumb trail is that it <strong>shouldn't</strong> be the first item that grabs the user's attention when arriving on a page.

<strong>Where should breadcrumbs be located?</strong>
Breadcrumb trails are usually displayed in the top half of the page, below the primary navigation menu if a horizontal menu layout is used.

## Breadcrumb Showcase

Now that we've discussed the who, what, when, where, why and hows of breadcrumb trails, we should take a look at some live examples. In the following section, you'll find a few examples of great websites that use breadcrumb trails.

## 1. Classic Text-Based Breadcrumbs

TypePad Design Assistant

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f429dfcf-17b3-4efb-9d69-3eaf2751e75f/typical-breadcrumb-typepad.jpg" alt="classic breadcrumb - example 1." width="495" height="78" /></figure>

NASA

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7017d1e7-16a3-4913-91a9-b5635cc107b3/greater-than-symbol-nasa.jpg" alt="Classic text-based breadcrumbs" width="280" height="132" /></figure>

Nestle uses a breadcrumb trail whose text is significantly smaller than the text on the rest of the page, effectively making it unobtrusive.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff50d5c7-1264-4efb-be3e-92090e8f4087/greater-than-symbol-nestle.jpg" alt="Nestle example." width="500" height="474" /></figure>

Marchand de Trucs

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b08b99e-b954-41f4-98bf-920852a8ecbd/typical-breadcrumb-marchand.jpg" alt="classic breadcrumb - example 2." width="500" height="150" /></figure>

Bridge 55

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f12514d-22ce-4b51-ae29-d48896457ce6/typical-breadcrumb-bridge-55.jpg" alt="classic breadcrumb - example 3." width="500" height="150" /></figure>

Overstock uses the standard "greater than" symbol for its attribute-based breadcrumb trail. Checkboxes for product attributes are used so that users can uncheck them to filter them out.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62d674bd-d7b4-4aef-8abb-bebd7f152976/typical-breadcrumb-overstock.jpg" alt="classic breadcrumb - example 4." width="505" height="167" /></figure>

## 2. Replacing `>` With Other Symbols

TechRadar UK and BP&lt; use right-pointing triangles.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64bbcb0c-5351-4711-b05b-61b71d438380/replacing-techradar.jpg" alt="Using other symbols for hierachy separators - example 2." width="495" height="78" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5f5419d-ee2f-47be-9a8b-ec3ba0b52bcb/replacing-bp.jpg" alt="Replacing the greater than symbol example." width="413" height="136" /></figure>

PSDTUTS and Martique use slashes.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a9a78bc-a1f0-4194-98e0-4da55e315d71/replacing-psdtuts.jpg" alt="Using other symbols for hierachy separators - example 3." width="500" height="111" /></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05b790ee-04ab-4db9-8a4c-01d4d2153ad5/replacing-martique.jpg" alt="Using other symbols for hierachy separators - example 4." width="500" height="106" /></figure>

Mouse to Minx uses a right-angled quotation mark to denote page hierarchy.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/114dd01f-03ae-4d47-b8fe-22021d3c1a5f/replacing-mouse-to-minx.jpg" alt="Using other symbols for hierachy separators - example 5." width="500" height="106" /></figure>

Jakob Nielsen's Alertbox uses right-pointing arrows.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/406e454d-78d8-430d-8cdd-512ca7d2b0bb/replacing-usitdotcome.jpg" alt="Using other symbols for hierachy separators - example 1." width="495" height="78" /></figure>

Target uses colons (:) for separators.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/034b4a24-2cf2-4dbd-a992-8d388ad01c99/replacing-target.jpg" alt="semicolon separator example." width="413" height="88" /></figure>

## 3. Beyond Simple Text Links

One current trend in breadcrumb design basically says, "Breadcrumbs don't have to be simple". In these designs, you'll see beautifully styled breadcrumbs that integrate well with the overall design.

Grooveshark

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6489844-4a71-4a02-b225-09f1fff1054a/beautifully-groove-shark.jpg" alt="styled breadcrumbs - example 1." width="459" height="81" /></figure>

Yahoo! TV

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1df38667-a7c5-4f35-8c67-d0a46a7e8788/beautifully-yahootv.jpg" alt="Beautiful breadcrumb trails." width="378" height="98" /></figure>

IDEO

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88c82839-ba0a-4637-9df4-7b7cdd53af5d/beautifully-ideo.jpg" alt="styled breadcrumbs - example 2." width="505" height="167" /></figure>

Apple Store

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f27d4cc2-80cb-4dc6-b1da-d467141dde9f/beautifully-apple.jpg" alt="styled breadcrumbs - example 3." width="505" height="167" /></figure>

Coolspotters

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26325270-7cca-442f-9487-871d81cd741f/beautifully-coolspotters.jpg" alt="styled breadcrumbs - example 4." width="505" height="167" /></figure>

Devlounge

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ab24ee-dbf9-49e1-b72b-82eec7272f37/beautifully-devlounge.jpg" alt="styled breadcrumbs - example 5." width="495" height="127" /></figure>

LottaNZB

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be4407c5-fe60-4e73-8ec1-ba1498b4963e/beautifully-launchpad.jpg" alt="" width="330" height="74" /></figure>

Pixelpoodle

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98555871-4d9a-4299-87ce-bf11fdb0db69/beautifully-pixeldoodle.jpg" alt="Beautifully-styled breadcrumbs - example." width="425" height="65" /></figure>

guardian.co.uk

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4f9114b-b65b-465a-b236-0294847e00fb/beautifully-guardianuk.jpg" alt="Beautiful navigation - examples." width="500" height="150" /></figure>

## 4. Breadcrumbs For Multi-Step Processes

Statement Tracker uses a breadcrumb trail to indicate the steps involved in registering for an account, as well as a progress indicator.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c410508-4514-4729-8734-8cca3e0ea0b8/sequential-statementtracker.jpg" alt="Sequential process example." width="500" height="204" /></figure>

Flickr uses a breadcrumb trail to indicate the number of sections in the Flickr tour.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/267a175b-1e7c-41cb-b51d-5e98829f2e7b/sequential-flickr.jpg" alt="breadcrumb" width="372" height="84" /></figure>

## 5. Breadcrumbs With Sub-Navigation

Here are some examples of breadcrumb trails whose links, when clicked on or hovered over, open a sub-navigation panel that lists additional attributes or locations.

MarketWatch has a fly-out sub-navigation menu that appears when you hover over a breadcrumb link.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe1dd7de-b18c-4601-9cc6-2823eb2f9cb9/subnav-marketwatch.jpg" alt="breadcrumb with sub-navigation example." width="413" height="166" /></figure>

Profoto has a unique breadcrumb trail: clicking on a breadcrumb link opens an area below it that gives users additional attributes to select from.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c1dcdba-0436-4501-9fc8-c7bffff4b490/primary-nav-protofoto.jpg" alt="Experimental Example 2." width="500" height="152" /></figure>

Cranfield University has a similar fly-out breadcrumb scheme, which serves a dual function: as an location indicator for the user and as a robust and interactive secondary navigation scheme.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f8cc58d-4e2d-404f-8e0c-a51e5d667445/primary-nav-cranfield.jpg" alt="Flyout Breadcrumbs" width="366" height="291" /></figure>

Lonely Planet also has a fly-out breadcrumb trail in which you can change attributes.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2abfbb8-3e3f-4a18-9bff-c15d76615184/primary-nav-lonely-planet.jpg" alt="flyout menu - example 3." width="471" height="74" /></figure>

Clicking on a breadcrumb link takes you to that item's page, while clicking on the downward-pointing arrow opens additional options.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cee88b9a-06d5-417b-9de7-bdc63ec532f4/primary-nav-lonely-planet-2.jpg" alt="Flyout menu - example 4." width="500" height="302" /></figure>

MSDN has a breadcrumb trail that opens a scrollable sub-navigation list when the user hovers over a link.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de796e7f-97e4-4830-a301-16dabc23c9c3/subnav-msdn.jpg" alt="subnavigation example 1." width="428" height="250" /></figure>

Wowhead has a multi-level sub-navigation scheme.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36c4b74c-7753-4b86-a076-bdb7fe9305df/subnav-wowhead.jpg" alt="" width="399" height="154" /></figure>

## 6. Interactive Breadcrumbs

Delicious lets you remove items in the breadcrumb trail of keyword tags to help you quickly find bookmarks.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e78e0a9a-1363-4b20-a762-8ed07ea989dd/interactive-delicious.jpg" alt="interactive example 1." width="243" height="99" /></figure>

## 7. Experimental Examples

Booreiland uses a breadcrumb-style navigation scheme for its primary menu, allowing visitors to quickly understand what they're currently viewing.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/324b70c9-eaef-4caf-886e-b37e8ca6da0d/primary-nav-booreiland.jpg" alt="Experimental example 1." width="500" height="215" /></figure>

### <span class="rh">Further Reading</span> on SmashingMag: [Link](#further-reading-on-smashingmag)

*   [Planning And Implementing Website Navigation](https://www.smashingmagazine.com/2011/06/planning-and-implementing-website-navigation/)
*   [Web Design Elements: Examples And Best Practices](https://www.smashingmagazine.com/web-design-essentials-examples-and-best-practices/ "Web Design Elements: Examples And Best Practices")
*   [Smashing Book 5 — Real-Life RWD (Book)](https://shop.smashingmagazine.com/products/smashing-book-5-real-life-responsive-web-design "Smashing Book 5 — Real-Life RWD (Book)")
*   [Mobile Navigation For Smashing Magazine: A Case Study](https://www.smashingmagazine.com/2015/09/mobile-navigation-for-smashing-magazine/ "Mobile Navigation For Smashing Magazine: A Case Study")

{{< signature "al, il" >}}

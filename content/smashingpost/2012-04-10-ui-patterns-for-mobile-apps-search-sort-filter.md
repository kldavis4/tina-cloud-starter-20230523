---
title: 'UI Patterns For Mobile Apps: Search, Sort And Filter'
slug: ui-patterns-for-mobile-apps-search-sort-filter
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cd3a17a9-5e06-4988-9006-b53534c4c18b/illusearch4.jpg
date: 2012-04-10T12:25:48.000Z
author: theresa-neil
description: >-
  As I was waiting for a table at a local restaurant the other day, I flipped
  through a couple of the free classified papers. I was shocked to realize how
  dependent I’ve grown on three simple features that just aren’t available in
  the analog world: **search, sort and filter**.
categories:
  - UX
  - Usability
  - Design Patterns
---
As I was waiting for a table at a local restaurant the other day, I flipped through a couple of the free classified papers. I was shocked to realize how dependent I’ve grown on three simple features that just aren’t available in the analog world: <strong>search, sort and filter</strong>.

AutoDirect and some of the other freebies are organized by category (like trucks, vans, SUVs) but others, like Greensheet, just list page after page of items for sale. I would actually have to read every single ad in the paper to find what I wanted. No thank you, I’ll use Craigslist on my phone instead.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Boost Your Mobile E-Commerce Sales With Design Patterns](https://www.smashingmagazine.com/2012/12/boost-your-mobile-e-commerce-sales-with-mobile-design-patterns/)
*   [The Current State Of E-Commerce Filtering](https://www.smashingmagazine.com/2015/04/the-current-state-of-e-commerce-filtering/)
*   [Smart Responsive Design Patterns](https://www.smashingmagazine.com/2016/05/smart-responsive-design-patterns-or-when-off-canvas-isnt-good-enough/)
*   [Thinking Like An App Designer](https://www.smashingmagazine.com/2015/04/thinking-like-an-app-designer/)

But after taking a look at Craigslist mobile, it became obvious we could all benefit from some best practices around mobile search, sort and filter UI design. This article explores a dozen different ways to surface and refine the data your customers want.

{{% feature-panel %}}

## Search Patterns

Before you ever try to design a search interface for any platform, buy and read these two books: <a title="Search Patterns" href="https://amzn.com/0596802277">Search Patterns: Design for Discovery</a> by Peter Morville and Jeffery Callender, and <a title="Designing Search" href="https://amzn.com/0470942231">Designing Search: UX Strategies for eCommerce Success</a> by Greg Nudelman.

Then take a look at these search patterns specific to mobile applications:

*   Explicit Search
*   Auto-Complete
*   Dynamic Search
*   Scoped Search
*   Saved & Recent
*   Search Form
*   Search Results

### Explicit Search

Explicit search relies on an explicit action to perform the search and view results. That action might be to tap a search button on the screen, like Walmart, or on the keyboard, like Target. The results are typically displayed in the area below the search bar. Consider pairing an explicit search pattern with the auto-complete pattern.</p>

<figure><a href="https://www.walmart.com/cp/Walmart-Mobile-App/1087865"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111366" title="4.2_Walmart_and_Target" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0a3504a-9e5b-4233-93fd-7c158e9ea0ce/4.2_Walmart_and_Target1" alt="" width="500" /></a><figcaption><a title="Walmart" href="https://www.walmart.com/cp/Walmart-Mobile-App/1087865">Walmart</a> uses a search button (Go) on the screen, Target uses the Search on the keyboard.</figcaption></figure>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111367" title="4.3_Target" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/daf4d1ab-ad51-4973-97bd-cbb13f67204d/4.3_Target1" alt="" width="500" /><figcaption>Target loading and then displaying search results.</figcaption></figure>

<blockquote>Offer a clear button in the field and an option to cancel the search. Use feedback to show the search is being performed.</blockquote>

### Auto-Complete

Probably the most useful search pattern that emerged in Web 2.0 is auto-complete. Typing will immediately surface a set of possible results, just tap on one to selected it and the search will be performed. Or continue typing your own criteria and then tap the explicit search button.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111368" title="4.4_Marketplace_and_Netflix" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/579d04ff-ce82-4f28-8074-58428ced0fa8/4.4_Marketplace_and_Netflix1" alt="" width="500" /><figcaption><a title="Android Marketplace" href="https://play.google.com/store/apps">Android Marketplace</a> (Google Play) and <a title="Netflix" href="https://blog.netflix.com/2010/08/netflix-now-available-on-your-iphone.html">Netflix</a> both use auto-complete</figcaption></figure>

Ideally the results will be displayed immediately, but a progress indicator (searching...) should be used for system feedback. Netflix (above) uses an indicator in the search field, whereas Fidelity (below) displays one where the results will eventually be displayed.

<figure><a href="https://personal.fidelity.com/products/trading/mobile/android.shtml"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111369" title="4.5_Fidelity" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4eb25121-8846-4ea8-ad3f-41fc9ca21b40/4.5_Fidelity1" alt="" width="500" /></a><figcaption><a title="Fidelity" href="https://personal.fidelity.com/products/trading/mobile/android.shtml">Fidelity</a> shows feedback while loading the auto-complete options.</figcaption></figure>

TripAdvisor provides an enhanced auto-complete, grouping the results by popular destinations, hotels, restaurants. LinkedIn does something similar by showing direct connections first, then other people in LinkedIn.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111370" title="4.6_TripAdvisor_LinkedIn" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3f91c8a-d3da-4587-8f2d-d1de326f8bf4/4.6_TripAdvisor_LinkedIn1" alt="" width="500" /><figcaption><a title="TripAdvisor" href="https://itunes.apple.com/us/app/tripadvisor-hotels-flights/id284876795?mt=8">TripAdvisor</a> and <a title="LinkedIn" href="https://play.google.com/store/apps/details?id=com.linkedin.android">LinkedIn</a> group the suggested options.</figcaption></figure>

<blockquote>Provide feedback if there could be a delay in displaying the results. Consider emphasizing the matching search text in the search results.</blockquote>

### Dynamic Search

This pattern may also be called dynamic filtering. Entering text in the search field will dynamically (onkeypress) filter the data on the screen. Note, the examples may look similar to auto-complete but there is a different interation model. The dynamic search pattern is used to refine or whittle down a existing and visible list of objects. In these examples from BlackBerry App World and WorldMate on Android, apps and hotels, respectively, were already displayed on the page.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111377" title="4.12_WorldMate_airbnb" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e56d841e-47e0-451e-840f-f96bf1473bf3/4.7_BlackBerry_and_WorldMate" alt="" width="500" /><figcaption><a title="BlackBerry App World" href="https://appworld.blackberry.com/webstore/?">BlackBerry App World</a> and <a title="WorldMate" href="https://www.worldmate.com/android/">WorldMate</a> offer dynamic search for refining a big list of results.</figcaption></figure>

<blockquote>Works well for refining constrained data sets, like an address book or personal media library, but may be impractical for searching large data sets from multiple sources.</blockquote>

### Scoped Search

Sometimes it is easier (and faster) to get to the desired result by scoping the search criteria before performing the search. Google and Photobucket use different designs to the same end.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111372" title="4.8_Google_and_Photobucket" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/321a9697-bf59-4cf3-84f2-9f95836a1bcb/4.8_Google_and_Photobucket1" alt="" width="500" /><figcaption><a title="Google" href="https://www.google.com/mobile/android/">Google</a> uses an overlay to present scope options, whereas Photobucket uses a dialog.</figcaption></figure>

AllRecipes also lets you select criteria (or filters) before submitting the search. Dropbox defaults the initial scope to All, but you can switch it to Files or Folders before or after tapping the search button.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111373" title="4.9_AllRecipes_and_DropBox" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4490f4ef-a01d-428b-abc3-c92ef397db4f/4.9_AllRecipes_and_DropBox1" alt="" width="500" /><figcaption>AllRecipes pushes the limit of scoping options, <a title="Dropbox" href="https://www.dropbox.com/iphoneapp">Dropbox</a> keeps it simple with just 3.</figcaption></figure>

<blockquote>Offer reasonable scoping options based on the data set. Three to six scoping options are plenty, consider a search form for advanced searching capabilities.</blockquote>

### Saved & Recent

Successful mobile interfaces follow a basic usability maxim: respect the users effort. Saved and recent searches do this by making it easy to select from previous searches, instead of retyping the same keywords or search criteria.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111374" title="4.10_eBay_and_Walmart" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1a60ac7-dfd3-46e8-b607-3dacc2169c15/4.10_eBay_and_Walmart1" alt="" width="500" /><figcaption><a title="eBay" href="https://mobile.ebay.com/iphone/ebay">eBay</a> lets customers explicity save searches. Both eBay and Walmart implicity save customers' most recent searches.</figcaption></figure>

Other options to respect the users’ effort involve location based searching options like Trulia, and bar code searching, like PriceCheck by Amazon.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111375" title="4.11_Trulia_and_Amazon-PriceCheck" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4882de0-e51f-47a6-b128-59335c08f136/4.11_Trulia_and_Amazon-PriceCheck1" alt="" width="500" /><figcaption>Trulia offers location based searching, <a title="Amazon" href="https://www.amazon.com/gp/feature.html?docId=aw_ppricecheck_iphone_mobile">Amazon</a> offers 4 ways to search.</figcaption></figure>

<figure><a href="https://www.google.com/mobile/shopper/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111376" title="4.11b_Google_Shopper" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/494c7cf5-986b-459b-844d-ebe30ae22647/4.11b_Google_Shopper1" alt="" width="500" /></a><figcaption><a title="Google Shopper" href="https://www.google.com/mobile/shopper/">Google Shopper</a> offers scan and speak search options and a full search history grouped by search date.</figcaption></figure>

<blockquote>Saved searches typically require additional steps to name a search for later use, whereas recent searches are implicitly saved and surfaced. Consider which one will best serve your customers’ needs.</blockquote>

### Search Form

This pattern is characterized by a separate form for entering search criteria, and an explicit search button.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111377" title="4.12_WorldMate_airbnb" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8360f0ad-cf60-404d-9112-19458e19bbc6/4.12_WorldMate_airbnb" alt="" width="500" /><figcaption>Search forms on <a title="WorldMate" href="https://www.worldmate.com/android/">WorldMate</a> and <a title="airbnb" href="https://www.airbnb.com/mobile">airbnb</a>.</figcaption></figure>

<figure><a href="https://www.wholefoodsmarket.com/apps/index.php"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111378" title="4.13_WholeFoods-Recipe-Search" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/020a03c7-5e74-4309-9aea-622e7edad7b3/4.13_WholeFoods-Recipe-Search1" alt="" width="500" /></a><figcaption><a title="WholeFoods" href="https://www.wholefoodsmarket.com/apps/index.php">WholeFood's</a> recipe search allows customers to add multiple criteria, course, category, special diets and keywords.</figcaption></figure>

<blockquote>Minimize the number of input fields. Implement OS specific input controls properly. Follow form design best practices (alignment, labels, size).</blockquote>

### Search Results

Once a search is performed the results can be displayed in the same screen or on a dedicate results screen. Results may be displayed in a table or list, on a map or satellite, or as thumbnail images. Multiple view options can be used depending on the type of results and user preferences.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111379" title="4.14_Kayak_and_Foursquare" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6beea9c5-c1ee-42d2-9610-a4773a7033a9/4.14_Kayak_and_Foursquare1" alt="" width="500" /><figcaption><a title="Kayak" href="https://www.kayak.com/iphone">Kayak</a> and <a title="FourSquare" href="https://foursquare.com/apps/">Foursquare</a> (webOS) show the results in a table.</figcaption></figure>

<figure><a href="https://www.airbnb.com/mobile"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111380" title="4.14b_airbnb" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73f5f5cc-eb12-4e35-b936-869c518b4a70/4.14b_airbnb1" alt="" width="500" /></a><figcaption><a title="airbnb" href="https://www.airbnb.com/mobile">airbnb</a> shows the results in a list and offers a map view toggle.</figcaption></figure>

<figure><a href="https://www.zappos.com/android-app"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111381" title="4.15_Zappos" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b783689a-a987-458d-87c5-be9fec28abcf/4.15_Zappos1" alt="" width="500" /></a><figcaption><a title="Zappos" href="https://www.zappos.com/android-app">Zappos</a> offers a list view and alternate carousel view for browsing search results.</figcaption></figure>

Lazy loading is a common technique to use so that some results will be displayed while the rest are being loaded. Many applications offer either a button to explicitly “view more results” or will automatically load more results when the screen is flicked.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111382" title="4.16_eBay-Motors_and_Best-Buy" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bcf83f3-45ab-431c-9e30-18f6b64e3889/4.16_eBay-Motors_and_Best-Buy1" alt="" width="500" /><figcaption><a title="eBay Motors" href="https://mobile.ebay.com/iphone/motors">eBay Motors</a> and <a title="Best Buy" href="https://play.google.com/store/apps/details?id=com.bestbuy.android&amp;hl=en">Best Buy</a>.</figcaption></figure>

<blockquote>Label the results with the number returned. Use lazy loading instead of paging. Apply a reasonable default sort order. Avoid paging tables, they break the natural interaction model for viewing information on a mobile device.</blockquote>

## Sort

It is important to choose a reasonable default sort for displaying search results. A little common sense plus user validation is the best way to choose the default sort order. These patterns offer options for changing the default sort:

*   Onscreen Sort
*   Sort Selector
*   Sort Form

### Onscreen Sort

When there are only a few sort options, an onscreen sort can provide a simple one tap solution. Placing the sort toggle at the top or bottom of the screen will depend on the other screen elements.

Target provides four sort options with a three toggle button. For the price sort option, they offer two choices: sort by price ascending and sort by price descending.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111383" title="4.18_Expedia_and_Target" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bdbdb740-0cbb-4544-99f1-39f7d899c8ca/4.18_Expedia_and_Target1" alt="" width="500" /><figcaption><a title="Expedia" href="https://www.expedia.com/">Expedia</a> (older version) and Target iOS use onscreen sort.</figcaption></figure>

<blockquote>Clearly show which option is selected or “on”. Consider the Sort Order Selector pattern if the option labels don’t fit nicely in a toggle button bar.</blockquote>

### Sort Order Selector

The selector pattern is a good alternative to the onscreen sort. There are a number of different UI controls that can be used for selection, but consider the design guidelines for the OS you are designing for (ex. the menu is common for Android app, and the picker and actionsheet are common in iOS apps).</p>

<figure><a href="https://play.google.com/store/apps/details?id=com.walmart.android&amp;hl=en"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111384" title="4.19_Walmart" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f93e28af-6d1b-4f31-9aaf-ffbc3eae0df6/4.19_Walmart1" alt="" width="500" /></a><figcaption><a title="Walmart" href="https://play.google.com/store/apps/details?id=com.walmart.android&amp;hl=en">Walmart</a> on Android uses the common menu control.</figcaption></figure>

The option titles can be longer (more explicit) and more options can be displayed. Walmart places the sort button in proximity with the search field, wheras Kayak offers sort and filter options at the bottom of the screen.</p>

<figure><a href="https://www.kayak.com/iphone"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111385" title="4.20_Kayak" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e5b069d-f5be-400f-8ddd-b97b246a70ce/4.20_Kayak1" alt="" width="500" /></a><figcaption><a title="Kayak" href="https://www.kayak.com/iphone">Kayak</a> on iOS uses the standard selector control.</figcaption></figure>

OS neutral solutions include a simple combobox, like Target on Android, or an overlay menu, like Awesome Note.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111386" title="4.21_Target_and_AwesomeNote" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9dd446d-44ae-4a27-a48f-f9f859e590ac/4.21_Target_and_AwesomeNote1" alt="" width="500" /><figcaption>Target on Android just uses a combobox. <a title="Awesome Note" href="https://www.bridworks.com/anote/en/main/index.php">AwesomeNote</a> uses an overlay.</figcaption></figure>

<blockquote>Follow OS design conventions for choosing the selector control, or choose an OS neutral implementation. Clearly show which sort option is applied.</blockquote>

### Sort Form

Some applications have consolidated the sort and filter options into one screen, typically titled “Refine”. This is the most effort intensive sort pattern requiring the user to open the form, select an option, and then apply the selection (by tapping “done” or “apply”).</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111387" title="4.22_Cars_and_eBay" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4396b362-9d3a-4d50-8d6e-dd2054cb1f21/4.22_Cars_and_eBay1" alt="" width="500" /><figcaption><a title="Cars.com" href="https://itunes.apple.com/us/app/cars-com/id353263352?mt=8">Cars.com</a> and <a title="eBay Classifieds" href="https://mobile.ebay.com/android/classifieds">eBay Classifieds</a>.</figcaption></figure>

<blockquote>Consider the more efficient sort option toggle or sort order selector patterns before choosing this design.</blockquote>

## Filter

Large sets of data can require additional filtering, also called refining. Filtering relies on the user selecting criteria by which to refine the set of search results or a large set of objects. Common filtering patterns include:

*   Onscreen Filter
*   Filter Drawer
*   Filter Dialog
*   Filter Form

Also see the earlier search pattern, Scoped Search, for an optional pre-filtering technique.</p>

### Onscreen filter

Similar to the onscreen sort, the onscreen filter is displayed with the results or list of objects. With one tap, the filter is applied. HeyZap uses the standard toggle button bar, whereas Google uses vertical tabs.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111388" title="4.24_HeyZap_and_Google" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45c3ebbc-e746-4f9a-bcf3-3bf94b546ce2/4.24_HeyZap_and_Google1" alt="" width="500" /><figcaption>HeyZap and <a title="Google" href="https://www.google.com/mobile/android/">Google</a>.</figcaption></figure>

CBS News and the ACL Festival app uses a scrolling filter bar as a way to let users quickly hone in on certain types of articles and bands, respectively.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111389" title="4.25_CBS-News_and_Austin-City-Limits-Music-Festival" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78c45af1-27e1-437b-8f12-9e646541c872/4.25_CBS-News_and_Austin-City-Limits-Music-Festival1" alt="" width="500" /><figcaption><a title="CBS News" href="https://play.google.com/store/apps/details?id=com.treemolabs.apps.cbsnews&amp;hl=en">CBS News</a> (single filter bar) and Austin City Limits Music Festival (double filter bar).</figcaption></figure>

Don’t use this filter pattern for primary navigation within your app, but instead use it to group and filter related content.

SXSW offers a filter button bar combined with a second row of filtering options. Feed a Fever news reader uses a super simple stylized set of comboboxes for filtering news feeds.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111390" title="4.26_SXSW_and_Feed-a-Fever" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a14a97fd-9ea9-426e-9af0-69a8cd1f26e6/4.26_SXSW_and_Feed-a-Fever1" alt="" width="500" /><figcaption><a title="SXSW" href="https://itunes.apple.com/us/app/sxsw-go/id418450665?mt=8">SXSW Conference</a> app and <a title="Feed a Fever" href="https://feedafever.com/">Feed a Fever</a>.</figcaption></figure>

<blockquote>Filter options should be clearly worded and easy to understand. Show the filters that are applied or “on”.</blockquote>

### Filter Drawer

Almost as efficient as the onscreen filter, a drawer can be used to reveal filter options. Flicking or tapping a handle will open the drawer. Audible’s drawer reveals a simple filter toggle bar, whereas Sam’s offers a host of filter options that can be applied to the map of club locations. A better design for Sam’s would be to leave the map visible and allow for dynamic filtering instead of the explicit “filter” button.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111391" title="4.27_Audible_and_Sam’s-Club" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b822ddbb-9e4c-401a-9eb9-117af950e216/4.27_Audible_and_Sam’s-Club1" alt="" width="500" /><figcaption><a title="Audible" href="https://www.audible.com/wireless/android">Audible</a> and <a title="Sam's Club" href="https://www3.samsclub.com/mobile">Sam's Club</a>.</figcaption></figure>

<figure><a href="https://www.expedia.com/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111392" title="4.27b_expedia" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd514f88-3afc-46f6-b13f-9d24a2e187a9/4.27b_expedia1" alt="" width="500" /></a><figcaption><a title="Expedia" href="https://www.expedia.com/">Expedia's</a> new filter drawer.</figcaption></figure>

### Filter Dialog

Like a pop-up on in a web app, the filter dialog is modal in nature. It requires the user to select a filter option, or cancel the action. TripAdvisor on iOS has a custom filter dialog, whereas USPS Mobile on Android relies on the default selector control.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111393" title="4.28_TripIt_and_DueTodayLite" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/702bb0ac-1889-4121-a40e-8533500b18b2/4.28_TripIt_and_DueTodayLite1" alt="" width="500" /><figcaption><a title="TripAdvisor" href="https://itunes.apple.com/us/app/tripadvisor-hotels-flights/id284876795?mt=8">TripAdvisor</a> and <a title="Due Today" href="https://play.google.com/store/apps/details?id=com.lakeridge.DueToday&amp;hl=en">Due Today</a> Lite.</figcaption></figure>

While the Filter Dialog may get the job done, the first two patterns provide more freedom for users to experiment with and apply filters directly in context.
<blockquote>Keep the options list short, avoid scrolling. Consider a Filter Form for lengthier or multi-select filter options.</blockquote>

### Filter Form

Large data sets can benefit from more advanced filter/refinement options. For example, WorldMate uses a form to filter hotels based on price, brand and stars. Zappos uses a similar approach, using the iOS standard drill down for selection, and the clear/done buttons in the title bar.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111394" title="4.29_WorldMate_and_Zappos" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/375686b5-5479-4835-bfca-060ce71fb7ee/4.29_WorldMate_and_Zappos1" alt="" width="500" /><figcaption><a title="WorldMate" href="https://www.worldmate.com/">WorldMate's</a> filter form (looks very similar to Kayak's design) and <a title="Zappos" href="https://www.zappos.com/iphone-app">Zappos</a> filter form for iOS.</figcaption></figure>

Freetime uses custom controls in their filter form. First you pick the filter category, then choose the filter criteria, then apply the filter to the calendar.</p>

<figure><a href="https://itunes.apple.com/us/app/free-time/id429232593?mt=8"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111395" title="4.30_Freetime" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec25634d-04f8-4f6d-8b29-3dc8decdfc03/4.30_Freetime1" alt="" width="500" height="404" /></a><figcaption><a title="freetime" href="https://itunes.apple.com/us/app/free-time/id429232593?mt=8">Free-Time</a> filter form.</figcaption></figure>

Conditional filters, also called predicate editors or expression builders, are an advanced filtering feature typically found in reporting tools. Here’s the standard layout used on the web and desktop.

SXSW offers a filter button bar combined with a second row of filtering options. Feed a Fever news reader uses a super simple stylized set of comboboxes for filtering news feeds.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111390" title="4.26_SXSW_and_Feed-a-Fever" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a14a97fd-9ea9-426e-9af0-69a8cd1f26e6/4.26_SXSW_and_Feed-a-Fever1" alt="" width="500" /><figcaption><a title="SXSW" href="https://itunes.apple.com/us/app/sxsw-go/id418450665?mt=8">SXSW Conference</a> app and <a title="Feed a Fever" href="https://feedafever.com/">Feed a Fever</a>.</figcaption></figure>

<blockquote>Filter options should be clearly worded and easy to understand. Show the filters that are applied or “on”.</blockquote>

### Filter Drawer

Almost as efficient as the onscreen filter, a drawer can be used to reveal filter options. Flicking or tapping a handle will open the drawer. Audible’s drawer reveals a simple filter toggle bar, whereas Sam’s offers a host of filter options that can be applied to the map of club locations. A better design for Sam’s would be to leave the map visible and allow for dynamic filtering instead of the explicit “filter” button.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111391" title="4.27_Audible_and_Sam’s-Club" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b822ddbb-9e4c-401a-9eb9-117af950e216/4.27_Audible_and_Sam’s-Club1" alt="" width="500" /><figcaption><a title="Audible" href="https://www.audible.com/wireless/android">Audible</a> and <a title="Sam's Club" href="https://www3.samsclub.com/mobile">Sam's Club</a>.</figcaption></figure>

<figure><a href="https://www.expedia.com/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111392" title="4.27b_expedia" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd514f88-3afc-46f6-b13f-9d24a2e187a9/4.27b_expedia1" alt="" width="500" /></a><figcaption><a title="Expedia" href="https://www.expedia.com/">Expedia's</a> new filter drawer.</figcaption></figure>

### Filter Dialog

Like a pop-up on in a web app, the filter dialog is modal in nature. It requires the user to select a filter option, or cancel the action. TripAdvisor on iOS has a custom filter dialog, whereas USPS Mobile on Android relies on the default selector control.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111393" title="4.28_TripIt_and_DueTodayLite" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/702bb0ac-1889-4121-a40e-8533500b18b2/4.28_TripIt_and_DueTodayLite1" alt="" width="500" /><figcaption><a title="TripAdvisor" href="https://itunes.apple.com/us/app/tripadvisor-hotels-flights/id284876795?mt=8">TripAdvisor</a> and <a title="Due Today" href="https://play.google.com/store/apps/details?id=com.lakeridge.DueToday&amp;hl=en">Due Today</a> Lite.</figcaption></figure>

While the Filter Dialog may get the job done, the first two patterns provide more freedom for users to experiment with and apply filters directly in context.
<blockquote>Keep the options list short, avoid scrolling. Consider a Filter Form for lengthier or multi-select filter options.</blockquote>

### Filter Form

Large data sets can benefit from more advanced filter/refinement options. For example, WorldMate uses a form to filter hotels based on price, brand and stars. Zappos uses a similar approach, using the iOS standard drill down for selection, and the clear/done buttons in the title bar.</p>

<figure><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111394" title="4.29_WorldMate_and_Zappos" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/375686b5-5479-4835-bfca-060ce71fb7ee/4.29_WorldMate_and_Zappos1" alt="" width="500" /><figcaption><a title="WorldMate" href="https://www.worldmate.com/">WorldMate's</a> filter form (looks very similar to Kayak's design) and <a title="Zappos" href="https://www.zappos.com/iphone-app">Zappos</a> filter form for iOS.</figcaption></figure>

Freetime uses custom controls in their filter form. First you pick the filter category, then choose the filter criteria, then apply the filter to the calendar.</p>

<figure><a href="https://itunes.apple.com/us/app/free-time/id429232593?mt=8"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111395" title="4.30_Freetime" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec25634d-04f8-4f6d-8b29-3dc8decdfc03/4.30_Freetime1" alt="" width="500" height="404" /></a><figcaption><a title="freetime" href="https://itunes.apple.com/us/app/free-time/id429232593?mt=8">Free-Time</a> filter form.</figcaption></figure>

Conditional filters, also called predicate editors or expression builders, are an advanced filtering feature typically found in reporting tools. Here’s the standard layout used on the web and desktop.</p>

<figure><a href="https://wufoo.com/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111396" title="4.31_build_expression_wufoo" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e998f862-cc0c-47c4-917f-8493bf09ec6c/4.31_build_expression_wufoo1" alt="" width="500" /></a><figcaption>Predicate editor in the <a title="Wufoo" href="https://wufoo.com/">Wufoo</a> web application.</figcaption></figure>

Creating a conditional filtering a mobile application can be challenging in a mobile form factor but Roambi has accomplished it.</p>

<figure><a href="https://www.roambi.com/"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="111397" title="4.32_Roambi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b253f4d1-e2d1-46af-b4d4-1d5f1ed94c39/4.32_Roambi1" alt="" width="500" /></a><figcaption><a title="Roambi" href="https://www.roambi.com/">Roambi's</a> predicate editor.</figcaption></figure>

<blockquote>Don’t over-design the filters, a simple onscreen filter or drawer will usually suffice. If a filter form is necessary, follow form design best practices.</blockquote>

## More Resources

Learn more about designing usable and effective mobile apps in <a href="https://www.amazon.com/Mobile-Design-Pattern-Gallery-Applications/dp/1449314325">Mobile Design Pattern Gallery: UI Patterns for iOS, Android, and More</a>:

*   Navigation
*   Forms
*   Tables
*   Tools
*   Charts
*   Invitations
*   Feedback & Affordance
*   Help

Also check out the Mobile Design Pattern Gallery <a href="https://www.mobiledesignpatterngallery.com">website</a>, blog and <a href="https://www.flickr.com/photos/mobiledesignpatterngallery/collections/">Flickr photostream</a> with +600 screenshots.</p>

<strong>Editor's Note:</strong> please notice that this article is a chapter from Theresa Neil’s new book <a href="https://www.mobiledesignpatterngallery.com">Mobile Design Pattern Gallery: UI Patterns for iOS, Android and More</a>, which provides solutions to common design challenges.

{{< signature "fi" >}}


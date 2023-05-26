---
title: 'How To Design Search For Your Mobile App'
slug: design-search-mobile-app
author: Suzanne Scacca
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff5c5c6b-8784-4936-8567-9583df3de5f7/neil-patel-search-vs-navigation.png
date: 2019-01-08T14:00:40+01:00
summary: >-
  As you work on creating better experiences for your mobile app users, spend some time thinking about the design of your app’s search bar. Things like placement, hint text, and the way search results are displayed contribute to how users engage with search as well as your app as a whole.
description: >-
  As you work on creating better experiences for your mobile app users, spend some time thinking about the design of your app’s search bar. Things like placement, hint text, and the way search results are displayed contribute to how users engage with search as well as your app as a whole.
categories:
  - Design
  - Mobile
  - Apps
---
<p>Why is Google the search behemoth it is today? Part of the reason is because of how it’s transformed our ability to search for answers.</p>

<p>Think about something as simple as looking up the definition of a word. 20 years ago, you would’ve had to pull your dictionary off the shelf to find an answer to your query. Now, you open your phone or turn on your computer, type or speak the word, and get an answer in no time at all and with little effort on your part.</p>

<p>This form of digital shortcutting doesn’t just exist on search engines like Google. Mobile apps now have self-contained search functions as well.</p>

<p>Is a search bar even necessary in a mobile app interface or is it overkill? Let’s take a look at why the search bar element is important for the mobile app experience. Then, we’ll look at a number of ways to design search based on the context of the query and the function of the app.</p>

<div class="c-felix-the-cat">
<h4 class="h3">Using The Web With A Screen Reader</h4>
<p>Did you know that VoiceOver makes up 11.7% of desktop screen reader users and rises to 69% of screen reader users on mobile? It’s important to know what sort of first-hand difficulties visually impaired users face and what web developers can do to help. <a href="https://www.smashingmagazine.com/2018/12/voiceover-screen-reader-web-apps/" class="btn btn--medium btn--blue">Read a related article&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

## Mobile App Search Is Non-Negotiable

<p>The search bar has been a standard part of websites for years, but statistics show that it isn’t always viewed as a necessity by users. This data from Neil Patel and <a href="https://neilpatel.com/blog/ecommerce-website-search/">Kissmetrics</a> focuses on the perception and usage of the search bar on e-commerce <em>websites</em>:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff5c5c6b-8784-4936-8567-9583df3de5f7/neil-patel-search-vs-navigation.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff5c5c6b-8784-4936-8567-9583df3de5f7/neil-patel-search-vs-navigation.png" sizes="100vw" caption="Data from a Kissmetrics infographic about site search. (Source: <a href='https://neilpatel.com/blog/ecommerce-website-search/'>Kissmetrics</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff5c5c6b-8784-4936-8567-9583df3de5f7/neil-patel-search-vs-navigation.png'>Large preview</a>)" alt="Kissmetrics site search infographic" >}}

<p>As you can see, 60% of surveyed users prefer using navigation instead of search while 47% opt for filterable “search” over regular search functionality.</p>

<p>On a desktop website, this makes sense. When a menu is well-designed and well-labeled &mdash; no matter how extensive it may be &mdash; it’s quite easy to use. Add to that advanced filtering options, and I can see why website visitors would prefer that to search.</p>

<p>But mobile app users are a different breed. They go to mobile apps for different reasons than they do websites. In sum, they want a faster, concentrated, and more convenient experience. However, since smartphone screens have limited space, it’s not really feasible to include an expansive menu or set of filters to aid in the navigation of an app.</p>

<p>This is <strong>why mobile apps need a search bar.</strong></p>

<p>You’re going to find a lot of use for search in mobile apps:</p>

<ul>
<li>Content-driven apps like newspapers, publishing platforms, and blogs;</li>
<li>e-Commerce shops with large inventories and categorization of those inventories;</li>
<li>Productivity apps that contain documents, calendars, and other searchable records;</li>
<li>Listing sites that connect users to the right hotel, restaurant, itinerary, item for sale, apartment for rent, and so on;</li>
<li>Dating and networking apps that connect users with vast quantities of “matches”.</li>
</ul>

<p>There are plenty more reasons why you’d need to use a search bar on your mobile app, but I’m going to let the examples below speak for themselves.</p>

{{% ad-panel-leaderboard %}}

## Ways To Design Search For Your Mobile App

<p>I’m going to break down this next section into two categories:</p>

<ol>
    <li>How to <a href="#designing-physical-search-element">design the physical search element</a> in your mobile app,</li>
    <li>How to <a href="#designing-search-bar-results-context">design the search bar and its results</a> within the context of the app.</li>
</ol>

### 1. Designing The Physical Search Element

<p>There are a number of points to consider when it comes to the physical presence of your app search element:</p>

#### Top Or Bottom?

<p><a href="https://medium.muz.li/designing-search-for-mobile-apps-ab2593e9e413">Shashank Sahay explains</a> why there are two places where the search element appears on a mobile app:</p>

<ul>
    <li><strong>1. Full-width bar at the top of the app.</strong><br />This is for apps that are driven by search. Most of the time, users open the app with the express purpose of conducting a search.</li>
</ul>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e687281-5c2e-4ac1-81a9-c28a740f5ebd/facebook-search-bar.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e687281-5c2e-4ac1-81a9-c28a740f5ebd/facebook-search-bar.png" sizes="100vw" caption="Facebook prioritizes app search by placing it at the top. (Source: <a href='https://www.facebook.com/'>Facebook</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e687281-5c2e-4ac1-81a9-c28a740f5ebd/facebook-search-bar.png'>Large preview</a>)" alt="Facebook app search" >}}

<p><a href="https://www.facebook.com/">Facebook</a> is a good example. Although Facebook users most likely do engage with the news feed in the app, I have a sneaking suspicion that Facebook’s data indicates that the search function is more commonly engaged with &mdash; at least in terms of first steps. Hence, why it’s placed at the top of the app.</p>

<ul>
    <li><strong>2. A tab in the bottom-aligned navigation bar.</strong><br />This is for apps that utilize search as an enhancement to the primary experience of using the app’s main features.</li>
</ul>

<p>Let’s contrast Facebook against one of its sister properties: <a href="https://www.instagram.com/">Instagram</a>. Unlike Facebook, Instagram is a very simple social media app. Users follow other accounts and get glimpses into the content they share through full-screen story updates as well as from inside their endless-scroll news feed.</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/461827d3-989e-4776-875a-f1f5b5e496d1/instagram-search-button.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/461827d3-989e-4776-875a-f1f5b5e496d1/instagram-search-button.png" sizes="100vw" caption="Instagram places its search function in the bottom navigation bar. (Source: <a href='https://www.instagram.com/'>Instagram</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/461827d3-989e-4776-875a-f1f5b5e496d1/instagram-search-button.png'>Large preview</a>)" alt="Instagram app search" >}}

<p>With that said, the search function does exist in the navigation bar so that users can look up other accounts to peruse through or follow.</p>

<p>As far as this basic breakdown goes, Sahay is right about how placement of search correlates with intention. But the designing of the search element goes beyond just where it’s placed on the app.</p>

#### Shallow Or Deep?

<p>There will be times when a mobile app would benefit from a search function deep within the app experience.</p>

<p>You’ll see this sort of thing quite often in e-commerce apps like <a href="https://www.bedbathandbeyond.com/">Bed Bath & Beyond</a>:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2da245ed-a8cb-45de-9f0c-420d53c0e287/bbb-search-stores.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2da245ed-a8cb-45de-9f0c-420d53c0e287/bbb-search-stores.png" sizes="100vw" caption="Bed Bath & Beyond uses deep search to help users find nearby stores (Source: <a href='https://www.bedbathandbeyond.com/'>Bed Bath & Beyond</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2da245ed-a8cb-45de-9f0c-420d53c0e287/bbb-search-stores.png'>Large preview</a>)" alt="Bed Bath & Beyond app search" >}}

<p>In this example, this search function exists outside of the standard product search on the main landing page. Results for this kind of search are also displayed in a unique way which is reflective of the purpose of the search:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c9e8a4d-1f18-4400-94ff-9a15c740ca49/bbb-search-map.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c9e8a4d-1f18-4400-94ff-9a15c740ca49/bbb-search-map.png" sizes="100vw" caption="Bed Bath & Beyond displays search results on a map. (Source: <a href='https://www.bedbathandbeyond.com/'>Bed Bath & Beyond</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c9e8a4d-1f18-4400-94ff-9a15c740ca49/bbb-search-map.png'>Large preview</a>)" alt="Bed Bath & Beyond map search results" >}}

<p>There are other ways you use might need to use “deep” search functions on e-commerce apps.</p>

<p>Think about stores that have loads of comments attached to each product. If your users want to zero in on what other consumers had to say about a product (for example, if a camping tent is waterproof), the search function would help them quickly get to reviews containing specific keywords.</p>

<p>You’ll also see deep searches planted within travel and entertainment apps like <a href="https://www.hotels.com/">Hotels.com</a>:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1c8b9fa-3f0b-4683-8934-be4ceea8af9d/hotels-deep-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1c8b9fa-3f0b-4683-8934-be4ceea8af9d/hotels-deep-search.png" sizes="100vw" caption="Hotels.com includes a deep search to narrow down results by property name. (Source: <a href='https://www.hotels.com/'>Hotels.com</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1c8b9fa-3f0b-4683-8934-be4ceea8af9d/hotels-deep-search.png'>Large preview</a>)" alt="Hotels.com app search" >}}

<p>You’re all probably familiar with the basic search function that goes with any travel-related app. You enter the details of your trip and it pulls up the most relevant results in a list or map format. That’s what this screenshot is of.</p>

<p>However, see where it says “Property Name” next to the magnifying glass? This is a search function within a search function. And the only things users can search for here are actual hotel property names.</p>

{{% ad-panel-leaderboard %}}

#### Bar, Tab, Or Magnifying Glass?

<p>This brings me to my next design point: how to know which design element to represent the search function with.</p>

<p>You’ve already seen clear reasons to use a full search bar over placing a tab in the navigation bar. But how about a miniaturized magnifying glass?</p>

<p>Here’s an example of how this is used in the <a href="https://www.youtube.com/">YouTube</a> mobile app:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b505bf19-a968-43c5-b7e8-c57d69b53281/youtube-search-glass.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b505bf19-a968-43c5-b7e8-c57d69b53281/youtube-search-glass.png" sizes="100vw" caption="YouTube uses a magnifying glass to represent its search function. (Source: <a href='https://www.youtube.com/'>YouTube</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b505bf19-a968-43c5-b7e8-c57d69b53281/youtube-search-glass.png'>Large preview</a>)" alt="YouTube app search icon" >}}

<p>The way I see it, the magnifying glass is the search design element you’d use when:</p>

<ul>
<li>One of the primary reasons users come to the app is to do a search,</li>
<li><em>And</em> it competes against another primary use case.</li>
</ul>

<p>In this case, YouTube needs the mini-magnifying glass because it serves two types of users:</p>

<ol>
<li>Users that come to the app to search for videos.</li>
<li>Users that come to the app to upload their own videos.</li>
</ol>

<p>To conserve space, links to both exist within the header of the YouTube app. If you have competing priorities within your app, consider doing the same.</p>

#### “Search” Or Give A Hint?

<p>One other thing to think about when designing search for mobile apps is the text inside the search box. To decide this, you have to ask yourself:</p>

<blockquote>“Will my users know what sort of stuff they can look up with this search function?”</blockquote>

<p>In most cases they will, but it might be best to include hint text inside the search bar just to make sure you’re not adding unnecessary friction. Here’s what I mean by that:</p>

<p>This is the app for <a href="https://www.airbnb.com/">Airbnb</a>:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d20a902d-e335-4543-9abc-833c9a07f683/airbnb-search-hint.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d20a902d-e335-4543-9abc-833c9a07f683/airbnb-search-hint.png" sizes="100vw" caption="Airbnb offers hint text to guide users to more accurate search results. (Source: <a href='https://www.airbnb.com/'>Airbnb</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d20a902d-e335-4543-9abc-833c9a07f683/airbnb-search-hint.png'>Large preview</a>)" alt="Airbnb app search text" >}}

<p>The search bar tells me to “Try ‘Costa de Valencia’”. It’s not necessarily an explicit suggestion. It’s more helping me figure out how I can use this search bar to research places to stay on an upcoming trip.</p>

<p>For users that are new to Airbnb, this would be a helpful tip. They might come to the site thinking it’s like Hotels.com that enables users to look up things like flights and car rentals. Airbnb, instead, is all about providing lodging and experiences, so this search text is a good way to guide users in the right direction and keep them from receiving a “Sorry, there are no results that match your query” response.</p>

### 2. Designing The Search Bar And Results In Context

<p>Figuring out where to place the search element is one point to consider. Now, you have to think about how to present the results to your mobile app users:</p>

#### Simple Search

<p>This is the most basic of the search functions you can offer. Users type their query into the search bar. Relevant results appear below. In other words, you leave it up to your users to know what they’re searching for and to enter it correctly.</p> 

<p>When a relevant query is entered, you can provide results in a number of ways.</p> 

<p>For an app like <a href="https://flipboard.com/">Flipboard</a>, results are displayed as trending hashtags:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b907f30-d7c2-4c6a-a16e-fb90f28eab25/flipboard-hashtag-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b907f30-d7c2-4c6a-a16e-fb90f28eab25/flipboard-hashtag-search.png" sizes="100vw" caption="Flipboard displays search results as a list of hashtags. (Source: <a href='https://flipboard.com/'>Flipboard</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b907f30-d7c2-4c6a-a16e-fb90f28eab25/flipboard-hashtag-search.png'>Large preview</a>)" alt="Flipboard app search results" >}}

<p>It’s not the most common way you’d see search results displayed, but it makes sense in this particular context. What users are searching for are categories of content they want to see in their feed. These hashtagged categories allow users to choose high-level topics that are the most relevant to them.</p>

<p><a href="https://www.espn.com/">ESPN</a> has a more traditional basic search function:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23943ab2-80d6-4413-a39c-67fc722a085f/espn-specific-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23943ab2-80d6-4413-a39c-67fc722a085f/espn-specific-search.png" sizes="100vw" caption="ESPN has designed its search results in a traditional list. (Source: <a href='https://www.espn.com/'>ESPN</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23943ab2-80d6-4413-a39c-67fc722a085f/espn-specific-search.png'>Large preview</a>)" alt="ESPN app search results" >}}

<p>As you can see, ESPN provides a list of results that contain the keyword. There’s nothing more to it than that though. As you’ll see in the following examples, you can program your app search to more closely guide users to the results they want to see.</p>

#### Filtered Search

<p>According to the aforementioned Kissmetrics survey, advanced filtering is a popular search method among website users. If your mobile app has a lot of content or a vast inventory of products, consider adding filters to the end of your search function to improve the experience further. Your users are already familiar with the search technique. Plus, it’ll save you the trouble of having to add advancements to the search functionality itself.</p>

<p><a href="https://www.yelp.com/">Yelp</a> has a nice example of this:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/616c1763-d488-43c2-9333-07a5d889fa27/yelp-filters.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/616c1763-d488-43c2-9333-07a5d889fa27/yelp-filters.png" sizes="100vw" caption="Yelp users have filter options available after doing a search. (Source: <a href='https://www.yelp.com/'>Yelp</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/616c1763-d488-43c2-9333-07a5d889fa27/yelp-filters.png'>Large preview</a>)" alt="Yelp app search filters" >}}

<p>In the search above, I originally looked for restaurants in my “Current Location”. Among the various filters displayed, I decided to add “Order Delivery” to my query. My search query then became:</p>

<blockquote>Restaurants > Current Location > Delivery</blockquote>

<p>This is really no different than using breadcrumbs on a website. In this case, you let users do the initial work by entering a search query. Then, you give them filters that allow them to narrow down their search further.</p>

<p>Again, this is another way to reduce the chances that users will encounter the “No results” response to their query. Because filters correlate to actual categories and segmentations that exist within the app, you can ensure they end up with valid search results every time.</p>

<p>e-Commerce websites are another good use case for filters. Here is how <a href="https://www.wayfair.com/">Wayfair</a> does this:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7635e1-f9ac-4be8-9f95-b9571cac7c3a/wayfair-filter-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7635e1-f9ac-4be8-9f95-b9571cac7c3a/wayfair-filter-search.png" sizes="100vw" caption="Wayfair includes filters in search to help users narrow down results. (Source: <a href='https://www.wayfair.com/'>Wayfair</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7635e1-f9ac-4be8-9f95-b9571cac7c3a/wayfair-filter-search.png'>Large preview</a>)" alt="Wayfair app search filters" >}}

<p>Wayfair’s list of search results is fairly standard for an e-commerce marketplace. The number of items are displayed, followed by a grid of matching product images and summary details.</p>  

<p>Here’s the thing though: Wayfair has a massive inventory. It’s the same with other online marketplaces like Amazon and Zappos. So, when you tell users that their search query produced 2,975 items, you need a way to mitigate some of the overwhelm that may come with that.</p>

<p>By placing the Sort and Filter buttons directly beside the search result total, you’re encouraging users to do a little more work on their search query to ensure they get the best and most relevant results.</p>

#### Predictive Search

<p>Autocomplete is something your users are already familiar with. For apps that contain lots of content, utilizing this type of search functionality could be majorly helpful to your users.</p>

<p>For one, they already know how it works and so they won’t be surprised when related query suggestions appear before them. In addition, autocomplete offers a sort of personalization. As you gather more data on a user as well as the kinds of searches they conduct, autocomplete anticipates their needs and provides a shortcut to the desired content.</p>

<p><a href="https://www.pinterest.com/">Pinterest</a> is a social media app that people use to aggregate content they’re interested in and to seek out inspiration for pretty much anything they’re doing in life:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cab59b5-da6f-46ca-bb65-f7345b186514/pinterest-autocomplete.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cab59b5-da6f-46ca-bb65-f7345b186514/pinterest-autocomplete.png" sizes="100vw" caption="Pinterest anticipates users’ search queries and provides autocomplete shortcuts. (Source: <a href='https://www.pinterest.com/'>Pinterest</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cab59b5-da6f-46ca-bb65-f7345b186514/pinterest-autocomplete.png'>Large preview</a>)" alt="Pinterest app search autocomplete" >}}

<p>Take a look at the search results above. Can you tell what I’ve been thinking about lately? The first is how I’m going to decorate my new apartment. The second is my next tattoo. And despite only typing out the word “Small”, Pinterest immediately knew what’s been top-of-mind with me as of recent. That doesn’t necessarily mean I as a user came to the app with that specific intention today… but it’s nice to see that personalized touch as I engage with the search bar.</p>

<p>Another app I engage with a lot is the <a href="https://www.apple.com/">Apple</a> Photos app:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/093f4408-367e-4f40-a056-283f1d165470/apple-photos-autocomplete-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/093f4408-367e-4f40-a056-283f1d165470/apple-photos-autocomplete-search.png" sizes="100vw" caption="Apple Photos uses autocomplete to help users find the most relevant photos. (Source: <a href='https://www.apple.com/'>Apple</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/093f4408-367e-4f40-a056-283f1d165470/apple-photos-autocomplete-search.png'>Large preview</a>)" alt="Apple Photos app search" >}}

<p>In addition to using it to store all of my personal photos, I use this on a regular basis to take screenshots for work (as I did in this article). As you can imagine, I have a lot of content saved to this app and it can be difficult finding what I need just by scrolling through my folders.</p>

<p>In the example above, I was trying to find a photo I had taken at Niagara Falls, but I couldn’t remember if I had labeled it as such. So, I typed in “water” and received some helpful autocomplete suggestions on “water”-related words as well as photos that fit the description.</p>

<p>I would also put “Recent Search” results into this bucket. Here’s an example from <a href="https://www.uber.com/">Uber</a>:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c100fef0-4c92-45da-89aa-2a896f2bbaac/uber-location-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c100fef0-4c92-45da-89aa-2a896f2bbaac/uber-location-search.png" sizes="100vw" caption="Uber’s recent search results provide one-click shortcuts to repeat users. (Source: <a href='https://www.uber.com/'>Uber</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c100fef0-4c92-45da-89aa-2a896f2bbaac/uber-location-search.png'>Large preview</a>)" alt="Uber app recent search results" >}}

<p>Before I even had a chance to type my search query in the Uber app, it displays my most recent search queries for me.</p>

<p>I think this would be especially useful for people who use ride-sharing services on a regular basis. Think about professionals who work in a city. Rather than own a car, they use Uber to transport to and from their office as well as client appointments. By providing a shortcut to recent trips in search results, the Uber app cuts down the time they spend booking a trip.</p>

<p>If you have enough data on your users and you have a way to anticipate their needs, autocomplete is a fantastic way to personalize search and improve the overall experience.</p>

#### Limited Search

<p>I think this time savings point is an important one to remember when designing search for mobile apps.</p>

<p>Unlike websites where longer times-on-page matter, that’s not always the case with mobile apps. Unless you’ve built a gaming or news app where users should spend lots of time engaging with the app on a daily basis, it’s not usually the amount of time spent inside the app that matters.</p>

<p>Your goal in building a mobile app is to <a href="https://www.smashingmagazine.com/2018/10/mobile-app-retention-rate/">retain users over longer periods</a>, which means providing a meaningful experience while they’re inside it. A well-thought-out search function will greatly contribute to this as it gets users immediately to what they want to see, even if it means they leave the app just a few seconds later.</p>

<p>If you have an app that needs to get users in and out of it quickly, think about limiting search results as <a href="https://ibotta.com/">Ibotta</a> has done:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5728a6a-993f-44ea-9f55-9b60aa65a796/ibotta-recent-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5728a6a-993f-44ea-9f55-9b60aa65a796/ibotta-recent-search.png" sizes="100vw" caption="Ibotta displays categories that users can search in. (Source: <a href='https://ibotta.com/'>Ibotta</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5728a6a-993f-44ea-9f55-9b60aa65a796/ibotta-recent-search.png'>Large preview</a>)" alt="Ibotta app search categories" >}}

<p>While users certainly can enter any query they’d like, Ibotta makes it clear that the categories below are the only ones available to search from. This serves as both a reminder of what the app is capable of as well as a means for circumventing the search results that don’t matter to users.</p>

<p><a href="https://www.hotels.com/">Hotels.com</a> also places limits on its search function:</p>

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4d2bd8f-3d77-46b4-b161-1347492580d2/hotels-highlighted-search.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4d2bd8f-3d77-46b4-b161-1347492580d2/hotels-highlighted-search.png" sizes="100vw" caption="Hotels.com forces users to make a choice so they don’t end up with too many results. (Source: <a href='https://www.hotels.com/'>Hotels.com</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4d2bd8f-3d77-46b4-b161-1347492580d2/hotels-highlighted-search.png'>Large preview</a>)" alt="Hotels.com limiting search results" >}}

<p>As you can see here, users can’t just look for hotels throughout the country of Croatia. It’s just too broad of a search and one that Hotels.com shouldn’t have to provide. For one, it’s probably too taxing on the Hotels.com server to execute a query of that nature. Plus, it would provide a terrible experience for users. Imagine how many hotels would show up in that list of results.</p>

<p>By reining in what your users can search for and the results they can see, you can improve the overall experience while shortening the time it takes them to convert.</p>

## Wrapping Up

<p>As you can see here, a search bar isn’t some throwaway design element. When your app promises a speedy and convenient experience to its users, a search bar can cut down on the time they have to spend inside it. It can also make the app a more valuable resource as it doesn’t require much work or effort to get to the desired content.</p>

{{< signature "ra, yk, il" >}}
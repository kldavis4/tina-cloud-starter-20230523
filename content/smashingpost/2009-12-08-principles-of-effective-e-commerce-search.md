---
title: Principles Of Effective Search In E-Commerce Design
slug: principles-of-effective-e-commerce-search
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d264db26-6abc-418a-9ef4-ce3320229422/ecommerce-bag.jpg
date: 2009-12-08T13:34:24.000Z
author: rung-andras
description: >-
  While product **findability** is a **key factor of success** in e-commerce, it is predominantly enabled by simple search alone. And while simple search usually doesn't fulfill complex needs among users, website developers and owners still regard advanced search as just another boring to-do item during development. Owners won't go so far as to leave it out, because every e-commerce website has some kind of advanced search functionality, but they probably do not believe it brings in much revenue.
categories:
  - UX
  - E-Commerce
  - Usability
---
On the contrary, well-devised advanced search offers several benefits and can be more than just a clumsy, complicated tool. First of all, effective search can accelerate the sales process. And faster sales can **increase conversions**, because you will not be losing customers who give up trying to find products. Furthermore, fast, precise and successful searches increase your customers' trust.

In this article, we will review how to build an interface that offers users the **power of advanced search** while preserving the **clarity of simple search**.

Also consider our previous articles:

*   [Search Results Design: Best Practices and Design Patterns](https://www.smashingmagazine.com/2009/09/28/search-results-design-best-practices-and-design-patterns/ "Search Results Design: Best Practices and Design Patterns")
*   [Designing The Holy Search Box: Examples And Best Practices](https://www.smashingmagazine.com/2008/12/04/designing-the-holy-search-box-examples-and-best-practices/ "Designing The Holy Search Box: Examples And Best Practices")
*   [15 Common Mistakes in E-Commerce Design](https://www.smashingmagazine.com/2009/10/08/15-common-mistakes-in-e-commerce-design-and-how-to-avoid-them/ "15 Common Mistakes in E-Commerce Design")

{{% feature-panel %}}

## 1\. Dismantling Barriers

Although almost every e-commerce website has advanced search, visitors do not use it. First of all, people only use tools that they see. Advanced search is usually hard to detect. The link is usually too small and ugly, and so the flashy simple search button nearby overwhelms it. So even if the user was inclined to perform an advanced search, they have no motivation to do it.

The word itself is scary: "advanced." It suggests we are about to encounter something complicated. And very often, we do. But even if we notice the advanced search link and are not intimidated by it, we don't use it because we **don't see the benefit**. The few who do use it see that once they perform the search, all "advanced-ness" is lost. So, to help our users exploit the power of advanced search, we have to fix usability problems, implement new approaches and improve our search terminology.</p>

## 2\. Approaches

There are several ways to enhance search. The classic approach for advanced search is **parameter search**. The user sets parameters using text boxes, operators and drop-down menus. When [usability gurus tell you not to use advanced search](https://www.useit.com/alertbox/20010513.html), they are generally referring to this type. It usually has a complicated interface but can be very simple and effective if only the most important fields are shown and you stick to the basic guidelines of form design.

[![momondo.com parameter search interface](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e57bcac7-d795-44fa-93a0-bcca14bd6356/momondo-e-commerce.jpg)](https://www.momondo.com)  
_[Momondo](https://www.momondo.com) elegantly and effectively sticks to the most important input fields, making parameter search user-friendly._

[![trulia.com parameter search interface](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7371282e-efab-494f-bf6c-9028aeced383/trulia-e-commerce.jpg)](https://www.trulia.com)  
_[Trulia](https://www.trulia.com)'s parameter search is a bit more complicated but thoughtfully supported by input hints and prompts. Even more options are hidden under the "More search options" link for advanced users._

A good way to avoid intimidating people is to disguise the complexity of the parameter search. Show only snippets of the interface by using the [responsive disclosure](https://www.designinginterfaces.com/Responsive_Disclosure)/[responsive enabling pattern](https://www.designinginterfaces.com/Responsive_Enabling). When the user sets a parameter, they move along, and then the next filter is shown. This solution can be useful for guiding novice users, but it can bore and irritate advanced users.

[![mybanktracker.com responsive disclosure pattern](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/898f4ab5-6daa-42f2-b1ce-875a421fabe8/mybanktracker-e-commerce.jpg)](https://www.mybanktracker.com/)  
_On [MyBankTracker](https://www.mybanktracker.com/), users have to select "Yes" for the "Compare your bank APY" option for the "What is your current APY?" question to be displayed._

**Faceted search** is becoming the de facto standard for e-commerce website. The user performs a simple search first, but then on the results page, they can narrow the search through a drill-down link (for a single choice) or a checkbox selection (for multiple non-overlapping choices).

This can be faster than the progressive disclosure/enabling pattern and easier to use than plain advanced search. [Amazon](https://www.amazon.com/) takes a similar but slightly modified approach: when a user begins a search, they can set some narrowing filters like "Only books" at the very start.

[![amazon.com filtered search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb83d2b2-5b07-446f-b7d7-cc0050cfeeb6/amazon-e-commerce.jpg)](https://www.amazon.com/)  
_Filtering on [Amazon](https://www.amazon.com/)._

[![plusplus.com filtered search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bef30e44-dea7-4599-ad40-6c05a6069bf0/plusplus-e-commerce.jpg)](https://www.plusplus.com/)  
_The search filtering on [Plus+](https://www.plusplus.com/) is a bit more complex but still easy to use. Again, it is supported by input hints and prompts._

## From here

[![kontain.com filtered search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b9c1677-35bb-453b-aad8-26629c57a71e/kontain-e-commerce.jpg)](https://www.kontain.com/)  
_[Kontain](https://www.kontain.com/) emphasizes the most important filtering options with different colors._

[![cleartrip.com parameter search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/806e29a8-3b61-4b83-9978-50557cb6c683/cleartrip-e-commerce.jpg)](https://www.cleartrip.com/)

[![cleartrip.com faceted search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe45006e-d038-4695-8968-ac75689e1b32/cleartrip2-e-commerce.jpg)](https://www.cleartrip.com/)  
_Travelers begin with a parameter search on [Cleartrip](https://www.cleartrip.com/) but then find the best deal with faceted search._

Website maintainers may choose to tag products, or even let users tag them themselves. **Tagging** gives a website an overlapping taxonomy so that users have different ways to reach products.

[![issuu.com tagging](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b02d9da-fb96-42bb-acf0-3a4b870cd520/issuu-e-commerce.jpg)](https://www.issuu.com/)  
_After a user performs a keyword search, [Issuu](https://www.issuu.com/) shows related tags to help the user narrow down the results. Note that the tags that are semantically closer to the search term have brighter colors._

## 3\. Building Better Search

**Faceted search** is the easiest and now safest method by which developers can offer users advanced search functionality. But how to implement it?

Before undertaking something as time-consuming as that, make sure your **website conforms to basic search usability principles**. Is the search box in the right place? Does it work as expected?

The structure of the search results page must also be crystal clear. The results must be ranked in a logical order (i.e. for the user, not for you) by relevance. Users should be able to scan and comprehend the results easily. Queries should be easy to refine and resubmit, and the search results page should show the query itself.

Consider basic user needs and behavior when planning search. You could frame it as adopting an "incremental construction" pattern. **Let users create their own search, step by step**. People may not comprehend the whole system at once, but if you guide them gently, searching will be made easier. Make their exploration of search functionality safe: users should be reassured that they can undo any option and not lose their results or settings.

[![myfonts.com incremental construction pattern](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd96486a-177a-4373-af93-d2a4c13089ab/myfonts-e-commerce.jpg)](https://myfonts.com/)  
_[MyFonts](https://www.myfonts.com/) allows users to control the complexity of their queries by using the **-** and **+** buttons to add and remove filters._

Your imagination may be a good start in defining which features deserve facets, but it is far from enough. Examine the traffic from your website and the search terms that users have typed into the simple search interface. Analyzing search query logs helps you handle spelling issues more effectively. Based on your analysis, you can also refine your [auto-suggest system](https://www.getelastic.com/trendspotting-rich-autocomplete-in-site-search/). What words, categories or taxonomy would describe these searches best? Use the most popular words in your search logs to label your facets and options.

Don't forget to check your competitors’ categories either. Perhaps you would sort your products differently, but you may get good ideas from them. When you have sorted out your facets, test them with real users. Don't just test the interface during the final phase; let users play with earlier versions as well.

## 4\. Categorizing Products

Let users choose from among only the **features** that might **influence their purchase**. Omit features that are not important to users, even if you think they are. Features rarely chosen by customers should be put at the end of the list or hidden under a "More options" link.

[![pricegrabber.com wine categories](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2719dc13-0cb1-4835-bc74-ddeeaa4047b1/pricegrabber-e-commerce.jpg)](https://www.pricegrabber.com/)  
_[PriceGrabber](https://www.pricegrabber.com/) allows users to control the complexity of their queries by using the **-** and **+** buttons to add and remove filters._

For your facets to work perfectly, you need a good **taxonomy (categories)**. If users don't understand your system, you lose. Don't make users have to guess your system. Figure out their mental model of your product range first. The categories in your taxonomy **should cover all products without overlap**. For example, if a user can filter by color, do not omit colorless items in the results, or items for which color is irrelevant. Avoid vague words like "Other" and "More." The category hierarchy should be shallow, so that users do not have to drill too deep to find a product.</p>

## 5\. Architecture Of Search

Although faceted search is much easier to use than the classic advanced search, it can become complex if too many facets are shown. Based on [George A. Miller's research, humans can deal adequately with 7 items, plus or minus 2](https://en.wikipedia.org/wiki/The_Magical_Number_Seven,_Plus_or_Minus_Two). This short-term memory constraint also informs the popular recommendation of the number of items to include in a navigation menu. **Don't have more than 10 facets**. Any more will confuse users, and the results will be about as helpful as the Dewey Decimal system.

Hide extra facets under a "More filters" link, even if you think they're all important. Everything cannot be equally important. If you think certain facets will be important for one user group and other facets important for another, then create a **drag-and-drop** interface, and allow users to **close facets**. Letting them save results or facet settings is useful, too, but make sure unregistered users can do it as well.

[![globrix.com closable panels](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fb7813c-b390-467c-885c-328e204c143a/globrix-e-commerce.jpg)](https://www.globrix.com/)  
_[Globrix](https://www.globrix.com/) has many facets, but the interface can be cleaned up easily by closing unused ones._

**Order facets by importance**. Most users will use only a few. Display only filter values that apply to the inventory you have available. If a facet has more than seven or eight options, put the extra options under a "More options" link or a different panel.

[![theperfumeshop.com facets](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3538843e-7d66-4d8f-921c-c73b6258fce5/theperfumeshop-e-commerce.jpg)](https://www.theperfumeshop.com/)  
_[The Perfume Shop](https://www.theperfumeshop.com/) gives priority to age and price. Note that it also indicates what is available in a given price range._

[![ratemyarea.com facets on panels](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bef18401-7ec1-41db-8cbf-5fd6e0576d74/ratemyarea-e-commerce.jpg)](https://www.ratemyarea.com/)  
_[Rate My Area](https://www.ratemyarea.com/) offers an unconventional combo input box to begin a search, but its role is communicated clearly. After performing a search, the user can access various facets in different panels._

Faceted search is still **keyword-driven**. If products would be easier to find by referring to categories or if users will have problems identifying their needs, then use filtered search or a well-designed parameter search. Faceted search is cool but not a cure-all.

[![wizzair.com map search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/86cd97bc-6c5b-47b7-a752-a9b4fc91c80b/wizzair-e-commerce.jpg)](https://www.wizzair.com/)  
_You do not have to type in your flight destination at [Wizz Air](https://www.wizzair.com/). Simply select it from a map._

## 6\. Enhancing Search

Whatever method you choose, you have several means of enhancing search. Do not automatically order the results page of the most frequent queries. Prioritize what you think **best matches the search** (i.e. the best bets). Add popular queries to the ones you've verified, and review the most popular results from time to time.

[![apple.com best bets](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa6d19b9-c963-480d-bb16-290b3f4a21be/apple-e-commerce.jpg)](https://www.apple.com/)  
_[Apple](https://www.apple.com/) puts what most users look for front and center. These best bets are supported with pictures._

**Cluster results** based on your or your users' tags, or get clustering algorithms to do the job. Clustering groups search results into categories but must be implemented with a powerful algorithm that can compete (or at least cooperate) with human tagging.

[![flickr clustering](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3b1b1c6d-4492-42a6-b61b-c83cfca661bf/flickr-e-commerce.jpg)](https://www.flickr.com/)  
_Tag clusters on [Flickr](https://www.flickr.com/) group results._

**Spell-check** is also crucial. Many products have names that are hard to remember or type correctly. Users might think to correct their misspelling when they find poor results, but they will be annoyed at having to do that... or worse, they might think that the website either doesn't work properly or does not have their product.

[![ebay.com spell checker](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cf53e717-e7fc-4209-adc0-be22a0f541e0/ebay-e-commerce.jpg)](https://www.ebay.com/)  
_[eBay](https://www.ebay.com/) helps users type complicated words._

**Auto-suggestions** can decrease the problems caused by mistyping or not knowing the proper terminology. Queries usually start with words, so unambiguous character inputting is crucial.

[![getsatisfaction.com autosuggestion](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7c74b67-8760-4f2f-8039-86263f5d2ab1/getsatisfaction-e-commerce.jpg)](https://www.getsatisfaction.com/)  
_[Get Satisfaction](https://www.getsatisfaction.com/) offers auto-suggestion that is easily scannable and structured._

If your results are somehow able to be localized in the real world, always **show them on a map.**

[![mybanktracker.com results on the map](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85540293-0311-43be-b352-48e6128c30e3/mybanktracker2-e-commerce.jpg)](https://www.mybanktracker.com/)  
_[MyBankTracker](https://www.mybanktracker.com/) shows its results on Google's well-known map. The pins are fairly big so that users can see what's on them, while the transparency maintains visual consistency._

## 7\. Communication And Language

The **success of your search** depends heavily on your users' understanding of what facets, filters and parameters do. Label them in easily understood language. Think about non-native English speakers as well. Communicate the benefits of advanced search clearly and concisely, and show visitors that advanced search helps them be more effective. Change the terrifying phrase "Advanced search" to something friendlier, like "Better search" or "Smart search." If your advanced search functionality is integrated in the simple search area, just name the whole tool "Search."

[![officemax.com unambiguous labeling](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bdcb575-5930-4b3d-8d66-bc5bc4474578/officemax-e-commerce.jpg)](https://www.officemax.com/)  
_[OfficeMax](https://www.officemax.com/) names labels facets in simple and unambiguous language._

## 8\. Grouping And Alignment

**Group similar items** and **separate different items** clearly. Indicate what is selected or not selected. Use a "Select" button that turns into an "Unselect" button when the user selects something, rather than a "Select all" checkbox (after checking "Select all," the user might want to check other boxes, in which case the system might not behave consistently). When you arrange items in a facet, think of what would be the most common workflow for using the facet.

[![yourwebjob.com checkboxes](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b8556bc-6a6c-446e-9b27-7d9697ecee3b/yourwebjob-e-commerce.jpg)](https://www.yourwebjob.com/)  
_[Your Web Job](https://www.yourwebjob.com/) provides checkboxes for narrowing a search. The page has no search button; when the user finishes typing, the search begins. Although this way of handling search is unconventional, it works because the feature is fast._

Several **interface patterns** are available to make search more usable. Titled sections can effectively separate facets. Use bigger font for titles, and position them close to the content. Allow panels to be closed and moved. Align labels flush with input fields to make them more scannable, even when they vary in length. If you have a lot of facets or if the filters on the search results page have many options, you can arrange them using <span class="removed_link" title="https://www.time-tripper.com/uipatterns/Card_Stack">card stacks</span>. But beware, information that users manipulate in one card won't be visible when they manipulate another. They may forget their settings or assume that search results will be based on the last-manipulated facet and that earlier filtering has been undone.

![comet.co.uk closable facets](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ffb8b71-2e6e-46f4-87b2-722f5cc76635/comet-e-commerce.jpg)  
_Comet lets users narrow their searches by clicking on facet links. Users can close and add facets, and the groupings show unambiguously what belongs to which facet. Note that Comet shows the number of items in a category beside each link._

**Diagonal balance** and a **liquid layout** make a search interface more usable. If users are able to change the size of the search interface, be aware of what happens to labels and values in drop-down lists when the size is set very small. Beautiful interfaces can fall apart if their behavior is not tested at many screen resolutions. And don't forget about mobile users, even if you don't have a mobile version yet.

**Buttons** play an important role in a search interface. Have as few as possible, but anything that triggers an action should be a button. Do not disguise such functionality with a non-button-like element. Label meaningfully; avoid vague words like "Okay" and "Done." Make buttons stand out on the page so that users see them when they've finished what they're doing. Place buttons at the end of workflows. Do not put anything that can modify the results of a button-triggered action after the button.</p>

## 9\. Forms And Controls

The design of facets is up to you. Text boxes and drop-down lists are usually more than enough, but you might want to use other things that can make forms and controls more usable.

Choose **sensible defaults** for radio buttons and drop-down lists. Also, illustrations often convey information much better than words. For example, illustrating types of mobile phones is much less clumsier than describing them. Forgiving formats and structured formats help users input useful queries. Forgiving formats give users flexibility in entering data, while structured formats help them enter data more precisely.

[![vodafone.co.uk illustrated choices](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b5808dd-89e9-473c-9d4b-cfe1ffc1f848/vodafone-e-commerce.jpg)](https://vodafone.co.uk/)  
_[Vodafone](https://vodafone.co.uk/) uses simple yet attractive icons to help users choose quickly._

**Input prompts** tell users what to do or type in a field, whereas **input hints** explain to users what they are expected to input in a field. Use them wisely: input prompts can be deleted, and too many input hints will annoy users. Also, the visual clutter might make them simply ignore important information.

[![tripadvisor.com illustrated choices](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa0840a3-73fb-4660-82ee-dde7c7e4e262/tripadvisor-e-commerce.jpg)](https://www.tripadvisor.com/)  
_[TripAdvisor](https://www.tripadvisor.com/) uses input hints, illustrated options and sensible defaults to enhance the usability of its parameter search._

## 10\. Handling Results

**Use dynamic filtering** where possible. Users want immediate results, so don't disappoint. If dynamic filtering would make your architecture too slow, consider reprogramming the page or narrowing the number of options. It might be worth it.

Show the **number of actual results** as well as the number of results the user would get if they were to filter by some other options. "List" and "tiled" are the basic views, but **alternative views** could help users scan results more easily.</p>

## 11\. Conclusion

Contrary to widespread belief, advanced search is not an old lumbering monster of the past. If usability is taken into account and key structural and conceptual modifications are made, it can be an effective tool for **increasing conversions** and helping your users access more products. Of course, not every e-commerce website needs advanced search. You may have too few products or your products may be unique and hard to categorize. Advanced or faceted search is more useful when you have a wide variety of products.</p>

### Showcase of Effective Search Interfaces

<span class="removed_link" title="https://www.topsy.com/">![topsy.com faceted search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5c51e2d-52de-4704-8aea-c20de1505a90/topsy-e-commerce.jpg)</span>  
_<span class="removed_link" title="https://www.topsy.com/">Topsy</span> implements just one facet, but the visual accents are effective._

[![collabfinder.com illustrated choices](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e982b8c7-7521-4636-9447-d2aa263832d9/amazon-e-commerce.png)](https://collabfinder.com/)  
_[Collabfinder](https://collabfinder.com/) helps users with input hints in the parameter search._

[![mozilla.org combined faceted and advanced search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e12a04ce-1307-4f90-83ab-a9b54236358f/firefox-e-commerce.jpg)](https://addons.mozilla.org/en-US/firefox/)  
_[Firefox](https://addons.mozilla.org/en-US/firefox/) combines parameter search with faceted search in a complex but easy-to-use interface._

[![delicious.com check box selection](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f687c59-ea2b-4420-afd9-d1e1e7657615/delicious-e-commerce.jpg)](https://delicious.com/)  
_[Delicious](https://delicious.com/) allows filtering by tags and auto-suggests during searches._

[![rofo.com filtered search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4d9206ff-c49e-495c-9f06-3ef2b7fa0257/rofo-e-commerce.jpg)](https://www.rofo.com/)  
_[Rofo](https://www.rofo.com/) implements a slider and drop-down menu in its filtered search. Users can refine their search results with facets, too._

![grooveshark.com filtered search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f466a08-288b-434d-ad53-b66657b4293f/grooveshark-e-commerce.jpg)  
_Grooveshark filters by tabs. It could have used a drop-down menu, but this solution lets users see all of their options at once._

[![fansnap.com illustrated choices, good defaults](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74a7e1c2-88e3-4483-8ba0-6ac167d6a3ec/fansnap-e-commerce.jpg)](https://www.fansnap.com/)  
_[FanSnap](https://www.fansnap.com/) uses illustrations and good defaults to handle complex data. Putting the search results on the left is a bit unusual, but good visual highlighting helps users understand the role of each tool._

![thedubaimail.com filtered search](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5dda330-5914-4297-b941-cdbda8b394bb/thedubaimail-e-commerce.jpg)  
_A simple yet elegant implementation of filtered search by [The Dubai Mall](https://www.thedubaimall.com/)._

![like.com colour chooser](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b07d1ad-ad1e-4962-9b40-dd870cc96ca3/like-e-commerce.jpg)  
_Like.com includes a color-picker panel as part of its filtering options. The visual samples help, because color names have different meanings for different people._

## Further Resources

*   [Best Practices for Designing Faceted Search Filters](https://www.uxmatters.com/mt/archives/2009/09/best-practices-for-designing-faceted-search-filters.php)

{{< signature "al" >}}


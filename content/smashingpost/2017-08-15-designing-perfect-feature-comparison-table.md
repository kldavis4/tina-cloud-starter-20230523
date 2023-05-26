---
title: Designing The Perfect Feature Comparison Table
slug: designing-perfect-feature-comparison-table
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/768911a0-3bf9-4fa9-beb4-7a566267e985/feature-comparison-example-preview-opt.png
date: 2017-08-15T16:40:30.000Z
summary: >-
  For a price tag that meets a certain threshold, we want to be _absolutely_ certain that we are making the right choice and are getting a good deal. That's where a **feature comparison table** makes all the difference.
description: >-
  For a price tag that meets a certain threshold or if we are particularly invested in the quality of a product, we want to be _absolutely_ certain that we are making the right choice and are getting a good product for a good price. That's where a **feature comparison table** makes all the difference.
categories:
  - Coding
  - E-Commerce
  - UX
  - Design Patterns
  - Web Design
  - Guides
  - Best Practices
---

Feature comparison tables are helpful not only in their primary function, though. When designed properly, they can aid in decision-making way beyond placing product specifications side by side. They can also add meaning to an otherwise too technical product specification sheet, explaining _why_ a certain feature is relevant to the customer or _how_ a certain product is better than the others.

After our close examination of [accordions](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/), [time and date pickers](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/) and [sliders](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/), in this article we'll look into all of the fine details that make a **perfect, accessible and helpful feature comparison table**. Please note that this article isn't necessarily about pricing plans, nor is it about data visualization methods. Rather, it's tailored specifically for the case where a customer wants to confirm their purchasing choice or can't choose between one of multiple preselected items.

Before diving into design decisions, we need to properly understand the user's goals, intentions and behavioral patterns.

<div class="c-felix-the-cat">
<h4 class="h3">Part Of: <a href="/category/design-patterns/">Design Patterns</a></h4>
<ul>
<li>Part 1: <a href="https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/">Perfect Accordion</a></li>
<li>Part 2: <a href="https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/">Perfect Responsive Configurator</a></li>
<li>Part 3: <a href="https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/">Perfect Date and Time Picker</a></li>
<li>Part 4: <strong>Perfect Feature Comparison</strong></li>
<li>Part 5: <a href="https://www.smashingmagazine.com/2017/07/designing-perfect-slider/">Perfect Slider</a></li>
<li>Part 6: <a href="https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/">Perfect Birthday Picker</a></li>
<li>Part 7: <a href="https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-mega-dropdown-hover-menus/">Perfect Mega-Dropdown Menus</a></li>
<li>Part 8: <a href="https://www.smashingmagazine.com/2021/07/frustrating-design-patterns-broken-frozen-filters/">Perfect Filters</a></li>
<li>Part 9: <a href="https://www.smashingmagazine.com/2021/08/frustrating-design-patterns-disabled-buttons/">Disabled Buttons</a></li>
<li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next ones.</li>
</ul>
</div>

## When Is A Feature Comparison Useful?

In observing customers in a few e-commerce projects, I found it quite revealing to notice how seemingly irrelevant a comparison feature appears to be to many customers. Quite often users will say that it clutters the interface, and that they never use the feature. The reason for it is simple: While we tend to purchase small low-priced items quite often, we tend to buy large high-priced items not so frequently. In fact, there are just not _that_ many situations where we actually _need_ a feature comparison.

<figure><a href="https://home.liebherr.com/en/ltu/products/household-appliances/floor-mounted-appliances-for-households/freezer-compartments/freezer-compartments.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/280a28b2-f7ce-4227-a527-244f851da7a8/liebherr-no-comparison-800w-opt.png" width="800" height="566" alt="Feature comparison table on Liebherr." /></a><figcaption>Often feature comparison is complemented with filters that help customers limit the scope of options. <a href="https://home.liebherr.com/en/ltu/products/household-appliances/floor-mounted-appliances-for-households/freezer-compartments/freezer-compartments.html">Liebherr</a> uses filters alone, avoiding feature comparison altogether. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6e8522f-4a99-4392-b467-0d0d916b665c/liebherr-no-comparison-large-opt.png">Large preview</a>)</figcaption></figure>

Not many customers would even think of comparing a few books or pairs of socks. However, relatively few customers would purchase a coffee machine or refrigerator without exploring their options thoroughly. A feature comparison is indeed irrelevant for "small" purchases, but it becomes important for "large" purchases. In fact, when customers are committed to making a large purchase but can't choose which product to buy, they are likely to end up not buying altogether, getting locked up in the choice paralysis. As a retailer, we obviously want to avoid these deadlock situations, and that's where a feature comparison element can be very useful, simplifying the decision-making process and filtering out items that don't meet relevant criteria.

<figure><a href="https://www.abcam.com/nav/proteins-and-peptides"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03ed09db-1cea-44c5-8a7b-a53de262f367/chemicals-800w-opt.png" width="800" height="504" alt="Feature comparison table on ABCam." /></a><figcaption>We can compare anything from locations to luggage to chemicals. Point in case: <a href="https://www.abcam.com/nav/proteins-and-peptides">Abcam.com</a>, a supplier of protein research tools to life scientists. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1cfcf3a-760d-418e-81c6-3550b96a94a6/chemicals-large-opt.png">Large preview</a>)</figcaption></figure>

The latter can apply to very different settings: We could be comparing locations, venues, glasses, cars, luggage, watches, TV sets or even [chemicals](https://www.abcam.com/nav/proteins-and-peptides). However, for the scope of this article, we'll be focusing on a very specific feature comparison among e-commerce retailers. The lessons we'll learn here can be applied to any kind of comparison context, although the fine details might vary.

One way or another, in the end, it all boils down to what kind of purchase the customer is about to make. As Joe Leech states in his [brilliant webinar on purchasing decisions](https://www.shopify.com/partners/blog/3-high-impact-tips-for-designing-an-ecommerce-site-that-converts), when shopping online, users have either a "non-considered" or a "considered" purchase in mind.

### Non-Considered Purchases

_Non-considered purchases_ are quick, low-effort purchases that we tend to make when we need a quick solution, or run errands. Whenever we need a pack of batteries, ordinary stationery, a "good-enough" dryer or a quick weekend getaway, what we're actually doing is checking a box off our to-do list and moving on. Few people get excited about selecting batteries or pencils, and so we are unlikely to explore different websites a few times just to buy that perfect pack. Instead, we tend to purchase such items quickly, often on the go, skimming over vendor reviews and shopping by price, shipping speed and convenience.

### Considered Purchases

_Considered purchases_, on the other hand, are slow, high-effort purchases, purchases that need time and consideration. When we buy a bicycle, a watch, a refrigerator or health insurance, we explore our options thoroughly, making sure we don't end up with something that isn't good enough or that doesn't fit or that would need to be replaced soon after. In such cases, we tend to keep exploring a possible purchase for quite a long time, often browsing many different retailers, comparing prices, reading reviews and examining pictures. We might even ask the opinion of our friends, colleagues and loved ones. Eventually, a final decision is made based on the expected quality and service, rather than convenience and speed, and it's not necessarily influenced by price point alone.

Of course, the more expensive an item, the more consideration it requires. But considered purchases aren't necessarily expensive: Any item with a certain attribute, such as longevity, speed or quality, has to be thoroughly considered as well. This includes gifts, flowers, wine and spirits, clothing, mortgages and health insurance. The reason for it is obvious: it's very hard to be very disappointed about a pack of batteries, but an uncomfortable gift, or wrong flowers sending a wrong message, or even an ill-fitting shirt that has to be returned, can be quite a frustrating experience.

<figure><a href="https://www.tvstore.nl/vergelijken/703168/705138"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1c11705-5ee7-4852-a0b4-17ce57f93d8e/feature-comparison-example-2-800w-opt.png" width="800" height="681" alt="TVStore.nl with a feature comparison table." /></a><figcaption>Considered purchases tend to be more complex and expensive. <a href="https://www.tvstore.nl/vergelijken/703168/705138">TVStore.nl</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7082e48-4873-4341-a1c0-b91d4f388f8c/feature-comparison-example-2-large-opt.png">Large preview</a>)</figcaption></figure>

Not many people know exactly what they want or need up front, unless they receive a trusted recommendation. So, every considered purchase requires a lot of thinking and consideration, comparing different options and filtering for that perfect one. The problem is that comparison isn't a particularly fun activity on the web. Details are often missing, prices are not transparent (how often do you add an item to the shopping cart and go through the entire checkout up to payment, only to see the real final price?) and model numbers (such as for appliances) are not consistent.

That's where a well-designed feature comparison can increase sales and improve user satisfaction. If we manage to pick up an indecisive customer in a moment of doubt — before they leave the website or start looking around — and guide them skillfully to a sound decision, then we are striving for a better customer experience, while also accounting for a larger profit and a more loyal customer base for the business. After all, customers don't have to shop around on other websites when purchasing (often) expensive items. That's something that might bear fruit for the business for years to come.

At this point, it's probably no big revelation that **feature comparison is relevant mostly for considered purchases**. They are particularly useful in cases where a product is relatively complex — potentially including details that might be confusing or ambiguous. Good examples of this are digital cameras and TVs — for an informed comparison of choices, one often needs an understanding of the technical capabilities of these devices. Another example would be a vacation or business trip — anything that requires many small decisions, such as availability, pricing, convenient departure and arrival times, budget, and a thorough planning of activities up front.

_What_ exactly makes a comparison relevant for the customer? Well, it's relevant if it helps users make a good, informed choice. A feature comparison could be designed to drive more customers towards "high-profit" margin sales, but if they aren't a good fit or if the customer feels they are overpaying, then the retailer will have to deal with either a high volume of returns or users abandoning them altogether in the long term.

When we observed and interviewed users to find out how a feature comparison might be relevant to them, we found that it essentially boils down to one single thing: seeing the difference between options, or filtering out unnecessary details quickly so that the differences become more obvious. Unfortunately (and surprisingly), many feature comparisons out there aren't particularly good at that.

{{% feature-panel %}}

## The Building Blocks Of Feature Comparison

If we wanted to compare two or more items against each other to find the better fit, what would be the most obvious way to do that? With clothes, we would try them on and pick the one that feels right. But what if trying things on isn't an option? When purchasing products online, we can rely on our past experiences, ratings, expert reviews, customer reviews and trustworthy recommendations to reduce the scope of options to just a few candidates.

Still, at some point, you might be left with a few too similar items — maybe one a bit too expensive, the other missing an important quality, and the third a recommendation from a friend's friend. So, what do you do? You list all options, examine their attributes side by side, and eliminate options until you have a winner. (Well, at least most people do that.)

Translated to common interface patterns, this naturally calls for a structured layout that aids in the quick scanning of options — probably a good ol' comparison _table_, with columns for products, and rows for their attributes. Once the user has selected products and prompted the comparison view, we can just extract all attributes from all selected products and list them as rows in the table. Should be easy enough, right? Yes, but that's not necessarily the best approach for meaningful comparison.

## Not All Attributes Are Created Equal

Ideally, we'd love to display **only meaningful, comparable attributes** that the customer cares about. Rather than extracting and lining up all product specs, we could determine and highlight all **relevant** product attributes, while keeping all other attributes accessible. This requires us to (1) find out what the user is interested in and (2) have consistent, well-structured data about our products.

While the first requirement is just a matter of framing the question properly in the UI, the second requirement is a tough nut to crack. In practice, having well-structured meta data often turns out to be remarkably difficult, not because of technical or design limitations, but because of content limitations.

Unless a retailer is using a specialized, actively maintained system that gathers, organizes and cleans up meta data about all products in their inventory, getting well-structured, complete and consistent attribute details — at least about products merely in the same category — turns out to be a major undertaking. You can surely manage meta data for a relative small clothing store, but if you as retailer rely on specs coming from third-party vendors, a meaningful comparison will require quite an effort.

<figure><a href="https://www.sharptvusa.com/compare/296,321"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f134dc09-c670-4a07-a7ed-ef874e02cb81/sharp-empty-data-800w-opt.png" width="800" height="524" alt="SharpTV feature comparison with a missing metadata." /></a><figcaption>Comparison is irrelevant if meta data is missing. Unfortunately, that's the case way too often. Case in point: <a href="https://www.sharptvusa.com/compare/296,321">Sharp TV</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3eef6ecb-b529-4b7d-b91b-8dfab0d79dcf/sharp-empty-data-large-opt.png">View large version</a>)</figcaption></figure>

## Houston, We've Got A (Content) Problem

This raises a question: How would you display a comparison table for two digital cameras if critical attributes were missing in one of them? In that case, meaningful comparison would be impossible, making it also impossible for the customer to make an informed decision. When faced with such a situation, rather than picking one of the options blindly, most customers will abandon the purchase altogether, because the worry about purchasing a wrong product outweighs the desire for a product at all.

[Conrad](https://www.conrad.com/ce/en/CatalogProductsCompare.html) lists all products in a table, with every other row alternating in background color. Like in many other retail stores, meta data is often incomplete and inconsistent, leaving users in the dark. In the example above, the number of HDMI inputs, the weight, the highlights and player dimensions aren't available for two of the three compared products.

<figure><a href="https://www.conrad.com/ce/en/CatalogProductsCompare.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b06a19d-642d-41e8-ba83-97b780744ab5/conrad-comparison-table-800w-opt.png" width="800" height="630" alt="Conrad feature comparison with missing meta data." /></a><figcaption><a href="https://www.conrad.com/ce/en/CatalogProductsCompare.html">Conrad</a> feature comparison with missing meta data. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/25e4e0af-d356-4b30-b58e-7d9dcae58bf4/conrad-comparison-table-large-opt.png">View large version</a>)</figcaption></figure>

The same happens when items are difficult to compare — for instance when **noisy ill-formatted data** appears next to well-structured data for many attributes. It might be possible to spot the differences between products with enough time investment, but it requires just too much work. In usability sessions, you can see this pattern manifest itself when customers prompt for a comparison view and scan the rows for a second or two, only to abandon the page a few seconds later. Moreover, once they've had this experience on the website, they will perceive the feature comparison on the website to be "broken" in general and ignore it altogether in future sessions.

{{< vimeo id="228784455" caption="When attributes are inconsistent, feature comparison becomes irrelevant. On <a href='https://www.hotpoint.co.uk/webapp/wcs/stores/servlet/CompareProductsDisplay?catalogId=10585&langId=-11&storeId=10236&catentryId=7211214&catentryId=7211208&catentryId=7211210'>Hotpoint</a>, attributes are missing. It's also impossible to remove an item from the selection, and on mobile, the third compared item is just dropped." >}}

So, what do we do if some information is missing, incomplete or inconsistent? Rather than display the comparison table as is, it would be better to inform the user that comparison isn't possible because some data about a particular product is missing, and then guide them to relevant pages (perhaps standalone reviews of the compared products) or ask them questions about attributes that are relevant to them, and suggest the "best" option instead.

## Those Attributes Aren't The End Of The World

Comparing by attributes matters, but extracting and reorganizing data from a specification sheet alone might not be particularly useful for a not-so-savvy customer. In fact, it might be helpful to extend or even replace some attributes with data that the user would find more understandable — for example, replacing technical jargon with practical examples from the user's daily routine? Or extracting advantages and disadvantages of products?

As [noted by Nielsen Norman Group](https://www.nngroup.com/articles/comparison-tables/), on Amazon, technical details aren't displayed as is. Instead, the comparison table translates technical attributes into language that is understandable by the average consumer. **Interface copy matters**: this goes for attributes as much as for wording on buttons, labels and thumbnails.

<figure><a href="https://www.amazon.com/Anker-PowerCore-Lipstick-Sized-Generation-Batteries/dp/B005X1Y7I2"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e578d2a8-51bd-45e0-bfec-2c5de7e3cf76/amazon-anker-comparison-800w-opt.png" width="800" height="602" alt="For its feature comparison, Amazon translates technical attributes into more understandable terms." /></a><figcaption><a href="https://www.amazon.com/Anker-PowerCore-Lipstick-Sized-Generation-Batteries/dp/B005X1Y7I2">Amazon</a> translates technical attributes into more understandable terms. For example, "# of iPhone 6s charges" or "# of Samsung S6 charges" (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03b2ea5b-eb83-41a2-b245-e2193c7d71e6/amazon-anker-comparison-large-opt.png">View large version</a>)</figcaption></figure>

For every two compared items, [Imaging Resource](https://www.imaging-resource.com) extracts the advantages and disadvantages of the products, as well as the respective strengths and weaknesses, in a list. This might not be the fastest way to compare attributes, but it nicely separates qualities by default, prominently highlighting critical differences between options. The website also provides extracts from reviews and suggests other relevant comparisons.

<figure><a href="https://www.imaging-resource.com/cameras/canon/t6i/vs/nikon/d3400/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe87b541-55e8-41ce-b703-5ffdb8e94d30/imaging-resource-comparison-800w-opt.png" width="800" height="592" alt="Professional digital camera feature comparison on Imaging-Resource" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea5c586a-8128-4274-87aa-1e80da216d1b/imaging-resource-comparison-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://www.imaging-resource.com/cameras/canon/t6i/vs/nikon/d3400/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1038c819-0cc6-4949-9fad-a413222e3602/imaging-resource-comparison-2-800w-opt.png" width="800" height="483" alt="Professional digital camera feature comparison on Imaging-Resource, secondary view" /></a><figcaption><a href="https://www.imaging-resource.com/cameras/canon/t6i/vs/nikon/d3400/">Imaging Resource</a> extracts the advantages and disadvantages of the products, as well as the respective strengths and weaknesses, in a list. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a208ee3f-3fce-4c98-8096-7bc3922b0de4/imaging-resource-comparison-2-large-opt.png">View large version</a>)</figcaption></figure>

[Versus](https://versus.com/en/sony-alpha-7r-vs-canon-eos-5d-mark-iii) goes one step further, highlighting how the features of the selected products compare against other products on average in a bar chart. Rather than only displaying all attributes as a table, they are also shown in a list view, with a detailed explanation of each attribute. Even better, the website puts every attribute into context by highlighting **how much better** the best product in that category is performing. The bonus is that members of the community can upvote every single attribute if they find it relevant. That's way more helpful for customers than single attribute values in a table.

<figure class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/228789451" width="640" height="421" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

<figcaption><a href="https://versus.com/en/sony-alpha-7r-vs-canon-eos-5d-mark-iii">Versus</a> highlights how the features of the selected products compare to other products on average in a bar chart.</figcaption></figure>

[Cool Blue](https://tvstore.nl/vergelijken/618863/728070/728077) has a fine feature comparison: Everything is just right. Not only does it display similar and different features prominently by default, it also highlights the pros and cons of each product and the pros and cons of each feature. The interface also granularly breaks down the rating for specific groups of features _and_ customer reviews.

{{< vimeo id="228781936" caption="<a href='https://tvstore.nl/vergelijken/618863/728070/728077'>Cool Blue</a> has a fine, well-designed feature comparison. Customer reviews and the pros and cons of each product make the comparison quite easy." >}}

[Flipkart](https://www.flipkart.com/home-kitchen/home-appliances/air-conditioners/pr?sid=j9e,abm,c54) provides feature comparison on most category pages and most product pages, with advantages, disadvantages and highlights extracted from reviews. That makes the feature comparison infinitely more relevant, and it might make it slightly easier to jump to a purchasing decision.

{{< vimeo id="228783554" caption="<a href='https://www.flipkart.com/home-kitchen/home-appliances/air-conditioners/pr?sid=j9e,abm,c54'>Flipkart</a> extract advantages and disadvantages of compared items from user reviews." >}}

More often than not, a detailed spec sheet alone might not be good enough for meaningful comparison. Extending the comparison with further details, such as relevant reviews, helpful rewording, as well as advantages and disadvantages in direct comparison can go a long way in helping the customer make that tough decision.

## Cleaning Up The Mess By Grouping Attributes

All of the options above provide a quick, scannable view of advantages and disadvantages, but depending on the complexity of a product, you might end up with 70 to 80 attributes lined up in a list. Going through all of them to find the ones that a customer cares about most would require quite some work.

One way to improve the scannability of attributes would be by **grouping attributes in sections** and then showing and collapsing them upon a click or tap. That's where [accordion guidelines](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/) come into play: In too many intefaces only icon acts as a toggle; of course, the entire bar should open or collapse the group of attributes. Additionally, an autocomplete search box or filter could allow customers to either jump to sections or to select and unselect categories for comparison.

Rather than just list all attributes, [Home Depot](https://www.homedepot.com/p/compare/?errorURL=ProductAttributeErrorView&langId=-1&storeId=10051&catalogId=10053&prodComp_0=207204027&prodComp_1=205594089&prodComp_2=301176928&N=5yc1vZc3oc) groups them into "Dimensions," "Details" and "Warranty / Certifications." It also highlights differences between products and has a fancy print view (accessible via a tiny print icon — let's see if you can find it!).

<figure><a href="https://www.homedepot.com/b/Appliances-Washers-Dryers-Washers-Top-Load-Washers/N-5yc1vZc3oc?catStyle=ShowProducts"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a37ceb1-5540-4a47-98db-aeae8df5b8e0/homedepot-comparison-table-800w-opt.png" width="800" height="526" alt="HomeDepot's feature comparison table, with grouped attributes." /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a36223ce-8c1d-494e-989c-e6d4b7cfdd13/homedepot-comparison-table-large-opt.png">View large version</a>)</figcaption></figure>

[Sharp](https://www.sharptvusa.com/compare/296,8,321) allows customers to select a category of interest from a list, or even to use autosuggest to quickly jump to a specific category. A checkbox on the right allows users to highlight the differences, too — although the highlight isn't always visually clear.

{{< vimeo id="228786884" caption="<a href='https://www.sharptvusa.com/compare/296,8,321'>Sharp</a> allows customers to select the category of interest from a list. That dropdown doesn't float, though." >}}

For its feature comparison, [Otto](https://www.otto.de/p/produktvergleich/softlayer/xRlnKDRS), a German retail store, not only groups all attributes but also turns each group into collapsible and extendable sections. Some sections additionally contain detailed information about an attribute, provided upon a tap or click.

{{< vimeo id="228786190" caption="<a href='https://www.otto.de/p/produktvergleich/softlayer/xRlnKDRS'>Otto</a> groups all attributes into collapsible and extendable sections." >}}

[Garmin](https://buy.garmin.com/en-US/US/catalog/product/compareResult.ep?compareProduct=552012&compareProduct=552032&compareProduct=552113) goes even further. Rather than just displaying a dropdown at the top of the page, it floats it alongside the products as the user scrolls the page. That's slightly better.

{{< vimeo id="228783561" caption="<a href='https://buy.garmin.com/en-US/US/catalog/product/compareResult.ep?compareProduct=552012&compareProduct=552032&compareProduct=552113'>Garmin</a> displays a dropdown with grouped attributes in the floating bar on the top." >}}

[Rtings.com](https://www.rtings.com/tv/reviews/best/by-features/hdr) extends a dropdown with filtering functionality for the entire table. If a customer is interested in a particular group of attributes, they can select the exact values that interest them. That's a level of granularity that a feature comparison table usually doesn't provide, and it's especially useful for lengthy comparison views.

{{< vimeo id="228786602" caption="<a href='https://www.rtings.com/tv/reviews/best/by-features/hdr'>Rtings.com</a> with filters applied to the entire table." >}}

Ultimately, a floating dropdown with a selection of the attribute section would be just enough for any comparison. In general, a slightly better organization of the attributes would help users navigate towards points of interest, but being able to easily see differences or similarities within those points of interest would also be useful.

## Highlight Differences Or Similarities… Or Both?

Because being able to easily see differences is one of the central purposes of a comparison, it makes sense to consider adding a toggle — like in Sharp's example above — to allow users to switch between seeing **only differences**, seeing only similarities and seeing all available attributes.

In fact, when users access a comparison table and notice the "show differences" button, they often first scroll down past the entire table just to see how time-consuming the comparison will be, only then returning back to that shiny button, pressing it and exploring the updated view.

In fact, that feature seems to be used quite heavily, and it's understandable why: Seeing the differences is exactly why customers actually prompt for a comparison view in the first place. That means that the option to highlight differences should be quite prominent. But then how exactly would you design it, and what options would you include, and what would the interaction look like?

On [MediaMarkt](https://www.mediamarkt.de/de/productcomparison.html), for example, customers can choose to see all attributes or only attributes by which products differ. The button for "showing only differences" is located in the left upper corner, next to product thumbnails. Keeping it closer to the table might make it more difficult to overlook it. The German retail store uses alternate background colors for product rows, but not for headings. Many products have 10 to 15 groups of attributes, and each of them can be shown and collapsed. Also, each product has a link to the full specification sheet.

{{< vimeo id="228785478" caption="On <a href='https://www.mediamarkt.de/de/productcomparison.html'>Mediamarkt</a>, a lightbox opens every time the user adds an item to the shopping cart. It might get annoying after the third click." >}}

The problem with highlighting differences is that it's enough for just one character in one table cell in the row to be slightly different, and the entire row will not disappear — even if all the other columns have the same, identical value. However, rather than just displaying the row as is, it would be infinitely more useful to actually **highlight** the difference — perhaps collapsing all "same" cells into one and highlighting that one cell that is different.

And then the question comes up: once "showing the differences" is selected, should identical attributes disappear altogether, or should they stay in the table with only different attributes being highlighted? It's probably a matter of personal preference. If there are 60–80 attributes to compare, we'd probably remove similar rows for easier scanning. If the table is smaller, removing rows might not be necessary.

[Electrolux](https://www.electrolux.lt/compare/?c=131220&query=232341&query=232332), for instance, contains a button in the left upper corner, acting as a toggle. The state is indicated with a checkmark which can be on or off. Rows with identical data aren't removed from the table — instead, differences are highlighted with a light blue background.

<figure><a href="https://www.electrolux.lt/compare/?c=131220&query=232341&query=232332"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/245a795c-89d2-438a-82e3-1c313f80697c/electrolux-show-the-differences-800w-opt.png" width="800" height="496" alt="Electrolux feature comparison" /></a><figcaption><a href="https://www.electrolux.lt/compare/?c=131220&query=232341&query=232332">Electrolux</a> highlights differences with a blue background without removing identical attributes. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/598ca821-6b36-4110-8fdb-8433f0e6bdeb/electrolux-show-the-differences-large-opt.png">Large preview</a>)</figcaption></figure>

{{< vimeo id="228785478" caption="On <a href='https://www.mediamarkt.de/de/productcomparison.html'>Mediamarkt</a>, a lightbox opens every time the user adds an item to the shopping cart. It might get annoying after the third click." >}}

[BestBuy](https://www.bestbuy.com/?intl=nosplash) contains a lot of exact numerical data, such as height "69.88 inches" and "69.9 inches". Most rows will never be omitted because of such minimal differences, making the comparison a bit more difficult.

{{< vimeo id="228781285" caption="<a href='https://www.bestbuy.com/?intl=nosplash'>BestBuy</a> with &ldquo;Show only differences&rdquo;. Grouping attributes and perhaps even repeating the button for every section would be helpful here." >}}

Seeing only differences is useful, but would users also benefit from seeing **only similarities**? In fact, providing this option is not very common, but there are some good use cases for it. As it turns out, one important scenario is when selected products have too many differences to scan through easily.

Here's an example. Let's imagine the customer has selected four digital cameras to compare, with each product having 60–80 attributes. Before embarking on a long journey through dozens of attributes, some customers will attempt to eliminate the options based on "simple" criteria, such as price or release date, "too weak" or "too expensive" or "not up to date" qualities. Obviously, while eliminating those items, they will want to make sure they aren't removing the wrong ones. In that particualr case, seeing similarities gives users validation that they are "still" looking at products that are "worth comparing" or "worth investing time into."

The main use case when it happens is when a customer is comparing a few strong, similar candidates. They might vary in a dozen attributes, yet the list of all 80 attributes is too lengthy to easily compare. With an option to see only similarities or only differences, the customer can break down the complexity into two parts. What you notice in such cases is that customers tend to take care of the "easier" task first: they will look into similarities first (just to be sure all options are "solid"), and then look specifically into the differences.

You might be wondering if it's necessary to provide the overview of all attributes? After all, the customers check both similarities and differences. The answer is "yes." Customers don't want to miss out on important details, and because they want to be certain about all available attributes, they will seek and examine the "all attributes" option as well, scanning it at least once during the session.

In terms of design, an obvious solution would be to use a group of mutually exclusive buttons or just one button or link that changes the contents and basically acts as a toggle.

[Samsung](https://samsung.com/us/televisions-home-theater/tvs/) allows customers not only to see all attributes, only similarities and only differences, but also to select what attributes are relevant and compare only by them, removing everything else. All attributes are grouped into accordions, which all can be expanded or collapsed with one click.

{{< vimeo id="228786878" caption="<a href='https://samsung.com/us/televisions-home-theater/tvs/'>Samsung</a> allows users to choose what items are relevant to them and compare only by them." >}}

[LG](https://www.lg.com/en/lgcompf4/compare/compare.lg?category=/de/monitore)'s interface is similar to [Samsung](https://samsung.com/us/televisions-home-theater/tvs/)'s, but the "compare" links are a bit too small, and because different views remain clickable all the time, it's not always clear what you are looking at. Also, I've still yet to figure out what "locking" an item above the product thumbnails in the comparison view means — it probably means displaying the item first.

{{< vimeo id="228785462" caption="On <a href='https://www.lg.com/en/lgcompf4/compare/compare.lg?category=/de/monitore'>LG</a>, customers can &ldquo;lock&rdquo; a product, but it's not very clear what that means." >}}

In practice, when encountering a feature to switch views, customers tend to alternate between all available options quite a lot. Seeing the differences and all attributes matters the most, but being able to see all similarities, while not necessary, might be reaffirming and supportive.

### Color-Coding For Easier Comparison

To highlight differences, we can remove similar or identical rows, but we could also use color-coding to indicate _how_ different the compared items are, and which of them performs better. An obvious way to do this would be to use some kind of colors or patterns on table cells. [Zipso](https://zipso.net/chromebook-specs-comparison-table/), for instance, colors fragments of each row for each selected attribute. While it's helpful for a few attributes, when many of them are selected, the presentation quickly becomes too difficult to compare.

<figure><a href="https://zipso.net/chromebook-specs-comparison-table/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b254de-d0fd-447e-8f55-724dbdcc74fc/zipso-comparison-table-800w-opt.png" width="800" height="501" alt="Zipso feature comparison" /></a><figcaption>Admittedly, not a feature comparison table, but rather a <a href="https://zipso.net/chromebook-specs-comparison-table/">performance benchmark table</a>. Still, highlighting rows can quickly become too noisy. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cacb8894-85f8-412e-a01c-2d9739466c88/zipso-comparison-table-large-opt.png">View large version</a>, <a href="https://player.vimeo.com/video/228789481">view HD video</a>)</figcaption></figure>

[Prisjakt](https://www.prisjakt.nu/produkt.php?j=2742665,794765,3015293,2859640) uses color-coding of table cells to highlight differences by default. Also, customers can highlight relevant rows by tapping or clicking on them (although, on tap, the differences aren't clear visually any longer). Every comparison also has a unique, shareable URL.

<figure><a href="https://www.prisjakt.nu/produkt.php?j=2742665,794765,3015293,2859640"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9042825b-8911-459c-a7f1-3415c8e570ff/prisjakt-comparison-800w-opt.png" width="800" height="493" alt="Prisjakt feature comparison, with color coding highlighting differences." /></a><figcaption><a href="https://www.prisjakt.nu/produkt.php?j=2742665,794765,3015293,2859640">Prisjakt</a> uses color coding to highlight relevant differences. <a href="https://player.vimeo.com/video/228786207">View video in HD</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff0a9c60-47ee-4c9c-ace5-ae34a0e3c6e8/prisjakt-comparison-large-opt.png">Large preview</a>)</figcaption></figure>

[ProductChart](https://www.productchart.com/3d_printers/14395_vs_5951) uses background bars to indicate which of the candidates performs better for a certain attribute. The length of the bar indicate how much better one of the options performs. Slightly highlighting the winner, or providing an overall score and suggesting a winner, might be helpful here.

<figure><a href="https://www.productchart.com/3d_printers/14395_vs_5951"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/304c2cf5-0bf2-4ff9-a4c0-561d3cb11438/productchart-visual-comparison-800w-opt.png" width="800" height="660" alt="A visual feature comparison on ProductChart." /></a><figcaption><a href="https://www.productchart.com/3d_printers/14395_vs_5951">ProductChart</a> highlights differences using background bars. (See <a href="https://player.vimeo.com/video/228786240">video</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5bccd2ea-ce27-47a8-babe-cf7858bc6a25/productchart-visual-comparison-large-opt.png">View large version</a>, <a href="https://player.vimeo.com/video/228786240">View video in HD</a>)</figcaption></figure>

[Digital Camera Database](https://www.digicamdb.com/compare/leica_tl2-vs-canon_eos-m6/) displays the differences between products with filled colored rectangles, to indicate the dimensions of difference. That's useful for highly technical and detailed comparisons, but not necessarily so for every kind of feature comparison.

<figure><a href="https://www.digicamdb.com/compare/leica_tl2-vs-canon_eos-m6/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5d62a47-aae8-497b-a82d-2e4fccd12dda/digicamdb-comparison-800w-opt.png" width="800" height="420" alt="Highlighting how much better one product is against another." /></a><figcaption>For every group of products, <a href="https://www.digicamdb.com/compare/leica_tl2-vs-canon_eos-m6/">Digita Camera Database</a> visually highlights how much better one of the candidates is. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e8c4119-04b6-4785-908e-bdf9bc425464/digicamdb-comparison-large-opt.png">View large version</a>)</figcaption></figure>

If your feature comparison table is likely to contain a lot of numerical data, it might be useful to highlight both the row and the column upon a tap or click, so that the user always knows they are looking at the right data point.

Color-coding is a simple way to highlight differences, but we also need to provide an accessible alternative, perhaps elaborating on the difference between products in a summary above the table.

{{% ad-panel-leaderboard %}}

## The Thing That Never Goes Away: Floating Header

You've probably been in this situation before. If you have three obscurely labelled products to compare, with over 50 attributes being compared _against_, you might have a very difficult time remembering exactly which product a column represents. To double-check, you'll need to scroll all the way back up to the headings, and then scroll back all the way down to continue exploring the attributes.

{{< vimeo id="228781411" caption="With many attributes displayed, users might need to jump back and forth in the table as they you can't see what products they are comparing. <a href='https://www.bol.com/nl/index.html'>Bol.com comparison</a>." >}}

One obvious way to make mapping less strained is by having **sticky column headers**, following the customer as they scroll down the comparison table. We don't necessarily need to keep all of the details in the header, but providing a product model's name, with its rating and a small thumbnail might be good enough.

[Sony](https://www.sony.com/electronics/lenses/t/camera-lenses?cameramount=a-mount&type=prime-lenses&view=compare) keeps product labels and thumbnails floating above the comparison table as the user compares products. This gives customers a very clear mapping between attributes and a product. To compare, a quick look at the header is enough — no extra scrolling necessary!

{{< vimeo id="228786910" caption="<a href='https://www.sony.com/electronics/lenses/t/camera-lenses?cameramount=a-mount&type=prime-lenses&view=compare'>Sony</a> keeps product labels and thumbnails floating above the comparison table." >}}

[Indesit](https://www.indesit.co.uk/Products/Laundry/Washing-Machines) solves the same problem in a slightly different way. The interface keeps thumbnails in a floating bar at the _bottom_ of the screen, rather than at the top. As the items are added, they are displayed in the bar at the bottom. To add the items though users need to hit the comparison icon tucked in the upper-right corner of the product — it might not be easy to identify. Ah, also the entire "Compare models" bar should act as a toggle — in the implementation, only the chevron icon triggers expansion and collapsing.

{{< vimeo id="228784501" caption="<a href='https://www.indesit.co.uk/Products/Laundry/Washing-Machines'>Indesit</a> uses a floating bottom bar to keep the mapping between the column and the product." >}}

So, if a floating bar is in use, should it float _above_ or _below_ the table — or does it even matter? Keeping headings above the content seems slightly more natural, especially when the thumb is hovering over the contents of the comparison view on narrow screens. Users need to be more careful when scrolling the page on narrow screens — which is why the bar in the Indesit example disappears entirely on mobile. Keeping the bar above the table just seems a bit more reliable.

Obviously, it's going to be very difficult to display all selected products as columns at all times. A table view works well if you have two to three products to compare, but probably not so well if there are five products in the table. In that case, a common way to conduct the comparison would be by sliding horizontally.

## Growing And Shrinking Those Tables

No conversation about tables can omit a close look into their responsive behavior across screens. A discussion of tables deserves a separate post, but there are a few common tricks to keep a table meaningful on narrow screens. Quite often, each table row will become a collapsed card, or headings will jump all over the place, or the table will be restructured to expose the data better, or the user can select which columns they want to see.

Problem solved? Not so fast. The feature comparison table is a beast of a special kind. The main purpose of the element is comparison: Keeping both attribute headings and product headings visible is important — after all, the customer wants to see the products they are comparing _and_ the features they are comparing against. This means that for easy comparison on narrow screens, we need to float product headings, while keeping the attribute column locked as the user scrolls down the page. That doesn't leave us with a lot of space to display actual product details.

Sadly, almost every other retail website makes feature comparison unavailable on narrow screens. Selected products will often disappear altogether, the comparison feature will be hidden, and loading a shared comparison link will appear to broken. In fact, it proved to be quite a challenge to find even a handful of examples out there.

Some interfaces try to make the best of what they have. [Crutchfield](https://www.crutchfield.com/Product/CompareTo.aspx?g=347650&compareItems=01|30519F4000&compareItems=01|30532J5205&compareItems=01|15832W600D&compareItems=01|30540M7000)'s interface, for example, is responsive, but that doesn't mean it's useful. On narrow views, items are displayed in a 2 × 2 grid, and so are product attributes. Because there is no visual relation to the actual product, it makes it very difficult to compare features.

{{< vimeo id="228781978" caption="<a href='https://www.crutchfield.com/Product/CompareTo.aspx?g=347650&compareItems=01|30519F4000&compareItems=01|30532J5205&compareItems=01|15832W600D&compareItems=01|30540M7000'>Crutchfield</a> displays products and features in 2 &#215; 2 grid &mdash; not very intuitive." >}}

[ProductReportCard](https://www.productreportcard.com/Best-Refrigerator-Reviews/Compare/13254-13255-13256) displays products in sets of three at a time. The attributes of each products are squeezed into a 33% column on narrow screens, making reading quite tiring, and comparison quite difficult.

{{< vimeo id="228786273" caption="Even if the meta data is present but the content isn't well organized for easy scanning, comparison will be quite difficult. Extracting pros and cons is noteworthy though. (Source: <a href='https://www.productreportcard.com/Best-Refrigerator-Reviews/Compare/13254-13255-13256'>ProductReportCard</a>)" >}}

[Urban Ladder](https://www.urbanladder.com/) allows its customers to shortlist and compare items in the product grid. Once the user hits the "Compare" button, they're presnted with a quick overview of similar products which are auto-suggested. On narrow screens, users can compare only two items at a time.

{{< vimeo id="229535034" caption="<a href='https://www.urbanladder.com/'>Urban Ladder</a> allows its customers to compare at most 2 items at a time." >}}

One way to manage this problem would be to avoid a table view altogether. Instead, we could **highlight similarities and differences in a list by default**, allowing customers to switch between these views.

Alternatively, we could ask the user to choose the attributes that they care about most, and once the input is done, we could highlight relevant features, and perhaps even pull some data from reviews, displaying both of them in a list. Every relevant attribute row could become an expanded card, while all less relevant attributes could be displayed as collapsed cards below.

As always, limited space requires a more focused view and since differences are usually what matter the most, highlighting them and removing everything else seems quite reasonable.

Admittedly, with all of these options, we are losing the big-picture view that a table can provide. If you'd like to keep a table, usually you'll have at most one column to fill in with actual content — as another column has to be reserved for attribute headings. To make it work, you could provide a stepper navigation between products, so that the user is able to switch between products predictably. In the same way, sometimes floating arrows are used left and right, similar to a slider.

[OBI](https://www.obi.de/compare) allows customers to add as many products as they wish for comparison. In a comparison view, the navigation between products in the table happens via a stepper in the left upper corner. Unfortunately, the feature comparison isn't available on narrow views.

{{< vimeo id="228785494" caption="<a href='https://www.obi.de/compare'>OBI</a> with a stepper, allowing to switch between options predictably." >}}

Alternatively, you could also extend the table with a segmented control or multi-combination selector at the top, allowing users to choose two or more products out of the product comparison list — and display them side by side. With two products, the user would end up with a beautifully readable, responsive comparison table, and with more selected items, they would get either a scrollable area or a summary of differences and similarities. The user could then choose what they'd rather see.

{{< vimeo id="229537556" caption="One strategy for making comparison tables work on mobile is converting the columns to tabs. This means users can't do true side by side comparison like they can on a full table, but at least they will be able to switch between products more easily than if they had to scroll or switch between mobile browser tabs." >}}

What to choose then? If the feature comparison table contains mostly numerical data, then it might be easier just to **explain differences** in products up front. If that's not the case or if the contents of the table is unpredictable, an option with **stepper navigation**, or a multi-combination selector, might work well. And if the product is complex and so attribute descriptions would be numerous and lengthy, then **extracting relevant data** and highlighting it, rather than sending the user on a journey through dozens of attributes, might be a better option.

<figure><a href="https://www.smashingmagazine.com/2015/08/responsive-upscaling-large-screen-e-commerce-design/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7613805e-05c1-436d-b9b2-0871cdeded44/11-recently-viewed-items-opt-small.jpg" alt="Suggestions could be displayed as a separate pane, floating on the right." /></a><figcaption>Product suggestions, a list of recently viewed items or a feature comparison view may be placed in a sidebar for easy cross-product navigation. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7613805e-05c1-436d-b9b2-0871cdeded44/11-recently-viewed-items-opt-small.jpg">View large version</a>)</figcaption></figure>

When talking about responsive behavior of components, we tend to focus on "regular" and "narrow" screens, but we could be exploring adjustments for "wide" screens as well. If we do have enough space to display a feature comparison prominently on wide screens, why not make the best use of it? As the user navigates the category page, for example, we could display the feature comparison as a floating pane on the right, while the left area could be dedicated to products highlighted in that category. As the customer adds an item for comparison, it could appear in the side-by-side comparison right away. In his article on "[Responsive Upscaling](https://www.smashingmagazine.com/2015/08/responsive-upscaling-large-screen-e-commerce-design/)," Christian Holst mentions a good number of techniques applicable to e-commerce UX on large screens. They can be quite relevant for feature comparison as well.

## Moving Things Around Until They Stick

What exactly happens before the comparison table appears? The customer will probably land on a category page, selecting a few items to compare, only to discover a button to prompt for the comparison. At this point, the customer might (or might not) know details about some of the selected items. In the same way, the order of selection for comparison might (or might not) be random. When displaying comparison results, a safe bet then is to display columns in the order of selection, because any different order might cause confusion.

As they are in the process of comparing, the customer will (hopefully) start to see things a bit more clearly, filtering out products that are clearly outperformed by selected competitors. To clear up the comparison view, we will allow the customer to remove a product from the comparison, of course, often indicated with an "x" in the upper-right corner of the column (or the floating header).

As it turns out, sometimes users will quickly dismiss one of the options, for example because it's too expensive anyway, but they would want to keep that option in the comparison view for reference — just to put other candidates in context. That "reference" option might end up being stuck in the middle of the table, getting in the way of the comparison between two or more "real" candidates.

Obviously, the best arrangement for these options would be to display the main candidates first, side by side, followed by the "reference" candidates. In fact, you could even go as far as to allow the customer to downgrade or downvote some candidates and push them a bit to the side, displayed in a less prominent gray color.

A slightly more robust option would be to allow users to drag columns as they wish. That would help in the beginning when the customer has added quite a few items to the list but then, for instance, realized that the price difference was too high and so wanted to rearrange the products. It would also help in the case with "reference" candidates. In fact, in interviews, users sometimes compared product columns with cards or brochures or sticky notes that they could move around to group important ones against less important ones. A digital equivalent of the same experience in a feature comparison table would be draggable columns.

On [Digital Photography Review](https://www.dpreview.com/products/compare/side-by-side?products=canon_eos100d&products=canon_eos650d&products=canon_eos800d), for example, users can move selected items left and right. That's a nice accessible alternative to drag-and-drop.

{{< vimeo id="229535569" caption="Users can move columns left and right as they wish on <a href='https://www.dpreview.com/products/compare/side-by-side?products=canon_eos100d&amp;products=canon_eos650d&amp;products=canon_eos800d'>Digital Photography Review</a>." >}}

The nature of [SocialCompare](https://socialcompare.com/en/comparison/apple-iphone-product-line-comparison) requires users to be able to drag columns and rows as they wish. However, moving columns around like cards might be helpful for customers of retail websites as well.

{{< vimeo id="228786897" caption="Draggable columns on <a href='https://socialcompare.com/en/comparison/apple-iphone-product-line-comparison'>SocialCompare</a>." >}}

It's important to note that drag-and-drop is (obviously) not accessible, so screen reader users would need to have access to navigation within the column headings. For example, you could have a `select` dropdown or a group of radio buttons as a fallback in that case.

But what if, after a detailed comparison, a customer is dissatisfied with all the options presented in the comparison view? In addition to being able to remove items from the list, it's important to be able to **add relevant items to the comparison view** — and "relevant" is important here. In most cases, the "add" button will simply return customers to the category page, where they would be asked to add more items for comparison. Instead, we could suggest products that are likely to fit the bill, perhaps by showing ones similar to the items selected.

<p>On <a href="https://www.carshowroom.com.au/compare-cars?count=3&amp;id=AA000G9YK0,AA000G9YN0,AA000G9Y14">Car Showroom</a>, customers can add new items by typing in the model reference and using autosuggest. Also notice that the interface provides navigation within the comparison &mdash; comfortable for quick jumps to relevant features.

{{< vimeo id="228781552" caption="<a href='https://www.carshowroom.com.au/compare-cars?count=3&amp;id=AA000G9YK0,AA000G9YN0,AA000G9Y14'>Car Showroom</a> with a &ldquo;Quick Add&rdquo; feature and autosuggest." >}}

## Second Opinions Matter, As Do Shareable URLs

<p>Because feature comparison is relevant mostly for purchases that take time, the more important the purchase, the more likely the customer is to explore the idea of buying an item over a long period of time. One thing we've noticed by observing shoppers is that, every now and again, in a moment of doubt, they will take a screenshot (or a series of screenshots) of the comparison table, and store it "for future reference," until they've made a decision. Well, that's not the full truth because one of the main reasons for storing that screenshot is to send it over to friends and colleagues who have a better understanding of technical details and to ask for their second opinion.

{{< vimeo id="228781798" caption="<a href='https://www.conrad.com/ce/en/CatalogProductsCompare.html'>Conrad</a> makes it possible for customers to save comparisons for future reference." >}}

Indeed, second opinions matter for many people &mdash; even from a close friend who isn't that knowledgeable in whatever category the product belongs to. That precious screenshot will end up wandering through Facebook chats and Skype chats, email attachments and WhatsApp groups. If your data tells you that many of your customers need a second opinion before purchasing items (and that will surely be the case for electronics or appliances), make it possible to "<strong>save the comparison for later or share it</strong>," enhanced with friendly and encouraging copy. This means that the every comparison should have a unique URL, featuring all or selected attributes, the expanded and collapsed groups of attributes and the order of products.

## Don't Lose That Selection

<p>It's no secret that many customers misuse their shopping cart or wish lists to keep a selection of products intact for when they visit the website next time (often shortly afterwards). In the same way, storing the comparison table persistently (perhaps in localStorage or in a Service Worker) for some time is a good idea. In fact, no customer would be pleased if compared products were to disappear after they accidentally closed the tab.

<p>Eventually, once the user visits the page a few days (or weeks) later, you could open a little message bar stating that their recently viewed items and compared items are still available, with an option to "dismiss" it. Should the user choose to explore that comparison, they could do it from the message bar. Should they browse a category and choose other products for comparison, obviously the comparison view should be overwritten with the newly selected products.

## Those Tiny Interaction Details

<p>Interaction with a feature comparison table might appear to be quite self-explanatory, but many tiny decisions have to be made before the user even gets to see the comparison.

### Where Should Comparison Be Possible?

<p>For one, the comparison feature obviously has to be indicated, promoted or featured somehow &mdash; but where exactly? There are many options. It could appear on the home page, in the category list or on the product page. It could also be available on the shopping cart page or on search results pages. On most e-commerce websites, the option to compare is visible only on the category page, often for the obvious reason of not distracting the customer from the purchasing funnel. Is it always the best solution, though?

<p>Well, we should ask ourselves first, when would a customer <em>want</em> to compare items in the first place? One common use case is when they are looking at similar options but can't decide which one to choose. This usually isn't the case on the home page (too early) or on the shopping cart page (too late), but it definitely is the case on a category page and (often) on the product page.

<p>On top of that, one can spot an interesting behavioral pattern when observing customers navigate category pages. When exploring options for purchase, a good number of users will open every potential product candidate in a separate tab and examine each thoroughly one by one first, closing tabs only if the candidate is clearly not good enough. Now, these customers might find a strong candidate and head straight to the checkout, or (more commonly) they might lean towards a few options.

<p>In the latter case, being able to add items for comparison on a product page would obviously save those annoying roundtrips between product pages and category pages. However, we would save not just clicks or taps &mdash; more importantly, we would avoid deadlocks, those situations where a customer is indecisive and can't proceed to check out, abandoning the purchase altogether. If the customer is undecided about the options, they will definitely end up not checking out; and if they do, you can expect the risk of high refund costs. In a way, feature comparison is an easy, helpful way to keep customers on the website by helping them making the right decision.

<p>Another common use case is when a customer comes to a website with strong options in mind already but is looking for more detailed specifics of each option. In that situation, the customer is likely to search for these products right in the search field, often typing in obscure model numbers that they wrote down in a physical retail store. If the appliance can't be found using search, some customers will still try to find it on the category page, but if their first attempts don't bring the expected results, they will abandon the website altogether. Similar to the previous case, here we can guide potential customers by suggesting the products they might have meant and making it easier for them to make a decision. Perhaps we could even provide more competitive price and delivery options than a physical store can. Again, adding the comparison selection right in the search results might be a good option to consider as well.

<p>There is another option, though. We could also highlight feature comparison as part of the global navigation. If you have a very limited range of products, each of them targeting a specific audience, it might be useful to clearly communicate what groups of customers each product is designed for.

<p>For example, <a href="https://www.biz.konicaminolta.com/products/index.html">Konica Minolta</a> provides a separate feature comparison link in the main navigation. Unfortunately, it's nothing but a list of all specifications for all products in a side-by-side view. Perhaps explaining the advantages of each product and whom it's best for would be more helpful. Still, customers can export and print out results for easy scanning and reading.

{{< vimeo id="228785450" caption="<a href='https://www.biz.konicaminolta.com/products/index.html'>Konica Minolta</a> uses a guide rather than a comparison table to help users make the right choice.]" >}}

<a href="https://www.vizio.com/tv-comparison">Vizio</a> prominently integrates feature comparison in the main navigation. All products can be chosen for comparison, but every navigation section also contains a "Compare Sizes / Models" link, which features the entire spectrum of products, all broken down into groups, with filters for choosing the relevant ones. The attributes are broken down in groups, too, and displayed as accordions in a tabular view, while the products always remain visible in a floating bar.

{{< vimeo id="228789460" caption="Navigation between products on <a href='https://www.vizio.com/tv-comparison'>Vizio</a> happens by sliding left and right. Attribute headings remain fixed." >}}

Quite surprisingly, <a href="https://www.amazon.com/s/?fst=as%3Aoff&amp;rh=n%3A172282%2Cn%3A!493964%2Cn%3A502394%2Cn%3A281052%2Cn%3A12556502011%2Cp_6%3AATVPDKIKX0DER%2Cp_72%3A1248879011&amp;bbn=12556502011&amp;ie=UTF8&amp;qid=1485934762&amp;rnid=1248877011&amp;ajr=2">Amazon</a> doesn't display feature comparison as an option on the category page. In fact, it is quite difficult to notice on the product page as well. But rather than allowing customers to select the products they'd like to compare, Amazon allows them to only "Compare with similar products." Only six attributes are displayed on mobile by default: the product's title and its thumbnail, the customer rating, the price, shipping info and the retailer. The attributes are disclosed progressively, upon a tap or click.

<figure><a href="https://www.amazon.com/Leica-Megapixel-Digital-3-0-Inch-18471/dp/B00NNVC1MS/"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78eab9c9-7987-4fbf-add5-e13918b86598/amazon-comparison-800w-opt.png" width="800" height="514" alt="Amazon's feature comparison" /></a><figcaption><a href="https://www.amazon.com/Leica-Megapixel-Digital-3-0-Inch-18471/dp/B00NNVC1MS/">Amazon</a> doesn't provide feature comparison as an option on category pages — instead, it displays similar items on the product page by default. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b36e2409-61e5-4d2d-9826-78f10f6ee9d4/amazon-comparison-large-opt.png">View large version</a>)</figcaption></figure>

Don't get me wrong: of course the main goal of the website isn't to bring as many people as possible to a comparison view, but rather to bring them to the checkout &mdash; with an item that will actually meet their needs. Because a comparison can help avoid deadlock, try enabling "adding to comparison" for product pages, category pages and search results, and then monitor conversion. If you have just a few products in the inventory, clearly labelling and targeting each group of customers might be a better (and simpler) option.

### The Life Of A Lonely Checkbox, Or How To Indicate Comparison

<p>Once we know which pages a feature comparison will appear on, we should ask ourselves how users will actually <em>add</em> items for comparison. This requires us to look very closely into the microscopic details of how the feature is indicated and how the user would interact with it.

<p>While some designers choose to use a link or button with a label (for example, "Add to compare"), others use iconography (a plus sign or a custom "compare" icon) to indicate comparison. A more common option, though, seems to be a good ol' <strong>checkbox with a label</strong>. A checkbox naturally communicates <em>that</em> and <em>how</em> an item can be selected and unselected, and with a proper label in place, it conveys the functionality unambiguously.

<figure><a href="https://www.tvstore.nl/category/192945/televisies.html?9155=24068"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ed55e76b-c1f1-4d49-b881-356a254c5c5e/tvstore-nl-800w-opt.png" width="800" height="858" alt="TVStore's feature comparison." /></a><figcaption>Can you spot the lonely checkbox on <a href="https://www.tvstore.nl/category/192945/televisies.html?9155=24068">Tvstore.nl</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72bee0bd-09b1-41cf-8728-9475d24282ff/tvstore-nl-large-opt.png">Large preview</a>)</figcaption></figure>

Now, where would you <strong>place that checkbox</strong>, you might ask? Frankly, if you look around e-commerce websites, you'll find it pretty much everywhere &mdash; sometimes residing on top above headings, sometimes below thumbnails, sometimes in the bottom-right corner next to reviews, and quite often just above the price, where it's difficult to miss. Admittedly, we couldn't spot any significant difference; however, one thing was noticeable: The options with a checkbox seemed to consistently make feature comparison slightly more obvious and easy to find than plain text links.

<figure><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a8424a7-61d4-4e6f-843a-fe408660367a/bol-comparison-800w-opt.png" width="800" height="504" alt="Bol.com feature comparison" /></a><figcaption>A usual suspect: the "compare" button appearing under the product thumbnail. Image credit: Bol.com</a>. (<a href="https://www.smashingmagazine.com/wp-content/uploads/2017/08/bol-comparison-large-ot.png">Large preview</a>)
</figcaption></figure>

Once the user has selected an item for comparison, it's important to <strong>confirm the selection</strong> &mdash; a checkbox does a good job of that, but we could also change the wording (for example, from "Add to compare" to "Remove from comparison") or change the background color (slightly highlighted) or fade in a label or a flag ("Shortlisted") or a popover. We also have to indicate the change of state for screen readers.

<p>Every selection should be easy to unselect with one tap as well, without resetting the entire selection. Unfortunately, the latter isn't that uncommon, as some websites choose to disable the checkbox to prevent double-selection, effectively making it impossible to remove the product from comparison without prompting a comparison view.

<figure><a href="https://products.geappliances.com/appliance/gea-category/refrigerators?TYPE=Side-by-Side"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd4adce6-b98e-4e4a-b391-762153c58c53/ge-appliances-800w-opt.png" width="800" height="634" alt="GE's feature comparison" /></a><figcaption>A humble checkbox label turning into a large blue button on <a href="https://products.geappliances.com/appliance/gea-category/refrigerators?TYPE=Side-by-Side">GE Appliances</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/355a0551-1206-4d19-889e-49a9c166ee0b/ge-appliances-large-opt.png">Large preview</a>)</figcaption></figure>

Obviously, we also need to place a "compare" button somewhere, so that customers can easily proceed over to the comparison view. Now, that view wouldn't make sense if there is no or only one item shortlisted for comparison. So, rather than displaying a disabled, grayed-out "comparison" button when there aren't enough items to compare, we could display it only if there are at least two items in the list &mdash; perhaps inlined next to those "Add to compare" checkboxes or links of all of the candidates that the customer has selected.

<p><a href="https://www.sony.com/electronics/lenses/t/camera-lenses?cameramount=a-mount&amp;type=prime-lenses">Sony</a>, for example, uses the text label "Select to compare" for all products in a category first, and if one item is selected, it changes the checkbox label on that item to "Select two or more to compare." When one more item is added for comparison, the label changes to "Selected," with a "Compare now" link appearing inline on all selected products.

<figure><a href="https://www.sony.com/electronics/interchangeable-lens-camera-products/t/interchangeable-lens-cameras"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbd20794-aa69-47f6-8d82-f9a301c8037a/sony-comparison-800w.gif" width="800" height="548" alt="Sony.com feature comparison" /></a><figcaption>Micro-interactions for adding an item to the feature comparison, on <a href="https://www.sony.com/electronics/interchangeable-lens-camera-products/t/interchangeable-lens-cameras">Sony.com</a>, <a href="https://vimeo.com/229536660">watch video in HD</a></figcaption></figure>

In fact, in practice, that "fancy" comparison button is unlikely to be very fancy, otherwise it would fight for attention with the primary buttons, such as "Add to cart." Therefore, more often than not, it's a subtle tertiary button that doesn't fight for attention but is noticeable, close to the comparison checkboxes. Still, we could gently highlight it for a blink of a second with a subtle transition or animation once a new item has been added for comparison.

<p>Wait a second! You might be thinking: well, if the feature comparison is so important, why not display a confirmation in a lightbox, prompting the customer to choose to go straight to the comparison or to continue browsing on the website? Well, the problem with this option is that it <strong>massively interrupts the flow</strong>. Rather than keeping the focus on the products, it directs the customer's attention to a confirmation message that has to be responded to with every new added item.

<p>Of course, we don't know if the customer will add two or four or more items for comparison, but having to get rid of the lightbox to continue browsing products seems excessive and just plain unnecessary. With an <strong>inlined "comparison" button</strong>, we get the best of both options: Should the user want to continue browsing, they would do so seamlessly. Should they want to compare, they can compare easily as well. And the focus always stays on what matters the most: the products.

<p>However, it's not the best we can do. One issue we kept noticing in usability sessions is that as customers explore their options and add items for comparison, eventually they are ready to prompt the comparison view, but often can't find the button to prompt it. In fact, they end up having to refind the products they've selected because that's where "compare now" buttons are located. That's especially difficult in a paginated category with a long list of scattered products.

<p>We can solve this problem by displaying a <strong>semi-transparent comparison overlay</strong> at the bottom of the page. The overlay could appear when a customer adds the very first item for comparison and could fade away when the selection is cleared. By dedicating a portion of the screen to comparison, we regain just enough space to subtly confirm the user's actions and to inform them about their next steps, without interrupting the flow.

<p><a href="https://www.homedepot.com/b/Appliances-Washers-Dryers-Washers-Top-Load-Washers/N-5yc1vZc3oc?catStyle=ShowProducts">Home Depot</a> uses a 60px tall comparison overlay at the bottom to highlight thumbnails of the selected products. The overlay us used to guide users through the selection &mdash; for example, by explaining how many items are required for comparison. Customers don't have to search for the selected items on a category page, but they can unselect options right from the overlay. That's also where an omnipresent "Compare" button resides.

{{< vimeo id="228783578" caption="Comparison overlay on <a href='https://www.homedepot.com/b/Appliances-Washers-Dryers-Washers-Top-Load-Washers/N-5yc1vZc3oc?catStyle=ShowProducts'>Home Depot</a>. Notice how the &ldquo;Compare&rdquo; label on the checkbox changes to the &ldquo;Compare Now&rdquo; link when at least two items are shortlisted for comparison." >}}

<a href="https://www.electrolux.lt/compare/?c=131220&query=232341&query=232332">Electrolux</a> displays notifications about selected items in the 75px tall bottom bar. It might be a bit too subtle to understand quickly. Rather than changing the text for "showing the differences" or "displaying all attributes," it uses a pseudo-checkbox that users can toggle on and off.

{{< vimeo id="228783244" caption="<a href='https://www.electrolux.lt/compare/?c=131220&query=232341&query=232332'>Electrolux</a> with a humble subtle notification bar at the bottom of the screen." >}}

<a href="https://www.appliancesconnection.com/french-door-refrigerators.html">Appliances Connection</a> uses a slightly less subtle 40px tall bar at the bottom, with a clear link indicating comparison and access to recently viewed items. The comparison view is sliding from top to bottom, and users can switch to recently viewed items as well.

<p>The design of showing and hiding similar features is slightly off, tucked in the upper-right corner. Also, customers can add "Stock ID or SKU" for comparison &mdash; but not many customers will know what that means.

{{< vimeo id="228779669" caption="<a href='https://www.appliancesconnection.com/french-door-refrigerators.html'>Appliances Connection</a> gives users quick access to compared and recently viewed items with a bottom bar." >}}

<a href="https://www.abcam.com/products/compare?&productCode=ab7403&productCode=ab9794&productCode=ab50036&productCode=ab7456">Abcam</a> implements the bottom bar slightly differently, as an accordion with items lined up in a vertical list. Unfortunately, once the user is in the comparison mode, it's impossible to remove items or clear the selection.

{{< vimeo id="228779643" caption="<a href='https://www.abcam.com/products/compare?&productCode=ab7403&productCode=ab9794&produntctCode=ab50036&productCode=ab7456'>Abcam</a> uses a subtle animation to provide visual confirmation." >}}

<a href="https://www.deltafaucet.com/bathroom/sink?searchFilter=true">Delta</a> displays "Add to compare" only on hover, along with other important details, such as price. Unlike in previous examples, "Add to comparison" prompts an overlay at the top of the screen, where the customer can add more items for comparison.

{{< vimeo id="228782836" caption="<a href='https://www.deltafaucet.com/bathroom/sink?searchFilter=true'>Delta</a> with a large comparison overlay at the top of the screen." >}}

In fact, overlay seems to be a quite common solution, and in fact, it can be helpful in quite many ways. For instance, if only one item is shortlisted, we could use the space to suggest similar comparable items, or even items that other customers often check out as well ("Suggest similar or better options").

<p>We could also group similar items and complement a comparison list with a <strong>shortlisted selection of products</strong>. What's the difference? Instead of prompting the customer to pick one type of products, then select specific items of that type and compare them, we could enable customers to add products of different kinds, group them in the background and keep them accessible for any time later &mdash; not necessarily only for comparison. Think of it as a sort of extended list of favorites, or wishlist, with each selection getting a label and perhaps even a shareable URL.

<p><a href="https://www.dpreview.com/products/compare/side-by-side?products=canon_eos100d&amp;products=canon_eos650d&amp;products=canon_eos800d">Digital Photography Review</a> does just that. The user can "mark" any item for shortlist and then compare items in a particular category later. That's a good example of resilient, forgiving design: Even if a customer selects batteries and laptops for comparison, they would never appear in a side-by-side comparison because they would be grouped separately. Each item can be removed individually, or the customer can remove an entire group, too.

{{< vimeo id="228783235" caption="<a href='https://www.dpreview.com/products/compare/side-by-side?products=canon_eos100d&amp;products=canon_eos650d&amp;products=canon_eos800d'>Digital Photography Review</a> has a shortlist selection, rather than comparison selection." >}}

While slightly more complex to implement, that's pretty much an absolute solutions that seems to be working fairly well. Alternatively, just having a "comparison" bar docked at the bottom of the page is surely a reliable solution as well.

### How Many Items Can Be Added For Comparison?

<p>While some interfaces are very restrictive, allowing exactly 2 items to be compared at a time, it's more common to allow up to 4–5 items for comparison — usually because of space limitations in the comparison view. Admittedly, the comparison becomes very complex with more than 5 items in the list, with columns getting hidden and "showing differences" getting less useful. But what if the customer chooses to compare more items after all?

<p>Well, not many customers are likely to do that, except for one specific exception. Some customers tend to misuse the shopping cart and feature comparison as wishlist, "saving items for later" as reference. If they choose to save a large number of items, we could of course let them navigate through products using a stepper, but perhaps by default we could reshape the table and extract highlights, advantages and disadvantages instead. That might be slightly less annoying than being disallowed to add an item for comparison altogether.

{{% ad-panel-leaderboard %}}

## The Fleeting Life Of Side-By-Side Comparison

<p>Eventually, after tapping on those checkboxes or links, the customer hopefully will choose to see a comparison of the shortlisted options side by side. This comparison is usually a short-lived species: It's used as long as it serves its purpose, potentially getting shared with friends and colleagues, only to disappear into oblivion a short while after. Now, the comparison could appear in different ways:

<ol>
<li>on the same page, as a full-page overlay;</li>
<li>on a separate new page, integrated in the website's layout;</li>
<li>on a separate new page, standalone;</li>
<li>in a separate tab or window opened in addition to the tab that the user is currently on.</li>
</ol>

<figure><a href="https://www.appliancesconnection.com/french-door-refrigerators.html"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de3d64f5-66f9-494a-bd06-f06e60036c32/appliance-connection-overlay-800w.gif" width="800" height="672" alt="Appliance Connection's feature comparison." /></a><figcaption><a href="https://www.appliancesconnection.com/french-door-refrigerators.html">Applainces Connection</a> with a sliding comparison overlay. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b889ef9-5f4d-4217-814d-5c14f58c51a7/appliance-connection-overlay.gif">Large preview</a>)
</figcaption></figure>

What's best? In most situations, the second option might be difficult to pull off meaningfully, just because of the amount of space that a feature comparison needs to enable quick comparison of attributes. Both the <strong>first and the third options</strong> are usually easier to implement, but the first one might appear slightly faster because no navigation between pages is involved. However, it will also require proper implementation of the URL change based on the state of the comparison. With a standalone page, this problem would be slightly easier to solve. As an alternative, you could suggest to "save the comparison" and generate a link that can be shared.

<p>The fourth option depends on your stake in the never-ending discussion of whether <a href="https://www.smashingmagazine.com/2008/07/should-links-open-in-new-windows/">links should be opened in new tabs</a> by default. That's probably a matter of preference, but usually we must have a very good reason to open a window in addition to the existing one. While it might make sense for PDF files or any pages that might cause a loss of inputted data, it might not be critical enough for a comparison view.

<p>Ideally, you could provide both options &mdash; the link could lead directly to the comparison view in the same tab, and a Wikipedia-like external-link icon could be used to indicate a view to be opened in a separate tab.

## A Slightly Different Feature Comparison, Or Asking The Right Question In A Right Way

<p>In the end, we just want to help users <strong>find relevant comparable attributes quickly</strong>. What better way to find them than by first asking the user to select the attributes that matter most to them?

### Match Score Comparison

<p>For instance, we could extract some of those attributes automatically by looking into the qualities that appear in reviews for selected products, and suggest them in a small panel above the side-by-side comparison &mdash; pretty much like tags that the user can confirm or add.

<p>Once the relevant attributes are defined, we could calculate the <strong>match score</strong> for all selected products (based on reviews and specifications), and if their average is way below expectations, suggest alternative products with a higher score instead.

{{< vimeo id="228781704" caption="Alternatively, to help with picking a &ldquo;winner&rdquo;, we could let customers highlight favorite options and then allow customers to remove everything else, rather than manually remove irrelevant options." >}}

The option with the highest score could be suggested as the "recommended purchase" or as the winner, with the percentage of customers who have ended up buying that product in the category and maybe even scores from external professional reviews. There, we could show options to purchase the item or pick it up in a store nearby more prominently. To round up, we could even complement the comparison with a lovely "battle" loading indicator to convey that we are "working hard" to find the best option.

<p><a href="https://www.toptenreviews.com/home/kitchen/best-side-by-side-refrigerators/">Top Ten Reviews</a> manages to display 10 products in a side-by-side comparison. Each product has a rating broken down by specific groups of features, but also an overall score. The winner is highlighted with a "Gold Award," and on narrow screens its column is fixed, while other products are compared against it. That's a slightly more opinionated design, but perhaps it's also slightly easier to detect the winning candidate from the user's perspective.

{{< vimeo id="228779569" caption="<a href='https://www.toptenreviews.com/home/kitchen/best-side-by-side-refrigerators/'>Top Ten Reviews</a> is slightly more opinionated but also slightly more useful." >}}

### Matrix Comparison View
<p>When looking into comparisons, we naturally think about feature comparison tables, but perhaps a filtered view or a visual view would be a better option for comparisons &mdash; especially for complex ones. <a href="https://www.productchart.com/monitors/">Product Chart</a>, for example, uses a matrix presentation of products, with price mapped against screen size for monitors. Features and attributes can be adjusted as filters on the left, and the fewer the candidates, the larger the thumbnails. That's not an option for every website, but it's interesting to see a comparison outside the scope of a tabular layout.

{{< vimeo id="228786295" caption="<a href='https://www.productchart.com/monitors/'>Product Chart</a> has a matrix view for products, with filters placed on the left." >}}

Feature comparison can, but doesn't have to be a complex task for customers. We could take care some of the heavy lifting by suggesting better options based on customer's preferences. Unfortunately, I'm yet to find any example of this concept in a real eCommerce interface.

### Integrating Comparison Seamlessly

<p>But what if we drop the idea of having a dedicated feature comparison altogether — and use a slightly more integrated approach instead? Customer's experiences reflected in reviews are often more valuable than product specs, so what if we let customers explore suggestions based on keywords extracted from reviews?

<p>In his article on <a href="https://medium.com/ux-for-india/customer-reviews-should-help-others-take-informed-decisions-and-not-confuse-them-37050f308523">UX Breakdown of Customer Reviews</a>, Raviteja Govindaraju suggested a couple of options of how it could look.

<figure><a href="https://medium.com/ux-for-india/customer-reviews-should-help-others-take-informed-decisions-and-not-confuse-them-37050f308523"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d00becb4-9b51-4d55-84a3-c49d79efff9c/dynamic-reviews.gif" width="608" height="422" alt="Dynamic reviews UX concept" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d00becb4-9b51-4d55-84a3-c49d79efff9c/dynamic-reviews.gif">Large preview</a>)</figcaption></figure>

<figure><a href="https://medium.com/ux-for-india/customer-reviews-should-help-others-take-informed-decisions-and-not-confuse-them-37050f308523"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc5ed209-a07d-4ca0-9f26-b183ee11165d/sort-by-keywords-800w-opt.png" width="800" height="552" alt="Sorting products by keyword extracted from reviews." /></a><figcaption>Integration of keywords extracted from reviews on a product page and a category page. A <a href="https://medium.com/ux-for-india/customer-reviews-should-help-others-take-informed-decisions-and-not-confuse-them-37050f308523">concept</a> by Raviteja Govindaraju. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19b74ec4-ee82-4b53-a63a-08be01694201/sort-by-keywords-large-opt.png">Large preview</a>)</figcaption></figure>

A product page could display extracted review keywords upon tap or click. On a category page, a product comparison would extend "common" filters with sorting by these keywords. Finally, instead of a feature comparison table, the customer could select the features they care about most and the overview would provide a list of "best" options for them.

<figure><a href="https://medium.com/ux-for-india/customer-reviews-should-help-others-take-informed-decisions-and-not-confuse-them-37050f308523"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fafc946-4b82-43de-8942-4c2cce11c08b/ideal-flow.gif" width="278" height="456" alt="Ideal user flow to find a product." /></a><figcaption>Relevant features first, selection later. A <a href="https://medium.com/ux-for-india/customer-reviews-should-help-others-take-informed-decisions-and-not-confuse-them-37050f308523">concept</a> by Raviteja Govindaraju.</figcaption></figure>

In the same way, if a customer is looking for a set of products rather than just one standalone product, we could provide "recommended" options in a <a href="https://medium.com/ux-for-india/exploring-e-commerce-navigation-patterns-8f5a4efbce09">contextual preview</a>. Based on measurements of an apartment, for example, we could suggest electronics and furniture that might work well. The feature might be particularly useful for the fashion industry as well.

<figure><a href="https://medium.com/ux-for-india/exploring-e-commerce-navigation-patterns-8f5a4efbce09"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54323cc7-0bea-4bac-8aa8-df0649783603/exploring-options-800w-opt.png" width="800" height="621" alt="Pins placed on the image to indicate customization." /></a><figcaption>The products could be presented in a contextual preview as well. A <a href="https://medium.com/ux-for-india/exploring-e-commerce-navigation-patterns-8f5a4efbce09">mock-up</a> by Raviteja Govindaraju. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/921eddbf-b0c3-4ee2-94ec-398b74694c4d/exploring-options-large-opt.png">Large preview</a>)</figcaption></figure>

These solutions basically provide a slightly extended filtering option, but it shows how a feature comparison can go beyond a "traditional" side-by-side comparison. The better and smarter the filtering options, the less critical a side-by-side feature comparison could be.

## Accessible Markup

<p>While <a href="https://twitter.com/smashingmag/status/897159927835353089">many of us</a> would consider the <code>table</code> element to mark up a comparison table, in accessibility terms, sometimes that might not be the best idea. The comparison could be just an unordered list (<code>li</code>) with headings &mdash; for instance, an <code>h2</code> for the title of each product and <code>h3</code> subheadings for the features of each product. Screen readers provide shortcuts for navigating between list items and headings, making it easier to jump back and forth to compare.

<p>That way, we could basically create cards, collapsed or not by default, and then progressively enhance the list towards a tabular view for easier visual scanning. Highlghting differences would then mean just rearranging cards based on customer's preferences. Still, with labels and headings, a table might be a good option as well.

<p>As <a href="https://twitter.com/LeonieWatson">Léonie Watson</a>, an accessibility engineer and W3C Web Platform WG co-chair, put it, "casting your eyes between two data sources is relatively easy to do, but a screen reader doesn't have any really good way to emulate that behavior". According to Léonie, "if there is a single comparison table (where the data to be compared is in different columns/rows), then the most important thing is that the table has proper markup. Without properly marked up row/column headers, it is hard to understand the context for the data in an individual table cell.

<p>Screen readers have keys for moving up/down through columns, and left/right through rows. When a screen reader moves focus left/right into a table cell, the column header is automatically announced before the content of the cell. Similarly, when screen reader focus moves up/down into a cell, the row header is announced before the cell content.

<p>If the data sources for comparison are in different places/tables, then things get a bit harder. You have to remember the data from one source long enough to be able to navigate to the data source for comparison, and frankly that's a cognitive burden most people will struggle with.

<p>A more general purpose solution is to offer customers choices of how the data is presented — for example, to choose to view all data in a single table, or to select certain objects for comparison." 

## Feature Comparison Design Checklist

<p>Phew! That was quite a journey. Below you'll find all of the design considerations one has to keep in mind when designing a feature comparison table. You thought it was easy? Think again.

<p>Now, below is a list of features that a good comparison is likely to have. We covered most of them in the beginning of this article, but they are worth having in one place after all:

<ul>
<li>Every column contains the price (or price graph), a link to the standalone product page, ratings, the number of reviews, a thumbnail, the product's model name, and a price-matching tooltip.</li>
<li>For every product, useful reviews, with major advantages and disadvantages as keywords, are extracted and highlighted above the comparison.</li>
<li>Attributes are consistent and have comparable meta data; they are grouped, and some of them are collapsed by default.</li>
<li>If there isn't enough meaningful meta data to compare against, explain that to the customer and suggest third-party reviews instead. Irrelevant tables are frustrating.</li>
<li>The customer can switch to seeing only differences, only similarities or all attributes.</li>
<li>The customer can reset their selection and return back to the products (perhaps with breadcrumb navigation at the top).</li>
<li>The customer can add new products to the comparison (for example, if they are unsatisfied with the results of a comparison).</li>
<li>Columns and rows are highlighted upon hover or tap.</li>
<li>The customer can rearrange columns by dragging or moving them left and right.</li>
<li>Every action provides confirmation or feedback.</li>
<li>Customers can generate a shareable link for comparison (for example, "Save comparison as…").</li>
<li>If the user spends too much time in the comparison view, a window with information for hotline support or chat is displayed.</li>
<li>Items are stored persistently after page refresh or abandonment.</li>
<li>The feature comparison is responsive, bringing focus to the differences and the advantages and disadvantages of products.</li>
</ul>

### Questions and Considerations

<p>And here are the questions the team will have to consider when designing and implementing a comparison table.

<ul>
<li>How do you indicate that comparison is possible?</li>
<li>What happens when the first item is added for comparison?</li>
<li>Have you disabled the option to compare when only one item has been selected?</li>
<li>Once an item has been selected, do you change the link or highlight the selected product, or display a comparison bar, or display a lightbox?</li>
<li>How do users unselect a selected option?</li>
<li>If only one item has been added for comparison, should we suggest products to compare or enable users to "find similar products"?</li>
<li>When an item has been selected, do you provide visual feedback to reaffirm and reassure users about their choice. (For example, "Good choice! That's one of the top-10 rated cameras in the category!")</li>
<li>How many items may a customer add for comparison (usually three to five)? What happens to the comparison if no or one item has been selected. What about more than five items?</li>
<li>As items are being compared, do we use animation or transitions to indicate comparison (such as a battle animation)?</li>
<li>Do we display the price (or price development), a link to the individual product page, ratings, reviews, a thumbnail, the product's model name, and price-matching tooltip?</li>
<li>Can users switch to see only differences, only similarities or all attributes?</li>
<li>Do we group and collapse attributes by default?</li>
<li>Do we track whether attributes are consistent and have comparable meta data? Otherwise, seeing differences would be meaningless.</li>
<li>Do we highlight columns and rows upon hover or tap?</li>
<li>Can the user move columns left and right?</li>
<li>What if the user compares items in unrelated categories (for example, a laptop against batteries)?</li>
<li>How do we allow users to add more items for comparison?</li>
<li>How do we allow users to remove items from comparison?</li>
<li>Should we dynamically track how many items are in the comparison list, and prompt a message if there are none ("Oh, nothing to compare! Here are some suggestions.") or one ("Boo-yah! You've got a winner!") or two ("So, you have just two candidates now.")?</li>
<li>Should we ask customers to choose what they care about most?</li>
<li>Do we suggest a "winner" among the products selected for comparison, perhaps based on the user's most relevant attributes?</li>
<li>Does every action have visual and/or aural feedback to indicate change?</li>
<li>Have we provided a shareable link for comparison (for example, "Save comparison as…")?</li>
<li>If the user spends too much time in the comparison view, should we prompt a window with information for hotline support or chat?</li>
<li>Are compared items stored persistently after the page is refreshed or abandoned?</li>
<li>Do we include a "Notify about price drop" option for email subscription?</li>
<li>Is the feature comparison accessible, coded as an unordered list?</li>
<li>How do we make the feature comparison behave responsively?</li>
</ul>

## Further Resources

<ul>
<li>"<a href="https://www.nngroup.com/articles/comparison-tables/">Comparison Tables</a>," Nielsen Norman Group,</li>
<li><a href="https://vimeo.com/tag:featurecomparison">Feature comparison implementations in HD</a> on Vimeo.</li>
</ul>

## Stay Tuned!

<p>This article is a <strong>part of the new ongoing series</strong> about design patterns here, on your truly Smashing Magazine. We'll be publishing an article in this series every two–three weeks. Don't miss the next one, on builders and configurators. Ah, interested in a <strong>(printed) book covering all of the patterns</strong>, including the one above? Let us know in the comments, too — perhaps we can look into combining all of these patterns into one single book and publish it on Smashing Magazine. <em>Keep rockin'!</em>

<p><em>Huge thanks to Heydon Pickering, Léonie Watson, Simon Minter, Penny Kirby, Marta Moskwa, Sumit Paul for providing feedback for this article before publication.</em>

{{< signature "al, yk, il" >}}


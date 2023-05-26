---
title: 'Designing Filters That Work: Best Practices and Guidelines'
slug: frustrating-design-patterns-broken-frozen-filters
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c5f2df3-3d78-4563-a599-8c924604e84a/7-frustrating-design-patterns.png
date: 2021-07-14T13:30:00.000Z
summary: >-
  Too often dealing with filters can be frustrating. Let’s get them right. That means never freeze the UI on a single input, provide text input fallback and never auto-scroll users on a single input. Here’s why.
description: >-
  Too often dealing with filters can be frustrating. Let’s get them right. That means never freeze the UI on a single input, provide text input fallback and never auto-scroll users on a single input. Here’s why.
categories:
  - Design Patterns
  - Usability
  - Best Practices
  - Web Design
  - UX
---

Filters are *everywhere*. While we often think of them appearing when booking flights or shopping online, filters are frequently used in pretty much every interface that features more than a handful of data points.

It’s not necessarily just the sheer amount of data that is difficult to make sense of though; it’s the **complexity and lack of consistency** that the data usually entails which requires some filtering &mdash; such a common scenario in data grids, enterprise dashboards, vaccine tracking and public records registries.

<div class="c-felix-the-cat">
<h4 class="h3">Part Of: <a href="/category/design-patterns/">Design Patterns</a></h4>
<ul>
<li>Part 1: <a href="https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/">Perfect Accordion</a></li>
<li>Part 2: <a href="https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/">Perfect Responsive Configurator</a></li>
<li>Part 3: <a href="https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/">Perfect Date and Time Picker</a></li>
<li>Part 4: <a href="https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/">Perfect Feature Comparison</a></li>
<li>Part 5: <a href="https://www.smashingmagazine.com/2017/07/designing-perfect-slider/">Perfect Slider</a></li>
<li>Part 6: <a href="https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/">Perfect Birthday Picker</a></li>
<li>Part 7: <a href="https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-mega-dropdown-hover-menus/">Perfect Mega-Dropdown Menus</a></li>
<li><strong>Part 8: Perfect Filters</strong></li>
<li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next ones.</li>
</ul>
</div>

## Designing For The Comfortable Range

As customers, we use filters to reduce a large set of options to a more manageable and highly relevant selection. Perhaps just a few dozens of payment slips instead of thousands, or just a handful of blouses rather than the entire collection.

We have specific attributes of interest, a specific *intent*, that we need to somehow communicate to the interface. We do so by breaking our intent down into a set of available features. That intent might be fairly specific or quite general, but in both cases, the design should **minimize the time** needed for customers to get from the default state (when no filters are selected) to the final state (when all filters are successfully applied).

{{< rimg breakout="true" href="https://transportnsw.info/trip#/trip?from=211099&to=poiID:858286362:95301001:-1:Sydney%20Opera%20House:Sydney:Sydney%20Opera%20House:ANY:POI:4890002:3754415:GDAV:nsw&leaving=true&excludedModes=11&onlyAccessible=false&walkSpeed=0&gettingFromMode=100&gettingToMode=100&onlyOpal=false&gettingToValue=20&gettingFromValue=20&tripPreference=0&travelMode=publicTransport" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c283becc-5402-4a3d-acb3-b3c4af0193bc/nsw-transport.jpg" width="800" height="492" sizes="100vw" caption="A well-designed filter in a well-designed trip planner UI. <a href='https://transportnsw.info/trip#/trip?from=211099&to=poiID:858286362:95301001:-1:Sydney%20Opera%20House:Sydney:Sydney%20Opera%20House:ANY:POI:4890002:3754415:GDAV:nsw&leaving=true&excludedModes=11&onlyAccessible=false&walkSpeed=0&gettingFromMode=100&gettingToMode=100&onlyOpal=false&gettingToValue=20&gettingFromValue=20&tripPreference=0&travelMode=publicTransport'>NSW Trip Planner</a>" alt="A well-designed filter in a well-designed trip planner UI." >}}

That’s only one part of the story though. Applying relevant filters is the easy part, but showing *just enough* relevant results is slightly more difficult. In fact, for every interface, and for every intent, we have a particular **comfortable range** in mind, that is a preferred number of options that we think we can manage relatively effortlessly.

This range of options doesn’t have to fit on a single screen, or be displayed on a single page, or be limited to a small shortlist that we can easily remember. It can be anything from **dozens to hundreds of items** scattered over a number of pages.

The important part is that this range meets our expectations that: 

- we are looking at highly relevant options,
- we can easily understand what we are exploring,
- we can spot the differences between all options, and
- we can process everything within a reasonable, foreseeable timeframe.

{{< rimg breakout="true" href="https://www.sears.com/tvs-electronics-televisions/b-1231470962?shipOrDelivery=true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/535f6b02-4359-450a-8b69-a9d8edf5d277/tv-filtering.jpg" width="800" height="488" sizes="100vw" caption="What's the comfortable range when choosing a TV? Probably not 500 options, but rather 5–10 good ones. That's where filters matter. <a href='https://www.sears.com/tvs-electronics-televisions/b-1231470962?shipOrDelivery=true'>Sears: TVs</a>" alt="What's the comfortable range when choosing a TV? Probably not 500 options, but rather 5–10 good ones. That's where filters matter." >}}

Unlike sorting, which merely *rearranges* the results according to some preferred attributes (*soft boundaries*), filters always represent **hard boundaries.** They strictly limit the scope of results. Not enough proper filters and users shoot way over the comfortable range; too many filters and users end up with zero-results and abandon the site altogether.

The comfortable range **varies significantly** from a product to product. The cue to where it lies can be inferred from how different the options actually are. In usability tests, we see people having no issues exploring 20–30 kinds of vehicles, 40–50 kinds of sneakers, 70–80 bouquets of flowers, or even paginating through 100–200 payment slips. Yet they feel utterly overwhelmed when exploring 15 different types of sharpies or AAA-batteries. As a rule of thumb, it seems that the more *different* the options are, the more comfortable we feel with a slightly larger set of options.

The ultimate question, then, is how to find that delicate balance, when our interface helps users *quickly* arrive at *just enough* results. One answer to that question lies in something that sounds awfully obvious: **eliminate any roadblocks** on users' path towards that comfortable range. It’s easier written than done though &mdash; especially when you have dozens or even hundreds of filters that have to be accessible on mobile, on desktop, and everywhere in-between.

## The Complexity of Filtering

At the first glance, filtering doesn’t seem like a particularly complex endeavour. Of course we can have lengthy debates about the right form elements for different kind of filters &mdash; autocomplete, radios, toggles, select-dropdowns, sliders and buttons just to name a few &mdash; but in their essence, all of the form elements are just basic input, right?

Well, as it turns out, there are quite a few facets of the experience that make designing filters **quite difficult**:

- filters can come in **various flavours** and shapes, for pricing, ratings, colors, dates, times, size, brand, capacity, features, level of experience, age range, symptoms, product status etc.
- filters usually come in **large numbers**, and they need to be displayed across screens,
- filters often have different **states** (selected, unselected, disabled)
- filters often need **sensible defaults**, and they have to remember user’s input,
- filters can be **interdependent**, and these dependencies need to be obvious,
- filters can be **difficult to validate**, e.g. when users can type in complex data, such as time or dates,
- filters need to support and show meaningful **error messages,**
- and so many others.

**Filters never exist on their own**; in one way or another, they are always connected to the results that they are acting upon. This connection often causes filters and matching results to be somewhat <em>synchronous</em>, as the latter depend on how fast the UI registers an input, and how much time it needs to successfully process it.

Now, addressing all the fine intricacies of each of these challenges is nothing short of monumental work, yet some issues are slightly more frustrating than others, making the overall experience painful and annoying, and hence causing high abandonment and high bounce rates. Let’s explore some of the critical ones.

{{% feature-panel id="vitaly-friedman" %}}

## Avoid Tiny Scrollable Panes

After just a few usability sessions with customers who try to use filters on their own device, one can spot some **common frustrations** making rounds over and over again. One of the most annoying patterns comes from lengthy filter sections that contain dozens of options. These options often get tucked away in a tiny scrollable pane, showing 3–4 options at a time and requiring vertical scrolling to browse the options. 

These sections often cause customers to scroll vertically, slowly, accurately, with extreme focus and precision. As they do so on mobile, some filters get activated by mistake, prompting the customer to be even more focused. A classic example of this pattern is the “Brands” filter, which often contains hundreds of options, sorted by popularity or by alphabet.

{{< rimg breakout="true" href="https://bt.rozetka.com.ua/blenders/c80155/producer=braun,domotec/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8528f3af-6fa4-46e8-81ac-34b0644da627/1-frustrating-design-patterns.png" width="800" height="423" sizes="100vw" caption="A large scrollable filter area on the left, on <a href='https://bt.rozetka.com.ua/blenders/c80155/producer=braun,domotec/'>Rozetka.ua</a>." alt="A large scrollable filter area on the left, on Rozetka.ua." >}}

An alternative option would be to show as many as 7–10 options at a time with an accordion that would expand and show all options on tap/click. These options don’t have to be displayed in their full height, but can live in a **larger scrollable pane**. But then they shouldn’t be activated by scrolling through the pane.

It’s also a good idea to compliment the filter with a search autocomplete and an alphabetical view if some of the popular options are highlighted at the top. A good example of it is [Rozetka.ua](https://bt.rozetka.com.ua/blenders/c80155/producer=braun,domotec/), an eCommerce retailer from Ukraine (see above).

## Always Provide Text Input Fallback For Sliders

Whenever users can define a large *range* of values, be it pricing range in retail store, max duration of a train trip or a min/max coverage for an insurance plan, we probably will use some sort of a **slider**. All sliders have one thing in common: they are wonderful when we want to encourage customers to explore many options quickly, but they are quite frustrating when the user has something specific in mind and hence needs to be a little bit more precise.

Just think about the frustration we usually have to go through when bumping up the price a little bit, from $200 to $215, or adding another hour for the duration of a flight. Doing so with a slider is difficult because it requires incredible precision, and that always produces mistakes and causes frustration.

We’ve covered [how to design a perfect slider](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/) in detail already, but probably the most important feature that every slider needs is to support different *speeds* of interaction. In fact, there are a few common types of interaction:

- when customers want to explore many options quickly, a good ol’ slider with a track and a thumb works perfectly fine;
- when customers want to be more precise in their exploration, we can help by **adding steppers** **(+/-)** for granular jumps forward and backwards,
- when customers have an exact value in mind, we can help by providing **text input fields** for min/max values, so users can type in values directly without having to use the slider,
- in all of these cases, solutions have to be accessible and support keyboard-only interaction.

Take a look at the [Lloydsbank](https://www.lloydsbank.com/)’s example below. A [personal loan calculator](https://www.lloydsbank.com/loans/loan-calculator.html) supports all types of interaction beautifully. Also, notice the focus styles when the thumb is activated, and ranges displayed below the interest rate slider at the top to indicate where the customer is currently navigating. The interest rate changes depending on how much money the customer would like to borrow.

{{< rimg breakout="true" href="https://www.lloydsbank.com/loans/loan-calculator.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8c08283-92bd-4984-93f2-7af03888a725/2-frustrating-design-patterns.png" width="800" height="502" sizes="100vw" caption="A slider that supports three speeds of interaction: a slider for quick exploration, a stepper for granular jumps and text input field fallback for more precision. On <a href='https://www.lloydsbank.com/loans/loan-calculator.html'>Lloydsbank</a>." alt="A slider that supports three speeds of interaction: a slider for quick exploration, a stepper for granular jumps and text input field fallback for more precision." >}}

Another interesting example of a well-designed slider comes from Made.com’s [Sofasizer](https://www.made.com/sofasizer), which allows you to filter couches based on the dimensions that they need to have. Rather than using a set of input fields, Made.com chose to use a visual interface with a “Resize” icon. You can drag the handle to adjust the size, or you can type in exact values in the height and width input fields.
 
{{< vimeo id="572281981" caption="Made.com’s <a href='https://www.made.com/sofasizer'>Sofasizer</a> allows you to filter couches based on the dimensions that they need to have to fit in your apartment. A text input fallback is provided as well." breakout="true" >}}

## Never Auto-Scroll Users On A Single Input

You’ve been there before. Perhaps in the rush of excitement you head to the retail store, click on all the right category links, swipe left and right through sub-navigation, and eagle eye into that one shiny new laptop that you now finally ready to commit to. What’s expecting you next might not be quite the experience you were hoping to indulge yourself on. Take a look at the example below. Can you spot what seems to be happening?

{{< vimeo id="572282565" caption="<a href='https://www.dell.com/en-us/work/shop/dell-laptops-and-notebooks/sr/laptops/latitude-laptops'>Dell</a>’s filters aren’t very responsive. If you tap fast, you’ll need to have a bit of luck for all your filter inputs to be registered successfully." breakout="true" >}}

In this example from [Dell.com](https://www.dell.com/), as you choose your laptop features, only a single input is registered at a time. If you happen to be selecting multiple options quickly, only the last input will be applied. And as an input *is* registered, the page refreshes, jumping the customer all the way to the top of the filtering sidebar. That means that the more filters you want to use &mdash; and usually navigate from top to bottom &mdash; the more you’ll have to keep scrolling down to find the right filter.

A reason why this implementation is so common is not because we want to auto-scroll customers to the top of the *filters* area, but rather because we want to drive them towards the **top of the products results** with filters applied. Being stuck somewhere in the middle of the list won’t be particularly useful once you have new filters applied. And indeed, it is better to show the top of the results with every filter update, but it doesn’t mean that we need to auto-scroll filters as well.

In fact, even if you’d like to specify just 6–10 features this way, you’ll need to embark on a quite stubborn **scrolling fight against the auto-scroll**, with only a single filter registered at a time. It *is* possible to tap or click on multiple filters at a time, but in this case unfortunately the UI won’t respond as expected. The overall experience is quite frustrating and disorienting, also because the website feels slow, and it always takes more and more effort to continue filtering. Not the best example of minimize the time from the default state to the final state.

One way to tackle these issues would be to **remove auto-scroll for filters altogether** and find a better way to indicate that only one input can be made at a time. For example, we could freeze the entire interface and thus disable any input until the new data comes back from the server. Then we'd need to wait for new results to be injected into the DOM, and only then have the UI coming back. While it is slightly clearer than the previous solution, it turns out to have issues on its own.

{{% ad-panel-leaderboard %}}

## Never Freeze The UI On A Single Input

Every time we freeze the UI on a single input, we actively slow down our customers in expressing their intent. We actually make it a bit more cumbersome for them to specify what they are interested in, prioritizing the display of results over the input. That seems to be a wrong prioritization though. Let’s take a look at the example below.

{{< vimeo id="572283531" caption="It’s common for customers to want to set multiple filters right after another. Freezing the UI on every single input slows them down and makes it just a bit more difficult. Example: <a href='https://www.sears.com/appliances-refrigerators/b-1020022'>Sears.com</a>." breakout="true" >}}

At [Sears.com](https://www.sears.com/appliances-refrigerators/b-1020022), every time a selection is made, not only is the UI fully blocked; the users are also pushed to the top of the page. That’s especially frustrating for filters that include accordions (“see more” link in “Brand”, for example). With every new filter, the user has to scroll down and open the accordion to find that particular attribute that they want to select. [Walmart](https://www.walmart.com/browse/sports-outdoors/treadmills/4125_4134_1074324_1074326) (see example below) follows the same pattern.

{{< vimeo id="572284295" caption="<a href='https://www.walmart.com/browse/sports-outdoors/treadmills/4125_4134_1074324_1074326'>Walmart</a> blocks the UI and auto-collapses filter groups on every single filter input." breakout="true" >}}

In these cases we need to rely on JavaScript to toggle between frozen and working states reliably, even if the data hasn’t come back from the server, or if it comes back slowly, or if it’s ill-formed. That’s a quite fragile assumption to rely on.

Now, of course we don’t know when the user has *finished* with their input, but it’s only reasonable to ensure that during the *entire* interaction with filters, the customer **never has to wait for an interface to respond back**. Now, if we look a bit closer at the three examples above, we’ll notice one similarity. All of them auto-apply *every* filter upon selection, disabling any further selection until the new results page comes back. 

However, it’s remarkably common for customers to **add multiple filters quickly**, sometimes in the same category. The behavior of the UI doesn’t support this intent well.

So, do we have any alternatives? An obvious alternative is to hand over the decision to the user about when the results should be updated. That could mean adding an **“Apply” button** and encourage customers to select all filters first before seeing *any* results. But it’s not necessarily the only option. Actually, as it turns out, we can do both: seeing up-to-date results while interacting with the filter without any delay. We just need to move from synchronous display of results to its asynchronous counterpart.

## Always Show Results Asynchronously

We mentioned already that filters and matching results are often somewhat synchronous. However, we could **split the parts of the UI** and render both of them separately, asynchronously. In that case, on every filter input, matching results could be updated asynchronously, while the filters always remain accessible and at the same place. With every new filter input, the user would see a flash of new content streaming in.

{{< vimeo id="572294363" caption="Asynchronous display of results on <a href='https://www.bestbuy.com/site/searchpage.jsp?_dyncharset=UTF-8&browsedCategory=abcat0910002&id=pcat17071&iht=n&ks=960&list=y&qp=brand_facet%3DBrand~Amana%5Ebrand_facet%3DBrand~GE%5Ebrand_facet%3DBrand~Samsung&sc=Global&st=categoryid%24abcat0910002&type=page&usc=All%20Categories&intl=nosplash'>BestBuy</a>. Customers never have to wait for the UI to respond back, and can select multiple filters at once. Real-time product list updates appear on the right." breakout="true" >}}

The [BestBuy](https://www.bestbuy.com/site/searchpage.jsp?_dyncharset=UTF-8&browsedCategory=abcat0910002&id=pcat17071&iht=n&ks=960&list=y&qp=brand_facet%3DBrand~Amana%5Ebrand_facet%3DBrand~GE%5Ebrand_facet%3DBrand~Samsung&sc=Global&st=categoryid%24abcat0910002&type=page&usc=All%20Categories) example above shows that pattern in action. As we select filters in the left sidebar, they get applied in the background while we can keep selecting more and more filters should we choose to do so. The product list gets updated asynchronously: there is never a disabled state as new content gets populated into the list of matching results every time the data gets back from the server.

We could make it a bit more obvious by showing that new products are being loaded in as new filters are being applied. A good example of that is [Coolblue](https://www.coolblue.nl/laptops), with an asynchronous sidebar filtering UI appearing on the left hand-side.

{{< vimeo id="572295197" caption="Asynchronous loading of results on <a href='https://www.coolblue.nl/laptops'>Coolblue.nl</a>, a retailer from the Netherlands. With every filter input, the results are greyed out, indicating that new data is expected." breakout="true" >}}

It’s worth emphasizing at this point that every input in the filters area needs to be registered, and then applied to the product list. We’ve noticed that for many customers that’s an expected behavior, unless you keep a floating “Apply” button close to the filters area. 

## Avoid Layout Shifts On Filter Input

As long as the interface isn’t blocking input, of course customers expect that they can set a number of filters one after another. However, depending on where the filters are located, at times they might encounter **accidental layout shifts**, so they have to orient themselves on the page again, scroll up and down to find where they left off, and then continue with the next input. Take a look at the example below. What seems to be the problem on [VictoriaPlum](https://victoriaplum.com/browse/shower-bath-suites) (displayed below)?

{{< vimeo id="572297303" caption="Layout shifts prevent customers from providing preferred filters quickly. A minor issue on <a href='https://victoriaplum.com/browse/shower-bath-suites'>VictoriaPlum</a>." breakout="true" >}}

Every time users interact with a filter, once the new product items come in, there is a small shift happening in the filtering area. Usually there are three reasons why it happens:

- on every filter input, filter sections that have been expanded by the customer automatically collapse,
- filters that were available earlier become unavailable, and they become hidden, reducing the height of the filtering area,
- the overview of applied filters is located above the filters area, so as it grows in size with every new filter, it pushes the filters down as well.

To avoid the first issue, we need to **maintain the state of accordions** and keep them open, even if the user has set a new filter or refreshed the page. We also need to keep the settings of filtering upon refresh, or navigation. In fact, we see customers expecting the filters to **still be applied** even if they go back to previous categories or pages (e.g. with the “Back” button).

For the second issue, if filters aren’t available any longer, rather than hiding them automatically, we can disable them, but also **explain why they are disabled** (a friendly hint might help) and what needs to be done to re-enable them. We can then also add an option to “Hide all unavailable options”.

Finally, we might want to reconsider the position of applied filters above the filters area. There are really not that many options where they could live though, and a better option seems to be the area above filtering results.

## Display Filters Above The Results

To avoid layout shifts altogether, we can display applied filters **above the product results**. That would keep the filtering area stable and predictable during the entire user interaction. In fact, it doesn’t have to be visible at all times. [Crate & Barrel](https://www.crateandbarrel.com/furniture/dining-benches/), in the example below, allows customers to hide and show filters on demand, while applied filters are added to the dedicated area above products. Note that an option to clear all filters is available as well. (The product page has changed since the video was recorded though.)

{{< rimg breakout="true" href="https://www.crateandbarrel.com/furniture/dining-benches/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2b163ca0-8d60-45a7-9c6c-55b511734821/3-frustrating-design-patterns.png" width="800" height="571" sizes="100vw" caption="No layout shifts in sight on <a href='https://www.crateandbarrel.com/furniture/dining-benches/'>Crate & Barrel</a>. A very calm experience, with filter area that can be hidden if not needed." alt="No layout shifts in sight on Crate & Barrel. A very calm experience, with filter area that can be hidden if not needed." >}}
 
Another option is to turn all filter sections into overlays and display them on tap/click above the results. In fact, you could even use **floating filters**, so as a customer scrolls down the page, the filters are still accessible all the time.

An example of this pattern is [Adidas](https://www.adidas.de/en/women-shoes) (see the image below). The filters bar is persistent; even as users are scrolling down the page, the filter overlay **won’t close automatically** &mdash; it requires user’s input, again handing over the control to the user. However, it does close automatically once one of the filters is selected. If the user wants to select multiple filters, they have to re-open the same filter group over and over again. Keeping the filters persistent might be a better idea. Still, the result: no layout shifts, no frustrating scrolling in narrow corridors, and filters are always accessible.

{{< rimg breakout="true" href="https://www.adidas.de/en/women-shoes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e9cddc6-e6f2-4fda-a56a-8b15ee42fb04/4-frustrating-design-patterns.png" width="800" height="635" sizes="100vw" caption="On <a href='https://www.adidas.de/en/women-shoes'>Adidas</a>, the filters are displayed above the product list. Each filter group opens an overlay. However, with every filter input, the filter group would need to be re-opened." alt="On Adidas, the filters are displayed above the product list. Each filter group opens an overlay. However, with every filter input, the filter group would need to be re-opened." >}}

Not to say that displaying filters above the results is *always* better by default. On [Asos](https://www.asos.com/women/shoes/cat/?cid=4172&nlid=ww|shoes|shop+by+product|view+all), every filter input causes jumps to the top of the page, so customers have to manually scroll down to continue filtering. Instead of re-rendering the entire page, it would make more sense to re-render the filters area and the product list separately.

{{< vimeo id="572300988" caption="You can’t have it all: on <a href='https://www.asos.com/women/shoes/cat/?cid=4172&nlid=ww|shoes|shop+by+product|view+all'>Asos</a>, filter appears on the top, but every filter input causes a jump to the very top of the page." breakout="true" >}}

In general though, the first two options (Crate & Barrel and Adidas) seem to work very well, and they leave more space for products to be displayed, while avoiding all the troubles that we discussed earlier. That’s a quite reliable pattern to use when we want to avoid roadblocks or confusion. But we can still do a bit more, for example with a good ol’ “apply” button.

## Show The Number of Results On The “Apply” Button

It almost feels a little bit archaic to have an “Apply” button for filters in times when we are getting used to seamless and smooth interactions, fade-ins and timed animations. However, if we want to drive customers towards a comfortable range, there is hardly a better way of doing so than **displaying the number of results as soon as possible**.

{{< rimg breakout="true" href="https://www.ikea.com/gb/en/cat/tv-media-storage-14885/?filters=f-online-sellable%3Atrue" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98421fe7-f756-4337-a3e1-bc1df810a3e6/5-frustrating-design-patterns.png" width="800" height="657" sizes="100vw" caption="<a href='https://www.ikea.com/gb/en/cat/tv-media-storage-14885/?filters=f-online-sellable%3Atrue'>Ikea</a> shows filters above the results, sometimes as an overlay, sometimes as a pill." alt="Ikea shows filters above the results, sometimes as an overlay, sometimes as a pill." >}}

[Ikea](https://www.ikea.com/gb/en/cat/tv-media-storage-14885/?filters=f-online-sellable%3Atrue) features filters at the top of the results. Sometimes filters appear in a drop-down overlay, and sometimes as a pill below the filters. But most of the time, unlike previous examples, when a filter is selected, it displays a **sidebar mega-filter-overlay** on the right with all available filtering options grouped there. As the customer is making their way through the filters, the product list is updated in the background asynchronously. More importantly, notice the “Apply” button which label changes depending on the input.

With every filter input, a new request is sent to the server, retrieving the number of results, and then showing that number in the UI. That’s a great way to give users a very clear sense of how far or how close they are towards their comfortable range.

{{< rimg breakout="true" href="https://www.ikea.com/gb/en/cat/tv-media-storage-14885/?filters=f-online-sellable%3Atrue" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/046d59bf-3be2-4d15-a6d6-5dd182eb3be7/6-frustrating-design-patterns.png" width="800" height="670" sizes="100vw" caption="Most filters on Ikea appear in a dedicated sidebar overlay. <a href='https://www.ikea.com/gb/en/cat/tv-media-storage-14885/?filters=f-online-sellable%3Atrue'>Ikea</a>." alt="Most filters on Ikea appear in a dedicate sidebar overlay." >}}

Another example is [Galaxus.ch](https://www.galaxus.ch/) (see below), a Swiss eCommerce retailer that provides a first-class experience when it comes to filtering. The filters are displayed above product results; a filter overlay appears on tap/click. No slowdowns, fast response times and a lovely integration of active filters with the filters area. A **great reference example** that is worth considering when designing any kind of filter.

{{< rimg breakout="true" href="https://www.galaxus.ch/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c5f2df3-3d78-4563-a599-8c924604e84a/7-frustrating-design-patterns.png" width="800" height="614" sizes="100vw" caption="Everything in one: on <a href='https://www.galaxus.ch/'>Galaxus.ch</a>, filters are displayed above product results, a filter overlay appears on tap/click, and the overlay doesn’t disappear unless the user chooses to dismiss it." alt="Everything in one: on Galaxus.ch, filters are displayed above product results, a filter overlay appears on tap/click, and the overlay doesn’t disappear unless the user chooses to dismiss it." >}}

In general, having an **“Apply” button** along with real-time updates of the content area seems to be working best. It really combines the best of both solutions: showing results immediately when they arrive, while keeping filters accessible at all times.

{{% ad-panel-leaderboard %}}

## Avoid Split-Screens On Mobile

The issues that we’ve explored in the article apply equally to large and small screens. However, on small screens, and especially on slow connections, these issues become even more critical. Most of the time, **interfaces tend to block the entire UI** on a single filter input, causing massive delays for customers on the go (e.g. [Crutchfield](https://www.crutchfield.com/g_300/All-Car-Stereos.html?tp=5684), [Walgreens](https://www.walgreens.com/q/multi+symptom+relief+?N=2000012489-2000011429-305525)). On the other hand, it’s common to split the screen to display a filters overlay, while still showing the product list updated in the background (e.g. [Nordstrom](https://www.nordstrom.com/browse/women/clothing/tops-tees?campaign=0419wmnclothinghdrp01a&jid=j012040-15278&cm_sp=merch-_-womens_15278_j012040-_-cathead_wmnclothing_p01_shop)).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/204d3d52-1808-4be8-9a37-d7d0e35959df/8-frustrating-design-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/204d3d52-1808-4be8-9a37-d7d0e35959df/8-frustrating-design-patterns.png" width="800" height="486" sizes="100vw" caption="The usual suspects: blocking the UI and splitting the screen: Walgreens, Nordstrom, Crutchfield. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/204d3d52-1808-4be8-9a37-d7d0e35959df/8-frustrating-design-patterns.png'>Large preview</a>)" alt="The usual suspects: blocking the UI and splitting the screen: <a href='https://www.walgreens.com/q/multi+symptom+relief+?N=2000012489-2000011429-305525'>Walgreens</a>, <a href='https://www.nordstrom.com/browse/women/clothing/tops-tees?campaign=0419wmnclothinghdrp01a&jid=j012040-15278&cm_sp=merch-_-womens_15278_j012040-_-cathead_wmnclothing_p01_shop'>Nordstrom</a>, <a href='https://www.crutchfield.com/g_300/All-Car-Stereos.html?tp=5684'>Crutchfield</a>." >}}

In general, though, it might be a better idea to experiment if a **full-page overlay** for filters would perform better. It gives more space to experiment with a multi-column view, or perhaps even display a swipeable area to choose filters without having to move between separate pages. In fact, using accordions that could collapse and expand instead of bringing the user to a separate page might be a good idea &mdash; similar to what we’ve discussed with [mega-dropdowns](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-mega-dropdown-hover-menus/). 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a49c836-e804-480e-b4e2-25c90cc600f7/9-frustrating-design-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a49c836-e804-480e-b4e2-25c90cc600f7/9-frustrating-design-patterns.png" width="800" height="486" sizes="100vw" caption="Better options for displaying filters: <a href='https://www.myntra.com/women-ethnic-wear'>Myntra</a> and <a href='https://tylko.com/shelves/'>Tylko</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5a49c836-e804-480e-b4e2-25c90cc600f7/9-frustrating-design-patterns.png'>Large preview</a>)" alt="Better options for displaying filters: Myntra and Tylko." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37e12f40-5e36-412c-9863-89fc286069e5/10-frustrating-design-patterns.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37e12f40-5e36-412c-9863-89fc286069e5/10-frustrating-design-patterns.png" width="800" height="486" sizes="100vw" caption="Good reference examples: Galaxus.ch, Wayfair and Lacoste. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37e12f40-5e36-412c-9863-89fc286069e5/10-frustrating-design-patterns.png'>Large preview</a>)" alt="Good reference examples: <a href='https://www.galaxus.de/en/s1/producttype/headphones-48?tagIds=591'>Galaxus.ch</a>, <a href='https://www.wayfair.com/bed-bath/sb0/bedding-c481592.html'>Wayfair</a> and <a href='https://www.lacoste.com/us/lacoste/men/'>Lacoste</a>." >}}

Unlike on desktop, having an “Apply” button in all these examples matters, and you can make it slightly more useful by adding the amount of products as a label on the button and keeping the button sticky at the bottom as the user is scrolling down.

## Filtering Design Checklist

As usual, here are all the things to keep in mind when designing any kind of filter &mdash; a little helper to avoid missing important details before heading into conversations with your fellows designers and developers. You can find a **full deck** of [Smart Interface Design Patterns Checklists](https://www.smashingmagazine.com/printed-books/checklist-cards/) at yours truly Smashing Magazine as well.

<ol>
  <li>Can we avoid a filter icon and show filters as they are?</li>
  <li>If not, what icon do we choose to indicate filtering?</li>
  <li>Is the icon + padding large enough for comfortable tapping?</li>
  <li>Do we put the icon at the top, bottom or floating (mobile/desktop)?</li>
  <li> What exactly happens when the user clicks/taps on the icon?</li>
  <li>How will the icon change on tap/click?</li>
  <li>Will we have some sort of animation or transition on click?</li>
  <li>Will filters appear as full page/partial overlay or slide-in?</li>
  <li>Can we avoid sidebar filtering as it’s usually slow?</li>
  <li>Do we expose popular or relevant filters by default?</li>
  <li>Do we display the number of expected results for each filter?</li>
  <li>Can we use a horizontal swiper to move between filters?</li>
  <li>Can we avoid drop-downs and use only buttons/chips + toggles?</li>
  <li>For complex filters, do we provide search within filters?</li>
  <li>Do we use icons to explain differences between various filters?</li>
  <li>Do we use the right elements for filters, e.g. sliders, buttons, toggles?</li>
  <li>Do filters apply automatically (yes, for slide-ins)?</li>
  <li>Do filters apply manually on confirmation (“Apply”) (yes, for overlays)?</li>
  <li>How do we communicate already selected filters?</li>
  <li>Can selected filters appear as removable pills, chips or tags?</li>
  <li>Do we recommend relevant filters based on selection?</li>
  <li>Do we track incompatibility between selected filters?</li>
  <li>How do error messages or warning appear in the UI?</li>
  <li>Do we allow customers to reset all filters quickly, at once?</li>
  <li>Are filters (or filters button) floating on scroll on mobile/desktop?</li>
  <li>Can users tap on the same spot to open/close filters?</li>
</ol>

## Wrapping Up

Too often the filtering experience on the web is broken and frustrating, making it just **unnecessarily difficult** for customers to get to that shiny comfortable range of relevant results. When designing the next filter, take a look at some of the common issues that you might want to avoid, and hopefully avoid all the frustration that comes from broken and inaccessible implementations.

- **Design for the comfortable range** of options, for the case when a customer wants to add multiple filters quickly &mdash; one right after another.
- For lengthy filter groups, **avoid tiny scrollable panes** and show as many as 7–10 options at a time with an accordion that would expand and show all options on tap/click. Add a search autocomplete and an alphabetical view as well.
- Always add steppers (+/-) and **text input fields** when using sliders,
- Customer often want to set a number of filters of the same type. **Never auto-scroll users on a single input** and never collapse a group of filters automatically.
- **Never freeze the UI on a single input**, and never make your customer wait for an interface to respond back when setting filters.
- Always update filters and show results **asynchronously**, so that on every filter input, matching results could be updated asynchronously, while the filters always remain accessible and at the same place.
- Always **avoid layout shifts** on filter input and consider displaying filters above the results. 
- On mobile, *“Apply”-button* could be sticky at the bottom of the screen. Update the *count of products* and show them on the button.

### Articles of The Series

If you find this article useful, here’s an overview of similar articles we’ve published over the years &mdash; and a few more are coming your way.

- [Perfect Accordion](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/)
- [Perfect Responsive Configurator](https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/)
- [Perfect Birthday Picker](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/)
- [Perfect Date and Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
- [Perfect Mega-Dropdown](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-mega-dropdown-hover-menus/)
- [Perfect Feature Comparison](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/)
- [Perfect Slider](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/)
- [Form Design Patterns Book](https://www.smashingmagazine.com/printed-books/form-design-patterns/) by Adam Silver, published on SmashingMag
- [Subscribe to our email newsletter](https://www.smashingmagazine.com/the-smashing-newsletter/) to not miss the next ones.

{{< signature "il" >}}

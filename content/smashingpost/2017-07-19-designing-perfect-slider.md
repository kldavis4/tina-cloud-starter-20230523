---
title: Designing The Perfect Slider UX
slug: designing-perfect-slider
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc6aef2f-e2e0-413d-9c44-d1ed543012b1/urbanladder-opt.png
date: 2017-07-19T18:43:27.000Z
author: vitaly-friedman
summary: >-
  When we think about a slider, we usually imagine an image gallery slider, or the infamous carousel, or perhaps off-canvas navigation, with the overlay sliding in from the side. However, this article is not about those kinds of sliders. Instead, we’ll look into the fine details of designing better slider controls for selecting a value or a range of values. Think of price range sliders, 360-degree-view sliders, timeline sliders, health insurance quote calculators, or build-your-own-mobile-plan features.
description: >-
  When we think about a slider, we usually imagine an image gallery slider, or the infamous carousel, or perhaps off-canvas navigation, with the overlay sliding in from the side. However, this article is not about those kinds of sliders. Instead, we’ll look into the fine details of designing better slider controls for selecting a value or a range of values. Think of price range sliders, 360-degree-view sliders, timeline sliders, health insurance quote calculators, or build-your-own-mobile-plan features.
categories:
  - Usability
  - UX
  - Navigation
  - Design Patterns
  - Best Practices
  - Guides
---
In all of these use cases, a slider is helpful because it allows users to explore a wide range of options quickly. For precise input, a slider can never beat a regular input field, but we can use a slider to nudge our customers to explore available options and, hence, aid them in making an informed decision.

<figure><a href="https://dribbble.com/shots/3499449-Responsive-House"><img
sizes="(max-width: 1504px) 100vw, 1504px"
srcset="
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6a04dc0-f6e3-4273-b600-8062e7770405/master-levels-nl3bom-c-scale-w-190.png 190w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ee7e59e-177f-44cd-9348-6749c2ed2965/master-levels-nl3bom-c-scale-w-694.png 694w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d8ee1ee-6285-4011-9b72-d18eaf9763ec/master-levels-nl3bom-c-scale-w-1010.png 1010w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/071e0ad5-3381-48b5-92af-8318425ba882/master-levels-nl3bom-c-scale-w-1278.png 1278w,
https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09a5e544-dff7-48fb-9701-08948d64961a/master-levels-nl3bom-c-scale-w-1504.png 1504w"
src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09a5e544-dff7-48fb-9701-08948d64961a/master-levels-nl3bom-c-scale-w-1504.png" alt="Selekting a skill level in an app."></a><figcaption>A set of buttons is always an alternative for a slider, but a slider can help visualize options and put them in context quickly (for example, when selecting a skill level in a game). (Image: <a href="https://dribbble.com/shots/3625539-Skill-level">Petri Jääskeläinen</a>)</figcaption></figure>

<figure><a href="https://dribbble.com/shots/3499449-Responsive-House"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a25d454-177c-416a-a1dc-19abcf71c4a7/responsive-house.gif" width="800" height="600" alt="responsive-house-slider" /></a><figcaption>Sliders can be helpful in exploring and visualizing options quickly, but not when it comes to precise input. This playful animation is by <a href="https://dribbble.com/shots/3499449-Responsive-House">Gal Shir</a> and can be found on <a href="https://codepen.io/davidkpiano/pen/xLKBpM">CodePen</a>.</figcaption></figure>

However, more often than not, sliders are just a bit too difficult to use, require just a bit too much precision, are a bit too confusing to navigate, and are a bit too difficult to grab and move around. After a close look at perfect [accordions](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/) and [date and time pickers](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/), let’s turn our attention to sliders, with **do’s and don’ts and things to keep in mind** when designing one. But first, we need to figure out when a slider makes sense in the first place.

### Table of Contents

1.  [When Do We Need A Slider Anyway?](#when-do-we-need-a-slider-anyway)
2.  [The Many Facets Of Sliders](#the-many-facets-of-sliders)
3.  ["That Slider Doesn’t Belong Here"](#that-slider-doesnt-belong-here)
4.  [Slider Design Considerations Checklist](#slider-design-considerations-checklist)
5.  [The Rules Of Thumb For Spacing](#the-rules-of-thumb-for-spacing)
6.  [Displaying Tick Marks And Current Values](#displaying-tick-marks-and-current-values)
7.  [Choosing The Slider’s Scale](#choosing-the-sliders-scale)
8.  [Eliminating Zero-Results Filtering](#eliminating-zero-results-filtering)
9.  [Indicating The Range Visually](#indicating-the-range-visually)
10.  [Visualizing The Output](#visualizing-the-output)
11.  [Smooth ’n’ Silky Sliding, Guaranteed!](#smooth-n-silky-sliding-guaranteed)
12.  [They Ought To Slide, But They Choose To Click](#they-ought-to-slide-but-they-choose-to-click)
13.  [Enhancing A Slider With Precise Inline Editing](#enhancing-a-slider-with-precise-inline-editing)
14.  [Visual Feedback On Cursor](#visual-feedback-on-cursor)
15.  [Giving A Slider That Extra Touch](#giving-a-slider-that-extra-touch)
16.  [Contrast and Keyboard Accessibility](#contrast-and-keyboard-accessibility)
17.  [Where Does It Leave Vertical Sliders?](#where-does-it-leave-vertical-sliders)
18.  [Summary](#summary)
19.  [Further Resources](#further-resources)

## When Do We Need A Slider Anyway?

It’s not that every interface would benefit from a fancy slider. However, when we want to expose a variety of options or help users limit a number of options quickly, a slider can serve the purpose very well. In fact, whenever the input is “fuzzy” or not precise, then a slider is probably the first option one would consider &mdash; for example, when the user must choose a down-payment range for a mortgage or a time range for an airport departure (i.e. earliest to latest). In this case, choosing an amount down to the last cent or choosing a departure time to the last second isn’t really necessary.

<figure><a href="https://www.zillow.com/mortgage-calculator/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6106ef73-09b0-48e4-8640-54b893f5c10f/zillow-mortgage-calc-opt.png" width="800" alt="Zillow Mortgage calculator" /></a><figcaption>When it comes to exploring options, a slider could provide a slightly faster interaction than just typing in values in an input field. (Image: <a href="https://www.zillow.com/mortgage-calculator/">Zillow Mortgage Calculator</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fffe4a03-4789-495c-924f-9d45955540ef/zillow-rent-large-opt.png">View large version</a>) (<a href="https://player.vimeo.com/video/225595887">Watch video in HD</a>)</figcaption></figure>

Similarly, when buying a household item like a dishwasher, your customers might want to specify **minimum and maximum measurements** for the item, so that it’s not too small but still fits the space in their kitchen.

<figure><a href="https://tylko.com/shelf/bookshelves/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad0bbf9a-4e28-489f-9fa8-e4bb30dadbbc/tylko-shelves.gif" width="800" height="" alt="tylko-shelves" /></a><figcaption>On <a href="https://tylko.com/shelf/bookshelves/">Tylko</a>, the slider is complemented with a segmented control.</figcaption></figure>

On [Tylko](https://tylko.com/shelf/bookshelves/), the slider is complemented with a segmented control &mdash; options displayed as the users hovers or taps over the product areas. The price is adjusted continually, and the slider is never blocked by changes in input. Minor downsides: Visual feedback when hovering over the track would help, and increasing the padding both for the thumb and the track would help. Also, it would be helpful to be able to tap on the current value and adjust it manually.

When exploring a vacation destination, e.g. on [RoutePerfect](https://www.routeperfect.com/trip-planner/), users might want to filter their options by activities they’d love to experience. In this case, a slider could be used to enable them to assign weights to various kind of activities, so that the final selection of options are accurately tailored to their interests. Or when dealing with maps, a slider could help users limit or extend the geographical scope of their search.

<figure><a href="https://www.routeperfect.com/trip-planner/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efac2dcf-232c-4bfe-b471-aa3e99b05835/routeperfect-sliders-800w-opt.png" width="" height="" alt="routeperfect-sliders" /></a><figcaption>On <a href="https://www.routeperfect.com/trip-planner/">Routeperfect</a>, customers can explore destinations by exploring activities with a slider. Great idea, but the execution could be a bit better. The track is tiny, and so is the thumb. Increased padding or steppers added on both edges of the sliders would help. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b422627e-1275-44db-ac4f-352162b0381a/routeperfect-sliders-large-opt.png">View large version</a>)</figcaption></figure>

This isn’t to say that sliders can’t be precise. In an online shop, you might want to indicate delivery options, ranging from “Standard” to “Express” to “Priority” to “Overnight.” You could, of course, use a regular dropdown, but then the user would need to choose one of the dropdown options first to see how it affects the total price. A better way would be to use radio buttons instead, explaining how long delivery would take for each option and how much more it would cost. Showing all options in plain sight right away [seems to be the better option](https://twitter.com/smashingmag/status/884820192060211201).

<figure><a href="https://www.fuckdropdowns.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec4936b5-0045-4c5c-ac5a-cc0daf518466/shipping-options-drop-down.png" width="600" /></a><br>
<a href="https://www.fuckdropdowns.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba739298-73d3-47b4-82d0-0e44e56a71b7/shipping-options-slider.png" width="800" /></a><figcaption>When designing a checkout for physical goods, what would you use to illustrate shipping options? Probably not a dropdown. <a href="https://twitter.com/smashingmag/status/884820192060211201">Radio buttons might work well</a>, but a slider could work as well. We just need to add hints indicating the timing and cost of delivery. (Image: <a href="https://www.fuckdropdowns.com/">Eric Campbell, Golden Krishna</a>)</figcaption></figure>

However, users might need time to figure out their best option. Is “Overnight” faster than “Express”? How “express” is “Express” anyway? Is “Priority” faster than “Overnight”? That’s a classic problem for which a slider shines. Once the labels are arranged horizontally, you can use the area above the slider to communicate when the item will be delivered at the latest and what the total price will be, while also perhaps adding an expected delivery time range under each label. The further you slide to the right, the more expensive the delivery and the faster they’ll receive their item. It’s just a bit clearer this way.

On [Swisscom](https://swisscom.ch/en/residential/internet-television-fixednetwork/inone-home.html#), radio buttons trigger progress bar animations for **visualizing a plan**. On [Surfmangd.se](https://surfmangd.se/data/5), a plan is explained in plain text, but users can choose any amount of data. If you have only a few distinct plans, then the first option seems to be better, but if the user can choose any plan of their choice, then the animation could be adjusted based on the value on the slider as well.

<figure><a href="https://www.swisscom.ch/en/residential/plans-rates/inone-home.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72d9670d-b75b-4259-abb5-7635c13c747d/swisscom-speed-visualizer.gif" width="800" alt="Speed visualizer" /></a><br /><a href="https://surfmangd.se/data/5"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94cf8740-cf4c-4b61-94c0-656298755bc2/surmangd-speed-estimator.gif" width="800" alt="Speed estimator" /></a><figcaption><a href="https://swisscom.ch/en/residential/internet-television-fixednetwork/inone-home.html">Swisscom</a> and <a href="https://surfmangd.se/data/5">Sufrmangd.se</a> take slightly different approaches to visualizing the speed of a plan.</figcaption></figure>

That’s how a slider could be useful beyond filtering: explaining options or informing decision-making. When choosing a mobile plan, for example, the customer could choose how much data they’d love to have and see the monthly pricing adjusted right away. A slider could also be a good extension (though not a replacement) for a pricing table; so, instead of browsing through a (potentially complex) feature-comparison table, users could see the benefits of different tiers of pricing by sliding their thumb horizontally. This also goes for any “**pay what you want**” kind of service, where the slider could explain what the owner would be able to afford offering with each pricing tier.

<figure><a href="https://archive.is/g3QRV"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bf61bf7-ebc8-4df1-b2c6-0584ec586b4f/offscreen-opt.png" alt="Name your price experiment" width="472" /></a><a href="https://worksthatwork.com/blog/name-your-price"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ab93cc0-312c-43a6-9e8c-032cf8d91b15/pay-what-you-want.png" alt="Name your price experiment" width="472" /></a><figcaption>If you want to provide users with payment options, a slider is a good way to visualize the price and what the publisher can afford to offer with each pricing tier. (Image: <a href="https://worksthatwork.com/blog/name-your-price">Works That Work</a> and <a href="https://archive.is/g3QRV">Offscreen</a> (archived)) (<a href="https://33.media.tumblr.com/e953a7212fd61ca4cd474b32ba55e8ef/tumblr_nesosh0SPr1r92sruo1_1280.jpg">View large version</a>)</figcaption></figure>

Another common use case where sliders are almost omnipresent is banks and energy suppliers. Most banks will offer house loans, car loans and mortgage calculators, and most energy companies will help you choose your plan based on your household’s energy consumption. In these cases, the actual monthly payment will depend on calculations that aren’t always straightforward and easy to understand, and a slider &mdash; showing financing options and the cost of a house or car or initial downpayment &mdash; would visualize these options.

{{< vimeo id="225683979" caption="Without a slider: A loan calculator doesn’t necessarily need a slider. Segmented control, smooth animations and accordions at work in <a href='https://www.ingdirect.com.au/home-loans.html'>ING Bank’s “Home Loans Comparison” tool</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99edfdbd-10cf-454a-9046-45985e1f7cd6/ingbank.gif'>Animated GIF</a>, <a href='https://player.vimeo.com/video/225683979'>Watch video in HD</a>)" >}}

{{< vimeo id="225684748" caption="With a slider: <a href='https://www.wealthsimple.com/en-ca/'>Wealthsimple</a> has a lovely slider indicating investment projections. In fact, online banking is a very common milieu for slider controls." >}}

In general, every time you’d like to **add a “fuzzy” filter** to your interface or **indicate relationships** between options, a slider is an option worth considering. However, a slow clunky slider is way more frustrating than a predictable, generic set of buttons. To be effective, a slider has to be very easy to manipulate, and it has to respond to changes quickly and continually. This requires a very thorough study of the appearance and interaction design of the absolutely perfect slider &mdash; and its main building blocks, of course. Luckily (or unluckily), sliders have many facets, and plenty of decisions can (and, therefore, eventually will) go wrong.

{{% feature-panel id="vitaly-friedman" %}}

## The Many Facets Of Sliders

Although a slider seems to be a very simple component, it comes in surprisingly many facets and shapes. Now, every slider has a **thumb** (also called _handle_ or _knob_) and a **track**, which the customer can slide over. As a slider’s value changes, usually the portion of the track between the lower-bound value and the position of the thumb fills with color. Because sliders always control _something_ &mdash; be it a single value or a range of values, a pricing tier, a position in 3D space, the level of fidelity of a map, etc. &mdash; that something has to be visualized and announced somehow, and its changes will probably trigger some changes in the interface as well.

{{< vimeo id="225596254" caption="The classic: Netflix’ video player has a large enough thumb, which increases in size on hover, providing visual feedback, a thick track and a thumbnail preview." >}}

Quite unsurprisingly, a horizontal slider resembles a timeline or, to be more specific, an audio or video player track, and in many situations, that’s exactly the mental model that we could be tapping into when designing our interfaces. The mechanics of a video player component are well known, and it makes sense to use this established pattern when making small and big decisions about the aesthetics and interaction design of a slider.

<figure><a href="https://www.lloydsbank.com/loans/personal-loan.asp"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c524de26-cc82-4d20-850c-8dac48a0450b/lloyds-large-opt.png" width="800" height="502" alt="Lloydsbank sliders" /></a><figcaption>Not much different from a video player slider: <a href="https://www.lloydsbank.com/loans/personal-loan.asp">Lloyds Bank loan calculator</a>, with labels, steppers, input value and a large enough thumb for comfortable tapping. Well done. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff33e8cf-9810-4844-820d-bd96163ee20c/lloydsbank-sliders-large-opt.png">View large version</a>)</figcaption></figure>

That means that, just like in a video player, the ranges should be clearly labelled, and the current value should be clearly visible. If we choose to display a thumbnail or preview or detail view, it should appear above the slider, and as the user slides from left to right, the track should fill like a tank (for example, its color should change). If the slider acts as a filter, then only the selected range on the track would be filled, of course. (The only exception would be a slider that accepts "negative" values as well: in that case the track should be filled from the center (`0`) to the thumb, clearly showing that the default value is located in the middle.)

Because there aren’t really many established conventions for the design of slider components, many questions have to be answered by designers. If you look at the [Lloyds Bank’s example](https://www.lloydsbank.com/loans/personal-loan.asp) above, you’ll find that the thumb has an icon indicating dragging. Though not very common, the icon clearly indicates affordance &mdash; that is, the possibility of action on the thumb. Adding a visual indicator might not be necessary, but it does raise a question: If you were to add a **visual indicator on a thumb**, what icon would you choose? After all, there are plenty of options: arrows pointing left and right, greater-than and less-than symbols, a custom thumb image, a rectangular handle?

<figure><a href="https://www.santanderconsumer.no/billan-og-fritidslan/sok-billan/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/768f31cd-36f1-4ab8-8ec6-d0edd712c45b/santander-transitions.gif" width="" height="" alt="" /></a><figcaption><a href="https://www.santanderconsumer.no/billan-og-fritidslan/sok-billan/">Santander loan calculator</a> with arrows used on the thumb. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5edea7b-ebc2-4ac8-ac06-25e866fec5a7/santdander-slider-large-opt.png">View large version</a>, <a href="https://player.vimeo.com/video/225727600">Watch video in HD</a>)</figcaption></figure>

As it often turns out in user observations, it doesn’t seem to matter that much. However, some users can be confused when they discover an arrow pointing in one of the directions as they feel that the handle can be dragged only in one direction. What to choose then? Personally, we’d probably go with Lloyds’ dragging icon or a large enough circular knob.

<figure><a href="https://nextfinance.no"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/636cae0e-d122-41b9-bdee-9f2686d26359/nextfinance-slider-800w-opt.png" width="" height="" alt="" /></a><figcaption><a href="https://nextfinance.no">Nextfinance.no</a> with brackets indicating the direction of movement. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b380a52f-a342-4387-93e8-6f7fc4b87f06/nextfinance-slider-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://instabank.no/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a22a7663-e276-4b18-80b5-53b54563dd8c/instabank-slider-800w-opt.png" width="" height="" alt="" /></a><figcaption><a href="https://instabank.no/">Instabank.no</a> with an arrow pointing to the right. A green thumb alone without an arrow might be less confusing. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9ff4b0a-1932-4ce3-bab7-fe5c39563446/instabank-slider-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://littlebigdetails.com/post/67368326403/turntablefm-the-subscription-model-has-a-slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/482c2b19-fc83-4b3a-af89-b22559439bfc/turntable-monkey-opt.png" width="800" height="" alt="Turntable.fm uses a monkey as a replacement for the slider’s thumb" /></a><figcaption>On Turntable.fm (now offline), the subscription selection had a slider that turned the monkey from content to ecstatic, depending on how much the customer wanted to pay. Unfortunately, the service isn’t available any longer. (Image: <a href="https://littlebigdetails.com/post/67368326403/turntablefm-the-subscription-model-has-a-slider">Little Big Details</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d95f22d-e81b-4d4a-aa72-cae3bcb6a67c/turntable-gold.gif">View large version</a>)</figcaption></figure>

### Single, Continuous Sliders

Now, if the main goal of a slider is to choose a single value from a range of values (for example, a mortgage calculator spanning up to 20 years from now), then we can use a **single, continuous slider**. One thumb and one track to rule them all. For example, almost every single 360-degree-view slider would be a single continuous slider. The position of the thumb on the track would indicate the current value, and this value would be updated as the user slides over the track. To help the user navigate the range of values, we’d probably need to indicate the minimum and maximum values on the slider as well. That’s certainly no groundbreaking news at this point.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/394656b9-ebf1-4eb8-b5ee-4f3c157d1fee/360degree-view.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/394656b9-ebf1-4eb8-b5ee-4f3c157d1fee/360degree-view.gif" width="686" height="" alt="360-degree" /></a><figcaption>Slider matters: How would you rotate the bill with the keyboard alone? <a href="https://www.thenewfiver.co.uk/">The New Fiver</a>, <a href="https://www.bankofcanada.ca/banknotes/banknote150/">Celebrating Canada’s 150th</a>.</figcaption></figure>

If we want to encourage users to explore various discrete positions or perspectives, a slider can help nudge users to these specific positions. It also provides a clear indication of what to do and allows for interaction with the keyboard. While “[Celebrating Canada’s 150th](https://www.bankofcanada.ca/banknotes/banknote150/)” looks very appealing, it’s not as accessible as [The New Fiver](https://www.thenewfiver.co.uk/). How would you rotate the bill with the keyboard alone?

{{< vimeo id="225729602" caption="A set of single, continuous sliders on the <a href='https://www.nytimes.com/interactive/2014/upshot/buy-rent-calculator.html'>New York Times’ buy versus rent calculator</a> &mdash; allowing the customer to explore thousands of options quickly. Notice how all values can be edited manually as well." >}}

A single slider is common in cases when we don’t expect users to provide a very specific input. It’s almost like a way out &mdash; an option to provide a more relaxed, “close enough” estimate as input. For a mortgage calculator, instead of stating “If I wanted to finish pay off by 15 November 2020, what would my monthly payments have to be?,” a customer can choose “If I wanted to finish paying off by late 2020, what would my monthly payments have to be?” Why does it matter? In this case, the input doesn’t require specificity, but requiring specific input makes it more difficult to consider various scenarios quickly. Jumping to exact dates requires making slow, exact decisions with every variation considered, and that goes against the purpose of the slider, which is to explore options quickly.

{{< vimeo id="225595945" caption="A single, continuous slider from <a href='https://www.zillow.com/mortgage-calculator/house-affordability/'>Zillow’s Affordability Calculator</a> &mdash; allowing the customer to explore various options quickly. Fixed values, such as annual income, monthly debts and down payment are defined once." >}}

The same goes for a project timeframe estimator in corporate settings. A single slider would nicely map with the timeline all the way until the deadline. Based on the input, a slider could also automatically display milestones that need to be achieved to complete that goal. That’s not something you can elegantly accomplish with a group of buttons or dropdowns.

### Single, Discrete Sliders

If continuous sliders allow customers to change the values on a slider continuously, discrete sliders allow only for predefined sets of values to be chosen. For example, you might be offering only a couple of predefined mobile data plans, rather than “choose any amount you like” kind of data. In such a case, a discrete slider could nicely present available options.

<figure><a href="https://www.yota.ru/voice/#/tariff/1500min"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06a7779f-b04d-412b-9eba-e60a042344b2/yota-phone.gif" width="800" height="563" alt="Yota.ru mobile plan calculator" /></a><figcaption>On <a href="https://www.yota.ru/voice/#/tariff/1500min">Yota.ru</a>, you can select one of the five predefined options. Notice the smooth transition between options and the short navigation in the beginning to indicate that the slider is draggable. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/06a7779f-b04d-412b-9eba-e60a042344b2/yota-phone.gif">View large version</a>)</figcaption></figure>

Some discrete sliders don’t provide a smooth (continuous) transition between states. As a result, navigating between values on, say, [Postbank Property Financing slider](https://www.postbank.de/privatkunden/baufinanzierung.html) might feel a bit laggy because the position on the track never actually follows the mouse pointer, but it’s clear that only a few predefined values are accepted.

<figure><a href="https://www.postbank.de/privatkunden/baufinanzierung.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135009bc-36ca-41e4-a030-603f296b46fe/postbank-credit-lag.gif" width="800"  alt="Single discrete slider on Postbank" /></a><figcaption>A discrete slider that allows users to dock to specific values on <a href="https://www.postbank.de/privatkunden/baufinanzierung.html">Postbank Property Financing slider</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135009bc-36ca-41e4-a030-603f296b46fe/postbank-credit-lag.gif">View large version</a>)</figcaption></figure>

A quick note: If you have just a handful of options, then you’ll need to actively consider why you’d choose a slider over a set of radio buttons, for example. In general, the fewer the options, the less likely a slider would be a good choice. We’ll discuss this a bit later in detail.

### Double or Dual-Point Sliders

Choosing just one value with a slider might not be enough in some scenarios, though. If we wanted to help users filter out irrelevantly priced items in an online shop, we would need to scope the results. We could just create two sliders &mdash; one for the minimum value and one of the maximum values. That’s not necessary, though. Instead, we can use a **double, continuous slider** (also called a _dual-point slider_), with two thumbs, indicating the lower and upper boundaries of the range, respectively. Just like with a single slider, we would probably use labels to indicate a minimum and maximum value on the slider’s full range.

{{< vimeo id="225596296" caption="By its nature, a slider is a great option for any interaction related to a timeline. This transaction viewer, which allows customers to adjust the handles on the date range to show transactions from those dates, is courtesy of <a href='https://twitter.com/willjohnsnow/status/885060497397227520'>Will Snow</a>." >}}

{{< vimeo id="225683959" caption="For its double slider, <a href='https://www.hipmunk.com/flights?newFlights=true#f=FRA;t=BCN;d=2017-07-21;r=2017-07-23'>Hipmunk</a> uses icons for departure and landing to indicate a departure range. Notice how the slider doesn’t just refresh results, but visually filters out options." >}}

In fact, every single **price range filter** is a double slider at its heart. However, you might wonder why you do not find it in many retail stores. The reason is the speed of selection. Especially with price filtering, users often want to be more precise than they can easily be with a slider &mdash; mostly because sliders are often tucked away with other filters (such as size, brand, features, color) in the sidebar, leaving the main content area for the product display. A price range slider just doesn’t yield the same input speed as input values and a set of predefined price ranges in smaller sizes.

<figure><a href="https://www.zoopla.co.uk/for-sale/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/468f9d28-d834-413d-b8ac-5da05969ae3a/zoopla-price-range-800w-opt.png" width="800" height="529" alt="zoopla-price-range" /></a><figcaption>The real-estate search website <a href="https://www.zoopla.co.uk/for-sale/">Zoopla.com</a> doesn’t use sliders. On most real-estate websites, the price range is defined with input fields. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22a251ab-f755-4fc1-af1e-6a001ff7e94f/zoopla-price-range-large-opt.png">View large version</a>)</figcaption></figure>

If the user doesn’t have to be specific in their input, then it’s not really necessary to use a dual slider for a price or duration of a flight. Kayak uses a single slider when the user is [exploring options](https://www.kayak.com/explore/FRA) but uses dual sliders when the user is [searching for a specific flight](https://www.kayak.com/flights/FRA,nearby-BCN,nearby/2017-07-20/2017-07-22). For a single slider, the input is interpreted as the maximum value that’s still acceptable. Notice that taps on the track are disabled: It’s possible to only manipulate the handles of the slider.

<figure><a href="https://www.kayak.com/explore/FRA"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b57c60ba-a839-4c7e-8afc-583f8a7c3513/kayak-slider.png" alt="Kayak’s Flight Search Results" /></a><br /><a href="https://www.kayak.com/flights/FRA,nearby-BCN,nearby/2017-07-20/2017-07-22"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb31b0c3-9154-47f5-91ea-f49d50590ea2/kayak-sliders-opt.png" alt="Kayak’s Flight Search Results" /></a><figcaption>The design of <a href="https://www.kayak.com/flights/FRA,nearby-BCN,nearby/2017-07-20/2017-07-22">Kayak’s filters</a> are adjusted based on user intent: a single slider for exploration, a dual-slider for filters. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b57c60ba-a839-4c7e-8afc-583f8a7c3513/kayak-slider.png">View large version: single slider</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3283aa4-5b5b-4d43-9732-ea32d4a59302/kayak-slider-2.png">View large version: dual slider</a>)</figcaption></figure>

In fact, while most slider controls tend to be either single or dual, what if we combined both dual and single sliders into one? On the first tap, the user would select a single value, indicating a way to define a range as well. Another tap would prompt a change of the value, while dragging the slider would create a range of values.

### Discrete Sliders

A slider with “min” and “max” labels alone leaves a bit too much room for interpretation. Of course, the selected value on the slider would appear above the thumb as users slide it, but if there are no “landmarks,” then the interaction is nothing but a boring guessing game &mdash; a bit further to the left or a bit further to the right to hit just the right price point? Even though the input is likely to be fuzzy, it has to be **predictable enough** to define the boundaries of the fuzziness easily.

Defining a price range without tick marks predictably and precisely could be quite difficult, especially if the scale isn’t linear. Notice that on [Hotpads.com](https://hotpads.com/san-francisco-ca/apartments-for-rent/map?price=800-2400), although the price range goes up to $7,500, the middle value on the track is $1,800\. Adding presets and tick marks could be helpful here.

<figure><a href="https://hotpads.com/san-francisco-ca/apartments-for-rent/map?price=800-2400"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e50f4797-a8d3-4988-a294-7beb0f670647/hotpads-800w-opt.png" width="800" height="503" alt="hotpads" /></a><figcaption>Defining a price range from $1,350 to $1,550 is more difficult than necessary. That’s a sign that the scale might need to be reconsidered. (<a href="https://hotpads.com/san-francisco-ca/apartments-for-rent/map?price=800-2400">Image source</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee6fba5c-f95b-4c90-8786-35e4be117aff/hotpads-large-opt.png">View large version</a>) (<a href="https://player.vimeo.com/video/225596778">Watch HD video</a>)</figcaption></figure>

The situation appears to be even more difficult on [UBS Hypothekenrechner](https://www.ubs.com/ch/de/swissbank/privatkunden/hypotheken/hypothekenrechner.html#2040000,100000,90000,6.5), where labels are missing entirely. How can the customer know what they are sliding over and know how precise they should be? It’s not really a big deal because the user is exploring values anyway, but they would need to orient themselves first. In such a case, some users would be more likely to use manual input than to start sliding.

<figure><a href="https://www.ubs.com/ch/de/swissbank/privatkunden/hypotheken/hypothekenrechner.html#2040000,100000,90000,6.5"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1eecc7ff-dc37-47b3-9b48-3940e3c66dfd/ubs-sliders-800w-opt.png" width="800" height="1026" alt="ubs-sliders" /></a><figcaption><a href="https://www.ubs.com/ch/de/swissbank/privatkunden/hypotheken/hypothekenrechner.html#2040000,100000,90000,6.5">UBS Hypothekenrechner</a> leaves too much open to interpretation. Notice that both the thumb and the track have very small padding, and only the handle is draggable. It makes the slider difficult to use. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90b4bda0-69dd-4138-8581-d99e84a6b918/ubs-sliders-large-opt.png">View large version</a>)</figcaption></figure>

Therefore, for both single and double sliders, it’s usually a good idea to add a few distinct predefined values (the trusty **tick marks along the slider rail**) that customers can easily snap (or “dock”) to. If every tick mark is clearly labelled, then tapping on each tick mark should change the value accordingly. And even if users don’t tap on these labels, seeing them helps to orient users _within_ the slider. Not so surprisingly, sliders with discrete labels are called “discrete” sliders.

As you probably spotted above, most discrete sliders are continuous as well. As we saw in [Postbank’s Property Financing slider](https://www.postbank.de/privatkunden/baufinanzierung.html), some implementations allow users to snap only to preselected, predefined values. By their nature, such sliders don’t feel snappy and just aren’t as engaging as continuous sliders. If you happen to have a scenario where they seem to be necessary &mdash; for example, for product ratings &mdash; that’s usually a warning sign that something isn’t quite right.

## “That Slider Doesn’t Belong Here”

Have you ever patiently observed users navigating a page with a slider control? Once you do, you are likely to make quite an astonishing discovery: It doesn’t matter how boring or exciting your UI components are on the page &mdash; nothing can compete with a good ol’ accordion and a good-lookin’ slider. In fact, when your users notice a slider control, a remarkable number of people will navigate towards the slider to “try it out” &mdash; grabbing the thumb and sliding it across the track to see what happens. Apparently, **interactive elements do matter**. We would observe it over and over and over again, on various websites representing various industries.

### Sliders Always Indicate Inclusion or Progress

Knowing that, then using a slider sounds like a catch, right? So, should a slider be preferred over everything else? Not really. The main problem we keep running into with sliders is the mismatch of expectations and the slider’s appearance. As designers, we might not think about it thoroughly, but for users, every value within a slider also indicates either **inclusion, progress, growing size or increased intensity**. If a slider has five predefined values and the user picks the third one (either by tapping on the label or by sliding towards it), there is a common expectation that the two options preceding the chosen one (to its left) will be _fully_ included in that third option as well. Sounds obvious, right? Well, this has some important practical implications.

Whenever the slider is manipulated from left to right, it’s important to keep in mind that the final value should have a relationship to preceding values. This is quite self-explanatory when you’re dealing with a better, more expensive service or a higher price point, but it gets confusing when a higher pricing plan communicates lower waiting times or a cheaper total price. Instead, it’s better to reframe the message by communicating “faster processing time” and “more or better savings.” In fact, in interviews, users often **compare a slider with a volume control** or an air-conditioning knob: The further the thumb is away from its initial position, the more, the faster, the better or the higher the value should be. One direction, with related values “growing” from left to right, is just more reliable.

On [UPC.ch](https://www.upc.ch/de/kombi-angebote/selber-kombinieren/), a radio button for the “Basic TV” and “Horizon TV” selection might be more obvious than a slider. Also, the filling of the track is a bit confusing because the track should always be filled up to the thumb.

<figure><a href="https://www.upc.ch/de/kombi-angebote/selber-kombinieren/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c43abee9-eb81-44af-af1b-30e322937f83/pricing-slider.gif" width="800" height="" alt="pricing-slider" /></a><figcaption>Sometimes a slider isn’t the right choice. On <a href="https://www.upc.ch/de/kombi-angebote/selber-kombinieren/">UPC.ch</a>, some users might be confused about the “Basic TV” and “Horizon TV” selection. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c43abee9-eb81-44af-af1b-30e322937f83/pricing-slider.gif">Large view</a>)</figcaption></figure>

In these cases, a set of checkboxes (for filtering) or mutually exclusive radio buttons (for selecting one size, as on a product page) might work better. Besides, if radio boxes are styled as labelled boxes, then your interface will be ready if some of the sizes go **out of stock**. To display “out of stock” with a slider, we would need to disallow a jump to some values and “jump over” these values to the available ones automatically. This might be quite confusing.

At this point we're probably assuming that the direction of the slider &mdash; be it progress or intensity &mdash; should be flipped upside down with a right-to-left interface. Indeed, that’s the case in many banking interfaces in Arabic world, but it’s not necessarily the rule in all of them.

<figure><a href="https://www.bankboubyan.com/ar/personal-finance-calculator/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/867c88f7-7e7a-470e-8f9c-279eafcb60a6/boubyan.gif" width="800" height="" alt="pricing-slider" /></a><figcaption><a href="https://www.bankboubyan.com/ar/personal-finance-calculator/">Boubyan Bank</a> (Kuwait) with values increasing from left to right.</figcaption></figure>

<figure><a href="https://www.anb.com.sa/Default.aspx?tabid=752&language=ar-SA"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9858e01-834c-4167-bd1e-b039c85beca2/anb.gif" width="800" height="" alt="Loan calculator slider" /></a><figcaption><a href="https://www.anb.com.sa/Default.aspx?tabid=752&language=ar-SA">Arab National Bank</a> with values increasing from left to right.</figcaption></figure>

<figure><a href="https://www.emiratesnbd.com/en/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d185a2f-8c14-48f0-a011-643d9f0a6607/emirates.gif" width="538" height="492" alt="Emirates NBD" /></a><figcaption><a href="https://www.emiratesnbd.com/en/">Emirates NBD</a> (UAE) with values increasing from right to left, as expected.</figcaption></figure>

### Sliders Are Not Optimal for Limited Options

It’s important to note that whenever only a few options are available, using a discrete slider to make a selection might feel a bit awkward. [Congstar’s prepaid plan builder](https://www.congstar.de/prepaid/prepaid-wie-ich-will/prepaid-karte/) provides only a few options. Just like in the previous example, radio buttons might be a better option, especially for the “Datenturbo” feature (which is basically an on/off toggle, but has to be operated as a slider).

<figure><a href="https://www.congstar.de/prepaid/prepaid-wie-ich-will/prepaid-karte/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c68b4150-9d33-4ccc-96f4-12e4cc9a62cb/congstar-sliders.gif" width="800" height="" alt="congstar-sliders" /></a><figcaption>Sometimes sliders aren’t really necessary: <a href="https://www.congstar.de/prepaid/prepaid-wie-ich-will/prepaid-karte/">Congstar’s prepaid plan builder</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c68b4150-9d33-4ccc-96f4-12e4cc9a62cb/congstar-sliders.gif">View large version</a>) (<a href="https://player.vimeo.com/video/225622537">Watch HD video</a>)</figcaption></figure>

While a single slider with a few available options feels awkward, it would be very frustrating to use in cases when the selection is very limited. Neither is a slider a good option if inclusion or progress or emphasis aren’t applicable to the problem you are solving. (It’s interesting that image galleries and carousels, which actually use the same metaphor of moving forward on a track of images and often even look similar to slider controls, usually aren’t used as much as “original” slider controls. Maybe that’s also because they often don’t convey any sense of inclusion or progress, and they appear to be placed in the carousel randomly.)

### Value Change Should Be Displayed Prominently

Because the main point of interaction with an slider is to display options quickly, it’s critical to **display the actual value or change right away**, without prompting the customer to actively select an option or click on a button first. The [cash loans calculator](https://www.zaba.hr/home/en/financing/cash-loans?idR=61&atr187=22.000&atr188=EUR&atr189=2&atr190=40&pr1=8&pr2=433&pr3=5) on Zagreb Bank includes both numerical value input and a slider (displayed on hover) to manipulate the value, but the user has to click on “Show options” to actually see the options. Displaying options right away would be better &mdash; otherwise, the slider wouldn’t really serve any purpose except perhaps to try to engage the user.

{{< vimeo id="225727616" caption="Displaying the actual value or change right away is critical. Having to click on “Show options” shouldn’t be necessary. (Source: <a href='https://www.zaba.hr/home/en/financing/cash-loans?idR=61&atr187=22.000&atr188=EUR&atr189=2&atr190=40&pr1=8&pr2=433&pr3=5'>Zagreb Bank’s cash loans calculator</a>)" >}}

[Deutschebank Service calculator](https://www.deutsche-bank.de/pfb/content/pk-service-rechner-und-tools.html#layer-43115), on the other hand, uses a slider control as input for the number of children in a household, and prompts a number pad to edit the value inline. A plain input field is probably a better option here.

{{< vimeo id="225622588" caption="A slider doesn’t belong here (nor do dropdowns for the year input). (Source: <a href='https://www.deutsche-bank.de/pfb/content/pk-service-rechner-und-tools.html#layer-43115'>DeuscheBank Service Calculator</a>)" >}}

Whenever one of the conditions isn’t really fulfilled, it’s probably a sign that a slider isn’t a perfect fit to solve the given problem. However, if it does make sense in your context, then you’d have to make a good number of design considerations to find the optimal solution for your design.

## Slider Design Considerations Checklist

So, what do we need to keep in mind when designing that perfect slider? Once we understand the problem we are solving, here are the questions we could ask ourselves next:

*   Is a slider the right solution for this problem, or should we use radio buttons or checkboxes instead?
*   How much **space can we afford** for the slider, and how do we make it work well on small and large screens?
*   Do we use a single or double slider?
*   Should the slider be **continuous or discrete**?
*   How do we design the **thumb**, the track and the labels?
*   How do we choose the **slider scale**: linear or non-linear?
*   How many tick points do we need, and how do we design them?
*   How do we label the lower and upper boundaries of the slider?
*   What icon do we use for the thumb, if any?
*   How and where do we display the current value?
*   Should the slider be complemented with a precise input (for example, an input field)? If yes, how do we indicate that a numeric input is **editable**?
*   Do we need any frequently used values or value ranges as presets to nudge users to the “best” options?
*   How do we indicate **availability** to avoid dead ends?
*   How should the slider track change with thumb movements?
*   With a double slider, what happens if the user moves the end thumb over the left thumb, or the other way around? What happens if the user taps or **clicks on an area between two thumbs**? Should the UI adjust the lower or the upper boundary? Or should this action be disabled altogether?
*   Are there any values on a slider that shouldn’t be accepted?
*   Should we accept ranges that have too many or too few options?
*   Should the user be able to **restore previous states** of their manipulation of the slider?
*   Should we add **animations or transitions** to the interaction as well?
*   What and how do we announce to a **screen reader**, and what do we need to keep in mind in terms of accessibility?
*   Do we have **interdependent sliders**, where a slider’s input depends on previous input? Should users be able to "lock" some values?

Again, not many straightforward answers to these seemingly innocent questions. Now that we know the building blocks of the slider, let’s take a closer look at all of the design decisions listed above step by step.

## The Rules Of Thumb For Spacing

While, as designers, we tend to dedicate a large portion of screen real estate to images and videos and galleries and carousels, sliders are often tucked away in sidebars and toolbars, primarily because they are supposed to act as filters, and so they are **placed next to other filtering options** that usually don’t need that much space, such as humble checkboxes and accordions. Admittedly, sliders do get a well-deserved spotlight in calculators and “builders,” but those are relatively rare.

{{< vimeo id="225596230" caption="Spacing issues: The slider on <a href='https://www.semanticscholar.org/search?year%5B%5D=2009&year%5B%5D=2010&q=Deep%20Learning&sort=relevance&ae=false'>Semantic Scholar</a> provides presets for quick filtering, but interacting with the slider is quite painful unless you zoom in three or four times. A slider needs space to make the sliding experience effortless." >}}

To be effective and easy to manipulate, sliders need space, a lot of space actually &mdash; but most importantly a lot of horizontal space. The thumb has to be large enough and the track has to be wide enough to jump to the tick marks. It’s going to be very difficult to make the exploration of options comfortable if a slider is around 200 to 300 pixels in width, tucked away from the main content area. Now, how do we translate that to general rules of thumb when designing a slider, then?

<figure><a href="https://fonts.google.com/?stylecount=12"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa89e3f1-6e04-447b-9a1d-9162d497e938/google-fonts-slider.gif" width="800" height="" alt="" /></a><figcaption>On <a href="https://fonts.google.com/?stylecount=12">Google Fonts size slider</a>, getting the value just right is difficult. This might be not the main point of interaction, but turning the value label into an input field on tap would help. A wider slider would help, too.</figcaption></figure>

An important variable that has a strong impact on spacing requirements is the number of “critical” tick marks on the slider. These are the marks that stand for important thresholds, be it an average price point or a budget threshold. The more critical tick marks you need to display, the more space a slider will need. Because the slider will have to be responsive as well, the spacing between these tick marks has to be large enough to not require too much precision.

<figure><a href="https://www.trulia.com/house-affordability-calculator/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7be3e486-66d1-4776-a9ce-fd0712ef8b4f/trulia-affordability.gif" width="800" height="" alt="Trulia Affordability Calculator"></a><figcaption>Trulia’s <a href="https://www.trulia.com/house-affordability-calculator/">house affordability calculator</a> provides a nice visualization of spending and thoroughly informs customers about their options. The padding on the thumb and on the track could be enlarged a tiny bit though. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7be3e486-66d1-4776-a9ce-fd0712ef8b4f/trulia-affordability.gif">View large version</a>) (<a href="https://player.vimeo.com/video/225597162">Watch HD video</a>)</figcaption></figure>

So, how large is large enough? If you can ensure that the horizontal spacing between critical tick marks is at least 65 pixels &mdash; on narrow and wide screens alike &mdash; that’s probably a good amount. And then there is the actual thumb and getting comfortable padding around it, so that the thumb is easy to grab and move across the track. In general, experiments show that making the thumb at least **32 × 32 pixels (rectangular or circular), with `3vw` or `1.5vmax` padding** (the former on narrow screens, the latter on wide screens) around it, seems to work fairly well. In fact, just from going through dozens of slider implementations, we see that the most usable ones hit that sweet spot well.

Now, the numbers above might feel like **magic numbers**, and to some degree that’s true: they’ve been discovered empirically by looking into sliders that appear to be more comfortable for users. It’s not that these numbers are always just right, but they give you a good enough estimate of the size that might work best.

You might be wondering why the padding is defined in `vw` and `vmax` units, rather than, say, pixels or percentages. The larger the area to traverse to hit the thumb, the larger the padding should be. In the worst case, traversing would need to happen from the edges of the viewport, and if we set padding in `vmax`, then it will always be large enough to hit the target easily. Instead of tying the padding to the width of the container, it feels more reliable to connect it with the actual viewport’s width or height. On narrow screens, where tapping is to be expected, `3vw` seems to be enough, but on desktop, you might be better off dialing the padding to `1.5vmax`.

So, what does this mean? Well, if you want to design a (single or dual) slider that works well at a 400-pixel width on narrow screens, then the considerations above would **limit the number of critical tick marks** in your budget. In fact, you’d be able to accommodate at most five items comfortably &mdash; anyway, this will usually be more than enough to display critical options. The math speaks for itself:

<pre class="language-js"><code>(400px - 32px - [(3vw * 500px) * 2]) / 65px =
(400px - 32px - (12px * 2)) / 65px =
344px / 65px =
5.29</code></pre>

Again, please do take these values with a grain of salt: We didn’t run any studies on the various sizes of the handle and its padding; we just determined these values experimentally, and tend to use them as a shortcut for better decisions. What works in one case might not work in another, but this might give you an idea of how to start designing that perfect slider.

<figure><a href="https://kontist.com/einkommensteuer-rechner-selbststaendig/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a831aa63-9790-42a0-9809-e3bbd0f6a345/kontist-tax-calculator.gif" width="800" height="" alt="" /></a><figcaption>Now, that’s a nice looking slider. Both on narrow and large screens, the padding is generous enough for comfortable and effortless movements. It’d be great to be able to enhance the slider by adjusting the value as an input element, though. (Image: <a href="https://kontist.com/einkommensteuer-rechner-selbststaendig/">Kontist.com Tax Calculator</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a831aa63-9790-42a0-9809-e3bbd0f6a345/kontist-tax-calculator.gif">View large version</a>) (<a href="https://player.vimeo.com/video/225597252">Watch video in HD</a>)</figcaption></figure>

Now, what about the **responsive behavior of that layout**? Obviously, the spacing between tick marks would scale down with narrower viewports. Because we are designing with viewport units in mind, grabbing the thumb and moving it will still work well. But moving between discrete values could become more difficult unless you start dropping a few tick marks and “widening” the scale artificially. Alternatively, it might be worth look into adjusting the number and the position of tick marks, and including slightly **different scales on narrow and on wide screens**.

On larger screens, eventually you would need to set a **maximum width** on the slider as well, because, otherwise, the area to traverse would be too large. Again, the fewer the tick marks, the less space a slider needs to remain usable.

Once we know the spacing constraints, we can design the slider around it. First, we need to position the labels for tick marks and choose the slider’s scale.

## Displaying Tick Marks And Current Values

Here’s a tricky question: Should tick marks be placed **above or below the slider track**? The question might sound obvious because sliders usually display marks below the track (not unlike school rulers), but would it be your first choice if you had to design it from scratch?

Let’s assume that we have plenty of tick marks to be placed on the track of a slider. If we displayed those marks very close to the track (above or below), then the label would definitely be obscured by the handle once the user slides over to that value. We could **space out the label vertically** and add a subtle vertical line indicating a connection between the value and its position on the slider.

For example, [SGS’ housing cost calculator](https://particuliers.societegenerale.fr/emprunter/simulateurs/votre_pret_immobilier.html) might not be the most attractive slider out there, but it does everything right. The tick marks are spaced out vertically and, as such, are easy to choose. While snapping to preselected values is easy, all values in between are accepted as well.

<figure><a href="https://particuliers.societegenerale.fr/emprunter/simulateurs/votre_pret_immobilier.html"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e10f2466-7aac-44fe-8f4d-d47a40078420/transitions-sgs.gif" width="800" height="" alt="" /></a><figcaption><a href="https://particuliers.societegenerale.fr/emprunter/simulateurs/votre_pret_immobilier.html">SGS’ housing cost calculator</a>, with tick marks, manual input and smooth transitions. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e10f2466-7aac-44fe-8f4d-d47a40078420/transitions-sgs.gif">View large version</a>) (<a href="https://player.vimeo.com/video/225684496">Watch video in HD</a>)</figcaption></figure>

That’s already helpful, but a slider never exists in isolation. And so, as we display the tick marks, we also need to display the current value (or values) prominently &mdash; either above or below the slider as well. We could also display the current value _on_ the thumb if it’s large enough &mdash; of course, if it’s not editable. What’s better? Well, the value is actually the main point of interaction, so displaying it prominently above the slider makes sense. Otherwise, if the current value is displayed below the slider, users on narrow screens might feel pressured to lift up their finger to see the value. In general, both options could work &mdash; we just need to make sure that we space out labels well enough.

But what if your interface contains a set of sliders &mdash; for example, a slider that adjusts brightness and contrast, RGB/HSB triplets, or a vertical equalizer? How would you display current value then? Well, in that case we have to distinguish between current values of each slider, and the final computed value. Obviously, the final value should be more prominent than each of the slider’s values. However, we need to ensure that it’s the main focus of interaction: so on narrow screens, for example, that value could be displayed in a floating fixed bar, following gradual slider adjustments.

In general, it seems to be a good idea to **position tick marks below the track and position value labels above the track**. And if your slider doesn’t have any tick marks (for example, in a price range filter), then placing the value labels [above the track seems to be a bit more resilient](https://www.nngroup.com/articles/gui-slider-controls/) &mdash; because the view would never be obscured by a floating finger.

## Choosing The Slider’s Scale

The positioning of labels is one thing, but picking a scale to accurately reflect the range of options is another. If your clothing store has hundreds of items, with prices ranging from $50 to $15,000, how exactly would you design the scale for your slider? What value would you position in the middle of the slider? What if most items are priced around $80, and exactly one item is priced at a remarkable $15,000?

By default, we’d assume that a proper slider scale should be linear, breaking down the entire range into a set of equidistant segments. However, in the case above, it would mean placing $7,500 in the middle of the slider. That would be highly ineffective, though, because 50% of the track would be used to control 1% of the products. Not only that, but choosing the desired range of values would become unnecessarily difficult, and if most products are in the $50 to $300 price range, then 5% of the track would be used to control 50% of all products. In other words, large portions of the slider would represent no change in the filtering, and small portions would represent huge changes in the filtering.

[Disneystore.com](https://www.disneystore.com/disneystore/product/category?offset=&priceRangeLower=7&priceRangeUpper=1028&sortKey=&productDims=1000295) has a couple of issues. Not only is the slider space very narrow, but selecting the price range between $800 and $1000 requires impeccable precision. When one of the values is selected, the entire page is blocked, and the user is automatically scrolled to the top of the page. This doesn’t encourage exploration. Adding manual text input or changing the scale could help here.

{{< vimeo id="225591616" caption="Choosing an appropriate price range on <a href='https://www.disneystore.com/disneystore/product/category?offset=&priceRangeLower=7&priceRangeUpper=1028&sortKey=&productDims=1000295'>Disneystore.com</a> requires skillful tapping skills. Adding manual text input or changing the scale could help here." >}}

In practice, a vast majority of products are clustered in a very narrow range, with very few residing at the edges of the scale. However,, as Sigurt Bladt Dinesen [discovered](https://www.howdoi.me/blog/slider-scale.html), underlying data is rarely a uniform distribution. If the scale of your slider doesn’t account for the distribution of prices in your inventory, then providing an accurate range of values would be an extremely frustrating experience, requiring explicit precision in contexts where it shouldn’t be required.

When this happens, users would suffer through slow, intense, strained attempts to set just the right range of values before giving up and resetting the filter altogether.

As [Baymard Institute discovered](https://baymard.com/blog/slider-interfaces) in usability tests, at [Crutchfield](https://www.crutchfield.com/g_300/All-Car-Stereos.html?tp=5684), 50% of the slider’s width is used to control just 2% of the 200+ products in the list. This, in turn, makes the slider needlessly sensitive in the $50 to $300 range, where 5% of the slider’s width is used to control 50% of all products.

<figure><a href="https://baymard.com/blog/slider-interfaces"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75dbb30e-5b90-4523-8fac-3c1e0c70c637/crutchfield-slider-800w-opt.jpg" width="800" height="532" alt="crutchfield-sliders" /></a><figcaption>When the slider’s scale is linear, it can be very difficult for users to set meaningful values. Point in case: <a href="https://www.crutchfield.com/g_300/All-Car-Stereos.html?tp=5684">Crutchfield</a>. Example from <a href="https://baymard.com/blog/slider-interfaces">Baymard Institute</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fce737f-8ca4-40d4-83db-3d212b8e79fb/crutchfield-slider-large-opt.jpg">View large version</a>)</figcaption></figure>

To solve this problem, for lengthy videos, YouTube changes allows users to change the scale and jump to a specific second if they want to. The feature might be difficult to discover, because it’s indicated with an arrow pointing up, but it’s useful. The track scale doesn’t hame to remain the same permanently. Thanks to [Chazz Basuta](https://twitter.com/thisguise/status/883311422079471616) for the heads up.

{{< vimeo id="225599198" caption="YouTube allows users to dynamically adjust the scale for lengthy videos." >}}

What would be a better scale, then? Study the purchasing behavior of your customers and **find the most frequent range** for their purchases. It could be a price range, but also a mobile data plan or a mortgage payoff timeframe. That range will inform your design decision: Dedicate as much as 50 to 60% of your track to that range, with outliers residing on the edge.

You could go so far as to **create distinct clusters of ranges** &mdash; perhaps “low-cost products” (up to $50), “popular products” ($50 to $350) and “high-cost products” (above $350), assigning 20% to the outliers and 60% to the most common range. Furthermore, you could extend the slider by providing frequently used presets as buttons just below the slider &mdash; some of your customers might appreciate it.

<figure><a href="https://www.urbanladder.com/sofa-cum-bed?src=cat_2#page-2"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc6aef2f-e2e0-413d-9c44-d1ed543012b1/urbanladder-opt.png" width="640" height="715" alt="Urbanladder pricing presets" /></a><figcaption>For their pricing filter, <a href="https://urbanladder.com/sofa-cum-bed?src=cat_2#page-2">Urbanladder</a> uses pre-defined presets that users can jump to.</figcaption></figure>

You might even go further by **dynamically adjusting interval jumps** based on the pricing distribution of your products ([using histogram equalization](https://www.howdoi.me/blog/slider-scale.html) to create so-called “biased” scales). So, as new products are added to the content management system, the intervals would be recalculated, and the design would be adjusted automatically.

A slightly simpler and, therefore, often preferred alternative is to use a **logarithmic or exponential curve**, which often matches real-world data quite accurately. In this case, the fewer the products above a certain threshold, the less area would be reserved for them on the slider track.

<figure><a href="https://www.smashingmagazine.com/2014/10/inventory-based-discrete-slider/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01d5c02d-d43c-46c0-bcaa-e4157975b9f3/linear-histogram-slider-opt.png" width="677" height="214" alt="linear-histogram-slider" /></a><figcaption>A linear price slider with histogram provides more information. (<a href="https://www.smashingmagazine.com/2014/10/inventory-based-discrete-slider/">Image source</a>)</figcaption></figure>

This approach doesn’t just help users navigate the ranges on the slider, though. Because the scale heavily depends on the inventory’s distribution, rather than a linear distribution of values, it also **reduces dead ends** &mdash; frustrating no-results pages. After all, most area on the track would be reserved for the most frequently purchased items.

But what if we wanted to eliminate a no-results experience altogether? Despite our efforts, users might choose just the range that has only a few items or no items at all. Your store might not have any shirts priced below $10, for example. Or by the sheer beauty of an accident, you don’t have any items in the $40 to $60 price range. That’s where we could use an inventory count slider or a histogram slider.

## Eliminating Zero-Results Filtering

An alternative way to design a scale is by examining the inventory count from a slightly different perspective. As Greg Nudelman [suggests in his article](https://www.smashingmagazine.com/2014/10/inventory-based-discrete-slider/), we can extend the slider with discrete values based on inventory counts.

We would divide our entire inventory &mdash; say, 100 capes &mdash; into 5 intervals, and we get 20 capes per interval. Next, we scan the price range to figure out the price (rounded to the nearest dollar) that corresponds to the **approximate inventory count** of 20\. Suppose the first 19 capes cost between $0 and $60 (remember that we’re still assuming no inventory in the $40 to $60 range), the second 21 capes fall in the $61 to $65 range, and so on.

<figure><a href="https://www.smashingmagazine.com/2014/10/inventory-based-discrete-slider/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b074e5f-2fa5-42bc-ab73-998c0985823a/alternative-price-slider-opt.png" width="" height="" alt="alternative-price-slider" /></a><figcaption>The alternative price slider is based on inventory count. (<a href="https://www.smashingmagazine.com/2014/10/inventory-based-discrete-slider/">Image source</a>)</figcaption></figure>

We basically break down the entire range into segments, each with the same number of results. Hitting that unfortunate area of $40 to $60 is still possible, of course, but it is less likely to be hit than in the previous examples. If the customer’s price range is larger than that of a single 20-item interval, then they can simply select a larger interval using the dual slider.

The ultimate solution would be to **actually display the distribution of items for every price range**, as a histogram. We could reserve 50 to 100 pixels in height above the slider to display a histogram with a product count. The taller the bar in a certain range, the more items would be matched there; the shorter the bar, the fewer products would be matched there. The histogram could be used for single and dual sliders, with or without discrete values, with a linear or algorithmic scale. In fact, it could also indicate most watched moments in a video or the most common selections in a mobile data plan.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbc7cf6f-c406-49bc-832f-663362f6d518/trulia-listing-overlay-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34b38312-030b-4dd5-b28e-c8c1a61a4df6/trulia-listing-overlay-800w-opt.png" width="800" height="774" alt="trulia-listing-overlay" /></a><figcaption>Another strategy to avoid zero-results pages: showing the distribution of prices on the map as an overlay, as an enhancement for slider price ranges. Here shows the median listing price on <a href="https://www.trulia.com/NY/New_York/#map-affordability-listing-price">Trulia</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fbc7cf6f-c406-49bc-832f-663362f6d518/trulia-listing-overlay-large-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd6bb1e7-7f3b-4387-b888-1fc42bff70c9/airbnb-slider-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0c79e3f1-66a8-48d6-b197-bde5539680a1/airbnb-slider-800w-opt.png" width="800" height="482" alt="airbnb-slider" /></a><figcaption>A classic: Airbnb’s histogram slider displays the distribution of prices and the average price per night. It gives users some context of what price is acceptable for a location. Unfortunately, tapping on the track requires a tad too much precision, and the histogram bars aren’t selectable at all. (Video courtesy of <a href="https://twitter.com/lucascerdan/status/885516317176066049">Lucas Erdan</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd6bb1e7-7f3b-4387-b888-1fc42bff70c9/airbnb-slider-large-opt.png">View large version</a>)</figcaption></figure>

By providing a hint about the expected number of results, users have to actively choose to see zero-results pages. In fact, that’s exactly what Airbnb does to **eliminate dead-end searches**, which don’t yield any available apartments to rent.

## Indicating The Range Visually

When it comes to making purchasing decisions &mdash; for example, for a mobile data plan, clothing or energy consumption &mdash; each of us is a special snowflake. Sometimes we have a clear enough idea of how much mobile data would be acceptable (“I need just about 5 GB of data”); sometimes we have a fuzzy idea of how much we’d be willing to spend on clothing (“I need to find a $50-ish gift”); and sometimes we need a visual or aural aid to make an informed decision (“I don’t know how many kilowatt hours I consume monthly in my household”).

In all of these cases, users would experience the slider very differently, approaching the filtering with **different intentions**. Depending on the level of confidence in their choice, users would pick different values as boundaries for the input. The more vague a user’s idea of what they want, the more likely that desired option would need to be placed in context, ending up in the middle of the selected range. The more confident the user, the more likely that desired option would end up as the lower or upper boundary of the selection. That’s hardly surprising but quite important to understand, because although many users are purchasing items in a few specific ranges, it doesn’t necessarily mean that they filter items accordingly.

It’s interesting that, in both of these cases, while the interface forces users to specify a range of values, customers actually might have only one single value in mind. In fact, [users often have a single-point mentality](https://baymard.com/blog/slider-interfaces), and so when operating a dual slider, they might be confused because they have to select two values instead of one. According to Baymard Institute, “more than 50% of the test subjects misinterpreted dual-point range sliders for price with a single-point slider.”

The solution? When designing a dual slider, it’s a good idea to **add some visual clues to indicate that the expected input is a range of values**, rather than one single value. A simple way of doing it is by attaching arrows to the handles, pointing towards each other. The arrows suggest a direction and act as indicators for a “from” to “to” input, implying that multiple values have to be set.

<figure><a href="https://baymard.com/blog/slider-interfaces"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62639382-70af-47fa-a067-87d31325a32e/wayfair-pointers-opt.jpg" width="658" height="460" alt="Wayfair slider" /></a><figcaption>Before moving to presets, Wayfair used to have a slider with arrows pointing in opposite directions to indicate measurements. (Image: <a href="https://baymard.com/blog/slider-interfaces">Baymard</a>)</figcaption></figure>

<figure><a href="https://www.crutchfield.com/g_300/All-Car-Stereos.html?tp=5684&pg=1#&price=340-2690"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da675e70-16bf-4bd5-906c-de65590ac8d8/crutchfield-arrows-800w-opt.png" width="800" height="383" alt="crutchfield-arrows" /></a><figcaption>In their new design, Crutchfield uses arrows pointing in opposite direction to indicate the range input. (<a href="https://www.crutchfield.com/g_300/All-Car-Stereos.html?tp=5684&pg=1#&price=340-2690">Image source</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1aed46c-06d6-44c9-9e34-85257c6b6f4e/crutchfield-arrows-large-opt.png">View large version</a>)</figcaption></figure>

Another solution would be to accept both single and multiple values. So, as the user taps on a value on the slider (let’s say on $80), you could automatically interpret the selection as a filter between $70 and $90, for example, and beautifully animate the transition from a $80 pricing point (a dot on the track) to a $70 to $90 range (a filled line on the track). You could also add a little hint explaining that users can adjust a range on the slider as well &mdash; and display the number of matches, too.

## Visualizing The Output

Remember that third case in which users need a visual or aural aid to make an informed decision? In that case, it’s a good idea to use some kind of **visualization to explain the various options** and the common scenarios in which they are used. The energy plan calculator, for example, could suggest a common range for an apartment, a house or a villa &mdash; illustrating each of the options, respectively.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1674cfa2-dc0d-498a-a539-61225bd51496/house-slider.gif" width="800" height="600" alt="house-slider" /></a><figcaption>Sometimes, visual comparison helps, as with this playful house size animation by Dino Franke.</figcaption></figure>

Deutsche Bank visualizes [house financing](https://www.deutsche-bank.de/pfb/content/pk-service-rechner-und-tools.html#layer-35574) expenses and the outcome by adjusting the house preview. The further the user slides over the track, the more impressive the house becomes.

{{< vimeo id="225622645" caption="Deutsche Bank visualizes <a href='https://www.deutsche-bank.de/pfb/content/pk-service-rechner-und-tools.html#layer-35574'>house financing</a> expenses and the outcome by adjusting the house preview." >}}

For its [visualization of home renovation costs](https://www.deutsche-bank.de/pfb/content/pk-service-rechner-und-tools.html#layer-35572), Deutsche Bank uses a set of accordions and sliders. Every selection contains a detailed suggestion about the expected costs. This makes a task such as calculating renovation costs more manageable and less overwhelming.

{{< vimeo id="225854232" caption="Deutsche Bank’s lovely <a href='https://www.deutsche-bank.de/pfb/content/pk-service-rechner-und-tools.html#layer-35572'>visualization of home renovation costs</a>. Good padding on the slider’s tracks, too." >}}

[Goteborg Energi](https://www.goteborgenergi.se/Privat/Produkter_och_priser/Elhandel/Vara_avtal) uses illustrations to indicate various energy-consumption levels for an apartment, house or villa. It also uses an overlay to explain each selection as the user moves the handle. Suddenly, abstract values make sense, because they are put in context.

{{< vimeo id="225591959" caption="A <a href='https://www.goteborgenergi.se/Privat/Produkter_och_priser/Elhandel/Vara_avtal'>two-step energy costs calculator</a> helps the user find their energy consumption first, and then choose an appropriate package." >}}

As a bonus, the slider also has predefined presets located further below the slider on the page. Notice how the slider’s value changes automatically to an input field when the user reaches the upper boundary of the slider. The only drawback is that the padding around the track could be slightly increased.

## Smooth ’n’ Silky Sliding, Guaranteed!

We said it before: The main purpose of a slider in the first place is to allow users to explore options. However, if the sliding experience is slow or clunky or unexpected, then exploration will quickly become frustrating. When a user interacts with a slider, we have to make sure that the interaction is **continuous and effortless**, and that requires a close look at the interaction design of the slider.

Now, as designers and developers, we expect users to grab the handle and move it across the horizontal track. This requires their thumb to be large enough for comfortable tapping (see “Rules of Thumb” above). However, this interaction is one of the many possible interactions, and not necessarily the one that users will prefer most of the time.

An obvious enhancement beyond moving the handle would be to **allow users to jump to any value on the track**. That means that not only the thumb but also the track should have enough vertical and horizontal padding (across the track and at the edges of the track) to be tapped easily &mdash; probably as much as the thumb itself. Also, we need to ensure that the visual feedback happens both when the user interacts with the handle and when they hover over the track. That visual feedback doesn’t only have to be the change of the mouse cursor over the entire slider area, though.

<figure><a href="https://twitter.com/ma11k"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a78f59c-73d5-4722-b837-52c88e6d5a2e/enlarge-hover.gif" width="400" height="165" alt="enlarge-hover" /></a><figcaption>By default, a handle should be large enough for comfortable tapping. However, we could also enlarge the handle on hover a bit to encourage interaction. (Image: <a href="https://twitter.com/ma11k">Mike Miroshnikov</a>)</figcaption></figure>

We could also enlarge the handle, change its color, add some shadow to the handle or even change the color of the track &mdash; on `:hover`, on tap _and_ when the slider is being dragged. On `:focus`, then, we could add a box around the whole slider and change the color or shade of the thumb, or add a thick border to the thumb to indicate that it’s active. Combine that with a lovely transition or animation, and you have a recipe for a quite lovely slider! Now, compare the two implementations below, on Trulia and Housing.com.

<figure><a href="https://www.trulia.com/rent_vs_buy/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/367f0e8b-d6f7-4224-a4ed-4df39e8bfacb/trulia-sync.gif" /></a><figcaption><a href="https://www.trulia.com/rent_vs_buy/">Trulia’s rent versus buy calculator</a>, when everything is in sync. No noticeable delay and a smooth adjustment all across the track. Also, check <a href="https://www.trulia.com/mortgage-payment-calculator/">Trulia’s mortgage payment calculator.</a></figcaption></figure>

This raises another common implementation detail: As the slider is being used, some of the input can get out of sync. As Ilya Birman [reminds us](https://ilyabirman.net/meanwhile/all/slider/), the slider is usually there to control something else &mdash; a value, a range of values or a state. It’s critical to ensure that **everything stays in sync**: the cursor’s shape, the hover effects, the position of the handle, the responsive to clicking and dragging, the change in values, the change of states inside and outside the slider area.

{{< vimeo id="225684051" caption="On <a href='https://housing.com/in/home-loans/check-eligibility/customize-offers/394424'>Housing.com</a>, there is a noticeable lag following movements of the thumb: The position on the track and the value selected are out of sync." >}}

This might be easy for a designer to require in their specifications, but from the technical perspective, it might be quite difficult to achieve. For example, if the slider affects the number of matches in the database, you’d need to execute AJAX requests to get that shiny JSON file with the results and update the results page live. In fact, it might take a noticeable amount of time to fetch new results, interpret them, map them on the slider and display them. Despite all of this happening in the background, we want to achieve a smooth ’n’ silky, continuous feedback as the slider is being manipulated.

For example, [Sparkasse Dresden](https://www.ostsaechsische-sparkasse-dresden.de/de/home/privatkunden/kredite-und-finanzierungen/privatkredit.html?n=true&) has a noticeable lag between movement of the slider on the track and the calculated value (displayed at the bottom of the screen). Also, the input field allows for any value to be typed in but accepts only very specific values, without providing any feedback. Feedback matters.

<figure><a href="https://www.ostsaechsische-sparkasse-dresden.de/de/home/privatkunden/kredite-und-finanzierungen/privatkredit.html?n=true&"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/660f632b-c1b6-45dd-9940-ec5e1ae3a53c/sparkasse-dresden.gif" width="800" height="" alt="sparkasse-dresden" /></a><figcaption><a href="https://www.ostsaechsische-sparkasse-dresden.de/de/home/privatkunden/kredite-und-finanzierungen/privatkredit.html?n=true&">Sparkasse Dresden</a> has noticeable lags with interaction. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/660f632b-c1b6-45dd-9940-ec5e1ae3a53c/sparkasse-dresden.gif">View large version</a>) (<a href="https://player.vimeo.com/video/225727603">Watch video in HD</a>)</figcaption></figure>

On [Zillow’s rent versus buy calculator](https://www.zillow.com/rent-vs-buy-calculator/), there is a slight delay between changes to the slider and the graphical presentation of the outcome. However, because the values are updated right away and there is a smooth animation between the states of the chart curves, it’s hardly annoying.

{{< vimeo id="225727620" caption="Continuous feedback on <a href='https://www.zillow.com/rent-vs-buy-calculator/'>Zillow’s rent versus buy calculator</a>; the delay is almost unnoticeable." >}}

So, what would be the ultimate solution? Instead of repainting the slider only when the data becomes available, we could **repaint the slider continuously while updating results asynchronously**. In general, the slider should never freeze, even if the data is not there yet. Ilya Birman provides a [reference implementation](https://ilyabirman.net/meanwhile/all/slider/) with full continuous feedback, which is definitely worth looking into before you begin implementation.

Another problem that comes up quite frequently is the magnifying glass and text selection on mobile devices. As the user grabs the handle and moves it across the track, sometimes due to inaccuracy of the finger, the movement might be interpreted as a double-tap, prompting selection or a magnifying glass. To solve this issue, disallow events on anything that isn’t interactive to prevent annoying prompts.

## They Ought To Slide, But They Choose To Click

Jumps on a track are quite predictable if we have a single slider allowing for a single value input. But what if we have a dual slider allowing for a range input? What should happen if the user clicks outside of the specified range or somewhere in the middle of the range, rather than dragging the handle left and right?

Because we **can’t predict the intent of this interaction**, sometimes designers tend to disable clicking behavior within the specified range altogether, providing a tooltip that suggests to drag the handles instead. Now, the reason why a user would tap on a specific point inside of the range is because they want to limit the scope of the search, and that tapped value is an important representative value in that range.

<figure><a href="https://housing.com/in/buy/real-estate-mumbai?locality_info=false&search_open=true"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/238c1ac4-2cd4-4f08-8594-358693f8fdc9/housing-track-opt.png" width="782" height="1372" alt="housing-track" /></a><figcaption>What should happen when the user taps on the middle of the price range? Example: <a href="https://housing.com/in/buy/real-estate-mumbai?locality_info=false&search_open=true">Housing.com</a>.</figcaption></figure>

If that value is positioned **close enough to the lower boundary**, we could shift it to the selected value. The same goes for the upper boundary. How close is close enough? Perhaps around 10 to 20% of the track’s width &mdash; at least that seems to be a reasonable value to indicate a relationship to the boundary. It won’t work all of the time, but it might work more often than not.

Alternatively, we could **suggest a smaller range** around the tapped value or indicate that the user can actually shift the entire range across the track, preserving the scope of the range.

Now, what happens if the user chooses to click outside of the specified range? That could be an indicator that the user would like to extend the range, but it could also be an indicator that the user is interested in that particular value. The decision isn’t obvious here, but, intuitively, we’ll look into extending the ranges, rather than change the scope of the range altogether.

If the click happens outside of the left boundary, we’d extend the left boundary. If it happens outside of the right boundary, we’d extend the right boundary. Either way, adding a link to **restore the initial state** would mitigate confusion and unexpected changes.

## Enhancing A Slider With Precise Inline Editing

You might have created a beautiful slider design with an appropriate slider scale and enough padding; the tick marks are thoughtfully set; the slider responds continuously; and users can easily snap to any value on the track. Sorry to be a party pooper, but it still might be not good enough to make the experience smooth, especially if users require just a tiny bit more precision when setting values on the slider.

<figure><a href="https://www.lendo.no/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f92a00a-1bb0-486f-8c4c-bbd49665b2fa/lendo-slider-800w-opt.png" width="800" height="629" alt="lendo-slider" /></a><figcaption>A beautifully presented text input fallback on <a href="https://www.lendo.no/">Lendo</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebfc617f-4590-48be-a7da-94a129477c42/lendo-slider-large-opt.png">View large version</a>)</figcaption></figure>

To provide a shortcut to precise input with a slider, we can use either **predefined presets** &mdash; frequently chosen values or value ranges &mdash; or enhance the slider with a **text input field fallback**. Both presets and the input field could be progressively disclosed &mdash; either by a tap on a button or just from a tap on the current value on the slider.

Now, how would you **indicate that the value is editable**? The obvious way would be to display it within an actual input field, or use a gray border on the white background, or add a dotted border bottom for that value. If nothing else helps, we could add a pencil icon. Or, upon pressing the handle, the text box could become editable and the value would be updated automatically with the thumb movement.

<figure><a href="https://ya.no/lan/s%C3%B8knadsskjema-step1"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81d3ae59-3ef8-4bbf-99e8-c0036c85fb22/yabank-slider-800w-opt.png" width=""800 height="230" alt="yabank-slider" /></a><figcaption>Not every slider needs a circular thumb. <a href="https://ya.no/lan/s%C3%B8knadsskjema-step1">Ya bank</a> has a square handle. A gray border around the value input indicates clearly that the value can be edited manually. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/984c4e25-8a77-4e82-88f0-ffe20fe88c6d/yabank-slider-large-opt.png">View large version</a>)</figcaption></figure>

Editable input raises another question. As the user taps on the value, should it disappear entirely, or **should the cursor jump to the end of the input**? In most cases, the second option would work better since it’s more predictable and easy to adjust. If the user has moved a slider’s thumb to a specific position and wants to make a fine adjustment, it’s easy enough to do by removing a few characters from the input rather than retyping it over again. However, it could be helpful to have a "reset" option to be able to restore the position on the slider &mdash; just in case.

Precise input might not always be necessary, but an interface would only improve from having an **option to jump to a specific value**. In general, it’s a good idea to keep the value editable for every slider &mdash; just in case the user wants to make a tiny final adjustment quickly.

{{< vimeo id="225683933" caption="<a href='https://www.halifax.co.uk/loans/compare-loans/online-loan/#'>Online loan calculator</a> by Halifax beautifully illustrates the annual percentage rates for different loan amounts." >}}

The [online loan calculator](https://www.halifax.co.uk/loans/compare-loans/online-loan/#) by Halifax beautifully illustrates the annual percentage rates for different loan amounts. Precise input is possible in the input field or by using steppers. It’s remarkable how much detail the slider provides without being overwhelming. The only downside is that it’s impossible to snap to the ranges displayed below the track or to tap on the tick marks.

## Visual Feedback On Cursor

And then there is the question of how exactly the cursor should change when the user is hovering over a thumb. Should the cursor become a `pointer`, or a resize cursor (`ew-resize`), or a resize column cursor (`col-resize`), or a `move` cursor, or perhaps a `grab`/`grabbing` cursor? The problem with all of these options is that they don’t necessarily indicate exactly what we need &mdash; usually they aren’t restricted to just one axis.

For example, in a drag-and-drop interface, we can move blocks both vertically and horizontally. The only exception is resizing (`ew-resize` or `col-resize`, to be specific), which indicates exactly the right direction. However, we aren’t really resizing a slider here, but dragging it across the track.

<figure><a href="https://www.sparkasse.at/scheibbs/privatkunden/wohnen-finanzieren/konsumfinanzierung/konsumkreditrechner?blueprint=/sgruppe/privatkunden/wohnen-finanzieren/konsumfinanzierung/konsumkreditrechner#/main"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74ec8a32-b0f5-4a25-adcb-17707c11f2bb/sparkasse-ew-resize.gif" width="690" height="444" alt="sparkasse-ew-resize" /></a><figcaption>On <a href="https://www.sparkasse.at/scheibbs/privatkunden/wohnen-finanzieren/konsumfinanzierung/konsumkreditrechner?blueprint=/sgruppe/privatkunden/wohnen-finanzieren/konsumfinanzierung/konsumkreditrechner#/main">Sparkasse.at</a>, the cursor changes to <code>ew-resize</code> on hover. Notice the unusual pendulum effect on the calculated value. The track could have larger padding, and the input is just a tiny bit difficult to edit. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74ec8a32-b0f5-4a25-adcb-17707c11f2bb/sparkasse-ew-resize.gif">View large version</a>) (<a href="https://player.vimeo.com/video/225684654">Watch video in HD</a>)</figcaption></figure>

<figure><a href="https://www.google.com/flights/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/707f58f5-d079-4fda-bb98-4968cf8150bd/google-col-resize.gif" width="800" height="632" alt="google-col-resize" /></a><figcaption><a href="https://www.google.com/flights/">Google Flights</a> uses <code>col-resize</code> to indicate that the item can be moved horizontally.</figcaption></figure>

As the user hovers over a thumb or a track, the safest option would be to use `pointer` to indicate interactivity. As the user grabs the handle, we could change the cursor to `grab`, and as it then wanders across the track, it could become `grabbing`. That would provide clear feedback of the current state of interaction.

## Giving A Slider That Extra Touch

The context of your website or application might require quite specific slider features or enhancements. If the range of values is likely to remain consistent but the lower and upper boundaries will change a lot &mdash; for example, in a TV guide or online banking application with a date-range selection &mdash; what about allowing users to shift the range of values across the track?

Indeed, on narrow screens, [Urban Ladder](https://urbanladder.com/sofa-cum-bed?src=cat_2#page-2) allows users to shift a price range. Notice how the price range shrinks automatically when the selected track area reaches the lower or upper boundaries. Unfortunately, with this implementation, touch events sometimes get in the way.

{{< vimeo id="225862397" >}}

However, the situation is slightly more complicated if we have interdependent sliders. A change on one slider might limit options for succeeding sliders. For [Taskstream](https://dribbble.com/shots/3419643-Taskstream-Microinteraction-Series-1), Juweek Adolphe suggested to extend the “fillable” area on sliders to indicate the changed range.

<figure><a href="https://dribbble.com/shots/3419643-Taskstream-Microinteraction-Series-1"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30acdabf-1b70-4a3b-ae2c-2eea12574822/taskstream.gif" width="800" height="600" alt="taskstream" /></a><figcaption>An interdependent slider. (Image: <a href="https://dribbble.com/shots/3419643-Taskstream-Microinteraction-Series-1">Juweek Adolphe</a>)</figcaption></figure>

If a change in value in one slider prompts other sliders to scale up or down, we could also “lock” a value in one slider with a padlock icon next to it &mdash; for example, for [split testing](https://dribbble.com/shots/3611765-Split-Testing/), as suggested by Rafael Conde.

<figure><a href="https://dribbble.com/shots/3611765-Split-Testing/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5920049-295d-48ce-928a-a1816af830bf/locking-the-value.gif" width="800" height="" alt="locking-the-value" /></a><figcaption>Netlify’s UI allows users to lock some values on a slider. (<a href="https://dribbble.com/shots/3611765-Split-Testing/">Image credit</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5920049-295d-48ce-928a-a1816af830bf/locking-the-value.gif">View large version</a>)</figcaption></figure>

Skandia’s [våra bolåneräntor](https://www.skandia.se/lana/bolan/bolanerantor/), a mortgage rate calculator, discloses progressively. As the first input is made, the rest of the calculator appears below. Simple and well designed.

Obviously, fancy animations and transitions won’t work in every scenario, but sometimes being less generic and predictable and slightly more experimental is worth it. Take a look at the nice overview of unusual progress indicator demos on [“Elastic Progress” on Codrops](https://tympanus.net/Development/ElasticProgress/).

<figure><a href="https://dribbble.com/shots/3551099-Slider"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49f4428b-ebc6-4bd6-b277-9c33047cb599/transition-animation.gif" width="800" height="600" alt="transition-animation" /></a><figcaption>Animation matters. Not every slider has to be generic. A fun, playful animation by Felippe Silveira is shown here. Also, look into the <a href="https://tympanus.net/Development/ElasticProgress/">“Elastic Progress” demos on Codrops</a>. (<a href="https://dribbble.com/shots/3551099-Slider">Source</a>)</figcaption></figure>

## Contrast and Keyboard Accessibility

Throughout this article, we’ve mostly talked about the experiences users have by tapping or dragging the slider or by interacting with it using a mouse. What we didn’t mention is the big number of accessibility issues that sliders often raise. The suggestions below are generously shared by [Ramón Corominas](https://twitter.com/tinitun).

One of them is **contrast**. In fact, as you might have spotted in some examples above, some sliders have almost no contrast between the selected part of the track and the unselected one. The track, tick marks, range labels, histogram bars and the thumb all need enough contrast against the background on which they are placed &mdash; otherwise detecting and operating a slider for users with low vision can easily become a nightmare.

Dual sliders and the sliders enhanced with a histogram require extra level of detail as they present a lot of detail that a screenreader user wouldn’t be able to access. That’s where we would need to use ARIA live regions and/or roles (`aria-live`, `aria-controls`, `aria-valuenow`, `aria-valuemin`, `aria-valuemax`) extensively to announce that extra level of information.

You don’t need ARIA if a slider is used on `<input type="range">`. The current value is always read out when it changes in screen readers, without `aria-valuenow` included. You can see Heydon Pickering’s [Drum Machine slider implementation](https://heydon.github.io/beadz-drum-machine/) as a reference.

Another issue is the appearance of sliders in the **high contrast mode**. If a slider uses only background colors or images for track, tick marks or even the thumb, they might completely disappear in high contrast mode. There, we could create three SVG images &mdash; one for the thumb(s), one for the "filled" part of the track, and one for the "empty" part of the track. Moving the thumb then will just change the widths of the "filled" and "empty" bars, so the full width of the slider remains the same. We could also include a 1-pixel white border, so it will appear when high contrast mode is activated.

Beyond that, the slider has to be **keyboard-accessible** as well. It doesn’t just mean that we need to design the controls to be accessible &mdash; keyboard input works slightly different when a screen reader is active, so we need to test both scenarios. Either way, interaction with a slider would be done in “steps.”, also providing aural feedback to screen reader users.

Once the user tabs through the page and hits the handle, they should be able to **edit the numeric value** or use left and right arrows to increment or decrement the value. It’s up to us, then, to choose a value that will make it comfortable to adjust the filter in granular steps. In the YouTube app, you can double-tap on the left to go back 10 seconds and on the right to go forward 10 seconds. On Netflix, you can use the left and right arrows to jump 10 seconds as well.

There are some fully accessible solutions for sliders, such as [Whatsock’s ARIA Horizontal Slider](https://whatsock.com/tsg/Coding%20Arena/ARIA%20Sliders/Horizontal/demo.htm) or [fd-Slider](https://github.com/freqdec/fd-slider). Obviously, they might not be perfect for your needs, so making fine adjustments and testing with real users will be necessary.

Still, even if all of these issues are solved, a slider might not be the fastest control for screen reader users or keyboard users. It might be better to **announce common choices first** and use a plain input field instead, then progressively enhancing it towards a slider with an editable value display. This might make interaction a bit more straightforward.

## Where Does It Leave Vertical Sliders?

While all examples and design considerations in this article focus on horizontal sliders, one might wonder where does it leave vertical sliders, when are they used and if there are any issues specific to them. In fact, vertical sliders are quite difficult to spot, and when they are used, they usually **control a spatial view or data visualization**. With maps, vertical sliders can help move between different panes or levels, while horizontal sliders enable interaction left and right.

One option would be to enable quick jumps to specific regions of a long list without using a dropdown menu &mdash; similar to the **vertical alphabet bar** used on iOS contacts. In fact, because lengthy lists often have a **scrollbar**, those scrollbars actually become single, continuous sliders; it’s just that the handle is often too tiny to navigate comfortably. Now, what if instead of a tiny scrollbar track we used a large enough thumb?

<figure><a href="https://adioso.com/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d0de182-ba1b-4dce-bfbe-3132b5345775/autosuggest.gif" alt="Adioso, flight search engine" /></a><figcaption><a href="https://adioso.com/">Adioso</a> groups all destinations into various groups, making options easy to access. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e46bca9b-b623-4cd7-b90e-df0347c5ad49/autosuggest-large.gif">Large view</a>)</figcaption></figure>

[Adioso](https://adioso.com/), a flight search engine, provides a sophisticated list of destinations grouped by cities, countries, continents, regions, states, wanderlists or even your friends. The list contains a tiny, almost unnoticeable, scrollbar on the right side which, for long lists, can be very difficult to scroll through. In cases when the handle becomes smaller than a certain threshold, we could **replace it with a large thumb** might help make the list easier to explore. Admittedly, autosuggest relieves this problem for Adioso, and so do tabs on the left side.

Another scenario where a vertical slider could be an interesting option, is a histogram view. If a service displays available flight options based on the departure/arrival time (with a dual horizontal slider, like Kayak does), sometimes a single very expensive flight might alters the scale of the whole visualization, so the differences in the lower prices become undistinguishable. What if we enhanced this experience with a vertical slider to **adjust the scale or filter the price range**, hence allowing users to "zoom in" to the lower values?

Finally, when it comes to spatial navigation in a map &mdash; which can be quite challenging in terms of accessibility &mdash; a combination of a horizontal and vertical sliders could be used to help users move through the map using the keyboard. Huge thanks to Ramón Corominas for these suggestions!

## Summary

If your interface accepts only a few input options, then using a slider probably would be an overkill. A set of radio buttons, checkboxes or predefined options might work better. But whenever the user’s input is supposed to **encourage exploration**, rather than precision, a slider is definitely a good option to consider. However, to be effective, a slider need space &mdash; the track should be wide and tall enough, the thumb large enough, and the padding for both generous enough; displaying the distribution of values in the background would mean that it needs enough both horizontal and vertical space.

The main point of interaction with the slider is to display options quickly. This means not forcing the user to click on a button to see the outcome or wait until the result is displayed. Feedback should be smooth and continuous, without noticeable lag &mdash; in fact, a slider should never freeze.

The thumb usually doesn’t need any special iconography, but it needs proper visual treatment, and smooth transitions and animations can increase the customer’s engagement. Tick marks not only are useful shortcuts to jump to discrete values, but also help orient users on the slider. When setting those tick marks, though, keep in mind that an **algorithmic scale usually works better** than a linear scale.

As users move the handle across the track, we could enlarge the handle on hover, add some shadow to it and change the color of the track. We also have to consider ARIA live regions and “manual” steps for keyboard accessibility and screen reader users. Finally, a good slider **allows for precision if needed**; so, extending it by turning the chosen value into a plain input field is usually a good idea.

Phew! And that’s a wrap! If you need some inspiration for better design of your slider, look into implementations of sliders in video players of popular streaming platforms. Unlike in other interfaces, sliders there are quite meticulously crafted as they are heavily used by their customers all the time.

Perhaps you’ve had **very different experiences** than the ones mentioned in this article? Let us know in the comments below! Also, if you have another component in mind that you’d love to have covered, let us know, too &mdash; we’ll see what we can do!

## Stay Tuned!

This article is **part of a new ongoing series** about responsive design patterns here on yours truly, Smashing Magazine. We’ll be publishing an article in this series every two weeks. Don’t miss the next one &mdash; on fancy (and not so fancy) feature comparison tables. Interested in a (printed) book covering all of the patterns, including the one above? Let us know in the comments, too &mdash; perhaps we can look into combining all of these patterns into a single book and publishing it on Smashing Magazine. Keep rockin’!

<div class="c-felix-the-cat">
<h4 class="h3">Part Of: <a href="/category/design-patterns/">Design Patterns</a></h4>
<ul>
<li>Part 1: <a href="https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/">Perfect Accordion</a></li>
<li>Part 2: <a href="https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/">Perfect Responsive Configurator</a></li>
<li>Part 3: <a href="https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/">Perfect Date and Time Picker</a></li>
<li>Part 4: <a href="https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/">Perfect Feature Comparison</a></li>
<li>Part 5: <strong>Perfect Slider</strong></li>
<li>Part 6: <a href="https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/">Perfect Birthday Picker</a></li>
<li>Part 7: <a href="https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-mega-dropdown-hover-menus/">Perfect Mega-Dropdown Menus</a></li>
<li>Part 8: <a href="https://www.smashingmagazine.com/2021/07/frustrating-design-patterns-broken-frozen-filters/">Perfect Filters</a></li>
<li>Part 9: <a href="https://www.smashingmagazine.com/2021/08/frustrating-design-patterns-disabled-buttons/">Disabled Buttons</a></li>
<li><a href="https://www.smashingmagazine.com/the-smashing-newsletter/">Subscribe to our email newsletter</a> to not miss the next ones.</li>
</ul>
</div>

### Further Resources

*   [Continuous Slider](https://material.io/guidelines/components/sliders.html#sliders-continuous-slider), “Components,” Material Design
*   “[Sliders](https://developer.apple.com/ios/human-interface-guidelines/ui-controls/sliders/),” Human Interface Guidelines, iOS, Apple
*   “[Slider Control Design Guidelines for Windows Phone](https://msdn.microsoft.com/en-us/library/windows/apps/hh202877(v=vs.105).aspx),” Windows Dev Center, Microsoft
*   “[Input Controls for Parameters: Balancing Exploration and Precision with Sliders, Knobs, and Matrices](https://www.nngroup.com/articles/sliders-knobs/),” Page Laubheimer, Nielsen Norman Group
*   “[Mobile UX Design: Sliders](https://uxplanet.org/mobile-ux-design-sliders-761ce4bb2a86),” Nick Babich, UX Planet
*   “[Mobile Design Pattern: Inventory-Based Discrete Slider](https://www.smashingmagazine.com/2014/10/inventory-based-discrete-slider/),” Greg Nudelman and Daria Kempka, Smashing Magazine
*   “[Slider Design: Rules of Thumb](https://www.nngroup.com/articles/gui-slider-controls/),” Aurora Harley, Nielsen Norman Group
*   [ARIA Horizontal Slider](https://whatsock.com/tsg/Coding%20Arena/ARIA%20Sliders/Horizontal/demo.htm), Whatsock
*   [fd-Slider: HTML5 Input Range Polyfill/Unobtrusive Accessible Slider](https://github.com/freqdec/fd-slider), Brian McAllister, GitHub
*   “[My Sliders](https://codepen.io/collection/DgYaMj), Ana Tudor, Codepen
    A huge collection of designs and implementations of sliders, collected and implemented by the one and only Ana Tudor.
*   [Sliders Inspiration Album](https://vimeo.com/album/4684443), a collection of 50 short videos of sliders, collected for this very article.

_This article is written with remarkable contributions by Ilya Birman, Christian Holst (Baymard Institute), Maya Virdee, Ramón Corominas, Sumit Paul, Melissa Regina &mdash; thank you so much for sharing thoughts and suggestions for this article!_

{{< signature "al, il" >}}

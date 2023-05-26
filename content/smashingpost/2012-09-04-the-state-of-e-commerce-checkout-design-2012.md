---
title: The State Of E-Commerce Checkout Design 2012
slug: the-state-of-e-commerce-checkout-design-2012
image: null
date: 2012-09-04T12:08:57.000Z
author: christian-holst
description: >-
  A year ago we published an article on 11 fundamental guidelines for e-commerce
  [checkout
  design](https://www.smashingmagazine.com/2011/04/06/fundamental-guidelines-of-e-commerce-checkout-design/)
  here at Smashing Magazine. The guidelines presented were based on the 63
  findings of a larger E-Commerce Checkout Usability research study we conducted
  in 2011 focusing strictly on the checkout user experience, from “cart” to
  “completed order".

  <a href="">![The State Of E-Commerce Checkout Design
  2012](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/787474f6-e9de-4163-87c7-8b6ff767118f/require-registration-compared-to-size.png
  "The State Of E-Commerce Checkout Design 2012")</a>

  This year we've taken a look at the state of e-commerce checkouts by
  documenting and benchmarking the checkout processes of the [top 100 grossing
  e-commerce websites](https://baymard.com/checkout-usability/benchmark) based on
  the findings from the original research study. This has lead to a massive
  checkout database with 508 checkout steps reviewed, 975 screenshots, and
  3,000+ examples of adherences and violations of the checkout usability
  guidelines.
categories:
  - UX
  - E-Commerce
  - Studies
  - User Research
---
A year ago we published an article on 11 fundamental guidelines for e-commerce [checkout design](https://www.smashingmagazine.com/2011/04/06/fundamental-guidelines-of-e-commerce-checkout-design/) here at Smashing Magazine. The guidelines presented were based on the 63 findings of a larger E-Commerce Checkout Usability research study we conducted in 2011 focusing strictly on the checkout user experience, from “cart” to “completed order".

This year we've taken a look at the state of e-commerce checkouts by documenting and benchmarking the checkout processes of the [top 100 grossing e-commerce websites](https://baymard.com/checkout-usability/benchmark) based on the findings from the original research study. This has lead to a massive checkout database with 508 checkout steps reviewed, 975 screenshots, and 3,000+ examples of adherences and violations of the checkout usability guidelines.

Here’s a walkthrough of just a handful of the interesting stats we’ve found when benchmarking the top 100 grossing e-commerce websites’ checkout processes:

1.  The average checkout process consist of **5.08 steps**.
2.  24% require **account registration**.
3.  81% think their newsletter is a **must have** (opt-out or worse).
4.  41% use **address validators**.
5.  50% asks for the **same information** twice.
6.  The average top 100 checkouts **violate** 33% of the checkout usability guidelines.

In this article I'll go over each of them and explain exactly what’s behind these numbers, showing you some real life implementations of do's and don'ts when it comes to checkout processes.

{{% feature-panel %}}

## The Average Checkout Process Consists Of 5.08 Steps (But It Doesn’t Influence Usability Too Much)

The average checkout consists of 5.08 steps, counting from the shopping cart to the step where the order is actually placed — often a _"review and confirm order"_ step. The shortest checkout process is one step (including cart) and the longest being a massive nine steps.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/269ab9d5-6658-4776-9719-eab62e7e05ed/step-distribution-new.png" alt="Average Number Of Checkout Steps" title="Average Number Of Checkout Steps" width="1260" height="597" loading="lazy" decoding="async" class="141094" />

Above you see the distribution among the top 100 grossing e-commerce websites in regards to the number of checkout steps they have. Note that only a single website had one step (including cart), and the “average” for this one website therefore shouldn’t have been given too much weight.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f69b0fa4-a626-4eb4-b771-d4bb3a2e8b08/score-as-a-function-of-steps.png" alt="Score As A Function Of Steps" title="Score As A Function Of Steps" width="761" height="362" loading="lazy" decoding="async" class="141099" />

Above, we’ve plotted the websites grouped after the number of checkout steps, moving out from the x-axis, as the groups average checkout usability score moves up the y-axis. As you can see, we’ve found that up until six checkout steps there isn’t a noticeable relation between the number of checkout steps and the quality of the user's checkout experience. This matches the test subject's behavior we observed during the checkout usability test back in 2011\. What matters the most for checkout experience isn’t the **number of steps** in a checkout process, but rather what the customer has to do at each step.

With that being said, there does seem to be an upper limit to the number of steps practically achievable in a checkout process before it begins to hurt the checkout experience. The websites with eight or nine steps have accumulated a significantly lower score in checkout usability than the rest of the checkout processes. This is often a result of required account registration (which typically induces more steps and is bad for checkout usability) as well as the fact that websites that end up with over eight checkout steps simply have more chances available to screw up the experience for their customers. At the time of testing, these were the websites with eight or more steps: Sephora ([8](https://baymard.com/checkout-usability/benchmark/top-100/94-sephora "Sephora's Checkout Process")), Amazon ([8](https://baymard.com/checkout-usability/benchmark/top-100/73-amazon "Amazon's Checkout Process")), Peapod ([8](https://baymard.com/checkout-usability/benchmark/top-100/38-peapod "PeaPod's Checkout Process")), Sony ([8](https://baymard.com/checkout-usability/benchmark/top-100/11-sony "Sony's Checkout Process")), Safeway ([9](https://baymard.com/checkout-usability/benchmark/top-100/82-safeway "Safeway's Checkout Process")), ShopNBC ([9](https://baymard.com/checkout-usability/benchmark/top-100/67-shopnbc "ShopNBC's Checkout Process")) and W.W. Grainger ([9](https://baymard.com/checkout-usability/benchmark/top-100/10-grainger "W.W. Grainger's Checkout Process")).

To recap: don’t focus too much on the number of steps in your checkout — instead spend your resources on what the customers **have to do** at each step, as that is what matters the most for the checkout experience. Three examples of this are the checkout processes of Apple, Walmart and Gap, which are all seven-step checkouts that perform approximately 50% higher than the average top 100 grossing checkouts (not to say that they are perfect, there are still room for further checkout improvements). While in theory it is possible, in practice none of the benchmarked websites with eight or more checkout steps had a checkout process that wasn’t greatly under-delivering in regards to the checkout user experience for a new customer.</p>

## 81% Think Their Newsletter Is A “Must Have” (And Don't Value Customer Privacy)

81% of the 100 largest e-commerce websites “assume” that their customers want their promotional emails by having a pre-checked newsletter checkbox (or worse) at some point during checkout.

[![Sehopra Pre-Checks The Newsletter Box](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24e94519-f038-4237-a96c-250efc007a95/register-for-the-best-cosmetics-fragrances-skin-care-and-gifts.png "Sehopra Pre-Checks The Newsletter Box")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24e94519-f038-4237-a96c-250efc007a95/register-for-the-best-cosmetics-fragrances-skin-care-and-gifts.png)
_[Large view](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24e94519-f038-4237-a96c-250efc007a95/register-for-the-best-cosmetics-fragrances-skin-care-and-gifts.png)._

One reason why customer hate being required to create an account to complete a purchase is because they have a mental model of _account = newsletter_. This became evident during the user testing, where we heard the same complaint over and over again: people hate creating an account when buying online. When we asked the test subjects why, 40% told us that they “didn’t want any newsletters”.

For years websites, including e-commerce websites, have tricked customers into “accidentally” signing up for newsletters that they didn’t want by visually downplaying a pre-checked “subscribe to newsletter” checkbox. So people have come to expect, that when they sign up for a new account, that they **also sign up for a newsletter**, or “spam” (as more than half of the test subjects had referred to such newsletters).

This mental model sadly isn’t just a misconception, but evidently something learned the hard way. Pre-checking the newsletter checkout is one thing, but of those 81% of the websites that think their newsletter is a “must have”, 32 of them proceed to do something even worse than pre-checking a checkbox:

[![Amazon Checkout Step 3](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/facf5c36-2e9e-4bff-90d8-ed008c11695c/amazon-checkout-step3.png "Amazon Checkout Step 3")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/facf5c36-2e9e-4bff-90d8-ed008c11695c/amazon-checkout-step3.png)
_Amazon is just one of the 32% of the top 100 grossing e-commerce websites that automatically signs customers up for their newsletters, without clearly informing the customer (only via the privacy link), and without giving an opting-out option during checkout. [Large view](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/facf5c36-2e9e-4bff-90d8-ed008c11695c/amazon-checkout-step3.png)._

These **32% automatically** sign up their new customers for their newsletters with no way of opting out during the checkout process, and often burying this fact deep down in their privacy policy. Typically, the only way for customers to “opt-out” on these websites are either by a privacy tab in an account settings section (if they were forced to register for an account) or by an unsubscribe link in the newsletters that the customers will automatically start receiving.

So what the test subjects displayed of **account = newsletter** is something they learned from shopping at websites (such as these from the top 32%). Only 8% of the top 100 e-commerce websites value their customers inbox and ask them to opt-in if they want to receive newsletters (as does the last 11%, which don't offer newsletter subscriptions at all during checkout.)

## 24% Require Account Registration

To put it differently: 24% don’t offer the customer a “guest checkout” option when placing an order, but force them to create accounts on their websites.

[![Sony Electronics Checkout Step 2 Account](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c1f1ce4-ec64-425a-9f85-8f86c0737f78/sony-electronics-checkout-step-2-account.png "Sony Electronics Checkout Step 2 Account")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a1bf82f-6cfe-4c4a-9f4c-d9cb1a8931cc/sony-electronics-checkout-step-2-account1.png)
_Sony (step [2](https://baymard.com/checkout-usability/benchmark/top-100/11-sony#step-2 "Sony's Checkout Process Step 2")) is just one of the 24% that require every new customer to register for an account when placing an order. [Large view](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4a1bf82f-6cfe-4c4a-9f4c-d9cb1a8931cc/sony-electronics-checkout-step-2-account1.png)._

During the checkout usability study, we (as have many others have before us) have identified multiple reasons why potential customers resent being forced to register for an account just for placing a simple order. We’ve already touched upon one of them, the mental model of _account = newsletter_. But let’s quickly list a handful more of them that we’ve found during the study:

1.  Signing up for an account means more steps and form fields to complete during checkout — essentially taking longer to complete.
2.  Most customers already have a myriad of logins and passwords to remember and don’t want more of them.
3.  When creating an account, customers are more likely to realize that you’re storing their information indefinitely.
4.  Many customers just don’t understand why they need an account to buy a product. As one test subject clearly expressed during testing: _“I don’t need to sign up for anything when I’m buying a perfume in a regular [brick and mortar] store.”_

[![Nordstrom's Checkout Process Step 3](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f7167b3-0246-448d-a4b5-9cf48f046b88/nordstrom-checkout-step-3-shipping-address-billing-address-834e300810b26d0bec54097fdbc3ea8b.png "Nordstrom Process Step 3")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d279bcc-c840-4b9d-935e-5f60bab6ab18/nordstrom-checkout-step-3-shipping-address-billing-address.png)
_Nordstorm (step [3](https://baymard.com/checkout-usability/benchmark/top-100/27-nordstrom#step-3 "Nordstrom's Checkout Process Step 3")) is one example of the 76% of the top 100 grossing e-commerce websites that offer new customers the much appreciated “guest checkout” option, but offering at the same time an easy optional account registration. [Large view](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d279bcc-c840-4b9d-935e-5f60bab6ab18/nordstrom-checkout-step-3-shipping-address-billing-address.png)._

When you do it right (as 76% of the e-commerce websites have done) and provide the much appreciated guest checkout option, you still have the possibility of asking for an optional account creation along (or after) the purchase. This can be done simply by creating a short section with a brief description and an optional password field. During the checkout usability study no test subjects were put-off by this approach, and just left the optional field(s) blank if they weren’t interested in creating an account with that particular website. But they generally liked the option on websites where they were interested in becoming repeat customers.

If we look into the type of websites that typically require account registration, there is a slight tendency towards them being the highest grossing websites:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/787474f6-e9de-4163-87c7-8b6ff767118f/require-registration-compared-to-size.png" alt="Require Registration Compared To Size" title="Require Registration Compared To Size" width="550" height="336" loading="lazy" decoding="async" class="141204" />

Of the 23 websites that had more than $1 billion in online sales (Internet Retailer 2010 sales estimates), 35% of them required account registration, whereas for the rest of them grossing less than $1 billion (and down to $148 million) it was only 21% that required account registration during checkout.

## 41% Use Address Validators

Of these 41%, 12% (relative) don't allow their customers to override the validation mechanism in case the address isn't recognized (though the customer is absolutely sure the address is correct).

[![Amway](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35d7c8a7-36d0-45a7-8670-9917ba961372/amway.png "Amway")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83059abc-8b21-4b7d-9b4e-d888db778fa8/amway1.png)
_Amway is one examples of the 12% (relative) that doesn't allow the customer to proceed in any way, in the event that the address validator is outright wrong, or the address validation database isn't updated properly. [Large view](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83059abc-8b21-4b7d-9b4e-d888db778fa8/amway1.png)._

An address validator can be a smart way to avoid common customer typos that might cause shipping problems, ones that otherwise would have resulted in undelivered or delayed orders. But street names, postal codes, etc. **aren’t consistent**, nor permanent. So the possibility still exists that it’s the address validation mechanism/database that is erroneous — not the customer's input. Those subsets of websites that don't allow the customer to force proceed through a potentially wrong address validator (at the time of testing: Office Depot, ShopNBC, Amway Global, FreshDirect, and CafePress) will leave the customers with no other option but to abandon their purchase as they are technically locked-out from completing the checkout process.

![Overstock Adhered](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e719d30-10a3-40a7-a93e-2421bab08071/overstock-adhered.png "Overstock Adhered")
_A decent implementation by Overstock (step [3](https://baymard.com/checkout-usability/benchmark/top-100/21-overstock-com#step-3 "Overstock's Checkout Step 3")) that informs the customers that their typed address doesn't match the address validation — and therefore, are likely to be wrong — while still giving the customers an option to force-proceed._

The advisable approach — implemented by the vast majority of the 41% of those websites utilizing address validators — informs the customer that the typed address doesn't match, yet still allows them to **force proceed** if they are sure that the address is right.</p>

## 50% Ask For The Same Information Twice

Instead of pre-filling the already typed-in information for the customer, 50% of the e-commerce websites add **needless friction** to their checkout experience by asking for the same information more than once. This is rarely at the same page (although that does happen) but is most often happening across multiple pages. Sometimes it’s the customer's name that isn’t pre-filled from the address step to the billing step. Other times it’s the zip code that the customer provided at the cart step (e.g. for a shipping calculator) which isn’t pre-filled at the the shipping address step. Although it is only fair to assume that in most cases users calculate the shipping to a certain zip code, this would also be the zip code that they plan on shipping the order to.

[![Apple Step5 Crop](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63613507-426c-46c8-93dd-98af5388debd/apple-checkout-step-5.png "Apple Step5 Crop")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea8ddcea-0d3d-45f3-979e-64ded8c80f64/apple-checkout-step-5-full-size.png)
_Apple is one of the 50% of e-commerce websites that asks for the same information more than once. At their [5](https://baymard.com/checkout-usability/benchmark/top-100/1-apple#step-5 "Apple's Checkout Step 5")’th checkout step the billing email address isn’t prefilled — even when the customer clicks the “Same as shipping information”-link. [Large view](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea8ddcea-0d3d-45f3-979e-64ded8c80f64/apple-checkout-step-5-full-size.png)._

Retyping information is a tedious task on a regular computer, but on a mobile device most users will find it outright annoying. Considering that all the benchmarked websites gross $148+ million per year in online sales, it seems rather sloppy that only half of them have dedicated the resources to removing needless checkout friction by ensuring that they don’t ask for the same information more than once (across multiple pages).

[![Hayneedle Step2 Cropped](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/836179c8-37ab-44cf-86b8-087df8d5e467/hayneedle-step2-cropped1.png "Hayneedle Step2 Cropped")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6095fa9-a038-471a-ab89-0aa47e7f6aea/hayneedle-step2-original.png)
_On the path to reducing needless checkout friction, only 10% of the websites helped their customers by pre-filling the state and/or city fields based on the zip code provided. Hayneedle (step [2](https://baymard.com/checkout-usability/benchmark/top-100/62-hayneedle#step-2 "Hayneedle's Checkout Step 2")) was one of them. The result: three less fields for the customer to fill + shipping dates and costs already updated at the page entry. [Large view](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6095fa9-a038-471a-ab89-0aa47e7f6aea/hayneedle-step2-original.png)._

On the same note for reducing needless checkout friction, only 10% of the websites helped their customers to fill-out even less form fields by **pre-filling** the state and/or city fields based on the zip code that the customer provides.</p>

## The Influence Of Revenue And Industry

The e-commerce websites grossing above the $1 billion mark scored 44% worse on checkout usability (for a first-time customer) than the e-commerce websites grossing below $1 billion.

When taking a closer looking at the checkout experience of these 23 websites that gross over $1 billion, it’s likely that some of that gap exists because these websites are more focused on forcing as many customers into their account eco-system as possible. Furthermore, the top grossing e-commerce websites also tend to be the ones with the most complex marketplace systems. These marketplace systems often end up inducing a lot of derived complexity into the checkout process, due to shipping and legal constraints, for a deal where the website only acts as the middleman. In comparison, some of the “smaller” websites in the top 24 to 100 grossing range had one simplified goal for their checkouts: to let the customer move as swiftly as possible through the checkout process.

[![Usability Score Vs. Online Sales Scatterplot](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b6b70e6-7779-4677-90fa-5029b07a1ee1/usability-score-vs-online-sales-scatterplot-550.png "Usability Score Vs. Online Sales Scatterplot")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/513cef2d-048f-41d7-b6cd-f6deedb5f282/usability-score-vs-online-sales-scatterplot.png)
_All the top 100 e-commerce websites plotted with checkout usability score moving up the y-axis and online sales moving out the x-axis (logarithmic scale). Notice that the far majority of checkouts that scored the highest on checkout usability are below the $1 billion sales mark. [Large view](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/513cef2d-048f-41d7-b6cd-f6deedb5f282/usability-score-vs-online-sales-scatterplot.png)._

If we take a look at specific e-commerce industries, the Automotive Parts industry had much better checkout usability than the rest of the industries (scoring 110% higher) whereas the Office Supplies industry scored the lowest (38% lower than average). Food & Drugs followed right behind in providing the worst checkout experience.

It’s interesting to see the that in both the worst and the best scoring industries, all three have a very similar checkout process. In fact, their checkouts are almost identical; have a look at [Staples’ checkout](https://baymard.com/checkout-usability/benchmark/top-100/2-staples "Staples' checkout"), [Office Depot's checkout](https://baymard.com/checkout-usability/benchmark/top-100/4-office-depot "Office Depot's checkout"), and [OfficeMax's checkout](https://baymard.com/checkout-usability/benchmark/top-100/6-officemax "OfficeMax's checkout"). I’m not going to speculate on who "was inspired” by whom, nor does it really matter. But in the Office Supplies industry it’s unfortunate, because as a consequence they all suffer from a very sub-standard checkout experience (38% lower than the average). While it’s clear that some of the top 100 e-commerce websites are using the same system vendor (and thus, end up with similar features and sequences in their checkout flow), the tendency of similar checkouts between competitors weren’t noticed to nearly the same degree in some of the other e-commerce industries (e.g. in Electronics).</p>

## The General State Of E-Commerce Checkouts

If we have an overall look at the top 100 grossing e-commerce checkout processes, the average checkout violates 21 checkout usability guidelines. This is an indication that checkout improvements are still much needed if the average cart abandonment rate of [65,95%](https://baymard.com/lists/cart-abandonment-rate "65,95% abandonment rate") is to be lowered (_“50% Ask for Same Information Twice”_ also points in this direction).

This overall lacking of checkout experience — even among the highest grossing e-commerce stores — is hardly rooted in an unwillingness to improve checkout experience, but is most likely due to a combination of factors, such as:

1.  Flows are much more difficult to improve than single pages.
2.  Checkouts often need deep, back-end integration, and thus require more IT capabilities to modify/test upon.
3.  Checkouts haven’t been on the agenda for top management (although, I believe this has changed a lot in recent years).
4.  Checkouts are for most designers much more dull to work on than product pages, home pages or new ad-campaigns.
5.  In a few cases, a poor user experience can still be good for business, at least in the short run (e.g. sneaking people into your newsletter).
6.  No Web convention for a checkout process exists.
7.  “Best practice” for checkout designs are scattered and scarce (only two to three research-based resources exist).
8.  Feedback from those who use the checkout process are only several degrees of separation from those who design and develop it.
9.  Improving most somewhat-optimized/decent checkouts aren't 1 to 3 "big fixes", but are most likely to be 10 to 30 smaller checkout changes.

If you want to further examine the checkout processes and flows of the 100 top grossing e-commerce websites for yourself — without filling out some 1,300 form fields, as we have done — you can do so in the free part of the [2012 E-Commerce Checkout Benchmark](https://baymard.com/checkout-usability/benchmark "2012 E-Commerce Checkout Benchmark"), as we’ve decided to make that part of the database publicly available.

{{< signature "jvb" >}}


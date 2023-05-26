---
title: 'Designing Effective Pricing Plans UX'
slug: designing-better-pricing-page
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37c160fe-99a6-4e3f-b754-dda006ff84fa/designing-better-pricing-page-sharing-card.jpg
date: 2022-07-06T12:00:00.000Z
summary: >-
  Pricing pages can be complex and confusing. Let's explore some design patterns, guidelines, real-life examples and best practices on how to design a better pricing page.
description: >-
  Pricing pages can be complex and confusing. Let's explore some design patterns, guidelines, real-life examples and best practices on how to design a better pricing page.
categories:
  - Design Patterns
  - Usability
  - UX
  - Accessibility
---
Imagine that you need to **design a pricing page**. The page is intended for a product that has four different pricing plans. All plans are designed for different audiences, vary in features, include some customization options, and are available in various currencies. For such a table, we should probably consider addressing specific groups with appropriate plan’s names and descriptions. We should also allow users to **highlight differences** between the plans and probably provide a fully-fledged feature comparison matrix.

Now, this doesn’t sound like a particularly challenging task at first, does it? After all, we’ve seen something quite similar already with our good ol’ [feature comparison tables](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/). In fact, many design patterns discussed there are very much applicable to pricing plans as well, so please take a look there first and come back afterward.

Surely not every pricing plan is as complex as a comparison of sophisticated 4K TVs or digital cameras, yet often pricing plans have **plenty of fine intricacies and caveats** of their own &mdash; hidden somewhere between tooltips, tabs, scrollable panes, and sizeable accordions. There is just a lot of information to display, and we need to show it well, driving users towards an option that works best for them, both on desktop and on mobile.

{{< rimg breakout="true" href="https://www.ableton.com/en/shop/live/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d564092c-b547-4788-84ad-755c60821975/1-designing-better-pricing-page.jpg" width="800" height="496" sizes="100vw" caption="One of the many: <a href='https://www.ableton.com/en/shop/live/'>Ableton Live</a>, with plenty of features to compare, collapsible accordions, large lists of all features repeated between plans, and tooltips. A classic. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d564092c-b547-4788-84ad-755c60821975/1-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

So if we wanted to design a better pricing table, what would we do? Well, let’s start with the very basic question: **how do people actually compare** attributes on a pricing page in the first place?

<p style="background-color: #e8f5ff;
border: 1px solid #dbeaff; border-radius: 11px; padding: 1.35rem 1.65rem;">This article is part of our ongoing series on <a href="/category/design-patterns">design patterns</a>. It’s also a part of the upcoming <a style="font-weight: bold" href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-ux/">4-weeks live UX training</a>&nbsp;🍣 and is in our recently released <a href="https://smart-interface-design-patterns.com/">video course</a> already.</p>

## Pricing Plans Comparison UX

When a customer lands on a pricing page, we can presume that they are looking for the pricing of a product that would **fit their needs best**. They might be just exploring what we have to offer, or they might be comparing our product with the offers of our competitors. Either way, we need to provide them with a neatly packaged bundle of features and a competitive pricing tag for those features.

For a given product, however, there might be literally hundreds and hundreds and hundreds of features. Comparing pricing plans by exploring every single feature one by one can be quite an adventure, time-consuming and cumbersome, and often not particularly exciting.

### 1. Lawn Mower Pattern

Usability studies [show](https://www.nngroup.com/articles/comparison-tables/) that users often rely on the [lawn mower pattern](https://www.nngroup.com/articles/lawn-mower-pattern/) when exploring feature comparison tables. That means that they begin in the top-left cell, move to the right until the end of the row, then drop down to the last cell of the next row and move back to the left until the end of the row.

{{< rimg href="https://www.nngroup.com/articles/lawn-mower-pattern/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba609cd0-25ca-4128-b8dd-390732c68dee/lawn-mower-border-2.jpg" width="800" height="496" sizes="100vw" caption="The lawn mower pattern in action: that’s how users scan data within comparison tables. Source: <a href='https://www.nngroup.com/articles/lawn-mower-pattern/'>NN Group</a>." alt="" >}}

Every now and again, however, they **randomly jump into one of the attributes** and study it in detail, stubbornly and passionately. While doing so, however, there are often jumps back to the headers of the table to verify that they are still exploring the right plan.

### 2. Frequent Verification of Table Headers

A typical problem that appears especially in complex pricing pages is the **loss of orientation**. Once users are in the middle of a pricing plan, they often refer back to the heading of the column to verify that they are exploring the right plan and review the plan’s price.

However, if headers aren’t visible, users tend to **scroll up and down the page repeatedly**, often losing focus while comparing. This is especially frustrating on mobile, where both the attributes and plans are often out of view, making any comparison within a table very challenging and tiring.

### 3. Sense of Progression: From Left to Right

If you need to locate the free plan or the enterprise plan, where would you expect it to be on the pricing page? Indeed, the free plan is likely to be on the left, and the enterprise plan either in a separate tab or on the right. Indeed, in left-to-right interfaces, we intuitively assume that there is a **sort of progression** from simple basic plans to expensive enterprise plans from left to right.

{{< rimg breakout="true" href="https://www.storyblok.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4b9b874-2247-4f18-9e6c-47fb75b75bf4/3-designing-better-pricing-page.jpg" width="800" height="605" sizes="100vw" caption="A typical pricing page design on <a href='https://www.storyblok.com/pricing'>Storyblok</a>. As plans “grow” from left to right, everything on the previous plan is included in the next plan. Notice that there are no tooltips in place here. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4b9b874-2247-4f18-9e6c-47fb75b75bf4/3-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

“Standard” and “most popular” plans are, of course, expected somewhere in the center. For customizable features and add-ons arranged vertically, the default selection or recommended features are expected to appear first, with more features listed next, **from least to more expensive**.

### 4. Complete List Of Features Used as Reference

We might assume that customers often know which features are relevant to them, and in fact, that is going to be the case in many scenarios. But when it comes to complex products, all bets are off. Some **features might sound familiar** or important, but their description might be somewhat cryptic. Other features might be irrelevant at the moment, yet become helpful for some tasks in the near future. As it turns out, "relevance" might be very much a **moving target**: while some features are known to be important up front, and others are definitely not, some *might* be relevant, yet they need to be discovered first.

And with hundreds of features in front of us, we might have a hard time finding these **possibly relevant features** without going through the entire list first. That’s why having a detailed comparison view of all features across all plans is very much needed: at the very least to understand what exactly a particular plan entails. Some users see it as the ultimate reference, used to clarify all the fine details that go into a plan.

Although it is indeed valuable, at the first glance, it also is **overwhelming**, often requiring minutes of tireless interaction, with thousands of eye gazes along the way. Going from row to row is exhausting, but many users see it as a necessary part of the process. (As we will see later, a feature comparison has to be available on the page, but it doesn’t have to be the front and center of the pricing page design).

### 5. Multiple Comparison Scans

In usability testing, one can observe **at least two comparison scans** that users perform when comparing pricing plans. For the first scan, we try to assess the scope of the features at large and **understand the differences** between available options. Once it’s done, we try to navigate towards a plan that seems to be fitting our role or our scope best. Not a big surprise there.

But eventually, we return to the top of the feature comparison table yet again, focus on that plan that we’ve pre-selected earlier, and explore it line by line in a **second, more focused comparison scan**. With mouse users, sometimes you can even see the user’s mouse pointer eloquently moving within the column representing that plan, from top to bottom, and lingering there for a while.

While the first scan allows us to find a plausible plan, the second scan helps us verify that that plan is indeed a good fit across all major features &mdash; plus to make sure that we didn’t miss anything important so far.

### 6. Not All Features Are Equal

Chances are high that not every prospective customer will want to explore all available features. In testing, users will often **jump between rows or entire sections** to skip attributes that aren’t relevant to them. There surely will be some important **key features** that need to be displayed at all times, but there will be some secondary, less significant features as well. Many of these features will be relevant for some customers but not for everyone.

So finding a good way to break down those features into groups and display them upon request will probably be quite helpful in keeping the comparison relatively simple. Also, we could provide shortcuts by associating each plan with a particular user profile or a company to help customers **quickly locate a plan** that might be working best for them.

With these behavior patterns in mind, let’s explore some design patterns and features that might come in handy when incorporating all these details into a pricing page design.

## Simple Prices, No Surprises

The design of a pricing page heavily depends on how complicated the pricing is in the first place. In some cases, we might not even need to reinvent the wheel as long as the pricing is quite straightforward. We just need to make sure customers understand the drill and the price for the offering.

[Stripe](https://stripe.com/en-de/pricing) gets away with a **simple pricing for everyone** except for large customers. All features are highlighted, but further down the page, along with testimonials, existing customers, integration options, and FAQ. If you have a simple pricing, that’s a reference example to keep close.

{{< rimg breakout="true" href="https://stripe.com/en-de/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e5b1b2b-a6f6-4462-ae31-34043335eda3/4-designing-better-pricing-page.jpg" width="800" height="540" sizes="100vw" caption="" alt="" >}}

{{< rimg breakout="true" href="https://stripe.com/en-de/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d6c2d3a-584c-4577-9265-47eb683b4390/5-designing-better-pricing-page.jpg" width="800" height="594" sizes="100vw" caption="Simple pricing, beautiful design. <a href='https://stripe.com/en-de/pricing'>Stripe</a> gets away with a simple pricing option for everyone except for large customers. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d6c2d3a-584c-4577-9265-47eb683b4390/5-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Algolia](https://www.algolia.com/pricing/) follows a **similar approach**. Rather than highlighting every individual feature at the top, the feature matrix is placed further down the page, with the enterprise option only visible closer to the footer of the page. There are also add-ons, further plans, and FAQ featured there.

{{< rimg breakout="true" href="https://www.algolia.com/pricing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c81a277e-6ef8-4aa9-82c5-e9bc6b1fb0d7/6-designing-better-pricing-page.jpg" width="800" height="447" sizes="100vw" caption="" alt="" >}}

{{< rimg breakout="true" href="https://www.algolia.com/pricing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc65d4c4-f3b9-415c-9a5f-f5221269a4bd/7-designing-better-pricing-page.jpg" width="800" height="392" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc65d4c4-f3b9-415c-9a5f-f5221269a4bd/7-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Fathom Analytics](https://usefathom.com/pricing) changes the pricing based on a single attribute: the **number of monthly page views**. Rather than displaying features for each plan, all features are listed separately in the right column, while the pricing options are displayed on the left. Also, notice the call to action “Get started with a free trial,” and an option to get 2 months free by switching to the yearly payment. Simple.

{{< rimg breakout="true" href="https://usefathom.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c50e285c-60bc-463e-bd9c-d5cabe4137a1/8-designing-better-pricing-page.jpg" width="800" height="708" sizes="100vw" caption="No complex pricing plans: just one that changes based on the number of monthly page views. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c50e285c-60bc-463e-bd9c-d5cabe4137a1/8-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Kissflow](https://kissflow.com/workflow/pricing/) doesn’t include a feature comparison matrix; nor are there any lengthy essays about available features or existing customers. Just **three simple options** with calls to action. While it might be enough for some companies, it might not be enough for others.

{{< rimg breakout="true" href="https://kissflow.com/workflow/pricing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fb0e6b9-0d9d-4577-b2cd-5595776b0d76/9-designing-better-pricing-page.jpg" width="800" height="548" sizes="100vw" caption="We need to find a balance between too much detail and too little detail. Would these pricing options be enough for everyone? (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fb0e6b9-0d9d-4577-b2cd-5595776b0d76/9-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

Sometimes pricing plans are slightly more nuanced and complicated. [amCharts](https://www.amcharts.com/online-store/) features **4 different kinds of licenses** available for every individual product. The pricing is displayed in a matrix, similar to the pattern we often see when booking flights, trains, or cinema tickets. Overall, we see a similar amount of options here, but they are displayed right away, while in the examples above, extended pricing options are hidden and revealed only once a user contacts customer support.

{{< rimg breakout="true" href="https://www.amcharts.com/online-store/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/268e9b2d-c522-428c-836f-726f731ea589/10-designing-better-pricing-page.jpg" width="800" height="530" sizes="100vw" caption="Sometimes pricing plans are complex, and making them easy to make sense of isn’t a trivial task. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/268e9b2d-c522-428c-836f-726f731ea589/10-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

For comparison, [HelloSign’s pricing page](https://app.hellosign.com/info/pricing) appears to be **quite complicated**, mostly due to plenty of cells all appearing as standalone blocks. Every attribute is repeated multiple times, making the pricing plans slightly more difficult to scan. Showing attributes separately in one column with checkmarks in each column might be a good idea here.

{{< rimg breakout="true" href="https://app.hellosign.com/info/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbf5a9ba-751a-47da-81d8-d570d507c8ef/11-designing-better-pricing-page.jpg" width="800" height="583" sizes="100vw" caption="The pricing plans aren’t complex, but they appear complex: there are plenty of cells with a grey background, so there seems to be a lot going on. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbf5a9ba-751a-47da-81d8-d570d507c8ef/11-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

However, it’s important to **show enough details** to make it clear to customers what the differences between plans are. For a while, [Evernote](https://evernote.com/compare-plans) was just displaying the plans within a table but not explaining the difference between them. Also, it might not be very obvious how “Sign up” and “Free trial” differ. That’s slightly confusing and oversimplified.

{{< rimg breakout="true" href="https://evernote.com/compare-plans" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85f3668f-45cb-4305-89d8-5c4d4899f3aa/12-designing-better-pricing-page.jpg" width="800" height="503" sizes="100vw" caption="" alt="" >}}

{{< rimg breakout="true" href="https://evernote.com/compare-plans" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e2a6e1-55c0-4aa2-afbe-4450573f1a8d/13-designing-better-pricing-page.jpg" width="800" height="580" sizes="100vw" caption="Maybe a little bit too much text on <a href='https://evernote.com'>Evernote</a>. Features are quite difficult to compare. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e2a6e1-55c0-4aa2-afbe-4450573f1a8d/13-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

Simple pricing definitely helps, but sometimes it might not be an option. For such cases, let’s explore how to turn some of the pricing plans above into slightly more scannable and digestible alternatives.

{{% feature-panel %}}

## The Obvious: The Pricing Table

Not much should surprise us about the design of pricing plans on a pricing page. Surely we’ll present them as columns side-by-side, with the main features presented for all plans and a call-to-action in-between. Also, at the top of the pricing table, we usually will find a toggle between the monthly and annual pricing and sometimes a currency selector.

[Notion pricing page](https://www.notion.so/pricing) is a great example of it, albeit a little bit different. All pricing plans are **billed annually by default**, with an option to switch to a monthly payment when signing up. Each plan explains the role for which it’s been created as long as the features of that plan. As we move from left to right, we keep adding more features.

{{< rimg breakout="true" href="https://www.notion.so/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f984968f-f586-4c2a-8e77-ec230a90bd86/14-designing-better-pricing-page.jpg" width="800" height="422" sizes="100vw" caption="Well-designed and straightforward. Simple pricing with friendly calls to action. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f984968f-f586-4c2a-8e77-ec230a90bd86/14-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

A comprehensive **feature comparison matrix** is displayed further down the page, with headings repeating for each new section and with tooltips that users can interact with to learn more details about every individual feature.

On [Rows](https://rows.com/pricing), pricing plans are beautifully presented **within a spreadsheet**, making it feel like a regular sheet that customers might use on their own when making their calculations. On mobile, each column becomes a standalone card, appearing one under another.

{{< rimg breakout="true" href="https://rows.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/debef421-2f31-4299-9c96-fbf6165427d4/15-designing-better-pricing-page.jpg" width="800" height="495" sizes="100vw" caption="As if it was a spreadsheet: the design fits well with the branding of the product. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/debef421-2f31-4299-9c96-fbf6165427d4/15-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

Sometimes all plans wouldn’t fit comfortably in one single row. For their six pricing plans, [Dropbox](https://www.dropbox.com/de/plans) **wraps them all** onto two separate rows. It definitely is a better idea than showing all plans in a condensed 6-column view. Rather than requiring a checkout, customers can also try out some plans for free.

{{< rimg breakout="true" href="https://www.dropbox.com/de/plans" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7776da7f-fd37-487a-8165-604647368139/16-designing-better-pricing-page.jpg" width="800" height="619" sizes="100vw" caption="Pricing plans showing up across a few rows. It takes quite a bit of space, but doesn’t appear too complicated. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7776da7f-fd37-487a-8165-604647368139/16-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Zendesk](https://www.zendesk.com/pricing) **groups their plans into tabs**. Not all plans are displayed at all times, and users are encouraged to specify what is it they are after first: individual plans or enterprise plans. There is also a dedicated comparison view to compare all 4 plans at once.

{{< rimg breakout="true" href="https://www.zendesk.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1f9e4b8-cbc4-4785-a923-05c3c4b28908/17-designing-better-pricing-page.jpg" width="800" height="571" sizes="100vw" caption="" alt="" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e5cdd42-1b5b-4139-85a5-044129255e43/44-v2-designing-better-pricing-page.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e5cdd42-1b5b-4139-85a5-044129255e43/44-v2-designing-better-pricing-page.jpg" width="800" height="498" sizes="100vw" caption="Tabs are a useful way to organize complex plans, but they also make some options less likely to be discovered. In use on <a href='https://www.zendesk.com/pricing'>Zendesk</a>, <a href='https://www.atlassian.com/software/jira/pricing'>Jira</a> and <a href='https://www.pluralsight.com/pricing'>Pluralsight</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e5cdd42-1b5b-4139-85a5-044129255e43/44-v2-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

An alternative way to display plans is to **allow users to choose** which plans appear to be most relevant to them. [N26](https://n26.com/en-de/plans) displays a drop-down menu &mdash; which allows users to choose which plans they’d like to study side-by-side. Depending on user’s screen, customers can compare up to 3 plans at once.

{{< rimg breakout="true" href="https://n26.com/en-de/plans" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b14e9d94-d484-4dee-bb81-b9f2669f6aee/18-designing-better-pricing-page.jpg" width="800" height="376" sizes="100vw" caption="Choose what you need, and we show it to you. Rather than showing all plans at once, users can choose what they want to explore on <a href='https://n26.com/en-de/plans'>N26</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b14e9d94-d484-4dee-bb81-b9f2669f6aee/18-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

Once you have more than a handful of plans to display, you can explore the option of **grouping them into tabs**, showing a few options in dropdowns, or wrapping them across multiple lines. What wouldn’t work well though, is squeezing all plans into one single space in a table, hence making users scroll the table horizontally. Usually, it’s a very good idea to avoid this experience at all costs.

## Focus on Key Features

As we keep designing and building and releasing all these wonderful features in our products, it might seem tempting for us to highlight *all of them* in our pricing plans. However, that’s usually the reason why pricing plans start appearing a bit too complicated, and require significant effort to figure out. An alternative approach is to **focus on key features first**, and display all the other features only if requested.

On [Contentful](https://www.contentful.com/pricing/), the pricing page doesn’t set focus on a lengthy feature comparison table; instead, the three main plans are highlighted at the top of the page, with **just a few key distinguished features**. The fully-fledged feature list is also available, but further down the page, rather than being the front and center of the experience. That’s simpler and better.

{{< rimg breakout="true" href="https://www.contentful.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df2ff6d9-5842-4907-9939-21a0c69c1c65/19-designing-better-pricing-page.jpg" width="800" height="587" sizes="100vw" caption="Just 4 key features highlighted for each plan: no lengthy list of benefits in sight on <a href='https://www.contentful.com/pricing/'>Contentful</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df2ff6d9-5842-4907-9939-21a0c69c1c65/19-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Chargebee](https://www.chargebee.com/pricing/) does **highlight plenty of features** of each plan, but a full comparison table appears only if the user actually chooses to see how the plans compare. On click, a modal window opens with all options lined out in a table.

{{< rimg breakout="true" href="https://www.chargebee.com/pricing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf78b117-1adb-4f4e-8e46-8661aead6d39/20-designing-better-pricing-page.jpg" width="800" height="702" sizes="100vw" caption="" alt="" >}}

{{< rimg breakout="true" href="https://www.chargebee.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3098dc8b-7a1e-4d70-b484-d8acfc25caa0/21-designing-better-pricing-page.jpg" width="800" height="649" sizes="100vw" caption="Showing all features in a mobile view might be slightly difficult on mobile. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3098dc8b-7a1e-4d70-b484-d8acfc25caa0/21-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Airtable](https://airtable.com/pricing) shows a few more features in a dense, compact view. With a bit of **color-coding**, each plan is highlighted slightly differently with a different background color. Notice that all prices, calls to action, and lists of features are aligned, so scanning the table is relatively easy. The list of all features and a plan comparison appear further down the page.

{{< rimg breakout="true" href="https://airtable.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/760490fa-a769-4e96-842b-dbc6c107b132/22-designing-better-pricing-page.jpg" width="800" height="717" sizes="100vw" caption="Different colors used for different plans, with the most popular plan having a more prominent call to action on <a href='https://airtable.com/pricing'>Airtable</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/760490fa-a769-4e96-842b-dbc6c107b132/22-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

More color-coding plans on [Codepen](https://codepen.io/accounts/signup). As users scan the features matrix, they can always rely not only on the position of the column but also on the **visual clues** to understand what plans they are exploring at the moment.

{{< rimg breakout="true" href="https://codepen.io/accounts/signup" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f94f3659-66a6-4ebf-a4e5-4bb29b8c167a/24-designing-better-pricing-page.jpg" width="800" height="690" sizes="100vw" caption="Colors provide visual clues to help customers navigate between columns more reliably. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f94f3659-66a6-4ebf-a4e5-4bb29b8c167a/24-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

In general, it’s worth testing just how necessary a large list of all features is, and whether a pricing page design would work better by **showing only a handful of distinguishable key features** instead. We could start with a design containing just a few items in the list, and add more once we know that the differences between the plans aren’t clear enough for our prspect customers.

## Show Differences Within Rows

In many examples above, features from one plan are fully included in the list of features from a higher-tier plan, but sometimes it’s not the case. You might have differences in charging fees or slightly different limitations depending on the select plan. In that case, you can follow [Podia](https://www.podia.com/pricing)’s example and **hide unavailable features**. While the contrast could be increased quite a bit, it makes it easy to compare each plan by scanning each row individually.

{{< rimg breakout="true" href="https://www.podia.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abc1e592-af9a-4e48-89d2-62f8875554de/25-designing-better-pricing-page.jpg" width="800" height="498" sizes="100vw" caption="When key features are available in all columns. On <a href='https://www.podia.com/pricing'>Podia</a>, it’s easy to spot the differences between the plans. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abc1e592-af9a-4e48-89d2-62f8875554de/25-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[N26](https://n26.com/en-de/plans) follows suit by **highlighting both available and unavailable options** in the same row. Each row can be expanded with a click on one of the chevrons and provides more details about each feature.

{{< rimg breakout="true" href="https://n26.com/en-de/plans" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fff5df61-9ddb-42fa-a800-57b05b6e1514/26-designing-better-pricing-page.jpg" width="800" height="457" sizes="100vw" caption="When every row is an accordion on each own. No need for tooltips on <a href='https://n26.com/en-de/plans'>N26</a> as details appear on tap/click. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fff5df61-9ddb-42fa-a800-57b05b6e1514/26-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Dovetailapp](https://dovetailapp.com/products/markup#pricing) explains differences by **highlighting the availability of features** rather than the lack thereof. It makes the feature comparison matrix slightly easier to scan.

{{< rimg breakout="true" href="https://dovetailapp.com/products/markup#pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84174213-c6b0-4957-b3cb-cf4b26b1ebb0/27-designing-better-pricing-page.jpg" width="800" height="523" sizes="100vw" caption="The fewer visual elements we have, the easier the pricing plan is to explore. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84174213-c6b0-4957-b3cb-cf4b26b1ebb0/27-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

When pricing plans are slightly more nuanced, with **significant differences between various tiers**, we can show all key features across all columns and highlight in which plan they are available. More details about each feature could appear within an accordion, rather than within tooltips. But we could also build up on top of these ideas, by explaining differences visually.

## Explain Differences Visually

Alternatively to a comparison matrix, we could try to **visualize differences between plans** within tabs, with a few animations that would explain a particular plan. [Twilio Segment](https://segment.com/pricing/) does just that. As users switch between tabs, the list of features is updated. This isn’t quite a side-by-side comparison, but it might be good enough to visualize how plans differ.

{{< rimg breakout="true" href="https://segment.com/pricing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b78bbc05-710e-4cb6-9a59-ec5544060464/28-designing-better-pricing-page.jpg" width="800" height="488" sizes="100vw" caption="<a href='https://segment.com/pricing/'>Twilio Segment</a> uses a visualization to highlight how different individual pricing plans are. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b78bbc05-710e-4cb6-9a59-ec5544060464/28-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Basecamp](https://basecamp.com/pricing) takes a similar approach by highlighting the main “business” plan but also explaining how the personal plan is different: it just doesn’t have some features that the main plan does. We can illustrate it by literally **crossing out the features** that are missing in that plan.

{{< rimg breakout="true" href="https://basecamp.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2298ebc5-702f-49d8-8588-0338d97abe0e/29-designing-better-pricing-page.jpg" width="800" height="575" sizes="100vw" caption="" alt="" >}}

{{< rimg breakout="true" href="https://basecamp.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e94f3532-02c1-45a2-9403-8357b9d411ae/30-designing-better-pricing-page.jpg" width="800" height="617" sizes="100vw" caption="<a href='https://basecamp.com/pricing'>Basecamp</a>: here’s what the main plain includes, and here’s what a personal plan doesn’t include. As simple as that. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e94f3532-02c1-45a2-9403-8357b9d411ae/30-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Ballpark](https://getballpark.com/pricing) visualizes the pricing plan by **building up a ballpark bundle** with a slider. It also explains all features that go along with the plan, and there is an option to use a free concierge onboarding as well.

{{< rimg breakout="true" href="https://getballpark.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eab50c18-b5ef-4c39-8ccf-cc2a7127e82c/31-designing-better-pricing-page.jpg" width="800" height="747" sizes="100vw" caption="Choose your own pricing plan, with a simple customization option visualized on <a href='https://getballpark.com/pricing'>Ballpark</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eab50c18-b5ef-4c39-8ccf-cc2a7127e82c/31-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

The examples featured above have one detail in common: **they don’t include a table**, but rather choose a slightly different, more simplified, way to highlight how the pricing plans differ. As we will see later, that’s usually a very good approach to avoid complexity that we usually get with feature comparison matrices. 

{{% ad-panel-leaderboard %}}
## Allow Users To See Only Differences and Only Similarities

Rather than showing the entire feature comparison matrix for complex plans, we could help customers make sense of the differences between the products by **highlighting these differences** immediately.

[Samsung’s comparison page](https://www.samsung.com/us/smartphones/galaxy-s21-5g/compare/?device-1=samsung-galaxy-s21-fe-5g&device-2=samsung-galaxy-s21-5g&device-3=samsung-galaxy-s21%2B-5g) of course isn’t a pricing page, but as a part of a feature comparison matrix, it allows users to select features that they are interested in, as well as **show differences and similarities** of each option.  Also, users can collapse entire groups of features, should they wish to do so.

{{< rimg breakout="true" href="https://www.samsung.com/us/smartphones/galaxy-s21-5g/compare/?device-1=samsung-galaxy-s21-fe-5g&device-2=samsung-galaxy-s21-5g&device-3=samsung-galaxy-s21%2B-5g" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faa8d6a4-07c0-45a1-b9d9-52d7fed3b9d7/32-designing-better-pricing-page.jpg" width="800" height="485" sizes="100vw" caption="A few years ago, customers could choose to see only differences and only similarities on Samsung. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/faa8d6a4-07c0-45a1-b9d9-52d7fed3b9d7/32-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

It’s probably obvious why we’d want to show the differences between plans to our customers, but why would we want to **show similarities only**? As it turns out, users often tend to choose a slightly more expensive plan, although they know that they won’t need all the features in that plan. What they are looking for next is the closest cheaper plan that is good enough as it covers most of the features available in a more expensive plan. For that reason, they might want to compare by showing only similarities to ensure that one plan is close enough compared to another.

## Use Sticky Headers

Since users often rely on table headers to verify that they are studying the right pricing plan, we can help them keep the headers in view at all times. We do so by **making headers floating** as users start scrolling down the page in a comparison table. [Contentful’s pricing page](https://www.contentful.com/pricing/) does just that. Both the title and the call to action are floating on top of the feature comparison matrix.

{{< rimg breakout="true" href="https://www.contentful.com/pricing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/747bfc12-0058-4b28-8755-df949da039bb/33-designing-better-pricing-page.jpg" width="800" height="595" sizes="100vw" caption="Floating headers with collapsible sections for features on <a href='https://www.contentful.com/pricing/'>Contentful</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/747bfc12-0058-4b28-8755-df949da039bb/33-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Intercom](https://www.intercom.com/pricing) highlights all features in a modal window, with the **pricing plans floating** as users scroll the table and explore their options.

{{< rimg breakout="true" href="https://www.intercom.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1888bca3-8c30-48cd-8d9f-65d196e29f06/34-designing-better-pricing-page.jpg" width="800" height="465" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1888bca3-8c30-48cd-8d9f-65d196e29f06/34-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

Additionally, to the titles of each pricing plans and calls to action, [Dropbox](https://www.dropbox.com/plans) keeps the **actual pricing points** and a yearly/monthly payment toggle floating on the top of the page as well.

{{< rimg breakout="true" href="https://www.dropbox.com/plans" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10c7f696-d335-4048-854c-ecb5ff5ca396/35-designing-better-pricing-page.jpg" width="800" height="474" sizes="100vw" caption="When pricing is floating as well. On <a href='https://www.dropbox.com/plans'>Dropbox</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10c7f696-d335-4048-854c-ecb5ff5ca396/35-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Figma](https://www.figma.com/pricing/) also sticks to **floating bars**. Additionally to pricing and calls to action, there are also tabs at the top, allowing users to switch between offered tools.

{{< rimg breakout="true" href="https://www.figma.com/pricing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d51624d-f839-44c6-8dbc-02f436ed9897/36-designing-better-pricing-page.jpg" width="800" height="451" sizes="100vw" caption="Floating bars are sticky on the top of the feature comparison matrix on <a href='https://www.figma.com/pricing/'>Figma</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6d51624d-f839-44c6-8dbc-02f436ed9897/36-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

As we saw ealerier, sticky headers always provide **a much needed reference** of what exactly customers are exploring at a given time. They do take a bit of space, but the comfort users get from comparing things without having to scroll up and down repeatedly is very much worth it.

## Group Attributes as Collapsible Sections

In the *Contentful* example above, we’ve seen that all features are not only grouped but also **entire groups of features can be collapsed** and opened at once. In fact, due to the sheer amount of available features, the option to skip some less important sections can significantly aid in navigation. Just like with regular cards, we make the entire bar act as an expander, so customers can skip over entire groups of features easily.

On [Zendesk](https://www.zendesk.com/pricing/#everyone), all features are grouped and **packaged into accordions** that can be open and collapsed at once. This allows for a faster scan of categories and makes the full list of features slightly more manageable.

{{< rimg breakout="true" href="https://www.zendesk.com/pricing/#everyone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c47c111-a3f7-4863-8af2-c066772f26fc/37-designing-better-pricing-page.jpg" width="800" height="498" sizes="100vw" caption="All features are grouped and packaged into accordions on <a href='https://www.zendesk.com/pricing/#everyone'>Zendesk</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c47c111-a3f7-4863-8af2-c066772f26fc/37-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

On [Ableton](https://www.ableton.com/en/shop/push/), all attributes are also grouped into accordions. Instead of using a chevron on the right, the `+` icon is used on the left. A click on any of the items opens a card for the entire row.

{{< rimg breakout="true" href="https://www.ableton.com/en/shop/push/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff190180-fa83-47c0-ab1c-b1066fb50263/38-designing-better-pricing-page.jpg" width="800" height="671" sizes="100vw" caption="Grouping features into accordions on <a href='https://www.ableton.com/en/shop/push/'>Ableton</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff190180-fa83-47c0-ab1c-b1066fb50263/38-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

{{< rimg breakout="true" href="https://www.ableton.com/en/shop/push/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b0522b-5381-49ea-97ef-b64d8a7f7b59/39-designing-better-pricing-page.jpg" width="800" height="673" sizes="100vw" caption="When accordions are expanded. Grouping features into accordions on <a href='https://www.ableton.com/en/shop/push/'>Ableton</a>.(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14b0522b-5381-49ea-97ef-b64d8a7f7b59/39-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

So, for tables on desktop, we **group features into accordions**, allow users to collapse them, and keep plans floating as users explore the table. Additionally, we keep features such as currency selection, monthly/annual pricing, and showing differences or similarities on the top of the table as well. This should give us a good starting point for our pricing page. But hold on, how do we now translate it all to mobile?

## Comparison Matrix on Mobile

Unfortunately, feature comparison tables just **don’t translate well to narrow screens** at all. Once there are a few dozens of feautures to display and, let’s say, at least 3 pricing plans, we need to provide some sort of **navigation within the table**. Usually, this ends up with a horizontal scroll within the table, which tends to be [slow, problematic, and tiring](https://www.nngroup.com/articles/horizontal-scrolling/).

If you have a relatively simple product, perhaps with just under 20 features, you might not need a feature comparison matrix at all &mdash; [Canva](https://www.canva.com/pricing/) avoids it on mobile and uses accordions instead, while on desktop, the comparison table does make its appearance.

{{< rimg breakout="true" href="https://www.canva.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79ccdcf8-acca-4896-8c0f-40559218dfc0/79-designing-better-pricing-page.jpg" width="800" height="473" sizes="100vw" caption="<a href='https://www.canva.com/pricing/'>Canva</a> shows a feature comparison table only on desktop, not on mobile." alt="" >}}

Comparing within a table with horizontal scroll is rarely a fun experience. On [Contentful](https://www.contentful.com/pricing/) and on [Hotjar](https://www.hotjar.com/pricing/), neither the attributes nor the corresponding pricing plan are obvious once you dive deep into the comparison matrix. Surely customers can scroll horizontally, yet this adds friction to the comparison.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e8b0a2-7c07-4ad4-a502-52c66b19ccae/40-v2-designing-better-pricing-page.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e8b0a2-7c07-4ad4-a502-52c66b19ccae/40-v2-designing-better-pricing-page.jpg" width="800" height="748" sizes="100vw" caption="With scrollable horizontal area within the table, exploring features is quite a nightmare. Examples: <a href='https://www.contentful.com/pricing/'>Contentful</a> and <a href='https://www.hotjar.com/pricing/'>Hotjar</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e8b0a2-7c07-4ad4-a502-52c66b19ccae/40-v2-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

As it turns out, **we might not need to display the table at all**. In fact, displaying any kind of complex tables on mobile is rarely a good idea, and there are a few other options that we could explore.

One of them is provided by [Mediamarkt](https://www.mediamarkt.de/). Instead of displaying a feature comparison table, we **ask users what features they are interested in**, or perhaps what role would apply best for them, and then display each feature as a separate step. In each step, we explain the differences between plans for each feature &mdash; rather than showing a table which would leave it to the user to make the comparison on their own.

{{< rimg breakout="true" href="https://www.mediamarkt.de/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab2ac0ed-279b-4fd8-a96b-7df539b59696/41-v2-designing-better-pricing-page.jpg" width="800" height="497" sizes="100vw" caption="Ask users what features they find relevant, and show only them: feature comparison on <a href='https://www.mediamarkt.de/'>Mediamarkt</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ab2ac0ed-279b-4fd8-a96b-7df539b59696/41-v2-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

Another option is to use **floating tabs**, following the example of [Mailchimp](https://mailchimp.com/pricing), [Cloudflare](https://www.cloudflare.com/plans/) and [Canva](https://www.canva.com/pricing/). On mobile, all pricing plans appear as sticky tabs on the top of the screen. As users scroll through features, they can flick through tabs to compare values.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26af5138-2d78-420d-9958-3a1a01e72020/42-v2-designing-better-pricing-page.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26af5138-2d78-420d-9958-3a1a01e72020/42-v2-designing-better-pricing-page.jpg" width="800" height="492" sizes="100vw" caption="Floating tabs in action, allowing users to switch between plans. Drawback: users can’t explore all options side-by-side. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26af5138-2d78-420d-9958-3a1a01e72020/42-v2-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

It might be a good idea to **move the tabs to the bottom of the screen** to avoid situations when users’ fingers obstruct some of the content on the screen, but comparing values by moving between tabs is worth testing.

[Cloudflare](https://www.cloudflare.com/plans/) is similar but also allows users to **jump between various groups of features** via a drop-down.

{{< rimg breakout="true" href="https://www.cloudflare.com/plans/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b001956c-614b-430f-9d55-82151f00f462/43-designing-better-pricing-page.jpg" width="800" height="501" sizes="100vw" caption="Customers can jump between various groups of features on <a href='https://www.cloudflare.com/plans/'>Cloudflare</a>." alt="" >}}

But it’s not necessary to allow users to see only one plan at a time. In fact, it’s likely that **at least two plans could be displayed side-by-side**. We can allow users to choose the plans of interest and show them next to each other. That’s the approach that [Dropbox](https://www.dropbox.com/plans) uses on mobile. Customers can choose 2 plans from the list of 5 existing plans and compare them side-by-side. Both [Twilio Segment](https://segment.com/pricing/) and [N26](https://n26.com/en-eu/plans) use tabs and swiping gestures to move between plans.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62cb3fd3-15dd-4233-a40f-cee7c476ca18/43b-v2-designing-better-pricing-page.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62cb3fd3-15dd-4233-a40f-cee7c476ca18/43b-v2-designing-better-pricing-page.jpg" width="800" height="488" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62cb3fd3-15dd-4233-a40f-cee7c476ca18/43b-v2-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

Finally, another way of managing a feature comparison matrix is by either **tilting headings** ([Gitlab](https://about.gitlab.com/pricing/)), or showing attributes on a separate row to make space for the 4 pricing plans values to appear in one single row ([Framer](https://www.framer.com/pricing/)) or **arrange all attributes vertically**, one under another, one row at a time ([Yousign](https://yousign.com/en-uk/pricing)). These all are fantastic options to avoid horizontal scrolling and make a feature comparison slightly easier to perform.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7a1266d-b225-4349-b549-1dc4c98c6b88/44b-designing-better-pricing-page.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7a1266d-b225-4349-b549-1dc4c98c6b88/44b-designing-better-pricing-page.jpg" width="800" height="479" sizes="100vw" caption="There are various ways of organizing features across plans: tilting headings, showing all features on a separate row, or showing one row at a time.(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7a1266d-b225-4349-b549-1dc4c98c6b88/44b-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

On [Netlify](https://www.netlify.com/pricing/), as you scroll down the page, all features are **repeated multiple times**, with a new section appearing as a sticky bar on the top, and hence indicating what the current plan is. On [Hubspot](https://www.netlify.com/pricing/) and [Chargebee](https://www.chargebee.com/pricing/), a modal view with a drop-down is used to jump between the plans. That’s quite a bit slower compared to tabs and usually not really necessary. It’s a good idea to see them here as the method of last resort.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e097dd52-375a-432b-b94f-b989755a743f/44c-designing-better-pricing-page.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e097dd52-375a-432b-b94f-b989755a743f/44c-designing-better-pricing-page.jpg" width="800" height="447" sizes="100vw" caption="Perhaps a little bit slower than necessary: tabs might be a good alternative here. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e097dd52-375a-432b-b94f-b989755a743f/44c-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

In general, if we could **avoid dropdowns to navigate between plans**, it’s a good idea to do so. There, using tabs or showing all features on a separate row might be a better option. Plus, we might want to explore ways to avoid tooltips as they can be quite difficult to get right as well.

## Tooltips and Feature Previews

Not all features listed in a comparison matrix are self-explanatory. Sometimes features might sound a bit unclear at first, so **we need to explain** what these features represent and how they could be valuable for customers. A common pattern to explain it is with **tooltips**. This usually happens by hovering/tapping on a dedicated tooltip-icon or the feature itself.

On [Notion](https://www.notion.so/pricing), hints explaining each feature are displayed when a user chooses to hover over the question mark icon. Unfortunately, they **aren’t focusable** and hence not keyboard-accessible. On mobile, the feature comparison table disappears altogether.

{{< rimg breakout="true" href="https://www.notion.so/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8e9540a-c6a0-4004-b5c8-07048edbda88/49-designing-better-pricing-page.jpg" width="800" height="426" sizes="100vw" caption="Hints appearing on hover on tooltips. Unfortunately, this implementation is inaccessible for keyboard users. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8e9540a-c6a0-4004-b5c8-07048edbda88/49-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

On [Airtable](https://airtable.com/pricing#limits), not only text hints but also **visual previews** appear on hover, including short animations that highlight and explain a feature. Unfortunately, there are no focus styles, nor are featured keyboard-accessible, so navigating between the features in a table is difficult.

{{< rimg breakout="true" href="https://airtable.com/pricing#limits" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92ec9a88-d9ca-4ac1-80bf-b2f4b7781f83/50-designing-better-pricing-page.jpg" width="800" height="676" sizes="100vw" caption="No focus styles, no tap/click alternative to hover tooltips. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92ec9a88-d9ca-4ac1-80bf-b2f4b7781f83/50-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Mailchimp](https://mailchimp.com/de/pricing/marketing/) **solves accessibility issues** by expecting a tap/click on a feature to open a nonmodal. Focus styles are in use, and keyboard users can move from one feature to another with Tab.

{{< rimg breakout="true" href="https://mailchimp.com/de/pricing/marketing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04c79e89-cef9-4751-90a1-a9c60b4f1c55/51-designing-better-pricing-page.jpg" width="800" height="494" sizes="100vw" caption="An accessible solution with tooltips opening on tap/click on <a href='https://mailchimp.com/de/pricing/marketing/'>Mailchimp</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04c79e89-cef9-4751-90a1-a9c60b4f1c55/51-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

On [Cloudflare](https://www.cloudflare.com/plans/#overview), **tooltips cover features listed further down the list**, making it difficult to move between features quickly. Also, notice that the position of the “info” icon doesn’t match the position of the “close” button in the tooltip, which slows down users who want to explore many features quickly.

{{< rimg breakout="true" href="https://www.cloudflare.com/plans/#overview" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/629b5da8-d035-48f2-a249-33c71fbcec32/52-designing-better-pricing-page.jpg" width="800" height="380" sizes="100vw" caption="Tooltips are problematic: they cover content, and to move forward we need to close the tooltip first. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/629b5da8-d035-48f2-a249-33c71fbcec32/52-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

Yet again, a problem that’s too common: **tooltips cover upcoming features** and make it difficult to navigate from one feature to the next quickly. Point in case: [Fantastical](https://flexibits.com/pricing).

{{< rimg breakout="true" href="https://flexibits.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/993989d8-88ce-42a6-877a-7245c46139f6/53-designing-better-pricing-page.jpg" width="800" height="481" sizes="100vw" caption="Yet again, tooltips covering some of the content: a too common problem for feature comparison tables.(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/993989d8-88ce-42a6-877a-7245c46139f6/53-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

You might have seen a common thread in the examples above. Indeed, at this point, it’s worth mentioning that [tooltips are problematic](https://adamsilver.io/blog/the-problem-with-tooltips-and-what-to-do-instead/); they cover content and require [focus trapping](https://css-tricks.com/focus-management-and-inert/), and if could replace them with accordions, we probably should. This goes hand in hand with the <a href='https://www.podia.com/pricing'>Podia example</a> featured below.

{{< rimg breakout="true" href="https://www.podia.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a58e130-7aba-4268-b2d1-e3e10031aa6b/54-designing-better-pricing-page.jpg" width="800" height="508" sizes="100vw" caption="No tooltips in sight. Instead, every feature is expandable and appears in an accordion. On <a href='https://www.podia.com/pricing'>Podia</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a58e130-7aba-4268-b2d1-e3e10031aa6b/54-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

On [Podia](https://www.podia.com/pricing) and [Netlify](https://www.netlify.com/pricing/), **every feature is explained in a separate accordion**. Frankly, not every feature *has* to be explained, and one issue might be that some customers might assume that `+` represents an option to add an add-on to the current price, which it isn’t. Perhaps having a chevron instead would be a bit more bulletproof.

[N26](https://n26.com/en-de/plans) uses **three chevrons per row**, but a tap/click on any of them expands the entire row and explains the differences of that feature across the plans.

{{< rimg breakout="true" href="https://n26.com/en-de/plans" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e8e1e4-c5ba-4b7c-9cfd-65e163b3e526/55-designing-better-pricing-page.jpg" width="800" height="457" sizes="100vw" caption="Three chevrons per row for pricing plans on <a href='https://n26.com/en-de/plans'>N26</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27e8e1e4-c5ba-4b7c-9cfd-65e163b3e526/55-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Confrere](https://confrere.com/pricing/) doesn’t have any tooltips nor accordions. There are lengthy descriptions of each feature, but these descriptions are provided **on separate pages** where each feature is explained in detail.

{{< rimg breakout="true" href="https://confrere.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a48d429a-78ff-4d30-aea4-a68b80affba6/56-designing-better-pricing-page.jpg" width="800" height="587" sizes="100vw" caption="No tooltips, no accordions. Instead, all features are explained in fine detail on separate pages. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a48d429a-78ff-4d30-aea4-a68b80affba6/56-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

When thinking about showing details about each feature, we could explore the option to rely not just on textual descrition but **show an actual feature preview** and even use cases when it could be helpful. The details could appear on tap/click, or even better within accordions, expanding a row as users interact with it.

{{% ad-panel-leaderboard %}}

## Flexibility With Customization Options

Ideally, we want to nudge users towards a plan that is a **perfect fit** for them. This is difficult to get right if we create a generic plan that’s supposed to be for everyone. Slack’s pricing for active users is a good example of flexible plans that accommodate well for the needs of the teams.

In the context of pricing plans, we can **allow customers to be more granular about pricing** by specifying the exact number of required seats and bandwidth and even customize the plan based on packages and add-ons that might be required. The end goal is to provide a **final price quickly** &mdash; not a random plan; a relevant plan that would work best for the user.

[Speedcurve](https://www.speedcurve.com/pricing/) allows users to **build their own plan** by specifying the amount of page views per month and the number of checks per month.

{{< rimg breakout="true" href="https://www.speedcurve.com/pricing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1e70451-5993-451b-9629-e603eb68a9aa/65-designing-better-pricing-page.jpg" width="800" height="472" sizes="100vw" caption="Build your own plan: customers can construct a plan that would accommodate their needs best on <a href='https://www.speedcurve.com/pricing/'>Speedcurve</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1e70451-5993-451b-9629-e603eb68a9aa/65-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Hotjar](https://www.hotjar.com/pricing/) changes its pricing based on whether **packages** are being used and based on how many daily sessions are expected to be used.

{{< rimg breakout="true" href="https://www.hotjar.com/pricing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a00b6d2d-5591-4782-bb65-9262e0fbc809/66-designing-better-pricing-page.jpg" width="800" height="501" sizes="100vw" caption="Packages in play at <a href='https://www.hotjar.com/pricing/'>Hotjar</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a00b6d2d-5591-4782-bb65-9262e0fbc809/66-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Mixpanel](https://mixpanel.com/pricing/) takes the number of MTUs into account, as well as any add-ons that the user might want to consider.

{{< rimg breakout="true" href="https://mixpanel.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abc6ace6-0256-480c-b3fd-7c7228bb045d/67-designing-better-pricing-page.jpg" width="800" height="503" sizes="100vw" caption="A custom plan builder at <a href='https://mixpanel.com/pricing/'>Mixpanel</a>, with add-ons available on request as well. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abc6ace6-0256-480c-b3fd-7c7228bb045d/67-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Intercom](https://www.intercom.com/pricing) focuses on **add-ons and extras** that can be added to the basic plan. This gives users an overview of the final price early on.

{{< rimg breakout="true" href="https://www.intercom.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b24a97a5-4c1a-4938-982b-5e4927cb7116/62-designing-better-pricing-page.jpg" width="800" height="552" sizes="100vw" caption="A simple basic plan is complemented with plenty of add-ons on <a href='https://www.intercom.com/pricing'>Intercom</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b24a97a5-4c1a-4938-982b-5e4927cb7116/62-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

Our ultimate design KPIs is to **reduce the time to relevance** in finding a perfect pricing plan. We can achieve it by being a bit more attentive to the exact needs that our customers have and provide a custom option that would be a perfect fit for them.

## Show a Transparent Pricing Example

Some pricing plans might be complex, and sometimes it’s not very obvious just what *exactly* is included and what isn’t included. We could **eliminate all doubts and concerns** by making it very clear how the price is calculated, what it includes, and if there are any hidden costs included. Stating that there are no hidden costs seems unnecessary but might very well help remove concerns.

[Intercom](https://www.intercom.com/pricing) explains how the price is calculated as well as any limitations and important facts to keep in mind when choosing a plan.

{{< rimg breakout="true" href="https://www.intercom.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de396b68-504f-4ff0-8dbe-694fb90ca476/57-designing-better-pricing-page.jpg" width="800" height="499" sizes="100vw" caption="We could explain how exactly a pricing works, and how it is calculated. <a href='https://www.intercom.com/pricin'>Intercom</a>.(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de396b68-504f-4ff0-8dbe-694fb90ca476/57-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Gumroad](https://gumroad.com/pricing) doesn’t leave any chance for any concerns. On their pricing page, a large area explains how the service works and what the pricing plan entails, along with a **pricing example** next to it.

{{< rimg breakout="true" href="https://gumroad.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b33a5c6-342e-4a78-841d-bb5d51c0d87b/58-designing-better-pricing-page.jpg" width="800" height="440" sizes="100vw" caption="Great idea: eliminate doubts and provide a pricing example to explain how a service works. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b33a5c6-342e-4a78-841d-bb5d51c0d87b/58-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

## Use Social Proof

But perhaps we can help out our users before they even start thinking about feature comparison at all. We can do so by explaining in detail **for whom the plan is designed**, what kind of companies would benefit from it, and what kind of companies already use it. That’s the social proof at its best.

[Intercom](https://www.intercom.com/pricing) allows customers to select between a plan intended for very small businesses or regular businesses. [Confrere](https://confrere.com/pricing/) explains the roles that a plan is designed for &mdash; consultants, physicians, therapists, or hospitals. Instead of focusing on generic plan titles, [Adobe XD](https://www.adobe.com/africa/products/xd/pricing/individual.html) highlights plans for individuals, students, businesses, and schools.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b1271c-bf4a-499b-a5c4-7be179994de6/47-v2-designing-better-pricing-page.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b1271c-bf4a-499b-a5c4-7be179994de6/47-v2-designing-better-pricing-page.jpg" width="800" height="490" sizes="100vw" caption="We could explain what roles and what kinds of companies each plan is designed for. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b1271c-bf4a-499b-a5c4-7be179994de6/47-v2-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[15five](https://www.15five.com/pricing/) explains **by whom each plan is typically used** &mdash; from PeopleOps teams to COOs and enterprises. This might nudge the decision enough without having to compare the features at all!

{{< rimg breakout="true" href="https://www.15five.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cacc0ac-9424-45da-95f1-f9e00428ad93/46-designing-better-pricing-page.jpg" width="800" height="" sizes="100vw" caption="We could explain what kind of users prefer each plan. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cacc0ac-9424-45da-95f1-f9e00428ad93/46-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Maze](https://maze.design/pricing/) explains how a company might be a good fit for a plan by using **testimonials and short case studies** with photos by various brands explaining how the plan helped them.

{{< rimg breakout="true" href="" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87135f98-e88a-4dcd-a3c1-2d1dec36ee81/59-designing-better-pricing-page.jpg" width="800" height="" sizes="100vw" caption="When customers want to find out if a plan is a good fit for them, they explore customers and companies like them preferring one of the plans. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87135f98-e88a-4dcd-a3c1-2d1dec36ee81/59-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Gumroad](https://gumroad.com/pricing) provides a **competitive matrix** comparing their pricing with the pricing of their main competitors. So does [Basecamp](https://basecamp.com/pricing).

{{< rimg breakout="true" href="https://gumroad.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b82ec86c-1e55-4f26-8334-3ebdc2c9a65f/60-designing-better-pricing-page.jpg" width="800" height="458" sizes="100vw" caption="Competitive pricing at Gumroad, comparing the pricing with their main competitors. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b82ec86c-1e55-4f26-8334-3ebdc2c9a65f/60-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

{{< rimg breakout="true" href="https://basecamp.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2436549-9f83-4bff-a475-9d98bf1f53d0/75-designing-better-pricing-page.jpg" width="800" height="451" sizes="100vw" caption="Competitive pricing at Basecamp, comparing the pricing with their main competitors. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2436549-9f83-4bff-a475-9d98bf1f53d0/75-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

[Intercom](https://www.intercom.com/pricing) suggests that a particular plan was **chosen by 53% of** businesses, so chances are pretty high that your business would be in a good place with that product.

{{< rimg breakout="true" href="https://www.intercom.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a78f9965-ff18-4a52-890f-c79f5a8580ab/70-designing-better-pricing-page.jpg" width="800" height="509" sizes="100vw" caption="Chosen by 53% of businesses. That statement alone might be enough to nudge owners of businesses towards that plan. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a78f9965-ff18-4a52-890f-c79f5a8580ab/70-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

And often, pricing plans are **complemented with brands** that use the product already, sometimes along with a few testimonials from actual people working in these companies. [Twilio Segment](https://segment.com/pricing/), [Airtable](https://airtable.com/pricing), [Netlify](https://www.netlify.com/pricing/) and [Chargebee](https://www.chargebee.com/pricing/) are good examples of just that.

{{< rimg breakout="true" href="https://segment.com/pricing/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca7b0d8f-19c9-44b5-884d-1c1f0a29acd2/71-designing-better-pricing-page.jpg" width="800" height="517" sizes="100vw" caption="<a href='https://segment.com/pricing/'>Twilio Segment</a> highlights the logos of brands using a particular brand right in the pricing plan. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca7b0d8f-19c9-44b5-884d-1c1f0a29acd2/71-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

{{< rimg breakout="true" href="https://airtable.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/596f838d-a53d-42db-abac-c173602f42cb/72-designing-better-pricing-page.jpg" width="800" height="435" sizes="100vw" caption="<a href='https://airtable.com/pricing'>Airtable</a> displays the brands trusting the product above its feature comparison matrix. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/596f838d-a53d-42db-abac-c173602f42cb/72-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

{{< rimg breakout="true" href="https://www.netlify.com/pricing" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35133e32-3adc-4963-a062-49fadbe1944e/73-designing-better-pricing-page.jpg" width="800" height="568" sizes="100vw" caption="A rolling overview of brands trusting the product on <a href='https://www.netlify.com/pricing/'>Netlify</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35133e32-3adc-4963-a062-49fadbe1944e/73-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

{{< rimg breakout="true" href="https://www.canva.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8492aeb-b8f3-48ae-87c3-e3ae6a4ae50c/80-designing-better-pricing-page.jpg" width="800" height="509" sizes="100vw" caption="A few testimonials can go a long way. They are front and center of the experience on <a href='https://www.canva.com'>Canva</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8492aeb-b8f3-48ae-87c3-e3ae6a4ae50c/80-designing-better-pricing-page.jpg'>Large preview</a>)" alt="" >}}

## Wrapping Up

Pricing plans seem to be obvious at first, but once we look a little bit closer, there are plenty of important considerations that need to be explored before heading into the design phase. Here’s a quick overview of some of the important things to think of when designing one:

- **Simple pricing** is always better, so always prefer it if possible.
- For complex plans, consider **wrapping, tabs**, and maybe dropdowns.
- No need to show all features at once: **focus on key features first**, and display the rest on request.
- **Show differences within rows** or explain differences visually.
- Allow users to **display only differences** and only similarities.
- Use sticky headers and group attributes within **accordions**.
- On mobile, **avoid horizontal scrolling** in tables.
- Consider turning every section into a **standalone evaluation step** of the best plan, use tabs, tilt headings, and show one attribute at a time. Avoid drop-downs.
- **Avoid hover tooltips** and show feature previews on tap/click.
- Expand details about each attribute on a separate row as an accordion.
- Provide **customization options** to allow for flexible custom plans.
- Prefer **transparent, honest, clear pricing** and don’t leave any chance to doubts or uncertainties.
- Use **social proof** to help users gain trust and understand what plan is the best fit for them.


## Meet Smart Interface Design Patterns

If you are interested in similar insights around UX, take a look at [**Smart Interface Design Patterns**](https://smart-interface-design-patterns.com/), our shiny new **9h-video course** with 100s of practical examples from real-life projects. Design patterns and guidelines on everything from mega-dropdowns to complex enterprise tables &mdash; with 5 new segments added every year. *Just sayin’!* [Check a free preview](https://www.youtube.com/watch?v=aSP5oR9g-ss).

<figure style="margin-bottom: 0"><a href="https://smart-interface-design-patterns.com/"><img style="border-radius: 11px" decoding="async" fetchpriority="low" width="950" height="492" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 400w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 800w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1200w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1600w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg" sizes="100vw" alt="Smart Interface Design Patterns"></a><figcaption class="op-vertical-bottom">Meet <a href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>, our new video course on interface design &amp; UX.</figcaption></figure>

<div class="btn--lined btn--lined--white-border" style="margin-top: 0.75em; margin-bottom: 0.75em"><a class="btn btn--large btn--green btn--text-shadow" href="https://smart-interface-design-patterns.com/">Jump to the video course&nbsp;&rarr;</a></div>

<p class="ticket-price__desc" style="font-size: .8em!important; text-align: center; line-height: 1.5; margin-top: 0; display: block;">100 design patterns &amp; real-life 
examples.<br>9h-video course + live UX training. <a href="https://www.youtube.com/watch?v=aSP5oR9g-ss">Free preview</a>.</p>

<p>If you find this article useful, here’s an overview of <strong>similar articles</strong> we’ve published over the years &mdash; and a few more are coming your way.</p>

### Related Articles

- [Designing A Perfect Infinite Scroll](https://www.smashingmagazine.com/2022/03/designing-better-infinite-scroll/)
- [Designing Perfect Breadcrumbs](https://www.smashingmagazine.com/2022/04/breadcrumbs-ux-design/)
- [Designing A Perfect Accordion](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/)
- [Designing A Perfect Responsive Configurator](https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/)
- [Designing A Perfect Birthday Picker](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/)
- [Designing A Perfect Date and Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
- [Designing A Perfect Feature Comparison](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/)
- [Designing A Perfect Slider](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/)
- “[Form Design Patterns Book](https://www.smashingmagazine.com/printed-books/form-design-patterns/),” written by Adam Silver

{{< signature "nl" >}}

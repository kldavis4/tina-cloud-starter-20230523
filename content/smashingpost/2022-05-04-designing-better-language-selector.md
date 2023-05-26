---
title: 'Designing A Perfect Language Selector UX'
slug: designing-better-language-selector
author: vitaly-friedman
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec0dac36-90ba-4295-b51b-f095fb2d90ff/designing-better-language-selector.jpg
date: 2022-05-04T10:00:00.000Z
summary: >-
  How difficult can it be to design a bulletproof language selector? It’s not as straightforward as one might think. We need to avoid redirects, decouple our language and country presets, allow for overrides, and use non-modal windows. Let’s dive in!
description: >-
  How difficult can it be to design a bulletproof language selector? It’s not as straightforward as one might think. We need to avoid redirects, decouple our language and country presets, allow for overrides, and use non-modal windows. Let’s dive in!
categories:
  - Design Patterns
  - Usability
  - UX
  - Accessibility
---

Imagine that you’ve just arrived in Tokyo. Full of impatience and excitement, you are just about to hit the road, yet there it comes: an **urgent warning** from your mobile provider, nudging you to top up your dwindling balance. With some justified concern, you go to the website, just to be redirected to the **Japanese version of the site**. You can’t read Japanese just yet, yet there is no obvious option to change the location, and there is no option to change the language either.

As the data keeps dwindling, you juggle between auto-translation and your limited VPN options &mdash; just to run out of data in the middle of the session. The language selector is somewhere there, yet it’s disguised between cryptic symbols and mysterious icons, nowhere to be found on the spot.

{{< rimg href="https://stripe.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ad18cfe-12b4-4fb4-81bb-9695dc0cb9d9/1-designing-better-language-selector.png" width="800" height="829" sizes="100vw" caption="Stripe with a popover allowing users to jump to a different country in the footer. <a href='https://stripe.com/'>Stripe</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ad18cfe-12b4-4fb4-81bb-9695dc0cb9d9/1-designing-better-language-selector.png'>Large preview</a>)" alt="<a href='https://stripe.com/'>Stripe</a> with a popover allowing users to jump to a different country in the footer." >}}

Chances are high that at some point you had a similar experience as well. As designers, we can of course make language selectors **more obvious and noticeable**, yet most of the time, the appearance of a component is only a part of the problem.

Too often, when we design interfaces, we subconsciously embed our **personal assumptions**, biases and expectations into our work. Of course, we can’t possibly consider all exceptions and all edge cases, along with all happy or unhappy coincidences. So we focus on the most common situations, eventually breaking a beautifully orchestrated user experience entirely for some of our disgruntled users.

Can we fix it? Absolutely! We just need to decouple presets, allow for overrides and allow users to specify their intent. But before we dive in, let’s explore what options we have in front of us.

<p style="background-color: #e8f5ff;
border: 1px solid #dbeaff; border-radius: 11px; padding: 1.35rem 1.65rem;">This article is part of our ongoing series on <a href="/category/design-patterns">design patterns</a>. It’s also a part of the upcoming <a style="font-weight: bold" href="https://smashingconf.com/online-workshops/workshops/vitaly-friedman-ux/">4-weeks live UX training</a>&nbsp;🍣 and will be in our recently released <a href="https://smart-interface-design-patterns.com/">video course</a> soon.</p>

## The Fine Little Details Of A Language Selector

Usually, we know when we need a language selector. Every multi-lingual website will need one, and this definitely holds true for public services and companies residing in countries with multiple national languages. It is also necessary for **global brands**, organizations and the hospitality industry &mdash; as well as eCommerce where goods might be paid in various currencies and shipped to various destinations around the world.

{{< rimg href="https://www.hikvision.com/en/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d021f79c-3c78-4f37-9d53-7ffa1418b5ba/2-designing-better-language-selector.png" width="800" height="527" sizes="100vw" caption="<a href='https://www.hikvision.com/en/'>Hikvision</a> with a sidebar overlay on the right. <a href='https://www.hikvision.com/en/'>Hikvinson</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d021f79c-3c78-4f37-9d53-7ffa1418b5ba/2-designing-better-language-selector.png'>Large preview</a>)" alt="Hikvision with a sidebar overlay on the right." >}}

Where do we place a language selector? Well, users have their usual suspects of course. In my experience, when asked to change a country or language, a vast majority of users will immediately **head to the header of the page first**, and if they can’t find it there, they’ll jump all the way to the bottom of the page and scout the footer next.

As for indicators of country selection, flags actually do work fairly well, and if users can’t spot them, they seek other icons that might represent a language in one way or the other &mdash; such as the globe icon or a “translation” icon. Obviously, when it comes to translations of articles or specific pages, users rely on the [laws of locality](https://learnui.design/blog/the-3-laws-of-locality.html) and search for a selection of language next to the title of the article. So far so good.

{{< rimg href="https://shop.lululemon.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc54664b-cd80-4df1-b01b-9355d1dc5fb0/3-designing-better-language-selector.png" width="800" height="482" sizes="100vw" caption="Lululemon with a sidebar overlay on the right. The language is selected with a separated dropdown. <a href='https://shop.lululemon.com/'>Lululemon</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc54664b-cd80-4df1-b01b-9355d1dc5fb0/3-designing-better-language-selector.png'>Large preview</a>)" alt="Lululemon with a sidebar overlay on the right. The language is selected with a separated dropdown." >}}

Design-wise, however, there are plenty of intricate details that we need to account for. Surely the selector on its own will live somewhere in the footer of the page, and it is also very likely to make its appearance in the header as well. However, we could also **auto-redirect users** based on their location and **auto-detect language** based on the browser’s preferences, or prompt a modal window and ask users to select a region first. We could be using text labels or abbreviations, icons or flags, native or custom dropdowns, preferences panes or sidebars, toggles, or standalone pages.

As we will see, many of these solutions have usability issues on their own; and if we want to **maximize clarity and reduce ambiguity**, we need to come up with a proper strategy of how to label and group languages, how to present them, and how to make the language selector obvious to users &mdash; without running into a wild mixture of accessibility and auto-translation problems down the line.

Let’s start with something that is probably obvious, but worth stating nevertheless &mdash; auto-redirects might be helpful, but they often cause more frustration and annoyance than a help.

{{% feature-panel id="vitaly-friedman" %}}


## Avoid Auto-Redirects

Many websites rely on redirects based on **user’s location (IP) or browser’s language**. However, if a person is located in Tokyo, it doesn’t necessarily imply that they fluently read Japanese. And if their preferred locale is Dutch, it doesn’t mean that they want to deliver physical items to the Netherlands. In the same way, if the preferred locale is French, yet it isn’t available on the site, a user might encounter a fallback language that isn’t necessarily the language that they are most comfortable with.

**We can’t confidently infer users’ preferences** without asking them first. That doesn’t mean that we should avoid redirects at all costs though. If a user happens to be connecting to a US website from Germany, it‘s perfectly reasonable to nudge them towards a German website. But if they happen to be connecting to a German website with an English locale preferred, it would be confusing to redirect them to the UK or US version of the site — even though it might very well be the user’s intent in some rare cases.

In general, **redirects based on location** are probably more instructive than redirects based on the browser’s language, but they are error-prone, too.

{{< rimg breakout="true" href="https://www.dyson.be/fr" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/daed8803-d2c8-4d9e-a963-e0391faef8cf/4-designing-better-language-selector.png" width="800" height="511" sizes="100vw" caption="A language selector drop-down in the header of <a href='https://www.dyson.be/fr'>Dyson.be</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/daed8803-d2c8-4d9e-a963-e0391faef8cf/4-designing-better-language-selector.png'>Large preview</a>)" alt="" >}}

On the very first visit, [Dyson.com](https://www.dyson.be/fr) nudges visitors to select the preferred region and language in the header on the page. Users can dismiss the bar and locate the language selector in the footer of the page again.

{{< rimg breakout="true" href="http://backcountry.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7863bbe0-79d5-4084-8066-680ca9beb278/58-designing-better-language-selector.png" width="716" height="314" sizes="100vw" caption="<a href='http://backcountry.com/'>Backcountry</a> auto-redirects users to another website. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7863bbe0-79d5-4084-8066-680ca9beb278/58-designing-better-language-selector.png'>Large preview</a>)" alt="Backcountry" >}}

[Backcountry](http://backcountry.com/), a US company for outdoor gear and clothing, automatically redirects its users to another site. Since 2018, the website is no longer available outside the U.S. as an answer to the GDPR regulations. Without a VPN, it’s **impossible to reach the website**, for example, to purchase and deliver a gift for a friend located in the U.S.

{{< rimg breakout="true" href="https://www.audi.com/de.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c0525d-38ff-4c10-b652-8205f06aa8e6/59-designing-better-language-selector.png" width="716" height="423" sizes="100vw" caption="<a href='https://www.audi.com/de.html'>Audi</a> auto-redirects users based on location. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/22c0525d-38ff-4c10-b652-8205f06aa8e6/59-designing-better-language-selector.png'>Large preview</a>)" alt="Audi" >}}

[Audi](https://www.audi.com/de.html) automatically redirects users to a country deemed as a **best fit**. However, users can choose their country by clicking on the language selector in the right upper corner. On click, a modal shows up with autocomplete and a disabled “Continue” button.

{{< rimg breakout="true" href="https://www.bmw.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de3b13bb-641e-499a-9573-8b411b12a37e/60-designing-better-language-selector.png" width="716" height="377" sizes="100vw" alt="BMW" >}}

{{< rimg breakout="true" href="https://www.bmw.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99550a32-ad47-466d-b310-8630920b517a/61-designing-better-language-selector.png" width="716" height="437" sizes="100vw" caption="<a href='https://www.bmw.com/'>BMW</a> avoids auto-redirect and guides users to a choice that works for them. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99550a32-ad47-466d-b310-8630920b517a/61-designing-better-language-selector.png'>Large preview</a>)" alt="BMW" >}}

A global [BMW website](https://www.bmw.com/) doesn’t automatically redirect users to any website. Instead, you can locate the **“BMW in your country” option** in the right upper corner of the header. It opens a modal with all the options listed, along with the prominent button at the top “BMW in your country”, which, on click, redirects users to the website considered to be the best fit for them. 

{{< rimg breakout="true" href="https://www.ikea.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99f66be3-fee3-4d15-a887-4ebe11a23725/62-designing-better-language-selector.png" width="716" height="375" sizes="100vw" caption="<a href='https://www.ikea.com/'>IKEA</a>, with a smart autocomplete for a language selection. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/99f66be3-fee3-4d15-a887-4ebe11a23725/62-designing-better-language-selector.png'>Large preview</a>)" alt="IKEA" >}}

[IKEA](https://www.ikea.com/), without an automatic redirect, but with a very large country selector that understands **domains, endonyms and languages** of the largest countries in the world. The “Go shopping” button might be the biggest button in the world and might deserve a spot in the World Guinness Records Book. Unfortunately, on the site, you can change the country, but not always the language.

While **polite nudging is reasonable**, automatic redirects are not. Once we start moving users from one site to another without asking them at all, we start baking our assumptions into the design, and that’s usually a red flag. We shouldn’t be surprised by increased levels of frustration and abandonment as a result. Ironically, this data is rarely tracked or known as the abandonment is happening on the “other” website, with different departments and teams on the other side of the globe.

Either way, whether we want to nudge users towards a different website, or we absolutely need to use an auto-redirect, it’s definitely a good idea to always allow users to **override redirects** with manual preferences. This requires us to tame our assumptions and decouple our presets.

## Decouple Location and Language Presets

Many websites rely on an assumption that **location, language and currency** are usually tightly coupled. After all, if a user chooses a location in Germany, they are very likely to prefer the German language and see prices in Euro. However, this is based on assumptions that work for many people, but **break the experience entirely** for others.

{{< rimg breakout="true" href="https://www.adidas.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c54d2c5-531a-4f7d-a0c2-de938e96d559/6-designing-better-language-selector.png" width="800" height="484" sizes="100vw" caption="Delivery location and language selection are tightly coupled on <a href='https://www.adidas.de/'>Adidas</a>. It’s impossible to adjust the country and the preferred language separately.  (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c54d2c5-531a-4f7d-a0c2-de938e96d559/6-designing-better-language-selector.png'>Large preview</a>)" alt="Delivery location and language selection are tightly coupled on Adidas. It’s impossible to adjust the country and the preferred language separately." >}}

For example, if you want to purchase sneakers on [Adidas](https://www.adidas.de/) from Germany but deliver them to your friend in Poland, you need to be able to make sense of the Polish language when checking out. You can either choose the German language with delivery to Germany or the Polish language with delivery to Poland. It’s impossible to select the English language with delivery options to Poland, for example. In other words, **both language and location are tightly coupled**.

As it turns out, there are plenty of scenarios where this assumption doesn’t work:

- A person is using a **German VPN**, but not be located in Germany nor understands German;
- A person is connecting from Germany, but be **visiting for a few days**, and they might not speak nor read German at all;
- A person is living in Germany, access a website in German, but prefers to pay with a company’s credit card in USD, rather than in EUR;
- A person is living in Germany might want to deliver an item from an American store to an **American friend**, but keeps getting redirected to a German website;
- A person is connecting from the USA but needs to be able to provide a VAT number because the product will be purchased by a German office with a **German credit card**.

Of course, we might consider all these situations to be **very rare edge cases** and dismiss them. But first, we need to track how many people actually experience such issues and end up leaving as a result. In practice, especially for global brands, these numbers might be more significant than one might think.

These problems appear because we frame common situations in tightly coupled and rather **inflexible presets**. Surely presets are useful as default options, but they break down when defaults aren’t good enough. That’s why it’s usually a good idea to decouple all presets, and allow users to make standalone choices.

{{< rimg breakout="true" href="https://mondraker.com/es/es" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4487f1b3-80ff-4582-84fb-e8cda00968d9/7-designing-better-language-selector.png" width="800" height="513" sizes="100vw" caption="A similar design, but a different approach. On Mondraker, users select location and language separately. <a href='https://mondraker.com/es/es'>Mondraker</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4487f1b3-80ff-4582-84fb-e8cda00968d9/7-designing-better-language-selector.png'>Large preview</a>)" alt="A similar design, but a different approach. On Mondraker, users select location and language separately." >}}

On [Mondraker](https://mondraker.com/es/es), users **select location and language separately**. All countries are grouped into tabs, and at the bottom users can choose the language of their preference. A very similar design, but a quite different approach. A downside: labeling all countries in a selected language is probably not as effective as using corresponding native labels instead.

{{< rimg breakout="true" href="https://monese.com/gb/en" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63fa1fc9-56ea-49b7-9c8e-9ac4fd171227/monese.jpg" width="764" height="423" sizes="100vw" caption="<a href='https://monese.com/gb/en'>Monese</a> with tabs, separating language and country selection. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63fa1fc9-56ea-49b7-9c8e-9ac4fd171227/monese.jpg'>Large preview</a>)" alt="" >}}

[Monese](https://monese.com/gb/en) shows **two tabs** in the right upper corner of the header. Users can switch between language and country, defining preferences for each separately.

User preferences don’t have to be limited by country and language alone. We can allow users to **customize further parts of the UI**, from currency and auto-translation to units of measurement and date formatting.

## Allow Users To Set Custom Preferences

For many sites, language and location are just the first important attributes that convey what website might be a good fit for a customer. However, to deliver value to users, we might want to go a little bit beyond that.

{{< rimg breakout="true" href="https://www.revolve.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b68d4436-0398-4961-873d-303fc190a6d9/9-designing-better-language-selector.png" width="800" height="442" sizes="100vw" alt="Revolve.com" >}}

{{< rimg breakout="true" href="https://www.revolve.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/487e522a-d728-4cf2-aae0-272c7e91c2d1/10-designing-better-language-selector.png" width="800" height="426" sizes="100vw" caption="<a href='https://www.revolve.com/'>Revolve</a> with separate selections for language, country and currency. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/487e522a-d728-4cf2-aae0-272c7e91c2d1/10-designing-better-language-selector.png'>Large preview</a>)" alt="Revolve.com" >}}

[Revolve.com](https://www.revolve.com/) uses **language, country and currency presets** based on the user’s IP and their browser’s locale. However, users can override these presets with custom preferences. They can choose a country for shipping, the language on the site and the currency. The hint for preferences is located in the header, with a combination of a language abbreviation, flag and a currency indicator.

These details are enough to **show all products with the final price** that includes delivery costs to their country and in the currency that’s most familiar to them. That’s what the perfect decoupling of location, language and currency is.

{{< rimg breakout="true" href="https://www.airbnb.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3e27ccb-60b3-4c08-9062-a3b35e1d5fce/11-designing-better-language-selector.png" width="800" height="404" sizes="100vw" alt="" >}}

{{< rimg breakout="true" href="https://www.airbnb.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b34af0e-c9e1-4155-acc6-085a697362a2/12-designing-better-language-selector.png" width="800" height="516" sizes="100vw" caption="The language and country selection are decoupled on <a href='https://www.airbnb.com/'>AirBnB</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1b34af0e-c9e1-4155-acc6-085a697362a2/12-designing-better-language-selector.png'>Large preview</a>)" alt="" >}}

[AirBnB](https://www.airbnb.com/) suggests languages and regions in groups, but also allows users to adjust their preferences and choose a language and region of their choice. Additionally, users can **opt-in to automatically translate descriptions** and reviews to English. The modal is prompted by a tap on the globe icon in the right upper corner of the header.

Once the settings are set, users can jump from one location to another, **compare prices in the same currency** and see reviews automatically translate to a language that they might understand better. That’s undoubtedly a win for the users.

{{< rimg href="https://de.iherb.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd37bf3-01e8-4dcc-a584-b715c599e310/13-designing-better-language-selector.png" width="800" height="1051" sizes="100vw" caption="<a href='https://de.iherb.com'>iHerb</a> with plenty of extra preferences available to users. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fd37bf3-01e8-4dcc-a584-b715c599e310/13-designing-better-language-selector.png'>Large preview</a>)" alt="" >}}

[iHerb](https://de.iherb.com) goes the extra mile by providing a whole range of additional preferences for their users. Not only can users choose their language, preferred currency and shipping destination (and specify it with ZIP code for US destinations) &mdash; they can also choose **preferred units of measure** and check available payment methods and available shipping methods. Bonus points for smart autocomplete input rather than a not-so-good old-fashioned [&lt;select&gt;-dropdown](https://www.fuckdropdowns.com/). 

{{< rimg breakout="true" href="https://www.ssga.com/de/en_gb/institutional/etfs/funds/spdr-sp-500-ucits-etf-dist-spy5-gy" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63d0d8f5-bbd2-4695-8a12-dc860e99218b/14-designing-better-language-selector.png" width="800" height="483" sizes="100vw" caption="<a href='https://www.ssga.com/de/en_gb/institutional/etfs/funds/spdr-sp-500-ucits-etf-dist-spy5-gy'>State Street of Global Advisors</a> provides not only a choice of location, but also settings for roles and types of available sites. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63d0d8f5-bbd2-4695-8a12-dc860e99218b/14-designing-better-language-selector.png'>Large preview</a>)" alt="State Street of Global Advisors" >}}

Some slightly different preferences can be defined on the [State Street of Global Advisors](https://www.ssga.com/de/en_gb/institutional/etfs/funds/spdr-sp-500-ucits-etf-dist-spy5-gy). On the first visit, a modal window appears explaining to users some of the assumptions that the interface is making about the location and their interests. Within the modal window, users can change a location, **specify their role** and choose a preferred type of site for their visit. 

In general, these are some of the useful adjustments that we could allow users to specify to customize the entire experience for them:

- Shipping location
- Preferred currency
- Units of measure
- **Time/date formatting**
- Time zones preferences
- **Level of experience**

The question, of course, is how to **surface all these settings to the user** &mdash; in a separate settings page, as a sidebar, in the header, or the footer? One disputable option is to show the settings in a modal or non-modal window upon entry to the site.

{{% ad-panel-leaderboard %}}

## A Case For Non-Modal Dialogs

Admittedly, modal windows are [rarely a good idea](https://www.nngroup.com/articles/modal-nonmodal-dialog/). They are disruptive and annoying as they require immediate attention. However, they are appropriate when we need to draw the user’s attention to important details &mdash; be it loss of data, mutually exclusive preferences or critical errors.

Some of the websites listed above **prompt a modal window** on the very first visit, asking users to specify their intent and their preferences before using the site. On others, default presets are silently applied, with an option to adjust them if needed &mdash; sometimes in a modal, and sometimes on a dedicated page.

{{< rimg href="https://www.onepeloton.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2597d68b-0e79-4751-868c-b79d879d5980/15-designing-better-language-selector.png" width="800" height="900" sizes="100vw" caption="<a href='https://www.onepeloton.com/'>Peloton</a> provides a choice for country preferences in a modal upon website entry. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2597d68b-0e79-4751-868c-b79d879d5980/15-designing-better-language-selector.png'>Large preview</a>)" alt="Peloton provides a choice for country preferences in a modal upon website entry." >}}

While modal windows will always be noticed, [usability tests show](https://youtu.be/mAiNdU1go1A?t=3744) that they are often **instinctively dismissed**, sometimes even before users realize what content they contain. On the other hand, users often don’t pay attention to any accessory navigation such as choice of currency, measurements or shipping location as they are very much focused on products. It’s only if the change of the language is necessary that they might notice that further settings can be adjusted as well.

{{< rimg breakout="true" href="https://booking.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8ba0d6d-628e-4520-9bc8-af8bc993dc20/16-designing-better-language-selector.png" width="800" height="419" sizes="100vw" alt="Booking" >}}

{{< rimg breakout="true" href="https://booking.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4caba1d-fcb7-4ff4-ad75-47f42d539173/17-designing-better-language-selector.png" width="800" height="632" sizes="100vw" caption="A language selector appearing in a modal on <a href='https://booking.com/'>Booking</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a4caba1d-fcb7-4ff4-ad75-47f42d539173/17-designing-better-language-selector.png'>Large preview</a>)" alt="Booking" >}}

{{< rimg breakout="true" href="https://booking.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9130a99-6bdf-4e6b-9f9c-ef4dbf900cb7/18-designing-better-language-selector.png" width="800" height="593" sizes="100vw" caption="A currency selector with most popular options listed on the top on <a href='https://booking.com/'>Booking</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9130a99-6bdf-4e6b-9f9c-ef4dbf900cb7/18-designing-better-language-selector.png'>Large preview</a>)" alt="Booking" >}}

Rather than using one modal with tabs, [Booking](https://booking.com/) uses **separate buttons** in the header for currency and language. The interface infers some settings from the user and applies them directly, with an option to override these settings. Rather than using a <code>&lt;select&gt;</code>-dropdown, which is often the slowest form component, all options are **displayed in plain text**, hence being searchable by in-browser search.

{{< rimg breakout="true" href="https://www.skyscanner.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f97dfc6-f254-45b4-88c1-1765459a05a2/19-designing-better-language-selector.png" width="800" height="518" sizes="100vw" caption="<a href='https://www.skyscanner.com/'>Skyscanner</a>, with the language, location and currency all decoupled and displayed in a modal window. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f97dfc6-f254-45b4-88c1-1765459a05a2/19-designing-better-language-selector.png'>Large preview</a>)" alt="Skyscanner" >}}

For comparison, [Skyscanner](https://www.skyscanner.com/) allows users to prompt all customization options with one large button, grouping all options in a few drop-downs. Also, the interface always allows users to fall back to the English language if they’ve accidentally made a mistake.

**Which option is better?** Ultimately, this will of course be decided by usability tests. In this particular case, showing a modal window upon entry might not be a bad idea since it provides tangible value to users &mdash; a value that they might not be able to spot otherwise. However, there might be an alternative option that could work even better &mdash; using a **non-modal dialog** instead.

{{< rimg breakout="true" href="https://www.patagonia.com/home/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24eb7a65-0ad6-456d-bda6-0625d946b318/20-designing-better-language-selector.png" width="800" height="477" sizes="100vw" caption="Patagonia uses a non-modal for location and language selection. <a href='https://www.patagonia.com/home/'>Patagonia</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24eb7a65-0ad6-456d-bda6-0625d946b318/20-designing-better-language-selector.png'>Large preview</a>)" alt="Patagonia uses a sticky non-modal for location and language selection." >}}

Upon website entry on [Patagonia](https://www.patagonia.com/home/), a **sticky non-modal dialog** appears in the left bottom corner. Users can choose location and language and save their preferences as a cookie. They can also always bring the selection back by accessing the preferences bar in the footer. 

{{< rimg breakout="true" href="https://www.ssga.com/de/en_gb/institutional/etfs/funds/spdr-sp-500-ucits-etf-dist-spy5-gy" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bccba3f-eb0e-49dd-8258-d01d982a35be/22-designing-better-language-selector.png" width="800" height="510" sizes="100vw" caption="Replacing modals with non-modals is usually a good idea. A mock-up of <a href='https://www.ssga.com/de/en_gb/institutional/etfs/funds/spdr-sp-500-ucits-etf-dist-spy5-gy'>State Street Global Advisors - SPDR</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bccba3f-eb0e-49dd-8258-d01d982a35be/22-designing-better-language-selector.png'>Large preview</a>)" alt="State Street Global Advisors" >}}

In the mock-up above, the important **content isn’t blocked by the modal**; users can scroll, navigate, select and copy-paste. However, the preference pane appears in the bottom right section of the screen. It can also be collapsed or minimized, but it does require an action from the user. It is a little bit more intrusive than when silently placed in the global navigation, but is easier to discover as well.

If you aren’t certain about the best option for your project, consider adding a link in the navigation bar first. Measure [design KPIs](https://www.smashingmagazine.com/2022/04/boosting-ux-with-design-kpis/) and test how they change with a non-modal option — a much **less intruding and more friendly** option — and ultimately a modal. Chances are high that the modals might perform better than one might think.

## Click-Through Menus For Countries

Large corporations know the problem too well: navigating dozens of options in a <strong>small overlay</strong>, or even a large modal is quite cumbersome and requires a **healthy dose of scrolling**. So it’s not very surprising that often websites present all available options on separate pages, broken down by regions and sometimes illustrated with country flags.

{{< rimg breakout="true" href="https://www.revolut.com/en-DE/change-country" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91c91e45-b876-47dc-b9c8-9f25920d0dff/23-designing-better-language-selector.png" width="800" height="525" sizes="100vw" caption="<a href='https://www.revolut.com/en-DE/change-country'>Revolut</a> with all available options displayed on a dedicated page. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/91c91e45-b876-47dc-b9c8-9f25920d0dff/23-designing-better-language-selector.png'>Large preview</a>)" alt="Revolut" >}}

[Revolut](https://www.revolut.com/en-DE/change-country) displays all available options on a separate, dedicated page. The countries are **written in the English language**, organized in groups and listed alphabetically. However, the page doesn’t only showcase available locations, but also locations that aren’t available yet. For this particular case, it might be a good idea to allow users to filter &mdash; e.g. hide all unavailable locations, perhaps with a toggle or tab above the list.

{{< rimg breakout="true" href="https://www.logitech.com/en-us/change-location.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47815086-19ca-40f8-becc-3976efb7bdfd/24-designing-better-language-selector.png" width="800" height="550" sizes="100vw" caption="<a href='https://www.logitech.com/en-us/change-location.html'>Logitech</a> displays languages in their local format — that might be easier to deal with for a truly global audience. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/47815086-19ca-40f8-becc-3976efb7bdfd/24-designing-better-language-selector.png'>Large preview</a>)" alt="Logitech" >}}

[Logitech](https://www.logitech.com/en-us/change-location.html) displays most **languages in their local format** &mdash; e.g. “Deutschland” for Germany, and “中文” for China. This eliminates the assumption that the user needs to understand English to find the country or language of their choice. On the page, all countries (and available languages) are grouped by geography and displayed across columns, making it easier for users to discover them.

{{< rimg href="https://dell.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6455e05-dd05-40e9-b569-2285d5875d5c/25-designing-better-language-selector.png" width="800" height="723" sizes="100vw" caption="Countries grouped into tabs on <a href='https://dell.com/'>Dell</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6455e05-dd05-40e9-b569-2285d5875d5c/25-designing-better-language-selector.png'>Large preview</a>)" alt="Dell" >}}

Rather than displaying all available options on one long page, [Dell](https://dell.com/) breaks countries by regions within **tabs**. No flags are being used, making the scanning a bit more difficult. Countries and languages are combined. In this case, less scrolling is required to find a location that would fit users best.

{{< rimg href="https://www.cisco.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2fd9092-d5d1-48f7-ae55-970c7b2feb2b/26-designing-better-language-selector.png" width="800" height="700" sizes="80vw" caption="Vertical tabs in action on <a href='https://www.cisco.com/'>Cisco</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2fd9092-d5d1-48f7-ae55-970c7b2feb2b/26-designing-better-language-selector.png'>Large preview</a>)" alt="Cisco" >}}

Not all tabs are alike though. [Cisco](https://www.cisco.com/) uses a small overlay with **vertical tabs**, rather than horizontal ones. This makes the selection very compact, and the solution very straightforward. It’s worth noting that the main disadvantage of tabs is that they make the content inaccessible with an in-browser search (well, [for now](https://twitter.com/addyosmani/status/1520459804656824320)). The user always has to select a region first.

{{< rimg breakout="true" href="https://www.edreams.gr/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/738ff172-4cea-464e-88c4-b90673eda4cc/27-designing-better-language-selector.png" width="800" height="761" sizes="100vw" caption="<a href='https://www.edreams.gr/'>eDreams</a> with accordions in action. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/738ff172-4cea-464e-88c4-b90673eda4cc/27-designing-better-language-selector.png'>Large preview</a>)" alt="eDreams" >}}

Another option, of course, is to group the countries with a **vertical accordion**, as it’s done on [eDreams](https://www.edreams.gr/), for example. You might need a bit more vertical space as a result, but all options can be scanned from top to bottom in one go.

{{< rimg breakout="true" href="https://www.oracle.com/index.html" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93e870cc-5400-4dac-a225-899021f3eb0e/63-designing-better-language-selector.png" width="800" height="" sizes="100vw" caption="<a href='https://www.oracle.com/index.html'>Oracle</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93e870cc-5400-4dac-a225-899021f3eb0e/63-designing-better-language-selector.png'>Large preview</a>)" alt="Oracle" >}}

A slightly different kind of country selector on [Oracle](https://www.oracle.com/index.html): a **click-through overlay menu**, with all countries grouped, rather than displaying a standalone page. That’s a very compact and straightforward solution.

If you need to display a wide range of languages, explore if you can group and display them on a single page. If it’s getting too overwhelming, consider grouping them within accordions or tabs &mdash; assuming that tabs appear like tabs and don’t contain cryptic labels. Or even better: provide users with poignant autocomplete suggestions.

## Show Autocomplete Suggestions

Getting autocomplete right isn’t an easy task. This is especially difficult if we are dealing with multiple pieces of information at once, i.e. both country and language. For it to work well, we need to **support frequent abbreviations**, [endonyms](https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_and_their_capitals_in_native_languages), and shorthands for all available options. And then, of course, our autocomplete suggestions should display both countries and languages, with an option to choose one option or another. Plus, we also might want to consider the support of multiple “primary” languages (English, French, Spanish, to name a few). Thats’ not easy at all!

{{< rimg breakout="true" href="https://frame.work/de/en/locale/edit" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24fff3ea-2a49-4bbd-bcdc-37e92bb4b365/64-designing-better-language-selector.png" width="909" height="23" sizes="100vw" caption="<a href='https://frame.work/de/en/locale/edit'>Framework</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24fff3ea-2a49-4bbd-bcdc-37e92bb4b365/64-designing-better-language-selector.png'>Large preview</a>)" alt="Framework" >}}

On [Framework](https://frame.work/de/en/locale/edit), users can select country and language separately, both with autocomplete, with the **most frequent options highlighted** on focus. There is no need to scroll through the list of countries to find the preferred option. While this might be perfectly enough for some scenarios, it might not be sufficient in a situation when the user’s country isn’t available in the list. Instead, we could indicate the **closest locations** to the preferred option, rather than guiding a user to a dead end.

{{< rimg href="https://frame.work/de/en/locale/edit" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92d45ad8-c24b-4bb3-b5fb-a07e6a0bbb3c/30-designing-better-language-selector.png" width="800" height="638" sizes="80vw" caption="We could allow users to jump to the locations nearby. Just a mock-up. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/92d45ad8-c24b-4bb3-b5fb-a07e6a0bbb3c/30-designing-better-language-selector.png'>Large preview</a>)" alt="Framework" >}}

In the mock-up above, **“4 locations nearby”** could open an accordion, highlighting the closest locations next to Lithuania (*Lietuva),* indented.  This pattern might not be applicable when a user is trying to open a new bank account, but it might be useful when a user is looking for a particular office in their country, but can’t locate it.

{{< rimg href="https://wise.com" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83e6d480-3ce5-4715-ab00-292445d969ea/31-designing-better-language-selector.png" width="800" height="653" sizes="100vw" caption="<a href='https://wise.com'>Wise</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83e6d480-3ce5-4715-ab00-292445d969ea/31-designing-better-language-selector.png'>Large preview</a>)" alt="Wise" >}}

[Wise](https://wise.com) also includes autocomplete for language settings. If the same language appears in multiple items, the autocomplete specifies what country it refers to. All language options are presented in their local format.

{{< rimg href="https://www.porsche.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7f1725a-990b-43f6-9cc5-f57473c57e8b/32-designing-better-language-selector.png" width="800" height="528" sizes="100vw" caption="<a href='https://www.porsche.com/'>Porsche</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7f1725a-990b-43f6-9cc5-f57473c57e8b/32-designing-better-language-selector.png'>Large preview</a>)" alt="Porsche" >}}

[Porsche](https://www.porsche.com/) uses an accordion along with autocomplete as a page overlay. The interface supports abbreviations and indicates available options with flag icons.

Undoubtedly autocomplete is a great addition to language selection. However, when testing it, explore how people use autocomplete, and what they are actually typing to find their country. Sometimes the **fine-tuning of making autocomplete work** for many different languages might be an effort way too underestimated and way too time-consuming. 

## Grouping Countries

Not every location or language has to represent with a separate entry in the language selector. If multiple countries are speaking the same language, what if indicated by grouping countries within one option?

{{< rimg breakout="true" href="https://dribbble.com/shots/2386084-Language-Selection-Modal/attachments/9275096?mode=media" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4044800c-6c28-484d-b5ab-0ece50411fd8/33-designing-better-language-selector.png" width="800" height="600" sizes="100vw" caption="Can we groupo countries and languages? A mock-up by <a href='https://dribbble.com/shots/2386084-Language-Selection-Modal/attachments/9275096?mode=media'>Daniel Marchini</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4044800c-6c28-484d-b5ab-0ece50411fd8/33-designing-better-language-selector.png'>Large preview</a>)" alt="Daniel Marchini" >}}

Daniel Marchini has come up with an [interesting concept](https://dribbble.com/shots/2386084-Language-Selection-Modal/attachments/9275096?mode=media) of **grouping flags within a single selection**. If the content will appear exactly the same for multiple countries, is it really necessary to show them separately? For example, the Portuguese language is displayed as an option for Portugal and Brazil, while the Spanish language is highlighted for Mexico and Spain. Obviously, not all countries could be grouped this way, but if you target users from specific countries, this might be worth a shot.

{{< rimg href="https://www.airwallex.com/eu" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4218426-66cd-40d0-b95d-daf126ba15ef/34-designing-better-language-selector.png" width="800" height="901" sizes="100vw" caption="European Union representing all European countries at once, on <a href='https://www.airwallex.com/eu'>Airwallex</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4218426-66cd-40d0-b95d-daf126ba15ef/34-designing-better-language-selector.png'>Large preview</a>)" alt="Airwallex" >}}

[Airwallex](https://www.airwallex.com/eu)’s country selector groups all European countries as “European Union”. The service is available in the **entire European Union**, so it’s not necessary to select an individual country. However, if you have a slightly longer list of options, and you are looking for an option to open a bank account in the Netherlands, you might need a bit of time to realize that the Netherlands is assumed as a country within the European Union.

## Use Flags For Countries, Text Labels For Languages

When designing a country selector, it feels almost natural to think about the flags they are represented by. After all, compared to just plain text, it should be much easier for users to locate the icon that they can immediately recognize. This is indeed true, however, as James Offer has suggested in his wonderful blog on [Flags are not languages](http://www.flagsarenotlanguages.com/blog/), flags are specific to countries, but **languages often cross borders**.

We can find French-speaking people in Canada, Vietnam, Senegal, Switzerland, and many other countries. It would be inaccurate to assume that all users from these countries associate their choice of language with a French flag. 

{{< rimg href="https://uxdesign.cc/my-take-on-language-selectors-945caceb58f7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8c6a273-46ac-404c-9329-5717c41ba600/36-designing-better-language-selector.png" width="800" height="417" sizes="80vw" caption="<a href='https://uxdesign.cc/my-take-on-language-selectors-945caceb58f7'>Zsolt Szilvai</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8c6a273-46ac-404c-9329-5717c41ba600/36-designing-better-language-selector.png'>Large preview</a>)" alt="Zsolt Szilvai" >}}

In the article “[My Take On Language Selectors](https://uxdesign.cc/my-take-on-language-selectors-945caceb58f7)”, Zsolt Szilvai shows an interesting example of such a conundrum. During the usability tests of an application designed for the UAE, many people found the fact that the Arabic language was visualized with one single flag, as it is used in many countries and cannot be identified with any particular flag alone.

{{< rimg breakout="true" href="https://www.curve.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11512b03-5609-47ad-a9af-a0c40fdb9a7d/65-designing-better-language-selector.png" width="800" height="499" sizes="100vw" caption="<a href='https://www.curve.com/'>Curve</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11512b03-5609-47ad-a9af-a0c40fdb9a7d/65-designing-better-language-selector.png'>Large preview</a>)" alt="Curve" >}}

[Curve.com](https://www.curve.com/) opts in for a default international version which is available in English. There are a few other options available as well but one might wonder about the difference between “International (English)” and “English (United States)”. When flags are used to indicate languages, it can quickly become a little bit confusing.

{{< rimg breakout="true" href="https://www.backmarket.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b7e3224-7d89-4954-8e69-4b374c42cc5e/39-designing-better-language-selector.png" width="800" height="303" sizes="100vw" caption="<a href='https://www.backmarket.com/'>Backmarket</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b7e3224-7d89-4954-8e69-4b374c42cc5e/39-designing-better-language-selector.png'>Large preview</a>)" alt="Backmarket" >}}

[Backmarket](https://www.backmarket.com/) includes a **list of flags in the footer** of the page to indicate local sites of the marketplace. When we want to drive users to specific local websites, we can safely use flags that best represent countries, rather than languages. Many sites also just add links in the footer instead, making language labels easier to find with an in-browser search.

{{< rimg href="https://www.bol.com/nl/nl/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b843148-26fe-4727-8711-62c516c5c937/40-designing-better-language-selector.png" width="800" height="691" sizes="100vw" caption="<a href='https://www.bol.com/nl/nl/'>Bol</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b843148-26fe-4727-8711-62c516c5c937/40-designing-better-language-selector.png'>Large preview</a>)" alt="Bol" >}}

Flags for countries, and plain text for languages. Everything seems to be about right on [Bol.com](https://www.bol.com/nl/nl/). The country selector (with a flag) is located in the right upper corner, where most users expect it.

To avoid misunderstandings, make sure that you use flags if your users need to select a **specific country**. However, if you’re providing users with a choice of a **specific language**, then flags are probably not going to work well. There, an autocomplete with all available countries and labels for languages written next to them might work better.

This of course brings up a question: how should these labels actually be written? In English or in a language’s local format?

## Label Languages Locally

Assumptions are error-prone, and if it goes for combinations of currency, language and location, this holds true for how we label languages as well. We shouldn’t assume that a user will be speaking one of the languages we choose to see as a default option. Instead, when users select a language, usually it’s better to always use the name of the language **in its local format**.

So rather than offering a choice of *German* and *Chinese*, assuming that users understand English, we can label these options as *Deutsch* and *中文*.

{{< rimg href="https://stripe.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6bc7abb-fd85-4e41-8e7e-42cb254543f7/41-designing-better-language-selector.png" width="800" height="1175" sizes="100vw" caption="On <a href='https://stripe.com/'>Stripe</a>, each language is labelled locally. No flags in use. <a href=''>Stripe</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6bc7abb-fd85-4e41-8e7e-42cb254543f7/41-designing-better-language-selector.png'>Large preview</a>)" alt="Stripe" >}}

But if the languages are labeled locally, somebody who happens to be in China might be experiencing issues switching to a slightly more familiar language. Surely flags would help to locate a button that would allow for that, but we could also **prefix the selected language with a label**, for example, “Language” to make it easier to spot the selector. Or we could just add a link saying “English” in the header. This of course relies on assumptions we are making, but it might be easier than hopping through the navigation bar and view-source with fingers crossed.  

{{< rimg breakout="true" href="https://booking.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ebb517-4ae3-4b08-9b7c-6b9e8f6a8e6b/66-designing-better-language-selector.png" width="800" height="351" sizes="100vw" caption="<a href='https://booking.com/'>Booking</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00ebb517-4ae3-4b08-9b7c-6b9e8f6a8e6b/66-designing-better-language-selector.png'>Large preview</a>)" alt="Booking" >}}

[Booking](https://booking.com/) provides a hint to indicate that users can change the language in a local language. If you prefer to show a hint on hover, that’s one of the very few cases where one might consider using a language that many users would understand, and it could be English.
 
{{< rimg href="https://booking.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e25fc2d-cf29-4872-a2be-08deea0c49b3/45-designing-better-language-selector.png" width="800" height="383" sizes="100vw" caption="<a href='https://booking.com/'>Booking</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e25fc2d-cf29-4872-a2be-08deea0c49b3/45-designing-better-language-selector.png'>Large preview</a>)" alt="Booking" >}}

{{% ad-panel-leaderboard %}}

## The Globe and Translate Icons

Since flags can be somewhat problematic, what would be a reasonable alternative to them? As briefly mentioned at the beginning of the article, we can also use icons such as “Globe” or “Translate” to indicate the choice of locales. There is as well an [official language icon](http://www.languageicon.org/), which is free to use, but unfortunately is still not as recognizable as the other icons.

{{< rimg breakout="true" href="https://uxdesign.cc/designing-language-selectors-that-work-well-with-assistive-technology-c645a16e73e7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97a39647-f975-4089-88e1-4f110ee3f7cb/47-designing-better-language-selector.png" width="800" height="258" sizes="100vw" caption="Language selector buttons with icons. Icon 1 shows the earth, icon 2 shows two letters from different alphabets. Designed by Zsolt Szilvai. <a href='https://uxdesign.cc/designing-language-selectors-that-work-well-with-assistive-technology-c645a16e73e7'>Zsolt Szilvai</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97a39647-f975-4089-88e1-4f110ee3f7cb/47-designing-better-language-selector.png'>Large preview</a>)" alt="Language selector buttons with icons. Icon 1 shows the earth, icon 2 shows two letters from different alphabets" >}}

Surely not everybody will be able to understand the icon in combination with a word that they can barely decipher, but if it’s prominently located in the header or the footer, the chance to be discovered are significantly higher.

{{< rimg href="https://www.tomorrow.one/en-EU/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efbe04fc-8e61-4471-9fa8-5381431ead89/48-designing-better-language-selector.png" width="800" height="536" sizes="100vw" caption="<a href='https://www.tomorrow.one/en-EU/'>Tomorrow</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efbe04fc-8e61-4471-9fa8-5381431ead89/48-designing-better-language-selector.png'>Large preview</a>)" alt="Tomorrow" >}}

[Tomorrow.one](https://www.tomorrow.one/en-EU/) displays a large drop-down selector with a globe icon in the footer of each page. It’s not available in the header on the site. Because pages aren’t very long, that’s probably not a big problem, but users might give up if they have to embark on a long-running scrolling marathon, or if the [infinite scroll](https://www.smashingmagazine.com/2022/03/designing-better-infinite-scroll/) prevents them from reaching the footer.

{{< rimg breakout="true" href="https://www.atlassian.com/it/software/jira" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4aa08b40-3b51-4b17-9c62-925d6b443ac9/49-designing-better-language-selector.png" width="800" height="490" sizes="100vw" caption="<a href='https://www.atlassian.com/it/software/jira'>Atlassian</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4aa08b40-3b51-4b17-9c62-925d6b443ac9/49-designing-better-language-selector.png'>Large preview</a>)" alt="Atlassian" >}}

On [Atlassian](https://www.atlassian.com/it/software/jira), the language selector is tucked at the very end of the page in the footer, with a globe icon indicating the selection. However, if the user with a different browser language preference enters the site, it **suggests changing the language** at the very top of the page, with a globe icon appearing there, too.

{{< rimg breakout="true" href="https://monday.com/lang/ko/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac61ad17-d208-494e-8d06-599185c32658/51-designing-better-language-selector.png" width="800" height="391" sizes="100vw" caption="<a href='https://monday.com/lang/ko/'>Monday</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac61ad17-d208-494e-8d06-599185c32658/51-designing-better-language-selector.png'>Large preview</a>)" alt="Monday" >}}

[Monday.com](https://monday.com/lang/ko/) keeps the language selection at the very top of the page, in the left upper corner. All options are presented in **three columns**, with the current selection highlighted in blue.

<!-- [=[{{< rimg breakout="true" href="https://ec.europa.eu/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7167303-1c60-4103-be08-22bf57b2c174/53-designing-better-language-selector.png" width="800" height="788" sizes="100vw" caption="<a href='https://ec.europa.eu/'>European Commison</a> (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7167303-1c60-4103-be08-22bf57b2c174/53-designing-better-language-selector.png'>Large preview</a>)" alt="European Commison" >}}

The [European Commison](https://ec.europa.eu/) website doesn’t use flags but rather labels that are ordered by alphabet, in the language’s local format. The alphabet helps users find their options. Also, the active selection is clearly highlighted as such. That’s an alternative to flags. -->

While flags are easier to recognize, icons can work as an alternative option as well, especially if you need to provide users with language options, rather than choices for location. Even if the selection is provided in the header, it’s a safe bet to also place it at the bottom to ensure that users can find it when they need to. 

## Avoid Language Shorthands or Initials

Another interesting problem that Zsolt Szilvai has [discovered](https://uxdesign.cc/my-take-on-language-selectors-945caceb58f7shows) in testing is related to the use **abbreviations, initials or shorthands** to indicate a particular language. When we are running out of space in navigation, we could be using “EN” for English, or “DE” for Germany, or “UA” for Ukraine. Indeed, these shorthands are often well-understood, but they bring surprising results when a user’s browser auto-translates all websites in a particular language.

{{< rimg href="https://uxdesign.cc/my-take-on-language-selectors-945caceb58f7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5613484-7ffd-4d5c-9efa-ee7c323c51be/decathlon.png" width="800" height="377" sizes="100vw" caption="<a href='https://uxdesign.cc/my-take-on-language-selectors-945caceb58f7'>Decathlon</a> with quite surprising language options on mobile (on the right). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5613484-7ffd-4d5c-9efa-ee7c323c51be/decathlon.png'>Large preview</a>)" alt="Decathlon" >}}

Not only does it often result in broken menus and surprising layouts; **browsers also translate language shorthands**, producing an interface that might be very difficult to make sense of. However, were the shorthands avoided in favor of the full local name of the language, the user wouldn’t have to deal with these issues at all. Instead, the translator would help them find a language that would work better for them.

{{< rimg href="https://uxdesign.cc/my-take-on-language-selectors-945caceb58f7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e234f38-b784-42f4-81f7-c246166608b0/56-designing-better-language-selector.png" width="800" height="721" sizes="100vw" caption="<a href='https://n26.com/en-eu'>N26</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e234f38-b784-42f4-81f7-c246166608b0/56-designing-better-language-selector.png'>Large preview</a>)" alt="N26" >}}

[N26.de](https://n26.com/en-eu) uses a shorthand “EN” for “English”. The selected language is **disabled in the list of options**, but it’s probably a good idea to increase the color contrast a little. As users scroll down the page, the header remains sticky, so there is really no need to display the language selector in the footer as well.

{{< rimg href="https://wise.com/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7ed3ac-091e-4c3e-a198-c2a8e4924553/57-designing-better-language-selector.png" width="909" height="480" sizes="100vw" caption="<a href='https://wise.com/'>Wise</a>, with languages displayed in full in a drop-down. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac7ed3ac-091e-4c3e-a198-c2a8e4924553/57-designing-better-language-selector.png'>Large preview</a>)" alt="Wise" >}}

[Wise](https://wise.com/) uses shorthands for language selection in the right upper corner, but displays the **languages in full** on click, with a noticeable focus style to indicate where a user currently is. This avoids the problem of auto-translation that often turns abbreviations into seemingly random strings.

## Wrapping Up

The country and language selector might appear like a quite trivial design challenge, but there are plenty of fine details that make or break the experience. When designing one, always **decouple presets** and reduce assumptions about groups that are likely to go together. Users expect the language selector to be located in the header or the footer of each page, and they often watch out for flags, “Globe” or “Translate” icons to find it.

If you have just a few languages, a drop-down overlay might be perfectly enough. If you need 10–15 languages, perhaps it’s worth exploring the option of a non-modal overlay with autocomplete. If there are even more options to display, consider using a standalone page, with countries grouped into tabs or accordions.

## Language Selector Checklist

As usual, here’s a general checklist of a few **important guidelines to consider** when designing a better language selector:

- **Nudge users**, but avoid auto-redirects.
- Decouple presets, be it location, language, or anything else.
- Allow users to set **custom preferences** (currency, time zones, units of measure).
- Consider using a **non-modal dialog**.
- Organize countries and languages in sections, tabs, and accordions.
- Provide input with **autocomplete suggestions**.
- Use flags for countries, but avoid them for languages.
- Consider the *Globe* and *Translate* icons instead of flags.
- **Label languages locally**, e.g. *Deutsch* instead of *German*.
- Avoid language shorthands or initials.
- For accessibility reasons, make sure the country selector appears in the header as well as in the footer, and is keyboard-accessible.


## Meet Smart Interface Design Patterns

If you are interested in similar insights around UX, take a look at [**Smart Interface Design Patterns**](https://smart-interface-design-patterns.com/), our shiny new **9h-video course** with 100s of practical examples from real-life projects. Design patterns and guidelines on everything from mega-dropdowns to complex enterprise tables &mdash; with 5 new segments added every year. *Just sayin’!* [Check a free preview](https://www.youtube.com/watch?v=aSP5oR9g-ss).

<figure style="margin-bottom: 0"><a href="https://smart-interface-design-patterns.com/"><img style="border-radius: 11px" decoding="async" fetchpriority="low" width="950" height="492" srcset="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 400w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_800/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 800w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1200/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1200w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_1600/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 1600w,
https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_2000/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg 2000w" src="https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cc4e1de-6921-474e-a3fb-db4789fc13dd/b4024b60-e627-177d-8bff-28441f810462.jpeg" sizes="100vw" alt="Smart Interface Design Patterns"></a><figcaption class="op-vertical-bottom">Meet <a href="https://smart-interface-design-patterns.com/">Smart Interface Design Patterns</a>, our new video course on interface design &amp; UX.</figcaption></figure>

<div class="btn--lined btn--lined--white-border" style="margin-top: 0.75em; margin-bottom: 0.75em"><a class="btn btn--large btn--green btn--text-shadow" href="https://smart-interface-design-patterns.com/">Jump to the video course&nbsp;&rarr;</a></div>

<p class="ticket-price__desc" style="font-size: .8em!important; text-align: center; line-height: 1.5; margin: 0; display: block;">100 design patterns &amp; real-life 
examples.<br>9h-video course + live UX training. <a href="https://www.youtube.com/watch?v=aSP5oR9g-ss">Free preview</a>.

## Resources

- [Flags are not languages](http://www.flagsarenotlanguages.com/blog/), a blog by James Offer
- [“My take on language selectors”](https://uxdesign.cc/my-take-on-language-selectors-945caceb58f7) + [accessible implementation details](https://uxdesign.cc/designing-language-selectors-that-work-well-with-assistive-technology-c645a16e73e7), by Zsolt Szilvai
- [UX practice: Skyscanner’s language selector](https://medium.com/nyc-design/ux-practice-skyscanners-language-selector-276167b4ed84)
- [Language switching UI/UX on multilingual sites](https://www.robertjelenic.com/language-switching-ui-ux-on-multilingual-sites/), by Robert Jelenic
- [Best practices for presenting website language selection](https://www.robertjelenic.com/language-switching-ui-ux-on-multilingual-sites/)
- [UI/UX design of a language selector](https://share-design.kr/en/article/ui-ux-design/1)
- [Interesting language selector patterns on Siemens Design System](https://ux.siemens-healthineers.com/ui-marcom/components/language-selection/usage/index.html)
- [Designing a language switch: Examples and best practices](https://usersnap.com/blog/design-language-switch/), by Thomas Peham

## Related Articles

If you find this article useful, here’s an overview of similar articles we’ve published over the years &mdash; and a few more are coming your way.

- [Designing A Better Infinite Scroll](https://www.smashingmagazine.com/2022/03/designing-better-infinite-scroll/)
- [Designing Better Breadcrumbs](https://www.smashingmagazine.com/2022/04/breadcrumbs-ux-design/)
- [Designing A Better Carousel UX](https://www.smashingmagazine.com/2022/04/designing-better-carousel-ux/)
- [Designing A Better Accordion](https://www.smashingmagazine.com/2017/06/designing-perfect-accordion-checklist/)
- [Designing A Better Responsive Configurator](https://www.smashingmagazine.com/2018/02/designing-a-perfect-responsive-configurator/)
- [Designing A Better Birthday Picker](https://www.smashingmagazine.com/2021/05/frustrating-design-patterns-birthday-picker/)
- [Designing A Better Date and Time Picker](https://www.smashingmagazine.com/2017/07/designing-perfect-date-time-picker/)
- [Designing A Better Feature Comparison](https://www.smashingmagazine.com/2017/08/designing-perfect-feature-comparison-table/)
- [Designing A Better Slider](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/)
- “[Form Design Patterns Book](https://www.smashingmagazine.com/printed-books/form-design-patterns/),” written by Adam Silver

{{< signature "il" >}}

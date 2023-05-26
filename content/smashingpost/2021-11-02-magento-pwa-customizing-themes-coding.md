---
title: 'Creating A Magento PWA: Customizing Themes vs. Coding From Scratch'
slug: magento-pwa-customizing-themes-coding
author: alex-husar
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77155632-96bd-44a8-af99-50ebad7534e6/magento-pwa-customizing-themes-coding.jpg
date: 2021-11-02T12:00:00.000Z
summary: >-
  This article sheds the spotlight on Magento PWAs and explains why business owners are getting them (often instead of native applications). Alex Husar introduces ways of how progressive web applications can be developed on Magento, as well as go over the major pros and cons of each development path.
description: >-
  This article sheds the spotlight on Magento PWAs and explains why business owners are getting them (often instead of native applications). Alex Husar introduces ways of how progressive web applications can be developed on Magento, as well as go over the major pros and cons of each development path.
categories:
  - PWA
  - Magento
  - Performance
  - Coding
---

When dealing with e-commerce at some point, you probably have heard, and perhaps used Magento, an open-source e-commerce platform. However, what if you want to build a progressive web app with Magento? Is it a good idea, why would you want to build it, and how would you go around building it?

## Why Do Business Owners Opt For Magento PWAs In The 2020s?

PWAs have been around for over five years, yet native applications outnumber them both in the quantity ratio and how many times users download them.

But here are some recent PWA-related findings by [Maximiliano Firtman](https://firt.dev/pwa-2021) regarding Chrome:

- The number of origins with PWAs grew 170% in 2020.
- Furthermore, the same resource states that during the last year, the use of Service Workers has also expanded by 38%.
- However, at the end of 2020, about 1% of websites included a Service Worker, and 2.2% had an installable Web App Manifest file.

### What Does This Mean?

Progressive web applications haven’t pushed out native apps to the extent that was expected yet. But many, including [Gartner](https://www.gartner.com/en/documents/3906717/how-progressive-web-apps-improve-digital-commerce-experi), believe that PWAs are the future of mobile sales that’ll overtake the market in the 2020s:

<blockquote>“Progressive web apps are a cost- and a skills-effective way to reach a wide audience with a close-to-native app experience that supports the full customer life cycle. Application leaders for digital commerce technologies must plan for PWAs when designing digital commerce experiences”.</blockquote>

Numerous big players have considered such an opinion and have recently implemented this technology. Some of the names include Amazon’s Luna, TikTok, Tinder, among many online retailers.

As a matter of fact, progressive web applications have already brought conversion benefits to a significant number of brands. Dozens of companies that have launched PWAs reached impressive results, showing the profitability of such a decision. Let’s look at some numbers:

- Since the launch of their PWA, [Trivago](https://www.thinkwithgoogle.com/intl/en-154/marketing-strategies/app-and-mobile/trivago-embrace-progressive-web-apps-as-the-future-of-mobile/) enhanced engagement, saw more than a 97% increase in click-outs to hotel offers, and evidently boosted its conversion.
- Based on the data provided by [divante](https://go.divante.com/top-30-progressive-web-apps)’s findings on 30 PWA case studies, progressive web apps have a 36% larger mobile conversion rate than native applications.

*“But these are mostly big players,”* you might think. *“Would small or middle-sized companies get any tangible return on investment from PWAs?”* Yes, they will.

- For instance, [Magento PWA statistics](https://www.pwastats.com/tags/conversions) suggest that the Butcher of Blue online store experienced a 169% increase in conversions after their progressive web app launch. The Rooted Objects brand saw 162% conversion growth, what a tangible boost!
- Moreover, Garten-und-Freizeit, a German e-commerce store that sells furniture, saw an amazing improvement in their metrics after getting a PWA. They achieved an almost [40% bounce rate decrease and over 350% additional active users](https://www.vuestorefront.io/case-studies/garten-und-freizeit) on their VueJS-based Magento progressive web app.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/126e9642-1fe9-4d7b-b4fa-9ebb32064b66/6-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/126e9642-1fe9-4d7b-b4fa-9ebb32064b66/6-creating-magento-pwa-customizing-themes-coding.png" width="800" height="590" sizes="100vw" caption="Image credit: <a href='https://www.garten-und-freizeit.de'>Garten-und-Freizeit</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/126e9642-1fe9-4d7b-b4fa-9ebb32064b66/6-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="Screenshots of the Garten-und-Freizeit website" >}}

## 5 Major Benefits Of Magento PWAs

There are several advantages of choosing in favor of progressive web applications, especially if we’re talking about massive Magento e-commerce stores. Below are some main things to consider.

### 1. Cost-Efficient And Effort-Saving Development

Perhaps these two points are worth mentioning first of all. Building a PWA is cheaper than a native application.

One of the reasons for that is because a PWA has the same code base. So unlike the case with native applications, the progressive web app needs to be coded only once. I.e., you don’t have to create code to fit the separate Android and iOS requirements.

This also implies that you don’t have to spend additional time and money on creating a PWA to suit various devices, greatly speeding up time-to-market. Why is that? Read point 2.

{{% feature-panel %}}

### 2. PWAs Work In Browsers

Unlike their native application “antecedents”, progressive web apps are **launched in browsers**. There are several things to bring up due to this.

#### Findable Pages

As PWAs work in browsers, they have web pages with URLs that work just like any other website (be it launched on a desktop or mobile device).

Following from the above, an undeniable strength of PWAs, when compared to native applications, is that their **pages are findable via search engines**. The pages can be crawled, indexed, and ranked, as it happens with regular websites. This is good news for an e-commerce store’s SEO (since if appropriately optimized, the pages can “grow” organically).

To compare, native applications installed on devices from app markets can’t boast having the same. For instance, the product pages of an e-commerce store’s native app don’t come in sight of search engines. Hence, they can’t be promoted separately or found by users who’ve input a search query in Google. You need a site for that.

Below is an example of the Netatmo PWA. As shown on the screenshots below, the product page of the store can be found via Google. That wouldn’t be the case if they opted for a native application.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9092dba-074e-4043-8ad5-e1ab357d708b/3-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9092dba-074e-4043-8ad5-e1ab357d708b/3-creating-magento-pwa-customizing-themes-coding.png" width="800" height="590" sizes="100vw" caption="Image credit: <a href='http://www.netatmo.com'>Netatmo</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9092dba-074e-4043-8ad5-e1ab357d708b/3-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="Screenshots of the Netatmo website" >}}

#### Installing A PWA To The Device Isn’t Obligatory

Here’s one more point worth noting. **PWAs don’t require installation from the App Store or Google Play** to the device to be used (like native apps do).

Again, PWAs are sites that run in browsers. Users who opened a PWA from a smartphone’s browser might even not be aware that they’re using a progressive web app, assuming that it’s just a well-performing site.

But for the convenience of shoppers, PWAs can be easily added to the home screen of the device. Such shortcuts look like any other native app icon, but their weight is unnoticeable to a user. On the contrary, a native application of an e-commerce store can come at 30, 50, or even 100 MB and up, consuming internal device storage. 

Check out how the “Add to Home Screen” feature works on the example below taken on the Apivita Magento PWA.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/125c1336-5392-46bf-a41d-9b992b152c24/12-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/125c1336-5392-46bf-a41d-9b992b152c24/12-creating-magento-pwa-customizing-themes-coding.png" width="800" height="590" sizes="100vw" caption="Image credit: <a href='https://www.apivita.com'>Apivita</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/125c1336-5392-46bf-a41d-9b992b152c24/12-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="Screenshots of the Apivita website" >}}

You might ask: *“But do people install PWA apps at all? And how many do so?”*

Here’s the thing, most mobile users who have opened a PWA in their browser might not realize they’re using a progressive web app. Just look at the screenshots that we’ve shown. At first glance, they all look like well-brushed-up mobile versions of sites. You probably won’t be able to tell whether it’s a PWA or not. But who cares? Well-executed PWA sites are a blast to use. 

The bottom line here is that these sites help to convert. So the question should be *“Does it matter how many people install PWAs?”* The answer is *“Probably not”*. This isn’t the case like with native applications whose success is at times predefined by the number of downloads.

In fact, according to [Google statistics](https://www.thinkwithgoogle.com/marketing-strategies/app-and-mobile/shopping-app-usage-statistics):

<blockquote>“Half of the users who are shopping via their smartphones are likely to access a shop’s mobile site because they aren’t willing to download the application from the marketplace.”</blockquote>

This is especially true for those who want to make one-time purchases. Therefore, we can conclude that it is reasonable to raise your store’s game by optimizing it for m-commerce. This primarily regards its UX\UI and speed, so a progressive web app can be a solution to consider.

### 3. The Design Gives Ground For Utmost Usability

Speaking of UX\UI, just like their native app “ancestors”, progressive web applications emphasize **enhanced usability**. Navigation, elements placement, and the overall “look” of PWAs are very familiar to regular downloadable applications. But this “look” is now available in browsers.

Because the focus is put on mobile-first, customers become happier with their browsing experience, increasing the store’s conversions.

Alibaba is one of the e-commerce giants that have “run the gamut” from a regular online retail store to a native application (created for mobile shopping purposes) and then on to a PWA. Although their native app was in great demand by clients, they decided to get a progressive web application to provide flawless UX for those who use the browser to shop on their site. As a result, they’ve tailored to the needs of their acquired clients (who habitually use the native app regularly) and made shopping easy for those customers who have accessed their site from a browser.

Let’s compare the look of Alibaba’s PWA and native app. I’ve used and added both to my iPhone to check out how they differ. The icons look the same on the home screen. Yet, the native application weighs 183.4 MB. So, I personally prefer to use the browser version.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27a72ff4-3653-488c-b5b2-a79a641bc576/5-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27a72ff4-3653-488c-b5b2-a79a641bc576/5-creating-magento-pwa-customizing-themes-coding.png" width="800" height="353" sizes="100vw" caption="Image credit: <a href='https://www.alibaba.com'>Alibaba</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27a72ff4-3653-488c-b5b2-a79a641bc576/5-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="Screenshots of the Alibaba website" >}}

Curiously, the native application seems to be more prioritized by the company. When you access the store from a browser, you are offered to go to the app market to download the native application.

In any case, the PWA has a neat design that reminds the style of a native application. We see that many elements that are important to the user are shown above the fold, space is used rationally, there’s a bottom menu bar that’s easy to reach by thumb, among other convenient design choices.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afbb6c16-9405-4701-9aba-b8f3963ff8f4/9-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afbb6c16-9405-4701-9aba-b8f3963ff8f4/9-creating-magento-pwa-customizing-themes-coding.png" width="800" height="353" sizes="100vw" caption="Image credit: <a href='https://www.alibaba.com'>Alibaba</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/afbb6c16-9405-4701-9aba-b8f3963ff8f4/9-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="Screenshots of the Alibaba website" >}}

The native application of Alibaba differs slightly from the PWA that I’ve shown in the screenshots above. The design, style, and element choice are similar. Both options of the store are equally easy to navigate.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1b044fe-c54c-4706-94b3-16e6e613b379/13-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1b044fe-c54c-4706-94b3-16e6e613b379/13-creating-magento-pwa-customizing-themes-coding.png" width="800" height="475" sizes="100vw" caption="Image credit: <a href='https://apps.apple.com/us/app/alibaba-com-b2b-trade-app/id503451073'>Alibaba native application</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1b044fe-c54c-4706-94b3-16e6e613b379/13-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="Screenshots of the Alibaba native application" >}}

### 4. PWAs Work Fast And Pave Way To Headless Commerce

Due to the use of modern frameworks, advanced caching and rendering, and data transmission via API, properly developed PWAs can be a seven-league step up **to boost the store’s speed**.

Fast stores have a significant influence on conversions and rankings. Consider this:

- [25% of users will flee a page](https://www.websitebuilderexpert.com/building-websites/website-load-time-statistics) if it takes over 4 seconds to load.
- With every additional loading second, the [conversion rate drops by almost 4.5%](https://www.portent.com/blog/analytics/research-site-speed-hurting-everyones-revenue.htm#:~:text=The%20first%205%20seconds%20of,(between%20seconds%200%2D5)).
- [7 out of 10 users state](https://unbounce.com/page-speed-report) that poor page speed impacts their choice to buy on another e-commerce store.

Far from perfect site speed and performance are common pain points for many Magento stores, which are usually massive and complicated. The thing is that the majority of Magento stores have been up and running for about a decade and use a monolithic architecture. In the 2020s, there is a more modern alternative, headless architecture, which implies decoupling the frontend and backend.

For complex mammoth-like Magento stores that are commonly struggling to tackle slow page speed and other issues, the switch to headless can be a good starting point for a more global future-oriented transformation. We’re talking about the store’s performance and compatibility (both now and in the long run).

The main idea behind [headless commerce](https://onilab.com/blog/magento-headless-commerce-explained) is that the site’s frontend and backend become detached from each other, and they communicate using API (for instance, GraphQL).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc94844c-80fd-4fcb-84c9-01e9301634de/11-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc94844c-80fd-4fcb-84c9-01e9301634de/11-creating-magento-pwa-customizing-themes-coding.png" width="800" height="590" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc94844c-80fd-4fcb-84c9-01e9301634de/11-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="The chart showing how the site’s frontend and backend become detached from each other, and how they communicate using API." >}}

It allows having more than one frontend that you may create to suit different touchpoints. I.e., you can have a native application, a PWA, and some other frontends that were developed for the devices that your customers may use to shop (like a smart speaker or smart refrigerator). These multiple “heads” are attached to the backend and database.

The separation of monolithic architecture (making it headless) brings many perks. Because each frontend is designed to cater to a particular device type, the UX\UI, performance, and conversions improve. Not to mention that it becomes easier and faster to implement changes in a decoupled store from the development perspective.

*“Is a PWA a “must” in this case, you ask?”*

No, but it can be a start for transitioning a Magento store to a full-fledged headless solution. Getting a progressive web application implies decoupling the backend from the frontend, that is splitting the monolithic architecture.

If the Magento PWA is well-built, it can bring a lot of improvement **both to the store’s desktop and mobile performance**. And smartphones and desktop computers are the two main touchpoints that bring Magento stores most conversions at the moment. Therefore, it makes sense to optimize the store to perform better on these devices.

What else should you note if you get a PWA? Since your store will already be decoupled, later on (if and when necessary) you can add on other “heads”. Perhaps, your customers will give preference to shopping on your Magento store from their smart TV in five years? It’ll be simpler for you to add another frontend to your site.

In any scenario, headless commerce is forecasted as the largest change in the e-commerce market within the next decade, so this is some food for thought.

### 5. Is That It?

Bringing up other PWA features, they can **support push notifications**. If you’re wondering, *“Wait, don’t native apps support push notifications too?”* You’re right, they do. My point is that it’s no longer an advantage of only traditional applications if you’re choosing which to develop (a PWA or a native application). 

Push notifications are crucial for a strong customer retention strategy, as friendly non-irritating reminders can bring clients back into the funnel. In fact, quality push notifications can [boost your retention rates by 3 to 10 times](https://www.airship.com/blog/7-mobile-engagement-statistics-that-show-how-push-notifications-boost-roi). So, it’s up to you whether to include push notifications in your marketing strategy or not.

Do people use push notifications? Here’s what ShopPop stats suggest:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee16a3e-5bd2-4067-861a-e9f78f68878d/4-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee16a3e-5bd2-4067-861a-e9f78f68878d/4-creating-magento-pwa-customizing-themes-coding.png" width="800" height="292" sizes="100vw" caption="Image credit: <a href='https://www.shoppop.com/blog/ecommerce-chat-marketing-statistics/'>ShopPop</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bee16a3e-5bd2-4067-861a-e9f78f68878d/4-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="The rundown on statistics for push notification marketing." >}}

The same may be said about offline mode. Progressive web apps are **capable of working offline**. To specify, users can continue using those parts of the site that were cached if the Internet connection is unstable or when offline. Hence, this feature is also not a perk of only traditional apps. And frankly, the feature set of progressive web applications for online retail continuously expands.

{{% ad-panel-leaderboard %}}

## Are Progressive Web Apps All Perfect?

No. Especially when we are talking about iOS. There are still issues with how PWAs work on iOS devices, but overall the situation for e-commerce is good. Among the most notable restrictions are the partial absence of in-app payment features. But these issues shouldn’t stop you from building your own PWA.

Secondly, as per usual, great things take time. Creating a Magento progressive web application is not a fast task. It’s challenging from the development perspective and is rather time-consuming. But so is developing a native application or optimizing a site, agree?

## Are Progressive Web Apps Worth It?

Don’t get me wrong. There are cases when native applications can be a better choice over PWAs. These may, for instance, include the game and social media app sectors.

But will your customers use your e-commerce store’s downloaded native app on a regular basis? Ask yourself, if you opt for building a traditional application (with all its benefits) will users take the time to go to an app market and download it, especially if it’s weighty? Will they use it often afterward or delete it if they wish to free up device storage space?

A PWA, on the other hand, is available from the browser at all times. This can be a benefit for people not willing to download any app to their device.

However, there are cases when native applications have proven themselves to be a highly efficient means of sales in e-commerce. Perhaps your e-commerce site can benefit from having **both a native application and a PWA**?

That was the case for Alibaba that we discussed above, this company even offers its repeat buyers perks for making purchases using their native app. Another example is the Tally Weijl online store that also has a PWA and a native application.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36842c7f-1535-4b3c-8bf6-74092bfbda75/8-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36842c7f-1535-4b3c-8bf6-74092bfbda75/8-creating-magento-pwa-customizing-themes-coding.png" width="800" height="590" sizes="100vw" caption="Sources: <a href='https://www.tally-weijl.com'>Tally Weijl</a>, the App Store. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36842c7f-1535-4b3c-8bf6-74092bfbda75/8-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="Screenshots of the Tally Weijl website and the App Store" >}}

Large e-commerce stores and big established brands often have both solutions. Consequently, smaller online retail stores and companies that don’t have an extended budget for developing two solutions usually opt for just one.

In any event, when deciding which to get (a PWA or native app), you must understand your audience’s needs and business specifics. At this point, you’re aiming at strengthening your m-commerce share and need a solution that’ll enhance mobile conversions. It’s up to you which option will best suit your business needs, every case is individual.

### What Can Getting A PWA Bring To The Table?

The bottom line is that with a PWA, you “kill two birds with one stone” since you optimize both the look and performance of the e-commerce store on desktop and mobile. If a user enjoys shopping at your store on a smartphone, he has the chance to add a link-like shortcut to the home screen for fast access to the PWA. But at the same time, they can benefit from getting an equally good shopping experience on a desktop computer.

Finally, the process of rebuilding a Magento e-commerce store into a PWA means splitting the backend and frontend. By shifting to an API-based approach and headless architecture, you prepare the store for the big changes expected on the market in the next 5 to 10 years. I.e., people will use a larger variety of devices to shop online, including smart TVs, home assistants, and so on. Therefore, with a headless architecture, you can later add on solutions that’ll support these devices too.

{{% ad-panel-leaderboard %}}

## The Three Main Approaches To Building PWAs On Magento

So, we’ve gone over a plethora of things that make PWAs great. But how are they built?

It is crucial to choose in favor of an optimal approach as you begin the process of building a progressive web application on Magento. As you might have guessed, there’s more than one path that a developer (or team of developers) can take when it comes to creating a PWA project. And depending on the choice, different timeframes, hardships, and obstacles may imply.

Let’s discuss the three main paths to PWA development on Magento. They are custom coding with the use of a progressive framework, adapting a ready-made toolkit, or combining both approaches. We’ll also cover the upsides and downsides of each of them.

### 1. Using A Modern Framework

This approach implies custom coding the Magento PWA from scratch using a progressive framework. These are, for example, ReactJS, VueJS, or AngularJS.

First and foremost, this path is suitable for those developers who already **have previous experience in building PWAs**. For those who are only making their first attempt to create a progressive web app, making an app from A to Z this way will be rather hard simply because the entire process is on you. You’ll have to think through the whole application, its logic, structure, architecture, as well as write and assemble all the needed code yourself.

On the other hand, opting for a progressive framework-only approach is the best choice if you need to **create a PWA with many custom features** or functionality. That said, it’ll be super tricky to build a highly unique and complex Magento PWA solution using only an out-of-the-box toolkit like Scandi PWA or Magento PWA Studio.

To explain, here are some screenshots from the Bright Star Kids Magento PWA. This store gives its clients the chance to personalize products. As you can see, there’s a multi-step product customization builder that allows making changes to the item. The only way to achieve such a feature on the PWA is to use custom coding.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a486d1c1-6c94-493b-942a-67d8dbb9c9eb/7-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a486d1c1-6c94-493b-942a-67d8dbb9c9eb/7-creating-magento-pwa-customizing-themes-coding.png" width="800" height="575" sizes="100vw" caption="Image credit: <a href='https://www.brightstarkids.com.au'>Bright Star Kids</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a486d1c1-6c94-493b-942a-67d8dbb9c9eb/7-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="Screenshots of the Bright Star Kids website" >}}

#### An Overview Of The Process

Many steps imply, but to give a brief overview, they can go down to 7 frontend and backend steps:

1. Making system adjustments (f.e., configuring Ubuntu, installing the nodeJS runtime environment).
2. Installing a progressive framework like ReactJS to build the app, taking care of the server-side rendering implementation (f.e., via Razzle).
3. Adding all the libraries that the app will need to function (including GraphQL, Redux, and other often used ones).
4. Shaping out the app’s architecture using folders to maintain the structure and navigation.
5. Putting together the app (setting up Redux and GraphQL components, working with the storage (reducers), setting up Razzle (that’s used for component loading), defining URL paths using routes).
6. Piecing the parts that the app will consist of (header area, login, account, navigation menu, dynamic parts of the page, footer area, etc).
7. Making a backend module with files and handling backend GraphQL which processes queries.

If you need a detailed guide on how it’s done, feel free to look into this tutorial with code on [building Magento PWAs with ReactJS](https://onilab.com/blog/how-to-build-a-pwa-storefront-magento-2-a-detailed-guide).

#### Good To Know

Let’s bring up a couple of things to keep in mind as you create a Magento PWA from scratch. Here we’ll share some tips on things that work in practice and some handy workarounds.

**1. Handling Service Workers**

Service workers are very important for progressive web applications. This Javascript file is needed for caching data, can play the role of a proxy that processes HTTP requests, and is used for creating functionality for push notifications and the offline mode. Configuring service workers can be very challenging.

One of the most efficient ways to approach service workers is by opting for a Razzle JS plugin. With its installation, you can properly set up the work of this file. When working on the offline mode, choose the service worker in combo with cache API. The method with data pulled from the network prior to cache is considered a good option.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b22f781c-58fe-4e53-80e2-986326b455d1/10-creating-magento-pwa-customizing-themes-coding.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b22f781c-58fe-4e53-80e2-986326b455d1/10-creating-magento-pwa-customizing-themes-coding.jpg" width="800" height="406" sizes="100vw" caption="Image credit: <a href='https://www.programmersought.com/article/82244396205/'>ProgrammerSought</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b22f781c-58fe-4e53-80e2-986326b455d1/10-creating-magento-pwa-customizing-themes-coding.jpg'>Large preview</a>)" alt="the graphics showing how to approach service workers with a Razzle JS plugin." >}}

**2. Rendering**

The matter of properly handling client-side and server-side rendering can get tricky during Magento PWA development. Client-side rendering should be optimized additionally as you’d want the site to perform quickly on mobile devices. But the good news is that modern frameworks allow for rendering apps on both sides (client and server).

You can set up server-side rendering in several ways, including via:

- a Headless Browser (Puppeteer or Selenium);
- proxy;
- server-side rendering tools like Next.js or Razzle;
- nodeJS.

Going for proxy can allow you to achieve great results but this path takes a lot of time. Tools like Razzle are quite simple to use. Nonetheless, choosing a custom Node.js solution might be the best choice if you’re constructing something very complex.

**3. Components & GraphQL**

Many mistakes are often made at the very beginning during the architecture stage. The biggest possible mistakes include improper component size or if components are laid out irrationally. If the components are too big, this can negatively impact performance and lead to rerendering.

On another note, large GraphQL requests can really backpedal your PWA. For this reason, we’d recommend minimizing the number of GraphQL requests and using tools like Varnish to cache GraphQL.

#### Modern Framework Use Pros:

This is certainly the way to go in terms of development if you’re aiming at building a PWA with a lot of custom-created features. If the store goes beyond the standard feature set, opt for this path. 

#### Cons Of The Approach:

This is not the path for newbies in PWA development. The entire process falls under the responsibility of the developers. It implies a bunch of stumbling blocks that a developer may face if something “falls between the cracks”.

For instance, many mistakes are often made at the very beginning during the architecture stage. Configuring service workers can also be very challenging. They are needed for caching data, thus speeding up the PWA, and are used for push notifications too. Other examples of possible mistakes include improper component size or if components are laid out irrationally. If the components are too big, this can negatively impact performance and lead to rerendering.

If you’re the one coding, you can forget or leave something out unintentionally. Moreover, you’ll probably encounter an issue or something that you haven’t thought through; this will lead to rewriting a lot of your own code to get it right.

{{% ad-panel-leaderboard %}}

### 2. Customizing Toolkit Solutions

Alternatively, there are package options for building Magento progressive web apps that can be tweaked. As you may have guessed, this option is more suitable for newbies.

What you have to understand is that **toolkits like this provide more or less universal code solutions**. This option can save developers their time on coding from the ground up, notably if they plan to create a standard Magento PWA without any unique features.

Nonetheless, because the toolkit code is made to be universal, **it’ll be tough to customize a theme if your PWA needs something nonstandard**. Therefore, if the Magento PWA store is going to be complex or should have unique features, then it’ll be too difficult to achieve the desired result using just a toolkit. Way too often, opting for an out-of-the-box solution in such a case is very unreasonable. You’ll pull a lot of excessive code that’ll need to be removed.

Have a look at the Timetravels progressive web application. Due to the peculiarities of the sold services, the checkout of this site is absolutely unique. It significantly differs from the checkouts of regular e-commerce sites and has a bunch of steps and fields. I.e., you won’t manage to build such a custom checkout using only the provided out-of-the-box resources.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46b6252d-bba2-40fe-9e67-6f5c6202d4ea/2-creating-magento-pwa-customizing-themes-coding.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46b6252d-bba2-40fe-9e67-6f5c6202d4ea/2-creating-magento-pwa-customizing-themes-coding.png" width="800" height="580" sizes="100vw" caption="Image credit: <a href='https://timetravels.fi'>Timetravels</a>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46b6252d-bba2-40fe-9e67-6f5c6202d4ea/2-creating-magento-pwa-customizing-themes-coding.png'>Large preview</a>)" alt="Screenshots of the Timetravels website" >}}

#### Top Three PWA Toolkits For Magento

The three most commonly used toolkit packages are Magento PWA Studio, Scandi PWA, and Vue Storefront. Let’s take a closer look at each of these.

**1. Magento PWA Studio**

The [Magento PWA Studio](https://magento.com/products/magento-commerce/pwa) is the official “toolbox” for PWA creation that Magento provides. Based on ReactJS, the PWA Studio uses React code blocks and offers ready-made components and front-end architecture for the PWA Storefront. The available tools in the Studio can save a developer’s time on manually creating elements that make up a standard PWA.

Among the strong points worth noting is that **the toolkit is non-monolithic**, meaning that developers can use only the required parts as opposed to the whole package.

Furthermore, the **framework and architecture of the PWA come out of the box**. Thus, you can avoid making critical mistakes at the very start of the project. Plus, you can save time on setups (such as the app builder), service workers, caching, and routing works.

Speaking of the specific tools that developers can get ahold of are:

- PWA Buildpack CLI tools (for setting up an environment for PWA development),
- Peregrine package (includes React hooks and components),
- Venia package (with the store and UI components for visuals),
- UPWARD-JS (for the UPWARD server that is the median between the PWA and the Magento server),
- Project documentation.

**2. Scandi PWA**

Another toolkit example is [Scandi PWA](https://scandipwa.com). Being very developer-oriented, Scandi PWA provides the theme that’s placed atop Magento. This set of tools also offers ready components and functionality that can be borrowed and modified.

Mentioning a PWA example built with the use of Scandi PWA, we showed a couple of screenshots of the Apivita store earlier in the article.

Actually, Scandi PWA currently covers a broader range of cases and offers more ready-made solutions than the PWA Studio. Due to the accessibility of its quite extensive selection of readily available solutions, it may possibly be a better choice for you if you want to speed up the development process and therefore cut development costs (provided that your PWA is more or less standard).

The Scandi PWA toolkit can boast of having a large number of solutions in its roadmap that can be adopted. These already include:

- Configuration basics (theming, branding, languages, time zone, location, multi-store setup, other store details);
- Catalog and content solutions (everything from configurable and simple products to managing the price and stock);
- Client (cart, login & passwords, previous orders, accounts, wishlists, etc.);
- Components for marketing (customer feedback, product lists, coupons, price rules in the catalog, etc.);
- Search & Navigation (menu, breadcrumbs visibility, layered navigation, quick search, pagination, and other SEO-important points, among others);
- Checkout (payment methods, shipping, guest checkout, among others).

**3. Vue Storefront**

[Vue Storefront](https://www.vuestorefront.io) offers an open-source headless solution that’s flexibly applicable for multiple eCommerce platforms (it is thus suitable not only for Magento). As such, the Garten-und-Freizeit store that we showed in the screenshots in the first part of the article is based on the Vue Storefront toolkit.

Based on VueJS, the toolset has many ready-for-use blocks. However, the partial lack of Vue documentation can make installation and maintenance tricky at times.

Listing the production-ready solutions that are available:

- server-side rendering,
- Vue Storefront API,
- CMS API,
- ElasticSearch support,
- Vue Analytics,
- Payment system integrations (Paypal, Stripe, Klarna, Mollie, Adyen).

Just as with the Scandi PWA case, Vue Storefront is developed by an individual company, not the official Magento team. Plus, this toolkit is suitable for integrating with numerous e-commerce platforms, thus, isn’t only Magento-oriented. These points are worth keeping in mind.

#### PWA Development Process Overview via Magneto PWA Studio

The approach of building a PWA using a toolkit differs from the one we described previously. If we take the Magento PWA Studio example, the steps can be shortlisted to the following:

1. Making system adjustments (f.e., configuring Ubuntu, installing the nodeJS runtime environment, and other software).
2. Setting up a new project (e.g., using the PWA Studio Buildpack).
3. Overriding default components that are provided by the Venia Concept to change the PWA to what you need (from the logo to any other parts of the PWA such as the menu).
4. Making a backend module with files and handling backend GraphQL and other queries.

Feel free to browse this detailed guide on [how to create a Magento PWA using the PWA Studio](https://onilab.com/blog/how-to-develop-a-site-using-magento-pwa-studio) if you’d like to check out code examples or need a step-by-step tutorial.

#### Good To Know

Here are a few recommendations to bear in mind if you decide to build a Magento PWA with the Magento PWA Studio toolkit.

- Mind the matter of styles during the standard component override. Additional styles bring about extra file weight which isn't good for your PWA. Therefore it is crucial to remove the unnecessary blocks of code containing unused default styles.
- Handling GraphQL queries smartly can be another problem to tackle. Because the Magento PWA Studio toolkit rarely uses query fragments, you may face obstacles. A workaround solution here is splitting big queries into parts and using them multiple times. Note, however, that this tip isn’t universally applicable and can lead to unpleasant consequences if used in inappropriate parts of the progressive web application (for example, in listings).
- Make sure to not get confused with talons and hooks, otherwise, you can mix up the visual and logic components. Put simply, hooks are reusable, talons are not. You can check out [this document](https://magento.github.io/pwa-studio/peregrine/talons/) for a more detailed explanation.

#### Toolkit Approach Pros:

As we’ve already mentioned, choosing a toolset as a path for creating a PWA is reasonable for those who have no prior experience with building PWAs.

The ready-made blocks are customizable and can shorten the time spent on installation, set-ups, etc. The process is more like an override rather than building from the ground up. 

#### Cons Of The Toolkit Approach:

If your project differs from what’s offered by the PWA Studio or other analogous packages as a standard, you may face the challenge of changing the code. And, at times, it’s very hard to modify it. 

You can end up not only wasting extra time on such code customization but also implementing PWA elements that’ll be unnecessary for your specific app (this can slow load time and lower performance).

Again, if the PWA that you’re developing requires highly customized solutions, custom development is the way to go, not tailoring ready blocks.

### 3. Opting For A Combo Solution

Finally, the third choice is using a combination of custom coding and some readily available toolkit pieces. This seems like a gold meridian for many developers.

#### An Overview Of The Process

Here are a couple of pointers:

- For instance, you can opt for a ready-made framework and architecture that are given in a toolkit. You may also make use of the parts that deal with caching, routing, and the service worker.
- Yet, when working on the frontend parts of the PWA, a developer can use his own code. This will be better than overriding and deleting the unneeded app code given in the toolkit.

#### Pros Of The Combined Approach:

It allows saving time on manual coding for standard features. It’s simpler to tweak the standard PWA parts and leave your unique code for the custom parts of the app.

#### Cons Of The Combined Approach:

A combined approach will involve additional code checks and studying what the ready-made solutions have on offer (i.e., what you can and can’t use for your PWA).

When you decide on using a blended approach, you can still end up with a deal of excessive code that’s “pulled” from the toolkit. Thus, to optimize your progressive web app, you’ll have to put in plenty of hours to review the code and remove all the parts you don’t need.

Similarly, you can face the need to untangle abstractions and fix the bugs that might occur due to mixing your code with that from the toolkit.

## Final Thoughts

All in all, Magento's progressive web applications are an investment that’s undoubtedly worth it. It’ll bring many benefits in the long run as well as show results straight off. What’s for development, there’s a lot to keep in mind because the process is by all means complex. Therefore, when choosing an approach, perhaps, the combined one that’ll give the chance to use a reasonable amount of custom coding with some solutions tweaked to your needs from toolkits is the best choice.

{{< signature "vf, yk, il" >}}

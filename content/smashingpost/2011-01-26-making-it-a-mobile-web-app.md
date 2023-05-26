---
title: 'Making It a Mobile Web App'
slug: making-it-a-mobile-web-app
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7e179c0-4de8-478d-9fe1-abdb7aef05f4/sencha-comp.jpg
date: 2011-01-26T16:14:07.000Z
author: kim-pimmel
summary: >-
  If you have developed an app for mobile devices, which model did you choose and why? In this article, Kim Pimmel goes through a good number of Mobile web apps advantages over native apps. 
description: >-
  If you have developed an app for mobile devices, which model did you choose and why? In this article, Kim Pimmel goes through a good number of Mobile web apps advantages over native apps. 
categories:
  - Mobile
  - Opinion Column
  - Apps
  - Android
---

Ask any interactive agency nowadays what their clients are asking for when they need a mobile experience &mdash; the answer will inevitably be "an iPhone and/or an iPad app." Native Apple apps are a hot commodity, and in today’s mobile application ecosystem, mobile web apps are not sexy. In fact, many people don’t even realize they are even an option. In certain cases, an iPhone/iPad app will be the right solution for their needs.

However, there are some situations where it may become a short-term win, but eventually a long-term loss. Mobile web apps offer a good number of advantages over native apps; and though they face some design, development and deployment challenges, they are a powerful cross platform, scalable and affordable solution.

### Increasing Fragmentation

Mobile apps are all the rage. There are a slew of startups targeting the iPad, countless entrepreneurs hacking together the next killer iPhone app, and it seems as though every big company has released an app of some sort. With the increasing penetration of Android phones, developers are scrambling to port their software.

But what about deploying to Windows Phone 7, Blackberry and Symbian? Who wants to study yet another SDK, learn another language, and go through yet *another* app submission process? Who will continue to keep the code up to date for all these platforms as each one splinters into new incarnations, releases new hardware and OS updates. Fragmentation is a costly long-term investment. And people are beginning to realize that native apps are not a sustainable long-term solution for all their needs.

<figure><img loading="lazy" decoding="async" class="67626" title="gap_iphone_android" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8d5ac7c7-78be-4946-82f7-ef3051f867b5/gap-iphone-android.jpg" alt="Screenshot" width="432" height="392" /><figcaption>GAP StyleMixer application for both iOS &amp; Android</figcaption></figure>

{{% feature-panel %}}

### The Mobile Web is Everywhere

As the native mobile app market becomes increasingly fragmented, it is becoming clear that there needs to be a solution which can re-use code and designs across platforms, and which eases deployment headaches. But why invent a new solution, when it already exists on every device out there: the Web. <a href="https://webkit.org/">Webkit</a> is gaining ground as the de facto standard for rendering web content, but even Webkit isn’t appropriate for every application. It wouldn’t be recommended for experiences that need complex graphics rendering, require hooks into specific hardware such as camera or accelerometer, or have hefty media requirements.

Though these constraints will change over time. But for all other apps that don’t need these features, using the mobile web frees developers to use their web technology of choice, so long as it will render on mobile browsers. Design and develop once, deploy everywhere. With smart design and code, a single web app could render appropriately on differing resolutions and screen sizes, and respond accordingly to touch, 5-way or cursor. Indeed, frameworks for mobile web app development already exist, such as <a href="https://www.sencha.com/">Sencha Touch</a>.

### Old News

Desktop web apps are far from a new idea &mdash; Rich Internet apps have been around for a while. Google has been pushing in this direction for years, creating a broad suite of online tools, primarily for the desktop, with an increasing focus on mobile. However, web apps have been slow to gain traction in the mobile space. Even with Apple promoting mobile web apps as the next best thing on their 1st generation iPhone in 2007, the focus is still squarely on native apps. And the primary reason for this is due to the overwhelming success of Apple’s (native) App Store.

{{% ad-panel-leaderboard %}}

### The App Store Model

Apple’s App Store was not the first to distribute native applications to mobile phones, but they proved it was a viable model, and launched the concept into popular culture. It’s this same model that would be necessary to make a mobile web app ecosystem successful.

<figure><img loading="lazy" decoding="async" class="67608" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2fa4fb8c-2f31-4aa8-a5f1-21c7a13f0857/android1.jpg" alt="Google's Android Market in Making It a Mobile Web App" width="500" height="451" /><figcaption>Foursquare App in Google’s Android Market</figcaption></figure>

As a consumer, it’s more appealing to go to one trusted online outlet for stuff than to waste time searching the web for the same thing, and putting yourself at risk of being hacked. Mobile web apps need a consolidated storefront for much the same reasons.

First, it’s easy to find apps when they are indexed, categorized, and searchable in one place. Second, a robust community of users exposing app popularity, contributing ratings and writing reviews makes it easier to evaluate your choices. Third, when I’ve decided to buy a game such as Plants and Zombies, I want to be sure my purchase will be a safe one &mdash; something a robust app store from a recognized company should offer. And since a web app is cross-platform, you could play it on your Android phone, your iPad, and your desktop &mdash; all with a single purchase. Buy once, use anywhere. It’s magic!

As a business or developer creating web apps, a **centralized web app store provides benefits** over doing it solo. Most importantly, it provides a source of monetization. This is the key to driving adoption of a web app ecosystem, as without revenue, businesses and developers will stick with money-making native apps. It’s also a marketing channel, allowing for easy discovery and promotion. Another potential benefit of using a web app storefront would be the APIs to help developers deal with authentication, licensing and other technical hurdles of digital distribution.

### It’s Possible Now

A great majority of native apps could be deployed today as full featured mobile web apps. The HTML5 family of technologies allow for refined typography, animation, streaming video, offline storage, and the list goes on. Probably the most high profile web app to date is the Youtube mobile site, which delivers a comparable experience to the native apps they have built.

{{< youtube id="GGT8ZCTBoBA" caption="Youtube Mobile Web Experience">}}

### Real World Challenges

As with any innovation, there are big questions that need to be answered. The most obvious is the issue of cross-platform compatibility. Building a robust and rich cross-platform mobile web app experience would benefit from HTML5 technology support, but currently RIM and Microsoft’s mobile offerings use their own standards. This weakens the des/dev once, deploy anywhere story; but is by no means a dealbreaker. Web developers have long dealt with coding to accommodate troublesome browsers, and this would be a similar case.

Another challenge in the ‘deploy anywhere’ scenario arises when you look at how a given design translates across devices with varying resolutions, form factors and input methods. Application designers will need to approach this problem by **targeting several key resolution/form factor combinations**, similar to what is recommended by the Android SDK. Depending on what device an app is being run on, the design, layout and functionality may differ significantly. This can be solved using a combination of intelligent design and careful development.

Last but not least is the problem of providing consistent, quality user experiences in this new application space. We’ve seen how the Android’s app offerings often leave much to be desired in terms of visual design and usability while Apple has been more successful in defining quality experiences. Providing a set of best practices, design patterns, and components for designers would go a long way towards the creation of quality mobile web app experiences that would win over consumers. As mobile web apps gain credibility, we will see more offering such as Sencha Touch and Sproutcore that provide solid web development and experience frameworks.

### The Inevitable Victory of the Web Browser

Web applications as ‘the next big idea’ might never happen &mdash; but in the coming years, more and more websites will have mobile incarnations that look a lot like applications. You’ll be swiping through articles, pinching photos, and flicking pests off your Farmville plot &mdash; all in your mobile browser. And people won’t even realize that in the end, the next generation mobile web won.

{{% ad-panel-leaderboard %}}

## What Do You Think?

This article is part of our *Opinion Column* section where we provide a platform for designers and developers to raise their voice and discuss their opinion with the community. What is your opinion on native mobile apps and HTML5 apps? Where do you see advantages and disadvantages of both? How do you predict mobile development in the upcoming years? Are we all getting a little carried away with the app hype? If you have developed an app for mobile devices, which model did you choose and why? Let us know what you think.

If you have developed an app for mobile devices, what paradigm did you choose?

### Further Reading

-   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)
-   [Facing The Challenge: Building A Responsive Web Application](https://www.smashingmagazine.com/2013/06/building-a-responsive-web-application/)
-   [Providing A Native Experience With Web Technologies](https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/)

{{< signature "il, vf, mrn" >}}

---
title: >-
  App Development Showdown: Why You Should Care About Revisiting The Native Vs.
  Hybrid Debate In 2017
slug: app-development-showdown-native-hybrid-debate
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/346b4f1c-2ac2-4d4c-80ee-3e16f7f5dfb5/1-app-development-showdown-frontpage-opt.png
date: 2016-12-20T21:09:21.000Z
author: scotthendersson
description: >-
  Back in 2007, the world met the iPhone for the very first time. After Apple’s
  product debut, it took less than six months for work to begin on PhoneGap,
  which would become one of the first and most adopted frameworks for hybrid
  mobile app development — that is, for apps written simultaneously for multiple
  platforms using HTML, CSS and JavaScript, rather than coded in native
  languages.

  When compared with the prospect of learning an entirely new language and
  development environment in order to program iOS (and soon Android) apps, the
  appeal of this type of development to the already huge population of web
  developers in the world was palpable.
categories:
  - Mobile
  - iOS
  - Android
  - Hybrid
  - Native
---
Back in 2007, the world met the iPhone for the very first time. After Apple's product debut, it took less than six months for work to begin on PhoneGap, which would become one of the first and most adopted frameworks for hybrid mobile app development — that is, for apps written simultaneously for multiple platforms using HTML, CSS and JavaScript, rather than coded in native languages.

When compared with the prospect of learning an entirely new language and development environment in order to program iOS (and soon Android) apps, the appeal of this type of development to the already huge population of web developers in the world was palpable.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Providing A Native Experience With Web Technologies](https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/)
*   [Cross-Platform Native Apps With A Single Code Set](https://www.smashingmagazine.com/2016/07/cross-platform-native-apps-single-code-set-telerik-nativescript/)

As with many things, however, execution in the real world didn't quite live up to the hype.

{{% feature-panel %}}

It quickly became apparent that giving apps created in hybrid frameworks a "native" feel wasn't always easy. Because these apps were essentially just rendering a web app in a native shell, mobile Internet connections and device hardware speeds at the time caused performance in many hybrid apps to range from "This is loading a little slower than my other apps" to "Apple straight up rejected this from the App Store for not behaving as expected!"

<strong>In short:</strong> Hybrid hadn't quite delivered, and many would-be hybrid developers bit the bullet and learned to work in native development platforms, or decided to delay their app development ambitions indefinitely. It was kind of a bummer.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89cc0bc9-039f-4597-aee1-7a27d6189fd7/1-app-development-showdown-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf36cf33-adeb-4269-97f3-92b0014495bd/1-app-development-showdown-650-opt.png" alt="Hybrid app development is vying for your attention again." width="650" height="340" /></a><figcaption>Hybrid app development is vying for your attention again. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89cc0bc9-039f-4597-aee1-7a27d6189fd7/1-app-development-showdown-large-opt.png">View large version</a>)</figcaption></figure>

As time went on, however, advancements in technology — namely, phone hardware — allowed for enough progress in the performance of hybrid apps to drive some bold new claims. A notable example is the report published by industry research giant Gartner predicting that, by 2016, 50% or more of apps deployed to the App Store and Google Play would be hybrid. The prediction was published way back in 2013, and the figure of 50% was <a href="https://gadgets.ndtv.com/apps/news/over-50-percent-of-mobile-apps-to-be-html5-native-hybrids-by-2016-gartner-355385">picked up</a> and <a href="https://www.idownloadblog.com/2013/02/04/gartner-mobile-apps-2016/">plastered</a> on <a href="https://memeburn.com/2013/02/gartner-half-of-all-apps-to-be-hybrid-by-2016-expect-a-50-smartphone-this-year/">virtually every</a> website covering the mobile development industry.

Now, many native frameworks and development tools even boast robust showcase libraries highlighting hybrid apps that have successfully made their way to market. Probably among the most notable are <a href="https://showcase.ionicframework.com/">Ionic's</a> and <a href="https://www.appcelerator.com/customers/app-showcase/">Appcelerator's</a>.</p>

## Bringing The Record Current

Have hybrid apps hit parity with their native counterparts yet? There have been several indications that we're at least moving in that direction. At any rate, being in the latter half of 2016 warrants a renewed discussion of the hybrid versus native debate — and what opportunities it might hold for current developers.</p>

### Native Apps Are Still Faster, But That Statement's Weight Is More Limited Than Before.

There's no beating around the bush: In our current development world, there are still situations in which native apps load and move about with more agility than their hybrid counterparts. That being said, the difference in experience is far less noticeable than even just a few years ago. Software development outfit Azoft wrote over a full year ago that, in its experience, hybrid apps were in many cases "just as good as native apps." Additionally, the general consensus has gone from "Native is better" to "Native is better in certain cases." Those certain cases tend to boil down to a few key factors now:

*   **Graphical behavior**.  Apps that need to utilize advanced 3D graphics, particle effects and multilayered animations are still not well suited to hybrid. Additionally, due to the knowledge and work put into such graphics, often used in games, the extent to which hybrid can expedite development (one of its main selling points) is diminished. This is because, where programming in hybrid frameworks can help you accomplish page-building and other app development tasks with less code, creating games and animations in general still requires specific knowledge and intensive work to get right.
*   **Hardware responsiveness**.  Apps that require very quick, responsive access to things like a device's accelerometer or similar hardware components are often still better suited to native development as well. This is because the need to call on these components with JavaScript — as is the case with hybrid apps — represents an extra step the device has to execute. That being said, this reality is declining in severity and will only continue to do so as phone hardware becomes more powerful.
*   **CPU requirements**.  CPU-intensive apps (such as those that intercept camera input in real time to apply live filters, or that quickly render video, or that process large amounts of data simultaneously, etc.) are the other category of native-suited apps, due to the same logic we touched on above. Again, this gap will likely narrow over time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48bec7fe-ac68-4fc1-af90-173c9ce37200/3-app-development-showdown-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/feaa44b2-f084-4968-a17b-603f386131af/3-app-development-showdown-650-opt.jpg" alt="A shot of this year's hit Pokemon GO" width="650" height="433" /></a><figcaption>A game like Pokemon GO almost certainly falls beyond the limits of hybrid development in 2016. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48bec7fe-ac68-4fc1-af90-173c9ce37200/3-app-development-showdown-large-opt.jpg">View large version</a>)</figcaption></figure>

### Hybrid Apps Still Have a Shorter Development Cycle and Time-To-Market.

Even in an extremely <a href="https://www.ymedialabs.com/hybrid-vs-native-mobile-apps-the-answer-is-clear/">pro-native post on Y Media Labs</a>, the author concedes that clients are probably better off seeking hybrid development "if the desired time to market is less than six months." His experience is far from exclusive: <a href="https://www.makeit.com/hybrid-app-development-vs-native-better-company/">Most articles</a> that <a href="https://www.mobiloud.com/blog/native-web-or-hybrid-apps/">explore this debate</a> conclude that development cycles can be greatly reduced by opting for hybrid.

Despite a rapidly growing number of developers with native coding skill sets, traditional app development is still a slow and complex process in many cases, and the timeframe within which a company or individual wants to get their app rolling can sometimes rule out native on its own.

Native tools regularly improve to help developers work more efficiently, but they are often outpaced in time savings by their counterparts in the hybrid world. The developers behind Ionic, a barebones framework for developing hybrid apps with raw HTML, CSS and JavaScript, recently launched <a href="https://ionicframework.com/">Ionic Creator</a>, a product with some drag-and-drop elements for prototyping; newcomer <a href="https://www.aquro.com/">Aquro</a> is making waves by combining visual workflows with web coding in its own way; and enterprise-focused companies such as <a href="https://telerik.com/">Telerik</a> have similar platforms as well.

It's also worth noting that much of this discrepancy in development efficiency between native and hybrid can be attributed to multiplatform projects. Because Android and iOS (and, in some hybrid platforms, Windows and web apps) can be developed simultaneously, the work hours needed to be put into a multiplatform mobile app can be significantly reduced by going hybrid. Plus, every time a client needs to update or add features to an app, again, those changes only have to be written once to be deployed across all of their platforms. That's generally a big advantage for both developers and their clients.</p>

### This Shorter Development Cycle Usually Means Lower Costs, as Well.

In a <a href="https://www.comentum.com/phonegap-vs-native-app-development.html">Comentum article</a> by app developer Bernard Kohan specifically comparing native development with development of hybrid projects in PhoneGap, he concluded that, depending on the size of an app project, businesses could save between 32 and 36% on their bill by opting for hybrid. When app development projects in the business world almost always operate in the five to six digit range, that can mean a difference of a lot of money, and clients will start to take notice and more often request hybrid development if they feel it meets their needs.

The research for Kohan's writeup was conducted in January of 2015, but the same trends have further developed since, and more recent investigations still find differences in the cost associated with the two development strategies.</p>

## What This Means For You, And How To Take Advantage Of It

The real takeaway from this shifting dynamic is a massive business opportunity for those who bother to take advantage of it.

Hybrid app development is likely to enter a golden era, when more enterprise clients and mid-sized businesses will want apps, but pricing can still be placed at a premium until the market is saturated.

Savvy developers can still charge large development fees to create apps for these clients with hybrid technologies, while undercutting native costs just enough to give these clients a deal they can feel good about. Plus, they can develop these apps at a quicker rate, which means a high hourly income and a client that's going to sing your praises for delivering their company's app in two and a half months, when native-based firms have projected four to five or more.

In a few years, however, the time savings of hybrid development will be better known, the expectations of buyers will be more closely aligned with the actual time involved in the creation of these apps, and the number of developers offering hybrid development will be higher, increasing the need to bid for jobs at competitive prices. Remember that this exact trend has played out in the world of website development over the past couple of decades.</p>

## A Hypothetical Example

Let's say, today in 2016, ACME Thumbtacks wants to contract a developer for an internal Android and iOS app to link up with its inventory system and let workers submit new orders from within the app when stock is low.

They approach a native development house, which quotes them $80,000 and gives a projected delivery date six months away. Armed with your favorite hybrid framework and development environment, you are approached by the client for a second opinion, and you let them know that you can complete the job in just two to three months, for $50,000.

Huge project savings <em>and</em> half the lead time?! They'd be fools not to go with you, and you pocket one heck of a price for a couple of months' work. Of course, these numbers will vary wildly from project to project, depending on the customer's needs and ability to pay, but you get the idea.

A word of caution: It is still important to be clear about client expectations for their app and the feasibility of those expectations within a hybrid development framework. This ensures you'll avoid embarrassing situations in which you might over-promise on functionality that should really still be executed natively!

### This Same Scenario Might Look Different A Few Years From Now.

ACME Thumbtacks now knows that their app's requirements aren't intensive enough to necessitate native development, so they explicitly look for hybrid developers. Because so many others have jumped on the trend and are perfectly happy with quoting a client just $20,000 for a few months of work, gone are the days of easy money!

While you'll still have plenty of work as an app developer, your golden goose will have flown away, or at least will have become more of a, uh, bronze pigeon. Plus, as the hybrid market becomes more and more crowded, those early adopters with more satisfied clients, testimonials and connections will be in a good place to maintain a high level of demand.

Much like web development in the late 1990s and early 2000s, hybrid app development will be a skill set that can be sold at a premium over the next few years. That, my friends, is the definition of an opportunity!

Of course, a lingering stigma continues to dog the hybrid development world. Depending on the structure you're working in (freelance or independent, or working in a firm with immediate superiors to report to, etc.), you might need to help more people overcome the perception that clients of hybrid development projects might be left with a subpar product.

One of the best things you can do to address this is to have those skeptics download a few of the apps from the showcase pages linked to earlier (or a <a href="https://phonegap.com/app/">few of PhoneGap's</a>) and consider whether the experiences they encounter would be satisfactory to a client. The truth of the matter is that most of these apps are likely indistinguishable from natively developed ones.

In the end, the decision of whether to jump through the hoops necessary to switch gears and/or start a whole new hybrid venture is up to you. But, hey, those hoops might just end up being made of gold.</p>

## Takeaways

*   Hybrid development maintains its speed advantage over native coding, especially for apps that need to run on multiple platforms.
*   Phone performance has helped hybrid development grow out of its stigma of clunkiness, but it's still far from a perfect solution for some project types.
*   The hybrid route currently presents a great opportunity for web developers to make a seamless (and lucrative) move into app development.
*   App development, whether native or hybrid, has an upward trajectory in demand that's probably worthy of your attention over the coming years.

{{< signature "da, vf, il, al" >}}


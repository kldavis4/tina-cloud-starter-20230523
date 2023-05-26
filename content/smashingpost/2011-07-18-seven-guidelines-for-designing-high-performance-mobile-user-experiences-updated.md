---
title: 'App Design Guidelines For High-Performance Mobile User Experiences'
slug: seven-guidelines-for-designing-high-performance-mobile-user-experiences
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0743773-1a5f-4721-b535-314d049406da/navigation-01.png
date: 2011-07-18T11:21:41.000Z
author: ivo-weevers
summary: >-
 Design plays an important role in building lasting relationships with end users. Ivo Weevers presents seven guidelines that can help shape design decisions related to performance while accounting for the needs of end users and businesses. 
description: >-
  In this article, we’ll discuss performance in relation to design and present
  seven guidelines that can help shape design decisions related to performance
  while accounting for the needs of end users and businesses. These guidelines
  are based on the experiences of our teams in designing native mobile apps for
  a broad product portfolio and on multiple mobile platforms.
categories:
  - UX
  - Mobile
  - Devices
  - Performance
  - UX
---

A positive first impression is essential to relationships. People look for trust and integrity, and they expect subsequent encounters to reflect and reinforce their first impression. The same principles apply to brands and their products. Design plays an important role in building lasting relationships with end users and, thus, in supporting the brand’s promise.

Users expect mobile services to be relevant and user-friendly and to perform well. The limitations of the medium, however, impose significant challenges to designing products that meet all of those expectations. While often underestimated, performance is a crucial contributor to a trustworthy mobile user experience. Therefore, it’s considered to be a key driver in app design guidelines.

In this article, **we’ll discuss performance in relation to design and present seven guidelines** that can help shape design decisions related to performance while accounting for the needs of end users and businesses. These guidelines are based on the experiences of our teams in designing native mobile apps for a broad product portfolio and on multiple mobile platforms.

{{% feature-panel %}}

## Performance For Mobile

People use their mobiles to enhance productivity, comfort and pleasure, everywhere and at anytime: waiting for the bus, walking on the sidewalk, checking which platform their train leaves from. Mobile applications need to focus on a core utility, and they need to be fast and reliable in order to be valuable in those environments.

Paradoxically, we’ve noticed that many mobile design cycles start with requests for great aesthetics first: “It has to look amazing!” Of course, stunning visuals will attract customers by making a great first impression. However, a long-lasting relationship depends on the quality of each encounter, which is also heavily influenced by how the app performs. An application that looks stunning but performs poorly can damage integrity. Users quickly notice software that is slow or likely to break (whether because of downtime, crashes, etc.), and this impairs both usage and brand perception. Users expect an app to be fast and responsive. If it’s not, it will get poor reviews, low ratings and low adoption numbers.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2669321-edc9-4620-b184-c1e390ecfa7a/cookmate-twitter.gif"><img class="99946" title="Twitter and Cookmate" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/918d65b2-6217-4de2-8fde-b87ad0fb9018/mobile-apps.jpg" alt="Twitter and Cookmate app" width="503" height="351" /></a><figcaption>The visuals in the Twitter app are not as rich as Cookmate’s (which are stunning), but reviews for the Twitter app in the App Store are much better.</figcaption></figure>

## Performance Supports Brand Differentiation

Every product encounter affects the brand perception. Users are looking for the best tools to enhance their lives. To attract a significant user base in a landscape that is becoming more populated each day, a mobile app has to stand out. It should do something no other app does, or do it better than others do. These benefits reinforce the brand. Because performance is an essential element in the user experience, it directly helps to differentiate the brand. Taking this one step further: making a technically challenging feature perform smoothly will give the product a unique selling point, one that will be difficult to imitate.

A good example is the Flickr iPhone app. Flickr states on its website that it has two main goals: to help people to make their photos available, and to enable new ways to organize photo and video. Guess what? That is exactly what its app does well, thus fulfilling its brand’s promise.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f249ab25-9af9-4f44-b588-1360880e3ca4/flickr.gif"><img class="99948" title="Flickr" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f249ab25-9af9-4f44-b588-1360880e3ca4/flickr.gif" alt="Flickr iPhone app" width="550" height="400" /></a><figcaption>Flickr does a good job of optimizing the key brand encounters.</figcaption></figure>

So, when planning an app, it is worth analyzing the market and trying to answer two questions. (1) What should it do differently from its competitors? (2) What should it do better than its competitors? Then, focus your design and development efforts on the resulting top three goals.

## A Key Design Exercise

Crafting products of any kind requires an appreciation of the way they are built. Well-established design and engineering disciplines have recognized this for a long time. A car’s design influences its aerodynamics. A beautiful eye-catching bridge has to cope with wind and with traffic passing over and beneath it. The same applies to interactive mobile services. Design choices affect features, content, interactivity, graphics and, therefore, performance.

We’ve noticed on several product teams that performance is believed to be exclusively the responsibility of developers, and therefore it is considered too late in the design process. But in order to assess feasibility, development needs to be considered during the creative process. Applying the seven guidelines below and considering relevant factors for mobile UI (see the next section) up front will help to incorporate the topic of performance into design discussions. Achieving a high-performance experience is not just a coding exercise. It is a key design exercise.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/059fd987-46ad-4b72-b988-3edeba4bdabe/erasmus.jpg"><img class="99954" title="Erasmus bridge" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/059fd987-46ad-4b72-b988-3edeba4bdabe/erasmus.jpg" alt="Erasmus bridge in Rotterdam" width="550" height="224" /></a><figcaption>The Erasmus bridge in Rotterdam, the Netherlands. (Image: <a href="https://en.wikipedia.org/wiki/Erasmusbrug">Wikipedia</a>)</figcaption></figure>

## Relevant Factors In Mobile UI Performance

The perception of performance is based on start-up time, page-loading behavior, smoothness of transitions and animations, errors, and waiting times. The diagram below illustrates these factors: the “app” (with its graphics, interaction, content, features and code) runs on a “mobile” device with certain technical capabilities (CPU, screen size, etc.) and a platform (Android, iOS, etc.). In many cases, the app connects over a “network,” with a set coverage and standard (LTE, 3G, 2G), to a “back end.” The two factors at the top are heavily influenced by the decisions of the design and development team. The bottom two factors are constraints that need to be taken into account.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5cbd607-d9ba-42d1-beee-7ef6ea14b4ac/model4.gif"><img class="aligncenter wp-image-106830 size-full" title="Relevant factors" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5cbd607-d9ba-42d1-beee-7ef6ea14b4ac/model4.gif" alt="app design guidelines - Performance factors" width="550" height="350" /></a><figcaption>Factors that influence performance.</figcaption></figure>

Decisions for each factor will affect performance. Any combination, enhancement (such as advanced visuals) or limitation (such as poor network coverage) could increase complexity. For example, content being loaded from the back end in addition to advanced graphics traveling over a slow network are a combination of factors that will reduce performance.

## 7 App Design Guidelines

The last years have seen dramatic changes in the mobile platform landscape. New UI paradigms have emerged, screens and processors are becoming as advanced as desktop computers, and input mechanisms have been revolutionized.

Within these shifting constraints, designers should always try to create a look and feel that is cutting-edge, memorable and high-performing. This is not just a matter of reducing image sizes. Decisions made at various levels of the design and the design process will have a significant impact. Let’s look at seven guidelines that have proven to be helpful tools at all design levels to achieve high-performing mobile user experiences.

### 1. Define UI Brand Signatures

Each user interaction with an app should reflect the story of the brand and should increase recognition, loyalty and satisfaction. Identifying which elements contribute most to the brand’s identity is essential. Examples are features, visuals, wording, fonts and animations. Our design teams work on many different products on different product teams. This could easily lead to several design and implementation variations of similar UI elements. Defining the core building blocks encourages reuse and discourages reinvention and, therefore, optimizes the design and implementation of a set of components.

One approach is to define the UI elements that form the core building blocks of the user interface and, together, to create the interface’s unique character. In the concept phase, identify those elements that do the following:

*   Differentiate the app (for example, the photo-viewing feature in the Path app);
*   Represent key functions (for example, a check-out feature for a store);
*   Set the pattern of the design language (for example, the header in the screenshot below).

<figure><a href="https://en.wikipedia.org/wiki/Metro_Design_Language"><img class="99942" title="Metro UI" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/535d4673-03e0-4cf7-8838-b16a7c9be8d8/wp7-musicvideo.jpg" alt="Metro UI" width="530" height="229" /></a><figcaption>Windows Phone 7’s Metro UI is a great example of how fonts, layout and interaction can establish a unique design DNA. (Image: <a href="https://en.wikipedia.org/wiki/Metro_Design_Language">Wikipedia</a>)</figcaption></figure>

The core signature elements need to be the most responsive. They will be seen by users over and over and will be reused in different product features. By focusing the design and implementation on this set of elements, each optimization will pay off multiple times.

### 2. Focus The Portfolio of Products

Whether a company wants to launch a product quickly, or develop a product portfolio (i.e. multiple products on one platform, the same product on multiple platforms, or both), or if facing limited time and resources, hard choices have to be made. Design and optimization efforts should be targeted at those products in the portfolio that matter most. A design priority matrix helps us understand where design efforts will pay off the most.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42d95e83-c745-4b20-bce7-204517fa5691/portfolio.gif"><img class="99924" title="Design Priority Matrix" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/42d95e83-c745-4b20-bce7-204517fa5691/portfolio.gif" alt="Design Priority Matrix" width="550" height="259" /></a><figcaption>Example of a design priority matrix.</figcaption></figure>

Focusing design efforts helps to optimize performance in the most rewarding areas. For example, if most of your anticipated customers are using Android phones, and competitors are also targeting them, dedicating more design effort to creating an elegant and fast Android app would be more valuable than dividing your efforts equally across all platforms.

### 3. Identify The Core User Stories

Our teams have faced several project kick-offs in which the initial list of requested features was lengthy, unfocused and impossible to build within the requested timeline. When dreaming up what a product should do, companies often lose sight of the fact that customers look for solutions that help them with very particular needs.

For example, one main shopping goal (besides socializing, inspiration, etc.) is to find and purchase a product. Whether in a small city, on Oxford Street in London or on the Internet, it’s about finding and buying what you’re looking for. The experience could be enriched to make shopping more fun, but the core goal &mdash; finding and purchasing &mdash; should never be lost. The same applies to the design of a shopping app (whether for games, music, vouchers). The user needs to be able to find and purchase quickly, regardless of whatever other functions that enrich the overall experience.

The illustrations below show two designs for a product detail page in a store. The left screen has advanced shopping features, such as gifting, related products and detailed reviews. The right screen is more focused on purchasing. Implementing the right screen will optimize the company’s story, and the team won’t get distracted by designing and implementing side features. Only when the basic core functionality is optimized can enrichment features be added, as long as they do not hinder the core user stories.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b7e9a60-338d-468e-b95c-279a8cb56a03/shop2.gif"><img class="aligncenter size-full wp-image-106829" title="Shop examples" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b7e9a60-338d-468e-b95c-279a8cb56a03/shop2.gif" alt="Two examples of a shop purchase screens" width="550" height="280" /></a><figcaption>Two kinds of purchasing screens.</figcaption></figure>

During the product definition process, the core user stories should be identified in order to focus the design and development efforts.

{{% ad-panel-leaderboard %}}

### 4. Optimize UI Flows And Elements

Users don’t like to wait. (Google puts “<a href="https://www.google.com/corporate/ux.html">Every millisecond counts</a>” as the second principle of its user experience.) Optimizing individual screens, flows and UI elements will reduce waiting times and keep users from thinking that they’re wasting their time.

**A. Speed up perceived performance**
The designer cannot control performance all of the time. The network might be slow; the device might be running other tasks in the background; certain operations might require a lot of calculation. If the user at least perceives that they are not losing time, then the app will make a solid impression. Design can help communicate this, even during unexpected delays.

The first step is to identify flows that will likely have delays (fetching back-end data, performing a lot of calculations, etc.). The second step is to guide users through these delays by introducing additional steps that they would perceive as being necessary (showing loading animations, displaying useful tips, etc.).

The following set of images shows possible steps in a content search:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bbef771-7052-4304-a9f5-9e27ae11f85d/loading-2.gif"><img class="aligncenter size-full wp-image-106835" title="Loading flow" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7bbef771-7052-4304-a9f5-9e27ae11f85d/loading-2.gif" alt="Loading flow" width="550" height="230" /></a></figure>

The user here experiences four steps:

1.  Hits the search button.
2.  Sees a loading animation.
3.  Sees the first part of the list, with textual content and placeholder images (which could be stored in the app itself).
4.  Sees the actual thumbnail images appear.

The user experiences short steps, rather than jumping directly from step one to four, and so perceives progress rather than delay.

Another example is when an app starts loading up. By first displaying a picture that matches the application’s layout, the user gets the impression that the app is loading more quickly. The screenshot below illustrates this; however, the perceived performance could be sped up even more by adding a simple progress notification in the blank space of the first screen. This would avoid the impression that something is waiting to be loaded. (In case of a slow connection the app does show a loading notification, thereby communicating progress to the user for that situation).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb57ce9e-2ebb-4442-8f42-b81a6ba3d248/facebook1.gif"><img class="100237" title="Facebook" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb57ce9e-2ebb-4442-8f42-b81a6ba3d248/facebook1.gif" alt="Startup loading of iPhone facebook app." width="550" height="400" /></a><figcaption>The Facebook app for the iPhone loading up.</figcaption></figure>

**B. Optimize individual UI elements**
Every UI element affects performance. And because every optimization contributes to overall performance, all UI elements should be considered. Key aspects to look at are:

*   **Elements on screen**.  The number and type of UI elements on the screen will affect the performance of that screen. For example, media items (audio, video, maps) will affect performance more than simple elements (static images, etc.).
*   **Element characteristics**.  The characteristics of an element, such as its resolution or image depth, affects drawing time. For example, on Android, each drawable resource (JPG, PNG) is decoded to bitmap format, so each optimized image will result in fewer kilobytes. Could you reduce the color depth? Or decrease the resolution?
*   **Drawing technique**.  The way a UI element is drawn by the app affects screen-loading time. For instance, is the entire background of a screen being drawn, even when a big opaque image is laid on top of it? Could a background be broken down into small tiles in order to reduce the size that needs to be uploaded?

### 5. Define UI Scaling Rules

Building the most appealing design is like navigating a terrain with many hurdles. It is a continual balancing act between functionality, aesthetics, usability and performance. Some platforms demand more UI compromises than others. No matter what the platform’s constraints, the brand’s key signatures should remain.

A UI scaling toolkit could help by communicating the relative importance of UI elements. Some elements are critical and contribute strongly to the brand’s identity, while removing others will have less of an impact. Our team has established the following categories:

*   **Essentials**.  Essentials are the brand’s core UI signatures (guideline 1). For example, the application’s header.
*   **Alternatives**.  Alternatives are less optimal, but good for high-end solutions that put a low burden on performance. An example is replacing transparent elements with opaque ones.
*   **Options**.  These are elements that enhance the experience but could be removed to maintain performance. For example, reducing a list of search results on a page from 25 items to 10.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/678b4b5d-6a6d-42d8-a859-341cca6ed161/scaling2.gif"><img class="aligncenter size-full wp-image-106831" title="UI scaling toolkit" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/678b4b5d-6a6d-42d8-a859-341cca6ed161/scaling2.gif" alt="UI scaling toolkit" width="550" height="278" /></a><figcaption>1. Essentials (the header).
2. Alternatives (opaque instead of transparent).
3. Options (reducing list length).</figcaption></figure>

### 6. Use A Performance Dashboard

Clear communication among the team is critical to delivering a great product. We’ve encountered several situations where expectations of how a product should perform differed between marketers, designers and developers. Because performance is affected by the requirements and constraints of all of these disciplines, performance expectations need to be agreed on. As a solution, we introduced performance dashboards. These help to measure, monitor and set goals for the product’s current state. Dashboards effectively communicate the product’s state and the team’s expectations and areas of focus. The dashboard we’ve used accounts for the following elements:

*   **Core user stories**.  Ensures that the dashboard communicates what the user experiences.
*   **Benchmark**.  Compares the app to a key competitor’s.
*   **Current measurement**.  Shows the performance of the product’s current implementation.
*   **Goal**.  Sets the performance goal for the app.
*   **Status**.  Indicates the current status of the app against the goal.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/620a6358-31ea-4ced-9150-f240a3b112dc/dashboard5.gif"><img class="108263" title="Example of Performance Dashboard" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/620a6358-31ea-4ced-9150-f240a3b112dc/dashboard5.gif" alt="Example of Performance Dashboard" width="550" height="329" /></a><figcaption>Example of a performance dashboard. (Numbers in seconds. For a good 3G connection.)</figcaption></figure>

Several tools can help you measure performance. You can do it subjectively, by manually recording the time for certain tasks, or objectively, with tools such as TraceView for the Android SDK (if you’re developing a native app).

### 7. Champion Dedicated UI Engineering Skills

Design has always gone hand in hand with technology. Being able to code high-performance user experiences is a specialist’s skill. It requires strong knowledge of front-end coding and a profound understanding of the design’s purpose.

The implementation of layout, graphics, animation and so on will have performance implications. Of the many things that need to be considered, here are two:

*   **Smart loading**.  Smart-loading mechanisms, such as lazy loading, first load visible content and then move on to content below the fold. This technique reduces the user’s waiting time and thus makes for a smoother experience.
*   **Background loading**.  This is another well-known example. Performance depends on whether the background is one large image, an amalgamation of small tiles (say, to create a texture) or a pure algorithm. The best solution depends on the situation.

In situations where responsibilities are split between the marketing, design and development teams, we’ve noticed that UI performance tends to fall between the cracks. Each team has its own goals, and so certain shared responsibilities, such as UI performance, lose attention. We’ve addressed this by including front-end coding specialists on the design team. This encourages focus on optimal UI implementation and performance, and it achieves a more advanced user experience.

## Conclusion

We’ve gone over seven guidelines that address performance relative to different aspects of mobile app design. Design choices affect performance, and so performance should be considered a key factor in the design process. Unfortunately, it tends to be looked at too late in the process, which ends up impairing the user experience significantly.

We have successfully introduced these guidelines into several product streams, which has in turn improved the performance of those products and fostered awareness of the issue among the teams. This has helped to shift the initial request from “It has to look amazing” to “It has to look, feel and work amazing!”

### Credits

A big thank you goes to my colleagues Daniela Aramu, Mark Howell and Mirja Leinss, who provided invaluable feedback on this article!

{{% ad-panel-leaderboard %}}

### Further Reading

*   [Creating High-Performance Mobile Websites](https://www.smashingmagazine.com/2013/08/creating-high-performance-mobile-websites/)
*   [Managing Mobile Performance Optimization](https://www.smashingmagazine.com/2016/03/managing-mobile-performance-optimization/)
*   [How To Make Your Websites Faster On Mobile Devices](https://www.smashingmagazine.com/2013/04/build-fast-loading-mobile-website/)
*   [The (Not So) Secret Powers Of The Mobile Browser](https://www.smashingmagazine.com/2016/12/the-not-so-secret-powers-of-the-mobile-browser/)

{{< signature "al, mrn" >}}

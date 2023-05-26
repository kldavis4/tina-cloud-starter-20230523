---
title: Keeping Your Android App Popular After Launch
slug: keep-your-android-app-popular-after-launch
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1b80de2-60e3-4eee-853c-185405e9acf2/01-droidy-opt.jpg'
date: 2015-10-08T21:07:08.000Z
author: ryanbateman
description: >-
  You’ve launched your app and it’s doing well. You worked hard, kept your
  initial features lean, and all of your effort has resulted in an app that
  users like and recommend to friends. So, how do you maintain that momentum and
  ensure that your app keeps gaining in popularity?
categories:
  - Mobile
  - Business
  - Apps
  - Android
---
You’ve **launched your app** and it’s doing well. You worked hard, kept your initial features lean, and all of your effort has resulted in an app that users like and recommend to friends. So, how do you maintain that momentum and ensure that your app keeps gaining in popularity?

This article covers some **practical approaches to keeping users interested** in and using your app, including talking to your users, keep on launching features, making the first impression count and using all functionalities of the operating system.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">How To Succeed With Your Mobile App</span>](https://www.smashingmagazine.com/2012/11/succeed-with-your-app/)
*   [Elements Of A Viral Launch Page](https://www.smashingmagazine.com/2011/09/elements-of-a-viral-launch-page/)
*   [Smart, Effective Strategies To Design Marketing Campaigns](https://www.smashingmagazine.com/2013/10/strategies-design-marketing-campaigns/)
*   [Lessons Learned After Shutting My Startup](https://www.smashingmagazine.com/2015/11/lessons-learned-shutting-startup/)

## Get Talking To Your Users

According to a survey conducted by Google and Ipsos MediaCT, the top three reasons why users abandon an app are lack of interest, change in user needs and simply lack of usefulness. But usefulness, necessity and interestingness are subjective and change over time — what you think your users need or like isn’t always accurate. So it’s important to **start a dialog with your users.**

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9f7d6b0-f66b-4ad5-8a1b-99cf4856e354/02-usefulness-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eb90ddf-729c-4d62-b0e0-d7be3519864e/02-usefulness-opt-small.png" alt="App usefulness is motivation for ~72% of apps being abandoned" /></a><figcaption>(Image: <a href="https://think.storage.googleapis.com/docs/mobile-app-marketing-insights.pdf">Think With Google</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9f7d6b0-f66b-4ad5-8a1b-99cf4856e354/02-usefulness-opt.png">View large version</a>)</figcaption></figure>

We’ve found that the best long-term approach is to **foster a “VIP” beta-testing community**. These beta-testing communities help us understand user needs, even as they change and adapt. These beta testers, in return, get early access to new features and have an opportunity to help shape the application, making them feel like VIPs and often turning them into advocates for the application as a result. We typically use the Play store’s [beta distribution channel](https://support.google.com/googleplay/android-developer/answer/3131213?hl=en-GB) and a Google+ community for this purpose. This distribution channel enables users to receive app updates via the Play store as normal, but from the beta release group. The Google+ community acts as a place to leave comments and bug reports, and access to the channel can be restricted.

Creating your own beta-testing community is simple. First, find the first few people who have rated your app lower than you’d like or who are particularly vocal about its design, and engage them in a dialog. Treat their complaints and concerns sincerely, and recognize that they’ve spent time trying out your application. If they’re open to the idea, ask them to join your beta-testing community, and, where possible, ensure that your subsequent releases address their concerns specifically. When you do so, let them know and thank them for their help. You’ll find that these users go from being critics to advocates.

[CCleaner for Android](https://www.piriform.com/ccleaner-android), an application published by Piriform, is one such application for which we took this approach. Within 18 months, it grew to over 15 million downloads, and the beta-testing group grew to 10,000 people. The people in this testing group have become **advocates** whose opinions help shape the app’s next features, keeping it useful and up to date with users’ needs. This beta group is very large. When setting up your own, try to keep it to a number that will allow you to respond to queries and bug reports, while still leaving you time to work on new features.</p>

## Keep Launching

If you’ve kept your first launch lean, you should have a **backlog of features** that you’d have loved to put in the product but sensibly didn’t. Keep that version 1.1 lean, too, and assume that half of the effort that goes into it will be bug fixes, but get it out sooner than later.

Aim to update your application regularly, and get users used to (and excited about) these updates. This regular update rhythm will both act as a good personal motivator as well as teach users to expect timely, interesting updates. Companies such as Spotify make these regular releases a [part of their engineering culture](https://vimeo.com/85490944), creating a “release train” that leaves the station every two weeks. Features that are not completed in time for the next train are shipped as part of the release but are deactivated and unseen by user.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc711b23-1a55-4678-b855-b4f18ca13bac/03-spotify-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3da37e56-ce91-4a72-a84a-ccf3157efaeb/03-spotify-opt-small.png" alt="Spotify releases regularly, sometimes with features partially completed but unseen by the user" /></a><figcaption>(Image: “<a href="https://vimeo.com/85490944">Spotify Engineering Culture, Part 1</a>”) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc711b23-1a55-4678-b855-b4f18ca13bac/03-spotify-opt.png">View large version</a>)</figcaption></figure>

There are a number of tools you should consider adopting when attempting to decrease the time between your app’s updates.

**Automated testing** is the most important. A continuous integration server, such as [Jenkins](https://jenkins-ci.org/), can be used to automatically run tests on features and changes that you’ve made to the code as you work, ensuring that you never code yourself into a corner. Knowing that your updates and changes haven’t caused a new bug or broken an older feature means you shouldn’t ever have to waste time “doubling back” over old code.

An **issue tracker** is a good tool for prioritizing your workflow and maximizing the value you send out with each update. JIRA is a one such tool used by many large teams, while Trello is a good alternative for lone developers. Both tools allow you to create issues (or cards) that you can use to monitor your backlog. This helps you to plan and organize releases with minimal hassle and keep your administrative overhead to a minimum.

If you’re using Git, then another practical method of managing this selective integration of new features in time for a release is the [Gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow). This workflow keeps code branches for new features separate from the main code base. When it’s time to create a release, these code branches can then be selectively merged back into the main code base.</p>

## Make That First Impression Count

According to a [survey conducted by Quettra](https://andrewchen.co/new-data-shows-why-losing-80-of-your-mobile-users-is-normal-and-that-the-best-apps-do-much-better/), on average 77% of users no longer actively engage with an app after just one week. If you want your app to keep engaging users and stay popular, then making a good impression in those first few days after installation is vital.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea93a71e-4f61-41cb-8e17-876f8d9f92a7/04-retention-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff8b6e40-608a-43fc-9c44-9e3a3460be1e/04-retention-opt-small.png" alt="App usefulness is motivation for ~72% of apps being abandoned" /></a><figcaption>(Image: <a href="https://andrewchen.co/new-data-shows-why-losing-80-of-your-mobile-users-is-normal-and-that-the-best-apps-do-much-better/">Quettra/Andrew Chen</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea93a71e-4f61-41cb-8e17-876f8d9f92a7/04-retention-opt.png">View large version</a>)</figcaption></figure>

As an app developer, your aim, therefore, should be to **highlight the app’s usefulness** to new users in the first week after installation. A good onboarding process that highlights the app’s functionality is vital. Where possible, this onboarding should walk users through a real use case or show real data to best impress upon them the purpose of the application.

This can be a challenge in some cases, such as when the app’s content is behind a paywall or when its content is populated entirely through user action. In the case of "The Sun", one of the world’s largest English-language newspapers, we worked with the company’s designers and API developers to ensure that the onboarding process contained real, timely data (in this case, football scores and recent headlines).</p>

<figure class="video-container"><iframe loading="lazy" src="https://player.vimeo.com/video/138465155" width="500" height="500" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

This real, time-sensitive data presented well, highlighted to new users exactly what kind of content they could expect and showed that care had been taken in its presentation. This approach caused adoption rates to spike and resulted in increased revenue.</p>

## Use Every Part Of The Buffalo

Android is far more than simply a phone operating system.

With a little work, it’s easy to move your app’s core functionality into any of Android’s other form factors and then tailor the UI and UX as necessary. Nothing delights a user more than an app that works well and seamlessly across all of their devices — from their phone to their new tablet and even to their Android TV. This cross-platform compatibility is a great way to outdo your competitors. You’ll no longer simply be competing on a single form factor.

Android applications are typically distributed as [Android application package](https://en.wikipedia.org/wiki/Android_application_package) (APK) files. These files can be produced for individual platforms, in which case multiple APK files would be produced, or a single APK can be produced that works on multiple Android form factors.

One way to ensure that you’re able to deliver a consistent experience across all of these platforms is to **produce a single APK file** that can easily be installed on any Android device. Producing a single APK has both [advantages and disadvantages.](https://developer.android.com/google/play/publishing/multiple-apks.html)

One advantage is **automatic installation on new devices**. If a user of your app buys a new device, once they log into the new device with their Google account, all of their compatible apps will automatically be synced. If you’ve produced a single APK, this means the user will find your app installed automatically on their new device. In the case of Android TV, where app discovery is generally more difficult, this is almost essential to gaining installation traction.

The biggest disadvantage in producing a single APK for all platforms is the **resulting file size**. This one APK will need to contain all resources for all platforms and configurations, meaning a potentially bloated APK for those with phones with small storage.

In terms of code structure, the best way to organize your code for easy portability across form factors is to ensure good separation of the app’s business logic (which typically won’t vary from device to device) from the presentation layer (which will). This will allow you to alter each platform’s UI and UX without having to alter any underlying logic.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d42f259-b556-4b70-9e8b-c158d6745dd4/06-berlin-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aff126a3-079e-44d5-a12e-9d65537329b0/06-berlin-opt-small.png" alt="Landing page UI may differs between two form-factors such as tablet and phone but it can share the same underlying business logic." /></a><figcaption>(Image: <a href="https://novoda.com/work/berliner">Novoda</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d42f259-b556-4b70-9e8b-c158d6745dd4/06-berlin-opt.png">View large version</a>)</figcaption></figure>

Here, for example, we see how an app with a single APK has a log-in page laid out in two different ways for the tablet and phone form factors. The underlying business logic for validating a password or making a call to the necessary API will be the same for both form factors, but how we present any errors and lay out the page will be different.

With this in mind, **we always start our projects with two modules**: “core,” which contains our core business logic, and “mobile,” which contains our Android- and platform-specific code. Within the mobile module, we then split our presentation layer code across various platforms as necessary, all while keeping the underlying business logic the same across our platforms. This separation of concerns ensures that we can not only parallelize development, but also reduce potential regression bugs. This approach has numerous other benefits, such as making standalone testing of core business logic easier.

## Final Notes

The tips mentioned above are all **long-term approaches** to maximizing user retention, driving daily usage and getting users hooked on your app, but they don’t have to be deployed simultaneously. Your general aim, and best approach, should simply be to demonstrate that you know and care about your users’ needs and requests.

{{< signature "al, ml, jb, da" >}}


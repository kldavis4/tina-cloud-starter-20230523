---
title: 'Building, Testing And Distributing Android Apps'
slug: getting-to-know-android
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e37e54dd-2272-4fc3-8e80-cb6e4905b6a3/mobiles-illu-324135.jpg
date: 2012-06-01T10:39:55.000Z
author: juhani-lehtimaki
description: >-
  When iOS started to gain momentum, soon after the first iPhone launched, many businesses started to pay attention to apps. The number of apps for iOS grew exponentially, and every company, big and small, rushed to create their own app to support their business.
categories:
  - Mobile
  - Apps
  - UX
  - Android
  - Design Patterns
---
When iOS started to gain momentum, soon after the first iPhone launched, many businesses started to pay attention to apps. The number of apps for iOS grew exponentially, and every company, big and small, rushed to create their own app to support their business.

For some time, iOS was the only platform you really had to care about. The audience was there. For a few years now, there has been another player in the market. Android’s marketshare growth has been phenomenal, and it simply cannot be ignored anymore. There are over 200 million Android users in the world—almost double the numer of iOS users. For businesses, reaching the Android crowds is potentially a very lucrative investment.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Build A Mobile Application With Native Android](https://www.smashingmagazine.com/2014/01/four-ways-to-build-a-mobile-app-part2-native-android/)
*   [What Every App Developer Should Know About Android](https://www.smashingmagazine.com/2014/10/what-every-app-developer-should-know-about-android/)
*   [A Field Guide To Mobile App Testing](https://www.smashingmagazine.com/2012/10/a-guide-to-mobile-app-testing/)

Android as a platform can appear intimidating to new players. Blogs and media are littered with articles about Android fragmentation and malware. The Android platform can feel complex, although it is very flexible. However, before getting started with an Android project, understanding the platform and ecosystem is imperative. Trying to apply the methods and tools that work on other platforms could lead to disaster.

{{% feature-panel %}}

In this article, we’ll explain parts of the application-building process and ecosystem for Android that could cause problems if misunderstood. We’ll talk about an approach to building a scalable app that looks and feels right at home on Android, and we’ll cover how to test it and your options for distributing it. The following topics would each need a full article to be explained fully, but this article should provide a good overview. After reading this article, you should have a good understanding of what kinds of decisions and <strong>challenges you will face when creating an Android app</strong>.</p>

## Make The App Scalable

Android devices come in many forms and sizes. The last official count is that 600 Android devices are available, and that number is growing every day. Building an app that runs on all of them is more difficult than building for just one or two screen sizes and one set of hardware. Fortunately, Android was built from the ground up with this in mind. The framework provides tools to help developers tackle the problem. But as with all tools, they only work if used correctly.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c01f6283-1a4b-4be9-b095-a93426eaee78/device.png"><img loading="lazy" decoding="async" class="size-medium wp-image-116622" title="device" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f8318b5-4899-4400-a820-f1f41cf96b56/device-300x120.png" alt="" width="300" height="120" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c01f6283-1a4b-4be9-b095-a93426eaee78/device.png">Large preview</a>.</em>

An iOS app is designed and built by placing pixels at the proper coordinates until the UI looks just right. Not so on Android! Android designers must think about the scalability of each component and the relationships between components. The philosophy is much closer to Web app design than to iOS app design.</p>

### A Continuum Instead Of A Separate Tablet UI

About half a year ago, Google rushed out the Android version named Honeycomb (3.0). Honeycomb was aimed at tablets and was never meant for anything else. The source code of Honeycomb was never released, and it never officially appeared on any phones. At the time, Apple had already established a practice by which developers provided two separate versions of their app, one for iPhone and one for iPad. Because of Apple’s model and the separate Android version for tablets, everyone seemed to assume that two separate versions of an app are needed on Android, too. Soon, the Internet was full of blog posts complaining that Android didn’t have enough tablet apps and that there was no way to search for them on the Google Play store.

Now, as Android Ice Cream Sandwich (4.0) is unifying all Android devices to run the same version of the OS, it all makes sense. Android is a continuum, and drawing a clear line between tablets and phones is impossible. In fact, checking whether an app is running on a tablet or phone is technically impossible. Checking the screen size (and many other features) at runtime, however, is possible.

This is where Android design starts to remind us of Web design. New technologies have enabled us to build websites that adapt automatically to the user’s browser size by scaling and moving components around as needed. This approach is called responsive Web design. The very same principles can be used on Android. On Android, however, we are not bound by the limits of the browser. Responsive design can be taken even further.</p>

### Responsive Android Design

Android developers can define multiple layouts for every screen of their app, and the OS will pick the best-fitting one at runtime. The OS knows which one fits best by using definitions that developers add to their layout (and other) folders in the app’s project resource tree.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04623172-33e1-4989-a893-6ab9a40b4bcf/screen-shot-2011-11-24-at-12.00"><img class="size-medium wp-image-116503" title="Layout folders structure" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acb8bbe7-ac66-4d9e-bb65-a8301269f500/screen-shot-2011-11-24-at-12.00" alt="" width="236" height="300" /></a><br>
<em>An example of the structure of layout folders, which distinguish between screen sizes and Android versions.</em>

Starting from Android version 3.2 — and, therefore, also on Ice Cream Sandwich — a more fine-grained approach was introduced. Developers may now define layouts based on the screen’s pixel density, independent of size, instead of using only the few categories that were available before.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ed5e863-47c9-4231-b328-8f5040be2c8b/screen-shot-2011-11-26-at-8.04"><img class="116678 " title="Screen Shot 2011-11-26 at 8.04.21 PM" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ed5e863-47c9-4231-b328-8f5040be2c8b/screen-shot-2011-11-26-at-8.04" alt="" width="612" height="53" /></a><br>
<em>An example of the new layout specifications based on screen size. It is very similar to CSS’ media queries. <a href="https://developer.android.com/guide/practices/screens_support.html#NewQualifiers">Android’s documentation</a> has more details.</em>

### Using Fragments to Implement Responsive Design

Fragments are the building blocks of Android UIs. They can be programmed either to be standalone screens or to be displayed with other fragments; but the most powerful ones are both, depending on the device that the app is running on. This enables us not only to rearrange the fragments but to move them deeper into the activity stack. <a href="https://www.smashingmagazine.com/2011/08/09/designing-for-android-tablets/">Dan McKenzie has written</a> about issues related to designing for big Android screens.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/299d851a-4d53-473e-b015-cb3e54512ad9/resonsive1.png"><img class="116506" title="Responsive design diagram 1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/299d851a-4d53-473e-b015-cb3e54512ad9/resonsive1.png" alt="" width="316" height="437" /></a><br>
<em>Each component is itself stretchable and scales to screens with similar sizes.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7a92034-b4a1-407b-909c-d9a1bd5b807c/responsive2.png"><img class="116507" title="Responsive design diagram 2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7a92034-b4a1-407b-909c-d9a1bd5b807c/responsive2.png" alt="" width="488" height="535" /></a><br>
<em>When a screen’s size is drastically different, the components need to be rearranged. They can be rearranged on the same level or moved deeper into the activity stack.</em>

## Make The App Look And Feel Android-Like

Consistency with other apps on the same platform is more important for an app’s look and feel than consistency with the same developer’s apps on other platforms. Having the look and feel of apps from a different platform will make the app feel foreign and make users unhappy.

(Remember to read Google’s <a href="https://developer.android.com/design/index.html">Android Design</a> guidelines.)

### Tabs

In Android apps, tabs should always be on top. This convention was established and is driven by Google’s design of its apps and by guidelines from advocates of Android development. Putting the tabs on top makes scaling an app to larger screen sizes easier. Putting tabs at the bottom of a tablet-sized UI wouldn’t make sense.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18803fd2-a3b0-4e8f-911f-c492496c14e7/largepreview-1.png"><img class="alignleft size-medium wp-image-116625" title="png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6ff0775-5203-46a4-bf0d-62909dc15631/png-171x300.png" alt="" width="171" height="300" /></a><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ff3b552-f853-4b59-b685-a062c7d8572e/ics1.png"><img class="aligncenter size-medium wp-image-116626" title="ics1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fc7650d-3ade-4734-b8bf-d2da41d6fb03/ics1-171x300.png" alt="" width="171" height="300" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18803fd2-a3b0-4e8f-911f-c492496c14e7/largepreview-1.png">Large preview</a>.</em>

Navigating between top-positioned tabs on a phone with a large screen can be difficult, especially when the person is using only one hand. The solution is to enable the user to swipe between tabs. This interaction model is not new, but in its latest release, Google has made it commonplace in Android apps. All bundled apps now support this interaction on tabbed UIs, and users will expect it to work in your app’s tabbed screens, too.</p>

### Android UI Patterns Can Put Users at Ease

Some UI patterns have become popular on Android — so much so that they are starting to define the look of Android apps. The action bar, one of the most popular patterns, is now part of Android’s core libraries and can be used in any app running on Android 3.0 and up.

Good third-party libraries are available to bring the action bar to apps that run on older versions of Android. <a href="https://actionbarsherlock.com/">ActionBarSherlock</a> is very stable and supports multiple versions and even automatically uses the native action bar when it detects a supported version of Android.

Another popular UI pattern is the dashboard. Many apps with a lot of functionality use the dashboard as their landing screen to give users a clear overview of and easy access to the app’s most important functionality.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f146aa38-0443-4170-ad54-1cf8111d4557/png-4.png"><img loading="lazy" decoding="async" class="size-medium wp-image-116665" title="png-4" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/191d7e8d-a918-4ab4-8051-12bcfd6eac15/png-4-172x300.png" alt="" width="172" height="300" /></a><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f817086-ee2f-4e66-8be4-b95005315d5b/png-2.png"><img class="aligncenter size-medium wp-image-116666" title="png-2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbefc510-7982-47a3-82e9-360a239c468b/png-2-172x300.png" alt="" width="172" height="300" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73f21e76-48c8-4d00-9f77-d701de8d1c2d/large-preview-2.png">Large preview</a>.</em>

Google Play (left) and Evernote (right) both put an action bar at the top of their screens to provide quick access to contextually relevant actions. Evernote’s landing screen clearly tells the user what they can do with the app, while providing easy access to those actions every time the app launches.

See Dan McKenzie’s article “<a href="https://www.smashingmagazine.com/2011/06/30/designing-for-android/">Designing for Android</a>” for more on the look and feel of Android apps.

## Integrate The App With Other Apps

The Android platform provides a powerful mechanism for apps to extend each other’s functionality. This mechanism is called “intents.” Apps can register to receive and launch intents. When an app registers to receive intents, it must tell the system what kind of intents it can handle. Your app could, for example, tell the system that it can show pictures or open Web page URLs. Now, whenever another app launches an intent to view an image or a Web page, the user has the option to choose your app to complete the action.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4c6fe9d-9f2b-4a54-aff0-5696bdff6b62/png-3.png"><img loading="lazy" decoding="async" class="size-medium wp-image-116669" title="png-3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45ec6658-c576-4536-81ac-d56b539ba395/png-3-172x300.png" alt="" width="172" height="300" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4c6fe9d-9f2b-4a54-aff0-5696bdff6b62/png-3.png">Large preview</a>.</em>

### Social Network Integration

On other mobile platforms, if an app wants to share something to Twitter, Facebook or another social network, it implements the sharing mechanisms internally in the app. Sharing requires a separate operation for each social network. On Android, this can be achieved more easily using intents. An app may launch an intent telling the system that it wants to share an image or text. Depending on which apps the user has installed, the user will be provided with a list of apps that can handle the operation. If the user chooses a Twitter or Facebook client, the client will open to its sharing screen with the text or image prefilled.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59b1d44b-0bf0-41b4-88ce-119ba886375d/png-7.png"><img class="alignleft size-medium wp-image-116671" title="png-7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76deff4b-0af5-40f4-b53c-ca16331a1c61/png-7-172x300.png" alt="" width="172" height="300" /></a><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a817756d-adf9-4aa8-ac88-cd8bfb360e05/png-8.png"><img class="aligncenter size-medium wp-image-116670" title="png-8" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f233ace-4cbf-4acb-8823-ebc1435aa3c0/png-8-172x300.png" alt="" width="172" height="300" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59b1d44b-0bf0-41b4-88ce-119ba886375d/png-7.png">Large preview</a>.</em>

There are many benefits to integrating with social networks using intents rather than implementing sharing directly from your app:

1.  Close to zero effort is required to build the functionality.
2.  Users don’t have to log into a separate application. The social network’s app takes care of logging in.
3.  You don’t have to limit the social networks that users may use to share from your app. All apps installed on the user’s device are available to be used.
4.  If a social network’s sharing protocol changes, you don’t have to worry about it. That service’s app will be updated to reflect the changes.
5.  Users might be using an unofficial app for a social network. Using intents, they may continue using their app of choice with the interface they are familiar with.
6.  The intents mechanism offers only options that the user actually uses (i.e. the apps that they have installed). No need to offer Facebook sharing to someone who doesn’t have a Facebook account.</p>

### Think of Other Opportunities

Extending the functionality of other apps via the intents system will benefit your app, too. Perhaps your app wouldn’t get used every day and would get buried under apps that are used more often. But if your app extends the functionality of other apps and keeps popping up as an option every time the user wants to perform an action that your app can handle, then it will be thought of more by users.

Intents have limitless possibilities. You can build your own intents hierarchy to extend certain functionality to other apps, in effect providing an API that is easy to use and maintain. You are essentially recommending to users other apps that complement yours and, in turn, extending your app’s features without having to write or maintain any code. The intents system is one of the most powerful features of the Android platform.</p>

## Quality Control

With the massive number of devices, testing an Android app is much more difficult than testing an iOS app. This is where the fragmentation causes the most problems. Testing on one or two devices is not enough; rather, you have to test on a variety of screen sizes, densities and Android versions.

In addition to what you would normally test on any other platform, you should the following:

*   Test your app thoroughly on the lowest Android version that it runs on. Accidentally using an API that isn’t actually available at runtime on some devices is easy.
*   Test that the search button works on all relevant screens.
*   Make sure that the D-pad and trackball navigation work on all screens.
*   Test all supported screen densities, or at least extra-high, high and medium. Low-density devices can be difficult to find.
*   Test on at least one tablet device. But try to test on as many screen sizes as possible.</p>

### Testing in the Cloud

New services are popping up to ease the pain of testing on multiple devices. Services such as <a href="https://testdroid.com/">Testdroid</a> enable developers to test their apps on multiple real devices through a Web interface. Simply upload your app’s package and automated testing script, and the service executes your scripts on dozens of devices. Results can be viewed in a Web browser. Examining screenshots from different devices is even possible, to ensure pixel-perfect UIs.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbf68946-5e46-47c7-a434-979c7de10c8e/screen-shot-2011-11-23-at-10.13"><img class="size-medium wp-image-116494" title="Testdroid cloud" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31f48799-f2f2-4eeb-960b-e97f86127afc/screen-shot-2011-11-23-at-10.13" alt="Testdroid cloud screenshot" width="300" height="215" /></a><br>
<em>Testdroid is a cloud service for testing Android apps on multiple devices. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbf68946-5e46-47c7-a434-979c7de10c8e/screen-shot-2011-11-23-at-10.13">Large preview</a>.</em>

## Distribute The App

Once your app is tested and ready, you need to get it to users. You’ll have to choose how to do it. Very few Android devices are restricted to one app store. The overwhelming majority of Android devices ship with Google Play, which is the most important route to reaching users on the platform.</p>

### Google Play

The Google Play store doesn’t have a formal process for approving apps. Any application package uploaded to Play will appear in the store’s listings to users. App guidelines do exist, but they are enforced only if there are complaints, and even then pretty randomly. This means that your app will be swamped by hundreds of other apps of varying quality.

So, how to rise above the masses and get the attention of users?

The first 30 days are important! Your app will appear in the listing for new paid or free apps during that time. Ranking relatively high in this listing during this time is much easier than ranking high in the overall top lists. Make sure that your app’s website links to Google Play from the start, and use all social networks to tell people about your app’s launch.

Getting recognized as a trusted brand is difficult. Google Play contains many apps that use registered trademarks without permission. Users have come to learn that a logo is no indication that an app was actually produced by that logo’s company. To increase trust, make sure the “Visit Developer’s Website” link points to the official website, and if possible link back to your app from there.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07a4dcbb-7e34-4a95-8a4a-a789a1545b15/screenshot-from-2012-04-26-192610.png"><img class="size-medium wp-image-111950" title="Top new apps on Google Play Store" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd868e14-e836-483b-9899-b089dd6fb634/screenshot-from-2012-04-26-192610-300x163.png" alt="" width="300" height="163" /></a><br>
<em>Top new apps on Google Play. <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07a4dcbb-7e34-4a95-8a4a-a789a1545b15/screenshot-from-2012-04-26-192610.png">Large preview</a>.</em>

Making an app work on all devices is sometimes impossible. Some devices lack the required hardware or simply run an old version of Android for which the required APIs don’t exist. You can list all of the requirements in the app’s manifest file, telling Google Play which devices the app is meant for and, thus, hiding it from listings that are being viewed on incompatible devices. But sometimes even that isn’t enough. In these cases, Google Play allows developers to prevent certain devices from downloading their app. While this option should be used only as a last resort, it is still better than allowing users to download something that you know does not work on their device.</p>

### Alternative App Stores

Google Play is not the only place to distribute your app. Amazon’s Appstore has lately gained attention due to the launch of Amazon’s Android-based Kindle Fire tablet. Amazon’s approach is fairly similar to Apple’s in that it has a formal review process. The Appstore is also accessible to non-Amazon devices, but currently only in the US.

Multiplatform app store <a href="https://www.getjar.com/">GetJar</a> also distributes Android apps. GetJar has a lot of users and is a well-known and trusted source, especially among people with not-so-smart phones.

Barnes &amp; Noble’s app store is a US-only eBook-based app store. Unlike Amazon’s, it is accessible only to B&amp;N’s Android hardware.</p>

### Multiple App Stores, Just One, or None?

Many people’s first instinct is to try to get their app into all stores. This decision should not be made lightly, though. Distributing through multiple stores might make the app reach more potential users. However, being spread across multiple app stores could prevent the app from ranking as high as it could in the listings for downloads and ratings. Having a thousand installations across three app stores might sound better than having two thousand installations in one store, but maybe those two thousand would push the app into a more visible spot in the store and help it rocket to tens of thousands of installations later.

An app doesn’t have to be in a store at all in order to be installed on devices. Android apps can be installed directly from websites or by transferring them from computer to phone. While you wouldn’t reach the same audience and wouldn’t benefit from the update mechanisms in app stores, there is definitely a place for direct distribution. Using forums and websites, developers can distribute their apps to alpha and beta communities without having to risk their reputation or low ratings in an app store. Distributing a major update or an unstable build to a limited number of dedicated testers and fans might be worth the extra effort.</p>

## Conclusion

Building a scalable and functional Android app is not impossible, but it requires careful planning and an understanding of the target platform. A blind approach or simply borrowing a design from another platform would likely end in failure. Achieving a successful end requires that you use Android’s tools correctly and follow the right design approach. Writing an Android app takes effort, but if done right, the app could reach a massive numbers of users.</p>

### Further Resources

Intents:

*   OpenIntents: Registry of Intents Protocol

Supporting multiple screen sizes:

*   “[Supporting Multiple Screens](https://developer.android.com/guide/practices/screens_support.html "https://developer.android.com/guide/practices/screens_support.html"),” Android Developers
*   “[Thinking Like a Web Designer](https://android-developers.blogspot.com/2011/09/thinking-like-web-designer.html "https://android-developers.blogspot.com/2011/09/thinking-like-web-designer.html"),” Android Developers
*   “[Deep Dive Into Responsive Mobile Design](https://www.pushing-pixels.org/2011/11/11/deep-dive-into-responsive-mobile-design-the-conclusion.html "Deep dive into responsive mobile design"),” Pushing Pixels
*   [Styling Android](https://blog.stylingandroid.com/)

Android design:

*   [Android Design](https://developer.android.com/design/index.html), official guidelines
*   [Android UI Patterns](https://www.androiduipatterns.com/)
*   [Android Niceties](https://androidniceties.tumblr.com/)
*   [Android Patterns](https://www.androidpatterns.com/)

Useful libraries:

*   [ActionBarSherlock](https://actionbarsherlock.com/)
*   [GreenDroid](https://greendroid.cyrilmottier.com/)
*   “[Support Package](https://developer.android.com/sdk/compatibility-library.html),” Android Developers

{{< signature "al" >}}


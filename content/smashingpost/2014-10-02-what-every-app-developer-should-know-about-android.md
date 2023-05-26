---
title: What Every App Developer Should Know About Android
slug: what-every-app-developer-should-know-about-android
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70fbb2cc-f0f9-401a-a50f-35f39873d38d/01-testdroid-phones-opt-500.jpg
date: 2014-10-02T15:17:30.000Z
author: villeveikkohelppi
description: >-
  In today’s fast-paced mobile market, consumers have no patience for mobile
  apps that compromise their experience. “Crashes” and “Not working” are the
  most common feedback on Google Play for unstable or sluggish apps (including games).
  lousy apps.
categories:
  - Mobile
  - Apps
  - Devices
  - Performance
  - Android
---
Those comments and ratings make hundreds of millions of potential downloaders skip those lousy apps. Sounds harsh, but that’s the way it is. An app succeeds not by chance. It is the result of the right decisions made at the right time. The most successful mobile app developers understand the importance of performance, quality and robustness across the array of mobile devices that their customers use.

Examples abound of just how easily a developer can go very, very wrong with their app. An app can behave differently on a <a href="https://www.androidcentral.com/devices">variety mobile devices</a>, even ones running the same OS version and identical hardware components.

Recommended reading: [Mobile Best Design Practices For Android](https://www.smashingmagazine.com/2012/07/android-design-tips/)

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bfe602a-3705-4990-adc1-233b4a5cfbb9/01-testdroid-phones-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70fbb2cc-f0f9-401a-a50f-35f39873d38d/01-testdroid-phones-opt-500.jpg" alt="Testdroid Cloud hosts hundreds of working Android and iOS devices." width="500" height="333" /></a><figcaption>Testdroid Cloud hosts hundreds of working Android and iOS devices. (Image credit: <a href="https://www.testdroid.com/">Testdroid</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bfe602a-3705-4990-adc1-233b4a5cfbb9/01-testdroid-phones-opt.jpg">View large version</a>)</figcaption></figure>

During Q1 of this year (1 January to 31 March), we gathered a significant amount of data from <a href="https://bitbar.com/testing/">Mobile App Testing</a> on tests done by many mobile app and game developers. Testdroid Cloud is an online cloud-based platform for mobile developers to test that their apps work perfectly on the devices that their customers use.

During this period, over 17.7 million tests were run on 288 distinct Android hardware models. To be clear, different versions of some popular models were tested but are counted in the data as one distinct device (such as the <a href="https://pdadb.net/index.php?m=specs&amp;id=4234">Samsung Galaxy S4 GT-i9505</a> running 4.2.2, API level 17). Some popular devices also had different versions of a single OS, such as the <a href="https://pdadb.net/index.php?m=specs&amp;id=3929">Google Nexus 7 ME370T</a> with Android OS version 4.1.2 (API level 16), 4.2.2 (API level 17) and 4.3 (API level 18).

All tests were automated, using standard <a href="https://developer.android.com/tools/testing/testing_android.html#Instrumentation">Android instrumentation</a> and different <a href="https://en.wikipedia.org/wiki/Test_automation#Framework_approach_in_automation">test-automation frameworks</a>. In case you are not familiar with instrumentation, <a href="https://developer.android.com/tools/testing/testing_android.html">Android has a tutorial</a> that explains basic test automation. Also, the tests caught problems through logs, screenshots, performance analysis, and the success-failure rate of test runs.</p>

<strong>Note:</strong> The data includes all test results, from the earliest stage (=APK ready) to when the application gets “finalized.” Therefore, it includes the exact problems that developers encountered during this process.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5f10e40-0a89-446a-b4f4-61dc402bb072/02-testdroid-infography-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38d8b8bb-d7d1-47d2-a6fc-159dad8c7daa/02-testdroid-infography-opt-500.jpg" alt="The research statistics, testbed and global coverage." width="500" height="500" /></a><figcaption>The research statistics, testbed and global coverage. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5f10e40-0a89-446a-b4f4-61dc402bb072/02-testdroid-infography-opt.jpg">View large version</a>)</figcaption></figure>

The goal for this research was to identify the most common problems and challenges that Android developers face with the devices they build for. The <a href="https://opensignal.com/reports/fragmentation-2013/">288 unique Android device models</a> represent a significant volume of Android use: approximately 92 to 97% of global Android volumes, depending on how it gets measured and what regions and markets are included. This research represents remarkable coverage of Android usage globally, and it shows the most obvious problems as well as the status of Android hardware and software from a developer’s point of view.

We’ll dive deep into two areas of the research: Android <a href="https://en.wikipedia.org/wiki/Android_version_history">software</a> and <a href="https://tech.firstpost.com/news-analysis/all-you-need-to-know-about-mobile-phone-chipsets-27704.html">hardware</a>. The software section focuses on OS versions and OEM customizations, and the hardware section breaks down to the component level (display, memory, chipset, etc.).</p>

Recommended reading: [Bringing Your App’s Data To Every User’s Wrist](https://www.smashingmagazine.com/2017/01/bringing-app-data-every-user-wrist-android-wear/)

## Android Software

Your app is software, but a lot of other software is involved in mobile devices, too. And this “other” software can make your software perform differently (read “wrong”). What can you do to make sure your software works well with the rest of the software in devices today? Let’s first look at some of the most common software issues experienced by app developers.

Android OS has been blamed for <a href="https://developer.android.com/about/dashboards/index.html">platform fragmentation</a>, making things very difficult for developers, users and pretty much every player in the ecosystem to keep up. However, that is not exactly the case. The OS very rarely makes things crack by itself — especially for app developers. More often it also involves OEM updates, hardware and many other factors — in addition to the OS.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/699f8803-758d-46bf-904f-98bf413f4e13/03-android-os-distribution-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd3286dc-64c2-4703-9bb3-abc342cd84fe/03-android-os-distribution-opt-500.png" alt="Data collected during a 7-day period ending on July 7, 2014." width="500" height="182" /></a><figcaption>Data collected for seven days, ending on 7 July 2014. (Image credit: <a href="https://developer.android.com/about/dashboards/index.html">Google</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/699f8803-758d-46bf-904f-98bf413f4e13/03-android-os-distribution-opt.png">View large version</a>)</figcaption></figure>

One reason why Android is tremendously popular among mobile enthusiasts and has quickly leaped ahead of Apple's iOS in market share is because it comes in <a href="https://developer.android.com/training/design-navigation/multiple-sizes.html">devices of all shapes</a>, prices and forms, from tens of different OEMs.

Also, the <a href="https://en.wikipedia.org/wiki/Android_(operating_system)#Software_stack">infrastructural software of Android</a> is robust, providing an excellent platform with a well-known Linux kernel, middleware and other software on top. In the following sections, we’ll look at the results of our research, broken down by OS version, OEM customizations and software dependencies.</p>

### How to Read the Graphs

The findings from this study are plotted on graphs. In those graphs, the dark black line is the median (50%) of the failure percentage of different devices in that group. The lines above the bars mark the upper quartile (75%), and the lines below mark the lower quartile (25%). The dashed lines are the maximum (top or right) and minimum (bottom or left). The circles represent outliers.</p>

## OS And Platform Versions

We’ll start with the most important factor in the problems experienced by app developers: <a href="https://en.wikipedia.org/wiki/Android_version_history">Android OS versions</a>. This dramatically affects which APIs developers can use and how those APIs are supported in variety of devices.

Many developers have experienced all of the great new features, improvements and additions that <a href="https://www.smashingmagazine.com/2013/05/08/brave-new-world-designing-for-a-maturing-android/">Android has brought version by version</a>. Some late-comers have played with only the latest versions, but some have been developing apps since the early days as days of Cupcake (1.5) and Doughnut (1.6). Of course, these versions are not relevant anymore.

The following table shows the release dates for the various OS versions (along with their code names) and notes why certain versions were excluded or were not used on the devices being tested.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a03a058-9978-4119-9e04-724def49d590/04-q1-releasedates-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88a41a3a-1528-461b-9ca1-c3e119864adf/04-q1-releasedates-opt-500.png" alt="The Release version for each OS version." width="500" height="360" /></a><figcaption>The release version of each OS version. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a03a058-9978-4119-9e04-724def49d590/04-q1-releasedates-opt.png">View large version</a>)</figcaption></figure>

The most typical situation with app developers who want to maximize support for all possible variants is that they’ll start testing from version 4.0 (Ice Cream Sandwich, API level 14). However, if you really want to maximize coverage, start from version 2.3.3 (Gingerbread, API level 10) and test all possible combinations up to the latest release of Kit Kat (currently 4.4.4 and, hopefully soon, Android L). Versions older than 4.0 still have serious use — and will continue to for some time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5f72ade-f184-46c0-9d2a-99ef7e4179c1/05-q1-failed-releaseversion-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ed30bc5-f317-4873-95a7-abcab6642074/05-q1-failed-releaseversion-color-opt-500.png" alt="The Failure Rate by Each OS Version." width="500" height="350" /></a><figcaption>The failure rate of each OS version. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e5f72ade-f184-46c0-9d2a-99ef7e4179c1/05-q1-failed-releaseversion-opt.png">View large version</a>)</figcaption></figure>

When it comes to the latest versions of Android — and let’s count Ice Cream Sandwich (<a href="https://en.wikipedia.org/wiki/Android_version_history#Android_4.0.3.E2.80.934.0.4_Ice_Cream_Sandwich_.28API_level_15.29">4.0.3 to 4.0.4</a>), Jelly Bean (<a href="https://en.wikipedia.org/wiki/Android_version_history#Android_4.1_Jelly_Bean_.28API_level_16.29">4.1.1 to 4.3</a>) and Kit Kat (<a href="https://en.wikipedia.org/wiki/Android_version_history#Android_4.4_KitKat_.28API_level_19.29">4.4 to 4.4.2</a>) among them — Ice Cream Sandwich is clearly the most robust platform. OEM updates were obviously the least problematic on this version, and the majority of tested apps worked very well on API level 15 (4.0.3 to 4.0.4).

The upgrade to Jelly Bean and API level 16 didn’t significantly introduce new incompatibility issues, and the median failure percentage remained relatively low. However, API level 16 had many outlier cases, and for good reasons. For instance, more problems were reported with Vsync, extendable notifications and especially with support for the lock screen and home screen rotation.

API level 17 brought improvements to the lock screen, and this version was generally stabile up to version 4.2.2. The failure rate went up when the majority of OEMs introduced their updates to this version. Apparently, it became more problematic for users than previous versions.

Perhaps most surprisingly, the <a href="https://community.verizonwireless.com/thread/824084">failure rate went up</a> when Kit Kat API level 19 was released. The average failure percentage reached nearly the same level as it was with Gingerbread. Google patched Kit Kat quite quickly with two releases (4.4.1 and 4.4.2). Of those, 4.4.2 seemed to live much longer, and then the 4.4.3 update came out more than half a year later.</p>

### Key Findings From OS Versions

*   On average, 23% of apps behave differently when a new version is installed. The median error percent was the smallest with Ice Cream Sandwich (1%), then Jelly Bean (8%), Honeycomb (8%), Kit Kat (21%) and, finally, Gingerbread (30%). This is actually lower than what was found in the study conducted with Q4 data (a 35% failure rate).
*   Despite old Android versions being used very little and Gingerbread being the oldest actively in use, some applications (40% of those tested) still work on even older versions (below 2.2). In other words, if an app works on version 2.2, then it will work 40% of the time in even older versions as well.
*   Over 50% of Android OS updates introduced problems that made apps fail in testing.
*   Testing failed 68% of the time when 5 apps were randomly picked out of 100.
*   The average duration of testing was 57 cycles per platform. Old versions were tested less than new ones: Gingerbread (12 test cycles), Ice Cream Sandwich (17), Jelly Bean (58) and Kit Kat (95).
*   An average testing cycle reduced 1.75% of bugs in the code overall.</p>

<strong>Note:</strong> A test cycle constitutes an iteration of a particular test script executed in one app version. When an app is changed and the test remains the same, that is counted as a new test cycle.</p>

### Tips and Takeaways

*   For maximal coverage either geographically or globally, using as many physical devices as possible is recommended. Track your target audience’s use of different OS versions. The global status of versions is [available on Google’s dashboard](https://developer.android.com/about/dashboards/index.html).
*   All OS versions above 2.3.3 are still relevant. This will not likely change soon because users of Gingerbread and Ice Cream Sandwich represent nearly one quarter of all Android users, and many of them do not update (or would have done so already).
*   If you want to cover 66% of OS volume, then testing with Kit Kat (4.4.x) and Jelly Bean (4.1 to 4.3) is enough (covering API 16 to 19).
*   To cover 75% of OS volumes, then test from version 4.0.3 (API level 15).
*   We recommend testing the following devices to maximize coverage:
    *   Amazon Kindle Fire D01400 — 2.3.4
    *   HTC Desire HD A9191 — 2.3.5
    *   Huawei Fusion 2 U8665 — 2.3.6
    *   Sony Xperia U ST25i — 2.3.7
    *   Asus Eee Pad Transformer TF101 — 4.0.3
    *   LG Lucid 4G — 4.0.4
    *   HTC One S X520e — 4.1.1
    *   Motorola Droid XYBOARD 10.1 MX617 4.1.2
    *   Acer Iconia B1-A71 — 4.2
    *   BQ Aquaris 5 HD — 4.2.1
    *   HTC One mini M4 — 4.2.2
    *   Samsung Galaxy Note II GT-N7100 — 4.3
    *   LG Google Nexus 5 D821 — 4.4
    *   HTC One M8 — 4.4.2

<strong>Note:</strong> These devices were selected because they are a good base to test certain platform versions, with different OEM customizations included. These devices are not the most problematic; rather, they were selected because they provide <a href="https://opensignal.com/reports/fragmentation-2013/">great coverage</a> and are representative of similar devices (with the same version OS, from the same manufacturer, etc.).</p>

## OEM Customizations

One stumbling block with Android — like any open-source project — is its customizability, which exposes the entire platform to problems. What is called “fragmentation” by developers would be considered a point of differentiation for OEMs. In recent years, all <a href="https://www.tested.com/tech/android/460386-state-oem-skins-android/">Android OEMs have eagerly built their own UI layers</a>, skins and other middleware on top of vanilla Android. This is a significant source of the fragmentation that affects developers.

In addition to UI layers, many OEMs have introduced <a href="https://forum.xda-developers.com/showthread.php?t=2570435">legacy software</a> — tailored to Android — and it, too, is preventing developers from building their apps to work identically across different brands of phones.</p>

<a href="https://www.xda-developers.com/android/three-all-in-one-solutions-for-android-driver-issues/">Drivers also cause major problems</a>, many related to graphics. Certain chipset manufacturers have done an especially bad job at updating their graphics drivers, which makes the colors in apps, games and any graphic content inconsistent across phones. Developers might encounter entirely different color schemes on various Android devices, none close to what they intended.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1408d21-92dc-41c9-9bb2-7db539b122e0/06-q1-failed-onecore-color-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84d4057f-ebfc-4ae3-a311-9df12d473521/06-q1-failed-onecore-color-opt-500-500x362.png" alt="Failure rate by OEM." width="500" height="362" /></a><figcaption>Failure rate by OEM. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1408d21-92dc-41c9-9bb2-7db539b122e0/06-q1-failed-onecore-color-opt.png">View large version</a>)</figcaption></figure>

### Key Findings Related to OEM Customizations

*   No surprise, Samsung devices are among the most robust and the most problematic. For example, Galaxy Nexus GT-I9250 is one of the most robust devices in all categories, while the Samsung Infuse 4G SGH-I997 failed the most in those same categories.
*   Asus devices, along with Xiaomi devices, are the most robust. Xiaomi implements Android differently, however; for instance, pop-ups make the controllability of some devices impossible.
*   Coolpad has, by volume, the most problems. Among the biggest brands, HTC has the least error-prone devices.
*   All of the big brands — HTC, Samsung, Sony and LG — have customizations that are problematic for certain types of applications. For example, Sony’s customizations breaks some basic functionality, such as viewing PDFs. Samsung’s customizations has problems with taking photos with the camera and interrupting calls.</p>

### Tips and Takeaways

*   The most common misconception is that Nexus devices are the best for testing. Those devices typically have the latest OS version and little to no OEM customization.
*   Pay attention to carrier- and operator-branded devices as well. Some of them implement Android totally differently, regardless of the name of the device or brand.</p>

## Dependencies On Other Software

Some applications require access to other apps. For example, many apps and games incorporate social media, and in the worst implementations, developers have assumed that every device integrates popular social media apps. Some devices come with those social media apps preinstalled, but if not, then your application just won’t work properly. Unfortunately, problems with software dependency turn into problems for app developers.</p>

### Key Findings Related to Dependencies on Other Software

*   92% of apps integrate with the given platform to show ads.
*   65% of apps integrate with at least one social media platform.
*   48% of apps integrate with at least two social media platforms.
*   33% of apps integrate with at least three or more social media platforms.</p>

### Tips and Takeaways

Check whether the software that your application depends on is installed on all devices. Do not assume that all of those third-party apps and other software exist on every device!

## Android Hardware

The Android device eco-system continues to grow and evolve. Many handset manufacturers continue to churn out devices with amazing specifications and hardware and with different form factors. Naturally, the <a href="https://opensignal.com/reports/fragmentation-2013/">sheer number of possible device configurations</a> presents a challenge to developers. Ensuring that an application works well on the widest range of devices is crucial and is the easiest way to avoid frustrating end users.

Most developer carefully weigh the <a href="https://insights.wired.com/profiles/blogs/the-best-advice-for-app-developers-skip-emulators#axzz38bhWO19j">pros and cons of testing on emulators and testing on real devices</a> to follow the right strategy. Typically, emulators are used in initial stages of development, while real devices are brought in later in the game. Your choice of platform on which to build your next big thing should be as honest as possible — from day one. In our experience, that is a cornerstone of creating a successful app — and gaining those hundreds of millions of downloads.</p>

### Screen Resolution, Display and Colors

The key to success with any app — especially games — is to get the UI and graphics right. This is a challenge because there are a lot of different resolutions, a lot of ways to present content and, naturally, a lot of different hardware.

With new high-end devices gaining popularity among users, the Android eco-system seems to be quickly headed towards high-resolution displays. High-resolution screens obviously make for a better user experience, but to take advantage of this, developers need to <a href="https://bitbar.com/test-early-test-often-testing-as-part-of-your-app-development/">update their apps and test for them</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00d88c96-e0ab-4b37-a4f8-ab13a23dd026/07-color-error-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66349f10-a990-4401-a607-2ead5df6fe3d/07-color-error-opt-500.jpg" alt="Identical app on 3 different Android devices running identical OS version and hardware." width="500" height="276" /></a><figcaption>Can you see the difference? An identical app is running on three different Android devices with the same OS version and hardware specifications. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/00d88c96-e0ab-4b37-a4f8-ab13a23dd026/07-color-error-opt.jpg">View large version</a>)</figcaption></figure>

However, <a href="https://developer.android.com/guide/practices/screens_support.html#testing">display resolution</a> is not always the cause of headaches for developers. In fact, applications fail more often because of screen orientation, density, color and the overall quality of the device’s screen. For example, many games suffer from poor-quality displays. For instance, a button in a certain part of the UI might get shown in a different shade than the one intended by the designer — or, in some cases, a totally different color.

This is a common issue. It can result not only from hardware components, but also when display drivers are implemented incorrectly. Graphical content could even be invisible in some apps because of color brightness or low pixel density. This kind of failure is apparent from screenshots in our tests.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142a2c8a-d019-487d-9d9a-d064689756f8/08-q1-failed-screenreso-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9655fc9b-7f5f-457a-b49f-d9bcf83ec676/08-q1-failed-screenreso-opt-500.png" alt="Failure rate by screen resolution" width="500" height="362" /></a><figcaption>Failure rate by screen resolution. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/142a2c8a-d019-487d-9d9a-d064689756f8/08-q1-failed-screenreso-opt.png">View large version</a>)</figcaption></figure>

No surprise that as the display resolution gets higher, apps present fewer problems. There are a few exceptions to this, but they can be attributed to how <a href="https://developer.android.com/about/dashboards/index.html">certain OEMs use various resolutions</a> in both low- and high-end devices.

The Android OS provides a <a href="https://www.smashingmagazine.com/2014/01/10/four-ways-to-build-a-mobile-app-part2-native-android/">environment to develop apps consistently</a> across devices, and it handles most of the work of adjusting each application’s UI to the given screen. Also, it comes with APIs that enables the developer to optimize an application’s UI for a <a href="https://www.smashingmagazine.com/2012/06/01/getting-to-know-android/">particular screen size or density</a>. For example, you might want one UI for tablets and another for handsets. Although the OS scales and resizes to make an application work on different screens, you should still <a href="https://www.androiduipatterns.com/">optimize your application for different screen sizes</a> and densities. In doing so, you’ll improve the user experience on all devices, and users will believe that your application was designed for their particular device, rather than simply stretched to fit their screen.</p>

### Key Findings Related to Screen Resolution

*   The median of error was the smallest in resolutions of 2560 × 1600 pixels (0.4%), then 1280 × 800 (0.7%) and 1280 × 720 pixels (1.5%). It was highest in resolutions of 400 × 240 (45%) and 320 × 240 pixels (44%).
*   The most typical problem relates not to resolution or the scaling of graphical content, but to how content adjusts to the orientation of the screen. According to our data, problems with screen orientation are 78% more likely than problems with the scaling of graphical content.
*   Wrong color themes and color sets were reported in 18% of devices, while 24% of apps appeared correctly on all 288 different devices.
*   In some cases, an Android OS update or OEM update fixed a display issue, but the percentage was relatively low (6%).
*   Apps worked nearly the same on high- and low-end devices (based on chipset) with the same resolution (just a 2% difference).
*   In general, the bigger a device’s display, the more likely an app will perform better.</p>

### Tips and Takeaways

*   Design graphical content for multiple screen sizes, but make it scale to different sizes automatically. This is strictly a design issue.
*   Many problems with resolution, display and color can be avoided by designing an application correctly in the first place and by testing it thoroughly on real Android devices. Emulators won’t yield reliable results or lead to a robust application.</p>

### Memory

Anything can happen when an Android device <a href="https://source.android.com/devices/low-ram.html">runs out of memory</a>. So, how does your application work when a device is low on memory?

Developers deal with this problem rather often. Many apps won’t run on certain Android devices because they consume too much memory. Typically, the <a href="https://www.appannie.com/indexes/all-stores/rank/overall/">most popular apps</a> — ones rated with four and five stars — do not have this problem because memory management has been implemented the right way, or else they have been excluded from being downloaded on low-end devices entirely. Too many of today’s apps were originally developed for high-end devices and can’t be run on low-end devices. What is clear is that you can easily tackle this problem by checking how your app works with different memory capacities.

Memory seems to significantly affect how a device copes with an application. If a device’s RAM is equal to or less than 512 MB, then the device will crash 40% of the time when certain applications are running.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dab126d6-8034-4a99-a598-c5d3ef4f14c4/09-q1-failed-ram-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19cdaae5-4cf6-4bc7-b13a-b6040ef4503e/09-q1-failed-ram-opt-500.png" alt="Failure rate of apps by memory size of device" width="500" height="351" /></a><figcaption>Failure rate of apps by memory size of device. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dab126d6-8034-4a99-a598-c5d3ef4f14c4/09-q1-failed-ram-opt.png">View large version</a>)</figcaption></figure>

If a device’s RAM is higher than 512 MB, then the device will crash approximately 10% of the time. That is statistically significant.</p>

### Key Findings Related to RAM

*   The median of error was lowest with RAM of 1024 MB (1%), then 1536 MB (3%) and next 768 MB (16%). It was highest with RAM of 336 (45%) and 168 MB (44%).
*   Approximately 10% of apps run on devices with more than 512 MB crash due memory-related issues.
*   Many OEMs do not give their devices the 512 MB of RAM that Google recommends as the minimum. Such devices are 87% more likely to have problems than devices with more memory.
*   The probability of failure drops 41% for devices that contain more than 576 MB of memory.</p>

### Chipsets

The difference in performance between <a href="https://tech.firstpost.com/news-analysis/all-you-need-to-know-about-mobile-phone-chipsets-27704.html">silicon chipsets</a> (CPU, GPU, etc.) is pretty amazing. This is not necessarily obvious to end users. Some people pay too much attention to the CPU’s clock rate, rather than the chipset and other factors that affect the performance of the device.

Imagine developing something that is targeted at high-end devices but that runs on low-end hardware. It simply wouldn’t work. The user experience would obviously suffer because a high-end app running on a low-end chipset with a low clock-frequency rate would suffer in performance. Many apps suffer severely because the activities on screen are synced with the clock, and the UI can’t refresh quickly enough to keep up with it. For users, this translates into poorly implemented graphics, blinking screens and general slowness.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/808934eb-c74b-4772-9335-5bf3010ae984/10-q1-failed-cpu-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27fbbba2-632a-4c92-a4fc-e6c7dbdac72f/10-q1-failed-cpu-opt-500.png" alt="Failure rate of apps by device clock rate" width="500" height="364" /></a><figcaption>Failure rate of apps by device clock rate. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/808934eb-c74b-4772-9335-5bf3010ae984/10-q1-failed-cpu-opt.png">View large version</a>)</figcaption></figure>

Let’s first look at the clock rate of devices that we tested.

To compare chipsets more easily, we categorized them based on their number of cores: single, dual and quad.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bb3eba3-0389-46c1-8e22-12ce23a71446/11-q1-failed-onecore-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75e7367f-b6d3-4475-b313-2fcabc54922b/11-q1-failed-onecore-opt-500.png" alt="Failure rate by single-core chipset" width="500" height="362" /></a><figcaption>Failure rate by single-core chipset. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bb3eba3-0389-46c1-8e22-12ce23a71446/11-q1-failed-onecore-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0874bc8-f306-4f32-91e6-e8f6b6191f70/12-q1-failed-dualcore-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bbfd4f78-d843-4789-8ce9-50f838b9ac03/12-q1-failed-dualcore-opt-500.png" alt="Failure rate by dual-core chipset" width="500" height="349" /></a><figcaption>Failure rate by dual-core chipset. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0874bc8-f306-4f32-91e6-e8f6b6191f70/12-q1-failed-dualcore-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/987e95f6-9875-47bb-bdbe-b5e213f84f3c/13-q1-failed-quadcore-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc389cb4-330d-4bd2-b08c-da9a9abf4866/13-q1-failed-quadcore-opt-500.png" /></a><figcaption>Failure rate by quad-core chipset. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/987e95f6-9875-47bb-bdbe-b5e213f84f3c/13-q1-failed-quadcore-opt.png">View large version</a>)</figcaption></figure>

Unlike the CPU architecture in chipsets — which is manufactured primarily by <a href="https://www.arm.com">ARM</a> — the graphics portion is manufactured by multiple vendors, which gives some semiconductor companies the flexibility to pick and choose which GPU goes best with the CPU in their chipsets.

Back in the day, the primary job of the graphics card was to render high-end graphical content and 3-D images on the screen. Today, GPUs are used for much more than games and are as crucial as the CPU, if not more so.

Today, all of the recent Android OS versions — Ice Cream Sandwich, Jelly Bean, Kit Kat and so on — rely heavily on the GPU because the interface and all animations are rendered on it, which is how you’re able to achieve transition effects that are buttery smooth. Today’s devices have many more GPU cores than CPU cores, so all graphics and rendering-intensive tasks are handled by them.</p>

### Key Findings Related to Chipset

*   **Single core**.  The median of error was lowest in Intel Atom Z2420 (0.2%), then in Qualcomm Snapdragon S2 MSM8255T (1.1%).
*   **Dual core**.  The median of error was lowest in MediaTek MT8317 (0.3%), then in Intel Atom Z2560 (0.4%).
*   **Quad core**.  The median of error was lowest in both MediaTek MT8125 (0.2%) and Qualcomm Snapdragon 600 APQ8064AB and APQ8064T (0.2%).
*   Many high-end devices are updated to the latest version of Android and get the latest OEM updates, which makes them more vulnerable to problems (67%) than low-end devices with the original OS version.
*   Clock rate doesn’t directly correlate with performance. Some benchmarks show significant improvement in performance, even when the user experience and the apps on those chipsets and devices don’t improve significantly.
*   Power consumption is naturally a bigger problem in some batteries, and some devices run out of battery life quickly. However, this is tightly related to the quality and age of the battery and cannot be attributed solely to the chipset.</p>

### Tips and Takeaways

*   Thoroughly test your application on all kinds of devices — low end, mid-range and high end — if it has heavy graphics (such as apps with video streaming) or uses the GPU heavily, to ensure maximal performance across an ecosystem.
*   Do not assume that your app works across different chipsets. Chipsets have a lot of differences between them!

### Other Hardware (Sensors, GPS, Wi-Fi, etc.)

Misbehaving sensors — and we’re not talking about sensors that are <a href="https://android.stackexchange.com/questions/59532/how-can-i-calibrate-the-tilting-sensor-on-android">poorly calibrated</a> or that cannot be calibrated — cause various problems in games that take input from the way the user handles the device. With GPS, the known problems are navigating indoors and not being able to reach satellites from some locations. To take a similar example with media streaming, video that is meant to be viewed in landscape mode might work well in landscape mode, but the user would have to rotate the device 180 degrees to see it right. Frankly, there is no way to properly test orientation with an emulator; also, things related to the accelerometer, geo-location and push notifications cannot be emulated or could yield inaccurate results.

Network issues come up every now and then, and a slow network will very likely affect the usability and experience of your application.</p>

## Conclusion

Today, all of the recent Android OS versions — Ice Cream Sandwich, Jelly Bean, Kit Kat and so on — rely heavily on the GPU because the interface and all animations are rendered on it, which is how you’re able to achieve transition effects that are buttery smooth. Today’s devices have many more GPU cores than CPU cores, so all graphics and rendering-intensive tasks are handled by them.</p>

### Key Findings Related to Chipset

*   **Single core**.  The median of error was lowest in Intel Atom Z2420 (0.2%), then in Qualcomm Snapdragon S2 MSM8255T (1.1%).
*   **Dual core**.  The median of error was lowest in MediaTek MT8317 (0.3%), then in Intel Atom Z2560 (0.4%).
*   **Quad core**.  The median of error was lowest in both MediaTek MT8125 (0.2%) and Qualcomm Snapdragon 600 APQ8064AB and APQ8064T (0.2%).
*   Many high-end devices are updated to the latest version of Android and get the latest OEM updates, which makes them more vulnerable to problems (67%) than low-end devices with the original OS version.
*   Clock rate doesn’t directly correlate with performance. Some benchmarks show significant improvement in performance, even when the user experience and the apps on those chipsets and devices don’t improve significantly.
*   Power consumption is naturally a bigger problem in some batteries, and some devices run out of battery life quickly. However, this is tightly related to the quality and age of the battery and cannot be attributed solely to the chipset.</p>

### Tips and Takeaways

*   Thoroughly test your application on all kinds of devices — low end, mid-range and high end — if it has heavy graphics (such as apps with video streaming) or uses the GPU heavily, to ensure maximal performance across an ecosystem.
*   Do not assume that your app works across different chipsets. Chipsets have a lot of differences between them!

### Other Hardware (Sensors, GPS, Wi-Fi, etc.)

Misbehaving sensors — and we’re not talking about sensors that are <a href="https://android.stackexchange.com/questions/59532/how-can-i-calibrate-the-tilting-sensor-on-android">poorly calibrated</a> or that cannot be calibrated — cause various problems in games that take input from the way the user handles the device. With GPS, the known problems are navigating indoors and not being able to reach satellites from some locations. To take a similar example with media streaming, video that is meant to be viewed in landscape mode might work well in landscape mode, but the user would have to rotate the device 180 degrees to see it right. Frankly, there is no way to properly test orientation with an emulator; also, things related to the accelerometer, geo-location and push notifications cannot be emulated or could yield inaccurate results.

Network issues come up every now and then, and a slow network will very likely affect the usability and experience of your application.</p>

## Conclusion

In this article, we’ve focused on two areas — Android software and hardware — and what app developers need to know about both. The Android eco-system is constantly changing and new devices, OS versions and hardware come out every week. This naturally presents a big challenge to application developers.

Testing on real devices prior to launch will make your app significantly more robust. In the next article, we will dive deep into this topic, covering the most essential testing methods, frameworks, devices and other infrastructure required to maximize testing.

How do you test mobile apps, and what devices do you use and why? Let us know which aspects of mobile app testing you would like us to cover in the next article.

{{< signature "da, al, ml, il" >}}


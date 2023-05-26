---
title: 'The Basics Of Test Automation For Apps, Games And The Mobile Web'
slug: basic-test-automation-for-apps-games-and-mobile-web
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90737464-1976-425f-8779-a80dffaccfe5/01-device-rack-opt-small.jpg
date: 2015-01-14T22:54:26.000Z
author: villeveikkohelppi
summary: >-
  Testing is crucial to ensuring success in the highly competitive landscape of mobile apps and games. But even poorly planned testing can take up 20 to 50% of your total development effort, in which case it would also account for the single biggest cost in your budget. To ensure that testing is extremely efficient, covering the breadth of today’s mobile ecosystems and device models, the best option is an online cloud-based service.
description: >-
  Testing is crucial to ensuring success in the highly competitive landscape of mobile apps and games. But even poorly planned testing can take up 20 to 50% of your total development effort, in which case it would also account for the single biggest cost in your budget. To ensure that testing is extremely efficient, covering the breadth of today’s mobile ecosystems and device models, the best option is an online cloud-based service.
categories:
  - Mobile
  - Apps
  - Testing
  - Devices
  - Games
  - iOS
  - Android
---
Mobile application ecosystems &mdash; let’s count Android and iOS here &mdash; are unbelievably dynamic, but they also suffer from both software and hardware fragmentation. This is especially true for Android, but <a href="https://www.zdnet.com/ios-8-usage-figures-showing-signs-of-stress-fragmentation-after-initial-uptick-7000034389/">fragmentation also exists in the iOS ecosystem</a>, as experienced with the rollout of iOS 8. As the latest version of iOS was released, many existing apps were made clumsy on updated devices.

Even the new iPhone 6 and <a href="https://www.gottabemobile.com/2014/10/22/iphone-6-plus-problems-fixes/">iPhone 6 Plus have had not-so-typical issues</a> for Apple devices. In addition, a significant proportion of users with older devices have very few options: essentially, buy new hardware (i.e. a new device) to get everything working well.</p>

In the Android world, things are different. As OEMs launch new devices, software updates and customizations for their devices, <a href="https://www.smashingmagazine.com/2014/10/02/what-every-app-developer-should-know-about-android/">application and game developers get serious headaches</a> trying to keep their latest products up to snuff and fully compatible with all possible device variants. Making a certain app or game work only on high-end devices is out of the question, though. Why would a developer want to miss out on a significant chunk of potential users?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/995386f7-e7d4-43fc-b24c-2e4f74b7e43e/01-device-rack-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90737464-1976-425f-8779-a80dffaccfe5/01-device-rack-opt-small.jpg" alt="Automation enables simultaneous testing on hundreds of real devices" width="500" height="333" /></a><figcaption>Automation enables simultaneous testing on hundreds of real devices. (Image credit: <a href="https://bitbar.com/testing/">Testdroid</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/995386f7-e7d4-43fc-b24c-2e4f74b7e43e/01-device-rack-opt.jpg">View large version</a>)</figcaption></figure>

Professional automated testing software is a solution to a common problem: how to produce high-quality, robust and reliable software with the ever-growing complexity of technology and under massive competitive pressure. <strong>Automated software testing is a cost-effective solution</strong> to this problem. Not to mention, it provides three business benefits:

*   increased testing efficiency,
*   increased testing effectiveness,
*   faster time to market.

This article walks through a sample use case for test automation and provides a downloadable example to get you started. Also, we’ll focus on different aspects of mobile test automation and explain how this relatively new yet popular topic can help mobile app and game developers to build better, more robust products for consumers. With the advanced example later in the article, we’ll show how image recognition can be used to test mobile games; specifically, we’ll run <a href="https://bitbar.com/the-basics-of-mobile-web-testing-using-appium-selenium/">Appium’s test automation</a> framework against Supercell’s <a href="https://www.supercell.net/games/view/clash-of-clans">Clash of Clan</a> game to illustrate how image recognition can be built into the test-automation process.</p>

{{% feature-panel %}}

## Test Automation Is Perfect For Mobile App Development

Developing mobile applications is very different from developing PC software or even embedded software. <a href="https://www.gartner.com/newsroom/id/2823619">Mobile development is meant to be agile</a>, and a lot of great tools and practices have been developed for that agility. However, doing something manually &mdash; such as testing an app &mdash; is never agile, which is why test automation has shown tremendous growth among app and game developers, speeding up their doings and yielding robust and better results.

To achieve compatibility between users, devices and the market, <a href="https://bitbar.com/test-early-test-often-testing-as-part-of-your-app-development/">including test automation as a part of the agile development process</a> is typical. Fortunately, a lot of tools are available, and test automation is a perfect fit for this process. For example, let’s say your typical development sprint is two weeks. You have daily standups and a lot of scrum activities, and you own internal policies that gear development to the final product. <strong>Test automation offers a significant value-add</strong> by enabling testing to be done in parallel &mdash; for example, as nightly test sessions. By the next morning, the tests will have been finalized and the results of the latest regression will be ready for review. Fixing an issue earlier will save a lot of time and get developers to finalize the product sooner; most importantly, it <a href="https://autotestcentral.com/how-test-automation-can-help-to-achieve-5-stars/285">cumulates to better quality</a>, with fewer bugs.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0014918d-5d7c-4156-825b-fc2c12469ac5/02-value-diagram-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40c17fb1-b1fb-4cc4-befb-cd3a4d2a2c1c/02-value-diagram-opt-small.jpg" alt="Value that test automation brings to agile process." width="500" height="385" /></a><figcaption>The value that test automation brings to the agile process. (Image credit: <a href="https://bitbar.com/testing/">Mobile App Testing</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0014918d-5d7c-4156-825b-fc2c12469ac5/02-value-diagram-opt.jpg">View large version</a>)</figcaption></figure>

Test automation offers the possibility to test mobile apps instantly and effectively. Once tests have been automated, they can be executed quickly and repeatedly, again and again. In almost all cases, this is the most cost-effective method for <a href="https://en.wikipedia.org/wiki/Regression_testing">regression testing</a> of software products that have a long maintenance life. In fact, test automation of any mobile app is the best way to increase the effectiveness, efficiency and coverage of the testing process. The true benefit of automation comes not only from the repeatability of tests, but also from the ability to execute tests that probably could not even be performed manually.</p>

## Things To Consider When Automating Mobile App Testing

Let’s look at how test automation (as opposed to manual testing) can improve the development process, add value and speed up development.</p>

### Costs and Assets

Regardless of whether you go for manual or automated testing, you’ll need the following assets and resources (all of which cost money): time, people, infrastructure, tools and training. Depending on the size of the project and the application, test automation will quite obviously provide a <strong>good return on investment</strong>. For example, once test cases have been created, automated tests can be run over and over again at no additional cost, and these can be more rapidly completed than any manual tests. Automated software testing can reduce the time required to run repetitive tests from weeks to hours. This is a significant time-saving that translates directly into cost-saving.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2caf892-a6b5-4308-b163-816636cbb50d/03-testing-in-ci-process-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cff21939-518d-4bf5-9454-1c279b49e3e1/03-testing-in-ci-process-opt-small.jpg" alt="Continous integration together with mobile app testing" width="500" height="255" /></a><figcaption>Continous integration together with mobile app testing. (Image credit: <a href="https://bitbar.com/testing/">Testdroid</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2caf892-a6b5-4308-b163-816636cbb50d/03-testing-in-ci-process-opt.png">View large version</a>)</figcaption></figure>

### Integrated App Development And Testing Cycle

Increasing efficiency and productivity with automation actually starts with adopting a new mindset. Software tests have to be repeated often during all development cycles to ensure the best possible quality of an application. Every time <a href="https://bitbar.com/increase-efficiency-and-productivity-with-test-automation/">source code is modified</a>, software tests should be repeated. For each release, your software should be tested on all supported variants of operating systems and all configurations of hardware. Manually repeating these tests would be costly and time-consuming. For example, running comprehensive tests manually on all variants of Android and on actual devices would take a lot of time.</p>

### Tools and Technology: Test Automation Frameworks

To get the most out of your efforts and maximize testing coverage, select the most robust and most <a href="https://en.wikipedia.org/wiki/Cross-platform">cross-platform</a> method. That automated methods can be used both to validate requirements and to reduce costs through automated test-case generation is well known. However, the full automatization of large software entities also comes with a cost that many companies haven’t been ready to pay for. Historically, one of the reasons has been a concern over the lack of adequate integration with well-established development life cycles.</p>

### Test Coverage and Reusability: Open Standards Mean No Vendor Lock-In

Automated testing can increase the depth and scope of tests and significantly improve software quality. Lengthy and thorough tests &mdash; often not doable with manual testing &mdash; can be run automatically. Ideally, test cases should have full access to an application and <a href="https://agiledata.org/essays/tdd.html">test all aspects of it</a> &mdash; memory contents, data tables, file contents and internal program states &mdash; to determine whether the product behaves as expected. Automated tests can easily <strong>execute thousands of complex test cases during every test run</strong>, providing coverage that is simply not possible with manual testing. Developers, freed from repetitive manual tests, will have more time to create new automated test cases and build more compelling features (and then more test cases).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ea832c3-02b7-4d57-8e0a-329c2cb0c38b/04-time-to-market-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3b55078-0dd2-4edc-b98c-7fe1d2e9abdc/04-time-to-market-opt-small.jpg" alt="Time to market for mobile web" width="500" height="396" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ea832c3-02b7-4d57-8e0a-329c2cb0c38b/04-time-to-market-opt.jpg">View large version</a>)</figcaption></figure>

### Improve Effectiveness and Finalize Sooner

In a nutshell, professional automated testing software is a solution to a common problem: how to produce high-quality, robust and reliable software with the ever-growing complexity of technology and under massive competitive pressure. Automated testing improves business results in three ways: greater testing efficiency, greater testing effectiveness and a shorter time to market.</p>

{{% ad-panel-leaderboard %}}

## Different Ways to Automate Mobile Testing

In general, there are three ways to automate the testing of mobile apps.</p>

### Handwritten Test Scripts

Typically, this is the best choice when you know what you’re doing and when you have programming-capable people doing the test scripts. Plenty of options are available for test automation frameworks, tools and integration &mdash; both commercial and open-source offerings. Having your engineers write all of the test scripts will take up some time and tie up resources, but it will get you exactly what you want: well-structured, thorough scripts that test precisely the aspects of your app that you want to test.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41bc94ef-c825-4463-8b91-cad093f01dc6/05-different-ways-to-automate-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49b0c252-b489-464a-bf1d-58d8ae5a4aa6/05-different-ways-to-automate-opt-small.jpg" alt="Manual versus automated testing for mobile apps" width="500" height="244" /></a><figcaption>Manual versus automated testing for mobile apps. (Image credit: <a href="https://bitbar.com/testing/">Testdroid</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41bc94ef-c825-4463-8b91-cad093f01dc6/05-different-ways-to-automate-opt.jpg">View large version</a>)</figcaption></figure>

### Record-Playback Approach

This approach is less error-prone because nothing needs to be written in code, but it is typically more limited in functionality. Tests can be quickly recorded and then played back again and again against different OS versions and device configurations. These tests focus on user interactions and user-driven activities. Some things might fall beyond a test’s scope (such as integration with other technologies and compatibility with other software).</p>

### Automatic Test Exercisers

Automatic test exercisers provide a great way to smoke-test applications. No specific tests are needed; rather, the focus is on testing user-interface logic (such as opening menus, clicking buttons, swiping and multi-gesture actions). Automatic test exercisers yield the least exact results but provide quick feedback on each iteration of an app.</p>

## Focus Areas In Testing For Mobile Apps And Games

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bbcdfa8-f3be-4c59-b2d0-ee44c8dc19bf/06-different-ways-to-test-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bb0f697-cb4b-4566-999e-25495c42cdbd/06-different-ways-to-test-opt-small.jpg" alt="Different ways to automate mobile app testing" width="500" height="340" /></a><figcaption>Different ways to automate mobile app testing. (Image credit: <a href="https://bitbar.com/testing/">Testdroid</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9bbcdfa8-f3be-4c59-b2d0-ee44c8dc19bf/06-different-ways-to-test-opt.jpg">View large version</a>)</figcaption></figure>

### User Interface and Functionality

A user interface and its overall functionality will directly affect <a href="https://www.appannie.com/indexes/all-stores/rank/overall/">how successful your app or game</a> will be. These two things, which encompass visual appeal and gameplay, are the most important things to get right &mdash; and you must ensure that device fragmentation doesn’t break any of these. Various things in the UI need to be tested:

*   **UI layouts and elements**.  Games especially are typically targeted at a high number of different screen resolutions and screen types. Regression testing should be done each and every time the UI’s layout changes to ensure that the game works.
*   **Menu structure and functions**.  Testing menu structures, functionality and behavior can be automated with instrumentation and the help of different test-automation frameworks.
*   **Screen orientation**.  Surprisingly, so many apps and games out there get this wrong. If a screen’s orientation changes during an interaction, for example, what happens? What is supposed to happen? Does the app or game work well in both landscape and portrait modes?
*   **Screen resolution**.  A lot of screen resolutions exist, especially on Android, and auto-scaling will usually help developers. However, test your game across these resolutions to ensure that the graphics do not stretch.</p>

### Graphics Performance

Performance needs to be consistent across all <a href="https://www.androidcentral.com/devices">device variants</a> among your users. Because of this, test on as many real devices as possible. To determine how well your app or game responds to various levels of usage, including performance and battery usage, consider creating tests that last for hours. To determine whether your game runs effectively under a heavy load for a long time, run load (or stress) tests. These performance tests will measure, for example, how responsive your game is on real devices.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ee57fb9-7457-4421-aa26-a6ef5e72f22a/07-performance-testing-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2eac8b44-4a06-4ada-9796-b6b3c2229547/07-performance-testing-opt-small.jpg" alt="Performance testing of CPU load and memory consumption" width="500" height="348" /></a><figcaption>Performance testing of CPU load and memory consumption. (Image credit: <a href="https://bitbar.com/testing/">Testdroid</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ee57fb9-7457-4421-aa26-a6ef5e72f22a/07-performance-testing-opt.png">View large version</a>)</figcaption></figure>

### Usability and User Experience (i.e. Good Entertainment)

Testing usability, navigation flow and user experience simply cannot be done on a desktop with a mouse and keyboard. So, <a href="https://bitbar.com/rely-only-on-real-emulators-vs-devices/">forget emulators and use only real devices</a>. And to test how usable and entertaining your app is, consider these two important things:

*   **User interaction and responsiveness**.  Testing performance is critical because this will make make or break the user experience. Performance lag, for example, is easy to expose with real devices.
*   **Background events**.  Interruptions, battery consumption and the effect of battery chargers on overall performance and usage all have a significant impact on the user experience &mdash; and entertainment value.</p>

### Multi-User Features

Nowadays, multi-user support is common in both apps and games. <strong>Testing multi-player capabilities is important</strong> and is naturally more challenging, requiring real users to measure performance. A typical case is a game communicating with the back-end server. In this case, connectivity is essential, to synchronize the back end with devices that need to get information about the gameplay. You should test a ton of different scenarios, many of which could severely affect the game’s experience, resulting in negative feedback and the game being uninstalled by users.</p>

### Social Integration

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77dca003-8d1a-43b6-9cee-e26793f0634f/08-social-integrations-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8659180a-05de-4460-942f-e45c41fa4ba5/08-social-integrations-opt-small.jpg" alt="Testing social integration in mobile apps" width="500" height="452" /></a><figcaption>Testing social integration in mobile apps. (Image credit: <a href="https://bitbar.com/testing/">Testdroid</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77dca003-8d1a-43b6-9cee-e26793f0634f/08-social-integrations-opt.jpg">View large version</a>)</figcaption></figure>

Integration with social networks is another important factor. Being able to share something across an ecosystem, with friends or just with oneself, is essential in many apps. Test this thoroughly with real Android and iOS devices, with different OS versions and different device configurations, to assess functionality and ease of use.</p>

### Security and Liabilities

Nearly all developers use some open-source components in their apps. This practice is widely accepted and highly recommended because it offloads the development of code for non-core functionality. However, identifying vulnerabilities and licensing restrictions with third-party code is often neglected by developers.</p>

## Breakdown: Android Test Automation Frameworks

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dbe570d-547b-4bff-8a66-eda941d7a7f8/09-frameworks-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b94e37e4-551c-433c-be1e-b2016c95150c/09-frameworks-opt-small.jpg" alt="Comparison of test automation frameworks" width="500" height="252" /></a><figcaption>Comparison of test automation frameworks. (Image credit: <a href="https://bitbar.com/testing">Testdroid</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dbe570d-547b-4bff-8a66-eda941d7a7f8/09-frameworks-opt.png">View large version</a>)</figcaption></figure>

<a href="https://code.google.com/p/robotium/">Robotium</a> is an Android test automation framework that fully supports native and hybrid applications. Robotium makes it easy to write powerful and robust automatic black-box UI tests for Android applications. With the support of Robotium, test case developers can write function, system and user acceptance test scenarios, spanning multiple Android activities.</p>

<a href="https://developer.android.com/tools/help/uiautomator/index.html">UIautomator</a>, by Google, provides an efficient way to test UIs. It creates automated functional test cases that can be executed against apps on real Android devices and emulators. It includes a viewer, which is a GUI tool to scan and analyze the UI components of an Android app.</p>

<a href="https://code.google.com/p/android-test-kit/wiki/Espresso">Espresso</a>, by Google, is a pretty new test automation framework that got open-sourced just last year, making it available for developers and testers to hammer out their UIs. Espresso has an API that is small, predictable, easy to learn and built on top of the <a href="https://developer.android.com/tools/testing/testing_android.html#Instrumentation">Android instrumentation framework</a>. You can quickly write concise and reliable Android UI tests with it.</p>

<a href="https://bitbar.com/blog/how-to-setup-and-get-started-with-calabash/">Calabash</a> is a cross-platform test automation framework for Android and iOS native and hybrid applications. Calabash’s easy-to-understand syntax enables even non-technical people to create and execute automated acceptance tests for apps on both of these mobile platforms.

And then there’s Appium. OK, let’s get into this one.</p>

## Appium: Executing Tests On Real Devices On A Cloud Service

In a nutshell, <a href="https://appium.io/">Appium</a> is a mobile test automation framework (and tool) for native, hybrid and mobile-web apps for iOS and Android. It uses <a href="https://code.google.com/p/selenium/wiki/JsonWireProtocol">JSONWireProtocol</a> internally to interact with iOS and Android apps using <a href="https://docs.seleniumhq.org/projects/webdriver/">Selenium’s WebDriver</a>.

In its architecture, Appium is an HTTP server written in Node.js that creates and handles multiple WebDriver sessions. Appium starts tests on the device and listens for commands from the main Appium server. It is almost the same as the Selenium server that gets HTTP requests from Selenium client libraries.

In fact, <strong>Appium is a pretty good choice for both apps and games because</strong>, in many cases, apps and games tend to be identical (or at least very similar) on both platforms, Android and iOS &mdash; and so the same test script can be applied to both. Another significant benefit of Appium is that users can write tests using their favorite development tools, environment and programming language, such as Java, Objective-C, JavaScript, PHP, Ruby, Python or C#, among many others.

Appium enables users to execute tests on mobile devices regardless of OS. This is possible because the Appium framework is basically a wrapper that translates <a href="https://bitbar.com/the-basics-of-mobile-web-testing-using-appium-selenium/">Selenium’s WebDriver commands to UIAutomation (iOS)</a>, <a href="https://developer.android.com/tools/help/uiautomator/index.html">UIautomator</a> (Android, API level 17 or higher) or <a href="https://selendroid.io/">Selendroid</a> (Android, API level 16 or lower) commands, depending on the device’s type.

For Android, this is how Appium compares to other test automation frameworks:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38d05911-7c54-416c-87f4-ba3a2662bd4c/10-framework-families-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce4d7a54-63b3-48dc-a93c-d9655077671d/10-framework-families-opt-small.png" alt="Family tree of Android Test automation frameworks" width="500" height="236" /></a><figcaption>Family tree of Android test automation frameworks. (Image credit: <a href="https://bitbar.com/testing/">Testdroid</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38d05911-7c54-416c-87f4-ba3a2662bd4c/10-framework-families-opt.png">View large version</a>)</figcaption></figure>

Android test suites are based on <a href="https://developer.android.com/tools/testing/testing_android.html#JUnit">JUnit</a>. In addition, Android provides an <a href="https://developer.android.com/tools/testing/testing_android.html">architecture and fully integrated testing capabilities with its standard tools</a>, which help developers to test at every level, from unit to framework. <a href="https://developer.android.com/tools/testing/testing_android.html#Instrumentation">Android instrumentation</a> is a set of control methods in the Android system. These methods control an Android component independently of its normal life cycle.

One of the best things about Appium is that, despite sounding architecturally complex, it actually isn’t &mdash; at all. For developers, <strong>it provides support for various programming languages</strong>, freedom from having to select tools, compatibility across the most important platforms (Android and iOS), freedom from having to install and configure devices to test and more.

If you are familiar with Selenium, then you’ve got Appium covered. An Appium test is pretty much the same as a Selenium test: They use the same WebDriver, and <a href="https://code.google.com/p/selenium/wiki/DesiredCapabilities">DesiredCapabilities</a> is used the same way. Configuring an application to run on Appium has a lot of similarities to Selenium &mdash; for example, those DesiredCapabilities. We’ll configure a sample test later in this article.

Also, Appium includes a component called the inspector. This inspector enables a host of functionality &mdash; for example, showing all of those UI elements in the application and enabling basic recording and playback.

However, you may not need the inspector because everything can be done in the code. The example later provides all of the scripts and instructions step by step, without using it.

<p><em>More information about Appium can be found in “<a href="https://appium.io/slate/en/tutorial/ios.html?ruby#getting-started-with-appium">Getting Started With Appium</a>.”</em></p>

{{% ad-panel-leaderboard %}}

## Setting Up The Environment

To get started, first <a href="https://github.com/bitbar/testdroid-samples/tree/master/appium/sample-scripts">download our Appium example</a>. The example is available in Python, Java and Ruby. Then, depending on which programming language you will be using, <a href="https://appium.io/downloads.html">select the appropriate client library</a>. <a href="https://appium.io/introduction.html">Appium’s documentation</a> provides all instructions, help and additional material.</p>

### Mac OS X and Linux

Ensure that Python 2.7.x or later is installed (it’s preinstalled on Mac OS X):

<pre><code class="language-python">$ python --version</code></pre>

Install Python if it’s not already (Linux only):

<pre><code class="language-python">$ sudo apt-get install python2.7</code></pre>

Check whether Python’s “pip” module is already installed:

<pre><code class="language-python">$ pip --version</code></pre>

If you’re on Mac OS X, install pip if it’s not already:

<pre><code class="language-python">$ curl https://raw.githubusercontent.com/pypa/pip/master/contrib/get-pip.py &gt; get-pip.py
$ sudo python get-pip.py
$ rm get-pip.py</code></pre>

If you’re on Linux, install pip if it’s not already:

<pre><code class="language-python">$ sudo apt-get install python-pip</code></pre>

Install the Selenium module for Python:

<pre><code class="language-python">$ sudo pip install selenium</code></pre>

Verify that Selenium is installed:

<pre><code class="language-python">$ pip freeze | grep -i selenium</code></pre>

### Windows

Ensure that Python 2.7.x or later is installed:

<pre><code class="language-python">$ python --version</code></pre>

If it’s not installed, download and run the setup from <a href="https://www.python.org/downloads/">Python’s download center</a>. To add Python environment variables, go to “System properties” → “Advanced System Settings” → “Environment Variables” → “System Variables” → “Edit Path,” and then insert the following at the end (assuming you have installed Python in the default location):

<pre><code class="language-python">C:\Python27\;C:\Python27\Scripts\
</code></pre>

Make sure to restart the command prompt to bring new environment variables into effect.

Also, check whether Python’s pip module is already installed:

<pre><code class="language-python">$ pip --version</code></pre>

Install pip if it’s not already:

<pre><code class="language-python">$ curl https://raw.github.com/pypa/pip/master/contrib/get-pip.py &gt; get-pip.py
$ python get-pip.py
$ del get-pip.py</code></pre>

Install Python’s Selenium module:

<pre><code class="language-python">$ pip install selenium</code></pre>

## Running The First Tests

Download the <a href="https://github.com/bitbar/testdroid-samples/tree/master/appium/sample-scripts/python">Appium sample test script and sample app</a>. The sample package includes the APK for Android, the IPA for iOS and one sample test script. In addition, there are three samples:

*   `appium_example_ios.py`
*   `appium_example_android.py` (for Android API level 17 and above)
*   `appium_example_selendroid.py` (for Android API level 16 and below)

### Step 1: Create Account and Upload the APK

<a href="https://bitbar.com/testing/try-for-free/">Create an account.</a> Note that this service provides a freemium option, and you don’t need a plan to complete these examples using real devices on a cloud service. If you want to access hundreds of device models, then different plans are available.

Before proceeding with running the test script, you’ll need to upload the APK or IPA to Testdroid’s cloud service via HTTP POST. Let’s try that using cURL.

For Mac OS X and Linux:

<pre><code class="language-bash">$ curl -s --user username@example.com:password -F myAppFile=@"/absolute/path/to/app/SampleApp-iOS.ipa" "https://appium.testdroid.com/upload"</code></pre>

### For Windows:

<pre><code class="language-bash">$ cd C:\path\to\directory\containing\the\application
$ curl -s --user username@example.com:password -F myAppFile=@"SampleApp-iOS.ipa" "https://appium.testdroid.com/upload"
</code></pre>

Upon successful upload, you will get a JSON response with <code>status:0</code> and an unique identifier for the uploaded app:

<pre><code class="language-bash">{
   “status”: 0,
   “sessionId”: “abcdefg-1234-5678-abcd-111122223333”,
   “value”: {
      “message”: “Uploads Successful”,
      “uploadCount”: 1,
      “rejectCount”: 0,
      “expiresIn”: 1800,
      “uploads”: {
         “myAppFile“: “abcdefg-1234-5678-abcd-111122223333/SampleApp-iOS.ipa“
      },
      “rejects”: {}
   }
}</code></pre>

### Step 2: Set Credentials and Other Parameters

Open the test script, <code>appium_sample_ios.py</code>, in any text editor. Set <code>screenshotDir</code> to the path where you want those screenshots to be saved on your machine. Set your credentials on <code>testdroid_username</code> and <code>testdroid_password</code> in DesiredCapabilities. Set the <code>myAppFile</code> identifier against <code>testdroid_app</code> in DesiredCapabilities. It should look like this:

<pre><code class="language-bash">desired_capabilities_cloud = {
   ‘testdroid_username’:    testdroid_username,
   ‘testdroid_password:     testdroid_password,
   ‘testdroid_project:      ‘Appium iOS Project 1’,
   ‘testdroid_target:       ‘iOS’,
   ‘testdroid_description:  ‘Appium project description’,
   ‘testdroid_testrun:      ‘Test Run 1’,
   ‘testdroid_device:       testdroid_device,
   ‘testdroid_app:          ‘sample/SampleApp-iOS.ipa’,
   ‘testdroid_platformName: ’iOS’,
   ‘testdroid_deviceName:   ‘iPhone device’,
   ‘testdroid_bundleId:     ‘com.bitbar.testdroid.SampleApp-iOS’
}</code></pre>

### Step 3: Run the Test Script

Execute the following command:

<pre><code class="language-bash">$ python sample-appium_ios.py</code></pre>

The console’s output should look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45204ba7-70ee-4106-9a0b-fbc0c4972109/11-console-output-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a24c5cca-d61a-4a0e-8e74-ff78e08ca2a6/11-console-output-opt-small.jpg" alt="Console output after test script" width="500" height="276" /></a><figcaption>Console’s output after test script. (Image credit: <a href="https://bitbar.com/testing/">Testdroid</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45204ba7-70ee-4106-9a0b-fbc0c4972109/11-console-output-opt.jpg">View large version</a>)</figcaption></figure>

### Step 4: Get Results From Cloud

The screenshots will be available locally on your machine in the directory that you specified in step 2. Log into your cloud service and navigate to the project’s name, as defined in the <code>_project</code> attribute of DesiredCapabilities, to access the following log files:

*   Appium’s server log,
*   Logcat and instruments log.</p>

## Advanced Example: Using Appium For Mobile Game Testing With Image Recognition

In this example, We’re using Supercell’s popular mobile game Clash of Clans. It’s a fantastic game and I’ll bet many of you have played it, so you should be pretty familiar with its look and gameplay. This example does basic clicks through the game’s tutorial.</p>

<pre><code class="language-bash">
## Example script that tests Clash of Clans tutorial first steps
## Works on different resolutions, both iOS and Android

import unittest

from time import sleep
from AppiumCloudTest import AppiumCloudTest, log
from selenium.common.exceptions import WebDriverException

class ClashOfClansTest(AppiumCloudTest):
   def setUp(self):
      # AppiumCloudTest takes settings from environment variables
      super(ClashOfClansTest, self).setUp()

   def test_tutorial(self):
      driver = self.get_driver() # Initialize Appium connection to device

      sleep(10) # Wait for game to load

      # Use this to get detected screen hierarchy
      # print self.driver.page_source

      # Dismiss the in-app purchases dialog if it shows
      okayButton = None
      if self.isAndroid():
         try:
            okayButton = driver.find_element_by_id('button3')
            okayButton.click()
            sleep(5)
         except WebDriverException:
            log("There was no in-app purchases dialog")
      else: # iOS
         self.driver.implicitly_wait(5) # Wait only 5 seconds to find it
         try:
            okayButton = driver.find_element_by_accessibility_id('Okay')
            okayButton.click()
            # No need to sleep here
         except WebDriverException:
            log("There was no in-app purchases dialog")
         self.driver.implicitly_wait(30)

      # Cancel iOS Game Center login
      if self.isIOS():
         #print self.driver.page_source
         try:
            self.driver.implicitly_wait(5)
            cancelButton = driver.find_element_by_accessibility_id('Cancel')
            log("Cancelling iOS Game Center login…")
            cancelButton.click()
            sleep(2)
         except WebDriverException:
            log("The Game Center login was not displayed")
         self.driver.implicitly_wait(30)

      self.screenshot("welcome-chief")

      # Check that a goldmine is on screen
      rect = self.find_image("queryimages/tutorial_goldmine.png",
         screenshot_match="screenshots/goldmine_match.png")
      self.assertIsNotNone(rect,
         "There should be a goldmine on screen at beginning of tutorial")
      log('Gold mine found at %s %s! Continuing…' % (rect[0], rect[1]))

      # Dismiss the bubbles
      self.tap_middle()
      sleep(2) # second blabla
      self.tap_middle()
      sleep(2) # Goblin appears
      self.tap_middle()
      sleep(1)

      # Go to shop
      # NOTE: tap_image does also assert, fails test if target not recognized
      self.tap_image("queryimages/shopbutton.png")
      sleep(1)

      # Buy cannon
      self.screenshot('cannon')
      self.tap_image("queryimages/cannon.png")
      sleep(2)

      # Place the cannon
      self.screenshot('place_the_cannon')
      self.tap_image("queryimages/place_the_cannon.png", width_modifier=0.75)
      sleep(2)
      self.screenshot('finish_now')
      # Use gem to finish right away
      self.tap_image("queryimages/finish_now.png")
      sleep(3)
      # Bring it on!
      self.screenshot('bring_it_on')
      self.tap_image("queryimages/bring_it_on.png", height_modifier=0.75)
      sleep(10)
      self.screenshot('battle')
      sleep(10)
      self.screenshot('end_of_battle')

      # To be continued…

if __name__ == '__main__':
   unittest.main()</code></pre>

Let’s look some of the stages in this test script. The <code>test_tutorial</code> contains the following steps:

1.  It first figures out whether the test executes on Android (`self.isAndroid()`) or iOS. As you can see, it looks for UI content differently. On Android, it tries to find a button by using an element’s ID (`element_name`) and on iOS by using an accessibility ID with a description (“Okay”). The same check happens for iOS’ Game Center login.
2.  Screenshots are taken at various steps and stored in files entered as a parameter in a function call.
3.  A check is done to see whether “goldmine” appears on screen by comparing two PNG files using a `self.find_image` call. If these pictures match (i.e. “goldmine” appears on screen), then the script continues executing the game’s tutorial.
4.  The tutorial proceeds with the following steps:
    1.  Go to shop.
    2.  Buy cannon.
    3.  Place the cannon.The information about all three of these items is stored in those PNG files: `shopbutton.png`, `cannon.png` and `place_the_cannon.png`.
5.  Finally, the tutorial finishes and the battle starts. After the battle, the application is closed.

The video below shows how the test executes at each step. For the video, I’ve used three devices: one iOS (iPhone 4S) and two Android phones (Samsung Galaxy S3 Mini and HTC One X). You can also <a href="https://www.youtube.com/watch?v=Q5U3HwpD1Ec">watch the video on YouTube</a>.</p>

## How Is Image Recognition Used Here?

The example shown uses image recognition (i.e. <a href="https://en.wikipedia.org/wiki/Template_matching">template matching</a>) to identify which features &mdash; basically, pixels and graphic content &mdash; are shown on screen and to compare the two pictures to each other. The algorithm built to recognize images was used on real devices and on two different platforms (Android and iOS), and it used a single test script for both platforms. This sort of image comparison is even very handy for recognizing UI elements and graphics that are resized and/or rotated.

Let’s say the template image has some distinctive features, such as text that can be easily abstracted from the background content. In this case, feature-based recognition can be used. In our example, if the “Button” text has been resized or rotated (or otherwise transformed), we can quickly and easily identify this and take further action.

The following functions explain the approach of comparing images:

<pre><code class="language-bash">def find_image(self, queryimage_file, screenshot_match=None):
   log('Trying to find %s in current screen' % queryimage_file)

   fd,screenshot_file = tempfile.mkstemp()
   try:  
      os.close(fd)
      # print screenshot_file
      head, tail = os.path.split(screenshot_file)
      self.screenshot(tail, path=head)
      head,tail = os.path.split(queryimage_file)
      screenshot_match='%s/%s-match.png' %
         (self.screenshot_dir, tail.split('.')[0])
      return ImageFinder.findImages(queryimage_file,
         "%s.png" % screenshot_file,
         scale_tolerance=0.9,
         screenshot_match=screenshot_match)
   finally:
      os.remove(screenshot_file)</code></pre>

<pre><code class="language-bash">def screenshot(self, name, path=None):
   full_path=None
   if path:
      full_path='%s/%s.png' % (path,name)
   else:
      full_path='%s/%s.png' % (self.screenshot_dir, name)

   try:
      self.get_driver().save_screenshot(full_path)
   except WebDriverException: # for iOS, sometimes times out, so retry!
      #log("Failed taking screenshot %s - retrying" % full_path)
      self.get_driver().save_screenshot(full_path)

   #
   width,height = get_image_size(full_path)
   if(height &gt; width):
      if self.platform_name == 'Android':
         #log("Rotating screenshot 270 degrees")
         os.system('sips -r 270 %s &gt;/dev/null 2&amp;&gt;1' % full_path)
      else:
         #log("Rotating screenshot 90 degrees")
         os.system('sips -r 90 %s &gt;/dev/null 2&amp;&gt;1' % full_path)</code></pre>

<pre><code class="language-bash">def tap_image(self, query_image,
   width_modifier=0.5, height_modifier=0.5, retries=2):

   retries_left = retries
   rect = None
   while retries_left &gt; 0 and not rect:
      rect = self.find_image(query_image)
      retries_left = retries_left - 1
   image_name = os.path.split(query_image)[1]
   self.assertIsNotNone(rect, "Image %s is on screen" % image_name)
   x = rect[0]+rect[2]*width_modifier
   y = rect[1]+rect[3]*height_modifier
   log('%s button found at %s %s (%sx%s), tapping at %s %s' %
      (image_name, rect[0], rect[1], rect[2], rect[3], x, y))

   self.tap(x,y)</code></pre>

<pre><code class="language-bash">def tap(self, x, y):
   log('Tapping at %s,%s' % (x,y))
   driver = self.get_driver()
   if self.isAndroid():
      if self.isSelendroid():
         touch_actions = TouchActions(driver)
         touch_actions.tap_and_hold(x, y).release(x,y).perform()
      else:
         action = TouchAction(driver)
         action.press(x=x, y=y).release().perform()
      else: # iOS
         action = TouchAction(driver)
         # TODO: Temporary hack
         # On iPhone 4S = res. 480 x 320 for taps but screenshots are 960 x 640
         action.press(x=int(x/2), y=int(y/2)).release().perform()</code></pre>

## Conclusion

Testing is crucial to ensuring success in the <a href="https://www.appannie.com/indexes/all-stores/rank/overall/">highly competitive landscape of mobile apps and games</a>. But even poorly planned testing can take up 20 to 50% of your total development effort, in which case it would also account for the single biggest cost in your budget. To ensure that testing is extremely efficient, covering the breadth of today’s mobile ecosystems and device models, the best option is an online cloud-based service.

If you only start thinking about testing a few days before the app hits the market, it’s too late. You’ll need to test a wealth of elements, data and functionality from day one. Here are some things to consider in making testing a part of your development process:

*   **Plan carefully: Automate generic processes as much as possible.** When you’re building a mobile app, a well thought out strategy is critical, a great user experience and design are paramount, and solid development and testing are fundamental. Many aspects of testing can be automated, and this automation will increase the depth and scope of your testing and significantly improve the app’s quality. Ideally, test cases should have full access to the application and test all aspects of it &mdash; memory contents, data tables, file contents and internal program states &mdash; to determine whether the product performs as expected.
*   **Your app will change during development: The same goes for testing.** Many things about your app will change as you’re creating it: the user interface, graphics, functionality, language support, the privacy policy, the use of external resources and much more. Even if [10% of your code changes](https://bitbar.com/strive-for-hermetic-but-never-compromise-integrity-of-app/) or is added to the app, you’ll still need to test 100% of the features. Manual testing can’t keep up with this, so your best option is to build all of your test cases for new features. Then, when a feature is added, all features will be automatically tested. Building your tests to be maintainable over the various development phases of your app is essential.
*   **Choose a testing technology and provider you can grow with.**.  If you already have an app on the market and are looking to create a similar one, then [select a technology](https://www.smashingmagazine.com/2014/01/10/four-ways-to-build-a-mobile-app-part2-native-android/) and vendor that meet your needs. For example, building your test cases according to a certain method or framework will enable you to reuse those test cases for your new application &mdash; at least to some extent. So, choose a technology and vendor that is able to handle your needs as your product scales up and as your testing has to cover new geographical areas and even support new platforms (for example, going from Android to iOS).
*   **Test automation is available 24/7.** Automation will reduce the time it takes to test new features and even the app itself by running 24/7.
*   **Use a cloud-based platform for truly global reach.**.  With an online cloud-based service, you’ll get instant access to [hundreds of real Android devices](https://insights.wired.com/profiles/blogs/the-best-advice-for-app-developers-skip-emulators). Especially with Android, having access to devices that are used in volume holds significant value. Running automated tests on these devices is easy and fast and provides all of the information you’ll need, preprocessed, summarized and in full detail.

What are your thoughts on test automation for mobile? Please let us know in the comments section!

### <span class="rh">Further Reading</span> on SmashingMag:

*   [Prioritizing Devices: Testing And Responsive Web Design](https://www.smashingmagazine.com/2014/07/testing-and-responsive-web-design/)
*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [Applying Participatory Design To Mobile Testing](https://www.smashingmagazine.com/2014/09/applying-participatory-design-to-mobile-testing/)
*   [A Guide To Simple And Painless Mobile User Testing](https://www.smashingmagazine.com/2015/12/simple-and-painless-mobile-user-testing/)

{{< signature "da, ml, al, il" >}}

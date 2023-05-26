---
title: 'Getting Started With Wearables: How To Plan, Build And Design'
slug: getting-started-wearables-plan-build-design
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29578827-cc0b-4b54-a268-3e3d599c458e/01-dicktracy-opt.png
date: 2015-10-13T02:53:32.000Z
author: maximilliano-firtman
description: >-
  If a user of your product is buying a smartwatch tomorrow and your app is not
  compatible with it or your notifications can’t be triggered from there, you
  might frustrate them. If you have a website or an app today, **it’s time to
  start planning support for wearable devices**. In this article, we’ll review
  the platforms available today, what we can do on each of them, how to plan the
  architecture, and how to develop apps or companion services for these new
  devices.

  Do you remember the shoe phone from Get Smart? If you don’t know what I’m
  talking about, you are probably too young (or I’m too old). (You can [Google
  it](https://www.google.lt/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=get%20smart%20shoe%20phone)
  now. Just go; I’ll wait here in this tab.) The shoe phone we saw on TV was
  followed by many other wearable devices on TV, such as the ones on Knight
  Rider, The Flintstones, James Bond and Dick Tracy. Many years later, we can
  say that wearable devices are here and ready to use. We, as designers and
  developers, need to **be ready to develop successful experiences** for them.
categories:
  - Mobile
  - Apps
  - Devices
  - UX
---
If a user of your product is buying a smartwatch tomorrow and your app is not compatible with it or your notifications can’t be triggered from there, you might frustrate them. If you have a website or an app today, <strong>it’s time to start planning support for wearable devices</strong>. In this article, we’ll review the platforms available today, what we can do on each of them, how to plan the architecture, and how to develop apps or companion services for these new devices.

Do you remember the shoe phone from Get Smart? If you don’t know what I’m talking about, you are probably too young (or I’m too old). (You can <a href="https://www.google.lt/webhp?sourceid=chrome-instant&amp;ion=1&amp;espv=2&amp;ie=UTF-8#q=get%20smart%20shoe%20phone">Google it</a> now. Just go; I’ll wait here in this tab.) The shoe phone we saw on TV was followed by many other wearable devices on TV, such as the ones on Knight Rider, The Flintstones, James Bond and Dick Tracy. Many years later, we can say that wearable devices are here and ready to use. We, as designers and developers, need to <strong>be ready to develop successful experiences</strong> for them.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29578827-cc0b-4b54-a268-3e3d599c458e/01-dicktracy-opt.png"><img title="Developing For Wearables" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29578827-cc0b-4b54-a268-3e3d599c458e/01-dicktracy-opt.png" alt="Developing For Wearables" /></a></figure>

In this article, we will cover the most important platforms ready to support our content and services, what we can do on them and where to start in terms of languages, SDKs and emulators.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Designing For Smartwatches And Wearables](https://www.smashingmagazine.com/2015/02/designing-for-smartwatches-wearables/)
*   [Bringing Your App’s Data To Every User’s Wrist With Android Wear](https://www.smashingmagazine.com/2017/01/bringing-app-data-every-user-wrist-android-wear/)
*   [Developing For Apple Watch Without The Device](https://www.smashingmagazine.com/2015/08/mymail-app-case-study/)
*   [Intimate And Interruptive: Designing For The Power Of Apple Watch](https://www.smashingmagazine.com/2015/10/intimate-interruptive-designing-power-apple-watch/)
*   [How We Designed And Built Our First Apple Watch App](https://www.smashingmagazine.com/2015/08/how-we-designed-and-built-our-first-apple-watch-app/)

{{% feature-panel %}}

## Watches And Bands Ready To Support Our App

Among the devices that run apps today, we will focus mostly on <strong>(smart) watches</strong>. Glasses and bands are also available, but their distribution is more limited.

Platform Phone requirement Screen Touch Mic Speaker Vibration Other features
<table class="tablesaw">
<thead></thead>
<tbody>
<tr>
<td>Android Wear</td>
<td>Android 4.2+ or iPhone*</td>
<td>circular or square</td>
<td>x</td>
<td>x</td>
<td></td>
<td>x</td>
<td>heart rate sensor*</td>
</tr>
<tr>
<td>Apple Watch</td>
<td>iPhone</td>
<td>square (32 or 42 mm)</td>
<td>x</td>
<td>x</td>
<td>x</td>
<td>x</td>
<td>heart rate sensor; crown; Force Touch</td>
</tr>
<tr>
<td>Samsung Gear (Tizen)</td>
<td>no phone required (Gear S only); any Android 4.4+ (Gear S2 only); Android Galaxy series</td>
<td>square, rectangular, circular</td>
<td>x</td>
<td>x</td>
<td>x</td>
<td>x</td>
<td>heart rate sensor*; rotating bezel*; camera*</td>
</tr>
<tr>
<td>Pebble</td>
<td>Android, iPhone</td>
<td>rectangular or circular; e-ink (black and white or color)</td>
<td></td>
<td>x* (Pebble Time only)</td>
<td></td>
<td>x</td>
<td>buttons</td>
</tr>
<tr>
<td>Microsoft Band</td>
<td>Android, iPhone, Windows</td>
<td>rectangular, ultra-wide</td>
<td>x</td>
<td>x* (Band 2 only)</td>
<td></td>
<td>x</td>
<td>heart rate sensor; skin temperature; UV Sensor*, Barometer*, Ambient Light*</td>
</tr>
<tr>
<td>Google Glass*</td>
<td>no phone required</td>
<td>transparent projection</td>
<td>x</td>
<td>x</td>
<td>x</td>
<td></td>
<td>eye tracker; camera</td>
</tr>
</tbody>
</table>
<sup>*</sup> Optional, based on model
<sup>**</sup> The Google Glass prototype is <a href="https://plus.google.com/+GoogleGlass/posts/9uiwXY42tvc">discontinued</a>; the next version might be different.

Note: Some providers, <a href="https://dev.fitbit.com">such as Fitbit</a>, offer an API from their cloud, instead of allowing you to connect your app to the device itself. Therefore, a native app on a user’s phone will upload data to the cloud, and your app can access that data from there after gaining the user’s permission.</p>

### Android Wear

Android Wear is a custom version of the popular Android OS for smartwatches only. Several manufacturers are creating Android Wear devices, and more than 15 devices are on the market today, including Motorola 360, Samsung Gear Live, LG G Round, Asus ZenWatch and Sony Smartwatch 3.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9bf81ab-e6be-4e07-befc-07595d79bbf9/02-android-wear-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6c2d7d0-69d2-46b9-b531-dd627375caff/02-android-wear-opt-small.png" alt="Android Wear is a custom version of the popular Android OS for smartwatches only" /></a><figcaption>Android Wear is a custom version of the popular Android OS for smartwatches only. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9bf81ab-e6be-4e07-befc-07595d79bbf9/02-android-wear-opt.png">View large version</a>)</figcaption></figure>

Android Wear is a fully capable OS, but in most situations it works as a phone companion. It connects to the web mainly through the phone’s connection. Some devices now support Wi-Fi networks, so if you are at home or at the office and your phone is out of range, your watch will work anyway, using the cloud to get data from your phone. The OS supports both square and circular screens, and it needs to be paired with an Android 4.2+ phone to work. At the time of writing, limited iOS support is available for a limited set of devices launched after August 2015.</p>

### Apple Watch

A year after Android Wear was released, Apple Watch appeared on the market, selling as many watches in one day as the Android counterpart did in one year, according to <a href="https://intelligence.slice.com/first-apple-watch-data-one-just-isnt-enough/">Slice Intelligence’s market research</a>. Besides having the same initials (AW), both platforms are quite different in terms of what the OS offers to the user.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a68b1fe5-c51b-4e45-9cf6-5997ec04496e/03-applewatch-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e337ddc1-8681-4239-9164-b80005b92428/03-applewatch-opt-small.png" alt="Apple Watch runs watchOS, a simple OS for the watch" /></a><figcaption>Apple Watch runs watchOS, a simple OS for the watch. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a68b1fe5-c51b-4e45-9cf6-5997ec04496e/03-applewatch-opt.png">View large version</a>)</figcaption></figure>

Apple Watch runs <strong>watchOS</strong>, a simple OS for the watch. On watchOS 1.0, apps ran on your phone, and the watch app itself had just a very simple UI module running on it. In watchOS 2.0 — launched with iOS 9 this month — apps runs directly on the smartwatch, with full access to native features.

In terms of hardware, there are more than 40 models, but designers and developers need only care about the two screen sizes: 38 and 42 millimeters. Besides the touchscreen, Apple Watch features a digital crown to scroll and zoom, a heart rate sensor and “Force Touch” (which distinguishes between a normal tap and a tap with pressure).

### Samsung Gear (Tizen-Based)

Gear is a series of smartwatches from Samsung, including Gear 2, Gear S and the recent Gear S2. These watches run Tizen, a relatively new OS from Samsung for mobile devices. There is also Gear Live, which is based on Android Wear and is the black sheep of the family.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fd1f583-0c39-4fda-a28c-acfa08824e83/04-gear-opt.png" alt="Gear is a series of smartwatches from Samsung" /><br>
<figcaption>Gear is a series of smartwatches from Samsung.</figcaption></figure>

Gear 2 features a square screen, Gear S has a larger (and taller) rectangular screen, and Gear S2 sports a round screen with a rotating bezel. Sensors vary by model and detect heart rate, UV, light and much more.

Gear S is <strong>completely autonomous</strong>, with its own 3G cellular connection, and it can be paired with a Galaxy Samsung device, as well as the other models in the family where that pairing process is mandatory. Gear S2 has a Wi-Fi and a 3G version, the latter coming with a GPS chip.

Gear devices usually don’t work with iPhones or with Androids outside of the Galaxy family. The only exception is the latest Gear S2, which works with any Android 4.4+ device.

Note: Samsung has a Gear Fit band that runs not Tizen but a much simpler OS. We can’t create apps for it, so it’s been left out of this article.</p>

### Pebble

The Pebble was one of the first successful smartwatches on the market. It started as a crowdfunded project, and one of its unique features is battery life of nearly a week. To achieve that goal, the Pebble features an <strong>e-ink screen</strong>, black and white in the early models and color in the latest Pebble Time. The latest version, the Pebble Time Round, uses a circular screen and it claims to be the thinnest and lightest smartwatch in the world today.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88357819-cb0f-4ec6-83b1-50a22cc096fc/05-pebble-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9afe7869-6a99-4d0f-8de3-a09cdf98c766/05-pebble-opt-small.png" alt="The Pebble was one of the first successful smartwatches on the market" /></a><figcaption>The Pebble was one of the first successful smartwatches on the market. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88357819-cb0f-4ec6-83b1-50a22cc096fc/05-pebble-opt.png">View large version</a>)</figcaption></figure>

The device is not touchscreen, doesn’t include sensors and is based on old-fashioned buttons. It features three buttons on the side for users to interact with apps. Pebble works when paired with an Android phone or iPhone; when an app is running on the watch, it needs the phone for network communication.

Pebble is the simplest watch on the market, and therein lies its success. It doesn’t include a heart rate monitor or touchscreen.</p>

### Microsoft Band

Microsoft Band is not a watch, but its features are quite similar to one. It includes a lot of sensors that are useful for health and fitness, including ones for heart rate, skin temperature and UV.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/188cbe39-308c-4b82-aa46-d63a5adf1a24/06-band-opt.png" alt="Microsoft Band is not a watch, but its features are quite similar to one" /><br>
<figcaption>Microsoft Band is not a watch, but its features are quite similar to one.</figcaption></figure>

It doesn’t support on-device apps, but Android, iOS and Windows Phone apps can send “tiles” to the device’s tiles, and the information will be shown on the ultrawide screen.</p>

### Google Glass

While this platform is still at an impasse and you can’t buy the initial $1,500 Glass prototype anymore, the platform will resurface as a product for the enterprise market, according to different sources. Clearly, we are not going to see everyone on the street wearing Glass soon, but it will probably be a good solution for work and for some industries.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6bffeffa-1ea4-420f-b40a-222cf968e02d/07-glass-opt.png" alt="Glass can be paired with Android or iOS" /><br>
<figcaption>Glass can be paired with Android or iOS.</figcaption></figure>

The prototype ran Android, and native apps were completely autonomous from the phone, running directly on Glass. The wearable features a projector that emulates a 25-inch screen at 2.5 meters (8 feet) from the user. It supports voice activation and has a multi-touch panel on the side.

Glass can be paired with Android or iOS to get a cellular connection and notifications from apps. In addition, the first Glass prototype featured Wi-Fi connection and standalone apps running on the device.</p>

### Other Platforms

Other platforms for wearables have become available on the market in these last few years. However, because of a lack of users, deprecation of the platform or lack of any public SDK, we will not cover them in this article. These include Samsung Gear Fit, Sony Smartwatches 1 and 2, Garmin smartwatches and NikeFuel.</p>

## What We Can Do For These Devices

We can offer several kind of solutions for wearable devices today:

*   **Standalone apps** run on the device itself. These apps may use the phone to get a network connection or get a connection directly though Wi-Fi.
*   **Companion apps** run primarily on the phone, sending UI commands to the device’s app and receiving interaction from the user. They can also be companions in a game or an app that is being controlled by the user on a phone (or TV)
*   **Faces** for watches feature a custom clock screen, the kind you see when you look at a watch without interacting with it.
*   **Cards or glances** are static views that are available quickly from the home screen and feature updated content from an app.
*   **Rich notifications** add wearable-specific abilities to the push or local notifications that are delivered by a phone app.</p>

### Installation Methods

Apps can be installed on a wearable device in two forms:

*   from a store specifically for the wearable (usually on a companion website);
*   from a smartphone app;
*   not installed at all, in which case a phone app would send the information to the wearable.

The most common method today is through a smartphone app. This means you will need an app in the phone’s store: Google Play, Apple’s App Store or the Microsoft Store. That app would include the wearable app in the package, and a native app in your phone’s OS would install the companion module on the watch. In this case, the watch might install new apps when the phone’s apps are updated, without the user taking explicit action.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea60c006-a71d-4ade-90c7-fc0376188610/08-appstore-opt-small.png" alt="Twitter’s support for Apple Watch is shown in the profile for Twitter’s phone app in the App Store" /><br>
<figcaption>Twitter’s support for Apple Watch is shown in the profile for Twitter’s phone app in the App Store.</figcaption></figure>

### Platform Support

Below is a breakdown of what we can do on each platform and how the installation process works:

PlatformStandalone appsCompanion appsFacesCardsRich notificationsInstallation
<table class="tablesaw">
<thead></thead>
<tbody>
<tr>
<td>Android Wear</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>phone app</td>
</tr>
<tr>
<td>Apple Watch</td>
<td>yes (2.0+)</td>
<td>yes</td>
<td>no*</td>
<td>yes (glances)</td>
<td>yes</td>
<td>phone app</td>
</tr>
<tr>
<td>Samsung Gear (Tizen)</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
<td>yes</td>
<td>store or phone app</td>
</tr>
<tr>
<td>Pebble</td>
<td>yes</td>
<td>yes</td>
<td>yes</td>
<td>no</td>
<td>no</td>
<td>store</td>
</tr>
<tr>
<td>Microsoft Band</td>
<td>no</td>
<td>no</td>
<td>N/A; custom “me tile”</td>
<td>yes, tiles</td>
<td>through web tiles</td>
<td>no installation</td>
</tr>
<tr>
<td>Google Glass</td>
<td>yes</td>
<td>N/A</td>
<td>yes</td>
<td>yes</td>
<td>phone app</td>
<td>store</td>
</tr>
</tbody>
</table>
<sup>*</sup> On watchOS 2.0, we can create “complications,” tiny pieces of information (such as an icon or a number) that the user can insert in one of the preinstalled faces, usually in one of the corners.</p>

## Designing The Wearable Experience

When creating your wearable app, do not just shrink your current phone app into the smaller screen. A wearable app should be created for micro-interactions and for accessing what the user needs exactly when they need it.

Let’s say you are creating an app for a hotel chain. A wearable app might offer the user the following:

*   A standalone app would update the user’s reservations all of the time, even if the phone has no connection or is not in range.
*   A companion app allows the user to search quickly for a hotel tonight or tomorrow in their current city from their watch. If the user wants to do a more complex search, they would probably use the phone. Making a complex wearable app from scratch is not a good idea. On some platforms, we can add advanced search for geek users to prevent frustration, but those options should be hidden from first view.
*   A card could appear automatically the day they need to check in and check out of a hotel.
*   A card could appear automatically when the user’s loyalty points with a hotel are about to expire.
*   A card could appear when the user is in a new city, offering a deal on a hotel for tonight. Be careful, though, not to spam the user’s wrist.
*   Rich notification could add actions to existing push notifications, such as for upgrading, cancelling a reservation or ordering a shuttle from the airport. In our current notifications, we could also provide background images and icons optimized for the wearable device.

A hotel app probably doesn’t need a custom watch face. You could try it, but I don’t think users will want it. For frequent travellers, we could create a complication for watchOS, with updated information about their next reservation.</p>

## Architecture Of A Wearable Solution

### Smartphone Module

Besides Google Glass and Samsung Gear S and S2 for autonomous applications, you will need two native apps in the stores to carry your wearable app (one for Android and one for iPhone).

With your native app on an Android phone, you will be able to support Android Wear, Tizen (only for Galaxy-based devices), Pebble and Microsoft Band users.

With the native app for iPhone, you will be able to support Apple Watch, Pebble and Microsoft Band users. For users of Windows on mobile — formerly Windows Phone — the Microsoft Band is currently the only compatible platform.

While some newer Android Wear watches support iOS, at the time of writing, iOS apps can’t carry Android Wear apps or support rich notifications for this platform.

If you don’t want to create a phone app — for example, if you are creating a game that is suitable only for wearables — you will probably need to <strong>create a container app</strong> anyway. Its only purpose would be to carry, set up and install the watch app and act as its connection to the world. Many developers already have a mobile app for phones, and so the wearable companion would work with it the next time they send an update to the store.

Usually you wouldn’t need to provide low-level communication between the watch and your module in the phone app. The software that manages the connection between the wearable and your phone, such as the Android Wear app, the Apple Watch app, the Pebble app, the Samsung Gear app or the Microsoft Health app, would do that job automatically, providing a public API that can be consumed from your native app in Java, Objective-C, Swift or .NET.</p>

### User Interface and Controls

I don’t need to explain that we are working with a very tiny screen here. Therefore, <strong>micro-layouts</strong> are the only solution to a successful wearable app. Be as short as possible, reduce every bit of text, and don’t just minify your mobile screen. Brainstorm and start from scratch with your wearable screens.

All platforms have <strong>a few common UI elements</strong>: labels (static text controls), buttons (no more than two in a row), progress indicators and scrollable lists. Design your UI with just these elements. Some platforms also help users pick dates and times and input text through dictation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8d057b5-17b9-45bd-8714-aea7d0bbe638/09-bezel-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f2d42b6-82f1-47ed-b6c4-4e4c6c3bf9ad/09-bezel-opt-small.png" alt="Gear's rotating bezel selection allows for some interesting UX experiences" /></a><figcaption>Gear's rotating bezel selection allows for some interesting UX experiences. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8d057b5-17b9-45bd-8714-aea7d0bbe638/09-bezel-opt.png">View large version</a>)</figcaption></figure>

The Gear S2 watch supports a rotating bezel selection, which allows for some interesting UX experiences. On Apple Watch, the digital crown is available for apps in watchOS 2.0, and it can be used for scrolling through a native list.</p>

### Screen Navigation

Navigation between screens is usually done in one of two ways.</p>

<strong>Modal or push screens</strong> appear after the user selects an item from a list or clicks a button. All platforms provide, through physical buttons or gestures, an automatic way to go back to the previous screen, so do not implement your own navigation for that.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0abac1-bb98-4ce5-96da-a41673565a43/10-watch3-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0fbe7e0f-ecd8-4edc-b809-2b6df969eadf/10-watch3-opt-small.png" alt="Example for modal or push screens" /></a><figcaption>Example for modal or push screens. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d0abac1-bb98-4ce5-96da-a41673565a43/10-watch3-opt.png">View large version</a>)</figcaption></figure>

<strong>Pages</strong> let you show different sections of information or sections similar to a tab navigator on a phone. To change pages, the user swipes left or right using their finger.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4310313-7e74-4036-ad8d-eb04e266f741/11-watch4-opt.png" alt="Example for Pages" /><br>
<figcaption>Example for Pages.</figcaption></figure>

### Screen and Images

Background images and animations are welcome on some platforms (such as Android Wear and Apple Watch). When working with images and set of images, we have two possibilities:

1.  static images that are already available in the wearable memory,
2.  images coming from the phone (or network) through Bluetooth.

The first option is ideal for <strong>performance</strong> because in some cases, as with Apple Watch, animations are done through a series of images in sequence (like an animated GIF).

In terms of screen size, we have to deal primarily with square and circular screens (which is a challenge in itself), while some devices have rectangular screens. We still have to prepare our assets for different screen densities, as we do with smartphones, but there is not much fragmentation in the field today, fortunately. But that will certainly change in future.

The following table shows the current screen sizes available on each platform:
PlatformScreen sizes
<table class="tablesaw">
<thead></thead>
<tbody>
<tr>
<td>Android Wear</td>
<td>320 × 320, square
320 × 290, round
360 × 360, round</td>
</tr>
<tr>
<td>Apple Watch</td>
<td>272 × 240, 38 mm
312 × 390, 42 mm</td>
</tr>
<tr>
<td>Samsung Gear (Tizen)</td>
<td>320 × 320, square (Gear 2)
360 × 480, rectangular (Gear S)
360 × 360, round (Gear S2)</td>
</tr>
<tr>
<td>Pebble</td>
<td>144 × 168, (black and white or 65 colors)
180 x 180, round (65 colors, Time Round)</td>
</tr>
<tr>
<td>Microsoft Band</td>
<td>320 × 106
320 x 128 (Band 2)</td>
</tr>
<tr>
<td>Google Glass*</td>
<td>640 × 360</td>
</tr>
</tbody>
</table>

### Push Notifications

Notifications are a key part of any wearable app. Notifications are usually sent from the app developer’s server to Apple, Google or Microsoft, which in turn sends the notification to the user’s phone. By default, your watch app takes those notifications and shows them to the user on their wearable.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ddaf12d-e3c6-4daa-9d0b-6e5ab594b280/12-notifications-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/150bfbc2-73f6-42eb-bc15-1e2006a72704/12-notifications-opt-small.png" alt="Notifications" /></a><figcaption>Notifications are usually sent from the app developer’s server to Apple, Google or Microsoft, which in turn sends the notification to the user’s phone. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ddaf12d-e3c6-4daa-9d0b-6e5ab594b280/12-notifications-opt.png">View large version</a>)</figcaption></figure>

Even if you haven’t created an app for wearable devices, your app already works with them if you are sending push notifications. In most situations, you will probably want to optimize those notifications for the form factor.

With Android Wear, you can set up a content provider that gets triggered when a notification is received from the server. On iPhone, you can set a custom interface to decide how notifications will be shown on Apple Watch.

Note: iOS’ Mail application shows a summary of incoming email on Apple Watch. If you want to customize the HTML that users see for email on the watch, Mail <a href="https://litmus.com/blog/how-to-send-hidden-version-email-apple-watch">supports an undocumented MIME type</a> that you can use in your multipart sending: <strong>text/watch-html</strong>.</p>

### Voice Commands

Some wearable devices have voice-recognition software that we can use in our apps when we need some kind of input from the user or as a trigger to open an app from the system.

With <strong>Android Wear</strong>, the user can browse apps by touching the screen or by saying “OK Google, start [name of app].” An app can also register an instruction to the system (such as “Take a note”) or a custom action through any string of words (such as “Book a room”). Android Wear also takes advantage of voice recognition through an “intent,” which returns the recognized text.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05ad5072-6981-4110-b88a-df6bea53c7c8/13-wear1-opt.png" alt="With Android Wear, the user can browse apps by voice recognition" /><br>
<figcaption>With Android Wear, the user can browse apps by voice recognition.</figcaption></figure>

On <strong>Apple Watch</strong>, the user can open an app from the visual cloud of apps, which can be zoomed in and out of with the crown and panned with the finger. The user can also ask Siri to open an app by name by pressing and holding the digital crown or by saying, “Hey Siri, open [name of app].” An app can also take advantage of Siri’s voice-recognition and dictation mode through a text-input field.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fe74453-ea80-4d19-9541-e64b2d8698cb/14-watch2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cebf89ee-b93c-4576-ba2f-2f860d537c76/14-watch2-opt-small.png" alt="On Apple Watch, the user can open an app from the visual cloud or ask Siri" /></a><figcaption>On Apple Watch, the user can open an app from the visual cloud or ask Siri. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3fe74453-ea80-4d19-9541-e64b2d8698cb/14-watch2-opt.png">View large version</a>)</figcaption></figure>

On <strong>Google Glass</strong>, we have access to dictation mode through an intent, which returns the recognized text. An app developer can also add an entry in the “OK Glass” voice menu (similar to Android Wear).

On <strong>Tizen</strong>, the user can open an app from the clock screen by saying, “Hi Gear, open [name of app].” You can use the Web Speech JavaScript API to get input from the user within your app.

Latest versions of Pebble and Microsoft Band have microphones for replying notifications. The Microsoft Band 2 also uses the mic for accessing Cortana assistant.

Remember that, even with devices that have a microphone, the user might not want to talk to their device like Dick Tracy in certain social situations. Therefore, always provide an alternative, such as a list of options to choose from.</p>

### Contextual Services and Content

The most successful wearable apps are the ones that provide the right information at the right time. To achieve this, the phone’s host app, in conjunction with the developer’s server, must be sensitive to the context of the user by providing rich notifications and updating cards (known as glances on Apple Watch and live tiles on Microsoft Band) so that they’re ready when the user tries to access them.

These contextual services prepare all of the meta data for when the user activates the app from a notification or card. For example, on an airline card, if the user’s flight is departing in 30 minutes, they should see information about their gate, and if they open the notification or activate the app from the card or glance screen, the app should show relevant information about the flight and not the generic home screen.

Google Now on Android Wear is one of the most interesting apps using contextual services:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/558184c0-02e5-4b79-8c49-6fef0c80c1ce/15-googlenow-opt.png" alt="Google Now uses contextual services" /><br>
<figcaption>Google Now uses contextual services.</figcaption></figure>

Both iOS and Android support <strong>geofencing</strong> on phones, so you can be notified when a user enters or exists a city or geographic boundary (such as an airport). When a notification comes from the OS, your app will verify the context and see whether it would be opportune to update a card or send a notification to the wearable device.

Other input data that is used in successful contextual wearable apps comes from sensors (such as for heart rate), beacons in range, roaming status and the accelerometer. For example, the Health app in Apple Watch use the wearer’s heart rate and the accelerometer to collect information about their daily activity.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3daaca6-5f02-4f34-a846-ad4f14561ebf/16-watch1-opt.png" alt="The Health app in Apple Watch use the wearer’s heart rate and the accelerometer to collect information about their daily activity" /><br>
<figcaption>The Health app in Apple Watch use the wearer’s heart rate and the accelerometer to collect information about their daily activity.</figcaption></figure>

## What Do You Need To Start?

Let’s say you are ready to create your app. What do you need? First, you will probably need the same official SDKs that you used to create your native apps for Android, iPhone and Windows. Remember that most wearable apps piggyback on native phone app.

If you are working on an unofficial development platform, verify whether it supports wearables. <a href="https://www.xamarin.com">Xamarin</a>, for example, currently supports smartwatch development.

If you are working with a hybrid approach, such as Apache Cordova or PhoneGap, I have bad news for you: <strong>Most wearable platforms don’t support webviews</strong>, so there is no way to use these tools. The only exceptions are Google Glass and Samsung’s Tizen, most of whose apps are basically HTML and JavaScript.

Let’s summarize the languages and platforms for wearable apps, before getting into the details of each platform:

PlatformLanguageRecommended IDEHost platform for companion app
<table class="tablesaw">
<thead></thead>
<tbody>
<tr>
<td style="font-weight: bold">Android Wear</td>
<td>Java or C++</td>
<td>Android Studio</td>
<td>Java</td>
</tr>
<tr>
<td style="font-weight: bold">Apple Watch</td>
<td>Objective-C or Swift</td>
<td>Xcode (Mac-only)</td>
<td>Objective-C or Swift</td>
</tr>
<tr>
<td style="font-weight: bold">Google Glass</td>
<td>Java or cloud-based</td>
<td>Android Studio</td>
<td>N/A</td>
</tr>
<tr>
<td style="font-weight: bold">Samsung Gear (Tizen)</td>
<td>HTML5 and JavaScript; C or C++ or EFL (for Gear S2 only)</td>
<td>Tizen SDK for wearables</td>
<td>Java for Android (with accessory SDK)</td>
</tr>
<tr>
<td style="font-weight: bold">Pebble</td>
<td>C or JavaScript</td>
<td>Pebble SDK or CloudPebble</td>
<td>Java for Android; Objective-C for iOS</td>
</tr>
<tr>
<td style="font-weight: bold">Microsoft Band</td>
<td>N/A for apps; HTML for web tiles</td>
<td>N/A</td>
<td>Java for Android; Objective-C for iOS; .NET for Windows</td>
</tr>
</tbody>
</table>

### Android Wear

For your Android app, you will need latest version of <a href="https://developer.android.com/tools/studio">Android Studio</a>, and then you would create an app with Android Wear support or just add a module to your current app (see the following image). This means that your Wear app will use the same layout XMLs and Java framework that you are used to from Android. The number of widgets you can use is limited (for example, no webview can be used), and some other UI elements are available only for wearables.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e0611c1-f5d4-42be-ae1e-46207430e218/17-android-studio-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c84ec54c-e114-4b38-862e-72748eee4e56/17-android-studio-opt-small.png" alt="For your Android app, you will need latest version of Android Studio" /></a><figcaption>For your Android app, you will need latest version of Android Studio. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e0611c1-f5d4-42be-ae1e-46207430e218/17-android-studio-opt.png">View large version</a>)</figcaption></figure>

From Android Studio and the latest version of the SDK, you can create an emulator for Wear (both round and square screens). More importantly, you can bind it to a real Android device through the Android Wear app as if it were a real smartwatch. <a href="https://developer.android.com/training/wearables/apps/creating.html">Instructions on doing this</a> are available in the documentation.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baab2575-558c-4bc3-9784-496dcda1811f/18-android-sdk-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa3c2607-9ccc-4356-9bb4-2b4056b8d8cb/18-android-sdk-opt-small.png" alt="You can create an emulator for Wear and bind it to a real Android device" /></a><figcaption>You can create an emulator for Wear and bind it to a real Android device. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/baab2575-558c-4bc3-9784-496dcda1811f/18-android-sdk-opt.png">View large version</a>)</figcaption></figure>

Your Android Wear app will be compiled, packaged and inserted in your mobile phone app. Through some meta data in your <code>AndroidManifest.xml</code> file, the Android Wear app on a user’s phone will detect the new app and install it on their watch.

Remember that Android Wear supports rich notifications, too. So, we don’t need to create an Android Wear app; we just need to use the Wear SDK to enhance our notifications.</p>

### Apple Watch

Apps are developed for Apple’s watchOS 1.0 using WatchKit, an extension of the current iOS development framework. A WatchKit app is just a set of UI resources that are bound to an extension in your iPhone app. The extension is hosted in the iPhone app with the real phone’s app.

You will need the latest version of Xcode tools (and a Mac computer for it). From there, you can add a WatchKit target to any iPhone application (see the next figure). The app will travel with the iPhone app and will be installed automatically in a user’s Apple Watch if one is present.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b6f018f-0596-445e-8dbc-89489e0d1849/19-xcode1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3952f34-d00a-41a3-899e-a9449dc4a6bd/19-xcode1-opt-small.png" alt="Apps for Apple’s watchOS 1.0 are developed using WatchKit" /></a><figcaption>Apps for Apple’s watchOS 1.0 are developed using WatchKit. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b6f018f-0596-445e-8dbc-89489e0d1849/19-xcode1-opt.png">View large version</a>)</figcaption></figure>

To help with iOS development, the WatchKit app includes a storyboard with every screen of your app, and those elements are bound to the controller living in the extension. You can use either Objective-C or Swift to develop your extension, and for the storyboard, you are not using the same controls available in UIKit, but rather a very limited suite of controls available in WatchKit.

WatchOS 2.0 includes native app support that can be executed without interaction with the phone, even using Wi-Fi to access the network when the phone is out of reach. We can create watchOS-native apps using Xcode 7 and with the watch simulator in Xcode (see the next figure).</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af15f6fa-cde4-41a0-9094-cda28c6f50ac/20-xcode2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54b3a20f-96c2-43a3-828c-01d9c3909960/20-xcode2-opt-small.png" alt="We can create watchOS-native apps using Xcode 7 and with the watch simulator in Xcode" /></a><figcaption>We can create watchOS-native apps using Xcode 7 and with the watch simulator in Xcode. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af15f6fa-cde4-41a0-9094-cda28c6f50ac/20-xcode2-opt.png">View large version</a>)</figcaption></figure>

A watch app can also include a glance screen (i.e. updated information that can be accessed quickly from the watch face) and complications. With ClockKit, a new framework on watchOS 2.0, apps can provide data using image and text templates to the watch face, as we see in the next figure.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da39900c-1a37-46ff-80fd-6d168eb1bc12/21-complications-opt.png" alt="Glance screen" /><br>
<figcaption>A watch app can also include a glance screen.</figcaption></figure>

### Tizen Wearable

For Samsung smartwatches with Tizen OS, we would create wearable web apps with HTML5, CSS and JavaScript. The apps will be packaged as a WGT file that can be distributed in the Galaxy Store as a standalone app, or it can piggyback on an Android application as a Gear companion app.

For Gear S2 smartwatches only, you can also create native apps using C, C++ or ETF.

For a Gear companion app, you would use the Samsung Accessory SDK for Android, which lets you create the host portion that will be consumed by the WGT app on the watch.

The <a href="https://developer.tizen.org/downloads/tizen-sdk">Tizen SDK for Wearable</a> is an Eclipse-based IDE that helps you design, develop and test your Tizen app through the Tizen emulator.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e05ca05-1b17-48d8-996f-16eb31f2eca4/22-tizensdk-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/156b7fdb-f83a-4d02-acf8-d0bc3003d7a8/22-tizensdk-opt-small.png" alt="The Tizen SDK for Wearable" /></a><figcaption>The Tizen SDK for Wearable. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e05ca05-1b17-48d8-996f-16eb31f2eca4/22-tizensdk-opt.png">View large version</a>)</figcaption></figure>

Samsung also offers free remote testing of real devices through its website, using a service known as Remote Test Lab. With this service, you can test your app on a real Samsung phone paired with a real Galaxy Gear smartwatch.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af86fcb3-d290-47b3-9aa6-19ce93519c2d/23-samsungrtl-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/798949e9-1316-495c-95e7-d6aab4ede489/23-samsungrtl-opt-small.png" alt="The Samsung Remote Test Lab" /></a><figcaption>The Samsung Remote Test Lab. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af86fcb3-d290-47b3-9aa6-19ce93519c2d/23-samsungrtl-opt.png">View large version</a>)</figcaption></figure>

### Pebble

To create a Pebble app, you would use C or JavaScript (<code>Pebble.js</code>). You can download the SDK for free and start developing and testing your Pebble app in the emulator.

If you are in a hurry, you can even bypass the installation and try the cloud-based IDE, compiler and emulator, which are available on <a href="https://cloudpebble.net/">CloudPebble</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d985d6ce-c9d8-4d3f-9701-8537a29374cb/24-cloudoebble-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67e0b5da-751b-44bc-8ab1-0e61c51cae51/24-cloudoebble-opt-small.png" alt="The CloudPebble" /></a><figcaption>The CloudPebble. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d985d6ce-c9d8-4d3f-9701-8537a29374cb/24-cloudoebble-opt.png">View large version</a>)</figcaption></figure>

Besides the app itself, which must be distributed through the Pebble app store, you will need to use Pebble’s Android or iPhone kit if you want to integrate your phone app with the watch (as a companion app).</p>

### Microsoft Band

Microsoft Band runs apps not on the device itself, but on a phone. Therefore, the SDK is for Android (Java), iPhone (Objective-C and Swift) and Windows (.NET).

Download <a href="https://developer.microsoftband.com/">Microsoft Band’s SDKs</a>, which will allow you to create an app that does the following:

*   customize the “me tile”, which is the initial default view on the start strip of the device,
*   create a tile that opens the app,
*   push updates to tiles through notifications and badges.

An app runs on the phone, and while it sends screens to the user, it also collects information from Band’s sensors.

At the time of writing, <strong>no Microsoft Band emulator</strong> is available, so you’ll need a real device to test your app.

Microsoft Band also supports <a href="https://developer.microsoftband.com/WebTile">web tiles</a>. A web tile is updated from a website through the Health app installed on Android, iOS or Windows. With a web tile, you don’t need to create your own native app to send data to Band. You can populate a web tile from an XML, RSS or JSON file on the web. With some meta data added, your web tile will provide updated information to Band without having to use the SDK. You can create a web tile from the <a href="https://developer.microsoftband.com/WebTile">online authoring tool</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84d313e8-9c3a-4a60-bd5d-afcecae84c73/25-webtile-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d33da373-4c12-41bb-8643-a1f5fb6306d8/25-webtile-opt-small.png" alt="Microsoft Band also supports web tiles" /></a><figcaption>Microsoft Band also supports web tiles. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84d313e8-9c3a-4a60-bd5d-afcecae84c73/25-webtile-opt.png">View large version</a>)</figcaption></figure>

### Google Glass

While we wait for the next version, let’s just summarize how apps for Glass were created for the prototype, now deprecated. Glassware (which is software that runs on Glass) can be created through a cloud-based API, known as the Mirror API, or through Android’s native SDK and the latest version of Android Studio. There is no way to emulate Google Glass, unfortunately.</p>

## Summary

Wearables are here to stay. As a user with more than a year of experience wearing different pre-Android Wear smartwatches, one year of wearing Android Wear and several months of wearing Apple Watch, I know the <strong>frustration</strong> one gets when an app does not offer a wearable add-on or when the app is not ready.

An instance of my frustration today is Whatsapp, which doesn’t allow me to reply to notifications from the watch app. Another is my smart TV’s phone app; I can turn my TV on and off from my phone but not from my watch. If I need to pull up my phone to do something quick that would be perfect for my wrist, then I’ll be frustrated as a user.

If you are offering content and/or a service for mobile users and it would be suitable for quick actions, <strong>start adding wearables support right now</strong>. Don’t frustrate your users.

As with any new form factor, it’s still not clear how users will use them. But remember that adding support for wearables is easy if you start with rich notifications. If you already have a mobile app for iOS or Android, then you just need to add some extensions to it and you are ready to go.

{{< signature "da, ml, al" >}}


---
title: 'How To Design For Android'
slug: designing-for-android
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c4e8b6b7-ddc0-4683-8899-98d1b0e47d79/android-green-illu.jpg
date: 2011-06-30T09:04:38.000Z
author: dan-mckenzie
summary: >-
  In this article, Dan McKenzie helps designers become familiar with what they need to know to get started with Android and to deliver the right assets to the development team. From demystifying Android screen densities, to what Android 3 is about.
description: >-
  Dan McKenzie helps designers become familiar with what they need to know to get started with Android and to deliver the right assets to the development team. From demystifying Android screen densities, to what Android 3 is about.
categories:
  - Coding
  - Design
  - Apps
  - Android
---

For designers, Android is the elephant in the room when it comes to app design. As much as designers would like to think it’s an <a title="iOS" href="https://en.wikipedia.org/wiki/IOS_%28Apple%29" rel="nofollow">iOS</a> world in which all anyones cares about are iPhones, iPads and the App Store, nobody can ignore that Android currently has the <a title="Android market share" href="https://www.pcworld.com/article/226339/android_market_share_growth_accelerating_nielsen_finds.html" rel="nofollow">majority of smartphone market share</a> and that it is being used on everything from tablets to e-readers. In short, the Google Android platform is quickly becoming ubiquitous, and brands are starting to notice.

But let’s face it. Android’s multiple devices and form factors make it feel like designing for it is an uphill battle. And its cryptic <a title="Android Developers" href="https://developer.android.com/guide/practices/ui_guidelines/index.html" rel="nofollow">documentation</a> is hardly a starting point for designing and producing great apps. Surf the Web for resources on Android design and you’ll find little there to guide you.

If all this feels discouraging (and if it’s the reason you’re not designing apps for Android), you’re not alone. Fortunately, Android is beginning to address the issues with multiple devices and screen sizes, and device makers are slowly arriving at standards that will eventually reduce complexity.

{{% feature-panel %}}

This article will help designers become familiar with what they need to know to get started with Android and to deliver the right assets to the development team. The topics we’ll cover are:

*   Demystifying Android screen densities,
*   Learning the fundamentals of Android design via design patterns,
*   Design assets your developer needs,
*   How to get screenshots,
*   What Android 3 is about, and what’s on the horizon.

## Android Smartphones And Display Sizes

When starting any digital design project, understanding the hardware first is a good idea. For iOS apps, that would be the iPhone and iPod Touch. Android, meanwhile, spans dozens of devices and makers. Where to begin?

The old baseline for screens supported for Android smartphone devices was the T-Mobile G1, the first commercially available Android-powered device which has an HVGA screen measuring 320 &times; 480 pixels.

<a title="Video graphics array" href="https://en.wikipedia.org/wiki/Quarter_Video_Graphics_Array#QVGA_.28320.C3.97240.29" rel="nofollow">HVGA</a> stands for “half-size video graphics array” (or half-size VGA) and is the standard display size for today’s smartphones. The iPhone 3GS, 3G and 2G use the same configuration.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/312aba99-409f-4160-815d-26e4352b1fb6/t-mobile-g1.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104536" title="t-mobile-g1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f445ff5b-fc9e-45fb-9042-1320b8bf9a8e/t-mobile-g1-e1307550246584.jpg" alt="Screenshot" width="261" height="480" /></a><figcaption>T-Mobile G1, the first commercially available Android device and the baseline for Android screen specifications.</figcaption></figure>

To keep things simple, Android breaks down physical screen sizes (measured as the screen’s diagonal length from the top-left corner to bottom-right corner) into four general sizes: small, normal, large and xlarge.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7272f58-f574-46ad-bef9-021ce952b52d/screen-sizes.gif" rel="nofollow"><img loading="lazy" decoding="async" class="104537" title="screen-sizes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de2a1a42-f5fa-4dac-b311-47a60ad049fa/two-mobiles.jpg" alt="Screenshot" width="544" height="415" /></a><figcaption>Two common Android screen sizes. (Image from Google I/O 2010)</figcaption></figure>

320 &times; 480 is considered a “normal” screen size by Android. As for “xlarge,” think tablets. However, the <a title="Most popular Android smartphones" href="https://developer.android.com/resources/dashboard/screens.html" rel="nofollow">most popular Android smartphones</a> today have WVGA (i.e. wide VGA) 800+ × 480-pixel HD displays. So, what’s “normal” is quickly changing. For now, we’ll say that most Android smartphones have large screens.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d741f4e-6e65-4cac-8608-e2a1a6c079d4/table.png" rel="nofollow"><img loading="lazy" decoding="async" class="104346" title="table" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d741f4e-6e65-4cac-8608-e2a1a6c079d4/table.png" alt="Screenshot" width="550" height="293" /></a><figcaption>Diagram of various screen configurations available from emulator skins in the Android SDK. (Image: Android Developers website)</figcaption></figure>

The variety of display sizes can be challenging for designers who are trying to create one-size-fits-all layouts. I’ve found the best approach is to design one set of layouts for 320 &times; 533 physical pixels and then introduce custom layouts for the other screen sizes.

While this creates more work for both the designer and developer, the larger physical screen size on bigger devices such as the Motorola Droid and HTC Evo might require changes to the baseline layouts that make better use of the extra real estate.

### What You Need to Know About Screen Densities

Screen sizes are only half the picture! Developers don’t refer to a screen’s resolution, but rather its density. Here’s how Android defines the terms in its <a title="Android Developers Guide" href="https://developer.android.com/guide/practices/screens_support.html" rel="nofollow">Developers Guide</a>:

*   **Resolution**.  The total number of physical pixels on a screen.
*   **Screen density**.  The quantity of pixels within a physical area of the screen, usually referred to as DPI (dots per inch).
*   **Density-independent pixel (DP)**.  This is a virtual pixel unit that you would use when defining a layout’s UI in order to express the layout’s dimensions or position in a density-independent way. The density-independent pixel is equivalent to one physical pixel on a 160 DPI screen, which is the baseline density assumed by the system of a “medium”-density screen. At runtime, the system transparently handles any scaling of the DP units as necessary, based on the actual density of the screen in use. The conversion of DP units to screen pixels is simple: pixels = DP * (DPI / 160). For example, on a 240 DPI screen, 1 DP equals 1.5 physical pixels. Always use DP units when defining your application’s UI to ensure that the UI displays properly on screens with different densities.

It’s a bit confusing, but this is what you need to know: Like screen sizes, Android divides screen densities into four basic densities: ldpi (low), mdpi (medium), hdpi (high), and xhdpi (extra high). This is important because you’ll need to deliver all graphical assets (bitmaps) in sets of different densities. At the very least, you’ll need to deliver mdpi and hdpi sets for any smartphone apps.

What this means is all bitmap graphics need to be scaled up or down from your baseline (320 &times; 533) screen layouts (note: there is also a way for <a href="https://code.google.com/p/svg-android/" rel="nofollow">parsing SVG files</a> that provides a way to scale vector art on different screens sizes and densities without loss of image quality).

The bitmap requirement is similar to preparing graphics for print vs. the Web. If you have any experience with print production, you’ll know that a 72 PPI image will look very pixelated and blurry when scaled up and printed. Instead, you would need to redo the image as a vector image or use a high-resolution photo and then set the file’s resolution at around 300 PPI in order to print it without any loss of image quality. Screen density for Android works similar, except that we’re not changing the file’s resolution, only the image’s size (i.e. standard 72 PPI is fine).

Let’s say you took a bitmap icon measuring 100 &times; 100 pixels from one of the screens of your baseline designs (remember the “baseline” is a layout set at 320 &times; 480). Placing this same 100 × 100 icon on a device with an lDPI screen would make the icon appear big and blurry. Likewise, placing it on a device with an hDPI screen would make it appear too small (due to the device having more dots per inch than the mDPI screen).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20979f48-a020-4d1f-8eab-0fa47cbf1d76/density-test-bad.png" rel="nofollow"><img loading="lazy" decoding="async" class="104538" title="density-test-bad" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20979f48-a020-4d1f-8eab-0fa47cbf1d76/density-test-bad.png" alt="Screenshot" width="550" height="131" /></a><figcaption>An application without density support. (Image: Android Developers website)</figcaption></figure>

To adjust for the different device screen densities, we need to follow a 3:4:6:8 scaling ratio between the four density sizes. (For the iPhone, it’s easy: it’s just a 2:1 ratio between the iPhone 4 and 3GS.) Using our ratios and some simple math, we can create four different versions of our bitmap to hand off to our developer for production:

*   75 &times; 75 for low-density screens (i.e. &times;0.75);
*   100 &times; 100 for medium-density screens (our baseline);
*   150 &times; 150 for high-density screens (&times;1.5);
*   200 &times; 200 for extra high-density screens (&times;2.0). (We’re concerned with only lDPI, mDPI and hDPI for Android smartphone apps.)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2524b726-28d4-41b9-ae66-45900bbee4aa/icon-sizes.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104336" title="icon-sizes" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2524b726-28d4-41b9-ae66-45900bbee4aa/icon-sizes.jpg" alt="Screenshot" width="550" height="274" /></a><figcaption>The final graphic assets would appear like this using the four different screen densities.</figcaption></figure>

After you’ve produced all of your graphics, you could organize your graphics library as follows:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bf32cf6-4365-4266-b6eb-2aaf3b00b357/folders.gif" rel="nofollow"><img loading="lazy" decoding="async" class="104334" title="folders" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bf32cf6-4365-4266-b6eb-2aaf3b00b357/folders.gif" alt="Screenshot" width="234" height="399" /></a><figcaption>The suggested organization and labeling of asset folders and files. In preparing our star graphic, all file prefixes could be preceded by the name *ic_star*, without changing the names of the respective densities.</figcaption></figure>

You might be confused about what PPI (pixels per inch) to set your deliverables at. Just leave them at the standard 72 PPI, and scale the images accordingly.

## Using Android Design Patterns

Clients often ask whether they can use their iPhone app design for Android. If you’re looking for shortcuts, building an app for mobile Web browsers using something like <a title="WebKit" href="https://en.wikipedia.org/wiki/WebKit" rel="nofollow">Webkit</a> and HTML5 is perhaps a better choice. But to produce a native Android app, the answer is no. Why? Because Android’s UI conventions are different from iPhone’s.

The big difference is the “Back” key, for navigating to previous pages. The Back key on Android devices is fixed and always available to the user, regardless of the app. It’s either a physical part of the device or digitally fixed to the bottom of the screen, independent of any app, as in the recently released Android 3.0 for tablets (more on this later).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48d30192-7244-47c7-928d-8ddb21925736/back-key.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="105807" title="back-key" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48d30192-7244-47c7-928d-8ddb21925736/back-key.jpg" alt="Screenshot" width="235" height="374" /></a><figcaption>The hard “Back” key on a smartphone running Android 2.0.</figcaption></figure>

The presence of a Back key outside of the app itself leaves space for other elements at the top of the screen, such as a logo, title or menu. While this navigational convention differs greatly from that of iOS, there are still other differentiators that Android calls “design patterns.” According to Android, a design pattern is a “general solution to a recurring problem.” Below are the main Android design patterns that were introduced with version 2.0.

{{% ad-panel-leaderboard %}}

### Dashboard

This pattern solves the problem of having to navigate to several layers within an app. It provides a launch pad solution for rich apps such as Facebook, LinkedIn and Evernote.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81219cc6-847d-49b1-a2f0-58d3ff2d8d15/pattern-dashboard.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104339" title="pattern-dashboard" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81219cc6-847d-49b1-a2f0-58d3ff2d8d15/pattern-dashboard.jpg" alt="Screenshot" width="471" height="392" /></a><figcaption>The dashboard design pattern, as used by Facebook and LinkedIn.</figcaption></figure>

### Action Bar

The action bar is one of Android’s most important design patterns and differentiators. It works very similar to a conventional website’s banner, with the logo or title typically on the left and the navigation items on the right. The action bar’s design is flexible and allows for hovering menus and expanding search boxes. It’s generally used as a global feature rather than a contextual one.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e882ddd-2156-4dac-8225-a5a25ae5e46e/pattern-action-bar.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104539" title="pattern-action-bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e882ddd-2156-4dac-8225-a5a25ae5e46e/pattern-action-bar.jpg" alt="Screenshot" width="471" height="392" /></a><figcaption>The action bar design pattern as used by Twitter.</figcaption></figure>

### Search Bar

This gives the user a simple way to search by category, and it provides search suggestions.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e3f1672-9413-4d0c-94e3-5464f9282294/pattern-search-bar.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104341" title="pattern-search-bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e3f1672-9413-4d0c-94e3-5464f9282294/pattern-search-bar.jpg" alt="Screenshot" width="471" height="392" /></a><figcaption>The search bar design pattern as used in the Google Search app.</figcaption></figure>

### Quick Actions

This design pattern is similar to iOS’ pop-up behavior that gives the user additional contextual actions. For example, tapping a photo in an app might trigger a quick action bar that allows the user to share the photo.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/612b627c-4f7c-48d0-b446-d7dc2d8698c0/pattern-quick-actions.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104340" title="pattern-quick-actions" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/612b627c-4f7c-48d0-b446-d7dc2d8698c0/pattern-quick-actions.jpg" alt="Screenshot" width="471" height="392" /></a><figcaption>The quick action design pattern as used by Twitter.</figcaption></figure>

### Companion Widget

<a title="Widgets" href="https://www.businessinsider.com/best-android-widgets-2011-4" rel="nofollow">Widgets</a> allow an app to display notifications on the user’s launch screen. Unlike push notifications in iOS, which behave as temporary modal dialogs, companion widgets remain on the launch screen. (Tip: to select a widget for your Android device, simply tap and hold any empty space on one of the launch screens.)

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ce8a93a-6217-433f-815e-49c07998e726/pattern-widgets.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104342" title="pattern-widgets" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ce8a93a-6217-433f-815e-49c07998e726/pattern-widgets.jpg" alt="Screenshot" width="471" height="392" /></a><figcaption>Companion widgets by Engadget, New York Times and Pandora.</figcaption></figure>

Using established design patterns is important for keeping the experience intuitive and familiar for your users. Users don’t want an iPhone experience on their Android device any more than a Mac user wants a Microsoft experience in their Mac OS environment. Understanding design patterns is the first step to learning to speak Android and designing an optimal experience for its users. Your developers will also thank you!

## Android Design Deliverables

OK, so you’ve designed your Android app and are ready to make it a reality. What do you need to hand off to the developer? Here’s a quick list of deliverables:

1.  Annotated wireframes of the user experience based on the baseline large screen size of 320 &times; 533 physical pixels. Include any additional screens for instances where a larger or smaller (320 &times; 480) screen size requires a modified layout or a landscape version is required.
2.  Visual design mockups of key screens for WVGA large size (320 x 533) screens (based on a WVGA 800 &times; 480 hdpi physical pixel screen size) in addition to any custom layouts needed for other screen sizes.
3.  Specifications for spacing, [font](https://www.droidfonts.com/home/androidsdk/) sizes and colors, and an indication of any bitmaps.
4.  A graphics library with lDPI, mDPI and hDPI versions of all bitmaps saved as transparent PNG files.
5.  Density-specific app icons, including the app’s launch icon, as transparent PNG files. Android already provides excellent [tips for designers](https://developer.android.com/guide/practices/ui_guidelines/icon_design.html "Tips for designers") on this topic, along with some downloads, including graphic PSD templates and other goodies.

## How To Take Screenshots

Your product manager has just asked for screenshots of the developer’s build. The developer is busy and can’t get them to you until tomorrow. What do you do?! As of this writing, Android has no built-in way to take screenshots (bummer, I know). The only way is to just deal with it, and that means pretending to be a developer for a while and downloading some really scary software. Let’s get started!

The following software must be downloaded:

1.  All USB drivers for your Android device,
2.  [Android software development kit](https://developer.android.com/sdk/index.html "Android SDK") (SDK),
3.  [Java SE SDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html "Java SE SDK")

Then, on your computer:

1.  Extract the USB drivers to a folder on your desktop,
2.  Extract the Android SDK to a folder on your desktop,
3.  Install the Java SE SDK.

On your Android device:

1.  Open “Settings” (you’ll find it in the apps menu),
2.  Tap on “Applications,”
3.  Tap on “Development,”
4.  Check the box for “USB debugging.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0791f4b6-eabb-420e-a19e-01159aa52e1b/settings.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104344" title="settings" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0791f4b6-eabb-420e-a19e-01159aa52e1b/settings.jpg" alt="Screenshot" width="471" height="392" /></a></figure>

Now, for the fun part:

1.  Connect your Android device to your computer via USB. Windows users: allow Windows to install all drivers. One of the drivers may not be found and will require you to go to the Window’s Device Manager under the Control Panel. There, you can locate the device (having a yellow warning icon next to it) and right-click on it.
2.  Choose to “update/install” the driver for your device.
3.  Go to your desktop. Open the Android SDK folder and select *SDK Setup.exe*.
4.  Allow it to automatically refresh its list of the operating system SDKs that are available, and select to install all packages.
5.  Once finished, exit the application.
6.  Go back to the opened Android SDK folder on your desktop, and open the “Tools” folder.
7.  Click on the file *ddms* to open the Dalvik Debug Monitor.
8.  Select your device from the “Name” pane.
9.  In the application’s top menu, open the “Device” menu, and choose “Screen capture…” A Device Screen Capture window will open, and you should see the launch screen of your Android device.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8e229f6-acaa-4914-a596-75e6089bc9f5/dalvik-screen.png" rel="nofollow"><img loading="lazy" decoding="async" class="104540" title="dalvik-screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8e229f6-acaa-4914-a596-75e6089bc9f5/dalvik-screen.png" alt="Screenshot" width="550" height="395" /></a><figcaption>The Dalvik Debut Monitor.</figcaption></figure>

To navigate:

1.  Grab your Android device and navigate to any page. Go back to your computer and select “Refresh” in the Device Screen Capture window. The current screen from your Android device should appear.
2.  If you’re on a Mac, you can just do the old Shift + Command + 4 trick to take a screenshot. In Windows, you can copy and paste it into one of the Windows media applications.

## About Android Tablets

At CES 2011, <a href="https://www.engadget.com/features/tablets-at-ces-2011/" rel="nofollow">companies rained down Android tablets</a>, with an array of screen sizes. However, after a quick review of the <a href="https://reviews.cnet.com/best-tablets/best-5-android-tablets" rel="nofollow">most popular ones</a>, we can conclude that the two important screen sizes to focus on in terms of physical pixels are 1280 &times; 800 and 800 &times; 480.

With the Android 3.0 Honeycomb release, Google provided device makers with an Android UI made for tablets. Gone is the hard “Back” button, replaced by an anchored software-generated navigation and system status bar at the bottom of the screen.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a09985e2-df56-4765-a0d8-c4f8496f2925/system-bar.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104345" title="system-bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a09985e2-df56-4765-a0d8-c4f8496f2925/system-bar.jpg" alt="Screenshot" width="550" height="384" /></a><figcaption>The anchored navigation and system bar in Android 3.0.</figcaption></figure>

Android 3.0 got a visual refresh, while incorporating all of the design patterns introduced in Android 2.0. One of the major differences with 3.0 is the Action Bar which has been updated to include tabs, drop-down menus or breadcrumbs. The action bar can also change its appearance to show contextual actions when the user selects single or multiple elements on a screen.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154370f6-ede3-4b0f-af55-f560c7415c9f/new-action-bar.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104337" title="new-action-bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/154370f6-ede3-4b0f-af55-f560c7415c9f/new-action-bar.jpg" alt="Screenshot" width="550" height="343" /></a><figcaption>The new action bar with tabs, introduced in Android 3.0.</figcaption></figure>

Another new feature added to the Android framework with 3.0 is a mechanism called “<a title="Fragments" href="https://android-developers.blogspot.com/2011/02/android-30-fragments-api.html" rel="nofollow">fragments</a>.” A fragment is a self-contained component in a layout that can change size and position depending on the screen’s orientation and size. This further addresses the problem of designing for multiple form factors by giving designers and developers a way to make their screen layout components elastic and stackable, depending on the screen limitations of the app. Screen components can be stretched, stacked, expanded and collapsed, and revealed and hidden.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e824715-15ab-4873-9cd3-99fd9b67c93c/fragments.gif" rel="nofollow"><img loading="lazy" decoding="async" class="104541" title="fragments" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e8a393b-ed9b-42a0-b3b6-ed6c8beee6ca/diagrams-green.jpg" alt="Screenshot" width="365" height="303" /></a><figcaption>Diagram showing examples of how fragments can be used.</figcaption></figure>

The next Android release, scrumptiously dubbed <a title="Android Ice Cream Sandwich" href="https://gizmodo.com/5800358/what-is-androids-ice-cream-sandwich" rel="nofollow">Ice Cream Sandwich</a>, promises to bring this functionality to Android smartphones as well, giving designers and developers the option to build an app using a one-size-fits-all strategy. This could be a paradigm shift for designers and developers, who will need to learn to think of app design in terms of puzzle pieces that can be stretched, stacked, expanded or hidden to fit the form factor. In short, this will allow one Android OS to run anywhere (with infinite possibilities!).

### A Word Of Advice

Do get your hands on an Android phone and tablet, and spend some time downloading apps and exploring their interfaces. In order to design for Android, you have to immerse yourself in the environment and know it intimately. This might sound obvious, but it’s always surprising to hear when even the product manager doesn’t have an Android device.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e07d8d3-df07-44ab-ba73-57e90abc0266/android-ice-cream-sandwich.jpg" rel="nofollow"><img loading="lazy" decoding="async" class="104332" title="android-ice-cream-sandwich" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e07d8d3-df07-44ab-ba73-57e90abc0266/android-ice-cream-sandwich.jpg" alt="Screenshot" width="400" height="305" /></a></figure>

## Online Resources

Here are some links to online resources I’ve found especially useful:

### Presentations

*   [Android Design Patterns](https://docs.google.com/fileview?id=0B9Lrx2XbHPV6NTBiYTA5OGMtYmEwNi00Yzc3LWIxNWUtZWYwZGZlZGViZWMz&hl=zh_CN "Android Design Patterns")
*   [Android User Interface Design Tips](https://www.slideshare.net/AndroidDev/android-ui-design-tips "Android User Interface Design Tips")

### Videos

*   [Designing and Implementing Android UIs for Phones and Tablets](https://youtube.com/watch?v=WGIU2JX1U5Y&feature=player_embedded#at=3469 "Designing and Implementing Android UIs for Phones and Tablets") (Google I/O 2011)

### Android Developers

*   [Supporting Multiple Screens](https://developer.android.com/guide/practices/screens_support.html "Supporting Multiple Screens")

### Other

*   [Android App Developers GUI Kits, Icons, Fonts and Tools](https://speckyboy.com/2010/05/10/android-app-developers-gui-kits-icons-fonts-and-tools/)

{{% ad-panel-leaderboard %}}

### Further Reading

*   [What Every App Developer Should Know About Android](https://www.smashingmagazine.com/2014/10/what-every-app-developer-should-know-about-android/)
*   [Designing For A Maturing Android](https://www.smashingmagazine.com/2013/05/brave-new-world-designing-for-a-maturing-android/)
*   [Mobile Design Practices For Android: Tips And Techniques](https://www.smashingmagazine.com/2012/07/android-design-tips/)
*   [Get Started Developing for Android with Eclipse](https://www.smashingmagazine.com/2010/10/get-started-developing-for-android-with-eclipse/)

{{< signature "al, il, kw, mrn" >}}

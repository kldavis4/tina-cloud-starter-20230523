---
title: 'How To Design For Android Tablets'
slug: designing-for-android-tablets
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d37a985d-e9a0-4d65-b724-e5833608dceb/image-13.jpg
date: 2011-08-09T13:13:17.000Z
author: dan-mckenzie
summary: >-
  In this post, Dan McKenzie helps designers become familiar with Android tablet app design by understanding the differences between the iPad iOS user interface and Android 3.x “Honeycomb” UI conventions and elements. Also, have a look at Honeycomb design patterns and layout strategies, and then review some of the best Android tablet apps out there.
description: >-
  This article helps designers become familiar with Android tablet app design by understanding the differences between the iPad iOS user interface and Android 3.x “Honeycomb” UI conventions and elements. 
categories:
  - Mobile
  - Tablets
  - Responsive Design
  - Android
---

More than ever, designers are being asked to create experiences for a variety of mobile devices. As tablet adoption increases and we move into the post-PC world, companies will compete for users’ attention with the quality of their experience. Designing successful apps for Android tablets requires not only a great concept that will encourage downloads, usage and retention, but also an experience that Android users will find intuitive and native to the environment.

The following will help designers become familiar with Android tablet app design by understanding the differences between the iPad iOS user interface and Android 3.x “Honeycomb” UI conventions and elements. We will also look at Honeycomb design patterns and layout strategies, and then review some of the best Android tablet apps out there.

{{% feature-panel %}}

Note that while Android 2.x apps for smartphones can run on tablets, Android 3.0 Honeycomb was designed and launched specifically for tablets. <a href="https://gizmodo.com/5800358/what-is-androids-ice-cream-sandwich">Future updates</a> promise to bring Honeycomb features to smartphone devices, as well as make it easier to design and build for multiple screen types.

For most of us, our first exposure to tablets was via the iPad. For this reason, it’s reasonable to begin comparing the two user interfaces. By comparing, we can align what we’ve learned about tablets and begin to focus on the key differences between the two, so that we can meet the unique UI needs of Android users. Not only will this help us get up to speed, but it becomes especially important when designing an Android tablet app from an existing iPad one.

## It’s Just Like The iPad, Right?

While the Android tablet and iPad experience share many similarities (touch gestures, app launch icons, modals, etc.), designers should be aware of the many differences before making assumptions and drawing up screens.

### Screen Size And Orientation

The biggest difference between the two platforms is the form factor. Layouts for the iPad are measured at 768 × 1024 physical pixels, and the iPad uses portrait mode as its default viewing orientation.

With Android tablets, it’s a bit more complicated, due to the multiple device makers. In general, there are 7- and 10-inch Android tablets screen sizes (measured diagonally from the top-left corner to the bottom-right), with sizes in between. However, most tablets are around 10 inches.

What does this mean in pixels? A good baseline for your layouts is 1280 &times; 752 pixels (excluding the system bar), based on a 10-inch screen size and using landscape (not portrait) as the default orientation. Like on the iPad, content on Android tablets can be viewed in both landscape or portrait view, but landscape mode is usually preferred.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee762225-3745-48da-9668-27590deaf1ac/image-1.jpg"><img loading="lazy" decoding="async" class="110063" title="image_1" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ee762225-3745-48da-9668-27590deaf1ac/image-1.jpg" alt="" width="550" height="306" /></a><figcaption>The portrait view on a typical 10-inch Android tablet (left) and on the iPad (right).</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5de0c82f-4270-494b-9fd9-a8fc1a45e976/image-2.jpg"><img loading="lazy" decoding="async" class="110064" title="image_2" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5de0c82f-4270-494b-9fd9-a8fc1a45e976/image-2.jpg" alt="" width="550" height="202" /></a><figcaption>The landscape view on a typical 10-inch Android tablet (left) and on the iPad (right).</figcaption></figure>

However, with Android, screen size is only the half of it. Android tablets also come in different “screen densities” &mdash; that is, the number of pixels within a given area of the screen. Without going into too much detail, designers have to prepare all production-ready bitmaps for three different screen densities, by scaling each bitmap to 1.5&times; and 2&times; its original size. So, a bitmap set to 100 &times; 100 pixels would also have copies at 150 &times; 150 and 200 &times; 200. By making three batches of graphics scaled at these sizes, you will be able to deliver your bitmaps to medium, high and extra-high density tablet screens without losing image quality.

For more information on screen densities and preparing graphics for Android devices, refer to my <a href="https://www.smashingmagazine.com/2011/06/30/designing-for-android/">previous article on designing for Android</a>.

### System Bar

While iOS makes minimal use of the system bar, Android Honeycomb expands its size to include notifications and soft navigation buttons. There is a “Back” button, a home button and a “Recent apps” button.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5733328f-0d9e-45f2-a1e7-a56ed0ab5b16/image-3.jpg"><img loading="lazy" decoding="async" class="110065" title="image_3" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5733328f-0d9e-45f2-a1e7-a56ed0ab5b16/image-3.jpg" alt="" width="550" height="464" /></a><figcaption>The Android Honeycomb system bar.</figcaption></figure>

Android Honeycomb’s system bar and buttons are always present and appear at the bottom of the screen regardless of which app is open. Think of it like a permanent UI fixture. The only exception is a “Lights out” mode, which dims the system bar to show immersive content, such as video and games.

### “Back” Button

While the bulkiness and permanence of the Honeycomb system bar might seem an obstacle to designers, it does free up the real estate that is typically taken by the “Back” button in iPad apps. The “Back” button in Honeycomb’s system bar works globally across all apps.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1604e0a-220b-4a82-9b26-8f9d913f6fce/image-4.jpg"><img loading="lazy" decoding="async" class="110066" title="image_4" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1604e0a-220b-4a82-9b26-8f9d913f6fce/image-4.jpg" alt="" width="550" height="188" /></a><figcaption>The “Back” button in the system bar.</figcaption></figure>

### Action Bar

The bulk of the UI differences between platforms is found in the top action bar. Android suggests a specific arrangement of elements and a specific visual format for the action bar, including the placement of the icon or logo, the navigation (e.g. drop-down menu or tabs) and common actions. This is one of the most unifying design patterns across Android Honeycomb apps, and familiarizing yourself with it before attempting customizations or something iPad-like would be worthwhile. More on the pervasive action bar later.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/205e1d75-5651-4929-a9e6-9d92697072b1/image-5.jpg"><img loading="lazy" decoding="async" class="110067" title="image_5" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/205e1d75-5651-4929-a9e6-9d92697072b1/image-5.jpg" alt="" width="550" height="357" /></a><figcaption>The action bar.</figcaption></figure>

### Widgets

New to iPad users will be Android’s widgets. As the name implies, these are small notification and shortcuts tools that users can set to appear on their launch screen. Widgets can be designed to show stack views, grid views and list views, and with Android 3.1, they are now resizable.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a94c5517-92e2-48d2-b8ca-8ce9714c72d9/image-6.jpg"><img loading="lazy" decoding="async" class="110068" title="image_6" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a94c5517-92e2-48d2-b8ca-8ce9714c72d9/image-6.jpg" alt="" width="550" height="343" /></a><figcaption>Several widgets on a launch screen.</figcaption></figure>

### Notifications

While iOS’ notifications system pushes simple alerts to your launch screen, Honeycomb offers rich notifications that pop up (“toast” we used to call them) in the bottom-right area of the screen, much like Growl on Mac OS X. Custom layouts for notifications can be anything from icons to ticker text to actionable buttons.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f2affa9-86e4-42b8-8885-07b8ca212473/image-7.jpg"><img loading="lazy" decoding="async" class="110069" title="image_7" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f2affa9-86e4-42b8-8885-07b8ca212473/image-7.jpg" alt="" width="550" height="343" /></a><figcaption>A notification on Android.</figcaption></figure>

### Settings

Access to settings in an iPad app are usually presented in a pop-over, triggered by an “i” button; and settings categories are broken up into tables for easy visual identification. Honeycomb has a different convention. It looks more like the iOS’ “General Settings” screen, where the user navigates categories on the left and views details on the right. This is the preferred (and more elegant) way to present multiple settings in Honeycomb.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/032151a8-c0f5-49ea-a1c4-89837fd700d1/image-8.jpg"><img loading="lazy" decoding="async" class="110070" title="image_8" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/032151a8-c0f5-49ea-a1c4-89837fd700d1/image-8.jpg" alt="" width="550" height="345" /></a><figcaption>The settings design pattern in the Calendar app.</figcaption></figure>

### UI Elements

As you can imagine, Android goes to great lengths to do everything opposite from its competitor (that’s called differentiation!). Honeycomb has its own UI conventions, and it now has a new “holographic UI” visual language for such routine actions as picking a time and date, selecting an option, setting the volume, etc. Understanding this UI language is important to building screen flows and creating layouts.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbf86169-7ae8-4154-9685-2405021839bf/image-9.jpg"><img loading="lazy" decoding="async" class="110071" title="image_9" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dbf86169-7ae8-4154-9685-2405021839bf/image-9.jpg" alt="" width="550" height="503" /></a><figcaption>A sampling of UI elements, taken from a slide in a Google I/O 2011 presentation.</figcaption></figure>

### Fonts

How many fonts does iPad 4.3 make available? The answer is <a href="https://iosfonts.com/">fifty-seven</a>.

How many does Android? <a href="https://stackoverflow.com/questions/3532397/how-to-retrieve-a-list-of-available-installed-fonts-in-android">Just three</a>.

Yep, those three are <a href="https://www.droidfonts.com/droidfonts/about/">Droid Sans, Droid Serif and Droid Sans Mono</a>. But there is an upside. While only these three ship with the platform, developers are free to bundle any other fonts with their apps.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e15fa79-ddca-4fd4-acda-55aa5804ce08/image-10.jpg"><img loading="lazy" decoding="async" class="110072" title="image_10" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e15fa79-ddca-4fd4-acda-55aa5804ce08/image-10.jpg" alt="" width="550" height="523" /></a><figcaption>Droid Sans, Droid Serif and Droid Sans Mono.</figcaption></figure>

## Anything The Same?

Luckily for designers who are already familiar with the iPad, the two platforms have some similarities.

### Touch Gestures

Tap, double-tap, flick, drag, pinch, rotate and scroll at will.

### Split View And Multi-Pane UI

The split view is one of the most common layouts for tablets. It consists of two side-by-side panes. Of course, you can add panes for more complex layouts.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e8561b2-5386-47a3-999c-c771714b9d2e/image-111.jpg"><img loading="lazy" decoding="async" class="110098" title="image_11" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e8561b2-5386-47a3-999c-c771714b9d2e/image-111.jpg" alt="" width="550" height="304" /></a><figcaption>Ustream’s split-view layout, with categories on the left and content on the right.</figcaption></figure>

{{% ad-panel-leaderboard %}}

### Embedded Multimedia

Both platforms allow embedded audio, video and maps.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a84ee02c-c136-41e4-a8df-a4bad6145261/image-121.jpg"><img loading="lazy" decoding="async" class="110099" title="image_12" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a84ee02c-c136-41e4-a8df-a4bad6145261/image-121.jpg" alt="" width="550" height="305" /></a><figcaption>The YouTube app, with an embedded video player.</figcaption></figure>

### Clipboard

For copying and pasting data into and out of applications.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d37a985d-e9a0-4d65-b724-e5833608dceb/image-13.jpg"><img loading="lazy" decoding="async" class="110075" style="margin: 10px" title="image_13" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d37a985d-e9a0-4d65-b724-e5833608dceb/image-13.jpg" alt="" width="352" height="161" /></a></figure>

### Drag And Drop

Both platforms have drag-and-drop capabilities.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ea88bb8-3761-4e34-99e9-0e45ca0107d3/image-14.jpg"><img loading="lazy" decoding="async" class="110076" title="image_14" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ea88bb8-3761-4e34-99e9-0e45ca0107d3/image-14.jpg" alt="" width="550" height="333" /></a><figcaption>The drag-and-drop feature in the Gmail app.</figcaption></figure>

## Design Patterns

Honeycomb continues many of the <a href="https://www.smashingmagazine.com/2011/06/30/designing-for-android/">design patterns introduced in Android 2.0</a> and expands on them. In case you’re not familiar with design patterns, they are, as defined in Android, a “general solution to a recurring problem.” Design patterns are key UI conventions designed by Android’s maintainers to help unify the user experience and to give designers and developers a template to work from. They are also customizable, so no need to fret!

As mentioned, the action bar is the most prominent Android UI component and is the one we’ll focus on here.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff3d4f9a-279a-4e77-ab56-12d2e2683cbd/image-151.jpg"><img loading="lazy" decoding="async" class="110097" title="image_15" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff3d4f9a-279a-4e77-ab56-12d2e2683cbd/image-151.jpg" alt="" width="550" height="328" /></a><figcaption>The action bar highlighted in the Calendar app.</figcaption></figure>

### Icon Or Logo

The action bar starts with an icon or logo on the far left. It is actionable; by tapping on it, the user is directed to the app’s home screen.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ffdbebb-80a1-4ef3-b30f-96cb1f04c102/image-16.jpg"><img loading="lazy" decoding="async" class="110078" title="image_16" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ffdbebb-80a1-4ef3-b30f-96cb1f04c102/image-16.jpg" alt="" width="550" height="261" /></a><figcaption>The Calendar app icon.</figcaption></figure>

### Navigation

Next, we’ll typically find some form of navigation, in the form of a drop-down or tab menu. Honeycomb uses a triangle graphic to indicate a drop-down menu and a series of underlines for tabs, which typically take up most of the action bar’s real estate.

A left arrow button might also appear to the left of the icon or logo or the label, for navigating back or cancelling a primary action.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fa111c0-5f15-4789-b558-45088c4fa617/image-171.jpg"><img loading="lazy" decoding="async" class="110100" title="image_17" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4fa111c0-5f15-4789-b558-45088c4fa617/image-171.jpg" alt="" width="550" height="346" /></a><figcaption>Three different kinds of action bar navigation.</figcaption></figure>

### Common Actions

Common actions, as the name implies, gives user such things as search, share and an overflow menu. They are always positioned to the right of the action bar, away from any tabs.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b1adf64-9e39-4990-8738-2503468cc1e4/image-181.jpg"><img loading="lazy" decoding="async" class="110101" title="image_18" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b1adf64-9e39-4990-8738-2503468cc1e4/image-181.jpg" alt="" width="550" height="262" /></a><figcaption>Common actions in the Calendar app.</figcaption></figure>

### Overflow Menu

The overflow menu is part of the common actions group and is sometimes separated by a vertical rule. It is a place for miscellaneous menu items, such settings, help and feedback.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e20a6ca-1dbc-498b-929e-6ffc5b242de1/image-191.jpg"><img loading="lazy" decoding="async" class="110102" title="image_19" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6e20a6ca-1dbc-498b-929e-6ffc5b242de1/image-191.jpg" alt="" width="550" height="262" /></a><figcaption>An overflow menu.</figcaption></figure>

### Search

Search is also a part of the common actions group. Unique to search is its expand and collapse action. Tap on the search icon and a search box expands out, letting you enter a query. Tap the “x” to cancel, and it collapses to its single-button state. This is a space saver when many actions or tabs need to be shown.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/240dd360-6f0f-47d5-83ee-e417486c90eb/image-20.jpg"><img loading="lazy" decoding="async" class="110082" title="image_20" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/240dd360-6f0f-47d5-83ee-e417486c90eb/image-20.jpg" alt="" width="550" height="185" /></a><figcaption>The search function collapsed (top) and expanded (bottom). Tapping the magnifying glass opens the search box, while tapping the “x” closes it.</figcaption></figure>

### Contextual Actions

Contextual actions change the format of the action bar when an item is selected, revealing options unique to that item. For example, if a photo app is displaying thumbnails, the action bar might change once an image is selected, providing contextual actions for editing that particular image.

To exit the contextual action bar, users can tap either “Cancel” or “Done” at the far right of the bar.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef94e2fa-40f5-4513-898e-0c7ef3071e91/image-21.jpg"><img loading="lazy" decoding="async" class="110083" title="image_21" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef94e2fa-40f5-4513-898e-0c7ef3071e91/image-21.jpg" alt="" width="550" height="77" /></a><figcaption>The contextual action bar is triggered when tapping and holding an email in the Gmail app.</figcaption></figure>

## Tablet Layout Strategies

### Using Fragments and Multi-Pane Views

The building blocks of Honeycomb design are “<a href="https://android-developers.blogspot.com/2011/02/android-30-fragments-api.html">Fragments</a>.” A Fragment is a self-contained layout component that can change size or layout position depending on the screen’s orientation and size. This further addresses the problem of designing for multiple form factors by giving designers and developers a way to make their screen layout components elastic and stackable, depending on the screen restraints of the device that is running the app. Screen components can be stretched, stacked, expanded or collapsed and shown or hidden.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1ebcd7c-5090-4ab8-9a41-d7e9a3903514/image-22.jpg"><img loading="lazy" decoding="async" class="110084" title="image_22" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f1ebcd7c-5090-4ab8-9a41-d7e9a3903514/image-22.jpg" alt="" width="550" height="289" /></a><figcaption>The Fragments framework gives designers and developers several options for maintaining their layouts across screen sizes and orientation modes.</figcaption></figure>

What makes Fragments so special? With a compatibility library, developers can bring this functionality to Android smartphones going back to version 1.6, allowing them to build apps using a one-size-fits-all strategy. In short, it enables designers and developers to build one app for everything.

While Fragments may be a term used more by developers, designers should still have a basic understanding of how capsules of content can be stretched, stacked, expanded and hidden at will.

The most common arrangement of Fragments is the split view. This layout is common in news apps and email clients, where a list is presented in a narrow column and a detailed view in a wider one.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74c18cf0-70e1-4b2e-8def-50a8eb46bc50/image-23.jpg"><img loading="lazy" decoding="async" class="110085" title="image_23" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/74c18cf0-70e1-4b2e-8def-50a8eb46bc50/image-23.jpg" alt="" width="550" height="301" /></a><figcaption>The split view used by USA Today.</figcaption></figure>

Another way to present a split view is to turn it on its side. In this case, the sideways list Fragment becomes a carousel, navigating horizontally instead of vertically.

### Orientation Strategies

While Fragments are great for applying one design to multiple screen sizes, they are also useful for setting orientation strategies. Your screen design might look great in landscape view, but what will you do with three columns in a narrow portrait view? Again, you have the option to stretch, stack or hide content. Think of Fragments like a bunch of stretchy puzzle pieces that you can move around, shape and eliminate as needed.

## A Word About Animation

The Honeycomb framework allows designers and developers to use a variety of animation effects. According to the Android 3.0 Highlights page, “Animations can create fades or movement between states, loop an animated image or an existing animation, change colors, and much more.” Honeycomb also boasts high-performance mechanisms for presenting 2-D and 3-D graphics. For a good overview of what Honeycomb is capable of, check out <a href="https://youtube.com/watch?v=DAXm0-HA8O8&amp;feature=player_embedded">this video</a>.

## Learning from Example

Android tablet apps are still a relatively new space, and some brands are only beginning to test the waters. Below is a list of apps for inspiration. You can download any of them from the <span class="removed_link" title="https://market.android.com/?hl=en">Android Market</span> or <a href="https://www.amazon.com/mobile-apps/b/ref=sa_menu_adr_app4?ie=UTF8&amp;node=2350149011">Amazon</a>.

**YouTube**  
Naturally, Google’s YouTube app for Honeycomb is exemplary, showcasing all of the design patterns and UI elements discussed above. To get a good feel for Honeycomb, download this app first and take it for a spin.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/166e0aed-6a62-4c9c-aba4-7571db779645/image-24.jpg"><img loading="lazy" decoding="async" class="110086" title="image_24" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/166e0aed-6a62-4c9c-aba4-7571db779645/image-24.jpg" alt="" width="550" height="304" /></a></figure>

**CNN**  
The CNN app makes good use of touch gestures (including flicking to view more content), the split view and fonts! A custom font (Rockwell) is used for news headlines.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f008bf1b-e013-44d2-960c-79b830dce399/image-26.jpg"><img loading="lazy" decoding="async" class="110088" title="image_26" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f008bf1b-e013-44d2-960c-79b830dce399/image-26.jpg" alt="" width="550" height="302" /></a></figure>

**CNBC**  
Another good news app, with animation (the stock ticker tape) and rich graphics and gradients. CNBC has one of the most visually compelling apps.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18b30e06-8195-40a5-adf1-2707ef3f21d5/image-27.jpg"><img loading="lazy" decoding="async" class="110089" title="image_27" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18b30e06-8195-40a5-adf1-2707ef3f21d5/image-27.jpg" alt="" width="550" height="303" /></a></figure>

**Plume**  
With its three-column layout, Plume is a good example of how layouts might need to be changed dramatically from landscape to portrait views.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6e6f63c-62ca-4fcd-8fb2-cf3cdb87597c/image-28.jpg"><img loading="lazy" decoding="async" class="110090" title="image_28" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6e6f63c-62ca-4fcd-8fb2-cf3cdb87597c/image-28.jpg" alt="" width="550" height="304" /></a></figure>

**FlightTrack**  
A data-heavy app done elegantly. Includes nice maps, subtle animation and standard Honeycomb UI elements.

Common actions, as the name implies, gives user such things as search, share and an overflow menu. They are always positioned to the right of the action bar, away from any tabs.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b1adf64-9e39-4990-8738-2503468cc1e4/image-181.jpg"><img loading="lazy" decoding="async" class="110101" title="image_18" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b1adf64-9e39-4990-8738-2503468cc1e4/image-181.jpg" alt="" width="550" height="262" /></a><figcaption>Common actions in the Calendar app.</figcaption></figure>

**Pulse**  
What else can you say: it’s Pulse for Android tablets! But comparing the Android and iPad versions, which are identical in almost every way, is still fun anyway.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ce57494-587f-4ed2-b07b-435e907e466a/image-30.jpg"><img loading="lazy" decoding="async" class="110092" title="image_30" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1ce57494-587f-4ed2-b07b-435e907e466a/image-30.jpg" alt="" width="550" height="304" /></a></figure>

**WeatherBug**  
This was one of the first Honeycomb apps in the Android Market. It makes good use of maps and of the holographic UI for showing pictures from weather cams.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a91d54d7-6709-4e0e-9d47-483ab4171b53/image-31.jpg"><img loading="lazy" decoding="async" class="110093" title="image_31" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a91d54d7-6709-4e0e-9d47-483ab4171b53/image-31.jpg" alt="" width="550" height="303" /></a></figure>

**Kindle**  
Kindle pretty much sticks to the book in using design patterns and Honeycomb UI elements. The outcome is elegant, while staying true to Android’s best practices.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f95f7847-ce65-47c4-9a3e-51bfc54ef662/image-32.jpg"><img loading="lazy" decoding="async" class="110094" title="image_32" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f95f7847-ce65-47c4-9a3e-51bfc54ef662/image-32.jpg" alt="" width="550" height="304" /></a></figure>

### Honorable Mentions

*   IMDb
*   News360
*   USA Today
*   AccuWeather
*   Ustream
*   Google Earth
*   Think Space

## Online Resources

### Video

*   [Designing and Implementing Android UIs for Phones and Tablets](https://youtube.com/watch?v=WGIU2JX1U5Y&feature=player_embedded#at=3469), Google I/O 2011
*   [Android 3.0 Honeycomb animation demo](https://youtube.com/watch?v=DAXm0-HA8O8&feature=player_embedded)

### Presentations

*   Designing and Implementing Android UIs for Phones and Tablets, Google I/O 2011 (PDF)

### Blogs

*   [Tablet UI Patterns](https://www.androiduipatterns.com/2011/06/tablet-ui-patterns-action-bar.html)

### Android Developers

*   [Supporting Multiple Screens](https://developer.android.com/guide/practices/screens_support.html)
*   [Icon Design](https://developer.android.com/guide/practices/ui_guidelines/icon_design.html)

{{% ad-panel-leaderboard %}}

### Further Reading

*   [How To Design For Android](https://www.smashingmagazine.com/2011/06/designing-for-android/)
*   [Mobile Design Practices For Android: Tips And Techniques](https://www.smashingmagazine.com/2012/07/android-design-tips/)
*   [Transform A Tablet Into An Affordable Kiosk For Your Clients](https://www.smashingmagazine.com/2012/11/transform-tablet-affordable-kiosk-clients/)

{{< signature "al, mrn" >}}

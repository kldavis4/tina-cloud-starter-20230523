---
title: 'Designing For Device Orientation: From Portrait To Landscape'
slug: designing-device-orientation-portrait-landscape
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/655e459c-617d-41e1-8d4b-213679d39707/swiss-school-illu.jpg
date: 2012-08-10T10:10:28.000Z
author: avi-itzkovitch
description: >-
  The accelerometer embedded in our smart devices is typically used to align the
  screen depending on the orientation of the device, i.e. when switching between
  portrait and landscape modes. This capability provides great opportunities to
  create better user experiences because it offers an additional layout with a
  simple turn of a device, and without pressing any buttons.
categories:
  - UX
  - Usability
  - UX
  - Design Patterns
  - Web Design
---
The accelerometer embedded in our smart devices is typically used to align the screen depending on the orientation of the device, i.e. when switching between portrait and landscape modes. This capability provides great opportunities to create better user experiences because it offers an additional layout with a simple turn of a device, and without pressing any buttons.

However, designing for device orientation brings various challenges and requires careful thinking. The experience must be as unobtrusive and transparent as possible, and we must understand the context of use for this functionality.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Breakpoints And The Future Of Websites](https://www.smashingmagazine.com/2014/07/breakpoints-and-the-future-websites/)
*   [<span class="headline">Building A Better Responsive Website</span>](https://www.smashingmagazine.com/2013/03/building-a-better-responsive-website/)
*   [How To Build A Mobile Website](https://www.smashingmagazine.com/2010/11/how-to-build-a-mobile-website/)

Nearly all mobile and tablet applications would benefit from being designed for device orientation. This article covers some of the basic concepts that designers and developers can use to add device orientation to their process. We’ll present some of the challenges when designing for device orientation, along with some solutions.

{{% feature-panel %}}

## Using Device Orientation For A Secondary Display

YouTube's mobile application is a great example of device orientation design. Portrait mode offers a feature-rich interface for video discovery and the user's account. Landscape mode provides an immersive experience with a full-screen video player and playback controls. When the video ends, the display switches back to portrait mode, prompting users to quickly tilt the device back and browse for additional videos.

However, using orientation to display a secondary interface can be confusing for users. For instance, in <a href="https://itunes.apple.com/us/app/cardmunch-business-card-reader/id478351777?mt=8">CardMunch</a> (a business-card reader by LinkedIn), users can convert business-card images into address book contacts using the smartphone’s camera. Rotating CardMunch to landscape mode changes the interface altogether to a carousel overview of all of your saved cards.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ba60542-63e0-44e0-9e55-cb60126e6fa7/youtube03.jpg"><img class="113254" title="YouTube's mobile interface in portrait and landscape modes." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ba60542-63e0-44e0-9e55-cb60126e6fa7/youtube03.jpg" alt="" width="800" height="421" /></a><br>
<em>YouTube’s mobile interface in portrait and landscape modes.</em>

This interface lacks any visual clues about its orientation, and it has limited controls. You are unable to edit or add business cards, making the carousel screen somewhat frustrating and confusing, especially if you’ve launched the app in landscape mode. In addition, the lack of visual clues in this landscape mode will deter most users from rotating the device and discovering the app’s other features.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34f4ad12-c945-41e7-91c1-a9db1658ad80/cardm.jpg"><img loading="lazy" decoding="async" class="113269" title="CardMunch by LinkedIn. " src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34f4ad12-c945-41e7-91c1-a9db1658ad80/cardm.jpg" alt="" width="800" height="421" /></a><br>
<em>CardMunch by LinkedIn is missing visual clues about its secondary interface.</em>

## Categories Of Orientation Design

To help UX professionals and developers, I have categorized four main patterns of device orientation design.</p>

### Fluid

This interface simply adjusts to the new orientation’s size.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab166ce-fad7-4db1-9780-f9eccf2e6c07/skype.jpg"><img loading="lazy" decoding="async" class="113277" title="Skype mobile interface. " src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ab166ce-fad7-4db1-9780-f9eccf2e6c07/skype.jpg" alt="" width="800" height="421" /></a><br>
<em>In Skype’s mobile interface, the icons change position when the screen moves from portrait to landscape.</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46461871-8835-4c02-bad1-1640fdbbec8e/pocket.jpg"><img loading="lazy" decoding="async" class="113280" title="Pocket mobile interface. " src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46461871-8835-4c02-bad1-1640fdbbec8e/pocket.jpg" alt="" width="800" height="421" /></a><br>
<em><a href="https://getpocket.com/">Pocket</a>’s mobile interface: same layout, different width.</em>

### Extended

This interface adjusts to the screen’s size, adding or subtracting layout components according to the dimensions of the chosen orientation. For example, <a href="https://itunes.apple.com/us/app/imdb-movies-tv/id342792525?mt=8">IMDb</a> for the iPad uses the wider screen in landscape mode to add a filmography on the left. This list is also accessible in portrait mode by clicking the “All filmography” button in the middle-right of the screen.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f74806b3-f302-496a-9ffd-2a46ecf89159/imdb.jpg"><img loading="lazy" decoding="async" class="113290" title="IMDb Movies &amp; TV for the iPad." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f74806b3-f302-496a-9ffd-2a46ecf89159/imdb.jpg" alt="" width="800" height="450" /></a><br>
<em>IMDb for the iPad.</em>

Providing visual elements and functionality in any orientation ultimately gives convenience to the user. However, not forcing the user to hold the device a certain way is crucial, especially if the desired functionality does not appear in the default orientation.</p>

### Complementary

With this interface, a changed orientation triggers an auxiliary screen with relevant supplementary information. An example would be a mobile financial application that displays data in the default portrait mode, and then provides a visual graph when the user rotates to landscape mode. The orientations show similar or complementary data and depend on each other.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5da4227d-ec18-48a6-8a44-6c5949406942/bank.jpg"><img loading="lazy" decoding="async" class="113295" title="An example of a complementary design interface." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5da4227d-ec18-48a6-8a44-6c5949406942/bank.jpg" alt="" width="800" height="450" /></a><br>
<em>An example of a complementary design interface</em>

### Continuous

Like YouTube, a continuous design enables the user to access a secondary interface by a simple rotation of the device. An example would be using a smartphone as a remote control for a smart TV. Rotating the device to landscape mode would reveal a full program guide, while also maintaining functionality for changing channels, browsing programs and recording future episodes.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2dbd6a2-8ee2-4dbe-8685-e694474a0e0e/remote.jpg"><img loading="lazy" decoding="async" class="113299" title="A smart remote and program guide." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c2dbd6a2-8ee2-4dbe-8685-e694474a0e0e/remote.jpg" alt="" width="800" height="450" /></a><br>
<em>A smart remote and program guide.</em>

## Considering The Default Orientation

<a href="https://itunes.apple.com/us/app/above-beyond-john-kascht/id454178260?mt=8">Above &amp; Beyond</a> is an interactive eBook for the iPad about the life and work of the American caricature artist John Kascht. The beautiful art in this book is displayed in both portrait and landscape modes. However, horizontal mode shows important interactive elements that do not appear in portrait mode, such as a way to return to the main menu. Portrait is the iPad’s default orientation, so including this type of added interactivity only in landscape mode might confuse many users.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fcae455-7eed-4928-b14b-7dc5a36f6af1/anb.jpg"><img loading="lazy" decoding="async" class="113302" title="A Page from Above &amp; Beyond: John Kascht. " src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fcae455-7eed-4928-b14b-7dc5a36f6af1/anb.jpg" alt="" width="800" height="450" /></a><br>
<em>A page from Above &amp; Beyond. The interactive elements do not appear in the default portrait mode.</em>

While portrait mode shows a detailed look at the art, and the interactive eBook provides some instructions at the beginning, a solution might be to allow users to tap the screen to reveal the menu. The default orientation for most smartphones and for the iPad is portrait. However, landscape is the default for Android, Windows 8 tablets and BlackBerry’s Playbook. To avoid confusion, remember that the primary orientation of your app should always serve the device’s default mode and functionality, not the other way around.

## Understanding The Context

When designing an application for smart devices, consider the context and circumstances in which that application will be used, particularly when designing for device orientation. Case in point: interactive cookbooks have become very popular. Hardware and accessory manufacturers are creating <a href="https://www.steelie.com/">devices</a> to help us use the <a href="https://www.belkin.com/IWCatProductPage.process?Product_Id=557465">iPad in the kitchen</a>, including a <a href="https://www.belkin.com/IWCatProductPage.process?Product_Id=557467">washable stylus</a> for use while cooking.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82ae1d2d-d771-44db-8ec1-a89b19f82c19/kitchen-ban-1.jpg"><img loading="lazy" decoding="async" class="113309" title="Devices to help us use the iPad in the kitchen." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82ae1d2d-d771-44db-8ec1-a89b19f82c19/kitchen-ban-1.jpg" alt="" width="1200" height="475" /></a>

We can use orientation to create a better experience in a cookbook. Using the iPad’s default portrait orientation, users can flip through the book and view the full recipe and ingredients list for a particular dish. Rotating the device to landscape mode will change the interface to a cook-friendly layout, with large buttons and step-by-step instructions. This cook-friendly interface would also prevent the tablet from auto-dimming, and it would allow users to flip pages by waving their hand in front of the built-in camera to avoid touching the screen with messy hands while cooking.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e924270-aedc-45b3-9183-e246cbc1bb61/betty.jpg"><img loading="lazy" decoding="async" class="113315" title="The Betty Crocker® Cookbook for iPad." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e924270-aedc-45b3-9183-e246cbc1bb61/betty.jpg" alt="" width="800" height="450" /></a><br>
<em><a href="https://www.bettycrocker.com/downloads-and-games/ipad-app">The Betty Crocker Cookbook</a> for iPad is an example of a cook-friendly interface.</em>

Understanding the context of the kitchen and how people cook with the iPad would make the interactive eBook much more functional. With the added consideration of device orientation, the user experience would be better overall.</p>

## Visual Clues About Orientation

An auxiliary screen or added functionality that depends on orientation can sometimes be counterintuitive. Without any visual clues in a particular orientation, a user might miss the added functionality altogether. A classic example of this is the iPhone’s built-in calculator, as pointed out in Salon’s post “How to Change the iPhone Calculator Into a Scientific Calculator” — functionality that many users do not know about.

When designing for device orientation, visual clues increase <a href="https://en.wikipedia.org/wiki/Findability">findability</a> and makes the user experience intuitive and transparent. Below are a few examples of visual clues for device orientation.</p>

### Title Bar

Affixing the title bar to the top of the default position in either orientation is a subtle clue for the user to tilt their head (or device) to read the text in the bar. This technique is essential when using orientation for a secondary display and serves as a gentle reminder about the added functionality.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21fb23ae-0096-4969-b1f4-b643f49360de/title-bar.jpg"><img loading="lazy" decoding="async" class="113320" title="Title Bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21fb23ae-0096-4969-b1f4-b643f49360de/title-bar.jpg" alt="" width="753" height="435" /></a>

<strong>Note:</strong> This method will not give <a href="https://en.wikipedia.org/wiki/Affordance">affordance</a> to the added display in the default (portrait) orientation. In this case, I recommend coach marks, a quick tutorial or a walkthrough video (when appropriate) to illustrate that the application is using orientation for a secondary display.</p>

### Toggle Switch

Much like the <a href="https://shareicons.com/">universal icon for sharing</a> or Apple’s familiar action button for sharing, I propose a standard icon to represent device orientation. You can <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/165d89a9-d8bc-468f-8084-90d2f4d3225e/device-orientation-icon-10.zip">download</a> the icon shown below and use it freely.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/496d7edd-0759-43cf-96f8-eac6771aa2d8/icons.jpg"><img loading="lazy" decoding="async" class="113324" title="icons" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/496d7edd-0759-43cf-96f8-eac6771aa2d8/icons.jpg" alt="" width="700" height="175" /></a>

The icon should appear at all times and be used as a toggle switch between orientation displays. Using the toggle would not require the user to rotate the device for the secondary view, but it would gradually encourage users to rotate the device to view the secondary interface without pressing the icon. Rotating the device back to the default orientation would automatically adjust the display. Ultimately, this icon would serve as a visual reminder for the added functionality; the user would not need to use this control to switch between orientation displays but would simply rotate the device instead.

Below are illustrations of this toggle icon in use:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f560310-73d9-4015-b2fd-65eb06c20b2e/toggle-switch02a.jpg"><img loading="lazy" decoding="async" class="113326" title="Title bar toggle switch button. " src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f560310-73d9-4015-b2fd-65eb06c20b2e/toggle-switch02a.jpg" alt="" width="900" height="463" /></a><br>
<em>Toggle button in the title bar.</em>

If standardized, the orientation icon would give affordance and serve as a visual clue. Here is an illustration of this toggle icon in a corner triangle.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7be2f91b-bc2a-4a28-88b5-01853e6185f5/toggle-switch02b.jpg"><img loading="lazy" decoding="async" class="113329" title="Corner triangle orientation display toggle switch. " src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7be2f91b-bc2a-4a28-88b5-01853e6185f5/toggle-switch02b.jpg" alt="" width="810" height="469" /></a><br>
<em>Orientation toggle in corner triangle.</em>

<strong>Note:</strong> The device orientation icon is not a proven idea, and the value of adding this somewhat redundant UI control is debatable. However, in my opinion, the idea is simple and effective and would enable designers to more fully rely on device orientation to enhance and extend their applications. Hopefully, the proposals here will spark a conversation in the design community and lead to a solution whereby, with a simple turn of the device, essential functionality is added to any application.</p>

### The Drawer

The idea here is to show a drawer-like control that users can tap or swipe in order to see the secondary view. Rotating the device would automatically open the drawer, much like a curtain opening. By using an animation to open and close the drawer, the designer can create a memorable effect for displaying data based on orientation.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71e21f88-7e73-4236-8d99-61ef2b7f53f5/the-drawer.jpg"><img loading="lazy" decoding="async" class="113334" title="Example of a drawer control." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/71e21f88-7e73-4236-8d99-61ef2b7f53f5/the-drawer.jpg" alt="" width="845" height="449" /></a><br>
<em>Illustration of a drawer control.</em>

## Conclusion

Designing for device orientation is not new. For example, when rotated to landscape mode, smartphones open a larger virtual keyboard, and the email applications in tablets switch to a <a href="https://en.wikipedia.org/wiki/Master%E2%80%93detail_interface">master–detail</a> interface. However, device orientation design is widely treated as secondary to the main interface because it is often missed by users who stick to the default orientation, mainly because they are not aware of its availability. By adding simple visual clues to the interface, UX professionals can make the case for using device orientation to enhance their products and, ultimately, for providing more engaging and user-friendly experiences.

<em>(al) (il)</em>


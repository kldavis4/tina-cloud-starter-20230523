---
title: 'Testing Mobile: Emulators, Simulators And Remote Debugging'
slug: testing-mobile-emulators-simulators-remote-debugging
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/619aa86a-0476-42eb-b02e-1d62d5bd5fbd/08-ios-debugger-opt-500.jpg
date: 2014-09-03T21:16:28.000Z
author: jon-raasch
description: >-
  In the early days of mobile, debugging was quite a challenge. Sure, you could
  get ahold of a device and perform a quick visual assessment, but what would
  you do after discovering a bug?

  With a distinct lack of debugging tools, developers turned to a variety of
  hacks. In general, these hacks were an attempt to recreate a given issue in a
  desktop browser and then debug with Chrome Developer Tools or a similar
  desktop toolkit. For instance, a developer might shrink the size of the
  desktop browser’s window to test a responsive website or alter the user agent
  to spoof a particular mobile device.
categories:
  - Mobile
  - Techniques
  - Testing
---
In the early days of mobile, debugging was quite a challenge. Sure, you could get ahold of a device and perform a quick visual assessment, but what would you do after discovering a bug?

With a distinct lack of debugging tools, developers turned to a variety of hacks. In general, these hacks were an attempt to recreate a given issue in a desktop browser and then debug with Chrome Developer Tools or a similar desktop toolkit. For instance, a developer might shrink the size of the desktop browser’s window to test a responsive website or alter the user agent to spoof a particular mobile device.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Prioritizing Devices: Testing And Responsive Web Design](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [<span class="headline">Establishing An Open Device Lab</span>](https://www.smashingmagazine.com/2012/09/establishing-an-open-device-lab/)

To put it bluntly, these hacks don't work. If you’re recreating issues on the desktop, then you can’t be certain that any of your fixes will work. This means you’ll be constantly bouncing back and forth between the mobile device and the hacks in your desktop browser.

{{% feature-panel %}}

Fast forward to today, when we have a robust suite of debugging tools that provide meaningful debugging information directly from a physical device. Best of all, you can use the same desktop debugging tools that you know and love, all on an actual mobile device.

In this article, we’ll explore a variety of emulators and simulators that you can use for quick and easy testing. Then, we’ll look at remote debugging tools, which enable you to connect a desktop computer to a mobile device and leverage a rich debugging interface.</p>

## Emulators And Simulators

Testing on real physical devices always pays off. But that doesn’t mean you shouldn’t also test on emulators and simulators. These virtual environments not only expand your testing coverage to more devices, but also are a quick and easy way to test small changes on the fly.</p>

### iOS Simulator

To test iOS devices, such as the iPhone and iPad, you have a number of options, most notably Apple’s official iOS Simulator. Included as part of Xcode, this simulator enables you to test across different software and hardware combinations, but only from a Mac.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efcc2c8b-d43e-4ec6-8896-0b488ddbb802/01-ios-simulator-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4806700-a9c8-4a15-9a31-de97097d7de3/01-ios-simulator-opt-500.jpg" alt="Viewing a website in iOS Simulator" width="294" height="600" /></a><figcaption>Viewing a website in iOS Simulator (Image: <a href="https://jonraasch.com/">Jon Raasch</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efcc2c8b-d43e-4ec6-8896-0b488ddbb802/01-ios-simulator-opt.jpg">View large version</a>)</figcaption></figure>

First, install and open Xcode. Then, in Xcode, right-click and select “Show Package Contents.” Go to “Contents” → “Applications” → “iPhone Simulator.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f92fec2d-ee77-4ede-a6e1-11cb1b180159/02-ios-simulator-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/73119588-6f92-483f-90d9-b359dd174858/02-ios-simulator-opt-500.jpg" alt="Finding iOS Simulator in Xcode" width="500" height="243" /></a><figcaption>Finding iOS Simulator in Xcode (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f92fec2d-ee77-4ede-a6e1-11cb1b180159/02-ios-simulator-opt.jpg">View large version</a>)</figcaption></figure>

Although iOS Simulator is difficult to find, using it is fortunately easy. Simply open up Safari in the simulator and test your website. You can switch between different iPhone and iPad devices, change the iOS version, rotate the viewport and more.

Note: If you’re not working on a Mac, you’ll have to find another option. You could look to <a href="https://download.cnet.com/iPadian/3000-2072_4-75607175.html">iPadian</a>, a Windows-based iPad simulator. Beyond that, a handful of other simulators exist, including certain <a href="https://iphone5simulator.com/">web-based offerings</a>. But, to be honest, none of these are very promising.</p>

### Android Emulator

Android also provides an emulator. Luckily, this one is cross-platform. Unfortunately, setting it up is a bit of a pain.

First, <a href="https://developer.android.com/sdk/index.html">download the bundle</a> that includes Android Development Tools (ADT) for Eclipse and the Android software development kit (SDK). Next, <a href="https://developer.android.com/sdk/installing/adding-packages.html">follow Google’s instructions</a> to install the SDK packages, making sure to install the default selections as well as the “Intel x86 Emulator Accelerator (HAXM installer)”. You’ll also need to track down HAXM — search your Mac for <code>IntelHaxm.dmg</code> or your PC for <code>IntelHaxm.exe</code>, and run the file to install it.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce45777-531e-445f-9fed-83cb63838ebf/03-android-emu-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f747b144-ed95-4602-a22b-9f8728dadb70/03-android-emu-opt-500.jpg" alt="Installing Android SDK packages. HAXM improves performance for the emulator." width="500" height="358" /></a><figcaption>Installing the Android SDK packages: HAXM improves the performance of the emulator. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ce45777-531e-445f-9fed-83cb63838ebf/03-android-emu-opt.jpg">View large version</a>)</figcaption></figure>

Next, create an Android virtual device (AVD) for whichever device you’re testing. If you go into the AVD manager, you’ll see a list of preset devices in “Device Definitions.” These cover a variety of Google products and some generic devices. To get started, select one of these presets and click “Create AVD.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24190964-61d1-4ab9-a011-a83d18c34115/04-android-emu-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d8bf84c-25ab-4b7c-a84b-8a0d81d46ed4/04-android-emu-opt-500.jpg" alt="The Device Definitions tab provides preset AVDs. Use one of these or create your own." width="500" height="356" /></a><figcaption>The “Device Definitions” tab provides preset AVDs. Use one of them or create your own. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24190964-61d1-4ab9-a011-a83d18c34115/04-android-emu-opt.jpg">View large version</a>)</figcaption></figure>

Set whatever you like for the CPU, and set “No skin“ and “Use host GPU.” Now you can run the virtual device and use Android’s browser to test your website.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e2105f2-53fd-427d-ade6-a95e9f507646/05-android-emu-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/017d7578-6ef6-478b-b60e-1ee32522183c/05-android-emu-opt-500.jpg" alt="Viewing a website in Android Emulator." width="329" height="600" /></a><figcaption>Viewing a website in the Android emulator (Image: <a href="https://www.smashingmagazine.com">Smashing Magazine</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e2105f2-53fd-427d-ade6-a95e9f507646/05-android-emu-opt.jpg">View large version</a>)</figcaption></figure>

Finally, you’ll probably want to <a href="https://developer.android.com/tools/help/emulator.html">learn some keyboard commands</a> to better interact with the emulator.

Note: <a href="https://www.manymo.com/">Manymo</a> is an alternative, in-browser Android emulator. You can even embed it in a web page, which is pretty darn cool.</p>

### Other Simulators and Emulators

*   BlackBerry Simulators
*   [Windows Phone Emulator for Windows 8](https://msdn.microsoft.com/en-us/library/windows/apps/ff402563(v=vs.105).aspx)
*   [Opera Mini Emulator](https://dev.opera.com/articles/installing-opera-mini-on-your-computer/)

### Remote Testing

Emulators and simulators are useful, but they’re not 100% accurate. Always test on as many real devices as possible.

That doesn’t mean you need to buy a hundred phones and tablets. You can take advantage of remote testing resources, which provide a web-based interface to interact with real physical devices. You’ll be able to interact with a phone remotely and view any changes in the screencast that is sent back to your machine.

If you want to test a Samsung device, such as the Galaxy S5, you can do so for free using Samsung’s <a href="https://developer.samsung.com/remotetestlab/">Remote Test Lab</a>, which enables you to test on a wide selection of Samsung devices.

Additionally, you can use the resources in <a href="https://www.keynote.com/solutions/testing/mobile-testing">Keynote Mobile Testing</a>. They’re not cheap, but the number of devices offered is pretty astonishing, and you can test a handful of devices for free.

Note: If you’re looking to get your hands on real devices, <a href="https://opendevicelab.com/">Open Device Lab</a> can point you to a lab in your area, where you can test on a range of devices for free.

## Remote Debugging

Remote debugging addresses a variety of the challenges presented by mobile debugging. Namely, how do you get meaningful debugging information from a small and relatively underpowered device?

Remote debugging tools provide an interface to connect to a mobile device from a desktop computer. Doing this, you can debug for a mobile device using the development tools on a more powerful, easier-to-use desktop machine.</p>

### iOS

With the release of iOS 6.0, Apple introduced a tool that enables you to use desktop Safari’s Web Inspector to debug iOS devices.

To get started, enable remote debugging on your iOS device by going to “Settings” → “Safari” → “Advanced” and enabling “Web Inspector.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0450b31-c39f-4b47-8e5d-5739b2cb3c71/06-ios-debugger-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14219bff-8020-486b-82cb-124332d1961d/06-ios-debugger-opt-500.jpg" alt="First enable Web Inspector in Settings &gt; Safari &gt; Advanced." width="500" height="369" /></a><figcaption>First, enable Web Inspector in “Settings” → “Safari” → “Advanced.” (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d0450b31-c39f-4b47-8e5d-5739b2cb3c71/06-ios-debugger-opt.jpg">View large version</a>)</figcaption></figure>

Next, physically connect your phone or tablet to your machine using a USB cable. Then, open Safari (version 6.0 or higher), and in “Preferences” → “Advanced,” select “Show Develop menu in menu bar.”

Now, in the “Develop” menu you should see your iOS device, along with any open pages in mobile Safari.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/092bbaa7-5f36-4e07-81a4-4ae9dc475afd/07-ios-debugger-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60a2a046-6e78-46e0-b832-29e5d56908c0/07-ios-debugger-opt-500.jpg" alt="Once your iOS device is connected, you'll see it in the Develop menu." width="500" height="163" /></a><figcaption>Once your iOS device is connected, you’ll see it in the “Develop” menu. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/092bbaa7-5f36-4e07-81a4-4ae9dc475afd/07-ios-debugger-opt.jpg">View large version</a>)</figcaption></figure>

Select one of these pages, and you’ll have a wide range of developer tools at your fingertips. For example, try out the DOM Inspector, which enables you to tap DOM elements on your mobile device and see debugging information on the desktop.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5aebe1a-75f9-4ad1-9647-884e576cefb2/08-ios-debugger-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/619aa86a-0476-42eb-b02e-1d62d5bd5fbd/08-ios-debugger-opt-500.jpg" alt="The Web Inspector in desktop Safari is inspecting this iPhone." width="500" height="375" /></a><figcaption>Web Inspector in desktop Safari is inspecting this iPhone. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5aebe1a-75f9-4ad1-9647-884e576cefb2/08-ios-debugger-opt.jpg">View large version</a>)</figcaption></figure>

The DOM Inspector is really just the beginning. iOS’ remote developer tools provide a ton of features, such as:

*   timelines to track network requests, layout and rendering tasks and JavaScript;
*   a debugger to set breakpoints and to profile the JavaScript;
*   a JavaScript console.

To learn more about what you can do, read through the documents in the “<a href="https://developer.apple.com/library/safari/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/Introduction/Introduction.html">Safari Web Inspector Guide</a>.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5a80098-5518-4f56-ab5d-65f5b9465e1f/09-ios-debugger-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5fb6d4f5-94c2-4a1d-af97-835fb92a65e3/09-ios-debugger-opt-500.jpg" alt="You don't need a physical iOS device to use remote debugging. You can also debug instances of the iOS Simulator." width="500" height="300" /></a><figcaption>You don’t need a physical iOS device to use remote debugging. You can also debug instances of iOS Simulator. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5a80098-5518-4f56-ab5d-65f5b9465e1f/09-ios-debugger-opt.jpg">View large version</a>)</figcaption></figure>

Note: Much like iOS Simulator, you can only do remote debugging for iOS on Mac OS X.</p>

### Android

Similar to iOS, Android has a remote debugging solution. The tools in it enable you to debug an Android device from a desktop machine using Chrome’s Developer Tools. Best of all, Android’s remote debugging is cross-platform.

First, go to “Settings” → “About Phone” on your Android 4.4+ phone (or “Settings” → “About Tablet”). Next, tap the “Build Number” seven (7) times. (No, I’m not joking. You’ll see a message about being a developer at the end.) Now, go back to the main settings and into “Developer Options.” Here, enable “USB debugging,” and you’re all set.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8c46008-493b-48b6-8bc2-453640e20fd0/10-android-debugger-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef989cb3-0733-46e3-b067-e54f38f09e4e/10-android-debugger-opt-500.jpg" alt="Left: Tap the Build Number seven times to enable developer mode. Right: Enable USB Debugging." width="500" height="439" /></a><figcaption>Left: Tap the “Build Number” seven times to enable developer mode. Right: Enable “USB debugging.”(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8c46008-493b-48b6-8bc2-453640e20fd0/10-android-debugger-opt.jpg">View large version</a>)</figcaption></figure>

Go into your desktop Chrome browser, and type <code>about:inspect</code> in the address bar. Enable “Discover USB devices,” and you’ll see your device in the menu.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/250994c4-66fa-471a-a30b-65b3dcf8a077/11-android-debugger-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb9ae5da-42cb-454d-88c3-b76175ba89a0/11-android-debugger-opt-500.jpg" alt="Once you enable Discover USB devices, you'll see a list of devices that are connected remotely to Chrome, along with a list of debuggable web pages or apps for each device." width="500" height="325" /></a><figcaption>Once you enable “Discover USB devices,” you’ll see a list of devices connected remotely to Chrome, along with a list of debuggable web pages or apps for each device. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/250994c4-66fa-471a-a30b-65b3dcf8a077/11-android-debugger-opt.jpg">View large version</a>)</figcaption></figure>

You should also see any open tabs in your mobile browser. Select whichever tab you want to debug, and you’ll be able to leverage a ton of useful tools, such as:

*   a DOM Inspector,
*   a network panel for external resources,
*   a sources panel to watch JavaScript and to set breakpoints,
*   a JavaScript console.

To learn more about what’s possible, read HTML5 Rocks’ tutorial “<a href="https://www.html5rocks.com/en/tutorials/developertools/part1/">Introduction to Chrome Developer Tools, Part One</a>.”

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e79c08a4-7f0b-4245-8ee4-0c3c89d50f45/12-android-debugger-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2fdb5bf-ada1-4c23-8f5c-7d58a697cd0a/12-android-debugger-opt-500.jpg" alt="Remote debugging Android. Here the DOM Inspector in the desktop browser is inspecting the page on the mobile device." width="500" height="296" /></a><figcaption>Here, the DOM Inspector in the desktop browser is remotely inspecting a page on the Android device. (Image: <a href="https://developer.chrome.com/devtools/docs/remote-debugging">Google</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e79c08a4-7f0b-4245-8ee4-0c3c89d50f45/12-android-debugger-opt.jpg">View large version</a>)</figcaption></figure>

Note: You can also remotely debug with the Android emulator.</p>

### Weinre

You now know how to remotely debug a variety of devices. But if you want to debug iOS on Windows or on Linux or debug other devices, such as Windows Phone or BlackBerry, then try Weinre, which works on any device.

Setting up Weinre is a bit more complicated because you have to install it on both the server and the page. To get started, install Node, and then install the Weinre module with the following command:

<pre><code class="language-bash">
npm install –g weinre
</code></pre>

Next, run the debugging server using your development machine’s IP:

<pre><code class="language-bash">
weinre --boundHost 10.0.0.1
</code></pre>

Note: Make sure to insert your own IP in the command above. You can find your IP on a Mac using the command <code>ipconfig getifaddr en0</code> and on Windows using <code>ipconfig</code>.

Next, go to the development server that is outputted by Weinre in the console (in my case, it’s <code>localhost:8080</code>). Here, look at the “Target Script” section, and grab the <code>&lt;script&gt;</code> tag. You’ll need to include that on whichever pages you want to debug.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83ccce2b-a680-4b37-8e6d-a04e2048c220/13-weinre-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66e1697e-5b93-4ad9-8893-33b83bf32e32/13-weinre-opt-500.jpg" alt="The Weinre development server gives you the client-side script embedding code, along with a link to the debugging interface." width="500" height="410" /></a><figcaption>The Weinre development server gives you the client-side script to embed, along with a link to the debugging interface. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83ccce2b-a680-4b37-8e6d-a04e2048c220/13-weinre-opt.jpg">View large version</a>)</figcaption></figure>

Finally, click on the link at the top of this page for the user interface for debugging clients (in my case, it’s <code>https://localhost:8080/client/#anonymous</code>). Now, once you open the page in your device, you should see it in the list of targets.

Note: If you’re having trouble connecting a device to your localhost, consider setting up a public tunnel with <a href="https://ngrok.com/">ngrok</a>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07099f1e-8ffc-4934-a1a2-774e37c60447/14-weinre-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e92e2bf-f603-40fb-b27b-dad4993238e2/14-weinre-opt-500.jpg" width="500" height="409" /></a><figcaption>Weinre’s debugging interface provides a link to each debuggable target. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07099f1e-8ffc-4934-a1a2-774e37c60447/14-weinre-opt.jpg">View large version</a>)</figcaption></figure>

At this point, you can leverage a lot of WebKit Developer Tools to debug the page. You can use handy tools such as the DOM Inspector:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffc4d391-508d-40ac-96b0-6a2f5a3b431d/15-weinre-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28b37a5a-257c-4ec2-ab28-c5105b153f77/15-weinre-opt-500.jpg" alt="Weinre is debugging iOS with the DOM Inspector" width="500" height="303" /></a><figcaption>Here, Weinre is debugging iOS with the DOM Inspector. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07099f1e-8ffc-4934-a1a2-774e37c60447/14-weinre-opt.jpg">View large version</a>)</figcaption></figure>

Once you get past the initial installation, Weinre lets you debug any device on any network. However, it’s not as powerful as the native solutions for iOS and Android. For example, you can’t use the “Sources” panel to debug JavaScript or take advantage of the profiler.

Note: <a href="https://vanamco.com/ghostlab/">Ghostlab</a> is another remote testing option that supports multiple platforms.</p>

## Conclusion

In this article, we’ve learned how to set up a robust testing suite using a combination of physical devices, emulators, simulators and remote testing tools. With these tools, you are now able to test a mobile website or app across a wide variety of devices and platforms.

We’ve also explored remote debugging tools, which provide useful information directly from a mobile device. Hopefully, you now realize the benefits of remote debugging for mobile. Without it, we’re really just taking stabs in the dark.</p>

### Further Reading

*   “[Mobile Emulators and Simulators: The Ultimate Guide](https://www.mobilexweb.com/emulators),” Maximiliano Firtman
*   “[Introduction to Chrome Developer Tools, Part One](https://www.html5rocks.com/en/tutorials/developertools/part1/),” Seth Ladd, HTML5 Rocks
*   “[About Safari Web Inspector](https://developer.apple.com/library/safari/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/Introduction/Introduction.html),” Safari Developer Library, Apple
*   “[Enable Remote Debugging With Safari Web Inspector in iOS 6](https://moduscreate.com/enable-remote-web-inspector-in-ios-6/),” Dave Ackerman, Modus Create
*   “[Remote Debugging on Android With Chrome](https://developer.chrome.com/devtools/docs/remote-debugging),” Chrome Developer Tools
*   “[Weinre as Remote Debugger](https://developer.mozilla.org/en-US/Firefox_OS/Platform/Gaia/Weinre_As_Remote_Debugger),” Mozilla Developer Network

{{< signature "da, al, ml, il" >}}


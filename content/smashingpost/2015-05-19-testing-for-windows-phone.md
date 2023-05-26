---
title: Testing For And With Windows Phone
slug: testing-for-windows-phone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f9a2f1b-292d-4f64-adec-783cf47fac45/01-nokia-920-opt.jpg
date: 2015-05-19T17:00:59.000Z
author: daniel-herken
description: >-
  Although Windows Phone usage is still low compared with other browsers it's
  sometimes necessary to test your web work for Internet Explorer Mobile. For
  web developers, this could be a complication.
  [Testing](https://www.smashingmagazine.com/2014/09/03/testing-mobile-emulators-simulators-remote-debugging/)
  for the **Windows Phone environment** is not always optional, but it can be a
  chore — especially because the version of [Internet
  Explorer](https://www.smashingmagazine.com/2015/01/26/inside-microsofts-new-rendering-engine-project-spartan/)
  that comes with the Windows Phone can be quirky at best. If you're a developer
  without a Windows Phone device, you might have to get a little creative to
  ensure that your websites are being rendered properly.

  In this article I want to point out a few different tools and techniques which
  can help **test websites for Windows Phone** even if you don't have the real
  device handy or if you are not developing on Windows. But first let's quickly
  look into the differences between mobile and desktop Internet Explorer.
categories:
  - Mobile
  - Testing
  - Devices
  - Windows Phone
---
Although Windows Phone usage is still low <a href="https://www.netmarketshare.com/browser-market-share.aspx?qprid=0&amp;qpcustomd=1">compared with other browsers</a> it's sometimes necessary to test your web work for Internet Explorer Mobile. For web developers, this could be a complication. Testing for the <strong>Windows Phone environment</strong> is not always optional, but it can be a chore — especially because the version of Internet Explorer that comes with the Windows Phone can be quirky at best. If you're a developer without a Windows Phone device, you might have to get a little creative to ensure that your websites are being rendered properly.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4f9a2f1b-292d-4f64-adec-783cf47fac45/01-nokia-920-opt.jpg" alt="Nokia Lumia 920" /><figcaption>The Nokia Lumia 920. (Image credit: <a href="https://www.microsoft.com">Microsoft</a>)</figcaption></figure>

In this article I want to point out a few different tools and techniques which can help test websites for Windows Phone even if you don't have the real device handy or if you are not developing on Windows. But first let's quickly look into the differences between mobile and desktop Internet Explorer.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Where Are The World’s Best Open Device Labs?](https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/)
*   [Open Device Labs: Why Should We Care?](https://www.smashingmagazine.com/2013/05/open-device-labs-why-should-we-care/)
*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)

{{% feature-panel %}}

## IE Mobile Explained

As Microsoft acknowledged in the past, the version of Internet Explorer found on mobile devices is <a href="https://msdn.microsoft.com/en-us/library/ie/dn736066%28v=vs.85%29.aspx">similar but not identical</a> to the desktop browser version. There are a few key features that are not available on Windows Phone:

*   HTML5 touch drag-and-drop support ([demo](https://html5demos.com/drag)).
*   Videos which use the [Encrypted Media Extension](https://msdn.microsoft.com/en-us/library/ie/bg182646(v=vs.85).aspx#eme) will not play on Windows Phone.
*   CSS Touch Views other than `overflow:scroll`
*   [CSS3 hyphenation](https://www.hongkiat.com/blog/css3-hyphenation/) is also not available

These are all rather minor features but you still need to know about the rendering differences and take these into account.</p>

## Testing Tools

Accuracy is not always the most important thing about this kind of testing. During development it's more important to test and iterate quickly than get a pixel-perfect implementation on the first try. But you do need to know how accurate your testing method is so you can plan the final test accordingly.

To help you get a sense of the accuracy of each testing method we'll compare each test tool against the rendering of two websites on a real device (Nokia Lumia 920). For reference, let's see how <a href="https://www.smashingmagazine.com">SmashingMag</a> (responsive) and <a href="https://www.quirksmode.org">Quirksmode</a> (not responsive) render on a real Windows Phone device:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b41be42a-8d94-4e31-a1ff-edd202df9bb1/02-device-rendering-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/34a0aa91-02bb-4b29-9306-5c58ea1bf86a/02-device-rendering-opt-small.png" alt="Rendering on the Nokia Lumia 920" /></a><figcaption>Rendering on the Nokia Lumia 920. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b41be42a-8d94-4e31-a1ff-edd202df9bb1/02-device-rendering-opt.png">View large version</a>)</figcaption></figure>

Later in the article we'll compare the original rendering with the rendering in the test tool to see how accurate the tool is. In the best case, a testing tool will produce the exact same rendering as the real device, with 100% accuracy. Let's dive right in, shall we?

### Internet Explorer Emulation

The fastest and easiest way to test a site for the Windows Phone environment is to use Internet Explorer and its built-in emulator service. Through the developer tools provided in the browser itself, you will be able to run a phone emulation. This includes options such as the browser profile, orientation and screen resolution. You can <strong>flip through settings in real time</strong> to look at different devices and resolutions, and you can complete testing locally on your computer before the site goes live. Furthermore, you can switch between the mobile versions of the website and the desktop version to ensure that none of your changes have affected the way the site looks on the desktop version of Internet Explorer.

Just like the device simulation in Chrome, this sounds like a great idea and an easy solution for quick testing. Most likely you'll need to test for Internet Explorer at some point, so why not integrate Windows Phone into this testing step?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c68961d-be0b-46bc-85ec-4b51bbb38b72/03-mag-ie-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11a14847-8cfd-4f88-94c7-86996bcc7a44/03-mag-ie-opt-small.png" alt="Nokia Lumia (left), IE emulation (right)" /></a><figcaption>Nokia Lumia (left), IE emulation (right). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c68961d-be0b-46bc-85ec-4b51bbb38b72/03-mag-ie-opt.png">View large version</a>)</figcaption></figure>

Unfortunately the rendering results show us that the emulation inside Internet Explorer is <strong>not yet reliable for testing responsive websites</strong>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57d43a9b-bf40-4aa8-a11d-80b26861bef8/04-q-ie-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9865b9e9-7623-4952-a7ea-3f7c0c466995/04-q-ie-opt-small.png" alt="Nokia Lumia (left), IE emulation (right)" /></a><figcaption>Nokia Lumia (left), IE emulation (right). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57d43a9b-bf40-4aa8-a11d-80b26861bef8/04-q-ie-opt.png">View large version</a>)</figcaption></figure>

It seems like the emulation ignores any viewport settings and just resizes the page so it fits the screen. While this is one of the fastest methods of seeing a website in a Windows Phone environment, it's mostly useful for quick checks of websites that are not responsive rather than more comprehensive testing.</p>

### Windows Phone Emulator

For designers who value accuracy more than a lightweight testing option, there is a <a href="https://msdn.microsoft.com/en-us/library/windows/apps/ff402563%28v=vs.105%29.aspx">Windows Phone Emulator</a> available for both Windows Phone 7 and Windows Phone 8. If you are not on Windows the emulators can also be used through a service such as <a href="https://www.browserstack.com">BrowserStack</a>.

The standalone Windows Phone emulator is much better than the emulation embedded into Internet Explorer. The emulator runs a copy of the entire Windows Phone operating system, so you can test native applications alongside your web project. It's the ideal solution for those who simply need to test on that one platform; using the emulator online may be a more comprehensive option for those who need to do a lot of cross-platform testing.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdcd4cde-d4f5-43d9-9683-cf93b9094748/05-mag-emulator-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79d100f0-ed6b-4536-9f2e-829cde631a3f/05-mag-emulator-opt-small.png" alt="Nokia Lumia (left), Windows Phone emulator (right)" /></a><figcaption>Nokia Lumia (left), Windows Phone emulator (right). (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cdcd4cde-d4f5-43d9-9683-cf93b9094748/05-mag-emulator-opt.png">View large version</a>)</figcaption></figure>

As the results show, the Windows Phone emulator is not quite as accurate in rendering as you would hope. In particular, the SVG icons of SmashingMagazine in the top-right <strong>do not work in the emulator, but display as intended on the actual device</strong>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54c27998-a027-4a0b-9600-7248fb4e80cd/06-q-emulator-tops.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/489f94f5-beef-4f85-8b96-5a78c9f0f8d8/06-q-emulator-opt-small.png" alt="Nokia Lumia (left), Windows Phone emulator" /></a><figcaption>Nokia Lumia (left), Windows Phone emulator. (right) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54c27998-a027-4a0b-9600-7248fb4e80cd/06-q-emulator-tops.png">View large version</a>)</figcaption></figure>

The emulator has some system limitations. For instance, the Windows Phone 8 emulator only runs on Windows 8 and higher. For those who have Mac OS X or other operating systems, it's impossible to install and use the emulator directly without using a virtual machine. Using a web-based solution is usually the best option.

As with all emulators, although the emulator provided by Microsoft is likely the most accurate available, it still won't be able to display the site with complete accuracy for each device. Some hardware issues remain that cannot be compensated for by an emulator. Still, the Windows emulator is probably the best emulator that you can find should you want to use a software emulator.</p>

### Real Device

The best method of testing for Windows Phone is undoubtedly testing with a real device. As we've seen, the emulator comes close but is not as accurate as we would like it to be. And, of course, there are certain things that just can't be simulated or emulated. For instance, the user experience might be altered by the way that the user needs to manipulate their touchscreen. When using a real device, most developers will focus on Windows Phone 8 as <a href="https://techcrunch.com/2014/11/27/windows-phone-8-1-finally-breaks-the-50-market-share-threshold/">Windows Phone 7 is already in decline</a>. The browser rendering may also vary depending on device, as the device resolution will differ from mobile device to mobile device.

If you don't want to purchase a dedicated testing device I would recommend you take a look at the services offered by <a href="https://perfectomobile.com">Perfecto Mobile</a>, <a href="https://www.crossbrowsertesting.com">CrossBrowserTesting.com</a> or <a href="https://www.keynote.com/solutions/testing/mobile-testing">DeviceAnywhere</a>, which give you online access to Windows Phone devices among many more. These real devices render just like my testing device so you'll be one the safe side here.

If you want to purchase a testing device you can go with the high-end solution and purchase the most powerful <a href="https://www.microsoft.com/de-de/mobile/smartphone-handy/lumia1520/">Lumia 1520</a>; choose something in the middle like the <a href="https://www.microsoft.com/en/mobile/phone/lumia920/">Lumia 920</a>; or stick to the low end with a <a href="https://www.microsoft.com/en/mobile/phone/lumia430-dual-sim/specifications/">Lumia 430</a>, the cheapest Windows Phone.

## Remote Debugging

Now that you can find all the design bugs, how can you fix them? I find nothing more frustrating than <strong>relying on random guesswork</strong> to fix a bug. Luckily you can use weinre (WEb INspector REmote) to get a decent remote debugger going for Windows Phone. It's similar to <a href="https://developer.chrome.com/devtools/docs/remote-debugging">remote debugging on Android in Chrome</a> but with fewer features.</p>

### Weinre

Weinre is an open source remote debugging tool for debugging websites on a Windows Phone (and any other mobile device, of course). As an open source tool, it is entirely free and more advanced developers can even modify its code. Microsoft even <a href="https://msdn.microsoft.com/en-us/library/windows/apps/ff402563%28v=vs.105%29.aspx">advises developers to use weinre</a> to debug on Windows Phone.

With weinre you are able to inspect the DOM and change it on the fly, allowing for real-time changes. Though the tool does not allow for advanced features like JavaScript debugging -- the entire thing runs on JavaScript, which limits it a little -- it's still an excellent solution for remote testing and debugging.

Using weinre is really easy. It runs on <a href="https://nodejs.org/">Node.js</a>. With two simple commands you can install and start the weinre server. On Windows:

<pre><code class="language-bash">npm -g install weinre
weinre --httpPort 8080 --boundHost -all-
</code></pre>

And on Mac OS X and Linux:

<pre><code class="language-bash">sudo npm -g install weinre
weinre --httpPort 8080 --boundHost -all-
</code></pre>

Weinre will now run at your localhost:8080. To debug your Windows Phone device you need to follow the steps below:

*   Open localhost:8080 on your development machine.
*   In the Target Script section of the website that opens you'll find the `<script>` element you need to add to the website you want to test.
*   Now open the page on your Windows Phone as normal.
*   On your development machine, the developer tools are now available here: localhost:8080/client/#anonymous.

Note that weinre is a debugging tool should never be run in production as this could pose a security risk.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f749c90-2895-4335-a5aa-afb49ff94fb4/07-weinre-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5621b946-2665-476a-9273-b4cb1fb2ef1f/07-weinre-opt-small.png" alt="Web Inspector Remote" /></a><figcaption>Web Inspector Remote. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f749c90-2895-4335-a5aa-afb49ff94fb4/07-weinre-opt.png">View large version</a>)</figcaption></figure>

If you want to use weinre as a development tool, you will need to have the devices that you intend to test for either physically, in the cloud, or emulated. Still, it is an excellent method of testing in real time and should be included in the arsenal of any web developer. The weinre debugging environment can be opened in any major browser.</p>

## What about Windows Phone 10?

As the time of writing no web service offered testing on the beta version of Windows Phone 10, and currently there is no device available which will have it preinstalled. But if you want to test for the upcoming new operating system you can either <a href="https://www.ibtimes.co.uk/how-install-windows-10-technical-preview-phones-any-windows-phone-8-1-device-1488013">update your device</a> to Windows 10 or <a href="https://www.codefoster.com/wponwin10/">run the emulator inside a Windows 10 installation</a> on your desktop machine using the latest Windows Phone SDK and Visual Studio 2013.</p>

## Summary

How does your website look on the Windows Phone platform? Approximately 3% of your mobile users will be using a Windows Phone -- so you may need to make sure that your site renders properly. As we've seen, it's not that easy to test for Windows Phone as all testing tools (even the emulator by Microsoft) don't render that reliably. I suggest going with one of the online services to access the real device as this works rather well. The only downside is that weinre will not work if you don't make your development machine reachable externally.</p>

### Resources

*   [Windows Phone Emulator](https://msdn.microsoft.com/en-us/library/windows/apps/ff402563%28v=vs.105%29.aspx)
*   [CrossBrowserTesting.com](https://www.crossbrowsertesting.com/)
*   [BrowserStack](https://www.browserstack.com/)
*   [Perfecto Mobile](https://perfectomobile.com/)
*   [DeviceAnywhere](https://www.keynote.com/solutions/testing/mobile-testing)
*   "[Test and Debug HTML5 Apps Remotely on Windows Phone 8 Devices](https://visualstudiomagazine.com/articles/2013/06/13/test-and-debug-html5-apps-remotely.aspx)" by Keith Ward in Visual Studio Magazine

{{< signature "da, ml, og" >}}


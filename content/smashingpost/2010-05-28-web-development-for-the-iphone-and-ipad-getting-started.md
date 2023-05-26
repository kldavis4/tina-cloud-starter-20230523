---
title: 'Web Development For The iPhone And iPad: Getting Started'
slug: web-development-for-the-iphone-and-ipad-getting-started
image: null
date: 2010-05-28T10:29:29.000Z
author: nick-francis
description: >-
  According to AdMob, the **iPhone operating system makes up 50% of the worldwide smartphone market**, with the next-highest OS being Android at 24%.
categories:
  - Mobile
  - Apps
  - iOS
  - iPhone
---
Sales projections for the Apple iPad run anywhere from one to four million units in the first year. Like it or not, the iPhone OS, and Safari in particular, have become a force to be reckoned with for Web developers. If you haven't already, it's time to dive in and familiarize yourself with the tools required to optimize websites and Web applications for this OS.

Thankfully, Safari on iPhone OS is a really great browser. Just like Safari 4 for the desktop, it has great CSS3 and HTML5 support. It also has some slick interface elements right out of the box, which sometimes vary between the iPhone and iPad. Lastly, because the iPhone OS has been around for quite some time now, a lot of resources are available.

Please consider reading our related articles:

*   [How To Create Your First iPhone App (2012 Edition)](https://www.smashingmagazine.com/2009/08/how-to-create-your-first-iphone-application/)
*   [iPhone Apps Design Mistakes: Disregard Of Context](https://www.smashingmagazine.com/2009/11/iphone-apps-design-mistakes-disregard-of-context/)
*   [iPhone design mistakes: Over-Design](https://www.smashingmagazine.com/2009/07/21/iphone-apps-design-mistakes-overblown-visuals/ "iPhone design mistakes: Overdesign")
*   [iPhone App Design Trends](https://www.smashingmagazine.com/2009/10/09/iphone-app-design-trends/)
*   [How to Create Your First iPhone Application](https://www.smashingmagazine.com/2009/08/11/how-to-create-your-first-iphone-application/)

I know that most discussion about the iPhone OS platform centers on native applications. But you can still create powerful, native-looking applications using HTML, JavaScript and CSS. This article focuses on <strong>three phases of building and optimizing your website: design, coding and testing.</strong>

{{% feature-panel %}}

Before we get into the three phases, let's look at some of the advantages and disadvantages of building a Web app rather than a native app.

Advantages of building a Web app instead of a native app:

1.  No Apple approval process or red tape, which is especially important given the [terms of service dispute](https://www.develop-online.net/news/34473/Apple-Control-freak-or-quality-catalyst) going on right now.
2.  Optimizing your Web app for other popular platforms like Android and Blackberry with the same code is much easier.
3.  You don't have to learn Objective-C.
4.  If you're charging users, you don't have to share revenue with Apple.
5.  You get 100% control over the means of payment, promotion and distribution to users… which could also be a negative, depending on how you look at it.

Disadvantages of building a Web app instead of a native app:

1.  No presence in the App Store.
2.  Installing the app on a device is a little trickier.
3.  No access to some of the features that are native to the iPhone OS, such as push notification and GUI controls.</p>

## Design

Designing a Web app for this platform is much like designing a native app, so you'll have access to some really great tools. Whether your wireframing tool of choice is pencil and paper or desktop software, you're covered.</p>

### Inspiration

Not many people know that Apple has a "<a title="Apple Web apps" href="https://www.apple.com/webapps/">Web apps</a>" section on its website, which is dedicated to showcasing optimized websites.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52e21644-9e04-40cc-b34c-332c418629aa/apple-webapps.png" alt="Apple Web apps" /><br>
<em>Featured Web app on the Apple website</em>

There are also some galleries elsewhere that showcase the finest in mobile Web design:

*   [Apple Web Apps Listing](https://www.apple.com/webapps/ "Apple Web apps")
*   [Mobile Awesomeness Design Gallery](https://www.mobileawesomeness.com "Mobile Awesomeness")
*   CSS iPhone Design Gallery
*   Well Placed Pixels
*   [Apple App Store](https://www.apple.com/iphone/apps-for-iphone/) (Even though these are native apps, you can find great visual inspiration here.)

### Paper

Paper prototyping has long been my tool of choice for wireframing new ideas or websites. What I really like about the tools below is that they provide perspective on the size and dimensional constraints that you're dealing with. To successfully optimize a Web app for the iPhone OS, you have to cut things out. I suggest keeping the design minimal by wireframing with a sharpie and one of the tools listed below.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4264c716-cc85-4014-b69b-c56979333c33/notepod.jpg" alt="Notepod" /><br>
<em><a title="Notepod" href="https://notepod.net/">Notepod</a> is great for sketching out rough ideas for the iPhone and iPad.</em>

*   [Notepod: iPad and iPhone sketchbooks](https://notepod.net/ "Notepod")
*   [App Sketchbook](https://appsketchbook.com/ "App Sketchbook")
*   [PixelPads](https://www.pixelpads.com/PixelPads_I_Features.html "PixelPads")
*   [UI Stencils sticky pads](https://www.uistencils.com/products/iphone-sticky-pad)
*   [Apress iPhone Application Sketch Book](https://apress.com/book/view/9781430228233)
*   Printable iPhone Wireframe Template (free)

### Digital

Once you know exactly how things will lay out in your design, we can move to the desktop and get specific. I really like wireframing with <a title="OmniGraffle for Mac" href="https://www.omnigroup.com/products/omnigraffle/">OmniGraffle</a>, but sometimes diving straight into Photoshop makes sense. Either way, these tools are a <em>huge</em> help in making it happen.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8d80bd6-70fe-453b-9b2e-486e863d62f2/ipad-gui.jpg" alt="iPad GUI" /><br>
<em>iPad GUI preview from Teehan + Lax.</em>

*   iPhone GUI PSD 3.0 and iPad GUI PSD (Photoshop)
*   [Layered iPhone GUI elements](https://www.designerstoolbox.com/designresources/iphone/) (Photoshop), from Designer's Toolbox
*   [PSD Vector Kit](https://www.smashingmagazine.com/2008/11/26/iphone-psd-vector-kit/) (Photoshop), from Smashing Magazine
*   iPad and iPhone stencils; see more at [Graffletopia](https://graffletopia.com/categories/iphone "Graffletopia") (OmniGraffle)
*   [iPhone and iPad Development GUI Kits, Stencils and Icons](https://speckyboy.com/2010/04/30/iphone-and-ipad-development-gui-kits-stencils-and-icons/)

<strong>Hungry for more?</strong> <a title="21 Prototyping, Mockup, and Wireframing Tools for iPhone App Development" href="https://iphoneized.com/2009/11/21-prototyping-mockup-wireframing-tools-iphone-app-development/">This article</a> has a good rundown of additional design tools.</p>

## Coding

When you start coding for Safari on the iPhone OS, understanding how the browser works is important. Also, there are subtle differences in the iPhone and iPad's browsers, such as how form-select boxes work. Most importantly, Safari has great CSS3 and HTML5 support, so you can use modern code without having to worry about cross-browser compatibility.</p>

### Education

Apple actually does a really good job of documenting Safari for the iPhone OS. The only shortcomings in my opinion are a lack of help with browser detection and window orientation. Read each of the articles below for everything you need to know about coding for this browser.

<a href="https://developer.apple.com/safari/library/documentation/InternetWeb/Conceptual/iPhoneWebAppHIG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007900">iPhone Human Interface Guidelines for Web Applications</a>
This is a good overall summary of how Safari for the iPhone OS works. It's certainly worth scanning through, because it has some good advice, although no specific coding examples.

<a title="iPad Human Interface Guidelines" href="https://developer.apple.com/iphone/library/documentation/General/Conceptual/iPadHIG/Introduction/Introduction.html">iPad Human Interface Guidelines</a>
This document does a good job of distinguishing iPhone elements and iPad elements. This is also worth scanning through, because it has some great advice on designing for the iPad.

<a href="https://developer.apple.com/safari/library/documentation/AppleApplications/Reference/SafariWebContent/Introduction/Introduction.html#//apple_ref/doc/uid/TP40002079-SW1">Safari Web Content Guide</a>
This document gets specific about the viewport, webclip icons, unique meta tags and event handling, among many other topics. Code examples are provided. I recommend reading it cover to cover before getting started.

<a href="https://developer.apple.com/safari/library/technotes/tn2010/tn2262.html">Preparing Your Web Content for the iPad</a>
This document provides tips on testing your website on the iPad, but its discussion on browser detection isn't as detailed as I would like.

Browser Detection
David Walsh provides good examples of proper browser detection <a title="iPad Detection Using JavaScript or PHP" href="https://davidwalsh.name/detect-ipad">for the iPad</a> and <a href="https://davidwalsh.name/detect-iphone">for the iPhone</a> on his blog. Options for PHP and Javascript are included.

<a title="Nettuts" href="https://net.tutsplus.com/tutorials/tools-and-tips/learn-how-to-develop-for-the-iphone/">Detecting iPhone Window Orientation</a>
This iPhone development tutorial from Nettuts provides a good example of how to vary style sheets according to the iPhone's orientation.

Detecting iPad Window Orientation
Detecting iPad's window orientation is <em>much</em> easier. Here's what the code looks like (no JavaScript required):

<pre><code class="language-markup tmp-xml">&lt;link rel="stylesheet" media="all and (orientation:portrait)" href="portrait.css"&gt;
&lt;link rel="stylesheet" media="all and (orientation:landscape)" href="landscape.css"&gt;</code></pre>

### jQTouch Mobile Framework

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62f6158d-a32a-4afc-bb24-a831816a4445/jqtouch.jpg" alt="jQTouch" />

While the iPhone has a few mobile development frameworks, jQTouch is far and away the best. jQTouch gives you all of the tools to make your mobile Web app look and feel like a native one. <a title="jQTouch—jQuery plugin for mobile web development" href="https://jqtouch.com/">Visit the website</a>, and go to the <a title="jQTouch β" href="https://jqtouch.com/preview/demos/main/">demo website</a> from your iPhone to get a feel for it.

My only complaint when building my first website with jQTouch was a lack of documentation and tutorials. I had to figure it out by playing with the demo website's code. Here are some jQTouch articles that proved helpful in coding my first website:

*   jQTouch Wiki on Google Code
*   [Building iPhone Apps with HTML, CSS and JavaScript, Chapter 4: Animation](https://building-iphone-apps.labs.oreilly.com/ch04.html)
*   PDF slides about getting started with jQTouch, by Philipp Bosch

## Testing

A crucial and somewhat tricky part of building a website or Web app for the iPhone OS is testing. It's a little more complicated than testing in a web browser, but familiarizing yourself with a couple of tools should make the process simple.</p>

### Liveview

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3774827-f316-4a4f-bc49-19ae06a961d1/liveview.jpg" alt="Liveview" />

<a title="LiveView for iPhone" href="https://www.zambetti.com/projects/liveview/">Liveview</a> is a really clever testing tool for when your app is in the design or initial coding phase. It allows you to broadcast an image from your desktop onto your phone so that you can see what it looks like. This is useful for getting text size and the visual specifics just right, because sometimes visualizing from Photoshop is hard.</p>

### Using the iPhone Simulator

In my opinion, no good iPhone or iPad emulators are available. The ones that are available are a waste of time. Much better is to download the <a href="https://daw.apple.com/cgi-bin/WebObjects/DSAuthWeb.woa/wa/login?appIdKey=D635F5C417E087A3B9864DAC5D25920C4E9442C9339FA9277951628F0291F620&amp;path=%2F%2Fiphone%2Findex.action">latest version of the SDK</a> and use Apple's official iPhone OS simulator, which of course supports the iPad as well.

Setting up the SDK and a local testing environment takes a few minutes but is well worth the effort, rather than depending on unofficial and often inaccurate emulators. I've written a step-by-step tutorial about <a title="Project83 Blog" href="https://www.project83.com/blog/how-to-test-iphone-websites-locally-with-the-iphone-simulator/">setting up a local testing environment</a> that's worth a read. One great thing about local testing is that it's faster and does not require an Internet connection. I highly recommend going this route until you are ready to launch.</p>

## PhoneGap: Best Of Both Worlds?

<strong>PhoneGap is a game-changer for Web developers.</strong> If you would rather create your app in HTML, CSS and JavaScript but want it to run natively and have it be available in the App Store, then <a title="PhoneGap" href="https://phonegap.com/">PhoneGap is the solution</a>. It's an open-source development tool that not only compiles your code for native use on the iPhone OS but also works for Android, Palm, Symbian, Windows Mobile and Blackberry devices.

PhoneGap also steers clear of the recently controversial 3.3.1 clause of Apple's terms of service. In other words, apps compiled with PhoneGap will still be approved. Check out the list of apps that are built with PhoneGap to learn more.</p>

## Feeling Overwhelmed?

If you are, then some good hosted services will make it easier to optimize your website for multiple platforms without having to start from scratch. There are various levels of flexibility available, but all the services use a WYSIWYG-like editor to help you create mobile websites on the fly. Depending on your Web app and client, one of the following may be a good fit:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/092cec00-de5d-4f63-ae6c-c2d361895621/mobify.png" alt="Mobify" /><br>
<em><a href="https://www.mobify.me/">Mobify</a> is a great alternative if you don't care to build from scratch.</em>

*   [Mobify](https://www.mobify.me/) (which powers [Smashing Magazine's mobile website](https://m.smashingmagazine.com "Smashing Magazine Mobile"))
*   [Wapple](https://wapple.net/)
*   [Mofuse](https://www.mofusepremium.com/)
*   Mobi10

## Conclusion

It's a great day to be a Web developer, because non-desktop platforms like the iPhone OS open up greater possibilities for us to express our creativity and entrepreneurial savvy, while allowing us to adhere to modern Web standards. All of the tools you need to create great a Web experience on the platform that's currently dominating the mobile space are out there. It's up to you to make the most of them!

{{< signature "al" >}}


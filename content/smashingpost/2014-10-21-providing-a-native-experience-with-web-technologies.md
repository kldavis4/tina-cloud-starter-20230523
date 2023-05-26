---
title: 'Hybrid Mobile Apps: Providing A Native Experience With Web Technologies'
slug: providing-a-native-experience-with-web-technologies
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63359009-cca5-43fe-bc88-c928d5dbac4d/01-html-baby-opt.jpg
date: 2014-10-21T17:00:41.000Z
author: patrick-rudolph
description: >-
  According to a recent report, HTML is the most widely used language for mobile
  app developers. The main reasons among developers for selecting web
  technologies is cross-platform portability of code and the low cost of
  development. We’ve also heard that hybrid apps tend to be sluggish and poorly
  designed. Let’s prove whether it’s possible to deliver the native look and
  feel that we’re used to.

  This article provides many **hints, code snippets and lessons learned** on how
  to build great hybrid mobile apps. I’ll briefly introduce hybrid mobile app
  development, including its benefits and drawbacks. Then, I’ll share lessons
  I’ve learned from over two years of developing Hojoki and CatchApp, both of
  which run natively on major mobile platforms and were built with HTML, CSS and
  JavaScript. Finally, we’ll review the most prominent tools to wrap code in a
  native app.
categories:
  - Mobile
  - Apps
  - Development
  - UX
---
According to a <span class="removed_link" title="https://www.visionmobile.com/product/developer-economics-q3-2014/">recent report</span>, HTML is the most widely used language for mobile app developers. The <span class="removed_link" title="https://www.visionmobile.com/product/developer-economics-2013-the-tools-report/">main reasons among developers for selecting web technologies</span> are cross-platform portability of code and the low cost of development. We’ve also heard that hybrid apps tend to be sluggish and poorly designed. Let’s prove whether it’s possible to deliver the native look and feel that we’re used to.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63359009-cca5-43fe-bc88-c928d5dbac4d/01-html-baby-opt.jpg" alt="HTML can do that." width="500" height="263" /></figure>

This article provides many <strong>hints, code snippets and lessons learned</strong> on how to build great hybrid mobile apps. I’ll briefly introduce hybrid mobile app development, including its benefits and drawbacks. Then, I’ll share lessons I’ve learned from over two years of developing Hojoki and CatchApp, both of which run natively on major mobile platforms and were built with HTML, CSS and JavaScript. Finally, we’ll review the most prominent tools to wrap code in a native app.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [What Every App Developer Should Know About Android](https://www.smashingmagazine.com/2014/10/what-every-app-developer-should-know-about-android/)
*   [How To Design For Android](https://www.smashingmagazine.com/2011/06/designing-for-android/)
*   [<span class="headline">Designing For A Maturing Android</span>](https://www.smashingmagazine.com/2013/05/brave-new-world-designing-for-a-maturing-android/)
*   [How To Design For Android Tablets](https://www.smashingmagazine.com/2011/08/designing-for-android-tablets/)

{{% feature-panel %}}

## What Are Hybrid Mobile Apps?

Mobile apps can be generally broken down into native, hybrid and web apps. Going the native route allows you to use all of the capabilities of a device and operating system, with a minimum of performance overhead on a given platform. However, building a web app allows your code to be ported across platforms, which can dramatically reduce development time and cost. Hybrid apps combine the best of both worlds, using a common code base to deploy native-like apps to a wide range of platforms.

There are two approaches to building a hybrid app:

*   **WebView app**.  The HTML, CSS and JavaScript code base runs in an internal browser (called WebView) that is wrapped in a native app. Some native APIs are exposed to JavaScript through this wrapper. Examples are Adobe PhoneGap and [Trigger.io](https://www.trigger.io).
*   **Compiled hybrid app**.  The code is written in one language (such as C# or JavaScript) and gets compiled to native code for each supported platform. The result is a native app for each platform, but less freedom during development. Examples are [Xamarin](https://xamarin.com/), [Appcelerator Titanium](https://www.appcelerator.com/titanium/) and <span class="removed_link" title="https://www.embarcadero.com/products/rad-studio/fmx">Embarcadero FireMonkey</span>.

While both approaches are widely used and exist for good reasons, <strong>we’ll focus on WebView apps</strong> because they enable developers to leverage most of their existing web skills. Let’s look at all of the benefits and drawbacks of hybrid apps compared to both native and mobile web apps.</p>

### Benefits

*   Developer can use existing web skills
*   One code base for multiple platforms
*   Reduced development time and cost
*   Easily design for various form factors (including tablets) using responsive web design
*   Access to some device and operating system features
*   Advanced offline capabilities
*   Increased visibility because the app can be distributed natively (via app stores) and to mobile browsers (via search engines)

### Drawbacks

*   Performance issues for certain types of apps (ones relying on complex native functionality or heavy transitions, such as 3D games)
*   Increased time and effort required to mimic a native UI and feel
*   Not all device and operating system features supported
*   Risk of being rejected by Apple if app does not feel native enough (for example, a simple website)

These drawbacks are significant and cannot be ignored, and they show that the hybrid approach does not suit all kinds of apps. You’ll need to carefully evaluate your target users, their platforms of choice and the app’s requirements. In the case of many apps, such as content-driven ones, the benefits outweigh the drawbacks. Such apps can typically be found in the “Business and Productivity,” “Enterprise” and “Media” categories in the app store.

Both Hojoki and CatchApp are very content-driven productivity apps, so we initially thought they would be a great match for hybrid development. The first three benefits mentioned above were especially helpful to us in building the mobile app for Hojoki in just four weeks. Obviously, that first version lacked many important things. The following weeks and months were filled with work on optimizing performance, crafting a custom UI for each platform and exploiting the advanced capabilities of different devices. The learning in that time was crucial to making the app look and feel native. I’ll share as many lessons as possible below.

So, <strong>how do you achieve a native look and feel</strong>? To a mobile web developer, being able to use the features of a device and operating system and being able to package their app for an app store sounds just awesome. However, if users are to believe it is a native app, then it will have to behave and look like one. Accomplishing this remains one of the biggest challenges for hybrid mobile developers.</p>

## Make Your Users Feel at Home

A single code base doesn’t mean that the app should look and feel exactly the same on all platforms. Your users will not care at all about the underlying cross-platform technology. They just want the app to behave as expected; they want to feel “at home.” Your first stop should be each platform’s design guidelines:

*   “[iOS Design Resources](https://developer.apple.com/library/ios/navigation/),” iOS Developer Library
*   “[Android Design](https://developer.android.com/design/index.html),” Android Developers
*   “[Design](https://dev.windowsphone.com/design),” Windows Dev Center

While these guidelines might not perfectly suit all kinds of apps, they still provide a comprehensive and standard set of interfaces and experiences that users on each platform will know and expect.</p>

### DIY vs. UI Frameworks

Implementing all of these components, patterns and animations on your own can be quite a challenge. All kinds of frameworks exist to help you with that, ranging from commercial (<a href="https://www.telerik.com/kendo-ui">Kendo UI</a>) to open-source ones (<a href="https://ionicframework.com/">Ionic</a>) and from ones with a common UI (<a href="https://jquerymobile.com/">jQuery Mobile</a> and <a href="https://onsenui.io/">Onsen UI</a>) to many platform-specific UIs (<a href="https://www.sencha.com/products/touch/">Sencha Touch</a> and <a href="https://chocolatechip-ui.com/">ChocolateChip-UI</a>). Some are really good at providing a pixel-perfect layout, while others are rather sloppy, thus making it easy for the user to identify a web app. However, my impression is that their main drawbacks are performance-related, because most UI frameworks try to be as all-embracing as possible. Judge for yourself by taking a few minutes to try the demos on your own device.

At Hojoki, we try to craft all components on our own using CSS3 and minimal JavaScript. This keeps us in control of performance and reduces overhead. We obviously use small libraries for complicated tasks that someone else has solved just fine.</p>

### Custom UI Components

Custom UI components also have many good use cases. Deciding between a platform’s UI and a custom UI will obviously depend on your target audience. If you want to do your own thing, you should have a deep understanding of UX design, because the guidelines linked to above were crafted by experts to meet the particular requirements of their platform’s users.

Whether you stick to a platform’s UI guidelines or do your own thing with custom components, know that there are certain design patterns that most people use every day and love. How are people usually introduced to a new app? Through a slideshow walkthrough or an instructional overlay. How do people navigate? With a tab bar or a <a href="https://github.com/jakiestfu/Snap.js">sidebar drawer</a>. How do users quickly load or refresh data? By pulling to refresh. (Native-like scrolling will be covered extensively further below.)

### Resources for Mobile UI Design

*   “[Mobile UI Design Patterns: 10+ Sites for Inspiration](https://sixrevisions.com/user-interface/mobile-ui-design-patterns-inspiration/),” Jacob Gube, Six Revisions
*   “<span class="removed_link" title="https://c2prods.com/2013/cloning-the-ui-of-ios-7-with-html-css-and-javascript/">Cloning the UI of iOS 7 With HTML, CSS and JavaScript</span>,” Côme Courteault
*   “[Tapping Into Mobile UI With HTML5](https://de.slideshare.net/yaelsahar/tapping-into-mobile-ui-with-html5)” (slides), Luke Melia and Yael Sahar, Slideshare

## Design A Native-Looking Header Bar

One important part of a UI is the header bar, with its title and navigation elements, most notably the “up” and “back” buttons. To me, many popular frameworks fail to provide a HTML and CSS solution that compares to a native app. Mimicking this part of the UI with a minimal DOM and a few lines of CSS for each platform is actually fairly easy:

<pre><code class="language-markup">
&lt;header&gt;
   &lt;button class="back"&gt;Feed&lt;/button&gt;
   &lt;h1&gt;Details&lt;/h1&gt;
   &lt;!-- more actions (e.g. a search button on the right side) --&gt;
&lt;/header&gt;
</code></pre>

Check out the full code of the <a href="https://jsfiddle.net/prud/dnebx02p/">native-looking header bar for iOS, Android and Windows Phone</a> on JSFiddle. This is my result:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/60814211-f0e6-4bf6-97ef-a0e1c3425c55/02-html-header-new-opt.png" alt="Native-looking headers made with HTML5 and CSS." width="320" height="220" /><br>
<figcaption>Native-looking headers made with HTML5 and CSS.</figcaption></figure>

Using the same DOM across all platforms is generally preferable because it results in cleaner code and, therefore, maximizes maintainability. I’ve found this to be easily possible for many UI components on iOS and Android (including the header bar, tab bar, custom navigation menu, settings page, popover and many more). However, this becomes much harder when adding support for Windows Phone, which comes with some very different design patterns.

## Support High-Resolution Screens

Nowadays, smartphones and tablets with high-resolution screens make up the vast majority of mobile devices, making up <a href="https://david-smith.org/iosversionstats/#retina">more than 80% of iOS devices</a> and <a href="https://developer.android.com/about/dashboards/index.html#Screens">over 70% on Android devices</a>. To make your images look crisp for everyone, you usually have to deliver twice the dimensions than what is actually shown in your app. Serving properly sized images for all different resolutions is one of the most discussed topics in responsive web design. There are various approaches, each with its benefits and drawbacks related to bandwidth, code maintainability and browser support. Let’s quickly review the most popular ones, in no particular order:

*   server-side resizing and delivering
*   client-side detection and replacement via JavaScript
*   HTML5 `picture` element
*   HTML5 `srcset` attribute
*   CSS `image-set`
*   CSS media queries
*   Resolution-independent images (SVG)

As always, there is no silver bullet for responsive images. It pretty much depends on the type of images and how they are used in the app. For static images (such as the logo and tutorial images), I try to use SVG. They scale perfectly without any extra effort and have <a href="https://caniuse.com/#feat=svg">great browser support as long as you’re fine with Android 3+</a>.

When SVG is not an option, the <a href="https://responsiveimages.org/">HTML5 <code>picture</code> element and <code>srcset</code> attributes</a> are definitely where front-end development is heading. Currently, their main drawback is the very limited browser support and, therefore, their need for polyfills.

In the meantime, <a href="https://www.uifuel.com/hd-retina-display-media-queries/">CSS background images and media queries</a> are the most pragmatic solution:

<pre><code class="language-css">
/* Normal-resolution CSS */
.logo {
   width: 120px;
   background: url(logo.png) no-repeat 0 0;
}

/* HD and Retina CSS */
@media
only screen and (-webkit-min-device-pixel-ratio: 1.25),
only screen and ( min--moz-device-pixel-ratio: 1.25),
only screen and ( -o-min-device-pixel-ratio: 1.25/1),
only screen and ( min-device-pixel-ratio: 1.25),
only screen and ( min-resolution: 200dpi),
only screen and ( min-resolution: 1.25dppx) {
	.logo {
      background: url(logo@2x.png) no-repeat 0 0;
      background-size: 120px; /* Equal to normal logo width */
   }
}
</code></pre>

However, your app might already contain a lot of content (such as news articles), and adjusting all of the <code>img</code> tags or replacing them with CSS would be exhausting. A server-side solution is the best choice in this case.

Starting last year, more and more Android manufacturers have gone one step further with what is called XXHDPI (or very very high-resolution) screens. Whichever solution above fits your need, keep in mind that you’ll need images that are three times the original dimensions to support Android’s latest flagship devices.</p>

## Use System Fonts

A simple yet important way to make users feel at home is to use system fonts.</p>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd913a79-7e24-4856-a124-ea59d9341581/03-native-fonts-new-opt.png" alt="Native fonts for iOS, Android and Windows Phone." width="400" height="200" /><br>
<figcaption>Native fonts for <a href="https://iosfonts.com/">iOS</a>, <a href="https://developer.android.com/design/style/typography.html">Android</a> and <a href="https://msdn.microsoft.com/library/windows/apps/hh700394.aspx#ux_font_choice">Windows Phone</a>.</figcaption></figure>

These are my recommended font stacks on the major platforms:

<pre><code class="language-css">
/* iOS */
font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;

/* Android */
font-family: 'RobotoRegular', 'Droid Sans', sans-serif;

/* Windows Phone */
font-family: 'Segoe UI', Segoe, Tahoma, Geneva, sans-serif;
</code></pre>

Furthermore, iOS 7 offers some interesting presets that automatically set the correct font family, font size and line height. It’s as easy as using <code>font: -apple-system-body</code> for normal text and <code>font: -apple-system-headline</code> for headings. This not only simplifies font declarations, but also improves accessibility through “<a href="https://support.apple.com/kb/HT5956">dynamic type</a>,” Apple’s system-wide font-size setting. You can dig deeper into iOS 7 font presets in a <a href="https://mir.aculo.us/2013/09/16/how-to-create-a-web-app-that-looks-like-a-ios7-native-app-part-1/">post by Thomas Fuchs</a>.</p>

## An Icon Is Worth A Thousand Words

Iconography is an important part of the user experience on all major mobile platforms. As with fonts, you’re usually best off using icons that your target audience already knows. Recalling what I said about high-resolution screens earlier, make sure that your icons are scaleable. Implementing them as a font via CSS’ <code>@font-face</code> rule is a great way to achieve this, and it comes with <a href="https://caniuse.com/#feat=fontface">wide browser support</a>. It even allows you to change an icon’s appearance (for example, its color, shadow and transparency) seamlessly via CSS. Here are my recommendations:

1.  **Get various platform icon fonts.** [Ionicons](https://ionicons.com/) is our baseline set because it includes nearly everything we need. This includes specific icons for iOS and Android in addition to their general ones. The rest come from specific platform icon fonts for [iOS](https://ios7-icon-font-demo.herokuapp.com/), Android [set 1](https://www.spiderflyapps.com/downloads/android-developer-icons-the-font/) and [set 2](https://github.com/Turbo87/Android-Action-Bar-Icon-Pack-Font) and [Windows Phone](https://modernuiicons.com/).
2.  **Combine them with a icon font generator.** Using multiple icon fonts is confusing and quickly adds up in size. That is why we use [Fontello](https://fontello.com/) to combine the different sets, adjust key codes and export them for each platform. The result is `<span class="icon">s</span>`, which looks like a search icon on iOS, Android and Windows Phone. Also, check out the popular alternatives [IcoMoon](https://icomoon.io/app) and [Fontastic](https://fontastic.me/).

On Windows Phone, you can also <a href="https://msdn.microsoft.com/library/windows/apps/jj841126.aspx">get away with the native <code>font-family: 'Segoe UI Symbol'</code></a>.</p>

## Optimize For Performance

Performance is usually considered to be one of the major disadvantages of a hybrid mobile app. This is mostly true if your app has a lot of heavy animations, contains huge scrolling lists and needs to run on old devices. However, if you are all right with supporting only newer platform versions (Android 4+, iOS 7+ and Windows Phone 8+), then you’ll very likely have satisfying results. It’s ultimately a question of how much effort you put into optimizing DOM and CSS selectors, writing performant JavaScript, reducing rendering time and minimizing the number of reflows and repaints. An endless number of articles and tutorials cover mobile web performance. These are some of my favorites:

*   “[Performance and UX Considerations for Successful PhoneGap Apps](https://www.tricedesigns.com/2013/03/11/performance-ux-considerations-for-successful-phonegap-apps/),” Andrew Trice
*   “[Mobile: Web Performance](https://estelle.github.io/mobileperf/)” (slides), Estelle Weyl
*   “[Writing Fast, Memory-Efficient JavaScript](https://www.smashingmagazine.com/2012/11/05/writing-fast-memory-efficient-javascript/),” Addy Osmani, Smashing Magazine
*   “[Minimizing Browser Reflow](https://developers.google.com/speed/articles/reflow),” Lindsey Simon, Google Developers
*   “[How to Make Your Website Faster on Mobile Devices](https://www.smashingmagazine.com/2013/04/03/build-fast-loading-mobile-website/),” Johan Johansson, Smashing Magazine

Beyond that, mobile hardware and rendering engines are improving at a rapid pace, with new devices coming out every other day. Developers can make the performance of a hybrid WebView app difficult to distinguish from that of a fully native app on the iPhone 5 series and on Android phones comparable to Nexus 4 and 5.</p>

## Increase Perceived Speed

Building a performant app is one thing, but making it <em>feel</em> fast is a whole other. Whether your app needs some time for a certain task (such as some heavy calculation or client-server communication), presenting instant feedback is crucial to providing a fluid and responsive experience. A common technique is to delay tasks that the user doesn’t need yet, while predicting and preloading the steps the user might take next. A famous example is Instagram, which <a href="https://www.cultofmac.com/164285/the-clever-trick-instagram-uses-to-upload-photos-so-quickly/">uploads photos in the background</a> while the user is busy adding tags and sharing. Perceived speed can be very different from actual speed, so let’s use it in our favor. Here are some no-brainers.</p>

### Remove the Click Delay on Touch Devices

A normal JavaScript click event handler on a touch device comes with a slight delay between the touchstart and the click being fired (usually around 300 milliseconds). This feature is built into the browser to detect whether the user is performing a single- or double-tap. If you don’t need the “double-tap to zoom” feature, you can safely eliminate these 300 milliseconds to get a much more responsive tap behavior. My favorite solution for this is the <a href="https://github.com/ftlabs/fastclick">FastClick</a> library. Use it on everything except Internet Explorer:

<pre><code class="language-javascript">
if ('ontouchstart' in window) {
   window.addEventListener('load', function() {
      FastClick.attach(document.body);
   }, false);
}
</code></pre>

Internet Explorer 10+ is a bit easier. You just need some CSS:

<pre><code class="language-css">
html {
   -ms-touch-action: manipulation; /* IE 10  */
       touch-action: manipulation; /* IE 11+ */
}
</code></pre>

### Style the Active State

As soon as the user taps an actionable element such as a button or a link, they should immediately get some kind of feedback that the app has detected their action. While the CSS pseudo-class <code>:hover</code> works great for this on the desktop, you need to switch to <code>:active</code> or a JavaScript solution for it to work on mobile. I’ve compared the three <a href="https://jsfiddle.net/prud/x9y6cfhg/">approaches to the active state</a> on JSFiddle. While they all work one way or another, you judge which is best for you.

Furthermore, remove the default tap highlight while adjusting your active states on mobile. I’d also recommend disabling user selections on actionable elements, because the selection menu would be quite disruptive if the user accidentally taps the button for too long.</p>

<strong>iOS and Android:</strong>

<pre><code class="language-css">
button {
   outline: 0;
   -webkit-tap-highlight-color: rgba(0,0,0,0);
   -webkit-tap-highlight-color: transparent;
   -webkit-touch-callout: none;
   -webkit-user-select: none;
      -moz-user-select: none;
       -ms-user-select: none;
           user-select: none;
}
</code></pre>

<strong>Windows Phone 8+:</strong>

<pre><code class="language-markup">
&lt;meta name="msapplication-tap-highlight" content="no"&gt;
</code></pre>

### Indicate Loading

Whenever your app is performing an action that will take some time to finish, even just for a second, consider adding a loading indicator. If you don’t, users will think that your app freezes occasionally, or they’ll click around when they shouldn’t, or they might even break things and then blame your app. From what I’ve experienced, animated GIFs are usually a bad idea in mobile browsers. As soon as there is a load on the CPU, the GIF freezes, thus defeating its entire purpose. I prefer <a href="https://fgnass.github.io/spin.js/">Spin.js</a> for its configurability and ease of use. Also, check out some other <a href="https://www.queness.com/post/9150/9-javascript-and-animated-gif-loading-animation-solutions">JavaScript solutions</a> and <a href="https://tympanus.net/codrops/2012/11/14/creative-css-loading-animations/">CSS loaders</a>.

Cross-platform tools like PhoneGap and Trigger.io also provide access to native loaders, which is great for showing a full-screen loading animation.</p>

## Get the Scrolling Right

Scrolling is one of the most important factors in the user experience of many apps. This is both a curse and a blessing because the success of its implementation will depend heavily on the scrolling niceties that your app relies on and on the mobile operating systems that need to be supported.

Scrollable content and a fixed header and/or footer bar are common to nearly all apps. There are two common approaches to achieving this with CSS:

1.  Enabling scrolling on the `body`, and applying `position: fixed` to the header;
2.  Disabling scrolling on the `body`, and applying `overflow: scroll` to the content;
3.  Disabling scrolling on the `body`, and applying JavaScript custom scrolling to the content.

While the first option has some benefits (such as iOS’s native scroll-to-top action and a simple code structure), I highly recommend going with the second option, <code>overflow: scroll</code>. It has <a href="https://remysharp.com/2012/05/24/issues-with-position-fixed-scrolling-on-ios/">fewer rendering issues</a> (although still a lot), and browser support is great on modern platforms (Android 4+, iOS 5+ and Windows Phone 8+), with a nice little <a href="https://github.com/filamentgroup/Overthrow#browser-support">polyfill for some older ones</a>. Alternatively, you could replace <code>overflow: scroll</code> with a custom scrolling library (the third option), such as <a href="https://iscrolljs.com/">iScroll</a>. While these JavaScript solutions allow for more flexibility with features (for example, the scroll position during momentum, event handling, customization of effects and scrollbars, etc.), they always penalize performance. This becomes critical when you’re using a lot of DOM nodes and/or CSS3 effects (such as <code>box-shadow</code>, <code>text-shadow</code>, <code>opacity</code> and <code>rgba</code>) in the content area.

Let’s look at some of the basic scrolling features.</p>

### Momentum Effect

The touch-friendly momentum effect enables users to quickly scroll through large content areas in an intuitive way. It can be easily activated with some simple CSS on iOS 5+ and in some versions of Chrome for Android. On iOS, this will also enable the content to bounce off the top and bottom edges.</p>

<pre><code class="language-css">
overflow-y: scroll;
-webkit-overflow-scrolling: touch;
</code></pre>

### Pull Down to Refresh

Various solution for this are available on the web, such as the one by <a href="https://damien.antipa.at/2012/10/16/ios-pull-to-refresh-in-mobile-safari-with-native-scrolling/">Damien Antipa</a>. While the solutions for iOS and Windows Phone have a similar look and feel, Android recently introduced its own mechanism (see below). We’ve implemented this in CatchApp using some JavaScript and CSS keyframes. (I have yet to wrap it up nicely and put it on GitHub, so stay tuned!)

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/817615ed-93c0-44cd-970a-7a737de8dccb/04-pull-ios-opt.jpg" alt="Pull down to refresh on iOS" width="367" height="162" /><br>
<figcaption>Pull down to refresh on iOS. (Image credit: <a href="https://damien.antipa.at/2012/10/16/ios-pull-to-refresh-in-mobile-safari-with-native-scrolling/">Damien Antipa</a>)</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e674f65c-fda3-4c40-9307-9dfba6696b1f/06-pull-android-opt.jpg" alt="Pull down to refresh on Android." width="367" height="236" /><br>
<figcaption>Pull down to refresh on Android. (Image credit: <a href="https://androidwidgetcenter.com/android-tips/how-to-refresh-gmail-on-android/">Android Widget Center</a>)</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f79a9d7-b176-4263-92bf-f6462af36def/05-pull-wp-opt.gif" alt="Pull down to refresh on Windows Phone." width="367" height="376" /><br>
<figcaption>Pull down to refresh on Windows Phone. (Image credit: <a href="https://dwcares.com/pull-to-refresh-2/">David Washington</a>)</figcaption></figure>

### Scroll to Top

Unfortunately, disabling scrolling on the <code>body</code> will also break iOS’ native feature that enables users to quickly get to the top of the page by tapping the status bar. I’ve written a small script that can be added to any element and that takes care of <a href="https://github.com/prud/ios-overflow-scroll-to-top">scrolling to the top using JavaScript</a>, even if the content is currently in momentum. Add it to the header of your mobile website or to the status bar with a native plugin (for example, in PhoneGap).

Many other scrolling features could be implemented on top of the native <code>overflow: scroll</code>, such as snapping to a certain element or just infinite scrolling. If your requirements are more advanced, definitely look at the JavaScript options out there.</p>

## Make It Easy To Hit Stuff

When performing a touch action, users will quite often miss their target by a few pixels, especially on small buttons (such as the ones in iOS’ top bar). Developers can assist users while keeping the design elegant by enabling an invisible touch area around small targets:

<pre><code class="language-markup">
&lt;button&gt;
   &lt;div class="innerButton"&gt;Click me!&lt;/div&gt;
&lt;/button&gt;
</code></pre>

You’ll have to put the event handler on the button element, while restricting the styles to <code>div.innerButton</code>. Check out the <a href="https://jsfiddle.net/prud/r7kqr1a3/">full example, including CSS</a>, on JSFiddle.</p>

## Using Touch Gestures

A smartphone is all about touching and gestures. We swipe, pinch, zoom, drag and long-tap all the time when interacting with touch devices. So, why not offer users the same means of controlling your hybrid app? <a href="https://quojs.tapquo.com/">QuoJS</a> and <a href="https://hammerjs.github.io/">Hammer.js</a> are well-known libraries for supporting all kinds of gestures. If you’d like more choice, check out Kevin Liew’s comparison of “<a href="https://www.queness.com/post/11755/11-multi-touch-and-touch-events-javascript-libraries">11 Multi-Touch and Touch Events JavaScript Libraries</a>.”

## Don’t Miss Out on Native Functionality

Building your app with web technology doesn’t necessarily mean that you can’t use native features. In fact, all major cross-platform development tools provide built-in access to the most important functionality. This includes APIs for device data, the file system, the network connection, geolocation, the accelerometer, notifications (including push) and much more.

You can usually even extend a development tool by building custom plugins. At Hojoki, we added many missing features, including reading the user’s setting for push notifications for our app, detecting the user’s time zone, and checking whether a third-party app is installed and launching it. Let’s look at two very simple examples for things that can be realized with native plugins. First, let’s enable JavaScript <code>focus()</code> for input fields on iOS 6+:

<pre><code class="language-clike">
if ([[[UIDevice currentDevice] systemVersion] floatValue] &gt;= 6) {
   [YourWebView setKeyboardDisplayRequiresUserAction:NO];
}
</code></pre>

## Optimize For Performance

Performance is usually considered to be one of the major disadvantages of a hybrid mobile app. This is mostly true if your app has a lot of heavy animations, contains huge scrolling lists and needs to run on old devices. However, if you are all right with supporting only newer platform versions (Android 4+, iOS 7+ and Windows Phone 8+), then you’ll very likely have satisfying results. It’s ultimately a question of how much effort you put into optimizing DOM and CSS selectors, writing performant JavaScript, reducing rendering time and minimizing the number of reflows and repaints. An endless number of articles and tutorials cover mobile web performance. These are some of my favorites:

*   “[Performance and UX Considerations for Successful PhoneGap Apps](https://www.tricedesigns.com/2013/03/11/performance-ux-considerations-for-successful-phonegap-apps/),” Andrew Trice
*   “[Mobile: Web Performance](https://estelle.github.io/mobileperf/)” (slides), Estelle Weyl
*   “[Writing Fast, Memory-Efficient JavaScript](https://www.smashingmagazine.com/2012/11/05/writing-fast-memory-efficient-javascript/),” Addy Osmani, Smashing Magazine
*   “[Minimizing Browser Reflow](https://developers.google.com/speed/articles/reflow),” Lindsey Simon, Google Developers
*   “[How to Make Your Website Faster on Mobile Devices](https://www.smashingmagazine.com/2013/04/03/build-fast-loading-mobile-website/),” Johan Johansson, Smashing Magazine

Beyond that, mobile hardware and rendering engines are improving at a rapid pace, with new devices coming out every other day. Developers can make the performance of a hybrid WebView app difficult to distinguish from that of a fully native app on the iPhone 5 series and on Android phones comparable to Nexus 4 and 5.</p>

## Increase Perceived Speed

Building a performant app is one thing, but making it <em>feel</em> fast is a whole other. Whether your app needs some time for a certain task (such as some heavy calculation or client-server communication), presenting instant feedback is crucial to providing a fluid and responsive experience. A common technique is to delay tasks that the user doesn’t need yet, while predicting and preloading the steps the user might take next. A famous example is Instagram, which <a href="https://www.cultofmac.com/164285/the-clever-trick-instagram-uses-to-upload-photos-so-quickly/">uploads photos in the background</a> while the user is busy adding tags and sharing. Perceived speed can be very different from actual speed, so let’s use it in our favor. Here are some no-brainers.</p>

### Remove the Click Delay on Touch Devices

A normal JavaScript click event handler on a touch device comes with a slight delay between the touchstart and the click being fired (usually around 300 milliseconds). This feature is built into the browser to detect whether the user is performing a single- or double-tap. If you don’t need the “double-tap to zoom” feature, you can safely eliminate these 300 milliseconds to get a much more responsive tap behavior. My favorite solution for this is the <a href="https://github.com/ftlabs/fastclick">FastClick</a> library. Use it on everything except Internet Explorer:

<pre><code class="language-javascript">
if ('ontouchstart' in window) {
   window.addEventListener('load', function() {
      FastClick.attach(document.body);
   }, false);
}
</code></pre>

Internet Explorer 10+ is a bit easier. You just need some CSS:

<pre><code class="language-css">
html {
   -ms-touch-action: manipulation; /* IE 10  */
       touch-action: manipulation; /* IE 11+ */
}
</code></pre>

### Style the Active State

As soon as the user taps an actionable element such as a button or a link, they should immediately get some kind of feedback that the app has detected their action. While the CSS pseudo-class <code>:hover</code> works great for this on the desktop, you need to switch to <code>:active</code> or a JavaScript solution for it to work on mobile. I’ve compared the three <a href="https://jsfiddle.net/prud/x9y6cfhg/">approaches to the active state</a> on JSFiddle. While they all work one way or another, you judge which is best for you.

Furthermore, remove the default tap highlight while adjusting your active states on mobile. I’d also recommend disabling user selections on actionable elements, because the selection menu would be quite disruptive if the user accidentally taps the button for too long.</p>

<strong>iOS and Android:</strong>

<pre><code class="language-css">
button {
   outline: 0;
   -webkit-tap-highlight-color: rgba(0,0,0,0);
   -webkit-tap-highlight-color: transparent;
   -webkit-touch-callout: none;
   -webkit-user-select: none;
      -moz-user-select: none;
       -ms-user-select: none;
           user-select: none;
}
</code></pre>

<strong>Windows Phone 8+:</strong>

<pre><code class="language-markup">
&lt;meta name="msapplication-tap-highlight" content="no"&gt;
</code></pre>

### Indicate Loading

Whenever your app is performing an action that will take some time to finish, even just for a second, consider adding a loading indicator. If you don’t, users will think that your app freezes occasionally, or they’ll click around when they shouldn’t, or they might even break things and then blame your app. From what I’ve experienced, animated GIFs are usually a bad idea in mobile browsers. As soon as there is a load on the CPU, the GIF freezes, thus defeating its entire purpose. I prefer <a href="https://fgnass.github.io/spin.js/">Spin.js</a> for its configurability and ease of use. Also, check out some other <a href="https://www.queness.com/post/9150/9-javascript-and-animated-gif-loading-animation-solutions">JavaScript solutions</a> and <a href="https://tympanus.net/codrops/2012/11/14/creative-css-loading-animations/">CSS loaders</a>.

Cross-platform tools like PhoneGap and Trigger.io also provide access to native loaders, which is great for showing a full-screen loading animation.</p>

## Get the Scrolling Right

Scrolling is one of the most important factors in the user experience of many apps. This is both a curse and a blessing because the success of its implementation will depend heavily on the scrolling niceties that your app relies on and on the mobile operating systems that need to be supported.

Scrollable content and a fixed header and/or footer bar are common to nearly all apps. There are two common approaches to achieving this with CSS:

1.  Enabling scrolling on the `body`, and applying `position: fixed` to the header;
2.  Disabling scrolling on the `body`, and applying `overflow: scroll` to the content;
3.  Disabling scrolling on the `body`, and applying JavaScript custom scrolling to the content.

While the first option has some benefits (such as iOS’s native scroll-to-top action and a simple code structure), I highly recommend going with the second option, <code>overflow: scroll</code>. It has <a href="https://remysharp.com/2012/05/24/issues-with-position-fixed-scrolling-on-ios/">fewer rendering issues</a> (although still a lot), and browser support is great on modern platforms (Android 4+, iOS 5+ and Windows Phone 8+), with a nice little <a href="https://github.com/filamentgroup/Overthrow#browser-support">polyfill for some older ones</a>. Alternatively, you could replace <code>overflow: scroll</code> with a custom scrolling library (the third option), such as <a href="https://iscrolljs.com/">iScroll</a>. While these JavaScript solutions allow for more flexibility with features (for example, the scroll position during momentum, event handling, customization of effects and scrollbars, etc.), they always penalize performance. This becomes critical when you’re using a lot of DOM nodes and/or CSS3 effects (such as <code>box-shadow</code>, <code>text-shadow</code>, <code>opacity</code> and <code>rgba</code>) in the content area.

Let’s look at some of the basic scrolling features.</p>

### Momentum Effect

The touch-friendly momentum effect enables users to quickly scroll through large content areas in an intuitive way. It can be easily activated with some simple CSS on iOS 5+ and in some versions of Chrome for Android. On iOS, this will also enable the content to bounce off the top and bottom edges.</p>

<pre><code class="language-css">
overflow-y: scroll;
-webkit-overflow-scrolling: touch;
</code></pre>

### Pull Down to Refresh

Various solution for this are available on the web, such as the one by <a href="https://damien.antipa.at/2012/10/16/ios-pull-to-refresh-in-mobile-safari-with-native-scrolling/">Damien Antipa</a>. While the solutions for iOS and Windows Phone have a similar look and feel, Android recently introduced its own mechanism (see below). We’ve implemented this in CatchApp using some JavaScript and CSS keyframes. (I have yet to wrap it up nicely and put it on GitHub, so stay tuned!)

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/817615ed-93c0-44cd-970a-7a737de8dccb/04-pull-ios-opt.jpg" alt="Pull down to refresh on iOS" width="367" height="162" /><br>
<figcaption>Pull down to refresh on iOS. (Image credit: <a href="https://damien.antipa.at/2012/10/16/ios-pull-to-refresh-in-mobile-safari-with-native-scrolling/">Damien Antipa</a>)</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e674f65c-fda3-4c40-9307-9dfba6696b1f/06-pull-android-opt.jpg" alt="Pull down to refresh on Android." width="367" height="236" /><br>
<figcaption>Pull down to refresh on Android. (Image credit: <a href="https://androidwidgetcenter.com/android-tips/how-to-refresh-gmail-on-android/">Android Widget Center</a>)</figcaption></figure>

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f79a9d7-b176-4263-92bf-f6462af36def/05-pull-wp-opt.gif" alt="Pull down to refresh on Windows Phone." width="367" height="376" /><br>
<figcaption>Pull down to refresh on Windows Phone. (Image credit: <a href="https://dwcares.com/pull-to-refresh-2/">David Washington</a>)</figcaption></figure>

### Scroll to Top

Unfortunately, disabling scrolling on the <code>body</code> will also break iOS’ native feature that enables users to quickly get to the top of the page by tapping the status bar. I’ve written a small script that can be added to any element and that takes care of <a href="https://github.com/prud/ios-overflow-scroll-to-top">scrolling to the top using JavaScript</a>, even if the content is currently in momentum. Add it to the header of your mobile website or to the status bar with a native plugin (for example, in PhoneGap).

Many other scrolling features could be implemented on top of the native <code>overflow: scroll</code>, such as snapping to a certain element or just infinite scrolling. If your requirements are more advanced, definitely look at the JavaScript options out there.</p>

## Make It Easy To Hit Stuff

When performing a touch action, users will quite often miss their target by a few pixels, especially on small buttons (such as the ones in iOS’ top bar). Developers can assist users while keeping the design elegant by enabling an invisible touch area around small targets:

<pre><code class="language-markup">
&lt;button&gt;
   &lt;div class="innerButton"&gt;Click me!&lt;/div&gt;
&lt;/button&gt;
</code></pre>

You’ll have to put the event handler on the button element, while restricting the styles to <code>div.innerButton</code>. Check out the <a href="https://jsfiddle.net/prud/r7kqr1a3/">full example, including CSS</a>, on JSFiddle.</p>

## Using Touch Gestures

A smartphone is all about touching and gestures. We swipe, pinch, zoom, drag and long-tap all the time when interacting with touch devices. So, why not offer users the same means of controlling your hybrid app? <a href="https://quojs.tapquo.com/">QuoJS</a> and <a href="https://hammerjs.github.io/">Hammer.js</a> are well-known libraries for supporting all kinds of gestures. If you’d like more choice, check out Kevin Liew’s comparison of “<a href="https://www.queness.com/post/11755/11-multi-touch-and-touch-events-javascript-libraries">11 Multi-Touch and Touch Events JavaScript Libraries</a>.”

## Don’t Miss Out on Native Functionality

Building your app with web technology doesn’t necessarily mean that you can’t use native features. In fact, all major cross-platform development tools provide built-in access to the most important functionality. This includes APIs for device data, the file system, the network connection, geolocation, the accelerometer, notifications (including push) and much more.

You can usually even extend a development tool by building custom plugins. At Hojoki, we added many missing features, including reading the user’s setting for push notifications for our app, detecting the user’s time zone, and checking whether a third-party app is installed and launching it. Let’s look at two very simple examples for things that can be realized with native plugins. First, let’s enable JavaScript <code>focus()</code> for input fields on iOS 6+:

<pre><code class="language-clike">
if ([[[UIDevice currentDevice] systemVersion] floatValue] &gt;= 6) {
   [YourWebView setKeyboardDisplayRequiresUserAction:NO];
}
</code></pre>

And here’s the code to copy a given string to the device’s clipboard on iOS:

<pre><code class="language-clike">
[[UIPasteboard generalPasteboard] setString:@"Your copied string"];
</code></pre>

## Always Provide a Way Out

Web developers often overlook how to handle bad situations in a hybrid app (for example, a connection timeout, a bad input, a timing issue, etc.). A hybrid app is fundamentally different from a website, mainly because there is no global refresh button, and an app can easily run in the background for weeks on some mobile operating systems. If the user runs into a dead end, their only option will be to restart the app, which entails force quitting and then restarting. Many people don’t even know how to do that, especially on Android 2.x (where it’s hidden deep in the app’s settings) and on iOS 6 and below (where you have to double-tap the home button, long-press the icon and kill it).

So, ignore the refresh button during development, and handle bad situations as they come up. For all other situations that would have unexpected outcomes, such as ones involving client-server communication, be prepared for things to go wrong, and provide a way out for users. This could be as easy as showing a full-screen error message — “Oops! Something bad happened. Please check your connection and try again” — with a big “Reload” button below.</p>

## How To Wrap It

Developing a hybrid mobile app means using the same tools and processes that you would usually use to develop (mobile) websites. Having said that, one thing I really like about the hybrid approach is that you can deploy HTML, CSS and JavaScript code as a mobile web app with relative ease. Make sure to implement fallbacks for native features, or find elegant workarounds if they are not supported at all. Most mobile developers prefer to keep users in a native app, and you could even advertise the app to your mobile website’s users.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/255a4062-9474-4377-b1a5-b4a411442b36/07-hybrid-app-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efc9eb97-70f1-4305-a37d-7b1ec3ae8dad/07-hybrid-app-opt-500.jpg" alt="Native WebView wrapper around a HTML/CSS/JavaScript code base." width="338" height="600" /></a><figcaption>A native WebView wrapper, with an HTML, CSS and JavaScript code base. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/255a4062-9474-4377-b1a5-b4a411442b36/07-hybrid-app-opt.jpg">View large version</a>)</figcaption></figure>

What about the native part? Your mobile web app (plain HTML, CSS and JavaScript) will be loaded in a WebView, which is an internal browser engine that renders an app the way a default browser on the device would render it (there might be slight differences — your mileage may vary). Additionally, native “bridges” are used to expose features of the device and operating system through an API to make them accessible with JavaScript. This usually includes access to the device’s camera, address book, geolocation, file system and native events (for example, via one of the hardware buttons on Android), to name just a few features.

A few cross-platform development tools provide that native bridge and simplify the whole process of wrapping it. Let’s dive into some options.</p>

### PhoneGap and Apache Cordova

<a href="https://phonegap.com/">PhoneGap</a> is certainly one of the most popular tools for cross-platform development. The name itself is often used synonymously with hybrid mobile app development.

There has been <a href="https://phonegap.com/2012/03/19/phonegap-cordova-and-what%E2%80%99s-in-a-name/">some confusion about its name</a> and relation to <a href="https://cordova.io">Apache Cordova</a>, which is understandable. The latter is a top-level Apache project that was formerly called PhoneGap. It offers a set of device APIs to access native functionality from HTML, CSS and JavaScript code running in a WebView. Now, Adobe PhoneGap is a distribution of Cordova — not unlike the way Chrome uses WebKit as its engine.

Both are open-source and free to use, with support for all major platforms and with an active community developing all kinds of plugins and extensions.

PhoneGap has shaped the hybrid lanscape significantly, and many new tools have emerged that offer <strong>additional services</strong> or that streamline the development process. They usually add a lot of convenience by enabling you to build an app in the cloud, thereby saving you the effort of locally installing all of the different platform SDKs and tools. Each tool has a different focus, level of platform support and price:

*   [PhoneGap Build](https://build.phonegap.com/)
*   [Telerik AppBuilder](https://www.telerik.com/appbuilder) (formerly Icenium)
*   [AppGyver Steroids](https://www.appgyver.com/)
*   [Appery.io](https://appery.io/) (formerly Tiggzi)
*   [Monaca](https://monaca.mobi)
*   [Intel XDK](https://software.intel.com/html5/tools)

### Sencha Touch

<a href="https://www.sencha.com/products/touch/">Sencha Touch</a> started out as a UI framework for the mobile web and has been around for years. Traditionally, developers have used Sencha to build an app while using another service, like PhoneGap, to deploy it as a hybrid app. Nowadays, Sencha offers this kind of functionality built in for free. Platform support includes iOS and Android (both via Sencha’s own native packager) BlackBerry, Windows 8 and more (via PhoneGap Build).</p>

### Trigger.io

At Hojoki, we started using <a href="https://trigger.io">Trigger.io</a> two and a half years ago because we were looking for a lightweight alternative to PhoneGap. Even though iOS and Android are its only supported platforms, it offers a good set of native APIs, custom plugins and third-party integration (including Parse push notifications, Flurry analytics and parts of Facebook’s SDK). Trigger.io’s command-line tools allowed us to integrate the app’s packaging into our <a href="https://gruntjs.com/">Grunt</a> build process, which is great if you love automation.

One of its key features is <a href="https://trigger.io/reload/">Reload</a>, which enables developers to push HTML, CSS and JavaScript updates to an app on the fly. Unlike PhoneGap Build’s <a href="https://docs.build.phonegap.com/en_US/tools_hydration.md.html">Hydration</a>, Reload is specifically designed for development and production apps. This makes it possible to legally bypass Apple’s submission process to push bug fixes and iterate quickly with A/B testing.

Once the 14-day trial is up, Trigger.io’s <a href="https://trigger.io/pricing/">steep pricing</a> is probably the biggest downside for many developers.</p>

<del datetime="2014-10-25T13:30:29+00:00">With MoSync having gone offline a couple of days ago, Trigger.io seems to be the only remaining tool that is not associated with PhoneGap.</del> <a href="https://www.mosync.com/">MoSync</a> seems to be another tool that is not associated with PhoneGap, however I'm not sure how actively it is being developed at the moment.</p>

### Test on Real Devices

Building a mobile app with web technologies obviously tempts us to do most of our testing in a web browser. This might be fine when developing non-native features, but definitely avoid it when releasing. Test with as many manufacturers, platforms and form factors as possible before submitting the app. Android’s fragmentation brings endless possibilities of differences in browser rendering, unsupported features and manufacturer modifications. While iOS does much better with rendering differences, Apple has a growing number of devices with varying sizes, resolutions and pixel densities. Check out “<a href="https://www.smashingmagazine.com/2014/07/14/testing-and-responsive-web-design/">Prioritizing Devices: Testing and Responsive Web Design</a>” to learn more.

When Facebook famously ditched most of its HTML5 and went native in 2012, it cited <a href="https://lists.w3.org/Archives/Public/public-coremob/2012Sep/0021.html">missing debugging tools and developer APIs</a> as one of its main reasons. <a href="https://venturebeat.com/2013/04/17/linkedin-mobile-web-breakup/">LinkedIn drew the same conclusions</a> half a year later, stating that HTML5 itself is ready, but basic tools and the ecosystem don’t support it yet. From what I’m seeing, the situation is getting better, with remote debugging in WebView on Android 4.4+ and an increasing number of development tools on all platforms:

*   “[Web Inspector](https://developer.apple.com/safari/tools/),” Safari (iOS)
*   “[Remote Debugging on Android with Chrome](https://developer.chrome.com/devtools/docs/remote-debugging)”
*   “[Debug Store Apps in Visual Studio](https://msdn.microsoft.com/en-us/library/windows/apps/hh441472.aspx)” (Windows Phone 8.1), Windows Dev Center
*   [Weinre](https://people.apache.org/~pmuellr/weinre/) (for everything), Patrick Mueller
*   [Edge Inspect](https://html.adobe.com/edge/inspect/) (for iOS and Android), Adobe

### Start Thinking in Terms of Hard Releases

When building an app for web browsers, deploying a hot fix to users is a simple step, which means that testing can lose some of its importance. This obviously needs to be reconsidered when you’re releasing an app through an app store. Think of it like software development in the ’90s: You’re now living in the world of hard releases.

So, why is this bad? First, the submission process could easily take a week or two (Hello, Apple!). Secondly, even if your hot fix is released quickly, that doesn’t guarantee that users will update the app any time soon. Here are my suggestions:

1.  Make testing a high priority.
2.  Have some kind of “force update” logic to deprecate old client versions.
3.  Use mechanisms like Trigger.io’s [Reload](https://trigger.io/reload/) to fix code on the fly.
4.  Apply for an [expedited app review](https://developer.apple.com/appstore/contact/appreviewteam/index.html) (Apple only) if you need to be fast.</p>

### Get It in the Stores

The tools mentioned above spit out a binary for each platform, which can then be submitted to the relevant store. From this point on, the process is exactly the same as publishing a “normal” native app. Some of the tools we’ve looked at might even have better documentation for this. Nevertheless, here are the official guides:

*   “[App Distribution Guide](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html),” Apple
*   “[Get Started With Publishing](https://developer.android.com/distribute/googleplay/start.html)” and “[Launch Checklist](https://developer.android.com/distribute/tools/launch-checklist.html),” Android Developers
*   “[Publish for Windows Phone](https://msdn.microsoft.com/library/windows/apps/jj206736.aspx),” Windows Dev Center

## Conclusion

Now that our hybrid mobile apps have been in Apple’s App Store and in Google Play for two years, I’d like to recapitulate some of the benefits and drawbacks mentioned at the beginning of this article.

For us, a web startup company with very limited resources and no native iOS or Android experience, building an app for multiple platforms in just a few weeks would have been impossible. Choosing the hybrid path enabled us to reuse a lot of code from the web app and to iterate quickly based on user feedback. We’ve even managed to publish native apps for Windows 8 for the desktop and Microsoft Surface as well as Mac OS X with exactly the same code base. The effort of moving to another platform will depend largely on the capabilities of the given browser and device and on the level of your need for native functionality. We needed push notifications, in-app purchases and access to the user’s contacts, among other things. Depending on your needs, a lot of native functionality could make you heavily dependent on the native wrapping tool that you choose.

Finally, let’s see whether hybrid apps really can deliver a native look and feel. Below is a compilation of user reviews from the app stores. Both positive and negative comments are included, but many of the negative reviews are for early releases, which had the same UI for all platforms and was comparatively slow in performance.
<blockquote>★ Great idea, but not a good app. The app runs extremely slow on my Samsung Galaxy Ace and Tab. The app also looks and controls like an iPhone app. This is confusing when you have never had an iPhone.

★★ Another reason apps should not use WebViews for UI.

★★ Service great but WebView app sucks.

★★★ It’s the right app in concept, but it really is too laggy to be practically used. And I’m using Jellybean so there is no excuse.

★★★ It lags a lot and the UI is not beautiful.

★★★ Good but very very slow.

★★★★ This app is very handy, but is a little slow to boot up.

★★★★★ This is working really hard well since the update. It’s a great app to begin with and now it’s working smoother and faster than before.

★★★★★ Extremely smooth and effective.

★★★★★ The app work flawlessly…

★★★★★ Beautiful designed app! Love the interface and the great overview of all your tools! Good job! Keep shippin!

★★★★★ This is an absolutely beautiful aggregate that runs buttery smooth, even on a 3GS. Recommend to anyone doing any sort of project.</blockquote>

We’re definitely moving away from platform-specific app development and towards the many new technologies that are emerging. <a href="https://youtu.be/9pmPa_KxsAM?t=2h56m6s">Larry Page said this</a> when asked at Google I/O last year about the future of the web:
<blockquote>In the very long term, I don’t think you should have to think about, as a developer, am I developing for this platform or another, or something like that. I think you should be able to work at a much higher level, and software you write should run everywhere, easily.</blockquote>

The (mobile) web is a major success story in this regard. Being able to use this platform and still be able to distribute an app in all stores is a huge step forward. It will be interesting to see how this all plays out. Whatever happens, using a technology that over a <a href="https://en.wikipedia.org/wiki/List_of_countries_by_number_of_Internet_users">third of the world’s population</a> (over two thirds in Europe and the US) relies on probably won’t be a bad choice.

{{< signature "da, al, ml" >}}


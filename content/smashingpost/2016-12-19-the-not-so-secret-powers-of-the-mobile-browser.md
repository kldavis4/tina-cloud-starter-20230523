---
title: The (Not So) Secret Powers Of The Mobile Browser
slug: the-not-so-secret-powers-of-the-mobile-browser
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98fee945-1ddc-4173-aed7-4ad4e470255d/application-shell-500-opt.jpeg
date: 2016-12-19T21:26:43.000Z
author: stephaniewalter
summary: >-
  This article presents some of the cool things you can do with APIs and other technologies to make your users’ lives easier. The future of the mobile browser is bright, shiny and fun. We can and will be able to build incredibly powerful things with web technologies.
description: >-
  This article presents some of the cool things you can do with APIs and other technologies to make your users’ lives easier. The future of the mobile browser is bright, shiny and fun.
categories:
  - Mobile
  - Browsers
  - Apps
  - API
---
Apple taught us, "There’s an app for that." And we believed it. Why wouldn’t we? But time has passed since 2009. Our mobile users have gotten more mature and are starting to weigh having space for new photos against installing your big fat e-commerce app. Meanwhile, mobile browsers have also improved. <strong>New APIs are being supported</strong>, and they will bring native app-like functionality to the mobile browser.

We can now access video and audio and use WebRTC to build a live video-chat web apps directly in the browser, no native app or plugin required. We can build progressive web apps that bring users an almost native app experience, with a launch icon, notifications, offline support and more. Using geolocation, battery status, ambient light detection, Bluetooth and the physical web, we can even go beyond responsive web design and build websites that will automagically adapt to users' needs and context.

*To help us dig into this world of new (and not so new) functionality and to guide us through this journey in the world of "Everything is possible in a mobile browser," I will illustrate this article with some fictional but plausible use cases. Dear reader, meet Zoe, my user. She’s around 30 and works as a developer in our industry in the very near future. She works all day long on a computer, so she doesn’t want to have one at home, and she uses her smartphone as a primary device to navigate the web.*

## Part 1: Accessing And Handling Images, Video And Audio Directly In The Browser

### Video and Audio Conference in the Browser (With WebRTC)

<em>Zoe is invited to speak at a conference. Instead of adding her on Skype, like people usually do, the conference organizers send Zoe a link to an online video and audio conference web app, <a href="https://apprtc.appspot.com/">AppRTC</a>.</em>

<em>Zoe simply enters the correct room number. The browser asks her permission to access her camera and microphone, and that’s it: She gets connected with the other person. Zoe doesn’t need to install or update any additional plugin or app. Everything happens directly in the browser, no extra steps, no friction.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dd87125-96c8-410e-a448-b24c90588ed4/webrtcchat-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/96a5dcc0-d109-4c27-a9d9-19c6452af1b2/webrtcchat-650-opt.jpg" alt="An online video conference chat in the browser" width="650" height="381" /></a><figcaption>Zoe doesn’t need to install anything to have an audio or video conference. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0dd87125-96c8-410e-a448-b24c90588ed4/webrtcchat-large-opt.jpg">View large version</a>)</figcaption></figure>

With a native app (especially on Android), you can ask users for a lot of permissions up front when they download your app. In the browser, users have to grant you access one API (i.e. one piece of functionality) at a time.

Using <a href="https://w3c.github.io/webrtc-pc/">WebRTC</a>, you can open a direct real-time communication channel between two clients. You can then share sound, video and any other data directly between them.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc138f3d-bc69-4768-b2a0-826f0178a005/ptop-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17214285-16b9-48fc-990a-3462f4932d44/ptop-650-opt.jpg" alt="Peer-to-peer explanation" width="650" height="381" /></a><figcaption>Using WebRTC for a peer-to-peer connection (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc138f3d-bc69-4768-b2a0-826f0178a005/ptop-large-opt.jpg">View large version</a>)</figcaption></figure>

This is powerful, but it’s <a href="https://caniuse.com/#feat=rtcpeerconnection">supported only</a> in Firefox and Chrome, and it’s under development for Edge and Safari. You will also need to access the video and audio streams. This can be done using the <a href="https://www.w3.org/TR/mediacapture-streams/"><code>getUserMedia</code> and Media Stream API</a> (which is <a href="https://caniuse.com/#feat=stream">not supported</a> in Internet Explorer or Safari).

Using this technology, we could imagine recreating a Google Hangouts or Facebook Messenger web app directly in the browser. The only thing missing would be access to the phone’s contacts. This is not currently possible from the browser with any kind of API.

### Uploading a Picture From the Camera to the Browser

<em>Zoe is asked by the conference’s organizers to fill her online bio for the conference. She logs into the website, goes to her account and finds the place to do so. When she taps on the "Update my picture" button, she can choose between taking a new picture with her camera or selecting a picture already taken. She chooses the first option and fills in her profile.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/058d8341-b24a-47e4-80cf-0d190178ea19/media-upload-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80260c9c-d05d-4b1a-92b6-4d9d4ee94a57/media-upload-650-opt.jpg" alt="Media upload possibilities" width="650" height="381" /></a><figcaption>Zoe chooses to take a picture with her phone. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/058d8341-b24a-47e4-80cf-0d190178ea19/media-upload-large-opt.jpg">View large version</a>)</figcaption></figure>

The HTML5 <code>file</code> input type has gotten a <a href="https://www.wufoo.com/html5/attributes/20-accept.html">new attribute, named <code>accept</code></a>.

You can pass a comma-separated list of types of content files. On mobile, this would trigger a dialog in which users can chose between different content sources or direct access to the camera:

<pre><code class="language-markup">&lt;input type="file" id="image" name="image" accept="image/*"&gt;
</code></pre>

If you want the user to skip the selection dialog and directly access their camera to take a picture, you can add the <code>capture</code> attribute:

<div class="break-out">

 <pre><code class="language-markup">&lt;input type="file" id="capture" name="capture" accept="image/*" capture="camera"&gt;
</code></pre>
</div>

This would also work if you want to capture video or audio:

<div class="break-out">

 <pre><code class="language-markup">&lt;input type="file" id = "video" name="video" accept="video/*" capture="camcorder"&gt;
&lt;input type="file" id="audio" name="audio" accept="audio/*" capture="microphone"&gt;
</code></pre>
</div>

If you want to have fun on your phone, I’ve put together a little <a href="https://codepen.io/stephaniewalter/full/xZoxOb/">demo with all of these inputs</a>.

Now that we can directly access media (videos, images and audio) in the browser, a whole new world of possibilities has opened up. You could change your avatar right on the responsive website of any of your social media accounts, and you could take and upload photos and videos to your timeline instantly. If you want to sell your car or bike on Craigslist, you don’t need to take pictures of it and then upload them to your computer; you can create your ad and add the images right in your mobile browser.

### Having Fun With Inputs

If we want to go one step further, we could imagine recreating an Instagram-type app directly in the browser using CSS3 filters and input type files.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/464c284a-7825-48e8-811e-18c2fa1d3fe4/cssgram-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7106faa1-d17f-487c-9965-c429962f5046/cssgram-650-opt.jpg" alt="CSSgram" width="650" height="381" /></a><figcaption>This is what Una started doing with her <a href="https://una.im/CSSgram/">CSSgram</a>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/464c284a-7825-48e8-811e-18c2fa1d3fe4/cssgram-large-opt.jpg">View large version</a>)</figcaption></figure>

There’s also a really fun <a href="https://guitar-tuner.appspot.com/">guitar tuner</a> web app that uses your microphone to make sure your guitar (or voice) is perfectly tuned. Pretty handy, isn’t it? Again, you don’t need to install anything.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b517df-71a6-42ab-9a9d-811ebd35228a/guitartuner-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a77e4651-70c0-4586-a99b-4ec185f4c294/guitartuner-650-opt.jpg" alt="Guitar tuner in the browser" width="650" height="381" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b517df-71a6-42ab-9a9d-811ebd35228a/guitartuner-large-opt.jpg">View large version</a>)</figcaption></figure>

## Part 2: Enhancing A Conference Website Into A Web App

In this second part, I want to show you how we can enhance the user experience on a conference website. You might be familiar with the concept of progressive enhancement on the web. I encourage you to apply it to the techniques that follow: Make sure that all of the main functionality on your website is accessible and works on a wide range of mobile browsers, and then progressively enhance the website with launch icons, notifications and offline support to build a better experience on mobile devices that support it.

{{% feature-panel %}}

## Installing And Launching The Website As A Progressive Web App

To access a website, most users either will already have it bookmarked and hidden in a sea of bookmark folders or will simply look for it on their favorite search engine. One of the main arguments in favor of apps is the launch icon: It’s already there, ready on the user’s home screen.

### Favicon for the Home Screen

Now, imagine that you could do the same for a website and launch it from the home screen, like you would do for any native app. Most modern browsers have this option available in a menu.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f0887d0-a1b4-451e-9099-17303bf3943b/add-to-home-button-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7bf4f8d-b0fd-4c94-9a01-a4332501cb3d/add-to-home-button-650-opt.jpg" alt="Firefox, Safari and Chrome can all add a website to the home screen from the menu." width="650" height="381" /></a><figcaption>A website can be added to the home screen from the menu in Firefox, Safari and Chrome. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f0887d0-a1b4-451e-9099-17303bf3943b/add-to-home-button-large-opt.jpg">View large version</a>)</figcaption></figure>

You’ll need some extra files and size to satisfy the range of browsers out there on the market, but this will work on iOS, Android (Chrome, Opera and Firefox) and Edge for mobile.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14825bc6-4789-446f-8ea4-7501bf7b8bda/launch-icon-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d8417be-874c-4b95-a8e0-4eb058427452/launch-icon-650-opt.jpg" alt="The favicon for my portfolio on different OS" width="650" height="381" /></a><figcaption>The favicon for my portfolio on different OS'. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14825bc6-4789-446f-8ea4-7501bf7b8bda/launch-icon-large-opt.jpg">View large version</a>)</figcaption></figure>

### Chrome’s App Install Banner

Not a lot of users know that they can add a website directly to their home screen. To make this functionality more discoverable, Chrome 42+ introduced the <a href="https://developers.google.com/web/updates/2015/03/increasing-engagement-with-app-install-banners-in-chrome-for-android">App Install Banner</a>. For the moment, the banner appears when users have visited a website at least twice, with at least five minutes having elapsed between visits.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09580085-9c1d-4255-b738-82c8dae18d28/add-to-hom-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/042f6467-5aca-4bf1-bbcd-0c13a0138d73/add-to-hom-650-opt.jpg" alt="Smart 'add to home screen banner' in Chrome" width="650" height="" /></a><figcaption>While preparing for her talk, Zoe visits the conference’s website a lot. After a few visits, a small banners appears, telling her she can add the website to her home screen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09580085-9c1d-4255-b738-82c8dae18d28/add-to-hom-large-opt.jpg">View large version</a>)</figcaption></figure>

Your website also has to meet a few technical criteria to trigger this banner, including having a service worker, being served over HTTPS (which we’ll get to later) and having a valid web app manifest file.

### The Web App Manifest File

Specified by the W3C, a <a href="https://w3c.github.io/manifest/">web app manifest</a> is a simple JSON file that enables a developer to control a lot of things about their web app, including its name, icon, launch screen and theme colors, as well as how they want it to launch. <a href="https://manifest-validator.appspot.com/">Web Manifest Validator</a> is a little online tool that will help you to validate the file. Once it’s created, you will need to <a href="https://developers.google.com/web/updates/2014/11/Support-for-installable-web-apps-with-webapp-manifest-in-chrome-38-for-Android#telling_the_browser_about_your_manifest">link it to your website</a>.

<pre><code class="language-javascript">{
  "short_name" : "SuperConf",
  "name": "SuperConf, an amazing conference",
  // Defines a default URL to launch
  "start_url": "/index.html",
  "icons": [
    {
      "src": "launchicon.png",
      "sizes": "96x96",
      "type": "image/png"
    }
     // Other icons go here
  ],
  // Launches the website without a URL bar
  "display": "standalone",
  // Provides a site-wide theme color
  "theme_color": "#fa9c00",
  // Provides a background color for the launch screen
  "background_color":"#ffffff"
}
</code></pre>

It’s <a href="https://developer.mozilla.org/en-US/docs/Web/Manifest">currently supported</a> in Android WebView, Opera Mobile, Chrome for Android and <a href="https://developers.google.com/web/updates/2014/11/Support-for-installable-web-apps-with-webapp-manifest-in-chrome-38-for-Android#what_every_developer_should_do_today">apparently Firefox</a> as well.

### Splash Screen

Starting in Chrome 47+, browsers use the manifest’s <code>theme_color</code>, <code>background_color</code>, <code>name</code> and <code>icons</code> to automatically generate a <a href="https://developers.google.com/web/updates/2015/10/splashscreen">launch screen</a> while a website loads.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cc2ebae-4812-4baa-885b-44fa9f2ae45f/splashscreen-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38ca2044-6a2e-4f96-9894-a2a3faa6b17a/splashscreen-650-opt.jpg" alt="Splash screen" width="650" height="381" /></a><figcaption>When Zoe is on a slow connection and is waiting for the website to load, she will see the icon of the conference, with an orange toolbar and a white background. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8cc2ebae-4812-4baa-885b-44fa9f2ae45f/splashscreen-large-opt.jpg">View large version</a>)</figcaption></figure>

### Customizing the Display Mode

With the <a href="https://w3c.github.io/manifest/#dfn-display-mode"><code>display</code> property</a> in the manifest file, a developer can choose how they want the website to launch once it has been added to the home screen:

*   `"display": "standalone"` launches the website in full-screen mode, without any URL bar (currently supported in Chrome and Opera).
*   `"display": "browser"` launches the website in the conventional mode, with the URL bar visible.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19f76b84-1485-4afe-944e-017fe5f82578/display-mode-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7950a8bd-72a4-4179-8157-bb00ec517ee6/display-mode-650-opt.jpg" alt="Display standalone versus browser" width="650" height="381" /></a><figcaption><code class="language-markup">"display": "browser"</code> is on the left and <code class="language-markup">"display": "standalone"</code> is on the right for two different websites. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19f76b84-1485-4afe-944e-017fe5f82578/display-mode-large-opt.jpg">View large version</a>)</figcaption></figure>

The W3C also specifies <code>fullscreen</code> mode, which launches a website using the entirety of the available display area on a mobile device, and <code>minimal-ui</code> mode, which gives the user access to a minimal set of UI elements. Neither seems to be supported anywhere yet.

Developers can also force an orientation with <code class="language-markup">"orientation": "landscape"</code> or <code class="language-markup">"orientation": "portrait"</code>, but unless you are building a video game, you might not want to use it.

### Be Careful With `meta name="apple-mobile-web-app-capable"` on iOS

Display mode isn’t supported on iOS. The <a href="https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html"><code>&lt;meta name="apple-mobile-web-app-capable"&gt;</code> tag</a> might look like it does the same thing, but it doesn't. It will work on a web app with no links (AJAX-loaded content, for instance), but as soon as you use this on a traditional website, things get ugly. When the user launches the website from the launch icon, it will open full screen, but as soon as they tap on a link, it will open in a new tab in Safari. To prevent this, you will need some JavaScript to override the click event (which does not sound ideal).

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/681697c3-1284-4b51-be3a-688bf7f239b2/apple-launch-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/41924d53-384a-450d-8598-910487982a02/apple-launch-650-opt.jpg" alt="on iOS" width="650" height="381" /></a><figcaption>By default, the launched page opens full screen, but any other URLs open in a new tab. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/681697c3-1284-4b51-be3a-688bf7f239b2/apple-launch-large-opt.jpg">View large version</a>)</figcaption></figure>

### Changing the Color of the URL Bar

Another fun thing you can do to delight users is to change the color of the URL bar. To change it for every page, you can use the HTML <code>meta</code> tag:

<pre><code class="language-markup">&lt;meta name="theme-color" content="#db5945"&gt;
</code></pre>

Here in France, we have a nice website that sells socks… only socks &mdash; but it does it quite well. Part of its success is due to the wide range of sock colors. And the color of the URL bar on every page matches the color of the displayed socks. This is one of those little details that can delight users and contribute to a fun overall experience.

{{< vimeo id="188562476" >}}

Using the <code>manifest.json</code> file, you can also provide a site-wide theme color: <code class="language-markup">"theme_color": "#133742"</code>.

Users will see this color in the URL bar as well as in the Android bar at the top when the website is in <code>browser</code> mode. It will also be used for the top bar of the splash screen, as seen before, and when the tab is displayed in a stack of many other tabs in multitasking mode.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0a25e10-1ff4-46a0-b520-03b1b95c88fb/theme-color-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1190443d-02ef-4e08-b9f0-7ddc13f0ef45/theme-color-650-opt.jpg" alt="Orange theme color" width="650" height="381" /></a><figcaption><code class="language-markup">"theme_color": "#133742"</code> gives a nice orange color theme to my website. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f0a25e10-1ff4-46a0-b520-03b1b95c88fb/theme-color-large-opt.jpg">View large version</a>)</figcaption></figure>

### One Tool to Generate Them All

If you want to provide a nice experience, there’s a lot to do and to think about, including making a lot of different sizes of icons for different operating systems. Some nice person has built a cool little tool named <a href="https://realfavicongenerator.net/">RealFaviconGenerator</a>. Feed it your favicon, and you’ll get a nice interface to play with and to tweak all of the things just mentioned. Grab the ZIP file, and voilà!

{{% ad-panel-leaderboard %}}

## Notification Access

<em>Zoe checks the program before the conference. From the little icon next to each talk, she understands that she can add a talk that she wants to attend to her schedule. A subscription button appears under each talk’s description, with short text explaining that users who have subscribed to the talk will get a notification 10 minutes before the talk starts, even if their browser is closed. Users must allow access through a browser dialog.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7945502a-164e-4f2d-8f57-d9068f03685a/notification-dial-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eba3936e-053a-4675-a4f4-61bdaa463efb/notification-dial-650-opt.jpg" alt="notification dialog" width="650" height="381" /></a><figcaption>The first time Zoe clicks the notification button, the browser shows a dialog asking for access to send notifications for this domain. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7945502a-164e-4f2d-8f57-d9068f03685a/notification-dial-large-opt.jpg">View large version</a>)</figcaption></figure>

### Being Smart When Asking Permissions on Mobile Browsers

The Chromium team put out an interesting document titled "<a href="https://docs.google.com/document/d/1WNPIS_2F0eyDm5SS2E6LZ_75tk6XtBSnR1xNjWJ_DPE/edit#heading=h.v5v9jr5n9i1w">Best Practices for Push Notifications Permissions UX</a>." Users need to understand what they will gain from giving you access to their notifications. Explain why you need this access, and put it in context. I’m seeing more and more websites and blogs asking to send notifications the first time a user arrives on the home page. As a user, I might have arrived on a blog by following a link on Twitter and might not know what the blog is about, so I’m going to need more context before accepting notifications (if I ever do accept them). In the browser, when a user denies access, the website will not be able to ask for it again (unless the user goes into the website settings). So, be smart about when and where you ask. This is a general rule for all permissions, by the way (media, notifications, geolocation, etc.).

### Integrating Notifications in the OS

<em>The conference day has finally arrived, and Zoe is getting a coffee when her phone vibrates. Even though the website and web app are closed, she has just gotten a notification directly on her locked phone, telling her that the first talk she has subscribed to will be starting in 10 minutes.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adb0da84-b8c6-40e4-abab-d664a1b534db/notifications-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e9d6ddd-25f6-46ff-aacf-916264d44483/notifications-650-opt.jpg" alt="Notification example" width="650" height="381" /></a><figcaption>Example of website notifications on Android (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/adb0da84-b8c6-40e4-abab-d664a1b534db/notifications-large-opt.jpg">View large version</a>)</figcaption></figure>

Mobile browser notifications can compete with native notifications because they get integrated directly in the notification center of the operating system. This means that they will get displayed outside of the browser or web app, even if it is closed. It will appear in the operating system’s notification center and will be displayed on the lock screen of the phone as well. Notifications in Chrome can also be shown in the desktop notification center of Windows 10 and Mac OS X.

### Meet the Push API and Service Workers

A service worker is JavaScript that runs in the background once installed. It acts as a sort of small proxy, pushing notifications to the browser. The Push API is part of the family of service worker technologies. Once activated on the page, the service worker receives the push message, and then it is up to you how to notify the user (for example, using push messages or one-page notifications). A the time of writing, <a href="https://caniuse.com/#feat=serviceworkers">service workers are supported</a> in Chrome, Firefox, Opera, Android browser and Chrome for Android (it is under consideration for WebKit), and the <a href="https://caniuse.com/#feat=push-api">Push API is supported</a> only in Firefox, Chrome and Chrome for Android 51.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1736f953-f85c-45f2-9098-de9a425dd97f/service-worker-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d659c9ab-c3cc-4ce6-89f7-16af453db4e3/service-worker-650-opt.jpg" alt="Service workers" width="650" height="381" /></a><figcaption>Service workers (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1736f953-f85c-45f2-9098-de9a425dd97f/service-worker-large-opt.jpg">View large version</a>)</figcaption></figure>

In short, to make notifications work, you will need:

*   HTTPS on your server,
*   a declaration of a service worker,
*   the Push API,
*   the user’s acceptance.

That’s as far as my technical skill goes. If you want to go deeper, here are a few resources from people far more qualified on the topic than me:

*   [Notification Generator](https://tests.peter.sh/notification-generator/), to help you test notifications.
*   "[Service Workers: An Introduction](https://www.html5rocks.com/en/tutorials/service-worker/introduction/)," Matt Gaunt, Google Developers
*   "[Beyond Offline](https://hacks.mozilla.org/2015/12/beyond-offline/)," Salva, Mozilla Hacks Discusses other cool things you can do with service workers.
*   "[Web Push Notifications: Timely, Relevant, and Precise](https://developers.google.com/web/fundamentals/engage-and-retain/push-notifications/)," Joseph Medley, Google Developers
*   "[Using the Push API](https://developer.mozilla.org/en-US/docs/Web/API/Push_API/Using_the_Push_API)," Mozilla Developer Network A long but interesting article.
*   [Is ServiceWorker Ready?](https://jakearchibald.github.io/isserviceworkerready/), Jake Archibald To check the status of browser support.

## Offline Access

<em>Zoe might not have noticed, but the conference’s schedule was cached offline while she was browsing. This means that, even if she doesn’t always have an Internet connection during the conference, she can still visit the website.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e9e7871-cd6f-4b32-b69b-2c5a43c3e5fa/service-worker-offline-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b21ef452-2ce3-4b2c-8eb9-b5b1afae2256/service-worker-offline-650-opt.jpg" alt="Service worker and offline access" width="650" height="381" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e9e7871-cd6f-4b32-b69b-2c5a43c3e5fa/service-worker-offline-large-opt.jpg">View large version</a>)</figcaption></figure>

This magic happens again with service workers. A service worker can intercept the user’s request and provide cached files to display the page faster, with or without a connection. The browser will first look for the cached files, instead of requesting the ones on the server. It can then also check whether the files need to be updated by looking for file modifications in the background. You can use this to make your website work offline, but you can also use it to cache part of the website &mdash; the user interface, if you like &mdash; to make it load faster.

I imagined all kinds of scenarios for Zoe when I was preparing for the ConFoo conference in March 2016. I wanted to create a demo page, but then in June I saw that Google I/O implemented everything I imagined, so I’ll let you play with that demo instead. Open your mobile browser, go to <a href="https://events.google.com/io2016/">events.google.com/io2016</a>, navigate to the schedule, and add some events to your list (you might need to log in with a Google account first). Then, add the website to your home screen, close Chrome, and launch the website from the home screen icon. Keep on adding things to your list. Switch to airplane mode, and you should see a short explanation that the connection has been lost and that changes will be synchronized with the server once you are back online. Add some more talks to the list, go back online, and voilà!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f954716-e70f-4dfe-9f1c-bac3c7482534/google-io-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0a542e96-4c38-4a0c-8249-0699f4086a70/google-io-650-opt.jpg" alt="Google I/O demo" width="650" height="381" /></a><figcaption><a href="https://events.google.com/io2016/">Google I/O 2016 website demo</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f954716-e70f-4dfe-9f1c-bac3c7482534/google-io-large-opt.jpg">View large version</a>)</figcaption></figure>

There are two other demos I really like:

*   [Pokedex.org](https://www.pokedex.org) An online index of Pokemon characters (predating PokemonGo!).
*   [2048](https://2048-opera-pwa.surge.sh/) A fun game that has saved me from boredom during hours of air travel.

Again, open the website, load it to your home screen, switch to airplane mode, and then come back.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de80bdb3-30b4-4b35-a833-1778c88c9254/pwa-example-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4cbe6b18-fb3f-4f25-8a77-51cb35390fee/pwa-example-650-opt.jpg" alt="Offline website demo" width="650" height="381" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de80bdb3-30b4-4b35-a833-1778c88c9254/pwa-example-large-opt.jpg">View large version</a>)</figcaption></figure>

If you want to go deeper in the code, I would recommend the following reading:

*   "[Create a Really, Really Simple Offline Page Using Service Workers](https://www.deanhume.com/Home/BlogPost/create-a-really--really-simple-offline-page-using-service-workers/10135)," Dean Hume
*   "[Offline Storage for Progressive Web Apps](https://medium.com/dev-channel/offline-storage-for-progressive-web-apps-70d52695513c#.89q94e79i)," Addy Osmani
*   "[Making a Simple Site Work Offline With ServiceWorker](https://css-tricks.com/serviceworker-for-offline/)," Nicolas Bevacqua, CSS-Tricks

{{% ad-panel-leaderboard %}}

## Going Full Steam: Progressive Web App

I’ve described how to enhance a website to add some native-like functionality. You could go one step further with a full-on progressive web app. In their article "<a href="https://medium.com/google-developers/instant-loading-web-apps-with-an-application-shell-architecture-7c0c2f10c73#.50aqnknm7">Instant Loading Web Apps With an Application Shell Architecture</a>," Addy Osmani and Matt Gaunt refer to a progressive web app as a web app that "can <em>progressively</em> change with use and user consent to give the user a more native-app-like experience." They cite an <a href="https://infrequently.org/2015/06/progressive-apps-escaping-tabs-without-losing-our-soul/">article in which Alex Russell</a> describes progressive web apps as "websites that took all the rights vitamins."

According to <a href="https://developers.google.com/web/progressive-web-apps/">Google’s documentation</a>, progressive web apps are:

*   **Progressive**  
They work for every user, regardless of browser choice, because they’re built with progressive enhancement as a core tenet. This bring us back to what I said at the beginning of this section: Make sure your website works even if all of this fancy new technology is not supported, and treat all of this as progressive enhancement.
*   **Responsive**  
They fit any form factor: desktop, mobile, tablet and whatever is next.
*   **Connectivity-independent**  
They can be enhanced with service workers to work offline or on a slow network.
*   **Fresh**  
They are always up to date, thanks to the service worker updating process.
*   **Safe**  
They must be served via HTTPS to prevent snooping and to ensure that content hasn’t been tampered with.
*   **Discoverable**  
They are identifiable as "applications" thanks to the manifest file and the service worker `registration.scope`, which allows search engines to find them (like any normal old-school website).
*   **Re-engageable**  
They make re-engagement easy through features such as push notifications. Again, for me, this is not mandatory, and you might want to be careful with it.
*   **Installable**  
They allow users to keep the apps they find most useful on their home screen, without the hassle of an app store.
*   **Linkable**  
They can easily be shared via a URL and do not require complex installation.
*   **App-like**  
They feel like an app to the user, with app-style interactions and navigation, because they’re built on the application shell model.

The last point about the application shell is where it gets really interesting and where progressive web apps bridge the gap between classic responsive websites and native apps. If you’ve created a native app, this should ring some bells. In a native app, the user would download the full UI (icons, fonts, etc.) when they install the app. Then, when they launch the app, the content is loaded from the server.

The concept of the application shell is pretty similar: It is the minimum HTML, CSS and JavaScript required to create your UI, the "chrome" of your interface. You would cache this to make the app load quickly. Then, the rest of the content would get dynamically loaded to populate the different views.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fc7f245-d791-4425-bcf1-142233724be1/application-shell-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6f20c4a-c5f9-4b20-8869-e54348f9a90f/application-shell-650-opt.jpg" alt="Explanation of application shell" width="650" height="381" /></a><figcaption>(Image: <a href="https://medium.com/google-developers/instant-loading-web-apps-with-an-application-shell-architecture-7c0c2f10c73#.p9tdc6jg8">Addy Osmani and Matt Gaunt</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6fc7f245-d791-4425-bcf1-142233724be1/application-shell-large-opt.jpg">View large version</a>)</figcaption></figure>

Also, the people at Opera have put together a <a href="https://pwa.rocks/">selection of progressive web apps</a>. If you want a taste of what progressive web apps can do, you’ll find demos and inspiration there.

## With Great Power…

… comes great responsibility. There’s currently <a href="https://adactio.com/journal/10708">some</a> <a href="https://www.kryogenix.org/days/2016/05/24/the-importance-of-urls/">debate</a> in the community about progressive web apps. Here are a few of the issues people are worrying about:

*   Is it really a good idea to hide URLs in a progressive web app? Developers have the choice, but it looked like Chrome was kind of in favor of `standalone` mode. And how are you supposed to share content? (Those awful share buttons might make a big comeback.)
*   A lot of current implementations seem to concentrate on the app part and forget the web part. Are we going to revert to dedicated mobile websites and desktop websites? I’m really looking forward to seeing more responsive and progressively enhanced demos.
*   Loading the application shell is like loading the chrome before the content, whereas many people want a "content-first" approach. Will users have to wait for your content to load even once the interface is already displayed?

If you ask me, not every website should be a progressive web app. For instance, transforming <a href="https://www.stephaniewalter.fr/">my portfolio</a> into a progressive web app was pretty silly, but I did it for a demo; like many people in the industry, my portfolio is also a little playground. In truth, nobody (except maybe my mum) would install my portfolio as an app on their phone. And that’s totally fine, because let’s face it: My portfolio isn’t really app-ish.

So, I guess a progressive web app would be a great idea for websites that users visit on a regular basis, such as news websites and blogs (which is the criterion Chrome uses in determining whether to show the install banner), e-commerce and restaurant-delivery websites (from which users might order regularly), and anything task-oriented (i.e. app-ish). I would add social networks such as Facebook to the list, but building a progressive web app is far less interesting to those companies than building a native one &mdash; how are they supposed to collect and sell all of their users' data if users can only access their services in the browser?

The thing about Facebook is that its mobile website works pretty well. But as soon as you try to view your messages, the website tries to open the Messenger app. Fun fact: Facebook has built a really nice <a href="https://www.messenger.com/">responsive website for Messenger</a> that works on desktop. You can shrink it to a mobile-ish size, and it still works. But as soon as you visit it on a mobile device (or with a mobile user agent), you get the mobile version of the website telling you that you need to install the app. So, when it comes to mobile apps versus progressive web apps (or responsive websites), even though we now have the tools and technology to build a lot of things in a mobile browser, there will always be different factors at play in the decisions of how to implement a service. The fact that you can’t access a phone’s address book from the browser is another piece of the puzzle.

To go deeper in this topic, you might want to read the following:

*   "[A Beginner’s Guide to Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)," Kevin Farrugia, Smashing Magazine
*   "[How We Made the RioRun Progressive Web App](https://www.theguardian.com/info/developer-blog/2016/aug/19/how-we-made-the-riorun-progressive-web-app)," Rich Harris, The Guardian
*   "[Progressive Web Apps](https://nolanlawson.github.io/pwas-2016-05/#/)" (conference slides), Nolan Lawson
*   "[Progressive Web App: A New Way to Experience Mobile](https://tech-blog.flipkart.net/2015/11/progressive-web-app/)," Amar Nagaram, Flipkart
*   "[Washington Post Unveils ‘Lightning-Fast' Mobile Website](https://www.wsj.com/articles/washington-post-unveils-lightning-fast-mobile-website-1473152456)," The Wall Street Journal
*   "[Designing Responsive Progressive Web Apps](https://cloudfour.com/thinks/designing-responsive-progressive-web-apps/)," Jason Grigsby, Cloud Four

## Part 3: Adapting The Website Or Web App To A User’s Current Needs And Context

Mobile devices are now equipped with a lot of different sensors that can get us a lot of information about our users (for best or worse). In this last part of the article, we will focus on how to enhance a website or web app for the user’s current needs, situation and context.

## Ambient Light Detection

<em>Back to Zoe for a moment. Thanks to the notification that popped up on her phone, she gets to the first talk in her schedule on time. She sits down in one of those comfortable theater chairs, and the room gets dark as the talk is about to start. She visits the conference website one last time before putting her phone away.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/810ec84f-7186-4efd-874e-8c877d68451d/ambient-light-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5664c518-c77e-4475-b3cd-a700d4b4d0e4/ambient-light-650-opt.jpg" alt="Website gets darker" width="650" height="381" /></a><figcaption>The website’s visual theme changes to a darker color, so that people aren’t disturbed by a bright screen while listening to the talk. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/810ec84f-7186-4efd-874e-8c877d68451d/ambient-light-large-opt.jpg">View large version</a>)</figcaption></figure>

Using the light sensors on the device, we can adapt the luminosity or contrast of a website to the ambient light. Apart from making a website darker when the user is in a dark room, this could have a lot of practical applications. Many of the websites that my company builds get used in a private room (or on a couch), but that’s not the case for a lot of the professional products and interfaces I build. Those need to be used "in the field" &mdash; outside, inside, on rainy days, on sunny days, anything you can imagine.

For example, I was working on a crane-monitoring interface. The interface works in a Chrome browser on both desktop and tablet. The operator needs to see alerts when the wind is blowing too fast in order to change the cranes' mode so that they don’t fall or collide with each other. The mobile device could be used in a really dark environment, or a lot of light might shine through the window directly onto the operator’s desk. Using ambient light sensors, we could maintain the contrast of the interface when there is too much light in the room, so that people monitoring the cranes will always be able to see alerts if something goes wrong.

In theory, there are two ways to do this. You could use the <a href="https://www.w3.org/TR/ambient-light/">Ambient Light Sensor API</a> to access the intensity level measured by the device’s light sensors. At the time of writing, <a href="https://caniuse.com/#feat=ambient-light">this is supported</a> only in Edge and Firefox for the desktop. A light-level query was expected in the "Media Queries Level 4" specification, but it seems to have been <a href="https://github.com/w3c/ambient-light/issues/12">deferred to "Media Queries Level 5</a>," so this is not for us today.

{{< vimeo id="188563595" >}}

## Enhance Conference Feedback Using Bluetooth URL Transfer

When a talk ends, it’s usually feedback time. When I was at ConFoo, the conference organizers had participants fill out a short form at the end of each talk. Then, a team would collect the forms, read them, scan them and send them to me with an average grade. This was awesome; I got all of the feedback one hour after my talk. But I’m guessing it was also a lot of work for the staff. Let’s see how we can enhance this using Bluetooth, URLs and smartphones, shall we?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7df6ce02-498c-4511-b640-6e8e6882624b/confoo-survey-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69b4c33d-436f-4359-a2e9-9a4c4f504e8c/confoo-survey-650-opt.jpg" alt="ConFoo feedback paper" width="650" height="381" /></a><figcaption>The ConFoo survey given to participants after each talk. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7df6ce02-498c-4511-b640-6e8e6882624b/confoo-survey-large-opt.jpg">View large version</a>)</figcaption></figure>

### The Physical Web Applied to Conference Feedback

This is a good time to meet the "physical web." <a href="https://google.github.io/physical-web/">Google has launched an initiative</a> to "enable quick and seamless interactions with physical objects and locations." The idea is to take advantage of the power of the web &mdash; hence, the URLs to share content and to allow users to interact with objects and locations in their surroundings without having to install anything. If you must, you could think of this as QR codes on steroids. Bluetooth beacons will broadcast URLs, and users' phones in the vicinity will be able to catch those URLs and directly open websites or web applications.

<em>Back to Zoe and our conference. A Bluetooth low-energy (BLE) beacon supporting the Eddystone protocol specification is embedded in the conference poster next to the door.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2aa50a4-aa0d-4bdf-af83-194595392219/pw-01-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76038fb2-739e-4272-ac4e-ae4f9fa03bba/pw-01-650-opt.jpg" alt="URL broadcast" width="650" height="381" /></a><figcaption>The beacon is broadcasting. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f2aa50a4-aa0d-4bdf-af83-194595392219/pw-01-large-opt.jpg">View large version</a>)</figcaption></figure>

<em>A little notification tells Zoe that a URL is being broadcast nearby, which her browser can scan and display.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81bea238-0320-4c95-b912-2c4db961307d/pw-02-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/770a2a02-8264-49c3-bc17-c9e621be4f08/pw-02-650-opt.jpg" alt="Device catches the URL" width="650" height="381" /></a><figcaption>The user gets a notification on their device. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81bea238-0320-4c95-b912-2c4db961307d/pw-02-large-opt.jpg">View large version</a>)</figcaption></figure>

<em>Zoe opens the URL directly in her browser and fills in the feedback form online. Staff are no longer required to scan the forms, and the organizers can do this for every talk.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6689732b-a0ee-45c4-b872-9756ae6671e3/pw-03-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd5ccf76-796f-4bad-a45b-6db0fdb8d39b/pw-03-650-opt.jpg" alt="The browser opens the URL" width="650" height="381" /></a><figcaption>The URL opens in a browser. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6689732b-a0ee-45c4-b872-9756ae6671e3/pw-03-large-opt.jpg">View large version</a>)</figcaption></figure>

For this to work, users need to activate the physical web in the browser and also enable Bluetooth. The physical web is not activated by default (for now). It can be activated on <a href="https://google.github.io/physical-web/try-physical-web">Chrome for both Android and iOS</a>. The physical web has been supported in Chrome for iOS since July 2015, and is available on Chrome for Android in version 49+ and on devices running Kit Kat (4.4) and above.

### What Happens Next Is Simply the Web

The great thing about this is that you could integrate a beacon into almost anything: a street poster, a dog collar, a rental bike or a rental car. The idea is to use this for small interactions for which you would not really consider building a native app, but for which you could easily create a web page. In a video introduction to the physical web, <a href="https://youtu.be/1yaLPRgtlR0?t=1m26s">Scott Jenson describes</a> an interesting way to pay for a parking meter.

The physical web is about getting URLs to phones. What happens next is simply the web.

This is where things get exciting! In her talk "<a href="https://www.slideshare.net/yiibu/the-internet-of-things-is-for-people">The Internet of Things Is for People</a>," Stephanie Rieger explains how you can do a lot of useful stuff by combining a URL with a place (no need for geolocation &mdash; you’ve got a beacon here, remember) and a time (i.e. when the URL is triggered); for example, allowing the user to dig deeper into useful and relevant content. You have the exact context of the user; so, you can trigger a URL for content that adapts accordingly to the situation &mdash; an amazing, progressively enhanced experience tailored to the user’s needs. Bring service workers, WebRTC, notifications, progressive web apps and all of the technologies discussed earlier into the mix, and this, my dear designer and developer friends, is going to be powerful!

Another interesting example from Stephanie’s conference slides is <a href="https://panic.com/blog/the-panic-sign/">Panic’s corporate sign in Portland</a>. The Panic team built an interactive sign for its building, and people can <a href="https://sign.panic.com/">go to a website</a> to change its color. How cool is that? The website is even a progressive web app. It’s fun to change the colors from where I live and imagine them changing on the building, but I’m a little far away. Many people walking around the area might not even be aware of this fun trick. With the physical web, we imagine that Panic could broadcast the URL of its fun little web app around the building, so that passersby can discover it.

If you are looking for more fun ideas for the physical web, check these out:

*   "[Create a Beacon-Enabled Treasure Box](https://www.hackster.io/agent-hawking-1/create-a-beacon-enabled-treasure-box-085314)," Jen Looper, Hackster
*   "[Physical Web Candy Machine](https://www.hackster.io/eely22/physical-web-controlled-candy-machine-ce6711)," Eric Ely, Hackster
*   "[Disney’s Fun Wheel Challenge Hands-On: Makes Waiting Fun](https://www.technobuffalo.com/videos/disney-fun-wheel-challenge-world-of-color-hands-on/)," Roy Choi, TechnoBuffalo Not the physical web, but something similar: Disney’s Fun Wheel Challenge game is available via a URL over Wi-Fi, so that people can have fun while waiting in line for a ride. No app required!
*   "[Physical Web](https://www.slideshare.net/jeffprestes/physical-web-62013819)" (conference slides), Jeff Prestes

### More Fun With the Web Bluetooth API

The physical web is but one attempt to play with Bluetooth and browsers. There’s also the <a href="https://webbluetoothcg.github.io/web-bluetooth/">Web Bluetooth API</a>, which will allow web applications and websites to access services exposed by devices. This means that in the future, we will be able to directly connect and control objects (watches, sensors, smart thermostats, etc.) to a browser through Bluetooth. I say "in the future" because <a href="https://caniuse.com/#feat=web-bluetooth">browser support is pretty low</a> at the moment: Chrome, with a flag. Eventually, we will be able to do really fun things directly in the browser, like change the colors and the mood of this cute little turtle using only a website and Bluetooth connection:

## Geolocation And Battery Status

<em>The conference ends a few hours later. Zoe is tired and decides to use the bike-rental service Velibre to get back to her hotel.</em>

### Adapting the Website to the User’s Location

<em>Zoe arrives on Velibre’s website. A big button says "Find my location," and a little snippet explains to Zoe that she will be able to find bike-rental stations nearby once she grants the website access to her location.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7961b304-ce16-4d4e-991f-e97f6ec3b2ab/gelocation-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/52548c0c-33e2-49dd-8f27-e110ff8f61c0/gelocation-650-opt.jpg" alt="Geolocation dialog" width="650" height="381" /></a><figcaption>Zoe taps the button, a little dialog box appears at the bottom of the website, and she accepts. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7961b304-ce16-4d4e-991f-e97f6ec3b2ab/gelocation-large-opt.jpg">View large version</a>)</figcaption></figure>

With the <a href="https://www.w3.org/TR/geolocation-API/">Geolocation API</a>, we can access the user’s current static location and also monitor changes in location when they move. Basically, you could do a lot of geolocation-related things that native apps do, directly in the browser. This is pretty <a href="https://caniuse.com/#feat=geolocation">well supported in every mobile browser</a> (except for Opera mini). Remember that, in the browser, users have to grant access first. So, you might want to make clear why you need their location. Asking it when the user first visits the website is not the best idea. Again, always ask in context, and explain what the user will gain.

And don’t forget to progressively enhance. A lot can go wrong with geolocation: The user might not see the dialog box (which I’ve seen with my own eyes in user-testing sessions), GPS might not be available, or the user simply might not grant access. Always provide a fallback. It could be as simple as a free-text input field that the user can fill in with their current (or desired) location. Also, don’t assume that users always want a given service at their current location; let them change the location. There was a cinema app that relied only on the user’s current location to provide a schedule of movies. This is great if the user wants to see something nearby, but it doesn’t work so well if they are looking for something to watch on a trip out of town. Don’t assume the user’s intention, and use these technologies as enhancements, not defaults.

### Adapting to Battery Level

<em>It was a really long day. Zoe used her phone a lot, and her battery is almost dead. She taps on Velibre’s button to ask for the closest bike station. The website detects that her battery is really low and loads a static map instead of an interactive one in order to save a bit of power.</em>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba373d1e-c5e6-4a05-8981-40f36ba66004/battery-large-opt.jpg"><img loading="lazy" decoding="async" class="fwi" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/897f520f-3854-4489-8350-53053445d20d/battery-650-opt.jpg" alt="Battery-saving map" width="650" height="381" /></a><figcaption>A little alert informs Zoe about the change to the static map and lets her choose the dynamic map if she wants. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba373d1e-c5e6-4a05-8981-40f36ba66004/battery-large-opt.jpg">View large version</a>)</figcaption></figure>

The <a href="https://www.w3.org/TR/battery-status/">Battery Status API</a> give you access to the battery level of the device. To be responsible, we could, say, propose fewer battery-consuming resources when the battery is low. This would be really useful for battery-draining functions such as GPS, peer-to-peer connections and animation. <a href="https://codepen.io/WhatWebCanDo/pen/epvKNB">Codepen has a demo</a> for you to play with. The API is <a href="https://caniuse.com/#feat=battery-status">currently supported</a> in Chrome, Firefox and Opera for the desktop and in the latest version of Chrome for Android.

## Conclusion

In this article, which is <a href="https://blog.stephaniewalter.fr/en/forget-apps-future-mobile-browser-nightlybuild-2016-conference/">inspired by a talk I gave</a>, I wanted to present you with some APIs, some technologies and some of the cool things you can do with them to make your users' lives easier. The future of the mobile browser is bright, shiny and fun. We can and will be able to build incredibly powerful things with web technologies.

In terms of mobile support for these technologies and APIs, it looks like the Android teams, followed by Firefox, Opera and Microsoft, are currently most focused on taking web apps to the next level and providing a more powerful experience for mobile browser users. iOS, on the other hand, is still far behind. Its lack of support for service workers might be the biggest issue here. If we truly want to be able to fill the gap between natives apps and mobile browsers, we need the notifications and offline functionality provided by service workers.

The big picture is complicated by more than just browser support. What would Apple gain by letting developers build web apps that don’t need to go in the App Store? Apple’s business model is tightly linked to iOS native applications? There’s an app for everything, right?

Is iOS holding us back? I don’t think so. We don’t need to embrace these new APIs and technologies as if they were supported everywhere. Building progressive web apps means building with performance in mind, while still providing a great mobile experience for users on all platforms and browsers. Make sure that users with devices that don’t support everything do not get frustrated with a blank page.

I’m just a designer, only one part of the whole chain. Now it’s your turn to build, to play, to share amazing websites and web apps!

### <span class="rh">Related Reading</span> on SmashingMag:

*   [Testing Mobile: Emulators, Simulators And Remote Debugging](https://www.smashingmagazine.com/2014/09/testing-mobile-emulators-simulators-remote-debugging/)
*   [What Every App Developer Should Know About Android](https://www.smashingmagazine.com/2014/10/what-every-app-developer-should-know-about-android/)
*   [What’s The Deal With The Samsung Internet Browser?](https://www.smashingmagazine.com/2016/10/whats-the-deal-with-the-samsung-internet-browser/)
*   [The Mobile Web Handbook](https://shop.smashingmagazine.com/products/mobile-web-handbook)

{{< signature "da, il, al" >}}

---
title: A Guide To Virtual Reality For Web Developers
slug: guide-virtual-reality-web-developers
author: ada-rose-cannon
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b91b817-790b-431e-b063-5c37c1663f94/vr-diagram-loop-500w-opt.png
date: 2017-09-04T20:54:36.000Z
summary: >-
  Recently, there has been a proliferation of virtual reality (VR) web browsers
  and VR capabilities added to traditional browsers. In this article, we’ll look
  at the state of browsers in VR and the state of VR on the web via the WebVR
  APIs.
description: >-
  Recently, there has been a proliferation of virtual reality (VR) web browsers
  and VR capabilities added to traditional browsers. In this article, we’ll look
  at the state of browsers in VR and the state of VR on the web via the WebVR
  APIs.
categories:
  - User Interaction
  - UX
  - UI
  - WebGL
  - Virtual Reality
---

The web community has experimented with VR before, with VRML, but now WebVR takes a new approach to VR, one more suited to the modern web. We've accelerated 3D on the web since 2011 with the release of WebGL. Now the web can handle VR thanks to new web APIs that take advantage of VR hardware using WebGL.

These APIs enable WebGL content to be displayed in 3D with a VR headset. They also provide headset and controller tracking information to give the user presence in the virtual world.

WebVR was first developed in 2014 at Mozilla. In 2016, an earlier version of the standard was available for desktop Chrome, Firefox and Samsung’s virtual reality web browser: Samsung Internet for Gear VR.

These days, the standard is incredibly well supported on phones and desktop computers for almost all major headsets.

The WebVR standards are worked on in the open, and they represent a collaboration between Mozilla, Google, Samsung, Oculus, Microsoft and, recently, Apple.

This means that a single website that uses WebVR can make an immersive scene and deliver it to all major VR platforms at once, desktop and mobile!

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist">&nbsp;</th>
<th>Mozilla Firefox</th>
<th>Google Chrome</th>
<th>Microsoft Edge</th>
<th>Oculus Browser</th>
<th>Samsung Internet</th>
<th>Safari on iOS</th>
</tr>
<tbody>
<tr>
<th>HTC Vive</th>
<td>Developer Edition</td>
<td>Chromium Experimental build</td>
<td>&ndash;</td>
<td>&ndash;</td>
<td>&ndash;</td>
<td>&ndash;</td>
</tr>
<tr>
<th>Oculus Rift</th>
<td>Developer Edition</td>
<td>Chromium Experimental build</td>
<td>&ndash;</td>
<td>&ndash;</td>
<td>&ndash;</td>
<td>&ndash;</td>
</tr>
<tr>
<th>Windows Mixed Reality</th>
<td>&ndash;</td>
<td>&ndash;</td>
<td>Windows 10 with Creators Update and Developer Mode enabled</td>
<td>&ndash;</td>
<td>&ndash;</td>
<td>&ndash;</td>
</tr>
<tr>
<th>Samsung Gear VR</th>
<td>&ndash;</td>
<td>&ndash;</td>
<td>&ndash;</td>
<td>supported</td>
<td>supported</td>
<td>&ndash;</td>
</tr>
<tr>
<th>Google Daydream</th>
<td>&ndash;</td>
<td>Chrome for Android (with Origin Trial)</td>
<td>&ndash;</td>
<td>&ndash;</td>
<td>&ndash;</td>
<td>&ndash;</td>
</tr>
<tr>
<th>Cardboard</th>
<td>&ndash;</td>
<td>Chrome for Android</td>
<td>&ndash;</td>
<td>&ndash;</td>
<td>&ndash;</td>
<td><a href="https://github.com/googlevr/webvr-polyfill/" rel="noopener noreferrer">via polyfill</a></td>
</tr>
</tbody>
</table>

_WebVR support as of June 2017 (Source: [Mozilla Blog](https://blog.mozilla.org/press/2017/06/mozilla-brings-virtual-reality-to-all-firefox-users/))_

The web’s ability to handle VR content allows one to easily share a VR experience in a URL and view it in the browser without the complicated app stores and long downloading times associated with native VR.

<figure class="video-container"><iframe loading="lazy" width="560" height="315" src="https://www.youtube.com/embed/38H8TaR1bBM" frameborder="0" allowfullscreen></iframe><figcaption>WebVR APIs demonstrated in Samsung Internet for Gear VR</figcaption></figure>

## Additional VR-Related Web APIs In Samsung Internet

These APIs are not part of the WebVR API but are useful for viewing immersive content on traditional websites in an immersive web browser without needing to use WebGL.

These APIs are being developed for Samsung Internet for Gear VR. We hope they will be picked up by other browsers and standardized.

### Panoramic Video

This involves the ability to play panoramic videos (monoscopic and stereoscopic) immersively by setting the `type="dimension=360;"` attribute on a `video` tag. These videos also get enhanced in Samsung Internet 5.0 by allowing the user to pan around within the video using their fingertips.

Possible values:

*   `dimension=3d-lr`: side-by-side 3D video
*   `dimension=3d-tb`: top-to-bottom 3D video
*   `dimension=360`: 360-degree video
*   `dimension=360-lr`: side-by-side 3D 360-degree video
*   `dimension=360-tb`: top-to-bottom 3D 360-degree video
*   `dimension=180`: 180-degree video
*   `dimension=180-lr`: side-by-side 3D 180-degree video
*   `dimension=180-tb`: top-to-bottom 3D 180-degree video

<pre><code class="language-markup">&lt;video src="/360.webm" type="video/webm; dimension=360;"&gt;&lt;/video&gt;
</code></pre>

### Changing the Sky

Another API available in Samsung Internet for Gear VR is a JavaScript API for changing the background image of the VR web browser to one of the developer’s choosing.

Your traditional 2D website will still be visible, but the surroundings will be set to one that matches the environment of your website.

<pre><code class="language-markup">
window.SamsungChangeSky({ sphere: 'https://site.com/blue-sky.jpg' });
</code></pre>

<figure class="video-container"><iframe loading="lazy" width="560" height="315" src="https://www.youtube.com/embed/9NefsqY3uGw" frameborder="0" allowfullscreen></iframe><figcaption>Example of changing the Skybox with JavaScript in Samsung Internet for Gear VR</figcaption></figure>

## What Is WebVR?

WebVR is a set of cross-browser JavaScript APIs that provide a variety of VR-related utilities to place the user in an immersive environment generated using WebGL.

By providing side-by-side rendered 3D images, these APIs will handle all of the complexity involved in displaying an undistorted stereoscopic 3D image to the user.

I won’t go into the details of implementing the standard here because the standard is still changing. Most users will never need to deal with them directly, because WebGL tools and libraries often handle the WebVR APIs for you.

{{% feature-panel %}}

## State Of The WebVR APIs

The current version of the API is known internally as version 1.1\. Version 2.0 will change some of the method names and remove some unused methods. It will also add some additional functionality for some hardware and use cases which were not anticipated during the first iteration of the API.

The precise details of the APIs can be [read on the Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API), and the standards are discussed [on GitHub](https://w3c.github.io/webvr/). There is interest from within the [WebVR community group](https://www.w3.org/community/webvr/) and the W3C to move to a W3C working group once they are ready.

Essentially, the WebVR API provides the following:

*   Headset tracking allows the user to look around in the virtual environment. Frame interpolation is built in, so that it is always tracking the user’s head, even if you skip the occasional frame.

<figure class="video-container"><iframe loading="lazy" width="560" height="315" src="https://www.youtube.com/embed/zck2afXvDvg" frameborder="0" allowfullscreen></iframe><figcaption>Pass-through camera, demonstrating head tracking in VR</figcaption></figure>

*   "Six degrees of freedom" and "three degrees of freedom" controller support allows controllers like those of the HTC Vive and the Gear VR to work in virtual reality. It allows the user to use their hands to interact with the virtual environment.
*   Information is given about how the headset needs the 3D information rendered, such as the field of view and how to position the render for each eye on the canvas.
*   A new headset-specific `requestAnimationFrame` is synced to the refresh rate of the display in the headset.
*   There is a method of submitting the rendered frames to the headset in the form of a WebGL-enabled canvas element.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e28da06-bcd3-42b2-821b-30e8d8f6f5a1/image4-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1187c3a-6f99-4da1-b1c1-6ed602c79b2f/image4-800w-opt.png" width="800" height="662" alt="Diagram describing the loop for VR." /></a><figcaption>Diagram describing the loop for VR. The headset provides position and rotation data; the developer uses this data to render the scene from the user’s point of view, then sends the rendered data to the headset to be distorted and displayed to the user. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e28da06-bcd3-42b2-821b-30e8d8f6f5a1/image4-large-opt.png">View large version</a>)</figcaption></figure>

## What Does It Mean To Build A WebVR Immersive Experience?

Surprisingly, building a virtual reality website raises many of the same problems as building a good mobile website or progressive web app.

### Starting Fast

One of the biggest problems being tackled on the web today is network performance, which is important because:

*   user attention spans are shrinking,
*   networks are getting more congested,
*   websites are getting bigger than ever.

WebGL and WebVR websites are certainly no exception to size. They can get very large if one is not careful!

Right now, VR content has an edge over traditional content because it is novel and interesting enough that users will likely wait a bit longer to have a go. Still, getting your 3D experience started in under a few seconds is extremely important. Users are impatient and only getting more so.

Before your VR-capable website has loaded, it is just a 2D website and a promise of cool things to come.

My advice here is to not preload everything. Instead load just enough for the user to get started, then dynamically load and start caching the rest. This behavior should be familiar if you have read about [Google’s PRPL pattern](https://developers.google.com/web/fundamentals/performance/prpl-pattern/).

Even just showing a blurred 360 skybox and some low-poly content, allowing the user to look around, will buy you precious seconds of engagement to bring in additional content and to bootstrap an engaging experience.

Showing something basic but fast is far better than losing the user because they’ve gotten bored waiting for a loading bar to complete.

But bear in mind, network operations can be CPU-intensive and block the main thread. This could give the user a bad experience if it happens a lot, so it is a fine line to walk.

Perhaps one or two very intensive assets need to be preloaded to avoid breaking the experience. However, if you have so many that it is taking a long time to start, then perhaps it’s worth thinking about finding a more performant alternative.

Making good use of a [service worker and the Cache API](https://medium.com/samsung-internet-dev/a-beginners-guide-to-service-workers-f76abf1960f6) to cache static assets for fast return visits is a great way to keep users coming back for more.

### Progressive Enhancement

The two main platforms for VR are polar opposites: high-end desktop computers with advanced controllers, and mid- to high-level mobile phones, which might have only a single rotation-tracked controller or no controller at all!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b02e35ea-bad3-4972-be85-32bcc865bae1/image3-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd065d21-0204-46c0-a363-4f18f1ba0d23/image3-800w-opt.jpg" width="800" height="600" alt="" /></a><figcaption>A photo of an HTC Vive with a position-tracking controller, Samsung Gear VR, Google Daydream and a pile of Google Cardboards in the back. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b02e35ea-bad3-4972-be85-32bcc865bae1/image3-large-opt.jpg">View large version</a>)</figcaption></figure>

This presents us with two challenges:

*   maintaining a consistent frame rate across platforms with wildly differing performance capabilities,
*   presenting a user-friendly experience across VR devices with a wide range of inputs.

Phones have by far the largest reach due to the popularity of Gear VR and Daydream and the cheap price and high availability of the Google Cardboard headsets.

Below, I have described some typical controller configurations. You don’t need to support them all, but handling the "no controller" situation as a baseline and also supporting another controller option if applicable will allow everyone to experience something. Supporting all controller configurations would be nice, but in my opinion is not a reasonable expectation.

Some libraries, such as [Universal Controls from A-Frame Extras](https://github.com/donmccurdy/aframe-extras), try to make the best out of whatever is available.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a015bc9a-0c9b-4d00-9b15-d6bf0038d449/image1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4bf6002d-031a-40a8-9f63-c3ff04a056d6/image1-800w-opt.png" width="800" height="400" alt="" /></a><figcaption>Web-compatible controllers with increasing levels of immersion. From left to right: Gaze-Based Tracking, Traditional Gaming Controllers, Rotation-Tracked Controllers, Position- and Rotation-Tracked Controllers, Full Gesture Recognition. (Eye illustration: Wikimedia Commons) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a015bc9a-0c9b-4d00-9b15-d6bf0038d449/image1-large-opt.png">View large version</a>)</figcaption></figure>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<thead>
<tr>
<th data-tablesaw-priority="persist">Interaction mechanism</th>
<th>How it increases engagement</th>
<th>Hardware and support</th>
</tr>
</thead>
<tbody>
<tr>
<td>Gaze-based interaction</td>
<td>Look at something to use it. (Most users will require this.)</td>
<td>Cardboard-like headsets; users with limited mobility for controllers</td>
</tr><tr>
<td>Traditional controllers (e.g. Xbox, Playstation)</td>
<td>Works with widely supported <a href="https://medium.com/samsung-internet-dev/the-gamepad-reloaded-5ba866770003#.8tzhs8qz2">Gamepad API</a><br>
<td>Can be used anywhere the API is supported on desktop and mobile (needs latest Safari)</td>
</tr><tr>
<td>Rotation-Tracked Controllers</td>
<td>Allows the user to gesture like a laser pointer</td>
<td>Can be used in Daydream devices and Gear VR to similar effect to the fully tracked controllers</td>
</tr><tr>
<td>Position- and Rotation-Tracked Controllers</td>
<td>Fully tracked hands; allows great immersion and interaction.</td>
<td>Most high-end VR has these, such as HTC Vive and Occulus Touch</td>
</tr><tr>
<td>Hand Tracking</td>
<td>Allows user’s hands to interact with the scene; great immersion</td>
<td>Built into Hololens, can be added by using the Leap Motion tracker</td>
</tr>
</tbody>
</table>

### Asymmetric Play

As with progressive enhancement on the web, supporting all levels of hardware does not mean you need to deliver the same experience to all.

A user with two fully tracked hands in the virtual world will have a much more engaging experience and should not be limited by being delivered the same experience as someone with no controller.

For example, a VR app in which you produce VR artwork could use tracked controllers to produce art on high-powered machines; on mobile, a user would be able to view this art in VR but be unable to edit it.

Another example would be a networked VR multiplayer game in which players use tracked controllers to play the game; a mobile viewer could watch it and use gazed-based interactions to choose different points of view.

### Test as You Develop

Like modern web design, the key is to design mobile-first. As you build your scene, regularly test it on **real** mid-level smartphones with no controllers to ensure it will work for the majority of your users.

WebVR allows you to target both platforms at once. However, delivering the same content to both could result in mobile devices struggling or desktops not being used to their full potential.

There is no problem having very well-performing graphics. A stylized low-poly appearance can look fantastic and render very quickly.

To upgrade graphics, one solution is to provide options for graphical quality before the user starts using WebVR. If the user requests high quality, then start downloading the large or difficult-to-render graphics.

Something more difficult but more seamless would be to start on the lowest graphical setting and detect how well the device is performing using commands such as `requestIdleCallback` or measure how long the rendering takes. If the device is running well, then maybe increase the graphics settings. If frames start getting skipped, then dynamically reduce them.

When you are upgrading your scene, you might decide to do a few things:

*   increase draw distance,
*   download and use high-resolution models or textures,
*   use more complex shaders.

This will ensure that users on mobile and desktop get the best possible experience. For most use cases, though, it is probably fine if desktop users get the mobile experience, because you can guarantee it will maintain a great frame rate on the desktop if it also does on mobile.

After all, there is more to a great scene than visual fidelity. Highly stylized games such as Team Fortress 2 still look great today, whereas "realistic" games from the same era have not aged so well.

A great scene should have a well-designed graphical style, with bold colors and strong silhouettes. This will help low-power and low-resolution devices look good, but will also still look great on desktop devices, needing only a bit of extra polish.

In VR, bear in mind that most users will have the equivalent of poor eyesight. So, minimize text or anything that will cause the user to strain to see something.

{{% ad-panel-leaderboard %}}

## What Does the Web Bring to VR?

The web is trying to solve some of the problems currently facing VR.

One of the biggest issues is that the user has to make a **big commitment** for a one-off experience that they might not want to come back to.

In native mobile and desktop VR, one has to download the app from an app store such as the Oculus store on Gear VR or from Steam for the HTC Vive or Oculus Rift.

This app store pattern lends itself well to expensive video games, in which users have already invested some money and so are going to return again and again. But for a one-off experience such as shopping, viewing a movie or trying a new social platform, this can be a high barrier to entry.

Users tend to be put off by the idea of having apps lying around on their device, taking up space or using up a large amount of their data allowance to download — especially users whose mobile devices have limited disk space or network data caps.

On the web, once the user leaves a page, they don’t have to worry about content hanging around, because the browser will clean it up if space is needed. If space is available, the developer can cache content on the device for when the user returns, letting the developer have their cake and eat it, too.

Of course, this requires the developer to make VR websites that are not stored as a single giant bundle; otherwise, the gains the web can provide will have been lost.

By delivering VR assets dynamically and separately like those of a web page, you can take advantage of all of the smart caching that the web can provide from the CDN, all the way down to the HTTP cache and the service worker’s Cache API on the device.

Furthermore, the user can jump right into your VR experience with very little waiting.

A highly optimized WebVR website should render the first frame within a single second of the user landing on the website — totally cutting out any lengthy initial downloads or app stores, and massively increasing engagement.

An experience can be shared with nothing but a URL, which can be distributed by social media or email or even written on a wall or displayed on a TV, making it much more likely that your VR content will go viral due to its low barrier to entry.

### Making the Most Out of the Quick Web

One feature that many WebVR websites have is that, before entering VR, the user can view and interact with the scene on their 2D display. The view will often rotate with the phone, giving the appearance of a magical window into a virtual space.

This magical window is a powerful pattern. It gives the user a preview of the VR scene without the need for a VR headset. This is great for when they don’t have their VR gear on hand or are on public transportation and don’t want to wear VR equipment in public.

Once the user has gotten a taste, they will be encouraged to bookmark your website to try it in VR at a time more suitable for them.

### The Web Has High-Level Interfaces to Low-Level APIs, Bringing Advanced Technology to Any Developer

Many web APIs you may have heard of or used have become massively more relevant in a VR context:

*   **WebSockets**  
    These are used to stream text and binary data to a server in real time. For VR, they can be used to sync hundreds of users in real time to enjoy a shared experienced and to view avatars representing each other. I recently produced an open-source demo in which I did this live for [over 150 users at a conference](https://medium.com/samsung-internet-dev/wow-that-was-some-night-in-vr-ba091be38794).
*   **WebRTC**  
    To expand upon shared VR, one can also use WebRTC to maintain peer-to-peer connections for binary data and video and audio streaming. This can be used to allow two avatars to voice chat or to sync the position and posture of a VR avatar without going through a central server. This can be used to connect six to eight users at a time.
*   **WebAudio**  
    [WebAudio](https://medium.com/samsung-internet-dev/web-audio-on-different-platforms-67fc9ffc2c4e) is one of the most surprisingly powerful APIs. The browser contains everything you need for audio manipulation and analysis. One can even use a panner node for 3D spatial audio in VR. For producing virtual environments that have an immersive feel, WebAudio is more important than ever.
*   **SpeechRecognition**  
    Newer browsers contain a built-in speech recognition engine! This is useful for giving commands and entering text when a real or virtual keyboard is difficult or unwieldy. Samsung has built a great [example for VR](https://samsunginter.net/word-drop/).

Many web APIs you may have heard of or used have become massively more relevant in a VR context:

*   **WebSockets**  
    These are used to stream text and binary data to a server in real time. For VR, they can be used to sync hundreds of users in real time to enjoy a shared experienced and to view avatars representing each other. I recently produced an open-source demo in which I did this live for [over 150 users at a conference](https://medium.com/samsung-internet-dev/wow-that-was-some-night-in-vr-ba091be38794).
*   **WebRTC**  
    To expand upon shared VR, one can also use WebRTC to maintain peer-to-peer connections for binary data and video and audio streaming. This can be used to allow two avatars to voice chat or to sync the position and posture of a VR avatar without going through a central server. This can be used to connect six to eight users at a time.
*   **WebAudio**  
    [WebAudio](https://medium.com/samsung-internet-dev/web-audio-on-different-platforms-67fc9ffc2c4e) is one of the most surprisingly powerful APIs. The browser contains everything you need for audio manipulation and analysis. One can even use a panner node for 3D spatial audio in VR. For producing virtual environments that have an immersive feel, WebAudio is more important than ever.
*   **SpeechRecognition**  
    Newer browsers contain a built-in speech recognition engine! This is useful for giving commands and entering text when a real or virtual keyboard is difficult or unwieldy. Samsung has built a great [example for VR](https://samsunginter.net/word-drop/).

## What Effect Might VR Have On The Web In The Long Term?

VR has already had an effect on the web platform; the WebVR APIs have been implemented across multiple platforms; and there are discussions about creating a WebVR working group within the W3C.

VR is already going mainstream, and with augmented-reality and mixed-reality devices starting to enter the consumer realm, it is important that the web be ready to take advantage of the new platforms.

WebVR as we know it today relies entirely on WebGL. Optimizing for WebGL will mean that browser vendors will have to look at taking advantage of hardware optimizations to increase rendering speed towards that of a natively compiled app. Speed is important, because dropping frames in VR can have disastrous effects, even to the point of making the user ill!

**WebGL 2** will soon be reaching stable browsers. Version 2 brings WebGL closer to the OpenGL ES 3.0 specification. Greater visual fidelity and faster ways to do advanced graphics will make VR truly an incredible visual experience.

WebAudio might be required to produce more accurate 3D audio transformations, known as head-related transfer functions, to better reproduce the high-quality 3D audio required by big-budget productions. Accurate 3D audio will be essential to delivering high-quality immersive video content such as 360-degree movies and immersive audio experiences.

Scripting on the web would benefit from significant performance improvements as well. A number of JavaScript APIs are in the works that can be used to increase performance on the web.

JavaScript itself can be optimized and precompiled. Another option is to compile other languages to WebAssembly (**WASM**). This can speed things up across the board, providing a bundle that is smaller to download and faster to parse and execute. If used wisely and modularly, WASM could be used to make the core rendering engine of a WebVR experience, which we could still interact with using JavaScript as we do today.

The browser can make use of web workers to enable calculations that do not block the main thread. This is good because the main thread is primarily used for rendering. Web workers are useful for manipulating large amounts of data with CPU-intensive calculations such as physics engines. By isolating the calculations from the main thread in this way, they are less likely to trigger frame drops.

Unfortunately, some cost is associated with sending data to and from web workers to use them in the main thread. This is alleviated partially by transferable objects. Transferable objects such as ArrayBuffers allow you to change the owner of the object, but handling the transferring of this object can be difficult and error-prone if a mistake is made. (I’ve written about [using ArrayBuffers on the web](https://medium.com/samsung-internet-dev/being-fast-and-light-using-binary-data-to-optimise-libraries-on-the-client-and-the-server-5709f06ef105).)

A new API called SharedArrayBuffer will allow multiple workers to share the same ArrayBuffer, which is useful for this case.

On the topic of workers, part of the issue is that, right now, the thread that renders the web page also needs to be used to render the WebGL scene. So, any side effects of other code that you run on the main thread, such as garbage collection or CPU-bound functions, could cause frames to be dropped.

OffscreenCanvas enables rendering to be performed in a web worker. This will help the very important and sensitive rendering loop to be isolated from the other threads.

The other important rendering use case is prerecorded 2D and 3D video. These can be used as textures in WebGL. But they lack fine-grained control. Just as we have an `audio` element and an AudioContext in JavaScript, we will need to add a videoContext to enable performant video manipulation to assist with playing 360-degree videos in 3D.

An area where VR currently lies at odds with the web as a whole is the rendering of documents. Displaying documents is the core functionality of the web platform, but displaying a document in WebGL is nigh impossible without some very slow, very clever rerendering.

It would be great to bring them together by having the browser expose rendered DOM content to WebGL. This would enable us to take advantage of the web’s power for 2D interfaces, but it could potentially be a security and privacy risk!

{{% ad-panel-leaderboard %}}

## Another Path

WebGL-based VR doesn’t necessarily have to be the future of VR on the web. Having to perform even the simplest use case for WebVR in WebGL seems shortsighted at best and potentially fatal for VR on the web in the long run.

Part of the strength of the web is that HTML is a declarative language. Browsers can interpret the language according to the platform. You won’t see the exact same website on your desktop computer as you would on your phone or TV. VR is yet another platform in the variety of media to experience the web.

By being declarative, like HTML or CSS, VR on the web could automatically handle rendering to balance rendering speed and visual fidelity. A high-end computer could use advanced shaders and detailed models; a low-power mobile phone could automatically use simple shading and low-poly models — much like the way the `picture` element can download images that are of the correct resolution and then crop for the given device.

HTML could be extended to include some common VR use cases, such as playing 360-degree and 3D videos and images, displaying 3D models, and moving bits of a web page outside of the 2D viewport into 3D space.

Samsung has started to look at some of these use cases in the web browser, Samsung Internet for Gear VR.

It has built-in support for 3D video using the `video` element. Displaying a side-by-side 3D, 360-degree video requires just an HTML tag:

<pre><code class="language-markup">&lt;video controls src="360video.mp4" type="video/mp4; dimension=360-lr;"&gt;
</code></pre>

## The Middle Path

Of course, these needn’t be mutually exclusive. The web can partially handle and optimize for simple VR use cases, while also providing optimizations for building immersive VR from scratch with WebGL.

The Extensible Web manifesto hinges on the idea that the web does not have to sacrifice extensibility for ease of use, that the community can use the low-level tools provided to extend the web platform using libraries.

VR is one case where this vision seems very relevant. We already have the low-level tools of WebGL and the WebVR APIs.

The [A-Frame](https://aframe.io) library provides custom HTML elements to build WebGL-based 3D scenes. A-Frame is usable on its own or with popular frameworks such as React and Angular.

A-Frame enables any web developer with HTML experience to describe VR-ready 3D scenes and to control them using familiar JavaScript. Even tools such as jQuery, Angular and React can be used to change a scene because, at the end of the day, it is still just HTML.

## Conclusion

The web has the power to bring virtual reality to the world, to every consumer, to every developer.

It is still early days for VR on the web, but now is the time to get building, to see what works and what doesn’t.

The web can show that VR is for more than video games. VR can be used to enhance everything we currently do on the web and even enable new interactions only possible in an immersive medium.

As developers, we can start building VR experiences on the web today. By getting involved and giving feedback about the standards process, we can ensure that VR on the web becomes a robust standard, paving the way for future developers to build on.

Even if you don’t think VR is mature yet, with mixed-reality and augmented-reality devices around the corner, what we build today will still be relevant then. The interface patterns we build for VR apply to all immersive media. Don’t get left behind.

Together, we will build the web of tomorrow.

<div class="c-felix-the-cat">
<h4 class="h3">Developing For Virtual Reality</h4>
<p>Any developer can create content for VR nowadays. To get a better understanding of VR development, working a demo project can help. <a href="https://www.smashingmagazine.com/2016/09/developing-for-virtual-reality-what-we-learned/" class="btn btn--medium btn--blue">Read a related article&nbsp;→</a>
</div>

{{< signature "rb, vf, yk, al, il" >}}

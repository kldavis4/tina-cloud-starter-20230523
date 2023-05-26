---
title: 'Best Of Both Worlds: Mixing HTML5 And Native Code'
slug: best-of-both-worlds-mixing-html5-native-code
image: >-
  https://www.smashingmagazine.com/general/2013/06/25/136973-revision-21/attachment/voyager-screenshot-shaded_500_mini/
date: 2013-10-17T10:06:47.000Z
author: peter-traeg
description: >-
  Much has been written recently in the ongoing debate between native and HTML5
  applications. There are three principal ways to develop a mobile solution:
  **native code, hybrid mobile app, mobile Web app**. Developing an application
  in HTML5 is a way to leverage code across multiple platforms, rather than
  having to write the entire application from scratch for each platform.
categories:
  - Mobile
  - Opinion Column
  - Apps
  - HTML5
---
Much has been written recently in the ongoing debate between native and HTML5 applications. There are three principal ways to develop a mobile solution:

*   native code,
*   hybrid mobile app,
*   mobile Web app.

Developing an application in HTML5 is a way to <strong>leverage code across multiple platforms</strong>, rather than having to write the entire application from scratch for each platform. As such, much of the user interface, perhaps the entire interface, would be done in HTML.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Providing A Native Experience With Web Technologies](https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/)
*   [<span class="headline">How To Design A Mobile Game With HTML5</span>](https://www.smashingmagazine.com/2012/10/design-your-own-mobile-game/)
*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)
*   [Building A First-Class App That Leverages Your Website](https://www.smashingmagazine.com/2016/02/building-first-class-app-leverages-website-case-study/)

{{% feature-panel %}}

“Hybrid application” is a term often given to applications that are developed largely in HTML5 for the user interface and that rely on native code to access device-specific features that are not readily available to Web applications. Much of this native code is non-visual in nature, simply passing data back to the HTML5 layer of the app, where it is rendered to the user. Libraries such as <a href="https://phonegap.com/">PhoneGap</a> provide this capability.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49312c8e-a970-4314-b08b-be6655f0f8d7/html5-native-arrows-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139148" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/638b861a-2814-4b19-a2c0-35a306777897/html5-native-arrows-500-mini.png" alt="html5-native-arrows_500_mini" width="500" height="84" /></a>

Much of the debate is not about whether HTML5 is up to the task of powering a mobile application’s user experience. Mark Zuckerberg’s <a href="https://techcrunch.com/2012/09/11/mark-zuckerberg-our-biggest-mistake-with-mobile-was-betting-too-much-on-html5/">comments</a> about some of the <a href="https://lists.w3.org/Archives/Public/public-coremob/2012Sep/0021.html">difficulties</a> Facebook has encountered with HTML5 on mobile are well known. Some of Facebook’s issues could likely be addressed through the techniques outlined by Sencha in its <a href="https://www.sencha.com/blog/the-making-of-fastbook-an-html5-love-story/">Fastbook</a> application and by LinkedIn in its <a href="https://engineering.linkedin.com/linkedin-ipad-5-techniques-smooth-infinite-scrolling-html5">infinite scrolling post</a>. Despite the latter article, LinkedIn subsequently <a href="https://venturebeat.com/2013/04/17/linkedin-mobile-web-breakup/">switched directions</a> towards using more native code.</p>

## Why Not Mix It Up?

Rather than build an app entirely with native or HTML5 technology, why not mix and match the technologies? With a hybrid application, building a mobile experience that leverages both native and HTML5 code for the user interface is quite possible. This enables the developer to use the most appropriate tool for the job when developing the user interface.

Clearly, developing portions of the user experience in two or more different technologies has some downsides. Chiefly, you would need developers who can handle both native development and HTML5. The portion of the user interface in native code couldn’t be readily used on other platforms and would need to be redeveloped. Given the broader scope of knowledge required by this technique and the difficulties outlined above, why would anyone want to embark on an endeavor that mixes user-interface technologies?

## HTML For Rich Document Layout

Perhaps your user experience dictates that documents be displayed in the application with rich formatting. While text formatting can be accomplished on platforms like iOS with <code>NSAttributedString</code>, this <strong>document structure is not readily portable to other device platforms</strong>, nor does it provide the full complement of features found in HTML. If the document requires formatted content such as tables to be displayed, then a solution like <code>NSAttributedString</code> won’t be up to the task.

Consider the iPad application below, which was developed for a genetic sequencing company. Here we have an example of a hybrid UI:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/def612c6-3cb5-4532-8057-2eb088ea42a0/voyager-screenshot-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139151" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ebb117e0-358d-44a7-a1ab-04efcc9fb028/voyager-screenshot-500-mini.png" alt="voyager-screenshot_500_mini" width="500" height="375" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/def612c6-3cb5-4532-8057-2eb088ea42a0/voyager-screenshot-mini.png">See larger view.</a>)</em>

Just looking at this application, it’s not readily apparent what has been done in native code and what portions are HTML5. <strong>Users of the application would be hard pressed to tell the difference.</strong> The document along the right side is of variable length. The table contains expandable rows, complete with CSS3 animations, and other text sections in the document vary in height as well.

Documents such as this are what HTML does best. Trying to create something like this in native code would have entailed considerably greater effort, with little benefit to the user. In this application, the HTML5 is generated with a mustache template, via the <a href="https://github.com/groue/GRMustache">GRMustache</a> library for iOS.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80fc7179-617f-4ed0-9717-eebc76b033ff/voyager-screenshot-shaded-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139150" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7381f4e-c87f-4fb2-af43-feb9485fb7a7/voyager-screenshot-shaded-500-mini.png" alt="voyager-screenshot-shaded_500_mini" width="500" height="424" /></a><br>
<em>The illustration above shows the technologies used to draw each portion of the screen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80fc7179-617f-4ed0-9717-eebc76b033ff/voyager-screenshot-shaded-mini.png">See larger view.</a>)</em>

Note that as the user scrolls up, the native document header near the top on the right dynamically resizes to show more content, thus illustrating how portions of the user interface can interact with each other. The user can tap on links and buttons in the HTML document area to pop up an internal Web viewer to load related documents. As we’ll see later in this article, creating this linkage between native and HTML experiences is relatively easy.</p>

## Desire For A “Best Of Breed” Approach

As we’ve seen, a given screen may readily mix the two technologies to provide a seamless experience. You may wish to use a native <code>UINavigationController</code>, with its associated <code>UINavigationBar</code>, on iOS, or use the action bar in an Android application. The remainder of the screen may be rendered in HTML5.

Below is an application that uses HTML5 for its shopping-cart experience, but retains the native navigation controller and tab bar for moving between pages of the workflow:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/372ef2a3-4312-4111-a978-3cad78e3403b/gallery-prints-1-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139154" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2a645d3b-d104-4caf-85cd-8c6191cc8b4f/gallery-prints-1-500-mini.png" alt="gallery-prints-1_500_mini" width="500" height="750" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/372ef2a3-4312-4111-a978-3cad78e3403b/gallery-prints-1-mini.png">See larger view.</a>)</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2df44483-798e-483d-8fd1-32984f16c013/gallery-review-order-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139156" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ba8d1a1-b4f8-434d-b151-0b44dcf4bc8b/gallery-review-order-500-mini.png" alt="gallery-review-order_500_mini" width="500" height="750" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2df44483-798e-483d-8fd1-32984f16c013/gallery-review-order-mini.png">See larger view.</a>)</em>

Here, <strong>the HTML5 content is actually loaded from a server</strong>, and it controls the workflow throughout the experience. A defined API allows the server-supplied HTML content to modify the contents of the navigation controller bar to suit the page in the workflow.

You may find that native controls, such as MapKit on iOS, provide superior performance to what can be achieved in HTML5. In this case, your HTML5 code could communicate with the iOS native layer and ask it to present the native content over or adjacent to the HTML content.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddd620f4-20e9-4f8e-b9dc-857a362ced8f/gallery-map-pin-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139158" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/069ee9d5-6860-4d20-b316-8e84968ad4f2/gallery-map-pin-500-mini.png" alt="gallery-map-pin_500_mini" width="500" height="750" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddd620f4-20e9-4f8e-b9dc-857a362ced8f/gallery-map-pin-mini.png">See larger view.</a>)</em>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59e792f6-c334-4e6f-92ef-a4fcd882bc03/gallery-loc-selected-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139160" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d32b2533-a1fb-4844-a434-684a246b62e2/gallery-loc-selected-500-mini.png" alt="gallery-loc-selected_500_mini" width="500" height="750" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/59e792f6-c334-4e6f-92ef-a4fcd882bc03/gallery-loc-selected-mini.png">See larger view.</a>)</em>

The examples above illustrate a native store-locator experience, displayed over top of the HTML5 workflow. Upon the user selecting a store location, the data would populate the HTML5 content, and the user would continue their workflow.

Once the user has completed interacting with the map, the results of their interaction may be passed back to the HTML5 document for further handling. Depending on how you wish to structure the application, <strong>native “widgets” may be implemented for each platform</strong> (iOS, Android, Windows, etc.) and then invoked from the common core HTML5 application. In this strategy, the HTML5 code would provide the workflow for the application, and the native content would sit in the background, waiting to provide the supplementary experience when needed.

If done properly, the user would have little indication of which portions are done in native code and which in HTML.

## Ease Of App Updates

Most people are aware that in order to update the native code on an iOS or Android app, it is necessary to resubmit the application through the normal publishing channels for that platform. In the case of iOS, it can take as long as seven days to get app updates approved by Apple. This makes it more difficult to time app updates to marketing requirements and to rapidly respond to changing business needs. Exposing a portion of the user experience through HTML and JavaScript means that some of the experience can be served from the Web and thus be dynamic.

As we saw earlier, it’s possible for this Web-served content to <strong>invoke native code in your application via a “bridge”</strong> that you create. This is much the same as the bridging mechanism that allows HTML code to communicate with native code in PhoneGap via the <a href="https://docs.phonegap.com/en/3.0.0/guide_hybrid_plugins_index.md.html">PhoneGap plugin interface</a>. The example application shown earlier uses this technique. This approach was chosen chiefly so that the purchasing workflow could be altered without having to redeploy the native application. A page served from the Web may now seamlessly display a natively rendered map using whatever mapping capability is present on the device. A well-defined interface between your Web page and the surrounding native container makes this possible.</p>

### Watch That Content!

For content coming from the Web, it’s generally best to restrict the traffic that can flow over this bridge. The built-in functionality of something like PhoneGap provides access to a wide range of device information, some of which may be well beyond your application’s purpose. If that Web content is compromised for some reason, through something like cross-site scripting, you might suddenly find this content invoking native code in a manner you never intended.

For this reason, when bridging from Web-sourced content to native code, use your own bridge code in order to tightly control exactly what the dynamically loaded content may invoke. Some platforms have additional controls to limit what native code may be invoked from a Web view. On Android, classes must explicitly register themselves as being <a href="https://developer.android.com/guide/webapps/webview.html#BindingJavaScript">JavaScript-accessible</a>. On Android 4.2, this can be further restricted to the individual methods by adding an <code>@JavaScriptInterface</code> annotation on the methods that you wish to access from a Web view.</p>

### Things to consider

*   Pulling content directly from a Web server is fine if the user is online. Remember that these are mobile applications with the potential for connectivity issues. What happens if network connectivity is interrupted? Some **offline capability** could be retained through the use of [AppCache](https://developer.mozilla.org/en-US/docs/HTML/Using_the_application_cache), but this needs to be planned for. Another approach will be covered in an upcoming section where updates to the HTML content are stored locally.
*   Hosting content on a Web server requires some **infrastructure**. There are now more "components" that must be considered as part of your complete app solution. It's no longer just some native code that's been deployed via the AppStore and potentially a set of backend services. Care must be taken that site updates do not conflict with the existing interface in the mobile applications. Keep in mind that if site changes necessitate an update to the mobile app itself, not everyone will necessarily update their copy of your app quickly, if at all. For this reason it may become necessary to version the site content so that it may be consumed with older versions of your mobile app. This is very much like the versioning built into some [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) based interfaces in order to support compatibility with older client applications.
*   Apple takes a dim view of applications that are merely a Web view wrapped in a native app. **Submissions to the iOS AppStore** will likely not be approved if you've done nothing more than wrap some Web content in a native app. Apple expects your application will make use of some device features that cannot be otherwise accomplished in Mobile Safari. Consider if your application can benefit by integrating with the camera, contact list, local data storage, offline operation, etc. Also remember that the content served in these Web views needs to remain consistent with the original submitted intent of the application.If you create a word-search game and then suddenly start serving totally unrelated content in your webviews this will violate Apple's terms and the app could be pulled from the AppStore. In accordance with the iOS developer agreement, updates may not change the primary purpose of the application by significantly altering the features or functionality of the application as submitted to the App Store.</p>

## Pushing Updates To Your App Experience

A variation on the loading of Web content as outlined above is to refresh local content with updates from the Web. In this approach, the Web content (HTML, CSS and JavaScript) is bundled on the server and downloaded to the mobile app client whenever the content is updated. This updated code can now change the user interface, application flow and so on, without the developer needing to update the app via the iOS App Store or Google Play.

Note that you can only update the HTML, CSS and JavaScript in this manner; native code cannot be updated. Apple allows JavaScript code to be downloaded and executed as long as it runs within the context of the <code>UIWebView</code> control in your iOS application. <strong>This is the only situation in which code “downloading” is allowed in iOS.</strong>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ce418e7-7db7-4e7c-934e-d0c61bf9515e/amway-android-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139162" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/989fb39e-319e-4055-a6c5-3e19a5845e38/amway-android-500-mini.png" alt="amway-android_500_mini" width="500" height="484" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ce418e7-7db7-4e7c-934e-d0c61bf9515e/amway-android-mini.png">See larger view.</a>)</em>

The application above is running on Android. The HTML content has been downloaded to the client as a bundle of content and is now being served locally. Note the use of the action bar to provide a navigation experience that is familiar to Android users. Below is the same application running on iOS, where a <code>UINavigationController</code> is used:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e090531-0411-4a6a-b4f7-a3ca6da82d3c/amway-ios-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139164" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3706df87-c2cf-4c54-b110-fa2902d04f8e/amway-ios-500-mini.png" alt="amway-ios_500_mini" width="270" height="480" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e090531-0411-4a6a-b4f7-a3ca6da82d3c/amway-ios-mini.png">See larger view.</a>)</em>

In addition to speeding up the updating process, this manner of transmitting app changes ensures that users will be running the latest code. In the traditional approach, native app updates are distributed via an application store, and the user is informed that an update is available, although they are not required to install the latest update. Not everyone updates apps regularly. Updating local HTML, CSS and JavaScript via a dynamically deployed update bundle mitigates this issue.

<strong>The ability to dynamically update local content</strong> is actually part of a commercial hybrid mobile-development platform called <a href="https://trigger.io/">Trigger.IO</a>. The <a href="https://trigger.io/reload/">Trigger.IO Reload</a> feature permits you to push updates to the HTML portion of your application. Note that native code cannot be updated in this manner. However, if much of your application’s flow is controlled with JavaScript and augmented with native code, then making substantial changes to your application’s workflow dynamically is possible.

Keep in mind that, according to the iOS developer agreement, these updates may not change the primary purpose of the application by significantly altering the features or functionality of the application as submitted to the App Store. As such, major releases would likely still have to be carried out in the traditional manner.</p>

## Dynamically Reloading Content For Development And Testing

The ability to dynamically load updates to an app could also accelerate the development process. The native development process on both iOS and Android generally requires application code to be compiled on a desktop computer and then transferred to the device for testing. Some development programs, such as <a href="https://www.icenium.com/">Icenium</a>, with its <a href="https://docs.icenium.com/icenium-mobile-app-development/using-icenium-ion/livesync-with-ion">LiveSync</a> and <a href="https://docs.icenium.com/icenium-mobile-app-development/using-icenium-ion/using-icenium-ion">Ion</a> tools, compile app updates in a cloud environment and then simply download the update to a native app that is already running on your device.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/663d90bb-373a-424f-8683-c19f0d11d5fa/icenium-ion-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139166" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dc82e84-487a-4e2b-96a1-5341f0d2e0c1/icenium-ion-500-mini.png" alt="icenium-ion_500_mini" width="310" height="600" /></a><br>
<em>Icenium Ion is reloading updated content. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/663d90bb-373a-424f-8683-c19f0d11d5fa/icenium-ion-mini.png">See larger view.</a>)</em>

As code changes are made and saved on the server, a simple three-finger tap-and-hold gesture will update the app on an iOS device. Icenium makes a similar capability available for Android. Adobe’s <a href="https://build.phonegap.com/">PhoneGap Build</a> makes updates possible via a feature known as <span class="removed_link" title="https://build.phonegap.com/docs/hydration">Hydration</span>. In this case, <strong>a developer can instantly reload any changes</strong> they make in their <a href="https://en.wikipedia.org/wiki/Integrated_development_environment">IDE</a> onto a variety of devices without having to physically connect the devices to a development machine and then push the code onto the devices.

Each time the application is started with Hydration enabled, the application will check the PhoneGap Build server to see whether a new version is available. If so, the user is prompted to update to the new version. This can make quality assurance of your application easier as well. You won’t have to worry about signing code updates, provisioning and so on if the person testing your app already has the native “shell” application installed.</p>

### Be Careful

While the appeal of dynamic application updates is strong, keep in mind that for content sourced from the Web, you must implement some controls to ensure that downloaded code cannot simply call any native method in your app. Failing to do so could expose your user’s data to a third party and violate your agreement with Apple or Google. In addition, updates loaded dynamically must not significantly change the purpose or functionality of the app. Failing to adhere to this would likely result in your application being removed from the iOS App Store or Google Play. Treat these techniques as a way to enhance the user experience and to deliver bug fixes and incremental features quickly, not to thwart the App Store’s approval process.</p>

## A Bridge Between Two Worlds

Both iOS and Android offer a Web view control that you can place in a native application. In the section below, I’ll offer some code examples to illustrate how JavaScript in a Web view can communicate with native code and how native code can invoke methods on the JavaScript in the Web view.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db07c0f5-397d-4410-915d-1937d5897459/phonegap-logo-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139168" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7b530ef-3ab4-4f20-997d-617fbe11d0ba/phonegap-logo-500-mini.png" alt="phonegap-logo_500_mini" width="500" height="500" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db07c0f5-397d-4410-915d-1937d5897459/phonegap-logo-mini.png">See larger view.</a>)</em>

Before we look at code, keep in mind that you also have the option to use PhoneGap (Apache Cordova) within an existing application with native controls. Starting with PhoneGap 1.4 for iOS and PhoneGap 1.9 for Android, placing a <code>CordovaWebView</code> into a native <code>ViewController</code> on iOS or into an activity on Android is possible. This permits your Web code to access the entire PhoneGap API and to access any PhoneGap plugins. You could, of course, follow the <a href="https://docs.phonegap.com/en/2.7.0/guide_plugin-development_index.md.html#Plugin%20Development%20Guide">PhoneGap plugin API</a> to expose your own native code to the <code>CordovaWebView</code>.

Assuming you don’t need the full capabilities of PhoneGap and you simply need to expose a small portion of functionality between the two worlds, implementing your own bridge with a relatively small amount of code is possible. The three applications referenced earlier in this document were all built in this manner using a “private API.” This further ensures that you tightly control the API that governs which portions of native functionality may be accessed by the Web view.</p>

## Bridging From iOS To A UIWebView

The <code>UIWebView</code> in iOS and its associated <code>UIWebViewDelegate</code> provide the mechanism that allows native code and JavaScript to communicate with each other. I have prepared a simple iOS application to show how a form in a <code>UIWebView</code> can communicate with a form in native code:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efc0caa8-adb0-4c4b-965d-add55e25c3fe/ios-bridge-example-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139170" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28f0cbe0-d0fe-43b7-9042-fd2f82726796/ios-bridge-example-500-mini.png" alt="ios-bridge-example_500_mini" width="384" height="734" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efc0caa8-adb0-4c4b-965d-add55e25c3fe/ios-bridge-example-mini.png">See larger view.</a>)</em>

Note that the upper portion of this screen, with the light-gray background, is rendered by the <code>UIWebView</code>. The lower portion, with the white background, is rendered natively.

This application simply passes a JSON object from the Web view to native code, and vice versa. The code for this and an Android version are available in a <a href="https://github.com/ptraeg/html5-in-mobile-apps">GitHub repository</a>.</p>

### Invoking Native iOS Code From JavaScript

My standard technique for moving data from the JavaScript to native code is to invoke a native execution method with a <code>command</code> name and pass along data in the form of a JSON string containing the arguments associated with the command.

<pre><code class="language-javascript">
var nativeBridge = {
   invoke: function (commandName, args) {
      console.log(commandName + ": " + JSON.stringify(args, null, 2));
      window.location = 'js-call:' + commandName + ':' +
                      encodeURIComponent(JSON.stringify(args));
  }
};
</code></pre>

This code attempts to navigate the browser to a new URL, but not one with a normal <code>https://</code> or <code>file://</code> URL scheme. In this case, we are using a custom protocol scheme of <code>js-call:</code>. On the Objective-C side of things, we’ll trap this attempt to navigate in our <code>UIWebViewDelegate</code>:

<pre><code class="language-javascript">
(BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType (UIWebViewNavigationType)navigationType
</code></pre>

Inside the delegate for this call, we can interrogate the incoming URL to see whether it’s a call from our JavaScript:

<pre><code class="language-clike">
NSString *requestURLString = [[request URL] absoluteString];
    if ([requestURLString hasPrefix:@"js-call:"]) {
</code></pre>

Now we can pull apart the request to determine the command name and the JSON arguments string:

<pre><code class="language-clike">
NSArray *components = [requestURLString componentsSeparatedByString:@":"];
NSString *commandName = (NSString*)[components objectAtIndex:1];
NSString *argsAsString = [ (NSString*)[components objectAtIndex:2] stringByReplacingPercentEscapesUsingEncoding:NSUTF8StringEncoding ];
</code></pre>

Now that we have the arguments as a string, we can turn them into an <code>NSDictionary</code> object:

<pre><code class="language-clike">
NSError *error = nil;
NSData *argsData = [argsAsString dataUsingEncoding:NSUTF8StringEncoding];
NSDictionary *args = (NSDictionary*)[NSJSONSerialization JSONObjectWithData:argsData options:kNilOptions error:&amp;error];
</code></pre>

With everything decoded, it’s now simple to invoke the right native method to properly take the data that we’ve received from JavaScript and update the native UI:

<pre><code class="language-clike">
if ([commandName isEqualToString:@"updateNames"]) {
   [self updateNativeNameValuesWithFirstName:[args objectForKey:@"fname"]
                                    LastName:[args objectForKey:@"lname"]];
}
</code></pre>

When successfully handling a call via the <code>js-call</code> URL scheme, we must remember to return a boolean <code>NO</code> value from our delegate to prevent the Web view from actually trying to visit the desired URL.</p>

### Invoking JavaScript From iOS Native Code

This approach is a bit more straightforward because we don’t have to use a delegate method. We can simply call the desired JavaScript function by passing the appropriate JavaScript method’s name and required arguments as a string value to the <code>UIWebView</code>’s <code>stringByEvaluatingJavaScriptFromString</code> method.

Here, we take some values from the native view and turn them into a JSON object via an <code>NSDictionary</code>:

<pre><code class="language-clike">
NSDictionary *namesDict = @{@"fname": self.fNameTextField.text,
                            @"lname": self.lNameTextField.text};
NSError *error;
NSData *namesData = [NSJSONSerialization dataWithJSONObject:namesDict
                                                    options:0
                                                      error:&amp;error];
NSString *namesJSON = [ [NSString alloc] initWithData:namesData
                                             encoding:NSUTF8StringEncoding] ;
</code></pre>

Now that we have the JSON values as a string, we can simply format a command and volley it over the wall to the Web view for execution:

<pre><code class="language-clike">
NSString *jsCommand = [NSString stringWithFormat:@"setNames(%@)", namesJSON];
[self.webView stringByEvaluatingJavaScriptFromString:jsCommand];
</code></pre>

As simple as that, we’ve roundtripped between JavaScript and Objective-C. This basic technique could, of course, be leveraged to build more complex interactions.</p>

## Bridging From Android To A Web View

Below is a screenshot of the Android application running the same HTML and JavaScript code that we used in the native iOS example.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a07f98b-52c4-4ffc-a9ed-2fcb9dd399cd/android-bridge-example-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139176" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb76130a-1c90-4449-8e27-d141eb87bc47/android-bridge-example-500-mini.png" alt="android-bridge-example_500_mini" width="480" height="654" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a07f98b-52c4-4ffc-a9ed-2fcb9dd399cd/android-bridge-example-mini.png">See larger view.</a>)</em>

As with the iOS example, the upper portion of this screen, with the light-gray background, is rendered by the Web view. The lower portion, with the white background, is rendered natively. The appearances of the iOS example and the Android example differ because we are using the default component styles for each platform. In addition, the Android example contains an action bar, which Android users would expect to find in an application.</p>

### Invoking Native Android Code From JavaScript

Android Web views have the benefit of being able to expose an entire Java class to JavaScript. There’s no need to trap an attempt to navigate off a Web view via some sort of custom URL scheme, as we did with iOS. First, we must signal to the Android Web view that it’s OK for JavaScript to execute on the Web view. I do this when loading the Web view content:

<pre><code class="language-java">
@Override
public void onStart() {
   super.onStart();
   WebSettings webSettings = webview.getSettings();
   webSettings.setJavaScriptEnabled(true);
   webview.loadUrl("file:///android_asset/webviewContent.html");
   webview.addJavaScriptInterface(new WebViewInterface(this), "Android");
}
</code></pre>

Note the last line in the code above. We are registering a particular class, in this case <code>WebViewInterface</code>, to be accessed via JavaScript. In addition, this class is being namespaced by the string <code>Android</code>. Thus, in our JavaScript we can test whether the namespace <code>Android</code> is defined and, if so, invoke methods on this class, like so:

<pre><code class="language-javascript">
if (window.Android) {
   Android.updateNames(JSON.stringify(nameData));
}
</code></pre>

On the Java side, the <code>WebViewInterface</code> is a standard Java class. If you are targeting the Android 4.2 SDK, then all methods to be exposed to JavaScript must be decorated with the <code>@JavaScriptInterface</code> attribute:

<pre><code class="language-java">
public class WebViewInterface {
   Context mContext;

   /** Instantiate the interface and set the context */
   WebViewInterface(Context c) {
       mContext = c;
   }

   @JavaScriptInterface
   public void updateNames(String namesJsonString) {
      Log.d(getPackageName(), "Sent from webview: " + namesJsonString);
      try {
         JSONObject namesJson = new JSONObject(namesJsonString);
         final String firstName = namesJson.getString("fname");
         final String lastName = namesJson.getString("lname");</code></pre>

// When invoked from JavaScript, this is executed on a thread // other than the UI thread. // Because we want to update the native UI controls, we must // create a runnable for the main UI thread. runOnUiThread(new Runnable() { public void run() { fnameEditText.setText(firstName); lnameEditText.setText(lastName); } }); } catch (JSONException e) { Log.e(getPackageName(), "Failed to create JSON object from Web view data"); } } }

Note that <strong>when the methods on this class are invoked by JavaScript, they are not executed on the main UI thread</strong>. Thus, if our intention is to update any part of the UI, we must create a new runnable and post it for execution on the main UI thread, like so:

<pre><code class="language-java">
runOnUiThread(new Runnable() {
   public void run() {
      fnameEditText.setText(firstName);
      lnameEditText.setText(lastName);
   }
});
</code></pre>

Invoking JavaScript from native Android code is essentially similar to how we call JavaScript from Objective-C. We load the JSON representation of the data into a string and then form a JavaScript function call. One difference is that the function reference must be prefixed with the <code>JavaScript:</code> protocol scheme:

<pre><code class="language-java">
public void sendNamesToWebView() {
   JSONObject namesJson = new JSONObject();
   try {
      namesJson.put("fname", fnameEditText.getText().toString());
      namesJson.put("lname", lnameEditText.getText().toString());
      webview.loadUrl( "JavaScript:setNames(" + namesJson.toString() + ")" );
   } catch (JSONException e) {
      Log.e(getPackageName(),
        "Failed to create JSON object for Web view");
   }
}
</code></pre>

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db07c0f5-397d-4410-915d-1937d5897459/phonegap-logo-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139168" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7b530ef-3ab4-4f20-997d-617fbe11d0ba/phonegap-logo-500-mini.png" alt="phonegap-logo_500_mini" width="500" height="500" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db07c0f5-397d-4410-915d-1937d5897459/phonegap-logo-mini.png">See larger view.</a>)</em>

Before we look at code, keep in mind that you also have the option to use PhoneGap (Apache Cordova) within an existing application with native controls. Starting with PhoneGap 1.4 for iOS and PhoneGap 1.9 for Android, placing a <code>CordovaWebView</code> into a native <code>ViewController</code> on iOS or into an activity on Android is possible. This permits your Web code to access the entire PhoneGap API and to access any PhoneGap plugins. You could, of course, follow the <a href="https://docs.phonegap.com/en/2.7.0/guide_plugin-development_index.md.html#Plugin%20Development%20Guide">PhoneGap plugin API</a> to expose your own native code to the <code>CordovaWebView</code>.

Assuming you don’t need the full capabilities of PhoneGap and you simply need to expose a small portion of functionality between the two worlds, implementing your own bridge with a relatively small amount of code is possible. The three applications referenced earlier in this document were all built in this manner using a “private API.” This further ensures that you tightly control the API that governs which portions of native functionality may be accessed by the Web view.</p>

## Bridging From iOS To A UIWebView

The <code>UIWebView</code> in iOS and its associated <code>UIWebViewDelegate</code> provide the mechanism that allows native code and JavaScript to communicate with each other. I have prepared a simple iOS application to show how a form in a <code>UIWebView</code> can communicate with a form in native code:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efc0caa8-adb0-4c4b-965d-add55e25c3fe/ios-bridge-example-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139170" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/28f0cbe0-d0fe-43b7-9042-fd2f82726796/ios-bridge-example-500-mini.png" alt="ios-bridge-example_500_mini" width="384" height="734" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/efc0caa8-adb0-4c4b-965d-add55e25c3fe/ios-bridge-example-mini.png">See larger view.</a>)</em>

Note that the upper portion of this screen, with the light-gray background, is rendered by the <code>UIWebView</code>. The lower portion, with the white background, is rendered natively.

This application simply passes a JSON object from the Web view to native code, and vice versa. The code for this and an Android version are available in a <a href="https://github.com/ptraeg/html5-in-mobile-apps">GitHub repository</a>.</p>

### Invoking Native iOS Code From JavaScript

My standard technique for moving data from the JavaScript to native code is to invoke a native execution method with a <code>command</code> name and pass along data in the form of a JSON string containing the arguments associated with the command.

<pre><code class="language-javascript">
var nativeBridge = {
   invoke: function (commandName, args) {
      console.log(commandName + ": " + JSON.stringify(args, null, 2));
      window.location = 'js-call:' + commandName + ':' +
                      encodeURIComponent(JSON.stringify(args));
  }
};
</code></pre>

This code attempts to navigate the browser to a new URL, but not one with a normal <code>https://</code> or <code>file://</code> URL scheme. In this case, we are using a custom protocol scheme of <code>js-call:</code>. On the Objective-C side of things, we’ll trap this attempt to navigate in our <code>UIWebViewDelegate</code>:

<pre><code class="language-javascript">
(BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType (UIWebViewNavigationType)navigationType
</code></pre>

Inside the delegate for this call, we can interrogate the incoming URL to see whether it’s a call from our JavaScript:

<pre><code class="language-clike">
NSString *requestURLString = [[request URL] absoluteString];
    if ([requestURLString hasPrefix:@"js-call:"]) {
</code></pre>

Now we can pull apart the request to determine the command name and the JSON arguments string:

<pre><code class="language-clike">
NSArray *components = [requestURLString componentsSeparatedByString:@":"];
NSString *commandName = (NSString*)[components objectAtIndex:1];
NSString *argsAsString = [ (NSString*)[components objectAtIndex:2] stringByReplacingPercentEscapesUsingEncoding:NSUTF8StringEncoding ];
</code></pre>

Now that we have the arguments as a string, we can turn them into an <code>NSDictionary</code> object:

<pre><code class="language-clike">
NSError *error = nil;
NSData *argsData = [argsAsString dataUsingEncoding:NSUTF8StringEncoding];
NSDictionary *args = (NSDictionary*)[NSJSONSerialization JSONObjectWithData:argsData options:kNilOptions error:&amp;error];
</code></pre>

With everything decoded, it’s now simple to invoke the right native method to properly take the data that we’ve received from JavaScript and update the native UI:

<pre><code class="language-clike">
if ([commandName isEqualToString:@"updateNames"]) {
   [self updateNativeNameValuesWithFirstName:[args objectForKey:@"fname"]
                                    LastName:[args objectForKey:@"lname"]];
}
</code></pre>

When successfully handling a call via the <code>js-call</code> URL scheme, we must remember to return a boolean <code>NO</code> value from our delegate to prevent the Web view from actually trying to visit the desired URL.</p>

### Invoking JavaScript From iOS Native Code

This approach is a bit more straightforward because we don’t have to use a delegate method. We can simply call the desired JavaScript function by passing the appropriate JavaScript method’s name and required arguments as a string value to the <code>UIWebView</code>’s <code>stringByEvaluatingJavaScriptFromString</code> method.

Here, we take some values from the native view and turn them into a JSON object via an <code>NSDictionary</code>:

<pre><code class="language-clike">
NSDictionary *namesDict = @{@"fname": self.fNameTextField.text,
                            @"lname": self.lNameTextField.text};
NSError *error;
NSData *namesData = [NSJSONSerialization dataWithJSONObject:namesDict
                                                    options:0
                                                      error:&amp;error];
NSString *namesJSON = [ [NSString alloc] initWithData:namesData
                                             encoding:NSUTF8StringEncoding] ;
</code></pre>

Now that we have the JSON values as a string, we can simply format a command and volley it over the wall to the Web view for execution:

<pre><code class="language-clike">
NSString *jsCommand = [NSString stringWithFormat:@"setNames(%@)", namesJSON];
[self.webView stringByEvaluatingJavaScriptFromString:jsCommand];
</code></pre>

As simple as that, we’ve roundtripped between JavaScript and Objective-C. This basic technique could, of course, be leveraged to build more complex interactions.</p>

## Bridging From Android To A Web View

Below is a screenshot of the Android application running the same HTML and JavaScript code that we used in the native iOS example.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a07f98b-52c4-4ffc-a9ed-2fcb9dd399cd/android-bridge-example-mini.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139176" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb76130a-1c90-4449-8e27-d141eb87bc47/android-bridge-example-500-mini.png" alt="android-bridge-example_500_mini" width="480" height="654" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7a07f98b-52c4-4ffc-a9ed-2fcb9dd399cd/android-bridge-example-mini.png">See larger view.</a>)</em>

As with the iOS example, the upper portion of this screen, with the light-gray background, is rendered by the Web view. The lower portion, with the white background, is rendered natively. The appearances of the iOS example and the Android example differ because we are using the default component styles for each platform. In addition, the Android example contains an action bar, which Android users would expect to find in an application.</p>

### Invoking Native Android Code From JavaScript

Android Web views have the benefit of being able to expose an entire Java class to JavaScript. There’s no need to trap an attempt to navigate off a Web view via some sort of custom URL scheme, as we did with iOS. First, we must signal to the Android Web view that it’s OK for JavaScript to execute on the Web view. I do this when loading the Web view content:

<pre><code class="language-java">
@Override
public void onStart() {
   super.onStart();
   WebSettings webSettings = webview.getSettings();
   webSettings.setJavaScriptEnabled(true);
   webview.loadUrl("file:///android_asset/webviewContent.html");
   webview.addJavaScriptInterface(new WebViewInterface(this), "Android");
}
</code></pre>

Note the last line in the code above. We are registering a particular class, in this case <code>WebViewInterface</code>, to be accessed via JavaScript. In addition, this class is being namespaced by the string <code>Android</code>. Thus, in our JavaScript we can test whether the namespace <code>Android</code> is defined and, if so, invoke methods on this class, like so:

<pre><code class="language-javascript">
if (window.Android) {
   Android.updateNames(JSON.stringify(nameData));
}
</code></pre>

On the Java side, the <code>WebViewInterface</code> is a standard Java class. If you are targeting the Android 4.2 SDK, then all methods to be exposed to JavaScript must be decorated with the <code>@JavaScriptInterface</code> attribute:

<pre><code class="language-java">
public class WebViewInterface {
   Context mContext;

   /** Instantiate the interface and set the context */
   WebViewInterface(Context c) {
       mContext = c;
   }

   @JavaScriptInterface
   public void updateNames(String namesJsonString) {
      Log.d(getPackageName(), "Sent from webview: " + namesJsonString);
      try {
         JSONObject namesJson = new JSONObject(namesJsonString);
         final String firstName = namesJson.getString("fname");
         final String lastName = namesJson.getString("lname");</code></pre>

// When invoked from JavaScript, this is executed on a thread // other than the UI thread. // Because we want to update the native UI controls, we must // create a runnable for the main UI thread. runOnUiThread(new Runnable() { public void run() { fnameEditText.setText(firstName); lnameEditText.setText(lastName); } }); } catch (JSONException e) { Log.e(getPackageName(), "Failed to create JSON object from Web view data"); } } }

Note that <strong>when the methods on this class are invoked by JavaScript, they are not executed on the main UI thread</strong>. Thus, if our intention is to update any part of the UI, we must create a new runnable and post it for execution on the main UI thread, like so:

<pre><code class="language-java">
runOnUiThread(new Runnable() {
   public void run() {
      fnameEditText.setText(firstName);
      lnameEditText.setText(lastName);
   }
});
</code></pre>

Invoking JavaScript from native Android code is essentially similar to how we call JavaScript from Objective-C. We load the JSON representation of the data into a string and then form a JavaScript function call. One difference is that the function reference must be prefixed with the <code>JavaScript:</code> protocol scheme:

<pre><code class="language-java">
public void sendNamesToWebView() {
   JSONObject namesJson = new JSONObject();
   try {
      namesJson.put("fname", fnameEditText.getText().toString());
      namesJson.put("lname", lnameEditText.getText().toString());
      webview.loadUrl( "JavaScript:setNames(" + namesJson.toString() + ")" );
   } catch (JSONException e) {
      Log.e(getPackageName(),
        "Failed to create JSON object for Web view");
   }
}
</code></pre>

That’s all there is to roundtripping JSON data between JavaScript and native Android code. Both sample applications are available in the <a href="https://github.com/ptraeg/html5-in-mobile-apps">GitHub repository</a> for your reference.</p>

## Web Views: What’s The Downside?

Like most things in software development, there must be some caveats to developing with Web views. Keep these in mind when considering the hybrid approach and determining which portions of your application to do with which technologies.

*   **Not all Web views render the same**.  The capability of Web views has improved markedly in the last two years. However, your user base may not be running the latest and greatest version of Android or iOS. The Android platform has generally lagged behind the iOS platform in the capability and performance of its Web view. Google appears to be putting in a renewed effort to improve that situation, but users stuck on old versions of Android (especially releases before Ice Cream Sandwich 4.x) might find that the performance of Web views, especially those with complex layouts, do not match what is achievable on iOS. Developers will need to test the HTML5 code on Android 2.2, 2.3 and 4.x to ensure that content renders consistently. Reserve sufficient time in your project to perform adequate testing across all mobile OS versions that you intend to support.
*   **Performance**.  Web views are typically not as performant as native code. However, in many situations, you may find the performance to be perfectly acceptable, particularly on current hardware. Keep in mind that bridging calls between the native and Web view portions of your code will exact a performance toll. You won’t want to make calls across this bridge at sub-second intervals, but for most applications this is not an issue.
*   **Scrolling behavior**.  Users might be able to distinguish between the way Web views scroll and the way native portions of the app scroll. Some of this can be mitigated in new versions of WebKit with the CSS3 `-webkit-overflow-scrolling: touch` property. You might also wish to look at solutions such as [FTScroller](https://github.com/ftlabs/ftscroller) and [iScroll](https://cubiq.org/iscroll-4).
*   **Complexity**.  As mentioned earlier, if you will be serving some content from Web servers you must ensure you have the infrastructure necessary to support this. Because your application now spans native code, Web servers, and potentially backend services there are more points of failure. When making Web content changes you must perform backwards compatibility testing against earlier deployed versions of the application to ensure existing versions of your application still running on users devices will continue to perform as expected.
*   **Developer Agreement Compliance**.  Familiarize yourself with the restrictions each app marketplace might impose on content provided from the Web. As this article identified there are some notable restrictions, particularly on the iOS platform, on what your app is permitted to do with content sourced from the Web. Failure to take these restrictions into account could result in your app not being approved for release, or an existing app being pulled from the AppStore.
*   **Security**.  As stated earlier content sourced from the Web should be treated with some suspicion, particularly if it will be interacting with an interface to your native code. Ensure you've exposed only those portions of your native code that are truly required for interaction with the Web layer. Failure to do so could result in some consequences should compromised Web content be able to freely into call your native code. Make sure you take standard Web security practices into account to ensure your Web content cannot be compromised to begin with.

Given the flexibility afforded by a hybrid solution, you have the freedom to write portions of your application in native code if you find that the performance of the Web view is insufficient for a given interaction. Of course, <strong>the more native code you write, the more code will have to be rewritten for every platform you intend to support</strong>. It’s a trade-off; however, a hybrid solution puts you in control of the application’s flexibility and performance.</p>

## Summary

The use of HTML5 in mobile app development is a somewhat controversial subject. However, it's important to understand the benefits each potential development strategy affords. As an app developer you have the ultimate decision on what strategy best suits the needs of your application. Despite some of the negative publicity that mobile HTML5 solutions have received in recent months, this article shows how HTML5 is still a valuable part of app development.

Keep performance, and security in mind when using any application development platform. Test early, and test often, across a variety of devices. As we’ve seen in this article, HTML5 brings with it many benefits that extend far beyond the convenience of sharing code across platforms. Used properly, the hybrid approach of marrying native and HTML5 code can create some truly unique and flexible solutions that would not otherwise be possible. Keep your technology choices open and flexible to reap the rewards of a hybrid experience.

<em>(al ea)</em>


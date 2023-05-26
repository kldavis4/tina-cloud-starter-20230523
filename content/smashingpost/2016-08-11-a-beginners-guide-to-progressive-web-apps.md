---
title: A Beginner's Guide To Progressive Web Apps
slug: a-beginners-guide-to-progressive-web-apps
author: kevinfarrugia
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64b03549-0bd9-4c23-b6fd-ca691e8ca3b8/sky-high-offline-500-opt.png
date: 2016-08-11T16:13:41.000Z
summary: >-
  PWAs take advantage of the latest technologies to combine the best of web and
  mobile apps. This articles look into recent advancements in the browser and
  the opportunities we, as developers, have to build a new generation of web
  apps.
description: >-
  PWAs take advantage of the latest technologies to combine the best of web and
  mobile apps. This articles look into recent advancements in the browser and
  the opportunities we, as developers, have to build a new generation of web
  apps.
categories:
  - Mobile
  - Apps
  - AMP
  - Service Workers
---
Progressive web apps could be the next big thing for the mobile web. Originally proposed by Google in 2015, they have already attracted a lot of attention because of the relative ease of development and the almost instant wins for the application’s user experience.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [The Building Blocks Of Progressive Web Apps](https://www.smashingmagazine.com/2016/09/the-building-blocks-of-progressive-web-apps/)
*   [Conversational Design Essentials: Tips For Building A Chatbot](https://www.smashingmagazine.com/2016/12/conversational-design-essentials-tips-for-building-a-chatbot/)
*   [Building A First-Class App That Leverages Your Website](https://www.smashingmagazine.com/2016/02/building-first-class-app-leverages-website-case-study/)
*   [Creating A Complete Web App In Foundation For Apps](https://www.smashingmagazine.com/2015/04/creating-web-app-in-foundation-for-apps/)

A progressive web application takes advantage of the latest technologies to <strong>combine the best of web and mobile apps</strong>. Think of it as a website built using web technologies but that acts and feels like an app. Recent advancements in the browser and in the availability of service workers and in the Cache and Push APIs have enabled web developers to allow users to install web apps to their home screen, receive push notifications and even work offline.

Progressive web apps take advantage of the much larger web ecosystem, plugins and community and the relative ease of deploying and maintaining a website when compared to a native application in the respective app stores. For those of you who develop on both mobile and web, you’ll appreciate that a website can be built in less time, that an API does not need to be maintained with backwards-compatibility (all users will run the same version of your website’s code, unlike the version fragmentation of native apps) and that the <strong>app will generally be easier to deploy and maintain</strong>.

{{% feature-panel %}}

## Why Progressive Web Apps?

A study has shown that, on average, an <a href="https://blog.gaborcselle.com/2012/10/every-step-costs-you-20-of-users.html">app loses 20%</a> of its users for every step between the user’s first contact with the app and the user starting to use the app. A user must first find the app in an app store, download it, install it and then, finally, open it. When a user finds your progressive web app, they will be able to immediately start using it, eliminating the unnecessary downloading and installation stages. And when the user returns to the app, they will be prompted to install the app and upgrade to a full-screen experience.

However, a native app is definitely not all bad. Mobile applications with push notifications achieve <a href="https://info.localytics.com/blog/push-messaging-drives-88-more-app-launches-for-users-who-opt-in">up to three times more retention</a> than their counterparts without push, and a user is three times more likely to reopen a mobile application than a website. In addition, a well-designed mobile application consumes less data and is much faster because some resources reside on the device.

A progressive web application takes advantage of a mobile app’s characteristics, resulting in improved user retention and performance, without the complications involved in maintaining a mobile application.</p>

### Use Cases

When should you build a progressive web app? Native is usually recommended for applications that you expect users to return to frequently, and a progressive web app is not any different. <a href="https://www.flipkart.com/">Flipkart</a> uses a progressive web app for its popular e-commerce platform, Flipkart Lite, and <a href="https://www.sbb.ch/en/timetable/mobile-apps/sbb-mobile.html">SBB </a> uses a progressive web app for its online check-in process, allowing users to access their tickets without an Internet connection.

When assessing whether your next application should be a progressive web app, a website or a native mobile application, first identify your users and the most important user actions. Being “progressive,” a progressive web app works in all browsers, and the experience is enhanced whenever the user’s browser is updated with new and improved features and APIs.

Thus, there is no compromise in the user experience with a progressive web app compared to a traditional website; however, you may have to decide what functionality to support offline, and you will have to facilitate navigation (remember that in standalone mode, the user does not have access to the back button). If your website already has an application-like interface, <strong>applying the concepts of progressive web apps will only make it better</strong>.

If certain features are required for critical user actions but are not yet available due to a lack of <a href="#crossBrowser">cross-browser support</a>, then a native mobile application might be the better option, guaranteeing the same experience for all users.</p>

## Characteristics Of A Progressive Web App

Before we jump into the code, it is important to understand that progressive web apps have the following <a href="https://developers.google.com/web/fundamentals/getting-started/your-first-progressive-web-app/">characteristics</a>:

*   **Progressive**.  By definition, a progressive web app must work on any device and enhance progressively, taking advantage of any features available on the user’s device and browser.
*   **Discoverable**.  Because a progressive web app is a website, it should be discoverable in search engines. This is a major advantage over native applications, which still lag behind websites in searchability.
*   **Linkable**.  As another characteristic inherited from websites, a well-designed website should use the URI to indicate the current state of the application. This will enable the web app to retain or reload its state when the user bookmarks or shares the app’s URL.
*   **Responsive**.  A progressive web app’s UI must fit the device’s form factor and screen size.
*   **App-like**.  A progressive web app should look like a native app and be built on the application shell model, with minimal page refreshes.
*   **Connectivity-independent**.  It should work in areas of low connectivity or offline (our favorite characteristic).
*   **Re-engageable**.  Mobile app users are more likely to reuse their apps, and progressive web apps are intended to achieve the same goals through features such as push notifications.
*   **Installable**.  A progressive web app can be installed on the device’s home screen, making it readily available.
*   **Fresh**.  When new content is published and the user is connected to the Internet, that content should be made available in the app.
*   **Safe**.  Because a progressive web app has a more intimate user experience and because all network requests can be intercepted through service workers, it is imperative that the app be hosted over HTTPS to prevent man-in-the-middle attacks.</p>

## Let’s Code!

Our first progressive web app, Sky High, will simulate an airport’s arrivals schedule. The first time the user accesses our web app, we want to show them a list of upcoming flights, retrieved from an API. If the user does not have an Internet connection and they reload the web app, we want to show them the flight schedule as it was when they last downloaded it with a connection.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d686502-b48a-4cdc-8b3b-b96a23643c16/sky-high-screenshot-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d686502-b48a-4cdc-8b3b-b96a23643c16/sky-high-screenshot-opt.png" alt="Sky High screenshot" width="250" /></a><figcaption>Sky High, our fictitious progressive web app (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d686502-b48a-4cdc-8b3b-b96a23643c16/sky-high-screenshot-opt.png">Large preview</a>)</figcaption></figure>

## The Basics

The first characteristic of a progressive web app is that it must work on all devices and must enhance on devices and browsers that allow it. Therefore, we’ve built our website using traditional HTML5 and with JavaScript that simulates the retrieval of data from a mock API. Throughout the application, we are using small bits of <a href="https://knockoutjs.com/">Knockout</a> to handle our Model-View-ViewModel (MVVM) bindings — a lightweight JavaScript framework that allows us to bind our JavaScript models to our HTML views. We chose to use Knockout because it is relatively simple to understand and does not clutter the code; however you may replace this with any other framework, such as React or AngularJS.

Our website follows Google’s <a href="https://material.google.com/">material design</a> guidelines, a set of principles that guide design and interaction. Material design not only serves as a unified standard across applications and devices, but also gives design meaning. We’ve used material design for Sky High’s arrivals view to give our progressive web app that native-app look and feel.

Finally, we tested our app to make sure it is <a href="https://addyosmani.com/blog/making-a-site-jank-free/">jank-free</a> and that scrolling is silky-smooth. Jank-free rendering has been shown to improve user engagement. Aim for a rendering of 60 frames per second.

For this demo, we will retrieve a static JSON file, instead of a real API. This is merely to keep things simple. In the real world, you would query an API or use WebSockets.</p>

### index.html

<div class="break-out">

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;

&lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
    &lt;title&gt;Sky-High Airport Arrivals&lt;/title&gt;
    &lt;link async rel="stylesheet" href="./css/style.css"&gt;
    &lt;link href="https://fonts.googleapis.com/css?family=Roboto:300,600,300italic,600italic" rel="stylesheet" type="text/css"&gt;
&lt;/head&gt;

&lt;body&gt;
    &lt;header&gt;
        &lt;div class="content"&gt;
            &lt;h3&gt;Arrivals&lt;/h3&gt;
        &lt;/div&gt;
    &lt;/header&gt;
    &lt;div class="container"&gt;
        &lt;div id="main" class="content"&gt;
            &lt;ul class="arrivals-list" data-bind="foreach: arrivals"&gt;
                &lt;li class="item"&gt;
                    &lt;span class="title" data-bind="html: title"&gt;&lt;/span&gt;
                    &lt;span class="status" data-bind="html: status"&gt;&lt;/span&gt;
                    &lt;span class="time" data-bind="html: time"&gt;&lt;/span&gt;
                &lt;/li&gt;
            &lt;/ul&gt;
        &lt;/div&gt;
    &lt;/div&gt;
    &lt;script src="./js/build/vendor.min.js"&gt;&lt;/script&gt;
    &lt;script src="./js/build/script.min.js"&gt;&lt;/script&gt;
&lt;/body&gt;

&lt;/html&gt;</code>
</pre></div>

The <code>index.html</code> file is relatively standard. We’ve created an HTML list and bound our View Model property <code>arrivals</code> to it using <a href="https://knockoutjs.com/documentation/introduction.html">Knockout</a>, through the attribute <code>data-bind="foreach: arrivals"</code>. The View Model <code>arrivals</code> is declared in the <code>page.js</code> file below and exposed in the <code>Page</code> module. On our HTML page, for each item in the <code>arrivals</code> array, we’ve bound the <code>title</code>, <code>status</code> and <code>time</code> properties to the HTML view.</p>

### page.js

<div class="break-out">

<pre><code class="language-js">(var Page = (function() {

    // declare the view model used within the page
    function ViewModel() {
        var self = this;
        self.arrivals = ko.observableArray([]);
    }

    // expose the view model through the Page module
    return {
        vm: new ViewModel(),
        hideOfflineWarning: function() {
            // enable the live data
            document.querySelector(".arrivals-list").classList.remove('loading')
            // remove the offline message
            document.getElementById("offline").remove();
            // load the live data
        },
        showOfflineWarning: function() {
            // disable the live data
            document.querySelector(".arrivals-list").classList.add('loading')
                // load html template informing the user they are offline
            var request = new XMLHttpRequest();
            request.open('GET', './offline.html', true);

            request.onload = function() {
                if (request.status === 200) {
                    // success
                    // create offline element with HTML loaded from offline.html template
                    var offlineMessageElement = document.createElement("div");
                    offlineMessageElement.setAttribute("id", "offline");
                    offlineMessageElement.innerHTML = request.responseText;
                    document.getElementById("main").appendChild(offlineMessageElement);
                } else {
                    // error retrieving file
                    console.warn('Error retrieving offline.html');
                }
            };

            request.onerror = function() {
                // network errors
                console.error('Connection error');
            };

            request.send();
        }
    }

})();</code></pre></div>

This <code>page.js</code> file exposes the <code>Page</code> module, which contains our ViewModel <code>vm</code> and two functions, <code>hideOfflineWarning</code> and <code>showOfflineWarning</code>. The View Model <code>ViewModel</code> is a simple JavaScript literal that will be used throughout the application. The property <code>arrivals</code> on the ViewModel is Knockout’s <code>observableArray</code>, which automatically binds our HTML to a JavaScript array, allowing us to push and pop items onto our array in JavaScript and automatically update the page’s HTML.

The functions <code>hideOfflineWarning</code> and <code>showOfflineWarning</code> enable the rest of our application to call these functions to update the page’s UI that displays whether we are connected online. The <code>showOfflineWarning</code> adds a class of <code>loading</code> to our <code>arrivals-list</code> HTML element to fade the list, and then it retrieves the HTML file <code>offline.html</code> through XHR. Assuming that the file has been retrieved successfully (<code>response.status === 200</code>), we append this to our HTML. Of course, if we aren’t using <a href="#serviceWorker">service workers</a> and the user is not connected to the Internet, then it would not be possible to retrieve <code>offline.html</code>, and so the user would see the browser’s offline page.

The business logic from where we retrieve the data from our API and bind it to our View Models and Views is found in <code><a href="https://github.com/IncredibleWeb/pwa-tutorial/blob/master/demo/js/arrivals.js">arrivals.js</a></code> and is standard MVVM functionality using Knockout. In the <code>arrivals.js</code> file, we simply initialize the services and View Models that we will be using throughout the application, and we expose a function — <code>Arrivals.loadData()</code> — that retrieves the data and binds it to the view model.

## Web App Manifest

Let’s make our web app more app-like. A web app manifest file is a simple JSON file that follows the <a href="https://w3c.github.io/manifest/">W3C’s specification</a>. With it, it is possible to run the web app in full-screen mode as a standalone application, to assign an icon that will get displayed when the application is installed on the device, and to assign a theme and background color to the app. In addition, Chrome on Android will proactively suggest that the user install the web app, via a <a href="https://developers.google.com/web/updates/2015/03/increasing-engagement-with-app-install-banners-in-chrome-for-android">web app install banner</a>. To display the installation prompt, your web app needs to:

*   have a valid web app manifest file,
*   be served over HTTPS,
*   have a valid service worker registered,
*   have been visited twice, with at least five minutes between each visit.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bfe97a0-b2e2-4fc0-9b77-3ddb639951ee/web-app-install-banner-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c41676c4-38d9-4d77-81c3-52f5e217767b/web-app-install-banner-500-opt.png" alt="Web app install banner" width="250" /></a><figcaption>Web app install banner (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bfe97a0-b2e2-4fc0-9b77-3ddb639951ee/web-app-install-banner-opt.png">View large version</a>)</figcaption></figure>

### manifest.json

<div class="break-out">

<pre><code class="language-json">{
    "short_name": "Arrivals",
    "name": "Arrivals at Sky High",
    "description": "Progressive web application demonstration",
    "icons": [
        {
            "src": "launcher-icon.png",
            "sizes": "48x48",
            "type": "image/png"
        },
        {
            "src": "launcher-icon-96.png",
            "sizes": "96x96",
            "type": "image/png"
        },
        {
            "src": "launcher-icon-144.png",
            "sizes": "144x144",
            "type": "image/png"
        },
        {
            "src": "launcher-icon-192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "launcher-icon-256.png",
            "sizes": "256x256",
            "type": "image/png"
        }
    ],
    "start_url": "./?utm_source=web_app_manifest",
    "display": "standalone",
    "orientation": "portrait",
    "theme_color": "#29BDBB",
    "background_color": "#29BDBB"
}</code></pre></div>

Let’s break down this manifest file:

*   `short_name` is a human-readable name for the application. In Chrome for Android, this is also the name accompanying the icon on the home screen.
*   `name` is also a human-readable name for the application and defines how the application will be listed.
*   `description` provides a general description of the web application.
*   `icons` defines an array of images of varying sizes that will serve as the application’s icon set. In Chrome for Android, the icon will be used on the splash screen, on the home screen and in the task switcher.
*   `start_url` is the starting URL of the application.
*   `display` defines the default display mode for the web application: `fullscreen`, `standalone`, `minimal-ui` or `browser`.
*   `orientation` defines the default orientation for the web application: `portrait` or `landscape`.
*   `theme_color` is the default theme color for the application. On Android, this is also used to color the status bar.
*   `background_color` defines the background color of the web application. In Chrome, it also defines the background color of the splash screen.
*   `related_applications` is not implemented in our example but is used to specify native application alternatives in the various app stores.

Add the <code>manifest.json</code> reference to the <code>index.html</code> file’s <code>head</code> tag:

<div class="break-out">

<pre><code class="language-markup">&lt;link rel="manifest" href="./manifest.json"&gt;</code></pre></div>

Once a user has added the web app to their home screen, they will be able to re-engage with your application immediately from their device, without having to directly open the browser. You can see how this is much more than a web bookmark.</p>

{{< vimeo id="177998478" >}}

<p><a href="https://vimeo.com/177998478">Add to Homescreen on Chrome for Android</a> from <a href="https://vimeo.com/smashingmagazine">Smashing Magazine</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

<figcaption>Add to home screen in Chrome for Android</figcaption></figure>

## Service Workers

One of the more exciting aspects of progressive web apps is that they can work offline. Using service workers, it is possible to show data that was retrieved in previous sessions of the app (using <a href="https://developer.mozilla.org/en/docs/Web/API/IndexedDB_API">IndexedDB</a>) or, alternatively, to show the application shell and inform the user that they are not connected to the Internet (the approach we’ve taken in this demo). Once the user reconnects, we can then retrieve the latest data from the server.

All of this is possible through service workers, which are event-driven scripts (written in JavaScript) that have access to domain-wide events, including network fetches. With them, we can cache all static resources, which could drastically reduce network requests and improve performance considerably, too.</p>

## Application Shell

The application shell is the minimum HTML, CSS and JavaScript required to power a user interface. A native mobile application includes the application shell as part of its distributable, whereas websites ordinarily request this over the network. Progressive web applications bridge this gap by placing the application shell’s resources and assets in the browser’s cache. In our Sky High application, we can see that our application shell consists of the top header bar, the fonts and any CSS required to render these elegantly.

To get started with service workers, we first need to create our service worker’s JavaScript file, <code>sw.js</code>, placed in the root directory.</p>

### sw.js

<div class="break-out">

<pre><code class="language-js">// Use a cacheName for cache versioning
var cacheName = 'v1:static';

// During the installation phase, you'll usually want to cache static assets.
self.addEventListener('install', function(e) {
    // Once the service worker is installed, go ahead and fetch the resources to make this work offline.
    e.waitUntil(
        caches.open(cacheName).then(function(cache) {
            return cache.addAll([
                './',
                './css/style.css',
                './js/build/script.min.js',
                './js/build/vendor.min.js',
                './css/fonts/roboto.woff',
                './offline.html'
            ]).then(function() {
                self.skipWaiting();
            });
        })
    );
});

// when the browser fetches a URL…
self.addEventListener('fetch', function(event) {
    // … either respond with the cached object or go ahead and fetch the actual URL
    event.respondWith(
        caches.match(event.request).then(function(response) {
            if (response) {
                // retrieve from cache
                return response;
            }
            // fetch as normal
            return fetch(event.request);
        })
    );
});</code></pre></div>

Let’s look more closely at our service worker. First, we are setting a <code>cacheName</code> variable. This is used to determine whether any changes have been made to our cached assets. For this example, we will be using a static name, meaning that our assets will not change or require updating.</p>

<div class="break-out">

<pre><code class="language-markup">self.addEventListener('install', function(e) {
    // declare which assets to cache
}</code></pre></div>

The <code>install</code> event fires during the installation phase of the service worker and will fire only once if the service worker is already installed. Therefore, refreshing the page will not trigger the installation phase again. During the installation phase, we are able to declare which assets will be cached. In our example above, we are caching one CSS file, two JavaScript files, our fonts file, our offline HTML template and, of course, the application root. <code>self.skipWaiting()</code> forces the waiting service worker to become active.

So far, we have declared our service worker, but before we see it kick into effect, we need to reference it in our JavaScript. In our application, we register it in <code>main.js</code>

<div class="break-out">

<pre><code class="language-js">// Register the service worker if available.
if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('./sw.js').then(function(reg) {
        console.log('Successfully registered service worker', reg);
    }).catch(function(err) {
        console.warn('Error whilst registering service worker', err);
    });
}

window.addEventListener('online', function(e) {
    // Resync data with server.
    console.log("You are online");
    Page.hideOfflineWarning();
    Arrivals.loadData();
}, false);

window.addEventListener('offline', function(e) {
    // Queue up events for server.
    console.log("You are offline");
    Page.showOfflineWarning();
}, false);

// Check if the user is connected.
if (navigator.onLine) {
    Arrivals.loadData();
} else {
    // Show offline message
    Page.showOfflineWarning();
}

// Set Knockout view model bindings.
ko.applyBindings(Page.vm);
</code></pre></div>

We’ve also included two event listeners to check whether the session’s state has changed from <code>online</code> to <code>offline</code> or vice versa. The event handlers then call the different functions to retrieve the data through <code>Arrivals.loadData()</code> and to enable or disable the offline message through <code>Page.showOfflineWarning</code> and <code>Page.hideOfflineWarning</code>, respectively. Our application also checks whether the user is currently online, using <a href="https://developer.mozilla.org/en-US/docs/Web/API/NavigatorOnLine/onLine">navigator.onLine</a>, and either retrieves the data or shows the offline warning accordingly. And in the last line of <code>main.js</code>, we apply the Knockout bindings to our View Model <code>Page.vm</code>.

If we load our application for the first time (with Chrome Developer Tools), we will see nothing new. However, upon reloading, we will see that a number of network resource have been retrieved from the service worker. This is our application shell.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e709815-b0a7-4023-b8da-841b71dbbf3a/app-shell-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a3662b1-d0c6-4d84-af2d-40f96c70f5bb/app-shell-500-opt.png" alt="Application shell" /></a><figcaption>Application shell network resources, in Chrome Developer Tools (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e709815-b0a7-4023-b8da-841b71dbbf3a/app-shell-opt.png">View large version</a>)</figcaption></figure>

## Offline Test

A user running the application without an Internet connection (assuming that they have already been on the page) will simply result in the application shell and the offline warning being displayed — an improvement over Chrome’s prowling t-rex. Once the user has established a network connection, we disable the warning and retrieve the latest data.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5a11b54-e391-44bc-bc2d-0f9d08983b0b/sky-high-offline-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64b03549-0bd9-4c23-b6fd-ca691e8ca3b8/sky-high-offline-500-opt.png" alt="Failing gracefully" /></a><figcaption>Render a custom HTML page instead of Chrome’s default page (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5a11b54-e391-44bc-bc2d-0f9d08983b0b/sky-high-offline-opt.png">View large version</a>)</figcaption></figure>

The Guardian takes a particularly interesting approach when offline users access its website, providing a crossword puzzle:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77fc7e28-a4d1-4572-b6f0-aa33cec5c8dd/the-guardian-opt.jpg"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be7307f1-8bba-4685-95f8-149308d3aa6d/the-guardian-500-opt.jpg" alt="The Guardian's offline crossword puzzle" /></a><figcaption>The Guardian’s offline crossword puzzle (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77fc7e28-a4d1-4572-b6f0-aa33cec5c8dd/the-guardian-opt.jpg">View large version</a>)</figcaption></figure>

## Push Notifications

Push notifications allow users to opt in to timely updates from applications they trust, helping them to re-engage with the apps. <a href="https://developers.google.com/web/updates/2015/03/push-notifications-on-the-open-web">Push notifications on the web</a> allow you to engage with your audience even when the browser is closed.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/833a0511-7ebe-4339-a8ce-1e6c2c197f2c/pwa-push-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75f19565-f8ed-4cd2-a671-75d6b2e1bf7f/pwa-push-opt-1024x279.png" alt="Push notifications" /></a><figcaption>Push notifications on <a href="https://jakearchibald-gcm.appspot.com/">Emojoy</a> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/833a0511-7ebe-4339-a8ce-1e6c2c197f2c/pwa-push-opt.png">View large version</a>)</figcaption></figure>

The Push API is supported in Chrome, Opera and Samsung’s browser and is under development in Firefox and Microsoft Edge. Unfortunately, there is no indication that the feature will be implemented in Safari.</p>

## Performance

One of the easiest wins with service workers is that we can improve performance with little to no effort. Comparing our website to itself before service workers were implemented, before we were retrieving over 200 KB upon page load; that is now reduced to 13 KB. On a regular 3G network, the page would have taken 3.5 seconds to load; now it takes 500 milliseconds.

These performance improvements are drastic because the application itself is very small and has limited functionality. Nevertheless, through the correct use of caching, it is possible to significantly improve performance and perceived performance, especially for users in places with low-connectivity.</p>

## Lighthouse

Google’s Chrome team has put together a tool for testing progressive web apps. <a href="https://github.com/GoogleChrome/lighthouse">Lighthouse</a> runs in Node.js or as a <a href="https://chrome.google.com/webstore/detail/lighthouse/blipmdconlkpinefehnmjammfjpmpbjk">Chrome plugin</a> and can be found on GitHub, too.

To run a Lighthouse test, your website needs to be available online, meaning that you cannot test on <code>localhost</code>.

To start, download the npm package:

<div class="break-out">

<pre><code class="language-js">npm install -g GoogleChrome/lighthouse</code></pre></div>

Once that’s installed, run Chrome (version 52 onwards):

<div class="break-out">

<pre><code class="language-js">npm explore -g lighthouse -- npm run chrome
lighthouse https://incredibleweb.github.io/pwa-tutorial/</code></pre></div>

The output of the Lighthouse run will be visible in the command line and will grade your website according to the progressive web app features and properties you have implemented — for example, whether you are using a <code>manifest.json</code> file or whether your page is available offline.</p>

## Conclusion

This article is merely an appetizer for progressive web apps. We could do a lot more to create that app-like experience users are looking for, whether by supporting push notifications with the <a href="https://developer.mozilla.org/en/docs/Web/API/Push_API">Push API</a>, making the app re-engageable, or using IndexedDB and <a href="https://developers.google.com/web/updates/2015/12/background-sync">background syncing</a> to improve the offline experience.</p>

### Cross-Browser Support

These are still early days for progressive web apps, and cross-browser support is still limited, especially in Safari and Edge. However, Microsoft openly supports progressive web apps and should be implementing more features by the end of the year.

*   **Service workers and Cache API**.  Supported in Chrome, Firefox, Opera and Samsung’s browser. In development in Microsoft Edge, expected to be available by the end of 2016\. Under consideration for Safari.
*   **Add to home screen**.  Supported in Chrome, Firefox, Opera, Android Browser and Samsung’s browser. Microsoft seems to indicate that progressive web apps will be available as store listings. No plans for Safari as of yet.
*   **Push API**.  Mostly supported in Chrome, Firefox, Opera and Samsung’s browser. In development in Microsoft Edge. No plans for Safari as of yet.

If more developers take advantage of the features offered by progressive web apps — which are relatively easy to implement and provide immediate rewards — then users will prefer consuming these web apps in supported browsers, hopefully convincing the other browser vendors to adapt.</p>

### Source Code

The entire source code for this tutorial is available <a href="https://github.com/IncredibleWeb/pwa-tutorial">in a Github repository</a>, and the demo is <a href="https://incredibleweb.github.io/pwa-tutorial/">available on GitHub Pages</a>.

{{< signature "da, al, il" >}}


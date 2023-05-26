---
title: 'Building An Online Magazine App For Windows 8, Part 1: The HTML5 App'
slug: online-magazine-app-for-windows-8-part1-html5-app
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88cfb4dc-177e-4c9a-a4ab-6f6d365f7afc/windowsapp.jpg
date: 2013-09-19T09:18:59.000Z
author: marcus-wendt
description: >-
  Back in 2010, Microsoft shifted its focus from propriety Web technology to
  open Web technology. The first fruits of this refocus materialized a few years
  later — in Internet Explorer, the Windows operating system, its developer
  tools and its cloud software.
categories:
  - Mobile
  - Techniques
  - Apps
  - HTML5
  - Windows
---
Back in 2010, <a href="https://www.zdnet.com/blog/microsoft/microsoft-our-strategy-with-silverlight-has-shifted/7834">Microsoft shifted its focus</a> from propriety Web technology to open Web technology. The first fruits of this refocus materialized a few years later — in Internet Explorer, the Windows operating system, its developer tools and its cloud software.

Things have changed for the better so far:

*   With version 10, Internet Explorer has finally grown up and become a fast modern browser.
*   You can build native Windows apps with JavaScript, HTML5 and CSS — apps that look and feel solid and have modern user interfaces.
*   On the server side, ASP.NET lets you own your own markup and HTTP services (finally), with Web developer-friendly tools like Razor and Web API.
*   At the cloud level, Microsoft has thrown its full weight behind Windows Azure, hosting HTTP servers en masse.

Across the board, Web developers should see significant improvements, making Windows an HTML5-friendly platform.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e252b62f-fcfd-4951-869e-046362854ae4/windows-8-layering-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ba8ed6e-402f-4353-84bf-672f9078225d/windows-8-layering-mini.png" alt="Windows 8 Modern UI layering" /></a><br>
<em>Windows 8 apps that reflect Microsoft’s “modern UI” can be built using a variety of technologies — HTML5, JavaScript and CSS being among them. Access to the native API enables you to do a lot more than you could from a browser. (<a>Larger view</a>)</em>

{{% feature-panel %}}

## A Two-Part Whirlwind Tour

In this first article in our two-part series, <strong>we’ll look at an HTML5 app that runs natively on Windows 8</strong>. In the second part, we’ll tie it up with the server and cloud. It will be a whirlwind tour through Microsoft-based Web development in 2013, with a hands-on case study and some code.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Beyond The Browser: From Web Apps To Desktop Apps](https://www.smashingmagazine.com/2017/03/beyond-browser-web-desktop-apps/)
*   [<span class="headline">Creating Universal Windows Apps With React Native</span>](https://www.smashingmagazine.com/2016/10/creating-universal-windows-apps-with-react-native/)
*   [Testing For And With Windows Phone](https://www.smashingmagazine.com/2015/05/testing-for-windows-phone/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)

If you code along with us, you’ll end up with an online magazine app, built with Web technology. The Windows 8 app will present articles fetched in JSON format from a content host running on Windows Azure. You will have a personally branded touch-friendly magazine app that you can submit to the Windows Store, that integrates with the <a href="https://winsupersite.com/article/windows8/windows-8-feature-focus-charms-144724">Search and Share charms</a> and that displays articles you manage in a cloud-based content management system (CMS).

In this first part, we’ll explain how you can launch and customize a pre-baked HTML5-based Windows Store app. In the second part, we’ll guide you through setting up your own content host, from where you can publish articles.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09b8d5ec-5ec4-4afa-af1a-e9a8a2735c67/magazine-app-on-surface-large-mini.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c2b3e23-a23e-4b76-a76b-0e33fa5769c6/magazine-app-on-surface-mini.jpg" alt="Surface RT running the Magazine App" /></a><br>
<em>Our app will run on any Windows 8 machine, including Windows RT devices such as the Microsoft Surface RT. (<a>Larger view</a>)</em>

The source code presented here, as well as the CMS back end, are all open source and easy to adapt, and the hosting and tools referred to here are available free of charge.

Throughout, you will find code snippets and links to relevant in-depth articles, and I’ll pass along some of the gotchas that I learned while building this app.</p>

## What You’ll Need To Get Started

To develop and debug a Windows Store app, you’ll need to be running Windows 8, either natively or <a href="https://www.nextofwindows.com/installing-windows-8-in-a-virtual-environment-with-vmware-player/">via a virtual machine</a>. To edit the HTML, CSS and so on, you can use your favorite editor and <a href="https://msdn.microsoft.com/en-us/library/windows/apps/hh924768.aspx">compile the app via the command line</a>; here, I’ll be using Visual Studio 2012. You can download <a href="https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-windows-8">Visual Studio Express 2012 for Windows 8</a> for free.</p>

## A Barebones App

Before diving into the pre-baked app, we should get to know the playing field a bit. So, here is what the code for a barebones Windows Store app might look like:

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html&gt;
    &lt;head&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;img src="https://upload.wikimedia.org/wikipedia/commons/2/28/HelloWorld.svg" /&gt;
    &lt;/body&gt;
&lt;/html&gt;
</code></pre>

To compile this into an app, Visual Studio will also need a project file and a manifest file (which contains meta data about your app). However, the HTML document above is all you really need to get a “Hello World.”

What you add is up to you, as long as it runs in Internet Explorer (IE) 10. (You can safely use CSS3, canvas, video, SVG, your favorite JavaScript libraries, etc.) In addition, you will also have the option to use the Windows Store API from JavaScript, to take advantage of Windows 8-specific features.

In our pre-baked app, we will use the Windows Store API. Even though it is optional, we will need it if we want things to feel native and to integrate with Windows 8.</p>

## Downloading And Launching The Magazine App

The source code for the magazine app is <a href="https://bit.ly/Win8MagazineApp">available on GitHub</a>. If you don’t have Git on your machine, simply download the ZIP file and extract the source code.

Once it’s downloaded, launch the project file, <code>Composite.AppFeed.Client.Template.jsproj</code>. When Visual Studio has launched, hit F5 to run the app.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/895df12d-d47f-45df-b85e-53fbb737bf8c/win8screenshot-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49d55f03-1c2d-4e8c-82f3-756a6b403980/win8screenshot-mini.png" alt="The app main view" /></a><br>
<em>The app’s main view shows articles within tiles that are familiar from Windows 8’s UI. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/895df12d-d47f-45df-b85e-53fbb737bf8c/win8screenshot-large-mini.png">Larger view</a>)</em>

<strong>Our app has the following basic features:</strong>

*   It’s a simple navigation app, with grouped items, a group view and an item view.
*   Clicking a group’s name will display the group view. Clicking an item’s tile will show the item.
*   Search and Share charms, device rotation, docking and the app bar all work.
*   Offline mode is supported (cached content is shown).
*   Rich HTML content is supported, including things like video.
*   It has the modern UI navigation experience expected in Windows 8 apps.

The Search and Share charms are part of a canonical charms menu in Windows 8, invoked by swiping in from the right edge (or moving your mouse to one of the right corners). The Search charm, as the name suggests, lets the user search, in our case, through articles in the app. The Share charm integrates with the user’s mail and social media accounts, enabling the user to share the URL of a given article.

In the following few sections, we will customize the design.

The sample content you see in the app is downloaded from the Web from various sources (including an existing blog, CodePlex and StackOverflow) and gives an idea of what existing raw Web content could look like when presented via this app. We will replace this default feed with one you control in part two.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ea20fcdb-8d60-447c-a47f-032a93c3dea6/project-explorer-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d394a931-2247-406a-a2b3-b17edacfe841/project-explorer-mini.png" alt="Project Explorer" /></a><br>
<em>The project explorer shows files that make up the HTML5 app.</em>

## Making The App Your Own

The project’s structure is pretty straightforward. The <code>css</code>, <code>images</code> and <code>js</code> folders contain global resources for the app, while the individual pages (including HTML, CSS and JavaScript) are defined below the <code>pages</code> folder. In the root, we have <code>default.html</code>, which is the app’s starting point, and <code>package.appxmanifest</code>, which contains meta data used by the operating system (OS) to present the app.

Once you know your way around the sources, you can customize as you wish. To customize the UI quickly, focus on the following files.</p>

### /package.appxmanifest

Edit the <code>package.appxmanifest</code> file. In the “Application UI” tab, specify your app’s title, language and description. In the “Packaging” tab, set a unique package name and publisher display name.

You can customize other things, such as the appearance of the tile for your app. The images for your tiles can be replaced in the <code>/images</code> folder (see below).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b710668d-6398-41dc-bbf9-eb9ea84e80d3/app-manifest-file-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09b65244-4cc5-4bab-8366-bfef58059e94/app-manifest-file-mini.png" alt="The app manifest file" /></a><br>
<em>The app’s manifest file is where you control how the app shows up in the OS. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b710668d-6398-41dc-bbf9-eb9ea84e80d3/app-manifest-file-large-mini.png">Larger view</a>)</em>

### /images Folder

Right-click the <code>/image</code> folder, select <code>Open Folder in File Explorer</code>, and replace the various-sized logos with your own. These logos will be used to create the tiles for the Windows 8 start screen and your app’s splash screen. You can change the background on the main page by replacing <code>background_mini.jpg</code>. Change <code>inapplogo.png</code> to customize the footer.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95c35395-4498-48f7-a2a8-1dcdd18567ab/file-explorer-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03e22dfa-c2b7-48c3-a90e-cbf038e29f50/file-explorer-mini.png" alt="File Explorer" /></a><br>
<em>Use PNG and JPEG images in your app and to represent the app on the start screen. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/95c35395-4498-48f7-a2a8-1dcdd18567ab/file-explorer-large-mini.png">Larger view</a>)</em>

### /css/default.css

Set the colors for the app’s bar and background at the top of <code>default.css</code>.</p>

### /js/options.js

In <code>options.js</code>, you can set the app’s title and details such as the “About” page’s URL, the privacy page’s URL and the alert text for offline mode.

At a minimum, customize the title and <code>websiteUrl</code>. Later on, when you’re running your own content host, change <code>dataHostUrl</code>, but keep it as is for now.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48b5220b-e2ee-44e1-9eb2-d942b0d2e776/options-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a69e500f-5a61-4f70-b2e7-15f358a2852f/options-mini.png" alt="options.js" /></a><br>
<em>The app’s global settings are controlled via JavaScript. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48b5220b-e2ee-44e1-9eb2-d942b0d2e776/options-large-mini.png">Larger view</a>)</em>

If you will be submitting your app to the Windows Store, pay attention to the value of <code>privacyUrl</code>; this is the URL that gets loaded when the user invokes yours app’s privacy policy, via the Settings charm. Because your app will be contacting a server on the Internet to fetch articles, you will need to explain your privacy policy to the user in order for your app to be approved by Microsoft. More on that in part two.</p>

## Diving Deeper Into The App

If you’ve updated the colors, titles, URLs and images, as explained above, then the major design elements of your magazine app should be branded to your liking. The next step is, obviously, to get your own content host up and running. But before we cover this, let’s cover a few pointers on further customizing the app.</p>

### IE 10 and the Windows Store App API

When building your app, you can safely use the HTML5 and CSS3 features of IE 10, including canvas and SVG. You can use any JavaScript library out there, such as AngularJS, jQuery or LESS. You are not required to test your pages in other browsers or in older versions of IE.

The Windows Store app API is by far the biggest change from the Web developer’s traditional experience. If you wish to interact with the OS, go through this API using JavaScript. <strong>The API also contains a host of other features</strong> that make JavaScript even more powerful. The API is unobtrusive in that you don’t have to care about it until you need to interact with the OS or want to use one of its features.

Here are a few APIs used by this app:

*   `WinJS` enables more advanced JavaScript features (such as the Promise object and XHR), which are excellent for writing asynchronous network interactions.
*   `Windows.UI`, `Windows.ApplicationModel` and `Windows.Storage` let you plug into the native OS and UI to do things such as interact with the charms menu and read and write to local files.
*   `WinJS.UI` contains presentation controls that act in accordance with Windows 8’s modern UI, including the scrollable list view that you see when launching the application.

For more on this, see “<a href="https://msdn.microsoft.com/en-us/library/windows/apps/br211377.aspx">Windows API for Windows Store Apps</a>.”

### Single-Page Navigation

This app uses a <a href="https://msdn.microsoft.com/en-us/library/windows/apps/hh738344.aspx">single-page navigation model</a>, meaning that HTML, CSS and JavaScript for individual subpages are loaded into <code>/default.html</code> as you invoke links. This enables you to preserve state across pages and to get smooth page transitions; but it also changes how page-specific CSS and scripts are written.

Below the <code>/pages</code> folder, you will find subfolders with HTML, CSS and JavaScript, making up the individual pages of the app, and this is where you can customize the individual views to your heart’s content.

Due to the single-page navigation model, expect the HTML, CSS and JavaScript from <code>/default.html</code> to stay with you all the time. When you navigate a subpage, scripts and CSS are loaded dynamically, and the HTML of a subpage is loaded into the <code>/default.html</code> div with the ID <code>contenthost</code>.

When you navigate from one page to another, CSS rules will <em>not</em> be unloaded, which means that <strong>any global selectors you style in a CSS file for a subpage will stick</strong>. If this is not desirable, you can prefix subpage-specific CSS selectors with a unique class name that identifies the subpage.

An example is this rule from <code>/pages/groupedItems/groupedItems.css</code>:

<pre><code class="language-css">
.groupeditemspage .groupeditemslist .group-header .group-title, .groupeditemspage .pagetitle {     
    color: #eeeeee; 
}
</code></pre>

The class name <code>groupeditemspage</code> is set in <code>/pages/groupedItems/gropuedItems.html</code> and only there. This enables us to set a light color for title text, but only for this particular subpage. When we navigate to one of the other subpages, the <code>groupeditemspage</code> class will no longer be in the DOM, and titles will fall back to a dark color, even though the CSS rules above still load.

It is worth mentioning that I’m using JavaScript (see <code>/js/navigation.js</code>) to lift this page-specific class name up to the <code>body</code> element on the current page every time the user navigates; this enables me to style all elements on the current DOM. If I didn’t do this, I would only be able to style elements below <code>contenthost</code> in <code>default.html</code>. If you study <code>groupedItems.css</code>, you will see a background image being set, and it only works because of this “move the subpage class up the DOM” trick — a small generic hack that lets us do more with CSS.</p>

### Single-Page Navigation Requires You To Unregister Resources

You also need to care about unregistering resources, such as removing event listeners when a subpage is unloaded. Because the DOM is always kept alive, failing to unregister subpage resources on unloading can lead to undesirable results.

An example is this handler from <code>/pages/groupedItems/groupedItems.js</code>:

<pre><code class="language-javascript">
unload: function () {
   var dataTransferManager = Windows.ApplicationModel.DataTransfer.DataTransferManager.getForCurrentView();
   dataTransferManager.removeEventListener("datarequested", shareDataRequested);
}
</code></pre>

Earlier in the subpage’s life, we subscribed to a data request event (which happens when a user invokes the Share charm), and we need to unsubscribe from this event when the user navigates away from that particular subpage.</p>

### A Few Words About CSS Media Queries

Your app can run on both classic Windows 8 PCs and ARM-based devices, such as the Surface RT tablet. In addition to a multitude of screen resolutions, be prepared for things such as horizontal to vertical rotation of the device and your app being snapped next to another one.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a89f782e-e89a-42f1-adf5-c275bce9b0ad/win8screenshot-snapped-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07d483fe-37dc-4e10-a6a6-66d222ff2924/win8screenshot-snapped-mini.jpg" alt="App running in snapped view" /></a><br>
<em>Windows 8 let you run two apps side by side, with one being “snapped.” Here, our app is snapped next to the Web browser, which lets users follow links in articles within the app without losing focus. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a89f782e-e89a-42f1-adf5-c275bce9b0ad/win8screenshot-snapped-large-mini.png">Larger view</a>)</em>

This you can do by using <a href="https://msdn.microsoft.com/library/windows/apps/Hh453556">CSS media queries for Windows 8 apps</a>. Below are a few sample declarations.

<pre><code class="language-css">
@media screen and (-ms-view-state: snapped) {
    .groupdetailpage .itemslist .win-groupheader {
        visibility: hidden;     
    } 
} 
@media screen and (-ms-view-state: fullscreen-portrait) {
    .groupdetailpage .itemslist .win-horizontal.win-viewport .win-surface {
        margin-left: 100px;     
    }
}
</code></pre>

You can also <a href="https://stackoverflow.com/questions/12274197/where-are-the-view-state-change-events-in-winjs">respond to rotation and snap events in scripting</a>. For example, see the <code>updateLayout</code> handler in <code>groupedItems.js</code>.</p>

### Testing and Debugging

The coding and debugging experience is slightly different than in normal Web development. For starters, your HTML app will run in a 100% chromeless full-screen environment, so <strong>the developer toolbar is not where you are used to seeing it</strong>. You’ll find it inside Visual Studio instead, which means you’ll have to jump between Visual Studio and your running app to inspect elements and so on.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dcb20fb-e397-4e8b-a17b-08a65e9b906d/visual-studio-dom-explorer-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d28a06d8-2c10-433e-aa51-0c41e7567d79/visual-studio-dom-explorer-mini.png" alt="DOM Explorer in Visual Studio" /></a><br>
<em>The DOM explorer in Visual Studio 2012 looks and feels like most other developer toolbars. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4dcb20fb-e397-4e8b-a17b-08a65e9b906d/visual-studio-dom-explorer-large-mini.png">Larger view</a>)</em>

On the bright side, you’ll have a nice spacious development canvas and excellent JavaScript debugging capabilities. And if you are running dual monitors, the experience is quite nice and seamless.

While your app is running, you will find a “DOM Explorer” tab in Visual Studio, which represents the page you are currently viewing. The “Select Element” button will bring focus to your HTML app and let you select an element, just like in the developer toolbars you know.

<a href="https://msdn.microsoft.com/en-us/library/windows/apps/hh441477.aspx">Visual Studio can launch your app</a> locally, via a simulator and on a remote device. The simulator lets you emulate different device sizes and test things such as touch events, geo-location services and changes in orientation, even though you are sitting in front of a classic PC.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b304d1e-d83b-43f8-b507-89148dee7f17/win-8-app-simulator-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26f5a386-1de2-4997-a08c-1ef814a72919/win-8-app-simulator-mini.jpg" alt="App Simulator" /></a><br>
<em>The simulator can launch a new log-in session on your Windows 8 machine, displaying everything as if it were running on the device you have selected. This lets you test how your app will behave (including with touch actions) on different device sizes and orientations. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7b304d1e-d83b-43f8-b507-89148dee7f17/win-8-app-simulator-large-mini.png">Larger view</a>)</em>

<a href="https://msdn.microsoft.com/en-us/library/windows/apps/hh441469.aspx">Remote machine debugging</a> is surprisingly easy to get up and running. Apart from letting you instantly test your app on a device like Surface RT, it is also an easy way to get your app onto a device. Once the app has been launched this way, it will stay on the device and can be used for demoing and so forth.</p>

### A Few Common Problems and How to Avoid Them

During development, I ran into two issues that took me way too much time to figure out. To save you from repeating my experience, I’ll leave you with two pointers as you polish the app.

If you ever find yourself developing a Windows Store app that fetches data from your local network, via a virtual private network or the like, you might need to edit <code>package.appxmanifest</code> and <strong>enable “Private Network (Client &amp; Server)”</strong> in the “Capabilities” tab. If this setting is not enabled and you are trying to read data from a local test server, then network communication will be blocked (with no usable hints). Uncheck this again before submitting the app, unless you expect users to need this feature.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69404b07-cf9a-47fd-a31a-b40e61d6096e/private-networks-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/923f5c78-a679-409c-99b7-8e3553c52442/private-networks-mini.png" alt="Capabilities of your app" /></a><br>
<em>You have to explicitly opt in to access things such as location, the webcam, private networks and the microphone. Users will be informed of this usage. To keep users from getting suspicious, select only what you need. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69404b07-cf9a-47fd-a31a-b40e61d6096e/private-networks-large-mini.png">Larger view</a>)</em>

If you write code that interacts with the Share charm and your code fails inside the <code>datarequested</code> handler or you stop a debugging session there, then you will experience a bug whereby the Share charm stops working, even if you restart the debugging session. The easiest way to fix this is to <a href="https://stackoverflow.com/questions/13847730/windows-8-app-share-charm-hangs-on-getting-info-from-appname">launch the Task Manager and restart <code>explorer.exe</code></a>.</p>

## What To Expect In Part 2

In the second and last part of this series, we’ll walk through setting up the <a href="https://compositec1.codeplex.com/">CMS back end</a>, getting it online and having the app read content from it. With the customized app and the back end online, you’ll have something of real value to publish, and we’ll briefly touch on how to do just that.

If you plan to submit your app to the Microsoft Store, now is a good time to <a href="https://msdn.microsoft.com/en-us/library/windows/apps/hh868184.aspx">sign up for a developer account</a>. If you choose the “individual account,” you will get up and running a whole lot faster; the “company account” requires verification but lets you publish apps using more features. Make sure you know the <a href="https://blogs.msdn.com/b/jennifer/archive/2012/09/18/what-is-the-difference-between-a-company-vs-individual-account-for-the-windows-store.aspx">differences between the two account types</a> before signing up. There is a $49 annual registration fee, while submitting apps is free.

<em>(al) (ea)</em>


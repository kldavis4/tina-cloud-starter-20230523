---
title: 'Building An Online Magazine App For Windows 8, Part 2: The Web Back End'
slug: online-magazine-app-for-windows-8-part2-web-backend
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ed84fde-6e97-4b4c-a0c1-b523ce082975/magazineapp.jpg
date: 2013-10-11T14:15:57.000Z
author: marcus-wendt
description: >-
  In [part one](https://www.smashingmagazine.com/2013/09/19/online-magazine-app-for-windows-8-part1-html5-app/)
  of this series, we got a customized magazine app for Windows 8 up and running. In this second and last part, we will shift our focus to the server and content.
categories:
  - Mobile
  - Techniques
  - Apps
  - HTML5
  - Windows
---
We will look at <strong>how our magazine app obtains the articles</strong> to be shown, examine the transport protocol and set up a live content host.

When done, you will have a cloud-based content management system running on a free hosting plan from where you can manage and publish articles. With this, our HTML5-based magazine app will essentially be ready to submit to the Windows Store.</p>

## Setting Up The Content Host Via A Web Browser

We will be using freely available tools and an open-source content management system (CMS) for the back end, and we will host the content on a free Azure website account; so, getting everything up and running will be free. The goal here is to set up all of the components you’ll need with a minimum of effort, leaving you with a working end-to-end understanding of Microsoft-based Web development in 2013 that you can expand upon.</p>

{{% feature-panel %}}

You can complete the entire process from your favorite browser.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fea5730b-b6b5-4897-a5d4-43ad8f61fbe9/republic-of-fritz-hansen-in-store-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c045db0-4ebd-4a0d-b9f4-825c2d4ab1d2/republic-of-fritz-hansen-in-store-mini.png" alt="" /></a><br>
<em>Here is how apps are presented in the Windows Store. A magazine app is used as a catalog by the Danish furniture designer Republic of Fritz Hansen, showing product data loaded from its website.</em>

Recommended reading: [Creating Universal Windows Apps With React Native](https://www.smashingmagazine.com/2016/10/creating-universal-windows-apps-with-react-native/)

## Articles Are Transported As JSON

In the Windows Store app file <code>/js/data.js</code>, the groups and articles to be displayed in the app are fetched from the content server using JSON:

<pre><code class="language-javascript">
var jsonGroup = {
    Key: "Group Key",               // key 
    Title: "Group title",           // title
    SubTitle: "Group sub title",    // subtitle
    GroupViewImage: "URL",          // image - used in tile views
    Image: "URL",                   // image - big group view image 
    Description: "HTML"             // html - a group description
};

var jsonArticle = {
    GroupKey: "Group Key",          // key of group article belongs to
    Title: "Article title",         // title
    SubTitle: "Article sub title",  // subtitle
    GroupViewImage: "URL",          // image - used in tile views
    Image: "URL",                   // image - big article lead image 
    Description: "HTML",            // html - the actual article
    Url: "URL"                      // url - for share charm
}
</code></pre>

The method used by the app to fetch data is rather crude. On launch, all articles are downloaded by the app and then cached on the local file system. The app auto-refreshes articles upon every launch or uses cached content if the content server is inaccessible.

To create your own content host, you would need to expose the structures covered below. For the purpose of this article, we will be using online services and pre-built bits to quickly raise up a content host with full content-management capabilities and the required JSON endpoints.</p>

## Azure Website Running Composite C1 CMS

Windows Azure is Microsoft’s cloud platform, which offers hosting and tools for building large-scale Web applications at one end and for providing easy access to Web applications at the other end. Here, we will be using the easy bits — i.e. Azure websites.

Azure allow you to host up to 10 websites for free. Setting up a content host on this platform is pretty easy. Here, we will set up <a href="https://compositec1.codeplex.com/">Composite C1</a>, an open-source CMS running on the .NET Web stack.

<strong>Full disclosure</strong>: I’m a member of the Composite C1 core team, so my choice of CMS is anything but impartial. Knowing the CMS very well has enabled me to create the tools for this article that should make this a fairly smooth ride, so please bear with me.

If you don’t want to take the cloud route here, you can download Composite C1 or the <a href="https://compositec1.codeplex.com/">source code from CodePlex</a>.</p>

## Windows Azure: Signing Up For The First Time

If you haven’t used an Azure website before, you’ll need to jump through the fiery hoops of registration, which will take about five minutes. You will be offered a 90-day free trial, but the Azure website you create here will keep on being free, even after the 90 days.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f9e4d49e-66b9-480f-8d78-90fac1c1f5a6/azure-sign-up-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d36c7d08-7b1f-4eb3-a343-97a882e406d9/azure-sign-up-mini.png" alt="" /></a><br>
<em>Sign up for a Windows Azure account.</em>

To complete the registration, you’ll need to provide a mobile phone number and credit-card number. Don’t panic: As long as you don’t upgrade your Azure website plan or actively use other paid Windows Azure services, you will never be charged.

Note that the free option has limitations on traffic and CPU usage, and you can’t customize the website’s domain name unless you pay up; however, for the purpose of feeding data to an app, a host name like <code>my-content-host.azurewebsites.net</code> is just fine.

Here is how to sign up:

1.  Go to the [Windows Azure page for a free trial](https://www.windowsazure.com/en-us/pricing/free-trial/).
2.  Click “Try it now.”
3.  Log in using a Microsoft account.
4.  In the registration wizard, specify your country, and click “Next.”
5.  On the second page, specify your mobile phone number, and click “Send text message.”
6.  Enter the six-digit code that you receive as a text message on your phone, and click “Verify code,” then “Next.”
7.  Fill in your credit-card details and address, and click “Next.”

### Creating an Azure Website

Once you have access to the Windows Azure management portal, here is how to create an Azure Website instance:

1.  Launch the [management portal](https://manage.windowsazure.com/).
2.  Click the “New” button in the lower toolbar.
3.  Select “Compute,” then “Web Site,” then “From Gallery.” [![Creating an Azure Website from gallery](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a97cb76f-19b4-4f28-9d97-f80888e34d23/creating-a-new-azure-website-mini.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d2cb6281-8491-4796-801d-48cd7d31c86f/creating-a-new-azure-website-large-mini.png)
4.  Select “.NET CMS Composite C1” and continue. [![Azure Website Gallery listing](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5bc7e57-a216-4f82-9710-ad205eb9872d/azure-websites-gallery-listing-mini.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/507fa29f-ece0-425f-aa6a-797ac5458c28/azure-websites-gallery-listing-large-mini.png)
5.  Specify a name and a location for your website, and finish the wizard. [![Creating an Azure Website](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4382a93d-b511-44ec-9d14-cb779a2b1764/configuring-azure-website-mini.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c35b3c44-576e-4f21-944c-6c4750a6f8a8/configuring-azure-website-large-mini.png)

This will create your website. In the websites view, you will see yours running in “Free” mode, and you will see the URL.

It could take half a minute for your website to be reported as ready. When it’s ready, you can launch it by clicking the URL.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eb6869ef-4add-4cb7-acb2-008adc85fe49/composite-c1-setup-wizard-welcome-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1f9877a-eb56-495c-9ce1-b8b309a6779b/composite-c1-setup-wizard-welcome-mini.png" alt="" /></a><br>
<em>Once you launch the website, the CMS set-up wizard kicks in.</em>

### The CMS Set-Up Wizard

“Next” your way through the CMS set-up wizard; the only major options will be the default language for content and the starter website. Select the “Open Cph — Razor” website if you fancy Twitter Bootstrap and want to look at ASP.NET Razor.

Once you have completed the wizard, you’ll see the CMS admin window (the C1 console) and the welcome screen:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c06b83a-f8f7-4e71-b1ba-a96df8633bd7/compositec1welcomescreen-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8fee9140-443e-49d2-b5b1-61473586787d/compositec1welcomescreen-mini.png" alt="" /></a><br>
<em>Welcome to the C1 console. This is where you can manage content, customize the website, install extension packages and other things.</em>

### Installing the App Feed Extensions

Using the C1 console, you can install two extension packages — made specifically for our magazine app — which will set up the bits needed to manage articles and feed it to the Windows 8 app. Some sample articles are also included, so that you have something to play around with.

To install the two packages, do the following in the C1 console:

1.  Go to the “System” view.
2.  Select “Packages,” then “Available Packages,” then “Composite.Tools,” and then select the `Composite.AppFeed.Server` package.
3.  Execute “Package Info” on it.
4.  In the document view, click “Install” and finish the installation wizard.
5.  Also, install the package named “Composite.AppFeed.Provider.Magazine.”

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5cd52352-f42d-4891-8278-d80e5fab1d5d/composite-c1-package-manager-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23ad3afc-8a80-4d43-a48c-d71e8a616c9a/composite-c1-package-manager-mini.png" alt="" /></a><br>
<em>The package manager lets you add features to the website.</em>

Recommended reading: [Beyond The Browser: From Web Apps To Desktop Apps](https://www.smashingmagazine.com/2017/03/beyond-browser-web-desktop-apps/)

### Under the Hood

The two package installations will add the following:

*   data types for articles and groups,
*   a user interface to manage these data types.
*   the basic plumbing needed to communicate with the Windows 8 app using JSON,
*   A configuration file in which you can set new providers for article content (i.e. to integrate with additional content sources).

To examine how these elements have come about or to extend something, get the <a href="https://c1packages.codeplex.com/">source code</a> for the <code>Composite.AppFeed.Server</code> and <code>Composite.AppFeed.Provider.Magazine</code> packages. We won’t get into the implementation details here; just note that things can be extended should you need it.</p>

## Managing Articles For The Magazine App

Once the packages have been installed, you will have the following new elements in the C1 console:

*   In the “Content” view, you will have a new folder named “Windows 8 App Magazine Content.” Here, you can create and edit articles and article groups.
*   In the “Media” view, you will have a new folder at `/Media Archive/App Feed images/Generic backgrounds`. Articles with no accompanying image will receive a random image from this folder to brighten up the Windows 8 tile-oriented interface.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/774c2ab8-d54c-4559-933b-e13356d1ba77/editing-article-large-mini-78x57.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26e833b2-dc91-474d-a400-4673a7fdf7dc/editing-article-mini.jpg" alt="" /></a><br>
<em>The editing UI in Composite C1 is called the C1 console.</em>

When you edit articles, you will do so visually or via the source view. You can do basic formatting, work with images, link to media and websites, embed HTML5 video, and call the C1 function to add dynamic content. This is the content that will show up in the Windows 8 app once we hook things up.</p>

### You Cannot Serve JavaScript in an Article’s HTML

In case you are wondering, if you add JavaScript-driven features to an article’s HTML, you will not see them run in the Windows 8 app. Security prohibits a Windows 8 HTML5 app from executing externally loaded JavaScript, which kind of makes sense because of the app’s privileged access to native APIs.

Should you need to include custom JavaScript, you can add your script files to the Windows 8 app project. On that side of the fence, anything goes.</p>

## Connect Your App To Your Azure Website

Once your website is running on a public URL, you can hook it up to your app like this:

1.  Open up the Windows 8 app project that we created in the first article in this series.
2.  Edit the `/js/settings.js` file.
3.  Change the value of `dataHostUrl` to reflect the URL of your local website, like `https://my-magazine-app.azurewebsites.net/`.
4.  Launch the app (hit F5).

When the app has launched, you will see the same content items as you saw in the CMS. If you go back to the CMS and change some content, you will see those changes in the app once you relaunch it.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/895df12d-d47f-45df-b85e-53fbb737bf8c/win8screenshot-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/49d55f03-1c2d-4e8c-82f3-756a6b403980/win8screenshot-mini.png" alt="" /></a><br>
<em>The sample content from the CMS is shown here in the Windows 8 app.</em>

## Publishing Your App To The Windows Store

The template that you initially downloaded and adapted should have all of the trimmings required for your app to pass the submission process. Still, make sure the following are in place:

*   Check that the information in `/package.appxmanifest` is relevant and up to date.
*   In `/js/settings.js`, the value of `privacyUrl` should point to a [public Web page containing your privacy policy](https://msdn.microsoft.com/en-us/library/windows/apps/hh694083.aspx#acr_4_1); the CMS is a convenient place to put such a page.
*   If your content has images featuring nudity or the like, set the correct age restrictions when submitting the app. Unlike [Apple](https://gizmodo.com/5562802/the-latest-examples-of-apples-stupid-editorial-censorship), Microsoft won’t censor your content, provided that you’ve set the [appropriate age rating](https://msdn.microsoft.com/en-us/library/windows/apps/hh694080.aspx).

You can <a href="https://msdn.microsoft.com/en-us/library/windows/apps/hh694081.aspx">run the app through a set of local tests</a> to catch issues that could complicate the approval process. Assuming you have created a developer account for the Windows Store, you can use Visual Studio to do the packaging, testing and uploading; go to <code>Project → Store → Create App Packages</code>.

The actual publication process is mostly Web-based and entails naming your app and adding descriptions and screenshots. For a detailed guide on this process, see “<a href="https://msdn.microsoft.com/en-us/library/windows/apps/br230835.aspx">Submitting Your App</a>.”

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/529f92a3-370c-4fce-955d-76278b7316b3/vs2012-project-store-create-app-packages-large-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8dff12f8-9e1f-46f5-aa04-bfa32cbf4d7d/vs2012-project-store-create-app-packages-mini.png" alt="" /></a><br>
<em>You can package, test and upload your app from within Visual Studio.</em>

I have seen a number of apps based on this template go through the approval process. Absent not having a working privacy policy or not specifying the correct age rating, the approval process has been a smooth ride.

Once you have submitted the app, expect it to be online within a day or two. And congratulations on publishing your first Windows 8 app!

Recommended reading: [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)

## Wrapping Up

With support for developing native Windows 8 apps using HTML5, JavaScript and CSS, Web developers can pretty easily step onto this scene.

The app we’ve created is generic and basic but open to customization. All of the elements used are open source and built for change, so <strong>you can modify the behavior and look of the app</strong> and customize the data model and CMS experience to meet your requirements.

Connecting your app to the content you manage in a CMS will come very naturally because you are using Web technology at both ends of the wire. The articles need not be the centerpiece of the app; obviously, you can take this in any direction. By having access to the OS-integrated JavaScript API available to Windows Store apps and by taking advantage of all of the HTML5 features of Internet Explorer 10, you will enjoy both a simpler and a richer development experience, all the while in a familiar setting.

If you have any questions, you can use the <a href="https://compositec1.codeplex.com/discussions">Composite C1 developer forum</a>. Happy coding!

<em>(al ea)</em>


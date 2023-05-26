---
title: 'How To Port Your Web App To Microsoft Teams'
slug: port-web-app-microsoft-teams
author: tomomi-imura-daisy-chaussee
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8fda5fb-e33f-4306-9325-e0e3fab7cc44/6-port-web-app-microsoft-teams.png
date: 2021-02-02T12:00:00.000Z
summary: >-
  On your list of places where people might access your web app, Teams is probably number “not-on-the-list”. But it turns out that making your app accessible where your users are already working has some profound benefits. In this article, we’ll look at how Teams makes web apps a first-class citizen, and how it enables you to interact with those apps in completely new ways. 
description: >-
  On your list of places where people might access your web app, Teams is probably number “not-on-the-list”. But it turns out that making your app accessible where your users are already working has some profound benefits. In this article, we’ll look at how Teams makes web apps a first-class citizen, and how it enables you to interact with those apps in completely new ways. 
categories:
  - Tools
  - Workflow
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Microsoft
  link: https://aka.ms/learntogether-smashing
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d7646c5-5c7a-47ef-b747-0413745ee642/microsoft-logo.svg
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://aka.ms/learntogether-smashing">Microsoft</a> who have been creating products such as Visual Studio, Teams, and many others, and have been actively supporting open source for years. <em>Thanks!</em>
---

Perhaps you are using Microsoft Teams at work and want to build an app that runs inside Teams. Or maybe you’ve already published an app on another platform and want to gain more users on Teams. In this article, we’ll see how to build a new web application in Teams, and how to integrate an existing one &mdash; with just a few lines of code.

You don’t need any prior experience to get started. We’ll use bare-minimum HTML code and toolsets to build a Teams tab (the simplest version of an app in Teams). While you’re walking through this tutorial, if you want to dive deeper, check out the on-demand videos from [Learn Together: Developing Apps for Teams](https://aka.ms/learntogether-smashing). It turns out that making your web application accessible where your users are already working has some benefits, including a reach of over 115 million daily active users. Let’s dive in!

## Microsoft Teams as a platform

You may be familiar with Teams as a collaborative communication tool, but as a developer, you could also view it as a **development platform**. In fact, Teams provides an alternative way to interact with and distribute your existing web applications. This is primarily because the tool has always been designed with the web in mind. One of the [key benefits of integrating web apps into Teams](https://channel9.msdn.com/Events/Microsoft-Learn/Learn-Together-Developing-Apps-for-Teams/Key-Benefits-of-Integrating-Web-Applications-into-Microsoft-Teams/?WT.mc_id=m365-11737-cxa) is providing a more productive way for users — your colleagues and Teams users around the world — to get the work done.

## Integration through tabs, embedded web apps

While there are many different paths to building and deploying Teams apps, one of the easiest is to integrate your existing web apps with Teams through what is called “tabs.” Tabs are basically embedded web apps created using HTML, TypeScript (or JavaScript), client-side frameworks such as React, or any server-side framework such as .NET.

Tabs allow you to **surface content in your app** by essentially embedding a web page in Teams using <code>&lt;iframes&gt;</code>. The application was specifically designed with this capability in mind, so you can integrate existing web apps to create custom experiences for yourself, your team, and your app users.

One useful feature about integrating your web apps with Teams is that you can pretty much use the developer tools you’re likely already familiar with: Git, Node.js, npm, and Visual Studio Code. To expand your apps with additional capabilities, you can use specialized tools such as the [Teams Yeoman generator command line tool](https://github.com/pnp/generator-teams) or [Teams Toolkit Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) and the [Microsoft Teams JavaScript client SDK](https://docs.microsoft.com/en-us/javascript/api/overview/msteams-client?view=msteams-client-js-latest/?WT.mc_id=m365-11737-cxa). They allow you to retrieve additional information and enhance the content you display in your Teams tab.

## Build a tab with an existing code sample

Let’s get started with the basics. (If you want to take it a step further to actually deploy your app, you can jump to the [Learn Together videos](https://channel9.msdn.com/Events/Microsoft-Learn/Learn-Together-Developing-Apps-for-Teams/?WT.mc_id=m365-11737-cxa)) to learn more.

To simplify the steps, let’s take a look at a code sample, so instead of the tooling outlined above, the only things you’ll need are:

*   Permission to develop on Teams or a developer tenant, which you can get for free through the [M365 Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program/?WT.mc_id=m365-11737-cxa),
*   App Studio: [install the App Studio app](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/build-and-test/app-studio-overview?WT.mc_id=m365-11737-cxa) in your Teams client
*   Basic web development skills

In this article, we’re going to use a web-based IDE called [Glitch](https://glitch.com/), which allows you to host and run this project quickly in the browser, so you don’t have to worry about the tunneling or deployment at this time. For the full-scale approach from start to finish, you can check out a [comprehensive tutorial on Microsoft Docs](https://docs.microsoft.com/en-us/microsoftteams/platform/build-your-first-app/build-first-app-overview/?WT.mc_id=m365-11737-cxa), which includes examples of a slightly more advanced [messaging extension](https://docs.microsoft.com/en-us/microsoftteams/platform/build-your-first-app/build-messaging-extension) or a [bot](https://docs.microsoft.com/en-us/microsoftteams/platform/build-your-first-app/build-bot).

Although Glitch is a great tool for tutorial purposes, this is not a scalable environment so, in reality, you'll also need a way to deploy and host your web services. In a nutshell, while you are developing, you need to set up a local development with a localhost tunneling, such as the 3rd party tool [ngrok](https://ngrok.com/), and for production, you'll need to deploy your app to a cloud service provider, for example, [Microsoft Azure Web Services](https://azure.microsoft.com/en-us/free/cloud-services/?WT.mc_id=m365-11737-cxa).

Also, you can use on-premises infrastructure to host your web services, but they must be publicly accessible (not behind a firewall). For this article, we will focus on how to make your web app available on Teams, so let’s go back to Glitch for now!

First, let’s go to the [sample code page](https://glitch.com/~msteams-tab-minimum) and **remix the project**. Remixing is like forking a repo on GitHub, so it generates a copy of the project for you, letting you modify the code however you want without messing with the original.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8fda5fb-e33f-4306-9325-e0e3fab7cc44/6-port-web-app-microsoft-teams.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8fda5fb-e33f-4306-9325-e0e3fab7cc44/6-port-web-app-microsoft-teams.png" sizes="100vw" caption="Remix the <a href='https://glitch.com/~msteams-tab-minimum'>sample code page</a> first. We’ll use it a starting foundation for our project. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8fda5fb-e33f-4306-9325-e0e3fab7cc44/6-port-web-app-microsoft-teams.png'>Large preview</a>)" alt="" >}}

Once you have your own project repo, you’ll also automatically get your own web server URL. For example, if your generated project name is <code>achieved-diligent-bell</code>, your web server URL would be https://achieved-diligent-bell.glitch.me. Of course, you can customize the name if you want.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8688370a-8e0e-4e8b-a709-2f2f6176374a/8-port-web-app-microsoft-teams.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8688370a-8e0e-4e8b-a709-2f2f6176374a/8-port-web-app-microsoft-teams.png" sizes="100vw" caption="Double-check your project name in the left upper corner. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8688370a-8e0e-4e8b-a709-2f2f6176374a/8-port-web-app-microsoft-teams.png'>Large preview</a>)" alt="" >}}

Web services up and running, you'll need to create an **app package** that can be distributed and installed in Teams. The app package to be installed to the Teams client contains two icons and a JSON manifest file describe the metadata for your app, the extension points your app is using, and pointers to the services powering those extension points.

## Create an app package

Now, you will need to create an app package to make your web app available in Teams. The package includes:

<pre><code class="language-markup">📁 your-app-package
 └── 📄 manifest.json
 └── 🖼 color.png (192x192)
 └── 🖼 outline.png (32x32)
</code></pre>

When creating your app package, you can choose to create it manually or use **[App Studio](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/build-and-test/app-studio-overview/?WT.mc_id=m365-11737-cxa)**, which is a useful app inside Teams that helps developers make Teams apps (yes, meta indeed). App Studio will guide you through the configuration of the app and create your app manifest automatically.

Once you have installed the App Studio app in your Teams client, open the app. You can launch it by clicking the three dots in the left menu bar.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14430cc0-fc75-41c9-b0f1-2342fcd1b569/7-port-web-app-microsoft-teams.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14430cc0-fc75-41c9-b0f1-2342fcd1b569/7-port-web-app-microsoft-teams.png" sizes="100vw" caption="Launch the App Studio app by clicking the three dots in the left menu bar. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14430cc0-fc75-41c9-b0f1-2342fcd1b569/7-port-web-app-microsoft-teams.png'>Large preview</a>)" alt="" >}}

Then, click the **Manifest Editor** tab from the top and select **Create a new app**.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f928edf0-90b4-42b6-95a8-247a92188c46/10-port-web-app-microsoft-teams.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f928edf0-90b4-42b6-95a8-247a92188c46/10-port-web-app-microsoft-teams.png" sizes="100vw" caption="Proceed with the Manifest Editor in the top navigation and select 'Create a new app'. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f928edf0-90b4-42b6-95a8-247a92188c46/10-port-web-app-microsoft-teams.png'>Large preview</a>)" alt="" >}}

You are going to need to fill out all the required fields including the app names, descriptions, etc.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e12d1ed8-b66d-4537-8409-edf6db3c78f6/9-port-web-app-microsoft-teams.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e12d1ed8-b66d-4537-8409-edf6db3c78f6/9-port-web-app-microsoft-teams.png" sizes="100vw" caption="Fill in some details, such as app names and descriptions. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e12d1ed8-b66d-4537-8409-edf6db3c78f6/9-port-web-app-microsoft-teams.png'>Large preview</a>)" alt="" >}}

In the App URLs section, fill out your privacy and TOU web pages. In this example, we are just using the placeholder URL, https://example.com.

Configure your personal tab by selecting **Capabilities > Tabs** from the left menu.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7631ce0b-49d3-4f8d-b052-d378c6b59e4f/2-port-web-app-microsoft-teams.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7631ce0b-49d3-4f8d-b052-d378c6b59e4f/2-port-web-app-microsoft-teams.png" sizes="100vw" caption="Now, you can configure the capabilities of the tab. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7631ce0b-49d3-4f8d-b052-d378c6b59e4f/2-port-web-app-microsoft-teams.png'>Large preview</a>)" alt="" >}}

Click the **Add button** under **Add a personal tab** and enter the info. Under Content URL, enter your webpage URL (in this case, it should be `https://[your-project-name].glitch.me/index.html`).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe1ff88e-ad8f-49cb-b5ed-caea4d90b56e/1-port-web-app-microsoft-teams.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe1ff88e-ad8f-49cb-b5ed-caea4d90b56e/1-port-web-app-microsoft-teams.png" sizes="100vw" caption="You will need to add your content URL — the one we’ve defined earlier. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fe1ff88e-ad8f-49cb-b5ed-caea4d90b56e/1-port-web-app-microsoft-teams.png'>Large preview</a>)" alt="" >}}

In the index.html file has a few lines of static HTML code:

<pre><code class="language-html">&lt;h1&gt;Hello world! &lt;/h1&gt;
&lt;p&gt;This is the bare-minimum setting for MS Teams Tabs.&lt;/p&gt;
</code></pre>

Feel free to tweak the content in the index.html as you want. This is the content to be displayed in your Teams client. Finally, go to **Finish > Test and distribute**.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f7ed630-cbc5-401f-98c1-c032ae43cef9/4-port-web-app-microsoft-teams.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f7ed630-cbc5-401f-98c1-c032ae43cef9/4-port-web-app-microsoft-teams.png" sizes="100vw" caption="Now you should be ready to finish, test and distribute. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f7ed630-cbc5-401f-98c1-c032ae43cef9/4-port-web-app-microsoft-teams.png'>Large preview</a>)" alt="" >}}

If you get any errors, you’ll have to go back and fix them. Otherwise, you can proceed by clicking “Install”. And voilà, now you have your own personal tab!

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfe2a513-63a2-46ac-bc00-2ff362cd4514/3-port-web-app-microsoft-teams.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfe2a513-63a2-46ac-bc00-2ff362cd4514/3-port-web-app-microsoft-teams.png" sizes="100vw" caption="Here we go: our first Tab is ready to go. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bfe2a513-63a2-46ac-bc00-2ff362cd4514/3-port-web-app-microsoft-teams.png'>Large preview</a>)" alt="" >}}

## Additional features with Teams SDK

This code sample only contains the bare minimal HTML code sample to just show you how to configure Teams to display your web app in Tabs. But of course, your web apps don’t need to be static, and you can **use web frameworks such as React** if you wish! (There are more deep-dive [examples using React](https://docs.microsoft.com/en-us/learn/modules/embedded-web-experiences/?WT.mc_id=m365-11737-cxa) that you can dive into as well.)

Teams has its own [JavaScript SDK](https://docs.microsoft.com/en-us/javascript/api/overview/msteams-client?view=msteams-client-js-latest&WT.mc_id=m365-11737-cxa) to provide additional functionality too, such as loading a configuration popup for teams, get user’s locale info, etc.

One useful example is detecting the “theme” of a Teams client — Teams has three themes, light (default), dark, and high-contrast mode. You would think CSS should handle the theming, but remember, your web app is displayed inside of the Teams' <code>iframe</code>, so you would need to use the SDK to handle the color change.

You can include the JavaScript either from [npm](https://www.npmjs.com/package/@microsoft/teams-js):

<pre><code class="language-bash">npm install --save @microsoft/teams-js
</code></pre>

Or include in your HTML:

<pre><code class="language-html">&lt;script src="https://statics.teams.cdn.office.net/sdk/v1.8.0/js/MicrosoftTeams.min.js"&gt;&lt;/script&gt;
</code></pre>

Now you can detect the current theme with the <code>getContext</code> method. And this is how you can determine the body text color:

<pre><code class="language-javascript">microsoftTeams.initialize();

microsoftTeams.getContext((context) => {
  if(context.theme !== 'default') {
    document.body.style.color = '#fff';  }
});
</code></pre>

The theme can be changed by a user after loading, so to detect the theme change event, add the following code snippet:

<pre><code class="language-javascript">microsoftTeams.registerOnThemeChangeHandler((theme)=> {
  if(theme !== 'default') {
    document.body.style.color = '#fff';
    document.body.style.color = 'inherit';
}
});
</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cade413a-734b-43cc-b845-1f6a83ffaff0/5-port-web-app-microsoft-teams.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cade413a-734b-43cc-b845-1f6a83ffaff0/5-port-web-app-microsoft-teams.png" sizes="100vw" caption="And so we’ve switched from a light mode to dark mode. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cade413a-734b-43cc-b845-1f6a83ffaff0/5-port-web-app-microsoft-teams.png'>Large preview</a>)" alt="" >}}

Hopefully, this simple tutorial helped you to get started with the first steps. If you’d like to continue developing for Teams, you can add more capabilities such as adding Teams-native UI components, search features, **messaging extensions**, and conversational bots, to build more interactive applications.

For a comprehensive guide using the recommended toolsets (Visual Studio Code, Yeoman Generator, etc.), check out [Teams Developer Docs](https://docs.microsoft.com/en-us/microsoftteams/platform/overview/?WT.mc_id=m365-11737-cxa) where you can learn more about tabs, messaging extensions, bots, webhooks, and the other capabilities that the Teams developer platform provides.

## Next Steps

With just a few clicks, you can integrate your apps into Teams and create new experiences for your users. And once you’ve developed apps and deployed them to Teams, you’ll have the potential of reaching a wide audience of users that use Teams daily.

You can [get started building today](https://docs.microsoft.com/en-us/learn/paths/m365-msteams-associate/?WT.mc_id=m365-11737-cxa) or [learn more from Learn Together: Developing Apps for Teams](https://aka.ms/learntogether-smashing) with on-demand videos and demos all around building apps for Teams.

{{< signature "vf, il" >}}

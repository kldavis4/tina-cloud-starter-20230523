---
title: Cross-Platform Native Apps With A Single Code Set Using Telerik NativeScript
slug: cross-platform-native-apps-single-code-set-telerik-nativescript
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d20fbcf-ea8f-4155-857a-75c73f155650/telerik-nativscript-opt-preview-78x34.png
date: 2016-07-29T17:46:15.000Z
author: nicraboy
description: >-
  Mobile applications are now a critical part of most enterprises, and there are
  many ways to create them, but what are the differences between these options
  and how do you choose between them? Do you choose to create native
  applications as Google and Apple intend? Do you choose to develop a mobile web
  hybrid application? Or do you find a middle ground?

  We’re going to look at some of the common problems with developing mobile
  applications, both native and hybrid, and how NativeScript by Telerik fills
  the gap. We’ll proceed to develop a NativeScript Android and iOS application
  from scratch (using the supplied [source
  code](https://smashingmagazine.com/provide/2016_nicraboy_sourcecode.zip)), and
  then convert the same application to use the bleeding-edge Angular 2
  JavaScript framework.
categories:
  - Mobile
  - Apps
  - Development
  - iOS
  - Android
---
Mobile applications are now a critical part of most enterprises, and there are many ways to create them, but what are the differences between these options and how do you choose between them? Do you choose to create native applications as Google and Apple intend? Do you choose to develop a mobile web hybrid application? Or do you find a middle ground?

We’re going to look at some of the common problems with developing mobile applications, both native and hybrid, and how NativeScript by Telerik fills the gap. We’ll proceed to develop a NativeScript Android and iOS application from scratch (using the supplied <a href="https://smashingmagazine.com/provide/2016_nicraboy_sourcecode.zip">source code</a>), and then convert the same application to use the bleeding-edge Angular 2 JavaScript framework.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Providing A Native Experience With Web Technologies](https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/)
*   [Diverse Test-Automation Frameworks For React Native Apps](https://www.smashingmagazine.com/2016/08/test-automation-frameworks-for-react-native-apps/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)

Going forward it is probably a good idea to know some information on who I am. I am an application developer that has been developing mobile applications as a hobby for the past five years. My mobile application projects were developed using a variety of technologies including native, Apache Cordova based frameworks, and NativeScript. I do not work for or have partnerships with any of the companies mentioned in this article. I am a tech enthusiast telling my story about mobile application development.

{{% feature-panel %}}

## What’s The Problem With Traditional App Development?

The Android marketplace, currently known as Google Play, launched in 2009, and the iTunes App Store launched in 2008. These opened the door to a new kind of software development. Developers could create an application for either platform and sell it in the app store.

Back then, if someone wanted to develop an iOS application, they would need to do so using the Objective-C programming language. Now, of course, Swift is an option for developing iOS applications as well. When it comes to Android applications, they could and still can be developed using Java.

Let’s go through a simple example. Let’s look at how to find an application’s version for Android:

<pre><code class="language-java">import android.content.pm.PackageInfo;
import android.content.pm.PackageManager;

PackageInfo packageInfo = getApplicationContext()
    .getPackageManager()
    .getPackageInfo(getApplicationContext().getPackageName(), PackageManager.GET_META_DATA);

System.out.println(packageInfo.versionCode);</code></pre>

To accomplish the same thing in Objective-C for an iOS application, the following would be done:

<pre><code class="language-objectivec">NSString *version = [[NSBundle mainBundle] objectForInfoDictionaryKey: @"CFBundleShortVersionString"];
NSLog(@"%@", version);</code></pre>

The problem here is that you need to know at least two different programming languages, one for each platform, to be able to develop applications that support both Android and iOS. For an independent or hobbyist developer, this could be time-consuming, and for an enterprise, hiring for the multi-platform skill sets could get expensive. After all, supporting only one mobile platform is no longer a good idea.

This is where hybrid mobile applications come into play.</p>

## What’s The Problem With Hybrid App Development?

Developing hybrid mobile applications isn’t anything new. PhoneGap, which has now split to become PhoneGap and Apache Cordova, came into existence in 2009. Hybrid frameworks such as Apache Cordova set out to make it easier for developers to create mobile applications by allowing them to use web technologies, namely CSS3, HTML5 and JavaScript. Many developers are already familiar with these technologies. By using web technologies, these frameworks solved the problem of developers needing to know specific platform languages (Objective-C and Java), as well as the platform APIs. Android and iOS applications could be created from the same code set.

Let’s continue our example of finding the application version, but this time with Apache Cordova and JavaScript.

<pre><code class="language-javascript">cordova.getAppVersion.getVersionNumber().then(function(version) {
    console.log(version);
});</code></pre>

This snippet will find the application version for both Android and iOS. This reduces the number of languages one needs to know, as well as the need for developer diversity. Instead of two developers developing for two platforms, you have one developing for both.

The problem with most of these hybrid frameworks is that they rely heavily on the web view of the device. Not all web views are treated equally, which results in an application performing unpredictably on the thousands of devices that exist. Old devices might not be able to process web code as quickly as new devices.

This is where NativeScript applications come into play.</p>

## What Is NativeScript, And How Does It Solve These Problems?

NativeScript is an open-source, cross-platform, mobile-development framework that uses common web technologies, as Apache Cordova does, to develop native Android and iOS applications that share a single code set — emphasis on <strong>native</strong> and <strong>single code set</strong>.

Like Apache Cordova, NativeScript uses JavaScript and a subset of CSS to create iOS and Android applications. The core difference here is in the user interface.

The user interface of a NativeScript application is designed in XML markup instead of HTML. While similar, they are not quite the same markup languages. XML is converted to the Android and iOS native equivalents at compile time, rather rendering in a web view, which has potentially poor performance on various devices. In other words, applications designed with NativeScript are rendered as native code, rather than parsed in a web view.

Take the following snippet, which continues the task of finding an application’s version:

<pre><code class="language-javascript">appversion.getVersionName().then(function(version) {
    console.log(version);
});</code></pre>

Writing this snippet is easier than writing the equivalents in Java and Objective-C and not too different from the equivalent in Apache Cordova. The main difference is that no web view is involved.

But why did I decide to dabble with NativeScript when there are similar cross platform native technologies like Xamarin or React Native? For one, I don't know ReactJS and I am not very strong with C#, both critical in the use of Xamarin and React Native. The most important selling point to me, which I explain towards the bottom of the article, is NativeScript's ability to support the Angular 2 JavaScript framework. Angular 2 is a very well constructed framework, created by Google, and having the option to use it is fantastic.

So, how does one create a NativeScript application?

## Creating Native Android And iOS Apps With NativeScript

NativeScript applications can be created on Mac, Linux and Windows computers with minimal configuration. We’ll see how to build an application that allows for user input in a popup dialog.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d20fbcf-ea8f-4155-857a-75c73f155650/telerik-nativscript-opt-preview-78x34.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8559be0f-f9f4-41cb-8cba-1f17cb907986/telerik-nativscript-opt-preview.png" alt="Android and iOS app built with NativeScript" width="500" height="218" /></a><figcaption>Android and iOS apps built with NativeScript. (Image: <a href="https://www.thepolyglotdeveloper.com">Nic Raboy</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d20fbcf-ea8f-4155-857a-75c73f155650/telerik-nativscript-opt-preview-78x34.png">View large version</a>)</figcaption></figure>

## Installing The Dependencies

Although NativeScript applications are developed in JavaScript, XML and a subset of CSS, the NativeScript command-line interface (CLI) is required for managing and building projects. The node package manager (npm), which is conveniently bundled with <a href="https://nodejs.org">Node.js</a>, is required to install the <a href="https://docs.nativescript.org/angular/start/quick-setup.html#the-nativescript-cli">NativeScript CLI</a>.

With Node.js installed, execute the following from the command prompt (Windows) or terminal (Mac and Linux):

<pre><code class="language-bash">npm install -g nativescript</code></pre>

On Mac or Linux, the use of <code>sudo</code> is typically required.

The NativeScript CLI isn’t the only requirement. To build an Android application, Java and the <a href="https://developer.android.com/studio/index.html">Android SDK</a> must first be installed. Android applications can be built from Mac, Linux or Windows machines. To build an iOS application, Xcode and the iOS development tools must be installed. The catch here is that iOS applications can only be built on a Mac.</p>

## Creating A New Project For Android And iOS

With the NativeScript dependencies installed, it is time to create a new project and start developing. From the terminal or command prompt, execute the following command:

<pre><code class="language-bash">tns create SmashingProject</code></pre>

This command will create a new project using the base NativeScript template and JavaScript. The great thing about NativeScript, and many JavaScript frameworks in general, is that you may use TypeScript. For example, to create a TypeScript project, execute the following instead:

<pre><code class="language-bash">tns create SmashingProject --template tsc</code></pre>

Other templates can be found on one of Telerik’s <a href="https://www.tjvantoll.com/2016/02/22/creating-nativescript-templates/">code blogs</a>. They make it easy to start development in certain scenarios. Perhaps you want to develop a JavaScript application — there is a template for that. Maybe you want to develop with TypeScript — there is a template for that. And so on.</p>

## Coding For Both Platforms

Our new project isn’t particularly useful yet because it cannot be built for any mobile platforms. At this point, various build platforms can be added.

In the command prompt or terminal, with the project as the current working directory, execute the following:

<pre><code class="language-bash">tns platform add android
tns platform add ios</code></pre>

These two commands will <a href="https://docs.nativescript.org/angular/tutorial/ng-chapter-1.html#13-add-target-development-platforms">add both the Android and iOS build platforms</a>. Remember that iOS can only be added on a Mac computer. Attempting to do so on a Windows or Linux computer will result in errors. In other words, Mac can build for Android and iOS, while Windows and Linux can build for Android only. This is because Apple hardware and software are proprietary, a benefit to people who own a Mac.

With the project created and the build platforms added, we can start developing.</p>

### Understanding the Model, View, View Model (MVVM) Structure

Before we get into the code, it is important to understand the model, view, view model (MVVN) structure that NativeScript follows. Each component can be described as follows:

*   The **model** can be thought of as an [application domain model](https://en.wikipedia.org/wiki/Domain_model). All of the business and validation logic happens in this file.
*   The **view** is the UI layer of the NativeScript application. It is built with a combination of XML markup and a [subset of CSS](https://docs.nativescript.org/ui/styling). Even though CSS can be used to design the user interface, not all CSS properties are available for use. This further reminds us that NativeScript applications are not web applications.
*   The **view model** contains properties, functions and data that are exposed to the application view. For example, suppose the view has a form with various text fields and a button. These text fields and button would be bound to the view model. When the button is clicked, a function from within the view model would be called. The values of the text fields would be accessible via the view model as well.

Each screen of a NativeScript application typically has its own MVVM, and breaking this up keeps the code clean. In our example project, add the following to the freshly created NativeScript project:

<pre><code class="language-bash">app/views/home/home.xml
app/views/home/home.js
app/views/home/home-view-model.js</code></pre>

These files represent the first page of the application.</p>

### Data-Binding With Observables

The properties, functions and other data elements found in a view model are exposed via an observable object or array. An <a href="https://docs.nativescript.org/cookbook/data/observable">observable</a> can be thought of data that appears over time, asynchronously. By using observables, the UI knows that the data in them isn’t finalized and that it can change at any time. This becomes useful if the data changes either in the front end or back end of the application.

Let’s look at the view model for the project. Open <code>app/views/home/home-view-model.js</code> and include the following code:

<pre><code class="language-javascript">var Observable = require("data/observable").Observable;

function createViewModel() {
    var viewModel = new Observable();
    viewModel.firstname = "";
    viewModel.lastname = "";

    viewModel.submit = function() {
        alert(this.firstname + " " + this.lastname);
    }

    return viewModel;
}

exports.createViewModel = createViewModel;</code></pre>

The view model returns an observable with <code>firstname</code> and <code>lastname</code> properties, as well as a single <code>submit</code> function. Anything in this observable can be accessed from the UI.</p>

### Creating That Fancy UI in Half the Time

The UI found in the <code>app/views/home/home.xml</code> file will contain a basic form, with two input fields and a button. Open it and include the following:

<pre><code class="language-markup">&lt;Page xmlns="https://schemas.nativescript.org/tns.xsd" navigatingTo="onNavigatingTo"&gt;
    &lt;StackLayout&gt;
        &lt;Label text="First Name:"&gt;&lt;/Label&gt;
        &lt;TextField text="{{ firstname }}"&gt;&lt;/TextField&gt;
        &lt;Label text="Last Name:"&gt;&lt;/Label&gt;
        &lt;TextField text="{{ lastname }}"&gt;&lt;/TextField&gt;
        &lt;Button text="Submit" tap="{{ submit }}"&gt;&lt;/Button&gt;
    &lt;/StackLayout&gt;
&lt;/Page&gt;</code></pre>

The <a href="https://docs.nativescript.org/cookbook/ui/label">Label</a> tags represent static text in the UI. The <a href="https://docs.nativescript.org/cookbook/ui/text-field">TextField</a> tags represent form fields that accept user input. And the <a href="https://docs.nativescript.org/cookbook/ui/button">Button</a> tags represent a tappable entity. The containing <a href="https://docs.nativescript.org/cookbook/ui/layouts/stack-layout">StackLayout</a> represents a vertically aligned group of UI elements.

Anything in braces is bound to the view model. Imagine trying to create this UI using Android’s XML template system or Xcode’s storyboard editor. It would probably take a lot longer, with more source code.</p>

### Bringing the View and View Model Together With a Model

The view and view model don’t do much alone. They need to be brought together with a NativeScript model. This model is found in the <code>app/views/home/home.js</code> file. Open it and include the following:

<pre><code class="language-javascript">var createViewModel = require("./home-view-model").createViewModel;

function onNavigatingTo(args) {
    var page = args.object;
    page.bindingContext = createViewModel();
}

exports.onNavigatingTo = onNavigatingTo;</code></pre>

The view model is bound to the page via the <code>bindingContext</code>.</p>

### Defining the First Page of the Application

The application MVVM was created, but NativeScript doesn’t know about it yet. To define the home view as the first page of the application, it must first be set in the application’s Bootstrap file. Open <code>app/app.js</code> and include the following code:

<pre><code class="language-javascript">var application = require("application");
application.start({ moduleName: "views/home/home" });</code></pre>

Other global application logic can be placed in this file as well.</p>

## Running The NativeScript App

With the application created, it can now be run on a device or in a simulator. Android and iOS simulators are not available immediately when you install Xcode or the Android SDK. Make sure to download one beforehand.

Be aware of a few commands when you try to run the application.

<pre><code class="language-bash">tns build [platform]</code></pre>

This command will <a href="https://docs.nativescript.org/angular/tutorial/ng-chapter-1.html#14-running-your-app">build the application</a> for either iOS or Android. It will not install the application or run it. To kill two birds with one stone, you can build and run the application with the following:

<pre><code class="language-bash">tns run [platform]</code></pre>

This command will install the application to a device, not a simulator. If you don’t have a physical Android or iOS device, adding the <code>--emulator</code> tag to the command will launch a simulator, which can be tested locally on your Mac, Linux or Windows computer.

During the development phase, the application will feel like it takes ages to rebuild. NativeScript has a live-reload feature that refreshes the device or simulator nearly instantly after you hit the save button. It can be used like so:

<pre><code class="language-bash">tns livesync [platform] --emulator --watch</code></pre>

This command watches for code changes and <a href="https://docs.nativescript.org/angular/tutorial/ng-chapter-1.html#15-development-workflow">live-syncs</a> them to the simulator — very convenient during development.</p>

## Take The NativeScript App To The Next Level With Angular 2

As of NativeScript 1.7, Angular 2 is supported, but not the default method of development as seen above. You might choose to create a NativeScript application with Angular 2 rather than vanilla JavaScript if you want to share application logic between a web application and a NativeScript application. The Angular 2 framework can be carried between web and mobile, making it very convenient and easy to maintain.

Let’s create an Angular 2 NativeScript app with the same goal as our previous example.

Create a new Angular 2 project by executing the following from the command prompt or terminal:

<pre><code class="language-bash">tns create SmashingAngular --ng</code></pre>

Notice this time that the template is the Angular 2 template, which includes all necessary dependencies for building an Angular 2 NativeScript application.

Add the appropriate build platforms to the project by executing the following, keeping in mind that iOS needs a Mac for development:

<pre><code class="language-bash">tns platform add ios
tns platform add android</code></pre>

The Angular 2 template doesn’t work off of an MVVM structure like the previous application. Instead, it has only an XML file and TypeScript component. Create the following files and directories in the project:

<pre><code class="language-bash">app/views/home/home.ts
app/views/home/home.xml</code></pre>

The application logic found in the <code>app/views/home/home.ts</code> file will look like this:

<pre><code class="language-javascript">import {Component} from "@angular/core";

@Component({
    selector: "my-app",
    templateUrl: "./views/home/home.xml",
})
export class Home {

    public firstname: string;
    public lastname: string;

    constructor() {
        this.firstname = "";
        this.lastname = "";
    }

    public submit() {
        alert(this.firstname + " " + this.lastname);
    }

}</code></pre>

The TypeScript component pairs with the <code>app/views/home/home.xml</code> file and contains two scope variables that can be bound to the UI. When the <code>submit</code> function is called, an alert will appear presenting whatever the two variables contain.

The UI file paired to this component looks like the following:

<pre><code class="language-markup">&lt;StackLayout orientation="vertical"&gt;
    &lt;Label text="First Name:"&gt;&lt;/Label&gt;
    &lt;TextField [(ngModel)]="firstname"&gt;&lt;/TextField&gt;
    &lt;Label text="Last Name:"&gt;&lt;/Label&gt;
    &lt;TextField [(ngModel)]="lastname"&gt;&lt;/TextField&gt;
    &lt;Button text="Submit" (tap)="submit()"&gt;&lt;/Button&gt;
&lt;/StackLayout&gt;</code></pre>

The use of <code>ngModel</code> is common in Angular applications. It is how bindings are accomplished between the UI and the application component.</p>

## Conclusion

NativeScript fills the gap in Java and Objective-C development, as well as the hybrid web development facilitated by frameworks such as Apache Cordova. Instead of developing Android applications with Java and iOS applications with Objective-C, we can create applications from a single code set, made up of JavaScript and XML. The applications are compiled to native applications, rather than running as low-performance web views.

NativeScript offers several ways to develop applications, including the bleeding-edge Angular 2 JavaScript framework.</p>

### Resources

*   [NativeScript](https://www.nativescript.org)
*   [Angular 2](https://www.angular.io/)
*   [Node.js](https://www.nodejs.org)

{{< signature "da, ml, al, vf" >}}


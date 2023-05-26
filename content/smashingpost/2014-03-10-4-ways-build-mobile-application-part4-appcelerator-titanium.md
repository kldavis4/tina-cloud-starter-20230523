---
title: 'Four Ways To Build A Mobile Application, Part 4: Appcelerator Titanium'
slug: 4-ways-build-mobile-application-part4-appcelerator-titanium
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ec3fcba-018d-4ca8-8975-0a767b6f99a5/illu-titanium.png
date: 2014-03-10T10:28:04.000Z
author: peter-traeg
description: >-
  This article is the last in a series of articles covering four ways to develop
  a mobile application. In previous articles, we covered how to build a tip
  calculator in [native iOS](https://www.smashingmagazine.com/2013/11/22/four-ways-to-build-a-mobile-app-part1-native-ios),
  [native Android](https://www.smashingmagazine.com/2014/01/10/four-ways-to-build-a-mobile-app-part2-native-android/)
  and [PhoneGap](https://www.smashingmagazine.com/2014/03/11/four-ways-to-build-a-mobile-app-part3-phonegap/). In this article, we’ll look at another cross-platform development tool, Appcelerator Titanium.  
categories:
  - Mobile
  - Apps
  - iOS
  - Android
  - Native
---
This article is the last in a series of articles covering four ways to develop a mobile application. In previous articles, we covered how to build a tip calculator in [native iOS](https://www.smashingmagazine.com/2013/11/22/four-ways-to-build-a-mobile-app-part1-native-ios), [native Android](https://www.smashingmagazine.com/2014/01/10/four-ways-to-build-a-mobile-app-part2-native-android/) and [PhoneGap](https://www.smashingmagazine.com/2014/02/11/four-ways-to-build-a-mobile-app-part3-phonegap/). In this article, we’ll look at another cross-platform development tool, Appcelerator Titanium.

PhoneGap enabled us to build a tip calculator app quickly and have it run on both the Android and iOS platforms. In doing so, we were left with a user interface (UI) that, while quite usable, did not offer quite the same experience as that of a truly native application. Our PhoneGap solution leveraged a Web view and rendered the UI with HTML5 and CSS3.

By contrast, Appcelerator Titanium applications render the UI using the platform’s native controls. **Titanium is intended to provide the experience of a native UI**, along with portability between the iOS, Android and BlackBerry platforms. Appcelerator plans to release support for Windows Phone and Windows 8 [later this year](https://www.appcelerator.com/blog/2014/01/windows-8-support-whats-going-on/).

Here’s the Appcelerator Titanium version of our sample FasTip application running on both iOS and Android:

[![FasTip application on iOS.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e6e91d41-ab7e-422b-b3f8-20301452568b/01-ios-screenshot-500.png "FasTip application on iOS.")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d5352fe-9505-40b2-b1c0-15853bc792be/01-ios-screenshot.png)  
_FasTip application on iOS. ([Large preview](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d5352fe-9505-40b2-b1c0-15853bc792be/01-ios-screenshot.png))_

{{% feature-panel %}}

[![FasTip application on Android.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e44fede-adbe-4834-b05f-af26b3345960/02-android-screenshot-500.png "FasTip application on Android.")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dbbfced-6a44-47bb-a43b-a4bfad10c0f3/02-android-screenshot.png)  
_FasTip application on Android. ([Large preview](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dbbfced-6a44-47bb-a43b-a4bfad10c0f3/02-android-screenshot.png))_

With Titanium, an application is written in JavaScript. However, instead of manipulating an HTML DOM, as would be done in a PhoneGap application, the JavaScript is interacting with Appcelerator Titanium’s API. Titanium provides UI objects for things like buttons, text fields, lists and so on, and these are backed by the mobile platform’s truly faithful representation of the respective native controls. In many cases, the code you write for one platform can run unmodified on other platforms as well. However, as we’ve seen with native iOS and Android’s different approaches to navigating screens (for example, `ViewControllers` with the `NavigationController` on iOS and `Activities` in Android), not all of these differences can be abstracted well. As such, even with Appcelerator, at least some parts of your code will have to be written specifically for each platform.

Appcelerator consists of a suite of products, including the Titanium SDK for building mobile applications, and some cloud services that can be used for the back end of the application. The products may be used independently of one another or in combination. The Titanium SDK and an integrated development environment (IDE) are offered free of charge for any commercial application. Appcelerator makes available at additional cost an [Enterprise](https://www.appcelerator.com/plans-pricing/) version that includes additional support, cloud services and analytics capabilities. Training courses and a certification program are also available for an additional fee.

A Eclipse-based IDE named [Titanium Studio](https://www.appcelerator.com/titanium/titanium-studio/) is offered by Appcelerator. This IDE contains a JavaScript editing environment, along with a source-level debugger.

[![Titanium Studio IDE overview.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dd9eac5-a463-49a7-9da6-5c477474d2fe/03-titanium-studio-ide-500.jpg "Titanium Studio IDE overview.")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f15089bf-e0fe-43ea-affb-8a6bdd734b29/03-titanium-studio-ide.jpg)  
_Titanium Studio IDE overview. ([Large preview](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f15089bf-e0fe-43ea-affb-8a6bdd734b29/03-titanium-studio-ide.jpg))_

As of the time of writing, no graphic layout tools exist that are akin to the ADT layout manager for Android or the StoryBoards and Interface Builder for iOS. With Titanium, the layout of screens is written either in JavaScript or in an XML definition language, as part of Appcelerator Titanium’s Alloy framework. Alloy is an application framework that allows you to specify the UI of an application in XML and apply styles to the controls in the project via a CSS-like syntax. I’ve included the code for both an Alloy and a Classic version of our application in the [same GitHub repository](https://github.com/ptraeg/mobile-apps-4-ways) that holds the code samples for the other articles in this series.</p>

## Starting Your First Project

Appcelerator Titanium and Titanium Studio are available free of charge. Appcelerator offers a “[Quick Start](https://docs.appcelerator.com/titanium/latest/#!/guide/Quick_Start-section-29004949_QuickStart-LaunchingTitaniumStudio)” document that fully covers the steps to get started. Just follow these steps to get Titanium’s tools:

1.  To use Titanium, you must [create a free developer account](https://my.appcelerator.com/auth/signup) on the Titanium website. Through this developer account, you will obtain the Titanium SDK and Titanium Studio IDE.
2.  Once you have a developer account, you’ll have access to Appcelerator’s [developer resources](https://my.appcelerator.com/resources). Here, you’ll find a series of “Getting Started” links, including ones to obtain the tools for Mac, Windows and Linux.
3.  Just as with PhoneGap, you’ll have to install the native SDKs for the platforms you wish to support. However, Titanium Studio makes that easy. A [Platform Configuration](https://docs.appcelerator.com/titanium/latest/#!/guide/Installing_Platform_SDKs-section-29004842_InstallingPlatformSDKs-StudioPlatformConfigurationTool) tool built right into Titanium Studio makes it easy to install and update the native SDKs:

    [![Install the native SDKs](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d35a193d-6429-4364-87dc-6966788f8bd4/04-install-sdk-500.png "Install the native SDKs")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/921c2b4e-289c-40bf-8d23-be7e3155a74d/04-install-sdk.png)  
    _Install the native SDKs. ([Large preview](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/921c2b4e-289c-40bf-8d23-be7e3155a74d/04-install-sdk.png))_

    Now you’re ready to create a project.
4.  From the “File” menu, choose “New” → “Mobile App Project.” This will open a dialog box that lets you choose an Alloy or Classic development project. As mentioned, Alloy is an application framework by Appcelerator that enables you to specify the UI of an application in XML and to use a CSS-like syntax to style the application. The Classic templates take an all-code approach. Appcelerator recommends Alloy for most new Titanium projects. Most of the examples in this article will use Alloy because I find its code structure to be more maintainable.

    [![Choose a development project.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/12a3f881-7f0a-4c44-b4fa-8f06eb83d794/05-newapp-step1-500.png "Choose a development project.")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7f6d0d9-9621-420d-af97-fc081ab7bcec/05-newapp-step1.png)  
    _Choose a development project. ([Large preview](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7f6d0d9-9621-420d-af97-fc081ab7bcec/05-newapp-step1.png))_

5.  Selecting the “Default Alloy” project will give you a simple project with one “Hello World” screen, a useful starting point. Clicking “Next” opens the next dialog:

    [![A simple project with as a useful starting point.](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/880b2aa3-12af-4917-a479-62eaefeab02c/06-newapp-step2-500.png "A simple project with as a useful starting point.")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3eff37e-408a-4865-8ab5-b95a5fc397e2/06-newapp-step2.png)  
    _A simple project with as a useful starting point. ([Large preview](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f3eff37e-408a-4865-8ab5-b95a5fc397e2/06-newapp-step2.png))_

    In the example above, we’ve filled in the fields for an app named “MySampleApp.” Once you click the “Finish” button, Titanium Studio will create the project’s directory structure and open it in the project explorer.
6.  Running the app is as easy as selecting a simulator in the device drop-down menu and pressing the “Run” button:

    [![run-on-ios-500](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16a3a4e4-25e4-4d44-b82e-2291636468b2/07-run-on-ios-500.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f28c26e-4caa-463d-a493-ce06d1b9d1a6/07-run-on-ios.png)  
    _Running the app. ([Large preview](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0f28c26e-4caa-463d-a493-ce06d1b9d1a6/07-run-on-ios.png))_

7.  The “Run” button has a drop-down menu of its own that provides options for debugging and packaging your application for distribution.</p>

## Organizing An Appcelerator Project

For this article, we’ll focus on the Alloy version of the application. Its project structure looks like this:

[![Project Structure](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a877bb96-3040-40c2-94c2-4de66360dca2/08-directory-structure.png "Project Structure")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a877bb96-3040-40c2-94c2-4de66360dca2/08-directory-structure.png)  
_Project Structure_

A project is a collection of XML, TSS (we’ll get to these later) and JavaScript files, along with any graphic assets required for the application. When the project is compiled for a platform, the compiler translates the XML and TSS files into JavaScript code and packages the code, along with the graphic assets, into a deployment package for the relevant mobile platform. The XML and TSS files are not interpreted at runtime; they’re there simply to save you the tedium of writing a lot of code for the layout and styles of the controls. Titanium’s documentation shows [how the XML and TSS are mapped](https://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_Concepts-section-34636240_AlloyConcepts-AlloyandtheTitaniumSDK) to JavaScript. If you’re familiar with Adobe Flex development, the XML files are handled much like MXML files.

<p>Every project starts off with an <code>index.xml</code> file, which serves as the starting point of the application. Upon opening the <code>index.xml</code> file in the <code>views</code> directory, we see the following:<br>

<pre class="language-markup"><code class="language-markup">&lt;Alloy&gt;
  &lt;Require id="calculator" src="calculator" platform="android"/&gt;
  &lt;NavigationWindow id="index" platform="ios"&gt;
    &lt;Require src="calculator" id="calculator"/&gt;
  &lt;/NavigationWindow&gt;
&lt;/Alloy&gt;</code></pre>

<p>This markup tells the compiler to load the contents of <code>calculator.xml</code> into the main window. Note the <code>platform="android"</code> attribute; every element in Alloy may be <a href="https://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_XML_Markup-section-35621528_AlloyXMLMarkup-ConditionalCode">decorated with a <code>platform</code> and/or <code>formFactor</code> attribute</a> to indicate that the element is meant for a particular platform (Android, iOS, etc.) or form factor (handheld or tablet).</p>

<p>After the <code>Require</code> element for Android, we see the same <code>Require</code> element but wrapped in a <a href="https://docs.appcelerator.com/titanium/latest/#!/api/Titanium.UI.iOS.NavigationWindow">NavigationWindow</a> element. As mentioned, Android and iOS have different mechanisms for moving the user between screens. In this case, <code>NavigationWindow</code> corresponds to the <code>UINavigationController</code> that we used to build our native iOS application. Android does not have a corresponding navigation element, and so navigation is handled differently. Titanium’s SDK exposes both forms of navigation to the developer, rather than attempting to abstract the differences via some lowest-common-denominator approach. This provides more direct access to the native controls but requires the developer to deal with these differences. As a result, in several places in our code, we’ll have to account for the requirements of each platform.</p>

<p>For each view, we have a corresponding controller file. Here are the contents of <code>index.js</code>:</p>

<pre class="language-javascript"><code class="language-javascript">if (OS_IOS) {
  Alloy.Globals.navgroup = $.index;
}

if (OS_ANDROID) {
  $.calculator.getView().open();
} else {
  $.index.open();
}</code></pre>

<p>This file begins with some code that checks <a href="https://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_Controllers-section-34636384_AlloyControllers-ConditionalCode">special variables</a> provided by Alloy to indicate the platform on which the application is running. For iOS, we assign a reference to the <code>NavigationWindow</code> object onto the <code>Alloy.Globals</code> object. <code>Alloy.Globals</code> is simply a common namespace where you can store objects that can be accessed anywhere in the application. In this case, we’re storing a reference to <code>NavigationWindow</code> so that we can access it anywhere in the app. The last section of code opens the controller that will display the main calculator view. For Android, we’ll open the view on the controller directly. For iOS, the view is in <code>NavigationWindow</code>, so we need to open <code>NavigationWindow</code> instead.</p>

## Defining The UI

<p>On the first screen of our application, the UI is defined by the <code>views/calculator.xml</code> file. It contains elements to describe each <code>TextField</code>, <code>Button</code>, <code>Label</code> and so on on the screen.</p>

<pre class="language-markup"><code class="language-markup">&lt;Alloy&gt;
  &lt;Window title="Alloy FasTip" backgroundColor="#fff"&gt;
    &lt;!-- Android menu --&gt;
    &lt;Menu platform="android"&gt;
      &lt;MenuItem
          onClick = "clickedSettings"
          title = "Settings"
          icon = "Ti.Android.R.drawable.ic_menu_preferences"
          showAsAction = "Ti.Android.SHOW_AS_ACTION_IF_ROOM" /&gt;
    &lt;/Menu&gt;

    &lt;!-- rightNavButton for platforms that support it --&gt;
    &lt;RightNavButton platform="ios"&gt;
      &lt;Button id="settingsButton"
          onClick="clickedSettings"
          title="Settings" /&gt;
    &lt;/RightNavButton&gt;

    &lt;TextField id="billAmtTextField"
          top="40"
          width="146"
          height="35"
          textAlign="right"
          hintText="Bill amount"
          keyboardType="Ti.UI.KEYBOARD_DECIMAL_PAD"
          returnKeyType="Ti.UI.RETURNKEY_DONE" /&gt;

    &lt;Button id='calcTipButton'
        onClick="clickedCalculate"
        title="Calculate Tip"
        top="100" width="122"
        class="primaryButton" /&gt;

    &lt;View top="170" width="Ti.UI.SIZE" height="Ti.UI.SIZE"&gt;
      &lt;Label left="13" width="124"
          top="0"
          textAlign="Ti.UI.TEXT_ALIGNMENT_RIGHT"&gt;
        Tip Amount:
      &lt;/Label&gt;
      &lt;Label id="tipAmtLabel" left="130"
          top="0" width="80"
          textAlign="Ti.UI.TEXT_ALIGNMENT_RIGHT"&gt;
        $0.00
      &lt;/Label&gt;
      &lt;Label left="13" width="124" top="30"
          textAlign="Ti.UI.TEXT_ALIGNMENT_RIGHT"
          class="totalAmt"&gt;
        Total Amount:
      &lt;/Label&gt;
      &lt;Label id="totalAmtLabel" left="130"
          top="30" width="80"
          textAlign="Ti.UI.TEXT_ALIGNMENT_RIGHT"
          class="totalAmt"&gt;
        $0.00
      &lt;/Label&gt;
    &lt;/View&gt;
  &lt;/Window&gt;
&lt;/Alloy&gt;</code></pre>

<p>At the top of the file, we run into another difference between platforms. Android supports menus that, as we saw in the article on native Android, appear in the action bar on Android 4.x devices. This menu element describes a single menu option on this screen, the settings wrench.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acbda0ac-19ec-4d3f-97d5-e0043bdd4a6a/09-android-actionbar.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acbda0ac-19ec-4d3f-97d5-e0043bdd4a6a/09-android-actionbar.png" alt="Android Action Bar." title="Android Action Bar." width="487" height="75"/></a><figcaption>Android Action Bar</figcaption></figure>

<pre class="language-markup"><code class="language-markup">&lt;!-- Android menu --&gt;
&lt;Menu&gt;
  &lt;MenuItem
      onClick = "clickedSettings"
      title = "Settings"
      icon = Ti.Android.R.drawable.ic_menu_preferences
      showAsAction = Ti.Android.SHOW_AS_ACTION_IF_ROOM /&gt;
&lt;/Menu&gt;</code></pre>

<p>The menu element applies only to Android, so decorating this with a platform-specific attribute, such as <code>platform="android"</code>, is not necessary. In iOS, this element will be ignored by the Alloy compiler.</p>

<p>To make the settings button appear in iOS, we need to add it to the iOS navigation controller’s button bar. This is accomplished with the following element, with an attribute that restricts it to iOS (<code>platform="ios"</code>):</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/82f4e14e-3460-44ff-bfaf-acfbf9676cee/10-ios-navcontroller.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ae56dd5-a0de-4255-97c0-d2119a080a61/10-ios-navcontroller-500.png" title="Android Navigation Controller" alt="iAndroid Navigation Controller" width="300" height="59" /></a><figcaption>Android Navigation Controller</figcaption></figure>

<pre class="language-markup"><code class="language-markup">&lt;RightNavButton platform="ios"&gt;
  &lt;Button id="settingsButton" onClick="clickedSettings"
      systemButton="Titanium.UI.iPhone.SystemButton.COMPOSE" /&gt;
&lt;/RightNavButton&gt;</code></pre>

<p>The <code>systemButton</code> attribute in the <code>Button</code> element above identifies one of iOS’ standard button styles. You could, of course, remove it and supply a text title or other suitable image if you desire.</p>

<p>Notice that in both cases, the menu item and the navigation button invoke the same function via the <code>onClick</code> attribute. The code for this screen is controlled by a JavaScript file with the same name as the <code>.xml</code> file. The Alloy framework refers to this as a controller, and by convention it is found in the <code>controllers/calculator.js</code> file. Alloy follows a <a href="https://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_Concepts-section-34636240_AlloyConcepts-ConventionoverConfiguration">set of conventions</a> that govern where all files are located in the directory structure and how they relate to each other.</p>

<p>The first function in our <code>calculator.js</code> file handles the click event when the user taps the “Calculate tip” button:</p>

<pre class="language-javascript"><code class="language-javascript">function clickedCalculate(e) {
  var tipPct = Ti.App.Properties.getDouble('tipPct', .15);
  var billAmt = parseFloat($.billAmtTextField.value) || 0;
  var tipAmt = billAmt * tipPct;
  var totalAmt = billAmt + tipAmt;
  $.tipAmtLabel.text = '$' + tipAmt.toFixed(2);
  $.totalAmtLabel.text = '$' + totalAmt.toFixed(2);
  $.billAmtTextField.blur();
}

Ti.App.addEventListener('recalc', clickedCalculate);</code></pre>

<p>To calculate the tip, we first attempt to retrieve the default tip percentage from <code>Ti.App.Properties</code>. This object is much like the objects we’ve used in the other three implementations: <code>NSUserDefaults</code> in iOS, <code>SharedPreferences</code> in Android and <code>LocalStorage</code> in PhoneGap. The controls that we defined in the <code>calculator.xml</code> file become properties in this controller, and we can reference them by using the <code>$.&lt;controlId&gt;</code> format. The calculation itself is very much like the code we used for PhoneGap &mdash; after all, this is still JavaScript.</p>

<p>In the <code>calculator.js</code> controller, we’ve also added an event listener via the <code>Ti.App.addEventListener</code> method. This enables our code to respond to events that occur elsewhere in the application. In this case, we’ll fire the <code>recalc</code> event from the settings screen when the user exits the window. This way, the calculator will always be up to date with the latest tip percentage. As we’ll soon see, the settings screen does not contain a direct reference to the calculator, so it cannot invoke methods on it directly. Using event listeners in this manner is a good way to decouple the controllers in our application, allowing them to continue communicating but without direct references to each other. These events come with some performance overhead, so use a direct callback if they’re going to fire in rapid succession.</p>

## Navigating Between Screens: Dealing With Platform Differences

<p>The following code is run when the user clicks the “Settings” button:</p>

<pre class="language-javascript"><code class="language-javascript">function clickedSettings(e) {
  var settingsController = Alloy.createController('settings');
  var win = settingsController.getView();

  if (Alloy.Globals.navgroup) {
    Alloy.Globals.navgroup.openWindow(win);
  } else if (OS_ANDROID) {
    win.open();
  }
}</code></pre>

<p>As soon as the user clicks the “Settings” button in the calculator view, the <code>clickedSettings</code> method on the calculator’s controller is invoked. Here, we create an instance of <code>settingsController</code> and get a reference to its view. The <code>Alloy.Globals</code> object is then checked for whether it contains a <code>navgroup</code> reference. Recall that this was established for iOS applications in the <code>index.js</code> file when our app first launched. Now we can use that <code>navgroup</code> to open the settings window. Android has no <code>navgroup</code> object, so we would just open the window directly.</p>

## The Settings Screen

<p>The settings screen is defined in <code>settings.xml</code>, and its content is very similar to what we saw in <code>calculator.xml</code>:</p>

<pre class="language-markup"><code class="language-markup">&lt;Alloy&gt;
  &lt;Window title="Settings" backgroundColor="#fff"&gt;
    &lt;!-- Android menu --&gt;
    &lt;Menu platform="android"&gt;
      &lt;MenuItem
          onClick="clickedDone"
          title="Done"
          icon = "Ti.Android.R.drawable.ic_menu_save"
          showAsAction = "Ti.Android.SHOW_AS_ACTION_IF_ROOM" /&gt;
    &lt;/Menu&gt;

    &lt;Label top="35"&gt;Set tip percentage&lt;/Label&gt;

    &lt;TextField id="tipPctTextField"
          top="72"
          width="60"
          height="35"
          textAlign="right"
          hintText="Tip %"
          keyboardType="Ti.UI.KEYBOARD_DECIMAL_PAD"
          returnKeyType="Ti.UI.RETURNKEY_DONE"
        &gt;&lt;/TextField&gt;
    &lt;Label top="72" left="195"&gt;%&lt;/Label&gt;

    &lt;Button id='saveButton'
        onClick="clickedSave"
        title="Save Settings"
        top="120" width="130"
        class="primaryButton" &gt;&lt;/Button&gt;
  &lt;/Window&gt;
&lt;/Alloy&gt;</code></pre>

<p>Just as with the calculator view, there are two different approaches to including a button in the action bar (in Android) or the navigation bar (in iOS). The “Done” button and “Save” button are wired to the relevant controller methods, as we’ll see next.</p>

<p>Upon the “Save” button being clicked, the following code is run in <code>settings.js</code>:</p>

<pre class="language-javascript"><code class="language-javascript">var tipPct = parseFloat( $.tipPctTextField.value );
if (tipPct > 0) {
  // Persist the new percentage value
  Ti.App.Properties.setDouble('tipPct', tipPct / 100);
  Ti.API.log('info', 'Settings saved');
  closeSettings();
} else {
  var dialog = Ti.UI.createAlertDialog({
        message: 'Enter a tip percentage greater than zero',
      ok: 'Try again',
      title: 'Invalid percentage'
      }).show();
}</code></pre>

<p>To preserve the value of the tip percentage for future use, we use <code>Ti.App.Properties.setDouble</code>, which will persist the value between runs of our application. For debugging purposes, we’ll also log a message via <code>Ti.API.log</code>, which will write a message to the device log. This is essentially the same as writing a message to <code>console.log()</code> in a browser.</p>

<p>The next important section of code deals with how the window is closed:</p>

<pre class="language-javascript"><code class="language-javascript">function closeSettings() {
  Ti.App.fireEvent("recalc");
  var settingsWindow = $.getView();
  if (Alloy.Globals.navgroup) {
    Alloy.Globals.navgroup.closeWindow(settingsWindow, {animated:true});
  } else {
    settingsWindow.close();
  }
}</code></pre>

<p>In this case, first, we’ll fire the <code>recalc</code> event that we established a listener for in the calculator controller earlier on. This will trigger the calculator to apply the new percentage value when the user leaves this screen. Just as we saw with opening the settings window, some platform-specific code is needed when the window is closed. The <code>Alloy.Globals</code> namespace is checked once again to see whether there is a <code>navgroup</code> for iOS. If so, we use it to close the window. On Android, we can close the window directly. Upon closing this window, the user will return to the previous calculator window and, because we’ve fired the <code>recalc</code> event, will see the tip calculation updated to reflect the newly saved percentage.</p>

## Styling Our Application

<p>In the past, Appcelerator required the developer to programmatically define each control and its attributes. This was tiresome if you wished to change the style of an application. You might have needed to go back and change a lot of code. With the Alloy framework, Appcelerator has added <a href="https://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_Styles_and_Themes-section-35621526_AlloyStylesandThemes-TitaniumStyleSheets">Titanium style sheets</a> (TSS). These work much like CSS in Web development. Each view and controller in an application has a corresponding TSS file, which allows you to adjust the style for that view in the application. In addition, the <code>app.tss</code> file governs the overall style of the whole application, allowing us to style the controls in all views of the application. The <code>app.tss</code> file is ideal for establishing consistency across views in an application. Here is the <code>app.tss</code> code for our application:</p>

<pre class="language-css"><code class="language-css">"Window": {
  backgroundColor:"#fff"
}

"Window[platform=android]": {
  navBarHidden: true
}

"Label": {
  width: Ti.UI.SIZE,
  height: Ti.UI.SIZE,
  color: "#000"
}

"TextField": {
  color: "#000"
}

"TextField[platform=ios]": {
  paddingLeft:10,
  paddingRight:10,
  borderColor:"#000",
  borderRadius: "10",
  borderWidth: "1"
}

"Button": {
  width: Ti.UI.SIZE,
  height: Ti.UI.SIZE,
  borderRadius: 15
}

".primaryButton": {
  backgroundColor: '#3883B5',
  color: '#fff'
}</code></pre>

<p>The TSS entries above may be applied to Alloy elements such as the <code>Window</code> and <code>TextField</code> objects. They may also be applied to specific controls, via a <code>class</code> attribute that works just like the <code>class</code> attribute in HTML. Recall that a “Calculate tip” button was in our <code>calculator.xml</code> file:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dd472b0-34f2-4b57-b929-17bc96d763b5/11-calctip-button.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1dd472b0-34f2-4b57-b929-17bc96d763b5/11-calctip-button.png" alt="“Calculate tip” button" title="“Calculate tip” button" width="249" height="63" /></a><figcaption>“Calculate tip” button</figcaption></figure>

<pre class="language-markup"><code class="language-markup">&lt;Button id='calcTipButton' onClick="clickedCalculate"
    title="Calculate Tip"
    top="100" width="122"
    class="primaryButton" &gt;
&lt;/Button&gt;</code></pre>

<p>This button has a class of <code>primaryButton</code>, which maps to the style defined in <code>app.tss</code>:</p>

<pre class="language-css"><code class="language-css">".primaryButton": {
  backgroundColor: '#3883B5',
  color: '#fff'
}</code></pre>

<p>We’ve used the same class name for the “Save settings” button on the settings screen, and it will receive the same styles. In addition, the “Calculate tip” button has rounded corners because we’ve styled all of the buttons in our application to look so:</p>

<pre class="language-css"><code class="language-css">"Button": {
  width: Ti.UI.SIZE,
  height: Ti.UI.SIZE,
  borderRadius: 15
}</code></pre>

<p>You may also specify styles based on platform. This TSS code applies only to <code>TextFields</code> in iOS:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a7d73f8-ca07-4101-9336-e671566ada09/12-bill-amount.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a7d73f8-ca07-4101-9336-e671566ada09/12-bill-amount.png" alt="“Bill amount” button" title="“Bill amount” button" width="300" height="78" /></a><figcaption>“Bill amount” button</figcaption></figure>

<pre class="language-css"><code class="language-css">
"TextField[platform=ios]": {
  paddingLeft:10,
  paddingRight:10,
  borderColor:"#000",
  borderRadius: "10",
  borderWidth: "1"
}</code></pre>

<p>Alloy also allows you to create platform-specific folder names under the <code>styles</code> directory and obtain styles that way as well. In addition, you can create <a href="https://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_Styles_and_Themes-section-35621526_AlloyStylesandThemes-Themes">themes</a> to apply different assets and styles based on the configuration of a particular build. Using a theme, you could load an entirely different set of assets, which would be useful if you’re working with different branding requirements from multiple clients.</p>

## Other Alloy Features

<p>Our simple application does not require several of Alloy’s other features, such as <a href="https://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_Models">models</a> and <a href="https://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_Collection_and_Model_Objects-section-36739589_AlloyCollectionandModelObjects-Collections">collections</a>. These features were actually drawn from the popular <a href="https://backbonejs.org/">Backbone.js</a> library, which should make them familiar to many JavaScript developers. In addition, you can reuse visual components across applications with <a href="https://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_Widgets">widgets</a>. A widget is self-contained and provides its own set of models, views and controllers, allowing it to be dropped into multiple applications.</p>

## Classic Appcelerator Applications

<p>In the GitHub repository, I’ve included sample code for our FasTip application written in the Classic development style. We won’t go through all of the code here &mdash; just a few highlights to show how this approach differs from Alloy. For most projects, I’d recommend using Alloy. However, note that Alloy essentially creates a Classic Appcelerator application from your Alloy code. Understanding traditional Appcelerator development is important if you want to dynamically add or remove controls at runtime.</p>

<p>When a Titanium application starts, it runs the contents of the <code>app.js</code> file. In FasTip, we’re largely relying on the same <code>app.js</code> file that is created when a new project is initialized in Titanium Studio. Note that the following code identifies which platform the app is running on:</p>

<pre class="language-javascript"><code class="language-javascript">(function() {
  // Determine platform and form factor and render appropriate components
  var osname = Ti.Platform.osname,
    version = Ti.Platform.version,
    height = Ti.Platform.displayCaps.platformHeight,
    width = Ti.Platform.displayCaps.platformWidth;

  var isTablet = osname === 'ipad' ||
    (osname === 'android' && (width > 899 || height > 899));</code></pre>

<p>The <code>Ti.Platform.osname</code> property provides the main clue as to whether we are running on an iPad, iPhone or Android device. You can see from this code that by using data provided by Ti.Platform, we can assume some things about the type of device that the app is running on. We saw the <code>Require</code> element used in Alloy to load one controller into another. Here’s an example done in straight code:</p>

<pre class="language-javascript"><code class="language-javascript">if (osname === 'iphone') {
Window = require('ui/handheld/ios/ApplicationWindow');
} else {
  Window = require('ui/handheld/android/ApplicationWindow');
}
new Window().open();</code></pre>

<p>Notice that the code snippet above loads a particular version of the <code>ApplicationWindow.js</code> script based on the value of <code>platform</code>.</p>

<p>The following is a block of code to add some controls to a window. It shows how controls may be created programmatically without the use of Alloy.</p>

<pre class="language-javascript"><code class="language-javascript">var isAndroid = (Ti.Platform.osname === 'android');

var billAmtTextField = Ti.UI.createTextField({
  id: 'billAmtTextField',
  borderStyle: Ti.UI.INPUT_BORDERSTYLE_ROUNDED,
  keyboardType: Ti.UI.KEYBOARD_DECIMAL_PAD,
  returnKeyType: Ti.UI.RETURNKEY_DONE,
  hintText:'Bill amount',
  textAlign: Ti.UI.TEXT_ALIGNMENT_RIGHT,
  top:40,
  width:'146dp', height: '35dp',
  color:'#000'
});
if (isAndroid) {
  billAmtTextField.font = {fontSize: '12dp'};
}
self.add(billAmtTextField);

var calcBillButton = Ti.UI.createButton( {
  title: 'Calculate Tip',
  top:100,
  width:'122dp', height: '30dp',
  color:'#000'
});
if (isAndroid) {
  calcBillButton.font = {fontSize: '10dp'};
}
self.add(calcBillButton);</code></pre>

<p>The <code>self</code> object above refers to the window, and <code>self.add()</code> is used to add each of the controls to the window. Specifying all of these attributes for every control that you add of a given type is tedious. Moreover, keeping the styles consistent in an app is difficult without the help of TSS style sheets, as in our Alloy example. In practice, if you do not use Alloy, then building controls from a JavaScript “factory pattern” would be better than calling the <code>Ti.UI.create</code> methods directly. This way, you would only have to change the factory methods to generate controls with different attributes.</p>

## Extending Titanium With Modules

<p>While Titanium does a great job of providing much of the common functionality found in the mobile platforms that it supports, what if you need to access device features that are not directly offered by Titanium? In PhoneGap, the plugin system provides this capability. Titanium offers a similar system, called <a href="https://docs.appcelerator.com/titanium/latest/#!/guide/Using_Modules">modules</a>, which enable your Titanium application to access native code. The <a href="https://marketplace.appcelerator.com/home">Appcelerator Marketplace</a> is a registry of both free and paid modules. In addition, a <a href="https://github.com/appcelerator/titanium_modules">GitHub repository</a> contains free open-source modules. You could, of course, <a href="https://docs.appcelerator.com/titanium/latest/#!/guide/Extending_Titanium_Mobile">write your own</a> modules, too.</p>

## Deploying Your Application

<p>Titanium Studio has a “Publish” option in the project explorer. Just right-click on the project and choose the appropriate publishing option:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaaecd8c-7a65-4a70-a43e-f18b7f2a0cb3/13-publish-app-step1.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ec5439b-a7e7-4334-beb8-a7bc8ba91757/13-publish-app-step1-500.png" title="Publish your application, Step 1." alt="Publish your application, Step 1." width="500" height="219" /></a><figcaption>Publish your application, Step 1. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eaaecd8c-7a65-4a70-a43e-f18b7f2a0cb3/13-publish-app-step1.png">Large preview</a>)</figcaption></figure>

As with any other development tool, you still need an account in the relevant app store to sell your application. Once you’ve chosen an option, the publishing dialogs will walk you through the process of signing the code and submitting it:</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03f33f7d-3370-44b5-98dc-0ead09a76ca1/14-publish-app-step2.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03f33f7d-3370-44b5-98dc-0ead09a76ca1/14-publish-app-step2.png" alt="Publish your application, Step 2." title="Publish your application, Step 2." width="498" height="511" /></a><figcaption>Publish your application, Step 2. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03f33f7d-3370-44b5-98dc-0ead09a76ca1/14-publish-app-step2.png">Large preview</a>)</figcaption></figure>

It’s convenient that this is built right into the Studio IDE, and the dialogs do a good job of walking you through the process. Titanium Studio’s documentation provides <a href="https://docs.appcelerator.com/platform/latest/#!/guide/Packaging_Titanium_Applications">more details</a> on the publishing process.</p>

## Appcelerator Cloud Services

<p>While not the focus of this article, I should mention <a href="https://www.appcelerator.com/cloud/">Appcelerator’s Cloud Services</a> (ACS). These services are a separate offering from Titanium. They are server-based back-end services that can be used to store data for an application. At present, the services vary from photo storage to access control. Titanium exposes these services in the following ways:</p>

<ul>
<li>in Titanium via a <a href="https://docs.appcelerator.com/cloud/latest/#!/guide/titanium">Ti.Cloud module</a>,</li>

<li>via a native <a href="https://docs.appcelerator.com/cloud/latest/#!/guide/ios">iOS</a> library,</li>

<li>via a native <a href="https://docs.appcelerator.com/cloud/latest/#!/guide/android">Android</a> library,</li>

<li>via a <a href="https://docs.appcelerator.com/cloud/latest/#!/guide/rest">REST-based API</a> for access from other platforms.</li>
</ul>

<p>A recent addition is <a href="https://docs.appcelerator.com/cloud/latest/#!/guide/node">Node.ACS</a>, which enables you to write custom <a href="https://nodejs.org/">NodeJS</a> server-side applications. This is useful for encapsulating custom business logic on the server side. There are certainly alternatives to ACS, including <a href="https://parse.com/">Parse</a> and <a href="https://www.stackmob.com/">StackMob</a>, but they don’t have the same level of integration with Appcelerator.</p>

## Learning Resources

<p>A series of <a href="https://bit.ly/TYZEGq">tutorials</a> are available to get you up to speed. Appcelerator offers a page of training resources, with many links on how to get started. It also offers a paid training and certification program for those who are interested in building skills in this way. The <a href="https://www.appcelerator.com/blog/">official blog</a> is also a good way to stay up to date on the latest news about the platform.</p>

<p>In addition to Appcelerator-supplied resources, <a href="https://www.tidev.io/">TiDev</a> is an independent resource for Titanium-related articles. Another repository of Titanium modules resides at <a href="https://gitt.io/">gitTio</a>, and Alloy-related components can be found at <a href="https://alloylove.com">Alloy Love</a></p>

## Appcelerator Titanium: Right For Your Project?

<p>Like most tools, this one has its pros and cons. The promise of cross-platform development, with better user experience (UX) performance than an HTML-based solution like PhoneGap, is certainly attractive. However, as we’ve seen from the examples above, the framework cannot fully abstract all of the differences between platforms and still provide a native-like experience. As such, you’ll likely find yourself tailoring the view and controller code in your application to each platform.</p>

<p>Because they’re still writing the platform-specific code with Appcelerator’s API, a developer would find it much easier to leverage their skills across multiple platforms &mdash; they’d still be writing everything in JavaScript. For non-visual portions of an application, doing things like making AJAX calls from an Appcelerator app is quite simple, and unlike the fully native platforms, the JSON responses from typical REST-based services are directly understood by JavaScript. The native platforms require you to use a JSON parser to transform the REST responses into something that the native language can work with. Even if you wind up splitting the code for the Android and iOS views in your application, you would likely have to write the data model and business logic code only once. This single base of code could then be accessed from the platform-specific views in your application.</p>

<p>As with any tool from a third-party vendor, there may be some lag before a platform’s new features become available in Appcelerator’s platform. The development team at Appcelerator doesn’t get access to betas of the iOS and Android SDKs any earlier than other developers, so it will take time for a platform’s new features to get added to the product. If you need access to cutting-edge features as soon as they’re released in beta, then you’re better off with a purely native approach. Still, Appcelerator is generally proactive in making its tools compatible with the latest SDK releases, enabling developers to update their apps soon after a new version of a platform has been made available to the general public. Answers to most support-related questions can be found in Appcelerator’s own forums. By contrast, questions relating to fully native development and to PhoneGap are more widely covered on third-party websites such as StackOverflow.</p>

## Series Summary

<p>We’ve seen how four different mobile technologies can be used to build the same application. A native application generally performs the best and provides the best access to a platform’s capabilities. Despite this, many enterprises are looking for solutions that run on multiple platforms.</p>

<p>PhoneGap is quite attractive to developers who have a strong background in HTML, CSS and JavaScript. It also offers a wide range of platform support, well beyond iOS and Android. As rendering performance and HTML5 compatibility improve on mobile devices, the gap in performance between native code and HTML narrows. Despite this, a UI implemented entirely in HTML and CSS might not be suitable for applications that are complex and have many animations. Still, in many cases, a properly written PhoneGap app provides a satisfying UX. The application’s UX designer and developer should work with the capabilities and limitations of the HTML5 platform, rather than try to force fit what could be accomplished in a purely native application.</p>

<p>Appcelerator requires the developer to learn its own API for UI controls &mdash; using, however, the native controls found on the platform. While the controls themselves will perform just as a native application’s would, all of the application logic will be running through a JavaScript engine. Thus, if the application performs a significant amount of calculations and data manipulation, then the performance would not match that of a truly native application. Moreover, Titanium abstracts the standard native controls into its own objects, meaning that not every property of the native controls would necessarily be exposed through Titanium. You could, of course, create modules to address this, but that would require additional effort. Depending on the number of modules necessary, the advantages of going with Titanium to begin with might be negated.</p>

<p>Your choice of development environment will depend largely on these factors:</p>

<ul>
<li><strong>Functional and UX requirements</strong><br />
As stated above, some types of applications require native development. If you are competing with a number of native apps in the app store, then you might have to build a native app as well, just to match or exceed the UX of the competing applications. Perhaps you need access to a feature in the latest version of the operating system, one not yet supported by PhoneGap or Titanium. Working around this with the relevant plugin or module in PhoneGap or Titanium might be possible. But this assumes that a plugin exists or that you have enough experience in the native environment to write the plugin yourself.</li>

<li><strong>Experience of the development team</strong><br />
Many people are interested in PhoneGap or Appcelerator because they want to avoid learning a new language and platform. However, one still has to understand plenty of nuances in developing for the mobile Web (in the case of PhoneGap) or for Titanium. While you might not have to learn a new language, you will certainly have to learn new APIs and have at least some knowledge of the underlying platform. For instance, with PhoneGap, one needs to be aware of the limitations of animation performance (particularly in old versions of Android), the responsiveness of touch events and so on. Poor performance in PhoneGap applications is often the result of developers not paying attention to these issues. Developers must learn to respect the conventions of the platform on which their app will run or risk frustrating end users. Remember that these are mobile apps, not Web apps or desktop apps. The techniques for developing Web or desktop applications do not necessarily hold true for mobile applications.</li>

<li><strong>Long-term maintenance</strong><br />
Over time, an application will likely need changes. Do you have resources available in the given development technology to perform this maintenance? Are Appcelerator Titanium developers any more readily available than native developers or HTML5 developers conversant with PhoneGap?</li>
</ul>

<p>We are fortunate to have several options for developing mobile applications. This overview has presented only four solutions. Other tools exist, such as <a href="https://xamarin.com/">Xamarin</a>’s products, which enable developers to write iOS, Android and Windows applications with .NET tools and C#. Developers of gaming applications might want to look at Corona SDK. Or perhaps you don’t need an app at all. If the browser’s capabilities would suffice, then a mobile website might be appropriate.</p>

<p>Hopefully, this series has provided insight into some of the options available for building an application. Here’s wishing you well with whatever development platform you find best meets your needs.</p>

{{< signature "al, ml" >}}


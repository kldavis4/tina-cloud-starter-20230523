---
title: A Guide To iOS App Development For Web Designers
slug: ios-sdk-for-designers
image: null
date: 2012-09-10T11:53:10.000Z
author: james-brocklehurst
description: >-
  As a designer looking to broaden your skill set, you’ve decided that learning
  to make native apps for Apple’s iOS platform is an attractive and potentially
  lucrative prospect. With a frisson of excitement, you start to do some
  research. The euphoria is short-lived however, as you quickly discover that
  **unless you are an experienced programmer, the task is far from easy**.
categories:
  - Mobile
  - Apps
  - iOS
  - iPhone
---
As a designer looking to broaden your skill set, you’ve decided that learning how to make native apps for Apple's iOS platform is an attractive and potentially lucrative prospect. With a frisson of excitement, you start to do some research. The euphoria is short-lived however, as you quickly discover that <strong>unless you are an experienced programmer, the task is far from easy</strong>.

The documentation provided by Apple is aimed at those with a degree in computer science. Books on iPhone and iPad development ask that you have a good grasp of Objective-C from the opening page. Online tutorials vary in quality, with many appearing out of date or contradictory.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Build A Mobile Website](https://www.smashingmagazine.com/2010/11/how-to-build-a-mobile-website/)
*   [Responsive Web Design: What It Is And How To Use It](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)

This post will help you get to know the iOS development tools a little better. It leads you through <strong>some choreographed steps of iPhone app development</strong>, even if you have little or no programming knowledge. It covers some key principles and applies these directly to something useful and relevant: the creation of a simple but functioning portfolio app.

{{% feature-panel %}}

The result will look like this:

<img loading="lazy" decoding="async" class="116798" title="iOS Portfolio App" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/379b53a0-ae4e-4e22-8431-5e218bd8f305/01-end-result.jpg" alt="iOS Portfolio App" width="550" height="266" />

## Going Native?

By “native” iOS development, we mean using Apple’s software development kit (SDK) and the programming language Objective-C to author apps for the iPhone, iPod Touch and iPad. Before we learn how to do this, it is worth mentioning why we would want to make an app this way, and what the alternatives might be.

In <a href="https://www.engadget.com/2010/09/09/apple-backpedaling-on-some-ios-development-restrictions-will-al/">relaxing the App Store’s submission review guidelines</a> in September 2010, Apple made it easier for developers to use third-party frameworks and more familiar languages, such as HTML, CSS and JavaScript, to create apps. Examples of such tools are Appcelerator’s Titanium Mobile, Nitobi’s PhoneGap (acquired by Adobe in 2011) and <a href="https://www.appmobi.com/">appMobi’s XDK</a> (now belonging to IBM), among others. In addition to the benefit of using the more familiar Web languages of HTML, CSS and JavaScript to author apps, these methods enable developers to output to other mobile platforms, such as Android and BlackBerry, with minimal rewriting of the source code.

The disadvantage of using third-party tools is that the resulting app will not be quite as efficient as one that is natively authored, and the newest features of the operating system and hardware will not be available, at least until the framework catches up. Each framework also has its own fairly extensive library of functions that have to be learned, along with its own idiosyncrasies, bugs and workarounds. Plus, to publish your app to the App Store, you will need to use Apple’s Xcode, the application used to work with the iOS SDK, so limited familiarity with native processes is still necessary.

A few “third way” solutions, such as Cocos 2D for iPhone and <a href="https://bakerframework.com/">Baker</a>, are also available, allowing you to connect framework files to an Objective-C project for a particular aim, such as to create a game or digital magazine. To make use of these and any others that come along in future, you will need at least a basic understanding of the SDK.

Therefore, if you are interested in developing for the iPhone, iPod and iPad and you accept that whatever authoring method you choose means having to find your way around Xcode, then getting familiar with the native SDK is a recommended first step.</p>

## Getting Started

You will need two things to be able to start working with the iOS SDK:

*   A Mac, running the latest version of OS X (there is currently no way to author natively for iOS on Windows or Linux, although apparently there is [a workaround](https://www.macincloud.com/));
*   Apple’s Xcode application.

To get Xcode, download it from the Mac App Store. It’s free but weighs in at nearly 1.5 GB and can take about half an hour to install, so you’ll need to put aside a bit of time to get it up and running.</p>

## Preparing Graphics

While waiting for that download to complete, we can look at how you might prepare and export graphics for iOS using Photoshop.

Because all iOS applications have one of two possible pixel densities (standard or Retina), you should aim to work in Photoshop using non-destructive techniques to reduce the need to design twice. This means creating buttons and interface elements using vector shapes and layer styles, and using smart objects for images, where possible. The recommended approach is to work at a Retina-display resolution first, and then scale down to standard resolution once the design is complete. Sometimes you will find that scaling down produces poor results, and you will have to tweak your smaller designs.

Plenty of templates with pre-built iOS system elements are available on the Web. <a href="https://www.teehanlax.com/blog/iphone-4-gui-psd-retina-display/">Teehan + Lax has one</a> that is pretty good and widely used. Apart from saving you from having to draw iOS system components from scratch, they also demonstrate how much space is left for content, once elements such as the status, navigation and tool bars are in place.

To set up a new blank iPhone document in an image editor, these are the settings you will need:

*   640 × 1136 pixels,
*   72 ppi,
*   RGB color mode.

The above is for a iPhone 5 or iPod Touch 5th generation.

The screen dimensions for the iPhone 4, 4S and iPod Touch fourth generation are slightly shorter, at 640 x 960 pixels. You can denote this in the same document using a ruler guide. Older non-retina devices are 320 × 480 pixels, which is exactly half the size of the fourth-gen retina display.

See Marc Edwards’ “<a href="https://www.smashingmagazine.com/2010/11/17/designing-for-iphone-4-retina-display-techniques-and-workflow/">Designing for iPhone 4 Retina Display</a>” for more information on iOS design techniques and workflows.</p>

### Some Quick Image Exporting Tips

*   iOS accepts a number of image formats, but PNG is recommended because of its support for alpha-transparency and its lossless compression.
*   Graphics for buttons should, in most cases, be exported just as background images, without accompanying text, because this allows for localization (in different languages), accessibility and text resizing between the Retina- and standard-display resolutions.
*   If exporting a button graphic, ensure that the pixels of the actual button are centered in the frame of the exported image, because Interface Builder doesn’t give you precise control over the positioning of button background images or foreground text. You might need to manually compensate for a drop shadow on the opposite sides, for instance.
*   Where possible, flatten design elements made from multiple layers into a single image file. Rebuilding layered UI components in Interface Builder can be a pain; plus, reducing the number of resources that your app uses will make it run quicker and take up less memory. Only interface components that need to respond to user interaction should be animated, and only interface components that will be controlled by the application should be exported as separate image files.
*   You will need to produce Retina and standard versions of every exported image and give them identical names, with a `@2x`suffix for the Retina version, like so:
    *   `image.png`
    *   `image@2x.png`
*   You can use my SuperSlicr Photoshop action (included in the package) to automate the scaling and exporting of elements from your PSD file.
*   Every pair of images that you make will need a unique and descriptive file name, because they are all stored in the same directory in the app bundle. File names should have only alphanumeric characters (no symbols), and underscores or hyphens instead of spaces. You may use capitalization.
*   Photoshop isn’t very good at compressing PNGs, so run them through porneL’s [ImageOptim](https://imageoptim.pornel.net/) to reduce their size before importing into Xcode. Xcode will also try to apply its own compression to imported images, which can sometimes increase file size, but [this can be disabled](https://imageoptim.com/xcode.html).</p>

## Xcode Overview

You’ve successfully installed Xcode? Great!

Next, you will need to download and unzip <a href="https://github.com/JamesBrocklehurst/Portfolio-iOS-App">these template files</a>. The package includes a source PSD, some exported PNGs and the required starter code.

In the package, navigate to the folder named <code>Begin Here</code>. Locate the Xcode project document named <code>Portfolio.xcodeproj</code>. Double-click on this file to open it in Xcode.

Once the document has loaded, click on the blue project icon on the left named <code>Portfolio, 1 target, iOS SDK</code>, and you should see a project summary screen in the main Xcode interface, as shown below. We will look at the contents of the summary screen in detail later.

<img loading="lazy" decoding="async" class="116800" title="Xcode Overview" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf191f15-c748-4735-8655-b6853af82cb5/03-xcode-overview.jpg" alt="Xcode Overview" width="550" height="322" />

The “Navigator” area on the left lists all of the files already associated with your project. These can be expanded out from the blue project icon. We will be mostly interested in those contained in the yellow <code>Portfolio</code> folder, or “group.” Three types of files are here:

*   `.h` A “header” (or interface) file.
*   `.m` A “message” (or implementation) file.
*   `.xib` An “XML interface builder” file, sometimes referred to as a NIB.

The “Editor” area will change depending on what task you are performing. Because we currently have the blue project file selected in the navigator, we are given the “Target Summary” screen. This gives us some basic options for our app, including which device types, iOS version and display orientation we want our app to support. We can also specify images to use for our app’s icon and launch image, which we will look at in detail later.

Single-click on <code>AppDelegate.m</code>. The editor area will now turn into a code editor and display the code contained in this file.

Now single-click on <code>MainWindow.xib</code> in the navigator area. The editor area will display Interface Builder, an integrated graphical user interface (GUI) for putting together the front-end of your application.

<img loading="lazy" decoding="async" class="116801" title="Interface Builder Overview" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d7e292e-8f78-4818-bdb1-c9f5fb73be9a/04-interface-builder-overview.jpg" alt="Interface Builder Overview" width="550" height="342" />

The “Inspector” has some tabbed controls at the top that you will need to be familiar with. The last four are the most important:

<img loading="lazy" decoding="async" class="116802" title="Inspector Bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/103c89f0-2eb8-455a-b2db-38b481dd09a7/05-inspector-bar.jpg" alt="Inspector Bar" width="550" height="250" />

The other important control is the big “Run” button in the top-left corner of Xcode. Pressing this will compile your project code into an app and then run it in an iOS simulator so that you can see whether it works without having to load it onto an actual device. If you press it now, it should launch the simulator and present you with a big virtual iPhone on your desktop.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7668e1a-f38a-4a1a-b3f6-32f16a356858/06-ios-simulator4.jpg"><img loading="lazy" decoding="async" class="119126" title="The iOS Simulator" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a7668e1a-f38a-4a1a-b3f6-32f16a356858/06-ios-simulator4.jpg" alt="The iOS Simulator" width="550" height="540" /></a>

The simulator works similar to an actual device. Have a play to see how it behaves. Under the “Hardware” menu, you can select different devices and iOS versions and simulate rotating and shaking the device. Holding <code>alt</code> allows you to pinch and zoom. The home button works, taking you to the springboard where there is even a functioning version of mobile Safari (which, incidentally, is great for testing locally hosted websites).

A more detailed guide to the interface is available in Apple’s “<a href="https://developer.apple.com/library/mac/#documentation/ToolsLanguages/Conceptual/Xcode4UserGuide/000-About_Xcode/about.html">Xcode 4 User Guide</a>.”

## Importing Graphics Into Xcode

The template package that you downloaded earlier contains some sample image files. You can either use these or use your own for the next section.

To import images into your project, Control-click on the “Images” group in the project navigator and select “Add Files to ‘Portfolio.’”

<img loading="lazy" decoding="async" class="116804" title="Adding Images" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07c9407c-3efd-47de-96fe-a298faa0edb3/07-add-images1.jpg" alt="Adding Images" width="400" height="381" />

Browse to the “PNGs” folder in the downloaded package and select all of the images. Check the “Copy items into destination group’s folder” box, and then click “Add.”

The images have now been imported into your project and are available to Xcode and Interface Builder. You can add more graphics to the “Images” group at any time by following this same process.</p>

## Editing The Template Without Writing Any Code

There is a debate in the iOS development community about whether one should build an app purely in code or with XIB files generated by Interface Builder and its GUI. Both methods seem to be supported by Apple, and each project necessitates its own approach. Developers who frown on the use of Interface Builder perhaps overlook the power of this tool, which enables us to establish the structure and outward appearance of our app efficiently and visually. For designers used to working with Adobe’s Creative Suite, this will be (almost) familiar territory. For this reason and because our app will be very “view-based,” we will use Interface Builder to begin with.

First, we will look at setting up some different screens, or “views,” that can be switched using some Tab Bar controls. Click on <code>MainWindow.xib</code> in the project navigator to bring up Interface Builder. In the library, select the “Show the Object Library” tab icon (the one that looks like a cube), and scroll through the list of objects until you find “View Controller.”

<img loading="lazy" decoding="async" class="116805" title="View Controller Object" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/775dd641-dc91-47da-b4e5-d0e3044f3553/08-view-controller-object.jpg" alt="View Controller Object" width="318" height="215" />

Expand the dock using the circular “Expand document outline” button at the bottom, then drag an instance of the View Controller object from the library onto the “Tab Bar Controller” in the dock. The Tab Bar Controller should expand, showing the View Controller nested inside.

Repeat this process twice more, until you have three View Controllers nested inside the Tab Bar Controller. The canvas area should also show the Tab Bar as having three unnamed tabs.

<img loading="lazy" decoding="async" class="116806" title="View Controllers Added To Tab Bar" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79c5ba90-d7d7-4e32-914a-72a7127945f2/09-view-controllers-added-to-tab-bar1.jpg" alt="View Controllers Added To Tab Bar" width="550" height="514" />

### View Controllers?

If you are wondering what a “View” and a “Controller” are, they are part of something called the “Model View Controller” (MVC) paradigm. This is an approach to programming that separates application data, logic and presentation to make things easier to work with. “Model” refers to the back-end aspect that manages data. “View” refers to the front-end user interface. “Controllers” bridge the front and back ends and enable things to happen in your app. We won’t be working with any 'persistent' data in this article, so we will only be encountering Views and their corresponding Controllers.</p>

### Creating Classes

We need to create some “classes” to generate each of our views; and because we are new to programming, this requires a bit of explanation first.

In object-oriented programming languages such as Objective-C, classes are used as a way to define elements within the application called “objects.” A class defines the qualities (or properties) that an object may have and what it can do (methods). It can then be asked to generate one or more “instances” of an object based on this definition, and these instances are used to make your application work.

Each of the three views that we want to make are objects, so we need to create some classes to be able to conjure them into existence.

To add a new View Controller class, Control-click on the yellow “Portfolio” folder in the navigator, and select “New File” from the contextual menu. In the sidebar of the options sheet that follows, select “Cocoa Touch,” then “Objective-C class.”

<img loading="lazy" decoding="async" class="121242" title="New Objective-C Class" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2173d6e8-88bb-43d5-9d59-d6af12dba8a5/new-objective-c-class.png" alt="New Objective-C Class" width="550" height="300" />

Click “Next.” Then, in the sheet that follows, enter “HomeViewController” in the “Class” field, select “UIViewController” in the “Subclass of” drop-down menu, and ensure that the “With XIB for user interface” box is checked.

<img loading="lazy" decoding="async" class="116808" title="Naming New View Controller" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/da58a286-4698-4f5a-b8af-21ed8ab4d31a/11-naming-new-view-controller.jpg" alt="Naming New View Controller" width="550" height="155" />

Clicking “Next” will give you a save dialogue box. Select the “Begin Here &gt; Portfolio” folder, and then hit “Create.”

Repeat this process for the other two views, naming each class “PortfolioViewController” and “ContactViewController,” respectively.

You can rearrange the order of the files in the navigator by dragging and dropping if you want. It should now look something like this:

<img loading="lazy" decoding="async" class="116809" title="View Controllers Added To Project Navigator" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/893a06ea-b39d-432f-aae4-152a8a2a714c/12-view-controllers-added-to-navigator1.jpg" alt="View Controllers Added To Project Navigator" width="259" height="320" />

### Configuring Tabs and Views

Return to <code>MainWindow.xib</code>. Select the first View Controller icon in the dock, then the Identity inspector. Select “HomeViewController” from the “Class” drop-down menu.

<img loading="lazy" decoding="async" class="116810" title="Connecting HomeViewController Class" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02605daf-9850-4200-9c9b-1f92ca444aed/13-connecting-home-viewcontroller1.jpg" alt="Connecting HomeViewController Class" width="259" height="177" />

Now go to the Attributes inspector. Type “Home” in the “Title” field, and select “HomeViewController” as the NIB name.

<img loading="lazy" decoding="async" class="116811" title="Connecting HomeViewController XIB" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bf45273-462b-42c8-9aec-6864357ce540/14-connecting-homeviewcontroller-xib.jpg" alt="Connecting HomeViewController XIB" width="259" height="144" />

Expand the View Controller in the dock and select its “Tab Bar Item.” In the Attributes inspector, set the title as “Home,” and select <code>tab-icon-home.png</code> from the Image drop-down menu. You don’t need to specify the <code>@2x</code> Retina version when selecting images in Xcode because they are called automatically when the application is running.

<img loading="lazy" decoding="async" class="116812" title="Customizing Tab Name And Icon" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/72b6d5b5-f7b3-4610-a92f-1ff7a00065d9/15-customise-tab-name-and-icon.jpg" alt="Customizing Tab Name And Icon" width="259" height="201" />

Repeat the above process for the Portfolio and Contact views, choosing the relevant classes, titles and image files.

The color of the tab bar highlight can be changed by selecting the main “Tab Bar” object in the dock, then “Image Tint” in the Attributes inspector. Although custom tints will only show up in devices running iOS 5 or higher, iOS 4 and below will safely fall back to showing a default blue highlight color.

Our views within tabs are now all set up! To check that they are working properly, we’ll need to add some dummy content to each view.

Select <code>HomeViewController.xib</code> in the navigator, then drag a “Label” from the library (at the top of the list) onto the view represented in the canvas. Double-clicking on the label in the canvas will allow you to edit its text. Change it to “Home.”

<img loading="lazy" decoding="async" class="116813" title="Adding A Label To The Home View" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/210b34c2-84f7-4e29-8e8f-e3ebe71dafde/16-adding-label-to-home-view1.jpg" alt="Adding A Label To The Home View" width="380" height="129" />

Repeat this for <code>PortfolioViewController.xib</code> and <code>ContactViewController.xib</code>, naming the labels appropriately.

Now hit the “Run” button, and check out your already functioning tabbed app in the simulator!

<img loading="lazy" decoding="async" class="117032" title="App Test With Labels" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5244d238-655a-42dc-93d1-e296c2376a91/17-app-test-with-labels-2.jpg" alt="App Test With Labels" width="257" height="500" />

## Adding Graphics And Text To The Views

As with desktop publishing applications, inserting images and text in Interface Builder requires you to make a containing element first. These can be dragged onto the canvas from the library, and they are called “Image View” and “Text View,” respectively. They can be repositioned and resized visually with the cursor, or you can type pixel measurements into the Size inspector for more precise control.

The Attributes inspector allows us to specify an image to place in the Image view. We may only choose from images that have been imported into the project.

The Attributes inspector also lets us set text for the Text view, and it gives us typography controls, a background color-picker and scrollbar options.

Arrange the graphics for <code>HomeViewController.xib</code>. Delete the label, and drag on an Image view from the library, setting its image’s name to <code>home-bg.png</code> and its mode to “Top Left” using the Attributes inspector.

<img loading="lazy" decoding="async" class="121240" title="Attributes Inspector Select Image" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3af59d64-397c-41cb-8750-add85b6f9948/attributes-select-image.png" alt="Attributes Inspector Select Image" width="259" height="159" />

In the Size inspector, check that the Image view has an X value of 16<code>0</code>, a Y value of <code>220</code>, a width of <code>320</code> and a height of <code>480</code>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d56bc449-104c-4e03-bac0-9dd77d0db9ed/screen-shot-2013-05-16-at-22.26"><img loading="lazy" decoding="async" class="136182" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d56bc449-104c-4e03-bac0-9dd77d0db9ed/screen-shot-2013-05-16-at-22.26" alt="Image View Size Inspector" width="255" height="267" /></a>

Now bring in Image Views for logo.png and twitterbox.png. Resize and position them appropriately.

Next, position a Text view over top. Edit it's content, center-align the text, set the text’s color to white, set a custom font (Snell Roundhand, Regular, 24 pixels), and set the background color to “Clear.”

<img loading="lazy" decoding="async" class="121239" title="Attributes Inspector Text View Controls" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2876e3e-02dc-4c9b-87c4-e43ee9e4ce34/attributes-inspector-text-view-controls.png" alt="Attributes Inspector Text View Controls" width="259" height="159" />

The result should look like this:

<img loading="lazy" decoding="async" class="116815" title="Adding Graphics To Home" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d1f2f3f-b8dc-45c4-909d-931db7ba4dfb/18-adding-graphics-to-home.jpg" alt="Adding Graphics To Home" width="346" height="500" />

Because our views are being placed inside a tab bar interface, we also need to simulate the black strip at the bottom of each view so that we can arrange items with this in mind. To do this, select the main “View” object in the dock. Then, in the Attribute inspector, under “Simulated Metrics,” choose “Tab Bar” from the “Bottom Bar” drop-down menu:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55d4300c-0731-4ee9-aecf-a3604c39250c/tab-bar-metric1.png"><img loading="lazy" decoding="async" class="136185" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/55d4300c-0731-4ee9-aecf-a3604c39250c/tab-bar-metric1.png" alt="tab-bar-metric" width="258" height="226" /></a>

This won’t actually add a tab bar to our view. It simply provides a visual reference to help us position the layout.

Another useful option under simulated metrics is "Size". At the moment the dimensions of our views are that of the 3.5 inch iPhone 4 or below. To switch the views to the 4 inch iPhone 5 dimensions, select "Retina 4 Full Screen" from the "Size" drop-down:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9d95c5b-86b5-43c7-ba26-0685a46d2c02/4-inch-screen-metric1.png"><img loading="lazy" decoding="async" class="136186" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d9d95c5b-86b5-43c7-ba26-0685a46d2c02/4-inch-screen-metric1.png" alt="4-inch-screen-metric" width="258" height="154" /></a>

Now, have a go at arranging the graphics and text for the Portfolio and Contact views. Either use the sample images at the top of this article, or refer to the source PSD provided in the template package.

When creating the thumbnail images in the Portfolio view and the social media buttons in the Contact view, <strong>use the “Round Rect Buttons” from the library instead of Image views</strong>. If you set the button type to “Custom” in the Attributes inspector, you can then set the button’s image in the same way as you would for an Image view. Set the button size in the Size inspector based on the image’s original dimensions. Using a “Round Rect Button” instead of an Image view allows us to add interactivity to them later.

Now, build and run to check that everything works OK in the simulator.</p>

## Extra Finesse

If you press the simulator’s home button, you will notice that your app has an uninspiring white icon on the springboard and a blank screen when it relaunches. Let’s fix that now.

Clicking on the blue “Portfolio” project icon in the navigator will take you back to the summary screen. Scrolling to the bottom of this screen will reveal empty wells awaiting custom images. Adding images is simply a case of dragging them from the Finder to the relevant well.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45d6bab5-3de4-43da-b8b3-a58fe6f5ae3a/20-app-icon-launch-image-wells3.jpg"><img loading="lazy" decoding="async" class="119124" title="App Icon And Launch Image Wells" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/45d6bab5-3de4-43da-b8b3-a58fe6f5ae3a/20-app-icon-launch-image-wells3.jpg" alt="App Icon And Launch Image Wells" width="550" height="500" /></a>

You will find the images you need for this project in the “App Icons” directory in the downloaded package.

If you want to make your own app icon, the images need to conform to the following sizes:

*   Standard: 57 × 57 pixels
*   Retina Display: 114 × 114 pixels

The launch images need to be the same as the display’s overall dimensions:

*   Standard: 320 × 480 pixels
*   Retina (3.5 inch): 640 × 960 pixels
*   Retina (4 inch): 640 x 1136 pixels

You will at a later date need some more sizes to display your app correctly in various contexts. An excellent resource detailing the required sizes has been <a href="https://mrgan.tumblr.com/post/708404794/ios-app-icon-sizes">produced by Neven Mrgan</a>. Apple’s “iOS Human Interface Guidelines” also give a <a href="https://developer.apple.com/library/ios/#DOCUMENTATION/UserExperience/Conceptual/MobileHIG/IconsImages/IconsImages.html">good breakdown</a> and include icon and launch image sizes for the new iPad.

iOS automatically rounds the corners of your app’s icon and overlays the standard glossy sheen on it, too, so you don’t need to include these elements in your design.

If, however, you want to create your own non-standard glossy effect or you don’t want gloss on your icon at all, then check the “Prerendered” box to the right of the App Icon wells.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f35b0db3-5c34-4223-8873-c9699ae4d955/23-icon-gloss-eg2.png"><img loading="lazy" decoding="async" class="119123" title="Icon Prerendered Example" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f35b0db3-5c34-4223-8873-c9699ae4d955/23-icon-gloss-eg2.png" alt="Icon Prerendered Example" width="550" height="145" /></a>

To change the name that appears below the icon, select the “Info” tab next to the “Summary” tab at the top of the editor. This will reveal an editor for the app’s <code>.plist</code> (property list) file, which is an XML document containing the main settings for your app:

<img loading="lazy" decoding="async" class="116818" title="App Info Plist" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/417edce1-a9e0-4d71-9594-57edd45744a3/21-info-plist.jpg" alt="App Info Plist" width="550" height="299" />

Some of the information here, such as “Main nib file base name,” points to resources required by the app when it first launches. Other information, such as “Bundle Identifier,” is used in the black art of provisioning and uploading to iTunes Connect for distribution on the App Store.

To change the name below the icon, change the “Bundle display name” value from <code>${PRODUCT_NAME}</code> to whatever you want.</p>

## The Minor Miracles Of The Xcode Assistant Editor

When we test our app, the custom buttons will respond to being tapped but won’t actually do anything. To make them work, we’ll need to write some code. Luckily, something called the Assistant Editor can help us with the first part of this process.

Select <code>ContactViewController.xib</code> from the navigator. Then, press the “Assistant Editor“ button in the top right of the Xcode window.

<img loading="lazy" decoding="async" class="116821" title="Assistant Editor Toggle" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4554eebf-ae56-4748-807d-bff8eb56e82c/24-assistant-editor-toggle.jpg" alt="Assistant Editor Toggle" width="260" height="97" />

This will display an Interface Builder window detailing <code>ContactViewController.xib</code>, alongside a Code Editor window, which shows the associated <code>ContactViewController.h</code> interface document. In the example below, the dock has been minimized, and the Utility area hidden to give the two editors more room. The Code Editor is also using the “Dusk” theme, which can be found under “Fonts and Colors” in <code>Xcode → Preferences</code>.

<img loading="lazy" decoding="async" class="116822" title="The Assistant Editor In Action" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79422240-9504-4d02-921a-026cb3c274ee/25-assistant-editor-in-action.jpg" alt="The Assistant Editor In Action" width="550" height="329" />

### Miracle 1: Declaring Properties and Methods

Features of a class generally fall into two main types: a “property,” which is a characteristic that the class might possess, and a “method,” which is something that it can do. When adding a button to ContactViewController, we need to declare the button as a property of the class and create a method for what happens when the button is tapped by the user.

The <code>.h</code> document should contain the following code:

<pre><code class="language-markup tmp-xml">#import &lt;UIKit/UIKit.h&gt;
@interface ContactViewController : UIViewController
@end</code></pre>

The <code>#import</code> statement at the top gives the class access to the required iOS user interface classes stored within the UIKit framework.

The <code>@interface</code> declaration starts by defining ContactViewController and stating that it is a subclass (meaning that it inherits all the features) of the UIViewController class, which is defined within UIKit.

We can add in extra items between the opening <code>@interface</code> declaration and its <code>@end</code>, to build on the foundation provided by the UIViewController class.

To do this, Control-click on our orange “WWW” button on the canvas in Interface Builder, drag the cursor to be just above <code>@end</code> in the code editor, and then release. A little dialogue box will pop up with some settings:

<img loading="lazy" decoding="async" class="116823" title="Outlet Dialogue" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d274e592-cf4e-43d2-a9e3-87486f6805f0/26-outlet-dialogue.jpg" alt="Outlet Dialogue" width="550" height="154" />

Check that the “Connection” is set to “Outlet,” type in the name <code>websiteButton</code>, and then press “Connect.” Xcode will insert a line of code into the <code>.h</code> document for you.

Repeat the process, this time changing “Connection” to “Action” and providing the name <code>openWebsite</code>.

<img loading="lazy" decoding="async" class="116824" title="Action Dialogue" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c18dcbf-5172-4084-82bf-7a9d381cc6f0/27-action-dialogue.jpg" alt="Action Dialogue" width="550" height="200" />

The code in your <code>.h</code> document should now look like this:

<pre><code class="language-markup tmp-xml">#import &lt;UIKit/UIKit.h&gt;
@interface ContactViewController : UIViewController
@property (retain, nonatomic) IBOutlet UIButton *websiteButton;
- (IBAction) openWebsite:(id)sender;
@end</code></pre>

So, what does this all mean?

The <code>@property</code> declaration states that the ContactViewController class has a property. It begins with some parameters: <code>retain</code>, which has to do with memory management (more on this later), and <code>nonatomic</code>, which means that it is not “multithreaded,” something that is common to all iOS properties. Next, there is a definition for the property return type, <code>IBOutlet</code>, which allows us to bind our code to the button we created in Interface Builder. <code>UIButton</code> states that the property will inherit from the UIButton class, defined within UIKit, and then the name of our property is given, which is <code>websiteButton</code>.

The second line of code is a method declaration. It starts by saying that it is an <code>IBAction</code>, which again lets us bind the code to the button object in the XIB. Then it is given a name, in this case, <code>openWebsite</code>. The <code>(id)sender</code> parameter allows us to find out which object called the method. This is handy in certain situations, although we don’t need it right now.

You might have noticed that when we created our View Controller classes, their names began with an uppercase letter, whereas the names we gave our property and method didn’t. This is an Objective-C naming convention and should be adhered to.

Hand-coding those two lines is possible, but using the Assistant Editor to do it saves a bit of time and ensures that the syntax is correct. It also performs a whole series of other tasks for us as well. Let’s look at what else it does.</p>

### Miracle 2: Method Generation and Memory Management

Return to “Standard Editor” mode, and select <code>ContactViewController.m</code>. Near the bottom, we will find the following line of code that the Assistant Editor has created:

<pre><code class="language-markup tmp-xml">- (IBAction)openWebsite:(id)sender {
}</code></pre>

This is the method implementation for our button action. In a minute, we will put some code in there to make our button work.

You should also find another method implementation that looks like this:

<pre><code class="language-markup tmp-xml">- (void) dealloc {
[_websiteButton release];
[super dealloc];
}</code></pre>

This method has to do with memory management and is defined within the Cocoa framework, which is why we haven’t needed to mention it in our interface.

Managing memory is very important when programming because a mobile device doesn’t have much to play with. When the <code>websiteButton</code> property is defined, a chunk of memory is allocated to it using the <code>retain</code> command. This command asks iOS to reserve a bit of memory for the button until we tell it to let it go. The <code>dealloc</code> method is activated only when the View instance is destroyed; so, by putting <code>websiteButton release</code> in there, we are asking iOS to free up the memory set aside for the button when this event occurs. If we don’t do this, then the memory keeps getting allocated, even when the button object isn’t in use anymore. This is called a “memory leak.” If left unchecked, these leaks will add up, affecting the app’s responsiveness and the device’s battery life and causing all sorts of other misdemeanors.

Thankfully, once again, the assistant editor has set this all up for us, so we don’t need to remember to do it.

It is probably worth mentioning that version 5+ of the iOS SDK comes with something called “Automatic Reference Counting” (ARC), which seeks to further automate memory management for iOS developers. When creating a new project, you have the option to turn ARC on and off. We are not using ARC in this project, so we can learn a bit about how memory management works. Integrating freely available components found on the Internet (many of which are written using manual reference counting) with an ARC-enabled project can also be difficult. With each subsequent release of the SDK, however, Apple is pushing more and more for developers to embrace ARC, and there are many advantages in doing so. <a href="https://maniacdev.com/ios-5-sdk-tutorial-and-guide/arc-automatic-reference-counting/">ManiacDev has compiled some useful resources</a> to make this transition smoother.</p>

### Miracle 3: Code Binding

The Assistant Editor has also connected our code to the button object in the XIB. Select <code>ContactViewController.xib</code>, expand the dock, and under “Placeholders” select “File’s Owner.” This represents the ContactViewController class. Now, select the Connections inspector. It should look like this:

<img loading="lazy" decoding="async" class="116825" title="Connections Inspector" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87a49371-02fc-4a46-9173-26e249b65795/28-connections-inspector.jpg" alt="Connections Inspector" width="258" height="214" />

Under “Outlets,” we can see the <code>websiteButton</code> property linked to the Button XIB object.

Under “Received Actions,” we can see that the <code>openWebsite</code> method is also connected to the Button.

Under it, there is also an associated event, “Touch Up Inside.” This means that the method will be called when the user touches and then releases their finger while still inside the button. This is the default touch event.</p>

## Handwriting Your First Bit Of Objective-C

Lets make that button do something!

Change the <code>openWebsite</code> method implementation in <code>ContactViewController.m</code> so that it looks like the following:

<pre><code class="language-markup tmp-xml">- (IBAction)openWebsite:(id)sender {
NSURL *webAddress = [NSURL URLWithString:@"http:www.mightymeta.co.uk"];
[[UIApplication sharedApplication] openURL:webAddress];
}</code></pre>

The syntax for a method is fairly straightforward. Simply provide the name of the method, and then put what you want to happen when the method is called between the pair of curly braces.

In this case, we are doing two things. First, we are creating a temporary variable named <code>webAddress</code> and assigning it a string of text that contains our email URL.

It is worth noting that this is something called a “convenience method.” It creates an instance of the NSURL class and automatically allocates some memory to it. It also sorts out the memory deallocation for you, so you don’t have to worry about releasing the <code>webAddress</code> variable.

The second line asks the OS to open the URL in a relevant application, which in this case would be the default Web browser.

Build and run to test whether it works.

To make the other buttons work, simply repeat the steps that we went through to create this button. Any <code>mailto:</code> URLs will work and will launch the default mail client. To make a phone call, put <code>tel:</code>, followed by the number you want to dial in place of the URL. You can change the name of the temporary variable to suit the purpose for each button.</p>

## Making a View Appear Modally

The portfolio section currently has some thumbnail images. Wouldn’t it be great if the user could tap on these to get bigger versions?

This can be achieved by creating what is called a “Modal View.” This is essentially a new view that is placed over top the previous one, and it comes with a range of animated transitions.</p>

### Create the Modal View

Modals are easy to create. First, generate a new class called <code>BigImageViewController</code> (Control-click on the “Portfolio” folder in the project navigator, then select “New File” and go through the options, like before).

Open the corresponding XIB in Interface Builder, add an Image view that fills the entire view, and set its image as <code>portfolio-modal-bg.png.</code> Add a custom Round Rect button, give it a background of <code>button-close.png</code>, set the color of the “Close” title to white, and place it in the top-left corner.

Next, place another image view over top the first. Fit it to near the edges of the paper background, but don’t assign an image to it:

<img loading="lazy" decoding="async" class="116826" title="Creating A Modal View" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f027bb4-6673-4acd-8184-833d3c94c7da/29-creating-modal1.jpg" alt="Creating A Modal View" width="352" height="500" />

Use the Assistant Editor to declare the empty Image view as an outlet named <code>imageFrame</code>, and connect the button to an action named <code>closeView</code> in <code>BigImageViewController.h</code> (you can select which file the right-hand window will display from the bar at its top):

<pre><code class="language-markup tmp-xml">@property (retain, nonatomic) IBOutlet UIImageView *imageFrame;
- (IBAction)closeView:(id)sender;</code></pre>

Then type the following into the <code>closeView</code> method in <code>BigImageViewController.m</code>:

<pre><code class="language-markup tmp-xml">- (IBAction)closeView:(id)sender {
[self dismissModalViewControllerAnimated:YES];
}</code></pre>

This code will close the modal view when the button is tapped.</p>

### Code for Launching the Modal

Now, using the Standard Editor, type in <code>PortfolioViewController.h</code> so that it looks like the following example:

<pre><code class="language-markup tmp-xml">#import &lt;UIKit/UIKit.h&gt;
#import "BigImageViewController.h"
@interface PortfolioViewController : UIViewController
@property (nonatomic, retain) UIImage *bigImage;
- (IBAction) selectImage1;
- (void) openBigImageView;
@end</code></pre>

Make sure to include the <code>#import</code> statement for the <code>BigImageViewController</code> header file. This is required so that we can send a message to this class and ask it to create an instance of itself.

A property and two method declarations are there. The second, <code>openBigImage</code>, doesn’t need to be connected to any objects in the XIB; so, it has a return type of <code>(void)</code>, meaning… well, a big black hole of nothingness.

We haven’t used the Assistant Editor here because we are doing something a little different from before. Because of this, we need to manually release the <code>bigImage</code> property at the start of <code>PortfolioView.m</code>, like so:

<pre><code class="language-markup tmp-xml">- (void) dealloc {
[_bigImage release];
[super dealloc];
}</code></pre>

Underneath the <code>dealloc</code> method, implement the two methods that we declared in the header:

<pre><code class="language-markup tmp-xml">- (IBAction) selectImage1 {
self.bigImage = [UIImage imageNamed: @"image1-big.png"];
[self openBigImageView];
}
- (void) openBigImageView {
BigImageViewController *bigImageView = [[[BigImageViewController alloc] initWithNibName:@"BigImageViewController" bundle:nil] autorelease];
bigImageView.modalTransitionStyle = UIModalTransitionStyleFlipHorizontal;
[self presentModalViewController:bigImageView animated:YES];
[bigImageView.imageFrame setImage:self.bigImage];
}</code></pre>

Wow, that’s a lot to take in. Lets go through it.

The <code>selectImage1</code> method sets the <code>bigImage</code> property to the image file that we want to use, and then calls the <code>openBigImageView</code> method.

The <code>openBigImageView</code> creates an instance of the <code>BigImageViewController</code> class named <code>bigImageView</code>, presents it as a modal using the “flip” transition style, and then sends its <code>imageFrame</code> the image file held by the <code>bigImage</code> property.

Because we have manually allocated memory to the instance of <code>BigImageViewController</code>, we need to release it at some point, but we don’t know how long the object will be needed for because it depends on how long the user keeps the modal active. The <code>autorelease</code> command helps us with this problem because it asks iOS to hold on to the memory for a bit and then release it later on, when it is deemed safe to do so.</p>

### Manual Code Binding

Now we need to connect our code to the objects in the XIB. Select <code>PortfolioViewController.xib</code>, and then the “File’s Owner” object in the dock, and then the Connections inspector.

Under “Received Actions,” you will find the <code>selectImage1</code> method, and an empty circle to the right of it. Click and drag a connection from this circle over to the relevant thumbnail button:

<img loading="lazy" decoding="async" class="116827" title="Binding A Button To Code Manually" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cfaeed00-0271-44bf-9685-7ee57e56f37b/30-binding-button.jpg" alt="Binding A Button To Code Manually" width="550" height="297" />

Select “Touch Up Inside” from the list of button events that appears.

Build and run to see whether it works. If everything is in place, you should be able to tap the thumbnail to reveal the bigger image.

See if you can work out how to do the same for the other images on the portfolio page. You will need to create <code>selectImage2</code>, <code>selectImage3</code> and <code>selectImage4</code> methods, but you won’t need another <code>openBigImage</code>. You could also try using different transition styles; you have four to choose from:

*   `UIModalTransitionStyleCoverVertical`
*   `UIModalTransitionStyleCrossDissolve`
*   `UIModalTransitionStyleFlipHorizontal`
*   `UIModalTransitionStylePartialCurl`

If you get really stuck, have a look at the completed project in the “End Result” folder of your downloaded template package.</p>

## In Conclusion

We’ve covered quite a lot of ground, having looked at the basics of the Xcode interface and how to arrange visual elements in Interface Builder. We’ve also been introduced to the key concepts of classes, properties, methods and memory management in Objective-C.

In the process, we have built a functioning, albeit limited, app. Making it ready for submission to the App Store would require a unique design and some additional functionality, such as adding Tweets to that empty speech bubble on the home page. Now that you have a grasp of the basics, take advantage of the great resources out there to help you with this next step.</p>

## Further Reading And Resources

### App Design

*   “iOS Human Interface Guidelines Part 1: Platform Characteristics,” Dinosaurs with Laserz A summary of the “iOS Human Interface Guidelines.”
*   [Pttrns](https://pttrns.com/) App design screenshots to inspire your next masterpiece.</p>

### App Development

*   “[Learn Objective-C](https://cocoadevcentral.com/d/learn_objectivec/),” Cocoa Dev Central A summary of the basics of Objective-C.
*   [Cocoa Controls](https://cocoacontrols.com/) Open-source UI components, such as carousels, maps and Twitter aggregators, to integrate in your project.
*   [ManiacDev.com](https://maniacdev.com/) iOS libraries, controls, tutorials, examples and tools, many of which are open source.
*   [Baker Ebook Framework](https://bakerframework.com/) and [PugPig](https://pugpig.com/) These enable you to build an interactive book or magazine using HTML5 and then wrap it into an app using Xcode.
*   [Creator](https://gamesalad.com/creator), GameSalad Want to make a promotional iPhone game using drag-and-drop behaviors and your new-found Xcode skills? Then GameSalad’s Creator is for you.

{{< signature "al" >}}


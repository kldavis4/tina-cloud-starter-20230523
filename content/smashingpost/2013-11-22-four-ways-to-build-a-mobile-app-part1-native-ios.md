---
title: 'Four Ways To Build A Mobile Application, Part 1: Native iOS'
slug: four-ways-to-build-a-mobile-app-part1-native-ios
image: >-
  https://www.smashingmagazine.com/general/2013/08/14/137316-revision-44/attachment/fastip-app-screens/
date: 2013-11-22T13:28:12.000Z
author: peter-traeg
description: >-
  The mobile application development landscape is filled with many ways to build
  a mobile app. Among the most popular are: **native iOS**, **native Android**,
  **PhoneGap** and **Appcelerator Titanium**.
categories:
  - Mobile
  - Apps
  - iOS
  - iPhone
  - Native
---
The mobile application development landscape is filled with many ways to build a mobile app. Among the most popular are:

*   native iOS,
*   [native Android](https://www.smashingmagazine.com/2014/01/four-ways-to-build-a-mobile-app-part2-native-android/),
*   [PhoneGap](https://www.smashingmagazine.com/2014/02/four-ways-to-build-a-mobile-app-part3-phonegap/),
*   [Appcelerator Titanium](https://www.smashingmagazine.com/2014/03/4-ways-build-mobile-application-part4-appcelerator-titanium/).

This article marks the start of a series of four articles covering the technologies above. The series will provide an overview of how to build a simple mobile application using each of these four approaches. Because few developers have had the opportunity to develop for mobile using a variety of tools, this series is intended to broaden your scope.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Providing A Native Experience With Web Technologies](https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/)
*   [A Beginner’s Guide To Progressive Web Apps](https://www.smashingmagazine.com/2016/08/a-beginners-guide-to-progressive-web-apps/)

{{% feature-panel %}}

Hopefully, armed with this knowledge, you will be in a better position to choose the right development tools for your mobile application’s needs. In this first article in the series, <strong>we’ll start with some background and then dig into iOS</strong>.

I’ve built the same simple application with each technology to demonstrate the basic concepts of development and the differences between the platforms and development tools. The purpose of this series is not to convert you to a particular technology, but rather to provide some insight into how applications are created with these various tools, highlighting some of the common terms and concepts in each environment.

FasTip is a simple application to calculate tips. Because this is a simple example, it uses the standard UI controls of each platform:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5031c55b-86c7-4e07-8d2a-f280ff5f9089/fastip-app-screens-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/50421a25-01e2-40d4-8f2e-384046c2230d/fastip-app-screens-500-opt.png" alt="fastip-app-screens-500" width="500" height="269" /></a></figure>

The screenshots above show the application running as <strong>native iOS</strong>, <strong>PhoneGap</strong> and <strong>native Android</strong> applications. Appcelerator Titanium uses native controls, so it looks the same as the native iOS and Android applications. Our application has two screens: a main screen where the tips are calculated, and a settings screen that enables the user to set a tip percentage. To keep things simple and straightforward, we’ll use the default styles of each environment.

The source code for each app is <a href="https://github.com/ptraeg/mobile-apps-4-ways">available on GitHub</a>.</p>

## Native iOS Development

Most applications in Apple’s App Store are written in the Objective-C programming language, and <strong>developers typically use Xcode</strong> to develop their applications.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ae1d147-faf1-41f7-8bdf-fdd8b2bff7de/xcode-screen-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03420713-346a-44a3-ae33-83d6559ac455/xcode-screen-500-opt.png" alt="xcode-screen-500" width="500" height="377" /></a></figure>

### Obtaining the Tools

To build an iOS app, <strong>you must use Mac OS X</strong>; other operating systems are not supported. The development tools that you’ll need, iOS 7 SDK and Xcode 5, are free of charge, and you can run the app that you build in the iOS simulator, which is part of the iOS SDK. To run your app on a real device and make it available in Apple’s App Store, you must pay $99 per year.

*   “About Xcode,” iOS Developer Library, Apple
*   “[iOS Dev Center](https://developer.apple.com/devcenter/ios/index.action),” Apple
*   “[iOS Developer Program](https://developer.apple.com/programs/ios/),” Apple

### Creating a New Project

Once you have installed Xcode, you’ll want to create a new project. Choose “Create a new Xcode project” from the welcome screen or via <code>File → New Project</code> in the menu.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/30f945df-78ef-4b09-99b7-76df793ad839/xcode-new-project-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ab604fb-4d00-45f4-a1f9-efe8621d111b/xcode-new-project-500-opt.png" alt="xcode-new-project-500" width="500" height="340" /></a></figure>

For a simple application such as this one, “Single View” is appropriate. Upon clicking “Next,” you will be presented with a dialog to enter some basic information about your application:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05e9a302-abc8-43d4-ac31-b92ef24595d0/new-project-options-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/54a94d87-8a8a-4293-a0cd-421e8f268e4c/new-project-options-500-opt.png" alt="new-project-options-500" width="500" height="339" /></a></figure>

The value that you enter in the “<a href="https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingBasics.html#//apple_ref/doc/uid/20001281-1002226-BBCJECED">Class Prefix</a>” option tells Xcode to attach that unique prefix to every class that you generate with Xcode. Because Objective-C does not support “namespacing,” as found in Java, attaching a unique prefix to your classes will avoid naming conflicts. The “Devices” setting lets you restrict your application to run only on an iPhone or an iPad; the “universal” option will enable the application to run on both.</p>

### Navigation Controllers and View Controllers

The screen functionality of iOS applications is grouped into what are known as <a href="https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewControllerCatalog/Introduction.html#//apple_ref/doc/uid/TP40011313">view controllers</a>. Our application will have two view controllers: one for the main screen and one for the settings screen. A view controller contains the logic needed to interact with the controls on a screen. It also interacts with another component called the <a href="https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewControllerCatalog/Chapters/NavigationControllers.html#//apple_ref/doc/uid/TP40011313-CH2-SW1">navigation controller</a>, which in turn provides the mechanism for moving between view controllers. A navigation controller provides the <a href="https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewControllerCatalog/Chapters/NavigationControllers.html#//apple_ref/doc/uid/TP40011313-CH2-SW3">navigation bar</a>, which appears at the top of each screen. The view controllers are pushed onto a stack of views that are managed by the navigation controller as the user moves from screen to screen.</p>

### Storyboards: Building the User Experience Visually

Starting with iOS 5, Xcode has had storyboards, which enable developers to quickly lay out a series of view controllers and define the content for each. Here’s our sample application in a storyboard:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfb609ca-82a1-4d17-9a97-6088ebe733b7/storyboard-overview-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba3c118e-7c69-4949-9315-9573d43291dd/storyboard-overview-500-opt.png" alt="storyboard-overview-500" width="500" height="315" /></a></figure>

The container on the left represents the navigation controller, which enables the user to move from screen to screen. The two objects on the right represent the two screens, or view controllers, that make up our app. The arrow leading from the main screen to the settings screen is referred to as a segue, and it indicates the transition from screen to screen. A new segue is created by selecting the button in the originating view and then, while the <code>Control</code> key is pressed, dragging the mouse to the destination view controller. Apple’s documentation provides more detail about this process.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ad50616-ce17-4696-8de2-6c4c8cb3b8ff/storyboard-properties-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19e2eb56-d3b3-4a7e-9bfd-e4df11c6cd3f/storyboard-properties-500-opt.png" alt="storyboard-properties-500" width="500" height="397" /></a></figure>

In the example above, we can see that a text field has been selected, and the property panel is used to adjust the various attributes of the controls. When this application was created, <strong>the “universal” app option was selected, enabling the app to run on both an iPhone and iPad</strong>. As a result, two versions of the storyboard file have been created. When the app is running on an iPhone or iPod Touch, the <code>_iPhone</code> version of the file will be used, and the <code>_iPad</code> version will be used for iPads. This allows a different layout to be used for the iPad’s larger display. The view controller will automatically load the appropriate layout. Keep in mind that if your storyboards expose different sets of controls for the iPad and the iPhone, then you must account for this in the code for your view controller.

In addition to directly positioning items at particular coordinates on the screen, <strong>you can also use the Auto Layout system</strong> that was introduced in iOS 6. This enables you to define constraints in the relationships between controls in the view. The storyboard editor enables you to create and edit these constraints.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5b83fc81-edeb-4ae4-9b38-0b90433a2040/storyboard-constraints-large-opt.png"><img loading="lazy" decoding="async" class="139427" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b7102b8c-f489-42e5-808f-0214f904a44d/storyboard-constraints-500-opt.png" alt="storyboard-constraints-500" width="500" height="511" /></a></figure>

The constraints can also be manipulated programmatically. The Auto Layout mechanism is quite sophisticated and a bit daunting to use at first. Apple has an extensive guide on Auto Layout in its documentation.

## Associating Storyboards With Your Code

To access the storyboard objects from the code, you must define the relationships between them. Connecting items from the storyboard to your code via Xcode is not obvious if you’re used to other development environments. Before you can do this, you must first create a view controller to hold these associations. This can be done with the following steps:

1.  Choose `File → New File`.
2.  In the dialog that appears, choose “Objective-C class”: [![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b9c04fc-a81f-4f39-8caa-809c52485302/file-new-template-opt.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b9c04fc-a81f-4f39-8caa-809c52485302/file-new-template-opt.png)
3.  In the next dialog, give your class a name and ensure that it inherits from `UIViewController`: [![file-new-options-500](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76440811-baf2-409c-8fe7-be7935cceed7/file-new-options-500-opt.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e3dba568-bf5b-41e3-9615-e81b987ba5f0/file-new-options-large-opt.png)
4.  Upon clicking “Next,” you’ll be asked to confirm where in the project the file should be saved. For a simple project, picking the main directory of the app is fine.
5.  Upon clicking “Next,” you’ll see that a new set of files has been created for your view controller. Now, associate that newly created view controller with the view controller in your storyboard.
6.  With the storyboard open, click on the view controller. In the “Identity Inspector” panel, pick the “Class” that this view controller is to be associated with: [![class-picker](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27c7fb36-832d-40a9-949b-6c5c09e89272/class-picker-opt.png)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27c7fb36-832d-40a9-949b-6c5c09e89272/class-picker-opt.png)
7.  Once this process is completed, the code for your view controller will be properly referenced by the storyboard entry.

To reference the controls that you’ve dragged onto a storyboard from your Objective-C code, <strong>you’ll need to define these relationships</strong>. The storyboard editor has an “assistant editor” view to help with this. Basically, it’s a split-pane view that shows both the storyboard and your code. In this example, we’ll reference a button that’s already been placed on the storyboard:
<ol>
 	<li>First, ensure that you’ve completed the steps above to associate the view controller class with the corresponding view controller in the storyboard.</li>
 	<li>Choose the assistant editor by clicking the icon that looks like this:
<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8be00757-e328-4f67-a6a9-9bdf17016cfb/assistant-editor-icon-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8be00757-e328-4f67-a6a9-9bdf17016cfb/assistant-editor-icon-opt.png" alt="assistant-editor-icon" width="110" height="47" /></a></figure></li>
 	<li>A split-pane view will open, with the storyboard on the left and your view controller class on the right.</li>
 	<li>Select the button in your storyboard and, while holding down the <code>Control</code> key, drag from the button to the interface area of your code.
<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9c16ee4-9fba-40d0-b7df-9a4d4a584c2a/create-outlet-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14a0378b-2fac-4ab6-9161-6c2131d2ef0d/create-outlet-500-opt.png" alt="create-outlet-500" width="500" height="151" /></a></figure></li>
 	<li>The resulting dialog will enable you to create an “outlet” for the button in your code. Simply give the button a name, and click the “Connect” button in the dialog. You may now reference the button in the view controller from your code.</li>
 	<li>Let’s hook up a method to be invoked when a person taps on the button. Select the button again, and use the same <code>Control</code>-and-drag maneuver to drop a reference into the interface section of your view controller.</li>
 	<li>This time, in the dialog box that appears, we’ll associate an “action,” rather than an outlet. Choose “Action” from the “Connection” drop-down menu, and enter a name like this:
<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5901ab1-3f8b-4e31-a448-831c16fd81f4/create-action-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ebbc381-c2f4-4bf4-ad72-3f459df95db9/create-action-500-opt.png" alt="create-action-500" width="500" height="159" /></a></figure>For the “Event,” use the default of “Touch Up Inside,” and press the “Connect” button.</li>
 	<li>Note that your class now has an interface with two entries in it:</li>
</ol>

<pre><code class="language-clike">
@interface FTSettingsViewController ()
@property (weak, nonatomic) IBOutlet UIButton *myButton;
- (IBAction)tappedMyButton:(id)sender;
@end
</code></pre>

The <code>IBOutlet</code> item is used to identify anything that you’re referencing from the storyboard, and the <code>IBAction</code> is used to identify actions that come from the storyboard. Notice also that Xcode has an empty method where you can place the code to be run when the user taps on the control:

<pre><code class="language-clike">
- (IBAction)tappedMyButton:(id)sender {
}
</code></pre>

The process above does take some getting used to and could certainly be made more intuitive. After some practice, it will get less awkward. You might find it useful to bookmark the section of the Xcode documentation that describes how to “Connect User Interface Objects to Your Code.”

As we’ll see later, you can also add objects to the view and manipulate their properties programmatically. In fact, <strong>applications of even moderate complexity typically perform a lot of manipulation in code</strong>. For complex apps, some developers eschew the storyboard and use the code-based alternative almost entirely.</p>

### Getting Into the Code

For even the most basic of applications to function, some code must be written. So far in the storyboard, we’ve laid out our user interface and the interactions between the view controllers. But no code has been written to perform the calculations, to persist the settings of the tip percentage and so on. That is all done by you, the developer, in Objective-C.

When an application is running, its overall lifecycle is handled by something called an <strong>“application delegate.”</strong> Various methods in this delegate are called when key events in the application’s lifecycle occur. These events could be any of the following:

*   the application is started,
*   the application is moved to the background,
*   the application is brought to the foreground,
*   the application is about to be terminated,
*   a push notification arrives.

The events above are handled in a file called <code>AppDelegate</code>. For our sample application, the default handling of these events is just fine; we don’t need to take any special action. The documentation has an overview of the application’s lifecycle and of responding to changes in an app’s state.

The next area of attention is the view controller. Just as with the application delegate, the view controller has its own lifecycle. The view controller’s lifecycle includes methods that are invoked when the following happens:

*   the view controller has been loaded;
*   the view controller is about to appear or has appeared on the screen;
*   the view controller is about to disappear or has disappeared from the screen;
*   the bounds of the view have changed (for example, because the device has been rotated) and the view will be laid out again.

The main code for our application is in the <code>FTViewController.m</code> file. Here is <strong>the first bit of code that initializes our screen:</strong>

<pre><code class="language-clike">
- (void)viewWillAppear:(BOOL)animated
{
    // Restore any default tip percentage if available
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    float tipPercentage = [defaults floatForKey:@"tipPercentage"];
    if (tipPercentage &gt; 0) {
        _tipPercentage = tipPercentage;
    } else {
        _tipPercentage = 15.0;
    }
    self.tipAmountLabel.text = [NSString stringWithFormat:@"%0.2f%%", _tipPercentage];
}
</code></pre>

In this application, we want to use whatever tip percentage value was stored in the past. To do this, we can use <a href="https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/UserDefaults/AccessingPreferenceValues/AccessingPreferenceValues.html#//apple_ref/doc/uid/10000059i-CH3-SW1">NSUserDefaults</a>, which is a persistent data store to hold settings and preferences for an application. Keep in mind that <strong>these values are not encrypted in any way</strong>, so this is not the best place to store sensitive data, such as passwords. A KeyChain API is provided in the iOS SDK to store such data. In the code above, we’re attempting to retrieve the <code>tipPercentage</code> setting. If that’s not found, we’ll just default to 15%.

When the user taps the “Calculate Tip” button, the following code is run:

<pre><code class="language-clike">
- (IBAction)didTapCalculate:(id)sender {
    float checkAmount, tipAmount, totalAmount;

    if (self.checkAmountTextField.text.length &gt; 0) {

        checkAmount = [self.checkAmountTextField.text floatValue];
        tipAmount = checkAmount * (_tipPercentage / 100);
        totalAmount = checkAmount + tipAmount;

        self.tipAmountLabel.text = [NSString stringWithFormat:@"$%0.2f", tipAmount];
        self.totalAmountLabel.text = [NSString stringWithFormat:@"$%0.2f", totalAmount];

    }

    [self.checkAmountTextField resignFirstResponder];

}
</code></pre>

We’re simply reading the value that the user has inputted in the “Amount” field and then calculating the tip’s value. Note how the <code>stringWithFormat</code> method is used to display the <code>tipAmount</code> value as a currency value.

When the user taps the “Settings” button in the navigation controller, the segue that we established in the storyboard will push the settings’ view controller onto the stack. A separate view controller file, <code>FTSettingsViewController</code>, will now handle the interactions on this screen. Pressing the “Done” button on this screen will run the following code:

<pre><code class="language-clike">
- (IBAction)didTapDone:(id)sender {

    float tipPercentage;
    tipPercentage = [self.tipPercentageTextField.text floatValue];

    if (tipPercentage &gt; 0) {

        NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
        [defaults setFloat:tipPercentage forKey:@"tipPercentage"];
        [defaults synchronize];

        [[self navigationController] popViewControllerAnimated:YES];

    } else {

        [[[UIAlertView alloc] initWithTitle:@"Invalid input"
                                    message:@"Percentage must be a decimal value"
                                   delegate:nil
                          cancelButtonTitle:@"ok"
                          otherButtonTitles:nil] show];

    }

}
</code></pre>

Here we’re retrieving the value from the text field and making sure that the inputted value is greater than 0. If it is, then we use <code>NSUserDefaults</code> to persist the setting. Calling the <code>synchronize</code> method is what will actually save the values to storage. After we’ve saved the value, we use the <code>popViewControllerAnimated</code> method on the navigation controller to remove the settings view and return to the prior screen. Note that if the user does not fill in the percentage correctly, then they will be shown the standard iOS <code>UIAlertView</code> dialog and will remain on the settings screen.

In the section above on view controllers and storyboards, I mentioned that the <strong>controls in a view can be manipulated programmatically</strong>. While that was not necessary for our application, the following is a snippet of code that creates a button and adds it to a particular location on the screen:

<pre><code class="language-clike">
CGRect buttonRect = CGRectMake(100, 75, 150, 80);
UIButton *myButton = [UIButton buttonWithType:UIButtonTypeRoundedRect];
myButton.frame = buttonRect;
[myButton setTitle:@"Click me!" forState:UIControlStateNormal];
[self.view addSubview:myButton];
</code></pre>

Generally speaking, all of the controls that you place in a view extend from an ancestor class named <code>UIView</code>. As such, buttons, labels, text-input fields and so on are all <code>UIViews</code>. One instance of a <code>UIView</code> is in the view controller. This can be referenced in your view controller’s code as <code>self.view</code>. <strong>The iOS SDK positions items in a view based on a frame</strong>, also referred to as <code>CGRect</code>, which is a structure that contains the x and y coordinates of the item, as well as the width and height of the object. Note in the code above that the button is instantiated and assigned a frame (location and size) and then added to the view controller’s view.</p>

### Running and Debugging an iOS Application

When Xcode and the iOS SDK are installed, so is the iOS simulator, which simulates an iOS device directly on your machine. Xcode has a drop-down menu that allows you to select different device configurations. Pressing the “Run” button in the upper-left corner will build the app and then run it in the chosen simulator.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/135b5893-5353-4d70-8568-4ef08f7c9204/device-chooser-large-opt.png"><img loading="lazy" decoding="async" class="139445" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bc9f0494-2665-43a1-a04e-6939730af0e7/device-chooser-500-opt.png" alt="device-chooser-500" width="500" height="175" /></a>

Using the menu above, you can switch between iPhones and iPads of different sizes, as well as between Retina and non-Retina versions of each device.

Debugging is done simply by clicking in the left margin of the code editor, where the line numbers appear. When the execution of your app reaches the breakpoint, the app will stop and the variable values in effect at that moment in time will appear below the code editor:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/83222aa3-fec3-462f-b85c-4af5a9fc6221/breakpoint-variables-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4acf7cb9-ec6a-4958-b979-c95cbe312957/breakpoint-variables-500-opt.png" alt="breakpoint-variables-500-opt" width="500" height="281" /></a></figure>

Some things, such as <strong>push notifications, cannot readily be tested in the simulator</strong>. For these things, you will need to test on a device, which requires you to register as an Apple developer for $99 a year. Once you have joined, you can plug in your device with a USB cable. Xcode will prompt you for your credentials and will offer to “provision” the device for you. Once the device is recognized, it will be shown in the same menu that allows you to switch between device simulators.

In Xcode, by going to <code>Window → Organizer</code> in the menu, you can display a tool that enables you to manage all of the devices visible in Xcode and to examine crash logs and more. The Organizer window also lets you take and export screenshots of your application.</p>

## Summary

Thus far, we’ve seen the basics of developing a simple native iOS application. Most applications are more complex than this, but these are the basic building blocks:

*   **Xcode**.  The development environment
*   **Storyboards**.  For laying out and configuring the user interface
*   **View controllers**.  Provide the basic logic for interacting with each of the views defined in the storyboards
*   **Navigation controllers**.  Enable the user to navigate between the different views

### Learning Resources

To get started with iOS development, you might want to consult these useful resources:

*   [_iOS Programming: The Big Nerd Ranch Guide_](https://www.amazon.com/iOS-Programming-Edition-Guides-ebook/dp/B007OWBAB0/ref=tmm_kin_title_0?ie=UTF8&qid=1365887748&sr=8-1), Joe Conway and Aaron Hillegass This book is excellent. It guides you through both Objective-C and iOS development and will hold your interest with some nice functional examples.
*   [_Objective-C Programming: The Big Nerd Ranch Guide_](https://www.amazon.com/Objective-C-Programming-Ranch-Guide-Guides/dp/0321706285/ref=pd_bxgy_b_text_y), Aaron Hillegass This book provides more detailed information about Objective-C, should you wish to delve into the language’s features, beyond what is covered in _iOS Programming_.
*   “[Coding Together: Developing iOS 6 Apps for iPhone and iPad](https://itunes.apple.com/us/course/coding-together-developing/id593208016),” Stanford University This series of videos is available through iTunes U.
*   “[WWDC 2013 Session Videos](https://developer.apple.com/wwdc/videos/),” Apple After each Worldwide Developers Conference, Apple publishes videos of all of the sessions. iOS developers at every level will find something here.
*   “[iOS 7 Design Resources](https://developer.apple.com/library/ios/navigation/),” Apple The documentation for iOS is quite good, and Apple has many well-written [guides](https://developer.apple.com/library/ios/navigation/#section=Resource%20Types&topic=Guides) on key features of the iOS SDK.
*   [Ray Wenderlich: Tutorials for iPhone / iOS Developers and Gamers](https://www.raywenderlich.com/) Ray provides a great series of tutorials, and new content is added regularly. Premium tutorials are also available at cost.

This concludes the first segment of our tour of app development. I hope it has given you <strong>some insight into the basic concepts</strong> behind native app development on iOS. The <a href="https://www.smashingmagazine.com/2014/01/four-ways-to-build-a-mobile-app-part2-native-android/">next article in this series</a> will cover how to build the same application using native Android development tools.

{{< signature "al, ea" >}}


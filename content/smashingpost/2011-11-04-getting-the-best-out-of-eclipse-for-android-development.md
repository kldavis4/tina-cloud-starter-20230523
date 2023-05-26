---
title: Getting The Best Out Of Eclipse For Android Development
slug: getting-the-best-out-of-eclipse-for-android-development
image: null
date: 2011-11-04T07:40:30.000Z
author: sue-smith
description: >-
  Getting into Android development can be quite a challenge, particularly if
  you’re new to Java or Eclipse or both. Whatever your past experience, you
  might feel tempted to start working away without checking that you’re making
  the best use of the IDE. In this article, we’ll go over a few tips, tools and
  resources that can maximize Eclipse’s usefulness and hopefully save you a few
  headaches. You might of course already be familiar with some (or all) of them
  and even be aware of others that we haven’t covered. If so, please do feel
  free to mention them.

  I’ve used Eclipse for Java development on and off for a few years, having
  recently started learning Android casually. I’m surprised at the lack of
  easily digestible material online about basic aspects of Android development,
  such as the topic of this article. I’ve found some useful information out
  there in disparate locations that are not particularly easy to come across.
  Most of the online content is still in the official Android Developer Guide,
  but it has to be said that it is pretty limited in practical material.
categories:
  - Coding
  - Eclipse
  - Android
---
Getting into Android development can be quite a challenge, particularly if you’re new to Java or Eclipse or both. Whatever your past experience, you might feel tempted to start working away without checking that you’re making the best use of the IDE. In this article, we’ll go over a few tips, tools and resources that can maximize Eclipse’s usefulness and hopefully save you a few headaches. You might of course already be familiar with some (or all) of them and even be aware of others that we haven’t covered. If so, please do feel free to mention them.

I’ve used Eclipse for Java development on and off for a few years, having recently started learning Android casually. I’m surprised at the lack of easily digestible material online about basic aspects of Android development, such as the topic of this article. I’ve found some useful information out there in disparate locations that are not particularly easy to come across. Most of the online content is still in the official Android Developer Guide, but it has to be said that it is pretty limited in practical material.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Get Started Developing for Android with Eclipse](https://www.smashingmagazine.com/2010/10/get-started-developing-for-android-with-eclipse/)
*   [Get Started Developing For Android With Eclipse, Reloaded](https://www.smashingmagazine.com/2011/03/get-started-developing-for-android-with-eclipse-reloaded/)
*   [Four Ways To Build A Mobile Application: Native Android](https://www.smashingmagazine.com/2014/01/four-ways-to-build-a-mobile-app-part2-native-android/)

The aim here, then, is to provide a concise overview of Android development tools specifically in Eclipse. If you’ve already started developing for Android, you will almost certainly have come across some of them, but a few might be new to you, especially if you’re learning Android casually or part time. If you’re approaching Android as a Java developer and are already accustomed to Eclipse, you’ll likely grasp this material well.

{{% feature-panel %}}

## Get To Know Eclipse

Going over some features of Eclipse itself that would be useful for developing Android projects would be worthwhile. If you already know your way around Eclipse, you can probably skip these first few sections, because they’re really aimed at people who are learning to use the IDE purely for Android development. Later sections include tips on using Eclipse specifically for Android, so you might find a bit or two in there that you haven’t explored yet.

<img class="106770" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d033287b-aac5-476b-b866-3093e2bf3818/eclipseandroid.png" alt="screenshot" width="500" height="300" /><br>
<em>The Eclipse IDE, with the “Hello Android” project open.</em>

Eclipse has a huge amount of flexibility for creating a working environment for your development projects. Many display options, tools and shortcuts in Eclipse enable you to interact with your projects in a way that will make sense to you directly. Having been an Eclipse user for a reasonable amount of time now, I still discover features in it that I had no idea existed and that could have saved me a lot of hassle in past projects.</p>

## Explore Perspectives

The Eclipse user interface provides a variety of ways to view the elements in any project. When you open Eclipse, depending on which “perspective” is open, you will typically see the screen divided into a number of distinct sections. In addition to the code editing area, you should see various aspects of the project represented in particular “views.”

A <strong>perspective</strong> in Eclipse is a group of views arranged to present a project in a particular way. If you open the “Window” menu, then select “Open Perspective,” you will usually see at least two options: “Debug” and “Java.” The Java perspective will likely form the basis of your Android development process; but for debugging, there is an Android-specific perspective called DDMS. Once you have set a perspective, you can still make alterations to the visible views, as well as adjust the layout by dragging the view areas around to suit yourself.

In general, when developing Android projects, some variation of the <strong>Java perspective</strong> is likely to be open, with the option of a few additional views, such as “LogCat,” where you can send and read the runtime output of your app. The <strong>Dalvik Debug Monitor Server (DDMS) perspective</strong> will likely be useful when the time comes to debug your Android applications. The tools in this perspective come as part of the Android software development kit (SDK), with Eclipse integration courtesy of the Android Developer Tools (ADT) plugin. The DDMS perspective provides a wide range of debugging tools, which we’ll cover in brief later on.</p>

## Make Use Of Views

By default, the Java perspective contains the main area to edit code and a handful of <strong>views</strong> with varying levels of usefulness for Android projects:

*   **Package Explorer**.  This provides a hierarchical way to explore your projects, allowing you to browse and control the various elements in them through a directory structure.
*   **Outline**.  Displays an interactive representation of the file currently open in the editor, arranged as logical code units, which can be useful for quickly jumping to a particular point in a big file.
*   **Problems**.  Lists errors and warnings generated at the system level during the development process.
*   **Javadoc**.  Useful if you’re creating your own documentation using Javadoc or using other language resources that have this documentation.
*   **Declaration**.  Particularly useful if your Android projects have a lot of classes and methods. You can click on a variable or method in your code to see its outline here, and then click within the view to jump to the point where the item is declared.

You can open new views in Eclipse by selecting “Show View” in the Window menu and clicking from there. Many of the available views won’t likely be of any use to your Android project, but it is worth experimenting with them. If you open a view and decide that you don’t want to display it after all, simply close it. Adjust or move open views to different locations in Eclipse by clicking and dragging their edges or the tabbed areas at the top.</p>

### Java Views Relevant to Android Development

The <strong>ADT plugin</strong> for Eclipse includes a variety of resources for Android development within the IDE, some of which we’ll cover in the sections below. Eclipse has additional views for general Java programming, some of which naturally have a greater potential for usefulness in Android development but don’t appear by default in the Java perspective. In my experience, views that are useful for Android development include “Call Hierarchy,” “Type Hierarchy” and “Tasks.”

The <strong>Call Hierarchy</strong> view displays an interactive list of the calls for any particular method, class or variable, so you can keep track of where your code excerpts are being called from. This is particularly useful if you’re altering existing code and need a sense of what will be affected.

<img class="106770" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc3121dd-7f4d-4b20-b46f-f599d1b2ed0d/callhierarchy.png" alt="screenshot" width="500" height="300" /><br>
<em>The Call Hierarchy view for a method in one of my projects.</em>

The <strong>Type Hierarchy</strong> view is relevant to Java projects that involve inheritance, which basically means that it’s relevant to all Android projects. Whenever you have a class that extends another class, this is inheritance and, thus, an instance when the Type Hierarchy view can be informative. If you’re not yet familiar with inheritance in Java, taking the time to at least read up on <a href="https://download.oracle.com/javase/tutorial/java/IandI/subclasses.html">the basics</a> is well worth it, because the technique is key to Android programming.

<img loading="lazy" decoding="async" class="106771" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e03fd3e1-bab1-4578-8cef-761b855c6eb4/typehierarchy.png" alt="screenshot" width="500" height="300" /><br>
<em>The Type Hierarchy for a user interface element in an Android project.</em>

The <strong>Tasks</strong> view is one I personally find helpful, but it really depends on how you choose to organize your projects. Think of the Tasks view as an interactive to-do list. For example, to add a task when you haven’t quite finished a particular bit of implementation but need to address something else right away, write a code comment, then right-click in the border area just to the left of the editor section, choose “Add Task,” and set your options from there. Once tasks are in a project, you can read them in the Tasks view, jumping to an individual task in your code by selecting it here. Tasks are also highlighted in the right-hand border of the editor.

<img loading="lazy" decoding="async" class="106772" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69fd50d5-3172-4374-a420-c78bcb3d685e/taskview.png" alt="screenshot" width="500" height="300" /><br>
<em>The Tasks view, with a random comment in the “Hello Android” project.</em>

### Android Debugging Views

The <strong>DDMS</strong> perspective contains several views for Android development and debugging. When you first open the perspective, you might feel a little overwhelmed, particularly because the views are all presented side by side in a rather convoluted arrangement. Chances are that once you learn the purpose of one, you’ll decide whether it’s relevant to your project; for a basic project, many of them will not be.

If you feel that closing some views would make the interface an easier environment to work in, then go ahead and close them; you can always open them again later. Starting simple is sometimes best, and then adding elements over time as they become relevant. In the early stages, your Android project is not likely to be complex anyway.

Let’s go through each <a href="https://developer.android.com/studio/profile/ddms.html?hl=in">DDMS view</a> in Eclipse, with a brief note on its purpose and use. The information is tailored to each view and so is pretty varied, but includes device, memory and process management.

The <strong>Devices</strong> view provides an overview of your running AVD emulators together with processes in operation, and it is the starting point for exploring your projects for the purpose of debugging. This view presents shortcuts to some debugging operations, so you can select your app’s processes from here to see the other debugging operations in action. In most cases, you can view information in the other DDMS views by selecting a running process in the Devices view while your app is running in an emulator, then using the buttons at the top of the view to capture debugging information. When you do this, you’ll see some of the other views being populated with data.

<img loading="lazy" decoding="async" class="106773" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/668db2ab-3e67-4279-82aa-06a42f54c664/devices.png" alt="screenshot" width="500" height="250" /><br>
<em>The Devices view, with a process selected for debugging.</em>

The <strong>Allocation Tracker</strong> view is particularly useful for apps that have significant demands on performance. This view provides insight into how the Dalvik Garbage Collector is managing memory for your app. If you’re not familiar with garbage collection in Java, you might want to read up on it, as well as familiarize yourself with basic <a href="https://java.sun.com/docs/books/performance/1st_edition/html/JPAppGC.fm.html">principles of efficiency</a> in Java programming, such as <a href="https://java.sun.com/docs/books/jls/third_edition/html/statements.html">variable scope</a>.

<img loading="lazy" decoding="async" class="106774" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38d56198-988c-44d6-8334-98a8d7fb7238/allocationtracker.png" alt="screenshot" width="500" height="330" /><br>
<em>The Allocation Tracker view in the DDMS perspective.</em>

The <strong>Emulator Control</strong> view enables you to emulate specific network contexts when testing your apps, allowing you to see how they function with varying constraints on speed, latency and network connectivity. A vital tool if your app depends on such external connections.

<img loading="lazy" decoding="async" class="106775" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/049f4443-a1f3-49e3-9c14-74bc0fb76ed4/emulatorcontrol.png" alt="screenshot" width="500" height="250" /><br>
<em>The Emulator Control view with telephony settings.</em>

The <strong>File Explorer</strong> view enables you to access and control the device’s file system (not the file system in your application’s structure as with the Package Explorer view). Using this, you can copy files to and from the device’s storage system; for example, in the case of an app storing data on the user’s SD card.

<img loading="lazy" decoding="async" class="106776" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4deb88f9-5362-4d19-8951-c7ac20fc5e81/fileexplorer.png" alt="screenshot" width="500" height="250" /><br>
<em>Looking at the SD card directory on a virtual device using the File Explorer view.</em>

The <strong>Heap</strong> view is another tool for analyzing and improving memory management in your app. You can manually control the Garbage Collector from this view. If you are unclear on how the constructs of your Java code relate to heap memory, this is another area you might want to <a href="https://java.sun.com/docs/books/jvms/second_edition/html/Overview.doc.html">read up on</a>.

<img loading="lazy" decoding="async" class="106777" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c470a33-8d42-4b0e-a7dd-8c119172f182/heap.png" alt="screenshot" width="500" height="270" /><br>
<em>The Heap view for a running app.</em>

The <strong>Threads</strong> view enables you to access information about the threads running in your application. If you are unfamiliar with the concept of threads, then this view won’t likely be of use to you. Typically, an Android application runs in a single process on a device, but if you implement a <a href="https://developer.android.com/guide/topics/fundamentals/processes-and-threads.html">deeper level of control</a> over your app’s processing at the level of threads, then this view will be relevant.

<img loading="lazy" decoding="async" class="106778" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f488e7b5-59dc-4a9f-acff-357cba41a259/threads.png" alt="screenshot" width="500" height="230" /><br>
<em>The Threads view for a particular running process.</em>

The <strong>LogCat</strong> view is useful for most Android apps, regardless of their complexity. A variety of messages are automatically outputted here when you run your app, but you can optionally use the view as <span class="removed_link" title="https://developer.android.com/guide/developing/debugging/debugging-log.html">your own custom log</span>. You can create log messages in various categories, including “Debug,” “Info,” “Warning,” “Error” and “Verbose,” which is typically used for low-priority information such as development trace statements. In the LogCat view, you can then filter the messages in order to quickly scroll to those you’re interested in. The messages are also color-coded, making them a little easier to absorb.

<img loading="lazy" decoding="async" class="106779" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e54b6316-ee9b-4611-ac6d-5304145a8dbd/logcat.png" alt="screenshot" width="500" height="300" /><br>
<em>The LogCat view as a virtual Android device starts up.</em>

A DDMS perspective view can optionally be added individually to the Java perspective if you find it useful for development as well as debugging. Eclipse is designed to enable you to interact with the project’s elements any way you like, so <strong>don’t be afraid to experiment with the interface</strong>.

## Exploit The Design Tools

The design tools in the ADT have undergone major improvements in recent releases, so if you’ve been disappointed by them in the past and perhaps opted for other tools to design your Android apps, having another look at them now is well worth it.

In the <strong>Graphical Layout</strong> view, you can view your designs with various settings for device software, hardware as well as orientation. The current version generally gives a greatly improved level of control over widgets, views and rendering than most previous versions. You can manage user-interface elements here using the graphical interface, rather than having to implement every aspect of your design in XML code.

<img loading="lazy" decoding="async" class="106780" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d1cb6fae-42c9-45dd-985d-d7a0fb6d2568/graphicallayout.png" alt="screenshot" width="500" height="400" /><br>
<em>The graphical view of an app’s XML layout.</em>

### Design and Graphical Utilities

The ADT plugin update of June 2011 introduced a variety of <a href="https://developer.android.com/sdk/eclipse-adt.html">visual refactoring</a> utilities. While your XML layout files are open in the editor, you can browse the options in Eclipse’s Refactoring menu for Android, choosing from various labor-saving tools such as “<a href="https://tools.android.com/recent/extractstylerefactoring">Extract Style</a>,” which provides a shorthand method of copying style attributes for reuse.

The <strong>Resource Explorer</strong> is a handy interactive way to explore your application’s resources without the hassle of searching the file structure in the “res” folder via the Package Explorer. Although not exclusively for design purposes, the tool is useful for checking what design resources are in your application’s structure. Depending on the app, your <a href="https://developer.android.com/guide/topics/resources/index.html">Resources directory</a> might also contain <a href="https://developer.android.com/guide/topics/resources/providing-resources.html">menu, array, string and value items</a>.

<img loading="lazy" decoding="async" class="106781" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3ccf5268-aefe-4c59-bd8b-32ddb3bd4b5f/resourceexplorer.png" alt="screenshot" width="500" height="210" /><br>
<em>The Resources Explorer showing the Resources directory for an app.</em>

On the subject of resources, the <strong>Resources</strong> interface for any XML files in your app enables you to manage such data graphically, if you prefer not to handle the XML code manually. This can be an effective way to manage both elements and attributes for your application’s XML data.

<img loading="lazy" decoding="async" class="106782" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a48fd1b9-7de2-4b09-98fe-ba9c914c600c/resources.png" alt="screenshot" width="500" height="250" /><br>
<em>A graphical view of the XML file for arrays in an app.</em>

Various visual interaction tools for XML resources have gradually been added and improved in the ADT plugin. For example, the <strong>Manifest</strong> file can also be viewed graphically when you want to control the tags in it, including “Permissions,” “Application” and “Instrumentation.”

<img loading="lazy" decoding="async" class="106939" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a02dbfd-b675-4398-9f69-804a1cf808ed/manifest1.png" alt="screenshot" width="500" height="350" /><br>
<em>An application’s Manifest file, presented graphically.</em>

## Set Your Android Preferences

The “Eclipse Window” menu provides access to the <strong>Preferences settings</strong> for the environment as a whole, with a dedicated section for Android. You may have used this when you first installed the SDK but might not have been in there since then. It’s worth having a look through the options and experimenting with them to create the environment you want.

In the Android section, the “Build” settings include your saved edits to the project’s files, and they also point Eclipse to your keystore for signing the application. The LogCat section lets you set properties for appearance and behavior in the LogCat view. Other options include choosing properties for the DDMS, the code editors and the launch process for the emulator.</p>

## Use The Android Run Configuration Options

When you launch your Android project using the <strong>Run Configurations</strong> menu, you can choose from a <a href="https://developer.android.com/studio/run/emulator.html">range of additional options</a> to suit the functionality of your app. With your Android project selected, choose the “Target” tab to see these options. The first section covers the more general launch parameters for the emulator, including control over speed and latency on the device. This feature is useful if your app depends on a network connection and you want to see how it functions with limited connectivity.</p>

### Emulator Command-Line Options

The “Target” tab also allows you to enter command-line options for the emulator that launches your app. Using these, you can tailor the appearance, properties and behavior of the emulator as it launches your app. A lot of options are here for various aspects of the device, including the following properties:

*   **UI**.  Includes scaling the display window and setting the DPI.
*   **Disk image**.  Includes the device’s SD card and cache memory.
*   **Media**.  Covers audio and radio properties.
*   **Debugging**.  Enables and disables specific debug tags.
*   **Network**.  In addition to network speed and latency, you can specify DNS and proxy servers.
*   **System**.  Includes slowing down the device CPU and setting the time zone.

For a full list, see the <span class="removed_link" title="https://developer.android.com/guide/developing/tools/emulator.html">Developer Guide</span>.</p>

## Choose Useful AVD Configurations

When you create virtual devices in Eclipse using the <a href="https://developer.android.com/studio/index.html">Android SDK and AVD Manager</a>, through the “Window” menu you can choose various settings, including <strong>API versions and hardware configurations</strong>, such as the size of the SD card and screen, plus optional hardware components. The sheer range of options can leave you wondering where to start, but the feature at least gives you <em>some</em> idea of how your apps will look and function on various devices.

<img loading="lazy" decoding="async" class="106921" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a9513f6-8cd4-4ea6-8f71-64c221c3e507/newavd.png" alt="screenshot" width="500" height="330" /><br>
<em>Entering the details for a new AVD.</em>

To create a virtual device, select “New,” enter a name and choose “Options.” You can edit your devices later if necessary. To start an AVD running, select it in the SDK and AVD Manager and click “Start.”

<img loading="lazy" decoding="async" class="106936" style="border: 1px solid #CCC" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/258ff8c8-cd34-4422-846a-e7efb4e26214/startavd1.png" alt="screenshot" width="500" height="290" /><br>
<em>Choosing from a variety of AVDs to start running.</em>

Some developers prefer configuration options that match the range of Android devices currently in use, which obviously vary widely, with multiple phone sizes and types, not to mention <a href="https://mobile.tutsplus.com/tutorials/android/android-sdk_tablet_virtual-device-configuration/">tablets</a>. There is no dedicated resource for finding this data, but a number of websites <a href="https://mobile.tutsplus.com/tutorials/android/common-android-virtual-device-configurations/">list these configuration details</a> periodically, so you can do a quick Web search when testing an app for release to find the most current information.

It must be said that <strong>there is a real limit in value to using actual device settings</strong>, because the emulator is merely a guide: <strong>it doesn’t replicate the look and feel of different devices with any authenticity</strong>. These limitations are especially pertinent when you consider the third parties involved, such as HTC’s Sense interface, which will substantially alter your application’s UI. This is why <strong>testing on actual devices</strong> is also important, but that’s another topic. The range of devices running Android will obviously continue to expand, so the feasibility of covering a significant chunk of them becomes more and more remote.

Rather than focusing on actual devices in use, another way to approach the AVD configuration settings while you’re in Eclipse (i.e. when you’re still developing rather than testing) is to simply try to cover a range of settings and to explore particular hardware and software configurations that could affect your app’s functionality. Visually speaking, it goes without saying that a <strong>relative</strong> rather than <strong>fixed</strong> design will cope better with various screen sizes.</p>

## Get And Keep Yourself Acquainted With Developer Resources

As you’re by now aware, if you weren’t already, the Android Developer Tools plugin is what allows you to develop, run, test and debug Android applications in Eclipse, together with the software development kit. Like Eclipse itself, both the SDK and ADT plugins offer many tools, many of which you could very easily remain unaware of and only a few of which we have touched on in this article.

The Android development resources undergo regular updates. You might be one of those people who are always on the ball, but if you’re anything like me, you’ll rarely find the time to keep abreast of these developments, especially if (like me) Android development is not your full-time job.

The Android Developer Guide <a href="https://developer.android.com/guide/developing/tools/index.html">lists the various tools in the SDK</a>, many of which you will not need to access directly, because the ADT plugin and Eclipse will handle interaction with them. But it’s worth browsing the list fairly regularly, just to be aware of the tools available. Even if you’re only getting into Android casually, these utilities can make an enormous difference to how productive and enjoyable your app’s experience is. The <a href="https://android-developers.blogspot.com/">Android Developers Blog</a> is another good source to keep abreast of developments.

The ADT plugin itself comes with a wealth of features and is regularly updated. The Android SDK Guide also has a <a href="https://developer.android.com/sdk/eclipse-adt.html">page on the plugin</a>, outlining versions and features; again, well worth checking out regularly, because there may be significant updates. Checking for updates in Eclipse through the “Help” menu is another good habit.

Android apps are, of course, extremely varied, so the utility of any given development tool is necessarily relative. Keeping a eye on updates to resources needn’t take up much time, because in many cases the updates will be irrelevant to you. But discovering the ones that <em>are</em> relevant could seriously improve your Android development efforts.</p>

## Following Best Practices

If you’re interested in developing a best-practices approach to <strong>managing and documenting</strong> your apps, check out <a href="https://maven.apache.org/">Apache Maven</a>, which uses the <a href="https://maven.apache.org/pom.html">project object model</a> (POM). If you’ve already used Maven for Java development in Eclipse, the <a href="https://code.google.com/p/maven-android-plugin/">Android plugin</a> and Integration tools will enable you to adopt the same development practices for your Android app. You can learn more about Maven <a href="https://maven.apache.org/guides/getting-started/index.html">on the Apache website</a>, and you can learn about getting started with it for Android <span class="removed_link" title="https://www.sonatype.com/books/mvnref-book/reference/android-dev.html">on the Sonatype website</span>.</p>

### Other Resources

*   “[Android Development Tutorial](https://www.vogella.de/articles/Android/article.html),” Lars Vogel
*   “[SDK Tools](https://developer.android.com/guide/developing/tools/index.html),” Android Developer Guide
*   “[Using DDMS](https://developer.android.com/studio/profile/ddms.html?hl=in),” Android Developer Guide
*   “[ADT Plugin for Eclipse](https://developer.android.com/sdk/eclipse-adt.html),” Android Developer Guide
*   “[Introduction to Android Development Using Eclipse and Android Widgets](https://www.ibm.com/developerworks/opensource/tutorials/os-eclipse-androidwidget/index.html),” IBM developerWorks
*   “[Eclipse Shortcuts](https://www.vogella.de/articles/EclipseShortcuts/article.html),” Lars Vogel
*   “[Eclipse Documentation](https://help.eclipse.org/indigo/index.jsp),” Eclipse Foundation
*   “[Eclipse IDE Tutorial](https://www.vogella.de/articles/Eclipse/article.html),” Lars Vogel
*   “[Develop Android Applications With Eclipse](https://www.ibm.com/developerworks/opensource/tutorials/os-eclipse-android/section5.html),” IBM developerWorks
*   “[Eclipse Tips and Customization](https://eagle.phys.utk.edu/guidry/android/eclipseTips.html),” University of Tennessee
*   “[Ten Tips for Android Application Development](https://answers.oreilly.com/topic/862-ten-tips-for-android-application-development/),” Zigurd Mednieks

### Related Articles

*   “[Android GUI PSD Vector Kit](https://www.smashingmagazine.com/2009/08/18/android-gui-psd-vector-kit/),” Smashing Magazine
*   “[Designing For Android](https://www.smashingmagazine.com/2011/06/30/designing-for-android/),” Dan McKenzie
*   “[Get Started Developing for Android with Eclipse](https://www.smashingmagazine.com/2010/10/25/get-started-developing-for-android-with-eclipse/),” Chris Blunt
*   “[Get Started Developing For Android With Eclipse, Reloaded](https://www.smashingmagazine.com/2011/03/28/get-started-developing-for-android-with-eclipse-reloaded/),” Chris Blunt

{{< signature "al" >}}


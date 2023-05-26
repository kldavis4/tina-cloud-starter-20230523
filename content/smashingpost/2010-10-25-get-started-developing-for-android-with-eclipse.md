---
title: Get Started Developing For Android With Eclipse
slug: get-started-developing-for-android-with-eclipse
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f833da72-8230-40dc-9bb2-0bc9c92e9e62/android2.jpg
date: 2010-10-25T12:40:45.000Z
author: chris-blunt
description: >-
  There's a lot to get excited about in mobile application development today.
  With increasingly sophisticated hardware, tablet PCs and a variety of software
  platforms (Symbian OS, iOS, WebOS, Windows Phone 7...), the landscape for
  mobile developers is full of opportunities — and a little complex as well.

  So much choice can be overwhelming when you just want to **get started
  building mobile applications**. Which platform should you choose? What
  programming language should you learn? What kit do you need for your planned
  project? In this tutorial, you'll learn how to start writing applications for
  [Android](https://android.com/), the open-source mobile operating system
  popularized by Google.
categories:
  - Coding
  - Eclipse
  - Android
---
There's a lot to get excited about in mobile application development today. With increasingly sophisticated hardware, tablet PCs and a variety of software platforms (Symbian OS, iOS, WebOS, Windows Phone 7...), the landscape for mobile developers is full of opportunities — and a little complex as well.

So much choice can be overwhelming when you just want to <strong>get started building mobile applications</strong>. Which platform should you choose? What programming language should you learn? What kit do you need for your planned project? In this tutorial, you'll learn how to start writing applications for <a href="https://android.com/">Android</a>, the open-source mobile operating system popularized by Google.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Getting The Best Out Of Eclipse For Android Development](https://www.smashingmagazine.com/2011/11/getting-the-best-out-of-eclipse-for-android-development/)
*   [Get Started Developing For Android With Eclipse, Reloaded](https://www.smashingmagazine.com/2011/03/get-started-developing-for-android-with-eclipse-reloaded/)
*   [Mobile Design Practices For Android: Tips And Techniques](https://www.smashingmagazine.com/2012/07/android-design-tips/)

## Why Develop for Android?

Android is an open-source platform based on the Linux kernel, and is installed on <a href="https://mashable.com/2010/09/16/android-comscore-july-2010/">thousands of devices</a> from a wide range of manufacturers. Android exposes your application to all sorts of hardware that you'll find in modern mobile devices — digital compasses, video cameras, GPS, orientation sensors, and more.

{{% feature-panel %}}

Android's free development tools make it possible for you to start writing software at little or no cost. When you're ready to show off your application to the world, you can publish it to Google's Android Market. <strong>Publishing to Android Market</strong> incurs a one-off registration fee (US $25 at the time of writing) and, unlike Apple's App Store which famously reviews each submission, makes your application available for customers to download and buy after a quick review process — unless the application is blatantly illegal.

Here are a few other advantages Android offers you as a developer:

*   The Android SDK is available for Windows, Mac and Linux, so you don't need to pay for new hardware to start writing applications.
*   An SDK built on Java. If you're familiar with the Java programming language, you're already halfway there.
*   By distributing your application on Android Market, it's available to [hundreds of thousands](https://www.wired.com/gadgetlab/2010/08/google-200000-android-phones/) of users instantly. You're not just limited to one store, because there are alternatives, too. For instance, you can release your application on your own blog. Amazon have recently been [rumoured](https://www.slashgear.com/amazon-android-app-store-tcs-leak-29104993/) to be preparing their own Android app store also.
*   As well as the technical [SDK documentation](https://developer.android.com/sdk/index.html), new resources are being published for Android developers as the platform gains popularity among both users and developers.

Enough with the talk — let's get started developing for Android!

## Installing Eclipse and the Android SDK

The recommended environment for <strong>developing Android applications</strong> is Eclipse with the Android Development Toolkit (ADT) plugin installed. I'll summarize the process here. If you need more detail, Google's own <a href="https://developer.android.com/sdk/">developer pages</a> do a good job of explaining the installation and configuration process.

*   Download the [Android SDK](https://developer.android.com/) for your platform (Windows, Mac OS X, or Linux).
*   Extract the downloaded file to somewhere memorable on your hard drive (on Linux, I use `/opt/local/`).
*   If you don't already have Eclipse installed, download and install the [Eclipse IDE for Java Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-developers/galileosr2) package. For programming, Google recommends using Eclipse 3.5 (Galileo).
*   Run Eclipse and choose _Help->Install New Software_.
*   Click _Add_ in the Available Software window.
*   Enter `Android Development Tools` in the _Name_ field, and `https://dl-ssl.google.com/android/eclipse/` in the _Location_ field.
*   Click _OK_ and check _Developer Tools_ in the list of available software. This will install the Android Development Tools and DDMS, Android's debugging tool.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09084184-0350-4c08-947c-8cac9c9ccea0/eclipse-install-adt.jpg"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-68739" title="eclipse_install_adt-550" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ef8fe09-f671-42af-8061-76702c4285d6/install.gif" alt="Screensot" width="500" height="519" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09084184-0350-4c08-947c-8cac9c9ccea0/eclipse-install-adt.jpg">Large image</a></em>

*   Click _Next_ and _Finish_ to install the plugin. You'll need to restart Eclipse once everything is installed.
*   When Eclipse restarts, choose _Window->Preferences_ and you should see _Android_ listed in the categories.
*   You now need to tell Eclipse where you've installed the Android SDK. Click _Android_ and then _Browse_ to select the location where you extracted the SDK files. For example, `/opt/local/android-sdk`. [![Configuring ADT](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/123d8ddd-c555-4ebd-a2d0-2792c6c0d85b/prefs.jpg "Configuring ADT")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2c665c6-fec5-4bb9-9375-f0ff316ad17a/eclipse-android-preferences.jpg) _[Large view](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2c665c6-fec5-4bb9-9375-f0ff316ad17a/eclipse-android-preferences.jpg)_
*   Click _OK_ to have Eclipse save the location of your SDK.</p>

## Targeting Android Platforms

Before you can start writing applications for Android, you need to download the SDK platforms for the Android devices for which you want to develop apps. Each platform has a different version of the Android SDK that may be installed on users' devices. For versions of Android 1.5 and above, there are two platforms available: <em>Android Open Source Project</em> and <em>Google</em>.

The <em>Android Open Source Project</em> platforms are open source, but do not include Google's proprietary extensions such as <em>Google Maps</em>. If you choose not to use the Google APIs, Google's mapping functionality won't be available to your application. Unless you have a specific reason not to, I'd recommended you to target one of the Google platforms, as this will allow you to take advantage of Google's proprietary extensions.

*   Choose _Window->Android SDK and AVD Manager_.
*   Click _Available Packages_ in the left column and check the repository to show a list of the available Android platforms.
*   You can choose which platforms to download from the list, or leave everything checked to download all the available platforms. When you're done, click _Install Selected_ and follow the installation instructions.[![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bda5b1f9-c72a-4334-acfc-6648f11e2be7/sdk.jpg "sdk_manager_platforms-550")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e758338b-0c4f-4e50-a302-abc8d9eae474/sdk-manager-platforms.jpg) _[Large image](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bf0bf1ab-3ef6-46aa-a1d3-30d9a22949c9/sdk-manager-platforms-550-e1287474433673.jpg)_

Once everything has been successfully downloaded, you're ready to start developing for Android.</p>

## Creating a New Android Project

Eclipse's New Project Wizard can create a new Android application for you, generating files and code that are ready to run right out of the box. It's a quick way to see something working, and a good starting point from which to develop your own applications:

*   Choose _File->New->Project..._
*   Choose _Android Project_
*   In the _New Project_ dialog, enter the following settings:

        Project Name: BrewClock
        Build Target: Google Inc. 1.6 (Api Level 4)
        Application Name: BrewClock
        Package Name: com.example.brewclock
        Create Activity: BrewClockActivity
        Min SDK Version: 4

    [![](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1981bfb-8d0c-4b37-83b4-f6f980f9355e/eclipse-new-project-settings.jpg "eclipse_new_project_settings")](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e1981bfb-8d0c-4b37-83b4-f6f980f9355e/eclipse-new-project-settings.jpg)

After clicking <em>Finish</em>, Eclipse will create a new Android project that's ready to run. Notice you told Eclipse to generate an Activity called <code>BrewClockActivity</code>? This is the code that Android actually uses to run your application. The generated code will display a simple 'Hello World' style message when the application runs.</p>

### Packages

The package name is an identifier for your application. When the time comes and you are willing to publish on Android Market, it's exactly this identifier that will be used to track your application for updates, so it's important to <strong>make sure it's unique</strong>. Although we're using the <code>com.example.brewclock</code> namespace here, for a real application it's best to choose something like <code>com.yourcompanyname.yourapplication</code>.</p>

### SDK Versions

The <code>Min SDK Version</code> is the earliest version of Android on which your application will run. With each new release of Android, the SDK adds and changes methods. By choosing an SDK version, Android (and the Android Market) knows that your application will only run on devices with a version of Android later or equal than the specified version.</p>

## Running Your Application

Now let's try running the application in Eclipse. As this is the first run, Eclipse will ask what type of project you are working on:

*   Choose _Run->Run_ or press _Ctrl+F11_.
*   Choose _Android Application_ and click _OK_.

Eclipse will now try to run the application on an Android device. At the moment, though, you don't have any Android devices running, so the run will fail and you'll be asked to create a new <em>Android Virtual Device</em> (AVD).

<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-68582" title="eclipse_no_avd" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a8c6308-95d0-446c-8909-09cbe56324c7/eclipse-no-avd.jpg" alt="" width="534" height="172" />

### Android Virtual Devices

An Android Virtual Device (AVD) is an emulator that simulates a real-world Android device, such as a mobile phone or Tablet PC. You can use AVDs to test how your application performs on a wide variety of Android devices, without having to buy every gadget on the market.

You can create as many AVDs as you like, each set up with different versions of the Android Platform. For each AVD you create, you can configure various hardware properties such as whether it has a physical keyboard, GPS support, the camera resolution, and so on.

Before you can run your application, you need to create your first AVD running the target SDK platform (Google APIs 1.6).

Let's do that now:

*   If you haven't tried to run your application yet, click _Run_ now (or hit _Ctrl+F11_)
*   When the target device warning pops up, click _Yes_ to create a new AVD.
*   Click _New_ in the _Android SDK and AVD Manager_ dialog that appears.
*   Enter the following settings for the AVD:

        Name: Android_1.6
        Target: Google APIs (Google Inc.) - API Level 4
        SD Card Size: 16 MiB
        Skin Built In: Default (HVGA)

*   Click _Create AVD_ to have Android build your new AVD.
*   Close the _Android SDK and AVD Manager_ dialog.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26795efb-3497-4565-9ac8-73026fd7a395/sdk-manager-new-avd.jpg"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-68583" title="sdk_manager_new_avd" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26795efb-3497-4565-9ac8-73026fd7a395/sdk-manager-new-avd.jpg" alt="" width="400" height="574" /></a>

### Running the Code

Try running your application again (<em>Ctrl+F11</em>). Eclipse will now build your project and launch the new AVD. Remember, the AVD emulates a complete Android system, so you'll even need to sit through the slow boot process just like a real device. For this reason, once the AVD is up and running, it's best not to close it down until you've finished developing for the day.

When the emulator has booted, Eclipse automatically installs and runs your application:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e88e5b30-32b0-41ea-9ea3-2c49c96c615b/app-running.jpg"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-68737" title="app_running-550" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd78c423-ecd8-45ff-92c9-682f11e4e505/app-running-550-e1287474474253.jpg" alt="" width="499" height="355" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e88e5b30-32b0-41ea-9ea3-2c49c96c615b/app-running.jpg">Large image</a></em>

## Building Your First Android Application

Testing generated code is all well and good, but you want to start building a real application. For this, we'll step through a simple design process and build an application that you can deploy to your Android device.

Most developers (myself included) like a <strong>constant supply of good tea or coffee</strong>. In the next section of this article you'll build a simple tea counter application to track how many cups of tea (<em>brews</em>) the user has drunk, and let them set a timer for brewing each cup.

You can download the complete code for this tutorial on <a href="https://github.com/cblunt/brewclock">GitHub</a>.</p>

### Designing the User Interface

One of the first steps to building any Android application is to design and build the user interface. Here's a quick sketch of how the application's interface will look:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b23b12f6-f5ae-47f2-a107-322f364b6783/design-sketch.jpg"><img loading="lazy" decoding="async" class="68578 alignnone" title="design_sketch" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b23b12f6-f5ae-47f2-a107-322f364b6783/design-sketch.jpg" alt="" width="331" height="505" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b23b12f6-f5ae-47f2-a107-322f364b6783/design-sketch.jpg">Large image</a></em>

The user will be able to set a brew time in minutes using the <em>+</em> and <em>-</em> buttons. When they click <em>Start</em>, a countdown will start for the specified number of minutes. Unless the user cancels the brew by tapping the button again, the brew count will be increased when the countdown timer reaches 0.</p>

### Building the Interface

Android user interfaces, or <em>layouts</em>, which are described in XML documents, can be found in the <code>res/layouts</code> folder. The template code that Eclipse generated already has a simple layout declared in <code>res/layouts/main.xml</code> which you may have seen previously while the application was running on the emulator.

Eclipse has a graphical layout designer that lets you build the interface by 'dragging' and 'dropping' controls around the screen. However, I often find it easier to write the interface in XML and use the graphical layout to preview the results.

Let's do this now by changing <code>main.xml</code> to match the design sketch above:

*   Open `res/layouts/main.xml` in Eclipse by double-clicking it in the _Package Explorer_.
*   Click the `main.xml` tab along the bottom of the screen to switch to XML view.

Now change the content of <code>main.xml</code> to:

<pre><code class="language-javascript"># /res/layouts/main.xml
&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;LinearLayout
  xmlns:android="https://schemas.android.com/apk/res/android"
  android:orientation="vertical"
  android:layout_width="fill_parent"
  android:layout_height="fill_parent"&gt;
  &lt;LinearLayout
    android:orientation="horizontal"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:padding="10dip"&gt;
    &lt;TextView
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:textSize="20dip"
      android:text="Brews: " /&gt;
    &lt;TextView
      android:layout_width="fill_parent"
      android:layout_height="wrap_content"
      android:text="None"
      android:gravity="right"
      android:textSize="20dip"
      android:id="@+id/brew_count_label" /&gt;
  &lt;/LinearLayout&gt;
  &lt;LinearLayout
    android:orientation="horizontal"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:layout_weight="1"
    android:gravity="center"
    android:padding="10dip"&gt;
    &lt;Button
      android:id="@+id/brew_time_down"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:text="-"
      android:textSize="40dip" /&gt;
    &lt;TextView
      android:id="@+id/brew_time"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:text="0:00"
      android:textSize="40dip"
      android:padding="10dip" /&gt;
    &lt;Button
      android:id="@+id/brew_time_up"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:text="+"
      android:textSize="40dip" /&gt;
  &lt;/LinearLayout&gt;
  &lt;Button
    android:id="@+id/brew_start"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:layout_gravity="bottom"
    android:text="Start" /&gt;
&lt;/LinearLayout&gt;</code></pre>

As you can see, Android's XML layout files are verbose, but allow you to control virtually every aspect of elements on the screen.

One of the most important interface elements in Android are <code>Layout</code> containers, such as the <code>LinearLayout</code> used in this example. These elements are invisible to the user but act as layout containers for other elements such as <code>Buttons</code> and <code>TextViews</code>.

There are several types of layout views, each of which is used to build different types of layout. As well as the <code>LinearLayout</code> and <code>AbsoluteLayout</code>, the <code>TableLayout</code> allows the use of complex grid-based interfaces. You can find out more about Layouts in the <a href="https://developer.android.com/guide/topics/ui/layout-objects.html">Common Layout Objects</a> section of the API documents.</p>

### Linking Your Layout With Code

After saving your layout, try running your application in the emulator again by pressing <em>Ctrl+F11</em>, or clicking the <em>Run</em> icon in Eclipse. Now instead of the 'Hello World' message you saw earlier, you'll see Android now displays your application's new interface.

If you click any of the buttons, they'll highlight as expected, but don't do anything yet. Let's remedy that by writing some code behind the interface layout:

<pre><code class="language-javascript"># /src/com/example/brewclock/BrewClockActivity.java
...
import android.widget.Button;
import android.widget.TextView;

public class BrewClockActivity extends Activity {
  /** Properties **/
  protected Button brewAddTime;
  protected Button brewDecreaseTime;
  protected Button startBrew;
  protected TextView brewCountLabel;
  protected TextView brewTimeLabel;

  ...
 }</code></pre>

Next, we'll change the call to <code>onCreate</code>. This is the method that gets called whenever Android starts your application. In the code that Eclipse generated, <code>onCreate</code> sets the activity's view to be <code>R.layout.main</code>. It's that line of code that tells Android to decode our layout XML document and display it to the user.</p>

### The Resource Object

In Android, <code>R</code> is a special object that is automatically generated to allow access to your project's resources (layouts, strings, menus, icons...) from within the code. Each resource is given an <code>id</code>. In the layout file above, these are the <code>@+id</code> XML attributes. We'll use those attributes to connect the <code>Buttons</code> and <code>TextViews</code> in our layout to the code:

<pre><code class="language-javascript"># /src/com/example/brewclock/BrewClockActivity.java
...
public class BrewClockActivity extends Activity {
  ...
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);

    // Connect interface elements to properties
    brewAddTime = (Button) findViewById(R.id.brew_time_up);
    brewDecreaseTime = (Button) findViewById(R.id.brew_time_down);
    startBrew = (Button) findViewById(R.id.brew_start);
    brewCountLabel = (TextView) findViewById(R.id.brew_count_label);
    brewTimeLabel = (TextView) findViewById(R.id.brew_time);
  }
}</code></pre>

### Listening For Events

In order to detect when the user taps one of our buttons, we need to implement a listener. You may be familiar with listeners or <em>callbacks</em> from other event-driven platforms, such as Javascript/jQuery events or Rails' callbacks.

Android provides a similar mechanism by providing <code>Listener</code> interfaces, such as <code>OnClickListener</code>, that define methods to be triggered when an event occurs. Implementing the <code>OnClickListener</code> interface will notify your application when the user taps the screen, and on which button they tapped. You also need to tell each button about the <code>ClickListener</code> so that it knows which listener to notify:

<pre><code class="language-javascript"># /src/com/example/brewclock/BrewClockActivity.java
...
// Be sure not to import
// `android.content.dialoginterface.OnClickListener`.
import android.view.View.OnClickListener; 

public class BrewClockActivity extends Activity
  implements OnClickListener {
  ...
  public void onCreate(Bundle savedInstanceState) {
    ...
    // Setup ClickListeners
    brewAddTime.setOnClickListener(this);
    brewDecreaseTime.setOnClickListener(this);
    startBrew.setOnClickListener(this);
  }
  ...
  public void onClick(View v) {
    // TODO: Add code to handle button taps
  }
}</code></pre>

Next we'll add code that handles each of our button presses. We'll also add four new properties to the Activity that will let the user set and track the brewing time, how many brews have been made, and whether the timer is currently running.

<pre><code class="language-javascript"># /src/com/example/brewclock/BrewClockActivity.java
...
public class BrewClockActivity extends Activity
  implements OnClickListener {
  ...
  protected int brewTime = 3;
  protected CountDownTimer brewCountDownTimer;
  protected int brewCount = 0;
  protected boolean isBrewing = false;
  ...
  public void onClick(View v) {
    if(v == brewAddTime)
      setBrewTime(brewTime + 1);
    else if(v == brewDecreaseTime)
      setBrewTime(brewTime -1);
    else if(v == startBrew) {
      if(isBrewing)
        stopBrew();
      else
        startBrew();
    }
  }
}</code></pre>

Notice we're using the <code>CountDownTimer</code> class provided by Android. This lets you easily create and start a simple countdown, and be notified at regular intervals whilst the countdown is running. You'll use this in the <code>startBrew</code> method below.

The following methods are all model logic that handles setting the brew time, starting and stopping the brew and maintaining a count of brews made. We'll also initialize the <code>brewTime</code> and <code>brewCount</code> properties in <code>onCreate</code>.

It would be good practice to move this code to a separate model class, but for simplicity we'll add the code to our <code>BrewClockActivity</code>:

<pre><code class="language-javascript"># /src/com/example/brewclock/BrewClockActivity.java
...
public class BrewClockActivity extends Activity
  implements OnClickListener {
  ...
  public void onCreate(Bundle savedInstanceState) {
    ...
    // Set the initial brew values
    setBrewCount(0);
    setBrewTime(3);
  }

  /**
   * Set an absolute value for the number of minutes to brew.
   * Has no effect if a brew is currently running.
   * @param minutes The number of minutes to brew.
   */
  public void setBrewTime(int minutes) {
    if(isBrewing)
      return;

    brewTime = minutes;

    if(brewTime &lt; 1)
      brewTime = 1;

    brewTimeLabel.setText(String.valueOf(brewTime) + "m");
  }

  /**
   * Set the number of brews that have been made, and update
   * the interface.
   * @param count The new number of brews
   */
  public void setBrewCount(int count) {
    brewCount = count;
    brewCountLabel.setText(String.valueOf(brewCount));
  }

  /**
   * Start the brew timer
   */
  public void startBrew() {
    // Create a new CountDownTimer to track the brew time
    brewCountDownTimer = new CountDownTimer(brewTime * 60 * 1000, 1000) {
      @Override
      public void onTick(long millisUntilFinished) {
        brewTimeLabel.setText(String.valueOf(millisUntilFinished / 1000) + "s");
      }

      @Override
      public void onFinish() {
        isBrewing = false;
        setBrewCount(brewCount + 1);

        brewTimeLabel.setText("Brew Up!");
        startBrew.setText("Start");
      }
    };

    brewCountDownTimer.start();
    startBrew.setText("Stop");
    isBrewing = true;
  }

  /**
   * Stop the brew timer
   */
  public void stopBrew() {
    if(brewCountDownTimer != null)
      brewCountDownTimer.cancel();

    isBrewing = false;
    startBrew.setText("Start");
  }
  ...
}</code></pre>

The only parts of this code specific to Android are setting the display labels using the <code>setText</code> method. In <code>startBrew</code>, we create and start a <code>CountDownTimer</code> to start counting down every second until a brew is finished. Notice that we define <code>CountDownTimer's</code> listeners (<code>onTick</code> and <code>onFinish</code>) inline. <code>onTick</code> will be called every 1000 milliseconds (1 second) the timer counts down, whilst <code>onFinish</code> is called when the timer reaches zero.</p>

### Avoiding Hard-Coded Text in your Code

To keep this tutorial code simple, I've intentionally written label strings directly in the code (e.g. <code>"Brew Up!"</code>, <code>"Start"</code>, <code>"Stop"</code>). Generally, this isn't good practice, as it makes finding and changing those strings harder in large projects.

Android provides a neat way to keep your text strings separate from code with the <code>R</code> object. <code>R</code> lets you define all your application's strings in an xml file (<code>res/values/strings.xml</code>) which you can then access in code by reference. For example:

<pre><code class="language-javascript"># /res/values/strings.xml
&lt;string name="brew_up_label"&gt;Brew Up!&lt;/string&gt;
...

# /res/com/example/brewclock/BrewClockActivity.java
...
brewLabel.setText(R.string.brew_up_label);
...</code></pre>

Now if you wanted to change <code>Brew Up!</code> to something else, you would only need to change it once in the <em>strings.xml</em> file. Your application starts to span dozens of code files which keeps all your strings in one place and makes a lot of sense!

### Trying BrewClock

With the code complete, it's time to try out the application. Hit <em>Run</em> or <em>Ctrl+F11</em> to start BrewClock in the emulator. All being well, you'll see the interface set up and ready to time your tea brewing! Try setting different brew times, and pressing <em>Start</em> to watch the countdown.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d775ac23-985c-4c5e-8d0d-bd8995abb822/app-finished.jpg"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-68736" title="app_finished-550" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de7aafe1-6e74-4757-967e-c1496d81d285/app-finished-550-e1287474491689.jpg" alt="" width="499" height="355" /></a><br>
<em><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d775ac23-985c-4c5e-8d0d-bd8995abb822/app-finished.jpg">Large image</a></em>

## Summary

In this short introduction to Android, you've installed the Android SDK and Eclipse Android Development Tools (ADT) plugin. You've set up an emulator, or virtual device that can test your applications. You've also built a working Android application which has <strong>highlighted a number of key concepts</strong> that you'll use when developing your own Android applications.

Hopefully, this has whet your appetite for building mobile applications, and experimenting in this exciting field. Android offers a great way to start writing applications for a range of current and upcoming mobile devices. If you've built or are working on your own mobile app, be sure to let us know about it in the comments!

<em>(ik), (vf)</em>


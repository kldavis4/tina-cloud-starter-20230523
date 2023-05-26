---
title: 'Four Ways To Build A Mobile Application, Part 2: Native Android'
slug: four-ways-to-build-a-mobile-app-part2-native-android
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a6fa165e-584d-4836-97aa-23e27e8b361a/android-illu-opt.png
date: 2014-01-10T13:25:17.000Z
author: peter-traeg
description: >-
  This article is the second in a series of four articles covering four ways to
  develop mobile applications. The [last
  article](https://www.smashingmagazine.com/2013/11/22/four-ways-to-build-a-mobile-app-part1-native-ios/)
  covered how to accomplish this using native iOS development tools. In this
  article, we’ll look at how to build the same sort of application using native
  Android tools.
categories:
  - Mobile
  - Apps
  - Android
  - Native
---
This article is the second in a series of four articles covering four ways to develop mobile applications. The <a href="https://www.smashingmagazine.com/2013/11/22/four-ways-to-build-a-mobile-app-part1-native-ios/">last article</a> covered how to accomplish this using native iOS development tools. In this article, we’ll look at how to build the same sort of application using native Android tools.

<strong>We’ve been building a simple tip calculator.</strong> As with the iOS application, this one contains two screens: a main view and a settings view. The settings view persists the default tip percentage to local storage using Android’s SDK support. (The source code for each app is <a href="https://github.com/ptraeg/mobile-apps-4-ways">available on GitHub</a>.)

## <span class="rh">Further Reading</span> on SmashingMag:

*   [What Every App Developer Should Know About Android](https://www.smashingmagazine.com/2014/10/what-every-app-developer-should-know-about-android/)
*   [How To Design For Android](https://www.smashingmagazine.com/2011/06/designing-for-android/)
*   [<span class="headline">Designing For A Maturing Android</span>](https://www.smashingmagazine.com/2013/05/brave-new-world-designing-for-a-maturing-android/)

Here’s the UI we’re following for this project:

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10b6cba8-27cd-46b8-8fb1-b5e5b23ae605/android-example-opt.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139877" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/10b6cba8-27cd-46b8-8fb1-b5e5b23ae605/android-example-opt.png" alt="android-example" width="272" height="513" /></a>

## Native Android Development: The Tools

For the Android platform, the Java language is used, along with the Eclipse integrated development environment (IDE). Google provides the <a href="https://developer.android.com/tools/index.html">Android Developer Tools</a> (ADT) plugin for the standard Eclipse IDE to support things like graphical layout definition and debugging. As of the time of writing, Google has also released a new IDE, called <a href="https://developer.android.com/sdk/installing/studio.html">Android Studio</a>, in early-access preview. This product is based on JetBrains’ IntelliJ IDE and will eventually replace Eclipse as the official development tool for Android applications. Because Android Studio is still in prerelease form, <strong>we’ll use Eclipse to develop this application</strong>. Eclipse is very stable, and many Android training resources using Eclipse abound.

The Android development environment is supported on Windows, Mac and Linux. There is no charge for the development tools, and applications may be freely deployed to devices. To submit apps to the Google Play marketplace, developers must <a href="https://play.google.com/apps/publish/signup/">sign up</a> for publishing and pay a one-time fee of $25. Submitting apps to Google Play is notably less involved than for iOS. When your application is submitted to Google, it is scanned for malware and common threats. Generally, the application becomes available to the general public within a few hours.

An <a href="https://developer.android.com/tools/index.html">overview</a> of the toolset can be found on the Android Developers website. Successful Android development entails use of the following tools:

*   Eclipse IDE
*   Android SDK
*   Android ADT
*   Android system images for the Android emulator
*   an Android device (technically not required but highly recommended)

### Grab an Installation Bundle to Ease Your Pain

In the past, you had to download, install and configure the tools individually. This took a fair amount of time and often led to confusion for new Android developers. To make the process easier, Google now offers “bundles,” which simplify the installation process. Bundles are offered for each operating system and are available on the page where you <a href="https://developer.android.com/sdk/index.html">download the developer SDK</a>.

Installing Eclipse, the SDK, the emulator and so on <a href="https://developer.android.com/sdk/installing/bundle.html">is as easy as unpacking</a> a ZIP file into a directory. If you have an existing installation of Eclipse and would prefer to use that instead, there are <a href="https://developer.android.com/sdk/installing/index.html">instructions for adding Android support</a> to it.</p>

## Loading An Existing Application Into Eclipse

Once the Android development tools have been installed, you may wish to import an existing project, such as the <a href="https://github.com/ptraeg/mobile-apps-4-ways">source code</a> for our sample app. In Eclipse, go to <code>File → Import</code> in the menu, which will display the following dialog:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1903c499-1784-4b46-b089-d4d702cd83b5/android-import-step1-500-opt.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="140375" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1903c499-1784-4b46-b089-d4d702cd83b5/android-import-step1-500-opt.jpg" alt="android-import-step1" width="554" height="551" /></a>

Once you’ve chosen the option to import an existing Android project, click the “Next” button, whereupon you will be able to specify the directory where the code that you wish to work with in Eclipse is located.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b10c3e3c-b0ff-4de7-b72a-4dd870a006b7/android-import-step2-500-opt.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="140376" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b10c3e3c-b0ff-4de7-b72a-4dd870a006b7/android-import-step2-500-opt.jpg" alt="android-import-step2" width="559" height="552" /></a>

Once you’ve selected a directory via the “Browse” button, Eclipse will automatically find any Android project in that directory and show it in the list of projects to import. Simply click the “Finish” button, and the project will appear in your list of projects along the left side of the IDE.</p>

## Steps To Building An Application

There are several steps to building an Android application. We’ll cover each in detail later in this article. The steps include the following:

1.  Define the user interface. The UI for an application is generally defined as a series of layout files. These are XML-based files that describe the controls on a screen and the relationship of their layouts relative to one another.
2.  Add image assets, language translations and other resources. **Android refers to non-code assets of a project as resources.** These are placed in the project in a directory structure defined by the Android SDK. At runtime, Android dynamically loads content from this directory structure. We’ll see later on how different assets and layouts can be loaded to support the wide variety of Android device configurations available in the market today.
3.  Write Java code to respond to various events that occur from the controls on a given screen and from changes in the lifecycle of an application. Java code is also responsible for loading the layout and menu files associated with each screen. And it’s used to control the flow from one screen to the next.
4.  Export the completed Android application as a file that can be uploaded to Google Play or shared with others directly.</p>

## The Eclipse ADT For Android Development

The Eclipse IDE provides the standard source-code editing tools, along with a source-level debugger that allows applications to be debugged on both the simulator and a physical device. In contrast to the storyboards used with iOS, a layout editor is used to define screen layouts:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f082bd2-4daa-4b77-bbc2-325afdcfb14b/adt-layout-editor.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139867" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e15ed4be-41a0-41cd-b549-598dce07a3a2/adt-layout-editor-500-opt.jpg" alt="ADT layout editor" width="500" height="299" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f082bd2-4daa-4b77-bbc2-325afdcfb14b/adt-layout-editor.png">Large view</a>)</em>

The layout editor works on a single screen at a time and is not able to define segues between screens, as in the iOS storyboard editor. However, the Android layout editor does have a very flexible layout system that supports the wide range of screen sizes and resolutions of Android devices.

Unlike the storyboard editor in iOS, you can edit the layouts in either visual mode, as shown above, or an XML-based editor. Simply use the tabs at the bottom of the layout editor to switch between the two views. As the layouts become more complex, being able to edit the layout files directly comes in handy. A snippet of layout XML looks like this:

<pre><code class="language-markup">
&lt;RelativeLayout xmlns:android="https://schemas.android.com/apk/res/android"
                xmlns:tools="https://schemas.android.com/tools"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                tools:context=".MainActivity" &gt;

    &lt;EditText
            android:id="@+id/billAmtEditText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentTop="true"
            android:layout_centerHorizontal="true"
            android:layout_marginTop="20dp"
            android:ems="10"
            android:gravity="right|center_vertical"
            android:hint="@string/billAmount"
            android:inputType="number|numberSigned|numberDecimal" &gt;
        &lt;requestFocus /&gt;
    &lt;/EditText&gt;

    &lt;Button
            android:id="@+id/calcTipButton"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@+id/billAmtEditText"
            android:layout_centerHorizontal="true"
            android:layout_marginTop="19dp"
            android:text="@string/calculateTip" /&gt;

    &lt;TextView
            android:id="@+id/TextView01"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignLeft="@+id/billAmtEditText"
            android:layout_below="@id/calcTipButton"
            android:layout_marginTop="18dp"
            android:text="@string/tipPercentage"
            android:textAppearance="?android:attr/textAppearanceMedium"/&gt;
&lt;/RelativeLayout&gt;
</code></pre>

## Android Resources: Support For Various Device Capabilities

The Android SDK was designed from the outset to support a wide variety of device capabilities. Much has been written about the “fragmentation” of devices on the Android platform. However, from the beginning, the Android SDK was designed to support this variety of device attributes, including screen size, pixel density and Android API versions.

Screen layouts, image assets (called drawables), styles and other configuration files are all incorporated in a series of subdirectories underneath a master “resource” directory. The <a href="https://developer.android.com/guide/topics/resources/providing-resources.html#AlternativeResources">Android SDK documentation</a> illustrates how multiple versions of the same file can be placed in uniquely named directories within this resource structure, so that the proper one is loaded depending on the capabilities and orientation of the device at runtime.

Consider this directory structure:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955d168b-1de5-4345-b98a-cdb98f04ad55/android-file-structure-opt.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139878" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/955d168b-1de5-4345-b98a-cdb98f04ad55/android-file-structure-opt.png" alt="android-file-structure" width="283" height="546" /></a>

The structure above shows <strong>uniquely named directories for drawable assets</strong>, with suffixes of <code>-hdpi</code>, <code>-ldpi</code>, <code>-mdpi</code> and so on. This permits the developer to supply different image content to correspond with the DPI resolution of a given screen. Similar capabilities extend to things like the layout files, which may supply unique content according to screen size, landscape or portrait orientation, etc. In the example above, we see unique folders for <code>values-v11</code> and <code>values-v14</code>. This allows for two different <code>styles.xml</code> files to be used for version 11 (Android 3.x) and version 14 (Android 4.x) of the Android operating system.

Note, also, the regular <code>values</code> directory. Android versions prior to version 11 would obtain their <code>styles.xml</code> from this directory. This fallback mechanism is in place for all resources. The SDK will attempt to find the resource in the particular directory and then fall back to a more “generic” resource if it’s not available. All of this occurs without the developer having to write any special code. Simply drop the resources into the proper directories, and the Android runtime will take care of the rest. Each of your resources <a href="https://developer.android.com/guide/topics/resources/accessing-resources.html">may be accessed</a> from both the XML and Java files in your application.

The resource system is quite powerful and supports <a href="https://developer.android.com/guide/topics/resources/available-resources.html">many types of resources</a>. In addition to the drawable, layout, menu and styles for your application, it can also be used to hold <a href="https://developer.android.com/guide/topics/resources/more-resources.html">application constants</a> for arrays or dimensional values in your application. In this manner, you can load different constant values for various device configurations simply by placing the files in the proper directory structure. You can also use this system to support <a href="https://developer.android.com/guide/topics/resources/localization.html">localization</a>. This is accomplished through the <code>strings.xml</code> file. Here’s an example of the <code>strings.xml</code> file associated with our application:

<pre><code class="language-markup">
&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;resources&gt;
    &lt;string name="app_name"&gt;FasTip&lt;/string&gt;
    &lt;string name="hello_world"&gt;Hello World!&lt;/string&gt;
    &lt;string name="menu_settings"&gt;Settings&lt;/string&gt;
    &lt;string name="billAmount"&gt;Bill Amount&lt;/string&gt;
    &lt;string name="calculateTip"&gt;Calculate Tip&lt;/string&gt;
    &lt;string name="tipAmount"&gt;Tip Amount&lt;/string&gt;
    &lt;string name="totalAmount"&gt;Total Amount&lt;/string&gt;
    &lt;string name="title_activity_settings"&gt;Settings&lt;/string&gt;
    &lt;string name="saveSettings"&gt;Save Settings&lt;/string&gt;
    &lt;string name="tipPercentage"&gt;Tip Percentage&lt;/string&gt;
    &lt;string name="percentSymbol"&gt;%&lt;/string&gt;
&lt;/resources&gt;
</code></pre>

The base string file is placed in the <code>res/values</code> directory of the application. If you wanted to offer a Spanish version of the same file, you would place it in the <code>res/values-es</code> directory.</p>

### Resource IDs

In the process of defining the layouts, you should <strong>associate an ID value with each control</strong> (or UI widget) that you wish to reference from code. This can be done by specifying an ID value in the properties inspector in the layout editor:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd832912-1d9e-41a9-b899-46fe11134e94/android-eclipse-id-property.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139872" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ffda244b-b16f-45ac-a1af-41e283770b83/android-eclipse-id-property-500-opt.jpg" alt="android-eclipse-id-property-500" width="500" height="352" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd832912-1d9e-41a9-b899-46fe11134e94/android-eclipse-id-property.png">Large view</a>)</em>

## Layout Managers

Android <a href="https://developer.android.com/guide/topics/ui/declaring-layout.html">layout</a> files may use a number of layout managers, or ViewGroups, to arrange the controls on the screen. This is Android’s approach to laying out views, much like the constraints system we saw in iOS. <strong>Here are some of the more common ViewGroups used in Android apps</strong>:

*   [LinearLayout](https://developer.android.com/guide/topics/ui/layout/linear.html) This is used to lay out a series of controls in either horizontal or vertical orientation.
*   [RelativeLayout](https://developer.android.com/guide/topics/ui/layout/relative.html) This is used to position controls relative to one another or to the bounds of their parents’ layout. This is a flexible layout system and is often used as an alternative to nesting linear layouts.
*   [ListView](https://developer.android.com/guide/topics/ui/layout/listview.html) This is a view group that presents a series of vertically scrolling items, much like a `UITableView` for those familiar with iOS. In Android, you write a [ListAdapter](https://developer.android.com/reference/android/widget/ListAdapter.html) to provide a view for each row of data in a data source.
*   [GridView](https://developer.android.com/guide/topics/ui/layout/gridview.html) This is similar to a list view, but it provides items in a two-dimensional, scrollable grid. Just like the list view, it also uses an adapter to provide view contents for each cell in the grid.

In our sample application, two layout files have been created: <code>activity_main.xml</code> for the main screen and <code>activity_settings.xml</code> for the settings screen. So far, we’ve just defined the appearance of things. Unlike the iOS storyboard editor, Android has no “assistant” tool to directly link the controls in the visual layout editor to the code. We’ll need to write some code to connect these components together and build the application.</p>

## Android: Activities And Intents

In iOS, we loaded the logic specific to a given screen into a <code>ViewController</code>. In Android, these separate screens are treated as separate “activities.” Just like in an iOS <code>UIViewController</code>, there is a defined life cycle for an activity that governs when the activity starts, pauses, resumes and stops.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20d06077-5ceb-47d6-b66e-099989c6ec50/activity-lifecycle-500-opt.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139866" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/20d06077-5ceb-47d6-b66e-099989c6ec50/activity-lifecycle-500-opt.png" alt="activity-lifecycle" width="513" height="663" /></a>

The diagram above comes straight from the Android <a href="https://developer.android.com/guide/components/activities.html#Lifecycle">Developers documentation</a> and shows the lifecycle of an activity. It’s up to the developer to place code in the various methods of the activity to respond to the various states of the lifecycle.

<pre><code class="language-clike">
@Override
protected void onCreate(Bundle savedInstanceState) {

    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    tipPctTextView = (TextView)this.findViewById(R.id.tipPctTextView);
    tipAmountTextView = (TextView)this.findViewById(R.id.tipAmtTextView);
    totalAmountTextView = (TextView)this.findViewById(R.id.totalAmtTextView);
    calcTipAmountButton = (Button)this.findViewById(R.id.calcTipButton);
    billAmountTextView = (EditText)this.findViewById(R.id.billAmtEditText);

    calcTipAmountButton.setOnClickListener(new OnClickListener() {
        @Override
        public void onClick(View v) {
            calculateTip();
        }
    });
}
</code></pre>

The code above is executed early on in the activity’s lifecycle. In this case, we are loading the layout file that was defined earlier, via this statement:

<pre><code class="language-clike">
setContentView(R.layout.activity_main);
</code></pre>

Upon successfully loading the layout, we obtain references to the various controls that make up the layout. Notice that we are referencing the layouts and the IDs via the <code>R.</code> notation. <strong>These are the resource IDs that we defined earlier in the layout manager.</strong> Additionally, we attach a click listener to define what code should run when the user taps on the “Calculate Tip” button.

In the iOS example, we used <code>NSUserDefaults</code> to save and restore the user’s preference for a tip percentage. In Android, the equivalent is <a href="https://developer.android.com/guide/topics/data/data-storage.html#pref">sharedPreferences</a>. This can be seen in the code snippet below, where we restore the persisted value for <code>tipPercentage</code> in the local variable <code>tipPctString</code>. Notice that the first time the user runs this app, a default value of <code>15.0</code> is used.

<pre><code class="language-clike">
private void loadTipPercentage() {
    SharedPreferences preferences =
                this.getSharedPreferences("AppPreferences", MODE_PRIVATE);
    String tipPctString = preferences.getString("tipPercentage", "15.0");
    tipPctTextView.setText(String.format("%s%%", tipPctString));
    tipPercentage = Double.parseDouble(tipPctString) / 100;
}
</code></pre>

### Defining a Menu for Our Activity

Android applications do not use the <code>NavigationController</code> approach of iOS applications. In Android 4.x devices, the choices that appear in the upper-right of the screen are part of the Android “<a href="https://developer.android.com/guide/topics/ui/actionbar.html">action bar</a>.”

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c310713-13fc-4735-b1d5-ceeb01817d51/android-action-bar-500-opt.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="140378" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c310713-13fc-4735-b1d5-ceeb01817d51/android-action-bar-500-opt.png" alt="android-action-bar" width="480" height="270" /></a><br>
<em>The action bar is the dark header in this screenshot. Note the settings button in the upper-right, which is defined by the menu.</em>

We populate the action bar by defining a series of <a href="https://developer.android.com/guide/topics/ui/menus.html">menu options</a> in an XML file, just as we did with the screen layout. The menu is placed in a menu directory within the resources directory. Here are the contents of the menu file used on the main screen of our application:

<pre><code class="language-markup">
&lt;menu xmlns:android="https://schemas.android.com/apk/res/android" &gt;
    &lt;item
        android:id="@+id/menu_settings"
        android:orderInCategory="100"
        android:showAsAction="ifRoom"
        android:title="@string/menu_settings"
        android:icon="@android:drawable/ic_menu_preferences"/&gt;
&lt;/menu&gt;
</code></pre>

Note that, in this case, we have just one menu option to access the settings screen. If more options were placed in the menu than could fit on the screen, then the remaining items would flow into a drop-down menu, accessible via the three vertical dots often seen in Android menus. To use the menu in our activity, we must load it at the correct time. This is done in the <code>onCreateOptionsMenu</code> method:

<pre><code class="language-clike">
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    // Inflate the menu; this adds items to the action bar if it is present.
    getMenuInflater().inflate(R.menu.activity_main, menu);
    return true;
}

// Respond to menu selections
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    // Handle item selection
    switch (item.getItemId()) {
        case R.id.menu_settings:
            this.startSettings();
            return true;
        default:
            return super.onOptionsItemSelected(item);
    }
}
</code></pre>

Notice how the <code>onOptionsItemSelected</code> method is used to determine what code is run when a given menu option is chosen.</p>

## Starting Another Activity

As we’ve seen from the code above, when the user chooses the settings icon from the action bar, the <code>startSettings()</code> method is invoked. This is the code that launches the second activity to display the settings screen:

<pre><code class="language-clike">
private void startSettings() {
    Intent settingsIntent = new Intent();
    settingsIntent.setClass(this, SettingsActivity.class);
    startActivity(settingsIntent);
}
</code></pre>

Android launches activities via an <a href="https://developer.android.com/guide/components/intents-filters.html">intent</a> object. In this simple example, we are creating a very specific intent to launch the <code>SettingsActivity</code> class, which contains the code to load and drive the settings screen. Most Android applications use this technique to move the user from one screen to the next in an application.</p>

### Using Intents for App Integration

Intents are considerably more flexible than this. It’s possible to use intents to launch a variety of activities. A common intent is to send an item to be shared via social networking apps. If you’ve used an Android device before, then you’ll know that doing something like this typically brings up a menu of applications that support a sharing intent. This list often contains applications such as Facebook and Twitter.

[![android-share-list-338](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d0829c0-70aa-4b61-b365-806f44d0b586/android-share-list-338-opt.jpg)](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5f24dbd0-2d81-431d-a85f-c55b800db785/android-share-list.png)

This particular sharing intent is known as <a href="https://developer.android.com/reference/android/content/Intent.html#ACTION_SEND">ACTION_SEND</a>. All of the applications that support sharing are listening for a common intent. <strong>When an Android application is installed on a device, its manifest file describes the intents it can process.</strong> In this way, several applications may be installed, each of which supports the same intent.

If only one application supports the intent, then that activity is immediately launched. Whereas if multiple applications are installed for the same intent, then Android would show a menu of options, from which the user would make a selection before the intent is sent to the chosen activity.

The intent system in Android is a unique feature that can be used to create workflows across several applications. When building for the Android platform, you should keep this capability in mind because it offers a way to integrate your application with others.</p>

## The Settings Screen

Much of what occurs here has already been covered in the section on the main activity. This activity has similar code in the <code>onCreate</code> method to load the appropriate layout file and obtain references to the controls. When the “Save Settings” button is pressed, the following code is run to save the tip percentage value to storage:

<pre><code class="language-clike">
private void saveSettings() {
    if (validateSettings()) {
        SharedPreferences preferences =
            this.getSharedPreferences("AppPreferences", MODE_PRIVATE);
        SharedPreferences.Editor prefEditor = preferences.edit();
        prefEditor.putString("tipPercentage",
            tipPercentageEditText.getText().toString());
        prefEditor.commit();
        this.finish();
    }
}
</code></pre>

Notice that the last line in the <code>saveSettings</code> method calls the <code>finish()</code> method. This causes the current activity to stop running and returns the user to the prior activity, which in our case is the main screen. Contrast this with iOS’ use of the <code>NavigationController</code> and the way we popped the current view controller off the stack of view controllers.</p>

## Running Your Application

Android provides two basic ways to test an application: in the Android emulator or on a regular device such as a phone or tablet. Unlike with iOS, you don’t have to pay any fees to deploy your app to your own device or to share it with other Android users. The only fee that is required is if you wish to <a href="https://developer.android.com/distribute/googleplay/publish/register.html">feature your app in Google Play</a>.

The emulator enables you to emulate a variety of Android versions, as well as different screen aspect ratios and resolutions. While testing your application on a real device is always a good idea, the emulator helps you to test on device configurations that are not readily available.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67ddacff-fa9e-47c2-bd81-92da290f4120/android-emulator-opt.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139876" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67ddacff-fa9e-47c2-bd81-92da290f4120/android-emulator-opt.jpg" alt="android-emulator" width="389" height="350" /></a>

<strong>To use the emulator, you must create an Android Virtual Device (AVD).</strong> Think of this as a virtual phone or tablet. Creating multiple AVDs, each with a unique configuration, is possible to test your app on different screen sizes and memory capacities. Android Developers provides details on how to <a href="https://developer.android.com/tools/devices/managing-avds.html">use the AVD manager</a> to set up these devices.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f0d97d0-0afc-4204-94e5-70497bb7f865/android-avd-manager-500-opt.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139869" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9f0d97d0-0afc-4204-94e5-70497bb7f865/android-avd-manager-500-opt.jpg" alt="android-avd-manager" width="438" height="291" /></a>

### Use Hardware Virtualization to Speed Up That Slow Emulator

The Android emulator has long been maligned for its poor performance on many machines. This is because, in the past, the emulator has been running actual code compiled for the ARM processor on a phone, rather than for the x86 CPU that’s likely on your development machine.

Recently, an x86 <a href="https://developer.android.com/tools/devices/emulator.html#accel-vm">hardware-virtualized</a> version has been made available. This version starts up and runs considerably faster than the traditional emulator. The hardware-virtualized version will generally run on a Windows or Mac OS X machine with an Intel Core i3 or later processor that supports hardware virtualization. AMD processors are currently supported only on Linux.

Creating an AVD that uses hardware virtualization requires that you set up Intel’s HAXM support first. The developer documentation provides <a href="https://developer.android.com/tools/devices/emulator.html#accel-vm">details on the process</a> to follow for your operating system. Make sure that you are running the <a href="https://software.intel.com/en-us/articles/intel-hardware-accelerated-execution-manager/">latest HAXM support</a>; if you’re on Mac OS X Mavericks, a recently released hotfix resolves issues there as well.</p>

### Testing on a Device

To test the application on your own device, you’ll need to enable USB debugging on the device. Google provides detailed instructions on <a href="https://developer.android.com/tools/device.html#setting-up">setting up your device</a> for debugging.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8f1c5ba-9c70-4137-b331-162188e33bed/android-usb-debug-opt.jpg"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139883" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e8f1c5ba-9c70-4137-b331-162188e33bed/android-usb-debug-opt.jpg" alt="android-usb-debug" width="304" height="541" /></a>

For Android 4.0 devices, go to <code>Settings → Developer Options</code> in the menu and you’ll see a checkbox to enable this. If you’re on Windows, you might need to install some USB drivers for your device; these can usually be downloaded from the manufacturer’s website. For Mac OS X, you usually will not need any drivers and can just plug in the device via a USB cable.

The Eclipse IDE provides a “targets” option that enables you to specify which device, or AVD, should be used to run your application. This can be found in <code>Run → Run Configurations</code> and <code>Run → Debug Configurations</code> in the menu. The “Targets” tab allows you to select which AVD should be used by default or to set a prompt each time to select a run or debug destination for the application:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3a953db7-5a73-4ce0-b863-8def441fb4a8/android-run-target.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139881" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e9744d5-cc09-4538-ad31-63946e19571a/android-run-target-500-opt.jpg" alt="android-run-target-500" width="500" height="397" /></a>

If you select “Always prompt to pick device,” then the IDE will present this dialog each time you choose to run or debug the application:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1ae0bcd-9335-444a-88f1-6a069e3c9790/android-device-chooser.png"><img loading="lazy" decoding="async"  loading="lazy" decoding="async" class="139870" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5dcce61b-5ad6-42f1-8468-f11d0f223db5/android-device-chooser-500-opt.jpg" alt="android-device-chooser-500" width="500" height="361" /></a>

Every time you run or debug the application, an APK file is built and written to the <code>/bin</code> directory of your project’s root directory. This is the application distribution package used for Android devices. It’s analogous to the IPA file for iOS applications. When you select a deployment target via the process above, the Android development tools will automatically install the APK on the target device or emulator and run it.</p>

## Sharing Your Application With Others

Submitting an application to Google Play is beyond the scope of this article. The documentation provides an <a href="https://developer.android.com/tools/publishing/publishing_overview.html">overview</a> of the process. You can also use the <a href="https://developer.android.com/tools/publishing/app-signing.html#ExportWizard">export wizard</a> in Eclipse to export an APK file. The resulting APK file can then be shared with others outside of Google Play via <a href="https://developer.android.com/distribute/open.html">open distribution</a>, and it is very useful when sharing copies of your application for testing prior to general release.</p>

## Android: Learning Resources

As with iOS, some excellent resources exist for getting started with Android. I recommend the following books and websites:

*   [_The Busy Coder’s Guide to Android Development_](https://commonsware.com/Android/), Mark L. Murphy This book is comprehensive, and the writing style is easy to follow. The author even offers a [free version](https://commonsware.com/Android/Android_3-6-CC.pdf) of the book based on an earlier version (Android 3.x) of the SDK.
*   [_Beginning Android 4 Application Development_](https://www.amazon.com/Beginning-Android-Application-Development-ebook/dp/B0075Y61NY/), Wei-Meng Lee For those looking for a shorter book, this does a good job of covering the basics, without as much detail or scope as Murphy’s book above.
*   [Vogella](https://www.vogella.com/android.html) This series of brief tutorials shows how to perform common operations in Android applications.
*   [Android Weekly](https://androidweekly.net/) This weekly newsletter will help you stay current on new blog posts and libraries of interest to the Android development community.</p>

### Summary

That wraps up our coverage of developing a native app for Android. We’ve seen some unique capabilities of the platform, such as the resource system, layouts, and the way that activities and intents work together. <a href="https://www.smashingmagazine.com/2014/02/four-ways-to-build-a-mobile-app-part3-phonegap/">In the next article</a>, we’ll take the tip calculator cross-platform, looking at what’s involved in developing our app for both iOS and Android using PhoneGap.

{{< signature "al, ea, il" >}}


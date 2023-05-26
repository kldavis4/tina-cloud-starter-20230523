---
title: 'From Zero To Appium: A How-To Guide For Configuring Appium With Android'
slug: from-zero-to-appium-guide-configuring-appium-android
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d69bcabc-25ef-427d-b3f1-24a3d4eab8a1/appium-architecture-preview-opt-1.png
date: 2016-04-28T21:12:27.000Z
author: antonioroavalverde
description: >-
  If you are a web developer who cares about quality, most probably you have
  heard of Selenium and the advantages of using such a tool for test automation.
  Now, if you are a mobile developer, you might know how much harder it is to
  test your app due to the existence of different platforms, different OS
  versions and even variety of devices.
categories:
  - Mobile
  - Android
---
If you are a web developer who cares about quality, most probably you have heard of Selenium and the advantages of using such a tool for test automation. (Check out my <a href="https://www.6020peaks.com/2015/12/how-to-build-a-test-automation-solution-for-your-web-projects/">article</a> on how to run your own continuous integration solution with Selenium).

Now, if you are a mobile developer, you might know how much harder it is to test your app due to the existence of different platforms, different OS versions and even variety of devices. Imagine how great it would be to write your tests only once and run them on different platforms. If so, then <strong>maybe today is your lucky day</strong>, because I want to tell you about <a href="https://appium.io">Appium</a>, a tool inspired by the Selenium WebDriver that allows you to write tests against multiple platforms using the same API.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [What Every App Developer Should Know About Android](https://www.smashingmagazine.com/2014/10/what-every-app-developer-should-know-about-android/)
*   [Diverse Test-Automation Frameworks For React Native Apps](https://www.smashingmagazine.com/2016/08/test-automation-frameworks-for-react-native-apps/)
*   [The Basics Of Test Automation For Apps, Games And The Mobile Web](https://www.smashingmagazine.com/2015/01/basic-test-automation-for-apps-games-and-mobile-web/)
*   [The Art Of Layout Testing With Galen Framework](https://www.smashingmagazine.com/2016/06/the-art-of-layout-testing-with-galen-framework/)

In short, Appium allows you to automatically interact with your app by exploiting the behavior of the components available in the user interface (buttons, lists, text labels, etc.). This mechanism can be reused to write tests that must be run repeatedly against the app. This kind of testing is known as functional testing, or black box testing in the literature, because it checks that the software does what the specification says without caring about the implementation details.

{{% feature-panel %}}

The biggest advantage of automating your tests is the speed at which they can be executed and the amount of time saved from avoiding manual repetition.

Tools for writing automation tests for Appium already exist; however, they are all platform-dependent. This means that if you have an app running on Android and on iOS, you would need to write the same test for each platform. The extra value provided by Appium is the possibility of running a test that shares the same code on every platform.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b6d6bae-e617-4e96-b9d1-79fa542b8207/appium-architecture-opt.png"><img loading="lazy" decoding="async"  src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec3a18cb-f440-4c05-9dd7-d8144e29a437/appium-architecture-preview-opt.png" alt="appium-architecture-preview-opt" width="500" height="191" /></a><figcaption>Appium architecture. (Image credit: <a href="https://www.6020peaks.com">www.6020peaks.com</a>) (<a href="https://test.smashingmagazine.com/wp-content/uploads/2016/04/appium-architecture-opt.png">View large version</a>)</figcaption></figure>

The philosophy behind Appium stems from the <a href="https://appium.io/introduction.html">following principles</a>:

*   You shouldn't have to recompile your app or modify it in any way in order to automate it.
*   You shouldn't be locked into a specific language or framework to write and run your tests.
*   A mobile automation framework shouldn't reinvent the wheel when it comes to automation APIs.
*   A mobile automation framework should be open source, in spirit and practice as well as in name!

Appium is a great tool; however, installing it might be a little cumbersome. In this tutorial, we’ll show you all of the steps required to successfully <a href="#appium-installation">install Appium</a> on an Ubuntu server. We encountered several issues during installation and couldn’t find a proper step-by-step tutorial; so, we hope this article solves that problem and saves you some headaches.</p>

<strong>Disclosure:</strong> I am not related to the Appium team in any way. All comments should be considered the personal opinion of a user who has been struggling with Android tests for a while and was expecting something like Selenium for the mobile world.

Appium requires a mobile platform to be installed in order for us to execute our tests. So, using Appium for testing an iOS app requires a machine <a href="https://stackoverflow.com/questions/33529495/is-it-possible-to-run-appium-ios-automated-tests-on-ubuntu">running Mac OS X and Xcode</a>. In this tutorial, we’ll focus uniquely on the Android platform, and we will show you in detail how to <a href="#appium-android-headless">set up a headless installation of Android</a>.

Finally, we will explain all of the configuration needed to <a href="#appium-python">run Appium tests with Python</a>. Note that this section is included for the sake of testing the installation and not for exploring all of Appium’s features. The topic of testing with Appium will be covered in a future article.</p>

## Install Appium

For this tutorial, we will rely on an Ubuntu 14.04 server distribution. Note that our aim is to build a system that helps us run mobile tests in a headless fashion (i.e. without requiring a physical display). So, we will assume the following requirements as our starting point.</p>

### Requirements

*   Ubuntu 14.04
*   Python (version 2.7.6 in this tutorial)
*   pip

Before we are able to run Appium, we need to make sure that the following tools are accessible in our system.</p>

### Summary of Tools Required by Appium

*   Java SDK 1.7 The openjdk-7-jdk package must be installed. Do not confuse it with openjdk-7-jre, which contains just the Java runtime environment.
*   [Apache Ant](https://ant.apache.org/) Java version of GNU make for building Java applications
*   [Apache Maven](https://maven.apache.org/) Java dependency management and build system
*   [RVM](https://rvm.io) Ruby Version Manager
*   [gem](https://rubygems.org/) Ruby package manager
*   [bundler](https://bundler.io/) Ruby dependency manager
*   [Node.js](https://nodejs.org/) JavaScript runtime
*   [npm](https://www.npmjs.com/) Node.js package manager
*   [grunt](https://gruntjs.com/) JavaScript task runner

These tools can be installed by following the next steps.</p>

### Step 0

Before you download the tools, we suggest creating a folder in your home directory that will be used to keep the files and later create the required environment variables in your path. For example, we are using a folder named <code>workspace</code>.</p>

### 1. Install Java

<pre><code class="language-bash">
$ sudo apt-get install openjdk-7-jdk
</code></pre>

Appium requires the <code>JAVA_HOME</code> variable and Java in your path. In order to do so, edit the <code>.bashrc</code> file:

<pre><code class="language-bash">
$ vim .bashrc
     export JAVA_HOME="/usr/lib/jvm/java-7-openjdk-amd64"
     export PATH="$PATH:$JAVA_HOME"
$ source .bashrc
</code></pre>

Run the following command to check whether Java is accessible:

<pre><code class="language-bash">
$ java -version
</code></pre>

You should get the following output in your terminal:

<pre><code class="language-bash">
java version "1.7.0_95"
OpenJDK Runtime Environment (IcedTea 2.6.4) (7u95-2.6.4-0ubuntu0.14.04.1)
OpenJDK 64-Bit Server VM (build 24.95-b01, mixed mode)
</code></pre>

### 2. Install Apache Ant

Move to the workspace folder that we created in step 0 and download the <a href="https://ant.apache.org/bindownload.cgi#Current%20Release%20of%20Ant">latest version of Apache Ant</a> (which is 1.9.6 at the time of writing):

<pre><code class="language-bash">
$ wget https://www.eu.apache.org/dist//ant/binaries/apache-ant-1.9.6-bin.tar.gz
</code></pre>

When that’s done, just uncompress the file and delete the original <code>.tar.gz</code> folder since we won’t need it anymore.</p>

<pre><code class="language-bash">
$ tar -xvzf apache-ant-1.9.6-bin.tar.gz
$ rm apache-ant-1.9.6-bin.tar.gz
</code></pre>

Now you will have a folder named <code>apache-ant-1.9.6</code> in your workspace folder. Use that folder to create the <code>ANT_HOME</code> in your <code>.bashrc</code> file:

<pre><code class="language-bash">
$vim .bashrc
     export ANT_HOME="$HOME/workspace/apache-ant-1.9.6"
     export PATH="$PATH:$ANT_HOME/bin" # Add ant to PATH
$source .bashrc
</code></pre>

From the <code>ANT_HOME</code> directory, run the following:

<pre><code class="language-bash">
$ ant -f fetch.xml -Ddest=system
</code></pre>

This will get the library dependencies of most of the Ant tasks that require them. If you don't do this, many of the dependent Ant tasks will not be available.</p>

### 3. Install Apache Maven

In your workspace folder, download the <a href="https://maven.apache.org/download.cgi">latest version of Apache Maven</a> (which is 3.3.9 at the time of writing):

<pre><code class="language-bash">
$ wget https://www.us.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
$ tar -xvzf apache-maven-3.3.9-bin.tar.gz
</code></pre>

Delete the <code>.tar.gz</code> file:

<pre><code class="language-bash">
$ rm apache-maven-3.3.9-bin.tar.gz
</code></pre>

Create the <code>MAVEN_HOME</code> variable and add it to the path:

<pre><code class="language-bash">
$ vim .bashrc
     export MAVEN_HOME="$HOME/workspace/apache-maven-3.3.9"
     export PATH="$PATH:$MAVEN_HOME/bin"
$source .bashrc
</code></pre>

Then, run the following command from the terminal to check that Maven has been properly configured:

<pre><code class="language-bash">
$mvn -v
</code></pre>

If everything is fine, you should get the following output:

<pre><code class="language-bash">
Apache Maven 3.3.9 (bb52d8502b132ec0a5a3f4c09453c07478323dc5; 2015-11-10T17:41:47+01:00)
Maven home: /home/6020peaks/workspace/apache-maven-3.3.9
Java version: 1.7.0_91, vendor: Oracle Corporation
Java home: /usr/lib/jvm/java-7-openjdk-amd64/jre
Default locale: en_US, platform encoding: ANSI_X3.4-1968
OS name: "linux", version: "3.13.0-74-generic", arch: "amd64", family: "unix"
</code></pre>

### 4. Install RVM

From a terminal, install the <a href="https://keybase.io/mpapis">mpapis public key</a>. You’ll need it to avoid errors while downloading RVM.</p>

<pre><code class="language-bash">
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
</code></pre>

Then, proceed to install RVM with Ruby:

<pre><code class="language-bash">
$ \curl -sSL https://get.rvm.io | bash -s stable --ruby
</code></pre>

Once this is done, proceed to update RubyGems and Bundler:

<pre><code class="language-bash">
$ gem update --system
$ gem install --no-rdoc --no-ri bundler
$ gem update
$ gem cleanup
</code></pre>

### 5. Install Node.js

The first rule for installing Node.js the right way is to avoid using <code>apt-get</code>, or else it will need <code>sudo</code> grants, and Appium will not work correctly. Instead, install <a href="https://github.com/Linuxbrew/linuxbrew">Linuxbrew</a>, and then install Node.js from it. In short, Linuxbrew is a package manager for Linux forked from the original <a href="https://brew.sh">Homebrew</a> for Mac OS X.

You can install Linuxbrew on Ubuntu by running the following commands. First, install the Linuxbrew dependencies:

<pre><code class="language-bash">
$ sudo apt-get install build-essential curl git m4 python-setuptools ruby texinfo libbz2-dev libcurl4-openssl-dev libexpat-dev libncurses-dev zlib1g-dev
</code></pre>

Then, install Linuxbrew by running this:

<pre><code class="language-bash">
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/linuxbrew/go/install)"
</code></pre>

Once installed, add <code>brew</code> to your path:

<pre><code class="language-bash">
$ vim .bashrc
$ export PATH="$PATH:$HOME/.linuxbrew/bin"
$ source .bashrc
$ brew doctor
</code></pre>

Now you are in shape to install Node.js from <code>brew</code>:

<pre><code class="language-bash">
$ brew install node
</code></pre>

Note that this step can take a bit of time, so please be patient and do not close the terminal. Once the process is done, check that Node.js and npm have been successfully installed by running the following:

<pre><code class="language-bash">
$ node --version
$ npm --version
</code></pre>

### 6. Install Grunt

Simply run the following command in the terminal, and npm will take care of everything:

<pre><code class="language-bash">
$ npm install -g grunt grunt-cli
</code></pre>

### 7. Install Appium

The latest Appium release is <a href="https://github.com/appium/appium/releases/tag/v1.5.0">1.5.0</a>, freshly baked as we write this tutorial and which, according to the developers on GitHub, introduces big changes from previous versions. One of these changes affects the way Appium is configured during installation; specifically, the <code>reset.sh</code> script we refer to below has been removed in version 1.5.0. Until this latest version gets enough feedback from the community, we suggest starting with the stable release, <a href="https://github.com/appium/appium/releases/tag/v1.4.16">1.4.16</a>.</p>

<strong>Note:</strong> In this section, we’ll work with version 1.4.16 of Appium, but all of the information in this tutorial applies independent of the version.

To install version 1.4.16, change the directory to the workspace folder you created at the beginning, and then download the source code from GitHub:

<pre><code class="language-bash">
$ wget https://github.com/appium/appium/archive/v1.4.16.tar.gz
$ tar -xvzf appium-1.4.16.tar.gz
$ rm appium-1.4.16.tar.gz
$ mv appium-1.4.16 appium
</code></pre>

Now, this stage is where the official Appium documentation gets confusing. According to the documentation, the next steps are to run the following commands to execute a collection of scripts that will set up Appium so that you can start it and test your app with it.</p>

<pre><code class="language-bash">
$ cd appium;
$ ./reset.sh —android  --verbose
</code></pre>

However, the documentation assumes that Android is already perfectly configured in your environment and ready for Appium. If that is the case, then you should not have any problem; otherwise, proceed with our instructions in the next section.</p>

## Set Up A Headless Installation Of Android

Because we are aiming to build a headless configuration for our test automation system, all of the instructions that follow are restricted to the terminal. Even though it is a bit more tedious than using the GUI, the advantage is that you can use commands to build your own script to automate the installation process.

The first step is to install the <a href="https://developer.android.com/sdk/index.html#Other">latest Android SDK for Linux</a>. Switch to your workspace folder and run the following commands:

<pre><code class="language-bash">
$ wget https://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
$ tar -xvzf android-sdk_r24.4.1-linux.tgz
$ rm android-sdk_r24.4.1-linux.tgz
</code></pre>

Then, create the <code>ANDROID_HOME</code> variable in <code>.bashrc</code>, and add <code>tools</code> and <code>platforms_tools</code> to the path:

<pre><code class="language-bash">
export ANDROID_HOME="$HOME/workspace/android-sdk-linux"
export PATH="$PATH:$ANDROID_HOME/tools"
export PATH="$PATH:$ANDROID_HOME/platform-tools"
</code></pre>

Refresh your environment so that the new variables are recognized by your terminal:

<pre><code class="language-bash">
$ source .bashrc
</code></pre>

Once the Android SDK is ready, the next step is to install the Android APIs that our apps will target in the tests. Note that Appium requires API level 17 or above in order to work properly.

Run the following command to see the list of available packages:

<pre><code class="language-bash">
$ android list sdk --all
</code></pre>

This will render a list like the following (edited for brevity):

<pre><code class="language-bash">
Refresh Sources:
  Fetching https://dl.google.com/android/repository/addons_list-2.xml
  Validate XML
  Parse XML
  Fetched Add-ons List successfully
  Refresh Sources
  Fetching URL: https://dl.google.com/android/repository/repository-11.xml
  Validate XML: https://dl.google.com/android/repository/repository-11.xml
==== shorted ====
Packages available for installation or update: 160
   1- Android SDK Tools, revision 24.4.1
   2- Android SDK Tools, revision 25.0.5 rc6
   3- Android SDK Platform-tools, revision 23.1
   4- Android SDK Build-tools, revision 23.0.2
   5- Android SDK Build-tools, revision 23.0.1
   6- Android SDK Build-tools, revision 23 (Obsolete)
==== shorted ====
  26- SDK Platform Android 6.0, API 23, revision 2
  27- SDK Platform Android 5.1.1, API 22, revision 2
  28- SDK Platform Android 5.0.1, API 21, revision 2
  29- SDK Platform Android 4.4W.2, API 20, revision 2
  30- SDK Platform Android 4.4.2, API 19, revision 4
  31- SDK Platform Android 4.3.1, API 18, revision 3
  32- SDK Platform Android 4.2.2, API 17, revision 3
  33- SDK Platform Android 4.1.2, API 16, revision 5
  34- SDK Platform Android 4.0.3, API 15, revision 5
  35- SDK Platform Android 4.0, API 14, revision 4 (Obsolete)
  36- SDK Platform Android 3.2, API 13, revision 1 (Obsolete)
  37- SDK Platform Android 3.1, API 12, revision 3 (Obsolete)
  38- SDK Platform Android 3.0, API 11, revision 2 (Obsolete)
  39- SDK Platform Android 2.3.3, API 10, revision 2
  40- SDK Platform Android 2.3.1, API 9, revision 2 (Obsolete)
  41- SDK Platform Android 2.2, API 8, revision 3
  42- SDK Platform Android 2.1, API 7, revision 3 (Obsolete)
  43- SDK Platform Android 2.0.1, API 6, revision 1 (Obsolete)
  44- SDK Platform Android 2.0, API 5, revision 1 (Obsolete)
  45- SDK Platform Android 1.6, API 4, revision 3 (Obsolete)
  46- SDK Platform Android 1.5, API 3, revision 4 (Obsolete)
  47- SDK Platform Android 1.1, API 2, revision 1 (Obsolete)
==== shorted ====
</code></pre>

The most important part of this list is the first number at the beginning of each line, because this is the identification number of the package that we want to install. You can install one or more packages at the same time with the following command:

<pre><code class="language-bash">
$ android update sdk -u -a -t 1,2,3,4,..,n
</code></pre>

<strong>Important:</strong> Make sure to install API 19. We’ve detected an open issue in Appium’s source code that requires API 19 in order to create a Bootstrap project for Android. For more details, check out lines 399 to 412 of the <a href="https://github.com/appium/appium/blob/1.4/grunt-helpers.js">grunt-helpers.js file</a> on GitHub:

<pre><code class="language-javascript">
module.exports.setupAndroidBootstrap = function (grunt, cb) {
  var projPath = path.resolve(__dirname, "lib", "devices", "android",
      "bootstrap");
  var args = ["create", "uitest-project", "-n", "AppiumBootstrap", "-t",
              "android-19", "-p", "."];
  // TODO: possibly check output of `android list target` to make sure api level 19 is available?
  setupAndroidProj(grunt, projPath, args, cb);
};

module.exports.setupAndroidApp = function (grunt, appName, cb) {
  var appPath = path.resolve(__dirname, "sample-code", "apps", appName);
  var args = ["update", "project", "--subprojects", "-t", "android-19", "-p", ".", "-n", appName];
  setupAndroidProj(grunt, appPath, args, cb);
};
</code></pre>

For the next step, you need to install the application binary interface (ABI) for the Android API that you’ve installed. You can choose from among <a href="https://developer.android.com/ndk/guides/abis.html">several ABIs</a>. This is required because if your target API does not have at least one ABI installed, then you won’t be able to create an emulator for it.

In our configuration, we’ve installed armeabi-v7a for API 19. You can do this by running the same command as before but with the right package number that you see in your own listing. For example:

<pre><code class="language-bash">
$ android update sdk -u -a -t 120
</code></pre>

<strong>Note:</strong> Replace the <code>-t</code> argument (<code>120</code>) with the package number you want to install.

Now we are ready to create a new Android emulator. Check out the document “<a href="https://developer.android.com/tools/devices/managing-avds-cmdline.html">Handling AVDs From the Command Line</a>” (AVDs being Android virtual devices) for more information.

Run the following command to see which Android images are already available in your system:

<pre><code class="language-bash">
$ android list targets
</code></pre>

You should get an output like this:

<pre><code class="language-bash">
Available Android targets:
----------
id: 1 or "android-19"
     Name: Android 4.4.2
     Type: Platform
     API level: 19
     Revision: 4
     Skins: HVGA, QVGA, WQVGA400, WQVGA432, WSVGA, WVGA800 (default), WVGA854, WXGA720, WXGA800, WXGA800-7in
 Tag/ABIs : default/armeabi-v7a
</code></pre>

To create a new AVD using this target, just run the following:

<pre><code class="language-bash">
$ android create avd -n emulator-19 -t 1
</code></pre>

The parameter <code>-n</code> helps us define a name for our AVD, which will be <code>emulator-19</code> in our case. This name is important because we need to tell Appium about it later in order to run our tests. The parameter <code>-t</code> is used to select the target from the previous list. In our case, the ID is <code>1</code> or <code>android-19</code>.

Once the command is done, we should get something similar to this output:

<pre><code class="language-bash">
Auto-selecting single ABI armeabi-v7a
Android 4.4.2 is a basic Android platform.
Do you wish to create a custom hardware profile [no]no
Created AVD 'emulator-19' based on Android 4.4.2, ARM (armeabi-v7a) processor,
with the following hardware config:
hw.lcd.density=240
hw.ramSize=512
vm.heapSize=48
</code></pre>

By default, the Android tool creates the AVD directory in <code>~/.android/avd/</code> (on Linux and Mac).

Finally, you can start the emulator by running this:

<pre><code class="language-bash">
$ emulator -avd  []
</code></pre>

Note that if you are using a real headless Ubuntu server, you will get the following error: “SDL init failure, reason is: No available video device.”

This means that it is not possible to detect a display connected to your machine. If you plan to run the Android test on a headless server, as we do, then you can start the emulator without a graphical display. You can solve this by running the following:

<pre><code class="language-bash">
$ emulator -avd emulator-19 -no-window
</code></pre>

Now that we have the Android SDK installed and the emulator running, it is a good time to run the Appium configuration that we referred to earlier.

Open a new terminal instance, and run the following commands from your workspace folder:

<pre><code class="language-bash">
$ cd appium;
$ ./reset.sh —android  --verbose
</code></pre>

If everything worked fine, you should see this message:

<pre><code class="language-bash">
Done, without errors.
---- reset.sh completed successfully ----
</code></pre>

We ran into the following problem for Ubuntu version 14.04 64-bit, as <a href="https://stackoverflow.com/questions/22701405/aapt-ioexception-error-2-no-such-file-or-directory-why-cant-i-build-my-grad">described on StackOverflow</a>:

<pre><code class="language-bash">
"android-sdk-linux/build-tools/23.0.2/aapt": error=2, No such file or directory
</code></pre>

Once the Android SDK is ready, the next step is to install the Android APIs that our apps will target in the tests. Note that Appium requires API level 17 or above in order to work properly.

Run the following command to see the list of available packages:

<pre><code class="language-bash">
$ android list sdk --all
</code></pre>

This will render a list like the following (edited for brevity):

<pre><code class="language-bash">
Refresh Sources:
  Fetching https://dl.google.com/android/repository/addons_list-2.xml
  Validate XML
  Parse XML
  Fetched Add-ons List successfully
  Refresh Sources
  Fetching URL: https://dl.google.com/android/repository/repository-11.xml
  Validate XML: https://dl.google.com/android/repository/repository-11.xml
==== shorted ====
Packages available for installation or update: 160
   1- Android SDK Tools, revision 24.4.1
   2- Android SDK Tools, revision 25.0.5 rc6
   3- Android SDK Platform-tools, revision 23.1
   4- Android SDK Build-tools, revision 23.0.2
   5- Android SDK Build-tools, revision 23.0.1
   6- Android SDK Build-tools, revision 23 (Obsolete)
==== shorted ====
  26- SDK Platform Android 6.0, API 23, revision 2
  27- SDK Platform Android 5.1.1, API 22, revision 2
  28- SDK Platform Android 5.0.1, API 21, revision 2
  29- SDK Platform Android 4.4W.2, API 20, revision 2
  30- SDK Platform Android 4.4.2, API 19, revision 4
  31- SDK Platform Android 4.3.1, API 18, revision 3
  32- SDK Platform Android 4.2.2, API 17, revision 3
  33- SDK Platform Android 4.1.2, API 16, revision 5
  34- SDK Platform Android 4.0.3, API 15, revision 5
  35- SDK Platform Android 4.0, API 14, revision 4 (Obsolete)
  36- SDK Platform Android 3.2, API 13, revision 1 (Obsolete)
  37- SDK Platform Android 3.1, API 12, revision 3 (Obsolete)
  38- SDK Platform Android 3.0, API 11, revision 2 (Obsolete)
  39- SDK Platform Android 2.3.3, API 10, revision 2
  40- SDK Platform Android 2.3.1, API 9, revision 2 (Obsolete)
  41- SDK Platform Android 2.2, API 8, revision 3
  42- SDK Platform Android 2.1, API 7, revision 3 (Obsolete)
  43- SDK Platform Android 2.0.1, API 6, revision 1 (Obsolete)
  44- SDK Platform Android 2.0, API 5, revision 1 (Obsolete)
  45- SDK Platform Android 1.6, API 4, revision 3 (Obsolete)
  46- SDK Platform Android 1.5, API 3, revision 4 (Obsolete)
  47- SDK Platform Android 1.1, API 2, revision 1 (Obsolete)
==== shorted ====
</code></pre>

The most important part of this list is the first number at the beginning of each line, because this is the identification number of the package that we want to install. You can install one or more packages at the same time with the following command:

<pre><code class="language-bash">
$ android update sdk -u -a -t 1,2,3,4,..,n
</code></pre>

<strong>Important:</strong> Make sure to install API 19. We’ve detected an open issue in Appium’s source code that requires API 19 in order to create a Bootstrap project for Android. For more details, check out lines 399 to 412 of the <a href="https://github.com/appium/appium/blob/1.4/grunt-helpers.js">grunt-helpers.js file</a> on GitHub:

<pre><code class="language-javascript">
module.exports.setupAndroidBootstrap = function (grunt, cb) {
  var projPath = path.resolve(__dirname, "lib", "devices", "android",
      "bootstrap");
  var args = ["create", "uitest-project", "-n", "AppiumBootstrap", "-t",
              "android-19", "-p", "."];
  // TODO: possibly check output of `android list target` to make sure api level 19 is available?
  setupAndroidProj(grunt, projPath, args, cb);
};

module.exports.setupAndroidApp = function (grunt, appName, cb) {
  var appPath = path.resolve(__dirname, "sample-code", "apps", appName);
  var args = ["update", "project", "--subprojects", "-t", "android-19", "-p", ".", "-n", appName];
  setupAndroidProj(grunt, appPath, args, cb);
};
</code></pre>

For the next step, you need to install the application binary interface (ABI) for the Android API that you’ve installed. You can choose from among <a href="https://developer.android.com/ndk/guides/abis.html">several ABIs</a>. This is required because if your target API does not have at least one ABI installed, then you won’t be able to create an emulator for it.

In our configuration, we’ve installed armeabi-v7a for API 19. You can do this by running the same command as before but with the right package number that you see in your own listing. For example:

<pre><code class="language-bash">
$ android update sdk -u -a -t 120
</code></pre>

<strong>Note:</strong> Replace the <code>-t</code> argument (<code>120</code>) with the package number you want to install.

Now we are ready to create a new Android emulator. Check out the document “<a href="https://developer.android.com/tools/devices/managing-avds-cmdline.html">Handling AVDs From the Command Line</a>” (AVDs being Android virtual devices) for more information.

Run the following command to see which Android images are already available in your system:

<pre><code class="language-bash">
$ android list targets
</code></pre>

You should get an output like this:

<pre><code class="language-bash">
Available Android targets:
----------
id: 1 or "android-19"
     Name: Android 4.4.2
     Type: Platform
     API level: 19
     Revision: 4
     Skins: HVGA, QVGA, WQVGA400, WQVGA432, WSVGA, WVGA800 (default), WVGA854, WXGA720, WXGA800, WXGA800-7in
 Tag/ABIs : default/armeabi-v7a
</code></pre>

To create a new AVD using this target, just run the following:

<pre><code class="language-bash">
$ android create avd -n emulator-19 -t 1
</code></pre>

The parameter <code>-n</code> helps us define a name for our AVD, which will be <code>emulator-19</code> in our case. This name is important because we need to tell Appium about it later in order to run our tests. The parameter <code>-t</code> is used to select the target from the previous list. In our case, the ID is <code>1</code> or <code>android-19</code>.

Once the command is done, we should get something similar to this output:

<pre><code class="language-bash">
Auto-selecting single ABI armeabi-v7a
Android 4.4.2 is a basic Android platform.
Do you wish to create a custom hardware profile [no]no
Created AVD 'emulator-19' based on Android 4.4.2, ARM (armeabi-v7a) processor,
with the following hardware config:
hw.lcd.density=240
hw.ramSize=512
vm.heapSize=48
</code></pre>

By default, the Android tool creates the AVD directory in <code>~/.android/avd/</code> (on Linux and Mac).

Finally, you can start the emulator by running this:

<pre><code class="language-bash">
$ emulator -avd  []
</code></pre>

Note that if you are using a real headless Ubuntu server, you will get the following error: “SDL init failure, reason is: No available video device.”

This means that it is not possible to detect a display connected to your machine. If you plan to run the Android test on a headless server, as we do, then you can start the emulator without a graphical display. You can solve this by running the following:

<pre><code class="language-bash">
$ emulator -avd emulator-19 -no-window
</code></pre>

Now that we have the Android SDK installed and the emulator running, it is a good time to run the Appium configuration that we referred to earlier.

Open a new terminal instance, and run the following commands from your workspace folder:

<pre><code class="language-bash">
$ cd appium;
$ ./reset.sh —android  --verbose
</code></pre>

If everything worked fine, you should see this message:

<pre><code class="language-bash">
Done, without errors.
---- reset.sh completed successfully ----
</code></pre>

We ran into the following problem for Ubuntu version 14.04 64-bit, as <a href="https://stackoverflow.com/questions/22701405/aapt-ioexception-error-2-no-such-file-or-directory-why-cant-i-build-my-grad">described on StackOverflow</a>:

<pre><code class="language-bash">
"android-sdk-linux/build-tools/23.0.2/aapt": error=2, No such file or directory
</code></pre>

To fix this, you need to install two extra libraries by running the following:

<pre><code class="language-bash">
$ sudo apt-get install lib32stdc++6 lib32z1
</code></pre>

Then, proceed to clean Git and run the Appium configuration again:

<pre><code class="language-bash">
$ git clean -dfx
$ git reset --hard
$ ./reset.sh —android  --verbose
</code></pre>

In the end, you should see a success message:

<pre><code class="language-bash">
Done, without errors.
---- reset.sh completed successfully ----
</code></pre>

Now, you can start the Appium server just by running this:

<pre><code class="language-bash">
$ node .
</code></pre>

## Running Appium Tests With Python

The first requirement at this stage is to get your Android emulator and Appium up and running.

Appium supports different languages that you can use to write tests. In our case, we want to use Python, so we need to install the <a href="https://github.com/appium/python-client">Appium Python Client</a> in our Python environment. Assuming you have pip installed, you can do this by running the following:

<pre><code class="language-bash">
$ pip install Appium-Python-Client
</code></pre>

For demonstration purposes, we will be using the sample code available in the <code>appium</code> folder available in our workspace. The <code>sample-code</code> folder contains examples of Appium tests written in different languages, plus a set of demo apps that we can use to get familiar with Appium’s API.

Go to the <code>sample-code/examples/python/</code> folder, and open the <code>android-simple.py</code> file. This file contains two tests that we will run on one of the sample Android apps.

The first thing we need to do is edit the <code>setUp</code> method to indicate the right information about our environment. Replace <code>platformVersion</code> with the platform used in your emulator — in our case, 4.2.2 (API 19). Don’t forget to also replace <code>deviceName</code> with the one you used to create your emulator — in our case, <code>emulator-19</code>.</p>

<pre><code class="language-python">
# Original android-simple.py

def setUp(self):
        desired_caps = {}
        desired_caps['platformName'] = 'Android'
        desired_caps['platformVersion'] = '4.2'
        desired_caps['deviceName'] = 'Android Emulator'
        desired_caps['app'] = PATH(
            '../../../sample-code/apps/ApiDemos/bin/ApiDemos-debug.apk'
        )

        self.driver = webdriver.Remote('https://localhost:4723/wd/hub', desired_caps)
</code></pre>

<pre><code class="language-python">
# Modified android-simple.py

def setUp(self):
        desired_caps = {}
        desired_caps['platformName'] = 'Android'
        desired_caps['platformVersion'] = ‘4.2.2'
        desired_caps['deviceName'] = 'emulator-19'
        desired_caps['app'] = PATH(
            '../../../sample-code/apps/ApiDemos/bin/ApiDemos-debug.apk'
        )

        self.driver = webdriver.Remote('https://localhost:4723/wd/hub', desired_caps)
</code></pre>

Once you do this, you can just run the test and observe the interaction in the terminal. To run the test, we recommend installing py.test in your Python environment. If you don’t have it yet, just run the following:

<pre><code class="language-bash">
$ pip install py.test
</code></pre>

Then, just run your Python test:

<pre><code class="language-bash">
$ py.test android-simple.py
</code></pre>

If everything has gone fine, you should see the following lines at the very bottom of the shell trace:

<pre><code class="language-bash">
=================================================================== 2 passed in 221.54 seconds ===================================================================
info: </code></pre>

This indicates that two tests were executed and that they passed successfully.

Finally, once the test has completed, if want to stop the emulator and Appium manually, you can do so by running two commands. To stop the Android emulator, run this:

<pre><code class="language-bash">
$ adb emu kill
</code></pre>

And to stop Appium, type <code>Control</code> + <code>C</code>.</p>

## Summary

Writing tests to guarantee bug-free software is not straightforward. However, the underlying technology to build a testing infrastructure should not be an impediment. Appium is a solution that protects you from the heterogeneity of mobile platforms and helps you focus on writing functional tests that can be run independent of platform.

In this tutorial, we have shown how to build your own test automation environment for Android by relying on Appium. We have described all of the steps required to successfully install Appium on a fresh Ubuntu 14.04 server and shown how simple it is to run Appium tests written in Python.

Hopefully, this guide has lowered the barrier for you to build your own mobile test automation solution.

{{< signature "al" >}}


---
title: Creating Universal Windows Apps With React Native
slug: creating-universal-windows-apps-with-react-native
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5160435-636d-4a68-bd4c-d91ae1ab3e3a/creating-universal-windows-apps-with-react-native-opt.png
date: 2016-10-04T17:03:41.000Z
author: ericrozell
description: >-
  React.js is a popular JavaScript library for building reusable UI components.
  React Native takes all the great features of React, from the one-way binding
  and virtual DOM to debugging tools, and applies them to mobile app development
  on iOS and Android.

  With the React Native Universal Windows platform extension, you can now make
  your React Native applications run on the Universal Windows families of
  devices, including desktop, mobile, and Xbox, as well as Windows IoT, Surface
  Hub, and HoloLens.
categories:
  - Mobile
  - Apps
  - React Native
  - Sponsored Content
---
<a href="https://facebook.github.io/react/">React.js</a> is a popular JavaScript library for building reusable UI components. <a href="https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/">React Native</a> takes all the great features of React, from the one-way binding and virtual DOM to <a href="https://facebook.github.io/react-native/docs/debugging.html">debugging tools</a>, and applies them to mobile app development on iOS and Android.

With the React Native Universal Windows platform extension, you can now make your React Native applications run on the Universal Windows families of devices, including desktop, mobile, and Xbox, as well as Windows IoT, Surface Hub, and HoloLens.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Beyond The Browser: From Web Apps To Desktop Apps](https://www.smashingmagazine.com/2017/03/beyond-browser-web-desktop-apps/)
*   [<span class="headline">Building Hybrid Apps With ChakraCore</span>](https://www.smashingmagazine.com/2016/09/building-hybrid-apps-with-chakracore/)
*   [Providing A Native Experience With Web Technologies](https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)

In this code story, we will walk through the process of setting up a Universal Windows project for React Native, importing core Windows-specific modules to your JavaScript components, and running the app with Visual Studio.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d5160435-636d-4a68-bd4c-d91ae1ab3e3a/creating-universal-windows-apps-with-react-native-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a200e5a-f1ac-4553-9371-4c672fd2a775/creating-universal-windows-apps-with-react-native-500px-opt.png" alt="Creating-Universal-Windows-Apps-with-React-Native" width="500" height="312" /></a></figure>

## Installing React Native For Windows

Installing the React Native Universal Windows platform extension is easy, whether you want to add the Windows platform to your existing app, or you want to start from scratch building an app just for Windows.</p>

### Adding React Native for Windows to Existing Projects

React Native developers may be familiar with <a href="https://github.com/RNPM/RNPM">RNPM</a>, a tool initially built to simplify the process of adding native dependencies to React Native projects. RNPM has a great plugin architecture upon which the React Native for Windows command line tools were built.

To start, make sure you have RNPM installed globally.

<pre><code class="language-bash">npm install -g rnpm
</code></pre>

Once RNPM is installed, install the Windows plugin for RNPM and initialize your project.

<pre><code class="language-bash">npm install --save-dev rnpm-plugin-windows
rnpm windows
</code></pre>

The <code>windows</code> command will do the following:

*   Install `react-native-windows` from [NPM](https://www.npmjs.com/package/react-native-windows),
*   Read the name of your project from `package.json`,
*   Use [Yeoman](https://yeoman.io/) to generate the Windows project files.

The RNPM plugin architecture searches your local package.json <code>dependencies</code> and <code>devDependencies</code> for modules that match <code>rnpm-plugin-*</code>, hence the <code>--save-dev</code> above.

Head to <a href="https://github.com/ReactWindows/react-native-windows/tree/master/local-cli/rnpm">GitHub</a> for more information on <code>rnpm-plugin-windows</code>.</p>

### Creating a React Native for Windows Project from Scratch

You have a few different options to create a React Native Universal Windows project from scratch. If your eventual intent is to also build apps for iOS and Android in the same code base, then the recommendation is to first use the <a href="https://facebook.github.io/react-native/docs/tutorial.html">existing tutorial</a> to set up your React Native project, and then follow the steps above. E.g.,

<pre>&lt;code="language-bash"&gt;npm install -g react-native-cli
react-native init myapp
</pre>

<strong>Note:</strong> the <code>react-native-windows</code> NPM package is only compatible with the latest versions of <code>react-native</code>, from version 0.27 onwards.

Otherwise, you can easily set yourself up with <code>npm init</code>.

<pre><code class="language-bash">mkdir myapp
cd myapp
npm init
npm install --save-dev rnpm-plugin-windows
rnpm windows
</code></pre>

<strong>Note:</strong> the default behavior for choosing the version of <code>react-native-windows</code> is to install the latest version if the <code>package.json</code> does not yet have a <code>react-native</code> dependency. Otherwise, if a <code>react-native</code> dependency already exists, the plugin will attempt to install a version of <code>react-native-windows</code> that matches the major and minor version of <code>react-native</code>.

The Windows plugin for RNPM will automatically install the <code>react-native</code> and <code>react</code> peer dependencies for <code>react-native-windows</code> if they have not yet been installed.</p>

## React Native For Windows Project Structure

There are a few boilerplate files that get generated for the Universal Windows App. The important ones include:

*   `index.windows.js` — This is the entry point to your React application.
*   `windows/myapp.sln` — This is where you should start to launch your app and debug native code.
*   `windows/myapp/MainPage.cs` — This is where you can tweak the native bridge settings, like available modules and components.

Here’s the full output:

<pre>&lt;code="language-bash"&gt;├── index.windows.js
├── windows
    ├── myapp.sln
    ├── myapp
        ├── Properties
            ├── AssemblyInfo.cs
            ├── Default.rd.xml
        ├── Assets
            ├── ...
        ├── App.xaml
        ├── App.xaml.cs
        ├── MainPage.cs
        ├── project.json
        ├── Package.appxmanifest
        ├── myapp_TemporaryKey.pfx
</pre>

We ship the core C# library for React Native as source on NPM. Having direct access to the source will help with debugging and making small tweaks where necessary. As long as the core ships as source, third party modules will also need to follow suit (although their dependencies may be binary). We’ll be working with the React Native community on <code>react-native link</code> support to make dependency management as simple as possible. Instructions for how to link dependencies are available on <a href="https://github.com/ReactWindows/react-native-windows/blob/master/docs/LinkingLibrariesWindows.md">GitHub</a>.</p>

## Building And Extending Apps For The Windows Platform

The core components and modules for React Native are imported as follows:
<div class="language-js language-bash"><br>
<pre class="highlight"><code><span class="kr">import</span> <span class="p">{</span>
  <span class="nx">View</span><span class="p">,</span>
  <span class="nx">Text</span><span class="p">,</span>
  <span class="nx">Image</span>
<span class="p">}</span> <span class="nx">from</span> <span class="s1">'react-native'</span><span class="p">;</span>
</code></pre>

Currently, the same goes for Android- and iOS-specific modules, i.e.:
<div class="language-js language-bash"><br>
<pre class="highlight"><code><span class="kr">import</span> <span class="p">{</span>
  <span class="nx">TabBarIOS</span><span class="p">,</span>
  <span class="nx">DrawerLayoutAndroid</span>
<span class="p">}</span> <span class="nx">from</span> <span class="s1">'react-native'</span><span class="p">;</span>
</code></pre>

Since Windows is a plugin to the framework, core modules specific to Windows are imported from <code>react-native-windows</code>, i.e.:
<div class="language-js language-bash"><br>
<pre class="highlight"><code><span class="kr">import</span> <span class="p">{</span>
  <span class="nx">FlipViewWindows</span><span class="p">,</span>
  <span class="nx">SplitViewWindows</span>
<span class="p">}</span> <span class="nx">from</span> <span class="s1">'react-native-windows'</span><span class="p">;</span>
</code></pre>

So, a typical imports section of a React component with a mixture of core and Windows-specific modules will look like:
<div class="language-js language-bash"><br>
<pre class="highlight"><code><span class="kr">import</span> <span class="nx">React</span><span class="p">,</span> <span class="p">{</span> <span class="nx">Component</span> <span class="p">}</span> <span class="nx">from</span> <span class="s1">'react'</span><span class="p">;</span>
<span class="kr">import</span> <span class="p">{</span>
  <span class="nx">AppRegistry</span><span class="p">,</span>
  <span class="nx">StyleSheet</span><span class="p">,</span>
  <span class="nx">Text</span><span class="p">,</span>
  <span class="nx">View</span>
<span class="p">}</span> <span class="nx">from</span> <span class="s1">'react-native'</span><span class="p">;</span>
<span class="kr">import</span> <span class="p">{</span>
  <span class="nx">SplitViewWindows</span>
<span class="p">}</span> <span class="nx">from</span> <span class="s1">'react-native-windows'</span><span class="p">;</span>
</code></pre>

There is a list of the core modules available on React Native for Windows on <a href="https://github.com/ReactWindows/react-native-windows/tree/master/docs/CoreParityStatus.md">GitHub</a>.

There are multiple ways to add conditional behavior to your apps based on the platform. One way that you might already recognize is the use of the <code>*.platform.js</code> pattern, i.e., <code>index.[android|ios|windows].js</code>. The <a href="https://github.com/facebook/node-haste"><code class="language-bash">node-haste</code></a> dependency graph will choose the filename that matches the active platform choice, and fallback to the filename without any platform indicator, if available. E.g., if you have files <code>MyComponent.windows.js</code> and <code>MyComponent.js</code>, <code>node-haste</code> will choose <code>MyComponent.js</code> for Android and iOS and <code>MyComponent.windows.js</code> for Windows.

Another way is to use conditional logic inside a component, as demonstrated in the simple component below.
<div class="language-js language-bash"><br>
<pre class="highlight"><code><span class="kr">import</span> <span class="nx">React</span><span class="p">,</span> <span class="p">{</span><span class="nx">Component</span><span class="p">}</span> <span class="nx">from</span> <span class="s1">'react'</span><span class="p">;</span>
<span class="kr">import</span> <span class="p">{</span>
  <span class="nx">Platform</span><span class="p">,</span>
  <span class="nx">Text</span><span class="p">,</span>
  <span class="nx">View</span>
<span class="p">}</span> <span class="nx">from</span> <span class="s1">'react-native'</span><span class="p">;</span>

<span class="kr">class</span> <span class="nx">HelloComponent</span> <span class="kr">extends</span> <span class="nx">Component</span> <span class="p">{</span>
  <span class="nx">render</span><span class="p">()</span> <span class="p">{</span>
    <span class="kd">var</span> <span class="nx">text</span> <span class="o">=</span> <span class="s2">"Hello world!"</span><span class="p">;</span>
    <span class="k">if</span> <span class="p">(</span><span class="nx">Platform</span><span class="p">.</span><span class="nx">OS</span> <span class="o">===</span> <span class="s1">'android'</span><span class="p">)</span> <span class="p">{</span>
      <span class="nx">text</span> <span class="o">=</span> <span class="s2">"Hello Android!"</span><span class="p">;</span>
    <span class="p">}</span> <span class="k">else</span> <span class="k">if</span> <span class="p">(</span><span class="nx">Platform</span><span class="p">.</span><span class="nx">OS</span> <span class="o">===</span> <span class="s1">'windows'</span><span class="p">)</span> <span class="p">{</span>
      <span class="nx">text</span> <span class="o">=</span> <span class="s2">"Hello Windows!"</span><span class="p">;</span>
    <span class="p">}</span>

    <span class="k">return</span> <span class="p">(</span>
      <span class="o">&lt;</span><span class="nx">View</span><span class="o">&gt;</span>
        <span class="o">&lt;</span><span class="nx">Text</span><span class="o">&gt;</span><span class="p">{</span><span class="nx">text</span><span class="p">}</span><span class="o">&lt;</span><span class="sr">/text</span><span class="err">&gt;
</span>      <span class="o">&lt;</span><span class="sr">/View</span><span class="err">&gt;
</span>    <span class="p">);</span>
  <span class="p">}</span>
<span class="p">}</span>
</code></pre>

Facebook has a very good article on cross-platform design with React Native at <a href="https://makeitopen.com/tutorials/building-the-f8-app/design/">makeitopen.com</a>.
## Running The Universal Windows App

There are a few options for running your React Native Universal Windows app. The easiest way, for now, is to launch the app in Visual Studio. After initializing the project, open the Visual Studio solution at <code>./windows/myapp.sln</code> in <a href="https://www.visualstudio.com/downloads/download-visual-studio-vs">Visual Studio 2015</a> (Community edition is supported). From Visual Studio, choose which platform you want to build for (x86, x64, or ARM), choose the target you want to deploy to, and press F5. We are still working on deployment from the command line, but work to enable a <code>run-windows</code> command to the RNPM plugin is underway.

The instructions for running React Native UWP apps, both from Visual Studio and from the CLI, will be evolving on <a href="https://github.com/ReactWindows/react-native-windows/blob/master/docs/RunningOnDeviceWindows.md">GitHub</a>. If you have any problems getting started with building or running your React Windows application, reach out on <a href="https://discord.gg/0ZcbPKXt5bWJVmUY">Discord</a> or <a href="https://github.com/ReactWindows/react-native-windows#opening-issues">open an issue</a>. We look forward to hearing your feedback and reviewing your <a href="https://github.com/ReactWindows/react-native-windows#contributing">contributions</a>!
## More Hands-On With Web And Mobile Apps

Check out these helpful resources on building web and Mobile Apps:
<ul>
 	<li><a href="https://msdn.microsoft.com/en-us/windows/uwp/get-started/universal-application-platform-guide?wt.mc_id=873567&amp;UWApsWReactAppsatSM">Intro to the Universal Windows Platform</a></li>
 	<li><a href="https://developer.microsoft.com/en-us/windows/bridges?wt.mc_id=873567&amp;UWApsWReactAppsatSM">How to port existing code to Windows with Windows Bridges</a></li>
 	<li><a href="https://mva.microsoft.com/training-topics/app-development?wt.mc_id=873567&amp;UWApsWReactAppsatSM#!lang=1049">App Development Courses and Tutorials</a></li>
 	<li><a href="https://mva.microsoft.com/training-topics/c-app-development?wt.mc_id=873567&amp;UWApsWReactAppsatSM#!lang=1049">C# / XAML Courses and tutorials</a></li>
 	<li><a href="https://azure.microsoft.com/en-us/services/app-service/?wt.mc_id=873566&amp;HybridAppsAppsatSM">Azure App Services</a></li>
 	<li><a href="https://www.visualstudio.com/en-us/features/xamarin-vs.aspx?wt.mc_id=873567&amp;UWApsWReactAppsatSM">Mobile Apps in Visual Studio with Xamarin</a></li>
</ul>
For further updates on the topic and new features, please view the <a href="https://www.microsoft.com/developerblog/real-life-code/2016/05/27/Creating-Universal-Windows-Apps-with-React-Native.html?wt.mc_id=873567&amp;UWApsWReactAppsatSM">original documentation</a>.

</div>
</div>
</div>
</div>
</div>


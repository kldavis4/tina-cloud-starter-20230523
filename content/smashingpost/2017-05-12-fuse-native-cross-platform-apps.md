---
title: How To Create Native Cross-Platform Apps With Fuse
slug: fuse-native-cross-platform-apps
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c1de9d1-0d01-4d15-bcae-629cfa79ef8c/how-fuse-works-500w-opt.png
date: 2017-05-12T03:48:38.000Z
author: anchetawern
description: >-
  Fuse is a toolkit for creating apps that run on both iOS and Android devices.
  It enables you to create apps using UX Markup, an XML-based language. But
  unlike the components in React Native and NativeScript, Fuse is not only used
  to describe the UI and layout; you can also use it to add effects and
  animation.

  Styles are described by adding attributes such as Color and Margin to the
  various elements. Business logic is written using JavaScript. Later on, we’ll
  see how all of these components are combined to build a truly native app.
categories:
  - Coding
  - JavaScript
  - Apps
  - Performance
  - React
  - React Native
---
<p>Styles are described by adding attributes such as <code>Color</code> and <code>Margin</code> to the various elements. Business logic is written using JavaScript. Later on, we'll see how all of these components are combined to build a truly native app.

In this article, you will learn what Fuse is all about. We'll see how it works and how it compares to other platforms such as React Native and NativeScript. In the <a href="https://www.smashingmagazine.com/2017/05/fuse-native-cross-platform-apps/#creating-a-weather-app-with-fuse">second half of the article</a>, you will create your first Fuse app. Specifically, you will create a weather app that shows the weather based on the user's current location. Here's what the output will look like:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8347c461-1911-4722-a357-cf3a14238e5a/app-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8347c461-1911-4722-a357-cf3a14238e5a/app-preview-opt.png" alt="Weather app Fuse preview" width="250" height="" /></a><figcaption>Weather app Fuse preview</figcaption></figure>

In creating the app, you will learn how to use some of Fuse's built-in UI components and learn how to access native device functionality such as geolocation. Towards the end of the article, you will consolidate your learning by looking at the advantages and disadvantages of using Fuse for your next mobile app project.

{{% feature-panel %}}

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
<li><a title="Read 'Best Of Both Worlds: Mixing HTML5 And Native Code'" href="https://www.smashingmagazine.com/2013/10/best-of-both-worlds-mixing-html5-native-code/" rel="bookmark">Best Of Both Worlds: Mixing HTML5 And Native Code</a></li>
<li><a title="Read 'Why You Should Consider React Native For Your Mobile App'" href="https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/" rel="bookmark">Why You Should Consider React Native For Your Mobile App</a></li>
<li><a title="Read 'A Glimpse Into The Future With React Native For Web'" href="https://www.smashingmagazine.com/2016/08/a-glimpse-into-the-future-with-react-native-for-web/" rel="bookmark">A Glimpse Into The Future With React Native For Web</a></li>
<li><a title="Read 'Hybrid Mobile Apps: Providing A Native Experience With Web Technologies'" href="https://www.smashingmagazine.com/2014/10/providing-a-native-experience-with-web-technologies/" rel="bookmark">Hybrid Mobile Apps: Providing A Native Experience With Web Technologies</a></li>
</ul>

## How Does Fuse Work?

I'd like to describe how Fuse works using the following diagram:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f9b174c-360f-41ba-a5b2-c3eb41757365/how-fuse-works-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6f9b174c-360f-41ba-a5b2-c3eb41757365/how-fuse-works-opt.png" alt="How Fuse works" width="355" height="500" /></a><figcaption>How Fuse works</figcaption></figure>

On the top layer are the UX Markup and JavaScript. This is where we will spend most of our time when working with Fuse. On the middle layer are the libraries that are packaged with Fuse. This includes the JavaScript APIs that allow access to native device features such as geolocation and the camera. Lastly, on the bottom layer is the Uno compiler, which is responsible for translating the UX Markup into pure native code (Objective-C for iOS and C++ for Android). Once the app runs, all of the UI that you will see will be native UI for that particular platform. JavaScript code is executed via a virtual machine on a separate thread. This makes the UI really snappy because JavaScript won't affect the UI's performance.</p>

## How Does It Compare To React Native And NativeScript?

Before we create an app with Fuse, one of the important questions that needs to be answered is how does it stack up against existing tools that do the same job. In this section, we'll learn about the features and tools available in Fuse compared to those of <a href="https://www.smashingmagazine.com/2017/06/transition-hybrid-apps-react-native/">React Native</a> and NativeScript, as well as how things are done on each platform. Specifically, we'll compare the following areas:
<ul>
 	<li>UI markup</li>
 	<li>Layout</li>
 	<li>JavaScript APIs</li>
 	<li>Extendability</li>
 	<li>JavaScript Libraries</li>
 	<li>Animation</li>
 	<li>Community</li>
 	<li>Development Workflow</li>
 	<li>Debugging</li>
</ul>

### UI Markup

On all platforms, the UI can be built using an XML-based language. Common UI components such as text fields, switches and sliders are available on each platform.

React Native has the most of these components, although some are not unified, which means that there can be a maximum of two ways to use a particular component. For example, one can be used on both platforms, and one for a specific platform only. A few components, such as the <code>ProgressBar</code>, are also implemented differently on each platform, which means that it's not totally "write once, run everywhere."

On the other hand, NativeScript has a unified way of implementing the different UI components on each platform. For every component, there's an equivalent native component for both Android and iOS.

Fuse has a decent number of UI components that will cover the requirements of most projects. One component that's not built into either React Native or NativeScript is the <code>Video</code> component, which can be used to play local videos and even videos from the Internet. The only component that is currently missing is the date-picker, which is especially useful during user registration. Though you can always create your own using the components that are already available to Fuse.</p>

### Layout

In React Native, layout is done with <a href="https://www.smashingmagazine.com/2016/11/css-grids-flexbox-box-alignment-new-layout-standard/">Flexbox</a>. In a nutshell, Flexbox enables you to specify how content should flow through the available space. For example, you can set <code>flex</code> to <code>1</code> and <code>flexDirection</code> to <code>row</code> in a container element in order to equally divide the available space among the children and to arrange the children vertically.</p>

<pre><code class="language-markup">&lt;View style={{flex: 1, flexDirection: 'row'}}&gt;
	&lt;View style={{backgroundColor: 'powderblue'}} /&gt;
	&lt;View style={{backgroundColor: 'skyblue'}} /&gt;
	&lt;View style={{backgroundColor: 'steelblue'}} /&gt;
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>View</span><span class="token punctuation">&gt;</span></span>
</code></pre>

In NativeScript, layout is achieved using layout containers, the most basic one being <code>StackLayout</code>, which puts all elements on top of each other, just like in the example below. In a horizontal orientation, they're placed side by side.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>StackLayout</span> <span class="token attr-name">orientation</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>vertical<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Image</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>assets/images/dog.png<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Image</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>assets/images/cat.png<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Image</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>assets/images/gorilla.png<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>StackLayout</span><span class="token punctuation">&gt;</span></span>	
</code></pre>

Similarly, Fuse achieves layout by using a combination of the different elements in UX Markup, the most common ones being <code>StackPanel</code>, <code>Grid</code> and <code>DockPanel</code>. <code>StackPanel</code> works similar to <code>StackLayout</code> in NativeScript. Here's an example:

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>StackPanel</span> <span class="token attr-name">Orientation</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Vertical<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Panel</span> <span class="token attr-name">Height</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>100<span class="token punctuation">"</span></span> <span class="token attr-name">Background</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Red<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Panel</span> <span class="token attr-name">Height</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>100<span class="token punctuation">"</span></span> <span class="token attr-name">Background</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>White<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Panel</span> <span class="token attr-name">Height</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>100<span class="token punctuation">"</span></span> <span class="token attr-name">Background</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Blue<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>StackPanel</span><span class="token punctuation">&gt;</span></span>
</code></pre>

### JavaScript APIs

All of the platforms cover all of the basics with JavaScript APIs. Things like camera functionality, platform information, geolocation, push notifications, HTTP requests and local storage can be done on all platforms. However, looking at the documentation for each platform, you could say that React Native has the most JavaScript APIs that bridge the gap between native and "JavaScript native" features. There's no official name yet for platforms such as React Native, NativeScript and Fuse, so let's just stick with "JavaScript native" for now, because they all use JavaScript to write code and they all offer native-like performance.</p>

### Extendability

If you need access to specific device features that don't expose a JavaScript API yet, each platform also provides ways for developers to tap into native APIs for Android and iOS.

NativeScript gives you access to all of the native APIs of the underlying platform through JavaScript. This means you don't have to touch any Swift, Objective-C or Java code in order to make use of the native APIs. The only requirement is that you know how the native APIs work.

React Native falls a bit short in accessing native APIs because you'll have to know the native language in order to extend native functionality. This is done by creating a native module (an Objective-C class for iOS or a Java class for Android), exposing your desired public methods to JavaScript, then importing it into your project.

Fuse allows you to extend functionality through a feature that it refers to as "foreign code." This allows you to call native code on each platform through the Uno language. The Uno language is the core technology of Fuse. It's what makes Fuse work behind the scenes. Making use of native features that aren't supported by the core Fuse library is done by creating an Uno class. Inside the Uno class, you can write the Objective-C or Java code that implements the functionality you want and have it exposed as JavaScript code, which you can then call from your project.

### JavaScript Libraries

Both React Native and NativeScript supports the use of all npm packages that don't have dependencies on the browser model. This means you can use a library such as lodash and moment simply by executing <code>npm install {package-name}</code> in your project directory and then importing it in any of your project files, just like in a normal JavaScript project.

Fuse, on the other hand, is currently lacking in this regard. Usage of existing JavaScript libraries is mostly not possible; only a <a href="https://www.fusetools.com/docs/fusejs/third-party-modules">short list of libraries</a> are known to work. The good news is that the developers are constantly working on polyfills to improve compatibility with existing libraries.</p>

### Animation

Another important part of the UX is animation. In React Native, animation is implemented via its Animated API. With it, you can customize the animation a lot. For example, you can specify how long an animation takes or how fast it runs. But this comes with the downside of not being beginner-friendly. Even simple animation such as scaling a particular element requires a lot of code. The good thing is that libraries such as <a href="https://github.com/oblador/react-native-animatable">React Native Animatable</a> make it easier to work with animation. Here's sample code for implementing a <code>fadeIn</code> animation using the Animatable library:

<pre><code class="language-markup">&lt;Animatable.View animation="fadeIn"&gt;Fade me in!&lt;/Animatable.View&gt;</code></pre>

NativeScript animations can be implemented in two ways: via the CSS3 animations API or the JavaScript API. Here's an example of scaling an element with a class of <code>el</code>:

<pre><code class="language-css"><span class="token selector">.el </span><span class="token punctuation">{</span>
    <span class="token property">animation-name</span><span class="token punctuation">:</span> scale<span class="token punctuation">;</span>
    <span class="token property">animation-duration</span><span class="token punctuation">:</span> 1<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token atrule">@keyframes scale </span><span class="token punctuation">{</span>
    <span class="token selector">from </span><span class="token punctuation">{</span> <span class="token property">transform</span><span class="token punctuation">:</span> scale(1, 1)<span class="token punctuation">;</span> <span class="token punctuation">}</span>
    <span class="token selector">to </span><span class="token punctuation">{</span> <span class="token property">transform</span><span class="token punctuation">:</span> scale(1.5, 1.5)<span class="token punctuation">;</span> <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>

And here's the JavaScript equivalent:

<pre><code class="language-javascript"><span class="token keyword">var</span> view <span class="token operator">=</span> page<span class="token punctuation">.</span><span class="token function">getViewById<span class="token punctuation">(</span></span><span class="token string">'box'</span><span class="token punctuation">)</span><span class="token punctuation">;</span><span class="token comment"> //must have an element with an ID of box in the markup
</span>view<span class="token punctuation">.</span><span class="token function">animate<span class="token punctuation">(</span></span><span class="token punctuation">{</span>
    scale<span class="token punctuation">:</span> <span class="token punctuation">{</span> x<span class="token punctuation">:</span> <span class="token number">1.5</span><span class="token punctuation">,</span> y<span class="token punctuation">:</span> <span class="token number">1.5</span><span class="token punctuation">}</span><span class="token punctuation">,</span>
    duration<span class="token punctuation">:</span> <span class="token number">1000</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>

Animation in Fuse is implemented via triggers and animators. Triggers are used to detect whether something is happening in the app, whereas animators are used to respond to those events. For example, to make something bigger when pressed, you would have this:

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Rectangle</span> <span class="token attr-name">Width</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>50<span class="token punctuation">"</span></span> <span class="token attr-name">Height</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>50<span class="token punctuation">"</span></span> <span class="token attr-name">Fill</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#ccc<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>WhilePressed</span><span class="token punctuation">&gt;</span></span>
    	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Scale</span> <span class="token attr-name">Factor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>2<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>WhilePressed</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>Rectangle</span><span class="token punctuation">&gt;</span></span>
</code></pre>

In this case, <code>&lt;WhilePressed&gt;</code> is the trigger and <code>&lt;Scale&gt;</code> is the animator.</p>

### Community

When it comes to community, React Native is the clear winner. Just the fact that it was created by Facebook is a big deal. Because the main technology used to create apps is React, React Native taps into that community as well. This means that a lot of projects can help you to develop apps. For example, you can reuse existing React components for your React Native project. And because many people use it, you can expect to quickly get help when you get stuck, because you can just search for an answer on Stack Overflow. React Native is also open-source, and the source code is <a href="https://github.com/facebook/react-native">available on GitHub</a>. This makes development really fast because the maintainers can accept help from developers outside of the organization.

NativeScript, meanwhile, was created by Telerik. The project has a decent-sized community behind it. If you look at <a href="https://github.com/NativeScript/NativeScript">its GitHub page</a>, currently over 10,000 people have starred the project. It has been forked 700 times, so one can assume that the project is getting a lot of contributions from the community. There are also a lot of NativeScript packages on npm and questions on Stack Overflow, so expect that you won't have to implement custom functionality from scratch or be left alone looking for answers if you get stuck.

Fuse is the lesser known among the three. It doesn't have a big company backing it up, and Fuse is basically the company itself. Even so, the project comes complete with documentation, a forum, a Slack channel, sample apps, sample code and video tutorials, which make it very beginner-friendly. The Fuse core is not yet open-source, but the developers will be making the code open-source soon.</p>

### Development Workflow

With React Native and NativeScript, you need to have an actual mobile device or an emulator if you want to view changes while you're developing the app. Both platforms also support live reloading, so every time you make a change to the source files, it automatically gets reflected in the app — although there's a slight delay, especially if your machine isn't that powerful.

Fuse, on the other hand, allows you to preview the app both locally and on any number of devices currently connected to your network. This means that both designers and developers can work at the same time and be able to preview changes in real time. This is helpful to the designer because they can immediately see what the app looks like with real data supplied by the developer's code.</p>

### Debugging

When it comes to debugging, both React Native and NativeScript tap into Chrome's Developer Tools. If you're coming from a web development background, the debugging workflow should make sense to you. That being said, not all features that you're used to when inspecting and debugging web projects are available. For example, both platforms allow you to debug JavaScript code but don't allow you to inspect the UI elements in the app. React Native has a built-in inspector that is the closest thing to the element inspector in Chrome's Developer Tools. NativeScript currently doesn't have this feature.

On the other hand, Fuse uses the Debugging Protocol in Google's V8 engine to debug JavaScript code. This allows you to do things like add breakpoints to your code and inspect what each object contains at each part in the execution of the code. The Fuse team encourages the use of the <a href="https://code.visualstudio.com/">Visual Studio Code</a> text editor for this, but any text editor or IDE that supports V8's Debugging Protocol should work. If you want to inspect and visually edit the UI elements, Fuse also includes an inspector — although it allows you to adjust only a handful of properties at the moment, things like widths, heights, margins, padding and colors.</p>

## Creating A Weather App With Fuse

Now you're ready to create a simple weather app with Fuse. It will get the user's location via the GeoLocation API and will use the OpenWeatherMap API to determine the weather in the user's location and then display it on the screen. You can find the full source code of the app in the <a href="https://github.com/anchetaWern/fuse-simple-weatherapp">GitHub repository</a>.

To start, go to the OpenWeatherMap website and <a href="https://home.openweathermap.org/users/sign_up">sign up for an account</a>. Once you're done signing up, it should provide you with an API key, which you can use to make a request to its API later on.

Next, visit the <a href="https://www.fusetools.com/downloads">Fuse downloads page</a>, enter your email address, download the Fuse installer for your platform, and then install it. Once it's installed, launch the Fuse dashboard and click on "New Project". This will open another window that will allow you to select the path to your project and enter the project's name.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6235dbc-71d2-48bf-abda-a2f7df118a4b/creating-a-project-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ff5ef4c-899c-4a6a-814e-e6f515331af4/creating-a-project-opt.png" alt="Creating a new Fuse project" width="500" height="343" /></a><figcaption>Creating a new Fuse project (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6235dbc-71d2-48bf-abda-a2f7df118a4b/creating-a-project-large-preview-opt.png">View large version</a>)</figcaption></figure>

Do that and then click on the "Create" button to create your project. If you're using Sublime Text 3, you can click on the "Open in Sublime Text 3" button to open a new Sublime Text instance with the <a href="https://packagecontrol.io/packages/Fuse">Fuse project</a> already loaded. Once you're in there, the first thing you'll want to do is install the Fuse package. This includes code completion, "Goto definition," previewing the app from Sublime and viewing the build.

Once the Fuse plugin is installed, open the <code>MainView.ux</code> file. This is the main file that we will be working with in this project. By default, it includes sample code for you to play with. Feel free to remove all of the contents of the file once you're done inspecting it.

When you create an app with Fuse, you always start with the <code>&lt;App&gt;</code> tag. This tells Fuse that you want to create a new page.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>App</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>App</span><span class="token punctuation">&gt;</span></span>
</code></pre>

Fuse allows you to reuse icon fonts that are commonly used for the web. Here, we're using <a href="https://erikflowers.github.io/weather-icons/">Weather Icons</a>. Use the <code>&lt;Font&gt;</code> tag to specify the location of the web font file in your app directory via the <code>File</code> attribute. For this project, it's in the <code>fonts</code> folder at the root directory of the project. We also need to give it a <code>ux:Global</code> attribute, which will serve as its ID when you want to use this icon font later on.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Font</span> <span class="token attr-name">File</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>fonts/weather-icons/font/weathericons-regular-webfont.ttf<span class="token punctuation">"</span></span> <span class="token attr-name"><span class="token namespace">ux:</span>Global</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>wi<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
</code></pre>

Next, we have the JavaScript code. We can include JavaScript code anywhere in UX Markup by using the <code>&lt;JavaScript&gt;</code> tag. Inside the tag will be the JavaScript code to be executed.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>JavaScript</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>JavaScript</span><span class="token punctuation">&gt;</span></span>
</code></pre>

In the <code>&lt;JavaScript&gt;</code> tag, require two built-in Fuse libraries: Observable and GeoLocation. Observable allows you to implement data-binding in Fuse. This makes it possible to change the value of the variable via JavaScript code and have it automatically reflected in the UI of the app. Data-binding in Fuse is also two-way; so, if a change is made to a value via the UI, then the value stored in the variable will also be updated, and vice versa.</p>

<pre><code class="language-javascript"><span class="token keyword">var</span> Observable <span class="token operator">=</span> <span class="token function">require<span class="token punctuation">(</span></span><span class="token string">'FuseJS/Observable'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>	
</code></pre>

GeoLocation allows you to get location information from the user's device.</p>

<pre><code class="language-javascript"><span class="token keyword">var</span> Geolocation <span class="token operator">=</span> <span class="token function">require<span class="token punctuation">(</span></span><span class="token string">'FuseJS/GeoLocation'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>	
</code></pre>

Create an object containing the hex code for each of the weather icons that we want to use. You can find the hex code on the <a href="https://erikflowers.github.io/weather-icons/">GitHub page of the icon font</a>.</p>

<pre><code class="language-css"><span class="token selector">var icons = </span><span class="token punctuation">{</span>
   <span class="token string">'clear'</span><span class="token punctuation">:</span> <span class="token string">'\uF00d'</span>,
   <span class="token string">'clouds'</span><span class="token punctuation">:</span> <span class="token string">'\uF002'</span>,
   <span class="token string">'drizzle'</span><span class="token punctuation">:</span> <span class="token string">'\uF009'</span>,
   <span class="token string">'rain'</span><span class="token punctuation">:</span> <span class="token string">'\uF008'</span>,
   <span class="token string">'thunderstorm'</span><span class="token punctuation">:</span> <span class="token string">'\uF010'</span>,
   <span class="token string">'snow'</span><span class="token punctuation">:</span> <span class="token string">'\uF00a'</span>,
   <span class="token string">'mist'</span><span class="token punctuation">:</span> <span class="token string">'\uF0b6'</span>,
   <span class="token string">'fog'</span><span class="token punctuation">:</span> <span class="token string">'\uF003',
</span>   'temp': '\uF055'
<span class="token punctuation">}</span><span class="token punctuation">;</span>	
</code></pre>

Create a function to convert Kelvin to Celsius. We need it because the OpenWeatherMap API returns temperatures in Kelvin.</p>

<pre><code class="language-javascript"><span class="token keyword">function</span> <span class="token function">kelvinToCelsius<span class="token punctuation">(</span></span>kelvin<span class="token punctuation">)</span><span class="token punctuation">{</span>
    <span class="token keyword">return</span> kelvin <span class="token operator">-</span> <span class="token number">273.15</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>	
</code></pre>

Determine whether it's currently day or night based on the time on the user's device. We'll use orange as the background color for the app if it's day, and purple if it's nighttime.</p>

<pre><code class="language-javascript"><span class="token keyword">var</span> hour <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Date</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">getHours<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">var</span> color <span class="token operator">=</span> <span class="token string">'#7417C0'</span><span class="token punctuation">;</span>
<span class="token keyword">if</span><span class="token punctuation">(</span>hour <span class="token operator">&gt;</span><span class="token operator">=</span> <span class="token number">5</span> <span class="token operator">&amp;&amp;</span> hour <span class="token operator">&lt;</span><span class="token operator">=</span> <span class="token number">18</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
    color <span class="token operator">=</span> <span class="token string">'#f38844'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>	
</code></pre>

Add the OpenWeather Map API key that you got earlier and create an observable variable that contains the weather data.</p>

<pre><code class="language-javascript"><span class="token keyword">var</span> api_key <span class="token operator">=</span> <span class="token string">'YOUR OPENWEATHERMAP API KEY'</span><span class="token punctuation">;</span>
<span class="token keyword">var</span> weather_data <span class="token operator">=</span> <span class="token function">Observable<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>	
</code></pre>

Get the location information:

<pre><code class="language-javascript"><span class="token keyword">var</span> loc <span class="token operator">=</span> Geolocation<span class="token punctuation">.</span>location<span class="token punctuation">;</span>	
</code></pre>

This will return an object containing the <code>latitude</code>, <code>longitude</code> and <code>accuracy</code> of the location. However, Fuse currently has a problem with getting location information on Android. If the location setting is disabled on the device, it won't ask you to enable it when you open the app. So, as a workaround, you'll need to first enable location before launching the app.

Make a request to the OpenWeatherMap API using the <code>fetch()</code> function. This function is available in Fuse's global scope, so you can call it from anywhere without including any additional libraries. This will work the same way as the <code>fetch()</code> function available in modern browsers: It also returns a promise that you need to listen to using the <code>then()</code> function. When the supplied callback function is executed, the raw response is passed in as an argument. You can't really use this yet since it contains the whole response object. To extract the data that the API actually returned, you need to call the <code>json()</code> function in the response object. This will return another promise, so you need to use <code>then()</code> one more time to extract the actual data. The data is then assigned as the value of the observable that we created earlier.</p>

<pre><code class="language-javascript"><span class="token keyword">var</span> req_url <span class="token operator">=</span> <span class="token string">'https://api.openweathermap.org/data/2.5/weather?lat='</span> <span class="token operator">+</span> loc<span class="token punctuation">.</span>latitude <span class="token operator">+</span> <span class="token string">'&amp;lon='</span> <span class="token operator">+</span> loc<span class="token punctuation">.</span>longitude <span class="token operator">+</span> <span class="token string">'&amp;apikey='</span> <span class="token operator">+</span> api_key<span class="token punctuation">;</span>
<span class="token function">fetch<span class="token punctuation">(</span></span>req_url<span class="token punctuation">)</span>
<span class="token punctuation">.</span><span class="token function">then<span class="token punctuation">(</span></span><span class="token keyword">function</span><span class="token punctuation">(</span>response<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> response<span class="token punctuation">.</span><span class="token function">json<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token punctuation">.</span><span class="token function">then<span class="token punctuation">(</span></span><span class="token keyword">function</span><span class="token punctuation">(</span>responseObject<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    weather_data<span class="token punctuation">.</span>value <span class="token operator">=</span> <span class="token punctuation">{</span>
        name<span class="token punctuation">:</span> responseObject<span class="token punctuation">.</span>name<span class="token punctuation">,</span>
        icon<span class="token punctuation">:</span> icons<span class="token punctuation">[</span>responseObject<span class="token punctuation">.</span>weather<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">.</span>main<span class="token punctuation">.</span><span class="token function">toLowerCase<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        weather<span class="token punctuation">:</span> responseObject<span class="token punctuation">.</span>weather<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        temperature<span class="token punctuation">:</span> <span class="token function">kelvinToCelsius<span class="token punctuation">(</span></span>responseObject<span class="token punctuation">.</span>main<span class="token punctuation">.</span>temp<span class="token punctuation">)</span>  <span class="token operator">+</span> <span class="token string">' °C'</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>	
</code></pre>

For your reference, here's a sample response returned by the API:

<pre><code class="language-javascript"><span class="token punctuation">{</span>
   <span class="token string">"coord"</span><span class="token punctuation">:</span><span class="token punctuation">{</span>
      <span class="token string">"lon"</span><span class="token punctuation">:</span><span class="token number">120.98</span><span class="token punctuation">,</span>
      <span class="token string">"lat"</span><span class="token punctuation">:</span><span class="token number">14.6</span>
   <span class="token punctuation">}</span><span class="token punctuation">,</span>
   <span class="token string">"weather"</span><span class="token punctuation">:</span><span class="token punctuation">[</span>
      <span class="token punctuation">{</span>
         <span class="token string">"id"</span><span class="token punctuation">:</span><span class="token number">803</span><span class="token punctuation">,</span>
         <span class="token string">"main"</span><span class="token punctuation">:</span><span class="token string">"Clouds"</span><span class="token punctuation">,</span>
         <span class="token string">"description"</span><span class="token punctuation">:</span><span class="token string">"broken clouds"</span><span class="token punctuation">,</span>
         <span class="token string">"icon"</span><span class="token punctuation">:</span><span class="token string">"04d"</span>
      <span class="token punctuation">}</span>
   <span class="token punctuation">]</span><span class="token punctuation">,</span>
   <span class="token string">"base"</span><span class="token punctuation">:</span><span class="token string">"stations"</span><span class="token punctuation">,</span>
   <span class="token string">"main"</span><span class="token punctuation">:</span><span class="token punctuation">{</span>
      <span class="token string">"temp"</span><span class="token punctuation">:</span><span class="token number">304.15</span><span class="token punctuation">,</span>
      <span class="token string">"pressure"</span><span class="token punctuation">:</span><span class="token number">1009</span><span class="token punctuation">,</span>
      <span class="token string">"humidity"</span><span class="token punctuation">:</span><span class="token number">74</span><span class="token punctuation">,</span>
      <span class="token string">"temp_min"</span><span class="token punctuation">:</span><span class="token number">304.15</span><span class="token punctuation">,</span>
      <span class="token string">"temp_max"</span><span class="token punctuation">:</span><span class="token number">304.15</span>
   <span class="token punctuation">}</span><span class="token punctuation">,</span>
   <span class="token string">"visibility"</span><span class="token punctuation">:</span><span class="token number">10000</span><span class="token punctuation">,</span>
   <span class="token string">"wind"</span><span class="token punctuation">:</span><span class="token punctuation">{</span>
      <span class="token string">"speed"</span><span class="token punctuation">:</span><span class="token number">7.2</span><span class="token punctuation">,</span>
      <span class="token string">"deg"</span><span class="token punctuation">:</span><span class="token number">260</span>
   <span class="token punctuation">}</span><span class="token punctuation">,</span>
   <span class="token string">"clouds"</span><span class="token punctuation">:</span><span class="token punctuation">{</span>
      <span class="token string">"all"</span><span class="token punctuation">:</span><span class="token number">75</span>
   <span class="token punctuation">}</span><span class="token punctuation">,</span>
   <span class="token string">"dt"</span><span class="token punctuation">:</span><span class="token number">1473051600</span><span class="token punctuation">,</span>
   <span class="token string">"sys"</span><span class="token punctuation">:</span><span class="token punctuation">{</span>
      <span class="token string">"type"</span><span class="token punctuation">:</span><span class="token number">1</span><span class="token punctuation">,</span>
      <span class="token string">"id"</span><span class="token punctuation">:</span><span class="token number">7706</span><span class="token punctuation">,</span>
      <span class="token string">"message"</span><span class="token punctuation">:</span><span class="token number">0.0115</span><span class="token punctuation">,</span>
      <span class="token string">"country"</span><span class="token punctuation">:</span><span class="token string">"PH"</span><span class="token punctuation">,</span>
      <span class="token string">"sunrise"</span><span class="token punctuation">:</span><span class="token number">1473025458</span><span class="token punctuation">,</span>
      <span class="token string">"sunset"</span><span class="token punctuation">:</span><span class="token number">1473069890</span>
   <span class="token punctuation">}</span><span class="token punctuation">,</span>
   <span class="token string">"id"</span><span class="token punctuation">:</span><span class="token number">1701668</span><span class="token punctuation">,</span>
   <span class="token string">"name"</span><span class="token punctuation">:</span><span class="token string">"Manila"</span><span class="token punctuation">,</span>
   <span class="token string">"cod"</span><span class="token punctuation">:</span><span class="token number">200</span>
<span class="token punctuation">}</span>	
</code></pre>

Export the variables so that it becomes available in the UI.</p>

<pre><code class="language-javascript">module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{</span>
    weather_data<span class="token punctuation">:</span> weather_data<span class="token punctuation">,</span>
    icons<span class="token punctuation">:</span> icons<span class="token punctuation">,</span>
    color<span class="token punctuation">:</span> color
<span class="token punctuation">}</span><span class="token punctuation">;</span>	
</code></pre>

Because this project is very small, I've decided to put everything in one file. But for real projects, the JavaScript code and the UX Markup should be separated. This is because the designers are the ones who normally work with UX Markup, and the developers are the ones who touch the JavaScript code. Separating the two allows the designer and the developer to work on the same page at the same time. You can separate the JavaScript code by creating a new JavaScript file in the project folder and then link it in your markup, like so:

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>JavaScript</span> <span class="token attr-name">File</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>js/weather.js<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>	
</code></pre>

Finally, add the actual UI of the app. Here, we're using <code>&lt;DockPanel&gt;</code> to wrap all of the elements. By default, <code>&lt;DockPanel&gt;</code> has a <code>Dock</code> property that is set to <code>Fill</code>, so it's the perfect container for filling the entire screen with content. Note that we didn't need to set that property below because it's implicitly added. Below, we have only assigned a <code>Color</code> attribute, which allows us to set the background color using the color that we exported earlier.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>DockPanel</span> <span class="token attr-name">Color</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{color}<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>DockPanel</span><span class="token punctuation">&gt;</span></span>	
</code></pre>

Inside <code>&lt;DockPanel&gt;</code> is <code>&lt;StatusBarBackground&gt;</code>, which we'll dock to the top of the screen. This allows us to show and customize the status bar on the user's device. If you don't use this component, <code>&lt;DockPanel&gt;</code> will consume the entirety of the screen, including the status bar. Simply setting this component will make the status bar visible. We don't really want to customize it, so we'll just leave the defaults.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>StatusBarBackground</span> <span class="token attr-name">Dock</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Top<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>	
</code></pre>

Below <code>&lt;StatusBarBackground&gt;</code> is the actual content. Here, we're wrapping everything in a <code>&lt;ScrollView&gt;</code> to enable the user to scroll vertically if the content goes over the available space. Inside is <code>&lt;StackPanel&gt;</code>, containing all of the weather data that we want to display. This includes the name of the location, the icon representing the current weather, the weather description and the temperature. You can display the variables that we exported earlier by wrapping them in braces. For objects, individual properties are accessed just like you would in JavaScript.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>ScrollView</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>StackPanel</span> <span class="token attr-name">Alignment</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Center<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Text</span> <span class="token attr-name">Value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{weather_data.name }<span class="token punctuation">"</span></span> <span class="token attr-name">FontSize</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>30<span class="token punctuation">"</span></span> <span class="token attr-name">Margin</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>0,20,0,0<span class="token punctuation">"</span></span> <span class="token attr-name">Alignment</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Center<span class="token punctuation">"</span></span> <span class="token attr-name">TextColor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#fff<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Text</span> <span class="token attr-name">Value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{weather_data.icon}<span class="token punctuation">"</span></span> <span class="token attr-name">Alignment</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Center<span class="token punctuation">"</span></span> <span class="token attr-name">Font</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>wi<span class="token punctuation">"</span></span> <span class="token attr-name">FontSize</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>150<span class="token punctuation">"</span></span> <span class="token attr-name">TextColor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#fff<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Text</span> <span class="token attr-name">Value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{weather_data.weather.description}<span class="token punctuation">"</span></span> <span class="token attr-name">FontSize</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>30<span class="token punctuation">"</span></span> <span class="token attr-name">Alignment</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Center<span class="token punctuation">"</span></span> <span class="token attr-name">TextColor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#fff<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>StackPanel</span> <span class="token attr-name">Orientation</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Horizontal<span class="token punctuation">"</span></span> <span class="token attr-name">Alignment</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Center<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Text</span> <span class="token attr-name">Value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{icons.temp}<span class="token punctuation">"</span></span> <span class="token attr-name">Font</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>wi<span class="token punctuation">"</span></span> <span class="token attr-name">FontSize</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>20<span class="token punctuation">"</span></span> <span class="token attr-name">TextColor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#fff<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Text</span> <span class="token attr-name">Value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{weather_data.temperature}<span class="token punctuation">"</span></span> <span class="token attr-name">Margin</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>10,0,0,0<span class="token punctuation">"</span></span> <span class="token attr-name">FontSize</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>20<span class="token punctuation">"</span></span> <span class="token attr-name">TextColor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#fff<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>StackPanel</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>StackPanel</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>ScrollView</span><span class="token punctuation">&gt;</span></span>	
</code></pre>

You might also notice that all attributes and their values are always capitalized; this is the standard in Fuse. Lowercase or uppercase won't really work. Also, notice that <code>Alignment="Center"</code> and <code>TextColor="#fff"</code> are repeated a few times. This is because Fuse doesn't have the concept of inheritance when it comes to styling properties, so setting <code>TextColor</code> or <code>Alignment</code> in a parent component won't actually affect the nested components. This means we need to repeat it for each component. This can be mitigated by creating components and then simply reusing them without specifying the same style properties again. But this isn't really flexible enough, especially if you need a different combination of styles for each component.

The last thing you'll need to do is to open the <code>{your project name}.unoproj</code> file at the root of your project folder. This is the Uno project file. By default, it contains the following:

<pre><code class="language-javascript"><span class="token punctuation">{</span>
  <span class="token string">"RootNamespace"</span><span class="token punctuation">:</span><span class="token string">""</span><span class="token punctuation">,</span>
  <span class="token string">"Packages"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"Fuse"</span><span class="token punctuation">,</span>
    <span class="token string">"FuseJS"</span>
  <span class="token punctuation">]</span><span class="token punctuation">,</span>
  <span class="token string">"Includes"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"*"</span>
  <span class="token punctuation">]</span>
<span class="token punctuation">}</span>	
</code></pre>

This file specifies what packages and files to include in the app's build. By default, it includes the <code>Fuse</code> and <code>FuseJS</code> packages and all of the files in the project directory. If you don't want to include all of the files, edit the items in the <code>Includes</code> array, and use a glob pattern to target specific files:

<pre><code class="language-javascript"><span class="token string">"Includes"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"*.ux"</span><span class="token punctuation">,</span>
    <span class="token string">"js/*.js"</span>
<span class="token punctuation">]</span>	
</code></pre>

You can also use <code>Excludes</code> to blacklist files:

<pre><code class="language-javascript"><span class="token string">"Excludes"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"node_modules/"</span>
<span class="token punctuation">]</span>	
</code></pre>

Going back to the <code>Packages</code>, <code>Fuse</code> and <code>FuseJS</code> allow you to use Fuse-specific libraries. This includes utility functions such as getting the environment in which Fuse is currently running:

<pre><code class="language-javascript"><span class="token keyword">var</span> env <span class="token operator">=</span> <span class="token function">require<span class="token punctuation">(</span></span><span class="token string">'FuseJS/Environment'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span>env<span class="token punctuation">.</span>mobile<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token function">debug_log<span class="token punctuation">(</span></span><span class="token string">"There's geo here!"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>	
</code></pre>

To keep things lightweight, Fuse includes only the very basics. So, you'll need to import things like geolocation as separate packages:

<pre><code class="language-javascript"><span class="token string">"Packages"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"Fuse"</span><span class="token punctuation">,</span>
    <span class="token string">"FuseJS"</span><span class="token punctuation">,</span>
    <span class="token string">"Fuse.GeoLocation"</span>
<span class="token punctuation">]</span><span class="token punctuation">,</span>	
</code></pre>

When it comes to debugging, both React Native and NativeScript tap into Chrome's Developer Tools. If you're coming from a web development background, the debugging workflow should make sense to you. That being said, not all features that you're used to when inspecting and debugging web projects are available. For example, both platforms allow you to debug JavaScript code but don't allow you to inspect the UI elements in the app. React Native has a built-in inspector that is the closest thing to the element inspector in Chrome's Developer Tools. NativeScript currently doesn't have this feature.

On the other hand, Fuse uses the Debugging Protocol in Google's V8 engine to debug JavaScript code. This allows you to do things like add breakpoints to your code and inspect what each object contains at each part in the execution of the code. The Fuse team encourages the use of the <a href="https://code.visualstudio.com/">Visual Studio Code</a> text editor for this, but any text editor or IDE that supports V8's Debugging Protocol should work. If you want to inspect and visually edit the UI elements, Fuse also includes an inspector — although it allows you to adjust only a handful of properties at the moment, things like widths, heights, margins, padding and colors.</p>

## Creating A Weather App With Fuse

Now you're ready to create a simple weather app with Fuse. It will get the user's location via the GeoLocation API and will use the OpenWeatherMap API to determine the weather in the user's location and then display it on the screen. You can find the full source code of the app in the <a href="https://github.com/anchetaWern/fuse-simple-weatherapp">GitHub repository</a>.

To start, go to the OpenWeatherMap website and <a href="https://home.openweathermap.org/users/sign_up">sign up for an account</a>. Once you're done signing up, it should provide you with an API key, which you can use to make a request to its API later on.

Next, visit the <a href="https://www.fusetools.com/downloads">Fuse downloads page</a>, enter your email address, download the Fuse installer for your platform, and then install it. Once it's installed, launch the Fuse dashboard and click on "New Project". This will open another window that will allow you to select the path to your project and enter the project's name.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6235dbc-71d2-48bf-abda-a2f7df118a4b/creating-a-project-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0ff5ef4c-899c-4a6a-814e-e6f515331af4/creating-a-project-opt.png" alt="Creating a new Fuse project" width="500" height="343" /></a><figcaption>Creating a new Fuse project (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6235dbc-71d2-48bf-abda-a2f7df118a4b/creating-a-project-large-preview-opt.png">View large version</a>)</figcaption></figure>

Do that and then click on the "Create" button to create your project. If you're using Sublime Text 3, you can click on the "Open in Sublime Text 3" button to open a new Sublime Text instance with the <a href="https://packagecontrol.io/packages/Fuse">Fuse project</a> already loaded. Once you're in there, the first thing you'll want to do is install the Fuse package. This includes code completion, "Goto definition," previewing the app from Sublime and viewing the build.

Once the Fuse plugin is installed, open the <code>MainView.ux</code> file. This is the main file that we will be working with in this project. By default, it includes sample code for you to play with. Feel free to remove all of the contents of the file once you're done inspecting it.

When you create an app with Fuse, you always start with the <code>&lt;App&gt;</code> tag. This tells Fuse that you want to create a new page.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>App</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>App</span><span class="token punctuation">&gt;</span></span>
</code></pre>

Fuse allows you to reuse icon fonts that are commonly used for the web. Here, we're using <a href="https://erikflowers.github.io/weather-icons/">Weather Icons</a>. Use the <code>&lt;Font&gt;</code> tag to specify the location of the web font file in your app directory via the <code>File</code> attribute. For this project, it's in the <code>fonts</code> folder at the root directory of the project. We also need to give it a <code>ux:Global</code> attribute, which will serve as its ID when you want to use this icon font later on.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Font</span> <span class="token attr-name">File</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>fonts/weather-icons/font/weathericons-regular-webfont.ttf<span class="token punctuation">"</span></span> <span class="token attr-name"><span class="token namespace">ux:</span>Global</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>wi<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
</code></pre>

Next, we have the JavaScript code. We can include JavaScript code anywhere in UX Markup by using the <code>&lt;JavaScript&gt;</code> tag. Inside the tag will be the JavaScript code to be executed.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>JavaScript</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>JavaScript</span><span class="token punctuation">&gt;</span></span>
</code></pre>

In the <code>&lt;JavaScript&gt;</code> tag, require two built-in Fuse libraries: Observable and GeoLocation. Observable allows you to implement data-binding in Fuse. This makes it possible to change the value of the variable via JavaScript code and have it automatically reflected in the UI of the app. Data-binding in Fuse is also two-way; so, if a change is made to a value via the UI, then the value stored in the variable will also be updated, and vice versa.</p>

<pre><code class="language-javascript"><span class="token keyword">var</span> Observable <span class="token operator">=</span> <span class="token function">require<span class="token punctuation">(</span></span><span class="token string">'FuseJS/Observable'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>	
</code></pre>

GeoLocation allows you to get location information from the user's device.</p>

<pre><code class="language-javascript"><span class="token keyword">var</span> Geolocation <span class="token operator">=</span> <span class="token function">require<span class="token punctuation">(</span></span><span class="token string">'FuseJS/GeoLocation'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>	
</code></pre>

Create an object containing the hex code for each of the weather icons that we want to use. You can find the hex code on the <a href="https://erikflowers.github.io/weather-icons/">GitHub page of the icon font</a>.</p>

<pre><code class="language-css"><span class="token selector">var icons = </span><span class="token punctuation">{</span>
   <span class="token string">'clear'</span><span class="token punctuation">:</span> <span class="token string">'\uF00d'</span>,
   <span class="token string">'clouds'</span><span class="token punctuation">:</span> <span class="token string">'\uF002'</span>,
   <span class="token string">'drizzle'</span><span class="token punctuation">:</span> <span class="token string">'\uF009'</span>,
   <span class="token string">'rain'</span><span class="token punctuation">:</span> <span class="token string">'\uF008'</span>,
   <span class="token string">'thunderstorm'</span><span class="token punctuation">:</span> <span class="token string">'\uF010'</span>,
   <span class="token string">'snow'</span><span class="token punctuation">:</span> <span class="token string">'\uF00a'</span>,
   <span class="token string">'mist'</span><span class="token punctuation">:</span> <span class="token string">'\uF0b6'</span>,
   <span class="token string">'fog'</span><span class="token punctuation">:</span> <span class="token string">'\uF003',
</span>   'temp': '\uF055'
<span class="token punctuation">}</span><span class="token punctuation">;</span>	
</code></pre>

Create a function to convert Kelvin to Celsius. We need it because the OpenWeatherMap API returns temperatures in Kelvin.</p>

<pre><code class="language-javascript"><span class="token keyword">function</span> <span class="token function">kelvinToCelsius<span class="token punctuation">(</span></span>kelvin<span class="token punctuation">)</span><span class="token punctuation">{</span>
    <span class="token keyword">return</span> kelvin <span class="token operator">-</span> <span class="token number">273.15</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>	
</code></pre>

Determine whether it's currently day or night based on the time on the user's device. We'll use orange as the background color for the app if it's day, and purple if it's nighttime.</p>

<pre><code class="language-javascript"><span class="token keyword">var</span> hour <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Date</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">getHours<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">var</span> color <span class="token operator">=</span> <span class="token string">'#7417C0'</span><span class="token punctuation">;</span>
<span class="token keyword">if</span><span class="token punctuation">(</span>hour <span class="token operator">&gt;</span><span class="token operator">=</span> <span class="token number">5</span> <span class="token operator">&amp;&amp;</span> hour <span class="token operator">&lt;</span><span class="token operator">=</span> <span class="token number">18</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
    color <span class="token operator">=</span> <span class="token string">'#f38844'</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>	
</code></pre>

Add the OpenWeather Map API key that you got earlier and create an observable variable that contains the weather data.</p>

<pre><code class="language-javascript"><span class="token keyword">var</span> api_key <span class="token operator">=</span> <span class="token string">'YOUR OPENWEATHERMAP API KEY'</span><span class="token punctuation">;</span>
<span class="token keyword">var</span> weather_data <span class="token operator">=</span> <span class="token function">Observable<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>	
</code></pre>

Get the location information:

<pre><code class="language-javascript"><span class="token keyword">var</span> loc <span class="token operator">=</span> Geolocation<span class="token punctuation">.</span>location<span class="token punctuation">;</span>	
</code></pre>

This will return an object containing the <code>latitude</code>, <code>longitude</code> and <code>accuracy</code> of the location. However, Fuse currently has a problem with getting location information on Android. If the location setting is disabled on the device, it won't ask you to enable it when you open the app. So, as a workaround, you'll need to first enable location before launching the app.

Make a request to the OpenWeatherMap API using the <code>fetch()</code> function. This function is available in Fuse's global scope, so you can call it from anywhere without including any additional libraries. This will work the same way as the <code>fetch()</code> function available in modern browsers: It also returns a promise that you need to listen to using the <code>then()</code> function. When the supplied callback function is executed, the raw response is passed in as an argument. You can't really use this yet since it contains the whole response object. To extract the data that the API actually returned, you need to call the <code>json()</code> function in the response object. This will return another promise, so you need to use <code>then()</code> one more time to extract the actual data. The data is then assigned as the value of the observable that we created earlier.</p>

<pre><code class="language-javascript"><span class="token keyword">var</span> req_url <span class="token operator">=</span> <span class="token string">'https://api.openweathermap.org/data/2.5/weather?lat='</span> <span class="token operator">+</span> loc<span class="token punctuation">.</span>latitude <span class="token operator">+</span> <span class="token string">'&amp;lon='</span> <span class="token operator">+</span> loc<span class="token punctuation">.</span>longitude <span class="token operator">+</span> <span class="token string">'&amp;apikey='</span> <span class="token operator">+</span> api_key<span class="token punctuation">;</span>
<span class="token function">fetch<span class="token punctuation">(</span></span>req_url<span class="token punctuation">)</span>
<span class="token punctuation">.</span><span class="token function">then<span class="token punctuation">(</span></span><span class="token keyword">function</span><span class="token punctuation">(</span>response<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> response<span class="token punctuation">.</span><span class="token function">json<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token punctuation">.</span><span class="token function">then<span class="token punctuation">(</span></span><span class="token keyword">function</span><span class="token punctuation">(</span>responseObject<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    weather_data<span class="token punctuation">.</span>value <span class="token operator">=</span> <span class="token punctuation">{</span>
        name<span class="token punctuation">:</span> responseObject<span class="token punctuation">.</span>name<span class="token punctuation">,</span>
        icon<span class="token punctuation">:</span> icons<span class="token punctuation">[</span>responseObject<span class="token punctuation">.</span>weather<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">.</span>main<span class="token punctuation">.</span><span class="token function">toLowerCase<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        weather<span class="token punctuation">:</span> responseObject<span class="token punctuation">.</span>weather<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        temperature<span class="token punctuation">:</span> <span class="token function">kelvinToCelsius<span class="token punctuation">(</span></span>responseObject<span class="token punctuation">.</span>main<span class="token punctuation">.</span>temp<span class="token punctuation">)</span>  <span class="token operator">+</span> <span class="token string">' °C'</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>	
</code></pre>

For your reference, here's a sample response returned by the API:

<pre><code class="language-javascript"><span class="token punctuation">{</span>
   <span class="token string">"coord"</span><span class="token punctuation">:</span><span class="token punctuation">{</span>
      <span class="token string">"lon"</span><span class="token punctuation">:</span><span class="token number">120.98</span><span class="token punctuation">,</span>
      <span class="token string">"lat"</span><span class="token punctuation">:</span><span class="token number">14.6</span>
   <span class="token punctuation">}</span><span class="token punctuation">,</span>
   <span class="token string">"weather"</span><span class="token punctuation">:</span><span class="token punctuation">[</span>
      <span class="token punctuation">{</span>
         <span class="token string">"id"</span><span class="token punctuation">:</span><span class="token number">803</span><span class="token punctuation">,</span>
         <span class="token string">"main"</span><span class="token punctuation">:</span><span class="token string">"Clouds"</span><span class="token punctuation">,</span>
         <span class="token string">"description"</span><span class="token punctuation">:</span><span class="token string">"broken clouds"</span><span class="token punctuation">,</span>
         <span class="token string">"icon"</span><span class="token punctuation">:</span><span class="token string">"04d"</span>
      <span class="token punctuation">}</span>
   <span class="token punctuation">]</span><span class="token punctuation">,</span>
   <span class="token string">"base"</span><span class="token punctuation">:</span><span class="token string">"stations"</span><span class="token punctuation">,</span>
   <span class="token string">"main"</span><span class="token punctuation">:</span><span class="token punctuation">{</span>
      <span class="token string">"temp"</span><span class="token punctuation">:</span><span class="token number">304.15</span><span class="token punctuation">,</span>
      <span class="token string">"pressure"</span><span class="token punctuation">:</span><span class="token number">1009</span><span class="token punctuation">,</span>
      <span class="token string">"humidity"</span><span class="token punctuation">:</span><span class="token number">74</span><span class="token punctuation">,</span>
      <span class="token string">"temp_min"</span><span class="token punctuation">:</span><span class="token number">304.15</span><span class="token punctuation">,</span>
      <span class="token string">"temp_max"</span><span class="token punctuation">:</span><span class="token number">304.15</span>
   <span class="token punctuation">}</span><span class="token punctuation">,</span>
   <span class="token string">"visibility"</span><span class="token punctuation">:</span><span class="token number">10000</span><span class="token punctuation">,</span>
   <span class="token string">"wind"</span><span class="token punctuation">:</span><span class="token punctuation">{</span>
      <span class="token string">"speed"</span><span class="token punctuation">:</span><span class="token number">7.2</span><span class="token punctuation">,</span>
      <span class="token string">"deg"</span><span class="token punctuation">:</span><span class="token number">260</span>
   <span class="token punctuation">}</span><span class="token punctuation">,</span>
   <span class="token string">"clouds"</span><span class="token punctuation">:</span><span class="token punctuation">{</span>
      <span class="token string">"all"</span><span class="token punctuation">:</span><span class="token number">75</span>
   <span class="token punctuation">}</span><span class="token punctuation">,</span>
   <span class="token string">"dt"</span><span class="token punctuation">:</span><span class="token number">1473051600</span><span class="token punctuation">,</span>
   <span class="token string">"sys"</span><span class="token punctuation">:</span><span class="token punctuation">{</span>
      <span class="token string">"type"</span><span class="token punctuation">:</span><span class="token number">1</span><span class="token punctuation">,</span>
      <span class="token string">"id"</span><span class="token punctuation">:</span><span class="token number">7706</span><span class="token punctuation">,</span>
      <span class="token string">"message"</span><span class="token punctuation">:</span><span class="token number">0.0115</span><span class="token punctuation">,</span>
      <span class="token string">"country"</span><span class="token punctuation">:</span><span class="token string">"PH"</span><span class="token punctuation">,</span>
      <span class="token string">"sunrise"</span><span class="token punctuation">:</span><span class="token number">1473025458</span><span class="token punctuation">,</span>
      <span class="token string">"sunset"</span><span class="token punctuation">:</span><span class="token number">1473069890</span>
   <span class="token punctuation">}</span><span class="token punctuation">,</span>
   <span class="token string">"id"</span><span class="token punctuation">:</span><span class="token number">1701668</span><span class="token punctuation">,</span>
   <span class="token string">"name"</span><span class="token punctuation">:</span><span class="token string">"Manila"</span><span class="token punctuation">,</span>
   <span class="token string">"cod"</span><span class="token punctuation">:</span><span class="token number">200</span>
<span class="token punctuation">}</span>	
</code></pre>

Export the variables so that it becomes available in the UI.</p>

<pre><code class="language-javascript">module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{</span>
    weather_data<span class="token punctuation">:</span> weather_data<span class="token punctuation">,</span>
    icons<span class="token punctuation">:</span> icons<span class="token punctuation">,</span>
    color<span class="token punctuation">:</span> color
<span class="token punctuation">}</span><span class="token punctuation">;</span>	
</code></pre>

Because this project is very small, I've decided to put everything in one file. But for real projects, the JavaScript code and the UX Markup should be separated. This is because the designers are the ones who normally work with UX Markup, and the developers are the ones who touch the JavaScript code. Separating the two allows the designer and the developer to work on the same page at the same time. You can separate the JavaScript code by creating a new JavaScript file in the project folder and then link it in your markup, like so:

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>JavaScript</span> <span class="token attr-name">File</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>js/weather.js<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>	
</code></pre>

Finally, add the actual UI of the app. Here, we're using <code>&lt;DockPanel&gt;</code> to wrap all of the elements. By default, <code>&lt;DockPanel&gt;</code> has a <code>Dock</code> property that is set to <code>Fill</code>, so it's the perfect container for filling the entire screen with content. Note that we didn't need to set that property below because it's implicitly added. Below, we have only assigned a <code>Color</code> attribute, which allows us to set the background color using the color that we exported earlier.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>DockPanel</span> <span class="token attr-name">Color</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{color}<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>DockPanel</span><span class="token punctuation">&gt;</span></span>	
</code></pre>

Inside <code>&lt;DockPanel&gt;</code> is <code>&lt;StatusBarBackground&gt;</code>, which we'll dock to the top of the screen. This allows us to show and customize the status bar on the user's device. If you don't use this component, <code>&lt;DockPanel&gt;</code> will consume the entirety of the screen, including the status bar. Simply setting this component will make the status bar visible. We don't really want to customize it, so we'll just leave the defaults.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>StatusBarBackground</span> <span class="token attr-name">Dock</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Top<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>	
</code></pre>

Below <code>&lt;StatusBarBackground&gt;</code> is the actual content. Here, we're wrapping everything in a <code>&lt;ScrollView&gt;</code> to enable the user to scroll vertically if the content goes over the available space. Inside is <code>&lt;StackPanel&gt;</code>, containing all of the weather data that we want to display. This includes the name of the location, the icon representing the current weather, the weather description and the temperature. You can display the variables that we exported earlier by wrapping them in braces. For objects, individual properties are accessed just like you would in JavaScript.</p>

<pre><code class="language-markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>ScrollView</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>StackPanel</span> <span class="token attr-name">Alignment</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Center<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Text</span> <span class="token attr-name">Value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{weather_data.name }<span class="token punctuation">"</span></span> <span class="token attr-name">FontSize</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>30<span class="token punctuation">"</span></span> <span class="token attr-name">Margin</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>0,20,0,0<span class="token punctuation">"</span></span> <span class="token attr-name">Alignment</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Center<span class="token punctuation">"</span></span> <span class="token attr-name">TextColor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#fff<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Text</span> <span class="token attr-name">Value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{weather_data.icon}<span class="token punctuation">"</span></span> <span class="token attr-name">Alignment</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Center<span class="token punctuation">"</span></span> <span class="token attr-name">Font</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>wi<span class="token punctuation">"</span></span> <span class="token attr-name">FontSize</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>150<span class="token punctuation">"</span></span> <span class="token attr-name">TextColor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#fff<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Text</span> <span class="token attr-name">Value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{weather_data.weather.description}<span class="token punctuation">"</span></span> <span class="token attr-name">FontSize</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>30<span class="token punctuation">"</span></span> <span class="token attr-name">Alignment</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Center<span class="token punctuation">"</span></span> <span class="token attr-name">TextColor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#fff<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>StackPanel</span> <span class="token attr-name">Orientation</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Horizontal<span class="token punctuation">"</span></span> <span class="token attr-name">Alignment</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Center<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Text</span> <span class="token attr-name">Value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{icons.temp}<span class="token punctuation">"</span></span> <span class="token attr-name">Font</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>wi<span class="token punctuation">"</span></span> <span class="token attr-name">FontSize</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>20<span class="token punctuation">"</span></span> <span class="token attr-name">TextColor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#fff<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
            <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>Text</span> <span class="token attr-name">Value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>{weather_data.temperature}<span class="token punctuation">"</span></span> <span class="token attr-name">Margin</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>10,0,0,0<span class="token punctuation">"</span></span> <span class="token attr-name">FontSize</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>20<span class="token punctuation">"</span></span> <span class="token attr-name">TextColor</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>#fff<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
        <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>StackPanel</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>StackPanel</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>ScrollView</span><span class="token punctuation">&gt;</span></span>	
</code></pre>

You might also notice that all attributes and their values are always capitalized; this is the standard in Fuse. Lowercase or uppercase won't really work. Also, notice that <code>Alignment="Center"</code> and <code>TextColor="#fff"</code> are repeated a few times. This is because Fuse doesn't have the concept of inheritance when it comes to styling properties, so setting <code>TextColor</code> or <code>Alignment</code> in a parent component won't actually affect the nested components. This means we need to repeat it for each component. This can be mitigated by creating components and then simply reusing them without specifying the same style properties again. But this isn't really flexible enough, especially if you need a different combination of styles for each component.

The last thing you'll need to do is to open the <code>{your project name}.unoproj</code> file at the root of your project folder. This is the Uno project file. By default, it contains the following:

<pre><code class="language-javascript"><span class="token punctuation">{</span>
  <span class="token string">"RootNamespace"</span><span class="token punctuation">:</span><span class="token string">""</span><span class="token punctuation">,</span>
  <span class="token string">"Packages"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"Fuse"</span><span class="token punctuation">,</span>
    <span class="token string">"FuseJS"</span>
  <span class="token punctuation">]</span><span class="token punctuation">,</span>
  <span class="token string">"Includes"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"*"</span>
  <span class="token punctuation">]</span>
<span class="token punctuation">}</span>	
</code></pre>

This file specifies what packages and files to include in the app's build. By default, it includes the <code>Fuse</code> and <code>FuseJS</code> packages and all of the files in the project directory. If you don't want to include all of the files, edit the items in the <code>Includes</code> array, and use a glob pattern to target specific files:

<pre><code class="language-javascript"><span class="token string">"Includes"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"*.ux"</span><span class="token punctuation">,</span>
    <span class="token string">"js/*.js"</span>
<span class="token punctuation">]</span>	
</code></pre>

You can also use <code>Excludes</code> to blacklist files:

<pre><code class="language-javascript"><span class="token string">"Excludes"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"node_modules/"</span>
<span class="token punctuation">]</span>	
</code></pre>

Going back to the <code>Packages</code>, <code>Fuse</code> and <code>FuseJS</code> allow you to use Fuse-specific libraries. This includes utility functions such as getting the environment in which Fuse is currently running:

<pre><code class="language-javascript"><span class="token keyword">var</span> env <span class="token operator">=</span> <span class="token function">require<span class="token punctuation">(</span></span><span class="token string">'FuseJS/Environment'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span>env<span class="token punctuation">.</span>mobile<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token function">debug_log<span class="token punctuation">(</span></span><span class="token string">"There's geo here!"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>	
</code></pre>

To keep things lightweight, Fuse includes only the very basics. So, you'll need to import things like geolocation as separate packages:

<pre><code class="language-javascript"><span class="token string">"Packages"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"Fuse"</span><span class="token punctuation">,</span>
    <span class="token string">"FuseJS"</span><span class="token punctuation">,</span>
    <span class="token string">"Fuse.GeoLocation"</span>
<span class="token punctuation">]</span><span class="token punctuation">,</span>	
</code></pre>

Once <code>Fuse.GeoLocation</code> has been added, Fuse will add the necessary libraries and permissions to the app once you've compiled the project.</p>

### Running the App

You can run the app via the Fuse dashboard by selecting the project and clicking on the "Preview" button.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/718b817f-14c5-46e7-aadf-403964f27b5a/running-the-app-large-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f91fb78-71cf-418d-8ed7-fe581c3d6357/running-the-app-opt.png" alt="Running the app" width="500" height="341" /></a><figcaption>Running the app (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/718b817f-14c5-46e7-aadf-403964f27b5a/running-the-app-large-preview-opt.png">View large version</a>)</figcaption></figure>

This lets you pick whether to run on Android, iOS or locally. (Note that there is no iOS option in the screenshot because I'm running on Windows.) Select "Local" for now, and then click on "Start." This should show you a blank screen because geolocation won't really work in a local preview. What you can do is close the preview then update the <code>req_url</code> to use the following instead, which allows you to specify a place instead of the coordinates:

<pre><code class="language-javascript"><span class="token keyword">var</span> req_url <span class="token operator">=</span> <span class="token string">'https://api.openweathermap.org/data/2.5/weather?q=london,uk&amp;apikey='</span> <span class="token operator">+</span> api_key<span class="token punctuation">;</span>
</code></pre>

You'll also need to comment out all of the code that uses geolocation:

<pre><code class="language-javascript"><span class="token comment">//var Geolocation = require('FuseJS/GeoLocation');
</span><span class="token comment">//var loc = Geolocation.location;
</span><span class="token comment">//var req_url = 'https://api.openweathermap.org/data/2.5/weather?lat=' + loc.latitude + '&amp;lon=' + loc.longitude + '&amp;apikey=' + api_key;
</span></code></pre>

Run the app again, and it should show you something similar to the screenshot at the beginning of the article.

If you want to run on a real device, please check "<a href="https://www.fusetools.com/docs/basics/preview-and-export">Preview and Export</a>" in the documentation. It contains detailed information on how to deploy your app to both Android and iOS devices.</p>

## Pros And Cons Of Fuse

Now that you have tested the waters, it's time to look at some of the pros and cons of using Fuse for your next mobile app project. As you have seen so far, Fuse is both developer- and designer-friendly, because of its real-time updates and multi-device preview feature, which enables developers and designers to work at the same time. Combine that with the native UX and access to device features, and you've got yourself a complete platform for building cross-platform apps. This section will drive home the point on why you should (or shouldn't) use Fuse for your next mobile app project. First, let's look at the advantages.</p>

### Developer- and Designer-Friendly

Fuse is developer-friendly because it uses JavaScript for the business logic. This makes it a very approachable platform for creating apps, especially for web developers and people who have some JavaScript experience. In addition, it plays nice with JavaScript transpilers such as Babel. This means that developers can use new <a href="https://www.smashingmagazine.com/2015/10/es6-whats-new-next-version-javascript/">ECMAScript 6</a> features to create Fuse apps.

At the same time, Fuse is designer-friendly because it allows you to import assets from tools such as Sketch, and it will automatically take care of slicing and exporting the pieces for you.

Aside from that, Fuse clearly separates the business logic and presentation code. The structure, styles and animations are all done in UX Markup. This means that business-logic code can be placed in a separate file and simply linked from the app page. The designer can then focus on designing the user experience. Being able to implement animations using UX Markup makes things simpler and easier for the designer.</p>

### Focus on Collaboration and Productivity

Fuse makes it very easy for designers and developers to collaborate in real time. It allows for simultaneous previewing of the app on multiple devices. You only need USB the first time you connect the device. Once the device has been connected, all you need to do is connect the device to the same Wi-Fi network as your development machine, and all your changes will be automatically reflected on all devices where the app is open. The sweetest part is that changes get pushed to all the devices almost instantly. And it works not just on code changes: Any change you make on any linked asset (such as images) will trigger the app to reload as well.

Fuse also comes with a preview feature that allows you to test changes without a real device. It's like an emulator but a lot faster. In "design mode," you can edit the appearance of the app using the graphical user interface. Developers will also benefit from the logging feature, which allows them to easily debug the app if there are any errors.</p>

### Very Extendable

If you need functionality not already provided by the Fuse libraries, Fuse also allows you to implement the functionality yourself using Uno. Uno is a language created by the Fuse team itself. It's a sub-language of C# that compiles to C++. This is Fuse's way of letting you access the native APIs of each platform (Android and iOS).</p>

### Native-Like UI Performance

UX Markup is converted to the native UI equivalent at compile time. This makes the UI really snappy and is comparable to native performance. And because animations are also written declaratively using UX Markup, animations are done natively as well. Behind the scenes, Fuse uses <a href="https://en.wikipedia.org/wiki/OpenGL_ES">OpenGL ES</a> acceleration to make things fast.</p>

### Cons

No tool is perfect, and Fuse is no exception. Here are a few things to consider before picking Fuse.
<ul>
 	<li>Structure and style are mixed together. This makes the code a bit difficult to edit because you have to specify styles separately for each element. This can be alleviated by creating components in which you put common styles.</li>
 	<li>Linux is not supported, and it's not currently on the road map. Though Linux developers who want to try out Fuse can still use a Windows Virtual Machine or Wine to install and use Fuse on their machine.</li>
 	<li>It's still in beta, which means it's still rough around the edges and not all the features that you might expect from a mobile app development platform is supported. That said, Fuse is very stable and does a good job at the small set of features that it currently supports.</li>
 	<li>It's not open-source, though there are plans to open-source the core Fuse platform. This doesn't mean that you can't use Fuse for anything though. You can freely use Fuse to create production apps. If you're interested about licensing, you can read more about it in the <a href="https://res.cloudinary.com/fusetools/raw/upload/staticwebsitecontent_v2/f904f85bf03ee6f2898f99d78777d445__media/fuse_developer_preview_license_agreement.pdf">Fuse License Agreement.</a></li>
</ul>

## Final Thoughts

We've learned about Fuse, a newcomer in the world of JavaScript native app development. From what I've seen so far, I can say that this project has a lot of potential. It really shines in multi-device support and animation. And the fact that it's both designer- and developer-friendly makes it a great tool for developing cross-platform apps.</p>

### Further Learning

<ul>
 	<li><a href="https://www.fusetools.com/docs">Fuse documentation</a>
There's no better place to learn about a new technology than the official documentation.</li>
 	<li>"<a href="https://www.youtube.com/playlist?list=PLdlqWm6b-XALJgM3fGa4q95Yipsgb8Q1o">Learning Fuse</a>," YouTube
If you learn better through videos, the Fuse team has put together this YouTube playlist to help you learn about the features that Fuse offers.</li>
 	<li>"<a href="https://medium.com/@fusetools/how-fuse-differs-from-react-native-and-nativescript-525344f02aaf#.iqhv9p5oo">How Fuse Differs From React Native and NativeScript</a>," Remi Pedersen, Medium
Learn the technical differences between Fuse and React Native and NativeScript.</li>
</ul>

{{< signature "da, vf, yk, al, il" >}}


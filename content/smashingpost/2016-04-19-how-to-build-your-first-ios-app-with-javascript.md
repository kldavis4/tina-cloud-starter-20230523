---
title: >-
  The Beauty Of React Native: Building Your First iOS App With JavaScript (Part
  2)
slug: how-to-build-your-first-ios-app-with-javascript
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e3d54f4-362e-4e44-a40d-825fb3e9c071/high5-featured-3.jpg
date: 2016-04-19T19:00:08.000Z
author: nashvail
description: >-
  In [part
  1](https://www.smashingmagazine.com/2016/04/the-beauty-of-react-native-building-your-first-ios-app-with-javascript-part-1/)
  of this tutorial we started building our iOS app from scratch. We started out
  by setting up a blank React Native project. Then we pulled data from the
  Unsplash.it API. Because downloading data takes time, we built a loading
  screen.

  In the process we went over positioning UI elements with flexbox and styling
  them using CSS-like properties. Towards the end of part 1 we downloaded and
  included a third-party `Swiper` component from GitHub, which allowed us to
  display wallpaper data in a swipeable container.
categories:
  - Coding
  - Mobile
  - JavaScript
  - Apps
  - iOS
  - Native
  - React
---
In <a href="https://www.smashingmagazine.com/2016/04/the-beauty-of-react-native-building-your-first-ios-app-with-javascript-part-1/">part 1 of this tutorial</a>, we started building our iOS app from scratch. We started out by setting up a blank React Native project. Then we pulled data from the Unsplash.it API.

Because downloading data takes time, we built a loading screen. In the process we went over positioning UI elements with <a href="https://www.smashingmagazine.com/2016/02/the-flexbox-reading-list/">flexbox</a> and styling them using CSS-like properties. Towards the end of part 1 we downloaded and included a third-party <code>Swiper</code> component from GitHub, which allowed us to display wallpaper data in a swipeable container.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2016/04/the-beauty-of-react-native-building-your-first-ios-app-with-javascript-part-1/#further-reading-on-smashingmag)

*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Internationalizing React Apps](https://www.smashingmagazine.com/2017/01/internationalizing-react-apps/)

It doesn't do much yet but that's all about to change. In this part of the tutorial we will start by replacing the photographer’s name with the actual wallpaper image along with proper credits. During this process you'll learn how to link a library in Xcode, as well as more on general styling and positioning of UI elements. Then we will go over building a custom double-tap listener using the PanResponder API and a little bit of math. Toward the end you will learn how to save pictures to the Camera Roll and also how to run your app on a physical device. To apply all your newly learned React Native skills there is a challenge waiting for you at the end.

{{% feature-panel %}}

Just like the first part, this article has five sections. Completing each section takes us a step closer to finishing our app.</p>

## 1\. Displaying Wallpapers And Credits

Let’s take a look at the data each wallpaper object holds. Consider the following sample data.</p>

<pre><code class="language-javascript">{
	author: "Patryk Sobczak"
	author_url: "https://unsplash.com/patryksobczak"
	filename: "0611_bS92UkQY8xI.jpeg"
	format: "jpeg"
	height: 1280
	id: 611
	post_url: "https://unsplash.com/photos/bS92UkQY8xI"
	width: 1920
}</code></pre>

To look at the wallpaper you can point your browser to <code>https://unsplash.it/{width}/{height}?image={id}</code> which translates to <a href="https://unsplash.it/1920/1280?image=611"><code>https://unsplash.it/1920/1280?image=611</code></a> in this case. That is one high-quality wallpaper.

Since we’re able to construct a URL for the image, we can add an <code>Image</code> component with proper <code>source</code> attribute.

But let’s not get ahead of ourselves. Wallpapers that we pull from Unsplash are high quality and may take time to load. If we simply use React Native’s <code>Image</code> component we will leave our users staring at a blank screen while the wallpaper loads. We need a progress bar-like component here – luckily, there is a component for just that.

The two components we will use to achieve our goal are <a href="https://github.com/oblador/react-native-image-progress">react-native-image-progress</a> and <a href="https://github.com/oblador/react-native-progress">react-native-progress</a>.

Head over to the project directory from terminal and run the following two commands:

<pre><code>npm install --save react-native-image-progress</code></pre>

<pre><code>npm install --save react-native-progress</code></pre>

Let's import these into our <i>index.ios.js</i> file. Add the following two lines right below the <code>use strict;</code> statement:

<pre><code class="language-javascript">var NetworkImage = require('react-native-image-progress');
var Progress = require('react-native-progress');</code></pre>

Since our wallpaper images cover the whole viewport, we will need to know the width and height of the viewport. To do that add:

<pre><code class="language-javascript">var {width, height} = React.Dimensions.get('window’);</code></pre>

outside the class declaration and right below the import statements. If you have been following carefully you’ll of course know that we can substitute <code>React.Dimensions</code> with <code>Dimensions</code> by adding a new line to the React import code block.</p>

<pre><code class="language-javascript">var {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  Component,
  ActivityIndicatorIOS,
/***/
  Dimensions // Add this line
/***/
} = React;</code></pre>

Just saving a couple of keystrokes, y'know.

Now, we will use the <code>NetworkImage</code> component in <code>renderResults</code>.</p>

<pre><code class="language-javascript">&lt;Swiper ... &gt;
  {wallsJSON.map((wallpaper, index) =&gt; {
    return(
    /***/
      &lt;View key={index}&gt;
        &lt;NetworkImage
          source={{uri: `https://unsplash.it/${wallpaper.width}/${wallpaper.height}?image=${wallpaper.id}`}}
          indicator={Progress.Circle}
          style={styles.wallpaperImage}&gt;
        &lt;/NetworkImage&gt;
      &lt;/View&gt;
    /***/
    );
  })}
&lt;/Swiper&gt;</code></pre>

Notice the value that <code>uri</code> holds inside <code>NetworkImage</code>’s <code>source</code> attribute. This is one of ES2015’s new features called <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/template_strings">template strings</a>. Template strings allow you to include variables right inside the string using <code>${variableName}</code> instead of concatenating them again and again using <code>+</code>.

I'll tell you again. ES2015 <em>is</em> pretty cool!

Add the following style definition to the <code>styles</code> variable:

<pre><code class="language-javascript">wallpaperImage: {
  flex: 1,
  width: width,
  height: height,
  backgroundColor: ‘#000’
}</code></pre>

Refresh the simulator and you should end up with a bunch of errors. Don't worry, we didn't break anything. The compiler is just complaining about a library it needs and cannot find. Let's help the compiler out.

Taking a closer look at the code we just added, notice one of the <code>NetworkImage</code>’s properties is <code>indicator</code> and it holds the value of <code>Progress.Circle</code>. As mentioned in the component’s docs on GitHub (don’t tell me you didn’t <a href="https://github.com/oblador/react-native-progress">read the docs</a>) <code>Progress.Circle</code> requires ReactART, which is a library to draw vector graphics using React. We don’t need to download anything new here, just include it in our project, this time through Xcode.

Clicking on any of the images below will point you to a larger version of that image, which will give you a better idea of what's going on.

Concentrate and pay close attention here.

Head to the following path from the root of the project: <i>node_modules/react-native/Libraries/ART/</i>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bca4830-01c6-4f3b-8b79-b0b983a01bde/fig16-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bca4830-01c6-4f3b-8b79-b0b983a01bde/fig16-react-native-preview-opt.png" alt="Path to ART library." /></a><figcaption>Path to ART library.</figcaption></figure>

<figure>See the <i>ART.xcodeproj</i> file? Drag that to Xcode under <i>SplashWalls/Libraries</i>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3167e6d2-c774-4afb-81c1-0151e328583d/fig17-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3167e6d2-c774-4afb-81c1-0151e328583d/fig17-react-native-preview-opt.png" />Libraries." /&gt;</a><figcaption>Drag ART.xcodeproj to SplashWalls/Libraries.</figcaption></figure><figure>Next, click on <strong>Build Phases</strong> located at the top along with <strong>General</strong>, <strong>Capabilities</strong> and others.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/096a105f-d39d-4550-9c2f-92c470e4ab5f/fig18-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/096a105f-d39d-4550-9c2f-92c470e4ab5f/fig18-react-native-preview-opt.png" alt="Location of Build Phases." /></a><figcaption>Location of Build Phases.</figcaption></figure><figure>Then, drag <i>libART.a</i> from under <i>ART.xcodeproj/Products</i> into <i>Link Binary With Libraries</i>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2dbe3f0-df77-452a-9772-c6932eed2616/fig19-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b2dbe3f0-df77-452a-9772-c6932eed2616/fig19-react-native-preview-opt.png" alt="Drag libART.a to Link Binary with Libraries." /></a><figcaption>Drag libART.a to Link Binary with Libraries.</figcaption></figure><figure>(Side note: generally inside the <i>Products</i> folder of React Native <i>Libraries</i> you will find a single <i>.a</i> file. For the libraries we will be linking in the future, make sure you drag the only <i>.a</i> file inside the <i>Products</i> folder into <i>Link Binary With Libraries</i>.)

That’s all. Linking libraries is such a drag (Pun Counter: 1).

Now, refresh the simulator. Cool! We already have the wallpapers showing up with loading indicators, and you can swipe through them. Feel like downloading one? Hold your horses, we're getting there.

The progress indicator currently follows the default color scheme and aesthetics. Let's change that. This is done by adding a new property <code>indicatorProps</code> to the <code>NetworkImage</code> component.</p>

<pre><code class="language-javascript">&lt;NetworkImage
  source={{uri: `https://unsplash.it/${wallpaper.width}/${wallpaper.height}?image=${wallpaper.id}`}}
  indicator={Progress.Circle}
  style={styles.wallpaperImage}&gt;
  /***/
  indicatorProps={{
    color: 'rgba(255, 255, 255)',
    size: 60,
    thickness: 7
  }}
  /***/
&lt;/NetworkImage&gt;</code></pre>

This will make the loading indicator look like this:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd51a27d-91a3-4308-acb4-34422e5b52e0/fig20-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd51a27d-91a3-4308-acb4-34422e5b52e0/fig20-react-native-preview-opt.png" alt="Image loading indicator." /></a><figcaption>Image loading indicator.</figcaption></figure><figure>Feel free to play around with the values. <em>Whatever makes you happy, whatever you want.</em> (10 internet points if you get the reference :-) )

Let's now add the picture credits. Insert two text components between the the opening and closing tags of <code>&lt;NetworkImage&gt;</code> as shown below.</p>

<pre><code class="language-javascript">&lt;NetworkImage
...
&gt;
/***/
    &lt;Text style={styles.label}&gt;Photo by&lt;/Text&gt;
    &lt;Text style={styles.label_authorName}&gt;{wallpaper.author}&lt;/Text&gt;
/***/
&lt;/NetworkImage&gt;</code></pre>

and add the following styles to the <code>styles</code> variable as well:

<pre><code class="language-javascript">label: {
  position: 'absolute',
  color: '#fff',
  fontSize: 13,
  backgroundColor: 'rgba(0, 0, 0, 0.8)',
  padding: 2,
  paddingLeft: 5,
  top: 20,
  left: 20,
  width: width/2
},
label_authorName: {
  position: 'absolute',
  color: '#fff',
  fontSize: 15,
  backgroundColor: 'rgba(0, 0, 0, 0.8)',
  padding: 2,
  paddingLeft: 5,
  top: 41,
  left: 20,
  fontWeight: 'bold',
  width: width/2
}</code></pre>

Refresh the simulator and Bam! We have the photo credits.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f729ef2d-14d9-42f4-a689-b892b5edc59b/fig21-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f729ef2d-14d9-42f4-a689-b892b5edc59b/fig21-react-native-preview-opt.png" alt="Wallpaper image with credits." /></a><figcaption>Wallpaper image with credits.</figcaption></figure><figure>Everything we did to add the photo credits is very straightforward. I don’t think there is anything to explain here, right?

With that, we’re done with this section. Now it's time to go through what I believe is the toughest section of the whole tutorial.
## 2. Detecting Double-Taps

In this section we will venture into the lands of PanResponder API. This API will help us do some really cool things like detect a double-tap.

If we'd wanted, we could have just put a download button over the wallpaper: tap the download button and download the wallpaper. But that’s not what grown-ups do. We will design our custom double-tap listener, listen for double-taps, and then download the image.

Before getting started, you could read about the <a href="https://facebook.github.io/react-native/docs/panresponder.html">PanResponder API</a>. I didn’t find it very helpful, though. It will all make sense once we start using the API. While we’re at it, you should know that React Native provides us with two APIs to handle touch and gestures: <a href="https://facebook.github.io/react-native/docs/gesture-responder-system.html">GestureResponder</a> and PanResponder. PanResponder is the higher-level API and more convenient to use, so we will stick with it.

Enough talking, let’s get our hands dirty. Inside the <code>SplashWall</code>'s constructor we’ll declare a blank object literal. Write the following line just after <code>this.state</code>'s closing brace:

<pre><code class="language-javascript">this.imagePanResponder = {};</code></pre>

Then add <code>PanResponder</code> in the imports block.</p>

<pre><code class="language-javascript">var {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  Component,
  ActivityIndicatorIOS,
  Dimensions,
/***/
  PanResponder
/***/
} = React;</code></pre>

As of now, our <code>imagePanResponder</code> is just an empty object literal, there is nothing special about it. What we need to do is convert it to a <code>PanResponder</code> and then wire it to our <code>&lt;NetworkImage&gt;</code> component, since that is the component we would like to detect double-taps on.

First, let's make our empty object literal special. For that, we will write a new lifecycle method, <code>componentWillMount</code>. This method is automatically fired right before initial rendering occurs.</p>

<pre><code class="language-javascript">componentWillMount() {
    this.imagePanResponder = PanResponder.create({
      onStartShouldSetPanResponder: this.handleStartShouldSetPanResponder,
      onPanResponderGrant: this.handlePanResponderGrant,
      onPanResponderRelease: this.handlePanResponderEnd,
      onPanResponderTerminate: this.handlePanResponderEnd
    });
  }
</code></pre>

Then we wire our <code>imagePanResponder</code> to the <code>NetworkImage</code> component like so:

<pre><code class="language-javascript">&lt;NetworkImage
		.
		.
		.
     {...this.imagePanResponder.panHandlers}&gt;</code></pre>

The three dots before <code>this.imagePanResponder.panHandlers</code> are what is called the <em>spread operator</em>. If you’re not familiar with it already, you can <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Spread_operator">read more about it</a> on the Mozilla Developer Network.

To understand what’s going on we will need to dive a little deeper into the PanResponder API.

Any touch event has three stages: <em>start</em>, <em>move</em>, and <em>release</em>; and a View/Component can claim to be the one that responds to a particular touch event. Notice the first key inside <code>PanResponder.create({...</code> that says <code>onStartShouldSetPanResponder</code>. As the name suggests, this is as though React Native asks if it should set PanResponder on this view when a touch is registered or started on it. In other words, should this view try to claim <em>touch responder</em> status.

We set this key’s value to <code>this.handleOnStartShouldSetPanResponder</code>, which is a method that will return true if we wanted the View to claim responder status, and false otherwise. In our case we will, of course, make it return true.</p>

<pre><code class="language-javascript">handleStartShouldSetPanResponder(e, gestureState) {
    return true;
}</code></pre>

The next key is <code>onPanResponderGrant</code>, which will hold a function to be fired once our view is <em>granted</em> a responder status. Let us call this function <code>handlePanResponderGrant</code>. For now, let's simply make it log a message to the console.</p>

<pre><code class="language-javascript">handlePanResponderGrant(e, gestureState) {
  console.log('Finger touched the image');
}
</code></pre>

The final two keys, which are pretty self-explanatory, hold the same value <code>handlePanResponderEnd</code>, which is what happens when a finger is lifted up from the responder component. For now, let's just make it log a message to the console.</p>

<pre><code class="language-javascript">handlePanResponderEnd(e, gestureState) {
  console.log('Finger pulled up from the image');
}</code></pre>

Refresh the simulator. Once a wallpaper is loaded, click on it and you should see the following in the console:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/381ecbb4-548e-4b05-8fd0-c1f704e472a8/fig22-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/381ecbb4-548e-4b05-8fd0-c1f704e472a8/fig22-react-native-preview-opt.png" alt="Logging message to the console on touch and lift." /></a><figcaption>Logging message to the console on touch and lift.</figcaption></figure><figure>Great! Now we know that our initial set-up is working correctly. Let's try to detect a double-tap.

Whenever a tap is registered, it's possible that tap concludes a double-tap. To check if a tap ends a double-tap we will need to have access to previous tap’s information: its location (<i>x</i>- and <i>y</i>-coordinates) and time stamp to be precise. Declare a new object literal <code>prevTouchInfo</code> just below the <code>imagePanHandler</code> object in the constructor.</p>

<pre><code class="language-javascript">this.prevTouchInfo = {
  prevTouchX: 0,
  prevTouchY: 0,
  prevTouchTimeStamp: 0
};</code></pre>

Then update <code>handlePanResponderGrant</code> to resemble the following:

<pre><code class="language-javascript">handlePanResponderGrant(e, gestureState) {
/***/
  var currentTouchTimeStamp = Date.now();

  if( this.isDoubleTap(currentTouchTimeStamp, gestureState) )
    console.log('Double tap detected');

  this.prevTouchInfo = {
    prevTouchX: gestureState.x0,
    prevTouchY: gestureState.y0,
    prevTouchTimeStamp: currentTouchTimeStamp
  };
/***/
}</code></pre>

<code>handlePanResponderGrant</code> is fired each time our <code>NetworkImage</code> component successfully claims the responder status or, in simpler words, whenever it is tapped on.

We are addressing <code>this</code> inside <code>handlePanResponderGrant</code>, but <code>this</code> inside this method is not our <code>SplashWalls</code> class; rather, it is <code>PanResponder</code>. To deal with this, before the closing brace of <code>constructor</code> add the following line:

<pre><code class="language-javascript">this.handlePanResponderGrant = this.handlePanResponderGrant.bind(this);</code></pre>

Now is a good time to shed some light on a small difference between the two patterns of declaring React classes we discussed in part 1. In this tutorial we’ve chosen to go with the ES2015 class syntax; the other option was to use <code>React.createClass({ ... })</code>. If we had gone with the other option, we wouldn’t have to bind <code>this</code> to the method in the <code>constructor</code>. It would’ve been taken care for us by <em>autobinding</em>. Again, when you make a choice, you lose some, you gain some.

The first thing we do inside <code>handlePandResponderGrant</code> is grab the tap's time stamp in <code>currentTouchTimeStamp</code> using <code>Date.now()</code>.

Then we check if this tap concludes a double-tap, using the <code>isDoubleTap</code> method:

<pre><code class="language-javascript">isDoubleTap(currentTouchTimeStamp, {x0, y0}) {
  var {prevTouchX, prevTouchY, prevTouchTimeStamp} = this.prevTouchInfo;
  var dt = currentTouchTimeStamp - prevTouchTimeStamp;

  return (dt &lt; DOUBLE_TAP_DELAY &amp;&amp; Utils.distance(prevTouchX, prevTouchY, x0, y0) &lt; DOUBLE_TAP_RADIUS);
}
</code></pre>

You will notice a couple of new things here. First are two constants <em>DOUBLE_TAP_DELAY</em> and <em>DOUBLE_TAP_RADIUS</em>. Define them with <em>NUM_WALLPAPERS</em>.</p>

<pre><code class="language-javascript">const DOUBLE_TAP_DELAY = 300; // milliseconds
const DOUBLE_TAP_RADIUS = 20;</code></pre>

Next, I have defined a new module, <i>Utils.js</i>, and included it in the <i>index.ios.js</i> file. <i>Utils.js</i> exports a single method: <code>distance</code>.</p>

<pre><code class="language-javascript">distance(x0, y0, x1, y1) {
  return Math.sqrt( Math.pow(( x1 - x0 ), 2) + Math.pow(( y1 - y0 ), 2) );
}</code></pre>

<code>distance</code> simply calculates and returns the distance between two points using the following geometry formula

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb82360-b2fa-496f-be4b-5102b28f0857/fig33-react-native-preview-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3cb82360-b2fa-496f-be4b-5102b28f0857/fig33-react-native-preview-opt.jpg" alt="The distance formula." /></a><figcaption>The distance formula.</figcaption></figure>Finally <code>isDoubleTap</code> in the return statement checks if the time difference between the previous and current tap is less than 300 milliseconds (<em>DOUBLE_TAP_DELAY</em>), and if the distance between the two consecutive taps is less than 20px (<em>DOUBLE_TAP_RADIUS</em>). If both conditions are met, the function returns true, otherwise false. Sound good? Great.

For one last step in <code>handlePanResponderGrant</code>, we update <code>prevTouchInfo</code> with the tap’s information that was just registered.

Let's try out our double-tap listener in the simulator. Once a wallpaper loads, try double-clicking anywhere on the wallpaper. You should be able to read “Double tap detected” in the console. Good job!
## 3. Saving Wallpaper To Camera Roll

On detecting a double-tap right now, all we’re doing is logging “Double tap detected” to the console. Replace that line with the following method call:

<pre><code class="language-javascript">if( isDoubleTap(currentTouchTimeStamp, gestureState) )
	this.saveCurrentWallpaperToCameraRoll();</code></pre>

We’ll get to declaring <code>saveCurrentWallpperToCameralRoll</code> later, but first declare the following variable inside the constructor:

<pre><code class="language-javascript">this.currentWallIndex = 0;</code></pre>

<code>currentWallIndex</code> holds the index of the wallpaper that is currently visible on the screen. The first wallpaper has an index of 0, the next has an index of 1, and so on.

On each swipe, we need to update the value of <code>currentWallIndex</code>. This is a very simple task thanks to react-native-swiper's API. Remember the function <code>onMomentumScrollEnd</code> that we touched on towards the end of last section in part 1? Now’s the time to finally declare it.</p>

<pre><code class="language-javascript">onMomentumScrollEnd(e, state, context) {
  this.currentWallIndex = state.index;
}</code></pre>

We’ll also need to bind <code>this</code> to this method. In the constructor, right below where we bind <code>this</code> to <code>handlePanResponderGrant</code>, add the following line:

<pre><code class="language-javascript">this.onMomentumScrollEnd = this.onMomentumScrollEnd.bind(this);</code></pre>

To be able to access the Camera Roll in our app we will need to link the <em>Camera Roll</em> library to our app.

Remember <a href="#">linking ReactART</a> in part 1? We’ll need to follow the exact same procedure with the <i>RCTCameraRoll.xcodeproj</i> file, which can be found in <i>node_modules/react-native/Libraries/CameraRoll</i>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d8fd915-ea72-4ec8-9f48-71697752c19c/fig23-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d8fd915-ea72-4ec8-9f48-71697752c19c/fig23-react-native-preview-opt.png" alt="Location of RCTCameraRoll.xcodeproj" /></a><figcaption>Location of RCTCameraRoll.xcodeproj</figcaption></figure><figure>Once you’ve linked to <code>CameraRoll</code>, add two new lines to the imports:

<pre><code class="language-javascript">var {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  Component,
  ActivityIndicatorIOS,
  Dimensions,
  PanResponder,
/***/
  CameraRoll, // Add this
  AlertIOS // and this
/***/
} = React;</code></pre>

Once the wallpaper has been saved to the Camera Roll, we’ll show the user an alert with a success message. We’ll need <code>AlertIOS</code> to do that. Now, we can define <code>saveCurrentWallpaperToCameraRoll</code>.</p>

<pre><code class="language-javascript">saveCurrentWallpaperToCameraRoll() {
  var {wallsJSON} = this.state;
  var currentWall = wallsJSON[this.currentWallIndex];
  var currentWallURL = `https://unsplash.it/${currentWall.width}/${currentWall.height}?image=${currentWall.id}`;

  CameraRoll.saveImageWithTag(currentWallURL, (data) =&gt; {
    AlertIOS.alert(
      'Saved',
      'Wallpaper successfully saved to Camera Roll',
      [
        {text: 'High 5!', onPress: () =&gt; console.log('OK Pressed!')}
      ]
    );
  },(err) =&gt;{
    console.log('Error saving to camera roll', err);
  });

}</code></pre>

The whole of <code>saveCurrentWallpaperToCameraRoll</code> is very straightforward. If you’re curious or feeling stuck you can read more about <a href="https://facebook.github.io/react-native/docs/cameraroll.html">CameraRoll</a> and <a href="https://facebook.github.io/react-native/docs/alertios.html">AlertIOS</a>.

Refresh the simulator, and once a wallpaper loads double-click on it. After a little delay you should be prompted to provide SplashWalls permission to access the Camera Roll Once that is done you should see an alert like one shown below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70773187-4463-4ea8-bd00-0f6ef3655332/fig24-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70773187-4463-4ea8-bd00-0f6ef3655332/fig24-react-native-preview-opt.png" alt="Alert modal pops up when wallpaper is successfully saved to the Camera Roll." /></a><figcaption>Alert modal pops up when wallpaper is successfully saved to the Camera Roll.</figcaption></figure><figure>Notice that there is a delay between double-tapping and the appearance of the alert modal. We can’t do anything about the delay but we don't have to leave the user hanging, thinking the double-tap didn’t work. We’ll take care of this in the next section.
## 4. Creating A Progress HUD Component

In this section we will create our very first component, which will be a progress heads-up display (HUD). All it includes is a spinner on a translucent black background with “Please wait…” text below it. We will show this component during the delay that occurs between the double-tap and the appearance of the alert modal, so the user knows their action worked and the app is responsive.

Create a new file, <i>ProgressHUD.js</i>, in the root directory of the app. Fill the file with the following lines:

<pre><code class="language-javascript">'use strict';

var React = require('react-native');

var {
  View,
  Text,
  Component,
  ActivityIndicatorIOS,
} = React;

class ProgressHUD extends Component {
	constructor(props) {
		super(props);
	}

	render() {
		var {width, height, isVisible} = this.props;
		if( isVisible ) {
			return(
				&lt;View
				 style={{
				 	flex: 1,
				 	flexDirection: 'row',
				 	justifyContent: 'center',
				 	alignItems: 'center',
				 	width: width,
				 	height: height,
				 	position: 'absolute',
				 	top: 0,
				 	left: 0,
				 	backgroundColor: 'rgba(0, 0, 0, 0.5)'
				 }}&gt;
				 &lt;ActivityIndicatorIOS
	          animating={true}
	          color={'#fff'}
	          size={'large'}
	          style={{margin: 15}} /&gt;
           &lt;Text style={{color:’#fff’}}&gt;Please wait...&lt;/Text&gt;
				&lt;/View&gt;

			);
		} else {
			return(&lt;View&gt;&lt;/View&gt;);
		}
	}
};

module.exports = ProgressHUD;</code></pre>

Notice the first line inside <code>render</code>. We’re creating three new variables and retrieving their values from <code>this.props</code>. Props in React are things passed to a component from inside another component, like width, height and <code>isVisible</code> will be passed to <code>ProgressHUD</code>:

<pre><code class="language-javascript">&lt;ProgressHUD width={width} height={height} isVisible={isHudVisible}/&gt;</code></pre>

Include <i>ProgressHUD.js</i> in <i>index.ios.js</i> file as shown.</p>

<pre><code class="language-javascript">// Components
var ProgressHUD = require('./ProgressHUD.js');</code></pre>

To control the visibility of the progress HUD, we will add a new state variable:

<pre><code class="language-javascript">this.state = {
  wallsJSON: [],
  isLoading: true,
/***/
  isHudVisible: false // add this
/***/
};</code></pre>

Now add the <code>&lt;ProgressHUD&gt;</code> component right after <code>&lt;/Swiper&gt;</code> in the <code>renderResults</code> method. Doing so will lead to an error because we will be returning more than one component, which is not allowed in React Native. To get around this, simply wrap everything inside <code>return()</code> (the swiper and progress HUD component), in a simple <code>&lt;View&gt;&lt;/View&gt;</code>.</p>

<pre><code class="language-javascript">renderResults() {
  var {wallsJSON, isHudVisible} = this.state;
  return (
  /***/
    &lt;View&gt;
  /***/
    &lt;Swiper
      ...&gt;

.
.
.
    &lt;/Swiper&gt;
  /***/
    &lt;ProgressHUD width={width} height={height} isVisible={isHudVisible}/&gt;
    &lt;/View&gt;
  /***/
  );
}</code></pre>

We’re passing in three props to <code>ProgressHUD</code>: the first two are the dimensions of the screen; the third is a Boolean value determining whether <code>ProgressHUD</code> returns a spinner with “Please Wait…” on a translucent background or just nothing.

We will control the hiding and showing of the progress HUD from inside <code>saveCurrentWallpaperToCameraRoll</code>. Update the method to resemble the following:

<pre><code class="language-javascript">saveCurrentWallpaperToCameraRoll() {

/***/
  // Make Progress HUD visible
  this.setState({isHudVisible: true});
/***/

  var {wallsJSON} = this.state;
  var currentWall = wallsJSON[this.currentWallIndex];
  var currentWallURL = `https://unsplash.it/${currentWall.width}/${currentWall.height}?image=${currentWall.id}`;

  CameraRoll.saveImageWithTag(currentWallURL, (data) =&gt; {

/***/
    // Hide Progress HUD
    this.setState({isHudVisible: false});
/***/

    AlertIOS.alert(
      'Saved',
      'Wallpaper successfully saved to Camera Roll',
      [
        {text: 'High 5!', onPress: () =&gt; console.log('OK Pressed!')}
      ]
    );
  },(err) =&gt;{
    console.log('Error saving to camera roll', err);
  });
}
</code></pre>

We make the HUD visible as soon as we enter the method, and hide it once <code>saveImageWithTag</code> is triggered.

Refresh the simulator and double-click on a wallpaper. You will notice the progress HUD becomes visible and goes away as soon as the alert dialog pops up.

But something odd is happening here: we are jumping back to the first image after the double-tap. This is because we’re modifying a state variable (<code>isHudVisible</code>) inside <code>saveWallpaperToCameraRoll</code> using <code>this.setState()</code>, which results in rerendering, and causes the swiper to reload data and start from the very first image.

To stop that from happening simply add a new attribute <code>index</code> to <code>Swiper</code>.</p>

<pre><code class="language-javascript">&lt;Swiper ...
        index={this.currentWallIndex}&gt;</code></pre>

This makes sure that when rerendering occurs we’re shown the same wallpaper that was visible earlier. Refresh the simulator and everything should be working as intended.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57d0f7a2-2643-44c7-8db7-6e96de585e0d/fig25-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/57d0f7a2-2643-44c7-8db7-6e96de585e0d/fig25-react-native-preview-opt.png" alt="ProgressHUD becomes visible on double tap." /></a><figcaption>Progress HUD becomes visible on double-tap.</figcaption></figure><figure>With that, we’ve almost finished building our cute little app. Right now we’re simply fetching five wallpapers on launch. Wouldn’t it be cool if we could just shake our iPhone and it fetched five new random wallpapers automagically?
## 5. Running The App On An iPhone And Detecting Shake Gesture

Even if you don’t have a physical device you can still detect a shake gesture in the simulator by pressing <kbd>Cmd + Ctrl + Z</kbd> with the simulator window in focus.

Let's make our app fetch five new random wallpapers every time we shake the device. Like rolling a die!

To enable our app to detect shakes we will need to install an npm module called <a href="https://www.npmjs.com/package/react-native-shake-event-ios">react-native-shake-event-ios</a>.

Head to the root of the project and run the following command from the terminal:

<pre><code class="language-bash">npm install --save react-native-shake-event-ios</code></pre>

One more thing we need to do is to link a library. As this is the third (and last) time we'll link a library in this tutorial, you should be acquainted with the process already.

Find the <i>RNShakeEvent.xcodeproj</i> inside <i>node_modules/react-native-shake-event-ios/</i> and link that through Xcode.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a3c311a-4ad9-4c0d-8412-4a201b504973/fig26-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8a3c311a-4ad9-4c0d-8412-4a201b504973/fig26-react-native-preview-opt.png" alt="Location of RNShakeEvent.xcodeproj" /></a><figcaption>Location of RNShakeEvent.xcodeproj</figcaption></figure><figure>Like any other library, we import it in our main file like so:

<pre><code class="language-javascript">var ShakeEvent = require('react-native-shake-event-ios');</code></pre>

Then, head over to the <code>componentWillMount</code> method. This is where we will wire our shake event listener. After doing that, our <code>componentWillMount</code> method should look like this:

<pre><code class="language-javascript">componentWillMount() {
  this.imagePanResponder = PanResponder.create({
    onStartShouldSetPanResponder: this.handleStartShouldSetPanResponder,
    onPanResponderGrant: this.handlePanResponderGrant,
    onPanResponderRelease: this.handlePanResponderEnd,
    onPanResponderTerminate: this.handlePanResponderEnd
  });

/***/
  // Fetch new wallpapers on shake
  ShakeEvent.addEventListener('shake', () =&gt; {
    this.initialize();
    this.fetchWallsJSON();
  });
/***/
}</code></pre>

In the <code>initialize</code> method we reset the values of variables like so:

<pre><code class="language-javascript">initialize() {
  this.setState({
    wallsJSON: [],
    isLoading: true,
    isHudVisible: false
  });

  this.currentWallIndex = 0;
}</code></pre>

Once that is done, new random wallpapers are fetched from the API via a <code>this.fetchWallsJSON()</code> call.

Now, it’s time to install our app on our device and run it without any dev server running. The
<a href="https://facebook.github.io/react-native/docs/running-on-device-ios.html">official React Native docs</a> have a slightly different and cumbersome procedure to do this, which requires you to bundle and minify your code using a host of different flags. This is totally unnecessary, as described in this <a href="https://github.com/react-native-fellowship/react-native-side-menu/pull/160">pull request</a>. I suggest you don’t even try to go through the official docs. Simply do what the following steps say and you should be good.
<ol>
 	<li>Head over to <i>Xcode/SplashWalls/SplashWalls/AppDeletegate.m</i>, comment out the line starting with <code>jsCodeLocation...</code> below <code>OPTION 1</code>, and uncomment the line starting with <code>jsCodeLocation...</code> below <code>OPTION 2</code>.<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0515ffc0-c0fb-4d60-9f48-bbbd095c9957/fig27-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0515ffc0-c0fb-4d60-9f48-bbbd095c9957/fig27-react-native-preview-opt.png" alt="Contents of AppDeletegate.m after this step." /></a><figcaption>Contents of AppDeletegate.m after this step. Notice OPTION 2 has been uncommented and OPTION 1 has been commented out.</figcaption></figure></li>
 	<li>Go to Product → Scheme → Edit Scheme, or simply press <kbd>Cmd + Shift + ,</kbd><figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6e78721-b3e0-41ce-84f9-7f711d096cf4/fig28-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c6e78721-b3e0-41ce-84f9-7f711d096cf4/fig28-react-native-preview-opt.png" alt="Change build configuration to Release." /></a><figcaption>Change build configuration to Release.</figcaption></figure>In the window that slides in, change <strong>Build Configuration</strong> under <strong>Run</strong> from <strong>Debug</strong> to <strong>Release</strong>. Click <strong>Close</strong>. Doing this will disable the Dev menu from popping up every time we shake the device.</li>
 	<li>Head to <strong>Build Settings</strong> and disable <strong>Dead Code Stripping</strong>.<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90362bc3-402f-4d33-8f7a-04d1f3f0b3ec/fig29-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90362bc3-402f-4d33-8f7a-04d1f3f0b3ec/fig29-react-native-preview-opt.png" /></a><figcaption>Simply type "Dead" in search field to find Dead Code Stripping option.</figcaption></figure></li>
 	<li>Make sure you have <strong>Bundle React Native code and images</strong> section under <strong>Build Phases</strong> with the following configuration:<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c27449e-fea8-49b9-9dcc-a8e047848407/fig30-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9c27449e-fea8-49b9-9dcc-a8e047848407/fig30-react-native-preview-opt.png" alt="Build Phases should have Bundle React Native code and images present." /></a><figcaption>Build Phases should have Bundle React Native code and images present.</figcaption></figure>If not, add it following <a href="https://facebook.github.io/react-native/docs/upgrading.html#from-0-13-to-0-14">the steps in the docs</a>. Now connect your iOS device to your Mac, select it in the Devices section and hit Run from Xcode.</p>

<img loading="lazy" decoding="async" src="https://res.cloudinary.com/indysigner/image/upload/v1544089435/13a425b7b3-preview-opt_vswgao.png" alt="Build Phases should have Bundle React Native code and images present." /></li>
</ol>
The whole process of bundling and installation will take a while initially. Once done you will be able to run the app on your device without any development server running. Whenever you want to go back to development simply reverse the steps 1 and 2.

As a final step, add an app icon to the app.
<ul>
 	<li><a href="https://www.dropbox.com/s/btnpea9ongeg131/SplashWallIcons.zip?dl=0">Download</a> the <i>.zip</i> file containing icons. Unzip it.</li>
 	<li>The app icon I designed is just a black rounded rectangle with a white circle in the center. If you want to design your own app icon, please go ahead. Make sure you follow <a href="https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/MobileHIG/IconMatrix.html">the iOS guidelines</a> regarding the dimensions of the icons.</li>
 	<li>In Xcode, head to <i>SplashWalls/SplashWalls/Images.xcassets</i>. In the left sidebar you should see a category called <strong>AppIcon</strong>; click on it.<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44d8f51c-9eda-4eb3-9860-72e8e3758b74/fig31-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44d8f51c-9eda-4eb3-9860-72e8e3758b74/fig31-react-native-preview-opt.png" alt="AppIcon section can be found under Images.xcassets." /></a><figcaption>AppIcon section can be found under Images.xcassets.</figcaption></figure></li>
 	<li>From the folder containing the icons, drag each icon to its appropriate holder.<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a85926fe-07fe-45fe-8909-0e2a5d116eb8/fig32-react-native-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a85926fe-07fe-45fe-8909-0e2a5d116eb8/fig32-react-native-preview-opt.png" alt="Placing App Icons in appropriate holders." /></a><figcaption>Placing App Icons in appropriate holders.</figcaption></figure></li>
</ul>
Run the app again from Xcode and this time you should see the AppIcon we just added instead of the default one.

Whoa! Did we just officially finish the app? Yes, of course we did.
## Wrapping Up

From fetching data over the network, to dynamic rendering, installing third party components, and linking libraries, the first part of this tutorial illustrated how simple it is to get up and running with a React Native project.

In the second part:
<ul>
 	<li>We started out by installing a <code>&lt;NetworkImage&gt;</code> component that allowed us to show loading indicators while the image loads in background.</li>
 	<li>We then touched on the PanResponder API and built a double-tap listener using it.</li>
 	<li>In the third section we made our app gain access to the Camera Roll.</li>
 	<li>In the fourth section we created our very own component that is visible during the delay between a double-tap and appearance of the alert dialog.</li>
 	<li>In the last section we detected the shake gesture, ran the app on a physical device, and even added an app icon.</li>
</ul>
After all this, I hope this two-part series got you acquainted with how React Native works and you learned something new. Maybe you even have an opinion on whether you’d like to pursue React Native development further. I’d love to hear your thoughts on it. React Native is still very young and has a lot of potential. It will be quite interesting to see where it is headed.

Again, all the code for the app we just built can be found <a href="https://github.com/nashvail/SplashWalls">on GitHub</a>.
## Up For A Challenge?

React Native provides a very convenient to use and powerful API for handling animations, appropriately named <a href="https://facebook.github.io/react-native/docs/animations.html">Animated</a>. In this tutorial there wasn't enough time to go over it, but I used the Animated API to add more functionalities to the app.

First, I created a long press listener using PanResponder. When a long press is detected on the right side of the screen, a home screen preview fades in; when a long press is detected on the left, a lock screen preview fades in. The fading in and out is handled by the Animated API. Check out the video below.
{{< vimeo id="163383239" >}}

</figure>If you’re up for a challenge why not add these functionalities to your own app? Or go ahead and develop some of your own beautiful apps. Once you have put together something cool, <a href="https://twitter.com/NashVail">show me on Twitter</a>.

{{< signature "og" >}}

</figure></figure></figure></figure></figure></figure></figure></figure></figure></figure></figure>


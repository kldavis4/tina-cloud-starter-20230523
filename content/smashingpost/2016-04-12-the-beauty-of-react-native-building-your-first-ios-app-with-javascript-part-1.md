---
title: React Native Tutorial – Building Your First iOS App With JavaScript (Part 1)
slug: the-beauty-of-react-native-building-your-first-ios-app-with-javascript-part-1
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43e826e8-aff1-45b9-a60b-d82d30cbe450/06-react-native-preview-opt.png
date: 2016-04-12T14:29:53.000Z
author: nashvail
description: >-
  These frameworks and **the whole idea of building mobile apps with
  JavaScript** never appealed to me, though. I always thought, why not just
  learn Swift/Objective-C or Java and build real apps? That definitely requires
  a significant amount of learning, but isn’t that what we developers do and
  should be good at? Quickly learn new languages and frameworks? What’s the
  point, then? For me, the advantages never outweighed the doubts.
categories:
  - Mobile
  - JavaScript
  - Apps
  - iOS
  - React
  - Swift
---
The idea of building mobile apps with JavaScript is not new. We’ve seen frameworks like <a href="https://ionicframework.com/">Ionic</a> and <a href="https://www.smashingmagazine.com/2014/02/four-ways-to-build-a-mobile-app-part3-phonegap/">PhoneGap</a> take on the challenge, and to some extent succeed in gaining a fair amount of developer and community support. To <a href="https://www.smashingmagazine.com/2016/04/how-to-build-your-first-ios-app-with-javascript/">part 2</a> of the tutorial.

These frameworks and <strong>the whole idea of building mobile apps with <a href="https://www.smashingmagazine.com/2016/04/finally-css-javascript-meet-cssx/">JavaScript</a></strong> never appealed to me, though. I always thought, why not just learn Swift/Objective-C or Java and build real apps? That definitely requires a significant amount of learning, but isn’t that what we developers do and should be good at? Quickly learn new languages and frameworks? What’s the point, then? For me, the advantages never outweighed the doubts.

Until I read <a href="https://medium.com/ios-os-x-development/an-ios-developer-on-react-native-1f24786c29f0#.avhlz9qsr">this article from Chalk + Chisel</a>, the following line in particular:
<blockquote>Fast-forward a couple of months, and I’m confident enough to say I may never write an iOS app in Objective-C or Swift again.</blockquote>

What? Are you, like… serious?

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Internationalizing React Apps](https://www.smashingmagazine.com/2017/01/internationalizing-react-apps/)

{{% feature-panel %}}

Reading such a bold assertion made me go ahead and give React Native a shot. Why not? I was already using React and loving it. React Native is so similar to React (duh!), you’ll feel right at home if you’re already a React developer. Even if you're not, React luckily happens to be very easy to wrap your head around.</p>

## What We Will Be Building

I’ve never had luck finding the perfect wallpaper app for my iPhone in the App store. On the desktop, <a href="https://unsplash.com/">Unsplash</a> is the one-stop shop for all my wallpaper needs. On the phone: Settings → Wallpaper :(

So, unlike some other tutorials where you build counters and barely use them, in this tutorial, together we’ll build ourselves an app that will pull random stunning wallpapers from Unsplash, display them in an aesthetically pleasing way, and allow you to save wallpapers of your choice to the Camera Roll. Believe me, I have found myself using this app more than I initially thought. Even if by the end of this tutorial React Native fails to impress you, you’ll still end up having a really cool wallpaper app. Isn’t that great?

Before we start, here are <strong>some things you should be familiar with:</strong>

1.  JavaScript
2.  Some [ES2015](https://babeljs.io/docs/learn-es2015/) features, namely [Classes](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes), [Arrow Functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions), [Destructuring](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) and [Template Strings](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/template_strings)
3.  Mac OS X Terminal
4.  CSS (yup!)
5.  [React](https://facebook.github.io/react/) (optional)

One more thing. As the title clearly states, in this tutorial we'll be building an <em>iOS</em> app. Which requires, yes, even with React Native, that you're on a Mac. With React Native you can definitely <a href="https://facebook.github.io/react-native/docs/linux-windows-support.html">build Android apps on Windows and Linux</a> but not iOS ones. Therefore, from here on in, this tutorial assumes you're running Mac OS X.</p>

## Takeaways

By the end of this tutorial, you’ll be familiar enough with React Native to start writing your own apps right away. We’ll go over setting up a project in Xcode, installing third party modules and components, linking libraries, styling with flexbox, creating a custom gesture listener, and many other things.

If you haven’t used React before, this tutorial will also set you up with React. React is the new hot JS library with a lot of potential, and I don’t see it going anywhere in near future.

This tutorial has been divided into two parts for your convenience. Each part has five sections. In each section we accomplish a goal that takes us a step closer to finishing our app. I’d advise that once started you should finish that whole section in one go since they are short, and in that way you'll get to know the whole concept I am trying to introduce without breaking your flow.

For your reference, the final code for the app we’re building can be found in <a href="https://github.com/nashvail/SplashWalls">this GitHub repo</a>.</p>

## 1\. Setting Up A Blank React Native Project

Make sure you have <a href="https://developer.apple.com/xcode/">Xcode 7.0</a> or higher installed. it can be downloaded free from the App Store.

Chances are (if you’re a web developer and reading this in 2016) you already have Node installed. But if that's not the case, go ahead and install <a href="https://nodejs.org/en/">Node</a> too. Another important tool we'll need is <a href="https://docs.npmjs.com/getting-started/what-is-npm">npm</a>. Node comes with npm installed; you'll need to update it, however, as it gets updated rather frequently. Follow <a href="https://docs.npmjs.com/getting-started/installing-node">this installation guide</a>.

That’s all we’ll need. Now, from the terminal run <code>npm install -g react-native-cli</code>. This will install React Native globally on your system.

If everything seems way too new to you, or you're just feeling a little lost in the whole installation process, the <a href="https://facebook.github.io/react-native/docs/getting-started.html#content">official getting started guide</a> is always there to help you out.

Find a good location on your computer where you would like to set up the project. Once there, from the terminal run <code>react-native init SplashWalls</code>.

This should fetch and install all the required modules and create a new folder called <i>SplashWalls</i>.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e9fc252-9088-4b5d-ba61-04dab53727a9/01-react-native-preview-opt.png"><img loading="lazy" decoding="async" class="alignnone" title="Initial contents of SplashWalls folder." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e9fc252-9088-4b5d-ba61-04dab53727a9/01-react-native-preview-opt.png" alt="react native tutorial" width="294" height="294" /></a><figcaption>Contents of SplashWalls folder.</figcaption></figure>

One great thing about React Native is you can write both Android and iOS applications together with a majority of JavaScript code shared between them. Inside the newly created folder you will find two <i>.js</i> files: <i>index.android.js</i> and <i>index.ios.js</i> – the names are self-explanatory. If you’re building an iOS app you’ll work with <i>index.ios.js</i>; with <i>index.android.js</i> for an Android app; and both for, you know, both platforms.

Since we’re building an iOS app, for the sake of this tutorial and to keep things clean we will get rid of the <i>index.android.js</i> and the <i>android</i> folder altogether. <i>index.ios.js</i> is the file we’ll be working with. This is the file that is first executed when the app launches.

Next, head on over to the <i>ios</i> folder and fire up <i>SplashWalls.xcodeproj</i>.

You should see a Xcode window pop up like one shown below.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d0ddf7d-4226-4174-b521-650b073dc4df/02-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Xcode on first launch." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7d0ddf7d-4226-4174-b521-650b073dc4df/02-react-native-preview-opt.png" alt="Xcode on first launch." /></a><figcaption>Xcode on first launch.</figcaption></figure>

Notice the warning in the image above that says “No matching provisioning profiles found.” Let's fix this.

First, change the text in the field <strong>Bundle Identifier</strong> to something custom. You need to make sure that whatever you enter follows <a href="https://en.wikipedia.org/wiki/Reverse_domain_name_notation">reverse DNS convention</a>, in which the domain name of your organization is reversed and suffixed with further identifiers. This convention helps distinguish your application from others on a device and on the App Store. I will use <em>com.nashvail.me.tutorial.SplashWalls</em>; simply substitute your name in place of mine if you can’t seem to make something up.

Next, choose your name from the team dropdown.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae363eee-7ad9-413e-89c6-26848abfd2e6/03-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Choose a team name." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae363eee-7ad9-413e-89c6-26848abfd2e6/03-react-native-preview-opt.png" alt="Choose a team name." /></a><figcaption>Choose a team name.</figcaption></figure>

Click on <strong>Fix Issue</strong>.

While we’re at it, notice the <strong>Deployment Info</strong> section. It has some default settings applied.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e7f3ac1-3060-4a21-a601-84ce2560be0d/04-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Initial Deployment info settings." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5e7f3ac1-3060-4a21-a601-84ce2560be0d/04-react-native-preview-opt.png" alt="Initial Deployment info settings." /></a><figcaption>Initial deployment info settings.</figcaption></figure>

Change the settings to match the following:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58aef14e-0367-4e2e-943d-42b11b5de869/05-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Final deployment info settings." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58aef14e-0367-4e2e-943d-42b11b5de869/05-react-native-preview-opt.png" alt="Final deployment info settings." /></a><figcaption>Final deployment info settings.</figcaption></figure>

We’ll make the app portrait-only and hide the status bar as well.

Go ahead and hit the <strong>Run</strong> button at the top-left in Xcode. Doing so will launch a terminal window like one shown below. Initial transformation takes a bit of time.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8ca1cdb-be2f-4fe9-9696-1eff688f3319/06-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Terminal window on first run." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8ca1cdb-be2f-4fe9-9696-1eff688f3319/06-react-native-preview-opt.png" alt="Terminal window on first run." /></a><figcaption>Terminal window on first run.</figcaption></figure>

Once done, you should see the following output in the simulator:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ad66847-236a-43c4-a837-fe0445f94f27/07-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Simulator on first launch." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ad66847-236a-43c4-a837-fe0445f94f27/07-react-native-preview-opt.png" alt="Simulator on first launch." /></a><figcaption>Simulator on first launch.</figcaption></figure>

And with this we’ve completed our very first section.

## 2\. Fetching Wallpaper Data From The API

In this section we will make calls to the <a href="https://unsplash.it">Unsplash.it</a> API asking for wallpaper data. But before we start doing all the interesting work, there is some set-up to be done.</p>

### Switching To ES2015 Class Syntax

On opening the <i>index.ios.js</i> file you’ll notice some initial code already present. This is the code responsible for the output in the simulator (previous image).

Inside <i>index.ios.js</i> notice the line of code that says <code>var SplashWalls = React.createClass({ ... })</code>. We are going to modify this. We will use ES2015’s <code>class</code> syntax for this tutorial.

We developers are curious souls. I know you must be asking, Why? Why switch to the <code>class</code> syntax?

It all comes down to personal preference. I have programmed extensively in object-oriented languages before and <code>class</code> just feels more familiar to me. Moreover, by using <code>class</code> you also choose to keep the code a little cleaner as you don’t have to add commas after each method declaration.

On the flip side, when you choose <code>class</code> you don’t get features like autobinding or access to the <code>isMounted</code> method, which is not a bad thing at all, as you’re not really going to find yourself at a loss by not using these.

Whichever way you go, you’re creating a class after all. My advice would be to use <code>class</code>. It’s a new feature and sooner or later you’ll find yourself using ES2015. And if you’re following this tutorial, you will have to use <code>class</code> – you don’t really have a choice!

For more on this consider reading “<a href="https://reactjsnews.com/composing-components">React.Component vs React.createClass</a>” by Naman Goel and Zach Silveira.

Once you’ve made the necessary changes, the block of code should now be as shown:

<pre><code class="language-javascript">class SplashWalls extends Component{
  render() {
    return (

  . &lt;View style={styles.container}&gt;
        &lt;Text style={styles.welcome}&gt;
          Welcome to React Native!
        &lt;/Text&gt;
        &lt;Text style={styles.instructions}&gt;
          To get started, edit index.ios.js
        &lt;/Text&gt;
        &lt;Text style={styles.instructions}&gt;
          Press Cmd+R to reload,{'\n'}
          Cmd+D or shake for dev menu
        &lt;/Text&gt;

   .&lt;/View&gt;
    );
  }
};
</code></pre>

For folks new to React, the code inside <code>return</code> parens may seem a little wacky, but it's not rocket science, just good old XML-like syntax called JSX. <a href="https://facebook.github.io/jsx/">Read more about it here</a>.

Compared with the pre-<code>class</code> implementation, the <code>var</code> syntax is gone. Also <code>render: function(){…</code> is now just <code>render(){…</code>.

Hey! But what is that `Component` you are extending? And you’d be right to ask. If you ran the project in Xcode now, you’d get an error saying `Component` is not defined. You can do two things here: replace `Component` with `React.Component`; or add a new line inside the block (shown below) at the top of the file.

In this and later code examples, I surround the newly added lines with <code>/***/</code> so that it's easier for you to compare the code you're writing with what is shown here. Just make sure that if you copy code from the samples you don't end up copying <code>/***/</code> along with the actual code. Since JSX doesn't support <code>/***/</code> comments, you will end up crashing the app if you included these in your JSX code.</p>

<pre><code class="language-javascript">var {
  AppRegistry,
  StyleSheet,
  Tex .t,
  View,
  /***/
  Component 
  /***/
} = React;
</code></pre>

All the block of code above does is save you a couple of keystrokes. For example, if you didn’t include these lines of code at the top, you’d have to write <code>React.AppRegistry</code> instead of just <code>AppRegistry</code> every time you wanted to do so. Pretty frigging cool! Isn’t it? OK, not so much.

Go back to Xcode and run the project once again to make sure you didn’t break anything in the process.

Everything good? Great! Let's move on.

Inside the <code>SplashWalls</code> class, the first thing we need to do is add a constructor. Inside the constructor we will initialize our state variables. The only two state variables we will need at this point are an array – <code>wallsJSON</code> – which is going to store all the JSON data fetched from the API, and <code>isLoading</code>, which is a Boolean variable, meaning it will hold a value of either true or false. Having this state variable will help us show and hide the loading screen depending on whether the data has been loaded or not.

Inside the <code>SplashWalls</code> class, add the <code>constructor</code> as shown below.</p>

<pre><code class="language-javascript">class SplashWalls extends Component{
/***/
  constructor(props) {
    super(props);

    this.state = {
      wallsJSON: [],
      isLoading: true
    };
  }
/***/
...
}
</code></pre>

Next, we will define a <em>fetchWallsJSON</em> method, which, well, does what it says. Leave a couple of lines below the constructor’s closing brace and add the following lines of code:

<pre><code class="language-javascript">fetchWallsJSON() {
	console.log(‘Wallpapers will be fetched’);
}</code></pre>

We would like this function to fire once our component has been successfully mounted. Add the <code>componentDidMount</code> method. Most of the described methods go inside the <code>SplashWalls</code> class – I’ll not forget to mention when they don’t.</p>

<code>componentDidMount</code> is a lifecycle method which is fired immediately after the first rendering occurs.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aec91e9e-2e87-419e-9ab9-85bddd05b8bb/32-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Simulator on first launch." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aec91e9e-2e87-419e-9ab9-85bddd05b8bb/32-react-native-preview-opt.png" alt="Initial render LifeCycle method call sequence." /></a><figcaption>Initial render lifecycle method call sequence. (Image credit: <a href="https://twitter.com/tutorialhorizon">TutorialHorizon</a>)</figcaption></figure>

<a href="https://facebook.github.io/react/docs/component-specs.html">Here's a good explanation of all the React component's lifecycle methods</a>. Just remember that since we're using the newer <code>class</code> syntax, we can omit the <code>getInitialState</code> method. It is substituted by a <code>this.state</code> variable declaration in the <code>constructor</code>.

It’s a good idea to organize methods inside your class in a clean manner. I like to keep all the custom methods separate from the lifecycle methods. You should too.

Let's declare <code>componentDidMount</code>:

<pre><code class="language-javascript">componentDidMount() {
	this.fetchWallsJSON();
}</code></pre>

Notice that inside the <code>fetchWallsJSON</code> method we have logged a message to the console – but where is the console? Hold tight.

Make sure you have the Simulator window selected and press <kbd>Cmd + Control + Z</kbd>. From the menu that pops up, select <strong>Debug in Chrome</strong>. This opens up a new tab. While in the same tab, head over to Dev Tools (<kbd>Option + Cmd + J</kbd>). In the console you will find the message “Wallpapers will be fetched”.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5b4635f-153f-43d4-9b80-dc33bafa9e1f/08-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Logged message in the console." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f5b4635f-153f-43d4-9b80-dc33bafa9e1f/08-react-native-preview-opt.png" alt="Logged message in the console." /></a><figcaption>Logged message in the console.</figcaption></figure>

Keep the debugger open for now. Visit <a href="https://unsplash.it/list">unsplash.it/list</a> in a new tab. You should see the whole viewport filled with a JSON array. Each element in the array is a JavaScript object holding data for a single wallpaper. This is the data we will be filtering through and grabbing random wallpapers from.

Let us first make <code>fetchWallsJSON</code> do more than just log a message to the console.</p>

<pre><code class="language-javascript">  fetchWallsJSON() {
	/***/
    var url = 'https://unsplash.it/list';
    fetch(url)
      .then( response =&gt; response.json() )
      .then( jsonData =&gt; {
        console.log(jsonData);
      })
	.catch( error =&gt; console.log(‘Fetch error ‘ + error) );
	/***/
  }</code></pre>

Refresh the simulator (<kbd>Cmd + R</kbd>) or, better, enable live reload by pressing <kbd>Cmd + Ctrl + Z</kbd> and choosing <strong>Enable live reload</strong>. By enabling live reload you don’t have to refresh the simulator each time you make a change to your code. Just save in the IDE and the simulator will automatically be refreshed. If you’ve ever developed an app in Xcode or Android Studio before, you’ll find this feature particularly amazing as you don’t have to hit the <strong>Run</strong> button and recompile the app every single time you make a change. These little bits make React Native so much more appealing.

On refresh, after waiting a few seconds, you should see the following output in the console:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a34cbafd-0bf6-4411-9009-e8e706108ed3/09-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Retrieved data logged in the console." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a34cbafd-0bf6-4411-9009-e8e706108ed3/09-react-native-preview-opt.png" alt="Retrieved data logged in the console." /></a><figcaption>Retrieved data logged in the console.</figcaption></figure>

Good, now we’re able to fetch wallpapers’ JSON data from the API. As you might have noticed there is a little delay before the data is logged to the console. This is because in the background the data is being downloaded from the servers, which takes time.

This looks like a perfect time to add a loading screen.</p>

## 3\. Adding A Loading Screen

By the end of this section we will have a loading screen show up while the JSON data is being downloaded.

First, get rid of everything from inside <code>SplashWall</code> class's <code>render</code> method and add these lines of code:

<pre><code class="language-javascript">  render() {
    var {isLoading} = this.state;
    if(isLoading)
      return this.renderLoadingMessage();
    else
      return this.renderResults();
  }</code></pre>

We have two new methods. Let's declare them too, while we’re at it

<pre><code class="language-javascript">  renderLoadingMessage() {
    return (

  . &lt;View style={styles.loadingContainer}&gt;
        &lt;ActivityIndicatorIOS
          animating={true}
          color={'#fff'}
          size={'small'} 
          style={{margin: 15}} /&gt;
          &lt;Text style={{color: '#fff'}}&gt;Contacting Unsplash&lt;/Text&gt;

   .&lt;/View&gt;
    );
  }

  renderResults() {
    return (

  . &lt;View&gt;
        &lt;Text&gt;
          Data loaded
        &lt;/Text&gt;

   .&lt;/View&gt;
    );
  }</code></pre>

Depending on what value the <code>isLoading</code> state variable holds, two different <code>View</code> components will be rendered. If <code>isLoading</code> is true we show a loading spinner followed by the text “Contacting Unsplash”; when <code>isLoading</code> is false (implying data has been loaded) we show the results, which as of now is just a <code>Text</code> component that says “Data loaded”.

But we’re missing something here: we’re not changing the value of <code>isLoading</code> once our data has been downloaded. Let us do just that. Head over to the <code>fetchWallsJSON</code> method and below the line that logs <code>jsonData</code> to the console, add one extra line to update <code>isLoading</code>.</p>

<pre><code class="language-javascript">  fetchWallsJSON() {
    var url = 'https://unsplash.it/list';
    fetch(url)
      .then( response =&gt; response.json() )
      .then( jsonData =&gt; {
        console.log(jsonData);
	/***/
        this.setState({isLoading: false}); //update isLoading 
	/***/
      })
	.catch( error =&gt; console.log(‘Fetch error ‘ + error) );
  }</code></pre>

<a href="https://facebook.github.io/react/docs/component-api.html#setstate">setState</a> is one of <a href="https://facebook.github.io/react/docs/component-api.html">React's Component API methods.</a> It is the primary method used to trigger UI updates.

Notice, in <code>renderLoadingMessage</code> we have a new component: <code>ActivityIndicatorIOS</code> (put simply, the spinner). We need to import this component before we can use it. <a href="#componentImport">Remember when we imported <code>Component</code> </a>where we saved a couple of keystrokes? We’ll need to do just that.</p>

<pre><code class="language-javascript">var {
  AppRegistry,
  StyleSheet,
  Tex .t,
  View,
  Component,
/***/
  ActivityIndicatorIOS // Add new component
/***/
} = React;</code></pre>

We need to do one more thing before we can see the results. Notice the <code>View</code> containing <code>ActivityIndicatorIOS</code> has style set to <code>styles.loadingContainer</code>. We’ll need to define that. Find the line that says <code>var styles = StyleSheet.create({…</code>. Here you will see there are some styles already defined. These styles are responsible for styling the initial “Welcome to React Native” message in the simulator. Get rid of all of the predefined styles and add just one for the <code>loadingContainer</code> as shown.</p>

<pre><code class="language-javascript">var styles = StyleSheet.create({
/***/
  loadingContainer: {
	flex: 1,
    flexDirection: 'row’,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#000'
  }
/***/
});</code></pre>

All of the styles you apply on components in React Native are declared in the manner shown above. <code>StyleSheet.create</code> takes in a JavaScript object containing styles as an argument and then the styles can be accessed using the <code>dot[.]</code> operator. Like we applied the style to wrapper <code>View</code> in the following manner.</p>

<pre><code class="language-javascript">&lt;View style={styles.loadingContainer}/&gt;</code></pre>

You’re also allowed to declare styles inline:

<pre><code class="language-javascript">&lt;View style={{
	flex: 1,
    flexDirection: 'row',
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#000'
  }} /&gt;</code></pre>

This makes our code a little cluttered, though. When you have a number of styles applied to a component, it’s always a good idea to store them in a variable.

The styles look a lot like CSS, don’t they? You know why? Because they’re supposed to – they’re not any different. This makes React Native even easier for web developers to pick up. When you build an app in a dedicated IDE (Xcode, for example) you’re provided with a <em>StoryBoard</em> to directly drag and position UI elements like buttons and labels on the screen. You can’t do that in React Native, which – believe me – isn’t a bad thing at all.</p>

<strong>React Native makes heavy use of flexbox to position elements on the screen.</strong> Once you’re comfortable with flexbox, positioning elements around is a breeze. I will on any day prefer flexbox layout over StoryBoard, period. It's just one of those things you have to try yourself to tell the difference.

Save the changes, head over to the simulator and press <kbd>Cmd + R</kbd>. You should see the loading screen.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6382eda-8773-4c50-9b48-5159bb2d1464/10-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Loading screen we just finished building." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6382eda-8773-4c50-9b48-5159bb2d1464/10-react-native-preview-opt.png" alt="Loading screen we just finished building." /></a><figcaption>Loading screen we just finished building.</figcaption></figure>

After a few seconds you should see the screen that says “Data loaded”.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6880e6ba-fb94-41c1-8918-6880f61f8399/11-react-native-preview-opt-178x118.png"><img loading="lazy" decoding="async" title="Data loaded message is visible once data finishes loading." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6880e6ba-fb94-41c1-8918-6880f61f8399/11-react-native-preview-opt-178x118.png" alt="Data loaded message is visible once data finishes loading." /></a><figcaption>The data loaded message is visible once data finishes loading.</figcaption></figure>

## 4\. Filtering And Picking Random Wallpapers

In this section we will filter through the wallpaper data and pick specified number of random wallpapers.

This section will focus more on JavaScript than React Native. We will go through creating a new module (file) that will handle random number generation. If modules in JavaScript sound new to you, consider going through the <a href="https://nodejs.org/api/modules.html#modules_modules">Node.js modules docs</a>.

Go to the line above the <code>class</code> declaration and declare a new constant that will tell the app the number of random wallpapers to pick; let’s make it five.</p>

<pre><code class="language-javascript">const NUM_WALLPAPERS = 5;</code></pre>

Now we’re going to create a module that’ll help us with the generation of random numbers. This module will export two functions. Let's look a look at each one of them.

*   `uniqueRandomNumbers`: This function takes in three arguments. First is the number of random numbers that are to be returned. The next two arguments define the range in which the random numbers are to be returned, namely `lowerLimit` and `upperLimit`. If you call the function `uniqueRandomNumbers(5, 10, 20)` you will be returned an array of five unique random numbers between 10 and 20.
*   `randomNumberInRange`: This function takes in two arguments defining the lower and upper limit respectively between which a single random number is returned. For example, if you call `randomNumberInRange(2, 10)` a unique random number between 2 and 10 is returned.

We could have merged both of these functions into one, but as I am a preacher of good quality code, I follow the <a href="https://en.wikipedia.org/wiki/Single_responsibility_principle">single responsibility principle</a>. SRP states, more or less, that each function should do one thing well and not do anything else. Following good programming principles saves you from a number of future headaches.

Create a new file in the same directory as <i>index.ios.js</i>. If we wanted to, we can put these functions in <i>index.ios.js</i>, but think about it: for the kind of purpose this new file serves we can simply copy this file and paste in any of our new projects that requires generation of random numbers and use it from there. Also, this keeps the code within <i>index.ios.js</i> that much cleaner.

We’ll call the file <i>RandManager.js</i>. Shown below is its content:

<pre><code class="language-javascript">module.exports = {
	uniqueRandomNumbers(numRandomNumbers, lowerLimit, upperLimit) {
		var uniqueNumbers = [];
		while( uniqueNumbers.length != numRandomNumbers ) {
			var currentRandomNumber = this.randomNumberInRange(lowerLimit, upperLimit);
			if( uniqueNumbers.indexOf(currentRandomNumber) === -1 ) 
				uniqueNumbers.push(currentRandomNumber);
		}
		return uniqueNumbers;
	},

	randomNumberInRange(lowerLimit, upperLimit) {
		return Math.floor( Math.random() * (1 + upperLimit - lowerLimit) ) + lowerLimit;
	}

};</code></pre>

Don’t forget to require the <code>RandManager</code> module in <i>index.ios.js</i>. Just add: <code>var RandManager = require(‘./RandManager.js’);</code> below the <code>use strict;</code> statement. Once we have <code>RandManager</code> ready, we’ll make the following changes to our <code>fetchWallsJSON</code> function:

<pre><code class="language-javascript">fetchWallsJSON() {
  var url = 'https://unsplash.it/list';
  fetch(url)
    .then( response =&gt; response.json() )
    .then( jsonData =&gt; {
    /***/
      var randomIds = RandManager.uniqueRandomNumbers(NUM_WALLPAPERS, 0, jsonData.length);
      var walls = [];
      randomIds.forEach(randomId =&gt; {
        walls.push(jsonData[randomId]);
      });

      this.setState({
        isLoading: false,
        wallsJSON: [].concat(walls)
      });
    /***/
    })
    .catch( error =&gt; console.log('JSON Fetch error : ' + error) );
}</code></pre>

Once we have the <code>jsonData</code>, we retrieve unique random numbers from <code>RandManager</code> and store them in the <code>randomIds</code> array. We then loop through this array, picking up wallpaper data objects present at a particular <code>randomId</code> and storing them in <code>walls</code> array.

Then we update our state variables: <code>isLoading</code> to false as data has been downloaded; and <code>wallsJSON</code> to <code>walls</code>.

To see the results, modify the <code>renderResults</code> function to resemble the following:

<pre><code class="language-javascript">renderResults() {
/***/
  var {wallsJSON, isLoading} = this.state;
  if( !isLoading ) {
    return (

  . &lt;View&gt;
        {wallsJSON.map((wallpaper, index) =&gt; {
          return(
            &lt;Text key={index}&gt;
              {wallpaper.id}
            &lt;/Text&gt;
          );
        })}

   .&lt;/View&gt;
    );
  }
/***/
}
</code></pre>

In the very first line inside <code>renderResults</code> we’re using a new ES2015 feature called <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment">destructuring</a>. With destructuring we have managed to substitute:

<pre><code class="language-javascript">var wallsJSON = this.state.wallsJSON,
	isLoading = this.state.isLoading;
</code></pre>

with:

<pre><code class="language-javascript">var {wallsJSON, isLoading} = this.state;</code></pre>

ES2015 is pretty cool, I am telling you.

Then, inside the <code>View</code> we loop through the retrieved <code>wallsJSON</code> data using <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map">map</a>. Whenever you want to loop through a collection in <a href="https://facebook.github.io/jsx/">JSX</a> you use the <code>map</code> construct.

Also, when looping through an array or collection and rendering a component, React Native requires you to give a <code>key</code>, a unique ID to each of the child components that renders. That is why you see a <em>key</em> property in

<pre><code class="language-javascript">&lt;Text key={index}&gt;</code></pre>

Once the simulator refreshes…

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/157f63d3-90e6-4872-bdfe-b889a8c9b3a5/12-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Randomly generated Ids are visible once data finishes loading." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/157f63d3-90e6-4872-bdfe-b889a8c9b3a5/12-react-native-preview-opt.png" alt="Randomly generated Ids are visible once data finishes loading." /></a><figcaption>Randomly generated IDs are visible once data finishes loading.</figcaption></figure>

We see five different random wallpaper IDs being displayed. Change <code>{wallpaper.id}</code> to <code>{wallpaper.author}</code> in <code>renderResults</code> and you should see something like the following.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38b98729-2792-408e-a1a2-c78c271f9ddb/13-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Author names corresponding to random ids." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38b98729-2792-408e-a1a2-c78c271f9ddb/13-react-native-preview-opt.png" alt="Author names corresponding to random ids." /></a><figcaption>Author names corresponding to random IDs.</figcaption></figure>

Great! Now we’re talking. We are now able to fetch and filter the specified number (five, in this case) of random wallpapers from the API. Looks like we’re done for this section. High five!

## 5\. Adding The Swiper Component

In this section we will include a <em>Swiper</em> component in our app. This component will allow us to display wallpapers in a swipeable container.

You'll learn how to include a third-party React Native component in our app. React Native has amazing community support and on GitHub there is a <a href="https://react.parts/native">rich collection</a> of all kinds of different third-party components.

For our purposes we will use <a href="https://github.com/leecade/react-native-swiper">react-native-swiper</a>.

Head to the project directory in the terminal and run the following command:

<pre><code class="bash">npm install react-native-swiper --save</code></pre>

Now require the <code>Swiper</code> component: add <code>var Swiper = require(‘react-native-swiper’);</code> below <code>use strict</code>.

Let's try out our newly included <code>Swiper</code> component.

Go to the <code>renderResults</code> method and replace <code>View</code> with <code>Swiper</code>. After doing this, your <code>renderResults</code> should look like this:

<pre><code class="language-javascript">renderResults() {
  var {wallsJSON, isLoading} = this.state;
  if( !isLoading ) {
    return (
    /***/
      &lt;Swiper&gt;
    /***/
        {wallsJSON.map((wallpaper, index) =&gt; {
          return(
            &lt;Text key={index}&gt;
              {wallpaper.author}
            &lt;/Text&gt;
          );
        })}
    /***/
      &lt;/Swiper&gt;
    /***/
    );
  }
}
</code></pre>

Doing so results in the following:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b659f6-d0c1-4050-9c97-5bb0b2f90e05/14-react-native-preview-opt.png"><img loading="lazy" decoding="async" title="Each author name visible in its very own container." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f7b659f6-d0c1-4050-9c97-5bb0b2f90e05/14-react-native-preview-opt.png" alt="Each author name visible in its very own container." /></a><figcaption>Each author name is visible in its very own container.</figcaption></figure>

Instead of showing the names of authors as a list, we have put them in a swiper which gives each wallpaper its very own screen, which we can swipe across. We need to do a couple more things here: add the following attributes to the <code>Swiper</code> component as shown.</p>

<pre><code class="language-javascript">&lt;Swiper
/***/
dot.{&lt;View style={{backgroundColor:'rgba(255,255,255,.4)', width: 8, height: 8,borderRadius: 10, marginLeft: 3, marginRight: 3, marginTop: 3, marginBottom: 3,}} /&gt;}

activeDot.{&lt;View style={{backgroundColor: '#fff', width: 13, height: 13, borderRadius: 7, marginLeft: 7, marginRight: 7}} /&gt;}

loop={false}

    {wallsJSON.map((wallpaper, index) =&gt; {
      return(
        &lt;Text key={index}&gt;
          {wallpaper.author}
        &lt;/Text&gt;
      );
    })}
  &lt;/Swiper&gt;
</code></pre>

Doing this:

*   Styles the pagination dots (makes the blue dots you see at the bottom in the previous image white and bigger).
*   Disables continuous swiping (`loop={false}`). That is, once you reach the final page and you swipe further you’re not taken back to the first wallpaper.
*   Will fire `onMomentumScrollEnd` (which we’ll be delving further into in the next part of the tutorial) each time we’re done swiping.

With this, we’ve come to an end of the first part. What a journey!

## To Sum Up The React Native Tutorial

*   In the first section you learned how to set up a blank React Native project in Xcode.
*   In the second section we talked about ES2015 classes and why you should prefer the newer syntax along with creating state variables and grabbing raw data from the API.
*   In section three we went over dynamically rendering the app based on the value a state variable holds. Also, we did some light flexbox positioning.
*   In the fourth section we created a brand new module to handle random number generation and also went over including it in the main file.
*   In the last section we added the first third-party component to our app, which was a cakewalk, thanks to Node.

Up until now, to be honest, our app doesn't look very special. I know. In the next part we will add actual images instead of just author names. Not only that, we will be doing some advanced stuff like creating a custom double-tap detector using the <code>PanHandler</code> API. You will learn how to link a library in Xcode and grant your app access to the Camera Roll. We will also create our very own component and a lot more. Sound interesting? See you in the next part.

{{< signature "da, ml, og, il" >}}


---
title: Why You Should Consider React Native For Your Mobile App
slug: consider-react-native-mobile-app
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1accc284-5885-44b9-8538-126c8097c468/reactive-native-preview-opt.png
date: 2016-04-07T12:56:53.000Z
author: claytonanderson
description: >-
  Like many others, I was initially skeptical of Facebook and Instagram's
  [React](https://facebook.github.io/react/). Initial demos of React's JavaScript
  language extension, JSX, made many developers uneasy. For years we had worked
  to separate HTML and JavaScript, but React seemed to combine them. Many also
  questioned the need for yet another client-side library in an ocean full of
  them.

  As it turns out, React has proved tremendously successful, both on my own
  projects, and with many others around the web, including large companies like
  [Netflix](https://techblog.netflix.com/2015/01/netflix-likes-react.html). And
  now with [React Native](https://facebook.github.io/react-native/), the
  framework has been brought to mobile. React Native is a great option for
  creating performant iOS and Android apps that feel at home on their respective
  platforms, all while building on any previous web development experience.
categories:
  - Coding
  - Mobile
  - Apps
  - React
---
Like many others, I was initially skeptical of Facebook and Instagram's <a href="https://facebook.github.io/react/">React</a>. Initial demos of React's JavaScript language extension, JSX, made many developers uneasy. For years we had worked to separate HTML and JavaScript, but React seemed to combine them. Many also questioned the need for yet another client-side library in an ocean full of them.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1accc284-5885-44b9-8538-126c8097c468/reactive-native-preview-opt.png" alt="react native" title="Why You Should Consider React Native For Your Mobile App" width="500" height="208" /></figure>

As it turns out, React has proved tremendously successful, both on my own projects, and with many others around the web, including large companies like <a href="https://techblog.netflix.com/2015/01/netflix-likes-react.html">Netflix</a>. And now with <a href="https://facebook.github.io/react-native/">React Native</a>, the framework has been brought to mobile. React Native is a great option for creating performant iOS and Android apps that feel at home on their respective platforms, all while building on any previous web development experience.</p>

## <span class="rh">Further Reading</span> on SmashingMag

*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Test Automation For Apps, Games And The Mobile Web](https://www.smashingmagazine.com/2015/01/basic-test-automation-for-apps-games-and-mobile-web/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)

{{% feature-panel %}}

This article will explain why I think you should consider using React Native, by providing an overview of the framework and what I believe to be its best features.</p>

## React Overview

Described by its creators as “A JavaScript library for building user interfaces”, React focuses on the view portion of your application. In more concrete terms, this means that when writing a React Native app, your view code will consist of writing React components, which are small pieces of code that describe how a portion of your app should look based on some set of input data. Let's look at a small example component which can be used to display a simple button. (I am omitting styles for the sake of clarity.)

<pre><code class="language-javascript">
const Button = React.createClass({
	propTypes: {
		onPress: React.PropTypes.func.isRequired,
		text: React.PropTypes.string.isRequired,
	},

	render() {
		return (
			&lt;TouchableOpacity onPress={this.props.onPress} style={...}&gt;
				&lt;Text style={...}&gt;{this.props.text}&lt;/Text&gt;
			&lt;/TouchableOpacity&gt;
		);
	}
});
</code></pre>

This <code>Button</code> component has two pieces of input data: <code>onPress</code>, which is a callback function for when the button is pressed; and <code>text</code>, which is the string to display inside the button. The <a href="https://www.smashingmagazine.com/2014/02/applying-xsl-transformations-to-responsive-web-design/">XML-like structure</a> you see returned by the <code>render</code> function is called JSX, which is syntactic sugar for React function calls. And <code>TouchableOpacity</code> and <code>Text</code> are existing components that are included with React Native. Now that this <code>Button</code> component has been created, it can be used many times throughout the application, with consistent behavior and styling.

While this is a simple example, it demonstrates how a React app is built, piece by piece. Continuing in this manner, you can create components that represent increasing layers of abstraction. For example, you might create a <code>ButtonGroup</code> component that contains several connected buttons. And building on top of that, you can write components that represent entire screens. Even as your app gets significantly larger, components remain understandable and manageably sized at each level.</p>

## Truly Native

Most mobile apps built with JavaScript use <a href="https://cordova.apache.org/">Cordova</a>, or a framework built on top of it, such as the popular <a href="https://ionicframework.com/">Ionic</a> or <a href="https://www.sencha.com/products/touch/">Sencha Touch</a>. With Cordova, you have the ability to make calls to native APIs, but the bulk of your app will be HTML and JavaScript inside a WebView. While you can approximate native components – and it is certainly possible to build a great UI with HTML and JS – no Cordova app will match the look and feel of a real native app. The little things - like scrolling acceleration, keyboard behavior, and navigation - all add up and can create frustrating experiences for your customers when they don't behave as expected.

Although you still write JavaScript with React Native, the components you define will end up rendering as native platform widgets. If you are familiar with React for the web, you'll feel right at home. And if you have written apps in Java or Objective-C, you'll immediately recognize many of React Native's components.

React's best feature when it originally launched for the web was making your app's view layer a pure output of state. As a developer, this means that instead of imperatively making changes to view components (for example, programmatically altering the text or color of a button by calling a function on it), you simply define what your view should look like based on input data, and React intelligently makes the changes for you when the state changes.

This shift in thinking can drastically <a href="https://www.smashingmagazine.com/2016/06/designing-modular-ui-systems-via-style-guide-driven-development/">simplify building UIs</a>. We've all used apps where the UI enters a weird unintended state after taking a path the developer didn't expect. With React, bugs like this are much easier to track down. You don't have to think as much about the user's path through the system, instead focusing on making sure your view declarations can handle all possible shapes for your app's state. This is a much easier problem to solve - and to test for. It is also more easily understood by the computer, so improvements to static analysis and type systems will only make these bugs easier to find.

React Native component definitions look and behave pretty much just like React for web components, but target native UI widgets instead of HTML. So instead of using a <code>&lt;div&gt;</code>, you would use a <code>&lt;View&gt;</code> (which on iOS gets rendered to a native <code>UIView</code>, and on Android, <code>android.view</code>). When your components' data changes, React Native will calculate what in your view needs to be altered, and make the needed calls to whatever native UI widgets are displayed.

And it is fast! JavaScript isn't as fast as native code can be, but for most tasks, JavaScript and React Native are more than capable of keeping your app running at 60 frames per second. Under the hood, your JavaScript code is run on its own thread, separate from the main UI thread. So even when your app is running complex logic, your UI can still be smoothly animating or scrolling at 60fps, so long as the UI isn't blocked by the JS thread.

Many software frameworks promise that they will let you make a great app for Android and iOS, but the product frequently ends up somewhere in the middle without feeling truly native to either. By embracing the native platforms while still letting your app share the majority of its codebase between platforms, React Native enables developers to make awesome native apps their customers will love, without the increase in budget building two separate apps could entail.</p>

## Ease Of Learning

One of React's greatest strengths is how readable it is, even to those unfamiliar with it. Many frameworks require that you learn a long list of concepts that are only useful within that framework, while ignoring language fundamentals. React does its absolute best to do the opposite. As an example, consider the difference between rendering a portion of a list of friends in React Native vs Ionic (AngularJS).

With Ionic, you use the <a href="https://docs.angularjs.org/api/ng/directive/ngRepeat">ngRepeat</a> directive. Let us say we have an array of friends, each of which contains the following fields: first_name, last_name and is_online. But we only want to show those friends that are currently online. Here is our controller:

<pre><code class="language-javascript">
function FriendCtrl($scope) {
	$scope.friends = [
		{
			first_name: 'John',
			last_name: 'Doe',
			is_online: true,
		},
		{
			first_name: 'Jane',
			last_name: 'Doe',
			is_online: true,
		},
		{
			first_name: 'Foo',
			last_name: 'Bar',
			is_online: false,
		}
	];
}
</code></pre>

And here is our view:

<pre><code class="language-markup">
&lt;div ng-controller="FriendCtrl"&gt;
	&lt;ul&gt;
		&lt;li ng-repeat="friend in friends | filter:{is_online:true}"&gt;
			{{friend.last_name}}, {{friend.first_name}}
		&lt;/li&gt;
	&lt;/ul&gt;
&lt;/div&gt;
</code></pre>

If you aren't familiar with Ionic/AngularJS, this code snippet raises some immediate questions. What is <code>$scope</code>? What is the syntax for <code>filter</code>? And how would I add additional behavior, like sorting the list of friends?

With React Native, you make use of your existing knowledge of language fundamentals, using the built-in <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter">filter</a> and <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map">map</a> functions.

<pre><code class="language-javascript">
const DemoComponent = React.createClass({
	render() {
		const friends = [
			{
				first_name: 'John',
				last_name: 'Doe',
				is_online: true,
			},
			{
				first_name: 'Jane',
				last_name: 'Doe',
				is_online: true,
			},
			{
				first_name: 'Foo',
				last_name: 'Bar',
				is_online: false,
			}
		];

		return (
			&lt;View&gt;
				{friends
					.filter(f =&gt; f.is_online)
					.map(f =&gt; &lt;View&gt;{f.last_name}, {f.first_name}&lt;/View&gt;)}
			&lt;/View&gt;
		);
	}
});
</code></pre>

While the React Native snippet still raises some questions (What does <code>React.createClass</code> do? What is <code>render</code>?), the fact that the bulk of the code here is just regular JavaScript means it will be more understandable and maintainable to newcomers.

As an experienced developer, using standard language features you already know will save you time, and make your code more understandable to other developers. But just as importantly, if you are less experienced with JavaScript, React serves as an excellent teaching tool. If you haven't yet learned how to use map or filter, learning React will teach you those too. Learning ngRepeat only teaches you ngRepeat.

And that is before considering multiplatform mobile development. While there will be some pieces of platform-specific code in a React Native project that targets both iOS and Android, the majority will be shared and all of it will be understandable to a JavaScript developer.

## Vibrant Ecosystem

Since the majority of your React Native code is just plain JavaScript, it reaps the benefits of all the advancements in the language and its ecosystem. Instead of waiting on your framework developers to implement all the array manipulation functions you want, why not just use <a href="https://lodash.com/">lodash</a>? For manipulating or displaying dates and times, just use <a href="https://momentjs.com/">Moment.js</a>. And all those amazing new <a href="https://github.com/lukehoban/es6features">ES6 language features</a> you've been waiting to try out? Not only is React a great fit, their use is encouraged!

Thanks to its declarative views, certain libraries are particularly suited for use with React Native. One I'd be remiss not to mention is <a href="https://redux.js.org/">redux</a>. Described as a "predictable state container", redux is an awesome library for manipulating your application's state. Redux is highly testable, and encourages writing small functions that are explicit about what data they change. Once your state changes are written this way, your app can take advantage of powerful features, like global <a href="https://rackt.org/redux/docs/recipes/ImplementingUndoHistory.html">undo/redo</a> and <a href="https://www.youtube.com/watch?v=xsSnOQynTHs">hot reloading</a>.</p>

## Developer Experience

Happy developers are productive developers, and React Native has a great development environment. Instead of repeatedly waiting for your code to compile and your app to restart while making tiny edits, changes to a React Native codebase are made to your running app without the need to restart (<a href="https://www.youtube.com/watch?v=7rDsRXj9-cU&amp;t=22m56s">see a demo of that here</a>).

And if you've written any JavaScript before, you're probably already familiar with the Chrome developer tools. When running React Native in development mode, you can attach to your desktop Chrome browser, so you'll be right at home with its debugger and profiling tools. Attaching to Chrome works either in the simulator or connected to a physical device.

For creating your app's layout, React Native uses <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes">flexbox</a>. While every layout engine has its own learning curve, upsides and downsides, React Native's support for flexbox means you can use the exact same layout code for Android, iOS and web, instead of learning three different engines.</p>

## And Beyond!

React Native apps consist entirely, or close to that, of JavaScript. If you let your mind wander, this opens up a world of opportunities.</p>

### Code Sharing

We've already discussed how React Native can share code between Android and iOS, but what about the web? Anything in a React project that doesn't directly tie to a native platform is already sharable. Think about an app that can render on the server, in a web browser, or on Android or iOS - all driven by one shared codebase. While we aren't quite there yet, the community is working on it. Keep an eye on the <a href="https://github.com/necolas/react-native-web">react-native-web</a> project.</p>

### Live Updates

Anyone who has shipped an iOS app has experienced the frustration of waiting for App Store approval. With React Native, it is possible to do live updates to your app without going through the App Store - much like for a web app. Since the bulk of your app will be JavaScript, you can fetch updates on the fly over the network. There are already services to help with this like <a href="https://apphub.io/">AppHub</a>, or you could build it yourself. As long as your app is aware of what version it is running and knows how to check the server for a newer version, you can publish updates to your app whenever you like. Long app approval times aren't a problem on Android, but you can still use live updates as a way of guaranteeing your customers have the latest and greatest version of your app installed.</p>

## Conclusion

Between the ease of development, quality of the apps built with it, and the richness of the platform and ecosystem, I've had a lot of fun learning and building with React Native. If you want to learn more, check out the links below!

### Resources

*   [A Deep Dive into React Native](https://www.youtube.com/watch?v=7rDsRXj9-cU)
*   [React Native Tutorial](https://facebook.github.io/react-native/docs/tutorial.html#content)
*   [Removing User Interface Complexity, or Why React is Awesome](https://jlongster.com/Removing-User-Interface-Complexity,-or-Why-React-is-Awesome)
*   [React Cheatsheet](https://ricostacruz.com/cheatsheets/react.html)

{{< signature "da, jb, ml, og" >}}


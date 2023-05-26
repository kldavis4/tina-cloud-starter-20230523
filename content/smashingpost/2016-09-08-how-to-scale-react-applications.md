---
title: How To Scale React Applications
slug: how-to-scale-react-applications
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64d9d69f-c8f5-45fd-873f-df71dfc257d8/react-boilerplate-v3-release-screenshot-500px-opt.png
date: 2016-09-08T17:49:35.000Z
author: maxstoiber
summary: >-
  Due to rich web applications, scaling has become an important topic on the frontend. The frontend of a complex app needs to be able to handle a large number of users, developers and parts. Max Stoiber shares everything you need to now about React Boilerplate to get started.
description: >-
  Due to rich web applications, scaling has become an important topic on the frontend. The frontend of a complex app needs to be able to handle a large number of users, developers and parts. Max Stoiber shares everything you need to now about React Boilerplate to get started.
categories:
  - Coding
  - Tools
  - JavaScript
  - React
---
We recently released version 3 of [React Boilerplate](https://github.com/mxstbr/react-boilerplate), one of the most popular React starter kits, after several months of work. The team spoke with hundreds of developers about how they build and scale their web applications, and I want to share some things we learned along the way.</p>

<figure><a href="https://twitter.com/mxstbr/status/732833839140229120"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/64d9d69f-c8f5-45fd-873f-df71dfc257d8/react-boilerplate-v3-release-screenshot-500px-opt.png" alt="Announcement of react-boilerplate v3 on Twitter" width="500" height="296" /></a><figcaption>The <a href="https://twitter.com/mxstbr/status/732833839140229120">tweet that announced</a> the release of version 3 of React Boilerplate</figcaption></figure>

We realized early on in the process that we didn’t want it to be "just another boilerplate." We wanted to give developers who were starting a company or building a product the best foundation to start from and to scale.

Traditionally, scaling was mostly relevant for server-side systems. As more and more users would use your application, you needed to make sure that you could add more servers to your cluster, that your database could be split across multiple servers, and so on.

Nowadays, due to rich web applications, scaling has become an important topic on the front end, too! The front end of a complex app needs to be able to handle a large number of users, developers and parts. These three categories of scaling (users, developers and parts) need to be accounted for; otherwise, there will be problems down the line.</p>

## <span class="rh">Further Reading</span> on SmashingMag

*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Test Automation For Apps, Games And The Mobile Web](https://www.smashingmagazine.com/2015/01/basic-test-automation-for-apps-games-and-mobile-web/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)

{{% feature-panel %}}

## Containers And Components

The first big improvement in clarity for big applications is the **differentiation between stateful ("containers") and stateless ("components") components**. Containers manage data or are connected to the state and generally don’t have styling associated with them. On the other hand, components have styling associated with them and aren’t responsible for any data or state management. I found this confusing at first. Basically, containers are responsible for how things work, and components are responsible for how things look.

Splitting our components like this enables us to cleanly separate reusable components and intermediary layers of data management. As a result, you can confidently go in and edit your components without worrying about your data structures getting messed up, and you can edit your containers without worrying about the styling getting messed up. Reasoning through and working with your application become much easier that way, the clarity being greatly improved!

## Structure

Traditionally, developers structured their React applications by type. This means they had folders like `actions/`, `components/`, `containers/`, etc.

Imagine a navigation bar container named `NavBar`. It would have some state associated with it and a `toggleNav` action that opens and closes it. This is how the files would be structured when grouped by type:

<pre><code class="language-javascript">react-app-by-type
		├── css
		├── actions
		│   └── NavBarActions.js
		├── containers
		│   └── NavBar.jsx
		├── constants
		│   └── NavBarConstants.js
		├── components
		│   └── App.jsx
		└── reducers
		    └── NavBarReducer.js
</code></pre>

While this works fine for examples, once you have hundreds or potentially thousands of components, development becomes very hard. To add a feature, you would have to search for the correct file in half a dozen different folders with thousands of files. This would quickly become tedious, and confidence in the code base would wane.

After a long discussion in our GitHub issues tracker and trying out a bunch of different structures, we believe we have found a much better solution:

Instead of grouping the files of your application by type, **group them by feature**! That is, put all files related to one feature (for example, the navigation bar) in the same folder.

Let’s look at what the folder structure would look like for our `NavBar` example:

<pre><code class="language-javascript">react-app-by-feature
		├── css
		├── containers
		│&nbsp;&nbsp;&nbsp;&nbsp;└── NavBar
		│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── NavBar.jsx
		│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── actions.js
		│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── constants.js
		│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── reducer.js
		└── components
		    └── App.jsx
</code></pre>

Developers working on this application would need to go into only a single folder to work on something. And they would need to create only a single folder to add a new feature. Renaming is easy with find and replace, and hundreds of developers could work on the same application at once without causing any conflicts!

When I first read about this way of writing React applications, I thought, "Why would I ever do that? The other way works absolutely fine!" I pride myself on keeping an open mind, though, so I tried it on a small project. I was smitten within 15 minutes. My confidence in the code base was immense, and, with the container-component split, working on it was a breeze.

It's important to note that this doesn't mean the redux actions and reducers can only be used in that component. They can (and should) be imported and used from other components!

Two questions popped into my head while working like this, though: "How do we handle styling?" and "How do we handle data-fetching?" Let me tackle these separately.</p>

{{% ad-panel-leaderboard %}}

## Styling

Apart from architectural decisions, working with CSS in a component-based architecture is hard due to two specific properties of the language itself: global names and inheritance.</p>

### Unique Class Names

Imagine this CSS somewhere in a large application:

<pre><code class="language-css">.header { /* … */ }
.title {
	background-color: yellow;
}</code></pre>

Immediately, you’ll recognize a problem: `title` is a very generic name. Another developer (or maybe even the same one some time later) might go in and write this code:

<pre><code class="language-css">.footer { /* … */ }
.title {
	border-color: blue;
}</code></pre>

This will create a naming conflict, and suddenly your title will have a blue border and a yellow background everywhere, and you’ll be digging into thousands of files to find the one declaration that has messed everything up!

Thankfully, a few smart developers have come up with a solution to this problem, which they’ve named [CSS Modules](https://github.com/css-modules/css-modules). The key to their approach is to **co-locate the styles of a component in their folder**:

<pre>
	<code>react-app-with-css-modules
		├── containers
		└── components
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── Button
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── Button.jsx
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── styles.css</code>
</pre>

The CSS looks exactly the same, except that we don’t have to worry about specific naming conventions, and we can give our code quite generic names:

<pre><code class="language-css">.button {
	/* … */
}</code></pre>

We then `require` (or `import`) these CSS files into our component and assign our JSX tag a `className` of `styles.button`:

<pre><code class="language-javascript">/* Button.jsx */
var styles = require('./styles.css');

&lt;div className={styles.button}&gt;&lt;/div&gt;
</code></pre>

If you now look into the DOM in the browser, you’ll see `<div class="MyApp__button__1co1k"></div>`! CSS Modules takes care of "uniquifying" our class names by prepending the application’s name and postpending a short hash of the contents of the class. This means that the **chance of overlapping classes is almost nil, and if they overlap, they will have the same contents anyway** (because the hash — that is, the contents — has to be the same).

## Reset Properties For Each Component

In CSS, certain properties inherit across nodes. For example, if the parent node has a `line-height` set and the child doesn’t have anything specified, it will automatically have the same `line-height` applied as the parent.

In a component-based architecture, that’s not what we want. Imagine a `Header` component and a `Footer` component with these styles:

<pre><code class="language-css">.header {
	line-height: 1.5em;
	/* … */
}

.footer {
	line-height: 1;
	/* … */
}</code></pre>

Let’s say we render a `Button` inside these two components, and suddenly our buttons look different in the header and footer of our page! This is true not only for `line-height`: About a dozen CSS properties will inherit, and tracking down and getting rid of those bugs in your application would be very hard.

In the front-end world, using a reset style sheet to normalize styles across browsers is quite common. Popular options include Reset CSS, Normalize.css and sanitize.css! What if we took that concept and had a **reset for every component**?

This is called an auto-reset, and it exists as a plugin for [PostCSS](https://postcss.org/)! If you add [PostCSS Auto Reset](https://github.com/maximkoretskiy/postcss-autoreset) to your PostCSS plugins, it’ll do this exactly: wrap a local reset around each component, setting all inheritable properties to their default values to override the inheritances.</p>

## Data-Fetching

The second problem associated with this architecture is data-fetching. Co-locating your actions to your components makes sense for most actions, but data-fetching is inherently a global action that’s not tied to a single component!

Most developers at the moment use [Redux Thunk](https://github.com/gaearon/redux-thunk) to handle data-fetching with Redux. A typical thunked action would look something like this:

<div class="break-out">

<pre><code class="language-javascript">/* actions.js */

function fetchData() {
	return function thunk(dispatch) {
		// Load something asynchronously.
		fetch('https://someurl.com/somendpoint', function callback(data) {
			// Add the data to the store.
			dispatch(dataLoaded(data));
		});
	}
}</code></pre></div>

This is a brilliant way to allow data-fetching from the actions, but it has two pain points: Testing those functions is very hard, and, conceptually, having data-fetching in the actions doesn’t quite seem right.

A big benefit of Redux is the pure action creators, which are easily testable. When returning a thunk from an action, suddenly you have to double-call the action, mock the `dispatch` function, etc.

Recently, a new approach has taken the React world by storm: [redux-saga](https://github.com/yelouafi/redux-saga). redux-saga utilizes Esnext generator functions to make asynchronous code look synchronous, and it makes those asynchronous flows very easy to test. The mental model behind sagas is that they are like a separate thread in your application that handles all asynchronous things, without bothering the rest of the application!

Let me illustrate with an example:

<div class="break-out">

<pre><code class="language-javascript">/* sagas.js */

import { call, take, put } from 'redux-saga/effects';

// The asterisk behind the function keyword tells us that this is a generator.
function* fetchData() {
	// The yield keyword means that we'll wait until the (asynchronous) function
	// after it completes.
	// In this case, we wait until the FETCH_DATA action happens.
	yield take(FETCH_DATA);
	// We then fetch the data from the server, again waiting for it with yield
	// before continuing.
	var data = yield call(fetch, 'https://someurl.com/someendpoint');
	// When the data has finished loading, we dispatch the dataLoaded action.
	put(dataLoaded(data));
}</code></pre></div>

Don’t be scared by the strange-looking code: This is a brilliant way to handle asynchronous flows!

The source code above almost **reads like a novel, avoids callback hell and, on top of that, is easy to test**. Now, you might ask yourself, why is it easy to test? The reason has to do with our ability to test for the "effects" that redux-saga exports without needing them to complete.

These effects that we import at the top of the file are handlers that enable us to easily interact with our redux code:

*   `put()` dispatches an action from our saga.
*   `take()` pauses our saga until an action happens in our app.
*   `select()` gets a part of the redux state (kind of like `mapStateToProps`).
*   `call()` calls the function passed as the first argument with the remaining arguments.

Why are these effects useful? Let’s see what the test for our example would look like:

<div class="break-out">

<pre><code class="language-javascript">/* sagas.test.js */

var sagaGenerator = fetchData();

describe('fetchData saga', function() {
	// Test that our saga starts when an action is dispatched,
	// without having to simulate that the dispatch actually happened!
	it('should wait for the FETCH_DATA action', function() {
		expect(sagaGenerator.next()).to.equal(take(FETCH_DATA));
	});

	// Test that our saga calls fetch with a specific URL,
	// without having to mock fetch or use the API or be connected to a network!
	it('should fetch the data from the server', function() {
		expect(sagaGenerator.next()).to.equal(call(fetch, 'https://someurl.com/someendpoint'));
	});

	// Test that our saga dispatches an action,
	// without having to have the main application running!
	it('should dispatch the dataLoaded action when the data has loaded', function() {
		expect(sagaGenerator.next()).to.equal(put(dataLoaded()));
	});
});</code></pre></div>

Esnext generators don’t go past the `yield` keyword until `generator.next()` is called, at which point they run the function, until they encounter the next `yield` keyword! By using the redux-saga effects, we can thus easily test asynchronous things without needing to mock anything and without relying on the network for our tests.

By the way, we co-locate the test files to the files we are testing, too. Why should they be in a separate folder? That way, all of the files associated with a component are truly in the same folder, even when we’re testing things!

If you think this is where the benefits of redux-saga end, you’d be mistaken! In fact, making data-fetching easy, beautiful and testable might be its smallest benefits!

{{% ad-panel-leaderboard %}}

### Using redux-saga as Mortar

Our components are now **decoupled**. They don’t care about any other styling or logic; they are concerned solely with their own business — well, almost.

Imagine a `Clock` and a `Timer` component. When a button on the clock is pressed, we want to start the timer; and when the stop button on the timer is pressed, you want to show the time on the clock.

Conventionally, you might have done something like this:

<div class="break-out">

<pre><code class="language-javascript">/* Clock.jsx */

import { startTimer } from '../Timer/actions';

class Clock extends React.Component {
	render() {
		return (
			/* … */
			&lt;button onClick={this.props.dispatch(startTimer())} /&gt;
			/* … */
		);
	}
}</code></pre></div>

<div class="break-out">

<pre><code class="language-javascript">/* Timer.jsx */

import { showTime } from '../Clock/actions';

class Timer extends React.Component {
	render() {
		return (
			/* … */
			&lt;button onClick={this.props.dispatch(showTime(currentTime))} /&gt;
			/* … */
		);
	}
}</code></pre></div>

Suddenly, you cannot use those components separately, and reusing them becomes almost impossible!

Instead, we can use redux-saga as the "mortar" between these decoupled components, so to speak. By listening for certain actions, we can react (pun intended) in different ways, depending on the application, which means that our components are now truly reusable.

Let’s fix our components first:

<div class="break-out">

<pre><code class="language-javascript">/* Clock.jsx */

import { startButtonClicked } from '../Clock/actions';

class Clock extends React.Component {
	/* … */
	&lt;button onClick={this.props.dispatch(startButtonClicked())} /&gt;
	/* … */
}</code></pre></div>

<div class="break-out">

<pre><code class="language-javascript">/* Timer.jsx */

import { stopButtonClicked } from '../Timer/actions';

class Timer extends React.Component {
	/* … */
	&lt;button onClick={this.props.dispatch(stopButtonClicked(currentTime))} /&gt;
	/* … */
}</code></pre></div>

Notice how each component is concerned only with itself and imports only its own actions!

Now, let’s use a saga to tie those two decoupled components back together:

<div class="break-out">

<pre><code class="language-javascript">/* sagas.js */

import { call, take, put, select } from 'redux-saga/effects';

import { showTime } from '../Clock/actions';
import { START_BUTTON_CLICKED } from '../Clock/constants';
import { startTimer } from '../Timer/actions';
import { STOP_BUTTON_CLICKED } from '../Timer/constants';

function* clockAndTimer() {
	// Wait for the startButtonClicked action of the Clock
	// to be dispatched.
	yield take(START_BUTTON_CLICKED);
	// When that happens, start the timer.
	put(startTimer());
	// Then, wait for the stopButtonClick action of the Timer
	// to be dispatched.
	yield take(STOP_BUTTON_CLICKED);
	// Get the current time of the timer from the global state.
	var currentTime = select(function (state) { return state.timer.currentTime });
	// And show the time on the clock.
	put(showTime(currentTime));
}</code></pre></div>

Beautiful.</p>

## Summary

Here are the key takeaways for you to remember:

*   Differentiate between containers and components.
*   Structure your files by feature.
*   Use CSS modules and PostCSS Auto Reset.
*   Use redux-saga to:
    *   have readable and testable asynchronous flows,
    *   tie together your decoupled components.

{{< signature "il, vf, al" >}}


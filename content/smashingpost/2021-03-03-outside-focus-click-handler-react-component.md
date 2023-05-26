---
title: 'Creating An Outside Focus And Click Handler React Component'
slug: outside-focus-click-handler-react-component
author: arihant-verma
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e4cdde09-0660-42a8-893c-7b47ee0ad208/outside-focus-click-handler-react-component.jpg
date: 2021-03-03T11:00:00.000Z
summary: >-
  In this article, we’ll look at how to create an outside focus and click handler with React. You’ll learn how to recreate an open-source React component (<a href="https://github.com/nanot1m/react-foco"><code>react-foco</code></a>) from scratch in doing so. To get the most out of this article, you’ll need a basic understanding of JavaScript classes, DOM event delegation and React. By the end of the article, you’ll know how you can use JavaScript class instance properties and event delegation to create a React component that helps you detect a click or focus outside of any React component.
description: >-
  In this article, we’ll look at how to create an outside focus and click handler with React. We will recreate an open source react component <a href="https://github.com/nanot1m/react-foco"><code>react-foco</code></a> from scratch in doing so.
categories:
  - Tools
  - React
  - JavaScript
---

Oftentimes we need to detect when a click has happened outside of an element or when the focus has shifted outside of it. Some of the evident examples for this use case are fly-out menus, dropdowns, tooltips and popovers. Let’s start the process of making this detection functionality.

## The DOM Way To Detect Outside Click

If you were asked to write code *to detect if a click happened inside a DOM node or outside of it*, what would you do? Chances are you’d use the [`Node.contains`](https://developer.mozilla.org/en-US/docs/Web/API/Node/contains) DOM API. Here’s how MDN explains it:

<blockquote><p>The <code>Node.contains()</code> method returns a <code>Boolean</code> value indicating whether a node is a descendant of a given node, i.e. the node itself, one of its direct children (<code>childNodes</code>), one of the children’s direct children, and so on.</p></blockquote>

Let’s quickly test it out. Let’s make an element we want to detect outside click for. I’ve conveniently given it a `click-text` class.

<pre><code class="language-html">&lt;section&gt;
  &lt;div class="click-text"&gt;
    click inside and outside me
  &lt;/div&gt;
&lt;/section&gt;</code></pre>

<pre><code class="language-javascript">const concernedElement = document.querySelector(".click-text");

document.addEventListener("mousedown", (event) => {
  if (concernedElement.contains(event.target)) {
    console.log("Clicked Inside");
  } else {
    console.log("Clicked Outside / Elsewhere");
  }
});</code></pre>

We did the following things:

1. Selected the HTML element with the class `click-text`.
2. Put a mouse down event listener on `document` and set an event handler callback function.
3. In the callback function, we are checking if our concerned element &mdash; for which we have to detect outside click &mdash; contains the element (including itself) which triggered the `mousedown` event (`event.target`). 

If the element which triggered the mouse down event is either our concerned element or any element which is inside the concerned element, it means we have clicked inside our concerned element.

Let’s click inside and outside of the element in the Codesandbox below, and check the console.

<iframe src="https://codesandbox.io/embed/sm1-outside-click-detection-in-javascript-hm7rb?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="SM1: Outside click detection in Javascript"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

## Wrapping DOM Hierarchy Based Detection Logic In A React Component

Great! So far we saw how to use DOM’s `Node.contains` API to detect click outside of an element. We can wrap that logic in a React component. We could name our new React component  `OutsideClickHandler`. Our `OutsideClickHandler` component will work like this:

<div class="break-out">

<pre><code class="language-javascript">&lt;OutsideClickHandler
  onOutsideClick={() =&gt; {
    console.log("I am called whenever click happens outside of 'AnyOtherReactComponent' component")
  }}
&gt;
  &lt;AnyOtherReactComponent /&gt;
&lt;/OutsideClickHandler&gt;</code></pre>
</div>

`OutsideClickHandler` takes in two props:

1. `children`  
It could be any valid React children. In the example above we are passing `AnyOtherReactComponent` component as `OutsideClickHandler`’s child.
    
2. `onOutsideClick`  
This function will be called if a click happens anywhere outside of `AnyOtherReactComponent` component.

Sounds good so far? Let’s actually start building our `OutsideClickHandler` component.

<pre><code class="language-javascript">import React from 'react';

class OutsideClickHandler extends React.Component {
  render() {
    return this.props.children;
  }
}</code></pre>

Just a basic React component. So far, we are not doing much with it. We’re just returning the children as they are passed to our `OutsideClickHandler` component. Let’s wrap the `children` with a div element and attach a React ref to it.

<pre><code class="language-javascript">import React, { createRef } from 'react';

class OutsideClickHandler extends React.Component {
  wrapperRef = createRef();

  render() {    
    return (
      &lt;div ref={this.wrapperRef}&gt;
        {this.props.children}
      &lt;/div&gt;
    )
  }  
}</code></pre>

We’ll use this `ref` to get access to the DOM node object associated with the `div` element. Using that, we’ll recreate the outside detection logic we made above.

Let’s attach `mousedown` event on document inside `componentDidMount` React life cycle method, and clean up that event inside `componentWillUnmount` React lifecycle method.

<div class="break-out">

<pre><code class="language-javascript">class OutsideClickHandler extends React.Component {
  componentDidMount() {
    document
      .addEventListener('mousedown', this.handleClickOutside);
  }

  componentWillUnmount(){
    document
      .removeEventListener('mousedown', this.handleClickOutside);
  }

  handleClickOutside = (event) =&gt; {
    // Here, we'll write the same outside click
    // detection logic as we used before.
  }
}</code></pre>
</div>

Now, let’s write the detection code inside `handleClickOutside` handler function.

<pre><code class="language-javascript">class OutsideClickHandler extends React.Component {
  componentDidMount() {
    document
      .addEventListener('mousedown', this.handleClickOutside);
  }

  componentWillUnmount(){
    document
      .removeEventListener('mousedown', this.handleClickOutside);
  }

  handleClickOutside = (event) =&gt; {
    if (
      this.wrapperRef.current &&
      !this.wrapperRef.current.contains(event.target)
    ) {
      this.props.onOutsideClick();
    }
  }
}</code></pre>

The logic inside `handleClickOutside` method says the following: 

> If the DOM node that was clicked (`event.target`) was neither our container div (`this.wrapperRef.current`) nor was it any node inside of it (`!this.wrapperRef.current.contains(event.target)`), we call the `onOutsideClick` prop.

This should work in the same way as the outside click detection had worked before. Let’s try clicking outside of the grey text element in the codesandbox below, and observe the console:

<iframe src="https://codesandbox.io/embed/sw2-outsideclickhandler-react-component-using-nodecontains-gcnp1?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="SW2: OutsideClickHandler react component using Node.contains"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

{{% feature-panel %}}

## The Problem With DOM Hierarchy Based Outside Click Detection Logic

But there’s one problem. Our React component doesn’t work if any of its children are rendered in a React portal.

But what are React portals?

<blockquote><p>“Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.”<br /><br />&mdash;  <a href="https://reactjs.org/docs/portals.html)">React docs for portals</a></p></blockquote>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62a69c53-9538-45eb-b4d3-6d10b859317d/1-creating-outside-focus-click-handler-react-component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62a69c53-9538-45eb-b4d3-6d10b859317d/1-creating-outside-focus-click-handler-react-component.png" width="800" height="257" sizes="100vw" caption="React children rendered in React portal do not follow top-down DOM hierarchy. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62a69c53-9538-45eb-b4d3-6d10b859317d/1-creating-outside-focus-click-handler-react-component.png'>Large preview</a>)" alt="Image showing that React children rendered in React portal do not follow top-down DOM hierarchy" >}}

In the image above, you can see that though `Tooltip` React component is a child of `Container` React component, if we inspect the DOM we find that Tooltip DOM node actually resides in a completely separate DOM structure i.e. it’s not inside the Container DOM node.

The problem is that in our outside detection logic so far, we are assuming that the children of `OutsideClickHandler` will be its direct descendants in the DOM tree. Which is not the case for React portals. If children of our component render in a React portal &mdash; which is to say they render in a separate DOM node which is outside the hierarchy of our `container div` in which our `OutsideClickHandler` component renders its children &mdash; then the `Node.contains` logic fails.

How would it fail though? If you’d try to click on the children of our `OutsideClickHandler` component &mdash; which renders in a separate DOM node using React portals &mdash; our component will register an outside click, which it shouldn’t. See for yourself:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29410830-efab-4e81-96bd-c718cf34ef13/6-creating-outside-focus-click-handler-react-component.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/abe4349b-5655-428e-9a5a-6650bd93de16/6-creating-outside-focus-click-handler-react-component-800w.gif" width="800" height="500" alt="GIF Image showing that if a React child rendered in React portal is clicked, OutsideClickHandler, which uses <code>Node.contains</code>, wrongly registers it as outside click" /></a><figcaption>Using <code>Node.contains</code> to detect outside click of React component gives wrong result for children rendered in a React portal. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/29410830-efab-4e81-96bd-c718cf34ef13/6-creating-outside-focus-click-handler-react-component.gif">Large preview</a>)</figcaption></figure>

Try it out:

<iframe src="https://codesandbox.io/embed/sm3-outsideclickhandler-with-nodecontains-do-not-work-with-portals-ebbml?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="SM3: OutsideClickHandler with Node.contains do not work with portals"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

Even though the popover that opens on clicking the button, is a child of `OutsideClickHandler` component, it fails to detect that it isn’t outside of it, and closes it down when it’s clicked.

## Using Class Instance Property And Event Delegation To Detect Outside Click

So what could be the solution? We surely can’t rely on DOM to tell us if the click is happening outside anywhere. We’ll have to do something with JavaScript by rewriting out `OutsideClickHandler` implementation.

Let’s start with a blank slate. So at this moment `OutsideClickHandler` is an empty React class.

The crux of correctly detecting outside click is:

1. To not rely on DOM structure.
2. To store the ‘clicked’ state somewhere in the JavaScript code.

For this event delegation will come to our aid. Let’s take an example of the same button and popover example we saw above in the GIF above.

We have two children of our `OutsideClickHandler` function. A button and a popover &mdash; which gets rendered in a portal outside of the DOM hierarchy of `OutsideClickHandler`, on button click, like so: 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1a55a0e-2033-4e26-9019-dad3d5340071/2-creating-outside-focus-click-handler-react-component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1a55a0e-2033-4e26-9019-dad3d5340071/2-creating-outside-focus-click-handler-react-component.png" width="800" height="483" sizes="100vw" caption="DOM Hierarchy of <code>document</code>, the <code>OutsideClickHandler</code> component, and its children rendered in React portal. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1a55a0e-2033-4e26-9019-dad3d5340071/2-creating-outside-focus-click-handler-react-component.png'>Large preview</a>)" alt="DOM Hierarchy of document, the OutsideClickHandler component, and its children rendered in React portal" >}}

When either of our children are clicked we set a variable `clickCaptured` to `true`. If anything outside of them is clicked, the value of `clickCaptured` will remain `false`.

We will store `clickCaptured`’s value in:

1. A class instance property, if you are using a class react component.
2. A ref, if you are using a functional React component.

{{% ad-panel-leaderboard %}}

We aren’t using React state to store `clickCaptured`’s value because we aren’t rendering anything based off of this `clickCaptured` data. The purpose of `clickCaptured` is ephemeral and ends as soon as we’ve detected if the click has happened inside or outside.

Let’s seee in the image below the logic for setting `clickCaptured`:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/879063d5-ffb0-4b50-88ea-5f5196d62fad/3-creating-outside-focus-click-handler-react-component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/879063d5-ffb0-4b50-88ea-5f5196d62fad/3-creating-outside-focus-click-handler-react-component.png" width="800" height="463" sizes="100vw" caption="When any of the children of the <code>OutsideClickHandler</code> component are clicked, we set <code>clickCaptured</code> to <code>true</code>. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/879063d5-ffb0-4b50-88ea-5f5196d62fad/3-creating-outside-focus-click-handler-react-component.png'>Large preview</a>)" alt="Diagram showing setting of clickCaptured to true variable when children of OutsideClickHandler component are clicked" >}}

Whenever a click happens anywhere, it bubbles up in React by default. It’ll reach to the `document` eventually.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35d75325-af9e-4160-a667-f4857839dbeb/4-creating-outside-focus-click-handler-react-component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35d75325-af9e-4160-a667-f4857839dbeb/4-creating-outside-focus-click-handler-react-component.png" width="800" height="347" sizes="100vw" caption="The value of the <strong>clickCaptured</strong> variable when mousedown event bubbles upto document &mdash; for both inside and outside click cases. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35d75325-af9e-4160-a667-f4857839dbeb/4-creating-outside-focus-click-handler-react-component.png'>Large preview</a>)" alt="Diagram showing the value of clickCaptured variable when mousedown event bubbles upto document, for both inside and outside click cases" >}}

When the click reaches `document`, there are two things that might have happened:

1.  `clickCaptured` will be true, if children where clicked.
2. `clickCaptured` will be false, if anywhere outside of them was clicked.

In the document’s event listener we will do two things now:

1.  If `clickCaptured` is true, we fire an outside click handler that the user of `OutsideClickHandler` might have given us through a prop.
2. We reset `clickCaptured` to `false`, so that we are ready for another click detection.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8157d7f6-976d-43f0-9197-40f1bf28fddb/5-creating-outside-focus-click-handler-react-component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8157d7f6-976d-43f0-9197-40f1bf28fddb/5-creating-outside-focus-click-handler-react-component.png" width="800" height="411" sizes="100vw" caption="Detecting if click happened inside or outside of React component by checking <code>clickCapture</code>’s value when mousedown event reaches document. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8157d7f6-976d-43f0-9197-40f1bf28fddb/5-creating-outside-focus-click-handler-react-component.png'>Large preview</a>)" alt="Diagram showing the detection of if click happened inside or outside of React component by checking clickCapture’s value when mousedown event reaches document" >}}

Let’s translate this into code.

<pre><code class="language-javascript">import React from 'react'

class OutsideClickHandler extends React.Component {
  clickCaptured = false;
  
  render() {
    if ( typeof this.props.children === 'function' ) {
      return this.props.children(this.getProps())
    }

    return this.renderComponent()
  }
}</code></pre>

We have the following things:

1. set initial value of `clickCaptured` instance property to `false`.
2. In the `render` method, we check if `children` prop is a function. If it is, we call it and pass it all the props we want to give it by calling `getProps` class method. We haven’t implemented `getProps` just yet.
3. If the `children` prop is not a function, we call `renderComponent` method. Let’s implement this method now.

<pre><code class="language-javascript">class OutsideClickHandler extends React.Component {
  renderComponent() {
    return React.createElement(
      this.props.component || 'span',
      this.getProps(),
      this.props.children
    )
  }
}</code></pre>

Since we aren’t using JSX, we are directly using React’s [**createElement**](https://reactjs.org/docs/react-api.html#createelement) API to wrap our children in either `this.props.component` or a `span`. `this.props.component` can be a React component or any of the HTML element’s tag name like ‘div’, ‘section’, etc. We pass all the props that we want to pass to our newly created element by calling `getProps` class method as the second argument.

Let’s write the `getProps` method now:

<pre><code class="language-javascript">class OutsideClickHandler extends React.Component {
  getProps() {
    return {
      onMouseDown: this.innerClick,
      onTouchStart: this.innerClick
    };
  }
}</code></pre>

Our newly created React element, will have the following props passed down to it: `onMouseDown` and `onTouchStart` for touch devices. Both of their values is the `innerClick` class method.

<pre><code class="language-javascript">class OutsideClickHandler extends React.Component {
  innerClick = () =&gt; {
    this.clickCaptured = true;
  }
}</code></pre>

If our new React component or anything inside of it &mdash; which could be a React portal &mdash; is clicked, we set the `clickCaptured` class instance property to true. Now, let’s add the `mousedown` and `touchstart` events to the document, so that we can capture the event that is bubbling up from below.

<div class="break-out">

<pre><code class="language-javascript">class OutsideClickHandler extends React.Component {
  componentDidMount(){
    document.addEventListener('mousedown', this.documentClick);
    document.addEventListener('touchstart', this.documentClick);
  }

  componentWillUnmount(){
    document.removeEventListener('mousedown', this.documentClick);
    document.removeEventListener('touchstart', this.documentClick);
  }

  documentClick = (event) =&gt; {
    if (!this.clickCaptured && this.props.onClickOutside) {
      this.props.onClickOutside(event);
    }
    this.clickCaptured = false;
  };
}</code></pre>
</div>

In the document **mousedown** and **touchstart** event handlers, we are checking if `clickCaptured` is falsy. 

1. `clickCaptured` would only be `true` if children of our React component would have been clicked.
2. If anything else would have been clicked `clickCaptured` would be `false`, and we’d know that outside click has happened.

If `clickCaptured` is falsy, we’ll call the `onClickOutside` method passed down in a prop to our `OutsideClickHandler` component.

That’s it! Let’s confirm that if we click inside the popover it doesn’t get closed now, as it was before:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ead1f85-65b9-4af4-836b-de052243a628/9-creating-outside-focus-click-handler-react-component.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e4786e0-bc77-47da-99c2-af8e9e482586/9-creating-outside-focus-click-handler-react-component-800w.gif" width="800" height="500" alt="GIF Image showing that if a React child rendered in React portal is clicked, OutsideClickHandler component, which uses event delegation, correctly registers it as inside click, and not outside click" /></a><figcaption>Using event delegation logic correctly detects an outside click, even if children are rendered in a React portal. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5ead1f85-65b9-4af4-836b-de052243a628/9-creating-outside-focus-click-handler-react-component.gif">Large preview</a>)</figcaption></figure>

Let’s try it out:

<iframe src="https://codesandbox.io/embed/sm4-outsideclickhandler-re-write-to-support-portals-cm51z?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="SM4: OutsideClickHandler Re Write To Support Portals"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

Wonderful!

{{% ad-panel-leaderboard %}}

## Outside Focus Detection

Now let’s take a step further. Let’s also add functionality to detect when focus has shifted outside of a React component. It’s going to be very similar implementation as we’ve done with click detection. Let’s write the code.

<div class="break-out">

 <pre><code class="language-javascript">class OutsideClickHandler extends React.Component {
  focusCaptured = false

  innerFocus = () =&gt; {
    this.focusCaptured = true;
  }

componentDidMount(){
    document.addEventListener('mousedown', this.documentClick);
    document.addEventListener('touchstart', this.documentClick);
    document.addEventListener('focusin', this.documentFocus);
  }

componentWillUnmount(){
    document.removeEventListener('mousedown', this.documentClick);
    document.removeEventListener('touchstart', this.documentClick);
    document.removeEventListener('focusin', this.documentFocus);
  }

documentFocus = (event) =&gt; {
    if (!this.focusCaptured && this.props.onFocusOutside) {
      this.props.onFocusOutside(event);
    }
    this.focusCaptured = false;
  };

getProps() { return { onMouseDown: this.innerClick, onTouchStart: this.innerClick, onFocus: this.innerFocus }; }
</code></pre>
</div>

Everything’s added mostly in the same fashion, except for one thing. You might have noticed that though we are adding an `onFocus` react event handler on our children, we are setting a `focusin` event listener to our document. Why not a `focus` event you say? Because,  🥁🥁🥁, [Starting from v17, React now maps](https://github.com/facebook/react/pull/19186) [`onFocus`](https://github.com/facebook/react/pull/19186) [React event to](https://github.com/facebook/react/pull/19186) [`focusin`](https://github.com/facebook/react/pull/19186) [native event internally.](https://github.com/facebook/react/pull/19186)

In case you are using v16 or before, instead of adding a `focusin` event handler to the document, you’ll have to add a `focus` event in capture phase instead. So that’ll be:

<pre><code class="language-javascript">document.addEventListener('focus', this.documentFocus, true);</code></pre>

Why in capture phase you might ask? Because as weird as it is, [focus event doesn’t bubble up](https://www.quirksmode.org/blog/archives/2008/04/delegating_the.html).

Since I’m using v17 in all my examples, I’m going to go ahead use the former. Let’s see what we have here:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2459bd8-4760-4322-b16a-6125eff3866f/8-creating-outside-focus-click-handler-react-component.gif"><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2932a3bf-a2ff-497e-adbe-145021e646f8/8-creating-outside-focus-click-handler-react-component-800w.gif" width="800" height="500" alt="GIF image showing correction detection of outside click and focus by React Foco component, which uses event delegation detection logic" /></a><figcaption>The React Foco component correctly detects an outside click and focus by using event delegation detection logic. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e2459bd8-4760-4322-b16a-6125eff3866f/8-creating-outside-focus-click-handler-react-component.gif">Large preview</a>)</figcaption></figure>

Let’s try it out ourselves, try clicking inside and outside of the pink background. Also use <kbd>Tab</kbd> and <kbd>Shift</kbd> + <kbd>Tab</kbd> keys ( in Chrome, Firefox, Edge ) or <kbd>Opt/Alt</kbd> + <kbd>Tab</kbd> and <kbd>Opt/Alt</kbd> + <kbd>Shift</kbd> + <kbd>Tab</kbd> (in Safari ) to toggle focussing between inner and outer button and see how focus status changes.

<iframe src="https://codesandbox.io/embed/sm5-final-component-zp0r2?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="SM5: Final Component"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

## Conclusion

In this article, we learned that the most straightforward way to detect a click outside of a DOM node in JavaScript is by using `Node.contains` DOM API. I explained the importance of knowing why using the same method to detect clicks outside of a React component doesn’t work when the React component has children which render in a React portal.

Also, now you know how to use a class instance property alongside an event delegation to correctly detect whether a click happened outside of a React component, as well as how to extend the same detection technique to outside focus detection of a React component with the `focusin` event caveat.

### Related Resources

1. [React Foco Github Repository](https://github.com/nanot1m/react-foco)
2. [mdn documentation for](https://developer.mozilla.org/en-US/docs/Web/API/Node/contains) [`Node.contains`](https://developer.mozilla.org/en-US/docs/Web/API/Node/contains) [DOM api](https://developer.mozilla.org/en-US/docs/Web/API/Node/contains)
3. [React docs for portals](https://reactjs.org/docs/portals.html)
4. [React](https://reactjs.org/docs/react-api.html#createelement) [`createElement`](https://reactjs.org/docs/react-api.html#createelement) [API](https://reactjs.org/docs/react-api.html#createelement)
5. [React Github codebase Pull Request for mapping](https://github.com/facebook/react/pull/19186) [`onFocus`](https://github.com/facebook/react/pull/19186) [and](https://github.com/facebook/react/pull/19186) [`onBlur`](https://github.com/facebook/react/pull/19186) [methods to internally use](https://github.com/facebook/react/pull/19186) [`focusin`](https://github.com/facebook/react/pull/19186) [and](https://github.com/facebook/react/pull/19186) [`focusout`](https://github.com/facebook/react/pull/19186) [native events.](https://github.com/facebook/react/pull/19186)
6. [Delegating Focus and Blur events](https://www.quirksmode.org/blog/archives/2008/04/delegating_the.html)

{{< signature "ks, vf, yk, il" >}}

---
title: An Introduction To DOM Events
slug: an-introduction-to-dom-events
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/931217a5-b0cf-4525-9f1f-85b9d516db50/illu-dom.jpg'
date: 2013-11-12T09:25:29.000Z
author: wilson-page
description: >-
  Click, touch, load, drag, change, input, error, resize — the list of possible DOM events is lengthy. Events can be triggered on any part of a document, whether by a user’s interaction or by the browser. They don’t just start and end in one place; they flow though the document, on a life cycle of their own. This life cycle is what makes DOM events so extensible and useful. As developers, **we should understand how DOM events work**, so that we can harness their potential and build engaging experiences.
categories:
  - Coding
  - Tools
  - JavaScript
  - Techniques
---
Click, touch, load, drag, change, input, error, resize — the list of possible DOM events is lengthy. Events can be triggered on any part of a document, whether by a user’s interaction or by the browser. They don’t just start and end in one place; they flow through the document, on a life cycle of their own. This life cycle is what makes DOM events so extensible and useful. As a developer, <strong>you should understand how DOM events work</strong>, so that you can harness their potential and build engaging experiences.

Throughout my time as a front-end developer, I felt that I was never given a straight explanation of how DOM events work. My aim here is to give you a clear overview of the subject, to get you up to speed more quickly than I did.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Introducing Live Extensions For Better-DOM](https://www.smashingmagazine.com/2014/02/introducing-live-extensions-better-dom-javascript/)
*   [Browser Input Events: Can We Do Better Than The Click?](https://www.smashingmagazine.com/2015/03/better-browser-input-events/)
*   [Writing A Better JavaScript Library For The DOM](https://www.smashingmagazine.com/2014/01/writing-a-better-javascript-library-for-the-dom/)
*   [Analyzing Network Characteristics Using JavaScript And The DOM](https://www.smashingmagazine.com/2011/11/analyzing-network-characteristics-using-javascript-and-the-dom-part-1/)

I will introduce the basics of working with DOM events, then delve into their inner workings, explaining how we can make use of them to solve common problems.

{{% feature-panel %}}

## Listening For DOM Events

In the past, browsers have had major inconsistencies in the way they attach event listeners to DOM nodes. Libraries such as <a title="jQuery" href="https://jquery.com/">jQuery</a> have been invaluable in abstracting away these oddities.

As we move ever closer to standardized browser environments, we can more safely use the APIs from the official specification. To keep it simple, I will describe how to manage events for the modern Web. If you are writing JavaScript for Internet Explorer (IE) 8 or below, I would advise using a <a title="addEventListener polyfill" href="https://developer.mozilla.org/en-US/docs/Web/API/EventTarget.removeEventListener#Polyfill_to_support_older_browsers">polyfill</a> or framework (such as <a title="jQuery" href="https://jquery.com">jQuery</a>) to manage event listeners.

In JavaScript, we can listen to events using this:

<pre><code class="language-javascript">
element.addEventListener(&lt;event-name&gt;, &lt;callback&gt;, &lt;use-capture&gt;);
</code></pre>

*   `event-name` (string) This is the name or type of event that you would like to listen to. It could be any of the standard DOM events (`click`, `mousedown`, `touchstart`, `transitionEnd`, etc.) or even your own custom event name (we’ll touch on custom events later).
*   `callback` (function) This function gets called when the event happens. The `event` object, containing data about the event, is passed as the first argument.
*   `use-capture` (boolean) This declares whether the callback should be fired in the “capture” phase. (Don’t worry: We’ll explain what that means a little later.)

<pre><code class="language-javascript">
var element = document.getElementById('element');

function callback() {
  alert('Hello');
}

// Add listener
element.addEventListener('click', callback);
</code></pre>

<a class="demo-button" href="https://jsbin.com/ayatif/2/edit">Demo: addEventListener</a>

## Removing Listeners

Removing event listeners once they are no longer needed is a best practice (especially in long-running Web applications). To do this, use the <code>element.removeEventListener()</code> method:

<pre><code class="language-javascript">
element.removeEventListener(&lt;event-name&gt;, &lt;callback&gt;, &lt;use-capture&gt;);
</code></pre>

But <code>removeEventListener</code> has one catch: You must have a reference to the callback function that was originally bound. Simply calling <code>element.removeEventListener('click');</code> will not work.

Essentially, if we have any interest in removing event listeners (which we should in “long-lived” applications), then we need to keep a handle on our callbacks. This means we cannot use anonymous functions.

<pre><code class="language-javascript">
var element = document.getElementById('element');

function callback() {
  alert('Hello once');
  element.removeEventListener('click', callback);
}

// Add listener
element.addEventListener('click', callback);
</code></pre>

<a class="demo-button" href="https://jsbin.com/ayamur/1/edit">Demo: removeEventListener</a>

## Maintaining Callback Context

An easy gotcha is callbacks being called with the incorrect context. Let’s explain with an example.

<pre><code class="language-javascript">
var element = document.getElementById('element');

var user = {
 firstname: 'Wilson',
 greeting: function(){
   alert('My name is ' + this.firstname);
 }
};

// Attach user.greeting as a callback
element.addEventListener('click', user.greeting);

// alert =&gt; 'My name is undefined'
</code></pre>

<a class="demo-button" href="https://jsbin.com/atoluy/1/edit">Demo: Incorrect callback context</a>

### Using Anonymous Functions

We expected the callback to correctly alert us with <code>My name is Wilson</code>. In fact, it alerts us with <code>My name is undefined</code>. In order for <code>this.firstName</code> to return <code>Wilson</code>, <code>user.greeting</code> must be called within the context (i.e. whatever is left of the dot when called) of <code>user</code>.

When we pass the <code>greeting</code> function to the <code>addEventListener</code> method, we are only passing a reference to the function; the context of <code>user</code> is not passed with it. Internally, the callback is called in the context of <code>element</code>, which means that <code>this</code> refers to <code>element</code>, not to <code>user</code>. Therefore, <code>this.firstname</code> is undefined.

There are two ways to prevent this context mismatch. First, we can call <code>user.greeting()</code> with the correct context inside an anonymous function.

<pre><code class="language-javascript">
element.addEventListener('click', function() {
  user.greeting();
  // alert =&gt; 'My name is Wilson'
});
</code></pre>

<a class="demo-button" href="https://jsbin.com/onomud/1/edit">Demo: Anonymous functions</a>

### Function.prototype.bind

The last method isn’t so good because now we don’t have a handle on the function when we want to remove it with <code>.removeEventListener()</code>. Plus, it’s pretty ugly. I prefer to use the <a title="Function.prototype.bind" href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind"><code>.bind()</code></a> method (built into all functions, as of ECMAScript 5) to generate a new function (<code>bound</code>) that will always run in the given context. We then pass that function as the callback to <code>.addEventListener()</code>.

<pre><code class="language-javascript">
// Overwrite the original function with
// one bound to the context of 'user'
user.greeting = user.greeting.bind(user);

// Attach the bound user.greeting as a callback
button.addEventListener('click', user.greeting);
</code></pre>

We also have a reference to the callback at hand, which we can use to unbind the listener if need be.

<pre><code class="language-javascript">
button.removeEventListener('click', user.greeting);
</code></pre>

<a class="demo-button" href="https://jsbin.com/ozolec/1/edit">Demo: Function.prototype.bind</a>

*   Check the [support page](https://kangax.github.io/es5-compat-table/#Function.prototype.bind) for `Function.prototype.bind` and [polyfill](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind#Compatibility) if you need it.

&nbsp;

## The Event Object

The event object is created when the event first happens; it travels with the event on its journey through the DOM. The function that we assign as a callback to an event listener is passed the event object as its first argument. We can use this object to access a wealth of information about the event that has occurred:

*   `type` (string) This is the name of the event.
*   `target` (node) This is the DOM node where the event originated.
*   `currentTarget` (node) This is the DOM node that the event callback is currently firing on.
*   `bubbles` (boolean) This indicates whether this is a “bubbling” event (which we’ll [explain later](#bubble-phase)).
*   `preventDefault` (function) This prevents any default behaviour from occurring that the user agent (i.e. browser) might carry out in relation to the event (for example, preventing a `click` event on an `<a>` element from loading a new page).
*   `stopPropagation` (function) This prevents any callbacks from being fired on any nodes further along the event chain, but it does not prevent any additional callbacks of the same event name from being fired on the current node. (We’ll talk about that [later](#stopping-propagation).)
*   `stopImmediatePropagation` (function) This prevents any callbacks from being fired on any nodes further along the event chain, including any additional callbacks of the same event name on the current node.
*   `cancelable` (boolean) This indicates whether the default behaviour of this event can be prevented by calling the [`event.preventDefault`](#preventing-default) method.
*   `defaultPrevented` (boolean) This states whether the `preventDefault` method has been called on the event object.
*   `isTrusted` (boolean) An event is said to be “trusted” when it originates from the device itself, not synthesized from within JavaScript.
*   `eventPhase` (number) This number represents the phase that the event is currently in: none (`0`), capture (`1`), target (`2`) or bubbling (`3`). We’ll go over event phases [next](#event-phases).
*   `timestamp` (number) This is the date on which the event occurred.

Many other properties can be found on the event object, but they are specific to the type of event in question. For example, mouse events will include <code>clientX</code> and <code>clientY</code> properties on the event object to indicate the location of the pointer in the viewport.

It’s best to use your favorite browser’s debugger or a <code>console.log</code> to look more closely at the event object and its properties.</p>

## Event Phases

When a DOM event fires in your app, it doesn’t just fire once where the event originated; it embarks on a journey of three phases. In short, the event flows from the document’s root to the target (i.e. capture phase), then fires on the event target (target phase), then flows back to the document’s root (bubbling phase).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/603c2b38-eaa7-4806-b5bc-cf7b3edbcd68/eventflow.png"><img class="aligncenter wp-image-129590 size-full" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/603c2b38-eaa7-4806-b5bc-cf7b3edbcd68/eventflow.png" alt="dom events" width="520" height="560" /></a><br>
<em>(Image source: <a href="https://www.w3.org/TR/DOM-Level-3-Events/#event-flow">W3C</a>)</em>

<a class="demo-button" href="https://jsbin.com/exezex/4/edit?css,js,output">Demo: Slow motion event path</a>

### Capture Phase

The first phase is the capture phase. The event starts its journey at the root of the document, working its way down through each layer of the DOM, firing on each node until it reaches the event target. The job of the capture phase is to build the propagation path, which the event will travel back through in the bubbling phase.

As mentioned, you can listen to events in the capture phase by setting the third argument of <code>addEventListener</code> to <code>true</code>. I have not found many use cases for capture phase listeners, but you could potentially prevent any clicks from firing in a certain element if the event is handled in the capture phase.

<pre><code class="language-javascript">
var form = document.querySelector('form');

form.addEventListener('click', function(event) {
  event.stopPropagation();
}, true); // Note: 'true'
</code></pre>

If you’re unsure, listen for events in the bubbling phase by setting the <code>useCapture</code> flag to <code>false</code> or <code>undefined</code>.</p>

### Target Phase

An event reaching the target is known as the target phase. The event fires on the target node, before reversing and retracing its steps, propagating back to the outermost document level.

In the case of nested elements, mouse and pointer events are always targeted at the most deeply nested element. If you have listened for a <code>click</code> event on a <code>&lt;div&gt;</code> element, and the user actually clicks on a <code>&lt;p&gt;</code> element in the div, then the <code>&lt;p&gt;</code> element will become the event target. The fact that events “bubble” means that you are able to listen for clicks on the <code>&lt;div&gt;</code> (or any other ancestor node) and still receive a callback once the event passes through.</p>

### Bubbling Phase

After an event has fired on the target, it doesn’t stop there. It bubbles up (or propagates) through the DOM until it reaches the document’s root. This means that the same event is fired on the target’s parent node, followed by the parent’s parent, continuing until there is no parent to pass the event onto.

Think of the DOM as an onion and the event target as the core of the onion. In the capture phase, the event drills into the onion through each layer. When the event reaches the core, it fires (the target phase), and then reverses, working its way back up through each layer (the propagation phase). Once the event has returned to the surface, its journey is over.

Bubbling is useful. It frees us from listening for an event on the exact element it came from; instead, we listen on an element further up the DOM tree, waiting for the event to reach us. If events didn’t bubble, we would have to, in some cases, listen for an event on many different elements to ensure that it is caught.

<a class="demo-button" href="https://jsbin.com/unuhec/4/edit">Demo: Identifying event phases</a>

The majority of, but not all, events bubble. When events do not bubble, it is usually for a good reason. If in doubt, check <a href="https://www.w3.org/TR/DOM-Level-3-Events/#event-types">the specification</a>.</p>

## Stopping Propagation

Interrupting the path of the event at any point on its journey (i.e. in the capture or bubbling phase) is possible simply by calling the <code>stopPropagation</code> method on the event object. Then, the event will no longer call any listeners on nodes that it travels through on its way to the target and back to the document.

<pre><code class="language-javascript">
child.addEventListener('click', function(event) {
 event.stopPropagation();
});

parent.addEventListener('click', function(event) {
 // If the child element is clicked
 // this callback will not fire
});
</code></pre>

Calling <code>event.stopPropagation()</code> will not prevent any additional event listeners from being called on the current target if multiple listeners for the same event exist. If you wish to prevent any additional listeners from being called on the current node, you can use the more aggressive <code>event.stopImmediatePropagation()</code> method.

<pre><code class="language-javascript">
child.addEventListener('click', function(event) {
 event.stopImmediatePropagation();
});

child.addEventListener('click', function(event) {
 // If the child element is clicked
 // this callback will not fire
});
</code></pre>

<a class="demo-button" href="https://jsbin.com/aparot/3/edit?html,js,output">Demo: Stopping propagation</a>

## Prevent The Browser’s Default Behavior

The browser has default behaviors that will respond when certain events occur in the document. The most common event is a link being clicked. When a <code>click</code> event occurs on an <code>&lt;a&gt;</code> element, it will bubble up to the document level of the DOM, and the browser will interpret the <code>href</code> attribute and reload the window at the new address.

In Web applications, developers usually want to manage the navigation themselves, without causing the page to refresh. To do this, we need to prevent the browser’s default response to clicks and instead do our own thing. To do this, we call <code>event.preventDefault()</code>.

<pre><code class="language-javascript">
anchor.addEventListener('click', function(event) {
  event.preventDefault();
  // Do our own thing
});
</code></pre>

We can prevent many other default behaviors in the browser. For example, we could prevent presses of the space bar from scrolling the page in an HTML5 game, or we could prevent clicks from selecting text.

Calling <code>event.stopPropagation()</code> here will only prevent callbacks that are attached further down the propagation chain from being fired. It will not prevent the browser from doing its thing.

<a class="demo-button" href="https://jsbin.com/ibotap/1/edit">Demo: Preventing default behavior</a>

## Custom DOM Events

The browser is not the only thing that is able to trigger DOM events. We can create our own custom events and dispatch them on any element in the document. This type of event would behave just the same as a regular DOM event.

<pre><code class="language-javascript">
var myEvent = new CustomEvent("myevent", {
  detail: {
    name: "Wilson"
  },
  bubbles: true,
  cancelable: false
});

// Listen for 'myevent' on an element
myElement.addEventListener('myevent', function(event) {
  alert('Hello ' + event.detail.name);
});

// Trigger the 'myevent'
myElement.dispatchEvent(myEvent);
</code></pre>

Synthesizing “untrusted” DOM events on elements (for example, <code>click</code>) to simulate user interaction is also possible. This can be useful when testing DOM-related libraries. If you’re interested, the Mozilla Developer Network has a <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/DOM/Events/Creating_and_triggering_events#Triggering_built-in_events">write-up on it</a>.

Note the following:

*   The `CustomEvent` API is not available in IE 8 and below.
*   The [Flight](https://flightjs.github.io/) framework from Twitter makes use of custom events to communicate between modules. This enforces a highly decoupled, modular architecture.

<a class="demo-button" href="https://jsbin.com/emuhef/1/edit">Demo: Custom events</a>

## Delegate Event Listeners

Delegate event listeners are a more convenient and performant way to listen for events on a large number of DOM nodes using a single event listener. For example, if a list contains 100 items that all need to respond to a <code>click</code> event in a similar way, then we could query the DOM for all of the list items and attach an event listener to each one. This would result in 100 separate event listeners. Whenever a new item is added to the list, the <code>click</code> event listener would have to be added to it. Not only does this risk getting expensive, but it is tricky to maintain.

Delegate event listeners can make our lives a lot easier. Instead of listening for the <code>click</code> event on each element, we listen for it on the parent <code>&lt;ul&gt;</code> element. When an <code>&lt;li&gt;</code> is clicked, then the event bubbles up to the <code>&lt;ul&gt;</code>, triggering the callback. We can identify which <code>&lt;li&gt;</code> element has been clicked by inspecting the <code>event.target</code>. Below is a crude example to illustrate:

<pre><code class="language-javascript">
var list = document.querySelector('ul');

list.addEventListener('click', function(event) {
  var target = event.target;

  while (target.tagName !== 'LI') {
    target = target.parentNode;
    if (target === list) return;
  }

  // Do stuff here
});
</code></pre>

This is better because we have only the overhead of a single event listener, and we no longer have to worry about attaching a new event listener when an item is added to the list. The concept is pretty simple but super-useful.

I wouldn’t recommend using such a crude implementation in your app. Instead, use an event delegate JavaScript library, such as FT Lab’s <a title="ftdomdelegate" href="https://github.com/ftlabs/ftdomdelegate">ftdomdelegate</a>. If you’re using jQuery, you can seamlessly use event delegation by passing a selector as the second parameter to the <code>.on()</code> method.

<pre><code class="language-javascript">
// Not using event delegation
$('li').on('click', function(){});

// Using event delegation
$('ul').on('click', 'li', function(){});
</code></pre>

<a class="demo-button" title="Demo: Delegate event listeners" href="https://jsbin.com/isojul/1/edit">Demo: Delegate event listeners</a>

## Useful Events

### load

The <code>load</code> event fires on any resource that has finished loading (including any dependent resources). This could be an image, style sheet, script, video, audio file, document or window.

<pre><code class="language-javascript">
image.addEventListener('load', function(event) {
  image.classList.add('has-loaded');
});
</code></pre>

<a class="demo-button" href="https://jsbin.com/uhimir/1/edit">Demo: Image load event</a>

### onbeforeunload

<code>window.onbeforeunload</code> enables developers to ask the user to confirm that they want to leave the page. This can be useful in applications that require the user to save changes that would get lost if the browser’s tab were to be accidentally closed.

<pre><code class="language-javascript">
window.onbeforeunload = function() {
  if (textarea.value != textarea.defaultValue) {
    return 'Do you want to leave the page and discard changes?';
  }
};
</code></pre>

Note that assigning an <code>onbeforeunload</code> handler prevents the browser <a href="https://developer.mozilla.org/en-US/docs/Using_Firefox_1.5_caching">from caching the page</a>, thus making return visits a lot slower. Also, <code>onbeforeunload</code> handlers must be synchronous.

<a class="demo-button" href="https://jsbin.com/inelaj/2/edit">Demo: onbeforeunload</a>

### Stopping Window bounce in Mobile Safari

At the Financial Times, we use a simple <code>event.preventDefault</code> technique to prevent mobile Safari from bouncing the window when it is scrolled.

<pre><code class="language-javascript">
document.body.addEventListener('touchmove', function(event) {
 event.preventDefault();
});
</code></pre>

Be warned that this will also prevent any native scrolling from working ( such as <code>overflow: scroll</code>). To allow native scrolling on a subset of elements that need it, we listen for the same event on the scrollable element and set a flag on the event object. In the callback at the document level, we decide whether to prevent the default behavior of the touch event based on the existence of the <code>isScrollable</code> flag.

<pre><code class="language-javascript">
// Lower down in the DOM we set a flag
scrollableElement.addEventListener('touchmove', function(event) {
 event.isScrollable = true;
});

// Higher up the DOM we check for this flag to decide
// whether to let the browser handle the scroll
document.addEventListener('touchmove', function(event) {
 if (!event.isScrollable) event.preventDefault();
});
</code></pre>

Manipulating the event object is not possible in IE 8 and below. As a workaround, you can set properties on the <code>event.target</code> node.</p>

### resize

Listening to the resize event on the <code>window</code> object is super-useful for complex responsive layouts. Achieving a layout with CSS alone is not always possible. Sometimes JavaScript has to help us calculate and set the size of elements. When the window is resized or the device’s orientation changes, then we would likely need to readjust these sizes.

<pre><code class="language-javascript">
window.addEventListener('resize', function() {
  // update the layout
});
</code></pre>

I recommended using a <a href="https://davidwalsh.name/function-debounce">debounced</a> callback to normalize the callback rate and prevent extreme thrashing in the layout.

<a class="demo-button" href="https://jsbin.com/usevow/1/edit">Demo: Window resizing</a>

### transitionEnd

Today we use CSS to power the majority of transitions and animations in our applications. Sometimes, though, we still need to know when a particular animation has finished.

<pre><code class="language-javascript">
el.addEventListener('transitionEnd', function() {
 // Do stuff
});
</code></pre>

Note the following:

*   If you’re using `@keyframe` animations, use the `animationEnd` event name, instead of `transitionEnd`.
*   Like a lot of events, `transitionEnd` bubbles. Remember either to call `event.stopPropagation()` on any descendant transition events or to check the `event.target` to prevent callback logic from running when it’s not supposed to.
*   Event names are still widely vendor-prefixed (for example, `webkitTransitionEnd`, `msTransitionEnd`, etc). Use a library such as [Modernizr](https://modernizr.com/ "Modernizr") to get the event name’s correct prefix.

<a class="demo-button" href="https://jsbin.com/ijogok/1/edit">Demo: Transition end</a>

### animationiteration

The <code>animationiteration</code> event will fire every time a currently animating element completes an iteration. This is useful if we want to stop an animation but not midway through.

<pre><code class="language-javascript">
function start() {
  div.classList.add('spin');
}

function stop() {
  div.addEventListener('animationiteration', callback);

  function callback() {
    div.classList.remove('spin');
    div.removeEventListener('animationiteration', callback);
  }
}
</code></pre>

If you’re interested, I’ve <a href="https://wilsonpage.co.uk/animation-iteration-event">written about the <code>animationiteration</code> event</a> in a little more detail on my blog.

<a class="demo-button" href="https://jsbin.com/AwoYuxE/2">Demo: Animation iteration</a>

### error

If an error occurs when a resource loads, we might want to do something about it, especially if our users are on a flaky connection. The Financial Times uses this event to detect any images that might have failed to load in an article and instantly hide them. Because the “<a href="https://www.w3.org/TR/DOM-Level-3-Events/#event-type-error">DOM Level 3 Events</a>” specification has redefined the <code>error</code> event to “not bubble,” we can handle the event in one of two ways.

<pre><code class="language-javascript">
imageNode.addEventListener('error', function(event) {
  image.style.display = 'none';
});
</code></pre>

Unfortunately, <code>addEventListener</code> does not address all use cases. My colleague <a href="https://twitter.com/pornelski">Kornel</a> has kindly pointed me to an <a href="https://jsbin.com/esimAWA/2/quiet">example that demonstrates</a> that the only way, sadly, to guarantee the execution of image <code>error</code> event callbacks is to use (the often frowned upon) inline event handlers.

<pre><code class="language-markup">
&lt;img src="https://example.com/image.jpg" onerror="this.style.display='none';" /&gt;
</code></pre>

The reason for this is that you cannot be sure that the code that binds the <code>error</code> event handler will be executed before the <code>error</code> event actually happens. Using inline handlers means that when the markup is parsed and the image is requested, our <code>error</code> listeners will be attached.

<a class="demo-button" href="https://jsbin.com/ekulop/2/edit">Demo: Image error</a>

## Lessons From The Event Model

A lot can be learned from the success of the DOM events model. We can employ similar decoupled concepts in our own projects. Modules in an application can be as complex as they need to be, so long as that complexity is sealed away behind a simple interface. Many front-end frameworks (such as Backbone.js) are heavily event-based, solving cross-module communication in a publish and subscribe model that is very similar to the DOM.

<strong>Event-based architectures are great.</strong> They give us a simple common interface in which to write applications that respond to physical interactions across thousands of devices! Via events, devices tell us exactly what has happened and when it occurred, letting us respond however we please. What goes on behind the scenes is not of concern; we get a level of abstraction that frees us to get on with building our awesome app.</p>

### Further Reading

*   “[Document Object Model Level 3 Events Specification](https://www.w3.org/TR/DOM-Level-3-Events),” W3C
*   “[Graphical representation of an event dispatched in a DOM tree using the DOM event flow](https://www.w3.org/TR/DOM-Level-3-Events/#dom-event-architecture)” (image) W3C
*   “[Event](https://developer.mozilla.org/en/docs/Web/API/Event),” Mozilla Developer Network
*   “[DOM Design Tricks II](https://alistapart.com/article/domtricks2),” J. David Eisenberg, A List Apart
*   “[Event compatibility tables](https://www.quirksmode.org/dom/events/),” Quirksmode

<em>Special thanks to <a href="https://twitter.com/pornelski">Kornel</a> for a brilliant technical review.</em>

{{< signature "al, il" >}}


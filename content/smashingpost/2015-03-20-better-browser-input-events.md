---
title: 'Browser Input Events: Can We Do Better Than The Click?'
slug: better-browser-input-events
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa2ac3f2-8ebf-4ea8-8fc4-cc7b14c8f6bb/better-browser-input-events.png
date: 2015-03-20T22:01:41.000Z
author: dustankasten
description: >-
  Responding to user input is arguably the core of what we do as interface
  developers. In order to build responsive web products, understanding how
  touch, mouse, pointer and keyboard actions and the browser work together is
  key. You have likely experienced the 300-millisecond delay in mobile browsers
  or wrestled with touchmove versus scrolling.

  In this article we will introduce the event cascade and use this knowledge to
  implement a demo of a tap event that supports the many input methods while not
  breaking in proxy browsers such as Opera Mini.
categories:
  - Coding
  - Devices
  - Responsive Design
  - Interaction Design
---
Responding to user input is arguably the core of what we do as interface developers. In order to build responsive web products, understanding how touch, mouse, pointer and keyboard actions and the browser work together is key. You have likely experienced the <a href="https://ionicframework.com/blog/hybrid-apps-and-the-curse-of-the-300ms-delay/">300-millisecond delay</a> in mobile browsers or <a href="https://docs.google.com/document/d/12k_LL_Ot9GjF8zGWP9eI_3IMbSizD72susba0frg44Y/">wrestled with touchmove</a> <a href="https://updates.html5rocks.com/2014/05/A-More-Compatible-Smoother-Touch">versus scrolling</a>.

In this article we will introduce the event cascade and use this knowledge to implement a demo of a tap event that supports the many input methods while not breaking in proxy browsers such as Opera Mini.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2012/08/javascript-events-responding-user/#further-reading-on-smashingmag)

*   [The (Not So) Secret Powers Of The Mobile Browser](https://www.smashingmagazine.com/2016/12/the-not-so-secret-powers-of-the-mobile-browser/)
*   [Building A Simple Cross-Browser Offline To-Do List](https://www.smashingmagazine.com/2014/09/building-simple-cross-browser-offline-todo-list-indexeddb-websql/)
*   [<span class="headline">JavaScript Events And Responding To The User</span>](https://www.smashingmagazine.com/2012/08/javascript-events-responding-user/)
*   [The Seven Deadly Sins Of JavaScript Implementation](https://www.smashingmagazine.com/2010/02/the-seven-deadly-sins-of-javascript-implementation/)
*   [7 JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)

## Overview

Three primary input methods are used to interact with the web today: digital cursors (mouse), tactile (direct touch or stylus) and keyboards. We have access to these in JavaScript through <a href="https://www.w3.org/TR/touch-events/">touch events</a>, <a href="https://www.w3.org/TR/DOM-Level-2-Events/events.html#Events-eventgroupings-mouseevents">mouse events</a>, <a href="https://www.w3.org/TR/pointerevents/">pointer events</a> and <a href="https://www.w3.org/TR/2014/WD-DOM-Level-3-Events-20140925/#keys">keyboard events</a>. In this article we are primarily concerned with touch- and mouse-based interactions, although some events have standard keyboard-based interactions, such as the <code>click</code> and <code>submit</code> events.

{{% feature-panel %}}

You have very likely already been implementing event handlers for touch and mouse events. There was a time in our not too distant pass when the recommended method was something akin to this:

<pre><code class="language-javascript">
/** DO NOT EVER DO THIS! */
$('a', ('ontouchstart' in window) ? 'touchend' : 'click', handler);
</code></pre>

Microsoft has led the charge to create a better, future-facing event model with the “Pointer Events” specification. Pointer events are an abstract input mechanism that is now a W3C recommendation. Pointer events give the user agent (UA) flexibility to house numerous input mechanisms under one event system. Mouse, touch and stylus are all examples that easily come to mind today, although implementations extending to <a href="https://www.thalmic.com/en/myo/">Myo</a> or <a href="https://logbar.jp/ring/en/">Ring</a> are imaginable. While web developers seem to be really excited about this, not all browser engineers have felt the same. Namely, Apple and Google have decided not to implement pointer events at this time.

Google’s decision is not necessarily final, but there is no active work being done on pointer events. Our input and usage of pointer events through polyfills and alternative solutions will be part of the equation that could eventually tip the scale the other way. Apple made its statement against pointer events in 2012, and I am unaware of any more public response from Safari’s engineers.</p>

## The Event Cascade

When a user taps an element on a mobile device, the browser fires a slew of events. This action typically fires a series of events such as the following: <code>touchstart</code> → <code>touchend</code> → <code>mouseover</code> → <code>mousemove</code> → <code>mousedown</code> → <code>mouseup</code> → <code>click</code>.

This is due to backwards compatibility with the web. Pointer events take an alternative approach, firing compatibility events inline: <code>mousemove</code> → <code>pointerover</code> → <code>mouseover</code> → <code>pointerdown</code> → <code>mousedown</code> → <code>gotpointercapture</code> → <code>pointerup</code> → <code>mouseup</code> → <code>lostpointercapture</code> → <code>pointerout</code> → <code>mouseout</code> → <code>focus</code> → <code>click</code>.

The event specification allows for UAs to differ in their implementation of compatibility events. Patrick Lauke and Peter-Paul Koch maintain extensive reference material on this topic, which is linked to in the resources section at the bottom of this article.

The following graphics show the event cascade for the following actions:

1.  an initial tap on an element,
2.  a second tap on an element,
3.  tapping off the element.

Please note: This event stack intentionally ignores where <code>focus</code> and <code>blur</code> events fit into this stack.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97a6a7fb-edcf-4930-82a5-f9d922252699/01-ios-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/23612af5-d424-4d26-b3a6-e5cfa20c5287/01-ios-opt-small.png" alt="The event cascade on iOS devices for tapping on an element twice and then tapping away" /></a><figcaption>The event cascade on iOS devices for tapping on an element twice and then tapping away. (Image: <a href="https://dribbble.com/stephendavis">Stephen Davis</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/97a6a7fb-edcf-4930-82a5-f9d922252699/01-ios-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df88416f-d2ab-4ce7-82ea-6f2212995300/02-android-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/349568cc-d774-4df9-a115-30aee4f33b24/02-android-opt-small.png" alt="The event cascade on most Android 4.4 devices for tapping an element twice and then tapping away" /></a><figcaption>The event cascade on most Android 4.4 devices for tapping an element twice and then tapping away. (Image: <a href="https://dribbble.com/stephendavis">Stephen Davis</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/699f8803-758d-46bf-904f-98bf413f4e13/03-android-os-distribution-opt.png">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01406cc3-bfe6-4c74-ad04-78dd5073f945/03-pointer-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ee34c3b-893b-42c1-8dfc-1bc20d4f45db/03-pointer-opt-small.png" alt="The event cascade on IE 11 (before compatibility touch events were implemented) for tapping an element twice and then tapping away." /></a><figcaption>The event cascade on Internet Explorer 11 (before compatibility touch events were implemented) for tapping an element twice and then tapping away. (Image: <a href="https://dribbble.com/stephendavis">Stephen Davis</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/01406cc3-bfe6-4c74-ad04-78dd5073f945/03-pointer-opt.png">View large version</a>)</figcaption></figure>

### Applying the Event Cascade

Most websites built today for the desktop web “just work” because of the efforts of browser engineers. Despite the cascade looking gnarly, the conservative approach of building for mouse events as we previously have will generally work.

Of course, there is a catch. The infamous 300-millisecond delay is the most famous, but the interplay between scrolling, <code>touchmove</code> and <code>pointermove</code> events, and browser painting are additional issues. Avoiding the 300-millisecond delay is easy if:

*   we optimize only for modern Chrome for Android and desktop, which use heuristics such as `<meta name="viewport" content="width=device-width">` to disable the delay;
*   we optimize only for iOS, and the user does a clear press, but not a quick tap and not a long tap — just a good, normal, clear press of an element (oh, it also depends on whether it’s in a UIWebView or a WKWebView — read [FastClick’s issue on the topic](https://github.com/ftlabs/fastclick/issues/262#issuecomment-56363076) for a good cry).

If our goal is to build web products that compete with native platforms in user experience and polish, then we need to decrease interaction response latency. To accomplish this, we need to be building on the primitive events (<code>down</code>, <code>move</code> and <code>up</code>) and creating our own composite events (<code>click</code>, <code>double-click</code>). Of course, we still need to include fallback handlers for the native events for broad support and accessibility.

Doing this requires no small amount of code or knowledge. To avoid the 300-millisecond (or any length of) delay across browsers, we need to handle the full interaction lifecycle ourselves. For a given <code>{type}down</code> event, we will need to bind all events that will be necessary to complete that action. When the interaction is completed, we will then need to clean up after ourselves by unbinding all but the starting event.

You, the website developer, are the only one to know whether the page should zoom or has another double-tap event it must wait for. If — and only if — you require the callback to be delayed should you allow a delay for the intended action.

In the following link, you will find a small, dependency-free tap demo to illustrate the effort required to create a multi-input, low-latency tap event. Polymer-gestures is a production-ready implementation of the tap and other events. Despite its name, it is not tied to the Polymer library in any way and can easily be used in isolation.

To be clear, implementing this from scratch is a bad idea. The following is for educational purposes only and should not be used in production. Production-ready solutions exist, such as <a href="https://github.com/ftlabs/fastclick/">FastClick</a>, <a href="https://github.com/Polymer/polymer-gestures">polymer-gestures</a> and <a href="https://hammerjs.github.io/">Hammer.js</a>.

*   **Demo:** The tap event
*   **Code:** [taps.js](https://github.com/Skookum/smashing-input-events/blob/gh-pages/taps.js#L1)

### The Important Bits

Binding your initial event handlers is where it all begins. The following pattern is considered the bulletproof way to handle multi-device input.

<pre><code class="language-javascript">
/**
 * If there are pointer events, let the platform handle the input 
 * mechanism abstraction. If not, then it’s on you to handle 
 * between mouse and touch events.
 */

if (hasPointer) {
  tappable.addEventListener(POINTER_DOWN, tapStart, false);
  clickable.addEventListener(POINTER_DOWN, clickStart, false);
}

else {
  tappable.addEventListener('mousedown', tapStart, false);
  clickable.addEventListener('mousedown', clickStart, false);

  if (hasTouch) {
    tappable.addEventListener('touchstart', tapStart, false);
    clickable.addEventListener('touchstart', clickStart, false);
  }
}

clickable.addEventListener('click', clickEnd, false);
</code></pre>

Binding touch event handlers could compromise rendering performance, even if they don’t do anything. To decrease this impact, binding tracking events in the starting event’s handler is often recommended. Don’t forget to clean up after yourself and unbind the tracking events in your action-completed handlers.

<pre><code class="language-javascript">
/**
 * On tapStart we want to bind our move and end events to detect 
 * whether this is a “tap” action.
 * @param {Event} event the browser event object
 */

function tapStart(event) {
  // bind tracking events. “bindEventsFor” is a helper that automatically 
  // binds the appropriate pointer, touch or mouse events based on our 
  // current event type. Additionally, it saves the event target to give 
  // us similar behavior to pointer events’ “setPointerCapture” method.

  bindEventsFor(event.type, event.target);
  if (typeof event.setPointerCapture === 'function') {
    event.currentTarget.setPointerCapture(event.pointerId);
  }

  // prevent the cascade
  event.preventDefault();

  // start our profiler to track time between events
  set(event, 'tapStart', Date.now());
}

/**
 * tapEnd. Our work here is done. Let’s clean up our tracking events.
 * @param {Element} target the html element
 * @param {Event} event the browser event object
 */

function tapEnd(target, event) {
  unbindEventsFor(event.type, target);
  var _id = idFor(event);
  log('Tap', diff(get(_id, 'tapStart'), Date.now()));
  setTimeout(function() {
    delete events[_id];
  });
}</code></pre>

The rest of the code should be pretty self-explanatory. In truth, it’s a lot of bookkeeping. Implementing custom gestures requires you to work closely with the browser event system. To save yourself the pain and heartache, don’t do this à la carte throughout your code base; rather, build or use a strong abstraction, such as <a href="https://hammerjs.github.io/">Hammer.js</a>, the <a href="https://github.com/jquery/PEP">Pointer Events</a> jQuery polyfill or polymer-gestures.

## Conclusion

Certain events that used to be very clear are now filled with ambiguity. The <code>click</code> event used to mean one thing and one thing only, but touchscreens have complicated it by needing to discern whether the action is a double-click, scroll, event or some other OS-level gesture.

The good news is that we now understand much better the event cascade and the interplay between a user’s action and the browser’s response. By understanding the primitives at work, we are able to make better decisions in our projects, for our users and for the future of the web.

What unexpected problems have you run into when building multi-device websites? What approaches have you taken to solve for the numerous interaction models we have on the web?

### Additional Resources

*   “[Pointer Events Finalized, But Apple’s Lack of Support Still a Deal Breaker](https://arstechnica.com/information-technology/2015/02/pointer-events-finalized-but-apples-lack-of-support-still-a-deal-breaker/),” Peter Bright
*   “Getting Touchy: An Introduction to Touch and Pointer Events,” including [slides](https://patrickhlauke.github.io/getting-touchy-presentation/) and [talk](https://www.youtube.com/watch?v=QYLC8o3U_XY), Patrick E. Lauke
*   “[Apple's Web?](https://timkadlec.com/2015/02/apples-web/)” by Tim Kadlec
*   “[Avoiding the 300ms Click Delay, Accessibly](https://timkadlec.com/2013/11/Avoiding-the-300ms-click-delay-accessibly/),” Tim Kadlec
*   “[Touch Table](https://www.quirksmode.org/mobile/tableTouch.html),” Peter-Paul Koch
*   “[Making the Web ‘Just Work’ With Any Input: Mouse, Touch, and Pointer Events](https://blogs.msdn.com/b/ie/archive/2014/09/05/making-the-web-just-work-with-any-input.aspx),” Jacob Rossi
*   [FastClick](https://github.com/ftlabs/fastclick) library
*   [Hammer.js](https://hammerjs.github.io/)
*   [polymer-gestures](https://github.com/Polymer/polymer-gestures)
*   [PointerEvents](https://github.com/jquery/PEP) jQuery polyfill
*   “Implement Custom Gestures,” Google Developers

{{< signature "da, al, ml" >}}


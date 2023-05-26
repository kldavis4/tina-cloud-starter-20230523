---
title: 'CSS3 Transitions: Thank God We Have A Specification!'
slug: css3-transitions-thank-god-specification
image: null
date: 2013-04-26T07:56:30.000Z
author: rodney-rehm
description: >-
  This article is packed with a number of quirks and issues you should be aware
  of when working with CSS3 transitions. Please note that I’m not showing any
  workarounds or giving advice on how to circumvent the issues discussed.
categories:
  - Coding
  - CSS
  - Techniques
  - CSS3
---
This article is packed with a number of quirks and issues you should be aware of when working with CSS3 transitions. Please note that I’m not showing any workarounds or giving advice on how to circumvent the issues discussed. Alex MacCaw has already written a very insightful and thorough article on “<a href="https://blog.alexmaccaw.com/css-transitions">All You Need to Know About CSS Transitions</a>.”

Whereas Alex wrote about achieving particular effects, I’m going to talk about the technical background, especially the JavaScript-facing side. Pitfalls — <strong>this article is all about pitfalls</strong>. Here is the table of contents if you would like to skip to a specific section:

*   [Specifying A Transition](#a1)
*   [When A Transition Is Complete](#a2)
*   [Transitionable Properties](#a3)
*   [Priority Of Transition Properties](#a4)
*   [Transitioning From And To `auto`](#a5)
*   [Implicit Transitions](#a6)
*   [Transitions And Pseudo-Elements](#a7)
*   [Background Tabs](#a8)
*   ["Invisible" Elements](#a9)
*   [Transitioning Before The DOM Is Ready](#a10)
*   [Rendering Quirks](#a11)
*   [Recommendations For The Specification](#a12)
*   [Use The `delay`, Luke!](#a13)
*   [Conclusion](#a14)

Separation of concerns is nothing new — we’ve been using template engines for years to accomplish exactly that, separating our HTML from whatever scripting language we were using. <strong>A website has three major concerns:</strong> structure (HTML), layout and style (CSS), and behavior (JavaScript). CSS crossed the line and became behavioral quite a while ago, but that’s a whole different discussion.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Improving User Flow Through Page Transitions](https://www.smashingmagazine.com/2016/07/improving-user-flow-through-page-transitions/)
*   [Let’s Play With Hardware-Accelerated CSS](https://www.smashingmagazine.com/2012/06/play-with-hardware-accelerated-css/)
*   [Understanding CSS Timing Functions](https://www.smashingmagazine.com/2014/04/understanding-css-timing-functions/)
*   [Why Transitions Are Important](https://www.smashingmagazine.com/2012/02/mission-transition/)

{{% feature-panel %}}

A couple of weeks ago, I was tasked with developing a JavaScript module that would allow for the use of CSS transitions in a way that the JavaScript side would know nothing about the transitions taking place. <strong>The actual problem is the asynchronousity of transitions.</strong> After writing a bunch of tests, I gave up on the task. It cannot be done with a reasonable amount of code and initialization time. My test results are what this article is all about.

Before getting started with transitions, we have to talk about a little, frequently used, helper function. <a href="https://developer.mozilla.org/en-US/docs/DOM/window.getComputedStyle"><code>getComputedStyle()</code></a> is a JavaScript method that returns a CSS property’s value as the browser interprets it. This API goes back to “<a href="https://www.w3.org/TR/DOM-Level-2-Style/css.html#CSS-CSSview-getComputedStyle">DOM Level 2: getComputedStyle()</a>” and “<a href="https://www.w3.org/TR/1998/REC-CSS2-19980512/cascade.html#computed-value">CSS Level 2: Computed Values</a>” — which basically specify that a computed style is an absolute value.

This is fine for properties such as <a href="https://developer.mozilla.org/en-US/docs/CSS/font-size"><code>font-size</code></a>, which take only one argument and are reliably converted to pixel values. However, it doesn’t cover how browsers should handle shorthand properties, such as <a href="https://developer.mozilla.org/en-US/docs/CSS/margin"><code>margin</code></a> — some browsers return nothing, others something semi-useful. Then there are properties with different but equivalent values to consider, such as <a href="https://developer.mozilla.org/en-US/docs/CSS/font-weight"><code>font-weight</code></a>’s <code>bold</code> and <code>700</code>. WebKit also has <a href="https://bugs.webkit.org/show_bug.cgi?id=106535">a bug</a> that extracts the computed value of properties from pseudo-elements.

<em>The quirks described here were identified in January 2013 using Firefox 18 (Gecko), Opera 12.12 (Presto), Internet Explorer 10 (Trident), Safari 6.0.2 (WebKit), Chrome 23 (WebKit), as well as Gecko’s and WebKit’s nightly build channels.</em>

Without further ado, <strong>let’s dive into the specifications and implementations</strong>, a world riddled with misconceptions. Please note that in order to be concise, I’ve omitted vendor prefixes from the examples.
<blockquote>"Not knowing is difficult to handle. It’s easier to assume."

– Dr. Axel Rauschmayer</blockquote>

… But assumptions are often wrong. I discovered the information in this article by creating a <a href="https://test.csswg.org/shepherd/search/spec/CSS3-TRANSITIONS/">CSS3 Transitions Test Suite</a>.</p>

## <a id="a1"></a>1\. Specifying A Transition

Besides the shorthand <a href="https://www.w3.org/TR/css3-transitions/#transition-property-property"><code>transition</code> property</a>, the CSS3 transition specification defines the following four CSS properties for specifying an animated change of state:

*   `transition-property`,
*   `transition-duration`,
*   `transition-delay`,
*   `transition-timing-function`.</p>

### CSS Properties to Transition

The <a href="https://www.w3.org/TR/css3-transitions/#transition-property-property"><code>transition-property</code> property</a> defines the <strong>property (or properties) to animate</strong>. The default is <code>all</code>, meaning that all properties a browser can transition will be animated on change (if there’s a <code>transition-duration</code> greater than <code>0s</code>). The property accepts one value or a list of comma-separated values (like all other <code>transition-*</code> properties).

The specification states that a browser should accept and preserve any property it doesn’t recognize. So, the following example would still run a transition on <code>padding</code> lasting 2 seconds:

<pre><code class="language-css">
transition-property: foobar, padding;
transition-duration: 1s, 2s;
</code></pre>

Contrary to the specification, WebKit parses the above to <code>transition-property: all</code>. Firefox and Opera parse it to <code>transition-property: all, padding</code>.</p>

### Duration of a Transition

The <a href="https://www.w3.org/TR/css3-transitions/#transition-duration-property"><code>transition-duration</code> property</a> defines the <strong>amount of time</strong> a transition should take to get from the initial state to the target state. It accepts a <a href="https://www.w3.org/TR/css3-values/#time"><code>&lt;time&gt;</code></a> value in seconds or milliseconds (for example, <code>2.3s</code> and <code>2300ms</code> both specify 2.3 seconds).

While the specification makes it clear that values must be a positive number, Opera also accepts <code>-5s</code> — at least for <code>getComputedStyle()</code>. Opera and Internet Explorer (IE) do not accept values lower than <code>10ms</code>, although the specification mentions no such limitation. In all fairness, you wouldn’t notice a transition lasting 9 milliseconds anyways. WebKit (except for the current WebKit nightly) has a bug in its <code>getComputedStyle()</code> implementation, returning values such as <code>0.009999999776482582s</code> instead of <code>0.01s</code>. At least all browsers agree on returning second-based values.</p>

### Delay of a Transition

The <a href="https://www.w3.org/TR/css3-transitions/#transition-delay-property"><code>transition-delay</code> property</a> defines the <strong>time to wait</strong> before executing a transition, also using <code>&lt;time&gt;</code> values. The <code>delay</code> may be a negative value, which will start the transition immediately and make it appear as though the transition had started at the given offset in time — essentially starting with a jump.

As with <code>transition-duration</code>, IE and Opera don’t accept values between <code>-10ms</code> and <code>10ms</code>. WebKit’s floating point issues appear here, too.</p>

### Timing Functions

The <a href="https://www.w3.org/TR/css3-transitions/#transition-timing-function-property"><code>transition-timing-function</code> property</a> defines the <strong>mathematical function used to calculate a property’s value</strong> at time <code>t</code>. There are three basic types: <code>cubic-bezier(x1, y1, x2, y2)</code>, <code>step(&lt;number&gt;, start|end)</code>, and keywords that map to predefined cubic bezier curves. Most likely, you already know the keywords <code>linear</code>, <code>ease</code>, <code>ease-in</code>, <code>ease-out</code> and <code>ease-in-out</code>. The math behind cubic beziers gets ridiculously unimportant when using <a href="https://twitter.com/LeaVerou">Lea Verou</a>’s charming little <a href="https://cubic-bezier.com/#.17,.67,.83,.67">Cubic Bezier Editor</a>. While cubic bezier curves make smooth transitions, the <code>step()</code> functions don’t. They instead jump to the next value (i.e. the next step) at a regular interval. This allows for frame-by-frame animations; see “<a href="https://lea.verou.me/2011/09/pure-css3-typing-animation-with-steps/">Pure CSS3 Typing Animation With steps()</a>” for an example.

The computed value of <code>linear</code> is usually represented as <code>cubic-bezier(0, 0, 1, 1)</code> — except for WebKit, which actually returns <code>linear</code>. But not to worry: WebKit will still return <code>cubic-bezier(0.25, 0.1, 0.25, 1)</code> instead of <code>ease</code>. The current WebKit nightly returns the keyword for all defined keywords, though. Looking on the bright side, in a couple of months WebKit won’t be inconsistent with itself — only with the rest of the browser world.

The specification stipulates that the <code>x</code> values must be between <code>0</code> and <code>1</code>, while the <code>y</code> values may exceed that range. Contrary to the specification, WebKit allows <code>x</code> to exceed the bounds, at least computationally. At the time of writing, the Android browser (version 4.0) mixes up ranges for <code>x</code> and <code>y</code>, essentially disallowing “bounce” effects.

## 2\. When A Transition Is Complete

I already mentioned that CSS transitions run asynchronously. The specification provides the <code>TransitionEnd</code> event to allow JavaScript to synchronize with the end of a transition. Sadly, the specification isn’t very specific about this event. In fact, it simply states that an event is to be fired for every property that has undergone a transition. If you need a single word to describe the situation, “nightmare” isn’t far off.

While the specification says that shorthand properties (such as <code>padding</code>) should run transitions for all properties that it covers (<code>padding-top</code>, <code>padding-right</code>, etc.), it doesn’t say which property should be named in a <code>TransitionEnd</code> event. While Gecko, Trident and Presto agree on triggering events for the longhand sub-properties (such as <code>padding-top</code>), even if a transition was defined for a shorthand property (such as <code>padding</code>), <strong>WebKit would take the opportunity to screw things up.</strong> WebKit would trigger an event for <code>padding</code> if (and only if) you specified <code>transition-property: padding</code>, but <code>transition-property: all</code> would trigger the event for <code>padding-left</code> et al. For some reason, iPhone 6.0.1’s Safari browser <em>might</em> also triggers events for <code>font-size</code> and <code>line-height</code> when <code>padding</code> is being transitioned. Confused yet?

<pre><code class="language-css">
.example {
  padding: 1px;
  transition-property: padding;
  transition-duration: 1s;
}

.example:hover {
  padding: 10px;
}
</code></pre>

The above CSS will trigger different <code>TransitionEnd</code> events across browsers:
<dl>
 	<dt>Gecko, Trident, Presto</dt>
 	<dd><code>padding-top</code>, <code>padding-right</code>, <code>padding-bottom</code>, <code>padding-left</code></dd>
 	<dt>WebKit</dt>
 	<dd><code>padding</code></dd>
</dl>

<pre><code class="language-css">
.example {
  padding: 1px;
  transition-property: all, padding;
  transition-duration: 1s;
}

.example:hover {
  padding: 10px;
}
</code></pre>

The CSS above will trigger different <code>TransitionEnd</code> events across browsers:
<dl>
 	<dt>Gecko, Trident, Presto, WebKit</dt>
 	<dd><code>padding-top</code>, <code>padding-right</code>, <code>padding-bottom</code>, <code>padding-left</code></dd>
 	<dt>Safari 6.0.1 on iPhone (not iPad, mind you!)</dt>
 	<dd><code>padding-top</code>, <code>padding-right</code>, <code>padding-bottom</code>, <code>padding-left</code>, <code>font-size</code>, <code>line-height</code></dd>
</dl>
I said that you could specify a negative <code>transition-delay</code> to “jumpstart” your transition. But what happens for <code>transition-duration: 1s; transition-delay: -1s;</code>? Gecko and WebKit immediately jump to the target value and trigger an event. Trident and Presto won’t trigger any events.

<strong>That floating point issue that WebKit experiences</strong> in <code>getComputedStyle()</code> is also present in <code>TransitionEnd.elapsedTime</code> — consistently in all browsers. <code>Math.round(event.elapsedTime * 1000) / 1000</code> will “fix” that for you.

WebKit and IE have implemented an <a href="https://snook.ca/archives/html_and_css/background-position-x-y">unspecified extension to <code>background-position</code></a> that causes them to trigger <code>TransitionEnd</code> events for <code>background-position-x</code> and <code>background-position-y</code>, instead of <code>background-position</code>.

So, even if you <em>knew</em> that a transition was taking place, you wouldn’t be able to rely on the <code>TransitionEnd.propertyName</code> that you’re given. While you <em>could</em> write loads of JavaScript to equalize the behavior, you wouldn’t be able to do this in a future-proof way without doing proper feature detection for every single property. And this could include properties you might not even know are animatable.</p>

## 3\. Transitionable Properties

The specification <a href="https://www.w3.org/TR/css3-transitions/#animatable-css">lists a number of CSS properties</a> that a browser is supposed to support animated transition for. This list contains properties of CSS2.1. Any of the newer properties will be marked as animatable in their respective specifications — as <a href="https://www.w3.org/TR/css3-flexbox/#order-property"><code>order</code> of the Flexible Box Layout</a> shows.

The property’s value type is an important factor. The property <code>margin-top</code> accepts <code>&lt;length&gt;</code> and <code>&lt;percentage&gt;</code> values, but according to the list of transitionable CSS properties, only <code>&lt;length&gt;</code> is to be animated. But that didn’t keep browser vendors from implementing transitions for <code>&lt;percentage&gt;</code> values anyway. The <code>word-spacing</code> property is a different story, though. The specification includes <code>&lt;percentage&gt;</code> values, but at the time of writing, no browser is able to animate that.

Ignoring the (inherently unreliable) <code>TransitionEnd</code> events, a property is transitioned from value A to value B if its <code>getComputedStyle()</code> value is different from A and B at a given time during the transition. Because there is no such thing as a “CSS property value changed” event, <strong>you’re left with polling the DOM</strong>. <a href="https://developer.mozilla.org/en-US/docs/DOM/window.setTimeout"><code>setTimeout()</code></a>’s resolution is not good enough to do this for fast transitions (a duration of less than a few hundred milliseconds). <a href="https://developer.mozilla.org/en-US/docs/DOM/window.requestAnimationFrame"><code>requestAnimationFrame()</code></a> is your friend for this. The browser will call you before it repaints to screen, allowing you to grab a couple of intermediate values during transitions. Except for Opera, all engines have this feature already.

Instead of bloating this article with a full compatibility table, I’ve sent my results to Oli Studholme (<a href="https://twitter.com/boblet">@boblet</a>), who has updated his list of “<a href="https://oli.jp/2010/css-animatable-properties/">CSS Animatable Properties</a>” accordingly.</p>

## 4\. Priority Of Transition Properties

The specification on the <a href="https://www.w3.org/TR/css3-transitions/#transition-property-property"><code>transition-property</code> property</a> states that we’re allowed to define a property multiple times:
<blockquote>"If a property is specified multiple times in the value of ‘transition-property’ (either on its own, via a shorthand that contains it, or via the ‘all’ value), then the transition that starts uses the duration, delay, and timing function at the index corresponding to the last item in the value of ‘transition-property’ that calls for animating that property."</blockquote>

So, we can make <code>padding</code> transition for 1 second, while making <code>padding-left</code> take 2 seconds; or define a default transition style using <code>transition-property: all</code> and overwrite that for particular properties.

In Firefox and IE, this works fine. Opera mixes up the priority order, though. Instead of simply using the <em>last</em> applicable property in the list, it treats <code>padding-left</code> as more specific than <code>padding</code> and <code>all</code>.

The real problem is WebKit. It’s somehow managed to execute a transition multiple times if a property is specified multiple times. To really freak out WebKit, try running a transition for <code>transition-property: padding, padding-left</code> with the very small <code>transition-duration: 0.1s</code> (warning: this is not a good idea for epileptics). WebKit will <em>render</em> the transition at least twice. But the real beauty is the <code>TransitionEnd</code> events, of which you could receive up to <em>hundreds</em> for a single transition.</p>

## 5\. Transitioning From And To `auto`

The CSS property value <code>auto</code> translates to “Dear browser, please calculate some reasonable value for this.” Paragraphs (<code>&lt;p&gt;</code>) and any block-level elements will be as wide as their parent if they have <code>width: auto</code>. There are times when you’ll change from <code>width: auto</code> to a specific width — and want to transition that change. The specification neither enforces nor denies the use of <code>auto</code> values for transitionable properties.

Firefox, IE and Opera cannot transition from or to <code>auto</code> values. IE makes a little exception for <code>z-index</code>, but that’s it. WebKit, on the other hand, is capable of transitioning from and to pretty much any CSS property that accepts the <code>auto</code> value. WebKit doesn’t like <code>clip</code> too much; for that property, it will only trigger a <code>TransitionEnd</code> event, without generating or showing any intermediate values or states during the transition.

For the other properties, such as <code>width</code> and <code>height</code>, WebKit’s behavior is not quite what you’d expect. If <code>width: auto</code> translated to a calculated width of <code>300px</code> and you transitioned that to <code>100px</code>, then your transition would not shrink from 300 to 100 pixels. Instead, it would grow from 0 to 100 pixels.

For a full compatibility table, have a look at “<a href="https://oli.jp/2010/css-animatable-properties/">CSS Animatable Properties</a>.”

## 6\. Implicit Transitions

An “implicit transition” happens when a change to one property causes another property to be transitioned — or if you change a property on a parent element and cause a child to transition either the inherited property or a dependent property. Confused? Consider <code>font-size: 18px; padding: 2em;</code> — the padding is calculated as <code>2 × font-size</code>, because that’s what em does, giving us 36 pixels.

There are various <strong>relative value types</strong>: <code>&lt;percentage&gt;</code>, <code>&lt;length&gt;</code>, <code>em</code>, <code>rem</code>, <code>vh</code>, <code>vw</code>, etc. Using a relative value, such as <code>padding: 2em</code>, makes the browser recalculate the property’s <code>getComputedValue()</code> every time its depending value (such as <code>font-size</code>) changes. That in turn triggers a transition for <code>padding</code> because the computed style has changed. This transition is considered to be “implicit” because the <code>padding</code> property was not modified explicitly.

Most browsers run these implicit transitions. The exception is IE 10, which runs them only for the <code>line-height</code> property. WebKit runs implicit transitions for all applicable properties except <code>vertical-align</code>. Besides font-relative property values, there are width-relative property values (usually <code>&lt;percentage&gt;</code>), viewport-relative property values (such as <code>vh</code> and <code>vw</code>), default initial values (such as <code>column-gap: 1em</code> in Opera), and then <a href="https://developer.mozilla.org/en-US/docs/CSS/color_value#currentColor_keyword"><code>currentColor</code></a>. All of these might — or might not — trigger implicit transitions.

In Firefox, these implicit transitions get particularly interesting when both the depending and the dependent properties are transitioned but their <code>transition-duration</code> or <code>transition-delay</code> do not match. While WebKit and Opera produce transitions that make sense visually, Firefox garbles things a bit. In IE, this is a non-issue because it doesn’t do implicit transitions.

Don’t forget about inheritance within the cascade. A <code>font-size</code> on a DOM element will be inherited by its children, as long as it’s not overwritten, potentially causing implicit transitions.</p>

## id="a7">7\. Transitions And Pseudo-Elements

Pseudo-elements (<code>:before</code> and <code>:after</code>) were introduced with <a href="https://www.w3.org/TR/CSS2/generate.html">CSS2 generated content</a>. Read “<a href="https://www.smashingmagazine.com/2011/07/13/learning-to-use-the-before-and-after-pseudo-elements-in-css/">Learning to Use the :before and :after Pseudo-Elements in CSS</a>” if you’re not yet familiar with generated content. While <a href="https://www.w3.org/TR/css3-content/">CSS3 content</a> defines additional pseudo-elements (<code>::alternate</code>, <code>::outside</code>), they are not (yet) supported. All animatable CSS properties should also be animatable for pseudo-elements.

Firefox and IE 10 will transition properties on pseudo-elements. Opera, Chrome and Safari will not. WebKit added support in January 2013 — which you can already check out in <a href="https://nightly.webkit.org/">WebKit nightly</a> and <a href="https://www.google.com/intl/en/chrome/browser/canary.html">Chrome Canary</a>.

Transitions of generated content bring their own set of funky issues. <code>TransitionEnd</code> events aren’t fired at all. At some point in the future, they’re supposed to be triggered on the owner element and provide their pseudo-element through <code>TransitionEnd.pseudoElement</code>. But even the “<a href="https://dev.w3.org/csswg/css3-transitions/#transition-events">Transition Events</a>” section of the “CSS Transitions” editor’s draft doesn’t specify that properly yet.

There was a time when we would change the value of the <code>content</code> property so that IE 8 would re-render that element in certain circumstances (like when entering a <code>:hover</code> state). It turns out that this fix for old IE interferes with this ability for all other browsers. So, when trying to transition a property on a pseudo-element, make sure the <code>content</code> is not changed.

IE 10 will not run a transition for a pseudo-element’s <code>:hover</code> state if the owner element doesn’t have a <code>:hover</code> state as well:

<pre><code class="language-css">
.some-selector:before {
  content: "hello";
  color: red;
  transition: all 1s linear 0s;
}

.some-selector:hover:before {
  color: green;
}
/* This next rule is necessary for IE 10 to transition :before on hover */
.some-selector:hover {}
</code></pre>

The weird thing about this issue isn’t that you need a (possibly empty) <code>:hover</code> state on the owner element. It’s that if you don’t have one, IE 10 will interpret the <code>:hover</code> as <code>:active</code> (i.e. active when you mousedown on the element). The even weirder part is that the <code>:active</code> state persists even after <code>mouseup</code> and is removed only by another click on the document.</p>

## 8\. Background Tabs

At the time of writing, IE 10 is the only browser that responds to a tab being in the background or foreground. While it will finish a running transition if the tab is pushed to the background, it won’t start any new transitions there. IE 10 will wait until the tab is pulled into the foreground before starting any new transitions. Fortunately, IE 10 already supports the <a href="https://www.w3.org/TR/page-visibility/">Page Visibility API</a>, allowing developers to respond to this behavior.

We can expect similar things to happen with other browsers as they continue putting background tabs to sleep.</p>

## 9\. “Invisible” Elements

So, are transitions executed for DOM elements that are not attached to the DOM? Nope, not a single browser does that — why should they? Well, then, what about hidden elements? Most browsers have figured out that there’s no need to run a transition on an invisible (i.e. not painted) element. Opera thinks differently about this — it’ll run a transition regardless of whether it is painted or not.</p>

## 10\. Transitioning Before The DOM Is Ready?

The <code>DOMContentLoaded</code> event is triggered when the document leaves parsing mode. If you’re into jQuery, we’re talking about <a href="https://api.jquery.com/ready/"><code>jQuery.ready()</code></a> right now. Transitions can be run <em>before</em> this event happens.</p>

## 11\. Rendering Quirks

The issues I’ve described up to this point were found by testing against the specification. The tests were run automatically. But as it turns out, quite a few more problems are visible to the eye. The following quirks have been found by various other developers and could affect your meddling with transitions just as much.

At this time, transitioning a background from gradient to gradient is not possible. Transitioning from gradient to solid color is possible — with a big caveat. If a gradient is in play, then the color transition will happen from white to the target color, appearing to quickly flash white at the beginning of the transition. This can be <a href="https://jsbin.com/oyuciz/1/">observed</a> in all current browsers.

Firefox seems to be using a different algorithm for rendering (or smoothing) images as they’re being animated (<a href="https://jsfiddle.net/fSjUb/3/">see an example</a>). Apparently, Gecko sacrifies quality for performance during animation. Note that this occurs if a <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=860261">low enough <code>transform: scale()</code> is in play</a>.

Firefox won’t properly animate from <code>a:visited</code> to <code>a:hover</code> or vice versa. Instead, it will jump from <code>a:visited</code> to <code>a:link</code> and then transition to <code>a:hover</code>, as you can see <a href="https://jsbin.com/avabaw/1">in this example</a>. This is mentioned somewhat in “<a href="https://developer.mozilla.org/en-US/docs/CSS/Privacy_and_the_:visited_selector">Privacy and the :visited Selector</a>” on the Mozilla Developer Network. While IE 10 agrees with Chrome, Safari and Opera on the proper transition, it also runs the transition from <code>a:link</code> to <code>a:visited</code> on page load.

Transitioning multiple properties is not synchronized in Firefox and Webkit. You can <a href="https://jsbin.com/uxenaz/1">see in this example</a> how making the <code>border</code> smaller by the same amount that the <code>padding</code> increases (and vice versa) causes the following content to shake a bit. IE 10 and Opera get this right.

Firefox won’t animate an element’s properties if one of its parent’s <code>position</code> is changed, <a href="https://jsbin.com/azipul/1">as you can see</a>. Webkit, Opera and IE 10 behave correctly.</p>

## 12\. Recommendations For The Specification

Having read the specification from top to bottom and actually tested all of the features, I think a few changes would help:

*   Introduce a `TransitionsEnd` (notice the plural), triggered once _all_ transitions for an element have completed. It could provide a list of properties that have been animated — but I don’t see the use case for knowing _what_ has transitioned, as long as I’m informed _when_ all animations are done.
*   Introduce a `TransitionStart` event, triggered for every property about to be transitioned. Because DOM events don’t come cheap and the JavaScript event loop and the rendering thread are not necessarily blocking each other, a single event `TransitionsStart` (there is that plural again) might be the better solution. I don’t see why I should be able to `cancel` the event, so this would be a “fire and forget” kind of thing.
*   Make it clear what `TransitionEnd` is supposed to be triggered for. That `padding` versus `padding-left` issue in WebKit is rather annoying.
*   Clearly specify how “implicit transitions,” such as `line-height: 1em` for `transition-property: font-size`, are to be handled.
*   Add a `::transitioning` pseudo-class that allows you to define `pointer-events: none` to prevent accidental hover states (among other things). The trick here is to prevent the application of styles that themselves would trigger a new transition or that would alter an already running transition.

In addition to these suggestions, we should be able to accomplish a number of common (simple) things without having to throw a lot of JavaScript at the problem:

*   Every once in a while, you’ll want to completely mute all transitions — for example, because you’re changing the layout and need to calculate dimensions and positions before unleashing your beautiful transitions upon the visitor.
*   Sometimes you’ll want to remove an object from the DOM and want that to be animated. Right now, you’d add a class, wait for the `TransitionEnd` event and then remove the element.
*   Just as with removing things, you’ll want to add a new element and animate its appearance. Right now, you have to insert the element, set some “invisible style,” force a repaint and then revert to the new element’s actual style.
*   Reordering, hiding and showing elements are common for any Web application. Giving that task a little style currently requires us to run utilities such as [Isotope](https://isotope.metafizzy.co/). A vanilla CSS solution could shave off some bytes.</p>

## 13\. Use The `delay`, Luke!

Imagine a number of elements packed together tightly. Imagine that the styles of those elements change on hover. Imagine moving your cursor (moderately quickly) over that group. What happens? Exactly: you’ll see the <a href="https://jsbin.com/irazox/1">styles of those elements flash</a>.

By adding a relatively short delay to your transitions, you can <a href="https://jsbin.com/egeniz/1/">mitigate that effect</a>; 20 milliseconds is undetectable to the human eye, but it’s enough for the mouse cursor to pass over small elements. The transitions won’t appear to lag because of this, and the visual distraction you might have caused just disappears. Simple trick, I know.</p>

## 14\. Conclusion

*   Be very careful when using `transition-property: all`. You _will_ get `TransitionEnd` events for properties that you didn’t expect to ever transition.
*   Be careful when using shorthand properties, because the number of triggered events varies between browsers.
*   Opera and IE don’t trigger events when a negative delay cancels out the duration.
*   WebKit has real issues with the priority of properties such as `transition-property: margin, margin-left`. Avoid this for now.
*   IE doesn’t support implicit transitions — for example, triggered for `padding: 2em` when `font-size` changes.
*   Firefox and Opera cannot parse `transition-property: all, width`.
*   Opera mixes up the priority of properties.
*   Transitions on pseudo-elements do not trigger `TransitionEnd` events.
*   IE 10 has a weird `:hover` bug when transitioning pseudo-elements.
*   The specification leaves a lot of room for improvement.</p>

### Related Content

If you’re interested in transitions and animations — and how to use them wisely — have a look at these fantastic resources:

*   “[Dynamic Visual Effects With CSS3 Transitions](https://docs.webplatform.org/wiki/tutorials/css_transitions),” Mike Sierra, Web Platform Docs
*   “[All You Need to Know About CSS Transitions](https://blog.alexmaccaw.com/css-transitions),” Alex MacCaw
*   [Meaningful Transitions](https://www.ui-transitions.com/)
*   “[Transitional Interfaces](https://medium.com/design-ux/926eb80d64e3),” Pasquale D’Silva
*   [Animatable](https://github.com/LeaVerou/animatable) (showcase of transitions), Lea Verou
*   “[CSS Animatable Properties](https://oli.jp/2010/css-animatable-properties/),” Oli Studholme

<em>Thanks go to <a href="https://oli.jp/">Oli Studholme</a> and <a href="https://lea.verou.me/">Lea Verou</a> for taking the time to review this article, and <a href="https://blog.linss.com/">Peter Linss</a> for walking me through the CSS Working Group’s testing infrastructure. Front page image credit: “<a href="https://medium.com/design-ux/926eb80d64e3">Transitional Interfaces</a>,” Pasquale D’Silva</em>

{{< signature "al" >}}


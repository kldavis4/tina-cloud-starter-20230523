---
title: 'A Practical Overview Of CSS Houdini'
slug: practical-overview-css-houdini
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fa0396da-2335-45cb-9b76-14cb1e55f306/practical-overview-css-houdini.png
date: 2020-03-19T12:30:00.000Z
summary: >-
  Houdini, an umbrella term for the collection of browser APIs, aims to bring significant improvements to the web development process and the development of CSS standards in general. Frontend developers will be able to extend the CSS with new features using JavaScript, hook into CSS rendering engine and tell the browser how to apply CSS during a render process. Houdini’s browser support is improving and some APIs are available for use today, so it’s a good time to become familiar with them and experiment. We are going to take a look at each part of Houdini, its current browser support and see how they can be used today using progressive enhancement.
description: >-
  In this article, we take a look at each part of Houdini, its current browser support, and see how they can be used today using progressive enhancement.
categories:
  - CSS
  - Tools
  - Browsers
---

It takes a long time for a new CSS feature or improvement to progress from an initial draft to a fully-supported and stable CSS feature that developers can use. JavaScript-based polyfills can be used as a substitute for the lack of browser support in order to use new CSS features before they’re officially implemented. But they are flawed in most cases. For example, [scrollsnap-polyfill](https://github.com/ckrack/scrollsnap-polyfill/) is one of several polyfills that can be used to fix browser support inconsistencies for the CSS Scroll Snap specification. But even that solution has some limitations, bugs and inconsistencies.

The potential downside to using polyfills is that they can have a [negative impact on performance](https://philipwalton.com/articles/the-dark-side-of-polyfilling-css/) and are difficult to implement properly. This downside is related to the browser’s DOM and CSSOM. Browser creates a **DOM (Document Object Model)** from HTML markup and, similarly, it created **CSSOM (CSS Object Model)** from CSS markup. These two object trees are independent of one another. JavaScript works on DOM and has very limited access to CSSOM.

JavaScript Polyfill solutions run only after the initial render cycle has been completed, i.e. when both DOM and CSSOM have been created and the document has finished loading. After Polyfill makes changes to styles in the DOM (by inlining them), it causes the render process to run again and the whole page re-renders. Negative performance impact gets even more apparent if they rely on the `requestAnimationFrame` method or depend on user interactions like scroll events.

Another obstacle in web development is various **constraints imposed by the CSS standards**. For example, there are only a limited number of CSS properties that can be natively animated. CSS knows how to natively animate colors, but doesn't know how to animate gradients. There has always been a need to innovate and create impressive web experiences by pushing the boundaries despite the tech limitations. That is why developers often tend to gravitate towards using less-than-ideal workarounds or JavaScript to implement more advanced styling and effects that are currently not supported by CSS such as masonry layout, advanced 3D effects, advanced animation, fluid typography, animated gradients, styled `select` elements, etc.

It seems **impossible for CSS specifications to keep up** with the various [feature demands from the industry](https://twitter.com/jensimmons/status/1062834380563828736) such as more control over animations, improved text truncation, better styling option for `input`  and `select` elements, more `display` options, more `filter` options, etc.

What could be the potential solution? Give developers a **native way of extending CSS using various APIs**. In this article, we are going to take a look at how frontend developers can do that using Houdini APIs, JavaScript, and CSS. In each section, we’re going to examine each API individually, check its browser support and current specification status, and see how they can be implemented today using Progressive enhancement.

{{% feature-panel %}}

## What Is Houdini?

Houdini, an umbrella term for the collection of browser APIs, aims to bring significant improvements to the web development process and the development of CSS standards in general. Developers will be able to extend the CSS with new features using JavaScript, hook into CSS rendering engine and tell the browser how to apply CSS during a render process. This will result in significantly better performance and stability than using regular polyfills.

Houdini specification consists of two API groups - **high-level APIs** and **low-level APIs**.

**High-level APIs** are closely related to the browser’s rendering process (style → layout → paint → composite). This includes:

- **Paint API**  
An extension point for the browser’s paint rendering step where visual properties (color, background, border, etc.) are determined.
- **Layout API**  
An extension point for the browser’s layout rendering step where element dimensions, position, and alignment are determined.
- **Animation API**  
An extension point for browser’s composite rendering step where layers are drawn to the screen and animated.

**Low-Level API**s form a foundation for high-level APIs. This includes:

- Typed Object Model API
- Custom Properties & Values API
- Font Metrics API
- Worklets

Some Houdini APIs are already available for use in [some browsers](https://ishoudinireadyyet.com/) with other APIs to follow suit when they’re ready for release. 

## The Future Of CSS

Unlike regular CSS feature specifications that have been introduced thus far, Houdini stands out by allowing developers to extend the CSS in a more native way. Does this mean that CSS specifications will stop evolving and no new official implementations of CSS features will be released? Well, that is not the case. Houdini’s goal is to aid the CSS feature development process by allowing developers to create working prototypes that can be easily standardized.

Additionally, developers will be able to share the open-source CSS Worklets more easily and with less need for browser-specific bugfixes.

{{% ad-panel-leaderboard %}}

## Typed Object Model API

Before Houdini was introduced, the only way for JavaScript to interact with CSS was by parsing CSS represented as string values and modifying them. Parsing and overriding styles manually can be difficult and error-prone due to the value type needing to be changed back and forth and value unit needing to be manually appended when assigning a new value.

<pre><code class="language-css">selectedElement.style.fontSize = newFontSize + "px"; // newFontSize = 20
console.log(selectedElement.style.fontSize); // "20px"
</code></pre>

**Typed Object Model (Typed OM)** API adds more semantic meaning to CSS values by exposing them as typed JavaScript objects. It significantly improves the related code and makes it more performant, stable and maintainable. CSS values are represented by the  `CSSUnitValue` interface which consists of a value and a unit property.

<pre><code class="language-css">{
  value: 20, 
  unit: "px"
}
</code></pre>

This new interface can be used with the following new properties:

- `computedStyleMap()`: for parsing computed (non-inline) styles. This is a method of selected element that needs to be invoked before parsing or using other methods.
- `attributeStyleMap`: for parsing and modifying inline styles. This is a property that is available on a selected element.

<div class="break-out">

 <pre><code class="language-javascript">// Get computed styles from stylesheet (initial value)
selectedElement.computedStyleMap().get("font-size"); // { value: 20, unit: "px"}

// Set inline styles
selectedElement.attributeStyleMap.set("font-size", CSS.em(2)); // Sets inline style
selectedElement.attributeStyleMap.set("color", "blue"); // Sets inline style

// Computed style remains the same (initial value)
selectedElement.computedStyleMap().get("font-size"); // { value: 20, unit: "px"}

// Get new inline style
selectedElement.attributeStyleMap.get("font-size"); // { value: 2, unit: "em"}
</code></pre>
</div>

Notice how specific CSS types are being used when setting a new numeric value. By using this syntax, many potential type-related issues can be avoided and the resulting code is more reliable and bug-free.

The  `get` and `set` methods are only a small subset of all available methods defined by the Typed OM API. Some of them include:

- `clear`: removes all inline styles
- `delete`: removes a specified CSS property and its value from inline styles
- `has`: returns a boolean if a specified CSS property is set
- `append`: adds an additional value to a property that supports multiple values
- etc.

### Feature detection

<div class="break-out">

 <pre><code class="language-javascript">var selectedElement = document.getElementById("example");

if(selectedElement.attributeStyleMap) {
  /&#42; ... &#42;/
}

if(selectedElement.computedStyleMap) {
  /&#42; ... &#42;/
}
</code></pre>
</div>

### W3C Specification Status

- [Working Draft](https://drafts.css-houdini.org/css-typed-om/): published for review by the community

### Browser Support

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
    <tr>
      <th>Google Chrome</th>
      <th>Microsoft Edge</th>
      <th>Opera Browser</th>
      <th>Firefox</th>
      <th>Safari</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Supported</td>
      <td>Supported</td>
      <td>Supported</td>
      <td>Not supported</td>
      <td>Partial support (*)</td>
    </tr>
  </tbody>
</table>

<p><sup>*</sup> <em>supported with “Experimental Web Platform features” or other feature flag enabled.</em></p>

<p><em>Data source: <a href="https://ishoudinireadyyet.com/">Is Houdini Ready Yet?</a></em></p>

## Custom Properties And Values API

The *CSS Properties And Values* API allows developers to extend CSS variables by adding a type, initial value and define inheritance. Developers can define CSS custom properties by registering them using the `registerProperty` method which tells the browsers how to transition it and handle fallback in case of an error.

<pre><code class="language-css">CSS.registerProperty({ 
  name: "--colorPrimary",
  syntax: "&lt;color&gt;", 
  inherits: false,
  initialValue: "blue",
});
</code></pre>

This method accepts an input argument that is an object with the following properties:

- `name`: the name of the custom property
- `syntax`: tells the browser how to parse a custom property. These are pre-defined values like `<color>`, `<integer>`, `<number>`, `<length>`, `<percentage>`, etc.
- `inherits`: tells the browser whether the custom property inherits its parent’s value.
- `initialValue`: tells the initial value that is used until it’s overridden and this is used as a fallback in case of an error.

{{% ad-panel-leaderboard %}}

In the following example, the `<color>` type custom property is being set. This custom property is going to be used in gradient transition. You might be thinking that current CSS doesn’t support transitions for background gradients and you would be correct. Notice how the custom property itself is being used in `transition`, instead of a `background` property that would be used for regular `background-color` transitions.

<div class="break-out">

 <pre><code class="language-css">.gradientBox { 
  background: linear-gradient(45deg, rgba(255,255,255,1) 0%, var(--colorPrimary) 60%);
  transition: --colorPrimary 0.5s ease;
  /&#42; ... &#42;/
}

.gradientBox:hover {
  --colorPrimary: red
  /&#42; ... &#42;/
}
</code></pre>
</div>

Browser doesn’t know how to handle gradient transition, but it knows how to handle color transitions because the custom property is specified as `<color>` type. On a browser that supports Houdini, a gradient transition will happen when the element is being hovered on. Gradient position percentage can also be replaced with CSS custom property (registered as `<percentage>` type) and added to a transition in the same way as in the example.

If `registerProperty` is removed and a regular CSS custom property is registered in a `:root` selector, the gradient transition won’t work. It’s required that `registerProperty` is used so the browser knows that it should treat it as color.

In the future implementation of this API, it would be possible to register a custom property directly in CSS. 

<pre><code class="language-css">@property --colorPrimary { 
  syntax: "&lt;color&gt;"; 
  inherits: false; 
  initial-value: blue;
}
</code></pre>

### Example

This simple example showcases gradient color and position transition on hover event using registered CSS custom properties for color and position respectively. Complete source code is available on the [example repository](https://github.com/codeAdrian/houdini-examples/tree/master/custom-properties-api).
 
<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acdaf093-aac3-43c5-bd69-eb0057497122/1-image-properties-api.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acdaf093-aac3-43c5-bd69-eb0057497122/1-image-properties-api.gif" alt="" /></a><figcaption>Animated gradient color and position using Custom Properties & Values API. Delay for each property added for effect in CSS transition property. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/acdaf093-aac3-43c5-bd69-eb0057497122/1-image-properties-api.gif">Large preview</a>)</figcaption></figure>

### Feature Detection

<pre><code class="language-css">if (CSS.registerProperty) {
  /&#42; ... &#42;/
}
</code></pre>

### W3C Specification Status

- [Working Draft](https://drafts.css-houdini.org/css-properties-values-api/): published for review by the community

### Browser Support

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
    <tr>
      <th>Google Chrome</th>
      <th>Microsoft Edge</th>
      <th>Opera Browser</th>
      <th>Firefox</th>
      <th>Safari</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Supported</td>
      <td>Supported</td>
      <td>Supported</td>
      <td>Not supported</td>
      <td>Not supported</td>
    </tr>
  </tbody>
</table>

<p><em>Data source: <a href="https://ishoudinireadyyet.com/">Is Houdini Ready Yet?</a></em></p>

## Font Metrics API

The *Font Metrics* API is still in a very early stage of development, so its specification may change in the future. In its current draft, **Font Metrics API** will provide methods for measuring dimensions of text elements that are being rendered on screen in order to allow developers to affect how text elements are being rendered on screen. These values are either difficult or impossible to measure with current features, so this API will allow developers to create text and font-related CSS features more easily. Multi-line dynamic text truncation is an example of one of those features.

### W3C Specification Status

- [Collection of Ideas](https://drafts.css-houdini.org/font-metrics-api/): no specification draft submitted at the moment

### Browser Support

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
    <tr>
      <th>Google Chrome</th>
      <th>Microsoft Edge</th>
      <th>Opera Browser</th>
      <th>Firefox</th>
      <th>Safari</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Not supported</td>
      <td>Not supported</td>
      <td>Not supported</td>
      <td>Not supported</td>
      <td>Not supported</td>
    </tr>
  </tbody>
</table>

<p><em>Data source: <a href="https://ishoudinireadyyet.com/">Is Houdini Ready Yet?</a></em></p>

## Worklets

Before moving onto the other APIs, it’s important to explain the Worklets concept. **Worklets** are scripts that run during render and are independent of the main JavaScript environment. They are an extension point for rendering engines. They are designed for parallelism (with 2 or more instances) and thread-agnostic, have reduced access to the global scope and are called by the rendering engine when needed. Worklets can be run only on HTTPS (on production environment) or on localhost (for development purposes).

Houdini introduces following Worklets to extend the browser render engine: 

- Paint Worklet - Paint API
- Animation Worklet - Animation API
- Layout Worklet - Layout API

## Paint API

The Paint API allows developers to use JavaScript functions to draw directly into an element’s background, border, or content using [2D Rendering Context](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D), which is a subset of the HTML5 Canvas API. Paint API uses Paint Worklet to draw an image that dynamically responds to changes in CSS (changes in CSS variables, for example). Anyone familiar with Canvas API will feel right at home with Houdini’s Paint API.

There are several steps required in defining a Paint Worklet:

1. Write and register a Paint Worklet using the `registerPaint` function
2. Call the Worklet in HTML file or main JavaScript file using `CSS.paintWorklet.addModule` function
3. Use the `paint()` function in CSS with a Worklet name and optional input arguments.

Let’s take a look at the `registerPaint` function which is used to register a Paint Worklet and define its functionality.

<div class="break-out">

 <pre><code class="language-css">registerPaint("paintWorketExample", class {
  static get inputProperties() { return ["--myVariable"]; }
  static get inputArguments() { return ["&lt;color&gt;"]; }
  static get contextOptions() { return {alpha: true}; }

  paint(ctx, size, properties, args) {
    /&#42; ... &#42;/
  }
});
</code></pre>
</div>

The `registerPaint` function consists of several parts:

- `inputProperties`:  
An array of CSS custom properties that the Worklet will keep track of. This array represents dependencies of a paint worklet.
- `inputArguments`:  
An array of input arguments that can be passed from `paint` function from inside the CSS.
- `contextOptions`: allow or disallow opacity for colors. If set to `false`, all colors will be displayed with full opacity.
- `paint`: the main function that provides the following arguments:
    - `ctx`: 2D drawing context, almost identical to Canvas API’s 2D drawing context.
    - `size`: an object containing the width and height of the element. Values are determined by the layout rendering process. Canvas size is the same as the actual size of the element.
    - `properties`: input variables defined in `inputProperties`
    - `args`: an array of input arguments passed in `paint` function in CSS

After the Worklet has been registered, it needs to be invoked in the HTML file by simply providing a path to the file.

<pre><code class="language-css">CSS.paintWorklet.addModule("path/to/worklet/file.js");
</code></pre>

Any Worklet can also be added from an external URL (from a Content Delivery Network, for example) which makes them modular and reusable.

<pre><code class="language-css">CSS.paintWorklet.addModule("https://url/to/worklet/file.js");
</code></pre>

After the Worklet has been called, it can be used inside CSS using the `paint` function. This function accepts the Worklet’s registered name as a first input argument and each input argument that follows it is a custom argument that can be passed to a Worklet (defined inside Worklet’s `inputArguments` ). From that point, the browser determines when to call the Worklet and which user actions and CSS custom properties value change to respond to.

<pre><code class="language-css">.exampleElement {
  /&#42; paintWorkletExample - name of the worklet
     blue - argument passed to a Worklet &#42;/
  background-image: paint(paintWorketExample, blue);
}
</code></pre>

### Example

The following example showcases Paint API and general Worklet reusability and modularity. It’s using the ripple Worklet directly from [Google Chrome Labs repository](https://github.com/GoogleChromeLabs/houdini-samples/blob/master/paint-worklet/ripple/paintworklet.js) and runs on a different element with different styles. Complete source code is available on the [example repository](https://github.com/codeAdrian/houdini-examples/tree/master/paint-api-example).

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4bfba2d-a245-4b76-a303-b0e78b0c293b/2-image-paint-api.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4bfba2d-a245-4b76-a303-b0e78b0c293b/2-image-paint-api.gif" alt="" /></a><figcaption>Ripple effect example (uses Ripple Worklet by Google Chrome Labs) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f4bfba2d-a245-4b76-a303-b0e78b0c293b/2-image-paint-api.gif">Large preview</a>)</figcaption></figure>

### Feature detection

<pre><code class="language-css">if ("paintWorklet" in CSS) {
  /&#42; ... &#42;/
}


@supports(background:paint(paintWorketExample)){
  /&#42; ... &#42;/
}
</code></pre>

### W3C Specification Status

- [Candidate recommendation](https://drafts.css-houdini.org/css-paint-api/): stable working draft ready for implementation

### Browser Support

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
    <tr>
      <th>Google Chrome</th>
      <th>Microsoft Edge</th>
      <th>Opera Browser</th>
      <th>Firefox</th>
      <th>Safari</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Supported</td>
      <td>Supported</td>
      <td>Supported</td>
      <td>Not supported</td>
      <td>Not supported</td>
    </tr>
  </tbody>
</table>

<p><em>Data source: <a href="https://ishoudinireadyyet.com/">Is Houdini Ready Yet?</a></em></p>

## Animation API

The *Animation* API extends web animations with options to listen to various events (scroll, hover, click, etc.) and improves performance by running animations on their own dedicated thread using an Animation Worklet. It allows for user action to control the flow of animation that runs in a performant, non-blocking way.

Like any Worklet, Animation Worklet needs to be registered first.

<pre><code class="language-css">registerAnimator("animationWorkletExample", class {
  constructor(options) {
    /&#42; ... &#42;/
  }
  animate(currentTime, effect) {
    /&#42; ... &#42;/
  }
});
</code></pre>

This class consists of two functions:

- `constructor`: called when a new instance is created. Used for general setup.
- `animate`: the main function that contains the animation logic. Provides the following input arguments:
    - `currentTime`: the current time value from the defined timeline
    - `effect`: an array of effects that this animation uses

After the Animation Worklet has been registered, it needs to be included in the **main JavaScript file**, animation (element, keyframes, options) needs to be defined and animation is instantiated with the selected timeline. Timeline concepts and web animation basics will be explained in the next section.

<div class="break-out">

 <pre><code class="language-css">/&#42; Include Animation Worklet &#42;/
await CSS.animationWorklet.addModule("path/to/worklet/file.js");;

/&#42; Select element that's going to be animated &#42;/
const elementExample = document.getElementById("elementExample");

/&#42; Define animation (effect) &#42;/
const effectExample = new KeyframeEffect(
  elementExample,  /&#42; Selected element that's going to be animated &#42;/
  [ /&#42; ... &#42;/ ],   /&#42; Animation keyframes &#42;/
  { /&#42; ... &#42;/ },   /&#42; Animation options - duration, delay, iterations, etc. &#42;/
);

/&#42; Create new WorkletAnimation instance and run it &#42;/
new WorkletAnimation(
  "animationWorkletExample"  /&#42; Worklet name &#42;/
  effectExample,             /&#42; Animation (effect) timeline &#42;/
  document.timeline,         /&#42; Input timeline &#42;/
  {},                        /&#42; Options passed to constructor &#42;/
).play();                    /&#42; Play animation &#42;/
</code></pre>
</div>

### Timeline Mapping

Web animation is based on timelines and **mapping of the current time to a timeline of an effect’s local time**. For example, let’s take a look at a repeating linear animation with 3 keyframes (start, middle, last) that runs 1 second after a page is loaded (delay) and with a 4-second duration.

Effect timeline from the example would look like this (with the 4-second duration with no delay):

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
    <tr>
      <th>Effect timeline (4s duration)</th>
      <th>Keyframe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0ms</td>
      <td>First keyframe - animation starts</td>
    </tr>
    <tr>
      <td>2000ms</td>
      <td>Middle keyframe - animation in progress</td>
    </tr>
    <tr>
      <td>4000ms</td>
      <td>Last keyframe - animation ends or resets to first keyframe</td>
    </tr>
  </tbody>
</table>

In order to better understand `effect.localTime`, by setting its value to 3000ms (taking into account 1000ms delay), resulting animation is going to be locked to a middle keyframe in effect timeline (1000ms delay + 2000ms for a middle keyframe). The same effect is going to happen by setting the value to 7000ms and 11000ms because the animation repeats in 4000ms interval (animation duration).

<pre><code class="language-css">animate(currentTime, effect) {
  effect.localTime = 3000; // 1000ms delay + 2000ms middle keyframe
}
</code></pre>

No animation happens when having a constant `effect.localTime` value because animation is locked in a specific keyframe. In order to properly animate an element, its `effect.localTime` needs to be dynamic. It’s required for the value to be a function that depends on the `currentTime` input argument or some other variable.

The following code shows a functional representation of 1:1 (linear function) mapping of a timeline to effect local time.

<pre><code class="language-css">animate(currentTime, effect) {
  effect.localTime = currentTime; // y = x linear function
}
</code></pre>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th>Timeline (<code>document.timeline</code>)</th>
      <th>Mapped effect local time</th>
      <th>Keyframe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>startTime</code> + 0ms (elapsed time)</td>
      <td><code>startTime</code> + 0ms</td>
      <td>First</td>
    </tr>
    <tr>
      <td><code>startTime</code> + 1000ms (elapsed time)</td>
      <td><code>startTime</code> + 1000ms (delay) + 0ms</td>
      <td>First</td>
    </tr>
    <tr>
      <td><code>startTime</code> + 3000ms (elapsed time)</td>
      <td><code>startTime</code> + 1000ms (delay) + 2000ms</td>
      <td>Middle</td>
    </tr>
    <tr>
      <td><code>startTime</code> + 5000ms (elapsed time)</td>
      <td><code>startTime</code> + 1000ms (delay) + 4000ms</td>
      <td>Last / First</td>
    </tr>
    <tr>
      <td><code>startTime</code> + 7000ms (elapsed time)</td>
      <td><code>startTime</code> + 1000ms (delay) + 6000ms</td>
      <td>Middle</td>
    </tr>
    <tr>
      <td><code>startTime</code> + 9000ms (elapsed time)</td>
      <td><code>startTime</code> + 1000ms (delay) + 8000ms</td>
      <td>Last / First</td>
    </tr>
  </tbody>
</table>

Timeline isn’t restricted to 1:1 mapping to effect’s local time. Animation API allows developers to **manipulate the timeline mapping** in  `animate`  function by using standard JavaScript functions to create complex timelines. Animation also doesn’t have to behave the same in each iteration (if animation is repeated).

Animation doesn’t have to depend on the document’s timeline which only starts counting milliseconds from the moment it’s loaded. User actions like scroll events can be used as a timeline for animation by using a `ScrollTimeline` object. For example, an animation can start when a user has scrolled to 200 pixels and can end when a user has scrolled to 800 pixels on a screen.

<div class="break-out">

 <pre><code class="language-css">const scrollTimelineExample = new ScrollTimeline({
  scrollSource: scrollElement,  /&#42; DOM element whose scrolling action is being tracked &#42;/
  orientation: "vertical",      /&#42; Scroll direction &#42;/
  startScrollOffset: "200px",   /&#42; Beginning of the scroll timeline &#42;/
  endScrollOffset: "800px",    /&#42; Ending of the scroll timeline &#42;/
  timeRange: 1200,              /&#42; Time duration to be mapped to scroll values*/
  fill: "forwards"              /&#42; Animation fill mode &#42;/
});

...
</code></pre>
</div>

The animation will automatically adapt to user scroll speed and remain smooth and responsive. Since Animation Worklets are running off the main thread and are connected to a browser’s rending engine, animation that depends on user scroll can run smoothly and be very performant.

### Example

The following example showcases how a non-linear timeline implementation. It uses modified [Gaussian function](https://mathworld.wolfram.com/GaussianFunction.html) and applies translation and rotation animation with the same timeline. Complete source code is available on the [example repository](https://github.com/codeAdrian/houdini-examples/tree/master/animation-api-example).

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66382772-0c0c-4b34-9326-4451db5d9c15/3-image-animation-api.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66382772-0c0c-4b34-9326-4451db5d9c15/3-image-animation-api.gif" alt="" /></a><figcaption>Animation created with Animation API which is using modified Gaussian function time mapping (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/66382772-0c0c-4b34-9326-4451db5d9c15/3-image-animation-api.gif">Large preview</a>)</figcaption></figure>

### Feature Detection

<pre><code class="language-css">if (CSS.animationWorklet) {
  /&#42; ... &#42;/
}
</code></pre>

### W3C Specification Status

- [First Public Working Draft](https://drafts.css-houdini.org/css-animationworklet/): ready for community review, prone to specification change

### Browser Support

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
    <tr>
      <th>Google Chrome</th>
      <th>Microsoft Edge</th>
      <th>Opera Browser</th>
      <th>Firefox</th>
      <th>Safari</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Partial support (*)</td>
      <td>Partial support (*)</td>
      <td>Partial support (*)</td>
      <td>Not supported</td>
      <td>Not supported</td>
    </tr>
  </tbody>
</table>

<p><sup>*</sup> <em>supported with “Experimental Web Platform features” flag enabled.</em></p>

<p><em>Data source: <a href="https://ishoudinireadyyet.com/">Is Houdini Ready Yet?</a></em></p>

## Layout API

The *Layout* API allows developers to extend the browser’s layout rendering process by defining new layout modes that can be used in `display` CSS property. Layout API introduces new concepts, is very complex and offers a lot of options for developing custom layout algorithms. 

Similarly to other Worklets, the layout Worklet needs to be registered and defined first.

<div class="break-out">

 <pre><code class="language-css">registerLayout('exampleLayout', class {
  static get inputProperties() { return ['--exampleVariable']; }

  static get childrenInputProperties() { return ['--exampleChildVariable']; }

  static get layoutOptions() {
    return {
      childDisplay: 'normal',
      sizing: 'block-like'
    };
  }

  intrinsicSizes(children, edges, styleMap) {
    /* ... */
  }

  layout(children, edges, constraints, styleMap, breakToken) {
    /* ... */
  }
});
</code></pre>
</div>

Worklet register contains the following methods:

- `inputProperties`:  
An array of CSS custom properties that the Worklet will keep track of that belongs to a Parent Layout element, i.e. the element that calls this layout. This array represents dependencies of a Layout Worklet.
- `childrenInputProperties`:  
An array of CSS custom properties that the Worklet will keep track of that belong to child elements of a Parent Layout element, i.e. the children of the elements that set this layout.
- `layoutOptions`: defines the following layout properties:
    - `childDisplay`: can have a pre-defined value of  `block` or `normal`. Determines if the boxes will be displayed as blocks or inline.
    - `sizing`: can have a pre-defined value of `block-like` or `manual`. It tells the browser to either pre-calculate the size or not to pre-calculate (unless a size is explicitly set), respectively.
- `intrinsicSizes`: defines how a box or its content fits into a layout context.
    - `children`: child elements of a Parent Layout element, i.e. the children of the element that call this layout.
    - `edges`: Layout Edges of a box
    - `styleMap`: typed OM styles of a box
- `layout`: the main function that performs a layout.
    - `children`: child elements of a Parent Layout element, i.e. the children of the element that call this layout.
    - `edges`: Layout Edges of a box
    - `constraints`: constraints of a Parent Layout
    - `styleMap`: typed OM styles of a box
    - `breakToken`: break token used to resume a layout in case of pagination or printing. 

Like in the case of a Paint API, the browser rendering engine determines when the paint Worklet is being called. It only needs to be added to an HTML or main JavaScript file.

<pre><code class="language-css">CSS.layoutWorklet.addModule('path/to/worklet/file.js');
</code></pre>

And, finally, it needs to be referenced in a CSS file

<pre><code class="language-css">.exampleElement {
  display: layout(exampleLayout);
}
</code></pre>

### How Layout API Performs Layout

In the previous example, `exampleLayout` has been defined using the Layout API.

<pre><code class="language-css">.exampleElement {
  display: layout(exampleLayout);
}
</code></pre>

This element is called a **Parent Layout** that is enclosed with **Layout Edges** which consists of paddings, borders and scroll bars. Parent Layout consists of child elements which are called **Current Layouts**. Current Layouts are the actual target elements whose layout can be customized using the Layout API. For example, when using `display: flex;` on an element, its children are being repositioned to form the flex layout. This is similar to what is being done with the Layout API.

Each **Current Layout** consists of **Child Layout** which is a layout algorithm for the LayoutChild (element, `::before` and `::after` pseudo-elements) and **LayoutChild** is a CSS generated box that only contains style data (no layout data). LayoutChild elements are automatically created by browser rendering engine on style step. Layout Child can generate a **Fragment** which actually performs layout render actions.

### Example

Similarly to the Paint API example, this example is importing a masonry layout Worklet directly from [Google Chrome Labs repository](https://github.com/GoogleChromeLabs/houdini-samples/blob/master/layout-worklet/masonry/masonry.js), but in this example, it’s used with image content instead of text. Complete source code is available on the [example repository](https://github.com/codeAdrian/houdini-examples/tree/master/layout-api-example).

<figure class="break-out"><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ede5f0c-d568-49fe-a83b-1a9561c2fded/4-image-layout-api.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ede5f0c-d568-49fe-a83b-1a9561c2fded/4-image-layout-api.gif" alt="" /></a><figcaption>Masonry layout example (uses Masonry Worklet by Google Chrome Labs (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ede5f0c-d568-49fe-a83b-1a9561c2fded/4-image-layout-api.gif">Large preview</a>)</figcaption></figure>

### Feature Detection

<pre><code class="language-css">if (CSS.layoutWorklet) {
  /&#42; ... &#42;/
}
</code></pre>

### W3C Specification Status

- [First Public Working Draft](https://drafts.css-houdini.org/css-layout-api/): ready for community review, prone to specification change

### Browser Support

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
    <tr>
      <th>Google Chrome</th>
      <th>Microsoft Edge</th>
      <th>Opera Browser</th>
      <th>Firefox</th>
      <th>Safari</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Partial support (*)</td>
      <td>Partial support (*)</td>
      <td>Partial support (*)</td>
      <td>Not supported</td>
      <td>Not supported</td>
    </tr>
  </tbody>
</table>

<p><sup>*</sup> <em>supported with “Experimental Web Platform features” flag enabled.</em></p>

<p><em>Data source: <a href="https://ishoudinireadyyet.com/">Is Houdini Ready Yet?</a></em></p>

## Houdini And Progressive Enhancement

Even though CSS Houdini doesn’t have optimal browser support yet, it can be used today with progressive enhancement in mind. If you are unfamiliar with Progressive enhancement, it would be worth to check out [this handy article](https://www.smashingmagazine.com/2009/04/progressive-enhancement-what-it-is-and-how-to-use-it/) which explains it really well. If you decide on implementing Houdini in your project today, there are few things to keep in mind:

- **Use feature detection to prevent errors.**  
Each Houdini API and Worklet offers a simple way of checking if it’s available in the browser. Use feature detection to apply Houdini enhancements only to browsers that support it and avoid errors.
- **Use it for presentation and visual enhancement only.**  
Users that are browsing a website on a browser that doesn’t yet support Houdini should have access to the content and core functionality of the website. User experience and the content presentation shouldn’t depend on Houdini features and should have a reliable fallback.
- **Make use of a standard CSS fallback.**  
For example, regular CSS Custom Properties can be used as a fallback for styles defined using Custom Properties & Values API.

Focus on developing a performant and reliable website user experience first and then use Houdini features for decorative purposes as a progressive enhancement.

## Conclusion

Houdini APIs will finally enable developers to keep the JavaScript code used for style manipulation and decoration closer to the browser’s rendering pipeline, resulting in better performance and stability. By allowing developers to hook into the browser rendering process, they will be able to develop various CSS polyfills that can be easily shared, implemented and, potentially, added to CSS specification itself. Houdini will also make developers and designers less constrained by the CSS limitations when working on styling, layouts, and animations, resulting in new delightful web experiences.

CSS Houdini features can be added to projects today, but strictly with progressive enhancement in mind. This will enable browsers that do not support Houdini features to render the website without errors and offer optimal user experience.

It’s going to be exciting to watch what the developer community will come up with as Houdini gains traction and better browser support. Here are some awesome examples of Houdini API experiments from the community:

- [CSS Houdini Experiments](https://css-houdini.rocks/)
- [Interactive Introduction to CSS Houdini](https://houdini.glitch.me/)
- [Houdini Samples by Google Chrome Labs](https://googlechromelabs.github.io/houdini-samples/)

### References

- [W3C Houdini Specification Drafts](https://drafts.css-houdini.org/)
- [State of Houdini (Chrome Dev Summit 2018)](https://www.youtube.com/watch?v=lK3OiJvwgSc)
- [Houdini’s Animation Worklet - Google Developers](https://developers.google.com/web/updates/2018/10/animation-worklet)
- [Interactive Introduction to CSS Houdini](https://houdini.glitch.me/)

{{< signature "ra, il" >}}

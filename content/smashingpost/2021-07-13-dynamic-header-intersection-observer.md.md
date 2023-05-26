---
title: 'Building A Dynamic Header With Intersection Observer'
slug: dynamic-header-intersection-observer
author: michelle-barker
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/67cc7303-3dc9-4d67-b0f4-b6f77783380f/dynamic-header-intersection-observer.jpg
date: 2021-07-13T12:00:00.000Z
summary: >-
  Have you ever needed to build a UI where some component on the page needs to respond to elements as they’re scrolled to a certain threshold within the viewport &mdash; or perhaps in and out of the viewport itself? In JavaScript, attaching an event listener to constantly fire a callback on scroll can be performance-intensive, and if used unwisely, can make for a sluggish user experience. But there is a better way with Intersection Observer.
description: >-
  In JavaScript, attaching an event listener to constantly fire a callback on scroll can be performance-intensive. But there is a better way with Intersection Observer.
categories:
  - UI
  - API
  - JavaScript
  - Performance
---

The [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) is a JavaScript API that enables us to observe an element and detect when it passes a specified point in a scrolling container &mdash; often (but not always) the viewport &mdash; triggering a callback function.

Intersection Observer can be considered more performant than listening for scroll events on the main thread, as it is asynchronous, and the callback will only fire when the element we’re observing meets the specified threshold, instead every time the scroll position is updated. In this article, we’ll walk through an example of how we can use Intersection Observer to build a fixed header component that changes when it intersects with different sections of the webpage.

## Basic Usage

To use Intersection Observer, we need to first create a new observer, which takes two parameters: An object with the observer’s options, and the callback function that we want to execute whenever the element we’re observing (known as the observer target) intersects with the root (the scrolling container, which must be an ancestor of the target element).

<pre><code class="language-css">const options = {
  root: document.querySelector('[data-scroll-root]'),
  rootMargin: '0px',
  threshold: 1.0
}

const callback = (entries, observer) => {
  entries.forEach((entry) => console.log(entry))
}

const observer = new IntersectionObserver(callback, options)
</code></pre>

When we’ve created our observer, we then need to instruct it to watch a target element:

<pre><code class="language-css">const targetEl = document.querySelector('[data-target]')

observer.observe(targetEl)
</code></pre>

Any of the options values can be omitted, as they will fall back to their default values:

<pre><code class="language-css">const options = {
  rootMargin: '0px',
  threshold: 1.0
}
</code></pre>

If no root is specified, then it will be classed as the browser viewport. The above code example shows the default values for both `rootMargin` and `threshold`. These can be hard to visualize, so are worth explaining:

### `rootMargin`

The `rootMargin` value is a bit like adding CSS margins to the root element &mdash; and, just like margins, can take multiple values, including negative values. The target element will be considered to be intersecting relative to the margins. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/769b2733-5700-4d2d-a32f-6850a173abaa/1-dynamic-header-intersection-observer.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/769b2733-5700-4d2d-a32f-6850a173abaa/1-dynamic-header-intersection-observer.png" width="800" height="" sizes="100vw" caption="The scroll root with positive and negative root margin values. The orange square is positioned at the point where it would be classed as “intersecting”, assuming a default threshold value of 1. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/769b2733-5700-4d2d-a32f-6850a173abaa/1-dynamic-header-intersection-observer.png'>Large preview</a>)" alt="" >}}

That means that an element can technically be classed as “intersecting” even when it is out of view (if our scroll root is the viewport).

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5908e69-f81a-4e1c-81e6-aae2f1b96a28/2-dynamic-header-intersection-observer.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5908e69-f81a-4e1c-81e6-aae2f1b96a28/2-dynamic-header-intersection-observer.png" width="800" height="" sizes="100vw" caption="The orange square is intersecting with the root, even though it is outside the visible area. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5908e69-f81a-4e1c-81e6-aae2f1b96a28/2-dynamic-header-intersection-observer.png'>Large preview</a>)" alt="" >}}

`rootMargin` defaults to `0px`, but can take a string consisting of multiple values, just like using the `margin` property in CSS.

### `threshold`

The `threshold` can consist of a single value or an array of values between 0 and 1. It represents the **proportion of the element that must be within the root bounds for it to be considered intersecting**. Using the default value of 1, the callback will fire when 100% of the target element is visible within the root.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b95822cd-d3e8-4b71-9d38-862e6d39990a/3-dynamic-header-intersection-observer.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b95822cd-d3e8-4b71-9d38-862e6d39990a/3-dynamic-header-intersection-observer.png" width="800" height="" sizes="100vw" caption="Thresholds of 1, 0, and 0.5 respectively result in the callback firing when 100%, 0% and 50% is visible. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b95822cd-d3e8-4b71-9d38-862e6d39990a/3-dynamic-header-intersection-observer.png'>Large preview</a>)" alt="" >}}

It’s not always easy to visualize when an element will be classed as visible using these options. I’ve built [a small tool](https://codepen.io/michellebarker/full/xxwLpRG) to help get to grips with Intersection Observer.

{{% feature-panel %}}

## Creating The Header

Now that we’ve grasped the basic principles, let’s start building our dynamic header. We’ll start with a webpage divided up into sections. This image shows the complete layout of the page we’ll be building:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/886e6b93-48a4-4282-8823-a7bd9e74058c/4-dynamic-header-intersection-observer.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/886e6b93-48a4-4282-8823-a7bd9e74058c/4-dynamic-header-intersection-observer.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/886e6b93-48a4-4282-8823-a7bd9e74058c/4-dynamic-header-intersection-observer.png'>Large preview</a>)" alt="" >}}

I’ve included a demo at the end of this article, so feel free to [jump straight to it](https://codepen.io/michellebarker/pen/aee240bb09868abfc5854854cf0843e3) if you’re keen to unpick the code. (There’s also a [Github repository](https://github.com/mbarker84/smashing-io-header).)

Each section has a minimum height of `100vh` (although they could be longer, depending on content). Our header is fixed at the top of the page and stays in place as the user scrolls (using `position: fixed`). The sections have different colored backgrounds, and when they meet the header, the colors of the header change to complement those of the section. There is also a marker to show the current section the user is in, which slides along when the next section arrives.
To make it easier for us to get straight to the relevant code, I’ve set up a [minimal demo](https://codepen.io/michellebarker/pen/488760bfec40302fcf0e8b7cd3e6093e) with our starting point (before we start using the Intersection Observer API), in case you’d like to follow along.

### Markup

We’ll start with the HTML for our header. This is going to be a fairly simple header with a home link and navigation, nothing especially fancy, but we’re going to use a couple of data attributes: `data-header` for the header itself (so we can target the element with JS), and three anchor links with the attribute `data-link`, which will scroll the user to the relevant section when clicked:

<pre><code class="language-javascript">&lt;header data-header&gt;
  &lt;nav class="header__nav"&gt;
    &lt;div class="header__left-content"&gt;
      &lt;a href="#0"&gt;Home&lt;/a&gt;
    &lt;/div&gt;
    &lt;ul class="header__list"&gt;
      &lt;li&gt;
        &lt;a href="#about-us" data-link&gt;About us&lt;/a&gt;
      &lt;/li&gt;
      &lt;li&gt;
        &lt;a href="#flavours" data-link&gt;The flavours&lt;/a&gt;
      &lt;/li&gt;
      &lt;li&gt;
        &lt;a href="#get-in-touch" data-link&gt;Get in touch&lt;/a&gt;
      &lt;/li&gt;
    &lt;/ul&gt;
  &lt;/nav&gt;
&lt;/header&gt;
</code></pre>

Next, the HTML for the rest of our page, which is divided up into sections. For brevity, I’ve only included the parts relevant to the article, but the full markup is included in the demo. Each section includes a data attribute specifying the name of the background color, and an `id` that corresponds to one of the anchor links in the header:

<pre><code class="language-javascript">&lt;main&gt;
  &lt;section data-section="raspberry" id="home"&gt;
    &lt;!--Section content--&gt;
  &lt;/section&gt;
  &lt;section data-section="mint" id="about-us"&gt;
    &lt;!--Section content--&gt;
  &lt;/section&gt;
  &lt;section data-section="vanilla" id="the-flavours"&gt;
    &lt;!--Section content--&gt;
  &lt;/section&gt;
  &lt;section data-section="chocolate" id="get-in-touch"&gt;
    &lt;!--Section content--&gt;
  &lt;/section&gt;
&lt;/main&gt;
</code></pre>

We’ll position our header with CSS so that it will stay fixed at the top of the page as the user scrolls:

<pre><code class="language-css">header {
  position: fixed;
  width: 100%;
}
</code></pre>

We’ll also give our sections a minimum height, and center the content. (This code isn’t necessary for the Intersection Observer to work, it’s just for the design.)

<pre><code class="language-css">section {
  padding: 5rem 0;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</code></pre>

### iframe Warning

While building this Codepen demo, I ran into a perplexing issue where my Intersection Observer code that *should* have worked perfectly was failing to fire the callback at the correct point of the intersection but instead firing when the target element intersected with the viewport edge. After a bit of head-scratching, I realized that this was because in Codepen the content is loaded within an iframe, which is treated differently. (See the section of the MDN docs on [Clipping and the intersection rectangle](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) for full details.)

As a workaround, in the demo we can wrap our markup in another element, which will act as the scrolling container &mdash; the root in our IO options &mdash; rather than the browser viewport, as we might expect:

<pre><code class="language-javascript">&lt;div class="scroller" data-scroller&gt;
  &lt;header data-header&gt;
    &lt;!--Header content--&gt;
  &lt;/header&gt;
  &lt;main&gt;
    &lt;!--Sections--&gt;
  &lt;/main&gt;
&lt;/div&gt;
</code></pre>

If you want to see how to use the viewport as the root instead for the same demo, this is included in the [Github repository](https://github.com/mbarker84/smashing-io-header).

## CSS

In our CSS we’ll define some custom properties for the colors we’re using. We’ll also define two additional custom properties for the header text and background colors, and set some initial values. (We’re going to update these two custom properties for the different sections later on.)

<pre><code class="language-css">:root {
  --mint: #5ae8d5;
  --chocolate: #573e31;
  --raspberry: #f2308e;
  --vanilla: #faf2c8;
  
  --headerText: var(--vanilla);
  --headerBg: var(--raspberry);
}
</code></pre>

We’ll use these custom properties in our header:

<pre><code class="language-css">header {
  background-color: var(--headerBg);
  color: var(--headerText);
}
</code></pre>

We’ll also set the colors for our different sections. I’m using the data attributes as the selectors, but you could just as easily use a class if you prefer.

<pre><code class="language-css">[data-section="raspberry"] {
  background-color: var(--raspberry);
  color: var(--vanilla);
}

[data-section="mint"]  {
  background-color: var(--mint);
  color: var(--chocolate);
}

[data-section="vanilla"] {
  background-color: var(--vanilla);
  color: var(--chocolate);
}

[data-section="chocolate"] {
  background-color: var(--chocolate);
  color: var(--vanilla);
}
</code></pre>

We can also set some styles for our header when each section is in view:

<pre><code class="language-css">/* Header */
[data-theme="raspberry"]  {
  --headerText: var(--raspberry);
  --headerBg: var(--vanilla);
}

[data-theme="mint"] {
  --headerText: var(--mint);
  --headerBg: var(--chocolate);
}

[data-theme="chocolate"]  {
  --headerText: var(--chocolate);
  --headerBg: var(--vanilla);
}
</code></pre>

There’s a stronger case for using data attributes here because we’re going to toggle the `data-theme` attribute of the header upon each intersection.

{{% ad-panel-leaderboard %}}

## Creating The Observer

Now that we have the basic HTML and CSS for our page set up, we can create an observer to watch for each of our sections coming into view. We want to fire a callback whenever a section comes into contact with the bottom of the header as we’re scrolling down the page. This means we need to set a negative root margin that corresponds to the height of the header.

<pre><code class="language-css">const header = document.querySelector('[data-header]')
const sections = [...document.querySelectorAll('[data-section]')]
const scrollRoot = document.querySelector('[data-scroller]')

const options = {
  root: scrollRoot,
  rootMargin: `${header.offsetHeight * -1}px`,
  threshold: 0
}
</code></pre>

We’re setting a threshold of *0*, as we want it to fire if *any* part of the section is intersecting with the root margin.

First of all, we’ll create a callback to change the `data-theme` value of the header. (This is more straightforward than adding and removing classes, especially when our header element may have other classes applied.)

<pre><code class="language-css">/* The callback that will fire on intersection */
const onIntersect = (entries) => {
  entries.forEach((entry) => {
    const theme = entry.target.dataset.section
    header.setAttribute('data-theme', theme)
  })
}
</code></pre>

Then we’ll create the observer to watch for the sections intersecting:

<pre><code class="language-css">/* Create the observer */
const observer = new IntersectionObserver(onIntersect, options)

/* Set our observer to observe each section */
sections.forEach((section) => {
  observer.observe(section)
})
</code></pre>

Now we should see our header colors update when each section meets the header.

{{< codepen height="480" theme_id="light" slug_hash="poPgpjZ" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Happy Face Ice Cream Parlour – Step 2](https://codepen.io/smashingmag/pen/poPgpjZ) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

However, you might notice that the colors aren’t updating correctly as we scroll down. In fact, the header is updating with the previous section’s colors each time! Scrolling upwards, on the other hand, it works perfectly. We need to determine the scroll direction and change the behavior accordingly.

### Finding The Scroll Direction

We’ll set a variable in our JS for the direction of scroll, with an initial value of `'up'`, and another for the last known scroll position (`prevYPosition`). Then, within the callback, if the scroll position is greater than the previous value, we can set the `direction` value as `'down'`, or `'up'` if vice versa.

<pre><code class="language-javascript">let direction = 'up'
let prevYPosition = 0

const setScrollDirection = () => {
  if (scrollRoot.scrollTop > prevYPosition) {
    direction = 'down'
  } else {
    direction = 'up'
  }

  prevYPosition = scrollRoot.scrollTop
}

const onIntersect = (entries, observer) => {
  entries.forEach((entry) => {
    setScrollDirection()
          
    /* ... */
  })
}
</code></pre>

We’ll also create a new function to update the header colors, passing in the target section as an argument:

<pre><code class="language-javascript">const updateColors = (target) => {
  const theme = target.dataset.section
  header.setAttribute('data-theme', theme)
}

const onIntersect = (entries) => {
  entries.forEach((entry) => {
    setScrollDirection()
    updateColors(entry.target)
  })
}
</code></pre>

So far we should see no change to the behavior of our header. But now that we know the scroll direction, we can pass in a different target for our `updateColors()` function. If the scroll direction is up, we’ll use the entry target. If it’s down, we’ll use the next section (if there is one).

<pre><code class="language-javascript">const getTargetSection = (target) => {
  if (direction === 'up') return target
  
  if (target.nextElementSibling) {
    return target.nextElementSibling
  } else {
    return target
  }
}

const onIntersect = (entries) => {
  entries.forEach((entry) => {
    setScrollDirection()
    
    const target = getTargetSection(entry.target)
    updateColors(target)
  })
}
</code></pre>

There’s one more issue, however: the header will update not only when the section hits the header, but when the next element comes into view at the bottom of the viewport. This is because our observer fires the callback twice: once as the element is entering, and again as it’s leaving.

To determine whether the header should update, we can use the `isIntersecting` key from the `entry` object. Let’s create another function to return a boolean value for whether the header colors should update:

<pre><code class="language-javascript">const shouldUpdate = (entry) => {
  if (direction === 'down' && !entry.isIntersecting) {
    return true
  }
  
  if (direction === 'up' && entry.isIntersecting) {
    return true
  }
  
  return false
}
</code></pre>

We’ll update our `onIntersect()` function accordingly:

<pre><code class="language-javascript">const onIntersect = (entries) => {
  entries.forEach((entry) => {
    setScrollDirection()
    
    /* Do nothing if no need to update */
    if (!shouldUpdate(entry)) return
    
    const target = getTargetSection(entry.target)
    updateColors(target)
  })
}
</code></pre>

Now our colors should update correctly. We can set a CSS transition, so that the effect is a little nicer:

<pre><code class="language-css">header {
  transition: background-color 200ms, color 200ms;
}
</code></pre>

{{< codepen height="480" theme_id="light" slug_hash="bGWEaEa" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Happy Face Ice Cream Parlour – Step 3](https://codepen.io/smashingmag/pen/bGWEaEa) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

{{% ad-panel-leaderboard %}}

## Adding The Dynamic Marker

Next we’ll add a marker to the header that updates its position as we scroll to the different sections. We can use a pseudo-element for this, so we don’t need to add anything to our HTML. We’ll give it some simple CSS styling to position it at the top left of the header, and give it a background color. We’re using `currentColor` for this, as it will take on the value of the header text color:

<pre><code class="language-css">header::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  height: 0.4rem;
  background-color: currentColor;
}
</code></pre>

We can use a custom property for the width, with a default value of 0. We’ll also use a custom property for the translate x value. We’re going to set the values for these in our callback function as the user scrolls.

<pre><code class="language-css">header::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  height: 0.4rem;
  width: var(--markerWidth, 0);
  background-color: currentColor;
  transform: translate3d(var(--markerLeft, 0), 0, 0);
}
</code></pre>

Now we can write a function that will update the width and position of the marker at the point of intersection:

<pre><code class="language-javascript">const updateMarker = (target) => {
  const id = target.id
  
  /* Do nothing if no target ID */
  if (!id) return
  
  /* Find the corresponding nav link, or use the first one */
  let link = headerLinks.find((el) => {
    return el.getAttribute('href') === `#${id}`
  })
  
  link = link || headerLinks[0]
  
  /* Get the values and set the custom properties */
  const distanceFromLeft = link.getBoundingClientRect().left
  
  header.style.setProperty('--markerWidth', `${link.clientWidth}px`)
  header.style.setProperty('--markerLeft', `${distanceFromLeft}px`)
}
</code></pre>

We can call the function at the same time we update the colors:

<pre><code class="language-javascript">const onIntersect = (entries) => {
  entries.forEach((entry) => {
    setScrollDirection()
    
    if (!shouldUpdate(entry)) return
    
    const target = getTargetSection(entry.target)
    updateColors(target)
    updateMarker(target)
  })
}
</code></pre>

We’ll also need to set an initial position for the marker, so it doesn’t just appear out of nowhere. When the document is loaded, we’ll call the `updateMarker()` function, using the first section as the target:

<pre><code class="language-javascript">document.addEventListener('readystatechange', e => {
  if (e.target.readyState === 'complete') {
    updateMarker(sections[0])
  }
})
</code></pre>

Finally, let’s add a CSS transition so that the marker slides across the header from one link to the next. As we’re transitioning the `width` property, we can use `will-change` to enable the browser to [perform optimizations](https://developer.mozilla.org/en-US/docs/Web/CSS/will-change).

<pre><code class="language-css">header::after {
  transition: transform 250ms, width 200ms, background-color 200ms;
  will-change: width;
}
</code></pre>

## Smooth Scrolling

For a final touch, it would be nice if, when a user clicks a link, they’re scrolled smoothly down the page, instead of it jumping to the section. These days we can do it right in our CSS, no JS required! For a more accessible experience, it’s a good idea to respect the user's motion preferences by only implementing smooth scrolling if they haven’t specified a preference for reduced motion in their system settings:

<pre><code class="language-css">@media (prefers-reduced-motion: no-preference) {
  .scroller {
    scroll-behavior: smooth;
  }
}
</code></pre>

## Final Demo

Putting all the above steps together results in the complete demo.

{{< codepen height="480" theme_id="light" slug_hash="XWRXVXQ" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Happy Face Ice Cream Parlour – Intersection Observer example](https://codepen.io/smashingmag/pen/XWRXVXQ) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

## Browser Support

Intersection Observer is [widely supported](https://caniuse.com/?search=intersection%20observer) in modern browsers. Where necessary it can be [polyfilled](https://github.com/w3c/IntersectionObserver) for older browsers &mdash; but I prefer to take a progressive enhancement approach where possible. In the case of our header, it would not be vastly detrimental to the user experience to provide a simple, unchanging version for non-supporting browsers.

To detect if Intersection Observer is supported, we can use the following:

<div class="break-out">

 <pre><code class="language-javascript">if ('IntersectionObserver' in window && 'IntersectionObserverEntry' in window && 'intersectionRatio' in window.IntersectionObserverEntry.prototype) {
  /* Code to execute if IO is supported */
} else {
  /* Code to execute if not supported */
}
</code></pre>
</div>

## Resources

Read more about Intersection Observer:

- Extensive documentation, with some practical examples from [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)
- Intersection Observer [visualiser tool](https://codepen.io/michellebarker/full/xxwLpRG)
- [Timing Element Visibility with the Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API/Timing_element_visibility) – another tutorial from MDN, that looks at how IO can be used to track ad visibility
- [This article](https://www.smashingmagazine.com/2018/01/deferring-lazy-loading-intersection-observer-api/) by Denys Mishunov covers some other uses for IO, including lazy-loading assets. Although that’s less necessary now (thanks to the `loading` attribute), there’s still plenty to learn here.

{{< signature "vf, il" >}}

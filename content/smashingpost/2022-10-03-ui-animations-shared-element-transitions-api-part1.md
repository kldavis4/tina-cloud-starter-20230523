---
title: 'Delightful UI Animations With Shared Element Transitions API (Part 1)'
slug: ui-animations-shared-element-transitions-api-part1
author: adrian-bece
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24c75fda-847f-4fc5-b9c2-9118523bda6b/ui-animations-shared-element-transitions-api.jpg
date: 2022-10-03T13:00:00.000Z
summary: >-
  Shared Element Transitions API is a game-changing feature that will enable us to create impressive and elaborate UI animations easily. In this article, Adrian Bece will explore its incredible potential by building four real-life examples from scratch.
description: >-
  Shared Element Transitions API is a game-changing feature that will enable us to create impressive and elaborate UI animations easily. In this article, Adrian Bece will explore its incredible potential by building four real-life examples from scratch.
categories:
  - CSS
  - API
  - Animation
  - UI
  - Techniques
---

Animations are an essential part of web design and development. They can draw attention, guide users on their journey, provide satisfying and meaningful feedback to interaction, [add character and flair to make the website stand out](https://teatrlalka.pl/en), and so much more!
 
Before we begin, let’s take a quick look at the following video and imagine how much CSS and JavaScript would take to create an animation like this. Notice that the cart counter is also animated, and the animation runs right after the previous one completes.

{{< vimeo id="750303184" >}}

JavaScript libraries like React and Vue probably popped into your mind right away, alongside JavaScript animation libraries like Framer Motion and GSAP. They do a solid job and certainly simplify the process. However, [JavaScript is the most expensive resource](https://vimeo.com/396638607) on the web, and these libraries are bundled alongside the content and primary resources. In the end, it’s up to the browser to download, parse and execute the animation engine before it’s ready for use.

What if we could just skip all that, use vanilla JavaScript and CSS, and **let the optimized browser API do all the heavy lifting** while **maintaining complete control** over how they perform transitions between the various UI states? With the new Shared Element Transitions API, implementing animations like this will become incredibly easy and seamless.

In this article, we’ll dive deeply into this game-changing API which is still in its early stages, and explore its incredible potential by **building four fun and exciting real-life examples** from scratch. 

## Browser Support And API Status

At the time of this article, API is in its early [“Editor’s](https://tabatkins.github.io/specs/css-shared-element-transitions/) [draft” stage](https://drafts.csswg.org/css-shared-element-transitions-1/), so the standard is not yet finalized, and the specs might change as time goes on.

Shared Element Transitions API is currently supported only in [Chrome version 104+ and Canary](https://chromestatus.com/feature/5193009714954240) with the **document-transition** flag enabled. **Examples will be accompanied by a video**, so you can easily follow along with the article if you don’t have the required browser installed.

{{% feature-panel %}}

## Shared Element Transitions API

Animating between UI states usually requires **both the current and the next state to be present** at the same time. Let’s take a simple image carousel that crossfades between the images as an example. We’ll even create that carousel later. If you were using only JavaScript without any libraries or frameworks, you’d have to ensure that both the current and next image are present, and then fade out the current image and fade in the next image simultaneously. You also have to handle a handful of edge cases and accessibility issues that might come up as a result of that.

In a nutshell, **Shared Element Transitions API** allows us to skip a lot of prep work by ensuring that both outgoing and incoming states are **visually** **present** at the same time. All we have to do is take care of the DOM updates and animation styles. The API also allows us to tap into those individual states and more and gives us full control over the animation using the standard CSS `animation` properties.

Let’s start with a simple and fun example. We’ll create an image gallery with the following animation - on card click, the image inside the card will expand and move from its place in the grid into a fixed overlay. When the expanded image in the overlay is clicked, it will return back into its place. Let’s see how we can create this animation in just a few lines of JavaScript and CSS.

{{< vimeo id="750305649" >}}

### Starting Markup, Styles And JavaScript

Let’s start with the following markup and some basic grid, card, and overlay styles. For more details, check out the source code in the following CodePen:

{{< codepen height="480" theme_id="light" slug_hash="MWGJNaw" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image gallery - vanilla (1) [forked]](https://codepen.io/smashingmag/pen/MWGJNaw) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

Let’s take a closer look at our JavaScript code:

<div class="break-out">

<pre><code class="language-javascript">// Select static & shared page elements.
const overlayWrapper = document.getElementById("js-overlay");
const overlayContent = document.getElementById("js-overlay-target");

function toggleImageView(index) {
    const image = document.getElementById(`js-gallery-image-${index}`);

    // Store image parent element.
    const imageParentElement = image.parentElement;

    // Move image node from grid to modal.
    moveImageToModal(image);
  
   // Create a click listener on the overlay for the active image element.
    overlayWrapper.onclick = function () {
        // Return the image to its parent element.
         moveImageToGrid(imageParentElement);
    };
}

// Helper functions for moving the image around and toggling the overlay.

function moveImageToModal(image) {
    // Show the overlay.
    overlayWrapper.classList.add("overlay--active");

    overlayContent.append(image);
}

function moveImageToGrid(imageParentElement) {
    imageParentElement.append(overlayContent.querySelector("img"));
  
    // Hide the overlay.
    overlayWrapper.classList.remove("overlay--active");
}
</code></pre>
</div>

On card click, we move the image element from the grid markup into the overlay, leaving the container node empty. Visually, we are applying `background-image` CSS to the empty container to create an illusion that the image is still there. We could have achieved the same effect with the duplicated image element with the optimal loading strategy, but I’ve chosen this approach for simplicity. 

We are also setting the overlay `onclick` event, which moves the image back into its `origin` container, and are also toggling the visibility CSS class on the overlay element.

It’s important to note that we are moving the image element from the grid HTML element into the overlay HTML element, so we have the same DOM node in the grid and the overlay. We can refer to the image as a **“Shared Element”**.

### Adding A Simple Crossfade Transition

Now that we have finished setting up the markup, basic styles, and JavaScript functionality, we are going to create our first state transition using the Shared Element Transitions API!

Let’s go into our `toggleImageView` function. First, we need to create a transition using the global `createDocumentTransition` function. And then, we just need to pass the callback function that updates the DOM to the `start` function:

<div class="break-out">

<pre><code class="language-javascript">// This function is now asynchronous.
async function toggleImageView(index) {
  const image = document.getElementById(`js-gallery-image-${index}`);
  const imageParentElement = image.parentElement;

  // Initialize transition from the API.
  const moveTransition = document.createDocumentTransition();

  // moveImageToTarget function is now called by the API "start" function.
  await moveTransition.start(() =&gt; moveImageToModal(image));

  // Create a click listener on the overlay for the active image element.
  overlayWrapper.onclick = async function () {
    // Initialize transition from the API.
    const moveTransition = document.createDocumentTransition();

    // moveImageToContainer function is now called by the API "start" function.
    await moveTransition.start(() =&gt; moveImageToGrid(imageParentElement));
  };
}
</code></pre>
</div>

Let’s look at our example with the Shared Element Transitions API included.

{{< codepen height="480" theme_id="light" slug_hash="yLjgmJN" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image gallery - crossfade (2) [forked]](https://codepen.io/smashingmag/pen/yLjgmJN) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{< vimeo 750308482 >}}

By changing just a few lines of code and calling our DOM update functions via the API, we got this neat little **crossfade animation** right out of the box. **All we had to do was to make sure that the DOM updated and called the required function.**

When we call the `start` function, the **API takes the** **outgoing screenshot of the page state** and performs the DOM update. When the update completes, the second, **incoming** **image** is captured**.** It’s important to point out that **what we see during the transition are screenshots of the elements, not the actual DOM elements.** That way, we can avoid any potential accessibility and usability issues during the transition.

**By default, Shared Element Transitions API will perform a crossfade animation** between these outgoing (fade-out) and incoming (fade-in) screenshots. This comes in handy as the browser ensures that both states are available for the entire animation duration, so we can focus more on customizing it!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/425e454f-c9a2-4c13-833e-ac7cfc5a89b0/1-ui-animations-shared-element-transitions-api-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/425e454f-c9a2-4c13-833e-ac7cfc5a89b0/1-ui-animations-shared-element-transitions-api-part1.png" width="800" height="450" sizes="100vw" caption="Shared Element Transitions API crossfade animation between the two UI states. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/425e454f-c9a2-4c13-833e-ac7cfc5a89b0/1-ui-animations-shared-element-transitions-api-part1.png'>Large preview</a>)" alt="Shared Element Transitions API crossfade animation between the two UI states" >}}

Although this animation looks alright, it’s just a minor improvement. Currently, the API doesn’t really know that the image (shared element) that is being moved from the container to the overlay is the same element in their respective states. We need to instruct the browser to pay special attention to the image element when switching between states, so let’s do that!

### Creating A Shared Element Animation

With `page-transition-tag` **CSS property**, we can easily tell the browser to watch for the element in both outgoing and incoming images, **keep track of element’s size and position** that are changing between them, and apply the appropriate animation.

We also need to apply the `contain: paint` or `contain: layout` to the shared element. **This wasn’t required for the crossfade animations, as it’s only required for elements that will receive the** `page-transition-tag`. If you want to learn more about CSS containment, Rachel Andrew wrote a [very detailed article](https://www.smashingmagazine.com/2019/12/browsers-containment-css-contain-property/) explaining it.

<pre><code class="language-css">.gallery&#95;&#95;image--active {
  page-transition-tag: active-image;
}

.gallery&#95;&#95;image {
  contain: paint;
}
</code></pre>

Another important caveat is that `page-transition-tag` **has to be unique, and we can apply it to only one element during the duration of the animation**. This is why we apply it to the active image element right before the image is moved to the overlay and remove it when the image overlay is closed and the image is returned to its original position:

<div class="break-out">

<pre><code class="language-javascript">async function toggleImageView(index) {
   const image = document.getElementById(`js-gallery-image-${index}`);

  // Apply a CSS class that contains the page-transition-tag before animation starts.
  image.classList.add("gallery&#95;&#95;image--active");

  const imageParentElement = image.parentElement;

  const moveTransition = document.createDocumentTransition();
  await moveTransition.start(() =&gt; moveImageToModal(image));

  overlayWrapper.onclick = async function () {
    const moveTransition = document.createDocumentTransition();
    await moveTransition.start(() =&gt; moveImageToGrid(imageParentElement));
    
    // Remove the class which contains the page-transition-tag after the animation ends.
    image.classList.remove("gallery&#95;&#95;image--active");
  };
}
</code></pre>
</div>

Alternatively, we could have used JavaScript to toggle the `page-transition-tag` property inline on the element. However, it’s better to use the CSS class `toggle` to make use of media queries to apply the tag conditionally:
 

<pre><code class="language-javascript">// Applies page-transition-tag to the image.
image.style.pageTransitionTag = "active-image";

// Removes page-transition-tag from the image.
image.style.pageTransitionTag = "none";
</code></pre>

And that’s pretty much it! Let’s take a look at our example with the shared element applied:

{{< codepen height="480" theme_id="light" slug_hash="OJZWKaK" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image gallery - crossfade + shared element (3) [forked]](https://codepen.io/smashingmag/pen/OJZWKaK) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{< vimeo 750319015 >}}

It looks much better, doesn’t it? Again, with just a few additional lines of CSS and JavaScript, we managed to create this complex transition between the two states that would otherwise take us hours to create. 

We’ve **instructed the browser to watch for size and position changes between the UI states** by tagging our shared active image element with a unique id and applying special animation. This is the **default behavior for elements with the** `page-transition-tag` set. In the next few examples, we’ll learn how to customize animation properties other than opacity, position, and size.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/895adde5-dabe-4b3b-8e0c-9961d5848a4b/2-ui-animations-shared-element-transitions-api-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/895adde5-dabe-4b3b-8e0c-9961d5848a4b/2-ui-animations-shared-element-transitions-api-part1.png" width="800" height="450" sizes="100vw" caption="Shared Element Transitions API treats the image element as the same element between the states, applies special position and size animations meanwhile crossfading everything else. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/895adde5-dabe-4b3b-8e0c-9961d5848a4b/2-ui-animations-shared-element-transitions-api-part1.png'>Large preview</a>)" alt="Shared Element Transitions API treats the image element as the same element between the states, applies special position and size animations meanwhile crossfading everything else" >}}

### Customizing Animation Duration And Easing Function

We’ve created this complex transition with just a few lines of CSS and JavaScript, which turned out great. However, we expect to have more control over the animation properties like duration, easing function, delay, and so on to create even more elaborate animations or compose them for even greater effect.

**Shared Element Transitions API makes use of CSS `animation` properties** and we can use them to fully customize our state animation. But which CSS selectors to use for these outgoing and incoming states that the API is generating for us?

Shared Element Transition API introduces new **pseudo-elements** that are added to DOM when its animations are run. Jake Archibald explains the pseudo-element tree in his [Chrome developers article](https://developer.chrome.com/blog/shared-element-transitions-for-spas/#transitioning-multiple-elements). By default (in case of crossfade animation), we get the following tree of pseudo-elements:

<pre><code class="language-css">::page-transition
└─ ::page-transition-container(root)
   └─ ::page-transition-image-wrapper(root)
      ├─ ::page-transition-outgoing-image(root)
      └─ ::page-transition-incoming-image(root)
</code></pre>

These pseudo-elements may seem a bit confusing at first, so I’m including [WICG’s concise explanation](https://github.com/WICG/shared-element-transitions/blob/main/explainer.md) for these pseudo-elements and their general purpose:

<blockquote><ul><li><code>::page-transition</code> sits in a top-layer, over everything else on the page.</li><li><code>::page-transition-outgoing-image(root)</code> is a screenshot of the old state, and <code>::page-transition-incoming-image(root)</code> is a live representation of the new state. Both render as CSS replaced content.</li><li><code>::page-transition-container</code> animates size and position between the two states.</li><li><code>::page-transition-image-wrapper</code> provides blending isolation, so the two images can correctly cross-fade.</li><li><code>::page-transition-outgoing-image</code> and <code>::page-transition-incoming-image</code> are the visual states to cross-fade.</li></ul></blockquote>

For example, when we apply the `page-transition-tag: active-image`, its pseudo-elements are added to the tree:

<pre><code class="language-css">::page-transition
├─ ::page-transition-container(root)
│  └─ ::page-transition-image-wrapper(root)
│     ├─ ::page-transition-outgoing-image(root)
│     └─ ::page-transition-incoming-image(root)
└─ ::page-transition-container(active-image)
   └─ ::page-transition-image-wrapper(active-image)
      ├─ ::page-transition-outgoing-image(active-image)
      └─ ::page-transition-incoming-image(active-image)
</code></pre>

In our example, we want to modify both the crossfade (root) animation and the shared element animation. We can use the universal selector `*` with the pseudo-element to change animation properties for all available transition elements and target pseudo-elements for specific animation using the `page-transition-tag` value.

In this example, we are applying `400ms` duration for all animated elements with an `ease-in-out` easing function, and then override the `active-image` transition easing function and setting a custom `cubic-bezier` value:

<pre><code class="language-css">::page-transition-container(&#42;) {
  animation-duration: 400ms;
  animation-timing-function: ease-in-out;
}

::page-transition-container(active-image) {
  animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
}
</code></pre>
   
{{< codepen height="480" theme_id="light" slug_hash="gOzgVJV" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image gallery - custom animation (4) [forked]](https://codepen.io/smashingmag/pen/gOzgVJV) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{< vimeo 750305649 >}}

### Feature Detection And Fallbacks

We got slightly carried away and made this example unusable on browsers that don’t support the API, so let’s fix that. We need to add some feature checks and fallbacks to make sure that the website remains usable for all users.

**Feature detection in JavaScript** is as simple as checking if the `createDocumentTransition` function exists:

<pre><code class="language-javascript">const isSupported = "createDocumentTransition" in document;

if(isSupported) {
    /&#42; Shared element transitions API is supported &#42;/
} else {
    /&#42; Shared element transitions API is not supported &#42;/
}
</code></pre>

**In CSS**, we can use the `@supports` tag to apply styles based on feature support conditionally. This is useful when you want to provide a less ideal but still effective standard CSS transition or animation:

<pre><code class="language-css">@supports (page-transition-tag: none) {
    /&#42; Shared element transitions API is supported &#42;/
    /&#42; Use the Shared Element Transisitons API styles &#42;/
}

@supports not (page-transition-tag: none) {
    /&#42; Shared element transitions API is not supported &#42;/
    /&#42; Use a simple CSS animation if possible &#42;/
}
</code></pre>

If we need to support even older browsers, we can conditionally apply the CSS class using JavaScript:

<pre><code class="language-javascript">if("createDocumentTransition" in document) {
  document.documentElement.classList.add("shared-elements-api");
}
</code></pre>

<pre><code class="language-javascript">html.shared-elements-api {
    /&#42; Shared element transitions API is supported &#42;/
}

html:not(.shared-elements-api) {
    /&#42; Shared element transitions API is not supported &#42;/
}
</code></pre>

We can check out our example on a browser that doesn’t support the API and see that the function still runs but is not animated.

{{< codepen height="480" theme_id="light" slug_hash="yLjMBLb" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image gallery - fallback (5) [forked]](https://codepen.io/smashingmag/pen/yLjMBLb) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35e3402b-bc94-403b-9c40-a8f479345719/3-ui-animations-shared-element-transitions-api-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35e3402b-bc94-403b-9c40-a8f479345719/3-ui-animations-shared-element-transitions-api-part1.png" width="800" height="536" sizes="100vw" caption="In these examples, I’m using CSS <code>@supports</code> query to toggle the banner visibility for unsupported browsers. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/35e3402b-bc94-403b-9c40-a8f479345719/3-ui-animations-shared-element-transitions-api-part1.png'>Large preview</a>)" alt="Examples where CSS @supports query is used to toggle the banner visibility for unsupported browsers" >}}

### Accessible Animations

It’s important to be aware of accessibility requirements when working with animations. Some people prefer [browsing the web with reduced motion](https://www.w3.org/WAI/WCAG21/Understanding/animation-from-interactions.html), so we must either remove an animation or provide a more suitable alternative. This can be easily done with a widely supported [prefers-reduced-motion](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion) media query.

The following code snippet turns off animations for all elements using the Shared Element Transitions API. This is a shotgun solution, and we need to ensure that DOM updates smoothly and remains usable even with the animations turned off:
 

<pre><code class="language-css">@media (prefers-reduced-motion) {
    /&#42; Turn off all animations &#42;/
    ::page-transition-container(&#42;),
    ::page-transition-outgoing-image(&#42;),
    ::page-transition-incoming-image(&#42;) {
        animation: none !important;
    }

    /&#42; Or, better yet, create accessible alternatives for these animations  &#42;/
}
</code></pre>
  
{{< codepen height="480" theme_id="light" slug_hash="RwypbPz" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Image gallery -completed (6) [forked]](https://codepen.io/smashingmag/pen/RwypbPz) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{% ad-panel-leaderboard %}}

## To-do List With Custom Animations

Now that we got familiar with the basics of the Shared Element Transitions API, we can move on to more complex examples and focus on composing animations and utilizing CSS `animation` properties and `@keyframe` to fully customize the animations.

Let’s create an interactive to-do list with 3 column containers: tasks in progress, completed tasks, and won’t-do tasks. We’ll use a similar approach as before and customize the animation to make the motion more natural and bouncier. Clicked item will subtly scale up as it leaves the parent container and will scale back down and slightly bounce when it moves to a target container. The remaining to-do list elements should also be animated smoothly to move over to the empty space.

{{< vimeo 750325434 >}}

### Starting Markup, Styles And JavaScript

We’ll use a very similar approach with moving elements around as in the previous example, so we’ll start with the Shared Element API already implemented with a default crossfade animation. Check out the following CodePen for more details.

{{< codepen height="480" theme_id="light" slug_hash="qBYrWbQ" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [To-do list - shared element transitions API (1) [forked]](https://codepen.io/smashingmag/pen/qBYrWbQ) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{< vimeo 750326591 >}}

Let’s dive right into the JavaScript code. We have a similar setup here as in the previous example. The only difference is that we can have two possible target containers for our items in the to-do list: the second (“Done”) or the third column (“Won’t-do”).

<pre><code class="language-javascript">async function moveCard(isDone) {
  // Select the active card. 
  const card = this.window.event.target.closest("li");

  // Get the target list id.
  const destination = document.getElementById(
    `js-list-${isDone ? "done" : "not-done"}`
  );

  //We'll use this class to hide the item controls while the animation is running.
  card.classList.add("card-moving");

  if (document.createDocumentTransition) {
    const moveTransition = document.createDocumentTransition();

    // Run animation.
    await moveTransition.start(() =&gt; destination.appendChild(card));
  } else {
    // Fallback.
    destination.appendChild(card);
  }
}
</code></pre>

Notice how the **Shared Element Transitions API freezes rendering, and we cannot interact with any other element** on the page while the animation is running. This is an important limitation to keep in mind, so it’s best to **avoid creating lengthy animations** that might harm usability and annoy users.

### Creating Shared Element Transition

Let’s start by adding `page-transition-tag` values to our card elements and setting up a basic position animation.

We’ll use two different sets of `page-transition-tag` values for this example:

- `card-active`: for an element that is currently being moved to another column. We’ll apply this tag right before the animation runs and remove it once it ends;
- `card-${index + 1}`: for other elements which are being moved within the first column to fill the empty space left by an animated card. They’ll have a unique tag based on their index.

<div class="break-out">

<pre><code class="language-javascript">// Assign unique page-transition-tag values to all task cards.
// We could have also done this manually in CSS by targeting :nth-child().
const allCards = document.querySelectorAll(".col:not(.col-complete) li");
allCards.forEach(
    (c, index) =&gt; (c.style.pageTransitionTag = `card-${index + 1}`)
);

async function moveCard(isDone) {
  const card = this.window.event.target.closest("li");
  const destination = document.getElementById(
    `js-list-${isDone ? "done" : "not-done"}`
  );

  //We'll use this class to hide the item controls while the animation is running.
  card.classList.add("card-moving");

  if (document.createDocumentTransition) {
    // Replace the item tag with an active (moving) element tag.
    card.style.pageTransitionTag = "card-active";

    const moveTransition = document.createDocumentTransition();
    await moveTransition.start(() =&gt; destination.appendChild(card));

    // Remove the tag after the animation ends.
    card.style.pageTransitionTag = "none";
  } else {
    destination.appendChild(card);
  }
}
</code></pre>
</div>

Of course, we also need to add a `contain` property to our cards which are list elements in our example. Without the property, the animation wouldn’t break, but it would fall back to the default crossfade animation.

**Note:** *In the future, this behavior might change, and the DOM update will occur without the animation.*

<pre><code class="language-css">li {
  contain: paint;
}
</code></pre>

And, just like that, we have a really nice position animation set up for our card elements. Notice how we are doing nothing more than just toggling `page-transition-tag` values and applying the `contain: paint` value in our CSS, and we’re getting all these delightful animations.

{{< codepen height="480" theme_id="light" slug_hash="YzLZKpo" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [To-do list - with shared element (2) [forked]](https://codepen.io/smashingmag/pen/YzLZKpo) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{< vimeo 750328964 >}}

This animation looks alright, but it feels somewhat rigid in this example. What gives? Sometimes the animation will look impressive right out of the box, like in the previous example. Other times, however, it will require some tuning. It usually depends on the motion, animation type, target look and feel, and purpose of the animation.

### Creating A Scaling And Bouncing Animation

We can take full advantage of CSS `animation` properties and create our custom keyframes for animation pseudo-elements to achieve the bouncing effect.

First, we’ll slightly increase the `animation-duration` value of the position animation. Even though `::page-transition-container` animates the size and position, we are using its direct child `::page-transition-image-wrapper` for scaling animation, so we don’t override the default positioning and size animation. We are also slightly delaying the scale animation just to make it flow better. 

And finally, we are adjusting the `animation-duration` value for all elements so everything remains in sync, and we are applying a custom `cubic-bezier` timing function to achieve the final bouncing effect:

<div class="break-out">

<pre><code class="language-css">/&#42; We are applying contain property on all browsers (regardless of property support) to avoid differences in rendering and introducing bugs &#42;/
li {
  contain: paint;
}

@supports (page-transition-tag: none) {
  ::page-transition-container(card-active) {
    animation-duration: 0.3s;
  }

  ::page-transition-image-wrapper(card-active) {
    animation: popIn 0.3s cubic-bezier(0.64, 0.57, 0.67, 2) 0.1s;
  }
}

@keyframes popIn {
  from {
    transform: scale(1.3);
  }
  to {
    transform: scale(1);
  }
}
</code></pre>
</div>

With just a few minor tweaks and a custom animation keyframe definition, we’ve created a delightful and whimsical animation to make our to-do example a bit more exciting.

{{< codepen height="480" theme_id="light" slug_hash="YzLZKZm" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [To-do list - jumping &amp; bouncing animation (3) [forked]](https://codepen.io/smashingmag/pen/YzLZKZm) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{< vimeo 750325434 >}}

## Image Carousel With Custom Crossfade Animation

Let’s move on to a simpler example in which we’ll keep the focus on creating custom animation keyframes for both outgoing and incoming images.

We’ll create a crossfading image carousel. This is the first idea that popped into my mind when I saw the [Shared Element Transitions API announcement video](https://www.youtube.com/watch?v=JCJUPJ_zDQ4). Last year, I built a web app to help me [keep track of my music collection](https://adrians-music-collection.vercel.app/), which displays a details page for each release. On that page, I’ve added a simple image carousel that shows images of an album cover, booklet, and packaging.

I grabbed the source code and simplified it for this example. So, let’s create a slightly more elaborate crossfade animation for this element and play around with CSS filters.

**Photosensitivity warning:** *This example involves animating image brightness to mimic a lightning flash. If this applies to you, skip the following video and embedded examples. You can still follow the example and create custom crossfade transition by omitting <code>brightness</code> values from CSS.*

{{< vimeo 750338001 >}}

### Starting Markup, Styles And JavaScript

In this example, we’ll showcase how we can run Shared Element Transitions API to animate even the smallest changes, like changing a single HTML property. As a proof of concept, we’ll have a single image HTML element, and we’ll change its `src` property as active image changes:

<pre><code class="language-html">&lt;section class="gallery"&gt;
  &lt;img src="..." id="js-gallery" decoding="sync" loading="eager" /&gt;
  &lt;aside class="gallery&#95;&#95;controls"&gt;
    &lt;div class="gallery&#95;&#95;status"&gt;
      &lt;span id="js-gallery-index"&gt;1&lt;/span&gt; / 11
    &lt;/div&gt;
    &lt;button onclick="previousImage()" class="gallery&#95;&#95;button"&gt;
      &lt;!-- ... --&gt;
    &lt;/button&gt;
    &lt;button onclick="nextImage()" class="gallery&#95;&#95;button"&gt;
      &lt;!-- ... --&gt;
    &lt;/button&gt;
  &lt;/aside&gt;
&lt;/section&gt;
</code></pre>

Let’s check out our JavaScript file. Now we have two functions, namely for moving backwards and forwards in the image array. We are running the same crossfade animation on both functions, and everything else is pretty much the same as in previous examples:

<div class="break-out">

<pre><code class="language-javascript">// Let's store all images in an array.
const images = [ "https://path.to/image-1.jpg", "https://path.to/image-2.jpg", "..."];
let index = 0;

function previousImage() {
  index -= 1;

  if (index &lt; 0) {
    index = images.length - 1;
  }

  updateIndex();
  crossfadeElements();
}

function nextImage() {
  index += 1;

  if (index &gt;= images.length) {
    index = 0;
  }

  updateIndex();
  crossfadeElements();
}

// Util functions for animation, index update and image src update.

async function crossfadeElements() {
  if (document.createDocumentTransition) {
    const imageTransition = document.createDocumentTransition();
    await imageTransition.start(updateImage);
  } else {
    updateImage();
  }
}

function updateIndex() {
  const galleryIndex = document.getElementById("js-gallery-index");
  galleryIndex.textContent = index + 1;
}

function updateImage() {
  const gallery = document.getElementById("js-gallery");
  gallery.src = images[index];
}
</code></pre>
</div>

We’ll start with default crossfade animation, so we can focus more on the CSS and customizing animation properties.

{{< codepen height="480" theme_id="light" slug_hash="YzLZzVN" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Crossfade image carousel - setup (1) [forked]](https://codepen.io/smashingmag/pen/YzLZzVN) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{< vimeo 750343664 >}}

### Applying Custom Keyframes

Let’s make this crossfade animation a bit more elaborate by playing around with custom animation keyframes. We are creating a crossfade animation that imitates a lightning flash.

Let’s create the following keyframes:

- `fadeOut`: the current image will become blurrier and increase in brightness as its opacity value animates from `1` to `0`;
- `fadeIn`: the next image will become less blurry and decrease in brightness as its opacity value animates from `0` to `1`.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04aebbec-3cb1-4143-a742-cf1dd971d517/4-ui-animations-shared-element-transitions-api-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04aebbec-3cb1-4143-a742-cf1dd971d517/4-ui-animations-shared-element-transitions-api-part1.png" width="800" height="632" sizes="100vw" caption="We’ll use CSS filters to animate the blur and brightness of the outgoing and incoming images as they fade out and fade in, respectively. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/04aebbec-3cb1-4143-a742-cf1dd971d517/4-ui-animations-shared-element-transitions-api-part1.png'>Large preview</a>)" alt="Visualization of CSS filters to animate the blur and brightness of the outgoing and incoming images" >}}

<pre><code class="language-css">@keyframes fadeOut {
    from {
        filter: blur(0px) brightness(1) opacity(1);
    }
    to {
        filter: blur(6px) brightness(8) opacity(0);
    }
}

@keyframes fadeIn {
    from {
        filter: blur(6px) brightness(8) opacity(0);
    }
    to {
        filter: blur(0px) brightness(1) opacity(1);
    }
}
</code></pre>

Now, all we have to do is assign the exit animation to the outgoing image pseudo-element and the entry animation to the incoming image pseudo-element. We can set a `page-transition-tag` directly to the HTML image element as it’s the only element that will perform this animation:

<div class="break-out">

<pre><code class="language-css">/&#42; We are applying contain property on all browsers (regardless of property support) to avoid differences in rendering and introducing bugs &#42;/
.gallery img {
    contain: paint;
}

@supports (page-transition-tag: supports-tag) {
    .gallery img {
        page-transition-tag: gallery-image;
    }

    ::page-transition-outgoing-image(gallery-image) {
        animation: fadeOut 0.4s ease-in both;
    }

    ::page-transition-incoming-image(gallery-image) {
        animation: fadeIn 0.4s ease-out 0.15s both;
    }
}
</code></pre>
</div>

Even the seemingly simple crossfade animations can look cool, don’t you think? I think this particular animation fits really nicely with the dark theme we have in the example.

{{< codepen height="480" theme_id="light" slug_hash="gOzbZXB" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Crossfade image carousel - completed (2) [forked]](https://codepen.io/smashingmag/pen/gOzbZXB) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{< vimeo 750338001 >}}

{{% ad-panel-leaderboard %}}

## Elaborate Add-to-cart Animation

In our final example, we’ll build the project we introduced in the very first video in this article. We finally get to build a neat add-to-cart animation!

In our previous examples, we ran a single custom animation on a single element. In this example, we’ll create two animations that run one after another. First, the click event will activate the dot that moves to the cart icon, and then the cart counter value change will be animated.

Regardless of animation complexity, Shared Element Transitions API streamlines the whole process and hands us complete control over the look and feel of the animation.

{{< vimeo 750303184 >}}

### Starting Markup, Styles And JavaScript

As in the previous examples, we’ll start with a basic markup and style setup and a basic crossfade animation:

<div class="break-out">

<pre><code class="language-javascript">// Select static page elements and initialize the counter.
const counterElement = document.getElementById("js-shopping-bag-counter");
let counter = 0;

async function addToCart() {
    const dot = createCartDot();
    const parent = this.window.event.target.closest("button");

    // Set the dot element to its starting position in a button.
    parent.append(dot);

    // Dot transition.
    if (document.createDocumentTransition) {
        const moveTransition = document.createDocumentTransition();
        // Move the dot to the cart icon.
        await moveTransition.start(() =&gt; moveDotToTarget(dot));
    }

    // Remove the dot after the animation completes.
    dot.remove();

    // Counter transition.
    if (document.createDocumentTransition) {
        const counterTransition = document.createDocumentTransition();
        await counterTransition.start(() =&gt; incrementCounter(counterElement));
    } else {
        incrementCounter();
    }
}

// Util functions for creating the dot element, moving the dot to target, and incrementing the counter.

function moveDotToTarget(dot) {
    const target = document.getElementById("js-shopping-bag-target");
    target.append(dot);
}

function incrementCounter() {
    counter += 1;
    counterElement.innerText = counter;
}

function createCartDot() {
    const dot = document.createElement("div");
    dot.classList.add("product&#95;&#95;dot");
    return dot;
}
</code></pre>
</div>

{{< codepen height="480" theme_id="light" slug_hash="eYrvYXm" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Add to cart animation - starting code (1) [forked]](https://codepen.io/smashingmag/pen/eYrvYXm) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

### Creating Composed Animations

First, we need to toggle a `page-transition-tag` value for our dynamic `dot` element and the `cart` element in their respective transition animations:

<div class="break-out">

<pre><code class="language-javascript">async function addToCart() {
   /&#42; ... &#42;/

  if (document.createDocumentTransition) {
    const moveTransition = document.createDocumentTransition();
    await moveTransition.start(() =&gt; moveDotToTarget(dot));
    dot.style.pageTransitionTag = "none";
  }

  dot.remove();

  if (document.createDocumentTransition) {
    counterElement.style.pageTransitionTag = "cart-counter";
    const counterTransition = document.createDocumentTransition();
    await counterTransition.start(() =&gt; incrementCounter(counterElement));
    counterElement.style.pageTransitionTag = "none";
  } else {
    incrementCounter();
  }
}

/&#42; ... &#42;/

function createCartDot() {
  const dot = document.createElement("div");
  dot.classList.add("product&#95;&#95;dot");
  dot.style.pageTransitionTag = "cart-dot";

  return dot;
}
</code></pre>
</div>

Next, we’ll customize both animations with CSS. For the `dot` animation, we’ll change its duration and timing function, and for `cart-counter`, we’ll add a slight vertical movement to a standard crossfade animation.

Notice how the `dot` element doesn’t have animations or CSS properties for changing dimensions. Its dimensions respond to the parent container. Its initial position is in the button container, and then it is moved to a smaller `cart` icon container, which is located behind the counter. Shared Elements API understands how element position and dimensions change during the animation and gives us this elegant transition animation right out of the box!

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33d27692-b13e-4d7f-9c97-e0c9775b51f0/5-ui-animations-shared-element-transitions-api-part1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33d27692-b13e-4d7f-9c97-e0c9775b51f0/5-ui-animations-shared-element-transitions-api-part1.png" width="800" height="666" sizes="100vw" caption="Our temporary <code>dot</code> element responds to container dimensions and the API detects this change in dimensions and positions and provides a smooth transition out of the box. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/33d27692-b13e-4d7f-9c97-e0c9775b51f0/5-ui-animations-shared-element-transitions-api-part1.png'>Large preview</a>)" alt="A temporary dot element responds to container dimensions and the API detects this change in dimensions and positions and provides a smooth transition out of the box" >}}

<div class="break-out">

<pre><code class="language-css">/&#42; We are applying contain property on all browsers (regardless of property support) to avoid differences in rendering and introducing bugs &#42;/
.product&#95;&#95;dot {
  contain: paint;
}

.shopping-bag&#95;&#95;counter span {
  contain: paint;
}

@supports (page-transition-tag: supports-tag) {
  ::page-transition-container(cart-dot) {
    animation-duration: 0.7s;
    animation-timing-function: ease-in;
  }

  ::page-transition-outgoing-image(cart-counter) {
    animation: toDown 0.3s cubic-bezier(0.4, 0, 1, 1) both;
  }

  ::page-transition-incoming-image(cart-counter) {
    animation: fromUp 0.3s cubic-bezier(0, 0, 0.2, 1) 0.3s both;
  }
}

@keyframes toDown {
  from {
    transform: translateY(0);
    opacity: 1;
  }
  to {
    transform: translateY(4px);
    opacity: 0;
  }
}

@keyframes fromUp {
  from {
    transform: translateY(-3px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}
</code></pre>
</div>

And that is it! It amazes me every time how elaborate these animations can turn out with so few lines of additional code, all thanks to Shared Element Transitions API. Notice that the `header` element with the `cart` icon is fixed, so it sticks to the top, and our standard animation setup works like a charm, regardless!

{{< codepen height="480" theme_id="light" slug_hash="vYjxEOR" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Add to cart animation - completed (2) [forked]](https://codepen.io/smashingmag/pen/vYjxEOR) by <a href="https://codepen.io/AdrianBece">Adrian Bece</a>.{{< /codepen >}}

{{< vimeo 750303184 >}}

## Conclusion

When done correctly, animations can [breathe life into any project](http://species-in-pieces.com/) and offer a [more delightful and memorable experience](https://teatrlalka.pl/en) to users. With the upcoming Shared Element Transitions API, creating complex UI state transition animations has never been easier, but we still need to be careful how we use and implement animations.

This simplicity can give way to bad practices, such as not using animations correctly, creating slow or repetitive animations, creating needlessly complex animations, and so on. It’s important to [learn best practices for animations](https://www.designbetter.co/animation-handbook) and on the web so we can effectively utilize this API to create truly amazing and accessible experiences or even consult with the designer if we are unsure on how to proceed.

In the next article, we’ll explore the API’s potential when it comes to transition between different pages in Single Page Apps (SPA) and the upcoming Cross-document same-origin transitions, which are yet to be implemented.

I am excited to see what the [dev community will build](https://codepen.io/jh3y/pen/YzaQezW) using this awesome new feature. Feel free to reach out on [Twitter](https://twitter.com/AdrianBeceDev) or [LinkedIn](https://www.linkedin.com/in/adrianbece/) if you have any questions or if you built something amazing using this API. 

Go ahead and build something awesome!

*Many thanks to [Jake Archibald](https://twitter.com/jaffathecake) for reviewing this article for technical accuracy.*

### References

- [Shared Element Transitions](https://github.com/WICG/shared-element-transitions/blob/main/explainer.md), WICG
- “[Smooth And Simple Page Transitions With The Shared Element Transition API](https://developer.chrome.com/blog/shared-element-transitions-for-spas/)”, Jake Archibald
- [Shared Element Transitions API Twitter thread](https://twitter.com/jh3yy/status/1550675304280035328), Jhey
- [CSS Shared Element Transitions Module Level 1](https://drafts.csswg.org/css-shared-element-transitions-1/), W3C

{{< signature "vf, yk, il" >}}

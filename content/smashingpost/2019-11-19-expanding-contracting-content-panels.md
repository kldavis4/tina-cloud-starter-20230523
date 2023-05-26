---
title: 'Make Your Own Expanding And Contracting Content Panels'
slug: expanding-contracting-content-panels
author: ben-frain
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1a010c8f-782d-4e35-a681-56ab9b3c4cda/expanding-contracting-content-panels-sharing-image.png
date: 2019-11-19T11:00:00.000Z
summary: >-
  In UI/UX, a common pattern that’s needed time and again is that of a simple animated opening and closing panel, or 'drawer'. You don’t need a library to make these. With some basic HTML/CSS and JavaScript, we’re going to learn how to do it ourselves.
description: >-
  In UI/UX, a common pattern that’s needed time and again is that of a simple animated opening and closing panel, or 'drawer'. You don’t need a library to make these. With some basic HTML/CSS and JavaScript, we’re going to learn how to do it ourselves.
categories:
  - UX
  - UI
  - JavaScript
  - CSS
---
We’ve called them an 'opening and closing panel' so far, but they are also described as expansion panels, or more simply, expanding panels.

To clarify exactly what we’re talking about, head on over to this example on CodePen:

{{< codepen height="480" theme_id="light" slug_hash="VwwqdWa" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}<a href="https://codepen.io/smashingmag/pen/VwwqdWa">Easy show/hide drawer (Multiples)</a> by <a href="https://codepen.io/benfrain">Ben Frain</a> on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

That is what we’ll be building in this short tutorial.

From a functionality point of view, there are a few ways to achieve the animated open and close that we are looking for. Each approach with its own benefits and trade-offs. I'm going to share the details of my 'go-to' method in detail in this article. Let’s consider possible approaches first.

## Approaches

There are variations on these techniques, but broadly speaking, the approaches fall into one of three categories:

1. Animate/transition the `height` or `max-height` of content.
2. Use `transform: translateY` to move elements into a new position, giving the illusion of a panel closing and then re-render the DOM once the transform is complete with the elements in their finishing position.
3. Use a library that does some combination/variation of 1 or 2!

{{% feature-panel %}} 

### Considerations Of Each Approach

From a performance perspective, using a transform is more effective than animating or transitioning the height/max-height. With a transform, the moving elements are rasterized and get shifted around by the GPU. This is a cheap and easy operation for a GPU so performance tends to be much better.

The basic steps when using a transform approach are:

1. Get the height of the content to be collapsed.
2. Move the content and everything after by the height of the content to be collapsed using `transform: translateY(Xpx)`. Operate the transform with the transition of choice to give a pleasing visual effect.
3. Use JavaScript to listen to the `transitionend` event. When it fires, `display: none` the content and remove the transform and everything should be in the right place.

Doesn’t sound too bad, right?

However, there are a number of considerations with this technique so I tend to avoid it for casual implementations unless performance is absolutely crucial.

For example, with the `transform: translateY` approach you need to consider the `z-index` of the elements. By default, the elements that transform up are after the trigger element in the DOM and therefore appear on-top of the things before them when translated up.

You also need to consider how many things appear *after* the content you want to collapse in the DOM. If you don’t want a big hole in your layout, you might find it easier to use JavaScript to wrap everything you want to move in a container element and just move that. Manageable but we have just introduced more complexity! This is, however, the *kind* of approach I went for when moving players up and down in [In/Out](https://io.benfrain.com). You can see how that was done [here](https://github.com/benfrain/whosin/blob/master/ts/repositionSlat.ts).

For more casual needs, I tend to go with transitioning the `max-height` of the content. This approach doesn’t perform as well as a transform. The reason being that the browser is tweening the height of the collapsing element throughout the transition; that causes a lot of layout calculations which are not as cheap for the host computer.

However, this approach wins from a simplicity point of view. The pay-off of suffering the afore-mentioned computational hit is that the DOM re-flow takes care of the position and geometry of everything. We have very little in the way of calculations to write plus the JavaScript needed to pull it off well is comparatively simple.

### The Elephant In The Room: Details And Summary Elements

Those with an intimate knowledge of HTML’s elements will know there is a native HTML solution to this problem in the form of the `details` and `summary` elements. Here’s some example markup:

<div class="break-out">

<pre><code class="language-markup">&lt;details&gt;
    &lt;summary&gt;Click to open/close&lt;/summary&gt;
    Here is the content that is revealed when clicking the summary...
&lt;/details&gt;</code></pre>
</div>

By default, browsers provide a little disclosure triangle next to the summary element; click the summary and the contents below the summary is revealed.

Great, hey? Details even support the `toggle` event in JavaScript so you can do this kind of thing to perform different things based upon whether it is open or closed (don’t worry if that kind of JavaScript expression seems odd; we’ll get to that in more detail shortly):

<pre><code class="language-javascript">details.addEventListener("toggle", () => {
    details.open ? thisCoolThing() : thisOtherThing();
})</code></pre>

OK, I'm going to halt your excitement right there. The details and summary elements don’t animate. Not by default and it is not currently possible to get them animating/transitioning open and closed with additional CSS and JavaScript.

If you know otherwise, I’d love to be proved wrong.

Sadly, as we need an opening and closing aesthetic we’ll have to roll up our sleeves and do the best and most accessible job we can with the other tools at our disposal.

Right, with the depressing news out of the way, let’s get on with making this thing happen.

### Markup Pattern

The basic markup is going to look like this:

<div class="break-out">

<pre><code class="language-markup">&lt;div class="container"&gt;
    &lt;button type="button" class="trigger"&gt;Show/Hide content&lt;/button&gt;
    &lt;div class="content"&gt;
        All the content here
    &lt;/div&gt;
&lt;/div&gt;</code></pre>
</div>

We have an outer container to wrap the expander and the first element is the button which serves as a trigger to the action. Notice the type attribute in the button? I always include that as by default a button inside a form will perform a submit. If you find yourself wasting a couple of hours wondering why your form isn’t working and buttons are involved in your form; make sure you check the type attribute!

The next element after the button is the content drawer itself; everything you want to be hiding and showing.

To bring things to life, we will make use of CSS custom properties, CSS transitions, and a little JavaScript.

{{% ad-panel-leaderboard %}}

### Basic Logic

The basic logic is this:

1. Let the page load, measure the height of the content.
2. Set the height of the content onto the container as the value of a CSS Custom Property.
3. Immediately hide the content by adding an `aria-hidden: "true"` attribute to it. Using `aria-hidden` ensures assistive technology knows that content is hidden too.
4. Wire up the CSS so that the `max-height` of the content class is the value of the custom property.
5. Pressing our trigger button toggles the aria-hidden property from true to false which in turn toggles the `max-height` of the content between `0` and the height set in the custom property. A transition on that property provides the visual flair &mdash; adjust to taste!

<p><strong>Note:</strong> <em>Now, this would be a simple case of toggling a class or attribute if <code>max-height: auto</code> equalled the height of the content. Sadly it doesn't. Go and shout about that to the W3C <a href="https://github.com/w3c/csswg-drafts/issues/626">here</a>.</em></p>

Let’s have a look how that approach manifests in code. Numbered comments show the equivalent logic steps from above in code.

Here is the JavaScript:

<div class="break-out">

<pre><code class="language-javascript">// Get the containing element
const container = document.querySelector(".container");
// Get content
const content = document.querySelector(".content");
// 1. Get height of content you want to show/hide
const heightOfContent = content.getBoundingClientRect().height;
// Get the trigger element
const btn = document.querySelector(".trigger");

// 2. Set a CSS custom property with the height of content
container.style.setProperty("--containerHeight", `${heightOfContent}px`);

// Once height is read and set
setTimeout(e => {
    document.documentElement.classList.add("height-is-set");
    3. content.setAttribute("aria-hidden", "true");
}, 0);

btn.addEventListener("click", function(e) {
    container.setAttribute("data-drawer-showing", container.getAttribute("data-drawer-showing") === "true" ? "false" : "true");
    // 5. Toggle aria-hidden
    content.setAttribute("aria-hidden", content.getAttribute("aria-hidden") === "true" ? "false" : "true");
})</code></pre>
</div>

The CSS:

<pre><code class="language-css">.content {
  transition: max-height 0.2s;
  overflow: hidden;
}
.content[aria-hidden="true"] {
  max-height: 0;
}
// 4. Set height to value of custom property
.content[aria-hidden="false"] {
  max-height: var(--containerHeight, 1000px);
}</code></pre>

### Points Of Note

#### What about multiple drawers?

When you have a number of open-and-hide drawers on a page you’ll need to loop through them all as they will likely be differing sizes.

To handle that we will need to do a `querySelectorAll` to get all the containers and then re-run your setting of custom variables for each content inside a `forEach`.

#### That setTimeout

I have a `setTimeout` with `0` duration before setting the container to be hidden. This is arguably unneeded but I use it as a 'belt and braces' approach to ensure the page has rendered first so the heights for the content are available to be read.

#### Only fire this when the page is ready

If you have other stuff going on, you might choose to wrap your drawer code up in a function that gets initialised on page load. For example, suppose the drawer function was wrapped up in a function called `initDrawers` we could do this:

<pre><code class="language-javascript">window.addEventListener("load", initDrawers);</code></pre>

In fact, we will add that in shortly.

#### Additional data-\* attributes on the container

There is a data attribute on the outer container that also gets toggled. This is added in case there is anything that needs to change with the trigger or container as the drawer opens/closes. For example, perhaps we want to change the color of something or reveal or toggle an icon.

#### Default value on the custom property

There’s a default value set on the custom property in CSS of `1000px`. That’s the bit after the comma inside the value: `var(--containerHeight, 1000px)`. This means if the `--containerHeight` gets screwed up in some way, you should still have a decent transition. You can obviously set that to whatever is suitable to your use case.

{{% ad-panel-leaderboard %}}

### Why Not Just Use A Default Value Of 100000px?

Given that `max-height: auto` doesn’t transition, you may be wondering why you don’t just opt for a set height of a value greater than you would ever need. For example, 10000000px?

The problem with that approach is that it will always transition from that height. If your transition duration is set to 1 second, the transition will 'travel' 10000000px in a second. If your content is only 50px high, you’ll get quite a quick opening/closing effect!

#### Ternary operator for toggles

We’ve made use of a ternary operator a couple of times to toggle attributes. Some folks hate them but I, [and others](https://css-tricks.com/in-defense-of-the-ternary-statement/), love them. They might seem a bit weird and a little 'code golf' at first but once you get used to the syntax, I think they are a more straightforward read than a standard if/else.

For the uninitiated, a ternary operator is a condensed form of if/else. They are written so that the thing to check is first, then the `?` separates what to execute if the check is true, and then the `:` to distinguish what should run if the check if false.

<pre><code class="language-javascript">isThisTrue ? doYesCode() : doNoCode();</code></pre>

Our attribute toggles work by checking if an attribute is set to `"true"` and if so, set it to `"false"`, otherwise, set it to `"true"`.

#### What happens on page resize?

If a user resizes the browser window, there’s a high probability the heights of our content will change. Therefore you might want to re-run setting the height for containers in that scenario. Now we are considering such eventualities, it seems like a good time to refactor things a little.

We can make one function to set the heights and another function to deal with the interactions. Then add two listeners on the window; one for when the document loads, as mentioned above, and then another to listen for the resize event.

#### A little extra A11Y

It’s possible to add a little extra consideration for accessibility by making use of the `aria-expanded`, `aria-controls` and `aria-labelledby` attributes. This will give a better indication to assisted technology when the drawers have been opened/expanded. We add `aria-expanded="false"` to our button markup alongside `aria-controls="IDofcontent"`, where `IDofcontent` is the value of an id we add to the content container.

Then we use another ternary operator to toggle the `aria-expanded` attribute on click in the JavaScript.

## All Together

With the page load, multiple drawers, extra A11Y work and handling resize events, our JavaScript code looks like this:

<div class="break-out">

 <pre><code class="language-javascript">var containers;
function initDrawers() {
    // Get the containing elements
    containers = document.querySelectorAll(".container");
    setHeights();
    wireUpTriggers();
    window.addEventListener("resize", setHeights);
}

window.addEventListener("load", initDrawers);

function setHeights() {
    containers.forEach(container => {
        // Get content
        let content = container.querySelector(".content");
        content.removeAttribute("aria-hidden");
        // Height of content to show/hide
        let heightOfContent = content.getBoundingClientRect().height;
        // Set a CSS custom property with the height of content
        container.style.setProperty("--containerHeight", `${heightOfContent}px`);
        // Once height is read and set
        setTimeout(e => {
            container.classList.add("height-is-set");
            content.setAttribute("aria-hidden", "true");
        }, 0);
    });
}

function wireUpTriggers() {
    containers.forEach(container => {
        // Get each trigger element
        let btn = container.querySelector(".trigger");
        // Get content
        let content = container.querySelector(".content");
        btn.addEventListener("click", () => {
            btn.setAttribute("aria-expanded", btn.getAttribute("aria-expanded") === "false" ? "true" : "false");
            container.setAttribute(
                "data-drawer-showing",
                container.getAttribute("data-drawer-showing") === "true" ? "false" : "true"
            );
            content.setAttribute(
                "aria-hidden",
                content.getAttribute("aria-hidden") === "true" ? "false" : "true"
            );
        });
    });
}
</code></pre>
</div>

You can also play with it on CodePen over here:

{{< codepen height="480" theme_id="light" slug_hash="VwwqdWa" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}<a href="https://codepen.io/smashingmag/pen/VwwqdWa">Easy show/hide drawer (Multiples)</a> by <a href="https://codepen.io/benfrain">Ben Frain</a> on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Summary

It’s possible to go on for some time further refining and catering for more and more situations but the basic mechanics of creating a reliable opening and closing drawer for your content should now be within your reach. Hopefully, you are also aware of some of the hazards. The `details` element can’t be animated, `max-height: auto` doesn’t do what you hoped, you can’t reliably add a massive max-height value and expect all content panels to open as expected.

To re-iterate our approach here: measure the container, store it’s height as a CSS custom property, hide the content and then use a simple toggle to switch between `max-height` of 0 and the height you stored in the custom property.

It might not be the absolute best performing method but I have found for most situations it is perfectly adequate and benefits from being comparatively straightforward to implement.

{{< signature "dm, yk, il" >}}

---
title: 'Respecting Users’ Motion Preferences'
slug: respecting-users-motion-preferences
author: michelle-barker
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/df53065e-5b99-4a67-ad0c-2cd67b07dc2a/respecting-users-motion-preferences.jpg
date: 2021-10-21T10:30:00.000Z
summary: >-
  The `prefers-reduced-motion` media query has excellent support in all modern browsers going back a couple of years. In this article, Michelle Barker explains why there’s no reason not to use it today to make your sites more accessible.
description: >-
  The `prefers-reduced-motion` media query has excellent support in all modern browsers going back a couple of years. In this article, Michelle Barker explains why there’s no reason not to use it today to make your sites more accessible.
categories:
  - CSS
  - JavaScript
  - Performance
  - Animation
---

When working with motion on the web, it’s important to consider that not everyone experiences it in the same way. What might feel smooth and slick to some might be annoying or distracting to others &mdash; or worse, induce feelings of sickness, or even cause seizures. Websites with **a lot of motion** might also have a higher impact on the battery life of mobile devices, or cause more data to be used (autoplaying videos, for instance, will require more of a user’s data than a static image). These are just some of the reasons why motion-heavy sites might not be desirable for all.

Most new operating systems enable the user to set their motion preferences in their system-level settings. The `prefers-reduced-motion` media query (part of the [Level 5 Media Queries](https://www.w3.org/TR/mediaqueries-5/#prefers-reduced-motion) specification) allows us to detect users’ system-level motion preferences, and apply CSS styles that respect that.

The two options for `prefers-reduced-motion` are `reduce` or `no-preference`. We can use it in the following way in our CSS to turn off an element’s animation if the user has explicitly set a **preference for reduced motion**:

<pre><code class="language-css">.some-element {
  animation: bounce 1200ms;
}

@media (prefers-reduced-motion: reduce) {
  .some-element {
    animation: none;
  }
}</code></pre>

Conversely, we could set the animation **only** if the user has no motion preference. This has the advantage of reducing the amount of code we need to write, and means it’s less likely we’ll forget to cater for users’ motion preferences:

<pre><code class="language-css">@media (prefers-reduced-motion: no-preference) {
  .some-element {
    animation: bounce 1200ms;
  }
}</code></pre>

An added advantage is that older browsers that don’t support `prefers-reduced-motion` will ignore the rule and only display our original, motion-free element.

## Which Rule?

Unlike `min-width` and `max-width` media queries, where the more-or-less established consensus is mobile-first (therefore favoring `min-width`), **there is no single “right” way** to write your reduced-motion styles. I tend to favor the second example (applying animations only if `prefers-reduced-motion: no-preference` evaluates true), for the reasons listed above. Tatiana Mac wrote [this excellent article](https://www.tatianamac.com/posts/prefers-reduced-motion/) which covers some of the approaches developers might consider taking, as well plenty of other great points, including key questions to ask when designing with motion on the web.

As always, **team communication** and **a consistent strategy** are key to ensuring all bases are covered when it comes to web accessibility.

{{% feature-panel %}}

## Practical Use: Applying `prefers-reduced-motion` To Scroll Behavior

`prefers-reduced-motion`  has plenty of applications beyond applying (or not applying) keyframe animations or transitions. One example is smooth scrolling. If we set `scroll-behaviour: smooth` on our `html` element, when a user clicks an in-page anchor link they will be smoothly scrolled to the appropriate position on the page (*currently not supported in Safari*):

<pre><code class="language-css">html {
  scroll-behavior: smooth;
}</code></pre>

Unfortunately, in CSS we don’t have much control over that behavior right now. If we have a long page of content, the page scrolls very fast, which can be a pretty unpleasant experience for someone with motion sensitivity. By wrapping it in a media query, we can **prevent that behavior** from being applied in cases where the user has a `reduced-motion` preference:

<pre><code class="language-css">@media (prefers-reduced-motion: no-preference) {
  html {
    scroll-behavior: smooth;
  }
}</code></pre>

## Catering For Motion Preferences In Javascript

Sometimes we need to apply motion in JavaScript rather than CSS. We can similarly detect a user’s motion preferences with JS, using `matchMedia`. Let’s see how we can conditionally implement smooth scroll behavior in our JS code:

<pre><code class="language-javascript">/* Set the media query */
const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)')

button.addEventListener('click', () =&gt; {
  /* If the media query matches, set scroll behavior variable to 'auto', 
  otherwise set it to 'smooth' */
  const behavior = prefersReducedMotion.matches ? 'auto' : 'smooth'

  /* When the button is clicked, the user will be scrolled to the top */
  window.scrollTo({
    x: 0,
    y: 0,
    behavior
  })
})</code></pre>

The same principle can be used to detect whether to implement motion-rich UIs with JS libraries &mdash; or even whether to load the libraries themselves.

In the following code snippet, the function returns early if the user prefers reduced motion, avoiding the unnecessary import of a large dependency &mdash; a performance win for the user. If they have no motion preference set, then we can [dynamically import](https://javascript.info/modules-dynamic-imports) the Greensock animation library and initialize our animations.

<pre><code class="language-javascript">const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)')

const loadGSAPAndInitAnimations = () =&gt; {
  /* If user prefers reduced motion, do nothing */
  if (prefersReducedMotion.matches) return
  
  /* Otherwise, import the GSAP module and initialize animations */
  import('gsap').then((object) =&gt; {
    const gsap = object.default
    /* Initialize animations with GSAP here */
  })
}

loadGSAPAndInitAnimations()</code></pre>

## `reduced-motion` Doesn’t Mean No Motion

When styling for reduced motion preferences, it’s important that we still provide the user with **meaningful and accessible indicators** of when an action has occurred. For instance, when switching off a distracting or motion-intensive hover state for users who prefer reduced motion, we must take care to provide a clear alternative style for when the user is hovering on the element.

The following demo shows an elaborate transition when the user hovers or focuses on a gallery item if they have no motion preference set. If they prefer reduced motion, the transition is more subtle, yet still clearly indicates the hover state:

{{< codepen height="480" theme_id="light" slug_hash="KKvMqaL" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Gallery with prefers-reduced-motion](https://codepen.io/smashingmag/pen/KKvMqaL) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

Reduced motion doesn’t necessarily mean removing *all* transforms from our webpage either. For instance, a button that has a small arrow icon that moves a few pixels on hover is unlikely to cause problems for someone who prefers a reduced-motion experience, and provides a more useful indicator of **a change of state** than color alone.

I sometimes see developers applying reduced motion styles in the following way, which eliminates all transitions and animations on all elements:

<pre><code class="language-css">@media screen and (prefers-reduced-motion: reduce) {
  * {
    animation: none !important;
    transition: none !important;
    scroll-behavior: auto !important;
  }
}</code></pre>

This is arguably better than ignoring users’ motion preferences, but doesn’t allow us to easily tailor elements to provide more subtle transitions when necessary.

In the following code snippet, we have a button that **grows in scale on hover**. We’re transitioning the colors and the scale, but users with a preference for reduced motion will get no transition at all:

<div class="break-out">

 <pre><code class="language-css">button {
  background-color: hotpink;
  transition: color 300ms, background-color 300ms, transform 500ms cubic-bezier(.44, .23, .47, 1.27);
}

button:hover,
button:focus {
  background-color: darkviolet;
  color: white;
  transform: scale(1.2);
}

@media screen and (prefers-reduced-motion: reduce) {
  &#42; {
    animation: none !important;
    transition: none !important;
    scroll-behavior: auto !important;
  }

  button {
    /&#42; Even though we would still like to transition the colors of our button, the following rule will have no effect &#42;/
    transition: color 200ms, background-color 200ms;
  }
        
  button:hover,
  button:focus {
    /&#42; Preventing the button scaling on hover &#42;/
    transform: scale(1);
  }
}</code></pre>
</div>

Check out [this demo](https://codepen.io/michellebarker/pen/GRvqZWN) to see the effect. This is perhaps not ideal, as the sudden color switch without a transition could feel more jarring than a transition of a couple of hundred milliseconds. This is one reason why, on the whole, I generally **prefer to style for reduced motion** on a case-by-case basis. 

If you’re interested, [this is the same demo refactored](https://codepen.io/michellebarker/pen/eYEzZQa) to allow for customizing the transition when necessary. It uses a custom property for the transition duration, which allows us to toggle the scale transition on and off without having to rewrite the whole declaration.

### When Removing Animation Is Better

Eric Bailey raises the point that “not every device that can access the web can also render animation, or render animation smoothly“ in his article, “[Revisiting prefers-reduced-motion, the reduced motion media query](https://css-tricks.com/revisiting-prefers-reduced-motion-the-reduced-motion-media-query/).” For devices with a low refresh rate, which can cause janky animations, it might in fact be **preferable to remove the animation**. The `update` media feature can be used to determine this:

<pre><code class="language-css">@media screen and
  (prefers-reduced-motion: reduce), 
  (update: slow) {
  * {
    animation-duration: 0.001ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.001ms !important;
  }
}</code></pre>

Be sure to read the full article for Eric’s recommendations, as he’s a first-rate person to follow in the field of accessibility.

{{% ad-panel-leaderboard %}}

## The Sum Of All Parts

It’s important to keep in mind the overall page design when focusing so tightly on component-level CSS. What might seem a fairly innocuous animation at the component level could have a far greater impact when it’s repeated throughout the page, and is one of many moving parts.

In Tatiana’s article, she suggests organizing animations (with `prefers-reduced-motion`) in a single CSS file, which can be loaded only if `(prefers-reduced-motion: no-preference)` evaluates true. Seeing the sum total of all our animations could have the added benefit of helping us **visualize the experience** of visiting the site as a whole, and tailor our reduced-motion styles accordingly.

## Explicit Motion Toggle

While `prefers-reduced-motion` is useful, it does have the drawback of only catering to users who are aware of the feature in their system settings. Plenty of users lack knowledge of this setting, while others might be using a borrowed computer, without access to system-level settings. Still, others might be happy with the motion for the vast majority of sites, but find sites with heavy use of motion hard to bear.

It can be annoying to have to adjust your system preferences just to visit one site. For these reasons, in some cases, it might be preferable to provide an explicit control on the site itself to **toggle motion on and off**. We can implement this with JS.

The following demo has several circles drifting around the background. The initial animation styles are determined by the user’s system preferences (with `prefers-reduced-motion`), however, the user has the ability to toggle motion on or off via a button. This adds a class to the `body`, which we can use to set styles depending on the selected preference. As a bonus, the **choice of motion preference** is also preserved in local storage &mdash; so it is “remembered” when the user next visits.

{{< codepen height="480" theme_id="light" slug_hash="porEQLB" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Reduced-motion toggle](https://codepen.io/smashingmag/pen/porEQLB) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

### Custom Properties

One feature in the demo is that the toggle sets a custom property, `--playState`, which we can use to play or pause animations. This could be especially handy if you need to **pause or play a number of animations** at once. First of all, we set the play state to `paused`:

<pre><code class="language-javascript">.circle {
  animation-play-state: var(--playState, paused);
}</code></pre>

If the user has set a preference for reduced motion in their system settings, we can set the play state to `running`:

<pre><code class="language-javascript">@media (prefers-reduced-motion: no-preference) {
  body {
    --playState: running;
  }
}</code></pre>

**Note:** *Setting this on the `body`, as opposed to the individual element, means the custom property can be inherited.*

When the user clicks the toggle, the custom property is updated on the `body`, which will toggle any instances where it is used:

<pre><code class="language-javascript">// This will pause all animations that use the `--playState` custom property
document.body.style.setProperty('--playState', 'paused')</code></pre>

This might not be the ideal solution in all cases, but one advantage is that the **animation simply pauses** when the user clicks the toggle, rather than jumping back to its initial state, which could be quite jarring.

Special thanks goes to [Scott O’Hara](https://twitter.com/scottohara) for his recommendations for improving the accessibility of the toggle. He made me aware that some screenreaders don’t announce the updated button text, which is changed when a user clicks the button, and suggested `role="switch"` on the button instead, with `aria-checked` toggled to `on` or `off` on click.

{{% ad-panel-leaderboard %}}

### Video Component

In some instances, toggling motion at the component level might be a better option. Take a webpage with an auto-playing video background. We should ensure the video doesn’t autoplay for users with a preference for reduced motion, but we should still provide a way for them to **play the video only *if* they choose**. (Some might argue we should avoid auto-playing videos full stop, but we don’t always win that battle!) Likewise, if a video is set to autoplay for users without a stated preference, we should also provide a way for them to pause the video.

This demo shows how we can **set the autoplay attribute** when the user has no stated motion preference, implementing a custom play/pause button to allow them to also toggle playback, regardless of preference:

{{< codepen height="480" theme_id="light" slug_hash="qBXNjqR" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Video with motion preference](https://codepen.io/smashingmag/pen/qBXNjqR) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

(I subsequently came upon [this post by Scott O‘Hara](https://codepen.io/scottohara/pen/bPOoEW), detailing this exact use case.)

### Using The `<picture>` Element

Chris Coyier wrote an [interesting article](https://css-tricks.com/reduced-motion-picture-technique-take-two/) combining a couple of techniques to load different media sources depending on the user’s motion preferences. This is pretty cool, as it means that for **users who prefer reduced motion**, the much larger GIF file won’t even be downloaded. The downside, as far as I can see, is that once the file is downloaded, there is no way for the user to switch back to the motion-free alternative.

I create a modified version of the demo which adds this option. (Switch on `reduced-motion` in your system preferences to see it in action.) Unfortunately, when toggling between the animated and motion-free options in Chrome, it appears the GIF file is downloaded afresh each time, which isn’t the case in other browsers:

{{< codepen height="480" theme_id="light" slug_hash="porbPXG" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Prefers Reduction Motion Technique PLUS! [forked]](https://codepen.io/smashingmag/pen/porbPXG) by <a href="https://codepen.io/michellebarker">Michelle Barker</a>.{{< /codepen >}}

Still, this technique seems like a more respectful way of displaying GIFs, which can be a source of frustration to users.

## Browser Support And Final Thoughts

`prefers-reduced-motion` has excellent support in all modern browsers going back a couple of years. As we’ve seen, by taking a reduced-motion-first approach, non-supporting browsers will simply get a `reduced-motion` fallback. There’s no reason not to use it today to make your sites more accessible.

Custom toggles most definitely have a place, and can **vastly improve the experience** for users who aren’t aware of this setting, or what it does. The downside for the user is inconsistency &mdash; if every developer is forced to come up with their own solution, the user needs to look for a motion toggle in a different place on every website.

It feels like the missing layer here is *browsers*. I’d love to see browsers implement `reduced-motion` toggles, somewhere easily accessible to the user, so that people know where to find it regardless of the site they’re browsing. It might encourage developers to spend more time ensuring motion accessibility, too.

### Related Resources

- [Level 5 Media Queries Specification](https://www.w3.org/TR/mediaqueries-5/#prefers-reduced-motion), World Wide Web Consortium (W3C)
- [`prefers-reduced-motion`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion), MDN Web Docs, Mozilla
- [Design With Reduced Motion For Motion Sensitivities](https://www.smashingmagazine.com/2020/09/design-reduced-motion-sensitivities/), Val Head, Smashing Magazine
- [Taking A No-Motion-First Approach To Animations](https://www.tatianamac.com/posts/prefers-reduced-motion/), Tatiana Mac
- [Reduced Motion Picture Technique, Take 2](https://css-tricks.com/reduced-motion-picture-technique-take-two/), Chris Coyier, CSS-Tricks
- [Revisiting `prefers-reduced-motion`, The Reduced Motion Media Query](https://css-tricks.com/revisiting-prefers-reduced-motion-the-reduced-motion-media-query/), Eric Bailey, CSS-Tricks
- [Reducing Motion To Improve Accessibility](https://www.a11ywithlindsey.com/blog/reducing-motion-improve-accessibility), Lindsey Kopacz

{{< signature "vf, yk, il" >}}

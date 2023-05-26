---
title: 'How To Build An Expandable Accessible Gallery'
slug: build-expandable-accessible-gallery
author: silvestar-bistrovic
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8271f985-0b13-4db2-afd6-3f6026272fc2/build-expandable-accessible-gallery.jpg
date: 2021-10-04T10:00:00.000Z
summary: >-
  In this article, we’ll be looking at how to set up a gallery that is expandable as well as accessible with a few tips and tricks along the way. Let’s get started!
description: >-
  In this article, we’ll be looking at how to set up a gallery that is expandable as well as accessible with a few tips and tricks along the way. Let’s get started!
categories:
  - Tools
  - CSS
  - CSS Grid
  - Accessibility
---

One of the use cases for using CSS Grid is to display a gallery of images, but a gallery on its own may not be that exciting. We could, for example, add a click effect to enlarge the image without affecting the grid to make it a little bit more fun. And of course, as to not exclude anybody from enjoying this feature, we should make it accessible, too.

In this article, I’ll explain how to build an accessible expandable gallery with a few tips and tricks along the way. Here’s how the final result looks like:

{{< codepen height="480" theme_id="light" slug_hash="PojxvJr" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [How to build accessible expandable gallery](https://codepen.io/smashingmag/pen/PojxvJr) by <a href="https://codepen.io/CiTA">Silvestar Bistrović</a>.{{< /codepen >}}

## The HTML

First, we are going to set the HTML structure. Of course, we could always do it in various ways, but let us use a list of images wrapped in buttons.

<pre><code class="language-html">&lt;ul class="js-favs"&gt;
  &lt;li&gt;
    &lt;button&gt;
      &lt;img src="/path/to/image" alt="" /&gt;
    &lt;/button&gt;
  &lt;/li&gt;
  ...
&lt;/ul&gt;</code></pre>

Now, to make the gallery accessible, we need to make some adjustments:

- Add the descriptive `alt` attribute to every image to help visually impaired people understand what is in the image;
- Use the `aria-expanded` attribute which informs assistive technologies if the image is expanded or not;
- Include `role="list"` to make sure assistive technologies announce the list because some screen readers might remove the list announcement. 
    
<blockquote>“It’s not just using <code>list-style: none</code>, but any CSS that would remove the bullet or number indicators of a list’s items will also remove the semantics.”<br /><br />&mdash; <a href="https://www.scottohara.me/blog/2019/01/12/lists-and-safari.html">“Fixing” Lists</a>, Scott O’Hara</blockquote>

Finally, let’s add a paragraph with helpful text on how to use the gallery, and wrap the whole code in a landmark (in this case, the `main` element).

<pre><code class="language-html">&lt;main&gt;
  &lt;p&gt;Use ESC to close larger picture.&lt;/p&gt;
  &lt;ul class="js-favs" role=”list”&gt;
    &lt;li&gt;
      &lt;button aria-expanded="false"&gt;
        &lt;img src="/path/to/image" alt="Description of the image." /&gt;
      &lt;/button&gt;
    &lt;/li&gt;
    ...
  &lt;/ul&gt;
&lt;/main&gt;</code></pre>

For the simplicity of the demo, I decided to use images wrapped with the `aria-expanded` attribute. A better solution might be to add only image tags and then use JavaScript to wrap these images in a button with the `aria-expanded` attribute. This may be considered as progressive enhancement since the expanding effect wouldn’t work without JavaScript anyway.

## The CSS

To define the grid layout, we could use CSS Grid. We’ll use `auto-fit` so that items can fit into the available space, but restrict themselves from shrinking under a certain width. This means that we’ll see a different number of items on different viewports without writing too many media queries.

<pre><code class="language-css">:root {
  --gap: 4px;
}

ul {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  grid-gap: var(--gap);
}

@media screen and (min-width: 640px) {
  ul {
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  }
}</code></pre>

To preserve the correct aspect ratio of the image, we could use the [`aspect-ratio` property](https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio). To reset the button style, we could add the `all: initial` declaration. We should also hide the overflow of the button. 

To make the image fit right into the button, we’ll use `object-fit: cover` declaration and set both `width` and `height` to `100%`:

<pre><code class="language-css">button {
  all: initial;
  display: block;
  width: 100%;
  aspect-ratio: 2/1;
  overflow: hidden;
  cursor: pointer;
}

img {
  height: 100%;
  width: 100%;
  object-fit: cover;
}</code></pre>

The expanding effect is done with the `scale` transformation. The transition is enabled by default, but if the user does not prefer transitions and animations, we can use the `prefers-reduced-motion` media query and set the `transition-duration` property to `0s`.

<pre><code class="language-css">:root {
  --duration-shrink: .5s;
  --duration-expand: .25s;
  --no-duration: 0s;
}

li {
  transition-property: transform, opacity;
  transition-timing-function: ease-in-out;
  transition-duration: var(--duration-expand);
}

li.is-zoomed {
  transition-duration: var(--duration-shrink);
}

@media (prefers-reduced-motion) {
  li,
  li.is-zoomed {    
    transition-duration: var(--no-duration);
  }
}</code></pre>

{{% feature-panel %}}

## The JavaScript

### Preparation

Before we make the element expandable, we need to prepare and calculate a few things.

First, we’ll need to get the duration of the transition by reading the CSS Custom Property `--duration-on`.

<pre><code class="language-javascript">let timeout = 0

// Get the transition timeout from CSS
const getTimeouts = () =&gt; {
  const durationOn = parseFloat(getComputedStyle(document.documentElement)
    .getPropertyValue('--duration-on'));
  
  timeout = parseFloat(durationOn) * 1000
}</code></pre>

Next, we’ll **set the data attributes** for the later calculation:

- the gap of the grid elements;
- the width of a single element;
- the number of items per row.

The first two are pretty straightforward. We could get the values from the computed CSS style.

To find the number of columns, we should iterate through each tile and compare the top position of each element. Once the top position changes, the item is in the new row, which gets us the number of items.

<pre><code class="language-javascript">// Set data attributes for calculations
const setDataAttrs = ($elems, $parent) =&gt; {
  // Get the top offset of the first element
  let top = getTop($elems[0])

  // Set grid gap from CSS
  const gridColumnGap = parseFloat(getComputedStyle(document.documentElement)
    .getPropertyValue('--gap'))
  $parent.setAttribute('data-gap', gridColumnGap)

  // Set grid item width from CSS
  const eStyle = getComputedStyle($elems[0])
  $parent.setAttribute('data-width', eStyle.width)

  // Iterate through grid items
  for (let i = 0; i &lt; $elems.length; i++) {
    const t = getTop($elems[i])

    // Check when top offset changes
    if (t != top) {
      // Set the number of columns and break stop the loop
      $parent.setAttribute('data-cols', i)
      break;
    }
  }
}</code></pre>

### Expanding Direction

To achieve the expandable effect, we should make some checks and calculations first. First, we should check if the item is in the last row and at the end of the row. If the item is in the last row, it should expand to the top. That means it should have the `transform-origin` property set to the `bottom` value.

**Important**: *If the element should expand to one direction, its `transform-origin` property should be set to an “opposite” value. Note that vertical and horizontal values should be combined.*

<pre><code class="language-javascript">// Set active item
const activateElem = ($elems, $parent, $elem, $button, lengthOfElems, i) =&gt; {
  // Get data attributes from parent
  const cols = parseInt($parent.getAttribute('data-cols'))
  const width = parseFloat($parent.getAttribute('data-width'))
  const gap = parseFloat($parent.getAttribute('data-gap'))

  // Calculate the number of rows
  const rows = Math.ceil(lengthOfElems / cols) - 1

  // Calculate if the item is in the last row
  const isLastRow = i + 1 &gt; rows * cols
  // Set default transform direction to top (expand down) 
  let transformOrigin = 'top'

  if (isLastRow) {
    // If the item is in the last row, set transform direction to bottom (expand up) 
    transformOrigin = 'bottom'
  }

  // Calculate if the item is the most right
  const isRight = (i + 1) % cols !== 0

  if (isRight) {
    // If the item is the most right, set transform direction to left (expand right) 
    transformOrigin += ' left'
  } else {
    // If the item is the most right, set transform direction to right (expand left) 
    transformOrigin += ' right'
  }

  $elem.style.transformOrigin = transformOrigin
}</code></pre>

### Expanding Effect

To enlarge the image without affecting the grid, we could use CSS transforms. In particular, we should use the scale transformation. I decided to make the image double in size, i.e. the factor is the ratio of the double width of the element plus grid-gap.

<pre><code class="language-javascript">// Calculate the scale coefficient
const scale = (width * 2 + gap) / width

// Set item CSS transform
$elem.style.transform = `scale(${scale})`</code></pre>

{{% ad-panel-leaderboard %}}

### Keyboard Support

Users who navigate sites by using a keyboard should be able to use the gallery. Going through the list works by default when using key <kbd>Tab</kbd>. Emulating the click works by default by pressing the <kbd>Enter</kbd> key while the item is focused. To enhance the default behavior, we should add support for <kbd>Esc</kbd> and the arrow keys.

Once we expand the item, pressing <kbd>Esc</kbd> should revert it to its standard size. We could do it by checking the code of the pressed key. The same goes for arrow keys, but the action is different. When pressing arrow keys, we want to get the previous or next sibling and then emulate the click on that element.

<pre><code class="language-javascript">// Set sibling as an active item
const activateSibling = ($sibling) =&gt; {
  // Find anchor
  const $siblingButton = $sibling.querySelector('button')

  // Unset global active element
  $activeElem = false

  // Focus and click on current
  $siblingButton.focus()
  $siblingButton.click()
}

// Set keyboard events
const setKeyboardEvents = () =&gt; {
  document.addEventListener('keydown', (e) =&gt; {
    // Take action only if global active element exists
    if ($activeElem) {
      // If key is “escape”, emulate the click on the global active element
      if (e.code === 'Escape') {
        $activeElem.click()
      }

      // If key is “left arrow”, activate the previous sibling
      if (e.code === 'ArrowLeft') {
        const $previousSibling = $activeElem.parentNode.previousElementSibling

        if($previousSibling) {
          activateSibling($previousSibling)
        }
      }

      // If key is “right arrow”, activate the next sibling
      if (e.code === 'ArrowRight') {
        const $nextSibling = $activeElem.parentNode.nextElementSibling

        if($nextSibling) {
          activateSibling($nextSibling)
        }
      }
    }
  })
}</code></pre>

### Toggling

To make the gallery element expanded, we should deactivate all other elements first. Then, if we click on the expanded element, it should revert to the standard size.  

<pre><code class="language-javascript">let $activeElem = false

// Deactivate grid items
const deactiveElems = ($elems, $parent, $currentElem, $button) =&gt; {
  // Unset parent class
  $parent.classList.remove('is-zoomed')

  for (let i = 0; i &lt; $elems.length; i++) {
    // Unset item class
    $elems[i].classList.remove('is-zoomed')
    // Unset item CSS transform
    $elems[i].style.transform = 'none'

    // Skip the rest if the item is the current item
    if ($elems[i] === $currentElem) {
      continue
    }
      
    // Unset item aria expanded if element exists
    if($button) {
      $button.setAttribute('aria-expanded', false)
    }
  }
}

// Set active item
const activateElem = ($elems, $parent, $elem, $button, lengthOfElems, i) =&gt; {
  ...
  
  // Reset all elements
  deactiveElems($elems, $parent, $elem, $button)

  if ($activeElem) {
    $activeElem = false
    return
  }

  $activeElem = $button
  
  ...
}


// Set click events on anchors
const setClicks = ($elems, $parent) =&gt; {
  $elems.forEach(($elem, i) =&gt; {
    // Find anchor
    const $button = $elem.querySelector('button')

    $button.addEventListener('click', (e) =&gt; {
      // Set active item on click
      activateElem($elems, $parent, $elem, $button, $elems.length, i)
    })
  })
}</code></pre>

### Z-index Issues

To prevent issues with `z-index` and stacking context, we should use the timeout to delay the transform. That is the same timeout that we calculated in the preparation phase.

<pre><code class="language-javascript">// Deactivate grid items
const deactiveElems = ($elems, $parent, $currentElem, $button) =&gt; {
  for (let i = 0; i &lt; $elems.length; i++) {
    ...

    // After a half of the timeout, reset CSS z-index to avoid overlay issues
    setTimeout(() =&gt; {
      $elems[i].style.zIndex = 0
    }, timeout)
  }
}

// Set active item
const activateElem = ($elems, $parent, $elem, $button, lengthOfElems, i) =&gt; {
  ...
  setTimeout(() =&gt; {
    // Set parent class
    $parent.classList.add('is-zoomed')
    // Set item class
    $elem.classList.add('is-zoomed')
    // Set item CSS transform
    $elem.style.transform = `scale(${scale})`
    // Set item aria expanded
    $button.setAttribute('aria-expanded', true)
    // Set global active item
    $activeElem = $button
  }, timeout)
}</code></pre>

{{% ad-panel-leaderboard %}}

### Viewport Resizing

If the viewport changes the size, we need to recalculate defaults because we defined a fluid grid that allows items to fill the available space and move from row to row.

<pre><code class="language-javascript">// Set resize events
const setResizeEvents = ($elems, $parent) =&gt; {
  window.addEventListener('resize', () =&gt; {
    // Set data attributes for calculations
    setDataAttrs($elems, $parent)
    // Deactivate grid items
    deactiveElems($elems, $parent)
  })
}</code></pre>

{{< vimeo id="613414984" caption="A preview of what the expandable accessible gallery demo can do. (<a href='https://codepen.io/smashingmag/pen/PojxvJr'>Try out on CodePen&nbsp;&rarr;</a>)" breakout="true" >}}

## A Word About Accessibility And Credits

I had no problems building this demo except with the accessibility part. I was not sure what to do and which aria attributes to use at first. Even after figuring out which attributes to use, I could not be 100% sure it was right. So the first step was to **test everything with a keyboard**. That was the easy part. Then I used the VoiceOver application (since I am using a Mac) to test how it works for visually impaired persons. It sounded good enough to me.

However, even after all that testing, I was still not 100% sure. So I decided to ask for help. I am a part of one Slack community for designers and developers ([BoagWorld](https://subscribe.boagworld.com/slack)), and I posted a question there. Fortunately, accessibility experts like [Todd Libby](https://www.smashingmagazine.com/author/todd-libby/) helped me test the demo on different devices and correct the code. I also asked [Manuel Matuzović](https://www.smashingmagazine.com/author/manuelmatuzovic/) for help and he helped me clean up the code.

I’m grateful to have the Internet and developer communities where we can all ask for help, get answers from professionals, and **solve problems together**. That is especially true with sensitive issues like accessibility. Accessibility is hard, and it does not take much to make it wrong. Less is more &mdash; at least it was in my case.

And finally, I wanted to share the greatest lesson:

<blockquote>“If you can use a native HTML element [<a href="https://www.w3.org/TR/using-aria/#bib-html51/">HTML51</a>] or attribute with the semantics and behavior you require <strong>already built-in</strong>, instead of re-purposing an element and adding an ARIA role, state or property to make it accessible, <strong>then do so</strong>.”<br /><br />&mdash; <a href="https://www.w3.org/TR/using-aria/#firstrule/">First Rule of ARIA Use</a>, W3C Working Draft 27 (Sept. 2018)</blockquote>

### Further Reading on Smashing Magazine

- [Accessible SVGs: Inclusiveness Beyond Patterns](https://www.smashingmagazine.com/2020/03/accessible-svgs-inclusiveness-beyond-patterns/), Carie Fisher
- [A Complete Guide To Accessible Front-End Components](https://www.smashingmagazine.com/2021/03/complete-guide-accessible-front-end-components/), Vitaly Friedman
- [Creating An Accessible Dialog From Scratch](https://www.smashingmagazine.com/2021/07/accessible-dialog-from-scratch/), Kitty Giraudel
- [When CSS Isn’t Enough: JavaScript Requirements For Accessible Components](https://www.smashingmagazine.com/2021/06/css-javascript-requirements-accessible-components/), Stephanie Eckles
- [Accessible SVGs: Perfect Patterns For Screen Reader Users](https://www.smashingmagazine.com/2021/05/accessible-svg-patterns-comparison/), Carie Fisher
- [How To Build An Accessible Front-End Application With Chakra UI And Nuxt.js](https://www.smashingmagazine.com/2020/07/accessible-front-end-application-chakra-ui-nuxtjs/), Kelvin Omereshone
- [Translating Design Wireframes Into Accessible HTML/CSS](https://www.smashingmagazine.com/2020/07/design-wireframes-accessible-html-css/), Harris Schneiderman

{{< signature "vf, yk, il" >}}

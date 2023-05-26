---
title: 'Enter The Dragon (Drop): Accessible List Reordering'
slug: dragon-drop-accessible-list-reordering
author: harris-schneiderman
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc95f06a-1a21-4535-b43c-6acffc89ff45/dragondrop-sticker.png
date: 2018-01-30T11:00:07+01:00
summary: >-
  There are tons of drag-and-drop list reordering modules out there today, very few of them are built with accessibility in mind. Dragon Drop seeks to fill this gap by providing means for all users to perform this somewhat common task.
description: >-
  There are tons of drag-and-drop list reordering modules out there today, very few of them are built with accessibility in mind. Dragon Drop seeks to fill this gap by providing means for all users to perform this somewhat common task.
categories:
  - Accessibility
  - Tools
  - JavaScript
  - Browsers
---
Over the years of being a web developer with a focus on accessibility, I have mostly dealt with widely-adopted, standardized UI components, well supported by assistive technologies (AT). For these types of widgets, there are concise [ARIA authoring practices](https://www.w3.org/TR/wai-aria-practices-1.1/) as well as great tools like [axe-core](https://www.axe-core.org/) that can be used to test web components for accessibility issues. Creating less common widgets, especially those that have no widely-adopted conventions for user interaction can be very tricky. 

One of the toughest challenges I've come across is the reorderable drag-and-drop list. While a reorderable list is a somewhat commonly used widget with intuitive conventions for mouse users, it's not clear how keyboard-only assistive technology users can perform this simple task. Due to the absence of supported ARIA attributes, Dragon Drop utilizes live regions to convey the information needed for all users to reorder a list.

## Live Regions

Live regions are HTML elements equipped with ARIA attributes that can be used to notify screen readers of content changes. They allow us to provide a completely customized screen reader announcement without having to move focus!  Live regions are great for real-time updates in remote parts of the page, status updates, and time-sensitive information. 

They're commonly used in chat logs, progress indicators, sports score updates, and weather alerts but should be used sparingly as they can easily create an overly-verbose experience for screen reader users. If you are new to live regions or just want to explore what they can do, check out my [live region playground](https://schne324.github.io/live-region-playground/), which allows you to configure your own custom live region. 

{{% feature-panel %}}

If you want to use live regions in your application, refer to the [Live Region module on npm](https://www.npmjs.com/package/live-region).

<pre><code class="language-html">&lt;div aria-live="assertive" role="log" aria-relevant="additions" aria-atomic="true">&lt;/div></code></pre>

### Why Use Live Regions?

In an ideal world, I would've been able to simply rely on the drag-and-drop ARIA attributes `aria-grabbed` and `aria-dropeffect`. However, in reality, the support for these attributes is rare, and where supported, the experience is confusing and counterintuitive for screen reader users. On top of that, these two attributes have been deprecated since ARIA 1.1, which means we won't see support for these attributes grow in the future. 

The [W3C conversation about this deprecation can be found here](https://lists.w3.org/Archives/Public/public-pfwg/2015Sep/0178.html?lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3BNEOwgUV0S86EqFWECz7CVw%3D%3D). Because of these problems, I decided against using `aria-grabbed` and `aria-dropeffect` in Dragon Drop. Varying support for ARIA attributes within the vast array of assistive technology/browser pairings is quite prevalent in the world of accessibility. Luckily, live region attributes such as `role`, `aria-live`, `aria-relevant`, and `aria-atomic` are quite widely supported by screen readers such as JAWS, NVDA, and VoiceOver.

## Optimized Accessibility

Dragon Drop is a highly configurable list reordering module that works for mouse, keyboard and assistive technology users. A couple of years ago, when I decided to write it, accessibly reordering lists had been brought up several times on projects I'd been working on but I had yet to see a working solution. Of the dozens of drag-and-drop list reorder plugins I came across, most of them weren't designed with accessibility in mind and, as a result, were very inaccessible. 

Dragon Drop has been tested with VoiceOver, JAWS and NVDA and enables AT users to successfully reorder a list. 

I set out to answer all of the questions that any user might have when encountering a reorderable list. These questions have been answered for sighted mouse users through common conventions, but what about the rest of the users?

### How Can I Pick Up An Item?

By providing a control which conveys the grabbed state of an item, along with some top-level help text, we can answer this question. For example, a control with the accessible text (gathered by AT though it's name, role and value) "Reorder Item 1, toggle button" tells the user that it is a button that when activated, will pick the item up and kick off a reordering. 

Dragon drop uses the `aria-pressed` attribute to let AT users know when an item is being "dragged" and when it is not. It can be configured to allow an entire item to be draggable, or just a child "drag handle", which in either case the presence of the `role="button"` and `tabindex="0"` is ensured. 

When a drag item is activated, `aria-pressed="true"` is applied to the element and a configurable announcement, such as _"Item 1 grabbed"_ is read out to screen readers via the live region.

### How Can I Move An Item?

Utilizing `aria-describedby` to associate the controls with useful help text such as _"Activate the reorder button and use the arrow keys to reorder the list or use your mouse to drag/reorder."_ tells the user how to go about actually reordering. This lets screen reader users know that when an item is pressed, the up and down arrow keys will move the item up and down the list respectively.

### How Can I Drop An Item?

Because the `aria-pressed` attribute is used, users can easily tell how to drop an item. In some way, shape or form, all of the most widely used screen readers convey the pressed state of a toggle button. The aria-pressed attribute is set to "false" when an item is dropped and a customized announcement such as _"Item 1 dropped"_ is read out to screen readers.

### How Do I Know When The List Has Been Reordered?

Every time the up and down arrow keys are used to alter the order of the list, we need to ensure that all users are notified of this change. For non-sighted users, we must once again rely on live regions. A configurable announcement such as _"The list has been reordered, Item 1 is now 4th in the list."_, is read out to convey the updated state of the reordered list. This is important because sighted users have immediate visual feedback of the altered order and that very same information needs to be conveyed to AT users.

### How Do I Cancel The Reordering?

Since we can't rely on a widely adopted convention for such interaction, we can simply include directions such as _"Press escape to cancel the reordering"_ within the help text. In addition, we utilize the live region to provide a customized readout that notifies the user of the cancellation.

### Keyboard Interaction

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
  <tr>
    <th data-tablesaw-priority="persist">Key</th>
    <th>Behavior</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><kbd>Enter</kbd> or <kbd>Space</kbd></td>
    <td>Toggles the item between the "grabbed" and "dropped" states</td>
  </tr>
  <tr>
    <td><kbd>"↓"</kbd></td>
    <td>Moves a "grabbed" item down in the list</td>
  </tr>
  <tr>
    <td><kbd>"↑"</kbd></td>
    <td>Moves a "grabbed" item up in the list</td>
  </tr>
  <tr>
    <td><kbd>Esc</kbd></td>
    <td>Cancels reordering and restores initial order</td>
  </tr>
</tbody>
</table>

## Seeing The Dragon In Action

Check the [Dragon Drop demo](https://schne324.github.io/dragon-drop/demo/) in which you experience a couple different configurations.

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/68e4a116-587e-44f1-b15f-ffa06a927530/dragon-drop-screenshot.png" sizes="100vw" caption="" alt="" >}}

## Dropping Dragon Drop Into Your App

Dragon Drop converts your ordinary list into a fully accessible drag-and-drop reorderable list:

<pre><code class="language-html">&lt;ul id="dragon">
  &lt;li>Item 1&lt;/li>
  &lt;li>Item 2&lt;/li>
  &lt;li>Item 3&lt;/li>
&lt;/ul>
&lt;script>
  const dragon = document.getElementById('dragon');
  // Enter the dragon
  new DragonDrop(dragon);
&lt;/script></code></pre>

### Installation

Dragon Drop is an open source (MIT License) project and can be installed via npm:

<pre><code class="language-bash">$ npm install drag-on-drop
</code></pre>

It can be used with modules like browserify or webpack:

<pre><code class="language-javascript">// if you're not down with ES6, you can require('drag-on-drop')
import DragonDrop from 'drag-on-drop';</code></pre>

Dragon Drop can also be easily dropped into your page with the [unpkg CDN](https://unpkg.com):

<pre><code class="language-html">&lt;script source="https://unpkg.com/drag-on-drop">&lt;/script>
&lt;script>
  var dragonDrop = new DragonDrop(listElement);
&lt;/script></code></pre>

### Configuration

To support a wide range of use cases, Dragon Drop is very configurable. 

Below is the default configuration:

<pre><code class="language-javascript">{
  item: 'li',
  handle: 'button',
  activeClass: 'dragon-active',
  inactiveClass: 'dragon-inactive',
  announcement: {
    grabbed: el => `Item ${el.innerText} grabbed`,
    dropped: el => `Item ${el.innerText} dropped`,
    reorder: (el, items) => {
      const pos = items.indexOf(el) + 1;
      const text = el.innerText;
      return `The list has been reordered, ${text} is now item ${pos} of ${items.length}`;
    },
    cancel: 'Reordering cancelled'
  }
}</code></pre>

**Announcements**

[Dragon Drop's "announcement" configuration option](https://github.com/schne324/dragon-drop#announcement-object) is the most important because is the backbone of the screen reader experience that Dragon Drop provides. It is an object containing `"grabbed"`, `"dropped"`, `"reorder"` and `"cancel"` functions allowing for custom live region announcements for all interactions that take place. 

Each of these functions must return a string of announcement text which is added to the live region when the given action occurs. An additional benefit of utilizing these functions is that it supports localizing the live region messages. 

To facilitate the announcements, the list item element in which the action took place upon and the array of items in the list are passed as the arguments respectively.

<pre><code class="language-javascript">{
  announcement: {
    // grabbed is called when an item is picked up
    grabbed: (targetItem, items) => `${targetItem.innerText} grabbed`,
    // dropped is called when an item is dropped
    dropped: (targetItem, items) => `${targetItem.innerText} grabbed`,
    // reorder is called each time the order of the list is altered
    reorder: (targetItem, items) => {
      return `${targetItem.innerText} is now ${items.indexOf(targetItem) + 1} of ${items.length}`
    },
    // cancel is called when a reordering is cancelled (via escape key)
    cancel: () => 'The initial order has been restored, reordering cancelled'
  }
}</code></pre>

**Help Text**

It is absolutely vital that you provide help text which describes how to use the reorderable list. This is something Dragon Drop doesn't do for you in order to remain less opinionated in how this text is made available to assistive technology. The recommended implementation is to use `aria-describedby` to associate the help text with the interactive items like so:

<pre><code class="language-html">&lt;p id="dragon-helper">Activate the reorder button and use the arrow keys to reorder the list or use your mouse to drag/reorder. Press escape to cancel the reordering.&lt;/p>
&lt;ul id="dragon">
  &lt;li>
&lt;button aria-describedby="dragon-helper">Reorder Item 1&lt;/button>
&lt;span>Item 1&lt;/span>
  &lt;/li>
  &lt;li>
&lt;button aria-describedby="dragon-helper">Reorder Item 2&lt;/button>
&lt;span>Item 2&lt;/span>
  &lt;/li>
  &lt;li>
&lt;button aria-describedby="dragon-helper">Reorder Item 3&lt;/button>
&lt;span>Item 3&lt;/span>
  &lt;/li>
&lt;/ul></code></pre>

## Dragon Drop On GitHub

The third version of Dragon Drop has recently been released. If you're interested in using it, please refer to the [Dragon Drop documentation on GitHub](https://github.com/schne324/dragon-drop). A special thanks goes out to the creators of [Dragula](https://github.com/bevacqua/dragula), the module Dragon Drop uses for mouse interaction, as well as Aaron Pearlman who designed the awesome logo!

## The Future Of The Dragon

If drag-and-drop interaction is added to the WAI-ARIA technical specification in the future, the fact that Dragon Drop relies on non-standard interaction and live regions could change. I will continue performing tests ensuring it remains well supported by as many screen readers as possible and keep up to date with the latest ARIA spec. In addition, there are quite a few features in the pipeline including support for touch screen/mobile devices as well as multi-column lists (like sprint boards). Another feature that may be added in the future is a Dragon Drop React component. 

{{< codepen height="480" theme_id="light" slug_hash="dZOGeG" default_tab="result" user="schne324" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/schne324/pen/dZOGeG/">React Dragon Drop</a> by Harris Schneiderman (<a href="https://codepen.io/schne324">@schne324</a>) on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

Currently, Dragon Drop can be used with React, as displayed in the demo below, but it is not ideal because the DOM changes caused by the reordering of the list are not picked up by React which can cause unexpected behavior. I urge anyone who finds bugs in Dragon Drop, or even has ideas for features to [create an issue on GitHub](https://github.com/schne324/dragon-drop/issues). All feedback and contribution is welcomed and greatly appreciated!

{{< signature "rb, ra, yk, il" >}}


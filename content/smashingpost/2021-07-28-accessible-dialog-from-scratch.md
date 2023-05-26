---
title: 'Creating An Accessible Dialog From Scratch'
slug: accessible-dialog-from-scratch
author: kitty-giraudel
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ef51448-125a-4906-98f1-11af0e3fad58/accessible-dialog-from-scratch.jpg
date: 2021-07-28T11:00:00.000Z
summary: >-
  Dialogs are everywhere in modern interface design (for good or for bad), and yet many of them are not accessible to assistive technologies. In this article, we will dig into how to create a short script to create accessible dialogs.
description: >-
  Dialogs are everywhere in modern interface design (for good or for bad), and yet many of them are not accessible to assistive technologies. In this article, we will dig into how to create a short script to create accessible dialogs.
categories:
  - Browsers
  - Interfaces
  - JavaScript
  - Accessibility
---

First of all, don’t do this at home. Do not write your own dialogs or a library to do so. There are plenty of them out there already that have been tested, audited, used and reused and you should prefer these ones over your own. [a11y-dialog](https://a11y-dialog.netlify.app/) is one of them, but there are more (listed at the end of this article).

Let me take this post as an opportunity to remind you all to **be cautious when using dialogs**. It is tentalizing to address all design problems with them, especially on mobile, but there often are other ways to overcome design issues. We tend to quickly fall into using dialogs not because they are necessarily the right choice but because they are easy. They set aside screen estate problems by trading them for context switching, which is not always the right trade-off. The point is: consider whether a dialog is the right design pattern before using it.

In this post, we’re going to write **a small JavaScript library for authoring accessible dialogs** from the very beginning (essentially recreating a11y-dialog). The goal is to understand what goes into it. We’re not going to deal with styling too much, just the JavaScript part. We will use modern JavaScript for sake of simplicity (such as classes and arrow functions), but keep in mind that this code might not work in legacy browsers.

1. [Defining the API](#defining-the-api)
2. [Instantiating the dialog](#instantiating-the-dialog)
3. [Showing and hiding](#showing-and-hiding)
4. [Closing with overlay](#closing-with-overlay)
5. [Closing with escape](#closing-with-escape)
6. [Trapping focus](#trapping-focus)
7. [Maintaining focus](#maintaining-focus)
8. [Restoring focus](#restoring-focus)
9. [Giving an accessible name](#giving-an-accessible-name)
10. [Handling custom events](#handling-custom-events)
11. [Cleaning up](#cleaning-up)
12. [Bring it all together](#bringing-it-all-together)
13. [Wrapping up](#wrapping-up)

## Defining The API

First, we want to define how we’re going to use our dialog script. We are going to keep it as simple as possible to begin with. We give it the root HTML element for our dialog, and the instance we get has a `.show(..)` and a `.hide(..)` method.

<pre><code class="language-javascript">class Dialog {
  constructor(element) {}
  show() {}
  hide() {}
}
</code></pre>

## Instantiating The Dialog

Let’s say we have the following HTML:

<pre><code class="language-html">&lt;div id="my-dialog"&gt;This will be a dialog.&lt;/div&gt;
</code></pre>

And we instantiate our dialog like this:

<pre><code class="language-javascript">const element = document.querySelector('#my-dialog')
const dialog = new Dialog(element)
</code></pre>

There are a few things we need to do under the hood when instantiating it:

- Hide it so it’s hidden by default (`hidden`).
- Mark it as a dialog for assistive technologies (`role="dialog"`).
- Make the rest of the page inert when open (`aria-modal="true"`).

<pre><code class="language-javascript">constructor (element) {
  // Store a reference to the HTML element on the instance so it can be used
  // across methods.
  this.element = element
  this.element.setAttribute('hidden', true)
  this.element.setAttribute('role', 'dialog')
  this.element.setAttribute('aria-modal', true)
}
</code></pre>

Note that we could have added these 3 attributes in our initial HTML not to have to add them with JavaScript, but this way it’s out of sight, out of mind. Our script can make sure things will work as they should, regardless of whether we’ve thought about adding all our attributes or not.

## Showing And Hiding

We have two methods: one to show the dialog and one to hide it. These methods won’t do much (for now) besides toggling the `hidden` attribute on the root element. We’re also going to maintain a boolean on the instance to quickly be able to assess if the dialog is shown or not. This will come in handy later.

<pre><code class="language-javascript">show() {
  this.isShown = true
  this.element.removeAttribute('hidden')
}

hide() {
  this.isShown = false
  this.element.setAttribute('hidden', true)
}
</code></pre>

To avoid the dialog being visible before JavaScript kicks in and hides it by adding the attribute, it might be interesting to add `hidden` to the dialog directly in the HTML from the get go.

<pre><code class="language-html">&lt;div id="my-dialog" hidden&gt;This will be a dialog.&lt;/div&gt;
</code></pre>

## Closing With Overlay

Clicking outside of the dialog should close it. There are several ways to do so. One way could be to listen to all click events on the page and filter out those happening within the dialog, but that’s relatively complex to do.

Another approach would be to listen to click events on the overlay (sometimes called “backdrop”). The overlay itself can be as simple as a `<div>` with some styles.

So when opening the dialog, we need to bind click events on the overlay. We could give it an ID or a certain class to be able to query it, or we could give it a data attribute. I tend to favor these for behavior hooks. Let’s modify our HTML accordingly:

<pre><code class="language-html">&lt;div id="my-dialog" hidden&gt;
  &lt;div data-dialog-hide>&lt;/div&gt;
  &lt;div>This will be a dialog.&lt;/div&gt;
&lt;/div&gt;
</code></pre>

Now, we can query the elements with the `data-dialog-hide` attribute within the dialog and give them a click listener that hides the dialog.

<pre><code class="language-javascript">constructor (element) {
  // … rest of the code
  // Bind our methods so they can be used in event listeners without losing the
  // reference to the dialog instance
  this._show = this.show.bind(this)
  this._hide = this.hide.bind(this)

  const closers = [...this.element.querySelectorAll('[data-dialog-hide]')]
  closers.forEach(closer => closer.addEventListener('click', this._hide))
}
</code></pre>

The nice thing about having something quite generic like this is that we can use the same thing for the close button of the dialog as well.

<pre><code class="language-javascript">&lt;div id="my-dialog" hidden&gt;
  &lt;div data-dialog-hide&gt;&lt;/div&gt;
  &lt;div&gt;
    This will be a dialog.
    &lt;button type="button" data-dialog-hide&gt;Close&lt;/button&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

{{% feature-panel %}}

## Closing With Escape

Not only should the dialog be hidden when clicking outside of it, but it also should be hidden when pressing <kbd>Esc</kbd>. When opening the dialog, we can bind a keyboard listener to the document, and remove it when closing it. This way, it only listens to key presses while the dialog is open instead of all the time.

<pre><code class="language-javascript">show() {
  // … rest of the code
  // Note: `_handleKeyDown` is the bound method, like we did for `_show`/`_hide`
  document.addEventListener('keydown', this._handleKeyDown)
}

hide() {
  // … rest of the code
  // Note: `_handleKeyDown` is the bound method, like we did for `_show`/`_hide`
  document.removeEventListener('keydown', this._handleKeyDown)
}

handleKeyDown(event) {
  if (event.key === 'Escape') this.hide()
}
</code></pre>

{{% ad-panel-leaderboard %}}

## Trapping Focus

Now that’s the good stuff. Trapping the focus within the dialog is kind of at the essence of the whole thing, and has to be the most complicated part (although probably not as complicated as you might think).

The idea is pretty simple: when the dialog is open, we listen for <kbd>Tab</kbd> presses. If pressing <kbd>Tab</kbd> on the last focusable element of the dialog, we programmatically move the focus to the first. If pressing <kbd>Shift</kbd> + <kbd>Tab</kbd> on the first focusable element of the dialog, we move it to the last one.

The function might look like this:

<pre><code class="language-javascript">function trapTabKey(node, event) {
  const focusableChildren = getFocusableChildren(node)
  const focusedItemIndex = focusableChildren.indexOf(document.activeElement)
  const lastIndex = focusableChildren.length - 1
  const withShift = event.shiftKey

  if (withShift && focusedItemIndex === 0) {
    focusableChildren[lastIndex].focus()
    event.preventDefault()
  } else if (!withShift && focusedItemIndex === lastIndex) {
    focusableChildren[0].focus()
    event.preventDefault()
  }
}
</code></pre>

The next thing we need to figure out is how to get all the focusable elements of the dialog (`getFocusableChildren`). We need to query all the elements that can theoretically be focusable, and then we need to make sure they effectively are.

The first part can be done with [focusable-selectors](https://github.com/KittyGiraudel/focusable-selectors). It’s a teeny tiny package I wrote which provides this array of selectors:

<pre><code class="language-javascript">module.exports = [
  'a[href]:not([tabindex^="-"])',
  'area[href]:not([tabindex^="-"])',
  'input:not([type="hidden"]):not([type="radio"]):not([disabled]):not([tabindex^="-"])',
  'input[type="radio"]:not([disabled]):not([tabindex^="-"]):checked',
  'select:not([disabled]):not([tabindex^="-"])',
  'textarea:not([disabled]):not([tabindex^="-"])',
  'button:not([disabled]):not([tabindex^="-"])',
  'iframe:not([tabindex^="-"])',
  'audio[controls]:not([tabindex^="-"])',
  'video[controls]:not([tabindex^="-"])',
  '[contenteditable]:not([tabindex^="-"])',
  '[tabindex]:not([tabindex^="-"])',
]
</code></pre>

And this is enough to get you 99% there. We can use these selectors to find all focusable elements, and then we can check every one of them to make sure it is actually visible on screen (and not hidden or something).

<pre><code class="language-javascript">import focusableSelectors from 'focusable-selectors'

function isVisible(element) {
  return element =>
    element.offsetWidth ||
    element.offsetHeight ||
    element.getClientRects().length
}

function getFocusableChildren(root) {
  const elements = [...root.querySelectorAll(focusableSelectors.join(','))]

  return elements.filter(isVisible)
}
</code></pre>

We can now update our `handleKeyDown` method:

<pre><code class="language-javascript">handleKeyDown(event) {
  if (event.key === 'Escape') this.hide()
  else if (event.key === 'Tab') trapTabKey(this.element, event)
}
</code></pre>

## Maintaining Focus

One thing that’s often overlooked when creating accessible dialogs is making sure the focus remains within the dialog even _after_ the page has lost focus. Think of it this way: **what happens if once the dialog is open?** We focus the URL bar of the browser, and then start tabbing again. Our focus trap is not going to work, since it only preserves the focus within the dialog when it’s inside the dialog to begin with.

To fix that problem, we can bind a focus listener to the `<body>` element when the dialog is shown, and move the focus to the first focusable element within the dialog.

<pre><code class="language-javascript">show () {
  // … rest of the code
  // Note: `_maintainFocus` is the bound method, like we did for `_show`/`_hide`
  document.body.addEventListener('focus', this._maintainFocus, true)
}

hide () {
  // … rest of the code
  // Note: `_maintainFocus` is the bound method, like we did for `_show`/`_hide`
  document.body.removeEventListener('focus', this._maintainFocus, true)
}

maintainFocus(event) {
  const isInDialog = event.target.closest('[aria-modal="true"]')
  if (!isInDialog) this.moveFocusIn()
}

moveFocusIn () {
  const target =
    this.element.querySelector('[autofocus]') ||
    getFocusableChildren(this.element)[0]

  if (target) target.focus()
}
</code></pre>

Which element to focus when opening the dialog is not enforced, and it could depend on which type of content the dialog displays. Generally speaking, there are a couple of options:

- **Focus the first element.**  
This is what we do here, since it is made easier by the fact that we already have a `getFocusableChildren` function.
- **Focus the close button.**  
This is also a good solution, especially if the button is absolutely positioned relatively to the dialog. We can conveniently make this happen by placing our close button as the first element of our dialog. If the close button lives in the flow of the dialog content, at the very end, it could be a problem if the dialog has a lot of content (and therefore is scrollable), as it would scroll the content to the end on open.
- [**Focus the dialog itself**](https://github.com/KittyGiraudel/a11y-dialog/issues/169).  
This is not very common among dialog libraries, but it should also work (although it would require adding `tabindex="-1"` to it so that’s possible since a `<div>` element is not focusable by default).

Note that we check whether there is an element with the `autofocus` HTML attribute within the dialog, in which case we would move the focus to it instead of the first item. 

## Restoring Focus

We’ve managed to successfully trap the focus within the dialog, but we forgot to move the focus inside the dialog once it opens. Similarly, we need to restore the focus back to the element that had it before the dialog was open.

When showing the dialog, we can start by keeping a reference to the element that has the focus (`document.activeElement`). Most of the time, this will be the button that was interacted with to open the dialog, but in rare cases where a dialog is opened programmatically, it could be something else.

<pre><code class="language-javascript">show() {
  this.previouslyFocused = document.activeElement
  // … rest of the code
  this.moveFocusIn()
}
</code></pre>

When hiding the dialog, we can move the focus back to that element. We guard it with a condition to avoid a JavaScript error if the element somehow no longer exists (or [if it was a SVG](https://github.com/KittyGiraudel/a11y-dialog/issues/108)):

<pre><code class="language-javascript">hide() {
  // … rest of the code
  if (this.previouslyFocused && this.previouslyFocused.focus) {
    this.previouslyFocused.focus()
  }
}
</code></pre>

## Giving An Accessible Name

It is important our dialog has an accessible name, which is how it will be listed in the accessibility tree. There are a couple of ways to address it, one of which is to define a name in the `aria-label` attribute, but [`aria-label` has issues](https://heydonworks.com/article/aria-label-is-a-xenophobe/).

Another way is to have a title within our dialog (whether hidden or not), and to associate our dialog to it with the `aria-labelledby` attribute. It might look like this:

<pre><code class="language-html">&lt;div id="my-dialog" hidden aria-labelledby="my-dialog-title"&gt;
  &lt;div data-dialog-hide&gt;&lt;/div&gt;
  &lt;div&gt;
    &lt;h1 id="my-dialog-title"&gt;My dialog title&lt;/h1&gt;
    This will be a dialog.
    &lt;button type="button" data-dialog-hide&gt;Close&lt;/button&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

I guess we could make our script apply this attribute dynamically based on the presence of the title and whatnot, but I’d say this is just as easily solved by authoring proper HTML, to begin with. No need to add JavaScript for that.

{{% ad-panel-leaderboard %}}

## Handling Custom Events

What if we want to react to the dialog being open? Or closed? There is currently no way to do it, but adding a small event system should not be too difficult. We need a function to register events (let’s call it `.on(..)`), and a function to unregister them (`.off(..)`).

<pre><code class="language-javascript">class Dialog {
  constructor(element) {
    this.events = { show: [], hide: [] }
  }
  on(type, fn) {
    this.events[type].push(fn)
  }
  off(type, fn) {
    const index = this.events[type].indexOf(fn)
    if (index > -1) this.events[type].splice(index, 1)
  }
}
</code></pre>

Then when showing and hiding the method, we’ll call all functions that have been registered for that particular event.

<pre><code class="language-javascript">class Dialog {
  show() {
    // … rest of the code
    this.events.show.forEach(event => event())
  }

  hide() {
    // … rest of the code
    this.events.hide.forEach(event => event())
  }
}
</code></pre>

## Cleaning Up

We might want to provide a method to clean up a dialog in case we’re done using it. It would be responsible for unregistering event listeners so they don’t last more than they should.

<pre><code class="language-javascript">class Dialog {
  destroy() {
    const closers = [...this.element.querySelectorAll('[data-dialog-hide]')]
    closers.forEach(closer => closer.removeEventListener('click', this._hide))

    this.events.show.forEach(event => this.off('show', event))
    this.events.hide.forEach(event => this.off('hide', event))
  }
}
</code></pre>

## Bringing It All Together

<pre><code class="language-javascript">import focusableSelectors from 'focusable-selectors'

class Dialog {
  constructor(element) {
    this.element = element
    this.events = { show: [], hide: [] }

    this._show = this.show.bind(this)
    this._hide = this.hide.bind(this)
    this._maintainFocus = this.maintainFocus.bind(this)
    this._handleKeyDown = this.handleKeyDown.bind(this)

    element.setAttribute('hidden', true)
    element.setAttribute('role', 'dialog')
    element.setAttribute('aria-modal', true)

    const closers = [...element.querySelectorAll('[data-dialog-hide]')]
    closers.forEach(closer => closer.addEventListener('click', this._hide))
  }

  show() {
    this.isShown = true
    this.previouslyFocused = document.activeElement
    this.element.removeAttribute('hidden')

    this.moveFocusIn()

    document.addEventListener('keydown', this._handleKeyDown)
    document.body.addEventListener('focus', this._maintainFocus, true)

    this.events.show.forEach(event => event())
  }

  hide() {
    if (this.previouslyFocused && this.previouslyFocused.focus) {
      this.previouslyFocused.focus()
    }

    this.isShown = false
    this.element.setAttribute('hidden', true)

    document.removeEventListener('keydown', this._handleKeyDown)
    document.body.removeEventListener('focus', this._maintainFocus, true)

    this.events.hide.forEach(event => event())
  }

  destroy() {
    const closers = [...this.element.querySelectorAll('[data-dialog-hide]')]
    closers.forEach(closer => closer.removeEventListener('click', this._hide))

    this.events.show.forEach(event => this.off('show', event))
    this.events.hide.forEach(event => this.off('hide', event))
  }

  on(type, fn) {
    this.events[type].push(fn)
  }

  off(type, fn) {
    const index = this.events[type].indexOf(fn)
    if (index > -1) this.events[type].splice(index, 1)
  }

  handleKeyDown(event) {
    if (event.key === 'Escape') this.hide()
    else if (event.key === 'Tab') trapTabKey(this.element, event)
  }

  moveFocusIn() {
    const target =
      this.element.querySelector('[autofocus]') ||
      getFocusableChildren(this.element)[0]

    if (target) target.focus()
  }

  maintainFocus(event) {
    const isInDialog = event.target.closest('[aria-modal="true"]')
    if (!isInDialog) this.moveFocusIn()
  }
}

function trapTabKey(node, event) {
  const focusableChildren = getFocusableChildren(node)
  const focusedItemIndex = focusableChildren.indexOf(document.activeElement)
  const lastIndex = focusableChildren.length - 1
  const withShift = event.shiftKey

  if (withShift && focusedItemIndex === 0) {
    focusableChildren[lastIndex].focus()
    event.preventDefault()
  } else if (!withShift && focusedItemIndex === lastIndex) {
    focusableChildren[0].focus()
    event.preventDefault()
  }
}

function isVisible(element) {
  return element =>
    element.offsetWidth ||
    element.offsetHeight ||
    element.getClientRects().length
}

function getFocusableChildren(root) {
  const elements = [...root.querySelectorAll(focusableSelectors.join(','))]

  return elements.filter(isVisible)
}
</code></pre>

## Wrapping Up

That was quite something, but we eventually got there! Once again, I would advise against rolling out your own dialog library since it’s not the most straightforward and errors could be highly problematic for assistive technology users. But at least now you know how it works under the hood!

If you need to use dialogs in your project, consider using one of the following solutions (kind reminder that we have our [comprehensive list of accessible components](https://www.smashingmagazine.com/2021/03/complete-guide-accessible-front-end-components/#accessible-modals) as well):

- Vanilla JavaScript implementations: [a11y-dialog](https://a11y-dialog.netlify.app) by yours truly or [aria-modal-dialog](https://github.com/scottaohara/accessible_modal_window) by Scott O’Hara.
- React implementations: [react-a11y-dialog](https://github.com/KittyGiraudel/react-a11y-dialog) by yours truly again, [reach/dialog](https://reach.tech/dialog/) from the Reach framework, or [@react-aria/dialog](https://react-spectrum.adobe.com/react-aria/useDialog.html) from Adobe. You might be interested in [this comparison of the 3 libraries](https://github.com/KittyGiraudel/react-a11y-dialog/issues/58).
- Vue implementations: [vue-a11y-dialog](https://github.com/morkro/vue-a11y-dialog) by Moritz Kröger, [a11y-vue-dialog](https://github.com/renatodeleao/a11y-vue-dialog) by Renato de Leão.

Here are more things that could be added but were not for sake of simplicity:

- Support for alert-dialogs via the `alertdialog` role. Refer to the a11y-dialog [documentation on alert dialogs](https://a11y-dialog.netlify.app/advanced/alert-dialog).
- Locking the ability to scroll while the dialog is open. Refer to the a11y-dialog [documentation on scroll lock](https://a11y-dialog.netlify.app/advanced/scroll-lock).
- Support for the native HTML `<dialog>` element because it’s sub-par and inconsistent. Refer to the a11y-dialog [documentation on the dialog element](https://a11y-dialog.netlify.app/advanced/dialog-element) and [this piece by Scott O’hara](https://www.scottohara.me/blog/2019/03/05/open-dialog.html) for more information about why it’s not worth the trouble.
- Support for nested dialogs because it’s questionable. Refer to the a11y-dialog [documentation on nested dialogs](https://a11y-dialog.netlify.app/advanced/nested-dialogs).
- Consideration for closing the dialog on browser navigation. In some cases, it might make sense to close the dialog when pressing the back button of the browser.

{{< signature "vf, il" >}}

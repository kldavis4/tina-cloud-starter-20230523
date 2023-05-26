---
title: 'CTA Modal: How To Build A Web Component'
slug: cta-modal-build-web-component
author: nathan-smith
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2bbadf16-a6e1-4d24-ba72-77cc51e3cc4e/cta-modal-build-web-component.jpg
date: 2022-04-28T09:30:00.000Z
summary: >-
  In this article, Nathan Smith explains how to create modal dialog windows with rich interaction that will only require authoring HTML in order to be used. They are based on Web Components that are currently supported by every major browser.
description: >-
  In this article, Nathan Smith explains how to create modal dialog windows with rich interaction that will only require authoring HTML in order to be used. They are based on Web Components that are currently supported by every major browser.
categories:
  - Apps
  - HTML
  - Browsers
  - JavaScript
  - Web Components
---

I have a confession to make &mdash; I am not overly fond of modal dialogs (or just “modals” for short). “Hate” would be too strong a word to use, but let’s say that nothing is more of a turnoff when starting to read an article than being “slapped in the face” with a modal window before I have even begun to comprehend what I am looking at.

Or, if I could [quote Andy Budd](https://twitter.com/andybudd/status/1477634654429663237): 

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">A typical website visit in 2022<br><br>1. Figure out how to decline all but essential cookies<br>2. Close the support widget asking if I need help<br>3. Stop the auto-playing video<br>4. Close the “subscribe to our newsletter” pop-up<br>5. Try and remember why I came here in the first place</p>&mdash; Andy Budd (@andybudd) <a href="https://twitter.com/andybudd/status/1477634654429663237?ref_src=twsrc%5Etfw">January 2, 2022</a></blockquote>

That said, modals are **everywhere** among us. They are a user interface paradigm that we cannot simply disinvent. When used *tastefully* and *wisely*, I dare say they can even help add more context to a document or to an app.

Throughout my career, I have written my fair share of modals. I have built bespoke implementations using vanilla JavaScript, jQuery, and more recently &mdash; [React](https://reactjs.org/). If you have ever struggled to build a modal, then you will know what I mean when I say: It is easy to get them wrong. Not only from a visual standpoint but there are plenty of tricky user interactions that need to be accounted for as well. 

I am the type of person who likes to “go deep” on topics that vex me &mdash; especially if I find the topic resurfacing &mdash; hopefully in an effort to avoid revisiting them ever again. When I started to get more into [Web Components](https://developer.mozilla.org/en-US/docs/Web/Web_Components), I had an “a-ha!” moment. Now that Web Components are widely supported by every major browser (RIP, [IE11](https://en.wikipedia.org/wiki/Internet_Explorer_11)), this opens up a whole new door of opportunity. I thought to myself:

<blockquote>“What if it were possible to build a modal that, as a developer authoring a page or app, I would not have to fuss with any additional JavaScript config?”</blockquote>

Write once and run everywhere, so to speak, or at least that was my lofty aspiration. Good news. It is indeed possible to build a modal with rich interaction that only requires authoring HTML to use.

**Note:** *In order to benefit from this article and code examples you will need some basic familiarity with HTML, CSS, and JavaScript.*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc511cb3-91ff-4aac-8034-859479befd27/3-cta-modal-build-web-component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc511cb3-91ff-4aac-8034-859479befd27/3-cta-modal-build-web-component.png" width="800" height="514" sizes="100vw" caption="CTA Modal &mdash; displaying a form. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cc511cb3-91ff-4aac-8034-859479befd27/3-cta-modal-build-web-component.png'>Large preview</a>)" alt="A screenshot of the CTA Modal dialog displaying a form." >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/401ad39a-7403-4b76-83ec-cc303494ae27/1-cta-modal-build-web-component.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/401ad39a-7403-4b76-83ec-cc303494ae27/1-cta-modal-build-web-component.png" width="800" height="501" sizes="100vw" caption="CTA Modal &mdash; scrollable content. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/401ad39a-7403-4b76-83ec-cc303494ae27/1-cta-modal-build-web-component.png'>Large preview</a>)" alt="A screenshot of the CTA Modal dialog displaying a scrollable piece of content." >}}

### Before We Even Begin

If you are tight on time and just want to see the finished product, check it out here:

- CTA Modal [Demo page](https://host.sonspring.com/cta-modal)
- CTA Modal [Git repo](https://github.com/nathansmith/cta-modal)

## Use The Platform

Now that we have covered the “why” of scratching this particular itch, throughout the rest of this article I will explain the “how” of building it.

First, a quick crash course on Web Components. They are bundled snippets of HTML, CSS, and JavaScript that encapsulate scope. Meaning, no styles from outside of a component will affect within, nor vice versa. Think of it like a hermetically sealed “[clean room](https://en.wikipedia.org/wiki/Cleanroom)” of UI design.

At first blush, this may seem nonsensical. Why would we want a chunk of UI that we cannot control externally via CSS? Hang onto that thought, because we will come back to it soon.

The best explanation is reusability. Building a component in this manner means we are not beholden to any particular JS framework *du jour*. One common phrase that gets bandied about in conversations around web standards is “[use the platform](https://timkadlec.com/remembers/2019-10-21-using-the-platform/).” Now more than ever, the platform itself has superb [cross-browser support](https://www.ravedigital.agency/blog/cross-browser-compatibility/).

## Deep Dive

*For reference, I will be referring to this code example &mdash; [`cta-modal.ts`](https://github.com/nathansmith/cta-modal/blob/main/src/assets/ts/cta-modal.ts).*

**Note:** *I am using [TypeScript](https://www.typescriptlang.org/) here, but you absolutely do* ***not*** *need any additional tooling to create a Web Component. In fact, I wrote my initial proof-of-concept in vanilla JS. I added TypeScript later, to bolster confidence in others using it as an NPM package.*

The `cta-modal.ts` file is chunked apart into several sections:

1. [Conditional wrapper](#conditional-wrapper);
2. Constants:
    - [Reusable variables](#reusable-variables),
    - [Component styles](#component-styles),
    - [Component markup](#component-markup);
3. `CtaModal` class:
    - [Constructor](#constructor),
    - [Binding `this` context](#binding-this-context),
    - [Lifecycle methods](#lifecycle-methods),
    - [Adding and removing events](#adding-and-removing-events),
    - [Detecting attribute changes](#detecting-attribute-changes),
    - [Focusing specific elements](#focusing-specific-elements),
    - [Detecting “outside” modal](#detecting-outside-modal),
    - [Detecting motion preference](#detecting-motion-preference),
    - [Toggling modal show/hide](#toggling-modal-show-hide),
    - Handle event: [click overlay](#handle-event-click-overlay),
    - Handle event: [click toggle](#handle-event-click-toggle),
    - Handle event: [focus element](#handle-event-focus-element),
    - Handle event: [keyboard](#handle-event-keyboard);
4. [DOM loaded callback](#dom-loaded-callback):
    - Waits for the page to be ready,
    - Registers the `<cta-modal>` tag.

{{% feature-panel %}}

### Conditional Wrapper

There is a single, top level `if` that wraps the entirety of the file’s code:

<pre><code class="language-javascript">// ===========================
// START: if "customElements".
// ===========================

if ('customElements' in window) {
  /&#42; NOTE: LINES REMOVED, FOR BREVITY. &#42;/
}

// =========================
// END: if "customElements".
// =========================</code></pre>

The reason for this is twofold. We want to ensure that there is [browser support](https://caniuse.com/custom-elementsv1) for `window.customElements`. If so, this gives us a handy way to maintain variable scope. Meaning, that when declaring variables via `const` or `let`, they do not “leak” outside of the `if {…}` block. Whereas using an old school `var` would be problematic, inadvertently creating several global variables.

### Reusable Variables

**Note:** *A JavaScript `class Foo {…}` differs from an HTML or CSS `class="foo"`.*

Think of it simply as: “A group of functions, bundled together.”

This section of the file contains [primitive](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) values that I intend to reuse throughout my JS [class](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) declaration. I will call out a few of them as being particularly interesting.

<pre><code class="language-javascript">// ==========
// Constants.
// ==========

/&#42; NOTE: LINES REMOVED, FOR BREVITY. &#42;/

const ANIMATION&#95;DURATION = 250;
const DATA&#95;HIDE = 'data-cta-modal-hide';
const DATA&#95;SHOW = 'data-cta-modal-show';
const PREFERS&#95;REDUCED&#95;MOTION = '(prefers-reduced-motion: reduce)';

const FOCUSABLE&#95;SELECTORS = [
  '[contenteditable]',
  '[tabindex="0"]:not([disabled])',
  'a[href]',
  'audio[controls]',
  'button:not([disabled])',
  'iframe',
  "input:not([disabled]):not([type='hidden'])",
  'select:not([disabled])',
  'summary',
  'textarea:not([disabled])',
  'video[controls]',
].join(',');</code></pre>

- `ANIMATION_DURATION`  
Specifies how long my CSS animations will take. I also reuse this later within a `setTimeout` to keep my CSS and JS in sync. It is set to `250` milliseconds, which is a quarter of a second.  
While CSS allows us to specify `animation-duration` in whole seconds (or milliseconds), JS uses increments of milliseconds. Going with this value allows me to use it for both.
- `DATA_SHOW` and `DATA_HIDE`  
These are strings for the HTML data attributes `'data-cta-modal-show'` and `'data-cta-modal-hide'` that are used to control the show/hide of modal, as well as adjust animation timing in CSS. They are used later in conjunction with `ANIMATION_DURATION`.
- `PREFERS_REDUCED_MOTION`  
A media query that determines whether or not a user has set their operating system’s preference to `reduce` for `prefers-reduced-motion`. I look at this value in both CSS and JS to determine whether to turn off animations.
- `FOCUSABLE_SELECTORS`  
Contains CSS selectors for all elements that could be considered focusable within a modal. It is used later more than once, via `querySelectorAll`. I have declared it here to help with readability, rather than adding clutter to a function body.

It equates to this string:

<div class="break-out">

 <pre><code class="language-markup">[contenteditable], [tabindex="0"]:not([disabled]), a[href], audio[controls], button:not([disabled]), iframe, input:not([disabled]):not([type='hidden']), select:not([disabled]), summary, textarea:not([disabled]), video[controls]</code></pre>
</div>
  
Yuck, right!? You can see why I wanted to break that into multiple lines.

As an astute reader, you may have noticed `type='hidden'` and `tabindex="0"` are using different quotation marks. That is purposeful, and we will revisit the reasoning later on.

### Component Styles

This section contains a multiline string with a `<style>` tag. As mentioned before, styles contained within a Web Component do not affect the rest of the page. It is worth noting how I am using embedded variables `${etc}` via string interpolation.

- We reference our variable `PREFERS_REDUCED_MOTION` to forcibly set animations to `none` for users who prefer reduced motion.
- We reference `DATA_SHOW` and `DATA_HIDE` along with `ANIMATION_DURATION` to allow shared control over CSS animations. Note the use of the `ms` suffix for milliseconds, since that is the lingua franca of CSS and JS.

<pre><code class="language-javascript">// ======
// Style.
// ======

const STYLE = `
  &lt;style&gt;
    /&#42; NOTE: LINES REMOVED, FOR BREVITY. &#42;/

    @media ${PREFERS_REDUCED_MOTION} {
      &#42;,
      &#42;:after,
      &#42;:before {
        animation: none !important;
        transition: none !important;
      }
    }

    [${DATA&#95;SHOW}='true'] .cta-modal&#95;&#95;overlay {
      animation-duration: ${ANIMATION&#95;DURATION}ms;
      animation-name: SHOW-OVERLAY;
    }

    [${DATA&#95;SHOW}='true'] .cta-modal&#95;&#95;dialog {
      animation-duration: ${ANIMATION&#95;DURATION}ms;
      animation-name: SHOW-DIALOG;
    }

    [${DATA&#95;HIDE}='true'] .cta-modal&#95;&#95;overlay {
      animation-duration: ${ANIMATION_DURATION}ms;
      animation-name: HIDE-OVERLAY;
      opacity: 0;
    }

    [${DATA_HIDE}='true'] .cta-modal&#95;&#95;dialog {
      animation-duration: ${ANIMATION_DURATION}ms;
      animation-name: HIDE-DIALOG;
      transform: scale(0.95);
    }
  &lt;/style&gt;
`;</code></pre>

### Component Markup

The markup for the modal is the most straightforward part. These are the essential aspects that make up the modal:

- slots,
- scrollable area,
- focus traps,
- semi-transparent overlay,
- dialog window,
- close button.

When making use of a `<cta-modal>` tag in one’s page, there are two insertion points for content. Placing elements inside these areas cause them to appear as part of the modal:

- `<div slot="button">` maps to `<slot name='button'>`,
- `<div slot="modal">` maps to `<slot name='modal'>`.

You might be wondering what “focus traps” are, and why we need them. These exist to snag focus when a user attempts to tab forwards (or backwards) outside of the modal dialog. If either of these receives focus, they will place the browser’s focus back inside.

Additionally, we give these attributes to the div we want to serve as our modal dialog element. This tells the browser that the `<div>` is semantically significant. It also allows us to place focus on the element via JS:

- `aria-modal='true'`,
- `role='dialog'`,
- `tabindex'-1'`.

<div class="break-out">

<pre><code class="language-javascript">// =========
// Template.
// =========

const FOCUS_TRAP = &#96;
  &lt;span
    aria-hidden='true'
    class='cta-modal&#95;&#95;focus-trap'
    tabindex='0'
  &gt;&lt;/span&gt;
&#96;;

const MODAL = &#96;
  &lt;slot name='button'&gt;&lt;/slot&gt;

  &lt;div class='cta-modal&#95;&#95;scroll' style='display:none'&gt;
    ${FOCUS_TRAP}

    &lt;div class='cta-modal&#95;&#95;overlay'&gt;
      &lt;div
        aria-modal='true'
        class='cta-modal&#95;&#95;dialog'
        role='dialog'
        tabindex='-1'
      &gt;
        &lt;button
          class='cta-modal&#95;&#95;close'
          type='button'
        &gt;&times;&lt;/button&gt;

        &lt;slot name='modal'&gt;&lt;/slot&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    ${FOCUS_TRAP}
  &lt;/div&gt;
&#96;;

// Get markup.
const markup = [STYLE, MODAL].join(EMPTY_STRING).trim().replace(SPACE_REGEX, SPACE);

// Get template.
const template = document.createElement(TEMPLATE);
template.innerHTML = markup;</code></pre>
</div>

You may be wondering: “Why not use the `dialog` tag?” Good question. At the time of this writing, it still has some cross-browser quirks. For more on that, read this article by [Scott O’hara](https://www.scottohara.me/blog/2019/03/05/open-dialog.html). Also, according to the [Mozilla documentation](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog), `dialog` is not allowed to have a `tabindex` attribute, which we need to put focus on our modal.

### Constructor

Whenever a JS class is instantiated, its `constructor` function is called. That is just a fancy term that means an *instance* of the `CtaModal` class is being created. In the case of our Web Component, this instantiation happens automatically whenever a `<cta-modal>` is encountered in a page’s HTML.

Within the `constructor` we call `super` which tells the `HTMLElement` class (which we are `extend`-ing) to call its own `constructor`. Think of it like glue code, to make sure we tap into some of the default lifecycle methods.

Next, we call `this._bind()` which we will cover a bit more later. Then we attach the “shadow DOM” to our class instance and add the markup that we created as a multiline string earlier.

After that, we get all the elements &mdash; from within the aforementioned *component markup* section &mdash; for use in later function calls. Lastly, we call a few helper methods that read attributes from the corresponding `<cta-modal>` tag.

<div class="break-out">

<pre><code class="language-javascript">// =======================
// Lifecycle: constructor.
// =======================

constructor() {
  // Parent constructor.
  super();

  // Bind context.
  this.&#95;bind();

  // Shadow DOM.
  this.&#95;shadow = this.attachShadow({ mode: 'closed' });

  // Add template.
  this.&#95;shadow.appendChild(
    // Clone node.
    template.content.cloneNode(true)
  );

  // Get slots.
  this.&#95;slotForButton = this.querySelector("[slot='button']");
  this.&#95;slotForModal = this.querySelector("[slot='modal']");

  // Get elements.
  this.&#95;heading = this.querySelector('h1, h2, h3, h4, h5, h6');

  // Get shadow elements.
  this.&#95;buttonClose = this.&#95;shadow.querySelector('.cta-modal&#95;&#95;close') as HTMLElement;
  this.&#95;focusTrapList = this.&#95;shadow.querySelectorAll('.cta-modal&#95;&#95;focus-trap');
  this.&#95;modal = this.&#95;shadow.querySelector('.cta-modal&#95;&#95;dialog') as HTMLElement;
  this.&#95;modalOverlay = this.&#95;shadow.querySelector('.cta-modal&#95;&#95;overlay') as HTMLElement;
  this.&#95;modalScroll = this.&#95;shadow.querySelector('.cta-modal&#95;&#95;scroll') as HTMLElement;

  // Missing slot?
  if (!this.&#95;slotForModal) {
    window.console.error('Required [slot="modal"] not found inside cta-modal.');
  }

  // Set animation flag.
  this.&#95;setAnimationFlag();

  // Set close title.
  this.&#95;setCloseTitle();

  // Set modal label.
  this.&#95;setModalLabel();

  // Set static flag.
  this.&#95;setStaticFlag();

  /&#42;
  =====
  NOTE:
  =====

    We set this flag last because the UI visuals within
    are contingent on some of the other flags being set.
  &#42;/

  // Set active flag.
  this.&#95;setActiveFlag();
}</code></pre>
</div>

### Binding `this` Context

This is a bit of JS wizardry that saves us from having to type tedious code needlessly elsewhere. When working with [DOM events](https://en.wikipedia.org/wiki/DOM_events) the context of `this` can change, depending on what element is being interacted with within the page.

One way to ensure that `this` always means the instance of our class is to specifically call `bind`. Essentially, this function makes it, so that it is handled automatically. That means we do not have to type things like this everywhere.

<pre><code class="language-javascript">/&#42; NOTE: Just an example, we don't need this. &#42;/
this.someFunctionName1 = this.someFunctionName1.bind(this);
this.someFunctionName2 = this.someFunctionName2.bind(this);</code></pre>

Instead of typing that snippet above, every time we add a new function, a handy `this._bind()` call in the `constructor` takes care of any/all functions we might have. This loop grabs every class property that is a `function` and binds it automatically.

<pre><code class="language-javascript">// ============================
// Helper: bind `this` context.
// ============================

&#95;bind() {
  // Get property names.
  const propertyNames = Object.getOwnPropertyNames(
    // Get prototype.
    Object.getPrototypeOf(this)
  ) as (keyof CtaModal)[];

  // Loop through.
  propertyNames.forEach((name) =&gt; {
    // Bind functions.
    if (typeof this[name] === FUNCTION) {
      /&#42;
      =====
      NOTE:
      =====

        Why use "@ts-expect-error" here?

        Calling `&#42;.bind(this)` is a standard practice
        when using JavaScript classes. It is necessary
        for functions that might change context because
        they are interacting directly with DOM elements.

        Basically, I am telling TypeScript:

        "Let me live my life!"

        😎
      &#42;/

      // @ts-expect-error bind
      this[name] = this[name].bind(this);
    }
  });
}</code></pre>

### Lifecycle Methods

By nature of this line, where we `extend` from `HTMLElement`, we get a few built-in function calls for “free.” As long as we name our functions by these names they will be called at the appropriate time within the lifecycle of our `<cta-modal>` component.

<pre><code class="language-javascript">// ==========
// Component.
// ==========

class CtaModal extends HTMLElement {
  /&#42; NOTE: LINES REMOVED, FOR BREVITY. &#42;/
}</code></pre>

- `observedAttributes`  
This tells the browser which attributes we are watching for changes.
- `attributeChangedCallback`  
If any of those attributes change, this callback will be invoked. Depending on which attribute changed, we call a function to read the attribute.
- `connectedCallback`  
This is called when a `<cta-modal>` tag is registered with the page. We use this opportunity to add all our event handlers.  
If you are familiar with [React](https://reactjs.org/), this is similar to the `componentDidMount` lifecycle event.
- `disconnectedCallback`  
This is called when a `<cta-modal>` tag is removed from the page. Likewise, we remove all obsolete event handlers when/if this occurs.  
It is similar to the `componentWillUnmount` lifecycle event in React.

**Note:** *It is worth pointing out that these are the only functions within our class that are not prefixed by an underscore (`_`). Though not strictly necessary, the reason for this is twofold. One, it makes it obvious which functions we have created for our new `<cta-modal>` and which are native lifecycle events of the `HTMLElement` class. Two, when we minify our code later the prefix denotes they can be mangled. Whereas the native lifecycle methods need to retain their names verbatim.*

<pre><code class="language-javascript">// ============================
// Lifecycle: watch attributes.
// ============================

static get observedAttributes() {
  return [ACTIVE, ANIMATED, CLOSE, STATIC];
}

// ==============================
// Lifecycle: attributes changed.
// ==============================

attributeChangedCallback(name: string, oldValue: string, newValue: string) {
  // Different old/new values?
  if (oldValue !== newValue) {
    // Changed [active="…"] value?
    if (name === ACTIVE) {
      this.&#95;setActiveFlag();
    }

    // Changed [animated="…"] value?
    if (name === ANIMATED) {
      this.&#95;setAnimationFlag();
    }

    // Changed [close="…"] value?
    if (name === CLOSE) {
      this.&#95;setCloseTitle();
    }

    // Changed [static="…"] value?
    if (name === STATIC) {
      this.&#95;setStaticFlag();
    }
  }
}

// ===========================
// Lifecycle: component mount.
// ===========================

connectedCallback() {
  this.&#95;addEvents();
}

// =============================
// Lifecycle: component unmount.
// =============================

disconnectedCallback() {
  this.&#95;removeEvents();
}</code></pre>

### Adding And Removing Events

These functions register (and remove) callbacks for various element and page-level events:

- buttons clicked,
- elements focused,
- keyboard pressed,
- overlay clicked.

<div class="break-out">

<pre><code class="language-javascript">// ===================
// Helper: add events.
// ===================

&#95;addEvents() {
  // Prevent doubles.
  this.&#95;removeEvents();

  document.addEventListener(FOCUSIN, this.&#95;handleFocusIn);
  document.addEventListener(KEYDOWN, this.&#95;handleKeyDown);

  this.&#95;buttonClose.addEventListener(CLICK, this.&#95;handleClickToggle);
  this.&#95;modalOverlay.addEventListener(CLICK, this.&#95;handleClickOverlay);

  if (this.&#95;slotForButton) {
    this.&#95;slotForButton.addEventListener(CLICK, this.&#95;handleClickToggle);
    this.&#95;slotForButton.addEventListener(KEYDOWN, this.&#95;handleClickToggle);
  }

  if (this.&#95;slotForModal) {
    this.&#95;slotForModal.addEventListener(CLICK, this.&#95;handleClickToggle);
    this.&#95;slotForModal.addEventListener(KEYDOWN, this.&#95;handleClickToggle);
  }
}

// ======================
// Helper: remove events.
// ======================

&#95;removeEvents() {
  document.removeEventListener(FOCUSIN, this.&#95;handleFocusIn);
  document.removeEventListener(KEYDOWN, this.&#95;handleKeyDown);

  this.&#95;buttonClose.removeEventListener(CLICK, this.&#95;handleClickToggle);
  this.&#95;modalOverlay.removeEventListener(CLICK, this.&#95;handleClickOverlay);

  if (this.&#95;slotForButton) {
    this.&#95;slotForButton.removeEventListener(CLICK, this.&#95;handleClickToggle);
    this.&#95;slotForButton.removeEventListener(KEYDOWN, this.&#95;handleClickToggle);
  }

  if (this.&#95;slotForModal) {
    this.&#95;slotForModal.removeEventListener(CLICK, this.&#95;handleClickToggle);
    this.&#95;slotForModal.removeEventListener(KEYDOWN, this.&#95;handleClickToggle);
  }
}</code></pre>
</div>

{{% ad-panel-leaderboard %}}

### Detecting Attribute Changes

These functions handle reading attributes from a `<cta-modal>` tag and setting various flags as a result:

- Setting an `_isAnimated` boolean on our class instance.
- Setting `title` and `aria-label` attributes on our close button.
- Setting an `aria-label` for our modal dialog, based on heading text.
- Setting an `_isActive` boolean on our class instance.
- Setting an `_isStatic` boolean on our class instance.

You may be wondering why we are using `aria-label` to relate the modal to its heading text (if it exists). At the time of this writing, browsers are not currently able to correlate an `aria-labelledby="…"` attribute &mdash; within the shadow DOM &mdash; to an `id="…"` that is located in the standard (aka “light”) DOM.

I will not go into great detail about that, but you can read more here:

- [W3C: cross-root ARIA](https://w3c.github.io/webcomponents-cg/#cross-root-aria)
- [WHATWG: element reflection ticket](https://github.com/whatwg/html/issues/6063)

<pre><code class="language-javascript">// ===========================
// Helper: set animation flag.
// ===========================

&#95;setAnimationFlag() {
  this.&#95;isAnimated = this.getAttribute(ANIMATED) !== FALSE;
}

// =======================
// Helper: add close text.
// =======================

&#95;setCloseTitle() {
  // Get title.
  const title = this.getAttribute(CLOSE) || CLOSE&#95;TITLE;

  // Set title.
  this.&#95;buttonClose.title = title;
  this.&#95;buttonClose.setAttribute(ARIA&#95;LABEL, title);
}

// ========================
// Helper: add modal label.
// ========================

&#95;setModalLabel() {
  // Set later.
  let label = MODAL&#95;LABEL&#95;FALLBACK;

  // Heading exists?
  if (this.&#95;heading) {
    // Get text.
    label = this.&#95;heading.textContent || label;
    label = label.trim().replace(SPACE&#95;REGEX, SPACE);
  }

  // Set label.
  this.&#95;modal.setAttribute(ARIA&#95;LABEL, label);
}

// ========================
// Helper: set active flag.
// ========================

&#95;setActiveFlag() {
  // Get flag.
  const isActive = this.getAttribute(ACTIVE) === TRUE;

  // Set flag.
  this.&#95;isActive = isActive;

  // Set display.
  this.&#95;toggleModalDisplay(() =&gt; {
    // Focus modal?
    if (this.&#95;isActive) {
      this.&#95;focusModal();
    }
  });
}

// ========================
// Helper: set static flag.
// ========================

&#95;setStaticFlag() {
  this.&#95;isStatic = this.getAttribute(STATIC) === TRUE;
}</code></pre>

### Focusing Specific Elements

The `_focusElement` function allows us to focus an element that may have been active before a modal became active. Whereas the `_focusModal` function will place focus on the modal dialog itself and will ensure that the modal backdrop is scrolled to the top.

<pre><code class="language-javascript">// ======================
// Helper: focus element.
// ======================

&#95;focusElement(element: HTMLElement) {
  window.requestAnimationFrame(() =&gt; {
    if (typeof element.focus === FUNCTION) {
      element.focus();
    }
  });
}

// ====================
// Helper: focus modal.
// ====================

&#95;focusModal() {
  window.requestAnimationFrame(() =&gt; {
    this.&#95;modal.focus();
    this.&#95;modalScroll.scrollTo(0, 0);
  });
}</code></pre>

### Detecting “Outside” Modal

This function is handy to know if an element resides outside the parent `<cta-modal>` tag. It returns a boolean, which we can use to take appropriate action. Namely, tab trapping navigation inside the modal while it is active.

<div class="break-out">

<pre><code class="language-javascript">// =============================
// Helper: detect outside modal.
// =============================

&#95;isOutsideModal(element?: HTMLElement) {
  // Early exit.
  if (!this.&#95;isActive || !element) {
    return false;
  }

  // Has element?
  const hasElement = this.contains(element) || this.&#95;modal.contains(element);

  // Get boolean.
  const bool = !hasElement;

  // Expose boolean.
  return bool;
}</code></pre>
</div>

### Detecting Motion Preference

Here, we reuse our variable from before (also used in our CSS) to detect if a user is okay with motion. That is, they have not explicitly set `prefers-reduced-motion` to `reduce` via their operating system preferences.

The returned boolean is a combination of that check, plus the `animated="false"` flag not being set on `<cta-modal>`.

<pre><code class="language-javascript">// ===========================
// Helper: detect motion pref.
// ===========================

&#95;isMotionOkay() {
  // Get pref.
  const { matches } = window.matchMedia(PREFERS_REDUCED_MOTION);

  // Expose boolean.
  return this.&#95;isAnimated && !matches;
}</code></pre>

### Toggling Modal Show/Hide

There is quite a bit going on in this function, but in essence, it is pretty simple.

- **If the modal is not active, show it.** If animation is allowed, animate it into place.
- **If the modal is active, hide it.** If animation is allowed, animate it disappearing.

We also cache the currently active element, so that when the modal closes we can restore focus.

The variables used in our CSS earlier are also used here:

- `ANIMATION_DURATION`,
- `DATA_SHOW`,
- `DATA_HIDE`.

<div class="break-out">

<pre><code class="language-javascript">// =====================
// Helper: toggle modal.
// =====================

&#95;toggleModalDisplay(callback: () =&gt; void) {
  // @ts-expect-error boolean
  this.setAttribute(ACTIVE, this.&#95;isActive);

  // Get booleans.
  const isModalVisible = this.&#95;modalScroll.style.display === BLOCK;
  const isMotionOkay = this.&#95;isMotionOkay();

  // Get delay.
  const delay = isMotionOkay ? ANIMATION&#95;DURATION : 0;

  // Get scrollbar width.
  const scrollbarWidth = window.innerWidth - document.documentElement.clientWidth;

  // Get active element.
  const activeElement = document.activeElement as HTMLElement;

  // Cache active element?
  if (this.&#95;isActive && activeElement) {
    this.&#95;activeElement = activeElement;
  }

  // =============
  // Modal active?
  // =============

  if (this.&#95;isActive) {
    // Show modal.
    this.&#95;modalScroll.style.display = BLOCK;

    // Hide scrollbar.
    document.documentElement.style.overflow = HIDDEN;

    // Add placeholder?
    if (scrollbarWidth) {
      document.documentElement.style.paddingRight = `${scrollbarWidth}px`;
    }

    // Set flag.
    if (isMotionOkay) {
      this.&#95;isHideShow = true;
      this.&#95;modalScroll.setAttribute(DATA&#95;SHOW, TRUE);
    }

    // Fire callback.
    callback();

    // Await CSS animation.
    this.&#95;timerForShow = window.setTimeout(() =&gt; {
      // Clear.
      clearTimeout(this.&#95;timerForShow);

      // Remove flag.
      this.&#95;isHideShow = false;
      this.&#95;modalScroll.removeAttribute(DATA&#95;SHOW);

      // Delay.
    }, delay);

    /&#42;
    =====
    NOTE:
    =====

      We want to ensure that the modal is currently
      visible because we do not want to put scroll
      back on the `&lt;html&gt;` element unnecessarily.

      The reason is that another `&lt;cta-modal&gt;` in
      the page might have been pre-rendered with an
      [active="true"] attribute. If so, we want to
      leave the page's overflow value alone.
    &#42;/
  } else if (isModalVisible) {
    // Set flag.
    if (isMotionOkay) {
      this.&#95;isHideShow = true;
      this.&#95;modalScroll.setAttribute(DATA&#95;HIDE, TRUE);
    }

    // Fire callback?
    callback();

    // Await CSS animation.
    this.&#95;timerForHide = window.setTimeout(() =&gt; {
      // Clear.
      clearTimeout(this.&#95;timerForHide);

      // Remove flag.
      this.&#95;isHideShow = false;
      this.&#95;modalScroll.removeAttribute(DATA&#95;HIDE);

      // Hide modal.
      this.&#95;modalScroll.style.display = NONE;

      // Show scrollbar.
      document.documentElement.style.overflow = EMPTY&#95;STRING;

      // Remove placeholder.
      document.documentElement.style.paddingRight = EMPTY&#95;STRING;

      // Delay.
    }, delay);
  }
}</code></pre>
</div>

### Handle Event: Click Overlay

When clicking on the semi-transparent overlay, assuming that `static="true"` is not set on the `<cta-modal>` tag, we close the modal.

<pre><code class="language-javascript">// =====================
// Event: overlay click.
// =====================

&#95;handleClickOverlay(event: MouseEvent) {
  // Early exit.
  if (this.&#95;isHideShow || this.&#95;isStatic) {
    return;
  }

  // Get layer.
  const target = event.target as HTMLElement;

  // Outside modal?
  if (target.classList.contains('cta-modal&#95;&#95;overlay')) {
    this.&#95;handleClickToggle();
  }
}</code></pre>

### Handle Event: Click Toggle

This function uses [event delegation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_delegation) on the `<div slot="button">` and `<div slot="modal">` elements. Whenever a child element with the class `cta-modal-toggle` is triggered, it will cause the active state of the modal to change.

This includes listening for various events that are considered activating a button:

- mouse clicks,
- pressing the `enter` key,
- pressing the `spacebar` key.

<div class="break-out">

<pre><code class="language-javascript">// ====================
// Event: toggle modal.
// ====================

&#95;handleClickToggle(event?: MouseEvent | KeyboardEvent) {
  // Set later.
  let key = EMPTY_STRING;
  let target = null;

  // Event exists?
  if (event) {
    if (event.target) {
      target = event.target as HTMLElement;
    }

    // Get key.
    if ((event as KeyboardEvent).key) {
      key = (event as KeyboardEvent).key;
      key = key.toLowerCase();
    }
  }

  // Set later.
  let button;

  // Target exists?
  if (target) {
    // Direct click.
    if (target.classList.contains('cta-modal&#95;&#95;close')) {
      button = target as HTMLButtonElement;

      // Delegated click.
    } else if (typeof target.closest === FUNCTION) {
      button = target.closest('.cta-modal-toggle') as HTMLButtonElement;
    }
  }

  // Get booleans.
  const isValidEvent = event && typeof event.preventDefault === FUNCTION;
  const isValidClick = button && isValidEvent && !key;
  const isValidKey = button && isValidEvent && [ENTER, SPACE].includes(key);

  const isButtonDisabled = button && button.disabled;
  const isButtonMissing = isValidEvent && !button;
  const isWrongKeyEvent = key && !isValidKey;

  // Early exit.
  if (isButtonDisabled || isButtonMissing || isWrongKeyEvent) {
    return;
  }

  // Prevent default?
  if (isValidKey || isValidClick) {
    event.preventDefault();
  }

  // Set flag.
  this.&#95;isActive = !this.&#95;isActive;

  // Set display.
  this.&#95;toggleModalDisplay(() =&gt; {
    // Focus modal?
    if (this.&#95;isActive) {
      this.&#95;focusModal();

      // Return focus?
    } else if (this.&#95;activeElement) {
      this.&#95;focusElement(this.&#95;activeElement);
    }
  });
}</code></pre>
</div>

{{% ad-panel-leaderboard %}}

### Handle Event: Focus Element

This function is triggered whenever an element receives `focus` on the page. Depending on the state of the modal, and which element was focused, we can trap tab navigation within the modal dialog. This is where our `FOCUSABLE_SELECTORS` from early comes into play.

<div class="break-out">

<pre><code class="language-javascript">// =========================
// Event: focus in document.
// =========================

&#95;handleFocusIn() {
  // Early exit.
  if (!this.&#95;isActive) {
    return;
  }

  // prettier-ignore
  const activeElement = (
    // Get active element.
    this.&#95;shadow.activeElement ||
    document.activeElement
  ) as HTMLElement;

  // Get booleans.
  const isFocusTrap1 = activeElement === this.&#95;focusTrapList[0];
  const isFocusTrap2 = activeElement === this.&#95;focusTrapList[1];

  // Set later.
  let focusListReal: HTMLElement[] = [];

  // Slot exists?
  if (this.&#95;slotForModal) {
    // Get "real" elements.
    focusListReal = Array.from(
      this.&#95;slotForModal.querySelectorAll(FOCUSABLE&#95;SELECTORS)
    ) as HTMLElement[];
  }

  // Get "shadow" elements.
  const focusListShadow = Array.from(
    this.&#95;modal.querySelectorAll(FOCUSABLE&#95;SELECTORS)
  ) as HTMLElement[];

  // Get "total" elements.
  const focusListTotal = focusListShadow.concat(focusListReal);

  // Get first & last items.
  const focusItemFirst = focusListTotal[0];
  const focusItemLast = focusListTotal[focusListTotal.length - 1];

  // Focus trap: above?
  if (isFocusTrap1 && focusItemLast) {
    this.&#95;focusElement(focusItemLast);

    // Focus trap: below?
  } else if (isFocusTrap2 && focusItemFirst) {
    this.&#95;focusElement(focusItemFirst);

    // Outside modal?
  } else if (this.&#95;isOutsideModal(activeElement)) {
    this.&#95;focusModal();
  }
}</code></pre>
</div>

### Handle Event: Keyboard

If a modal is active when the `escape` key is pressed, it will be closed. If the `tab` key is pressed, we evaluate whether or not we need to adjust which element is focused.

<pre><code class="language-javascript">// =================
// Event: key press.
// =================

&#95;handleKeyDown({ key }: KeyboardEvent) {
  // Early exit.
  if (!this.&#95;isActive) {
    return;
  }

  // Get key.
  key = key.toLowerCase();

  // Escape key?
  if (key === ESCAPE && !this.&#95;isHideShow && !this.&#95;isStatic) {
    this.&#95;handleClickToggle();
  }

  // Tab key?
  if (key === TAB) {
    this.&#95;handleFocusIn();
  }
}</code></pre>

### DOM Loaded Callback

This event listener tells the window to wait for the DOM (HTML page) to be loaded, and then parses it for any instances of `<cta-modal>` and attaches our JS interactivity to it. Essentially, we have created a new HTML tag and now the browser knows how to use it.

<pre><code class="language-javascript">// ===============
// Define element.
// ===============

window.addEventListener('DOMContentLoaded', () =&gt; {
  window.customElements.define('cta-modal', CtaModal);
});</code></pre>

## Build Time Optimization

I will not go into great detail about this aspect, but I think it is worth calling out.

After transpiling from TypeScript to JavaScript, I run [Terser](https://terser.org/) against the JS output. All the aforementioned functions that begin with an underscore (`_`) are marked as safe to mangle. That is, they go from being named `_bind` and `_addEvents` to single letters instead.

That step brings the file size down considerably. Then I run the minified output through a [minifyWebComponent.js](https://github.com/nathansmith/cta-modal/blob/main/scripts/minifyWebComponent.js) process that I created, which compresses the embedded `<style>` and markup even further.

For example, class names and other attributes (and selectors) are minified. This happens in the CSS and HTML.

- `class='cta-modal__overlay'` becomes `class=o`. The quotes are removed as well because the browser does not technically need them to understand the intent.
- The one CSS selector that is left untouched is `[tabindex="0"]`, because removing the quotes from around the `0` seemingly makes it invalid when parsed by `querySelectorAll`. However, it is safe to minify within HTML from `tabindex='0'` to `tabindex=0`.

When it is all said and done, the file size reduction looks like this (in bytes):

- un-minified: 16,849,
- terser minify: 10,230,
- and my script: 7,689.

To put that into perspective, the `favicon.ico` file on Smashing Magazine is 4,286 bytes. So, we are not really adding much overhead at all, for a lot of functionality that only requires writing HTML to use.

## Conclusion

If you have read this far, thanks for sticking with me. I hope that I have at least piqued your interest in Web Components!

I know we covered quite a bit, but the good news is: That is all there is to it. There are no frameworks to learn unless you want to. Realistically, you can get started writing your own Web Components using vanilla JS without a build process.

There really has never been a better time to `#UseThePlatform`. I look forward to seeing what you imagine.

### Further Reading

I would be remiss if I did not mention that there are a myriad of other modal options out there.

While I am biased and feel my approach brings something unique to the table &mdash; otherwise I would not have tried to “reinvent the wheel” &mdash; you may find that one of these will better suit your needs.

The following examples differ from CTA Modal in that they all require at least ***some*** additional JavaScript to be written by the end-user developer. Whereas with CTA Modal, all you have to author is the HTML code.

**Flat HTML & JS:**

- [a11y-dialog](https://a11y-dialog.netlify.app)
- [Bootstrap modal](https://getbootstrap.com/docs/5.1/components/modal)
- [Micromodal](https://micromodal.vercel.app)

**Web Components:**

- [aria-modal](https://keiya01.github.io/aria-modal-doc/top)
- [web-dialog](https://github.com/andreasbm/web-dialog) with [@a11y/focus-trap](https://appnest-demo.firebaseapp.com/focus-trap)

**jQuery:**

- [jQuery Modal](https://jquerymodal.com)
- [Lightbox](https://lokeshdhakar.com/projects/lightbox2)
- [Thickbox](http://codylindley.com/thickbox)

**React:**

- [React Modal](https://reactcommunity.org/react-modal)

**Vue:**

- [Vue.js Modal](http://vue-js-modal.yev.io)

<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

{{< signature "mb, vf, yk, il" >}}

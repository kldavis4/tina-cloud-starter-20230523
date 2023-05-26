---
title: How To Make Modal Windows Better For Everyone
slug: making-modal-windows-better-for-everyone
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/38864008-4af6-4362-b3b5-e2fde4b5ffaa/illu-modals.jpg'
date: 2014-09-15T19:23:29.000Z
author: scottohara
description: >-
  To you, [modal
  windows](https://www.smashingmagazine.com/2009/05/27/modal-windows-in-modern-web-design/)
  might be a blessing of additional screen real estate, providing a way to
  deliver contextual information, notifications and other actions relevant to
  the current screen. On the other hand, modals might feel like a hack that
  you’ve been forced to commit in order to cram extra content on the screen.
  These are the extreme ends of the spectrum, and users are caught in the
  middle. Depending on how a user browses the Internet, modal windows can be
  downright confusing.
categories:
  - Accessibility
  - JavaScript
  - UX
  - Semantics
last_updated: 2021-08-10T11:30:00.000Z
---
To you, <a href="https://www.smashingmagazine.com/2009/05/27/modal-windows-in-modern-web-design/">modal windows</a> might be a blessing of additional screen real estate, providing a way to deliver contextual information, notifications and other actions relevant to the current screen. On the other hand, modals might feel like a hack that you’ve been forced to commit in order to cram extra content on the screen. These are the extreme ends of the spectrum, and users are caught in the middle. Depending on how a user browses the Internet, <strong>modal windows can be downright confusing</strong>.

Modals quickly shift visual focus from one part of a website or application to another area of (hopefully related) content. The action is usually not jarring if initiated by the user, but it can be annoying and disorienting if it occurs automatically, as happens with the modal window’s evil cousins, the “nag screen” and the “interstitial.”

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Modal Windows In Modern Web Design](https://www.smashingmagazine.com/2009/05/modal-windows-in-modern-web-design/)
*   [New Approaches To Designing Log-In Forms](https://www.smashingmagazine.com/2011/08/new-approaches-to-designing-login-forms/)
*   [Innovative Techniques To Simplify Sign-Ups And Log-Ins](https://www.smashingmagazine.com/2011/05/innovative-techniques-to-simplify-signups-and-logins/)
*   [<span class="headline">Better Interface Design: Logins, Menus And Other Fancy Modules</span>](https://www.smashingmagazine.com/2016/04/inspiring-ui-demos-logins-menus-toggles-and-more/)

However, modals are merely a mild annoyance in the end, right? The user just has to click the “close” button, quickly skim some content or fill out a form to dismiss it.

{{% feature-panel %}}

Well, imagine that you had to navigate the web with a keyboard. Suppose that a modal window appeared on the screen, and you had very little context to know what it is and why it’s obscuring the content you’re trying to browse. Now you’re wondering, “How do I interact with this?” or “How do I get rid of it?” because your keyboard’s focus hasn’t automatically moved to the modal window.

This scenario is more common than it should be. And it’s fairly easy to solve, as long as we make our content accessible to all through sound usability practices.

For an example, I’ve set up a <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3987b0ea-3723-43cc-8b03-334eefdb8bf2/inaccessible.html">demo of an inaccessible modal window</a> that appears on page load and that isn’t entirely semantic. First, interact with it using your mouse to see that it actually works. Then, try interacting with it using only your keyboard.</p>

## Better Semantics Lead To Better Usability And Accessibility

Usability and accessibility are lacking in many modal windows. Whether they’re used to provide additional actions or inputs for interaction with the page, to include more information about a particular section of content, or to provide notifications that can be easily dismissed, modals need to be easy for everyone to use.

To achieve this goal, first we must focus on the semantics of the modal’s markup. This might seem like a no-brainer, but the step is not always followed.

Suppose that a popular gaming website has a full-page modal overlay and has implemented a “close” button with the code below:

<pre><code class="language-markup">&lt;div id="modal_overlay"&gt;
  &lt;div id="modal_close" onClick="modalClose()"&gt;
    X
  &lt;/div&gt;
  …
&lt;/div&gt;
</code></pre>

This <code>div</code> element has no semantic meaning behind it. Sighted visitors will know that this is a “close” button because it looks like one. It has a hover state, so there is some visual indication that it can be interacted with.

But this element has no inherit semantic meaning to people who use a keyboard or screen reader.

There’s no default way to enable users to tab to a <code>div</code> without adding a <code>tabindex</code> attribute to it. However, we would also need to add a <code>:focus</code> state to visually indicate that it is the active element. That still doesn’t give screen readers enough information for users to discern the element’s meaning. An “X” is the only label here. While we can assume that people who use screen readers would know that the letter “X” means “close,” if it was a multiplication sign (using the HTML entity <code>&amp;times;</code>) or a cross mark (<code>❌</code>), then some screen readers wouldn’t read it at all. We need a better fallback.

We can circumvent all of these issues simply by writing the correct, semantic markup for a button and by adding an ARIA label for screen readers:

<pre><code class="language-markup">&lt;div id="modal_overlay"&gt;
  &lt;button type="button" class="btn-close" id="modal_close" aria-label="close"&gt;
    X
  &lt;/button&gt;
&lt;/div&gt;
</code></pre>

By changing the <code>div</code> to a button, we’ve significantly improved the semantics of our “close” button. We’ve addressed the common expectation that the button can be tabbed to with a keyboard and appear focused, and we’ve provided context by adding the ARIA label for screen readers.

That’s just one example of how to make the markup of our modals more semantic, but we can do a lot more to create a useful and accessible experience.</p>

## Making Modals More Usable And Accessible

Semantic markup goes a long way to building a fully usable and accessible modal window, but still more CSS and JavaScript can take the experience to the next level.</p>

### Including Focus States

Provide a focus state! This obviously isn’t exclusive to modal windows; many elements lack a proper focus state in some form or another beyond the browser’s basic default one (which may or may not have been cleared by your CSS reset). At the very least, pair the focus state with the hover state you’ve already designed:

<pre><code class="language-css">.btn:hover, .btn:focus {
  background: #f00;
}
</code></pre>

However, because focusing and hovering are different types of interaction, giving the focus state its own style makes sense.

<pre><code class="language-css">.btn:hover {
  background: #f00;
}

:focus {
  box-shadow: 0 0 3px rgba(0,0,0,.75);
}
</code></pre>

Really, any item that can be focused should have a focus state. Keep that in mind if you’re extending the browser’s default dotted outline.</p>

### Saving Last Active Element

When a modal window loads, the element that the user last interacted with should be saved. That way, when the modal window closes and the user returns to where they were, the focus on that element will have been maintained. Think of it like a bookmark. Without it, when the user closes the modal, they would be sent back to the beginning of the document, left to find their place. Add the following to your modal’s opening and closing functions to save and reenable the user’s focus.

<pre><code class="language-javascript">var lastFocus;

function modalShow () {
  lastFocus = document.activeElement;
}

function modalClose () {
  lastFocus.focus(); // place focus on the saved element
}
</code></pre>

### Shifting Focus

When the modal loads, focus should shift from the last active element either to the modal window itself or to the first interactive element in the modal, such as an input element. This will make the modal more usable because sighted visitors won’t have to reach for their mouse to click on the first element, and keyboard users won’t have to tab through a bunch of DOM elements to get there.

<pre><code class="language-javascript">var modal = document.getElementById('your-modal-id-here');

function modalShow () {
   modal.setAttribute('tabindex', '0');
   modal.focus();
}
</code></pre>

### Going Full Screen

If your modal takes over the full screen, then obscure the contents of the main document for both sighted users and screen reader users. Without this happening, a keyboard user could easily tab their way outside of the modal without realizing it, which could lead to them interacting with the main document before completing whatever the modal window is asking them to do.

Use the following JavaScript to confine the user’s focus to the modal window until it is dismissed:

<pre><code class="language-javascript">function focusRestrict ( event ) {
  document.addEventListener('focus', function( event ) {
    if ( modalOpen &amp;&amp; !modal.contains( event.target ) ) {
      event.stopPropagation();
      modal.focus();
    }
  }, true);
}
</code></pre>

While we want to prevent users from tabbing through the rest of the document while a modal is open, we don’t want to prevent them from accessing the browser’s chrome (after all, sighted users wouldn’t expect to be stuck in the browser’s tab while a modal window is open). The JavaScript above prevents tabbing to the document’s content outside of the modal window, instead bringing the user to the top of the modal.

If we also put the modal at the top of the DOM tree, as the first child of <code>body</code>, then hitting <kbd>Shift + Tab</kbd> would take the user out of the modal and into the browser’s chrome. If you’re not able to change the modal’s location in the DOM tree, then use the following JavaScript instead:

<pre><code class="language-javascript">var m = document.getElementById('modal_window'),
    p = document.getElementById('page');

// Remember that &lt;div id="page"&gt; surrounds the whole document,
// so aria-hidden="true" can be applied to it when the modal opens.

function swap () {
  p.parentNode.insertBefore(m, p);
}

swap();
</code></pre>

If you can’t move the modal in the DOM tree or reposition it with JavaScript, you still have other options for confining focus to the modal. You could keep track of the first and last focusable elements in the modal window. When the user reaches the last one and hits <kbd>Tab</kbd>, you could shift focus back to the top of the modal. (And you would do the opposite for <kbd>Shift + Tab</kbd>.)

A second option would be to create a list of all focusable nodes in the modal window and, upon the modal firing, allow for tabbing only through those nodes.

A third option would be to find all focusable nodes outside of the modal and set <code>tabindex="-1"</code> on them.

The problem with these first and second options is that they render the browser’s chrome inaccessible. If you must take this route, then adding a well-marked “close” button to the modal and supporting the <kbd>Escape</kbd> key are critical; without them, you will effectively trap keyboard users on the website.

The third option allows for tabbing within the modal and the browser’s chrome, but it comes with the performance cost of listing all focusable elements on the page and negating their ability to be focused. The cost might not be much on a small page, but on a page with many links and form elements, it can become quite a chore. Not to mention, when the modal closes, you would need to return all elements to their previous state.

Clearly, we have a lot to consider to enable users to effectively tab within a modal.</p>

### Dismissing

Finally, modals should be easy to dismiss. Standard <code>alert()</code> modal dialogs can be closed by hitting the <kbd>Escape</kbd> key, so following suit with our modal would be expected — and a convenience. If your modal has multiple focusable elements, allowing the user to just hit <kbd>Escape</kbd> is much better than forcing them to tab through content to get to the “close” button.

<pre><code class="language-javascript">function modalClose ( e ) {
  if ( !e.keyCode || e.keyCode === 27 ) {
    // code to close modal goes here
  }
}

document.addEventListener('keydown', modalClose);
</code></pre>

Moreover, closing a full-screen modal when the overlay is clicked is conventional. The exception is if you don’t want to close the modal until the user has performed an action.

Use the following JavaScript to close the modal when the user clicks on the overlay:

<pre><code class="language-javascript">mOverlay.addEventListener('click', function( e )
  if (e.target == modal.parentNode)
    modalClose( e );
  }
}, false);
</code></pre>

## Additional Accessibility Steps

Beyond the usability steps covered above, <a href="https://www.w3.org/TR/wai-aria/">ARIA roles, states and properties</a> will add yet more hooks for assistive technologies. For some of these, nothing more is required than adding the corresponding attribute to your markup; for others, additional JavaScript is required to control an element’s state.</p>

### aria-hidden

Use the <code>aria-hidden</code> attribute. By toggling the value <code>true</code> and <code>false</code>, the element and any of its children will be either hidden or visible to screen readers. However, as with all ARIA attributes, it carries no default style and, thus, will not be hidden from sighted users. To hide it, add the following CSS:

<pre><code class="language-css">.modal-window[aria-hidden="true"] {
  display: none;
}
</code></pre>

Notice that the selector is pretty specific here. The reason is that we might not want all elements with <code>aria-hidden="true"</code> to be hidden (as with our earlier example of the “X” for the “close” button).</p>

### role="dialog"

Add <code>role="dialog"</code> to the element that contains the modal’s content. This tells assistive technologies that the content requires the user’s response or confirmation. Again, couple this with the JavaScript that shifts focus from the last active element in the document to the modal or to the first focusable element in the modal.

However, if the modal is more of an error or alert message that requires the user to input something before proceeding, then use <code>role="alertdialog"</code> instead. Again, set the focus on it automatically with JavaScript, and confine focus to the modal until action is taken.</p>

### aria-label

Use the <code>aria-label</code> or <code>aria-labelledby</code> attribute along with <code>role="dialog"</code>. If your modal window has a heading, you can use the <code>aria-labelledby</code> attribute to point to it by referencing the heading’s ID. If your modal doesn’t have a heading for some reason, then you can at least use the <code>aria-label</code> to provide a concise label about the element that screen readers can parse.</p>

## What About HTML5’s Dialog Element?

Chrome 37 beta and Firefox Nightly 34.0a1 support the <code>dialog</code> element, which provides extra semantic and accessibility information for modal windows. Once this native <code>dialog</code> element is established, we won’t need to apply <code>role="dialog"</code> to non-dialog elements. For now, even if you’re using a polyfill for the <code>dialog</code> element, also use <code>role="dialog"</code> so that screen readers know how to handle the element.

The exciting thing about this element is not only that it serves the semantic function of a dialog, but that it come with its own methods, which will replace the JavaScript and CSS that we currently need to write.

For instance, to display or dismiss a dialog, we’d write this base of JavaScript:

<pre><code class="language-javascript">var modal = document.getElementById('myModal'),
  openModal = document.getElementById('btnOpen'),
  closeModal = document.getElementById('btnClose');

// to show our modal
openModal.addEventListener( 'click', function( e ) {
  modal.show();
  // or
  modal.showModal();
});

// to close our modal
closeModal.addEventListener( 'click', function( e ) {
  modal.close();
});
</code></pre>

The <code>show()</code> method launches the dialog, while still allowing users to interact with other elements on the page. The <code>showModal()</code> method launches the dialog and prevents users from interacting with anything but the modal while it’s open.

The <code>dialog</code> element also has the <code>open</code> property, set to <code>true</code> or <code>false</code>, which replaces <code>aria-hidden</code>. And it has its own <code>::backdrop</code> pseudo-element, which enables us to style the modal when it is opened with the <code>showModal()</code> method.

There’s more to learn about the <code>dialog</code> element than what’s mentioned here. It might not be ready for prime time, but once it is, this semantic element will go a long way to helping us develop usable, accessible experiences.</p>

## Where To Go From Here?

Whether you use a jQuery plugin or a homegrown solution, step back and evaluate your modal’s overall usability and accessibility. As minor as modals are to the web overall, they are common enough that if we all tried to make them friendlier and more accessible, we’d make the web a better place.

I’ve prepared a <a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6793fff0-3ca1-4c05-b383-81aa8c9163e8/accessible.html">demo of a modal window</a> that implements all of the accessibility features covered in this article.

{{< signature "hp, il, al, ml" >}}


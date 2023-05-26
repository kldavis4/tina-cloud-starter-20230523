---
title: Building Inclusive Toggle Buttons
author: heydon-pickering
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f8ba49f4-bb76-4bce-a3b6-a04019952362/labels-preview-500-opt.png
date: 2017-09-19T19:26:20.000Z
slug: building-inclusive-toggle-buttons
summary: >-
  Toggle buttons are one of the simpler design patterns out there, often based
  on just one element. But it’s still easy to design them badly. Making them
  inclusive is a question of language, visual design, markup, and behavior.
description: >-
  Toggle buttons are one of the simpler design patterns out there, often based
  on just one element. But it’s still easy to design them badly. Making them
  inclusive is a question of language, visual design, markup, and behavior.
categories:
  - Coding
---
In this inaugural post, I’ll be exploring what it takes to make toggle buttons inclusive. As with any component, there’s no one way to go about this, especially when such controls are examined under different contexts. However, there’s certainly plenty to forget to do or to otherwise screw up, so let’s try to avoid any of that.

<div class="c-felix-the-cat">
<h4 class="h3">Improving Interface Design</h4>
<p>Did you know that with just a few simple tricks, you can help make a user’s interaction more pleasant? We've got your back, with an inspiring list of dialog and modal windows, signup and login screens, navigation and menus, and even more sliders and toggles. <a href="https://www.smashingmagazine.com/2016/04/inspiring-ui-demos-logins-menus-toggles-and-more/" class="btn btn--medium btn--blue">Read a related article →</a></p>
</div>

## Changing State

If a web application did not change according to the instructions of its user, the resulting experience would be altogether unsatisfactory. Nevertheless, the luxury of being able to make web documents augment themselves instantaneously, without recourse to a page refresh, has not always been present.

{{% feature-panel %}}

Unfortunately, somewhere along the way we decided that accessible web pages were only those where very little happened — static documents, designed purely to be read. Accordingly, we made little effort to make the richer, _stateful_ experiences of web applications inclusive.

A popular misconception has been that screen readers _don’t understand_ JavaScript. Not only is this entirely untrue — all major screen readers react to changes in the DOM as they occur — but basic state changes, communicated both visually and to assistive technology software, do not necessarily depend on JavaScript to take place anyway.</p>

## Checkboxes And Radio Buttons

Form elements are the primitives of interactive web pages and, where we’re not employing them directly, we should be paying close attention to how they behave. Their handling of state changes have established usability conventions we would be foolish to ignore.

Arguably, an out-of-the-box input of the `checkbox` type is a perfectly serviceable on/off switch all its own. Where labelled correctly, it has all the fundamental ingredients of an accessible control: it’s screen reader and keyboard accessible between platforms and devices, and it communicates its change of state (_checked_ to _unchecked_ or vice versa) without needing to rebuild the entire document.

In the following example, a checkbox serves as the toggle for an email notifications setting.

<pre><code class="language-html">&lt;input type="checkbox" id="notify" name="notify" value="on"&gt;  
&lt;label for="notify"&gt;Notify by email&lt;/label&gt;  
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70fbb963-cdca-462d-b668-41cd9aff0c3a/1-notify-by-email-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/70fbb963-cdca-462d-b668-41cd9aff0c3a/1-notify-by-email-preview-opt.png" width="703" height="100" alt="The notify my email control with checkbox checked" /></a></figure>

Screen reader software is fairly uniform in its interpretation of this control. On focusing the control (moving to it using the **Tab** key) something similar to, _"Notify by email, checkbox, unchecked"_ will be announced. That’s the label, role, and state information all present.

On checking the checkbox, most screen reader software will announce the changed state, “checked” (sometimes repeating the label and role information too), immediately. Without JavaScript, we’ve handled state and screen reader software is able to feed back to the user.</p>

### Screen readers are not just for the blind

Some operate screen readers to assist their understanding of an interface. Others may be visually dyslexic or have low literacy. There are even those who have little physical or cognitive trouble understanding an interface who simply prefer to have it read out to them sometimes.

**Supporting screen reader software is supporting screen reader software, not blind people**. Screen readers are a tool a lot of different people like to use.

In this case, the on/off part of the switch is not communicated by the label but the state. Instead, the label is for identifying the thing that we are turning off or on. Should research show that users benefit from a more explicit on/off metaphor, a radio button group can be employed.

<pre><code class="language-html">&lt;fieldset&gt;  
  &lt;legend&gt;Notify by email&lt;/legend&gt;
  &lt;input type="radio" id="notify-on" name="notify" value="on" checked&gt;
  &lt;label for="notify-on"&gt;on&lt;/label&gt;
  &lt;input type="radio" id="notify-off" name="notify" value="off"&gt;
  &lt;label for="notify-off"&gt;off&lt;/label&gt;
&lt;/fieldset&gt;  
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7347680e-0cc9-44a0-a454-8374e0d45728/2-notify-by-email-radios-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7347680e-0cc9-44a0-a454-8374e0d45728/2-notify-by-email-radios-preview-opt.png" width="651" height="220" alt="Fieldset with notify by email group label (legend) and radio buttons labeled on and off. The on one is selected." /></a></figure>

Group labels are a powerful tool. As their name suggests, they can provide a single label to related (grouped) items. In this case, the `<fieldset>` group element works together with the `<legend>` element to provide the group label "Notify by email" to the pair of radio buttons. These buttons are made a pair by sharing a `name` attribute value, which makes it possible to toggle between them using your arrow keys. HTML semantics don’t just add information but also affect behavior.

In the Windows screen readers JAWS and NVDA, when the user focuses the first control, the group label is prepended to that control’s individual label and the grouped radio buttons are enumerated. In NVDA, the term "grouping" is appended to make things more explicit. In the above example, focusing the first (checked by default) radio button elicits, _"Notify by email, grouping, on radio button, checked, one of two"_.

Now, even though the checked state (announced as "selected" in some screen readers) is still being toggled, what we’re really allowing the user to do it switch between "on" and "off". Those are the two possible _lexical states_, if you will, for the composite control.</p>

### Styling form elements

Form elements are notoriously hard to style, but there are well-supported CSS techniques for styling radio and checkbox controls, as I wrote in _[Replacing Radio Buttons Without Replacing Radio Buttons](https://www.sitepoint.com/replacing-radio-buttons-without-replacing-radio-buttons/)_. For tips on how to style select elements and file inputs, consult _[WTF Forms?](https://wtfforms.com/)_ by Mark Otto.</p>

### This doesn’t quite feel right

Both the checkbox and radio button implementations are tenable as on/off controls. They are, after all, accessible by mouse, touch, keyboard, and assistive technology software across different devices, browsers, and operating systems.

But accessibility is only a part of inclusive design. These controls also have to _make sense_ to users; they have to play an unambiguous role within the interface.

The trouble with using form elements is their longstanding association with the collection of data. That is, checkboxes and radio buttons are established as controls for designating _values_. When a user checks a checkbox, they may just be switching a state, but they may _suspect_ they are also choosing a value for submission.

Whether you’re a sighted user looking at a checkbox, a screen reader user listening to its identity being announced, or both, its etymology is problematic. We expect toggle buttons to be buttons, but checkboxes and radio buttons are really inputs.</p>

## A True Toggle Button

Sometimes we use `<button>` elements to submit forms. To be fully compliant and reliable these buttons should take the `type` value of `submit`.

<pre><code class="language-javascript">&lt;button type="submit"&gt;Send&lt;/button&gt;  
</code></pre>

But these are only one variety of button, covering one use case. In truth, `<button>` elements can be used for all sorts of things, and not just in association with forms. They’re just _buttons_. We remind ourselves of this by giving them the `type` value of `button`.

<pre><code class="language-html">&lt;button type="button"&gt;Send&lt;/button&gt;  
</code></pre>

The generic button is your go-to element for changing anything within the interface (using JavaScript and without reloading the page) except one’s location within and between documents, which is the purview of links.

Next to links, buttons should be the interactive element you use most prolifically in web applications. They come prepackaged with the "button" role and are keyboard and screen reader accessible by default. Unlike some form elements, they are also trivial to style.

So how do we make a `<button>` a toggle button? It’s a case of using WAI-ARIA as a progressive enhancement. WAI-ARIA offers states that are not available in basic HTML, such as the _pressed_ state. Imagine a power switch for a computer. When it’s pressed — or pushed in — that denotes the computer is in its "on" state. When it’s unpressed — poking out — the computer must be off.

<pre><code class="language-html">&lt;button type="button" aria-pressed="true"&gt;  
  Notify by email
&lt;/button&gt;  
</code></pre>

WAI-ARIA state attributes like `aria-pressed` behave like booleans but, unlike standard HTML state attributes like `checked` they must have an explicit value of `true` or `false`. Just adding `aria-pressed` is not reliable. Also, the absence of the attribute would mean the _unpressed_ state would not be communicated (a button without the attribute is just a generic button).

You can use this control inside a form, or outside, depending on your needs. But if you do use it inside a form, the `type="button"` part is important. If it’s not there, some browsers will default to an implicit `type="submit"` and try to submit the form. You don’t have to use `event.preventDefault()` on `type="button"` controls to suppress form submission.

Switching the state from `true` (on) to `false` (off) can be done via a simple click handler. Since we are using a `<button>`, this event type can be triggered with a mouse click, a press of either the **Space** or **Enter** keys, or by tapping the button through a touch screen. Being responsive to each of these actions is something built into `<button>` elements as standard. If you consult the [HTMLButtonElement](https://developer.mozilla.org/en/docs/Web/API/HTMLButtonElement) interface, you’ll see that other properties, such as `disabled`, are also supported out-of-the-box. Where `<button>` elements are not used, these behaviors have to be emulated with bespoke scripting.

<pre><code class="language-javascript">const toggle = document.querySelector('[aria-pressed]');

toggle.addEventListener('click', (e) =&gt; {  
  let pressed = e.target.getAttribute('aria-pressed') === 'true';
  e.target.setAttribute('aria-pressed', String(!pressed));
});
</code></pre>

### A clearer state

An interesting thing happens when a button with the `aria-pressed` state is encountered by some screen readers: it is identified as a "toggle button" or, in some cases, "push button". The presence of the state attribute changes the button’s identity.

When focusing the example button with `aria-pressed="true"` using NVDA, the screen reader announces,_"Notify by email, toggle button, pressed"_. The "pressed" state is more apt than "checked", plus we eschew the form data input connotations. When the button is clicked, immediate feedback is offered in the form of _"not pressed"_.</p>

### Styling

The HTML we construct is an important part of the design work we do and the things we create for the web. I'm a strong believer in doing HTML First Prototyping™, making sure there’s a solid foundation for the styled and branded product.

In the case of our toggle button, this foundation includes the semantics and behavior to make the button interoperable with various input (e.g. voice activation software) and output (e.g. screen reader) devices. That’s possible using HTML, but CSS is needed to make the control understandable visually.

Form should follow function, which is simple to achieve in CSS: everything in our HTML that makes our simple toggle button function can also be used to give it form.

*   `<button>` → `button` element selector
*   `aria-pressed="true"` → `[aria-pressed="true"]` attribute selector.

In a consistent and, therefore, easy to understand interface, buttons should share a certain look. Buttons should all look like buttons. So, our basic toggle button styles should probably inherit from the `button` element block:

<pre><code class="language-css">/* For example... */
button {  
  color: white;
  background-color: #000;
  border-radius: 0.5rem;
  padding: 1em 2em;
}
</code></pre>

There are a number of ways we could visually denote "pressed". Interpreted literally, we might make the button look _pressed in_ using some inset `box-shadow`. Let’s employ an attribute selector for this:

<pre><code class="language-css">[aria-pressed="true"] {
  box-shadow: inset 0 0 0 0.15rem #000,
              inset 0.25em 0.25em 0 #fff;
}
</code></pre>

To complete the pressed/unpressed metaphor, we can use some positioning and `box-shadow` to make the unpressed button “poke out”. This block should appear above the `[aria-prressed="true"]` block in the cascade.

<pre><code class="language-css">[aria-pressed] {
  position: relative;
  top: -0.25rem;
  left: -0.25rem;
  box-shadow: 0.125em 0.125em 0 #fff,
              0.25em 0.25em #000;
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d372d13-3266-4346-8623-da90681fe31a/3-notify-by-email-aria-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d372d13-3266-4346-8623-da90681fe31a/3-notify-by-email-aria-preview-opt.png" width="702" height="130" alt="Left button, sticking out, is labeled aria-pressed equals false. Right button, visually depressed, is labelled aria-pressed equals true." /></a></figure>

(**Note:** This styling method is offered just as one idea. You may find that something more explicit, like the use of "on"/"off" labels in an example to follow, is better understood by more users.)

### Don’t rely on color alone

"On" is often denoted by a green color, and "off" by red. This is a well-established convention and there’s no harm in incorporating it. However, be careful not to *only* use color to describe the button’s two states. If you did, some color blind users would not be able to differentiate them.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/724d7a6e-d7cc-46b5-bbab-0302bc3b74c1/4-notify-by-email-colors-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/724d7a6e-d7cc-46b5-bbab-0302bc3b74c1/4-notify-by-email-colors-preview-opt.png" width="702" height="130" alt="The aria-pressed false button has a red background color and the aria-pressed true button has a green background color" /></a><figcaption>These versions of the control would fail <a href="https://www.w3.org/TR/2008/REC-WCAG20-20081211/#visual-audio-contrast-without-color">WCAG 2.0 1.4.1 Use Of Color (Level A)</a><br>
</figcaption></figure>

**Focus styles**

It’s important buttons, along with _all_ interactive components, have focus styles. Otherwise people navigating by keyboard cannot see which element is in their control and ready to be operated.

The best focus styles do not affect layout (the interface shouldn’t jiggle around distractingly when moving between elements). Typically, one would use `outline`, but `outline` only ever draws a box in most browsers. To fit a focus style around the curved corners of our button, a `box-shadow` is better. Since we are using `box-shadow` already, we have to be a bit careful: note the two comma-separated `box-shadow` styles in the pressed-and-also-focused state.

<pre><code class="language-css">/* Remove the default outline and
add the outset shadow */  
[aria-pressed]:focus {
  outline: none;
  box-shadow: 0 0 0 0.25rem yellow;
}

/* Make sure both the inset and
outset shadow are present */  
[aria-pressed="true"]:focus {
  box-shadow: 0 0 0 0.25rem yellow,
              inset 0 0 0 0.15rem #000,
              inset 0.25em 0.25em 0 #fff;  
}
</code></pre>

## Changing Labels

The previous toggle button design has a self-contained, unique label and differentiates between its two states using a change in attribution which elicits a style. What if we wanted to create a button that changes its label from “on” to “off” or “play” to “pause”?

It’s perfectly easy to do this in JavaScript, but there are a couple of things we need to be careful about.

1.  If the _label_ changes, what happens with the state?
2.  If the label is just “on” or “off” (“play” or “pause”; “active” or “inactive”) how do we know what the button actually controls?

In the previous toggle button example, the label described _what_ would be on or off. Where the “what” part is not consistent, confusion quickly ensues: once “off”/unpressed has become “on”/pressed, I have to unpress the “on” button to turn the “off” button back on. What?

As a rule of thumb, you should never change pressed state and label together. If the label changes, the button has already changed state in a sense, just not via explicit WAI-ARIA state management.

In the following example, just the label changes.

<pre><code class="language-javascript">const button = document.querySelector('button');

button.addEventListener('click', (e) =&gt; {  
  let text = e.target.textContent === 'Play' ? 'Pause' : 'Play';
  e.target.textContent = text;
});
</code></pre>

The problem with this method is that the label change is not announced as it happens. That is, when you click the play button, feedback equivalent to “pressed” is absent. Instead, you have to unfocus and refocus the button manually to hear that it has changed. Not an issue for sighted users, but less ergonomic for blind screen reader users.

Play/pause buttons usually switch between a play symbol (a triangle on its side) and a pause symbol (two vertical lines). We _could_ do this while keeping a consistent non-visual label and changing state.

<pre><code class="language-html">&lt;!-- Paused state --&gt;  
&lt;button type="button" aria-pressed="false" aria-label="play"&gt;  
  &amp;#x25b6;
&lt;/button&gt;

&lt;-- Playing state --&gt;  
&lt;button type="button" aria-pressed="true" aria-label="play"&gt;  
  &amp;#x23f8;
&lt;/button&gt;  
</code></pre>

Because `aria-label` overrides the unicode symbol text node, the paused button is announced as something similar to, _“Play button, not pressed”_ and the playing button as ,_“Play button, pressed”_.

This works pretty well, except for where voice recognition and activation is concerned. In voice recognition software, you typically need to identify buttons by vocalizing their labels. And if a user sees a pause symbol, their first inclination is to say “pause”, not “play”. For this reason, switching the label rather than the state is more robust here.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b011f1ed-4099-4c63-b2e3-59d94871e641/5-labels-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b011f1ed-4099-4c63-b2e3-59d94871e641/5-labels-preview-opt.png" width="600" height="562" alt="Three implementation examples. The first just changes label from play to pause and is okay. The second keeps the play label and changes state, which is incorrect because the pause button cannot be identified with voice recognition. The third changes label and state so the button becomes a pause button which is pressed, which is incorrect. Only use one of the first two implementations." /></a><figcaption>Never change label and state at the same time. In this example, that would result in a paused button in the pressed state. Since the video or audio would be playing at this point, the lexical "pause" state cannot be also be considered "pressed" on "on".
</figcaption></figure>

### Auxiliary labeling

In some circumstances, we may want to provide on/off switches which actually read “on/off”. The trick with these is making sure there is a clear association between each toggle switch and a respective, auxiliary label.

Imagine the email notification setting is grouped alongside other similar settings in a list. Each list item contains a description of the setting followed by an on/off switch. The on/off switch uses the terms “on” and “off” as part of its design. Some `<span>` elements are provided for styling.

<pre><code class="language-html">&lt;h2&gt;Notifications&lt;/h2&gt;  
&lt;ul&gt;  
  &lt;li&gt;
    Notify by email
    &lt;button&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
  &lt;li&gt;
    Notify by SMS
    &lt;button&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
  &lt;li&gt;
    Notify by fax
    &lt;button&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
  &lt;li&gt;
    Notify by smoke signal
    &lt;button&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
&lt;/ul&gt;  
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/262eacd1-2179-4edd-a67b-51c71b461fe9/6-notifications-list-preview-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/262eacd1-2179-4edd-a67b-51c71b461fe9/6-notifications-list-preview-opt.png" width="701" height="374" alt="A list of notifications settings with associated buttons reading with either on or off highlighted, depending on the state" /></a></figure>

The virtue of lists is that, both visually and non-visually, they group items together, showing they are related. Not only does this help comprehension, but lists also provide navigational shortcuts in some screen readers. For example, JAWS provides the **L** (list) and **I** (list item) quick keys for moving between and through lists.

Each ‘label’ and button is associated by belonging to a common list item. However, not providing an explicit, unique label is dangerous territory — especially where voice recognition is concerned. Using `aria-labelledby`, we can associate each button with the list’s text:

<pre><code class="language-html">&lt;h2&gt;Notifications&lt;/h2&gt;  
&lt;ul&gt;  
  &lt;li&gt;
    &lt;span id="notify-email"&gt;Notify by email&lt;/span&gt;
    &lt;button aria-labelledby="notify-email"&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
  &lt;li&gt;
    &lt;span id="notify-sms"&gt;Notify by SMS&lt;/span&gt;
    &lt;button aria-labelledby="notify-sms"&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
  &lt;li&gt;
    &lt;span id="notify-fax"&gt;Notify by fax&lt;/span&gt;
    &lt;button aria-labelledby="notify-fax"&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
  &lt;li&gt;
    &lt;span id="notify-smoke"&gt;Notify by smoke signal&lt;/span&gt;
    &lt;button aria-labelledby="notify-smoke"&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
&lt;/ul&gt;  
</code></pre>

Each `aria-labelledby` value matches the appropriate span `id`, forming the association and giving the button its unique label. It works much like a `<label>` element’s `for` attribute identifying a field’s `id`.

**The switch role**

Importantly, the ARIA label overrides each button’s textual content, meaning we can once again employ `aria-pressed` to communicate state. However, since these buttons are explicitly “on/off” switches, we can instead use the [WAI-ARIA switch role](https://www.w3.org/TR/wai-aria-1.1/#switch), which communicates state via `aria-checked`.

<pre><code class="language-html">&lt;h2&gt;Notifications&lt;/h2&gt;  
&lt;ul&gt;  
  &lt;li&gt;
    &lt;span id="notify-email"&gt;Notify by email&lt;/span&gt;
    &lt;button role="switch" aria-checked="true" aria-labelledby="notify-email"&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
  &lt;li&gt;
    &lt;span id="notify-sms"&gt;Notify by SMS&lt;/span&gt;
    &lt;button role="switch" aria-checked="true" aria-labelledby="notify-sms"&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
  &lt;li&gt;
    &lt;span id="notify-fax"&gt;Notify by fax&lt;/span&gt;
    &lt;button role="switch" aria-checked="false" aria-labelledby="notify-fax"&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
  &lt;li&gt;
    &lt;span id="notify-smoke"&gt;Notify by smoke signal&lt;/span&gt;
    &lt;button role="switch" aria-checked="false" aria-labelledby="notify-smoke"&gt;
      &lt;span&gt;on&lt;/span&gt;
      &lt;span&gt;off&lt;/span&gt;
    &lt;/button&gt;
  &lt;/li&gt;
&lt;/ul&gt;  
</code></pre>

How you would style the active state is quite up to you, but I’d personally save on writing class attributes to the `<span>`s with JavaScript. Instead, I’d write some CSS using pseudo classes to target the relevant span dependent on the state.

<pre><code class="language-css">[role="switch"][aria-checked="true"] :first-child,
[role="switch"][aria-checked="false"] :last-child {
  background: #000;
  color: #fff;
}
</code></pre>

**Traversing the settings**

Now let’s talk about navigating through this settings section using two different strategies: by **Tab** key (jumping between focusable elements only) and browsing by screen reader (moving through each element).

Even when navigating by **Tab** key, it’s not only the identity and state of the interactive elements you are focusing that will be announced in screen readers. For example, when you focus the first `<button>`, you’ll hear that it is a _switch_ with the label “Notify by email”, in its _on_ state. “Switch” is the role and `aria-checked="true"` is vocalized as “on” where this role is present.

**Switch role support**

The `switch` role is not quite as well supported as `aria-pressed`. For example, it is not recognized by the ChromeVox screen reader extension for Chrome.

However, ChromeVox _does_ support `aria-checked`. This means that, instead of _"Switch, Notify by email, on"_ being announced, _"Button, Notify by email, checked"_ is instead. This isn’t as evocative, but it is adequate. More than likely, it will simply be mistaken for a checkbox input.

Curiously, NVDA regards a button with `role="switch"` and `aria-checked="true"` as a toggle button in its pressed state. Since on/off and pressed/unpressed are equivalent, this is acceptable (though slightly disappointing).

But in most screen readers you’ll also be told you’ve entered a list of four items and that you’re on the first item — useful contextual information that works a bit like the group labelling I covered earlier in this post.

Importantly, because we have used `aria-labelledby` to associate the adjacent text to the button as its label, that is also available when navigating in this mode.

When browsing from item to item (for example, by pressing the down key when the NVDA screen reader is running), everything you encounter is announced, including the heading (_"Notifications, heading level two"_). Of course, browsing in this fashion, _"Notify by email"_ is announced on its own as well as in association with the adjacent button. This is somewhat repetitive, but makes sense: "Here’s the setting name, and here’s the on/off switch for the setting of this name."

How explicitly you need to associate controls to the things they control is a finer point of UX design and worth considering. In this case we’ve preserved our classic on/off switches for sighted users, without confusing or misleading either blind or sighted screen reader users no matter which keyboard interaction mode they are using. It’s pretty robust.</p>

## Conclusion

How you design and implement your toggle buttons is quite up to you, but I hope you’ll remember this post when it comes to adding this particular component to your pattern library. There’s no reason why toggle buttons — or any interface component for that matter — should marginalize the number of people they often do.

You can take the basics explored here and add all sorts of design nuances, including animation. It’s just important to lay a solid foundation first.</p>

### Checklist

*   Use form elements such as checkboxes for on/off toggles if you are certain the user won’t believe they are for submitting data.
*   Use `<button>` elements, not links, with `aria-pressed` or `aria-checked`.
*   Don’t change label and state together.
*   When using visual "on" and "off" text labels (or similar) you can override these with a unique label via `aria-labelledby`.
*   Be careful to make sure the contrast level between the button’s text and background color meets WCAG 2.0 requirements.

_This article originally appeared on [Inclusive Components](https://inclusive-components.design/). If you'd like to know more about similar inclusive component articles, follow [@inclusicomps](https://twitter.com/inclusicomps) on Twitter or subscribe to the [RSS feed](https://inclusive-components.design/rss/). By supporting [inclusive-components.design](https://www.patreon.com/inclusicomps) on Patreon, you can help to make it the most comprehensive database of robust interface components available._

{{< signature "ms, vf, il" >}}


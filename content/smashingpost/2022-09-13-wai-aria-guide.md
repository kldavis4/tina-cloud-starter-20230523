---
title: 'Making Sense Of WAI-ARIA: A Comprehensive Guide'
slug: wai-aria-guide
author: kate-kalcevich
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5f0e5d2-bebc-4ea0-bf42-5557f79ab433/wai-aria-guide.jpg
date: 2022-09-13T10:00:00.000Z
summary: >-
  In this article, Kate Kalcevich explains when to use ARIA and how to use it properly so that you can use ARIA in a way that’s helpful to the many disabled people who use [assistive technology](https://makeitfable.com/glossary/?utm_source=Smashing+Magazine&utm_medium=sponsored+content&utm_campaign=Upskill&utm_term=Fable&utm_content=Sept2022) to navigate the Internet. Let’s dive in!
description: >-
  In this article, Kate Kalcevich explains when to use ARIA and how to use it properly so that you can use ARIA in a way that’s helpful to the many disabled people who use [assistive technology](https://makeitfable.com/glossary/?utm_source=Smashing+Magazine&utm_medium=sponsored+content&utm_campaign=Upskill&utm_term=Fable&utm_content=Sept2022) to navigate the Internet. Let’s dive in!
categories:
  - Accessibility
  - Coding
  - JavaScript
disable_ads: true
disable_panels: true
disable_newsletterbox: true
sponsor:
  title: Fable
  link: https://makeitfable.com/?utm_source=Smashing+Magazine&utm_medium=sponsored+content&utm_campaign=Upskill&utm_term=Fable&utm_content=Sept2022
  image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c939a5c5-317f-472a-bb79-895a097520c2/fable-logo.png
  description: >-
    This article has been kindly supported by our dear friends at <a href="https://makeitfable.com/?utm_source=Smashing+Magazine&utm_medium=sponsored+content&utm_campaign=Upskill&utm_term=Fable&utm_content=Sept2022">Fable</a>, who enable your team to gain the skills and confidence needed to build inclusive products. If you’re ready to bring the voices of people with disabilities into your product development and accessibility training processes, <a href="https://makeitfable.com/contact-fable/?utm_source=Smashing+Magazine&utm_medium=sponsored+content&utm_campaign=Upskill&utm_term=Fable&utm_content=Sept2022">book a call</a> with them to learn more.
---

The [Web Accessibility Initiative &mdash; Accessible Rich Internet Applications (WAI-ARIA)](https://www.w3.org/TR/wai-aria-1.1/) is a technical specification that provides direction on how to improve the accessibility of web applications. Where the Web Content Accessibility Guidelines (WCAG) focus more on static web content, **WAI-ARIA focuses on making interactions more accessible.**

Interactions on the web are notorious for being inaccessible and are often part of the most critical functions such as:

- submitting a job application,
- purchasing from an online store, or 
- booking a healthcare appointment.

I’m currently the Head of Accessibility Innovation at Fable, a company that connects organizations to people with disabilities for user research and accessibility testing and provides custom training for digital teams to gain the skills to build inclusive products.

As an instructor for accessible web development, I spend a lot of time examining the source code of websites and web apps and ARIA is one of the things I see developers misusing the most.

## HTML

When you use HTML elements like `input`, `select`, and `button`, there are two things you’ll get for accessibility: information about the element is passed to the [DOM (Document Object Model)](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) and into an [Accessibility Tree](https://developer.mozilla.org/en-US/docs/Glossary/Accessibility_tree). Assistive technologies can access the nodes of the accessibility tree to understand: 

- what kind of element it is by checking its role, e.g., checkbox;
- what state the element is in, e.g., checked/not checked;
- the name of the element, e.g., “Sign up for our newsletter.”

The other thing you get when using HTML elements is keyboard interactivity. For example, a checkbox can be focused using the tab key and selected using the spacebar (specific interactions can vary by browser and operating system, but the point is they are available and standardized across all websites when you use HTML elements).

When you don’t use HTML, for example, if you build your own custom select using `<div>`s and `<span>`s or you use a component library, you need to do extra work to provide information about the element and build keyboard interactivity for assistive technology users. This is where ARIA comes into play.

## ARIA

Accessible Rich Internet Applications (ARIA) include a set of roles and attributes that define ways to make web content and web applications more accessible to people with disabilities.

You can use ARIA to pass information to the accessibility tree. ARIA roles and attributes don’t include any keyboard interactivity. Adding `role="button”` to a `<div>` doesn’t make it respond when you press the <kbd>Enter</kbd> key &mdash; that you have to build using JavaScript or another language. However, the [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/patterns/) does include a list of *what* keyboard interactivity should be added to various components such as accordions, buttons, carousels, etc.

## Roles

Let’s start with roles. What the heck is this thing in the code below? 

<pre><code class="language-html">&lt;div className="dd-wrapper"&gt;
  &lt;div className="dd-header"&gt;
    &lt;div className="dd-header-title"&gt;&lt;/div&gt;
  &lt;/div&gt;
  &lt;div className="dd-list"&gt;
    &lt;button className="dd-list-item"&gt;&lt;/button&gt;
    &lt;button className="dd-list-item"&gt;&lt;/button&gt;
    &lt;button className="dd-list-item"&gt;&lt;/button&gt;
  &lt;/div&gt;
&lt;/div&gt;
</code></pre>

This is actually a snippet of code I found online from a select element for React. The fact that the element is completely unrecognizable from the code is exactly the issue that any assistive technology would have &mdash; it can’t tell the user what it is or how to interact with it because there’s no ARIA role.

Watch what we can do here:

<pre><code class="language-html">&lt;div className="dd-wrapper" role="listbox"&gt;
</code></pre>

You might not be familiar with a `listbox`, but it’s a type of `select` that a screen reader user could recognize and know how to interact with. Now you could just use `<select>`, and you wouldn’t have to give it a role because it’s already got one that the DOM and accessibility tree will recognize, but I know that’s not always a feasible option.

A role tells an assistive technology user what the thing is, so make sure you use the correct role. A button is very different from a banner. Choose a role that matches the function of the component you’re building.

Another thing you should know about ARIA roles is that they override an HTML element’s inherent role.

<pre><code class="language-html">&lt;img role="button"&gt;
</code></pre>

This is no longer an image but a button. There are very few reasons to do this, and unless you exactly knew what you’re doing and why, I’d stay away from overriding existing HTML roles. There are many other ways to achieve this that make more sense from accessibility and a code robustness perspective:

<pre><code class="language-html">&lt;button&gt;&lt;img src="image.png" alt="Print" /&gt;&lt;/button&gt; 
&lt;input type="image" src="image.png" alt="Print" /&gt;
&lt;button style="background: url(image.png)" /&gt;Print&lt;/button&gt;
</code></pre>

If you’re building a component, you can look up the pattern for that component in the [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/patterns/) which includes information on which role(s) to use. You can also look up all [available roles in the mdn web docs](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles).

In summary, if you’re building something that doesn’t have a semantic HTML tag that describes it (i.e., anything interactive built using `<div>` or `<span>`), it needs to have an ARIA role so that assistive technology can recognize what it is.

## States And Properties (Aka ARIA Attributes)

In addition to knowing what an element is, if it has a state (e.g., `hidden`, `disabled`, `invalid`, `readonly`, `selected`, and so on) or changes state (e.g., `checked`/`not checked`, `open`/`closed`, and so on), you need to tell assistive technology users what its current state is and its new state whenever it changes. You can also share certain properties of an element. The [difference between states and properties isn’t really clear or important](https://www.w3.org/TR/wai-aria-1.0/states_and_properties), so let’s just call them attributes.

Here are some of the most common ARIA attributes you might need to use:

- `aria-checked`  
It’s used with `="true"` or `="false"` to indicate if checkboxes and radio buttons are currently checked or not.
- `aria-current`  
It’s used with `="true"` or `="false"` to indicate the current page within breadcrumbs or pagination.
- `aria-describedby`  
It’s used with the id of an element to add more information to a form field in addition to its label. `aria-describedby` can be used to give examples of the required format for a field, for example, a date, or to add an error message to a form field.

<pre><code class="language-html">&lt;label for="birthday"&gt;Birthday&lt;/label&gt;
&lt;input type="text" id="birthday" aria-describedby="date-format"&gt;
&lt;span id="date-format"&gt;MM-DD-YYYY&lt;/span&gt;
</code></pre>

- `aria-expanded`  
It’s used with `="true"` or `="false"` to indicate if pressing a button will show more content. Examples include accordions and navigation items with submenus.

<pre><code class="language-html">&lt;button aria-expanded="false"&gt;Products&lt;/button&gt;
</code></pre>

This indicates that the Products menu will open a submenu (for example, of different product categories). If you were to code it like this:

<pre><code class="language-html">&lt;a href="/products/"&gt;Products&lt;/a&gt;
</code></pre>

You’re setting the expectation that it’s a link, and clicking it will go to a new page. If it’s not going to go to a new page, but it actually stays on the same page but opens a submenu, that’s what button plus `aria-expanded` says to an assistive technology user. That simple difference between `<button>` and `<a>` and the addition of `aria-expanded` communicates so much about how to interact with elements and what will happen when you do.

- `aria-hidden`  
It’s used with `="true"` or `="false"` to hide something that is visible, but you don’t want assistive technology users to know about it. Use it with extreme caution as there are very few cases where you don’t want equivalent information to be presented.

One interesting use case I’ve seen is a card with both an image and the text title of the card linking to the same page but structured as two separate links. Imagine many of these cards on a page. For a screen reader user, they’d hear every link read out twice. So the image links used `aria-hidden="true"`. The ideal way to solve this is to combine the links into one that has both an image and the text title, but real-life coding isn’t always ideal, and you don’t always have that level of control.

Note that this breaks the fourth rule of ARIA (which we’ll get to in a bit), but it does it in a way that doesn’t break accessibility. Use it with extreme caution when there are no better workarounds, and you’ve tested it with assistive technology users.

- `aria-required`  
It’s used with `="true"` or `="false"` to indicate if a form element has to be filled out before the form can be submitted.

If you’re building a component, you can look up the attributes for that component on the [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/patterns/). The [mdn web docs covers states and properties](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes#states_and_properties_defined_on_mdn) as well as ARIA roles.

Keep in mind that all these ARIA attributes tell a user something, but you still have to code the thing you’re telling them. `aria-checked="true"` doesn’t actually check a checkbox; it just tells the user the checkbox is checked, so that better be true or you’ll make things worse and not better for accessibility. The exception would be `aria-hidden="true"` which removes an element from the accessibility tree, effectively hiding it from anyone using assistive technology who can’t see.

So now we know how to use ARIA to explain what something is, what state it’s in, and what properties it has. The last thing I’ll cover is focus management.

## Focus Management

Anything interactive on a website or web app must be able to receive focus. Not everyone will use a mouse, trackpad, or touch screen to interact with sites. Many people use their keyboard or an assistive technology device that emulates a keyboard. This means that for everything you can click on, you should also be able to use the tab key or arrow keys to reach it and the <kbd>Enter</kbd> key, and sometimes the spacebar, to select it.

There are three concepts you’ll need to consider if you use `<div>` and `<span>` to create interactive elements:

1. You need to add `tabindex="0"` so that a keyboard or emulator can focus on them.
2. For anything that accepts keyboard input, you need to add an event listener to listen for key presses.
3. You need to add the appropriate role so that a screen reader user can identify what element you’ve built.

Remember that native HTML controls already accept keyboard focus and input and have inherent roles. This is just what you need to do when creating custom elements from non-semantic HTML. 

Ben Myers does a deep dive into [turning a `div` into a button](https://benmyers.dev/blog/clickable-divs/), and I’ll share parts of his example here. Notice the tabindex and the role:

<pre><code class="language-html">&lt;div tabindex="0" role="button" onclick="doSomething();"&gt;
    Click me!
&lt;/div&gt;
</code></pre>

And you’ll need JavaScript to listen to the key presses:

<div class="break-out">

<pre><code class="language-javascript">const ENTER = 13;
const SPACE = 32;
// Select your button and store it in ‘myButton’
myButton.addEventListener('keydown', function(event) {
    if (event.keyCode === ENTER || event.keyCode === SPACE) {
        event.preventDefault(); // Prevents unintentional form submissions, page scrollings, the like
        doSomething(event);
    }
});
</code></pre>
</div>

When it comes to figuring out which keys to listen for, I suggest looking up the component you’re building in the [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/patterns/) and following the keyboard interaction recommendations.

## Common Mistakes

Having looked at a lot of code in my lifetime, I see some accessibility errors being made repeatedly. Here’s a list of the most common mistakes I find and how to avoid them:

<h3 id="marker" style="text-transform: none;">Using An <code>aria-labelledby</code> Attribute That References An ID That Doesn’t Exist</h3>

For example, a modal that has a title in the modal but `aria-labelledby` is referencing something else that no longer exists. It’s probably something removed by another developer who didn’t realize the `aria-labelledby` connection was there. Instead, the modal title could’ve been an `<h1>` and either `aria-labelledby` could reference the `<h1>` or you could set the focus on the `<h1>` when the modal opens and a screen reader user would know what’s going on as long as `role="dialog” ` was also used. Try to avoid fragile structures that, if someone else came along and edited the code, would break easily.

### Not Moving The Focus Into The Modal When It Opens

Countless times I’ve seen a screen reader user navigating the page behind the modal either unaware a modal has opened or confused because they can’t find the contents of the modal. There are several ways to trap focus within a modal, but one of the newer methods is to add `inert` to the `<main>` landmark (and, of course, make sure the modal isn’t inside `<main>`). [`Inert` is getting better support across browsers](https://caniuse.com/?search=inert) lately. To learn more, check out Lars Magnus Klavenes’ [Accessible modal dialogs using `inert`](https://larsmagnus.co/blog/accessible-modal-dialogs-using-inert).

### Adding Roles That Duplicate HTML

In general, doing something like this `<button role="button”>` is pointless. There is one case where it *might* make sense to do this. VoiceOver and Safari remove `list` element semantics when `list-style: none` is used. This was done on purpose because if there is no indication to a sighted user that the content is a list, why tell a screen reader user that it’s a list? If you want to override this, you can add an explicit ARIA `role="list"` to the `<ul>`.

Adrian Roselli says an unstyled list not being announced as a list “…may not be a big deal unless user testing says you really need a list.” I agree with him on that point, but I’m sharing the fix in case your user testing shows it’s beneficial.

<h3 id="marker" style="text-transform: none;">Adding <code>tabindex="0"</code> To Every Element</h3>

Sometimes developers start using a screen reader and assume that tabbing is the only way to navigate; therefore, anything without tabindex isn’t accessible. This is NOT true. Remember, if you don’t know how to use a screen reader, you can’t troubleshoot usability issues. Meet with an everyday screen reader user to figure those out.

### Using Child Roles Without Parent Roles

For example, `role="option"` must have a direct parent with `role="listbox"`.

<pre><code class="language-html">&lt;div role="listbox"&gt;
    &lt;ul&gt;
      &lt;li role="option"&gt;
</code></pre>

The above code isn’t valid because there’s a `<ul>` between the parent and child elements. This can be fixed by adding a presentation role to essentially hide the `<ul>` from the accessibility tree, like `<ul role="presentation”>`.

<h3 id="marker" style="text-transform: none;">Using <code>role="menu"</code> For Navigation</h3>

Website navigation is really a table of contents and not a menu. ARIA menus are not meant to be used for navigation but application behavior like the menus in a desktop application. Instead, use `<nav>`, and if you have child navigation links, those should be hidden until a button is pressed to show them:

<pre><code class="language-html">&lt;nav aria-label="Main menu"&gt;
    &lt;button aria-expanded="false"&gt;Products&lt;/button&gt;
    &lt;ul hidden&gt;
       &lt;li&gt;Cat pyjamas&lt;/li&gt;...
</code></pre>

If you want to learn more, Heydon Pickering does a deep dive into [Building Accessible Menu Systems](https://www.smashingmagazine.com/2017/11/building-accessible-menu-systems/) in his Smashing Magazine article.

Regarding navigation, using `<nav>` more than once on a page without giving each instance a unique label means that screen reader users will have to explore each navigation region to find the one they’re looking for. A simple `aria-label` on each `<nav>` will make it much easier.

<pre><code class="language-html">&lt;nav aria-label="Customer service"&gt;
  &lt;ul&gt;
    &lt;li&gt;&lt;a href="#"&gt;Help&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Order tracking&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Shipping &amp; Delivery&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Returns&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Contact us&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Find a store&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;/nav&gt;
</code></pre>

## How To Validate ARIA

Use automated accessibility checkers like [Axe](https://www.deque.com/axe/browser-extensions/) or [WAVE](https://wave.webaim.org/extension/) extensions when you run your code in a browser. Accessibility linters like [Axe for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=deque-systems.vscode-axe-linter) or [ESLint for JSX elements](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y) will check your code as you write it.

Listen to your code with a screen reader. You’d never ship code without running it in a browser to make sure it works, and using a screen reader can be the same kind of check. [NVDA](https://www.nvaccess.org/) is free for Windows, and [VoiceOver](https://www.apple.com/ca/accessibility/vision/) comes built into Macs and iPhones. [TalkBack](https://support.google.com/accessibility/android/topic/3529932?hl=en&ref_topic=9078845) is built into Android phones.

Test with assistive technology users. I consider this mandatory for any large organization that has a budget for accessibility (and they all should). There are companies that can recruit assistive technology users for testing or run user testing for you, and the company I work for can provide 2-day turnarounds on user testing that is facilitated by you or unmoderated to support accessibility testing at scale.

## Frameworks And Component Libraries

If you’re using a web framework, one way to make the lift of building for accessibility a bit lighter is to use a component library with accessibility built in. I’ll add the caveat that accessibility can be complex and not everything that claims to be accessible is truly usable by assistive technology users. The best way to ensure accessibility is to always test with the users you are building for. 

Here are some starting points for your search:

- [React Aria](https://react-spectrum.adobe.com/react-aria/index.html)
- [Vue A11y](https://vue-a11y.com/)
- [Material Design 3](https://m3.material.io/)
- [Lion](https://lion-web.netlify.app/)
- [Open UI](https://open-ui.org/)

## Conclusion

Hopefully, this has demystified ARIA for you. Like a secret language that only the most elite accessibility geeks know, it has its own Fight Club-esque rules.

1. The first rule of ARIA is “Don’t use ARIA.” A `<button>` will always be better than `<div role="button">`.
2. Secondly, don’t override native semantics. Instead of `<button role="heading">`, use `<h3><button>`.
2. Also, always remember that all ARIA interactive elements must work with the keyboard.
3. Don’t use `role="presentation"` or `aria-hidden="true"` on a focusable element. `<button role="presentation”>` means you’re hiding that button only from assistive technology users. That’s not just inaccessible; it’s outright excluding certain users.
4. Last but not least, all interactive elements must have an accessible name. There are many ways to do that, and here are some of them:

<pre><code class="language-html">&lt;button&gt;Print&lt;/button&gt; (the name is the button text)

&lt;div aria-label="Settings"&gt;&lt;svg&gt;&lt;/div&gt; (the aria-label assigns a name)

&lt;div aria-labelledby="myName"&gt;
  &lt;h1 id="myName"&gt;Heading&lt;/h1&gt;
&lt;/div&gt;

&lt;label for="name"&gt;Name&lt;/label&gt;
&lt;input type="text" id="name" /&gt;
</code></pre>

I like to think of ARIA as a tool used by the most elite Special Ops Team that you call in for your most difficult accessibility challenges. Well, maybe I just always wanted to do one-arm pushups like Emily Blunt in Edge of Tomorrow, and this is the closest I can get. Anyhow, I hope this was helpful and that you are no longer confused about ARIA. Go forth and build accessible things!

{{< signature "vf, yk, il" >}}

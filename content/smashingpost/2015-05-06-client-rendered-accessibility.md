---
title: Notes On Client-Rendered Accessibility
slug: client-rendered-accessibility
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7cf3d821-4b0b-4528-8562-afb5eaf093e1/excerpt-accessibility.jpg
date: 2015-05-06T17:00:38.000Z
author: marcysutton
description: >-
  As creators of the web, we bring innovative, well-designed interfaces to life.
  We find satisfaction in improving our craft with each design or line of code.
  But this push to elevate our skills can be self-serving: Does a new [CSS
  framework](https://www.smashingmagazine.com/2014/02/19/responsive-design-frameworks-just-because-you-can-should-you/)
  or JavaScript abstraction pattern serve our users or us as developers?
categories:
  - UX
  - User Interaction
  - UX
  - Accessibility
  - React
---
As creators of the web, we bring innovative, well-designed interfaces to life. We find satisfaction in improving our craft with each design or line of code. But this push to elevate our skills can be self-serving: Does a new CSS framework or JavaScript abstraction pattern serve our users or us as developers?

## <span class="rh">Further Reading</span> on SmashingMag

*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Test Automation For Apps, Games And The Mobile Web](https://www.smashingmagazine.com/2015/01/basic-test-automation-for-apps-games-and-mobile-web/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)

If a framework encourages best practices in development while also improving our workflow, it might serve both our users’ needs and ours as developers. If it encourages best practices in accessibility alongside other areas, like performance, then it has potential to improve the state of the web.

Despite our pursuit to do a better job every day, sometimes we forget about accessibility, the practice of designing and developing in a way that’s inclusive of people with disabilities. We have the power to improve lives through technology — we should use our passion for the craft to build a more accessible web.

{{% feature-panel %}}

These days, we build a lot of client-rendered web applications, also known as single-page apps, JavaScript MVCs and MV-whatever. AngularJS, React, Ember, Backbone.js, Spine: You may have used or seen one of these JavaScript frameworks in a recent project. Common user experience-related characteristics include asynchronous postbacks, animated page transitions, and dynamic UI filtering. With frameworks like these, creating a poor user experience for people with disabilities is, sadly, pretty easy. Fortunately, we can employ best practices to make things better.

In this article, we will **explore techniques for building accessible client-rendered web applications**, making our jobs as web creators even more worthwhile.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16e1125e-1808-4d37-b2e8-bddb6b1bfe5e/whatever.gif"><img alt="Clueless character making 'Whatever' gesture" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8b6a47a-5c9b-4e55-8418-19176d65c898/01-whatever-opt.gif"></a><figcaption>MV-whatever. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16e1125e-1808-4d37-b2e8-bddb6b1bfe5e/whatever.gif">Show animated Gif</a>)</figcaption></figure>

## Semantics

Front-end JavaScript frameworks make it easy for us to create and consume custom HTML tags like `<pizza-button>`, which you’ll see in an example later on. React, AngularJS and Ember enable us to attach behavior to made-up tags with no default semantics, using JavaScript and CSS. We can even use [Web Components](https://www.smashingmagazine.com/2014/03/04/introduction-to-custom-elements/) now, a set of new standards holding both the promise of extensibility and a challenge to us as developers. With this much flexibility, it’s critical for users of assistive technologies such as screen readers that we use semantics to communicate what’s happening without relying on a visual experience.

Consider a common [form control](https://webaim.org/techniques/forms/controls): A checkbox opting you out of marketing email is pretty significant to the user experience. If it isn’t announced as “Subscribe checked check box” in a screen reader, you might have no idea you’d need to uncheck it to opt out of the subscription. In client-side web apps, it’s possible to construct a form model from user input and post JSON to a server regardless of how we mark it up — possibly even without a `<form>` tag. With this freedom, knowing how to create accessible forms is important.

To keep our friends with screen readers from opting in to unwanted email, we should:

*   use native inputs to easily announce their role (purpose) and state (checked or unchecked);
*   provide an accessible name using a `<label>`, with `id` and `for` attribute pairing — `aria-label` on the input or `aria-labelledby` pointing to another element’s `id`.

<pre><code class="language-markup">
&lt;form&gt;
  &lt;label for="subscribe"&gt;
    Subscribe
  &lt;/label&gt;
  &lt;input type="checkbox" id="subscribe" checked&gt;
&lt;/form&gt;
</code></pre>

### Native Checkbox With Label

If native inputs can’t be used (with good reason), create custom checkboxes with `role=checkbox`, `aria-checked`, `aria-disabled` and `aria-required`, and wire up keyboard events. See the W3C’s “[Using WAI-ARIA in HTML](https://www.w3.org/TR/aria-in-html/).”

### Custom Checkbox With ARIA

<pre><code class="language-markup">
&lt;form&gt;
  &lt;some-checkbox role="checkbox" tabindex="0" aria-labelledby="subscribe" aria-checked="true"&gt;
  &lt;/some-checkbox&gt;
  &lt;some-label id="subscribe"&gt;Subscribe&lt;/some-label&gt;
&lt;/form&gt;
</code></pre>

Form inputs are just one example of the [use of semantic HTML](https://webaim.org/techniques/semanticstructure/) and ARIA attributes to communicate the purpose of something — other important considerations include headings and page structure, buttons, anchors, lists and more. [ARIA](https://www.w3.org/TR/wai-aria/), or Accessible Rich Internet Applications, exists to fill in gaps where accessibility support for HTML falls short (in theory, it can also be used for XML or SVG). As you can see from the checkbox example, ARIA requirements quickly pile up when you start writing custom elements. Native inputs, buttons and other semantic elements provide keyboard and accessibility support for free. The moment you create a custom element and bolt ARIA attributes onto it, you become responsible for managing the role and state of that element.

Although ARIA is great and capable of many things, understanding and using it is a lot of work. It also doesn’t have the broadest support. Take [Dragon NaturallySpeaking](https://assistivetechnology.about.com/od/SpeechRecognition/p/Dragon-Naturallyspeaking-As-Assistive-Technology.htm) — this assistive technology, which people use all the time to make their life easier, is just starting to gain ARIA support. Were I a browser implementer, I’d focus on native element support first, too — so it makes sense that ARIA might be added later. For this reason, use native elements, and you won’t often need to use ARIA roles or states (`aria-checked`, `aria-disabled`, `aria-required`, etc.). If you must create custom controls, read up on ARIA to learn the [expected keyboard behavior](https://www.w3.org/WAI/PF/aria-practices/#keyboard) and how to use attributes correctly.

**Tip:** Use Chrome’s [Accessibility Developer Tools](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb) to audit your code for errors, and you’ll get the bonus “Accessibility Properties” inspector.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5101bcbf-e2d2-4dbd-ad9e-0b5c7a3ccd64/02-rawosks-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/563208e7-8bab-4e83-a712-61cb6abdd840/02-rawosks-opt-small.png" alt="AngularJS material in Chrome with accessibility inspector open" /></a><figcaption>AngularJS material in Chrome with accessibility inspector open. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5101bcbf-e2d2-4dbd-ad9e-0b5c7a3ccd64/02-rawosks-opt.png">View large version</a>)</figcaption></figure>

### Web Components and Accessibility

An important topic in a discussion on accessibility and semantics is Web Components, a set of new standards landing in browsers that enable us to natively create reusable HTML widgets. Because Web Components are still so new, the syntax is majorly in flux. In December 2014, [Mozilla said it wouldn’t support HTML imports](https://hacks.mozilla.org/2014/12/mozilla-and-web-components/), a seemingly obvious way to distribute new components; so, for now that technology is natively [available in Chrome and Opera](https://caniuse.com/#feat=imports) only. Additionally, up for debate is the syntax for extending native elements (see the [discussion about `is=""` syntax](https://lists.w3.org/Archives/Public/public-webapps/2015JanMar/0361.html)), along with how rigid the shadow DOM boundary should be. Despite these changes, here are some tips for writing semantic Web Components:

*   Small components are more reusable and easier to manage for any necessary semantics.
*   Use native elements within Web Components to gain behavior for free.
*   Element IDs within the shadow DOM do not have the same scope as the host document.
*   The same non-Web Component accessibility guidelines apply.

For more information on Web Components and accessibility, have a look at these articles:

*   “[Polymer and Web Component Accessibility: Best Practices](https://unobfuscated.blogspot.com/2015/03/polymer-and-web-component-accessibility.html),” Dylan Barrell
*   “[Web Components Punch List](https://www.paciellogroup.com/blog/2014/09/web-components-punch-list/),” Steve Faulkner
*   “[Accessible Web Components](https://www.polymer-project.org/0.5/articles/accessible-web-components.html),” Addy Osmani and Alice Boxhall, Polymer

## Interactivity

Native elements such as buttons and inputs come prepackaged with events and properties that work easily with keyboards and assistive technologies. Leveraging these features means less work for us. However, given how easy JavaScript frameworks and CSS make it to create custom elements, such as `<pizza-button>`, we might have to do more work to deliver pizza from the keyboard if we choose to mark it up as a new element. For keyboard support, custom HTML tags need:

*   `tabindex`, preferably `0` so that you don’t have to manage the entire page’s tab order ([WebAIM discusses this](https://webaim.org/techniques/keyboard/tabindex));
*   a keyboard event such as `keypress` or `keydown` to trigger callback functions.</p>

## Focus Management

Closely related to interactivity but serving a slightly different purpose is focus management. The term “client-rendered” refers partly to a single-page browsing experience where routing is handled with JavaScript and there is no server-side page refresh. Portions of views could update the URL and replace part or all of the DOM, including where the user’s keyboard is currently focused. When this happens, **focus is easily lost, creating a pretty unusable experience** for people who rely on a keyboard or screen reader.

Imagine sorting a list with your keyboard’s arrow keys. If the sorting action rebuilds the DOM, then the element that you’re using will be rerendered, losing focus in the process. Unless focus is deliberately sent back to the element that was in use, you’d lose your place and have to tab all the way down to the list from the top of the page again. You might just leave the website at that point. Was it an app you needed to use for work or to find an apartment? That could be a problem.

In client-rendered frameworks, we are responsible for ensuring that focus is not lost when rerendering the DOM. The easy way to test this is to use your keyboard. If you’re focused on an item and it gets rerendered, do you bang your keyboard against the desk and start over at the top of the page or gracefully continue on your way? Here is one focus-management technique from [Distiller](https://drinkdistiller.com) using Spine, where focus is sent back into relevant content after rendering:

<pre><code class="language-coffeescript">
class App.FocusManager
constructor:
$(‘body’).on ‘focusin’, (e) =&gt;
@oldFocus = e.target
</code></pre>

<pre><code class="language-coffeescript">
App.bind 'rendered', (e) =&gt;
return unless @oldFocus

if @oldFocus.getAttribute('data-focus-id')
@_focusById()
else
@_focusByNodeEquality()

_focusById: -&gt;
focusId = @oldFocus.getAttribute('data-focus-id')
newFocus = document.querySelector("##{focusId}")
App.focus(newFocus) if newFocus

_focusByNodeEquality: -&gt;
allNodes = $('body *:visible').get()
for node in allNodes
if App.equalNodes(node, @oldFocus)
App.focus(node)
</code></pre>

In this helper class, JavaScript (implemented in CoffeeScript) binds a `focusin` listener to `document.body` that checks anytime an element is focused, using [event delegation](https://learn.jquery.com/events/event-delegation/), and it stores a reference to that focused element. The helper class also subscribes to a Spine `rendered` event, tapping into client-side rendering so that it can gracefully handle focus. If an element was focused before the rendering happened, it can focus an element in one of two ways. If the old node is identical to a new one somewhere in the DOM, then focus is automatically sent to it. If the node isn’t identical but has a `data-focus-id` attribute on it, then it looks up that `id`’s value and sends focus to it instead. This second method is useful for when elements aren’t identical anymore because their text has changed (for example, “item 1 of 5” becoming labeled off screen as “item 2 of 5”).

Each JavaScript MV-whatever framework will require a slightly different approach to focus management. Unfortunately, most of them won’t handle focus for you, because it’s hard for a framework to know what should be focused upon rerendering. By testing rendering transitions with your keyboard and making sure focus is not dropped, you’ll be empowered to add support to your application. If this sounds daunting, inquire in your framework’s support community about how focus management is typically handled (see [React’s GitHub repo](https://github.com/facebook/react/issues/1791#issuecomment-82987932) for an example). There are people who can help!

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad87a87a-b6d8-499c-82ce-98dae716d052/cat-helping.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/729c3474-d2ec-4f79-ad57-faf1e598807c/03-helping-opt.gif" alt="Cat 'helping' by laying on keyboard"></a><figcaption>Cat “helping”. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad87a87a-b6d8-499c-82ce-98dae716d052/cat-helping.gif">View animated Gif</a>)</figcaption></figure>

## Notifying The User

There is a debate about [whether client-side frameworks are actually good for users](https://tantek.com/2015/069/t1/js-dr-javascript-required-dead), and plenty of people [have an opinion](https://adactio.com/journal/8245) on them. Clearly, most client-rendered app frameworks could improve the user experience by providing easy asynchronous UI filtering, form validation and live content updates. To make these dynamic updates more inclusive, developers should also update users of assistive technologies when something is happening away from their keyboard focus.

Imagine a scenario: You’re typing in an autocomplete widget and a list pops up, filtering options as you type. Pressing the down arrow key cycles through the available options, one by one. One technique to announce these selections would be to append messages to an [ARIA live region](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions), a mechanism that screen readers can use to subscribe to changes in the DOM. As long as the live region exists when the element is rendered, any text appended to it with JavaScript will be announced (meaning you can’t add bind `aria-live` and add the first message at the same time). This is essentially how [Angular Material](https://material.angularjs.org/)’s autocomplete handles dynamic screen-reader updates:

<pre><code class="language-markup">
&lt;md-autocomplete md-selected-item="ctrl.selectedItem" aria-disabled="false"&gt;
&lt;md-autocomplete-wrap role="listbox"&gt;
  &lt;input type="text" aria-label="{{ariaLabel}}" aria-owns="ul_001"&gt;
&lt;/md-autocomplete-wrap&gt;
&lt;ul role="presentation" id="ul_001"&gt;
  &lt;li ng-repeat="(index, item) in $mdAutocompleteCtrl.matches" role="option" tabIndex="0"&gt;
&lt;/ul&gt;
&lt;aria-status class="visually-hidden" role="alert"&gt;
  &lt;p ng-repeat="message in messages"&gt;{{message}}&lt;/p&gt;
&lt;/aria-status&gt;
&lt;/md-autocomplete&gt; 
</code></pre>

In the simplified code above (the [full directive](https://github.com/angular/material/blob/master/src/components/autocomplete/js/autocompleteDirective.js#L43) and [related controller](https://github.com/angular/material/blob/master/src/components/autocomplete/js/autocompleteController.js) source are on GitHub), when a user types in the `md-autocomplete` text input, list items for results are added to a neighboring unordered list. Another neighboring element, `aria-status`, gets its `aria-live` functionality from the `alert` role. When results appear, a message is appended to `aria-status` announcing the number of items, “There is one match” or “There are four matches,” depending on the number of options. When a user arrows through the list, that item’s text is also appended to `aria-status`, announcing the currently highlighted item without the user having to move focus from the input. By curating the list of messages sent to an ARIA live region, we can implement an inclusive design that goes far beyond the visual. Similar regions can be used to validate forms.

For more information on accessible client-side validation, read Marco Zehe’s “[Easy ARIA Tip #3: `aria-invalid` and Role `alert`](https://www.marcozehe.de/2008/07/16/easy-aria-tip-3-aria-invalid-and-role-alert/)” or Deque’s post on [accessible forms](https://www.deque.com/blog/accessible-client-side-form-validation-html5-wai-aria/).</p>

## Conclusion

So far, we’ve talked about accessibility with screen readers and keyboards. Also **consider readability**: This includes color contrast, readable fonts and obvious interactions. In client-rendered applications, all of the typical [web accessibility principles](https://webaim.org/intro/) apply, in addition to the specific ones outlined above. The resources listed below will help you incorporate accessibility in your current or next project.

It is up to us as developers and designers to ensure that everyone can use our web applications. By knowing what makes an accessible user experience, we can serve a lot more people, and possibly even make their lives better. We need to remember that client-rendered frameworks aren’t always the right tool for the job. There are plenty of legitimate use cases for them, hence their popularity. There are definitely [drawbacks to rendering everything on the client](https://alistapart.com/article/let-links-be-links). However, even as solutions for seamless server- and client-side rendering improve over time, these same accessibility principles of focus management, semantics and alerting the user will remain true, and they will enable more people to use your apps. Isn’t it cool that we can use our craft to help people through technology?

## Resources

*   “[Design Accessibly, See Differently: Color Contrast Tips and Tools](https://www.smashingmagazine.com/2014/10/22/color-contrast-tips-and-tools-for-accessibility/),” Cathy O’Connor, Smashing Magazine
*   “[Web Accessibility for Designers](https://webaim.org/resources/designers/),” WebAIM
*   [Accessibility Developer Tools](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb),” Chrome plugin
*   “[Using WAI-ARIA in HTML](https://www.w3.org/TR/aria-in-html/),” W3C
*   “How I Audit a Website for Accessibility,” Marcy Sutton, Substantial
*   “[Using ngAria](https://angularjs.blogspot.com/2014/11/using-ngaria.html),” Marcy Sutton
*   “[Protractor Accessibility Plugin](https://marcysutton.com/angular-protractor-accessibility-plugin/),” Marcy Sutton  
    Protractor is AngularJS’ end-to-end testing framework.

_Thanks to Heydon Pickering for reviewing this article._

{{< signature "hp, al, ml" >}}


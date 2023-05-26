---
title: The WAI Forward
slug: the-wai-forward
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6572104-138c-42cd-b703-ea8ce1733dee/2-wai-plaster-preview-opt.jpg
date: 2014-07-09T21:23:49.000Z
author: heydon-pickering
description: >-
  _It's one thing to create a web application and quite another to keep it
  accessible — independent of the device that the user is using and its
  capabilities. That's why [Heydon Pickering](https://twitter.com/heydonworks),
  now the accessibility editor on Smashing Magazine, wrote an eBook [Apps For
  All: Coding Accessible Web
  Applications](https://shop.smashingmagazine.com/apps-for-all-coding-accessible-web-applications.html),
  outlining the roadmap for well-designed, accessible applications._

  _This article is an excerpt of a chapter in the eBook that introduces many of
  the ideas and techniques presented. Reviewed by Steve Faulkner, it's an eBook
  you definitely shouldn't miss if you're a developer who cares about
  well-structured content and inclusive interface design. – Ed._

  Because the W3C’s mission from the outset has been to make the web accessible,
  accessibility features are built into its specifications. As responsible
  designers, we have the job of creating compelling web experiences without
  disrupting the inclusive features of a simpler design.
categories:
  - Coding
  - Mobile
  - Responsive Design
  - Accessibility
  - Smashing eBooks
---
<em>It's one thing to create a web application and quite another to keep it accessible — independent of the device that the user is using and its capabilities. That's why <a href="https://twitter.com/heydonworks">Heydon Pickering</a>, now the accessibility editor on Smashing Magazine, wrote an eBook <a href="https://shop.smashingmagazine.com/apps-for-all-coding-accessible-web-applications.html">Apps For All: Coding Accessible Web Applications</a>, outlining the roadmap for well-designed, accessible applications.</em>

<em>This article is an excerpt of a chapter in the eBook that introduces many of the ideas and techniques presented. Reviewed by <a href="https://twitter.com/stevefaulkner">Steve Faulkner</a>, it's an eBook you definitely shouldn't miss if you're a developer who cares about well-structured content and inclusive interface design. – Ed.</em>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)
*   [Accessibility: Improving The UX For Color-Blind Users](https://www.smashingmagazine.com/2016/06/improving-ux-for-color-blind-users/)
*   [Making Accessibility Simpler, With Ally.js](https://www.smashingmagazine.com/2015/12/making-accessibility-simpler/)
*   [Inclusive Front-End Design Patterns, A New Smashing Book](https://www.smashingmagazine.com/inclusive-design-patterns/)

Because the W3C’s mission from the outset has been to make the web accessible, accessibility features are built into its specifications. As responsible designers, we have the job of creating compelling web experiences without disrupting the inclusive features of a simpler design.

{{% feature-panel %}}

As <a href="https://twitter.com/scottjehl/status/411237303579721728">Scott Jehl said</a>:
<blockquote>"Accessibility is not something we add to a website, but something we start with and risk losing with each enhancement. It is to be retained."</blockquote>

Unfortunately, not all websites are destined to be as simple as the provocative manifesto that is “<a href="https://motherfuckingwebsite.com/">This Is a Mother****ing Website</a>” and, as web interfaces evolve, complying with the <a href="https://www.w3.org/TR/WCAG20/">Web Content Accessibility Guidelines</a> (WCAG 2.0) has become increasingly difficult. As we together embrace the advancements of the web and our newfound power to construct hitherto impossible web-based software, we need to tackle the accessibility of new idioms. We need to find a way to adopt new tools and techniques to keep the playing field level.

It’s time to embrace change.</p>

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2014/10/color-contrast-tips-and-tools-for-accessibility/#further-reading-on-smashingmag)

*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)
*   <span data-sheets-value="{&quot;1&quot;:2,&quot;2&quot;:&quot;Mobile And Accessibility: Why You Should Care And What You Can Do About It&quot;}" data-sheets-userformat="{&quot;2&quot;:268480,&quot;9&quot;:0,&quot;10&quot;:2,&quot;14&quot;:{&quot;1&quot;:2,&quot;2&quot;:1136076},&quot;15&quot;:&quot;Arial&quot;,&quot;21&quot;:1}">[Mobile And Accessibility: Why You Should Care](https://www.smashingmagazine.com/2014/05/mobile-accessibility-why-care-what-can-you-do/)</span>
*   [Accessibility Originates With UX: A BBC iPlayer Case Study](https://www.smashingmagazine.com/2015/02/bbc-iplayer-accessibility-case-study/)
*   [Accessibility APIs: A Key To Web Accessibility](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/)

## ARIA: A Passion For Parity

The Web Accessibility Initiative’s (WAI) specification for <a href="https://www.w3.org/WAI/intro/aria">Accessible Rich Internet Applications</a> (WAI-ARIA) is an accessibility resource like WCAG 2.0, with certain notable differences. If it helps, you could think of the two resources as siblings: Both have been brought up in the same environment and have been instilled with the same basic values, but they differ in personality. WCAG 2.0 is the cautious homebody who keeps the home fires burning, while the more gregarious WAI-ARIA has ambitions to take accessibility to new territories.

Unlike WCAG 2.0, ARIA is not only a set of recommendations but a suite of attributes to be included in your HTML. Its tools enable you to alter and increase the amount of information shared about your HTML with users of assistive technologies. This is extremely useful when you’re making web apps because the roles, properties, states and relationships of elements in a web app are liable to be a lot more complex and dynamic. One way of looking at it is that ARIA gives you the tools to meet the WCAG’s requirements in web apps.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0bec1be7-03ae-46fd-bd8a-14634479f8bc/1-wai-spider-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c1efcd43-d47b-4f87-a7b2-e9b7b7494067/1-wai-spider-preview-opt.jpg" alt="1-wai-spider-preview-opt" width="500" height="266" /></a></figure>

## The Two Purposes Of ARIA

ARIA gives you the ability to reclassify and otherwise augment the perceived meaning (or semantics) of your HTML. That’s pretty powerful, but what is the purpose of it? ARIA has two main applications.</p>

### Remedy

ARIA can be used as a remedy to improve the information provided to assistive technology by poorly coded, unsemantic markup.

<figure><a class="at" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58c75379-099e-4840-83bf-157b56f1f4ab/2-wai-plaster-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d6572104-138c-42cd-b703-ea8ce1733dee/2-wai-plaster-preview-opt.jpg" alt="2-wai-plaster-preview-opt" width="500" height="278" /></a></figure>

For example, a developer might use a <code>&lt;div&gt;</code> and some JavaScript to emulate a <code>type="checkbox"</code>. They shouldn’t, but they might. To make this <code>&lt;div&gt;</code> actually understandable as a checkbox, the ARIA <a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_checkbox_role">role of <code>checkbox</code></a> can be added as an attribute, making screen readers think it is, in fact, a standard checkbox. In addition, our developer must use the <code>aria-checked</code> attribute to indicate whether the checkbox is indeed checked.

<pre><code class="language-markup">
&lt;div class="toggle-thingy" role="checkbox" aria-checked="false" tabindex="0"&gt;Yes?&lt;/div&gt;
</code></pre>

Using the proper <code>input</code> element, <code>type</code> attribute and <code>checked</code> attribute to communicate this information would be better — they are better supported than ARIA (which is relatively modern), and the <code>input</code> element would be automatically focusable, like a semantic <code>&lt;button&gt;</code> (so, no need for the <code>tabindex</code>). Nonetheless, we can employ ARIA in this way to make quick fixes to markup, often without disturbing the design of the application.</p>

### Enhancement

As we’ve established, web applications are more complex than simple web documents, and our use of HTML elements tends to exceed the basic semantics gifted to them. ARIA’s killer feature is its ability to help authors like you and me communicate many of these more ambitious uses in an accessible way.

Take ARIA’s <a href="https://www.w3.org/TR/wai-aria/states_and_properties#aria-haspopup"><code>aria-haspopup</code> attribute</a>. It represents a property of certain elements that have a hidden submenu. The owner of this property is likely to be an <code>&lt;a&gt;</code> or <code>&lt;button&gt;</code> element and, without this special attribute, that’s <em>all</em> it would be to the user of a screen reader: No clue would be given that the submenu exists.

<pre><code class="language-markup">&lt;li&gt;
  &lt;a href="#submenu" aria-haspopup="true" aria-controls="submenu1"&gt;Main link&lt;/a&gt;
  &lt;ul id="submenu"&gt;
    &lt;li&gt;&lt;a href="/somewhere/"&gt;Submenu link&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="/somewhere/else/"&gt;Another link&lt;/a&gt;&lt;/li&gt;
  &lt;/ul&gt;
&lt;/li&gt;
</code></pre>

Some of these ARIA attributes are expected to be replaced by simple HTML elements and attributes. As I write, the <code>&lt;dialog&gt;</code> element is <a href="https://twitter.com/stevefaulkner/status/413263499863658496">being slowly adopted</a> as the successor to the <code>dialog</code> and <code>alertdialog</code> ARIA role attributes, for example.

Where possible, superseding ARIA with plain HTML(5) is good because it simplifies the markup and centralizes the W3C’s advice. However, many attributes that communicate specific contextual information, such as the <code>aria-haspopup</code> and <a href="https://msdn.microsoft.com/en-us/library/ie/cc848872%28v=vs.85%29.aspx"><code>aria-controls</code></a> properties in the code above, are unlikely to find as much mainstream support for inclusion as perhaps <code>haspopup</code> and <code>controls</code> will have.

As Steve Faulkner points out in “<a href="https://blog.paciellogroup.com/2010/04/html5-and-the-myth-of-wai-aria-redundance/">HTML5 and the Myth of WAI-ARIA Redundance</a>”, much of ARIA will continue to exist unbested. The unique power of ARIA is to bridge the gap between the experiences of sighted and unsighted web users.</p>

## Role-Playing

A lot of my friends and colleagues are keen on tabletop role-playing games, which, in case you’re not familiar with them, are games in which participants play fictional characters who embark on quests and fight battles in fantastical worlds. Although I’m not a big exponent of these games myself, I’ve noticed similarities between the way characters are role-played in games and the way HTML elements act within web applications. Accordingly, I’ll use this role-playing metaphor to explain ARIA’s <strong>roles, properties and states</strong> in greater detail.

Don’t worry, you won’t have to be a big role-playing geek to follow along. I’m not!

## Roles

Each player in a role-playing game normally maintains a “character sheet” that lists the important characteristics of the character they are playing. In HTML, the name of the character might be the <code>id</code> of an element. Each must be unique.

Characters have a lot more information than that in the sheet, though. For example, characters dwelling in these fantasy worlds usually belong to one “race” or another. Common standbys are elves, dwarves and trolls. These are like HTML element types: broad groupings of participants with common characteristics.

<figure></figure>

In ARIA, the <code>role</code> attribute overrides the element type, much like a player in a game overrides their workaday existence as a 21st-century human to become a mighty dwarf. In the example from the last section, an insipid <code>&lt;div&gt;</code> assumed the role of a checkbox by being given <code>role="checkbox"</code>.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2d1d66fd-53ea-44f9-937c-b7410ae5b171/4-wai-char-sheet-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/27f306a0-9da9-4f1e-8149-dc7e56a0aa24/4-wai-char-sheet-preview-opt.jpg" alt="4-wai-char-sheet-preview-opt" width="500" height="299" /></a></figure>

<a href="https://www.w3.org/TR/wai-aria/roles">Roles in ARIA</a>, like races in a role-playing game, are a part of a character’s identity that we might be interested in. We might expect dwarves to be strong and good at constructing machines, just like we expect a <code>&lt;button&gt;</code> to have the characteristics and behaviors already discussed. By putting <code>role="button"</code> on an element that isn’t actually a <code>&lt;button&gt;</code>, we are asking assistive technologies to identify it as a button, evoking those characteristics.</p>

## Properties

Character sheets with just names and races would be a bit limited. We’d probably be a bit uncomfortable with so much emphasis on race, too. The whole point of ARIA is that it recognizes elements not just for their generic, reductive classification. Much better to identify characters and elements by their individual assets and talents.

A typical sheet would list a set of characteristics for a character that, in one way or another, the game identifies as having a certain currency and importance. For instance, you might be an elf but one who is special for the ability to cast certain magic spells. In much the same way, we looked at an <code>&lt;a&gt;</code> element that is made special for having the property of a submenu. This would be identified to the accessibility layer, just like the basic role, via the <code>aria-haspopup="true"</code> property attribute.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/824cbaba-8f44-4a89-a687-9d490c8a47bb/5-wai-char-sheet-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/331c7b7c-0d14-428d-abc7-17368f22f46e/5-wai-char-sheet-preview-opt.jpg" alt="5-wai-char-sheet-preview-opt" width="500" height="318" /></a></figure>

A <a href="https://www.w3.org/TR/wai-aria/states_and_properties">huge number of properties</a> have been specified and documented. Some are global, meaning that any element may have them, while others are reserved for particular contexts and elements. Dwarves are usually precluded from having good longbow accuracy, whereas the skill is common to elves. The <code>aria-label</code> that we would use to label a button is global, whereas <code>aria-required</code>, which denotes a required user entry, would normally be used in form fields or elements with form-field roles, such as <code>listbox</code> and <code>textbox</code>.</p>

## States

Perhaps the most important distinction between a static web document and an application is that the elements in an application tend to change — sometimes dramatically — according to user interaction and timed events. Depending on what’s happening in an application at any one time, the elements therein could be said to be in certain, often temporary, states.

In role-playing games, you have to keep tabs on the state of your character: How healthy are you? What items have you collected? Who have you befriended? This is all scribbled down, erased and scribbled down some more on the character sheet. Keeping track of the state of interactive elements is important for accessibility, too.

In your application, the state of an element is usually represented visually. In role-playing games and in screen-reader buffers, this is not the case: It has to be imagined. If your dwarf character has donned their magic cloak of invisibility, you’d probably want to write this down on the character sheet so that you remember. Similarly, writing the <a href="https://www.w3.org/TR/wai-aria/states_and_properties#aria-hidden"><code>aria-hidden</code> attribute</a> on an element ensures that the accessible state of invisibility is recorded properly.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b48a4963-206e-4cdb-b9a4-0ed0a3e578f4/6-wai-char-sheet-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/521a3f74-5efd-4e3c-8ae6-be139fd08569/6-wai-char-sheet-preview-opt.jpg" alt="6-wai-char-sheet-preview-opt" width="500" height="338" /></a></figure>

States such as <a href="https://www.w3.org/TR/wai-aria/states_and_properties#aria-expanded"><code>aria-expanded</code></a> are announced according to a value of <code>true</code> or <code>false</code>. An item with <code>aria-expanded="false"</code> is announced by JAWS and NVDA Windows screen readers as “collapsed.” If — or, rather, when — it is set to <code>aria-expanded="true"</code>, then the item will be announced as “expanded.”

## Our First ARIA Widget

It’s about time we put everything we’ve learned about roles, properties and states into practice and build our first ARIA widget.

The term “widget” is often used in JavaScript development to denote a singular pocket of script-enabled interactive functionality. Mercifully, the ARIA definition corresponds, and ARIA widgets can be thought of as JavaScript widgets that have been made accessible with appropriate ARIA attributes.

Let’s make a simple toolbar — a group of button controls that enable us to organize some content. In this case, we’ll set up controls to sort content alphabetically and reverse alphabetically. Fortunately, we have access to the W3C’s guide on authoring ARIA widgets, “<a href="https://www.w3.org/WAI/PF/aria-practices/#accessiblewidget">General Steps for Building an Accessible Widget With WAI-ARIA</a>,” which covers a similar example for a toolbar.</p>

### The Toolbar Role

There’s no such thing as a <code>&lt;toolbar&gt;</code> element in HTML, unless you <a href="https://www.techrepublic.com/blog/web-designer/learn-more-about-web-components-with-these-demos/">create one as a web component</a>. In any case, because there’s no <em>standard</em> element for toolbars, we need to include the <code>toolbar</code> role in our toolbar’s parent element. This marks the scope of the widget:

<pre><code class="language-markup">
&lt;div role="toolbar"&gt;
  /* toolbar functionality goes here */
&lt;/div&gt;
</code></pre>

(Note: A <code>&lt;menu&gt;</code> element takes a <code>type</code> of <code>toolbar</code>, but it has <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/menu">not been adopted by browser vendors</a> so is unable to provide the information we need.)

The toolbar’s purpose in our design should be obvious from its visual relationship to the content it affects. This won’t communicate anything aurally, however, so we should provide an accessible name for our toolbar via the now familiar <code>aria-label</code> property. That’s one role and one property so far.

<pre><code class="language-markup">
&lt;div role="toolbar" aria-label="sorting options"&gt;
  /* toolbar functionality goes here */
&lt;/div&gt;
</code></pre>

Now let’s add the buttons that will be our controls.

<pre><code class="language-markup">&lt;div role="toolbar" aria-label="sorting options"&gt;
  &lt;button&gt;A to Z&lt;/button&gt;
  &lt;button&gt;Z to A&lt;/button&gt;
&lt;/div&gt;
</code></pre>

Even without the additional widget properties and states, we’ve already improved the user’s recognition of the toolbar: Using the NVDA screen reader or the JAWS screen reader with Firefox, when a user focuses the first button, they are informed that they’re inside a toolbar and — thanks to the <code>aria-label</code> — told what it is for.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/77dfc5c9-567b-43f7-8f78-9f4a88bc208f/7-wai-toolbar-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4ec1a0fb-6398-4d6e-9eaa-43c42a57273b/7-wai-toolbar-preview-opt.jpg" alt="7-wai-toolbar-preview-opt" width="500" height="223" /></a></figure>

### The Relationship

So far, we haven’t actually connected our toolbar to the content it controls. We need a relationship attribute, which is a special kind of property attribute that communicates a relationship between elements. Our widget is used to control the content, to manipulate and reorganize it, so we’ll go with <code>aria-controls</code>. We’ll join the dots using an <code>id</code> value, just as we did in the earlier example of the popup menu.

<pre><code class="language-markup">
&lt;div role="toolbar" aria-label="sorting options" aria-controls="sortable"&gt;
  &lt;button&gt;A to Z&lt;/button&gt;
  &lt;button&gt;Z to A&lt;/button&gt;
&lt;/div&gt;

&lt;ul id="sortable"&gt;
  &lt;li&gt;Fiddler crab&lt;/li&gt;
  &lt;li&gt;Hermit crab&lt;/li&gt;
  &lt;li&gt;Red crab&lt;/li&gt;
  &lt;li&gt;Robber crab&lt;/li&gt;
  &lt;li&gt;Sponge crab&lt;/li&gt;
  &lt;li&gt;Yeti crab&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

Note that we’ve added <code>aria-controls</code> to the toolbar itself, not to each individual button. Both would be acceptable, but using it just the once is more succinct, and the buttons should each be considered individual components that belong to the controlling toolbar. If we want to check which properties and states are supported for widget roles like <code>toolbar</code>, the specification provides a list of “<a href="https://www.w3.org/WAI/PF/aria/roles#toolbar">inherited states and properties</a>” in each case. Consult this when you build a widget. <a href="https://www.w3.org/WAI/PF/aria/roles#toolbar">As you will see</a>, <code>aria-controls</code> is an inherited property of <code>toolbar</code>.

Some screen readers do very little explicitly with this relationship of information, while others are quite outspoken. JAWS actually announces a keyboard command to enable the user to move focus to the controlled element: “Use <code>JAWS key + Alt + M</code> to move to controlled element.” Once you’ve affected it, you might want to go and inspect it, and JAWS is helping you to do just that here.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/89ab902e-2690-468a-8c5e-862fbc3e4956/8-wai-toolbar-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d3097ee2-b3c1-420a-8b95-9d1f91df00e4/8-wai-toolbar-preview-opt.jpg" alt="8-wai-toolbar-preview-opt" width="500" height="315" /></a></figure>

### Pressed and Unpressed

Depending on which sorting option is our current preference, we could say that the button that commands that option is in a “selected,” or “pressed,” state. This is where the <code>aria-pressed</code> state attribute comes in, taking a value of <code>true</code> for pressed or <code>false</code> for unpressed. States are dynamic and should be toggled with JavaScript. On the page being loaded, just the first button will be set to <code>true</code>.

<pre><code class="language-markup">
&lt;div role="toolbar" aria-label="sorting options" aria-controls="sortable"&gt;
  &lt;button aria-pressed="true"&gt;A to Z&lt;/button&gt;
  &lt;button aria-pressed="false"&gt;Z to A&lt;/button&gt;
&lt;/div&gt;
&lt;ul id="sortable"&gt;
  &lt;li&gt;Fiddler crab&lt;/li&gt;
  &lt;li&gt;Hermit crab&lt;/li&gt;
  &lt;li&gt;Red crab&lt;/li&gt;
  &lt;li&gt;Robber crab&lt;/li&gt;
  &lt;li&gt;Sponge crab&lt;/li&gt;
  &lt;li&gt;Yeti crab&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

Pairing the styles for active (<code>:active</code>) buttons with the styles for <code>aria-pressed</code> buttons is a good practice. Both are buttons that have been “pushed down,” whether momentarily or semi-permanently.

<pre><code class=" language-css">button:active, button[aria-pressed="true"] {
  position: relative;
  top: 3px; /* 3px drop */
  box-shadow: 0 1px 0 #222; /* less by 3px */
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6c3b408f-dbc8-4d45-8c27-2867effcbaf4/9-wai-toolbar-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2afbbb94-99ea-4df9-adeb-c1aed0053b28/9-wai-toolbar-preview-opt.jpg" alt="9-wai-toolbar-preview-opt" width="500" height="235" /></a></figure>

When the user focuses a button with <code>aria-pressed</code> present using either NVDA or JAWS with Firefox, the button is identified as a “toggle button.” Using the latest version of JAWS and focusing a button with <code>aria-pressed="true"</code> will append the word “pressed” to the announcement accordingly. In the <a href="https://www.chromevox.com/">ChromeVox</a> screen reader for the Chrome browser, an <code>aria-pressed="true"</code> button is announced as “button pressed” and <code>aria-pressed="false"</code> as “button not pressed.” To a greater or lesser extent, most modern browsers and screen readers articulate helpful information about the state or potential state of these buttons.</p>

### Keyboard Controls

Not quite there yet. For toolbars — as with many ARIA widgets — the W3C <a href="https://www.w3.org/WAI/PF/aria-practices/#toolbar">recommends certain keyboard navigation features</a>, often to emulate the equivalent in desktop software. Pressing the left and right arrow keys should switch focus between the buttons, and pressing “Tab” should move focus out of the toolbar. We’ll add <code>tabindex="-1"</code> to the list and focus it using JavaScript whenever the user presses “Tab.” We do this to allow users to move directly to the list once they’ve chosen a sorting option. In a toolbar with several buttons, this could potentially save them from having to tab through a number of adjacent buttons to get to the list.

<pre><code class="language-markup">
&lt;div role="toolbar" aria-label="sorting options" aria-controls="sortable"&gt;
    &lt;button aria-pressed="true"&gt;A to Z&lt;/button&gt;
    &lt;button aria-pressed="false"&gt;Z to A&lt;/button&gt;
  &lt;/div&gt;
  &lt;ul id="sortable" tabindex="-1"&gt;
    &lt;li&gt;Fiddler crab&lt;/li&gt;
    &lt;li&gt;Hermit crab&lt;/li&gt;
    &lt;li&gt;Red crab&lt;/li&gt;
    &lt;li&gt;Robber crab&lt;/li&gt;
    &lt;li&gt;Sponge crab&lt;/li&gt;
    &lt;li&gt;Yeti crab&lt;/li&gt;
  &lt;/ul&gt;
  </code></pre>

<pre><code class=" language-javascript">
$(listToSort).focus();
</code></pre>

## All Done

That concludes our ARIA widget. A <a href="https://heydonworks.com/practical_aria_examples/#toolbar-widget">live demo</a> is ready for you to play with and test. Remember that it’s not really about sorting, per se — that’s all done with JavaScript. The aim is to make explicit the relationships and states of our application, so that whatever we are doing to our content — sorting it, editing it, searching it, creating it, recreating it — our users on keyboards and screen readers are kept in the loop.

The next chapter of the <a href="https://shop.smashingmagazine.com/apps-for-all-coding-accessible-web-applications.html">Apps For All: Coding Accessible Web Applications</a> eBook puts the application functionality to one side and addresses how to actually <em>find</em> that application functionality in the first place. Mobility is a big part of accessibility online and off, so it's important to look at different ways to help our users get around.

{{< signature "al, il" >}}


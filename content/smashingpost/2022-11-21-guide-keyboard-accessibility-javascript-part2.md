---
title: 'A Guide To Keyboard Accessibility: JavaScript (Part 2)'
slug: guide-keyboard-accessibility-javascript-part2
author: cristian-diaz
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a82e6cd4-ff56-4c9f-b2ba-dc9ce1403ccf/guide-keyboard-accessibility-javascript-part2.jpg
date: 2022-11-21T10:00:00.000Z
summary: >-
  This article is the second of two parts about a guide to making websites accessible to keyboard users. Here Cristian Diaz covers a toolset on JavaScript that you can mix into different components to create a great experience for keyboard users.
description: >-
  This article is the second of two parts about a guide to making websites accessible to keyboard users. Here Cristian Diaz covers a toolset on JavaScript that you can mix into different components to create a great experience for keyboard users.
categories:
  - Accessibility
  - HTML
  - CSS
  - JavaScript
  - Guides
---

In the [previous article](https://www.smashingmagazine.com/2022/11/guide-keyboard-accessibility-html-css-part1/), we talked about how to improve accessibility for keyboard users using HTML and CSS. Those languages can do the job most of the time, but certain design requirements and the nature of certain components create the need for more complex interactions, and this is where JavaScript comes into play.

For keyboard accessibility purposes, most of the job is done with basic tools that open many possibilities for keyboard interactivity. This article covers a toolset that you can mix into different components to improve accessibility for keyboard users.

## The Basics

Most of the time, your job with JavaScript to enhance components’ keyboard accessibility will be done with just a handful of tools, including the use of event listeners and certain JavaScript methods of a couple of Web APIs that can help us in this task.

One of the most important tools we have to add interactivity to our projects is the existence of **events,** which is the execution of functions that trigger when the element you’re checking receives a change. 

### `keydown` Event

One example of an event you can listen to with this Web API is the `keydown` event, which checks when a key is pressed.

Now, this isn’t used to add keyboard accessibility to elements like buttons or links because, by default, when you add a `click` event listener to them, this will also trigger the event when you use the <kbd>Enter</kbd> (for button and links) and <kbd>Space</kbd> keys (button only). Instead, the utility of the `keydown` event comes when you need to add functionality to other keys.

To add an example, let’s come back to [the tooltip we created in the first part of this article](https://www.smashingmagazine.com/2022/11/guide-keyboard-accessibility-html-css-part1/#tooltips). I mentioned that this tooltip needs to be closed when you press the <kbd>Esc</kbd> key. We’d need a `keydown` event listener to check if the pressed key is <kbd>Esc</kbd>. For that, we need to detect the event’s pressed key. In this case, we’ll check the event `key`’s property.

We’ll use [keycode.info](http://keycode.info) to check the event dump for this key. If you press the <kbd>Esc</kbd> key on this page, you’ll notice that `e.key` is equal to `"Escape"`. 

**Note:** *There are two other ways to detect the pressed key, and those are checking `e.keyCode` and `e.which`. They will return a number. In the case of the <kbd>Esc</kbd> key, it’ll be* ***27***. *But, keep in mind those are deprecated alternatives, and while they work, `e.key` is the preferred option.*

With that, we need to select our buttons and add the event listener. My approach to this matter is to use this event listener to add a class to the button and add this class as an exception to show it using the `:not()` pseudo-class. Let’s start changing our CSS a bit:

<pre><code class="language-css">button:not(.hide-tooltip):hover + [role="tooltip"],
button:not(.hide-tooltip):focus + [role="tooltip"],
[role="tooltip"]:hover {
  display: block;
}
</code></pre>

Now, with this exception added, let’s create our event listener!

<pre><code class="language-javascript">const buttons = [...document.querySelectorAll("button")]

buttons.forEach(element =&gt; {
  element.addEventListener("keydown", (e) =&gt; {
    if (e.key === "Escape") {
      element.classList.add("hide-tooltip")
    }
  })
})
</code></pre>

And there you have it! With just a sprinkle of JavaScript, we have added an accessibility function to our tooltip. And that was just the start of what we can do with a `keydown` event listener. It’ll be a crucial tool to improve keyboard accessibility for multiple components, but there is another event listener we should take into consideration.

### `blur` Event

There is another event we’ll use often. This one detects when the element stops receiving focus. This event listener is important, and most of the time, you’ll use it to reverse the possible changes you have made with the `keydown` event listener.

Let’s come back to the tooltip. Right now, it has a problem: if you press the <kbd>Esc</kbd> key to close the tooltip, and then you focus on the same element again, the tooltip won’t appear. Why? Because we added the `hide-tooltip` class when you press the <kbd>Esc</kbd> key, but **we never removed this class.** This is where `blur` comes into play. Let’s add an event listener to revert this functionality.

<pre><code class="language-javascript">element.addEventListener("blur", (e) =&gt; {
  if (element.classList.contains("hide-tooltip")) {
    element.classList.remove("hide-tooltip");
  }
});
</code></pre>

### Other Event Listeners (And Why You Might Don’t Need Them)

I mentioned that we’re going to need two event listeners in our toolkit, but there are other event listeners you could use, like `focusout` or `focus`. However, I think use cases for them are quite scarce. There is a special mention to `focus` because even if you can find good use cases for it, you need to be very careful. After all, if you don’t use it properly, you can cause a **change of context.**

A change of context is defined by WCAG as “major changes that, if made without user awareness, can disorient users who are not able to view the entire page simultaneously.” Some examples of change of context include:

- Opening a new window;
- Changing the layout of your site significantly;
- Moving the focus to another part of the site.

This is important to keep in mind because creating a change of context at the moment of focusing on an element is a failure of WCAG criteria 3.2.1:

<blockquote>When any user interface component receives focus, it does not initiate a change of context.<br /><br />&mdash; Success Criterion 3.2.1: Focus order</blockquote>

If you’re not careful, bad use of a function that listens to the `focus` event can create a change of context. Does that mean you shouldn’t use it? Not really, but to be honest, I can hardly find a use for this event. Most of the time, you’ll be using the `:focus` pseudo-class to create similar functionalities.

With that said, there is at least one component pattern that can benefit from this event listener in some cases, but I’ll cover it later when I start talking about components, so let’s put a pin on that topic for now.

### `focus()` Method

Now, **this** is something we’ll be using with some frequency! This method from the HTMLElement API allows us to bring the keyboard focus to a particular element. By default, it’ll draw the focus indicator in the element and will scroll the page to the element’s location. This behavior can be changed with a couple of parameters:

- `preventScroll`  
When it’s set to `true`, will make the browser doesn’t scroll until the programmatically focused element.
- `focusVisible`  
When set to `false`, it will make the programmatically focused element doesn’t display its focus indicator. This property **works only on Firefox right now**.

Keep in mind that to focus the element, it needs to be either focusable or tabbable. If you need to bring the focus to a normally not tabbable element (like a dialog window), you’ll need to add the attribute `tabindex` with a negative integer to make it focusable. You can check out how `tabindex` works in [the first part of this guide](https://www.smashingmagazine.com/2022/11/guide-keyboard-accessibility-html-css-part1/#tabindex-attribute).

<pre><code class="language-html">&lt;button id="openModal"&gt;Bring focus&lt;/button&gt;
&lt;div id="modal" role="dialog" tabindex="-1"&gt;
  &lt;h2&gt;Modal content&lt;/h2&gt;
&lt;/div&gt;
</code></pre>

Then we’ll add a `click` event listener to the button to make the dialog window focused:

<pre><code class="language-javascript">const button = document.querySelector("#openModal");
const modal = document.querySelector("#modal")

button.addEventListener("click", () =&gt; {
  modal.focus()
})
</code></pre>

And there you have it! This method will be very handy in a lot of components in tandem with the `keydown` attribute, so understanding how both of them work is crucial.

### Changing HTML Attributes With JavaScript

Certain HTML attributes need to be modified with JavaScript to create accessibility in complex component patterns. Two of the most important ones for keyboard accessibility are `tabindex` and the more recently added `inert`. `tabindex` can be modified using `setAttribute`. This attribute requires two parameters:

- `name`  
It checks the name of the attribute you want to modify.
- `value`  
It will add the string this attribute requires if it doesn’t require a particular attribute (for example, if you add the attributes `hidden` or `contenteditable`, you’ll need to use an empty string).

Let’s check a quick example of how to use it:

<pre><code class="language-javascript">const button = document.querySelector("button")

button.setAttribute("tabindex", "-1")
</code></pre>

`setAttribute` will help a lot for accessibility in general. (I use it a lot to change ARIA attributes when needed!) But, when we talk about keyboard accessibility, `tabindex` is almost the only attribute you’ll be modifying with this method.

I mentioned the `inert` attribute before, and this one works a bit differently because it has its own property in the HTMLElement Web API. `HTMLElement.inert` is a boolean value that will let us toggle the `inert` attribute.

Keep in mind a couple of things before thinking about using this attribute:

- You’ll need a polyfill because it’s not fully implemented in all browsers and is still quite recent. [This polyfill](https://github.com/WICG/inert) created by Chrome engineers works pretty well in the tests I have made, so if you need this property, this is a safe approach, but keep in mind that it might have unexpected behaviors.
- You can use `setAttribute` to change this attribute as well! Both work equally well, even with a polyfill. Whichever you decide to use is up to you.

<pre><code class="language-javascript">const button = document.querySelector("button")

// Syntax with HTMLElement.inert
button.inert = true

// Syntax with Element.setAttribute()
button.setAttribute("inert", "")
</code></pre>

This combination of tools will be handy for keyboard accessibility purposes. Now let’s start to see them in action!

{{% feature-panel %}} 

## Component Patterns

### Toggletips

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef80660a-1d7c-4d84-a253-12d61f9a51c4/1-guide-keyboard-accessibility-html-css-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef80660a-1d7c-4d84-a253-12d61f9a51c4/1-guide-keyboard-accessibility-html-css-part2.png" width="800" height="194" sizes="100vw" caption="Carbon Design System toggletip. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef80660a-1d7c-4d84-a253-12d61f9a51c4/1-guide-keyboard-accessibility-html-css-part2.png'>Large preview</a>)" alt="A button being keyboard focused with a message below it that says 'Custom content here'" >}}

We learned how to make a tooltip in the previous part, and I mentioned how to enhance it with JavaScript, but there is another pattern for this kind of component called **toggletip**, which is a tooltip that works when you click them, instead of hovering on them.

Let’s check a quick list of what we need to make sure it happens:

- When you press the button, the information should be announced to screen readers. That should happen when you press the button again. Pressing the button **won’t close the toggletip**.
- The toggletip will be closed when you either click outside the toggletip, stop focusing the button, or press the <kbd>Esc</kbd> key.

I’ll take Heydon Pickering’s approach that he talks about in his book [*Inclusive Components*](https://inclusive-components.design/tooltips-toggletips/). So, let’s start with the markup:

<pre><code class="language-html">&lt;p&gt;If you need to check more information, check here
  &lt;span class="toggletip-container"&gt;
    &lt;button class="toggletip-button"&gt;
      &lt;span class="toggletip-icon" aria-hidden="true"&gt;?&lt;/span&gt;
      &lt;div class="sr-only"&gt;Más información&lt;/div&gt;
    &lt;/button&gt;
    &lt;span role="status" class="toggletip-info"&gt;&lt;/span&gt;
  &lt;/span&gt;
&lt;/p&gt;
</code></pre>

The idea is to inject the necessary HTML inside the element with the `role="status"`. That’ll make screen readers announce the content when you click it. We’re using a `button` element to make it tabbable. Now, let’s create the script to show the content!

<pre><code class="language-javascript">toggletipButton.addEventListener("click", () =&gt; {
  toggletipInfo.innerHTML = "";
  setTimeout(() =&gt; {
    toggletipInfo.innerHTML = toggletipContent;
  }, 100);
});
</code></pre>

As Heydon mentions in his book, we use this approach of first removing the container’s HTML content and then using `setTimeout` to add it to make sure every time you click it, it’ll be announced for screen reader users. Now we need to check that when you’re clicking elsewhere, the content stops showing.

<pre><code class="language-javascript">document.addEventListener("click", (e) =&gt; {
  if (toggletipContainer !== e.target) {
    toggletipInfo.innerHTML = ""
  }
})
</code></pre>

With that out of the way, it’s time to add keyboard accessibility to this component. We don’t need to make the toggletip’s content show when you press the button because a good HTML semantic does that for us already. We need to make the toggletip’s content stop showing when you press the <kbd>Esc</kbd> key and when you stop focusing on this button. It works very similarly to what we did for tooltips in the previous section as examples, so let’s start working with that. First, we’ll use the `keydown` event listener to check when the <kbd>Esc</kbd> key is pressed:

<pre><code class="language-javascript">toggletipContainer.addEventListener("keydown", (e) =&gt; {
  if (e.key === "Escape") {
    toggletipInfo.innerHTML = ""
    }
})
</code></pre>

And now, we need to check the `blur` event to do the same. This one should be on the `button` element instead of the container itself.

<pre><code class="language-javascript">
toggletipButton.addEventListener("blur", () => {
  toggletipInfo.innerHTML = "";
});
</code></pre>

And this is our result!

{{< codepen height="480" theme_id="light" slug_hash="WNyjeJK" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Toggletip demo [forked]](https://codepen.io/smashingmag/pen/WNyjeJK) by <a href="https://codepen.io/ItsCrisDiaz">Cristian Diaz</a>.{{< /codepen >}}

As I mentioned, this works very similarly to the tooltip we made, but I did that for a reason. Unless you’re making something very unconventional, those patterns will repeat themselves quite often.

As Stephanie Eckles mentions in her article “[4 Required Tests Before Shipping New Features](https://thinkdobecreate.com/articles/4-required-tests-before-shipping-new-features/)”, there are some expected behaviors keyboard users expect from components, like being able to close something you just opened by pressing the <kbd>Esc</kbd> key, or being able to navigate a group of related options using the <kbd>Arrow</kbd> keys.

If you keep those patterns in mind, you’ll notice overlap in certain components’ behaviors, and that’ll repeat when you start creating JavaScript code to ensure keyboard accessibility. So keeping this list in mind will help you to understand what requirements the components you’re creating will need.

Speaking of which, let’s check another common component pattern.

### Tabs

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e09cf858-6d61-45cb-826e-479b514c4a09/2-guide-keyboard-accessibility-html-css-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e09cf858-6d61-45cb-826e-479b514c4a09/2-guide-keyboard-accessibility-html-css-part2.png" width="800" height="531" sizes="100vw" caption="Carbon Design System tabs. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e09cf858-6d61-45cb-826e-479b514c4a09/2-guide-keyboard-accessibility-html-css-part2.png'>Large preview</a>)" alt="Two groups of tabs: the first one has grey text and a border at the bottom, and the selected one has darker text with a blue border. The second tab group has grey text and a grey background, while the selected tab has a lighter background and a blue top border" >}}

#### Roving `tabindex`

Tabbed interfaces are patterns that you can still see from time to time. They have a very interesting functionality when we talk about keyboard navigation: when you press the <kbd>Tab</kbd> key, it’ll go to the active tab panel. To navigate between the tab list, you’ll need to use the <kbd>Arrow</kbd> keys. This is a technique called **roving `tabindex`** that consists in removing the ability of the non-active elements to be tababble by adding the attribute `tabindex="-1"` and then using other keys to allow the navigation between those items.

With tabs, this is the expected behavior for those:

- When you press <kbd>Left</kbd> or <kbd>Up</kbd> keys, it’ll move the keyboard focus onto the previous tab. If the focus is on the first tab, it’ll move the focus to the last tab.
- When you press the <kbd>Right</kbd> or <kbd>Down</kbd> keys, it’ll move the keyboard focus onto the next tab. If the focus is on the first tab, it’ll move the focus to the last tab.

Creating this functionality is a mix of three techniques we saw before: modifying `tabindex` with `setAttribute`, the `keydown` event listener, and the `focus()` method. Let’s start by checking the markup of this component:

<pre><code class="language-html">&lt;ul role="tablist"&gt;
  &lt;li role="presentation"&gt;
    &lt;button id="tab1" role="tab" aria-selected="true"&gt;Tomato&lt;/button&gt;
  &lt;/li&gt;
  &lt;li role="presentation"&gt;
    &lt;button id="tab2" role="tab" tabindex="-1"&gt;Onion&lt;/button&gt;
  &lt;/li&gt;
  &lt;li role="presentation"&gt;
    &lt;button id="tab3" role="tab" tabindex="-1"&gt;Celery&lt;/button&gt;
  &lt;/li&gt;
  &lt;li role="presentation"&gt;
    &lt;button id="tab4" role="tab" tabindex="-1"&gt;Carrot&lt;/button&gt;
  &lt;/li&gt;
&lt;/ul&gt;
&lt;div class="tablist-container"&gt;
  &lt;section role="tabpanel" aria-labelledby="tab1" tabindex="0"&gt;
  &lt;/section&gt;
  &lt;section role="tabpanel" aria-labelledby="tab2" tabindex="0" hidden&gt;
  &lt;/section&gt;
  &lt;section role="tabpanel" aria-labelledby="tab3" tabindex="0" hidden&gt;
  &lt;/section&gt;
  &lt;section role="tabpanel" aria-labelledby="tab4" tabindex="0" hidden&gt;
  &lt;/section&gt;
&lt;/div&gt;
</code></pre>

We are using `aria-selected="true"` to show which is the active tab, and we’re adding `tabindex="-1"` to make the non-active tabs unable to be selected with the <kbd>Tab</kbd> key. Tabpanels should be tabbable if there is no tabbable element inside of it, so this is why I added the attribute `tabindex="0"` and the non-active tabpanels are hidden by using the attribute `hidden`.

Time to add the navigation with the arrow keys. For this, we’ll need to create an array with the tabs and then create a function for it. Our next step is to check which is the first and last tab in the list. This is important because the action that will happen when you press a key will change if the keyboard focus is on one of those elements.

<pre><code class="language-javascript">const TABS = [...TABLIST.querySelectorAll("[role='tab']")];

const createKeyboardNavigation = () =&gt; {
  const firstTab = TABS[0];
  const lastTab = TABS[TABS.length - 1];
}
</code></pre>

After that, we’ll add a `keydown` event listener to each tab. I’ll start by adding the functionality with <kbd>Left</kbd> and <kbd>Up</kbd> arrows.

<pre><code class="language-javascript">// Previous code of the createKeyboardNavigation function
TABS.forEach((element) =&gt; {
  element.addEventListener("keydown", function (e) {
    if (e.key === "ArrowUp" || e.key === "ArrowLeft") {
      e.preventDefault();
      if (element === firstTab) {
        lastTab.focus();
      } else {
        const focusableElement = TABS.indexOf(element) - 1;
        TABS[focusableElement].focus();
      }
    }
  }
}
</code></pre>

This is what’s happening here:

- First, we check that the pressed key is the <kbd>Up</kbd> or <kbd>Left</kbd> arrow. For that, we check the `event.key`.
- If that’s true, we need to prevent those keys scroll the page because, remember, by default, they do that. We can use `e.preventDefault()` for this goal.
- If the focused key is the first tab, it’ll automatically bring the keyboard focus to the last one. This is made by calling the method `focus()` to focus the last tab (which we store in a variable).
- If it’s not the case, we need to check which is the position of the active tab. As we store the tab elements in an array, we can use the method `indexOf()` to check the position.
- As we’re trying to navigate to the previous tab, we can subtract `1` from the result of `indexOf()` and then search the corresponding element in the `TABS` array and programmatically focus it with the `focus()` method.

Now we need to do a very similar process with the <kbd>Down</kbd> and <kbd>Right</kbd> keys:

<pre><code class="language-javascript">// Previous code of the createKeyboardNavigation function
else if (e.key === "ArrowDown" || e.key === "ArrowRight") {
  e.preventDefault();
  if (element == lastTab) {
    firstTab.focus();
  } else {
    const focusableElement = TABS.indexOf(element) + 1;
    TABS[focusableElement].focus();
  }
}
</code></pre>

As I mentioned, it’s a very similar process. Instead of subtracting one from the `indexOf()` result, we **add** `1` because we want to bring the keyboard focus to the **next** element.

#### Showing The Content And Changing HTML Attributes

We created the navigation, and now we need to show and hide the content as well as manipulate the attributes `aria-selected` and `tabindex`. Remember, we need to make that when the keyboard focus is on the active panel, and you press <kbd>Shift</kbd> + <kbd>Tab</kbd>, the focus should be in the active tab.

First, let’s create the function that shows the panel.

<pre><code class="language-javascript">const showActivePanel = (element) =&gt; {
  const selectedId = element.target.id;
  TABPANELS.forEach((e) =&gt; {
    e.hidden = "true";
  });
  const activePanel = document.querySelector(
    `[aria-labelledby="${selectedId}"]`
  );
  activePanel.removeAttribute("hidden");
};
&lt;
</code></pre>

What we’re doing here is checking the `id` of the tab is being pressed, then hiding all the tab panels, and then looking for the tab panel we want to activate. We’ll know it’s the tab because it has the attribute `aria-labelledby` and uses the same value as the tab’s `id`. Then we show it by removing the attribute `hidden`.

Now we need to create a function to change the attributes:

<pre><code class="language-javascript">const handleSelectedTab = (element) =&gt; {
  const selectedId = element.target.id;
  TABS.forEach((e) =&gt; {
    const id = e.getAttribute("id");
    if (id === selectedId) {
      e.removeAttribute("tabindex", "0");
      e.setAttribute("aria-selected", "true");
    } else {
      e.setAttribute("tabindex", "-1");
      e.setAttribute("aria-selected", "false");
    }
  });
};
</code></pre>

What we’re doing here is, again, checking the `id` attribute and then looking at each tab. We’ll check if this tab’s `id` corresponds with the pressed element’s `id`.

If it’s the case, we’ll make it keyboard tabbable by either removing the attribute `tabindex` (because it’s a `button`, so it’s keyboard tabbable by default) or by adding the attribute `tabindex="0"`. Additionally, we’ll add an indicator to screen reader users that this is the active tab by adding the attribute `aria-selected="true"`.

If it doesn’t correspond, `tabindex` and `aria-selected` will be set to `-1` and `false`, respectively.

Now, all we need to do is add a `click` event listener to each tab to handle both functions.

<pre><code class="language-javascript">TABS.forEach((element) =&gt; {
  element.addEventListener("click", (element) =&gt; {
    showActivePanel(element),
    handleSelectedTab(element);
  });
});
</code></pre>

And that’s it! We created the functionality to make tabs work, but we can do a little something else if needed.

#### Activate Tab On Focus

Do you remember what I mentioned about the `focus` event listener? You should be careful when you use it because it can create a change of context by accident, but it has some use, and **this** component is a perfect opportunity to use it!

According to [ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/practices/keyboard-interface/#kbd_selection_follows_focus), we can make the displayed content show when you focus on the tab. This concept is often referred to as a **follow focus** and can be helpful for keyboard and screen reader users because it allows navigating more easily through the content.

However, you need to keep a couple of considerations about it:

- If showing the content means making a lot of petitions and, by extension, making the network slower, making the displayed content follow the focus is not desired.
- If it changes the layout in a significant way, that can be considered a change of context. That depends on the kind of content you want to show, and doing a change of context on focus is an accessibility issue, as I explained previously.

In this case, the amount of content doesn’t suppose a big change in either network or layout, so I’ll make the displayed content follows the focus of the tabs. This is a very simple task with the `focus` event listener. We can just literally copy and paste the event listener we created and just change `click` to `focus`.

<pre><code class="language-javascript">TABS.forEach((element) =&gt; {
  element.addEventListener("click", (element) =&gt; {
    showActivePanel(element),
    handleSelectedTab(element);
  });

  element.addEventListener("focus", (element) =&gt; {
    showActivePanel(element),
    handleSelectedTab(element);
  });
});
</code></pre>

And there you have it! Now the displayed content will work without the need to click the tab. Doing that or making it only work with a click is up to you and is surprisingly a very nuanced question. Personally, I’d stick just with making it shows when you press the tab because I think the experience of changing the attribute `aria-selected` by just focusing on the element can be slightly confusing. Still, it’s just a hypothesis on my part so take what I say with a grain of salt and always check it with users.

#### Additional `keydown` Event Listeners

Let’s come back to the `createKeyboardNavigation` for a moment. There are a couple of keys we can add. We can make the <kbd>Home</kbd> and <kbd>End</kbd> key brings the keyboard focus to the first and last tab, respectively. This is completely optional, so it’s ok if you don’t do it, but just to reiterate how a `keydown` event listener helps out, I’ll do that.

It’s a very easy task. We can create another couple of `if` statements to check if the <kbd>Home</kbd> and <kbd>End</kbd> keys are being pressed, and because we have stored the first and last tabs in variables, we can you focus them with the `focus()` method.

<pre><code class="language-javascript">// Previous code of the createKeyboardNavigation function
else if (e.key === "Home") {
  e.preventDefault();
  firstTab.focus()
} else if (e.key === "End") {
  e.preventDefault();
  lastTab.focus()
}
</code></pre>

And this is our result!

{{< codepen height="480" theme_id="light" slug_hash="YzvVXWw" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Tab demo [forked]](https://codepen.io/smashingmag/pen/YzvVXWw) by <a href="https://codepen.io/ItsCrisDiaz">Cristian Diaz</a>.{{< /codepen >}}

With this code, we have made this component accessible for keyboard and screen reader users. This shows how useful the basic concepts of `keydown` event listener, the `focus()` method, and the changes we can make with `setAttribute` are to manipulate complex components. Let’s check one more, a very complicated one, and how the `inert` attribute can help us to handle this task easily.

{{% ad-panel-leaderboard %}}

### Modals

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a14900a6-6b2a-4bce-adc4-891ceac1928e/3-guide-keyboard-accessibility-html-css-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a14900a6-6b2a-4bce-adc4-891ceac1928e/3-guide-keyboard-accessibility-html-css-part2.png" width="800" height="370" sizes="100vw" caption="Carbon Design System modal. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a14900a6-6b2a-4bce-adc4-891ceac1928e/3-guide-keyboard-accessibility-html-css-part2.png'>Large preview</a>)" alt="An opened modal with some filler text and two buttons that say Cancel and Save" >}}

#### Opening And Closing The Modal

Modals are quite a complex pattern when we talk about keyboard accessibility, so let’s start with an easy task &mdash; opening and closing the modal.

It is indeed easy, but you need to keep something in mind: it’s very likely the button opens the modal, and the modal is far away in the DOM. So you need to manage the focus programmatically when you manage this component. There is a little catch here: you need to store which element opened the modal so we can return the keyboard focus returns to this element at the moment we close it.

Luckily, there is an easy way to do that, but let’s start by creating the markup of our site:

<pre><code class="language-html">&lt;body&gt;
  &lt;header&gt;
    &lt;!-- Header's content --&gt;
  &lt;/header&gt;
  &lt;main&gt;
    &lt;!-- Main's content --&gt;
    &lt;button id="openModal"&gt;Open modal&lt;/button&gt;
  &lt;/main&gt;
  &lt;footer&gt;
    &lt;!-- Footer's content --&gt;
  &lt;/footer&gt;
  &lt;div role="dialog"
    aria-modal="true"
    aria-labelledby="modal-title"
    hidden
    tabindex="-1"&gt;
    &lt;div class="dialog&#95;&#95;overlay"&gt;&lt;/div&gt;
    &lt;div class="dialog&#95;&#95;content"&gt;
      &lt;h2 id="modal-title"&gt;Modal content&lt;/h2&gt;
      &lt;ul&gt;
        &lt;li&gt;&lt;a href="#"&gt;Modal link 1&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href="#"&gt;Modal link 2&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href="#"&gt;Modal link 3&lt;/a&gt;&lt;/li&gt;
      &lt;/ul&gt;
      &lt;button id="closeModal"&gt;Close modal&lt;/button&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/body&gt;
</code></pre>

As I mentioned, the modal and the button are far away from each other in the DOM. This will make it easier to create a focus trap later, but for now, let’s check the modal’s semantics:

- `role="dialog"` will give the element the required semantics for screen readers. It needs to have a label to be recognized as a dialog window, so we’ll use the modal’s title as the label using the attribute `aria-labelledby`.
- `aria-modal="true"` helps to make a screen reader user can only read the content of the element’s children, so it blocks access from screen readers. However, as you can see on [the `aria-modal` page for a11ysupport.com](https://a11ysupport.io/tech/aria/aria-modal_attribute), it’s not fully supported, so you can’t rely just on that for this task. It’ll be useful for screen readers who support it, but you’ll see there is another way to ensure screen reader users don’t interact with anything besides the modal once it’s opened.
- As I mentioned, we need to bring the keyboard focus to our modal, so this is why we added the attribute `tabindex="-1"`.

With that in mind, we need to create the function to open our modal. We need to check which was the element that opened it, and for that, we can use the property `document.activeElement` to check which element is being keyboard-focused right now and store it in a variable. This is my approach for this task:

<pre><code class="language-javascript">let focusedElementBeforeModal

const modal = document.querySelector("[role='dialog']");
const modalOpenButton = document.querySelector("#openModal")
const modalCloseButton = document.querySelector("#closeModal")

const openModal = () =&gt; {
  focusedElementBeforeModal = document.activeElement
  
  modal.hidden = false;
  modal.focus();
};
</code></pre>

It’s very simple: 

1. We store the button that opened the modal;
2. Then we show it by removing the attribute `hidden`;
3. Then we bring the focus to the modal with the `focus()` method.

It’s essential that you store the button **before** bringing the focus to the modal. Otherwise, the element that would be stored in this case would be the modal itself, and you don’t want that.

Now, we need to create the function to close the modal:

<pre><code class="language-javascript">const closeModal = () =&gt; {
  modal.hidden = true;
  focusedElementBeforeModal.focus()
}
</code></pre>

This is why it’s important to store the proper element. When we close the modal, we’ll bring back the keyboard focus to the element that opened it. With those functions created, all we have to do is add the event listeners for those functions! Remember that we also need to make the modal closes when you press the <kbd>Esc</kbd> key.

<pre><code class="language-javascript">modalOpenButton.addEventListener("click", () =&gt; openModal())
modalCloseButton.addEventListener("click", () =&gt; closeModal())
modal.addEventListener("keydown", (e) =&gt; {
  if (e.key === "Escape") {
    closeModal()
  }
})
</code></pre>

Right now, it looks very simple. But if that were all, modals wouldn’t be considered a complex pattern for accessibility, were they? This is where we need to create a very key task for this component, and we have two ways to do it.

#### Creating A Focus Trap

A **focus trap** ensures the keyboard focus can’t escape from the component. This is crucial because if a keyboard user can interact with anything outside a modal once it’s opened, it can create a very confusing experience. We have two ways to do that right now.

One of them is checking each element that can be tabbable with a keyboard, then storing which are the first and the last, and doing this:

- When the user presses <kbd>Shift</kbd> + <kbd>Tab</kbd> and the keyboard focus is on the first tabbable element (remember, you can check that with `document.activeElement`), the focus will go to the last tabbable element.
- When the user presses <kbd>Tab</kbd>, and the keyboard focus is on the last tabbable element, the keyboard focus should go to the first tabbable element.

Normally, I’d show you how to make this code, but I think [A11y solutions](https://a11y-solutions.stevenwoodson.com/solutions/focus/modals/) made a very good script to create a focus trap. It sort of works as the keyboard navigation with the arrow keys we created for tab elements (as I mentioned before, patterns repeat themselves!), so I invite you to check this page.

I don’t want to use this approach as the main solution because it’s not exactly flawless. Those are some situations this approach doesn’t cover.

The first one is that **it doesn’t take into account screen readers**, *especially* mobile screen readers. As Rahul Kumar mentions in his article “[Focus Trapping for Accessibility (A11Y)](https://medium.com/@im_rahul/focus-trapping-looping-b3ee658e5177)”, Talkback and Voiceover allow the user of gestures and double taps to navigate to the next or previous focusable element, and those gestures **can’t** be detected with an event listener because those gestures are something that technically speaking doesn’t happen in the browser. There is a solution for that, but I’ll put a pin on that topic for a moment.

The other concern is that this focus trap approach can lead to weird behaviors if you use certain combinations of tabbable elements. Take, for example, this modal:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e45e9748-fa92-4e72-9bfa-b6470311baea/4-guide-keyboard-accessibility-html-css-part2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e45e9748-fa92-4e72-9bfa-b6470311baea/4-guide-keyboard-accessibility-html-css-part2.png" width="800" height="374" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e45e9748-fa92-4e72-9bfa-b6470311baea/4-guide-keyboard-accessibility-html-css-part2.png'>Large preview</a>)" alt="A modal with the title 'Survey' and a question that says 'How big is your team?' and three answer options in radio inputs: 1 to 3 people, 4 to 10 people and more than 10 people, Below it, there is a button with the name 'Send answer'" >}}

Technically speaking, the first tabbable element is the first `input`. However, all the inputs in this example should focus on the last tabbable element (in this case, the `button` element) when the user presses the keys <kbd>Shift</kbd> + <kbd>Tab</kbd>. Otherwise, it could cause a weird behavior if the user presses those keys when the keyboard focus is on the second or third `input`.

If we want to create a more reliable solution, the best approach is using the `inert` attribute to make outer content inaccessible for screen readers and keyboard users, ensuring they can interact only with the modal’s content. Remember, this will require the `inert` polyfill to add more robustness to this technique.

**Note**: *It’s important to note that despite the fact a focus trap and using `inert` in practice help to ensure keyboard accessibility for modals, they don’t work exactly the same. The main difference is that setting all documents but modal as `inert`, it’ll* ***still*** *let you move outside of the website and interact with the browser’s elements. This is arguably better for security concerns but deciding if you want to create a focus trap manually or use the `inert` attribute is up to you.*

What we’ll do first is select all areas that don’t have the role `dialog.` As `inert` will remove all keyboard and screen reader interaction with the elements **and their children**, we’ll need to select only the direct children of `body.` This is why we let the modal container exist at the same level as tags like `main`, `header`, or `footer`.

<div class="break-out">

<pre><code class="language-javascript">// This selector works well for this specific HTML structure. Adapt according to your project.
const nonModalAreas = document.querySelectorAll("body &gt; &#42;:not([role='dialog'])")
</code></pre>
</div>

Now we need to come back to the `openModal` function. After opening the modal, we need to add the attribute `inert` to those elements. This should be the last step in the function:

<pre><code class="language-javascript">const openModal = () =&gt; {
  // Previously added code
  nonModalAreas.forEach((element) =&gt; {
    element.inert = true
  })
};
</code></pre>

What about when you close the modal? You need to go to the `closeModal` function and remove this attribute. This needs to go **before** everything else in the code runs. Otherwise, the browser won’t be able to focus on the button that opened this modal.

<pre><code class="language-javascript">const closeModal = () =&gt; {
  nonModalAreas.forEach((element) =&gt; {
    element.inert = false;
  });
// Previously added code
};
</code></pre>

And this is our result!

{{< codepen height="480" theme_id="light" slug_hash="NWzjqYM" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Modal test [forked]](https://codepen.io/smashingmag/pen/NWzjqYM) by <a href="https://codepen.io/ItsCrisDiaz">Cristian Diaz</a>.{{< /codepen >}}

Let’s suppose you don’t feel comfortable using the `inert` attribute right now and want to create a focus trap manually, as the one A11y Solutions shows. What can you do to ensure screen reader users can’t get out of the modal? `aria-modal` can help with that, but remember, the support for this property is quite shaky, especially for Talkback and VoiceOver for iOS. So the next best thing we can do is add the attribute `aria-hidden="true"` to all elements that are not the modal. It’s a very similar process to the one we made for the `inert` attribute, and you can use the same elements in the array we used for this topic as well!

<pre><code class="language-javascript">const openModal = () =&gt; {
  //Previously added code
  nonModalAreas.forEach((element) =&gt; {
    element.setAttribute("aria-hidden", "true")
  });
};

const closeModal = () =&gt; {
  nonModalAreas.forEach((element) =&gt; {
    element.removeAttribute("aria-hidden")
  });
  // Previously added code
};
</code></pre>

So, whether you decide to use the `inert` attribute or create a focus trap manually, you can ensure user experience for keyboard and screen reader users works at its best.

#### `<dialog>` Element

You might notice the markup I used and that I didn’t use the relatively new `<dialog>` element, and there is a reason for that. Yes, this element helps a lot by managing focus to the modal and to the button that opened easily, but, as Scott O’Hara points out in his article “[Having an open dialog](https://www.scottohara.me/blog/2019/03/05/open-dialog.html)”, it still has some accessibility issues that **even with a polyfill** are not fully solved yet. So I decided to use a more robust approach there with the markup.

If you haven’t heard about this element, it has a couple of functions to open and close the dialog, as well as some new functionalities that will be handy when we create modals. If you want to check how it works, you can check [Kevin Powell’s video about this element](https://youtu.be/TAB_v6yBXIE).

That doesn’t mean you shouldn’t use it at all. Accessibility’s situation about this element is improving, but keep in mind you still need to take into consideration certain details to make sure it works properly.

### Other Component Patterns

I could go on with many component patterns, but to be honest, I think it’ll start getting redundant because, as a matter of fact, those patterns are quite similar between the different kinds of components you can make. Unless you have to make something very unconventional, those patterns we have seen here should be enough!

With that said, how can you know what requirements you will need for a component? This is an answer with many nuances that this article cannot cover. There are some resources like [Scott O’Hara’s accessible components’ repository](https://github.com/scottaohara/accessible_components) or [UK government’s design system](https://design-system.service.gov.uk/), but this is a question that does not have a simple answer. The most important thing about this topic is to **always** test them with disabled users to know what flaws they can have in terms of accessibility.

{{% ad-panel-leaderboard %}}

## Wrapping Up

Keyboard accessibility can be quite hard, but it’s something you can achieve once you understand how keyboard users interact with a site and what principles you should keep in mind. Most of the time, HTML and CSS will do a great job of ensuring keyboard accessibility, but sometimes you’ll need JavaScript for more complex patterns.

It’s quite impressive what you can do for keyboard accessibility once you notice most of the time, the job is made with the same basic tools. Once you understand what you need to do, you can mix those tools to create a great user experience for keyboard users!

{{< signature "yk, il" >}}

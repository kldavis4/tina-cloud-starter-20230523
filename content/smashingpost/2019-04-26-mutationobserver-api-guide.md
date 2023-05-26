---
title: 'Getting To Know The MutationObserver API'
slug: mutationobserver-api-guide
author: louis-lazaris
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fc2c6700-89a1-420b-acdb-62ddceb66c2e/louis-lazaris-mutationobserver-api.png
date: 2019-04-26T13:30:16+02:00
summary: >-
  Monitoring for changes to the DOM is sometimes needed in complex web apps and frameworks. By means of explanations along with interactive demos, this article will show you how you can use the MutationObserver API to make observing for DOM changes relatively easy.
description: >-
  Monitoring for changes to the DOM is sometimes needed in complex web apps and frameworks. By means of explanations along with interactive demos, this article will show you how you can use the MutationObserver API to make observing for DOM changes relatively easy.
categories:
  - API
  - JavaScript
  - Apps
  - Frameworks
---
In complex web apps, DOM changes can be frequent. As a result, there are instances where your app might need to respond to a specific change to the DOM.

For some time, the accepted way to look for changes to the DOM was by means of a feature called [Mutation Events](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Mutation_events), which is [now deprecated](https://www.w3.org/TR/DOM-Level-3-Events/#interface-mutationevent). The W3C-approved replacement for Mutation Events is the [MutationObserver API](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver), which is what I’ll be discussing in detail in this article.

A number of older articles and references discuss why the old feature was replaced, so I won’t go into detail on that here (besides the fact that I wouldn’t be able to do it justice). The `MutationObserver` API has [near complete browser support](https://caniuse.com/#feat=mutationobserver), so we can use it safely in most &mdash; if not all &mdash; projects, should the need arise.

## Basic Syntax For A MutationObserver

A `MutationObserver` can be used in a number of different ways, which I’ll cover in detail in the rest of this article, but the basic syntax for a `MutationObserver` looks like this:

<pre><code class="language-javascript">let observer = new MutationObserver(callback);
    
function callback (mutations) {
  // do something here
}

observer.observe(targetNode, observerOptions);
</code></pre>

The first line creates a new `MutationObserver` using the `MutationObserver()` constructor. The argument passed into the constructor is a callback function that will be called on each DOM change that qualifies.

The way to determine what qualifies for a particular observer is by means of the final line in the above code. On that line, I’m using the `observe()` method of the `MutationObserver` to begin observing. You can compare this to something like `addEventListener()`. As soon as you attach a listener, the page will 'listen' for the specified event. Similarly, when you start observing, the page will begin 'observing' for the specified `MutationObserver`.

{{% feature-panel %}}

The `observe()` method takes two arguments: The *target*, which should be the node or node tree on which to observe for changes; and an *options* object, which is a `MutationObserverInit` object that allows you to define the configuration for the observer.

The final key basic feature of a `MutationObserver` is the `disconnect()` method. This allows you to stop observing for the specified changes, and it looks like this:

<pre><code class="language-javascript">observer.disconnect();
</code></pre>

## Options To Configure A MutationObserver

As mentioned, the `observe()` method of a `MutationObserver` requires a second argument that specifies the options to describe the `MutationObserver`. Here’s how the options object would look with all possible property/value pairs included:

<pre><code class="language-javascript">let options = {
  childList: true,
  attributes: true,
  characterData: false,
  subtree: false,
  attributeFilter: ['one', 'two'],
  attributeOldValue: false,
  characterDataOldValue: false
};
</code></pre>

When setting up the `MutationObserver` options, it’s not necessary to include all these lines. I’m including these simply for reference purposes, so you can see what options are available and what types of values they can take. As you can see, all except one are Boolean.

In order for a `MutationObserver` to work, at least one of `childList`, `attributes`, or `characterData` needs to be set to `true`, otherwise an error will be thrown. The other four properties work in conjunction with one of those three (more on this later).

So far I’ve merely glossed over the syntax to give you an overview. The best way to consider how each of these features works is by providing code examples and live demos that incorporate the different options. So that’s what I’ll do for the rest of this article.

{{% ad-panel-leaderboard %}}

## Observing Changes To Child Elements Using childList

The first and simplest `MutationObserver` you can initiate is one that looks for child nodes of a specified node (usually an element) to be added or removed. For my example, I’m going to create an unordered list in my HTML, and I want to know whenever a child node is added or removed from this list element.

The HTML for the list looks like this:

<pre><code class="language-html">&lt;ul id="myList" class="list"&gt;
  &lt;li&gt;Apples&lt;/li&gt;
  &lt;li&gt;Oranges&lt;/li&gt;
  &lt;li&gt;Bananas&lt;/li&gt;
  &lt;li class="child"&gt;Peaches&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

The JavaScript for my `MutationObserver` includes the following:

<div class="break-out">

 <pre><code class="language-javascript">let mList = document.getElementById('myList'),
options = {
  childList: true
},
observer = new MutationObserver(mCallback);

function mCallback(mutations) {
  for (let mutation of mutations) {
    if (mutation.type === 'childList') {
      console.log('Mutation Detected: A child node has been added or removed.');
    }
  }
}

observer.observe(mList, options);
</code></pre>
</div>

This is only part of the code. For brevity, I’m showing the most important sections that deal with the `MutationObserver` API itself.

Notice how I’m looping through the `mutations` argument, which is a `MutationRecord` object that has a number of different properties. In this case, I’m reading the `type` property and logging a message indicating that the browser has detected a mutation that qualifies. Also, notice how I’m passing the `mList` element (a reference to my HTML list) as the targeted element (i.e. the element on which I want to observe for changes).

- [See full interactive demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/aXVVjg?editors=0011)

Use the buttons to start and stop the `MutationObserver`. The log messages help clarify what’s happening. Comments in the code also provide some explanation.

Note a few important points here:

* The callback function (which I’ve named `mCallback`, to illustrate that you can name it whatever you want) will fire each time a successful mutation is detected and after the `observe()` method is executed.
* In my example, the only 'type' of mutation that qualifies is `childList`, so it makes sense to look for this one when looping through the MutationRecord. Looking for any other type in this instance would do nothing (the other types will be used in subsequent demos).
* Using `childList`, I can add or remove a text node from the targeted element and this too would qualify. So it doesn’t have to be an element that’s added or removed.
* In this example, only immediate child nodes will qualify. Later in the article, I’ll show you how this can apply to all child nodes, grandchildren, and so on.

## Observing For Changes To An Element’s Attributes

Another common type of mutation that you might want to track is when an attribute on a specified element changes. In the next interactive demo, I’m going to observe for changes to attributes on a paragraph element.

<pre><code class="language-javascript">let mPar = document.getElementById('myParagraph'),
  options = {
    attributes: true
  },
  observer = new MutationObserver(mCallback);

function mCallback (mutations) {
  for (let mutation of mutations) {
    if (mutation.type === 'attributes') {
      // Do something here...
    }
  }
}

observer.observe(mPar, options);
</code></pre>

- [Try out the demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/XOzaWv?editors=0011)

Again, I’ve abbreviated the code for clarity, but the important parts are:

* The `options` object is using the `attributes` property, set to `true` to tell the `MutationObserver` that I want to look for changes to the targeted element’s attributes.
* The mutation type I’m testing for in my loop is `attributes`, the only one that qualifies in this case.
* I’m also using the `attributeName` property of the `mutation` object, which allows me to find out which attribute was changed.
* When I trigger the observer, I’m passing in the paragraph element by reference, along with the options.

In this example, a button is used to toggle a class name on the targeted HTML element. The callback function in the mutation observer is triggered every time the class is added or removed.

{{% ad-panel-leaderboard %}}

## Observing For Character Data Changes

Another change you might want to look for in your app is mutations to character data; that is, changes to a specific text node. This is done by setting the `characterData` property to `true` in the `options` object. Here’s the code:

<pre><code class="language-javascript">let options = {
    characterData: true
  },
  observer = new MutationObserver(mCallback);
  
function mCallback(mutations) {
  for (let mutation of mutations) {
    if (mutation.type === 'characterData') {
      // Do something here...
    }
  }
}
</code></pre>

Notice again the `type` being looked for in the callback function is `characterData`.

- [See live demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/pGdpvq?editors=0011)

In this example, I’m looking for changes to a specific text node, which I target via `element.childNodes[0]`. This is a little hacky but it will do for this example. The text is user-editable via the `contenteditable` attribute on a paragraph element.

### Challenges When Observing For Character Data Changes

If you’ve fiddled around with `contenteditable`, then you might be aware that there are keyboard shortcuts that allow for rich text editing. For example, CTRL-B makes text bold, CTRL-I makes text italic, and so forth. This will break up the text node into multiple text nodes, so you’ll notice the `MutationObserver` will stop responding unless you edit the text that’s still considered part of the original node.

I should also point out that if you delete all the text, the `MutationObserver` will no longer trigger the callback. I’m assuming this happens because once the text node disappears, the target element is no longer in existence. To combat this, my demo stops observing when the text is removed, although things do get a little sticky when you use rich text shortcuts.

But don’t worry, later in this article, I’ll discuss a better way to use the `characterData` option without having to deal with as many of these quirks.

## Observing For Changes To Specified Attributes

Earlier I showed you how to observe for changes to attributes on a specified element. In that case, although the demo triggers a class name change, I could have changed any attribute on the specified element. But what if I want to observe changes to one or more specific attributes while ignoring the others?

I can do that using the optional `attributeFilter` property in the `option` object. Here’s an example:

<div class="break-out">

 <pre><code class="language-javascript">let options = {
      attributes: true,
      attributeFilter: ['hidden', 'contenteditable', 'data-par']
    },
    observer = new MutationObserver(mCallback);

function mCallback (mutations) {
  for (let mutation of mutations) {
    if (mutation.type === 'attributes') {
      // Do something here...
    }
  }
}
</code></pre>
</div>

As shown above, the `attributeFilter` property accepts an array of specific attributes that I want to monitor. In this example, the `MutationObserver` will trigger the callback each time one or more of the `hidden`, `contenteditable`, or `data-par` attributes is modified.

- [See live demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/pGGdVr?editors=0011)

Again I’m targeting a specific paragraph element. Notice the select drop down that chooses which attribute will be changed. The `draggable` attribute is the only one that won’t qualify since I didn’t specify that one in my options.

Notice in the code that I’m again using the `attributeName` property of the `MutationRecord` object to log which attribute was changed. And of course, as with the other demos, the `MutationObserver` won’t start monitoring for changes until the "start" button is clicked.

One other thing I should point out here is that I don’t need to set the `attributes` value to `true` in this case; it’s implied due to `attributesFilter` being set to true. That’s why my options object could look as follows, and it would work the same:

<pre><code class="language-javascript">let options = {
  attributeFilter: ['hidden', 'contenteditable', 'data-par']
}
</code></pre>

On the other hand, if I explicitly set `attributes` to `false` along with an `attributeFilter` array, it wouldn’t work because the `false` value would take precedence and the filter option would be ignored.

## Observing For Changes To Nodes And Their Sub-Tree

So far when setting up each `MutationObserver`, I’ve only been dealing with the targeted element itself and, in the case of `childList`, the element’s immediate children. But there certainly could be a case where I might want to observe for changes to one of the following:

* An element and all its child elements;
* One or more attributes on an element and on its child elements;
* All text nodes inside an element.

All of the above can be achieved using the `subtree` property of the options object.

### childList With subtree

First, let’s look for changes to an element’s child nodes, even if they’re not immediate children. I can alter my options object to look like this:

<pre><code class="language-javascript">options = {
  childList: true,
  subtree: true
}
</code></pre>

Everything else in the code is more or less the same as the previous `childList` example, along with some extra markup and buttons.

- [See live demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/PVgyLa?editors=0011)

Here there are two lists, one nested inside the other. When the `MutationObserver` is started, the callback will trigger for changes to either list. But if I were to change the `subtree` property back to `false` (the default when it’s not present), the callback would not execute when the nested list is modified.

### Attributes With subtree

Here’s another example, this time using `subtree` with `attributes` and `attributeFilter`. This allows me to observe for changes to attributes not only on the target element but also on the attributes of any child elements of the target element:

<pre><code class="language-javascript">options = {
  attributes: true,
  attributeFilter: ['hidden', 'contenteditable', 'data-par'],
  subtree: true
}
</code></pre>

- [See live demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/ywYaYv?editors=0011)

This is similar to the previous attributes demo, but this time I’ve set up two different select elements. The first one modifies attributes on the targeted paragraph element while the other one modifies attributes on a child element inside the paragraph.

Again, if you were to set the `subtree` option back to `false` (or remove it), the second toggle button would not trigger the `MutationObserver` callback. And, of course, I could omit `attributeFilter` altogether, and the `MutationObserver` would look for changes to *any* attributes in the subtree rather than the specified ones.

### characterData With subtree

Remember in the earlier `characterData` demo, there were some problems with the targeted node disappearing and then the `MutationObserver` no longer working. While there are ways to get around that, it’s easier to target an element directly rather than a text node, then use the `subtree` property to specify that I want all the character data inside that element, no matter how deeply nested it is, to trigger the `MutationObserver` callback.

My options in this case would look like this:

<pre><code class="language-javascript">options = {
  characterData: true,
  subtree: true
}
</code></pre>

- [See live demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/bZVpMZ?editors=0011)

After you start the observer, try using CTRL-B and CTRL-I to format the editable text. You’ll notice this works much more effectively than the previous `characterData` example. In this case, the broken up child nodes don’t affect the observer because we’re observing all nodes inside the targeted node, instead of a single text node.

## Recording Old Values

Often when observing for changes to the DOM, you’ll want to take note of the old values and possibly store them or use them elsewhere. This can be done using a few different properties in the `options` object.

### attributeOldValue

First, let’s try logging out the old attribute value after it’s changed. Here’s how my options will look along with my callback:

<pre><code class="language-javascript">options = {
  attributes: true,
  attributeOldValue: true
}

function mCallback (mutations) {
  for (let mutation of mutations) {
    if (mutation.type === 'attributes') {
      // Do something here...
    }
  }
}
</code></pre>

- [See live demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/wNNjrP?editors=0011)

Notice the use of the `attributeName` and `oldValue` properties of the `MutationRecord` object. Try the demo by entering different values in the text field. Notice how the log updates to reflect the previous value that was stored.

### characterDataOldValue

Similarly, here’s how my options would look if I want to log old character data:

<pre><code class="language-javascript">options = {
  characterData: true,
  subtree: true,
  characterDataOldValue: true
}
</code></pre>

- [See live demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/aXrzex?editors=0011)

Notice the log messages indicate the previous value. Things do get a little wonky when you add HTML via rich text commands to the mix. I’m not sure what the correct behavior is supposed to be in that case but it is more straightforward if the only thing inside the element is a single text node.

## Intercepting Mutations Using takeRecords()

Another method of the `MutationObserver` object that I haven’t mentioned yet is `takeRecords()`. This method allows you to more or less intercept the mutations that are detected before they are processed by the callback function.

I can use this feature using a line like this:

<pre><code class="language-javascript">let myRecords = observer.takeRecords();
</code></pre>

This stores a list of the DOM changes in the specified variable. [In my demo](https://codepen.io/impressivewebs/pen/oVNeRp?editors=0011), I’m executing this command as soon as the button that modifies the DOM is clicked. Notice that the start and add/remove buttons don’t log anything. This is because, as mentioned, I’m intercepting the DOM changes before they are processed by the callback.

Notice, however, what I’m doing in the event listener that stops the observer:

<div class="break-out">

 <pre><code class="language-javascript">btnStop.addEventListener('click', function () {
  observer.disconnect();
  if (myRecords) {
    console.log(`${myRecords[0].target} was changed using the ${myRecords[0].type} option.`);
  }
}, false);
</code></pre>
</div>

As you can see, after stopping the observer using `observer.disconnect()`, I’m accessing the mutation record that was intercepted and I’m logging the target element as well as the type of mutation that was recorded. If I had been observing for multiple types of changes then the stored record would have more than one item in it, each with its own type.

When a mutation record is intercepted in this way by calling `takeRecords()`, the queue of mutations that would normally be sent to the callback function is emptied. So if for some reason you need to intercept these records before they’re processed, `takeRecords()` would come in handy.

## Observing For Multiple Changes Using A Single Observer

Note that if I’m looking for mutations on two different nodes on the page, I can do so using the same observer. This means after I call the constructor, I can execute the `observe()` method for as many elements as I want.

Thus, after this line:

<pre><code class="language-javascript">observer = new MutationObserver(mCallback);
</code></pre>

I can then have multiple `observe()` calls with different elements as the first argument:

<pre><code class="language-javascript">observer.observe(mList, options);
observer.observe(mList2, options);
</code></pre>

- [See live demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/OqJMeG?editors=0011)

Start the observer, then try the add/remove buttons for both lists. The only catch here is that if you hit one of the "stop" buttons, the observer will stop observing for both lists, not just the one it’s targeting.

## Moving A Node Tree That’s Being Observed

One last thing I’ll point out is that a `MutationObserver` will continue to observe for changes to a specified node even after that node has been removed from its parent element.

For example, try out the following demo:

- [See live demo &nbsp;&rarr;](https://codepen.io/impressivewebs/pen/GeRWPX?editors=0011)

This is another example that uses `childList` to monitor for changes to the child elements of a target element. Notice the button that disconnects the sub-list, which is the one being observed. Click the "Start..." button, then click the "Move..." button to move the nested list. Even after the list is removed from its parent, the `MutationObserver` continues to observe for the specified changes. Not a major surprise that this happens, but it’s something to keep in mind.

## Conclusion

That covers just about all the primary features of the `MutationObserver` API. I hope this deep dive has been useful for you to get familiar with this standard. As mentioned, [browser support is strong](https://caniuse.com/#feat=mutationobserver) and you can read more about this API [on MDN’s pages](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver).

I’ve put all the demos for this article into [
a CodePen collection](https://codepen.io/collection/njwmrK/), should you want to have an easy place to mess around with the demos.

{{< signature "dm, il" >}}

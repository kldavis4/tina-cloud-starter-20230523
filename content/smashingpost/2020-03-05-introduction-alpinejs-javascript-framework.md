---
title: 'Introducing Alpine.js: A Tiny JavaScript Framework'
slug: introduction-alpinejs-javascript-framework
author: phil-smith
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7c71702-d0f7-4ecc-a369-6407f7a935d0/2-alpinejs-javascript-framework.png
date: 2020-03-05T11:30:00.000Z
summary: >-
  Ever built a website and reached for jQuery, Bootstrap, Vue.js or React to acheive some basic user interaction? Alpine.js is a fraction of the size of these frameworks because it involves no build steps and provides all of the tools you need to build a basic user interface.
description: >-
  Ever built a website and reached for jQuery, Bootstrap, Vue.js or React to acheive some basic user interaction? Alpine.js is a fraction of the size of these frameworks because it involves no build steps and provides all of the tools you need to build a basic user interface.
categories:
  - JavaScript
  - Frameworks
---

Like most developers, I have a bad tendency to over-complicate my workflow, especially if there’s some new hotness on the horizon. Why use CSS when you can use CSS-in-JS? Why use Grunt when you can use Gulp? Why use Gulp when you can use Webpack? Why use a traditional CMS when you can go headless? Every so often though, the new-hotness makes life simpler.

Recently, the rise of utility based tools like [Tailwind CSS](https://www.smashingmagazine.com/2020/02/tailwindcss-react-project/) have done this for CSS, and now Alpine.js promises something similar for JavaScript. 

In this article, we’re going to take a closer look at [Alpine.js](https://github.com/alpinejs/alpine) and how it can replace JQuery or larger JavaScript libraries to build interactive websites. If you regularly build sites that require a sprinkling on Javascript to alter the UI based on some user interaction, then this article is for you. 

Throughout the article, I refer to Vue.js, but don’t worry if you have no experience of Vue &mdash; that is not required. In fact, part of what makes Alpine.js great is that you barely need to know any JavaScript at all.

Now, let’s get started.

## What Is Alpine.js?

According to project author Caleb Porzio:

<blockquote>“Alpine.js offers you the reactive and declarative nature of big frameworks like Vue or React at a much lower cost. You get to keep your DOM, and sprinkle in behavior as you see fit.”</blockquote>

Let’s unpack that a bit.

Let’s consider a basic UI pattern like *Tabs*. Our ultimate goal is that when a user clicks on a tab, the tab contents displays. If we come from a PHP background, we could easily achieve this server side. But the page refresh on every tab click isn’t very ‘reactive’.

To create a better experience over the years, developers have reached for jQuery and/or Bootstrap. In that situation, we create an event listener on the tab, and when a user clicks, the event fires and we tell the browser what to do. 

{{< codepen height="480" theme_id="light" slug_hash="PoqKBXr" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/PoqKBXr">Showing / hiding with jQuery</a> by <a href="https://codepen.io/monkeyphil">Phil</a> on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

That works. But this style of coding where we tell the browser exactly what to do (imperative coding) quickly gets us in a mess. Imagine if we wanted to disable the button after it has been clicked, or wanted to change the background color of the page. We’d quickly get into some serious spaghetti code.

Developers have solved this issue by reaching for frameworks like Vue, Angular and React. These frameworks allow us to write cleaner code by utilizing the virtual DOM: a kind of mirror of the UI stored in the browser memory. The result is that when you ‘hide’ a DOM element (like a tab) in one of these frameworks; it doesn’t add a `display:none;` style attribute, but instead it literally disappears from the ‘real’ DOM. 

This allows us to write more declarative code that is cleaner and easier to read. But this is at a cost. Typically, the bundle size of these frameworks is large and for those coming from a jQuery background, the learning curve feels incredibly steep. Especially when all you want to do is toggle tabs! And that is where Alpine.js steps in.

{{% feature-panel %}}

Like Vue and React, Alpine.js allows us to write declarative code but it uses the “real” DOM; amending the contents and attributes of the same nodes that you and I might edit when we crack open a text editor or dev-tools. As a result, you can lose the filesize, wizardry and cognitive-load of larger framework but retain the declarative programming methodology. And you get this with no bundler, no build process and no script tag. Just load 6kb of Alpine.js and you’re away!

<table class="tablesaw break-out" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <thead>
  <tr>
  <th></th>
  <th>Alpine.js</th>
  <th>JQuery</th>
  <th>Vue.js</th>
  <th>React + React DOM</th>
  </tr>
  </thead>
  <tbody>
  <tr>
   <td>Coding style
   </td>
   <td>Declarative
   </td>
   <td>Imperative
   </td>
   <td>Declarative
   </td>
   <td>Declarative
   </td>
  </tr>
  <tr>
   <td>Requires bundler
   </td>
   <td>No
   </td>
   <td>No
   </td>
   <td>No
   </td>
   <td>Yes
   </td>
  </tr>
  <tr>
   <td>Filesize (GZipped, minified)
   </td>
   <td>6.4kb
   </td>
   <td>30kb
   </td>
   <td>32kb
   </td>
   <td>5kb + 36kb
   </td>
  </tr>
  <tr>
   <td>Dev-Tools
   </td>
   <td>No
   </td>
   <td>No
   </td>
   <td>Yes
   </td>
   <td>Yes
   </td>
  </tr>
  </tbody>
</table>

### When Should I Reach For Alpine?

For me, Alpine’s strength is in the ease of DOM manipulation. Think of those things you used out of the box with Bootstrap, Alpine.js is great for them. Examples would be:

*   Showing and hiding DOM nodes under certain conditions,
*   Binding user input,
*   Listening for events and altering the UI accordingly,
*   Appending classes.

You can also use Alpine.js for templating if your data is available in JSON, but let’s save that for another day.

### When Should I Look Elsewhere?

If you’re fetching data, or need to carry out additional functions like validation or storing data, you should probably look elsewhere. Larger frameworks also come with dev-tools which can be invaluable when building larger UIs.

{{% ad-panel-leaderboard %}}

## From jQuery To Vue To Alpine

Two years ago, Sarah Drasner posted an article on Smashing Magazine, “[Replacing jQuery With Vue.js: No Build Step Necessary](https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/),” about how Vue could replace jQuery for many projects. That article started me on a journey which led me to use Vue almost every time I build a user interface. Today, we are going to recreate some of her examples with Alpine, which should illustrate its advantages over both jQuery and Vue in certain use cases.

Alpine’s syntax is almost entirely lifted from Vue.js. In total, there are 13 directives. We’ll cover most of them in the following examples.

### Getting Started

Like Vue and jQuery, no build process is required. Unlike Vue, Alpine it initializes itself, so there’s no need to create a new instance. Just load Alpine and you’re good to go.

<div class="break-out">

 <pre><code class="language-markup">&lt;script src="https://cdn.jsdelivr.net/gh/alpinejs/alpine@v1.9.4/dist/alpine.js" defer&gt;&lt;/script&gt;
</code></pre>
</div>

The scope of any given component is declared using the `x-data` directive. This kicks things off and sets some default values if required:

<pre><code class="language-markup">&lt;div x-data="{ foo: 'bar' }"&gt;...&lt;/div&gt;
</code></pre>

### Capturing User Inputs

- [See section in Sarah Drasner’s article&nbsp;&rarr;](https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/#capturing-user-inputs)

`x-model` allow us to keep any input element in sync with the values set using `x-data`. In the following example, we set the name value to an empty string (within the `form` tag). Using `x-model`, we bind this value to the input field. By using `x-text`, we inject the value into the `innerText` of the paragraph element.

{{< codepen height="480" theme_id="light" slug_hash="WNvEKav" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/WNvEKav">Capturing user input with Alpine.js</a> by <a href="https://codepen.io/monkeyphil">Phil</a> on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

This highlights the key differences with Alpine.js and both jQuery and Vue.js.

Updating the paragraph tag in jQuery would require us to listen for specific events (keyup?), explicitly identify the node we wish to update and the changes we wish to make. Alpine’s syntax on the other hand, just specifies what should happen. This is what is meant by declarative programming.

Updating the paragraph in Vue while simple, would require a new script tag:

<pre><code class="language-javascript">new Vue({ el: '#app', data: { name: '' } });
</code></pre>

While this might not seem like the end of the world, it highlights the first major gain with Alpine. There is no context-switching. Everything is done right there in the HTML &mdash; no need for any additional JavaScript.

### Click Events, Boolean Attributes And Toggling Classes

- [See section in Sarah Drasner’s article&nbsp;&rarr;](https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/#toggling-classes)

Like with Vue, `:` serves as a shorthand for `x-bind` (which binds attributes) and `@` is shorthand for `x-on` (which indicates that Alpine should listen for events).

In the following example, we instantiate a new component using `x-data`, and set the default value of `show` to be false. When the button is clicked, we toggle the value of `show`. When this value is true, we instruct Alpine to append the `aria-expanded` attribute.

`x-bind` works differently for classes: we pass in object where the key is the class-name (`active` in our case) and the value is a boolean expression (`show`).

{{< codepen height="480" theme_id="light" slug_hash="QWbMBJj" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/QWbMBJj">Click Events, Boolean Attributes and Toggling Classes with Alpine.js</a> by <a href="https://codepen.io/monkeyphil">Phil</a> on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

### Hiding And Showing

- [See section in Sarah Drasner’s article&nbsp;&rarr;](https://www.smashingmagazine.com/2018/02/jquery-vue-javascript/#hiding-and-showing)

The syntax showing and hiding is almost identical to Vue.

{{< codepen height="480" theme_id="light" slug_hash="LYVjBXm" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/LYVjBXm">Showing / hiding with Alpine.js</a> by <a href="https://codepen.io/monkeyphil">Phil</a> on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

This will set a given DOM node to `display:none`. If you need to remove a DOM element completely, `x-if` can be used. However, because Alpine.js doesn’t use the Virtual DOM, `x-if` can only be used on a `<template></template>` (tag that wraps the element you wish to hide).

{{% ad-panel-leaderboard %}}

## Magic Properties

In addition to the above directives, three *Magic Properties* provide some additional functionality. All of these will be familiar to anyone working in Vue.js.

*   `$el` fetches the root component (the thing with the x-data attribute);
*   `$refs` allows you to grab a DOM element;
*   `$nextTick` ensures expressions are only executed once Alpine has done its thing;
*   `$event` can be used to capture a nature browser event.

{{< codepen height="480" theme_id="light" slug_hash="bGdrjOG" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/bGdrjOG">Magic Properties</a> by <a href="https://codepen.io/monkeyphil">Phil</a> on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Let’s Build Something Useful

It’s time to build something for the real world. In the interests of brevity I’m going to use Bootstrap for styles, but use Alpine.js for all the JavaScript. The page we’re building is a simple landing page with a contact form displayed inside a modal that submits to some form handler and displays a nice success message. Just the sort of thing a client might ask for and expect *pronto!*

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a6eca3e-7f93-438f-8702-df2cc406773a/3-alpinejs-javascript-framework.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a6eca3e-7f93-438f-8702-df2cc406773a/3-alpinejs-javascript-framework.png" sizes="100vw" caption="Initial view (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6a6eca3e-7f93-438f-8702-df2cc406773a/3-alpinejs-javascript-framework.png'>Large preview</a>)" alt="Initial view of the demo app" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7c71702-d0f7-4ecc-a369-6407f7a935d0/2-alpinejs-javascript-framework.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7c71702-d0f7-4ecc-a369-6407f7a935d0/2-alpinejs-javascript-framework.png" sizes="100vw" caption="Modal open (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7c71702-d0f7-4ecc-a369-6407f7a935d0/2-alpinejs-javascript-framework.png'>Large preview</a>)" alt="View of the demo app with modal open" >}}

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c0bd665-5074-45b0-828f-2a1ed83b7687/1-alpinejs-javascript-framework.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c0bd665-5074-45b0-828f-2a1ed83b7687/1-alpinejs-javascript-framework.png" sizes="100vw" caption="Success message (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c0bd665-5074-45b0-828f-2a1ed83b7687/1-alpinejs-javascript-framework.png'>Large preview</a>)" alt="View of the demo app with success message displaying" >}}

**Note**: *You can view the original markup [here](https://github.com/philyboysmith/alpine-demo/blob/master/demo.html).*

To make this work, we could add jQuery and Bootstrap.js, but that is quite a bit of overhead for not a lot of functionality. We could probably write it in Vanilla JS, but who wants to do that? Let’s make it work with Alpine.js instead.

First, let’s set a scope and some initial values:

<div class="break-out">

 <pre><code class="language-markup">&lt;body class="text-center text-white bg-dark h-100 d-flex flex-column" x-data="{ showModal: false, name: '', email: '', success: false }"&gt;
</code></pre>
</div>

Now, let’s make our button set the `showModal` value to true:

<div class="break-out">

 <pre><code class="language-markup">&lt;button class="btn btn-lg btn-secondary" @click="showModal = true" &gt;Get in touch&lt;/button&gt;
 </code></pre>
</div>

When `showModal` is true, we need to display the modal and add some classes:

<div class="break-out">

 <pre><code class="language-markup">&lt;div class="modal  fade text-dark" :class="{ 'show d-block': showModal }" x-show="showModal" role="dialog"&gt;
 </code></pre>
</div>

Let’s bind the input values to Alpine:

<div class="break-out">

 <pre><code class="language-markup">&lt;input type="text" class="form-control" name="name" x-model="name" &gt;
&lt;input type="email" class="form-control" name="email" x-model="email" &gt;
 </code></pre>
</div>

And disable the ‘Submit’ button, until those values are set:

<div class="break-out">

 <pre><code class="language-markup">&lt;button type="button" class="btn btn-primary" :disabled="!name || !email"&gt;Submit&lt;/button&gt;</code></pre>
</div>

Finally, let’s send data to some kind of asynchronous function, and hide the modal when we’re done:

<div class="break-out">

 <pre><code class="language-markup">&lt;button type="button" class="btn btn-primary" :disabled="!name || !email" @click="submitForm({name: name, email: email}).then(() => {showModal = false; success= true;})"&gt;Submit&lt;/button&gt;
 </code></pre>
</div>

And that’s about it! 

{{< codepen height="480" theme_id="light" slug_hash="vYOJaMb" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen <a href="https://codepen.io/smashingmag/pen/vYOJaMb">Something useful built with Alpine.js</a> by <a href="https://codepen.io/monkeyphil">Phil</a> on <a href="https://codepen.io">CodePen</a>.{{< /codepen >}}

## Just Enough JavaScript

When building websites, I’m increasingly trying to ask myself what would be “just enough JavaScript”? When building a sophisticated web application, that might well be React. But when building a marketing site, or something similar, Alpine.js feels like enough. (And even if it’s not, given the similar syntax, switching to Vue.js takes no time at all).

It’s incredibly easy to use (especially if you’ve never used VueJS). It’s tiny (&lt; 6kb gzipped). And it means no more context switching between HTML and JavaScript files.

There are more advanced features that aren’t included in this article and Caleb is constantly adding new features. If you want to find out more, take a look at [the official docs on Github](https://github.com/alpinejs/alpine).

{{< signature "ra, il" >}}

---
title: Writing A Better JavaScript Library For The DOM
slug: writing-a-better-javascript-library-for-the-dom
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/468939fa-073b-43f3-b0e8-783cf83b936e/illu-jquery.jpg'
date: 2014-01-13T10:27:32.000Z
author: maksim-chemerisuk
description: >-
  At present, jQuery is the _de facto_ library for working with the document
  object model (DOM). It can be used with popular client-side MV* frameworks
  (such as Backbone), and it has a ton of plugins and a very large community.
categories:
  - Coding
  - CSS
  - JavaScript
  - jQuery
---
At present, jQuery is the <em>de facto</em> library for working with the document object model (DOM). It can be used with popular client-side MV* frameworks (such as Backbone), and it has a ton of plugins and a very large community. As developers’ interest in JavaScript increases by the minute, a lot of people are becoming curious about <strong>how native APIs really work</strong> and about when we can just use them instead of including an extra library.

Lately, I have started to see more and more problems with jQuery, at least my use of it. Most of the problems are with jQuery’s core and can’t be fixed without breaking backwards compatibility — which is very important. I, like many others, continued using the library for a while, navigating all of the pesky quirks every day.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Introducing Live Extensions For Better-DOM](https://www.smashingmagazine.com/2014/02/introducing-live-extensions-better-dom-javascript/)
*   [Browser Input Events: Can We Do Better Than The Click?](https://www.smashingmagazine.com/2015/03/better-browser-input-events/)
*   [Analyzing Network Characteristics Using JavaScript And The DOM](https://www.smashingmagazine.com/2011/11/analyzing-network-characteristics-using-javascript-and-the-dom-part-1/)

Then, <a title="Daniel Buchner" href="https://twitter.com/csuwildcat">Daniel Buchner</a> created <a title="SelectorListener" href="https://github.com/csuwildcat/SelectorListener">SelectorListener</a>, and <strong>the idea of “live extensions”</strong> manifested. I started to think about creating a set of functions that would enable us to build unobtrusive DOM components using a better approach than what we have used so far. The objective was to review existing APIs and solutions and to build a clearer, testable and lightweight library.

{{% feature-panel %}}

## Adding Useful Features To The Library

The idea of live extensions encouraged me to develop the <a title="the better-dom project" href="https://github.com/chemerisuk/better-dom">better-dom project</a>, although other interesting features make the library unique. Let’s review them quickly:

*   live extensions
*   native animations
*   embedded microtemplating
*   internationalization support

### Live Extensions

jQuery has a concept called “live events.” Drawing on the idea of event delegation, it enables developers to handle existing and future elements. But more flexibility is required in a lot of cases. For example, delegated events fall short when the DOM needs to be mutated in order to initialize a widget. Hence, live extensions.

<strong>The goal is to define an extension once</strong> and have any future elements run through the initialization function, regardless of the widget’s complexity. This is important because it enables us to write Web pages declaratively; so, it works great with AJAX applications.

<a><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/623078f2-f829-46b7-8448-03d5d4dcb011/new-feature-with-jquery.jpg" alt="Live extensions make is easier to handle any future elements." width="500" height="293" /></a><br>
<em>Live extensions enable you to handle any future elements without the need to invoke the initialization function. (<a href="https://www.flickr.com/photos/peterhellberg/3777750788/">Image credits</a>)</em>

Let’s look at a simple example. Let’s say <strong>our task is to implement a fully customizable tooltip.</strong> The <code>:hover</code> pseudo-selector won’t help us here because the position of the tooltip changes with the mouse cursor. Event delegation doesn’t fit well either; listening to <code>mouseover</code> and <code>mouseleave</code> for all elements in the document tree is very expensive. Live extensions to the rescue!

<pre><code class="language-javascript">
DOM.extend("[title]", {
  constructor: function() {
    var tooltip = DOM.create("span.custom-title");

    // set the title's textContent and hide it initially
    tooltip.set("textContent", this.get("title")).hide();

    this
      // remove legacy title
      .set("title", null)
      // store reference for quicker access
      .data("tooltip", tooltip)
      // register event handlers
      .on("mouseenter", this.onMouseEnter, ["clientX", "clientY"])
      .on("mouseleave", this.onMouseLeave)
      // insert the title element into DOM
      .append(tooltip);
  },
  onMouseEnter: function(x, y) {
    this.data("tooltip").style({left: x, top: y}).show();
  },
  onMouseLeave: function() {
    this.data("tooltip").hide();
  }
});
</code></pre>

We can style the <code>.custom-title</code> element in CSS:

<pre><code class="language-css">
.custom-title {
  position: fixed; /* required */
  border: 1px solid #faebcc;
  background: #faf8f0;
}
</code></pre>

The most interesting part happens when you insert a new element with a <code>title</code> attribute in the page. The custom tooltip will work <strong>without any initialization</strong> call.

Live extensions are self-contained; thus, they don’t require you to invoke an initialization function in order to work with future content. So, they can be combined with any DOM library and will simplify your application logic by separating the UI code into many small independent pieces.

Last but not least, a few words on <a title="Web Components" href="https://www.w3.org/TR/components-intro/">Web components</a>. A section of the specification, “<a title="Decorators" href="https://www.w3.org/TR/components-intro/#decorator-section">Decorators</a>,” aims to solve a similar problem. Currently, it uses a markup-based implementation with a special syntax for attaching event listeners to child elements. But it’s still an early draft:
<blockquote>"Decorators, unlike other parts of Web Components, do not have a specification yet."</blockquote>

### Native Animations

<a title="Thanks to Apple" href="https://www.apple.com/html5/showcase/transitions/">Thanks to Apple</a>, CSS has <a title="good animation support in CSS" href="https://caniuse.com/#search=animation">good animation support</a> now. In the past, animations were usually implemented in JavaScript via <code>setInterval</code> and <code>setTimeout</code>. It was a cool feature — but now it's more like a bad practice. Native animations will always be smoother: They are usually faster, take less energy and degrade well if not supported by the browser.

In better-dom, there is no <code>animate</code> method: just <code>show</code>, <code>hide</code> and <code>toggle</code>. To capture a hidden element state in CSS, the library uses the standards-based <code>aria-hidden</code> attribute.

To illustrate how it works, <strong>let’s add a simple animation effect</strong> to the custom tooltip that we introduced earlier:

<pre><code class="language-css">
.custom-title {
  position: fixed; /* required */
  border: 1px solid #faebcc;
  background: #faf8f0;
  /* animation code */
  opacity: 1;
  -webkit-transition: opacity 0.5s;
  transition: opacity 0.5s;
}

.custom-title[aria-hidden=true] {
  opacity: 0;
}
</code></pre>

Internally, <code>show()</code> and <code>hide()</code> set the <code>aria-hidden</code> attribute value to be <code>false</code> and <code>true</code>. It enables the CSS to handle the animations and transitions.

You can see a demo with <a title="more animation examples using better-dom" href="https://jsfiddle.net/C3WeM/5/">more animation examples that use better-dom</a>.</p>

### Embedded Microtemplating

HTML strings are annoyingly verbose. Looking for a replacement, I found the excellent <a title="emmet project" href="https://www.smashingmagazine.com/2013/03/26/goodbye-zen-coding-hello-emmet/">Emmet</a>. Today, Emmet is quite a popular plugin for text editors, and it has a nice and compact syntax. Take this HTML:

<pre><code class="language-javascript">
body.append("&lt;ul&gt;&lt;li class='list-item'&gt;&lt;/li&gt;&lt;li class='list-item'&gt;&lt;/li&gt;&lt;li class='list-item'&gt;&lt;/li&gt;&lt;/ul&gt;");
</code></pre>

And compare it to the equivalent microtemplate:

<pre><code class="language-javascript">
body.append("ul&gt;li.list-item*3");
</code></pre>

In better-dom, any method that accepts HTML may use Emmet expressions as well. The <a title="The abbreviation parser is fast" href="https://web.archive.org/web/20140622060746/https://jsperf.com:80/dom-create-vs-jquery/18">abbreviation parser is fast</a>, so no need to worry about a performance penalty. A template <a title="precompilation function" href="https://github.com/chemerisuk/better-dom/wiki/Microtemplating#where-to-use">precompilation function</a> also exists to be used on demand.</p>

### Internationalization Support

Developing a UI widget often requires localization — not an easy task. Over the years, many have tackled this in different ways. With better-dom, I believe that <strong>changing the state of a CSS selector is like switching languages</strong>.

Conceptually speaking, switching a language is like changing the “representation” of content. In CSS2, several pseudo-selectors help to describe such a model: <code>:lang</code> and <code>:before</code>. Take the code below:

<pre><code class="language-css">
[data-i18n="hello"]:before {
  content: "Hello Maksim!";
}

[data-i18n="hello"]:lang(ru):before {
  content: "Привет Максим!";
}
</code></pre>

The trick is simple: The value of the <code>content</code> property changes according to the current language, which is determined by the <code>lang</code> attribute of the <code>html</code> element. By using data attributes such as <code>data-i18n</code>, we can maintain the textual content in HTML:

<pre><code class="language-css">
[data-i18n]:before {
  content: attr(data-i18n);
}

[data-i18n="Hello Maksim!"]:lang(ru):before {
  content: "Привет Максим!";
}
</code></pre>

Of course, such CSS isn’t exactly attractive, so better-dom has two helpers: <code>i18n</code> and <code>DOM.importStrings</code>. The first is used to update the <code>data-i18n</code> attribute with the appropriate value, and the second localizes strings for a particular language.

<pre><code class="language-javascript">
label.i18n("Hello Maksim!");
// the label displays "Hello Maksim!"
DOM.importStrings("ru",  "Hello Maksim!", "Привет Максим!");
// now if the page is set to ru language,
// the label will display "Привет Максим!"
label.set("lang", "ru");
// now the label will display "Привет Максим!"
// despite the web page's language
</code></pre>

Parameterized strings can be used as well. Just add <code>${param}</code> variables to a key string:

<pre><code class="language-javascript">
label.i18n("Hello ${user}!", {user: "Maksim"});
// the label will display "Hello Maksim!"
</code></pre>

## Making Native APIs More Elegant

Generally, we want to stick to standards. But sometimes the standards aren’t exactly user-friendly. <strong>The DOM is a total mess</strong>, and to make it bearable, we have to wrap it in a convenient API. Despite all of the improvements made by open-source libraries, some parts could still be done better:

*   getter and setter,
*   event handling,
*   functional methods support.</p>

### Getter and Setter

The native DOM has the <strong>concept of attributes and properties of elements</strong> that could behave differently. Assume we have the markup below on a Web page:

<pre><code class="language-markup">
&lt;a href="/chemerisuk/better-dom" id="foo" data-test="test"&gt;better-dom&lt;/a&gt;
</code></pre>

To explain why “the DOM is a total mess,” let’s look at this:

<pre><code class="language-javascript">
var link = document.getElementById("foo");

link.href; // =&gt; "https://github.com/chemerisuk/better-dom"
link.getAttribute("href"); // =&gt; "/chemerisuk/better-dom"
link["data-test"]; // =&gt; undefined
link.getAttribute("data-test"); // =&gt; "test"

link.href = "abc";
link.href; // =&gt; "https://github.com/abc"
link.getAttribute("href"); // =&gt; "abc"
</code></pre>

An attribute value is equal to the appropriate string in HTML, while the element property with the same name could have some special behavior, such as generating the fully qualified URL in the listing above. These differences can be confusing.

In practice, it’s hard to imagine a practical situation in which such a distinction would be useful. Moreover, the developer should always keep in mind which value (attribute or property) is being used that introduces unnecessary complexity.

In better-dom, things are clearer. <strong>Every element has only smart getters and setters.</strong>

<pre><code class="language-javascript">
var link = DOM.find("#foo");

link.get("href"); // =&gt; "https://github.com/chemerisuk/better-dom"
link.set("href", "abc");
link.get("href"); // =&gt; "https://github.com/abc"
link.get("data-attr"); // =&gt; "test"
</code></pre>

In the first step, it does a property lookup, and if it’s defined, then it’s used for manipulation. Otherwise, getter and setter work with the appropriate attribute of the element. For booleans (checked, selected, etc.), you could just use <code>true</code> or <code>false</code> to update the value: Changing such a property on an element would trigger the appropriate attribute (native behavior) to be updated.</p>

### Improved Event Handling

Event handling is a big part of the DOM, however, I've discovered one fundamental problem: Having an event object in element listeners forces a developer who cares about testability to mock the first argument, or to create an extra function that passes only event properties used in the handler.

<pre><code class="language-javascript">
var button = document.getElementById("foo");

button.addEventListener("click", function(e) {
  handleButtonClick(e.button);
}, false);
</code></pre>

This is really annoying. What if we extracted the changing part as an argument? This would allow us to get rid of the extra function:

<pre><code class="language-javascript">
var button = DOM.find("#foo");

button.on("click", handleButtonClick, ["button"]);
</code></pre>

By default, the event handler passes the <code>["target", "defaultPrevented"]</code> array, so no need to add the last argument to get access to these properties:

<pre><code class="language-javascript">
button.on("click", function(target, canceled) {
  // handle button click here
});
</code></pre>

<strong>Late binding is supported as well</strong> (I’d recommend reading Peter Michaux’s review of the topic). It’s a more flexible alternative to the regular event handlers that <a title="exists in the W3C standard" href="https://www.w3.org/TR/DOM-Level-2-Events/events.html#Events-EventListener-handleEvent">exist in the W3C’s standard</a>. It could be useful when you need frequent <code>on</code> and <code>off</code> method calls.

<pre><code class="language-javascript">
button._handleButtonClick = function() { alert("click!"); };

button.on("click", "_handleButtonClick");
button.fire("click"); // shows "clicked" message
button._handleButtonClick = null;
button.fire("click"); // shows nothing
</code></pre>

Last but not least, better-dom has none of the shortcuts that exist in legacy APIs and that behave inconsistently across browsers, like <code>click()</code>, <code>focus()</code> and <code>submit()</code>. The only way to call them is to use the <code>fire</code> method, which executes the default action when no listener has returned <code>false</code>:

<pre><code class="language-javascript">
link.fire("click"); // clicks on the link
link.on("click", function() { return false; });
link.fire("click"); // triggers the handler above but doesn't do a click
</code></pre>

### Functional Methods Support

ES5 standardized a couple of useful methods for arrays, including <code>map</code>, <code>filter</code> and <code>some</code>. They allow us to use common collection operations in a standards-based way. As a result, today we have projects like <a title="underscore" href="https://underscorejs.org/">Underscore</a> and <a title="lodash" href="https://lodash.com/">Lo-Dash</a>, which polyfill these methods for old browsers.

Each element (or collection) in better-dom has the methods below built in:

*   `each` (which differs from `forEach` by returning `this` instead of `undefined`)
*   `some`
*   `every`
*   `map`
*   `filter`
*   `reduce[Right]`

<pre><code class="language-javascript">
var urls, activeLi, linkText; 

urls = menu.findAll("a").map(function(el) {
  return el.get("href");
});
activeLi = menu.children().filter(function(el) {
  return el.hasClass("active");
});
linkText = menu.children().reduce(function(memo, el) {
  return memo || el.hasClass("active") &amp;&amp; el.find("a").get()
}, false);
</code></pre>

## Avoiding jQuery Problems

Most of the following issues can’t be fixed in jQuery without breaking backwards compatibility. That’s why creating a new library seemed like the logical way out.

*   the “magical” `$` function
*   the value of the `[]` operator
*   issues with `return false`
*   `find` and `findAll`

### The “Magical” $ Function

Everyone has heard at some point that the <code>$</code> (dollar) function is kind of like magic. A single-character name is not very descriptive, so it looks like a built-in language operator. That’s why inexperienced developers call it inline everywhere.

Behind the scenes, <strong>the dollar is quite a complex function</strong>. Executing it too often, especially in frequent events such as <code>mousemove</code> and <code>scroll</code>, could cause poor UI performance.

Despite so many articles recommending jQuery objects to be cached, developers continue to insert the dollar function inline, because the library’s syntax encourages them to use this coding style.

Another issue with the dollar function is that it allows us to do two completely different things. People have gotten used to such a syntax, but it’s a bad practice of a function design in general:

<pre><code class="language-javascript">
$("a"); // =&gt; searches all elements that match “a” selector
$("&lt;a&gt;"); // =&gt; creates a &lt;a&gt; element with jQuery wrapper
</code></pre>

<strong>In better-dom, several methods cover the responsibilities of the dollar function</strong> in jQuery: <code>find[All]</code> and <code>DOM.create</code>. <code>find[All]</code> is used to search element(s) according to the CSS selector. <code>DOM.create</code> makes a new elements tree in memory. Their names make it very clear what they are responsible for.</p>

### Value of the [] Operator

Another reason for the problem of frequent dollar function calls is the brackets operator. When a new jQuery object is created, all associated nodes are stored in numeric properties. But note that the value of such a property contains a native element instance (not a jQuery wrapper):

<pre><code class="language-javascript">
var links = $("a");

links[0].on("click", function() { ... }); // throws an error
$(links[0]).on("click", function() { ... }); // works fine
</code></pre>

Because of such a feature, every functional method in jQuery or another library (like Underscore) requires the current element to be wrapped with <code>$()</code> inside of a callback function. Therefore, developers must always keep in mind the type of object they are working with — a native element or a wrapper — despite the fact that they are using a library to work with the DOM.

In better-dom, the brackets operator returns a library’s object, so developers can forget about native elements. There is only one acceptable way to access them: by using a special <code>legacy</code> method.

<pre><code class="language-javascript">
var foo = DOM.find("#foo");

foo.legacy(function(node) {
  // use Hammer library to bind a swipe listener
  Hammer(node).on("swipe", function(e) {
    // handle swipe gesture here
  }); 
});
</code></pre>

In reality, this method is required in very rare cases, such as to be compatible with a native function or with another DOM library (like <a title="Hammer" href="https://eightmedia.github.io/hammer.js/">Hammer</a> in the example above).</p>

### Issues With return false

One thing that really blows my mind is the strange <code>return false</code> interception in jQuery’s event handlers. According to the W3C’s standards, it should <a title="in most cases" href="https://www.w3.org/TR/DOM-Level-3-Events/#events-dt-cancelable-event">in most cases</a> cancel the default behavior. In jQuery, <code>return false</code> also <a title="stops event delegation" href="https://api.jquery.com/on/#event-handler">stops event delegation</a>.

Such interception creates problems:

1.  Invoking `stopPropagation()` by itself could lead to compatibility problems, because it prevents listeners that are related to some other task from doing their work.
2.  Most developers (even experienced ones) are not aware of such behavior.

It’s unclear why the jQuery community decided to go cross-standards. But better-dom is not going to repeat the same mistake. Thus, <code>return false</code> in an event handler <em>only</em> prevents the browser’s default action, without messing with event propagation, as everyone would expect.</p>

### find and findAll

Element search is <strong>one of the most expensive operations</strong> in the browser. Two native methods could be used to implement it: <code>querySelector</code> and <code>querySelectorAll</code>. The difference is that the first one stops searching on the first match.

This feature enables us to decrease the iterations count dramatically in certain cases. In my tests, the <a title="speed improvement could be up to 20x" href="https://web.archive.org/web/20150607181758/https://jsperf.com:80/dom-find-all-vs-jquery-find/3">speed was up to 20 times faster</a>! Also, you can expect that the improvement will grow according to the size of the document tree.

jQuery has a <code>find</code> method that uses <code>querySelectorAll</code> for general cases. Currently, no function uses <code>querySelector</code> to fetch only the first matched element.

The better-dom library has two separate methods: <code>find</code> and <code>findAll</code>. They allow us to use <code>querySelector</code> optimization. To estimate the potential improvement in performance, I searched for the usage of these methods in all of the source code of my last commercial project:

*   `find` 103 matches across 11 files
*   `findAll` 14 matches across 4 files

The <code>find</code> method is definitely much more popular. It means that <code>querySelector</code> optimization makes sense in most use cases and could give a major performance boost.</p>

## Conclusion

Live extensions really make solving front-end problems much easier. Splitting the UI in many small pieces leads to more independent and maintainable solutions. But as we’ve shown, a framework is not only about them (although it is the main goal).

One thing I’ve learned in the development process is that if you don’t like a standard or you have a different opinion of how things should work, then <strong>just implement it and prove that your approach works</strong>. It’s really fun, too!

More information about the <em>better-dom project</em> <a title="the better-dom project github" href="https://github.com/chemerisuk/better-dom">can be found on GitHub</a>.

button.on("click", handleButtonClick, ["button"]);
</code></pre>

By default, the event handler passes the <code>["target", "defaultPrevented"]</code> array, so no need to add the last argument to get access to these properties:

<pre><code class="language-javascript">
button.on("click", function(target, canceled) {
  // handle button click here
});
</code></pre>

<strong>Late binding is supported as well</strong> (I’d recommend reading Peter Michaux’s review of the topic). It’s a more flexible alternative to the regular event handlers that <a title="exists in the W3C standard" href="https://www.w3.org/TR/DOM-Level-2-Events/events.html#Events-EventListener-handleEvent">exist in the W3C’s standard</a>. It could be useful when you need frequent <code>on</code> and <code>off</code> method calls.

<pre><code class="language-javascript">
button._handleButtonClick = function() { alert("click!"); };

button.on("click", "_handleButtonClick");
button.fire("click"); // shows "clicked" message
button._handleButtonClick = null;
button.fire("click"); // shows nothing
</code></pre>

Last but not least, better-dom has none of the shortcuts that exist in legacy APIs and that behave inconsistently across browsers, like <code>click()</code>, <code>focus()</code> and <code>submit()</code>. The only way to call them is to use the <code>fire</code> method, which executes the default action when no listener has returned <code>false</code>:

<pre><code class="language-javascript">
link.fire("click"); // clicks on the link
link.on("click", function() { return false; });
link.fire("click"); // triggers the handler above but doesn't do a click
</code></pre>

### Functional Methods Support

ES5 standardized a couple of useful methods for arrays, including <code>map</code>, <code>filter</code> and <code>some</code>. They allow us to use common collection operations in a standards-based way. As a result, today we have projects like <a title="underscore" href="https://underscorejs.org/">Underscore</a> and <a title="lodash" href="https://lodash.com/">Lo-Dash</a>, which polyfill these methods for old browsers.

Each element (or collection) in better-dom has the methods below built in:

*   `each` (which differs from `forEach` by returning `this` instead of `undefined`)
*   `some`
*   `every`
*   `map`
*   `filter`
*   `reduce[Right]`

<pre><code class="language-javascript">
var urls, activeLi, linkText; 

urls = menu.findAll("a").map(function(el) {
  return el.get("href");
});
activeLi = menu.children().filter(function(el) {
  return el.hasClass("active");
});
linkText = menu.children().reduce(function(memo, el) {
  return memo || el.hasClass("active") &amp;&amp; el.find("a").get()
}, false);
</code></pre>

## Avoiding jQuery Problems

Most of the following issues can’t be fixed in jQuery without breaking backwards compatibility. That’s why creating a new library seemed like the logical way out.

*   the “magical” `$` function
*   the value of the `[]` operator
*   issues with `return false`
*   `find` and `findAll`

### The “Magical” $ Function

Everyone has heard at some point that the <code>$</code> (dollar) function is kind of like magic. A single-character name is not very descriptive, so it looks like a built-in language operator. That’s why inexperienced developers call it inline everywhere.

Behind the scenes, <strong>the dollar is quite a complex function</strong>. Executing it too often, especially in frequent events such as <code>mousemove</code> and <code>scroll</code>, could cause poor UI performance.

Despite so many articles recommending jQuery objects to be cached, developers continue to insert the dollar function inline, because the library’s syntax encourages them to use this coding style.

Another issue with the dollar function is that it allows us to do two completely different things. People have gotten used to such a syntax, but it’s a bad practice of a function design in general:

<pre><code class="language-javascript">
$("a"); // =&gt; searches all elements that match “a” selector
$("&lt;a&gt;"); // =&gt; creates a &lt;a&gt; element with jQuery wrapper
</code></pre>

<strong>In better-dom, several methods cover the responsibilities of the dollar function</strong> in jQuery: <code>find[All]</code> and <code>DOM.create</code>. <code>find[All]</code> is used to search element(s) according to the CSS selector. <code>DOM.create</code> makes a new elements tree in memory. Their names make it very clear what they are responsible for.</p>

### Value of the [] Operator

Another reason for the problem of frequent dollar function calls is the brackets operator. When a new jQuery object is created, all associated nodes are stored in numeric properties. But note that the value of such a property contains a native element instance (not a jQuery wrapper):

<pre><code class="language-javascript">
var links = $("a");

links[0].on("click", function() { ... }); // throws an error
$(links[0]).on("click", function() { ... }); // works fine
</code></pre>

Because of such a feature, every functional method in jQuery or another library (like Underscore) requires the current element to be wrapped with <code>$()</code> inside of a callback function. Therefore, developers must always keep in mind the type of object they are working with — a native element or a wrapper — despite the fact that they are using a library to work with the DOM.

In better-dom, the brackets operator returns a library’s object, so developers can forget about native elements. There is only one acceptable way to access them: by using a special <code>legacy</code> method.

<pre><code class="language-javascript">
var foo = DOM.find("#foo");

foo.legacy(function(node) {
  // use Hammer library to bind a swipe listener
  Hammer(node).on("swipe", function(e) {
    // handle swipe gesture here
  }); 
});
</code></pre>

In reality, this method is required in very rare cases, such as to be compatible with a native function or with another DOM library (like <a title="Hammer" href="https://eightmedia.github.io/hammer.js/">Hammer</a> in the example above).</p>

### Issues With return false

One thing that really blows my mind is the strange <code>return false</code> interception in jQuery’s event handlers. According to the W3C’s standards, it should <a title="in most cases" href="https://www.w3.org/TR/DOM-Level-3-Events/#events-dt-cancelable-event">in most cases</a> cancel the default behavior. In jQuery, <code>return false</code> also <a title="stops event delegation" href="https://api.jquery.com/on/#event-handler">stops event delegation</a>.

Such interception creates problems:

1.  Invoking `stopPropagation()` by itself could lead to compatibility problems, because it prevents listeners that are related to some other task from doing their work.
2.  Most developers (even experienced ones) are not aware of such behavior.

It’s unclear why the jQuery community decided to go cross-standards. But better-dom is not going to repeat the same mistake. Thus, <code>return false</code> in an event handler <em>only</em> prevents the browser’s default action, without messing with event propagation, as everyone would expect.</p>

### find and findAll

Element search is <strong>one of the most expensive operations</strong> in the browser. Two native methods could be used to implement it: <code>querySelector</code> and <code>querySelectorAll</code>. The difference is that the first one stops searching on the first match.

This feature enables us to decrease the iterations count dramatically in certain cases. In my tests, the <a title="speed improvement could be up to 20x" href="https://web.archive.org/web/20150607181758/https://jsperf.com:80/dom-find-all-vs-jquery-find/3">speed was up to 20 times faster</a>! Also, you can expect that the improvement will grow according to the size of the document tree.

jQuery has a <code>find</code> method that uses <code>querySelectorAll</code> for general cases. Currently, no function uses <code>querySelector</code> to fetch only the first matched element.

The better-dom library has two separate methods: <code>find</code> and <code>findAll</code>. They allow us to use <code>querySelector</code> optimization. To estimate the potential improvement in performance, I searched for the usage of these methods in all of the source code of my last commercial project:

*   `find` 103 matches across 11 files
*   `findAll` 14 matches across 4 files

The <code>find</code> method is definitely much more popular. It means that <code>querySelector</code> optimization makes sense in most use cases and could give a major performance boost.</p>

## Conclusion

Live extensions really make solving front-end problems much easier. Splitting the UI in many small pieces leads to more independent and maintainable solutions. But as we’ve shown, a framework is not only about them (although it is the main goal).

One thing I’ve learned in the development process is that if you don’t like a standard or you have a different opinion of how things should work, then <strong>just implement it and prove that your approach works</strong>. It’s really fun, too!

More information about the <em>better-dom project</em> <a title="the better-dom project github" href="https://github.com/chemerisuk/better-dom">can be found on GitHub</a>.

{{< signature "al, il, ea" >}}


---
title: 'Introducing Live Extensions For Better-DOM: What They Are And How They Work'
slug: introducing-live-extensions-better-dom-javascript
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8ad690ce-d7cb-4271-bf44-8b2fe40b041a/add-ons-illus.jpg
date: 2014-02-05T09:09:17.000Z
author: maksim-chemerisuk
description: >-
  After recently writing an article on “[Writing A Better JavaScript Library For
  The DOM](https://www.smashingmagazine.com/2014/01/13/better-javascript-library-for-the-dom/
  "Writing A Better JavaScript Library For The DOM")”, I realized that the topic
  is indeed a very complex one and that it's important to understand what
  exactly live extensions are and how they work.
categories:
  - Coding
  - JavaScript
  - Techniques
  - jQuery
---
After recently writing an article on “<a title="Writing A Better JavaScript Library For The DOM" href="https://www.smashingmagazine.com/2014/01/13/better-javascript-library-for-the-dom/">Writing A Better JavaScript Library For The DOM</a>”, I realized that the topic is indeed a very complex one and that it's important to understand what exactly live extensions are and how they work. In today's article, I will answer most questions that were asked regarding "<a title="Live Extensions" href="https://github.com/chemerisuk/better-dom/wiki/Live-extensions">live extensions</a>" and help you get going with this new concept.</p>

## The Responsibilities Of Live Extensions

Event handling is one of the key principles of working with the DOM. Events are the primary means of receiving feedback from user interaction.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Browser Input Events: Can We Do Better Than The Click?](https://www.smashingmagazine.com/2015/03/better-browser-input-events/)
*   [Analyzing Network Characteristics Using JavaScript And The DOM](https://www.smashingmagazine.com/2011/11/analyzing-network-characteristics-using-javascript-and-the-dom-part-1/)
*   [Building A Simple Cross-Browser Offline To-Do List](https://www.smashingmagazine.com/2014/09/building-simple-cross-browser-offline-todo-list-indexeddb-websql/)
*   [<span class="headline">JavaScript Events And Responding To The User</span>](https://www.smashingmagazine.com/2012/08/javascript-events-responding-user/)

{{% feature-panel %}}

### Simple Event Binding

In this first example, documentation and tutorials that cover DOM events is what I call “simple event binding”. You attach a listener for the desired event on the DOM element in which you expect it to happen on.

<pre><code class="language-javascript">
link.addEventListener("click", function(e) {
  // do something when the link is clicked
}, false);
</code></pre>

The first argument indicates the type of an event, the second argument is a listener, and the third argument defines an event phase (so-called "bubbling" or "capturing"). The reason why the last argument exists is because most DOM events traverse the DOM tree from document node to target node (capture phase) and back to the document node (bubble phase). This process is called “event flow” and brings several powerful features.</p>

### Live and Delegated Events

Instead of attaching a handler for each element in a group, we can attach one listener onto an ancestor shared by all of the elements in that specific group. Then, we can determine where an event took place using the <code>target</code> property of the event object, passed into the listener. This is known as “event delegation”:

<pre><code class="language-javascript">
list.addEventListener("click", function(e) {
  if (e.target.tagName === "LI") {
    // do something when a child &lt;li&gt; element is clicked
  }
}, false);
</code></pre>

By having all event handlers on a particular parent, we can update the <code>innerHTML</code> property of this element without losing the ability to listen to events for new elements. The feature was called "Live Events" in jQuery, and it quickly became popular because of its ability to filter events by a CSS selector. Later, <a title="delegated events" href="https://learn.jquery.com/events/event-delegation/#event-propagation">delegated events</a> replaced them due to their flexibility by allowing to bind a listener to any element within the document tree.

But even event delegation does not overcome the following problems:

*   When DOM mutation is required after a new element (that matches a specific selector) comes into the document tree,
*   When an element should be initialized on a excessive event such as `scroll` or `mousemove`,
*   Or on non-bubbling events, e.g. `load`, `error`, etc.

This is what live Extensions aim to solve.</p>

### Live Extensions Use Cases

Take a look at the following diagram that explains the responsibilities:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d5b18ae-49b4-4dc8-b88b-f7373f9466ec/live-extension-respo-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d5b18ae-49b4-4dc8-b88b-f7373f9466ec/live-extension-respo-opt.jpg" alt="live-extension-respo" width="500" height="474" /></a>

<strong>1. DOM Mutations For Existing And Future Elements</strong>

Imagine you want to develop a reusable datepicker widget. In HTML5, there is a standards-based <code>&lt;input type="date"&gt;</code> element that could be used to create a polyfill. But the problem is that this element looks and behaves very different from browser to browser:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/525b020f-38fc-4803-8ab3-e3c1f859001a/date-input-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/525b020f-38fc-4803-8ab3-e3c1f859001a/date-input-opt.jpg" alt="dateinputs" width="500" height="251" /></a><br>
<em>Date input element in different browsers.</em>

The only way to make the element behave consistently is to set the type attribute value to <code>"text"</code>. This will cancel a legacy implementation and enable JavaScript to make your own. Try defining a live extension with the example below:

<pre><code class="language-javascript">
DOM.extend("input[type=date]", {
  constructor: function() {
    // cancel browser-specific implementation
    this.set("type", "text");
    // make your own styleable datepicker,
    // attach additional event handlers etc.
  }
});
</code></pre>

<strong>2. Media Query Callbacks</strong>

I highly recommend reading Paul Hayes' article on how to “<a title="Use CSS transitions to link Media Queries and JavaScript" href="https://www.paulrhayes.com/2011-11/use-css-transitions-to-link-media-queries-and-javascript/">Use CSS transitions to link Media Queries and JavaScript</a>”.
<blockquote>"A common problem in responsive design is the linking of CSS3’s media queries and JavaScript. For instance on a larger screen we can restyle, but it might be useful to use JavaScript and pull in different content at the same time, e.g. higher quality images."</blockquote>

Paul was probably the first who started to use “hidden force” of CSS3 animation events to solve mutation-related problems. Live extensions are powered by the same trick, therefore you can use them to make DOM modifications depending on the current viewport:

<pre><code class="language-javascript">
DOM.extend(".rwd-menu", {
  constructor: function() {
    var viewportWidth = DOM.find("html").get("clientWidth");

    if (viewportWidth &lt; 768) {
      // hide &lt;ul&gt; and construct Emmet abbreviation for a
      // &lt;select&gt; element that should be used on small screens
      this.hide().after("select[onchange='location=this.value']&gt;" +
        this.children("li").reduce(function(memo, item) {
          var text = item.get("textContent"),
            href = item.find("a").get("href");

          memo.push("option[value=" + href + "]&gt;<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98845fc8-55a6-4475-ac3a-bfdc206a8f11/live-extension-respo.png"><img loading="lazy" decoding="async" class="size-medium wp-image-130776" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1deb579b-ae95-4df8-b214-c75878423d72/live-extension-respo-300x284.png" alt="live-extension-respo" width="300" height="284" /></a>{" + text + "}");
          return memo;
        }, []).join("^"));
    }
  }
});
</code></pre>

<strong>3. Element Media Queries</strong>

Back in 2011, Andy Hume <a title="implemented a script" href="https://github.com/ahume/selector-queries/">implemented a script</a> for applying styles depending on the dimensions of a particular element (not viewport, like for media queries). Later, this technique was named “element media queries”:
<blockquote>"Media queries work really well when you want to adjust the core layouts of the site, but they're less suited to changing styles at a smaller more granular level."</blockquote>

With the help of live extensions, it’s easy to implement element media queries support using the <code>offset</code> method:

<pre><code class="language-javascript">
DOM.extend(".signup-form", {
  constructor: function() {
    var currentWidth = this.offset().width;
    // add extra class depending on current width
    if (currentWidth &lt; 150) {
      this.addClass("small-signup-form");
    } else if (currentWidth &gt; 300) {
      this.addClass("wide-signup-form");
    }
  }
});
</code></pre>

<strong>4. Efficiently Attach A Global Listener To Frequent Events</strong>

<pre><code class="language-javascript">
DOM.extend(".detectable", {
  constructor: function() {
    // mousemove bubbles but it’s usually a very bad
    // idea to listen to such event on a document level
    // but live extensions help to solve the issue
    this.on("mousemove", this.onMouseMove, ["pageX", "pageY"]);
  },
  onMouseMove: function(x, y) {
    // just output current coordinates into console
    console.log("mouse position: x=" + x + ", y=" + y);
  }
});
</code></pre>

<strong>5. Listing Non-Bubbling Events On A Document Level</strong>

<pre><code class="language-javascript">
DOM.extend("img.safe-img", {
  constructor: function() {
    // error event doesn’t bubble so it’s not
    // possible to do the same using live events
    this.on("error", this.onError);
  },
  onError: function() {
    // show a predefined png if an image download fails
    this.src = "/img/download-failed.png"
  }
});
</code></pre>

## Brief Look Into History

The problems which live extensions aim to solve is not entirely new, of course. There are different approaches that address the above-mentioned issues. Let’s have a quick look at some of them.</p>

### HTML Components

Internet Explorer started supporting <a href="https://msdn.microsoft.com/en-US/library/ie/ms531079.aspx">DHTML behaviors</a> with IE 5.5:
<blockquote>"DHTML behaviors are components that encapsulate specific functionality or behavior on a page. When applied to a standard HTML element on a page, a behavior enhances that element's default behavior."</blockquote>

To attach behavior to future elements, Internet Explorer used an <code>*.htc</code> file with a special syntax. Here's an example illustrating how we used to make <code>:hover</code> work on elements instead of <code>&lt;a&gt;</code>:

<pre><code class="language-javascript">
&lt;PUBLIC:COMPONENT URN="urn:msdn-microsoft-com:workshop" &gt;
  &lt;PUBLIC:ATTACH EVENT="onmouseover" ONEVENT="Hilite()" /&gt;
  &lt;PUBLIC:ATTACH EVENT="onmouseout"  ONEVENT="Restore()"  /&gt;
  &lt;SCRIPT LANGUAGE="JScript"&gt;
  var normalColor, normalSpacing;

  function Hilite() {
    normalColor  = currentStyle.color;
    normalSpacing= currentStyle.letterSpacing;

    runtimeStyle.color  = "red";
    runtimeStyle.letterSpacing = 2;
  }

  function Restore() {
    runtimeStyle.color  = normalColor;
    runtimeStyle.letterSpacing = normalSpacing;
  }
&lt;/SCRIPT&gt;
&lt;/PUBLIC:COMPONENT&gt;
</code></pre>

If you provided the above-mentioned code into the <code>hilite.htc</code> file, you could access it within CSS through the <code>behavior</code> property:

<pre><code class="language-css">
li {
  behavior: url(hilite.htc);
}
</code></pre>

I was really surprised to discover that <a title="HTML components supported creating custom tags" href="https://msdn.microsoft.com/en-us/library/ms531076(v=vs.85).aspx">HTML components supported creating custom tags</a> (starting from version 5.5), have single domain limitations and tons of other stuff that you probably have never used before. Despite <a title="Microsoft submitting a proposal to W3C" href="https://www.w3.org/TR/NOTE-HTMLComponents">Microsoft submitting a proposal to W3C</a>, other browser vendors decided not to support this feature. As a result, HTML components were removed from Internet Explorer 10.</p>

### Decorators

In my <a href="https://www.smashingmagazine.com/2014/01/13/better-javascript-library-for-the-dom/">previous article</a>, I mentioned the <a title="Decorators section" href="https://www.w3.org/TR/components-intro/#decorator-section">Decorators</a> which are a part of Web components. Here’s how you can implement the open/closed state indicator of the <a title="&lt;details&gt; element" href="https://www.hongkiat.com/blog/html5-details-summary-tags/"><code>&lt;details&gt;</code> element</a> using decorators:

<pre><code class="language-javascript">
&lt;decorator id="details-closed"&gt;
  &lt;script&gt;
    function clicked(event) {
      event.target.setAttribute('open', 'open');
    }
    [{selector: '#summary', type: 'click', handler: clicked}];
  &lt;/script&gt;
  &lt;template&gt;
    &lt;a id="summary"&gt;
      &amp;blacktriangleright; &lt;content select="summary"&gt;&lt;/content&gt;
    &lt;/a&gt;
  &lt;/template&gt;
&lt;/decorator&gt;

&lt;decorator id="details-open"&gt;
  &lt;script&gt;
  function clicked(event) {
    event.target.removeAttribute('open');
  }
  [{selector: '#summary', type: 'click', handler: clicked}];
  &lt;/script&gt;
  &lt;template&gt;
    &lt;a id="summary"&gt;
      &amp;blacktriangledown; &lt;content select="summary"&gt;&lt;/content&gt;
    &lt;/a&gt;
    &lt;content&gt;&lt;/content&gt;
  &lt;/template&gt;
&lt;/decorator&gt;
</code></pre>

Decorators are also applied using the special <code>decorator</code> property in CSS:

<pre><code class="language-css">
details {
  decorator: url(#details-closed);
}

details[open] {
  decorator: url(#details-open);
}
</code></pre>

You'll quickly notice that this is very close to what Microsoft proposed in <em>HTML Components</em>. The difference is that instead of separate HTC files, decorators are HTML elements that can be defined within the same document. The example above is only provided to show that the Web platform is working on these topics, since decorators aren’t properly specified just yet.</p>

## Live Extensions API

While designing APIs for live extensions, I decided to follow the following rules:

1.  **Live extensions should be declared in JavaScript.** I strongly believe that everything that somehow changes the behavior of an element should be presented in a JavaScript file. (Note that better-dom inserts a new CSS rule behind the scenes, but this includes only implementation details).
2.  **APIs should be simple to use.** No tricky file formats or new HTML elements: only a small amount of knowledge related to the constructor and event handlers is required to start developing a live extension (thus, the barrier to entry should be low).

As a result, there are only two methods to deal with: <code>DOM.extend</code> and <code>DOM.mock</code>.</p>

### DOM.extend

<code>DOM.extend</code> declares a live extension. It accepts a CSS selector as the first argument which defines what elements you want to capture. General advice: try to make the selector simple.

Ideally, you should only use a tag name, class or attribute with or without a value or their combinations with each other. These selectors can be tested quicker without calling an expensive <a title="matchesSelector method" href="https://developer.mozilla.org/en-US/docs/Web/API/Element.matches"><code>matchesSelector</code> method</a>.

The second argument is a live extension definition. All properties of the object will be mixed with an element wrapper interface except <em>constructor</em> and <em>event handlers</em>.

Let’s look at a simple example. Let's assume we have such an element on a Web page:

<pre><code class="language-markup">
&lt;div class="signin-form modal-dlg"&gt;...&lt;/div&gt;
</code></pre>

The task is to show it as a modal dialog. This is how the live extension could look like:

<pre><code class="language-javascript">
DOM.extend(".modal-dlg", {
  constructor: function() {
    var backdrop = DOM.create("div.modal-dlg-backdrop");
    // using bind to store reference to backdrop internally
    this.showModal = this.showModal.bind(this, backdrop);
    // we will define event handlers later
  },
  showModal: function(backdrop) {
    this.show();
    backdrop.show();
  }
});
</code></pre>

Now you can access the public method <code>showModal</code> in any (present or future) element that has the <code>modal-dlg</code> class (in our case this is the <code>signin-form</code> div):

<pre><code class="language-javascript">
var signinForm = DOM.find(".signin-form");

DOM.find(".signin-btn").on("click", function() {
  // the signin button doesn’t have the modal-dlg class
  // so it’s interface doesn’t contain the showModal method
  console.log(this.showModal); // =&gt; undefined
  signinForm.showModal(); // =&gt; shows the signin dialog
});
</code></pre>

<em>Note</em>: The <code>better-dom-legacy.js</code> file which is included conditionally for Internet Explorer versions 8 and 9, contains the <a title="es5-shim" href="https://github.com/kriskowal/es5-shim">es5-shim</a> library so you can safely use standards-based EcmaScript 5 functions (such as <a title="Function.prototype.bind" href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind"><code>Function.prototype.bind</code></a>) in your code. I’ve been using the <code>bind</code> method heavily in my code to build testable methods easily.</p>

### The Constructor Property

The constructor function is called when an element becomes <em>visible</em>. This is because of the <code>animationstart</code> event that is used to implement <code>DOM.extend</code>. Browsers are clever so they don’t fire animation events for hidden elements. This lazy initialization saves resources sometimes, but be careful with accessing initially hidden elements.

In older Internet Explorers versions such as 8 and 9, <code>contentready</code> event from <code>better-dom-legacy.htc</code> is used to implement live extensions. Therefore, the constructor function executes immediately in these browsers — even for hidden elements.

<em>Note</em>: Keep in mind <em>not</em> to rely on time whenever an extension has been initialized. The actual initialization of a live extension varies across browsers!

Constructor is usually the place where you attach event handlers and perform DOM mutations where necessary. Once the function has been completed, all methods that begin with “on” (in better-dom 1.7 also “do”) followed by an uppercase letter, event handlers, will be removed from the element wrapper’s interface.

Let’s update our <code>.signin-form</code> live extension with the help of a close button and the <code>ESC</code> key:

<pre><code class="language-javascript">
DOM.extend(".modal-dlg", {
  constructor: function() {
    var backdrop = DOM.create("div.modal-dlg-backdrop"),
      closeBtn = this.find(".close-btn");

    this.showModal = this.showModal.bind(this, backdrop);
    // handle click on the close button and ESC key
    closeBtn.on("click", this.onClose.bind(this, backdrop));
    DOM.on("keydown", this.onKeyDown.bind(this, closeBtn), ["which"])
  },
  showModal: function(backdrop) {
    this.show();
    backdrop.show();
  },
  onClose: function(backdrop) {
    this.hide();
    frame.hide();
  },
  onKeyDown: function(closeBtn, which) {
    if (which === 27) {
      // close dialog by triggering click event
      closeBtn.fire("click");
    }
  }
});
</code></pre>

Despite the fact that the live extension contains both <code>onClose</code> and <code>onKeyDown</code> methods, they won’t be mixed into the element wrapper interface:

<pre><code class="language-javascript">
var signinForm = DOM.find(".signin-form");

console.log(signinForm.onClose); // =&gt; undefined
console.log(signinForm.onKeyDown); // =&gt; undefined
</code></pre>

This kind of behavior exists simply because you can have multiple live extensions for a single element that may overload public methods of each other and produce unexpected results. For event handlers, this is not possible; they exist only inside of the constructor function.</p>

### Extending * Elements

Sometimes it is useful to extend all of the element wrappers with a particular method (or methods). But then again, you can also use the universal selector to solve the problem:

<pre><code class="language-javascript">
DOM.extend("*", {
  gesture: function(type, handler) {
    // implement gestures support
  }
});
…
DOM.find("body").gesture("swipe", function() {
  // handle a swipe gesture on body
});
</code></pre>

The <code>*</code> selector has a special behavior: all extension declaration properties will be injected directly into the element wrapper prototype except for the constructor which is totally ignored. Therefore, there is no performance penalty that is usually associated with the universal selector.

<em>Note</em>: Never pass more specific selectors such as <code>.some-class *</code> into <code>DOM.extend</code> because they are slow and do not have the same behavior as mentioned above.</p>

### Multiple Live Extensions on the Same Element

More often that not, it makes sense to split a large live extension into several pieces to reduce complexity. For instance, you may have such an element on your page:

<pre><code class="language-markup">
&lt;div class="infinite-scroll chat"&gt;&lt;/div&gt;
</code></pre>

There are two different extensions attached to it. The <code>.infinite-scroll</code> extension implements a well-known infinite scroll pattern, e.g. it’s responsible for loading new content. At the same time, the <code>.chat</code> extension shows tooltips whenever a user hovers over a userpic, adds smileys into messages, and so on. However, be accurate with multiple extensions: even though all event handlers may have been removed from the interface, you still may have public methods that intersect with each other.</p>

### Inheritance

Live extensions respect declaration order; you can use this to your advantage and develop your own component hierarchy. Late binding helps to declare overridable event handlers and method overloading allows to redefine a method implementation in a child extension:

<pre><code class="language-javascript">
DOM.extend(".my-widget", {
  constructor: function() {
    this.on("click", "_handleClick");
  },
  showMessage: function() { }
});

DOM.extend(".my-button", {
  _handleClick: function() {
    console.log("I am a button!");
  },
  showMessage: function() {
    alert("I am a button message!");
  }
});
</code></pre>

If you take a closer look at the code above, you'll notice that the <code>.my-button</code> extension does not attach a click listener. The registration is done with the help of late binding instead of a simple event handler in <code>.my-widget</code>. Late binding is a perfect choice here: even if a child does not implement <code>_handleClick</code> there won’t be any errors since the handler will be silently ignored.

While spreading functionality across multiple modules is possible, this is not recommended in everyday use. Double check if you really need to go in this direction, because it’s the most complex one.</p>

### Writing Tests with DOM.mock

One requirement for a high-quality widget is test coverage. New elements are captured by a live extension asynchronously, so it’s not that easy to simply make them in memory. To solve this problem, better-dom has the <code>DOM.mock</code> function:

<pre><code class="language-javascript">
var myButton = DOM.mock("button.my-button");
</code></pre>

<code>DOM.mock</code> creates elements, just like <code>DOM.create</code>. Additionally, it synchronously applies the registered live extensions to the newly created elements. For even more convenience, all wrapper objects created by <code>DOM.mock</code> preserve event handlers (e.g. <code>onClick</code>), so you can test them.

From time to time, you may need to create a “fake” instance of an element. Use <code>DOM.mock</code> without arguments to make such an object:

<pre><code class="language-javascript">
console.log(DOM.mock().length); // =&gt; 0
</code></pre>

A test for the modal dialog live extension introduced earlier could look like this (I use <a title="Jasmine" href="https://github.com/pivotal/jasmine">Jasmine</a>):

<pre><code class="language-javascript">
describe(".modal-dlg", function() {
  var dlg, backdrop;

  beforeEach(function() {
    dlg = DOM.mock("div.modal-dlg");
    backdrop = DOM.mock();
  });

  it("should hide itself and backdrop on close", function() {
    var dlgSpy = spyOn(dlg, "hide"),
      backdropSpy = spyOn(backdrop, "hide");

    dlg.onClose(backdrop);
    expect(dlgSpy).toHaveBeenCalled();
    expect(backdropSpy).toHaveBeenCalled();
  });

  it("should show itself and backdrop on show", function() {
    var dlgSpy = spyOn(dlg, "show"),
      backdropSpy = spyOn(backdrop, "show");

    dlg.showModal(backdrop);
    expect(dlgSpy).toHaveBeenCalled();
    expect(backdropSpy).toHaveBeenCalled();
  });
});
</code></pre>

### Feature Detection (in better-dom 1.7)

There are some cases when filtering with a CSS selector is not flexible enough. For instance, let's say you want to declare a live extension but only for browsers that support (or do not support) a particular feature. You may need to run tests in a headless browser like <a title="PhantomJS" href="https://phantomjs.org/">PhantomJS</a> that support the feature natively. Starting with better-dom 1.7, <code>DOM.extend</code> supports the optional argument <code>condition</code>.

Assume we need to create a polyfill for the <a title="placeholder attribute" href="https://www.w3.org/TR/2011/WD-html5-20110525/common-input-element-attributes.html#the-placeholder-attribute"><code>placeholder</code> attribute</a>. It doesn’t make sense to implement it for browsers that have built-in support. Below is an example of how the feature detection could look like:

<pre><code class="language-javascript">
var supportsPlaceholder = typeof DOM.create("input")
      .get("placeholder") === "string";
</code></pre>

By using just a simple "If" statement as shown in the example below, we won’t have an ability to test the widget because PhantomJS supports the <code>placeholder</code> attribute and the live extension will never be declared.

<pre><code class="language-javascript">
if (!supportsPlaceholder) {
  DOM.extend("[placeholder]", {
    // implement placeholder support
  };
}
</code></pre>

In order to solve this problem, you can use an extra <code>condition</code> argument in <code>DOM.extend</code> that might be Boolean or a function:

<pre><code class="language-javascript">
DOM.extend("[placeholder]", !supportsPlaceholder, {
  constructor: function() { … },
  onFocus: function() { … },
  onBlur: function() { … }
});
</code></pre>

<code>DOM.mock</code> ignores the <code>condition</code> argument, so you can access all methods of the <code>[placeholder]</code> extension even if current browser passes the check:

<pre><code class="language-javascript">
var input = DOM.mock("input[placeholder=test]");

typeof input.onFocus; // =&gt; "function"
</code></pre>

## Conclusion

Live extensions — and better-dom as an implementation of the concept — are a good base to build upon whenever your target is uncertain, e.g. when creating a polyfill that may or may not be used on a particular site. Or regular widgets that may or may not be needed, depending upon some AJAX call.

Live extensions aim to separate declaration and the use of widgets. They bring loose coupling (or decoupling, rather) of any DOM-based component, and allow your code to become smaller, cleaner and easier to maintain. You can even combine such independent pieces with any existing framework within the market (or with the vanilla DOM, of course).

You may now be thinking, "But wait, there are projects like <a title="Polymer" href="https://www.polymer-project.org/">Polymer</a> or <a title="x-tags" href="https://www.x-tags.org/">x-tags</a>, right?" Well, <strong>live extensions cover a different area</strong>; they are not about custom tags but rather about extending existing ones instead. I prefer a standards-based way (if possible) of creating UI widgets, so making polyfills is my choice.

Better-dom also has another advantage: a carefully crafted live extension does not force you to rewrite a website's markup using different tags. All you need is to simply include a script file on your page. Standards-based elements can potentially work without JavaScript, so they degrade well when it’s disabled. And the library’s <a title="browser support" href="https://github.com/chemerisuk/better-dom#browser-support">browser support</a> allows you to start using live extensions straight away.

Feel free to share your thoughts in the comments section below or on the <a title="better-dom project home page" href="https://github.com/chemerisuk/better-dom">better-dom project home page</a>.

{{< signature "il" >}}


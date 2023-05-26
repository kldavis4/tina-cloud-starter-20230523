---
title: Making A Complete Polyfill For The HTML5 Details Element
slug: complete-polyfill-html5-details-element
image: null
date: 2014-11-28T22:56:17.000Z
author: maksim-chemerisuk
description: >-
  HTML5 introduced a bunch of new tags, one of which is `<details>`. This
  element is a solution for a common UI component: a collapsible block. Almost
  every framework, including Bootstrap and jQuery UI, has its own plugin for a
  similar solution, but none conform to the HTML5 specification — probably
  because most were around long before `<details>` got specified and, therefore,
  represent different approaches.
categories:
  - Coding
  - CSS
  - JavaScript
  - HTML5
---
HTML5 introduced a bunch of new tags, one of which is <code>&lt;details&gt;</code>. This element is a solution for a common UI component: a collapsible block. Almost every framework, including Bootstrap and jQuery UI, has its own plugin for a similar solution, but none conform to the HTML5 specification — probably because most were around long before <code>&lt;details&gt;</code> got specified and, therefore, represent different approaches. A standard element allows everyone to use the same markup for a particular type of content. That’s why creating a robust polyfill <a href="https://caniuse.com/#feat=details">makes sense</a>.</p>

<em>Disclaimer</em>: This is quite a technical article, and while I’ve tried to minimize the code snippets, the article still contains quite a few of them. So, be prepared!

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2013/01/the-importance-of-sections/#further-reading-on-smashingmag)

*   [Coding An HTML 5 Layout From Scratch](https://www.smashingmagazine.com/2009/08/designing-a-html-5-layout-from-scratch/)
*   [Sexy New HTML5 Semantics](https://www.smashingmagazine.com/2011/11/html5-semantics/)
*   [Learning to Love HTML5](https://www.smashingmagazine.com/2010/11/learning-to-love-html5/)
*   [HTML 5 Cheat Sheet (PDF)](https://www.smashingmagazine.com/2009/07/html-5-cheat-sheet-pdf/)

## Existing Solutions Are Incomplete

<a href="https://github.com/mathiasbynens/jquery-details">I’m not</a> the <a href="https://github.com/manuelbieh/Details-Polyfill">first person</a> to try to implement such a polyfill. Unfortunately, all other solutions exhibit one or another problem:

{{% feature-panel %}}

1.  **No support for future content** Support for future content is extremely valuable for single-page applications. Without it, you would have to invoke the initialization function every time you add content to the page. Basically, a developer wants to be able to drop `<details>` into the DOM and be done with it, and not have to fiddle with JavaScript to get it going.
2.  **The `toggle` event is missing** This event is a notification that a `details` element has changed its `open` state. Ideally, it should be a vanilla DOM event.

In this article we'll use <a href="https://github.com/chemerisuk/better-dom">better-dom</a> to make things simpler. The main reason is the <a href="https://github.com/chemerisuk/better-dom/wiki/Live-extensions">live extensions</a> feature, which solves the problem of invoking the initialization function for dynamic content. (For more information, read my <a href="https://www.smashingmagazine.com/2014/02/05/introducing-live-extensions-better-dom-javascript/">detailed article about live extensions</a>.) Additionally, better-dom outfits live extensions with a <strong>set of tools that do not (yet) exist in vanilla DOM</strong> but that come in handy when implementing a polyfill like this one.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/78a247bb-5521-4f26-97ac-af2e84603d2f/1-details-element-in-safari-8-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/40b9362a-5f7f-4603-bcf7-054ad3a6f2e0/1-details-element-in-safari-8-opt.jpg" alt="1-details-element-in-Safari-8-opt" width="500" height="227" /></a><figcaption>The <code>details</code> element in Safari 8 (<a>View large version</a>)</figcaption></figure>

Check out the <a href="https://chemerisuk.github.io/better-details-polyfill/">live demo</a>.

Let's take a closer look at all of the hurdles we have to overcome to make <code>&lt;details&gt;</code> available in browsers that don't support it.</p>

## Future Content Support

To start, we need to declare a live extension for the <code>"details"</code> selector. What if the browser already supports the element natively? Then we’ll need to add some feature detection. This is easy with the optional second argument <code>condition</code>, which prevents the logic from executing if its value is equal to <code>false</code>:

<pre><code class="language-javascript">
// Invoke extension only if there is no native support
var open = DOM.create("details").get("open");

DOM.extend("details", typeof open !== "boolean", {
  constructor: function() {
    console.log("initialize &lt;details&gt;…");
  }
});
</code></pre>

As you can see, we are trying to detect native support by checking for the <code>open</code> property, which obviously only exists in browsers that recognize <code>&lt;details&gt;</code>.

What sets <a href="https://chemerisuk.github.io/better-dom/DOM.html#extend"><code>DOM.extend</code></a> apart from a simple call like <code>document.querySelectorAll</code> is that the <code>constructor</code> function executes for future content, too. And, yes, it works with any library for manipulating the DOM:

<pre><code class="language-javascript">
// You can use better-dom…
DOM.find("body").append(
  "&lt;details&gt;&lt;summary&gt;TITLE&lt;/summary&gt;&lt;p&gt;TEXT&lt;/p&gt;&lt;/details&gt;");
// =&gt; logs "initialize &lt;details&gt;…"

// or any other DOM library, like jQuery…
$("body").append(
  "&lt;details&gt;&lt;summary&gt;TITLE&lt;/summary&gt;&lt;p&gt;TEXT&lt;/p&gt;&lt;/details&gt;");
// =&gt; logs "initialize &lt;details&gt;…"

// or even vanilla DOM.
document.body.insertAdjacentElement("beforeend",
  "&lt;details&gt;&lt;summary&gt;TITLE&lt;/summary&gt;&lt;p&gt;TEXT&lt;/p&gt;&lt;/details&gt;");
// =&gt; logs "initialize &lt;details&gt;…"
</code></pre>

In the following sections, we’ll replace the <code>console.log</code> call with a real implementation.</p>

## Implementation Of `<summary>` Behavior

The <code>&lt;details&gt;</code> element may take <code>&lt;summary&gt;</code> as a child element.
<blockquote>The first summary element child of details, if one is present, represents an overview of details. If no child summary element is present, then the user agent should provide its own legend (for example, “Details”).</blockquote>

Let’s add mouse support. A click on the <code>&lt;summary&gt;</code> element should toggle the <code>open</code> attribute on the parent <code>&lt;details&gt;</code> element. This is what it looks like using better-dom:

<pre><code class="language-javascript">
DOM.extend("details", typeof open !== "boolean", {
  constructor: function() {
    this
      .children("summary:first-child")
      .forEach(this.doInitSummary);
  },
  doInitSummary: function(summary) {
    summary.on("click", this.doToggleOpen);
  },
  doToggleOpen: function() {
    // We’ll cover the open property value later.
    this.set("open", !this.get("open"));
  }
});
</code></pre>

The <code>children</code> method returns a JavaScript array of elements (not an array-like object as in vanilla DOM). Therefore, if no <code>&lt;summary&gt;</code> is found, then the <code>doInitSummary</code> function is not executed. Also, <code>doInitSummary</code> and <code>doToggleOpen</code> are <a href="https://github.com/chemerisuk/better-dom/wiki/Live-extensions#public-members-and-private-functions">private functions</a>, they always are invoked for the current element. So, we can pass <code>this.doInitSummary</code> to <code>Array#forEach</code> without extra closures, and everything will execute correctly there.

Having keyboard support in addition to mouse support is good as well. But first, let’s make <code>&lt;summary&gt;</code> a focusable element. A typical solution is to set the <code>tabindex</code> attribute to <code>0</code>:

<pre><code class="language-javascript">
doInitSummary: function(summary) {
  // Makes summary focusable
  summary.set("tabindex", 0);
  …
}
</code></pre>

Now, the user hitting the space bar or the “Enter” key should toggle the state of <code>&lt;details&gt;</code>. In better-dom, there is no direct access to the event object. Instead, we need to declare which properties to grab using an extra array argument:

<pre><code class="language-javascript">
doInitSummary: function(summary) {
  …
  summary.on("keydown", ["which"], this.onKeyDown);
}
</code></pre>

Note that we can reuse the existing <code>doToggleOpen</code> function; for a <code>keydown</code> event, it just makes an extra check on the first argument. For the click event handler, its value is always equal to <code>undefined</code>, and the result will be this:

<pre><code class="language-javascript">
doInitSummary: function(summary) {
  summary
    .set("tabindex", 0)
    .on("click", this.doToggleOpen)
    .on("keydown", ["which"], this.doToggleOpen);
},
doToggleOpen: function(key) {
  if (!key || key === 13 || key === 32) {
    this.set("open", !this.get("open"));
    // Cancel form submission on the ENTER key.
    return false;
  }
}
</code></pre>

Now we have a mouse- and keyboard-accessible <code>&lt;details&gt;</code> element.

## `<summary>` Element Edge Cases

The <code>&lt;summary&gt;</code> element introduces several edge cases that we should take into consideration:

### 1. When `<summary>` Is a Child But Not the First Child

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cae55a51-e0e3-4f62-aa52-0e0c5ad954b9/2-summary-element-is-not-the-first-child-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/326d9781-af39-4339-aa83-821469833fb9/2-summary-element-is-not-the-first-child-opt.jpg" alt="2-summary-element-is-not-the-first-child-opt" width="500" height="197" /></a><figcaption>What the Chrome browser outputs when the <code>summary</code> element is not the first child. (<a>View large version</a>)</figcaption></figure>

Browser vendors have tried to fix such <em>invalid markup</em> by moving <code>&lt;summary&gt;</code> to the position of the first child visually, even when the element is not in that position in the flow of the DOM. I was confused by such behavior, so I <a href="https://lists.w3.org/Archives/Public/public-html/2014Nov/0043.html">asked the W3C for clarification</a>. The W3C confirmed that <code>&lt;summary&gt;</code> must be the first child of <code>&lt;details&gt;</code>. If you check the markup in the screenshot above on <a href="https://validator.w3.org/nu/">Nu Markup Checker</a>, it will fail with the following error message:
<blockquote>Error: Element summary not allowed as child of element details in this context. […] Contexts in which element summary may be used: As the first child of a details element.</blockquote>

My approach is to move the <code>&lt;summary&gt;</code> element to the position of the first child. In other words, the polyfill fixes the invalid markup for you:

<pre><code class="language-javascript">
doInitSummary: function(summary) {
  // Make sure that summary is the first child
  if (this.child(0) !== summary) {
    this.prepend(summary);
  }
  …
}
</code></pre>

### 2. When the `<summary>` Element Is Not Present

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/671d4ba9-c4e2-44ba-99ae-60b673e40ebb/3-summary-element-does-not-exist-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07bb8e06-ef38-49a1-8fa6-db1a45a8b045/3-summary-element-does-not-exist-opt.jpg" alt="3-summary-element-does-not-exist-opt" width="500" height="145" /></a><figcaption>What the Chrome browser outputs when the <code>summary</code> element is not present (<a>View large version</a>)</figcaption></figure>

As you can see in the screenshot above, browser vendors insert “Details” as a legend into <code>&lt;summary&gt;</code> in this case. The markup stays untouched. Unfortunately, we can’t achieve the same without accessing the <a href="https://www.w3.org/TR/shadow-dom/">shadow DOM</a>, which unfortunately has <a href="https://caniuse.com/#feat=shadowdom">weak support</a> at present. Still, we can set up <code>&lt;summary&gt;</code> manually to comply with standards:

<pre><code class="language-javascript">
constructor: function() {
  …
  var summaries = this.children("summary");
  // If no child summary element is present, then the
  // user agent should provide its own legend (e.g. "Details").
  this.doInitSummary(
    summaries[0] || DOM.create("summary&gt;`Details`"));
}
</code></pre>

## Support For `open` Property

If you try the code below in browsers that support <code>&lt;details&gt;</code> natively and in others that don’t, you’ll get different results:

<pre><code class="language-javascript">
details.open = true;
// &lt;details&gt; changes state in Chrome and Safari
details.open = false;
// &lt;details&gt; state changes back in Chrome and Safari
</code></pre>

In Chrome and Safari, changing the value of <code>open</code> triggers the addition or removal of the attribute. Other browsers do not respond to this because they do not support the <code>open</code> property on the <code>&lt;details&gt;</code> element.

Properties are different from simple values. They have a pair of getter and setter functions that are invoked every time you read or assign a new value to the field. And JavaScript has had an API to declare properties since version 1.5.

The good news is that one old browser we are going to use with our polyfill, Internet Explorer (IE) 8, has <em>partial</em> support for the <code>Object.defineProperty</code> function. The limitation is that the function works only on DOM elements. But that is exactly what we need, right?

There is a problem, though. If you try to set an attribute with the same name in the setter function in IE 8, then the browser will stack with infinite recursion and crashes. In old versions of IE, changing an attribute will trigger the change of an appropriate property and vice versa:

<pre><code class="language-javascript">
Object.defineProperty(element, "foo", {
  …
  set: function(value) {
    // The line below triggers infinite recursion in IE 8.
    this.setAttribute("foo", value);
  }
});
</code></pre>

So you can’t modify the property without changing an attribute there. This limitation has prevented developers from using the <code>Object.defineProperty</code> for quite a long time.

The good news is that I’ve found a solution.</p>

## Fix For Infinite Recursion In IE 8

Before describing the solution, I’d like to give some background on one feature of the HTML and CSS parser in browsers. In case you weren’t aware, these <strong>parsers are case-insensitive</strong>. For example, the rules below will produce the same result (i.e. a base red for the text on the page):

<pre><code class="language-css">
body { color: red; }
/* The rule below will produce the same result. */
BODY { color: red; }
</code></pre>

The same goes for attributes:

<pre><code class="language-javascript">
el.setAttribute("foo", "1");
el.setAttribute("FOO", "2");
el.getAttribute("foo"); // =&gt; "2"
el.getAttribute("FOO"); // =&gt; "2"
</code></pre>

Moreover, you can’t have uppercased and lowercased attributes with the same name. But you can have both on a JavaScript object, because <strong>JavaScript is case-sensitive</strong>:

<pre><code class="language-javascript">
var obj = {foo: "1", FOO: "2"};
obj.foo; // =&gt; "1"
obj.FOO; // =&gt; "2"
</code></pre>

Some time ago, I found that IE 8 supports the deprecated <a href="https://msdn.microsoft.com/en-us/library/ie/ms536739(v=vs.85).aspx">legacy argument <code>lFlags</code></a> for attribute methods, which allows you to change attributes in a case-sensitive manner:
<blockquote>
<ul>
 	<li><code>lFlags</code> [in, optional]
<ul>
 	<li>Type: Integer</li>
 	<li>Integer that specifies whether to use a case-sensitive search to locate the attribute.</li>
</ul>
</li>
</ul>
</blockquote>

Remember that the infinite recursion happens in IE 8 because the browser is trying to update the attribute with the same name and therefore triggers the setter function over and over again. What if we use the <code>lFlags</code> argument to get and set the <strong>uppercased attribute value</strong>:

<pre><code class="language-javascript">
// Defining the "foo" property but using the "FOO" attribute
Object.defineProperty(element, "foo", {
  get: function() {
	return this.getAttribute("FOO", 1);
  },
  set: function(value) {
    // No infinite recursion!
    this.setAttribute("FOO", value, 1);
  }
});
</code></pre>

As you might expect, IE 8 updates the uppercased field <code>FOO</code> on the JavaScript object, and the setter function does not trigger a recursion. Moreover, the uppercased attributes work with CSS too — as we stated in the beginning, that parser is case-insensitive.</p>

## Polyfill For The `open` Attribute

Now we can define an <code>open</code> property that <strong>works in every browser:</strong>

<pre><code class="language-javascript">
var attrName = document.addEventListener ? "open" : "OPEN";

Object.defineProperty(details, "open", {
  get: function() {
    var attrValue = this.getAttribute(attrName, 1);
    attrValue = String(attrValue).toLowerCase();
    // Handle boolean attribute value
    return attrValue === "" || attrValue === "open";
  }
  set: function(value) {
    if (this.open !== value) {
      console.log("firing toggle event");
    }

    if (value) {
      this.setAttribute(attrName, "", 1);
    } else {
      this.removeAttribute(attrName, 1);
    }
  }
});
</code></pre>

Check how it works:

<pre><code class="language-javascript">
details.open = true;
// =&gt; logs "firing toggle event"
details.hasAttribute("open"); // =&gt; true
details.open = false;
// =&gt; logs "firing toggle event"
details.hasAttribute("open"); // =&gt; false
</code></pre>

Excellent! Now let’s do similar calls, but this time using <code>*Attribute</code> methods:

<pre><code class="language-javascript">
details.setAttribute("open", "");
// =&gt; silence, but fires toggle event in Chrome and Safari
details.removeAttribute("open");
// =&gt; silence, but fires toggle event in Chrome and Safari
</code></pre>

The reason for such behavior is that the <strong>relationship between the <code>open</code> property and the attribute should be bidirectional</strong>. Every time the attribute is modified, the <code>open</code> property should reflect the change, and vice versa.

The simplest cross-browser solution I’ve found for this issue is to override the attribute methods on the target element and invoke the setters manually. This avoids bugs and the performance penalty of legacy <a href="https://msdn.microsoft.com/en-us/library/ie/ms536956(v=vs.85).aspx"><code>propertychange</code></a> and <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Mutation_events"><code>DOMAttrModified</code></a> events. Modern browsers <a href="https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver">support <code>MutationObservers</code></a>, but that doesn’t cover our browser scope.</p>

## Final Implementation

Obviously, walking through all of the steps above when defining a new attribute for a DOM element wouldn’t make sense. We need a utility function for that which hides cross-browser quirks and complexity. I’ve added such a function, named <a href="https://chemerisuk.github.io/better-dom/$Element.html#defineAttribute"><code>defineAttribute</code></a>, in better-dom.

The first argument is the name of the property or attribute, and the second is the <code>get</code> and <code>set</code> object. The getter function takes the attribute’s value as the first argument. The setter function accepts the property’s value, and the returned statement is used to update the attribute. Such a syntax allows us to hide the trick for IE 8 where an uppercased attribute name is used behind the scenes:

<pre><code class="language-javascript">
constructor: function() {
  …
  this.defineAttribute("open", {
    get: this.doGetOpen,
    set: this.doSetOpen
  });
},
doGetOpen: function(attrValue) {
  attrValue = String(attrValue).toLowerCase();
  return attrValue === "" || attrValue === "open";
},
doSetOpen: function(propValue) {
  if (this.get("open") !== propValue) {
    this.fire("toggle");
  }
  // Adding or removing boolean attribute "open"
  return propValue ? "" : null;
}
</code></pre>

Having a true polyfill for the <code>open</code> attribute simplifies our manipulation of the <code>&lt;details&gt;</code> element’s state. Again, this <strong>API is framework-agnostic</strong>:

<pre><code class="language-javascript">
// You can use better-dom…
DOM.find("details").set("open", false);

// or any other DOM library, like jQuery…
$("details").prop("open", true);

// or even vanilla DOM.
document.querySelector("details").open = false;
</code></pre>

## Notes On Styling

The CSS part of the polyfill is simpler. It has some basic style rules:

<pre><code class="language-css">
summary:first-child ~ * {
  display: none;
}

details[open] &gt; * {
  display: block;
}

/*  Hide native indicator and use pseudo-element instead */
summary::-webkit-details-marker {
  display: none;
}
</code></pre>

I didn’t want to introduce any extra elements in the markup, so obvious choice is to style the <code>::before</code> pseudo-element. This pseudo-element is used to indicate the current state of <code>&lt;details&gt;</code> (according to whether it is open or not). But IE 8 has some quirks, as usual — namely, with updating the pseudo-element state. I got it to work properly only by changing the <code>content</code> property’s value itself:

<pre><code class="language-css">
details:before {
  content: '\25BA';
  …
}

details[open]:before {
  content: '\25BC';
}
</code></pre>

For other browsers, the zero-border trick will draw a font-independent CSS triangle. With a double-colon syntax for the <code>::before</code> pseudo-element, we can apply rules to IE 9 and above:

<pre><code class="language-css">
details::before {
  content: ’;
  width: 0;
  height: 0;
  border: solid transparent;
  border-left-color: inherit;
  border-width: 0.25em 0.5em;
  …
  transform: rotate(0deg) scale(1.5);
}

details[open]::before {
  content: ’;
  transform: rotate(90deg) scale(1.5);
}
</code></pre>

The final enhancement is a small transition on the triangle. Unfortunately, Safari does not apply it for some reason (perhaps a bug), but it degrades well by ignoring the transition completely:

<pre><code class="language-css">
details::before {
  …
  transition: transform 0.15s ease-out;
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e840da6-2050-44ff-b46e-a8c92fb02a83/4-details-element-animation.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e840da6-2050-44ff-b46e-a8c92fb02a83/4-details-element-animation.gif" alt="4-details-element-animation" width="357" height="184" /></a><figcaption>A sample animation for the toggle triangle</figcaption></figure>

## Putting It All Together

Some time ago, I started using transpilers in my projects, and they are great. Transpilers enhance source files. You can even code in a completely different language, like CoffeeScript instead of JavaScript or LESS instead of CSS etc. However, my intention in using them is to decrease unnecessary noise in the source code and to learn new features in the near future. That’s why transpilers do not go against any standards in my projects — I’m just using some extra ECMAScript 6 (ES6) stuff and CSS post-processors (<a href="https://github.com/postcss/autoprefixer">Autoprefixer</a> being the main one).

Also, to speak about bundling, I quickly found that distributing <code>*.css</code> files along with <code>*.js</code> is slightly annoying. In searching for a solution, I found <a href="https://www.html5rocks.com/en/tutorials/webcomponents/imports/">HTML Imports</a>, which aims to solve this kind of problem in the future. At present, the feature has relatively <a href="https://caniuse.com/#feat=imports">weak browser support</a>. And, frankly, bundling all of that stuff into a single HTML file is not ideal.

So, I built my own approach for bundling: better-dom has a function, <a href="https://chemerisuk.github.io/better-dom/DOM.html#importStyles"><code>DOM.importStyles</code></a>, that allows you to import CSS rules on a web page. This function has been in the library since the beginning because <code>DOM.extend</code> uses it internally. Since I use better-dom and transpilers in my code anyway, I created a simple gulp task:

<pre><code class="language-javascript">
gulp.task("compile", ["lint"], function() {
  var jsFilter = filter("*.js");
  var cssFilter = filter("*.css");

  return gulp.src(["src/*.js", "src/*.css"])
    .pipe(cssFilter)
    .pipe(postcss([autoprefixer, csswring, …]))
     // need to escape some symbols
    .pipe(replace(/\\|"/g, "\\$&amp;"))
     // and convert CSS rules into JavaScript function calls
    .pipe(replace(/([^{]+)\{([^}]+)\}/g,
      "DOM.importStyles(\"$1\", \"$2\");\n"))
    .pipe(cssFilter.restore())
    .pipe(jsFilter)
    .pipe(es6transpiler())
    .pipe(jsFilter.restore())
    .pipe(concat(pkg.name + ".js"))
    .pipe(gulp.dest("build/"));
});
</code></pre>

To keep it simple, I didn’t put in any optional steps or dependency declarations (see the <a href="https://github.com/chemerisuk/better-dom-boilerplate/blob/master/gulpfile.js#L34">full source code</a>). In general, the compilation task contains the following steps:

1.  Apply Autoprefixer to the CSS.
2.  Optimize the CSS, and transform it into the sequence of `DOM.importStyles` calls.
3.  Apply ES6 transpilers to JavaScript.
4.  Concatenate both outputs to a `*.js` file.</p>

## Support For `open` Property

If you try the code below in browsers that support <code>&lt;details&gt;</code> natively and in others that don’t, you’ll get different results:

<pre><code class="language-javascript">
details.open = true;
// &lt;details&gt; changes state in Chrome and Safari
details.open = false;
// &lt;details&gt; state changes back in Chrome and Safari
</code></pre>

In Chrome and Safari, changing the value of <code>open</code> triggers the addition or removal of the attribute. Other browsers do not respond to this because they do not support the <code>open</code> property on the <code>&lt;details&gt;</code> element.

Properties are different from simple values. They have a pair of getter and setter functions that are invoked every time you read or assign a new value to the field. And JavaScript has had an API to declare properties since version 1.5.

The good news is that one old browser we are going to use with our polyfill, Internet Explorer (IE) 8, has <em>partial</em> support for the <code>Object.defineProperty</code> function. The limitation is that the function works only on DOM elements. But that is exactly what we need, right?

There is a problem, though. If you try to set an attribute with the same name in the setter function in IE 8, then the browser will stack with infinite recursion and crashes. In old versions of IE, changing an attribute will trigger the change of an appropriate property and vice versa:

<pre><code class="language-javascript">
Object.defineProperty(element, "foo", {
  …
  set: function(value) {
    // The line below triggers infinite recursion in IE 8.
    this.setAttribute("foo", value);
  }
});
</code></pre>

So you can’t modify the property without changing an attribute there. This limitation has prevented developers from using the <code>Object.defineProperty</code> for quite a long time.

The good news is that I’ve found a solution.</p>

## Fix For Infinite Recursion In IE 8

Before describing the solution, I’d like to give some background on one feature of the HTML and CSS parser in browsers. In case you weren’t aware, these <strong>parsers are case-insensitive</strong>. For example, the rules below will produce the same result (i.e. a base red for the text on the page):

<pre><code class="language-css">
body { color: red; }
/* The rule below will produce the same result. */
BODY { color: red; }
</code></pre>

The same goes for attributes:

<pre><code class="language-javascript">
el.setAttribute("foo", "1");
el.setAttribute("FOO", "2");
el.getAttribute("foo"); // =&gt; "2"
el.getAttribute("FOO"); // =&gt; "2"
</code></pre>

Moreover, you can’t have uppercased and lowercased attributes with the same name. But you can have both on a JavaScript object, because <strong>JavaScript is case-sensitive</strong>:

<pre><code class="language-javascript">
var obj = {foo: "1", FOO: "2"};
obj.foo; // =&gt; "1"
obj.FOO; // =&gt; "2"
</code></pre>

Some time ago, I found that IE 8 supports the deprecated <a href="https://msdn.microsoft.com/en-us/library/ie/ms536739(v=vs.85).aspx">legacy argument <code>lFlags</code></a> for attribute methods, which allows you to change attributes in a case-sensitive manner:
<blockquote>
<ul>
 	<li><code>lFlags</code> [in, optional]
<ul>
 	<li>Type: Integer</li>
 	<li>Integer that specifies whether to use a case-sensitive search to locate the attribute.</li>
</ul>
</li>
</ul>
</blockquote>

Remember that the infinite recursion happens in IE 8 because the browser is trying to update the attribute with the same name and therefore triggers the setter function over and over again. What if we use the <code>lFlags</code> argument to get and set the <strong>uppercased attribute value</strong>:

<pre><code class="language-javascript">
// Defining the "foo" property but using the "FOO" attribute
Object.defineProperty(element, "foo", {
  get: function() {
	return this.getAttribute("FOO", 1);
  },
  set: function(value) {
    // No infinite recursion!
    this.setAttribute("FOO", value, 1);
  }
});
</code></pre>

As you might expect, IE 8 updates the uppercased field <code>FOO</code> on the JavaScript object, and the setter function does not trigger a recursion. Moreover, the uppercased attributes work with CSS too — as we stated in the beginning, that parser is case-insensitive.</p>

## Polyfill For The `open` Attribute

Now we can define an <code>open</code> property that <strong>works in every browser:</strong>

<pre><code class="language-javascript">
var attrName = document.addEventListener ? "open" : "OPEN";

Object.defineProperty(details, "open", {
  get: function() {
    var attrValue = this.getAttribute(attrName, 1);
    attrValue = String(attrValue).toLowerCase();
    // Handle boolean attribute value
    return attrValue === "" || attrValue === "open";
  }
  set: function(value) {
    if (this.open !== value) {
      console.log("firing toggle event");
    }

    if (value) {
      this.setAttribute(attrName, "", 1);
    } else {
      this.removeAttribute(attrName, 1);
    }
  }
});
</code></pre>

Check how it works:

<pre><code class="language-javascript">
details.open = true;
// =&gt; logs "firing toggle event"
details.hasAttribute("open"); // =&gt; true
details.open = false;
// =&gt; logs "firing toggle event"
details.hasAttribute("open"); // =&gt; false
</code></pre>

Excellent! Now let’s do similar calls, but this time using <code>*Attribute</code> methods:

<pre><code class="language-javascript">
details.setAttribute("open", "");
// =&gt; silence, but fires toggle event in Chrome and Safari
details.removeAttribute("open");
// =&gt; silence, but fires toggle event in Chrome and Safari
</code></pre>

The reason for such behavior is that the <strong>relationship between the <code>open</code> property and the attribute should be bidirectional</strong>. Every time the attribute is modified, the <code>open</code> property should reflect the change, and vice versa.

The simplest cross-browser solution I’ve found for this issue is to override the attribute methods on the target element and invoke the setters manually. This avoids bugs and the performance penalty of legacy <a href="https://msdn.microsoft.com/en-us/library/ie/ms536956(v=vs.85).aspx"><code>propertychange</code></a> and <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Mutation_events"><code>DOMAttrModified</code></a> events. Modern browsers <a href="https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver">support <code>MutationObservers</code></a>, but that doesn’t cover our browser scope.</p>

## Final Implementation

Obviously, walking through all of the steps above when defining a new attribute for a DOM element wouldn’t make sense. We need a utility function for that which hides cross-browser quirks and complexity. I’ve added such a function, named <a href="https://chemerisuk.github.io/better-dom/$Element.html#defineAttribute"><code>defineAttribute</code></a>, in better-dom.

The first argument is the name of the property or attribute, and the second is the <code>get</code> and <code>set</code> object. The getter function takes the attribute’s value as the first argument. The setter function accepts the property’s value, and the returned statement is used to update the attribute. Such a syntax allows us to hide the trick for IE 8 where an uppercased attribute name is used behind the scenes:

<pre><code class="language-javascript">
constructor: function() {
  …
  this.defineAttribute("open", {
    get: this.doGetOpen,
    set: this.doSetOpen
  });
},
doGetOpen: function(attrValue) {
  attrValue = String(attrValue).toLowerCase();
  return attrValue === "" || attrValue === "open";
},
doSetOpen: function(propValue) {
  if (this.get("open") !== propValue) {
    this.fire("toggle");
  }
  // Adding or removing boolean attribute "open"
  return propValue ? "" : null;
}
</code></pre>

Having a true polyfill for the <code>open</code> attribute simplifies our manipulation of the <code>&lt;details&gt;</code> element’s state. Again, this <strong>API is framework-agnostic</strong>:

<pre><code class="language-javascript">
// You can use better-dom…
DOM.find("details").set("open", false);

// or any other DOM library, like jQuery…
$("details").prop("open", true);

// or even vanilla DOM.
document.querySelector("details").open = false;
</code></pre>

## Notes On Styling

The CSS part of the polyfill is simpler. It has some basic style rules:

<pre><code class="language-css">
summary:first-child ~ * {
  display: none;
}

details[open] &gt; * {
  display: block;
}

/*  Hide native indicator and use pseudo-element instead */
summary::-webkit-details-marker {
  display: none;
}
</code></pre>

I didn’t want to introduce any extra elements in the markup, so obvious choice is to style the <code>::before</code> pseudo-element. This pseudo-element is used to indicate the current state of <code>&lt;details&gt;</code> (according to whether it is open or not). But IE 8 has some quirks, as usual — namely, with updating the pseudo-element state. I got it to work properly only by changing the <code>content</code> property’s value itself:

<pre><code class="language-css">
details:before {
  content: '\25BA';
  …
}

details[open]:before {
  content: '\25BC';
}
</code></pre>

For other browsers, the zero-border trick will draw a font-independent CSS triangle. With a double-colon syntax for the <code>::before</code> pseudo-element, we can apply rules to IE 9 and above:

<pre><code class="language-css">
details::before {
  content: ’;
  width: 0;
  height: 0;
  border: solid transparent;
  border-left-color: inherit;
  border-width: 0.25em 0.5em;
  …
  transform: rotate(0deg) scale(1.5);
}

details[open]::before {
  content: ’;
  transform: rotate(90deg) scale(1.5);
}
</code></pre>

The final enhancement is a small transition on the triangle. Unfortunately, Safari does not apply it for some reason (perhaps a bug), but it degrades well by ignoring the transition completely:

<pre><code class="language-css">
details::before {
  …
  transition: transform 0.15s ease-out;
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e840da6-2050-44ff-b46e-a8c92fb02a83/4-details-element-animation.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e840da6-2050-44ff-b46e-a8c92fb02a83/4-details-element-animation.gif" alt="4-details-element-animation" width="357" height="184" /></a><figcaption>A sample animation for the toggle triangle</figcaption></figure>

## Putting It All Together

Some time ago, I started using transpilers in my projects, and they are great. Transpilers enhance source files. You can even code in a completely different language, like CoffeeScript instead of JavaScript or LESS instead of CSS etc. However, my intention in using them is to decrease unnecessary noise in the source code and to learn new features in the near future. That’s why transpilers do not go against any standards in my projects — I’m just using some extra ECMAScript 6 (ES6) stuff and CSS post-processors (<a href="https://github.com/postcss/autoprefixer">Autoprefixer</a> being the main one).

Also, to speak about bundling, I quickly found that distributing <code>*.css</code> files along with <code>*.js</code> is slightly annoying. In searching for a solution, I found <a href="https://www.html5rocks.com/en/tutorials/webcomponents/imports/">HTML Imports</a>, which aims to solve this kind of problem in the future. At present, the feature has relatively <a href="https://caniuse.com/#feat=imports">weak browser support</a>. And, frankly, bundling all of that stuff into a single HTML file is not ideal.

So, I built my own approach for bundling: better-dom has a function, <a href="https://chemerisuk.github.io/better-dom/DOM.html#importStyles"><code>DOM.importStyles</code></a>, that allows you to import CSS rules on a web page. This function has been in the library since the beginning because <code>DOM.extend</code> uses it internally. Since I use better-dom and transpilers in my code anyway, I created a simple gulp task:

<pre><code class="language-javascript">
gulp.task("compile", ["lint"], function() {
  var jsFilter = filter("*.js");
  var cssFilter = filter("*.css");

  return gulp.src(["src/*.js", "src/*.css"])
    .pipe(cssFilter)
    .pipe(postcss([autoprefixer, csswring, …]))
     // need to escape some symbols
    .pipe(replace(/\\|"/g, "\\$&amp;"))
     // and convert CSS rules into JavaScript function calls
    .pipe(replace(/([^{]+)\{([^}]+)\}/g,
      "DOM.importStyles(\"$1\", \"$2\");\n"))
    .pipe(cssFilter.restore())
    .pipe(jsFilter)
    .pipe(es6transpiler())
    .pipe(jsFilter.restore())
    .pipe(concat(pkg.name + ".js"))
    .pipe(gulp.dest("build/"));
});
</code></pre>

To keep it simple, I didn’t put in any optional steps or dependency declarations (see the <a href="https://github.com/chemerisuk/better-dom-boilerplate/blob/master/gulpfile.js#L34">full source code</a>). In general, the compilation task contains the following steps:

1.  Apply Autoprefixer to the CSS.
2.  Optimize the CSS, and transform it into the sequence of `DOM.importStyles` calls.
3.  Apply ES6 transpilers to JavaScript.
4.  Concatenate both outputs to a `*.js` file.

And it works! I have transpilers that make my code clearer, and the only output is a <strong>single JavaScript file</strong>. Another advantage is that, when JavaScript is disabled, those style rules are completely ignored. For a polyfill like this, such behavior is desirable.</p>

## Closing Thoughts

As you can see, developing a polyfill is not the easiest challenge. On the other hand, the solution can be used for a relatively long time: standards do not change often and have been discussed at length behind the scenes. Also everyone is using the same language and is connecting with the same APIs which is a great thing.

With the common logic moved into utility functions, the source code is not very complex. This means that, at present, we really lack advanced tools to make robust polyfills that work close to native implementations (or better!). And I don’t see good libraries for this yet, unfortunately.

Libraries such as jQuery, Prototype and MooTools are all about providing extra sugar for working with the DOM. While sugar is great, we also need more utility functions to build more robust and unobtrusive polyfills. Without them, we might end up with a ton of plugins that are hard to integrate in our projects. May be it's time to move into this direction?

Another technique that has arisen recently is <a href="https://webcomponents.org">Web Components</a>. I’m really excited by tools like the shadow DOM, but I’m not sure if <a href="https://w3c.github.io/webcomponents/spec/custom/">custom elements</a> are the future of web development. Moreover, custom elements can introduce new problems if everyone starts creating their own custom tags for common uses. My point is that <strong>we need to learn (and try to improve) the standards first before introducing a new HTML element</strong>. Fortunately, I’m not alone in this; <a href="https://adactio.com/journal/7431">Jeremy Keith, for one, shares a similar view</a>.

Don’t get me wrong. Custom elements are a nice feature, and they definitely have use cases in some areas. I look forward to them being implemented in all browsers. I’m just not sure if they’re a silver bullet for all of our problems.

To reiterate, I'd encourage creating more robust and unobtrusive polyfills. And we need to build more advanced tools to make that happen more easily. The example with <code>&lt;details&gt;</code> shows that achieving such a goal today is possible. And I believe this direction is future-proof and the one we need to move in.

{{< signature "al" >}}


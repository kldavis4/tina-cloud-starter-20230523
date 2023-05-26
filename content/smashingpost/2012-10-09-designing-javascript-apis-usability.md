---
title: How To Design Better JavaScript APIs
slug: designing-javascript-apis-usability
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7e25b926-38ab-4f09-9d55-88df28847ff3/illu-apis.jpg'
date: 2012-10-09T09:34:39.000Z
author: rodney-rehm
description: >-
  At some point or another, you will find yourself writing JavaScript code that
  exceeds the couple of lines from a jQuery plugin. Your code will do a whole
  lot of things; it will (ideally) be used by many people who will approach your
  code differently. They have different needs, knowledge and expectations.
categories:
  - Coding
  - JavaScript
  - Programming
---
At some point or another, you will find yourself writing JavaScript code that exceeds the couple of lines from a jQuery plugin. Your code will do a whole lot of things; it will (ideally) be used by many people who will approach your code differently. They have different needs, knowledge and expectations.

<img title="Time Spent On Creating Vs Time Spent On Using" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3f3241bf-8546-4ff1-b7b0-64cdf4f821a8/pie-chart.jpg" alt="Time Spent On Creating Vs Time Spent On Using" />

This article covers the most important things that you will need to consider before and while writing your own utilities and libraries. We'll focus on how to make your code <em>accessible</em> to other developers. A couple of topics will be touching upon jQuery for demonstration, yet this article is neither about jQuery nor about writing plugins for it.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [A Beginner’s Guide To jQuery-Based JSON API Clients](https://www.smashingmagazine.com/2012/02/beginners-guide-jquery-based-json-api-clients/)
*   [Accessibility APIs: A Key To Web Accessibility](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/)
*   [<span class="headline">Writing Fast, Memory-Efficient JavaScript</span>](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)
*   [7 JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)

{{% feature-panel %}}

Peter Drucker once said: "The computer is a moron." Don't write code for morons, write for humans! Let's dive into <strong>designing the APIs that developers will love using</strong>.</p>

### Table of Contents

*   [Fluent Interface](#fluent-interface)
*   [Consistency](#consistency)
*   [Handling Arguments](#handling-arguments)
*   [Extensibility](#extensibility)
*   [Hooks](#hooks)
*   [Generating Accessors](#generating-accessors)
*   [The Reference Horror](#the-reference-horror)
*   [The Continuation Problem](#the-continuation-problem)
*   [Handling Errors](#handling-errors)
*   [Going Asynchronous](#going-asynchronous)
*   [Debugging Fluent Interfaces](#debugging-fluent-interfaces)
*   [Documenting APIs](#documenting-apis)
*   [Conclusion](#conclusion)

## Fluent Interface

The <a href="https://en.wikipedia.org/wiki/Fluent_interface#JavaScript">Fluent Interface</a> is often referred to as <em>Method Chaining</em> (although that's only half the truth). To beginners it looks like the <em>jQuery style</em>. While I believe the API style was a key ingredient in jQuery's success, it wasn't invented by them — credits seem to go to Martin Fowler who <a href="https://martinfowler.com/bliki/FluentInterface.html">coined the term</a> back in 2005, roughly a year before jQuery was released. Fowler only gave the thing a name, though — Fluent Interfaces have been around for a much longer time.

Aside from major simplifications, jQuery offered to even out severe browser differences. It has always been the <em>Fluent Interface</em> that I have loved most about this extremely successful library. I have come to enjoy this particular API style so much that it became immediately apparent that I wanted this style for <a href="https://medialize.github.com/URI.js/">URI.js</a>, as well. While tuning up the URI.js API, I constantly looked through the jQuery source to find the little tricks that would make my implementation as simple as possible. I found out that I was not alone in this endeavor. <a href="https://twitter.com/leaverou">Lea Verou</a> created <a href="https://lea.verou.me/chainvas/">chainvas</a> — a tool to wrap regular getter/setter APIs into sweet fluent interfaces. Underscore's <a href="https://underscorejs.org/#chain"><code>_.chain()</code></a> does something similar. In fact, most of the newer generation libraries support method chaining.</p>

### Method Chaining

The general idea of <a href="https://en.wikipedia.org/wiki/Method_chaining">Method Chaining</a> is to achieve code that is as fluently readable as possible and thus quicker to understand. With <em>Method Chaining</em> we can form code into sentence-like sequences, making code easy to read, while reducing noise in the process:

<pre><code class="language-javascript">// regular API calls to change some colors and add an event-listener
var elem = document.getElementById("foobar");
elem.style.background = "red";
elem.style.color = "green";
elem.addEventListener('click', function(event) {
  alert("hello world!");
}, true);

// (imaginary) method chaining API
DOMHelper.getElementById('foobar')
  .setStyle("background", "red")
  .setStyle("color", "green")
  .addEvent("click", function(event) {
    alert("hello world");
  });</code></pre>

Note how we didn't have to assign the element's reference to a variable and repeat that over and over again.</p>

### Command Query Separation

<a href="https://en.wikipedia.org/wiki/Command-query_separation">Command and Query Separation</a> (CQS) is a concept inherited from imperative programming. Functions that change the state (internal values) of an object are called <em>commands</em>, functions that retrieve values are called <em>queries</em>. In principle, queries return data, commands change the state — but neither does both. This concept is one of the foundations of the everyday getter and setter methods we see in most libraries today. Since <em>Fluent Interfaces</em> return a self-reference for chaining method calls, we're already breaking the rule for <em>commands</em>, as they are not supposed to return anything. On top of this (easy to ignore) trait, we (deliberately) break with this concept to keep APIs as simple as possible. An excellent example for this practice is jQuery's <a href="https://api.jquery.com/css/"><code>css()</code></a> method:

<pre><code class="language-javascript">var $elem = jQuery("#foobar");

// CQS - command
$elem.setCss("background", "green");
// CQS - query
$elem.getCss("color") === "red";

// non-CQS - command
$elem.css("background", "green");
// non-CQS - query
$elem.css("color") === "red";</code></pre>

As you can see, getter and setter methods are merged into a single method. The action to perform (namely, <em>query</em> or <em>command</em>) is decided by the amount of arguments passed to the function, rather than by which function was called. This allows us to expose fewer methods and in turn type less to achieve the same goal.

It is not necessary to compress getters and setters into a single method in order to create a fluid interface — it boils down to personal preference. Your documentation should be very clear with the approach you've decided on. I will get into documenting APIs later, but at this point I would like to note that multiple function signatures may be harder to document.</p>

### Going Fluent

While method chaining already does most of the job for going fluent, you're not off the hook yet. To illustrate the next step of <em>fluent</em>, we're pretending to write a little library handling date intervals. An interval starts with a date and ends with a date. A date is not necessarily connected to an interval. So we come up with this simple constructor:

<pre><code class="language-javascript">// create new date interval
var interval = new DateInterval(startDate, endDate);
// get the calculated number of days the interval spans
var days = interval.days();</code></pre>

While this looks right at first glance, this example shows what's wrong:

<pre><code class="language-javascript">var startDate = new Date(2012, 0, 1);
var endDate = new Date(2012, 11, 31)
var interval = new DateInterval(startDate, endDate);
var days = interval.days(); // 365</code></pre>

We're writing out a whole bunch of variables and stuff we probably won't need. A nice solution to the problem would be to add a function to the Date object in order to return an interval:

<pre><code class="language-javascript">// DateInterval creator for fluent invocation
Date.prototype.until = function(end) {

  // if we weren't given a date, make one
  if (!(end instanceof Date)) {
    // create date from given arguments,
    // proxy the constructor to allow for any parameters
    // the Date constructor would've taken natively
    end = Date.apply(null,
      Array.prototype.slice.call(arguments, 0)
    );
  }

  return new DateInterval(this, end);
};</code></pre>

Now we can create that <code>DateInterval</code> in a fluent, easy to type-and-read fashion:

<pre><code class="language-javascript">var startDate = new Date(2012, 0, 1);
var interval = startDate.until(2012, 11, 31);
var days = interval.days(); // 365

// condensed fluent interface call:
var days = (new Date(2012, 0, 1))
  .until(2012, 11, 31) // returns DateInterval instance
  .days(); // 365</code></pre>

As you can see in this last example, there are less variables to declare, less code to write, and the operation almost reads like an english sentence. With this example you should have realized that method chaining is only a part of a fluent interface, and as such, the terms are not synonymous. To provide fluency, you have to think about code streams — where are you coming from and where you are headed.

This example illustrated fluidity by extending a native object with a custom function. This is as much a religion as using semicolons or not. In Extending built-in native objects. Evil or not? <a href="https://twitter.com/kangax">kangax</a> explains the ups and downs of this approach. While everyone has their opinions about this, the one thing everybody agrees on is keeping things consistent. As an aside, even the followers of "Don't pollute native objects with custom functions" would probably let the following, still somewhat fluid trick slide:

<pre><code class="language-javascript">String.prototype.foo = function() {
  return new Foo(this);
}

"I'm a native object".foo()
  .iAmACustomFunction();</code></pre>

With this approach your functions are still within your namespace, but made accessible through another object. Make sure your equivalent of <code>.foo()</code> is a non-generic term, something highly unlikely to collide with other APIs. Make sure you provide proper <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Object/valueOf"><code>.valueOf()</code></a> and <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Object/toString"><code>.toString()</code></a> methods to convert back to the original primitive types.

## Consistency

<a href="https://twitter.com/jaffathecake">Jake Archibald</a> once had a slide defining <em>Consistency</em>. It simply read <a href="https://www.slideshare.net/slideshow/embed_code/5426258?startSlide=59"><em>Not PHP</em></a>. Do. Not. Ever. Find yourself naming functions like <em>str_repeat()</em>, <em>strpos()</em>, <em>substr()</em>. Also, don't ever shuffle around positions of arguments. If you declared <code>find_in_array(haystack, needle)</code> at some point, introducing <code>findInString(needle, haystack)</code> will invite an angry mob of zombies to rise from their graves to hunt you down and force you to write delphi for the rest of your life!

### Naming Things

<blockquote>"There are only two hard problems in computer science: cache-invalidation and naming things."

— Phil Karlton</blockquote>

I've been to numerous talks and sessions trying to teach me the finer points of naming things. I haven't left any of them without having heard the above said quote, nor having learnt how to actually name things. My advice boils down to <em>keep it short but descriptive and go with your gut</em>. But most of all, keep it consistent.

The <code>DateInterval</code> example above introduced a method called <code>until()</code>. We could have named that function <code>interval()</code>. The latter would have been closer to the returned value, while the former is more <em>humanly readable</em>. Find a line of wording you like and stick with it. Consistency is 90% of what matters. Choose one style and keep that style — even if you find yourself disliking it at some point in the future.</p>

## Handling Arguments

<img title="Good Intentions" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e67e035d-134e-4752-820a-80b9b3d2b376/good-intention.jpg" alt="Good Intentions" />

How your methods accept data is more important than making them chainable. While method chaining is a pretty generic thing that you can easily make your code do, handling arguments is not. You'll need to think about how the methods you provide are most likely going to be used. Is code that uses your API likely to repeat certain function calls? Why are these calls repeated? How could your API help the developer to reduce the noise of repeating method calls?

jQuery's <a href="https://api.jquery.com/css/"><code>css()</code></a> method can set styles on a DOM element:

<pre><code class="language-javascript">jQuery("#some-selector")
  .css("background", "red")
  .css("color", "white")
  .css("font-weight", "bold")
  .css("padding", 10);</code></pre>

There's a pattern here! Every method invocation is naming a style and specifying a value for it. This calls for having the method accept a map:

<pre><code class="language-javascript">jQuery("#some-selector").css({
  "background" : "red",
  "color" : "white",
  "font-weight" : "bold",
  "padding" : 10
});</code></pre>

jQuery's <a href="https://api.jquery.com/on/"><code>on()</code></a> method can register event handlers. Like <code>css()</code> it accepts a map of events, but takes things even further by allowing a single handler to be registered for multiple events:

<pre><code class="language-javascript">// binding events by passing a map
jQuery("#some-selector").on({
  "click" : myClickHandler,
  "keyup" : myKeyupHandler,
  "change" : myChangeHandler
});

// binding a handler to multiple events:
jQuery("#some-selector").on("click keyup change", myEventHandler);</code></pre>

You can offer the above function signatures by using the following <em>method pattern</em>:

<pre><code class="language-javascript">DateInterval.prototype.values = function(name, value) {
  var map;

  if (jQuery.isPlainObject(name)) {
    // setting a map
    map = name;
  } else if (value !== undefined) {
    // setting a value (on possibly multiple names), convert to map
    keys = name.split(" ");
    map = {};
    for (var i = 0, length = keys.length; i &lt; length; i++) {
      map[keys[i]] = value;
    }
  } else if (name === undefined) {
    // getting all values
    return this.values;
  } else {
    // getting specific value
    return this.values[name];
  }

  for (var key in map) {
    this.values[name] = map[key];
  }

  return this;
};</code></pre>

If you are working with collections, think about what you can do to reduce the number of loops an API user would probably have to make. Say we had a number of <code>&lt;input&gt;</code> elements for which we want to set the default value:

<pre><code class="language-markup tmp-html">&lt;input type="text" value="" data-default="foo"&gt;
&lt;input type="text" value="" data-default="bar"&gt;
&lt;input type="text" value="" data-default="baz"&gt;</code></pre>

We'd probably go about this with a loop:

<pre><code class="language-javascript">jQuery("input").each(function() {
  var $this = jQuery(this);
  $this.val($this.data("default"));
});</code></pre>

What if we could bypass that method with a simple callback that gets applied to each <code>&lt;input&gt;</code> in the collection? jQuery developers have thought of that and allow us to write less™:

<pre><code class="language-javascript">jQuery("input").val(function() {
  return jQuery(this).data("default");
});</code></pre>

It's the little things like accepting maps, callbacks or serialized attribute names, that make using your API not only cleaner, but more comfortable and efficient to use. Obviously not all of your APIs' methods will benefit from this method pattern — it's up to you to decide where all this makes sense and where it is just a waste of time. Try to be as consistent about this as humanly possible. <em>Reduce the need for boilerplate code with the tricks shown above and people will invite you over for a drink.</em>

### Handling Types

Whenever you define a function that will accept arguments, you decide what data that function accepts. A function to calculate the number of days between two dates could look like:

<pre><code class="language-javascript">DateInterval.prototype.days = function(start, end) {
  return Math.floor((end - start) / 86400000);
};</code></pre>

As you can see, the function expects numeric input — a millisecond timestamp, to be exact. While the function does what we intended it to do, it is not very versatile. What if we're working with <code>Date</code> objects or a string representation of a date? Is the user of this function supposed to cast data all the time? No! Simply verifying the input and casting it to whatever we need it to be should be done in a central place, not cluttered throughout the code using our API:

<pre><code class="language-javascript">DateInterval.prototype.days = function(start, end) {
  if (!(start instanceof Date)) {
    start = new Date(start);
  }
  if (!(end instanceof Date)) {
    end = new Date(end);
  }

  return Math.floor((end.getTime() - start.getTime()) / 86400000);
};</code></pre>

By adding these six lines we've given the function the power to accept a Date object, a numeric timestamp, or even a string representation like <code>Sat Sep 08 2012 15:34:35 GMT+0200 (CEST)</code>. We do not know how and for what people are going to use our code, but with a little foresight, we can make sure there is little pain with integrating our code.

The experienced developer can spot another problem in the example code. We're assuming <code>start</code> comes before <code>end</code>. If the API user accidentally swapped the dates, he'd be given a negative value for the number of days between <code>start</code> and <code>end</code>. Stop and think about these situations carefully. If you've come to the conclusion that a negative value doesn't make sense, fix it:

<pre><code class="language-javascript">DateInterval.prototype.days = function(start, end) {
  if (!(start instanceof Date)) {
    start = new Date(start);
  }
  if (!(end instanceof Date)) {
    end = new Date(end);
  }

  return Math.abs(Math.floor((end.getTime() - start.getTime()) / 86400000));
};</code></pre>

JavaScript allows type casting a number of ways. If you're dealing with primitives (string, number, boolean) it can get as simple (as in "short") as:

<pre><code class="language-javascript">function castaway(some_string, some_integer, some_boolean) {
  some_string += "";
  some_integer += 0; // parseInt(some_integer, 10) is the safer bet
  some_boolean = !!some_boolean;
}</code></pre>

I'm not advocating you to do this everywhere and at all times. But these innocent looking lines may save time and some suffering while integrating your code.</p>

### Treating `undefined` as an Expected Value

There will come a time when <code>undefined</code> is a value that your API actually expects to be given for setting an attribute. This might happen to "unset" an attribute, or simply to gracefully handle bad input, making your API more robust. To identify if the value <code>undefined</code> has actually been passed by your method, you can check the <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Functions_and_function_scope/arguments"><code>arguments</code></a> object:

<pre><code class="language-javascript">function testUndefined(expecting, someArgument) {
  if (someArgument === undefined) {
    console.log("someArgument was undefined");
  }
  if (arguments.length &gt; 1) {
    console.log("but was actually passed in");
  }
}

testUndefined("foo");
// prints: someArgument was undefined
testUndefined("foo", undefined);
// prints: someArgument was undefined, but was actually passed in</code></pre>

### Named Arguments

<pre><code class="language-javascript">event.initMouseEvent(
  "click", true, true, window,
  123, 101, 202, 101, 202,
  true, false, false, false,
  1, null);</code></pre>

The function signature of <a href="https://developer.mozilla.org/en-US/docs/DOM/event.initMouseEvent">Event.initMouseEvent</a> is a nightmare come true. There is no chance any developer will remember what that <code>1</code> (second to last parameter) means without looking it up in the documentation. No matter how good your documentation is, do what you can so people don't have to look things up!

### How Others Do It

Looking beyond our beloved language, we find Python knowing a concept called <a href="https://www.diveintopython.net/power_of_introspection/optional_arguments.html">named arguments</a>. It allows you to declare a function providing default values for arguments, allowing your attributed names to be stated in the calling context:

<pre><code class="language-javascript">function namesAreAwesome(foo=1, bar=2) {
  console.log(foo, bar);
}

namesAreAwesome();
// prints: 1, 2

namesAreAwesome(3, 4);
// prints: 3, 4

namesAreAwesome(foo=5, bar=6);
// prints: 5, 6

namesAreAwesome(bar=6);
// prints: 1, 6</code></pre>

Given this scheme, initMouseEvent() could've looked like a self-explaining function call:

<pre><code class="language-javascript">event.initMouseEvent(
  type="click",
  canBubble=true,
  cancelable=true,
  view=window,
  detail=123,
  screenX=101,
  screenY=202,
  clientX=101,
  clientY=202,
  ctrlKey=true,
  altKey=false,
  shiftKey=false,
  metaKey=false,
  button=1,
  relatedTarget=null);</code></pre>

In JavaScript this is not possible today. While "the next version of JavaScript" (frequently called ES.next, ES6, or Harmony) will have <a href="https://wiki.ecmascript.org/doku.php?id=harmony:parameter_default_values">default parameter values</a> and <a href="https://wiki.ecmascript.org/doku.php?id=harmony:rest_parameters">rest parameters</a>, there is still no sign of named parameters.</p>

### Argument Maps

JavaScript not being Python (and ES.next being light years away), we're left with fewer choices to overcome the obstacle of "argument forests". jQuery (and pretty much every other decent API out there) chose to work with the concept of "option objects". The signature of <a href="https://api.jquery.com/jquery.ajax/">jQuery.ajax()</a> provides a pretty good example. Instead of accepting numerous arguments, we only accept an object:

<pre><code class="language-javascript">function nightmare(accepts, async, beforeSend, cache, complete, /* and 28 more */) {
  if (accepts === "text") {
    // prepare for receiving plain text
  }
}

function dream(options) {
  options = options || {};
  if (options.accepts === "text") {
    // prepare for receiving plain text
  }
}</code></pre>

Not only does this prevent insanely long function signatures, it also makes calling the function more descriptive:

<pre><code class="language-javascript">nightmare("text", true, undefined, false, undefined, /* and 28 more */);

dream({
  accepts: "text",
  async: true,
  cache: false
});</code></pre>

Also, we do not have to touch the function signature (adding a new argument) should we introduce a new feature in a later version.</p>

### Default Argument Values

<a href="https://api.jquery.com/jQuery.extend/">jQuery.extend()</a>, <a href="https://underscorejs.org/#extend">_.extend()</a> and Protoype's <a href="https://api.prototypejs.org/language/Object/extend/">Object.extend</a> are functions that let you merge objects, allowing you to throw your own preset options object into the mix:

<pre><code class="language-javascript">var default_options = {
  accepts: "text",
  async: true,
  beforeSend: null,
  cache: false,
  complete: null,
  // …
};

function dream(options) {
  var o = jQuery.extend({}, default_options, options || {});
  console.log(o.accepts);
}

// make defaults public
dream.default_options = default_options;

dream({ async: false });
// prints: "text"</code></pre>

You're earning bonus points for making the default values publicly accessible. With this, anyone can change <code>accepts</code> to "json" in a central place, and thus avoid specifying that option over and over again. Note that the example will always append <code>|| {}</code> to the initial read of the option object. This allows you to call the function without an argument given.</p>

### Good Intentions — a.k.a. "Pitfalls"

Now that you know how to be truly flexible in accepting arguments, we need to come back to an old saying:
<blockquote>"With great power comes great responsibility!"

— Voltaire</blockquote>

As with most weakly-typed languages, JavaScript does automatic casting when it needs to. A simple example is testing the truthfulness:

<pre><code class="language-javascript">var foo = 1;
var bar = true;

if (foo) {
  // yep, this will execute
}

if (bar) {
  // yep, this will execute
}</code></pre>

We're quite used to this automatic casting. We're so used to it, that we forget that although something is truthful, it may not be the boolean truth. Some APIs are so flexible they are <em>too smart</em> for their own good. Take a look at the signatures of <a href="https://api.jquery.com/toggle/">jQuery.toggle()</a>:

<pre><code class="language-javascript">.toggle( /* int */ [duration] [, /* function */  callback] )
.toggle( /* int */ [duration] [, /* string */  easing] [, /* function */ callback] )
.toggle( /* bool */ showOrHide )</code></pre>

It will take us some time decrypting why these behave <em>entirely</em> different:

<pre><code class="language-javascript">var foo = 1;
var bar = true;
var $hello = jQuery(".hello");
var $world = jQuery(".world");

$hello.toggle(foo);
$world.toggle(bar);</code></pre>

We were <em>expecting</em> to use the <code>showOrHide</code> signature in both cases. But what really happened is <code>$hello</code> doing a toggle with a <code>duration</code> of one millisecond. This is not a bug in jQuery, this is a simple case of <em>expectation not met</em>. Even if you're an experienced jQuery developer, you <em>will</em> trip over this from time to time.

You are free to add as much convenience / sugar as you like — but do not sacrifice a clean and (mostly) robust API along the way. If you find yourself providing something like this, think about providing a separate method like <code>.toggleIf(bool)</code> instead. Whatever choice you make, keep your API consistent!

## Extensibility

<img title="Developing Possibilities" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/323ab35f-f5bd-44bf-bc4d-c982a931ff5b/developing-possibilities.jpg" alt="Developing Possibilities" />

With option objects, we've covered the topic of extensible configuration. Let's talk about allowing the API user to extend the core and API itself. This is an important topic, as it allows your code to focus on the important things, while having API users implement edge-cases themselves. Good APIs are concise APIs. Having a hand full of configuration options is fine, but having a couple dozen of them makes your API feel bloated and opaque. Focus on the primary-use cases, only do the things most of your API users will need. Everything else should be left up to them. To allow API users to extend your code to suit their needs, you have a couple of options...</p>

### Callbacks

Callbacks can be used to achieve extensibility by configuration. You can use callbacks to allow the API user to override certain parts of your code. When you feel specific tasks may be handled differently than your default code, refactor that code into a configurable callback function to allow an API user to easily override that:

<pre><code class="language-javascript">var default_options = {
  // ...
  position: function($elem, $parent) {
    $elem.css($parent.position());
  }
};

function Widget(options) {
  this.options = jQuery.extend({}, default_options, options || {});
  this.create();
};

Widget.prototype.create = function() {
  this.$container = $("&lt;div&gt;&lt;/div&gt;").appendTo(document.body);
  this.$thingie = $("&lt;div&gt;&lt;/div&gt;").appendTo(this.$container);
  return this;
};

Widget.protoype.show = function() {
  this.options.position(this.$thingie, this.$container);
  this.$thingie.show();
  return this;
};</code></pre>

<pre><code class="language-javascript">var widget = new Widget({
  position: function($elem, $parent) {
    var position = $parent.position();
    // position $elem at the lower right corner of $parent
    position.left += $parent.width();
    position.top += $parent.height();
    $elem.css(position);
  }
});
widget.show();</code></pre>

Callbacks are also a generic way to allow API users to customize elements your code has created:

<pre><code class="language-javascript">// default create callback doesn't do anything
default_options.create = function($thingie){};

Widget.prototype.create = function() {
  this.$container = $("&lt;div&gt;&lt;/div&gt;").appendTo(document.body);
  this.$thingie = $("&lt;div&gt;&lt;/div&gt;").appendTo(this.$container);
  // execute create callback to allow decoration
  this.options.create(this.$thingie);
  return this;
};</code></pre>

<pre><code class="language-javascript">var widget = new Widget({
  create: function($elem) {
    $elem.addClass('my-style-stuff');
  }
});
widget.show();</code></pre>

Whenever you accept callbacks, be sure to document their signature and provide examples to help API users customize your code. Make sure you're consistent about the context (where <code>this</code> points to) in which callbacks are executed in, and the arguments they accept.</p>

### Events

Events come naturally when working with the DOM. In larger application we use events in various forms (e.g. PubSub) to enable communication between modules. Events are particularly useful and feel most natural when dealing with UI widgets. Libraries like jQuery offer simple interfaces allowing you to easily conquer this domain.

Events interface best when there is something happening — hence the name. Showing and hiding a widget could depend on circumstances outside of your scope. Updating the widget when it's shown is also a very common thing to do. Both can be achieved quite easily using jQuery's event interface, which even allows for the use of delegated events:

<pre><code class="language-javascript">Widget.prototype.show = function() {
  var event = jQuery.Event("widget:show");
  this.$container.trigger(event);
  if (event.isDefaultPrevented()) {
    // event handler prevents us from showing
    return this;
  }

  this.options.position(this.$thingie, this.$container);
  this.$thingie.show();
  return this;
};</code></pre>

<pre><code class="language-javascript">// listen for all widget:show events
$(document.body).on('widget:show', function(event) {
  if (Math.random() &gt; 0.5) {
    // prevent widget from showing
    event.preventDefault();
  }

  // update widget's data
  $(this).data("last-show", new Date());
});

var widget = new Widget();
widget.show();</code></pre>

You can freely choose event names. Avoid using <a href="https://developer.mozilla.org/en-US/docs/DOM/DOM_event_reference">native events</a> for proprietary things and consider namespacing your events. jQuery UI's event names are comprised of the widget's name and the event name <code>dialogshow</code>. I find that hard to read and often default to <code>dialog:show</code>, mainly because it is immediately clear that this is a custom event, rather than something some browser might have secretly implemented.</p>

## Hooks

Traditional getter and setter methods can especially benefit from hooks. Hooks usually differ from callbacks in their number and how they're registered. Where callbacks are usually used on an instance level for a specific task, hooks are usually used on a global level to customize values or dispatch custom actions. To illustrate how hooks can be used, we'll take a peek at <a href="https://api.jquery.com/jQuery.cssHooks/">jQuery's cssHooks</a>:

<pre><code class="language-javascript">// define a custom css hook
jQuery.cssHooks.custombox = {
  get: function(elem, computed, extra) {
    return $.css(elem, 'borderRadius') == "50%"
      ? "circle"
      : "box";
  },
  set: function(elem, value) {
    elem.style.borderRadius = value == "circle"
      ? "50%"
      : "0";
  }
};

// have .css() use that hook
$("#some-selector").css("custombox", "circle");</code></pre>

By registering the hook <code>custombox</code> we've given jQuery's <code>.css()</code> method the ability to handle a CSS property it previously couldn't. In my article <a href="https://blog.rodneyrehm.de/archives/11-jQuery-Hooks.html">jQuery hooks</a>, I explain the other hooks that jQuery provides and how they can be used in the field. You can provide hooks much like you would handle callbacks:

<pre><code class="language-javascript">DateInterval.nameHooks = {
  "yesterday" : function() {
    var d = new Date();
    d.setTime(d.getTime() - 86400000);
    d.setHours(0);
    d.setMinutes(0);
    d.setSeconds(0);
    return d;
  }
};

DateInterval.prototype.start = function(date) {
  if (date === undefined) {
    return new Date(this.startDate.getTime());
  }

  if (typeof date === "string" &amp;&amp; DateInterval.nameHooks[date]) {
    date = DateInterval.nameHooks[date]();
  }

  if (!(date instanceof Date)) {
    date = new Date(date);
  }

  this.startDate.setTime(date.getTime());
  return this;
};</code></pre>

<pre><code class="language-javascript">var di = new DateInterval();
di.start("yesterday");</code></pre>

In a way, hooks are a collection of callbacks designed to handle custom values within your own code. With hooks you can stay in control of almost everything, while still giving API users the option to customize.</p>

## Generating Accessors

<img title="Duplication" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8398348b-1ab4-4f32-ad03-f86b96c4b10a/duplication.jpg" alt="Duplication" width="500" height="280" />

Any API is likely to have multiple accessor methods (getters, setters, executors) doing similar work. Coming back to our <code>DateInterval</code> example, we're most likely providing <code>start()</code> and <code>end()</code> to allow manipulation of intervals. A simple solution could look like:

<pre><code class="language-javascript">DateInterval.prototype.start = function(date) {
  if (date === undefined) {
    return new Date(this.startDate.getTime());
  }

  this.startDate.setTime(date.getTime());
  return this;
};

DateInterval.prototype.end = function(date) {
  if (date === undefined) {
    return new Date(this.endDate.getTime());
  }

  this.endDate.setTime(date.getTime());
  return this;
};</code></pre>

As you can see we have a lot of repeating code. A DRY (Don't Repeat Yourself) solution might use this generator pattern:

<pre><code class="language-javascript">var accessors = ["start", "end"];
for (var i = 0, length = accessors.length; i &lt; length; i++) {
  var key = accessors[i];
  DateInterval.prototype[key] = generateAccessor(key);
}

function generateAccessor(key) {
  var value = key + "Date";
  return function(date) {
    if (date === undefined) {
      return new Date(this[value].getTime());
    }

    this[value].setTime(date.getTime());
    return this;
  };
}</code></pre>

This approach allows you to generate multiple similar accessor methods, rather than defining every method separately. If your accessor methods require more data to setup than just a simple string, consider something along the lines of:

<pre><code class="language-javascript">var accessors = {"start" : {color: "green"}, "end" : {color: "red"}};
for (var key in accessors) {
  DateInterval.prototype[key] = generateAccessor(key, accessors[key]);
}

function generateAccessor(key, accessor) {
  var value = key + "Date";
  return function(date) {
    // setting something up
    // using `key` and `accessor.color`
  };
}</code></pre>

In the chapter <em>Handling Arguments</em> we talked about a method pattern to allow your getters and setters to accept various useful types like maps and arrays. The method pattern itself is a pretty generic thing and could easily be turned into a generator:

<pre><code class="language-javascript">function wrapFlexibleAccessor(get, set) {
  return function(name, value) {
    var map;

    if (jQuery.isPlainObject(name)) {
      // setting a map
      map = name;
    } else if (value !== undefined) {
      // setting a value (on possibly multiple names), convert to map
      keys = name.split(" ");
      map = {};
      for (var i = 0, length = keys.length; i &lt; length; i++) {
        map[keys[i]] = value;
      }
    } else {
      return get.call(this, name);
    }

    for (var key in map) {
      set.call(this, name, map[key]);
    }

    return this;
  };
}

DateInterval.prototype.values = wrapFlexibleAccessor(
  function(name) {
    return name !== undefined
      ? this.values[name]
      : this.values;
  },
  function(name, value) {
    this.values[name] = value;
  }
);</code></pre>

Digging into the art of writing DRY code is well beyond this article. <a href="https://twitter.com/rmurphey">Rebecca Murphey</a> wrote <a href="https://rmurphey.com/blog/2010/07/12/patterns-for-dry-er-javascript/">Patterns for DRY-er JavaScript</a> and <a href="https://twitter.com/mathias">Mathias Bynens'</a> slide deck on <a href="https://slideshare.net/mathiasbynens/how-dry-impacts-javascript-performance-faster-javascript-execution-for-the-lazy-developer">how DRY impacts JavaScript performance</a> are a good start, if you're new to the topic.</p>

## The Reference Horror

Unlike other languages, JavaScript doesn't know the concepts of <em>pass by reference</em> nor <em>pass by value</em>. Passing data by value is a safe thing. It makes sure data passed to your API and data returned from your API may be modified outside of your API without altering the state within. Passing data by reference is often used to keep memory overhead low, values passed by reference can be changed anywhere outside your API and affect state within.

In JavaScript there is no way to tell if arguments should be passed by reference or value. Primitives (strings, numbers, booleans) are treated as <em>pass by value</em>, while objects (any object, including Array, Date) are handled in a way that's comparable to <em>by reference</em>. If this is the first you're hearing about this topic, let the following example enlighten you:

<pre><code class="language-javascript">// by value
function addOne(num) {
  num = num + 1; // yes, num++; does the same
  return num;
}

var x = 0;
var y = addOne(x);
// x === 0 &lt;--
// y === 1

// by reference
function addOne(obj) {
  obj.num = obj.num + 1;
  return obj;
}

var ox = {num : 0};
var oy = addOne(ox);
// ox.num === 1 &lt;--
// oy.num === 1</code></pre>

The <em>by reference</em> handling of objects can come back and bite you if you're not careful. Going back to the <code>DateInterval</code> example, check out this bugger:

<pre><code class="language-javascript">var startDate = new Date(2012, 0, 1);
var endDate = new Date(2012, 11, 31)
var interval = new DateInterval(startDate, endDate);
endDate.setMonth(0); // set to january
var days = interval.days(); // got 31 but expected 365 - ouch!</code></pre>

Unless the constructor of DateInterval <em>made a copy</em> (<code>clone</code> is the technical term for a copy) of the values it received, any changes to the original objects will reflect on the internals of DateInterval. This is <em>usually</em> not what we want or expect.

Note that the same is true for values returned from your API. If you simply return an internal object, any changes made to it outside of your API will be reflected on your internal data. This is most certainly not what you want. <a href="https://api.jquery.com/jQuery.extend/">jQuery.extend()</a>, <a href="https://underscorejs.org/#extend">_.extend()</a> and Protoype's <a href="https://api.prototypejs.org/language/Object/extend/">Object.extend</a> allow you to easily escape the reference horror.

If this summary did not suffice, read the excellent chapter <a href="https://docstore.mik.ua/orelly/webprog/jscript/ch11_02.htm">By Value Versus by Reference</a> from O'Reilly's <a href="https://docstore.mik.ua/orelly/webprog/jscript/index.htm">JavaScript – The Definitive Guide</a>.</p>

## The Continuation Problem

In a fluent interface, all methods of a chain are executed, regardless of the state that the base object is in. Consider calling a few methods on a jQuery instance that contain no DOM elements:

<pre><code class="language-javascript">jQuery('.wont-find-anything')
  // executed although there is nothing to execute against
  .somePlugin().someOtherPlugin();</code></pre>

In non-fluent code we could have prevented those functions from being executed:

<pre><code class="language-javascript">var $elem = jQuery('.wont-find-anything');
if ($elem.length) {
  $elem.somePlugin().someOtherPlugin();
}</code></pre>

Whenever we chain methods, we lose the ability to prevent certain things from happening — we can't escape from the chain. As long as the API developer knows that objects can have a state where methods don't actually do anything but <code>return this;</code>, everything is fine. Depending on what your methods do internally, it may help to prepend a trivial <code>is-empty</code> detection:

<pre><code class="language-javascript">jQuery.fn.somePlugin = function() {
  if (!this.length) {
    // "abort" since we've got nothing to work with
    return this;
  }

  // do some computational heavy setup tasks
  for (var i = 10000; i &gt; 0; i--) {
    // I'm just wasting your precious CPU!
    // If you call me often enough, I'll turn
    // your laptop into a rock-melting jet engine
  }

  return this.each(function() {
    // do the actual job
  });
};</code></pre>

## Handling Errors

<img title="Fail Fast" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80f92509-8fc3-40c3-818b-3fa59e23969e/fail-faster.jpg" alt="Fail Faster" />

I was lying when I said we couldn't escape from the chain — there is an <code>Exception</code> to the rule (pardon the pun ☺).

We can always eject by throwing an Error (Exception). Throwing an Error is considered a deliberate abortion of the current flow, most likely because you came into a state that you couldn't recover from. But beware — not all Errors are helping the debugging developer:

<pre><code class="language-javascript">// jQuery accepts this
$(document.body).on('click', {});

// on click the console screams
//   TypeError: ((p.event.special[l.origType] || {}).handle || l.handler).apply is not a function
//   in jQuery.min.js on Line 3</code></pre>

Errors like these are a major pain to debug. Don't waste other people's time. Inform an API user if he did something stupid:

<pre><code class="language-javascript">if (Object.prototype.toString.call(callback) !== '[object Function]') { // see note
  throw new TypeError("callback is not a function!");
}</code></pre>

Note: <code>typeof callback === "function"</code> should not be used, as older browsers may report objects to be a <code>function</code>, which they are not. In Chrome (up to version 12) <code>RegExp</code> is such a case. For convenience, use <a href="https://api.jquery.com/jQuery.isfunction/">jQuery.isFunction()</a> or <a href="https://underscorejs.org/#isFunction">_.isFunction()</a>.

Most libraries that I have come across, regardless of language (within the weak-typing domain) don't care about rigorous input validation. To be honest, my own code only validates where I anticipate developers stumbling. Nobody really does it, but all of us should. Programmers are a lazy bunch — we don't write code just for the sake of writing code or for some cause we don't truly believe in. The developers of Perl6 have recognized this being a problem and decided to incorporate something called <em>Parameter Constraints</em>. In JavaScript, their approach might look something like this:

<pre><code class="language-javascript">function validateAllTheThings(a, b {where typeof b === "numeric" and b &lt; 10}) {
  // Interpreter should throw an Error if b is
  // not a number or greater than 9
}</code></pre>

While the syntax is as ugly as it gets, the idea is to make validation of input a top-level citizen of the language. JavaScript is nowhere near being something like that. That's fine — I couldn't see myself cramming these constraints into the function signature anyways. It's admitting the problem (of weakly-typed languages) that is the interesting part of this story.

JavaScript is neither weak nor inferior, we just have to work a bit harder to make our stuff really robust. Making code robust does not mean accepting any data, waving your wand and getting some result. Being robust means not accepting rubbish <em>and telling the developer about it</em>.

Think of input validation this way: A couple of lines of code behind your API can make sure that no developer has to spend hours chasing down weird bugs because they accidentally gave your code a string instead of a number. This is the one time you can tell people <em>they're wrong</em> and they'll actually love you for doing so.</p>

## Going Asynchronous

So far we've only looked at synchronous APIs. Asynchronous methods usually accept a callback function to inform the outside world, once a certain task is finished. This doesn't fit too nicely into our fluent interface scheme, though:

<pre><code class="language-javascript">Api.protoype.async = function(callback) {
  console.log("async()");
  // do something asynchronous
  window.setTimeout(callback, 500);
  return this;
};
Api.protoype.method = function() {
  console.log("method()");
  return this;
};</code></pre>

<pre><code class="language-javascript">// running things
api.async(function() {
  console.log('callback()');
}).method();

// prints: async(), method(), callback()</code></pre>

This example illustrates how the asynchronous method <code>async()</code> begins its work but immediately returns, leading to <code>method()</code> being invoked before the actual task of <code>async()</code> completed. There are times when we want this to happen, but generally we expect <code>method()</code> to execute <em>after</em> <code>async()</code> has completed its job.</p>

### Deferreds (Promises)

To some extent we can counter the mess that is a mix of asynchronous and synchronous API calls with <a href="https://wiki.commonjs.org/wiki/Promises/A">Promises</a>. jQuery knows them as <a href="https://api.jquery.com/category/deferred-object/">Deferreds</a>. A Deferred is returned in place of your regular <code>this</code>, which forces you to eject from method chaining. This may seem odd at first, but it effectively prevents you from continuing synchronously after invoking an asynchronous method:

<pre><code class="language-javascript">Api.protoype.async = function() {
  var deferred = $.Deferred();
  console.log("async()");

  window.setTimeout(function() {
    // do something asynchronous
    deferred.resolve("some-data");
  }, 500);

  return deferred.promise();
};</code></pre>

<pre><code class="language-javascript">api.async().done(function(data) {
  console.log("callback()");
  api.method();
});

// prints: async(), callback(), method()</code></pre>

The Deferred object let's you register handlers using <code>.done()</code>, <code>.fail()</code>, <code>.always()</code> to be called when the asynchronous task has completed, failed, or regardless of its state. See <a href="https://sitr.us/2012/07/31/promise-pipelines-in-javascript.html">Promise Pipelines In JavaScript</a> for a more detailed introduction to Deferreds.</p>

## Debugging Fluent Interfaces

While <em>Fluent Interfaces</em> are much nicer to develop with, they do come with certain limitations regarding de-buggability.

As with any code, <em>Test Driven Development</em> (TDD) is an easy way to reduce debugging needs. Having written URI.js in TDD, I have not come across major pains regarding debugging my code. However, TDD only <em>reduces</em> the need for debugging — it doesn't replace it entirely.

Some voices on the internet suggest writing out each component of a chain in their separate lines to get proper line-numbers for errors in a stack trace:

<pre><code class="language-javascript">foobar.bar()
  .baz()
  .bam()
  .someError();</code></pre>

This technique does have its benefits (though better debugging is not a solid part of it). Code that is written like the above example is even simpler to read. Line-based differentials (used in version control systems like SVN, GIT) might see a slight win as well. Debugging-wise, it is only Chrome (at the moment), that will show <code>someError()</code> to be on line four, while other browsers treat it as line one.

Adding a simple method to logging your objects can already help a lot — although that is considered "manual debugging" and may be frowned upon by people used to "real" debuggers:

<pre><code class="language-javascript">DateInterval.prototype.explain = function() {
  // log the current state to the console
  console.dir(this);
};

var days = (new Date(2012, 0, 1))
  .until(2012, 11, 31) // returns DateInterval instance
  .explain() // write some infos to the console
  .days(); // 365</code></pre>

### Function names

Throughout this article you've seen a lot of demo code in the style of <code>Foo.prototype.something = function(){}</code>. This style was chosen to keep examples brief. When writing APIs you might want to consider either of the following approaches, to have your console properly identify function names:

<pre><code class="language-javascript">Foo.prototype.something = function something() {
  // yadda yadda
};</code></pre>

<pre><code class="language-javascript">Foo.prototype.something = function() {
  // yadda yadda
};
Foo.prototype.something.displayName = "Foo.something";</code></pre>

The second option <code>displayName</code> was introduced by WebKit and later adopted by Firebug / Firefox. <code>displayName</code> is a bit more code to write out, but allows arbitrary names, including a namespace or associated object. Either of these approaches can help with anonymous functions quite a bit.

Read more on this topic in <a href="https://kangax.github.com/nfe/">Named function expressions demystified</a> by <a href="https://twitter.com/kangax">kangax</a>.</p>

## Documenting APIs

One of the hardest tasks of software development is documenting things. Practically everyone hates doing it, yet everybody laments about bad or missing documentation of the tools they need to use. There is a wide range of tools that supposedly help and automate documenting your code:

*   [YUIDoc](https://yui.github.com/yuidoc/) (requires Node.js, npm)
*   [JsDoc Toolkit](https://github.com/p120ph37/node-jsdoc-toolkit) (requires Node.js, npm)
*   [Markdox](https://github.com/cbou/markdox) (requires Node.js, npm)
*   [Dox](https://github.com/visionmedia/dox) (requires Node.js, npm)
*   [Docco](https://jashkenas.github.com/docco/) (requires Node.js, Python, CoffeeScript)
*   [JSDuck](https://github.com/senchalabs/jsduck) (reqires Ruby, gem)
*   [JSDoc 3](https://github.com/jsdoc3/jsdoc) (requires Java)

At one point or another all of these tool won't fail to disappoint. JavaScript is a very dynamic language and thus particularly diverse in expression. This makes a lot of things extremely difficult for these tools. The following list features a couple of reasons why I've decided to prepare documentation in vanilla HTML, markdown or <a href="https://en.wikipedia.org/wiki/DocBook">DocBoock</a> (if the project is large enough). jQuery, for example, has the same issues and doesn't document their APIs within their code at all.

1.  Function signatures aren't the only documentation you need, but most tools focus only on them.
2.  Example code goes a long way in explaining how something works. Regular API docs usually fail to illustrate that with a fair trade-off.
3.  API docs usually fail horribly at explaining things _behind the scenes_ (flow, events, etc).
4.  Documenting methods with multiple signatures is usually a real pain.
5.  Documenting methods using option objects is often not a trivial task.
6.  Generated Methods aren't easily documented, neither are default callbacks.

If you can't (or don't) want to adjust your code to fit one of the listed documentation tools, projects like <a href="https://gregfranko.com/Document-Bootstrap/">Document-Bootstrap</a> might save you some time setting up your home brew documentation.

Make sure your Documentation is more than just some generated API doc. Your users will appreciate any examples you provide. Tell them how your software flows and which events are involved when doing something. Draw them a map, if it helps their understanding of whatever it is your software is doing. And above all: keep your docs in sync with your code!

### Self-Explanatory Code

Providing good documentation will not keep developers from actually reading your code — your code is a piece of documentation itself. Whenever the documentation doesn't suffice (and every documentation has its limits), developers fall back to reading the actual source to get their questions answered. Actually, you are one of them as well. You are most likely reading your own code again and again, with weeks, months or even years in between.

You should be writing code that explains itself. Most of the time this is a non-issue, as it only involves you thinking harder about naming things (functions, variables, etc) and sticking to a core concept. If you find yourself writing code comments to document how your code does something, you're most likely wasting time — your time, and the reader's as well. Comment on your code to explain <em>why</em> you solved the problem this particular way, rather than explaining <em>how</em> you solved the problem. The <em>how</em> should become apparent through your code, so don't repeat yourself. Note that using comments to mark sections within your code or to explain general concepts is totally acceptable.</p>

## Conclusion

*   An API is a contract between you (the provider) and the user (the consumer). Don't just change things between versions.
*   You should invest as much time into the question _How will people use my software?_ as you have put into _How does my software work internally?_
*   With a couple of simple tricks you can greatly reduce the developer's efforts (in terms of the lines of code).
*   Handle invalid input as early as possible — throw Errors.
*   Good APIs are flexible, better APIs don't let you make mistakes.

Continue with <a href="https://vimeo.com/35689836">Reusable Code for good or for awesome</a> (<a href="https://www.slideshare.net/jaffathecake/reusable-code-for-good-or-for-awesome">slides</a>), a Talk by <a href="https://twitter.com/jaffathecake">Jake Archibald</a> on designing APIs. Back in 2007 Joshua Bloch gave the presentation <a href="https://youtube.com/watch?v=heh4OeB9A-c">How to Design A Good API and Why it Matters</a> at Google Tech Talks. While his talk did not focus on JavaScript, the basic principles that he explained still apply.

Now that you're up to speed on designing APIs, have a look at <a href="https://addyosmani.com/resources/essentialjsdesignpatterns/book/">Essential JS Design Patterns</a> by <a href="https://twitter.com/addyosmani">Addy Osmani</a> to learn more about how to structure your internal code.

<em>Thanks go out to <a href="https://twitter.com/bassistance">@bassistance</a>, <a href="https://twitter.com/addyosmani">@addyosmani</a> and @hellokahlil for taking the time to proof this article.</em>


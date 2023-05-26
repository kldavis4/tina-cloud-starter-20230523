---
title: What You Need To Know About JavaScript Scope
slug: what-you-need-to-know-about-javascript-scope
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742c8ad8-59a0-4317-9ea1-b94b7d926dd2/formu.gif
date: 2009-08-01T11:28:50.000Z
author: colin-ramsay
description: >-
  Understanding scope in programming is key to appreciating how your variables
  interact with the rest of your code. In some languages, this can be quite
  straightforward, but JavaScript's anonymous functions and event handling
  features, along with a couple of little quirks, mean that handling scope in
  your applications can become frustrating.
categories:
  - Coding
  - JavaScript
---
Understanding scope in programming is key to appreciating how your variables interact with the rest of your code. In some languages, this can be quite straightforward, but JavaScript's anonymous functions and event handling features, along with a couple of little quirks, mean that handling scope in your applications can become frustrating.

This article discusses how JavaScript handles scope and how various JavaScript libraries provide methods for dealing with it and how they smooth out a few bumps. We'll also look at how you can get back to basics and do some interesting scope wrangling without a library, a useful approach if you're writing code that needs to stand alone. 

You might be interested in the following related posts:

*   [Seven JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)
*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)
*   [Useful JavaScript Libraries and jQuery Plugins](https://www.smashingmagazine.com/2012/09/useful-javascript-libraries-jquery-plugins-web-developers/)

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e6a4b99-0031-4827-999b-933247001387/js.jpg" alt="JavaScript Scope" width="502" height="335" />

{{% feature-panel %}}

## You Are Here

So what is "scope"? We might say that it refers to your current location. If you run some JavaScript like...

<pre><code class="language-javascript">var iAmGlobal = 5 * 5;</code></pre>

... then you're running in the global scope, the big wide world, where you can't go any further out. For something like...

<pre><code class="language-javascript">function doSomething() {
  var inner = 5 * 5;
};</code></pre>

... you're now boxed in by this function, running within its scope. The phrase "boxed in" is appropriate; take a look at this code:

<pre><code class="language-javascript">var g = "global";
function go() { 
  var l = "local";
}
go();
alert(l); // throws a reference error</code></pre>

You'll see that when we run the <code>go</code> function, the <code>l</code> variable is contained within that function's scope. It cannot be accessed from a higher level scope.</p>

### How it Works

As well as variable scope, JavaScript uses the <code>this</code> keyword to get a reference to the current execution context. That rather terrifying term boils down this: at any point in your JavaScript code, you can ask "Help! Where am I?" and get back an object reference. This reference is for the current context, the object that "owns" the currently executing code.

Now, you might think, given what we've just learned about scope, the owner of the current code would be the scope in which it is executed. After all, in JavaScript, even functions are objects and can be passed around in variables. But no. Take this function, for instance:

<pre><code class="language-javascript">function go() { console.debug(this); }
go();</code></pre>

This gives you a reference to the top-level execution context; in a browser, that's the browser window itself.

There are a few exceptions to this. For example, if we create a JavaScript object and then call a method on it, then the scope is bound to the object:

<pre><code class="language-javascript">var myObject = { 
  go: function() {
    console.debug(this);
  } 
};
myObject.go(); // console.debugs a reference to myObject</code></pre>

Similarly, when using functions as constructors, you see the same behavior:

<pre><code class="language-javascript">function MyClass() {
  this.go = function() {
    console.debug(this);
  }
}

var instance1 = new MyClass();
var instance2 = new MyClass();

instance1.go(); // console.debugs a reference to the MyClass instance1
instance2.go(); // console.debugs a reference to the MyClass instance2</code></pre>

However, notice in this case that the reference is to the individual object instance rather than the class definition, which contrasts with the previous object literal example in which we will always receive a reference to the same object.

With event handlers, things get a little more confusing. If you specify an event handler inline in HTML, then you end up with it referencing the global window object. However, if you use JavaScript to wire your events, then you get a reference to the DOM object that raised it; for example, a click handler on a button would have the button element as the reference.

Event handlers are a common situation in which you would want to bind a function to a different scope; many JavaScript libraries provide features to help do just that. Let's take a look at some common options.</p>

## Libraries

Many developers use JavaScript libraries to avoid having to deal with browser inconsistencies and to take advantage of the many shortcuts they offer. Scope handling is something most libraries give a helping hand with, so let's take a look at what a few of the major players offer.</p>

### Prototype

Prototype comes with a bind method that allows a developer to specify the bound context for a function.

<pre><code class="language-javascript">var products = ['Shoes', 'Sweater', 'Jeans', 'Wig'];

function showCount() {
  for(var i = 0; i &lt; number; i++) {
    document.body.innerHTML += this[i] + '. ';
  }
}

var fn = showCount.bind(products);
fn(2); // outputs Shoes. Sweater. to the document</code></pre>

It also supports passing arguments that are "remembered" when you call the function, and these can be used to create shortcut functions; basically a version of a function that defaults to passing in certain arguments:

<pre><code class="language-javascript">var showOne = showCount.bind(products, 1);
var showFour = showCount.bind(products, 4);
showOne(); // outputs Shoes.
showFour(); // output Shoes. Sweater. Jeans. Wig.</code></pre>

See Prototype's <code>Function.curry</code> for more information on this particular aspect of <code>Function.bind</code>. The second useful feature of Prototype's scope handling is <code>bindAsEventListener</code>. This is very similar to <code>bind</code> but ensures that the first argument passed to the event handler is the event object.

<pre><code class="language-javascript">Event.observe(
  $('showCountButton'),
  'click',
  showCountHandler.bindAsEventListener(products, 2)
);</code></pre>

Here we're using Prototype's event functions to set up an event listener when the <code>showCountButton</code> is clicked. We're passing our <code>products</code> array as the context, which the function is bound to, but in this case the <code>showCountHandler</code> would look something like this:

<pre><code class="language-javascript">function showCountHandler(e, number) {
  for(var i = 0; i &lt; number; i++) {
    document.body.innerHTML += this[i] + '. ';
  }
  Event.stop(e);
}</code></pre>

So we have the <code>products</code> array as <code>this</code>, but we also have the <code>e</code> event object automatically passed as the first parameter, which we can later use to stop the default event.

The two Prototype methods for binding context are handy because they're used in exactly the same way, so you have a very simple and consistent method of taming your context.</p>

### Ext JS

Ext JS is farther reaching than either Prototype or MooTools in that it provides a full end-to-end framework for UI and application creation. This means it also provides correspondingly more features to control scope. To compare it with Prototype, let's look at how to bind to a particular context:

<pre><code class="language-javascript">var fn = showCount.createDelegate(products, 4);</code></pre>

This is identical in usage to Prototype's bind method. But is there a difference when dealing with event handlers?

<pre><code class="language-javascript">Ext.get('showCountButton').on('click', 
  showCountHandler.createDelegate(products, 4)
);</code></pre>

That's right: there is no difference. Ext JS will normalize the event object into an <code>Ext.EventObject</code> for you and then append your additional arguments after that. However, there are two caveats to this. First, Ext doesn't just pass the event object to the handler, but also passes the source of the event (in this case, the <code>showCountButton</code>) and any options that were passed to the <code>on</code> method. So, our handler now looks like this:

<pre><code class="language-javascript">function showCountHandler(e, source, options, number) {}</code></pre>

However, there is a shortcut to using <code>createDelegate</code>, and it involves understanding the arguments of the <code>on</code> method. We can do this like so:

<pre><code class="language-javascript">Ext.get('showCountButton').on('click', showCountHandler, products, { number: 4 });</code></pre>

The third argument of <code>on</code> is the scope under which the handler should run, which eliminates the need to use <code>createDelegate</code>. However, in order to pass further parameters, we have to use the <code>options</code> parameter. So our handler in this case would be:

<pre><code class="language-javascript">function showCountHandler(e, source, options) {
  number = options.number;
}</code></pre>

This is not quite as elegant on the handler side of things, but it's useful to know that Ext JS provides a variety of methods for accomplishing similar things, and you can use them accordingly when building your applications.</p>

### MooTools

The MooTools library provides two methods that are essentially like replacements for Prototype versions: <code>bind</code> and <code>bindWithEvent</code>, a.k.a. <code>bindAsEventListener</code>. However, on top of these familiar features, it provides a couple more that lend some extra flexibility. My favorite is <code>Function.create</code>:

<pre><code class="language-javascript">var fn = showCount.create({
  bind: products,
  arguments: 4
});</code></pre>

This is nice and succinct, and to turn this into an event handler, we do this:

<pre><code class="language-javascript">showCount.create({
  bind: products,
  arguments: 4,
  event: true
});</code></pre>

We can pass additional options, such as <code>delay</code>, which defers the execution of the function by a specified number of milliseconds, and <code>periodical</code>, which fires the function every time the specified interval elapses.

One library conspicuous in its absence is jQuery, which doesn't offer any context binding facility. But JavaScript does have built-in features that allow you to manage context in many scenarios, and it also provides relatively simple methods of building your own solutions to more complicated problems.</p>

## On Your Own

I'm no snob: leveraging the hard work of the great developers who have spent a lot of time on their libraries makes total sense. They will have worked through all of the bugs and edge cases so that you don't have to. On the other hand, understanding what's happening on the JavaScript level is important, not only as an academic exercise but also for those occasions when you can't rely on a library.

Sometimes offering standalone and library-independent scripts is best; for example, if you would like to make your code available publicly and for widespread use. By relying on a library, you restrict the use of the code to people who use that library.

Let's take a look at how scope and context can be handled without using a library.</p>

### Call and Apply

JavaScript functions have two methods available to them that are of particular interest for handling context. Let's look at <code>call</code>:

<pre><code class="language-javascript">showCount.call(products, 4);</code></pre>

<code>Apply</code> is very similar but is used when you don't know how many arguments you will be passing. It takes an array as its second parameter:

<pre><code class="language-javascript">showCount.apply(products, [4]);</code></pre>

Both of these achieve the same goal, but your usage case will determine which would work best for you.</p>

### Event Handler Scope

We saw in the explanations of scope how event handlers cause problems, and we also saw how the various JavaScript libraries provide means of getting around this. If you're stuck with bare-bones JavaScript, then you simply have to write your own means of scoping event handlers, and we'll look at how to do that now.

<code>Call</code> and <code>apply</code> trigger the function immediately: that's not what we're after. Instead, we want to return a new function, which will then be called when the event fires. So:

<pre><code class="language-javascript">Function.prototype.bindContext = function() {
  // when adding functions using prototype, "this" is the
  // object which the new function was called on 
  var callingFunction = this;

  // pass the desired scope object as the first arg
  var scope = arguments[0];

  // create a new arguments array with the first arg removed 
  var otherArgs = [];
  for(var i = 1; i &lt; arguments.length; i++){ 
    otherArgs.push(arguments[i]);
  }

  // return a function remembering to include the event 
  return function(e) {
    // Add the event object to the arguments array
    otherArgs.push(e || window.event);
    // Array is in the wrong order so flip it
    otherArgs.reverse();

    // Now use apply to set scope and arguments
    callingFunction.apply(scope, otherArgs);
  }
}</code></pre>

This is a basic implementation with no error handling, but it provides a useful base to expand on and for understanding the overall approach. Dealing with event handler scope is essential for most JavaScript applications, and no developer should be tied to a single framework, so an appreciation for handling this problem at a low level is useful for every coder.</p>

## Conclusion

When building any large JavaScript application, a solid understanding of scope is not only useful but pretty much necessary. While using a common JavaScript library is a useful shortcut, it's certainly never bad to get back to basics and roll your own solution in order to gain more control of JavaScript scope.</p>

## Further Resources

*   [An introduction to scope in Dojo.](https://almaer.com/blog/dealing-with-javascript-scope-issues-the-tale-of-alex-kindly-indulging-me)
*   [A huge technical reference on scope and closures in JavaScript.](https://www.jibbering.com/faq/faq_notes/closures.html)
*   [Interesting scope "gotcha."](https://happygiraffe.net/blog/2008/08/27/javascript-scope/)

{{< signature "al" >}}


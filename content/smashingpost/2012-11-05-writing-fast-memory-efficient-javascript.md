---
title: 'How To Write Fast, Memory-Efficient JavaScript'
slug: writing-fast-memory-efficient-javascript
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bd465a6d-92c2-418b-bdc0-8df9a0cd9ad2/robo-vacuum.jpg
date: 2012-11-05T15:00:57.000Z
author: addy-osmani
description: >-
  JavaScript engines such as Google’s V8 (Chrome, Node) are specifically
  designed for the fast execution of large JavaScript applications. As you
  develop, if you care about memory usage and performance, you should be aware
  of some of what's going on in your user's browser's JavaScript engine behind
  the scenes.
categories:
  - Coding
  - JavaScript
  - Optimization
  - Performance
---
JavaScript engines such as Google’s <a href="https://code.google.com/p/v8/">V8</a> (Chrome, Node) are specifically designed for the <a href="https://www.html5rocks.com/en/tutorials/speed/v8/">fast execution</a> of large JavaScript applications. As you develop, if you care about memory usage and performance, you should be aware of some of what's going on in your user's browser's JavaScript engine behind the scenes.

Whether it’s V8, <a href="https://developer.mozilla.org/en-US/docs/SpiderMonkey">SpiderMonkey</a> (Firefox), <a href="https://my.opera.com/ODIN/blog/carakan-faq">Carakan</a> (Opera), <a href="https://en.wikipedia.org/wiki/Chakra_(JScript_engine)">Chakra</a> (IE) or something else, doing so can help you <strong>better optimize your applications</strong>. That's not to say one should optimize for a single browser or engine. Never do that.

You should, however, ask yourself questions such as:

*   Is there anything I could be doing more efficiently in my code?
*   What (common) optimizations do popular JavaScript engines make?
*   What is the engine unable to optimize for, and is the garbage collector able to clean up what I’m expecting it to?

There are many common pitfalls when it comes to writing memory-efficient and fast code, and in this article we’re going to explore some test-proven approaches for writing code that performs better.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Front-End Peformance Checklist 2019](https://www.smashingmagazine.com/2019/01/front-end-performance-checklist-2019-pdf-pages/)
*   [How To Make Your Websites Faster On Mobile Devices](https://www.smashingmagazine.com/2013/04/build-fast-loading-mobile-website/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Everything You Need To Know About AMP](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)

## So, How Does JavaScript Work In V8?

While it's possible to develop large-scale applications without a thorough understanding of JavaScript engines, any car owner will tell you they've looked under the hood at least once. As Chrome is my browser of choice, I'm going to talk a little about its JavaScript engine. V8 is made up of a few core pieces.

*   A **base compiler**, which parses your JavaScript and generates native machine code before it is executed, rather than executing bytecode or simply interpreting it. This code is initially not highly optimized.
*   V8 represents your objects in an **object model**. Objects are represented as associative arrays in JavaScript, but in V8 they are represented with [hidden classes](https://github.com/v8/v8/wiki/Design%20Elements), which are an internal type system for optimized lookups.
*   The **runtime profiler** monitors the system being run and identifies “hot” functions (i.e. code that ends up spending a long time running).
*   An **optimizing compiler** recompiles and optimizes the “hot” code identified by the runtime profiler, and performs optimizations such as inlining (i.e. replacing a function call site with the body of the callee).
*   V8 supports **deoptimization**, meaning the optimizing compiler can bail out of code generated if it discovers that some of the assumptions it made about the optimized code were too optimistic.
*   It has a **garbage collector**. Understanding how it works can be just as important as the optimized JavaScript.</p>

## Garbage Collection

Garbage collection is <strong>a form of memory management</strong>. It's where we have the notion of a collector which attempts to reclaim memory occupied by objects that are no longer being used. In a garbage-collected language such as JavaScript, objects that are still referenced by your application are not cleaned up.

Manually de-referencing objects is not necessary in most cases. By simply putting the variables where they need to be (ideally, as local as possible, i.e. inside the function where they are used versus an outer scope), things should just work.

<a href="https://www.flickr.com/photos/26817893@N05/2864644153/"><img loading="lazy" decoding="async" title="Garbage Collection Attempts To Reclaim Memory" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/19e345c6-a8a5-4728-84b5-51f5f19ab661/robot-cleaner.jpg" alt="javascript performance" width="500" height="456" /></a><br>
<em>Garbage collection attempts to reclaim memory. Image source: <a href="https://www.flickr.com/photos/26817893@N05/2864644153/">Valtteri Mäki</a>.</em>

It's not possible to force garbage collection in JavaScript. You wouldn't want to do this, because the garbage collection process is controlled by the runtime, and it generally knows best when things should be cleaned up.</p>

### De-Referencing Misconceptions

In quite a few discussions online about reclaiming memory in JavaScript, the <code>delete</code> keyword is brought up, as although it was supposed to be used for just removing keys from a map, some developers think you can force de-referencing using it. Avoid using <code>delete</code> if you can. In the below example, <code>delete o.x</code> does a lot more harm than good behind the scenes, as it changes <code>o</code>'s hidden class and makes it a generic slow object.

<pre><code class="language-javascript">var o = { x: 1 };
delete o.x; // true
o.x; // undefined</code></pre>

That said, you are almost certain to find references to <code>delete</code> in many popular JavaScript libraries - it does have a purpose in the language. The main takeaway here is to avoid modifying the structure of hot objects at runtime. JavaScript engines can detect such "hot" objects and attempt to optimize them. This is easier if the object's structure doesn't heavily change over its lifetime and <code>delete</code> can trigger such changes.

There are also misconceptions about how <code>null</code> works. Setting an object reference to <code>null</code> doesn't “null” the object. It sets the object reference to <code>null</code>. Using <code>o.x = null</code> is better than using <code>delete</code>, but it's probably not even necessary.

<pre><code class="language-javascript">var o = { x: 1 };
o = null;
o; // null
o.x // TypeError</code></pre>

If this reference was the last reference to the object, the object is then eligible for garbage collection. If the reference was not the last reference to the object, the object is reachable and will not be garbage collected.

Another important note to be aware of is that global variables are not cleaned up by the garbage collector during the life of your page. Regardless of how long the page is open, variables scoped to the JavaScript runtime global object will stick around.

<pre><code class="language-javascript">var myGlobalNamespace = {};</code></pre>

Globals are cleaned up when you refresh the page, navigate to a different page, close tabs or exit your browser. Function-scoped variables get cleaned up when a variable falls out of scope. When functions have exited and there aren't any more references to it, the variable gets cleaned up.</p>

### Rules of Thumb

To give the garbage collector a chance to collect as many objects as possible as early as possible, <strong>don't hold on to objects you no longer need</strong>. This mostly happens automatically; here are a few things to keep in mind.

*   As mentioned earlier, a better alternative to manual de-referencing is to use variables with an appropriate scope. I.e. instead of a global variable that's nulled out, just use a function-local variable that goes out of scope when it's no longer needed. This means cleaner code with less to worry about.
*   Ensure that you're unbinding event listeners where they are no longer required, especially when the DOM objects they're bound to are about to be removed
*   If you're using a data cache locally, make sure to clean that cache or use an aging mechanism to avoid large chunks of data being stored that you're unlikely to reuse

### Functions

Next, let's look at functions. As we've already said, garbage collection works by reclaiming blocks of memory (objects) which are no longer reachable. To better illustrate this, here are some examples.

<pre><code class="language-javascript">function foo() {
    var bar = new LargeObject();
    bar.someCall();
}</code></pre>

When <code>foo</code> returns, the object which <code>bar</code> points to is automatically available for garbage collection, because there is nothing left that has a reference to it.

Compare this to:

<pre><code class="language-javascript">function foo() {
    var bar = new LargeObject();
    bar.someCall();
    return bar;
}

// somewhere else
var b = foo();</code></pre>

We now have a reference to the object which survives the call and persists until the caller assigns something else to <code>b</code> (or <code>b</code> goes out of scope).</p>

### Closures

When you see a function that returns an inner function, that inner function will have access to the outer scope even after the outer function is executed. This is basically a <a href="https://robertnyman.com/2008/10/09/explaining-javascript-scope-and-closures/">closure</a> — an expression which can work with variables set within a specific context. For example:

<pre><code class="language-javascript">function sum (x) {
    function sumIt(y) {
        return x + y;
    };
    return sumIt;
}

// Usage
var sumA = sum(4);
var sumB = sumA(3);
console.log(sumB); // Returns 7</code></pre>

The function object created within the execution context of the call to <code>sum</code> can't be garbage collected, as it's referenced by a global variable and is still very much accessible. It can still be executed via <code>sumA(n)</code>.

Let's look at another example. Here, can we access <code>largeStr</code>?

<pre><code class="language-javascript">var a = function () {
    var largeStr = new Array(1000000).join('x');
    return function () {
        return largeStr;
    };
}();</code></pre>

Yes, we can, via <code>a()</code>, so it's not collected. How about this one?

<pre><code class="language-javascript">var a = function () {
    var smallStr = 'x';
    var largeStr = new Array(1000000).join('x');
    return function (n) {
        return smallStr;
    };
}();</code></pre>

We can't access it anymore and it's a candidate for garbage collection.</p>

### Timers

One of the worst places to leak is in a loop, or in <code>setTimeout()</code>/<code>setInterval()</code>, but this is quite common.

Consider the following example.

<pre><code class="language-javascript">var myObj = {
    callMeMaybe: function () {
        var myRef = this;
        var val = setTimeout(function () {
            console.log('Time is running out!');
            myRef.callMeMaybe();
        }, 1000);
    }
};</code></pre>

If we then run:

<pre><code class="language-javascript">myObj.callMeMaybe();</code></pre>

to begin the timer, we can see every second “Time is running out!” If we then run:

<pre><code class="language-javascript">myObj = null;</code></pre>

The timer will still fire. <code>myObj</code> won't be garbage collected as the closure passed to <code>setTimeout</code> has to be kept alive in order to be executed. In turn, it holds references to <code>myObj</code> as it captures <code>myRef</code>. This would be the same if we'd passed the closure to any other function, keeping references to it.

It is also worth keeping in mind that references inside a <code>setTimeout</code>/<code>setInterval</code> call, such as functions, will need to execute and complete before they can be garbage collected.</p>

## Be Aware Of Performance Traps

It's important never to optimize code until you actually need to. This can't be stressed enough. It's easy to see a number of micro-benchmarks showing that N is more optimal than M in V8, but test it in a real module of code or in an actual application, and <strong>the true impact of those optimizations may be much more minimal</strong> than you were expecting.

<a href="https://www.flickr.com/photos/tim_uk/7717078488/sizes/c/in/photostream/"><img title="Speed Trap" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ae57923-ff1a-4c31-8a89-6fdade383677/speed-trap.jpg" alt="Speed trap." width="500" height="350" /></a><br>
<em>Doing too much can be as harmful as not doing anything. Image source: <a href="https://www.flickr.com/photos/tim_uk/7717078488/sizes/c/in/photostream/">Tim Sheerman-Chase</a>.</em>

Let's say we want to create a module which:

*   Takes a local source of data containing items with a numeric ID,
*   Draws a table containing this data,
*   Adds event handlers for toggling a class when a user clicks on any cell.

There are a few different factors to this problem, even though it's quite straightforward to solve. How do we store the data? How do we efficiently draw the table and append it to the DOM? How do we handle events on this table optimally?

A first (naive) take on this problem might be to store each piece of available data in an object which we group into an array. One might use jQuery to iterate through the data and draw the table, then append it to the DOM. Finally, one might use event binding for adding the click behavior we desire.

<strong>Note: This is NOT what you should be doing</strong>

<pre><code class="language-javascript">var moduleA = function () {

    return {

        data: dataArrayObject,

        init: function () {
            this.addTable();
            this.addEvents();
        },

        addTable: function () {

            for (var i = 0; i &lt; rows; i++) {
                $tr = $('&lt;tr&gt;&lt;/tr&gt;');
                for (var j = 0; j &lt; this.data.length; j++) {
                    $tr.append('&lt;td&gt;' + this.data[j]['id'] + '&lt;/td&gt;');
                }
                $tr.appendTo($tbody);
            }

        },
        addEvents: function () {
            $('table td').on('click', function () {
                $(this).toggleClass('active');
            });
        }

    };
}();</code></pre>

Simple, but it gets the job done.

In this case however, the only data we're iterating are IDs, a numeric property which could be more simply represented in a standard array. Interestingly, directly using <code>DocumentFragment</code> and native DOM methods are more optimal than using jQuery (in this manner) for our table generation, and of course, event delegation is typically more performant than binding each <code>td</code> individually.

Note that jQuery does use <code>DocumentFragment</code> internally behind the scenes, but in our example, the code is calling <code>append()</code> within a loop and each of these calls has little knowledge of the other so it may not be able to optimize for this example. This should hopefully not be a pain point, but be sure to benchmark your own code to be sure.

In our case, adding in these changes results in some good (expected) performance gains. Event delegation provides decent improvement over simply binding, and <a href="https://jsperf.com/first-pass">opting for <code>documentFragment</code></a> was a real booster.

<pre><code class="language-javascript">var moduleD = function () {

    return {

        data: dataArray,

        init: function () {
            this.addTable();
            this.addEvents();
        },
        addTable: function () {
            var td, tr;
            var frag = document.createDocumentFragment();
            var frag2 = document.createDocumentFragment();

            for (var i = 0; i &lt; rows; i++) {
                tr = document.createElement('tr');
                for (var j = 0; j &lt; this.data.length; j++) {
                    td = document.createElement('td');
                    td.appendChild(document.createTextNode(this.data[j]));

                    frag2.appendChild(td);
                }
                tr.appendChild(frag2);
                frag.appendChild(tr);
            }
            tbody.appendChild(frag);
        },
        addEvents: function () {
            $('table').on('click', 'td', function () {
                $(this).toggleClass('active');
            });
        }

    };

}();</code></pre>

We might then look to other ways of improving performance. You may have read somewhere that using the prototypal pattern is more optimal than the module pattern (we confirmed it wasn't earlier), or heard that using JavaScript templating frameworks are highly optimized. Sometimes they are, but use them because they make for readable code. Also, precompile!. Let's test and find out how true this hold in practice.

<pre><code class="language-javascript">moduleG = function () {};

moduleG.prototype.data = dataArray;
moduleG.prototype.init = function () {
    this.addTable();
    this.addEvents();
};
moduleG.prototype.addTable = function () {
    var template = _.template($('#template').text());
    var html = template({'data' : this.data});
    $tbody.append(html);
};
moduleG.prototype.addEvents = function () {
   $('table').on('click', 'td', function () {
       $(this).toggleClass('active');
   });
};

var modG = new moduleG();</code></pre>

As it turns out, in this case the performance benefits are negligible. <a href="https://jsperf.com/second-pass">Opting for templating and prototypes</a> didn't really offer anything more than what we had before. That said, performance isn't really the reason modern developers use either of these things — it's the readability, inheritance model and maintainability they bring to your codebase.

More complex problems include efficiently drawing images using canvas and <a href="https://jsperf.com/canvas-pixel-manipulation/30">manipulating pixel data</a> with or without <a href="https://jsperf.com/typed-arrays-for-pixel-manipulation">typed arrays</a>

Always give micro-benchmarks a close lookover before exploring their use in your application. Some of you may recall the <a href="https://jsperf.com/dom-vs-innerhtml-based-templating/473">JavaScript templating shoot-off</a> and the <a href="https://jsperf.com/javascript-templating-shootoff-extended/26">extended shoot-off that followed</a>. You want to make sure that tests aren't being impacted by constraints you're unlikely to see in real world applications — test optimizations together in actual code.</p>

## V8 Optimization Tips

Whilst detailing every V8 optimization is outside the scope of this article, there are certainly many tips worth noting. Keep these in mind and you'll reduce your chances of writing unperformant code.

*   Certain patterns will cause V8 to bail out of optimizations. A try-catch, for example, will cause such a bailout. For more information on what functions can and can't be optimized, you can use `--trace-opt file.js` with the d8 shell utility that comes with V8.
*   If you care about speed, try very hard to keep your functions monomorphic, i.e. make sure that variables (including properties, arrays and function parameters) only ever contain objects with the same hidden class. For example, don't do this:

<pre><code class="language-javascript">function add(x, y) {
   return x+y;
}

add(1, 2);
add('a','b');
add(my_custom_object, undefined);</code></pre>

*   Don't load from uninitialized or deleted elements. This won't make a difference in output, but it will make things slower.
*   Don't write enormous functions, as they are more difficult to optimize

For more tips, watch Daniel Clifford's Google I/O talk <a href="https://youtube.com/watch?v=UJPdhx5zTaw">Breaking the JavaScript Speed Limit with V8</a> as it covers these topics well. <a href="https://floitsch.blogspot.co.uk/2012/03/optimizing-for-v8-introduction.html">Optimizing For V8 — A Series</a> is also worth a read.</p>

### Objects Vs. Arrays: Which Should I Use?

*   If you want to store a bunch of numbers, or a list of objects of the same type, use an array.
*   If what you semantically need is an object with a bunch of properties (of varying types), use an object with properties. That's pretty efficient in terms of memory, and it's also pretty fast.
*   Integer-indexed elements, regardless of whether they're stored in an array or an object, are [much faster to iterate over than object properties](https://jsperf.com:80/performance-of-array-vs-object/3).
*   Properties on objects are quite complex: they can be created with setters, and with differing enumerability and writability. Items in arrays aren't able to be customized as heavily — they either exist or they don't. At an engine level, this allows for more optimization in terms of organizing the memory representing the structure. This is particularly beneficial when the array contains numbers. For example, when you need vectors, don't define a class with properties x, y, z; use an array instead..

There’s really only one major difference between objects and arrays in JavaScript, and that's the arrays' magic <code>length</code> property. If you’re keeping track of this property yourself, objects in V8 should be just as fast as arrays.</p>

### Tips When Using Objects

*   Create objects using a constructor function. This ensures that all objects created with it have the same hidden class and helps avoid changing these classes.
*   There are no restrictions on the number of different object types you can use in your application or on their complexity (within reason: long prototype chains tend to hurt, and objects with only a handful of properties get a special representation that's a bit faster than bigger objects). For “hot” objects, try to keep the prototype chains short and the field count low.

<strong>Object Cloning</strong>
Object cloning is a common problem for app developers. While it's possible to benchmark how well various implementations work with this type of problem in V8, be very careful when copying anything. Copying big things is generally slow — don't do it. <code>for..in</code> loops in JavaScript are particularly bad for this, as they have a devilish specification and will likely never be fast in any engine for arbitrary objects.

When you absolutely do need to copy objects in a performance-critical code path (and you can't get out of this situation), use an array or a custom “copy constructor” function which copies each property explicitly. This is probably the fastest way to do it:

<pre><code class="language-javascript">function clone(original) {
  this.foo = original.foo;
  this.bar = original.bar;
}
var copy = new clone(original);</code></pre>

<strong>Cached Functions in the Module Pattern</strong>
Caching your functions when using the module pattern can lead to performance improvements. See below for an example where the variation you're probably used to seeing is slower as it forces new copies of the member functions to be created all the time.

<img title="Performance Improvements When Using The Module And Prototypal Patterns" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cbb2c9a3-1b1d-41c2-ae45-c21c8f748813/screen-shot-2012-11-06-at-10.42" alt="Performance improvements" width="500" height="253" /><br>
<em>Performance improvements when using the module or prototypal patterns.</em>

Here is a <a href="https://jsperf.com:80/prototypal-performance/12">test of prototype versus module pattern performance</a>

<pre><code class="language-javascript">// Prototypal pattern
  Klass1 = function () {}
  Klass1.prototype.foo = function () {
      log('foo');
  }
  Klass1.prototype.bar = function () {
      log('bar');
  }

  // Module pattern
  Klass2 = function () {
      var foo = function () {
          log('foo');
      },
      bar = function () {
          log('bar');
      };

      return {
          foo: foo,
          bar: bar
      }
  }

  // Module pattern with cached functions
  var FooFunction = function () {
      log('foo');
  };
  var BarFunction = function () {
      log('bar');
  };

  Klass3 = function () {
      return {
          foo: FooFunction,
          bar: BarFunction
      }
  }

  // Iteration tests

  // Prototypal
  var i = 1000,
      objs = [];
  while (i--) {
      var o = new Klass1()
      objs.push(new Klass1());
      o.bar;
      o.foo;
  }

  // Module pattern
  var i = 1000,
      objs = [];
  while (i--) {
      var o = Klass2()
      objs.push(Klass2());
      o.bar;
      o.foo;
  }

  // Module pattern with cached functions
  var i = 1000,
      objs = [];
  while (i--) {
      var o = Klass3()
      objs.push(Klass3());
      o.bar;
      o.foo;
  }
// See the test for full details</code></pre>

<strong>Note:</strong> If you don't require a class, avoid the trouble of creating one. Here's an <a href="https://jsperf.com/prototypal-performance/54">example of how to gain performance boosts by remoxing the class overhead altogether</a>.</p>

### Tips When Using Arrays

Next let's look at a few tips for arrays. In general, <strong>don't delete array elements</strong>. It would make the array transition to a slower internal representation. When the key set becomes sparse, V8 will eventually switch elements to dictionary mode, which is even slower.

<strong>Array Literals</strong>
Array literals are useful because they give a hint to the VM about the size and type of the array. They're typically good for small to medium sized arrays.

<pre><code class="language-javascript">// Here V8 can see that you want a 4-element array containing numbers:
var a = [1, 2, 3, 4];

// Don't do this:
a = []; // Here V8 knows nothing about the array
for(var i = 1; i &lt;= 4; i++) {
     a.push(i);
}</code></pre>

<strong>Storage of Single Types Vs. Mixed Types</strong>
It’s never a good idea to mix values of different types (e.g. numbers, strings, undefined or true/false) in the same array (i.e. <code>var arr = [1, “1”, undefined, true, “true”]</code>)

<a href="https://jsperf.com:80/type-inference-performance/2">Test of type inference performance</a>

As we can see from the results, the array of <code>ints</code> is the fastest.

<strong>Sparse Arrays vs. Full Arrays</strong>
When you use sparse arrays, be aware that accessing elements in them is much slower than in full arrays. That's because V8 doesn't allocate a flat backing store for the elements if only a few of them are used. Instead, it manages them in a dictionary, which saves space, but costs time on access.

<a href="https://jsperf.com:80/sparse-arrays-vs-full-arrays">Test of sparse arrays versus full arrays</a>.

The full array <code>sum</code> and <code>sum</code> of all elements on an array without zeros were actually the fastest. Whether the full array contains zeroes or not should not make a difference.

<strong>Packed Vs. Holey Arrays</strong>
Avoid “holes” in an array (created by deleting elements or <code>a[x] = foo</code> with <code>x &gt; a.length</code>). Even if only a single element is deleted from an otherwise “full” array, things will be much slower.

<a href="https://jsperf.com/packed-vs-holey-arrays">Test of packed versus holey arrays</a>.

<strong>Pre-allocating Arrays Vs. Growing As You Go</strong>
Don't pre-allocate large arrays (i.e. greater than 64K elements) to their maximum size, instead grow as you go. Before we get to the performance tests for this tip, keep in mind that this is specific to only some JavaScript engines.

<img title="Empty Literal VS. Pre-Allocated Array In Various Browsers" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f74460f8-d608-4c67-a73a-5d9fcbe042ee/graph2.jpg" alt="Test of empty literal versus pre-allocated arrays in various browsers." width="500" height="323" /><br>
<em>Test of empty literal versus pre-allocated array in various browsers.</em>

Nitro (Safari) actually treats pre-allocated arrays more favorably. However, in other engines (V8, SpiderMonkey), not pre-allocating is more efficient.

<a href="https://jsperf.com/pre-allocated-arrays">Test of pre-allocated arrays</a>.

<pre><code class="language-javascript">// Empty array
var arr = [];
for (var i = 0; i &lt; 1000000; i++) {
    arr[i] = i;
}

// Pre-allocated array
var arr = new Array(1000000);
for (var i = 0; i &lt; 1000000; i++) {
    arr[i] = i;
}</code></pre>

## Optimizing Your Application

In the world of Web applications, <strong>speed is everything</strong>. No user wants a spreadsheet application to take seconds to sum up an entire column or a summary of their messages to take a minute before it's ready. This is why squeezing every drop of extra performance you can out of code can sometimes be critical.

<a href="https://www.flickr.com/photos/perolofforsberg/6691744587/in/photostream/"><img title="Old Phone On iPad Screen" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/90cd1dea-9200-44fd-a766-b69dc8ecc851/improving-apps.jpg" alt="An old phone on the screen of an iPad." width="500" height="375" /></a><br>
<em>Image source: <a href="https://www.flickr.com/photos/perolofforsberg/6691744587/in/photostream/">Per Olof Forsberg</a>.</em>

While understanding and improving your application performance is useful, it can also be difficult. We recommend the following steps to fix performance pain points:

*   Measure it: Find the slow spots in your application (~45%)
*   Understand it: Find out what the actual problem is (~45%)
*   Fix it! (~10%)

Some of the tools and techniques recommended below can assist with this process.</p>

### Benchmarking

There are many ways to run benchmarks on JavaScript snippets to test their performance — the general assumption being that benchmarking is simply comparing two timestamps. One such pattern was pointed out by the <a href="https://jsperf.com/">jsPerf</a> team, and happens to be used in <a href="https://www.webkit.org/perf/sunspider/sunspider.html">SunSpider</a>'s and <a href="https://krakenbenchmark.mozilla.org/">Kraken</a>'s benchmark suites:

<pre><code class="language-javascript">var totalTime,
    start = new Date,
    iterations = 1000;
while (iterations--) {
  // Code snippet goes here
}
// totalTime → the number of milliseconds taken
// to execute the code snippet 1000 times
totalTime = new Date - start;</code></pre>

Here, the code to be tested is placed within a loop and run a set number of times (e.g. six). After this, the start date is subtracted from the end date to find the time taken to perform the operations in the loop.

However, this oversimplifies how benchmarking should be done, especially if you want to run the benchmarks in multiple browsers and environments. Garbage collection itself can have an impact on your results. Even if you're using a solution like <code>window.performance</code>, you still have to account for these pitfalls.

Regardless of whether you are simply running benchmarks against parts of your code, writing a test suite or coding a benchmarking library, there's a lot more to JavaScript benchmarking than you might think. For a more detailed guide to benchmarking, I highly recommend reading <a href="https://mathiasbynens.be/notes/javascript-benchmarking">JavaScript Benchmarking</a> by Mathias Bynens and John-David Dalton.</p>

### Profiling

The Chrome Developer Tools have good support for <a href="https://developers.google.com/web/tools/chrome-devtools/#profiles-panel-profile-execution-time-and-memory-usage">JavaScript profiling</a>. You can use this feature to detect what functions are eating up the most of your time so that you can then go optimize them. This is important, as even small changes to your codebase can have serious impacts on your overall performance.

<img title="Profiles Panel In Chrome Developer Tools" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d676824a-42a8-4412-91db-16e6c506a97d/profiling.jpg" alt="Profiles panel in Chrome Developer Tools." width="500" height="315" /><br>
<em>Profiles Panel in Chrome Developer Tools.</em>

Profiling starts with obtaining a baseline for your code's current performance, which can be discovered using the Timeline. This will tell us how long our code took to run. The Profiles tab then gives us a better view into what's happening in our application. The JavaScript CPU profile shows us how much CPU time is being used by our code, the CSS selector profile shows us how much time is spent processing selectors and Heap snapshots show how much memory is being used by our objects.

Using these tools, we can isolate, tweak and reprofile to gauge whether changes we're making to specific functions or operations are improving performance.

<img title="The Profile Tab Gives Information About Your Code's Performance" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b768f0e-39f5-4cbd-b696-64751e2e6b9d/profiling2.jpg" alt="The profile tab gives information about your code's performance." width="500" height="293" /><br>
<em>The Profile tab gives you information about your code's performance.</em>

For a good introduction to profiling, read <a href="https://www.smashingmagazine.com/2012/06/12/javascript-profiling-chrome-developer-tools/">JavaScript Profiling With The Chrome Developer Tools</a>, by Zack Grossbart.

Tip: Ideally, you want to ensure that your profiling isn't being affected by extensions or applications you've installed, so run Chrome using the <code>--user-data-dir &lt;empty_directory&gt;</code> flag. Most of the time, this approach to optimization testing should be enough, but there are times when you need more. This is where V8 flags can be of help.</p>

### Avoiding Memory Leaks — Three Snapshot Techniques for Discovery

Internally at Google, the Chrome Developer Tools are heavily used by teams such as Gmail to help us discover and squash memory leaks.

<img title="Memory Statistics In Chrome Developer Tools" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/85ade6fa-0340-4cc3-9bf2-9476f2377bae/devtools.jpg" alt="Memory statistics in Chrome Developer Tools." width="500" height="283" /><br>
<em>Memory statistics in Chrome Developer Tools.</em>

Some of the memory statistics that our teams care about include private memory usage, JavaScript heap size, DOM node counts, storage clearing, event listener counts and what's going on with garbage collection. For those familiar with event-driven architectures, you might be interested to know that one of the most common issues we used to have were <code>listen()</code>’s without <code>unlisten()</code>’s (Closure) and missing <code>dispose()</code>’s for objects that create event listeners.

Luckily the DevTools can help locate some of these issues, and Loreena Lee has a fantastic presentation available documenting the <a href="https://docs.google.com/presentation/d/1wUVmf78gG-ra5aOxvTfYdiLkdGaR9OhXRnOlIcEmu2s/pub?start=false&amp;loop=false&amp;delayms=3000#slide=id.g1d65bdf6_0_0">"3 snapshot" technique</a> for finding leaks within the DevTools that I can't recommend reading through enough.

The gist of the technique is that you record a number of actions in your application, force a garbage collection, check if the number of DOM nodes doesn't return to your expected baseline and then analyze three heap snapshots to determine if you have a leak.</p>

### Memory Management in Single-Page Applications

Memory management is quite important when writing modern single-page applications (e.g. AngularJS, Backbone, Ember) as they almost never get refreshed. This means that memory leaks can become apparent quite quickly. This is a huge trap on mobile single-page applications, because of limited memory, and on long-running applications like email clients or social networking applications. <strong>With great power comes great responsibility.</strong>

There are various ways to prevent this. In Backbone, ensure you always dispose old views and references using <code>dispose()</code> (currently available in <a href="https://github.com/documentcloud/backbone/blob/master/backbone.js#L1234">Backbone (edge)</a>). This function was recently added, and removes any handlers added in the view's 'events' object, as well as any collection or model listeners where the view is passed as the third argument (callback context). <code>dispose()</code> is also called by the view's <code>remove()</code>, taking care of the majority of basic memory cleanup needs when the element is <a href="https://github.com/documentcloud/backbone/blob/master/backbone.js#L1235">cleared from the screen</a>. Other libraries like Ember <a href="https://github.com/emberjs/ember.js/blob/d8f76a7fdde741ae3d1e07b12df9cb6718170e48/packages/ember-handlebars/lib/helpers/binding.js#L296">clean up observers</a> when they detect that elements have been removed from view to avoid memory leaks.

Some sage advice from Derick Bailey:
<blockquote>“Other than being aware of how events work in terms of references, just follow the standard rules for manage memory in JavaScript and you’ll be fine. If you are loading data in to a Backbone collection full of User objects you want that collection to be cleaned up so it’s not using anymore memory, you must remove all references to the collection and the individual objects in it. Once you remove all references, things will be cleaned up. This is just the standard JavaScript garbage collection rule.”</blockquote>

In his article, Derick covers many of the common <a href="https://lostechies.com/derickbailey/2012/03/19/backbone-js-and-javascript-garbage-collection/">memory pitfalls</a> when working with Backbone.js and how to fix them.

There is also a helpful tutorial available for <a href="https://github.com/felixge/node-memory-leak-tutorial">debugging memory leaks in Node</a> by Felix Geisendörfer worth reading, especially if it forms a part of your broader SPA stack.</p>

### Minimizing Reflows

When a browser has to recalculate the positions and geometrics of elements in a document for the purpose of re-rendering it, we call this <a href="https://www.youtube.com/watch?feature=player_embedded&amp;v=ZHxbs5WEQzE">reflow</a>. Reflow is a user-blocking operation in the browser, so it's helpful to understand how to improve reflow time.

<img title="Chart Of Reflow Time" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/36d4aab3-9a2b-4bd2-802e-137b920f0b44/reflow.jpg" alt="Chart of reflow time." width="500" height="310" /><br>
<em>Chart of reflow time.</em>

You should batch methods that <a href="https://stackoverflow.com/questions/510213/when-does-reflow-happen-in-a-dom-environment">trigger reflow</a> or that repaint, and use them sparingly. It’s important to process off DOM where possible. This is possible using <a href="https://www.w3.org/TR/DOM-Level-2-Core/core.html#ID-B63ED1A3">DocumentFragment</a>, a lightweight document object. Think of it as a way to extract a portion of a document’s tree, or create a new “fragment” of a document. Rather than constantly adding to the DOM using nodes, we can use document fragments to build up all we need and only perform a single insert into the DOM to avoid excessive reflow.

For example, let's write a function that adds 20 <code>div</code>s to an element. Simply appending each new <code>div</code> directly to the element could trigger 20 reflows.

<pre><code class="language-javascript">function addDivs(element) {
  var div;
  for (var i = 0; i &lt; 20; i ++) {
    div = document.createElement('div');
    div.innerHTML = 'Heya!';
    element.appendChild(div);
  }
}</code></pre>

To work around this issue, we can use <code>DocumentFragment</code>, and instead, append each of our new <code>div</code>s to this. When appending to the <code>DocumentFragment</code> with a method like <code>appendChild</code>, all of the fragment's children are appended to the element triggering only one reflow.

<pre><code class="language-javascript">function addDivs(element) {
  var div;
  // Creates a new empty DocumentFragment.
  var fragment = document.createDocumentFragment();
  for (var i = 0; i &lt; 20; i ++) {
    div = document.createElement('a');
    div.innerHTML = 'Heya!';
    fragment.appendChild(div);
  }
  element.appendChild(fragment);
}</code></pre>

You can read more about this topic at <a href="https://developers.google.com/speed/articles/javascript-dom">Make the Web Faster</a>,
<a href="https://blog.tojicode.com/2012/03/javascript-memory-optimization-and.html">JavaScript Memory Optimization</a> and <a href="https://gent.ilcore.com/2011/08/finding-memory-leaks.html">Finding Memory Leaks</a>.</p>

### JavaScript Memory Leak Detector

To help discover JavaScript memory leaks, two of my fellow Googlers (Marja Hölttä and Jochen Eisinger) developed a tool that works with the Chrome Developer Tools (specifically, the remote inspection protocol), and retrieves heap snapshots and detects what objects are causing leaks.

<img title="A Tool For Detecting JavaScript Memory Leaks" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dfb62c17-2eb4-478a-b4d5-da852ba850a3/leak.jpg" alt="A tool for detecting JavaScript memory leaks." width="500" height="271" /><br>
<em>A tool for detecting JavaScript memory leaks.</em>

There's a whole post on <a href="https://google-opensource.blogspot.de/2012/08/leak-finder-new-tool-for-javascript.html">how to use the tool</a>, and I encourage you to check it out or view the <a href="https://code.google.com/p/leak-finder-for-javascript/">Leak Finder project page</a>.

Some more information: In case you're wondering why a tool like this isn't already integrated with our Developer Tools, the reason is twofold. It was originally developed to help us catch some specific memory scenarios in the Closure Library, and it makes more sense as an external tool (or maybe even an extension if we get a heap profiling extension API in place).</p>

### V8 Flags for Debugging Optimizations & Garbage Collection

Chrome supports passing a number of flags directly to V8 via the <code>js-flags</code> flag to get more detailed output about what the engine is optimizing. For example, this traces V8 optimizations:

<pre><code class="language-javascript">"/Applications/Google Chrome/Google Chrome" --js-flags="--trace-opt --trace-deopt"</code></pre>

Windows users will want to run <code>chrome.exe --js-flags="--trace-opt --trace-deopt"</code>

When developing your application, the following V8 flags can be used.

*   `trace-opt` - log names of optimized functions and show where the optimizer is skipping code because it can't figure something out.
*   `trace-deopt` - log a list of code it had to deoptimize while running.
*   `trace-gc` - logs a tracing line on each garbage collection.

V8’s tick-processing scripts mark optimized functions with an <code>*</code> (asterisk) and non-optimized functions with <code>~</code> (tilde).

If you're interested in learning more about V8's flags and how V8's internals work in general, I strongly recommend looking through Vyacheslav Egorov's <a href="https://mrale.ph/blog/2011/12/18/v8-optimization-checklist.html">excellent post on V8 internals</a>, which summarizes the best resources available on this at the moment.</p>

### High-Resolution Time and Navigation Timing API

<a href="https://www.w3.org/TR/hr-time/">High Resolution Time</a> (HRT) is a JavaScript interface providing the current time in sub-millisecond resolution that isn't subject to system clock skews or user adjustments. Think of it as a way to measure more precisely than we've previously had with <code>new Date</code> and <code>Date.now()</code>. This is helpful when we're writing performance benchmarks.

<img title="High Resolution Time (HRT) Provides The Current Time In Sub-Millisecond Resolution" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/529f7e3a-74fa-4a30-bbf5-ee08c3902e1c/perfnow.jpg" alt="High Resolution Time (HRT) provides the current time in sub-millisecond resolution." width="500" height="143" /><br>
<em>High Resolution Time (HRT) provides the current time in sub-millisecond resolution.</em>

HRT is currently available in Chrome (stable) as <code>window.performance.webkitNow()</code>, but the prefix is dropped in Chrome Canary, making it available via <code>window.performance.now()</code>. Paul Irish has written <a href="https://updates.html5rocks.com/2012/08/When-milliseconds-are-not-enough-performance-now">more about HRT</a> in a post on HTML5Rocks.

So, we now know the current time, but what if we wanted an API for accurately measuring performance on the web?

Well, one is now also available in the <a href="https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming/Overview.html">Navigation Timing API</a>. This API provides a simple way to get accurate and detailed time measurements that are recorded while a webpage is loaded and presented to the user. Timing information is exposed via <code>window.performance.timing</code>, which you can simply use in the console:

<img title="Timing Information Is Shown In The Console" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c5def3c3-d80c-4a14-a5b3-c67eae66c640/performance.jpg" alt="Timing information is shown in the console." width="500" height="292" /><br>
<em>Timing information is shown in the console.</em>

Looking at the data above, we can extract some very useful information. For example, network latency is <code>responseEnd-fetchStart</code>, the time taken for a page load once it's been received from the server is <code>loadEventEnd-responseEnd</code> and the time taken to process between navigation and page load is <code>loadEventEnd-navigationStart</code>.

As you can see above, a <code>perfomance.memory</code> property is also available that gives access to JavaScript memory usage data such as the total heap size.

For more details on the Navigation Timing API, read Sam Dutton's great article <a href="https://www.html5rocks.com/en/tutorials/webperformance/basics/">Measuring Page Load Speed With Navigation Timing</a>.</p>

### about:memory and about:tracing

<code>about:tracing</code> in Chrome offers an intimate view of the browser’s performance, recording all of Chrome’s activities across every thread, tab and process.

<img title="About:Tracing Offers An Intimate View Of The Browser’s Performance" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c8857654-0e74-45dd-949c-be8486204267/tracing.jpg" alt="about:tracing offers an intimate view of the browser’s performance." width="500" height="275" /><br>
<em><code>About:Tracing</code> offers an intimate view of the browser’s performance.</em>

What’s really useful about this tool is that it allows you to capture profiling data about what Chrome is doing under the hood, so you can properly adjust your JavaScript execution, or optimize your asset loading.

Lilli Thompson has an excellent <a href="https://www.html5rocks.com/en/tutorials/games/abouttracing/">write-up for games developers</a> on using <code>about:tracing</code> to profile WebGL games. The write-up is also useful for general JavaScripters.

Navigating to <code>about:memory</code> in Chrome is also useful as it shows the exact amount of memory being used by each tab, which is helpful for tracking down potential leaks.</p>

## Conclusion

As we've seen, <strong>there are many hidden performance gotchas in the world of JavaScript engines</strong>, and no silver bullet available to improve performance. It's only when you combine a number of optimizations in a (real-world) testing environment that you can realize the largest performance gains. But even then, understanding how engines interpret and optimize your code can give you insights to help tweak your applications.

<strong>Measure It. Understand it. Fix it.</strong> Rinse and repeat.

<a href="https://www.flickr.com/photos/38891164@N02/4266609887/"><img title="Measuring" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a92f842e-ffae-4986-bb85-ba0bb1b9f228/barometer.jpg" alt="Measuring." width="480" height="320" /></a><br>
<em>Image source: <a href="https://www.flickr.com/photos/38891164@N02/4266609887/">Sally Hunter</a>.</em>

Remember to care about optimization, but stop short of opting for micro-optimization at the cost of convenience. For example, some developers opt for <code>.forEach</code> and <code>Object.keys</code> over <code>for</code> and <code>for in</code> loops, even though they're slower, for the convenience of being able to scope. Do make sanity calls on what optimizations your application absolutely needs and which ones it could live without.

Also, be aware that although JavaScript engines continue to get faster, the next real bottleneck is the DOM. Reflows and repaints are just as important to minimize, so remember to only touch the DOM if it's absolutely required. And do care about networking. HTTP requests are precious, especially on mobile, and you should be using HTTP caching to reduce the size of assets.

Keeping all of these in mind will ensure that you get the most out of the information from this post. I hope you found it helpful!

### Credits

This article was reviewed by Jakob Kummerow, Michael Starzinger, Sindre Sorhus, Mathias Bynens, John-David Dalton and Paul Irish.

<em><a href="https://www.flickr.com/photos/26817893@N05/2864644153/">Image source</a> of picture on front page.</em>

<em>(cp) (jc)</em>


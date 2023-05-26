---
title: 'Understanding Weak Reference In JavaScript'
slug: understanding-weak-reference-javascript
author: frank-joseph
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/44544ece-23b3-48cb-b2bf-0183a32d2bee/understanding-weak-reference-javascript.jpg
date: 2022-05-25T09:30:00.000Z
summary: >-
  In this article, Frank Joseph explains both weak and strong references in JavaScript, as well as the concept of reachability. Let’s dig in!
description: >-
  In this article, Frank Joseph explains both weak and strong references in JavaScript, as well as the concept of reachability. Let’s dig in!
categories:
  - JavaScript
  - Performance
  - Coding
---

Memory and performance management are important aspects of software development and ones that every software developer should pay attention to. Though useful, weak references are not often used in JavaScript. `WeakSet` and `WeakMap` were introduced to JavaScript in the ES6 version.

## Weak Reference

To clarify, unlike strong reference, weak reference doesn’t prevent the referenced object from being reclaimed or collected by the garbage collector, even if it is the only reference to the object in memory.

Before getting into strong reference, `WeakSet`, `Set`, `WeakMap`, and `Map`, let’s illustrate weak reference with the following snippet:

<pre><code class="language-javascript">// Create an instance of the WeakMap object.
let human = new WeakMap():

// Create an object, and assign it to a variable called man.
let man = { name: "Joe Doe" };

// Call the set method on human, and pass two arguments (key and value) to it.
human.set(man, "done")

console.log(human)</code></pre>

The output of the code above would be the following:

<pre><code class="language-javascript">WeakMap {{…} =&gt; 'done'}

man = null;
console.log(human)</code></pre>

The `man` argument is now set to the `WeakMap` object. At the point when we reassigned the `man` variable to `null`, the only reference to the original object in memory was the weak reference, and it came from the `WeakMap` that we created earlier. When the JavaScript engine runs a garbage-collection process, the `man` object will be removed from memory and from the `WeakMap` that we assigned it to. This is because it is a weak reference, and it doesn’t prevent garbage collection.

It looks like we are making progress. Let’s talk about strong reference, and then we’ll tie everything together.

## Strong Reference

A strong reference in JavaScript is a reference that prevents an object from being garbage-collected. It keeps the object in memory.

The following code snippets illustrate the concept of strong reference:

<pre><code class="language-javascript">let man = {name: "Joe Doe"};

let human = [man];

man =  null;
console.log(human);</code></pre>

The result of the code above would be this:
    

<pre><code class="language-javascript">// An array of objects of length 1. 
[{…}]</code></pre>

The object cannot be accessed via the `dog` variable anymore due to the strong reference that exists between the `human` array and object. The object is retained in memory and can be accessed with the following code:

<pre><code class="language-javascript">console.log(human[0])</code></pre>

The important point to note here is that a weak reference doesn’t prevent an object from being garbage-collected, whereas a strong reference does prevent an object from being garbage-collected.

## Garbage Collection in JavaScript

As in every programming language, memory management is a key factor to consider when writing JavaScript. Unlike C, JavaScript is a high-level programming language that automatically allocates memory when objects are created and that clears memory automatically when the objects are no longer needed. The process of clearing memory when objects are no longer being used is referred to as garbage collection. It is almost impossible to talk about garbage collection in JavaScript without touching on the concept of reachability.

### Reachability

All values that are within a specific scope or that are in use within a scope are said to be “reachable” within that scope and are referred to as “reachable values”. Reachable values are always stored in memory.

Values are considered reachable if they are:

- values in the root of the program or referenced from the root, such as global variables or the currently executing function, its context, and callback;
- values accessible from the root by a reference or chain of references (for example, an object in the global variable referencing another object, which also references another object &mdash; these are all considered reachable values).

The code snippets below illustrate the concept of reachability:

<pre><code class="language-javascript">let languages = {name: “JavaScript”};</code></pre>

Here we have an object with a key-value pair (with the name `JavaScript`) referencing the global variable `languages`. If we overwrite the value of `languages` by assigning `null` to it…

<pre><code class="language-javascript">languages = null;</code></pre>

… then the object will be garbage-collected, and the value `JavaScript` cannot be accessed again. Here is another example:

<pre><code class="language-javascript">let languages = {name: “JavaScript”};

let programmer = languages;</code></pre>

From the code snippets above, we can access the object property from both the `languages` variable and the `programmer` variable. However, if we set `languages` to `null`…

<pre><code class="language-javascript">languages = null;</code></pre>

… then the object will still be in memory because it can be accessed via the `programmer` variable. This is how garbage collection works in a nutshell.

**Note:** *By default, JavaScript uses strong reference for its references. To implement weak reference in JavaScript, you would use `WeakMap`, `WeakSet`, or `WeakRef`.*

## Comparing Set and WeakSet

A set object is a collection of unique values with a single occurrence. A set, like an array, does not have a key-value pair. We can iterate through a set of arrays with the array methods `for… of` and `.forEach`.

Let’s illustrate this with the following snippets:

<pre><code class="language-javascript">let setArray = new Set(["Joseph", "Frank", "John", "Davies"]);
for (let names of setArray){
  console.log(names)
}// Joseph Frank John Davies
</code></pre>

We can use the `.forEach` iterator as well:

<pre><code class="language-javascript"> setArray.forEach((name, nameAgain, setArray) =&gt;{
   console.log(names);
 });</code></pre>

A `WeakSet` is a collection of unique objects. As the name applies, `WeakSet`s use weak reference. The following are properties of `WeakSet()`:

- It may only contain objects.
- Objects within the set can be reachable somewhere else.
- It cannot be looped through.
- Like `Set()`, `WeakSet()` has the methods `add`, `has`, and `delete`.

The code below illustrates how to use `WeakSet()` and some of the methods available:
    

<pre><code class="language-javascript">const human = new WeakSet();

let paul = {name: "Paul"};
let mary = {gender: "Mary"};

// Add the human with the name paul to the classroom. 
const classroom = human.add(paul);

console.log(classroom.has(paul)); // true

paul = null;

// The classroom will be cleaned automatically of the human paul.

console.log(classroom.has(paul)); // false</code></pre>

On line 1, we’ve created an instance of `WeakSet()`. On lines 3 and 4, we created objects and assigned them to their respective variables. On line 7, we added `paul` to the `WeakSet()` and assigned it to the `classroom` variable. On line 11, we made the `paul` reference `null`. The code on line 15 returns `false` because `WeakSet()` will be automatically cleaned; so, `WeakSet()` doesn’t prevent garbage collection.

## Comparing Map and WeakMap

As we know from the section on garbage collection above, the JavaScript engine keeps a value in memory as long as it is reachable. Let’s illustrate this with some snippets:

<pre><code class="language-javascript">let smashing = {name: "magazine"};
// The object can be accessed from the reference.

// Overwrite the reference smashing.
smashing = null;
// The object can no longer be accessed.</code></pre>

Properties of a data structure are considered reachable while the data structure is in memory, and they are usually kept in memory. If we store an object in an array, then as long as the array is in memory, the object can still be accessed even if it has no other references.

<pre><code class="language-javascript">let smashing = {name: "magazine"};

let arr = [smashing];

// Overwrite the reference.
smashing = null;
console.log(array[0]) // {name: 'magazine'}</code></pre>

We’re still able to access this object even if the reference has been overwritten because the object was saved in the array; hence, it was saved in memory as long the array is still in memory. Therefore, it was not garbage-collected. As we’ve used an array in the example above, we can use `map` too. While the `map` still exists, the values stored in it won’t be garbage-collected.

<pre><code class="language-javascript">let map = new Map();

let smashing {name: "magazine"};

map.set(smashing, "blog");

// Overwrite the reference.
smashing = null;

// To access the object.
console.log(map.keys());</code></pre>

Like an object, `map`s can hold key-value pairs, and we can access the value through the key. But with `map`s, we must use the `.get()` method to access the values.

According to Mozilla Developer Network, the `Map` object holds key-value pairs and remembers the original insertion order of the keys. Any value (both objects and [primitive values](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)) may be used as either key or value.

Unlike a `map`, `WeakMap` holds a weak reference; hence, it doesn’t prevent garbage collection from removing values that it references if those values are not strongly referenced elsewhere. Apart from this, `WeakMap` is the same as `map`. `WeakMap`s are not enumerable due to weak references.

With `WeakMap`, the keys must be objects, and the values may be a number or a string.

The snippets below illustrate how `WeakMap` works and the methods in it:

<pre><code class="language-javascript">// Create a weakMap.
let weakMap = new WeakMap();

let weakMap2 = new WeakMap();

// Create an object.
let ob = {};

// Use the set method.
weakMap.set(ob, "Done");

// You can set the value to be an object or even a function.
weakMap.set(ob, ob)

// You can set the value to undefined.
weakMap.set(ob, undefined);

// WeakMap can also be the value and the key.
weakMap.set(weakMap2, weakMap)

// To get values, use the get method.
weakMap.get(ob) // Done

// Use the has method.
weakMap.has(ob) // true

weakMap.delete(ob)

weakMap.has(ob) // false</code></pre>

One major side effect of using objects as keys in a `WeakMap` with no other references to it is that they will be automatically removed from memory during garbage collection.

## Areas of Application of WeakMap

`WeakMap` can be used in two areas of web development: caching and additional data storage.

### Caching

This a [web technique that involves](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching) saving (i.e. storing) a copy of a given resource and serving it back when requested. The result from a function can be cached so that whenever the function is called, the cached result can be reused.

Let’s see this in action. Create a file, name it `cachedResult.js`, and write the following in it:

<div class="break-out">

<pre><code class="language-javascript"> let cachedResult = new WeakMap();
 // A function that stores a result.
function keep(obj){
if(!cachedResult.has(obj){
  let result = obj;
  cachedResult.set(obj, result);
  }
return cachedResult.get(obj);
}


let obj = {name: "Frank"};

let resultSaved = keep(obj)

obj = null;

// console.log(cachedResult.size); Possible with map, not with WeakMap</code></pre>
</div>

If we had used `Map()` instead of `WeakMap()` in the code above, and there were multiple invocations on the function `keep()`, then it would only calculate the result the first time it was called, and it would retrieve it from `cachedResult` the other times. The side effect is that we’ll need to clean `cachedResult` whenever the object is not needed. With `WeakMap()`, the cached result will be automatically removed from memory as soon as the object is garbage-collected. Caching is a great means of improving software performance &mdash; it could save the costs of database usage, third-party API calls, and server-to-server requests. With caching, a copy of the result from a request is saved locally.

### Additional Data

Another important use of `WeakMap()` is additional data storage. Imagine we are building an e-commerce platform, and we have a program that counts visitors, and we want to be able to reduce the count when visitors leave. This task would be very demanding with Map, but quite easy to implement with `WeakMap()`:

<pre><code class="language-javascript">let visitorCount = new WeakMap();
function countCustomer(customer){
   let count = visitorCount.get(customer) || 0;
    visitorCount.set(customer, count + 1);
}</code></pre>

Let’s create client code for this:

<pre><code class="language-javascript">let person = {name: "Frank"};

// Taking count of person visit.
countCustomer(person)

// Person leaves.
person = null;</code></pre>

With `Map()`, we will have to clean `visitorCount` whenever a customer leaves; otherwise, it will grow in memory indefinitely, taking up space. But with `WeakMap()`, we do not need to clean `visitorCount`; as soon as a person (object) becomes unreachable, it will be garbage-collected automatically.

## Conclusion

In this article, we learned about weak reference, strong reference, and the concept of reachability, and we tried to connect them to memory management as best we could. I hope you found this article valuable. Feel free to drop a comment.

{{< signature "il, al, yk" >}}

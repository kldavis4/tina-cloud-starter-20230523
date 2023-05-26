---
title: 'ECMAScript 6 (ES6): What’s New In The Next Version Of JavaScript'
slug: es6-whats-new-next-version-javascript
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/073bcf09-a76f-4c67-9bc3-2025de0880f5/javascript-opt.jpg
date: 2015-10-28T17:04:28.000Z
author: lars-kappert
summary: >-
  You’ve probably heard about <strong>ECMAScript 6</strong> (or ES6) already. It’s the next version of JavaScript, and it has some great new features. The features have varying degrees of complexity and are useful in both simple scripts and complex applications.
description: >-
  You’ve probably heard about <strong>ECMAScript 6</strong> (or ES6) already. It’s the next version of JavaScript, and it has some great new features. The features have varying degrees of complexity and are useful in both simple scripts and complex applications.
categories:
  - Coding
  - JavaScript
  - Web Development
---
<p>In this article, we’ll discuss a hand-picked selection of ES6 features that you can use in your everyday JavaScript coding. Please note that support for these new ECMAScript 6 features is well underway in modern browsers, although support varies. If you need to support old versions of browsers that lack many ES6 features, I’ll touch on solutions that might help you start using ES6 today.</p>

<p>Most of the code samples come with an external “Run this code” link, so that you can see the code and play with it.</p>

## Variables

### let

You’re used to declaring variables using <code>var</code>. You can now use <code>let</code> as well. The subtle difference lies in scope. While <code>var</code> results in a variable with the surrounding function as its scope, the scope of a variable declared using <code>let</code> is only the block it is in.

<pre><code class="language-javascript">if(true) {
   let x = 1;
}
console.log(x); // undefined
</code></pre>

This can make for cleaner code, resulting in fewer variables hanging around. Take this classic array iteration:

<pre><code class="language-javascript">for(let i = 0, l = list.length; i &lt; l; i++) {
   // do something with list[i]
}

console.log(i); // undefined
</code></pre>

Often one would use, for example, the <code>j</code> variable for another iteration in the same scope. But with <code>let</code>, you could safely declare <code>i</code> again, since it’s defined and available only within its own block scope.</p>

### const

There is another way to declare block-scoped variables. With <code>const</code>, you declare a read-only reference to a value. You must assign a variable directly. If you try to change the variable or if you don’t a set a value immediately, then you’ll get an error:

<pre><code class="language-javascript">const MY_CONSTANT = 1;
MY_CONSTANT = 2 // Error
const SOME_CONST; // Error
</code></pre>

Note that you can still change object properties or array members:

<pre><code class="language-javascript">const MY_OBJECT = {some: 1};
MY_OBJECT.some = 'body'; // Cool
</code></pre>

{{% feature-panel %}}

## Arrow Functions

Arrow functions are a great addition to the JavaScript language. They make for short and concise code. We are introducing arrow functions early in this article so that we can take advantage of them in other examples later on. The next code snippet shows an arrow function, with the same function written in the familiar ES5 style:

<pre><code class="language-javascript">let books = [{title: 'X', price: 10}, {title: 'Y', price: 15}];

let titles = books.map( item =&gt; item.title );

// ES5 equivalent:
var titles = books.map(function(item) {
   return item.title;
});
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20books%20%3D%20%5B%7Btitle%3A%20'X'%2C%20price%3A%2010%7D%2C%20%7Btitle%3A%20'Y'%2C%20price%3A%2015%7D%5D%3B%0A%0Alet%20titles%20%3D%20books.map(%20item%20%3D%3E%20item.title%20)">Run this code</a></li>
</ul>

<p>If we look at the syntax of arrow functions, there is no <code>function</code> keyword. What remains is zero or more arguments, the “fat arrow” (<code>=&gt;</code>) and the function expression. The <code>return</code> statement is implicitly added.</p>

With zero or more than one argument, you must provide parentheses:

<pre><code class="language-javascript">// No arguments
books.map( () =&gt; 1 ); // [1, 1]

// Multiple arguments
[1,2].map( (n, index) =&gt; n * index ); // [0, 2]
</code></pre>

<p>Put the function expression in a block (<code>{ ... }</code>) if you need more logic or more white space:</p>

<pre><code class="language-javascript">let result = [1, 2, 3, 4, 5].map( n =&gt; {
   n = n % 3;
   return n;
});
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20result%20%3D%20%5B1%2C%202%2C%203%2C%204%2C%205%5D.map(%20n%20%3D%3E%20%7B%0A%20%20%20%20n%20%3D%20n%20%25%203%3B%0A%20%20%20%20return%20n%3B%0A%7D)">Run this code</a></li>
</ul>

<p>Not only do arrow functions mean fewer characters to type, but they also behave differently from regular functions. An arrow function expression inherits <code>this</code> and <code>arguments</code> from the surrounding context. This means you can get rid of ugly statements like <code>var that = this</code>, and you won’t need to bind functions to the correct context. Here’s an example (note <code>this.title</code> versus <code>that.title</code> in the ES5 version):</p>

<div class="break-out">

<pre><code class="language-javascript">let book = {
   title: 'X',
   sellers: ['A', 'B'],
   printSellers() {
      this.sellers.forEach(seller =&gt; console.log(seller + ' sells ' + this.title));
   }
}

// ES5 equivalent:
var book = {
   title: 'X',
   sellers: ['A', 'B'],
   printSellers: function() {
      var that = this;
      this.sellers.forEach(function(seller) {
         console.log(seller + ' sells ' + that.title)
      })
   }
}</code></pre></div>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20book%20%3D%20%7B%0A%20%20%20%20title%3A%20'X'%2C%0A%20%20%20%20sellers%3A%20%5B'A'%2C%20'B'%5D%2C%0A%20%20%20%20printSellers()">Run this code</a></li>
</ul>

## Strings

### Methods

<p>A couple of convenience methods have been added to the <code>String</code> prototype. Most of them basically eliminate some workarounds with the <code>indexOf()</code> method to achieve the same:</p>

<pre><code class="language-javascript">'my string'.startsWith('my'); //true
'my string'.endsWith('my'); // false
'my string'.includes('str'); // true
</code></pre>

Simple but effective. Another convenience method has been added to create a repeating string:

<pre><code class="language-javascript">'my '.repeat(3); // 'my my my '
</code></pre>

### Template Literal

Template literals provide a clean way to create strings and perform string interpolation. You might already be familiar with the syntax; it’s based on the dollar sign and curly braces <code>${..}</code>. Template literals are enclosed by backticks. Here’s a quick demonstration:

<div class="break-out">

<pre><code class="language-javascript">let name = 'John',
   apples = 5,
   pears = 7,
   bananas = function() { return 3; }

console.log(`This is ${name}.`);

console.log(`He carries ${apples} apples, ${pears} pears, and ${bananas()} bananas.`);

// ES5 equivalent:
console.log('He carries ' + apples + ' apples, ' + pears + ' pears, and ' + bananas() +' bananas.');
</code></pre></div>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20name%20%3D%20'John'%2C%0A%20%20%20%20apples%20%3D%205%2C%0A%20%20%20%20pears%20%3D%207%2C%0A%20%20%20%20bananas%20%3D%20function()">Run this code</a></li>
</ul>

In the form above, compared to ES5, they’re merely a convenience for string concatenation. However, template literals can also be used for multi-line strings. Keep in mind that white space is part of the string:

<pre><code class="language-javascript">let x = `1...
2...
3 lines long!`; // Yay

// ES5 equivalents:
var x = "1...\n" + 
"2...\n" +
"3 lines long!";

var x = "1...\n2...\n3 lines long!";
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20x%20%3D%20%601...%0A2...%0A3%20lines%20long!%60%3B">Run this code</a></li>
</ul>

## Arrays

The <code>Array</code> object now has some new static class methods, as well as new methods on the <code>Array</code> prototype.

First, <code>Array.from</code> creates <code>Array</code> instances from array-like and iterable objects. Examples of array-like objects include:

- the `arguments` within a function;
- a `nodeList` returned by `document.getElementsByTagName()`;
- the new `Map` and `Set` data structures.

<div class="break-out">

<pre><code class="language-javascript">let itemElements = document.querySelectorAll('.items');
let items = Array.from(itemElements);
items.forEach(function(element) {
    console.log(element.nodeType)
});

// A workaround often used in ES5:
let items = Array.prototype.slice.call(itemElements);</code></pre></div>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20itemElements%20%3D%20document.querySelectorAll('div')">Run this code</a></li>
</ul>

In the example above, you can see that the <code>items</code> array has the <code>forEach</code> method, which isn’t available in the <code>itemElements</code> collection.

An interesting feature of <code>Array.from</code> is the second optional <code>mapFunction</code> argument. This allows you to create a new mapped array in a single invocation:

<div class="break-out">

<pre><code class="language-javascript">let navElements = document.querySelectorAll('nav li');
let navTitles = Array.from(navElements, el =&gt; el.textContent);</code></pre></div>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20navElements%20%3D%20document.querySelectorAll('nav%20li')">Run this code</a></li>
</ul>

Then, we have <code>Array.of</code>, which behaves much like the <code>Array</code> constructor. It fixes the special case when passing it a single number argument. This results in <code>Array.of</code> being preferable to <code>new Array()</code>. However, in most cases, you’ll want to use array literals.

<div class="break-out">

<pre><code class="language-javascript">let x = new Array(3); // [undefined, undefined, undefined]
let y = Array.of(8); // [8]
let z = [1, 2, 3]; // Array literal</code></pre></div>

Last but not least, a couple of methods have been added to the <code>Array</code> prototype. I think the <code>find</code> methods will be very welcome to most JavaScript developers.

- `find` returns the first element for which the callback returns `true`.
- `findIndex` returns the index of the first element for which the callback returns `true`.
- `fill` “overwrites” the elements of an array with the given argument.

<pre><code class="language-javascript">[5, 1, 10, 8].find(n =&gt; n === 10) // 10

[5, 1, 10, 8].findIndex(n =&gt; n === 10) // 2

[0, 0, 0].fill(7) // [7, 7, 7]
[0, 0, 0, 0, 0].fill(7, 1, 3) // [0, 7, 7, 7, 0]</code></pre>

## Math

A couple of new methods have been added to the <code>Math</code> object.

- `Math.sign` returns the sign of a number as `1`, `-1` or `0`.
- `Math.trunc` returns the passed number without fractional digits.
- `Math.cbrt` returns the cube root of a number.

<pre><code class="language-javascript">Math.sign(5); // 1
Math.sign(-9); // -1

Math.trunc(5.9); // 5
Math.trunc(5.123); // 5

Math.cbrt(64); // 4
</code></pre>

If you want to learn more about the <a href="https://www.2ality.com/2015/04/numbers-math-es6.html">new number and math features in ES6</a>, Dr. Axel Rauschmayer has you covered.</p>

{{% ad-panel-leaderboard %}}

## Spread Operator

<p>The spread operator (<code>...</code>) is a very convenient syntax to expand elements of an array in specific places, such as arguments in function calls. Showing you some examples is probably the best way to demonstrate just how useful they are.</p>

<p>First, let’s see how to expand elements of an array within another array:</p>

<div class="break-out">

<pre><code class="language-javascript">let values = [1, 2, 4];
let some = [...values, 8]; // [1, 2, 4, 8]
let more = [...values, 8, ...values]; // [1, 2, 4, 8, 1, 2, 4]

// ES5 equivalent:
let values = [1, 2, 4];
// Iterate, push, sweat, repeat...
// Iterate, push, sweat, repeat...
</code></pre></div>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20values%20%3D%20%5B1%2C%202%2C%204%5D%3B%0Alet%20some%20%3D%20%5B...values%2C%208%5D%3B%0Alet%20more%20%3D%20%5B...values%2C%208%2C%20...values%5D%3B%0Aconsole.log(some)">Run this code</a></li>
</ul>

<p>The spread syntax is also powerful when calling functions with arguments:</p>

<pre><code class="language-javascript">let values = [1, 2, 4];

doSomething(...values);

function doSomething(x, y, z) {
   // x = 1, y = 2, z = 4
}

// ES5 equivalent:
doSomething.apply(null, values);
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20values%20%3D%20%5B1%2C%202%2C%204%5D%3B%0AdoSomething(...values)">Run this code</a></li>
</ul>

<p>As you can see, this saves us from the often-used <code>fn.apply()</code> workaround. The syntax is very flexible, because the spread operator can be used anywhere in the argument list. This means that the following invocation produces the same result:</p>

<pre><code class="language-javascript">let values = [2, 4];
doSomething(1, ...values);
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20values%20%3D%20%5B2%2C%204%5D%3B%0AdoSomething(1%2C%20...values)">Run this code</a></li>
</ul>

<p>We’ve been applying the spread operator to arrays and arguments. In fact, it can be applied to all iterable objects, such as a <code>NodeList</code>:</p>

<pre><code class="language-javascript">let form = document.querySelector('#my-form'),
   inputs = form.querySelectorAll('input'),
   selects = form.querySelectorAll('select');

let allTheThings = [form, ...inputs, ...selects];
</code></pre>

<ul>
  <li><a href="https://jsbin.com/vibaxerino/edit?html,js,console">Run this code</a></li>
</ul>

<p>Now, <code>allTheThings</code> is a flat array containing the <code>&lt;form&gt;</code> node and its <code>&lt;input&gt;</code> and <code>&lt;select&gt;</code> child nodes.</p>

{{% ad-panel-leaderboard %}}

## Destructuring

<p>Destructuring provides a convenient way to extract data from objects or arrays. For starters, a good example can be given using an array:</p>

<pre><code class="language-javascript">let [x, y] = [1, 2]; // x = 1, y = 2

// ES5 equivalent:
var arr = [1, 2];
var x = arr[0];
var y = arr[1];
</code></pre>

<p>With this syntax, multiple variables can be assigned a value in one go. A nice side effect is that you can easily swap variable values:</p>

<pre><code class="language-javascript">let x = 1,
   y = 2;

[x, y] = [y, x]; // x = 2, y = 1
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20x%20%3D%201%2C%0A%20%20%20%20y%20%3D%202%3B%0A%0A%5Bx%2C%20y%5D%20%3D%20%5By%2C%20x%5D%3B%0A">Run this code</a></li>
</ul>

<p>Destructuring also works with objects. Make sure to have matching keys:</p>

<pre><code class="language-javascript">let obj = {x: 1, y: 2};
let {x, y} = obj; // x = 1, y = 2
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20obj%20%3D%20%7Bx%3A%201%2C%20y%3A%202%7D%3B%0Alet%20%7Bx%2C%20y%7D%20%3D%20obj%3B">Run this code</a></li>
</ul>

<p>You could also use this mechanism to change variable names:</p>

<pre><code class="language-javascript">let obj = {x: 1, y: 2};
let {x: a, y: b} = obj; // a = 1, b = 2
</code></pre>

<p>Another interesting pattern is to simulate multiple return values:</p>

<pre><code class="language-javascript">function doSomething() {
   return [1, 2]
}

let [x, y] = doSomething(); // x = 1, y = 2
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=true&spec=false&code=function%20doSomething()">Run this code</a></li>
</ul>

<p>Destructuring can be used to assign default values to argument objects. With an object literal, you can actually simulate named parameters.</p>

<pre><code class="language-javascript">function doSomething({y = 1, z = 0}) {
   console.log(y, z);
}
doSomething({y: 2});
</code></pre>

## Parameters

### Default Values

<p>In ES6, defining default values for function parameters is possible. The syntax is as follows:</p>

<pre><code class="language-javascript">function doSomething(x, y = 2) {
   return x * y;
}

doSomething(5); // 10
doSomething(5, undefined); // 10
doSomething(5, 3); // 15
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=true&spec=false&code=function%20doSomething(x%2C%20y%20%3D%202)">Run this code</a></li>
</ul>

<p>Looks pretty clean, right? I’m sure you’ve needed to fill up some arguments in ES5 before:</p>

<pre><code class="language-javascript">function doSomething(x, y) {
   y = y === undefined ? 2 : y;
   return x * y;
}
</code></pre>

<p>Either <code>undefined</code> or no argument triggers the default value for that argument.</p>

### Rest Parameters

<p>We’ve been looking into the spread operator. Rest parameters are very similar. It also uses the <code>...</code> syntax and allows you to store trailing arguments in an array:</p>

<pre><code class="language-javascript">function doSomething(x, ...remaining) {
   return x * remaining.length;
}
</code></pre>

As you can see, this saves us from the often-used <code>fn.apply()</code> workaround. The syntax is very flexible, because the spread operator can be used anywhere in the argument list. This means that the following invocation produces the same result:

<pre<code class="language-javascript">let values = [2, 4];
doSomething(1, ...values);
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20values%20%3D%20%5B2%2C%204%5D%3B%0AdoSomething(1%2C%20...values)">Run this code</a></li>
</ul>

We’ve been applying the spread operator to arrays and arguments. In fact, it can be applied to all iterable objects, such as a <code>NodeList</code>:

<pre><code class="language-javascript">let form = document.querySelector('#my-form'),
   inputs = form.querySelectorAll('input'),
   selects = form.querySelectorAll('select');

let allTheThings = [form, ...inputs, ...selects];
</code></pre>

<ul>
  <li><a href="https://jsbin.com/vibaxerino/edit?html,js,console">Run this code</a></li>
</ul>

<p>Now, <code>allTheThings</code> is a flat array containing the <code>&lt;form&gt;</code> node and its <code>&lt;input&gt;</code> and <code>&lt;select&gt;</code> child nodes.</p>

## Destructuring

Destructuring provides a convenient way to extract data from objects or arrays. For starters, a good example can be given using an array:

<pre><code class="language-javascript">let [x, y] = [1, 2]; // x = 1, y = 2

// ES5 equivalent:
var arr = [1, 2];
var x = arr[0];
var y = arr[1];
</code></pre>

With this syntax, multiple variables can be assigned a value in one go. A nice side effect is that you can easily swap variable values:

<pre><code class="language-javascript">let x = 1,
   y = 2;

[x, y] = [y, x]; // x = 2, y = 1
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20x%20%3D%201%2C%0A%20%20%20%20y%20%3D%202%3B%0A%0A%5Bx%2C%20y%5D%20%3D%20%5By%2C%20x%5D%3B%0A">Run this code</a></li>
</ul>

Destructuring also works with objects. Make sure to have matching keys:

<pre><code class="language-javascript">let obj = {x: 1, y: 2};
let {x, y} = obj; // x = 1, y = 2
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=let%20obj%20%3D%20%7Bx%3A%201%2C%20y%3A%202%7D%3B%0Alet%20%7Bx%2C%20y%7D%20%3D%20obj%3B">Run this code</a></li>
</ul>

You could also use this mechanism to change variable names:

<pre><code class="language-javascript">let obj = {x: 1, y: 2};
let {x: a, y: b} = obj; // a = 1, b = 2
</code></pre>

Another interesting pattern is to simulate multiple return values:

<pre><code class="language-javascript">function doSomething() {
   return [1, 2]
}

let [x, y] = doSomething(); // x = 1, y = 2
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=true&spec=false&code=function%20doSomething()">Run this code</a></li>
</ul>

Destructuring can be used to assign default values to argument objects. With an object literal, you can actually simulate named parameters.

<pre><code class="language-javascript">function doSomething({y = 1, z = 0}) {
   console.log(y, z);
}
doSomething({y: 2});
</code></pre>

## Parameters

### Default Values

<p>In ES6, defining default values for function parameters is possible. The syntax is as follows:</p>

<pre><code class="language-javascript">function doSomething(x, y = 2) {
   return x * y;
}

doSomething(5); // 10
doSomething(5, undefined); // 10
doSomething(5, 3); // 15
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=true&spec=false&code=function%20doSomething(x%2C%20y%20%3D%202)">Run this code</a></li>
</ul>

<p>Looks pretty clean, right? I’m sure you’ve needed to fill up some arguments in ES5 before:</p>

<pre><code class="language-javascript">function doSomething(x, y) {
   y = y === undefined ? 2 : y;
   return x * y;
}
</code></pre>

<p>Either <code>undefined</code> or no argument triggers the default value for that argument.</p>

### Rest Parameters

<p>We’ve been looking into the spread operator. Rest parameters are very similar. It also uses the <code>...</code> syntax and allows you to store trailing arguments in an array:</p>

<pre><code class="language-javascript">function doSomething(x, ...remaining) {
   return x * remaining.length;
}

doSomething(5, 0, 0, 0); // 15
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=function%20doSomething(x%2C%20...remaining">Run this code</a></li>
</ul>

## Modules

Modules are certainly a welcome addition to the JavaScript language. I think this major feature alone is worth digging into ES6.

Any serious JavaScript project today uses some sort of module system — maybe something like the “revealing module pattern” or the more extensive formats AMD or CommonJS. However, browsers don’t feature any kind of module system. You always need a build step or a loader for your AMD or CommonJS modules. Tools to handle this include RequireJS, Browserify and Webpack.

The ES6 specification includes both a new syntax and a loader mechanism for modules. If you want to use modules and write for the future, this is the syntax you should use. Modern build tools support this format, perhaps via a plugin, so you should be good to go. (No worries — we’ll discuss this further in the “Transpilation” section later on.)

Now, on to the ES6 module syntax. Modules are designed around the <code>export</code> and <code>import</code> keywords. Let’s examine an example with two modules right away:

<pre><code class="language-javascript">// lib/math.js

export function sum(x, y) {
   return x + y;
}
export var pi = 3.141593;
</code></pre>

<pre><code class="language-javascript">// app.js

import { sum, pi } from "lib/math";
console.log('2π = ' + sum(pi, pi));
</code></pre>

<p>As you can see, there can be multiple <code>export</code> statements. Each must explicitly state the type of the exported value (<code>function</code> and <code>var</code>, in this example).</p>

<p>The <code>import</code> statement in this example uses a syntax (similar to destructuring) to explicitly define what is being imported. To import the module as a whole, the <code>*</code> wildcard can be used, combined with the <code>as</code> keyword to give the module a local name:</p>

<pre><code class="language-javascript">// app.js

import * as math from "lib/math";
console.log('2π = ' + math.sum(math.pi, math.pi));
</code></pre>

<p>The module system features a <code>default</code> export. This can also be a function. To import this default value in a module, you’ll just need to provide the local name (i.e. no destructuring):</p>

<pre><code class="language-javascript">// lib/my-fn.js

export default function() {
   console.log('echo echo');
}

// app.js

import doSomething from 'lib/my-fn';
doSomething();
</code></pre>

<p>Please note that the <code>import</code> statements are synchronous, but the module code doesn’t execute until all dependencies have loaded.</p>

## Classes

<p>Classes are a well-debated feature of ES6. Some believe that they go against the prototypal nature of JavaScript, while others think they lower the barrier to entry for beginners and people coming from other languages and that they help people writing large-scale applications. In any case, they are part of ES6. Here’s a very quick introduction.</p>

<p>Classes are built around the <code>class</code> and <code>constructor</code> keywords. Here’s a short example:</p>

<pre><code class="language-javascript">class Vehicle {
   constructor(name) {
      this.name = name;
      this.kind = 'vehicle';
   }
   getName() {
      return this.name;
   }   
}

// Create an instance
let myVehicle = new Vehicle('rocky');
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=true&spec=false&code=class%20Vehicle%20%7B%0A%20%20%20%20constructor(name)">Run this code</a></li>
</ul>

<p>Note that the class definition is not a regular object; hence, there are no commas between class members.</p>

<p>To create an instance of a class, you must use the <code>new</code> keyword. To inherit from a base class, use <code>extends</code>:</p>

<pre><code class="language-javascript">class Car extends Vehicle {
   constructor(name) {
      super(name);
      this.kind = 'car'
   }
}

let myCar = new Car('bumpy');

myCar.getName(); // 'bumpy'
myCar instanceof Car; // true
myCar instanceof Vehicle; //true
</code></pre>

<ul>
  <li><a href="https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=true&spec=false&code=class%20Vehicle%20%7B%0A%20%20%20%20constructor(name)">Run this code</a></li>
</ul>

<p>From the derived class, you can use <code>super</code> from any constructor or method to access its base class:</p>

- To call the parent constructor, use `super()`.
- To call another member, use, for example, `super.getName()`.

<p>There’s more to using classes. If you want to dig deeper into the subject, I recommend “<a href="https://www.2ality.com/2015/02/es6-classes-final.html">Classes in ECMAScript 6</a>” by Dr. Axel Rauschmayer.</p>

## Symbols

<p>Symbols are a new primitive data type, like <code>Number</code> and <code>String</code>. You can use symbols to create unique identifiers for object properties or to create unique constants.</p>

<pre><code class="language-javascript">const MY_CONSTANT = Symbol();

let obj = {};
obj[MY_CONSTANT] = 1;
</code></pre>

<p>Note that key-value pairs set with symbols are not returned by <code>Object.getOwnPropertyNames()</code>, and they are not visible in <code>for...in</code> iterations, <code>Object.keys()</code> or <code>JSON.stringify()</code>. This is in contrast to regular string-based keys. You can get an array of symbols for an object with <code>Object.getOwnPropertySymbols()</code>.</p>

<p>Symbols work naturally with <code>const</code> because of their immutable character:</p>

<pre><code class="language-javascript">const CHINESE = Symbol();
const ENGLISH = Symbol();
const SPANISH = Symbol();

switch(language) {
   case CHINESE:
      // 
      break;
   case ENGLISH:
      // 
      break;
   case SPANISH:
      // 
      break;
   default:
      // 
      break;
}
</code></pre>

You can give a symbol a description. You can’t use it to access the symbol itself, but it’s useful for debugging.

<pre><code class="language-javascript">const CONST_1 = Symbol('my symbol');
const CONST_2 = Symbol('my symbol');

typeof CONST_1 === 'symbol'; // true

CONST_1 === CONST_2; // false
</code></pre>

<p>Want to learn more about symbols? Mozilla Developer Network has a good page about the new <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol">symbol primitive</a>.</p>

## Transpilation

<p>We can write our code in ES6 today. As mentioned in the introduction, browser support for ES6 features is not extensive yet and varies a lot. It’s very likely that not all of the ES6 code you write will be understood by the browsers of your users. This is why we need to convert it to the previous version of JavaScript (ES5), which runs fine in any modern browser. This conversion is often referred to as “transpilation.” We’ll need to do this with our applications until the browsers we want to support understand ES6.</p>

### Getting Started

<p>Transpiling code is not hard. You can transpile code directly from the command line, or you can include it as a plugin for a task runner, such as Grunt or Gulp. Plenty of transpilation solutions are out there, including Babel, Traceur and TypeScript. See, for instance, the <a href="https://babeljs.io/docs/setup/">many ways to start using ES6</a> with Babel (formerly “6to5”). Most features of ES6 are at your disposal!</p>

<p>Now that you’re hopefully enthusiastic about using ES6, why not start using it? Depending on the features you want to use and the browsers or environments you need to support (such as Node.js), you’ll probably want to incorporate a transpiler in your workflow. And if you’re up for it, there are also file watchers and live browser reloaders to make your coding experience seamless.</p>

<p>If you’re starting from scratch, you might just want to transpile your code from the command line (see, for example, the <a href="https://babeljs.io/docs/usage/cli/">Babel CLI documentation</a>). If you are already using a task runner, such as Grunt or Gulp, you can add a plugin such as <a href="https://www.npmjs.com/package/gulp-babel">gulp-babel</a> or the <a href="https://github.com/babel/babel-loader">babel-loader</a> for Webpack. For Grunt, there is <a href="https://github.com/babel/grunt-babel">grunt-babel</a> and many other <a href="https://gruntjs.com/plugins?q=es6">ES6-related plugins</a>. Folks using Browserify might want to check out <a href="https://github.com/babel/babelify">babelify</a>.</p>

<p>Many features can be converted to ES5-compatible code without significant overhead. Others do require extra stopgaps (which can be provided by the transpiler) and/or come with a performance penalty. Some are simply impossible. To play around with ES6 code and see what the transpiled code looks like, you can use various interactive environments (also known as REPLs):</p>

- Traceur: [website](https://github.com/google/traceur-compiler), [REPL](https://google.github.io/traceur-compiler/demo/repl.html)
- Babel: [website](https://babeljs.io/), [REPL](https://babeljs.io/repl/)
- TypeScript: [website](https://www.typescriptlang.org/), [REPL](https://www.typescriptlang.org/Playground)
- [ScratchJS](https://github.com/richgilbank/Scratch-JS) (Chrome extension)

<p>Note that TypeScript is not exactly a transpiler. It’s a typed superset of JavaScript that compiles to JavaScript. Among other features, it supports many ES6 features, much like the other transpilers.</p>

### So, What Exactly Can I Use?

<p>In general, some of the features of ES6 can be used almost for “free,” such as modules, arrow functions, rest parameters and classes. These features can be transpiled to ES5 without much overhead. Additions to <code>Array</code>, <code>String</code> and <code>Math</code> objects and prototypes (such as <code>Array.from()</code> and <code>"it".startsWith("you")</code>) require so-called “polyfills.” Polyfills are stopgaps for functionality that a browser doesn’t natively support yet. You can load a polyfill first, and your code will run as if the browser has that functionality. Both Babel and Traceur do provide such polyfills.</p>

<p>See Kangax’s <a href="https://kangax.github.io/compat-table/es6/">ES6 compatibility table</a> for a full overview of ES6 features that are supported by both transpilers and browsers. It is motivating to see that, at the time of writing, the latest browsers already support 55% to over 70% of all ES6 features. Microsoft Edge, Google Chrome and Mozilla’s Firefox are really competing with each other here, which is great for the web at large.</p>

<p>Personally, I’m finding that being able to easily use new ES6 features such as modules, arrow functions and rest parameters is a relief and a significant improvement to my own coding. Now that I’m comfortable with writing in ES6 and transpiling my code to ES5, more ES6 goodness will follow naturally over time.</p>

## What’s Next?

<p>Once you’ve installed a transpiler, you might want to start using “small” features, such as <code>let</code> and arrow functions. Keep in mind that code that is already written as ES5 will be left untouched by the transpiler. As you enhance your scripts with ES6 and enjoy using it, you can gradually sprinkle more and more ES6 features onto your code. Perhaps convert some of the code to the new modules or class syntax. I promise it’ll be good!</p>

<p>There is much more to ES6 than we were able to cover in this article. Uncovered features include <code>Map</code>, <code>Set</code>, tagged template strings, generators, <code>Proxy</code> and <code>Promise</code>. Let me know if you want these features to be covered in a follow-up article. In any case, a book that covers all of ES6 is <a href="https://exploringjs.com/"><em>Exploring ES6</em></a> by Dr. Axel Rauschmayer, which I can happily recommend for a deep dive.</p>

## Closing Thought

<p>By using a transpiler, all of your code is effectively “locked” to ES5, while browsers keep adding new features. So, even if a browser fully supports a particular ES6 feature, the ES5-compatible version will be used, <a href="https://kpdecker.github.io/six-speed/">possibly performing worse</a>. You can count on the fact that any ES6 feature, and eventually all of them, will be supported at some point (in the browsers and environments you need to support at that time). Until then, we need to manage this and selectively disable ES6 features from getting transpiled to ES5 and prevent unnecessary overhead. With this in mind, decide for yourself whether it is time to start using (parts of) ES6. <a href="https://babeljs.io/users/">Some companies think it is</a>.</p>

### <span class="rh">Further Reading</span> on SmashingMag:

- [Writing Next Generation Reusable JavaScript Modules in ECMAScript 6](https://www.smashingmagazine.com/2016/02/writing-next-generation-reusable-javascript-modules/)
- [How To Use Arguments And Parameters In ECMAScript 6](https://www.smashingmagazine.com/2016/07/how-to-use-arguments-and-parameters-in-ecmascript-6/)
- [Making A Complete Polyfill For The HTML5 Details Element](https://www.smashingmagazine.com/2014/11/complete-polyfill-html5-details-element/)
- [Generating SVG With React](https://www.smashingmagazine.com/2015/12/generating-svg-with-react/)

{{< signature "al, ml, il" >}}

---
title: 'How To Use ES6 Arguments And Parameters'
slug: how-to-use-arguments-and-parameters-in-ecmascript-6
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8e864da2-661f-4669-ae74-be76edf773a6/js-brackets-image-opt.jpg
date: 2016-07-20T18:03:40.000Z
author: farazkelhini
summary: >-
  Developers are using ECMAScript 6 features more and more, and soon these features will be unavoidable. In this tutorial, you’ll learn how ECMAScript 6 has upgraded parameter handling in JavaScript, and more.
description: >-
  Developers are using ECMAScript 6 features more and more, and soon these features will be unavoidable. In this tutorial, you’ll learn how ECMAScript 6 has upgraded parameter handling in JavaScript, and more.
categories:
  - Coding
  - Tools
  - JavaScript
---
ECMAScript 6 (or ECMAScript 2015) is the newest version of the ECMAScript standard and has remarkably improved parameter handling in JavaScript. We can now use rest parameters, default values and destructuring, among other new features.

In this tutorial, we will explore arguments and parameters in detail and see how ECMAScript 6 has upgraded them.

## Arguments Versus Parameters

Arguments and parameters are often referred to interchangeably. Nevertheless, for the purpose of this tutorial, we will make a distinction. In most standards, parameters (or formal parameters) are what’s given in the function declaration, and arguments (or actual parameters) are what’s passed to the function. Consider this function:

<pre><code class="language-javascript">function foo(param1, param2) {
    // do something
}
foo(10, 20);
</code></pre>

<p>In this function, <code>param1</code> and <code>param2</code> are function parameters, and the values passed to the function (<code>10</code> and <code>20</code>) are arguments.</p>

## Spread Operator (...)

<p>In ECMAScript 5, the <code>apply()</code> method is a convenient tool for passing an array as arguments to a function. For example, it’s commonly used with the <code>Math.max()</code> method to find the highest value in an array. Consider this code fragment:</p>

<pre><code class="language-javascript">var myArray = [5, 10, 50];
Math.max(myArray);    // Error: NaN
Math.max.apply(Math, myArray);    // 50
</code></pre>

<p>The <code>Math.max()</code> method doesn’t support arrays; it accepts only numbers. When an array is passed to the <code>Math.max()</code> function, it throws an error. But when the <code>apply()</code> method is used, the array is sent as individual numbers, so the <code>Math.max()</code> method can handle it.</p>

{{% feature-panel %}}

<p>Fortunately, with the introduction of the spread operator in ECMAScript 6, we no longer need to use the <code>apply()</code> method. With the spread operator, we can easily expand an expression into multiple arguments:</p>

<pre><code class="language-javascript">var myArray = [5, 10, 50];
Math.max(...myArray);    // 50
</code></pre>

<p>Here, the spread operator expands <code>myArray</code> to create individual values for the function. While simulating the spread operator using <code>apply()</code> in ECMAScript 5 is possible, the syntax is confusing and lacks the flexibility of the spread operator. The spread operator not only is easier to use, but packs more features. For example, it can be used multiple times and can be mixed with other arguments in a <code>function</code> call:</p>

<div class="break-out">

<pre><code class="language-javascript">function myFunction() {
  for(var i in arguments){
    console.log(arguments[i]);
  }
}
var params = [10, 15];
myFunction(5, ...params, 20, ...[25]);    // 5 10 15 20 25
</code></pre></div>

Another advantage of the spread operator is that it can easily be used with constructors:

<div class="break-out">

<pre><code class="language-javascript">new Date(...[2016, 5, 6]);    // Mon Jun 06 2016 00:00:00 GMT-0700 (Pacific Daylight Time)
</code></pre></div>

Of course, we could rewrite the preceding code in ECMAScript 5, but we would need to use a complicated pattern to avoid getting a type error:

<div class="break-out">

<pre><code class="language-javascript">new Date.apply(null, [2016, 4, 24]);    // TypeError: Date.apply is not a constructor
new (Function.prototype.bind.apply(Date, [null].concat([2016, 5, 6])));   // Mon Jun 06 2016 00:00:00 GMT-0700 (Pacific Daylight Time)
</code></pre></div>

### Spread Operator Browser Support In Function Calls

Desktop browsers:
<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap="">
<thead>
<tr>
<th data-tablesaw-priority="persist">Chrome</th>
<th>Firefox</th>
<th>Internet Explorer</th>
<th>Microsoft Edge</th>
<th>Opera</th>
<th>Safari</th>
</tr>
</thead>
<tbody>
<tr>
<td>46</td>
<td>27</td>
<td>–</td>
<td>Supported</td>
<td>–</td>
<td>7.1</td>
</tr>
</tbody>
</table>

Mobile browsers:
<table class="tablesaw" data-tablesaw-mode="swipe" data-tablesaw-minimap="">
<thead>
<tr>
<th data-tablesaw-priority="persist">Chrome for Android</th>
<th>Firefox Mobile</th>
<th>Safari Mobile</th>
<th>Opera Mobile</th>
<th>IE Mobile</th>
</tr>
</thead>
<tbody>
<tr>
<td>46</td>
<td>27</td>
<td>8</td>
<td>–</td>
<td>–</td>
</tr>
</tbody>
</table>

{{% ad-panel-leaderboard %}}

## Rest Parameters

The rest parameter has the same syntax as the spread operator, but instead of expanding an array into parameters, it collects parameters and turns them into an array.

<pre><code class="language-javascript">function myFunction(...options) {
     return options;
}
myFunction('a', 'b', 'c');      // ["a", "b", "c"]
</code></pre>

If there are no arguments, the rest parameter will be set to an empty array:

<pre><code class="language-javascript">function myFunction(...options) {
     return options;
}
myFunction();      // []
</code></pre>

<p>A rest parameter is particularly useful when creating a variadic function (a function that accepts a variable number of arguments). Having the benefit of being arrays, rest parameters can readily replace the <code>arguments</code> object (which we’ll explain later in this tutorial). Consider this function, written in ECMAScript 5:</p>

<div class="break-out">

<pre><code class="language-javascript">function checkSubstrings(string) {
  for (var i = 1; i &lt; arguments.length; i++) {
    if (string.indexOf(arguments[i]) === -1) {
      return false;
    }
  }
  return true;
}
checkSubstrings('this is a string', 'is', 'this');   // true
</code></pre></div>

<p>This function checks whether a string contains a number of substrings. The first problem with this function is that we have to look inside the <code>function</code>’s body to see that it takes multiple arguments. The second problem is that the iteration must start from <code>1</code> instead of <code>0</code>, because <code>arguments[0]</code> points to the first argument. If we later decide to add another parameter before or after the string, we might forget to update the loop. With the rest parameters, we easily avoid these problems:</p>

<div class="break-out">

<pre><code class="language-javascript">function checkSubstrings(string, ...keys) {
  for (var key of keys) {
    if (string.indexOf(key) === -1) {
      return false;
    }
  }
  return true;
}
checkSubstrings('this is a string', 'is', 'this');   // true
</code></pre></div>

<p>The output of this function is the same as the previous one. Here again, the parameter <code>string</code> is filled with the argument that is passed first, but the rest of the arguments are put in an array and assigned to the variable <code>keys</code>.</p>

<p>Using the rest parameter instead of the <code>arguments</code> object improves the readability of the code and avoids <a href="https://github.com/petkaantonov/bluebird/wiki/Optimization-killers#3-managing-arguments">optimization issues</a> in JavaScript. Nevertheless, the rest parameter is not without its limitations. For example, it must be the last argument; otherwise, a syntax error will occur:</p>

<div class="break-out">

<pre><code class="language-javascript">function logArguments(a, ...params, b) {
        console.log(a, params, b);
}
logArguments(5, 10, 15);    // SyntaxError: parameter after rest parameter
</code></pre></div>

<p>Another limitation is that only one rest parameter is allowed in the <code>function</code> declaration:</p>

<div class="break-out">

<pre><code class="language-javascript">function logArguments(...param1, ...param2) {
}
logArguments(5, 10, 15);    // SyntaxError: parameter after rest parameter
</code></pre></div>

### Rest Parameters Browser Support

<p>Desktop browsers:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Chrome</th>
      <th>Firefox</th>
      <th>Internet Explorer</th>
      <th>Microsoft Edge</th>
      <th>Opera</th>
      <th>Safari</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>47</td>
      <td>15</td>
      <td>–</td>
      <td>Supported</td>
      <td>34</td>
      <td>–</td>
    </tr>
  </tbody>
</table>

<p>Mobile browsers:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Chrome for Android</th>
      <th>Firefox Mobile</th>
      <th>Safari Mobile</th>
      <th>Opera Mobile</th>
      <th>IE Mobile</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>47</td>
      <td>15</td>
      <td>–</td>
      <td>–</td>
      <td>–</td>
    </tr>
  </tbody>
</table>

## Default Parameters

### Default Parameters In ECMAScript 5

<p>JavaScript does not support default parameters in ECMAScript 5, but there is an easy workaround. Using a logical <code>OR</code> operator (<code>&#124;&#124;</code>) inside the function, we can easily simulate default parameters in ECMAScript 5. Consider this function:</p>

<pre><code class="language-javascript">function foo(param1, param2) {
   param1 = param1 || 10;
   param2 = param2 || 10;
   console.log(param1, param2);
}
foo(5, 5);  // 5 5
foo(5);    // 5 10
foo();    // 10 10
</code></pre>

<p>This function expects two arguments, but when it is called without arguments, it will use the default values. Inside the function, missing arguments are automatically set to undefined; so, we can detect these arguments and declare default values for them. To detect missing arguments and set default values, we use the logical <code>OR</code> operator (<code>&#124;&#124;</code>). This operator examines its first argument: If it’s <a href="https://developer.mozilla.org/en-US/docs/Glossary/Truthy">truthy</a>, the operator returns it; if it’s not, the operator returns its second argument.</p>

<p>This approach is commonly used in functions, but it has a flaw. Passing <code>0</code> or <code>null</code> will trigger a default value, too, because these are considered falsy values. So, if we actually need to pass <code>0</code> or <code>null</code> to this function, we would need an alternate way to check whether an argument is missing:</p>

<pre><code class="language-javascript">function foo(param1, param2) {
  if(param1 === undefined){
    param1 = 10;
  }
  if(param2 === undefined){
    param2 = 10;
  }
  console.log(param1, param2);
}
foo(0, null);    // 0, null
foo();    // 10, 10
</code></pre>

<p>Inside this function, the types of passed arguments are checked to make sure they are undefined before default values are assigned. This approach requires just a bit more code, but it is a safer alternative and allows us to pass <code>0</code> and <code>null</code> to the function.</p>

{{% ad-panel-leaderboard %}}

### Default Parameters In ECMAScript 6

<p>With ECMAScript 6, we no longer need to check for undefined values to simulate default parameters. We can now put default values right in the <code>function</code> declaration:</p>

<pre><code class="language-javascript">function foo(a = 10, b = 10) {
  console.log(a, b);
}
foo(5);    // 5 10
foo(0, null);    // 0 null
</code></pre>

<p>As you can see, omitting an argument triggers the default value, but passing <code>0</code> or <code>null</code> won’t. We can even use functions to retrieve values for default parameters:</p>

<pre><code class="language-javascript">function getParam() {
    alert("getParam was called");
    return 3;
}
function multiply(param1, param2 = getParam()) {
    return param1 * param2;
}
multiply(2, 5);     // 10
multiply(2);     // 6 (also displays an alert dialog)
</code></pre>

<p>Note that the <code>getParam</code> function is called only if the second argument is omitted. So, when we call the <code>multiply()</code> function with two parameters, the alert won’t be displayed.</p>

<p>Another interesting feature of default parameters is that we are able to refer to other parameters and variables in the <code>function</code> declaration:</p>

<pre><code class="language-javascript">function myFunction(a=10, b=a) {
     console.log('a = ' + a + '; b = '  + b);
}
myFunction();     // a=10; b=10
myFunction(22);    // a=22; b=22
myFunction(2, 4);    // a=2; b=4
</code></pre>

<p>You can even perform operations in the <code>function</code> declaration:</p>

<pre><code class="language-javascript">function myFunction(a, b = ++a, c = a*b) {
     console.log(c);
}
myFunction(5);    // 36
</code></pre>

Note that, unlike some other languages, JavaScript evaluates default parameters at call time:

<pre><code class="language-javascript">function add(value, array = []) {
  array.push(value);
  return array;
}
add(5);    // [5]
add(6);    // [6], not [5, 6]
</code></pre>

### Default Parameter Browser Support

<p>Desktop browsers:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Feature</th>
      <th>Chrome</th>
      <th>Firefox</th>
      <th>Internet Explorer</th>
      <th>Microsoft Edge</th>
      <th>Opera</th>
      <th>Safari</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Basic support</td>
      <td>49</td>
      <td>15</td>
      <td>–</td>
      <td>14</td>
      <td>–</td>
      <td>–</td>
    </tr>
    <tr>
      <td>Parameters without defaults after default parameter</td>
      <td>49</td>
      <td>26</td>
      <td>–</td>
      <td>14</td>
      <td>–</td>
      <td>–</td>
    </tr>
  </tbody>
</table>

<p>Mobile browsers:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Feature</th>
      <th>Chrome for Android</th>
      <th>Firefox Mobile</th>
      <th>Safari Mobile</th>
      <th>Opera Mobile</th>
      <th>IE Mobile</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Basic support</td>
      <td>49</td>
      <td>15</td>
      <td>–</td>
      <td>–</td>
      <td>–</td>
    </tr>
    <tr>
      <td>Parameters without defaults after default parameter</td>
      <td>46</td>
      <td>26</td>
      <td>–</td>
      <td>–</td>
      <td>–</td>
    </tr>
  </tbody>
</table>

## Destructuring

Destructuring is a new feature in ECMAScript 6 that enables us to extract values from arrays and object and to assign them to variables using a syntax that is similar to object and array literals. The syntax is clear and easy to understand and is particularly useful when passing arguments to a function.

In ECMAScript 5, a configuration object is often used to handle a large number of optional parameters, especially when the order of properties does not matter. Consider this function:

<pre><code class="language-javascript">function initiateTransfer(options) {
    var  protocol = options.protocol,
        port = options.port,
        delay = options.delay,
        retries = options.retries,
        timeout = options.timeout,
        log = options.log;
    // code to initiate transfer
}
options = {
  protocol: 'http',
  port: 800,
  delay: 150,
  retries: 10,
  timeout: 500,
  log: true
};
initiateTransfer(options);
</code></pre>

<p>This pattern is commonly used by JavaScript developers, and it works well, but we have to look inside the <code>function</code> body to see what parameters it expects. With destructured parameters, we can clearly indicate the parameters in the <code>function</code> declaration:</p>

<pre><code class="language-javascript">function initiateTransfer({protocol, port, delay, retries, timeout, log}) {
     // code to initiate transfer
};
var options = {
  protocol: 'http',
  port: 800,
  delay: 150,
  retries: 10,
  timeout: 500,
  log: true
}
initiateTransfer(options);
</code></pre>

In this function, we’ve used an object destructuring pattern, instead of a configuration object. This makes our function not only more concise, but easier to read.

We can also combine destructured parameters with regular ones:

<pre class="breakout"><code class="language-javascript">function initiateTransfer(param1, {protocol, port, delay, retries, timeout, log}) {
     // code to initiate transfer
}
initiateTransfer('some value', options);
</code></pre>

<p>Note that a type error will be thrown if parameters are omitted in the <code>function</code> call:</p>

<pre class="breakout"><code class="language-javascript">function initiateTransfer({protocol, port, delay, retries, timeout, log}) {
     // code to initiate transfer
}
initiateTransfer();  // TypeError: Cannot match against 'undefined' or 'null'
</code></pre>

This is the desired behavior when we need parameters to be required, but what if we want them to be optional? To prevent this error when parameters are missing, we need to assign a default value to destructured parameters:

<pre class="breakout"><code class="language-javascript">function initiateTransfer({protocol, port, delay, retries, timeout, log} = {}) {
     // code to initiate transfer
}
initiateTransfer();    // no error
</code></pre>

In this function, an empty object is provided as the default value for the destructured parameters. Now, if this function is called without any parameters, no error will occur.

We can also assign a default value to each destructured parameter:

<pre><code class="language-javascript">function initiateTransfer({
    protocol = 'http',
    port = 800,
    delay = 150,
    retries = 10,
    timeout = 500,
    log = true
}) {
     // code to initiate transfer
}
</code></pre>

<p>In this example, every property has a default parameter, eliminating the need for us to manually check for undefined parameters and assign default values inside the <code>function</code> body.</p>

### Destructuring Browser Support

<p>Desktop browsers:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Feature</th>
      <th>Chrome</th>
      <th>Firefox</th>
      <th>Internet Explorer</th>
      <th>Microsoft Edge</th>
      <th>Opera</th>
      <th>Safari</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Basic support</td>
      <td>49</td>
      <td>2.0</td>
      <td>–</td>
      <td>14</td>
      <td>–</td>
      <td>7.1</td>
    </tr>
    <tr>
      <td>Destructured parameter with default value assignment</td>
      <td>49</td>
      <td>47</td>
      <td>–</td>
      <td>14</td>
      <td>–</td>
      <td>–</td>
    </tr>
  </tbody>
</table>

<p>Mobile browsers:</p>

<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
  <thead>
    <tr>
      <th data-tablesaw-priority="persist">Feature</th>
      <th>Chrome for Android</th>
      <th>Firefox Mobile</th>
      <th>Safari Mobile</th>
      <th>Opera Mobile</th>
      <th>IE Mobile</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Basic support</td>
      <td>49</td>
      <td>1</td>
      <td>8</td>
      <td>–</td>
      <td>–</td>
    </tr>
    <tr>
      <td>Parameters without defaults after default parameter</td>
      <td>49</td>
      <td>47</td>
      <td>–</td>
      <td>–</td>
      <td>–</td>
    </tr>
  </tbody>
</table>

## Passing Arguments

There are two ways to pass arguments to a function: by reference or by value. Modifying an argument that’s passed by reference is reflected globally, but modifying an argument that’s passed by value is reflected only inside the function.

In some languages, such as Visual Basic and PowerShell, we have the option to specify whether to pass an argument by reference or by value, but that’s not the case with JavaScript.

### Passing Arguments By Value

<p>Technically, JavaScript can only pass by value. When we pass an argument to a function by value, a copy of that value is created within the <code>function</code> scope. Thus, any changes to the value are reflected only inside the <code>function</code>. Consider this example:</p>

<pre><code class="language-javascript">var a = 5;
function increment(a) {
    a = ++a;
    console.log(a);
}
increment(a);   // 6
console.log(a);    // 5
</code></pre>

<p>Here, modifying the argument inside the function has no effect on the original value. So, when the variable is logged from outside the function, the printed value is still <code>5</code>.</p>

### Passing Arguments By Reference

In JavaScript, everything is passed by value, but when we pass a variable that refers to an object (including arrays), the “value” is a reference to the object, and changing a property of an object referenced by a variable does change the underlying object.

Consider this function:

<pre><code class="language-javascript">function foo(param){
    param.bar = 'new value';
}
obj = {
    bar : 'value'
}
console.log(obj.bar);   // value
foo(obj);
console.log(obj.bar);   // new value
</code></pre>

As you can see, the property of the object is modified inside the function, but the modified value is visible outside of the function.

When we pass a non-primitive value such as an array or object, behind the scene a variable is created that points to the location of the original object in memory. This variable is then passed to the function, and modifying it will affect the original object.

## Type Checking And Missing Or Extra Parameters

<p>In a strongly typed language, we have to specify the type of parameters in the <code>function</code> declaration, but JavaScript lacks this feature. In JavaScript, it doesn’t matter what type of data or how many arguments we pass to a function.</p>

Suppose we have a function that accepts only one argument. When we call that function, we are not limited to pass just one argument to the function; we are free to pass one, two or more arguments! We may even choose to pass nothing at all, and no errors will occur.

The number of arguments and parameters can differ in two ways:

- **Fewer arguments than parameters**.  
The missing parameters will equal `undefined`.
- **More arguments than parameters**.  
The extra parameters will be ignored but can be retrieved via the special array-like variable arguments (discussed next).

## Mandatory Arguments

<p>If an argument is missing in a <code>function</code> call, it will be set to <code>undefined</code>. We can take advantage of this behavior and throw an error if an argument is omitted:</p>

<pre><code class="language-javascript">function foo(mandatory, optional) {
    if (mandatory === undefined) {
        throw new Error('Missing parameter: mandatory');
    }
}
</code></pre>

In ECMAScript 6, we can take this further and use default parameters to set mandatory arguments:

<pre class="breakout"><code class="language-javascript">function throwError() {
    throw new Error('Missing parameter');
}
function foo(param1 = throwError(), param2 = throwError()) {
    // do something
}
foo(10, 20);    // ok
foo(10);   // Error: missing parameter
</code></pre>

## Arguments Object

<p>The support for rest parameters was added to ECMAScript 4 with the intention of replacing the <code>arguments</code> object, but ECMAScript 4 never came to fruition. With the release of ECMAScript 6, JavaScript now officially supports the rest parameters. It also nixed the plan to drop support for the <code>arguments</code> object.</p>

<p>The <code>arguments</code> object is an array-like object that is available within all functions. It allows the <code>argument</code>’s values passed to the function to be retrieved by number, rather than by name. The object allows us to pass any number of arguments to a function. Consider the following code fragment:</p>

<pre><code class="language-javascript">function checkParams(param1) {
    console.log(param1);    // 2
    console.log(arguments[0], arguments[1]);    // 2 3
    console.log(param1 + arguments[0]);    // 2 + 2
}
checkParams(2, 3);
</code></pre>

<p>This function expects to receive only one argument. When we call it with two arguments, the first argument is accessible in the function by the parameter name <code>param1</code> or the arguments object <code>arguments[0]</code>, but the second argument is accessible only as <code>arguments[1]</code>. Also, note that the <code>arguments</code> object can be used in conjunction with named arguments.</p>

<p>The <code>arguments</code> object contains an entry for each argument passed to the function, and the index of the first entry starts at <code>0</code>. If we wanted to access more arguments in the example above, we would write <code>arguments[2]</code>, <code>arguments[3]</code> and so on.</p>

<p>We could even skip setting named parameters altogether and just use the <code>arguments</code> object:</p>

<pre><code class="language-javascript">function checkParams() {
    console.log(arguments[1], arguments[0], arguments[2]);
}
checkParams(2, 4, 6);  // 4 2 6
</code></pre>

In fact, named parameters are a convenience, not a necessity. Similarly, the rest parameters can be used to reflect the passed arguments:

<pre class="breakout"><code class="language-javascript">function checkParams(...params) {
    console.log(params[1], params[0], params[2]);    // 4 2 6
    console.log(arguments[1], arguments[0], arguments[2]);    // 4 2 6
}
checkParams(2, 4, 6);
</code></pre>

<p>The <code>arguments</code> object is an array-like object, but it lacks array methods such as <code>slice()</code> and <code>foreach()</code>. In order to use array methods on the <code>arguments</code> object, the object first needs to be converted into a real array:</p>

<pre><code class="language-javascript">function sort() {
    var a = Array.prototype.slice.call(arguments);
    return a.sort();
}
sort(40, 20, 50, 30);    // [20, 30, 40, 50]
</code></pre>

<p>In this function, <code>Array.prototype.slice.call()</code> is used as a quick way to convert the <code>arguments</code> object into an array. Next, the <code>sort()</code> method sorts the items of the array and returns it.</p>

<p>ECMAScript 6 has an even more straightforward way. <code>Array.from()</code>, a new addition in ECMAScript 6, creates a new array from any array-like object:</p>

<pre><code class="language-javascript">function sort() {
    var a = Array.from(arguments);
    return a.sort();
}
sort(40, 20, 50, 30);    // [20, 30, 40, 50]
</code></pre>

## The Length Property

<p>Although the arguments object is not technically an array, it has a <code>length</code> property that can be used to check the number of arguments passed to a function:</p>

<pre><code class="language-javascript">function countArguments() {
    console.log(arguments.length);
}
countArguments();    // 0
countArguments(10, null, "string");    // 3
</code></pre>

<p>By using the <code>length</code> property, we have a better control over the number of arguments passed to a function. For example, if a function requires two arguments to work, we could use the <code>length</code> property to check the number of passed arguments, and throw an error if they are fewer than expected:</p>

<pre class="breakout"><code class="language-javascript">function foo(param1, param2) {
    if (arguments.length &lt; 2) {
        throw new Error("This function expects at least two arguments");
    } else if (arguments.length === 2) {
        // do something
    }
}
</code></pre>

<p>Rest parameters are arrays, so they have a <code>length</code> property. In ECMAScript 6 the preceding code can be rewritten with rest parameters:</p>

<pre class="breakout"><code class="language-javascript">function foo(...params) {
  if (params.length &lt; 2) {
        throw new Error("This function expects at least two arguments");
    } else if (params.length === 2) {
        // do something
    }
}
</code></pre>

## The Callee And Caller Properties

<p>The <code>callee</code> property refers to the function that is currently running, and the <code>caller</code> refers to the function that has called the currently executing function. In ECMAScript 5 strict mode, these properties are deprecated, and attempting to access them causes a TypeError.</p>

<p>The <code>arguments.callee</code> property is useful in recursive functions (a recursive function is a regular function that refers to itself by its name), especially when the function name is not available (an anonymous function). Because an anonymous function doesn’t have a name, the only way to refer to it is by <code>arguments.callee</code>.</p>

<pre><code class="language-javascript">var result = (function(n) {
  if (n &lt;= 1) {
    return 1;
  } else {
    return n * arguments.callee(n - 1);
  }
})(4);   // 24
</code></pre>

## Arguments Object In Strict And Non-Strict Modes

<p>In ECMAScript 5 non-strict mode, the <code>arguments</code> object has an unusual feature: It keeps its values in sync with the values of the corresponding named parameters.</p>

Consider the following code fragment:

<pre><code class="language-javascript">function foo(param) {
   console.log(param === arguments[0]);    // true
   arguments[0] = 500;
   console.log(param === arguments[0]);    // true
   return param
}
foo(200);    // 500
</code></pre>

<p>Inside this function, a new value is assigned to <code>arguments[0]</code>. Because <code>arguments</code>’ values always stay in sync with the values of named parameters, the change to <code>arguments[0]</code> will also change the value of <code>param</code>. In fact, they are like two different names for the same variable. In ECMAScript 5 strict mode, this confusing behavior of the <code>arguments</code> object has been removed:</p>

<pre><code class="language-javascript">"use strict";
function foo(param) {
   console.log(param === arguments[0]);    // true
   arguments[0] = 500;
   console.log(param === arguments[0]);    // false
   return param
}
foo(200);   // 200
</code></pre>

<p>This time, changing <code>arguments[0]</code> doesn’t affect <code>param</code>, and the output is as expected. The output of this function in ECMAScript 6 is the same as in ECMAScript 5 strict mode, but keep in mind that when default values are used in the <code>function</code> declaration, the <code>arguments</code> object is not affected:</p>

<pre><code class="language-javascript">function foo(param1, param2 = 10, param3 = 20) {
   console.log(param1 === arguments[0]);    // true
   console.log(param2 === arguments[1]);    // true
   console.log(param3 === arguments[2]);    // false
   console.log(arguments[2]);    // undefined
   console.log(param3);    // 20
}
foo('string1', 'string2');
</code></pre>

<p>In this function, even though <code>param3</code> has a default value, it’s not equal to <code>arguments[2]</code> because only two argument are passed to the function. In other words, setting default values has no effect on the <code>arguments</code> object.</p>

## Conclusion

ECMAScript 6 has brought hundreds of small and big improvements to JavaScript. More and more, developers are using ECMAScript 6 features, and soon these features will be unavoidable. In this tutorial, we’ve learned how ECMAScript 6 has upgraded parameter handling in JavaScript, but we’ve just scratched the surface of ECMAScript 6. A lot of other new and interesting features of the language are worth checking out.

### Links

- [ECMAScript 6 Compatibility Table](https://kangax.github.io/compat-table/es6/), Juriy Zaytsev
- “[ECMAScript 2015 Language Specification](https://www.ecma-international.org/ecma-262/6.0/),” ECMA International

{{< signature "rb, ml, al, il" >}}

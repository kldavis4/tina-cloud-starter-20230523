---
title: '10 Oddities And Secrets About JavaScript'
slug: 10-oddities-and-secrets-about-javascript
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ce14553a-26c9-4d44-b6c0-d65176b6ccb0/ten-yellow-illustrator-illu.jpg
date: 2011-05-30T11:11:42.000Z
author: andy-croxall
summary: >-
  A collection of JavaScript’s curiosities and well-kept secrets for intermediate developers. Andy Croxall gives you an insight into how these oddities can be useful to your code. 
description: >-
  A collection of JavaScript’s curiosities and well-kept secrets for intermediate developers. Andy Croxall gives you an insight into how these oddities can be useful to your code.
categories:
  - Coding
  - JavaScript
  - Mathematics
  - Errors
  - Essentials
---

JavaScript. At once bizarre and yet beautiful, it is surely the programming language that Pablo Picasso would have invented. Null is apparently an object, an empty array is apparently equal to <code>false</code>, and functions are bandied around as though they were tennis balls.

This article is aimed at intermediate developers who are curious about more advanced JavaScript. It is a collection of JavaScript’s oddities and well-kept secrets. Some sections will hopefully give you insight into how these curiosities can be useful to your code, while other sections are pure WTF material. So, let’s get started.

{{% feature-panel %}}

## Data Types And Definitions

### 1. Null is an Object

Let’s start with everyone’s favorite JavaScript oddity, as well known as it is. Null is apparently an object, which, as far as contradictions go, is right up there with the best of them. Null? An object? “Surely, the definition of null is the **total absence of meaningful value**,” you say. You’d be right. But that’s the way it is. Here’s the proof:

<pre><code class="language-javascript">alert(typeof null); //alerts 'object'</code></pre>

Despite this, null is not considered an instance *of* an object. (In case you didn’t know, values in JavaScript are instances of base objects. So, every number is an instance of the <code>Number</code> object, every object is an instance of the <code>Object</code> object, and so on.) This brings us back to sanity, because if null is the absence of value, then it obviously can’t be an instance of anything. Hence, the following evaluates to <code>false</code>:

<pre><code class="language-javascript">alert(null instanceof Object); //evaluates false</code></pre>

### 2. NaN is a Number

You thought null being an object was ridiculous? Try dealing with the idea of <code>NaN</code> &mdash; “not a number” &mdash; being a number! Moreover, <code>NaN</code> is not considered equal to itself! Does your head hurt yet?

<pre><code class="language-javascript">alert(typeof NaN); //alerts 'Number'
alert(NaN === NaN); //evaluates false</code></pre>

In fact <code>NaN</code> is **not equal to anything**. The only way to confirm that something is <code>NaN</code> is via the function <code>isNaN()</code>.

### 3. An Array With No Keys == False (About Truthy and Falsy)

Here’s another much-loved JavaScript oddity:

<pre><code class="language-javascript">alert(new Array() == false); //evaluates true</code></pre>

To understand what’s happening here, you need to understand the concepts of **truthy and falsy**. These are sort of true/false-lite, which will anger you somewhat if you majored in logic or philosophy.

I’ve read many explanations of what truthy and falsy are, and I feel the easiest one to understand is this: in JavaScript, **every non-boolean value has a built-in boolean flag** that is called on when the value is asked to behave like a boolean; like, for example, when you compare it to a boolean.

Because apples cannot be compared to pears, when JavaScript is asked to compare values of differing data types, it first “**coerces**” them into a common data type. <code>False</code>, <code>zero</code>, <code>null</code>, <code>undefined</code>, empty strings and <code>NaN</code> all end up becoming <code>false</code> &mdash; not permanently, just for the given expression. An example to the rescue:

<pre><code class="language-javascript">var someVar = 0;
alert(someVar == false); //evaluates true</code></pre>

Here, we’re attempting to compare the number <code>0</code> to the boolean <code>false</code>. Because these data types are incompatible, **JavaScript secretly coerces our variable into its truthy or falsy equivalent**, which in the case of <code>0</code> (as I said above) is falsy.

You may have noticed that I didn’t include empty arrays in the list of falsies above. Empty arrays are curious things: they actually evaluate to truthy *but*, when compared against a boolean, behave like a falsy. Confused yet? With good cause. Another example perhaps?

<pre><code class="language-javascript">var someVar = []; //empty array
alert(someVar == false); //evaluates true
if (someVar) alert('hello'); //alert runs, so someVar evaluates to true</code></pre>

To avoid coercion, you can use the **value and type comparison operator**, <code>===</code>, (as opposed to <code>==</code>, which compares only by value). So:

<pre><code class="language-javascript">var someVar = 0;
alert(someVar == false); //evaluates true &ndash; zero is a falsy
alert(someVar === false); //evaluates false &ndash; zero is a number, not a boolean</code></pre>

Phew. As you’ve probably gathered, this is a broad topic, and I recommend reading up more on it &mdash; particularly on data coercion, which, while not uniquely a JavaScript concept, is nonetheless prominent in JavaScript.

I discuss the concept of truthy and falsy and data coercion more over here. And if you really want to sink your teeth into what happens internally when JavaScript is asked to compare two values, then check out <a href="https://www.mozilla.org/js/language/E262-3.pdf">section 11.9.3 of the ECMA-262</a> document specification.

## Regular Expressions

### 4. replace() Can Accept a Callback Function

This is one of JavaScript’s best-kept secrets and arrived in v1.3. Most usages of <code>replace()</code> look something like this:

<pre><code class="language-javascript">alert('10 13 21 48 52'.replace(/d+/g, '*')); //replace all numbers with *</code></pre>

This is a simple replacement: a string, an asterisk. But what if we wanted more control over how and when our replacements take place? What if we wanted to replace only numbers under 30? This can’t be achieved with regular expressions alone (they’re all about strings, after all, not maths). We need to **jump into a callback function to evaluate each match**.

<pre><code class="language-javascript">alert('10 13 21 48 52'.replace(/d+/g, function(match) {
	return parseInt(match) &lt; 30 ? '*' : match;
}));</code></pre>

For every match made, JavaScript calls our function, passing the match into our match argument. Then, we return either the asterisk (if the number matched is under 30) or the match itself (i.e. no match should take place).

### 5. Regular Expressions: More Than Just Match and Replace

Many intermediate JavaScript developers get by just on <code>match</code> and <code>replace</code> with regular expressions. But JavaScript defines more methods than these two.

Of particular interest is <code>test()</code>, which works like <code>match</code> except that it doesn’t return matches: **it simply confirms whether a pattern matches**. In this sense, it is computationally lighter.

<pre><code class="language-javascript">alert(/w{3,}/.test('Hello')); //alerts 'true'</code></pre>

The above looks for a pattern of three or more alphanumeric characters, and because the string <code>Hello</code> meets that requirement, we get <code>true</code>. We don’t get the actual match, just the result.

Also of note is the <code>RegExp</code> object, by which you can create dynamic regular expressions, as opposed to static ones. The majority of regular expressions are declared using short form (i.e. enclosed in forward slashes, as we did above). That way, though, **you can’t reference variables, so making dynamic patterns is impossible**. With <code>RegExp()</code>, though, you can.

<pre><code class="language-javascript">function findWord(word, string) {
	var instancesOfWord = string.match(new RegExp('b'+word+'b', 'ig'));
	alert(instancesOfWord);
}
findWord('car', 'Carl went to buy a car but had forgotten his credit card.');</code></pre>

Here, we’re making a dynamic pattern based on the value of the argument <code>word</code>. The function returns the number of times that <code>word</code> appears in string as a word in its own right (i.e. not as a part of other words). So, our example returns <code>car</code> once, ignoring the <code>car</code> tokens in the words <code>Carl</code> and <code>card</code>. It forces this by checking for a word boundary (<code>b</code>) on either side of the word that we’re looking for.

Because <code>RegExp</code> are specified as strings, not via forward-slash syntax, we can use variables in building the pattern. This also means, however, that we must double-escape any special characters, as we did with our word boundary character.

## Functions And Scope

### 6. You Can Fake Scope

The scope in which something executes defines what variables are accessible. Free-standing JavaScript (i.e. JavaScript that does not run inside a function) operates within the global scope of the <code>window</code> object, to which everything has access; whereas local variables declared inside functions are accessible only within that function, not outside.

<pre><code class="language-javascript">var animal = 'dog';
function getAnimal(adjective) { alert(adjective+' '+this.animal); }
getAnimal('lovely'); //alerts 'lovely dog';</code></pre>

Here, our variable and function are both declared in the global scope (i.e. on <code>window</code>). Because this always points to the current scope, in this example it points to <code>window</code>. Therefore, the function looks for <code>window.animal</code>, which it finds. So far, so normal. But we can actually **con our function into thinking that it’s running in a different scope**, regardless of its own natural scope. We do this by calling its built-in <code>call()</code> method, rather than the function itself:

<pre><code class="language-javascript">var animal = 'dog';
function getAnimal(adjective) { alert(adjective+' '+this.animal); };
var myObj = {animal: 'camel'};
getAnimal.call(myObj, 'lovely'); //alerts 'lovely camel'</code></pre>

Here, our function runs not on <code>window</code> but on <code>myObj</code> &mdash; specified as the first argument of the call method. Essentially, <code>call()</code> pretends that our function is a method of <code>myObj</code> (if this doesn’t make sense, you might want to read up on JavaScript’s system of prototypal inheritance). Note also that any arguments we pass to <code>call()</code> after the first will be passed on to our function &mdash; hence we’re passing in <code>lovely</code> as our <code>adjective</code> argument.

I’ve heard JavaScript developers say that they’ve gone years without ever needing to use this, not least because good code design ensures that you don’t need this smoke and mirrors. Nonetheless, it’s certainly an interesting one.

As an aside, <code>apply()</code> does the same job as <code>call()</code>, except that arguments to the function are specified as an array, rather than as individual arguments. So, the above example using <code>apply()</code> would look like this:

<pre><code class="language-javascript">getAnimal.apply(myObj, ['lovely']); //func args sent as array</code></pre>

{{% ad-panel-leaderboard %}}

### 7. Functions Can Execute Themselves

There’s no denying it:

<pre><code class="language-javascript">(function() { alert('hello'); })(); //alerts 'hello'</code></pre>

The syntax is simple enough: we declare a function and immediately call it just as we call other functions, with <code>()</code> syntax. You might wonder why we would do this. It seems like a contradiction in terms: a function normally contains code that we want to execute later, not now, otherwise we wouldn’t have put the code in a function.

One good use of self-executing functions (SEFs) is to **bind the current values of variables** for use inside delayed code, such as callbacks to events, timeouts and intervals. Here is the problem:

<pre><code class="language-javascript">var someVar = 'hello';
setTimeout(function() { alert(someVar); }, 1000);
var someVar = 'goodbye';</code></pre>

Newbies in forums invariably ask why the <code>alert</code> in the <code>timeout</code> says <code>goodbye</code> and not <code>hello</code>. The answer is that the <code>timeout</code> callback function is precisely that &mdash; a callback &mdash; so it doesn’t evaluate the value of <code>someVar</code> until it runs. And by then, <code>someVar</code> has long since been overwritten by <code>goodbye</code>.

SEFs provide a solution to this problem. Instead of specifying the timeout callback implicitly as we do above, we return it from an SEF, into which we pass the current value of <code>someVar</code> as arguments. Effectively, this means **we pass in and isolate the current value of <code>someVar</code>, protecting it from whatever happens to the actual variable <code>someVar</code> thereafter**. This is like taking a photo of a car before you respray it; the photo will not update with the resprayed color; it will forever show the color of the car at the time the photo was taken.

<pre><code class="language-javascript">var someVar = 'hello';
setTimeout((function(someVar) {
	return function()  { alert(someVar); }
})(someVar), 1000);
var someVar = 'goodbye';</code></pre>

This time, it alerts <code>hello</code>, as desired, because it is alerting the isolated version of <code>someVar</code> (i.e. the function argument, *not* the outer variable).

## The Browser

### 8. Firefox Reads and Returns Colors in RGB, Not Hex

I’ve never really understood why Mozilla does this. Surely it realizes that anyone interrogating computed colors via JavaScript is interested in hex format and not RGB. To clarify, here’s an example:

<pre><code class="language-markup tmp-html">

Hello, world!

&lt;script&gt;
var ie = navigator.appVersion.indexOf('MSIE') != -1;
var p = document.getElementById('somePara');
alert(ie ? p.currentStyle.color : getComputedStyle(p, null).color);
&lt;/script&gt;</code></pre>

While most browsers will alert <code>ff9900</code>, Firefox returns <code>rgb(255, 153, 0)</code>, the RGB equivalent. Plenty of JavaScript functions are out there for converting RGB to hex.

Note that when I say computed color, I’m referring to the current color, **regardless of how it is applied to the element**. Compare this to style, which reads only style properties that were implicitly set in an element’s style attribute. Also, as you’ll have noticed in the example above, IE has a different method of detecting computed styles from other browsers.

As an aside, jQuery’s <code>css()</code> method encompasses this sort of computed detection, and it returns styles however they were applied to an element: implicitly or through inheritance or whatever. Therefore, you would relatively rarely need the native <code>getComputedStyle</code> and <code>currentStyle</code>.

## Miscellaneous

### 9. 0.1 + 0.2 !== 0.3

This one is an oddity not just in JavaScript; it’s actually a prevailing problem in computer science, and it affects many languages. The output of this is 0.30000000000000004.

This has to do with an issue called **machine precision**. When JavaScript tries to execute the line above, it converts the values to their binary equivalents.

This is where the problem starts. 0.1 is not really 0.1 but rather its binary equivalent, **which is a near-ish (but not identical) value**. In essence, as soon as you write the values, they are doomed to lose their precision. You might have just wanted two simple decimals, but what you get, as Chris Pine notes, is binary floating-point arithmetic. Sort of like wanting your text translated into Russian but getting Belorussian. Similar, but not the same.

More is going on here, but it’s beyond the scope of this article (not to mention the mathematical capabilities of this author).

Workarounds for this problem are a favorite on computer science and developer forums. Your choice, to a point, comes down to the sort of calculations you’re doing. The pros and cons of each are beyond the scope of this article, but the common choice is between the following:

1.  Converting to integers and calculating on those instead, then converting back to decimals afterward; or
2.  Tweaking your logic to **allow for a range rather than a specific result**.

So, for example, rather than…

<pre><code class="language-javascript">var num1 = 0.1, num2 = 0.2, shouldEqual = 0.3;
alert(num1 + num2 == shouldEqual); //false</code></pre>

… we would do this:

<pre><code class="language-javascript">alert(num1 + num2 &gt; shouldEqual - 0.001 &amp;&amp; num1 + num2 &lt; shouldEqual + 0.001); //true</code></pre>

Translated, this says that because 0.1 + 0.2 is apparently not 0.3, check instead that it’s **more or less** 0.3 &mdash; specifically, within a range of 0.001 on either side of it. The obvious drawback is that, for very precise calculations, this will return inaccurate results.

### 10. Undefined Can Be Defined

OK, let’s end with a silly, rather inconsequential one. Strange as it might sound, <code>undefined</code> is not actually a reserved word in JavaScript, even though it has a special meaning and is the only way to determine whether a variable is undefined. So:

<pre><code class="language-javascript">var someVar;
alert(someVar == undefined); //evaluates true</code></pre>

So far, so normal. But:

<pre><code class="language-javascript">undefined = "I'm not undefined!";
var someVar;
alert(someVar == undefined); //evaluates false!</code></pre>

You can also check <a href="https://developer.mozilla.org/en/JavaScript/Reference/Reserved_Words">Mozilla’s list of all reserved words in JavaScript</a> for future reference.

{{% ad-panel-leaderboard %}}

## Further Resources

*   [JavaScript Oddities Explained. Comparing.](https://blog.frontendforce.com/2010/05/javascript-oddities-explained-comparing)
*   [JavaScript Gotchas](https://www.evotech.net/blog/2008/10/13-javascript-gotchas/)
*   [Yet More on Gotchas](https://www.codeproject.com/KB/scripting/javascript-gotchas.aspx)
*   [replace() callback functions](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/String/Replace)

### Further Reading

*   [JavaScript Profiling With The Chrome Developer Tools](https://www.smashingmagazine.com/2012/06/javascript-profiling-chrome-developer-tools/)
*   [Writing Fast, Memory-Efficient JavaScript](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)
*   [Powerful Workflow Tips, Tools And Tricks For Web Designers](https://www.smashingmagazine.com/2013/10/powerful-workflow-tips-tools-and-tricks-for-web-designers/)
*   [The Future Of Frontend Build Tools](https://www.smashingmagazine.com/2022/06/future-frontend-build-tools/)

{{< signature "al, il, mrn" >}}

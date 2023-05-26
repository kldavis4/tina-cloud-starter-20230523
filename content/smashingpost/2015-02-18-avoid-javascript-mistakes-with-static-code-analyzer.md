---
title: Terrible JavaScript Mistakes To Avoid With A Static Code Analyzer
slug: avoid-javascript-mistakes-with-static-code-analyzer
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a0763142-7f68-46b6-a584-48cf9187c75c/js-blue-code-illu-opt.png
date: 2015-02-18T23:05:59.000Z
author: zack-grossbart
description: >-
  Hardly any line of my code comes out perfect the first time I write it. Well,
  most of the time… Some of the time… Um, hardly ever. The truth is that I spend
  more time chasing down my own stupid programming errors than I’d like to
  admit. That’s why I use static analyzers in every JavaScript file I write.

  Static analyzers look at code and find problems before you run it. They do
  simple checks, like enforcing syntax (for example, tabs instead of spaces),
  and more holistic checks, like making sure your functions aren’t too complex.
  Static analyzers also **find errors that you can’t find with testing**, like
  instances of `==` when you meant `===`.
categories:
  - Coding
  - JavaScript
  - Errors
  - Web Development
---
Hardly any line of my code comes out perfect the first time I write it. Well, most of the time… Some of the time… Um, hardly ever. The truth is that I spend more time chasing down my own stupid programming errors than I’d like to admit. That’s why I use static analyzers in every JavaScript file I write.

Static analyzers look at code and find problems before you run it. They do simple checks, like enforcing syntax (for example, tabs instead of spaces), and more holistic checks, like making sure your functions aren’t too complex. Static analyzers also <strong>find errors that you can’t find with testing</strong>, like instances of <code>==</code> when you meant <code>===</code>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Stylelint: The Style Sheet Linter We’ve Always Wanted](https://www.smashingmagazine.com/2016/05/stylelint-the-style-sheet-linter-weve-always-wanted/)
*   [ESLint: The Next-Generation JavaScript Linter](https://www.smashingmagazine.com/2015/09/eslint-the-next-generation-javascript-linter/)
*   [Why Coding Style Matters](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/)

In large projects and on big teams, you’ll be happy to have a little help finding those “simple” bugs that turn out to be a lot less simple than they looked.

{{% feature-panel %}}

## JSLint, JSHint And Closure Compiler

You have three main choices for static analyzers in the JavaScript world: <a href="https://www.jslint.com/">JSLint</a>, <a href="https://www.jshint.com/">JSHint</a> and <a href="https://developers.google.com/closure/compiler/">Closure Compiler</a>.</p>

### JSLint

JSLint was the first static analyzer for JavaScript. You can run it <a href="https://www.jslint.com/">on the official website</a> or use <a href="https://code.google.com/p/jslint4java/">one of the wrappers</a> to run it on your local files. JSLint finds a lot of useful errors, but it’s very rigid. Here’s a good example:

<pre><code class="language-javascript">
var s = 'mystring';
for (var i = 0; i &lt; s.length; i++) {
  console.log(s.charAt(i));
}</code></pre>

JSLint will show two errors for this code:

<pre><code class="language-javascript">Unexpected '++'.
Move 'var' declarations to the top of the function.</code></pre>

The first problem is the declaration of the variable <code>i</code> at the top of the loop. JSLint also doesn’t like the <code>++</code> operator at the end of the loop declaration. It wants the code to look like this:

<pre><code class="language-javascript">
var s = 'mystring';
var i;
for (i = 0; i &lt; s.length; i = i + 1) {
  console.log(s.charAt(i));
}</code></pre>

I appreciate where JSLint is coming from, but it’s just too strict for me. It was too rigid for <a href="https://anton.kovalyov.net/">Anton Kovalyov</a> as well, so he created JSHint.</p>

### JSHint

JSHint works similarly to JSLint, but it’s written on top of <a href="https://nodejs.org/">Node.js</a> and it’s much more flexible. JSHint has a <a href="https://www.jshint.com/docs/options/">long list of options</a>, making it possible to create custom checks by <a href="https://www.jshint.com/docs/reporters/">writing your own reporter</a>.

You can run JSHint from <a href="https://jshint.com/">the website</a>, but most of the time you would <a href="https://jshint.com/install/">install JSHint as a local command-line tool</a> using Node.js. Once JSHint is installed, you can run it against your files with a command like this:

<pre><code class="language-javascript">
jshint test.js</code></pre>

JSHint also has plugins for popular text editors, so you can run JSHint while you’re coding.</p>

### Closure Compiler

Closure Compiler, from Google, is a different breed. As the name suggests, it’s a compiler as well as a checker. It’s written in Java and based on the <a href="https://developer.mozilla.org/en-US/docs/Mozilla/Projects/Rhino">Rhino</a> parser from Mozilla. Closure Compiler has a simple mode to do basic code checking, but it also has more advanced modes to do extra checking and enforce special type declarations.

Closure Compiler reports errors in JavaScript code, but it also creates minimized versions of JavaScript. The compiler removes white space, comments and unused variables and simplifies long statements to make a script as small as possible.

Google makes a simple version of its compiler <a href="https://closure-compiler.appspot.com/home">available on the Web</a>, but most of the time you’ll want to <a href="https://developers.google.com/closure/compiler/">download Closure Compiler</a> and run it locally.

Closure Compiler will output a list of files into a single minimized file after checking their code. You can run it like that after you’ve downloaded the <code>compiler.jar</code> file.

<pre><code class="language-javascript">
java -jar compiler.jar --js_output_file compress.js --js test1.js --js test2.js</code></pre>

### Choosing the Right Checker

In my projects, I combine Closure Compiler with JSHint. Closure Compiler does the minimization and basic checking, while JSHint handles the more complex code analysis. The two work well together, and each covers some areas that the other doesn’t. In addition, I can use the extension capabilities of JSHint to write custom checkers. One common checker I write checks for particular functions that I don’t want, like calling functions that I don’t want to allow in my project.

Now that we’ve looked at a few checkers, let’s look at some bad code. All of these six examples are code you should never write and are spots where code checkers would keep you out of trouble.

This article uses JSHint for most examples, but Closure Compiler would produce similar warnings.</p>

## == Versus ===

JavaScript is a <a href="https://www.smashingmagazine.com/2013/04/18/introduction-to-programming-type-systems/">dynamically typed</a> language. You don’t have to declare types when you’re coding, but they exist at runtime. JavaScript offers two compare operators to handle these dynamic types: <code>==</code> and <code>===</code>. Let’s look at an example.

<pre><code class="language-javascript">
var n = 123;
var s = '123';

if (n == s) {
  alert('The variables were equal');
}

if (n === s) {
  alert('The variables were identical');
}</code></pre>

The <code>==</code> operator compares the values of the two objects. It converts the objects and compares them separately from their types. The <code>===</code> operator compares the object types and the values. In this case, the first <code>if</code> block will pop up an alert, and the second <code>if</code> block won’t — because <code>n</code> and <code>s</code> have the same value but not the same type.

The <code>==</code> comparator is a relic from the C language roots of JavaScript. Using it is almost always a mistake: Comparing values separate from types is rarely what the developer means to do. In reality, the number “one hundred twenty-three” is different from the string “one two three.” These operators are easy to mistype and even easier to misread.

Check this code with JSHint and you’ll get this:

<pre><code class="language-javascript">test.js: line 9, col 12, Expected '===' and instead saw '=='.</code></pre>

## Undefined Variables And Late Definitions

Let’s start with some simple code:

<pre><code class="language-javascript">
function test() {
  var myVar = 'Hello, World';
  console.log(myvar);
}</code></pre>

See the bug? I make this mistake all the time. Run this code and you’ll get an error:

<pre><code class="language-javascript">ReferenceError: myvar is not defined</code></pre>

Let’s make the problem a little more difficult to spot:

<pre><code class="language-javascript">
function test() {
  myVar = 'Hello, World';
  console.log(myVar);
}</code></pre>

Run this and you’ll get:

<pre><code class="language-javascript">Hello, World</code></pre>

This second example works, but it has some very unexpected side effects. The rules for declaring JavaScript variables and the scopes they end up in are confusing at best.

In the first case, JSHint will tell you this:

<pre><code class="language-javascript">
test.js: line 3, col 17, 'myvar' is not defined.
</code></pre>

In the second case, it will tell you this:

<pre><code class="language-javascript">
test.js: line 2, col 5, 'myVar' is not defined.
test.js: line 3, col 17, 'myVar' is not defined.
</code></pre>

The first case saves you from a runtime bug. You don’t have to test your app — JSHint will find the error for you. The second case is worse because testing won’t find the bug.

The problem with the second case is insidiously subtle and complex. The variable <code>myVar</code> has now escaped from its function scope and been <a href="https://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html">hoisted</a> into the global scope for the whole page. This means that it will exist and have a value of <code>Hello, World</code> after the <code>test</code> function has run. This is called “global scope pollution.”

The <code>myVar</code> variable will exist for every other function that runs after the <code>test</code> function. Run the following code after you’ve run the <code>test</code> function:

<pre><code class="language-javascript">
console.log('myVar: ' + myVar);</code></pre>

You’ll still get <code>Hello, World</code>. The <code>myVar</code> variable will hang around your code like mold, causing tricky bugs you won’t find until 3:00 am the night before you release, all because you forgot to type <code>var</code>.</p>

## Variable Reuse

Redefining variables is allowed in JavaScript, but it’s almost always an accident. Take a look:

<pre><code class="language-javascript">
function incrementCount(counter) {
  if (counter.count) {
    counter.count++;
  } else {
    var counter = 1;
    counter.count = counter;
  }
}</code></pre>

In this function we’re incrementing the <code>count</code> property on the object that was passed in, but we need to add the property if it doesn’t already exist. See the bug?

This function will never add or increment a counter on anything. The <code>else</code> statement will always be called, and it will redefine the function argument <code>counter</code>. Basically this function creates a new object, assigns a property to it and then loses the object when the function returns. It will never change the object that was passed in.

This simple typo will make the code run without any errors but will produce a very strange result.

JSHint will tell you this:

<pre><code class="language-javascript">
test.js: line 21, col 21, 'counter' is already defined.
</code></pre>

## Curly Braces In Blocks, Loops And Conditionals

<pre><code class="language-javascript">
if (false)
  doSomethingElse();
  doSomething();
</code></pre>

Will this code <code>doSomething</code> or <code>doSomethingElse</code>? At first glance, I always think it won’t <code>doSomething</code> or <code>doSomethingElse</code>. That’s the way it works in Python, but not in JavaScript. JavaScript will treat the one line after the <code>if</code> statement merely as part of the block; the indenting doesn’t matter.

This issue is simply about code readability. If you can’t understand what the code will do, then you’ll write bugs.

Python and CoffeeScript like to skip the curly braces. That might work fine in languages that guarantee to format white space well, but JavaScript is looser than that. JavaScript allows a lot of strange syntax, and curly braces will keep you out of trouble.

<pre><code class="language-javascript">
if (false) {
  doSomethingElse();
  doSomething();
}</code></pre>

Add the braces and you’ll always make code more readable. Skip them and JSHint will tell you this:

<pre><code class="language-javascript">
test.js: line 27, col 5, Expected '{' and instead saw 'doSomething'.
</code></pre>

## Single And Double Quotes

<pre><code class="language-javascript">
console.log("This is a string. It's OK.");
console.log('This string is OK too.');
console.log("This string " + 'is legal, but' + "really not OK.");
</code></pre>

JavaScript allows you to define a string with single or double quotes. It’s nice to have the flexibility, like when you’re defining HTML, but the added flexibility can lead to some very inconsistent code.

Google has a code style guide that always uses single quotes for strings, so that they don’t have to escape double quotes in HTML. I can’t argue that single quotes are better than double quotes, but I can argue for consistency. Keeping everything consistent makes code more readable.

JSHint will warn you about mixed quotes like this:

<pre><code class="language-javascript">
test.js: line 31, col 27, Mixed double and single quotes.
</code></pre>

Copying and pasting or mistyping a quote is easy. Once you have one bad quote, others will follow, especially if a lot of people are editing the file. Static analyzers will help keep the quotes consistent and prevent a big cleanup in the future.</p>

## Cyclomatic Complexity

<a href="https://en.wikipedia.org/wiki/Cyclomatic_complexity">Cyclomatic complexity</a> is the measure of how complex a given block of code is. Look at the code and count the number of paths that could possibly run: That number is its cyclomatic complexity.

For example, this code has a cyclomatic complexity of 1:

<pre><code class="language-javascript">
function main() {
  return 'Hello, World!';
}
</code></pre>

You can follow only one path through this code.

Let’s add a little conditional logic:

<pre><code class="language-javascript">
function main() {
  if (true) {
    return 'Hello, World!';
  } else {
    return 'Hello, unWorld!';
  }
}
</code></pre>

The cyclomatic complexity has jumped to 2.

Ideal code is easy to read and understand. The higher the cyclomatic complexity, the more difficult the code will be to understand. Everyone agrees that high cyclomatic complexity is bad, but no one agrees on a limit; 5 is fine, and 100 is too high — but there’s a lot of gray area in the middle.

If the cyclomatic complexity gets to the predefined limit, then JSHint will let you know.

<pre><code class="language-javascript">
test.js: line 35, col 24, This function's cyclomatic complexity is too high. (17)
</code></pre>

JSHint is the only one of the three checkers that looks at cyclomatic complexity. It also allows you to set the limit. Go above the <code>maxcomplexity</code> number that you’ve set and JSHint will warn you. I like to set the limit to 14, but I’ll go a little higher in projects in which I do a lot of parsing or when I have other reasons to need many code paths.

The real reason the complexity number is important is that it tells you when to refactor your code. The first time you write a long function, it always makes sense. But if you wait six months and then come back to fix bugs, you’ll be glad that you took the time to make it easier to read.

Cyclomatic complexity usually breaks down with laundry lists. For example, I created a calendar, and I wanted to get the correct first day of the week for each country. I had a function that looked something like this:

<pre><code class="language-javascript">
function getFirstDay(country) {
  if (country === 'USA') {
    return 'Sunday';
  } else if (country === 'France') {
    return 'Monday';
  } else if…
}
</code></pre>

I supported a lot of countries, so the cyclomatic complexity quickly grew to over 50. Although the code was very easy to read, the number of paths was high, so my code analyzer complained. In the end, I split up the function to get the complexity below my maximum. It was a hack for this particular case, but it’s a small price to pay for cleaner code overall.</p>

## Check Everything That You’ll Ever Edit More Than Once

Static checkers find the bugs that you wouldn’t come across with simple testing. They also find bugs at compile time, as opposed to runtime — those middle-of-the-night bugs that only creep in when a dozen people are all trying to do the same thing. Finding all of those subtle bugs is a long and painful process without code checking.

I began this article by claiming that I always use a code analyzer, but I don’t in one case: with throwaway code. I like using quick prototypes to show interactive ideas and to help my team come together on how something should work. Those prototypes are write-once code; I never need to fix bugs in them because I’ll be throwing away the prototypes a few weeks later. This throwaway code exists solely for the quick demos, and I don’t care if it has subtle bugs. Everything I care about, though, gets analyzed.

Fixing these types of bugs at the beginning of a project is easy; finding them on the night before you release will drive you nuts. Code analyzers have saved my butt many times, and they’ll also save yours.

<em>Image on front page created by <a href="https://www.flickr.com/photos/7162499@N02/3260095534/">Ruiwen Chua</a>.</em>

{{< signature "al, ml, da" >}}


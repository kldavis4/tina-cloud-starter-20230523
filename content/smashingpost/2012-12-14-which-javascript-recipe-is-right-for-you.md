---
title: Which JavaScript Recipe Is Right For You?
slug: which-javascript-recipe-is-right-for-you
image: null
date: 2012-12-14T16:01:35.000Z
author: zack-grossbart
description: >-
  JavaScript has been called everything from great to awful to the [assembly
  language](https://en.wikipedia.org/wiki/Assembly_language) of the Web, but we
  all use it. Love JavaScript or hate it: everyone admits there are serious
  flaws and not many other choices.
categories:
  - Coding
  - JavaScript
---
JavaScript has been called everything from great to awful to the <a href="https://en.wikipedia.org/wiki/Assembly_language">assembly language</a> of the Web, but we all use it. Love JavaScript or hate it: everyone admits there are serious flaws and not many other choices.

Let's start with some fundamental negatives. JavaScript has no good answer for some really basic features of modern programming languages: private variables and functions, packages and modules, standard localization mechanisms, code completion in editors.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Terrible JavaScript Mistakes To Avoid With A Static Code Analyzer](https://www.smashingmagazine.com/2015/02/avoid-javascript-mistakes-with-static-code-analyzer/)
*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)
*   [ESLint: The Next-Generation JavaScript Linter](https://www.smashingmagazine.com/2015/09/eslint-the-next-generation-javascript-linter/)
*   [Why Coding Style Matters](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/)

While JavaScript is missing a lot of features, it's the very dynamic nature of the language that scares so many static programming believers. This is all valid JavaScript:

{{% feature-panel %}}

<pre><code class="language-javascript">obj1 = {
    func1: function() {
        return "I'm function 1";
    }
};

obj1['func2'] = function() {
    return "I'm function 2";
};

obj1['fu' + 'nc' + 3] = function() {
    return "I'm function 3";
}

var f = 'func4';

obj1[f] = function() {
    return "I'm function 4";
}

alert(obj1.func2());
alert(obj1.func3());
alert(obj1.func4());</code></pre>

Most languages support <a href="https://en.wikipedia.org/wiki/Reflection_(computer_programming)">dynamic code loading</a>, but JavaScript encourages it. JavaScript has a lot of dark corners. Did you know that adding two arrays in JavaScript results in an empty string, or that <code>[] + {}</code> results in the string <code>[object Object]</code> but <code>{} + []</code> is 0? <a href="https://www.destroyallsoftware.com/talks/wat">Wat</a>?!?

JavaScript makes it so easy to write unreadable code that it's <a href="https://blogs.adobe.com/bparadie/2012/05/07/the-pew-pew-manifesto/">impossible to write large projects in JavaScript</a>… except for Twitter, Facebook, Google, every big website you've ever heard of and hundreds of others.

These shortcomings cause me problems every day, but I still love JavaScript. It's fun to code and it's far from the assembly language of the Web. Assembly is nearly impossible to write by hand and even harder to read:

<pre>C005 B7 80 04        STA A  ACIA
C008 86 11           LDA A
C00A B7 80 04        STA A  ACIA
</pre>

JavaScript is easy to write. If I have a button and want to know when someone clicks it, I could import a library like <a href="https://jquery.com/">jQuery</a> and write a <code>click</code> function:

<pre><code class="language-javascript">$('#myButton').click(function() {
    alert('I was clicked');
});</code></pre>

Your grandmother can guess what this code does. That's why JavaScript is a good <a href="https://www.stanford.edu/class/cs101/">first programming language</a> and a great prototyping language. JavaScript programs go from a blank page to a working app ridiculously fast. They're quick to write, don't require a compiler and allow you to do anything you need.

These two views of JavaScript are difficult to reconcile. Is JavaScript an ill-defined loose language designed to cause premature gray hair, or a fun place to work? The answer is both.

We face this choice with every new Web project. <strong>Should we write JavaScript, or another language that generates it?</strong> This article shows you how to choose.

## JavaScript Is Constantly Improving

JavaScript is the most popular client-side programming language in the world. It's tough to find a website that doesn't run it. It's also come a long way with the introduction of excellent libraries like <a href="https://jquery.com/">jQuery</a>, <a href="https://backbonejs.org/">Backbone</a> and countless others. JavaScript wins easily for small projects, but it falters when the projects and teams get larger.

Every large JavaScript project adopts conventions to compensate for the lack of language features. They're simple patterns like using an underscore to mark some functions as private, or adding comments before arguments to indicate the expected type.

<pre><code class="language-javascript">function formatDate(/* Date */ d) {
    var day = d.getDate();
    var month = d.getMonth() + 1;
    var year = d.getFullYear();
    return date + "-" + month + "-" + year;
}</code></pre>

These comments help, but there's nothing to stop you from passing a string, number or anything else to the <code>formatDate</code> function. You can't enforce a coding convention and you'll never know it's broken until the code actually runs in your production environment and fails. Extra type checking like <code>instanceOf</code> makes the program fail with a better error message, but it still fails at runtime instead of getting caught by the compiler.

Tools like <a href="https://www.jslint.com/">JSLint</a> or <a href="https://www.jshint.com/">JSHint</a> find common syntax problems like using <code>==</code> when you should have used <code>===</code>, but they don't address the larger issues. Libraries like <a href="https://requirejs.org/">RequireJS</a> provide some support for modules in JavaScript, but that's still just a convention. With nothing to enforce these patterns, you'll spend endless hours tracking down annoying bugs. It's never fun to debug someone else's JavaScript.

Programmers love coming up with new solutions to existing problems, but there aren't many good alternatives to JavaScript.</p>

## Google Web Toolkit (GWT)

Google made the first major effort to replace JavaScript with <a href="https://developers.google.com/web-toolkit/">GWT</a>. The idea was to write Java code and compile it into JavaScript. Java provides many of the language features JavaScript is missing, and the compiler makes it possible to do a lot of checking before your code runs. With a nice debugger and a UI library added in, GWT looked like it would take over the world.

It didn't.

GWT hasn't failed (yet), but it hasn't succeeded either. Java is a difficult language to write. It has a lot of complexity and requires a deep understanding of object-oriented programming.

Most of Java's complexity comes from the hard problems it solves. That's nice if you were going to have those problems, but overkill if you weren't.

GWT added the complexity of the Web on top of Java. It was also positioned as a way to write code for the Web without needing to worry about browsers or HTML. It produced interfaces that looked clunky and ran slowly. It also led to some bad <a href="https://www.zackgrossbart.com/hackito/antiptrn-gwt/">anti-patterns</a>.

It's possible to write <a href="https://www.spiffyui.org">good applications in GWT</a>, but it takes a lot of work.

Even more distressing are the clear indications that GWT isn't the future. Google's still maintaining it, but the community is dwindling and its dreams of world domination are long gone. Even Google never really used GWT. All of their major products (Search, Gmail, Maps, Calendar, Docs, Google+) are written in JavaScript. Well… sort of JavaScript, but we'll get to that a little later.

I still use GWT professionally, but I question it with every new project. GWT tried to drastically change the JavaScript ecosystem and it's tough to turn an aircraft carrier on a dime.

## CoffeeScript

The <a href="https://coffeescript.org/">CoffeeScript</a> team didn't redefine JavaScript, they just gave it a face-lift. CoffeeScript added new syntax to improve some of the day-to-day difficulties of JavaScript programming without drastically changing the language.

Instead of this:

<pre><code class="language-javascript">$(document).ready(function() {
    alert('Hello World!');
});</code></pre>

CoffeeScript lets you write this:

<pre><code class="language-javascript">$(document).ready -&gt;
    alert 'Hello World!';</code></pre>

The general philosophy is that writing less code means you have fewer bugs. CoffeeScript simplifies the JavaScript syntax by removing the need to declare <code>var</code> and using white-space indenting instead of curly braces.

CoffeeScript is growing fast, <a href="https://www.rubyinside.com/rails-3-1-adopts-coffeescript-jquery-sass-and-controversy-4669.html">loved by Ruby programmers</a> and hated by anyone with a secret crush on curly brackets. CoffeeScript compiles into JavaScript either when the page is run, or ahead of time during a build step.

CoffeeScript makes many syntactic improvements over JavaScript, but it has two main flaws. The first is that you can't debug directly in CoffeeScript. Browsers don't run CoffeeScript natively so you get all errors in compiled JavaScript and have to translate them back to your source code. That means you can't write a CoffeeScript application without a pretty deep understanding of the JavaScript it will produce.

The second major flaw of CoffeeScript is that it's basically just JavaScript with a different syntax. CoffeeScript means writing less code, but it doesn't fix the real problems of JavaScript as a language. It's still the case that I love my CoffeeScript and hate everyone else's.</p>

## Google Closure Tools

Around the same time that CoffeeScript came out, Google made another effort to improve JavaScript with the <a href="https://developers.google.com/closure/">Google Closure Tools</a>. Google tried to make GWT the next dominant Web technology, but it let Closure slip quietly out the door.

Closure includes a templating mechanism and a widget library, but the most interesting parts are the <a href="https://developers.google.com/closure/compiler/">Closure Compiler</a> and the <a href="https://developers.google.com/closure/utilities/">Closure Linter</a>.

The Closure compiler (like the <a href="https://developer.yahoo.com/yui/compressor/">YUI Compressor</a>) takes your JavaScript and squishes it down so it takes less time to download and runs faster in production. The general idea is that you develop in standard JavaScript and compile it for release.

The Closure compiler turns this:

<pre><code class="language-javascript">function sayHello() {
   alert('Hello World!');
}

$(document).ready(function() {
   sayHello();
});</code></pre>

into this:

<pre><code class="language-javascript">$(document).ea(function(){alert("Hello World!")});</code></pre>

The result's tough to read, but it runs a lot faster.

The Closure compiler supports two major modes: simple and advanced. Simple mode takes any JavaScript and compresses it by removing comments and white space, substituting variable names and making other safe changes. Simple mode has a very low chance of breaking your JavaScript, and it can find some issues when it compiles.

<a href="https://developers.google.com/closure/compiler/docs/api-tutorial3">Advanced mode</a> provides much better compression, but there's a pretty good chance it will break your code unless you plan ahead. Advanced requires extra information to tell the compiler what not to remove. The very dynamic nature of JavaScript makes it tough for the compiler to follow every path in your code tree without some help.

The Closure tools also introduce <a href="https://developers.google.com/closure/compiler/docs/js-for-compiler">JSDoc</a> tags, which tell the compiler more about how your code works. In regular JavaScript you might define an object with three states for your application:

<pre><code class="language-javascript">myProject.threeStates = {
    TRUE: 1,
    FALSE: -1,
    MAYBE: 0
};</code></pre>

You know that this is an <a href="https://en.wikipedia.org/wiki/Enumerated_type">enumerated type</a> which constrains a value to one of these three options, but the compiler doesn't know. Neither does that other developer on your team who added a fourth value dynamically. JSDoc lets you specify how this code works:

<pre><code class="language-javascript">/**
 * Enum for my three states.
 * @enum {number}
 */
myProject.threeStates = {
    TRUE: 1,
    FALSE: -1,
    MAYBE: 0
};</code></pre>

By adding this comment you're making it clear that this is an enumeration, that it only contains numbers and that you're defining it as a <a href="https://en.wikipedia.org/wiki/Strong_typing">strong type</a> which you can use elsewhere. Combine this feature with the Closure linter that forces you to write comments like this and you're basically redefining JavaScript. It still looks like JavaScript, but turned into a strongly-typed language.

That's easy to see with the <code>@type</code> annotation:

<pre><code class="language-javascript">/**
 * The name of the user
 * @type {string}
 */
var name = 'Zack';</code></pre>

JSDoc supports other annotations that control everything from what a function returns to who can call it. Add a module loader, and the Closure library addresses a lot of the shortcomings of JavaScript, by turning it into Java.

Closure code looks like Java with clunkier syntax. It's strongly typed, uses a similar packaging mechanism and has a powerful compiler. That's a good and bad thing in all the ways that Java is good and bad.

Google isn't putting much marketing behind the Closure tools, but they're putting a lot of engineering there. All of the major Google products use Closure. <a href="https://highscalability.com/blog/2011/7/12/google-is-built-using-tools-you-can-use-too-closure-java-ser.html">Google+ was built on Closure</a> from the ground up.

The Closure community is growing, but there still aren't many people outside of Google who know it well. Closure also suffers from the need to maintain backward compatibility with JavaScript. The syntax looks clunky and only more advanced JavaScript and object-oriented programmers can write it.

Some people thought the Web needed a brand-new language. So Google continued its frenemy relationship with JavaScript by creating Dart.</p>

## Dart

<a href="https://www.dartlang.org/">Dart</a> totally replaces JavaScript with a language that's strongly-typed, uses interfaces and looks a lot like a simplified Java.

<pre><code class="language-javascript">library hi;

import 'dart:html';

main() {
  query('#status').text = 'Hi, Dart';
}</code></pre>

This simple “Hello World!” example shows packages, imports and methods similar to Java syntax.

Dart can compile into JavaScript, but running it natively in the browser gets you better performance and debugging. Google controls the Chrome browser and may add native support for Dart there. They already have <a href="https://www.dartlang.org/dartium/">a special version running on Windows</a>. But it isn't all up to Google.

Chrome depends on <a href="https://en.wikipedia.org/wiki/WebKit">WebKit</a>, which also powers Safari from Apple. Webkit is an open source project made up of about one third Google people, one third Apple people and one third other people. The Chrome team would like to change Webkit to support Dart; that would make their lives easier, and also make Safari support Dart. If that happened they could claim two major browsers support it, and pressure the others to start. The Safari team doesn't want the Web to run on a new language owned by Google, so they're adamant about not including Dart.

It looks like <a href="https://news.ycombinator.com/item?id=2982949">none of the other browsers will support Dart</a> either. That leaves you compiling Dart into JavaScript and losing some of the nicer features like integrated debuggers.

Dart has many technical merits; it's eclipsed by larger political problems.

Some very smart Googlers work on Dart and it has some nice features, but it's still an invention of Google and isn't standard. It wasn't developed by a community and there are good reasons for other vendors to distrust it.

The only thing certain about Dart is that its future is unknown. A preview (version 0.1) was recently released but isn't really usable outside of Google. Dart is a language to keep an eye on, but not a real option yet.</p>

## Opa

<a href="https://opalang.org/">Opa</a> is the new kid on the block with a 1.0 release last August. It's a strongly-typed language with a growing community. You write Opa and compile into other languages like JavaScript, but it isn't just client-side. Opa mixes client-side and server-side programming into a single file.

Opa supports client, server and database development with a single language. Using the same code base, it compiles into JavaScript, native executables and SQL code. They recently added support for non-relational databases like <a href="https://www.mongodb.org/">MongoDB</a> as well.

Unlike Dart, Opa draws heavily on functional programming languages like <a href="https://en.wikipedia.org/wiki/Erlang_(programming_language)">Erlang</a>. That makes it appeal to nerds, but the entry bar is pretty high. Opa lacks the simple syntax of CoffeeScript, and you can't really teach yourself Opa without a strong background in other programming languages.

Though the bar is high, Opa rewards your learning investment by giving you a single environment where you don't have to switch languages between client and server. It hasn't grown much beyond samples and small websites, but it's gaining ground.</p>

## What Should I Do?

The JavaScript problem is everyone's problem; there are no good answers. It's possible to write good JavaScript that scales to large projects, but that takes constant attention and the right culture.

There are a few other options for generating JavaScript (for example, <a href="https://clojure.org/">Clojure</a> compiles into JavaScript), but they're still small projects without much real-world use.

Google writes most of their client-side code with the Closure tools and they're starting to adopt more Dart. Other large websites like Twitter use JavaScript combined with other technologies like Ruby On Rails. Big open source projects like WordPress mostly stick with straight JavaScript and jQuery. Facebook uses a combination of all of them. Microsoft combines jQuery with .Net and some other server-side technologies which interact with JavaScript. They've also released a new static-typed JavaScript variant called <a href="https://www.typescriptlang.org/">TypeScript</a>.

That just scratches the surface. The CoffeeScript project maintains a comprehensive list of <a href="https://github.com/jashkenas/coffee-script/wiki/List-of-languages-that-compile-to-JS">languages that compile into JavaScript</a>.

If your project is small, then just write JavaScript. jQuery is very well done; so are many other JavaScript libraries. Keep your project small and the problems stay small.

But the line between small and large is blurry. Small projects get bigger with time, and you can get into big trouble writing large JavaScript applications without a lot of process to keep you out of the <a href="https://shop.oreilly.com/product/9780596517748.do">bad parts</a>. The other options are either has-beens or aren't-yets.

A big part of this problem is the difficulty of finding a single language that keeps everyone happy. Small websites want something simple that makes it easy to get started and produce an app quickly. Large projects want the structure to keep the code base maintainable for years. The two goals are at odds and no language has ever satisfied both parties. That's why <a href="https://en.wikipedia.org/wiki/Visual_Basic">Visual Basic</a> and <a href="https://en.wikipedia.org/wiki/C%2B%2B">C++</a> are both so popular.

There's also no reason to choose just one. GWT combines well with regular JavaScript, and you can use the Closure Compiler simple optimizations with any JavaScript project.

JavaScript will never be the best language for all applications, but browsers won't support another one anytime soon. The key to using JavaScript well is to understand its limitations and know when not to use it. JavaScript is easy for small projects; you need planning, care and help from other libraries to work on larger ones.

<em>Image on front page created by <a href="https://www.flickr.com/photos/7162499@N02/3260095534/">Ruiwen Chua</a>.</em>

{{< signature "cp" >}}


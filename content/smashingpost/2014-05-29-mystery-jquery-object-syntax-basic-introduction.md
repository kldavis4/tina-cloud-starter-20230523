---
title: 'The Mystery Of The jQuery Object: A Basic Introduction'
slug: mystery-jquery-object-syntax-basic-introduction
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9774c33e-a006-4308-8736-4049a25a2247/download-jquery-option-opt.png
date: 2014-05-29T21:19:12.000Z
author: paul-tero
summary: >-
  This article is a beginners’ guide to JavaScript syntax and how it is used by jQuery. jQuery is just a JavaScript library that has a special-looking function, `$`, and that encourages the use of <strong>shorthand objects</strong>, <strong>anonymous functions</strong> and <strong>method chaining</strong>. jQuery is not alone &mdash; libraries like <a href="https://yuilibrary.com/">YUI</a> (Yahoo User Interface) do similar things.
description: >-
  This article is a beginners’ guide to JavaScript syntax and how it is used by jQuery. jQuery is just a JavaScript library that has a special-looking function, `$`, and that encourages the use of <strong>shorthand objects</strong>, <strong>anonymous functions</strong> and <strong>method chaining</strong>. jQuery is not alone &mdash; libraries like <a href="https://yuilibrary.com/">YUI</a> (Yahoo User Interface) do similar things.
categories:
  - Coding
  - JavaScript
  - jQuery
---

Have you ever come across a bit of JavaScript like `$(".cta").click(function(){})` and thought, “What the $('#x') is that” If it looks like gibberish to you, then please read on. If you think that snippet of code couldn’t possibly be real, then please browse some <a href="https://learn.jquery.com/about-jquery/how-jquery-works/">jQuery examples</a>. They are full of such constructions.

This article covers the key concepts that underly such intimidating fragments of code, but we’ll start with a longer example, based on a simple example of animating a square. You are probably not required to do this every day, but it makes for a concise and tidy demonstration:

<pre><code class="language-javascript">$(document).ready(function(){
	$("button").click(function(){
		$("div").animate({height:"toggle"}).append("hi");
	});
});
</code></pre>

We’ll go through every word and feature of the code above, along with <strong>a detailed look at JavaScript functions, the jQuery object and event-driven programming</strong>. By the end, you will hopefully no longer feel anxious in the face of such inscrutable code.

## What Is `$`?

At first glance, `$` looks like some special, complex JavaScript functionality. It’s not. The dollar symbol has no special significance in JavaScript. In fact, `$` is just a function. It is an alternative name for the <a href="https://api.jquery.com/jquery/">`jQuery` function</a>.

And the `jQuery` function is the raison d’être of the very popular <a href="https://jquery.com/">jQuery library</a>. jQuery is a compact JavaScript library that irons out many of the annoying differences between browser manufacturers and provides many useful features for manipulating and animating parts of Web pages. You can include the `jQuery` function (i.e. `$`) in your page by referencing a copy of the library:

<pre><code class="language-markup">&lt;script src="https://code.jquery.com/jquery-1.11.1.min.js"&gt;&lt;/script&gt;
</code></pre>

Alternatively, you can download your own copy <a href="https://jquery.com/download/">from jQuery’s website</a>:

{{< rimg href="https://jquery.com/download/" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9774c33e-a006-4308-8736-4049a25a2247/download-jquery-option-opt.png" width="500" sizes="100vw" caption="Downloading jQuery is very easy." alt="Downloading jQuery is very easy" >}}

The `jQuery` function usually takes a single argument, either a <strong>selector</strong> or a JavaScript reference to something on the page, such as `document`.

A selector is just a piece of CSS, the part before the `{…}`. So, `$("div")` is the same as `jQuery("div")` and behaves very roughly like the following CSS by selecting all of the `&lt;div&gt;` tags on the current page:

<pre><code class="language-markup">&lt;style&gt;
	div {…}
&lt;/style&gt;
</code></pre>

At the beginning of our example, `$(document)` passes the JavaScript variable `document` into the `jQuery` function. The `document` variable is set automatically by the browser. It refers to the top of the <a href="https://developer.mozilla.org/en/docs/Web/API/Document">document object model</a> (DOM). The DOM is the browser’s own analysis of all of the HTML in the page, upon which the functionality of jQuery is built. For example, jQuery’s `$("div")` does roughly the same thing as `document.getElementsByTagName("div")`.

{{% feature-panel %}}

### Key Takeaway

Remember that `$` is just a function, an alternative and handier name for the `jQuery` function.

## The Dot

The `.` that comes after `$(document)` signifies a wealth of functionality. The dot is used with JavaScript objects. At its simplest, a JavaScript object is a collection of properties. For example:

<pre><code class="language-javascript">var digger = new Object();
digger.species = "gerbil";
digger.name = "Digger";
digger.color = "white";
</code></pre>

{{< rimg breakout="true" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3e32acf7-aefa-481d-a7d3-a2bc82255d4f/digger-500px.jpg" width="500" sizes="100vw" caption="The inspiration for this JavaScript object." alt="The inspiration for this JavaScript object" >}}

In this example, the variable `digger` is an object, and we have assigned it three subvariables: `species`, `name` and `color`. In object-oriented jargon, these are known as <strong>member variables</strong>. All of the above can be written more concisely as this:

<pre><code class="language-javascript">var digger = {species:"gerbil", name:"Digger", color:"white"};
</code></pre>

You can also assign functions as properties of an object. Gerbils are generally very quiet rodents, but occasionally they make a high-pitched meeping sort of noise. In JavaScript, that might look like this:

<pre><code class="language-javascript">function meepMeep(){
	alert("meep meep");
}
</code></pre>

In JavaScript, the boundaries between variables, functions and objects are quite blurred. So, a function can easily be assigned to a (member) variable:

<pre><code class="language-javascript">digger.speak = meepMeep;
</code></pre>

You can now call this function to make the gerbil speak:

<pre><code class="language-javascript">digger.speak();
</code></pre>

In object-oriented parlance, this is now a <strong>member function</strong>, or a <strong>method</strong>. Methods may refer to other methods and member variables within the same object. Imagine that Digger has learned to speak English, which is quite remarkable for a gerbil:

<pre><code class="language-javascript">function myNameIs(){
	alert("Meep! I am a " + this.species);
}
//assign the function
digger.sayMyName = myNameIs;
//call the function
digger.sayMyName();
</code></pre>

In the `myNameIs` function, the special variable `this` refers to the containing object, and `this.species` is the same as `digger.species` and has the value `gerbil`. If you tried to call `myNameIs()` by itself, without the object, then `this` would refer to the JavaScript `window` object and `this.species` would be `window.species`, which is undefined. The page would alert “Meep! I am a undefined.”

Objects can also be used as the return values for functions. This is a nice function that I use all of the time:

<pre><code class="language-javascript">function giveMeTheGerbil(){
	return digger;
}
</code></pre>

This will return a reference to the (global) variable or object `digger`, which you can then treat in exactly the same way as the original `digger`:

<pre><code class="language-javascript">var digger2 = giveMeTheGerbil();
//alerts "Meep! I am a gerbil"
digger2.sayMyName();
</code></pre>

However, you can skip the intermediary variable and just call `sayMyName` directly on the returned value of `giveMeTheGerbil`:

<pre><code class="language-javascript">giveMeTheGerbil().sayMyName();
</code></pre>

Stripped of the inner code, this is the same programmatic structure as in the first line of our original example:

<pre><code class="language-javascript">$(document).ready(…);
</code></pre>

The next section describes what `ready` actually does.

### Key Points

The shorthand object notation looks like `{name:"Digger", species:"gerbil"}`.

The keyword `this` is used in a function attached to an object (a method) and refers to the containing object.

{{% ad-panel-leaderboard %}}

## Anonymous Functions

In JavaScript, there are several ways to create functions. The following is the classic way (a <a href="https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/">function declaration</a>), which should be familiar to anyone who has done some programming:

<pre><code class="language-javascript">function meepMeep(){
	alert("meep meep");
}
</code></pre>

We’ve seen above that functions can be assigned to variables. We created the `meepMeep` function and assigned it to `digger.speak`. In fact, functions may be created anonymously (called a function expression), without any name at all, and then assigned to a variable:

<pre><code class="language-javascript">var meepMeep = function(){
	alert("meep meep");
};
</code></pre>

In JavaScript, functions may be assigned to variables and passed around just like any other variable. Consider this rather useless function:

<pre><code class="language-javascript">function runMe(f){
	f();
}
</code></pre>

It has one argument, called `f`. `runMe` treats that argument like a function and runs it. So, you could call this:

<pre><code class="language-javascript">runMe(meepMeep);
</code></pre>

This would simply run the `meepMeep` function. It gets more interesting when you don’t even bother to officially name `meepMeep` at all. You could simply create it when needed and pass it immediately into `runMe`:

<pre><code class="language-javascript">runMe(function(){
	alert("meep meep");
});
</code></pre>

In fact, anywhere `meepMeep` can appear, so can its anonymous equivalent. Take this:

<pre><code class="language-javascript">meepMeep();
</code></pre>

Instead of that, you could put an anonymous function in place of `meepMeep`, although wrapping it in an extra set of parentheses is required:

<pre><code class="language-javascript">(function(){
	alert("meep meep");
})();
</code></pre>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d7e8d129-3b64-43fa-b217-51146f578226/meepmeep-opt.png" width="500" sizes="100vw" caption="This is the result of all of the above ways of calling `meepMeep()`." alt="This is the result of all of the above ways of calling meepMeep()" >}}

This technique is often used to provide variable scoping in JavaScript. Can you follow what this code will do?

<pre><code class="language-javascript">var x=3;
(function(){
	var x=4; console.log("x is " + x);
})();
console.log ("x is " + x);
</code></pre>

The `var` keyword within the function is important here. It declares a variable within a function. The anonymous function here defines its own local variable, `x`, assigns it the value `4` and then outputs it. Because of the `var` keyword, the function’s `x` remains completely separate from the `var x=3` on the previous line. Therefore, this code will output `x is 4` and then `x is 3`.

Because our gerbil is no longer doing any high-pitched squeaking, the code above uses `<a href="https://developer.mozilla.org/en-US/docs/Web/API/console.log">console.log</a>`, rather than `alert`, to output its result. The `console.log` is available in modern browsers (in other words, not in old Internet Explorers) and shows its output unobtrusively in the browser’s <a href="https://webmasters.stackexchange.com/questions/8525/how-to-open-the-javascript-console-in-different-browsers">error, Web or JavaScript console</a>.

Anonymous functions are the next piece of the puzzle. jQuery’s `<a href="https://api.jquery.com/ready/">ready</a>` method is like a time-delayed version of the `runMe` function above. The `ready` method waits until the DOM has fully loaded and then runs the provided function. So, when the `document` is finally `ready`, the following anonymous function will run:

<pre><code class="language-javascript">function(){
	$("button").click (…)
}
</code></pre>

The `$(document).ready(…)` is a common way for programmers to execute some JavaScript only after all of the HTML document has been processed.

### Key Takeaway

Anonymous functions are functions without a name, like `function(){alert(1);}`. They can be assigned to variables, passed into other functions or run immediately to provide scoping.

## Method Chaining

Before delving further into the sample code, we need to review one more concept that often occurs in JavaScript. <a href="https://en.wikipedia.org/wiki/Method_chaining">Method chaining</a> refers to running several functions in a row. This is really just an extension of the `giveMeTheGerbil()` example above:

<pre><code class="language-javascript">giveMeTheGerbil().sayMyName();
</code></pre>

Let’s redefine the gerbil-related functions to return a reference to themselves.

<pre><code class="language-javascript">digger.speak = function(){
	alert("meep meep"); return this;
}
digger.sayMyName = function(){
	alert("Meep! I am a " + this.species); return this;
}
</code></pre>

These two functions now do something to `digger` and then return `digger`. Not much different, but the addition allows us to chain the functions together:

<pre><code class="language-javascript">giveMeTheGerbil().speak().sayMyName().speak();
</code></pre>

This line of code will first run `giveMeTheGerbil`, returning a reference to the `digger` object. Now, it essentially becomes equivalent to this:

<pre><code class="language-javascript">digger.speak().sayMyName().speak();
</code></pre>

Next, the `speak` method of the `digger` object runs and alerts `meep meep`. This also returns a reference to `digger`, and then the code becomes this:

<pre><code class="language-javascript">digger.sayMyName().speak();
</code></pre>

After that, `sayMyName` runs and again returns a reference to `digger`, etc. It will cause three alerts: `meep meep`, `Meep! I am a gerbil`, `meep meep`.

This sort of chaining often happens in JavaScript. You might see it with `<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String">string</a>` objects:

<pre><code class="language-javascript">var s = "I have a dagger."; 
console.log(s.substring(9, 15).replace("a", "i").toUpperCase());
</code></pre>

The code above starts with the full string `s`, extracts a substring, replaces the letter “a” with “i,” changes the resulting word to uppercase and returns the resulting string, which is shown in the console log.

Of course, chaining happens all over the place in jQuery and appears in our example:

<pre><code class="language-javascript">$("div").animate({height:"toggle"}).append("hi");
</code></pre>

The `$("div")` looks up all `&lt;div&gt;` elements in the page and returns them as part of a jQuery object. It runs the `animate` method on the jQuery object and then runs `append`, each time returning and operating on a jQuery object.

These chains can get long. Below is a <a href="https://forum.jquery.com/topic/jquery-my-longest-chain-so-far">particularly long jQuery chain</a>, proudly posted several years ago:

<img loading="lazy" decoding="async" title="A very long jQuery chain." src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e8252b6-b279-4f49-8040-c587a40f55f5/longest-chain-opt.png" alt="A very long jQuery chain." width="500" /><br>
<em>A very long jQuery chain.</em>

Generally speaking, long chains like this are hard to debug and maintain. So, avoiding really long ones is usually a good idea, but they can be useful in miniature.

### Key Takeaway

Functions belonging to objects (i.e. methods) that return references to themselves may be chained together, allowing you to execute a lot of code without storing the intermediate results.

## The jQuery Object

Our example uses several jQuery methods: `ready`, `click`, `animate` and `append`. These are all functions attached to the jQuery object, similar to how `speak` and `myNameIs` are functions attached to the `digger` object and to how `substr`, `replace` and `toUpperCase` go with strings.

These functions are all methods of the jQuery object, and they all return a jQuery object. Internally, though, the jQuery object is far more sophisticated than `digger` or a `string` could ever hope to be.

As mentioned earlier, the barriers between concepts can get blurry in JavaScript. The jQuery object behaves like an object and an array. You treat it like an object when you chain, but you can also treat it like an array:

<pre><code class="language-javascript">var mydivs = $("div");
for (var i = 0; i &lt; mydivs.length; i++) {console.log(mydivs[i].innerHTML);}
</code></pre>

In this example, `$("div")` looks up all `&lt;div&gt;` elements in the page and stores the resulting jQuery object in the `mydivs` variable. The code loops through the jQuery object as if it were an array of nodes (actually, a `<a href="https://developer.mozilla.org/en-US/docs/Web/API/NodeList">NodeList</a>`) in the DOM. These nodes are also <a href="https://developer.mozilla.org/en-US/docs/Web/API/Element">objects</a> with properties of their own, such as `outerHTML` and `innerHTML`.

Achieving the same result by turning these nodes back into jQuery objects and then calling the jQuery method `html` is also possible. To do this, pass them into `$`, which turns pretty much anything into a jQuery object:

<pre><code class="language-javascript">var mydivs = $("div");
for (var i = 0; i &lt; mydivs.length; i++) {console.log($(mydivs[i]).html());}
</code></pre>

Both of these will output the HTML contents of each `&lt;div&gt;` on the page.

Note that when you run a piece of jQuery such as `$("div").animate(…).append(…);`, the animation happens on all of the `&lt;div&gt;` elements in the jQuery object, and they are all passed to the next function in the chain as part of the jQuery object. (This is true of most but not all jQuery functions. <a href="https://api.jquery.com/">See jQuery’s documentation</a>.)

### Key Takeaway

The jQuery function `$` and many of the jQuery methods like `click` and `animate` return a jQuery object, which is part object and part array. The array-like part contains references to nodes in the DOM.

{{% ad-panel-leaderboard %}}

## Putting It All Together

We can now look at the example as a whole. The `$(document)` returns a jQuery object referring to the page itself. The `.ready(…)` is passed a function that runs when the page has finished parsing and the DOM is fully available:

<pre><code class="language-javascript">function(){
	$("button").click(…);
}
</code></pre>

This function uses the main `jQuery` function to look up all `&lt;button&gt;` elements in the page. It returns a jQuery object that has a `click` method. The `click` method is passed another anonymous function:

<pre><code class="language-javascript">function(){
	$("div").animate ({height:"toggle"}).append("hi");
}
</code></pre>

This function looks up all `&lt;div&gt;` elements, returns a jQuery object, and first calls its `animate` method. The argument to jQuery’s `animate` method is a list of properties to animate, passed in as the shorthand object `{height:"toggle"}`. This tells jQuery to toggle the height of all `&lt;div&gt;` elements in the page. The first time, it will reduce their heights to zero. The next time, it will animate them back up to their original heights.

The `animate` method also returns a jQuery object. This is chained to the `append` method that adds the “hi” string to every `&lt;div&gt;` each time the button is pressed. Paste this into an HTML page or <a href="https://jsbin.com/rikemiho/1">view it on JS Bin</a> to see the whole thing in action:

<pre><code class="language-markup">&lt;button&gt;Click me&lt;/button&gt;
&lt;div style="width:100px;height:100px;background:green;"&gt;&lt;/div&gt;
&lt;script src="https://code.jquery.com/jquery-1.8.3.js"&gt;&lt;/script&gt;
&lt;script&gt;
$(document).ready(function(){
	$("button").click(function(){
		$("div").animate({height:"toggle"}).append("hi");
	});
});
&lt;/script&gt;
</code></pre>

{{< rimg src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9844bb3f-0ffa-405c-a939-72b55d3245ab/expanding-div-opt.png" width="500" sizes="100vw" caption="How the page looks after a few clicks." alt="How the page looks after a few clicks" >}}

Every time the `&lt;button&gt;` is clicked, the green `&lt;div&gt;` collapses or expands and gets an extra “hi” added to it. This snippet of code won’t get you out of any life-threatening situations, but it is good to fully understand.

## Event-Driven Headaches

This snippet looks innocent enough:

<pre><code class="language-javascript">//set h to 200
var h = 200; 
$(document).ready(function(){
	$("button").click(function(){
		//animate up to h, 200 pixels high
		$("div").animate({height:h});
	});
});
</code></pre>

You would expect the `&lt;div&gt;` to expand to 200 pixels. But a lot could happen in between the variable `h` being assigned the value of `200` and the animation actually running. In a complex jQuery application, the variable name `h` might get reused, or some other part of your application might change the value. And you will stare intently at those few lines of code wondering why on Earth your box animates to only 50 pixels high, instead of 200. It’s because somewhere else in your code, you might have an unobtrusive `for (h=1; h&lt;50; h++) {…}` changing the value of `h`.

To be fair, this issue is not caused by jQuery or by anonymous functions, but it is a hazard of event-driven programming in general. The lines above run at three different times: when they are first processed (`$(document).ready(…)`), when the document loads (`$("button").click(…)`) and when the button is clicked (`$("div").animate(…)`).

Server-side code written in languages such as PHP runs sequentially and in order, from beginning to end, outputting HTML to make a Web page and then finishing. JavaScript can do this, too, but it is most powerful when attached to events, such as button clicks. This is <a href="https://en.wikipedia.org/wiki/Event-driven_programming">event-driven programming</a>, and it’s not only JavaScript. The programming behind smartphone apps is also largely event-driven, with Objective-C or Java or C++ responding to touchscreen events on your Apple, Android or Windows phone.

If the code above were translated into Java and run on an Android phone, then the reference to `h` in the innermost function would cause an error. This is because `h` has not been declared as a global (or `static` in Java) variable, and so the inner code has no idea what its value should be. While that wouldn’t change the issue, it would at least force you to think more clearly about how to use variables.

One quick way to avoid headaches like this is to scope your variables. This example can be fixed by declaring the variable `var h` in the first anonymous function. Now, that `h` will take precedence over any other global `h`:

<pre><code class="language-javascript">$(document).ready (function(){
	//set h to 200
	var h = 200;
	$("button").click (function(){
		//animate up to h, 200 pixels high
		$("div").animate ({height:h});
	});
});
</code></pre>

If you must use a global configuration variable, then another technique is to name and group the variables well. And clearly commenting your code is always recommended:

<pre><code class="language-javascript">//properties of the animation
var animationConfig = {upToHeight:200};
//when document is loaded
$(document).ready(function(){
	//when any &lt;button&gt; element is clicked
	$("button").click(function(){
		//change the height of all &lt;div&gt;s
		$("div").animate({height:animationConfig.upToHeight});
	});
});
</code></pre>

## Conclusion

This article is a beginners’ guide to JavaScript syntax and how it is used by jQuery. jQuery is just a JavaScript library that has a special-looking function, `$`, and that encourages the use of <strong>shorthand objects</strong>, <strong>anonymous functions</strong> and <strong>method chaining</strong>. jQuery is not alone &mdash; libraries like <a href="https://yuilibrary.com/">YUI</a> (Yahoo User Interface) do similar things.

You can now look a complex piece of jQuery directly in the face with no doubt or uncertainty in your mind. You know what it does. Due to the complexities of event-driven programming, you might not be sure when, but you do know how.

### Further Reading on SmashingMag

*   [Useful jQuery Function Demos For Your Projects](https://www.smashingmagazine.com/2012/05/50-jquery-function-demos-for-aspiring-web-developers/)
*   [Developing Dependency Awareness](https://www.smashingmagazine.com/2016/05/developing-dependency-awareness/)
*   [Scaling Down The BEM Methodology For Small Projects](https://www.smashingmagazine.com/2014/07/bem-methodology-for-small-projects/)

{{< signature "al, ml, il" >}}

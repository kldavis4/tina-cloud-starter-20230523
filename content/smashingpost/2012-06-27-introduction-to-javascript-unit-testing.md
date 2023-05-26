---
title: Introduction To JavaScript Unit Testing
slug: introduction-to-javascript-unit-testing
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/577b793a-2d4b-4424-b7e3-6df179ee36c8/prettydate-tests-frontpage1.png
date: 2012-06-27T07:31:31.000Z
author: joern-zaefferer
description: >-
  You probably know that testing is good, but the first hurdle to overcome when trying to write unit tests for client-side code is the lack of any actual units; JavaScript code is written for each page of a website or each module of an application and is closely intermixed with back-end logic and related HTML. In the worst case, the code is completely mixed with HTML, as inline events handlers.
categories:
  - Coding
  - JavaScript
  - Testing
---
You probably know that testing is good, but the first hurdle to overcome when trying to write unit tests for client-side code is the lack of any actual units; JavaScript code is written for each page of a website or each module of an application and is closely intermixed with back-end logic and related HTML. In the worst case, the code is completely mixed with HTML, as inline events handlers.

This is likely the case when no JavaScript library for some DOM abstraction is being used; writing inline event handlers is much easier than using the DOM APIs to bind those events. More and more developers are picking up a library such as jQuery to handle the DOM abstraction, allowing them to move those inline events to distinct scripts, either on the same page or even in a separate JavaScript file. However, putting the code into separate files doesn’t mean that it is ready to be tested as a unit.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Writing Fast, Memory-Efficient JavaScript</span>](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)
*   [JavaScript Mistakes To Avoid With A Static Code Analyzer](https://www.smashingmagazine.com/2015/02/avoid-javascript-mistakes-with-static-code-analyzer/)
*   [Analyzing Network Characteristics Using JavaScript And DOM](https://www.smashingmagazine.com/2011/11/analyzing-network-characteristics-using-javascript-and-the-dom-part-1/)
*   [Find The Right JavaScript Solution With A 7-Step Test](https://www.smashingmagazine.com/2010/01/find-the-right-javascript-solution-with-a-7-step-test/)

What is a unit anyway? In the best case, it is a pure function that you can deal with in some way — a function that always gives you the same result for a given input. This makes unit testing pretty easy, but most of the time you need to deal with side effects, which here means DOM manipulations. It’s still useful to figure out which units we can structure our code into and to build unit tests accordingly.

{{% feature-panel %}}

## Building Unit Tests

With that in mind, we can obviously say that starting with unit testing is much easier when starting something from scratch. But that’s not what this article is about. This article is to help you with the harder problem: extracting existing code and testing the important parts, potentially uncovering and fixing bugs in the code.

The process of extracting code and putting it into a different form, without modifying its current behavior, is called refactoring. Refactoring is an excellent method of improving the code design of a program; and because any change could actually modify the behaviour of the program, it is safest to do when unit tests are in place.

This chicken-and-egg problem means that to add tests to existing code, you have to take the risk of breaking things. So, until you have solid coverage with unit tests, you need to continue manually testing to minimize that risk.

That should be enough theory for now. Let’s look at a practical example, testing some JavaScript code that is currently mixed in with and connected to a page. The code looks for links with <code>title</code> attributes, using those titles to display when something was posted, as a relative time value, like “5 days ago”:

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;
    &lt;title&gt;Mangled date examples&lt;/title&gt;
    &lt;script&gt;
    function prettyDate(time){
        var date = new Date(time || ""),
            diff = ((new Date().getTime() - date.getTime()) / 1000),
            day_diff = Math.floor(diff / 86400);

        if (isNaN(day_diff) || day_diff &lt; 0 || day_diff &gt;= 31) {
            return;
        }

        return day_diff == 0 &amp;&amp; (
                diff &lt; 60 &amp;&amp; "just now" ||
                diff &lt; 120 &amp;&amp; "1 minute ago" ||
                diff &lt; 3600 &amp;&amp; Math.floor( diff / 60 ) + " minutes ago" ||
                diff &lt; 7200 &amp;&amp; "1 hour ago" ||
                diff &lt; 86400 &amp;&amp; Math.floor( diff / 3600 ) + " hours ago") ||
            day_diff == 1 &amp;&amp; "Yesterday" ||
            day_diff &lt; 7 &amp;&amp; day_diff + " days ago" ||
            day_diff &lt; 31 &amp;&amp; Math.ceil( day_diff / 7 ) + " weeks ago";
    }
    window.onload = function(){
        var links = document.getElementsByTagName("a");
        for (var i = 0; i &lt; links.length; i++) {
            if (links[i].title) {
                var date = prettyDate(links[i].title);
                if (date) {
                    links[i].innerHTML = date;
                }
            }
        }
    };
    &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;ul&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;a href="/2008/01/blah/57/" title="2008-01-28T20:24:17Z"&gt;January 28th, 2008&lt;/a&gt;
        by &lt;a href="/john/"&gt;John Resig&lt;/a&gt;
    &lt;/small&gt;
&lt;/li&gt;
&lt;!-- more list items --&gt;
&lt;/ul&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

If you ran that example, you’d see a problem: none of the dates get replaced. The code works, though. It loops through all anchors on the page and checks for a <code>title</code> property on each. If there is one, it passes it to the <code>prettyDate</code> function. If <code>prettyDate</code> returns a result, it updates the <code>innerHTML</code> of the link with the result.</p>

## Make Things Testable

The problem is that for any date older than 31 days, <code>prettyDate</code> just returns undefined (implicitly, with a single <code>return</code> statement), leaving the text of the anchor as is. So, to see what’s supposed to happen, we can hardcode a “current” date:

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;
    &lt;title&gt;Mangled date examples&lt;/title&gt;
    &lt;script&gt;
    function prettyDate(now, time){
        var date = new Date(time || ""),
            diff = (((new Date(now)).getTime() - date.getTime()) / 1000),
            day_diff = Math.floor(diff / 86400);

        if (isNaN(day_diff) || day_diff &lt; 0 || day_diff &gt;= 31) {
            return;
        }

        return day_diff == 0 &amp;&amp; (
                diff &lt; 60 &amp;&amp; "just now" ||
                diff &lt; 120 &amp;&amp; "1 minute ago" ||
                diff &lt; 3600 &amp;&amp; Math.floor( diff / 60 ) + " minutes ago" ||
                diff &lt; 7200 &amp;&amp; "1 hour ago" ||
                diff &lt; 86400 &amp;&amp; Math.floor( diff / 3600 ) + " hours ago") ||
            day_diff == 1 &amp;&amp; "Yesterday" ||
            day_diff &lt; 7 &amp;&amp; day_diff + " days ago" ||
            day_diff &lt; 31 &amp;&amp; Math.ceil( day_diff / 7 ) + " weeks ago";
    }
    window.onload = function(){
        var links = document.getElementsByTagName("a");
        for (var i = 0; i &lt; links.length; i++) {
            if (links[i].title) {
                var date = prettyDate("2008-01-28T22:25:00Z", links[i].title);
                if (date) {
                    links[i].innerHTML = date;
                }
            }
        }
    };
    &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;ul&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;a href="/2008/01/blah/57/" title="2008-01-28T20:24:17Z"&gt;January 28th, 2008&lt;/a&gt;
        by &lt;a href="/john/"&gt;John Resig&lt;/a&gt;
    &lt;/small&gt;
&lt;/li&gt;
&lt;!-- more list items --&gt;
&lt;/ul&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

*   [Run this example.](https://smashingmagazine.com/provide/introduction-to-js-unit-testing-code/1-mangled.html)

Now, the links should say “2 hours ago,” “Yesterday” and so on. That’s something, but still not an actual testable unit. So, without changing the code further, all we can do is try to test the resulting DOM changes. Even if that did work, any small change to the markup would likely break the test, resulting in a really bad cost-benefit ratio for a test like that.</p>

## Refactoring, Stage 0

Instead, let’s refactor the code just enough to have something that we can unit test.

We need to make two changes for this to happen: pass the current date to the <code>prettyDate</code> function as an argument, instead of having it just use <code>new Date</code>, and extract the function to a separate file so that we can include the code on a separate page for unit tests.

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;
    &lt;title&gt;Refactored date examples&lt;/title&gt;
    &lt;script src="prettydate.js"&gt;&lt;/script&gt;
    &lt;script&gt;
    window.onload = function() {
        var links = document.getElementsByTagName("a");
        for ( var i = 0; i &lt; links.length; i++ ) {
            if (links[i].title) {
                var date = prettyDate("2008-01-28T22:25:00Z", links[i].title);
                if (date) {
                    links[i].innerHTML = date;
                }
            }
        }
    };
    &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;ul&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;a href="/2008/01/blah/57/" title="2008-01-28T20:24:17Z"&gt;January 28th, 2008&lt;/a&gt;
        by &lt;a href="/john/"&gt;John Resig&lt;/a&gt;
    &lt;/small&gt;
&lt;/li&gt;
&lt;!-- more list items --&gt;
&lt;/ul&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

&nbsp;

Here’s the contents of <code>prettydate.js</code>:

<pre><code class="language-javascript">function prettyDate(now, time){
    var date = new Date(time || ""),
        diff = (((new Date(now)).getTime() - date.getTime()) / 1000),
        day_diff = Math.floor(diff / 86400);

    if (isNaN(day_diff) || day_diff &lt; 0 || day_diff &gt;= 31) {
        return;
    }

    return day_diff == 0 &amp;&amp; (
            diff &lt; 60 &amp;&amp; "just now" ||
            diff &lt; 120 &amp;&amp; "1 minute ago" ||
            diff &lt; 3600 &amp;&amp; Math.floor( diff / 60 ) + " minutes ago" ||
            diff &lt; 7200 &amp;&amp; "1 hour ago" ||
            diff &lt; 86400 &amp;&amp; Math.floor( diff / 3600 ) + " hours ago") ||
        day_diff == 1 &amp;&amp; "Yesterday" ||
        day_diff &lt; 7 &amp;&amp; day_diff + " days ago" ||
        day_diff &lt; 31 &amp;&amp; Math.ceil( day_diff / 7 ) + " weeks ago";
}</code></pre>

*   [Run this example.](https://smashingmagazine.com/provide/introduction-to-js-unit-testing-code/2-getting-somewhere.html)

Now that we have something to test, let’s write some actual unit tests:

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;
    &lt;title&gt;Refactored date examples&lt;/title&gt;
    &lt;script src="prettydate.js"&gt;&lt;/script&gt;
    &lt;script&gt;
    function test(then, expected) {
        results.total++;
        var result = prettyDate("2008-01-28T22:25:00Z", then);
        if (result !== expected) {
            results.bad++;
            console.log("Expected " + expected + ", but was " + result);
        }
    }
    var results = {
        total: 0,
        bad: 0
    };
    test("2008/01/28 22:24:30", "just now");
    test("2008/01/28 22:23:30", "1 minute ago");
    test("2008/01/28 21:23:30", "1 hour ago");
    test("2008/01/27 22:23:30", "Yesterday");
    test("2008/01/26 22:23:30", "2 days ago");
    test("2007/01/26 22:23:30", undefined);
    console.log("Of " + results.total + " tests, " + results.bad + " failed, "
        + (results.total - results.bad) + " passed.");
    &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

*   [Run this example.](https://smashingmagazine.com/provide/introduction-to-js-unit-testing-code/3-first-test.html) (Make sure to enable a console such as Firebug or Chrome’s Web Inspector.)

This will create an ad-hoc testing framework, using only the console for output. It has no dependencies to the DOM at all, so you could just as well run it in a non-browser JavaScript environment, such as Node.js or Rhino, by extracting the code in the <code>script</code> tag to its own file.

If a test fails, it will output the expected and actual result for that test. In the end, it will output a test summary with the total, failed and passed number of tests.

If all tests have passed, like they should here, you would see the following in the console:
<blockquote>Of 6 tests, 0 failed, 6 passed.</blockquote>

To see what a failed assertion looks like, we can change something to break it:
<blockquote>Expected 2 day ago, but was 2 days ago.

Of 6 tests, 1 failed, 5 passed.</blockquote>

While this ad-hoc approach is interesting as a proof of concept (you really can write a test runner in just a few lines of code), it’s much more practical to use an existing unit testing framework that provides better output and more infrastructure for writing and organizing tests.

## The QUnit JavaScript Test Suite

The choice of framework is mostly a matter of taste. For the rest of this article, we’ll use <a href="https://qunitjs.com">QUnit</a> (pronounced “q-unit”), because its style of describing tests is close to that of our ad-hoc test framework.

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;
    &lt;title&gt;Refactored date examples&lt;/title&gt;

    &lt;link rel="stylesheet" href="qunit.css" /&gt;
    &lt;script src="qunit.js"&gt;&lt;/script&gt;
    &lt;script src="prettydate.js"&gt;&lt;/script&gt;

    &lt;script&gt;
    test("prettydate basics", function() {
        var now = "2008/01/28 22:25:00";
        equal(prettyDate(now, "2008/01/28 22:24:30"), "just now");
        equal(prettyDate(now, "2008/01/28 22:23:30"), "1 minute ago");
        equal(prettyDate(now, "2008/01/28 21:23:30"), "1 hour ago");
        equal(prettyDate(now, "2008/01/27 22:23:30"), "Yesterday");
        equal(prettyDate(now, "2008/01/26 22:23:30"), "2 days ago");
        equal(prettyDate(now, "2007/01/26 22:23:30"), undefined);
    });
    &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div id="qunit"&gt;&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

*   [Run this example.](https://smashingmagazine.com/provide/introduction-to-js-unit-testing-code/4-qunit-test.html)

Three sections are worth a closer look here. Along with the usual HTML boilerplate, we have three included files: two files for QUnit (<code>qunit.css</code> and <code>qunit.js</code>) and the previous <code>prettydate.js</code>.

Then, there’s another script block with the actual tests. The <code>test</code> method is called once, passing a string as the first argument (naming the test) and passing a function as the second argument (which will run the actual code for this test). This code then defines the <code>now</code> variable, which gets reused below, then calls the <code>equal</code> method a few times with varying arguments. The <code>equal</code> method is one of several assertions that QUnit provides. The first argument is the result of a call to <code>prettyDate</code>, with the <code>now</code> variable as the first argument and a <code>date</code> string as the second. The second argument to <code>equal</code> is the expected result. If the two arguments to <code>equal</code> are the same value, then the assertion will pass; otherwise, it will fail.

Finally, in the body element is some QUnit-specific markup. These elements are optional. If present, QUnit will use them to output the test results.

The result is this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a56d3e8b-0aba-40ed-9b1a-fe849c55bb69/4a-green.png"><img loading="lazy" decoding="async" class="118914 size-full" title="4a-green" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a56d3e8b-0aba-40ed-9b1a-fe849c55bb69/4a-green.png" alt="javascript unit testing" width="491" height="204" /></a>

With a failed test, the result would look something like this:

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62de4cec-cfdc-4cc3-8cb1-2e4603345705/4b-red.png"><img loading="lazy" decoding="async" class="118915 size-full" title="4b-red" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62de4cec-cfdc-4cc3-8cb1-2e4603345705/4b-red.png" alt="javascript unit testing" width="495" height="454" /></a>

Because the test contains a failing assertion, QUnit doesn’t collapse the results for that test, and we can see immediately what went wrong. Along with the output of the expected and actual values, we get a <code>diff</code> between the two, which can be useful for comparing larger strings. Here, it’s pretty obvious what went wrong.</p>

## Refactoring, Stage 1

The assertions are currently somewhat incomplete because we aren’t yet testing the <code>n weeks ago</code> variant. Before adding it, we should consider refactoring the test code. Currently, we are calling <code>prettyDate</code> for each assertion and passing the <code>now</code> argument. We could easily refactor this into a custom assertion method:

<pre><code class="language-javascript">test("prettydate basics", function() {
    function date(then, expected) {
        equal(prettyDate("2008/01/28 22:25:00", then), expected);
    }
    date("2008/01/28 22:24:30", "just now");
    date("2008/01/28 22:23:30", "1 minute ago");
    date("2008/01/28 21:23:30", "1 hour ago");
    date("2008/01/27 22:23:30", "Yesterday");
    date("2008/01/26 22:23:30", "2 days ago");
    date("2007/01/26 22:23:30", undefined);
});</code></pre>

*   [Run this example.](https://smashingmagazine.com/provide/introduction-to-js-unit-testing-code/5-qunit-test-refactored.html)

Here we’ve extracted the call to <code>prettyDate</code> into the <code>date</code> function, inlining the <code>now</code> variable into the function. We end up with just the relevant data for each assertion, making it easier to read, while the underlying abstraction remains pretty obvious.</p>

## Testing The DOM manipulation

Now that the <code>prettyDate</code> function is tested well enough, let’s shift our focus back to the initial example. Along with the <code>prettyDate</code> function, it also selected some DOM elements and updated them, within the <code>window</code> load event handler. Applying the same principles as before, we should be able to refactor that code and test it. In addition, we’ll introduce a module for these two functions, to avoid cluttering the global namespace and to be able to give these individual functions more meaningful names.

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;
    &lt;title&gt;Refactored date examples&lt;/title&gt;
    &lt;link rel="stylesheet" href="qunit.css" /&gt;
    &lt;script src="qunit.js"&gt;&lt;/script&gt;
    &lt;script src="prettydate2.js"&gt;&lt;/script&gt;
    &lt;script&gt;
    test("prettydate.format", function() {
        function date(then, expected) {
            equal(prettyDate.format("2008/01/28 22:25:00", then), expected);
        }
        date("2008/01/28 22:24:30", "just now");
        date("2008/01/28 22:23:30", "1 minute ago");
        date("2008/01/28 21:23:30", "1 hour ago");
        date("2008/01/27 22:23:30", "Yesterday");
        date("2008/01/26 22:23:30", "2 days ago");
        date("2007/01/26 22:23:30", undefined);
    });

    test("prettyDate.update", function() {
        var links = document.getElementById("qunit-fixture").getElementsByTagName("a");
        equal(links[0].innerHTML, "January 28th, 2008");
        equal(links[2].innerHTML, "January 27th, 2008");
        prettyDate.update("2008-01-28T22:25:00Z");
        equal(links[0].innerHTML, "2 hours ago");
        equal(links[2].innerHTML, "Yesterday");
    });

    test("prettyDate.update, one day later", function() {
        var links = document.getElementById("qunit-fixture").getElementsByTagName("a");
        equal(links[0].innerHTML, "January 28th, 2008");
        equal(links[2].innerHTML, "January 27th, 2008");
        prettyDate.update("2008-01-28T22:25:00Z");
        equal(links[0].innerHTML, "Yesterday");
        equal(links[2].innerHTML, "2 days ago");
    });
    &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div id="qunit"&gt;&lt;/div&gt;
    &lt;div id="qunit-fixture"&gt;
        &lt;ul&gt;
            &lt;li class="entry" id="post57"&gt;
                &lt;p&gt;blah blah blah…&lt;/p&gt;
                &lt;small class="extra"&gt;
                    Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-28T20:24:17Z"&gt;January 28th, 2008&lt;/a&gt;&lt;/span&gt;
                    by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
                &lt;/small&gt;
            &lt;/li&gt;
            &lt;li class="entry" id="post57"&gt;
                &lt;p&gt;blah blah blah…&lt;/p&gt;
                &lt;small class="extra"&gt;
                    Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-27T22:24:17Z"&gt;January 27th, 2008&lt;/a&gt;&lt;/span&gt;
                    by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
                &lt;/small&gt;
            &lt;/li&gt;
        &lt;/ul&gt;
    &lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

Here’s the contents of <code>prettydate2.js</code>:

<pre><code class="language-javascript">var prettyDate = {
    format: function(now, time){
        var date = new Date(time || ""),
            diff = (((new Date(now)).getTime() - date.getTime()) / 1000),
            day_diff = Math.floor(diff / 86400);

        if (isNaN(day_diff) || day_diff &lt; 0 || day_diff &gt;= 31) {
            return;
        }

        return day_diff === 0 &amp;&amp; (
                diff &lt; 60 &amp;&amp; "just now" ||
                diff &lt; 120 &amp;&amp; "1 minute ago" ||
                diff &lt; 3600 &amp;&amp; Math.floor( diff / 60 ) + " minutes ago" ||
                diff &lt; 7200 &amp;&amp; "1 hour ago" ||
                diff &lt; 86400 &amp;&amp; Math.floor( diff / 3600 ) + " hours ago") ||
            day_diff === 1 &amp;&amp; "Yesterday" ||
            day_diff &lt; 7 &amp;&amp; day_diff + " days ago" ||
            day_diff &lt; 31 &amp;&amp; Math.ceil( day_diff / 7 ) + " weeks ago";
    },

    update: function(now) {
        var links = document.getElementsByTagName("a");
        for ( var i = 0; i &lt; links.length; i++ ) {
            if (links[i].title) {
                var date = prettyDate.format(now, links[i].title);
                if (date) {
                    links[i].innerHTML = date;
                }
            }
        }
    }
};</code></pre>

*   [Run this example.](https://smashingmagazine.com/provide/introduction-to-js-unit-testing-code/6-qunit-dom.html)

The new <code>prettyDate.update</code> function is an extract of the initial example, but with the <code>now</code> argument to pass through to <code>prettyDate.format</code>. The QUnit-based test for that function starts by selecting all <code>a</code> elements within the <code>#qunit-fixture</code> element. In the updated markup in the body element, the <code>&lt;div id="qunit-fixture"&gt;…&lt;/div&gt;</code> is new. It contains an extract of the markup from our initial example, enough to write useful tests against. By putting it in the <code>#qunit-fixture</code> element, we don’t have to worry about DOM changes from one test affecting other tests, because QUnit will automatically reset the markup after each test.

Let’s look at the first test for <code>prettyDate.update</code>. After selecting those anchors, two assertions verify that these have their initial text values. Afterwards, <code>prettyDate.update</code> is called, passing along a fixed date (the same as in previous tests). Afterwards, two more assertions are run, now verifying that the <code>innerHTML</code> property of these elements have the correctly formatted date, “2 hours ago” and “Yesterday.”

## Refactoring, Stage 2

The next test, <code>prettyDate.update, one day later</code>, does nearly the same thing, except that it passes a different date to <code>prettyDate.update</code> and, therefore, expects different results for the two links. Let’s see if we can refactor these tests to remove the duplication.

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;
    &lt;title&gt;Refactored date examples&lt;/title&gt;
    &lt;link rel="stylesheet" href="qunit.css" /&gt;
    &lt;script src="qunit.js"&gt;&lt;/script&gt;
    &lt;script src="prettydate2.js"&gt;&lt;/script&gt;
    &lt;script&gt;
    test("prettydate.format", function() {
        function date(then, expected) {
            equal(prettyDate.format("2008/01/28 22:25:00", then), expected);
        }
        date("2008/01/28 22:24:30", "just now");
        date("2008/01/28 22:23:30", "1 minute ago");
        date("2008/01/28 21:23:30", "1 hour ago");
        date("2008/01/27 22:23:30", "Yesterday");
        date("2008/01/26 22:23:30", "2 days ago");
        date("2007/01/26 22:23:30", undefined);
    });

    function domtest(name, now, first, second) {
        test(name, function() {
            var links = document.getElementById("qunit-fixture").getElementsByTagName("a");
            equal(links[0].innerHTML, "January 28th, 2008");
            equal(links[2].innerHTML, "January 27th, 2008");
            prettyDate.update(now);
            equal(links[0].innerHTML, first);
            equal(links[2].innerHTML, second);
        });
    }
    domtest("prettyDate.update", "2008-01-28T22:25:00Z:00", "2 hours ago", "Yesterday");
    domtest("prettyDate.update, one day later", "2008-01-29T22:25:00Z:00", "Yesterday", "2 days ago");
    &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div id="qunit"&gt;&lt;/div&gt;
    &lt;div id="qunit-fixture"&gt;
        &lt;ul&gt;
            &lt;li class="entry" id="post57"&gt;
                &lt;p&gt;blah blah blah…&lt;/p&gt;
                &lt;small class="extra"&gt;
                    Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-28T20:24:17Z"&gt;January 28th, 2008&lt;/a&gt;&lt;/span&gt;
                    by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
                &lt;/small&gt;
            &lt;/li&gt;
            &lt;li class="entry" id="post57"&gt;
                &lt;p&gt;blah blah blah…&lt;/p&gt;
                &lt;small class="extra"&gt;
                    Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-27T22:24:17Z"&gt;January 27th, 2008&lt;/a&gt;&lt;/span&gt;
                    by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
                &lt;/small&gt;
            &lt;/li&gt;
        &lt;/ul&gt;
    &lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

*   [Run this example.](https://smashingmagazine.com/provide/introduction-to-js-unit-testing-code/7-qunit-dom-refactored.html)

Here we have a new function called <code>domtest</code>, which encapsulates the logic of the two previous calls to test, introducing arguments for the test name, the date string and the two expected strings. It then gets called twice.</p>

## Back To The Start

With that in place, let’s go back to our initial example and see what that looks like now, after the refactoring.

<pre><code class="language-markup tmp-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;
    &lt;title&gt;Final date examples&lt;/title&gt;
    &lt;script src="prettydate2.js"&gt;&lt;/script&gt;
    &lt;script&gt;
    window.onload = function() {
        prettyDate.update("2008-01-28T22:25:00Z");
    };
    &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;ul&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-28T20:24:17Z"&gt;&lt;span&gt;January 28th, 2008&lt;/span&gt;&lt;/a&gt;&lt;/span&gt;
        by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
    &lt;/small&gt;
&lt;/li&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-27T22:24:17Z"&gt;&lt;span&gt;January 27th, 2008&lt;/span&gt;&lt;/a&gt;&lt;/span&gt;
        by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
    &lt;/small&gt;
&lt;/li&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-26T22:24:17Z"&gt;&lt;span&gt;January 26th, 2008&lt;/span&gt;&lt;/a&gt;&lt;/span&gt;
        by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
    &lt;/small&gt;
&lt;/li&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-25T22:24:17Z"&gt;&lt;span&gt;January 25th, 2008&lt;/span&gt;&lt;/a&gt;&lt;/span&gt;
        by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
    &lt;/small&gt;
&lt;/li&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-24T22:24:17Z"&gt;&lt;span&gt;January 24th, 2008&lt;/span&gt;&lt;/a&gt;&lt;/span&gt;
        by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;

    &lt;/small&gt;
&lt;/li&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-14T22:24:17Z"&gt;&lt;span&gt;January 14th, 2008&lt;/span&gt;&lt;/a&gt;&lt;/span&gt;
        by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
    &lt;/small&gt;
&lt;/li&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2008-01-04T22:24:17Z"&gt;&lt;span&gt;January 4th, 2008&lt;/span&gt;&lt;/a&gt;&lt;/span&gt;
        by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
    &lt;/small&gt;
&lt;/li&gt;
&lt;li class="entry" id="post57"&gt;
    &lt;p&gt;blah blah blah…&lt;/p&gt;
    &lt;small class="extra"&gt;
        Posted &lt;span class="time"&gt;&lt;a href="/2008/01/blah/57/" title="2007-12-15T22:24:17Z"&gt;&lt;span&gt;December 15th, 2008&lt;/span&gt;&lt;/a&gt;&lt;/span&gt;
        by &lt;span class="author"&gt;&lt;a href="/john/"&gt;John Resig&lt;/a&gt;&lt;/span&gt;
    &lt;/small&gt;
&lt;/li&gt;
&lt;/ul&gt;

&lt;/body&gt;
&lt;/html&gt;</code></pre>

*   [Run this example.](https://smashingmagazine.com/provide/introduction-to-js-unit-testing-code/8-endstate.html)

For a non-static example, we’d remove the argument to <code>prettyDate.update</code>. All in all, the refactoring is a huge improvement over the first example. And thanks to the <code>prettyDate</code> module that we introduced, we can add even more functionality without clobbering the global namespace.</p>

## Conclusion

Testing JavaScript code is not just a matter of using some test runner and writing a few tests; it usually requires some heavy structural changes when applied to code that has been tested only manually before. We’ve walked through an example of how to change the code structure of an existing module to run some tests using an ad-hoc testing framework, then replacing that with a more full-featured framework to get useful visual results.

QUnit itself has a lot more to offer, with specific support for testing asynchronous code such as timeouts, AJAX and events. Its visual test runner helps to debug code by making it easy to rerun specific tests and by providing stack traces for failed assertions and caught exceptions. For further reading, check out the <a href="https://qunitjs.com/cookbook">QUnit Cookbook</a>.

<em>(al) (km)</em>


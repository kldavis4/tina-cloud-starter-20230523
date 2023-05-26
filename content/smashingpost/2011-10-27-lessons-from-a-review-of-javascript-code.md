---
title: 9 Lessons From A Review Of JavaScript Code
slug: lessons-from-a-review-of-javascript-code
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a8e8cfc5-5494-45e6-99de-e0483692e0b2/sitting-properly-at-desk-illu.jpg
date: 2011-10-27T11:32:05.000Z
author: addy-osmani
description: >-
  Before we start, I’d like to pose a question: when was the last time you asked someone to review your code? Reviewing code is possibly the single best technique to improve the overall quality of your solutions, and if you’re not actively taking advantage of it, then you’re missing out on identifying bugs and hearing suggestions that could make your code better.
categories:
  - Coding
  - JavaScript
---
None of us write 100% bug-free code all of the time, so don’t feel there’s a stigma attached to seeking help. Some of the most experienced developers in our industry, from framework authors to browser developers, regularly request reviews of their code from others; asking whether something could be tweaked should in no way be considered embarrassing. Reviews are a technique like any other and should be used where possible.

## <span class="rh">Further Reading</span> on SmashingMag:

*   [JavaScript Mistakes To Avoid With A Static Code Analyzer](https://www.smashingmagazine.com/2015/02/avoid-javascript-mistakes-with-static-code-analyzer/)
*   [<span class="headline">Writing Fast, Memory-Efficient JavaScript</span>](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)
*   [JavaScript Profiling With The Chrome Developer Tools](https://www.smashingmagazine.com/2012/06/javascript-profiling-chrome-developer-tools/)
*   [How To Keep Your Coding Workflow Organized](https://www.smashingmagazine.com/2011/01/cleaning-up-the-mess-how-to-keep-your-coding-workflow-organized/)

Today we’ll look at <em>where </em>to get your code reviewed, <em>how</em> to structure your requests, and <em>what </em>reviewers look for. I was recently asked to review some code for a new JavaScript application, and thought I’d like to share some of my feedback, because it covers some JavaScript fundamentals that are always useful to bear in mind.

{{% feature-panel %}}

## Introduction

Reviewing code goes hand in hand with maintaining strong coding standards. That said, standards don’t usually prevent logical errors or misunderstandings about the quirks of a programming language, whether it’s JavaScript, Ruby, Objective-C or something else. Even the most experienced developers can make these kinds of mistakes, and reviewing code can greatly assist with catching them.

The first reaction most of us have to criticism is to defend ourselves (or our code), and perhaps lash back. While criticism can be slightly demoralizing, <strong>think of it as a learning experience</strong> that spurs us to do better and to improve ourselves; because in many cases, once we’ve calmed down, it actually does.

Also remember that no one is obliged to provide feedback on your work, and if the comments are indeed constructive, then be grateful for the time spent offering the input.

Reviews enable us to build on the experience of others and to benefit from a second pair of eyes. And at the end of the day, they are an opportunity for us to write better code. Whether we take advantage of them is entirely our choice.</p>

## Where Can I Get My Code Reviewed?

Often the most challenging part is actually finding an experienced developer who you trust to do the review. Below are some places where you can request others to review your code (sometimes in other languages, too).

*   JSMentors JSMentors is a mailing list that discusses everything to do with JavaScript (including Harmony), and a number of experienced developers are on its review panel (including JD Dalton, Angus Croll and Nicholas Zakas). These mentors might not always be readily available, but they do their best to provide useful, constructive feedback on code that’s been submitted. If you’re looking for assistance with a specific JavaScript framework beyond vanilla JavaScript, the majority of frameworks and libraries have mailing lists or forums that you can post to and that might provide a similar level of assistance.
*   [freenode IRC](https://webchat.freenode.net) Many chat rooms here are dedicated both to discussing the JavaScript language and to requests for help or review. The most popular rooms are obviously named, and #javascript is particularly useful for generic JavaScript requests, while channels such as #jquery and #dojo are better for questions and requests related to particular libraries and frameworks.
*   [Code Review](https://codereview.stackexchange.com) (beta) You would be forgiven for confusing Code Review with StackOverflow, but it’s actually a very useful, broad-spectrum, subjective tool for getting peer review of code. While on StackOverflow you might ask the question “Why isn’t my code working?,” Code Review is more suited to questions like “Why is my code so ugly?” If you still have any doubt about what it offers, I strongly recommend checking out the [FAQs](https://codereview.stackexchange.com/faq).
*   [Twitter](https://twitter.com) This might sound odd, but at least half of the code that I submit for review is through social networks. Social networks work best, of course, if your code is open source, but trying them never hurts. The only thing I suggest is to ensure that the developers who you follow and interact with are experienced; a review by a developer with insufficient experience can sometimes be worse than no review at all, so be careful!
*   [GitHub + reviewth.is](https://github.com/) We all know that GitHub provides an excellent architecture for reviewing code. It comes with commits, file and line comments, update notifications, an easy way to track forks of gits and repositories, and more. All that’s missing is a way to actually initiate reviews. A tool called reviewth.is attempts to rectify that by giving you a post-commit hook that helps to automate this process, so changes that get posted in the wild have a clear #reviewthis hash tag, and you can tag any users who you wish to review your updates. If many of your colleagues happen to develop in the same language as you do, this set-up can work well for code reviews sourced closer to home. One [workflow that works well with this](https://stackoverflow.com/questions/3730527/workflow-for-github-based-code-review) (if you’re working on a team or on a collaborative project) is to perform your own work in a topic branch in a repository and then send through pull requests on that branch. Reviewers would examine the changes and commits and could then make line-by-line and file-by-file comments. You (the developer) would then take this feedback and do a destructive rebase on that topic branch, re-push it, and allow the review cycle to repeat until merging them would be acceptable.</p>

## How Should I Structure My Review Requests?

The following are some guidelines (based on experience) on how to structure your requests for code reviews, to increase the chances of them being accepted. You can be more liberal with them if the reviewer is on your team; but if the reviewer is external, then these might save you some time:

*   Isolate what you would like to be reviewed; ensure that it can be easily run, forked and commented; be clear about where you think improvements could be made; and, above all, be patient.
*   Make it as easy as possible for the reviewer to look at, demo and change your code.
*   Don’t submit a ZIP file of your entire website or project; very few people have the time to go through all of this. The only situation in which this would be acceptable is if your code absolutely required local testing.
*   Instead, isolate and reduce what you would like to be reviewed on [jsFiddle](https://jsfiddle.net), on [jsbin](https://www.jsbin.com) or in a [GitHub](https://gist.github.com) gist. This will allow the reviewer to easily fork what you’ve provided and to show changes and comments on what can be improved. If you would prefer a “diff” between your work and any changes they’ve recommended, you might also be interested in [PasteBin](https://pastebin.com), which supports this.
*   Similarly, don’t just submit a link to a page and ask them to “View source” in order to see what can be improved. On websites with a lot of scripts, this task would be challenging and lowers the chances of a reviewer agreeing to help. No one wants to work to find what you want reviewed.
*   Clearly indicate where you _personally_ feel the implementation could be improved. This will help the reviewer quickly home in on what you’re most interested in having reviewed and will save them time. Many reviewers will still look at other parts of the code you’ve submitted regardless, but at least help them prioritize.
*   Indicate what (if any) research you’ve done into techniques for improving the code. The reviewer might very well suggest the same resources, but if they’re aware that you already know of them, then they might offer alternative suggestions (which is what you want).
*   If English isn’t your first language, there’s no harm in saying so. When other developers inform me of this, I know whether to keep the language in my review technical or simple.
*   **Be patient**. Some reviews take several days to get back to me, and nothing’s wrong with that. Other developers are usually busy with other projects, and someone who agrees to schedule a look at your work is being kind. Be patient, don’t spam them with reminders, and be understanding if they get delayed. Doing this sometimes pay off, because the reviewer can provide even more detailed feedback when they have more time.</p>

## What Should Code Reviews Provide?

Jonathan Betz, a former developer at Google, once said that a code review should ideally address six things:

1.  **Correctness** Does the code do everything it claims?
2.  **Complexity** Does it accomplish its goals in a straightforward way?
3.  **Consistency** Does it achieve its goals consistently?
4.  **Maintainability** Could the code be easily extended by another member of the team with a reasonable level of effort?
5.  **Scalability** Is the code written in such a way that it would work for both 100 users and 10,000? Is it optimized?
6.  **Style** Does the code adhere to a particular style guide (preferably one agreed upon by the team if the project is collaborative)?

While I agree with this list, expanding it into an action guide of what reviewers should <strong>practically</strong> aim to give developers would be useful. So, reviewers should do the following:

*   Provide clear comments, demonstrate knowledge, and communicate well.
*   Point out the shortfalls in an implementation (without being overly critical).
*   State why a particular approach isn’t recommended, and, if possible, refer to blog posts, gists, specifications, [MDN](https://developer.mozilla.org) pages and [jsPerf](https://web.archive.org/web/20160131082743/https://jsperf.com:80/) tests to back up the statement.
*   Suggest alternative solutions, either in a separate runnable form or integrated in the code via a fork, so that the developer can clearly see what they did wrong.
*   Focus on solutions first, and style second. Suggestions on style can come later in the review, but address the fundamental problem as thoroughly as possible before paying attention to this.
*   Review beyond the scope of what was requested. This is entirely at the reviewer’s discretion, but if I notice issues with other aspects of a developer’s implementation, then I generally try to advise them on how those, too, might be improved. I’ve yet to receive a complaint about this, so I assume it’s not a bad thing.</p>

## Collaborative Code Reviews

Although a review by one developer can work well, an alternative approach is to bring more people into the process. This has a few distinct advantages, including reducing the load on individual reviewers and exposing more people to your implementation, which could potentially lead to more suggestions for improvements. It also allows a reviewer’s comments to be screened and corrected if they happen to make a mistake.

To assist the group, you may wish to employ a collaborative tool to allow all reviewers to simultaneously inspect and comment on your code. Luckily, a few decent ones out there are worth checking out:

*   [Review Board](https://www.reviewboard.org/) This Web-based tool is available for free under the MIT license. It integrates with Git, CVS, Mercurial, Subversion and a number of other source-control systems. Review Board can be installed on any server running Apache or lighttpd and is free for personal and commercial use.
*   [Crucible](https://www.atlassian.com/software/crucible) This tool by Australian software company Atlassian is also Web-based. It’s aimed at the enterprise and works best with distributed teams. Crucible facilitates both live review and live commenting and, like Review Board, integrates with a number of source-control tools, including Git and Subversion.
*   [Rietveld](https://code.google.com/p/rietveld/) Like the other two, Rietveld also supports collaborative review, but it was actually written by the creator of Python, Guido van Rossum. It is designed to run on Google’s cloud service and benefits from Guido’s experience writing Mondrian, the proprietary app that Google uses internally to review its code.
*   Others A number of other options for collaborative code review weren’t created for that purpose. These include [CollabEdit](https://collabedit.com/) (free and Web-based) and, my personal favorite, [EtherPad](https://piratepad.net/front-page/) (also free and Web-based).

<figure><a href="https://www.flickr.com/photos/joelogon/324259281/sizes/m/in/photostream/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0174f16b-fe31-41c8-bba1-824291fd6d99/exhaustion.jpg" /></a><figcaption>(Image Source: <a href="https://www.flickr.com/photos/joelogon/324259281/sizes/m/in/photostream/">joelogon</a>)</figcaption></figure>

## Lessons From A JavaScript Code Review

On to the review.

A developer recently wrote in, asking me to review their code and provide some useful suggestions on how they might improve it. While I’m certainly not an expert on reviewing code (don’t let the above fool you), here are the problems and solutions that I proposed.</p>

### Problem 1

<strong>Problem:</strong> Functions and objects are passed as arguments to other functions without any type validation.

<strong>Feedback:</strong> Type validation is an essential step in ensuring that you’re working only with input of a desired type. Without sanitization checks in place, you run the risk of users passing in just about anything (a string, a date, an array, etc.), which could easily break your application if you haven’t developed it defensively. For functions, you should do the following at a minimum:

1.  Test to ensure that arguments being passed actually exist,
2.  Do a `typeof` check to prevent the app from executing input that is not a valid function at all.

<pre><code class="language-javascript">if (callback &amp;&amp; typeof callback === "function"){
    /* rest of your logic */
}else{
    /* not a valid function */
}</code></pre>

Unfortunately, a simple <code>typeof</code> check <strong>isn’t enough</strong> on its own. As Angus Croll points out in his post “<a href="https://javascriptweblog.wordpress.com/2011/08/08/fixing-the-javascript-typeof-operator/">Fixing the typeof operator</a>,” you need to be aware of a number of issues with <code>typeof</code> checking if you’re using them for anything other than functions.

For example, <code>typeof null</code> returns <code>object</code>, which is technically incorrect. In fact, when <code>typeof</code> is applied to any object type that isn’t a function, it returns <code>object</code>, not distinguishing between <code>Array</code>, <code>Date</code>, <code>RegEx</code> or whatever else.

The solution is to use <code>Object.prototype.toString</code> to call the underlying internal property of JavaScript objects known as <code>[[Class]]</code>, the class property of the object. Unfortunately, specialized built-in objects generally overwrite <code>Object.prototype.toString</code>, but you can force the generic <code>toString</code> function on them:

<pre><code class="language-javascript">Object.prototype.toString.call([1,2,3]); //"[object Array]"</code></pre>

You might also find Angus’s function below useful as a more reliable alternative to <code>typeof</code>. Try calling <code>betterTypeOf()</code> against objects, arrays and other types to see what happens.

<pre><code class="language-javascript">function betterTypeOf( input ){
    return Object.prototype.toString.call(input).match(/^[objects(.*)]$/)[1];
}</code></pre>

Here, <code>parseInt()</code> is being blindly used to parse an integer value of user input, but no base is specified. This can cause issues.

In <a href="https://shop.oreilly.com/product/9780596517748.do"><em>JavaScript: The Good Parts</em></a>, Douglas Crockford refers to <code>parseInt()</code> as being dangerous. Although you probably know that passing it a string argument returns an integer, you should also ideally specify a base or radix as the second argument, otherwise it might return unexpected output. Take the following example:

<pre><code class="language-javascript">parseInt('20');       // returns what you expect, however…
parseInt('020');      // returns 16
parseInt('000020');   // returns 16
parseInt('020', 10);  // returns 20 as we've specified the base to use</code></pre>

You’d be surprised by how many developers omit the second argument, but it happens quite regularly. Remember that your users (if permitted to freely enter numeric input) won’t necessarily follow standard number conventions (because they’re crazy!). I’ve seen <code>020</code>, <code>,20</code>, <code>;'20</code> and many other variations used, so do your best to parse as broad a range of inputs as possible. The following tricks to using <code>parseInt()</code> are occasionally better:

<pre><code class="language-javascript">Math.floor("020");   // returns 20
Math.floor("0020");  //returns 20
Number("020");  //returns 20
Number("0020"); //returns 20
+"020"; //returns 20</code></pre>

### Problem 2

<strong>Problem:</strong> Checks for browser-specific conditions being met are repeated throughout the code base (for example, feature detection, checks for supported ES5 features, etc.).

<strong>Feedback:</strong> Ideally, your code base should be as DRY as possible, and there are some elegant solutions to this problem. For example, you might benefit from the <strong>load-time configuration</strong> pattern here (also called load-time and init-time branching). The basic idea is that you test a condition only once (when the application loads) and then access the result of that test for all subsequent checks. This pattern is commonly found in JavaScript libraries that configure themselves at load time to be optimized for a particular browser.

This pattern could be implemented as follows:

<pre><code class="language-javascript">var tools = {
    addMethod: null,
    removeMethod: null
};

if(/* condition for native support */){
    tools.addMethod = function(/* params */){
        /* method logic */
    }
}else{
    /* fallback - eg. for IE */
    tools.addMethod = function(/* */){
        /* method logic */
    }
}</code></pre>

The example below demonstrates how this can be used to normalize getting an <code>XMLHttpRequest</code> object.

<pre><code class="language-javascript">var utils = {
    getXHR: null
};

if(window.XMLHttpRequest){
    utils.getXHR = function(){
        return new XMLHttpRequest;
    }
}else if(window.ActiveXObject){
    utils.getXHR = function(){
        /* this has been simplified for example sakes */
        return new ActiveXObject(’Microsoft.XMLHTTP’);
    }
}</code></pre>

For a great example, Stoyan Stefanov applies this to attaching and removing event listeners cross-browser, in his book <a href="https://shop.oreilly.com/product/9780596806767.do"><em>JavaScript Patterns</em></a>:

<pre><code class="language-javascript">var utils = {
    addListener: null,
    removeListener: null
};
// the implementation
if (typeof window.addEventListener === ’function’) {
    utils.addListener = function ( el, type, fn ) {
        el.addEventListener(type, fn, false);
    };
    utils.removeListener = function ( el, type, fn ) {
        el.removeEventListener(type, fn, false);
    };
} else if (typeof document.attachEvent === ’function’) { // IE
    utils.addListener = function ( el, type, fn ) {
        el.attachEvent(’on’ + type, fn);
    };
    utils.removeListener = function ( el, type, fn ) {
        el.detachEvent(’on’ + type, fn);
    };
} else { // older browsers
    utils.addListener = function ( el, type, fn ) {
        el[’on’ + type] = fn;
    };
    utils.removeListener = function ( el, type, fn ) {
        el[’on’ + type] = null;
    };
}</code></pre>

### Problem 3

<strong>Problem:</strong> The native <code>Object.prototype</code> is being extended regularly.

<strong>Feedback:</strong> Extending native types is generally frowned upon, and few (if any) popular code bases should dare to extend <code>Object.prototype</code>. The reality is that there is not likely a situation in which you absolutely need to extend it in this way. In addition to breaking the object-as-hash tables in JavaScript and increasing the chance of naming collisions, it’s generally considered bad practice, and modifying it should only be a last resort (this is quite different from extending your own <em>custom</em> <code>object</code> properties).

If for some reason you <em>do</em> end up extending the <code>object</code> prototype, ensure that the method doesn’t already exist, and document it so that the rest of the team is aware why it’s necessary. You can use the following code sample as a guide:

<pre><code class="language-javascript">if(typeof Object.prototype.myMethod != ’function’){
    Object.prototype.myMethod = function(){
        //implem
    };
}</code></pre>

<a href="https://twitter.com/kangax">Juriy Zaytsev</a> has a great post on extending native and host objects, which may be of interest.</p>

### Problem 4

<strong>Problem:</strong> Some of the code is heavily blocking the page because it’s either waiting on processes to complete or data to load before executing anything further.

<strong>Feedback:</strong> Page-blocking makes for a poor user experience, and there are a number of ways to work around it without impairing the application.

One solution is to use “deferred execution” (via promises and futures). The basic idea with promises is that, rather than issuing blocking calls for resources, you immediately return a promise for a future value that will eventually be fulfilled. This rather easily allows you to write non-blocking logic that can be run asynchronously. It is common to introduce callbacks into this equation that execute once the request completes.

I’ve written a relatively comprehensive <a href="https://msdn.microsoft.com/en-us/scriptjunkie/gg723713">post</a> on this with Julian Aubourg, if you’re interested in doing this through jQuery, but it can of course be implemented with vanilla JavaScript as well.

Micro-framework <a href="https://github.com/kriskowal/">Q</a> offers a CommonJS-compatible implementation of promises and futures that is relatively comprehensive and can be used as follows:

<pre><code class="language-javascript">/* define a promise-only delay function that resolves when a timeout completes */
function delay(ms) {
    var deferred = Q.defer();
    setTimeout(deferred.resolve, ms);
    return deferred.promise;
}

/* usage of Q with the 'when' pattern to execute a callback once delay fulfils the promise */
Q.when(delay(500), function () {
        /* do stuff in the callback */
});</code></pre>

If you’re looking for something more basic that can be read through, then here is Douglas Crockford’s implementation of promises:

<pre><code class="language-javascript">function make_promise() {
  var status = ’unresolved’,
      outcome,
      waiting = [],
      dreading = [];

  function vouch( deed, func ) {
    switch (status) {
    case ’unresolved’:
      (deed === ’fulfilled’ ? waiting : dreading).push(func);
      break;
    case deed:
      func(outcome);
      break;
    }
  };

  function resolve( deed, value ) {
    if (status !== ’unresolved’) {
      throw new Error(’The promise has already been resolved:’ + status);
    }
    status = deed;
    outcome = value;
    (deed == ’fulfilled’ ? waiting : dreading).forEach(function (func) {
      try {
        func(outcome);
      } catch (ignore) {}
    });
    waiting = null;
    dreading = null;
  };

  return {
    when: function ( func ) {
      vouch(’fulfilled’, func);
    },
    fail: function ( func ) {
      vouch(’smashed’, func);
    },
    fulfill: function ( value ) {
      resolve(’fulfilled’, value);
    },
    smash: function ( string ) {
      resolve(’smashed’, string);
    },
    status: function () {
      return status;
    }
  };
};</code></pre>

### Problem 5

<strong>Problem:</strong> You’re testing for explicit numeric equality of a property using the <code>==</code> operator, but you should probably be using <code>===</code> instead

<strong>Feedback:</strong> As you may or may not know, the identity <code>==</code> operator in JavaScript is fairly liberal and considers values to be equal even if they’re of completely different types. This is due to the operator forcing a coercion of values into a single type (usually a number) prior to performing any comparison. The <code>===</code> operator will, however, not do this conversion, so if the two values being compared are not of the same type, then <code>===</code> will just return <code>false</code>.

The reason I recommend considering <code>===</code> for more specific type comparison (in this case) is that <code>==</code> is known to have a number of gotchas and is considered to be unreliable by many developers.

You might also be interested to know that in abstractions of the language, such as CoffeeScript, the <code>==</code> operator is completely dropped in favor of <code>===</code> beneath the hood due to the former’s unreliability.

Rather than take my word for it, see the examples below of boolean checks for equality using <code>==</code>, some of which result in rather unexpected outputs.

<pre><code class="language-javascript">3 == "3" // true
3 == "03" // true
3 == "0003" // true
3 == "+3" //true
3 == [3] //true
3 == (true+2) //true
’ trn ’ == 0 //true
"trn" == 0 //true
"t" == 0 // true
"tn" == 0 // true
"tr" == 0 // true
" " == 0 // true
" t" == 0 // true
"  " == 0 // true
" rn " == 0 //true</code></pre>

The reason that many of the (stranger) results in this list evaluate to <code>true</code> is because JavaScript is a weakly typed language: it applies type coercion <em>wherever</em> possible. If you’re interested in learning more about why some of the expressions above evaluate to <code>true</code>, look at the <a href="https://es5.github.com/#x9.3.1">Annotated ES5</a> guide, whose explanations are rather fascinating.

Back to the review. If you’re 100% certain that the values being compared cannot be interfered with by the user, then proceed with using the <code>==</code> operator with caution. Just remember that <code>===</code> covers your bases better in the event of an unexpected input.</p>

### Problem 6

<strong>Problem:</strong> An uncached array <code>length</code> is being used in all <code>for</code> loops. This is particularly bad because you’re using it when iterating through an HTMLCollection.

Here’s an example:

<pre><code class="language-javascript">for( var i=0; i&lt;myArray.length;i++ ){
    /* do stuff */
}</code></pre>

<strong>Feedback:</strong> The problem with this approach (which I still see a number of developers using) is that the array <code>length</code> is unnecessarily re-accessed on each loop’s iteration. This can be very slow, especially when working with HTMLCollections (in which case, caching the <code>length</code> can be anywhere up to 190 times faster than repeatedly accessing it, as Nicholas C. Zakas mentions in his book <a href="https://shop.oreilly.com/product/9780596802806.do"><em>High-Performance JavaScript</em></a>). Below are some options for caching the array <code>length</code>.

<pre><code class="language-javascript">/* cached outside loop */
var len = myArray.length;
for ( var i = 0; i &lt; len; i++ ) {
}

/* cached inside loop */
for ( var i = 0, len = myArray.length; i &lt; len; i++ ) {
}

/* cached outside loop using while */
var len = myArray.length;
while (len--) {
}</code></pre>

A <a href="https://web.archive.org/web/20160131082743/https://jsperf.com:80/">jsPerf</a> test that compares the performance benefits of caching the array <code>length</code> inside and outside the loop, using prefix increments, counting down and more is also available, if you would like to study which performs the best.</p>

### Problem 7

<strong>Problem:</strong> jQuery’s <code>$.each()</code> is being used to iterate over objects and arrays, in some cases while <code>for</code> is being used in others.

<strong>Feedback:</strong> In jQuery, we have two ways to seamlessly iterate over objects and arrays. The generic <a href="https://api.jquery.com/jQuery.each/"><code>$.each</code></a> iterates over both of these types, whereas <a href="https://api.jquery.com/each/"><code>$.fn.each()</code></a> iterates over a jQuery object specifically (where standard objects can be wrapped with <code>$()</code> should you wish to use them with the latter). While the lower-level <code>$.each</code> performs better than <code>$.fn.each()</code>, both standard JavaScript <code>for</code> and <code>while</code> loops perform much better than either, as proven by this jsPerf test. Below are some examples of loop alternatives that also perform better:

<pre><code class="language-javascript">/* jQuery $.each */
$.each(a, function() {
 e = $(this);
});

/* classic for loop */
var len = a.length;
for ( var i = 0; i &lt; len; i++ ) {
    //if this must be a jQuery object do..
    e = $(a[i]);
    //otherwise just e = a[i] should suffice
};

/* reverse for loop */
for ( var i = a.length; i-- ) {
    e = $(a[i]);
}

/* classic while loop */
var i = a.length;
while (i--) {
    e = $(a[i]);
}

/* alternative while loop */
var i = a.length - 1;

while ( e = a[i--] ) {
    $(e)
};</code></pre>

You might find Angus Croll’s post on “<a href="https://javascriptweblog.wordpress.com/2010/10/11/rethinking-javascript-for-loops/">Rethinking JavaScript <code>for</code> Loops</a>” an interesting extension to these suggestions.

Given that this is a data-centric application with a potentially large quantity of data in each object or array, you should consider a refactor to use one of these. From a scalability perspective, you want to shave off as many milliseconds as possible from process-heavy routines, because these can build up when hundreds or thousands of elements are on the page.</p>

### Problem 8

<strong>Problem:</strong> JSON strings are being built in-memory using string concatenation.

<strong>Feedback:</strong> This could be approached in more optimal ways. For example, why not use <code>JSON.stringify()</code>, a method that accepts a JavaScript object and returns its JSON equivalent. Objects can generally be as complex or as deeply nested as you wish, and this will almost certainly result in a simpler, shorter solution.

<pre><code class="language-javascript">var myData = {};
myData.dataA = [’a’, ’b’, ’c’, ’d’];
myData.dataB = {
    ’animal’: ’cat’,
    ’color’: ’brown’
};
myData.dataC = {
    ’vehicles’: [{
        ’type’: ’ford’,
        ’tint’: ’silver’,
        ’year’: ’2015’
    }, {
        ’type’: ’honda’,
        ’tint’: ’black’,
        ’year’: ’2012’
    }]
};
myData.dataD = {
    ’buildings’: [{
        ’houses’: [{
            ’streetName’: ’sycamore close’,
            ’number’: ’252’
        }, {
            ’streetName’: ’slimdon close’,
            ’number’: ’101’
        }]
    }]
};
console.log(myData); //object
var jsonData = JSON.stringify(myData);

console.log(jsonData);
/*
{"dataA":["a","b","c","d"],"dataB":{"animal":"cat","color":"brown"},"dataC":{"vehicles":[{"type":"ford","tint":"silver","year":"2015"},{"type":"honda","tint":"black","year":"2012"}]},"dataD":{"buildings":[{"houses":[{"streetName":"sycamore close","number":"252"},{"streetName":"slimdon close","number":"101"}]}]}}
 */</code></pre>

As an extra debugging tip, if you would like to pretty-print JSON in your console for easier reading, then the following extra arguments to <code>stringify()</code> will achieve this:

<pre><code class="language-javascript">JSON.stringify({ foo: "hello", bar: "world" }, null, 4);</code></pre>

### Problem 9

<strong>Problem:</strong> The namespacing pattern used is technically invalid.

<strong>Feedback:</strong> While namespacing is implemented correctly across the rest of the application, the initial check for namespace existence is invalid. Here’s what you currently have:

<pre><code class="language-javascript">if ( !MyNamespace ) {
  MyNamespace = { };
}</code></pre>

The problem is that <code>!MyNamespace</code> will throw a <code>ReferenceError</code>, because the <code>MyNamespace</code> variable was never declared. A better pattern would take advantage of boolean conversion with an inner variable declaration, as follows:

<pre><code class="language-javascript">if ( !MyNamespace ) {
  var MyNamespace = { };
}
</code></pre>

<strong>Problem:</strong> Some of the code is heavily blocking the page because it’s either waiting on processes to complete or data to load before executing anything further.

<strong>Feedback:</strong> Page-blocking makes for a poor user experience, and there are a number of ways to work around it without impairing the application.

One solution is to use “deferred execution” (via promises and futures). The basic idea with promises is that, rather than issuing blocking calls for resources, you immediately return a promise for a future value that will eventually be fulfilled. This rather easily allows you to write non-blocking logic that can be run asynchronously. It is common to introduce callbacks into this equation that execute once the request completes.

I’ve written a relatively comprehensive <a href="https://msdn.microsoft.com/en-us/scriptjunkie/gg723713">post</a> on this with Julian Aubourg, if you’re interested in doing this through jQuery, but it can of course be implemented with vanilla JavaScript as well.

Micro-framework <a href="https://github.com/kriskowal/">Q</a> offers a CommonJS-compatible implementation of promises and futures that is relatively comprehensive and can be used as follows:

<pre><code class="language-javascript">/* define a promise-only delay function that resolves when a timeout completes */
function delay(ms) {
    var deferred = Q.defer();
    setTimeout(deferred.resolve, ms);
    return deferred.promise;
}

/* usage of Q with the 'when' pattern to execute a callback once delay fulfils the promise */
Q.when(delay(500), function () {
        /* do stuff in the callback */
});</code></pre>

If you’re looking for something more basic that can be read through, then here is Douglas Crockford’s implementation of promises:

<pre><code class="language-javascript">function make_promise() {
  var status = ’unresolved’,
      outcome,
      waiting = [],
      dreading = [];

  function vouch( deed, func ) {
    switch (status) {
    case ’unresolved’:
      (deed === ’fulfilled’ ? waiting : dreading).push(func);
      break;
    case deed:
      func(outcome);
      break;
    }
  };

  function resolve( deed, value ) {
    if (status !== ’unresolved’) {
      throw new Error(’The promise has already been resolved:’ + status);
    }
    status = deed;
    outcome = value;
    (deed == ’fulfilled’ ? waiting : dreading).forEach(function (func) {
      try {
        func(outcome);
      } catch (ignore) {}
    });
    waiting = null;
    dreading = null;
  };

  return {
    when: function ( func ) {
      vouch(’fulfilled’, func);
    },
    fail: function ( func ) {
      vouch(’smashed’, func);
    },
    fulfill: function ( value ) {
      resolve(’fulfilled’, value);
    },
    smash: function ( string ) {
      resolve(’smashed’, string);
    },
    status: function () {
      return status;
    }
  };
};</code></pre>

### Problem 5

<strong>Problem:</strong> You’re testing for explicit numeric equality of a property using the <code>==</code> operator, but you should probably be using <code>===</code> instead

<strong>Feedback:</strong> As you may or may not know, the identity <code>==</code> operator in JavaScript is fairly liberal and considers values to be equal even if they’re of completely different types. This is due to the operator forcing a coercion of values into a single type (usually a number) prior to performing any comparison. The <code>===</code> operator will, however, not do this conversion, so if the two values being compared are not of the same type, then <code>===</code> will just return <code>false</code>.

The reason I recommend considering <code>===</code> for more specific type comparison (in this case) is that <code>==</code> is known to have a number of gotchas and is considered to be unreliable by many developers.

You might also be interested to know that in abstractions of the language, such as CoffeeScript, the <code>==</code> operator is completely dropped in favor of <code>===</code> beneath the hood due to the former’s unreliability.

Rather than take my word for it, see the examples below of boolean checks for equality using <code>==</code>, some of which result in rather unexpected outputs.

<pre><code class="language-javascript">3 == "3" // true
3 == "03" // true
3 == "0003" // true
3 == "+3" //true
3 == [3] //true
3 == (true+2) //true
’ trn ’ == 0 //true
"trn" == 0 //true
"t" == 0 // true
"tn" == 0 // true
"tr" == 0 // true
" " == 0 // true
" t" == 0 // true
"  " == 0 // true
" rn " == 0 //true</code></pre>

The reason that many of the (stranger) results in this list evaluate to <code>true</code> is because JavaScript is a weakly typed language: it applies type coercion <em>wherever</em> possible. If you’re interested in learning more about why some of the expressions above evaluate to <code>true</code>, look at the <a href="https://es5.github.com/#x9.3.1">Annotated ES5</a> guide, whose explanations are rather fascinating.

Back to the review. If you’re 100% certain that the values being compared cannot be interfered with by the user, then proceed with using the <code>==</code> operator with caution. Just remember that <code>===</code> covers your bases better in the event of an unexpected input.</p>

### Problem 6

<strong>Problem:</strong> An uncached array <code>length</code> is being used in all <code>for</code> loops. This is particularly bad because you’re using it when iterating through an HTMLCollection.

Here’s an example:

<pre><code class="language-javascript">for( var i=0; i&lt;myArray.length;i++ ){
    /* do stuff */
}</code></pre>

<strong>Feedback:</strong> The problem with this approach (which I still see a number of developers using) is that the array <code>length</code> is unnecessarily re-accessed on each loop’s iteration. This can be very slow, especially when working with HTMLCollections (in which case, caching the <code>length</code> can be anywhere up to 190 times faster than repeatedly accessing it, as Nicholas C. Zakas mentions in his book <a href="https://shop.oreilly.com/product/9780596802806.do"><em>High-Performance JavaScript</em></a>). Below are some options for caching the array <code>length</code>.

<pre><code class="language-javascript">/* cached outside loop */
var len = myArray.length;
for ( var i = 0; i &lt; len; i++ ) {
}

/* cached inside loop */
for ( var i = 0, len = myArray.length; i &lt; len; i++ ) {
}

/* cached outside loop using while */
var len = myArray.length;
while (len--) {
}</code></pre>

A <a href="https://web.archive.org/web/20160131082743/https://jsperf.com:80/">jsPerf</a> test that compares the performance benefits of caching the array <code>length</code> inside and outside the loop, using prefix increments, counting down and more is also available, if you would like to study which performs the best.</p>

### Problem 7

<strong>Problem:</strong> jQuery’s <code>$.each()</code> is being used to iterate over objects and arrays, in some cases while <code>for</code> is being used in others.

<strong>Feedback:</strong> In jQuery, we have two ways to seamlessly iterate over objects and arrays. The generic <a href="https://api.jquery.com/jQuery.each/"><code>$.each</code></a> iterates over both of these types, whereas <a href="https://api.jquery.com/each/"><code>$.fn.each()</code></a> iterates over a jQuery object specifically (where standard objects can be wrapped with <code>$()</code> should you wish to use them with the latter). While the lower-level <code>$.each</code> performs better than <code>$.fn.each()</code>, both standard JavaScript <code>for</code> and <code>while</code> loops perform much better than either, as proven by this jsPerf test. Below are some examples of loop alternatives that also perform better:

<pre><code class="language-javascript">/* jQuery $.each */
$.each(a, function() {
 e = $(this);
});

/* classic for loop */
var len = a.length;
for ( var i = 0; i &lt; len; i++ ) {
    //if this must be a jQuery object do..
    e = $(a[i]);
    //otherwise just e = a[i] should suffice
};

/* reverse for loop */
for ( var i = a.length; i-- ) {
    e = $(a[i]);
}

/* classic while loop */
var i = a.length;
while (i--) {
    e = $(a[i]);
}

/* alternative while loop */
var i = a.length - 1;

while ( e = a[i--] ) {
    $(e)
};</code></pre>

You might find Angus Croll’s post on “<a href="https://javascriptweblog.wordpress.com/2010/10/11/rethinking-javascript-for-loops/">Rethinking JavaScript <code>for</code> Loops</a>” an interesting extension to these suggestions.

Given that this is a data-centric application with a potentially large quantity of data in each object or array, you should consider a refactor to use one of these. From a scalability perspective, you want to shave off as many milliseconds as possible from process-heavy routines, because these can build up when hundreds or thousands of elements are on the page.</p>

### Problem 8

<strong>Problem:</strong> JSON strings are being built in-memory using string concatenation.

<strong>Feedback:</strong> This could be approached in more optimal ways. For example, why not use <code>JSON.stringify()</code>, a method that accepts a JavaScript object and returns its JSON equivalent. Objects can generally be as complex or as deeply nested as you wish, and this will almost certainly result in a simpler, shorter solution.

<pre><code class="language-javascript">var myData = {};
myData.dataA = [’a’, ’b’, ’c’, ’d’];
myData.dataB = {
    ’animal’: ’cat’,
    ’color’: ’brown’
};
myData.dataC = {
    ’vehicles’: [{
        ’type’: ’ford’,
        ’tint’: ’silver’,
        ’year’: ’2015’
    }, {
        ’type’: ’honda’,
        ’tint’: ’black’,
        ’year’: ’2012’
    }]
};
myData.dataD = {
    ’buildings’: [{
        ’houses’: [{
            ’streetName’: ’sycamore close’,
            ’number’: ’252’
        }, {
            ’streetName’: ’slimdon close’,
            ’number’: ’101’
        }]
    }]
};
console.log(myData); //object
var jsonData = JSON.stringify(myData);

console.log(jsonData);
/*
{"dataA":["a","b","c","d"],"dataB":{"animal":"cat","color":"brown"},"dataC":{"vehicles":[{"type":"ford","tint":"silver","year":"2015"},{"type":"honda","tint":"black","year":"2012"}]},"dataD":{"buildings":[{"houses":[{"streetName":"sycamore close","number":"252"},{"streetName":"slimdon close","number":"101"}]}]}}
 */</code></pre>

As an extra debugging tip, if you would like to pretty-print JSON in your console for easier reading, then the following extra arguments to <code>stringify()</code> will achieve this:

<pre><code class="language-javascript">JSON.stringify({ foo: "hello", bar: "world" }, null, 4);</code></pre>

### Problem 9

<strong>Problem:</strong> The namespacing pattern used is technically invalid.

<strong>Feedback:</strong> While namespacing is implemented correctly across the rest of the application, the initial check for namespace existence is invalid. Here’s what you currently have:

<pre><code class="language-javascript">if ( !MyNamespace ) {
  MyNamespace = { };
}</code></pre>

The problem is that <code>!MyNamespace</code> will throw a <code>ReferenceError</code>, because the <code>MyNamespace</code> variable was never declared. A better pattern would take advantage of boolean conversion with an inner variable declaration, as follows:

<pre><code class="language-javascript">if ( !MyNamespace ) {
  var MyNamespace = { };
}

//or
var myNamespace = myNamespace || {};

// Although a more efficient way of doing this is:
// myNamespace || ( myNamespace = {} );
// jsPerf test: https://jsperf.com/conditional-assignment

//or
if ( typeof MyNamespace == ’undefined’ ) {
  var MyNamespace = { };
}</code></pre>

This could, of course, be done in numerous other ways. If you’re interested in reading about more namespacing patterns (as well as some ideas on namespace extension), I recently wrote “<a href="https://addyosmani.com/blog/essential-js-namespacing/">Essential JavaScript Namespacing Patterns</a>.” <a href="https://twitter.com/kangax">Juriy Zaytsev</a> also has a pretty <a href="https://perfectionkills.com/unnecessarily-comprehensive-look-into-a-rather-insignificant-issue-of-global-objects-creation/">comprehensive post on namespacing patterns</a>.</p>

## Conclusion

That’s it. Reviewing code is a great way to enforce and maintain quality, correctness and consistency in coding standards at as high a level as possible. I strongly recommend that all developers give them a try in their daily projects, because they’re an excellent learning tool for both the developer and the reviewer. Until next time, try getting your code reviewed, and good luck with the rest of your project!

{{< signature "al, il" >}}

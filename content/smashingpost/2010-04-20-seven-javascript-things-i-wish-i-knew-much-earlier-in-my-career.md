---
title: 7 JavaScript Things I Wish I Knew Much Earlier In My Career
slug: seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5d358d5-97c3-4879-b1d1-a98213bba670/javascript-objects.png
date: 2010-04-20T13:21:58.000Z
author: christian-heilmann
summary: >-
  Do you feel like you’re wasting time learning the ins and outs of all of the browsers and working around their issues? Well Chris did, too. Doing this back then secured his career and ensured that he had a great job. But we shouldn’t have to go through this trial by fire any longer.
description: >-
  Do you feel like you’re wasting time learning the ins and outs of all of the browsers and working around their issues? Well Chris did, too. Doing this back then secured his career and ensured that he had a great job. But we shouldn’t have to go through this trial by fire any longer.
categories:
  - Coding
  - JavaScript
  - Career
---
I've been writing JavaScript code for much longer than I care to remember. I am very excited about the language’s recent success; it’s good to be a part of that success story. I've written dozens of articles, book chapters and one full book on the matter, and yet I keep finding new things. Here are some of the "aha!" moments I've had in the past, which you can try out rather than waiting for them to come to you by chance.

## Shortcut Notations

One of the things I love most about JavaScript now is shortcut notations to generate objects and arrays. So, in the past when we wanted to create an object, we wrote:

<pre><code class="language-javascript">var car = new Object();
car.colour = 'red';
car.wheels = 4;
car.hubcaps = 'spinning';
car.age = 4;</code></pre>

The same can be achieved with:

<pre><code class="language-javascript">var car = {
  colour:'red',
  wheels:4,
  hubcaps:'spinning',
  age:4
}</code></pre>

Much shorter, and you don’t need to repeat the name of the object. Right now, <code>car</code> is fine, but what happens when you use <code>invalidUserInSession</code>? The main gotcha in this notation is IE. Never ever leave a trailing comma before the closing curly brace or you’ll be in trouble.

The other handy shortcut notation is for arrays. The old school way of defining arrays was this:

<pre><code class="language-javascript">var moviesThatNeedBetterWriters = new Array(
  'Transformers','Transformers2','Avatar','Indiana Jones 4'
);</code></pre>

The shorter version of this is:

<pre><code class="language-javascript">var moviesThatNeedBetterWriters = [
  'Transformers','Transformers2','Avatar','Indiana Jones 4'
];</code></pre>

The other thing about arrays is that there is no such thing as an associative array. You will find a lot of code examples that define the above <code>car</code> example like so:

<pre><code class="language-javascript">var car = new Array();
car['colour'] = 'red';
car['wheels'] = 4;
car['hubcaps'] = 'spinning';
car['age'] = 4;</code></pre>

This is not Sparta; this is madness—don’t bother with this. "Associative arrays" is a confusing name for objects.

{{% feature-panel %}}

Another very cool shortcut notation is the ternary notation for conditions. So, instead of the following…

<pre><code class="language-javascript">var direction;
if(x &lt; 200){
  direction = 1;
} else {
  direction = -1;
}</code></pre>

… You could write a shorter version using the ternary notation:

<pre><code class="language-javascript">var direction = x &lt; 200 ? 1 : -1;</code></pre>

The <code>true</code> case of the condition is after the question mark, and the other case follows the colon.</p>

## JSON As A Data Format

Before I discovered JSON to store data, I did all kinds of crazy things to put content in a JavaScript-ready format: arrays, strings with control characters to split, and other abominations. The creation of <a href="https://json.org">JSON</a> by Douglas Crockford changed all that. Using JSON, you can store complex data in a format that is native to JavaScript and doesn’t need any extra conversion to be used immediately.

JSON is short for "JavaScript Object Notation" and uses both of the shortcuts we covered earlier.

{{% feature-panel %}}

So, if I wanted to describe a band, for example, I could do the following:

<pre><code class="language-javascript">var band = {
  "name":"The Red Hot Chili Peppers",
  "members":[
    {
      "name":"Anthony Kiedis",
      "role":"lead vocals"
    },
    {
      "name":"Michael 'Flea' Balzary",
      "role":"bass guitar, trumpet, backing vocals"
    }, 
    {
      "name":"Chad Smith",
      "role":"drums,percussion"
    },
    {
      "name":"John Frusciante",
      "role":"Lead Guitar"
    }
  ],
  "year":"2009"
}</code></pre>

You can use JSON directly in JavaScript and, when wrapped in a function call, even as a return format of APIs. This is called JSON-P and is supported by a lot of APIs out there. You can use a data endpoint, returning JSON-P directly in a script node:

<div class="break-out">

<pre><code class="language-javascript">&lt;div id="delicious"&gt;&lt;/div&gt;&lt;script&gt;
function delicious(o){
  var out = '&lt;ul&gt;';
  for(var i=0;i&lt;o.length;i++){
    out += '&lt;li&gt;&lt;a href="' + o[i].u + '"&gt;' + 
           o[i].d + '&lt;/a&gt;&lt;/li&gt;';
  }
  out += '&lt;/ul&gt;';
  document.getElementById('delicious').innerHTML = out;
}
&lt;/script&gt;
&lt;script src="https://feeds.delicious.com/v2/json/codepo8/javascript?count=15&amp;callback=delicious"&gt;&lt;/script&gt;</code></pre></div>

This calls the Delicious Web service to get my latest JavaScript bookmarks in JSON format and then displays them as an unordered list.

In essence, JSON is probably the most lightweight way of describing complex data—and it runs in a browser. You can even use it in PHP using the <code>json_decode()</code> function.</p>

{{% ad-panel-leaderboard %}}

## Native JavaScript Functions (Math, Array And String)

One thing that amazed me is how much easier my life got once I read up thoroughly on the math and string functions of JavaScript. You can use these to avoid a lot of looping and conditions. For example, when I had the task of finding the largest number in an array of numbers, I used to write a loop, like so:

<pre><code class="language-javascript">var numbers = [3,342,23,22,124];
var max = 0;
for(var i=0;i&lt;numbers.length;i++){
  if(numbers[i] &gt; max){
    max = numbers[i];
  }
}
alert(max);</code></pre>

This can be achieved without a loop:

<pre><code class="language-javascript">var numbers = [3,342,23,22,124];
numbers.sort(function(a,b){return b - a});
alert(numbers[0]);</code></pre>

Notice that you cannot use <code>sort()</code> on a number array because it sorts lexically. There’s a <a href="https://www.javascriptkit.com/javatutors/arraysort.shtml">good tutorial on <code>sort()</code> here</a> in case you need to know more.

Another interesting method is <code>Math.max()</code>. This one returns the largest number from a list of parameters:

<pre><code class="language-javascript">Math.max(12,123,3,2,433,4); // returns 433</code></pre>

Because this tests for numbers and returns the largest one, you can use it to test for browser support of certain properties:

<pre><code class="language-javascript">var scrollTop= Math.max(
 doc.documentElement.scrollTop,
 doc.body.scrollTop
);</code></pre>

This works around an Internet Explorer problem. You can read out the <code>scrollTop</code> of the current document, but depending on the <code>DOCTYPE</code> of the document, one or the other property is assigned the value. When you use <code>Math.max()</code> you get the right number because only one of the properties returns one; the other will be <code>undefined</code>. You can read more about shortening JavaScript with math functions <a href="https://www.wait-till-i.com/2007/06/28/shortening-javascripts-with-math/">here</a>.

Other very powerful functions to manipulate strings are <code>split()</code> and <code>join()</code>. Probably the most powerful example of this is writing a function to attach CSS classes to elements.

The thing is, when you add a class to a DOM element, you want to add it either as the first class or to already existing classes with a space in front of it. When you remove classes, you also need to remove the spaces (which was much more important in the past when some browsers failed to apply classes with trailing spaces).

So, the original function would be something like:

<pre><code class="language-javascript">function addclass(elm,newclass){
  var c = elm.className;
  elm.className = (c === ’) ? newclass : c+' '+newclass;
}</code></pre>

You can automate this using the <code>split()</code> and <code>join()</code> methods:

<pre><code class="language-javascript">function addclass(elm,newclass){
  var classes = elm.className.split(' ');
  classes.push(newclass);
  elm.className = classes.join(' ');
}</code></pre>

This automatically ensures that classes are space-separated and that yours gets tacked on at the end.

{{% ad-panel-leaderboard %}}

## Event Delegation

Events make Web apps work. I love events, especially custom events, which make your products extensible without your needing to touch the core code. The main problem (and actually one of its strengths) is that events are removed from the HTML—you apply an event listener to a certain element and then it becomes active. Nothing in the HTML indicates that this is the case though. Take this abstraction issue (which is hard for beginners to wrap their heads around) and the fact that "browsers" such as IE6 have all kind of memory problems and too many events applied to them, and you’ll see that not using too many event handlers in a document is wise.

This is where <span class="removed_link" title="https://icant.co.uk/sandbox/eventdelegation/">event delegation</span> comes in. When an event happens on a certain element and on all the elements above it in the DOM hierarchy, you can simplify your event handling by using a single handler on a parent element, rather than using a lot of handlers.

What do I mean by that? Say you want a list of links, and you want to call a function rather than load the links. The HTML would be:

<div class="break-out">

<pre><code class="language-javascript">&lt;h2&gt;Great Web resources&lt;/h2&gt;
&lt;ul id="resources"&gt;
  &lt;li&gt;&lt;a href="https://opera.com/wsc"&gt;Opera Web Standards Curriculum&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="https://sitepoint.com"&gt;Sitepoint&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="https://alistapart.com"&gt;A List Apart&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="https://yuiblog.com"&gt;YUI Blog&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="https://blameitonthevoices.com"&gt;Blame it on the voices&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="https://oddlyspecific.com"&gt;Oddly specific&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;</code></pre></div>

The normal way to apply event handlers here would be to loop through the links:

<pre><code class="language-javascript">// Classic event handling example
(function(){
  var resources = document.getElementById('resources');
  var links = resources.getElementsByTagName('a');
  var all = links.length;
  for(var i=0;i&lt;all;i++){
    // Attach a listener to each link
    links[i].addEventListener('click',handler,false);
  };
  function handler(e){
    var x = e.target; // Get the link that was clicked
    alert(x);
    e.preventDefault();
  };
})();</code></pre>

This could also be done with a single event handler:

<pre><code class="language-javascript">(function(){
  var resources = document.getElementById('resources');
  resources.addEventListener('click',handler,false);
  function handler(e){
    var x = e.target; // get the link tha
    if(x.nodeName.toLowerCase() === 'a'){
      alert('Event delegation:' + x);
      e.preventDefault();
    }
  };
})();</code></pre>

Because the click happens on all the elements in the list, all you need to do is compare the <code>nodeName</code> to the right element that you want to react to the event.

Disclaimer: while both of the event examples above work in browsers, they fail in IE6. For IE6, you need to apply an event model other than the W3C one, and this is why we use libraries for these tricks.

The benefits of this approach are more than just being able to use a single event handler. Say, for example, you want to add more links dynamically to this list. With event delegation, there is no need to change anything; with simple event handling, you would have to reassign handlers and re-loop the list.</p>

## Anonymous Functions And The Module Pattern

One of the most annoying things about JavaScript is that it has no scope for variables. Any variable, function, array or object you define that is not inside another function is global, which means that other scripts on the same page can access—and will usually override— them.

The workaround is to encapsulate your variables in an anonymous function and call that function immediately after you define it. For example, the following definition would result in three global variables and two global functions:

<pre><code class="language-javascript">var name = 'Chris';
var age = '34';
var status = 'single';
function createMember(){
  // [...]
}
function getMemberDetails(){
  // [...]
}</code></pre>

Any other script on the page that has a variable named <code>status</code> could cause trouble. If we wrap all of this in a name such as <code>myApplication</code>, then we work around that issue:

<pre><code class="language-javascript">var myApplication = function(){
  var name = 'Chris';
  var age = '34';
  var status = 'single';
  function createMember(){
    // [...]
  }
  function getMemberDetails(){
    // [...]
  }
}();</code></pre>

This, however, doesn’t do anything outside of that function. If this is what you need, then great. You may as well discard the name then:

<pre><code class="language-javascript">(function(){
  var name = 'Chris';
  var age = '34';
  var status = 'single';
  function createMember(){
    // [...]
  }
  function getMemberDetails(){
    // [...]
  }
})();</code></pre>

If you need to make some of the things reachable to the outside, then you need to change this. In order to reach <code>createMember()</code> or <code>getMemberDetails()</code>, you need to return them to the outside world to make them properties of <code>myApplication</code>:

<pre><code class="language-javascript">var myApplication = function(){
  var name = 'Chris';
  var age = '34';
  var status = 'single';
  return{
    createMember:function(){
      // [...]
    },
    getMemberDetails:function(){
      // [...]
    }
  }
}();
// myApplication.createMember() and 
// myApplication.getMemberDetails() now works.</code></pre>

This is called a module pattern or singleton. It was mentioned a lot by Douglas Crockford and is used very much in the <a href="https://yuilibrary.com/">Yahoo User Interface Library YUI</a>. What ails me about this is that I need to switch syntaxes to make functions or variables available to the outside world. Furthermore, if I want to call one method from another, I have to call it preceded by the <code>myApplication</code> name. So instead, I prefer simply to return pointers to the elements that I want to make public. This even allows me to shorten the names for outside use:

<pre><code class="language-javascript">var myApplication = function(){
  var name = 'Chris';
  var age = '34';
  var status = 'single';
  function createMember(){
    // [...]
  }
  function getMemberDetails(){
    // [...]
  }
  return{
    create:createMember,
    get:getMemberDetails
  }
}();
//myApplication.get() and myApplication.create() now work.</code></pre>

I've called this "<a href="https://www.wait-till-i.com/2007/08/22/again-with-the-module-pattern-reveal-something-to-the-world/">revealing module pattern</a>."

## Allowing For Configuration

Whenever I've written JavaScript and given it to the world, people have changed it, usually when they wanted it to do things that it couldn’t do out of the box—but also often because I made it too hard for people to change things.

The workaround is to add configuration objects to your scripts. I've <a href="https://www.wait-till-i.com/2008/05/23/script-configuration/">written about JavaScript configuration objects in detail</a>, but here’s the gist:

*   Have an object as part of your whole script called `configuration`.
*   In it, store all of the things that people will likely change when they use your script:
    *   CSS ID and class names;
    *   Strings (such as labels) for generated buttons;
    *   Values such as "number of images being displayed," "dimensions of map";
    *   Location, locale and language settings.
*   Return the object as a public property so that people can override it.

Most of the time you can do this as a last step in the coding process. I've put together an example in "<a href="https://www.wait-till-i.com/2008/02/07/five-things-to-do-to-a-script-before-handing-it-over-to-the-next-developer/">Five things to do to a script before handing it over to the next developer</a>."

In essence, you want to make it easy for people to use your code and alter it to their needs. If you do that, you are much less likely to get confusing emails from people who complain about your scripts and refer to changes that someone else actually did.</p>

## Interacting With The Back End

One of the main things I learned from all my years with JavaScript is that it is a great language with which to make interactive interfaces, but when it comes to crunching numbers and accessing data sources, it can be daunting.

Originally, I learned JavaScript to replace Perl because I was sick of copying things to a <code>cgi-bin</code> folder in order to make it work. Later on, I learned that making a back-end language do the main data churning for me, instead of trying to do all in JavaScript, makes more sense with regard to security and language.

If I access a Web service, I could get JSON-P as the returned format and do a lot of data conversion on the client, but why should I when I have a server that has a richer way of converting data and that can return the data as JSON or HTML… and cache it for me to boot?

So, if you want to use AJAX, learn about HTTP and about writing your own caching and conversion proxy. You will save a lot of time and nerves in the long run.</p>

## Browser-Specific Code Is A Waste Of Time. Use Libraries!

When I started Web development, the battle between using <code>document.all</code> and using <code>document.layers</code> as the main way to access the document was still raging. I chose <code>document.layers</code> because I liked the idea of any layer being its own document (and I had written more than enough <code>document.write</code> solutions to last a lifetime). The layer model failed, but so did <code>document.all</code>. When Netscape 6 went all out supporting only the W3C DOM model, I loved it, but end users didn’t care. End users just saw that this browser didn’t show the majority of the Internets correctly (although it did)—the code we produced was what was wrong. We built short-sighted code that supported a state-of-the-art environment, and the funny thing about the state of the art is that it is constantly changing.

I've wasted quite some time learning the ins and outs of all of the browsers and working around their issues. Doing this back then secured my career and ensured that I had a great job. But we shouldn’t have to go through this trial by fire any longer.

Libraries such as YUI, jQuery and Dojo are here to help us with this. They take on the problems of browsers by abstracting the pains of poor implementation, inconsistencies and flat-out bugs, and relieve us of the chore. Unless you want to beta test a certain browser because you’re a big fan, don’t fix browser issues in your JavaScript solutions, because you are unlikely to ever update the code to remove this fix. All you would be doing is adding to the already massive pile of outdated code on the Web.

That said, relying solely on libraries for your core skill is short-sighted. Read up on JavaScript, watch some good videos and tutorials on it, and understand the language. (Tip: closures are God’s gift to the JavaScript developer.) Libraries will help you build things quickly, but if you assign a lot of events and effects and need to add a class to every HTML element in the document, then you are doing it wrong.

## Resources

In addition to the resources mentioned in this article, also check out the following to learn more about JavaScript itself:

- [Douglas Crockford on JavaScript](https://javascript.crockford.com/)  
An in-depth video Lecture series.

### Related Posts

You may be interested in the following related posts:

- [The Seven Deadly Sins Of JavaScript Implementation](https://www.smashingmagazine.com/2010/02/22/the-seven-deadly-sins-of-javascript-implementation/)
- [Developing Sites With AJAX: Design Challenges and Common Issues](https://www.smashingmagazine.com/2010/02/10/some-things-you-should-know-about-ajax/)
- [45 Powerful CSS/JavaScript-Techniques](https://www.smashingmagazine.com/2010/01/12/45-powerful-css-javascript-techniques/)

{{< signature "al, il" >}}

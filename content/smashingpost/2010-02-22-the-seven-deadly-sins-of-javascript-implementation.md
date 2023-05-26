---
title: The Seven Deadly Sins Of JavaScript Implementation
slug: the-seven-deadly-sins-of-javascript-implementation
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aa11e86d-698e-44d4-b525-09359daa3e42/javascript2.jpg
date: 2010-02-22T12:45:40.000Z
author: christian-heilmann
description: >-
  Using JavaScript has become increasingly easy over the last few years. Whereas back in the day we needed to know the quirks of every browser, now many libraries such as jQuery, YUI, Dojo and MooTools allow someone who doesn't even know JavaScript to spruce up boring HTML documents with impressive and shiny effects. By piggy-backing on the CSS selector engine, we have moved away from the complexity and inconsistencies of the DOM and made things much easier.
categories:
  - Coding
  - JavaScript
---
If you look at some of the code that has been released, though, we do seem to have taken a step backwards. In gaining easier access, we also became a bit sloppy with our code. Finding clearly structured, easy-to-maintain jQuery code is quite tough, which is why many plug-ins do the same thing. Writing one yourself is faster than trying to fathom what other developers have done.

Be sure to check out the following articles:

*   [Seven JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)
*   [<span class="headline">JavaScript Events And Responding To The User</span>](https://www.smashingmagazine.com/2012/08/javascript-events-responding-user/)
*   [A Quick Look Into The Math Of Animations With JavaScript](https://www.smashingmagazine.com/2011/10/quick-look-math-animations-javascript/)

The <strong>rules for solid, maintainable and secure JavaScript</strong> haven't changed, though. So, let's run through the seven sins of JavaScript development that will bite you in the backside when you have to maintain the code later on or hand it over to another party.

{{% feature-panel %}}

We've all had to work with code written by other people. We have despaired over the lack of maintainability and documentation as well as weird logic. Funny enough, as developers, we started to see this as normal and got used to ignoring other people's work and instead writing new code for the same problems over and over, as if we were subconsciously trying to secure our jobs by leaving behind unmaintainable code—code that only we understood, while complaining that no good solutions were out there.</p>

## Sins Of Our Fathers: Browser-Specific Code

One of the main obstacles that kept us from evolving as developers was that JavaScript was largely browser-specific.

This was mainly because browsers did not support the standards (or were shipped before the governing bodies agreed on standards at all), and because we had to deliver our work before the competition and without extending the overly optimistic deadline set by our project managers.

This happens to be one reason why Internet Explorer 6 refuses to die. Hundreds of expensive software packages that are being used in offices worldwide were built when this browser was state of the art. This—and the monoculture that advocated using one software vendor for everything from the operating system to documents to spreadsheets to the browser—is the reason why companies now can't simply discontinue support for it. It also means that newer versions of IE will always have to support the rendering mistakes of IE6 in one way or another. IE6 is the Frankenstein of the Internet, haunting its creators, terribly misunderstood by the townsfolk, who would sooner kill it, burn it and dance around it than make any sense of it.

The good news is that you won't find many scripts these days that begin with <code>if(document.all){}</code> and continue with <code>else if(document.layers){}</code>. If you do find one, please send its creator a brief email encouraging them to move on or, better yet, to redirect their website to a better script that is actually being maintained.</p>

### Libraries to the Rescue

The job of JavaScript libraries such as jQuery, YUI, MooTools, Dojo and Glow is to make JavaScript development predictable and to relieve developers of the living hell that we call browser support. In other words, they fix random bugs in browsers and free us to adopt standards without worrying that certain browsers won't recognize them.

For example, the DOM method <code>getElementById(id)</code> should be straightforward: find the element with the ID <code>id</code> and return it. But because some versions of IE and Opera also return elements that have the <code>name</code> attribute of <code>id</code>, <a href="https://github.com/jquery/jquery/blob/master/src/core.js">jQuery solves the problem this way</a>:

<pre><code class="language-javascript">var elem;

elem = document.getElementById( match[2] );

if ( elem ) {
// Handle the case where IE and Opera return items
// by name instead of ID
if ( elem.id !== match[2] ) {
return rootjQuery.find( selector );
}

// Otherwise, we inject the element directly into the jQuery object
this.length = 1;
this[0] = elem;
}</code></pre>

This is where libraries are awfully useful and is why JavaScript libraries are here to stay. Browsers will always do things wrong, and old browsers will not be upgraded by end users, either because of the aforementioned company regulations or because people simply don't care to keep up with the times.

So, while the practice of building software for certain browsers is on the decline (at least for JavaScript—with CSS, we have a whole other headache ahead of us), we still have to be mindful of certain sins.</p>

## Sin #1: Not Playing Nice With Other Scripts

Here's the first one, which we still see a lot of on the Web. Sadly, it is very common in demo code for APIs and Web services: global variables, functions and DOM-1 event handlers.

What do I mean by these? Consider the following:

*   Every script in the HTML document has the same rights as the others and can, if need be, overwrite what other scripts have done before.
*   If you define a variable or function name, and some other include uses the same name, the initial one will be overwritten.
*   The same applies to event handlers if you attach them the old-school `onEvent` way.

Say you have the script <em>script_one.js</em>:

<pre><code class="language-javascript">x = 5;
function init(){
  alert('script one init');
  document.getElementsByTagName('h1')[0].onclick = function(){
    this.style.background = 'blue';
  }
}
alert('x is '+x);
window.onload = init;</code></pre>

And immediately after this one, you include another script, <em>script_two.js</em>:

<pre><code class="language-javascript">x = 10;
  function init(){
    alert('script two init');
    document.getElementsByTagName('h1')[0].onclick = function(){
      this.style.color = 'white';
    }
  }
  alert('x is '+x);
  window.onload = init;</code></pre>

If you open this document in a browser, you will find that x turns from 5 to 10 and that the first <code>init()</code> is never called. The <code>script two init alert()</code> does not come up, nor does the <code>h1</code> get a blue background when you click it. Only the text turns to white, which renders it invisible.

The solution is not to use <code>onEvent</code> handlers, but rather the proper DOM level 2 event handlers (they don't work in IE, but let's not worry about that at the moment—remember, this is what libraries are for). Furthermore, wrap your functions in another with a more unique name to prevent them from overriding each other.

<pre><code class="language-javascript">var scriptOne = function(){
  var x = 5;
  function init(){
    alert('script one init');
    document.getElementsByTagName('h1')[0].addEventListener(
      'click',
      function(e){
        var t = e.target;
        t.style.background = 'blue';
      },
      false
    );
  }
  alert('x inside is '+x);
  return {init:init};
}();
window.addEventListener('load',scriptOne.init,false);
alert('x outside is '+x);

var scriptTwo = function(){
  var x = 10;
  function init(){
    alert('script two init');
    document.getElementsByTagName('h1')[0].addEventListener(
      'click',
      function(e){
        var t = e.target;
        t.style.color = 'white';
      },
      false
    );
  }
  alert('x inside is '+x);
  return {init:init};
}();
window.addEventListener('load',scriptTwo.init,false);
alert('x outside is '+x);</code></pre>

If you run this in a browser (not Internet Explorer 6), everything will come up as you expect: x is first 5, then 10 on the inside, and the heading turns blue and white when you click it. Both <code>init()</code> functions are called, too.

You also get an error. Because <code>x</code> is not defined outside the functions, the <code>alert('x outside is '+x);</code> never works.

The reason is that by moving the <code>x</code> into the <code>scriptOne</code> and <code>scriptTwo</code> functions and adding the <code>var</code> keyword in front of them, we have made them a part of those functions but hid them from the outside world. This is called a closure and is <a href="https://developer.mozilla.org/en/Core_JavaScript_1.5_Guide/Working_with_Closures">explained in detail here</a>. It is probably the most powerful feature of JavaScript.

Using closures and <code>var</code> keywords, you won't have the problem of variables with similar names overriding each other. This also applies in jQuery: you should <a href="https://jquery-howto.blogspot.com/2009/01/namespace-your-javascript-function-and.html">namespace your functions</a>.

This can be tough to grasp, so let's look at a simpler example:

<pre><code class="language-javascript">var x = 4;
var f = 3;
var me = 'Chris';
function init(){}
function load(){}</code></pre>

All of these are global variables and functions now. Any other script having the same variables will override these.

You can nest them in an object to avoid this:

<pre><code class="language-javascript">var longerAndMoreDistinct = {
  x : 4,
  f : 3,
  me : 'Chris',
  init : function(){},
  load : function(){}
}</code></pre>

That way, only the <code>longerAndMoreDistinct</code> is global. If you want to run this function, you now have to call <code>longerAndMoreDistinct.init()</code> instead of <code>init()</code>. You can reach <code>me</code> as <code>longerAndMoreDistinct.me</code> and so on.

I don't like this because I have to switch from one notation to another. So, we can do the following:

<pre><code class="language-javascript">var longerAndMoreDistinct = function(){
  var x = 4;
  var f = 3;
  var me = 'Chris';
  function init(){}
  function load(){} 
}();</code></pre>

You define <code>longerAndMoreDistinct</code> as the outcome of a function without a name that gets immediately executed (this is the <code>()</code> on the last line). This now means that all of the variables and functions inside exist only in this world and cannot be accessed from outside at all. If you want to make them accessible from outside, you need to return them to the outside world:

<pre><code class="language-javascript">var longerAndMoreDistinct = function(){
  var x = 4;
  var f = 3;
  var me = 'Chris';
  function load(){}
  return {
    init:function(){}
  } 
}();</code></pre>

Now <code>init()</code> is available as <code>longerAndMoreDistinct.init()</code> again. This construct of wrapping things in an anonymous function and returning some of them is called the <a href="https://www.wait-till-i.com/2007/07/24/show-love-to-the-module-pattern/">Module pattern</a>, and it keeps your variables safe. Personally, I still hate the shift in syntax, so I came up with the <a href="https://www.wait-till-i.com/2007/08/22/again-with-the-module-pattern-reveal-something-to-the-world/">revealing module pattern</a>. Instead of returning the real function, all I do is return a pointer to it:

<pre><code class="language-javascript">var longerAndMoreDistinct = function(){
  var x = 4;
  var f = 3;
  var me = 'Chris';
  function load(){}
  function init(){}
  return {
    init:init
  } 
}();</code></pre>

This way, I can make things either available or not available simply by adding to the object that is returned.

If you don't need to give anything to the world and just want to run some code and keep all of your variables and function names safe, you can dispense with the name of the function:

<pre><code class="language-javascript">(function(){
  var x = 4;
  var f = 3;
  var me = 'Chris';
  function load(){}
  function init(){}
})();</code></pre>

Using <code>var</code> and wrapping code in this construct makes it inaccessible to the outside world, but still makes it execute.

You may find this to be complex stuff, but there is a good way to check your code. <a href="https://www.jslint.com/">JSLint</a> is a validator for JavaScript, much like the HTML or CSS validators, and it tells you all the things that might be wrong with your code.

## Sin #2: Believing Instead Of Testing

The next big sin related to implementing JavaScript is expecting everything to go right: every parameter being in the right format, every HTML element you try to enhance being truly available, and every end user entering information in the right format. This will never be the case, and that last assumption is an especially bad one because it allows malicious users to inject dangerous code.

When you write JavaScript and give it to the world or integrate it in a product that will be maintained by a third party, a little paranoia is a good thing.

<code>typeof</code> is your friend. Regular expressions are your friend. <code>indexOf()</code>, <code>split</code> and <code>length</code> are your friends. In other words, do everything you can to make sure that incoming data is the right format.

You will get a lot of errors with native JavaScript; if you do anything wrong, you'll know what happened. The annoying thing about most JavaScript libraries is that when they fail to execute some functionality, they do it silently. The maintainer is left guessing and has to run through all the code and start debugging with stop points (or—shudder!—<code>alerts()</code>) to reverse-engineer where you entered instable code. To avoid this, simply wrap whatever you can in a test case rather than try to access it.</p>

## Sin #3: Using The Wrong Technology For The Job

The biggest problem with JavaScript happens when you use the wrong tool for the job. It makes maintenance a nightmare and deteriorates the code's quality. Use tools for the jobs they were meant for. This means:

*   Absolutely essential content and mark-up should be in HTML, regardless of the environment it will be displayed in.
*   Any "look and feel" elements should be maintainable through CSS. You should not have to scour through JavaScript to change a color.
*   Any interaction with the user that goes beyond hover effects (which, by definition, are an _invitation_ to interact and not the interaction itself—because they are inaccessible to keyboard users) should be done with JavaScript.

The main reason why this is still a valid, pragmatic and sensible approach to development is that as Web technologies get muddled (for example, you can create content with CSS and JavaScript, animate and transform in CSS and—if you really want—paint with HTML), people's skills and interests in these different technologies vary quite a bit.

Semantic mark-up buffs are not much interested in applying closures in JavaScript. JavaScript developers are not much interested in the order of elements in CSS. And CSS fans aren't keen to learn how to make a JavaScript animation run flicker-free.

This results in the same problems being solved over and over again, only with different technologies. This is a market-wide problem: a lot of state-of-the-art Canvas tricks were done in Flash years ago, their impact debated and their problems fixed.

My favorite instance of this is when people write loops to hide a lot of elements on the page to make them available later on.

Say this is your HTML:

<pre><code class="language-javascript">&lt;h2&gt;Section 1&lt;/h2&gt;
&lt;div class="section"&gt;
  &lt;p&gt;Section 1 content&lt;/p&gt;
&lt;/div&gt;

&lt;h2&gt;Section 2&lt;/h2&gt;
&lt;div class="section"&gt;
  &lt;p&gt;Section 2 content&lt;/p&gt;
&lt;/div&gt;

&lt;h2&gt;Section 3&lt;/h2&gt;
&lt;div class="section"&gt;
  &lt;p&gt;Section 3 content&lt;/p&gt;
&lt;/div&gt;

&lt;h2&gt;Section 4&lt;/h2&gt;
&lt;div class="section"&gt;
  &lt;p&gt;Section 4 content&lt;/p&gt;
&lt;/div&gt;</code></pre>

The normal jQuery solution for this would be:

<pre><code class="language-javascript">$(document).ready(function(){
  $('.section').hide();
  $('h2').click(function(e){
    $(this).next().toggle();
  })
});</code></pre>

And then you realize that making the style of the current section deviate from that of the other sections would be great.

<pre><code class="language-javascript">$(document).ready(function(){
  $('.section').hide();
  $('h2').click(function(e){
    $(this).next().toggle();
    $(this).next().css('background','#ccc');
    $(this).next().css('border','1px solid #999');
    $(this).next().css('padding','5px');
  })
});</code></pre>

A few things are wrong with this. For starters, you've made it hard to maintain this by controlling the look and feel in JavaScript, not CSS (more on this later). Secondly, performance: while jQuery is amazingly speedy, a lot of code is still hidden under the hood in <code>$('.section').hide()</code>. The last, and very painful, performance issue is the copied and pasted lines that set the CSS. Don't ask jQuery to find the next sibling four times and do something to it. You could store the <code>next()</code> in a variable, but even that is not needed if you chain. If you really need to set a lot of CSS in jQuery, use a map:

<pre><code class="language-javascript">$(document).ready(function(){
  $('.section').hide();
  $('h2').click(function(e){
    $(this).next().toggle().css({
      'background':'#ffc',
      'border':'1px solid #999',
      'padding':'5px'
    });
  })
});</code></pre>

What if you then want to allow only one of them to be open at any time? Inexperienced developers would do something like this:

<pre><code class="language-javascript">$(document).ready(function(){
  $('.section').hide();
  $('h2').click(function(e){
    $('.section').hide();
    $(this).next().toggle().css({
      'background':'#ffc',
      'border':'1px solid #999',
      'padding':'5px'
    });
  })
});</code></pre>

This does the job, but you're looping around the document and accessing the DOM a lot, which is slow. You can alleviate this by keeping the current open section in a variable:

<pre><code class="language-javascript">$(document).ready(function(){
  var current = false;
  $('.section').hide();
  $('h2').click(function(e){
    if(current){
      current.hide();
    }
    current = $(this).next();
    current.toggle().css({
      'background':'#ffc',
      'border':'1px solid #999',
      'padding':'5px'
    });
  })
});</code></pre>

Predefine the current section as <code>false</code>, and set it when you click the first heading. You would then hide <code>current</code> only if it is true, thereby removing the need for another loop through all elements that have the class <code>section</code>.

But here is the interesting thing: if all you want is to show and hide sections, you don't need any looping at all! CSS already goes through the document when it renders and applies classes. You just need to give the CSS engine something to hang on to, such as a class for the <code>body</code>:

<pre><code class="language-javascript">$(document).ready(function(){
  $('body').addClass('js');
  var current = null;
  $('h2').click(function(e){
    if(current){
      current.removeClass('current');
    }
    current = $(this).next().addClass('current');
  })
});</code></pre>

By adding the class <code>js</code> to the body of the document and toggling the class <code>current</code> for the current section, you maintain control of the look and feel in CSS:

<pre><code class="language-javascript">&lt;style type="text/css" media="screen"&gt;
  .section{
    border:1px solid #999;
    background:#ccc;
  }
  .js .section{
    display:none;
  }
  .js .current{
    display:block;
    border:1px solid #999;
    background:#ffc;
  }
&lt;/style&gt;</code></pre>

The beauty of this is that the handle will be re-usable by the CSS designer and maintainer. Anything without the <code>.js</code> selector would be the non-scripting-enabled version of a part of the document, and anything with the <code>.js</code> selector is applied only when JavaScript is available. And yes, you should think about the case when it is not.</p>

## Sin #4: Depending On JavaScript And Certain Input Devices

There is quite a discussion about the need to consider non-JavaScript environments in this day and age, but here is a fact: JavaScript can be turned off, and any JavaScript could break the page for the other scripts that are included. Given the flakiness of code out there that may be running alongside yours and the instability of wireless and mobile connections, I for one want to build one thing: <strong>code that works</strong>.

So, making sure that the most basic usage of your product does not depend on JavaScript is not just nice to have but essential if you expect people to actually use the product.

Absolutely nothing is wrong with using JavaScript heavily. On the contrary, it makes the Web much smoother and saves us a lot of time if done right. But you should never promise functionality that doesn't work. And if you rely on JavaScript, this is exactly what you're doing. I've already covered the effects of bad JavaScript in detail in the <a href="https://www.smashingmagazine.com/2010/02/10/some-things-you-should-know-about-ajax/">AJAX</a>, <a href="https://www.smashingmagazine.com/2010/01/21/find-the-right-javascript-solution-with-a-7-step-test/">JavaScript testing</a> and <a href="https://www.smashingmagazine.com/2010/01/14/web-security-primer-are-you-part-of-the-problem/">security</a> articles here on Smashing Magazine, but once again here are some simple steps you can take to make sure you don't break your promise to end users:

*   Anything vital to the functionality of your product should not require JavaScript. Forms, links and server-side validation and re-direct scripts are your friends.
*   If something depends on JavaScript, build it with JavaScript and add it to the document using the DOM or the equivalent method in your library of choice.
*   If you add JavaScript functionality, make sure it works with the keyboard and mouse. Click and submit handlers are bullet-proof, whereas key and mouse events are flaky and don't work on mobile devices.
*   By writing clever back-end code that recognizes when data is required by JavaScript rather than building APIs that render HTML, you avoid having to do double-maintenance, which is an argument that many of the "Everyone enables JavaScript" zealots bring up a lot. For proof of this, check out the [presentation on building Web applications using YQL and YUI](https://www.yuiblog.com/blog/2010/02/11/video-heilmann-yql/) that I gave a few weeks ago (video in English and German).</p>

### When JavaScript Dependence Is Okay (to a Degree)

A lot of misunderstanding about JavaScript dependence stems from people making blanket statements based on the environments they work in.

If you are a Google engineer working on Gmail, you would be hard pressed to think of why you would even bother working without JavaScript. The same goes for widget developers who work on OpenSocial widgets, mobile applications, Apple widgets and Adobe Air. In other words, if your environment already depends on JavaScript, then by all means don't bother with a fall-back.

But do not take these closed environments and edge-case applications as the standard by which we should be measuring JavaScript. JavaScript's greatest power and greatest problem is its versatility. Saying that all websites can stand JavaScript because Gmail needs it is like saying that all cars should have a start button because they work great in Hybrids, or that hybrid cars should have massive tanks and cow catchers because they work great on Hummers. The technical feature set of a product depends on its implementation and target market. Different applications have different base functionality that needs to be satisfied in order to reach the largest audience and not block people out.</p>

### Consider the Use Cases and Maintenance

One fascinating aspect of JavaScript-dependent code is that, in many cases, people have simply not considered all the use cases (here's a great example). Take the following HTML:

<pre><code class="language-javascript">&lt;form action="#" id="f"&gt;
  &lt;div&gt;
    &lt;label for="search"&gt;Search&lt;/label&gt;
    &lt;input type="text" value="kittens" id="search"&gt;
    &lt;input type="submit" id="s" value="go"&gt;
  &lt;/div&gt;
&lt;/form&gt;
&lt;div id="results"&gt;&lt;/div&gt;</code></pre>

Without JavaScript, this does nothing whatsoever. There is no sensible <code>action</code> attribute, and the text field has no <code>name</code> attribute. So, even when you send the form off, the server won't get the information that the user has entered.

Using jQuery and a JSON data source such as <a href="https://developer.yahoo.com/yql">YQL</a>, you can do a pure JavaScript search with this:

<pre><code class="language-javascript">$('#s').click(function(event){
  event.preventDefault();
  $('&lt;ul/&gt;').appendTo('#results');
  var url =
  $.getJSON('https://query.yahooapis.com/v1/public/yql?'+
            'q=select%20abstract%2Cclickurl%2Cdispurl%2Ctitle%20'+
            'from%20search.web%20where%20query%3D%22'+
            $('#search').val() + '%22&amp;format=json&amp;'+
            'callback=?',
    function(data){
      $.each(data.query.results.result,
        function(i,item){
          $('&lt;li&gt;&lt;h3&gt;&lt;a href="'+item.clickurl+'"&gt;'+
             item.title+' ('+item.dispurl+')&lt;/a&gt;&lt;/h3&gt;&lt;p&gt;'+
             (item.abstract || ’) +'&lt;/p&gt;&lt;/li&gt;').
            appendTo("#results ul");
        });
    });
});</code></pre>

This works… unless of course you are like me and prefer to send forms by hitting "Enter" rather than clicking the "Submit" button. Unless I tab through the whole form and focus on the "Submit" button, I get nothing.

So, that's the first thing to fix. If you create forms, never use a click handler on the button. Instead, use the submit event of the form. This catches both the clicking "Submit" and hitting "Enter" cases. With one change, you now support all of the keyboard users out there, and the whole change is contained in the first line:

<pre><code class="language-javascript">$('#f').submit(function(event){
  event.preventDefault();
  $('&lt;ul/&gt;').appendTo('#results');
  var url =
  $.getJSON('https://query.yahooapis.com/v1/public/yql?'+
            'q=select%20abstract%2Cclickurl%2Cdispurl%2Ctitle%20'+
            'from%20search.web%20where%20query%3D%22'+
            $('#search').val() + '%22&amp;format=json&amp;'+
            'callback=?',
    function(data){
      $.each(data.query.results.result,
        function(i,item){
          $('&lt;li&gt;&lt;h3&gt;&lt;a href="'+item.clickurl+'"&gt;'+
             item.title+' ('+item.dispurl+')&lt;/a&gt;&lt;/h3&gt;&lt;p&gt;'+
             (item.abstract || ’) +'&lt;/p&gt;&lt;/li&gt;').
            appendTo("#results ul");
        });
    });
});</code></pre>

We've now covered the first case. But without JavaScript, the form still doesn't do anything. And another problem brings us to the next sin of writing JavaScript.</p>

## Sin #5: Making Maintenance Unnecessarily Hard

One thing that keeps great code off the Web is that our work environment, deadlines and hiring practices condition developers to build code for quick release, without considering how difficult maintaining that code will be later on. I once called JavaScript the village bicycle of Web design (<a href="https://www.slideshare.net/cheilmann/fronteers-maintainability-presentation">slides here</a>): anyone can go for a ride. Because the code is available in the open, future maintainers will be able to mess around with it and extend it any way they like.

The sad thing is that the harder your code is to maintain, the more errors will be added to it, leading it to look more like alphabet soup than organized script.

Take the above example. Those of you who haven't worked with <a href="https://developer.yahoo.com/yql">YQL</a> and JSON-P for cross-domain AJAX undoubtedly had a "What?" moment looking at the code. Furthermore, keeping a lot of HTML in JavaScript easy to follow is hard, and guess what is the first thing to change when a new design for the page comes along? Exactly: the HTML and CSS. So, to make it easier to maintain, I for one would shift all of the work to the back end, thus making the form work without JavaScript and keeping maintenance of all the HTML in the same document:

<pre><code class="language-javascript">&lt;?php
if(isset($_GET['search'])){
  $search = filter_input(INPUT_GET, 'search', FILTER_SANITIZE_ENCODED);
  $data = getdata($search);
  if($data-&gt;query-&gt;results){

    $out = '&lt;ul&gt;';

    foreach($data-&gt;query-&gt;results-&gt;result as $r){

      $out .= "&lt;li&gt;
                 &lt;h3&gt;
                   &lt;a href="{$r-&gt;clickurl}"&gt;{$r-&gt;title}   
                     &lt;span&gt;({$r-&gt;dispurl})&lt;/span&gt;
                   &lt;/a&gt;
                 &lt;/h3&gt;
                 &lt;p&gt;{$r-&gt;abstract}&lt;/p&gt;
               &lt;/li&gt;";
    }

    $out .= '&lt;/ul&gt;';

  } else {

    $out = '&lt;h3&gt;Error: could not find any results&lt;/h3&gt;';

  }
}

if($_SERVER['HTTP_X_REQUESTED_WITH']!=’){
  echo $out;
  die();
}
?&gt;
&lt;!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
 "https://www.w3.org/TR/html4/strict.dtd"&gt;
&lt;html&gt;
&lt;head&gt;
  &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8"&gt; 
  &lt;title&gt;Ajax Search with PHP API&lt;/title&gt;
  &lt;link rel="stylesheet" href="styles.css" type="text/css"&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;form action="independent.php" id="f"&gt;
    &lt;div&gt;
      &lt;label for="search"&gt;Search&lt;/label&gt;
      &lt;input type="text" value="kittens" name="search" id="search"&gt;
      &lt;input type="submit" id="s" value="Go"&gt;
    &lt;/div&gt;
  &lt;/form&gt;
  &lt;div id="results"&gt;&lt;?php if($out!=’){echo $out;}?&gt;&lt;/div&gt;
  &lt;script src="jquery.js"&gt;&lt;/script&gt;
  &lt;script src="ajaxform.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
&lt;?php
function getdata($search){
  $url = 'https://query.yahooapis.com/v1/public/yql?'.
         'q=select%20abstract%2Cclickurl%2Cdispurl%2Ctitle%20'.
         'from%20search.web%20where%20query%3D%22'.$search.'%22'.
         '&amp;format=json';
  $ch = curl_init();
  curl_setopt($ch, CURLOPT_URL, $url);
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
  $output = curl_exec($ch);
  curl_close($ch);
  $data = json_decode($output);
  return $data;
}
?&gt;</code></pre>

Someone who doesn't understand PHP at all should still be able to change the HTML display without breaking the code. With this in place, the JavaScript boils down to a very simple script:

<pre><code class="language-javascript">$('#f').submit(function(event){
  event.preventDefault();
  $.get('independent.php?search=' + $('#search').val(),
    function(data) {
      $('#results').html(data);
    }
  );
});</code></pre>

The normal way to make code more maintainable is to move everything that is likely to change away from the main functional part of the script into a configuration object at the very top of the script. You can return this as an object to the outside world to allow people to set it before they initialize the main functionality.

So, one change we can make to our earlier example—albeit a small one now, but that can change quickly when more requirements come in—is to have a configuration section right up front that defines the CSS classes in use:

<pre><code class="language-javascript">$(document).ready(function(){
  /* Configuration object - change classes, IDs and string here */
  var config = {
  /* CSS classes that get applied dynamically */
    javascriptenabled:'js',
    currentsection:'current'
  }

  /* functionality starts here */
  $('body').addClass(config.javascriptenabled);
  var current = null;
  $('h2').click(function(e){
    if(current){
      current.removeClass(config.currentsection);
    }
    current = $(this).next().addClass(config.currentsection);
  })
});</code></pre>

For more information on configuration objects and why they rock for maintenance, check out the blog post "<a href="https://www.wait-till-i.com/2008/05/23/script-configuration/">Providing Script Configuration Inline and Programatically</a>".

In summary, go over your code once more when you think you've finished with it and the next person is about to take it over.</p>

## Sin #6: Not Documenting Your Code

"Good code documents itself" is a terribly common and misguided belief. In my years as a developer, I've found that my style of coding has changed constantly. What was common knowledge and best practice in 2004 might be forgotten or even considered poor style these days.

&lt;h2&gt;Section 2&lt;/h2&gt;
&lt;div class="section"&gt;
  &lt;p&gt;Section 2 content&lt;/p&gt;
&lt;/div&gt;

&lt;h2&gt;Section 3&lt;/h2&gt;
&lt;div class="section"&gt;
  &lt;p&gt;Section 3 content&lt;/p&gt;
&lt;/div&gt;

&lt;h2&gt;Section 4&lt;/h2&gt;
&lt;div class="section"&gt;
  &lt;p&gt;Section 4 content&lt;/p&gt;
&lt;/div&gt;</code></pre>

The normal jQuery solution for this would be:

<pre><code class="language-javascript">$(document).ready(function(){
  $('.section').hide();
  $('h2').click(function(e){
    $(this).next().toggle();
  })
});</code></pre>

And then you realize that making the style of the current section deviate from that of the other sections would be great.

<pre><code class="language-javascript">$(document).ready(function(){
  $('.section').hide();
  $('h2').click(function(e){
    $(this).next().toggle();
    $(this).next().css('background','#ccc');
    $(this).next().css('border','1px solid #999');
    $(this).next().css('padding','5px');
  })
});</code></pre>

A few things are wrong with this. For starters, you've made it hard to maintain this by controlling the look and feel in JavaScript, not CSS (more on this later). Secondly, performance: while jQuery is amazingly speedy, a lot of code is still hidden under the hood in <code>$('.section').hide()</code>. The last, and very painful, performance issue is the copied and pasted lines that set the CSS. Don't ask jQuery to find the next sibling four times and do something to it. You could store the <code>next()</code> in a variable, but even that is not needed if you chain. If you really need to set a lot of CSS in jQuery, use a map:

<pre><code class="language-javascript">$(document).ready(function(){
  $('.section').hide();
  $('h2').click(function(e){
    $(this).next().toggle().css({
      'background':'#ffc',
      'border':'1px solid #999',
      'padding':'5px'
    });
  })
});</code></pre>

What if you then want to allow only one of them to be open at any time? Inexperienced developers would do something like this:

<pre><code class="language-javascript">$(document).ready(function(){
  $('.section').hide();
  $('h2').click(function(e){
    $('.section').hide();
    $(this).next().toggle().css({
      'background':'#ffc',
      'border':'1px solid #999',
      'padding':'5px'
    });
  })
});</code></pre>

This does the job, but you're looping around the document and accessing the DOM a lot, which is slow. You can alleviate this by keeping the current open section in a variable:

<pre><code class="language-javascript">$(document).ready(function(){
  var current = false;
  $('.section').hide();
  $('h2').click(function(e){
    if(current){
      current.hide();
    }
    current = $(this).next();
    current.toggle().css({
      'background':'#ffc',
      'border':'1px solid #999',
      'padding':'5px'
    });
  })
});</code></pre>

Predefine the current section as <code>false</code>, and set it when you click the first heading. You would then hide <code>current</code> only if it is true, thereby removing the need for another loop through all elements that have the class <code>section</code>.

But here is the interesting thing: if all you want is to show and hide sections, you don't need any looping at all! CSS already goes through the document when it renders and applies classes. You just need to give the CSS engine something to hang on to, such as a class for the <code>body</code>:

<pre><code class="language-javascript">$(document).ready(function(){
  $('body').addClass('js');
  var current = null;
  $('h2').click(function(e){
    if(current){
      current.removeClass('current');
    }
    current = $(this).next().addClass('current');
  })
});</code></pre>

By adding the class <code>js</code> to the body of the document and toggling the class <code>current</code> for the current section, you maintain control of the look and feel in CSS:

<pre><code class="language-javascript">&lt;style type="text/css" media="screen"&gt;
  .section{
    border:1px solid #999;
    background:#ccc;
  }
  .js .section{
    display:none;
  }
  .js .current{
    display:block;
    border:1px solid #999;
    background:#ffc;
  }
&lt;/style&gt;</code></pre>

The beauty of this is that the handle will be re-usable by the CSS designer and maintainer. Anything without the <code>.js</code> selector would be the non-scripting-enabled version of a part of the document, and anything with the <code>.js</code> selector is applied only when JavaScript is available. And yes, you should think about the case when it is not.</p>

## Sin #4: Depending On JavaScript And Certain Input Devices

There is quite a discussion about the need to consider non-JavaScript environments in this day and age, but here is a fact: JavaScript can be turned off, and any JavaScript could break the page for the other scripts that are included. Given the flakiness of code out there that may be running alongside yours and the instability of wireless and mobile connections, I for one want to build one thing: <strong>code that works</strong>.

So, making sure that the most basic usage of your product does not depend on JavaScript is not just nice to have but essential if you expect people to actually use the product.

Absolutely nothing is wrong with using JavaScript heavily. On the contrary, it makes the Web much smoother and saves us a lot of time if done right. But you should never promise functionality that doesn't work. And if you rely on JavaScript, this is exactly what you're doing. I've already covered the effects of bad JavaScript in detail in the <a href="https://www.smashingmagazine.com/2010/02/10/some-things-you-should-know-about-ajax/">AJAX</a>, <a href="https://www.smashingmagazine.com/2010/01/21/find-the-right-javascript-solution-with-a-7-step-test/">JavaScript testing</a> and <a href="https://www.smashingmagazine.com/2010/01/14/web-security-primer-are-you-part-of-the-problem/">security</a> articles here on Smashing Magazine, but once again here are some simple steps you can take to make sure you don't break your promise to end users:

*   Anything vital to the functionality of your product should not require JavaScript. Forms, links and server-side validation and re-direct scripts are your friends.
*   If something depends on JavaScript, build it with JavaScript and add it to the document using the DOM or the equivalent method in your library of choice.
*   If you add JavaScript functionality, make sure it works with the keyboard and mouse. Click and submit handlers are bullet-proof, whereas key and mouse events are flaky and don't work on mobile devices.
*   By writing clever back-end code that recognizes when data is required by JavaScript rather than building APIs that render HTML, you avoid having to do double-maintenance, which is an argument that many of the "Everyone enables JavaScript" zealots bring up a lot. For proof of this, check out the [presentation on building Web applications using YQL and YUI](https://www.yuiblog.com/blog/2010/02/11/video-heilmann-yql/) that I gave a few weeks ago (video in English and German).</p>

### When JavaScript Dependence Is Okay (to a Degree)

A lot of misunderstanding about JavaScript dependence stems from people making blanket statements based on the environments they work in.

If you are a Google engineer working on Gmail, you would be hard pressed to think of why you would even bother working without JavaScript. The same goes for widget developers who work on OpenSocial widgets, mobile applications, Apple widgets and Adobe Air. In other words, if your environment already depends on JavaScript, then by all means don't bother with a fall-back.

But do not take these closed environments and edge-case applications as the standard by which we should be measuring JavaScript. JavaScript's greatest power and greatest problem is its versatility. Saying that all websites can stand JavaScript because Gmail needs it is like saying that all cars should have a start button because they work great in Hybrids, or that hybrid cars should have massive tanks and cow catchers because they work great on Hummers. The technical feature set of a product depends on its implementation and target market. Different applications have different base functionality that needs to be satisfied in order to reach the largest audience and not block people out.</p>

### Consider the Use Cases and Maintenance

One fascinating aspect of JavaScript-dependent code is that, in many cases, people have simply not considered all the use cases (here's a great example). Take the following HTML:

<pre><code class="language-javascript">&lt;form action="#" id="f"&gt;
  &lt;div&gt;
    &lt;label for="search"&gt;Search&lt;/label&gt;
    &lt;input type="text" value="kittens" id="search"&gt;
    &lt;input type="submit" id="s" value="go"&gt;
  &lt;/div&gt;
&lt;/form&gt;
&lt;div id="results"&gt;&lt;/div&gt;</code></pre>

Without JavaScript, this does nothing whatsoever. There is no sensible <code>action</code> attribute, and the text field has no <code>name</code> attribute. So, even when you send the form off, the server won't get the information that the user has entered.

Using jQuery and a JSON data source such as <a href="https://developer.yahoo.com/yql">YQL</a>, you can do a pure JavaScript search with this:

<pre><code class="language-javascript">$('#s').click(function(event){
  event.preventDefault();
  $('&lt;ul/&gt;').appendTo('#results');
  var url =
  $.getJSON('https://query.yahooapis.com/v1/public/yql?'+
            'q=select%20abstract%2Cclickurl%2Cdispurl%2Ctitle%20'+
            'from%20search.web%20where%20query%3D%22'+
            $('#search').val() + '%22&amp;format=json&amp;'+
            'callback=?',
    function(data){
      $.each(data.query.results.result,
        function(i,item){
          $('&lt;li&gt;&lt;h3&gt;&lt;a href="'+item.clickurl+'"&gt;'+
             item.title+' ('+item.dispurl+')&lt;/a&gt;&lt;/h3&gt;&lt;p&gt;'+
             (item.abstract || ’) +'&lt;/p&gt;&lt;/li&gt;').
            appendTo("#results ul");
        });
    });
});</code></pre>

This works… unless of course you are like me and prefer to send forms by hitting "Enter" rather than clicking the "Submit" button. Unless I tab through the whole form and focus on the "Submit" button, I get nothing.

So, that's the first thing to fix. If you create forms, never use a click handler on the button. Instead, use the submit event of the form. This catches both the clicking "Submit" and hitting "Enter" cases. With one change, you now support all of the keyboard users out there, and the whole change is contained in the first line:

<pre><code class="language-javascript">$('#f').submit(function(event){
  event.preventDefault();
  $('&lt;ul/&gt;').appendTo('#results');
  var url =
  $.getJSON('https://query.yahooapis.com/v1/public/yql?'+
            'q=select%20abstract%2Cclickurl%2Cdispurl%2Ctitle%20'+
            'from%20search.web%20where%20query%3D%22'+
            $('#search').val() + '%22&amp;format=json&amp;'+
            'callback=?',
    function(data){
      $.each(data.query.results.result,
        function(i,item){
          $('&lt;li&gt;&lt;h3&gt;&lt;a href="'+item.clickurl+'"&gt;'+
             item.title+' ('+item.dispurl+')&lt;/a&gt;&lt;/h3&gt;&lt;p&gt;'+
             (item.abstract || ’) +'&lt;/p&gt;&lt;/li&gt;').
            appendTo("#results ul");
        });
    });
});</code></pre>

We've now covered the first case. But without JavaScript, the form still doesn't do anything. And another problem brings us to the next sin of writing JavaScript.</p>

## Sin #5: Making Maintenance Unnecessarily Hard

One thing that keeps great code off the Web is that our work environment, deadlines and hiring practices condition developers to build code for quick release, without considering how difficult maintaining that code will be later on. I once called JavaScript the village bicycle of Web design (<a href="https://www.slideshare.net/cheilmann/fronteers-maintainability-presentation">slides here</a>): anyone can go for a ride. Because the code is available in the open, future maintainers will be able to mess around with it and extend it any way they like.

The sad thing is that the harder your code is to maintain, the more errors will be added to it, leading it to look more like alphabet soup than organized script.

Take the above example. Those of you who haven't worked with <a href="https://developer.yahoo.com/yql">YQL</a> and JSON-P for cross-domain AJAX undoubtedly had a "What?" moment looking at the code. Furthermore, keeping a lot of HTML in JavaScript easy to follow is hard, and guess what is the first thing to change when a new design for the page comes along? Exactly: the HTML and CSS. So, to make it easier to maintain, I for one would shift all of the work to the back end, thus making the form work without JavaScript and keeping maintenance of all the HTML in the same document:

<pre><code class="language-javascript">&lt;?php
if(isset($_GET['search'])){
  $search = filter_input(INPUT_GET, 'search', FILTER_SANITIZE_ENCODED);
  $data = getdata($search);
  if($data-&gt;query-&gt;results){

    $out = '&lt;ul&gt;';

    foreach($data-&gt;query-&gt;results-&gt;result as $r){

      $out .= "&lt;li&gt;
                 &lt;h3&gt;
                   &lt;a href="{$r-&gt;clickurl}"&gt;{$r-&gt;title}   
                     &lt;span&gt;({$r-&gt;dispurl})&lt;/span&gt;
                   &lt;/a&gt;
                 &lt;/h3&gt;
                 &lt;p&gt;{$r-&gt;abstract}&lt;/p&gt;
               &lt;/li&gt;";
    }

    $out .= '&lt;/ul&gt;';

  } else {

    $out = '&lt;h3&gt;Error: could not find any results&lt;/h3&gt;';

  }
}

if($_SERVER['HTTP_X_REQUESTED_WITH']!=’){
  echo $out;
  die();
}
?&gt;
&lt;!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
 "https://www.w3.org/TR/html4/strict.dtd"&gt;
&lt;html&gt;
&lt;head&gt;
  &lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8"&gt; 
  &lt;title&gt;Ajax Search with PHP API&lt;/title&gt;
  &lt;link rel="stylesheet" href="styles.css" type="text/css"&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;form action="independent.php" id="f"&gt;
    &lt;div&gt;
      &lt;label for="search"&gt;Search&lt;/label&gt;
      &lt;input type="text" value="kittens" name="search" id="search"&gt;
      &lt;input type="submit" id="s" value="Go"&gt;
    &lt;/div&gt;
  &lt;/form&gt;
  &lt;div id="results"&gt;&lt;?php if($out!=’){echo $out;}?&gt;&lt;/div&gt;
  &lt;script src="jquery.js"&gt;&lt;/script&gt;
  &lt;script src="ajaxform.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
&lt;?php
function getdata($search){
  $url = 'https://query.yahooapis.com/v1/public/yql?'.
         'q=select%20abstract%2Cclickurl%2Cdispurl%2Ctitle%20'.
         'from%20search.web%20where%20query%3D%22'.$search.'%22'.
         '&amp;format=json';
  $ch = curl_init();
  curl_setopt($ch, CURLOPT_URL, $url);
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
  $output = curl_exec($ch);
  curl_close($ch);
  $data = json_decode($output);
  return $data;
}
?&gt;</code></pre>

Someone who doesn't understand PHP at all should still be able to change the HTML display without breaking the code. With this in place, the JavaScript boils down to a very simple script:

<pre><code class="language-javascript">$('#f').submit(function(event){
  event.preventDefault();
  $.get('independent.php?search=' + $('#search').val(),
    function(data) {
      $('#results').html(data);
    }
  );
});</code></pre>

The normal way to make code more maintainable is to move everything that is likely to change away from the main functional part of the script into a configuration object at the very top of the script. You can return this as an object to the outside world to allow people to set it before they initialize the main functionality.

So, one change we can make to our earlier example—albeit a small one now, but that can change quickly when more requirements come in—is to have a configuration section right up front that defines the CSS classes in use:

<pre><code class="language-javascript">$(document).ready(function(){
  /* Configuration object - change classes, IDs and string here */
  var config = {
  /* CSS classes that get applied dynamically */
    javascriptenabled:'js',
    currentsection:'current'
  }

  /* functionality starts here */
  $('body').addClass(config.javascriptenabled);
  var current = null;
  $('h2').click(function(e){
    if(current){
      current.removeClass(config.currentsection);
    }
    current = $(this).next().addClass(config.currentsection);
  })
});</code></pre>

For more information on configuration objects and why they rock for maintenance, check out the blog post "<a href="https://www.wait-till-i.com/2008/05/23/script-configuration/">Providing Script Configuration Inline and Programatically</a>".

In summary, go over your code once more when you think you've finished with it and the next person is about to take it over.</p>

## Sin #6: Not Documenting Your Code

"Good code documents itself" is a terribly common and misguided belief. In my years as a developer, I've found that my style of coding has changed constantly. What was common knowledge and best practice in 2004 might be forgotten or even considered poor style these days.

Documenting all of the tricks and workarounds we do to make our code work in different browsers is definitely a good idea. This allows future maintainers to remove them when the targeted browser version becomes obsolete or a library function fixes the issue.

Commenting your code also allows the maintainer to trace it back to you should they need some piece of information, and it allows people who have stumbled across your script to include it in a larger solution or library (which has happened to me). Because JavaScripts tend replicate on the Web (in all of those blogs and "script collections"), it is also a way to make your name known.

Don't go overboard with commenting, though. Obvious things don't need to be spelled out. I have found the following situations worthy of comment:

*   **Necessary hacks**.  Browser hacks; content clean-up; things that should be supported server-side but are not yet.
*   **Sections that are likely to change**.  Timely solutions; IDs, classes and strings (as explained earlier).
*   **Start of classes and reusable functions**.  With name, author, version, date and license.
*   **Third-party code**.  Give credit where credit is due.
*   **Sections with dependencies**.  Some comment like, "Needs the Google API with an own key—this one will not work on your server."

In short, comment on anything that deviates from the normal flow of coding. I tend to use <code>/* */</code> instead of <code>//</code> because it won't create a bug if people remove the line break by accident.</p>

### Special Case: Commenting Out Code

One special case is commenting out sections that will be necessary in future releases or that depend on functionality not currently available. This can be amazingly useful but also a security risk, depending on what you're commenting out. For example, don't leave in any code that points to server-side APIs that are not available yet but could at any time be half-implemented. I've seen this before, where administrator links with the full unprotected path were commented out in the HTML.

Still, commenting out can be very useful for debugging. One neat trick is the following:

<pre><code class="language-javascript">/*

myFunction('do something');

// */</code></pre>

This is now commented out. But by adding a single slash in front of the first comment line, you will uncomment the whole block and make it live.

<pre><code class="language-javascript">//*

myFunction('do something');

// */</code></pre>

This trick makes it awfully easy to toggle whole blocks.</p>

## Sin #7: Optimizing For Machines, Not People

The last sin is over-optimizing JavaScript based on the scads of information about performance that are available to us. You will find a lot of information on the Web about optimizing JavaScript for performance in the current browser environment. Notice that "current browser environment"—much information is browser- and version-specific and a necessary evil for now, but not necessarily in future. If your application is large or your website is high traffic, knowing and applying this information could make or break it. Again, though, a lot of this applies to edge cases that would have little impact on small projects and environments. This optimization does make it harder to maintain the code; some of the things we need to do to make browsers run fast on high-scale websites, such as writing out script nodes with <code>document.write()</code>, are downright nasty.

When faced with the choice between making code cleaner and easier to amend, extend and understand on the one hand, and shaving two milliseconds off every page load on the other, I opt for the former. A lot of JavaScript optimization can be done through scripts. And rather than teach all developers on a project the ins and outs of JavaScript performance, an expert team (or even a tool) could optimize the code before it goes live.

If you can do anything with machines to make the jobs of other machines easier, do it. The time has come for us to apply build processes as much to front-end code as we do to back-end code, instead of forcing ourselves to follow coding practices that go against the natural flow of writing code.</p>

## Further Reading

I hope you've gotten an idea now of how to make scripts more useful, easier to extend and safer to use. For more information, please check out the following links:

*   The Importance of Maintainable JavaScript
*   [Five Things to Do to a Script Before You Hand It to the Next Developer](https://www.wait-till-i.com/2008/02/07/five-things-to-do-to-a-script-before-handing-it-over-to-the-next-developer/)
*   Pragmatic Progressive Enhancement
*   [Planning JavaScript and Ajax for Larger Teams](https://www.wait-till-i.com/2007/11/28/planning-javascript-for-larger-teams-draft-handout-version/) (presentation)

{{< signature "al" >}}


---
title: An Introduction To Full Stack JavaScript
slug: introduction-to-full-stack-javascript
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b1b285d6-4c85-486e-b5b1-0de2ec6643ce/illu-javascript.jpg
date: 2013-11-21T15:24:53.000Z
author: emily-storz
description: >-
  Nowadays, with any Web app you build, you have dozens of architectural
  decisions to make. And you want to make the right ones: **You want to use
  technologies that allow for rapid development**, constant iteration, maximal
  efficiency, speed, robustness and more.
categories:
  - Coding
  - Tools
  - JavaScript
  - Techniques
---
Nowadays, with any Web app you build, you have dozens of architectural decisions to make. And you want to make the right ones: <strong>You want to use technologies that allow for rapid development</strong>, constant iteration, maximal efficiency, speed, robustness and more. You want to be lean and you want to be agile. You want to use technologies that will help you succeed in the short and long term. And those technologies are not always easy to pick out.

In my experience, <a href="https://theothersideofcode.com/building-full-javascript-application-stack">full-stack JavaScript</a> hits all the marks. You’ve probably seen it around; perhaps you’ve considered its usefulness and even debated it with friends. But have you tried it yourself? In this post, I’ll give you an overview of why full-stack JavaScript might be right for you and how it works its magic.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">A Thorough Introduction To Backbone.Marionette (Part 1)</span>](https://www.smashingmagazine.com/2013/02/introduction-backbone-marionette/)
*   [<span class="headline">Journey Through The JavaScript MVC Jungle</span>](https://www.smashingmagazine.com/2012/07/journey-through-the-javascript-mvc-jungle/)
*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [Get Up And Running With Grunt](https://www.smashingmagazine.com/2013/10/get-up-running-grunt/)

To give you a quick preview:

{{% feature-panel %}}

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87d12e31-e949-4e90-8a92-08a88e1f1dfe/toptal-blog-image-large-opt.png"><img loading="lazy" decoding="async" class="130329 size-full" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9d1d98f3-1021-45c9-8985-50590fb30200/toptal-blog-500-opt.png" alt="full stack javascript" width="500" height="561" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/87d12e31-e949-4e90-8a92-08a88e1f1dfe/toptal-blog-image-large-opt.png">Large view</a>)</em>

I’ll introduce these components piece by piece. But first, a short note on how we got to where we are today.</p>

## Why I Use JavaScript

I’ve been a Web developer since 1998. Back then, <a href="https://www.theperlreview.com/articles/php.html">we used Perl</a> for most of our server-side development; but even since then, we’ve had JavaScript on the client side. Web server technologies have changed immensely since then: We went through wave after wave of languages and technologies, such as PHP, ASP, JSP, .NET, Ruby, Python, just to name a few. Developers began to realize that using two different languages for the client and server environments complicates things.

In the early era of PHP and ASP, when template engines were just an idea, <strong>developers embedded application code in their HTML</strong>. Seeing embedded scripts like this was not uncommon:

<pre><code class="language-php">
&lt;script&gt;
    &lt;?php
        if ($login == true){
    ?&gt;
    alert("Welcome");
    &lt;?php
        }
    ?&gt;
&lt;/script&gt;
</code></pre>

Or, even worse:

<pre><code class="language-php">
&lt;script&gt;
    var users_deleted = [];
    &lt;?php
        $arr_ids = array(1,2,3,4);
        foreach($arr_ids as $value){
    ?&gt;
    users_deleted.push("&lt;php&gt;");
    &lt;?php
        }
    ?&gt;
&lt;/script&gt;
</code></pre>

For starters, there were the typical errors and confusing statements between languages, such as <code>for</code> and <code>foreach</code>. Furthermore, writing code like this on the server and on the client to handle the same data structure is uncomfortable even today (unless, of course, you have a development team with engineers dedicated to the front end and engineers for the back end — but even if they can share information, they wouldn’t be able to collaborate on each other’s code):

<pre><code class="language-php">
&lt;?php
    $arr = array("apples", "bananas", "oranges", "strawberries"),
    $obj = array();
    $i = 10;
    foreach($arr as $fruit){
        $obj[$fruit] = $i;
        $i += 10;
    }
    echo json_encode(obj);
?&gt;
&lt;script&gt;
    $.ajax({
        url:"/json.php",
        success: function(data){
            var x;
            for(x in data){
                alert("fruit:" + x + " points:" + data[x]);
            }
        }
    });
&lt;/script&gt;
</code></pre>

The initial attempts to unify under a single language were to create client components on the server and compile them to JavaScript. This didn’t work as expected, and most of those projects failed (for example, ASP MVC replacing <a href="https://stackoverflow.com/questions/102558/biggest-advantage-to-using-asp-net-mvc-vs-web-forms">ASP.NET Web forms</a>, and <a href="https://www.gwtproject.org/overview.html">GWT</a> arguably being replaced in the near future by <a href="https://www.2ality.com/2013/05/google-polymer.html">Polymer</a>). But the idea was great, in essence: a single language on the client and the server, enabling us to reuse components and resources (and this is the keyword: resources).

The answer was simple: <strong>Put JavaScript on the server.</strong>

JavaScript was actually <a href="https://www.infoworld.com/d/application-development/javascript-conquers-the-server-969">born server-side</a> in Netscape Enterprise Server, but the language simply wasn’t ready at the time. After years of trial and error, <a href="https://www.toptal.com/nodejs/why-the-hell-would-i-use-node-js">Node.js</a> finally emerged, which not only put JavaScript on the server, but also promoted the idea of <a href="https://blog.mixu.net/2011/02/01/understanding-the-node-js-event-loop/">non-blocking programming</a>, bringing it from the world of nginx, thanks to the Node creator’s nginx background, and (wisely) keeping it simple, thanks to JavaScript’s event-loop nature.

(In a sentence, non-blocking programming aims to put time-consuming tasks off to the side, usually by specifying what should be done when these tasks are completed, and allowing the processor to handle other requests in the meantime.)

<strong>Node.js changed the way we handle I/O access forever.</strong> As Web developers, we were used to the following lines when accessing databases (I/O):

<pre><code class="language-javascript">
var resultset = db.query("SELECT * FROM 'table'");
drawTable(resultset);
</code></pre>

This line essentially blocks your code, because your program stops running until your database driver has a <code>resultset</code> to return. In the meantime, your platform’s infrastructure provides the means for concurrency, usually using threads and forks.

With Node.js and non-blocking programming, we’re given more control over program flow. Now (even if you still have parallel execution hidden by your database (I/O) driver), you can define what the program should do in the meantime and what it <em>will do</em> when you receive the <code>resultset</code>:

<pre><code class="language-sql">
db.query("SELECT * FROM 'table'", function(resultset){
   drawTable(resultset);
});
doSomeThingElse();
</code></pre>

With this snippet, we’ve defined two program flows: The first handles our actions just after sending the database query, while the second handles our actions just after we receive our <code>resultSet</code> using a simple callback. This is an elegant and powerful way to manage concurrency. As they say, <strong>“Everything runs in parallel — except your code.”</strong> Thus, your code will be easy to write, read, understand and maintain, all without your losing control over program flow.

These ideas weren’t new at the time — so, why did they become so popular with Node.js? Simple: Non-blocking programming can be achieved in several ways. Perhaps the easiest is to use callbacks and an <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/EventLoop">event loop</a>. In most languages, that’s not an easy task: While callbacks are a common feature in some other languages, an event loop is not, and you’ll often find yourself grappling with external libraries (for example, Python with <a href="https://www.tornadoweb.org/en/stable/">Tornado</a>).

But in JavaScript, <a href="https://www.impressivewebs.com/callback-functions-javascript/">callbacks</a> are built into the language, as is the event loop, and almost every programmer who has even dabbled in JavaScript is familiar with them (or at least has used them, even if they <a href="https://developer.yahoo.com/blogs/ydn/part-1-understanding-event-loops-writing-great-code-11401.html">don’t quite understand what the event loop is</a>). Suddenly, every startup on Earth could reuse developers (i.e. resources) on both the client and server side, solving the “Python Guru Needed” <a href="https://www.wantedanalytics.com/insight/2011/05/24/computer-programmers-are-in-demand-employers-post-220000-new-jobs-over-past-30-days-4/">job posting problem</a>.

So, now we have an <a href="https://chetansurpur.com/blog/2010/10/why-node-js-is-totally-awesome.html">incredibly fast platform</a> (thanks to non-blocking programming), with a programming language that’s incredibly easy to use (thanks to JavaScript). But is it enough? Will it last? I’m sure JavaScript will have an important place in the future. Let me tell you why.</p>

### Functional Programming

JavaScript was the first programming language to <a href="https://www.crockford.com/javascript/javascript.html">bring the functional paradigm</a> to the masses (of course, Lisp came first, but most programmers have never built a production-ready application using it). Lisp and Self, <a href="https://exploringdata.github.io/vis/programming-languages-influence-network/#JavaScript">Javascript’s main influences</a>, are full of innovative ideas that can free our minds to explore new techniques, patterns and paradigms. And they all carry over to JavaScript. Take a look at <a href="https://blog.jcoglan.com/2011/03/05/translation-from-haskell-to-javascript-of-selected-portions-of-the-best-introduction-to-monads-ive-ever-read/">monads</a>, <a href="https://uxul.wordpress.com/2009/03/02/generating-church-numbers-with-javascript/">Church numbers</a> or even (for a more practical example) <a href="https://underscorejs.org">Underscore</a>’s <a href="https://underscorejs.org/#collections">collections functions</a>, which can save you lines and lines of code.</p>

### Dynamic Objects and Prototypal Inheritance

Object-oriented programming without classes (and without endless hierarchies of classes) allows for fast development — just create objects, add methods and use them. More importantly, it reduces refactoring time during maintenance tasks by enabling the programmer to modify instances of objects, instead of classes. This speed and flexibility pave the way for rapid development.</p>

### JavaScript Is the Internet

JavaScript was <a href="https://www.computer.org/csdl/mags/co/2012/02/mco2012020007.pdf">designed for the Internet</a>. It’s been here since the beginning, and it’s <a href="https://www.netmagazine.com/news/firefox-23-hide-disable-javascript-option-132851">not going away</a>. All attempts to destroy it have failed; recall, for instance, the downfall of <a href="https://jaxenter.com/douglas-crockford-java-was-a-colossal-failure-javascript-is-succeeding-because-it-works-45928.html">Java Applets</a>, VBScript’s replacement by <a href="https://www.typescriptlang.org">Microsoft’s TypeScript</a> (which compiles to JavaScript), and Flash’s demise at the hands of the mobile market and HTML5. <strong>Replacing JavaScript without breaking millions of Web pages is impossible</strong>, so our goal going forward should be to improve it. And no one is better suited for the job than <a href="https://www.ecma-international.org/memento/TC39.htm">Technical Committee 39</a> of ECMA.

Sure, alternatives to JavaScript are born every day, like <a href="https://coffeescript.org">CoffeeScript</a>, <a href="https://www.typescriptlang.org">TypeScript</a> and the <a href="https://github.com/jashkenas/coffee-script/wiki/List-of-languages-that-compile-to-JS">millions of languages that compile to JavaScript</a>. These alternatives might be useful for development stages (<a href="https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/">via source maps</a>), but they will fail to supplant JavaScript in the long run for two reasons: Their communities will never be bigger, and their best features will be adopted by ECMAScript (i.e. JavaScript). JavaScript is not an assembly language: It’s a high-level programming language with source code that you can understand — so, you <em>should</em> understand it.</p>

## End-to-End JavaScript: Node.js And MongoDB

We’ve covered the reasons to use JavaScript. Next, we’ll look at JavaScript as a reason to use Node.js and MongoDB.</p>

### Node.js

<a href="https://www.toptal.com/nodejs/why-the-hell-would-i-use-node-js">Node.js</a> is a platform for building fast and scalable network applications — that’s pretty much what the Node.js website says. But Node.js is more than that: It’s the hottest JavaScript runtime environment around right now, used by a ton of applications and libraries — <strong>even browser libraries are now running on Node.js</strong>. More importantly, this fast server-side execution allows developers to focus on more complex problems, such as <a href="https://github.com/NaturalNode/natural">Natural</a> for <a href="https://en.wikipedia.org/wiki/Natural_language_processing">natural language processing</a>. Even if you don’t plan to write your main server application with Node.js, you can use tools built on top of Node.js to improve your development process; for example, <a href="https://bower.io/">Bower</a> for front-end package management, Mocha for unit testing, <a href="https://gruntjs.com">Grunt</a> for automated build tasks and even <a href="https://brackets.io">Brackets</a> for full-text code editing.

So, if you’re going to write JavaScript applications for the server or the client, you should become familiar with Node.js, because you will need it daily. Some interesting <a href="https://vertx.io/">alternatives</a> exist, but none have even 10% of Node.js’ community.</p>

### MongoDB

<a href="https://www.mongodb.org">MongoDB</a> is a <a href="https://en.wikipedia.org/wiki/NoSQL">NoSQL</a> document-based database that uses JavaScript as its query language (but is not written in JavaScript), thus completing our end-to-end JavaScript platform. But that’s not even the main reason to choose this database.

MongoDB is <a href="https://blog.mongodb.org/post/119945109/why-schemaless">schema-less</a>, <strong>enabling you to persist objects in a flexible way</strong> and, thus, adapt quickly to changes in requirements. Plus, it’s highly <a href="https://siliconangle.com/blog/2013/06/21/mongodb-brings-speed-scalability-and-performance-to-handling-unstructured-data-mongodbdays/">scalable</a> and <a href="https://docs.mongodb.org/manual/core/map-reduce/">based on map-reduce</a>, making it suitable for big data applications. MongoDB is so flexible that it can be used as a schema-less document database, a relational data store (although it <a href="https://docs.mongodb.org/manual/faq/fundamentals/">lacks</a> <a href="https://en.wikipedia.org/wiki/Database_transaction">transactions</a>, which can only be <a href="https://docs.mongodb.org/manual/tutorial/perform-two-phase-commits/">emulated</a>) and even as a key-value store for caching responses, like <a href="https://memcached.org">Memcached</a> and <a href="https://redis.io">Redis</a>.</p>

## Server Componentization With Express

Server-side componentization is never easy. But with <a href="https://expressjs.com">Express</a> (and <a href="https://www.senchalabs.org/connect/">Connect</a>) came the idea of “middleware.” In my opinion, middleware is the best way to define components on the server. If you want to compare it to a known pattern, it’s pretty close to pipes and filters.

<strong>The basic idea is that your component is part of a pipeline.</strong> The pipeline processes a request (i.e. the input) and generates a response (i.e. the output), but your component isn’t responsible for the entire response. Instead, it modifies only what it needs to and then delegates to the next piece in the pipeline. When the last piece of the pipeline finishes processing, the response is sent back to the client.

We refer to these pieces of the pipeline as middleware. Clearly, we can create two kinds of middleware:

*   **Intermediates**.  An intermediate processes the request and the response but is not fully responsible for the response itself and so delegates to the next middleware.
*   **Finals**.  A final has full responsibility over the final response. It processes and modifies the request and the response but doesn’t need to delegate to the next middleware. In practice, delegating to the next middleware anyway will allow for architectural flexibility (i.e. for adding more middleware later), even if that middleware doesn’t exist (in which case, the response would go straight to the client).

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f562f5c1-7949-40d5-94fe-659d3f205845/user-manager-large-opt.png"><img loading="lazy" decoding="async" class="130333" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1bd4d115-5e1c-4be3-9e5d-c35a514773ec/user-manager-500-opt.png" alt="user-manager-500-opt" width="500" height="307" /></a><br>
<em>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f562f5c1-7949-40d5-94fe-659d3f205845/user-manager-large-opt.png">Large view</a>)</em>

As a concrete example, <strong>consider a “user manager” component on the server</strong>. In terms of middleware, we’d have both finals and intermediates. For our finals, we’d have such features as creating a user and listing users. But before we can perform those actions, we need our intermediates for authentication (because we don’t want unauthenticated requests coming in and creating users). Once we’ve created these authentication intermediates, we can just plug them in anywhere that we want to turn a previously unauthenticated feature into an authenticated feature.</p>

## Single-Page Applications

When working with full-stack JavaScript, you’ll often focus on creating <a href="https://en.wikipedia.org/wiki/Single-page_application">single-page applications</a> (SPAs). Most Web developers are tempted more than once to try their hand at SPAs. I’ve built several (mostly proprietary), and I believe that they are simply the <a href="https://medium.com/tech-talk/fb44da86dc1f">future of Web applications</a>. Have you ever compared an SPA to a regular Web app on a mobile connection? The <strong>difference in responsiveness</strong> is in the order of tens of seconds.

(Note: Others might disagree with me. Twitter, for example, <a href="https://blog.twitter.com/2012/improving-performance-twittercom">rolled back its SPA approach</a>. Meanwhile, large websites such as <a href="https://techcrunch.com/2012/11/30/why-enterprise-apps-are-moving-to-single-page-design/">Zendesk</a> are moving towards it. I’ve seen enough evidence of the benefits of SPAs to believe in them, but experiences vary.)

If SPAs are so great, why build your product in a legacy form? A common argument I hear is that people are worried about SEO. But if you handle things correctly, this shouldn’t be an issue: You can take different approaches, from <a href="https://vickev.com/#!/article/easily-index-your-single-page-application-thanks-to-phantomjs">using a headless browser</a> (such as <a href="https://phantomjs.org/">PhantomJS</a>) to render the HTML when a Web crawler is detected to performing <a href="https://youtube.com/watch?v=sGpHDHAIpYE">server-side rendering</a> with the help of existing frameworks.</p>

## Client Side MV* With Backbone.js, Marionette And Twitter Bootstrap

Much has been said about <a href="https://blog.stevensanderson.com/2012/08/01/rich-javascript-applications-the-seven-frameworks-throne-of-js-2012/">MV* frameworks for SPAs</a>. It’s a tough choice, but I’d say that the top three are <a href="https://backbonejs.org">Backbone.js</a>, <a href="https://emberjs.com">Ember</a> and <a href="https://angularjs.org">AngularJS</a>.

All three are very well regarded. But <a href="https://todomvc.com">which is best for you</a>?

Unfortunately, I must admit that I have limited experience with AngularJS, so I’ll leave it out of the discussion. Now, Ember and Backbone.js represent two different ways of attacking the same problem.

<a href="https://www.toptal.com/backbone-js/">Backbone.js</a> is minimal and offers just enough for you to create a simple SPA. Ember, on the other hand, is a complete and professional framework for creating SPAs. It has more bells and whistles, but also a steeper learning curve. (You can read <a href="https://www.smashingmagazine.com/2013/11/07/an-in-depth-introduction-to-ember-js/">more about Ember.js here</a>.)

Depending on the size of your application, the decision could be as easy as <strong>looking at the “features used” to “features available” ratio</strong>, which will give you a big hint.

Styling is a challenge as well, but again, we can count on frameworks to bail us out. For CSS, <a href="https://twitter.github.io/bootstrap/">Twitter Bootstrap</a> is a good choice because it offers a complete set of styles that are both ready to use out of the box and <a href="https://www.smashingmagazine.com/2013/03/12/customizing-bootstrap/">easy to customize</a>.

Bootstrap was created in the <a href="https://lesscss.org/">LESS</a> language, and it’s open source, so we can modify it if need be. It comes with a ton of UX controls that are <a href="https://twitter.github.io/bootstrap/components.html">well documented</a>. Plus, a <a href="https://twitter.github.io/bootstrap/customize.html">customization model</a> enables you to create your own. It is definitely the right tool for the job.</p>

## Best Practices: Grunt, Mocha, Chai, RequireJS and CoverJS

Finally, we should define some best practices, as well as mention how to implement and maintain them. Typically, my solution centers on several tools, which themselves are based on Node.js.</p>

### Mocha and Chai

These tools enable you to improve your development process by applying <a href="https://www.agiledata.org/essays/tdd.html">test-driven development</a> (TDD) or <a href="https://dannorth.net/introducing-bdd/">behavior-driven development</a> (BDD), creating the infrastructure to organize your unit tests and a runner to automatically run them.

<a href="https://en.wikipedia.org/wiki/List_of_unit_testing_frameworks#JavaScript">Plenty</a> of unit test frameworks exist for JavaScript. Why use Mocha? The short answer is that it’s flexible and complete.

The long answer is that it has two important features (interfaces and reporters) and one significant absence (assertions). Allow me to explain:

*   **Interfaces**.  Maybe you’re used to TDD concepts of suites and unit tests, or perhaps you prefer BDD ideas of behavior specifications with `describe` and `should`. Mocha lets you use both approaches.
*   **Reporters**.  Running your test will generate reports of the results, and you can format these results using various reporters. For example, if you need to feed a continuous integration server, you’ll find a reporter to do just that.
*   **Lack of an assertion library**.  Far from being a problem, Mocha was designed to let you use the assertion library of your choice, giving you even more flexibility. You have [plenty of options](https://stackoverflow.com/questions/10472152/standalone-assertion-libraries#answer-10480546), and this is where Chai comes into play.

Chai is a flexible assertion library that lets you use any of the three major assertion styles:

*   `assert` This is the classic assertion style from old-school TDD. For example:

        assert.equal(variable, "value");

*   `expect` This chainable assertion style is most commonly used in BDD. For example:

        expect(variable).to.equal("value");

*   `should` This is also used in BDD, but I prefer `expect` because `should` often sounds repetitive (i.e. with the behavior specification of “it (should do something…)”). For example:

        variable.should.equal("value");

Chai combines perfectly with Mocha. Using just these two libraries, you can write your tests in TDD, BDD or any style imaginable.</p>

### Grunt

Grunt enables you to automate build tasks, anything including simple copying-and-pasting and concatenation of files, template precompilation, style language (i.e. SASS and LESS) compilation, unit testing (with Mocha), linting and code minification (for example, with <a href="https://github.com/mishoo/UglifyJS">UglifyJS</a> or <a href="https://developers.google.com/closure/compiler/">Closure Compiler</a>). You can add your own automated task to Grunt or <a href="https://gruntjs.com/plugins">search the registry</a>, where hundreds of plugins are available (once again, using a tool with a great community behind it pays off). Grunt can also <a href="https://github.com/gruntjs/grunt-contrib-watch">monitor your files</a> and trigger actions when any are modified.</p>

### RequireJS

RequireJS might sound like just another way to load modules with the <a href="https://github.com/amdjs/amdjs-api/wiki/AMD">AMD</a> API, but I assure you that it is much more than that. With RequireJS, you can define dependencies and hierarchies on your modules and let the RequireJS library load them for you. It also <strong>provides an easy way to avoid global variable space pollution</strong> by defining all of your modules inside functions. This makes the modules reusable, unlike <a href="https://www.kenneth-truyers.net/2013/04/27/javascript-namespaces-and-modules/">namespaced modules</a>. Think about it: If you define a module like <code>Demoapp.helloWordModule</code> and you want to port it to <code>Firstapp.helloWorldModule</code>, then you would need to change every reference to the <code>Demoapp</code> namespace in order to make it portable.

RequireJS will also help you embrace the <a href="https://merrickchristensen.com/articles/javascript-dependency-injection.html">dependency injection</a> pattern. Suppose you have a component that needs an instance of the main application object (a singleton). From using RequireJS, you realize that you shouldn’t use a global variable to store it, and you can’t have an instance as a RequireJS dependency. So, instead, you need to require this dependency in your module constructor. Let’s see an example.

In <code>main.js</code>:

<pre><code class="language-javascript">
  define(
      ["App","module"],
      function(App, Module){
          var app = new App();

          var module = new Module({
              app: app
          })

          return app;
      }
  );
</code></pre>

In <code>module.js</code>:

<pre><code class="language-javascript">
  define([],
      function(){
          var module = function(options){
              this.app = options.app;
          };
          module.prototype.useApp = function(){
              this.app.performAction();
          };
          return module
      }
  );
</code></pre>

Note that we cannot define the module with a dependency to <code>main.js</code> without creating a circular reference.</p>

### CoverJS

<a href="https://en.wikipedia.org/wiki/Code_coverage">Code coverage</a> is a metric for evaluating your tests. As the name implies, it tells you how much of your code is covered by your current test suite. CoverJS measures your tests’ code coverage by instrumenting statements (instead of lines of code, like <a href="https://siliconforks.com/jscoverage/">JSCoverage</a>) in your code and generating an instrumented version of the code. It can also generate reports to feed your <a href="https://martinfowler.com/articles/continuousIntegration.html">continuous integration</a> server.</p>

## Conclusion

Full-stack JavaScript isn’t the answer to every problem. But its community and technology will carry you a long way. With JavaScript, you can create scalable, maintainable applications, unified under a single language. There’s no doubt, it’s a force to be reckoned with.

{{< signature "al, ea" >}}


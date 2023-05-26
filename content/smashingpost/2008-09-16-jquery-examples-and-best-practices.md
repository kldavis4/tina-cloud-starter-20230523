---
title: 'jQuery and JavaScript Coding: Examples and Best Practices'
slug: jquery-examples-and-best-practices
image: null
date: 2008-09-16T16:15:47.000Z
author: alex-holt
description: >-
  When used correctly,jQuery can help you make your website more interactive,
  interesting and exciting. This article will share some best practices and
  examples for using the popular Javascript framework to create unobtrusive,
  accessible DOM scripting effects.
categories:
  - Coding
  - JavaScript
  - jQuery
---
<strong><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/008c9dcb-20ff-413f-986f-0d0273f85022/postit.png" alt="Things to do today.." width="260" height="208" align="right" /></strong>

When used correctly, <strong>jQuery </strong>can help you make your website more interactive, interesting and exciting. This article will share some best practices and examples for using the popular Javascript framework to create unobtrusive, accessible DOM scripting effects. The article will explore what constitutes <strong>best practices with regard to Javascript</strong> and, furthermore, why jQuery is a good choice of a framework to implement best practices. 

You may want to take a look at the following newer posts:

*   [Essential jQuery Plugin Patterns](https://www.smashingmagazine.com/2011/10/essential-jquery-plugin-patterns/)
*   [Useful JavaScript Libraries and jQuery Plugins](https://www.smashingmagazine.com/useful-javascript-libraries-jquery-plugins-part-2/)
*   [jQuery and JavaScript Coding: Examples and Best Practices](https://www.smashingmagazine.com/2008/09/jquery-examples-and-best-practices/)
*   [Useful jQuery Function Demos For Your Projects](https://www.smashingmagazine.com/2012/05/50-jquery-function-demos-for-aspiring-web-developers/)

## 1\. Why jQuery?

<a href="https://jquery.com/">jQuery</a> is ideal because it can create impressive animations and interactions. jQuery is simple to understand and easy to use, which means the learning curve is small, while the possibilities are (almost) infinite.

{{% feature-panel %}}

### Javascript and Best Practices

Javascript has long been the subject of many heated debates about whether it is possible to use it while still adhering to best practices regarding accessibility and standards compliance.

The answer to this question is still unresolved, however, the emergence of Javascript frameworks like jQuery has provided the necessary tools to create beautiful websites without having to worry (as much) about accessibility issues.

Obviously there are cases where a Javascript solution is not the best option. The rule of thumb here is:<strong> use DOM scripting to <em>enhance</em> functionality, not create it.</strong>

### Unobtrusive DOM Scripting

While the term “DOM scripting” really just refers to the use of scripts (in this case, Javascripts) to access the Document Object Model, it has widely become accepted as a way of describing what should really be called "unobtrusive DOM scripting"—basically, the art of adding Javascript to your page in such a way that if there were NO Javascript, the page would still work (or at least degrade gracefully). In the website world, our DOM scripting is done using Javascript.</p>

### The Bottom Line: Accessible, Degradable Content

The aim of any web producer, designer or developer is to create content that is accessible to the widest range of audience. However, this has to be carefully balanced with design, interactivity and beauty. Using the theories set out in this article, designers, developers and web producers will have the knowledge and understanding to use jQuery for DOM scripting in an accessible and degradable way; maintaining content that is beautiful, functional AND accessible.</p>

## 2\. Unobtrusive DOM Scripting?

In an ideal world, websites would have dynamic functionality AND effects that degrade well. What does this mean? It would mean finding a way to include, say, a snazzy Javascript Web 2.0 animated sliding news ticker widget in a web page, while still ensuring that it fails gracefully if a visitor's browser can't (or won't) run Javascripts.

The theory behind this technique is quite simple: the ultimate aim is to use Javascript for non-invasive, "behavioural" elements of the page. Javascript is used to add or enhance interactivity and effects. The primary rules for DOM scripting follow.</p>

### Rule #1: Separate Javascript Functionality

Separate Javascript functionality into a "behavioural layer," so that it is separate from and independent of (X)HTML and CSS. (X)HTML is the markup, CSS the presentation and Javascript the behavioural layer. This means storing ALL Javascript code in external script files and building pages that <strong>do not rely on Javascript to be usable. </strong>

For a demonstration, check out the following code snippets:

#### **![Cross](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05bc6cf0-4adf-44ba-a708-039697114a75/cross.gif)**Bad markup:

Never include Javascript events as inline attributes. This practice should be completely wiped from your mind.

<pre><code class="language-markup tmp-html">&lt;a onclick="doSomething()" href="#"&gt;Click!&lt;/a&gt;</code></pre>

#### ![Tick](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d89e1c9-0e08-41b3-af44-a1ee8e55960c/tick.gif)Good markup:

All Javascript behaviours should be included in external script files and linked to the document with a &lt;script&gt; tag in the head of the page. So, the anchor tag would appear like this:

<pre><code class="language-markup tmp-html">&lt;a href="backuplink.html" class="doSomething"&gt;Click!&lt;/a&gt;</code></pre>

And the Javascript inside the myscript.js file would contain something like this:

<pre><code class="language-javascript">...

$('a.doSomething').click(function(){
	// Do something here!
	alert('You did something, woo hoo!');
});
...</code></pre>

The <a href="https://docs.jquery.com/Events/click">.click() method in jQuery</a> allows us to easily attach a click event to the result(s) of our selector. So the code will select all of the &lt;a&gt; tags of class "doSomething" and attach a click event that will call the function. In practice, this

In Rule #2 there is a further demonstration of how a similar end can be achieved without inline Javascript code.</p>

### Rule #2: NEVER Depend on Javascript

To be truly unobtrusive, a developer should never rely on Javascript support to deliver content or information. It's fine to use Javascript to enhance the information, make it prettier, or more interactive—but never assume the user's browser will have Javascript enabled. This rule of thumb can in fact be applied to any third-party technology, such as Flash or Java. If it's not built into every web browser (and always enabled), then be sure that the page is still completely accessible and usable without it.

#### **![Cross](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05bc6cf0-4adf-44ba-a708-039697114a75/cross.gif)Bad markup:**

The following snippet shows Javascript that might be used to display a "Good morning" (or "afternoon") message on a site, depending on the time of day. (Obviously this is a rudimentary example and would in fact probably be achieved in some server-side scripting language).

<pre><code class="language-markup tmp-html">&lt;script language="javascript"&gt;
var now = new Date();
if(now.getHours() &lt; 12)
	document.write('Good Morning!');
else
	document.write('Good Afternoon!');
&lt;/script&gt;</code></pre>

This inline script is bad because if the target browser has Javascript disabled, NOTHING will be rendered, leaving a gap in the page. This is NOT graceful degradation. The non-Javascript user is missing out on our welcome message.

##### ![Tick](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d89e1c9-0e08-41b3-af44-a1ee8e55960c/tick.gif)Good markup:<a name="domscript1"></a>

A semantically correct and accessible way to implement this would require much simpler and more readable (X)HTML, like:

<pre><code class="language-markup tmp-html">&lt;p title="Good Day Message"&gt;Good Morning!&lt;/p&gt;</code></pre>

By including the "title" attribute, this paragraph can be selected in jQuery using a selector ([selectors are explained later in this article](#Selectors)) like the one in the following Javascript snippet:

<pre><code class="language-javascript">var now = new Date();
if(now.getHours() &gt;= 12)
{
	var goodDay = $('p[title="Good Day Message"]');
	goodDay.text('Good Afternoon!');
}</code></pre>

The beauty here is that all the Javascript lives in an external script file and the page is rendered as standard (X)HTML, which means that if the Javascript isn't run, the page is still 100% semantically pure (X)HTML—no Javascript cruft. The only problem would be that in the afternoon, the page would still say "Good morning." However, this can be seen as an acceptable degradation.</p>

### Rule #3: Semantic and Accessible Markup Comes First

It is very important that the (X)HTML markup is semantically structured. (While it is outside the scope of this article to explain why, see the links below for further reading on semantic markup.) The general rule here is that if the page's markup is semantically structured, it should follow that it is also accessible to a wide range of devices. This is not always true, though, but it is a good rule of thumb to get one started.

Semantic markup is important to unobtrusive DOM scripting because it shapes the path the developer will take to create the DOM scripted effect. The FIRST step in building any jQuery-enhanced widget into a page is to write the markup and make sure that the markup is semantic. Once this is achieved, the developer can then use jQuery to interact with the semantically correct markup (leaving an (X)HTML document that is clean and readable, and separating the behavioural layer).

#### **![Cross](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05bc6cf0-4adf-44ba-a708-039697114a75/cross.gif)Terrible markup:**

The following snippet shows a typical list of items and descriptions in a typical (and terribly UNsemantic) way.

<pre><code class="language-markup tmp-html">&lt;table&gt;
    &lt;tr&gt;
        &lt;td onclick="doSomething();"&gt;First Option&lt;/td&gt;
        &lt;td&gt;First option description&lt;/td&gt;
    &lt;/tr&gt;
    &lt;tr&gt;
        &lt;td onclick="doSomething();"&gt;Second Option&lt;/td&gt;
        &lt;td&gt;Second option description&lt;/td&gt;
    &lt;/tr&gt;
&lt;/table&gt;</code></pre>

#### **![Cross](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05bc6cf0-4adf-44ba-a708-039697114a75/cross.gif)Bad markup:**

The following snippet shows a typical list of items and descriptions in a more semantic way. However, the inline Javascript is far from perfect.

<pre><code class="language-markup tmp-html">&lt;dl&gt;
    &lt;dt onclick="doSomething();"&gt;First Option&lt;/dt&gt;
    &lt;dd&gt;First option description&lt;/dd&gt;
    &lt;dt onclick="doSomething();"&gt;Second Option&lt;/dt&gt;
    &lt;dd&gt;Second option description&lt;/dd&gt;
&lt;/dl&gt;</code></pre>

#### **![Tick](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d89e1c9-0e08-41b3-af44-a1ee8e55960c/tick.gif)Good markup:**

This snippet shows how the above list <strong>should</strong> be marked up. Any interaction with Javascript would be attached at DOM load using jQuery, effectively removing all behavioural markup from the rendered (X)HTML.

<pre><code class="language-markup tmp-html">&lt;dl id="OptionList"&gt;
    &lt;dt&gt;First Option&lt;/dt&gt;
    &lt;dd&gt;First option description&lt;/dd&gt;
    &lt;dt&gt;Second Option&lt;/dt&gt;
    &lt;dd&gt;Second option description&lt;/dd&gt;
&lt;/dl&gt;</code></pre>

The &lt;id&gt; of "OptionList" will enable us to target this particular definition list in jQuery using a selector—<a href="#Selectors">more on this later</a>.</p>

## 3\. Understanding jQuery for Unobtrusive DOM Scripting

This section will explore three priceless tips and tricks for using jQuery to implement best practices and accessible effects.</p>

### <a name="Selectors"></a>Understanding Selectors: the Backbone of jQuery

The first step to unobtrusive DOM scripting (at least in jQuery and Prototype) is using selectors. Selectors can (amazingly) select an element out of the DOM tree so that it can be manipulated in some way.

If you're familiar with CSS then you'll understand selectors in jQuery; they're almost the same thing and use almost the same syntax. jQuery provides a special utility function to select elements. It is called $.

#### A set of very simple examples of jQuery selectors:

<pre><code class="language-javascript">$(document); // Activate jQuery for object
$('#mydiv')  // Element with ID "mydiv"
$('p.first') // P tags with class first.
$('p[title="Hello"]') // P tags with title "Hello"
$('p[title^="H"]') // P tags title starting with H</code></pre>

#### So, as the Javascript comments suggest:

1.  <span class="javascript">**$(document);**</span> The first option will apply the jQuery library methods to a DOM object (in this case, the document object).
2.  <span class="javascript">**$('#mydiv')**</span> The second option will select every <div> that has the <id> attribute set to "mydiv".
3.  <span class="javascript">**$('p.first')**</span> The third option will select all of the <p> tags with the class of "first".
4.  <span class="javascript">**$('p[title="Hello"]')**</span> This option will select from the page all <p> tags that have a title of "Hello". Techniques like this enable the use of much more semantically correct (X)HTML markup, while still facilitating the DOM scripting required to create complex interactions.
5.  <span class="javascript">**$('p[title^="H"]')**</span> This enables the selection of all of the <p> tags on the page that have a title that starts with the letter H.

#### These examples barely scratch the surface.

Almost anything you can do in CSS3 will work in jQuery, plus many more complicated selectors. The complete list of selectors is well documented on the <a href="https://docs.jquery.com/Selectors">jQuery Selectors documentation page</a>. If you're feeling super-geeky, you could also read the <a href="https://www.w3.org/TR/css3-selectors/">CSS3 selector specification</a> from the W3C.</p>

### Get ready. $(document).ready()

Traditionally Javascript events were attached to a document using an "onload" attribute in the &lt;body&gt; tag of the page. Forget this practice. Wipe it from your mind.

jQuery provides us with a special utility on the document object, called "ready", allowing us to execute code ONLY after the DOM has completely finished loading. This is the key to unobtrusive DOM scripting, as it allows us to completely separate our Javascript code from our markup. Using <code>$(document).ready()</code>, we can queue up a series of events and have them execute after the DOM is initialized.

This means that we can create entire effects for our pages without changing the markup for the elements in question.

#### Hello World! Why $(document).ready() is SO cool

To demonstrate the beauty of this functionality, let's recreate the standard introduction to Javascript: a "Hello World" alert box.

The following markup shows how we might have run a "Hello World" alert without jQuery:

##### **![Cross](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05bc6cf0-4adf-44ba-a708-039697114a75/cross.gif)**Bad markup:

<pre><code class="language-markup tmp-html">&lt;script language="javascript"&gt;
alert('Hello World');
&lt;/script&gt;</code></pre>

##### **![Tick](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d89e1c9-0e08-41b3-af44-a1ee8e55960c/tick.gif)**Good markup:

Using this functionality in jQuery is simple. The following code snippet demonstrates how we might call the age-old "Hello World" alert box after our document has loaded. The true beauty of this markup is that it lives in an external Javascript file. There is NO impact on the (X)HTML page.

<pre><code class="language-javascript">$(document).ready(function()
{
	alert('Hello World');
});</code></pre>

##### How it works

The $(document).ready() function takes a function as its argument. (In this case, an anonymous function is created inline—a technique that is used throughout the jQuery documentation.) The function passed to $(document).ready() is called after the DOM has finished loading and executes the code inside the function, in this case, calling the alert.</p>

### Dynamic CSS Rule Creation

One problem with many DOM scripting effects is that they often require us to hide elements of the document from view. This hiding is usually achieved through CSS. However, this is less than desirable. If a user's browser does not support Javascript (or has Javascript disabled), yet <em>does </em>support CSS, then the elements that we hide in CSS will never be visible, since our Javascript interactions will not have run.

The solution to this comes in the form of a plugin for jQuery called cssRule, which allows us to use Javascript to easily add CSS rules to the style sheet of the document. This means we can hide elements of the page using CSS—however the CSS is ONLY executed IF Javascript is running.

#### **![Cross](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/05bc6cf0-4adf-44ba-a708-039697114a75/cross.gif)**Bad markup:

<pre><code class="language-markup tmp-html">HTML:
&lt;h2&gt;This is a heading&lt;/h2&gt;
&lt;p class="hide-me-first"&gt;
This is some information about the heading.
&lt;/p&gt;

CSS:
p.hide-me-first
{
	display: none;
}</code></pre>

Assuming that a paragraph with the class of "hide-me-first" is going to first be hidden by CSS and then be displayed by a Javascript after some future user interaction, if the Javascript never runs the content will never be visible.

#### **![Tick](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d89e1c9-0e08-41b3-af44-a1ee8e55960c/tick.gif)**Good markup:

<pre><code class="language-markup tmp-html">HTML:
&lt;h2&gt;This is a heading&lt;/h2&gt;
&lt;p class="hide-me-first"&gt;
This is some information about the heading.
&lt;/p&gt;

jQuery Javascript:
$(document).ready(function{
	jQuery.cssRule("p.hide-me-first", "display", "none");
});</code></pre>

Using a $(document).ready() Javascript here to hide the paragraph element means that if Javascript is disabled, the paragraphs won't ever be hidden—so the content is still accessible. This is the key reason for runtime, Javascript-based, dynamic CSS rule creation.</p>

## 4\. Conclusion

jQuery is an extremely powerful library that provides all the tools necessary to create beautiful interactions and animations in web pages, while empowering the developer to do so in an accessible and degradable manner.

<strong>This article has covered:</strong>

1.  Why unobtrusive DOM scripting is so important for accessibility,
2.  Why jQuery is the natural choice to implement unobtrusive DOM scripting effects,
3.  How jQuery selectors work,
4.  How to implement unobtrusive CSS rules in jQuery.</p>

## 5\. Further Reading

### Further Reading: jQuery and JavaScript Practices

1.  _jQuery Web Site:_ [How jQuery Works](https://docs.jquery.com/How_jQuery_Works) and [Tutorials](https://docs.jquery.com/Tutorials) _John Resig + Other Contributors_ One of jQuery's true strengths is the documentation provided by John Resig and his team.
2.  [Learning jQuery](https://www.learningjquery.com/)
3.  [jQuery Tutorials For Designers](https://www.webdesignerwall.com/tutorials/jquery-tutorials-for-designers/)
4.  [The Seven Rules Of Pragmatic Progressive Enhancement](https://ajaxian.com/archives/the-seven-rules-of-pragmatic-progressive-enhancement)
5.  [A List Apart: Behavioral Separation](https://www.alistapart.com/articles/behavioralseparation) _Jeremy Keith_ A more in-depth explanation of the idea of separating Javascript into an unobtrusive "behavioural" layer.

<em>Simon Willison</em>
A great set of slides about using jQuery unobtrusively. Also, finishes with a wonderful summary of jQuery methods and usage.</p>

### Further Reading: Semantic Markup

1.  [Wikipedia: Definition of Semantics](https://en.wikipedia.org/wiki/Semantic) It's worth understanding the idea of semantics in general prior to trying to wrap one's head around the concept of semantic markup.
2.  [Who cares about semantic markup?](https://www.mezzoblue.com/archives/2005/05/30/who_cares_ab/) _Dave Shea_ Dave Shea explores the benefits of semantic markup and
3.  [Standards don't necessarily have anything to do with being semantically correct](https://www.kottke.org/03/08/standards-semantically-correct) _Jason Kottke_ Kottke discusses the differences between standards compliance and semantic markup.
4.  [CSS3 selector specification](https://www.w3.org/TR/css3-selectors/) _W3C_ The complete specification for CSS3 selectors (most of which work perfectly in jQuery selectors also). This is great reading for anyone who likes to keep up to date with best practices and standards compliance.


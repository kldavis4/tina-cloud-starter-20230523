---
title: 'Guidelines For Working With External Code Libraries'
slug: working-with-external-code-libraries
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/701f7237-f82b-44dc-b10a-8f72d4ddf0d4/umlwebsite.jpg
date: 2011-06-20T13:33:51.000Z
author: sue-smith
summary: >-
  Sue Smith goes through a few tips and techniques (with particular reference to JavaScript and a little PHP) that can make working with other people’s code more productive. Whether you’re a software developer or a Web designer who does a bit of coding from time to time this article offers you ways to learn to see unfamiliar code as an opportunity.
description: >-
  Sue Smith goes through a few tips and techniques that can make working with other people’s code more productive. Whether you’re a software developer or a Web designer who does a bit of coding from time to time this article offers you ways to learn to see unfamiliar code as an opportunity.
categories:
  - Productivity
  - Business
  - Workflow
  - Communication
---

Working with code that was created by some other person or organization is routine for developers, but it can be one of the most demanding activities, particularly if you’re still learning.

From using code libraries to working on a team of developers, there are bound to be times when you need to get to grips with code written by someone other than yourself.

Whether you’re a software developer or a Web designer who does a bit of coding from time to time, your work routine might sometimes be isolated, but your work typically is not. When you use an external resource or work on an existing system, you see that your work exists in the context of other technologies and, yes, other people.

For developers, the nightmare of **other people’s code** is one of the most frustrating aspects of the job. But I believe this needn’t be the case. If you can get into a few “healthy” habits and learn to see unfamiliar code as an opportunity, then your working day will be less stressful and your own code-writing skills will ultimately improve. Don’t worry: this isn’t a self-help presentation, and no mantras will be required.

In this article, we’ll go through a few tips and techniques (with particular reference to JavaScript and a little PHP) that can make working with other people’s code less nightmarish and more productive. If you come from a programming background, you might already indulge in many of these activities already. But who knows? Maybe you haven’t come across some of them yet. If you’re anything like me, you pick these things up in a haphazard, random sort of way. If you come from a design background, some of the tips might well be new to you.

Steering clear of the “[Should Web Designers Know How To Code?](https://www.smashingmagazine.com/2010/11/11/should-web-designers-know-how-to-code/)” debate, this article is written to be helpful to people who are primarily designers but have chosen to get more involved in coding, as well as people who are primarily developers but are just getting started.

{{% feature-panel %}}

## A Brief(-ish) Aside On Development Patterns

For developers who come from more of a design background, seeing the value in some of the techniques that more seasoned programmers use can be difficult. Let’s briefly look at some of these, and **don’t worry if you don’t know much about programming** (and don’t really care to), this is really general stuff that will more than likely prove useful. If you’re an experienced programmer, this section will likely be less relevant to you.

When you go about creating an application, whether for the desktop or the Web, you have a number of choices: not just in technologies, but in how you use them. Generally speaking, the result is a load of code that is executed to produce the required functionality and appearance. However, various options, techniques and patterns are involved in organizing and designing this code to make it carry out the **required tasks**.

<figure><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/701f7237-f82b-44dc-b10a-8f72d4ddf0d4/umlwebsite.jpg" alt="UML Website System"/><figcaption>Development patterns are used to split up the various tasks involved in creating an application. (Image: <a href="https://commons.wikimedia.org/wiki/File:Metamodel_Linkedin.jpg">Jean-Marie Favre</a>, part of <a href="https://en.wikipedia.org/wiki/Unified_Modeling_Language">UML</a> diagram representing LinkedIn’s social networking system.)</figcaption></figure>

### Organized Code

[Development patterns](https://en.wikipedia.org/wiki/Design_pattern_%28computer_science%29 "Wikipedia: Design pattern") represent different approaches to building code to implement specified functionality. In many cases, they involve grouping sections of code and assigning these **well-defined sets of responsibilities (and data)**.

One of the most intuitive development models of this kind is [object-oriented](https://en.wikipedia.org/wiki/Object-oriented_programming "Wikipedia: Object Oriented Programming"), in which tasks are distributed between objects (with class declarations that define how objects should behave). For example, you could have an object in a payroll system that is responsible for handling wage calculations, another for processing payments and so on. Code that is external to an object should be able to use it **without having to get involved in the details** of what’s going on inside it.

The idea of separating code into sections, with clearly defined roles and interfaces, is common to the wide variety of programming languages and development patterns in use; for example, [model-view-controller](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller "Wikipedia: Model View Controller") architecture, and programming paradigms used with language types such as [declarative](https://en.wikipedia.org/wiki/Declarative_programming "Wikipedia: Declarative Programming") and [imperative](https://en.wikipedia.org/wiki/Imperative_programming "Wikipedia: Imperative Programming"). Object-oriented programming is one of the many styles of [structured](https://en.wikipedia.org/wiki/Structured_programming "Wikipedia: Structured Programming") programming.

Say you were writing code for a payroll system and wanted to find out how much tax an employee has to pay. The code that handles wage calculations could contain a function written in this form (pseudo-code):

<pre><code class="language-javascript">number getTaxAmount(number topLine)</code></pre>

This means that external code can call the `getTaxAmount` function, passing the employee’s total wage figure (`topLine`) as a parameter and getting the amount of tax returned as a number. How `getTaxAmount` works out the amount of tax owed is irrelevant from the point of view of the “customer” code. All it needs to know is:

*   What the function is called,
*   What the parameters are,
*   What it returns, and
*   What its purpose is (which would hopefully be outlined in an informative comment, although this doesn’t always happen.)

If this isn’t making much sense to you, don’t worry. Having these concepts in mind as you work with code will eventually pay off. It’s an area where learning the theory before the practice can sometimes be helpful for beginners.

### Interfaces

Let’s use a car analogy to illustrate this. When you learn to drive a car, you learn what the controls are, how to access and use them, and what their general purpose is. For example, you know that pressing the accelerator generally makes the car speed up. But you don’t need to know *how* the accelerator makes the car speed up in order to effectively use the car.

<figure><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/26e77621-c75b-441b-8425-7a855312facb/tools.jpg" alt="Tools"/><figcaption>You don’t have to know how it works, as long as you know how to achieve the desired result. (Image: <a href="https://www.flickr.com/photos/vincentxrevolution/3677029410/in/photostream/">Vincent X</a>.)</figcaption></figure>

Looking at both the tax code example and the car analogy, we can say that the reason that these functions are usable is that, from an external perspective, the **interface** is clear. The interface is the point of access for the user: the controls in the case of the car, and the function outline (or [signature](https://en.wikipedia.org/wiki/Signature_%28computer_science%29 "Wikipedia: Signature")) in the case of the payroll system. You can make use of the functionality of a chunk of code **as long as you understand how to access its interface**. This is a basic principle in many of the development patterns you’ll come across when reading code, both server-side with languages such as PHP and ASP, and client-side with languages such as JavaScript.

So, when developers work on substantial applications, they can usually make use of code written by someone else with relative ease, so long as the interface for the code is **well defined** (and, ideally, commented). Again, all they need to know is what it does at an abstract, generalized level, what inputs it takes (for example, the parameters) and what it returns.

### What Does This Have To Do With Anything?

Okay, let’s see how this applies to working with other people’s code. However a piece of code has been developed, when you’re working with it, chances are you will only really need to understand certain elements in order to make good use of it. Bearing the development concepts in mind, you can **focus your reading of the code** on those few relevant areas. Learn to see code in terms of the visible interfaces (for example, function outlines, variables that are particularly visible or persistent, and class declarations, if applicable), and don’t waste time looking into their details unless you have to.

The rest of this article runs through some of the key skills involved in reading code.

Software developers working on big applications typically program on a team, and these skills are picked up naturally. When you code on a more casual basis, you can still pick up the skills, but you may just need to consciously focus on them at first. The more experience you gain, the more automatic these practices become.

If you’ve ever used a code library (jQuery, for example, or another JavaScript resource) and have called on it on one of your Web pages, then you’ve accessed its functionality in much the same way as what’s outlined above. You’ve **called on it through a defined interface**; in this case, whatever code you included in the HTML to use it, even if just a link to a script in the header of the page.

## Some Useful Habits

Before we get to specific tips, let’s go over some general habits that will help when you try to make sense of an external library or other code.

### Be a Reader

Get into the habit of reading other people’s code, even when you don’t have to. Life’s too short, you say? Give it a try anyway; it’s less of a punishment than you may think! If you see some functionality on a website that fascinates you, look at the code if it’s visible.

<figure><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/737b1394-5386-40e3-be0f-606121ab816a/source1.jpg" alt="Source Code"/><figcaption>Taking a peek at the source code on the jQuery Thickbox page.</figcaption></figure>

If you’re new to programming, most of the code you look at won’t make much sense at first, but you might be surprised by how your brain soaks it up. The more code you look at, the more attuned you become to processing it visually. Few professional writers would feel equipped to do their job if they didn’t spend time reading the work of other writers. Why is coding any different?

Browser tools like [Firebug](https://getfirebug.com/ "Firebug") are really useful here, because they let you hone in on exactly the bits of code that you’re interested in, ignoring the rest. If you work with, or are interested in working with, certain technologies, focus on them. Most websites are made up of many different elements, so **don’t waste time reading stuff you’re unlikely to use**. If you’re only interested in client-side scripts, just look at those. For server-side code, there are many freely downloadable scripts you can look at.

<figure><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94fe5abb-09fb-41d3-b145-d0953b9824cf/firebugshot1.png" alt="Firebug"/><figcaption>Firebug enables you to view the mark-up of each element on a Web page, in this case the <a href="https://www.bbc.co.uk/news/">BBC News</a>.</figcaption></figure>

### Learn a Bit More Than You Really Need To

As you start gaining development skills, particularly if you’ve mainly been a designer, you will typically use only **small isolated excerpts of code** at any one time. So, you may not become aware of the larger development concepts at work in the language. Having a casual look at the structure of an application that’s larger than what you’re used to is a great way to acquaint yourself with these patterns.

On a similar note, it’s also worth finding out, at least in theory, about the types of development models that a language is used with. It may seem that higher-level concepts are not relevant to smaller tasks, but being *aware* of them is useful no matter how small or big your projects are. As time passes, you may find yourself working on bigger systems anyway.

<figure><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75af35cf-ab3e-4f16-ae97-cdfed1dd6ec7/coding-one.jpg" alt="Smashing Magazine Site DOM"/><figcaption>A look at Smashing Magazine’s website DOM, an interactive way to explore how a website’s various elements relate to each other.</figcaption></figure>

I know that spending time reading code voluntarily may be hard to justify when you’re up against a deadline, trying to get a decent hourly rate, perhaps pay the rent and eat once in a while. But the habit really will save you time and stress down the line. You have to spend only a couple of minutes here and there to benefit from it.

{{% ad-panel-leaderboard %}}

### See Through Someone Else’s Eyes

Any development project is a **problem-solving** exercise. When you approach your own projects, you inevitably view them from your own angle. Moreover, programming is a linguistic activity, not unlike natural language, and there are typically many ways to express the same thing.

The downside to this is that another person’s code can seem impenetrable, because it’s specific to that individual’s point of view. The upside is that looking at how someone else has solved a problem invariably opens your mind to **new possibilities**. As with natural language, the fact that we all have different perspectives does not prevent us from being able to communicate, because we have a **shared discourse** that is understood.

Observe the ways in which code solves problems, particularly when the approach is unfamiliar to you, and especially when the code achieves functionality that you have attempted yourself. Consider how you might have approached the task, and in doing so learn something about how your brain **breaks up** the tasks involved in addressing coding problems. If nothing else, you might pick up a few tricks and time-saving bits of syntax.

## Tips For Working With External Libraries And Other Code

If you’ve ever sat down to use a code library and found yourself struggling to understand it well enough to make good use of it, here are a few tips to help.

### Examine The Evidence

Your first point of access to a code library should generally be the **documentation and comments** that come with it. I say “should” because as we all know they are sometimes lacking. But it’s always worth a look, and well-documented code makes a huge difference.

<pre><code class="language-javascript">/* Here is an informative comment explaining the
*  function that the code appears before, indicating,
*  its logic, purpose, parameters and anything returned.
*/
function greatFunction(someInput)
{
 //What's happening and why
 var someElement = document.getElementById(someInput);

 //and so on…
}</code></pre>

**Don’t take comments as gospel**. Programmers are only human (insert your favorite joke here), and comments often get out of sync with code, especially when changes are made and the comments are not updated.

### Stick To The Path

Don’t try to read code linearly as it appears in scripts. Read it in the **order of execution**, starting from obvious entry points. If a library provides instructions on how to carry out certain tasks, for example, start from the function calls that are specified, and work through what happens from there.

Typically with a JavaScript or PHP library, you’ll be adding some function call or link to your HTML or server-side script. So, in the first instance, look for the origins of any such calls in the source code. Again, browser tools and IDEs can be really helpful here. Follow the **train of logic** from your entry point through to any other functions that are being called in turn. Take your time, and build a picture.

Let’s work through an example: the [jQuery plug-in for SuperSleight](https://allinthehead.com/retro/338/supersleight-jquery-plugin "jQuery Supersleight") for handling PNG transparency in IE6\. To use this plug-in, you link to the script in the header of the page and add the following function call in your page’s script:

<pre><code class="language-javascript">$('#content').supersleight();</code></pre>

To see what happens when this function is executed, look in the _supersleight.js_ script for the function being called (`supersleight`) and see what happens in there. You’ll see that it contains further function calls and processing, some of which in turn refer to the jQuery script itself. Here is the start of the function:

<pre><code class="language-javascript">jQuery.fn.supersleight = function(settings) {
 settings = jQuery.extend({
 imgs: true,
 backgrounds: true,
 shim: 'x.gif',
 apply_positioning: true
 }, settings);

 return this.each(function(){
 //…</code></pre>

Naturally, you can look up the details of the internal function calls if you wish, although you’ll find that the jQuery script is a little more difficult to read!

The point is that if you want to make sense of code without tearing your hair out, you need to read it in the order in which it will be processed. With Firebug, you can speed up the process using the “DOM” and “Script” tabs. Many of the other browser plug-ins for Web development, such as [Web Developer](https://addons.mozilla.org/en-US/firefox/addon/web-developer/ "Web Developer") and [Web Inspector](https://www.apple.com/safari/features.html "Web Inspector"), have similar functions. For server-side code, an IDE serves this function.

### Give Yourself Some Clues

If the code you’re working with has a long complex flow of execution, then adding **trace statements** can be useful. Trace statements are a way to find out what is happening at particular points in the logic of a program. An example of a trace statement would be writing out the value of a variable at some point in the execution, perhaps for an alert dialog in JavaScript code, as in this example:

<pre><code class="language-javascript">function someFunction(aParameter)
{
 alert("parameter value: "+aParameter);
 //other processing…
}</code></pre>

You can use trace statements to check variable values (as above), to test whether functions are being called, or for anything else you find helpful. Adding trace statements at **key points** in a piece of code and then running the code can give you a good sense of the functionality at work.

If you add a trace statement to a function that you believe is being called, and then the trace is not outputted, this is an indicator that something has gone wrong at some point in the code before the trace statement. In this case, you can move the trace statement to an earlier point of execution and see if it runs there, which might give you a better idea of where the code is breaking down. For example, let’s say you have the following function being called on a page:

<pre><code class="language-javascript">function someFunction(aParameter)
{
 document.getElementById("thing").style.color="#330000";
 alert("parameter value: "+aParameter);
 //other processing…
}</code></pre>

If you test the page and the alert dialog does not appear, then something went wrong before it was called. If you move the alert call to one line earlier in the script (i.e. swap lines 3 and 4), and it does appear, then you know something is wrong with the line you just moved it in front of. If the alert still does not appear, then chances are the function is not being called and you need to have another look at wherever the call originates.

This is a simple example, but the practice of using trace statements is useful even if you’re not working with much programming code. The alert function is obviously intrusive at times, so an alternative to consider is the [console.log()](https://getfirebug.com/logging "Logging with Firebug") function, which you can use to send messages to Firebug. A number of other advanced debugging tools for JavaScript are illustrated in “[JavaScript Debugging for Beginners](https://www.webmonkey.com/2010/02/javascript_debugging_for_beginners/ "JavaScript Debugging for Beginners"),” by Webmonkey.

### Isolate Trouble Spots

If any sections of code are particularly baffling, copy them into a separate script and run them from there. Experiment with the code in this second file to see if you can get an idea of what’s going on.

Consider the `someFunction` function above. If you were having trouble getting to grips with it, you could copy it into a new JavaScript file, add a link to the new file in your page’s header, and then explicitly call the function in the HTML, as in this example:

<pre><code class="language-markup tmp-xml"><a id="link1" onmouseover="someFunction(this.id)" href="somelocation.html">Hover to test</a></code></pre>

In this case, you know the function is being called when you hover over the link, and you can control the parameter to see how it functions.

Remember, you don’t need to understand every detail of a script in order to get good use out of it, so take the time to do it only if it’s really necessary. Don’t worry about utility functions that have little bearing on the code you’re interested in.

### Consider The Context

Whenever you try to process code mentally, take an approach that is appropriate to the platform and context. If you have a general idea of **what the code is for**, keep this in mind as you read it, because it will continually provide clues to the logic at work.

Familiarize yourself with the **programming and naming conventions** of the language in question. Most languages have [standards and conventions](https://en.wikipedia.org/wiki/Naming_convention_%28programming%29 "Wikipedia: Programming Naming Convention") for naming variables, files, classes, functions and whatever else they use. Grasping these makes reading the code far easier.

There’s no guarantee that the other programmer will have adhered to these recommendation, but for many of the most widely used code libraries, they will have. Some programmers have their own rules for naming code elements, which can bring consistency even if it isn’t the standard. Naturally, it helps if the names are meaningful.

Here are a few conventions. In JavaScript, names for variables and functions typically use CamelCase:

<pre><code class="language-javascript">//variable
var myFirstName

//function
function doSomeAction

//as in Java, class names often start uppercase
function MyClass</code></pre>

In PHP, you may come across the following conventions (the underscore is also common in names of SQL database tables and columns):

<pre><code class="language-php">//variable
$my_first_name

//function
function doSomeAction

//class
class My_Class</code></pre>

You’ll come across many more conventions in the different languages, and the extent to which programmers adhere to them varies greatly. But hey, if the Internet wasn’t a complete mess, so many fantastic things wouldn’t have come of it.

### Step Back

When you read a section of code, you really want a sense of the overall structure. For this reason, it can be useful to step back, literally, by **zooming out** from the text. Many experienced developers swear by this technique, and all you need to do is open the code in an editor with zoom controls and then zoom out until it’s really small. Don’t worry if you can’t read the details; you’re aiming for an overview.

The more programming code you read (as opposed to mark-up), the more you’ll get into the habit of seeing the **structures, shapes and patterns** at work. For example, as a non-programmer, you would read a JavaScript file like a natural language: starting at the top, focusing initially on the first few lines, which perhaps contain a list of variable names and other details that are not generally significant. If you read the same file from a coder’s perspective, you’d initially see the functions, loops, conditionals, etc., and the code’s defining structures.

Unlike with a natural language, you can grasp some level of meaning in an excerpt of code by looking at these larger structures. With natural language, meaning is contained primarily at the level of words and sentences. So, you need to make a slight **mental adjustment** when reading code.

Look at this example PHP code:

<pre><code class="language-php">$first_name="John";
$last_name="Smith";
$age=11;
function doSomethingPointless()
{
 $count=0;
 while($count&lt;$age)
 {
  echo $first_name." ".$last_name." ";
  $count++;
 }
}</code></pre>

If someone who is totally unfamiliar with code saw this, the first thing they would likely focus on is the list of variables at the top. For someone more accustomed to working with code, they would notice the structure (i.e. the function with a loop inside it).

### Focus

Bearing in mind the development concepts outlined above, focus your reading on those areas that are most likely to be relevant to you. Look at the level of files, classes, functions, variables and obvious entry points, as illustrated in the “Stick to the Path” section above. You can make use of an external library even by ignoring most of it.

### Take a Snapshot

If the code you’re working with is for a big application and you need a good grasp of its overall structure, try **scribbling down an impression** of it, either textually or as a rough diagram. The act of sketching the application’s structure is a good way to impress it on your mind so that it persists when you get to working with the code.

A sketch of an application or code elements could involve writing the names of classes, files, functions or variables, and illustrating the relationships between them with connecting lines. This is most likely to be useful if you’ve been working with code for a while. (See the LinkedIn UML-class diagram near the top of this article for inspiration on this.)

### Look Away Now

Sometimes you need a break from staring at code to give your brain a chance to make sense of it. There will almost certainly be times when you feel you’re getting nowhere. I often find that when I take a break and come back, I’ve actually understood more than I thought.

### Just in Case

This one may seem obvious, but if you’re making changes to code, keep copies of the original for reference. Losing track of what you’ve added and what was already there is a recipe for stress.

### Advanced Tools

For more advanced programmers, a number of software tools can help when you’re trying to make sense of a big application. Naturally, developing your project in an [integrated development environment](https://en.wikipedia.org/wiki/Comparison_of_integrated_development_environments "Wikipedia: Comparison of integrated development environments") (IDE) such as [Eclipse](https://www.eclipse.org/) or [NetBeans](https://netbeans.org/index.html "NetBeans") helps, because it makes the code more easily navigable by highlighting various types of relationship between elements.

<figure><img src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/754364e2-56a9-4f08-baeb-3c0c50c27de9/coding-two.jpg" alt="Eclipse Screenshot"/><figcaption>One of my Android projects open in the Java browsing view in Eclipse looking at a method’s call hierarchy.</figcaption></figure>

Additional tools for reading code employ different approaches and are designed to suit different languages, but in most cases they use some sort of visualization technique to help you wrap your head around it.

Here are a few related resources:

*   [Grok2: Source Code Comprehension Tools](http://www.grok2.com/code_comprehension.html)  
    A rundown of many source-code reading tools.
*   [University of British Columbia: Source Code Comprehension Tools](https://www.cs.ubc.ca/~murphy/cs319/index.html)  
    An overview and analysis of code reading tools.
*   [Source Insight Program Editor and Analyzer](https://www.sourcedyn.com/)  
    Project-oriented program code editor and code browser for C, C++, C#, Java and more.
*   [AspectBrowser for Eclipse](https://cseweb.ucsd.edu/~wgg/Software/AB/)  
    A visualization tool for Eclipse.
*   [Cscope](https://cscope.sourceforge.net/)  
    A developer’s tool for browsing source code.

## Don’t Let It End There

It’s easy to see working with other people’s code as a necessary evil, but I genuinely believe that it’s a valuable exercise in and of itself. When you work on Web projects, particularly as a freelancer, you often end up working in a vacuum, which is not always good for your professional development. Exposing yourself to new code (rather than to passers-by when you finally lose it!) is a great way to absorb **good practices and varied perspectives**.

Ultimately, the skills you learn from working with other people’s code should feed back into your own code-writing habits. Few of us have been spared the experience of staring at a piece of code we wrote ourselves only a few short days, hours or even minutes before and wondering what we were thinking. If you think like both a reader and a writer, you will ultimately create something that is **better structured, more reliable and that you’d be happy for other developers to look at**.

Go on. It’s fun. Honest! Embrace your inherent geekery, and develop an unquenchable love for code.

## Other Resources

Some related material on reading code and working with other people’s code in general:

*   “[The P.G. Wodehouse Method of Refactoring](https://basildoncoder.com/blog/2008/03/21/the-pg-wodehouse-method-of-refactoring/),” Basildon Coder  
    Exploring the trials and tribulations of working with legacy code.
*   “[Code Reading: The Open Source Perspective](https://www.spinellis.gr/codereading/),” Spinellis  
    A seminal text on code reading.
*   “[Why I Love Reading Other People’s Code and You Should Too](https://www.skorks.com/2010/05/why-i-love-reading-other-peoples-code-and-you-should-too/),” Skorks  
    A celebration of code reading, with helpful tips.
*   “[How to Read Other People’s Code, and Why](https://designbygravity.wordpress.com/2009/10/23/how-to-read-other-peoples-code-and-why/),” Design by Gravity  
    Overview of the key principles of reading code.
*   “[Tips to Read Other People’s Code](https://coliveira.net/software/tips-to-read-other-peoples-code/),” Carlos Oliveira  
    An accessible list of code-reading tips.
*   “[Tips for Reading Code](http://wiki.c2.com/?TipsForReadingCode),” Cunningham & Cunningham  
    Another rundown of code-reading principles.
*   “[Hell Is Other People’s Code](http://exodusdev.com/blog/mike/hell-is-other-peoples-code),” Exodus Development  
    A fun rant about the downside.

Material related to other topics touched on in this article:

*   “[Introduction to OMG’s Unified Modeling Language](https://www.omg.org/gettingstarted/what_is_uml.htm)”  
    An accessible introduction to UML.
*   “[Design Patterns](https://sourcemaking.com/design_patterns),” SourceMaking  
    A very readable overview and analysis of design patterns.
*   “[Programming Paradigm](https://en.wikipedia.org/wiki/Programming_paradigm),” Wikipedia  
    An introduction to programming paradigms.

{{% ad-panel-leaderboard %}}

### Further Reading

*   [jQuery and JavaScript Coding: Examples and Best Practices](https://www.smashingmagazine.com/2008/09/16/jquery-examples-and-best-practices/ "jQuery and JavaScript Coding: Examples and Best Practices")  
    A rundown of guiding principles and practices for both tools.
*   [What Is the Worst Design or Programming Mistake You’ve Ever Made?](https://www.smashingmagazine.com/2010/09/10/what-is-the-worst-design-or-programming-mistake-you-ve-ever-made/ "What Is The Worst Design or Programming Mistake You’ve Ever Made?")  
    Yet more proof that learning to program is primarily about learning to find the mistakes you’ve made.
*   [Getting Started With Ruby on Rails](https://www.smashingmagazine.com/2009/03/19/getting-started-with-ruby-on-rails/ "Getting Started With Ruby On Rails")  
    While specifically about Ruby On Rails, this article covers general Web application development concepts.
*   [PHP: What You Need to Know to Play With the Web](https://www.smashingmagazine.com/2010/04/15/php-what-you-need-to-know-to-play-with-the-web/ "PHP: What You Need To Know To Play With The Web")  
    A great first guide to using PHP.
*   [YQL: Using Web Content for Non-Programmers](https://www.smashingmagazine.com/2010/12/21/yql-using-web-content-for-non-programmers/ "YQL: Using Web Content For Non-Programmers")  
Tips on using Web content that are very accessible to those without development experience.

{{< signature "al, mrn" >}}

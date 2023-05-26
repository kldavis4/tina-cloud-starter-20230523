---
title: Introduction To Developing Fireworks Extensions (They're Just JavaScript!)
slug: introduction-to-developing-fireworks-extensions-theyre-just-javascript
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c68e5bb3-815b-4702-9cde-61fbe032aff5/illu-fireworks.jpg'
date: 2014-06-04T20:32:50.000Z
author: dmitriy-fabrikant
description: >-
  One of the most powerful features of Adobe Fireworks is that you can extend
  its functionality. Almost anything you can do through Fireworks’ interface —
  and even some things that you can’t — can also be achieved by writing a simple
  JavaScript extension.

  **Fireworks extensions are of two main types: commands and command panels**.
  If you find yourself repeatedly performing a tedious task, you could write a
  command to automate the process and save yourself a lot of time.
  Alternatively, if you are missing a particular feature that would improve your
  workflow, you could write a more complex extension — a command panel — to
  implement it.
categories:
  - Fireworks
  - JavaScript
  - Tutorials
  - Extensions
---
One of the most powerful features of Adobe Fireworks is that you can extend its functionality. Almost anything you can do through Fireworks’ interface — and even some things that you can’t — can also be achieved by writing a simple JavaScript extension.

<strong>Fireworks extensions are of two main types: commands and command panels</strong>. If you find yourself repeatedly performing a tedious task, you could write a command to automate the process and save yourself a lot of time. Alternatively, if you are missing a particular feature that would improve your workflow, you could write a more complex extension — a command panel — to implement it.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Developing A Design Workflow In Adobe Fireworks](https://www.smashingmagazine.com/2012/06/developing-a-design-workflow-in-adobe-fireworks/)
*   [Switching From Adobe Fireworks To Sketch: Ten Tips And Tricks](https://www.smashingmagazine.com/2015/10/switching-adobe-fireworks-sketch-10-tips-tricks/)
*   [The Present And Future Of Adobe Fireworks](https://www.smashingmagazine.com/2013/12/present-future-adobe-fireworks/)
*   [The Power of Adobe Fireworks: What Can You Achieve With It?](https://www.smashingmagazine.com/2010/09/the-power-of-adobe-fireworks-what-can-you-achieve-with-it/)

I learned to develop Fireworks extensions by writing the <a href="https://www.smashingmagazine.com/2012/05/25/blueprints-for-the-web-specctr-adobe-fireworks-plugin/">Specctr plugin</a>. While working on Specctr, I’ve witnessed Fireworks’ passionate community actively support the app — an app that has been widely overlooked by Adobe. (Sadly, Fireworks CS6 is the <a href="https://www.smashingmagazine.com/2013/12/19/present-future-adobe-fireworks/">last major release</a> from Adobe, but it is still available as a standalone application and through Creative Cloud. Adobe plans to support Fireworks at least through the next major releases of Mac OS X and Windows OS and to release bug fixes and patches for it.)

{{% feature-panel %}}

Although Fireworks is an excellent screen design tool out of the box, it has benefited greatly from contributions from the Fireworks community — namely, developers such as <a href="https://johndunning.com/fireworks/">John Dunning</a>, <a href="https://fireworks.abeall.com/extensions/">Aaron Beall</a> and <a href="https://mattstow.com/">Matt Stow</a>, among others, who have written many indispensable extensions, such as <a href="https://johndunning.com/fireworks/about/SVG">SVG Import</a> and <a href="https://fireworks.abeall.com/extensions/commands/Export/">SVG Export</a> (which add full-featured SVG support to Fireworks), <a href="https://johndunning.com/fireworks/about/GenerateWebAssets">Generate Web Assets</a>, <a href="https://mattstow.com/css-professionalzr.html">CSS Professionalzr</a> (which extends the features of the <a href="https://helpx.adobe.com/fireworks/learn/tutorials/how-to/extract-css-properties.html">CSS Properties</a> panel to Fireworks CS6) and many more.

Now that we can’t expect Adobe to add any more features to Fireworks, the ability to extend the app becomes even more important, because many designers still rely on it (while looking for alternatives, of course, such as <a href="https://www.bohemiancoding.com/sketch/">Sketch 3.0</a>), and <strong>through extensions, new features and panels</strong> can be added. This article is aimed at those interested in developing extensions for Fireworks. We’ll introduce the JavaScript underpinnings of Fireworks and, in the process, write a few JavaScript examples to get you started.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/058b0ca0-a4c7-4255-a396-c396a53984c6/01-copy-paste-opt.gif" alt="Now that Adobe won't add more features to Fireworks, the ability to extend the app becomes important." width="500" height="240" /><br>
<figcaption>Now that Adobe won't add more features to Fireworks, the ability to extend the app becomes important.</figcaption><figure>This article will cover the following:
<ul>
 	<li>using the History panel to see how user actions map to JavaScript code;</li>
 	<li>exploring the JavaScript code that moves an element on the canvas, to gain insight into Fireworks’ document object model (DOM);</li>
 	<li>using Fireworks’ Console extension to run and debug extensions;</li>
 	<li>using the DOM Inspector extension to debug and develop extensions;</li>
 	<li>writing a simple extension to increase a document’s canvas size automatically.</li>
</ul>
Let’s get started!
## Do You Speak JavaScript? Fireworks Does!

Fireworks speaks JavaScript. It exposes a JavaScript <a href="https://en.wikipedia.org/wiki/Application_programming_interface">application programming interface</a> (API) via <a href="https://help.adobe.com/en_US/fireworks/cs/extend/index.html">Fireworks’ document object model</a> (DOM), which represents its constituent parts and functions. That’s a long way of saying that you can write JavaScript to tell Fireworks what to do.

Fireworks lets you run the JavaScript in two basic ways: commands and command panels.
### Commands
The first option is to execute JavaScript as commands. Commands are simple text files that contain JavaScript and that are saved with a <code>.jsf</code> extension. To make them available from the “Commands” menu in Fireworks, you must save them in the <code>&lt;Fireworks&gt;/Configuration/Commands/</code> directory (where <code>&lt;Fireworks&gt;</code> is a stand-in for the installation directory of Adobe Fireworks on your computer — see “A Note on Locations” below).
### Command Panels
The second option is to build a command panel. Command panels are Flash panels powered by <a href="https://en.wikipedia.org/wiki/ActionScript">ActionScript</a>, which in turn can call JavaScript code to boss Fireworks around. Fireworks has an embedded Flash player and can run these panels. The panels are in SWF format and should be saved in the <code>&lt;Fireworks&gt;/Configuration/Command Panels/</code> directory so that they can be accessed from the “Window” menu in Fireworks.
## A Note On Locations

Below are the exact locations of the <code>Commands</code> and <code>Command Panels</code> folders on both Mac and Windows.
### Mac OS X
<ul>
 	<li><code>/Applications/Adobe Fireworks CS6/Configuration/Commands/</code></li>
 	<li><code>/Users/&lt;USERNAME&gt;/Library/Application Support/Adobe/Fireworks CS6/Commands/</code></li>
 	<li><code>/Applications/Adobe Fireworks CS6/Configuration/Command Panels/</code></li>
 	<li><code>/Users/&lt;USERNAME&gt;/Library/Application Support/Adobe/Fireworks CS6/Command Panels/</code></li>
</ul>
### Windows
Windows 8.1, 8, 7, Vista and 64-bit (for 32-bit, simply remove the <code> (x86)</code>):
<ul>
 	<li><code>C:\Program Files (x86)\Adobe\Adobe Fireworks CS6\Configuration\Commands\</code></li>
 	<li><code>C:\Users\&lt;USERNAME&gt;\AppData\Roaming\Adobe\Fireworks CS6\Commands\</code></li>
 	<li><code>C:\Program Files (x86)\Adobe\Adobe Fireworks CS6\Configuration\Command Panels\</code></li>
 	<li><code>C:\Users\&lt;USERNAME&gt;\AppData\Roaming\Adobe\Fireworks CS6\Command Panels\</code></li>
</ul>
Windows XP:
<ul>
 	<li><code>C:\Program Files\Adobe\Adobe Fireworks CS6\Configuration\Commands\</code></li>
 	<li><code>C:\Documents and Settings\&lt;USERNAME&gt;\Application Data\Adobe\Fireworks CS6\Commands\</code></li>
 	<li><code>C:\Program Files\Adobe\Adobe Fireworks CS6\Configuration\Command Panels\</code></li>
 	<li><code>C:\Documents and Settings\&lt;USERNAME&gt;\Application Data\Adobe\Fireworks CS6\Command Panels\</code></li>
</ul>
## How To Choose Between Commands And Command Panels

When should you write a command, and when should you write a command panel?

Generally, a command is useful for automating some action that requires no or very little user input, such as <a href="https://johndunning.com/fireworks/about/GroupCommands">pasting elements into an existing group</a> or quickly <a href="https://fireworks.abeall.com/extensions/commands/Layer/">collapsing all layers</a>. A command is also easier to build and test.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ccb0331b-c018-42ea-a2f0-d5e066267185/02-specctr-panel-opt.png" alt="The Specctr panel." width="500" height="328" /><br>
<figcaption>The Specctr panel.</figcaption><figure>But if the action you’d like to automate requires a lot of user interaction or if you would like to organize a group of commands in one place for quick access, then you might want to build a command panel instead. For example, the Specctr panel that I made groups together a number of JavaScript commands and can be configured by the user (such as when setting a specification’s color or when setting the amount by which to increase the margins around the canvas to make room for a generated specification). So, opting for a command panel was obvious in this case. Commands panels are more complex and require more time to develop and test.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1614cfd3-a39e-451d-bd5d-408524412e89/03-specctr-canvas-expand-opt.png" alt="Specctr canvas expand feature" width="500" height="150" /><br>
<figcaption>The “Expand Canvas” feature in the Specctr plugin.</figcaption><figure>The “Expand Canvas” functionality in Specctr was the inspiration for some of the functionality that we will learn to implement in this article.

Regardless of whether you write a command or build a command panel, you will be interacting with Fireworks via JavaScript. Now let’s peek inside Fireworks’ JavaScript heart!

<strong>Note:</strong> How to build a command panel is beyond the scope of this article. We’ll focus instead on the basics of developing a Fireworks extension and how to write your first extension. To learn more about command panels, do check out Trevor McCauley’s excellent article “<a href="https://www.adobe.com/devnet/fireworks/articles/creating_panels_pt1.html">Creating Fireworks Panels</a>.”
## History Panel

The History panel in Fireworks provides an easy way to examine the JavaScript running behind the scenes.

As a quick example, open the History panel (<code>Window → History</code>), select a text element and then move it anywhere on the canvas.

A “Move” item will be added to the list of actions in the History panel.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d218fcd8-985c-48db-9407-d54075a3ad83/04-history-panel-opt.gif" alt="History Panel - a move item in the list" width="500" height="240" /><br>
<figcaption>In the History panel, select and move a text object. A “Move” item will then be added to the steps in the history. You can also select and “replay” a history step (or set of steps).</figcaption><figure>This History panel entry represents the JavaScript code corresponding to the action you have performed.

Next, click the “Copy steps to clipboard” button in the bottom-right corner of the History panel, and paste it in the text element that you’ve just moved (i.e. replacing the “Move Me!” text).

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8db4478a-497e-40d3-9838-f7e2a5ab1a45/05-history-panel-opt.gif" alt="History panel: copy and paste an item from the history." width="500" height="240" />In
<figcaption>the History panel, copy and paste a history item as simple JavaScript code.</figcaption><figure>Voilà, the code! This is a quick way to see the <a href="https://help.adobe.com/en_US/fireworks/cs/extend/WS5b3ccc516d4fbf351e63e3d1183c94856c-7c8c.html">JavaScript</a> that represents the actions you perform through the user interface in Fireworks.

If you moved an object 2 pixels to the right (along the x-axis) and 46 pixels down (along the y-axis), this is how the JavaScript code would look:

<pre><code class="language-javascript">
fw.getDocumentDOM().moveSelectionBy({x:2, y:46}, false, false);
</code></pre>

We can save this code to Fireworks’ “Commands” menu by clicking on the “Save steps as a command” button in the bottom-right corner of the History panel.

Once this simple command has been saved to the <code>Commands</code> folder, you’ll be able to run it from the “Commands” menu, use it in more complex Fireworks batch-processing scripts and more. Whenever run, the command will move any selected object on the canvas 2 pixels to the right along the x-axis and 46 pixels down along the y-axis. You can also easily customize this command by editing the <code>x</code> and <code>y</code> values in the <code>.jsf</code> file that Fireworks saved at the location described earlier in this article.

This was a very simple example, but it shows that developing a Fireworks extension is not that hard — at least not in the beginning!
## Fireworks Console

Let’s dig a bit deeper. When you’re developing an extension, being able to execute a one-off JavaScript command without having to save it to the “Commands” menu every time would be useful. To execute the “Move” command without having to first add it to the “Commands” menu, let’s install John Dunning’s <a href="https://johndunning.com/fireworks/about/FWConsole">Fireworks Console</a> extension. This command panel has a text input that lets you type arbitrary JavaScript code and run it by clicking the “Eval” button.

Make sure to select the text element (the method is called <code>move<strong>Selection</strong>By</code>, after all) and paste the “Move” code into the Console. Then, hit “Eval” to run it.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/46829588-a936-4a74-91ff-eef348a7b73b/06-fireworks-console-opt.png" alt="Fireworks Console" width="500" height="220" /><figcaption>The Fireworks Console extension.</figcaption><figure>You should see the selected text on the canvas move 10 pixels to the right and 10 pixels down as Fireworks executes the JavaScript in the Console panel.

This is a great way to quickly test different commands and to make sure that the code you are working on actually does what it is supposed to do.
## Console Debugging

While building the Specctr panel, I used the JavaScript <code>alert</code> function to check the output of my code at various places in its execution.
### myCode.jsf

<pre><code class="language-javascript">
…
// Check the value of myVariable:
alert("my variable:", myVariable);
…</code></pre>

As in Web development, JavaScript alerts in Fireworks pause the code’s execution until you click to proceed. This means that if you had multiple values that you wanted to alert in the code, you would have to repeatedly press the “OK” button in the alert pop-up to continue executing the code.

Instead, we can use the panel to log our extension’s output to the console!

When the Console panel first launches, it introduces an object named <code>console</code> into Fireworks’ global namespace. This means that we can use the <code>console</code> object’s <code>log</code> function to log messages out to the Console panel’s output pane, as we’ll see now.
### myCode.jsf

<pre><code class="language-javascript">
…
console.log("myProgramVariable", myVariable);
…
</code></pre>

This doesn’t interrupt the code from executing. Because Fireworks does not provide any way for you to set breakpoints in the code, logging to the console is the method that I would recommend when debugging extensions.
## Fireworks DOM

Just as the <code>console</code> object is a JavaScript representation of Fireworks’ Console panel, the different concepts and functionality that make up Fireworks have JavaScript representations. This organization of JavaScript objects that models Fireworks’ behavior is called the Fireworks DOM.
### fw Object
We can see the DOM being accessed by our “Move” JavaScript code from earlier:

<pre><code class="language-javascript">
fw.getDocumentDOM().moveSelectionBy({x:2, y:46}, false, false);
</code></pre>

The <code>fw</code> object is a JavaScript object that models or represents Fireworks itself. It contains properties that describe Fireworks’ current state. For example <code>fw.selection</code> is an array that represents all of the currently selected elements on the canvas.

We can see this by selecting the text element that we’ve been working with and, in the Console panel, typing <code>fw.selection</code>, then clicking the “Eval” button. Here is the Console panel’s output:

<pre><code class="language-javascript">
[{
…
alignment: "justify",
face: "GillSans",
fontsize: "34pt",
…
}]
</code></pre>

In the output window, you should see a <a href="https://en.wikipedia.org/wiki/JSON">JSON</a> representation of the <code>fw.selection</code> array containing objects that symbolize each of the selected design elements on the canvas. (JSON is just a human-readable representation of JavaScript objects — in our case, the text element that we selected.)
### Viewing the DOM
When the formatting of the Console’s output gets too long, it leaves something to be desired. So, to see the properties and values of objects (object methods are not shown) in the Fireworks DOM, I use Aaron Beall’s <a href="https://fireworks.abeall.com/extensions/panels/#DOM-Inspector">DOM Inspector</a> panel, another indispensable companion in my journey of developing extensions.

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2f83aefc-41c8-4f79-9a20-f81cd9b39458/07-dom-inspector-opt.png" alt="DOM Inspector" width="500" height="180" /><br>
<figcaption>The DOM Inspector panel</figcaption><figure>Install the DOM Inspector panel, and then select the text object that represents the “Move” code (or any text object). Make sure that the drop-down menu at the top of the DOM Inspector panel is set to <code>fw.selection</code>. You should see an expanded <code>[object Text]</code> in the Inspector, along with all of its properties and values.

From the drop-down menu, I can select between viewing the contents of four objects:
<ul>
 	<li><code>fw.selection</code>
An array of currently selected elements on the canvas</li>
 	<li><code>fw</code>
The Fireworks object</li>
 	<li><code>dom</code>
The DOM of the currently active document (which we will discuss next)</li>
 	<li><code>dom.pngText</code>
A property of the currently active document (available for us to write to so that we can save data to the current document and retrieve it even after restarting Fireworks)</li>
</ul>
### Document DOM
In the DOM Inspector panel, we can switch to the <code>documentDOM</code> and explore its state. We can also access the <code>documentDOM</code> via JavaScript with the <code>getDocumentDOM()</code> method, as we did with the “Move” command:

<pre><code class="language-javascript">
fw.getDocumentDOM().moveSelectionBy({x:10, y:10}, false, false);
</code></pre>

The <code>getDocumentDOM()</code> method invocation returns only the DOM object of the currently active document, rather than the entire Fireworks DOM, and allows us to manipulate that document via its properties and methods. For example, the <code>moveSelectionBy()</code> method (which the History panel taught us about) does the work of moving elements around the document’s canvas.
### Selection Bias
Acting on the <strong>current selection</strong> is a common pattern when developing Fireworks extensions. It mirrors the way that the user selects elements on the canvas with the mouse, before performing some action on that selection.

<pre><code class="language-javascript">
fw.getDocumentDOM().moveSelectionBy({x:10, y:10}, false, false);
</code></pre>

The document DOM’s <a href="https://help.adobe.com/en_US/fireworks/cs/extend/WS5b3ccc516d4fbf351e63e3d1183c94856c-7c8c.html">moveSelectionBy()</a> function takes a JavaScript object as a parameter:

<pre><code class="language-javascript">
{x:10, y:10}
</code></pre>

Given an origin in the top-left corner, this tells Fireworks to move the selected object by <code>x</code> pixels to the right and by <code>y</code> pixels down.

The other two boolean parameters (<code>false</code>, <code>false</code>) indicate to <code>move</code> (as opposed to <code>copy</code>) the selection and to move the <code>entire element</code> (as opposed to a <code>sub-selection</code>, if any exists).

Like the <code>moveSelectionBy()</code> method, many other Document DOM <a href="https://help.adobe.com/en_US/fireworks/cs/extend/WS5b3ccc516d4fbf351e63e3d1183c94856c-7ffe.html">methods</a> act on the current selection (<code>cloneSelection()</code> and <code>flattenSelection()</code>, to name two).
## Expand Your Horizons (And The Canvas)

Using what we have learned so far, let’s write a simple command that will expand the size of our canvas.
### Canvas Size
To increase the size of the canvas, we need to know the current size. Our panel can call the JavaScript below to access the canvas’ current dimensions:

<pre><code class="language-javascript">
  var = canvasWidth = fw.getDocumentDOM().width;
  var = canvasHeight = fw.getDocumentDOM().height;
</code></pre>

Now, let’s see how to change these dimensions.
### Setting the Canvas’ Size
To set the canvas’ size, we call <a href="https://help.adobe.com/en_US/fireworks/cs/extend/WS5b3ccc516d4fbf351e63e3d1183c94856c-7a9e.html">the <code>setDocumentCanvasSize()</code> method</a> of the Document DOM.

<pre><code class="language-javascript">
fw.getDocumentDOM().setDocumentCanvasSize({left:0, top:0, right:200, bottom:200});
</code></pre>

The method takes a “bounding rectangle” as a parameter:

<pre><code class="language-javascript">
{left:0, top:0, right:200, bottom:200}
</code></pre>

The size of the rectangle will determine the new size of the canvas:

<pre><code class="language-javascript">
right - left = 200
bottom - top = 200
</code></pre>

Here, the rectangle is bounded by the object; therefore, the canvas is 200 × 200 pixels.
### Increasing the Canvas’ Size: A Simple Command
Let’s create a simple command that will double the canvas’ size automatically.

Instead of going through the <code>Modify → Canvas → Canvas Size</code> menu and then figuring out a width and height to input and then pressing “OK” whenever we want to increase the canvas’ size, we can combine the two code samples from above to create a quick shortcut to double the canvas’ size.

The code might look something like this:

<pre><code class="language-javascript">
// Double Canvas Size command, v.0.1 :)
var newWidth = fw.getDocumentDOM().width * 2;
var newHeight = fw.getDocumentDOM().height * 2;
fw.getDocumentDOM().setDocumentCanvasSize({left:0, top:0, right: newWidth, bottom: newHeight});
</code></pre>

I’m working on a Mac, so to make this command available from the “Commands” menu in Fireworks, I could save the code above as <code>double_size.jsf</code> in the following location:

<pre><code>/Users/&lt;MYUSERNAME&gt;/Library/Application Support/Adobe/Fireworks CS6/Commands/double_size.jsf
</code></pre>

(Check the beginning of the article to see where to save your <code>.jsf</code> commands if you are on a different OS.)

I leave it as an exercise for you to write and save a simple command that cuts the canvas’ size in half.
## Conclusion

We’ve covered quite a few things in this article:
<ul>
 	<li>With the help of the History panel, we’ve seen the JavaScript that makes Fireworks run.</li>
 	<li>We’ve broken down the JavaScript code needed to move a text element on the canvas, learned about the Fireworks DOM and seen how to manipulate it.</li>
 	<li>We’ve gone over how the Console panel executes and tests our JavaScript code. We’ve learned how to debug an extension by logging to the JavaScript <code>console</code> object that the panel introduces into Fireworks’ global namespace.</li>
 	<li>We’ve covered the DOM Inspector panel and how to use it to check the properties and values of various parts of the Fireworks DOM.</li>
 	<li>We’ve written a simple command to change the canvas’ size automatically.</li>
</ul>
Of course, we’ve just scratched the surface. These are just the basics to help you get started with developing Fireworks extensions. <strong>Use the techniques and resources in this article</strong> as a springboard to make more sophisticated extensions that will help you in your daily design work.

Another great way to learn more about Fireworks extensions is by deconstructing other extensions. Because Fireworks commands are simple JavaScript files, you could learn a lot by studying the code of other developers. I’d especially recommend the extensions created by the following people:
<ul>
 	<li><a title="John Dunning's Fireworks extensions" href="https://johndunning.com/fireworks/">John Dunning</a></li>
 	<li><a title="Matt Stow's Fireworks extensions" href="https://mattstow.com/fireworks.html">Matt Stow</a></li>
 	<li><a title="Aaron Beall's Fireworks extensions" href="https://fireworks.abeall.com/extensions/">Aaron Beall</a></li>
 	<li><a title="Trevor McCauley's Fireworks extensions" href="https://www.senocular.com/fireworks/extensions/">Trevor McCauley</a></li>
 	<li>Ale Muñoz</li>
</ul>
(The <span class="removed_link" title="https://www.projectphoenix.io/">Project Phoenix</span> extensions, recently rebooted by <a href="https://twitter.com/chunwui">Linus Lim</a>, are also worth mentioning. They include Font List, Super Nudge, Auto Save, Rename, Transform, Alignment Guides, Perspective Mockups, Retina Scaler, Layer Commands, Used Fonts and many others.)

Finally, below you’ll find an incomplete list of resources to help you along the way. If you think I’ve missed something important (or if you have any questions), let me know in the comments. I’d be happy to help.
### Further Reading
<ul>
 	<li>“<a href="https://help.adobe.com/en_US/fireworks/cs/extend/index.html">Extending Fireworks</a>,” Adobe
This is the official guide to developing extensions for Fireworks CS5 and CS6 (including the “<a href="https://help.adobe.com/en_US/fireworks/cs/extend/WS5b3ccc516d4fbf351e63e3d1183c94988d-7ff7.html">Fireworks Object Model</a>” documentation).</li>
 	<li><a href="https://www.fireworksguruforum.com/">FireworksGuru Forum</a>
Want to ask <a title="John Dunning's Twitter profile" href="https://twitter.com/fwextensions">John</a>, Aaron or <a title="Matt Stow's Twitter profile" href="https://twitter.com/stowball">Matt</a> a <a title="Forum section for Fireworks extension developers" href="https://www.fireworksguruforum.com/index.php?showforum=8">question</a>? You’ll probably find them here.</li>
 	<li>“<a href="https://github.com/fwextensions/fwjs-errata">Adobe Fireworks JavaScript Engine Errata</a>,” John Dunning
Dunning breaks down the quirks of the JavaScript interpreter that ships with Fireworks. Something not working as it should? Check it here. The list is pretty extensive!</li>
 	<li><a href="https://johndunning.com/fireworks/about/FWConsole">Fireworks Console</a>, John Dunning
This is a must-have if you write Fireworks extensions!</li>
 	<li><a href="https://fireworks.abeall.com/extensions/panels/#DOM-Inspector">DOM Inspector</a> (panel), Aaron Beall</li>
 	<li>“<a href="https://www.adobe.com/devnet/fireworks/articles/creating_panels_pt1.html">Creating Fireworks Panels, Part 1: Introduction to Custom Panels</a>,” Trevor McCauley
This was one of the first tutorials that I read to learn how to develop extensions for Fireworks. McCauley has written many cool extensions for Fireworks, and this article is an excellent read!</li>
</ul>

{{< signature "al, mb, ml" >}}

</figure></figure></figure></figure></figure></figure></figure></figure></figure></figure></figure></figure></figure></figure>


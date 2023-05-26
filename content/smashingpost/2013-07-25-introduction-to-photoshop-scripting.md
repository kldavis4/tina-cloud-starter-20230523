---
title: Introduction To Photoshop Scripts
slug: introduction-to-photoshop-scripting
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7c5a9bc1-626e-445b-984d-a7ecd1229af4/kamil-illu-3413.png
date: 2013-07-25T17:56:28.000Z
author: kamil-khadeyev
description: >-
  Automation is useful in the work of every designer. It saves precious time on
  repetitive tasks and helps us solve certain problems more quickly and easily.
categories:
  - Tools
  - Workflow
  - Photoshop
  - Graphic Design
---
Automation is useful in the work of every designer. It saves precious time on repetitive tasks and helps us solve certain problems more quickly and easily.

You can automate your workflow in Photoshop with actions, which are pretty popular and which most of you already know about and use. Today, we’ll introduce you to an advanced automation technique: Photoshop Scripts. All you need for this is basic knowledge of JavaScript, which some of us Web designers already have.

I’ve known about Photoshop scripts for years but decided to really dive in a few months ago. I had avoided it because I thought it was the domain of smart math-minded programmers. I was wrong, and today I’ll show that, although it requires some basic programming skills, scripting <strong>isn’t hard to grasp</strong>.

But first, we have to answer the obvious question.

{{% feature-panel %}}

## Why Do We Need Scripts?

Why should we would learn to script if Photoshop already has pretty nice actions? The answer is <strong>interactivity</strong>. When you use an action, you can’t really control how it behaves in different situations; it is like a videotape that just keeps playing again and again without any change.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8b3cbcfb-4a35-4106-abfb-3e6b534fd5f3/start-image-mini.png" alt="Photoshop Scripts" width="500" height="200" />

A script is more dynamic; its behavior changes according to the parameters you input or the context of its application. Sounds useful, no?

## Requirements

You don’t have to be an advanced programmer to be able to write scripts; I’m just a graphic designer, like most of you. But you should at least have a basic understanding of JavaScript and some experience with properties and methods to get the most out of this article.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/07e15ec2-ae11-4d4f-b7b8-9b88e202429e/smashingpost-requirements-mini.png" alt="Requirements" />

If you are not familiar with JavaScript at all, fear not! There are plenty of places to learn the basics of programming. <a href="https://www.codecademy.com/en/tracks/javascript">Codecademy</a>, for example, has pretty neat interactive lessons.

I work in Adobe Photoshop CS5, but everything we’ll cover applies to newer versions, too; Adobe hasn’t made any major updates to its scripting API since CS5. I will refer to the latest version of the scripting documentation, though, which is CS6.

## Getting Started

When you record actions in Photoshop, you set the order of the steps to achieve a certain result — that’s your <strong>algorithm</strong>. Then, you press “Record” and replicate them in Photoshop one by one. Scripting is similar, but instead of doing these steps in Photoshop, you write them down as lines of code. Most actions that you do in Photoshop have their own script equivalent as a function.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/db6987b9-eecd-401f-b694-96a02bd1e3d6/smashingpost-start-mini.png" alt="Start here" />

Let’s say you are creating an action that scales a document to 150% of its original size. You’d go through these steps:

1.  Open `Image → Image Size`.
2.  Enter `150%` in `width` and `height`.
3.  Hit “OK.”

The same process with a script would look like this:

1.  Call the application: `app`
2.  Target a document: `activeDocument`
3.  Call the function to resize the image: `resizeImage(width, height)`

And the code would look like this:

<pre><code class="language-javascript">app.activeDocument.resizeImage("150%", "150%");
</code></pre>

### Language

There are three ways to write scripts for Photoshop: using <strong>AppleScript</strong> on Mac, <strong>VBScript</strong> on Windows or <strong>JavaScript</strong> on either platform. I use the third because it is cross-platform and I already have some experience with it.

### Tools

Adobe has its own utility for writing scripts, called <strong>ExtendedScript Toolkit</strong>.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b02ecc9-a607-4773-9238-ecc21246e178/smashingpost-extendedtoolkit-big-mini.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4886d021-c009-4c56-91ae-d2f346501ce1/smashingpost-extendedtoolkit-small-mini.png" alt="Adobe ExtendedScript Toolkit" /></a><br>
<em>The main window for Adobe’s ExtendedScript Toolkit. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4b02ecc9-a607-4773-9238-ecc21246e178/smashingpost-extendedtoolkit-big-mini.png">View large version.</a>)</em>

The toolkit comes with Photoshop, and you can find it in the following folder:

*   Mac OS X `/Applications/Utilities/Adobe Utilities CS6/ExtendScript Toolkit CS6/`
*   Windows `C:Program FilesAdobeAdobe Utilities - CS6ExtendScript Toolkit CS6` (or `Program Files (x86)` for 64-bit machines)

The user interface of the ExtendedScript Toolkit is pretty straightforward. To start writing scripts, first select the target application in the drop-down menu. If Photoshop is running, then look for the green chain icon near the drop-down menu:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f44e9962-b6da-4a76-a330-0be8b8f92714/smashingpost-extendedtoolkit-app-mini.png" alt="Application Select" />

Now you can write something like this:

<pre><code class="language-javascript">alert("Hello Photoshop!");
</code></pre>

Press <code>cmd + R</code> (or just hit the “Play” button in the toolbar) to run your script. ExtendedScript Toolkit should switch to Photoshop and show an alert box:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c88c9b96-f393-4fbb-b161-d64275b0e3bf/smashingpost-alert0-mini.png" alt="Hello Photoshop!" />

ExtendedScript Toolkit has some other neat features for debugging scripts, but this is enough for this article. You can learn more about how to use it by going to <code>Help → JavaScript Tools Guide</code>.

You can use any plain-text editor to write a script; just save it as a <code>.jsx</code> file. To run it, you’ll have to go to <code>File → Scripts → Browse</code> in Photoshop and select it. Alternatively, just open the script file with Photoshop. You can also add a line of code at the top of the script so that the file always opens in Photoshop:

<pre><code class="language-javascript">#target photoshop
</code></pre>

Save your scripts in the <code>Photoshop/Presets/Scripts/</code> directory, and access them with <code>File → Scripts</code>. You can also set up a hotkey; just go to <code>Edit → Keyboard Shortcuts</code>, navigate to <code>File → Scripts → [your script’s name]</code>, and set the shortcut you want.

ExtendedScript Toolkit can run and debug code from the integrated development environment, and it has an object model viewer built in, which is useful. So, I recommend using the toolkit to write your scripts. Unfortunately, the Mac version crashes sometimes, so keep that in mind.

### Photoshop Object Model

To make writing scripts easier, you should understand how things relate to each other in Photoshop’s Document Object Model (DOM). Understanding it is not so hard if you look at Photoshop itself. The main object in Photoshop’s DOM is the application. In the application, we have a collection of documents that are currently open in Photoshop.

Each document contains elements — such as layers (called <code>ArtLayers</code>), groups of layers (<code>LayerSets</code>), channels, history states and so on — just like in a regular PSD document.

A simplified visualization of Photoshop’s DOM is below. A more detailed containment hierarchy can be found on page 12 of “<a href="https://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/products/photoshop/pdfs/cs6/Photoshop-CS6-Scripting-Guide.pdf">Adobe Photoshop CS6 Scripting Guide</a>” (PDF).

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b331ef2-a91f-4348-83c1-7df81ec4b53e/dom-mini.png" alt="Simplified visualization of Photoshop API" /><br>
<em>A simplified visualization of Photoshop’s DOM.</em>

Each of these objects has its own properties and methods that you can work with. For example, to change the opacity of the selected layer in a document, you would go to <code>Application → Document → Layer → Opacity</code> and set the desired value. The code would look like this:

<pre><code class="language-javascript">app.activeDocument.activeLayer.opacity = 50;
</code></pre>

As you may have guessed, <code>activeDocument</code> and <code>activeLayer</code> determine the currently selected document and layer.

You can find descriptions of most objects and their properties and methods in “<a href="https://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/products/photoshop/pdfs/cs6/Photoshop-CS6-JavaScript-Ref.pdf">Adobe Photoshop CS6 JavaScript Scripting Reference</a>” (PDF), or in ExtendedScript Toolkit by going to <code>Help → Object Model Viewer</code>.

Let’s see how this works in a real-world example. In this next section, we’ll write our own script based on an action.

## Remastering The RotateMe Action As A Script

A few years ago at Christmas time, I had an idea for an action to help me draw snowflakes.

### Drawing Snowflake 101

1.  Draw one stem of the snowflake with a pattern.![Step One](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d6d7965-85e0-492c-a31f-58573af7141d/snowflake-step1-mini.png)
2.  Duplicate the stem, and rotate it a few degrees.![Step Two](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b49acb81-c537-4152-a106-9f47097c76be/snowflake-step2-mini.png)
3.  Repeat the second step until you have a full circle.![Step Three](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/259c1ded-4ebd-44ac-a063-388d9bbf8c8a/snowflake-final-mini.png)

Duplicating and rotating each stem manually is tedious, so I came up with an <a href="https://blog.kam88.com/en/rotateme-photoshop-actions.html">action to automate it</a>. The algorithm looks like this:

1.  Duplicate the stem.
2.  Rotate it by however many degrees you’ve chosen, using the Transform tool.
3.  Duplicate the layer.
4.  Use the “Repeat Transform” function.
5.  Repeat steps 4 and 5 until you have a full circle.

Pretty neat. But the action had a disadvantage: You can set only a certain number of stems for the snowflake, according to the number of degrees you set in third step of the algorithm.

Back when I wasn’t familiar with scripting, I just made a few versions of the action, each of which produced a snowflake with a different number of stems.

Today, <strong>we will remaster this action as a dynamic script</strong> that takes your input on the number of stems. Let’s get started!

### Algorithm

When you start writing a script, defining the algorithm first before digging into the code itself is always a good idea. In our case, the algorithm will work like this:

1.  Ask the user to enter the number of stems.
2.  Calculate the rotation angle.
3.  Duplicate and rotate the layer by the number set in the first step.

Let’s start with saving the current or selected layer to a variable for further use:

<pre><code class="language-javascript">// Save selected layer to variable:
var originalStem = app.activeDocument.activeLayer;
</code></pre>

Note that in JavaScript, you can mark a line with double slashes (<code>//</code>) to make it a comment. Comments are used to describe parts of code for future reference and don’t affect the behavior of the script.

Let’s move on to our algorithm now.

### 1. Ask User for Input

We can take input from the user with the <code>prompt(message, default value[, title])</code> function. This function shows a dialog box with the <code>message</code> and an input field that contains the <code>default value</code>. When the user hits “OK,” the function returns the inputted value; so, we have to save it to the variable to be able to be used.

<div class="break-out">

 <pre><code class="language-javascript">// Ask user for input by showing prompt box and save inputted value to variable:
var stemsAmount = prompt("Processing ""+originalStem.name+""nHow many stems do you need?", 12);
</code></pre>
</div>

Note that I used <code>originalStem.name</code> in the message, so the dialog box will show the name of selected layer.

On Mac OS X, the first line of the message is in bold and functions as the title. So, our main message should be on the second line. To make a new line, type <code>n</code>.

In Windows, you can specify a third argument in the function to set the title:

<div class="break-out">

 <pre><code class="language-javascript">// Ask user for input by showing prompt box and save inputted value to variable:
var stemsAmount = prompt("How many stems do you need?", 12, "Processing "+originalStem.name);
</code></pre>
</div>

If we run the code in Photoshop, it will show this dialog box:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cb8328ca-f28f-4d1c-b24c-57fefd90f4cf/smashingpost-alert-mini.png" alt="Prompt dialog" />

When the user hits “OK,” the inputted value will be saved to the <code>stemsAmount</code> variable. If the user clicks “Cancel,” then the function will return a <code>null</code> value. We’ll use this later.

### 2. Calculate the Rotation Angle

To calculate the rotation angle, we have to divide 360 degrees (a full circle) by the number of stems:

<pre><code class="language-javascript">// Calculate the rotation angle
var angle = 360 / stemsAmount;
</code></pre>

### 3. Duplicate and Rotate

Now we have everything we need to make duplicates of our stem. To do this, we’ll use the <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Statements/for"><code>for</code></a> loop. It lets us repeatedly run lines of code as many times as we’d like. Our loop will look like this:

<pre><code class="language-javascript">for(var i = 1; i &lt; stemsAmount; i++){
	// This code will run "stemAmount - 1" of times
};
</code></pre>

Note that the first instance of an object in programming has the value of <code>0</code>, but because our first layer is already on the canvas, we’re starting the loop from <code>1</code> instead.

To duplicate and rotate our layer, we will use the <code>duplicate()</code> and <code>rotate(angle, AnchorPosition)</code> methods: the number of layers to be rotated in <code>angle</code> multiplied by the indexed number of duplicates. <code>AnchorPosition</code> determines the point around which the layer will rotate. You can see this point when you use the Transform tool in Photoshop — it looks like a small circle with a crosshair. In scripting, it has only 9 specified values — i.e. the 9 positions of the anchor point:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ac42f3a4-11cc-43df-a928-19828e3dce50/bottomcenter-mini.png" alt="AnchorPosition visualization" />

In our case, it is the bottom center of the layer, <code>BOTTOMCENTER</code>. Photoshop uses a lot of other constants here and there in some of the functions, which you can find on page 197 of “<a href="https://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/products/photoshop/pdfs/cs6/Photoshop-CS6-JavaScript-Ref.pdf">Adobe Photoshop CS6 JavaScript Reference</a>” (PDF).

So, our loop will look like this:

<pre><code class="language-javascript">// Duplicate and rotate layers:
for(var i = 1; i &lt; stemsAmount; i++){
	// Duplicate original layer and save it to the variable 
	var newStem = originalStem.duplicate();

	// Rotate new layer
	newStem.rotate(angle * i, AnchorPosition.BOTTOMCENTER);
};
</code></pre>

And the completed code will look like the following. You can try to run it.

<div class="break-out">

 <pre><code class="language-javascript">// Save selected layer to variable:
var originalStem = app.activeDocument.activeLayer;

// Ask user for input by showing prompt box and save inputted value to variable:
var stemsAmount = prompt("Processing ""+originalStem.name+""nHow many stems do you need?", 12);

// Calculate the rotation angle:
var angle = 360 / stemsAmount;

// Duplicate and rotate layers:
for(var i = 1; i &lt; stemsAmount; i++){
	// Duplicate original layer and save it to the variable
	var newStem = originalStem.duplicate();

	// Rotate new layer
	newStem.rotate(angle * i, AnchorPosition.BOTTOMCENTER); 
};
</code></pre>
</div>

### Final Touches

<pre><code class="language-javascript">// Duplicate and rotate layers:
for(var i = 1; i &lt; stemsAmount; i++){
	// Duplicate original layer and save it to the variable 
	var newStem = originalStem.duplicate();

	// Rotate new layer
	newStem.rotate(angle * i, AnchorPosition.BOTTOMCENTER);
};
</code></pre>

And the completed code will look like the following. You can try to run it.

<div class="break-out">

 <pre><code class="language-javascript">// Save selected layer to variable:
var originalStem = app.activeDocument.activeLayer;

// Ask user for input by showing prompt box and save inputted value to variable:
var stemsAmount = prompt("Processing ""+originalStem.name+""nHow many stems do you need?", 12);

// Calculate the rotation angle:
var angle = 360 / stemsAmount;

// Duplicate and rotate layers:
for(var i = 1; i &lt; stemsAmount; i++){
	// Duplicate original layer and save it to the variable
	var newStem = originalStem.duplicate();

	// Rotate new layer
	newStem.rotate(angle * i, AnchorPosition.BOTTOMCENTER); 
};
</code></pre>
</div>

### Final Touches

I’ll usually try to achieve the main goal with a script, and when everything works correctly, I’ll start to refine the code. In our case, we have to make sure that the user inputs a valid number in the prompt box — i.e. a positive integer, greater than one.

Also, to prevent Photoshop from going crazy, we will restrict the number of stems — let’s say, to 100. To do this, we will use a <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while"><code>while</code></a> loop to show the user an error message in the event of an invalid submission, and the prompt box will continue to be shown until the user enters a valid value or hits the “Cancel” button (remember that the prompt returns <code>null</code> if the user hits “Cancel”).

The new code looks like this:

<div class="break-out">

 <pre><code class="language-javascript">// Save selected layer to variable:
var originalStem = app.activeDocument.activeLayer;

// Ask user for input by showing prompt box and save inputted value to variable:
var stemsAmount = prompt ("Processing ""+originalStem.name+""nHow many stems do you need? (From 2 to 100)", 12);

// Check that user entered a valid number and, if invalid, show error message and ask for input again
while(isNaN(stemsAmount) || stemsAmount &lt;= 0 || stemsAmount &gt; 100){
	// If user clicks "Cancel" button, then exit loop
	if(stemsAmount == null) break;

	// Show error message…
	alert("Please enter number in range from 2 to 100");
	// …and ask for input again
	stemsAmount = prompt("Processing ""+originalStem.name+""nHow many stems do you need? (From 2 to 100)", 12);
};

// Run the copying process
if(stemsAmount != null){ 
	// Calculate the rotation angle
	var angle = 360 / parseInt(stemsAmount);

	// Duplicate and rotate layers:
	for(var i = 1; i &lt; stemsAmount; i++){
		// Duplicate original layer and save it to the variable
		var newStem = originalStem.duplicate();

		// Rotate new layer
		newStem.rotate(angle * i, AnchorPosition.BOTTOMCENTER);
	};
};
</code></pre>
</div>

As you may have noticed, we’re using the <code>isNaN(value)</code> function, which returns <code>true</code> if <code>value</code> is “not a number” and <code>parseInt(value)</code> to convert the <code>value</code> to an integer when we calculate the rotation angle.

The next thing we will do is manage the layers, renaming our new layers by adding an index to them. Also to make sure that we do not mess up document’s layers, let’s place our stems in a group.

Renaming the layers is not a hard task. We will just use the <code>name</code> property of the layer and add an index number to it:

<pre><code class="language-javascript">// Add index to new layers
newStem.name = originalStem.name + " " + (i+1);
</code></pre>

A group in Photoshop’s API is called a <code>LayerSet</code> and we can access all groups of the document by calling the <code>layerSets</code> property. To add a new group to a document, we have to call the <code>layerSets</code>’ method <code>add()</code>:

<div class="break-out">

 <pre><code class="language-javascript">// Create a group for stems
var stemsGroup = app.activeDocument.layerSets.add();
	stemsGroup.name = originalStem.name + " ("+stemsAmount+" stems)";
</code></pre>
</div>

Then, to add a layer to the group, we will use the <code>move(relativeObject, ElementPlacement)</code> function. Note that the <code>move()</code> function moves a layer in the layer stack, not on the canvas. (You can move a layer on the canvas with the <code>translate(deltaX[, deltaY])</code> function.)

<code>ElementPlacement</code> is another constant, this one determining how we will place our layer relative to… well, <code>relativeObject</code>. In our case, we will use <code>ElementPlacement.INSIDE</code> to place the original layer inside a group:

<pre><code class="language-javascript">// Place original layer in group
originalStem.move(stemsGroup, ElementPlacement.INSIDE);
</code></pre>

We will place each new copy of the layer at the bottom of all layers in the group using <code>ElementPlacement.PLACEATEND</code>. The result is all of our layers arranged in ascending order, the first layer at the top and the last at the bottom:

<pre><code class="language-javascript">// Place new layer inside stems group
newStem.move(stemsGroup, ElementPlacement.PLACEATEND);
</code></pre>

You can read more about the <code>ElementPlacement</code> constant on page 202 of “<a href="https://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/products/photoshop/pdfs/cs6/Photoshop-CS6-JavaScript-Ref.pdf">Adobe Photoshop CS6 JavaScript Reference</a>” (PDF).

## Final Code

That’s it! <code>RotateMe.jsx</code> is done. Our final code looks like this:

<div class="break-out">

 <pre><code class="language-javascript">
// Save selected layer to variable:
var originalStem = app.activeDocument.activeLayer;

// Ask user for input by showing prompt box and save inputted value to variable:
var stemsAmount = prompt ("Processing ""+originalStem.name+""nHow many stems do you need? (From 2 to 100)", 12);

// Check that user entered a valid number and, if invalid, show error message and ask for input again
while(isNaN(stemsAmount) || stemsAmount &lt;= 0 || stemsAmount &gt; 100){
	// If user clicks "Cancel" button, then exit loop
	if(stemsAmount == null) break;

	// Show error message…
	alert("Please enter number in range from 2 to 100");
	// …and ask for input again
	stemsAmount = prompt("Processing ""+originalStem.name+""nHow many stems do you need? (From 2 to 100)", 12);
};

// Run the copying process
if(stemsAmount != null){ 
	// Calculate the rotation angle
	var angle = 360 / parseInt(stemsAmount);

	// Create a group for stems
	var stemsGroup = app.activeDocument.layerSets.add();
		stemsGroup.name = originalStem.name + " ("+stemsAmount+" stems)";
	// Place original layer in group
	originalStem.move(stemsGroup, ElementPlacement.INSIDE);

	// Duplicate and rotate layers:
	for(var i = 1; i &lt; stemsAmount; i++){
		// Duplicate original layer and save it to the variable
		var newStem = originalStem.duplicate();

		// Rotate new layer
		newStem.rotate(angle * i, AnchorPosition.BOTTOMCENTER);

		// Add index to new layers
		newStem.name = originalStem.name + " " + (i+1);

		// Place new layer inside stems group
		newStem.move(stemsGroup, ElementPlacement.PLACEATEND);
	};

	// Add index to the original layer
	originalStem.name += " 1";
};
</code></pre>
</div>

That wasn’t too hard, was it?

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1704c6b9-c1ab-4aed-848b-4751a14e785c/smashingpost-finish-mini.png" alt="Finish" />

Now you can put it in the <code>Photoshop/Presets/Scripts/</code> folder and run it by going to <code>File → Scripts</code> in Photoshop. Using different shapes with different values can yield interesting results:

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e61bc42d-0e7b-43fa-8e6f-c70494114d01/smashingpost-examples-mini.png" alt="" />

*   [Download the source file](https://cl.ly/Q7jt/file) (RotateMe.jsx)

## Conclusion

As you can see from the number of links in the resources section below, there’s much more to say about scripting than can fit in an introductory article. But I hope the little that we’ve described today piques your interest and shows how powerful and helpful scripting is.

<img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/234073cf-0ddc-4768-999c-6d44bd4c2408/smashingpost-conclusion-mini.png" alt="Community Power!" />

If you decide to dive into it, let’s learn together and share our experience. Ask your questions and share what you’ve done in the comments. If you are not a coder, consider leaving an idea for a script; maybe another reader will make it happen.

Let’s make Photoshop more useful together!

### Resources

I’m still learning about Photoshop scripts, too, and here are some resources that are helping me along the way:

*   “[Adobe Photoshop Scripting](https://www.adobe.com/devnet/photoshop/scripting.html),” Adobe Developer Connection  
All of the documentation and utilities for scripting.
*   “[Adobe Introduction to Scripting](https://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/products/indesign/pdfs/Adobe_Intro_to_Scripting1.pdf)” (PDF) Adobe  
Here are the basics on scripting for Adobe applications. The nice thing about scripting for Photoshop is that you can apply your knowledge to other Adobe products; you just need to learn the application’s DOM, and you’ll be ready to go.
*   “[Adobe Photoshop CS6 Scripting Guide](https://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/products/photoshop/pdfs/cs6/Photoshop-CS6-Scripting-Guide.pdf)” (PDF), Adobe  
In this introductory guide to scripting for Photoshop, you’ll find the basics on getting started with scripting.
*   “[Photoshop CS6 JavaScript Reference](https://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/products/photoshop/pdfs/cs6/Photoshop-CS6-JavaScript-Ref.pdf)” (PDF), Adobe  
This describes all of the objects and their functions and methods that you can use in scripting for Photoshop. This is one of the documents I use most when writing scripts.
*   “[JavaScript](https://developer.mozilla.org/en/docs/JavaScript),” Mozilla Developer Network  
Here are answers to all kinds of questions about general JavaScript functions and usage.
*   “[JavaScript Tools Guide](https://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/products/indesign/pdfs/JavaScriptToolsGuide_CS5.pdf)” (PDF), Adobe  
This has basic information about ExtendedScript Toolkit and some advanced techniques, such as file system access and ScriptUI and working with XML, sockets and more.
*   [PS-Scripts](https://ps-scripts.com/bb/index.php)  
An independent forum about scripting for Photoshop. I wasn't able to sign up to participate in discussions (because of some kind of pre-moderation system), but it has plenty of answered questions and solved problems to discover.
*   [Photoshop Scripting](https://forums.adobe.com/community/photoshop/photoshop_scripting), Adobe Community  
Adobe’s official forum for Photoshop scripting has some good discussion on problems encountered by users.

### <span class="rh">Further Reading</span> on SmashingMag:

*   [The Ultimate Collection Of Useful Photoshop Actions](https://www.smashingmagazine.com/2008/10/the-ultimate-collection-of-useful-photoshop-actions/)
*   [Retinize It: Free Photoshop Action For Slicing Graphics For HD Screens](https://www.smashingmagazine.com/2013/07/retinize-it-photoshop-action-slicing-graphics-retina/)
*   [Mastering Photoshop: Unknown Tricks and Time-Savers](https://www.smashingmagazine.com/2010/01/obscure-adobe-photoshop-time-savers/)

{{< signature "al, ea" >}}

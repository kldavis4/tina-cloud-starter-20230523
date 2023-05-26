---
title: Make Your Own Bookmarklets With jQuery
slug: make-your-own-bookmarklets-with-jquery
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/81a5ec29-6dc0-42bc-aa0b-83f8b4102fe4/dec-15-space-race-preview-opt.png
date: 2010-05-23T19:40:55.000Z
author: tommy-iamnotagoodartist
description: >-
  **Bookmarklets** are small JavaScript-powered applications in link form. Often
  "one-click" tools and functions, they're typically used to extend the functionality of the browser and to interact with Web services. They can do things like post to your WordPress or Tumblr blog, submit any selected text to Google Search, or modify a current page's CSS… and _many_ other things!
categories:
  - Coding
  - jQuery
---
Because they run on JavaScript (a client-side programming language), bookmarklets (sometimes called "favelets") are supported by all major browsers on all platforms, without any additional plug-ins or software needed. In most instances, the user can just drag the bookmarklet link to their toolbar, and that's it!

<img loading="lazy" decoding="async" class="37608" title="Make Your Own Bookmarklets with jQuery" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a9e4d2fb-b30e-4a4b-a76a-ddcb6df0ab7b/makeyourownbookmarklets.jpg" alt="Make Your Own Bookmarklets with jQuery" width="500" height="333" />

{{% feature-panel %}}

In this article, we'll go through how to <strong>make your own</strong> bookmarklets, using the <a href="https://jquery.com/">jQuery</a> JavaScript framework.</p>

## Getting Started

You can make a faux <a href="https://en.wikipedia.org/wiki/Uniform_Resource_Identifier">URI</a> with JavaScript by prefacing the code with <code>javascript:</code>, like so:

<pre><code class="language-markup tmp-html">&lt;a href="javascript: alert('Arbitrary JS code!');"&gt;Alert!&lt;/a&gt;</code></pre>

Notice that when we put it in the <code>href</code> attribute, we replaced what would normally be double quotes (") with single quotes ('), so the <code>href</code> attribute's value and JavaScript function don't get cut off midway. That's not the only way to circumvent that problem, but it'll do for now.

We can take this concept as far as we want, adding multiple lines of JavaScript inside these quote marks, with each line separated by a semicolon (;), sans line break. If your bookmarklet won't need any updating later, this method of "all inclusiveness" will probably be fine. For this tutorial, we'll be externalizing the JavaScript code and storing it in a .JS file, which we'll host somewhere else.

A link to an externalized bookmarklet:

<pre><code class="language-markup tmp-html">&lt;a href="javascript:(function(){document.body.appendChild(document.createElement('script')).src='https://foo.bar/baz.js';})();"&gt;Externalized Bookmarklet&lt;/a&gt;</code></pre>

This looks for the document's body and appends a <code>&lt;script&gt;</code> element to it with a <code>src</code> we've defined, in this case, "https://foo.bar/baz.js". Keep in mind that if the user is on an empty tab or a place which, for some reason, has no body, nothing will happen as nothing can be appended to.

You can host that .JS file wherever is convenient, but keep bandwidth in mind if you expect a <em>ton</em> of traffic.</p>

## Enter jQuery

Since many of you may be familiar with the <a href="https://jquery.com/">jQuery</a> framework, we'll use that to build our bookmarklet.

The best way to get it inside of our .JS file is to append it from <a href="https://code.google.com/apis/ajaxlibs/">Google's CDN</a>, conditionally wrapped to only include it if necessary:

<pre><code class="language-javascript">(function(){

	// the minimum version of jQuery we want
	var v = "1.3.2";

	// check prior inclusion and version
	if (window.jQuery === undefined || window.jQuery.fn.jquery &lt; v) {
		var done = false;
		var script = document.createElement("script");
		script.src = "https://ajax.googleapis.com/ajax/libs/jquery/" + v + "/jquery.min.js";
		script.onload = script.onreadystatechange = function(){
			if (!done &amp;&amp; (!this.readyState || this.readyState == "loaded" || this.readyState == "complete")) {
				done = true;
				initMyBookmarklet();
			}
		};
		document.getElementsByTagName("head")[0].appendChild(script);
	} else {
		initMyBookmarklet();
	}

	function initMyBookmarklet() {
		(window.myBookmarklet = function() {
			// your JavaScript code goes here!
		})();
	}

})();</code></pre>

(Script appending from jQuery's source code, adapted by Paul Irish: <a href="https://pastie.org/462639">https://pastie.org/462639</a>)

That starts by defining <code>v</code>, the minimum version of jQuery that our code can safely use. Using that, it then checks to see if jQuery needs to be loaded. If so, it adds it to the page with cross-browser event handling support to run <code>initMyBookmarklet</code> when jQuery's ready. If not, it jumps straight to <code>initMyBookmarklet</code>, which adds the <code>myBookmarklet</code> to the global window object.</p>

## Grabbing Information

Depending on what kind of bookmarklet you're making, it may be worthwhile to grab information from the current page. The two most important things are <code>document.location</code>, which returns the page's URL, and <code>document.title</code>, which returns the page's title.

You can also return any text the user may have selected, but it's a little more complicated:

<pre><code class="language-javascript">function getSelText() {
	var SelText = ’;
	if (window.getSelection) {
		SelText = window.getSelection();
	} else if (document.getSelection) {
		SelText = document.getSelection();
	} else if (document.selection) {
		SelText = document.selection.createRange().text;
	}
	return SelText;
}</code></pre>

(Modified from <a href="https://www.codetoad.com/javascript_get_selected_text.asp">https://www.codetoad.com/javascript_get_selected_text.asp</a>)

Another option is to use JavaScript's <code>input</code> function to query the user with a pop-up:

<pre><code class="language-javascript">var yourname = prompt("What's your name?","my name...");</code></pre>

## Dealing with Characters

If you'll be putting all your JavaScript into the link itself rather than an external file, you may want a better way to nest double quotes (as in, "a quote 'within a quote'") than just demoting them into singles. Use <code>&amp;quot;</code> in their place (as in, "a quote <code>&amp;quot;</code>within a quote<code>&amp;quot;</code>"):

<pre><code class="language-markup tmp-html">&lt;a
href="javascript:var%20yourname=prompt(&amp;quot;What%20is%20your%20name?&amp;quot;);alert%20(&amp;quot;Hello,%20"+yourname+"!&amp;quot;)"&gt;What is your name?&lt;/a&gt;</code></pre>

In that example, we also encoded the spaces into <code>%20</code>, which may be beneficial for older browsers or to make sure the link doesn't fall apart in transit somewhere.

Within JavaScript, you may sometimes need to escape quotes. You can do so by prefacing them with a backslash ():

<pre><code class="language-javascript">alert("This is a "quote" within a quote.");</code></pre>

## Putting It All Together

Just for fun, let's make a little bookmarklet that checks to see if there's a selected word on the page, and, if there is, searches <a href="https://wikipedia.org/">Wikipedia</a> and shows the results in a jQuery-animated iFrame.

We'll start by combining the framework from "Enter jQuery" with the text selection function from "Grabbing Information":

<pre><code class="language-javascript">(function(){

	var v = "1.3.2";

	if (window.jQuery === undefined || window.jQuery.fn.jquery &lt; v) {
		var done = false;
		var script = document.createElement("script");
		script.src = "https://ajax.googleapis.com/ajax/libs/jquery/" + v + "/jquery.min.js";
		script.onload = script.onreadystatechange = function(){
			if (!done &amp;&amp; (!this.readyState || this.readyState == "loaded" || this.readyState == "complete")) {
				done = true;
				initMyBookmarklet();
			}
		};
		document.getElementsByTagName("head")[0].appendChild(script);
	} else {
		initMyBookmarklet();
	}

	function initMyBookmarklet() {
		(window.myBookmarklet = function() {
			function getSelText() {
				var s = ’;
				if (window.getSelection) {
					s = window.getSelection();
				} else if (document.getSelection) {
					s = document.getSelection();
				} else if (document.selection) {
					s = document.selection.createRange().text;
				}
				return s;
			}
			// your JavaScript code goes here!
		})();
	}

})();</code></pre>

Next, we'll look for any selected text and save it to a variable, "s". If there's nothing selected, we'll try to prompt the user for something:

<pre><code class="language-javascript">var s = "";
s = getSelText();
if (s == "") {
	var s = prompt("Forget something?");
}</code></pre>

After checking to make sure we received an actual value for "s", we'll append the new content to the document's body. In it will be: a container div ("wikiframe"), a background veil ("wikiframe_veil") and a "Loading..." paragraph, the iFrame itself, and some CSS to make things look pretty and affix everything above the actual page.

<pre><code class="language-javascript">if ((s != "") &amp;&amp; (s != null)) {
	$("body").append("
	&lt;div id='wikiframe'&gt;
		&lt;div id='wikiframe_veil' style=’&gt;
			&lt;p&gt;Loading...&lt;/p&gt;
		&lt;/div&gt;
		&lt;iframe src='https://en.wikipedia.org/w/index.php?&amp;search="+s+"' onload="$('#wikiframe iframe').slideDown(500);"&gt;Enable iFrames.&lt;/iframe&gt;
		&lt;style type='text/css'&gt;
			#wikiframe_veil { display: none; position: fixed; width: 100%; height: 100%; top: 0; left: 0; background-color: rgba(255,255,255,.25); cursor: pointer; z-index: 900; }
			#wikiframe_veil p { color: black; font: normal normal bold 20px/20px Helvetica, sans-serif; position: absolute; top: 50%; left: 50%; width: 10em; margin: -10px auto 0 -5em; text-align: center; }
			#wikiframe iframe { display: none; position: fixed; top: 10%; left: 10%; width: 80%; height: 80%; z-index: 999; border: 10px solid rgba(0,0,0,.5); margin: -5px 0 0 -5px; }
		&lt;/style&gt;
	&lt;/div&gt;");
	$("#wikiframe_veil").fadeIn(750);
}</code></pre>

We set the iFrame's <code>src</code> attribute to Wikipedia's search URL plus "s". Its CSS sets it to <code>display: none;</code> by default, so we can have it make a grander entrance when its page is loaded via its <code>onload</code> attribute and a jQuery animation.

After all that's added to the page, we'll fade in the background veil.

Notice the backslashes at the end of each line of appended HTML. These allow for multiple rows and make everything easier on the eyes for editing.

Almost done, but we need to make sure these elements don't already exist before appending them. We can accomplish that by throwing the above code inside a <code>($("#wikiframe").length == 0)</code> conditional statement, accompanied by some code to remove it all if the statement returns negative.

The end result .JS file:

<pre><code class="language-javascript">(function(){

	var v = "1.3.2";

	if (window.jQuery === undefined || window.jQuery.fn.jquery &lt; v) {
		var done = false;
		var script = document.createElement("script");
		script.src = "https://ajax.googleapis.com/ajax/libs/jquery/" + v + "/jquery.min.js";
		script.onload = script.onreadystatechange = function(){
			if (!done &amp;&amp; (!this.readyState || this.readyState == "loaded" || this.readyState == "complete")) {
				done = true;
				initMyBookmarklet();
			}
		};
		document.getElementsByTagName("head")[0].appendChild(script);
	} else {
		initMyBookmarklet();
	}

	function initMyBookmarklet() {
		(window.myBookmarklet = function() {
			function getSelText() {
				var s = ’;
				if (window.getSelection) {
					s = window.getSelection();
				} else if (document.getSelection) {
					s = document.getSelection();
				} else if (document.selection) {
					s = document.selection.createRange().text;
				}
				return s;
			}
			if ($("#wikiframe").length == 0) {
				var s = "";
				s = getSelText();
				if (s == "") {
					var s = prompt("Forget something?");
				}
				if ((s != "") &amp;&amp; (s != null)) {
					$("body").append("
					&lt;div id='wikiframe'&gt;
						&lt;div id='wikiframe_veil' style=’&gt;
							&lt;p&gt;Loading...&lt;/p&gt;
						&lt;/div&gt;
						&lt;iframe src='https://en.wikipedia.org/w/index.php?&amp;search="+s+"' onload="$('#wikiframe iframe').slideDown(500);"&gt;Enable iFrames.&lt;/iframe&gt;
						&lt;style type='text/css'&gt;
							#wikiframe_veil { display: none; position: fixed; width: 100%; height: 100%; top: 0; left: 0; background-color: rgba(255,255,255,.25); cursor: pointer; z-index: 900; }
							#wikiframe_veil p { color: black; font: normal normal bold 20px/20px Helvetica, sans-serif; position: absolute; top: 50%; left: 50%; width: 10em; margin: -10px auto 0 -5em; text-align: center; }
							#wikiframe iframe { display: none; position: fixed; top: 10%; left: 10%; width: 80%; height: 80%; z-index: 999; border: 10px solid rgba(0,0,0,.5); margin: -5px 0 0 -5px; }
						&lt;/style&gt;
					&lt;/div&gt;");
					$("#wikiframe_veil").fadeIn(750);
				}
			} else {
				$("#wikiframe_veil").fadeOut(750);
				$("#wikiframe iframe").slideUp(500);
				setTimeout("$('#wikiframe').remove()", 750);
			}
			$("#wikiframe_veil").click(function(event){
				$("#wikiframe_veil").fadeOut(750);
				$("#wikiframe iframe").slideUp(500);
				setTimeout("$('#wikiframe').remove()", 750);
			});
		})();
	}

})();</code></pre>

Note that we fade out and remove the "wikiframe" content both if the user re-clicks the bookmarklet after it's loaded <em>and</em> if the user clicks on its background veil.

The HTML bookmarklet to load that script:

<pre><code class="language-markup tmp-html">&lt;a href="javascript:(function(){if(window.myBookmarklet!==undefined){myBookmarklet();}else{document.body.appendChild(document.createElement('script')).src='https://iamnotagoodartist.com/stuff/wikiframe2.js?';}})();"&gt;WikiFrame&lt;/a&gt;</code></pre>

<a>WikiFrame</a>

See that <code>(window.myBookmarklet!==undefined)</code> conditional? That makes sure the .JS file is only appended once and jumps straight to running the <code>myBookmarklet()</code> function if it already exists.</p>

## Make It Better

This example was fun, but it definitely could be better.

For starters, it isn't compressed. If your script will be accessed a lot, keeping two versions of your code may be a good idea: one normal working version and one compressed minimized version. Serving the compressed one to your users will save loading time for them and bandwidth for you. Check the resource links below for some good JavaScript compressors.

While the bookmarklet technically works in IE6, its use of static positioning means that it just kind of appends itself to the bottom of the page. Not very user-friendly! With some more time and attention to <a href="https://www.smashingmagazine.com/2009/10/14/css-differences-in-internet-explorer-6-7-and-8/">rendering differences in IE</a>, the bookmarklet could be made to function and <em>look</em> the same (or at least comparable) in different browsers.

In our example, we used jQuery, which is an excellent tool for developing more advanced JavaScript applications. But if your bookmarklet is simple and doesn't require a lot of CSS manipulation or animation, chances are you may not need something so advanced. Plain old JavaScript might suffice. Remember, the less you force the user to load, the faster their experience and the happier they will be.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="37612" title="Bookmarklets" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/893b0e7f-3693-41cc-bc03-011aa139a23c/bookmarklets.jpg" alt="Bookmarklets" width="500" height="333" />

### Things to Keep in Mind and Best Practices

Untested code is broken code, as old-school programmers will tell you. While bookmarklets will run on any browser that supports JavaScript, testing them in as many browsers as you can wouldn't hurt. Especially when working with CSS, a whole slew of variables can affect the way your script works. At the very least, enlist your friends and family to test the bookmarklet on their computers and their browsers.

Speaking of CSS, remember that any content you add to a page will be affected by that page's CSS. So, applying a <a href="https://www.smashingmagazine.com/2007/09/21/css-frameworks-css-reset-design-from-scratch/">reset</a> to your elements to override any potentially inherited margins, paddings or font stylings would be wise.

Because bookmarklets are, by definition, extraneous, many of the guidelines for JavaScript—such as unobtrusiveness and graceful degradation—aren't as sacred as they normally are. For the most part, though, a healthy understanding of best practices for traditional <a href="https://net.tutsplus.com/tutorials/javascript-ajax/24-javascript-best-practices-for-beginners/">JavaScript</a> and <a href="https://www.smashingmagazine.com/2008/09/16/jquery-examples-and-best-practices/">its frameworks</a> will only help you:

*   Develop a coding style and stick to it. Keep it consistent, and keep it neat.
*   Take it easy on the browser. Don't run processes that you don't need, and don't create unnecessary global variables.
*   Use comments where appropriate. They make jumping back into the code later on much easier.
*   Avoid shorthand JavaScript. Use plenty of semi-colons, even when your browser would let you get away without them.</p>

## Further Resources

### Helpful JavaScript Tools

*   [JSLint](https://www.jslint.com/) JavaScript validation tool.
*   [Bookmarklet Builder](https://subsimple.com/bookmarklets/jsbuilder.htm) Made way back in 2004, but still useful.
*   <span class="removed_link" title="https://www.w3avenue.com/2009/05/19/list-of-really-useful-free-tools-for-javascript-developers/">List of Really Useful Free Tools for JavaScript Developers</span> Courtesy of W3Avenue.
*   [JS Bin](https://jsbin.com/) Open-source collaborative JavaScript debugging tool.
*   How to Dynamically Insert Javascript and CSS A well-written examination of JavaScript and CSS appending, and its potential pitfalls.
*   [Run jQuery Code Bookmarklet](https://benalman.com/projects/run-jquery-code-bookmarklet/) A pretty cool script that checks for and loads jQuery all within the bookmarklet. Also has a [handy generator](https://benalman.com/code/test/jquery-run-code-bookmarklet/).
*   [Google AJAX Libraries API](https://code.google.com/apis/ajaxlibs/) Do you prefer Prototype or MooTools to jQuery? Load your preference straight from Google and save yourself the bandwidth.</p>

### JavaScript and CSS Compressors

*   [Online Javascript Compression Tool](https://jscompress.com/) JavaScript compressor, with both Minify and Packer methods.
*   [Clean CSS](https://www.cleancss.com/) CSS formatter and optimizer, based on [csstidy](https://csstidy.sourceforge.net/), with a nice GUI and plenty of options.
*   [Scriptalizer](https://scriptalizer.com/) Combines and compresses multiple JavaScript and/or CSS files.
*   [JavaScript Unpacker and Beautifier](https://jsbeautifier.org/) Useful for translating super-compressed code into something more human-legible (and vice versa).</p>

### Collections

*   [myBookmarklets](https://krapplack.de/?u=/bookmarklets/)
*   [Bookmarklets.com](https://www.bookmarklets.com/)
*   [Bookmarklets, Favelets and Snippets](https://www.smashingmagazine.com/2007/01/24/bookmarklets-favelets-and-snippets/) Via Smashing Magazine.
*   [Quix](https://quixapp.com/) "Your Bookmarklets, On Steroids."
*   [Jesse's Bookmarklets](https://www.squarefree.com/bookmarklets/)
*   [Marklets](https://www.marklets.com/bookmarklets/)

## Further Reading:

*   [Time Savers, Tools And Useful Services For Web Designers](https://www.smashingmagazine.com/time-savers-tools-useful-services-web-design/)
*   [Essential jQuery Plugin Patterns](https://www.smashingmagazine.com/2011/10/essential-jquery-plugin-patterns/)
*   [Useful jQuery Function Demos For Your Projects](https://www.smashingmagazine.com/2012/05/50-jquery-function-demos-for-aspiring-web-developers/)

{{< signature "al" >}}


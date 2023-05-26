---
title: Commonly Confused Bits Of jQuery
slug: commonly-confused-bits-of-jquery
image: null
date: 2010-08-04T13:04:15.000Z
author: andy-croxall
description: >-
  The explosion of JavaScript libraries and frameworks such as **jQuery** onto the front-end development scene has opened up the power of JavaScript to a far wider audience than ever before. It was born of the need — expressed by a crescendo of screaming by front-end developers who were fast running out of hair to pull out — to improve JavaScript's somewhat primitive API, to make up for the lack of unified implementation across browsers and to make it more compact in its syntax.
categories:
  - Coding
  - jQuery
  - Essentials
---
All of which means that, unless you have some odd grudge against jQuery, those days are gone — you can actually get stuff done now. A script to find all links of a certain CSS class in a document and bind an event to them now requires one line of code, not 10. To power this, jQuery brings to the party its own API, featuring a host of functions, methods and syntactical peculiarities. Some are confused or appear similar to each other but actually differ in some way. <strong>This article clears up some of these confusions</strong>.</p>

## 1\. .parent() vs. .parents() vs. .closest()

All three of these methods are concerned with navigating upwards through the DOM, above the element(s) returned by the selector, and matching certain parents or, beyond them, ancestors. But they differ from each other in ways that make them each uniquely useful.</p>

### parent(selector)

This simply matches the <strong>one immediate parent</strong> of the element(s). It can take a selector, which can be useful for matching the parent only in certain situations. For example:

{{% feature-panel %}}

<pre><code class="language-javascript">$('span#mySpan').parent().css('background', '#f90');
$('p').parent('div.large').css('background', '#f90');</code></pre>

The first line gives the parent of <code>#mySpan</code>. The second does the same for parents of all <code>&lt;p&gt;</code> tags, provided that the parent is a <code>div</code> and has the class <code>large</code>.

<em>Tip:</em> the ability to limit the reach of methods like the one in the second line is a common feature of jQuery. The majority of DOM manipulation methods allow you to specify a selector in this way, so it's not unique to <code>parent()</code>.</p>

### parents(selector)

This acts in much the same way as <code>parent()</code>, except that it is not restricted to just one level above the matched element(s). That is, it can return <strong>multiple ancestors</strong>. So, for example:

<pre><code class="language-javascript">$('li.nav').parents('li'); //for each LI that has the class nav, go find all its parents/ancestors that are also LIs</code></pre>

This says that for each <code>&lt;li&gt;</code> that has the class <code>nav</code>, return all its parents/ancestors that are also <code>&lt;li&gt;</code>s. This could be useful in a multi-level navigation tree, like the following:

<pre><code class="language-markup tmp-html">&lt;ul id='nav'&gt;
	&lt;li&gt;Link 1
		&lt;ul&gt;
			&lt;li&gt;Sub link 1.1&lt;/li&gt;
			&lt;li&gt;Sub link 1.2&lt;/li&gt;
			&lt;li&gt;Sub link 1.3&lt;/li&gt;
		&lt;/ul&gt;
	&lt;li&gt;Link 2
		&lt;ul&gt;
			&lt;li&gt;Sub link 2.1

			&lt;li&gt;Sub link 2.2

		&lt;/ul&gt;
	&lt;/li&gt;
&lt;/ul&gt;</code></pre>

Imagine we wanted to color every third-generation <code>&lt;li&gt;</code> in that tree orange. Simple:

<pre><code class="language-javascript">$('#nav li').each(function() {
	if ($(this).parents('#nav li').length == 2)
		$(this).css('color', '#f90');
});</code></pre>

This translates like so: for every <code>&lt;li&gt;</code> found in <code>#nav</code> (hence our <code>each()</code> loop), whether it's a direct child or not, see how many <code>&lt;li&gt;</code> parents/ancestors are above it within <code>#nav</code>. If the number is two, then this <code>&lt;li&gt;</code> must be on level three, in which case color.</p>

### closest(selector)

This is a bit of a well-kept secret, but very useful. It works like <code>parents()</code>, except that it returns <strong>only one parent/ancestor</strong>. In my experience, you'll normally want to check for the existence of one particular element in an element's ancestry, not a whole bunch of them, so I tend to use this more than <code>parents()</code>. Say we wanted to know whether an element was a descendant of another, however deep in the family tree:

<pre><code class="language-javascript">if ($('#element1').closest('#element2').length == 1)
	alert("yes - #element1 is a descendent of #element2!");
else
	alert("No - #element1 is not a descendent of #element2");</code></pre>

<em>Tip:</em> you can simulate <code>closest()</code> by using <code>parents()</code> and limiting it to one returned element.

<pre><code class="language-javascript">$($('#element1').parents('#element2').get(0)).css('background', '#f90');</code></pre>

One quirk about <code>closest()</code> is that traversal starts from the element(s) matched by the selector, not from its parent. This means that if the selector that passed inside <code>closest()</code> matches the element(s) it is running on, it will return itself. For example:

<pre><code class="language-javascript">$('div#div2').closest('div').css('background', '#f90');</code></pre>

This will turn <code>#div2</code> itself orange, because <code>closest()</code> is looking for a <code>&lt;div&gt;</code>, and the nearest <code>&lt;div&gt;</code> to <code>#div2</code> is itself.

## 2\. .position() vs. .offset()

These two are both concerned with reading the position of an element — namely the first element returned by the selector. They both return an object containing two properties, left and top, but they differ in <strong>what the returned position is relative to</strong>.

<code>position()</code> calculates positioning relative to the offset parent — or, in more understandable terms, the nearest parent or ancestor of this element that has <code>position: relative</code>. If no such parent or ancestor is found, the position is calculated relative to the document (i.e. the top-left corner of the viewport).

<code>offset()</code>, in contrast, always calculates positioning relative to the document, regardless of the <code>position</code> attribute of the element's parents and ancestors.

Consider the following two <code>&lt;div&gt;</code>s:
<div id="wrapperDiv" style="position: relative; left: 100px; width: 300px; height: 190px; background: #f90; margin: 10px; padding: 10px;">

Hello - I'm outerDiv. I have position: relative and left: 100px
<div id="innerDiv" style="position: absolute; left: 50px; top: 80px; width: 150px; height: 100px; background: #f00; padding: 10px;">
<p style="color: #fff;">Hi - I'm #innerDiv. I have position absolute, left: 50px and top: 80px.</p>

</div>
</div>
Querying (no pun intended) the <code>offset()</code> and <code>position()</code> of <code>#innerDiv</code> will return different results.

<pre><code class="language-javascript">var position = $('#innerDiv').position();
var offset = $('#innerDiv').offset();
alert("Position: left = "+position.left+", top = "+position.top+"n"+
      "Offset: left = "+offset.left+" and top = "+offset.top
)</code></pre>

<script type="text/javascript">// <![CDATA[

function getPositionAndOffset() {
	var position = $('#innerDiv').position();
	var offset = $('#innerDiv').offset();
	alert("Position: left = "+position.left+", top = "+position.top+"n"+
	      "Offset: left = "+offset.left+" and top = "+offset.top
	)
}
// ]]></script>

Try it yourself to see the results: <a href="javascript:getPositionAndOffset()">click here</a>.</p>

## 3\. .css('width') and .css('height') vs. .width() and .height()

These three, you won't be shocked to learn, are concerned with calculating the dimensions of an element in pixels. They both return the offset dimensions, which are the genuine dimensions of the element no matter how stretched it is by its inner content.

<strong>They differ in the data types they return</strong>: <code>css('width')</code> and <code>css('height')</code> return dimensions as strings, with <code>px</code> appended to the end, while <code>width()</code> and <code>height()</code> return dimensions as integers.

There's actually another little-known difference that concerns IE (quelle surprise!), and it's why you should avoid the <code>css('width')</code> and <code>css('height')</code> route. It has to do with the fact that IE, when asked to read “computed” (i.e. not implicitly set) dimensions, unhelpfully returns <code>auto</code>. In jQuery core, <code>width()</code> and <code>height()</code> are based on the <code>.offsetWidth</code> and <code>.offsetHeight</code> properties resident in every element, which IE <em>does</em> read correctly.

But if you're working on elements with dimensions implicitly set, you don't need to worry about that. So, if you wanted to read the width of one element and set it on another element, you'd opt for <code>css('width')</code>, because the value returned comes ready appended with 'px'.

But if you wanted to read an element's <code>width()</code> with a view to performing a calculation on it, you'd be interested only in the figure; hence <code>width()</code> is better.

Note that <strong>each of these can simulate the other</strong> with the help of an extra line of JavaScript, like so:

<pre><code class="language-javascript">var width = $('#someElement').width(); //returns integer
width = width+'px'; //now it's a string like css('width') returns
var width = $('#someElement').css('width'); //returns string
width = parseInt(width); //now it's an integer like width() returns</code></pre>

Lastly, <code>width()</code> and <code>height()</code> actually have another trick up their sleeves: they can return <strong>the dimensions of the window and document</strong>. If you try this using the <code>css()</code> method, you'll get an error.</p>

## 4\. .click() (etc) vs. .bind() vs. .live() vs. .delegate

These are all concerned with binding events to elements. The differences lie in what elements they bind to and how much we can influence the event handler (or “callback”). If this sounds confusing, don't worry. I'll explain.</p>

### click() (etc)

It's important to understand that <code>bind()</code> is the daddy of jQuery's event-handling API. Most tutorials deal with events with simple-looking methods, such as <code>click()</code> and <code>mouseover()</code>, but behind the scenes these are just the lieutenants who report back to <code>bind()</code>.

These lieutenants, or aliases, give you quick access to bind certain event types to the elements returned by the selector. They all take one argument: a callback function to be executed when the event fires. For example:

<pre><code class="language-javascript">$('#table td ').click(function() {
	alert("The TD you clicked contains '"+$(this).text()+"'");
});</code></pre>

This simply says that whenever a <code>&lt;div&gt;</code> inside <code>#table</code> is clicked, alert its text content.</p>

### bind()

We can do the same thing with <code>bind</code>, like so:

<pre><code class="language-javascript">$('#table td ').bind('click', function() {
	alert("The TD you clicked contains '"+$(this).text()+"'");
});</code></pre>

Note that this time, the event type is passed as the first argument to <code>bind()</code>, with the callback as the second argument. Why would you use <code>bind()</code> over the simpler alias functions?

Very often you wouldn't. But <code>bind()</code> gives you more control over what happens in the event handler. It also allows you to bind more than one event at a time, by space-separating them as the first argument, like so:

<pre><code class="language-javascript">$('#table td').bind('click contextmenu', function() {
	alert("The TD you clicked contains '"+$(this).text()+"'");
});</code></pre>

Now our event fires whether we've clicked the <code>&lt;td&gt;</code> with the left or right button. I also mentioned that <code>bind()</code> gives you more control over the event handler. How does that work? It does it by passing three arguments rather than two, with argument two being a data object containing properties readable to the callback, like so:

<pre><code class="language-javascript">$('#table td').bind('click contextmenu', {message: 'hello!'}, function(e) {
	alert(e.data.message);
});</code></pre>

As you can see, we're passing into our callback a set of variables for it to have access to, in our case the variable <code>message</code>.

You might wonder why we would do this. Why not just specify any variables we want outside the callback and have our callback read those? The answer has to do with <strong>scope and closures</strong>. When asked to read a variable, JavaScript starts in the immediate scope and works outwards (this is a fundamentally different behavior to languages such as PHP). Consider the following:

<pre><code class="language-javascript">var message = 'you left clicked a TD';
$('#table td').bind('click', function(e) {
	alert(message);
});
var message = 'you right clicked a TD';
$('#table td').bind('contextmenu', function(e) {
	alert(message);
});</code></pre>

No matter whether we click the <code>&lt;td&gt;</code> with the left or right mouse button, we will be told it was the right one. This is because the variable <code>message</code> is read by the <code>alert()</code> at the time of the event firing, not at the time the event was bound.

If we give each event its <em>own</em> “version” of <code>message</code> at the time of binding the events, we solve this problem.

<pre><code class="language-javascript">$('#table td').bind('click', {message: 'You left clicked a TD'}, function(e) {
	alert(e.data.message);
});
$('#table td').bind('contextmenu', {message: 'You right clicked a TD'}, function(e) {
	alert(e.data.message);
});</code></pre>

Events bound with <code>bind()</code> and with the alias methods (<code>.mouseover()</code>, etc) are unbound with the <code>unbind()</code> method.</p>

### live()

This works almost exactly the same as <code>bind()</code> but with one crucial difference: events are bound both to current and future elements — that is, any elements that do not currently exist but which may be DOM-scripted after the document is loaded.

<strong>Side note:</strong> DOM-scripting entails creating and manipulating elements in JavaScript. Ever notice in your Facebook profile that when you “add another employer” a field magically appears? That's DOM-scripting, and while I won't get into it here, it looks broadly like this:

<pre><code class="language-javascript">var newDiv = document.createElement('div');
newDiv.appendChild(document.createTextNode('hello, world!'));
$(newDiv).css({width: 100, height: 100, background: '#f90'});
document.body.appendChild(newDiv);</code></pre>

### delegate()

A shortfall of <code>live()</code> is that, unlike the vast majority of jQuery methods, <strong>it cannot be used in chaining</strong>. That is, it must be used directly on a selector, like so:

<pre><code class="language-javascript">$('#myDiv a').live('mouseover', function() {
	alert('hello');
});</code></pre>

But not…

<pre><code class="language-javascript">$('#myDiv').children('a').live('mouseover', function() {
	alert('hello');
});</code></pre>

… which will fail, as it will if you pass direct DOM elements, such as <code>$(document.body)</code>.

<code>delegate()</code>, which was developed as part of jQuery 1.4.2, goes some way to solving this problem by accepting as its first argument a context within the selector. For example:

<pre><code class="language-javascript">$('#myDiv').delegate('a', 'mouseover', function() {
	alert('hello');
});</code></pre>

Like <code>live()</code>, <code>delegate()</code> binds events both to current and future elements. Handlers are unbound via the <code>undelegate()</code> method.</p>

### Real-Life Example

For a real-life example, I want to stick with DOM-scripting, because this is an important part of any RIA (rich Internet application) built in JavaScript.

Let's imagine a flight-booking application. The user is asked to supply the names of all passengers travelling. Entered passengers appear as new rows in a table, <code>#passengersTable</code>, with two columns: “Name” (containing a text field for the passenger) and “Delete” (containing a button to remove the passenger's row).

To add a new passenger (i.e. row), the user clicks a button, <code>#addPassenger</code>:

<pre><code class="language-javascript">$('#addPassenger').click(function() {
	var tr = document.createElement('tr');
	var td1 = document.createElement('td');
	var input = document.createElement('input');
	input.type = 'text';
	$(td1).append(input);
	var td2 = document.createElement('td');
	var button = document.createElement('button');
	button.type = 'button';
	$(button).text('delete');
	$(td2).append(button);
	$(tr).append(td1);
	$(tr).append(td2);
	$('#passengersTable tbody').append(tr);
});</code></pre>

Notice that the event is applied to <code>#addPassenger</code> with <code>click()</code>, not <code>live('click')</code>, because we know <strong>this button will exist from the beginning</strong>.

What about the event code for the “Delete” buttons to delete a passenger?

<pre><code class="language-javascript">$('#passengersTable td button').live('click', function() {
	if (confirm("Are you sure you want to delete this passenger?"))
	$(this).closest('tr').remove();
});</code></pre>

Here, we apply the event with <code>live()</code> because the element to which it is being bound (i.e. the button) did not exist at runtime; it was DOM-scripted later in the code to add a passenger.

Handlers bound with <code>live()</code> are unbound with the <code>die()</code> method.

The convenience of <code>live()</code> comes at a price: one of its drawbacks is that you cannot pass an object of multiple event handlers to it. Only one handler.</p>

## 5\. .children() vs. .find()

Remember how the differences between <code>parent()</code>, <code>parents()</code> and <code>closest()</code> really boiled down to a question of reach? So it is here.</p>

### children()

This returns the immediate children of an element or elements returned by a selector. As with most jQuery DOM-traversal methods, it is optionally filtered with a selector. So, if we wanted to turn all <code>&lt;td&gt;</code>s orange in a table that contained the word “dog”, we could use this:

<pre><code class="language-javascript">$('#table tr').children('td:contains(dog)').css('background', '#f90');</code></pre>

### find()

This works very similar to <code>children()</code>, only it looks at both children and more distant descendants. It is also often a safer bet than <code>children()</code>.

Say it's your last day on a project. You need to write some code to hide all <code>&lt;tr&gt;</code>s that have the class <code>hideMe</code>. But some developers omit <code>&lt;tbody&gt;</code> from their table mark-up, so we need to cover all bases for the future. It would be risky to target the <code>&lt;tr&gt;</code>s like this…

<pre><code class="language-javascript">$('#table tbody tr.hideMe').hide();</code></pre>

… because that would fail if there's no <code>&lt;tbody&gt;</code>. Instead, we use <code>find()</code>:

<pre><code class="language-javascript">$('#table').find('tr.hideMe').hide();</code></pre>

This says that wherever you find a <code>&lt;tr&gt;</code> in <code>#table</code> with <code>.hideMe</code>, of whatever descendancy, hide it.</p>

## 6\. .not() vs. !.is() vs. :not()

As you'd expect from functions named “not” and “is,” these are opposites. But there's more to it than that, and these two are <strong>not really equivalents</strong>.</p>

### .not()

<code>not()</code> returns elements that do not match its selector. For example:

<pre><code class="language-javascript">$('p').not('.someclass').css('color', '#f90');</code></pre>

That turns all paragraphs that do <em>not</em> have the class <code>someclass</code> orange.</p>

### .is()

If, on the other hand, you want to target paragraphs that <em>do</em> have the class <code>someclass</code>, you could be forgiven for thinking that this would do it:

<pre><code class="language-javascript">$('p').is('.someclass').css('color', '#f90');</code></pre>

In fact, this would cause an error, because <strong><code>is()</code> does not return elements: it returns a boolean</strong>. It's a testing function to see whether any of the chain elements match the selector.

So when is <code>is</code> useful? Well, it's useful for querying elements about their properties. See the real-life example below.</p>

### :not()

<code>:not()</code> is the pseudo-selector equivalent of the method <code>.not()</code> It performs the same job; the only difference, as with all pseudo-selectors, is that you can use it in the middle of a selector string, and jQuery's string parser will pick it up and act on it. The following example is equivalent to our <code>.not()</code> example above:

<pre><code class="language-javascript">$('p:not(.someclass)').css('color', '#f90');</code></pre>

### Real-Life Example

As we've seen, <code>.is()</code> is used to test, not filter, elements. Imagine we had the following sign-up form. Required fields have the class <code>required</code>.

<pre><code class="language-markup tmp-html">&lt;form id='myform' method='post' action='somewhere.htm'&gt;
	&lt;label&gt;Forename *
	&lt;input type='text' class='required' /&gt;
	&lt;br /&gt;
	&lt;label&gt;Surname *
	&lt;input type='text' class='required' /&gt;
	&lt;br /&gt;
	&lt;label&gt;Phone number
	&lt;input type='text' /&gt;
	&lt;br /&gt;
	&lt;label&gt;Desired username *
	&lt;input type='text' class='required' /&gt;
	&lt;br /&gt;
	&lt;input type='submit' value='GO' /&gt;
&lt;/form&gt;</code></pre>

When submitted, our script should check that no required fields were left blank. If they were, the user should be notified and the submission halted.

<pre><code class="language-javascript">$('#myform').submit(function() {
	if ($(this).find('input').is('.required[value=]')) {
		alert('Required fields were left blank! Please correct.');
		return false; //cancel submit event
	}
});</code></pre>

Here we're not interested in returning elements to manipulate them, but rather just in querying their existence. Our <code>is()</code> part of the chain merely checks for the existence of fields within <code>#myform</code> that match its selector. It returns true if it finds any, which means required fields were left blank.</p>

## 7\. .filter() vs. .each()

These two are concerned with iteratively visiting each element returned by a selector and doing something to it.</p>

### .each()

<code>each()</code> loops over the elements, but it can be used in two ways. The first and most common involves passing a callback function as its only argument, which is also used to act on each element in succession. For example:

<pre><code class="language-javascript">$('p').each(function() {
	alert($(this).text());
});</code></pre>

This visits every <code>&lt;p&gt;</code> in our document and alerts out its contents.

What about the event code for the “Delete” buttons to delete a passenger?

<pre><code class="language-javascript">$('#passengersTable td button').live('click', function() {
	if (confirm("Are you sure you want to delete this passenger?"))
	$(this).closest('tr').remove();
});</code></pre>

Here, we apply the event with <code>live()</code> because the element to which it is being bound (i.e. the button) did not exist at runtime; it was DOM-scripted later in the code to add a passenger.

Handlers bound with <code>live()</code> are unbound with the <code>die()</code> method.

The convenience of <code>live()</code> comes at a price: one of its drawbacks is that you cannot pass an object of multiple event handlers to it. Only one handler.</p>

## 5\. .children() vs. .find()

Remember how the differences between <code>parent()</code>, <code>parents()</code> and <code>closest()</code> really boiled down to a question of reach? So it is here.</p>

### children()

This returns the immediate children of an element or elements returned by a selector. As with most jQuery DOM-traversal methods, it is optionally filtered with a selector. So, if we wanted to turn all <code>&lt;td&gt;</code>s orange in a table that contained the word “dog”, we could use this:

<pre><code class="language-javascript">$('#table tr').children('td:contains(dog)').css('background', '#f90');</code></pre>

### find()

This works very similar to <code>children()</code>, only it looks at both children and more distant descendants. It is also often a safer bet than <code>children()</code>.

Say it's your last day on a project. You need to write some code to hide all <code>&lt;tr&gt;</code>s that have the class <code>hideMe</code>. But some developers omit <code>&lt;tbody&gt;</code> from their table mark-up, so we need to cover all bases for the future. It would be risky to target the <code>&lt;tr&gt;</code>s like this…

<pre><code class="language-javascript">$('#table tbody tr.hideMe').hide();</code></pre>

… because that would fail if there's no <code>&lt;tbody&gt;</code>. Instead, we use <code>find()</code>:

<pre><code class="language-javascript">$('#table').find('tr.hideMe').hide();</code></pre>

This says that wherever you find a <code>&lt;tr&gt;</code> in <code>#table</code> with <code>.hideMe</code>, of whatever descendancy, hide it.</p>

## 6\. .not() vs. !.is() vs. :not()

As you'd expect from functions named “not” and “is,” these are opposites. But there's more to it than that, and these two are <strong>not really equivalents</strong>.</p>

### .not()

<code>not()</code> returns elements that do not match its selector. For example:

<pre><code class="language-javascript">$('p').not('.someclass').css('color', '#f90');</code></pre>

That turns all paragraphs that do <em>not</em> have the class <code>someclass</code> orange.</p>

### .is()

If, on the other hand, you want to target paragraphs that <em>do</em> have the class <code>someclass</code>, you could be forgiven for thinking that this would do it:

<pre><code class="language-javascript">$('p').is('.someclass').css('color', '#f90');</code></pre>

In fact, this would cause an error, because <strong><code>is()</code> does not return elements: it returns a boolean</strong>. It's a testing function to see whether any of the chain elements match the selector.

So when is <code>is</code> useful? Well, it's useful for querying elements about their properties. See the real-life example below.</p>

### :not()

<code>:not()</code> is the pseudo-selector equivalent of the method <code>.not()</code> It performs the same job; the only difference, as with all pseudo-selectors, is that you can use it in the middle of a selector string, and jQuery's string parser will pick it up and act on it. The following example is equivalent to our <code>.not()</code> example above:

<pre><code class="language-javascript">$('p:not(.someclass)').css('color', '#f90');</code></pre>

### Real-Life Example

As we've seen, <code>.is()</code> is used to test, not filter, elements. Imagine we had the following sign-up form. Required fields have the class <code>required</code>.

<pre><code class="language-markup tmp-html">&lt;form id='myform' method='post' action='somewhere.htm'&gt;
	&lt;label&gt;Forename *
	&lt;input type='text' class='required' /&gt;
	&lt;br /&gt;
	&lt;label&gt;Surname *
	&lt;input type='text' class='required' /&gt;
	&lt;br /&gt;
	&lt;label&gt;Phone number
	&lt;input type='text' /&gt;
	&lt;br /&gt;
	&lt;label&gt;Desired username *
	&lt;input type='text' class='required' /&gt;
	&lt;br /&gt;
	&lt;input type='submit' value='GO' /&gt;
&lt;/form&gt;</code></pre>

When submitted, our script should check that no required fields were left blank. If they were, the user should be notified and the submission halted.

<pre><code class="language-javascript">$('#myform').submit(function() {
	if ($(this).find('input').is('.required[value=]')) {
		alert('Required fields were left blank! Please correct.');
		return false; //cancel submit event
	}
});</code></pre>

Here we're not interested in returning elements to manipulate them, but rather just in querying their existence. Our <code>is()</code> part of the chain merely checks for the existence of fields within <code>#myform</code> that match its selector. It returns true if it finds any, which means required fields were left blank.</p>

## 7\. .filter() vs. .each()

These two are concerned with iteratively visiting each element returned by a selector and doing something to it.</p>

### .each()

<code>each()</code> loops over the elements, but it can be used in two ways. The first and most common involves passing a callback function as its only argument, which is also used to act on each element in succession. For example:

<pre><code class="language-javascript">$('p').each(function() {
	alert($(this).text());
});</code></pre>

This visits every <code>&lt;p&gt;</code> in our document and alerts out its contents.

But <code>each()</code> is more than just a method for running on selectors: it can also be used to handle <strong>arrays and array-like objects</strong>. If you know PHP, think <code>foreach()</code>. It can do this either as a method or as a core function of jQuery. For example…

<pre><code class="language-javascript">var myarray = ['one', 'two'];
$.each(myarray, function(key, val) {
	alert('The value at key '+key+' is '+val);
});</code></pre>

… is the same as:

<pre><code class="language-javascript">var myarray = ['one', 'two'];
$(myarray).each(function(key, val) {
	alert('The value at key '+key+' is '+val);
});</code></pre>

That is, for each element in <code>myarray</code>, in our callback function its key and value will be available to read via the <code>key</code> and <code>val</code> variables, respectively. The first of the two examples is the better choice, since it makes little sense to pass an array as a jQuery selector, even if it works.

One of the great things about this is that you can also iterate over objects — but only in the first way (i.e. <code>$.each</code>).

jQuery is known as a DOM-manipulation and effects framework, quite different in focus from other frameworks such as MooTools, but <code>each()</code> is an example of its occasional foray into extending JavaScript's native API.</p>

### .filter()

<code>filter()</code>, like <code>each()</code>, visits each element in the chain, but this time to remove it from the chain if it doesn't pass a certain test.

The most common application of <code>filter()</code> is to pass it a selector string, just like you would specify at the start of a chain. So, the following are equivalents:

<pre><code class="language-javascript">$('p.someClass').css('color', '#f90');
$('p').filter('.someclass').css('color', '#f90');</code></pre>

In which case, why would you use the second example? The answer is, sometimes you want to affect element sets that you cannot (or don't want to) change. For example:

<pre><code class="language-javascript">var elements = $('#someElement div ul li a');
//hundreds of lines later...
elements.filter('.someclass').css('color', '#f90');</code></pre>

<code>elements</code> was set long ago, so we cannot — indeed may not wish to — change the elements that return, but we might later want to filter them.

<code>filter()</code> really comes into its own, though, when you pass it a filter function to which each element in the chain in turn is passed. <strong>Whether the function returns true or false determines whether the element stays in the chain</strong>. For example:

<pre><code class="language-javascript">$('p').filter(function() {
	return $(this).text().indexOf('hello') != -1;
}).css('color', '#f90')</code></pre>

Here, for each <code>&lt;p&gt;</code> found in the document, if it contains the string <code>hello</code>, turn it orange. Otherwise, don't affect it.

We saw above how <code>is()</code>, despite its name, was not the equivalent of <code>not()</code>, as you might expect. Rather, <strong>use <code>filter()</code> <strong>or</strong> <strong><code>has()</code></strong> as the positive equivalent of <code>not()</code>.</strong>

Note also that unlike <code>each()</code>, <code>filter()</code> cannot be used on arrays and objects.</p>

### Real-Life Example

You might be looking at the example above, where we turned <code>&lt;p&gt;</code>s starting with <code>hello</code> orange, and thinking, "But we could do that more simply." You'd be right:

<pre><code class="language-javascript">$('p:contains(hello)').css('color', '#f90')</code></pre>

For such a simple condition (i.e. contains <code>hello</code>), that's fine. But <strong><code>filter()</code> is all about letting us perform more complex or long-winded evaluations</strong> before deciding whether an element can stay in our chain.

Imagine we had a table of CD products with four columns: artist, title, genre and price. Using some controls at the top of the page, the user stipulates that they do not want to see products for which the genre is “Country” or the price is above $10. These are two filter conditions, so we need a filter function:

<pre><code class="language-javascript">$('#productsTable tbody tr').filter(function() {
	var genre = $(this).children('td:nth-child(3)').text();
	var price = $(this).children('td:last').text().replace(/[^d.]+/g, ’);
	return genre.toLowerCase() == 'country' || parseInt(price) &gt;= 10;
}).hide();</code></pre>

So, for each <code>&lt;tr&gt;</code> inside the table, we evaluate columns 3 and 4 (genre and price), respectively. We know the table has four columns, so we can target column 4 with the <code>:last</code> pseudo-selector. For each product looked at, we assign the genre and price to their own variables, just to keep things tidy.

For the price, we replace any characters that might prevent us from using the value for mathematical calculation. If the column contained the value <code>$14.99</code> and we tried to compute that by seeing whether it matched our condition of being below $10, we would be told that it's not a number, because it contains the $ sign. Hence we strip away everything that is not number or dot.

Lastly, we return true (<strong>meaning the row will be hidden</strong>) if either of our conditions are met (i.e. the genre is country or the price is $10 or more).

<code>filter()</code>

## 8\. .merge() vs. .extend()

Let's finish with a foray into more advanced JavaScript and jQuery. We've looked at positioning, DOM manipulation and other common issues, but jQuery also provides some utilities for dealing with the native parts of JavaScript. This is not its main focus, mind you; libraries such as MooTools exist for this purpose.</p>

### .merge()

<code>merge()</code> allows you to merge the contents of two arrays into the first array. This entails <strong>permanent change for the first array</strong>. It does not make a new array; values from the second array are appended to the first:

<pre><code class="language-javascript">var arr1 = ['one', 'two'];
var arr2 = ['three', 'four'];
$.merge(arr1, arr2);</code></pre>

After this code runs, the <code>arr1</code> will contain four elements, namely <code>one</code>, <code>two</code>, <code>three</code>, <code>four</code>. <code>arr2</code> is unchanged. (If you're familiar with PHP, this function is equivalent to <code>array_merge()</code>.)

### .extend()

<code>extend()</code> does a similar thing, but for objects:

<pre><code class="language-javascript">var obj1 = {one: 'un', two: 'deux'}
var obj2 = {three: 'trois', four: 'quatre'}
$.extend(obj1, obj2);</code></pre>

<code>extend()</code> has a little more power to it. For one thing, you can merge more than two objects — you can pass as many as you like. For another, it can merge recursively. That is, if properties of objects are themselves objects, you can ensure that they are merged, too. To do this, pass <code>true</code> as the first argument:

<pre><code class="language-javascript">var obj1 = {one: 'un', two: 'deux'}
var obj2 = {three: 'trois', four: 'quatre', some_others: {five: 'cinq', six: 'six', seven: 'sept'}}
$.extend(true, obj1, obj2);</code></pre>

Covering everything about the behaviour of JavaScript objects (and how merge interacts with them) is beyond the scope of this article, but you can <a href="https://api.jquery.com/jQuery.extend/">read more here</a>.

The difference between <code>merge()</code> and <code>extend()</code> in jQuery is <strong>not the same as it is in MooTools</strong>. One is used to amend an existing object, the other creates a new copy.</p>

## There You Have It

We've seen some similarities, but more often than not intricate (and occasionally major) differences. jQuery is not a language, but it deserves to be learned as one, and by learning it you will make better decisions about what methods to use in what situation.

It should also be said that this article does not aim to be an exhaustive guide to all jQuery functions available for every situation. For DOM traversal, for example, there's also nextUntil() and parentsUntil().

While there are strict rules these days for writing semantic and SEO-compliant mark-up, JavaScript is still very much the playground of the developer. No one will demand that you use <code>click()</code> instead of <code>bind()</code>, but that's not to say one isn't a better choice than the other. It's all about the situation.</p>

## Related Posts

You may be interested in the following related posts:

*   [Seven JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/20/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)
*   [The Seven Deadly Sins Of JavaScript Implementation](https://www.smashingmagazine.com/2010/02/22/the-seven-deadly-sins-of-javascript-implementation/)
*   [Developing Sites With AJAX: Design Challenges and Common Issues](https://www.smashingmagazine.com/2010/02/10/some-things-you-should-know-about-ajax/)

<em>We appreciate the feedback of our Twitter followers who reviewed the article before it was published.</em>

{{< signature "al" >}}


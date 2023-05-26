---
title: Useful jQuery Function Demos For Your Projects
slug: 50-jquery-function-demos-for-aspiring-web-developers
image: https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cb4c953-d90d-470a-b8f4-5b6efd744896/50-jquery-function-demos.jpg
date: 2012-05-31T10:15:59.000Z
author: sam-deering
summary: >-
  This article sheds lights on some of the most popular jQuery functions that you can use to write fantastic code for your next Web development projects.
description: >-
  This article sheds lights on some of the most popular jQuery functions that you can use to write fantastic code for your next Web development projects.
categories:
  - Coding
  - CSS
  - jQuery
  - HTML
---
Every aspiring Web developer should know about the power of JavaScript and how it can be used to enhance the ways in which people see and interact with Web pages. Fortunately, to help us be more productive, we can use the power of JavaScript libraries, and in this article we will take a good look at jQuery in action.

![50 jQuery Function Demos for Aspiring Web Developers](https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9cb4c953-d90d-470a-b8f4-5b6efd744896/50-jquery-function-demos.jpg "50 jQuery Function Demos for Aspiring Web Developers")

### What Is jQuery?

In a nutshell, **jQuery is a leading JavaScript library** that can perform wonders on your Web pages and make your Web development life much easier and more enjoyable. With the rise in popularity of jQuery since its arrival in 2006, over an estimated 24 million websites (50% of them being the 10,000 most visited websites) currently reap the benefits, and as Google Trends suggests, it’s the most popular JavaScript library.

Thousands of Web developers worldwide use jQuery to innovate on their websites and stay up to date on trends. This surge has been influenced by several jQuery gurus who have helped make jQuery what is today. I would like to personally thank these guys and gals for their hard work and would like to do my part to spread the news about JavaScript and jQuery. In this article, we’ll show you over **50 of jQuery’s most renowned functions**, demonstrated with live visual examples. The jQuery library is comprehensive, so hopefully seeing these most frequently used functions in action will improve your understanding of how they can work together to produce excellent results.

## jQuery And CSS

Styles play a big part in the look and feel of any website, and jQuery can help us change them dynamically. In this section, we will look at how jQuery can be used to dynamically add and remove style classes and entire cascading style sheets.

### .css()

You can **change your website’s styles dynamically** with jQuery’s [.css()](https://api.jquery.com/css/) function. Either change styles that are already declared inline or in CSS files (such as `font-size`, `color`, `background-color`, etc.) or create new styles for elements.

### .addClass() and .toggleClass()

In addition to the `.css()` function, you can **apply currently defined CSS classes** by using the [.addClass()](https://api.jquery.com/addClass/) function. Its counterpart function, `.removeClass()`, reverses the action.

The [.toggleClass()](https://api.jquery.com/toggleClass/) function is a **huge time-saver** for toggling a state on and off with CSS. The following example sets event handlers for `mouseenter` (which applies the CSS class `img-hover` to the image) and `mouseleave` (which removes it).

## jQuery Animations And Effects

We can use jQuery to create some very smooth animations and effects with minimal effort. Animations and effects are always best demonstrated with examples, so let’s dive right in.

### .animate()

The [.animate()](https://api.jquery.com/animate/) function can be used to animate the movement and/or appearance of elements on a Web page. Let’s look at both. You may define the settings parameter with a set duration (in milliseconds) or any of the words `slow`, `normal` or `fast`. The callback, which is the function that runs after the animation has finished, is optional.

The `.animate()` function is asynchronous, so **multiple animations may run at the same time**. You can also use the `.stop()` function to stop the animation. If you click “Run demo” and then “Reset” during the animation, it will demonstrate the `.stop()` function.

**Many pure JavaScript functions** are used frequently in animations, such as `setInterval()`, `clearInterval()`, `setTimeout()` and `clearTimeout()`. Once again, these functions are included in the list because understanding what they can do is important to supporting the jQuery’s animation functions.

### setInterval() and clearInterval()

You can **automate a task based on time** using the JavaScript `setInterval()` function, which can be used to specify a regular time-based trigger.

### setTimeout() and clearTimeout()

You can also **delay a task based on time** using the JavaScript `setTimeout()` function, which can be set to wait for a specified length of time before running the code.

### .slideToggle() and .fadeToggle()

jQuery provides various toggle functions that save us heaps of time when we want to **bind related events to the same element**. For example, [.slideToggle()](https://api.jquery.com/slideToggle/) binds both [.slideUp()](https://api.jquery.com/slideUp/) and [.slideDown()](https://api.jquery.com/slideDown/) to the element and also manages that state for us.

The `.fadeToggle()` function is similar to `.slideToggle()` but with a **fading effect** that uses the `.fadeIn()` and `.fadeOut()` methods.

### .delay()

In this demonstration, we’ll mainly use jQuery’s awesome function-chaining ability by running the `.fadeOut()`, `.fadeIn()` and `.delay()` functions together on the same element. This is very similar to the `setTimeout()` function we saw earlier but without allowing us to easily interrupt the delay.

## jQuery And DOM Manipulation

The DOM (document object model) is all of the HTML content that you see on a website (text, images, container elements, etc.). We can use jQuery to **perform wonders with the DOM** when all page elements have been loaded. The event that captures when the DOM is ready is called [`.ready()`](https://api.jquery.com/ready/), and there are a [few ways](https://www.jquery4u.com/dom-modification/types-document-ready/) to call it. In this section are demos of jQuery functions that change the DOM in some way.

### .clone()

The jQuery [`.clone()`](https://api.jquery.com/clone/) function is pretty simple to use; it basically just copies the element that you specify into a new element.

### .html(), .text() and .empty()

Using [`.html()`](/https://api.jquery.com/html/) is the most common way to **get or set the content of an element** using jQuery. If you just want the text and not the HTML tags, you can use [`.text()`](https://api.jquery.com/text/), which will return a string containing the combined text of all matched elements. These functions are browser-dependent (i.e. `.html()` uses the browser’s `innerHTML` property), so the results returned (including white space and line breaks) will always depend on the browser you are using.

In this example, we are also making use of the [`.empty()`](https://api.jquery.com/empty/) function, which is a quick way to get rid of the content within, and `.prev()`, which can be used to reference the preceding element, in this case the demo buttons.

### .append(), prepend(), .after() and .before()

These function provide the means of **inserting content in particular places** relative to elements already on the Web page. Although the differences may appear trivial, each has its own purpose, and knowing exactly where they will all place content will save you coding time.

## jQuery And AJAX

The jQuery library has a full suite of AJAX capabilities that **enables us to load data from a server without refreshing the browser page**. In this section, we will have a quick look at refreshing page content, loading scripts and retrieving data from different Web pages and servers.

### $.ajax()

The [`$.ajax()`](https://api.jquery.com/jQuery.ajax/) function is arguably the most used jQuery function. It gives us a means of **dynamically loading content, scripts and data** and using them on a live Web page. Other common uses are submitting a form using AJAX and sending data to server-side scripts for storing in a database.

The `$.ajax()` function has a lot of settings, and the kind team at jQuery has provided many **shorthand AJAX methods that already contain the settings we require**. Some developers like to write out the full AJAX settings, mainly because they require more options than many shorthand methods provide (such as `beforeSubmit()`). Also, note that you can use the Firebug NET.panel to [analyze HTTP requests](https://www.jquery4u.com/testing/http-request-net-panel-httpfox-fiddler2/) for testing, monitoring and debugging AJAX calls.

Demo: Use `$.ajax()` to load content without reloading the entire page.

For this demo, HTML content is held in separate files, which are inserted below using AJAX. Showing a loading icon while an AJAX request is processing is courteous. The third content block below has a two-second delay to simulate the loading icon.

We can also use functions such as [`$.parseJSON()`](https://api.jquery.com/jQuery.parseJSON/) and [`JSON.parse()`](https://www.json.org/js.html) from ECMAScript5, which simplifies JSON parsing. If you’re interested in JSON parsing and tree recursion, see the “Online JSON Tree Viewer Tool.”

### .load()

The [`.load()`](https://api.jquery.com/load/) function is an AJAX **shorthand method for inserting HTML** straight into a matched element on the Web page.

### JSONP

AJAX requests are subject to the [same origin policy](https://en.wikipedia.org/wiki/Same_origin_policy), which means you may only send requests to the same domain. Fortunately, `$.ajax()` has a property named [JSONP](https://www.jquery4u.com/json/jsonp-examples/) (i.e. JSON with padding), which allows a page to request data from a server on a different domain. It works by wrapping the target data in a JavaScript callback function. Note that the response is not parsed as JSON and may be any JavaScript expression.

The AJAX shorthand functions [`$.getJSON`](https://api.jquery.com/jQuery.getJSON/) and [`$.getScript`](https://api.jquery.com/jQuery.getScript/) and more AJAX examples can be found on my blog.

## jQuery And Events

Managing events using regular JavaScript is entirely possible, however, jQuery provides a much more user-friendly interface to manage Web page events. Examples of such events are clicking a hyperlink, moving the mouse over an image and even pressing a key on the keyboard; the list goes on. Here are some examples of key jQuery functions that may be used to manage events.

### .bind() and .unbind()

The [`.bind()`](https://api.jquery.com/bind/) function is very useful for **adding event triggers and handlers to your DOM elements**. In case you didn’t know, you can bind your DOM elements to a whole [list of events](https://www.jquery4u.com/events/jquery-list-events-bind/), such as `submit`, `change`, `mouseenter` and `mouseleave`.

You may have also seen [`.click()`](https://api.jquery.com/click/) used in jQuery code. There is no functional difference between `.click()` and `.bind('click')`, but with the latter we have the benefits of being able to specify custom events and add data parameters. There is also an [`.unbind()`](https://api.jquery.com/unbind/) function to remove any events that have already been bound. As of jQuery 1.7 the .bind() function is an alias to .on() function. When you type in console: “_jQuery.fn.bind.toString()_” it will return: “_function (a, b, c) { return this.on(a, null, b, c); }_“.

**Note:** The key difference between `keydown` and `keypress` events is that the latter captures each individual character entered, as opposed to just firing once per key press. To illustrate, this simple tool [shows the keycodes for any key](https://www.jquery4u.com/events/find-keycode-keyboard-key-press) that you press.

### .live(), .on() and .off()

The [`.live()`](https://api.jquery.com/live/) function is essentially the same as `.bind()`, but it can **capture events on new elements** that didn’t exist on the page when it was loaded; for example, if your Web page has loaded and then you dynamically insert an image onto it. If we used `.bind()` to attach an event when the mouse hovers over the image, it would not work. But if we used `.live()`, it would work! As of jQuery 1.7, you are advised to **make use of the new `.on()` and `.off()` functions**, instead of the `.live()` function, which has a few disadvantages to [`.on()`](https://api.jquery.com/on/). See “[jQuery 1.7+ `.on()` vs. `.live()` Review](https://www.jquery4u.com/jquery-functions/on-vs-live-review/)” for a more detailed explanation of the differences.

### .delegate()

The [`.delegate()`](https://api.jquery.com/delegate/) function provides a means of attaching event handlers to new elements (similar to the `.live()` function covered above). You might find **`.delegate()` to be faster than `.live()`** because the latter searches the entire document namespace for the elements as opposed to a single document. The much more important difference is that `.live()` is prone to break if used with traversing.

### .preventDefault()

The [`.preventDefault()`](https://api.jquery.com/event.preventDefault/) function can be applied to **stop any element with a default action from firing**: hyperlinks, keyboard shortcuts, form submit buttons, etc. These are probably the most common uses, and the function stops the hyperlink from going to its destination (the `href`). It’s very useful for stopping those default actions and running your custom JavaScript actions instead.

### .stopPropagation()

There are methods that do things similar to `.preventDefault()` but that behave differently. The [`.stopPropagation()`](https://api.jquery.com/event.stopPropagation/) function **prevents the event from occurring on any ancestor elements**. This can be used if you have an exception to the rule that you’ve specified for a container element with child elements. This function currently **does not work with `.live()` events** because it handles events once they have propagated to the top of the document.

### .stopImmediatePropagation()

This function is nice for **stopping all future bound events**. The events will fire in the order they were bound, and when it hits the [`.stopImmediatePropagation()`](https://api.jquery.com/event.stopImmediatePropagation/) function, all further bound events are not fired.

## Finding, Looping And Filtering Results

jQuery gives us fast access to finding anything on the page and the ability to **loop through or filter results** as we please. It also has **powerful functions to manipulate and extend data** and functionality associated with JavaScript objects. There are so many things to cover in this section, so we have narrowed them down to a few key functions.

### $.each() and .each()

There are two different methods for iterating with jQuery: [`.each()`](https://api.jquery.com/each/) is used to iterate only over jQuery objects collections, while [`$.each()`](https://api.jquery.com/jquery.each/) is a general function for iterating over JavaScript objects and arrays. I am a big fan of functions such as these and [JavaScript shorthand techniques](https://www.jquery4u.com/javascript/shorthand-javascript-techniques/) that provide us with a fast alternative to basic JavaScript coding.

You can use `$.each()` and `.each()` on a lot of different things, such as DOM elements, arrays, objects and JSON. For those of you who are keen, you could try [five more jQuery `.each()` examples](https://www.jquery4u.com/jquery-functions/jquery-each-examples/).

### $.data(), .data(), $.hasData() and $.removeData()

Updates to the jQuery library (mainly since 1.4) has brought the ability to **attach data of any type to DOM elements**. This is a very useful alternative to storing data in JavaScript objects and other such methods. There are two versions: [`$.data()`](https://api.jquery.com/jquery.data/), which takes in the element as a parameter, and [`.data()`](https://api.jquery.com/data/), which can attach directly to matched elements.

Note that `$.data()` returns a data object to the caller, whereas `.data()` does not. There are also many utility functions, such as [`$.hasData()`](https://api.jquery.com/jQuery.hasData/), [`$.removeData()`](https://api.jquery.com/jQuery.removeData/), that help with data management.

### .match(), .test() and :contains()

Together with the jQuery [`:contains()`](https://api.jquery.com/contains-selector/) selector, you can use the pure JavaScript functions `.match()` and `.test()` to **save time when filtering for string values**. Let’s look at some examples.

We can use `.test()` to check whether any emails are present, and use `.match()` to extract them. We can also use the `:contains()` selector to match substrings inside any of that element’s descendants (this is case sensitive).

### .find()

The [`.find()`](https://api.jquery.com/find/) function is very useful for **matching elements filtered by a selector, jQuery object or element**. The `.find()` function can be used with the functions [`.children()`](https://api.jquery.com/children/) (which searches only the direct child siblings of the matched elements) and [`.parents()`](https://api.jquery.com/parents/) (which searches the direct parent elements of the matched element).

### .filter()

The [`.filter()`](https://api.jquery.com/filter/) function allows us to **reduce a set of matched elements** based on a jQuery selector. This is useful when you want to process a group of elements and then further process specific child elements. The `.filter()` function can be used in a few different ways, such as to filter by a class name, function or jQuery object.

### .slice()

The [`.slice()`](https://api.jquery.com/slice/) function lets us easily **specify a subset of elements to perform actions on**. It takes two parameters: `start` and `end` indices of subelements in a matched parent element.

Demo: Use `.slice()` to perform actions on a subset of elements.

### .prev() and next()

The [`.prev()`](https://api.jquery.com/prev/) and [`.next()`](https://api.jquery.com/next/) functions can be used to **reference the immediately preceding or next element in a set of matched elements** (in the DOM hierarchy). You can also add a selector to the functions that acts as a filter on the elements (shown in the demo).

### $.extend()

The [`$.extend()`](https://api.jquery.com/jquery.extend/) function can be used to **combine two or more objects** into the first object or into a completely new object.

Instead of copying all of the code that processes the form, we can use `$.extend()` to **copy the functionality to our new forms**, thus avoiding repetitive code. You might have noticed that the target element specified is a blank object; this is a trick that you will often see to create a new object of `object1` and extend it with `objectN` (`N` representing any number of objects). So, in the example, we want to “copy” the existing functionality of `forms.enquiry` and simply override the email address.

Addy Osmani’s book _Learning JavaScript Design Patterns_ gives greater insight into how to use the `$.extend()` function to override the default values of jQuery plugins.

### .serialize() and .serializeArray()

The [`.serialize()`](https://api.jquery.com/serialize/) and [`.serializeArray()`](https://api.jquery.com/serializeArray/) functions can **create string and array values from form fields** in seconds! There are two demos here: the first outputs all of the form’s fields and their values, and the second creates a URL string with the form fields and values appended to the form action ready to be sent.

## Conclusion

Although we have only scratched the surface of jQuery in this article, we hope you have learned something about some of the most popular jQuery functions and are able to use them to write fantastic code for your next Web development project. Thanks for reading!

{{< signature "al, km, il" >}}

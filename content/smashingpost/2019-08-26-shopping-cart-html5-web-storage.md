---
title: 'Creating A Shopping Cart With HTML5 Web Storage'
slug: shopping-cart-html5-web-storage
author: matt-zand
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53da399b-33d2-4f64-a09f-977426c72136/shopping-cart-html5-web-storage.png
date: 2019-08-26T14:30:59+02:00
summary: >-
  This tutorial will show you how  to harness the power of HTML5 web storage by creating a shopping cart step-by-step. What you learn from this tutorial can easily be applied to other site features that may not require database storage such as user preferences, users’ favorite contents, wish list, user settings like username and password and more.<br /><br /><strong>Update (27,29 Aug) Editor’s Note</strong>: We have updated the examples to address accessibility issues in the HTML.
description: >-
  This tutorial will show you how to harness the power of HTML5 web storage by creating a shopping cart step-by-step. What you learn from this tutorial can easily be applied to other site features that may not require database storage and more.
categories:
  - E-Commerce
  - HTML5
---
With the advent of HTML5, many sites were able to replace JavaScript plugin and codes with simple more efficient HTML codes such as audio, video, geolocation, etc. HTML5 tags made the job of developers much easier while enhancing page load time and site performance. In particular, HTML5 web storage was a game changer as they allow users’ browsers to store user data without using a server. So the creation of web storage, allowed front-end developers to accomplish more on their website without knowing or using server-side coding or database.

Online e-commerce websites predominantly use server-side languages such as PHP to store users’ data and pass them from one page to another. Using JavaScript back-end frameworks such as Node.js, we can achieve the same goal. However, in this tutorial, we’ll show you step by step how to build a shopping cart with HTML5 and some minor JavaScript code. Other uses of the techniques in this tutorial would be to store user preferences, the user’s favorite content, wish lists, and user settings like name and password on websites and native mobile apps without using a database.

Many high-traffic websites rely on complex techniques such as server clustering, DNS load balancers, client-side and server-side caching, distributed databases, and microservices to optimize performance and availability. Indeed, the major challenge for dynamic websites is to fetch data from a database and use a server-side language such as PHP to process them. However, remote database storage should be used only for essential website content, such as articles and user credentials. Features such as user preferences can be stored in the user’s browser, similar to cookies. Likewise, when you build a native mobile app, you can use HTML5 web storage in conjunction with a local database to increase the speed of your app. Thus, as front-end developers, we need to explore ways in which we can exploit the power of HTML5 web storage in our applications in the early stages of development.

I have been a part of a team developing a large-scale social website, and we used HTML5 web storage heavily. For instance, when a user logs in, we store the hashed user ID in an HTML5 session and use it to authenticate the user on protected pages. We also use this feature to store all new push notifications — such as new chat messages, website messages, and new feeds — and pass them from one page to another. When a social website gets high traffic, total reliance on the server for load balancing might not work, so you have to identify tasks and data that can be handled by the user’s browser instead of your servers.

{{% feature-panel %}}

## Project Background

A shopping cart allows a website’s visitor to view product pages and add items to their basket. The visitor can review all of their items and update their basket (such as to add or remove items). To achieve this, the website needs to store the visitor’s data and pass them from one page to another, until the visitor goes to the checkout page and makes a purchase. Storing data can be done via a server-side language or a client-side one. With a server-side language, the server bears the weight of the data storage, whereas with a client-side language, the visitor’s computer (desktop, tablet or smartphone) stores and processes the data.  Each approach has its pros and cons. In this tutorial, we’ll focus on a simple client-side approach, based on HTML5 and JavaScript.

**Note**: *In order to be able to follow this tutorial, basic knowledge of HTML5, CSS and JavaScript is required.*

### Project Files

Click [here](https://smashingmagazine.com/provide/html5-js-shopping-cart-source-files.zip) to download the project’s source files. You can see a [live demo](https://blockchain.dcwebmakers.com/demo/html5-js-shopping-cart/index.html), too.

## Overview Of HTML5 Web Storage

HTML5 web storage allows web applications to store values locally in the browser that can survive the browser session, just like cookies. Unlike cookies that need to be sent with every HTTP request, web storage data is never transferred to the server; thus, web storage outperforms cookies in web performance. Furthermore, cookies allow you to store only 4 KB of data per domain, whereas web storage allows at least 5 MB per domain. Web storage works like a simple array, mapping keys to values, and they have two types:

- **Session storage**  
This stores data in one browser session, where it becomes available until the browser or browser tab is closed. Popup windows opened from the same window can see session storage, and so can iframes inside the same window. However, multiple windows from the same origin (URL) cannot see each other’s session storage.
- **Local storage**  
This stores data in the web browser with no expiration date. The data is available to all windows with the same origin (domain), even when the browser or browser tabs are reopened or closed.

Both storage types are currently supported in all major web browsers. Keep in mind that you cannot pass storage data from one browser to another, even if both browsers are visiting the same domain.

## Build A Basic Shopping Cart

To build our shopping cart, we first create an HTML page with a simple cart to show items, and a simple form to add or edit the basket. Then, we add HTML web storage to it, followed by JavaScript coding. Although we are using HTML5 local storage tags, all steps are identical to those of HTML5 session storage and can be applied to HTML5 session storage tags. Lastly, we’ll go over some jQuery code, as an alternative to JavaScript code, for those interested in using jQuery.

## Add HTML5 Local Storage To Shopping Cart

Our HTML page is a basic page, with tags for external JavaScript and CSS referenced in the head.

<div class="break-out">

 <pre><code class="language-html">&lt;!doctype html&gt;
&lt;html lang="en-US"&gt;
&lt;head&gt;
&lt;title&gt;HTML5 Local Storage Project&lt;/title&gt;
&lt;meta charset="UTF-8"&gt;
&lt;meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"&gt;
&lt;meta name="rating" content="General"&gt;
&lt;meta name="expires" content="never"&gt;
&lt;meta name="language" content="English, EN"&gt;
&lt;meta name="description" content="Shopping cart project with HTML5 and JavaScript"&gt;
&lt;meta name="keywords" content="HTML5,CSS,JavaScript, html5 session storage, html5 local storage"&gt;
&lt;meta name="author" content="dcwebmakers.com"&gt;
&lt;script src="Storage.js"&gt;&lt;/script&gt;
&lt;link rel="stylesheet" href="StorageStyle.css"&gt;
&lt;/head&gt;
</code></pre>
</div>

Below is the HTML content that appears in the page’s body:

<div class="break-out">

 <pre><code class="language-html">&lt;form name="ShoppingList"&gt;
	&lt;fieldset&gt;
		&lt;legend&gt;Shopping cart&lt;/legend&gt;
		&lt;label&gt;Item: &lt;input type="text" name="name"&gt;&lt;/label&gt;
		&lt;label&gt;Quantity: &lt;input type="text" name="data"&gt;&lt;/label&gt;

		&lt;input type="button" value="Save"   onclick="SaveItem()"&gt;
		&lt;input type="button" value="Update" onclick="ModifyItem()"&gt;
		&lt;input type="button" value="Delete" onclick="RemoveItem()"&gt;
	&lt;/fieldset&gt;
	&lt;div id="items_table"&gt;
		&lt;h2&gt;Shopping List&lt;/h2&gt;
		&lt;table id="list"&gt;&lt;/table&gt;
		&lt;label&gt;&lt;input type="button" value="Clear" onclick="ClearAll()"&gt;
		* Delete all items&lt;/label&gt;
	&lt;/div&gt;
&lt;/form&gt;
</code></pre>
</div>

## Adding JavaScript To The Shopping Cart

We’ll create and call the JavaScript function `doShowAll()` in the `onload()` event to check for browser support and to dynamically create the table that shows the storage name-value pair.

<pre><code class="language-javascript">&lt;body onload="doShowAll()"&gt;
</code></pre>

Alternatively, you can use the JavaScript onload event by adding this to the JavaScript code:

<pre><code class="language-javascript">window.load=doShowAll();
</code></pre>

Or use this for jQuery:

<pre><code class="language-javascript">$( window ).load(function() {
  doShowAll();
});
</code></pre>

In the `CheckBrowser()` function, we would like to check whether the browser supports HTML5 storage. Note that this step might not be required because most modern web browsers support it.

<div class="break-out">

 <pre><code class="language-javascript">/*
=====> Checking browser support.
 //This step might not be required because most modern browsers do support HTML5.
 */
 //Function below might be redundant.
function CheckBrowser() {
	if ('localStorage' in window && window['localStorage'] !== null) {
		// We can use localStorage object to store data.
		return true;
	} else {
			return false;
	}
}
</code></pre>
</div>

Inside the `doShowAll()`, if the `CheckBrowser()` function evaluates first for browser support, then it will dynamically create the table for the shopping list during page load. You can iterate the keys (property names) of the key-value pairs stored in local storage inside a JavaScript loop, as shown below. Based on the storage value, this method populates the table dynamically to show the key-value pair stored in local storage.

<div class="break-out">

 <pre><code class="language-javascript">// Dynamically populate the table with shopping list items.
//Step below can be done via PHP and AJAX, too.
function doShowAll() {
	if (CheckBrowser()) {
		var key = "";
		var list = "&lt;tr&gt;&lt;th&gt;Item&lt;/th&gt;&lt;th&gt;Value&lt;/th&gt;&lt;/tr&gt;\n";
		var i = 0;
		//For a more advanced feature, you can set a cap on max items in the cart.
		for (i = 0; i &lt;= localStorage.length-1; i++) {
			key = localStorage.key(i);
			list += "&lt;tr&gt;&lt;td&gt;" + key + "&lt;/td&gt;\n&lt;td&gt;"
					+ localStorage.getItem(key) + "&lt;/td&gt;&lt;/tr&gt;\n";
		}
		//If no item exists in the cart.
		if (list == "&lt;tr&gt;&lt;th&gt;Item&lt;/th&gt;&lt;th&gt;Value&lt;/th&gt;&lt;/tr&gt;\n") {
			list += "&lt;tr&gt;&lt;td&gt;&lt;i&gt;empty&lt;/i&gt;&lt;/td&gt;\n&lt;td&gt;&lt;i&gt;empty&lt;/i&gt;&lt;/td&gt;&lt;/tr&gt;\n";
		}
		//Bind the data to HTML table.
		//You can use jQuery, too.
		document.getElementById('list').innerHTML = list;
	} else {
		alert('Cannot save shopping list as your browser does not support HTML 5');
	}
}
</code></pre>
</div>

**Note**: *Either you or your framework will have a preferred method of creating new DOM nodes and handling events. To keep things clear and focused, our example uses* `.innerHTML` and inline event handlers *even though we'd normally avoid that in production code.*

**Tip:** *If you’d like to use jQuery to bind data, you can just replace* `document.getElementById('list').innerHTML = list;` *with* `$(‘#list’).html()=list;`.

{{% ad-panel-leaderboard %}}

## Run And Test The Shopping Cart

In the previous two sections, we added code to the HTML head, and we added HTML to the shopping cart form and basket. We also created a JavaScript function to check for browser support and to populate the basket with the items in the cart. In populating the basket items, the JavaScript fetches values from HTML web storage, instead of a database. In this part, we’ll show you how the data are inserted into the HTML5 storage engine. That is, we’ll use HTML5 local storage in conjunction with JavaScript to insert new items to the shopping cart, as well as edit an existing item in the cart.

**Note**: *I’ve added tips sections below to show jQuery code, as an alternative to the JavaScript ones.*

We’ll create a separate HTML `div` element to capture user input and submission. We’ll attach the corresponding JavaScript function in the `onClick` event for the buttons.

<div class="break-out">

 <pre><code class="language-javascript">&lt;input type="button" value="Save"   onclick="SaveItem()"&gt;
&lt;input type="button" value="Update" onclick="ModifyItem()"&gt;
&lt;input type="button" value="Delete" onclick="RemoveItem()"&gt;
</code></pre>
</div>

You can set properties on the `localStorage` object similar to a normal JavaScript object. Here is an example of how we can set the local storage property `myProperty` to the value `myValue`:

<pre><code class="language-javascript">localStorage.myProperty="myValue";
</code></pre>

You can delete local storage property like this:

<pre><code class="language-javascript">delete localStorage.myProperty;
</code></pre>

Alternately, you can use the following methods to access local storage:

<pre><code class="language-javascript">localStorage.setItem('propertyName','value');
localStorage.getItem('propertyName');
localStorage.removeItem('propertyName');
</code></pre>

To save the key-value pair, get the value of the corresponding JavaScript object and call the `setItem`  method:

<pre><code class="language-javascript">function SaveItem() {

    var name = document.forms.ShoppingList.name.value;
    var data = document.forms.ShoppingList.data.value;
    localStorage.setItem(name, data);
    doShowAll();

}
</code></pre>

Below is the jQuery alternative for the `SaveItem` function. First, add an ID to the form inputs:

<pre><code class="language-javascript">&lt;label&gt;Item: &lt;input type="text" name="name" id="name"&gt;&lt;/label&gt;
&lt;label&gt;Quantity: &lt;input type="text" name="data" id="data"&gt;&lt;/label&gt;
</code></pre>

Then, select the form inputs by ID, and get their values. As you can see below, it is much simpler than JavaScript:

<pre><code class="language-javascript">function SaveItem() {
    var name = $("#name").val();
    var data = $("#data").val();
    localStorage.setItem(name, data);
    doShowAll();
}
</code></pre>

To update an item in the shopping cart, you have to first check whether that item’s key already exists in local storage, and then update its value, as shown below:

<div class="break-out">

 <pre><code class="language-javascript">//Change an existing key-value in HTML5 storage.
function ModifyItem() {
	var name1 = document.forms.ShoppingList.name.value;
	var data1 = document.forms.ShoppingList.data.value;
	//check if name1 is already exists

//Check if key exists.
			if (localStorage.getItem(name1) !=null)
			{
			  //update
			  localStorage.setItem(name1,data1);
			  document.forms.ShoppingList.data.value = localStorage.getItem(name1);
			}

	doShowAll();
}
</code></pre>
</div>

Below shows the jQuery alternative.

<div class="break-out">

 <pre><code class="language-javascript">function ModifyItem() {
    var name1 = $("#name").val();
    var data1 = $("#data").val();
    //Check if name already exists.
//Check if key exists.
   		 if (localStorage.getItem(name1) !=null)
   		 {
   		   //update
   		   localStorage.setItem(name1,data1);
   		   var new_info=localStorage.getItem(name1);
   		   $("#data").val(new_info);
   		 }

    doShowAll();
}
</code></pre>
</div>

We will use the `removeItem` method to delete an item from storage.

<div class="break-out">

 <pre><code class="language-javascript">function RemoveItem()
{
var name=document.forms.ShoppingList.name.value;
document.forms.ShoppingList.data.value=localStorage.removeItem(name);
doShowAll();
}
</code></pre>
</div>

**Tip:** *Similar to the previous two functions, you can use jQuery selectors in the* `RemoveItem` *function.*

There is another method for local storage that allows you to clear the entire local storage. We call the `ClearAll()` function in the `onClick` event of the “Clear” button:

<pre><code class="language-javascript">&lt;input type="button" value="Clear" onclick="ClearAll()"&gt;
</code></pre>

We use the `clear` method to clear the local storage, as shown below:

<pre><code class="language-javascript">function ClearAll() {
    localStorage.clear();
    doShowAll();
}
</code></pre>

## Session Storage

The `sessionStorage` object works in the same way as `localStorage`. You can replace the above example with the `sessionStorage` object to expire the data after one session. Once the user closes the browser window, the storage will be cleared. In short, the APIs for `localStorage` and `sessionStorage` are identical, allowing you to use the following methods:

- `setItem(key, value)`
- `getItem(key)`
- `removeItem(key)`
- `clear()`
- `key(index)`
- `length`

{{% ad-panel-leaderboard %}}

## Shopping Carts With Arrays And Objects

Because HTML5 web storage only supports single name-value storage, you have to use JSON or another method to convert your arrays or objects into a single string. You might need an array or object if you have a category and subcategories of items, or if you have a shopping cart with multiple data, like customer info, item info, etc. You just need to implode your array or object items into a string to store them in web storage, and then explode (or split) them back to an array to show them on another page. Let’s go through a basic example of a shopping cart that has three sets of info: customer info, item info and custom mailing address. First, we use JSON.stringify to convert the object into a string. Then, we use JSON.parse to reverse it back.

**Hint**: *Keep in mind that the key-name should be unique for each domain.*

<div class="break-out">

 <pre><code class="language-javascript">//Customer info
//You can use array in addition to object.
var obj1 = { firstname: "John", lastname: "thomson" };
var cust = JSON.stringify(obj1);

//Mailing info
var obj2 = { state: "VA", city: "Arlington" };
var mail = JSON.stringify(obj2);

//Item info
var obj3 = { item: "milk", quantity: 2 };
var basket = JSON.stringify(obj3);

//Next, push three strings into key-value of HTML5 storage.

//Use JSON parse function below to convert string back into object or array.
var New_cust=JSON.parse(cust);
</code></pre>
</div>

## Summary

In this tutorial, we have learned how to build a shopping cart step by step using HTML5 web storage and JavaScript. We’ve seen how to use jQuery as an alternative to JavaScript. We’ve also discussed JSON functions like stringify and parse to handle arrays and objects in a shopping cart. You can build on this tutorial by adding more features, like adding product categories and subcategories while storing data in a JavaScript multi-dimensional array. Moreover, you can replace the whole JavaScript code with jQuery.

We’ve seen what other things developers can accomplish with HTML5 web storage and what other features they can add to their websites. For example, you can use this tutorial to store user preferences, favorited content, wish lists, and user settings like names and passwords on websites and native mobile apps, without using a database.

To conclude, here are a few issues to consider when implementing HTML5 web storage:

- Some users might have privacy settings that prevent the browser from storing data.
- Some users might use their browser in incognito mode.
- Be aware of a few security issues, like DNS spoofing attacks, cross-directory attacks, and sensitive data compromise.

### Related Reading

- “[Browser Storage Limits And Eviction Criteria](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Browser_storage_limits_and_eviction_criteria),” MDN web docs, Mozilla
- “[Web Storage](https://html.spec.whatwg.org/multipage/webstorage.html),” HTML Living Standard,
- “[This Week In HTML 5](https://blog.whatwg.org/this-week-in-html-5-episode-30),” The WHATWG Blog

{{< signature "dm, il" >}}

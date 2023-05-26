---
title: Creating A Client-Side Javascript Shopping Cart
slug: create-client-side-shopping-cart
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2259d8f2-d4b6-420e-8a89-b793f4b0cd40/code-react-opt.jpg'
date: 2014-02-13T10:59:19.000Z
author: gabriele-romanato
description: >-
  In this series of articles, we’ll cover in depth a practical implementation of
  session storage by creating a complete e-commerce shopping cart with the
  `sessionStorage` object and jQuery.
categories:
  - Coding
  - PHP
  - JavaScript
  - jQuery
  - HTML
---
Session storage is a new feature introduced by the W3C’s “<a href="https://www.w3.org/TR/webstorage/">Web Storage</a>” specification. It’s supported in Internet Explorer 8+, Firefox, Chrome, Safari and Opera Desktop (for a complete list, please consult “<a href="https://caniuse.com/#feat=namevalue-storage">Can I Use</a>”). In this series of articles, we’ll cover in depth a practical implementation of session storage by creating a complete e-commerce shopping cart with the <code>sessionStorage</code> object and jQuery.

Bear in mind that, in these articles, I’m not going to propose a new technique to replace existing server-side techniques, but rather just a proof of concept of session storage.</p>

## Session Storage: A Quick Reminder

We use sessions to store data and share such data across several pages. Usually, a user would pick a product, and we’d save the product’s name along with the chosen quantity and price.

Then, the user would fill out a form with their personal information, and we’d save it in the current session before the end of the process, which is typically the checkout page and the subsequent redirection to the payment gateway (for example, PayPal).

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Fundamental Guidelines Of E-Commerce Checkout Design](https://www.smashingmagazine.com/2011/04/fundamental-guidelines-of-e-commerce-checkout-design/)
*   [Reducing Abandoned Shopping Carts In E-Commerce](https://www.smashingmagazine.com/2014/10/reducing-abandoned-shopping-carts/)
*   [Local Storage And How To Use It On Websites](https://www.smashingmagazine.com/2010/10/local-storage-and-how-to-use-it/)
*   [A Little Journey Through (Small And Big) E-Commerce Websites](https://www.smashingmagazine.com/2013/12/e-commerce-websites-showcase/)

<strong>How are shopping carts built?</strong> PHP, for instance, makes frequent use of associative arrays to create the basic structure of a shopping cart. Associative arrays enable PHP Web developers to keep session data structured and organized.

JavaScript sessions work differently. Generally, a session expires when the user closes their browser (but bear in mind that the concept of “closing a browser” is not clear on mobile devices). When a session expires, all data stored in the session storage of a Web browser is removed. There’s no need to explicitly initialize a session because in JavaScript a session takes the form of the global <code>sessionStorage</code> object and is always present. It’s up to us to write data into the current session.

Session data comes in the form of key-value pairs, and the value of each key may contain only strings. To write data, we can use the <code>sessionStorage.setItem( name, value )</code> method:

<pre><code class="language-javascript">
sessionStorage.setItem( "total", 120 );
</code></pre>

In this case, the key named <code>total</code> now contains the value <code>120</code> as a string, although we’ve used an integer in our call to the <code>.setItem()</code> method. This value will be available until the session expires, unless we use <code>sessionStorage.removeItem( "total" )</code> to remove the named key or we call <code>sessionStorage.clear()</code> to entirely remove all keys and values from the session storage.

<strong>Note</strong> that when a key doesn’t exist in session storage, its value is always <code>null</code>. Then, when we remove a key from session storage and try again to get its value, we’d simply get <code>null</code>.

As you may have guessed, our key now is always available, even as the user navigates the pages of our website. To get its value, we simply write the following:

<pre><code class="language-javascript">
var total = sessionStorage.getItem( "total" );
console.log( total ); // '120', a string
</code></pre>

We can also update its value by using <code>sessionStorage.setItem()</code> again with a new value:

<pre><code class="language-javascript">
var total = parseInt( sessionStorage.getItem( "total" ) );
var quantity = 2;
var updatedTotal = total * quantity;
sessionStorage.setItem( "total", updatedTotal ); // '240', a string
</code></pre>

Now, the key named <code>total</code> has a value of <code>240</code> with our last update. Why did we call <code>parseInt()</code>? This is a simple technique to convert a numerical string into a true number, ensuring that our calculation will be consistent. Remember that all values in session storage are strings, and our calculations must be between only numbers.

<strong>But wait! What about objects?</strong> Objects may be stored in session storage by first turning them into JSON strings (with <code>JSON.stringify()</code>) and then back into JavaScript objects (with <code>JSON.parse()</code>):

<pre><code class="language-javascript">
var cart = {
	item: "Product 1",
	price: 35.50,
	qty: 2
};
var jsonStr = JSON.stringify( cart );
sessionStorage.setItem( "cart", jsonStr );
// now the cart is {"item":"Product 1","price":35.50,"qty":2}
var cartValue = sessionStorage.getItem( "cart" );
var cartObj = JSON.parse( cartValue );
// original object
</code></pre>

To update our object, we simply extend it and then repeat the procedure above.</p>

## Security Considerations

Security is important. If we read the <a href="https://www.w3.org/TR/webstorage/#security-storage">security notes</a> of the W3C’s specification, then we’d be aware of the security risks of even a client-side technology such as Web storage.

The US Computer Emergency Readiness Team’s <a href="https://www.us-cert.gov/sites/default/files/publications/TIP-12-298-01-Website-Security.pdf">technical paper on website security</a> (PDF) clearly states:
<blockquote>"Every community organization, corporation, business, or government agency relies on an outward-facing website to provide information about themselves, announce an event, or sell a product or service. Consequently, public-facing websites are often the most targeted attack vectors for malicious activity."</blockquote>

Even if a browser session ends when the browser itself is closed, malicious attacks can still take place, especially if the browser has been compromised by certain exploits. Moreover, compromised websites can often be used to spread malware that targets particular browsers.

For this reason, <strong>make sure your website is safe</strong> before relying on any technique to store data in the browser. Keeping a website safe is beyond the scope of this article, but by simply following security best practices, you should be able to benefit from Web storage without worrying too much about its security implications.</p>

## Our Sample Project: Winery

Our sample project is an online store that sells wine. It’s a simple e-commerce website whose only complication is in how its shipping charges are calculated.

In short, wines are sold in packages of six bottles. This means that the total quantity of bottles sold must always be in multiples of six. Shipping charges are calculated, then, according to the total quantity of bottles sold.

Our store will rely on PayPal, so we’ll have to create a Business account in PayPal Sandbox to test our code.

The user may add and remove products from their shopping cart, update the cart, change the quantity of each product, and empty the cart. They have to fill a form with their contact information, specifying whether their billing address is the same as their shipping address.

Before being redirected to PayPal, the user will see a summary page with their personal data, their cart, and the cart’s total price plus shipping charges.

After completing their purchase, the user should be redirected back to our website. This is <strong>the only step of the process that we can’t handle only with JavaScript</strong>. PayPal will send back various data over an HTTP request that has to be processed with a server-side language (such as PHP). If you need more information to get started with this kind of processing, please consult <a href="https://developer.paypal.com/docs/classic/ipn/gs_IPN/">PayPal’s tutorial</a>.

## HTML Structure

Our project is made up of the following sections:

*   `index.html` This contains the list from which users may add products to their shopping cart, specifying the quantity for each product.
*   `cart.html` This is the shopping cart page where users may update or empty their cart. Alternatively, they can go back to the main page to continue shopping or proceed to the checkout page.
*   `checkout.html` On this page, users fill out a form with their personal information — specifically, their billing and shipping addresses.
*   `order.html` This page contains a brief summary of the user’s order plus the PayPal form. Once a user submits the form, they will be redirected to PayPal’s landing page.

We’ll go over the markup for this project in the following sections.</p>

### index.html

The main components of this page are the forms that enable the user to add products to their shopping cart.

<pre><code class="language-markup">
&lt;div class="product-description" data-name="Wine #1" data-price="5"&gt;
	&lt;h3 class="product-name"&gt;Wine #1&lt;/h3&gt;
		&lt;p class="product-price"&gt;&amp;euro; 5&lt;/p&gt;
		&lt;form class="add-to-cart" action="cart.html" method="post"&gt;
			&lt;div&gt;
				&lt;label for="qty-1"&gt;Quantity&lt;/label&gt;
				&lt;input type="text" name="qty-1" id="qty-1" class="qty" value="1" /&gt;
			&lt;/div&gt;
			&lt;p&gt;&lt;input type="submit" value="Add to cart" class="btn" /&gt;&lt;/p&gt;
		&lt;/form&gt;
&lt;/div&gt;
</code></pre>

The data attributes used here for storing product names and prices can be accessed via jQuery using the <a href="https://api.jquery.com/data/">.data()</a> and <a href="https://api.jquery.com/jquery.data/">$.data()</a> methods.</p>

### cart.html

Our shopping cart page is made up of three components: a table with the product’s information, an element that displays the subtotal, and a list
of cart actions.

<pre><code class="language-markup">
&lt;form id="shopping-cart" action="cart.html" method="post"&gt;
	&lt;table class="shopping-cart"&gt;
		&lt;thead&gt;
			&lt;tr&gt;
				&lt;th scope="col"&gt;Item&lt;/th&gt;
				&lt;th scope="col"&gt;Qty&lt;/th&gt;
				&lt;th scope="col"&gt;Price&lt;/th&gt;
			&lt;/tr&gt;
		&lt;/thead&gt;
		&lt;tbody&gt;&lt;/tbody&gt;
	&lt;/table&gt;
	&lt;p id="sub-total"&gt;
		&lt;strong&gt;Sub Total&lt;/strong&gt;: &lt;span id="stotal"&gt;&lt;/span&gt;
	&lt;/p&gt;
	&lt;ul id="shopping-cart-actions"&gt;
		&lt;li&gt;
			&lt;input type="submit" name="update" id="update-cart" class="btn" value="Update Cart" /&gt;
		&lt;/li&gt;
		&lt;li&gt;
			&lt;input type="submit" name="delete" id="empty-cart" class="btn" value="Empty Cart" /&gt;
		&lt;/li&gt;
		&lt;li&gt;
			&lt;a href="index.html" class="btn"&gt;Continue Shopping&lt;/a&gt;
		&lt;/li&gt;
		&lt;li&gt;
			&lt;a href="checkout.html" class="btn"&gt;Go To Checkout&lt;/a&gt;
		&lt;/li&gt;
	&lt;/ul&gt;
&lt;/form&gt;
</code></pre>

The table contained in this page is empty, and we’ll fill it with data via JavaScript. The element that displays the subtotal works just as a placeholder for JavaScript. The first two actions, “Update Cart” and “Empty Cart,” will be handled by JavaScript, while the latter two actions are just plain links to the product’s list page and the checkout page, respectively.</p>

### checkout.html

This page has four components:

*   a table that shows the ordered items (the same table shown earlier in the shopping cart section), plus the final price and shipping charges;
*   a form in which the user must fill in their billing details;
*   a form with shipping information;
*   a checkbox to enable the user to specify that their billing details are the same as their shipping details.

<pre><code class="language-markup">
&lt;table id="checkout-cart" class="shopping-cart"&gt;
	&lt;thead&gt;
		&lt;tr&gt;
			&lt;th scope="col"&gt;Item&lt;/th&gt;
			&lt;th scope="col"&gt;Qty&lt;/th&gt;
			&lt;th scope="col"&gt;Price&lt;/th&gt;
		&lt;/tr&gt;
	&lt;/thead&gt;
	&lt;tbody&gt;

	&lt;/tbody&gt;
&lt;/table&gt;

&lt;div id="pricing"&gt;
	&lt;p id="shipping"&gt;
		&lt;strong&gt;Shipping&lt;/strong&gt;: &lt;span id="sshipping"&gt;&lt;/span&gt;
	&lt;/p&gt;

	&lt;p id="sub-total"&gt;
		&lt;strong&gt;Total&lt;/strong&gt;: &lt;span id="stotal"&gt;&lt;/span&gt;
	&lt;/p&gt;
&lt;/div&gt;

&lt;form action="order.html" method="post" id="checkout-order-form"&gt;
	&lt;h2&gt;Your Details&lt;/h2&gt;
		&lt;fieldset id="fieldset-billing"&gt;
			&lt;legend&gt;Billing&lt;/legend&gt;
				&lt;!-- Name, Email, City, Address, ZIP Code, Country (select box) --&gt;

&lt;div&gt;
	&lt;label for="name"&gt;Name&lt;/label&gt;
	&lt;input type="text" name="name" id="name" data-type="string" data-message="This field may not be empty" /&gt;
&lt;/div&gt;

&lt;div&gt;
	&lt;label for="email"&gt;Email&lt;/label&gt;
	&lt;input type="text" name="email" id="email" data-type="expression" data-message="Not a valid email address" /&gt;
&lt;/div&gt;

&lt;div&gt;
	&lt;label for="city"&gt;City&lt;/label&gt;
	&lt;input type="text" name="city" id="city" data-type="string" data-message="This field may not be empty" /&gt;
&lt;/div&gt;

&lt;div&gt;
	&lt;label for="address"&gt;Address&lt;/label&gt;
		&lt;input type="text" name="address" id="address" data-type="string" data-message="This field may not be empty" /&gt;
&lt;/div&gt;

&lt;div&gt;
	&lt;label for="zip"&gt;ZIP Code&lt;/label&gt;
	&lt;input type="text" name="zip" id="zip" data-type="string" data-message="This field may not be empty" /&gt;
&lt;/div&gt;

&lt;div&gt;
	&lt;label for="country"&gt;Country&lt;/label&gt;
		&lt;select name="country" id="country" data-type="string" data-message="This field may not be empty"&gt;
			&lt;option value=""&gt;Select&lt;/option&gt;
			&lt;option value="US"&gt;USA&lt;/option&gt;
			&lt;option value="IT"&gt;Italy&lt;/option&gt;
		&lt;/select&gt;
&lt;/div&gt;
&lt;/fieldset&gt;

&lt;div id="shipping-same"&gt;Same as Billing &lt;input type="checkbox" id="same-as-billing" value=""/&gt;&lt;/div&gt;

&lt;fieldset id="fieldset-shipping"&gt;
&lt;legend&gt;Shipping&lt;/legend&gt;
	&lt;!-- Same fields as billing --&gt;
&lt;/fieldset&gt;

&lt;p&gt;&lt;input type="submit" id="submit-order" value="Submit" class="btn" /&gt;&lt;/p&gt;

&lt;/form&gt;
</code></pre>

Data attributes are used here for validation. The <code>data-type</code> attribute specifies the type of data we’re validating, and <code>data-message</code> contains the error message to be shown in case of failure.

I didn’t use the email validation built into Web browsers just for the sake of simplicity, but you could use it if you want.</p>

### order.html

This final page contains a brief recap of the user’s order, their details and the PayPal form.

<pre><code class="language-markup">
&lt;h1&gt;Your Order&lt;/h1&gt;

&lt;table id="checkout-cart" class="shopping-cart"&gt;
	&lt;thead&gt;
		&lt;tr&gt;
			&lt;th scope="col"&gt;Item&lt;/th&gt;
			&lt;th scope="col"&gt;Qty&lt;/th&gt;
			&lt;th scope="col"&gt;Price&lt;/th&gt;
		&lt;/tr&gt;
	&lt;/thead&gt;
	&lt;tbody&gt;
	&lt;/tbody&gt;
&lt;/table&gt;

&lt;div id="pricing"&gt;
	&lt;p id="shipping"&gt;
		&lt;strong&gt;Shipping&lt;/strong&gt;: &lt;span id="sshipping"&gt;&lt;/span&gt;
	&lt;/p&gt;

	&lt;p id="sub-total"&gt;
		&lt;strong&gt;Total&lt;/strong&gt;: &lt;span id="stotal"&gt;&lt;/span&gt;
	&lt;/p&gt;
&lt;/div&gt;

&lt;div id="user-details"&gt;
	&lt;h2&gt;Your Data&lt;/h2&gt;
		&lt;div id="user-details-content"&gt;&lt;/div&gt;
&lt;/div&gt;

&lt;form id="paypal-form" action="" method="post"&gt;
	&lt;input type="hidden" name="cmd" value="_cart" /&gt;
	&lt;input type="hidden" name="upload" value="1" /&gt;
	&lt;input type="hidden" name="business" value="" /&gt;

	&lt;input type="hidden" name="currency_code" value="" /&gt;
	&lt;input type="submit" id="paypal-btn" class="btn" value="Pay with PayPal" /&gt;
&lt;/form&gt;
</code></pre>

The PayPal form and other elements of this page are initially empty, except for those fields that don’t need to be generated dynamically.</p>

## JavaScript Code

The CSS layout of this project will have no actual influence on the goal we want to achieve. Even if we disabled CSS entirely, the project would continue to function, thanks to the strong relationship between the HTML’s structure and the JavaScript’s behavior.

We’ll use an <strong>object-oriented approach</strong> because of the complexity of our goals. Our object will be based on a simple constructional pattern and will use both private and public methods.</p>

### Object Structure

Our object has a very simple structure. The constructor function both initializes the top-level element that wraps our DOM’s entire structure and invokes the initialization method.

<pre><code class="language-javascript">
(function( $ ) {
	$.Shop = function( element ) {
		this.$element = $( element ); // top-level element
		this.init();
	};

	$.Shop.prototype = {
		init: function() {
			// initializes properties and methods
		}
	};

	$(function() {
		var shop = new $.Shop( "#site" ); // object's instance
	});

})( jQuery );
</code></pre>

The object’s instance is created when the DOM is ready. We can test that everything has worked fine as follows:

<pre><code class="language-javascript">
$(function() {
	var shop = new $.Shop( "#site" );
	console.log( shop.$element );
});
</code></pre>

This outputs the following:

<pre><code class="language-javascript">
x.fn.x.init[1]
	0: div#site
	context: document
	length: 1
	selector: "#site"
</code></pre>

Now that we know our object has been instantiated correctly, we can define its properties.</p>

### Object Properties

The properties of our object break down into two categories: first, the properties for handling calculations, forms and validation, and secondly, the references to HTML elements.

<pre><code class="language-javascript">
$.Shop.prototype = {
	init: function() {
		// Properties

			this.cartPrefix = "winery-"; // prefix string to be prepended to the cart's name in session storage
			this.cartName = this.cartPrefix + "cart"; // cart's name in session storage
			this.shippingRates = this.cartPrefix + "shipping-rates"; // shipping rates key in session storage
			this.total = this.cartPrefix + "total"; // total key in the session storage
			this.storage = sessionStorage; // shortcut to sessionStorage object

			this.$formAddToCart = this.$element.find( "form.add-to-cart" ); // forms for adding items to the cart
			this.$formCart = this.$element.find( "#shopping-cart" ); // Shopping cart form
			this.$checkoutCart = this.$element.find( "#checkout-cart" ); // checkout form cart
			this.$checkoutOrderForm = this.$element.find( "#checkout-order-form" ); // checkout user details form
			this.$shipping = this.$element.find( "#sshipping" ); // element that displays the shipping rates
			this.$subTotal = this.$element.find( "#stotal" ); // element that displays the subtotal charges
			this.$shoppingCartActions = this.$element.find( "#shopping-cart-actions" ); // cart actions links
			this.$updateCartBtn = this.$shoppingCartActions.find( "#update-cart" ); // update cart button
			this.$emptyCartBtn = this.$shoppingCartActions.find( "#empty-cart" ); // empty cart button
			this.$userDetails = this.$element.find( "#user-details-content" ); // element that displays the user's information
			this.$paypalForm = this.$element.find( "#paypal-form" ); // PayPal form

			this.currency = "&amp;euro;"; // HTML entity of the currency to be displayed in layout
			this.currencyString = "€"; // currency symbol as text string
			this.paypalCurrency = "EUR"; // PayPal's currency code
			this.paypalBusinessEmail = "yourbusiness@email.com"; // your PayPal Business account email address
			this.paypalURL = "https://www.sandbox.paypal.com/cgi-bin/webscr"; // URL of the PayPal form

			// object containing patterns for form validation
			this.requiredFields = {
				expression: {
					value: /^([w-.]+)@((?:[w]+.)+)([a-z]){2,4}$/
				},

				str: {
					value: ""
				}

			};

			// public methods invocation
	}
};
</code></pre>

Let’s go over these properties one by one.

<strong>Storage and other properties:</strong>

*   `cartPrefix` A prefix to be prepended to the cart’s name key in session storage
*   `cartName` The cart’s name key in session storage (combines the `cartPrefix` string with the `cart` string)
*   `shippingRates` The shipping rate key in session storage
*   `total` The total’s key in session storage
*   `storage` Shortcut to the `sessionStorage` object.
*   `currency` An HTML entity used to display the current currency in the layout
*   `currencyString` The current currency symbol used in the element’s text
*   `paypalCurrency` PayPal’s currency text code
*   `paypalBusinessEmail` The email address of your PayPal Business account
*   `paypalURL` The URL of PayPal’s form (defaults to the URL of PayPal Sandbox)
*   `requiredFields` An object containing the patterns and rules for form validation

<strong>References to elements:</strong>

*   `$formAddToCart` The forms for adding products to the shopping cart
*   `$formCart` The shopping cart form
*   `$checkoutCart` The checkout’s shopping cart form
*   `$checkoutOrderForm` The checkout’s form where users input their personal information
*   `$shipping` The element that contains and displays shipping rates
*   `$subTotal` The element that contains and displays the total charges
*   `$shoppingCartActions` The elements that contain the actions related to the shopping cart
*   `$updateCartBtn` The button to update the shopping cart
*   `$emptyCartBtn` The button for emptying the cart
*   `$userDetails` The element that contains and displays the information entered by the user
*   `$paypalForm` PayPal’s form

All of the elements are prefixed with the <code>$</code> sign, meaning that they’re jQuery objects. But <strong>not all of these elements are available on all pages</strong>. To check whether a jQuery element exists, simply test its <code>length</code> property:

<pre><code class="language-javascript">
if( $element.length ) {
	// the element exists
}
</code></pre>

Another approach, not used in our project, is to add a particular ID or class to the <code>body</code> element and perform actions conditionally:

<pre><code class="language-javascript">
var $body = $( "body" ),
	page = $body.attr( "id" );

	switch( page ) {
		case "product-list":
			// actions for handling products
			break;
		case "shopping-cart":
			// actions for handling the shopping cart
			break;
		case "checkout":
			// actions for handling the checkout's page
			break;
		default:
			break;
	}
</code></pre>

### Object Methods

The actions of our code take place in our object’s methods, which, in turn, can be divided into public and private methods. Private methods operate in the background, so to speak, and help the public methods perform their tasks. These methods are prefixed with an underscore and are never used directly.

Public methods, meanwhile, operate directly on page elements and data, and they’re unprefixed. We’ve already seen the <code>init()</code> method, which simply initializes properties and other public methods in the object’s constructor function. The other methods will be explained below.</p>

### Private Methods (Helpers)

The first private method, <code>_emptyCart()</code>, simply empties the current session storage in the browser:

<pre><code class="language-javascript">
$.Shop.prototype = {
	// empties session storage

	_emptyCart: function() {
		this.storage.clear();
	}
};
</code></pre>

To format a number by a set number of decimal places, we implement the <code>_formatNumber()</code> method:

<pre><code class="language-javascript">
/* Format a number by decimal places
 * @param num Number the number to be formatted
 * @param places Number the decimal places
 * @returns n Number the formatted number
*/

_formatNumber: function( num, places ) {
	var n = num.toFixed( places );
	return n;
}
</code></pre>

This method makes use of JavaScript’s <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed">toFixed()</a> method of the <code>Number</code> object. Its role in our project is to properly format prices.

Because <strong>not all of the prices in our pages are contained in data attributes</strong>, we need a specialized method to extract the numeric portion of a string from text nodes. This method is named <code>_extractPrice()</code>:

<pre><code class="language-javascript">
/* Extract the numeric portion from a string
 * @param element Object the jQuery element that contains the relevant string
 * @returns price String the numeric string
 */

_extractPrice: function( element ) {
	var self = this;
	var text = element.text();
	var price = text.replace( self.currencyString, "" ).replace( " ", "" );
	return price;
}
</code></pre>

Above, <code>self</code> is a reference to the <code>$.Shop</code> object, and we’ll need it every time we want to access a property or a method of our object without worrying much about scope.

You can bulletproof this method by adding a further routine that strips out all trailing white space:

<pre><code class="language-javascript">
var text = $.trim( element.text() );
</code></pre>

Bear in mind that jQuery’s <a href="https://api.jquery.com/jQuery.trim/">$.trim()</a> method removes all new lines, spaces (including non-breaking spaces) and tabs from the beginning and end of a string. If these white space characters occur in the middle of a string, they are preserved.

Then, <strong>we need two methods to convert strings into numbers and numbers into strings</strong>. This is necessary to perform calculations and to display the results on our pages.

<pre><code class="language-javascript">
/* Converts a numeric string into a number
 * @param numStr String the numeric string to be converted
 * @returns num Number the number, or false if the string cannot be converted
 */

_convertString: function( numStr ) {
	var num;
	if( /^[-+]?[0-9]+.[0-9]+$/.test( numStr ) ) {
		num = parseFloat( numStr );
	} else if( /^d+$/.test( numStr ) ) {
		num = parseInt( numStr );
	} else {
		num = Number( numStr );
	}

	if( !isNaN( num ) ) {
		return num;
	} else {
		console.warn( numStr + " cannot be converted into a number" );
		return false;
	}
},

/* Converts a number to a string
 * @param n Number the number to be converted
 * @returns str String the string returned
 */

_convertNumber: function( n ) {
	var str = n.toString();
	return str;
}
</code></pre>

Above, <code>_convertString()</code> runs the following tests:

1.  Does the string have a decimal format? If so, it uses the [parseFloat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat) function.
2.  Does the string have an integer format? If so, it uses the [parseInt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt) function.
3.  If the format of the string cannot be detected, it uses the [Number()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) constructor.
4.  If the result is a number (tested with the [isNaN()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN) function), it returns the number. Otherwise, it outputs a warning to the JavaScript console and returns `false`.

By contrast, <code>_convertNumber()</code> simply invokes the <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toString">toString()</a> method to convert a number into a string.

The next step is to define two methods to <strong>convert a JavaScript object into a JSON string</strong> and a JSON string back into a JavaScript object:

<pre><code class="language-javascript">
/* Converts a JSON string to a JavaScript object
 * @param str String the JSON string
 * @returns obj Object the JavaScript object
 */

_toJSONObject: function( str ) {
	var obj = JSON.parse( str );
	return obj;
},

/* Converts a JavaScript object to a JSON string
 * @param obj Object the JavaScript object
 * @returns str String the JSON string
 */

_toJSONString: function( obj ) {
	var str = JSON.stringify( obj );
	return str;
}
</code></pre>

The first method makes use of the <code>JSON.parse()</code> method, while the latter invokes the <code>JSON.stringify()</code> method (see Mozilla Developer Network’s article on “<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_native_JSON">Using Native JSON</a>”).

Why do we need these methods? Because our cart will also store the information related to each product using the following data format (spaces added for legibility):
<table class="table-overview"><br>
<tbody>
<tr>
<td><strong>Key</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td><code>winery-cart</code></td>
<td><code>{ "items": [ { "product": "Wine #1", "qty": 5, "price": 5 } ] }</code></td>
</tr>
</tbody>
</table>

The <code>winery-cart</code> key contains a JSON string that represents an array of objects (i.e. <code>items</code>) in which each object shows the relevant information about a product added by the user — namely, the product’s name, the quantity and the price.

It’s pretty obvious that we also now need a specialized method to add items to this particular key in session storage:

<pre><code class="language-javascript">
/* Add an object to the cart as a JSON string
 * @param values Object the object to be added to the cart
 * @returns void
 */

_addToCart: function( values ) {
	var cart = this.storage.getItem( this.cartName );
	var cartObject = this._toJSONObject( cart );
	var cartCopy = cartObject;
	var items = cartCopy.items;
	items.push( values );

	this.storage.setItem( this.cartName, this._toJSONString( cartCopy ) );
}
</code></pre>

This method gets the cart’s key from session storage, converts it to a JavaScript object and adds a new object as a JSON string to the cart’s array. The newly added object has the following format:

<pre><code class="language-javascript">
this._addToCart({
	product: "Test",
	qty: 1,
	price: 2
});
</code></pre>

Now, our cart key will look like this:
<table class="table-overview">
<tbody>
<tr>
<td><strong>Key</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td><code>winery-cart</code></td>
<td><code>{ "items": [ { "product": "Wine #1", "qty": 5, "price": 5 }, { "product": "Test", "qty": 1, "price": 2 } ] }</code></td>
</tr>
</tbody>
</table>

Shipping is calculated according to the overall number of products added to the cart, not the quantity of each individual product:

<pre><code class="language-javascript">
/* Custom shipping rates calculated based on total quantity of items in cart
 * @param qty Number the total quantity of items
 * @returns shipping Number the shipping rates
 */

_calculateShipping: function( qty ) {
	var shipping = 0;
	if( qty &gt;= 6 ) {
		shipping = 10;
	}
	if( qty &gt;= 12 &amp;&amp; qty &lt;= 30 ) {
		shipping = 20;
	}

	if( qty &gt;= 30 &amp;&amp; qty &lt;= 60 ) {
		shipping = 30;
	}

	if( qty &gt; 60 ) {
		shipping = 0;
	}

	return shipping;

}
</code></pre>

You can replace this method’s routines with your own. In this case, shipping charges are calculated based on specific amounts.

<strong>We also need to validate the checkout form</strong> where users insert their personal information. The following method takes into account the special visibility toggle by which the user may specify that their billing information is the same as their shipping information.

<pre><code class="language-javascript">
/* Validates the checkout form
 * @param form Object the jQuery element of the checkout form
 * @returns valid Boolean true for success, false for failure
 */

_validateForm: function( form ) {
		var self = this;
		var fields = self.requiredFields;
		var $visibleSet = form.find( "fieldset:visible" );
		var valid = true;

		form.find( ".message" ).remove();

	$visibleSet.each(function() {

		$( this ).find( ":input" ).each(function() {
		var $input = $( this );
		var type = $input.data( "type" );
		var msg = $input.data( "message" );

		if( type == "string" ) {
			if( $input.val() == fields.str.value ) {
				$( "&lt;span class='message'/&gt;" ).text( msg ).
				insertBefore( $input );

				valid = false;
			}
		} else {
			if( !fields.expression.value.test( $input.val() ) ) {
				$( "&lt;span class='message'/&gt;" ).text( msg ).
				insertBefore( $input );

				valid = false;
			}
		}

	});
	});

	return valid;
}
</code></pre>

When validation messages are added upon the form being submitted, we need to clear these messages before going any further. In this case, we take into account only the fields contained in a <code>fieldset</code> element that is still visible after the user has checked the visibility toggle.

Validation takes place by checking whether the current field requires a simple string comparison (<code>data-type="string"</code>) or a regular expression test (<code>data-type="expression"</code>). Our tests are based on the <code>requiredFields</code> property. If there’s an error, we’ll show a message by using the <code>data-message</code> attribute of each field.

Note that the validation routines used above have been inserted just for demonstration purposes, and they have several flaws. For better validation, I recommend a dedicated jQuery plugin, such as <a href="https://bassistance.de/jquery-plugins/jquery-plugin-validation/">jQuery Validation</a>.

Last but not least is <strong>registering the information that the user has entered</strong> in the checkout form:

<pre><code class="language-javascript">
/* Save the data entered by the user in the checkout form
 * @param form Object the jQuery element of the checkout form
 * @returns void
 */

_saveFormData: function( form ) {
	var self = this;
	var $visibleSet = form.find( "fieldset:visible" );

	$visibleSet.each(function() {
		var $set = $( this );
		if( $set.is( "#fieldset-billing" ) ) {
			var name = $( "#name", $set ).val();
			var email = $( "#email", $set ).val();
			var city = $( "#city", $set ).val();
			var address = $( "#address", $set ).val();
			var zip = $( "#zip", $set ).val();
			var country = $( "#country", $set ).val();

			self.storage.setItem( "billing-name", name );
			self.storage.setItem( "billing-email", email );
			self.storage.setItem( "billing-city", city );
			self.storage.setItem( "billing-address", address );
			self.storage.setItem( "billing-zip", zip );
			self.storage.setItem( "billing-country", country );
		} else {
			var sName = $( "#sname", $set ).val();
			var sEmail = $( "#semail", $set ).val();
			var sCity = $( "#scity", $set ).val();
			var sAddress = $( "#saddress", $set ).val();
			var sZip = $( "#szip", $set ).val();
			var sCountry = $( "#scountry", $set ).val();

			self.storage.setItem( "shipping-name", sName );
			self.storage.setItem( "shipping-email", sEmail );
			self.storage.setItem( "shipping-city", sCity );
			self.storage.setItem( "shipping-address", sAddress );
			self.storage.setItem( "shipping-zip", sZip );
			self.storage.setItem( "shipping-country", sCountry );

		}
	});
}
</code></pre>

Again, this method takes into account the visibility of the fields based on the user’s choice. Once the form has been submitted, our session storage may have the following details added to it:
<table class="table-overview"><br>
<tbody>
<tr>
<td><strong>Key</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td><code>billing-name</code></td>
<td>John Doe</td>
</tr>
<tr>
<td><code>billing-email</code></td>
<td>jdoe@localhost</td>
</tr>
<tr>
<td><code>billing-city</code></td>
<td>New York</td>
</tr>
<tr>
<td><code>billing-address</code></td>
<td>Street 1</td>
</tr>
<tr>
<td><code>billing-zip</code></td>
<td>1234</td>
</tr>
<tr>
<td><code>billing-country</code></td>
<td>USA</td>
</tr>
</tbody>
</table>

### Public Methods

Our public methods are invoked in the initialization method (<code>init()</code>). The first thing to do is create the initial keys and values in session storage.

<pre><code class="language-javascript">
// Creates the cart keys in session storage

createCart: function() {
	if( this.storage.getItem( this.cartName ) == null ) {

		var cart = {};
		cart.items = [];

		this.storage.setItem( this.cartName, this._toJSONString( cart ) );
		this.storage.setItem( this.shippingRates, "0" );
		this.storage.setItem( this.total, "0" );
	}
}
</code></pre>

The first check tests whether our values have already been added to session storage. We need this test because we could actually overwrite our values if we run this method every time a document has finished loading.

Now, our session storage looks like this:
<table class="table-overview"><br>
<tbody>
<tr>
<td><strong>Key</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td><code>winery-cart</code></td>
<td>{"items":[]}</td>
</tr>
<tr>
<td><code>winery-shipping-rates</code></td>
<td>0</td>
</tr>
<tr>
<td><code>winery-total</code></td>
<td>0</td>
</tr>
</tbody>
</table>

Now, we need to <strong>handle the forms where the user may add products</strong> to their shopping cart:

<pre><code class="language-javascript">
// Adds items to shopping cart

handleAddToCartForm: function() {
	var self = this;
	self.$formAddToCart.each(function() {
		var $form = $( this );
		var $product = $form.parent();
		var price = self._convertString( $product.data( "price" ) );
		var name =  $product.data( "name" );

		$form.on( "submit", function() {
			var qty = self._convertString( $form.find( ".qty" ).val() );
			var subTotal = qty * price;
			var total = self._convertString( self.storage.getItem( self.total ) );
			var sTotal = total + subTotal;
			self.storage.setItem( self.total, sTotal );
			self._addToCart({
				product: name,
				price: price,
				qty: qty
			});
			var shipping = self._convertString( self.storage.getItem( self.shippingRates ) );
			var shippingRates = self._calculateShipping( qty );
			var totalShipping = shipping + shippingRates;

			self.storage.setItem( self.shippingRates, totalShipping );
		});
	});
}
</code></pre>

Every time a user submits one of these forms, we have to read the product quantity specified by the user and multiply it by the unit price. Then, we need to read the total’s key contained in session storage and update its value accordingly. Having done this, we call the <code>_addToCart()</code> method to store the product’s details in storage. The quantity specified will also be used to <strong>calculate the shipping rate</strong> by comparing its value to the value already stored.

Suppose that a user chooses the first product, Wine #1, whose price is €5.00, and specifies a quantity of 5. The session storage would look like this once the form has been submitted:
<table class="table-overview"><br>
<tbody>
<tr>
<td><strong>Key</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td><code>winery-cart</code></td>
<td>{"items":[{"product":"Wine #1","price":5,"qty":5}]}</td>
</tr>
<tr>
<td><code>winery-shipping-rates</code></td>
<td>0</td>
</tr>
<tr>
<td><code>winery-total</code></td>
<td>25</td>
</tr>
</tbody>
</table>

Suppose the same user goes back to the product list and chooses Wine #2, whose price is €8.00, and specifies a quantity of 2:
<table class="table-overview"><br>
<tbody>
<tr>
<td><strong>Key</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td><code>winery-cart</code></td>
<td>{"items":[{"product":"Wine #1","price":5,"qty":5},{"product":"Wine #2","price":8,"qty":2}]}</td>
</tr>
<tr>
<td><code>winery-shipping-rates</code></td>
<td>0</td>
</tr>
<tr>
<td><code>winery-total</code></td>
<td>41</td>
</tr>
</tbody>
</table>

Finally, our eager user returns again to the product list, chooses Wine #3, whose price is €11.00, and specifies a quantity of 6:
<table class="table-overview"><br>
<tbody>
<tr>
<td><strong>Key</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td><code>winery-cart</code></td>
<td>{"items":[{"product":"Wine #1","price":5,"qty":5},{"product":"Wine #2","price":8,"qty":2},{"product":"Wine #3","price":11,"qty":6}]}</td>
</tr>
<tr>
<td><code>winery-shipping-rates</code></td>
<td>10</td>
</tr>
<tr>
<td><code>winery-total</code></td>
<td>107</td>
</tr>
</tbody>
</table>

At this point, we need to <strong>accurately display the cart</strong> when the user goes to the shopping cart page or checkout page:

<pre><code class="language-javascript">
// Displays the shopping cart

displayCart: function() {
	if( this.$formCart.length ) {
		var cart = this._toJSONObject( this.storage.getItem( this.cartName ) );
		var items = cart.items;
		var $tableCart = this.$formCart.find( ".shopping-cart" );
		var $tableCartBody = $tableCart.find( "tbody" );

		for( var i = 0; i &lt; items.length; ++i ) {
			var item = items[i];
			var product = item.product;
			var price = this.currency + " " + item.price;
			var qty = item.qty;
			var html = "&lt;tr&gt;&lt;td class='pname'&gt;" + product + "&lt;/td&gt;" + "&lt;td class='pqty'&gt;&lt;input type='text' value='" + qty + "' class='qty'/&gt;&lt;/td&gt;" + "&lt;td class='pprice'&gt;" + price + "&lt;/td&gt;&lt;/tr&gt;";

			$tableCartBody.html( $tableCartBody.html() + html );
		}

		var total = this.storage.getItem( this.total );
		this.$subTotal[0].innerHTML = this.currency + " " + total;
	} else if( this.$checkoutCart.length ) {
		var checkoutCart = this._toJSONObject( this.storage.getItem( this.cartName ) );
		var cartItems = checkoutCart.items;
		var $cartBody = this.$checkoutCart.find( "tbody" );

		for( var j = 0; j &lt; cartItems.length; ++j ) {
			var cartItem = cartItems[j];
			var cartProduct = cartItem.product;
			var cartPrice = this.currency + " " + cartItem.price;
			var cartQty = cartItem.qty;
			var cartHTML = "&lt;tr&gt;&lt;td class='pname'&gt;" + cartProduct + "&lt;/td&gt;" + "&lt;td class='pqty'&gt;" + cartQty + "&lt;/td&gt;" + "&lt;td class='pprice'&gt;" + cartPrice + "&lt;/td&gt;&lt;/tr&gt;";

			$cartBody.html( $cartBody.html() + cartHTML );
		}

		var cartTotal = this.storage.getItem( this.total );
		var cartShipping = this.storage.getItem( this.shippingRates );
		var subTot = this._convertString( cartTotal ) + this._convertString( cartShipping );

		this.$subTotal[0].innerHTML = this.currency + " " + this._convertNumber( subTot );
		this.$shipping[0].innerHTML = this.currency + " " + cartShipping;

	}
}
</code></pre>

If the cart’s table is on the shopping cart page, then this method iterates over the array of objects contained in the <code>winery-cart</code> key and populates the table by adding a text field to allow users to modify the quantity of each product. For the sake of simplicity, I didn’t include an action to remove an item from the cart, but that procedure is pretty simple:

1.  Get the `items` array, contained in session storage.
2.  Get the product’s name, contained in the `td` element with the `pname` class.
3.  Create a new array by filtering out the item with the product’s name, obtained in step 2 (you can use [$.grep()](https://api.jquery.com/jQuery.grep/)).
4.  Save the new array in the `winery-cart` key.
5.  Update the total and shipping charge values.

<pre><code class="language-javascript">
var items = [
	{
		product: "Test",
		qty: 1,
		price: 5
	},
	{
		product: "Foo",
		qty: 5,
		price: 10
	},
	{
		product: "Bar",
		qty: 2,
		price: 8
	}
];

items = $.grep( items, function( item ) {
	return item.product !== "Test";

});

console.log( items );

/*
	Array[2]
		0: Object
			price: 10
			product: "Foo"
			qty: 5
		1: Object
			price: 8
			product: "Bar"
			qty: 2
*/
</code></pre>

Then, we need a method that updates the cart with a new quantity value for each product:

<pre><code class="language-javascript">
// Updates the cart

updateCart: function() {
		var self = this;
	if( self.$updateCartBtn.length ) {
		self.$updateCartBtn.on( "click", function() {
			var $rows = self.$formCart.find( "tbody tr" );
			var cart = self.storage.getItem( self.cartName );
			var shippingRates = self.storage.getItem( self.shippingRates );
			var total = self.storage.getItem( self.total );

			var updatedTotal = 0;
			var totalQty = 0;
			var updatedCart = {};
			updatedCart.items = [];

			$rows.each(function() {
				var $row = $( this );
				var pname = $.trim( $row.find( ".pname" ).text() );
				var pqty = self._convertString( $row.find( ".pqty &gt; .qty" ).val() );
				var pprice = self._convertString( self._extractPrice( $row.find( ".pprice" ) ) );

				var cartObj = {
					product: pname,
					price: pprice,
					qty: pqty
				};

				updatedCart.items.push( cartObj );

				var subTotal = pqty * pprice;
				updatedTotal += subTotal;
				totalQty += pqty;
			});

			self.storage.setItem( self.total, self._convertNumber( updatedTotal ) );
			self.storage.setItem( self.shippingRates, self._convertNumber( self._calculateShipping( totalQty ) ) );
			self.storage.setItem( self.cartName, self._toJSONString( updatedCart ) );

		});
	}
}
</code></pre>

Our method loops through all of the relevant table cells of the cart and builds a new object to be inserted in the <code>winery-cart</code> key. It also recalculates the total price and shipping charge by taking into account the newly inserted values of the quantity fields.

Suppose that a user changes the quantity of Wine #2 from 2 to 6:
<table class="table-overview"><br>
<tbody>
<tr>
<td><strong>Key</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td><code>winery-cart</code></td>
<td>{"items":[{"product":"Wine #1","price":5,"qty":5},{"product":"Wine #2","price":8,"qty":6},{"product":"Wine #3","price":11,"qty":6}]}</td>
</tr>
<tr>
<td><code>winery-shipping-rates</code></td>
<td>20</td>
</tr>
<tr>
<td><code>winery-total</code></td>
<td>139</td>
</tr>
</tbody>
</table>

If the user wants to empty their cart and start over, we simply have to add the following action:

<pre><code class="language-javascript">
// Empties the cart by calling the _emptyCart() method
// @see $.Shop._emptyCart()

emptyCart: function() {
	var self = this;
	if( self.$emptyCartBtn.length ) {
		self.$emptyCartBtn.on( "click", function() {
			self._emptyCart();
		});
	}
}
</code></pre>

Now, session storage has been emptied entirely, and <strong>the user may start making purchases again</strong>. However, if they decide to finalize their order instead, then we need to handle the checkout form when they insert their personal information.

<pre><code class="language-javascript">
// Handles the checkout form by adding a validation routine and saving user’s info in session storage

handleCheckoutOrderForm: function() {
	var self = this;
	if( self.$checkoutOrderForm.length ) {
		var $sameAsBilling = $( "#same-as-billing" );
		$sameAsBilling.on( "change", function() {
			var $check = $( this );
			if( $check.prop( "checked" ) ) {
				$( "#fieldset-shipping" ).slideUp( "normal" );
			} else {
				$( "#fieldset-shipping" ).slideDown( "normal" );
			}
		});

		self.$checkoutOrderForm.on( "submit", function() {
			var $form = $( this );
			var valid = self._validateForm( $form );

			if( !valid ) {
				return valid;
			} else {
				self._saveFormData( $form );
			}
		});
	}
}
</code></pre>

The first thing we need to do is <strong>hide the shipping fields</strong> if the user checks the toggle that specifies that their billing information is the same as their shipping information. We use the <code>change</code> event, combined with jQuery’s <a href="https://api.jquery.com/prop/">.prop()</a> method. (If you’re curious about the difference between <code>.prop()</code> and <code>.attr()</code>, <a href="https://stackoverflow.com/questions/5874652/prop-vs-attr">StackOverflow has a good discussion</a> of it.)

Then, we validate the form by returning a <code>false</code> value in case of errors, thus preventing the form from being submitted. If validation succeeds, we save the user’s data in storage. For example:
<table class="table-overview"><br>
<tbody>
<tr>
<td><strong>Key</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td><code>winery-cart</code></td>
<td>{"items":[{"product":"Wine #1","price":5,"qty":5},{"product":"Wine #2","price":8,"qty":6},{"product":"Wine #3","price":11,"qty":6}]}</td>
</tr>
<tr>
<td><code>winery-shipping-rates</code></td>
<td>20</td>
</tr>
<tr>
<td><code>winery-total</code></td>
<td>139</td>
</tr>
<tr>
<td><code>billing-name</code></td>
<td>John Doe</td>
</tr>
<tr>
<td><code>billing-email</code></td>
<td>jdoe@localhost</td>
</tr>
<tr>
<td><code>billing-city</code></td>
<td>New York</td>
</tr>
<tr>
<td><code>billing-address</code></td>
<td>Street 1</td>
</tr>
<tr>
<td><code>billing-zip</code></td>
<td>1234</td>
</tr>
<tr>
<td><code>billing-country</code></td>
<td>USA</td>
</tr>
</tbody>
</table>
<strong>The final step is the page with the PayPal form.</strong> First, we need to display the user’s information gathered on the checkout page:

<pre><code class="language-javascript">
// Displays the user's information

displayUserDetails: function() {
	if( this.$userDetails.length ) {
		if( this.storage.getItem( "shipping-name" ) == null ) {
			var name = this.storage.getItem( "billing-name" );
			var email = this.storage.getItem( "billing-email" );
			var city = this.storage.getItem( "billing-city" );
			var address = this.storage.getItem( "billing-address" );
			var zip = this.storage.getItem( "billing-zip" );
			var country = this.storage.getItem( "billing-country" );

			var html = "&lt;div class='detail'&gt;";
				html += "&lt;h2&gt;Billing and Shipping&lt;/h2&gt;";
				html += "&lt;ul&gt;";
				html += "&lt;li&gt;" + name + "&lt;/li&gt;";
				html += "&lt;li&gt;" + email + "&lt;/li&gt;";
				html += "&lt;li&gt;" + city + "&lt;/li&gt;";
				html += "&lt;li&gt;" + address + "&lt;/li&gt;";
				html += "&lt;li&gt;" + zip + "&lt;/li&gt;";
				html += "&lt;li&gt;" + country + "&lt;/li&gt;";
				html += "&lt;/ul&gt;&lt;/div&gt;";

			this.$userDetails[0].innerHTML = html;
		} else {
			var name = this.storage.getItem( "billing-name" );
			var email = this.storage.getItem( "billing-email" );
			var city = this.storage.getItem( "billing-city" );
			var address = this.storage.getItem( "billing-address" );
			var zip = this.storage.getItem( "billing-zip" );
			var country = this.storage.getItem( "billing-country" );

			var sName = this.storage.getItem( "shipping-name" );
			var sEmail = this.storage.getItem( "shipping-email" );
			var sCity = this.storage.getItem( "shipping-city" );
			var sAddress = this.storage.getItem( "shipping-address" );
			var sZip = this.storage.getItem( "shipping-zip" );
			var sCountry = this.storage.getItem( "shipping-country" );

			var html = "&lt;div class='detail'&gt;";
				html += "&lt;h2&gt;Billing&lt;/h2&gt;";
				html += "&lt;ul&gt;";
				html += "&lt;li&gt;" + name + "&lt;/li&gt;";
				html += "&lt;li&gt;" + email + "&lt;/li&gt;";
				html += "&lt;li&gt;" + city + "&lt;/li&gt;";
				html += "&lt;li&gt;" + address + "&lt;/li&gt;";
				html += "&lt;li&gt;" + zip + "&lt;/li&gt;";
				html += "&lt;li&gt;" + country + "&lt;/li&gt;";
				html += "&lt;/ul&gt;&lt;/div&gt;";

				html += "&lt;div class='detail right'&gt;";
				html += "&lt;h2&gt;Shipping&lt;/h2&gt;";
				html += "&lt;ul&gt;";
				html += "&lt;li&gt;" + sName + "&lt;/li&gt;";
				html += "&lt;li&gt;" + sEmail + "&lt;/li&gt;";
				html += "&lt;li&gt;" + sCity + "&lt;/li&gt;";
				html += "&lt;li&gt;" + sAddress + "&lt;/li&gt;";
				html += "&lt;li&gt;" + sZip + "&lt;/li&gt;";
				html += "&lt;li&gt;" + sCountry + "&lt;/li&gt;";
				html += "&lt;/ul&gt;&lt;/div&gt;";

			this.$userDetails[0].innerHTML = html;

		}
	}
}
</code></pre>

Our method first <strong>checks whether the user has inputted either billing or shipping information or both</strong>. Then, it simply builds an HTML fragment by getting the user’s data from session storage.

Finally, the user may buy the products by submitting the PayPal form. The form redirects them to PayPal, but the fields need to be filled in properly before the form can be submitted.

<pre><code class="language-javascript">
// Appends the required hidden values to PayPal's form before submitting

populatePayPalForm: function() {
	var self = this;
	if( self.$paypalForm.length ) {
		var $form = self.$paypalForm;
		var cart = self._toJSONObject( self.storage.getItem( self.cartName ) );
		var shipping = self.storage.getItem( self.shippingRates );
		var numShipping = self._convertString( shipping );
		var cartItems = cart.items;
		var singShipping = Math.floor( numShipping / cartItems.length );

		$form.attr( "action", self.paypalURL );
		$form.find( "input[name='business']" ).val( self.paypalBusinessEmail );
		$form.find( "input[name='currency_code']" ).val( self.paypalCurrency );

		for( var i = 0; i &lt; cartItems.length; ++i ) {
			var cartItem = cartItems[i];
			var n = i + 1;
			var name = cartItem.product;
			var price = cartItem.price;
			var qty = cartItem.qty;

			$( "&lt;div/&gt;" ).html( "&lt;input type='hidden' name='quantity_" + n + "' value='" + qty + "'/&gt;" ).
			insertBefore( "#paypal-btn" );
			$( "&lt;div/&gt;" ).html( "&lt;input type='hidden' name='item_name_" + n + "' value='" + name + "'/&gt;" ).
			insertBefore( "#paypal-btn" );
			$( "&lt;div/&gt;" ).html( "&lt;input type='hidden' name='item_number_" + n + "' value='SKU " + name + "'/&gt;" ).
			insertBefore( "#paypal-btn" );
			$( "&lt;div/&gt;" ).html( "&lt;input type='hidden' name='amount_" + n + "' value='" + self._formatNumber( price, 2 ) + "'/&gt;" ).
			insertBefore( "#paypal-btn" );
			$( "&lt;div/&gt;" ).html( "&lt;input type='hidden' name='shipping_" + n + "' value='" + self._formatNumber( singShipping, 2 ) + "'/&gt;" ).
			insertBefore( "#paypal-btn" );

		}

	}
}
</code></pre>

First, we get some important information from session storage — namely, the shipping rate and the total number of items in the cart. We divide the total shipping amount by the number of items to get the shipping rate for each item.

Then, we set the URL for the <code>action</code> attribute of the form, together with our business email and currency code (taken from the <code>paypalBusinessEmail</code> and <code>paypalCurrency</code> properties, respectively).

Finally, we loop through the items of our cart, and we append to the form several hidden input elements containing the quantities, the names of the products, the number of items for each product, the prices (amounts), and the unit shipping rates.

The monetary values are formatted as <code>00,00</code>. Explaining all of the possible values of a PayPal form and the various types of PayPal forms goes well beyond the scope of this article, If you want to go deeper, I recommend the following reading:

*   “[HTML Form Basics for PayPal Payments Standard](https://developer.paypal.com/docs/classic/paypal-payments-standard/integration-guide/formbasics/),” PayPal Developer
*   “[HTML Variables for PayPal Payments Standard](https://developer.paypal.com/docs/classic/paypal-payments-standard/integration-guide/Appx_websitestandard_htmlvariables/),” PayPal Developer

## Preview And Source Code

The following video shows the result. I’ve omitted PayPal’s landing page to protect my account’s data.

Get the code from the <a href="https://github.com/gabrieleromanato/jQuery-sessionStorage-shopping-cart">GitHub repository</a>. Just change the <code>paypalBusinessEmail</code> property of the <code>$.Shop</code> object to your PayPal Sandbox email account.</p>

### Other Resources

*   “[DOM Storage Guide](https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Storage),” Mozilla Developer Network
*   “[Introduction to Session Storage](https://www.nczonline.net/blog/2009/07/21/introduction-to-sessionstorage/),” Nicholas C. Zakas
*   “[Using data-* Attributes](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_data_attributes),” Mozilla Developer Network

{{< signature "al, ea" >}}


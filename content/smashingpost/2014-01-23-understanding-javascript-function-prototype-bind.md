---
title: Understanding JavaScript Bind ()
slug: understanding-javascript-function-prototype-bind
image: null
date: 2014-01-23T09:47:00.000Z
author: ben-howdle
description: >-
  Function binding is probably your least concern when beginning with
  JavaScript, but when you realize that you need a solution to the problem of
  how to keep the context of “this” within another function, then you might not
  realize that what you actually need is Function.prototype.bind().
categories:
  - Coding
  - Tools
  - JavaScript
  - Techniques
---
Function binding is most probably your least concern when beginning with JavaScript, but when you realize that you need a solution to the problem of how to keep the context of <code>this</code> within another function, then you might not realize that what you actually need is <code>Function.prototype.bind()</code>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [What You Need To Know About JavaScript Scope](https://www.smashingmagazine.com/2009/08/what-you-need-to-know-about-javascript-scope/)
*   [An Introduction To DOM Events](https://www.smashingmagazine.com/2013/11/an-introduction-to-dom-events/)
*   [7 JavaScript Things I Wish I Knew Much Earlier In My Career](https://www.smashingmagazine.com/2010/04/seven-javascript-things-i-wish-i-knew-much-earlier-in-my-career/)
*   [<span class="headline">How To Write Fast, Memory-Efficient JavaScript</span>](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)

<p>The first time you hit upon the problem, you might be inclined to set <code>this</code> to a variable that you can reference when you change context. Many people opt for <code>self</code>, <code>_this</code> or sometimes <code>context</code> as a variable name. They’re all usable and nothing is wrong with doing that, but there is a better, dedicated way.<p>

<a href="https://twitter.com/jaffathecake/">Jack Archibald tweets about</a> caching <code>this</code>:

<blockquote class="twitter-tweet" lang="en">Ohhhh I would do anything for scope, but I won't do that = this

— Jake Archibald (@jaffathecake) February 20, 2013</blockquote>

<p>It should have been more apparent to me when <a href="https://twitter.com/sindresorhus/">Sindre Sorhus spelled it out</a>:</p>

<blockquote class="twitter-tweet" lang="en"><a href="https://twitter.com/benhowdle">@benhowdle</a> <a href="https://twitter.com/search?q=%24this&amp;src=ctag">$this</a> for jQuery, for plain JS i don't, use .bind()

— Sindre Sorhus (@sindresorhus) February 22, 2013</blockquote>

<p>I ignored this wise advice for many months.</p>

{{% feature-panel %}}

## What Problem Are We Actually Looking To Solve?

Here is sample code in which one could be forgiven for caching the context to a variable:

<pre><code class="language-javascript">
var myObj = {

    specialFunction: function () {

    },

    anotherSpecialFunction: function () {

    },

    getAsyncData: function (cb) {
        cb();
    },

    render: function () {
        var that = this;
        this.getAsyncData(function () {
            that.specialFunction();
            that.anotherSpecialFunction();
        });
    }
};

myObj.render();
</code></pre>

If we had left our function calls as <code>this.specialFunction()</code>, then we would have received the following error:

<pre><code class="language-javascript">
Uncaught TypeError: Object [object global] has no method 'specialFunction'
</code></pre>

We need to keep the context of the <code>myObj</code> object referenced for when the callback function is called. Calling <code>that.specialFunction()</code> enables us to maintain that context and correctly execute our function. However, this could be neatened somewhat by using <code>Function.prototype.bind()</code>.

Let’s rewrite our example:

<pre><code class="language-javascript">
render: function () {

    this.getAsyncData(function () {

        this.specialFunction();

        this.anotherSpecialFunction();

    }.bind(this));

}
</code></pre>

### What Did We Just Do?

Well, <code>.bind()</code> simply creates a new function that, when called, has its <code>this</code> keyword set to the provided value. So, we pass our desired context, <code>this</code> (which is <code>myObj</code>), into the <code>.bind()</code> function. Then, when the callback function is executed, <code>this</code> references <code>myObj</code>.

If you’re interested to see what <code>Function.prototype.bind()</code> might look like and what its doing internally, here is a very simple example:

<pre><code class="language-javascript">
Function.prototype.bind = function (scope) {
    var fn = this;
    return function () {
        return fn.apply(scope);
    };
}
</code></pre>

And here is a very simple use case:

<pre><code class="language-javascript">
var foo = {
    x: 3
}

var bar = function(){
    console.log(this.x);
}

bar(); // undefined

var boundFunc = bar.bind(foo);

boundFunc(); // 3
</code></pre>

We’ve created a new function that, when executed, has its <code>this</code> set to <code>foo</code> — not the global scope, as in the example where we called <code>bar();</code>.</p>

## Browser Support

<table class="table-overview">
<tbody>
<tr>
<th style="font-family: 'Proxima Nova Bold', Arial;">Browser</th>
<th style="font-family: 'Proxima Nova Bold', Arial;">Version support</th>
</tr>
<tr>
<td>Chrome</td>
<td>7</td>
</tr>
<tr>
<td>Firefox (Gecko)</td>
<td>4.0 (2)</td>
</tr>
<tr>
<td>Internet Explorer</td>
<td>9</td>
</tr>
<tr>
<td>Opera</td>
<td>11.60</td>
</tr>
<tr>
<td>Safari</td>
<td>5.1.4</td>
</tr>
</tbody>
</table>

As you can see, unfortunately, <code>Function.prototype.bind</code> isn’t supported in Internet Explorer 8 and below, so you’ll run into problems if you try to use it without a fallback.

Luckily, Mozilla Developer Network, being the wonderful resource it is, <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind">provides a rock-solid alternative</a> if the browser hasn’t implemented the native <code>.bind()</code> method:

<pre><code class="language-javascript">
if (!Function.prototype.bind) {
  Function.prototype.bind = function (oThis) {
    if (typeof this !== "function") {
      // closest thing possible to the ECMAScript 5 internal IsCallable function
      throw new TypeError("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var aArgs = Array.prototype.slice.call(arguments, 1),
        fToBind = this,
        fNOP = function () {},
        fBound = function () {
          return fToBind.apply(this instanceof fNOP &amp;&amp; oThis
                                 ? this
                                 : oThis,
                               aArgs.concat(Array.prototype.slice.call(arguments)));
        };

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();

    return fBound;
  };
}
</code></pre>

## Patterns For Usage

When learning something, I find it useful not only to thoroughly learn the concept, but to see it <em>applied</em> to what I’m currently working on (or something close to it). Hopefully, some of the examples below can be applied to your code or to problems you’re facing.</p>

### Click Handlers

One use is to track clicks (or to perform an action after a click) that might require us to store information in an object, like so:

<pre><code class="language-javascript">
var logger = {
    x: 0,
    updateCount: function(){
        this.x++;
        console.log(this.x);
    }
}
</code></pre>

We might assign click handlers like this and subsequently call the <code>updateCount()</code> in our <code>logger</code> object:

<pre><code class="language-javascript">
document.querySelector('button').addEventListener('click', function(){
    logger.updateCount();
});
</code></pre>

But we’ve had to create an unnecessary anonymous function to allow the <code>this</code> keyword to stand correct in the <code>updateCount()</code> function.

This could be neatened up, like so:

<pre><code class="language-javascript">
document.querySelector('button').addEventListener('click', logger.updateCount.bind(logger));
</code></pre>

We’ve used the subtly handy <code>.bind()</code> function to create a new function and then set the scope to be bound to the <code>logger</code> object.</p>

### setTimeout

If you’ve ever worked with templating engines (such as Handlebars) or especially with certain MV* frameworks (I can only speak of Backbone.js from experience), then you might be aware of the problem that occurs when you render the template but want to access the new DOM nodes immediately after your render call.

Suppose we try to instantiate a jQuery plugin:

<pre><code class="language-javascript">
var myView = {

    template: '/* a template string containing our &lt;select /&gt; */',

    $el: $('#content'),

    afterRender: function () {
        this.$el.find('select').myPlugin();
    },

    render: function () {
        this.$el.html(this.template());
        this.afterRender();
    }
}

myView.render();
</code></pre>

You might find that it works — but not all the time. Therein lies the problem. It’s a rat race: Whatever happens to get there first wins. Sometimes it’s the render, sometimes it’s the plugin’s instantiation.

Now, unbeknownst to some, we can use a slight hack with <code>setTimeout()</code>.

With a slight rewrite, we can safely instantiate our jQuery plugin once the DOM nodes are present:

<pre><code class="language-javascript">
//

    afterRender: function () {
        this.$el.find('select').myPlugin();
    },

    render: function () {
        this.$el.html(this.template());
        setTimeout(this.afterRender, 0);
    }

//
</code></pre>

However, we will receive the trusty message that the function <code>.afterRender()</code> cannot be found.

What we do, then, is throw our <code>.bind()</code> into the mix:

<pre><code class="language-javascript">
//

    afterRender: function () {
        this.$el.find('select').myPlugin();
    },

    render: function () {
        this.$el.html(this.template());
        setTimeout(this.afterRender.bind(this), 0);
    }

//
</code></pre>

Now, our <code>afterRender()</code> function will execute in the correct context.</p>

### Tidier Event Binding With querySelectorAll

The DOM API improved significantly once it included such useful methods as <code>querySelector</code>, <code>querySelectorAll</code> and the <code>classList</code> API, to name a few of the many.

However, there’s not really a way to natively add events to a <code>NodeList</code> as of yet. So, we end up stealing the <code>forEach</code> function from the <code>Array.prototype</code> to loop, like so:

<pre><code class="language-javascript">
Array.prototype.forEach.call(document.querySelectorAll('.klasses'), function(el){
    el.addEventListener('click', someFunction);
});
</code></pre>

We can do better than that, though, with our friend <code>.bind()</code>:

<pre><code class="language-javascript">
var unboundForEach = Array.prototype.forEach,
    forEach = Function.prototype.call.bind(unboundForEach);

forEach(document.querySelectorAll('.klasses'), function (el) {
    el.addEventListener('click', someFunction);
});
</code></pre>

We now have a tidy method to loop our DOM nodes.</p>

### Conclusion

As you can see, the javascript bind <code>()</code> function can be subtly included for many different purposes, as well as to neaten existing code. Hopefully, this overview has given you what you need to add <code>.bind()</code> to your own code (if necessary!) and to harness the power of transforming the value of <code>this</code>.

{{< signature "al, il" >}}


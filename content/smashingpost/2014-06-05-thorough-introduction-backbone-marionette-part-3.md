---
title: A Thorough Introduction To Backbone.Marionette (Part 3)
slug: thorough-introduction-backbone-marionette-part-3
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1aa2ebaa-1fbe-4567-a3f2-10f36859f7c5/backbone-marionette-javascript-illu.jpg
date: 2014-06-05T21:38:20.000Z
author: joseph-zimmerman
description: >-
  In this series on Backbone.Marionette, we’ve already discussed `Application`
  and `Module`. This time, we’ll be taking a gander at **how Marionette helps
  make views better in Backbone**. Marionette extends the base `View` class from
  Backbone to give us more built-in functionality, to eliminate most of the
  boilerplate code and to convert all of the common code down to configuration.
categories:
  - Coding
  - Frameworks
  - JavaScript
---
<em>To help you tap the full potential of Marionette, we've prepared an entire <a href="https://shop.smashingmagazine.com/better-backbone-applications-with-marionettejs.html">eBook</a> full of useful hands-on examples which is also available in the <a href="https://shop.smashingmagazine.com/smashing-library-complete.html">Smashing Library</a>. — Ed.</em>

In this series on Backbone.Marionette, we’ve already discussed <code>Application</code> and <code>Module</code>. This time, we’ll be taking a gander at <strong>how Marionette helps make views better in Backbone</strong>. Marionette extends the base <code>View</code> class from Backbone to give us more built-in functionality, to eliminate most of the boilerplate code and to convert all of the common code down to configuration.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">A Thorough Introduction To Backbone.Marionette (Part 1)</span>](https://www.smashingmagazine.com/2013/02/introduction-backbone-marionette/)
*   [<span class="headline">A Thorough Introduction To Backbone.Marionette (Part 2)</span>](https://www.smashingmagazine.com/2013/04/thorough-introduction-backbone-marionette-part-2-modules/)
*   [Backbone.js Tips And Patterns](https://www.smashingmagazine.com/2013/08/backbone-js-tips-patterns/)
*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)

I highly recommend that you go back and read the articles about <a title="A Thorough Introduction to Marionette Part 1: Application" href="https://www.smashingmagazine.com/2013/02/11/introduction-backbone-marionette/">Application</a> and <a title="A Thorough Introduction to Marionette Part 2: Modules" href="https://www.smashingmagazine.com/2013/04/02/thorough-introduction-backbone-marionette-part-2-modules/">Module</a> first, if you haven’t already. Some things may be mentioned in this article that refer to the previous articles, and this is part of a series about Marionette, so if you wish to learn about Marionette, you should read the whole series.

{{% feature-panel %}}

## Event Binding

Up until recently, Backbone views were often mishandled, causing a horrible problem known as “zombie views.” The problem was caused by the views listening to events on the model, which in itself is completely harmless. The problem was that when the views were no longer needed and were “discarded,” they never stopped listening to the events on the model, which means that the model still had a reference to the view, keeping it from being garbage-collected. This caused the amount of memory used by the application to constantly grow, and the view would still be responding to events from the model, although it wouldn’t be rendering anything because it was removed from the DOM.

Many Backbone extensions and plugins — including Marionette — remedied this early on. I won’t go into any detail on that, though, because Backbone’s developers remedied this problem themselves (finally!) in the recently released Backbone 1.0 by adding the <code>listenTo</code> and <code>stopListening</code> methods to <code>Events</code>, which Backbone’s <code>View</code> “class" inherits from. Marionette’s developers have since removed their own implementation of this feature, but that doesn’t mean Marionette doesn’t help us out with some other things related to event binding.

To make binding to events on the view’s models and collections simpler, Marionette gives us a few properties to use when extending Marionette’s views: <code>modelEvents</code> and <code>collectionEvents</code>. Simply pass in an object where the keys are the name of the event we’re listening to on the model or collection, and the property is the name(s) of the function to call when that event is triggered. Look at this simple example:

<pre><code class="language-javascript">
Backbone.Marionette.View.extend({ // We don't normally directly extend this view
    modelEvents: {
        'change:attribute': 'attributeChanged render',
        'destroy': 'modelDestroyed'
    },

    render: function(){ … },
    attributeChanged: function(){ … },
    modelDestroyed: function(){ … }
});
</code></pre>

This accomplishes the same thing as using <code>listenTo</code>, except it requires less code. Here’s the equivalent code using <code>listenTo</code>.

<pre><code class="language-javascript">
Backbone.Marionette.View.extend({ // We don't normally directly extend this view
    initialize: function() {
        this.listenTo(this.model, 'change:attribute', this.attributeChanged); 
        this.listenTo(this.model, 'change:attribute', this.render); 
        this.listenTo(this.model, 'destroy', this.modelDestroyed);
    },

    render: function(){ … },
    attributeChanged: function(){ … },
    modelDestroyed: function(){ … }
});
</code></pre>

There are a couple key things to note. First, <code>modelEvents</code> is used to listen to the view’s model, and <code>collectionEvents</code> is used to listen to the view’s collection (<code>this.model</code> and <code>this.collection</code>, respectively). Secondly, you may have noticed that there are two callbacks for the <code>change:attribute</code> event. When you specify a string for the callbacks, you can have as many callback function names as you want, separated by spaces. All of these functions will be invoked when the event is triggered. Any function name that you specify in the string must be a method of the view.

There are alternative ways to specify <code>modelEvents</code> and <code>collectionEvents</code>, too. First, instead of using a string to specify the names of methods on the view, you can assign anonymous functions:

<pre><code class="language-javascript">
Backbone.Marionette.View.extend({ // We don't normally directly extend this view
    modelEvents: {
        'change': function() {
            …
        }
    }
});
</code></pre>

This probably isn’t the best practice, but the option is there if you need it. Also, instead of simply assigning an object literal to <code>modelEvents</code> or <code>collectionEvents</code>, you can assign a function. The function will need to return an object that has the events and callbacks. This allows you to create the list of events and callbacks dynamically. I haven’t been able to think of any situations in which you would need to determine event bindings dynamically, but if you need it, this could be very handy.

<pre><code class="language-javascript">
Backbone.Marionette.View.extend({ // We don't normally directly extend this view
    modelEvents: function() {
        return {'destroy': 'modelDestroyed'};
    },

    modelDestroyed: function(){ … }
});
</code></pre>

The <code>modelEvents</code> and <code>collectionEvents</code> feature follows the pattern that Backbone and Marionette use as often as possible: Relegate code to simple configuration. Backbone itself did this with the <code>events</code> hash, which enables you to easily set up DOM event listeners. Marionette’s <code>modelEvents</code> and <code>collectionEvents</code> are directly inspired by the original <code>events</code> configuration in Backbone. You’ll see this configuration concept show up a lot, especially in subsequent articles, when we get into <code>ItemView</code>, <code>CollectionView</code> and <code>CompositeView</code>.</p>

## Destroying A View

As I mentioned at the beginning of the previous section, sometimes a view needs to be discarded or removed because a model was <a title="Backbone.Model Documentation: destroy" href="https://backbonejs.org/#Model-destroy">destroyed</a> or because we need to show a different view in its place. With <code>stopListening</code>, we have the power to clean up all of those event bindings. But what about destroying the rest of the view? Backbone has a <code>remove</code> function that calls <code>stopListening</code> for us and also removes the view from the DOM.

Generally, this would be all you need, but Marionette takes it a step further by adding the <code>close</code> function. When using Marionette’s views, you’ll want to call <code>close</code> instead of <code>remove</code> because it will clean up all of the things that Marionette’s views set up in the background.

Another benefit offered by Marionette’s <code>close</code> method is that it fires off some events. At the start of closing the view, it’ll fire off the <code>before:close</code> event, and then the <code>close</code> event when it’s finished. In addition to the events, you can specify methods on the view that will run just before these events are fired.

<pre><code class="language-javascript">
Backbone.Marionette.View.extend({ // We don't normally directly extend this view
    onBeforeClose: function() {
        // This will run just before the before:close event is fired
    },

    onClose: function(){
        // This will run just before the close event is fired
    }
});
</code></pre>

If you want to run some code before the view disappears completely, you can use the <code>onBeforeClose</code> and <code>onClose</code> view methods to automatically have it run without your needing to listen to the events. Simply declare the methods, and Marionette will make sure they are invoked. Of course, other objects will still need to listen to the events on the view.</p>

## DOM Refresh

Back when we discussed <code>Application</code>, I mentioned <code>Region</code> a bit. I won’t get into this much here (once all of the articles about views are done, I’ll go into more detail), but know that a <code>Region</code> is an object that handles the showing and hiding or discarding of views in a particular part of the DOM. Look at the code below to see how to render a view in a <code>Region</code>.

<pre><code class="language-javascript">
var view = new FooView(); // Assume FooView has already been defined
region.show(view); // Assume the region was already instantiated. Just use "show" to render the view.
</code></pre>

When you use <code>show</code>, it will render the view (all view classes that Marionette implements that are based on this base <code>View</code> class will also call the <code>onRender</code> function if you’ve defined it and will fire a <code>render</code> event when <code>render</code> is invoked), attach it to the DOM and then show the view, which simply means that a <code>show</code> event is fired so that components will know that the view was rendered via a <code>Region</code>. After a view has been rendered and then shown, if the view is rendered again, it will trigger a DOM refresh.

This actually isn’t true at the moment because of a bug, but it’s on the developers’ to-do list. Currently, when a view is rendered, it will set a flag saying that it was rendered. Then, when the view is shown, it will set a flag saying that it was shown. The moment when both of these flags have been activated, it will trigger a DOM refresh. Then, any time after that, the DOM refresh will be triggered any time the view is rendered or shown. Keep this in mind if you need to use this functionality.

When a DOM refresh is triggered, first, it will run the <code>onDomRefresh</code> method of the view (if you defined one) and then trigger the <code>dom:refresh</code> event on the view. This is mostly useful for UI plugins (such as jQuery UI, Kendo UI, etc.) with some widgets that depend on the DOM element they are working with being in the actual DOM. Often, when a view is rendered, it won’t be appended into the DOM until after the rendering has finished. This means that you can’t use the plugin during <code>render</code> or in your <code>onRender</code> function.

However, you can use it in <code>onShow</code> (which is invoked just before the <code>show</code> event is triggered) because a Region is supposed to be attached to an existing DOM node (as we’ll see in a future article). Now, since the view has been shown, you will know that the view is in the DOM; so, every time <code>render</code> is called, a DOM refresh will take place immediately after the rendering, and you can call the UI plugin’s functionality safely again.

## DOM Triggers

Sometimes, when a user clicks a button, you want to respond to the event, but you don’t want the view to handle the work. Instead, you want the view to trigger an event so that other modules that are listening for this event can respond to it. Suppose you have code that looks like this:

<pre><code class="language-javascript">
Backbone.Marionette.View.extend({ // We don't normally directly extend this view
    events: {
        'click .awesomeButton': 'buttonClicked'
    },
    buttonClicked: function() {
        this.trigger('awesomeButton:clicked', this);
    }
});
</code></pre>

The function for handling the click event just triggers an event on the view. Marionette has a feature that allows you to specify a hash of these events to simplify this code. By specifying the <code>triggers</code> property when extending a <code>View</code>, you can assign a hash very similar to the <code>events</code> property; but, instead of giving it the name of one of the view’s methods to invoke, you give it the name of an event to fire. So, we can convert the previous snippet to this:

<pre><code class="language-javascript">
Backbone.Marionette.View.extend({ // We don't normally directly extend this view
    triggers: {
        'click .awesomeButton': ' awesomeButton:clicked '
    }
});
</code></pre>

And it’ll do nearly the same thing. There is one major difference between these two snippets: the arguments that are passed to the listening functions. In the first snippet, all we passed to the functions listening for the event was <code>this</code>, which was the view. Using <code>triggers</code>, Marionette will pass a single object with three properties as the argument to each of the functions. These three properties are the following:

*   `view` A reference to the view object that triggered the event.
*   `model` A reference to the view’s `model` property, if it has one.
*   `collection` A reference to the view’s `collection` property, if it has one.

So, if you were subscribing to the event from the previous snippet, it would look like this:

<pre><code class="language-javascript">
// 'view' refers to an instance of the previously defined View type
view.on('awesomeButton:clicked', function(arg) {
    arg.view; // The view instance
    arg.model; // The view's model
    arg.collection; // The view's collection
}
</code></pre>

I know there isn’t a surplus of use cases for this, but in the few situations where this applies, it can save plenty of hassle.</p>

## DOM Element Caching

Often, <code>this.$el</code> isn’t the only element that you’ll need to directly manipulate. In such cases, many people will do something like this:

<pre><code class="language-javascript">
Backbone.Marionette.View.extend({ // We don't normally directly extend this view
    render: function() {
        this.list = this.$('ul');
        this.listItems = this.$('li');
        . . .
        // Now we use them and use them in other methods, too.
    }
});
</code></pre>

Once again, Marionette makes this simpler by converting this all into a simple configuration. Just specify a <code>ui</code> property that contains a hash of names and their corresponding selectors:

<pre><code class="language-javascript">
Backbone.Marionette.View.extend({ // We don't normally directly extend this view
    ui: {
        list: 'ul',
        listItems: 'li'
    }
});
</code></pre>

You can access these elements with <code>this.ui.x</code>, where <code>x</code> is the name specified in the hash, such as <code>this.ui.list</code>. This <code>ui</code> property is converted into the cached jQuery objects by the <code>bindUIElements</code> method. If you’re extending <code>Marionette.View</code>, instead of one of the other view types that Marionette offers, then you’ll need to call this method yourself; otherwise, the other view types will call it for you automatically.

<pre><code class="language-javascript">
Backbone.Marionette.View.extend({ // We don't normally directly extend this view
    ui: {
        list: 'ul',
        listItems: 'li'
        },
    render: function() {
        // render template or generate your HTML, then…
        this.bindUIElements();
        // now you can manipulate the elements
        this.ui.list.hide();
        this.ui.listItems.addClass('someCoolClass');
    }
});
</code></pre>

## Conclusion

We’ve already seen a plethora of features that Marionette brings to views that cut down on the complexity and amount of code required for common tasks, but we haven’t even touched on the most important part. <code>Marionette.View</code> doesn’t handle any of the rendering responsibilities for us, but Marionette has three other view types that do: <code>ItemView</code>, <code>CollectionView</code> and <code>CompositeView</code>.

These view types, which are what you’ll actually be extending in your code (note the “We don’t normally directly extend this view” comment in all of the code snippets), will take a few minor configuration details and then handle the rest of the rendering for you. We’ll see how this is all done in the next article. For now, ponder all of these features that you’ve been introduced to.

<em>(Front page image credits: <a href="https://www.flickr.com/photos/nyuhuhuu/4443886636/">nyuhuhuu</a></em>)

{{< signature "al, il" >}}


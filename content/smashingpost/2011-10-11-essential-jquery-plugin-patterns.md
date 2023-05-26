---
title: Essential jQuery Plugin Patterns
slug: essential-jquery-plugin-patterns
image: >-
  https://www.smashingmagazine.com/general/2014/03/04/183006-revision-9/attachment/idiots/
date: 2011-10-11T12:30:11.000Z
author: addy-osmani
description: >-
  I occasionally write about implementing _design patterns_ in JavaScript.
  They’re an excellent way of building upon proven approaches to solving common
  development problems, and I think there’s a lot of benefit to using them. But
  while well-known JavaScript patterns are useful, another side of development
  could benefit from its own set of design patterns: jQuery plugins. The
  official jQuery _plugin authoring guide_ offers a great starting point for
  getting into writing plugins and widgets, but let’s take it further.
categories:
  - Coding
  - jQuery
---
I occasionally write about implementing <a href="https://addyosmani.com/resources/essentialjsdesignpatterns/book/" rel="nofollow">design patterns</a> in JavaScript. They’re an excellent way of building upon proven approaches to solving common development problems, and I think there’s a lot of benefit to using them. But while well-known JavaScript patterns are useful, another side of development could benefit from its own set of design patterns: jQuery plugins. The official jQuery <a href="https://docs.jquery.com/Plugins/Authoring" rel="nofollow">plugin authoring guide</a> offers a great starting point for getting into writing plugins and widgets, but let’s take it further.

Plugin development has evolved over the past few years. We no longer have just one way to write plugins, but many. In reality, certain patterns might work better for a particular problem or component than others.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Useful JavaScript And jQuery Tools, Libraries, Plugins](https://www.smashingmagazine.com/2011/04/useful-javascript-and-jquery-tools-libraries-plugins/)
*   [Useful JavaScript Libraries and jQuery Plugins](https://www.smashingmagazine.com/2012/09/useful-javascript-libraries-jquery-plugins-web-developers/)
*   [Spicing Up Your Website With jQuery Goodness](https://www.smashingmagazine.com/2010/06/spice-up-your-website-with-jquery-goodness/)
*   [<span class="headline">Magnific Popup, A Truly Responsive Lightbox</span>](https://www.smashingmagazine.com/2013/05/truly-responsive-lightbox/)

Some developers may wish to use the jQuery UI <a href="https://ajpiano.com/widgetfactory/" rel="nofollow">widget factory</a>; it’s great for complex, flexible UI components. Some may not. Some might like to structure their plugins more like modules (similar to the module pattern) or use a more formal module format such as <a href="https://github.com/amdjs/amdjs-api/wiki/AMD" rel="nofollow">AMD (asynchronous module definition)</a>. Some might want their plugins to harness the power of prototypal inheritance. Some might want to use custom events or pub/sub to communicate from plugins to the rest of their app. And so on.

{{% feature-panel %}}

I began to think about plugin patterns after noticing a number of efforts to create a one-size-fits-all jQuery plugin boilerplate. While such a boilerplate is a great idea in theory, the reality is that we rarely write plugins in one fixed way, using a single pattern all the time.

Let’s assume that you’ve tried your hand at writing your own jQuery plugins at some point and you’re comfortable putting together something that works. It’s functional. It does what it needs to do, but perhaps you feel it could be structured better. Maybe it could be more flexible or could solve more issues. If this sounds familiar and you aren’t sure of the differences between many of the different jQuery plugin patterns, then you might find what I have to say helpful.

My advice won’t provide solutions to every possible pattern, but it will cover popular patterns that developers use in the wild.

<strong>Note:</strong> This post is targeted at intermediate to advanced developers. If you don’t feel you’re ready for this just yet, I’m happy to recommend the official jQuery <a href="https://docs.jquery.com/Plugins/Authoring" rel="nofollow">Plugins/Authoring</a> guide, Ben Alman’s <a href="https://msdn.microsoft.com/en-us/scriptjunkie/ff696759" rel="nofollow">plugin style guide</a> and Remy Sharp’s “<a href="https://remysharp.com/2010/06/03/signs-of-a-poorly-written-jquery-plugin/" rel="nofollow">Signs of a Poorly Written jQuery Plugin</a>.”

## Patterns

jQuery plugins have very few defined rules, which one of the reasons for the incredible diversity in how they’re implemented. At the most basic level, you can write a plugin simply by adding a new function property to jQuery’s <code>$.fn</code> object, as follows:

<pre><code class="language-javascript">$.fn.myPluginName = function() {
    // your plugin logic
};</code></pre>

This is great for compactness, but the following would be a better foundation to build on:

<pre><code class="language-javascript">(function( $ ){
  $.fn.myPluginName = function() {
    // your plugin logic
  };
})( jQuery );</code></pre>

Here, we’ve wrapped our plugin logic in an anonymous function. To ensure that our use of the <code>$</code> sign as a shorthand creates no conflicts between jQuery and other JavaScript libraries, we simply pass it to this closure, which maps it to the dollar sign, thus ensuring that it can’t be affected by anything outside of its scope of execution.

An alternative way to write this pattern would be to use <code>$.extend</code>, which enables you to define multiple functions at once and which sometimes make more sense semantically:

<pre><code class="language-javascript">(function( $ ){
    $.extend($.fn, {
        myplugin: function(){
            // your plugin logic
        }
    });
})( jQuery );</code></pre>

We could do a lot more to improve on all of this; and the first complete pattern we’ll be looking at today, the lightweight pattern, covers some best practices that we can use for basic everyday plugin development and that takes into account common gotchas to look out for.

### Some Quick Notes

While most of the patterns below will be explained, I recommend reading through the comments in the code, because they will offer more insight into why certain practices are best.

I should also mention that none of this would be possible without the previous work, input and advice of other members of the jQuery community. I’ve listed them inline with each pattern so that you can read up on their individual work if interested.</p>

## A Lightweight Start

Let’s begin our look at patterns with something basic that follows best practices (including those in the jQuery plugin-authoring guide). This pattern is ideal for developers who are either new to plugin development or who just want to achieve something simple (such as a utility plugin). This lightweight start uses the following:

*   Common best practices, such as a semi-colon before the function’s invocation; `window, document, undefined` passed in as arguments; and adherence to the jQuery core style guidelines.
*   A basic defaults object.
*   A simple plugin constructor for logic related to the initial creation and the assignment of the element to work with.
*   Extending the options with defaults.
*   A lightweight wrapper around the constructor, which helps to avoid issues such as multiple instantiations.

<pre><code class="language-javascript">/*!
 * jQuery lightweight plugin boilerplate
 * Original author: @ajpiano
 * Further changes, comments: @addyosmani
 * Licensed under the MIT license
 */

// the semi-colon before the function invocation is a safety 
// net against concatenated scripts and/or other plugins 
// that are not closed properly.
;(function ( $, window, document, undefined ) {

    // undefined is used here as the undefined global 
    // variable in ECMAScript 3 and is mutable (i.e. it can 
    // be changed by someone else). undefined isn't really 
    // being passed in so we can ensure that its value is 
    // truly undefined. In ES5, undefined can no longer be 
    // modified.

    // window and document are passed through as local 
    // variables rather than as globals, because this (slightly) 
    // quickens the resolution process and can be more 
    // efficiently minified (especially when both are 
    // regularly referenced in your plugin).

    // Create the defaults once
    var pluginName = 'defaultPluginName',
        defaults = {
            propertyName: "value"
        };

    // The actual plugin constructor
    function Plugin( element, options ) {
        this.element = element;

        // jQuery has an extend method that merges the 
        // contents of two or more objects, storing the 
        // result in the first object. The first object 
        // is generally empty because we don't want to alter 
        // the default options for future instances of the plugin
        this.options = $.extend( {}, defaults, options) ;

        this._defaults = defaults;
        this._name = pluginName;

        this.init();
    }

    Plugin.prototype.init = function () {
        // Place initialization logic here
        // You already have access to the DOM element and
        // the options via the instance, e.g. this.element 
        // and this.options
    };

    // A really lightweight plugin wrapper around the constructor, 
    // preventing against multiple instantiations
    $.fn[pluginName] = function ( options ) {
        return this.each(function () {
            if (!$.data(this, 'plugin_' + pluginName)) {
                $.data(this, 'plugin_' + pluginName, 
                new Plugin( this, options ));
            }
        });
    }

})( jQuery, window, document );</code></pre>

### Further Reading

*   [Plugins/Authoring](https://docs.jquery.com/Plugins/Authoring), jQuery
*   “[Signs of a Poorly Written jQuery Plugin](https://remysharp.com/2010/06/03/signs-of-a-poorly-written-jquery-plugin/),” Remy Sharp
*   “[How to Create Your Own jQuery Plugin](https://msdn.microsoft.com/en-us/scriptjunkie/ff608209),” Elijah Manor
*   “[Style in jQuery Plugins and Why It Matters](https://msdn.microsoft.com/en-us/scriptjunkie/ff696759),” Ben Almon
*   “Create Your First jQuery Plugin, Part 2,” Andrew Wirick

## “Complete” Widget Factory

While the authoring guide is a great introduction to plugin development, it doesn’t offer a great number of conveniences for obscuring away from common plumbing tasks that we have to deal with on a regular basis.

The jQuery UI Widget Factory is a solution to this problem that helps you build complex, stateful plugins based on object-oriented principles. It also eases communication with your plugin’s instance, obfuscating a number of the repetitive tasks that you would have to code when working with basic plugins.

In case you haven’t come across these before, stateful plugins keep track of their current state, also allowing you to change properties of the plugin after it has been initialized.

One of the great things about the Widget Factory is that the majority of the jQuery UI library actually uses it as a base for its components. This means that if you’re looking for further guidance on structure beyond this template, you won’t have to look beyond the jQuery UI repository.

Back to patterns. This jQuery UI boilerplate does the following:

*   Covers almost all supported default methods, including triggering events.
*   Includes comments for all of the methods used, so that you’re never unsure of where logic should fit in your plugin.

<pre><code class="language-javascript">/*!
 * jQuery UI Widget-factory plugin boilerplate (for 1.8/9+)
 * Author: @addyosmani
 * Further changes: @peolanha
 * Licensed under the MIT license
 */

;(function ( $, window, document, undefined ) {

    // define your widget under a namespace of your choice
    //  with additional parameters e.g.

    // $.widget( "namespace.widgetname", (optional) - an 
    // existing widget prototype to inherit from, an object 
    // literal to become the widget's prototype ); 

    $.widget( "namespace.widgetname" , {

        //Options to be used as defaults
        options: {
            someValue: null
        },

        //Setup widget (eg. element creation, apply theming
        // , bind events etc.)
        _create: function () {

            // _create will automatically run the first time 
            // this widget is called. Put the initial widget 
            // setup code here, then you can access the element 
            // on which the widget was called via this.element.

            // The options defined above can be accessed 
            // via this.options this.element.addStuff();
        },

        // Destroy an instantiated plugin and clean up 
        // modifications the widget has made to the DOM
        destroy: function () {

            // this.element.removeStuff();
            // For UI 1.8, destroy must be invoked from the 
            // base widget
            $.Widget.prototype.destroy.call(this);
            // For UI 1.9, define _destroy instead and don't 
            // worry about 
            // calling the base widget
        },

        methodB: function ( event ) {
            //_trigger dispatches callbacks the plugin user 
            // can subscribe to
            // signature: _trigger( "callbackName" , [eventObject], 
            // [uiObject] )
            // eg. this._trigger( "hover", e /*where e.type == 
            // "mouseenter"*/, { hovered: $(e.target)});
            this._trigger('methodA', event, {
                key: value
            });
        },

        methodA: function ( event ) {
            this._trigger('dataChanged', event, {
                key: value
            });
        },

        // Respond to any changes the user makes to the 
        // option method
        _setOption: function ( key, value ) {
            switch (key) {
            case "someValue":
                //this.options.someValue = doSomethingWith( value );
                break;
            default:
                //this.options[ key ] = value;
                break;
            }

            // For UI 1.8, _setOption must be manually invoked 
            // from the base widget
            $.Widget.prototype._setOption.apply( this, arguments );
            // For UI 1.9 the _super method can be used instead
            // this._super( "_setOption", key, value );
        }
    });

})( jQuery, window, document );</code></pre>

### Further Reading

*   [The jQuery UI Widget Factory](https://ajpiano.com/widgetfactory/#slide1)
*   “[Introduction to Stateful Plugins and the Widget Factory](https://msdn.microsoft.com/en-us/scriptjunkie/ff706600),” Doug Neiner
*   “[Widget Factory](https://wiki.jqueryui.com/w/page/12138135/Widget factory)” (explained), Scott Gonzalez
*   “[Understanding jQuery UI Widgets: A Tutorial](https://bililite.com/blog/understanding-jquery-ui-widgets-a-tutorial/),” Hacking at 0300

## Namespacing And Nested Namespacing

Namespacing your code is a way to avoid collisions with other objects and variables in the global namespace. They’re important because you want to safeguard your plugin from breaking in the event that another script on the page uses the same variable or plugin names as yours. As a good citizen of the global namespace, you must also do your best not to prevent other developers’ scripts from executing because of the same issues.

JavaScript doesn’t really have built-in support for namespaces as other languages do, but it does have objects that can be used to achieve a similar effect. Employing a top-level object as the name of your namespace, you can easily check for the existence of another object on the page with the same name. If such an object does not exist, then we define it; if it does exist, then we simply extend it with our plugin.

Objects (or, rather, object literals) can be used to create nested namespaces, such as <code>namespace.subnamespace.pluginName</code> and so on. But to keep things simple, the namespacing boilerplate below should give you everything you need to get started with these concepts.

<pre><code class="language-javascript">/*!
 * jQuery namespaced 'Starter' plugin boilerplate
 * Author: @dougneiner
 * Further changes: @addyosmani
 * Licensed under the MIT license
 */

;(function ( $ ) {
    if (!$.myNamespace) {
        $.myNamespace = {};
    };

    $.myNamespace.myPluginName = function ( el, myFunctionParam, options ) {
        // To avoid scope issues, use 'base' instead of 'this'
        // to reference this class from internal events and functions.
        var base = this;

        // Access to jQuery and DOM versions of element
        base.$el = $(el);
        base.el = el;

        // Add a reverse reference to the DOM object
        base.$el.data( "myNamespace.myPluginName" , base );

        base.init = function () {
            base.myFunctionParam = myFunctionParam;

            base.options = $.extend({}, 
            $.myNamespace.myPluginName.defaultOptions, options);

            // Put your initialization code here
        };

        // Sample Function, Uncomment to use
        // base.functionName = function( paramaters ){
        // 
        // };
        // Run initializer
        base.init();
    };

    $.myNamespace.myPluginName.defaultOptions = {
        myDefaultValue: ""
    };

    $.fn.mynamespace_myPluginName = function 
        ( myFunctionParam, options ) {
        return this.each(function () {
            (new $.myNamespace.myPluginName(this, 
            myFunctionParam, options));
        });
    };

})( jQuery );</code></pre>

### Further Reading

*   “[Namespacing in JavaScript](https://javascriptweblog.wordpress.com/2010/12/07/namespacing-in-javascript/),” Angus Croll
*   “[Use Your $.fn jQuery Namespace](https://ryanflorence.com/use-your-fn-jquery-namespace/),” Ryan Florence
*   “JavaScript Namespacing,” Peter Michaux
*   “[Modules and namespaces in JavaScript](https://www.2ality.com/2011/04/modules-and-namespaces-in-javascript.html),” Axel Rauschmayer

## Custom Events For Pub/Sub (With The Widget factory)

You may have used the Observer (Pub/Sub) pattern in the past to develop asynchronous JavaScript applications. The basic idea here is that elements will publish event notifications when something interesting occurs in your application. Other elements then subscribe to or listen for these events and respond accordingly. This results in the logic for your application being significantly more decoupled (which is always good).

In jQuery, we have this idea that custom events provide a built-in means to implement a publish and subscribe system that’s quite similar to the Observer pattern. So, <code>bind('eventType')</code> is functionally equivalent to performing <code>subscribe('eventType')</code>, and <code>trigger('eventType')</code> is roughly equivalent to <code>publish('eventType')</code>.

Some developers might consider the jQuery event system as having too much overhead to be used as a publish and subscribe system, but it’s been architected to be both reliable and robust for most use cases. In the following jQuery UI widget factory template, we’ll implement a basic custom event-based pub/sub pattern that allows our plugin to subscribe to event notifications from the rest of our application, which publishes them.

<pre><code class="language-javascript">/*!
 * jQuery custom-events plugin boilerplate
 * Author: DevPatch
 * Further changes: @addyosmani
 * Licensed under the MIT license
 */

// In this pattern, we use jQuery's custom events to add 
// pub/sub (publish/subscribe) capabilities to widgets. 
// Each widget would publish certain events and subscribe 
// to others. This approach effectively helps to decouple 
// the widgets and enables them to function independently.

;(function ( $, window, document, undefined ) {
    $.widget("ao.eventStatus", {
        options: {

        },

        _create : function() {
            var self = this;

            //self.element.addClass( "my-widget" );

            //subscribe to 'myEventStart'
            self.element.bind( "myEventStart", function( e ) {
                console.log("event start");
            });

            //subscribe to 'myEventEnd'
            self.element.bind( "myEventEnd", function( e ) {
                console.log("event end");
            });

            //unsubscribe to 'myEventStart'
            //self.element.unbind( "myEventStart", function(e){
                ///console.log("unsubscribed to this event"); 
            //});
        },

        destroy: function(){
            $.Widget.prototype.destroy.apply( this, arguments );
        },
    });
})( jQuery, window , document );

//Publishing event notifications
//usage: 
// $(".my-widget").trigger("myEventStart");
// $(".my-widget").trigger("myEventEnd");</code></pre>

### Further Reading

*   “Communication Between jQuery UI Widgets,” Benjamin Sternthal
*   “[Understanding the Publish/Subscribe Pattern for Greater JavaScript Scalability](https://msdn.microsoft.com/en-us/scriptjunkie/hh201955.aspx),” Addy Osmani

## Prototypal Inheritance With The DOM-To-Object Bridge Pattern

In JavaScript, we don’t have the traditional notion of classes that you would find in other classical programming languages, but we do have prototypal inheritance. With prototypal inheritance, an object inherits from another object. And we can apply this concept to jQuery plugin development.

<a href="https://alexsexton.com/" rel="nofollow">Alex Sexton</a> and <a href="https://scottgonzalez.com/" rel="nofollow">Scott Gonzalez</a> have looked at this topic in detail. In sum, they found that for organized modular development, clearly separating the object that defines the logic for a plugin from the plugin-generation process itself can be beneficial. The benefit is that testing your plugin’s code becomes easier, and you can also adjust the way things work behind the scenes without altering the way that any object APIs you’ve implemented are used.

In Sexton’s previous post on this topic, he implements a bridge that enables you to attach your general logic to a particular plugin, which we’ve implemented in the template below. Another advantage of this pattern is that you don’t have to constantly repeat the same plugin initialization code, thus ensuring that the concepts behind DRY development are maintained. Some developers might also find this pattern easier to read than others.

<pre><code class="language-javascript">/*!
 * jQuery prototypal inheritance plugin boilerplate
 * Author: Alex Sexton, Scott Gonzalez
 * Further changes: @addyosmani
 * Licensed under the MIT license
 */

// myObject - an object representing a concept that you want 
// to model (e.g. a car)
var myObject = {
  init: function( options, elem ) {
    // Mix in the passed-in options with the default options
    this.options = $.extend( {}, this.options, options );

    // Save the element reference, both as a jQuery
    // reference and a normal reference
    this.elem  = elem;
    this.$elem = $(elem);

    // Build the DOM's initial structure
    this._build();

    // return this so that we can chain and use the bridge with less code.
    return this;
  },
  options: {
    name: "No name"
  },
  _build: function(){
    //this.$elem.html('&lt;h1&gt;'+this.options.name+'&lt;/h1&gt;');
  },
  myMethod: function( msg ){
    // You have direct access to the associated and cached
    // jQuery element
    // this.$elem.append('&lt;p&gt;'+msg+'&lt;/p&gt;');
  }
};

// Object.create support test, and fallback for browsers without it
if ( typeof Object.create !== 'function' ) {
    Object.create = function (o) {
        function F() {}
        F.prototype = o;
        return new F();
    };
}

// Create a plugin based on a defined object
$.plugin = function( name, object ) {
  $.fn[name] = function( options ) {
    return this.each(function() {
      if ( ! $.data( this, name ) ) {
        $.data( this, name, Object.create(object).init( 
        options, this ) );
      }
    });
  };
};

// Usage:
// With myObject, we could now essentially do this:
// $.plugin('myobj', myObject);

// and at this point we could do the following
// $('#elem').myobj({name: "John"});
// var inst = $('#elem').data('myobj');
// inst.myMethod('I am a method');</code></pre>

### Further Reading

*   “[Using Inheritance Patterns To Organize Large jQuery Applications](https://alexsexton.com/?p=51),” Alex Sexton
*   “[How to Manage Large Applications With jQuery or Whatever](https://www.slideshare.net/SlexAxton/how-to-manage-large-jquery-apps)” (further discussion), Alex Sexton
*   “[Practical Example of the Need for Prototypal Inheritance](https://blog.bigbinary.com/2010/03/12/pratical-example-of-need-for-prototypal-inheritance.html),” Neeraj Singh
*   “[Prototypal Inheritance in JavaScript](https://javascript.crockford.com/prototypal.html),” Douglas Crockford

## jQuery UI Widget Factory Bridge

If you liked the idea of generating plugins based on objects in the last design pattern, then you might be interested in a method found in the jQuery UI Widget Factory called <code>$.widget.bridge</code>. This bridge basically serves as a middle layer between a JavaScript object that is created using <code>$.widget</code> and jQuery’s API, providing a more built-in solution to achieving object-based plugin definition. Effectively, we’re able to create stateful plugins using a custom constructor.

Moreover, <code>$.widget.bridge</code> provides access to a number of other capabilities, including the following:

*   Both public and private methods are handled as one would expect in classical OOP (i.e. public methods are exposed, while calls to private methods are not possible);
*   Automatic protection against multiple initializations;
*   Automatic generation of instances of a passed object, and storage of them within the selection’s internal `$.data` cache;
*   Options can be altered post-initialization.

For further information on how to use this pattern, look at the comments in the boilerplate below:

<pre><code class="language-javascript">/*!
 * jQuery UI Widget factory "bridge" plugin boilerplate
 * Author: @erichynds
 * Further changes, additional comments: @addyosmani
 * Licensed under the MIT license
 */

// a "widgetName" object constructor
// required: this must accept two arguments,
// options: an object of configuration options
// element: the DOM element the instance was created on
var widgetName = function( options, element ){
  this.name = "myWidgetName";
  this.options = options;
  this.element = element;
  this._init();
}

// the "widgetName" prototype
widgetName.prototype = {

    // _create will automatically run the first time this 
    // widget is called
    _create: function(){
        // creation code
    },

    // required: initialization logic for the plugin goes into _init
    // This fires when your instance is first created and when 
    // attempting to initialize the widget again (by the bridge)
    // after it has already been initialized.
    _init: function(){
        // init code
    },

    // required: objects to be used with the bridge must contain an 
    // 'option'. Post-initialization, the logic for changing options
    // goes here.

    option: function( key, value ){

        // optional: get/change options post initialization
        // ignore if you don't require them.

        // signature: $('#foo').bar({ cool:false });
        if( $.isPlainObject( key ) ){
            this.options = $.extend( true, this.options, key );

        // signature: $('#foo').option('cool'); - getter
        } else if ( key &amp;&amp; typeof value === "undefined" ){
            return this.options[ key ];

        // signature: $('#foo').bar('option', 'baz', false);
        } else {
            this.options[ key ] = value;
        }

        // required: option must return the current instance.

        // When re-initializing an instance on elements, option 
        // is called first and is then chained to the _init method.
        return this;  
    },

    // notice no underscore is used for public methods
    publicFunction: function(){ 
        console.log('public function');
    },

    // underscores are used for private methods
    _privateFunction: function(){ 
        console.log('private function');
    }
};

// usage:

// connect the widget obj to jQuery's API under the "foo" namespace
// $.widget.bridge("foo", widgetName);

// create an instance of the widget for use
// var instance = $("#elem").foo({
//     baz: true
// });

// your widget instance exists in the elem's data
// instance.data("foo").element; // =&gt; #elem element

// bridge allows you to call public methods...
// instance.foo("publicFunction"); // =&gt; "public method"

// bridge prevents calls to internal methods
// instance.foo("_privateFunction"); // =&gt; #elem element</code></pre>

### Further Reading

*   “[Using $.widget.bridge Outside of the Widget Factory](https://erichynds.com/jquery/using-jquery-ui-widget-factory-bridge/),” Eric Hynds

## jQuery Mobile Widgets With The Widget factory

jQuery mobile is a framework that encourages the design of ubiquitous Web applications that work both on popular mobile devices and platforms and on the desktop. Rather than writing unique applications for each device or OS, you simply write the code once and it should ideally run on many of the A-, B- and C-grade browsers out there at the moment.

The fundamentals behind jQuery mobile can also be applied to plugin and widget development, as seen in some of the core jQuery mobile widgets used in the official library suite. What’s interesting here is that even though there are very small, subtle differences in writing a “mobile”-optimized widget, if you’re familiar with using the jQuery UI Widget Factory, you should be able to start writing these right away.

The mobile-optimized widget below has a number of interesting differences than the standard UI widget pattern we saw earlier:

*   `$.mobile.widget` is referenced as an existing widget prototype from which to inherit. For standard widgets, passing through any such prototype is unnecessary for basic development, but using this jQuery-mobile specific widget prototype provides internal access to further “options” formatting.
*   You’ll notice in `_create()` a guide on how the official jQuery mobile widgets handle element selection, opting for a role-based approach that better fits the jQM mark-up. This isn’t at all to say that standard selection isn’t recommended, only that this approach might make more sense given the structure of jQM pages.
*   Guidelines are also provided in comment form for applying your plugin methods on `pagecreate` as well as for selecting the plugin application via data roles and data attributes.

<pre><code class="language-javascript">/*!
 * (jQuery mobile) jQuery UI Widget-factory plugin boilerplate (for 1.8/9+)
 * Author: @scottjehl
 * Further changes: @addyosmani
 * Licensed under the MIT license
 */

;(function ( $, window, document, undefined ) {

    //define a widget under a namespace of your choice
    //here 'mobile' has been used in the first parameter
    $.widget( "mobile.widgetName", $.mobile.widget, {

        //Options to be used as defaults
        options: {
            foo: true,
            bar: false
        },

        _create: function() {
            // _create will automatically run the first time this 
            // widget is called. Put the initial widget set-up code 
            // here, then you can access the element on which 
            // the widget was called via this.element
            // The options defined above can be accessed via 
            // this.options

            //var m = this.element,
            //p = m.parents(":jqmData(role='page')"),
            //c = p.find(":jqmData(role='content')")
        },

        // Private methods/props start with underscores
        _dosomething: function(){ ... },

        // Public methods like these below can can be called 
                // externally: 
        // $("#myelem").foo( "enable", arguments );

        enable: function() { ... },

        // Destroy an instantiated plugin and clean up modifications 
        // the widget has made to the DOM
        destroy: function () {
            //this.element.removeStuff();
            // For UI 1.8, destroy must be invoked from the 
            // base widget
            $.Widget.prototype.destroy.call(this);
            // For UI 1.9, define _destroy instead and don't 
            // worry about calling the base widget
        },

        methodB: function ( event ) {
            //_trigger dispatches callbacks the plugin user can 
            // subscribe to
            //signature: _trigger( "callbackName" , [eventObject],
            //  [uiObject] )
            // eg. this._trigger( "hover", e /*where e.type == 
            // "mouseenter"*/, { hovered: $(e.target)});
            this._trigger('methodA', event, {
                key: value
            });
        },

        methodA: function ( event ) {
            this._trigger('dataChanged', event, {
                key: value
            });
        },

        //Respond to any changes the user makes to the option method
        _setOption: function ( key, value ) {
            switch (key) {
            case "someValue":
                //this.options.someValue = doSomethingWith( value );
                break;
            default:
                //this.options[ key ] = value;
                break;
            }

            // For UI 1.8, _setOption must be manually invoked from 
            // the base widget
            $.Widget.prototype._setOption.apply(this, arguments);
            // For UI 1.9 the _super method can be used instead
            // this._super( "_setOption", key, value );
        }
    });

})( jQuery, window, document );

//usage: $("#myelem").foo( options );

/* Some additional notes - delete this section before using the boilerplate.

 We can also self-init this widget whenever a new page in jQuery Mobile is created. jQuery Mobile's "page" plugin dispatches a "create" event when a jQuery Mobile page (found via data-role=page attr) is first initialized.

We can listen for that event (called "pagecreate" ) and run our plugin automatically whenever a new page is created.

$(document).bind("pagecreate", function (e) {
    // In here, e.target refers to the page that was created 
    // (it's the target of the pagecreate event)
    // So, we can simply find elements on this page that match a 
    // selector of our choosing, and call our plugin on them.
    // Here's how we'd call our "foo" plugin on any element with a 
    // data-role attribute of "foo":
    $(e.target).find("[data-role='foo']").foo(options);

    // Or, better yet, let's write the selector accounting for the configurable 
    // data-attribute namespace
    $(e.target).find(":jqmData(role='foo')").foo(options);
});

That's it. Now you can simply reference the script containing your widget and pagecreate binding in a page running jQuery Mobile site, and it will automatically run like any other jQM plugin.
 */</code></pre>

## RequireJS And The jQuery UI Widget Factory

RequireJS is a script loader that provides a clean solution for encapsulating application logic inside manageable modules. It’s able to load modules in the correct order (through its order plugin); it simplifies the process of combining scripts via its excellent optimizer; and it provides the means for defining module dependencies on a per-module basis.

James Burke has written a comprehensive set of tutorials on getting started with RequireJS. But what if you’re already familiar with it and would like to wrap your jQuery UI widgets or plugins in a RequireJS-compatible module wrapper?.

In the boilerplate pattern below, we demonstrate how a compatible widget can be defined that does the following:

*   Allows the definition of widget module dependencies, building on top of the previous jQuery UI boilerplate presented earlier;
*   Demonstrates one approach to passing in HTML template assets for creating templated widgets with jQuery (in conjunction with the jQuery tmpl plugin) (View the comments in `_create()`.)
*   Includes a quick tip on adjustments that you can make to your widget module if you wish to later pass it through the RequireJS optimizer

<pre><code class="language-javascript">/*!
 * jQuery UI Widget + RequireJS module boilerplate (for 1.8/9+)
 * Authors: @jrburke, @addyosmani
 * Licensed under the MIT license
 */

// Note from James:
// 
// This assumes you are using the RequireJS+jQuery file, and 
// that the following files are all in the same directory: 
//
// - require-jquery.js 
// - jquery-ui.custom.min.js (custom jQuery UI build with widget factory) 
// - templates/ 
//    - asset.html 
// - ao.myWidget.js 

// Then you can construct the widget like so: 

//ao.myWidget.js file: 
define("ao.myWidget", ["jquery", "text!templates/asset.html", "jquery-ui.custom.min","jquery.tmpl"], function ($, assetHtml) {

    // define your widget under a namespace of your choice
    // 'ao' is used here as a demonstration 
    $.widget( "ao.myWidget", { 

        // Options to be used as defaults
        options: {}, 

        // Set up widget (e.g. create element, apply theming, 
        // bind events, etc.)
        _create: function () {

            // _create will automatically run the first time 
            // this widget is called. Put the initial widget 
            // set-up code here, then you can access the element 
            // on which the widget was called via this.element.
            // The options defined above can be accessed via 
            // this.options

            //this.element.addStuff();
            //this.element.addStuff();
            //this.element.tmpl(assetHtml).appendTo(this.content); 
        },

        // Destroy an instantiated plugin and clean up modifications 
        // that the widget has made to the DOM
        destroy: function () {
            //t his.element.removeStuff();
            // For UI 1.8, destroy must be invoked from the base 
            // widget
            $.Widget.prototype.destroy.call( this );
            // For UI 1.9, define _destroy instead and don't worry 
            // about calling the base widget
        },

        methodB: function ( event ) {
            // _trigger dispatches callbacks the plugin user can 
            // subscribe to
            //signature: _trigger( "callbackName" , [eventObject], 
            // [uiObject] )
            this._trigger('methodA', event, {
                key: value
            });
        },

        methodA: function ( event ) {
            this._trigger('dataChanged', event, {
                key: value
            });
        },

        //Respond to any changes the user makes to the option method
        _setOption: function ( key, value ) {
            switch (key) {
            case "someValue":
                //this.options.someValue = doSomethingWith( value );
                break;
            default:
                //this.options[ key ] = value;
                break;
            }

            // For UI 1.8, _setOption must be manually invoked from 
            // the base widget
            $.Widget.prototype._setOption.apply( this, arguments );
            // For UI 1.9 the _super method can be used instead
            //this._super( "_setOption", key, value );
        }

        //somewhere assetHtml would be used for templating, depending 
        // on your choice.
    }); 
}); 

// If you are going to use the RequireJS optimizer to combine files 
// together, you can leave off the "ao.myWidget" argument to define: 
// define(["jquery", "text!templates/asset.html", "jquery-ui.custom.min"], …</code></pre>

### Further Reading

*   Using RequireJS with jQuery, Rebecca Murphey
*   “[Fast Modular Code With jQuery and RequireJS](https://speakerrate.com/talks/2983-fast-modular-code-with-jquery-and-requirejs),” James Burke
*   “jQuery’s Best Friends ,” Alex Sexton
*   “[Managing Dependencies With RequireJS](https://www.angrycoding.com/2011/09/managing-dependencies-with-requirejs.html),” Ruslan Matveev

## Globally And Per-Call Overridable Options (Best Options Pattern)

For our next pattern, we’ll look at an optimal approach to configuring options and defaults for your plugin. The way you’re probably familiar with defining plugin options is to pass through an object literal of defaults to <code>$.extend</code>, as demonstrated in our basic plugin boilerplate.

If, however, you’re working with a plugin with many customizable options that you would like users to be able to override either globally or on a per-call level, then you can structure things a little differently.

Instead, by referring to an options object defined within the plugin namespace explicitly (for example, <code>$fn.pluginName.options</code>) and merging this with any options passed through to the plugin when it is initially invoked, users have the option of either passing options through during plugin initialization or overriding options outside of the plugin (as demonstrated here).

<pre><code class="language-javascript">/*!
 * jQuery 'best options' plugin boilerplate
 * Author: @cowboy
 * Further changes: @addyosmani
 * Licensed under the MIT license
 */

;(function ( $, window, document, undefined ) {

    $.fn.pluginName = function ( options ) {

        // Here's a best practice for overriding 'defaults'
        // with specified options. Note how, rather than a 
        // regular defaults object being passed as the second
        // parameter, we instead refer to $.fn.pluginName.options 
        // explicitly, merging it with the options passed directly 
        // to the plugin. This allows us to override options both 
        // globally and on a per-call level.

         options = $.extend( {}, $.fn.pluginName.options, options );

        return this.each(function () {

            var elem = $(this);

        });
    };

    // Globally overriding options
    // Here are our publicly accessible default plugin options 
    // that are available in case the user doesn't pass in all 
    // of the values expected. The user is given a default
    // experience but can also override the values as necessary.
    // eg. $fn.pluginName.key ='otherval';

    $.fn.pluginName.options = {

        key: "value",
        myMethod: function ( elem, param ) {

        }
    };

})( jQuery, window, document );</code></pre>

### Further Reading

*   [jQuery Pluginization](https://benalman.com/talks/jquery-pluginization.html) and the [accompanying gist](https://gist.github.com/472783/e8bf47340413129a8abe5fac55c83336efb5d4e1), Ben Alman

## A Highly Configurable And Mutable Plugin

Like Alex Sexton’s pattern, the following logic for our plugin isn’t nested in a jQuery plugin itself. We instead define our plugin’s logic using a constructor and an object literal defined on its prototype, using jQuery for the actual instantiation of the plugin object.

Customization is taken to the next level by employing two little tricks, one of which you’ve seen in previous patterns:

*   Options can be overridden both globally and per collection of elements;
*   Options can be customized on a **per-element** level through HTML5 data attributes (as shown below). This facilitates plugin behavior that can be applied to a collection of elements but then customized inline without the need to instantiate each element with a different default value.

You don’t see the latter option in the wild too often, but it can be a significantly cleaner solution (as long as you don’t mind the inline approach). If you’re wondering where this could be useful, imagine writing a draggable plugin for a large set of elements. You could go about customizing their options like this:

<pre><code class="language-javascript">javascript
$('.item-a').draggable({'defaultPosition':'top-left'});
$('.item-b').draggable({'defaultPosition':'bottom-right'});
$('.item-c').draggable({'defaultPosition':'bottom-left'});
//etc</code></pre>

But using our patterns inline approach, the following would be possible:

<pre><code class="language-javascript">javascript
$('.items').draggable();</code></pre>

<pre><code class="language-javascript">html
&lt;li class="item" data-plugin-options='{"defaultPosition":"top-left"}'&gt;&lt;/div&gt;
&lt;li class="item" data-plugin-options='{"defaultPosition":"bottom-left"}'&gt;&lt;/div&gt;</code></pre>

And so on. You may well have a preference for one of these approaches, but it is another potentially useful pattern to be aware of.

<pre><code class="language-javascript">/*
 * 'Highly configurable' mutable plugin boilerplate
 * Author: @markdalgleish
 * Further changes, comments: @addyosmani
 * Licensed under the MIT license
 */

// Note that with this pattern, as per Alex Sexton's, the plugin logic
// hasn't been nested in a jQuery plugin. Instead, we just use
// jQuery for its instantiation.

;(function( $, window, document, undefined ){

  // our plugin constructor
  var Plugin = function( elem, options ){
      this.elem = elem;
      this.$elem = $(elem);
      this.options = options;

      // This next line takes advantage of HTML5 data attributes
      // to support customization of the plugin on a per-element
      // basis. For example,
      // &lt;div class=item' data-plugin-options='{"message":"Goodbye World!"}'&gt;&lt;/div&gt;
      this.metadata = this.$elem.data( 'plugin-options' );
    };

  // the plugin prototype
  Plugin.prototype = {
    defaults: {
      message: 'Hello world!'
    },

    init: function() {
      // Introduce defaults that can be extended either 
      // globally or using an object literal.

      this.config = $.extend({}, this.defaults, this.options, 
      this.metadata);

      // Sample usage:
      // Set the message per instance:
      // $('#elem').plugin({ message: 'Goodbye World!'});
      // or
      // var p = new Plugin(document.getElementById('elem'), 
      // { message: 'Goodbye World!'}).init()
      // or, set the global default message:
      // Plugin.defaults.message = 'Goodbye World!'

      this.sampleMethod();
      return this;
    },

    sampleMethod: function() {
      // eg. show the currently configured message
      // console.log(this.config.message);
    }
  }

  Plugin.defaults = Plugin.prototype.defaults;

  $.fn.plugin = function(options) {
    return this.each(function() {
      new Plugin(this, options).init();
    });
  };

  //optional: window.Plugin = Plugin;

})( jQuery, window , document );</code></pre>

### Further Reading

*   “[Creating Highly Configurable jQuery Plugins](https://markdalgleish.com/2011/05/creating-highly-configurable-jquery-plugins/),” Mark Dalgleish
*   “[Writing Highly Configurable jQuery Plugins, Part 2](https://markdalgleish.com/2011/09/html5data-creating-highly-configurable-jquery-plugins-part-2/),” Mark Dalgleish

## AMD- And CommonJS-Compatible Modules

While many of the plugin and widget patterns presented above are acceptable for general use, they aren’t without their caveats. Some require jQuery or the jQuery UI Widget Factory to be present in order to function, while only a few could be easily adapted to work well as globally compatible modules both client-side and in other environments.

For this reason, a number of developers, including me, <a href="https://cdnjs.com" rel="nofollow">CDNjs</a> maintainer <a href="https://github.com/thomasdavis" rel="nofollow">Thomas Davis</a> and <a href="https://github.com/rpflorence" rel="nofollow">RP Florence</a>, have been looking at both the <a href="https://github.com/amdjs/amdjs-api/wiki/AMD" rel="nofollow">AMD</a> (Asynchronous Module Definition) and <a href="https://wiki.commonjs.org/wiki/Modules" rel="nofollow">CommonJS</a> module specifications in the hopes of extending boilerplate plugin patterns to cleanly work with packages and dependencies. <a href="https://twitter.com/unscriptable" rel="nofollow">John Hann</a> and <a href="https://gist.github.com/1251221" rel="nofollow">Kit Cambridge</a> have also explored work in this area.</p>

### AMD

The AMD module format (a specification for defining modules where both the module and dependencies can be asynchronously loaded) has a number of distinct advantages, including being both asynchronous and highly flexible by nature, thus removing the tight coupling one commonly finds between code and module identity. It’s considered a reliable stepping stone to the <a href="https://wiki.ecmascript.org/doku.php?id=harmony:modules" rel="nofollow">module system</a> proposed for ES Harmony.

When working with anonymous modules, the idea of a module’s identity is DRY, making it trivial to avoid duplication of file names and code. Because the code is more portable, it can be easily moved to other locations without needing to alter the code itself. Developers can also run the same code in multiple environments just by using an AMD optimizer that works with a CommonJS environment, such as <a href="https://github.com/jrburke/r.js/" rel="nofollow">r.js</a>.

With AMD, the two key concepts you need to be aware of are the <code>require</code> method and the <code>define</code> method, which facilitate module definition and dependency loading. The <code>define</code> method is used to define named or unnamed modules based on the specification, using the following signature:

<pre><code class="language-javascript">define(module_id /*optional*/, [dependencies], definition function /*function for instantiating the module or object*/);</code></pre>

As you can tell from the inline comments, the module’s ID is an optional argument that is typically required only when non-AMD concatenation tools are being used (it could be useful in other edge cases, too). One of the benefits of opting not to use module IDs is having the flexibility to move your module around the file system without needing to change its ID. The module’s ID is equivalent to folder paths in simple packages and when not used in packages.

The dependencies argument represents an array of dependencies that are required by the module you are defining, and the third argument (factory) is a function that’s executed to instantiate your module. A barebones module could be defined as follows:

<pre><code class="language-javascript">// Note: here, a module ID (myModule) is used for demonstration
// purposes only

define('myModule', ['foo', 'bar'], function ( foo, bar ) {
    // return a value that defines the module export
    // (i.e. the functionality we want to expose for consumption)
    return function () {};
});

// A more useful example, however, might be:
define('myModule', ['math', 'graph'], function ( math, graph ) {
    return {
            plot: function(x, y){
                    return graph.drawPie(math.randomGrid(x,y));
            }
    };
});</code></pre>

The <code>require</code> method, on the other hand, is typically used to load code in a top-level JavaScript file or in a module should you wish to dynamically fetch dependencies. Here is an example of its usage:

<pre><code class="language-javascript">// Here, the 'exports' from the two modules loaded are passed as
// function arguments to the callback

require(['foo', 'bar'], function ( foo, bar ) {
        // rest of your code here
});

// And here's an AMD-example that shows dynamically loaded
// dependencies

define(function ( require ) {
    var isReady = false, foobar;

    require(['foo', 'bar'], function (foo, bar) {
        isReady = true;
        foobar = foo() + bar();
    });

    // We can still return a module
    return {
        isReady: isReady,
        foobar: foobar
    };
});</code></pre>

The above are trivial examples of just how useful AMD modules can be, but they should provide a foundation that helps you understand how they work. Many big visible applications and companies currently use AMD modules as a part of their architecture, including <a href="https://www.ibm.com" rel="nofollow">IBM</a> and the <a href="https://www.bbc.co.uk/iplayer/" rel="nofollow">BBC iPlayer</a>. The specification has been discussed for well over a year in both the Dojo and CommonJS communities, so it’s had time to evolve and improve. For more reasons on why many developers are opting to use AMD modules in their applications, you may be interested in James Burke’s article “<a href="https://tagneto.blogspot.com/2011/04/on-inventing-js-module-formats-and.html" rel="nofollow">On Inventing JS Module Formats and Script Loaders</a>.”

Shortly, we’ll look at writing globally compatible modules that work with AMD and other module formats and environments, something that offers even more power. Before that, we need to briefly discuss a related module format, one with a specification by CommonJS.</p>

### CommonJS

In case you’re not familiar with it, <a href="https://www.commonjs.org/" rel="nofollow">CommonJS</a> is a volunteer working group that designs, prototypes and standardizes JavaScript APIs. To date, it’s attempted to ratify standards for <a href="https://www.commonjs.org/specs/modules/1.0/" rel="nofollow">modules</a> and <a href="https://wiki.commonjs.org/wiki/Packages/1.0" rel="nofollow">packages</a>. The CommonJS module proposal specifies a simple API for declaring modules server-side; but, as John Hann correctly states, there are really only two ways to use CommonJS modules in the browser: either wrap them or wrap them.

What this means is that we can either have the browser wrap modules (which can be a slow process) or at build time (which can be fast to execute in the browser but requires a build step).

Some developers, however, feel that CommonJS is better suited to server-side development, which is one reason for the current disagreement over which format should be used as the de facto standard in the pre-Harmony age moving forward. One argument against CommonJS is that many CommonJS APIs address server-oriented features that one would simply not be able to implement at the browser level in JavaScript; for example, <code>io&gt;</code>, <code>system</code> and <code>js</code> could be considered unimplementable by the nature of their functionality.

That said, knowing how to structure CommonJS modules is useful so that we can better appreciate how they fit in when defining modules that might be used everywhere. Modules that have applications on both the client and server side include validation, conversion and templating engines. The way some developers choose which format to use is to opt for CommonJS when a module can be used in a server-side environment and to opt for AMD otherwise.

Because AMD modules are capable of using plugins and can define more granular things such as constructors and functions, this makes sense. CommonJS modules are able to define objects that are tedious to work with only if you’re trying to obtain constructors from them.

From a structural perspective, a CommonJS module is a reusable piece of JavaScript that exports specific objects made available to any dependent code; there are typically no function wrappers around such modules. Plenty of great tutorials on implementing CommonJS modules are out there, but at a high level, the modules basically contain two main parts: a variable named <code>exports</code>, which contains the objects that a module makes available to other modules, and a <code>require</code> function, which modules can use to import the exports of other modules.

<pre><code class="language-javascript">// A very basic module named 'foobar'
function foobar(){
        this.foo = function(){
                console.log('Hello foo');
        }

        this.bar = function(){
                console.log('Hello bar');
        }
}

exports.foobar = foobar;

// An application using 'foobar'

// Access the module relative to the path
// where both usage and module files exist
// in the same directory

var foobar = require('./foobar').foobar,
    test   = new foobar.foo();

test.bar(); // 'Hello bar'</code></pre>

There are a number of great JavaScript libraries for handling module loading in AMD and CommonJS formats, but my preference is <a href="https://requirejs.org" rel="nofollow">RequireJS</a> (<a href="https://github.com/unscriptable/curl" rel="nofollow">curl.js</a> is also quite reliable). Complete tutorials on these tools are beyond the scope of this article, but I recommend John Hann’s post “<a href="https://unscriptable.com/index.php/2011/03/30/curl-js-yet-another-amd-loader/" rel="nofollow">curl.js: Yet Another AMD Loader</a>,” and James Burke’s post “<a href="https://msdn.microsoft.com/en-us/scriptjunkie/ff943568" rel="nofollow">
LABjs and RequireJS: Loading JavaScript Resources the Fun Way</a>.”

With what we’ve covered so far, wouldn’t it be great if we could define and load plugin modules compatible with AMD, CommonJS and other standards that are also compatible with different environments (client-side, server-side and beyond)? Our work on AMD and UMD (Universal Module Definition) plugins and widgets is still at a very early stage, but we’re hoping to develop solutions that can do just that.

One such pattern we’re working on at the moment appears below, which has the following features:

*   A core/base plugin is loaded into a `$.core` namespace, which can then be easily extended using plugin extensions via the namespacing pattern. Plugins loaded via script tags automatically populate a `plugin` namespace under `core` (i.e. `$.core.plugin.methodName()`).
*   The pattern can be quite nice to work with because plugin extensions can access properties and methods defined in the base or, with a little tweaking, override default behavior so that it can be extended to do more.
*   A loader isn’t necessarily required at all to make this pattern fully function.

<strong>usage.html</strong>

<pre><code class="language-javascript">&lt;script type="text/javascript" src="https://code.jquery.com/jquery-1.6.4.min.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="pluginCore.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="pluginExtension.js"&gt;&lt;/script&gt;

&lt;script type="text/javascript"&gt;

$(function(){

    // Our plugin 'core' is exposed under a core namespace in 
    // this example, which we first cache
    var core = $.core;

    // Then use use some of the built-in core functionality to 
    // highlight all divs in the page yellow
    core.highlightAll();

    // Access the plugins (extensions) loaded into the 'plugin'
    // namespace of our core module:

    // Set the first div in the page to have a green background.
    core.plugin.setGreen("div:first");
    // Here we're making use of the core's 'highlight' method
    // under the hood from a plugin loaded in after it

    // Set the last div to the 'errorColor' property defined in 
    // our core module/plugin. If you review the code further down,
    // you'll see how easy it is to consume properties and methods
    // between the core and other plugins
    core.plugin.setRed('div:last');
});

&lt;/script&gt;</code></pre>

<strong>pluginCore.js</strong>

<pre><code class="language-javascript">// Module/Plugin core
// Note: the wrapper code you see around the module is what enables
// us to support multiple module formats and specifications by 
// mapping the arguments defined to what a specific format expects
// to be present. Our actual module functionality is defined lower 
// down, where a named module and exports are demonstrated. 
// 
// Note that dependencies can just as easily be declared if required
// and should work as demonstrated earlier with the AMD module examples.

(function ( name, definition ){
  var theModule = definition(),
      // this is considered "safe":
      hasDefine = typeof define === 'function' &amp;&amp; define.amd,
      // hasDefine = typeof define === 'function',
      hasExports = typeof module !== 'undefined' &amp;&amp; module.exports;

  if ( hasDefine ){ // AMD Module
    define(theModule);
  } else if ( hasExports ) { // Node.js Module
    module.exports = theModule;
  } else { // Assign to common namespaces or simply the global object (window)
    (this.jQuery || this.ender || this.$ || this)[name] = theModule;
  }
})( 'core', function () {
    var module = this;
    module.plugins = [];
    module.highlightColor = "yellow";
    module.errorColor = "red";

  // define the core module here and return the public API

  // This is the highlight method used by the core highlightAll()
  // method and all of the plugins highlighting elements different
  // colors
  module.highlight = function(el,strColor){
    if(this.jQuery){
      jQuery(el).css('background', strColor);
    }
  }
  return {
      highlightAll:function(){
        module.highlight('div', module.highlightColor);
      }
  };

});</code></pre>

<strong>pluginExtension.js</strong>

<pre><code class="language-javascript">// Extension to module core

(function ( name, definition ) {
    var theModule = definition(),
        hasDefine = typeof define === 'function',
        hasExports = typeof module !== 'undefined' &amp;&amp; module.exports;

    if ( hasDefine ) { // AMD Module
        define(theModule);
    } else if ( hasExports ) { // Node.js Module
        module.exports = theModule;
    } else { // Assign to common namespaces or simply the global object (window)

        // account for for flat-file/global module extensions
        var obj = null;
        var namespaces = name.split(".");
        var scope = (this.jQuery || this.ender || this.$ || this);
        for (var i = 0; i &lt; namespaces.length; i++) {
            var packageName = namespaces[i];
            if (obj &amp;&amp; i == namespaces.length - 1) {
                obj[packageName] = theModule;
            } else if (typeof scope[packageName] === "undefined") {
                scope[packageName] = {};
            }
            obj = scope[packageName];
        }

    }
})('core.plugin', function () {

    // Define your module here and return the public API.
    // This code could be easily adapted with the core to
    // allow for methods that overwrite and extend core functionality
    // in order to expand the highlight method to do more if you wish.
    return {
        setGreen: function ( el ) {
            highlight(el, 'green');
        },
        setRed: function ( el ) {
            highlight(el, errorColor);
        }
    };

});</code></pre>

While this is beyond the scope of this article, you may have noticed that different types of <code>require</code> methods were mentioned when we discussed AMD and CommonJS.

The concern with a similar naming convention is, of course, confusion, and the community is currently split on the merits of a global <code>require</code> function. John Hann’s suggestion here is that rather than call it <code>require</code>, which would probably fail to inform users of the difference between a global and inner <code>require</code>, renaming the global loader method something else might make more sense (such as the name of the library). For this reason, curl.js uses <code>curl</code>, and RequireJS uses <code>requirejs</code>.

This is probably a bigger discussion for another day, but I hope this brief walkthrough of both module types has increased your awareness of these formats and has encouraged you to further explore and experiment with them in your apps.</p>

### Further Reading

*   “[Using AMD Loaders to Write and Manage Modular JavaScript](https://unscriptable.com/code/Using-AMD-loaders/#0),” John Hann
*   “Demystifying CommonJS Modules,” Alex Young
*   “[AMD Module Patterns: Singleton](https://unscriptable.com/index.php/2011/09/22/amd-module-patterns-singleton/),” John Hann
*   Current discussion thread about AMD- and UMD-style modules for jQuery plugins, GitHub
*   “[Run-Anywhere JavaScript Modules Boilerplate Code](https://www.sitepen.com/blog/2010/09/30/run-anywhere-javascript-modules-boilerplate-code/),” Kris Zyp
*   “[Standards And Proposals for JavaScript Modules And jQuery](https://tagneto.blogspot.com/2010/12/standards-and-proposals-for-javascript.html),” James Burke

## What Makes A Good jQuery Plugin?

At the end of the day, patterns are just one aspect of plugin development. And before we wrap up, here are my criteria for selecting third-party plugins, which will hopefully help developers write them.

<strong>Quality</strong>
Do your best to adhere to best practices with both the JavaScript and jQuery that you write. Are your solutions optimal? Do they follow the <a href="https://docs.jquery.com/JQuery_Core_Style_Guidelines" rel="nofollow">jQuery core style guidelines</a>? If not, is your code at least relatively clean and readable?

<strong>Compatibility</strong>
Which versions of jQuery is your plugin compatible with? Have you tested it with the latest builds? If the plugin was written before jQuery 1.6, then it might have issues with attributes, because the way we approach them changed with that release. New versions of jQuery offer improvements and opportunities for the jQuery project to improve on what the core library offers. With this comes occasional breakages (mainly in major releases) as we move towards a better way of doing things. I’d like to see plugin authors update their code when necessary or, at a minimum, test their plugins with new versions to make sure everything works as expected.

<strong>Reliability</strong>
Your plugin should come with its own set of unit tests. Not only do these prove your plugin actually works, but they can also improve the design without breaking it for end users. I consider unit tests essential for any serious jQuery plugin that is meant for a production environment, and they’re not that hard to write. For an excellent guide to automated JavaScript testing with QUnit, you may be interested in “<a href="https://msdn.microsoft.com/en-us/scriptjunkie/gg749824" rel="nofollow">Automating JavaScript Testing With QUnit</a>,” by <a href="https://bassistance.de/" rel="nofollow">Jorn Zaefferer</a>.

<strong>Performance</strong>
If the plugin needs to perform tasks that require a lot of computing power or that heavily manipulates the DOM, then you should follow best practices that minimize this. Use <a href="https://web.archive.org/web/20160131082743/https://jsperf.com:80/" rel="nofollow">jsPerf.com</a> to test segments of your code so that you’re aware of how well it performs in different browsers before releasing the plugin.

<strong>Documentation</strong>
If you intend for other developers to use your plugin, ensure that it’s well documented. Document your API. What methods and options does the plugin support? Does it have any gotchas that users need to be aware of? If users cannot figure out how to use your plugin, they’ll likely look for an alternative. Also, do your best to comment the code. This is by far the best gift you could give to other developers. If someone feels they can navigate your code base well enough to fork it or improve it, then you’ve done a good job.

<strong>Likelihood of maintenance</strong>
When releasing a plugin, estimate how much time you’ll have to devote to maintenance and support. We all love to share our plugins with the community, but you need to set expectations for your ability to answer questions, address issues and make improvements. This can be done simply by stating your intentions for maintenance in the <em>README</em> file, and let users decide whether to make fixes themselves.</p>

### Conclusion

Today, we’ve explored several time-saving design patterns and best practices that can be employed to improve your plugin development process. Some are better suited to certain use cases than others, but I hope that the code comments that discuss the ins and outs of these variations on popular plugins and widgets were useful.

Remember, when selecting a pattern, be practical. Don’t use a plugin pattern just for the sake of it; rather, spend some time understanding the underlying structure, and establish how well it solves your problem or fits the component you’re trying to build. Choose the pattern that best suits your needs.

And that’s it. If there's a particular pattern or approach you prefer taking to writing plugins which you feel would benefit others (which hasn't been covered), please feel free to stick it in a <a href="https://gist.github.com" rel="nofollow">gist</a> and share it in the comments below. I'm sure it would be appreciated.

Until next time, happy coding!

<em>Thanks to John Hann, Julian Aubourg, Andree Hanson and everyone else who reviewed this post for their comments and feedback.</em>

<em>(al) (il)</em>


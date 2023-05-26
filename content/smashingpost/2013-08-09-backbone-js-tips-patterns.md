---
title: Backbone.js Tips And Patterns
slug: backbone-js-tips-patterns
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4e74d1c5-7d80-4c09-b801-fab59c92ad2b/illu-backbone.jpg'
date: 2013-08-09T08:30:56.000Z
author: phillip-whisenhunt
description: >-
  Backbone.js is a popular open-source JavaScript “MV” framework that has
  gained significant traction since its first release a little over three years
  ago. Although Backbone.js provides structure to JavaScript applications, it
  leaves a lot of design patterns and decisions up to the developer, for better
  or worse, and developers run into many common problems when they first begin
  developing in Backbone.js.
categories:
  - Coding
  - Frameworks
  - JavaScript
---
<a title="Backbone.js" href="https://backbonejs.org/">Backbone.js</a> is a popular open-source <strong>JavaScript “MV*” framework</strong> that has gained significant traction since its first release a little over three years ago. Although Backbone.js provides structure to JavaScript applications, it leaves a lot of design patterns and decisions up to the developer, for better or worse, and developers run into many common problems when they first begin developing in Backbone.js.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Journey Through The JavaScript MVC Jungle</span>](https://www.smashingmagazine.com/2012/07/journey-through-the-javascript-mvc-jungle/)
*   [<span class="headline">A Thorough Introduction To Backbone.Marionette</span>](https://www.smashingmagazine.com/2013/02/introduction-backbone-marionette/)
*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)
*   [Get Up And Running With Grunt](https://www.smashingmagazine.com/2013/10/get-up-running-grunt/)

Therefore, in this article, we’ll explore different design patterns that you can use in your Backbone.js applications, and we’ll look at many of the common gotchas that trip up developers.

<a title="Austin, Texas in autumn by rutlo, on Flickr" href="https://www.flickr.com/photos/rutlo/5220159766/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2417cf62-6c84-4f8d-9ff7-78e37c6e1f3e/a5220159766-c2f06fa1dd.jpg" alt="Austin, Texas in autumn" width="500" height="333" /></a><br>
<em>Applications, like buildings, are best built following known patterns. (Image: <a title="Austin, Texas in autumn by rutlo, on Flickr" href="https://www.flickr.com/photos/rutlo/5220159766/">Matthew Rutledge</a>)</em>

{{% feature-panel %}}

## Perform Deep Copies Of Objects

JavaScript treats all primitive-type variables as pass-by-value. So, the value of a variable is passed when the variable is referenced.

<pre><code class="language-javascript">
var helloWorld = “Hello World”;
var helloWorldCopy = helloWorld;
</code></pre>

For example, the code above will set <code>helloWorldCopy</code> equal to the value of <code>helloWorld</code>. So, any modification to <code>helloWorldCopy</code> will not modify <code>helloWorld</code>, since it is a copy. JavaScript <strong>treats all non-primitive type variables as pass-by-reference</strong>, meaning that JavaScript will pass a reference of the memory address of the variable when the variable is referenced.

<pre><code class="language-javascript">
var helloWorld = {
    ‘hello’: ‘world’
}
var helloWorldCopy = helloWorld;
</code></pre>

For example, the code above will set <code>helloWorldCopy</code> equal to the reference of <code>helloWorld</code>, and, as you might guess, any modifications to <code>helloWorldCopy</code> would directly manipulate <code>helloWorld</code>. If you’d like to have a copy of the <code>helloWorld</code>, you will have to create a copy of the object.

You’re probably wondering, “Why is he explaining all of this pass-by-reference stuff?” Well, <strong>Backbone.js does not copy objects</strong>, which means that if you <code>.get()</code> an object from a model, any modifications to that object will directly manipulate the object! Let’s look at an example to illustrate where this can become an issue. Let’s say you have a <code>Person</code> model like the following:

<pre><code class="language-javascript">
var Person = Backbone.Model.extend({
   defaults: {
        'name': 'John Doe',
        'address': {
            'street': '1st Street'
            'city': 'Austin',
            'state': 'TX'
            'zipCode': 78701
        }
   }
});
</code></pre>

And let’s say you create a new <code>person</code> object:

<pre><code class="language-javascript">
var person = new Person({
    'name': 'Phillip W'
});
</code></pre>

Now, let’s manipulate some of the attributes of the new <code>person</code> object:

<pre><code class="language-javascript">
person.set('name', 'Phillip W.', { validate: true });
</code></pre>

The code above successfully manipulates the <code>name</code> attribute of the <code>person</code> object. Now let’s try to manipulate the address of the <code>person</code> object. However, before doing so, let’s add some validation for the address.

<pre><code class="language-javascript">
var Person = Backbone.Model.extend({
    validate: function(attributes) {

        if(isNaN(attributes.address.zipCode)) return "Address ZIP code must be a number!";
    },

    defaults: {
        'name': 'John Doe',
        'address': {
            'street': '1st Street'
            'city': 'Austin',
            'state': 'TX'
            'zipCode': 78701
        }
    }
});
</code></pre>

Now, let’s attempt to manipulate the address with an incorrect ZIP code.

<pre><code class="language-javascript">
var address = person.get('address');
address.zipCode = 'Hello World';
// Raises an error since the ZIP code is invalid
person.set('address', address, { validate: true });
console.log(person.get('address'));
/* Prints an object with these properties.
{
    'street': '1st Street'
    'city': 'Austin',
    'state': 'TX'
    'zipCode': 'Hello World'
}
*/
</code></pre>

How can this be? Our validation has raised an error! Why are the attributes still changed? As mentioned, <strong>Backbone.js does not copy model attributes</strong>; it simply returns whatever you’re asking for. So, as you might guess, if you ask for an object, you will get a reference to that object, and any manipulation to the object will directly manipulate the actual object in the model. This can quickly lead you down a very dark rabbit hole that can take you hours of debugging to diagnose.

<a title="Rabbit hole by david.orban, on Flickr" href="https://www.flickr.com/photos/davidorban/4004632688/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2559178d-8492-4fb1-bfac-063f22f25aa7/a4004632688-1392c1827c.jpg" alt="Rabbit hole" width="500" height="387" /></a><br>
<em>Performing a deep copy of model objects can save you from going down a rabbit hole of debugging. (Image: <a title="Rabbit hole by david.orban, on Flickr" href="https://www.flickr.com/photos/davidorban/4004632688/">David Orban</a>)</em>

This issue catches developers who are new to Backbone.js and even seasoned JavaScript developers off guard. This issue has been heavily discussed <a href="https://github.com/documentcloud/backbone/issues/2315">in the GitHub issues</a> section of Backbone.js. As <a title="Jeremy Ashkenas" href="https://ashkenas.com/">Jeremy Ashkenas</a> points out there, <strong>performing a deep copy is a very difficult problem to solve</strong>, and it can become an expensive operation for very large, deep objects.

Luckily, jQuery provides an implementation of deep copying, <a title="jQuery .extend" href="https://api.jquery.com/jQuery.extend/"><code>$.extend</code></a>. As an aside, <a title="Underscore.js" href="https://underscorejs.org/">Underscore.js</a>, a dependency of Backbone.js, provides the <a title="Underscore.js .extend" href="https://underscorejs.org/#extend"><code>_.extend</code></a> function, but I would avoid using it because it does not perform a deep copy. <a href="https://lodash.com/">Lo-Dash</a>, a forked and optimized version of Underscore.js, provides a <a href="https://lodash.com/docs#clone"><code>_.clone</code></a> function with the option to perform a deep copy. However, I use <a title="jQuery .extend" href="https://api.jquery.com/jQuery.extend/"><code>$.extend</code></a> to perform a deep copy of any object that I <code>.get()</code> from a model using the following syntax. Remember to pass <code>true</code>, so that it performs a deep copy of the object.

<pre><code class="language-javascript">
var address = $.extend(true, {}, person.address);
</code></pre>

We now have an exact copy of the <code>address</code> object, and we can modify it to our heart’s content without worrying about modifying the actual model. You should be aware that this pattern works for the above example because all of the members of the address object are immutable(numbers, strings, etc.), and that while the above example works you should use caution when deep copying objects that contain objects. You should also know that there is a small performance hit from performing a deep copy, but I have never seen this cause noticeable problems. However, if you’re deep copying massive objects, or thousands of objects all at once, you’ll likely want to do some performance profiling. This leads us directly to the next pattern.</p>

## Create Facades To Objects

In the real world, requirements change often, and so does the JavaScript Object Notation (or <a title="JSON" href="https://www.json.org/">JSON</a>) returned by the endpoints that your models and collections hit. This can become a really big pain point in your code base if your view is tightly coupled to the underlying data model. Therefore, I <strong>create getters and setters for all objects</strong>.

The pros of this pattern are many. If any of the underlying data structures change, then the view layers shouldn’t have to update that much; you will have one point of access to the data, so you are less likely to forget to do a deep copy, and your code will be more maintainable and much easier to debug. The downside is that this pattern can cause a bit of bloat in your models or collections.

Let’s look at an example to illustrate this pattern. Imagine we have a <code>Hotel</code> model that contains rooms and the currently available rooms, and that we want to be able to retrieve rooms by bed size.

<pre><code class="language-javascript">
var Hotel = Backbone.Model.extend({
    defaults: {
        "availableRooms": ["a"],
        "rooms": {
            "a": {
                "size": 1200,
                "bed": "queen"
            },
            "b": {
                "size": 900,
                "bed": "twin"
            },
            "c": {
                "size": 1100,
                "bed": "twin"
            }
        },

        getRooms: function() {
            $.extend(true, {}, this.get("rooms"));
        },

        getRoomsByBed: function(bed) {
            return _.where(this.getRooms(), { "bed": bed });
        }
    }
});
</code></pre>

Now let’s imagine that tomorrow you will be releasing your code, and you find out that the endpoint developers forgot to tell you that the data structure of rooms has changed from an object to an array. Your code now looks like the following.

<pre><code class="language-javascript">
var Hotel = Backbone.Model.extend({
    defaults: {
        "availableRooms": ["a"],
        "rooms": [
            {
                "name": "a",
                "size": 1200,
                "bed": "queen"
            },
            {
                "name": "b",
                "size": 900,
                "bed": "twin"
            },
            {
                "name": "c",
                "size": 1100,
                "bed": "twin"
            }
        ],

        getRooms: function() {
            var rooms = $.extend(true, {}, this.get("rooms")),
             newRooms = {};

            // transform rooms from an array back into an object
            _.each(rooms, function(room) {
                newRooms[room.name] = {
                    "size": room.size,
                    "bed": room.bed
                }
            });
        },

        getRoomsByBed: function(bed) {
            return _.where(this.getRooms(), { "bed": bed });
        }
    }
});
</code></pre>

We updated only one function in order to transform the <code>Hotel</code> structure into the structure that the rest of our application expects, and our entire app still behaves as expected. If we didn’t have a getter here, we might potentially have to update each point of access to <code>rooms</code>. Ideally, you would want to update all of your functions to work with the new data structure, but if you’re pressed for time and have to release, this pattern can save you.

As an aside, this pattern can be thought of as both a <a title="Facade Design Pattern" href="https://addyosmani.com/resources/essentialjsdesignpatterns/book/#facadepatternjavascript">facade design pattern</a>, because it hides the complexity of creating a copy of your objects, or a <a title="Bridge Design Pattern" href="https://en.wikipedia.org/wiki/Bridge_pattern">bridge design pattern</a>, because it can be used to transform data into what is expected. A good rule of thumb is to <strong>use getters and setters on anything that is an object</strong>.

## Store Data Not Persisted By The Server

Although Backbone.js prescribes that models and collections map to <a title="Representational State Transfer" href="https://en.wikipedia.org/wiki/Representational_state_transfer">representational state transfer</a> (or REST-ful) endpoints, you will sometimes find that you want to store data in your models or collections that is not persisted on the server. Many other articles about Backbone.js, such as “<a title="Backbone.js Tips: Lessons from the trenches." href="https://supportbee.com/devblog/2011/07/29/backbone-js-tips-lessons-from-the-trenches/">Backbone.js Tips: Lessons From the Trenches</a>” by Prateek Dayal of SupportBee, describe this pattern. Let’s look at a quick example to help explain where this might come in handy. Suppose you have a <code>ul</code> list.

<pre><code class="language-markup">
&lt;ul&gt;
  &lt;li&gt;&lt;a href="#" data-id="1"&gt;One&lt;/a&gt;&lt;/li&gt;
  &lt;li&gt;&lt;a href="#" data-id="2"&gt;Two&lt;/a&gt;&lt;/li&gt;
    . . .
  &lt;li&gt;&lt;a href="#" data-id="n"&gt;n&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

Where <code>n</code> is 200 and when the user clicks on one of the items, that item becomes selected and is visualized to the user as the chosen item by a <code>selected</code> class being added. One approach to this would be the following:

<pre><code class="language-javascript">
var Model = Backbone.Model.extend({
    defaults: {
        items: [
            {
                "name": "One",
                "id": 1
            },
            {
                "name": "Two",
                "id": 2
            },
            {
                "name": "Three",
                "id": 3
            }
        ]
    }
});

var View = Backbone.View.extend({
    template: _.template($('#list-template').html()),

    events: {
        "#items li a": "setSelectedItem"
    },

    render: function() {
        $(this.el).html(this.template(this.model.toJSON()));
    },

    setSelectedItem: function(event) {
        var selectedItem = $(event.currentTarget);
        // Set all of the items to not have the selected class
        $('#items li a').removeClass('selected');
        selectedItem.addClass('selected');
        return false;
    }
});
</code></pre>

<pre><code class="language-markup">
&lt;script id="list-template" type="template"&gt;
&lt;ul id="items"&gt;
        &lt;% for(i = items.length - 1; i &gt;= 0; i--) { %&gt;
  &lt;li&gt;
                &lt;a href="#" data-id="&lt;%= item[i].id %&gt;"&gt;&lt;%= item[i].name %&gt;&lt;/a&gt;&lt;/li&gt;
&lt;% } %&gt;&lt;/ul&gt;
&lt;/script&gt;
</code></pre>

Now let’s say we want to figure out which item has been selected. One way would be to traverse the list. But if the list is really long, this could become quite an expensive task. Therefore, <strong>let’s also store which item is selected when the user clicks on a list item</strong>.

<pre><code class="language-javascript">
var View = Backbone.View.extend({
    initialize: function(options) {
        // Re-render when the model changes
        this.model.on('change:items', this.render, this);
    },

    template: _.template($('#list-template').html()),

    events: {
        "#items li a": "setSelectedItem"
    },

    render: function() {
        $(this.el).html(this.template(this.model.toJSON()));
    },

    setSelectedItem: function(event) {
        var selectedItem = $(event.currentTarget);
        // Set all of the items to not have the selected class
        $('#items li a').removeClass('selected');
        selectedItem.addClass('selected');
        // Store a reference to what item was selected
        this.selectedItemId = selectedItem.data('id'));
        return false;
    }
});
</code></pre>

Now we can now easily determine which item has been selected, and we don’t have to traverse the <a title="Document Object Model" href="https://en.wikipedia.org/wiki/Document_Object_Model">Document Object Model</a> (DOM). This pattern is extremely useful for storing extraneous data that you might want to keep track of; keep in mind also that you can create models and collections that don’t necessarily have endpoints associated with them to store extraneous view data.

The downsides to this pattern are that if you store extraneous data in your models or collections, they won’t really follow a RESTful architecture since they won’t map perfectly to a Web resource; also, this pattern can cause a bit of bloat in your objects; and it can cause a bit of pain when saving your models if your endpoint strictly accepts only the JSON it expects.

You may be asking yourself, "How do I determine if I should put the extra data in the view or the model?". If the extra attributes you’re adding are centered around rendering, such as the height of a container, they should probably be added to the view. If the attributes have anything to do with the underlying data model, then you may want to push that into the model. For example, if the above example were more flushed out and for some reason I only wanted users to be able to select a specific range of items from the list of items returned by the model, I would likely push that logic into the model. In short, as most things go, it really depends on the situation. You can argue for keeping your models truly faithful to REST and you can argue that you should keep your views as dumb as possible and push as much logic into your models.</p>

## Render Parts Of Views Instead Of Entire Views

When you first begin developing Backbone.js applications, your views will typically be structured something like this:

<pre><code class="language-javascript">
var View = Backbone.View.extend({
    initialize: function(options) {
        this.model.on('change', this.render, this);
    },

    template: _.template($(‘#template’).html()),

    render: function() {
        this.$el.html(template(this.model.toJSON());
        $(‘#a’, this.$el).html(this.model.get(‘a’));
        $(‘#b’, this.$el).html(this.model.get(‘b’));
    }
});
</code></pre>

Here, any change to your model will trigger a complete re-rendering of the view. I was a practitioner of this pattern when I first began developing with Backbone.js. But as my view code grew in size, I quickly realized that this approach was not maintainable or optimal because the view was being completely re-rendered when any attribute of the model changed.

When I ran into this problem, I did a quick Google search to see what others had done and found Ian Storm Taylor’s blog post, “<a title="Break Apart Your Backbone.js Render Methods" href="https://ianstormtaylor.com/break-apart-your-backbonejs-render-methods/">Break Apart Your Backbone.js Render Methods</a>,” in which he describes listening for individual attribute changes in the model and then <strong>re-rendering only the part of the view corresponding to the changed attribute</strong>. Taylor also describes returning a reference to the object so that the individual rendering functions can be easily chained together. The example above now transforms into something much more maintainable and performant because we are only updating portions of the view that correspond to the model attributes that have changed.

<pre><code class="language-javascript">
var View = Backbone.View.extend({
    initialize: function(options) {
        this.model.on('change:a', this.renderA, this);
        this.model.on('change:b', this.renderB, this);
    },

    renderA: function() {
        $(‘#a’, this.$el).html(this.model.get(‘a’));
        return this;
    },

    renderB: function() {
        $(‘#b’, this.$el).html(this.model.get(‘b’));
        return this;
    },

    render: function() {
        this
            .renderA()
            .renderB();
    }
});
</code></pre>

I should mention that many plugins, such as <a title="Backbone.StickIt" href="https://nytimes.github.io/backbone.stickit/">Backbone.StickIt</a> and <a title="Backbone.ModelBinder" href="https://github.com/theironcook/Backbone.ModelBinder">Backbone.ModelBinder</a>, provide key-value bindings between model attributes and view elements, which can save you from a lot of boilerplate code. So, check them out if you have complex form fields.</p>

## Keep Models Agnostic To Views

As Jeremy Ashkenas points out in one of Backbone.js’ <a href="https://github.com/documentcloud/backbone/issues/21">GitHub issues</a>, Backbone.js doesn’t enforce any real separation of concerns between the data and view layer, except that models are not created with a reference to their view. Because Backbone.js doesn’t enforce a separation of concerns, should you? I and many other Backbone.js developers, such as <a title="avoiding common backbone.js pitfalls" href="https://ozkatz.github.io/avoiding-common-backbonejs-pitfalls.html">Oz Katz</a> and <a title="Backbone.js Tips: Lessons From The Trenches" href="https://supportbee.com/devblog/2011/07/29/backbone-js-tips-lessons-from-the-trenches/">Dayal</a>, believe the answer is overwhelmingly yes: Models and collections, the data layer, should be entirely agnostic of the views that are bound to them, keeping a clear separation of concerns. If you don’t follow a separation of concerns, your code base could quickly turn into spaghetti code, and <strong>no one likes spaghetti code</strong>.

<a title="spaghetti by gotosira, on Flickr" href="https://www.flickr.com/photos/gotosira/4699302559/"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/51f065e3-5814-4343-8e30-90281a732082/a4699302559-eeeaab770f.jpg" alt="Spaghetti." width="500" height="375" /></a><br>
<em>Keeping your models agnostic to your views will help prevent spaghetti code, and no one likes spaghetti code! (Image: Sira Hanchana)</em>

Keeping your data layer completely agnostic to the view layer allows for a more modular, reusable and maintainable code base. You can easily reuse and extend models and collections throughout your application without concern for the views that are tying into them. Following this pattern <strong>enables developers who are new to your project to quickly dive into the code base</strong>, because they will know exactly where rendering takes place and where all of the business logic of your application should live.

This pattern also enforces the <a title="Single Responsibility Principle" href="https://en.wikipedia.org/wiki/Single_responsibility_principle">single responsibility principle</a>, which dictates that each class should have a single responsibility, and its responsibility should be encapsulated in the class, since your models and collections should handle data and your views should handle rendering.</p>

## Parameter Mapping In Routers

The best way to demonstrate how this pattern came about is through an example. Let’s say you have some sort of search page, and that the search page allows users to add two different filter types, <code>foo</code> and <code>bar</code>, each of which has a multitude of options. Therefore, your URL structure would start off looking something like this:

<pre><code class="language-javascript">
'search/:foo'
'search/:bar'
'search/:foo/:bar'
</code></pre>

Now, all of these routes use the exact same view and model, so you would ideally like them all to use the same function, <code>search()</code>. However, if you examine Backbone.js, there isn’t any sort of parameter mapping; the parameters are just plopped into the function from left to right. So, in order for them all to use the same function, you would end up creating different functions to correctly map the parameters to <code>search()</code>.

<pre><code class="language-javascript">
routes: {
    'search/:foo': 'searchFoo',
    'search/:bar': 'searchBar',
    'search/:foo/:bar': 'search'
},

search: function(foo, bar) {
},

// I know this function will actually still map correctly, but for explanatory purposes, it's left in.
searchFoo: function(foo) {
    this.search(foo, undefined);
},

searchBar: function(bar) {
    this.search(undefined, bar);
},
</code></pre>

As you can imagine, this pattern could quickly bloat your routers. When I first ran into this problem, I attempted to do some parsing of the actual function definitions with regular expressions to “magically” map the parameters, which would have worked — but only if I had followed specific constraints. So, I scrapped the idea (I might still throw this into a Backbone plugin sometime). I opened an <a href="https://github.com/documentcloud/backbone/issues/1833">issue on GitHub</a>, and Ashkenas suggested mapping all of the parameters in the search function.

The code above now transforms into something much more maintainable:

<pre><code class="language-javascript">
routes: {
    'base/:foo': 'search',
    'base/:bar': 'search',
    'base/:foo/:bar': 'search'
},

search: function() {
    var foo, bar, i;

    for(i = arguments.length - 1; i &gt;= 0; i--) {

        if(arguments[i] === 'something to determine foo') {
            foo = arguments[i];
            continue;
        }
        else if(arguments[i] === 'something to determine bar') {
            bar = arguments[i];
            continue;
        }
    }
},
</code></pre>

This pattern can drastically reduce router bloat. However, be aware that it will not work for parameters that are not distinguishable. For example, if you had two parameters that were both IDs and followed the pattern <code>XXXX-XXXX</code>, you would not be able to identify which ID corresponded to which parameter.</p>

## model.fetch() Won’t Clear Your Model

This usually trips up those who are new to Backbone.js: <code>model.fetch()</code> will not clear out your model, but rather <strong>extends the attributes of your model</strong>. Therefore, if your model has attributes <code>x</code>, <code>y</code> and <code>z</code> and your fetch returns <code>y</code> and <code>z</code>, then <code>x</code> will still be in the model and only <code>y</code> and <code>z</code> will be updated. The following example visualizes this concept.

<pre><code class="language-javascript">
var Model = Backbone.Model.extend({
    defaults: {
        x: 1,
        y: 1,
        z: 1
    }
});
var model = new Model();
/* model.attributes yields
{
    x: 1,
    y: 1,
    z: 1
} */
model.fetch();
/* let’s assume that the endpoint returns this
{
    y: 2,
    z: 2,
} */
/* model.attributes now yields
{
    x: 1,
    y: 2,
    z: 2
} */
</code></pre>

## PUTs Require An ID Attribute

This one also usually trips up those who are new to Backbone.js. To have your models send a <a title="HTTP PUT Verb" href="https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods">HTTP PUT</a> request when you call <code>.save()</code>, your model is required to have an ID attribute set. Remember that the HTTP PUT verb is designed to be an update, so it makes sense that to send a PUT request, your model is required to have an ID. In an ideal world, all of your models would have a perfect ID attribute named ID, but the JSON data that you receive from your endpoints will likely not always have perfectly named IDs.

Therefore, if you need to update a model, <strong>be sure that an ID is on the model before saving it</strong>. Backbone.js versions 0.5 and greater allow you to change the name of the ID attribute of your models using <code>idAttribute</code>, in case your endpoint doesn’t return IDs named <code>id</code>.

If are stuck using a version of Backbone.js lower than 0.5, I suggest that you modify the <code>parse</code> function of your collection or model to map your expected ID attribute to the attribute ID. Here’s a quick example of how you can achieve this by modifying your parse function. Let’s imagine you have a collection of cars whose IDs are <code>carID</code>.

<pre><code class="language-javascript">
parse: function(response) {

    _.each(response.cars, function(car, i) {
        // map the returned ID of carID to the correct attribute ID
        response.cars[i].id = response.cars[i].carID;
    });

    return response;
},</code></pre>

## Model Data On Page Load

Sometimes you will find that your models or collections need to be initialized with data on page load. Many articles about Backbone.js patterns, such as Rico Sta Cruz’ “<a title="Backbone patterns" href="https://ricostacruz.com/backbone-patterns/">Backbone Patterns</a>” and Katz’ “<a title="Avoiding Common Backbone.js Pitfalls" href="https://ozkatz.github.io/avoiding-common-backbonejs-pitfalls.html">Avoiding Common Backbone.js Pitfalls</a>,” discuss this pattern. This pattern is easily achieved by inlining a script on the page and rendering out the data in either single-model attributes or JSON, using the server-side language of your choice. For example, in Rails, I use one of the following:

<pre><code class="language-javascript">
// a single attribute
var model = new Model({
    hello: 
});
// or to have json
var model = new Model();
</code></pre>

Using this pattern could improve your search engine rankings by “instantly” rendering out your page, and it could drastically shorten the time it takes for your application to be up and running by limiting the application’s initial HTTP requests.</p>

## Handling Failed Model Attribute Validation

Very often, you will want to know what model attributes have failed validation. For example, if you have an extremely complex form field, you might want to know which model attribute has failed validation so that you can highlight the input field corresponding to the attribute. Unfortunately, alerting your views as to which model attributes have failed validation is not directly baked into Backbone.js, but you can use a few different pattern to handle this.</p>

### Return an Error Object

One pattern to notify your views of which model attributes have failed validation is to pass back an object with some sort of flag detailing which attribute has failed validation, such as the following:

<pre><code class="language-javascript">
// Inside your model
validate: function(attrs) {
    var errors = [];

    if(attrs.a &lt; 0) {
        errors.push({
            'message': 'Form field a is messed up!',
            'class': 'a'
        });
    }
    if(attrs.b &lt; 0) {
        errors.push({
            'message': 'Form field b is messed up!',
            'class': 'b'
        });
    }

    if(errors.length) {
        return errors;
    }
}
// Inside your view
this.model.on('invalid’, function(model, errors) {
    _.each(errors, function(error, i) {
        $(‘.’ + error.class).addClass('error');
        alert(error.message);
    });
});
</code></pre>

The advantage of this pattern is that you are handling all invalid messages in one location. The disadvantage is that your invalid method could become a large <code>switch</code> or <code>if</code> statement if you deal with invalid attributes differently.</p>

### Broadcast Custom Error Event

An alternative pattern, suggested by a friend of mine, <a title="Derick Bailey" href="https://lostechies.com/derickbailey/">Derick Bailey</a>, is to trigger custom errors events for each model attribute. This allows your views to bind to specific error events for individual attributes:

<pre><code class="language-javascript">
// Inside your model
validate: function(attrs) {

    if(attrs.a &lt; 0) {
            this.trigger(‘invalid:a’, 'Form field a is messed up!', this);
    }
    if(attrs.b &lt; 0) {
            this.trigger(‘invalid:b’, 'Form field b is messed up!', this);
    }
}
// Inside your view
this.model.on('invalid:a’, function(error) {
        $(‘a’).addClass('error');
        alert(error);
});
this.model.on('invalid:b’, function(error) {
        $(‘b’).addClass('error');
        alert(error);
});
</code></pre>

The advantage of this pattern is that your view bindings are explicit in the type of error they are bound to, and if you have specific instructions for each type of attribute error, it can clean up your view code and make it more maintainable. The one downside of this pattern is that your views could become rather bloated if there aren’t many differences in how you handle different attribute errors.

Both patterns have their pros and cons, and you should think about which pattern is best for your use case. If you treat all failed validation errors the same way, then the first approach would probably be best; if you have specific UI changes per model attribute, then the latter approach would be better.</p>

## HTTP Status Code 200 Trigger Error

If the endpoint that your model or collection is hitting returns invalid JSON, then your model or collection will trigger an “error” event, even if the endpoint returns a 200 HTTP status code. This issue mostly comes up when developing locally against mock JSON data. So, a good rule of thumb is to throw any mock JSON files you’re developing through a <a title="JSON Formatter" href="https://jsonformatter.curiousconcept.com/"><strong>JSON validator</strong></a>. Or get a <strong>plugin</strong> for your IDE that will catch any ill-formatted JSON.</p>

## Create A Generic Error Display

This one could save you time and create a uniform pattern for handling and visualizing error messages, which will improve your user’s overall experience. In any Backbone.js app that I develop, I create a generic view that handles alerts:

<pre><code class="language-javascript">
var AlertView = Backbone.View.extend({
    set: function(typeOfError, message) {
        var alert = $(‘.in-page-alert’).length ? $(‘.in-page-alert’): $(‘.body-alert’);
        alert
            .removeClass(‘error success warning’)
            .addClass(typeOfError)
            .html(message)
            .fadeIn()
            .delay(5000)
            .fadeOut();
    }
});
</code></pre>

The view above first looks to see whether there is a view-specific <code>in-page-alert</code> div, which you would declare inside of your view’s markup. If there is no view-specific div, then it falls back to a generic <code>body-alert</code> div, which you would declare somewhere in the layout. This enables you to deliver a consistent error message to your users and provides a useful fallback in case you forget to specify a view-specific <code>in-page-alert</code> div. The pattern above streamlines how you handle error messages in your views, as follows:

<pre><code class="language-javascript">
var alert = new AlertView();

this.model.on('error', function(model, error) {
    alert.set('TYPE-OF-ERROR', error);
});
</code></pre>

## Update Single-Page App Document Titles

This is more of a usability concern than anything. If you’re developing a single-page application, remember to <strong>update the document title of each page</strong>! I’ve written a simple Backbone.js plugin, <a title="Backbone.js Router Title Helper" href="https://github.com/pwhisenhunt/Backbonejs-Router-Title-Helper">Backbone.js Router Title Helper</a>, that does this in a simple and elegant format by extending the Backbone.js router. It allows you to specify a title’s object literal, whose keys map to route function names and whose values are page titles.

<pre><code class="language-javascript">
Backbone.Router = Backbone.Router.extend({

    initialize: function(options){
        var that = this;

        this.on('route', function(router, route, params) {

            if(that.titles) {
                if(that.titles[router]) document.title = that.titles[router];
                else if(that.titles.default) document.title = that.titles.default;
                else throw 'Backbone.js Router Title Helper: No title found for route:' + router + ' and no default route specified.';
            }
        });
    }
});
</code></pre>

### Cache Objects In Single-Page Applications

While we are on the topic of single-page applications, another pattern you could follow is to cache objects that will be reused! This case is fairly straightforward and simple:

<pre><code class="language-javascript">
// Inside a router
initialize: function() {

    this.cached = {
        view: undefined,
        model: undefined
    }
},

index: function(parameter) {
    this.cached.model = this.cached.model || new Model({
        parameter: parameter
    });
    this.cached.view = this.cached.view || new View({
        model: this.cached.model
    });
}
</code></pre>

This pattern will give your application a small bump in speed because you won’t have to reinitialize your Backbone.js objects. However, it could cause your application’s memory footprint to grow rather large; so, I’ll typically only cache objects that are commonly used throughout an application. If you’ve developed Backbone.js apps in the past, then you’re likely asking yourself, <strong>“What if I want to refetch data?”</strong> You can refetch data each time the route is triggered:

<pre><code class="language-javascript">
// Inside a router
initialize: function() {

    this.cached = {
        view: undefined,
        model: undefined
    }
},

index: function(parameter) {
    this.cached.model = this.cached.model || new Model({
        parameter: parameter
    });
    this.cached.view = this.cached.view || new View({
        model: this.cached.model
    });
    this.cached.model.fetch();
}
</code></pre>

This pattern will work when your application must retrieve the latest data from the endpoint (for example, an inbox). However, if the data that you’re fetching is dependent on the state of the application (assuming that the state is maintained through your URL and parameters), then you would be refetching data even if the application’s state hasn’t changed since the user was last on the page. A better solution would be to refetch data only when the state of the application (<code>parameter</code>) has changed:

<pre><code class="language-javascript">
// Inside a router
initialize: function() {

    this.cached = {
        view: undefined,
        model: undefined
    }
},

index: function(parameter) {
    this.cached.model = this.cached.model || new Model({
        parameter:parameter
    });
    this.cached.model.set('parameter', parameter);
    this.cached.view = this.cached.view || new View({
        model: this.cached.model
    });
}

// Inside of the model
initialize: function() {
    this.on("change:parameter", this.fetchData, this);
}
</code></pre>

## JSDoc Functions And Backbone.js Classes

I’m a huge fan of documentation and <a href="https://en.wikipedia.org/wiki/JSDoc">JSDoc</a>. I JSDoc all Backbone classes and functions in the following format:

<pre><code class="language-javascript">
var Thing = Backbone.View.extend(/** @lends Thing.prototype */{
    /** @class Thing
     * @author Phillip Whisenhunt
     * @augments Backbone.View
     * @contructs Thing object */
    initialize() {},

    /** Gets data by ID from the thing. If the thing doesn't have data based on the ID, an empty string is returned.
     * @param {String} id The id of get data for.
     * @return {String} The data. */
    getDataById: function(id) {}
});
</code></pre>

If you document your Backbone classes in the format above, then you can generate beautiful documentation that contains all of your classes and functions with parameters, return types and descriptions. Be sure to keep the <code>initialize</code> function as the first function declared, which helps when generating JSDoc. If you’d like to see an example of a project that uses JSDoc, check out the <a title="HomeAway Calendar Widget" href="https://github.com/homeaway/calendar-widget">HomeAway Calendar Widget</a>. There is also a <a title="Grunt.js" href="https://gruntjs.com/">Grunt.js</a> plugin, <a title="Grunt-JSDoc-Plugin" href="https://github.com/krampstudio/grunt-jsdoc-plugin">grunt-jsdoc-plugin</a>, to generate documentation as part of your build process.</p>

## Practice Test-Driven Development

In my opinion, if you’re writing in Backbone.js, you should be following <a title="Test Driven Development" href="https://en.wikipedia.org/wiki/Test-driven_development">test-driven development</a> (TDD) for your models and collections. I follow TDD by first writing failing <a title="Jasmine.js" href="https://github.com/pivotal/jasmine">Jasmine.js</a> unit tests against my models or collections. Once the unit tests are written and failing, I flush out the model or collection.

By this point, all of my Jasmine tests will have been passing, and I have confidence that my model functions all work as expected. Since I’ve been following TDD, my view layer has been super-easy to write and also extremely thin. When you begin practicing TDD, you will definitely slow down; but once you wrap your head around it, your <strong>productivity and the quality of your code will dramatically increase</strong>.

I hope these tips and patterns have helped! If you have suggestions for other patterns or you’ve found a typo or you think that one of these patterns isn’t the best approach, please leave a comment below or <a title="Phillip Whisenhunt Twiter" href="https://twitter.com/pwhisenhunt">tweet me</a>.

<em>Thanks to <a title="Patrick Lewis" href="https://www.mountaindrawn.com/">Patrick Lewis</a>, <a title="Addy Osmani" href="https://addyosmani.com/blog/">Addy Osmani</a>, <a title="Derick Bailey" href="https://lostechies.com/derickbailey/">Derick Bailey</a> and <a title="Iam Storm Taylor" href="https://ianstormtaylor.com/">Ian Storm Taylor</a> for reviewing this article.</em>

<em>(al) (ea)</em>


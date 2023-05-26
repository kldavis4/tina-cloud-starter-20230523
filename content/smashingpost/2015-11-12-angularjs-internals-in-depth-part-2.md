---
title: 'AngularJS’ Internals In Depth, Part 2'
slug: angularjs-internals-in-depth-part-2
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b0a1dfa-0f78-4b86-b555-2c7217f3528c/01-mindbender.png'
date: 2015-11-12T03:29:58.000Z
author: nicolasbevacqua
description: >-
  In the [previous article in this
  series](https://www.smashingmagazine.com/2015/01/22/angularjs-internals-in-depth/
  "AngularJS Internals in Depth, Part 1"), I discussed scope events and the
  behavior of the digest cycle. This time around, I’ll talk about directives.
  This article will cover **isolate scopes, transclusion, linking functions,
  compilers, directive controllers and more**.

  If the figure looks unreasonably mind-bending, then this article might be for
  you. This article is based on the AngularJS v1.3.0 tree.
categories:
  - Coding
  - JavaScript
  - Angular
---
In the <a title="AngularJS Internals in Depth, Part 1" href="https://www.smashingmagazine.com/2015/01/22/angularjs-internals-in-depth/">previous article in this series</a>, I discussed scope events and the behavior of the digest cycle. This time around, I’ll talk about directives. This article will cover <strong>isolate scopes, transclusion, linking functions, compilers, directive controllers and more</strong>.

If the figure looks unreasonably mind-bending, then this article might be for you.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d521deba-e5db-4dfe-8bd2-ecc0f5433ff5/angular-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddc9c6d8-d097-4530-a520-38787891edf0/angular-opt-preview.png" alt="Angular" width="500" height="177" /></a><figcaption>(Image credit: <a href="https://docs.angularjs.org/guide/concepts">Angular JS documentation</a>) (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d521deba-e5db-4dfe-8bd2-ecc0f5433ff5/angular-opt.png">Large version</a>)</figcaption></figure>

<strong>Disclaimer:</strong> This article is based on the <a title="AngularJS on GitHub" href="https://github.com/angular/angular.js/tree/v1.3.0">AngularJS v1.3.0 tree</a>.</p>

## What The Hell Is A Directive?

A directive is a <strong>typically small</strong> component that is meant to interact with the DOM in AngularJS. It is used as an abstraction layer on top of the DOM, and most manipulation can be achieved without touching DOM elements, wrapped in jQuery, jqLite or otherwise. This is accomplished by using expressions, and other directives, to achieve the results you want.

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag: [Link](https://www.smashingmagazine.com/2015/01/angularjs-internals-in-depth/#further-reading-on-smashingmag)

*   [An Introduction To Unit Testing In AngularJS Applications](https://www.smashingmagazine.com/2014/10/introduction-to-unit-testing-in-angularjs/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Automating Style Guide-Driven Development](https://www.smashingmagazine.com/2015/03/automating-style-guide-driven-development/)

Directives in AngularJS’ core can bind an element’s property (<strong>such as visibility, class list, inner text, inner HTML, or value</strong>) to a scope’s property or expression. Most notably, these bindings will be updated whenever changes in the scope are digested, using watches. Similarly, and in the opposite direction, DOM attributes can we “watched” using an <code>$observe</code> function, which will trigger a callback whenever the watched property changes.

Directives are, simply put, the single most important face of AngularJS. If you master directives, then you won’t have any issues dealing with AngularJS applications. Likewise, if you don’t manage to get a hold of directives, you’ll be cluelessly grasping at straws, unsure what you’ll pull off next. Mastering directives takes time, particularly if you’re trying to stay away from merely wrapping a snippet of jQuery-powered code and calling it a day.

In AngularJS, you’re able to build componentized directives, services and controllers that can be reused as often as it makes sense for them to be reused. For instance, you might have a simple directive that turns on a class based on a watched scope expression, and I’d imagine that would be a pretty common directive, used everywhere in your application, to signal the state of a particular component in your code. You could have a service to aggregate keyboard shortcut-handling, and have controllers, directives and other services register shortcuts with that service, rooting all of your keyboard shortcut-handling in one nicely self-contained service.

Directives are also reusable pieces of functionality, but most often, these are <strong>assigned to DOM fragments, or templates</strong>, rather than merely providing functionality. Time to dive deep down into AngularJS directives and their use cases.</p>

## Creating A Directive

Earlier, I <a href="https://ponyfoo.com/2014/02/14/angle-brackets-rifle-scopes">listed each property available on a scope</a> in AngularJS, and I used that to explain the digest mechanism and how scopes operate. I’ll do the same for directives, but this time I’ll go through the properties of the object returned by a directive’s factory function and how each of those properties influences the directive we’re defining.

The first thing of note is the name of the directive. Let’s look at a brief example.</p>

<pre><code class="language-javascript">
angular.module('PonyDeli').directive('pieceOfFood', function () {
  var definition = { // </code></pre>

Even though in the snippet above we’re defining a directive named <code>'pieceOfFood'</code>, AngularJS convention stipulates that we use a hyphenated version of that name in the HTML markup. That is, if this directive were implemented as an attribute, then I might need to refer it in my HTML like so:

<pre><code class="language-markup">
&lt;span piece-of-food&gt;&lt;/span&gt;
</code></pre>

By default, directives can only be triggered as attributes. But what if you want to change this behavior? You can use the <code>restrict</code> option.

*   [`restrict`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L2004) Defines how a directive may be applied in markup

<pre><code class="language-javascript">
angular.module('PonyDeli').directive('pieceOfFood', function () {
  return {
    restrict: 'E',
    template: // ...
  };
});
</code></pre>

For some reason I cannot fathom, they’ve decided to obfuscate what’s otherwise a verbose framework, and we’ve ended up with single capital letters to define how a directive is restricted. A list of <a title="Where can I add a directive? - AngularJS on GitHub" href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1343">available <code>restrict</code> choices</a> appears on GitHub, and the <a title="&#96;'EA'&#96; is the default &#96;restrict&#96; value - AngularJS on GitHub" href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L754">default value is <code>EA</code></a>.

*   `'A'`: attributes are allowed `<span piece-of-food></span>`
*   `'E'`: elements are allowed `<piece-of-food></piece-of-food>`
*   `'C'`: as a class name `<span class='piece-of-food'></span>`
*   `'M'`: as a comment `<!-- directive: piece-of-food -->`
*   `'AE'`: You can combine any of these to loosen up the restriction a bit.

Don’t ever use <code>'C'</code> or <code>'M'</code> to restrict your directives. Using <code>'C'</code> doesn’t stand out in markup, and <code>'M'</code> was meant for backwards compatibility. If you feel like being funny, though, you could make a case for setting <code>restrict</code> to <code>'ACME'</code>.

(Remember how in the last article I said to <strong>take advice with a pinch of salt</strong>? Don’t do that with mine — my advice is awesome!)

Unfortunately, the rest of the properties in a directive definition object are much more obscure.

*   [`scope`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1287-L1289 "Determining the scope of a directive - AngularJS on GitHub") sets how a directive interacts with **the `$parent` scope**

Because we discussed scopes at length in the previous article, learning how to use the <code>scope</code> property <strong>properly</strong> shouldn’t be all that excruciating. Let’s start with the default value, <code>scope: false</code>, where the scope chain remains unaffected: You’ll get <strong>whatever scope is found</strong> on the associated element, following the rules I <a title="AngularJS Internals in Depth, Part 1" href="https://www.smashingmagazine.com/2015/01/22/angularjs-internals-in-depth/">outlined in the previous article</a>.

Leaving the scope chain untouched is obviously useful when your directive doesn’t interact with the scope at all, but that rarely happens. A much more common scenario in which not touching the scope is useful is creating a directive that has no reason to be instanced more than once on any given scope and that just interacts with a single scope property, the <strong>directive’s name</strong>. This is most declarative when combined with <code>restrict: 'A'</code>, the default <code>restrict</code> value. (The code below is <a title="A piece of food on CodePen" href="https://codepen.io/bevacqua/pen/iexmJ">available on Codepen</a>.)

<pre><code class="language-javascript">
angular.module('PonyDeli').directive('pieceOfFood', function () {
  return {
    template: '{{pieceOfFood}}',
    link: function (scope, element, attrs) {
      attrs.$observe('pieceOfFood', function (value) {
        scope.pieceOfFood = value;
      });
    }
  };
});
</code></pre>

<pre><code class="language-markup">
&lt;body ng-app='PonyDeli'&gt; 
  &lt;span piece-of-food='Fish &amp; Chips'&gt;&lt;/span&gt;
&lt;/body&gt;
</code></pre>

There are a few things to note here that we haven’t discussed yet. You’ll learn more about the <code>link</code> property later in this article. For the time being, think of it as a <strong>controller that runs for each instance of the directive</strong>.

In the directive’s linking function, we can access <code>attrs</code>, which is a collection of attributes present on <code>element</code>. This collection has a special method, called <code>$observe()</code>, which will fire a callback <a title="Observing attributes - AngularJS on GitHub" href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1039-L1047">whenever a property changes</a>. Without watching the attribute for changes, the property wouldn’t ever make it to the scope, and we wouldn’t be able to bind to it in our template.

We can twist the code above, making it much more useful, by adding <code>scope.$eval</code> to the mix. Remember how it can be used to evaluate an expression against a scope? Look at the code below (<a title="Interpreting food-scopes on CodePen" href="https://codepen.io/bevacqua/pen/ilgtv">also on Codepen</a>) to get a better idea of how that could help us.</p>

<pre><code class="language-javascript">
var deli = angular.module('PonyDeli', []);

deli.controller('foodCtrl', function ($scope) {
  $scope.piece = 'Fish &amp; Chips';
});

deli.directive('pieceOfFood', function () {
  return {
    template: '{{pieceOfFood}}',
    link: function (scope, element, attrs) {
      attrs.$observe('pieceOfFood', function (value) {
        scope.pieceOfFood = scope.$eval(value);
      });
    }
  };
});
</code></pre>

<pre><code class="language-markup">
&lt;body ng-app='PonyDeli' ng-controller='foodCtrl'&gt;
  &lt;span piece-of-food='piece'&gt;&lt;/span&gt;
&lt;/body&gt;
</code></pre>

In this case, I’m evaluating the attribute’s value, <code>piece</code>, against the scope, which defined <code>$scope.piece</code> at the controller. Of course, you could use a template like <code>{{piece}}</code> directly, but that would require specific knowledge about which property in the scope you want to track. This pattern provides a <strong>little more flexibility</strong>, although you’re still going to be sharing the scope <strong>across all directives</strong>, which can lead to <strong>unexpected behavior</strong> if you were to try adding more than one directive in the same scope.

## Playful Child Scopes

You could solve that issue by creating a child scope, which inherits prototypically from its parent. To create a child scope, you merely need to declare <code>scope: true</code>.</p>

<pre><code class="language-javascript">var deli = angular.module('PonyDeli', []);

deli.controller('foodCtrl', function ($scope) {
  $scope.pieces = ['Fish &amp; Chips', 'Potato Salad'];
});

deli.directive('pieceOfFood', function () {
  return {
    template: '{{pieceOfFood}}',
    scope: true,
    link: function (scope, element, attrs) {
      attrs.$observe('pieceOfFood', function (value) {
        scope.pieceOfFood = scope.$eval(value);
      });
    }
  };
});
</code></pre>

<pre><code class="language-markup">&lt;body ng-app='PonyDeli' ng-controller='foodCtrl'&gt;
  &lt;p piece-of-food='pieces[0]'&gt;&lt;/p&gt;
  &lt;p piece-of-food='pieces[1]'&gt;&lt;/p&gt;
&lt;/body&gt;
</code></pre>

As you can see, we’re now able to <a title="Directive child scopes on CodePen" href="https://codepen.io/bevacqua/pen/JrLev">use multiple instances</a> of the directive and get the desired behavior because each directive is creating its own scope. However, there’s a limitation: Multiple directives on an element all get the same scope.</p>

<strong>Note:</strong> If multiple directives on the same element request a new scope, then only one new scope is created.</p>

### Lonely, Isolate Scope

One last option is to create a local, or isolate, scope. The difference between an isolate scope and a child scope is that the former doesn’t inherit from its parent (but it’s <strong>still accessible on <code>scope.$parent</code></strong>). You can declare an isolate scope like this: <code>scope: {}</code>. You can add properties to the object, which get data-bound to the parent scope but are accessible on the local scope. Much like <code>restrict</code>, isolate scope properties have a terse but confusing syntax, in which you can use symbols such as <code>&amp;</code>, <code>@</code> and <code>=</code> to define how the property is bound.

You may omit the property’s name if you’re going to use that as the key in your local scope. That is to say, <code>pieceOfFood: '='</code> is a shorthand for <code>pieceOfFood: '=pieceOfFood'</code>; they are equivalent.</p>

## Choose Your Weapon: `@`, `&` Or `=`

What do those symbols mean, then? The examples I coded, enumerated below, might help you decode them.</p>

### Attribute Observer: `@`

Using <code>@</code> binds to the result of <a title="Buying vegetables on CodePen" href="https://codepen.io/bevacqua/pen/IxvBc">observing an attribute</a> against the parent scope.</p>

<pre><code class="language-markup">&lt;body ng-app='PonyDeli' ng-controller='foodCtrl'&gt;
  &lt;p note='You just bought some {{type}}'&gt;&lt;/p&gt;
&lt;/body&gt;
</code></pre>

<pre><code class="language-javascript">deli.directive('note', function () {
  return {
    template: '{{note}}',
      scope: {
        note: '@'
      }
  };
});
</code></pre>

This is <a title="Observing an attribute value - AngularJS on GitHub" href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1854-L1856">equivalent to observing the attribute</a> for changes and updating our local scope. Of course, using the <code>@</code> notation is much more “AngularJS.”

<pre><code class="language-javascript">deli.directive('note', function () {
  return {
    template: '{{note}}',
    scope: {},
    link: function (scope, element, attrs) {
      attrs.$observe('note', function (value) {
        scope.note = value;
      });
    }
  };
});
</code></pre>

Attribute observers are most useful when <strong>consuming options for a directive</strong>. If we want to change the directive’s behavior based on changing options, though, then writing the <code>attrs.$observe</code> line ourselves might make more sense than having AngularJS <a title="Observing an attribute value - AngularJS on GitHub" href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1854-L1856">do it internally</a> and creating a watch on our end, which would be slower.

In these cases, merely replacing <code>scope.note = value</code>, in the <code>$observe</code> handler shown above, into whatever you would have put on the <code>$watch</code> listener should do.</p>

<strong>Note:</strong> keep in mind that, when dealing with <code>@</code>, we’re <strong>talking about observing and attribute</strong>, instead of binding to the parent scope.</p>

### Expression Builder: `&`

Using <code>&amp;</code> gives you an <a title="Expression evaluation on CodePen" href="https://codepen.io/bevacqua/pen/glhso">expression-evaluating function</a> in the context of the parent scope.</p>

<pre><code class="language-markup">&lt;body ng-app='PonyDeli' ng-controller='foodCtrl'&gt;
  &lt;p note='"You just bought some " + type'&gt;&lt;/p&gt;
&lt;/body&gt;
</code></pre>

<pre><code class="language-javascript">deli.directive('note', function () {
  return {
    template: '{{note()}}',
    scope: {
      note: '&amp;'
    }
  };
});
</code></pre>

Below, I’ve outlined how you might implement that same functionality in the linking function, in case you aren’t aware of <code>&amp;</code>. This one is a tad lengthier than <code>@</code>, because it is <a title="Parsing a getter expression - AngularJS on GitHub" href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1902-L1905">parsing the expression in the attribute</a> once, building a reusable function.</p>

<pre><code class="language-javascript">deli.directive('note', function ($parse) {
  return {
    template: '{{note()}}',
    scope: {},
    link: function (scope, element, attrs) {
      var parentGet = $parse(attrs.note);

      scope.note = function (locals) {
        return parentGet(scope.$parent, locals);
      };
    }
  };
});
</code></pre>

Expression builders, as we can see, generate a method that queries the parent scope. You can execute the method whenever you’d like and even watch it for output changes. This method should be treated as a read-only query on a parent expression and, as such, would be most useful in two scenarios. The first one is when you need to watch for changes on the parent scope, in which case you would set up a watch on the function expression <code>note()</code>, which is, in essence, what we did in the example above.

The other situation in which this might come in handy is when you need access to a method on the parent scope. Suppose the parent scope has a method that refreshes a table, while your local scope represents a table row. When the table row is deleted, you might want to refresh the table. If the button is in the child scope, then it would make sense to use a <code>&amp;</code> binding to access the refresh functionality on the parent scope. That’s just a contrived example — you might prefer to use events for that kind of thing, or maybe even structure your application in some way so that complicating things like that can be avoided.</p>

### Bi-Directional Binding: `=`

Using <code>=</code> sets up <a title="Bi-directional binding on CodePen" href="https://codepen.io/bevacqua/pen/sDmAo">bi-directional binding</a> between the local and parent scopes.</p>

<pre><code class="language-markup">&lt;body ng-app='PonyDeli' ng-controller='foodCtrl'&gt;
  &lt;button countable='clicks'&gt;&lt;/button&gt;
  &lt;span&gt;Got {{clicks}} clicks!&lt;/span&gt;
&lt;/body&gt;
</code></pre>

<pre><code class="language-javascript">deli.directive('countable', function () {
  return {
    template:
      '&lt;button ng-disabled="!remaining"&gt;' +
        'Click me {{remaining}} more times! ({{count}})' +
      '&lt;/button&gt;',
    replace: true,
    scope: {
      count: '=countable'
    },
    link: function (scope, element, attrs) {
      scope.remaining = 10;

      element.bind('click', function () {
        scope.remaining--;
        scope.count++;
        scope.$apply();
      });
    }
  };
});
</code></pre>

Bi-directional binding is <a title="Bi-directional binding implementation - AngularJS on GitHub" href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1866-L1898">quite a bit more complicated</a> than <code>&amp;</code> or <code>@</code>.</p>

<pre><code class="language-javascript">deli.directive('countable', function ($parse) {
  return {
    template:
      '&lt;button ng-disabled="!remaining"&gt;' +
        'Click me {{remaining}} more times! ({{count}})' +
      '&lt;/button&gt;',
    replace: true,
    scope: {},
    link: function (scope, element, attrs) {

      // you're definitely better off just using '&amp;'

      var compare;
      var parentGet = $parse(attrs.countable);
      if (parentGet.literal) {
        compare = angular.equals;
      } else {
        compare = function(a,b) { return a === b; };
      }
      var parentSet = parentGet.assign; // or throw
      var lastValue = scope.count = parentGet(scope.$parent);

      scope.$watch(function () {
        var value = parentGet(scope.$parent);
        if (!compare(value, scope.count)) {
          if (!compare(value, lastValue)) {
            scope.count = value;
          } else {
            parentSet(scope.$parent, value = scope.count);
          }
        }
        return lastValue = value;
      }, null, parentGet.literal);

      // I told you!

      scope.remaining = 10;

      element.bind('click', function () {
        scope.remaining--;
        scope.count++;
        scope.$apply();
      });
    }
  };
});
</code></pre>

This form of data-binding is <strong>arguably the most useful</strong> of all three. In this case, the parent scope property is kept in sync with the local scope. Whenever the local scope’s value is updated, it gets set on the parent scope. Likewise, whenever the parent scope value changes, the local scope gets updated. The most straightforward scenario I’ve got for you for when this would be useful is whenever you have a child scope that is used to represent a sub-model of the parent scope. Think of your typical <a title="CRUD on Wikipedia" href="https://en.wikipedia.org/wiki/Create,_read,_update_and_delete">CRUD</a> table (create, read, update, delete). The table as a whole would be the parent scope, whereas each row would be contained in an isolate directive that binds to the row’s data model through a two-way <code>=</code> binding. This would allow for modularity, while still allowing for effective communication between the master table and its children.

That took a lot of words, but I think I’ve managed to sum up how the <code>scope</code> property works when declaring directives and what the most common use cases are. Let’s move on to other properties in the directive definition object, shall we?

## Sensible View Templates

Directives are most effective when they contain small reusable snippets of HTML. That’s where the true power of directives comes from. These templates may be provided in plain text or as a resource that AngularJS queries when bootstrapping the directive.

*   [`template`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1614 "Setting a view template - AngularJS on GitHub") This is how you would provide the view template as plain text. `template: '<span ng-bind="message" />'`
*   [`templateUrl`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L2099 "Using templateUrl to fetch a template using AJAX - AngularJS on GitHub") This allows you to provide the URL to an HTML template. `templateUrl: /partials/message.html`

Using <code>templateUrl</code> to separate the HTML from your linking function is awesome. Making an AJAX request whenever you want to initialize a directive for the first time, not so much. However, you can circumvent the AJAX request if you pre-fill the <code>$templateCache</code> with a build task, such as <a title="grunt-angular-templates on GitHub" href="https://github.com/ericclemmons/grunt-angular-templates">grunt-angular-templates</a>. You could also inline your view templates in the HTML, but that is slower because the DOM has to be parsed, and that’s not as convenient in a large project with a ton of views. You don’t want an immense “layout” with all of the things, but rather individual files that contain just the one view. That would be the <strong>best of both worlds</strong>: separation of concerns without the extra overhead of AJAX calls.

You could also provide a <code>function (tElement, tAttrs)</code> as the <code>template</code>, but this is <strong>neither necessary nor useful.</strong>

*   [`replace`](https://codepen.io/bevacqua/pen/iteGj "Replaced versus inlined directives") Should the template be inserted as a child element or inlined?

The <a href="https://code.angularjs.org/1.3.0-beta.11/docs/api/ng/service/$compile">documentation for this property</a> is woefully confusing:
<blockquote><code>replace</code>
specify where the template should be inserted. Defaults to <code>false</code>.
<ul>
 	<li><code>true</code> — the template will replace the current element</li>
 	<li><code>false</code> — the template will replace the contents of the current element</li>
</ul>
</blockquote>

So, when replace is <code>false</code>, the directive actually replaces the element? That doesn’t sound right. If you <a title="Replaced versus inlined directives" href="https://codepen.io/bevacqua/pen/iteGj">check out my pen</a>, you’ll find out that the element simply gets appended if <code>replace: false</code>, and it gets <a title="'Replacing' an element with a directive - AngularJS on GitHub" href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1622-L1659">sort of replaced</a> if <code>replace: true</code>.

As a rule of thumb, try to keep replacements to a minimum. Directives should keep interference with the DOM as close as possible to none, whenever possible, of course.

Directives are compiled, which results in a pre-linking function and a post-linking function. You can define the code that returns these functions or just provide them. Below are the different ways you can provide linking functions. I warn you: This is yet another one of those “features” in AngularJS that I feel is more of a drawback, because it <strong>confuses the hell out of newcomers for little to no gain</strong>. Behold!

<pre><code class="language-javascript">compile: function (templateElement, templateAttrs) {
  return {
    pre: function (scope, instanceElement, instanceAttrs, controller) {
      // pre-linking function
    },
    post: function (scope, instanceElement, instanceAttrs, controller) {
      // post-linking function
    }
  }
}
</code></pre>

<pre><code class="language-javascript">compile: function (templateElement, templateAttrs) {
  return function (scope, instanceElement, instanceAttrs, controller) {
    // post-linking function
  };
}
</code></pre>

<pre><code class="language-javascript">link: {
  pre: function (scope, instanceElement, instanceAttrs, controller) {
    // pre-linking function
  },
  post: function (scope, instanceElement, instanceAttrs, controller) {
    // post-linking function
  }
}
</code></pre>

<pre><code class="language-javascript">link: function (scope, instanceElement, instanceAttrs, controller) {
  // post-linking function
}
</code></pre>

Actually, you could even forget about the directive definition object we’ve been discussing thus far and merely return a post-linking function. However, this isn’t recommended even by AngularJS peeps, so you’d better stay away from it. Note that the linking functions don’t follow the dependency-injection model you find when declaring controllers or directives. For the most part, dependency injection in AngularJS is made available at the top level of the API, but most other methods have static well-documented parameter lists that you can’t change.</p>

<pre><code class="language-javascript">deli.directive('food', function () {
  return function (scope, element, attrs) {
    // post-linking function
  };
});
</code></pre>

Before proceeding, here’s an important note from the AngularJS documentation I’d like you to take a look at:

<strong>Note:</strong> The template instance and the link instance may be different objects if the template has been cloned. For this reason it is not safe to do anything other than DOM transformations that apply to all cloned DOM nodes within the compile function. Specifically, DOM listener registration should be done in a linking function rather than in a compile function.

Compile functions currently take in a third parameter, a transclude linking function, but it’s deprecated. Also, you shouldn’t be altering the DOM during compile functions (on <code>templateElement</code>). Just do yourself a favor and avoid <code>compile</code> entirely; provide pre-linking and post-linking functions directly. Most often, a post-linking function is just enough, which is what you’re using when you assign a <code>link</code> function to the definition object.

I have a rule for you here. Always use a post-linking function. If a scope absolutely needs to be pre-populated before the DOM is linked, then do just that in the pre-linking function, but bind the functionality in the post-linking function, like you normally would have. You’ll rarely need to do this, but I think it’s still worth mentioning.</p>

<pre><code class="language-javascript">link: {
  pre: function (scope, element, attrs, controller) {
    scope.requiredThing = [1, 2, 3];
  },
  post: function (scope, element, attrs, controller) {
    scope.squeal = function () {
      scope.$emit("squeal");
    };
  }
}
</code></pre>

*   [`controller`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1814 "Controller instances can be shared on the scope - AngularJS on GitHub") This is a controller instance on the directive.

Directives can have controllers, which makes sense because directives can create a scope. The controller is shared among all directives on the scope, and it is accessible as the fourth argument in linking functions. These controllers are a useful communication channel across directives on the same scoping level, which may be contained in the directive itself.

*   [`controllerAs`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1814 "Assigning a controllerAs alias - AngularJS on GitHub") This is the controller alias to refer to in the template.

Using a controller alias allows you to use the controller within the template itself, because it will be made available in the scope.

*   [`require`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1764-L1768 "Require or whine - AngularJS on GitHub") This will throw an error if you don’t link some other directive(s) on this element!

The documentation for <code>require</code> is surprisingly straightforward, so I’ll just cheat and paste that here:
<blockquote>Require another directive and inject its controller as the fourth argument to the linking function. The <code>require</code> takes a string name (or array of strings) of the directive(s) to pass in. If an array is used, the injected argument will be an array in corresponding order. If no such directive can be found, or if the directive does not have a controller, then an error is raised. The name can be prefixed with:
<ul>
 	<li><code>(no prefix)</code> Locate the required controller on the current element. Throw an error if not found</li>
 	<li><code>?</code> Attempt to locate the required controller or pass <code>null</code> to the <code>link</code> fn if not found</li>
 	<li><code>^</code> Locate the required controller by searching the element’s parents. Throw an error if not found</li>
 	<li><code>?^</code> Attempt to locate the required controller by searching the element’s parents or pass <code>null</code> to the <code>link</code> fn if not found</li>
</ul>
</blockquote>

Require is useful when our directive depends on other directives in order to work. For example, you might have a dropdown directive that depends on a list-view directive, or an error dialog directive that depends on having an error message directive. The example below, on the other hand, defines a <code>needs-model</code> directive that throws an error if it doesn’t find an accompanying <code>ng-model</code> — presumably because <code>needs-model</code> uses that directive or somehow depends on it being available on the element.</p>

<pre><code class="language-javascript">angular.module('PonyDeli').directive(‘needsModel’, function () {
  return {
    require: 'ngModel’,
  }
});
</code></pre>

<pre><code class="language-markup">&lt;div needs-model ng-model=’foo’&gt;&lt;/div&gt;
</code></pre>

*   [`priority`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L2199-L2204 "Priority Sort - AngularJS on GitHub") This defines the order in which directives are applied.

Cheating time!
<blockquote>When there are multiple directives defined on a single DOM element, sometimes it is necessary to specify the order in which the directives are applied. The <code>priority</code> is used to sort the directives before their <code>compile</code> functions get called. Priority is defined as a number. Directives with greater numerical <code>priority</code> are compiled first. Pre-link functions are also run in priority order, but post-link functions are run in reverse order. The order of directives with the same priority is <em>undefined</em>. The default priority is <code>0</code>.</blockquote>

*   [`terminal`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1536-L1538 "Enforcing terminal priority - AngularJS on GitHub") This prevents further processing of directives.</p>

<blockquote>If set to true then the current <code>priority</code> will be the last set of directives which will execute (any directives at the current priority will still execute as the order of execution on same <code>priority</code> is <em>undefined</em>).</blockquote>

## Transcluding For Much Win

*   [`transclude`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1572-L1609 "Transcluded directives - AngularJS on GitHub") This compiles the content of the element and makes it available to the directive.

I’ve saved the best (worst?) for last. This property allows two values, for more fun and less profit. You can set it either to <code>true</code>, which enables transclusion, or to <code>'element'</code>, in which case the whole element, including any directives defined at a lower priority, get transcluded.

At a high level, transclusion allows the consumer of a directive to define a snippet of HTML, which can then be included into some part of the directive, using an <code>ng-transclude</code> directive. This sounds way too complicated, and it’s only kind of complicated. An example might make things clearer.</p>

<pre><code class="language-javascript">angular.module('PonyDeli').directive('transclusion', function () {
  return {
    restrict: 'E',
    template:
      '&lt;div ng-hide="hidden" class="transcluded"&gt;' +
        '&lt;span ng-transclude&gt;&lt;/span&gt;' +
        '&lt;span ng-click="hidden=true" class="close"&gt;Close&lt;/span&gt;' +
      '&lt;/div&gt;',
    transclude: true
  };
});
</code></pre>

<pre><code class="language-markup">&lt;body ng-app='PonyDeli'&gt;
  &lt;transclusion&gt;
    &lt;span&gt;The plot thickens!&lt;/span&gt;
  &lt;/transclusion&gt;
&lt;/body&gt;
</code></pre>

You can <a title="Basic Transclusion on CodePen" href="https://codepen.io/bevacqua/pen/rlmwB">check it out on CodePen</a>, of course. What happens when you try to get scopes into the mix? Well, the content that gets transcluded inside the directive will still respond to the parent content, correctly, even though it’s placed inside the directive and even if the directive presents an isolate scope. This is what you’d expect because the transcluded content is defined in the consuming code, which belongs to the parent scope, and not the directive’s scope. The directive still binds to its local scope, as usual.</p>

<pre><code class="language-javascript">var deli = angular.module('PonyDeli', []);

deli.controller('foodCtrl', function ($scope) {
  $scope.message = 'The plot thickens!';
});

deli.directive('transclusion', function () {
  return {
    restrict: 'E',
    template:
      '&lt;div ng-hide="hidden" class="transcluded"&gt;' +
        '&lt;span ng-transclude&gt;&lt;/span&gt;' +
        '&lt;span ng-click="hidden=true" class="close" ng-bind="close"&gt;&lt;/span&gt;' +
      '&lt;/div&gt;',
    transclude: true,
    scope: {},
    link: function (scope) {
      scope.close = 'Close';
    }
  };
});
</code></pre>

<pre><code class="language-markup">&lt;body ng-app='PonyDeli' ng-controller='foodCtrl'&gt;
  &lt;transclusion&gt;
    &lt;span ng-bind='message'&gt;&lt;/span&gt;
  &lt;/transclusion&gt;
&lt;/body&gt;
</code></pre>

You can <a title="Transcluded Scopes on CodePen" href="https://codepen.io/bevacqua/pen/lFHoE">find that one on CodePen</a> as well. There you have it: transclusion, demystified.

*   [`template`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1614 "Setting a view template - AngularJS on GitHub") This is how you would provide the view template as plain text. `template: '<span ng-bind="message" />'`
*   [`templateUrl`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L2099 "Using templateUrl to fetch a template using AJAX - AngularJS on GitHub") This allows you to provide the URL to an HTML template. `templateUrl: /partials/message.html`

Using <code>templateUrl</code> to separate the HTML from your linking function is awesome. Making an AJAX request whenever you want to initialize a directive for the first time, not so much. However, you can circumvent the AJAX request if you pre-fill the <code>$templateCache</code> with a build task, such as <a title="grunt-angular-templates on GitHub" href="https://github.com/ericclemmons/grunt-angular-templates">grunt-angular-templates</a>. You could also inline your view templates in the HTML, but that is slower because the DOM has to be parsed, and that’s not as convenient in a large project with a ton of views. You don’t want an immense “layout” with all of the things, but rather individual files that contain just the one view. That would be the <strong>best of both worlds</strong>: separation of concerns without the extra overhead of AJAX calls.

You could also provide a <code>function (tElement, tAttrs)</code> as the <code>template</code>, but this is <strong>neither necessary nor useful.</strong>

*   [`replace`](https://codepen.io/bevacqua/pen/iteGj "Replaced versus inlined directives") Should the template be inserted as a child element or inlined?

The <a href="https://code.angularjs.org/1.3.0-beta.11/docs/api/ng/service/$compile">documentation for this property</a> is woefully confusing:
<blockquote><code>replace</code>
specify where the template should be inserted. Defaults to <code>false</code>.
<ul>
 	<li><code>true</code> — the template will replace the current element</li>
 	<li><code>false</code> — the template will replace the contents of the current element</li>
</ul>
</blockquote>

So, when replace is <code>false</code>, the directive actually replaces the element? That doesn’t sound right. If you <a title="Replaced versus inlined directives" href="https://codepen.io/bevacqua/pen/iteGj">check out my pen</a>, you’ll find out that the element simply gets appended if <code>replace: false</code>, and it gets <a title="'Replacing' an element with a directive - AngularJS on GitHub" href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1622-L1659">sort of replaced</a> if <code>replace: true</code>.

As a rule of thumb, try to keep replacements to a minimum. Directives should keep interference with the DOM as close as possible to none, whenever possible, of course.

Directives are compiled, which results in a pre-linking function and a post-linking function. You can define the code that returns these functions or just provide them. Below are the different ways you can provide linking functions. I warn you: This is yet another one of those “features” in AngularJS that I feel is more of a drawback, because it <strong>confuses the hell out of newcomers for little to no gain</strong>. Behold!

<pre><code class="language-javascript">compile: function (templateElement, templateAttrs) {
  return {
    pre: function (scope, instanceElement, instanceAttrs, controller) {
      // pre-linking function
    },
    post: function (scope, instanceElement, instanceAttrs, controller) {
      // post-linking function
    }
  }
}
</code></pre>

<pre><code class="language-javascript">compile: function (templateElement, templateAttrs) {
  return function (scope, instanceElement, instanceAttrs, controller) {
    // post-linking function
  };
}
</code></pre>

<pre><code class="language-javascript">link: {
  pre: function (scope, instanceElement, instanceAttrs, controller) {
    // pre-linking function
  },
  post: function (scope, instanceElement, instanceAttrs, controller) {
    // post-linking function
  }
}
</code></pre>

<pre><code class="language-javascript">link: function (scope, instanceElement, instanceAttrs, controller) {
  // post-linking function
}
</code></pre>

Actually, you could even forget about the directive definition object we’ve been discussing thus far and merely return a post-linking function. However, this isn’t recommended even by AngularJS peeps, so you’d better stay away from it. Note that the linking functions don’t follow the dependency-injection model you find when declaring controllers or directives. For the most part, dependency injection in AngularJS is made available at the top level of the API, but most other methods have static well-documented parameter lists that you can’t change.</p>

<pre><code class="language-javascript">deli.directive('food', function () {
  return function (scope, element, attrs) {
    // post-linking function
  };
});
</code></pre>

Before proceeding, here’s an important note from the AngularJS documentation I’d like you to take a look at:

<strong>Note:</strong> The template instance and the link instance may be different objects if the template has been cloned. For this reason it is not safe to do anything other than DOM transformations that apply to all cloned DOM nodes within the compile function. Specifically, DOM listener registration should be done in a linking function rather than in a compile function.

Compile functions currently take in a third parameter, a transclude linking function, but it’s deprecated. Also, you shouldn’t be altering the DOM during compile functions (on <code>templateElement</code>). Just do yourself a favor and avoid <code>compile</code> entirely; provide pre-linking and post-linking functions directly. Most often, a post-linking function is just enough, which is what you’re using when you assign a <code>link</code> function to the definition object.

I have a rule for you here. Always use a post-linking function. If a scope absolutely needs to be pre-populated before the DOM is linked, then do just that in the pre-linking function, but bind the functionality in the post-linking function, like you normally would have. You’ll rarely need to do this, but I think it’s still worth mentioning.</p>

<pre><code class="language-javascript">link: {
  pre: function (scope, element, attrs, controller) {
    scope.requiredThing = [1, 2, 3];
  },
  post: function (scope, element, attrs, controller) {
    scope.squeal = function () {
      scope.$emit("squeal");
    };
  }
}
</code></pre>

*   [`controller`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1814 "Controller instances can be shared on the scope - AngularJS on GitHub") This is a controller instance on the directive.

Directives can have controllers, which makes sense because directives can create a scope. The controller is shared among all directives on the scope, and it is accessible as the fourth argument in linking functions. These controllers are a useful communication channel across directives on the same scoping level, which may be contained in the directive itself.

*   [`controllerAs`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1814 "Assigning a controllerAs alias - AngularJS on GitHub") This is the controller alias to refer to in the template.

Using a controller alias allows you to use the controller within the template itself, because it will be made available in the scope.

*   [`require`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1764-L1768 "Require or whine - AngularJS on GitHub") This will throw an error if you don’t link some other directive(s) on this element!

The documentation for <code>require</code> is surprisingly straightforward, so I’ll just cheat and paste that here:
<blockquote>Require another directive and inject its controller as the fourth argument to the linking function. The <code>require</code> takes a string name (or array of strings) of the directive(s) to pass in. If an array is used, the injected argument will be an array in corresponding order. If no such directive can be found, or if the directive does not have a controller, then an error is raised. The name can be prefixed with:
<ul>
 	<li><code>(no prefix)</code> Locate the required controller on the current element. Throw an error if not found</li>
 	<li><code>?</code> Attempt to locate the required controller or pass <code>null</code> to the <code>link</code> fn if not found</li>
 	<li><code>^</code> Locate the required controller by searching the element’s parents. Throw an error if not found</li>
 	<li><code>?^</code> Attempt to locate the required controller by searching the element’s parents or pass <code>null</code> to the <code>link</code> fn if not found</li>
</ul>
</blockquote>

Require is useful when our directive depends on other directives in order to work. For example, you might have a dropdown directive that depends on a list-view directive, or an error dialog directive that depends on having an error message directive. The example below, on the other hand, defines a <code>needs-model</code> directive that throws an error if it doesn’t find an accompanying <code>ng-model</code> — presumably because <code>needs-model</code> uses that directive or somehow depends on it being available on the element.</p>

<pre><code class="language-javascript">angular.module('PonyDeli').directive(‘needsModel’, function () {
  return {
    require: 'ngModel’,
  }
});
</code></pre>

<pre><code class="language-markup">&lt;div needs-model ng-model=’foo’&gt;&lt;/div&gt;
</code></pre>

*   [`priority`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L2199-L2204 "Priority Sort - AngularJS on GitHub") This defines the order in which directives are applied.

Cheating time!
<blockquote>When there are multiple directives defined on a single DOM element, sometimes it is necessary to specify the order in which the directives are applied. The <code>priority</code> is used to sort the directives before their <code>compile</code> functions get called. Priority is defined as a number. Directives with greater numerical <code>priority</code> are compiled first. Pre-link functions are also run in priority order, but post-link functions are run in reverse order. The order of directives with the same priority is <em>undefined</em>. The default priority is <code>0</code>.</blockquote>

*   [`terminal`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1536-L1538 "Enforcing terminal priority - AngularJS on GitHub") This prevents further processing of directives.</p>

<blockquote>If set to true then the current <code>priority</code> will be the last set of directives which will execute (any directives at the current priority will still execute as the order of execution on same <code>priority</code> is <em>undefined</em>).</blockquote>

## Transcluding For Much Win

*   [`transclude`](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L1572-L1609 "Transcluded directives - AngularJS on GitHub") This compiles the content of the element and makes it available to the directive.

I’ve saved the best (worst?) for last. This property allows two values, for more fun and less profit. You can set it either to <code>true</code>, which enables transclusion, or to <code>'element'</code>, in which case the whole element, including any directives defined at a lower priority, get transcluded.

At a high level, transclusion allows the consumer of a directive to define a snippet of HTML, which can then be included into some part of the directive, using an <code>ng-transclude</code> directive. This sounds way too complicated, and it’s only kind of complicated. An example might make things clearer.</p>

<pre><code class="language-javascript">angular.module('PonyDeli').directive('transclusion', function () {
  return {
    restrict: 'E',
    template:
      '&lt;div ng-hide="hidden" class="transcluded"&gt;' +
        '&lt;span ng-transclude&gt;&lt;/span&gt;' +
        '&lt;span ng-click="hidden=true" class="close"&gt;Close&lt;/span&gt;' +
      '&lt;/div&gt;',
    transclude: true
  };
});
</code></pre>

<pre><code class="language-markup">&lt;body ng-app='PonyDeli'&gt;
  &lt;transclusion&gt;
    &lt;span&gt;The plot thickens!&lt;/span&gt;
  &lt;/transclusion&gt;
&lt;/body&gt;
</code></pre>

You can <a title="Basic Transclusion on CodePen" href="https://codepen.io/bevacqua/pen/rlmwB">check it out on CodePen</a>, of course. What happens when you try to get scopes into the mix? Well, the content that gets transcluded inside the directive will still respond to the parent content, correctly, even though it’s placed inside the directive and even if the directive presents an isolate scope. This is what you’d expect because the transcluded content is defined in the consuming code, which belongs to the parent scope, and not the directive’s scope. The directive still binds to its local scope, as usual.</p>

<pre><code class="language-javascript">var deli = angular.module('PonyDeli', []);

deli.controller('foodCtrl', function ($scope) {
  $scope.message = 'The plot thickens!';
});

deli.directive('transclusion', function () {
  return {
    restrict: 'E',
    template:
      '&lt;div ng-hide="hidden" class="transcluded"&gt;' +
        '&lt;span ng-transclude&gt;&lt;/span&gt;' +
        '&lt;span ng-click="hidden=true" class="close" ng-bind="close"&gt;&lt;/span&gt;' +
      '&lt;/div&gt;',
    transclude: true,
    scope: {},
    link: function (scope) {
      scope.close = 'Close';
    }
  };
});
</code></pre>

<pre><code class="language-markup">&lt;body ng-app='PonyDeli' ng-controller='foodCtrl'&gt;
  &lt;transclusion&gt;
    &lt;span ng-bind='message'&gt;&lt;/span&gt;
  &lt;/transclusion&gt;
&lt;/body&gt;
</code></pre>

You can <a title="Transcluded Scopes on CodePen" href="https://codepen.io/bevacqua/pen/lFHoE">find that one on CodePen</a> as well. There you have it: transclusion, demystified.</p>

### Further Reading

Here are some additional resources you can read to extend your comprehension of AngularJS.

*   “[AngularJS’ Internals in Depth, Part 1](https://www.smashingmagazine.com/2015/01/22/angularjs-internals-in-depth/ "AngularJS Internals in Depth, Part 1"),” Nicolas Bevacqua, Smashing Magazine
*   “AngularJS : When writing a directive, how do I decide if a need no new scope, a new child scope, or a new isolate scope?,” StackOverflow
*   “[Transclusion Basics](https://egghead.io/lessons/angularjs-transclusion-basics "AngularJS Transclusion Basics - Egghead.io")” (screencast), John Lindquist, Egghead.io
*   “AngularJS : When to use transclude 'true' and transclude 'element'?,” StackOverflow
*   “[Understanding AngularJS Directives Part 1: Ng-repeat and Compile](https://liamkaufman.com/blog/2013/05/13/understanding-angularjs-directives-part1-ng-repeat-and-compile/ "Understanding AngularJS Directives Part 1: ng-repeat and Compile"),” Liam Kaufman

Please comment on any issues regarding this article, so that everyone can benefit from your feedback. Also, you should <a title="@nzgb on Twitter" href="https://twitter.com/nzgb">follow me on Twitter</a>!

{{< signature "al, ml" >}}


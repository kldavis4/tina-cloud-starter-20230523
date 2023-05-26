---
title: AngularJS' Internals In Depth
slug: angularjs-internals-in-depth
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a797a397-c040-4e9e-9766-e18420d9e306/event-loop-illu-opt.png
date: 2015-01-22T23:03:22.000Z
author: nicolasbevacqua
description: >-
  AngularJS presents a remarkable number of interesting design choices in its
  code base. Two particularly interesting cases are the way in which scopes work
  and how directives behave.

  The first thing anyone is taught when approaching AngularJS for the first time
  is that directives are meant to interact with the DOM, or whatever manipulates
  the DOM for you, such as jQuery ([get over jQuery
  already](https://ponyfoo.com/articles/getting-over-jquery)!). What immediately
  becomes _(and remains)_ confusing for most, though, is the **interaction
  between scopes, directives and controllers**.
categories:
  - Coding
  - Mobile
  - JavaScript
  - Angular
---
AngularJS presents a remarkable number of interesting design choices in its code base. Two particularly interesting cases are the way in which scopes work and how directives behave.

The first thing anyone is taught when approaching AngularJS for the first time is that directives are meant to interact with the DOM, or whatever manipulates the DOM for you, such as jQuery (<a href="https://ponyfoo.com/articles/getting-over-jquery">get over jQuery already</a>!). What immediately becomes <i>(and remains)</i> confusing for most, though, is the <strong>interaction between scopes, directives and controllers</strong>.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [AngularJS’ Internals In Depth, Part 2](https://www.smashingmagazine.com/2015/11/angularjs-internals-in-depth-part-2/)
*   [An Introduction To Unit Testing In AngularJS Applications](https://www.smashingmagazine.com/2014/10/introduction-to-unit-testing-in-angularjs/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Automating Style Guide-Driven Development](https://www.smashingmagazine.com/2015/03/automating-style-guide-driven-development/)

After the confusion sets in, you start learning about the advanced concepts: the digest cycle, isolate scopes, transclusion and the different linking functions in directives. These are mind-blowingly complex as well. I won’t cover directives in this article, but they’ll be addressed in its follow-up.

{{% feature-panel %}}

This article will navigate the salt marsh that is AngularJS scopes and the lifecycle of an AngularJS application, while providing an amusingly informative, in-depth read.

(The bar is high, but scopes are sufficiently hard to explain. If I’m going to fail miserably at it, at least I’ll throw in a few more promises I can’t keep!)

If the following figure looks unreasonably mind-bending, then this article might be for you.</p>

<figure><a href="https://github.com/angular/angular.js/wiki/Understanding-Scopes"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9b0a1dfa-0f78-4b86-b555-2c7217f3528c/01-mindbender.png" alt="01-mindbender" width="364" height="279" /></a><figcaption>(<a href="https://github.com/angular/angular.js/wiki/Understanding-Scopes">Image credit</a>) (<a>View large version</a>)</figcaption></figure>

(Disclaimer: This article is based on <a href="https://github.com/angular/angular.js/tree/v1.3.0">AngularJS version 1.3.0</a>.)

AngularJS uses scopes to abstract communication between directives and the DOM. Scopes also exist at the controller level. Scopes are plain old JavaScript objects (POJO) that AngularJS does not heavily manipulate. They only add a bunch of “internal” properties, prefixed with one or two <code>$</code> symbols. The ones prefixed with <code>$$</code> aren’t necessary as frequently, and using them is often a code smell, which can be avoided by having a deeper understanding of the digest cycle.</p>

## What Kind Of Scopes Are We Talking About?

In AngularJS slang, a “scope” is not what you might be used to when thinking about JavaScript code or even programming in general. Usually, scopes are used to refer to the bag in a piece of code that holds the context, variables and so on.

(In most languages, variables are held in imaginary bags, which are defined by curly braces (<code>{}</code>) or code blocks. This is known as “<a href="https://en.wikipedia.org/wiki/Scope_(computer_science)#Block_scope">block scoping</a>.” JavaScript, in contrast, deals in “<a href="https://en.wikipedia.org/wiki/Scope_(computer_science)#Lexical_scoping">lexical scoping</a>,” which pretty much means that the bags are defined by functions, or the global object, rather than by code blocks. Bags may contain any number of smaller bags. Each bag can access the candy (sweet, sweet variables) inside its parent bag (and in its parent’s parent, and so on), but they can’t poke holes in smaller, or child, bags.)

As a quick and dirty example, let’s examine the function below.</p>

<pre><code class="language-javascript">
function eat (thing) {
   console.log('Eating a ' + thing);
}

function nuts (peanut) {
   var hazelnut = 'hazelnut';

   function seeds () {
      var almond = 'almond';
      eat(hazelnut); // I can reach into the nuts bag!
   }

   // Almonds are inaccessible here.
   // Almonds are not nuts.
}
</code></pre>

I won’t dwell on <a href="https://ponyfoo.com/articles/where-does-this-keyword-come-from"><code>this</code> matter</a> any longer, because these are not the scopes people refer to when talking about AngularJS. Refer to “<a href="https://ponyfoo.com/articles/where-does-this-keyword-come-from">Where Does <code>this</code> Keyword Come From?</a>” if you’d like to learn more about scopes in the context of the JavaScript language.</p>

### Scope Inheritance in AngularJS

Scopes in AngularJS are also context, but on AngularJS’ terms. In AngularJS, a scope is associated with an element (and all of its child elements), while an element is not necessarily directly associated with a scope. Elements are assigned a scope is one of the following three ways.

The first way is if a scope is created on an element by a controller or a directive (directives don’t always introduce new scopes).</p>

<pre><code class="language-markup">
&lt;nav ng-controller='menuCtrl'&gt;
</code></pre>

Secondly, if a scope isn’t present on the element, then it’s inherited from its parent.</p>

<pre><code class="language-markup">
&lt;nav ng-controller='menuCtrl'&gt;
   &lt;a ng-click='navigate()'&gt;Click Me!&lt;/a&gt; &lt;!-- also &lt;nav&gt;'s scope --&gt;
&lt;/nav&gt;
</code></pre>

Thirdly, if the element isn’t part of an <code>ng-app</code>, then it doesn’t belong to a scope at all.</p>

<pre><code class="language-markup">
&lt;head&gt;
   &lt;h1&gt;Pony Deli App&lt;/h1&gt;
&lt;/head&gt;
&lt;main ng-app='PonyDeli'&gt;
   &lt;nav ng-controller='menuCtrl'&gt;
      &lt;a ng-click='navigate()'&gt;Click Me!&lt;/a&gt;
   &lt;/nav&gt;
&lt;/main&gt;
</code></pre>

To figure out an element’s scope, try to think of elements <strong>recursively inside out</strong> following the three rules I’ve just outlined. Does it create a new scope? That’s its scope. Does it have a parent? Check the parent, then. Is it not part of an <code>ng-app</code>? Tough luck — no scope.

You can (and most definitely should) use the magic of developer tools to easily figure out the scope of an element.</p>

### Pulling Up AngularJS’ Internal Scope Properties

I’ll walk through a few properties in a typical scope to introduce certain concepts, before moving on to explaining how digests work and behave internally. I’ll also let you in on how I get to these properties. First, I’ll open Chrome and navigate to the application I’m working on, which is written in AngularJS. Then, I’ll inspect an element and open the developer tools.

(Did you know that <a href="https://developers.google.com/chrome-developer-tools/docs/commandline-api#0_-_4"><code>$0</code> gives you access to the last selected element</a> in the “Elements” pane? <code>$1</code> gives you access to the previously selected element, and so on. I prognosticate that you’ll use <code>$0</code> the most, particularly when working with AngularJS.)

For any given DOM element, <code>angular.element</code> wraps that in either <a href="https://jquery.com/">jQuery</a> or jqLite, jQuery’s <a href="https://github.com/angular/angular.js/blob/caed2dfe4feeac5d19ecea2dbb1456b7fde21e6d/src/jqLite.js">own little mini version</a>. Once it’s wrapped, you get access to a <code>scope()</code> function that returns — you guessed it! — the AngularJS scope associated with that element. Combining that with <code>$0</code>, I find myself using the following command quite often.</p>

<pre><code class="language-javascript">
angular.element($0).scope()
</code></pre>

(Of course, if you know that you’ll be using jQuery, then <code>$($0).scope()</code> will work just the same. And <code>angular.element</code> works every time, regardless of whether jQuery is available.)

Then, I’m able to inspect the scope, assert that it’s the scope I expected, and assert whether the property’s values match what I was expecting. Super-useful! Let’s see what special properties are available in a typical scope, those prefixed with one or more dollar signs.</p>

<pre><code class="language-javascript">
for(o in $($0).scope())o[0]=='$'&amp;&amp;console.log(o)
</code></pre>

That’s good enough. I’ll go over all of the properties, clustering them by functionality, and go over each portion of AngularJS’ scoping philosophy.

## Examining A Scope’s Internals In AngularJS

Below, I’ve listed the properties yielded by that command, grouped by area of functionality. Let’s start with the basic ones, which merely provide scope navigation.

*   `[$id](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L127)` uniquely identifies the scope
*   `[$root](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L131)` root scope
*   `[$parent](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L217)` parent scope, or `null` if `scope == scope.$root`
*   `[$$childHead](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L223)` first child scope, if any, or `null`
*   `[$$childTail](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L221)` last child scope, if any, or `null`
*   `[$$prevSibling](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L218)` previous sibling scope, if any, or `null`
*   `[$$nextSibling](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L220)` next sibling scope, if any, or `null`

No surprises here. Navigating scopes like this would be utter nonsense. Sometimes accessing the <code>$parent</code> scope might seem appropriate, but there are always better, less coupled, ways to deal with parental communication than by tightly binding people scopes together. One such way is to use event listeners, our next batch of scope properties!

### Event Model in AngularJS Scope

The properties described below enable us to publish events and subscribe to them. This is a pattern known as <a href="https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern">PubSub</a>, or just events.

*   `[$$listeners](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L1092)` event listeners registered on the scope
*   `[$on(evt, fn)](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L1089-L1109)` attaches an event listener `fn` named `evt`
*   `[$emit(evt, args)](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L1134-L1182)` fires event `evt`, roaring upward on the scope chain, triggering on the current scope and all `$parent`s, including the `$rootScope`
*   `[$broadcast(evt, args)](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L1206-L1258)` fires event `evt`, triggering on the current scope and all of its children

When triggered, event listeners are passed an <code>event</code> object and any arguments passed to the <code>$emit</code> or <code>$broadcast</code> function. There are many ways in which scope events can provide value.

A directive might use events to announce that something important has happened. Check out the sample directive below, where a button can be clicked to announce that you feel like eating food of some type.</p>

<pre><code class="language-javascript">
angular.module('PonyDeli').directive('food', function () {
   return {
      scope: { // I'll come back to directive scopes later
         type: '=type'
      },
      template: '&lt;button ng-click="eat()"&gt;I want to eat some {{type}}!&lt;/button&gt;',
      link: function (scope, element, attrs) {
         scope.eat = function () {
            letThemHaveIt();
            scope.$emit('food.order, scope.type, element);
         };

         function letThemHaveIt () {
            // Do some fancy UI things
         }
      }
   };
});
</code></pre>

I namespace my events, and so should you. It prevents name collisions, and it makes clear where events originate from or what event you’re subscribing to. Imagine you have an interest in analytics and want to track clicks on <code>food</code> elements using <a href="https://mixpanel.com/">Mixpanel</a>. That would actually be a reasonable need, and there’s no reason why that should be polluting your directive or your controller. You could put together a directive that does the food-clicking analytics-tracking for you, in a nicely self-contained manner.</p>

<pre><code class="language-javascript">
angular.module('PonyDeli').directive('foodTracker', function (mixpanelService) {
   return {
      link: function (scope, element, attrs) {
         scope.$on('food.order, function (e, type) {
            mixpanelService.track('food-eater', type);
         });
      }
   };
});
</code></pre>

The service implementation is not relevant here, because it would merely wrap Mixpanel’s client-side API. The HTML would look like what’s below, and I’ve thrown in a controller to hold all of the food types that I want to serve in my deli. The <a href="https://github.com/angular/angular.js/blob/v1.3.0/src/Angular.js#L1293"><code>ng-app</code></a> directive helps AngularJS to auto-bootstrap my application as well. Rounding out the example, I’ve added an <code>ng-repeat</code> directive so that I can render all of my food without repeating myself; it’ll just loop through <code>foodTypes</code>, available on <code>foodCtrl</code>’s scope.</p>

<pre><code class="language-markup">
&lt;ul ng-app='PonyDeli' ng-controller='foodCtrl' food-tracker&gt;
   &lt;li food type='type' ng-repeat='type in foodTypes'&gt;&lt;/li&gt;
&lt;/ul&gt;

angular.module('PonyDeli').controller('foodCtrl', function ($scope) {
   $scope.foodTypes = ['onion', 'cucumber', 'hazelnut'];
});
</code></pre>

The fully working example is <a href="https://codepen.io/bevacqua/pen/qmBGd">hosted on CodePen</a>.

That’s a good example on paper, but you need to think about whether you need an event that anyone can subscribe to. Maybe a service will do? In this case, it could go either way. You could argue that you’ll need events because you don’t know who else is going to subscribe to <code>food.order</code>, which means that using events would be more future-proof. You could also say that the <code>food-tracker</code> directive doesn’t have a reason to be, because it doesn’t interact with the DOM or even the scope at all other than to listen to an event, which you could replace with a service.

Both thoughts would be correct, in the given context. As more components need to be <code>food.order</code>-aware, then it might feel clearer that events are the way to go. In reality, though, events are most useful when you actually need to bridge the gap between two (or more) scopes and other factors aren’t as important.

As we’ll see when we inspect directives more closely in the upcoming second part of this article, events aren’t even necessary for scopes to communicate. A child scope may read from its parent by binding to it, and it may also update those values.

(There’s rarely a good reason to host events to help children communicate better with their parents.)

Siblings often have a harder time communicating with each other, and they often do so through a common parent. That generally translates into broadcasting from <code>$rootScope</code> and listening on the siblings of interest, as below.</p>

<pre><code class="language-markup">
&lt;body ng-app='PonyDeli'&gt;
   &lt;div ng-controller='foodCtrl'&gt;
      &lt;ul food-tracker&gt;
         &lt;li food type='type' ng-repeat='type in foodTypes'&gt;&lt;/li&gt;
      &lt;/ul&gt;
      &lt;button ng-click='deliver()'&gt;I want to eat that!&lt;/button&gt;
   &lt;/div&gt;
   &lt;div ng-controller='deliveryCtrl'&gt;
      &lt;span ng-show='received'&gt;
         A monkey has been dispatched. You shall eat soon.
      &lt;/span&gt;
   &lt;/div&gt;
&lt;/body&gt;

angular.module('PonyDeli').controller('foodCtrl', function ($rootScope) {
   $scope.foodTypes = ['onion', 'cucumber', 'hazelnut'];
   $scope.deliver = function (req) {
      $rootScope.$broadcast('delivery.request', req);
   };
});

angular.module('PonyDeli').controller('deliveryCtrl', function ($scope) {
   $scope.$on('delivery.request', function (e, req) {
      $scope.received = true; // deal with the request
   });
});
</code></pre>

This one is <a href="https://codepen.io/bevacqua/pen/CzGla">also on CodePen</a>.

Over time, you’ll learn to lean towards events or services accordingly. I could say that you should use events when you expect view models to change in response to <code>event</code> and that you ought to use services when you don’t expect changes to view models. Sometimes the response is a mixture of both: an action triggers an event that calls a service, or a service that broadcasts an event on <code>$rootScope</code>. It depends on the situation, and you should analyze it as such, rather than attempting to nail down the elusive one-size-fits-all solution.

If you have two components that communicate through <code>$rootScope</code>, then you might prefer to use <code>$rootScope.$emit</code> (rather than <code>$broadcast</code>) and <code>$rootScope.$on</code>. That way, the event would only spread among <code>$rootScope.$$listeners</code>, and it wouldn’t waste time looping through every child of <code>$rootScope</code>, which you just know won’t have any listeners for that event. Below is an example service using <code>$rootScope</code> to provide events without limiting itself to a particular scope. It provides a <code>subscribe</code> method that allows consumers to register event listeners, and it might do things internally that trigger that event.</p>

<pre><code class="language-javascript">
angular.module('PonyDeli').factory("notificationService", function ($rootScope) {
   function notify (data) {
      $rootScope.$emit("notificationService.update", data);
   }

   function listen (fn) {
      $rootScope.$on("notificationService.update", function (e, data) {
         fn(data);
      });
   }

   // Anything that might have a reason
   // to emit events at later points in time
   function load () {
      setInterval(notify.bind(null, 'Something happened!'), 1000);
   }

   return {
      subscribe: listen,
      load: load
   };
});
</code></pre>

You guessed right! This one is <a href="https://codepen.io/bevacqua/pen/HsBCa">also on CodePen</a>.

Enough events-versus-services banter. Shall we move on to some other properties?

### Digesting Changesets

Understanding this intimidating process is the key to understanding AngularJS.

AngularJS bases its data-binding features in a dirty-checking loop that tracks changes and fires events when these change. This is simpler than it sounds. No, really. It is! Let’s quickly go over each of the core components of the <code>$digest</code> cycle. First, there’s the <code>scope.$digest</code> method, which recursively digests changes in a scope and its children.

1.  `[$digest()](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L710)` executes the `$digest` dirty-checking loop
2.  `[$$phase](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L1271)` current phase in the digest cycle, one of `[null, '$apply', '$digest']`

You need to be careful about triggering digests, because attempting to do so when you’re already in a digest phase would cause AngularJS to blow up in a mysterious haze of unexplainable phenomena. In other words, pinpointing the root cause of the issue would be pretty hard.

Let’s look at <a href="https://docs.angularjs.org/api/ng.$rootScope.Scope#methods_$digest">what the documentation says</a> about <code>$digest</code>.
<blockquote>Processes all of the <a title="$watch on AngularJS documentation" href="https://docs.angularjs.org/api/ng.$rootScope.Scope#methods_$watch">watchers</a> of the current scope and its children. Because a <a title="$watch on AngularJS documentation" href="https://docs.angularjs.org/api/ng.$rootScope.Scope#methods_$watch">watcher</a>’s listener can change the model, the <a title="$digest on AngularJS documentation" href="https://docs.angularjs.org/api/ng.$rootScope.Scope#methods_$digest">$digest()</a> keeps calling the <a title="$watch on AngularJS documentation" href="https://docs.angularjs.org/api/ng.$rootScope.Scope#methods_$watch">watchers</a> until no more listeners are firing. This means that it is possible to get into an infinite loop. This function will throw <code>'Maximum iteration limit exceeded.'</code> if the number of iterations exceeds 10.

Usually, you don’t call <a title="$digest on AngularJS documentation" href="https://docs.angularjs.org/api/ng.$rootScope.Scope#methods_$digest">$digest()</a> directly in <a title="ng-controller on AngularJS documentation" href="https://docs.angularjs.org/api/ng.directive:ngController">controllers</a> or in <a title="Directives on AngularJS documentation" href="https://docs.angularjs.org/api/ng.$compileProvider#methods_directive">directives</a>. Instead, you should call <a title="$apply on AngularJS documentation" href="https://docs.angularjs.org/api/ng.$rootScope.Scope#methods_$apply">$apply()</a> (typically from within a <a title="Directives on AngularJS documentation" href="https://docs.angularjs.org/api/ng.$compileProvider#methods_directive">directives</a>), which will force a <a title="$digest on AngularJS documentation" href="https://docs.angularjs.org/api/ng.$rootScope.Scope#methods_$digest">$digest()</a>.</blockquote>

So, a <code>$digest</code> processes all watchers, and then processes the watchers that those watchers trigger, until nothing else triggers a watch. Two questions remain to be answered for us to understand this loop.

*   What the hell is a “watcher”?!
*   What triggers a `$digest`?!

The answers to these questions vary wildly in terms of complexity, but I’ll keep my explanations as simple as possible so that they’re clear. I’ll begin talking about watchers and let you draw your own conclusions.

If you’ve read this far, then you probably already know what a watcher is. You’ve probably used <a href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L356"><code>scope.$watch</code></a>, and maybe even used <a href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L530"><code>scope.$watchCollection</code></a>. The <code>$$watchers</code> property has all of the watchers on a scope.

*   `[$watch(watchExp, listener, objectEquality)](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L356)` adds a watch listener to the scope
*   `[$watchCollection](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L530)` watches array items or object map properties
*   `[$$watchers](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L383)` contains all of the watches associated with the scope

Watchers are the single most important aspect of an AngularJS application’s data-binding capabilities, but AngularJS needs our help in order to trigger those watchers; otherwise, it can’t effectively update data-bound variables appropriately. Consider the following example.</p>

<pre><code class="language-markup">
&lt;body ng-app='PonyDeli'&gt;
   &lt;ul ng-controller='foodCtrl'&gt;
      &lt;li ng-bind='prop'&gt;&lt;/li&gt;
      &lt;li ng-bind='dependency'&gt;&lt;/li&gt;
   &lt;/ul&gt;
&lt;/body&gt;

angular.module('PonyDeli').controller('foodCtrl', function ($scope) {
   $scope.prop = 'initial value';
   $scope.dependency = 'nothing yet!';

   $scope.$watch('prop', function (value) {
      $scope.dependency = 'prop is "' + value + '"! such amaze';
   });

   setTimeout(function () {
      $scope.prop = 'something else';
   }, 1000);
});
</code></pre>

So, we have <code>'initial value'</code>, and we’d expect the second HTML line to change to <code>'prop is "something else"! such amaze'</code> after a second, right? Even more interesting, you’d at the very least expect the first line to change to <code>'something else'</code>! Why doesn’t it? That’s not a watcher… or is it?

Actually, a lot of what you do in the HTML markup ends up creating a watcher. In this case, <a href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/directive/ngBind.js#L54-L68">each <code>ng-bind</code> directive created a watcher</a> on the property. It will update the HTML of the <code>&lt;li&gt;</code> whenever <code>prop</code> and <code>dependency</code> change, similar to how our watch will change the property itself.

This way, you can now think of your code as having three watches, one for each <code>ng-bind</code> directive and the one in the controller. How is AngularJS supposed to know that the property is updated after the timeout? You could remind AngularJS of an update to the property by adding a manual digest to the <code>timeout</code> callback.</p>

<pre><code class="language-javascript">
setTimeout(function () {
   $scope.prop = 'something else';
   $scope.$digest();
}, 1000);
</code></pre>

I’ve set up a CodePen <a href="https://codepen.io/bevacqua/pen/lLbtI">without the <code>$digest</code></a>, and one that <a href="https://codepen.io/bevacqua/pen/vwDoz">does <code>$digest</code></a> after the timeout. The more <a href="https://ponyfoo.com/articles/the-angular-way">AngularJS way</a> to do it, however, would be to use the <a href="https://github.com/angular/angular.js/blob/v1.3.0/src/ng/timeout.js#L35"><code>$timeout</code> service</a> instead of <code>setTimeout</code>. It provides some error-handling, and it executes <code>$apply()</code>.</p>

<pre><code class="language-javascript">
$timeout(function () {
   $scope.prop = 'something else';
}, 1000);
</code></pre>

*   `[$apply(expr)](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L1018-L1033)` parses and evaluates an expression and then executes the `$digest` loop on `$rootScope`

In addition to executing the digest on every scope, <code>$apply</code> provides error-handling functionality as well. If you’re trying to tune performance, then using <code>$digest</code> might be warranted, but I’d stay away from it until you feel really comfortable with how AngularJS works internally. One would actually need to call <code>$digest()</code> manually very few times; <code>$apply</code> is almost always a better choice.

We’re back to the second question now.

*   What triggers a `$digest`?!

Digests are triggered internally in strategic places all over AngularJS’ code base. They are triggered either directly or by calls to <code>$apply()</code>, like we’ve observed in the <code>$timeout</code> service. Most directives, both those found in AngularJS’ core and those out in the wild, trigger digests. Digests fire your watchers, and watchers update your UI. That’s the basic idea anyway.

You will find a pretty good resource with best practices in the AngularJS wiki, which is linked to at the bottom of this article.

I’ve explained how watches and the <code>$digest</code> loop interact with each other. Below, I’ve listed properties related to the <code>$digest</code> loop that you can find on a scope. These help you to parse text expressions through AngularJS’ compiler or to execute pieces of code at different points in the digest cycle.

*   `[$eval(expression, locals)](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L922-L924)` parse and evaluate a scope expression immediately
*   `[$evalAsync(expression)](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L955-L967)` parse and evaluate an expression at a later point in time
*   `[$$asyncQueue](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L736-L744)` async task queue, consumed on every digest
*   `[$$postDigest(fn)](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L969-L971)` executes `fn` after the next digest cycle
*   `[$$postDigestQueue](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L970)` methods registered with `$$postDigest(fn)`

Phew! That’s it. It wasn’t that bad, was it?

### The Scope Is Dead! Long Live the Scope!

Here are the last few, rather dull-looking, properties in a scope. They deal with the scope’s life cycle and are mostly used for internal purposes, although you may want to <code>$new</code> scopes by yourself in some cases.

*   `[$$isolateBindings](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/compile.js#L756)` isolate scope bindings (for example, `{ options: '@megaOptions' }` — very internal
*   `[$new(isolate)](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L193)` creates a child scope or an `isolate` scope that won’t inherit from its parent
*   `[$destroy](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L857)` removes the scope from the scope chain; scope and children won’t receive events, and watches won’t fire anymore
*   `[$$destroyed](https://github.com/angular/angular.js/blob/v1.3.0/src/ng/rootScope.js#L863)` has the scope been destroyed?

Isolate scopes? What is this madness? The second part of this article is dedicated to directives, and it covers <code>isolate</code> scopes, transclusion, linking functions, compilers, directive controllers and more. Wait for it!

### Further Reading

Here are some additional resources you can read to extend your comprehension of AngularJS.

*   “[The Angular Way](https://ponyfoo.com/articles/the-angular-way),” Nicolas Bevacqua
*   “[Anti-Patterns](https://github.com/angular/angular.js/wiki/Anti-Patterns),” AngularJS, GitHub
*   “[Best Practices](https://github.com/angular/angular.js/wiki/Best-Practices),” AngularJS, GitHub
*   [TodoMVC AngularJS example](https://todomvc.com/examples/angularjs/#/)
*   [Egghead.io: Bite-Sized Video Training With AngularJS](https://egghead.io/), John Lindquist
*   [ng-newsletter](https://www.ng-newsletter.com/)
*   “Using `scope.$watch` and `scope.$apply`,” StackOverflow

Please comment on any issues regarding this article, so that everyone can benefit from your feedback.

{{< signature "ml, al" >}}


---
title: Qualities Of Good Flux Implementations
slug: qualities-of-good-flux-implementations
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7f1b30f7-11fa-4f31-8931-ea0ef72f77b7/flux-react2.png'
date: 2015-06-22T18:36:20.000Z
author: jimcowart
description: >-
  It has been an exciting year for my team. Last year we kicked off a project
  using React, and over the course of the project we've learned a lot about
  React and Flux — Facebook's recommended architectural principles for React
  apps. In this article, we'll take a look at some of the key lessons we've
  learned.

  Whether you're new to React and Flux, or going as far as building your own
  Flux implementation, I think you'll not only enjoy this journey with us, but
  find some **thought-provoking questions and wisdom** you can apply in your own
  endeavors.
categories:
  - Coding
  - Frameworks
  - JavaScript
---
It has been an exciting year for my team. Last year we kicked off a project using <a href="https://facebook.github.io/react/">React</a>, and over the course of the project we've learned a lot about React and <a href="https://facebook.github.io/react/blog/2014/05/06/flux.html">Flux</a> — Facebook's recommended architectural principles for React apps. In this article, we'll take a look at some of the key lessons we've learned.

Whether you're new to React and Flux, or going as far as building your own Flux implementation, I think you'll not only enjoy this journey with us, but find some <strong>thought-provoking questions and wisdom</strong> you can apply in your own endeavors.</p>

## <span class="rh">Further Reading</span> on SmashingMag

*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)
*   [Notes On Client-Rendered Accessibility](https://www.smashingmagazine.com/2015/05/client-rendered-accessibility/)

## Helpful Background

This post assumes you have some level of familiarity with React and Flux. Already familiar with them? Feel free to skip to "Introducing Lux.js" section. Otherwise, I recommend reading through the links below.

{{% feature-panel %}}

### React

<a href="https://facebook.github.io/react/">React</a> is an open-source JavaScript library, maintained mainly by Facebook, and intended to be used in large applications that use data that changes over time. Obviously this is especially helpful when developing <strong>single-page applications</strong>. If you're familiar with the <em>model-view-controller</em> pattern, React is considered to be only the <em>view</em>, handling the user interface in an app, and can be used in conjunction with other JavaScript libraries or larger MVC frameworks. Here's a high level summary of React:

*   React focuses on _view_ concerns, and does not attempt to be an "everything framework"
*   React UIs are built out of components.
*   React components can be written using [JSX](https://facebook.github.io/react/docs/jsx-in-depth.html) — an XML-based extension to JavaScript — or with plain JavaScript.
*   React components render to a virtual DOM. Subsequent renders are "diffed" with the previous render, and the minimum number of DOM mutations are executed to effectively patch the DOM to bring it up to date.

Check out Facebook's <a href="https://facebook.github.io/react/docs/getting-started.html">Getting Started</a> guide.</p>

### Flux

<a href="https://facebook.github.io/flux/">Flux</a> is an <strong>architectural pattern</strong> recommended by Facebook for building apps with React. Whereas React's opinions <em>nudge</em> you towards unidirectional data flow, Flux provides a fuller picture as to what that <em>actually</em> looks like. Several Flux implementations have arisen (LeanKit's <a href="https://github.com/LeanKit-Labs/lux.js">lux.js</a>, included), providing a fascinating insight into how different teams are tackling the challenges they face. A high-level summary of Flux would include:

*   Flux apps have three main abstractions: views (React components), stores, and the dispatcher.
*   Views "propagate" actions (e.g. user interaction) through the dispatcher.
*   The dispatcher handles notifying the various stores of the action.
*   If a store's state changes, it emits a change event, and views depending on that store for state will rerender.

Check out Facebook's <a href="https://facebook.github.io/flux/docs/overview.html#content">overview of Flux</a>.</p>

## Introducing Lux.js

JavaScript developers crank out new frameworks as fast as a politician making promises at a campaign rally. Why, then, write another framework? I love this subject, though it falls outside the scope of this article. <a href="https://github.com/LeanKit-Labs/lux.js">Lux.js</a> is an <strong>implementation of the Flux architecture</strong> using React; we've tailored it to fit our team's specific set of needs, skills and goals. In fact, our work with lux attempts to strike a delicate balance between consistent opinions and flexibility to include other libraries that best solve the problem at hand.

Over time, failing and succeeding in quite a few projects, we've found the following qualities to be the drivers of success in our own flux implementation:

1.  Don't get in React's way.
2.  Continuously eliminate boilerplate.
3.  Treat every input as an action.
4.  Store operations _must_ be synchronous.
5.  Make it easy to play well with non-lux/non-React instances.</p>

### Examples

Dmitri Voronianski created <a href="https://github.com/voronianski/flux-comparison">flux-comparison</a>, which lets you see a <strong>side-by-side comparison</strong> of several flux variants (using a basic shopping cart example). I've implemented the same example using lux to help illustrate the explanations along the way. I highly recommend checking this project out — it's a great way to quickly familiarize yourself with several leading Flux implementations.

OK, with all that out of the way, let's look closer at the qualities I mentioned above.</p>

## Staying Out Of The Way

React does a great job at focusing only on what it aims to solve. By not being prescriptive on broader things like remote data communications (HTTP, WebSockets), and by providing hooks that enable you to incorporate non-React UI libraries, React gives you the opportunity to assemble the tools that best address the needs of your app. Just as React stays out of the way of concerns it doesn't solve for, we've found it's equally important to stay out of React's way. It's easy to get in the way as you begin <strong>abstracting common patterns</strong> in how you use another library/framework behind your own API. (Note: this isn't always a bad thing!) For example, let's look at the common component behaviors we've built into lux, and how our usage of them has evolved.</p>

### Controller Views

You will often hear React developers refer to <em>controller views</em> — a React component that typically sits at or near the top of a section of the page, which listens to one or more stores for changes in their state. As stores emit change events, the controller view updates with the new state and <strong>passes changes down to its children</strong> via props.

lux provides a <code>controllerView</code> method that gives you back a React component capable of listening to lux stores. Under the hood, lux uses mixins to give the React components different behaviors, and the <code>controllerView</code> method gives a component both a <code>store</code> mixin (making it capable of listening to stores), and an ActionCreator mixin (making it capable of publishing actions). For example:

<pre><code class="language-javascript">var CartContainer = lux.controllerView({

  getActions: [ "cartCheckout" ],

  stores: {
    listenTo: [ "cart" ],
    onChange: function() {
      this.setState(getStateFromStores());
    }
  },

  getInitialState: function () {
    return getStateFromStores();
  },

  onCheckoutClicked: function () {
    var products = this.state.products;
    if (!products.length) {
      return;
    }
    this.cartCheckout(products);
  },

  render: function () {
    return (
      &lt;Cart products={this.state.products} total={this.state.total} onCheckoutClicked={this.onCheckoutClicked} /&gt;
    );
  }
});
</code></pre>

While we still like this convenient approach, we've found ourselves moving to the alternative approach of setting up a plain React component, and passing the lux mixins necessary to achieve the same result. Note that here we're calling <code>React.createClass</code> and using the <code>mixins</code> option:

<pre><code class="language-javascript">var CartContainer = React.createClass({

  mixins: [ lux.reactMixin.store, lux.reactMixin.actionCreator ],

  getActions: [ "cartCheckout" ],

  stores: {
    listenTo: [ "cart" ],
    onChange: function() {
      this.setState(getStateFromStores());
    }
  },

  // other methods, etc.
});
</code></pre>

Either approach is valid, though we feel the second approach is more out of React's way. Why?

*   We get a component's `displayName` for free (as the JSX transformer will use our `var` name when it sees `React.createClass`).
*   Some controller views don't need to be ActionCreators. The second approach means we could only pass the `store` mixin in those cases, keeping concerns focused. The first approach always gives the component both mixins, even if not used.
*   There's no need to explicitly pass the React instance to lux (done via `lux.initReact( React )`) so that it knows how to create components.

Note: Why spend time explaining these two different approaches? It's about staying out of React's way. We can easily fall prey to either over- or underabstracting, thus we need to give ourselves room to adapt as our understanding improves. The evolution of our approach over time has been informed as we've asked ourselves what makes a good flux implementation. This process of continually questioning and evaluating is a vital part of the life of any library or framework.

## Boilerplate Elimination

In our experience, adopting React and Flux has moved infrastructure and framework concerns into the background so we can focus on <em>actually creating features for our app</em>. Still, there are annoying bits of code that tend to crop up a lot. For example, consider this common approach to wiring/unwiring components to listen to store change events:

<pre><code class="language-javascript">// Taken from the facebook-flux example:
// https://github.com/voronianski/flux-comparison/blob/master/facebook-flux/js/components/CartContainer.jsx
var CartContainer = React.createClass({
  // only showing the methods we're interested in

  componentDidMount: function () {
    CartStore.addChangeListener(this._onChange);
  },

  componentWillUnmount: function () {
    CartStore.removeChangeListener(this._onChange);
  },

  // more methods, etc.
});
</code></pre>

Honestly, the boilerplate tax isn't high here, but it's still present. Since mixins can provide component life cycle methods, we made this automatic when you include lux mixins:

<pre><code class="language-javascript">
var ProductsListContainer = React.createClass({

  mixins: [ lux.reactMixin.store ],

  stores: {
    listenTo: [ "products" ],
    onChange: function() {
      this.setState(getAllProducts());
    }
  },

  // more methods, etc.
});
</code></pre>

When our <code>ProductsListContainer</code> stands up, it will be ready to listen to any of the store namespaces provided in the <code>stores.listenTo</code> array, and those subscriptions will be removed if the component unmounts. Goodbye boilerplate!

### ActionCreator Boilerplate

In Flux apps, you'll usually see dedicated ActionCreator modules like this:

<pre><code class="language-javascript">// snippet from: https://github.com/voronianski/flux-comparison/blob/master/facebook-flux/js/actions/ActionCreators.js
var ActionsCreators = exports;

ActionsCreators.receiveProducts = function (products) {
  AppDispatcher.handleServerAction({
    type: ActionTypes.RECEIVE_PRODUCTS,
    products: products
  });
};

ActionsCreators.addToCart = function (product) {
  AppDispatcher.handleViewAction({
    type: ActionTypes.ADD_TO_CART,
    product: product
  });
};
</code></pre>

As we regularly asked what repeated code we could eliminate and replace with convention, ActionCreator APIs kept coming up. In our case, we use <a href="https://github.com/postaljs/postal.js">postal.js</a> for communication between ActionCreators and the dispatcher (postal is an in-memory message bus library, providing advanced publish/subscribe functionality). 99.9% of the time, an ActionCreator method published an action message with no additional behavior. Things evolved over time like this:

<pre><code class="language-javascript">// The very early days
// `actionChannel` is a ref to a postal channel dedicated to lux Actions
var ActionCreators = {
  addToCart: function() {
    actionChannel.publish( {
      topic: "execute.addToCart",
      data: {
        actionType: ActionTypes.ADD_TO_CART,
        actionArgs: arguments
      }
    } );
  }
};
</code></pre>

That was very quickly abstracted into an ActionCreator mixin to enable this:

<pre><code class="language-javascript">// The early-ish days
var ActionCreators = lux.actionCreator({
  addToCart: function( product ) {
    this.publishAction( ActionTypes.ADD_TO_CART, product );
  }
});
</code></pre>

You'll notice two things in the code above: first, the use of <code>lux.actionCreator</code>, which mixes <code>lux.mixin.actionCreator</code> into the target; and second, the <code>publishAction</code> method (provided by the mixin).

At the same time we were using the above mixin approach, we'd fallen into the practice of having matching handler names on our stores (the handler method name matched the action type). For example, here's a lux store that handles the <code>addToCart</code> action:

<pre><code class="language-javascript">var ProductStore = new lux.Store( {

  state: { products: [] },

  namespace: "products",

  handlers: {
    addToCart: function( product ) {
      var prod = this.getState().products.find( function( p ) {
          return p.id === product.id;
      } );
      prod.inventory = prod.inventory &gt; 0 ? prod.inventory - 1 : 0;
    }
  },

  // other methods, etc.
} );
</code></pre>

Matching action type names and store handler names made conventional wire-up very simple, but we saw another area where we could eliminate boilerplate: if 99% of our ActionCreator API implementations just published a message, why not infer creation of ActionCreator APIs based on what gets handled by stores? So we did, while still allowing custom implementations of ActionCreator methods where needed. For example, when the store instance in the snippet above is created, lux will see that it handles an <code>addToCart</code> action. If an ActionCreator API hasn't already been defined for this action under <code>lux.actions</code>, lux will create one, with the default behavior of publishing the action message.

Taking this approach means our components can specify what ActionCreator methods they want in an à-la-carte style. In this next snippet, our ProductItemContainer is using the <code>lux.reactMixin.actionCreator</code> mixin, which looks for a <code>getActions</code> array, and provides the specified actions as top level methods on the component. You can see we're using the <code>addToCart</code> ActionCreator method in the <code>onAddToCartClicked</code> handler method.</p>

<pre><code class="language-javascript">var ProductItemContainer = React.createClass({

  mixins: [ lux.reactMixin.actionCreator ],

  getActions: [ "addToCart" ],

  onAddToCartClicked: function () {
    this.addToCart(this.props.product);
  },

  render: function () {
    return (
      &lt;ProductItem product={this.props.product} onAddToCartClicked={this.onAddToCartClicked} /&gt;
    );
  }
});
</code></pre>

As with any convention, there are trade-offs. Composition is an important aspect of ActionCreator APIs. They <strong>should be modeled separate from the component(s)</strong> that use them. So far, we believe this approach upholds that, while trading some of the explicit nature (e.g. keeping ActionCreators in their own module) for flexibility and terseness.</p>

## Everything Is An Action

Since this behavior of providing ActionCreator APIs was abstracted into a mixin, it made it possible for both React components as well as non-lux/React instances to use the mixin. My team has been taking advantage of this when it comes to things like remote data APIs. We're using a hypermedia client called <a href="https://github.com/LeanKit-Labs/halon">halon</a>, which understands how to consume our hypermedia resources using an extended version of <a href="https://tools.ietf.org/html/draft-kelly-json-hal-06">HAL</a> (Hypermedia Application Language, an open specification for defining the structure of HTTP resources). Covering hypermedia is beyond the scope of this article, but a number of good <a href="https://martinfowler.com/articles/richardsonMaturityModel.html">resources</a> <a href="https://phlyrestfully.readthedocs.org/en/latest/halprimer.html">exist</a> if you're interested in learning more. Our client-side wrapper for halon uses lux's <code>actionCreator</code> and <code>actionListener</code> mixins so that it can not only publish actions, but also handle them.

We approach it this way because we believe <em>every input</em> — whether it be user input or queued asynchronous execution (via Ajax, postMessage, WebSockets, etc.) — <em>should be fed into the client as an action</em>. If you've kept up with any of the React discussions over time, you might be thinking, "Jim, Facebook is OK with calling dispatch directly on an XHR response, rather than use another ActionCreator". Absolutely — and that makes perfect sense when your implementation gives your util modules (like remote data APIs) a handle to the dispatcher. With lux, we opted for the gateway to the dispatcher to be via message contract, and removed the need for the dispatcher to be a dependency of any module.

So if <strong>every input is an action</strong>, this means we might have actions in our system that none of our stores care about. Other actions might be of interest to both a store and our remote data API. The value of how this complements and forces you into the pit of unidirectional data flow success can be illustrated in this image:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a00b7690-54bf-4e97-9449-77cd1d7d837c/01-luxdataflow1-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fecc09c2-090b-4462-8a98-d71237c046db/01-luxdataflow1-opt-small.png" alt="Unidirectional data flow in lux.js" /></a><figcaption>Unidirectional data flow in lux.js. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a00b7690-54bf-4e97-9449-77cd1d7d837c/01-luxdataflow1-opt.png">View large version</a>)</figcaption></figure>

In the above scenario, a user clicked a button on the page that resulted in a server request. When the server responds, the response is published as a new action. While we <em>know</em> that the two actions are related, modeling things this way reinforces the avoidance of cascading updates, <em>and</em> it means your app's behavior will be capable of handling data being <em>pushed</em> to it, not just <em>pulled</em> through HTTP requests.

What if we wanted to update the UI to reflect that data is loading? It's as easy as having the appropriate store handle the same action:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d52aa95-872b-4989-a7e1-a05f8ec63d77/02-luxdataflow2-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9a2ecbb1-2e35-4a3e-bb20-17d1172b29bc/02-luxdataflow2-opt-small.png" alt="Unidirectional data flow in lux.js." /></a><figcaption>Unidirectional data flow in lux.js: Update the UI. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d52aa95-872b-4989-a7e1-a05f8ec63d77/02-luxdataflow2-opt.png">View large version</a>)</figcaption></figure>

Another benefit of treating every input as an action: it makes it easy to see what behaviors are possible in your app. For example, here's the output of calling <code>lux.utils.printActions()</code>:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bde8d61e-8d4b-43cd-964f-3e4bd544600b/03-luxprintactions-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/eacb480f-69ae-420e-96bd-86571d52c789/03-luxprintactions-opt-small.png" alt="Unidirectional data flow in lux.js" /></a><figcaption>Unidirectional data flow in lux.js: Output of calling <code>lux.utils.printActions()</code>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bde8d61e-8d4b-43cd-964f-3e4bd544600b/03-luxprintactions-opt.png">View large version</a>)</figcaption></figure>

Lux also provides a utility method to view what stores would participate in handling an action, and in what order: <code>lux.utils.printStoreDepTree(actionName)</code>:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24eb459c-9995-45e3-884f-d2ded4ed5a6c/04-luxprintstoredeptree-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bcbe51d7-bdb9-46e9-ac3f-9007a32a0d93/04-luxprintstoredeptree-opt-small.png" alt="Unidirectional data flow in lux.js" /></a><figcaption>Unidirectional data flow in lux.js: <code>lux.utils.printStoreDepTree(actionName)</code>. (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/24eb459c-9995-45e3-884f-d2ded4ed5a6c/04-luxprintstoredeptree-opt.png">View large version</a>)</figcaption></figure>

### Lux + Ajax Examples

We've resisted any temptation to be too prescriptive when it comes to how you should interact with remote endpoints in lux. The main guideline we follow is to wrap your remote access in a developer-friendly API in the client (rather than scatter Ajax requests throughout the codebase!), and make that API wrapper an ActionListener and ActionCreator. For example, let's look at a couple of conceptual approaches you can take:

#### Plain Ajax

The example below only shows the relevant portions of each piece. Our component publishes an action message for the <code>cartCheckout</code> action, and our <code>WebApi</code> wrapper listens for it. Notice that our response handler for the Ajax call actually publishes a new action message:

<pre><code class="language-javascript">// in a CartContainer.jsx module
var CartContainer = React.createClass({
  // other methods, properties, etc.

  onCheckoutClicked: function() {
    var products = this.state.products;
    if (!products.length) {
      return;
    }
    this.cartCheckout(products);
  }
});

// In a WebApi.js module
var webApi = lux.actionCreatorListener({
  handlers: {
    cartCheckout: function(products) {
      $.ajax({
        url: "cart/checkout",
        method: "POST",
        data: products
      }).then(
        function(data) {
          this.publishAction("successCheckout", data);
        }.bind(this),
        cartErrorHandler
      );
    }
  }
});
</code></pre>

#### How We Use halon

One of the many things we've grown to love about hypermedia resources is the <strong>built-in discoverability</strong>. Instead of having to hard-code specific links (as in the example above), halon allows us to <em>follow</em> links returned with resources, so the only URL we have to know is where we go to get the OPTIONS. In this approach, our WebApi module initializes halon (which results in an OPTIONS request to the server), and the resulting instance will contain the top-level resources we can act on, with their "actions" exposed as methods. In this case we have a <code>cart</code> resource that exposes a <code>checkout</code> action:

<pre><code class="language-javascript">// in a CartContainer.jsx module
var CartContainer = React.createClass({
  // other methods, properties, etc.

  onCheckoutClicked: function() {
    var products = this.state.products;
    if (!products.length) {
      return;
    }
    this.cartCheckout(products);
  }
});

// In a WebApi.js module
var hal = halon( {
  root: "https://some-server.com/api",
  adapter: halon.jQueryAdapter( $ ),
  version: 1
} );
var webApi = lux.actionCreatorListener({
  handlers: {
    cartCheckout: function(products) {
      hal.cart.checkout(products)
        .then(
          function(data) {
            this.publishAction("successCheckout", data);
          }.bind(this),
          cartErrorHandler
        );
    }
  }
});
</code></pre>

## Stores And Synchronicity

### Actions, Stores And Remote Data I/O

I believe a classic pitfall to those rolling their own Flux implementations is <strong>putting remote data</strong> I/O in stores. In the first version of lux, I not only fell into this pit, I pulled out a golden shovel and dug even deeper. Our stores had the ability to make HTTP calls — and as a result, the need for action dispatch cycles to be asynchronous was unavoidable. This introduced a ripple of bad side effects:

*   Retrieving data from a store was an asynchronous operation, so it wasn't possible to synchronously use a store's state in a controller ciew's `getInitialState` method.
*   We found that requiring asynchronous reads of store state discouraged the use of read-only helper methods on stores.
*   Putting I/O in stores led to actions being initiated by stores (e.g. on XHR responses or WebSocket events). This quickly undermined the gains from unidirectional data flow. Flux stores publishing their own actions could lead to cascading updates — the very thing we wanted to avoid!

I think the temptation to fall into this pit has to do with the trend of client-side frameworks to date. Client-side models are often treated as write-through caches for server-side data. Complex server/client synchronization tools have sprung up, effectively encouraging a sort of two-way binding across the server/client divide. Yoda said it best: you must unlearn what you have learned.

About the time I realized I'd be better off making lux stores synchronous, I read Reto Schläpfer's post “<a href="https://www.code-experience.com/async-requests-with-react-js-and-flux-revisited/">Async requests with React.js and Flux, revisited</a>”. He had experienced the same pain, and the same realization. Making lux stores synchronous, from the moment the dispatcher begins handling an action to the moment stores emit change events, made our app more deterministic and enabled our controller views to synchronously read store state as they initialized. We finally felt like we'd found the droids we were looking for.

Let's take a look at one of the lux stores in the flux-comparison example:

<pre><code class="language-javascript">var CartStore = new lux.Store( {
  namespace: "cart",

  state: { products: { } },

  handlers: {
    addToCart: {
      waitFor: [ 'products' ],
      handler: function( product ) {
        var newState = this.getState();
        newState.products[ product.id ] = (
          newState.products[ product.id ] ||
          assign( products.getProduct( product.id ), { quantity: 0 } )
        );
        newState.products[ product.id ].quantity += 1;
        this.setState( newState );
      }
    },
    cartCheckout: function() {
      this.replaceState( { products: {} } );
    },
    successCheckout: function( products ) {
      // this can be used to redirect to success page, etc.
      console.log( 'YOU BOUGHT:' );
      if ( typeof console.table === "function" ) {
        console.table( products );
      } else {
        console.log( JSON.stringify( products, null, 2 ) );
      }
    }
  },

  getProduct: function( id ) {
    return this.getState().products[ id ];
  },

  getAddedProducts: function() {
    var state = this.getState();
    return Object.keys( state.products ).map( function( id ) {
      return state.products[ id ];
    } );
  },

  getTotal: function() {
    var total = 0;
    var products = this.getState().products;
    for (var id in products) {
      var product = products[ id ];
      total += product.price * product.quantity;
    }
    return total.toFixed( 2 );
  }
} );
</code></pre>

A lux store contains (at least) a <code>handlers</code> property and a <code>namespace</code>. The names of the keys on the <code>handlers</code> property match the action type that they handle. In keeping with Flux principles, it's possible for lux stores to wait on other stores before executing their handler. The stores you need to wait on can be specified on a per-action basis. The <code>addToCart</code> handler above is a good example. In the <code>waitFor</code> array, you specify the namespaces of any other store you need to wait on — this handler waits on the "products" store. The dispatcher determines the order in which stores need to execute their handlers at runtime, so there's no need to worry about managing the order yourself in your store logic. (Note that if you don't need to wait on any other stores, the handler value can be just the handler function itself rather than the object literal representation on <code>addToCart</code> above.)

You can also set initial state on the store, as we're doing above, and provide top-level methods that are used for reading data (the lux store prototype provides the <code>getState()</code> method). Since store handlers execute synchronously, you can safely read a store's state from any component's <code>getInitialState</code> method, and you can be assured that no other action will interrupt or mutate store state while another action is being handled.

lux stores also provide <code>setState</code> and <code>replaceState</code> methods, but if you attempt to invoke them directly, an exception will be thrown. Those methods can only be invoked during a dispatch cycle; we put this rather heavy-handed opinion in place to reinforce the guideline that only stores mutate their own state, and that's done in a handler.</p>

## Plays Well With Others

Another key lesson for our team: it needs to be simple for lux and non-React/non-lux (external) instances to play well together. To that end, lux provides mixins that can be used by external instances.</p>

### Store Mixin

The <code>store</code> mixin enables you to listen for store change events. For example, this snippet shows an instance that's wired to listen to our ProductStore and CartStore:

<pre><code class="language-javascript">var storeLogger = lux.mixin({
  stores: {
    listenTo: [ "products", "cart" ],
    onChange: function() {
      console.log( "STORE LOGGER: Received state change event" );
    },
  }
}, lux.mixin.store);
</code></pre>

### ActionCreator Mixin

The actionCreator mixin gives the instance a <code>publishAction( actionName, arg1, arg2…)</code> method. This method handles packaging the metadata about the action into a message payload and then publishes it (if you've created a custom ActionCreator that does more than just publish the action message, it will invoke that behavior):

<pre><code class="language-javascript">// calling lux.actionCreator is a convenience wrapper around
// lux.mixin( target, lux.mixin.actionCreator );
var creator = lux.actionCreator( {
  doAThing: function() {
    this.publishAction( "doJazzHands", "hey, I can lux, too!", true, "story" );
  }
} );
</code></pre>

### ActionListener Mixin

The actionListener mixin wires the instance into postal, so that it listens for any lux action messages. When a message arrives, it checks the <code>handlers</code> property for a matching handler and invokes it:

<pre><code class="language-javascript">var listener = lux.actionListener({
  handlers: {
    doJazzHands: function(msg, someBool, lastArg) {
      console.log(msg, someBool, lastArg); // -&gt; hey, I can lux, too! true story
    }
  }
});
</code></pre>

### Why Not Both?

It's not uncommon — especially if remote data API wrappers are involved — to need both actionCreator and actionListener mixins. lux provides a convenience method for this, unsurprisingly named <code>actionCreatorListener</code>. In the flux-comparison example, the wrapper around the mock remote data API uses this:

<pre><code class="language-javascript">// WebAPIUtils.js
var shop = require( '../../../common/api/shop' );
var lux = require( 'lux.js' );

module.exports = lux.actionCreatorListener( {
  handlers: {
    cartCheckout: function( products ) {
      shop.buyProducts( products, function() {
        this.publishAction( "successCheckout", products );
      }.bind( this ) );
    },
    getAllProducts: function() {
      shop.getProducts( function( products ) {
        this.publishAction( "receiveProducts", products );
      }.bind( this ) );
    },
  }
} );
</code></pre>

The above module listens for the <code>cartCheckout</code> and <code>getAllProducts</code> actions. As it handles them, it uses the <code>publishAction</code> method (simulating how a server response would initiate a new Action).

So far, the mixins have covered every need we've had to make non-lux/non-React instances play well with lux. If those weren't enough, though, the underlying message contracts for actions and store update notifications are very simple, and could serve as an alternative. In fact, we plan to use those in some future Chrome dev tools extensions for lux.</p>

## Wrapping Up

As I've looked through other Flux implementations, I've been encouraged to see that these principles are frequently present in them as well. The number of options available can feel overwhelming, but overall I find it an encouraging development. Solid and successful patterns like <strong>Flux will, by their very nature, encourage multiple implementations</strong>. If our experience is any indication, keeping these principles in mind can help guide you as you select, or write, the Flux implementation you need.

{{< signature "rb, ml, og" >}}


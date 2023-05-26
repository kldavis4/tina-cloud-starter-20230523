---
title: React To The Future With Isomorphic Apps
slug: react-to-the-future-with-isomorphic-apps
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/80c34ea8-1121-4cef-9754-60d244b9749a/code-functions-illu-opt.jpg
date: 2015-04-21T21:06:18.000Z
author: jonathancreamer
description: >-
  Things often come full circle in software engineering. The web in particular
  started with servers delivering content down to the client. Recently, with the
  creation of modern web frameworks such as AngularJS and Ember, we’ve seen a
  push to render on the client and **only use a server for an API**. We’re now
  seeing a possible return or, rather, more of a combination of both
  architectures happening.

  React has quickly risen to immense popularity in the JavaScript community.
  There are a number of reasons for its success. One is that Facebook created it
  and uses it. This means that many developers at Facebook work with it, fixing
  bugs, suggesting features and so on.
categories:
  - Coding
  - JavaScript
  - Apps
  - Node.js
  - API
  - React
---
Things often come full circle in software engineering. The web in particular started with servers delivering content down to the client. Recently, with the creation of modern web frameworks such as AngularJS and Ember, we’ve seen a push to render on the client and <strong>only use a server for an API</strong>. We’re now seeing a possible return or, rather, more of a combination of both architectures happening.</p>

## What Is React?

React is a JavaScript library for building user interfaces.

According to the <a href="https://facebook.github.io/react/">official website</a>. It is a way to create reusable front-end components. Plain and simple, that is the goal of React.</p>

### What Makes It Different?

React has quickly risen to immense popularity in the JavaScript community. There are a number of reasons for its success. One is that Facebook created it and uses it. This means that many developers at Facebook work with it, fixing bugs, suggesting features and so on.

{{% feature-panel %}}

<figure><img title="React To The Future With Isomorphic Apps" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2259d8f2-d4b6-420e-8a89-b793f4b0cd40/code-react-opt.jpg" alt="React To The Future With Isomorphic Apps" /></figure>

Another reason for its quick popularity is that it’s different. It’s unlike <a href="https://angularjs.org/">AngularJS</a>, <a href="https://backbonejs.org">Backbone.js</a>, <a href="https://emberjs.com/">Ember</a>, <a href="https://knockoutjs.com">Knockout</a> and pretty much any of the other popular MV* JavaScript frameworks that have come out during the JavaScript revolution in the last few years. Most of these other frameworks operate on the idea of two-way binding to the DOM and updating it based on events. They also all <strong>require the DOM to be present</strong>; so, when you’re working with one of these frameworks and you want any of your markup to be rendered on the server, you have to use something like PhantomJS.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [The Beauty Of React Native](https://www.smashingmagazine.com/2016/04/the-beauty-of-react-native-building-your-first-ios-app-with-javascript-part-1/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [Styled-Components: Enforcing Best Practices In Component-Based Systems](https://www.smashingmagazine.com/2017/01/styled-components-enforcing-best-practices-component-based-systems/)

## Virtual DOM

React is often described as the “V” in an MVC application. But it does the V quite differently than other MV* frameworks. It’s different from things like Handlebars, Underscore templates and AngularJS templates. React operates on the concept of a “virtual DOM.” It maintains this virtual DOM in memory, and any time a change is made to the DOM, React does a quick diff of the changes, batches them all into one update and hits the actual DOM all at once.

This has huge ramifications. First and foremost, performance-wise, you’re not constantly doing DOM updates, as with many of the other JavaScript frameworks. <strong>The DOM is a huge bottleneck with front-end performance.</strong> The second ramification is that React can render on the server just as easily as it can on the client.

React exposes a method called <code>React.renderToString()</code>. This method enables you to pass in a component, which in turn renders it and any child components it uses, and simply returns a string. You can then take that string of HTML and simply send it down to the client.</p>

### Example

These components are built with a syntax called JSX. At first, JSX looks like a weird HTML-JavaScript hybrid:

<pre><code class="language-javascript">
var HelloWorld = React.createClass({
  displayName: "HelloWorld",
  render() {
    return (
      &lt;h1&gt;Hello {this.props.message}&lt;/h1&gt;
    );
  }
});

React.render(&lt;HelloWorld message="world" /&gt;, document.body);
</code></pre>

What you do with this <code>.jsx</code> format is pass it through (or “transpile”) <code>webpack</code>, <code>grunt</code>, <code>gulp</code>, or your “renderer” of choice and then spit out JavaScript that looks like this:

<pre><code class="language-javascript">
var HelloWorld = React.createClass({
  displayName: "HelloWorld",
  render: function() {
    return (
      React.createElement("h1", null, "Hello ", this.props.message)
    );
  }
});

React.render(React.createElement(HelloWorld, {message: "world"}), document.body);
</code></pre>

That’s what our <code>HelloWorld.jsx</code> component transpiles to — nothing more than simple JavaScript. Some would consider this a violation of the separation of concerns by mixing JavaScript with HTML. At first, this seems like exactly what we’re doing. However, after working with React for a while, you realize that the close proximity of your component’s markup to the JavaScript enables you to develop more quickly and to maintain it longer because you’re not jumping back and forth between HTML and JavaScript files. <strong>All the code for a given component lives in one place.</strong>

<code>React.render</code> attaches your <code>&lt;HelloWorld&gt;</code> component to the <code>body</code>. Naturally, that could be any element there. This causes the component’s <code>render</code> method to fire, and the result is added to the DOM inside the <code>&lt;body&gt;</code> tag.

With a React component, whatever you pass in as attributes — say, <code>&lt;HelloWorld message="world" /&gt;</code> — you have access to in the component’s <code>this.props</code>. So, in the <code>&lt;HelloWorld&gt;</code> component, <code>this.props.message</code> is <code>world</code>. Also, look a bit closer at the JSX part of the code:

<pre><code class="language-javascript">
return (
  &lt;h1&gt;Hello {this.props.message}&lt;/h1&gt;
);
</code></pre>

You’ll notice first that you have to wrap the HTML in parentheses. Secondly, <code>this.props.message</code> is wrapped in braces. The braces give you access to the component via <code>this</code>.

Each component also has access to its “state.” With React, each component manages its state with a few simple API methods, <code>getState</code> and <code>setState</code>, as well as <code>getInitialState</code> for when the component first loads. Whenever the state changes, the <code>render</code> method simply re-renders the component. For example:

<pre><code class="language-javascript">
var Search = React.createClass({
  getInitialState() {
    return {
      search: ""
    };
  },
  render() {
    return (
      &lt;div className="search-component"&gt;
        &lt;input type="text" onChange={this.changeSearch} /&gt;
        &lt;span&gt;You are searching for: {this.state.search}&lt;/span&gt;
      &lt;/div&gt;
    );
  },
  changeSearch(event) {
    var text = event.target.value;

    this.setState({
      search: text
    });
  }
});

React.render(&lt;Search /&gt;, document.body);
</code></pre>

In this example, the <code>getInitialState</code> function simply returns an object literal containing the initial state of the component.

The <code>render</code> function returns JSX for our elements — so, an <code>input</code> and a <code>span</code>, both wrapped in a <code>div</code>. Keep in mind that only one element can ever be returned in JSX as a parent. In other words, you can’t return <code>&lt;div&gt;&lt;/div&gt;&lt;div&gt;&lt;/div&gt;</code>; you can only return one element with multiple children.

Notice the <code>onChange={this.changeSearch}</code>. This tells the component to fire the <code>changeSearch</code> function when the change event fires on the input.

The <code>changeSearch</code> function receives the <code>event</code> fired from the DOM event and can grab the current text of the input. Then, we call <code>setState</code> and pass in the text. This causes <code>render</code> to fire again, and the <code>{this.state.search}</code> will reflect the new change.

Many other APIs in React are available to work with, but at a high level, what we did above is as easy as it gets for creating a simple React component.

## Isomorphic JavaScript

With React, we can build “isomorphic” apps.
<blockquote>i·so·mor·phic: “corresponding or similar in form and relations”</blockquote>

This has already become a buzzword in 2015. Basically, it just means that we get to use the same code on the client and on the server.

This approach has many benefits.</p>

### Eliminate the FOUC

With AngularJS, Ember (for now) and SPA-type architecture, when a user first hits the page, all of the assets have to download. With SPA applications, this can take a second, and most users these days expect a loading time of less than two seconds. While content is loading, the page is unrendered. This is called the “flash of unstyled content” (FOUC). One benefit of an isomorphic approach to building applications is that you get the speed benefits of rendering on the server, and you can still render components after the page loads on the client.

The job of an isomorphic app is not to replace the traditional server API, but merely to help eliminate FOUC and to give users the better, faster experience that they are growing accustomed to.</p>

### Shared Code

One big benefit is being able to use the same code on the client and on the server. Simply create your components, and they will work in both places. In most systems, such as <a href="https://rubyonrails.org/">Rails</a>, <a href="https://asp.net/mvc">ASP.NET MVC</a>, you will typically have <code>erb</code> or <code>cshtml</code> views for rendering on the server. You then have to have client-side templates, such as Handlebars or Hogan.js, which often duplicate logic. With React, the same components work in both places.</p>

### Progressive Enhancement

Server rendering allows you to send down the barebones HTML that a client needs to display a website. You can then enhance the experience or render more components in the client.

Delivering a nice experience to a user on a flip phone in Africa, as well as an enhanced experience to a user on a 15-inch MacBook Pro with Retina Display, hooked up to the new 4K monitor, is normally a rather tedious task.

React goes above and beyond just sharing components. When you render React components on the server and ship the HTML down to the client, React on the client side notices that the HTML already exists. It simply <strong>attaches event handlers to the existing elements</strong>, and you’re ready to go.

This means that you can ship down only the HTML needed to render the page; then, any additional things can be pulled in and rendered on the client as needed. You get the benefit of fast page loading by server rendering, and you can reuse the components.</p>

## Creating An Isomorphic Express App

<a href="https://expressjs.com/">Express</a> is one of the most popular Node.js web servers. Getting up and running with rendering React with Express is very easy.

Adding React rendering to an Express app takes just a few steps. First, add <code>node-jsx</code> and <code>react</code> to your project with this:

<pre><code class="language-bash">npm install node-jsx --save
npm install react --save
</code></pre>

Let’s create a basic <code>app.jsx</code> file in the <code>public/javascripts/components</code> directory, which requires our <code>Search</code> component from earlier:

<pre><code class="language-javascript">
var React = require("react"),
  Search = require("./search");

var App = React.createClass({
  render() {
    return (
      &lt;Search /&gt;
    );
  }
});

module.exports = App;
</code></pre>

Here, we are requiring <code>react</code> and our <code>Search.jsx</code> component. In the <code>App</code> render method, we can simply use the component with <code>&lt;Search /&gt;</code>.

Then, add the following to one of your routers where you’re planning on rendering with React:

<pre><code class="language-javascript">
require("node-jsx").install({
  harmony: true,
  extension: ".jsx"
});
</code></pre>

All this does is allow us to actually use <code>require</code> to grab <code>.jsx</code> files. Otherwise, Node.js wouldn’t know how to parse them. The <code>harmony</code> option allows for ECMAScript 6-style components.

Next, require in your component and pass it to <code>React.createFactory</code>, which will return a function that you can call to invoke the component:

<pre><code class="language-javascript">
var React = require("react"),
  App = React.createFactory(require("../public/javascripts/components/app")),
  express = require("express"),
  router = express.Router();
</code></pre>

Then, in a route, simply call <code>React.renderToString</code> and pass it your component:

<pre><code class="language-javascript">
router.get("/", function(req, res) {
  var markup = React.renderToString(
    App()
  );

  res.render("index", {
    markup: markup
  });
});
</code></pre>

Finally, in your view, simply output the markup:

<pre><code class="html">
&lt;body&gt;
  &lt;div id="content"&gt;
    {{{markup}}}
  &lt;/div&gt;
&lt;/body&gt;
</code></pre>

That’s it for the server code. Let’s look at what’s necessary on the client side.</p>

## Webpack

<a href="https://webpack.github.io/">Webpack</a> is a JavaScript bundler. It bundles all of your static assets, including JavaScript, images, CSS and more, into a single file. It also enables you to process the files through different types of loaders. You could write your JavaScript with CommonJS or AMD modules syntax.

For React <code>.jsx</code> files, you’ll just need to configure your <code>webpack.config</code> file a bit in order to compile all of your <code>jsx</code> components.

Getting started with Webpack is easy:

<pre><code class="shell">
npm install webpack -g # Install webpack globally
npm install jsx-loader --save # Install the jsx loader for webpack
</code></pre>

Next, create a <code>webpack.config.js</code> file.

<pre><code class="language-javascript">
var path = require("path");

module.exports = [{
  context: path.join(__dirname, "public", "javascripts"),
  entry: "app",
  output: {
    path: path.join(__dirname, "public", "javascripts"),
    filename: "bundle.js"
  },
  module: {
    loaders: [
      { test: /\.jsx$/, loader: "jsx-loader?harmony"}
    ]
  },
  resolve: {
    // You can now require('file') instead of require('file.coffee')
    extensions: ["", ".js", ".jsx"],
    root: [path.join(__dirname, "public", "javascripts")],
    modulesDirectories: ["node_modules"]
  }
}];
</code></pre>

Let’s break this down:

*   `context` This is the root of your JavaScript files.
*   `entry` This is the main file that will load your other files using CommonJS’ `require` syntax by default.
*   `output` This tells Webpack to output the code in a bundle, with a path of `public/javascripts/bundle.js`.

The <code>module</code> object is where you set up “loaders.” A loader simply enables you to test for a file extension and then pass that file through a loader. Many loaders exist for things like CSS, Sass, HTML, CoffeeScript and JSX. Here, we just have the one, <code>jsx-loader?harmony</code>. You can append options as a “query string” to the loader’s name. Here, <code>?harmony</code> enables us to use ECMAScript 6 syntax in our modules. The <code>test</code> tells Webpack to pass any file with <code>.jsx</code> at the end to <code>jsx-loader</code>.

In <code>resolve</code> we see a few other options. First, <code>extensions</code> tells Webpack to omit the extensions of certain file types when we <code>require</code> files. This allows us just to do <code>require("./file")</code>, rather than <code>require("./file.js")</code>. We’re also going to set a <code>root</code>, which is simply the root of where our files will be required from. Finally, we’ll allow Webpack to pull modules from the <code>node_modules</code> directory with the <code>modulesDirectories</code> option. This enables us to install something like Handlebars with <code>npm install handlebars</code> and simply <code>require("handlebars")</code>, as you would in a Node.js app.</p>

## Client-Side Code

In <code>public/javascripts/app.js</code>, we’ll require in the same <code>App</code> component that we required in Express:

<pre><code class="language-javascript">
var React = require("react"),
  App = React.createFactory(require("components/app"));

if (typeof window !== "undefined") {
  window.onload = function() {
    React.render(App(), document.getElementById("content"));
  };
}
</code></pre>

We’re going to check that we’re in the browser with the <code>typeof window !== "undefined"</code>. Then, we’ll attach to the <code>onload</code> event of the window, and we’ll call <code>React.render</code> and pass in our <code>App()</code>. The second argument we need here is a DOM element to mount to. This needs to be the same element in which we rendered the React markup on the server — in this case, the <code>#content</code> element.

The <code>Search</code> component in the example above was rendered on the server and shipped down to the client. The client-side React sees the rendered markup and attaches only the event handlers! This means we’ll get to see an initial page while the JavaScript loads.

All of the code above is <a href="https://github.com/jcreamer898/expressiso">available on GitHub</a>.</p>

## Conclusion

Web architecture definitely goes through cycles. We started out rendering everything on the server and shipping it down to the client. Then, JavaScript came along, and we started using it for simple page interactions. At some point, JavaScript grew up and we realized it could be used to build large applications that render all on the client and that use the server to retrieve data through an API.

In 2015, we’re starting to realize that we have these powerful servers, with tons of memory and CPU, and that they do a darn good job of rendering stuff for us. T<strong>his isomorphic approach to building applications might just give us the best of both worlds</strong>: using JavaScript in both places, and delivering to the user a good experience by sending down something they can see quickly and then building on that with client-side JavaScript.

React is one of the first of what are sure to be many frameworks that enable this type of behavior. Ember’s developers are already working on isomorphic-style applications as well. Seeing how this all works out is definitely going to be fun!

### Resources

*   [React](https://facebook.github.io/react/)
*   [React Lessons](https://egghead.io/technologies/react), Egghead.io
*   [Express](https://expressjs.com/)
*   “[Isomorphic Examples](https://react.rocks/tag/Isomorphic),” React.rocks
*   [Webpack](https://webpack.github.io), GitHub
*   [JSX Loader for Webpack](https://github.com/petehunt/jsx-loader), Pete Hunt, GitHub

{{< signature "rb, al, il" >}}


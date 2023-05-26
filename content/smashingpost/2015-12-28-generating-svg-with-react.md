---
title: Generating SVG With React
slug: generating-svg-with-react
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b8fd0663-dd8e-4974-83d0-2446de261c35/01-staticgen-stats-opt-preview.png
date: 2015-12-28T19:50:13.000Z
author: ilya
description: >-
  React is one of today’s most popular ways to create a component-based UI. It
  helps to organize an application into small, human-digestible chunks. With its
  “re-render the whole world” approach, you can **avoid any complex internal
  interactions between small components**, while your application continues to
  be blazingly fast due to the DOM-diffing that React does under the hood (i.e.
  updating only the parts of the DOM that need to be updated).

  But can we apply the same techniques to web graphics — SVG in particular? Yes!
  I don’t know about you, but for me SVG code becomes messy pretty fast. Trying
  to grasp what’s wrong with a graph or visualization just by looking at SVG
  generator templates (or the SVG source itself) is often overwhelming, and
  attempts to **maintain internal structure or separation of concerns** are
  often complex and tedious.
categories:
  - Coding
  - JavaScript
  - SVG
  - React
---
<a href="https://facebook.github.io/react/">React</a> is one of today’s most popular ways to create a component-based UI. It helps to organize an application into small, human-digestible chunks. With its “re-render the whole world” approach, you can <strong>avoid any complex internal interactions between small components</strong>, while your application continues to be blazingly fast due to the DOM-diffing that React does under the hood (i.e. updating only the parts of the DOM that need to be updated). But can we apply the same techniques to web graphics — SVG in particular? Yes!

I don’t know about you, but for me SVG code becomes messy pretty fast. Trying to grasp what’s wrong with a graph or visualization just by looking at SVG generator templates (or the SVG source itself) is often overwhelming, and attempts to <strong>maintain internal structure or separation of concerns</strong> are often complex and tedious.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)
*   [Rethinking Responsive SVG](https://www.smashingmagazine.com/2014/03/rethinking-responsive-svg/)
*   [How To Scale React Applications](https://www.smashingmagazine.com/2016/09/how-to-scale-react-applications/)
*   [A Glimpse Into The Future With React Native For Web](https://www.smashingmagazine.com/2016/08/a-glimpse-into-the-future-with-react-native-for-web/)

Thanks to Facebook, we have React to do the work for us.

{{% feature-panel %}}

First, React works with the DOM (and the DOM is not only HTML). So, you can work with SVG exactly in the way you normally do with HTML. For example, here is a circle:

<pre><code class="language-javascript">import React from 'react';

export default class App extends React.Component {
  render() {
    return (
      &lt;svg&gt;
        &lt;circle cx={50} cy={50} r={10} fill="red" /&gt;
      &lt;/svg&gt;
    )
  }
}</code></pre>

<figure><a href="/wp-content/uploads/2015/10/29472-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a1ea10f2-fa39-4657-b8a4-844d2cea9507/29472-opt-preview.png" alt="React works with the DOM so you can work with SVG exactly in the way you normally do with HTML" /></a><figcaption>React works with the DOM so you can work with SVG exactly in the way you normally do with HTML. (<a href="/wp-content/uploads/2015/10/29472-opt.png">View large version</a>)</figcaption></figure>

As I said, from React’s perspective, there is <strong>no difference between working with HTML or working with SVG</strong> (or, as you may heard lately, mobile views or canvas).

But let’s try to create something a little more complex, so that we can see how React helps to <strong>structure SVG in a human-understandable way</strong>.

Imagine we need to build a dashboard to visualize the most complex data set ever:

<pre><code class="language-none">[
  [1, 3],
  [2, 5],
  [3, 2],
  [4, 16],
  [18, 5]
]</code></pre>

This is just an array of x and y coordinate pairs, nothing more.

I will use <a href="https://github.com/gaearon/react-hot-boilerplate">React Hot Boilerplate</a> as a starting point to save time configuring our development essentials, including the following:

*   [webpack](https://webpack.github.io/) This very powerful module bundler will process and manage all dependencies for us.
*   [babel](https://babeljs.io/) This code transpiler allows us to use ECMAScript 6 (ES6) in browsers that don’t yet support it.
*   [react-hot-loader](https://github.com/gaearon/react-hot-loader) This great tool will update our React components in the browser without reloading the whole page.

We will start by changing <code>script/index.js</code> to bootstrap our dashboard:

<pre><code class="language-javascript">
import React from 'react';
import ReactDOM from 'react-dom';
import App from './app';
import data from './data';

ReactDOM.render(&lt;App data={data} /&gt;, document.getElementById('root'));</code></pre>

Here, <code>script/data.js</code> is just our data array that was mentioned previously:

<pre><code class="language-javascript">export default [
   [1, 3],
   [2, 5],
   [3, 2],
   [4, 16],
   [18, 5]
 ];
</code></pre>

Now, we will prepare our <code>script/app.js</code> to render our future graph:

<pre><code class="language-javascript">import React from 'react';
import Graph from './components/graph';

export default class App extends React.Component {
  render() {
    return (
      &lt;Graph data={this.props.data} /&gt;
    )
  }
}</code></pre>

This is the most interesting part: the opportunity to stop and think about what our graph consists of. This is one of the best processes when developing with React: We can think about high-level components first and split them into more granular ones later.

For example, <code>scripts/components/graph.js</code>:

<pre><code class="language-javascript">import React from 'react';
import Axis from './axis';
import GraphBody from './graph_body';

export default class Graph extends React.Component {
  render() {
    return (
      &lt;svg&gt;
        &lt;Axis
          length={width}
          horizontal={true}
        /&gt;
        &lt;Axis
          length={height}
          horizontal={false}
        /&gt;
        &lt;GraphBody
          data={this.props.data}
        /&gt;
      &lt;/svg&gt;
    )
  }
}</code></pre>

Two axes and a graph body — looks logical to me. Of course, the code will not work. This is just an attempt to shape an initial API of our graph: We haven’t implemented child components yet, and we have some undefined variables such as <code>width</code> and <code>height</code>. Let’s finish this step by step.

We need to set some dimensions for our graph. We could hardcode them, but better to use <code>defaultProps</code>:

<pre><code class="language-javascript">export default class Graph extends React.Component {
  static defaultProps = { width: 800, height: 600 };</code></pre>

Now, if we pass no <code>width</code> or <code>height</code> to the <code>Graph</code> component as <code>props</code>, then default values will be used.

We could transfer these values to the <code>svg</code> itself:

<pre><code class="language-markup">&lt;svg width={this.props.width} height={this.props.height}&gt;</code></pre>

And then we could extend the declarations of the axes and graph body by giving them some initial positions:

<pre><code class="language-javascript">import React from 'react';
import Axis from './axis';
import GraphBody from './graph_body';

export default class Graph extends React.Component {
  static defaultProps = { width: 800, height: 600 };

  render() {
    return (
      &lt;svg width={this.props.width} height={this.props.height}&gt;
        &lt;Axis
          x={20}
          y={this.props.height - 100}
          length={this.props.width}
          horizontal={true}
        /&gt;
        &lt;Axis
          x={20}
          y={0}
          length={this.props.height - 100}
          horizontal={false}
        /&gt;
        &lt;GraphBody
          x={20}
          y={this.props.height - 100}
          data={this.props.data}
        /&gt;
      &lt;/svg&gt;
    )
  }
}</code></pre>

Just look: We can read that like plain English. Anyone should be able to understand what is happening here. Now, when our parent component looks ready, it’s time to switch focus to the children.

Axes should just return lines, nothing complex there. <a href="https://developer.mozilla.org/en/docs/Web/SVG/Element/line">According to the SVG specification</a>, to create a line, we need to pass four coordinates: <code>x1, y1, x2, y2</code>. And keep in mind that axes may be vertical or horizontal and should respect the initial position passed through <code>props</code>:

Here is <code>scripts/components/axis.js</code>:

<pre><code class="language-javascript">import React from 'react';

export default class Axis extends React.Component {
  prepareCords() {
    let coords = {
      x1: this.props.x,
      y1: this.props.y
    }

    if(this.props.horizontal) {
      coords.x2 = coords.x1 + this.props.length;
      coords.y2 = coords.y1;
    } else {
      coords.x2 = coords.x1;
      coords.y2 = coords.y1 + this.props.length;
    }

    return coords;
  }

  render() {
    let coords = this.prepareCords();
    return (
      &lt;line {...coords} stroke="green" strokeWidth={2} /&gt;
    )
  }
}</code></pre>

Here, <code>{...coords}</code> is just a fancy new ES6 way to write <code>x1={coords.x1} x2={coords.x2} y1={coords.y1} y2={coords.y2}.</code> Thanks to Babel, we can use it without waiting for browsers to implement it.

Just to test that the axis works, let’s stub a graph body implementation:

<pre><code class="language-javascript">import React from 'react';

export default class GraphBody extends React.Component {
  render() {
    return null;
  }
}</code></pre>

Returning <code>null</code> in this case will force React to render a <code>noscript</code> tag. We can achieve the same “empty” result by using <code>return &lt;g /&gt;</code>, which will return an empty SVG group.

Groups in SVG are something like <code>div</code> elements in HTML, very useful when your component should return more than one node. By default, this will not work in JSX (only the last node will be returned), so we’ll wrap everything in a <code>&lt;g&gt;</code> element to avoid this.

At this time in our browser, we should see two axes:

<figure><a href="/wp-content/uploads/2015/10/29473-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e02f59ea-a7f1-4bdb-8cb6-8b237c077b40/29473-opt-preview.png" alt="Groups in SVG are something like div elements in HTML" /></a><figcaption>Groups in SVG are something like div elements in HTML. (<a href="/wp-content/uploads/2015/10/29473-opt.png">View large version</a>)</figcaption></figure>

The next step is to remove the stub and create a fully functional graph body. To draw a graph line, we will use a <a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/path">path</a>. This requires us to pass a specially crafted string as a <code>d</code> parameter. Crafting this string is easy; it consists of two parts: an initial <code>Moveto</code> command and a bunch of <code>Lineto</code> commands to draw the graph itself:

<code>Moveto</code> will be our starting point: <code>M ${this.props.x} ${this.props.y}</code>. This will move our brush to the initial coordinates. Then, we will connect each data point together with the <code>L x y</code> command.

However, we can’t pass <code>x</code> and <code>y</code> just as we get them from the data set. We need to sum them with a starting point for <code>x</code> and subtract from the starting point for <code>y</code>, because the y axis in SVG goes from top to bottom.

The resulting code looks like this:

<pre><code class="language-javascript">import React from 'react';

export default class GraphBody extends React.Component {
  static defaultProps = { multiplier: 20 };

  prepareData() {
    let d = [`M ${this.props.x} ${this.props.y}`];

    let collector = this.props.data.map(chunk =&gt; {
      let xNext = this.props.x + chunk[0] * this.props.multiplier;
      let yNext = this.props.y - chunk[1] * this.props.multiplier;
      return `L ${xNext} ${yNext}`;
    });

    return d.concat(collector).join(' ');
  }

  render() {
    let d = this.prepareData();
    return(
      &lt;path d={d}
        stroke="orange"
        strokeWidth={1}
        fill="none"
      /&gt;
    )
  }
}</code></pre>

I’ve also multiplied the coordinates by a constant just to make the graph prettier.</p>

<figure><a href="/wp-content/uploads/2015/10/29474-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7478633a-157b-4171-b9c5-46183a07239c/29474-opt-preview.png" alt="Adding support for multiple data sets is an easy task for us, thanks to React’s top-to-bottom data flow approach." /></a><figcaption>Adding support for multiple data sets is an easy task for us, thanks to React’s top-to-bottom data flow approach. (<a href="/wp-content/uploads/2015/10/29474-opt.png">View large version</a>)</figcaption></figure>

So, we’re ready to ship! But let’s say that just before that, our data changes. Suppose the data science department extends our data set by another array and asks us to create a way to switch data on the fly.

Our new <code>data.js</code> looks like this:

<pre><code class="language-javascript">export default [
 [
   [1, 3],
   [2, 5],
   [3, 2],
   [4, 16],
   [18, 5]
 ],
 [
   [1, 16],
   [2, 23],
   [3, 5],
   [4, 3],
   [5, 1]
 ]
];</code></pre>

Adding support for multiple data sets is an easy task for us, thanks to <strong>React’s top-to-bottom data flow approach</strong>. We just need to change the data that we are passing to the <code>Graph</code> component dynamically; React will do the re-rendering for us.

So, the new <code>index.js</code> is this:

<pre><code class="language-javascript">
import React from 'react';
import ReactDOM from 'react-dom';
import App from './app';
import data from './data';

ReactDOM.render(&lt;App datasets={data} /&gt;, document.getElementById('root'));</code></pre>

And here is <code>scripts/app.js</code>:

<pre><code class="language-javascript">import React from 'react';
import Graph from './components/graph';

export default class App extends React.Component {
  render() {
    return (
      &lt;Graph data={this.props.datasets[0]} /&gt; # or this.props.datasets[1] just to check that everything is working 
    )
  }
}</code></pre>

However, changing the data set in the code is not user-friendly at all (even if we have React Hot Load to magically update the page for us). So, let’s add an option to change the data set.

Here is <code>scripts/app.js</code>:

<pre><code class="language-javascript">import React from 'react';
import Graph from './components/graph'

export default class App extends React.Component {
  state = { dataSetIndex: 0 }

  selectDataset(event) {
    this.setState({dataSetIndex: event.target.value});
  }

  render() {
    let options = this.props.datasets.map((_, index) =&gt; {
      return &lt;option key={index} value={index}&gt;Dataset {index + 1}&lt;/option&gt;
    });

    return (
      &lt;div&gt;
        &lt;select
          value={this.state.dataSetIndex}
          onChange={this.selectDataset.bind(this)} &gt;
          {options}
        &lt;/select&gt;
        &lt;Graph data={this.props.datasets[this.state.dataSetIndex]} /&gt;
      &lt;/div&gt;
    )
  }
}</code></pre>

Now our data miners are happy; they can play with data sets on the fly!

But tomorrow comes, and now they want to be able to <strong>download rendered graphs to work with offline</strong>. Previously, that would mean a <a href="/2014/05/26/love-generating-svg-javascript-move-to-server/">lot of work</a>, but React has no real DOM dependency, so you can render it on a server easily.

We start by creating a simple <a href="https://expressjs.com/">Express</a> app that handles incoming requests for SVG graphs (<code>svg_server.js</code>):

<pre><code class="language-javascript">require("babel-register");
var express = require('express');
var app = express();
var data = require('./scripts/data').default;
var svgRenderer = require('./scripts/svg_renderer').default;

app.get('/svg', function (req, res) {
  var svg = svgRenderer(data[0]);
  res.send(svg);
});

var server = app.listen(3000, function () {
  var host = server.address().address;
  var port = server.address().port;
  console.log('Example app listening at https://%s:%s', host, port);
});</code></pre>

As you can see, only three lines are really from our application:

<pre><code class="language-javascript">var data = require('./scripts/data');
var svgRenderer = require('./scripts/svg_renderer');
var svg = svgRenderer(data[0]);</code></pre>

All of the other lines are just the Express boilerplate and hooks.

And <code>scripts/svg_renderer.js</code> will look a lot like our old version of the main <code>App</code>:

<pre><code class="language-javascript">
import React from 'react';
import ReactDOMServer from 'react-dom/server';
import Graph from './components/graph'

export default function(data) {
  return ReactDOMServer.renderToStaticMarkup(&lt;Graph data={data}/&gt;);
}</code></pre>

To test it, we would:

1.  run `node svg_server.js`,
2.  open `localhost:3000/svg`,
3.  and, to be fully sure, run `curl localhost:3000/svg`, and receive.</p>

<pre><code class="language-markup">&lt;svg width="800" height="600"&gt;&lt;line x1="20" y1="500" x2="820" y2="500" stroke="green" stroke-width="2"&gt;&lt;/line&gt;&lt;line x1="20" y1="0" x2="20" y2="500" stroke="green" stroke-width="2"&gt;&lt;/line&gt;&lt;path d="M 20 500 L 40 440 L 60 400 L 80 460 L 100 180 L 380 400" stroke="orange" stroke-width="1" fill="none"&gt;&lt;/path&gt;&lt;/svg&gt;</code></pre>

Server-side rendering!

Now, our data science department fully loves us and we can finally go home. If you missed anything, you can find the whole example <a href="https://github.com/somebody32/react-svg-smashing">in the repository</a>.

I hope this tutorial shows you that, <strong>from React’s perspective, there is no difference at all in what to render</strong>. You can leverage all of the ideas that shape your HTML in SVG, and have small, understandable components that anyone can easily change without breaking any external dependencies.

But should you create your own graph systems from scratch? No, plenty of great solutions can be extended easily to work with React (and even completed integrations — <a href="https://github.com/esbullington/react-d3">react-d3</a>, for example). My hope is that, in making this graph, you’ve come to understand how these integrations work under the hood.

A small warning before wrapping up. Keep in mind that React does not support all SVG elements right now (there are <a href="https://github.com/facebook/react/issues?utf8=%E2%9C%93&amp;q=is%3Aissue+is%3Aopen+svg">some limitations and missing pieces</a>), but you’ll probably find that it has what you need for the most common scenarios. For the less common ones, React provides a way to set the <code>innerHTML</code> of an element via <a href="https://facebook.github.io/react/tips/dangerously-set-inner-html.html">dangerouslySetInnerHTML</a>, which can help you work around any missing SVG elements you might require. Also, looks like many of these issues <a href="https://github.com/facebook/react/pull/5714">will be fixed</a> in the next React version.

Happy vectorizing!

{{< signature "ds, jb, ml, al" >}}


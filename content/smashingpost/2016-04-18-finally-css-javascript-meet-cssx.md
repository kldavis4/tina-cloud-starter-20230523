---
title: 'Finally, CSS In JS! Meet CSSX'
slug: finally-css-javascript-meet-cssx
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1de5e2ff-47f1-4c3d-9a82-9b1aca9c9f3f/01-cssx-preview-opt.jpg
date: 2016-04-18T16:12:12.000Z
author: krasimirtsonev
description: >-
  JavaScript is a wonderful language. It’s rich, it’s dynamic, and it’s so
  tightly coupled to the web nowadays. The concept of writing everything in
  JavaScript doesn’t sound so crazy anymore. First, **we started writing our
  back end in JavaScript**, and then Facebook introduced JSX, in which we mix
  HTML markup with JavaScript. Why not do the same for CSS?

  Imagine a web componentdistributed as a single `.js` file and containing
  everything — markup, logic and styles. We would still have our basic style
  sheets, but the dynamic CSS would be a part of JavaScript. Now this is
  possible, and one way to achieve it is with CSSX. CSSX is a project that
  swallowed my spare time for a month. It was challenging and interesting, and
  it definitely pushed me to learn a lot of new stuff. The result is a set of
  tools that allows you to write vanilla CSS in JavaScript.
categories:
  - Coding
  - CSS
  - JavaScript
---
JavaScript is a wonderful language. It’s rich, it’s dynamic, and it’s so tightly coupled to the web nowadays. The concept of writing everything in JavaScript doesn’t sound so crazy anymore. First, <strong>we started writing our back end in JavaScript</strong>, and then Facebook introduced <a href="https://facebook.github.io/react/docs/jsx-in-depth.html">JSX</a>, in which we mix HTML markup with JavaScript. Why not do the same for CSS in JS?

Imagine a web <a href="https://github.com/krasimir/react-cssx">component</a> distributed as a single <code>.js</code> file and containing everything — markup, logic and styles. We would still have our basic <a href="https://www.smashingmagazine.com/mastering-css-principles-comprehensive-reference-guide/">style sheets</a>, but the dynamic CSS would be a part of JavaScript. Now this is possible, and one way to achieve it is with <a href="https://github.com/krasimir/cssx">CSSX</a>. CSSX is a project that swallowed my spare time for a month. It was challenging and interesting, and it definitely pushed me to learn a lot of new stuff. The result is a set of tools that allows you to write vanilla CSS in JavaScript.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [React Native: Building Your First iOS App With JavaScript](https://www.smashingmagazine.com/2016/04/the-beauty-of-react-native-building-your-first-ios-app-with-javascript-part-1/)
*   [Styling Web Components Using A Shared Style Sheet](https://www.smashingmagazine.com/2016/12/styling-web-components-using-a-shared-style-sheet/)
*   [Enforcing Best Practices In Component-Based Systems](https://www.smashingmagazine.com/2017/01/styled-components-enforcing-best-practices-component-based-systems/)
*   [<span class="headline">Building A Cross-Platform WebGL Game With Babylon.js</span>](https://www.smashingmagazine.com/2016/07/babylon-js-building-sponza-a-cross-platform-webgl-game/)

Similar to JSX, CSSX offers encapsulation. Being able to see all parts of a single component is a big step forward. The <a href="https://en.wikipedia.org/wiki/Separation_of_concerns">separation of concerns</a> defined development for years, but the web is changing. Very often, we’ll work entirely in the browser, and Facebook’s approach with JSX makes a lot of sense. Understanding what is going on is easier when everything is in one place. We bind parts of JavaScript to parts of HTML anyway. By mixing both together, we’re just making these bindings explicit. If it works for HTML, it would definitely work for CSS.

{{% feature-panel %}}

## CSS In JS - The Concept

My thinking around putting CSS in JavaScript dates back to 2013, when I created a <a href="https://github.com/krasimir/absurd/">library</a> that started as a CSS preprocessor but that I converted to a client-side tool. The idea was simple: Convert object literals to valid CSS, which is later applied to the page. The styles “travel” with the JavaScript. They are bundled together, and you don’t have to manage external style sheets. While I was experimenting with this approach, I identified two issues:

*   Flash of unstyled text (FOUT) was the first problem. If we rely on JavaScript to deliver the CSS, then the user will see unstyled content for a second (or more) before getting the styled page. This results in layout shifts and leads to a bad user experience.
*   The second problem is that there is no style sheet. There are plenty of examples of styles being applied with JavaScript, but most of them are inline styles. In other words, they modify the `style` property of the DOM element. That’s fine, but we can’t go through all of the elements that need styling and change their attributes. Also, not everything can be placed in a `style` attribute — media queries and pseudo-classes, for example.

My goal was to solve these two problems, and I started shaping a solution. The following image illustrates how I imagined working with CSS in JavaScript:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63ed3a17-9fd0-4f11-9ad7-cdd712e022dc/01-cssx-opt.jpg"><img loading="lazy" decoding="async" class="alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1de5e2ff-47f1-4c3d-9a82-9b1aca9c9f3f/01-cssx-preview-opt.jpg" alt="css in js" width="500" height="237" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/63ed3a17-9fd0-4f11-9ad7-cdd712e022dc/01-cssx-opt.jpg">View large version</a>)</figcaption></figure>

There would be a library that stands between your code and the actual styles applied to the page. Its responsibility would be to create a virtual style sheet, and it would associate a <code>&lt;style&gt;</code> tag with it. Then, it would provide an API for managing CSS rules. Every interaction with your JavaScript style sheet would be mirrored to the injected <code>&lt;style&gt;</code> tag. With this approach, you would keep the dynamic styles tightly coupled to the JavaScript that controls it. You wouldn’t have to define new CSS classes because you would generate the CSS rules on the fly at runtime.

I prefer to generate and inject CSS because inline styling doesn’t scale. It’s technically easy, but it simply doesn’t scale. If there is CSS in JavaScript, we should be able to control it like a real style sheet. We should be able to define styles and then add, remove or update them inside. And those changes should be applied to the page just like the style sheet in a static file.

The FOUT problem is a matter of trade-offs. The question is not, “Should we put our CSS in JavaScript,” but rather, “What part of the CSS could be written in JavaScript?” Certainly the typography, the grid, the colors should all be in a static file so that browsers can consume it as quickly as possible. However, a ton of stuff is not needed immediately — for example, classes relating to state, like <code>is-clicked</code> and <code>is-activated</code>. In the world of single-page apps, <strong>everything generated by JavaScript can be styled with JavaScript</strong>. That’s because it does not appear before we have the whole JavaScript bundle. In a large-scale application, forming different blocks and keeping them separated is really important. The fewer the dependencies a single component has, the better. HTML and CSS are hard dependencies of our <a href="https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/">client-side JavaScript</a> views. Without them, we can’t really display content. Grouping them in one place would reduce the complexity of our projects.

Based on these conclusions, I started writing the CSSX client-side library.</p>

## Meet The CSSX Library

To make the <a href="https://github.com/krasimir/cssx/tree/master/packages/cssx">CSSX library</a> available, either include the <a href="https://github.com/krasimir/cssx/tree/master/packages/cssx/lib">cssx.min.js</a> file on your page or install the npm module by running <code>npm install cssx</code>. If you have a build process, then you’ll probably be interested in the npm package.

An online demo is <a href="https://krasimir.github.io/cssx/playground/try-it-out-bin/">available on GitHub</a>. You can see CSSX in action there.

(The CSSX client-side library is needed so that the CSSX is injected at runtime. Later, we will see what other modules are required to support the vanilla CSS syntax. Till then, let’s focus on the JavaScript-only API.)

Here is a very basic example of one style sheet with one rule registered in it:

<pre><code class="language-javascript">
var sheet = cssx();
sheet.add('p &gt; a', {
  'font-size': '20px'
});
</code></pre>

If we ran this in a browser, we’d see a new <code>style</code> tag injected in the head of the document:

<pre><code class="language-markup">
&lt;style id="_cssx1" type="text/css"&gt;p &gt; a{font-size:20px;}&lt;/style&gt;
</code></pre>

The <code>add</code> method accepts a selector and CSS properties as an object literal. This works, but it’s a static declaration. There would be almost no benefit to doing this in JavaScript. We could just as easily place these styles in our external CSS file. Let’s transform the code to the following:

<pre><code class="language-javascript">
var sheet = cssx();
var rule = sheet.add('p &gt; a');
var setFontSize = function (size) {
  return { 'font-size': size + 'px' };
};

rule.update(setFontSize(20));
…
rule.update(setFontSize(24));
</code></pre>

Now there’s another thing. We are now able to change the font size dynamically. The result of the code above is this:

<pre><code class="language-css">
p &gt; a {
  font-size: 24px;
}
</code></pre>

So, writing CSS in JavaScript now becomes a composition of object literals. We may use all of the features of the JavaScript language to build them. Simple things like defining a variable, using factory functions and extending base classes are here by default. Encapsulation, reusability, modularity — we get all of these things for free.

The CSSX library has a minimalist API, mainly because JavaScript is really flexible. The composition of the CSS is left to the developer. The exposed functions revolve around the production of actual styles. For example, while writing CSS, we tend to create groups. Some of these groups are formed by the structure of the layout — styles for the header, the sidebar and the footer. Here is how to scope the styles using a CSSX rule object:

<pre><code class="language-javascript">
var sheet = cssx();

// `header` is a CSSX rule object
var header = sheet.add('.header');

header.descendant('nav', { margin: '10px' });
header.descendant('nav a', { float: 'left' });
header.descendant('.hero', { 'font-size': '3em' });
</code></pre>

The result of this snippet is this:

<pre><code class="language-css">
.header nav {
  margin: 10px;
}
.header nav a {
  float: left;
}
.header .hero {
  font-size: 3em;
}
</code></pre>

Instead of <code>header.descendant</code>, we may use <code>header.d</code>. It would be annoying to have to write <code>descendant</code> all of the time; so, a <code>.d</code> shortcut exists.

We have another method similar to <code>descendant</code> — <code>nested</code>. Instead of chaining the selectors, the library would nest the definitions. Here is an example:

<pre><code class="language-javascript">
var smallScreen = sheet.add('@media all and (max-width: 320px)');
smallScreen.nested('body', { 'font-size': '10px' });

/* results in
@media all and (max-width: 320px) {
  body {
    font-size: 10px;
  }
}
*/
</code></pre>

This API may be used to create media queries or <code>@keyframes</code> definitions. In theory, this is enough to produce a Sass-like output. There is also the <code>.n</code> shortcut, instead of <code>.nested</code>.

So far, we’ve seen how to produce valid CSS that gets applied to the page at runtime. However, writing styles like that takes a lot of time, and even though our code has a good structure, it’s not as nice as writing vanilla CSS.

## The Challenging Part: Actual CSS Syntax In JavaScript

As we’ve seen, writing CSS in the format shown above is not really nice, mainly because we have to wrap almost everything in quotation marks. We can do some optimization, like using camel casing, creating helpers for the different units and so on, but it’s still not as clean and simple as regular CSS. Placing vanilla CSS in JavaScript leads to the well-known unexpected token error, because the JavaScript engine is not designed to accept code in such a format. OK, then, how do we introduce the syntax we want? JSX created it, right? Well, it didn’t. We don’t have actual HTML tags working in JavaScript. What’s happening is that we translate (or, more accurately, <strong>transpile</strong>) JSX to valid JavaScript at buildtime. The final bundle that is executed in the browser contains valid code. Here is an example:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79993316-c4dc-4b95-967d-6811de366fa3/02-transpiler-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/48fbbe73-63b6-463e-9429-c11b6472bfd4/02-transpiler-preview-opt.jpg" alt="CSSX" width="500" height="315" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/79993316-c4dc-4b95-967d-6811de366fa3/02-transpiler-opt.jpg">View large version</a>)</figcaption></figure>

Of course, this comes at a cost: one more step in our build process, more configuration and more things to think about. But, to be honest, I’m ready to trade that for better code organization and scalability. JSX simply makes our life better by hiding the complexity of managing HTML templates.

And JSX was exactly what I wanted, but for CSS. I started digging into <a href="https://babeljs.io/">Babel</a>, because that’s the official transpiler of JSX at the moment. It uses the <a href="https://github.com/babel/babylon">Babylon</a> module to parse the source code and transform it to an <a href="https://en.wikipedia.org/wiki/Abstract_syntax_tree">abstract syntax tree</a> (AST). Later, the <a href="https://github.com/babel/babel/tree/master/packages/babel-generator">babel-generator</a> parses that tree and turns it into valid JavaScript code. That’s how Babel understands JSX. It uses same approach for the ES6 features that are still not supported by all the browsers.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02b4aaf3-1e8d-40f4-8c7a-988532d895ac/03-babel-transpile-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/136a997b-68ea-430a-a187-93bbebe08b04/03-babel-transpile-preview-opt.jpg" alt="Babel transpiler" width="500" height="315" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/02b4aaf3-1e8d-40f4-8c7a-988532d895ac/03-babel-transpile-opt.jpg">View large version</a>)</figcaption></figure>

So, all I had to do is see how Babylon understands JSX and do the same for CSS. The module is written like so, so it allows extension from the outside. In fact, almost anything can be changed. JSX is a plugin there, and I was keen to create one for CSSX.

I knew about AST and how helpful it can be, but I never spent time learning how to generate one. It is basically a process of reading small chunks (or tokens) of the code, one by one. We have a bunch of assertions trying to form a meaningful sequence of tokens. If something is recognized, then we define a context and continue parsing until we exit the current context and continue with another one. Of course, there are many edge cases that have to be covered. And the fun part is that we can’t extend the parser until we know every little detail about it. It took me a couple of weeks to read and really understand what is going on there.

In the beginning, I made the mistake of following the JSX plugin’s implementation. I can’t tell you how many times I started the CSSX plugin. Every time, I ended up with something that either didn’t fully cover the CSS syntax or broke JavaScript’s syntax. Then, I realized that<strong> JSX is quite different</strong>, and I started extending only what CSS needs. The test-driven development approach worked perfectly here. I should mention that Babylon has more then 2100 tests. And that’s absolutely reasonable considering that the module understands such a rich and dynamic language like JavaScript.

I had to make a couple of interesting design decisions. First, I tried parsing code like this:

<pre><code class="language-javascript">
var styles = {
  margin: 0,
  padding: 0
}
</code></pre>

Everything was going fine until I decided to run my plugin against all of the tests in Babylon. The parser usually produces an <code>ObjectExpression</code> node from this code, but I was doing something else because I <em>recognized</em> this as CSSX. I effectively broke the JavaScript language. There is no way to find out what we have until we parse the whole block. That’s why I decided to use another syntax:

<pre><code class="language-javascript">
var styles = cssx({
  margin: 0;
  padding: 0;
});
</code></pre>

We are explicitly saying here that we are writing a CSSX expression. Tweaking the parser is much easier when we have a clear entry point. JSX does not have this problem because HTML is not even close to JavaScript, and there are no such conflicts.

I was using CSSX with the <code>cssx( … )</code> notation for a while, but then I realized that I could replace it with <code>&lt;style&gt; … &lt;/style&gt;</code>. It was a cheap switch. Every time the code lands in the parser, just before processing it, we run a simple <a href="https://github.com/krasimir/babylon-plugin-cssx/blob/master/src/index.js#L26-L28">regex replacement</a>:

<pre><code class="language-javascript">
code = code.replace(/&lt;style&gt;/g, 'cssx(').replace(/&lt;\/style&gt;/g, ')');
</code></pre>

This helps us write the following:

<pre><code class="language-javascript">
var styles = &lt;style&gt;{
  margin: 0;
  padding: 0;
}&lt;/style&gt;;
</code></pre>

And we have the same result in the end.</p>

## Start Writing Vanilla CSS In JavaScript

Let’s say we have a tool that understands CSSX and produces proper AST. The next step is to get a transpiler that generates valid JavaScript. The package that deals with that is <a href="https://github.com/krasimir/cssx/tree/master/packages/cssx-transpiler">CSSX-Transpiler</a>. Under the hood, we are still using <code>babel-generator</code>, but only after we substitute our custom CSSX nodes with something that Babel understands. Another helpful module is <a href="https://github.com/babel/babel/tree/master/packages/babel-types">babel-types</a>. There are a ton of utility functions, and without them, generating a tree for the generator would be really difficult.</p>

### Types of CSSX Expressions

Let’s see a couple of simple transformations.</p>

<pre><code class="language-javascript">
var styles = &lt;style&gt;{
  font-size: 20px;
  padding: 0;
}&lt;/style&gt;;
</code></pre>

This is transformed to the following:

<pre><code class="language-javascript">
var styles = (function () {
  var _2 = {};
  _2['padding'] = '0';
  _2['font-size'] = '20px';
  return _2;
}.apply(this));
</code></pre>

That’s the first type, where we produce a simple object literal. The equivalent of the code above is this:

<pre><code class="language-javascript">
var styles = {
  'font-size': '20px',
  'padding': '0'
};
</code></pre>

If you scroll up, you will see that that’s exactly what we need in the CSSX client-side library. If we operated with a lot of those, then it would be nice to use vanilla CSS.

The second expression contains more information. It bundles the whole CSS rule — selector and properties:

<pre><code class="language-javascript">
var sheet = &lt;style&gt;
  .header &gt; nav {
    font-size: 20px;
    padding: 0;
  }
&lt;/style&gt;;
</code></pre>

Here is the transpiled JavaScript:

<pre><code class="language-javascript">
var sheet = (function () {
  var _2 = {};
  _2['padding'] = '0';
  _2['font-size'] = '20px';

  var _1 = cssx('_1');

  _1.add('.header &gt; nav', _2);

  return _1;
}.apply(this));
</code></pre>

Note that we are defining a new style sheet — <code>cssx('_1')</code> — I should clarify that if we run this code twice, we won’t be creating an additional <code>&lt;style&gt;</code> tag. We’d be using the same one because <code>cssx()</code> receives the same ID (<code>_1</code>) and returns the same style sheet object.

If we added more CSS rules, we’d see more <code>_1.add()</code> lines.</p>

### Going Dynamic

As mentioned, the main benefit of writing CSS in JavaScript is to gain access to wider range of tools, such as defining a function that gets a number and outputs a <code>font-size</code> rule. I had hard time deciding on the syntax for these “dynamic parts.” In JSX, this is solved easily by wrapping code in braces. Again, doing the same in CSSX would be difficult because braces conflict with other stuff. We always use them when defining CSS rules. So, I initially decided to replace them with the grave accent (or the backtick):

<pre><code class="language-javascript">
var size = 20;
var styles = &lt;style&gt;
  .header &gt; nav {
    font-size: `size + 2`px;
    padding: 0;
  }
&lt;/style&gt;;
</code></pre>

The result would be this:

<pre><code class="language-css">
.header &gt; nav {
  padding: 0;
  font-size: 22px;
}
</code></pre>

We can use dynamic parts everywhere. Whatever we place inside is considered valid JavaScript and is executed.</p>

<pre><code class="language-javascript">
var size = 20;
var prop = 'size';
var selector = 'header';
var styles = &lt;style&gt;
  .`selector` &gt; nav {
    font-`prop`: `size + 2`px;
    padding: 0;
  }
&lt;/style&gt;;
</code></pre>

Similar to JSX, the code is transformed to valid JavaScript:

<pre><code class="language-javascript">
var size = 20;
var prop = 'size';
var selector = 'header';
var styles = (function () {
  var _2 = {};
  _2['padding'] = '0';
  _2["font-" + prop] = size + 2 + "px";

  var _1 = cssx('_1');

  _1.add("." + selector + " &gt; nav", _2);

  return _1;
}.apply(this));
</code></pre>

I should mention that the self-invoking function around the transpiled code is needed to keep the right scope. The code we place inside the so-called dynamic expressions should use the right context. Otherwise, we’d probably be requesting access to undefined variables or would be reading from the global scope. The other reason to use a closure is to avoid collisions with other parts of our application.

After getting some feedback, I decided to support two other syntaxes for those dynamic expressions. Some solid refactoring was needed for the code that defines words inside CSSX. Now, it is possible to use <code>{{ … }}</code> or <code>&lt;% … %&gt;</code>:

<pre><code class="language-javascript">
var size = 20;
var styles = &lt;style&gt;
  .header &gt; nav {
    font-size: px;
    padding: 0;
  }
&lt;/style&gt;;
</code></pre>

## “Show Me The Code!”

Let’s build something real and see how CSSX works in practice. And because CSSX is inspired by JSX, we’ll create a simple <a href="https://facebook.github.io/react/">React</a> navigation menu. The result will look like this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3921c252-a9e0-4181-8669-8c2a23df9e71/04-react-example-opt.gif" alt="React CSSX example" width="204" height="293" /></figure>

(The final source code of this example is <a href="https://github.com/krasimir/cssx/tree/master/playground/react">available on GitHub</a>. Simply download the files, and install the dependencies with <code>npm install</code>. Then, run <code>npm run dev</code> to compile the JavaScript, and open <code>example/index.html</code> in a browser. A <a href="https://krasimir.github.io/cssx/playground/react/example/">live demo</a> of the result is also available.)

### The Base

We’ve already established that CSSX is not meant to serve all of the CSS. It should contain only those bits that are dynamic. The basic CSS in this example would be as follows:

<pre><code class="language-css">
body {
  font-family: Helvetica, Tahoma;
  font-size: 18px;
}
ul {
  list-style: none;
  max-width: 200px;
}
ul, li {
  margin: 0;
  padding: 0;
}
li {
  margin-bottom: 4px;
}
</code></pre>

Our navigation will be made up of an unordered list of items. Every item will contain an <code>&lt;a&gt;</code> tag, which represents the clickable area.</p>

### The Navigation Component

(Don’t worry if you are not familiar with React. The same code can be applied in other frameworks. What is important here is how we use CSSX to style the buttons and define their behavior.)

The first thing we have to do is render links on the page. Let’s say that the items in the list will come to the component as an <code>items</code> property. We’ll loop through them and create <code>&lt;li&gt;</code> tags.</p>

<pre><code class="language-css">
class Navigation extends React.Component {
  constructor(props) {
    super(props);
    this.state = { color: '#2276BF' };
  }
  componentWillMount() {
    // Create our style sheet here
  }
  render() {
    return &lt;ul&gt;{ this._getItems() }&lt;/ul&gt;;
  }
  _getItems() {
    return this.props.items.map((item, i) =&gt; {
      return (
        &lt;li key={ i }&gt;
          &lt;a className='btn' onClick={ this._handleClick.bind(this, i) }&gt;
            { item }
          &lt;/a&gt;
        &lt;/li&gt;
      )
    })
  }
  _handleClick(index) {
    // Handle link's click here
  }
}
</code></pre>

We’ve put a <code>color</code> variable in the component’s state and will use it later in our style sheet. Because the styles will be generated at runtime, we may go even further by writing a function that returns the color. Note that, by placing the CSS in the JavaScript, we are no longer living in the static, declarative land of CSS!

As it is, the component is ready for rendering.</p>

<pre><code class="language-javascript">
const ITEMS = [
  'React',
  'Angular',
  'Vue',
  'Ember',
  'Knockout',
  'Vanilla'
];

ReactDOM.render(
  &lt;Navigation items={ ITEMS } /&gt;,
  document.querySelector('body')
);
</code></pre>

The browser simply displays our <code>ITEMS</code> on the screen. Within the static CSS, we’ve removed the default bullets of the unordered list and cleared the space around the items. The result is this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e5d80b1-a3b7-4d74-8feb-06ef796a26d4/05-react-example-opt.png" alt="React CSSX example" width="128" height="128" /></figure>

Now, let’s add some CSSX and define the initial look of the items. A good place to do this is the <code>componentWillMount</code> function because it’s the method that is fired before the component gets on the page.</p>

<pre><code class="language-javascript">
componentWillMount() {
  var color = this.state.color;
  &lt;style&gt;
    li {
      padding-left: 0;
      (w)transition: padding-left 300ms ease;
    }
    .btn {
      display: block;
      cursor: pointer;
      padding: 0.6em 1em;
      border-bottom: solid 2px `color`;
      border-radius: 6px;        
      background-color: `shadeColor(color, 0.5)`;
      (w)transition: background-color 400ms ease;
    }
    .btn:hover {
      background-color: `shadeColor(color, 0.2)`;
    }
  &lt;/style&gt;;
}
</code></pre>

Notice how we’ve used CSSX expressions to define the bottom border’s color and the background color. <code>shadeColor</code> is a helper function that accepts a color in HEX format and shades it based on the second parameter (which is between <code>-1</code> and <code>1</code>). That’s not really important right now. The result of this code is a new style sheet injected in the <code>head</code> of the page. The CSS there is exactly what we need:

<pre><code class="language-css">
li {
  padding-left: 0;
  transition: padding-left 300ms ease;
  -webkit-transition: padding-left 300ms ease;
}
.btn {
  background-color: #91bbdf;
  border-radius: 6px;
  border-bottom: solid 2px #2276BF;
  padding: 0.6em 1em;
  cursor: pointer;
  display: block;
  transition: background-color 400ms ease;
  -webkit-transition: background-color 400ms ease;
}
.btn:hover {
  background-color: #4e91cc;
}
</code></pre>

The <code>(w)</code> in front of the properties generates a prefixed version.

Now, our navigation is not simple text anymore:

If you scroll up, you will see that that’s exactly what we need in the CSSX client-side library. If we operated with a lot of those, then it would be nice to use vanilla CSS.

The second expression contains more information. It bundles the whole CSS rule — selector and properties:

<pre><code class="language-javascript">
var sheet = &lt;style&gt;
  .header &gt; nav {
    font-size: 20px;
    padding: 0;
  }
&lt;/style&gt;;
</code></pre>

Here is the transpiled JavaScript:

<pre><code class="language-javascript">
var sheet = (function () {
  var _2 = {};
  _2['padding'] = '0';
  _2['font-size'] = '20px';

  var _1 = cssx('_1');

  _1.add('.header &gt; nav', _2);

  return _1;
}.apply(this));
</code></pre>

Note that we are defining a new style sheet — <code>cssx('_1')</code> — I should clarify that if we run this code twice, we won’t be creating an additional <code>&lt;style&gt;</code> tag. We’d be using the same one because <code>cssx()</code> receives the same ID (<code>_1</code>) and returns the same style sheet object.

If we added more CSS rules, we’d see more <code>_1.add()</code> lines.</p>

### Going Dynamic

As mentioned, the main benefit of writing CSS in JavaScript is to gain access to wider range of tools, such as defining a function that gets a number and outputs a <code>font-size</code> rule. I had hard time deciding on the syntax for these “dynamic parts.” In JSX, this is solved easily by wrapping code in braces. Again, doing the same in CSSX would be difficult because braces conflict with other stuff. We always use them when defining CSS rules. So, I initially decided to replace them with the grave accent (or the backtick):

<pre><code class="language-javascript">
var size = 20;
var styles = &lt;style&gt;
  .header &gt; nav {
    font-size: `size + 2`px;
    padding: 0;
  }
&lt;/style&gt;;
</code></pre>

The result would be this:

<pre><code class="language-css">
.header &gt; nav {
  padding: 0;
  font-size: 22px;
}
</code></pre>

We can use dynamic parts everywhere. Whatever we place inside is considered valid JavaScript and is executed.</p>

<pre><code class="language-javascript">
var size = 20;
var prop = 'size';
var selector = 'header';
var styles = &lt;style&gt;
  .`selector` &gt; nav {
    font-`prop`: `size + 2`px;
    padding: 0;
  }
&lt;/style&gt;;
</code></pre>

Similar to JSX, the code is transformed to valid JavaScript:

<pre><code class="language-javascript">
var size = 20;
var prop = 'size';
var selector = 'header';
var styles = (function () {
  var _2 = {};
  _2['padding'] = '0';
  _2["font-" + prop] = size + 2 + "px";

  var _1 = cssx('_1');

  _1.add("." + selector + " &gt; nav", _2);

  return _1;
}.apply(this));
</code></pre>

I should mention that the self-invoking function around the transpiled code is needed to keep the right scope. The code we place inside the so-called dynamic expressions should use the right context. Otherwise, we’d probably be requesting access to undefined variables or would be reading from the global scope. The other reason to use a closure is to avoid collisions with other parts of our application.

After getting some feedback, I decided to support two other syntaxes for those dynamic expressions. Some solid refactoring was needed for the code that defines words inside CSSX. Now, it is possible to use <code>{{ … }}</code> or <code>&lt;% … %&gt;</code>:

<pre><code class="language-javascript">
var size = 20;
var styles = &lt;style&gt;
  .header &gt; nav {
    font-size: px;
    padding: 0;
  }
&lt;/style&gt;;
</code></pre>

## “Show Me The Code!”

Let’s build something real and see how CSSX works in practice. And because CSSX is inspired by JSX, we’ll create a simple <a href="https://facebook.github.io/react/">React</a> navigation menu. The result will look like this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3921c252-a9e0-4181-8669-8c2a23df9e71/04-react-example-opt.gif" alt="React CSSX example" width="204" height="293" /></figure>

(The final source code of this example is <a href="https://github.com/krasimir/cssx/tree/master/playground/react">available on GitHub</a>. Simply download the files, and install the dependencies with <code>npm install</code>. Then, run <code>npm run dev</code> to compile the JavaScript, and open <code>example/index.html</code> in a browser. A <a href="https://krasimir.github.io/cssx/playground/react/example/">live demo</a> of the result is also available.)

### The Base

We’ve already established that CSSX is not meant to serve all of the CSS. It should contain only those bits that are dynamic. The basic CSS in this example would be as follows:

<pre><code class="language-css">
body {
  font-family: Helvetica, Tahoma;
  font-size: 18px;
}
ul {
  list-style: none;
  max-width: 200px;
}
ul, li {
  margin: 0;
  padding: 0;
}
li {
  margin-bottom: 4px;
}
</code></pre>

Our navigation will be made up of an unordered list of items. Every item will contain an <code>&lt;a&gt;</code> tag, which represents the clickable area.</p>

### The Navigation Component

(Don’t worry if you are not familiar with React. The same code can be applied in other frameworks. What is important here is how we use CSSX to style the buttons and define their behavior.)

The first thing we have to do is render links on the page. Let’s say that the items in the list will come to the component as an <code>items</code> property. We’ll loop through them and create <code>&lt;li&gt;</code> tags.</p>

<pre><code class="language-css">
class Navigation extends React.Component {
  constructor(props) {
    super(props);
    this.state = { color: '#2276BF' };
  }
  componentWillMount() {
    // Create our style sheet here
  }
  render() {
    return &lt;ul&gt;{ this._getItems() }&lt;/ul&gt;;
  }
  _getItems() {
    return this.props.items.map((item, i) =&gt; {
      return (
        &lt;li key={ i }&gt;
          &lt;a className='btn' onClick={ this._handleClick.bind(this, i) }&gt;
            { item }
          &lt;/a&gt;
        &lt;/li&gt;
      )
    })
  }
  _handleClick(index) {
    // Handle link's click here
  }
}
</code></pre>

We’ve put a <code>color</code> variable in the component’s state and will use it later in our style sheet. Because the styles will be generated at runtime, we may go even further by writing a function that returns the color. Note that, by placing the CSS in the JavaScript, we are no longer living in the static, declarative land of CSS!

As it is, the component is ready for rendering.</p>

<pre><code class="language-javascript">
const ITEMS = [
  'React',
  'Angular',
  'Vue',
  'Ember',
  'Knockout',
  'Vanilla'
];

ReactDOM.render(
  &lt;Navigation items={ ITEMS } /&gt;,
  document.querySelector('body')
);
</code></pre>

The browser simply displays our <code>ITEMS</code> on the screen. Within the static CSS, we’ve removed the default bullets of the unordered list and cleared the space around the items. The result is this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1e5d80b1-a3b7-4d74-8feb-06ef796a26d4/05-react-example-opt.png" alt="React CSSX example" width="128" height="128" /></figure>

Now, let’s add some CSSX and define the initial look of the items. A good place to do this is the <code>componentWillMount</code> function because it’s the method that is fired before the component gets on the page.</p>

<pre><code class="language-javascript">
componentWillMount() {
  var color = this.state.color;
  &lt;style&gt;
    li {
      padding-left: 0;
      (w)transition: padding-left 300ms ease;
    }
    .btn {
      display: block;
      cursor: pointer;
      padding: 0.6em 1em;
      border-bottom: solid 2px `color`;
      border-radius: 6px;        
      background-color: `shadeColor(color, 0.5)`;
      (w)transition: background-color 400ms ease;
    }
    .btn:hover {
      background-color: `shadeColor(color, 0.2)`;
    }
  &lt;/style&gt;;
}
</code></pre>

Notice how we’ve used CSSX expressions to define the bottom border’s color and the background color. <code>shadeColor</code> is a helper function that accepts a color in HEX format and shades it based on the second parameter (which is between <code>-1</code> and <code>1</code>). That’s not really important right now. The result of this code is a new style sheet injected in the <code>head</code> of the page. The CSS there is exactly what we need:

<pre><code class="language-css">
li {
  padding-left: 0;
  transition: padding-left 300ms ease;
  -webkit-transition: padding-left 300ms ease;
}
.btn {
  background-color: #91bbdf;
  border-radius: 6px;
  border-bottom: solid 2px #2276BF;
  padding: 0.6em 1em;
  cursor: pointer;
  display: block;
  transition: background-color 400ms ease;
  -webkit-transition: background-color 400ms ease;
}
.btn:hover {
  background-color: #4e91cc;
}
</code></pre>

The <code>(w)</code> in front of the properties generates a prefixed version.

Now, our navigation is not simple text anymore:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e7f54a48-06bc-4535-bc61-5adff93e2b9d/06-react-example2-opt.png" alt="React CSSX example" width="157" height="223" /><br>
<figcaption>React CSSX example.</figcaption></figure>

The last bit of our component is the interaction with the user. If we click on some of the links, they should shrink from the left and a static background color should be set. In the <code>_handleClick</code> function, we’ll receive the index of the clicked item; so, we can use <code>nth-child</code> CSS selector to style the correct button:

<pre><code class="language-javascript">
_handleClick(index) {
  &lt;style&gt;
    li:nth-child({{ index + 1 }}) {
      padding-left: 2em;
    }
    li:nth-child({{ index + 1 }}) .btn {
      background-color: {{ this.state.color }};
    }
  &lt;/style&gt;;
}
</code></pre>

This works but there is one problem. An item that has been clicked is not restored to its initial state if we click on another link. After two clicks, for example, our document might contain the following:

<pre><code class="language-css">
li:nth-child(4) {
  padding-left: 2em;
}
li:nth-child(4) .btn {
  background-color: #2276BF;
}
li:nth-child(3) {
  padding-left: 2em;
}
li:nth-child(3) .btn {
  background-color: #2276BF;
}
</code></pre>

So, we have to clear the style sheet before styling the clicked item.</p>

<pre><code class="language-javascript">
var stylesheet, row;

// creating a new style sheet
stylesheet = cssx('selected');

// clearing all the styles
stylesheet.clear();

// adding the styles
stylesheet.add(
  &lt;style&gt;
  li:nth-child({{ index + 1 }}) {
    padding-left: 2em;
  }
  li:nth-child({{ index + 1 }}) .btn {
    background-color: {{ this.state.color }};
  }
  &lt;/style&gt;
);
</code></pre>

Or, if we go with method chaining, we’d have this:

<pre><code class="language-javascript">
cssx('selected')
  .clear()
  .add(
    &lt;style&gt;
      li:nth-child({{ index + 1 }}) {
        padding-left: 2em;
      }
      li:nth-child({{ index + 1 }}) .btn {
        background-color: {{ this.state.color }};
      }
    &lt;/style&gt;
  );
</code></pre>

Notice that we’ve specified an ID of the style sheet: <code>selected</code>. This is important; otherwise, we’d get a different style sheet every time.

With the change above, our example works exactly as the animated GIF at the beginning of this section.

Even with such a simple example, we can recognize some of CSSX’s benefits:

*   We don’t have to deal with additional CSS classes.
*   There is no interaction with the DOM because we don’t have to add or remove CSS classes.
*   We have real dynamic CSS, tightly coupled with the logic of the component.</p>

## Summary

HTML and CSS in JavaScript might seem strange, but the truth is that we have been doing it for years. We precompile our templates and place them in JavaScript. We form HTML as strings, and we use inline styling produced by JavaScript. So, why not use the same syntax directly?

In the last year, I’ve used <a href="https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/">React</a> heavily, and I can say that JSX is not bad at all. In fact, it improves maintainability and shortens the time spent getting into a new project.

I’m still experimenting with CSSX. I do see similarities with JSX in the workflow and result. If you want to see how it works, <a href="https://krasimir.github.io/cssx/playground/try-it-out-bin/">check out the demo</a>.</p>

## Links

### Language

*   [CSSX language](https://github.com/krasimir/cssx/blob/master/docs/cssx-lang.md), GitHub

### Packages

*   [CSSX](https://github.com/krasimir/cssx/tree/master/packages/cssx) (client-side library)
*   [CSSX-transpiler](https://github.com/krasimir/cssx/tree/master/packages/cssx-transpiler)
*   [gulp-cssx](https://github.com/krasimir/cssx/tree/master/packages/gulp-cssx) (plugin)
*   [cssx-loader](https://github.com/krasimir/cssx/tree/master/packages/cssx-loader) (for Webpack)

### Examples

*   “[Using Vanilla CSS in React Applications](https://github.com/krasimir/react-cssx),” GitHub CSSX component for React applications
*   [CSSX playground](https://krasimir.github.io/cssx/playground/try-it-out/)
    *   [Basic](https://github.com/krasimir/cssx/tree/master/playground/basic)
    *   [Transpiler](https://github.com/krasimir/cssx/tree/master/playground/transpiler)
    *   [transpiler-gulp](https://github.com/krasimir/cssx/tree/master/playground/transpiler-gulp)
    *   [transpiler-webpack](https://github.com/krasimir/cssx/tree/master/playground/transpiler-webpack)
    *   [React](https://github.com/krasimir/cssx/tree/master/playground/react) (On which our example is based)

{{< signature "rb, ml, al, il" >}}


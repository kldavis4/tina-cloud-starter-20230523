---
title: Writing Reusable Components in ES6
slug: writing-reusable-components-es6
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/933561a8-4d8d-487e-8f39-06ae5a4ee515/js-opt.png'
date: 2016-02-03T02:29:15.000Z
author: jimcowart
description: >-
  Are you excited to **take advantage of new JavaScript language features** but
  not sure _where_ to start, or _how_? You're not alone! I've spent the better
  part of the last year and a half trying to ease this pain. During that time
  there have been some amazing quantum leaps in JavaScript tooling.

  These leaps have made it possible for you and me to dive head first into
  writing fully ES6 modules, without compromising on the essentials like
  testing, linting and (most importantly) the ability for others to easily
  consume what we write.
categories:
  - Coding
  - JavaScript
---
Are you excited to <strong>take advantage of new JavaScript language features</strong> but not sure <em>where</em> to start, or <em>how</em>? You're not alone! I've spent the better part of the last year and a half trying to ease this pain. During that time there have been some amazing quantum leaps in JavaScript tooling.

These leaps have made it possible for you and me to dive head first into writing fully ES6 modules, without compromising on the essentials like testing, linting and (most importantly) the ability for others to easily consume what we write.</p>

<figure><a href="https://github.com/lukehoban/es6features"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/933561a8-4d8d-487e-8f39-06ae5a4ee515/js-opt.png" alt="Writing Next Generation Reusable JavaScript Modules" width="500" height="500" /></a><figcaption>ECMAScript 6 is here. An <a href="https://github.com/lukehoban/es6features">overview of fancy and useful features in the new version of JavaScript</a>.</figcaption></figure>

In this post, we're going to focus on <strong>how to create a JavaScript package written in ES6</strong> that's usable in a site or app regardless of whether you're using CommonJS, asynchronous module definition (AMD) or plain browser global modules.</p>

<blockquote><strong>Wait, is it ES6 or ES2015?</strong> My habits certainly prefer ES6, but the name was recently and officially changed to ES2015. However, there's a greater level of awareness of ES6, which is how I will refer to it in this post.

{{% feature-panel %}}

<p>I'd also like to give special thanks to <a href="https://twitter.com/dougneiner">Doug Neiner</a> and <a href="https://twitter.com/rpniemeyer">Ryan Niemeyer</a> – both have shared this journey into better ES6 tooling. This post wouldn't have been possible without them.</p></blockquote>

## The Tools

In parts 1 and 2 of this series, we'll look at some of the tools that make this possible. Today we'll cover writing, transpiling and packaging our library; and in part 2 we'll focus on linting, formatting and testing (using JSCS, ESLint, mocha, Chai, Karma and Istanbul). Meet your new best friends for part 1:

*   [Babel](https://babeljs.io/) (which just celebrated its first birthday) has made the process of transpiling ES6 to ES5 not only simple, but _pleasant_.
*   [webpack](https://webpack.github.io/) silenced every aspect of the "module wars" on my team by letting us consume _everything_ (CommonJS, AMD and ES6) with aplomb. It turns out that webpack also does a fantastic job of packaging standalone ES6 libraries – a fact we will look at closely during this post.
*   [Gulp](https://gulpjs.com/) is a powerful tool for automating build-related tasks.</p>

## The Goal

### Write In ES6, Use In ES5

We're going to talk about writing ES6 client-side <em>libraries</em>, not bundling entire sites or apps. (This is really any reusable bit of code you'd like to share between projects, whether it's an open source software project or something you use internally at work between applications.) <i>"Wait a second"</i>, you might be thinking. <i>"Won't it be a while until the browser range I have to support can handle ES6?"</i>

That's correct! However, I mentioned <a href="https://babeljs.io/">Babel</a> above because we're going to use it to convert our ES6 to ES5, making it a practical option to use today for most situations.</p>

<div class="c-felix-the-cat">
<h4 class="h3">What's New In ES6</h4>
<p>ES6 is the next big version of JavaScript, and it has some great new features. The features have varying degrees of complexity and are useful in both simple scripts and complex applications. Let's cover a <strong>hand-picked selection of ES6 features</strong> that you can use in your everyday JavaScript coding, shall we? <a href="https://www.smashingmagazine.com/2015/10/es6-whats-new-next-version-javascript/" class="btn btn--medium btn--blue">Read a related article →</a></p>
</div>

### Make It Easy For Anyone To Consume

The second part of our goal is to write a module that we could use in most common module ecosystems. Die-hard AMD fan? You get a module. CommonJS plus browserify the only song you sing? And <em>you</em> get a module. Not sure what the AMD versus CommonJS fuss is about, and you just want to drop the <code>&lt;script&gt;</code> tag on the page and go? <em>You</em> get a module too! It's a bit like an Oprah module giveaway – where the part of Oprah is played by <a href="https://webpack.github.io/">webpack</a>. webpack will help package our module in a special wrapper called a <a href="https://github.com/umdjs/umd">universal module definition (UMD)</a>, making it possible to consume in any of the above scenarios.</p>

## Setting Up Our Project

Over the next few minutes, we'll be working towards the <a href="https://github.com/ifandelse/legoQuotes/releases/tag/v1.0.0">resulting code here</a>. I usually start a project off with <i>src/</i>, <i>spec/</i> and <i>lib/</i> folders. In our <i>src/</i> folder, you'll see a contrived but fun set of example modules that, when used together, let us retrieve a random quote from a <a href="https://www.imdb.com/title/tt1490017/">Lego Movie</a> character. While the behavior is fairly useless, this example makes use of <a href="https://www.2ality.com/2015/02/es6-classes-final.html">classes</a>, <a href="https://www.2ality.com/2014/09/es6-modules-final.html">modules</a>, <code><a href="https://www.2ality.com/2015/02/es6-scoping.html">const</a></code>, <a href="https://www.2ality.com/2015/01/es6-destructuring.html">destructuring</a>, a <a href="https://www.2ality.com/2015/03/es6-generators.html">generator</a> and more – all features we'd like to safely transpile to ES5.

The main focus of this post is to discuss how to use Babel and webpack to transpile and package an ES6 library. However, I also wanted to take a brief look at our example code so that you can see that we are indeed using ES6.

<strong>Note:</strong> Don't worry if you're new to ES6 syntax. These examples are simple enough to follow.</p>

## The LegoCharacter Class

In our <i>LegoCharacter.js</i> module, we see the following (be sure to read the comments for more explanation):

<pre><code class="language-javascript">// LegoCharacter.js
// Let's import only the getRandom method from utils.js
import { getRandom } from "./utils";

// the LegoCharacter class is the default export of the module, similar
// in concept to how many node module authors would export a single value
export default class LegoCharacter {
   // We use destructuring to match properties on the object
   // passed into separate variables for character and actor
   constructor( { character, actor } ) {
      this.actor = actor;
      this.name = character;
      this.sayings = [
         "I haven't been given any funny quotes yet."
      ];
   }
   // shorthand method syntax, FOR THE WIN
   // I've been making this typo for years, it's finally valid syntax :)
   saySomething() {
      return this.sayings[ getRandom( 0, this.sayings.length - 1 ) ];
   }
}
</code></pre>

Pretty boring on its own – this class is meant to be extended, which we do in our <i>Emmet.js</i> module:

<pre><code class="language-javascript">// emmet.js
import LegoCharacter from "./LegoCharacter";

// Here we use the extends keyword to make
// Emmet inherit from LegoCharacter
export default class Emmet extends LegoCharacter {
   constructor() {
      // super lets us call the LegoCharacter's constructor
      super( { actor: "Chris Pratt", character: "Emmet" } );
      this.sayings = [
         "Introducing the double-decker couch!",
         "So everyone can watch TV together and be buddies!",
         "We're going to crash into the sun!",
         "Hey, Abraham Lincoln, you bring your space chair right back!",
         "Overpriced coffee! Yes!"
      ];
   }
}
</code></pre>

Both <i>LegoCharacter.js</i> and <i>emmet.js</i> are separate <em>files</em> in our project – this will be case for each module in our example. Depending on how you've been writing JavaScript, this might seem a bit foreign to you. By the time we're done, though, we'll have a ‘built’ version that combines them together.</p>

## The index.js

Our <i>index.js</i> – another file in our project – is the main entry point for our library. It imports a few Lego character classes, creates instances of them and provides a generator function to <code>yield</code> a random quote any time a caller asks for one:

<pre><code class="language-javascript">// index.js
// Notice that lodash isn't being imported via a relative path
// but all the other modules are. More on that in a bit :)
import _ from "lodash";
import Emmet from "./emmet";
import Wyldstyle from "./wyldstyle";
import Benny from "./benny";
import { getRandom } from "./utils";

// Taking advantage of new scope controls in ES6
// once a const is assigned, the reference cannot change.
// Of course, transpiling to ES5, this becomes a var, but
// a linter that understands ES6 can warn you if you
// attempt to re-assign a const value, which is useful.
const emmet = new Emmet();
const wyldstyle = new Wyldstyle();
const benny = new Benny();
const characters = { emmet, wyldstyle, benny };

// Pointless generator function that picks a random character
// and asks for a random quote and then yields it to the caller
function* randomQuote() {
   const chars = _.values( characters );
   const character = chars[ getRandom( 0, chars.length - 1 ) ];
   yield `${character.name}: ${character.saySomething()}`;
}

// Using object literal shorthand syntax, FTW
export default {
   characters,
   getRandomQuote() {
      return randomQuote().next().value;
   }
};
</code></pre>

In a nutshell, the <i>index.js</i> module imports lodash, the classes for our three Lego characters and a utility function. It then creates instances of our Lego characters and exports them (makes them available to consuming code) as well as the <code>getRandomQuote</code> method. If all goes well, when this code is transpiled to ES5 it should still do exactly the same thing.

## OK. Now What?

We have all this shiny new JavaScript, but how do we transpile it to ES5? First, let's install Babel using <a href="https://docs.npmjs.com/getting-started/installing-npm-packages-globally">npm</a>:

<pre><code class="language-bash">npm install -g babel</code></pre>

Installing Babel globally gives us a <code>babel</code> <a href="https://babeljs.io/docs/usage/cli/">command line interface (CLI) option</a>. If we navigate to our project's root directory and type this, we can transpile the modules to ES5 and drop them in the <i>lib/</i> directory:

<pre><code>babel ./src -d ./lib/</code></pre>

Looking at our <i>lib</i> folder, we'll see these files listed:

<pre><code class="language-bash">LegoCharacter.js
benny.js
emmet.js
index.js
utils.js
wyldstyle.js
</code></pre>

Remember how I mentioned above that we were putting each of our ES6 modules into its own file? Babel has taken each of those files, converted them to ES5 and written them to the same file structure in our <i>lib</i> folder. A quick glance at these files might tell you a couple of things:

*   First, these files could be consumed in node right now, as long as the _[babel/register](https://babeljs.io/docs/usage/require/)_ runtime dependency was required first. You'll see an example of these running in node before the end of this post. (Transpiling typically involves a runtime dependency even though many – but not all – of these features are now available natively in [node v4](https://nodejs.org/en/docs/es6/).)
*   Second, we still have some work to do so that these files can be packaged into _one_ file and wrapped in a [universal module definition (UMD)](https://github.com/umdjs/umd) and used in a browser.</p>

## Enter webpack

Odds are you've heard of <a href="https://webpack.github.io/">webpack</a>, whose description calls it "a bundler for JavaScript and friends." The most common use case for webpack is to act as a bundler and loader for a website, enabling you to bundle your JavaScript, as well as other assets like CSS and templates, into one (or more) files. webpack has an amazing ecosystem of "loaders," which are transformations applied to files loaded by webpack. While building a UMD isn't the <em>most common</em> use case for webpack, it turns out we can use a webpack loader to load our ES6 modules and transpile them to ES5, and webpack's bundling process to build out a single output file of our example project.</p>

### Loaders

Used extensively in webpack, loaders can do things like transpile ES6 to ES5, Less to CSS, load JSON files, render templates and <em>much</em> more. Loaders take a <code>test</code> pattern to use for matching files that they should transform. Many loaders can take additional configuration options as well, which we'll be making use of. (Curious as to what other loaders exist? Check out <a href="https://webpack.js.org/loaders/">this list</a>.)

Let's go ahead and install webpack globally (which gives us a webpack <a href="https://webpack.github.io/docs/cli.html">CLI</a>):

<pre><code class="language-bash">npm install -g webpack</code></pre>

Next we can install <a href="https://www.npmjs.com/package/babel-loader">babel-loader</a> to our local project. This loader enables webpack to load our ES6 modules and transpile them to ES5. We can install it, and save it to our package.json's <code>devDependencies</code> by running this:

<pre><code class="language-bash">npm install --save-dev babel-loader</code></pre>

Before we can use webpack, though, we need to create a webpack configuration file that tells webpack what we want it to do with our source files. Usually named <i>webpack.config.js</i>, a webpack configuration file is a node.js module that exports a set of configuration values telling webpack what to do.

Here's our initial <i>webpack.config.js</i> file. I've commented the code heavily, and we'll also discuss some of the important details below:

<pre><code class="language-javascript">module.exports = {
   // entry is the "main" source file we want to include/import
   entry: "./src/index.js",
   // output tells webpack where to put the bundle it creates
   output: {
      // in the case of a "plain global browser library", this
      // will be used as the reference to our module that is
      // hung off of the window object.
      library: "legoQuotes",
      // We want webpack to build a UMD wrapper for our module
      libraryTarget: "umd",
      // the destination file name
      filename: "lib/legoQuotes.js"
   },
   // externals let you tell webpack about external dependencies
   // that shouldn't be resolved by webpack.
   externals: [
      {
         // We're not only webpack that lodash should be an
         // external dependency, but we're also specifying how
         // lodash should be loaded in different scenarios
         // (more on that below)
         lodash: {
            root: "_",
            commonjs: "lodash",
            commonjs2: "lodash",
            amd: "lodash"
         }
      }
   ],
   module: {
      loaders: [
         // babel loader, testing for files that have a .js extension
         // (except for files in our node_modules folder!).
         {
            test: /\.js$/,
            exclude: /node_modules/,
            loader: "babel",
            query: {
               compact: false // because I want readable output
            }
         }
      ]
   }
};
</code></pre>

So let's look at a couple of key values in our configuration.</p>

## Output

A webpack configuration file can be given an <code>output</code> object that describes how webpack should build and package the source. In our example above, we're telling webpack to output a UMD library to our <i>lib/</i> directory.</p>

## Externals

You might have noticed our example library uses lodash. We want our built library to be smart enough to require lodash from an external source, rather than have to include lodash itself in the output. The <code>externals</code> option in a webpack config file lets you specify the dependencies that should remain external. In the case of lodash, its global property key (<code>_</code>) is not the same as its name ("lodash"), so our configuration above tells webpack how to require lodash for each given module scenario (CommonJS, AMD and browser root).</p>

## The Babel Loader

You'll notice that our babel-loader just calls itself "babel" for the loader name. This is a webpack naming convention: where the module name is "myLoaderName-loader", webpack treats it as "myLoaderName."

We're testing for any file ending in <i>.js</i>, except for files that live under our <i>node_modules/</i> folder. The <code>compact</code> option we're passing to the babel loader turns off whitespace compression because I'd like our unminified built source to be readable. (We'll add a minified build in a moment.)

If we run <code>webpack</code> in our console at the project root, it will see our <i>webpack.config.js</i> file and build our library, giving us output similar to this:

<pre><code class="language-bash">» webpack
Hash: f33a1067ef2c63b81060
Version: webpack 1.12.1
Time: 758ms
            Asset     Size  Chunks             Chunk Names
lib/legoQuotes.js  12.5 kB       0  [emitted]  main
    + 7 hidden modules
</code></pre>

If we look in our <i>lib/</i> folder, we'll see a newly minted <i>legoQuotes.js</i> file. This time, the contents are wrapped in webpack's UMD, which we can see in this snippet:

<pre><code class="language-javascript">(function webpackUniversalModuleDefinition(root, factory) {
   if(typeof exports === 'object' &amp;&amp; typeof module === 'object')
      module.exports = factory(require("lodash"));
   else if(typeof define === 'function' &amp;&amp; define.amd)
      define(["lodash"], factory);
   else if(typeof exports === 'object')
      exports["legoQuotes"] = factory(require("lodash"));
   else
      root["legoQuotes"] = factory(root["_"]);
})(this, function(__WEBPACK_EXTERNAL_MODULE_1__) {

// MODULE CODE HERE

});
</code></pre>

This UMD performs one kind of CommonJS check, then an AMD check, then another style of CommonJS and finally it falls back to plain browser globals. You can see how it knew to look for lodash as "lodash" if we were in a CommonJS or AMD environment, and to look for <code>_</code> on the window (root) if we were dealing with plain browser globals.</p>

## What Happened, Exactly?

When we ran <code>webpack</code> in our console, it looked for the default name of a configuration file (<i>webpack.config.js</i>), and read the configuration. From there it saw that the <i>src/index.js</i> file was our main entry point, and began loading it and its dependencies (except for lodash, which we told webpack was external). Each of these dependencies is a <i>.js</i> file, so the babel loader would be run on the file, transpiling it from ES6 to ES5 as it was loaded. From there, all files loaded were written to a single output file, <i>legoQuotes.js</i>, which is dropped into the <i>lib</i> folder.

Looking at the module code you'll see that our ES6 source has indeed been transpiled to ES5. For example, our <code>LegoCharacter</code> class is now an ES5 constructor function:

<pre><code class="language-javascript">// around line 179
var LegoCharacter = (function () {
   function LegoCharacter(_ref) {
      var character = _ref.character;
      var actor = _ref.actor;
      _classCallCheck(this, LegoCharacter);
      this.actor = actor;
      this.name = character;
      this.sayings = ["I haven't been given any funny quotes yet."];
   }

   _createClass(LegoCharacter, [{
      key: "saySomething",
      value: function saySomething() {
         return this.sayings[(0, _utils.getRandom)(0, this.sayings.length - 1)];
      }
   }]);

   return LegoCharacter;
})();
</code></pre>

## [](#its-usable)It's Usable!

At this point we could include this built file in both a browser (IE9+, as a general rule) and node and it would work in either, as long as the babel runtime dependency is included.

If we wanted to use this in the browser, it would look something like this:

<pre><code class="language-markup">&lt;!-- index.html --&gt;
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
   &lt;meta charset="utf-8"&gt;
   &lt;meta http-equiv="X-UA-Compatible" content="IE=edge"&gt;
   &lt;title&gt;Lego Quote Module Example&lt;/title&gt;
   &lt;link rel="stylesheet" href="style.css"&gt;
&lt;/head&gt;
&lt;body&gt;
   &lt;div class="container"&gt;
      &lt;blockquote id="quote"&gt;&lt;/blockquote&gt;
      &lt;button id="btnMore"&gt;Get Another Quote&lt;/button&gt;
   &lt;/div&gt;
   &lt;script src="../node_modules/lodash/index.js"&gt;&lt;/script&gt;
   &lt;script src="../node_modules/babel-core/browser-polyfill.js"&gt;&lt;/script&gt;
   &lt;script src="../lib/legoQuotes.js"&gt;&lt;/script&gt;
   &lt;script src="./main.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

You can see we've included our <i>legoQuotes.js</i> file (just below babel's <i>browser-polyfill.js</i> file) just like any other <code>&lt;script&gt;</code> tag (above). Our <i>main.js</i> file, which uses our legoQuotes library, looks like this:

<pre><code class="language-javascript">// main.js
( function( legoQuotes ) {
   var btn = document.getElementById( "btnMore" );
   var quote = document.getElementById( "quote" );

   function writeQuoteToDom() {
      quote.innerHTML = legoQuotes.getRandomQuote();
   }

   btn.addEventListener( "click", writeQuoteToDom );
   writeQuoteToDom();
} )( legoQuotes );
</code></pre>

To use it in node, it would look like this:

<pre><code class="language-javascript">require("babel/polyfill");
var lego = require("./lib/legoQuotes.js");
console.log(lego.getRandomQuote());
// &gt; Wyldstyle: Come with me if you want to not die.
</code></pre>

## Moving To Gulp

Both Babel's and webpack's CLIs are very useful, but it's common to use a task runner such as Gulp to handle executing these kinds of tasks. This consistency can pay off if you participate in many projects, as the main CLI commands you'll need to remember consist of <code>gulp someTaskName</code>. I don't think there's a right or wrong answer here, for the most part. If you prefer the CLIs, use them. Using Gulp is simply one possible way to go about it.</p>

### [](#build-task)Setting Up A Build Task

First, let's install gulp:

<pre><code class="language-bash">npm install -g gulp</code></pre>

Next, let's create a gulp file that can run what we have done so far. We'll use the <a href="https://www.npmjs.com/package/webpack-stream">webpack-stream</a> gulp plugin, which I've installed by running <code>npm install --save-dev webpack-stream</code>. This plugin can consume our <i>webpack.config.js</i> file and allow webpack to play nicely with gulp.</p>

<pre><code class="language-javascript">// gulpfile.js
var gulp = require( "gulp" );
var webpack = require( "webpack-stream" );

gulp.task( "build", function() {
   return gulp.src( "src/index.js" )
      .pipe( webpack( require( "./webpack.config.js" ) ) )
      .pipe( gulp.dest( "./lib" ) )
} );
</code></pre>

Since I'm using gulp to source our <i>index.js</i> and to write to the output directory, I've tweaked the <i>webpack.config.js</i> file by removing <code>entry</code> and updating the <code>filename</code>. I've also added a <a href="https://webpack.js.org/configuration/devtool/"><code>devtool</code></a> prop, set to the value of <code>#inline-source-map</code> (this will write a source map at the end of the file in a comment):

<pre><code class="language-javascript">// webpack.config.js
module.exports = {
   output: {
      library: "legoQuotes",
      libraryTarget: "umd",
      filename: "legoQuotes.js"
   },
   devtool: "#inline-source-map",
   externals: [
      {
         lodash: {
            root: "_",
            commonjs: "lodash",
            commonjs2: "lodash",
            amd: "lodash"
         }
      }
   ],
   module: {
      loaders: [
         {
            test: /\.js$/,
            exclude: /node_modules/,
            loader: "babel",
            query: {
               compact: false
            }
         }
      ]
   }
};
</code></pre>

### [](#minifying)What About Minifying?

I'm glad you asked! One approach to minifying can be done using the <a href="https://www.npmjs.com/package/gulp-uglify">gulp-uglify</a> plugin, along with <a href="https://www.npmjs.com/package/gulp-sourcemaps">gulp-sourcemaps</a> (since we'd like a source map for our min file) and <a href="https://www.npmjs.com/package/gulp-rename">gulp-rename</a> (which lets us target a different file name so we don't overwrite our non-minified build). I've added both to our project via:

<pre><code class="language-bash">npm install --save-dev gulp-uglify gulp-sourcemaps gulp-rename</code></pre>

In this approach, our unminified source will still have an inline source map, but our usage of gulp-sourcemaps below will cause the minified file's source map to be written as a separate file (with a comment in the minified file pointing to the source map file):

<pre><code class="language-javascript">// gulpfile.js
var gulp = require( "gulp" );
var webpack = require( "webpack-stream" );
var sourcemaps = require( "gulp-sourcemaps" );
var rename = require( "gulp-rename" );
var uglify = require( "gulp-uglify" );

gulp.task( "build", function() {
   return gulp.src( "src/index.js" )
      .pipe( webpack( require( "./webpack.config.js" ) ) )
      .pipe( gulp.dest( "./lib" ) )
      .pipe( sourcemaps.init( { loadMaps: true } ) )
      .pipe( uglify() )
      .pipe( rename( "legoQuotes.min.js" ) )
      .pipe( sourcemaps.write( "./" ) )
      .pipe( gulp.dest( "lib/" ) );
} );
</code></pre>

If we run <code>gulp build</code> in our console, we should see something similar to:

<pre><code class="language-bash">» gulp build
[19:08:25] Using gulpfile ~/git/oss/next-gen-js/gulpfile.js
[19:08:25] Starting 'build'...
[19:08:26] Version: webpack 1.12.1
        Asset     Size  Chunks             Chunk Names
legoQuotes.js  23.3 kB       0  [emitted]  main
[19:08:26] Finished 'build' after 1.28 s
</code></pre>

Our <i>lib/</i> directory will now contain three files: <i>legoQuotes.js</i>, <i>legoQuotes.min.js</i> and <i>legoQuotes.min.js.map</i>. Not only does everyone attending the <del>Oprah</del> <ins>webpack</ins> show get a module, but they also get a sourcemap to make debugging the minified file a possibility.</p>

## [](#banner-plugin)Webpack Banner Plugin

If you need to include a licence comment header at the top of your built files, webpack makes it easy. I've updated our <i>webpack.config.js</i> file to include the <code><a href="https://webpack.js.org/plugins/banner-plugin/#src/components/Sidebar/Sidebar.jsx">BannerPlugin</a></code>. I don't like hardcoding the banner's information if I don't need to, so I've imported the <i>package.json</i> file to get the library's information. I also converted the <i>webpack.config.js</i> file to ES6, and am using a <a href="https://www.2ality.com/2015/01/template-strings-html.html">template string</a> to render the banner. Towards the bottom of the <i>webpack.config.js</i> file you can see I've added a <code>plugins</code> property, with the <code>BannerPlugin</code> as the only plugin we're currently using:

<pre><code class="language-javascript">// webpack.config.js
import webpack from "webpack";
import pkg from "./package.json";
var banner = `
   ${pkg.name} - ${pkg.description}
   Author: ${pkg.author}
   Version: v${pkg.version}
   Url: ${pkg.homepage}
   License(s): ${pkg.license}
`;

export default {
   output: {
      library: pkg.name,
      libraryTarget: "umd",
      filename: `${pkg.name}.js`
   },
   devtool: "#inline-source-map",
   externals: [
      {
         lodash: {
            root: "_",
            commonjs: "lodash",
            commonjs2: "lodash",
            amd: "lodash"
         }
      }
   ],
   module: {
      loaders: [
         {
            test: /\.js$/,
            exclude: /node_modules/,
            loader: "babel",
            query: {
               compact: false
            }
         }
      ]
   },
   plugins: [
      new webpack.BannerPlugin( banner )
   ]
};
</code></pre>

<em>(Note: It's worth mentioning that by converting my webpack.config.js file to ES6, I can't run it via the webpack CLI any longer.)</em>

Our updated <i>gulpfile.js</i> includes two additions: the requiring of the babel register hook (on line 1) and the passing of options to the gulp-uglify plugin:

<pre><code class="language-javascript">// gulpfile.js
require("babel/register");
var gulp = require( "gulp" );
var webpack = require( "webpack-stream" );
var sourcemaps = require( "gulp-sourcemaps" );
var rename = require( "gulp-rename" );
var uglify = require( "gulp-uglify" );

gulp.task( "build", function() {
   return gulp.src( "src/index.js" )
      .pipe( webpack( require( "./webpack.config.js" ) ) )
      .pipe( gulp.dest( "./lib" ) )
      .pipe( sourcemaps.init( { loadMaps: true } ) )
      .pipe( uglify( {
         // This keeps the banner in the minified output
         preserveComments: "license",
         compress: {
            // just a personal preference of mine
               negate_iife: false
            }
      } ) )
      .pipe( rename( "legoQuotes.min.js" ) )
      .pipe( sourcemaps.write( "./" ) )
      .pipe( gulp.dest( "lib/" ) );
} );
</code></pre>

## [](#whats-next)What's Next?

We're a good way into our journey! So far we've stepped through a quick evolution of using babel and webpack's CLIs to build our library, then moved on to use gulp (and related plugins) to handle the build for us. The <a href="https://github.com/ifandelse/legoQuotes/releases/tag/v1.0.0">code related to this post</a> includes an <i>example/</i> directory with both a browser- and node-based example of our working transpiled module. In our next post, we'll look at using ESLint and JSCS for linting and formatting, mocha and chai to write tests, Karma to run those tests and istanbul to measure our test coverage. In the meantime, you might want to check out “<a href="https://www.smashingmagazine.com/2012/10/designing-javascript-apis-usability/">Designing Better JavaScript APIs</a>,” a fantastic article that can help guide you in writing better modules.

{{< signature "rb, jb, ml, og" >}}


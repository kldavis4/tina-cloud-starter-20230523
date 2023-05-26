---
title: Optimizing Critical-Path Performance With Express Server And Handlebars
slug: optimizing-critical-path-performance-with-express-server-and-handlebars
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0ed9ad4-69a6-4359-b3e4-ba6d968635e4/03-criticalcss-schema-preview-opt.png
date: 2016-08-03T17:41:50.000Z
author: filipbartos
description: >-
  Recently, I’ve been working on an isomorphic React website. This website was
  developed using React, running on an Express server. Everything was going
  well, but I still wasn’t satisfied with a load-blocking CSS bundle. So, I
  started to think about options for how to implement the critical-path
  technique on an Express server.

  This article contains my notes about **installing and configuring a
  critical-path performance optimization** using Express and Handlebars.
  Throughout this article, I’ll be using Node.js and Express. Familiarity with
  them will help you understand the examples.
categories:
  - Coding
  - CSS
  - Performance
  - Node.js
  - React
---
Recently, I’ve been working on an isomorphic React website. This website was developed using React, running on an Express server. Everything was going well, but I still wasn’t satisfied with a load-blocking CSS bundle. So, I started to think about options for how to implement the critical-path technique on an Express server.

This article contains my notes about **installing and configuring a critical-path performance optimization** using Express and Handlebars.</p>

## <span class="rh">Further reading</span> on Smashing:

*   [Perceived Performance](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/)
*   [Getting Ready For HTTP/2](https://www.smashingmagazine.com/2016/02/getting-ready-for-http2/)
*   [Front-End Performance Checklist 2017](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)

## Prerequisites

Throughout this article, I’ll be using Node.js and Express. Familiarity with them will help you understand the examples.

{{% feature-panel %}}

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f244bb0e-5b67-4927-9815-de7a7ffa671d/01-criticalcss-article-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/03d9e420-eff0-43a5-8b7c-52f77f9af3ef/01-criticalcss-article-preview-opt.png" alt="Lifecycle of Critical Path Performance Optimization" width="500" height="163" /></a><figcaption>Lifecycle of critical-path performance optimization (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f244bb0e-5b67-4927-9815-de7a7ffa671d/01-criticalcss-article-opt.png">View large version</a>)</figcaption></figure>

### tl;dr

I have [prepared a repository](https://github.com/FilipBartos/express-handlebars-criticalcss "Express-handlebars-criticalcss") with a quick and easy demo.</p>

## The Basics

Critical-path optimization is a technique that eliminates render-blocking CSS. This technique can dramatically increase the speed at which a website loads. The aim of this method is to get rid of the time that a user waits for a CSS bundle to load. Once the bundle has loaded, the browser saves it to its cache, and any subsequent reloads are served from the cache. Based on this, our objectives are the following:

*   Distinguish between the first and second (and nth) loads.
*   On the first load, load the CSS bundle asynchronously, and attach a load event listener so that we can find out when the bundle is ready to be served.
*   While the bundle is being loaded, inline some small critical CSS, to make the user experience as similar as possible to the end result.
*   Once the event listener reports that the CSS bundle is ready, remove the inline CSS and serve the bundle.
*   Ensure that other sources (JavaScript bundles, etc.) are not blocking the rendering.</p>

## Detecting The First Load

To detect the first load, we are going to use a cookie. If a cookie has not been set, then that means it’s the first load. Otherwise, it will be the second or nth load.</p>

## Loading The CSS Bundle Asynchronously

To start asynchronously downloading the CSS bundle, we are going to use a simple technique involving an invalid `media` attribute value. Setting the `media` attribute to an invalid value will cause the CSS bundle to download asynchronously but will not apply any styles until the `media` attribute has been set to a valid value. In other words, in order to apply styles from the CSS bundle, we will change the `media` attribute to a valid value once the bundle has loaded.</p>

## Critical CSS Vs. CSS Bundle

We will keep critical styles inline in the markup only during the downloading of the CSS bundle. Once the bundle has loaded, that critical CSS will be removed from the markup. To do this, we will also create some critical JavaScript, which will basically be a little JavaScript handler.</p>

## Lifecycle

To sum up, here is simple schema of our lifecycle:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd91a16d-e098-4466-9407-5dff5fa5baf6/02-criticalcss-graph-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e05632bd-7eec-40f1-925c-8f504b5076ad/02-criticalcss-graph-preview-opt.png" alt="Lifecycle of critical path performance optimization" width="500" height="262" /></a><figcaption>Lifecycle of critical-path performance optimization (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd91a16d-e098-4466-9407-5dff5fa5baf6/02-criticalcss-graph-opt.png">View large version</a>)</figcaption></figure>

## Going Isomorphic

Now that you know more about this technique, imagine it in combination with an isomorphic JavaScript application. Isomorphic JavaScript, also called universal JavaScript, simply means that an application written in JavaScript is able to run and generate HTML markup on the server. If you are curious, read more about React’s approach regarding [ReactDOM.renderToString](https://facebook.github.io/react/docs/top-level-api.html#reactdomserver.rendertostring) and [ReactDOM.renderToStaticMarkup](https://facebook.github.io/react/docs/top-level-api.html#reactdomserver.rendertostaticmarkup).

You might still be wondering why we need to generate HTML on the server. Well, think about the first load. When using client-side-only code, our visitors will have to wait for the JavaScript bundle. While the JavaScript bundle is being loaded, visitors will see a blank page or a preloader. I believe that the goal of front-end developers should be to minimize such scenarios. With isomorphic code, it’s different. Instead of a blank page and preloader, visitors will see the generated markup, even without the JavaScript bundle. Of course, the CSS bundle will also take some time to load, and without it our visitors will see only unstyled markup. Thankfully, using critical-path performance optimization, this is easy to solve.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17e0c875-346c-4600-b001-2a834679bec6/03-criticalcss-schema-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e0ed9ad4-69a6-4359-b3e4-ba6d968635e4/03-criticalcss-schema-preview-opt.png" alt="Isomorphic JavaScript application" width="500" height="439" /></a><figcaption>Isomorphic JavaScript application (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17e0c875-346c-4600-b001-2a834679bec6/03-criticalcss-schema-opt.png">View large version</a>)</figcaption></figure>

## Preparing The Environment

### Express

Express is a minimal and flexible Node.js web application framework.

First, install all of the required packages: `express`, `express-handlebars` and `cookie-parser`. `express-handlebars` is a Handlebars views engine for Express, and `cookie-parser` will help us with cookies later.</p>

<pre><code class="language-bash">npm install express express-handlebars cookie-parser --save-dev</code></pre>

Create a `server.js` file with imports of those packages. We will also use the `path` package later, which is part of Node.js.</p>

<pre><code class="language-javascript">import express from 'express';
import expressHandlebars from 'express-handlebars';
import cookieParser from 'cookie-parser';
import path from 'path';</code></pre>

Create the Express application:

<pre><code class="language-javascript">var app = express();</code></pre>

Mount `cookie-parser`:

<pre><code class="language-javascript">app.use(cookieParser());</code></pre>

Our CSS bundle will be available at `/assets/css/bundle.css`. To serve static files from Express, we have to set the path name of the directory where our static files are. This can be done using the built-in middleware function `express.static`. Our files will be in a directory named `build`; so, the local file at `/build/assets/css/bundle.css` will be served by the browser at `/assets/css/bundle.css`.</p>

<pre><code class="language-javascript">app.use(express.static('build'));</code></pre>

For the purpose of this demonstration, setting up a single HTTP `GET` route (`/`) will suffice:

<pre><code class="language-javascript">// Register simple HTTP GET route for /
app.get('/', function(req, res){
  // Send status 200 and render content. Content, in this case, is a non-existent template. For me, rendering the layout is important.
  res.status(200).render('content');
});</code></pre>

And let’s bind Express to listen on port `3000`:

<pre><code class="language-javascript">// Set the server port to 3000, and log the message when the server is ready.
app.listen(3000, function(){
  console.log('Local server is listening…');
});</code></pre>

## Babel And ES2016

Given the ECMAScript 2016 (or ES2016) syntax, we are going to install Babel and its presets. Babel is a JavaScript compiler that enables us to use next-generation JavaScript today. Babel presets are just a specific Babel transformation logic extracted into smaller groups of plugins (or presets). Our demo requires React and ES2015 presets.</p>

<pre><code class="language-bash">npm install babel-core babel-preset-es2015 babel-preset-react --save-dev</code></pre>

Now, create a `.babelrc` file with the following code. This is where we’re essentially saying, “Hey Babel, use these presets”:

<pre><code class="language-json">{
  "presets": [
    "es2015",
    "react"
  ]
}</code></pre>

As Babel’s [documentation says](https://babeljs.io/docs/setup/#babel_register), to handle ES2016 syntax, Babel requires a `babel-core/register` hook at the entry point of the application. Otherwise, it will throw an error. Let’s create `entry.js`:

<pre><code class="language-javascript">require("babel-core/register");
require('./server.js');</code></pre>

Now, test the configuration:

<pre><code class="language-bash">$ node entry.js</code></pre>

Your terminal should log this message:

<pre><code class="language-bash">Local server is listening…</code></pre>

However, if you navigate your browser to [https://localhost:3000/](https://localhost:3000/), you will get this error:

<pre><code class="language-bash">Error: No default engine was specified and no extension was provided.</code></pre>

This simply means that Express doesn’t know what or how to render. We’ll get rid of this error in the next section.</p>

## Handlebars

[Handlebars](https://handlebarsjs.com/) is referred to as “minimal templating on steroids.” Let’s set it up. Open `server.js`:

<pre><code class="language-javascript">// register new template engine
// first parameter = file extension
// second parameter = callback = expressHandlebars
// defaultLayout is the name of default layout located in layoutsDir.
app.engine('handlebars', expressHandlebars(
{
  defaultLayout: 'main',
  layoutsDir:    path.join(__dirname, 'views/layouts'),
  partialsDir: path.join(__dirname, 'views/partials')
}
));
// register new view engine
app.set('view engine', 'handlebars');</code></pre>

Create the directories `views/layouts` and `views/partials`. In `views/layouts`, create a file named `main.handlebars`, and insert the following HTML. This will be our main layout.</p>

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;en&quot;&gt;
  &lt;head&gt;
    &lt;meta charset=&quot;UTF-8&quot;&gt;
    &lt;title&gt;Critical-Path Performance Optimization&lt;/title&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;assets/css/bundle.css&quot; id=&quot;cssbundle&quot; media=&quot;none&quot;/&gt;
  &lt;/head&gt;
  &lt;body&gt;
  &lt;/body&gt;
&lt;/html&gt;</code></pre>

Also create a file named `content.handlebars` in `views` directory, and insert the following HTML.</p>

<pre><code class="language-markup">&lt;div id=&quot;app&quot;&gt;magic here&lt;/div&gt;</code></pre>

Start the server now:

<pre><code class="language-bash">$ node entry.js</code></pre>

Go to [https://localhost:3000](https://localhost:3000). The error is gone, and the layout’s markup is ready.</p>

## Critical Path

Our environment is ready. Now, we can implement the critical-path optimization.</p>

### Determining The First Load

As you will recall, our first objective is to determine whether or not a load is the first. Based on this, we can decide whether to serve critical styles or the CSS bundle from the browser’s cache. We will use a cookie for this. If a cookie is set, then that means it’s not the first load; otherwise, it is. The cookie will be created in the critical JavaScript file, which will be injected inline in the template with the critical styles. Checking for the cookie will be handled by Express.

Let’s name the critical JavaScript file `fastjs`. We must be able to insert the content of `fastjs` in the layout file if a cookie doesn’t exist. I’ve found Handlebars partials to be pretty easy to use. Partials are useful when you have markup that you want to reuse in multiple places. They can be called by other templates and are mostly used for the header, footer, navigation and so on.

In the Handlebars section, I’ve defined a partials directory at `/views/partials`. Let’s create a `/views/partials/fastjs.handlebars` file. In this file, we’ll add a script tag with an ID of `fastjs`. We will use this ID later to remove the script from the DOM.</p>

<pre><code class="language-markup">&lt;script id='fastjs'&gt;
&lt;/script&gt;</code></pre>

Now, open `/views/layouts/main.handlebars`. Calling the partial is done through the syntax `{{> partialName }}`. This code will be replaced by the contents of our target partial. Our partial is named `fastjs`, so add the following line before the end of the `head` tag:

<pre><code class="language-markup">&lt;head&gt;
…
{{&gt; fastjs}}
&lt;/head&gt;</code></pre>

The markup at [https://localhost:3000](https://localhost:3000) now contains the contents of the `fastjs` partial. A cookie will be created using this simple JavaScript function.</p>

<pre><code class="language-markup">&lt;script id='fastjs'&gt;
// Let's create a cookie named 'fastweb', setting its value to 'cache' and its expiration to one day
createCookie('fastweb', 'cache', 1);

// function to create cookie
function createCookie(name,value,days) {
  var expires = &quot;&quot;;
  if (days) {
    var date = new Date();
    date.setTime(date.getTime()+(days*24*60*60*1000));
    var expires = &quot;; expires=&quot;+date.toGMTString();
  }
  document.cookie = name+&quot;=&quot;+value+expires+&quot;; path=/&quot;;
}
&lt;/script&gt;</code></pre>

You can check that [https://localhost:3000](https://localhost:3000) contains the cookie named `fastweb`. The `fastjs` content should be inserted only if a cookie doesn’t exist. To determine this, we need to check on the Express side whether one exists. This is easily done with the `cookie-parser` npm package and Express. Go to this bit of code in `server.js`:

<pre><code class="language-javascript">app.get('/', function(req, res){
  res.status(200).render('content');
});</code></pre>

The `render` function accepts in the second position an optional object containing local variables for the view. We can pass a variable into the view like so:

<pre><code class="language-javascript">app.get('/', function(req, res){
  res.status(200).render('content', {needToRenderFast: true});
});</code></pre>

Now, in our view, we can print the variable `needToRenderFast`, whose value will be `true`. We want the value of this variable to be set to `true` if a cookie named `fastweb` does not exist. Otherwise, the variable should be set to `false`. Using `cookie-parser`, checking for the cookie’s existence is possible with this simple code:

<pre><code class="language-javascript">//Check whether cookie named fastweb is set to a value of 'cache'
req.cookies.fastweb === 'cache'</code></pre>

And here it is rewritten for our needs:

<pre><code class="language-javascript">app.get('/', function(req, res){
  res.status(200).render('content', {
    needToRenderFast: !(req.cookies.fastweb === 'cache')
  });
});</code></pre>

The view knows, based on value of this variable, whether to render the critical files. Thanks to Handlebars’ built-in helpers — namely, the `if block` helper — this is also easy to implement. Open the layout file and add an `if` helper:

<pre><code class="language-markup">&lt;head&gt;
…
{{#if needToRenderFast}}
{{&gt; fastjs}}
{{/if}}
&lt;/head&gt;</code></pre>

Voilà! The `fastjs` content gets inserted only if a cookie doesn’t exist.</p>

## Injecting Critical CSS

The critical CSS file must be inserted at the same time as the critical JavaScript file. First, create another partial named `/views/partials/fastcss.handlebars`. The contents of this `fastcss` file is simple:

<pre><code class="language-markup">&lt;style id=&quot;fastcss&quot;&gt;
  body{background:#E91E63;}
&lt;/style&gt;</code></pre>

Just import it as we did the `fastjs` partial. Open the layout file:

<pre><code class="language-markup">&lt;head&gt;
…
{{#if needToRenderFast}}
{{&gt; fastcss}}
{{&gt; fastjs}}
{{/if}}
&lt;/head&gt;</code></pre>

## Handling The Loading Of The CSS Bundle

The trouble now is that, even though the CSS bundle has loaded, the critical partials still remain in the DOM. Fortunately, this is easy to fix. Our layout’s markup looks like this:

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;en&quot;&gt;
  &lt;head&gt;
    &lt;meta charset=&quot;UTF-8&quot;&gt;
    &lt;title&gt;Critical-Path Performance Optimization&lt;/title&gt;
    {{#if needToRenderFast}}
    &lt;link rel=&quot;stylesheet&quot; href=&quot;assets/css/bundle.css&quot; id=&quot;cssbundle&quot; media=&quot;none&quot;/&gt;
    {{&gt; fastcss}}
    {{&gt; fastjs}}
    {{/if}}
  &lt;/head&gt;
  &lt;body&gt;
  &lt;/body&gt;
&lt;/html&gt;</code></pre>

Our `fastjs`, `fastcss` and CSS bundle have their own IDs. We can take advantage of that. Open the `fastjs` partial and find the references to those elements.</p>

<pre><code class="language-javascript">var cssBundle = document.getElementById('cssbundle'),
fastCss = document.getElementById('fastcss'),
fastJs = document.getElementById('fastjs');</code></pre>

We want to be notified when the CSS bundle has loaded. This is possible using an event listener:

<pre><code class="language-javascript">cssBundle.addEventListener('load', handleFastcss);</code></pre>

The `handleFastcss` function will be called immediately after the CSS bundle has loaded. At that moment, we want to propagate styles from the CSS bundle, remove the `#fastjs` and `#fastcss` elements and create the cookie. As mentioned at the beginning of this article, the styles from the CSS bundle will be propagated by changing the `media` attribute of the CSS bundle to a valid value — in our case, a value of `all`.</p>

<pre><code class="language-javascript">function handleFastcss() {
  cssBundle.setAttribute('media', 'all');
}</code></pre>

Now, just remove the `#fastjs` and `#fastcss` elements:

<pre><code class="language-javascript">function handleFastcss() {
  cssBundle.setAttribute('media', 'all');
  fastCss.parentNode.removeChild(fastCss);
  fastJs.parentNode.removeChild(fastJs);
}</code></pre>

And call the <code>createCookie</code> function inside the <code>handleFastcss</code> function.</p>

<pre><code class="language-javascript">function handleFastcss() {
  createCookie('fastweb', 'cache', 1);
  cssBundle.setAttribute('media', 'all');
  fastCss.parentNode.removeChild(fastCss);
  fastJs.parentNode.removeChild(fastJs);
}</code></pre>

Our final `fastjs` script is as follows:

<pre><code class="language-markup">&lt;script id='fastjs'&gt;
var cssBundle = document.getElementById('cssbundle'),
fastCss =  document.getElementById('fastcss'),
fastJs =  document.getElementById('fastjs');

cssBundle.addEventListener('load', handleFastcss);

function handleFastcss() {
  createCookie('fastweb', 'cache', 1);
  cssBundle.setAttribute('media', 'all');
  fastCss.parentNode.removeChild(fastCss);
  fastJs.parentNode.removeChild(fastJs);
}
function createCookie(name,value,days) {
  var expires = &quot;&quot;;
  if (days) {
    var date = new Date();
    date.setTime(date.getTime()+(days*24*60*60*1000));
    var expires = &quot;; expires=&quot;+date.toGMTString();
  }
  document.cookie = name+&quot;=&quot;+value+expires+&quot;; path=/&quot;;
}
&lt;/script&gt;</code></pre>

Please note that this CSS load handler works only on the client side. If client-side JavaScript is disabled, it will continue using the styles in `fastcss`.</p>

## Handling The Second And Nth Load

The first load now behaves as expected. But when we reload the page in the browser, it remains without styles. That’s because we’ve only dealt with the scenario in which a cookie doesn’t exist. If a cookie does exist, the CSS bundle must be linked in the standard way.

Edit the layout file:

<pre><code class="language-markup">&lt;head&gt;
  …
  {{#if needToRenderFast}}
  &lt;link rel=&quot;stylesheet&quot; href=&quot;assets/css/bundle.css&quot; id=&quot;cssbundle&quot; media=&quot;none&quot;/&gt;
  {{&gt; fastcss}}
  {{&gt; fastjs}}
  {{else}}
  &lt;link rel=&quot;stylesheet&quot; href=&quot;assets/css/bundle.css&quot; id=&quot;cssbundle&quot; media=&quot;all&quot;/&gt;
  {{/if}}
&lt;/head&gt;</code></pre>

Save it, and view the result.</p>

## Result

The GIF below shows the first load. As you can see, while the CSS bundle is downloading, the page has a different background. This is caused by the styles in the `fastcss` partial. The cookie is created, and the `bundle.css` request ends with a status of “[200 OK](https://httpstatuses.com/200).”

<figure><div class="aspect-ratio">{{< vimeo 173274439 >}}</div><figcaption>Critical-path performance optimization: first load</figcaption></figure>

As you will recall, our first objective is to determine whether or not a load is the first. Based on this, we can decide whether to serve critical styles or the CSS bundle from the browser’s cache. We will use a cookie for this. If a cookie is set, then that means it’s not the first load; otherwise, it is. The cookie will be created in the critical JavaScript file, which will be injected inline in the template with the critical styles. Checking for the cookie will be handled by Express.

Let’s name the critical JavaScript file `fastjs`. We must be able to insert the content of `fastjs` in the layout file if a cookie doesn’t exist. I’ve found Handlebars partials to be pretty easy to use. Partials are useful when you have markup that you want to reuse in multiple places. They can be called by other templates and are mostly used for the header, footer, navigation and so on.

In the Handlebars section, I’ve defined a partials directory at `/views/partials`. Let’s create a `/views/partials/fastjs.handlebars` file. In this file, we’ll add a script tag with an ID of `fastjs`. We will use this ID later to remove the script from the DOM.</p>

<pre><code class="language-markup">&lt;script id='fastjs'&gt;
&lt;/script&gt;</code></pre>

Now, open `/views/layouts/main.handlebars`. Calling the partial is done through the syntax `{{> partialName }}`. This code will be replaced by the contents of our target partial. Our partial is named `fastjs`, so add the following line before the end of the `head` tag:

<pre><code class="language-markup">&lt;head&gt;
…
{{&gt; fastjs}}
&lt;/head&gt;</code></pre>

The markup at [https://localhost:3000](https://localhost:3000) now contains the contents of the `fastjs` partial. A cookie will be created using this simple JavaScript function.</p>

<pre><code class="language-markup">&lt;script id='fastjs'&gt;
// Let's create a cookie named 'fastweb', setting its value to 'cache' and its expiration to one day
createCookie('fastweb', 'cache', 1);

// function to create cookie
function createCookie(name,value,days) {
  var expires = &quot;&quot;;
  if (days) {
    var date = new Date();
    date.setTime(date.getTime()+(days*24*60*60*1000));
    var expires = &quot;; expires=&quot;+date.toGMTString();
  }
  document.cookie = name+&quot;=&quot;+value+expires+&quot;; path=/&quot;;
}
&lt;/script&gt;</code></pre>

You can check that [https://localhost:3000](https://localhost:3000) contains the cookie named `fastweb`. The `fastjs` content should be inserted only if a cookie doesn’t exist. To determine this, we need to check on the Express side whether one exists. This is easily done with the `cookie-parser` npm package and Express. Go to this bit of code in `server.js`:

<pre><code class="language-javascript">app.get('/', function(req, res){
  res.status(200).render('content');
});</code></pre>

The `render` function accepts in the second position an optional object containing local variables for the view. We can pass a variable into the view like so:

<pre><code class="language-javascript">app.get('/', function(req, res){
  res.status(200).render('content', {needToRenderFast: true});
});</code></pre>

Now, in our view, we can print the variable `needToRenderFast`, whose value will be `true`. We want the value of this variable to be set to `true` if a cookie named `fastweb` does not exist. Otherwise, the variable should be set to `false`. Using `cookie-parser`, checking for the cookie’s existence is possible with this simple code:

<pre><code class="language-javascript">//Check whether cookie named fastweb is set to a value of 'cache'
req.cookies.fastweb === 'cache'</code></pre>

And here it is rewritten for our needs:

<pre><code class="language-javascript">app.get('/', function(req, res){
  res.status(200).render('content', {
    needToRenderFast: !(req.cookies.fastweb === 'cache')
  });
});</code></pre>

The view knows, based on value of this variable, whether to render the critical files. Thanks to Handlebars’ built-in helpers — namely, the `if block` helper — this is also easy to implement. Open the layout file and add an `if` helper:

<pre><code class="language-markup">&lt;head&gt;
…
{{#if needToRenderFast}}
{{&gt; fastjs}}
{{/if}}
&lt;/head&gt;</code></pre>

Voilà! The `fastjs` content gets inserted only if a cookie doesn’t exist.</p>

## Injecting Critical CSS

The critical CSS file must be inserted at the same time as the critical JavaScript file. First, create another partial named `/views/partials/fastcss.handlebars`. The contents of this `fastcss` file is simple:

<pre><code class="language-markup">&lt;style id=&quot;fastcss&quot;&gt;
  body{background:#E91E63;}
&lt;/style&gt;</code></pre>

Just import it as we did the `fastjs` partial. Open the layout file:

<pre><code class="language-markup">&lt;head&gt;
…
{{#if needToRenderFast}}
{{&gt; fastcss}}
{{&gt; fastjs}}
{{/if}}
&lt;/head&gt;</code></pre>

## Handling The Loading Of The CSS Bundle

The trouble now is that, even though the CSS bundle has loaded, the critical partials still remain in the DOM. Fortunately, this is easy to fix. Our layout’s markup looks like this:

<pre><code class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;en&quot;&gt;
  &lt;head&gt;
    &lt;meta charset=&quot;UTF-8&quot;&gt;
    &lt;title&gt;Critical-Path Performance Optimization&lt;/title&gt;
    {{#if needToRenderFast}}
    &lt;link rel=&quot;stylesheet&quot; href=&quot;assets/css/bundle.css&quot; id=&quot;cssbundle&quot; media=&quot;none&quot;/&gt;
    {{&gt; fastcss}}
    {{&gt; fastjs}}
    {{/if}}
  &lt;/head&gt;
  &lt;body&gt;
  &lt;/body&gt;
&lt;/html&gt;</code></pre>

Our `fastjs`, `fastcss` and CSS bundle have their own IDs. We can take advantage of that. Open the `fastjs` partial and find the references to those elements.</p>

<pre><code class="language-javascript">var cssBundle = document.getElementById('cssbundle'),
fastCss = document.getElementById('fastcss'),
fastJs = document.getElementById('fastjs');</code></pre>

We want to be notified when the CSS bundle has loaded. This is possible using an event listener:

<pre><code class="language-javascript">cssBundle.addEventListener('load', handleFastcss);</code></pre>

The `handleFastcss` function will be called immediately after the CSS bundle has loaded. At that moment, we want to propagate styles from the CSS bundle, remove the `#fastjs` and `#fastcss` elements and create the cookie. As mentioned at the beginning of this article, the styles from the CSS bundle will be propagated by changing the `media` attribute of the CSS bundle to a valid value — in our case, a value of `all`.</p>

<pre><code class="language-javascript">function handleFastcss() {
  cssBundle.setAttribute('media', 'all');
}</code></pre>

Now, just remove the `#fastjs` and `#fastcss` elements:

<pre><code class="language-javascript">function handleFastcss() {
  cssBundle.setAttribute('media', 'all');
  fastCss.parentNode.removeChild(fastCss);
  fastJs.parentNode.removeChild(fastJs);
}</code></pre>

And call the <code>createCookie</code> function inside the <code>handleFastcss</code> function.</p>

<pre><code class="language-javascript">function handleFastcss() {
  createCookie('fastweb', 'cache', 1);
  cssBundle.setAttribute('media', 'all');
  fastCss.parentNode.removeChild(fastCss);
  fastJs.parentNode.removeChild(fastJs);
}</code></pre>

Our final `fastjs` script is as follows:

<pre><code class="language-markup">&lt;script id='fastjs'&gt;
var cssBundle = document.getElementById('cssbundle'),
fastCss =  document.getElementById('fastcss'),
fastJs =  document.getElementById('fastjs');

cssBundle.addEventListener('load', handleFastcss);

function handleFastcss() {
  createCookie('fastweb', 'cache', 1);
  cssBundle.setAttribute('media', 'all');
  fastCss.parentNode.removeChild(fastCss);
  fastJs.parentNode.removeChild(fastJs);
}
function createCookie(name,value,days) {
  var expires = &quot;&quot;;
  if (days) {
    var date = new Date();
    date.setTime(date.getTime()+(days*24*60*60*1000));
    var expires = &quot;; expires=&quot;+date.toGMTString();
  }
  document.cookie = name+&quot;=&quot;+value+expires+&quot;; path=/&quot;;
}
&lt;/script&gt;</code></pre>

Please note that this CSS load handler works only on the client side. If client-side JavaScript is disabled, it will continue using the styles in `fastcss`.</p>

## Handling The Second And Nth Load

The first load now behaves as expected. But when we reload the page in the browser, it remains without styles. That’s because we’ve only dealt with the scenario in which a cookie doesn’t exist. If a cookie does exist, the CSS bundle must be linked in the standard way.

Edit the layout file:

<pre><code class="language-markup">&lt;head&gt;
  …
  {{#if needToRenderFast}}
  &lt;link rel=&quot;stylesheet&quot; href=&quot;assets/css/bundle.css&quot; id=&quot;cssbundle&quot; media=&quot;none&quot;/&gt;
  {{&gt; fastcss}}
  {{&gt; fastjs}}
  {{else}}
  &lt;link rel=&quot;stylesheet&quot; href=&quot;assets/css/bundle.css&quot; id=&quot;cssbundle&quot; media=&quot;all&quot;/&gt;
  {{/if}}
&lt;/head&gt;</code></pre>

Save it, and view the result.</p>

## Result

The GIF below shows the first load. As you can see, while the CSS bundle is downloading, the page has a different background. This is caused by the styles in the `fastcss` partial. The cookie is created, and the `bundle.css` request ends with a status of “[200 OK](https://httpstatuses.com/200).”

<figure><div class="aspect-ratio">{{< vimeo 173274439 >}}</div><figcaption>Critical-path performance optimization: first load</figcaption></figure>

The second GIF shows the reloading scenario. A cookie has already been created, the critical files are ignored, and the `bundle.css` request ends with a status of “[304 Not modified](https://httpstatuses.com/304).”

<figure><div class="aspect-ratio">{{< vimeo 173274440 >}}</div><figcaption>Critical-path performance optimization: second and nth load</figcaption></figure>

## Conclusion

We’ve gone through the whole lifecycle shown in the schema above. As a next step, check that all requests to scripts, images, fonts and so on are asynchronous and do not block rendering. Also, don’t forget to enable gZip compression on the server; nice Express [middleware](https://github.com/expressjs/compression) is available for this.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd91a16d-e098-4466-9407-5dff5fa5baf6/02-criticalcss-graph-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e05632bd-7eec-40f1-925c-8f504b5076ad/02-criticalcss-graph-preview-opt.png" alt="Lifecycle of critical-path performance optimization" width="500" height="262" /></a><figcaption>Lifecycle of critical-path performance optimization (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd91a16d-e098-4466-9407-5dff5fa5baf6/02-criticalcss-graph-opt.png">View large version</a>)</figcaption></figure>

### Recommended Reading

*   “[React to the Future With Isomorphic Apps](https://www.smashingmagazine.com/2015/04/react-to-the-future-with-isomorphic-apps/),” Jonathan Creamer
*   “[Understanding Critical CSS](https://www.smashingmagazine.com/2015/08/understanding-critical-css/),” Dean Hume
*   “[Website Performance Optimization](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/?hl=en),” Ilya Grigorik
*   “[Browser Progress Bar Is an Anti-Pattern](https://www.igvita.com/2015/06/25/browser-progress-bar-is-an-anti-pattern/),” Ilya Grigorik

{{< signature "rb, ml, mh, vf, al, il" >}}


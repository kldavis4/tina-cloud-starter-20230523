---
title: 'Create A Bookmarking Application With FaunaDB, Netlify And 11ty'
slug: bookmarking-application-faunadb-netlify-11ty
author: bryan-robinson
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8eb076b0-5f36-4a11-82b3-677a31bff272/bookmarking-application-faunadb-netlify-11ty-app-running.jpg
date: 2019-10-24T13:30:59+02:00
summary: >-
  In this article, we’ll create a personal bookmarking site using FaunaDB, Netlify Functions and 11ty data files.
description: >-
  In this article, we’ll create a personal bookmarking site using FaunaDB, Netlify Functions and 11ty data files.
categories:
  - JavaScript
  - Apps
  - Eleventy
---
The JAMstack (JavaScript, APIs and Markup) revolution is in full swing. Static sites are secure, fast, reliable and fun to work on. At the heart of the JAMstack are static site generators (SSGs) that store your data as flat files: Markdown, YAML, JSON, HTML, and so on. Sometimes, managing data this way can be overly complicated. Sometimes, we still need a database.

With that in mind, Netlify &mdash; a static site host and FaunaDB &mdash; a serverless cloud database &mdash; collaborated to make combining both systems easier. 

## Why A Bookmarking Site?

The JAMstack is great for many professional uses, but one of my favorite aspects of this set of technology is its low barrier to entry for personal tools and projects.

There are plenty of good products on the market for most applications I could come up with, but none would be exactly set up for me. None would give me full control over my content. None would come without a cost (monetary or informational).

With that in mind, we can create our own mini-services using JAMstack methods. In this case, we’ll be creating a site to store and publish any interesting articles I come across in my daily technology reading.

I spend a lot of time reading articles that have been shared on Twitter. When I like one, I hit the "heart" icon. Then, within a few days, it’s nearly impossible to find with the influx of new favorites. I want to build something as close to the ease of the "heart," but that I own and control.

How are we going to do that? I’m glad you asked.

<blockquote>Interested in getting the code? You can <a href="https://github.com/brob/netlify-fauna-bookmarks">grab it on Github</a> or just deploy straight to Netlify from that repository! Take a look at the <a href="https://fauna-bookmarks.netlify.com">finished product here</a>.</blockquote>

## Our Technologies

### Hosting And Serverless Functions: Netlify

For hosting and serverless functions, we’ll be utilizing Netlify. As an added bonus, with the new collaboration mentioned above, Netlify’s CLI &mdash; "Netlify Dev" &mdash; will automatically connect to FaunaDB and store our API keys as environment variables.

### Database: FaunaDB

FaunaDB is a "serverless" NoSQL database. We’ll be using it to store our bookmarks data.

### Static Site Generator: 11ty

I’m a big believer in HTML. Because of this, the tutorial won’t be using front-end JavaScript to render our bookmarks. Instead, we’ll utilize 11ty as a static site generator. 11ty has built-in data functionality that makes fetching data from an API as easy as writing a couple of short JavaScript functions.

### iOS Shortcuts

We’ll need an easy way to post data to our database. In this case, we’ll use iOS’s Shortcuts app. This could be converted to an Android or desktop JavaScript bookmarklet, as well.

{{% feature-panel %}}

## Setting Up FaunaDB Via Netlify Dev

Whether you have already signed up for FaunaDB or you need to create a new account, the easiest way to set up a link between FaunaDB and Netlify is via Netlify’s CLI: Netlify Dev. You can find full instructions [from FaunaDB here](https://docs.fauna.com/fauna/current/start/netlify) or follow along below.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/167ab831-afbf-4c2e-9242-db2547709b3d/bookmarking-application-faunadb-netlify-11ty-netlify-dev-screenshot.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/167ab831-afbf-4c2e-9242-db2547709b3d/bookmarking-application-faunadb-netlify-11ty-netlify-dev-screenshot.jpg" sizes="100vw" caption="Netlify Dev running in the final project with our environment variable names showing (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/167ab831-afbf-4c2e-9242-db2547709b3d/bookmarking-application-faunadb-netlify-11ty-netlify-dev-screenshot.jpg'>Large preview</a>)" alt="Netlify Dev running in the final project with our environment variable names showing" >}}

If you don’t already have this installed, you can run the following command in Terminal:

<pre><code class="language-bash">npm install netlify-cli -g</code></pre>

From within your project directory, run through the following commands:

<div class="break-out">

<pre><code class="language-bash">netlify init // This will connect your project to a Netlify project

netlify addons:create fauna // This will install the FaunaDB "addon"

netlify addons:auth fauna // This command will run you through connecting your account or setting up an account
</code></pre>
</div>

Once this is all connected, you can run `netlify dev` in your project. This will run any build scripts we set up, but also connect to the Netlify and FaunaDB services and grab any necessary environment variables. Handy!

### Creating Our First Data

From here, we’ll log into FaunaDB and create our first data set. We’ll start by creating a new Database called "bookmarks." Inside a Database, we have Collections, Documents and Indexes.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec14f2d9-0fa8-4245-bfaf-fed66229a540/bookmarking-application-faunadb-netlify-11ty-fauna-console-with-links.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec14f2d9-0fa8-4245-bfaf-fed66229a540/bookmarking-application-faunadb-netlify-11ty-fauna-console-with-links.jpg" sizes="100vw" caption="A screenshot of the FaunaDB console with data (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec14f2d9-0fa8-4245-bfaf-fed66229a540/bookmarking-application-faunadb-netlify-11ty-fauna-console-with-links.jpg'>Large preview</a>)" alt="A screenshot of the FaunaDB console with data" >}}

A Collection is a categorized group of data. Each piece of data takes the form of a Document. A Document is a "single, changeable record within a FaunaDB database," according to Fauna’s documentation. You can think of Collections as a traditional database table and a Document as a row.

For our application, we need one Collection, which we’ll call "links." Each document within the "links" Collection will be a simple JSON object with three properties. To start, we’ll add a new Document that we’ll use to build our first data fetch.

<div class="break-out">

<pre><code class="language-javascript">{
  "url": "https://css-irl.info/debugging-css-grid-part-2-what-the-fraction/",
  "pageTitle": "CSS { In Real Life } | Debugging CSS Grid – Part 2: What the Fr(action)?",
  "description": "CSS In Real Life is a blog covering CSS topics and useful snippets on the web’s most beautiful language. Published by Michelle Barker, front end developer at Ordoo and CSS superfan."
}</code></pre>
</div>

This creates the basis for the information we’ll need to pull from our bookmarks as well as provides us with our first set of data to pull into our template.

If you’re like me, you want to see the fruits of your labor right away. Let’s get something on the page!

## Installing 11ty And Pulling Data Into A Template

Since we want the bookmarks to be rendered in HTML and not fetched by the browser, we’ll need something to do the rendering. There are many great ways of doing it, but for ease and power, I love using the 11ty static site generator.

Since 11ty is a JavaScript static site generator, we can install it via NPM.

<pre><code class="language-bash">npm install --save @11ty/eleventy</code></pre>

From that installation, we can run `eleventy` or `eleventy --serve` in our project to get up and running.

Netlify Dev will often detect 11ty as a requirement and run the command for us. To have this work - and make sure we’re ready to deploy, we can also create "serve" and "build" commands in our `package.json`.

<pre><code class="language-javascript">"scripts": {
    "build": "npx eleventy",
    "serve": "npx eleventy --serve"
  }</code></pre>

### 11ty’s Data Files

Most static site generators have an idea of a "data file" built-in. Usually, these files will be JSON or YAML files that allow you to add extra information to your site.

In 11ty, you can use JSON data files or JavaScript data files. By utilizing a JavaScript file, we can actually make our API calls and return the data directly into a template.

<p class="c-pre-sidenote--left">By default, 11ty wants data files stored in a <code>&#95;data</code> directory. You can then access the data by using the file name as a variable in your templates. In our case, we’ll create a file at <code>&#95;data/bookmarks.js</code> and access that via the <code>{{ bookmarks }}</code> variable name.</p><p class="c-sidenote c-sidenote--right">If you want to dig deeper into data file configuration, you can read through examples in the <a href="https://www.11ty.io/docs/data/">11ty documentation</a> or check out this tutorial on <a href="https://bryanlrobinson.com/blog/using-eleventys-javascript-data-files/">using 11ty data files with the Meetup API</a>.</p>

The file will be a JavaScript module. So in order to have anything work, we need to export either our data or a function. In our case, we’ll export a function.

<pre><code class="language-javascript">module.exports = async function() {
    const data = mapBookmarks(await getBookmarks());

    return data.reverse()
}</code></pre>

Let’s break that down. We have two functions doing our main work here: `mapBookmarks()` and `getBookmarks()`. 

The `getBookmarks()` function will go fetch our data from our FaunaDB database and `mapBookmarks()` will take an array of bookmarks and restructure it to work better for our template.

Let’s dig deeper into `getBookmarks()`.

### `getBookmarks()`

First, we’ll need to install and initialize an instance of the FaunaDB JavaScript driver.

<pre><code class="language-bash">npm install --save faunadb</code></pre>

Now that we’ve installed it, let’s add it to the top of our data file. This code is [straight from Fauna’s docs](https://docs.fauna.com/fauna/current/drivers/javascript#requiring-the-driver).

<div class="break-out">

<pre><code class="language-javascript">// Requires the Fauna module and sets up the query module, which we can use to create custom queries.
const faunadb = require('faunadb'),
      q = faunadb.query;

// Once required, we need a new instance with our secret
var adminClient = new faunadb.Client({
   secret: process.env.FAUNADB_SERVER_SECRET
});
</code></pre>
</div>

<p class="c-pre-sidenote--left">After that, we can create our function. We’ll start by building our first query using built-in methods on the driver. This first bit of code will return the database references we can use to get full data for all of our bookmarked links. We use the <code>Paginate</code> method, as a helper to manage cursor state should we decide to paginate the data before handing it to 11ty. In our case, we’ll just return all the references.</p>

<p class="c-sidenote c-sidenote--right">In this example, I’m assuming you installed and connected FaunaDB via the Netlify Dev CLI. Using this process, you get local environment variables of the FaunaDB secrets. If you didn’t install it this way or aren’t running <code>netlify dev</code> in your project, you’ll need a package like <code>dotenv</code> to create the environment variables. You’ll also need to add your environment variables to your Netlify site configuration to make deploys work later.</p>

<div class="break-out">

<pre><code class="language-javascript">adminClient.query(q.Paginate(
       q.Match( // Match the reference below
           q.Ref("indexes/all_links") // Reference to match, in this case, our all_links index
       )
   ))
   .then( response => { ... })</code></pre>
</div>

This code will return an array of all of our links in reference form. We can now build a query list to send to our database.

<div class="break-out">

<pre><code class="language-javascript">adminClient.query(...)
    .then((response) => {
        const linkRefs = response.data; // Get just the references for the links from the response
        const getAllLinksDataQuery = linkRefs.map((ref) => {
        return q.Get(ref) // Return a Get query based on the reference passed in
   })

return adminClient.query(getAllLinksDataQuery).then(ret => {
    return ret // Return an array of all the links with full data
       })
   }).catch(...)</code></pre>
</div>

From here, we just need to clean up the data returned. That’s where `mapBookmarks()` comes in!

### `mapBookmarks()`

In this function, we deal with two aspects of the data.

First, we get a free dateTime in FaunaDB. For any data created, there’s a timestamp (`ts`) property. It’s not formatted in a way that makes Liquid’s default date filter happy, so let’s fix that.

<pre><code class="language-javascript">function mapBookmarks(data) {
    return data.map(bookmark => {
        const dateTime = new Date(bookmark.ts / 1000);
        ...
    })
}</code></pre>

With that out of the way, we can build a new object for our data. In this case, it will have a `time` property, and we’ll use the Spread operator to destructure our `data` object to make them all live at one level.

<pre><code class="language-javascript">function mapBookmarks(data) {
    return data.map(bookmark => {
        const dateTime = new Date(bookmark.ts / 1000);

        return { time: dateTime, ...bookmark.data }
    })
}</code></pre>

Here’s our data before our function:

<pre><code class="language-javascript">{
  ref: Ref(Collection("links"), "244778237839802888"),
  ts: 1569697568650000,

  data: {
    url: 'https://sample.com',
    pageTitle: 'Sample title',
    description: 'An escaped description goes here'
  }
}
</code></pre>

Here’s our data after our function:

<pre><code class="language-javascript">{
    time: 1569697568650,
    url: 'https://sample.com',
    pageTitle: 'Sample title'
    description: 'An escaped description goes here'
}
</code></pre>

Now, we’ve got well-formatted data that’s ready for our template!

Let’s write a simple template. We’ll loop through our bookmarks and validate that each has a `pageTitle` and a `url` so we don’t look silly.

<div class="break-out">

<pre><code class="language-html">&lt;div class="bookmarks"&gt;
   {% for link in bookmarks %}
       {% if link.url and link.pageTitle %} // confirms there’s both title AND url for safety

        &lt;div class="bookmark"&gt;
            &lt;h2&gt;&lt;a href="{{ link.url }}"&gt;{{ link.pageTitle }}&lt;/a&gt;&lt;/h2&gt;
            &lt;p&gt;Saved on {{ link.time | date: "%b %d, %Y"  }}&lt;/p&gt;
            {% if link.description != "" %}
                &lt;p&gt;{{ link.description }}&lt;/p&gt;
            {% endif %}
        &lt;/div&gt;

       {% endif %}
   {% endfor %}
&lt;/div&gt;
</code></pre>
</div>

We’re now ingesting and displaying data from FaunaDB. Let’s take a moment and think about how nice it is that this renders out pure HTML and there’s no need to fetch data on the client side!

But that’s not really enough to make this a useful app for us. Let’s figure out a better way than adding a bookmark in the FaunaDB console.

{{% ad-panel-leaderboard %}}

## Enter Netlify Functions

Netlify’s Functions add-on is one of the easier ways to deploy AWS lambda functions. Since there’s no configuration step, it’s perfect for DIY projects where you just want to write the code.

This function will live at a URL in your project that looks like this: `https://myproject.com/.netlify/functions/bookmarks` assuming the file we create in our functions folder is `bookmarks.js`.

### Basic Flow

1. Pass a URL as a query parameter to our function URL.
2. Use the function to load the URL and scrape the page’s title and description if available.
3. Format the details for FaunaDB.
4. Push the details to our FaunaDB Collection.
5. Rebuild the site.

### Requirements

We’ve got a few packages we’ll need as we build this out. We’ll use the netlify-lambda CLI to build our functions locally. `request-promise` is the package we’ll use for making requests. Cheerio.js is the package we’ll use to scrape specific items from our requested page (think jQuery for Node). And finally, we’ll need FaunaDb (which should already be installed.

<pre><code class="language-bash">npm install --save netlify-lambda request-promise cheerio</code></pre>

Once that’s installed, let’s configure our project to build and serve the functions locally.

We’ll modify our "build" and "serve" scripts in our `package.json` to look like this:

<div class="break-out">

<pre><code class="language-javascript">"scripts": {
    "build": "npx netlify-lambda build lambda --config ./webpack.functions.js && npx eleventy",
    "serve": "npx netlify-lambda build lambda --config ./webpack.functions.js && npx eleventy --serve"
}
</code></pre>
</div>

**Warning:** *There’s an error with Fauna’s NodeJS driver when compiling with Webpack, which Netlify’s Functions use to build. To [get around this](https://github.com/netlify/netlify-faunadb-example/issues/8), we need to define a configuration file for Webpack. You can save the following code to a new* &mdash; *or existing* &mdash; `webpack.config.js`.

<pre><code class="language-javascript">const webpack = require('webpack');

module.exports = {
  plugins: [ new webpack.DefinePlugin({ "global.GENTLY": false }) ]
};</code></pre>

Once this file exists, when we use the `netlify-lambda` command, we’ll need to tell it to run from this configuration. This is why our "serve" and "build scripts use the `--config` value for that command.

### Function Housekeeping

In order to keep our main Function file as clean as possible, we’ll create our functions in a separate `bookmarks` directory and import them into our main Function file.

<pre><code class="language-javascript">import { getDetails, saveBookmark } from "./bookmarks/create";</code></pre>

### `getDetails(url)`

The `getDetails()` function will take a URL, passed in from our exported handler. From there, we’ll reach out to the site at that URL and grab relevant parts of the page to store as data for our bookmark.

We start by requiring the NPM packages we need:

<pre><code class="language-javascript">const rp = require('request-promise');
const cheerio = require('cheerio');</code></pre>

Then, we’ll use the `request-promise` module to return an HTML string for the requested page and pass that into `cheerio` to give us a very jQuery-esque interface.

<pre><code class="language-javascript">const getDetails = async function(url) {
    const data = rp(url).then(function(htmlString) {
        const $ = cheerio.load(htmlString);
        ...
}</code></pre>

From here, we need to get the page title and a meta description. To do that, we’ll use selectors like you would in jQuery. 

**Note:** *In this code, we use* `'head > title'` *as the selector to get the title of the page. If you don’t specify this, you may end up getting* `<title>` *tags inside of all SVGs on the page, which is less than ideal.*

<div class="break-out">

<pre><code class="language-javascript">const getDetails = async function(url) {
  const data = rp(url).then(function(htmlString) {
    const $ = cheerio.load(htmlString);
    const title = $('head > title').text(); // Get the text inside the tag
    const description = $('meta[name="description"]').attr('content'); // Get the text of the content attribute

// Return out the data in the structure we expect
    return {
      pageTitle: title,
      description: description
    };
  });
  return data //return to our main function
}</code></pre>
</div>

With data in hand, it’s time to send our bookmark off to our Collection in FaunaDB!

### `saveBookmark(details)`

For our save function, we’ll want to pass the details we acquired from `getDetails` as well as the URL as a singular object. The Spread operator strikes again!

<pre><code class="language-javascript">const savedResponse = await saveBookmark({url, ...details});</code></pre>

In our `create.js` file, we also need to require and setup our FaunaDB driver. This should look very familiar from our 11ty data file.

<pre><code class="language-javascript">const faunadb = require('faunadb'),
      q = faunadb.query;

const adminClient = new faunadb.Client({
   secret: process.env.FAUNADB_SERVER_SECRET
});
</code></pre>

Once we’ve got that out of the way, we can code.

{{% ad-panel-leaderboard %}}

First, we need to format our details into a data structure that Fauna is expecting for our query. Fauna expects an object with a data property containing the data we wish to store.

<pre><code class="language-javascript">const saveBookmark = async function(details) {
const data = {
   data: details
};

...

}</code></pre>

Then we’ll open a new query to add to our Collection. In this case, we’ll use our query helper and use the Create method. Create() takes two arguments. First is the Collection in which we want to store our data and the second is the data itself.

After we save, we return either success or failure to our handler.

<div class="break-out">

 <pre><code class="language-javascript">const saveBookmark = async function(details) {
const data = {
   data: details
};

return adminClient.query(q.Create(q.Collection("links"), data))
   .then((response) => {
        /&#42; Success! return the response with statusCode 200 &#42;/
        return {
             statusCode: 200,
             body: JSON.stringify(response)
         }
     }).catch((error) => {
        /&#42; Error! return the error with statusCode 400 &#42;/
        return  {
             statusCode: 400,
             body: JSON.stringify(error)
         }
     })
}</code></pre>
</div>

Let’s take a look at the full Function file.

<div class="break-out">

<pre><code class="language-javascript">import { getDetails, saveBookmark } from "./bookmarks/create";
import { rebuildSite } from "./utilities/rebuild"; // For rebuilding the site (more on that in a minute)

exports.handler = async function(event, context) {
    try {
        const url = event.queryStringParameters.url; // Grab the URL

        const details = await getDetails(url); // Get the details of the page
        const savedResponse = await saveBookmark({url, ...details}); //Save the URL and the details to Fauna

        if (savedResponse.statusCode === 200) {
            // If successful, return success and trigger a Netlify build
            await rebuildSite();
            return { statusCode: 200, body: savedResponse.body }
         } else {
            return savedResponse //or else return the error
         }
     } catch (err) {
        return { statusCode: 500, body: `Error: ${err}` };
     }
};
</code></pre>
</div>

### `rebuildSite()`

The discerning eye will notice that we have one more function imported into our handler: `rebuildSite()`. This function will use Netlify’s Deploy Hook functionality to rebuild our site from the new data every time we submit a new &mdash; successful &mdash; bookmark save.

In your site’s settings in Netlify, you can access your Build & Deploy settings and create a new "Build Hook." Hooks have a name that appears in the Deploy section and an option for a non-master branch to deploy if you so wish. In our case, we’ll name it "new_link" and deploy our master branch.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58bf7a4f-3248-4227-bb3c-0c2a6ed96d69/bookmarking-application-faunadb-netlify-11ty-netlify-build-hook.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58bf7a4f-3248-4227-bb3c-0c2a6ed96d69/bookmarking-application-faunadb-netlify-11ty-netlify-build-hook.png" sizes="100vw" caption="A visual reference for the Netlify Admin’s build hook setup (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/58bf7a4f-3248-4227-bb3c-0c2a6ed96d69/bookmarking-application-faunadb-netlify-11ty-netlify-build-hook.png'>Large preview</a>)" alt="A visual reference for the Netlify Admin’s build hook setup" >}}

From there, we just need to send a POST request to the URL provided.

We need a way of making requests and since we’ve already installed `request-promise`, we’ll continue to use that package by requiring it at the top of our file.

<div class="break-out">

<pre><code class="language-javascript">const rp = require('request-promise');

const rebuildSite = async function() {
    var options = {
         method: 'POST',
         uri: 'https://api.netlify.com/build_hooks/5d7fa6175504dfd43377688c',
         body: {},
         json: true
    };

    const returned = await rp(options).then(function(res) {
         console.log('Successfully hit webhook', res);
     }).catch(function(err) {
         console.log('Error:', err);
     });

    return returned
}
</code></pre>
</div>

{{< vimeo id="368119408" caption="A demo of the Netlify Function setup and the iOS Shortcut setup combined" >}}

## Setting Up An iOS Shortcut

So, we have a database, a way to display data and a function to add data, but we’re still not very user-friendly.

Netlify provides URLs for our Lambda functions, but they’re not fun to type into a mobile device. We’d also have to pass a URL as a query parameter into it. That’s a LOT of effort. How can we make this as little effort as possible?

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d68438f8-23dc-4253-b34c-bce3428ade47/bookmarking-application-faunadb-netlify-11ty-ios-shortcuts-image.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d68438f8-23dc-4253-b34c-bce3428ade47/bookmarking-application-faunadb-netlify-11ty-ios-shortcuts-image.png" sizes="100vw" caption="A visual reference for the setup for our Shortcut functionality (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d68438f8-23dc-4253-b34c-bce3428ade47/bookmarking-application-faunadb-netlify-11ty-ios-shortcuts-image.png'>Large preview</a>)" alt="A visual reference for the setup for our Shortcut functionality" >}}

Apple’s Shortcuts app allows the building of custom items to go into your share sheet. Inside these shortcuts, we can send various types of requests of data collected in the share process.

Here’s the step-by-step Shortcut:

1. Accept any items and store that item in a "text" block.
2. Pass that text into a "Scripting" block to URL encode (just in case).
3. Pass that string into a URL block with our Netlify Function’s URL and a query parameter of `url`.
4. From "Network" use a "Get contents" block to POST to JSON to our URL.
5. Optional: From "Scripting" "Show" the contents of the last step (to confirm the data we’re sending).

To access this from the sharing menu, we open up the settings for this Shortcut and toggle on the "Show in Share Sheet" option.

As of iOS13, these share "Actions" are able to be favorited and moved to a high position in the dialog.

We now have a working "app" for sharing bookmarks across multiple platforms!

## Go The Extra Mile!

If you’re inspired to try this yourself, there are a lot of other possibilities to add functionality. The joy of the DIY web is that you can make these sorts of applications work for you. Here are a few ideas:

1. Use a faux "API key" for quick authentication, so other users don’t post to your site (mine uses an API key, so don’t try to post to it!).
2. Add tag functionality to organize bookmarks.
3. Add an RSS feed for your site so that others can subscribe.
4. Send out a weekly roundup email programmatically for links that you’ve added.

Really, the sky is the limit, so start experimenting!

{{< signature "dm, yk" >}}

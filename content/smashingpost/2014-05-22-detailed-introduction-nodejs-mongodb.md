---
title: An Introduction To Node.js And MongoDB
slug: detailed-introduction-nodejs-mongodb
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17ceed32-eed8-45ed-8802-6ea7827c784d/nodejs-illu.jpg'
date: 2014-05-22T21:33:00.000Z
author: elliotbonneville
description: >-
  Node.js is a rapidly growing technology that has been overtaking the world of
  server-side programming with surprising speed. MongoDB is a technology that’s
  revolutionizing database usage. Together, **the two tools are a potent
  combination**, thanks to the fact that they both employ JavaScript and JSON.
categories:
  - Coding
  - Backend
  - Node.js
---
Node.js is a rapidly growing technology that has been overtaking the world of server-side programming with surprising speed. MongoDB is a technology that’s revolutionizing database usage. Together,<strong> the two tools are a potent combination</strong>, thanks to the fact that they both employ JavaScript and JSON.

At first glance, coming to grips with Node.js and MongoDB can seem both time-consuming and painful. Read on to learn how to wield these tools quickly and easily. Before getting started, let’s take a quick look at what this article offers:

*   Set up a basic server with Node.js.
*   Establish a connection to a MongoDB database.
*   Learn how to select records through database calls.
*   Finally, build and serve an HTML page with our newly retrieved data.

<img title="A Detailed Introduction To Node.js And MongoDB" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c458ea9e-b50c-43cf-9bcb-996b135d8790/mongodb-intro-opt.jpg" alt="A Detailed Introduction To Node.js And MongoDB" width="500" height="320" />

## Installing The Requisite Technologies

Let’s get started by setting up a basic Node.js server. If you haven’t already, install Node.js by <a href="https://howtonode.org/how-to-install-nodejs">following the instructions on How to Node</a> or in one of the many articles like it floating around the Web. The next thing we’ll need is a small MongoDB database; I’ve already created one for us to test, but if you’d like to create your own, go ahead and set up an account on MongoLab, which will provide you with free hosting for a database of your own (and offer a remarkable scope of paid services).

{{% feature-panel %}}

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Web Scraping With Node.js](https://www.smashingmagazine.com/2015/04/web-scraping-with-nodejs/)
*   [Sailing With Sails.js: An MVC-style Framework For Node.js](https://www.smashingmagazine.com/2015/11/sailing-sails-js-mvc-style-framework-node-js/)
*   [Why You Should Stop Installing Your WebDev Environment Locally](https://www.smashingmagazine.com/2016/04/stop-installing-your-webdev-environment-locally-with-docker/)
*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)

Now that Node.js is set up and we have a database to connect to, we’ll need to install MongoJS, which is the library that Node.js uses to communicate with MongoDB. Luckily for us, when you installed Node.js, you also installed npm, which makes it a breeze to install MongoJS. Simply open up a terminal, navigate to the directory where your Node.js server will be located, and run <code>npm install mongojs</code>. The automated package manager will take care of the rest.</p>

### Examining The Server Code

With the preliminaries out of the way, we can proceed to writing the actual Node.js server, which we’ll run on localhost for the purpose of this tutorial. The first thing to do with any Node.js application is include the modules we’ll be using. In this case, we’ll need the HTTP module, which is used to create the server, and the MongoJS module, which we installed earlier:

<pre><code class="language-javascript">
var http = require("http"),
    mongojs = require("mongojs");
</code></pre>

Once we’ve included the modules we’re going to use, we need to connect to a MongoDB database. We need two things to do this. The first is a MongoDB connection URI. This is provided by default when you create a server on MongoLab, but just for the record, you can find the <a href="https://docs.mongodb.org/manual/reference/connection-string/">specification for MongoDB connection URIs</a> in the documentation. The second thing you’ll need is an array of <a href="https://docs.mongodb.org/manual/reference/glossary/#term-collection">collections</a> (which are “groupings of MongoDB documents”) that you’d like to access in that database. We just want to access one collection in this case, but you can stick as many as you’d like in the array.

Once you have the database URI and the array of collections that you’d like to access, establishing a connection to a database is simple:

<pre><code class="language-javascript">
var uri = "mongodb://demo_user:demo_password@ds027769.mongolab.com:27769/demo_database",
    db = mongojs.connect(uri, ["demo_collection"]);
</code></pre>

We’ll need to create our server as well, using the HTTP module:

<pre><code class="language-javascript">
var server = http.createServer(requestHandler);
</code></pre>

When we call the <code>createServer</code> function, it expects a function to handle all incoming requests. This is the function that is called when a browser requests data from the server. The request-handling function, which we’ve aptly named <code>requestHandler</code>, is passed two variables: a request variable, which represents the browser’s page request, and a response variable, which is the response we’ll give to the browser. Let’s look at the <code>requestHandler</code> function:

<pre><code class="language-javascript">
function requestHandler(request, response) {
</code></pre>

The first thing we’ll do in the request handler is tell the browser what format our response will be in — HTML, plain text or something else entirely — so that it knows how to handle the data it gets.

<pre><code class="language-javascript">
response.writeHead(200, {"Content-Type": "text/html"});
</code></pre>

The next thing we’ll do — and this is the interesting bit — is query the database we linked to earlier, so that we have information to work with. We’ll pass a JSON object to the <code>find</code> function, specifying the property that we’d like the returned records to share. The <code>find</code> function returns a cursor to the documents returned by our query; this cursor is iterable and contains all of the data we need.

<pre><code class="language-javascript">
db.demo_collection.find({"color": "red"}, function(err, records) {
</code></pre>

## When Things Go South

Within the <code>find</code> function, we’re given two variables to work with: <code>err</code> and <code>records</code>. The <code>err</code> variable contains any data about an error, if one has occurred. First, we check whether any errors have been thrown while attempting the database query. If no problem occurred, then we carry on. But if one did, then we wouldn’t have any data to work with and the rest of the function would be useless, so we’d just log the issue and return immediately; there’d be no point in executing the rest of the function.

<pre><code class="language-javascript">
if(err) {
    console.log("There was an error executing the database query.");
    response.end();
    return;
}
</code></pre>

OK, now that we’ve got our data, which is contained in the cursor <code>records</code>, we need to iterate that data and build an HTML string for the server to give to the browser. We’ll create a variable to hold our HTML string, and then iterate through our records. Then, we’ll build a string for each document and append it to the main HTML string:

<pre><code class="language-javascript">
var html = '&lt;h2&gt;Vehicles with a red finish&lt;/h2&gt;',
    i = records.length;

while(i--) {
    html += '&lt;p&gt;&lt;b&gt;Name:&lt;/b&gt; ' 
         + records[i].name 
         + ' &lt;br /&gt;&lt;b&gt;Number of wheels:&lt;/b&gt; ' 
         + records[i].wheels 
         + '&lt;br /&gt;&lt;b&gt;Color: &lt;/b&gt;' 
         + records[i].color;
}
</code></pre>

Finally, once we’ve finished iterating through all of the records, we’ll write our response by generating an HTML string with a quick <code>while</code> loop. Now, Node.js offers many more methods for displaying HTML, the most common of which is by serving up a static page (often with a framework such as Express), but generating a string is a quick and dirty way to display some basic HTML.

This particular HTML string contains the data for the entire page. So, once we call <code>response.write</code>, we’ll know that the client has all of the information it needs, and we’ll end the response so that it can load the page.

<pre><code class="language-javascript">
response.write(html);
response.end();
</code></pre>

## Wonder Twins, Activate!

That’s pretty much all there is to creating a basic HTML server with Node.js and using that server to connect to a MongoDB database. The last thing to do is tell the server to listen at whatever port we specify:

<pre><code class="language-javascript">server.listen(8888);
</code></pre>

Executing this code will fire up a local server that you can access at port 8888 (<code>localhost:8888</code> in your browser).</p>

## Conclusion

As you can see, setting up a Node.js server and connecting it to a MongoDB database is remarkably simple, at least compared to the majority of technologies that compete with this power duo. Of course, setting up security and proper error-handling can take a little more work, but resources for working with Node.js and MongoDB are growing rapidly. Together, the tools offer a quick yet enormously flexible solution that’s taking the server-side programming world by storm.</p>

### Further Reading

*   “[Install MongoDB](https://docs.mongodb.org/manual/installation/),” MongoDB Read up on how to install a local copy of MongoDB.
*   “[Tutorial: MongoDB 2.4.2 on OS X Using Homebrew](https://blog.nicoversity.com/2013/04/tutorial-mongodb-2-4-2-on-os-x-using-homebrew/),” Nico Reski An in-depth tutorial on setting up MongoDB on OS X with Homebrew.
*   “[The Dead-Simple Step-by-Step Guide for Front-End Developers to Getting Up and Running With Node.JS, Express, Jade, and MongoDB](https://cwbuecheler.com/web/tutorials/2013/node-express-mongo/),” Christopher Buecheler This tutorial covers a more advanced Node.js and MongoDB application.
*   “[The Node.js MongoDB Driver Manual](https://mongodb.github.io/node-mongodb-native/),” MongoDB If you’re serious about MongoDB, you might want to check out the documentation.

{{< signature "il, al" >}}


---
title: 'Sailing With Sails.js: An MVC-style Framework For Node.js'
slug: sailing-sails-js-mvc-style-framework-node-js
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec37e5e1-5e45-4318-a368-84b3bff0c2b9/sails-opt.png'
date: 2015-11-24T19:01:28.000Z
author: slavafomin
description: >-
  I had been doing server-side programming with Symfony 2 and PHP for at least
  three years before I started to see some productivity problems with it. Don’t
  get me wrong, I like Symfony quite a lot: It’s a mature, elegant and
  professional framework. But I’ve realized that **too much of my precious time
  is spent not on the business logic** of the application itself, but on
  supporting the architecture of the framework.

  I don’t think I’ll surprise anyone by saying that we live in a fast-paced
  world. The whole startup movement is a constant reminder to us that, in order
  to achieve success, we need to be able to test our ideas as quickly as
  possible. The faster we can iterate on our ideas, the faster we can reach
  customers with our solutions, and the better our chances of getting a
  product-market fit before our competitors do or before we exceed our limited
  budget. And in order to do so, **we need instruments suitable** to this type
  of work.
categories:
  - Coding
  - Frameworks
  - JavaScript
---
I had been doing server-side programming with Symfony 2 and PHP for at least three years before I started to see some productivity problems with it. Don’t get me wrong, I like Symfony quite a lot: It’s a mature, elegant and professional framework. But I’ve realized that <strong>too much of my precious time is spent not on the business logic</strong> of the application itself, but on supporting the architecture of the framework.

I don’t think I’ll surprise anyone by saying that we live in a fast-paced world. The whole startup movement is a constant reminder to us that, in order to achieve success, we need to be able to test our ideas as quickly as possible.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Web Scraping With Node.js](https://www.smashingmagazine.com/2015/04/web-scraping-with-nodejs/)
*   [<span class="headline">Journey Through The JavaScript MVC Jungle</span>](https://www.smashingmagazine.com/2012/07/journey-through-the-javascript-mvc-jungle/)
*   [<span class="headline">A Thorough Introduction To Backbone.Marionette</span>](https://www.smashingmagazine.com/2013/02/introduction-backbone-marionette/)
*   [A Detailed Introduction To Webpack](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/)

The faster we can iterate on our ideas, the faster we can reach customers with our solutions, and the better our chances of getting a product-market fit before our competitors do or before we exceed our limited budget. And in order to do so, <strong>we need instruments suitable</strong> to this type of work.

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/13d35e78-9e0f-4dc0-959f-d6fda0e5e58f/sails-opt-3.png" alt="Sailing With Sails.js" /></figure>

If you’re developing a complex application with three hundred pages of documentation for some big corporate client and you know most of its details from the start, then Symfony 2 or some enterprise Java framework would probably be the best tool for the job. However, if you are a startup developer or you just want to <strong>test some of your ideas quickly without compromising the overall quality</strong> of the application, then <a href="https://sailsjs.org/">Sails</a> (or Sails.js) is a very interesting candidate to consider.

I’ll neither confirm nor deny that Sails is being developed by a giant smart octopus, but I will do my best to guide you from the humble ensign to being the confident captain of your own ship!

## Introduction

Sails is a comprehensive <strong>MVC-style framework for Node.js</strong> specifically designed for rapid development of server-side applications in JavaScript. It’s robust service-oriented architecture provides different types of components you can use to neatly organize code and separate responsibilities. And if you’re disciplined, then developing an enterprise-level application with it is even possible.

Written in JavaScript, Sails gives you the additional benefit of being able to <strong>share your code between the server and client</strong>. This could be very helpful, for example, for implementing data validation where you need to have the same validation rules both in the client and on the server. Also, with Sails you need to master only one programming language, instead of several.

One major concept of the framework is that <strong>it wraps a stack of loosely coupled components</strong>. Almost every aspect of the system is customizable: You can add, remove or replace most of the core components without compromising the framework’s overall stability. In other words, if you need to get a job done as quickly as possible, Sails will help you by providing robust built-in components with sensible defaults; however, if you’d like to create a fully customized solution, Sails will not stand in your way either. If you are already familiar with the philosophy behind the Node.js development community, then you will get what I mean; if not, then you will understand it during the course of this article.

Under the hood, Sails contains probably the most well-known web framework for Node.js, Express. <a href="https://expressjs.com/">Express</a> is a very simple, basic framework. It provides the mere bones for your web development needs. To implement a serious web app with it, you will need to find and integrate a bunch of third-party components yourself. Also, Express doesn’t really care about the structure of code or a project’s file system, so you will need to manage that yourself and come up with a sensible structure. That’s where Sails comes to the rescue. Built on top of Express’ robust design, it <strong>provides all required components out of the box</strong> and gives developer a well-thought-out organization for their code and project files. With Sails, you will be able to start development with the built-in and documented tools.

I believe the best way to understand something is to get ahold of it and explore it firsthand. So, enough talking. <strong>Let’s grab the code</strong> and create our first local project!

## Getting Started

I’ll start with a clean slate. Let’s begin by installing all of the requirements and the latest version of Sails itself.

I’m using Ubuntu Linux, so all commands will be presented for this OS. Please adjust them according to your working environment.</p>

### Install Node.js

To install the latest version of Node.js on your Ubuntu machine from <a href="https://github.com/nodesource/distributions">NodeSource Node.js Binary Distributions</a>, just run these three commands:

<pre><code class="language-bash">
# Make sure cURL is available in the system
sudo apt-get install -y curl

# Adding NodeSource repository to the system via provided script
curl -sL https://deb.nodesource.com/setup_dev | sudo bash -

# Actually installing the Node.js from the NodeSource repository
sudo apt-get install -y nodejs
</code></pre>

You can confirm that Node.js has been successfully installed by using this command:

<pre><code class="language-bash">node --version</code></pre>

It should output something like <code>v0.12.4</code>.

<strong>Note:</strong> If you’re not using Ubuntu, then please see Joyent’s instructions on <a href="https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager">installing Node.js on different platforms</a>.</p>

### Install Sails

The following command will install Sails globally:

<pre><code class="language-bash">sudo npm -g install sails</code></pre>

You can test whether the framework was installed with this command:

<pre><code class="language-bash">sails --version</code></pre>

It should output the number of the latest stable version of Sails.</p>

### Create a Project

Let’s create the test project that we will be experimenting with:

<pre><code class="language-bash">
sails new sails-introduction
cd ./sails-introduction
</code></pre>

### Start a Project

The most interesting aspect of Node.js is that the application doesn’t require an external web server in order to operate. In the world of Node.js, the application and the web server are the same thing. When you run your Sails application, it binds to the given port and listens for HTTP requests. All requests are handled in the same OS process sequentially by your application. (In contrast, Apache will spawn multiple sub-processes or threads, and each request will have its own context space.)

So, how can your application serve multiple requests without those requests noticeably blocking each other? The key to this is a major feature of the Node.js: <strong>asynchronosity</strong>. All heavy operations, such as I/O and database access, are performed in a non-blocking asynchronous fashion. Every asynchronous method allows you to specify a callback function, which is activated as soon as the requested operation completes. The result of the operation (or error description) gets passed to your callback function. That way, your application can delegate all heavy work and continue with its own business, returning later to collect the results and continue where it left off.

<strong>Note:</strong> The more convenient and modern approach is to use promises instead of callback functions, but that is beyond the scope of this article. Please see <a href="https://www.html5rocks.com/en/tutorials/es6/promises/">Jake Archibald’s article</a> for more insight into the topic.

Let’s start our project to see that everything is working fine. Just run the following:

<pre><code class="language-bash">sails lift</code></pre>

Sails will initialize the application, bind to the configured port and start to listen for HTTP requests.

<strong>Note:</strong> When your application is lifted, the terminal window will be in blocked state. You can press <code>Control + C</code> to terminate the application and return to the command prompt.

Now, you will be able to open the default application in your favorite browser by visiting https://localhost:1337/.

At this point, the default page should load correctly.</p>

## Diving Into Sails

Now, let’s dissect our project to understand what makes it tick!

Sails is an MVC framework, so starting from these components to see what glues them all together makes sense.

The entry point to our application is the <code>app.js</code> file, which lies at the root of the project. You could call it a front controller if you’d like; however, it wouldn’t make sense to edit its content. All it does is require top-level dependencies and give control to Sails itself. After that, all of the magic happens in the framework.</p>

### Routing Component

When Sails receives an HTTP request, it actually uses its router component to find the controller responsible for generating the response. Router matching can be controlled through a special configuration file located at <code>config/routes.js</code>. If you open this file now, you will see that it contains only a single entry:

<pre><code class="language-javascript">
module.exports.routes = {
  '/': {
    view: 'homepage'
  }
};</code></pre>

<strong>Note:</strong> The default project for Sails contains <em>a lot</em> of comments, which were introduced specifically to speed up project configurations and ease the learning curve. Feel free to remove them if you’d like. No code snippets in this article will contain any built-in comments, in order to preserve space and improve readability.

The left part of the expression, <code>'/'</code>, is the URL pattern that tells Sails that the following configuration (the right part) should be used for an index page. The <code>view</code> property of the configuration contains the <code>homepage</code> value, which is the name of the view (the V in MVC).</p>

### Views Layer

Views are handled by a separate component of the framework. With the help of the “Consolidate” Node.js package, Sails supports <a href="https://github.com/tj/consolidate.js#supported-template-engines">at least 31 different templating languages</a>. So, choose the language that is most suitable for you, your project and your team.

All templates are located in the <code>views</code> directory of your project. You will find there the aforementioned <code>views/homepage.ejs</code> template file that is used to render the home page, and you can play with it if you like.

<strong>Note:</strong> All templates are rendered dynamically on the server. You will not need to restart Sails in order to refresh any changed templates. All changes will be shown immediately upon the page being refreshed. Try it!

If you look at the <code>homepage.ejs</code> template, you will notice that it’s not complete. It’s missing basic HTML elements, such as the <code>DOCTYPE</code>, <code>html</code>, <code>head</code> <code>body</code> tags. This is on purpose. The most reusable parts of the template are extracted into a separate template file, <code>views/layout.ejs</code>. The name of the layout template is configured in the <code>config/views.js</code> file (look for the <code>layout</code> property). This really helps to keep things DRY. However, if you need to use another layout for some particular page, you can easily override the property dynamically in your controller.

Be advised that this layout configuration works only for the default EJS templating system and will not work with other languages. This is done for the purpose of legacy- and backwards-compatibility. Using the layout functionality provided by the templating language of your choice is recommended. For example, in Twig and Jinja2, you can use the <code>extends</code> expression to extend a parent template and overload required blocks.</p>

### Using Custom Views Engine

This section demonstrates how to change the views engine that is used to render templates in Sails. This should give you an idea of how easy some parts of Sails can be overridden and customized. I’m going to use the Twig/Jinja2 templating language, because of its flexibility and extensibility. I’ve been using it for at least three years now, and the language has never constrained me in any way. So, I highly recommend you try it.

<strong>Note:</strong> Twig and Jinja2 are a common family of templating languages with the same core functionality and features. However, each concrete implementation can have its own small differences and flavors. I will be using the Swig library during the course of this article. It provides a concrete implementation of the Twig and Jinja2 templating syntax for Node.js. Please see Swig’s official documentation for more details.

As I said earlier, Sails delegates view rendering to the Node.js package called “Consolidate.” This package actually consolidates about 30 different view engines. I will be using the Swig view engine, which implements support for the Twig and Jinja2 templating languages. To use it, I will need to complete a few simple steps:

1.  Define dependencies and install the Swig package: `npm install --save swig`.
2.  Change Sails’ configuration a bit by editing the `config/views.js` file. All you need to do is to set the `engine` property to `swig`.
3.  Rewrite all templates from EJS format to Twig and Jinja2\. Don’t forget to change the extension to `.swig`!
4.  Reload the Sails server.

<strong>Note:</strong> In order to see the changes, you will need to reload the application by terminating the server and then lifting it again.

An answer on Stack Overflow gives some hints on how this can be automated.

The content for all of the changed files are provided below for your reference.

<strong>config/views.js:</strong>

<pre><code class="language-javascript">
module.exports.views = {
  engine: 'swig'
};
</code></pre>

<strong>views/layout.swig:</strong>

<pre><code class="language-markup">
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
  &lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;title&gt;{{ title|default('The Default Title') }}&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    {% block body %}{% endblock %}
  &lt;/body&gt;
&lt;/html&gt;
</code></pre>

<strong>views/homepage.swig:</strong>

<pre><code class="language-markup">
{% extends 'layout.swig' %}
{% set title = 'Homepage Title' %}
{% block body %}
  &lt;h1&gt;Homepage!&lt;/h1&gt;
  &lt;p&gt;Welcome to the homepage!&lt;/p&gt;
{% endblock %}
</code></pre>

<strong>views/404.swig:</strong>

<pre><code class="language-markup">
{% extends 'layout.swig' %}
{% set title = 'Page Not Found' %}
{% block body %}
  &lt;h1&gt;{{ title }}&lt;/h1&gt;
{% endblock %}
</code></pre>

The content for <code>403.swig</code> and <code>500.swig</code> is almost the same as for <code>404.swig</code> presented above. I will leave it to you to fix the files yourself.</p>

### The Controller

OK, we’ve looked into the routes and views components, but where is the controller part of the MVC, you ask? Actually, the default Sails project is so simple that it doesn’t require any custom logic. If you open the <code>api/controllers</code> directory, you will see that it’s empty.

As you have guessed, Sails can even run without a controller; the routing configuration may specify the view directly, without the need of a controller. This could be a useful feature for static pages that don’t require any input from the user or any additional processing, as is the case with our home page right now. But let’s fix this shortcoming and introduce some business logic into our route.

Let’s create a new controller for our home page with the following command:

<code class="language-bash">sails generate controller homepage</code>

Sails will generate a file for you, <code>api/controllers/HomepageController.js</code>.

We can open this file and introduce a new action for our home page. I will call it <code>index</code>:

<pre><code class="language-javascript">
module.exports = {
  index: function (request, response) {
    return response.view('homepage', {
      currentDate: (new Date()).toString()
    });
  }
};
</code></pre>

This simple action will just render our <code>homepage</code> view that we discussed earlier and pass an additional variable to it called <code>currentDate</code>, which will contain the textual presentation of the current date.

<strong>Note:</strong> The controller’s action is a simple JavaScript function that accepts two arguments: the special <code>request</code> and <code>response</code> objects. These objects correspond directly to the objects provided by the Express framework. Please look at <a href="https://expressjs.com/3x/api.html">Express’ documentation</a> for the API details.

To make Sails actually use our controller, we need to slightly alter the routing configuration in the <code>config/routes.js</code> file:

<pre><code class="language-javascript">
module.exports.routes = {
  '/': 'HomepageController.index'
};
</code></pre>

Here, we are telling the system to give control of the request to our <code>HomepageController</code> and, specifically, its <code>index</code> action. Now, the controller is responsible for handling the request and generating the response.

Also, don’t forget to add the following line to the <code>views/homepage.swig</code>:

<pre><code class="language-markup">
&lt;p&gt;Current date is: {{ currentDate }}&lt;/p&gt;
</code></pre>

This will render the date string passed from the controller.

Now, reload the server and refresh the page. You should see the changes.</p>

### Shadow Routes for Actions

By default, Sails will generate <strong>implicit</strong> routes (also called <strong>shadow</strong> routes) for every controller’s action. The generated URL will look like <code>/:controller/:action</code>. In our case it will be https://localhost:1337/homepage/index. Although, this feature can be useful, sometimes it’s not desired (such as when you get two URLs for a home page, as in our case).

You can control this behavior by configuring the <code>blueprints</code> component, which can be done in two place. The first and most obvious place is the <code>config/blueprints.js</code> configuration file. You can disable action shadow routes for an entire application by setting the <code>actions</code> option to <code>false</code>:

<pre><code class="language-javascript">
module.exports.blueprints = {
  actions: false
};
</code></pre>

However, to disable shadow routes for a single controller only, you would set it in the controller itself, <code>api/controllers/HomepageController.js</code>:

<pre><code class="language-javascript">
module.exports = {
  _config: {
    actions: false
  },
  index: function (request, response) {
    return response.view('homepage', {
      currentDate: (new Date()).toString()
    });
  }
};
</code></pre>

The special <code>_config</code> option of the controller’s module allows you to provide custom configuration for a specific controller.</p>

### Model Layer

The final part of the MVC paradigm is the model. Sails comes with an advanced ORM/ODM component called Waterline. It was initially designed as a part of the Sails framework and later extracted into a separate Node.js module that can now be used independently.

Waterline provides an abstraction layer that connects your application to a wide variety of databases transparently and seamlessly. The main idea is that you would define your application’s domain model as a set of related entities (JavaScript objects) and that entities are automatically mapped to the database’s underlying tables and/or documents. The interesting aspect of Waterline is that it supports related entities between several databases. For example, you could store users in the PostgreSQL database and related orders in the MongoDB; the abstraction layer would be able to fetch them for you without your even noticing the difference.

Waterline is a pretty big component, and I’m not able to fully cover it in this introductory article, but I will try to give you the taste of it.

Suppose we are creating a simple app to manage contacts. Our app will have just two types of entities: a person and their contact information. The end user would be able to create a person and add multiple contact details for them.

Each separate database system that you would use in your Sails project requires a connection specification. The <strong>connections</strong> are configured in the <code>config/connections.js</code> file. I’m going to use a special database type called <code>sails-disk</code>. This database <strong>adapter</strong> is actually built into Sails, and it stores all data in a simple JSON file. This can be very useful when you are starting to design an app and have not yet selected or deployed a real database server.

Let’s now open the <code>config/connections.js</code> file and configure our connection:

<pre><code class="language-javascript">
module.exports.connections = {
  main: {
    adapter: 'sails-disk'
  }
};
</code></pre>

This short configuration is enough for the <code>sails-disk</code> adapter. However, in a real-world scenario, you would need to provide all of the details required to connect to the database system of your choice — for example, the host name, port number, database name, username and so on.

Also, we would need to configure the model layer to use the specified connection by default for each model that we define. Open the <code>config/models.js</code> file and change its content to the following:

<pre><code class="language-javascript">
module.exports.models = {
  connection: 'main',
  migrate: 'alter'
};
</code></pre>

The <code>migrate</code> property controls how Sails rebuilds the schema in your underlying database when a model definition changes. When it’s set to <code>alter</code>, Sails will try to update the schema without losing any data each time while the application lifts. The <code>drop</code> could also be a viable option in some cases — then, Sails will just recreate the schema every time the app is lifted. In a production environment, Sails will use the <code>safe</code> option, which will not make any changes to the schema at all. This really helps with protecting the fragile data in the production database. In safe mode, you will need to execute the migration manually. Leaving the <code>migrate</code> option undefined is also possible. In this case, Sails will ask you for an interactive choice every time when a migration is required.

Now, we are ready to define our models. Let’s use Sails’ built-in generator to create model files for us. Just issue these commands:

<pre><code class="language-bash">
sails generate model person
sails generate model contact
</code></pre>

Sails will create two basic files. Let’s edit them.

First, open the generated <code>api/models/Person.js</code> model and edit it:

<pre><code class="language-javascript">
module.exports = {
  attributes: {
    firstName: {
      type: 'string',
      size: 128,
      required: true
    },
    lastName: {
      type: 'string',
      size: 128
    },
    contacts: {
      collection: 'Contact',
      via: 'person'
    }
  }
};
</code></pre>

Here, we are defining three fields: <code>firstName</code>, <code>lastName</code> and the <code>contacts</code> collection to hold the contact details. To define a many-to-one relationship between two models, we need to use two special properties. The <code>collection</code> property holds the name of the related model. The <code>via</code> property tells Waterline what field of the related model will be used to map back to this model. Hopefully, this is pretty self-explanatory.

Also, the <code>size</code> property specifies the maximum length of the string in the database column, and the <code>required</code> property specifies which columns may not contain null values.

Let’s edit the second model in <code>api/models/Contact.js</code> file:

<pre><code class="language-javascript">
module.exports = {
  attributes: {
    type: {
      type: 'string',
      enum: ['mobile', 'work', 'home', 'skype', 'email'],
      required: true,
      size: 16
    },
    value: {
      type: 'string',
      size: 128,
      required: true
    },
    person: {
      model: 'Person',
      required: true
    }
  }
};
</code></pre>

Here, we’re defining yet another three fields. The <code>type</code> field will hold the type of the contact information. It could be a mobile number, a home phone number, a work number, etc. The additional <code>enum</code> property specifies the list of accepted values for this field. The <code>value</code> field holds the corresponding value. And the <code>person</code> field, mentioned earlier, maps the <code>contact</code> model to its parent <code>person</code> model through the special <code>model</code> property.

<strong>Note:</strong> We are not defining any primary keys or ID fields in our models. Waterline handles that for us automatically. The form of the ID’s value will depend on the database adapter being used because each database system uses different strategies to generate unique keys.

Also, Waterline will create two additional fields for each model, called <code>createdAt</code> and <code>updatedAt</code>. These fields hold the dates of when the entity was created and updated, respectively.

This behavior can be configured through the <a href="https://sailsjs.org/#!/documentation/concepts/ORM/model-settings.html">model options</a>.</p>

### Using Sails’ Console to Test the Models

Sails offers a very nice interactive console that immerses the developer in the depth of an application’s context and that runs any JavaScript code we like.

The models are now defined, and we can use Sails’ console to test them and learn some basic APIs of Waterline.

Run the following command to launch Sails’ console:

<pre><code class="language-bash">sails console</code></pre>

After the console has launched, we can type in and execute some JavaScript in the context of our application. This is a quick way to test some aspects of a project.

First, let’s create some entities. Just type the following code into Sails’ console and execute it:

<pre><code class="language-javascript">
Person.create({ firstName: 'John', lastName: 'Doe' }).exec(console.log);
</code></pre>

The <code>Person</code> here is the model we defined earlier (Sails exposes all models globally for your convenience). The <code>create()</code> is the method that creates new entities of the specified models; it takes an object with the field’s values as an argument. Make sure to correctly specify all required fields. Finally, the <code>exec()</code> method actually runs the required operations on the underlying database. It takes a single argument, the callback function, which will be called when the action completes. The created entity gets passed to it as a second argument. We are using the convenient <code>console.log</code> function here to output the newly created entity to the console.

The result should look as follows:

<pre><code class="language-javascript">
{
  firstName: 'John',
  lastName: 'Doe',
  createdAt: '2015-05-07T22:01:26.251Z',
  updatedAt: '2015-05-07T22:01:26.251Z',
  id: 1
}
</code></pre>

See how the unique ID was assigned to the entity and additional fields were added with the actual dates.

Next, let’s create two contacts:

<pre><code class="language-javascript">
Contact.create({ type: 'mobile', value: '+7 123 123-45-67', person: 1 }).exec(console.log);
Contact.create({ type: 'skype', value: 'johndoe', person: 1 }).exec(console.log);
</code></pre>

Make sure to specify the required <code>person</code> field with the proper ID value. This way, Waterline will know how to relate the entities to each other.

The final thing to do is fetch the created person, as well as the collection of its child contacts:

<pre><code class="language-javascript">
Person.find(1).populate('contacts').exec(console.log);
</code></pre>

The <code>find()</code> method finds entities of the specified model; by passing <code>1</code> to it, we are telling Waterline to find the <code>person</code> entity with the ID of <code>1</code>. The <code>populate()</code> method fetches the related entities; it accepts the name of the field to fetch.

It should return the person entity with all of its child contact entities as a traversable JavaScript object.

<strong>Note:</strong> I suggest that you experiment now and create multiple entities. As part of your experiment, see how validation rules are enforced by omitting some required fields or by using an incorrect <code>enum</code> value.

Of course, use <a href="https://sailsjs.org/#!/documentation/concepts/ORM">Waterline’s documentation</a> to your advantage!

### Shadow Routes for Models

The Blueprints component, mentioned earlier when we talked about controllers, also comes into play with models. Again, it makes the developer’s life easier with two useful features: automatic <strong>REST</strong> and <strong>shortcut</strong> routes for our models.

By default, the Blueprints API provides implicit (shadow) routes for each model, with a defined controller. For this to work, we need to create empty controllers for our models. Just create two files, <code>api/controllers/PersonController.js</code> and <code>api/controllers/ContactController.js</code>, with the following content:

<pre><code class="language-javascript">
module.exports = {
};
</code></pre>

After that, restart the application.

Now, with the help of the Blueprint API and its shortcut routes, we can enter the following URLs in the browser:
<table class="article-table three-columns">
<thead>
<tr>
<th>URL</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>/person/create?firstName=John&amp;lastName=Doe</code></td>
<td>to create a new person entity</td>
</tr>
<tr>
<td><code>/person/find/2</code></td>
<td>to get the person with the ID of <code>2</code></td>
</tr>
<tr>
<td><code>/person/update/2?firstName=James</code></td>
<td>to update a person with the ID of <code>2</code>, giving it a new first name</td>
</tr>
</tbody>
</table>

These shortcut methods could be pretty useful during application development, but should be disabled in a production environment. I will show you how to do exactly that in the “Environments” section of this article.

Another, and probably the most useful, part of Blueprints is the automatic support for the REST APIs. The following implicit routes are provided for CRUD operations:
<table class="article-table three-columns">
<thead>
<tr>
<th>HTTP Method</th>
<th>URL</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>POST</code></td>
<td><code>/person</code></td>
<td>creates a new person</td>
</tr>
<tr>
<td><code>GET</code></td>
<td><code>/person/2</code></td>
<td>gets a person with ID of <code>2</code></td>
</tr>
<tr>
<td><code>PUT</code></td>
<td><code>/person/2</code></td>
<td>updates a person with ID of <code>2</code></td>
</tr>
<tr>
<td><code>DELETE</code></td>
<td><code>/person/2</code></td>
<td>deletes a person with ID of <code>2</code></td>
</tr>
</tbody>
</table>

Let’s create a new person using the REST API provided. I’ll use the great application for Google Chrome called <a href="https://www.getpostman.com/">Postman</a>. It’s free and extremely useful for working with different HTTP APIs.

Select the <code>POST</code> HTTP method. Enter the URL <code>https://localhost:1337/person</code>, and provide the following JSON “raw” request body:

<pre><code class="language-javascript">
{
  "firstName": "John",
  "lastName": "Doe"
}
</code></pre>

Make sure to select <code>application/json</code> as the request’s content type.

Now, hit the “Send” button.

Sails should satisfy your request and return a new entity with the freshly generated ID: <code>STATUS 201 Created</code>.

<pre><code class="language-javascript">
{
  "firstName": "John",
  "lastName": "Doe",
  "createdAt": "2015-05-13T21:54:41.287Z",
  "updatedAt": "2015-05-13T21:54:41.287Z",
  "id": 4
}
</code></pre>

<strong>Note:</strong> I would recommend experimenting with these methods now. Try to create a new person and some contacts. Update the contacts to assign them to a different person. Try to delete a person. What happens with their associated contacts?

Every implicit Blueprint API route will be provided only if the model’s controller lacks the required action. For example, when you’re getting a single entity, the Blueprint API will look for an action called <code>findOne</code>. If such an action is not present in your model controller, then the Blueprint API will implement its own generic version of it. However, when an action is present, it will be called instead. Let’s create a very simple example just for the sake of demonstration: <code>api/controllers/PersonController.js</code>:

<pre><code class="language-javascript">
module.exports = {
  findOne: function (request, response) {
    Person.find(request.params.id).exec(function (error, persons) {
      var person = persons[0];
      person.fullName = person.firstName + ' ' + person.lastName;
      response.json(person);
    });
  }
};
</code></pre>

This is a very simplified example of how such an action could work. All it does is fetch the required entity from the database and generate a new field called <code>fullName</code> from the first and last name of the person; then, it just returns a JSON result.

<strong>Be advised:</strong> This is a simple example that doesn’t handle errors or edge cases properly.

The complete list of all REST operations that are supported by the Blueprint API can be found in the <a href="https://sailsjs.org/#!/documentation/reference/blueprint-api">official documentation</a>.</p>

### Environments

Sails supports multiple execution environments; the built-in ones are <strong>development</strong> and <strong>production</strong>. When you run <code class="language-bash">sails lift</code>, it runs your app in the development environment by default. In other words, it’s equivalent to running <code class="language-bash">sails lift --dev</code>. You can also execute <code class="language-bash">sails lift --prod</code> to run your application in the production environment.

Multiple environments are provided to make the developer’s life easier. For example, in a development environment, some caching functionality is disabled by default in order to always return fresh results. Also, Sails will look for changes in your assets directory and will recompile assets in real time using its Grunt task.

We can take this concept further and use it to our advantage.

Each environment can override the application configuration to make it behave differently. If you look in your <code>config</code> directory, you will find a subdirectory named <code>env</code>. It contains custom configuration files for each environment. By default, these files are empty (not counting the comments).

Let’s configure our application to use port <code>80</code> in a production environment and also disable the Blueprint API’s shortcut methods. Open the <code>config/env/production.js</code> file and change its content:

<pre><code class="language-javascript">
module.exports = {
  port: 80,
  blueprints: {
    shortcuts: false
  }
};
</code></pre>

Now, start Sails using the following command:

<pre><code class="language-bash">sudo sails lift --prod</code></pre>

Here, <code>sudo</code> is required in order to bind to the privileged port. Also, make sure that the port you’ve specified is not used by some other web server, like Apache 2 or nginx. If you can’t start Sails this way for some reason, just replace the port with something else, like <code>8080</code>, and run the command again without the <code>sudo</code>.

Now, your Sails app should listen on port <code>80</code>, and all shortcut requests like <a href="https://localhost/person/find/2">https://localhost/person/find/2</a> should not work. However, the REST API should work as expected.

You can also check the current environment in your code dynamically and adjust the business logic according to it. The name of the current environment is stored in the global <code>sails.config.environment</code> property. Here’s an example:

<pre><code class="language-javascript">
if ('production' == sails.config.environment) {
  // Actually send the email only in production environment.
  sendEmail();
}
</code></pre>

## Final Words

In this introductory article, I’ve shown you the most important parts of the Sails framework and given you some specific examples to get you going. Of course, if you want to use it in your daily work, you will have to spend some time mastering it and taking it to the next level. The good news is that Sails comes with pretty solid documentation and an active community. The creator of Sales even answers questions on StackOverflow personally. You will not be alone.

And remember, constant self-education and exploration is key to success. When you get some good results with Sails, feel free to come by and help the developers make it even better.

I’m hoping to continue writing about more specific aspects of Sails to give you an even deeper understanding of the framework itself and the Node.js ecosystem as well. Stay tuned!

{{< signature "al, ml, rb, jb" >}}


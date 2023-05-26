---
title: Ember JS – An In-Depth Introduction
slug: an-in-depth-introduction-to-ember-js
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/43009de5-2a88-45b2-9870-457977cff82f/emberjs-logo1.png'
date: 2013-11-07T10:52:48.000Z
author: julien-knebel
description: >-
  With the release of Ember.js 1.0, it's just about time to consider giving it a try. This article aims to introduce Ember.js to newcomers who want to learn more about the framework. Users often say that the learning curve is steep, but once you’ve overcome the difficulties, then this framework is tremendous.
categories:
  - Coding
  - Tools
  - JavaScript
  - Techniques
  - HTML
---
Ember JS is a client-side javascript framework for creating aspiring single-page web apps. With the release of Ember JS 1.0, it's just about time to consider giving it a try. This article aims to introduce Ember.js to newcomers who want to learn about this framework.

Users often say that the learning curve is steep, but once you’ve overcome the difficulties, then Ember.js is tremendous. This happened to me as well. While the <a href="https://emberjs.com/guides/">official guides</a> are more accurate and up to date than ever (for real!), this post is my attempt to make things even smoother for beginners.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [React To The Future With Isomorphic Apps](https://www.smashingmagazine.com/2015/04/react-to-the-future-with-isomorphic-apps/)
*   [Write Your Next Web App With Ember CLI](https://www.smashingmagazine.com/2016/01/write-next-web-app-ember-cli/)
*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)
*   [Get Up And Running With Grunt](https://www.smashingmagazine.com/2013/10/get-up-running-grunt/)

First, we will clarify the main concepts of the framework. Next, we’ll go in depth with a step-by-step tutorial that teaches you how to build a simple Web app with Ember.js and Ember-Data, which is Ember’s data storage layer. Then, we will see how <code>views</code> and <code>components</code> help with handling user interactions. Finally, we will dig a little more into Ember-Data and template precompiling.

{{% feature-panel %}}

<figure><img loading="lazy" decoding="async" title="An In-Depth Introduction To Ember.js" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/18a1d0d9-ff0c-4656-8ec2-ef71cd41046f/emberjs-logo.png" alt="ember js" width="500" height="406" /><figcaption>Ember's famous little mascot, Tomster. (<a href="https://emberjs.com/">Image credits</a>)</figcaption></figure>

The <strong>unstyled demo below</strong> will help you follow each step of the tutorial. The <strong>enhanced demo </strong>is basically the same but with a lot more CSS and animations and a fully responsive UX when displayed on small screens.</p>

<figure><a class="cr" href="https://jkneb.github.io/ember-crud/unstyled">Unstyled demo</a> <a class="cr" href="https://github.com/jkneb/ember-crud">Source code</a> <a class="cr" href="https://jkneb.github.io/ember-crud">Enhanced demo</a></figure>

### Table of Contents

*   [Definitions of main concepts](#main_concepts)
*   [Let’s build a simple CRUD](#lets_build_an_app)
    *   [Sketch our app](#sketch_our_app)
    *   [What you’ll need to get started](#what_you_need_to_get_started)
    *   [Our files directory structure](#set_up_our_files_structure)
    *   [Precompile templates or not?](#precompile_templates_or_not)
    *   [Set up the model with Ember-Data’s FixtureAdapter](#set_up_the_model_with_ember_data_fixtureadapter)
    *   [Instantiate the router](#instantiate_the_router)
    *   [The application template](#the_application_template)
    *   [The users route](#the_users_route)
    *   [Object vs. array controller](#object_vs_array_controller)
    *   [Displaying the number of users](#displaying_the_number_of_users)
    *   [Computed properties](#computed_properties)
    *   [Redirecting from the index page](#redirecting_from_the_index_page)
    *   [Single user route](#single_user_route)
    *   [Edit a user](#edit_a_user)
    *   [Our first action](#our_first_action)
    *   [TransitionTo or TransitionToRoute?](#transitionTo_or_transitionToRoute)
    *   [Saving user modifications](#saving_user_modifications)
    *   [Delete a user](#delete_a_user)
    *   [Create a user](#create_a_user)
    *   [Format data with helpers](#format_data_with_helpers)
    *   [Format data with bound helpers](#format_data_with_bound_helpers)
    *   [Switch to the LocalStorage adapter](#switch_to_the_localstorage_adapter)
*   [Playing with views](#playing_with_views)
    *   [jQuery and the didInsertElement](#jquery_and_the_didinsertelement)
    *   [Side panel components with className bindings](#side_panel_components_with_classname_bindings)
    *   [Modals with layout and event bubbling](#modals_with_layout_and_event_bubbling)
*   [What is Ember-Data](#what_is_ember_data)
    *   [The store](#the_store)
    *   [Adapters](#adapters)
    *   [What about not using Ember-Data?](#what_about_not_using_emberdata)
*   [What is Handlebars template precompiling?](#what_is_handlebars_template_precompiling)
    *   [Template naming conventions](#templates_naming_conventions)
    *   [Precompiling with Grunt](#precompiling_with_grunt)
    *   [Precompiling with Rails](#precompiling_with_rails)
*   [Conclusion](#conclusion)
    *   [Tools, tips and resources](#tools_tips_resources)
    *   [Acknowledgments](#acknowledgments)

## Definitions Of Ember JS Main Concepts

The diagram below illustrates how routes, controllers, views, templates and models interact with each other.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88aa0a8d-b90c-4b2a-b3a3-ef46bbc98f42/ember-sketch.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88aa0a8d-b90c-4b2a-b3a3-ef46bbc98f42/ember-sketch.png" alt="ember-sketch" width="500" height="482" /></a></figure>

Let’s define these concepts. And if you’d like to learn more, check the relevant section of the official guides:

*   [Models](https://emberjs.com/guides/models)
*   [The Router](https://emberjs.com/guides/routing)
*   [Controllers](https://emberjs.com/guides/controllers)
*   [Views](https://emberjs.com/guides/views)
*   [Components](https://emberjs.com/guides/components/)
*   [Templates](https://emberjs.com/guides/templates/handlebars-basics)
*   [Helpers](https://emberjs.com/guides/templates/writing-helpers)

### Models

Suppose our application handles a collection of users. Well, those users and their informations would be the model. Think of them as the database data. Models may be retrieved and updated by implementing AJAX callbacks inside your routes, or you can rely on Ember-Data (a data-storage abstraction layer) to greatly simplify the retrieval, updating and persistence of models over a REST API.</p>

### The Router

There is the <code>Router</code>, and then there are routes. The <code>Router</code> is just a synopsis of all of your routes. Routes are the URL representations of your application’s objects (for example, a route’s <code>posts</code> will render a collections of posts). The goal of routes is to query the model, from their <code>model</code> hook, to make it available in the controller and in the template. Routes can also be used to set properties in controllers, to execute events and actions, and to connect a particular template to a particular controller. Last but not least, the <code>model</code> hook can return promises so that you can implement a <code>LoadingRoute</code>, which will wait for the model to resolve asynchronously over the network.</p>

### Controllers

At first, a <code>controller</code> gets a model from a <code>route</code>. Then, it makes the bridge between the model and the view or template. Let’s say you need a convenient method or function for switching between editing mode to normal mode. A method such as <code>goIntoEditMode()</code> and <code>closeEditMode()</code> would be perfect, and that’s exactly what controllers can be used for.

Controllers are auto-generated by Ember.js if you don’t declare them. For example, you can create a <code>user</code> template with a <code>UserRoute</code>; and, if you don’t create a <code>UserController</code> (because you have nothing special to do with it), then Ember.js will generate one for you internally (in memory). The <a href="https://chrome.google.com/webstore/detail/ember-inspector/bmdblncegkenkacieihfhpjfppoconhi">Ember Inspector</a> extension for Chrome can help you track those magic controllers.</p>

### Views

Views represent particular parts of your application (the visual parts that the user can see in the browser). A <code>View</code> is associated with a <code>Controller</code>, a Handlebars <code>template</code> and a <code>Route</code>. The difference between views and templates can be tricky. You will find yourself dealing with views when you want to handle events or handle some custom interactions that are impossible to manage from templates. They have a very convenient <code>didInsertElement</code> hook, through which you can play with jQuery very easily. Furthermore, they become extremely useful when you need to build reusable views, such as modals, popovers, date-pickers and autocomplete fields.</p>

### Components

A <code>Component</code> is a completely isolated <code>View</code> that has no access to the surrounding context. It’s a great way to build reusable components for your apps. A <a href="https://jsbin.com/OMOgUzo/1/edit?html,js,output">Twitter Button</a>, a custom <a href="https://pixelhandler.com/posts/create-a-custom-select-box-using-ember-component">select box</a> and those <a href="https://jsbin.com/odosoy/132/edit?html,js,output">reusable charts</a> are all great examples of components. In fact, they’re such a great idea that the W3C is actually working with the Ember team on a <a href="https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/custom/index.html">custom element</a> specification.</p>

### Templates

Simply put, a template is the view’s HTML markup. It prints the model data and automatically updates itself when the model changes. Ember.js uses <a href="https://handlebarsjs.com">Handlebars</a>, a lightweight templating engine also maintained by the Ember team. It has the usual templating logic, like <code>if</code> and <code>else</code>, loops and formatting <code>helpers</code>, that kind of stuff. Templates may be precompiled (if you want to cleanly organize them as separate <code>.hbs</code> or <code>.handlebars</code> files) or directly written in <code>&lt;script type="text/x-handlebars"&gt;&lt;/script&gt;</code> tags in your HTML page. Jump to the section on <a href="#what_is_handlebars_template_precompiling">templates precompiling</a> to dig into the subject.</p>

### Helpers

Handlebars helpers are functions that modify data before it is rendered on the screen — for example, to format dates better than <code>Mon Jul 29 2013 13:37:39 GMT+0200 (CEST)</code>. In your template, the date could be written as <code>{{date}}</code>. Let’s say you have a <code>formatDate</code> helper (which converts dates into something more elegant, like “One month ago” or “29 July 2013”). In this case, you could use it like so: <code>{{formatDate date}}</code>.</p>

### Components? Helpers? Views? HELP!

The Ember.js forum <a href="https://discuss.emberjs.com/t/whats-the-difference-between-ember-helpers-components-and-views/2201/2">has an answer</a> and StackOverflow <a href="https://stackoverflow.com/questions/18593424/views-vs-components-in-ember-js">has a response</a> that should alleviate your headache.</p>

## Let’s Build An App

In this section, we’ll build a real app, a simple interface for managing a group of users (a <a href="https://en.wikipedia.org/wiki/Create,_read,_update_and_delete">CRUD</a> app). Here’s what we’ll do:

*   look at the architecture we’re aiming for;
*   get you started with the dependencies, files structure, etc.;
*   set up the model with Ember-Data’s `FixtureAdapter`;
*   see how routes, controllers, views and templates interact with each other;
*   finally, replace the `FixtureAdapter` with the `LSAdapter` to persist data in the browser’s local storage.</p>

### Sketch Our App

We need a basic view to render a group of users (see 1 below). We need a single-user view to see its data (2). We need to be able to edit and delete a given user’s data (3). Finally, we need a way to create a new user; for this, we will reuse the edit form.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f0b0bee-babd-4c71-9b0a-380209311c7c/app-sketch.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f0b0bee-babd-4c71-9b0a-380209311c7c/app-sketch.png" alt="app-sketch" width="800" height="560" /></a></figure>

Ember.js strongly relies on naming conventions. So, if you want the page <code>/foo</code> in your app, you will have the following:

*   a `foo` template,
*   a `FooRoute`,
*   a `FooController`,
*   and a `FooView`.

Learn more about <a href="https://emberjs.com/guides/concepts/naming-conventions">Ember’s naming conventions</a> in the guides.</p>

### What You’ll Need to Get Started

You will need:

*   jQuery,
*   Ember.js itself (obviously),
*   Handlebars (i.e. Ember’s templating engine),
*   Ember-Data (i.e. Ember’s data-persistence abstraction layer).</p>

<pre><code class="language-markup">
/* /index.html
*/
 …
 &lt;script src="//code.jquery.com/jquery-2.0.3.min.js"&gt;&lt;/script&gt;
 &lt;script src="//builds.emberjs.com/handlebars-1.0.0.js"&gt;&lt;/script&gt;
 &lt;script src="//builds.emberjs.com/tags/v1.1.2/ember.js"&gt;&lt;/script&gt;
 &lt;script src="//builds.emberjs.com/tags/v1.0.0-beta.3/ember-data.js"&gt;&lt;/script&gt;
 &lt;script&gt;
   // your code
 &lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

Ember’s website has a <a href="https://emberjs.com/builds">builds section</a>, where you can find all of the links for Ember JS and Ember-Data. Currently, Handlebars is not there; you will find it on the <a href="https://handlebarsjs.com">official Handlebars</a> website.

Once we have loaded the required dependencies, we can get started building our app. First, we create a file named <code>app.js</code>, and then we initialize Ember:

<pre><code class="language-javascript">
/* /app.js
*/
window.App = Ember.Application.create();
</code></pre>

Just to be sure everything is OK, you should see Ember’s debugging logs in the browser’s console.</p>

<figure><img loading="lazy" decoding="async" class="128627" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/660e4258-bc3c-4720-9516-435be849972a/console-log-1.png" alt="console-log-1" width="500" height="271" /></figure>

### Our Files Directory Structure

There’s not much of a convention on how to organize files and folders. The <a href="https://github.com/stefanpenner/ember-app-kit">Ember App Kit</a> (a Grunt-based environment to scaffold Ember apps) provides a kind of standard for this because it is maintained by the Ember team. Even simpler, you could put everything in a single <code>app.js</code> file. In the end, it’s really up to you.

For this tutorial, we will simply put controllers in a <code>controllers</code> folder, views in a <code>views</code> folder and so on.</p>

<pre><code class="language-markup">
components/
controllers/
helpers/
models/
routes/
templates/
views/
app.js
router.js
store.js
</code></pre>

### Precompile Templates or Not?

There are two ways to declare templates. The easiest way is to add special <code>script</code> tags to your <code>index.html</code> file.</p>

<pre><code class="language-markup">
&lt;script type="text/x-handlebars" id="templatename"&gt;
  &lt;div&gt;I'm a template&lt;/div&gt;
&lt;/script&gt;
</code></pre>

Each time you need a template, you’d add another script tag for it. It’s fast and easy but can become a real mess if you have too many templates.

The other way is to create an <code>.hbs</code> (or <code>.handlebars</code>) file for each of your templates. This is called “template precompiling,” and a <a href="#what_is_handlebars_template_precompiling">complete section</a> is dedicated to it later in this article.

Our <a href="https://jkneb.github.io/ember-crud/unstyled">unstyled demo</a> uses <code>&lt;script type="text/x-handlebars"&gt;</code> tags, and all of the templates for our <a href="https://jkneb.github.io/ember-crud">enhanced demo</a> are stored in <code>.hbs</code> files, which are precompiled with a <a href="https://gruntjs.com">Grunt</a> task. This way, you can compare the two techniques.</p>

### Set Up the Model With Ember-Data’s FixtureAdapter

Ember-Data is a library that lets you retrieve records from a server, hold them in a <code>Store</code>, update them in the browser and, finally, save them back to the server. The <code>Store</code> can be configured with various adapters (for example, the <code>RESTAdapter</code> interacts with a JSON API, and the <code>LSAdapter</code> persists your data in the browser’s local storage). An <a href="#what_is_ember_data">entire section</a> is dedicated to Ember-Data later in this article.

Here, we are going to use the <code>FixtureAdapter</code>. So, let’s instantiate it:

<pre><code class="language-javascript">
/* /store.js
*/
App.ApplicationAdapter = DS.FixtureAdapter;
</code></pre>

In previous versions of Ember, you had to subclass the <code>DS.Store</code>. We don’t need to do that anymore to instantiate adapters.

The <code>FixtureAdapter</code> is a great way to start with Ember JS and Ember-Data. It lets you work with sample data in the development stage. At the end, we will switch to the <a href="https://github.com/rpflorence/ember-localstorage-adapter">LocalStorage adapter</a> (or <code>LSAdapter</code>).

Let’s define our model. A user would have a <code>name</code>, an <code>email</code> address, a short <code>bio</code>, an <code>avatarUrl</code> and a <code>creationDate</code>.</p>

<pre><code class="language-javascript">
/* /models/user.js
*/
App.User = DS.Model.extend({
  name         : DS.attr(),
  email        : DS.attr(),
  bio          : DS.attr(),
  avatarUrl    : DS.attr(),
  creationDate : DS.attr()
});
</code></pre>

Now, let’s feed our <code>Store</code> with the sample data. Feel free to add as many users as you need:

<pre><code class="language-javascript">
/* /models/user.js
*/
App.User.FIXTURES = [{
  id: 1,
  name: 'Sponge Bob',
  email: 'bob@sponge.com',
  bio: 'Lorem ispum dolor sit amet in voluptate fugiat nulla pariatur.',
  avatarUrl: 'https://jkneb.github.io/ember-crud/assets/images/avatars/sb.jpg',
  creationDate: 'Mon, 26 Aug 2013 20:23:43 GMT'
}, {
  id: 2,
  name: 'John David',
  email: 'john@david.com',
  bio: 'Lorem ispum dolor sit amet in voluptate fugiat nulla pariatur.',
  avatarUrl: 'https://jkneb.github.io/ember-crud/assets/images/avatars/jk.jpg',
  creationDate: 'Fri, 07 Aug 2013 10:10:10 GMT'
}
…
];
</code></pre>

Learn more about <a href="https://emberjs.com/guides/models/">models in the documentation</a>.</p>

### Instantiate the Router

Let’s define our <code>Router</code> with the routes we want (based on the <a href="#sketch_our_app">diagram we made earlier</a>).</p>

<pre><code class="language-javascript">
/* /router.js
*/
App.Router.map(function(){
  this.resource('users', function(){
    this.resource('user', { path:'/:user_id' }, function(){
      this.route('edit');
    });
    this.route('create');
  });
});
</code></pre>

This <code>Router</code> will generate exactly this:
<table class="tablesaw break-out" data-tablesaw-mode="swipe" data-tablesaw-minimap>
<tbody>
<tr>
<th>URL</th>
<th>Route Name</th>
<th>Controller</th>
<th>Route</th>
<th>Template</th>
</tr>
<tr>
<td>N/A</td>
<td>N/A</td>
<td><code>ApplicationController</code></td>
<td><code>ApplicationRoute</code></td>
<td><code>application</code></td>
</tr>
<tr>
<td><code>/</code></td>
<td><code>index</code></td>
<td><code>IndexController</code></td>
<td><code>IndexRoute</code></td>
<td><code>index</code></td>
</tr>
<tr>
<td>N/A</td>
<td><code>users</code></td>
<td><code>UsersController</code></td>
<td><code>UsersRoute</code></td>
<td><code>users</code></td>
</tr>
<tr>
<td><code>/users</code></td>
<td><code>users.index</code></td>
<td><code>UsersIndexController</code></td>
<td><code>UsersIndexRoute</code></td>
<td><code>users/index</code></td>
</tr>
<tr>
<td>N/A</td>
<td><code>user</code></td>
<td><code>UserController</code></td>
<td><code>UserRoute</code></td>
<td><code>user</code></td>
</tr>
<tr>
<td><code>/users/:user_id</code></td>
<td><code>user.index</code></td>
<td><code>UserIndexController</code></td>
<td><code>UserIndexRoute</code></td>
<td><code>user/index</code></td>
</tr>
<tr>
<td><code>/users/:user_id/edit</code></td>
<td><code>user.edit</code></td>
<td><code>UserEditController</code></td>
<td><code>UserEditRoute</code></td>
<td><code>user/edit</code></td>
</tr>
<tr>
<td><code>/users/create</code></td>
<td><code>users.create</code></td>
<td><code>UsersCreateController</code></td>
<td><code>UsersCreateRoute</code></td>
<td><code>users/create</code></td>
</tr>
</tbody>
</table>

The <code>:user_id</code> part is called a dynamic segment because the corresponding user ID will be injected into the URL. So, it will look like <code>/users/3/edit</code>, where <code>3</code> is the user with the ID of 3.

You can define either a <code>route</code> or a <code>resource</code>. Keep in mind that a <code>resource</code> is a group of routes and that it allows routes to be nested.

A <code>resource</code> also resets the nested naming convention to the last resource name, which means that, instead of having <code>UsersUserEditRoute</code>, you would have <code>UserEditRoute</code>. In other words, in case this confuses you, if you have a resource nested inside another resource, then your files name would be:

*   `UserEditRoute` instead of `UsersUserEditRoute`;
*   `UserEditControler` instead of `UsersUserEditController`;
*   `UserEditView` instead of `UsersUserEditView`;
*   for templates, `user/edit` instead of `users/user/edit`.

Learn more about <a href="https://emberjs.com/guides/routing/defining-your-routes">how to define routes</a> in the guides.</p>

### The Application Template

Each Ember JS app needs an <code>Application</code> template, with an <code>{{outlet}}</code> tag that holds all other templates.</p>

<pre><code class="language-markup">
/* /templates/application.hbs
*/
&lt;div class="main"&gt;
  &lt;h1&gt;Hello World&lt;/h1&gt;
  {{outlet}}
&lt;/div&gt;
</code></pre>

If you’ve decided to follow this tutorial without precompiling templates, here’s what your <code>index.html</code> should look like:

<pre><code class="language-markup">
/* /index.html
*/
  …
  &lt;script type="text/x-handlebars" id="application"&gt;
    &lt;div class="main"&gt;
      &lt;h1&gt;Hello World&lt;/h1&gt;
      {{outlet}}
    &lt;/div&gt;
  &lt;/script&gt;

  &lt;script src="dependencies.js"&gt;&lt;/script&gt;
  &lt;script src="your-app.js"&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

### The Users Route

This route deals with our group of users. Remember we saw <a href="#router">earlier</a>, in the definitions, that a route is responsible for querying the model. Well, routes have a <code>model</code> hook through which you can perform AJAX requests (for retrieving your models, if you don’t use Ember-Data) or for querying your <code>Store</code> (if you do use Ember-Data). If you’re interested in retrieving models without Ember-Data, you can <a href="#what_about_not_using_emberdata">jump to the section</a> in which I briefly explain how to do it.

Now, let’s create our <code>UsersRoute</code>:

<pre><code class="language-javascript">
/* /routes/usersRoute.js
*/
App.UsersRoute = Ember.Route.extend({
  model: function(){
    return this.store.find('user');
  }
});
</code></pre>

Learn more about <a href="https://emberjs.com/guides/routing/specifying-a-routes-model">how to specify the routes <code>model</code> hook</a> in the guides.

If you visit your app at the URL <code>https://localhost/#/users</code>, nothing will happen, because we need a <code>users</code> template. Here it is:

<pre><code class="language-markup">
/* /templates/users.hbs
*/
&lt;ul class="users-listing"&gt;
  {{#each user in controller}}
    &lt;li&gt;{{user.name}}&lt;/li&gt;
  {{else}}
    &lt;li&gt;no users… :-(&lt;/li&gt;
  {{/each}}
&lt;/ul&gt;
</code></pre>

The <code>each</code> loop iterates over the users collection; here, <code>controller</code> equals <code>UsersController</code>. Notice that the <code>{{#each}}</code> loop has an <code>{{else}}</code> statement; so, if the model is empty, then <code>no users… :-(</code> will be printed.

Because we’ve followed Ember’s naming conventions, we can omit the declaration of the <code>UsersController</code>. Ember will guess that we are dealing with a collection because we’ve used the plural of “user.”

### Object vs. Array Controller

An <code>ObjectController</code> deals with a single object, and an <code>ArrayController</code> deals with multiple objects (such as a collection). We just saw that, in our case, we don’t need to declare the <code>ArrayController</code>. But for the purpose of this tutorial, let’s declare it, so that we can set some sorting properties on it:

<pre><code class="language-javascript">
/* /controllers/usersController.js
*/
App.UsersController = Ember.ArrayController.extend({
  sortProperties: ['name'],
  sortAscending: true // false = descending
});
</code></pre>

Here, we’ve simply sorted our users alphabetically. Learn more about <a href="https://emberjs.com/guides/controllers/">controllers in the guides</a>.</p>

### Displaying the Number of Users

Let’s use <code>UsersController</code> to create our first <a href="https://emberjs.com/guides/object-model/computed-properties/">computed property</a>. This will display the number of users, so that we can see changes when adding or deleting users.

In the template, we just need something as simple as this:

<pre><code class="language-javascript">
/* /templates/users.hbs
*/
…
&lt;div&gt;Users: {{usersCount}}&lt;/div&gt;
…
</code></pre>

In <code>UsersController</code>, let’s declare the <code>usersCount</code> property — but not like a regular property, because this one will be a function that returns the model’s length.</p>

<pre><code class="language-javascript">
/* /controllers/usersController.js
*/
App.UsersController = Em.ArrayController.extend({
  …
  usersCount: function(){
    return this.get('model.length');
  }.property('@each')
});
</code></pre>

Basically, <code>usersCount</code> takes the <code>.property('@each')</code> method, which tells Ember.js that this function is in fact a property that is watching for any changes to one of the models in the collection (i.e. the users). Later, we will see <code>usersCount</code> incrementing and decrementing as we create and delete users.</p>

### Computed Properties

Computed properties are powerful. They let you declare functions as properties. Let’s see how they work.</p>

<pre><code class="language-javascript">
App.Person = Ember.Object.extend({
  firstName: null,
  lastName: null,

  fullName: function() {
    return this.get('firstName') + ' ' + this.get('lastName');
  }.property('firstName', 'lastName')
});

var ironMan = App.Person.create({
  firstName: "Tony",
  lastName:  "Stark"
});

ironMan.get('fullName') // "Tony Stark"
</code></pre>

In this example, the <code>Person</code> object has two static properties, which are <code>firstName</code> and <code>lastName</code>. It also has a <code>fullName</code> computed property, which concatenates a full name by retrieving the value of the two static properties. Note that the <code>.property('firstName', 'lastName')</code> method tells the function to re-execute if either <code>firsName</code> or <code>lastName</code> changes.

Properties (whether static or computed) are retrieved with <code>.get('property')</code> and can be set with <code>.set('property', newValue)</code>.

If you find yourself setting multiple properties consecutively, a better way to do it is with one single <code>.setProperties({})</code>, rather than with multiple instances of <code>.set()</code>. So, instead of doing this…

<pre><code class="language-javascript">
this.set('propertyA', 'valueA');
this.set('propertyB', valueB);
this.set('propertyC', 0);
this.set('propertyD', false);
</code></pre>

… you would do this:

<pre><code class="language-javascript">
this.setProperties({
  'propertyA': 'valueA',
  'propertyB': valueB,
  'propertyC': 0,
  'propertyD': false
});
</code></pre>

The documentation has so much more information about how to bind data with <a href="https://emberjs.com/guides/object-model/computed-properties/">computed properties</a>, <a href="https://emberjs.com/guides/object-model/observers">observers</a> and <a href="https://emberjs.com/guides/object-model/bindings">bindings</a>.</p>

### Redirecting From the Index Page

If you go to the home page of your app (<code>https://localhost/</code>), you might be asking yourself why nothing is happening. That’s because you are viewing the index page, and we don’t have an <code>index</code> template. Let’s add one, then. We’ll call it <code>index.hbs</code>.

Ember.js will notice that you are creating the <code>index</code> template for <code>IndexRoute</code>; so, no need to tell it anything else about the index in the <code>Router</code>. This is called an initial route. Three of them are available: <code>ApplicationRoute</code>, <code>IndexRoute</code> and <code>LoadingRoute</code>. Learn more about them <a href="https://emberjs.com/guides/routing/defining-your-routes/#toc_initial-routes">in the guides</a>.

Now, let’s add a link to the user’s page with the <code>{{#link-to}}…{{/link-to}}</code> block helper. Why a block helper? Because you’re able to write text between the opening and closing tags, as if it were a real custom HTML element.</p>

<pre><code class="language-markup">
/* /templates/index.hbs
*/
{{#link-to "users"}} Go to the users page {{/link-to}}
</code></pre>

This takes the route’s name that you want to link to as the first argument (the second optional argument is a model). Under the hood, it’s just a regular <code>&lt;a&gt;</code> element, although Ember also handles for us the <code>active</code> class name when reaching the matching route. Those <code>link-to</code>’s are perfect for navigation menus. Learn more about them <a href="https://emberjs.com/guides/templates/links">in the guides</a>.

Another approach would be to tell <code>IndexRoute</code> to redirect to <code>UsersRoute</code>. Again, pretty easy:

<pre><code class="language-javascript">
/* /routes/indexRoute.js
*/
App.IndexRoute = Ember.Route.extend({
  redirect: function(){
    this.transitionTo('users');
  }
});
</code></pre>

Now, when you visit the home page, you will immediately be redirected to the <code>/#/users</code> URL.</p>

### Single User Route

Before getting our hands dirty with building the dynamic segment, we need a way to link to each user from the <code>users</code> template. Let’s use the <code>{{#link-to}}</code> block helper inside the user’s <code>each</code> loop.</p>

<pre><code class="language-markup">
/* /templates/users.hbs
*/
…
{{#each user in controller}}
  &lt;li&gt;
    {{#link-to "user" user}}
      {{user.name}}
    {{/link-to}}
  &lt;/li&gt;
{{/each}}
</code></pre>

The second argument of <code>link-to</code> is the model that will be passed to <code>UserRoute</code>.

OK, let’s get back to our single user template. It looks like this:

<pre><code class="language-markup">
/* /templates/user.hbs
*/
&lt;div class="user-profile"&gt;
  &lt;img {{bind-attr src="avatarUrl"}} alt="User's avatar" /&gt;
  &lt;h2&gt;{{name}}&lt;/h2&gt;
  &lt;span&gt;{{email}}&lt;/span&gt;
  &lt;p&gt;{{bio}}&lt;/p&gt;
  &lt;span&gt;Created {{creationDate}}&lt;/span&gt;
&lt;/div&gt;
</code></pre>

Note that you can’t use <code>&lt;img src="{{avatarUrl}}"&gt;</code>, because data inside attributes are bound with the <code>bind-attr</code> helper. For instance, you could do something like <code>&lt;img {{bind-attr height="imgHeight}}"/&gt;</code>, where <code>imgHeight</code> is a computed property in the current controller.

You’ll find all you need to know about binding <a href="https://emberjs.com/guides/templates/binding-element-attributes/">attributes</a> and <a href="https://emberjs.com/guides/templates/binding-element-class-names/">class names</a> in the guides.

So far, so good. But nothing happens when you click on the user’s links, because we told the <code>Router</code> that we want <code>UserRoute</code> to be nested in <code>UsersRoute</code>. So, we need an <code>{{outlet}}</code> in which to render the user template.</p>

<pre><code class="language-markup">
/* /templates/users.hbs
*/
…
{{#each user in controller}}
…
{{/each}}

{{outlet}}
</code></pre>

An <code>{{outlet}}</code> is like a dynamic placeholder into which other templates can be injected when <code>{{#link-to}}</code> tags are clicked. It allows for views to be nested.

Now, you should be able to view the user template injected in the page when visiting the page at the URL <code>/#/users/1</code>.

Hey, wait a minute! We have declared neither <code>UserRoute</code> nor <code>UserController</code>, but it’s still working! Why is that? Well, <code>UserRoute</code> is the singular of <code>UsersRoute</code>, so Ember has generated the route and the controller for us (in memory). Thank goodness for naming conventions!

For the sake of consistency, let’s declare them anyway, so that we can see how they look:

<pre><code class="language-javascript">
/* /routes/userRoute.js
*/
App.UserRoute = Ember.Route.extend({
  model: function(params) {
    return this.store.find('user', params.user_id);
  }
});
</code></pre>

<pre><code class="language-javascript">
/* /controllers/userController.js
*/
App.UserController = Ember.ObjectController.extend();
</code></pre>

Learn more about <a href="https://emberjs.com/guides/routing/specifying-a-routes-model/#toc_dynamic-models">dynamic segments</a> in the guides.</p>

### Edit a User

Moving on to the edit user form nested in the single user, the template looks like this:

<pre><code class="language-markup">
/* /templates/user/edit.hbs
*/
&lt;div class="user-edit"&gt;
  &lt;label&gt;Choose user avatar&lt;/label&gt;
  {{input value=avatarUrl}}

  &lt;label&gt;User name&lt;/label&gt;
  {{input value=name}}

  &lt;label&gt;User email&lt;/label&gt;
  {{input value=email}}

  &lt;label&gt;User short bio&lt;/label&gt;
  {{textarea value=bio}}
&lt;/div&gt;
</code></pre>

Let’s talk about those <code>{{input}}</code> and <code>{{textarea}}</code> tags. This form’s goal is to enable us to edit the user’s data, and these custom <code>input</code> tags take the model’s properties as parameters to enable data-binding.

Note that it’s <code>value=model</code>, without the <code>" "</code>. The <code>{{input}}</code> helper is a shorthand for <code>{{Ember.TextField}}</code>. Ember.js has those <a href="https://emberjs.com/guides/views/built-in-views">built-in views</a> especially for form elements.

If you visit your app at the URL <code>/#/users/1/edit</code>, nothing will happen, because, again, we need an <code>{{outlet}}</code> to nest the edit template into the single user template.</p>

<pre><code class="language-markup">
/* /templates/user.hbs
*/
…
{{outlet}}
</code></pre>

Now, the template is correctly injected in the page. But the fields are still empty, because we need to tell the route which model to use.</p>

<pre><code class="language-javascript">
/* /routes/userEditRoute.js
*/
App.UserEditRoute = Ember.Route.extend({
  model: function(){
    return this.modelFor('user');
  }
});
</code></pre>

The <code><a href="https://emberjs.com/api/classes/Ember.Route.html#method_modelFor">modelFor</a></code> method lets you use the model of another route. Here, we’ve told <code>UserEditRoute</code> to get the model of <code>UserRoute</code>. The fields are now correctly populated with the model data. Try to edit them — you will see the changes occur in the parent templates as well!

### Our First Action

OK, now we need a button to click that redirects us from <code>UserRoute</code> to <code>UserEditRoute</code>.</p>

<pre><code class="language-markup">
/* /templates/user.hbs
*/
&lt;div class="user-profile"&gt;
  &lt;button {{action "edit"}}&gt;Edit&lt;/button&gt;
  …
</code></pre>

We just added a simple <code>button</code> that triggers our first <code>{{action}}</code>. Actions are events that trigger associated methods in their current controller. If no method is found in the controller, then the action bubbles up through routes until it matches something. This is explained well <a href="https://emberjs.com/guides/templates/actions/#toc_action-bubbling">in the guides</a>.

In other words, if we <code>click</code> on the <code>button</code>, then it will trigger the <code>edit</code> action found in the controller. So, let’s add it to <code>UserController</code>:

<pre><code class="language-javascript">
/* /controllers/userController.js
*/
App.UserController = Ember.ObjectController.extend({
  actions: {
    edit: function(){
      this.transitionToRoute('user.edit');
    }
  }
});
</code></pre>

Actions, whether in controllers or in routes, are stored in an <code>actions</code> hash. But this is not the case for default actions, such as <code>click</code>, <code>doubleClick</code>, <code>mouseLeave</code> and <code>dragStart</code>. The Ember.js website has a <a href="https://emberjs.com/api/classes/Ember.View.html#toc_event-names">complete list</a>.

Here, basically, our <code>edit</code> action says, “Go to the <code>user.edit</code> route.” That’s pretty much it.</p>

### TransitionTo or TransitionToRoute?

On a side note, transitioning from routes is slightly different from transitioning from controllers:

<pre><code class="language-javascript">
// from a route
this.transitionTo('your.route')
// from a controller
this.transitionToRoute('your.route')
</code></pre>

### Saving User Modifications

Let’s see how to save modifications after a user’s data has been edited. By saving, we mean persisting the changes. With Ember-Data, this means telling <code>Store</code> to <code>save()</code> the new <code>record</code> of the modified user. The <code>Store</code> will then tell the <code>adapter</code> to perform an AJAX PUT request (if our adapter is the <code>RESTAdapter</code>).

From our application’s point of view, this would be an “OK” <code>button</code> that saves modifications and then transitions to the parent route. Again, we’ll use an <code>{{action}}</code>.</p>

<pre><code class="language-javascript">
/* /templates/user/edit.hbs
*/
&lt;button {{action "save"}}&gt; ok &lt;/button&gt;
</code></pre>

<pre><code class="language-javascript">
/* /controllers/userEditController.js
*/
App.UserEditController = Ember.ObjectController.extend({
  actions: {
    save: function(){
      var user = this.get('model');
      // this will tell Ember-Data to save/persist the new record
      user.save();
      // then transition to the current user
      this.transitionToRoute('user', user);
    }
  }
});
</code></pre>

Our edit mode is working well. Now, let’s see how to delete a user.</p>

### Delete a User

We can add a delete <code>button</code> beside the edit button in the <code>user</code> template — again, with a <code>delete</code> <code>{{action}}</code>, this time defined in <code>UserController</code>.</p>

<pre><code class="language-javascript">
/* /templates/user.hbs
*/
&lt;button {{action "delete"}}&gt;Delete&lt;/button&gt;
</code></pre>

<pre><code class="language-javascript">
/* /controllers/userController.js
*/
…
actions: {
  delete: function(){
    // this tells Ember-Data to delete the current user
    this.get('model').deleteRecord();
    this.get('model').save();
    // then transition to the users route
    this.transitionToRoute('users');
  }
}
</code></pre>

Now, when you click on the “Delete” button, the <code>user</code> is instantly trashed. A bit rough. We should add a confirm state, something like “Are you sure?” with “Yes” and “No” buttons. To do this, we need to change <code>{{action "delete"}}</code> to make it show <code>confirm-box</code> instead of immediately deleting the user. Then, we obviously need to put <code>confirm-box</code> in the user template.</p>

<pre><code class="language-javascript">
/* /templates/user.hbs
*/
{{#if deleteMode}}
&lt;div class="confirm-box"&gt;
  &lt;h4&gt;Really?&lt;/h4&gt;
  &lt;button {{action "confirmDelete"}}&gt; yes &lt;/button&gt;
  &lt;button {{action "cancelDelete"}}&gt; no &lt;/button&gt;
&lt;/div&gt;
{{/if}}
</code></pre>

We’ve just written our first Handlebars <code>{{if}}</code> statement. It prints <code>div.confirm-box</code> only if the <code>deleteMode</code> property is <code>true</code>. We need to define this <code>deleteMode</code> in the current controller and then change the <code>delete</code> action to make it toggle <code>deleteMode</code>’s value to <code>true</code> or <code>false</code>. Now, our <code>UserController</code> looks like this:

<pre><code class="language-javascript">
/* /controllers/userController.js
*/
App.UserController = Ember.ObjectController.extend({
  // the deleteMode property is false by default
  deleteMode: false,

  actions: {
    delete: function(){
      // our delete method now only toggles deleteMode's value
      this.toggleProperty('deleteMode');
    },
    cancelDelete: function(){
      // set deleteMode back to false
      this.set('deleteMode', false);
    },
    confirmDelete: function(){
      // this tells Ember-Data to delete the current user
      this.get('model').deleteRecord();
      this.get('model').save();
      // and then go to the users route
      this.transitionToRoute('users');
      // set deleteMode back to false
      this.set('deleteMode', false);
    },
    // the edit method remains the same
    edit: function(){
      this.transitionToRoute('user.edit');
    }
  }
});
</code></pre>

Deletion now works perfectly with the “Yes” and “No” buttons. Awesome! Finally, the last thing to build is the create route.</p>

### Create a User

To create a user, let’s do something fun: Let’s reuse the edit template, because the create form will be exactly the same as the edit user form. First, we declare the create route, which will return an empty object in its <code>model</code> hook:

<pre><code class="language-javascript">
/* /routes/usersCreateRoute.js
*/
App.UsersCreateRoute = Ember.Route.extend({
  model: function(){
    // the model for this route is a new empty Ember.Object
    return Em.Object.create({});
  },

  // in this case (the create route), we can reuse the user/edit template
  // associated with the usersCreateController
  renderTemplate: function(){
    this.render('user.edit', {
      controller: 'usersCreate'
    });
  }
});
</code></pre>

Note the <code>renderTemplate</code> method; it enables us to associate a particular template with a route. Here, we’re telling <code>UsersCreateRoute</code> to use the user and edit template with <code>UsersCreateController</code>. Learn more about renderTemplate <a href="https://emberjs.com/guides/routing/rendering-a-template/">in the guides</a>.

Now, let’s define another <code>save</code> action, but this time in <code>UsersCreateController</code>. (Remember that an <code>action</code> first tries to match a corresponding method in the <em>current</em> controller.)

<pre><code class="language-javascript">
/* /controllers/usersCreateController.js
*/
App.UsersCreateController = Ember.ObjectController.extend({
  actions: {
    save: function(){
      // just before saving, we set the creationDate
      this.get('model').set('creationDate', new Date());

      // create a record and save it to the store
      var newUser = this.store.createRecord('user', this.get('model'));
      newUser.save();

      // redirects to the user itself
      this.transitionToRoute('user', newUser);
    }
  }
});
</code></pre>

Finally, let’s add the <code>{{#link-to}}</code> helper in the users templates, so that we can access the creation form:

<pre><code class="language-javascript">
/* /templates/users.hbs
*/
{{#link-to "users.create" class="create-btn"}} Add user {{/link-to}}
…
</code></pre>

That’s all there is to creating users!

### Format Data With Helpers

We’ve <a href="#helpers">already defined</a> what <code>helpers</code> are. Now, let’s see how to create one that will format an ugly date into a nice clean formatted one. The <a href="https://momentjs.com">Moment.js</a> library is awesome for this purpose.

Grab <a href="https://momentjs.com">Moment.js</a> and load it in the page. Then, we’ll define our first helper:

<pre><code class="language-javascript">
/* /helpers/helpers.js
*/
Ember.Handlebars.helper('formatDate', function(date){
  return moment(date).fromNow();
});
</code></pre>

Modify the user template so that it uses the <code>formatDate</code> helper on the <code>{{creationDate}}</code> property:

<pre><code class="language-javascript">
/* /templates/user.hbs
*/
…
&lt;span&gt;Created {{formatDate creationDate}}&lt;/span&gt;
…
</code></pre>

That’s it! You should see the dates nicely formatted: “2 days ago,” “One month ago,” etc.</p>

### Format Data With Bound Helpers

In this case, our date is static data because it’s not going to change in the future. But if you have data that needs to be updated (for example, a formatted price), then you would have to use a <code>BoundHelper</code> instead of the regular helper.</p>

<pre><code class="language-javascript">
/* /helpers/helpers.js
*/
Ember.Handlebars.registerBoundHelper('formatDate', function(date){
  return moment(date).fromNow();
});
</code></pre>

A bound helper is able to automatically update itself if the data changes. Learn more about bound helpers in the guides.</p>

### Switch to the LocalStorage Adapter

Our app looks to be working fine, so we are ready to switch to the real thing. We could enable the <code>RESTAdapter</code>, but then we would need a REST server on which we could perform GET, PUT, POST and DELETE requests. Instead, let’s use <code>LSAdapter</code>, a third-party adapter that you can <span class="removed_link" title="https://github.com/rpflorence/ember-localstorage-adapter/blob/master/localstorage_adapter.js">download on GitHub</span>. Load it in your page (just after Ember-Data), comment out all of the <code>FIXTURE</code> data, and change <code>ApplicationAdapter</code> to <code>DS.LSAdapter</code>:

<pre><code class="language-javascript">
/* /store.js
*/
App.ApplicationAdapter = DS.LSAdapter;
</code></pre>

Now, your users’ data will persist in local storage. That’s all! Seriously, it’s that easy. Just to be sure, open the Developer Tools in your browser and go into the “Resource” panel. In the “Local Storage” tab, you should find an entry for <code>LSAdapter</code> with all of your users’ data.</p>

<figure><img loading="lazy" decoding="async" class="128812" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d93c04ac-b204-4226-90cd-16205421c849/console-localstorage.png" alt="console-localstorage" width="500" height="271" /></figure>

## Playing With Views

So far, we haven’t declared any views in our simple CRUD, only templates. Why would we care about views? Well, they are powerful for events handling, animations and reusable components.</p>

### jQuery and the didInsertElement

How can we use jQuery the way we are used to for Ember.js’ views? Each view and component has a <code>didInsertElement</code> hook, which assures us that the view has indeed been inserted into the DOM. With that, you have secure jQuery access to elements in the page.</p>

<pre><code class="language-javascript">
App.MyAwesomeComponent = Em.Component.extend({
  didInsertElement: function(){
    // this = the view
    // this.$() = $(the view)
    this.$().on('click', '.child .elem', function(){
      // do stuff with jQuery
    });
  }
});
</code></pre>

If you’ve registered jQuery-like events from inside <code>didInsertElement</code>, then you can use <code>willDestroyElement</code> to clean them up after the view has been removed from the DOM, like so:

<pre><code class="language-javascript">
App.MyAwesomeComponent = Em.Component.extend({
  didInsertElement: function(){
    this.$().on('click', '.child .elem', function(){
      // do stuff with jQuery
    });
  },
  willDestroyElement: function(){
    this.$().off('click');
  }
});
</code></pre>

### Side Panel Components With className Bindings

The combination of computed property and <code>className</code> binding sounds like a scary technique, but it’s really not that bad. The idea is that we add or remove a CSS class on an element if a property is either <code>true</code> or <code>false</code>. Of course, the CSS class contains a CSS transition.

Suppose we have a hidden div in the DOM. When this div has a class of <code>opened</code>, it slides in. When it has a class of <code>closed</code>, it slides out. A side panel is a perfect example for this, so let’s build one.

Here’s a JS Bin so that you can test the code:

<a class="jsbin-embed" href="https://emberjs.jsbin.com/utimiZI/12/embed?js,output">Reusable Ember.js side panels</a>

Let’s go through each tab in turn:

*   **JavaScript tab**.  First, we declare our `SidePanelComponent` with default `classNames`. Then, `classNameBindings` is used to test whether `isOpen` is `true` or `false`, so that it returns `closed` or `opened`. Finally, `component` has a `toggleSidepanel` action that simply toggles the `isOpen` boolean.
*   **HTML tab**.  This is the side panel’s markup. Note the `{{#side-panel}}…{{/side-panel}}` block tags; we can put whatever we want between them, which makes our side panel incredibly reusable. The `btn-toggle` button calls the `toggleSidepanel` action located in the component. The `{{#if isOpen}}` adds some logic by checking the value of the `isOpen` property.
*   **CSS tab**.  Here, we are basically putting the side panel off screen. The `opened` class slides it in, and `closed` slides it out. The animation is possible because we are listening for `translate2D` changes (`transition:transform .3s ease`).

The guides have a lot more examples on how to bind class names <a href="https://emberjs.com/guides/components/customizing-a-components-element">from components</a> and <a href="https://emberjs.com/guides/templates/binding-element-class-names">from inside templates</a>.</p>

### Modals With Layout and Event Bubbling

This technique is way more complicated than the previous one, because a lot of Ember.js features are involved. The idea is to make an event bubble from a view to a route so that we can toggle a property located in a controller somewhere in the app. Also, here we are using a <code>View</code> instead of a <code>Component</code> (remember that, under the hood, a component is an isolated view).</p>

<a class="jsbin-embed" href="https://emberjs.jsbin.com/aKUWUF/8/embed?js,output">Reusable Ember.js modals</a>

*   **JavaScript tab**.  The `modalView` is the default `layout` for all of our modals. It has two methods, `showModal` and `hideModal`. The `showModal` method is called with an `action` that bubbles up, first through controller, then through routes, until it finds a corresponding `showModal` action. We’ve stored `showModal` in the highest route possible, the `applicationRoute`. Its only goal is to set the `modalVisible` property inside the controller that was passed in the `action`’s second argument. And yes, creating a property at the same time as we set it is possible.
*   **HTML tab**.  Each modal has its own template, and we’ve used the convenient `{{#view App.ModalView}}…{{/view}}` block tags to encapsulate them in `modal_layout`. The modal’s controllers are not even declared because Ember.js has them in memory. Note that the `{{render}}` helper takes parameters, which are the template’s name and a generated controller for this template. So, here we are calling a `modal01` template and a `modal01` controller (auto-generated).
*   **CSS tab**.  For the purpose of this example, modals need to be present in the DOM. This can feel like a constraint, but the main benefit is the reduced paint cost; otherwise, Ember has to inject and remove them every time we call them. The second benefit is CSS transitions. The `shown` class applies two transitions: first, the top position (because the modal is off screen by default), then, with a little delay, it transitions the opacity (which also has a [reduced](https://speakerdeck.com/ariya/fluid-user-interface-with-hardware-acceleration?slide=36) paint [cost](https://css-tricks.com/w3conf-ariya-hidayat-fluid-user-interface-with-hardware-acceleration) when transitioning). The `hidden` class does the same in reverse. Obviously, you can apply a [lot of cool transitions](https://tympanus.net/Development/ModalWindowEffects) to your modals if they stay in the DOM.

The guides have a lot more information about <a href="https://emberjs.com/guides/views/handling-events">events</a>, <a href="https://emberjs.com/guides/understanding-ember/the-view-layer/#toc_event-bubbling">event bubbling</a>, <a href="https://emberjs.com/guides/views/adding-layouts-to-views">layouts</a> and the <a href="https://emberjs.com/guides/templates/rendering-with-helpers/#toc_the-code-render-code-helper">{{render}}</a> helper tag.</p>

## What Is Ember-Data?

Ember-Data is in beta as of the time of writing, so please use it with caution.

It is a library that lets you retrieve records from a server, hold them in a store, update them in the browser and, finally, save them back to the server. The store may be configured with various adapters, depending on your back end. Here’s a diagram of Ember-Data’s architecture.</p>

<img class="128828 alignnone" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dd3d8a2e-a67a-4324-9123-621dce55503d/ember-data-sketch.png" alt="ember-data-sketch" width="500" height="600" />

### The Store

The store holds data loaded from the server (i.e. records). Routes and controllers can query the store for records. If a given record is called for the first time, then the store tells the adapter to load it over the network. Then, the store caches it for the next time you ask for it.</p>

### Adapters

The application queries the store, and the adapter queries the back end. Each adapter is made for a particular back end. For example, the <code>RESTAdapter</code> deals with JSON APIs, and <code>LSAdapter</code> deals with local storage.

The idea behind Ember-Data is that, if you have to change the back end, then you simply plug another adapter, without having to touch a single line of your application’s code.

*   `FixtureAdapter` `FixtureAdapter` is perfect for testing Ember and Ember-Data. Fixtures are just sample data that you can work with until your app reaches the production phase. We went over how to configure it in an [earlier part of this article](#set_up_the_model_with_ember_data_fixtureadapter).
*   `RESTAdapter` `RESTAdapter` is the default adapter in Ember-Data. It lets you perform GET, PUT, POST and DELETE requests over a REST API. It also requires some [specific JSON conventions](https://emberjs.com/guides/models/the-rest-adapter/#toc_json-conventions) in return. Enabling `RESTAdapter` looks like this:

        App.ApplicationAdapter = DS.RESTAdapter.extend({
          host: 'https://your.api.com'
        });

    There’s a lot more to discover about `RESTAdapter` [in the guides](https://emberjs.com/guides/models/the-rest-adapter).
*   **Custom adapter**.  You could use something other than the two default adapters (`FixtureAdapter` and `RESTAdapter`). A [bunch of them are on GitHub](https://github.com/search?q=ember+adapter&ref=reposearch). For instance, there’s the [LocalStorage Adapter](https://github.com/rpflorence/ember-localstorage-adapter), which is demonstrated in the guides’ sample [Todos](https://emberjs.com/guides/getting-started/using-other-adapters) app and is also the one I use in the [demo](https://jkneb.github.io/ember-crud).</p>

### What About Not Using Ember-Data?

In this article, I’ve chosen to cover Ember-Data because it’s almost stable and is probably one of the coolest thing happening these days in the JavaScript world. But perhaps you’re wondering whether getting rid of it is possible. The answer is yes! In fact, using Ember.js without Ember-Data is pretty easy.

There are two ways to do it.

You could use another library for your model’s retrieval and persistence. <a href="https://github.com/ebryn/ember-model">Ember-Model</a>, <a href="https://github.com/zendesk/ember-resource">Ember-Resource</a>, <a href="https://github.com/endlessinc/ember-restless">Ember-Restless</a> and the recent <span class="removed_link" title="https://epf.io/">EPF</span> are good alternatives. EmberWatch has written a great little article that sums up “<a href="https://blog.emberwatch.com/2013/06/19/alternatives-ember-data.html">Alternatives to Ember Data</a>.”

The other way would be to not rely on a library, in which case you would have to implement methods to retrieve models with AJAX calls. “<a href="https://eviltrout.com/2013/03/23/ember-without-data.html">Ember Without Ember Data</a>,” by Robin Ward (the guy behind <a href="https://www.discourse.org/">Discourse</a>), is a great read. “<a href="https://net.tutsplus.com/tutorials/javascript-ajax/getting-into-ember-js-part-3">Getting Into Ember.js, Part 3</a>” by Rey Bango on Nettuts+ deals specifically with models.

For instance, here’s a static method with <code>reopenClass</code> on a model:

<pre><code class="language-javascript">
/* /models/user.js
*/
// our own findStuff method inside the User model
App.User.reopenClass({
  findStuff: function(){
    // use regular AJAX / Promises calls
    return $.getJSON("https://your.api.com/api").then(function(response) {
      var users = [];
      // creates new Ember objects and store them into the users Array
      response.users.forEach(function(user){
        users.push( App.User.create(user) );
      });
      // finally returns the array full of Ember Objects
      return users;
    });
  }
});
</code></pre>

You would use your <code>findStuff</code> method in your routes’ <code>model</code> hook:

<pre><code class="language-javascript">
/* /routes/usersRoute.js
*/
App.UsersRoute = Em.Route.extend({
  model: function(){
    return App.User.findStuff();
  }
});
</code></pre>

## What Is Handlebars Template Precompiling?

Basically, template precompiling entails grabbing all Handlebars templates, transposing them into JavaScript strings, and then storing them in <code>Ember.TEMPLATES</code>. It also entails an additional JavaScript file to load in your page, which will contain the JavaScript-compiled versions of all of your Handlebars templates.

For very simple apps, precompiling can be avoided. But if you have too many <code>&lt;script type="text/x-handlebars"&gt;</code> templates in your main HTML file, then precompiling will help to organize your code.

Furthermore, precompiling your templates will enable you to use the runtime version of Handlebars, which is lighter than the regular one. You can find both the runtime and standard versions on the <a href="https://handlebarsjs.com/">Handlebars website</a>.</p>

### Template Naming Conventions

<code><a href="https://emberjs.com/guides/templates/rendering-with-helpers/">Partials</a></code> have to begin with a <code>_</code>. So, you will have to declare a <code>_yourpartial.hbs</code> file or, if you don’t precompile your templates, a <code>&lt;script type="text/x-handlebars" id="_yourpartial"&gt;</code> tag.</p>

<code><a href="https://emberjs.com/guides/components">Components</a></code> have to begin with <code>components/</code>. So, you will have to store them in a <code>components/</code> folder or, if you don’t precompile templates, declare a <code>&lt;script type="text/x-handlebars" id="components/your-component"&gt;</code> tag. Component names are hyphenated.

Otherwise, views have a <code>templateName</code> property in which you can specify which template to associate with the view. Take this declaration of a template:

<pre><code class="language-markup">
&lt;script type="text/x-handlebars" id="folder/some-template"&gt;
  Some template
&lt;/script&gt;
</code></pre>

You can associate it with a particular view:

<pre><code class="language-javascript">
App.SomeView = Em.View.extend({
  templateName: 'folder/some-template'
});
</code></pre>

### Precompiling With Grunt

If you use <a href="https://www.smashingmagazine.com/2013/10/get-up-running-grunt/">Grunt</a>, then you probably use it for other building-related tasks (concatenation, compression, that kind of stuff), in which case you should be familiar with the <code>package.json</code> file, which comes with Node.js and Node Packaged Modules. I’ll assume you are already familiar with Grunt.

As of the time of writing, two plugins are available for Grunt to transpose your <code>.hbs</code> files to a <code>templates.js</code> file: <code><a href="https://github.com/yaymukund/grunt-ember-handlebars">grunt-ember-handlebars</a></code> and <code><a href="https://github.com/dgeb/grunt-ember-templates">grunt-ember-templates</a></code>. The latter seems a bit more up to date than the former.

I’ve made a Gist for each of them, in case you need help with configuration:

*   `grunt-ember-handlebars` ([see the Gist](https://gist.github.com/jkneb/6072299)),
*   `grunt-ember-templates` ([see the Gist](https://gist.github.com/jkneb/6599001)).

Once it’s configured, you should be able to run <code>grunt</code> in a command-line editor, which should produce the <code>templates.js</code> file. Load it into <code>index.html</code> (after <code>ember.js</code>), and then go into the browser’s console and type <code>Em.TEMPLATES</code>. You should see a hash containing all of the compiled templates.

Be aware that Ember.js doesn’t need the template file’s complete path, nor the file’s extension. In other words, the template’s name should be <code>users/create</code>, not <code>/assets/js/templates/users/create.hbs</code>.

Both plugins have options to handle this. Simply refer to the respective guide, or look at the Gists linked to above. You should end up with something like this:

<figure><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6ceb28e0-f530-447b-82db-3cc2ed9d2c5c/console-templates.png" alt="console-templates" width="500" height="271" /></figure>

And this is exactly what we need to make everything work as intended. It’s all you need to know about precompiling with Grunt.</p>

### Precompiling With Rails

Precompiling with Rails is surely the easiest way to do it. The <a href="https://github.com/emberjs/ember-rails">Ember-Rails gem</a> handles pretty much everything for you. It <em>almost</em> works out of the box. Carefully follow the installation instructions in the <code>readme</code> file on GitHub, and you should be all good. Right now, in my humble opinion, Rails has the best Ember and Handlebars integration available.</p>

## Tools, Tips And Resources

### Chrome Ember Extension

<a href="https://chrome.google.com/webstore/detail/ember-inspector/bmdblncegkenkacieihfhpjfppoconhi">Ember Extension</a> is a very convenient Chrome extension. Once installed, an “Ember” tab will appear near the “Console” tab. Then, you can navigate through controllers, routes and views. And the “Data” tab will greatly help you to explore your records if you are using Ember-Data.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/6b148b92-9399-41f7-bc95-f26785c35bba/console-ember-extension1.png"><img class="size-medium wp-image-128619" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/deb2acc8-47f7-4797-9120-80ece357e9bd/console-ember-extension1-300x156.png" alt="console-ember-extension" width="300" height="156" /></a><figcaption>Exploring your app’s objects has never been so easy.</figcaption></figure>

### Ember App Kit

Maintained by the Ember team, the <a href="https://iamstef.net/ember-app-kit/">Ember App Kit</a> lets you easily scaffold Ember JS apps. It contains <a href="https://gruntjs.com/">Grunt</a> for compiling assets, <a href="https://www.jshint.com/">JSHint</a>, <a href="https://qunitjs.com/">QUnit</a>, the <a href="https://karma-runner.github.io/0.10/index.html">Kharma</a> test runner, <a href="https://bower.io/">Bower</a> and <a href="https://wiki.ecmascript.org/doku.php?id=harmony:modules">ES6 Modules</a> support.</p>

### Ember Tools

This GitHub project, <a href="https://github.com/rpflorence/ember-tools">Ember Tools</a>, is a basic command-line interface for creating and scaffolding Ember apps. Take a minute to watch the animated GIF in the <code>readme</code> file, and you’ll see why it’s so cool.</p>

### Development and Minified Version

Always use the development build when developing because it contains a lot of comments, a unit-testing package and a ton of helpful error messages, all of which has been removed in the minified build. Find links to both in the builds section of the <a href="https://emberjs.com/builds">Ember.js website</a>.</p>

### Debugging Tips

Ember JS usually gives you cool human-readable errors in the browser’s console (remember to use the development version). Sometimes, though, figuring out what’s going on is tricky. Some convenient methods are <code>{{log something}}</code> and <code>{{controller}}</code>, which helpfully prints the current <code>controller</code> for the template to which you’ve added this helper.

Or you could log each <code>Router</code> transition like so:

<pre><code class="language-javascript">
window.App = Ember.Application.create({
  LOG_TRANSITIONS: true
});
</code></pre>

The guides have an <a href="https://emberjs.com/guides/understanding-ember/debugging">exhaustive list</a> of these handy little methods.</p>

### Properly Comment Your Handlebars

This one can be frustrating. Never ever comment a Handlebars tag with a regular HTML comment. If you do, you’ll completely break the app, without getting a clue about what’s happening.</p>

<pre><code class="language-markup">
// never do this
&lt;!-- {{foo}} --&gt;

// instead do this
{{!foo}}
</code></pre>

## Conclusion

I hope this <em>long</em> article has given you a better understanding of this awesome framework. But the truth is, we’ve only scratched the surface. There’s so much more to cover. For instance, we have the router and its asynchronous nature, which resolves model requests with promises (so that you can easily implement loading spinners). There is also the object model, with its class and instances inheritance, mixins, observers, filters, macros, collectionViews, components, dependencies managed between controllers, and testing package. And so much more!

Obviously, I couldn’t cover everything. Fortunately, the guides will take you through all of these topics very well.

Happy Ember.js coding, folks!

### Resources

*   [Ember.js Guides](https://emberjs.com/guides/) The best place to learn Ember
*   [Ember.js Cookbook](https://emberjs.com/guides/cookbook/) A new section of the guides that solves very specific use cases
*   [EmberWatch](https://emberwatch.com) Aggregates all important resources out there
*   [Ember Weekly](https://emberweekly.com/issues.html) Perfect for keeping up to date
*   [Ember.js Discussion Forum](https://discuss.emberjs.com) Where discussion happens (and it’s made with Ember.js)

### Acknowledgments

Huge thanks to <a href="https://twitter.com/MatBreton">Mathieu Breton</a> and <a href="https://twitter.com/ficastelli">Philippe Castelli</a>, who both taught me everything they know about Ember.js while I was learning it. Also, a big thank you to <a href="https://twitter.com/tomdale">Tom Dale</a>, who helped me to revise this very long article.

{{< signature "al, il" >}}


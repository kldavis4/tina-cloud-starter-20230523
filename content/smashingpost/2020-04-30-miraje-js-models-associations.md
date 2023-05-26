---
title: 'Mirage JS Deep Dive: Understanding Mirage JS Models And Associations (Part 1)'
slug: miraje-js-models-associations
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d04f3f87-5533-4d5d-9424-2dc6a76284fe/miraje-js-models-associations.png
date: 2020-04-30T09:30:00.000Z
summary: >-
  In this first part of the Mirage JS Deep Dive series, we will be looking at Mirage JS models and associations. We’ll take a closer look at what they are and the roles they play in crafting out production-ready frontend without an actual backend with Mirage JS.
description: >-
  In this first part of the Mirage JS Deep Dive series, we will be looking at Mirage JS models and associations. We’ll take a closer look at what they are and the roles they play in crafting out production-ready frontend without an actual backend with Mirage JS.
categories:
  - API
  - Vue
  - JavaScript
---

Mirage JS is helping simplify modern front-end development by providing the ability for front-end engineers to craft applications without relying on an actual back-end service. In this article, I’ll be taking a framework-agnostic approach to show you Mirage JS models and associations. If you haven’t heard of Mirage JS, you can read my [previous article](https://www.smashingmagazine.com/2020/02/api-mocking-mirage-vue-javascript/) in which I introduce it and also integrate it with the progressive framework Vue.js.

Note: *These deep-dive series are framework agnostic, meaning that we would be looking at Mirage JS itself and not the integration into any front-end framework.*

- Part 1: **Understanding Mirage JS Models And Associations**
- [Part 2](https://www.smashingmagazine.com/2020/05/mirage-javascript-factories-fixtures-serializers/): Understanding Factories, Fixtures And Serializers
- [Part 3](https://www.smashingmagazine.com/2020/06/mirage-javascript-timing-response-passthrough/): Understanding Timing, Response And Passthrough 
- [Part 4](https://www.smashingmagazine.com/2020/06/mirage-javascript-cypress-ui-testing): Using Mirage JS And Cypress For UI Testing

## Models

Mirage JS borrowed some terms and concepts which are very much familiar to back-end developers, however, since the library would be used mostly by front-end teams, it’s appropriate to learn what these terms and concepts are. Let’s get started with what models are.

## What Are Models?

Models are classes that define the properties of a particular data to be stored in a database. For example, if we have a user model, we would define the properties of a user for our application such as name, email, and so on. So each time we want to create a new user, we use the user model we’ve defined.

{{% feature-panel %}}

## Creating models In Mirage JS

Though Mirage JS would allow you mockup data manually, using the Mirage Model class would give you a whole lot of awesome development experience because you’d have at your fingertips, data persistence. 

Models wrap your database and allow you to create relationships that are really useful for returning different collections of data to your app.

Mirage uses an in-memory database to store entries you make using its model. Also without models, you won’t have access to associations which we would look at in a bit.

So, in order to create a model in Mirage JS first of, you have to import the Model class from Mirage JS like so:

<pre><code class="language-javascript">import { Server, Model } from ‘miragejs’
</code></pre>

Then, in our ‘Server’ options we use it as the following:

<pre><code class="language-javascript">let server = new Server({
  models: {
    user: Model,
  }
</code></pre>

**Note**: *If you don’t know what Mirage JS server is, it’s how Mirage JS intercepts network requests. I explained it in detail in my [previous](https://www.smashingmagazine.com/2020/02/api-mocking-mirage-vue-javascript/) article.*

From the above, you could see we are creating a user model instance. Doing so allows us to persist entries for the said model.

## Creating Entries

To create new entries for our user model, you need to use the schema class like so:

<pre><code class="language-javascript">let user = schema.users.create({name: “Harry Potter”})
</code></pre>

**Note**: *Mirage JS automatically pluralize your models to form the schema. You could also see we are not explicitly describing before-hand, the properties the user model instance would have. This approach makes for the rapid creation of entries and flexibility in adding fields for the said entries.*

You’d most likely be creating instances of your model in the `seeds()` method of your server instance, so in that scenario you’d create a new user instance using the `create()` method of the `server` object like so:

<pre><code class="language-javascript">let server = new Server({
  models: {
    user: Model
  },

  seeds(server) {
    server.create("user", { name: "Harry Potter" });
});
</code></pre>

In the above code, I redundantly added the snippet for both the server and model creation as to establish some context. 

*To see a full working Mirage JS server see my [previous article](https://www.smashingmagazine.com/2020/02/api-mocking-mirage-vue-javascript/) on the same subject or [check this repo](https://github.com/DominusKelvin/miragejs-demo-vue).*

## Accessing Properties And Relationships
 
You could access the properties or fields of a model instance using dot notation. So if we want to create a new user instance for the user model, then use this:

<pre><code class="language-javascript">let user = schema.users.create({name: “Hermione Granger”})
</code></pre>

We can also access the name of the user simply by using the following:

<pre><code class="language-javascript">user.name
// Hermione Granger
</code></pre>

Furthermore, if the instance created has a relationship called ‘posts’ for example, we can access that by using:

<pre><code class="language-javascript">user.posts
// Returns all posts belonging to the user 
</code></pre>

## Finding An Instance

Let’s say you’ve created three instances of the user model and you want to find the first one you could simply use the schema on that model like so:

<pre><code class="language-javascript">let firstUser = schema.users.find(1)
// Returns the first user
</code></pre>

## More Model Instance Properties

Mirage exposes a couple of useful properties on model instances. Let’s take a closer look at them.

### `associations`

You could get the associations of a particular instance by using the `associations` property.

<pre><code class="language-javascript">let harry = schema.users.create({name: “Harry Potter”})
user.associations
// would return associations of this instance if any
</code></pre>

According to the Mirage JS docs, the above would return a hash of relationships belonging to that instance.

## attrs

We can also get all the fields or attributes of a particular instance by using the attrs property of a model instance like so:

<pre><code class="language-javascript">harry.attrs
// { name: “Harry Potter” }
</code></pre>

## Methods

### destroy()

This method removes the instances it is called on from Mirage JS database. 

<pre><code class="language-javascript">harry.destroy()
</code></pre>

### isNew()

This method returns true if the model has not been persisted yet to the database. Using the `create` method of the schema would always save an instance to Mirage JS database so `isNew()` would always return false. However, if you use the new method to create a new instance and you haven’t called `save()` on it, `isNew()` would return true.

Here’s an example:

<pre><code class="language-javascript">let ron = schema.users.new({name: “Ronald Weasley”})

ron.isNew()

// true

ron.save()

ron.isNew()

// false
</code></pre>

### isSaved()

This is quite the opposite of the `isNew()` method. You could use it to check if an instance has been saved into the database. It returns true if the instance has been saved or false if it hasn’t been saved.

### reload()

This method reloads an instance from Mirage Js database. Note it works only if that instance has been saved in the database. It’s useful to get the actual attributes in the database and their values if you have previously changed any. For example:

<pre><code class="language-javascript">let headmaster = schema.users.create({name: “Albus Dumbledore”})

headmaster.attrs
// {id: 1, name: “Albus Dumbledore”}

headmaster.name = “Severus Snape”

headmaster.name
// Severus Snape

headmaster.reload()

headmaster.name

// Albus Dumbledore
</code></pre>

### save()

This method does what it says which is, it saves or creates a new record in the database. You’d only need to use it if you created an instance without using the `create()` method. Let’s see it in action.

<pre><code class="language-javascript">let headmaster = schema.users.new({name: “Albus Dumbledore”})

headmaster.id
// null

headmaster.save()

headmaster.name = “Severus Snape”
// Database has not yet been updated to reflect the new name

headmaster.save()
// database has been updated

headmaster.name

// Severus Snape
</code></pre>

### toString()

This method returns a simple string representation of the model and id of that particular instance. Using our above headmaster instance of the user model, when we call:

<pre><code class="language-javascript">headmaster.toString()
</code></pre>

We get:

<pre><code class="language-javascript">// “model:user:1”
</code></pre>

### update()

This method updates a particular instance in the database. An example would be:

<pre><code class="language-javascript">let headmaster = schema.users.find(1)
headmaster.update(“name”, “Rubeus Harris”)
</code></pre>

**Note**: *The `update()` takes two arguments. The first is the key which is a string and the second argument is the new value you want to update it as.*

## Associations

Since we’ve now been well acquainted with Models and how we use them in Mirage JS, let’s look at it’s counterpart &mdash; associations.

Associations are simply relationships between your models. The relationship could be one-to-one or one-to-many.

Associations are very common in backend development they are powerful for getting a model and its related models, for example, let’s say we want a user and all his posts, associations are utilized in such scenarios. Let’s see how we set that up in Mirage JS.

Once you’ve defined your models, you can create relationships between them using Mirage JS association helpers

Mirage has the following associations helpers

- `hasMany()`  
use for defining to-many relationships 
- `belongsTo()`  
use for defining to-one relationships

When you use either of the above helpers, Mirage JS injects some useful properties and methods in the model instance. Let’s look at a typical scenario of posts, authors, and comments. It could be inferred that a particular author can have more than one blog post also, a particular post can have comments associated with it. So let’s see how we can mock out these relationships with Mirage JS association helpers:

## belongsTo()

### Import Helpers

First import the belongsTo

<pre><code class="language-javascript">import { Server, Model, belongsTo } from 'miragejs'
</code></pre>

Next we create our models and use the extend method to add our relationships like so

<pre><code class="language-javascript">new Server({
  models: {
    post: Model.extend({
      author: belongsTo(),
    }),

    author: Model,
  },
})
</code></pre>

The above defines a to-one relationship from the post model to an author model. Doing so, the belongsTo helper adds several properties and methods to the affected models. Hence we can now do the following:

<div class="break-out">

 <pre><code class="language-javascript">post.authorId // returns the author id of the post
post.author // Author instance
post.author = anotherAuthor
post.newAuthor(attrs) // creates a new author without saving to database
post.createAuthor(attrs) // creates a new author and save to database
</code></pre>
</div>

## hasMany()

This helper like its belongsTo counterpart needs to be imported from Mirage JS before use, so:

<pre><code class="language-javascript">import { Server, Model, hasMany } from 'miragejs'
</code></pre>

Then we can go on creating our to-many relationships:

<pre><code class="language-javascript">  models: {
    post: Model.extend({
      comments: hasMany(),
    }),

    comment: Model,
  },
})
</code></pre>

Like belongsTo(), hasMany() helper also adds several properties and method automatically to the affected models:

<div class="break-out">

 <pre><code class="language-javascript">post.commentIds // [1, 2, 3]
post.commentIds = [2, 3] // updates the relationship
post.comments // array of related comments
post.comments = [comment1, comment2] // updates the relationship
post.newComment(attrs) // new unsaved comment
post.createComment(attrs) // new saved comment (comment.postId is set)
</code></pre>
</div>

The above snippet is adapted from the well written Mirage JS [documentation](https://miragejs.com/docs/main-concepts/relationships/)

## Conclusion

Mirage JS is set out to make mocking our back-end a breeze in modern front-end development. In this first part of the series, we looked at models and associations/relationships and how to utilize them in Mirage JS. 

- Part 1: **Understanding Mirage JS Models And Associations**
- [Part 2](https://www.smashingmagazine.com/2020/05/mirage-javascript-factories-fixtures-serializers/): Understanding Factories, Fixtures And Serializers
- [Part 3](https://www.smashingmagazine.com/2020/06/mirage-javascript-timing-response-passthrough/): Understanding Timing, Response And Passthrough 
- [Part 4](https://www.smashingmagazine.com/2020/06/mirage-javascript-cypress-ui-testing): Using Mirage JS And Cypress For UI Testing

{{< signature "dm, ra, il" >}}

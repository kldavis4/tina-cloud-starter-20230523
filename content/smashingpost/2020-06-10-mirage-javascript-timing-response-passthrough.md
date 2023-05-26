---
title: 'Mirage JS Deep Dive: Understanding Timing, Response And Passthrough (Part 3)'
slug: mirage-javascript-timing-response-passthrough
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/98d62832-3377-44f9-a326-1568a7ac39c8/mirage-javascript-timing-response-passthrough.png
date: 2020-06-10T12:30:00.000Z
summary: >-
  In this third part of Mirage JS Deep Dive series, we will be focusing on using `response`, `timing` and `passthrough` in Mirage for a better handle on simulating an actual backend server. However, before you begin reading this article, please read the [introduction to MirageJS](https://www.smashingmagazine.com/2020/02/api-mocking-mirage-vue-javascript/) first as well as [Part 1](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/) and [Part 2](https://www.smashingmagazine.com/2020/05/mirage-javascript-factories-fixtures-serializers/) of this series.
description: >-
  In this third part of Mirage JS Deep Dive series, we will be focusing on using `response`, `timing` and `passthrough` in Mirage for a better handle on simulating an actual backend server.
categories:
  - API
  - JavaScript
---

Mirage JS was built to give frontend developers the ability to simulate actual backend API calls. So far, we have seen how we can create records with Mirage, intercept API requests via route handlers and, last but not least, how the shape of the data returned to us from Mirage is affected.

In this part of the series, we will see Mirage mechanism for simulating other aspects of an actual backend server like slow network, HTTP status code response, and also making requests to an actual backend even though Mirage is intercepting your frontend requests.

Let’s begin by simulating slow network requests.

## Timing

When developing your frontend application that relies on a backend API, it’s useful to see how your application behaves under slow networks (think about testing loading messages and loaders). This test is important because requests to backend API are **asynchronous** in nature. What this means is that we can’t make assumptions about when we will get the response so we need to write our code as if it might come immediately, or there might be a delay.

A common reason for a delay in response is a slow Internet connection. It is then really important to know how your app would behave in such circumstances. Mirage caters to this need by making available a `timing` option which is a property passed to a route handler that tells the handler to wait for a particular duration specified by the timing option (in milliseconds) before returning a response whenever the route it is handling is called.

**Note**: *By default, Mirage is setting a `400ms` delay for the server during development and `0` during testing so your tests can run faster (no one really enjoys slow tests).*

{{% feature-panel %}}

We now know in theory how to customize Mirage’s server response time. Let’s see a couple of ways to tweak that response time via the `timing` option.

### `timing` On *routes()*

As earlier stated, Mirage sets a default delay for the server response time to be `400ms` during development and `0` for tests. You could override this default on the `routes` method on the Server instance.

In the example below, I am setting the `timing` option to `1000ms` in the `routes` method to artificially set the response delay for all routes:

<pre><code class="language-javascript">import { Server } from 'miragejs'

new Server({
    routes() {
        this.routes = 1000
    }
})
</code></pre>

The above tells Mirage to wait for `1000` milliseconds before returning a response. So if  your front-end make a request to a route handler like the one below:

<pre><code class="language-javascript">this.get('/users', (schema) => {
    return schema.users.all();
});
</code></pre>

Mirage will take 1000 milliseconds to respond.

**Tip**: *Instead of directly using the `schema` object, you could use ES 6 object restructuring to make your route handler cleaner and shorter like below:*

<pre><code class="language-javascript">this.get('/users', ({ users }) => {
    return users.all()
}
</code></pre>

### `timing` For Individual Routes

Although the `this.timing` property is useful, in some scenarios you wouldn’t want to delay all your routes. Because of this scenario, Mirage gives you the ability to set the `timing` option in a config options object you could pass at the end of a route handler.
Taking our above code snippets, let’s pass the `1000ms` response delay to the route itself as opposed to globally setting it:

<pre><code class="language-javascript">this.get('/users', ({ users }) => {
  return users.all();
 }, { timing: 1000 });
</code></pre>

The result is the same as globally assigning the timing. But now you have the ability to specify different timing delays for individual routes. You could also set a global timing with `this.timing` and then override it in a route handler. Like so:

<pre><code class="language-javascript">this.timing = 1000

this.get('users', ( { users } ) => {
    return users.all()
})

this.get('/users/:id', ({ users }, request) => {
    let { id } = request.params;
     return users.find(id);
 }, { timing: 500 });
</code></pre>

So now when we make a request to `/users/1`, it will return the below user JSON in half of the time (500ms) it would take for every other route.

<pre><code class="language-javascript">{
  "user": {
    "name": "Kelvin Omereshone",
    "age": 23,
    "id": "1"
  }
}
</code></pre>

## Passthrough

Route handlers are the Mirage mechanism for intercepting requests your frontend application makes. By default, Mirage will throw an error similar to the one below when your app makes a request to an endpoint that you haven’t defined a Route handler for in your server instance. 

<blockquote>Error: Mirage: Your app tried to <code>GET '/unknown'</code>, but there was no route defined to handle this request. Define a route for this endpoint in your <code>routes()</code> config. Did you forget to define a namespace?</blockquote>

You can, however, tell Mirage that if it sees a request to a route that you didn’t define a route handler for, it should allow that request to go through. This is useful if you have an actual backend and you want to use Mirage to test out endpoints that haven’t been implemented yet in your backend. To do this, you would need to make a call to the `passthrough` method inside the `routes` methods in your Mirage server instance.

{{% ad-panel-leaderboard %}}

Let’s see it in code:

<div class="break-out">

 <pre><code class="language-javascript">import { Server } from 'miragejs'

new Server({
    routes() {
        // you can define your route handlers above the passthrough call
        this.passthrough()
    }
})
</code></pre>
</div>

**Note**: *It is recommended keeping the call to `passthrough` at the bottom in order to give your route handlers precedence.*

Now when Mirage sees requests to a route that you didn’t define in Mirage, it would let them "passthrough". I really find this useful because it makes Mirage play nicely with an actual backend. So a scenario would be, you are ahead of your backend team and you want to make a request to an endpoint that you don’t have in your production backend, you could just mock out that endpoint in mirage and because of the `passthrough` option, you wouldn’t need to worry about other parts of your app making requests failing.

### Using `passthrough` To Whitelist Route

`passthrough` takes in options to allow you to have more control over routes you want to whitelist. So as opposed to calling `passthrough` without any option and allowing routes not present in mirage to `passthrough`, you can pass in one or more strings of the routes you want to whitelist to `passthrough`. So if we want to whitelist `/reviews` and `/pets` we can do that using `passthrough` like so:

<pre><code class="language-javascript">this.passthrough('/reviews', '/pets)
</code></pre>

You can also do multiple calls to `passthrough`:

<pre><code class="language-javascript">this.passthrough('/reviews')
this.passthrough('/pets')
</code></pre>

**Note**: *I find passing multiple route strings to `passthrough` cleaner as opposed to making multiple calls. But you are free to use whatever feels natural to you.*

### Using `passthrough` On A Set Of HTTP Verbs

The above `passthrough` we defined will allow all HTTP verbs (GET, POST, PATCH, DELETE) to `passthrough`. If your use case requires you to allow a subset of the HTTP verbs to `passthrough`, Mirage provides an options array on the `passthrough` method wherein you pass the verbs you want Mirage to whitelist on a particular route. Let’s see it in code:

<pre><code class="language-javascript">// this allows post requests to the /reviews route to passthrough
this.passthrough('/reviews', ['post']);
</code></pre>

You could also pass multiple strings of routes as well as the HTTP verbs array like so:

<div class="break-out">

 <pre><code class="language-javascript">// this allows post and patch requests to /reviews and /pets routes to passthrough

this.passthrough('/pets', 'reviews', ['post', 'patch'])
</code></pre>
</div>

## Response

Now you see the level of customization Mirage gives you with both the `timing` option and `passthrough` method, it feels only natural for you to know how to customize the HTTP status code Mirage sends for the requests you make. By default, Mirage would return a status of `200` which says everything went fine. (Check out [this article](https://codeburst.io/know-your-http-status-a-cheat-sheet-for-http-status-codes-5fb43863e589?gi=521cc94bfde0) for a refresher on HTTP status code.) Mirage, however, provides the `Response` class which you can use to customize the HTTP status code as well as other HTTP headers to be sent back to your frontend application.

The `Response` class gives you more control over your route handler. You can pass in the following to the Response class [constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor):

* The HTTP status code,
* [HTTP Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers),
* Data (a JSON payload to be returned to the frontend).

To see how the `Response` class works, we would start on an easy note by rewriting our previous route handler using the `Response` class. So we would take the below route handler:

<pre><code class="language-javascript">this.get('users', ( { users } ) => {
return users.all()
})
</code></pre>

and then reimplement using the `Response` class. To do this we first need to import the `Response` class from Mirage:

<pre><code class="language-javascript">import { Response } from 'miragejs'
</code></pre>

We would then rewrite our route handler using the `Response` class:

<pre><code class="language-javascript">this.get('/users', ({ users }) => {
    return new Response(200, {}, users.all());
});
</code></pre>

**Note**: *We are passing an empty `{}` to the header argument because we are do not want to set any header values for this response.*

I believe we can infer that Mirage under the hood uses the `Response` class when we previously returned `users.all()` because both implementations would act the same way and return the same JSON payload. 

I will admit the above use of `Response` is a little bit verbose because we are not doing anything special yet. However, the `Response` class holds a world of possibility to allows you to simulate different server states and set headers.

{{% ad-panel-leaderboard %}}

### Setting Server States

With the `Response` class, you can now simulate different server states via the status code which is the first argument the `Response` constructor takes. You can now pass in 400 to simulate a bad request, 201 to simulate the created state when you create a new resource in Mirage, and so on. With that in mind, let’s customize `/users/:id` route handler and pass in 404 to simulate that a user with the particular ID was not found.

<pre><code class="language-javascript">this.get('/users/:id', (schema, request) => {
   let { id } = request.params;
   return new Response(404, {}, { error: 'User with id ${id} not found'});
});
</code></pre>

Mirage would then return a 404 status code with the error message similar to the below JSON payload:

<pre><code class="language-json">{
  "error": "User with id 5 not found"
}
</code></pre>

### Setting Headers

With the `Response` class, you can set response headers by passing an object as the second argument to the `Response` constructor. With this flexibility, you can simulate setting any headers you want. Still using our `/users/:id` route, we can set headers like so:

<div class="break-out">

 <pre><code class="language-javascript">this.get('/users/:id', (schema, request) => {
     let { id } = request.params;
     return new Response(404, {"Content-Type" : "application/json", author: 'Kelvin Omereshone' }, { error: `User with id ${id} not found`});
});
</code></pre>
</div>

Now when you check Mirage logs in your browser console, you would see the headers we set.

## Wrapping Up

In this part of the Mirage JS Deep Dive series, I have expounded three mechanisms that Mirage exposes to its users in order to simulate a real server. I look forward to seeing you use Mirage better with the help of this article.

Stay tuned for the next and final part of the series coming up next week!

- [Part 1](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/): Understanding Mirage JS Models And Associations
- [Part 2](https://www.smashingmagazine.com/2020/05/mirage-javascript-factories-fixtures-serializers/): Understanding Factories, Fixtures And Serializers
- Part 3: **Understanding Timing, Response And Passthrough**
- [Part 4](https://www.smashingmagazine.com/2020/06/mirage-javascript-cypress-ui-testing): Using Mirage JS And Cypress For UI Testing

{{< signature "ra, il" >}}

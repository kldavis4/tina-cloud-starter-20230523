---
title: 'Setting Up API Mocking With Mirage JS And Vue.js'
slug: api-mocking-mirage-vue-javascript
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d853307-2145-4c0d-affa-e52da3bc6895/api-mocking-mirage-vue-javascript.png
date: 2020-02-13T11:00:00.000Z
summary: >-
  This article introduces Mirage JS, an API mocking library that lets you build, test and share a complete working JavaScript application without having to rely on any backend API or services. You’ll also learn how to set up Mirage JS with the progressive front-end framework, Vue.js.
description: >-
  This article introduces Mirage JS, an API mocking library that lets you build, test and share a complete working JavaScript application without having to rely on any backend API or services. You’ll also learn how to set up Mirage JS with the progressive front-end framework, Vue.js.
categories:
  - API
  - Vue
  - JavaScript
---

In the era of SPA and the JAMstack, there has always been a separation of concern between the APIs and front-end development. Almost all JavaScript projects that can be found out in the wild interact with a web service or API and either use it for authentications or getting user-related data.

So, whenever you’re working on a project and the necessary API still hasn’t been implemented by the back-end team or you need to quickly test a feature, you have some of the following options:

- You could proxy to a locally running version of your actual backend which, in most cases as a front-end developer, you wouldn’t have.
- You could comment out actual request and replace with mock data. (This is okay but not so great as you would need to undo that to get to production and you might not be able to deal with network states and latency.)

## What Is API Mocking?

API mocking is an imitation or a simulation of an actual API. It is mostly done in order to intercept requests that are supposed to be made to an actual backend API but this mocking exist on your frontend.

## Why is API Mocking Important

API mocking is significantly important in a lot of ways:

1. It makes for a very good front-end development experience not to depend on production APIs before building out features.
2. You could share your entire frontend and it would work without depending on an actual backend API.

{{% feature-panel %}}

## What Is Mirage JS?

Mirage JS was created 5 years ago and was pretty much used in the Ember community before [Sam Selikoff](https://twitter.com/samselikoff) officially [announced](https://mobile.twitter.com/samselikoff/status/1220780180064567296) its release on the 24th of January, 2020 on Twitter.

Mirage JS solves the pain point for testing backend APIs without depending on those APIs. It allows for seamless front-end development experience by mocking production APIs.

Mirage JS is an API mocking library for Vue.js, React, Angular and Ember frameworks

## What Makes Mirage JS A Better Choice?

There have been other options for API mocking (such as Axios interceptors, [Typicode’s JSON server](https://github.com/typicode/json-server), and so on) but what I think is pretty interesting about Mirage is that it doesn’t get in the way of your development process (as you would see when we set it up with Vue in a bit). It is lightweight and yet powerful.

It comes with battery included out of the box that allows you to replicate real production API consumption scenarios like simulating a slow network with its [timing option](https://miragejs.com/docs/main-concepts/route-handlers/#timing).

## Getting Started With Mirage JS And Vue.js

So now that you know what Mirage JS is and why it’s important to your front-end development workflow, let’s look at setting it up with the progressive web framework: Vue.js.

## Creating A Green-Field (Clean Installation) Vue Project

Using the Vue [CLI](https://cli.vuejs.org/), create a fresh *Vue.js* project by going into the directory you want the project to be created in and running (in your terminal):

<pre><code class="language-bash">vue create miragejs-demo-vue 
</code></pre>

The above command would set up a new Vue project which you can now `cd` into and run either `yarn serve` or `npm run serve`.

## #Installing Mirage JS

Now let’s install Mirage JS as a development dependency in our *Vue.js* project by running the following command:

<pre><code class="language-bash">yarn add -D miragejs
</code></pre>

Or if you are using NPM, run this:

<pre><code class="language-bash">npm install --save-dev miragejs
</code></pre>

And that’s it! Mirage JS is now installed in our *Vue.js* project.

{{% ad-panel-leaderboard %}}

## Let’s Mock Out Something

With Mirage JS installed, let’s see how we configure it to talk to Vue and mock out a basic todos (an API that returns a list of todos) API.

### Define Your Server

To get started, we need to create a *server.js* file in the `/src` directory of our *Vue.js* project. After that, add the following:

<pre><code class="language-javascript">import { Server, Model } from 'miragejs'

export function makeServer({ environment = "development" } = {}) {

let server = new Server({
  environment,

    models: {
      todo: Model,
    },

  seeds(server) {
  server.create("todo", { content: "Learn Mirage JS" })
  server.create("todo", { content: "Integrate With Vue.js" })
  },

  routes() {

    this.namespace = "api"

    this.get("/todos", schema => {
      return schema.todos.all()
    })
    
  },
  })

  return server
}
</code></pre>

### Code Explained

Firstly, the *server.js* file is how you set up Mirage JS to create a new instance of it’s mock (fake) server which will intercept all API calls you make in your app matching the routes that you define.

Now, I agree the above may be overwhelming at first, but let’s take a closer look at what’s going on here:

<pre><code class="language-javascript">import { Server, Model } from 'miragejs'
</code></pre>

From the above code snippet, we are importing `Server` and `Model` from `miragejs`.

- `Server`  
This is a class exposed by Mirage to helps us instantiate a new instance of a Mirage JS server to "serve" as our fake server.
- `Model`  
Another class exposed by Mirage to help in creating models(a model determines the structure of a Mirage JS database entry) powered by Mirage’s ORM.

<pre><code class="language-javascript">export function makeServer({ environment = "development" } = {}) {}
</code></pre>

The above basically export a function called `makeServer` from the `src/server.js`. You could also note we are passing in an environment parameter and setting Mirage’s environment mode to `development` (you would see us passing test environment later on in this article).

### The Body Of `makeServer`

Now we are doing a couple of things in the `makeServer` body. Let’s take a look:

<pre><code class="language-javascript">let server = new Server({})
</code></pre>

We are instantiating a new instance of the Server class and passing it a configuration option. The content of the configuration options help set up mirage:

<pre><code class="language-javascript">{
  environment,

  models: {
    todo: Model,
  },

  seeds(server) {
  server.create("todo", { content: "Learn Mirage JS" })
  server.create("todo", { content: "Integrate With Vue.js" })
  },

  routes() {

    this.namespace = "api"

    this.get("/todos", schema => {
      return schema.todos.all()
    })
  },
  
  }
</code></pre>

Firstly we are passing the `environment` parameter we initialized in the function definition.

<pre><code class="language-javascript">models: {
    todo: Model,
  },
</code></pre>

The next option which is the `models` option takes an object of the different models we want Mirage to mock.

In the above, we simply want a todo model which we are instantiating from the Model class.

<pre><code class="language-javascript">seeds(server) {
server.create("todo", { content: "Learn Mirage JS" })
server.create("todo", { content: "Integrate With Vue.js" })
},
</code></pre>

The next option is the seeds method which takes in a parameter called `server`. The seeds method helps create seeds(seeds are initial data or an entry into Mirage’s database) for our models. In our case to create the seeds for the todo model we do:

<pre><code class="language-javascript">server.create("todo", { content: "Learn Mirage JS" })
server.create("todo", { content: "Integrate With Vue.js" })
</code></pre>

so the server has a create method which expects as the first argument a string which corresponds to the name of the model, then an object which will contain the properties or attributes of a particular seed.

<pre><code class="language-javascript">routes() {

    this.namespace = "api"

    this.get("/todos", schema => {
      return schema.todos.all()
    })
  },
</code></pre>

finally, we have the routes method which defines the various route(routes are our mock API endpoints) Mirage JS is going to mock. Let’s look at the body of the method:

<pre><code class="language-javascript">this.namespace = "api"
</code></pre>

this line sets up the namespace for all routes that means our todo route can now be accessed from /api/todos.

<pre><code class="language-javascript">this.get("/todos", schema => {
  return schema.todos.all()
})
</code></pre>

The above creates a get route and it’s handler using the `this.get()` method. The `get()` method expects the route i.e "/todos" and a handler function that takes in `schema` as an argument. The schema object is how you interact with Mirage’s ORM which is powered by Mirage JS in-memory database.

Finally:

<pre><code class="language-javascript">return schema.todos.all()
</code></pre>

We are returning a list of all our todos, using the schema object made possible by Mirage’s ORM.

### src/main.js

So we are done setting up `src/server.js` but Vue doesn’t know about it(at least not yet). So let’s import it in our *main.js* file like so:

<pre><code class="language-javascript">import { makeServer } from "./server"
</code></pre>

Then we call the `makeServer` function like so:

<pre><code class="language-javascript">if (process.env.NODE_ENV === "development") {
  makeServer()
}
</code></pre>

The above `if` conditional is a guard to make sure mirage only runs in development.

{{% ad-panel-leaderboard %}}

## Set up Complete!

Now we’ve set up Miragejs with Vue. Let’s see it in action. In our *App.vue* file, we would clear out the content and replace with the below snippet:

<pre><code class="language-javascript">&lt;template&gt;
  &lt;ul id="todos"&gt;
    &lt;li v-for="todo in todos" v-bind:key="todo.id"&gt;{{ todo.content }}&lt;/li&gt;
  &lt;/ul&gt;
&lt;/template&gt;

&lt;script&gt;
  export default {
    name: 'app',

    data() {
      return {
        todos: []
      }
    },

    created() {
      fetch("/api/todos")
        .then(res =&gt; res.json())
        .then(json =&gt; {
          this.todos = json.todos
        })
    }
  }
&lt;/script&gt;
</code></pre>

If you are familiar with Vue.js, the above would be nothing new but for the sake of being total, what we are doing is making an API request using `fetch` when our `App.vue` component is created, then we pass in the returned data to the todos array in our component state. Afterward, we are using a v-for to iterate the todos array and displaying the content property of each todo.

## Where Is The Mirage JS Part?

If you notice, in our App.vue component, we didn’t do anything specific to Mirage, we are just making an API call as we would normally do. This feature of Mirage is really great for DX cause under the hood, Mirage would intercept any requests that match any of the routes defined in src/server.js while you are in development. 

This is pretty handy cause no work would be needed in your part to switch to an actual production server when you are in a production environment provided the routes match your production API endpoints.

So restart your Vue dev server via `yarn serve` to test Mirage JS.

You should see a list of two todos. One thing you’d find pretty interesting is that we did not need to run a terminal command to start up Mirage because it removes that overhead by running as a part of your Vue.js application.

## Mirage JS And Vue test-utils

If you are already using Vue Test-utils in your Vue application, you’d find it exciting to know that Mirage can easily work with it to mock network requests. Let’s see an example set up using our todos application.

We would be using Jest for our unit-testing. So if you are following along, you could pretty much use the Vue CLI to install the `@vue/unit-jest` plugin like so:

<pre><code class="language-bash">vue add @vue/unit-jest
</code></pre>

The above will install `@vue/cli-plugin-unit-jest` and `@vue/test-utils` development dependencies while also creating a `tests` directory and a *jest.config.js* file. It will also add the following command in our *package.json* `scripts` section (pretty neat):

<pre><code class="language-json">"test:unit": "vue-cli-service test:unit"
</code></pre>

## Let’s Test!

We would update our *App.vue* to look like this:

<pre><code class="language-javascript">&lt;!-- src/App.vue --&gt;
&lt;template&gt;
  &lt;div v-if="serverError" data-testid="server-error"&gt;
    {{ serverError }}
  &lt;/div&gt;

  &lt;div v-else-if="todos.length === 0" data-testid="no-todos"&gt;
    No todos!
  &lt;/div&gt;

  &lt;div v-else&gt;
    &lt;ul id="todos"&gt;
      &lt;li
        v-for="todo in todos"
        v-bind:key="todo.id"
        :data-testid="'todo-' + todo.id"
      &gt;
        {{ todo.content }}
      &lt;/li&gt;
    &lt;/ul&gt;
  &lt;/div&gt;
&lt;/template&gt;

&lt;script&gt;
  export default {
    name: "app",

    data() {
      return {
        todos: [],
        serverError: null,
      }
    },

    created() {
      fetch("/api/todos")
        .then(res =&gt; res.json())
        .then(json =&gt; {
          if (json.error) {
            this.serverError = json.error
          } else {
            this.todos = json.todos
          }
        })
    },
  }
&lt;/script&gt;
</code></pre>

Nothing really epic is going on in the above snippet; we are just structuring to allow for the network testing we would be implementing with our unit test.

Although Vue CLI has already added a `/tests` folder for us, I find it to be a much better experience when my tests are placed close to the components they are testing. So create a `/__tests__` folder in `src/` and create an *App.spec.js* file inside it. (This is also the recommended approach by Jest.)

<pre><code class="language-javascript">// src/__tests__/App.spec.js
import { mount } from "@vue/test-utils"
import { makeServer } from "../server"
import App from "../App.vue"

let server

beforeEach(() => {
  server = makeServer({ environment: "test" })
})

afterEach(() => {
  server.shutdown()
})
</code></pre>

So to set up our unit testing, we are importing the `mount` method from `@vue/test-utils`, importing the Miragejs server we created earlier and finally importing the `App.vue` component.

Next, we are using the `beforeEach` life cycle function to start the Mirage JS server while passing in the test environment. (Remember, we set by default the environment to be `development`.)

Lastly, we are shutting down the server using `server.shutdown` in the `afterEach` lifecycle method.

### Our Tests

Now let’s flesh out our test (we would be adopting the quickstart section of the Mirage js [docs](https://miragejs.com/quickstarts/vue/vue-test-utils). So your *App.spec.js* would finally look like this:

<div class="break-out">

 <pre><code class="language-javascript">// src/__tests__/App.spec.js

import { mount } from "@vue/test-utils"
import { makeServer } from "./server"
import App from "./App.vue"

let server

beforeEach(() => {
  server = makeServer({ environment: "test" })
})

it("shows the todos from our server", async () => {
  server.create("todo", { id: 1, content: "Learn Mirage JS" })
  server.create("todo", { id: 2, content: "Integrate with Vue.js" })

  const wrapper = mount(App)

  // let’s wait for our vue component to finish loading data
  // we know it’s done when the data-testid enters the dom.
  await waitFor(wrapper, '[data-testid="todo-1"]')
  await waitFor(wrapper, '[data-testid="todo-2"]')

  expect(wrapper.find('[data-testid="todo-1"]').text()).toBe("Learn Mirage JS")
  expect(wrapper.find('[data-testid="todo-2"]').text()).toBe("Integrate with Vue.js")
})

it("shows a message if there are no todo", async () => {
  // Don’t create any todos

  const wrapper = mount(App)
  await waitFor(wrapper, '[data-testid="no-todos"]')

  expect(wrapper.find('[data-testid="no-todos"]').text()).toBe("No todos!")
})

// This helper method returns a promise that resolves
// once the selector enters the wrapper’s dom.
const waitFor = function(wrapper, selector) {
  return new Promise(resolve => {
    const timer = setInterval(() => {
      const todoEl = wrapper.findAll(selector)
      if (todoEl.length > 0) {
        clearInterval(timer)
        resolve()
      }
    }, 100)
  })
}

afterEach(() => {
  server.shutdown()
})
</code></pre>
</div>

**Note**: *We are using a helper here (as defined in the Mirage JS docs). It returns a promise that allows us to know when the elements we are testing are already in the DOM.*

Now run `yarn test:unit`. 

All your tests should pass at this point.

## Testing Different Server State With Mirage JS

We could alter our Mirage JS server to test for different server states. Let’s see how.

<pre><code class="language-javascript">// src/__tests__/App.spec.js
import { Response } from "miragejs"
</code></pre>

First, we import the `Response` class from Mirage, then we create a new test scenario like so:

<pre><code class="language-javascript">it("handles error responses from the server", async () => {
  // Override Mirage’s route handler for /todos, just for this test
  server.get("/todos", () => {
    return new Response(
      500,
      {},
      {
        error: "The database is taking a break.",
      }
    )
  })

  const wrapper = mount(App)

  await waitFor(wrapper, '[data-testid="server-error"]')

  expect(wrapper.find('[data-testid="server-error"]').text()).toBe(
    "The database is taking a break."
  )
})
</code></pre>

Run your test and it all should pass.

## Conclusion

This article aimed to introduce you to Mirage JS and show you how it makes for a better front-end development experience. We saw the problem Mirage JS created to address (building production-ready front-end without any actual backend API) and how to set it up with Vue.js.

Although this article scratched the surface of what Mirage JS can do, I believe it is enough to get you started.

- *You could go through the [docs](https://miragejs.com/docs/getting-started/introduction) as well as join the Mirage JS discord [server](https://discordapp.com/invite/pPsdsrn).*
- *The supporting repo for this article is available on [GitHub](https://github.com/DominusKelvin/miragejs-demo-vue).*

### References

* [The Mirage Docs](https://miragejs.com/docs/getting-started/introduction) 
* [Mirage Vue Quickstart](https://miragejs.com/quickstarts/vue)

{{< signature "dm, il" >}}

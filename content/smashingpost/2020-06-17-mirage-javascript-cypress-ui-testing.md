---
title: 'Mirage JS Deep Dive: Using Mirage JS And Cypress For UI Testing (Part 4)'
slug: mirage-javascript-cypress-ui-testing
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c72a433-bd2c-4d6b-9a8c-04c325d4f20a/mirage-javascript-cypress-ui-testing.png
date: 2020-06-17T10:30:00.000Z
summary: >-
  In this final part of Mirage JS Deep Dive series, we will be putting everything we’ve learned in the past series into learning how to perform UI tests with Mirage JS.
description: >-
  In this final part of Mirage JS Deep Dive series, we will be putting everything we’ve learned in the past series into learning how to perform UI tests with Mirage JS.
categories:
  - UI
  - API
  - Testing
  - JavaScript
---

One of my favorite quotes about software testing is from the Flutter documentation. It says:

<blockquote> “How can you ensure that your app continues to work as you add more features or change existing functionality? By writing tests.”</blockquote>

On that note, this last part of the [Mirage JS Deep Dive series](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/) will focus on using Mirage to test your JavaScript front-end application.

**Note**: *This article assumes a [Cypress](https://www.cypress.io/) environment. Cypress is a testing framework for UI testing. You can, however, transfer the knowledge here to whatever UI testing environment or framework you use.*

### Read <span class="rh">Previous Parts</span> Of The Series:

- [Part 1](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/): Understanding Mirage JS Models And Associations
- [Part 2](https://www.smashingmagazine.com/2020/05/mirage-javascript-factories-fixtures-serializers/): Understanding Factories, Fixtures And Serializers
- [Part 3](https://www.smashingmagazine.com/2020/06/mirage-javascript-timing-response-passthrough/): Understanding Timing, Response And Passthrough

## UI Tests Primer

UI or User Interface test is a form of [acceptance testing](https://en.wikipedia.org/wiki/Acceptance_testing) done to verify the **user** flows of your front-end application. The emphasis of these kinds of software tests is on the end-user that is the actual person who will be interacting with your web application on a variety of devices ranging from desktops, laptops to mobile devices. These **users** would be interfacing or interacting with your application using input devices such as a keyboard, mouse, or touch screens. UI tests, therefore, are written to mimic the **user** interaction with your application as close as possible.

Let’s take an e-commerce website for example. A typical UI test scenario would be:

- The user can view the list of products when visiting the homepage.

Other UI test scenarios might be:

- The user can see the name of a product on the product’s detail page.
- The user can click on the "add to cart" button.
- The user can checkout.

You get the idea, right?

In making UI Tests, you will mostly be relying on your back-end states, i.e. did it return the products or an error? The role Mirage plays in this is to make those server states available for you to tweak as you need. So instead of making an actual request to your production server in your UI tests, you make the request to Mirage mock server.

For the remaining part of this article, we will be performing UI tests on a fictitious e-commerce web application UI. So let’s get started.

{{% feature-panel %}}

## Our First UI Test

As earlier stated, this article assumes a Cypress environment. Cypress makes testing UI on the web fast and easy. You could simulate clicks and navigation and you can programmatically visit routes in your application. See the [docs](https://docs.cypress.io/guides/overview/why-cypress.html#In-a-nutshell) for more on Cypress.

So, assuming Cypress and Mirage are available to us, let’s start off by defining a proxy function for your API request. We can do so in the `support/index.js` file of our Cypress setup. Just paste the following code in:

<div class="break-out">

 <pre><code class="language-javascript">// cypress/support/index.js
Cypress.on("window:before:load", (win) => {
  win.handleFromCypress = function (request) {
    return fetch(request.url, {
      method: request.method,
      headers: request.requestHeaders,
      body: request.requestBody,
    }).then((res) => {
      let content =
        res.headers.map["content-type"] === "application/json"
          ? res.json()
          : res.text()
      return new Promise((resolve) => {
        content.then((body) => resolve([res.status, res.headers, body]))
      })
    })
  }
})
</code></pre>
</div>

Then, in your app bootstrapping file (`main.js` for Vue, `index.js` for React), we’ll use Mirage to proxy your app’s API requests to the `handleFromCypress` function only when Cypress is running. Here is the code for that:

<div class="break-out">

 <pre><code class="language-javascript">import { Server, Response } from "miragejs"

if (window.Cypress) {
  new Server({
    environment: "test",
    routes() {
      let methods = ["get", "put", "patch", "post", "delete"]
      methods.forEach((method) => {
        this[method]("/*", async (schema, request) => {
          let [status, headers, body] = await window.handleFromCypress(request)
          return new Response(status, headers, body)
        })
      })
    },
  })
}
</code></pre>
</div>

With that setup, anytime Cypress is running, your app knows to use Mirage as the mock server for all API requests.

Let’s continue writing some UI tests. We’ll begin by testing our homepage to see if it has **5 products** displayed. To do this in Cypress, we need to create a `homepage.test.js` file in the `tests` folder in the root of your project directory. Next, we’ll tell Cypress to do the following:

* Visit the homepage i.e `/` route
* Then **assert** if it has li elements with the class of `product` and also checks if they are 5 in numbers.

Here is the code:

<pre><code class="language-javascript">// homepage.test.js
it('shows the products', () => {
  cy.visit('/');

  cy.get('li.product').should('have.length', 5);
});
</code></pre>

You might have guessed that this test would fail because we don’t have a production server returning 5 products to our front-end application. So what do we do? We mock out the server in Mirage! If we bring in Mirage, it can intercept all network calls in our tests. Let’s do this below and start the Mirage server before each test in the `beforeEach` function and also shut it down in the `afterEach` function. The `beforeEach` and `afterEach` functions are both provided by Cypress and they were made available so you could run code before and after each test run in your test suite &mdash; hence the name. So let’s see the code for this: 

<pre><code class="language-javascript">// homepage.test.js
import { Server } from "miragejs"

let server

beforeEach(() => {
  server = new Server()
})

afterEach(() => {
  server.shutdown()
})

it("shows the products", function () {
  cy.visit("/")

  cy.get("li.product").should("have.length", 5)
})
</code></pre>

Okay, we are getting somewhere; we have imported the Server from Mirage and we are starting it and shutting it down in `beforeEach` and `afterEach` functions respectively. Let’s go about mocking our product resource.

<pre><code class="language-javascript">
// homepage.test.js
import { Server, Model } from 'miragejs';

let server;

beforeEach(() => {
  server = new Server({
    models: {
      product: Model,
    },

    routes() {
      this.namespace = 'api';

      this.get('products', ({ products }, request) => {
        return products.all();
      });
    },
  });
});

afterEach(() => {
  server.shutdown();
});

it('shows the products', function() {
  cy.visit('/');

  cy.get('li.product').should('have.length', 5);
});
</code></pre>

**Note**: *You can always take a peek at the previous parts of this series if you don’t understand the Mirage bits of the above code snippet.*

- [Part 1](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/): *Understanding Mirage JS Models And Associations*
- [Part 2](https://www.smashingmagazine.com/2020/05/mirage-javascript-factories-fixtures-serializers/): *Understanding Factories, Fixtures And Serializers*
- [Part 3](https://www.smashingmagazine.com/2020/06/mirage-javascript-timing-response-passthrough/): *Understanding Timing, Response And Passthrough*

Okay, we have started fleshing out our Server instance by creating the product model and also by creating the route handler for the `/api/products` route. However, if we run our tests, it will fail because we don’t have any products in the Mirage database yet.

Let’s populate the Mirage database with some products. In order to do this, we could have used the `create()` method on our server instance, but creating 5 products by hand seems pretty tedious. There should be a better way.

Ah yes, there is. Let’s utilize factories (as explained in the [second part](https://www.smashingmagazine.com/2020/05/mirage-javascript-factories-fixtures-serializers/) of this series). We’ll need to create our product factory like so:

<pre><code class="language-javascript">// homepage.test.js
import { Server, Model, Factory } from 'miragejs';

let server;

beforeEach(() => {
  server = new Server({
    models: {
      product: Model,
    },
     factories: {
      product: Factory.extend({
        name(i) {
            return `Product ${i}`
        }
      })
    },

    routes() {
      this.namespace = 'api';

      this.get('products', ({ products }, request) => {
        return products.all();
      });
    },
  });
});

afterEach(() => {
  server.shutdown();
});

it('shows the products', function() {
  cy.visit('/');

  cy.get('li.product').should('have.length', 5);
});
</code></pre>

Then, finally, we’ll use `createList()` to quickly create the 5 products that our test needs to pass.

Let’s do this:

<pre><code class="language-javascript">// homepage.test.js
import { Server, Model, Factory } from 'miragejs';

let server;

beforeEach(() => {
  server = new Server({
    models: {
      product: Model,
    },
     factories: {
      product: Factory.extend({
        name(i) {
            return `Product ${i}`
        }
      })
    },

    routes() {
      this.namespace = 'api';

      this.get('products', ({ products }, request) => {
        return products.all();
      });
    },
  });
});

afterEach(() => {
  server.shutdown();
});

it('shows the products', function() {
  server.createList("product", 5)
  cy.visit('/');

  cy.get('li.product').should('have.length', 5);
});
</code></pre>

So when we run our test, it passes!

**Note**: *After each test, Mirage’s server is shutdown and reset, so none of this state will leak across tests.*

{{% ad-panel-leaderboard %}}

## Avoiding Multiple Mirage Server

If you have been following along this series, you’d notice when we were using Mirage in development to intercept our network requests; we had a `server.js` file in the root of our app where we set up Mirage. In the spirit of DRY (Don’t Repeat Yourself), I think it would be good to utilize that server instance instead of having two separate instances of Mirage for both development and testing. To do this (in case you don’t have a `server.js` file already), just create one in your project **src** directory.

**Note**: *Your structure will differ if you are using a JavaScript framework but the general idea is to setup up the server.js file in the src root of your project.*

So with this new structure, we’ll export a function in `server.js` that is responsible for creating our Mirage server instance. Let’s do that:

<pre><code class="language-javascript">// src/server.js

export function makeServer() { /* Mirage code goes here */}
</code></pre>

Let’s complete the implementation of the `makeServer` function by removing the Mirage JS server we created in `homepage.test.js` and adding it to the `makeServer` function body:

<pre><code class="language-javascript">import { Server, Model, Factory } from 'miragejs';

export function makeServer() {
  let server = new Server({
    models: {
      product: Model,
    },
    factories: {
      product: Factory.extend({
        name(i) {
          return `Product ${i}`;
        },
      }),
    },
    routes() {
      this.namespace = 'api';

      this.get('/products', ({ products }) => {
        return products.all();
      });
    },
    seeds(server) {
      server.createList('product', 5);
    },
  });
  return server;
}
</code></pre>

Now all you have to do is import `makeServer` in your test. Using a single Mirage Server instance is cleaner; this way you don’t have to maintain two server instances for both development and test environments.

After importing the `makeServer` function, our test should now look like this:

<pre><code class="language-javascript">import { makeServer } from '/path/to/server';

let server;

beforeEach(() => {
  server = makeServer();
});

afterEach(() => {
  server.shutdown();
});

it('shows the products', function() {
  server.createList('product', 5);

  cy.visit('/');

  cy.get('li.product').should('have.length', 5);
});
</code></pre>

So we now have a central Mirage server that serves us in both development and testing. You can also use the `makeServer` function to start Mirage in development (see [first part](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/) of this series).

Your Mirage code should not find it’s way into production. Therefore, depending on your build setup, you would need to only start Mirage during development mode.

**Note**: *Read my article on [how to set up API Mocking with Mirage and Vue.js](https://www.smashingmagazine.com/2020/02/api-mocking-mirage-vue-javascript/) to see how I did that in Vue so you could replicate in whatever front-end framework you use.*

## Testing Environment

Mirage has two environments: **development** (default) and **test**. In development mode, the Mirage server will have a default response time of 400ms(which you can customize. See the third article of this series for that), logs all server responses to the console, and loads the development seeds.

However, in the test environment, we have:

- 0 delays to keep our tests fast
- Mirage suppresses all logs so as not to pollute your CI logs
- Mirage will also ignore the `seeds()` function so that your seed data can be used solely for development but won’t leak into your tests. This helps keep your tests deterministic.

Let’s update our `makeServer` so we can have the benefit of the test environment. To do that, we’ll make it accept an object with the environment option(we will default it to development and override it in our test). Our `server.js` should now look like this:

<pre><code class="language-javascript">// src/server.js
import { Server, Model, Factory } from 'miragejs';

export function makeServer({ environment = 'development' } = {}) {
  let server = new Server({
    environment,

    models: {
      product: Model,
    },
    factories: {
      product: Factory.extend({
        name(i) {
          return `Product ${i}`;
        },
      }),
    },

    routes() {
      this.namespace = 'api';

      this.get('/products', ({ products }) => {
        return products.all();
      });
    },
    seeds(server) {
      server.createList('product', 5);
    },
  });
  return server;
}
</code></pre>

Also note that we are passing the environment option to the Mirage server instance using the [ES6 property shorthand](https://es6-features.org/#PropertyShorthand). Now with this in place, let’s update our test to override the environment value to test. Our test now looks like this:

<pre><code class="language-javascript">import { makeServer } from '/path/to/server';

let server;

beforeEach(() => {
  server = makeServer({ environment: 'test' });
});

afterEach(() => {
  server.shutdown();
});

it('shows the products', function() {
  server.createList('product', 5);

  cy.visit('/');

  cy.get('li.product').should('have.length', 5);
});
</code></pre>

## AAA Testing

Mirage encourages a standard for testing called the triple-A or AAA testing approach. This stands for **Arrange**, **Act** and **Assert**. You could see this structure in our above test already:

<pre><code class="language-javascript">it("shows all the products", function () {
  // ARRANGE
  server.createList("product", 5)

  // ACT
  cy.visit("/")

  // ASSERT
  cy.get("li.product").should("have.length", 5)
})
</code></pre>

You might need to break this pattern but 9 times out of 10 it should work just fine for your tests.

{{% ad-panel-leaderboard %}}

## Let’s Test Errors

So far, we’ve tested our homepage to see if it has 5 products, however, what if the server is down or something went wrong with fetching the products? We don’t need to wait for the server to be down to work on how our UI would look like in such a case. We can simply simulate that scenario with Mirage.

Let’s return a 500 (Server error) when the user is on the homepage. As we have seen in a previous article, to customize Mirage responses we make use of the Response class. Let’s import it and write our test.

<div class="break-out">

 <pre><code class="language-javascript">homepage.test.js
import { Response } from "miragejs"

it('shows an error when fetching products fails', function() {
  server.get('/products', () => {
    return new Response(
      500,
      {},
      { error: "Can’t fetch products at this time" }
    );
  });

  cy.visit('/');

  cy.get('div.error').should('contain', "Can’t fetch products at this time");
});
</code></pre>
</div>

What a world of flexibility! We just override the response Mirage would return in order to test how our UI would display if it failed fetching products. Our overall `homepage.test.js` file would now look like this:

<div class="break-out">

 <pre><code class="language-javascript">// homepage.test.js
import { Response } from 'miragejs';
import { makeServer } from 'path/to/server';

let server;

beforeEach(() => {
  server = makeServer({ environment: 'test' });
});

afterEach(() => {
  server.shutdown();
});

it('shows the products', function() {
  server.createList('product', 5);

  cy.visit('/');

  cy.get('li.product').should('have.length', 5);
});

it('shows an error when fetching products fails', function() {
  server.get('/products', () => {
    return new Response(
      500,
      {},
      { error: "Can’t fetch products at this time" }
    );
  });

  cy.visit('/');

  cy.get('div.error').should('contain', "Can’t fetch products at this time");
});
</code></pre>
</div>

Note the modification we did to the `/api/products` handler only lives in our test. That means it works as we previously define when you are in development mode.

So when we run our tests, both should pass.

**Note**: *I believe its worthy of noting that the elements we are querying for in Cypress should exist in your front-end UI. Cypress doesn’t create HTML elements for you.*

## Testing The Product Detail Page

Finally, let’s test the UI of the product detail page. So this is what we are testing for:

- User can see the product name on the product detail page

Let’s get to it. First, we create a new test to test this user flow.

Here is the test:

<pre><code class="language-javascript">it("shows the product’s name on the detail route", function() {
  let product = this.server.create('product', {
    name: 'Korg Piano',
  });

  cy.visit(`/${product.id}`);

  cy.get('h1').should('contain', 'Korg Piano');
});
</code></pre>

Your `homepage.test.js` should finally look like this.

<div class="break-out">

 <pre><code class="language-javascript">// homepage.test.js
import { Response } from 'miragejs';
import { makeServer } from 'path/to/server;

let server;

beforeEach(() => {
  server = makeServer({ environment: 'test' });
});

afterEach(() => {
  server.shutdown();
});

it('shows the products', function() {
  console.log(server);
  server.createList('product', 5);

  cy.visit('/');

  cy.get('li.product').should('have.length', 5);
});

it('shows an error when fetching products fails', function() {
  server.get('/products', () => {
    return new Response(
      500,
      {},
      { error: "Can’t fetch products at this time" }
    );
  });

  cy.visit('/');

  cy.get('div.error').should('contain', "Can’t fetch products at this time");
});

it("shows the product’s name on the detail route", function() {
  let product = server.create('product', {
    name: 'Korg Piano',
  });

  cy.visit(`/${product.id}`);

  cy.get('h1').should('contain', 'Korg Piano');
});
</code></pre>
</div>

When you run your tests, all three should pass.

## Wrapping Up

It’s been fun showing you the inners of Mirage JS in this series. I hope you have been better equipped to start having a better front-end development experience by using Mirage to mock out your back-end server. I also hope you’ll use the knowledge from this article to write more acceptance/UI/end-to-end tests for your front-end applications.

- [Part 1](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/): Understanding Mirage JS Models And Associations
- [Part 2](https://www.smashingmagazine.com/2020/05/mirage-javascript-factories-fixtures-serializers/): Understanding Factories, Fixtures And Serializers
- [Part 3](https://www.smashingmagazine.com/2020/06/mirage-javascript-timing-response-passthrough/): Understanding Timing, Response And Passthrough
- Part 4: **Using Mirage JS And Cypress For UI Testing**

{{< signature "ra, il" >}}

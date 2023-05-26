---
title: 'Mirage JS Deep Dive: Understanding Factories, Fixtures And Serializers (Part 2)'
slug: mirage-javascript-factories-fixtures-serializers
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/343dbc90-8c54-47de-8d2e-449e796197a2/mirage-javascript-factories-fixtures-serializers.png
date: 2020-05-29T11:00:00.000Z
summary: >-
  In this second part of the Mirage JS Deep Dive series, we will be looking at Mirage JS’ Factories, Fixtures, and Serializers. We’ll see how they enable rapid API mocking using Mirage.
description: >-
  In this second part of the Mirage JS Deep Dive series, we will be looking at Mirage JS’ Factories, Fixtures, and Serializers. We’ll see how they enable rapid API mocking using Mirage.
categories:
  - API
  - JavaScript
---

In the [previous](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/) article of this series, we understudied Models and Associations as they relate to Mirage. I explained that Models allow us to create dynamic mock data that Mirage would serve to our application when it makes a request to our mock endpoints. In this article, we will look at three other Mirage features that allow for even more rapid API mocking. Let’s dive right in!

**Note**: *I highly recommend reading my first two articles if you haven’t to get a really solid handle on what would be discussed here. You could however still follow along and reference the previous articles when necessary.*

* [Setting Up API Mocking With Mirage JS And Vue](https://www.smashingmagazine.com/2020/02/api-mocking-mirage-vue-javascript/)
* [Mirage JS Models And Associations](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/)

## Factories

In a [previous article](https://www.smashingmagazine.com/2020/02/api-mocking-mirage-vue-javascript/), I explained how Mirage JS is used to mock backend API, now let’s assume we are mocking a product resource in Mirage. To achieve this, we would create a **route handler** which will be responsible for intercepting requests to a particular endpoint, and in this case, the endpoint is `api/products`. The route handler we create will return all products. Below is the code to achieve this in Mirage:

<pre><code class="language-javascript">import { Server, Model } from 'miragejs';

new Server({
    models: {
      product: Model,
    },

   routes() {
        this.namespace = "api";
        this.get('products', (schema, request) => {
        return schema.products.all()
    })
   }
});
    },
</code></pre>

The output of the above would be:

<pre><code class="language-json">{
  "products": []
}
</code></pre>

We see from the output above that the product resource is empty. This is however expected as we haven't created any records yet.

**Pro Tip**: *Mirage provides shorthand needed for conventional API endpoints. So the route handler above could also be as short as: `this.get('/products')`.*

{{% feature-panel %}}

Let’s create records of the `product` model to be stored in Mirage database using the `seeds` method on our `Server` instance:

<pre><code class="language-javascript"> seeds(server) {
      server.create('product', { name: 'Gemini Jacket' })
      server.create('product', { name: 'Hansel Jeans' })
  },
</code></pre>

The output:

<pre><code class="language-json">{
  "products": [
    {
      "name": "Gemini Jacket",
      "id": "1"
    },
    {
      "name": "Hansel Jeans",
      "id": "2"
    }
  ]
}
</code></pre>

As you can see above, when our frontend application makes a request to `/api/products`, it will get back a collection of products as defined in the `seeds` method. 

Using the `seeds` method to seed Mirage’s database is a step from having to manually create each entry as an object. However, it wouldn't be practical to create 1000(or a million) new product records using the above pattern. Hence the need for **factories**.

### Factories Explained

Factories are a faster way to create new database records. They allow us to quickly create multiple records of a particular model with variations to be stored in the Mirage JS database.

Factories are also objects that make it easy to generate realistic-looking data without having to seed those data individually. Factories are more of  **recipes** or **blueprints** for creating records off models.

### Creating A Factory

Let’s examine a Factory by creating one. The factory we would create will be used as a blueprint for creating new products in our Mirage JS database.

<pre><code class="language-javascript">import { Factory } from 'miragejs'

new Server({
    // including the model definition for a better understanding of what’s going on
    models: {
        product: Model
    },
    factories: {
        product: Factory.extend({})
    }
})
</code></pre>

From the above, you’d see we added a `factories` property to our `Server` instance and define another property inside it that by convention is of the same name as the model we want to create a factory for, in this case, that model is the `product` model. The above snippet depicts the pattern you would follow when creating factories in Mirage JS.

Although we have a factory for the `product` model, we really haven't added properties to it. The properties of a factory can be simple types like **strings**, **booleans** or **numbers**, or **functions** that return dynamic data as we would see in the full implementation of our new product factory below:

<div class="break-out">

 <pre><code class="language-javascript">import { Server, Model, Factory } from 'miragejs'

new Server({
    models: {
        product: Model
    },

   factories: {
      product: Factory.extend({
        name(i) {
          //  i is the index of the record which will be auto incremented by Mirage JS
          return `Awesome Product ${i}`; // Awesome Product 1, Awesome Product 2, etc.
        },
        price() {
          let minPrice = 20;
          let maxPrice = 2000;
          let randomPrice =
            Math.floor(Math.random() * (maxPrice - minPrice + 1)) + minPrice;
          return `$ ${randomPrice}`;
        },
        category() {
          let categories = [
            'Electronics',
            'Computing',
            'Fashion',
            'Gaming',
            'Baby Products',
          ];
          let randomCategoryIndex = Math.floor(
            Math.random() * categories.length
          );
          let randomCategory = categories[randomCategoryIndex];
          return randomCategory;
        },
         rating() {
          let minRating = 0
          let maxRating = 5
          return Math.floor(Math.random() * (maxRating - minRating + 1)) + minRating;
        },
      }),
    },
})
</code></pre>
</div>

In the above code snippet, we are specifying some javascript logic via `Math.random` to create dynamic data each time the factory is used to create a new product record. This shows the strength and flexibility of Factories. 

Let’s create a product utilizing the factory we defined above. To do that, we call `server.create` and pass in the model name (`product`) as a string. Mirage will then create a new record of a product using the product factory we defined. The code you need in order to do that is the following:

<pre><code class="language-javascript">new Server({
    seeds(server) {
        server.create("product")
    }
})
</code></pre>

**Pro Tip**: *You can run `console.log(server.db.dump())` to see the records in Mirage’s database.*

A new record similar to the one below was created and stored in the Mirage database.

<pre><code class="language-json">{
  "products": [
    {
      "rating": 3,
      "category": "Computing",
      "price": "$739",
      "name": "Awesome Product 0",
      "id": "1"
    }
  ]
}
</code></pre>

### Overriding factories

We can override some or more of the values provided by a factory by explicitly passing them in like so:

<div class="break-out">

 <pre><code class="language-javascript">server.create("product", {name: "Yet Another Product", rating: 5, category: "Fashion" })
</code></pre>
</div>

The resulting record would be similar to:

<pre><code class="language-json">{
  "products": [
    {
      "rating": 5,
      "category": "Fashion",
      "price": "$782",
      "name": "Yet Another Product",
      "id": "1"
    }
  ]
}
</code></pre>

### createList

With a factory in place, we can use another method on the server object called `createList`. This method allows for the creation of multiple records of a particular model by passing in the model name and the number of records you want to be created. Below is it’s usage:

<pre><code class="language-javascript">server.createList("product", 10)
</code></pre>

Or

<pre><code class="language-javascript">server.createList("product", 1000)
</code></pre>

As you’ll observe, the `createList` method above takes two arguments: the model name as a string and a non-zero positive integer representing the number of records to create. So from the above, we just created 500 records of products! This pattern is useful for UI testing as you’ll see in a future article of this series.

{{% ad-panel-leaderboard %}}

## Fixtures

In software testing, a **test fixture** or **fixture** is a state of a set or collection of objects that serve as a baseline for running tests. The main purpose of a fixture is to ensure that the test environment is well known in order to make results repeatable.

Mirage allows you to create fixtures and use them to seed your database with initial data.

**Note**: *It is recommended you use factories 9 out of 10 times though as they make your mocks more maintainable.*

### Creating A Fixture

Let’s create a simple fixture to load data onto our database:

<pre><code class="language-javascript"> fixtures: {
      products: [
        { id: 1, name: 'T-shirts' },
        { id: 2, name: 'Work Jeans' },
      ],
  },
</code></pre>

The above data is automatically loaded into the database as Mirage’s initial data. However, if you have a seeds function defined, Mirage would ignore your fixture with the assumptions that you meant for it to be overridden and instead use factories to seed your data.

### Fixtures In Conjunction With Factories

Mirage makes provision for you to use Fixtures alongside Factories. You can achieve this by calling `server.loadFixtures()`. For example:

<pre><code class="language-javascript"> fixtures: {
    products: [
      { id: 1, name: "iPhone 7" },
      { id: 2, name: "Smart TV" },
      { id: 3, name: "Pressing Iron" },
    ],
  },

  seeds(server) {
    // Permits both fixtures and factories to live side by side
    server.loadFixtures()

    server.create("product")
  },
</code></pre>

### Fixture files

Ideally, you would want to create your fixtures in a separate file from `server.js` and import it. For example you can create a directory called `fixtures` and in it create `products.js`. In `products.js` add:

<pre><code class="language-javascript">// &lt;PROJECT-ROOT&gt;/fixtures/products.js
export default [
  { id: 1, name: 'iPhone 7' },
  { id: 2, name: 'Smart TV' },
  { id: 3, name: 'Pressing Iron' },
];
</code></pre>

Then in `server.js` import and use the products fixture like so:

<pre><code class="language-javascript">import products from './fixtures/products';
 fixtures: {
    products,
 },
</code></pre>

I am using ES6 property shorthand in order to assign the products array imported to the `products` property of the fixtures object.

It is worthy of mention that fixtures would be ignored by Mirage JS during tests except you explicitly tell it not to by using `server.loadFixtures()`

### Factories vs. Fixtures

In my opinion, you should abstain from using fixtures except you have a particular use case where they are more suitable than factories. Fixtures tend to be more verbose while factories are quicker and involve fewer keystrokes.

## Serializers

It’s important to return a JSON payload that is expected to the frontend hence **serializers**. 

<blockquote>A serializer is an object that is responsible for transforming a **Model** or **Collection** that’s returned from your route handlers into a JSON payload that’s formatted the way your frontend app expects.<br /><br />Mirage Docs</blockquote>

Let’s take this route handler for example:

<pre><code class="language-javascript">this.get('products/:id', (schema, request) => {
        return schema.products.find(request.params.id);
      });
</code></pre>

A Serializer is responsible for transforming the response to something like this:

<pre><code class="language-json">{
  "product": {
    "rating": 0,
    "category": "Baby Products",
    "price": "$654",
    "name": "Awesome Product 1",
    "id": "2"
  }
}
</code></pre>

### Mirage JS Built-in Serializers

To work with Mirage JS serializers, you’d have to choose which built-in serializer to start with. This decision would be influenced by the type of JSON your backend would eventually send to your front-end application. Mirage comes included with the following serializers:

* `JSONAPISerializer`  
This serializer follows the [JSON:API spec](https://jsonapi.org/).
* `ActiveModelSerializer`  
This serializer is intended to mimic APIs that resemble Rails APIs built with the [active_model_serializer gem](https://github.com/rails-api/active_model_serializers).
* `RestSerializer`  
The `RestSerializer` is Mirage JS "catch all" serializer for other common APIs.

{{% ad-panel-leaderboard %}}

## Serializer Definition

To define a serialize, import the appropriate serializer e.g `RestSerializer` from `miragejs` like so:

<pre><code class="language-javascript">import { Server, RestSerializer } from "miragejs"
</code></pre>

Then in the `Server` instance:

<pre><code class="language-javascript">new Server({
  serializers: {
    application: RestSerializer,
  },
})
</code></pre>

The `RestSerializer` is used by Mirage JS by default. So it’s redundant to explicitly set it. The above snippet is for exemplary purposes.

Let’s see the output of both `JSONAPISerializer` and `ActiveModelSerializer` on the same route handler as we defined above

## JSONAPISerializer

<pre><code class="language-javascript">import { Server, JSONAPISerializer } from "miragejs"
new Server({
  serializers: {
    application: JSONAPISerializer,
  },
})
</code></pre>

The output:

<pre><code class="language-json">{
  "data": {
    "type": "products",
    "id": "2",
    "attributes": {
      "rating": 3,
      "category": "Electronics",
      "price": "$1711",
      "name": "Awesome Product 1"
    }
  }
}
</code></pre>

## ActiveModelSerializer

To see the ActiveModelSerializer at work, I would modify the declaration of `category` in the products factory to:

<pre><code class="language-javascript">productCategory() {
          let categories = [
            'Electronics',
            'Computing',
            'Fashion',
            'Gaming',
            'Baby Products',
          ];
          let randomCategoryIndex = Math.floor(
            Math.random() * categories.length
          );
          let randomCategory = categories[randomCategoryIndex];
          return randomCategory;
        },
</code></pre>

All I did was to change the name of the property to `productCategory` to show how the serializer would handle it.

Then, we define the `ActiveModelSerializer` serializer like so:

<pre><code class="language-javascript">import { Server, ActiveModelSerializer } from "miragejs"
new Server({
  serializers: {
    application: ActiveModelSerializer,
  },
})
</code></pre>

The serializer transforms the JSON returned as:

<pre><code class="language-json">{
  "rating": 2,
  "product_category": "Computing",
  "price": "$64",
  "name": "Awesome Product 4",
  "id": "5"
}
</code></pre>

You’ll notice that `productCategory` has been transformed to `product_category` which conforms to the [active_model_serializer gem](https://github.com/rails-api/active_model_serializers) of the Ruby ecosystem.

## Customizing Serializers

Mirage provides the ability to customize a serializer. Let’s say your application requires your attribute names to be camelcased, you can override `RestSerializer` to achieve that. We would be utilizing the `lodash` utility library:

<pre><code class="language-javascript">import { RestSerializer } from 'miragejs';
import { camelCase, upperFirst } from 'lodash';
serializers: {
      application: RestSerializer.extend({
        keyForAttribute(attr) {
          return upperFirst(camelCase(attr));
        },
      }),
    },
</code></pre>

This should produce JSON of the form:

<pre><code class="language-json"> {
      "Rating": 5,
      "ProductCategory": "Fashion",
      "Price": "$1386",
      "Name": "Awesome Product 4",
      "Id": "5"
    }
</code></pre>

## Wrapping Up

You made it! Hopefully, you’ve got a deeper understanding of Mirage via this article and you’ve also seen how utilizing factories, fixtures, and serializers would enable you to create more production-like API mocks with Mirage.

- [Part 1](https://www.smashingmagazine.com/2020/04/miraje-js-models-associations/): Understanding Mirage JS Models And Associations
- Part 2: **Understanding Factories, Fixtures And Serializers**
- [Part 3](https://www.smashingmagazine.com/2020/06/mirage-javascript-timing-response-passthrough/): Understanding Timing, Response And Passthrough 
- [Part 4](https://www.smashingmagazine.com/2020/06/mirage-javascript-cypress-ui-testing): Using Mirage JS And Cypress For UI Testing

{{< signature "ra, il" >}}

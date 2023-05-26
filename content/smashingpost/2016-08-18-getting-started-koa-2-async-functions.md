---
title: Building A Server-Side Application With Async Functions and Koa 2
slug: getting-started-koa-2-async-functions
image: 'https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9ef0b58d-bfb2-4a42-9eed-33ce2b83800f/koa-2.png'
date: 2016-08-18T15:57:06.000Z
author: alexrudenko
description: >-
  One of the upcoming features of JavaScript that I especially like is the
  [support for asynchronous
  functions](https://tc39.github.io/ecmascript-asyncawait/). In this article, I
  would like to show you a very practical example of building a **server-side
  application using Koa 2**, a new version of the web framework, which relies
  heavily on this feature.

  First, I’ll recap what async functions are and how they work. Then, I’ll
  highlight the differences between Koa 1 and Koa 2\. After that, I will
  describe my demo app for Koa 2, covering all aspects of development, including
  testing (using Mocha, Chai and Supertest) and deployment (using PM2).
categories:
  - Coding
  - Frameworks
  - JavaScript
  - API
---
One of the upcoming features of JavaScript that I especially like is the <a href="https://tc39.github.io/ecmascript-asyncawait/">support for asynchronous functions</a>. In this article, I would like to show you a very practical example of building a <strong>server-side application using Koa 2</strong>, a new version of the web framework, which relies heavily on this feature.

First, I’ll recap what async functions are and how they work. Then, I’ll highlight the differences between Koa 1 and Koa 2. After that, I will describe my demo app for Koa 2, covering all aspects of development, including testing (using Mocha, Chai and Supertest) and deployment (using PM2).</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Understanding JavaScript’s Function.prototype.bind](https://www.smashingmagazine.com/2014/01/understanding-javascript-function-prototype-bind/)
*   [Server-Side Rendering With React, Node And Express](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
*   [Why You Should Consider React Native For Your Mobile App](https://www.smashingmagazine.com/2016/04/consider-react-native-mobile-app/)

## Async Functions

The old problem of complex JavaScript applications is how to deal with callbacks and how to structure the code to avoid so-called “callback hell.” Several solutions have been developed over time, some of which are still based on callbacks and others that rely on more recent features of JavaScript — <strong>promises and generators</strong>. Let’s compare callbacks, promises and generators using the example of a function that fetches two JSON files in sequence.
<pre class="language-javascript"><code>// Fetch two files with callbacks
function doWork(cb) {
  fetch('data1.json', (err1, result1) =&gt; {
    if (err1) {
      return cb(err1);
    }
    fetch('data2.json', (err2, result2) =&gt; {
      if (err2) {
        return cb(err2);
      }
      cb(null, {
        result1,
        result2,
      });
    })
  });
}</code>
</pre>

Nested anonymous inline callback functions are the primary indicator of callback hell. You could restructure the code and split the functions into modules, but you would have to rely on callbacks anyway.
<pre class="language-javascript"><code class="language-javascript">// Fetch two files with promises
function doWork(cb) {
  fetch('data1.json')
    .then(result1 =&gt;
      fetch('data2.json')
        .then(result2 =&gt; cb(null, {
          result1,
          result2,
        })))
    .catch(cb);
}</code>
</pre>

The promise-based version looks a bit better, but the calls are still nested and we need to reorganize the code to appear sequential.
<pre class="language-javascript"><code class="language-javascript">// Fetch two files with generators
function* doWork() {
  var result1 = yield fetch('data1.json');
  var result2 = yield fetch('data2.json');
  return { result1, result2 };
}</code>
</pre>

Generators allow for the shortest solution, and this looks like normal synchronous code, whereas the callback and promise snippets are clearly asynchronous and highly nested. Nevertheless, the generator solution requires that we change the function type to the generator function by adding <code>*</code> after the <code>function</code> keyword, and it requires the special way to invoke <code>doWork</code>. This looks somewhat unintuitive, and the <code>async/await</code> syntax addresses this drawback by providing better abstraction. Look at the same example using async functions:
<pre class="language-javascript"><code class="language-javascript">async function doWork() {
  // Fetch two files with async/await
  var result1 = await fetch('data1.json');
  var result2 = await fetch('data2.json');
  return { result1, result2 };
}</code></pre>

{{% feature-panel %}}

This syntax can be interpreted as follows: Functions marked with the <code>async</code> keyword allow us to use the <code>await</code> keyword in them, which pauses the execution of the function to wait for the asynchronous operations to finish. The asynchronous operation can be represented by a generator, a promise or another async function. Also, you can use <code>try</code>/<code>catch</code> to handle any errors or rejections that occur during the async operations that you <code>await</code>. The same error-handling mechanism is possible with the generator-based control flow.</p>

## What is Koa?

Koa is positioned as a next generation web framework and it was designed by the people who created Express (and in particular, by <a href="https://github.com/tj">TJ</a>). Koa is very lightweight and modular and allows writing code without using callbacks. Koa application is an array of middleware functions that run in sequence processing incoming requests and providing a response. Every middleware function has the access to the context object that wraps native node request and response objects and provides an improved API to work with them. Basic Koa application looks like this:
<pre class="language-javascript"><code class="language-javascript">// This is Koa 1
var koa = require('koa');
var app = koa();

app.use(function *(){
  this.body = 'Hello World';
});

app.listen(3000);
</code></pre>

This is not much except for this in the Koa core. Advanced functionality is provided by 3rd-party modules.</p>

## Koa 2 Versus Koa 1

Koa 1 is famous for its early adoption of generators and for supporting generator-based control out of the box. This is what a typical piece of code for Koa 1 that uses the middleware cascading and improved error handling looks like:
<pre class="language-javascript"><code class="language-javascript">// Adapted from https://github.com/koajs/koa
// In Koa 1.0, middleware is a generator function.
app.use(function *(next) {
  try {
    yield next;
  } catch (err) {
    // the request context is &lt;code&gt;this&lt;/code&gt;
    this.body = { message: err.message }
    this.status = err.status || 500
  }
})

app.use(function *(next) {
  const user = yield User.getById(this.session.id);
  this.body = user;
})</code></pre>

Koa 2 removes built-in support for generators and uses async functions instead. The signature of middleware functions will change to support <code>async</code> arrow functions. Here is what the same code looks like written for Koa 2:
<pre class="language-javascript"><code class="language-javascript">// Taken from https://github.com/koajs/koa
// Uses async arrow functions
app.use(async (ctx, next) = &gt; {
  try {
    await next(); // next is now a function, await instead of yield
  } catch (err) {
    ctx.body = { message: err.message };
    ctx.status = err.status || 500;
  }
});

app.use(async ctx =&gt; {
  // await instead of yield
  const user = await User.getById(ctx.session.id);
  // ctx instead of this
  ctx.body = user;
});</code></pre>

Using normal functions, promises and generator functions is still possible, as described in the <a href="https://github.com/koajs/koa/tree/v2.x#common-function">documentation for Koa 2</a>.</p>

## Koa Versus Express

Koa is a simpler and leaner framework than Express, built on top of the Node.js’ HTTP module. Express provides built-in features for routing, templating and sending files and other features, whereas Koa provides the very minimum, as well as a generator-based (Koa 1) or async/await-based (Koa 2) control flow. Routing, templating and other features are provided as separate modules by the community, and normally there are several alternatives to choose from. The Koa section of GitHub has a <a href="https://github.com/koajs/koa/blob/master/docs/koa-vs-express.md">document with additional insight</a> on the differences between Koa and Express.</p>

## Status of Koa 2

Koa 2 will be released once the async/await feature is available in Node.js natively. Fortunately, async/await and Koa 2.0 can be tested right now using Babel. We will get to this soon. First, let’s go over the scope of the app that I built to demonstrate Koa 2 and async functions.</p>

## Demo App

The goal here is to build a simple app that tracks page views for a static website — something like Google Analytics but much simpler. The app will have two endpoints:

*   one to store the information about an event (for example, a page view);
*   and one to get the total number of events;
*   additionally, the endpoints have to be secured with an API key.

Redis will be used to store the events data. The functionality will be tested by unit and API tests. The full source code of the app is <a href="https://github.com/OrKoN/koa2-example-app">available on Github</a>.</p>

### App Dependencies

Let’s start with the list of modules needed for the app, along with explanations for why they are needed. First, here are the dependencies needed at runtime:

<pre><code class="language-bash">npm install --save \
  # babel-polyfill provides the runtime that async functions need
  babel-polyfill \
  # The Koa framework itself
  koa@next \
  # Because Koa is minimalist, we need a parser
  # to parse JSON in the body of requests
  koa-bodyparser@next \
  # and the router
  koa-router@next \
  # The redis module to store the app's data
  redis\
  # The Koa cors module to allow cross-origin requests
  kcors@next</code>
</pre>

Note that the version for Koa modules we are using is <code>next</code>. This means that this version will be compatible with Koa 2, and many modules already provide it. Here are the modules needed for development and testing:

<pre><code class="language-bash">npm install --save-dev \
  # To write assertions in our tests
  chai \
  # A popular testing framework
  mocha \
  # API-level tests
  supertest \
  # Babel CLI to build our app
  babel-cli \
  # A set of Babel plugins to support ES6 features
  babel-preset-es2015 \
  # and to support stage-3 features
  babel-preset-stage-3 \
  # Overrides Node.js's require and compiles modules at runtime
  babel-register \
  # To watch JavaScript files in development and restart the server
  # if there are changes in the files
  nodemon </code></pre>

### How to Organize the Application?

After trying out several ways to organize the application’s files, I came up with the following simple structure that is suitable for small apps and small teams:

*   `index.js` The main entry point of the app
*   `ecosystem.json` The PM2 ecosystem, which describes how to start the app
*   `src` The source of the app, containing JavaScript files to be compiled by Babel
*   `config` The app’s configuration files
*   `build` The build of the app, containing the compiled code from `src`The `src` directory contains the following:
    *   `api.js` The module that defines the app’s API
    *   `app.js` The module that instantiates and configures the Koa app’s instance
    *   `config.js` The module that provides the configuration of the app to other modulesIf additional files or modules are needed as the app grows, we would put them in a subfolder of the `src` folder — for example, `src/models` for application models, `src/routes` for more modular API definitions, `src/gateways` for modules that interact with external services, and so on.

    ### NPM Scripts As A Task Runner

    After using Gulp and Grunt as task runners, I came to the conclusion that npm scripts are better than separate tools when working on server-side projects. One of the advantages of npm scripts is that they allow you to invoke locally installed modules as if there were globally installed. I use the following scripts, which need to be defined in `package.json`:

        "scripts": {
          "start": "node index.js",
          "watch": "nodemon --exec npm run start",
          "build": "babel src -d build",
          "test": "npm run build; mocha --require 'babel-polyfill' --compilers js:babel-register"
        }

    The `start` script simply runs `index.js`. The `watch` script runs the `start` script using the nodemon tool, which automatically restarts the server whenever you change something in the app. Note that nodemon is installed as a local development dependency and does not have to be installed globally. The `build` script compiles the files in the `src` folder using Babel and outputs the results to the `build` folder. The `test` script runs the `build` script first and then runs tests using `mocha`. Mocha requires two modules: `babel-polyfill`, to provide runtime dependencies of the compiled code, and `babel-register`, to compile the test files before executing them. Additionally, presets for Babel have to be added to `package.json`, so that you don’t have to provide them in the command line:

        {
          "babel": {
            "presets": [
              "es2015",
              "stage-3"
            ]
          }
        }

    This preset enable all ECMAScript 2015 features, as well as features that are currently in [stage 3](https://github.com/tc39/ecma262#current-proposals). With this installed and configured, we can start developing the app.

    ### The Application’s Code

    First, let’s look at `index.js`:

        const port = process.env.PORT || 4000;
        const env = process.env.NODE_ENV || 'development';
        const src = env === 'production' ? './build/app' : './src/app';

        require('babel-polyfill');
        if (env === 'development') {
          // for development use babel/register for faster runtime compilation
          require('babel-register');
        }

        const app = require(src).default;
        app.listen(port);

    The module reads two environmental variables: `PORT` and `NODE_ENV`. `NODE_ENV` should be either `development` or `production`. In development mode, `babel-register` will be used to compile modules at runtime. `babel-register` caches the results of the compilation and, thus, reduces the server start time, so that you can iterate faster during development. Because this module is not recommended for production use, the precompiled version from the `build` directory will be used in production mode. `index.js` is the only file of the project that will not be compiled by Babel and that must use native module syntax (i.e. CommonJS). Therefore, the app’s instance is located in the `default` property of the imported `app` module, which is an ECMAScript 6 module that exports the app’s instance as a default export:

        export default app;

    This is important to keep in mind if you mix ECMAScript 6 and CommonJS modules. Now to the `app.js` file itself. This and the other files discussed below are always compiled by Babel in both development and production environments, and the new syntax (including async functions) may be used freely in them:

        import Koa from 'koa';
        import api from './api';
        import config from './config';
        import bodyParser from 'koa-bodyparser';
        import cors from 'kcors';

        const app = new Koa()
          .use(cors())
          .use(async (ctx, next) => {
            ctx.state.collections = config.collections;
            ctx.state.authorizationHeader = `Key ${config.key}`;
            await next();
          })
          .use(bodyParser())
          .use(api.routes())
          .use(api.allowedMethods());

        export default app;

    Here, we are using ECMAScript 2015’s `import` syntax to import the required modules. Then, we create a new instance of the Koa application and attach several middleware functions to it using the `use` method. The last thing we do is export the app so that it can be used by `index.js`. The second middleware function in the chain is an async function and an arrow function at the same time:

        app.use(async (ctx, next) => {
          // Set up the request context
          ctx..state.collections = config.collections;
          ctx..state.authorizationHeader = `Key ${config.key}`;
          await next();
          // The execution will reach here only when
          // the next function returns and finishes all async tasks
          // console.log('Request is done');
        })

    In Koa 2, the `next` parameter is an async function that triggers the next middleware function in the list. Just like in Koa 1, you can control whether the current middleware function should do its job before or after the others by putting the call to `next` either at the beginning of the current function or at the end. Also, you can catch all errors in the downstream middleware functions by wrapping the `await next();` statement in a `try/catch` statement wherever doing so makes sense.

    ### Defining the API

    The `api.js` file is where the core logic of our app resides. Because Koa does not provide routing out of the box, the app has to use the `koa-router` module:

        import KoaRouter from 'koa-router';

        const api = KoaRouter();

    Here, `koa-router` provides functions to define middleware functions for specific HTTP methods and paths — for example, the route that stores events in the database:

        // Declare a post method and what it does
        // :collection is a parameter
        api.post('/:collection',
          // First, validate auth key
          validateKey,
          // Then, validate that the provided collection exists
          validateCollection,
          // Handle adding the new item to the collection
          async (ctx, next) => {
            // Use ES6 destructuring to extract the collection param
            const { collection } = ctx.params;
            // Wait until the persistence layer saves the item
            const count = await ctx
              .state
              .collections[collection]
              .add(ctx.request.body);

            // Reply with 201 Created when the item is saved
            ctx.status = 201;
          });

    Each method can have several handlers, which run sequentially and have exactly the same signature as the middleware functions defined in the top level of `app.js`. For example, `validateKey` and `validateCollection` are simply async functions that validate the incoming request and return 404 or 401 if the provided event collection does not exist or if the API key is not valid:

        const validateCollection = async (ctx, next) => {
          const { collection } = ctx.params;
          if (!(collection in ctx.state.collections)) {
            return ctx.throw(404);
          }
          await next();
        }

        const validateKey = async (ctx, next) => {
          const { authorization } = ctx.request.headers;
          if (authorization !== ctx.state.authorizationHeader) {
            return ctx.throw(401);
          }
          await next();
        }

    Note that arrow middleware functions cannot refer to the context of the current request using `this` (i.e. `this` is always undefined in the examples thus far). Therefore, request and response objects as well as Koa helpers are available in the context object (`ctx`). Koa 1 had no separate context object, and `this` referred to the current request context. After defining other [API methods](https://github.com/OrKoN/koa2-example-app/blob/master/src/api.js), we finally export the API to be connected to the Koa application in `app.js`:

        export default api;

    ### Persistence Layer

    In `api.js`, we accessed the `collections` array in the context `ctx`, which we initialized in `app.js`. These collection objects are responsible for storing and retrieving data stored in Redis. The `Collection` class is as follows:

        // Use promise-based Redis client
        const redis = require('promise-redis')();
        const db = redis.createClient();

        class Collection {

          // Full source:
          // https://github.com/OrKoN/koa2-example-app/blob/master/src/collection.js

          async count() {
            // We can `await` for promises
            // The await syntax allows us to work with
            // async calls as if they were synchronous
            var count = await db
              .zcount(this.name, '-inf', '+inf');
            return Number(count);
          }

          async add(event) {
            await db
              .zadd(this.name, 1, JSON.stringify(event));

            await this._incrGroups(event);
          }

          async _incrGroups(event) {
            // ES6 for:of syntax allows for easier iteration
            // groupBy is an array that holds possible attributes of the event
            for (let attr of this.groupBy) {
              // We can use await inside loops,
              // thus calling async operations sequentially in the loop
              await db.hincrby(`${this.name}_by_${attr}`, event[attr], 1);
            }
          }
        }

        export default Collection;

    The async/await syntax is really helpful here because it allows us to coordinate several async operations easily — for example, in a loop. But there is one important thing to keep in mind. Let’s look at the `_incrGroups` method:

        async _incrGroups(event) {
          // ES6 for:of syntax allows iterating easier
          for (let attr of this.groupBy) {
            // We can use await inside loops,
            // thus calling async operations sequentially in the loop
            await db.hincrby(`${this.name}_by_${attr}`, event[attr], 1);
          }
        }

    Here, the keys are incremented sequentially, meaning that the next key will be incremented once the previous incrementation has succeeded. But this kind of job can be done in parallel! With async/await, the task might not be easy to accomplish, but promises can help:

        // Start all increments in parallel
        // because there is no await inside the map callback here
        const promises = this.groupBy.map(attr =>
          db.hincrby(`${this.name}_by_${attr}`, event[attr], 1));
        // Wait for all of them to finish
        await Promise.all(promises);

    The interchangeability of promises and async functions is very helpful.

    ### Testing

    The app’s tests are located in the [`test` folder](https://github.com/OrKoN/koa2-example-app/tree/master/test). Let’s look at `apiSpec.js`, which represents the test specification for the app’s API:

        import { expect } from 'chai';
        import request from 'supertest';
        import app from '../build/app';
        import config from '../build/config';

    We import `expect` from `chai` and `supertest`. We use the precompiled version of the app and the config to make sure that we are testing exactly the same code that will be running in production. Next, we write the tests for the API, leveraging the async/await syntax to achieve sequential execution of the test steps:

        describe('API', () => {
          const inst = app.listen(4000);

          describe('POST /:collection', () => {
            it('should add an event', async () => {
              const page = 'https://google.com';
              const encoded = encodeURIComponent(page);
              const res = await request(inst)
                .post(<code>/pageviews</code>)
                .set({
                  Authorization: 'Key ' + config.key
                })
                .send({
                  time: 'now',
                  referrer: 'a',
                  agent: 'b',
                  source: 'c',
                  medium: 'd',
                  campaign: 'e',
                  page: page
                })
                .expect(201);
              // here res is available
              // you can use res.headers, res.body etc
              // no callback for <code>expect</code> or <code>end</code> functions is required.
              expect(res.body).to.be.empty;
            });
          });
        });

    Note that functions passed to `it` functions are marked with `async`. This means that `await` can be used to run asynchronous tasks, including the `supertest` requests, which return `then`-able objects and which, therefore, are compatible with what `await` expects.

    ### Deployment With PM2

    Once the app is ready and tests have passed, let’s prepare everything to run the app in production. For this, let’s declare `ecosystem.json`, which will hold the production configuration of the app:

        {
          "apps" : [
              {
                "name"        : "koa2-example-app",
                // The entry point to the compiled version of the app
                "script"      : "index.js",
                // In production, we don't want to watch for changes in files
                "watch"       : false,
                // And we want to merge logs from all instances
                "merge_logs"  : true,
                // We want to timestamp log messages
                "log_date_format": "YYYY-MM-DD HH:mm Z",
                "env": {
                  // And include environment variables for the app
                  "NODE_ENV": "production",
                  "PORT": 4000
                },
                // Start two processes of the app, and balance the load between them
                "instances": 2,
                // Start app as a cluster
                "exec_mode"  : "cluster_mode",
                // Watch failures and auto-restart processes
                "autorestart": true
              }
          ]
        }

    If your app requires additional servers (for example, a cron job), you can add them to `ecosystem.json`, and they will be started together with the main server. To start the app on the production server, you can run this:

        pm2 start ecosystem.json

    And to persist the configuration, you would run this:

        pm2 save

    PM2 provides some monitoring features (try `pm2 list`, `pm2 info`, `pm2 monit`). For example, PM2 shows how much memory your application is using. This basic Koa application consumes 44 MB per Node.js process.

    ### Conclusion

    Babel allows us to build apps using ECMAScript syntax that is not natively available but that includes async/await, which makes writing asynchronous code more enjoyable. The code that uses the async/await syntax is easier to read and maintain. Koa 2 and Babel allow you to start using async functions right now. Nevertheless, Babel brings additional overhead and requires additional configuration and an extra build step. Therefore, waiting until async/await is natively available in Node.js is recommended. Koa 2 should be officially released once this happens. Then, Koa 2 will be a good alternative to Express because it is more modular and simpler and allows for configuration the way you want it. The deployment section of this tutorial might be too simple and unscalable. It leaves open the question of how and when to build and actually deploy the code — you can do this manually (`rsync`, `scp`) or set up a continuous integration server for this. Also, the inner architecture of the app is too simple yet is suitable for a demo. Larger and more ambitious apps might require other entities, such as gateways, mappers, repositories and so on, but all of them can leverage async functions. I hope you’ve enjoyed this tutorial. Thanks for reading!

    #### Links

    *   [Koa](https://github.com/koajs/koa/wiki), GitHub A list of Koa modules
    *   “[Async Functions, Stage 3 Draft](https://tc39.github.io/ecmascript-asyncawait/),” Ecma International Technical Committee 39, GitHub The async specification
    *   [koa2-example-app](https://github.com/OrKoN/koa2-example-app) The full source code of our demo app
    *   “[Middleware](https://github.com/koajs/koa/wiki#middleware),” Koa, GitHub Middleware support for Koa 2
    *   “[Koa 2.0.0](https://github.com/koajs/koa/issues/533),” GitHub The GitHub issue to track the progress of Koa 2
    *   “[Async/Await implementation in V8](https://github.com/nodejs/promises/issues/4),” GitHub The GitHub issue to track the progress of Async/Await implementation in Node_(al)_


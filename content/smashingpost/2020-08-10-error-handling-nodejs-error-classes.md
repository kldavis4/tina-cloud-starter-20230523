---
title: 'Better Error Handling In NodeJS With Error Classes'
slug: error-handling-nodejs-error-classes
author: kelvin-omereshone
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2dbd0b35-8a07-4450-86b5-23e2a2a35b79/error-handling-nodejs-error-classes.png
date: 2020-08-10T10:00:00.000Z
summary: >-
  This article is for JavaScript and NodeJS developers who want to improve error-handling in their applications. Kelvin Omereshone explains the `error` class pattern and how to use it for a better, more efficient way of handling errors across your applications.
description: >-
  This article is for JavaScript and NodeJS developers who want to improve error-handling in their applications. Kelvin Omereshone explains the `error` class pattern and how to use it for a better, more efficient way of handling errors across your applications.
categories:
  - JavaScript
  - Node.js
  - Apps
---

Error handling is one of those parts of software development that don’t quite get the amount of attention it really deserves. However, building robust applications requires dealing with errors properly.

You can get by in NodeJS without properly handling errors but due to the asynchronous nature of NodeJS, improper handling or errors can cause you pain soon enough &mdash; especially when debugging applications.

Before we proceed, I would like to point out the type of errors we’ll be discussing how to utilize error classes.

## Operational Errors

These are errors discovered during the run time of a program. Operational errors are not bugs and can occur from time to time mostly because of one or a combination of several external factors like a database server timing out or a user deciding to make an attempt on SQL injection by entering SQL queries in an input field. 

Below are more examples of operational errors:

- Failed to connect to a database server;
- Invalid inputs by the user (server responds with a `400` response code);
- Request timeout;
- Resource not found (server responds with a 404 response code);
- Server returns with a `500` response.

It’s also worthy of note to briefly discuss the counterpart of Operational Errors.
 
## Programmer Errors

These are bugs in the program which can be resolved by changing the code. These types of errors can not be handled because they occur as a result of the code being broken. Example of these errors are:

* Trying to read a property on an object that is not defined.

<div class="break-out">

<pre><code class="language-javascript"> const user = {
   firstName: 'Kelvin',
   lastName: 'Omereshone',
 }

 console.log(user.fullName) // throws 'undefined' because the property fullName is not defined</code></pre>
</code>
</div>

* Invoking or calling an asynchronous function without a callback.
* Passing a string where a number was expected.

This article is about **Operational Error handling** in NodeJS. Error handling in NodeJS is significantly different from error handling in other languages. This is due to the asynchronous nature of JavaScript and the openness of JavaScript with errors. Let me explain:

In JavaScript, instances of the `error` class is not the only thing you can throw. You can literally throw any data type this openness is not allowed by other languages.

For example, a JavaScript developer may decide to throw in a number instead of an error object instance, like so:

<div class="break-out">

<pre><code class="language-javascript">// bad
throw 'Whoops :)';

// good
throw new Error('Whoops :)')
</code></pre>
</div>

You might not see the problem in throwing other data types, but doing so will result in a harder time debugging because you won’t get a stack trace and other properties that the [Error object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error) exposes which are needed for debugging.
 
Let’s look at some incorrect patterns in error handling, before taking a look at the Error class pattern and how it is a much better way for error handling in NodeJS.

{{% feature-panel %}}

## Bad Error Handling Pattern #1: Wrong Use Of Callbacks

**Real-world scenario**: *Your code depends on an external API requiring a callback to get the result you expect it to return.*

Let’s take the below code snippet:

<div class="break-out">

<pre><code class="language-javascript">'use strict';

const fs = require('fs');

const write = function () {
    fs.mkdir('./writeFolder');
    fs.writeFile('./writeFolder/foobar.txt', 'Hello World');
}

write();
</code></pre>
</div>

Until NodeJS 8 and above, the above code was legitimate, and developers would simply fire and forget commands. This means developers weren’t required to provide a callback to such function calls, and therefore could leave out error handling. What happens when the `writeFolder` hasn’t been created? The call to `writeFile` won’t be made and we wouldn’t know anything about it. This might also result in race condition because the first command might not have finished when the second command started again, you wouldn’t know.

Let’s start solving this problem by solving the race condition. We would do so by giving a callback to the first command `mkdir` to ensure the directory indeed exists before writing to it with the second command. So our code would look like the one below:

<div class="break-out">

<pre><code class="language-javascript">'use strict';

const fs = require('fs');

const write = function () {
    fs.mkdir('./writeFolder', () =&gt; {
        fs.writeFile('./writeFolder/foobar.txt', 'Hello World!');
    });
}

write();
</code></pre>
</div>

Though we solved the race condition, we are not done quite yet. Our code is still problematic because even though we used a callback for the first command, we have no way of knowing if the folder `writeFolder` was created or not. If the folder wasn’t created, then the second call will fail again but still, we ignored the error yet again. We solve this by...

### Error Handling With Callbacks

In order to handle error properly with callbacks, you must make sure you always use the error-first approach. What this means is that you should first check if there is an error returned from the function before going ahead to use whatever data(if any) was returned. Let’s see the wrong way of doing this:

<div class="break-out">

<pre><code class="language-javascript">'use strict';


// Wrong
const fs = require('fs');

const write = function (callback) {
    fs.mkdir('./writeFolder', (err, data) =&gt; {
        if (data) fs.writeFile('./writeFolder/foobar.txt', 'Hello World!');
        else callback(err)
    });
}

write(console.log);
</code></pre>
</div>

The above pattern is wrong because sometimes the API you are calling might not return any value or might return a falsy value as a valid return value. This would make you end up in an error case even though you might apparently have a successful call of the function or API.

The above pattern is also bad because it’s usage would eat up your error(your errors won’t be called even though it might have happened). You will also have no idea of what is happening in your code as a result of this kind of error handling pattern. So the right way for the above code would be:

<div class="break-out">

<pre><code class="language-javascript">'use strict';

// Right
const fs = require('fs');

const write = function (callback) {
    fs.mkdir('./writeFolder', (err, data) =&gt; {
        if (err) return callback(err)
        fs.writeFile('./writeFolder/foobar.txt', 'Hello World!');
    });
}

write(console.log);
</code></pre>
</div>

## Wrong Error Handling Pattern #2: Wrong Use Of Promises

**Real-world scenario**: *So you discovered Promises and you think they are way better than callbacks because of callback hell and you decided on promisifying some external API your code base depended upon. Or you are consuming a promise from an external API or a browser API like the fetch() function.*

These days we don’t really use callbacks in our NodeJS codebases, we use [promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). So let’s reimplement our example code with a promise:

<div class="break-out">

<pre><code class="language-javascript">'use strict';

const fs = require('fs').promises;

const write = function () {
    return fs.mkdir('./writeFolder').then(() =&gt; {
        fs.writeFile('./writeFolder/foobar.txt', 'Hello world!')
    }).catch((err) =&gt; {
        // catch all potential errors
        console.error(err)
    })
}
</code></pre>
</div>

Let’s put the above code under a microscope &mdash; we can see that we are branching off the `fs.mkdir` promise into another promise chain(the call to fs.writeFile) without even handling that promise call. You might think a better way to do it would be:

<div class="break-out">

<pre><code class="language-javascript">'use strict';

const fs = require('fs').promises;

const write = function () {
    return fs.mkdir('./writeFolder').then(() =&gt; {
        fs.writeFile('./writeFolder/foobar.txt', 'Hello world!').then(() =&gt; {
            // do something
        }).catch((err) =&gt; {
            console.error(err);
        })
    }).catch((err) =&gt; {
        // catch all potential errors
        console.error(err)
    })
}
</code></pre>
</div>

But the above would not scale. This is because if we have more promise chain to call, we would end up with something similar to the [callback hell](https://callbackhell.com/) which promises were made to solve. This means our code will keep indenting to the right. We would have a promise hell on our hands.

## Promisifying A Callback-Based API

Most times you would want to promisify a callback-based API on your own in order to better handle errors on that API. However, this is not really easy to do. Let’s take an example below to explain why.

<div class="break-out">

<pre><code class="language-javascript">function doesWillNotAlwaysSettle(arg) {
    return new Promise((resolve, reject) =&gt; {
       doATask(foo, (err) =&gt; {
           if (err) {
                return reject(err);
            }

            if (arg === true) {
                resolve('I am Done')
            }
        });
    });
}
</code></pre>
</div>

From the above, if `arg` is not `true` and we don’t have an error from the call to the `doATask` function then this promise will just hang out which is a [memory leak](https://en.wikipedia.org/wiki/Memory_leak) in your application.

### Swallowed Sync Errors In Promises

Using the Promise constructor has several difficulties one of these difficulties is; as soon as it is either resolved or rejected it cannot get another state. This is because a promise can only get a single state &mdash; either it is pending or it is resolved/rejected. This means we can have dead zones in our promises. Let’s see this in code:

<div class="break-out">

<pre><code class="language-javascript">function deadZonePromise(arg) {
    return new Promise((resolve, reject) =&gt; {
        doATask(foo, (err) =&gt; {
            resolve('I’m all Done');
            throw new Error('I am never reached') // Dead Zone
        });
    });
}
</code></pre>
</div>

From the above we see as soon as the promise is resolved, the next line is a dead zone  and will never be reached. This means any following synchronous error handling perform in your promises will just be swallowed and will never be thrown.

{{% ad-panel-leaderboard %}}

## Real-World Examples

The examples above help explain poor error handling patterns, let’s take a look at the sort of problems you might see in real-life.

### Real World Example #1 &mdash; Transforming Error To String

**Scenario**: *You decided the error returned from an API is not really good enough for you so you decided to add your own message to it.*

<div class="break-out">

<pre><code class="language-javascript">'use strict';

function readTemplate() {
    return new Promise(() =&gt; {
      databaseGet('query', function(err, data) {
          if (err) {
           reject('Template not found. Error: ', + err);
          } else {
            resolve(data);
          }
        });
    });
}

readTemplate();
</code></pre>
</div>

Let’s look at what is wrong with the above code. From the above we see the developer is trying to improve the error thrown by the `databaseGet` API by concatenating the returned error with the string "Template not found". This approach has a lot of downsides because when the concatenation was done, the developer implicitly runs `toString` on the error object returned. This way he loses any extra information returned by the error(say goodbye to stack trace). So what the developer has right now is just a string that is not useful when debugging.

A better way is to keep the error as it is or wrap it in another error that you’ve created and attached the thrown error from the databaseGet call as a property to it.

### Real-World Example #2: Completely Ignoring The Error

**Scenario**: *Perhaps when a user is signing up in your application, if an error occur you want to just catch the error and show a custom message but you completely ignored the error that was caught without even logging it for debugging purposes.*

<div class="break-out">

<pre><code class="language-javascript">router.get('/:id', function (req, res, next) {
    database.getData(req.params.userId)
    .then(function (data) {
        if (data.length) {
            res.status(200).json(data);
        } else {
            res.status(404).end();
        }
    })
    .catch(() =&gt; {
        log.error('db.rest/get: could not get data: ', req.params.userId);
        res.status(500).json({error: 'Internal server error'});
    })
});
</code></pre>
</div>

From the above, we can see that the error is completely ignored and the code is sending 500 to the user if the call to the database failed. But in reality, the cause for the database failure might be malformed data sent by the user which is an error with the status code of 400.

In the above case, we would be ending up in a debugging horror because you as the developer wouldn’t know what went wrong. The user won’t be able to give a decent report because 500 internal server error is always thrown. You would end up wasting hours in finding the problem which will tantamount to wastage of your employer’s time and money.

### Real-World Example #3: Not Accepting The Error Thrown From An API

**Scenario**: *An error was thrown from an API you were using but you don’t accept that error instead you marshall and transform the error in ways that make it useless for debugging purposes.*

Take the following code example below:

<div class="break-out">

<pre><code class="language-javascript">async function doThings(input) {
    try {
        validate(input);
        try {
            await db.create(input);
        } catch (error) {
            error.message = `Inner error: ${error.message}`

            if (error instanceof Klass) {
                error.isKlass = true;
            }

            throw error
        }
    } catch (error) {
        error.message = `Could not do things: ${error.message}`;
        await rollback(input);
        throw error;
    }
}
</code></pre>
</div>

A lot is going on in the above code that would lead to debugging horror. Let’s take a look:

* Wrapping `try/catch` blocks: You can see from the above that we are wrapping `try/catch` block which is a very bad idea. We normally try to reduce the use of `try/catch` blocks to minify the surface where we would have to handle our error (think of it as DRY error handling);
* We are also manipulating the error message in the attempt to improve which is also not a good idea;
* We are checking if the error is an instance of type `Klass` and in this case, we are setting a boolean property of the error `isKlass` to truev(but if that check passes then the error is of the type `Klass`);
* We are also rolling back the database too early because, from the code structure, there is a high tendency that we might not have even hit the database when the error was thrown.

Below is a better way to write the above code:

<div class="break-out">

<pre><code class="language-javascript">async function doThings(input) {
    validate(input);

    try {
        await db.create(input);
    } catch (error) {
        try {
            await rollback();
        } catch (error) {
            logger.log('Rollback failed', error, 'input:', input);
        }
        throw error;
    }
}
</code></pre>
</div>

Let’s analyze what we are doing right in the above snippet:

* We are using one `try/catch` block and only in the catch block are we using another `try/catch` block which is to serve as a guard in case something goes on with that rollback function and we are logging that;
* Finally, we are throwing our original received error meaning we don’t lose the message included in that error.

### Testing 

We mostly want to test our code(either manually or automatically). But most times we are only testing for the positive things. For a robust test, you must also test for errors and edge cases. This negligence is responsible for bugs finding their way into production which would cost more extra debugging time.

**Tip**: *Always make sure to test not only the positive things(getting a status code of 200 from an endpoint) but also all the error cases and all the edge cases as well.*

### Real-World Example #4: Unhandled Rejections

If you’ve used promises before, you have probably run into `unhandled rejections`. 

Here is a quick primer on unhandled rejections. Unhandled rejections are promise rejections that weren’t handled. This means that the promise was rejected but your code will continue running.

Let’s look at a common real-world example that leads to unhandled rejections..

<div class="break-out">

<pre><code class="language-javascript">'use strict';

async function foobar() {
    throw new Error('foobar');
}

async function baz() {
    throw new Error('baz')
}


(async function doThings() {
    const a = foobar();
    const b = baz();

    try {
        await a;
        await b;
    } catch (error) {
        // ignore all errors!
    }
})();
</code></pre>
</div>

The above code at first look might seem not error-prone. But on a closer look, we begin to see a defect. Let me explain: What happens when `a` is rejected? That means `await b` is never reached and that means its an unhandled rejection. A possible solution is to use `Promise.all` on both promises. So the code would read like so:

<div class="break-out">

<pre><code class="language-javascript">'use strict';

async function foobar() {
    throw new Error('foobar');
}

async function baz() {
    throw new Error('baz')
}


(async function doThings() {
    const a = foobar();
    const b = baz();

    try {
        await Promise.all([a, b]);
    } catch (error) {
        // ignore all errors!
    }
})();
</code></pre>
</div>

Here is another real-world scenario that would lead to an unhandled promise rejection error:

<div class="break-out">

<pre><code class="language-javascript">'use strict';

async function foobar() {
    throw new Error('foobar');
}

async function doThings() {
    try {
        return foobar()
    } catch {
        // ignoring errors again !
    }
}

doThings();
</code></pre>
</div>

If you run the above code snippet, you will get an unhandled promise rejection, and here is why: Although it’s not obvious, we are returning a promise (foobar) before we are handling it with the `try/catch`. What we should do is await the promise we are handling with the `try/catch` so the code would read:

<div class="break-out">

<pre><code class="language-javascript">'use strict';

async function foobar() {
    throw new Error('foobar');
}

async function doThings() {
    try {
        return await foobar()
    } catch {
        // ignoring errors again !
    }
}

doThings();
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Wrapping Up On The Negative Things

Now that you have seen wrong error handling patterns, and possible fixes, let’s now dive into Error class pattern and how it solves the problem of wrong error handling in NodeJS.

## Error Classes

In this pattern, we would start our application with an `ApplicationError` class this way we know all errors in our applications that we explicitly throw are going to inherit from it. So we would start off with the following error classes:

* `ApplicationError`  
This is the ancestor of all other error classes i.e all other error classes inherits from it.
* `DatabaseError`  
Any error relating to Database operations will inherit from this class.
* `UserFacingError`  
Any error produced as a result of a user interacting with the application would be inherited from this class.

Here is how our `error` class file would look like:

<div class="break-out">

<pre><code class="language-javascript">'use strict';

// Here is the base error classes to extend from

class ApplicationError extends Error {
    get name() {
        return this.constructor.name;
    }
}

class DatabaseError extends ApplicationError { }

class UserFacingError extends ApplicationError { }

module.exports = {
    ApplicationError,
    DatabaseError,
    UserFacingError
}
</code></pre>
</div>

This approach enables us to distinguish the errors thrown by our application. So now if we want to handle a bad request error (invalid user input) or a not found error (resource not found) we can inherit from the base class which is `UserFacingError` (as in the code below).

<div class="break-out">

<pre><code class="language-javascript">const { UserFacingError } = require('./baseErrors')

class BadRequestError extends UserFacingError {
    constructor(message, options = {}) {
        super(message);

        // You can attach relevant information to the error instance
        // (e.g.. the username)

        for (const [key, value] of Object.entries(options)) {
            this[key] = value;
        }
    }

    get statusCode() {
        return 400;
    }
}


class NotFoundError extends UserFacingError {
    constructor(message, options = {}) {
        super(message);

        // You can attach relevant information to the error instance
        // (e.g.. the username)

        for (const [key, value] of Object.entries(options)) {
            this[key] = value;
        }
    }
    get statusCode() {
        return 404
    }
}

module.exports = {
    BadRequestError,
    NotFoundError
}
</code></pre>
</div>

One of the benefits of the `error` class approach is that if we throw one of these errors, for example, a `NotFoundError`, every developer reading this codebase would be able to understand what is going on at this point in time(if they read the code). 

You would be able to pass in multiple properties specific to each error class as well during the instantiation of that error.

Another key benefit is that you can have properties that are always part of an error class, for example, if you receive a UserFacing error, you would know that a statusCode is always part of this error class now you can just directly use it in the code later on.

## Tips On Utilizing Error Classes

* Make your own module(possibly a private one) for each error class that way you can simply import that in your application and use it everywhere. 
* Throw only errors that you care about(errors that are instances of your error classes). This way you know your error classes are your only Source of Truth and it contains all information necessary to debug your application.
* Having an abstract error module is quite useful because now we know all necessary information concerning errors our applications can throw are in one place.
* Handle errors in layers. If you handle errors everywhere, you have an inconsistent approach to error handling which is hard to keep track of. By layers I mean like database, express/fastify/HTTP layers, and so on.

Let’s see how error classes looks in code. Here is an example in express:

<div class="break-out">

<pre><code class="language-javascript">const { DatabaseError } = require('./error')
const { NotFoundError } = require('./userFacingErrors')
const { UserFacingError } = require('./error')

// Express
app.get('/:id', async function (req, res, next) {
    let data

    try {
        data = await database.getData(req.params.userId)
    } catch (err) {
        return next(err);
    }

    if (!data.length) {
        return next(new NotFoundError('Dataset not found'));
    }

    res.status(200).json(data)
})

app.use(function (err, req, res, next) {
    if (err instanceof UserFacingError) {
        res.sendStatus(err.statusCode);

        // or

        res.status(err.statusCode).send(err.errorCode)
    } else {
        res.sendStatus(500)
    }

    // do your logic
    logger.error(err, 'Parameters: ', req.params, 'User data: ', req.user)
});
</code></pre>
</div>

From the above, we are leveraging that Express exposes a global error handler which allows you handle all your errors in one place. You can see the call to `next()` in the places we are handling errors. This call would pass the errors to the handler which is defined in the `app.use` section. Because express does not support async/await we are using `try/catch` blocks.

So from the above code, to handle our errors we just need to check if the error that was thrown is a `UserFacingError` instance and automatically we know that there would be a statusCode in the error object and we send that to the user (you might want to have a specific error code as well which you can pass to the client) and that is pretty much it. 

You would also notice that in this pattern (`error` class pattern) every other error that you did not explicitly throw is a `500` error because it is something unexpected that means you did not explicitly throw that error in your application. This way, we are able to distinguish the types of error going on in our applications.

## Conclusion

Proper error handling in your application can make you sleep better at night and save debug time. Here are some takeaway key points to take from this article:

* Use error classes specifically set up for your application;
* Implement abstract error handlers;
* Always use async/await;
* Make errors expressive;
* User promisify if necessary;
* Return proper error statuses and codes;
* Make use of promise hooks.

{{% newsletter-panel %}}

{{< signature "ra, yk, il" >}}

---
title: 'Dynamic Static Typing In TypeScript'
slug: dynamic-static-typing-typescript
author: stefan-baumgartner
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b918a308-b481-46e2-9877-1351fe2d699c/dynamic-static-typing-typescript.jpg
date: 2021-01-29T15:00:00.000Z
summary: >-
  In this article, we look at some of the more advanced features of TypeScript, like union types, conditional types, template literal types, and generics. We want to formalize the most dynamic JavaScript behavior in a way that we can catch most bugs before they happen. We apply several learnings from all chapters of <a href="https://www.smashingmagazine.com/printed-books/typescript-in-50-lessons/">TypeScript in 50 Lessons</a>, a book we’ve published here on Smashing Magazine late 2020. If you are interested in learning more, be sure to check it out!
description: >-
  In this article, we look at some of the more advanced features of TypeScript, like union types, conditional types, template literal types, and generics. We want to formalize the most dynamic JavaScript behavior in a way that we can catch most bugs before they happen.
categories:
  - Tools
  - Coding
  - JavaScript
  - TypeScript
---

JavaScript is an inherently dynamic programming language. We as developers can express a lot with little effort, and the language and its runtime figure out what we intended to do. This is what makes JavaScript so popular for beginners, and which makes experienced developers productive! There is a caveat, though: We need to be alert! Mistakes, typos, correct program behavior: A lot of that happens in our heads!

Take a look at the following example.

<pre><code class="language-typescript">app.get("/api/users/:userID", function(req, res) {
  if (req.method === "POST") {
    res.status(20).send({
      message: "Got you, user " + req.params.userId
    });
  }
})
</code></pre>

We have an [https://expressjs.com/](Express)-style server that allows us to define a route (or path), and executes a callback if the URL is requested.

The callback takes two arguments:

1. **The `request` object.**  
Here we get information on the [HTTP method used](https://developer.mozilla.org/de/docs/Web/HTTP/Methods) (e.g GET, POST, PUT, DELETE), and additional parameters that come in. In this example `userID` should be mapped to a parameter `userID` that, well, contains the user’s ID!
2. **The `response` or `reply` object.**  
Here we want to prepare a proper response from the server to the client. We want to send correct status codes (method `status`) and send JSON output over the wire.

What we see in this example is heavily simplified, but gives a good idea what we are up to. The example above is also riddled with errors! Have a look:

<pre><code class="language-typescript">app.get("/api/users/:userID", function(req, res) {
  if (req.method === "POST") { /* Error 1 */
    res.status(20).send({ /* Error 2 */
      message: "Welcome, user " + req.params.userId /* Error 3 */
    });
  }
})
</code></pre>

Oh wow! Three lines of implementation code, and three errors? What has happened?

1. The first error is nuanced. While we tell our app that we want to listen to *GET* requests (hence `app.get`), we only do something if the request method is *POST*. At this particular point in our application, `req.method` can’t be *POST*. So we would never send any response, which might lead to unexpected timeouts.
2. Great that we explicitly send a status code! `20` isn’t a valid status code, though. Clients might not understand what’s happening here.
3. This is the response we want to send back. We access the parsed arguments but have a mean typo. It’s `userID` not `userId`. All our users would be greeted with "Welcome, user undefined!". Something you definitely have seen in the wild!

And things like that happen! Especially in JavaScript. We gain expressiveness -- not once did we have to bother about types -- but have to pay close attention to what we’re doing.

This is also where JavaScript gets a lot of backlash from programmers who aren’t used to dynamic programming languages. They usually have compilers pointing them to possible problems and catching errors upfront. They might come off as snooty when they frown upon the amount of extra work you have to do in your head to make sure everything works right. They might even tell you that JavaScript has no types. Which is not true.

Anders Hejlsberg, the lead architect of TypeScript, said in his [MS Build 2017 keynote](https://channel9.msdn.com/Events/Build/2017/B8088) that “<em>it’s not that JavaScript has no type system. There is just no way of formalizing it</em>”.

And this is TypeScript’s main purpose. TypeScript wants to understand your JavaScript code better than you do. And where TypeScript can’t figure out what you mean, you can assist by providing extra type information.

{{% feature-panel %}}

## Basic Typing

And this is what we’re going to do right now. Let’s take the `get` method from our Express-style server and add enough type information so we can exclude as many categories of errors as possible.

We start with some basic type information. We have an `app` object that points to a `get` function. The `get` function takes `path`, which is a string, and a callback.

<pre><code class="language-typescript">const app = {
  get, /* post, put, delete, ... to come! */
};

function get(path: string, callback: CallbackFn) {
  // to be implemented --> not important right now
}
</code></pre>

While `string` is a basic, so-called *primitive* type, `CallbackFn` is a *compound* type that we have to explicitly define.

`CallbackFn` is a function type that takes two arguments:

- `req`, which is of type `ServerRequest`
- `reply` which is of type `ServerReply`

`CallbackFn` returns `void`.

<div class="break-out">

 <pre><code class="language-typescript">type CallbackFn = (req: ServerRequest, reply: ServerReply) => void;
</code></pre>
</div>

`ServerRequest` is a pretty complex object in most frameworks. We do a simplified version for demonstration purposes. We pass in a `method` string, for `"GET"`, `"POST"`, `"PUT"`, `"DELETE"`, etc. It also has a `params` record. Records are objects that associate a set of keys with a set of properties. For now, we want to allow for every `string` key to be mapped to a `string` property. We refactor this one later.

<pre><code class="language-typescript">type ServerRequest = {
  method: string;
  params: Record&lt;string, string&gt;;
};
</code></pre>

For `ServerReply`, we lay out some functions, knowing that a real `ServerReply` object has much more. A `send` function takes an optional argument with the data we want to send. And we have the possibility to set a status code with the `status` function.

<pre><code class="language-typescript">type ServerReply = {
  send: (obj?: any) => void;
  status: (statusCode: number) => ServerReply;
};
</code></pre>

That’s already something, and we can rule out a couple of errors:

<div class="break-out">

 <pre><code class="language-typescript">app.get("/api/users/:userID", function(req, res) {
  if(req.method === 2) {
//   ^^^^^^^^^^^^^^^^^ 💥 Error, type number is not assignable to string

    res.status("200").send()
//             ^^^^^ 💥 Error, type string is not assignable to number
  }
})
</code></pre>
</div>

But we still can send wrong status codes (any number is possible) and have no clue about the possible HTTP methods (any string is possible). Let’s refine our types.

## Smaller Sets

You can see primitive types as a set of all possible values of that certain category. For example, `string` includes all possible strings that can be expressed in JavaScript, `number` includes all possible numbers with double float precision. `boolean` includes all possible boolean values, which are `true` and `false`.

TypeScript allows you to refine those sets to smaller subsets. For example, we can create a type `Method` that includes all possible strings we can receive for HTTP methods:

<pre><code class="language-typescript">type Methods= "GET" &#124; "POST" &#124; "PUT" &#124; "DELETE";

type ServerRequest = {
  method: Methods;
  params: Record&lt;string, string&gt;;
};
</code></pre>

`Method` is a smaller set of the bigger `string` set. `Method` is a union type of literal types. A literal type is the smallest unit of a given set. A literal string. A literal number. There is no ambiguity. It’s just `"GET"`. You put them in a union with other literal types, creating a subset of whatever bigger types you have. You can also do a subset with literal types of both `string` and `number`, or different compound object types. There are lots of possibilities to combine and put literal types into unions.

This has an immediate effect on our server callback. Suddenly, we can differentiate between those four methods (or more if necessary), and can exhaust all possibilites in code. TypeScript will guide us:

<pre><code class="language-typescript">app.get("/api/users/:userID", function (req, res) {
  // at this point, TypeScript knows that req.method
  // can take one of four possible values
  switch (req.method) {
    case "GET":
      break;
    case "POST":
      break;
    case "DELETE":
      break;
    case "PUT":
      break;
    default:
      // here, req.method is never
      req.method;
  }
});
</code></pre>

With every `case` statement you make, TypeScript can give you information on the available options. [Try it out for yourself](https://www.typescriptlang.org/play?#code/C4TwDgpgBAshwAsD2ATAzlAvFARAcQFEAVHKAH1wAUB5AZRPKoFUGKcARAgGWIJwG4AUINCQotYAENgAVzQBhVNGwBGAAxrG6lVrUAmRno2G1OikYPm1AZhMAWEwFYTANhMB2EwA5DetxWtjANNGQMsoQNtgh2DnYP8oQShkiLVPYJ8KOyCobLNc-UZsqIKYgriChOz0gsyCgE4i9Sb8uxVwtpK2sraKtqqVGra6uyNGJJTRjr0uvR69Pr8ivRG9RqzrVrseu3Xcx00sx1b6vYPDqAP8g-CDkoOyg4qDhIOag7qJ5IOz5opj671OqOU5CQQAYyQADs0MAoJIwGAsFAAN4TADm8AANIIAL5g0TQWgQABOADdSQAlCBgAA2IGRaOSaAgUJQAC4oAAKJAAIwAVgB+TmSKEgACUWAAfFAyUgAJYoITMqSyNCcrmw6RyRQoCCciTahRKSWYGXE8lUmn0oT44QicDQeSSWm03mScEAawAYlDkVySRAAI4G0kUknUoMyCCwrFQQN0kChy0R60S6WyhVK4SE8Rhq1RmNw7BMqAAW3gyA5sErqDQyqgYEkJMkZfVUGpkJJKAAPLCSfKoei4-3B+ipbawQAzGRQ8HAeXQqCY4BcpuITmjodx8Eut0ez2c52u91e32S0sAekvUGASCgvOg8rLdIgFahwAgKCgAFofzKoSQOFnzAJASSkD943ldEEDhQCAHc8WEBEwAAOhXLkcEvBF5UvORSTQS92XwkkAEl2BwOMZznBclwDYM40DNALwma94ThRB5QwUDB2AOMiEdWhwQHMA4U9BCMEQaR42DVCK0QVBWJvXc-SkT1oGhDSpygKckBkElGyQNA0HlXlaWgMkXWjNAJjQeD5WAcEEG5QMgzk2sUBYlIoF3FlcEIEh2S+FJeUDSRPQbZJfOgHAaHoHAgu85JQogcLIqgPUp0kGRaWARKkrY5BwygJBivkqtguSVz3IU7NklxPFxX4IA). If you exhausted all options, TypeScript will tell you in your `default` branch that this can `never` happen. This is literally the type `never`, which means that you possibly have reached an error state that you need to handle.

That’s one category of errors less. We know now exactly which possible HTTP methods are available.

We can do the same for HTTP status codes, by defining a subset of valid numbers that `statusCode` can take:

<pre><code class="language-typescript">type StatusCode =
  100 | 101 | 102 | 200 | 201 | 202 | 203 | 204 | 205 |
  206 | 207 | 208 | 226 | 300 | 301 | 302 | 303 | 304 |
  305 | 306 | 307 | 308 | 400 | 401 | 402 | 403 | 404 |
  405 | 406 | 407 | 408 | 409 | 410 | 411 | 412 | 413 |
  414 | 415 | 416 | 417 | 418 | 420 | 422 | 423 | 424 |
  425 | 426 | 428 | 429 | 431 | 444 | 449 | 450 | 451 |
  499 | 500 | 501 | 502 | 503 | 504 | 505 | 506 | 507 |
  508 | 509 | 510 | 511 | 598 | 599;

type ServerReply = {
  send: (obj?: any) => void;
  status: (statusCode: StatusCode) => ServerReply;
};
</code></pre>

Type `StatusCode` is again a union type. And with that, we exclude another category of errors. Suddenly, code like that fails:

<div class="break-out">

 <pre><code class="language-typescript">app.get("/api/user/:userID", (req, res) => {
 if(req.method === "POS") {
//   ^^^^^^^^^^^^^^^^^^^ 'Methods' and '"POS"' have no overlap.
    res.status(20)
//             ^^ '20' is not assignable to parameter of type 'StatusCode'
 }
})
</code></pre>

And our software becomes a lot safer! But we can do more!
</div>

## Enter Generics

When we define a route with `app.get`, we implicitly know that the only HTTP method possible is `"GET"`. But with our type definitions, we still have to check for all possible parts of the union.

The type for `CallbackFn` is correct, as we could define callback functions for all possible HTTP methods, but if we explicitly call `app.get`, it would be nice to save some extra steps which are only necessary to comply with typings.

TypeScript generics can help! Generics are one of the major features in TypeScript that allow you to get the most dynamic behaviour out of static types. In [TypeScript in 50 Lessons](https://www.smashingmagazine.com/printed-books/typescript-in-50-lessons/), we spend the last three chapters digging into all the intricacies of generics and their unique functionality.

What you need to know right now is that we want to define `ServerRequest` in a way that we can specify a part of `Methods` instead of the entire set. For that, we use the generic syntax where we can define parameters as we would do with functions:

<pre><code class="language-typescript">type ServerRequest&lt;Met extends Methods&gt; = {
  method: Met;
  params: Record&lt;string, string&gt;;
};
</code></pre>

This is what happens:

1. `ServerRequest` becomes a generic type, as indicated by the angle brackets
2. We define a generic parameter called `Met`, which is a subset of type `Methods`
3. We use this generic parameter as a generic variable to define the method.

I also encourage you to check out [my article on naming generic parameters](https://fettblog.eu/tidy-typescript-name-your-generics/).

With that change, we can specify different `ServerRequest`s without duplicating things:

<pre><code class="language-typescript">type OnlyGET = ServerRequest<"GET">;
type OnlyPOST = ServerRequest<"POST">;
type POSTorPUT = ServerRquest<"POST" | "PUT">;
</code></pre>

Since we changed the interface of `ServerRequest`, we have to make changes to all our other types that use `ServerRequest`, like `CallbackFn` and the `get` function:

<pre><code class="language-typescript">type CallbackFn&lt;Met extends Methods&gt; = (
  req: ServerRequest&lt;Met&gt;,
  reply: ServerReply
) =&gt; void;

function get(path: string, callback: CallbackFn&lt;"GET"&gt;) {
  // to be implemented
}
</code></pre>

With the `get` function, we pass an actual argument to our generic type. We know that this won’t be just a subset of `Methods`, we know exactly which subset we are dealing with.

Now, when we use `app.get`, we only have on possible value for `req.method`:

<pre><code class="language-typescript">app.get("/api/users/:userID", function (req, res) {
  req.method; // can only be get
});
</code></pre>

This ensures that we don’t assume that HTTP methods like `"POST"` or similar are available when we create an `app.get` callback. We know exactly what we are dealing with at this point, so let’s reflect that in our types.

We already did a lot to make sure that `request.method` is reasonably typed and represents the actual state of affairs. One nice benefit we get with subsetting the `Methods` union type is that we can create a general purpose callback function *outside* of `app.get` that is type-safe:

<div class="break-out">

 <pre><code class="language-typescript">const handler: CallbackFn&lt;"PUT" &#124; "POST"&gt; = function(res, req) {
  res.method // can be "POST" or "PUT"
};

const handlerForAllMethods: CallbackFn&lt;Methods&gt; = function(res, req) {
  res.method // can be all methods
};


app.get("/api", handler);
//              ^^^^^^^ 💥 Nope, we don’t handle "GET"

app.get("/api", handlerForAllMethods); // 👍 This works
</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Typing Params

What we haven’t touched yet is typing the `params` object. So far, we get a record that allows accessing every `string` key. It’s our task now to make that a little bit more specific!

We do that by adding another generic variable. One for methods, one for the possible keys in our `Record`:

<pre><code class="language-typescript">type ServerRequest&lt;Met extends Methods, Par extends string = string&gt; = {
  method: Met;
  params: Record&lt;Par, string&gt;;
};
</code></pre>

The generic type variable `Par` can be a subset of type `string`, and the default value is every string. With that, we can tell `ServerRequest` which keys we expect:

<pre><code class="language-typescript">// request.method = "GET"
// request.params = {
//   userID: string
// }
type WithUserID = ServerRequest<"GET", "userID">
</code></pre>

Let’s add the new argument to our `get` function and the `CallbackFn` type, so we can set the requested parameters:

<pre><code class="language-typescript">function get&lt;Par extends string = string&gt;(
  path: string,
  callback: CallbackFn&lt;"GET", Par&gt;
) {
  // to be implemented
}

type CallbackFn&lt;Met extends Methods, Par extends string&gt; = (
  req: ServerRequest&lt;Met, Par&gt;,
  reply: ServerReply
) =&gt; void;
</code></pre>

If we don’t set `Par` explicitly, the type works as we are used to, since `Par` defaults to `string`. If we set it though, we suddenly have a proper definition for the `req.params` object!

<pre><code class="language-typescript">app.get&lt;"userID"&gt;("/api/users/:userID", function (req, res) {
  req.params.userID; // Works!!
  req.params.anythingElse; // 💥 doesn’t work!!
});
</code></pre>

That’s great! There is one little thing that can be improved, though. We still can pass *every* string to the `path` argument of `app.get`. Wouldn’t it be better if we could reflect `Par` in there as well?

We can! With the release of version 4.1, TypeScript is able to create *template literal types*. Syntactically, they work just like string template literals, but on a type level. Where we were able to split the set `string` into subsets with *string literal types* (like we did with Methods), template literal types allow us to include an entire spectrum of strings.

Let’s create a type called `IncludesRouteParams`, where we want to make sure that `Par` is properly included in the Express-style way of adding a colon in front of the parameter name:

<pre><code class="language-typescript">type IncludesRouteParams&lt;Par extends string&gt; =
  &#124; `${string}/:${Par}`
  &#124; `${string}/:${Par}/${string}`;
</code></pre>

The generic type `IncludesRouteParams` takes one argument, which is a subset of `string`. It creates a union type of two template literals:

1. The first template literal starts with *any* `string`, then includes a `/` character followed by a `:` character, followed by the parameter name. This makes sure that we catch all cases where the parameter is at the end of the route string.
2. The second template literal starts with *any* `string`, followed by the same pattern of `/`, `:` and the parameter name. Then we have another `/` character, followed by *any* string. This branch of the union type makes sure we catch all cases where the parameter is somewhere within a route.

This is how `IncludesRouteParams` with the parameter name `userID` behaves with different test cases:

<div class="break-out">

 <pre><code class="language-typescript">const a: IncludeRouteParams<"userID"> = "/api/user/:userID" // 👍
const a: IncludeRouteParams<"userID"> = "/api/user/:userID/orders" // 👍
const a: IncludeRouteParams<"userID"> = "/api/user/:userId" // 💥
const a: IncludeRouteParams<"userID"> = "/api/user" // 💥
const a: IncludeRouteParams<"userID"> = "/api/user/:userIDAndmore" // 💥
</code></pre>
</div>

Let’s include our new utility type in the `get` function declaration.

<pre><code class="language-typescript">function get&lt;Par extends string = string&gt;(
  path: IncludesRouteParams&lt;Par&gt;,
  callback: CallbackFn&lt;"GET", Par&gt;
) {
  // to be implemented
}

app.get&lt;"userID"&gt;(
  "/api/users/:userID",
  function (req, res) {
    req.params.userID; // YEAH!
  }
);
</code></pre>

Great! We get another safety mechanism to ensure that we don’t miss out on adding the parameters to the actual route! How powerful.

## Generic bindings

But guess what, I’m still not happy with it. There are a few issues with that approach that become apparent the moment your routes get a little more complex.

1. The first issue I have is that we need to explicitly state our parameters in the generic type parameter. We have to bind `Par` to `"userID"`, even though we would specify it anyway in the path argument of the function. This is not JavaScript-y!
2. This approach only handles one route parameter. The moment we add a union, e.g `"userID" | "orderId"` the failsafe check is satisfied with only *one* of those arguments being available. That’s how sets work. It can be one, or the other.

There must be a better way. And there is. Otherwise, this article would end on a very bitter note.

Let’s inverse the order! Let’s not try to define the route params in a generic type variable, but rather extract the variables from the `path` we pass as the first argument of `app.get`.

To get to the actual value, we have to see out how *generic binding* works in TypeScript. Let’s take this `identity` function for example:

<pre><code class="language-typescript">function identity&lt;T&gt;(inp: T) : T {
  return inp
}
</code></pre>

It might be the most boring generic function you ever see, but it illustrates one point perfectly. `identity` takes one argument, and returns the same input again. The type is the generic type `T`, and it also returns the same type.

Now we can bind `T` to `string`, for example:

<pre><code class="language-typescript">const z = identity&lt;string&gt;("yes"); // z is of type string
</code></pre>

This explicitly generic binding makes sure that we only pass `strings` to `identity`, and since we explicitly bind, the return type is also `string`. If we forget to bind, something interesting happens:

<pre><code class="language-typescript">const y = identity("yes") // y is of type "yes"
</code></pre>

In that case, TypeScript infers the type from the argument you pass in, and binds `T` to the *string literal type* `"yes"`. This is a great way of converting a function argument to a literal type, which we then use in our other generic types.

Let’s do that by adapting `app.get`.

<pre><code class="language-typescript">function get&lt;Path extends string = string&gt;(
  path: Path,
  callback: CallbackFn&lt;"GET", ParseRouteParams&lt;Path&gt;&gt;
) {
  // to be implemented
}
</code></pre>

We remove the `Par` generic type and add `Path`. `Path` can be a subset of any `string`. We set `path` to this generic type `Path`, which means the moment we pass a parameter to `get`, we catch its string literal type. We pass `Path` to a new generic type `ParseRouteParams` which we haven’t created yet.

Let’s work on `ParseRouteParams`. Here, we switch the order of events around again. Instead of passing the requested route params to the generic to make sure the path is alright, we pass the route path and extract the possible route params. For that, we need to create a conditional type.

{{% ad-panel-leaderboard %}}

## Conditional Types And Recursive Template Literal Types

Conditional types are syntactically similar to the ternary operator in JavaScript. You check for a condition, and if the condition is met, you return branch A, otherwise, you return branch B. For example:

<pre><code class="language-typescript">type ParseRouteParams&lt;Rte&gt; =
  Rte extends `${string}/:${infer P}`
  ? P
  : never;
</code></pre>

Here, we check if `Rte` is a subset of every path that ends with the parameter at the end Express-style (with a preceding `"/:"`). If so, we infer this string. Which means we capture its contents into a new variable. If the condition is met, we return the newly extracted string, otherwise, we return never, as in: "There are no route parameters",

If we try it out, we get something like that:

<div class="break-out">

 <pre><code class="language-typescript">type Params = ParseRouteParams&lt;"/api/user/:userID"&gt; // Params is "userID"

type NoParams = ParseRouteParams&lt;"/api/user"&gt; // NoParams is never --&gt; no params!
</code></pre>
</div>

Great, that’s already much better than we did earlier. Now, we want to catch all other possible parameters. For that, we have to add another condition:

<div class="break-out">

 <pre><code class="language-typescript">type ParseRouteParams&lt;Rte&gt; = Rte extends `${string}/:${infer P}/${infer Rest}`
  ? P | ParseRouteParams&lt;`/${Rest}`&gt;
  : Rte extends `${string}/:${infer P}`
  ? P
  : never;
</code></pre>
</div>

Our conditional type works now as follows:

1. In the first condition, we check if there is a route parameter somewhere in between the route. If so, we extract both the route parameter and everything else that comes after that. We return the newly found route parameter `P` in a union where we call the same generic type recursively with the `Rest`. For example, if we pass the route `"/api/users/:userID/orders/:orderID"` to `ParseRouteParams`, we infer `"userID"` into `P`, and `"orders/:orderID"` into `Rest`. We call the same type with `Rest`
2. This is where the second condition comes in. Here we check if there is a type at the end. This is the case for `"orders/:orderID"`. We extract `"orderID"` and return this literal type.
3. If there is no more route parameter left, we return never.

[Dan Vanderkam](https://effectivetypescript.com/2020/11/05/template-literal-types/) shows a similar, and more elaborate type for `ParseRouteParams`, but the one you see above should work as well. If we try out our newly adapted `ParseRouteParams`, we get something like this:

<pre><code class="language-typescript">// Params is "userID"
type Params = ParseRouteParams<"/api/user/:userID"&gt;

// MoreParams is "userID" | "orderID"
type MoreParams = ParseRouteParams<"/api/user/:userID/orders/:orderId"&gt;
</code></pre>

Let’s apply this new type and see what our final usage of `app.get` looks like.

<pre><code class="language-typescript">app.get("/api/users/:userID/orders/:orderID", function (req, res) {
  req.params.userID; // YES!!
  req.params.orderID; // Also YES!!!
});
</code></pre>

Wow. That just looks like the JavaScript code we had at the beginning!

## Static Types For Dynamic Behavior

The types we just created for one function `app.get` make sure that we exclude a ton of possible errors:

1. We can only pass proper numeric status codes to `res.status()`
2. `req.method` is one of four possible strings, and when we use `app.get`, we know it only be `"GET"`
3. We can parse route params and make sure that we don’t have any typos inside our callback

If we look at the example from the beginning of this article, we get the following error messages:

<pre><code class="language-typescript">app.get("/api/users/:userID", function(req, res) {
  if (req.method === "POST") {
//    ^^^^^^^^^^^^^^^^^^^^^
//    This condition will always return 'false'
//     since the types '"GET"' and '"POST"' have no overlap.
    res.status(20).send({
//             ^^
//             Argument of type '20' is not assignable to
//             parameter of type 'StatusCode'
      message: "Welcome, user " + req.params.userId
//                                           ^^^^^^
//         Property 'userId' does not exist on type
//    '{ userID: string; }'. Did you mean 'userID'?
    });
  }
})
</code></pre>

And all that before we actually run our code! Express-style servers are a perfect example of the dynamic nature of JavaScript. Depending on the method you call, the string you pass for the first argument, a lot of behavior changes inside the callback. Take another example and all your types look entirely different.

But with a few well-defined types, we can catch this dynamic behavior while editing our code. At compile time with static types, not at runtime when things go boom!

And this is the power of TypeScript. A static type system that tries to formalize all the dynamic JavaScript behavior we all know so well. If you want to try the example we just created, head over to the [TypeScript playground](https://www.typescriptlang.org/play?#code/MYewdgzgLgBAhgBwTAvDA3gKBjA5gUygBpMBfAbk0ygE8F8YBlfAJwDdWAlfBAGxtQZsMCPjAATAFwwAFCABGAKwD80uGBoBKVAD4YbEAEtxlHNDhQArhGkzzViAGEQ4-NMZQL156+0o9zOxcPPyUFFQA9BEAxCz4uIbgTJ4OPvjUdAweXk4uDCjCAD4wAIwADGVFpWUlVeUATFX1FU01rY04xc0AzK0ALK0ArK0AbK0A7K0AHE31Y50w3S0LS7UrZR0wxUu96wPrw+vzW4tlk+szC33LJ9drtxtV17sP+w+HD8fF1+cPlw8ATie5WB92+JU24Je4Le4I+4K+MD6JV+4P+32aT3qkKR9WhuNhuPhuMRfXq6NxQKu3TBSL6hPpVNug0qV0GtL6AKZxRZrJOLNpLJxLPxLMJLOJLMRLNRMBZFJZ3LlIIW7MFAIVXMoUWiYnEcQS4CotHoMAAsoQABYuCCCABEAHEAKIAFTtJztAAUAPKMN0ez0AVX9xTtABEnQAZV1Ou2UTAAM0sYGAUESYDwhAAPJ6LJaYPgAB5QPW26AsQxgXCCcuV3A6GTCBB56S5qCWkg4YBwXi8eRwYAAa2kjh7fYHg4AYmAs47XXaiDBcyxRJwQJYS8u4ABbCA5vM6HSYbRYHBRGBQEAweQMQzbvj4bdiEviMjGzJLuAr-Brjf4Le7lmnAlnoaDAQwRYlhItoAAYACToLWVakBEkgIZWCasEuKHoWAmEsDA3DQKQMHCMoS4nMuq7rpuX47nuMERAhRFQCRR44NI4EFsWpYwPBiFQBWyGobh+HYaRODkZ6wjSGA+AcCw8Ymgwo69v2Q7TlmFqwJBvHada4gQIuy7cVBhkiIJdagbIwhxAAju4rAKdwdmWPg0BaYQxlfjonYwHEfA0I5QQsNwgXHro+hGCY76moEzn4K57lQJ5Ok8dB5pWja3kEbpGVIdWaAFdZp4wE+7YuNI2mmDAzYsPR0joDAADaADSMCVp+LAALrSAVMDhOEmCIAgAB0BBQDIdoRIghgRNYrAQKhC0sAAkmGqEgCwrhreIC4wEmKZpkkMj2YucQQCetmJaNdX0aNK3rTVF2jfY1gyM0ZSaK9eoyJoYT-ZgQA) and fiddle around with it.

<hr />

<p><em><a href="https://www.smashingmagazine.com/printed-books/typescript-in-50-lessons/"><img loading="lazy" decoding="async"  style="float:right;margin-top:1em;margin-left:1.5em;margin-bottom:1em;border-radius:11px;max-width:50%" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e9832cc8-7166-408e-9dc4-0070761aae5f/smashing-typescript-book-400x400.png" width="200" height="200" loading="lazy" decoding="async" alt="TypeScript in 50 Lessons by Stefan Baumgartner" /></a>In this article, we touched upon many concepts. If you’d like to know more, check out <a href="https://www.smashingmagazine.com/printed-books/typescript-in-50-lessons/">TypeScript in 50 Lessons</a>, where you get a gentle introduction to the type system in small, easily digestible lessons. Ebook versions are available immediately, and the print book will make a great reference for your coding library.</em></p>

{{< signature "vf, il" >}}

---
title: 'A Comparison Of <code>async/await</code> Versus <code>then/catch</code>'
slug: comparison-async-await-versus-then-catch
author: bret-cameron
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba0789dc-581e-47ec-b9c7-684a5c71193a/comparison-async-await-versus-then-catch.png
date: 2020-11-23T13:30:00.000Z
summary: >-
  In JavaScript, there are two main ways to handle asynchronous code: <code>then/catch</code> (ES6) and <code>async/await</code> (ES7). These syntaxes give us the same underlying functionality, but they affect readability and scope in different ways. In this article, we’ll see how one syntax lends itself to maintainable code, while the other puts us on the road to callback hell!
description: >-
  In JavaScript, there are two main ways to handle asynchronous code: <code>then/catch</code> (ES6) and <code>async/await</code> (ES7). These syntaxes give us the same underlying functionality, but they affect readability and scope in different ways. In this article, we’ll see how one syntax lends itself to maintainable code, while the other puts us on the road to callback hell!
categories:
  - Tools
  - Coding
  - JavaScript
---

JavaScript runs code line by line, moving to the next line of code only after the previous one has been executed. But executing code like this can only take us so far. Sometimes, we need to perform tasks that take a long or unpredictable amount of time to complete: fetching data or triggering side-effects via an API, for example. 

Rather than letting these tasks block JavaScript’s main thread, the language allows us to run certain tasks in parallel. ES6 saw the introduction of the Promise object as well as new methods to handle the execution of these Promises: `then`, `catch`, and `finally`. But a year later, in ES7, the language added another approach and two new keywords: `async` and `await`.

This article isn’t an explainer of asynchronous JavaScript; there are lots of good resources available for that. Instead, it addresses a less-covered topic: which syntax &mdash; `then/catch` or `async/await` &mdash; is better? In my view, unless a library or legacy codebase forces you to use `then/catch`, the better choice for readability and maintainability is `async/await`. To demonstrate that, we’ll use both syntaxes to solve the same problem. By slightly changing the requirements, it should become clear which approach is easier to tweak and maintain. 

We’ll start by recapping the main features of each syntax, before moving to our example scenario.

## `then`, `catch` And `finally`

`then` and `catch` and `finally` are methods of the Promise object, and they are chained one after the other. Each takes a callback function as its argument and returns a Promise.

For example, let’s instantiate a simple Promise:

<pre><code class="language-javascript">const greeting = new Promise((resolve, reject) =&gt; {
  resolve("Hello!");
});</code></pre>

Using `then`, `catch` and `finally`, we could perform a series of actions based on whether the Promise is resolved (`then`) or rejected (`catch`) &mdash; while `finally` allows us to execute code once the Promise is settled, regardless of whether it was resolved or rejected:

<div class="break-out">

<pre><code class="language-javascript">greeting
  .then((value) =&gt; {
    console.log("The Promise is resolved!", value);
  })
  .catch((error) =&gt; {
    console.error("The Promise is rejected!", error);
  })
  .finally(() =&gt; {
    console.log(
      "The Promise is settled, meaning it has been resolved or rejected."
    );
  });</code></pre>
</div>

For the purposes of this article, we only need to use `then`. Chaining multiple `then` methods allows us to perform successive operations on a resolved Promise. For example, a typical pattern for fetching data with `then` might look something like this:

<pre><code class="language-javascript">fetch(url)
  .then((response) => response.json())
  .then((data) =&gt; {
    return {
      data: data,
      status: response.status,
    };
  })
  .then((res) =&gt; {
    console.log(res.data, res.status);
  });</code></pre>

## `async` And `await`

By contrast, `async` and `await` are keywords which make synchronous-looking code asynchronous. We use `async` when defining a function to signify that it returns a Promise. Notice how the placement of the `async` keyword depends on whether we’re using regular functions or arrow functions:

<pre><code class="language-javascript">async function doSomethingAsynchronous() {
  // logic
}

const doSomethingAsynchronous = async () =&gt; {
  // logic
};</code></pre>

`await`, meanwhile, is used before a Promise. It pauses the execution of an asynchronous function until the Promise is resolved. For example, to await our `greeting` above, we could write:

<pre><code class="language-javascript">async function doSomethingAsynchronous() {
  const value = await greeting;
}</code></pre>

We can then use our `value` variable as if it were part of normal synchronous code.

As for error handling, we can wrap any asynchronous code inside a `try...catch...finally` statement, like so:

<div class="break-out">

<pre><code class="language-javascript">async function doSomethingAsynchronous() {
  try {
    const value = await greeting;
    console.log("The Promise is resolved!", value);
  } catch((error) {
    console.error("The Promise is rejected!", error);
  } finally {
    console.log(
      "The Promise is settled, meaning it has been resolved or rejected."
    );
  }
}</code></pre>
</div>

Finally, when returning a Promise inside an `async` function, you don’t need to use `await`. So the following is acceptable syntax.

<pre><code class="language-javascript">async function getGreeting() {
  return greeting;
}</code></pre>

However, there’s one exception to this rule: you do need to write `return await` if you’re looking to handle the Promise being rejected in a `try...catch` block.

<pre><code class="language-javascript">async function getGreeting() {
  try {
    return await greeting;
  } catch (e) {
    console.error(e);
  }
}</code></pre>

Using abstract examples might help us understand each syntax, but it’s difficult to see why one might be preferable to the other until we jump into an example.

{{% feature-panel %}}

## The Problem

Let’s imagine we need to perform an operation on a large dataset for a bookstore. Our task is to find all authors who have written more than 10 books in our dataset and return their bio. We have access to a library with three asynchronous methods:

<pre><code class="language-javascript">// getAuthors - returns all the authors in the database
// getBooks - returns all the books in the database
// getBio - returns the bio of a specific author</code></pre>

Our objects look like this:

<div class="break-out">

<pre><code class="language-javascript">// Author: { id: "3b4ab205", name: "Frank Herbert Jr.", bioId: "1138089a" }
// Book: { id: "e31f7b5e", title: "Dune", authorId: "3b4ab205" }
// Bio: { id: "1138089a", description: "Franklin Herbert Jr. was an American science-fiction author..." }</code></pre>
</div>

Lastly, we’ll need a helper function, `filterProlificAuthors`, which takes all the posts and all the books as arguments, and returns the IDs of those authors with more than 10 books:

<div class="break-out">

<pre><code class="language-javascript">function filterProlificAuthors() {
  return authors.filter(
    ({ id }) =&gt; books.filter(({ authorId }) =&gt; authorId === id).length &gt; 10
  );
}</code></pre>
</div>

## The Solution

### Part 1

To solve this problem, we need to fetch all the authors and all the books, filter our results based on our given criteria, and then get the bio of any authors who fit that criteria. In pseudo-code, our solution might look something like this:

<pre><code class="language-javascript">FETCH all authors
FETCH all books
FILTER authors with more than 10 books
FOR each filtered author
  FETCH the author’s bio</code></pre>

Every time we see `FETCH` above, we need to perform an asynchronous task. So how could we turn this into JavaScript? First, let’s see how we might code these steps using `then`:

<pre><code class="language-javascript">getAuthors().then((authors) =&gt;
  getBooks()
    .then((books) =&gt; {
      const prolificAuthorIds = filterProlificAuthors(authors, books);
      return Promise.all(prolificAuthorIds.map((id) =&gt; getBio(id)));
    })
    .then((bios) =&gt; {
      // Do something with the bios
    })
);</code></pre>

This code does the job, but there’s some nesting going on that can make it difficult to understand at a glance. The second `then` is nested inside the first `then`, while the third `then` is parallel to the second.

Our code might become a little more readable if we used `then` to return even synchronous code? We could give `filterProlificAuthors` its own `then` method, like below:

<pre><code class="language-javascript">getAuthors().then((authors) =&gt;
  getBooks()
    .then((books) =&gt; filterProlificAuthors(authors, books))
    .then((ids) =&gt; Promise.all(ids.map((id) =&gt; getBio(id))))
    .then((bios) =&gt; {
      // Do something with the bios
    })
);</code></pre>

This version has the benefit that each `then` method fits on one line, but it doesn’t save us from multiple levels of nesting. 

What about using `async` and `await`? Our first pass at a solution might look something like this:

<div class="break-out">

<pre><code class="language-javascript">async function getBios() {
  const authors = await getAuthors();
  const books = await getBooks();
  const prolificAuthorIds = filterProlificAuthors(authors, books);
  const bios = await Promise.all(prolificAuthorIds.map((id) =&gt; getBio(id)));
  // Do something with the bios
}</code></pre>
</div>

To me, this solution already appears simpler. It involves no nesting and can be easily expressed in just four lines &mdash; all at the same level of indentation. However, the benefits of `async/await` will become more apparent as our requirements change.

{{% ad-panel-leaderboard %}}

### Part 2

Let’s introduce a new requirement. This time, once we have our `bios` array, we want to create an object containing `bios`, the total number of authors, and the total number of books.

This time, we’ll start with `async/await`:

<div class="break-out">

<pre><code class="language-javascript">async function getBios() {
  const authors = await getAuthors();
  const books = await getBooks();
  const prolificAuthorIds = filterProlificAuthors(authors, books);
  const bios = await Promise.all(prolificAuthorIds.map((id) =&gt; getBio(id)));
  const result = {
    bios,
    totalAuthors: authors.length,
    totalBooks: books.length,
  };
}</code></pre>
</div>

Easy! We don’t have to do anything to our existing code, since all the variables we need are already in scope. We can just define our `result` object at the end.

With `then`, it’s not so simple. In our `then` solution from Part 1, the `books` and `bios` variables are never in the same scope. While we *could* introduce a global `books` variable, that would pollute the global namespace with something we only need in our asynchronous code. It would be better to reformat our code. So how could we do it?

One option would be to introduce a third level of nesting:

<pre><code class="language-javascript">getAuthors().then((authors) =&gt;
  getBooks().then((books) =&gt; {
    const prolificAuthorIds = filterProlificAuthors(authors, books);
    return Promise.all(prolificAuthorIds.map((id) =&gt; getBio(id))).then(
      (bios) =&gt; {
        const result = {
          bios,
          totalAuthors: authors.length,
          totalBooks: books.length,
        };
      }
    );
  })
);</code></pre>

Alternatively, we could use array destructuring syntax to help pass `books` down through the chain at every step:

<pre><code class="language-javascript">getAuthors().then((authors) =&gt;
  getBooks()
    .then((books) =&gt; [books, filterProlificAuthors(authors, books)])
    .then(([books, ids]) =&gt;
      Promise.all([books, ...ids.map((id) =&gt; getBio(id))])
    )
    .then(([books, bios]) =&gt; {
      const result = {
        bios,
        totalAuthors: authors.length,
        totalBooks: books.length,
      };
    })
);</code></pre>

To me, neither of these solutions is particularly readable. It’s difficult to work out &mdash; at a glance &mdash; which variables are accessible where.

{{% ad-panel-leaderboard %}}

### Part 3

As a final optimisation, we can improve the performance of our solution and clean it up a little by using `Promise.all` to fetch the authors and books at the same time. This helps clean up our `then` solution a little:

<div class="break-out">

<pre><code class="language-javascript">Promise.all([getAuthors(), getBooks()]).then(([authors, books]) =&gt; {
  const prolificAuthorIds = filterProlificAuthors(authors, books);
  return Promise.all(prolificAuthorIds.map((id) =&gt; getBio(id))).then((bios) =&gt; {
    const result = {
      bios,
      totalAuthors: authors.length,
      totalBooks: books.length,
    };
  });
});</code></pre>
</div>

This may be the best `then` solution of the bunch. It removes the need for multiple levels of nesting and the code runs faster. 

Nevertheless, `async/await` remains simpler:

<div class="break-out">

<pre><code class="language-javascript">async function getBios() {
  const [authors, books] = await Promise.all([getAuthors(), getBooks()]);
  const prolificAuthorIds = filterProlificAuthors(authors, books);
  const bios = await Promise.all(prolificAuthorIds.map((id) =&gt; getBio(id)));
  const result = {
    bios,
    totalAuthors: authors.length,
    totalBooks: books.length,
  };
}</code></pre>
</div>

There’s no nesting, only one level of indentation, and much less chance of bracket-based confusion!

## Conclusion

Often, using chained `then` methods can require fiddly alterations, especially when we want to ensure certain variables are in scope. Even for a simple scenario like the one we discussed, there was no obvious best solution: each of the five solutions using `then` had different tradeoffs for readability. By contrast, `async/await` lent itself to a more readable solution that needed to change very little when the requirements of our problem were tweaked.

In real applications, the requirements of our asynchronous code will often be more complex than the scenario presented here. While `async/await` provides us with an easy-to-understand foundation for writing trickier logic, adding many `then` methods can easily force us further down the path towards callback hell &mdash; with many brackets and levels of indentation making it unclear where one block ends and the next begins. 

For that reason &mdash; if you have the choice &mdash; choose `async/await` over `then/catch`.

{{< signature "sh, ra, yk, il" >}}

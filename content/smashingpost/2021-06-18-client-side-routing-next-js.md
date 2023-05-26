---
title: 'Client-Side Routing In Next.js'
slug: client-side-routing-next-js
author: adebiyi-adedotun
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a51f6c83-5e1a-4535-b28a-2018310ffc3b/client-side-routing-next-js.jpg
date: 2021-06-18T13:00:00.000Z
summary: >-
  Next.js has a file-based routing system in which each page automatically becomes a route based on its file name. Each page is a default exported React component from the pages directory that can be used to define the most common route patterns. This article will guide you through almost everything you need to know about Routing in Next.js and point you in the direction of related topics and concepts.
description: >-
  Next.js has a file-based routing system in which each page automatically becomes a route based on its file name. This article will guide you through almost everything you need to know about Routing in Next.js and point you in the direction of related topics and concepts.
categories:
  - React
  - Next.js
  - JavaScript
  - Guides
---

Hyperlinks have been one of the jewels of the Web [since its inception](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks) . According to MDN, hyperlinks are what makes the Web, *a web.* While used for purposes such as linking between documents, its primary use is to reference different web pages identifiable by a unique web address or a [URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL).

Routing is an important aspect of each web application as much as hyperlinks are to the Web. It is a mechanism through which requests are routed to the code that handles them. In relation to routing, Next.js pages are referenced and identifiable by a unique URL path. If the Web consists of **navigational** **web pages** interconnected by **hyperlinks**, then each Next.js app consists of route-able pages (route handlers or routes) interconnected by a router.

Next.js has built-in support for routing that can be unwieldy to unpack, especially when considering rendering and data fetching. As a prerequisite to understanding client-side routing in Next.js, it is necessary to have an overview of concepts like routing, rendering, and data fetching in Next.js.

This article will be beneficial to React developers who are familiar with Next.js and want to learn how it handles routing. You need to have a working knowledge of React and Next.js to get the most out of the article, which is solely about client-side routing and related concepts in Next.js. 

## Routing And Rendering

Routing and Rendering are complementary to each other and will play a huge part through the course of this article. I like how [Gaurav explains](https://www.pluralsight.com/guides/pros-and-cons-of-client-side-routing-with-react) them: 

<blockquote><strong>Routing</strong> is the process through which the user is navigated to different pages on a website.<br /><br /><strong>Rendering</strong> is the process of putting those pages on the UI. Every time you request a route to a particular page, you are also rendering that page, but not every render is an outcome of a route.</blockquote>

[Take five minutes](https://signalvnoise.com/posts/3124-give-it-five-minutes) to think about that.

What you need to understand about rendering in Next.js is that each page is [pre-rendered](https://nextjs.org/docs/basic-features/pages#pre-rendering) in advance alongside the minimal JavaScript code necessary for it to become fully interactive through a process known as hydration. How Next.js does this is highly dependent on the [form of pre-rendering](https://nextjs.org/docs/basic-features/pages#two-forms-of-pre-rendering): **Static Generation** or **Server-side rendering**, which are both highly coupled to the data fetching technique used, and separated by **when** the HTML for a page is generated.

Depending on your data fetching requirements, you might find yourself using built-in data fetching functions like `getStaticProps`, `getStaticPaths`, or, `getServerSideProps`, client-side data fetching tools like SWR, react-query, or traditional data fetching approaches like [fetch-on-render](https://reactjs.org/docs/concurrent-mode-suspense.html#approach-1-fetch-on-render-not-using-suspense), [fetch-then-render](https://reactjs.org/docs/concurrent-mode-suspense.html#approach-2-fetch-then-render-not-using-suspense), [render-as-you-fetch](https://reactjs.org/docs/concurrent-mode-suspense.html#approach-3-render-as-you-fetch-using-suspense) (with [Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html)).

Pre-rendering (before rendering &mdash; *to the UI*) is complementary to Routing, and highly coupled with data fetching &mdash; a whole topic of its own in Next.js. So while these concepts are either complementary or closely related, this article will be solely focused on mere navigation between pages (routing), with references to related concepts where necessary.

With that out of the way, let’s begin with the fundamental gist: Next.js has a file-system-based router built on the [concept of pages](https://nextjs.org/docs/basic-features/pages).

{{% feature-panel %}}

## Pages

Pages in Next.js are React Components that are automatically available as routes. They are exported as default exports from the pages directory with supported file extensions like `.js`, `.jsx`, `.ts`, or `.tsx`.

A typical Next.js app will have a folder structure with top-level directories like **pages**, **public**, and **styles.**

<pre><code class="language-javascript">next-app
├── node_modules
├── pages
│   ├── index.js // path: base-url (/)
│   ├── books.jsx // path: /books
│   └── book.ts // path: /book
├── public
├── styles
├── .gitignore
├── package.json
└── README.md</code></pre>

Each page is a React component:

<pre><code class="language-javascript">// pages/books.js &mdash; `base-url/book`
export default function Book() {
  return <h1>Books</h1>
}</code></pre>

**Note**: *Keep in mind that pages can also be referred to as “route handlers”.*

## Custom Pages

These are special pages that reside in the **pages** directory but do not participate in routing. They are prefixed with the underscore symbol, as in, `_app.js`, and `_document.js`.

- `_app.js`  
This is a custom component that resides in the pages folder. Next.js uses this component to initialize pages.
- `_document.js`  
Like `_app.js`, `_document.js` is a custom component that Next.js uses to augment your applications `<html>` and `<body>` tags. This is necessary because Next.js pages skip the definition of the surrounding document’s markup. 

<div class="break-out">

<pre><code class="language-javascript">next-app
├── node_modules
├── pages
│   ├── _app.js // ⚠️ Custom page (unavailable as a route)
│   ├── _document.jsx // ⚠️ Custom page (unavailable as a route)
│   └── index.ts // path: base-url (/)
├── public
├── styles
├── .gitignore
├── package.json
└── README.md</code></pre>
</div>

## Linking Between Pages

Next.js exposes a `Link` component from the `next/link` API that can be used to perform client-side route transitions between pages.

<pre><code class="language-javascript">// Import the &lt;Link/&gt; component
import Link from "next/link";

// This could be a page component
export default function TopNav() {
  return (
    &lt;nav&gt;
      &lt;Link href="/"&gt;Home&lt;/Link&gt;
      &lt;Link href="/"&gt;Publications&lt;/Link&gt;
      &lt;Link href="/"&gt;About&lt;/Link&gt;
    &lt;/nav&gt;
  )
}

// This could be a non-page component
export default function Publications() {
  return (
    &lt;section&gt;
      &lt;TopNav/&gt;
      {/* ... */}
    &lt;/section&gt;
  )
}</code></pre>

The `Link` component can be used inside any component, page or not. When used in its most basic form as in the example above, the `Link` component translates to a hyperlink with an `href` attribute. (More on `Link` in the next/link section below.)

{{% ad-panel-leaderboard %}}

## Routing

Next.js file-based routing system can be used to define the most common route patterns. To accommodate for these patterns, each route is separated based on its *definition.*

### Index Routes

By default, in your Next.js app, the initial/default route is `pages/index.js` which automatically serves as the starting point of your application as `/`. With a base URL of `localhost:3000`, this index route can be accessed at the base URL level of the application in the browser.

Index routes automatically act as the default route for each directory and can eliminate naming redundancies. The directory structure below exposes two route paths: `/` and `/home`.

<pre><code class="language-javascript">next-app
└── pages
    ├── index.js // path: base-url (/)
    └── home.js // path: /home</code></pre>

The elimination is more apparent with **nested routes**.

### Nested Routes

A route like `pages/book` is one level deep. To go deeper is to create nested routes, which requires a nested folder structure. With a base-url of `https://www.smashingmagazine.com`, you can access the route `https://www.smashingmagazine.com/printed-books/printed-books` by creating a folder structure similar to the one below:

<div class="break-out">

<pre><code class="language-javascript">next-app
└── pages
    ├── index.js // top index route
    └── printed-books // nested route
        └── printed-books.js // path: /printed-books/printed-books</code></pre>
</div>

Or eliminate path redundancy with index routes and access the route for printed books at `https://www.smashingmagazine.com/printed-books`.

<pre><code class="language-javascript">next-app
└── pages
    ├── index.js // top index route
    └── printed-books // nested route
        └── index.js // path: /printed-books</code></pre>

**Dynamic routes** also play an important role in eliminating redundancies.

### Dynamic Routes

From the previous example we use the index route to access all printed books. To access individual books requires either creating different routes for each book like:

<div class="break-out">

<pre><code class="language-javascript">// ⚠️ Don't do this.
next-app
└── pages
    ├── index.js // top index route
    └── printed-books // nested route
        ├── index.js // path: /printed-books
        ├── typesript-in-50-lessons.js // path: /printed-books/typesript-in-50-lessons
        ├── checklist-cards.js // path: /printed-books/checklist-cards
        ├── ethical-design-handbook.js // path: /printed-books/ethical-design-handbook
        ├── inclusive-components.js // path: /printed-books/inclusive-components
        └── click.js // path: /printed-books/click</code></pre>
</div>

which is highly redundant, unscalable, and can be remedied with dynamic routes like:

<pre><code class="language-javascript">// ✅ Do this instead.
next-app
└── pages
    ├── index.js // top index route
    └── printed-books
        ├── index.js // path: /printed-books
        └── [book-id].js // path: /printed-books/:book-id</code></pre>

The bracket syntax &mdash; `[book-id]` &mdash; is the **dynamic segment**, and is not limited to files alone. It can also be used with folders like the example below, making the author available at the route `/printed-books/:book-id/author`.

<div class="break-out">

<pre><code class="language-javascript">next-app
└── pages
    ├── index.js // top index route
    └── printed-books
        ├── index.js // path: /printed-books
        └── [book-id]
            └── author.js // path: /printed-books/:book-id/author</code></pre>
</div>

The dynamic segment(s) of a route is exposed as a query parameter that can be accessed in any of the connecting component involved in the route with `query` object of the `useRouter()` hook &mdash; (More on this in the next/router API section).

<pre><code class="language-javascript">// printed-books/:book-id
import { useRouter } from 'next/router';

export default function Book() {
  const { query } = useRouter();

  return (
    &lt;div&gt;
      &lt;h1&gt;
        book-id &lt;em&gt;{query['book-id']}&lt;/em&gt;
      &lt;/h1&gt;
    &lt;/div&gt;
  );
}</code></pre>

<div class="break-out">

<pre><code class="language-javascript">// /printed-books/:book-id/author
import { useRouter } from 'next/router';

export default function Author() {
  const { query } = useRouter();

  return (
    &lt;div&gt;
      &lt;h1&gt;
        Fetch author with book-id &lt;em&gt;{query['book-id']}&lt;/em&gt;
      &lt;/h1&gt;
    &lt;/div&gt;
  );
}
</code></pre>
</div>

### Extending Dynamic Route Segments With Catch All Routes

You’ve seen the dynamic route segment bracket syntax as in the previous example with `[book-id].js`. The beauty of this syntax is that it takes things even further with *Catch-All Routes*. You can infer what this does from the name: it catches all routes.

When we looked at the dynamic example, we learned how it helps eliminate file creation redundancy for a single route to access multiple books with their ID. But there’s something else we could have done.

Specifically, we had the path `/printed-books/:book-id`, with a directory structure:

<pre><code class="language-javascript">next-app
└── pages
    ├── index.js
    └── printed-books
        ├── index.js
        └── [book-id].js</code></pre>

If we updated the path to have more segments like categories, we might end up with something like: `/printed-books/design/:book-id`, `/printed-books/engineering/:book-id`, or better still `/printed-books/:category/:book-id`.

Let’s add the release year: `/printed-books/:category/:release-year/:book-id`. Can you see a pattern? The directory structure becomes:

<pre><code class="language-javascript">next-app
└── pages
    ├── index.js
    └── printed-books
        └── [category]
            └── [release-year]
                └── [book-id].js</code></pre>

We substituted the use of named files for dynamic routes, but somehow still ended up with another form of redundancy. Well, there’s a fix: Catch All Routes that eliminates the need for deeply nested routes:

<pre><code class="language-javascript">next-app
└── pages
    ├── index.js
    └── printed-books
        └── [...slug].js</code></pre>

It uses the same bracket syntax except that it is prefixed with three dots. Think of the dots like the JavaScript spread syntax. You might be wondering: If I use the catch-all routes, how do I access the category (`[category]`), and release year (`[release-year]`). Two ways:

1. In the case of the printed-books example, the end goal is the book, and each book info will have its metadata attached with it, or
2. The “slug” segments are returned as an array of query parameter(s).

<div class="break-out">

<pre><code class="language-javascript">import { useRouter } from 'next/router';

export default function Book() {
  const { query } = useRouter();
  // There's a brief moment where `slug` is undefined
  // so we use the Optional Chaining (?.) and Nullish coalescing operator (??)
  // to check if slug is undefined, then fall back to an empty array
  const [category, releaseYear, bookId] = query?.slug ?? [];

  return (
    &lt;table&gt;
      &lt;tbody&gt;
        &lt;tr&gt;
          &lt;th&gt;Book Id&lt;/th&gt;
          &lt;td&gt;{bookId}&lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
          &lt;th&gt;Category&lt;/th&gt;
          &lt;td&gt;{category}&lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
          &lt;th&gt;Release Year&lt;/th&gt;
          &lt;td&gt;{releaseYear}&lt;/td&gt;
        &lt;/tr&gt;
      &lt;/tbody&gt;
    &lt;/table&gt;
  );
}</code></pre>
</div>

Here’s more example for the route `/printed-books/[…slug]`:

<table>
    <thead>
        <tr>
            <th>Path</th>
            <th>Query parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
      <td><code>/printed-books/click.js</code></td>
            <td>{ “slug”: [“click”] }</td>
        </tr>
        <tr>
      <td><code>/printed-books/2020/click.js</code></td>
            <td>{ “slug”: [“2020”, “click”] }</td>
        </tr>
        <tr>
      <td><code>/printed-books/design/2020/click.js</code></td>
            <td>{ “slug”: [“design”, “2020”, “click”] }</td>
        </tr>
    </tbody>
</table>

As it is with the catch-all route, the route `/printed-books` will throw a 404 error unless you provide a fallback index route.

<pre><code class="language-javascript">next-app
└── pages
    ├── index.js
    └── printed-books
        ├── index.js // path: /printed-books
        └── [...slug].js</code></pre>

This is because the catch-all route is “strict”. It either matches a slug, or it throws an error. If you’d like to avoid creating index routes alongside catch-all routes, you can use the **optional catch-all routes** instead.

### Extending Dynamic Route Segments With Optional Catch-All Routes

The syntax is the same as catch-all-routes, but with double square brackets instead.

<pre><code class="language-javascript">next-app
└── pages
    ├── index.js
    └── printed-books
        └── [[...slug]].js</code></pre>

In this case, the catch-all route (slug) is optional and if not available, fallbacks to the path `/printed-books`, rendered with `[[…slug]].js` route handler, without any query params.

<blockquote>Use catch-all alongside index routes, or optional catch-all routes alone. Avoid using catch-all and optional catch-all routes alongside.</blockquote>

### Routes Precedence

The capability to be able to define the most common routing patterns can be a “black swan”. The possibility of routes clashing is a looming threat, most especially when you start getting dynamic routes worked up.

When it makes sense to do so, Next.js lets you know about route clashes in the form of errors. When it doesn’t, it applies precedence to routes according to their specificity.

For example, it is an error to have more than one dynamic route on the same level.

<div class="break-out">

<pre><code class="language-javascript">// ❌ This is an error
// Failed to reload dynamic routes: Error: You cannot use different slug names for the // same dynamic path ('book-id' !== 'id').
next-app
└── pages
    ├── index.js
    └── printed-books
        ├── [book-id].js
        └── [id].js</code></pre>
</div>

If you look closely at the routes defined below, you’d notice the potential for clashes. 

<pre><code class="language-javascript">// Directory structure flattened for simplicity
next-app
└── pages
    ├── index.js // index route (also a predefined route)
    └── printed-books
        ├── index.js
        ├── tags.js // predefined route
        ├── [book-id].js // handles dynamic route
        └── [...slug].js // handles catch all route</code></pre>

For example, try answering this: what route handles the path `/printed-books/inclusive-components`?

 - `/printed-books/[book-id].js`, or
 - `/printed-books/[…slug].js`.

The answer lies in the “specificity” of the route handlers. Predefined routes come first, followed by dynamic routes, then catch-all routes. You can think of the route request/handling model as a pseudo-code with the following steps:

1. Is there is a **predefined route handler** that can handle the route?
    - `true` &mdash; handle the route request.
    - `false` &mdash; go to 2.
2. Is there a **dynamic route handler** that can handle the route?
    - `true` &mdash; handle the route request.
    - `false` &mdash; go to 3.
3. Is there a **catch-all route handler** that can handle the route?
    - `true` &mdash; handle the route request.
    - `false` &mdash; throw a 404 page not found.

Therefore, `/printed-books/[book-id].js` wins.

Here are more examples:

<table class="tablesaw break-out">
    <thead>
        <tr>
            <th>Route</th>
            <th>Route handler</th>
      <th>Type of route</th>
        </tr>
    </thead>
    <tbody>
        <tr>
      <td><code>/printed-books</code></td>
            <td><code>/printed-books</code></td>
      <td>Index route</td>
        </tr>
        <tr>
            <td><code>/printed-books/tags</code></td>
            <td><code>/printed-books/tags.js</code></td>
      <td>Predefined route</td>
        </tr>
        <tr>
            <td><code>/printed-books/inclusive-components</code></td>
            <td><code>/printed-books/[book-id].js</code></td>
      <td>Dynamic route</td>
        </tr>
    <tr>
            <td><code>/printed-books/design/inclusive-components</code></td>
            <td><code>/printed-books/[...slug].js</code></td>
      <td>Catch-all route</td>
        </tr>
    </tbody>
</table>



## The `next/link` API

The `next/link` API exposes the `Link` component as a declarative way to perform client-side route transitions.

<pre><code class="language-javascript">import Link from 'next/link'

function TopNav() {
  return (
    &lt;nav&gt;
      &lt;Link href="/"&gt;Smashing Magazine&lt;/Link&gt;
      &lt;Link href="/articles"&gt;Articles&lt;/Link&gt;
      &lt;Link href="/guides"&gt;Guides&lt;/Link&gt;
      &lt;Link href="/printed-books"&gt;Books&lt;/Link&gt;
    &lt;/nav&gt;
  )
}</code></pre>

The `Link` component will resolve to a regular HTML hyperlink. That is, `<Link href="/">Smashing Magazine</Link>` will resolve to  `<a href="/">Smashing Magazine</a>`.

The `href` prop is the only required prop to the `Link` component. See the [docs](https://nextjs.org/docs/api-reference/next/link) for a complete list of props available on the `Link` component.

There are other mechanisms of the `Link` component to be aware of.

### Routes With Dynamic Segments

Prior to Next.js 9.5.3, `Link`ing to dynamic routes meant that you had to provide both the `href` and `as` prop to `Link` as in:

<pre><code class="language-javascript">import Link from 'next/link';

const printedBooks = [
  { name: 'Ethical Design', id: 'ethical-design' },
  { name: 'Design Systems', id: 'design-systems' },
];

export default function PrintedBooks() {
  return printedBooks.map((printedBook) =&gt; (
    &lt;Link
      href="/printed-books/[printed-book-id]"
      as={`/printed-books/${printedBook.id}`}
    &gt;
      {printedBook.name}
    &lt;/Link&gt;
  ));
}</code></pre>

Although this allowed Next.js to interpolate the href for the dynamic parameters, it was tedious, error-prone, and somewhat imperative, and has now been fixed for the majority of use-cases with the release of Next.js 10. 

This fix is also backward compatible. If you have been using both `as` and `href`, nothing breaks. To adopt the new syntax, discard the `href` prop and its value, and rename the `as` prop to `href` as in the example below:

<div class="break-out">

<pre><code class="language-javascript">import Link from 'next/link';

const printedBooks = [
  { name: 'Ethical Design', id: 'ethical-design' },
  { name: 'Design Systems', id: 'design-systems' },
];

export default function PrintedBooks() {
  return printedBooks.map((printedBook) =&gt; (
    &lt;Link href={`/printed-books/${printedBook.id}`}&gt;{printedBook.name}&lt;/Link&gt;
  ));
}</code></pre>
</div>

> See [Automatic resolving of href](https://nextjs.org/blog/next-10#automatic-resolving-of-href).

### Use-cases For The `passHref` Prop

Take a close look at the snippet below:

<div class="break-out">

<pre><code class="language-javascript">import Link from 'next/link';

const printedBooks = [
  { name: 'Ethical Design', id: 'ethical-design' },
  { name: 'Design Systems', id: 'design-systems' },
];

// Say this has some sort of base styling attached
function CustomLink({ href, name }) {
  return &lt;a href={href}&gt;{name}&lt;/a&gt;;
}

export default function PrintedBooks() {
  return printedBooks.map((printedBook) =&gt; (
    &lt;Link href={`/printed-books/${printedBook.id}`} passHref&gt;
      &lt;CustomLink name={printedBook.name} /&gt;
    &lt;/Link&gt;
  ));
}</code></pre>
</div>

The `passHref` props force the `Link` component to pass the `href` prop down to the `CustomLink` child component. This is compulsory if the `Link` component wraps over a component that returns a hyperlink `<a>` tag. Your use-case might be because you are using a library like styled-components, or if you need to pass multiple children to the `Link` component, as it only expects a single child.

> See the [docs](https://nextjs.org/docs/api-reference/next/link#if-the-child-is-a-custom-component-that-wraps-an-a-tag) to learn more.

### URL Objects

The `href` prop of the `Link` component can also be a URL object with properties like `query` which is automatically formatted into a URL string.

With the `printedBooks` object, the example below will link to:

1. `/printed-books/ethical-design?name=Ethical+Design` and
2. `/printed-books/design-systems?name=Design+Systems`.

<pre><code class="language-javascript">import Link from 'next/link';

const printedBooks = [
  { name: 'Ethical Design', id: 'ethical-design' },
  { name: 'Design Systems', id: 'design-systems' },
];

export default function PrintedBooks() {
  return printedBooks.map((printedBook) =&gt; (
    &lt;Link
      href={{
        pathname: `/printed-books/${printedBook.id}`,
        query: { name: `${printedBook.name}` },
      }}
    &gt;
      {printedBook.name}
    &lt;/Link&gt;
  ));
}</code></pre>

If you include a dynamic segment in the `pathname`, then you must also include it as a property in the query object to make sure the query is interpolated in the `pathname`:

<pre><code class="language-javascript">import Link from 'next/link';

const printedBooks = [
  { name: 'Ethical Design', id: 'ethical-design' },
  { name: 'Design Systems', id: 'design-systems' },
];

// In this case the dynamic segment `[book-id]` in pathname
// maps directly to the query param `book-id`
export default function PrintedBooks() {
  return printedBooks.map((printedBook) =&gt; (
    &lt;Link
      href={{
        pathname: `/printed-books/[book-id]`,
        query: { 'book-id': `${printedBook.id}` },
      }}
    &gt;
      {printedBook.name}
    &lt;/Link&gt;
  ));
}</code></pre>

The example above have paths:

1. `/printed-books/ethical-design`, and
2. `/printed-books/design-systems`.

If you inspect the `href` attribute in VSCode, you’d find the type `LinkProps`, with the `href` property a `Url` type, which is either a `string` or `UrlObject` as mentioned previously.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742d24b6-2df9-4547-b6ae-29ec805103fa/1-client-side-routing-next-js.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742d24b6-2df9-4547-b6ae-29ec805103fa/1-client-side-routing-next-js.png" width="800" height="618" sizes="100vw" caption="Inspecting <code>LinkProps</code> in VSCode. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/742d24b6-2df9-4547-b6ae-29ec805103fa/1-client-side-routing-next-js.png'>Large preview</a>)" alt="A screenshot of the inspected LinkProps type in VSCode" >}}

Inspecting the `UrlObject` further leads to the interface with the properties:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f943f3e-3c10-4cc8-b386-c8237a0f8cfd/2-client-side-routing-next-js.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f943f3e-3c10-4cc8-b386-c8237a0f8cfd/2-client-side-routing-next-js.png" width="800" height="596" sizes="100vw" caption="Inspecting UrlObject in VSCode. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f943f3e-3c10-4cc8-b386-c8237a0f8cfd/2-client-side-routing-next-js.png'>Large preview</a>)" alt="A screenshot of the inspected <code>UrlObject</code> in VSCode" >}}

You can learn more about these properties in the [Node.js URL module documentation](https://nodejs.org/api/url.html#url_url_strings_and_url_objects).

One use case of the hash is to link to specific sections in a page.

<div class="break-out">

<pre><code class="language-javascript">import Link from 'next/link';

const printedBooks = [{ name: 'Ethical Design', id: 'ethical-design' }];

export default function PrintedBooks() {
  return printedBooks.map((printedBook) =&gt; (
    &lt;Link
      href={{
        pathname: `/printed-books/${printedBook.id}`,
        hash: 'faq',
      }}
    &gt;
      {printedBook.name}
    &lt;/Link&gt;
  ));
}</code></pre>
</div>

The hyperlink will resolve to `/printed-books/ethical-design#faq`.

> Learn more in [the docs](https://nextjs.org/docs/api-reference/next/link#with-url-object).

{{% ad-panel-leaderboard %}}

## The `next/router` API

If the `next/link` is declarative, then the `next/router` is imperative. It exposes a `useRouter` hook that allows access to the [`router`](https://nextjs.org/docs/api-reference/next/router#router-object) object inside any function component. You can use this hook to manually perform routing, most especially in certain scenarios where the `next/link` is not enough, or where you need to “hook” into the routing.

<div class="break-out">

<pre><code class="language-javascript">import { useRouter } from 'next/router';

export default function Home() {
  const router = useRouter();

  function handleClick(e) {
    e.preventDefault();
    router.push(href);
  }

  return (
    &lt;button type="button" onClick={handleClick}&gt;Click me&lt;/button&gt;
  )
}</code></pre>
</div>

`useRouter` is a React hook and cannot be used with classes. Need the `router` object in class components? Use `withRouter`.

<div class="break-out">

<pre><code class="language-javascript">import { withRouter } from 'next/router';

function Home({router}) {
  function handleClick(e) {
    e.preventDefault();
    router.push(href);
  }

  return (
    &lt;button type="button" onClick={handleClick}&gt;Click me&lt;/button&gt;
  )
}

export default withRouter(Home);</code></pre>
</div>

### The `router` Object

Both the `useRouter` hook and `withRouter` higher-order component, return a router object with properties like `pathname`, `query`, `asPath`, and `basePath` that gives you information about the URL state of the current page, `locale`, `locales`, and `defaultLocale` that gives information about the active, supported, or current default locale.

The router object also has methods like `push` for navigating to a new URL by adding a new URL entry into the history stack, `replace`, similar to push but replaces the current URL instead of adding a new URL entry into the history stack.

Learn more about the [router object](https://nextjs.org/docs/api-reference/next/router#router-object).

## Custom Route Configuration With `next.config.js`

This is a regular Node.js module that can be used to configure certain Next.js behavior.

<pre><code class="language-javascript">module.exports = {
  // configuration options
}</code></pre>

> Remember to restart your server anytime you update `next.config.js`. [Learn more](https://nextjs.org/docs/api-reference/next.config.js/introduction).

### Base Path

It was mentioned that the initial/default route in Next.js is `pages/index.js` with path `/`. This is configurable and you can make your default route a sub-path of the domain.

<pre><code class="language-javascript">module.exports = {
  // old default path: /
  // new default path: /dashboard
  basePath: '/dashboard',
};</code></pre>

These changes will automatically take effect in your application with all `/` paths routed to `/dashboard`.

> This feature can only be used with Next.js 9.5 and above. [Learn more](https://nextjs.org/docs/api-reference/next.config.js/basepath).

### Trailing Slash

By default, a trailing slash will not be available at the end of each URL. However, you can switch that with:

<pre><code class="language-javascript">module.exports = {
  trailingSlash: true
};</code></pre>

<pre><code class="language-javascript"># trailingSlash: false
/printed-books/ethical-design#faq
# trailingSlash: true
/printed-books/ethical-design/#faq</code></pre>

Both the [base path](https://nextjs.org/docs/api-reference/next.config.js/basepath) and [trailing slash](https://nextjs.org/docs/api-reference/next.config.js/trailing-slash) features can only be used with Next.js 9.5 and above.

## Conclusion

Routing is one of the most important parts of your Next.js application, and it reflects in the file-system-based router built on the concept of pages. Pages can be used to define the most common route patterns. The concepts of routing and rendering are closely related. Take the lessons of this article with you as you build your own Next.js app or work on a Next.js codebase. And check the resources below to learn more.

### Related Resources

- [Next.js official documentation for Pages](https://nextjs.org/docs/basic-features/pages)
- [Next.js official documentation for data fetching](https://nextjs.org/docs/basic-features/data-fetching)
- [Next.js official documentation for next.config.js](https://nextjs.org/docs/api-reference/next.config.js/introduction)
- [Next.js 10: Automatic resolving of](https://nextjs.org/blog/next-10#automatic-resolving-of-href) [`href`](https://nextjs.org/blog/next-10#automatic-resolving-of-href)
- [Next.js official documentation for next/link](https://nextjs.org/docs/api-reference/next/link)
- [Next.js official documentation for next/router](https://nextjs.org/docs/api-reference/next/router)

{{< signature "vf, yk, il" >}}

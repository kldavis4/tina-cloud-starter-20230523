---
title: 'What Web Frameworks Solve And How To Do Without Them (Part 1)'
slug: web-frameworks-guide-part1
author: noam-rosenthal
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7ca7294e-9325-4bab-8617-0bc3d42e3053/web-frameworks-guide.jpg
date: 2022-01-28T14:00:00.000Z
summary: >-
  In this article, Noam Rosenthal dives deep into a few technical features that are common across frameworks, and explains how some of the different frameworks implement them and what they cost.
description: >-
  In this article, Noam Rosenthal dives deep into a few technical features that are common across frameworks, and explains how some of the different frameworks implement them and what they cost.
categories:
  - React
  - Frameworks
  - JavaScript
---

I have recently become very interested in comparing frameworks to vanilla JavaScript. It started after some frustration I had using React in some of my freelance projects, and with my recent, more intimate acquaintance with web standards as a specification editor.

I was interested to see what are the **commonalities and differences between the frameworks**, what the web platform has to offer as a leaner alternative, and whether it’s sufficient. My objective is not to bash frameworks, but rather to understand the costs and benefits, to determine whether an alternative exists, and to see whether we can learn from it, even if we do decide to use a framework.

In this first part, I will deep dive into a few technical features common across frameworks, and how some of the different frameworks implement them. I will also look at the cost of using those frameworks.

## The Frameworks

I chose four frameworks to look at: React, being the dominant one today, and three newer contenders that claim to do things differently from React.

- [React](https://reactjs.org/)  
“React makes it painless to create interactive UIs. Declarative views make your code more predictable and easier to debug.”
- [SolidJS](https://www.solidjs.com/)  
“Solid follows the same philosophy as React… It however has a completely different implementation that forgoes using a virtual DOM.”
- [Svelte](https://svelte.dev/)  
“Svelte is a radical new approach to building user interfaces… a compile step that happens when you build your app. Instead of using techniques like virtual DOM diffing, Svelte writes code that surgically updates the DOM when the state of your app changes.”
- [Lit](https://lit.dev/)  
“Building on top of the Web Components standards, Lit adds just … reactivity, declarative templates, and a handful of thoughtful features.”

To summarize what the frameworks say about their differentiators:

- React makes building UIs easier with declarative views.
- SolidJS follows React’s philosophy but uses a different technique.
- Svelte uses a compile-time approach to UIs.
- Lit uses existing standards, with some added lightweight features.

## What Frameworks Solve

The frameworks themselves mention the words declarative, reactivity, and virtual DOM. Let’s dive into what those mean.

### Declarative Programming

Declarative programming is a paradigm in which logic is defined without specifying the control flow. We describe what the result needs to be, rather than what steps would take us there.

In the early days of declarative frameworks, circa 2010, DOM APIs were a lot more bare and verbose, and writing web applications with imperative JavaScript required a lot of boilerplate code. That’s when the concept of “[model-view-viewmodel](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel)” (MVVM) became prevalent, with the then-groundbreaking Knockout and AngularJS frameworks, providing a JavaScript declarative layer that handled that complexity inside the library.

MVVM is not a widely used term today, and it’s somewhat of a variation of the older term “data-binding”.

### Data Binding

Data binding is a declarative way to express how data is synchronized between a model and a user interface.

All of the popular UI frameworks provide some form of data-binding, and their tutorials start with a data-binding example.

Here is data-binding in JSX (SolidJS and React):

<pre><code class="language-javascript">function HelloWorld() {
 const name = "Solid or React";

 return (
     &lt;div&gt;Hello {name}!&lt;/div&gt;
 )
}
</code></pre>

Data-binding in Lit:

<pre><code class="language-javascript">class HelloWorld extends LitElement {
 @property()
 name = 'lit';

 render() {
   return html`&lt;p&gt;Hello ${this.name}!&lt;/p&gt;`;
 }
}
</code></pre>

Data-binding in Svelte:

<pre><code class="language-javascript">&lt;script&gt;
  let name = 'world';
&lt;/script&gt;

&lt;h1&gt;Hello {name}!&lt;/h1&gt;
</code></pre>

### Reactivity

Reactivity is a declarative way to express the propagation of change.

When we have a way to declaratively express data-binding, we need an efficient way for the framework to propagate changes.

The React engine compares the result of rendering with the previous result, and it applies the difference to the DOM itself. This way of handling change propagation is called the [virtual DOM](https://reactjs.org/docs/faq-internals.html#what-is-the-virtual-dom).

In SolidJS, this is done more explicitly, with its store and built-in elements. For example, the `Show` element would keep track of what has changed internally, instead of the virtual DOM.

In Svelte, the “reactive” code is generated. Svelte knows which events can cause a change, and it generates straightforward code that draws the line between the event and the DOM change.

In Lit, reactivity is accomplished using element properties, essentially relying on the built-in reactivity of HTML custom elements.

{{% feature-panel %}}

### Logic

When a framework provides a declarative interface for data-binding, with its implementation of reactivity, it also needs to provide some way to express some of the logic that is traditionally written imperatively. The basic building blocks of logic are “if” and “for”, and all of the major frameworks provide some expression of these building blocks.

#### Conditionals

Apart from binding basic data such as numbers and string, every framework supplies a “conditional” primitive. In React, it looks like this:

<pre><code class="language-javascript">const [hasError, setHasError] = useState(false);  
return hasError ? &lt;label&gt;Message&lt;/label&gt; : null;
…
setHasError(true);
</code></pre>

SolidJS provides a built-in conditional component, [`Show`](https://www.solidjs.com/docs/latest/api#%3Cshow%3E):

<pre><code class="language-javascript">&lt;Show when={state.error}&gt;
  &lt;label&gt;Message&lt;/label&gt;
&lt;/Show&gt;
</code></pre>

Svelte provides the `#if` directive:

<pre><code class="language-javascript">{#if state.error}
  &lt;label&gt;Message&lt;/label&gt;
{/if}
</code></pre>

In Lit, you’d use an explicit ternary operation in the `render` function:

<pre><code class="language-javascript">render() {
 return this.error ? html`&lt;label&gt;Message&lt;/label&gt;`: null;
}
</code></pre>

#### Lists

The other common framework primitive is list-handling. Lists are a key part of UIs &mdash; list of contacts, notifications, etc. &mdash; and to work efficiently, they need to be reactive, not updating the whole list when one data item changes.

In React, list-handling looks like this:

<pre><code class="language-javascript">contacts.map((contact, index) =>
 &lt;li key={index}&gt;
   {contact.name}
 &lt;/li&gt;)
</code></pre>

React uses the special `key` attribute to differentiate between list items, and it makes sure that the whole list doesn’t get replaced with every render.

In SolidJS, the `for` and `index` built-in elements are used:

<pre><code class="language-javascript">&lt;For each={state.contacts}&gt;
  {contact => &lt;DIV&gt;{contact.name}&lt;/DIV&gt; }
&lt;/For&gt;
</code></pre>

Internally, SolidJS uses its own store in conjunction with `for` and `index` to decide which elements to update when items change. It’s more explicit than React, allowing us to avoid the complexity of the virtual DOM.

Svelte uses the `each` directive, which gets transpiled based on its updaters:

<pre><code class="language-javascript">{#each contacts as contact}
  &lt;div&gt;{contact.name}&lt;/div&gt;
{/each}
</code></pre>

Lit supplies a `repeat` function, which works similarly to React’s `key`-based list mapping:

<pre><code class="language-javascript">repeat(contacts, contact => contact.id,
    (contact, index) => html`&lt;div&gt;${contact.name}&lt;/div&gt;`
</code></pre>

### Component Model

One thing that is out of the scope of this article is the component model in the different frameworks and how it can be dealt with using custom HTML elements.

**Note**: *This is a big subject, and I hope to cover it in a future article because this one would get too long. :)*

{{% ad-panel-leaderboard %}}

## The Cost

Frameworks provide declarative data-binding, control flow primitives (conditionals and lists), and a reactive mechanism to propagate changes.

They also provide other major things, such as a way to reuse components, but that’s a subject for a separate article.

Are frameworks useful? Yes. They give us all of these convenient features. But is that the right question to ask? Using a framework comes at a cost. Let’s see what those costs are.

### Bundle Size

When looking at bundle size, I like looking at the minified non-Gzip’d size. That’s the size that is the most relevant to the CPU cost of JavaScript execution.

- ReactDOM is about 120 KB.
- SolidJS is about 18 KB.
- Lit is about 16 KB.
- Svelte is about 2 KB, but the size of the generated code varies.

It seems that today’s frameworks are doing a better job than React of keeping the bundle size small. The virtual DOM requires a lot of JavaScript.

### Builds

Somehow we got used to “building” our web apps. It’s impossible to start a front-end project without setting up Node.js and a bundler such as Webpack, dealing with some recent configuration changes in the Babel-TypeScript starter pack, and all that jazz.

The more expressive and the smaller the bundle size of the framework, the bigger the burden of build tools and transpilation time.

Svelte claims that the [virtual DOM is pure overhead](https://svelte.dev/blog/virtual-dom-is-pure-overhead). I agree, but perhaps “building” (as with Svelte and SolidJS) and custom client-side template engines (as with Lit) are also pure overhead, of a different kind?

### Debugging

With building and transpilation come a different kind of cost.

The code we see when we use or debug the web app is totally different from what we wrote. We now rely on special debugging tools of varying quality to reverse engineer what happens on the website and to connect it with bugs in our own code.

In React, the call stack is never “yours” &mdash; React handles scheduling for you. This works great when there are no bugs. But try to identify the cause of infinite-loop re-renders and you’ll be in for a world of pain.

In Svelte, the bundle size of the library itself is small, but you’re going to ship and debug a whole bunch of cryptic generated code that is Svelte’s implementation of reactivity, customized to your app’s needs.

With Lit, it’s less about building, but to debug it effectively you have to understand its template engine. This might be the biggest reason why my sentiment towards frameworks is skeptical.

When you look for custom declarative solutions, you end up with more painful imperative debugging. The examples in this document use Typescript for API specification, but the code itself doesn’t require transpilation.

### Upgrades

In this document, I’ve looked at four frameworks, but there are more frameworks than I can count (AngularJS, Ember.js, and Vue.js, to name a [few](https://en.wikipedia.org/wiki/Comparison_of_JavaScript-based_web_frameworks)). Can you count on the framework, its developers, its mindshare, and its ecosystem to work for you as it evolves?

One thing that is more frustrating than fixing your own bugs is having to find workarounds for framework bugs. And one thing that’s more frustrating than framework bugs are bugs that occur when you upgrade a framework to a new version without modifying your code.

True, this problem also exists in browsers, but when it occurs, it happens to everyone, and in most cases a fix or a published workaround is imminent. Also, most of the patterns in this document are based on mature web platform APIs; there is not always a need to go with the bleeding edge.

{{% ad-panel-leaderboard %}}

## Summary

We dived a bit deeper into understanding the core problems frameworks try to solve and how they go about solving them, focusing on data-binding, reactivity, conditionals and lists. We also looked at the cost.

In [Part 2](https://www.smashingmagazine.com/2022/02/web-frameworks-guide-part2), we will see how these problems can be addressed without using a framework at all, and what we can learn from it. Stay tuned!

*Special thanks to the following individuals for technical reviews: Yehonatan Daniv, Tom Bigelajzen, Benjamin Greenbaum, Nick Ribal and Louis Lazaris.*

{{< signature "vf, il, al" >}}

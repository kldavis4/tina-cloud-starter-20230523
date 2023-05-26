---
title: 'Tree-Shaking: A Reference Guide'
slug: tree-shaking-reference-guide
author: atila-fassina
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0e27a101-d2e0-4661-9e12-b53b68051dbf/tree-shaking-reference-guide.jpg
date: 2021-05-14T10:30:00.000Z
summary: >-
  “Tree-shaking” is a must-have performance optimization when bundling JavaScript. In this article, we dive deeper on how exactly it works and how specs and practice intertwine to make bundles leaner and more performant. Plus, you’ll get a tree-shaking checklist to use for your projects.
description: >-
  “Tree-shaking” is a must-have performance optimization when bundling JavaScript. In this article, we dive deeper on how exactly it works and how specs and practice intertwine to make bundles leaner and more performant. Plus, you’ll get a tree-shaking checklist to use for your projects.
categories:
  - Guides
  - Webpack
  - JavaScript
  - Optimization
---

Before starting our journey to learn what tree-shaking is and how to set ourselves up for success with it, we need to understand what modules are in the JavaScript ecosystem.

Since its early days, JavaScript programs have grown in complexity and the number of tasks they perform. The need to compartmentalize such tasks into closed scopes of execution became apparent. These compartments of tasks, or values, are what we call **modules**. They’re main purpose is to prevent repetition and to leverage reusability. So, architectures were devised to allow such special kinds of scope, to expose their values and tasks, and to consume external values and tasks.

To dive deeper into what modules are and how they work, I recommend “[ES Modules: A Cartoon Deep-Dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)”. But to understand the nuances of tree-shaking and module consumption, the definition above should suffice.

## What Does Tree-Shaking Actually Mean?

Simply put, tree-shaking means removing unreachable code (also known as dead code) from a bundle. As Webpack version 3’s documentation states:

<blockquote>“You can imagine your application as a tree. The source code and libraries you actually use represent the green, living leaves of the tree. Dead code represents the brown, dead leaves of the tree that are consumed by autumn. In order to get rid of the dead leaves, you have to shake the tree, causing them to fall.”</blockquote>

The term was first popularized in the front-end community by [the Rollup team](https://rollupjs.org/guide/en/#tree-shaking). But authors of all dynamic languages have been struggling with the problem since much earlier. The idea of a tree-shaking algorithm can be traced back to at least the early 1990s.

In JavaScript land, tree-shaking has been possible since the ECMAScript module (ESM) specification in ES2015, previously known as ES6. Since then, tree-shaking has been enabled by default in most bundlers because they reduce output size without changing the program’s behaviour.

The main reason for this is that ESMs are static by nature. Let‘s dissect what that means.

{{% feature-panel %}}

## ES Modules vs. CommonJS

CommonJS predates the ESM specification by a few years. It came about to address the lack of support for reusable modules in the JavaScript ecosystem. CommonJS has a `require()` function that fetches an external module based on the path provided, and it adds it to the scope during runtime.

That `require` is a `function` like any other in a program makes it hard enough to evaluate its call outcome at compile-time. On top of that is the fact that adding `require` calls anywhere in the code is possible &mdash; wrapped in another function call, within if/else statements, in switch statements, etc.

With the learning and struggles that have resulted from wide adoption of the CommonJS architecture, the ESM specification has settled on this new architecture, in which modules are imported and exported by the respective keywords `import` and `export`. Therefore, no more functional calls. ESMs are also allowed only as top-level declarations &mdash; nesting them in any other structure is not possible, being as they are **static**: ESMs do not depend on runtime execution.

## Scope and Side Effects

There is, however, another hurdle that tree-shaking must overcome to evade bloat: side effects. A function is considered to have side effects when it alters or relies on factors external to the scope of execution. A function with side effects is considered **impure**. A pure function will always yield the same result, regardless of context or the environment it’s been run in.

<pre><code class="language-ts">const pure = (a:number, b:number) => a + b
const impure = (c:number) => window.foo.number + c
</code></pre>

Bundlers serve their purpose by evaluating the code provided as much as possible in order to determine whether a module is pure. But code evaluation during compiling time or bundling time can only go so far. Therefore, it’s assumed that packages with side effects cannot be properly eliminated, even when completely unreachable.

Because of this, bundlers now accept a key inside the module’s `package.json` file that allows the developer to declare whether a module has no side effects. This way, the developer can opt out of code evaluation and hint the bundler; the code within a particular package can be eliminated if there’s no reachable import or `require` statement linking to it. This not only makes for a leaner bundle, but also can speed up compiling times.

<pre><code class="language-json">
{
	"name": "my-package",
	"sideEffects": false
}
</code></pre>

So, if you are a package developer, make conscientious use of `sideEffects` before publishing, and, of course, revise it upon every release to avoid any unexpected breaking changes.

In addition to the root `sideEffects` key, it is also possible to determine purity on a file-by-file basis, by annotating an inline comment, `/*@__PURE__*/`, to your method call.

<pre><code class="language-javascript">const x = */@__PURE__*/eliminated_if_not_called()
</code></pre>

I consider this inline annotation to be an escape hatch for the consumer developer, to be done in case a package has not declared `sideEffects: false` or in case the library does indeed present a side effect on a particular method.

## Optimizing Webpack

From version 4 onward, Webpack has required progressively less configuration to get best practices working. The functionality for a couple of plugins has been incorporated into core. And because the development team takes bundle size very seriously, they have made tree-shaking easy.

If you’re not much of a tinkerer or if your application has no special cases, then tree-shaking your dependencies is a matter of just one line.

The `webpack.config.js` file has a root property named `mode`. Whenever this property’s value is `production`, it will tree-shake and fully optimize your modules. Besides eliminating dead code with the `TerserPlugin`, `mode: 'production'` will enable deterministic mangled names for modules and chunks, and it will activate the following plugins:

- flag dependency usage,
- flag included chunks,
- module concatenation,
- no emit on errors.

It’s not by accident that the trigger value is `production`. You will not want your dependencies to be fully optimized in a development environment because it will make issues much more difficult to debug. So I would suggest going about it with one of two approaches.

On the one hand, you could pass a `mode` flag to the Webpack command line interface:

<pre><code class="language-bash"># This will override the setting in your webpack.config.js
webpack --mode=production
</code></pre>

Alternatively, you could use the `process.env.NODE_ENV` variable in `webpack.config.js`:

<pre><code class="language-javascript">mode: process.env.NODE_ENV === 'production' ? 'production' : development
</code></pre>

In this case, you must remember to pass `--NODE_ENV=production` in your deployment pipeline.

Both approaches are an abstraction on top of the much known `definePlugin` from Webpack version 3 and below. Which option you choose makes absolutely no difference.

{{% ad-panel-leaderboard %}}

## Webpack Version 3 and Below

It’s worth mentioning that the scenarios and examples in this section might not apply to recent versions of Webpack and other bundlers. This section considers usage of [UglifyJS version 2](https://github.com/mishoo/UglifyJS/tree/v2.x), instead of [Terser](https://github.com/terser/terser). UglifyJS is the package that Terser was forked from, so code evaluation might differ between them.

Because Webpack version 3 and below don’t support the `sideEffects` property in `package.json`, all packages must be completely evaluated before the code gets eliminated. This alone makes the approach less effective, but several caveats must be considered as well.

As mentioned above, the compiler has no way of finding out by itself when a package is tampering with the global scope. But that’s not the only situation in which it skips tree-shaking. There are fuzzier scenarios.

Take this package example from Webpack’s documentation:

<pre><code class="language-javascript">// transform.js
import * as mylib from 'mylib';

export const someVar = mylib.transform({
  // ...
});

export const someOtherVar = mylib.transform({
  // ...
});
</code></pre>

And here is the entry point of a consumer bundle:

<pre><code class="language-javascript">// index.js

import { someVar } from './transforms.js';

// Use `someVar`...
</code></pre>

There’s no way to determine whether `mylib.transform` instigates side effects. Therefore, no code will be eliminated.

Here are other situations with a similar outcome:

- invoking a function from a third-party module that the compiler cannot inspect,
- re-exporting functions imported from third-party modules.

A tool that might help the compiler get tree-shaking to work is [babel-plugin-transform-imports](https://www.npmjs.com/package/babel-plugin-transform-imports). It will split all member and named exports into default exports, allowing the modules to be evaluated individually.

<pre><code class="language-javascript">// before transformation
import { Row, Grid as MyGrid } from 'react-bootstrap';
import { merge } from 'lodash';

// after transformation
import Row from 'react-bootstrap/lib/Row';
import MyGrid from 'react-bootstrap/lib/Grid';
import merge from 'lodash/merge';
</code></pre>

It also has a configuration property that warns the developer to avoid troublesome import statements. If you’re on Webpack version 3 or above, and you have done your due diligence with basic configuration and added the recommended plugins, but your bundle still looks bloated, then I recommend giving this package a try.

## Scope Hoisting and Compile Times

In the time of CommonJS, most bundlers would simply wrap each module within another function declaration and map them inside an object. That’s not any different than any map object out there:

<pre><code class="language-javascript">(function (modulesMap, entry) {
  // provided CommonJS runtime
})({
  "index.js": function (require, module, exports) {
	 let { foo } = require('./foo.js')
	 foo.doStuff()
  },
  "foo.js": function(require, module, exports) {
     module.exports.foo = {
	   doStuff: () => { console.log('I am foo') }
	 }
  }
}, "index.js")
</code></pre>

Apart from being hard to analyze statically, this is fundamentally incompatible with ESMs, because we’ve seen that we cannot wrap `import` and `export` statements. So, nowadays, bundlers hoist every module to the top level:

<pre><code class="language-javascript">// moduleA.js
let $moduleA$export$doStuff = () => ({
  doStuff: () => {}
})

// index.js
$moduleA$export$doStuff()
</code></pre>

This approach is fully compatible with ESMs; plus, it allows code evaluation to easily spot modules that aren’t being called and to drop them. The caveat of this approach is that, during compiling, it takes considerably more time because it touches every statement and stores the bundle in memory during the process. That’s a big reason why bundling performance has become an even greater concern to everyone and why compiled languages are being leveraged in tools for web development. For example, [esbuild](https://esbuild.github.io/) is a bundler written in Go, and [SWC](https://swc.rs/) is a TypeScript compiler written in Rust that integrates with Spark, a bundler also written in Rust.

To better understand scope hoisting, I highly recommend [Parcel version 2’s documentation](https://v2.parceljs.org/features/scope-hoisting/).

## Avoid Premature Transpiling

There’s one specific issue that is unfortunately rather common and can be devastating for tree-shaking. In short, it happens when you’re working with special loaders, integrating different compilers to your bundler. Common combinations are TypeScript, Babel, and Webpack &mdash; in all possible permutations.

Both Babel and TypeScript have their own compilers, and their respective loaders allow the developer to use them, for easy integration. And therein lies the hidden threat.

These compilers reach your code _before_ code optimization. And whether by default or misconfiguration, these compilers often output CommonJS modules, instead of ESMs. As mentioned in a previous section, CommonJS modules are dynamic and, therefore, cannot be properly evaluated for dead-code elimination.

This scenario is becoming even more common nowadays, with the growth of “isomorphic” apps (i.e. apps that run the same code both server- and client-side). Because Node.js does not have standard support for ESMs yet, when compilers are targeted to the `node` environment, they output CommonJS.

So, be sure to **check the code that your optimization algorithm is receiving**.

{{% ad-panel-leaderboard %}}

## Tree-Shaking Checklist

Now that you know the ins and outs of how bundling and tree-shaking work, let’s draw ourselves a checklist that you can print somewhere handy for when you revisit your current implementation and code base. Hopefully, this will save you time and allow you to optimize not only the perceived performance of your code, but maybe even your pipeline’s build times!

1. Use ESMs, and not only in your own code base, but also favour packages that output ESM as their consumables.
2. Make sure you know exactly which (if any) of your dependencies have not declared `sideEffects` or have them set as `true`.
3. Make use of inline annotation to declare method calls that are **pure** when consuming packages with side effects.
4. If you’re outputting CommonJS modules, make sure to optimize your bundle **before** transforming the import and export statements.

## Package Authoring

Hopefully, by this point we all agree that ESMs are the way forward in the JavaScript ecosystem. As always in software development, though, transitions can be tricky. Luckily, package authors can adopt non-breaking measures to facilitate swift and seamless migration for their users.

With some small additions to `package.json`, your package will be able to tell bundlers the environments that the package supports and how they’re supported best. Here’s a [checklist from Skypack](https://docs.skypack.dev/package-authors/package-checks#esm):

- Include an ESM export.
- Add `"type": "module"`.
- Indicate an entry point through `"module": "./path/entry.js"` (a community convention).

And here’s an example that results when all best practices are followed and you wish to support both web and Node.js environments:

<pre><code class="language-javascript">{
	// ...
	"main": "./index-cjs.js",
	"module": "./index-esm.js",
	"exports": {
		"require": "./index-cjs.js",
		"import": "./index-esm.js"
	}
	// ...
}
</code></pre>

In addition to this, the Skypack team has introduced a **package quality score** as a benchmark to determine whether a given package is set up for longevity and best practices. The tool is [open-sourced on GitHub](https://github.com/skypackjs/package-check) and can be added as a `devDependency` to your package to perform the checks easily before each release.

## Wrapping Up

I hope this article has been useful to you. If so, consider sharing it with your network. I look forward to interacting with you in the comments or on Twitter.

## Useful Resources

### Articles and Documentation

- “[ES Modules: A Cartoon Deep-Dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)”, Lin Clark, Mozilla Hacks
- “[Tree Shaking](https://webpack.js.org/guides/tree-shaking/)”, Webpack
- “[Configuration](https://webpack.js.org/configuration/)”, Webpack
- “[Optimization](https://webpack.js.org/configuration/optimization/)”, Webpack
- “[Scope Hoisting](https://v2.parceljs.org/features/scope-hoisting/)”, Parcel version 2’s documentation

### Projects and Tools

- [Terser](https://github.com/terser/terser)
- [babel-plugin-transform-imports](https://www.npmjs.com/package/babel-plugin-transform-imports)
- [Skypack](https://skypack.dev)
- [Webpack](https://webpack.js.org/)
- [Parcel](https://v2.parceljs.org/)
- [Rollup](https://rollupjs.org/guide/en/#tree-shaking)
- [esbuild](https://esbuild.github.io/)
- [SWC](https://swc.rs/)
- [Package Check](https://github.com/skypackjs/package-check)

{{< signature "vf, il, al" >}}

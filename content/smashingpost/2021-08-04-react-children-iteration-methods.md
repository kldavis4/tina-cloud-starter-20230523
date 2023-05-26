---
title: 'React Children And Iteration Methods'
slug: react-children-iteration-methods
author: arihant-verma
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ae9c0d62-009e-45c0-a600-d747533e49e5/react-children-iteration-methods.jpg
date: 2021-08-04T10:30:00.000Z
summary: >-
  In this article, we’ll discuss and learn about the use case of iterating over React `children` and the ways to do it. In particular, we will deep dive into one of the utility methods, `React.Children.toArray`, that React gives us, which helps to iterate over the <code>children</code> in a way which ensures performance and determinism.
description: >-
  In this article, we’ll discuss and learn about the use case of iterating over React `children` and the ways to do it. In particular, we will deep dive into one of the utility methods, `React.Children.toArray`, that React gives us, which helps to iterate over the <code>children</code> in a way which ensures performance and determinism.
categories:
  - React
  - Tools
  - Performance
---

The most obvious and common prop that developers work with within React is the `children` prop. In the majority of cases, there is no need to understand how the `children` prop looks like. But in some cases, we want to inspect the `children` prop to maybe wrap each child in another element/component or to reorder or slice them. In those cases inspecting how the `children` prop looks like becomes essential.

In this article, we’ll look at a React utility `React.Children.toArray` which lets us prepare the `children` prop for inspection and iteration, some of its shortcomings and how to overcome them &mdash; through a small open-source package, to keep our React code function the way it is deterministically supposed to behave, keeping performance intact. If you know the basics of React and have at least an idea about what the `children` prop in React is, this article is for you.

While working with React, most of the time we do not touch the `children` prop any more than using it in React components directly.

<pre><code class="language-javascript">function Parent({ children }) {
  return &lt;div className="mt-10"&gt;{children}&lt;/div&gt;;
}</code></pre>

But sometimes we have to iterate over the `children` prop so that we can enhance or change the children without having the user of the components explicitly do it themselves. One common use case is to pass the iteration index-related information to child components of a parent like so:

<pre data-line="4, 13-21, 34-36, 41-43"><code class="language-javascript">import { Children, cloneElement } from "react";

function Breadcrumbs({ children }) {
  const arrayChildren = Children.toArray(children);

  return (
    &lt;ul
      style={{
        listStyle: "none",
        display: "flex",
      }}
    &gt;
      {Children.map(arrayChildren, (child, index) =&gt; {
        const isLast = index === arrayChildren.length - 1;

        if (! isLast && ! child.props.link ) {
          throw new Error(
            `BreadcrumbItem child no. ${index + 1}
            should be passed a 'link' prop`
          )
        } 

        return (
          &lt;&gt;
            {child.props.link ? (
              &lt;a
                href={child.props.link}
                style={{
                  display: "inline-block",
                  textDecoration: "none",
                }}
              &gt;
                &lt;div style={{ marginRight: "5px" }}&gt;
                  {cloneElement(child, {
                    isLast,
                  })}
                &lt;/div&gt;
              &lt;/a&gt;
            ) : (
              &lt;div style={{ marginRight: "5px" }}&gt;
                {cloneElement(child, {
                  isLast,
                })}
              &lt;/div&gt;
            )}
            {!isLast && (
              &lt;div style={{ marginRight: "5px" }}&gt;
                &gt;
              &lt;/div&gt;
            )}
          &lt;/&gt;
        );
      })}
    &lt;/ul&gt;
  );
}

function BreadcrumbItem({ isLast, children }) {
  return (
    &lt;li
      style={{
        color: isLast ? "black" : "blue",
      }}
    &gt;
      {children}
    &lt;/li&gt;
  );
}

export default function App() {
  return (
    &lt;Breadcrumbs&gt;
      &lt;BreadcrumbItem
        link="https://goibibo.com/"
      &gt;
        Goibibo
      &lt;/BreadcrumbItem&gt;

      &lt;BreadcrumbItem
        link="https://goibibo.com/hotels/"
      &gt;
        Hotels
      &lt;/BreadcrumbItem&gt;

      &lt;BreadcrumbItem&gt;
       A Fancy Hotel Name
      &lt;/BreadcrumbItem&gt;
    &lt;/Breadcrumbs&gt;
  );
}
</code></pre>

Take a look at the [Codesandbox demo](https://codesandbox.io/embed/sm-article-21-lt6le?fontsize=14&hidenavigation=1&theme=dark). Here we’re doing the following:

1. We are using the `React.Children.toArray` method to ensure that the `children` prop is always an array. If we do not do that, doing `children.length` might blow because the `children`  prop can be an object, an array, or even a function. Also, if we try to use the array `.map` method on `children` directly it might blow up.
2. In the parent `Breadcrumbs` component we are iterating over its children by using the utility method `React.Children.map`.
3. Because we have access to `index` inside the iterator function (second argument of callback function of `React.Children.map`) we are able to detect if the child is last-child or not.
4. If it is the last child we clone the element and pass in the `isLast` prop to it so that the child can style itself based on it.
5. If it is not the last child, we ensure that all those children which aren’t the last child have a `link` prop on them by throwing an error if they don’t. We clone the element as we did in step 4. and pass the `isLast` prop as we did before, but we also additionally wrap this cloned element in an anchor tag. 

The user of `Breadcrumbs` and `BreadcrumbItem` doesn’t have to worry about which children should have links and how they should be styled. Inside the `Breadcrumbs` component, it automatically gets handled.

This pattern of *implicitly* passing in props and/or having `state` in the parent and passing the state and state changers down to the children as props is called the [compound component pattern](https://kentcdodds.com/blog/compound-components-with-react-hooks/). You might be familiar with this pattern from React Router’s `Switch` component, which takes `Route` components as its children:

<pre><code class="language-javascript">// example from react router docs
// https://reactrouter.com/web/api/Switch

import { Route, Switch } from "react-router";

let routes = (
  &lt;Switch&gt;
    &lt;Route exact path="/"&gt;
      &lt;Home /&gt;
    &lt;/Route&gt;
    &lt;Route path="/about"&gt;
      &lt;About /&gt;
    &lt;/Route&gt;
    &lt;Route path="/:user"&gt;
      &lt;User /&gt;
    &lt;/Route&gt;
    &lt;Route&gt;
      &lt;NoMatch /&gt;
    &lt;/Route&gt;
  &lt;/Switch&gt;
);</code></pre>

Now that we have established that there are needs where we have to iterate over `children` prop sometimes, and having used two of the children utility methods `React.Children.map` and `React.Children.toArray`, let’s refresh our memory about one of them: `React.Children.toArray`.

{{% feature-panel %}}

## `React.Children.toArray`

Let’s start by seeing with an example what this method does and where it might be useful.

<pre><code class="language-javascript">import { Children } from 'react'

function Debugger({children}) {
  // let’s log some things
  console.log(children);
  console.log(
    Children.toArray(children)
  )
  return children;
}

const fruits = [
  {name: "apple", id: 1},
  {name: "orange", id: 2},
  {name: "mango", id: 3}
]

export default function App() {
  return (
    &lt;Debugger&gt;
        &lt;a
          href="https://css-tricks.com/"
          style={{padding: '0 10px'}}
        &gt;
          CSS Tricks
        &lt;/a&gt;

        &lt;a
          href="https://smashingmagazine.com/"
          style={{padding: '0 10px'}}
        &gt;
          Smashing Magazine
        &lt;/a&gt;

        {
          fruits.map(fruit =&gt; {
            return (
              &lt;div key={fruit.id} style={{margin: '10px'}}&gt;
                {fruit.name}
              &lt;/div&gt;
            )
          })
        }
    &lt;/Debugger&gt;
  )
}</code></pre>

Take a look at the [Codesandbox demo](https://codesandbox.io/embed/sm-article-22-hhuws?fontsize=14&hidenavigation=1&theme=dark). We have a `Debugger` component, which does nothing much in terms of rendering &mdash; it just returns `children` as is. But it does log two values: `children` and `React.Children.toArray(children)`.

If you open up the console, you’d be able to see the difference.

- The first statement which logs `children` prop, shows the following as its value’s data structure: 

<pre><code class="language-javascript">[
  Object1, ----&gt; first anchor tag
  Object2, ----&gt; second anchor tag
  [
    Object3, ----&gt; first fruit
    Object4, ----&gt; second fruit
    Object5] ----&gt; third fruit
  ]
]</code></pre>

- The second statement which logs `React.Children.toArray(children)` logs:

<pre><code class="language-javascript">[
  Object1, ----&gt; first anchor tag
  Object2, ----&gt; second anchor tag
  Object3, ----&gt; first fruit
  Object4, ----&gt; second fruit
  Object5, ----&gt; third fruit
]</code></pre>

Let’s read the method’s documentation in React docs to make sense of what is happening.

> `React.Children.toArray` returns the `children` opaque data structure as a flat array with keys assigned to each child. Useful if you want to manipulate collections of children in your render methods, especially if you want to reorder or slice `children` before passing it down.

Let’s break that down:

1. Returns the `children` opaque data structure as a flat array.
2. With keys assigned to each child.

The first point says that that `children` (which is an opaque data structure, meaning it can be an object, array, or a function, as described earlier) is converted to a flat array. Just like we saw in the example above. Additionally, this [GitHub issue comment](https://github.com/facebook/react/issues/6889#issuecomment-221858162) also explains its behavior:

> It (`React.Children.toArray`) does not pull children out of elements and flatten them, that wouldn’t really make any sense. It flattens nested arrays and objects, i.e. so that `[['a', 'b'],['c', ['d']]]` becomes something similar to `['a', 'b', 'c', 'd']`.

<pre><code class="language-javascript">React.Children.toArray(
  [
    ["a", "b"],
    ["c", ["d"]]
  ]
).length === 4;</code></pre>

Let’s see what the second point (‘With keys assigned to each child.’) says, by expanding one child each from the previous logs of the example.

### Expanded Child From  `console.log(children)`

<pre><code class="language-javascript">{
  $$typeof: Symbol(react.element),
  key: null,
  props: {
    href: "https://smashingmagazine.com",
    children: "Smashing Magazine",
    style: {padding: "0 10px"}
  },
  ref: null,
  type: "a",
  // … other properties
}</code></pre>

{{% ad-panel-leaderboard %}}

### Expanded Child From `console.log(React.Children.toArray(children))`

<pre data-line="3"><code class="language-javascript">{
  $$typeof: Symbol(react.element),
  key: ".0",
  props: {
    href: "https://smashingmagazine.com",
    children: "Smashing Magazine",
    style: {padding: "0 10px"}
  },
  ref: null,
  type: "a",
  // … other properties
}</code></pre>

As you can see, besides flattening the `children` prop into a flat array, it also adds unique keys to each of its children. From the React docs:

<blockquote><code>React.Children.toArray()</code> changes keys to preserve the semantics of nested arrays when flattening lists of children. That is, <code>toArray</code> prefixes each key in the returned array so that each element’s key is scoped to the input array containing it.</blockquote>

Because the `.toArray` method might change the order and place of `children`, it has to make sure that it maintains unique keys for each of them for [reconciliation and rendering optimization](https://reactjs.org/docs/reconciliation.html#recursing-on-children).

Let’s give a little bit more attention to *`so that each element’s key is scoped to the input array containing it.`*, by looking at the keys of each element of the second array (corresponding to `console.log(React.Children.toArray(children))`).

<pre data-line="6-10"><code class="language-javascript">import { Children } from 'react'

function Debugger({children}) {
  // let’s log some things
  console.log(children);
  console.log(
    Children.map(Children.toArray(children), child =&gt; {
      return child.key
    }).join('\n')
  )
  return children;
}

const fruits = [
  {name: "apple", id: 1},
  {name: "orange", id: 2},
  {name: "mango", id: 3}
]

export default function App() {
  return (
    &lt;Debugger&gt;
        &lt;a
          href="https://css-tricks.com/"
          style={{padding: '0 10px'}}
        &gt;
          CSS Tricks
        &lt;/a&gt;
        &lt;a
          href="https://smashingmagazine.com/"
          style={{padding: '0 10px'}}
        &gt;
          Smashing Magazine
        &lt;/a&gt;
        {
          fruits.map(fruit =&gt; {
            return (
              &lt;div key={fruit.id} style={{margin: '10px'}}&gt;
                {fruit.name}
              &lt;/div&gt;
            )
          })
        }
    &lt;/Debugger&gt;
  )
}</code></pre>

<pre><code class="language-javascript">.0  ----&gt; first link
.1  ----&gt; second link
.2:$1 ----&gt; first fruit
.2:$2 ----&gt; second fruit
.2:$3 ----&gt; third fruit</code></pre>

As you can see that the fruits, which were originally a nested array inside the original `children` array, have keys that are prefixed with `.2`. The `.2` corresponds to the fact that they were a part of an array. The suffix, namely `:$1` ,`:$2`, `:$3`, is corresponding to the jsx parent `div` element corresponding to fruits. If we had used index as key instead, then we’d have got `:0`, `:1`, `:2` as suffixes.

So suppose you had three level of nesting inside `children` array, like so:

<pre><code class="language-javascript">import { Children } from 'react'

function Debugger({children}) {
  const retVal = Children.toArray(children)
  console.log(
    Children.map(retVal, child => {
      return child.key
    }).join('\n')
  )
  return retVal
}

export default function App() {
  const arrayOfReactElements = [
    &lt;div key="1"&gt;First&lt;/div&gt;,
    [
      &lt;div key="2"&gt;Second&lt;/div&gt;,
      [
        &lt;div key="3"&gt;Third&lt;/div&gt;
      ]
    ]
  ];
  return (
    &lt;Debugger&gt;
      {arrayOfReactElements}
    &lt;/Debugger&gt;
  )
}</code></pre>

The keys will look like

<pre><code class="language-javascript">.$1
.1:$2
.1:1:$3</code></pre>

Check the [Codesandbox demo](https://codesandbox.io/embed/sm-article-23-5fwrd?fontsize=14&hidenavigation=1&theme=dark). The `$1`, `$2`, `$3` suffixes are because of the original keys put on the React elements in an array, otherwise React complains of lack of keys 😉 .

From whatever we’ve read so far we can come to two use cases for `React.Children.toArray`.

1. If there’s an absolute need that `children` should always be an array, you can use `React.Children.toArray(children)` instead. It’ll work perfectly even when `children` is an object or a function too.
    
2. If you have to sort, filter, or slice `children` prop you can rely on `React.Children.toArray` to always preserve unique keys of all the children.

**There’s a problem with `React.Children.toArray`** 🤔. Let’s look at this piece of code to understand what the problem is:

<pre data-line="32-45"><code class="language-javascript">import { Children } from 'react'

function List({children}) {
  return (
    &lt;ul&gt;
      {
        Children.toArray(
          children
        ).map((child, index) =&gt; {
          return (
            &lt;li
              key={child.key}
            &gt;
              {child}
            &lt;/li&gt;
          )
        })
      }
    &lt;/ul&gt;
  )
}

export default function App() {
  return (
    &lt;List&gt;
      &lt;a
        href="https://css-tricks.com"
        style={{padding: '0 10px'}}
      &gt;
        Google
      &lt;/a&gt;
      &lt;&gt;
        &lt;a
          href="https://smashingmagazine.com"
          style={{padding: '0 10px'}}
        &gt;
          Smashing Magazine
        &lt;/a&gt;
        &lt;a
          href="https://arihantverma.com"
          style={{padding: '0 10px'}}
        &gt;
          {"Arihant’s Website"}
        &lt;/a&gt;
      &lt;/&gt;
    &lt;/List&gt;
  )
}</code></pre>

Check the [Codesandbox demo](https://codesandbox.io/embed/sm-article-24-dqld3?fontsize=14&hidenavigation=1&theme=dark). If you see what gets rendered for the children of the fragment, you’ll see that both of the links get rendered inside one `li` tag! 😱

This is because [`React.Children.toArray`](https://github.com/facebook/react/issues/6889) [doesn’t traverse into fragments](https://github.com/facebook/react/issues/6889). So what can we do about it? Fortunately, nothing 😅 . We already have an open-sourced package called [`react-keyed-flatten-children`](https://github.com/grrowl/react-keyed-flatten-children). It’s a small function that does its magic. 

Let’s see what it does. In pseudo-code (these points are linked in the actual code below), it does this:

1. It is a function that takes `children` as its only necessary argument.
2. Iterates over `React.Children.toArray(children)` and gathers children in an accumulator array.
3. While iterating, if a child node is a string or a number, it pushes the value as is in the accumulator array.
4. If the child node is a valid React element, it clones it, gives it the appropriate key, and pushes it to the accumulator array.
5. If the child node is a fragment, then the function calls itself with fragment’s children as its argument (this is how it *traverses through a fragment*) and pushes the result of calling itself in the accumulator array.
6. While doing all this it keeps the track of the depth of traversal (of fragments), so that the children inside fragments would have correct keys, the same way as keys work with nested arrays, as we saw earlier above.

<pre><code class="language-javascript">import {
  Children,
  isValidElement,
  cloneElement
} from "react";

import { isFragment } from "react-is";

import type {
  ReactNode,
  ReactChild,
} from 'react'

/*************** 1. ***************/
export default function flattenChildren(
  // only needed argument
  children: ReactNode,
  // only used for debugging
  depth: number = 0,
  // is not required, start with default = []
  keys: (string | number)[] = [] 
): ReactChild[] {
  /*************** 2. ***************/
  return Children.toArray(children).reduce(
    (acc: ReactChild[], node, nodeIndex) =&gt; {
      if (isFragment(node)) {
        /*************** 5. ***************/
        acc.push.apply(
          acc,
          flattenChildren(
            node.props.children,
            depth + 1,
            /*************** 6. ***************/
            keys.concat(node.key || nodeIndex)
          )
        );
      } else {
        /*************** 4. ***************/
        if (isValidElement(node)) {
          acc.push(
            cloneElement(node, {
              /*************** 6. ***************/
              key: keys.concat(String(node.key)).join('.')
            })
          );
        } else if (
          /*************** 3. ***************/
          typeof node === "string"
          || typeof node === "number"
        ) {
          acc.push(node);
        }
      }
      return acc; 
    },
    /*************** Acculumator Array ***************/
    []
  );
}</code></pre>

Let’s retry our previous example to use this function and see for ourselves that it fixes our problem.

<pre data-line="1, 7-13"><code class="language-javascript">import flattenChildren from 'react-keyed-flatten-children'
import { Fragment } from 'react'

function List({children}) {
  return (
    &lt;ul&gt;
      {
        flattenChildren(
          children
        ).map((child, index) =&gt; {
          return &lt;li key={child.key}&gt;{child}&lt;/li&gt;
        })
      }
    &lt;/ul&gt;
  )
}
export default function App() {
  return (
    &lt;List&gt;
      &lt;a
        href="https://css-tricks.com"
        style={{padding: '0 10px'}}
      &gt;
        Google
      &lt;/a&gt;
      &lt;Fragment&gt;
        &lt;a
          href="https://smashingmagazine.com"
          style={{padding: '0 10px'}}&gt;
          Smashing Magazine
        &lt;/a&gt;
        
        &lt;a
          href="https://arihantverma.com"
          style={{padding: '0 10px'}}
        &gt;
          {"Arihant’s Website"}
        &lt;/a&gt;
      &lt;/Fragment&gt;
    &lt;/List&gt;
  )
}</code></pre>

And [here’s the final result](https://codesandbox.io/embed/sm-article-25-b76gn?fontsize=14&hidenavigation=1&theme=dark) (on Codesandbox)! *Woooheeee!* It works.

As an add-on, if you are new to testing &mdash; like I am at the point of this writing &mdash; you might be interested in [7 tests](https://github.com/grrowl/react-keyed-flatten-children/blob/master/index.spec.tsx) written for this utility function. It’ll be fun to read the tests to deduce the functionality of the function.

{{% ad-panel-leaderboard %}}

## The Long Term Problem With `Children` Utilities

<blockquote>“<code>React.Children</code> is a leaky abstraction, and is in maintenance mode.”<br /><br />&mdash; <a href="https://github.com/reactjs/rfcs/pull/61#issuecomment-431247764">Dan Abramov</a></blockquote>

The problem with using `Children` methods to change `children` behavior is that they only work for one level of nesting of components. If we wrap one of our `children` in another component, we lose composability. Let’s see what I mean by that, by picking up the first example that we saw &mdash; the breadcrumbs.

<pre data-line="13-18, 64-69, 86"><code class="language-javascript">import { Children, cloneElement } from "react";

function Breadcrumbs({ children }) {
  return (
    &lt;ul
      style={{
        listStyle: "none",
        display: "flex",
      }}
    &gt;
      {Children.map(children, (child, index) =&gt; {
        const isLast = index === children.length - 1;
        // if (! isLast && ! child.props.link ) {
        //   throw new Error(`
        //     BreadcrumbItem child no.
        //     ${index + 1} should be passed a 'link' prop`
        //   )
        // } 
        return (
          &lt;&gt;
            {child.props.link ? (
              &lt;a
                href={child.props.link}
                style={{
                  display: "inline-block",
                  textDecoration: "none",
                }}
              &gt;
                &lt;div style={{ marginRight: "5px" }}&gt;
                  {cloneElement(child, {
                    isLast,
                  })}
                &lt;/div&gt;
              &lt;/a&gt;
            ) : (
              &lt;div style={{ marginRight: "5px" }}&gt;
                {cloneElement(child, {
                  isLast,
                })}
              &lt;/div&gt;
            )}
            {!isLast && (
              &lt;div style={{ marginRight: "5px" }}&gt;&gt;&lt;/div&gt;
            )}
          &lt;/&gt;
        );
      })}
    &lt;/ul&gt;
  );
}

function BreadcrumbItem({ isLast, children }) {
  return (
    &lt;li
      style={{
        color: isLast ? "black" : "blue",
      }}
    &gt;
      {children}
    &lt;/li&gt;
  );

}
const BreadcrumbItemCreator = () =&gt;
  &lt;BreadcrumbItem
    link="https://smashingmagazine.com"
  &gt;
    Smashing Magazine
  &lt;/BreadcrumbItem&gt;

export default function App() {
  return (
    &lt;Breadcrumbs&gt;
      &lt;BreadcrumbItem
        link="https://goibibo.com/"
      &gt;
        Goibibo
      &lt;/BreadcrumbItem&gt;

      &lt;BreadcrumbItem
        link="https://goibibo.com/hotels/"
      &gt;
        Goibibo Hotels
      &lt;/BreadcrumbItem&gt;

      &lt;BreadcrumbItemCreator /&gt;

      &lt;BreadcrumbItem&gt;
        A Fancy Hotel Name
      &lt;/BreadcrumbItem&gt;
    &lt;/Breadcrumbs&gt;
  );
}</code></pre>

Take a look at the [Codesandbox demo](https://codesandbox.io/embed/sm-article-26-7067h?fontsize=14&hidenavigation=1&theme=dark). Although our new component `<BreadcrumbItemCreator />` rendered, our `Breadcrumb` component doesn’t have any way to extract out the `link` prop from it, because of which, it doesn’t render as link.

To fix this problem React team had come with &mdash; now defunct &mdash; experimental API called [react-call-return](https://www.npmjs.com/package/react-call-return).

[Ryan Florence’s Video](https://www.youtube.com/watch?v=60MfXWyQhRE) explains this problem in detail, and how `react-call-return` fixed it. Since the package was never published in any version of React, [there are plans to take inspiration from it and make something production-ready.](https://github.com/reactjs/rfcs/pull/61#issuecomment-584402735)

## Conclusion

To conclude, we learned about:

1. The `React.Children` utility methods. We saw two of them: `React.Children.map` to see how to use it to make compound components, and `React.Children.toArray` in depth.
2. We saw how `React.Children.toArray` converts opaque `children` prop &mdash; which could be either object, array or function &mdash; into a flat array, so that one could operate over it in required manner &mdash; sort, filter, splice, etc…
3. We learned that `React.Children.toArray` doesn’t traverse through React Fragments.
4. We learned about an open-source package called `react-keyed-flatten-children` and understood how it solves the problem.
5. We saw that `Children` utilities are in maintenance mode [because they do not compose well](https://twitter.com/0xca0a/status/1371016849664704513).

You might also be interested in reading how to use other `Children` methods to do everything you can do with `children` in Max Stoiber’s blog post [React Children Deep Dive](https://mxstbr.blog/2017/02/react-children-deepdive/).

### Resources

- [Compound components with react hooks](https://kentcdodds.com/blog/compound-components-with-react-hooks/)
- [React.Children.toArray array flattening github issue explanation](https://github.com/facebook/react/issues/6889#issuecomment-221858162)
- [React reconciliation: Recursing on children](https://reactjs.org/docs/reconciliation.html#recursing-on-children)
- [`React.Children.toArray` doesn’t traverse into fragments](https://github.com/facebook/react/issues/6889)
- [`react-keyed-flatten-children`](https://github.com/grrowl/react-keyed-flatten-children)
- [`react-keyed-flatten-children`](https://github.com/grrowl/react-keyed-flatten-children/blob/master/index.spec.tsx) [tests](https://github.com/grrowl/react-keyed-flatten-children/blob/master/index.spec.tsx)
- [react-call-return](https://www.npmjs.com/package/react-call-return)
- [Ryan Florence’s Video explaining react-call-return](https://www.youtube.com/watch?v=60MfXWyQhRE)
- [React team’s plan to replace `Children` utilities with something more composable](https://github.com/reactjs/rfcs/pull/61#issuecomment-584402735)
- [Max Stoiber’s `React Children` Deep Dive](https://mxstbr.blog/2017/02/react-children-deepdive/)
- [`React.Children` is a leaky abstraction, and is in maintenance mode](https://github.com/reactjs/rfcs/pull/61#issuecomment-431247764)

{{< signature "ks, vf, yk, il" >}}

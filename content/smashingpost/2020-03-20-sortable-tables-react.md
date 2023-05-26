---
title: 'Creating Sortable Tables With React'
slug: sortable-tables-react
author: kristofer-giltvedt-selbekk
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/996b44b1-9e4f-4489-af4d-8b6e1002af89/sortable-tables-react.png
date: 2020-03-20T12:30:00.000Z
summary: >-
  Making your tables sortable in React might sound like a daunting task, but it doesn’t have to be too difficult. In this article, we’re going to implement all you need to sort out all of your table sorting needs.
description: >-
  Making your tables sortable in React might sound like a daunting task, but it doesn’t have to be too difficult. In this article, we’re going to implement all you need to sort out all of your table sorting needs.
categories:
  - React
  - JavaScript
  - Tools
  - Techniques
---

Table sorting has always been a pretty hard issue to get right. There’s a lot of interactions to keep track of, extensive DOM mutations to do and even intricate sorting algorithms, too. It’s just one of those challenges that are hard to get right. Right?

Instead of pulling in external libraries, let’s try to make stuff ourselves. In this article, we’re going to create a reusable way to sort your tabular data in React. We’ll go through each step in detail, and learn a bunch of useful techniques along the way.

We won’t go through basic React or JavaScript syntax, but you don’t have to be an expert in React to follow along.

## Creating A Table With React

First, let’s create a sample table component. It’ll accept an array of products, and output a very basic table, listing out a row per product.

<pre><code class="language-javascript">function ProductTable(props) {
  const { products } = props;
  return (
    &lt;table&gt;
      &lt;caption&gt;Our products&lt;/caption&gt;
      &lt;thead&gt;
        &lt;tr&gt;
          &lt;th&gt;Name&lt;/th&gt;
          &lt;th&gt;Price&lt;/th&gt;
          &lt;th&gt;In Stock&lt;/th&gt;
        &lt;/tr&gt;
      &lt;/thead&gt;
      &lt;tbody&gt;
        {products.map(product =&gt; (
          &lt;tr key={product.id}&gt;
            &lt;td&gt;{product.name}&lt;/td&gt;
            &lt;td&gt;{product.price}&lt;/td&gt;
            &lt;td&gt;{product.stock}&lt;/td&gt;
          &lt;/tr&gt;
        ))}
      &lt;/tbody&gt;
    &lt;/table&gt;
  );
}</code></pre>

{{% feature-panel %}}

Here, we accept an array of products and loop them out into our table. It’s static and not sortable at the moment, but that’s fine for now.

## Sorting The Data

If you’d believe all the whiteboard interviewers, you’d think software development was almost all sorting algorithms. Luckily, we won’t be looking into a quick sort or bubble sort here.

Sorting data in JavaScript is pretty straightforward, thanks to the built-in array function [`sort()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort). It’ll sort arrays of numbers and strings without an extra argument:

<pre><code class="language-javascript">const array = ['mozzarella', 'gouda', 'cheddar'];
array.sort();
console.log(array); // ['cheddar', 'gouda', 'mozzarella']</code></pre>

If you want something a bit more clever, you can pass it a sorting function. This function is given two items in the list as arguments, and will place one in front of the other based on what you decide.

Let’s start by sorting the data we get alphabetically by name.

<pre><code class="language-javascript">function ProductTable(props) {
  const { products } = props;
  let sortedProducts = [...products];
  sortedProducts.sort((a, b) =&gt; {
    if (a.name &lt; b.name) {
      return -1;
    }
    if (a.name &gt; b.name) {
      return 1;
    }
    return 0;
  });
  return (
    &lt;Table&gt;
      {/* as before */}
    &lt;/Table&gt;
  );
}</code></pre>

So what’s going on here? First, we create a copy of the products prop, which we can alter and change as we please. We need to do this because the `Array.prototype.sort` function alters the original array instead of returning a new sorted copy.

Next, we call `sortedProducts.sort`, and pass it a `sorting` function. We check if the `name` property of the first argument `a` is before the second argument `b`, and if so, return a negative value. This indicates that `a` should come before `b` in the list. If the first argument’s name is after the second argument’s name, we return a positive number, indicating that we should place `b` before `a`. If the two are equal (i.e. both have the same name), we return `0` to preserve the order.

{{% ad-panel-leaderboard %}}

## Making Our Table Sortable

So now we can make sure the table is sorted by name &mdash; but how can we change the sorting order ourselves?

To change what field we sort by, we need to remember the currently sorted field. We’ll do that with the [`useState`](https://reactjs.org/docs/hooks-state.html) hook.

A hook is a special kind of function that lets us “hook” into some of React’s core functionality, like managing state and triggering side effects. This particular hook lets us maintain a piece of internal state in our component, and change it if we want to. This is what we’ll add:

<pre><code class="language-javascript">const [sortedField, setSortedField] = React.useState(null);</code></pre>

We start by not sorting anything at all. Next, let’s alter the table headings to include a way to change what field we want to sort by.

<div class="break-out">

<pre><code class="language-javascript">const ProductsTable = (props) =&gt; {
  const { products } = props;
  const [sortedField, setSortedField] = React.useState(null);
  return (
    &lt;table&gt;
      &lt;thead&gt;
        &lt;tr&gt;
          &lt;th&gt;
            &lt;button type="button" onClick={() =&gt; setSortedField('name')}&gt;
              Name
            &lt;/button&gt;
          &lt;/th&gt;
          &lt;th&gt;
            &lt;button type="button" onClick={() =&gt; setSortedField('price')}&gt;
              Price
            &lt;/button&gt;
          &lt;/th&gt;
          &lt;th&gt;
            &lt;button type="button" onClick={() =&gt; setSortedField('stock')}&gt;
              In Stock
            &lt;/button&gt;
          &lt;/th&gt;
        &lt;/tr&gt;
      &lt;/thead&gt;
      {/* As before */}
    &lt;/table&gt;
  );
};</code></pre>
</div>

Now, whenever we click a table heading, we update the field we want to sort by. Neat-o!

We’re not doing any actual sorting yet though, so let’s fix that. Remember the sorting algorithm from before? Here it is, just slightly altered to work with any of our field names.

<pre><code class="language-javascript">const ProductsTable = (props) =&gt; {
  const { products } = props;
  const [sortedField, setSortedField] = React.useState(null);
  let sortedProducts = [...products];
  if (sortedField !== null) {
    sortedProducts.sort((a, b) =&gt; {
      if (a[sortedField] &lt; b[sortedField]) {
        return -1;
      }
      if (a[sortedField] &gt; b[sortedField]) {
        return 1;
      }
      return 0;
    });
  }
  return (
    &lt;table&gt;</code></pre>

We first make sure we’ve chosen a field to sort by, and if so, we sort the products by that field.

## Ascending vs Descending

The next feature we want to see is a way to switch between ascending and descending order. We’ll switch between ascending and descending order by clicking the table heading one more time.

To implement this, we’ll need to introduce a second piece of state &mdash; the sort order. We’ll refactor our current `sortedField` state variable to keep both the field name and its direction. Instead of containing a string, this state variable will contain an object with a key (the field name) and a direction. We’ll rename it to `sortConfig` to be a bit clearer.

Here’s the new sorting function:

<pre><code class="language-javascript"> sortedProducts.sort((a, b) =&gt; {
  if (a[sortConfig.key] &lt; b[sortConfig.key]) {
    return sortConfig.direction === 'ascending' ? -1 : 1;
  }
  if (a[sortConfig.key] &gt; b[sortConfig.key]) {
    return sortConfig.direction === 'ascending' ? 1 : -1;
  }
  return 0;
});</code></pre>

Now, if the direction is ‘ascending’, we’ll do as we did previously. If it’s not, we’ll do the opposite, giving us descending ordering.

Next up, we’ll create a new function &mdash; `requestSort` &mdash; which will accept the field name, and update the state accordingly.

<div class="break-out">

<pre><code class="language-javascript">const requestSort = key =&gt; {
  let direction = 'ascending';
  if (sortConfig.key === key && sortConfig.direction === 'ascending') {
    direction = 'descending';
  }
  setSortConfig({ key, direction });
}</code></pre>
</div>

We’ll also have to change our click handlers to use this new function!

<div class="break-out">

<pre><code class="language-javascript">return (
  &lt;table&gt;
    &lt;thead&gt;
      &lt;tr&gt;
        &lt;th&gt;
          &lt;button type="button" onClick={() =&gt; requestSort('name')}&gt;
            Name
          &lt;/button&gt;
        &lt;/th&gt;
        &lt;th&gt;
          &lt;button type="button" onClick={() =&gt; requestSort('price')}&gt;
            Price
          &lt;/button&gt;
        &lt;/th&gt;
        &lt;th&gt;
          &lt;button type="button" onClick={() =&gt; requestSort('stock')}&gt;
            In Stock
          &lt;/button&gt;
        &lt;/th&gt;
      &lt;/tr&gt;
    &lt;/thead&gt;
  {/* as before */}
  &lt;/table&gt;
);</code></pre>
</div>

Now we’re starting to look pretty feature-complete, but there’s still one big thing left to do. We need to make sure that we only sort our data when we need to. Currently, we’re sorting all of our data on every render, which will lead to all sorts of performance issues down the line. Instead, let’s use the built-in [`useMemo`](https://reactjs.org/docs/hooks-reference.html#usememo) hook to memoize all the slow parts!

<div class="break-out">

<pre><code class="language-javascript">const ProductsTable = (props) =&gt; {
  const { products } = props;
  const [sortConfig, setSortConfig] = React.useState(null);
  
  React.useMemo(() =&gt; {
    let sortedProducts = [...products];
    if (sortedField !== null) {
      sortedProducts.sort((a, b) =&gt; {
        if (a[sortConfig.key] &lt; b[sortConfig.key]) {
          return sortConfig.direction === 'ascending' ? -1 : 1;
        }
        if (a[sortConfig.key] &gt; b[sortConfig.key]) {
          return sortConfig.direction === 'ascending' ? 1 : -1;
        }
        return 0;
      });
    }
    return sortedProducts;
  }, [products, sortConfig]);</code></pre>
</div>

If you haven’t seen it before, `useMemo` is a way to cache &mdash; or memoize &mdash; expensive computations. So given the same input, it doesn’t have to sort the products twice if we re-render our component for some reason. Note that we want to trigger a new sort whenever our products change, or the field or direction we sort by changes.

Wrapping our code in this function will have huge performance implications for our table sorting!

{{% ad-panel-leaderboard %}}

## Making It All Reusable

One of the best things about hooks is how easy it is to make logic reusable. You’ll probably be sorting all types of tables throughout your application, and having to reimplement the same stuff all over again sounds like a drag.

React has this feature called [custom hooks](https://reactjs.org/docs/hooks-custom.html). They sound fancy, but all they are are regular functions that use other hooks inside of them. Let’s refactor our code to be contained in a custom hook, so we can use it all over the place!

<div class="break-out">

<pre><code class="language-javascript">const useSortableData = (items, config = null) =&gt; {
  const [sortConfig, setSortConfig] = React.useState(config);
  
  const sortedItems = React.useMemo(() =&gt; {
    let sortableItems = [...items];
    if (sortConfig !== null) {
      sortableItems.sort((a, b) =&gt; {
        if (a[sortConfig.key] &lt; b[sortConfig.key]) {
          return sortConfig.direction === 'ascending' ? -1 : 1;
        }
        if (a[sortConfig.key] &gt; b[sortConfig.key]) {
          return sortConfig.direction === 'ascending' ? 1 : -1;
        }
        return 0;
      });
    }
    return sortableItems;
  }, [items, sortConfig]);

  const requestSort = key =&gt; {
    let direction = 'ascending';
    if (sortConfig && sortConfig.key === key && sortConfig.direction === 'ascending') {
      direction = 'descending';
    }
    setSortConfig({ key, direction });
  }

  return { items: sortedItems, requestSort };
}</code></pre>
</div>

This is pretty much copy and paste from our previous code, with a bit of renaming thrown in. `useSortableData` accepts the items, and an optional initial sort state. It returns an object with the sorted items, and a function to re-sort the items.

Our table code now looks like this:

<pre><code class="language-javascript">const ProductsTable = (props) =&gt; {
  const { products } = props;
  const { items, requestSort } = useSortableData(products);
  return (
    &lt;table&gt;{/* ... */}&lt;/table&gt;
  );
};</code></pre>

## A Last Touch

There’s one tiny piece missing &mdash; a way to indicate how the table is sorted. In order to indicate that in our design, we need to return the internal state as well &mdash; the `sortConfig`. Let’s return that as well, and use it to generate styles we can apply to our table headings!

<div class="break-out">

<pre><code class="language-javascript">const ProductTable = (props) =&gt; {
  const { items, requestSort, sortConfig } = useSortableData(props.products);
  const getClassNamesFor = (name) =&gt; {
    if (!sortConfig) {
      return;
    }
    return sortConfig.key === name ? sortConfig.direction : undefined;
  };
  return (
    &lt;table>
      &lt;caption&gt;Products&lt;/caption&gt;
      &lt;thead&gt;
        &lt;tr&gt;
          &lt;th&gt;
            &lt;button
              type="button"
              onClick={() =&gt; requestSort('name')}
              className={getClassNamesFor('name')}
            &gt;
              Name
            &lt;/button&gt;
          &lt;/th&gt;
         {/* … */}
        &lt;/tr&gt;
      &lt;/thead&gt;
      {/* … */}
    &lt;/table&gt;
  );
};</code></pre>
</div>

And with that, we’re done!

## Wrapping Up

As it turns out, creating your own table sorting algorithm wasn’t an impossible feat after all. We found a way to model our state, we wrote a generic sorting function, and we wrote a way to update what our sorting preferences are. We made sure everything was performant and refactored it all into a custom hook. Finally, we provided a way to indicate the sort order to the user.

You can see a demo of the table in this [CodeSandbox](https://codesandbox.io/embed/table-sorting-example-ur2z9?fontsize=14&hidenavigation=1&theme=dark):

<iframe
     src="https://codesandbox.io/embed/table-sorting-example-ur2z9?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Table sorting example"
     allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media; usb"
     sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"
   ></iframe>

{{< signature "ra, yk, il" >}}

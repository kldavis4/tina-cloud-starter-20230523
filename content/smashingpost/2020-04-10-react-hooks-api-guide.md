---
title: 'Getting Started With The React Hooks API'
slug: react-hooks-api-guide
author: shedrack-akintayo
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/7fdca25d-1080-4d2c-b0f6-50fc5a827ed5/react-hooks-api-guide.png
date: 2020-04-10T09:30:00.000Z
summary: >-
  In this tutorial, you are going to learn and understand what React hooks are, the basic React Hooks that are available and also examples of how to write them for your React applications. In the process, you will also get to know about some additional hooks that were shipped with React 16.8 and also how to write your own custom React Hooks.
description: >-
  This tutorial shares examples of how to use React Hooks for your applications. In the process, you will also get to know about some additional hooks that were shipped with React 16.8 and also how to write your own custom React Hooks.
categories:
  - API
  - React
  - React Hooks
  - Guides
---

When React 16.8 was released officially in early February 2019, it shipped with an additional API that lets you use state and other features in React without writing a class. This additional API is called **Hooks** and they’re becoming popular in the React ecosystem, from open-sourced projects to being used in production applications.

React Hooks are completely opt-in which means that rewriting existing code is unecessary, they do not contain any breaking changes, and they’re available for use with the release of React 16.8. Some curious developers have been making use of the Hooks API even before it was released officially, but back then it was not stable and was only an experimental feature. Now it is stable and recommended for React developers to use.

**Note**: *We won’t be talking about React or JavaScript in general. A good knowledge of ReactJS and JavaScript will come in handy as you work through this tutorial.*

## What Are React Hooks?

React Hooks are in-built functions that allow React developers to use state and lifecycle methods inside functional components, they also work together with existing code, so they can easily be adopted into a codebase. The way Hooks were pitched to the public was that they allow developers to use state in functional components but under the hood, Hooks are much more powerful than that. They allow React Developers to enjoy the following benefits:

- Improved code reuse;
- Better code composition;
- Better defaults;
- Sharing non-visual logic with the use of custom hooks; 
- Flexibility in moving up and down the `components` tree.

With React Hooks, developers get the power to use functional components for almost everything they need to do from just rendering UI to also handling state and also logic &mdash; which is pretty neat.

## Motivation Behind The Release Of React Hooks

According to the [ReactJS official documentation](https://reactjs.org/docs/hooks-intro.html), the following are the motivation behind the release of React Hooks:

- **Reusing stateful logic between components is difficult.**  
With Hooks, you can reuse logic between your components without changing their architecture or structure.
- **Complex components can be difficult to understand.**  
When components become larger and carry out many operations, it becomes difficult to understand in the long run. Hooks solve this by allowing you separate a particular single component into various smaller functions based upon what pieces of this separated component are related (such as setting up a subscription or fetching data), rather than having to force a split based on lifecycle methods. 
- **Classes are quite confusing.**  
Classes are a hindrance to learning React properly; you would need to understand how `this` in JavaScript works which differs from other languages. React Hooks solves this problem by allowing developers to use the best of React features without having to use classes.

{{% feature-panel %}}

## The Rules Of Hooks

There are two main rules that are strictly to be adhered to as stated by the React core team in which they outlined in the [hooks proposal documentation](https://reactjs.org/docs/hooks-rules.html).

- Make sure to not use Hooks inside loops, conditions, or nested functions;
- Only use Hooks from inside React Functions.

## Basic React Hooks

There are 10 in-built hooks that was shipped with React 16.8 but the basic (commonly used) hooks include:

<ul>
  <li><a href="#useState"><code>useState()</code></a></li>
  <li><a href="#useEffect"><code>useEffect()</code></a></li>
  <li><a href="#useContext"><code>useContext()</code></a></li>
  <li><a href="#useReducer"><code>useReducer()</code></a></li>
</ul>

These are the 4 basic hooks that are commonly used by React developers that have adopted React Hooks into their codebases.

### <code>useState()</code>

The `useState()` hook allows React developers to update, handle and manipulate state inside functional components without needing to convert it to a class component. Let’s use the code snippet below is a simple Age counter component and we will use it to explain the power and syntax of the `useState()` hook.

<div class="break-out">

<pre><code class="language-javascript">function App() {
  const [age, setAge] = useState(19);
  const handleClick = () =&gt; setAge(age + 1)

  return 
      &lt;div> 
          I am {age} Years Old 
        &lt;div&gt; 
        &lt;button onClick={handleClick}&gt;Increase my age! &lt;/button&gt;
      &lt;/div&gt;
   &lt;/div&gt;
}
</code></pre>
</div>

If you’ve noticed, our component looks pretty simple, concise and it’s now a functional component and also does not have the level of complexity that a class component would have.

The `useState()` hook receives an initial state as an argument and then returns, by making use of array destructuring in JavaScript, the two variables in the array can be named what. The first variable is the actual state, while the second variable is a function that is meant for updating the state by providing a new state.

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec6c1643-97e5-405a-b39d-c1bcc56bcac8/01-use-state-project.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/345c665e-86b5-44d3-8372-9389da157f86/01-use-state-project-800w.gif" width="800" height="" alt="" /></a><figcaption>Our finished React app (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ec6c1643-97e5-405a-b39d-c1bcc56bcac8/01-use-state-project.gif">Large preview</a>)</figcaption></figure>

This is how our component should look when it is rendered in our React application. By clicking on the “Increase my Age” button, the state of the age will change and the component would work just like a class component with state.

### <code>useEffect()</code>

The `useEffect()` hook accepts a function that would contain effectual code. In functional components, effects like mutations, subscriptions, timers, logging, and other effects are not allowed to be placed inside a functional component because doing so would lead to a lot of inconsistencies when the UI is rendered and also confusing bugs. 

In using the  `useEffect()` hook, the effectual function passed into it will execute right after the render has been displayed on the screen. Effects are basically peeked into the imperative way of building UIs that is quite different from React’s functional way.

By default, effects are executed mainly after the render has been completed, but you have the option to also fire them when certain values change.

The `useEffect()` hook mostly into play for side-effects that are usually used for interactions with the Browser/DOM API or external API-like data fetching or subscriptions. Also, if you are already familiar with how React lifecycle methods work, you can also think of `useEffect()` hook as **component mounting**, **updating** and **unmounting** &mdash; all combined in one function. It lets us replicate the lifecycle methods in functional components.

We will use the code snippets below to explain the most basic way that we can by using the `useEffect()` hook.

{{% ad-panel-leaderboard %}}

#### Step 1: Define The State Of Your Application

<div class="break-out">

<pre><code class="language-javascript">import React, {useState} from 'react';
function App() {
    //Define State
    const [name, setName] = useState({firstName: 'name', surname: 'surname'});
    const [title, setTitle] = useState('BIO');
    
    return(
        &lt;div&gt;
            &lt;h1&gt;Title: {title}&lt;/h1&gt;
            &lt;h3&gt;Name: {name.firstName}&lt;/h3&gt;
            &lt;h3&gt;Surname: {name.surname}&lt;/h3&gt;
        &lt;/div&gt;
    );
};
export default App
</code></pre>
</div>

Just like we discussed in the previous section on how to use the `useState()` hook to handle state inside functional components, we used it in our code snippet to set the state for our app that renders my full name. 
 
#### Step 2: Call The useEffect Hook
 
<div class="break-out">

<pre><code class="language-javascript">
import React, {useState, useEffect} from 'react';
function App() {
    //Define State
    const [name, setName] = useState({firstName: 'name', surname: 'surname'});
    const [title, setTitle] = useState('BIO');
   
    //Call the use effect hook
    useEffect(() =&gt; {
      setName({FirstName: 'Shedrack', surname: 'Akintayo'})
    }, [])//pass in an empty array as a second argument
    
    return(
        &lt;div&gt;
            &lt;h1&gt;Title: {title}&lt;/h1&gt;
            &lt;h3&gt;Name: {name.firstName}&lt;/h3&gt;
            &lt;h3&gt;Surname: {name.surname}&lt;/h3&gt;
        &lt;/div&gt;
    );
};
export default App
</code></pre>
</div>

We have now imported the `useEffect` hook and also made use of the `useEffect()` function to set the state of our the name and surname property which is pretty neat and concise. 

You may have noticed the `useEffect` hook in the second argument which is an empty array; this is because it contains a call to the `setFullName` which does not have a list of dependencies. Passing the second argument will prevent an infinite chain of updates (`componentDidUpdate()`) and it’ll also allow our `useEffect()` hook to act as a `componentDidMount` lifecycle method and render once without re-rendering on every change in the tree.

Our React app should now look like this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af586a2d-ddad-4083-b931-027cd802b8c4/02-use-effect-project.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af586a2d-ddad-4083-b931-027cd802b8c4/02-use-effect-project.png" sizes="100vw" caption="React app using the <code>useEffect</code> Hook (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/af586a2d-ddad-4083-b931-027cd802b8c4/02-use-effect-project.png'>Large preview</a>)" alt="" >}}

We can also use change the `title` property of our application inside the `useEffect()` function by calling the `setTitle()` function, like so:

<div class="break-out">

<pre><code class="language-javascript">import React, {useState, useEffect} from 'react';
function App() {
    //Define State
    const [name, setName] = useState({firstName: 'name', surname: 'surname'});
    const [title, setTitle] = useState('BIO');
   
    //Call the use effect hook
    useEffect(() =&gt; {
      setName({firstName: 'Shedrack', surname: 'Akintayo'})
      setTitle({'My Full Name'}) //Set Title
    }, [])// pass in an empty array as a second argument
    
    return(
        &lt;div&gt;
            &lt;h1&gt;Title: {title}&lt;/h1&gt;
            &lt;h3&gt;Name: {name.firstName}&lt;/h3&gt;
            &lt;h3&gt;Surname: {name.surname}&lt;/h3&gt;
        &lt;/div&gt;
    );
};
export default App
</code></pre>
</div>

Now after our application has rerendered, it now shows the new title.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d4690d1-2fa3-4197-b401-a4ea26d1ca03/03-use-effect-project-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d4690d1-2fa3-4197-b401-a4ea26d1ca03/03-use-effect-project-2.png" sizes="100vw" caption="Our finished project (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0d4690d1-2fa3-4197-b401-a4ea26d1ca03/03-use-effect-project-2.png'>Large preview</a>)" alt="" >}}

### <code>useContext()</code>

The `useContext()` hook accepts a context object, i.e the value that is returned from `React.createContext`, and then it returns the current context value for that context. 

This hook gives functional components easy access to your React app context. Before the `useContext` hook was introduced you would need to set up a `contextType` or a `<Consumer>` to access your global state passed down from some provider in a class component. 

Basically, the `useContext` hook works with the React Context API which is a way to share data deeply throughout your app without the need to manually pass your app props down through various levels. Now, the `useContext()` makes using Context a little easier.

The code snippets below will show how the Context API works and how the `useContext` Hook makes it better.

#### The Normal Way To Use The Context API

<div class="break-out">

<pre><code class="language-javascript">import React from "react";
import ReactDOM from "react-dom";

const NumberContext = React.createContext();
function App() {
  return (
    &lt;NumberContext.Provider value={45}&gt;
      &lt;div&gt;
        &lt;Display /&gt;
      &lt;/div&gt;
    &lt;/NumberContext.Provider&gt;
  );
}
function Display() {
  return (
    &lt;NumberContext.Consumer&gt;
      {value =&gt; &lt;div&gt;The answer to the question is {value}.&lt;/div&gt;}
    &lt;/NumberContext.Consumer&gt;
  );
}
ReactDOM.render(&lt;App /&gt;, document.querySelector("#root"));
</code></pre>
</div>

Let’s now break down the code snippet and explain each concept.

Below, we are creating a context called `NumberContext`. It is meant to return an object with two values: `{ Provider, Consumer }`.

<pre><code class="language-javascript">const NumberContext = React.createContext();</code></pre>

Then we use the `Provider` value that was returned from the `NumberContext` we created to make a particular value available to all the children.

<pre><code class="language-javascript">function App() {
  return (
    &lt;NumberContext.Provider value={45}&gt;
      &lt;div&gt;
        &lt;Display /&gt;
      &lt;/div&gt;
    &lt;/NumberContext.Provider&gt;
  );
}</code></pre>

With that, we can use the `Consumer` value that was returned from the `NumberContext` we created to get the value we made available to all children. If you have noticed, this component did not get any props.

<div class="break-out">

<pre><code class="language-javascript">function Display() {
  return (
    &lt;NumberContext.Consumer&gt;
      {value =&gt; &lt;div&gt;The answer to the question is {value}.&lt;/div&gt;}
    &lt;/NumberContext.Consumer&gt;
  );
}
ReactDOM.render(&lt;App /&gt;, document.querySelector("#root"));

</code></pre>
</div>

Note how we were able to get the value from the `App` component into the `Display` component by wrapping our content in a `NumberContext.Consumer` and using the render props method to retrieve the value and render it.

Everything works well and the render props method we used is a really good pattern for handling dynamic data, but in the long run, it does introduce some unnecessary nesting and confusion if you’re not used to it.

#### Using The useContext Method

To explain the `useContext` method we will rewrite the `Display` component using the useContext hook.

<pre><code class="language-javascript">// import useContext (or we could write React.useContext)
import React, { useContext } from 'react';

// old code goes here

function Display() {
  const value = useContext(NumberContext);
  return &lt;div&gt;The answer is {value}.&lt;/div&gt;;
}</code></pre>

That’s all we need to do in order to display our value. Pretty neat, right? You call the `useContext()` hook and pass in the context object we created and we grab the value from it.

**Note:** *Don’t forget that the argument that is passed to the useContext hook must be the context object itself and any component calling the useContext will always re-render when the context value changes.*

{{% ad-panel-leaderboard %}}

### <code>useReducer()</code>

The `useReducer` hook is used for handling complex states and transitions in state. It takes in a `reducer` function and also an initial state input; then, it returns the current state and also a `dispatch` function as output by the means of array destructuring.

The code below is the proper syntax for using the `useReducer` hook.

<div class="break-out">

<pre><code class="language-javascript">const [state, dispatch] = useReducer(reducer, initialArg, init);
</code></pre>
</div>

It is sort of an alternative to the `useState` hook; it is usually preferable to `useState` when you have complex state logic that has to do with multiple sub-values or when the next state is dependent on the previous one.

## Other React Hooks Available

<table class="tablesaw table--no-stripe break-out table-saw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td><code>useCallback</code></td>
      <td>This hook returns a callback function that is memoized and that only changes if one dependency in the dependency tree changes.</td>
    </tr>
    <tr>
      <td><code>useMemo</code></td>
      <td>This hook returns a memoized value, you can pass in a “create” function and also an array of dependencies. The value it returns will only use the memoized value again if one of the dependencies in the dependency tree changes.</td>
    </tr>
    <tr>
      <td><code>useRef</code></td>
      <td>This hook returns a mutable ref object whose <code>.current</code> property is initialized to the passed argument (<code>initialValue</code>). The returned object will be available for the full lifetime of the component.</td>
    </tr>
    <tr>
      <td><code>useImperativeHandle</code></td>
      <td>This hook is used for customizing the instance value that is made available for parent components when using refs in React.</td>
    </tr>
    <tr>
      <td><code>useLayoutEffect</code></td>
      <td>This hook similar to the <code>useEffect</code> hook, however, it fires synchronously after all DOM mutations. It also renders in the same way as <code>componentDidUpdate</code> and <code>componentDidMount</code>.</td>
    </tr>
    <tr>
      <td><code>useDebugValue</code></td>
      <td>This hook can be used to display a label for custom hooks in the React Dev Tools. It is very useful for debugging with the React Dev Tools.</td>
    </tr>
  </tbody>
</table>

## Custom React Hooks

A “custom Hook” is a JavaScript function whose names are prefixed with the word `use` and can be used to call other Hooks. It also lets you to extract component logic into reusable functions; they are normal JavaScript functions that can make use of other Hooks inside of it, and also contain a common stateful logic that can be made use of within multiple components.

The code snippets below demonstrate an example of a custom React Hook for implementing infinite scroll (by [Paulo Levy](https://github.com/pflevy)):

<div class="break-out">

<pre><code class="language-javascript">import { useState } from "react";

export const useInfiniteScroll = (start = 30, pace = 10) =&gt; {
  const [limit, setLimit] = useState(start);
  window.onscroll = () =&gt; {
    if (
      window.innerHeight + document.documentElement.scrollTop ===
      document.documentElement.offsetHeight
    ) {
      setLimit(limit + pace);
    }
  };
  return limit;
};
</code></pre>
</div>

This custom Hook accepts two arguments which are `start` and `pace`. The start argument is the starting number of elements to be rendered while the pace argument is the subsequent number of elements that are to be rendered. By default, the `start` and `pace` arguments are set to `30` and `10` respectively which means you can actually call the Hook without any arguments and those default values will be used instead.

So in order to use this Hook within a React app, we would use it with an online API that returns ‘fake’ data:

<div class="break-out">

<pre><code class="language-javascript">import React, { useState, useEffect } from "react";
import { useInfiniteScroll } from "./useInfiniteScroll";

const App = () =&gt; {
  let infiniteScroll = useInfiniteScroll();

  const [tableContent, setTableContent] = useState([]);

  useEffect(() =&gt; {
    fetch("https://jsonplaceholder.typicode.com/todos/")
      .then(response =&gt; response.json())
      .then(json =&gt; setTableContent(json));
  }, []);

  return (
    &lt;div style={{ textAlign: "center" }}&gt;
      &lt;table&gt;
        &lt;thead&gt;
          &lt;tr&gt;
            &lt;th&gt;User ID&lt;/th&gt;
            &lt;th&gt;Title&lt;/th&gt;
          &lt;/tr&gt;
        &lt;/thead&gt;
        &lt;tbody&gt;
          {tableContent.slice(0, infiniteScroll).map(content =&gt; {
            return (
              &lt;tr key={content.id}&gt;
                &lt;td style={{ paddingTop: "10px" }}&gt;{content.userId}&lt;/td&gt;
                &lt;td style={{ paddingTop: "10px" }}&gt;{content.title}&lt;/td&gt;
              &lt;/tr&gt;
            );
          })}
        &lt;/tbody&gt;
      &lt;/table&gt;
    &lt;/div&gt;
  );
};

export default App;
</code></pre>
</div>

The code above will render a list of fake data (`userID` and `title`) that make use of the infinite scroll hook to display the initial number of data on the screen.

## Conclusion

I hope you enjoyed working through this tutorial. You could always read more on React Hooks from the references below. 

If you have any questions, you can leave them in the comments section and I’ll be happy to answer every single one!

*The supporting repo for this article is [available on Github](https://github.com/hacktivist123/React-Hooks-Project).*

### Resources And Further Reading

- “[Hooks API Reference](https://reactjs.org/docs/hooks-reference.htm),” React.js Docs
- “[What Are React Hooks?](https://www.robinwieruch.de/react-hooks/),” Robin Wieruch 
- “[How The `useContext` Hook Works](https://daveceddia.com/usecontext-hook/),” Dave Ceddia
- “[React Hooks: How To Use `useEffect()`](https://medium.com/javascript-in-plain-english/react-hooks-how-to-use-useeffect-ecea3e90d84f),” Hossein Ahmadi, Medium
- “[Writing Your Own Custom React Hooks](https://blog.bitsrc.io/writing-your-own-custom-hooks-4fbcf77e112e),” Aayush Jaiswal, Medium
- “[Easy To Understand React Hook Recipes](https://usehooks.com),” Gabe Ragland, useHooks(🐠)

{{< signature "ks, ra, yk, il" >}}

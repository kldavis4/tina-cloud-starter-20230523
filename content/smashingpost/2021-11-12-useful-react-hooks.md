---
title: 'Useful React Hooks That You Can Use In Your Projects'
slug: useful-react-hooks
author: ifeanyi-dike
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ad5f8d5b-6da6-4441-a6f7-466c79e7fb0d/useful-react-hooks.jpg
date: 2021-11-12T10:00:00.000Z
summary: >-
  React class-based components are messy, confusing, hard for humans and machines. But before React 16.8, class-based components were mandatory for any projects that require states, life-cycle methods, and many other important functionalities. All these changed with the introduction of hooks in React 16.8. Hooks are game-changers. They have simplified React, made it neater, easier to write and debug, and also reduced the learning curve.
description: >-
  The React team introduced several hooks in React 16.8 which you can use from third-party providers in your application, or even create your own custom hook. In this tutorial, we’ll take a look at some of the most useful hooks in React and how to use them.
categories:
  - React
  - Tools
  - Tutorials
  - JavaScript
---

Hooks are simply functions that allow you to **hook into** or **make use of** React features. They were introduced at the [React Conf 2018](https://www.youtube.com/watch?v=dpw9EHDh2bM) to address three major problems of class components: wrapper hell, huge components, and confusing classes. Hooks give power to React functional components, making it possible to develop an entire application with it.

The aforementioned problems of class components are connected and solving one without the other could introduce further problems. Thankfully, hooks solved all the problems simply and efficiently while creating room for more interesting features in React. Hooks do not replace already existing React concepts and classes, they merely provide an API to access them directly.

The React team introduced several hooks in React 16.8. However, you could also use hooks from third-party providers in your application or even create a custom hook. In this tutorial, we’ll take a look at some useful hooks in React and how to use them. We’ll go through several code examples of each hook and also explore how you’d create a custom hook.

**Note:** *This tutorial requires a basic understanding of Javascript (ES6+) and React.*
 
{{% feature-panel %}}

## Motivation Behind Hooks

As stated earlier, hooks were created to solve three problems: wrapper hell, huge components, and confusing classes. Let’s take a look at each of these in more detail.

### Wrapper Hell

Complex applications built with class components easily run into wrapper hell. If you examine the application in the React Dev Tools, you will notice deeply nested components. This makes it very difficult to work with the components or debug them. While these problems could be solved with **higher-order components** and **render props**, they require you to modify your code a bit. This could lead to confusion in a complex application. 

Hooks are easy to share, you don’t have to modify your components before reusing the logic.

A good example of this is the use of the Redux `connect` Higher Order Component (HOC) to subscribe to the Redux store. Like all HOCs, to use the connect HOC, you have to export the component alongside the defined higher-order functions. In the case of `connect`, we’ll have something of this form.

<pre><code class="language-javascript">export default connect(mapStateToProps, mapDispatchToProps)(MyComponent)</code></pre>

Where `mapStateToProps` and `mapDispatchToProps` are functions to be defined. 

Whereas in the Hooks era, one can easily achieve the same result neatly and succinctly by using the Redux `useSelector` and `useDispatch` hooks.

### Huge Components

Class components usually contain side effects and stateful logic. As the application grows in complexity, it is common for the component to become messy and confusing. This is because the side effects are expected to be organized by **lifecycle methods** rather than functionality. While it is possible to split the components and make them simpler, this often introduces a higher level of abstraction.

Hooks organize side effects by functionality and it is possible to split a component into pieces based on the functionality.

### Confusing Classes

Classes are generally a more difficult concept than functions. React class-based components are verbose and a bit difficult for beginners. If you are new to Javascript, you could find functions easier to get started with because of their lightweight syntax as compared to classes. The syntax could be confusing; sometimes, it is possible to forget binding an event handler which could break the code.

React solves this problem with functional components and hooks, allowing developers to focus on the project rather than code syntax.

For instance, the following two React components will yield exactly the same result.

<pre><code class="language-javascript">import React, { Component } from "react";
export default class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      num: 0
    };
    this.incrementNumber = this.incrementNumber.bind(this);
  }
  incrementNumber() {
    this.setState({ num: this.state.num + 1 });
  }
  render() {
    return (
      &lt;div&gt;
        &lt;h1&gt;{this.state.num}&lt;/h1&gt;
        &lt;button onClick={this.incrementNumber}&gt;Increment&lt;/button&gt;
      &lt;/div&gt;
    );
  }
}</code></pre>
   

<pre><code class="language-javascript">import React, { useState } from "react";
export default function App() {
  const [num, setNum] = useState(0);
  function incrementNumber() {
    setNum(num + 1);
  }
  return (
    &lt;div&gt;
      &lt;h1&gt;{num}&lt;/h1&gt;
      &lt;button onClick={incrementNumber}&gt;Increment&lt;/button&gt;
    &lt;/div&gt;
  );
}</code></pre>

The first example is a class-based component while the second is a functional component. Although this is a simple example, notice how bogus the first example is compared to the second.

## The Hooks Convention And Rules

Before delving into the various hooks, it could be helpful to take a look at the convention and rules that apply to them. Here are some of the rules that apply to hooks.

1. The naming convention of hooks should start with the prefix `use`. So, we can have `useState`, `useEffect`, etc. If you are using modern code editors like Atom and VSCode, the ESLint plugin could be a very useful feature for React hooks. The plugin provides useful warnings and hints on the best practices.
2. Hooks must be called at the top level of a component, before the return statement. They can't be called inside a conditional statement, loop, or nested functions.
3. Hooks must be called from a React function (inside a React component or another hook). It shouldn’t be called from a Vanilla JS function.

## The `useState` Hook

The `useState` hook is the most basic and useful React hook. Like other built-in hooks, this hook must be imported from `react` to be used in our application.

<pre><code class="language-javascript">import {useState} from 'react'</code></pre>

To initialize the state, we must declare both the state and its updater function and pass an initial value.

<pre><code class="language-javascript">const [state, updaterFn] = useState('')</code></pre>

We are free to call our state and updater function whatever we want but by convention, the first element of the array will be our state while the second element will be the updater function. It is a common practice to prefix our updater function with the prefix **set** followed by the name of our state in camel case form.

For instance, let’s set a state to hold count values.

<pre><code class="language-javascript">const [count, setCount] = useState(0)</code></pre>

Notice that the initial value of our `count` state is set to `0` and not an empty string. In other words, we can initialize our state to any kind of JavaScript variables, namely number, string, boolean, array, object, and even BigInt. There is a clear difference between setting states with the `useState` hook and class-based component states. It is noteworthy that the `useState` hook returns an array, also known as state variables and in the example above, we destructured the array into `state` and the `updater` function.

### Rerendering Components

Setting states with the `useState` hook causes the corresponding component to rerender. However, this only happens if React detects a difference between the previous or old state and the new state. React does the state comparison using the Javascript `Object.is` [algorithm](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is#description). 

### Setting States With `useState`

Our `count` state can be set to new state values by simply passing the new value to the `setCount` updater function as follows `setCount(newValue)`. 

This method works when we don't want to reference the previous state value. If we wish to do that, we need to pass a function to the `setCount` function.

Assuming we want to add 5 to our `count` variable anytime a button is clicked, we could do the following.

<pre><code class="language-javascript">import {useState} from 'react'

const CountExample = () =&gt; {
  // initialize our count state
  const [count, setCount] = useState(0)
  
  // add 5 to to the count previous state
  const handleClick = () =&gt;{
    setCount(prevCount =&gt; prevCount + 5)
  } 
  return(
    &lt;div&gt;
      &lt;h1&gt;{count} &lt;/h1&gt;
      &lt;button onClick={handleClick}&gt;Add Five&lt;/button&gt;
    &lt;/div&gt;
  )
}

export default CountExample</code></pre>

In the code above, we first imported the `useState` hook from `react` and then initialized the `count` state with a default value of 0. We created an `onClick` handler to increment the value of `count` by 5 whenever the button is clicked. Then we displayed the result in an `h1` tag.

### Setting Arrays And Object States

States for arrays and objects can be set in much the same way as other data types. However, if we wish to retain already existing values, we need to use the ES6 spread operator when setting states.

The spread operator in Javascript is used to create a new object from an already existing object. This is useful here because `React` compares the states with the `Object.is` operation and then rerender accordingly.

Let’s consider the code below for setting states on button click.

<pre><code class="language-javascript">import {useState} from 'react'

const StateExample = () =&gt; {
  //initialize our array and object states
  const [arr, setArr] = useState([2, 4])
  const [obj, setObj] = useState({num: 1, name: 'Desmond'})
  
  // set arr to the new array values
  const handleArrClick = () =&gt;{
    const newArr = [1, 5, 7]
    setArr([...arr, ...newArr])
  } 
  
  // set obj to the new object values
  const handleObjClick = () =&gt;{
    const newObj = {name: 'Ifeanyi', age: 25}
    setObj({...obj, ...newObj})
  } 

  return(
    &lt;div&gt;
      &lt;button onClick ={handleArrClick}&gt;Set Array State&lt;/button&gt;
      &lt;button onClick ={handleObjClick}&gt;Set Object State&lt;/button&gt;
    &lt;/div&gt;
  )
}

export default StateExample</code></pre>

In the above code, we created two states `arr` and `obj`, and initialized them to some array and object values respectively. We then created `onClick` handlers called `handleArrClick` and `handleObjClick` to set the states of the array and object respectively. When `handleArrClick` fires, we call `setArr` and use the ES6 spread operator to spread already existing array values and add `newArr` to it.

We did the same thing for `handleObjClick` handler. Here we called `setObj`, spread the existing object values using the ES6 spread operator, and updated the values of `name` and `age`.

### Async Nature Of `useState`

As we have already seen, we set states with `useState` by passing a new value to the updater function. If the updater is called multiple times, the new values will be added to a queue and re-rendering is done accordingly using the JavaScript `Object.is` comparison.

The states are updated asynchronously. This means that the new state is first added to a pending state and thereafter, the state is updated. So, you may still get the old state value if you access the state immediately it is set.

Let’s consider the following example to observe this behavior.

<iframe src="https://codesandbox.io/embed/vibrant-bogdan-49hl4?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="vibrant-bogdan-49hl4"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

In the code above, we created a `count` state using the `useState` hook. We then created an `onClick` handler to increment the `count` state whenever the button is clicked.
Observe that although the `count` state increased, as displayed in the `h2` tag, the previous state is still logged in the console. This is due to the async nature of the hook.

If we wish to get the new state, we can handle it in a similar way we would handle async functions. Here is one way to do that.

<iframe src="https://codesandbox.io/embed/dazzling-haze-ukzrs?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="dazzling-haze-ukzrs"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

Here, we stored created `newCountValue` to store the updated count value and then set the `count` state with the updated value. Then, we logged the updated count value in the console.

{{% ad-panel-leaderboard %}}

## The `useEffect` Hook

`useEffect` is another important React hook used in most projects. It does a similar thing to the class-based component’s `componentDidMount`, `componentWillUnmount`, and `componentDidUpdate` lifecycle methods. `useEffect` provides us an opportunity to write imperative codes that may have side effects on the application. Examples of such effects include logging, subscriptions, mutations, etc.

The user can decide when the `useEffect` will run, however, if it is not set, the side effects will run on every rendering or rerendering.

Consider the example below.

<pre><code class="language-javascript">import {useState, useEffect} from 'react'

const App = () =&gt;{
  const [count, setCount] = useState(0)
  useEffect(() =&gt;{
    console.log(count)
  })

  return(
    &lt;div&gt;
      ...
    &lt;/div&gt;
  )
}</code></pre>

In the code above, we simply logged `count` in the `useEffect`. This will run after every render of the component.

Sometimes, we may want to run the hook once (on the mount) in our component. We can achieve this by providing a second parameter to `useEffect` hook.

<pre><code class="language-javascript">import {useState, useEffect} from 'react'

const App = () =&gt;{
  const [count, setCount] = useState(0)
  useEffect(() =&gt;{
    setCount(count + 1)
  }, [])

  return(
    &lt;div&gt;
      &lt;h1&gt;{count}&lt;/h1&gt;
      ...
    &lt;/div&gt;
  )
}</code></pre>

The `useEffect` hook has two parameters, the first parameter is the function we want to run while the second parameter is an array of dependencies. If the second parameter is not provided, the hook will run continuously.

By passing an empty square bracket to the hook’s second parameter, we instruct React to run the `useEffect` hook only once, on the mount. This will display the value `1` in the `h1` tag because the count will be updated once, from 0 to 1, when the component mounts.

We could also make our side effect run whenever some dependent values change. This can be done by passing these values in the list of dependencies.

For instance, we could make the `useEffect` to run whenever `count` changes as follows.

<pre><code class="language-javascript">import { useState, useEffect } from "react";
const App = () =&gt; {
  const [count, setCount] = useState(0);
  useEffect(() =&gt; {
    console.log(count);
  }, [count]);
  return (
    &lt;div&gt;
      &lt;button onClick={() =&gt; setCount(count + 1)}&gt;Increment&lt;/button&gt;
    &lt;/div&gt;
  );
};
export default App;</code></pre>

The `useEffect` above will run when either of these two conditions is met.

1. On mount &mdash; after the component is rendered. 
2. When the value of `count` changes.

On mount, the `console.log` expression will run and log `count` to 0. Once the `count` is updated, the second condition is met, so the `useEffect` runs again, this will continue whenever the button is clicked.

Once we provide the second argument to `useEffect`, it is expected that we pass all the dependencies to it. If you have `ESLINT` installed, it will show a lint error if any dependency is not passed to the parameter list. This could also make the side effect behave unexpectedly, especially if it depends on the parameters that are not passed.

### Cleaning Up The Effect

`useEffect` also allows us to clean up resources before the component unmounts. This may be necessary to prevent memory leaks and make the application more efficient. To do this, we’d return the clean-up function at the end of the hook.

<pre><code class="language-javascript">useEffect(() =&gt; {
  console.log('mounted')

  return () =&gt; console.log('unmounting... clean up here')
})</code></pre>

The `useEffect` hook above will log `mounted` when the component is mounted. *Unmounting… clean up here* will be logged when the component unmounts. This can happen when the component is removed from the UI.

The clean-up process typically follows the form below.

<pre><code class="language-javascript">useEffect(() =&gt; {
  //The effect we intend to make
  effect
  
  //We then return the clean up
  return () =&gt; the cleanup/unsubscription
})</code></pre>

While you may not find so many use cases for `useEffect` subscriptions, it is useful when dealing with subscriptions and timers. Particularly, when dealing with web sockets, you may need to unsubscribe from the network to save resources and improve performance when the component unmounts.

### Fetching And Refetching Data With `useEffect`

One of the commonest use cases of the `useEffect` hook is fetching and prefetching data from an API.

To illustrate this, we’ll use fake user data I created from `JSONPlaceholder` to fetch data with the `useEffect` hook.

<pre><code class="language-javascript">import { useEffect, useState } from "react";
import axios from "axios";

export default function App() {
  const [users, setUsers] = useState([]);
  const endPoint =
    "https://my-json-server.typicode.com/ifeanyidike/jsondata/users";

  useEffect(() =&gt; {
    const fetchUsers = async () =&gt; {
      const { data } = await axios.get(endPoint);
      setUsers(data);
    };
    fetchUsers();
  }, []);

  return (
    &lt;div className="App"&gt;
      {users.map((user) =&gt; (
            &lt;div&gt;
              &lt;h2&gt;{user.name}&lt;/h2&gt;
              &lt;p&gt;Occupation: {user.job}&lt;/p&gt;
              &lt;p&gt;Sex: {user.sex}&lt;/p&gt;
            &lt;/div&gt;
          ))}
    &lt;/div&gt;
  );
}</code></pre>

In the code above, we created a `users` state using the `useState` hook. Then we fetched data from an API using Axios. This is an asynchronous process, and so we used the async/await function, we could have also used the dot then the syntax. Since we fetched a list of users, we simply mapped through it to display the data.

Notice that we passed an empty parameter to the hook. This ensures that it is called just once when the component mounts.

We can also **refetch** the data when some conditions change. We’ll show this in the code below.

<pre><code class="language-javascript">import { useEffect, useState } from "react";
import axios from "axios";

export default function App() {
  const [userIDs, setUserIDs] = useState([]);
  const [user, setUser] = useState({});
  const [currentID, setCurrentID] = useState(1);

  const endPoint =
    "https://my-json-server.typicode.com/ifeanyidike/userdata/users";

  useEffect(() =&gt; {
    axios.get(endPoint).then(({ data }) =&gt; setUserIDs(data));
  }, []);

  useEffect(() =&gt; {
    const fetchUserIDs = async () =&gt; {
      const { data } = await axios.get(`${endPoint}/${currentID}`});
      setUser(data);
    };

    fetchUserIDs();
  }, [currentID]);

  const moveToNextUser = () =&gt; {
    setCurrentID((prevId) =&gt; (prevId &lt; userIDs.length ? prevId + 1 : prevId));
  };
  const moveToPrevUser = () =&gt; {
    setCurrentID((prevId) =&gt; (prevId === 1 ? prevId : prevId - 1));
  };
  return (
    &lt;div className="App"&gt;
        &lt;div&gt;
          &lt;h2&gt;{user.name}&lt;/h2&gt;
          &lt;p&gt;Occupation: {user.job}&lt;/p&gt;
          &lt;p&gt;Sex: {user.sex}&lt;/p&gt;
        &lt;/div&gt;
  
      &lt;button onClick={moveToPrevUser}&gt;Prev&lt;/button&gt;
      &lt;button onClick={moveToNextUser}&gt;Next&lt;/button&gt;
    &lt;/div&gt;
  );
}</code></pre>

Here we created two `useEffect` hooks. In the first one, we used the dot then syntax to get all users from our API. This is necessary to determine the number of users.

We then created another `useEffect` hook to get a user based on the `id`. This `useEffect` will refetch the data whenever the id changes. To ensure this, we passed the `id` in the dependency list.

Next, we created functions to update the value of our `id` whenever the buttons are clicked. Once the value of the `id` changes, the `useEffect` will run again and refetch the data.

If we want, we can even clean up or cancel the promise-based token in Axios, we could do that with the clean-up method discussed above.

<pre><code class="language-javascript">useEffect(() =&gt; {
    const source = axios.CancelToken.source();
    const fetchUsers = async () =&gt; {
      const { data } = await axios.get(`${endPoint}/${num}`, {
        cancelToken: source.token
      });
      setUser(data);
    };
    fetchUsers();

    return () =&gt; source.cancel();
  }, [num]);</code></pre>

Here, we passed the Axios’ token as a second parameter to `axios.get`. When the component unmounts we then canceled the subscription by calling the cancel method of the source object.

## The `useReducer` Hook

The `useReducer` hook is a very useful React hook that does a similar thing to the `useState` hook. According to the [React documentation](https://reactjs.org/docs/hooks-reference.html#usereducer), this hook should be used to handle more complex logic than the `useState` hook. It’s worthy of note that the `useState` hook is internally implemented with the useReducer hook.

The hook takes a reducer as an argument and can optionally take the initial state and an init function as arguments. 

<pre><code class="language-javascript">const [state, dispatch] = useReducer(reducer, initialState, init)</code></pre>

Here, `init` is a function and it is used whenever we want to create the initial state lazily. 

Let’s look at how to implement the `useReducer` hook by creating a simple to-do app as shown in the sandbox below.

{{< vimeo id="617035545" caption="Todo Example" breakout="true" >}}

<iframe src="https://codesandbox.io/embed/naughty-bhaskara-iq9y5?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="naughty-bhaskara-iq9y5"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

First off, we should create our reducer to hold the states.

<pre><code class="language-javascript">export const ADD_TODO = "ADD_TODO";
export const REMOVE_TODO = "REMOVE_TODO";
export const COMPLETE_TODO = "COMPLETE_TODO";

const reducer = (state, action) =&gt; {
  switch (action.type) {
    case ADD_TODO:
      const newTodo = {
        id: action.id,
        text: action.text,
        completed: false
      };
      return [...state, newTodo];
    case REMOVE_TODO:
      return state.filter((todo) =&gt; todo.id !== action.id);
    case COMPLETE_TODO:
      const completeTodo = state.map((todo) =&gt; {
        if (todo.id === action.id) {
          return {
            ...todo,
            completed: !todo.completed
          };
        } else {
          return todo;
        }
      });
      return completeTodo;
    default:
      return state;
  }
};
export default reducer;</code></pre>

We created three constants corresponding to our action types. We could have used strings directly but this method is preferable to avoid typos.

Then we created our reducer function. Like in `Redux`, the reducer must take the state and the action object. But unlike Redux, we don't need to initialize our reducer here. 

Furthermore, for a lot of state management use-cases, a `useReducer` along with the `dispatch` exposed via context can enable a larger application to fire actions, update `state` and listen to it.

Then we used the `switch` statements to check the action type passed by the user. If the action type is `ADD_TODO`, we want to pass a new to-do and if it is `REMOVE_TODO`, we want to filter the to-dos and remove the one that corresponds to the `id` passed by the user. If it is `COMPLETE_TODO`, we want to map through the to-dos and toggle the one with the `id` passed by the user.

Here is the `App.js` file where we implemented the `reducer`.

<pre><code class="language-javascript">import { useReducer, useState } from "react";
import "./styles.css";
import reducer, { ADD_TODO, REMOVE_TODO, COMPLETE_TODO } from "./reducer";
export default function App() {
  const [id, setId] = useState(0);
  const [text, setText] = useState("");
  const initialState = [
    {
      id: id,
      text: "First Item",
      completed: false
    }
  ];

  //We could also pass an empty array as the initial state
  //const initialState = []
  
  const [state, dispatch] = useReducer(reducer, initialState);
  const addTodoItem = (e) =&gt; {
    e.preventDefault();
    const newId = id + 1;
    setId(newId);
    dispatch({
      type: ADD_TODO,
      id: newId,
      text: text
    });
    setText("");
  };
  const removeTodo = (id) =&gt; {
    dispatch({ type: REMOVE_TODO, id });
  };
  const completeTodo = (id) =&gt; {
    dispatch({ type: COMPLETE_TODO, id });
  };
  return (
    &lt;div className="App"&gt;
      &lt;h1&gt;Todo Example&lt;/h1&gt;
      &lt;form className="input" onSubmit={addTodoItem}&gt;
        &lt;input value={text} onChange={(e) =&gt; setText(e.target.value)} /&gt;
        &lt;button disabled={text.length === 0} type="submit"&gt;+&lt;/button&gt;
      &lt;/form&gt;
      &lt;div className="todos"&gt;
        {state.map((todo) =&gt; (
          &lt;div key={todo.id} className="todoItem"&gt;
            &lt;p className={todo.completed && "strikethrough"}&gt;{todo.text}&lt;/p&gt;
            &lt;span onClick={() =&gt; removeTodo(todo.id)}&gt;&#10005;&lt;/span&gt;
            &lt;span onClick={() =&gt; completeTodo(todo.id)}&gt;&#10003;&lt;/span&gt;
          &lt;/div&gt;
        ))}
      &lt;/div&gt;
    &lt;/div&gt;
  );
}</code></pre>

Here, we created a form containing an input element, to collect the user’s input, and a button to trigger the action. When the form is submitted, we dispatched an action of type `ADD_TODO`, passing a new id and to-do text. We created a new id by incrementing the previous id value by 1. We then cleared the input text box. To delete and complete to-do, we simply dispatched the appropriate actions. These have already been implemented in the reducer as shown above.

However, the magic happens because we are using the `useReducer` hook. This hook accepts the reducer and the initial state and returns the state and the dispatch function. Here, the dispatch function serves the same purpose as the setter function for the `useState` hook and we can call it anything we want instead of `dispatch`.

To display the to-do items, we simply mapped through the list of to-dos returned in our state object as shown in the code above.

This shows the power of the `useReducer` hook. We could also achieve this functionality with the `useState` hook but as you can see from the example above, the `useReducer` hook helped us to keep things neater. `useReducer` is often beneficial when the state object is a complex structure and is updated in different ways as against a simple value-replace. Also, once these update functions get more complicated, `useReducer` makes it easy to hold all that complexity in a reducer function (which is a pure JS function) making it very easy to write tests for the reducer function alone.

We could have also passed the third argument to the `useReducer` hook to create the initial state lazily. This means that we could calculate the initial state in an `init` function.

For instance, we could create an `init` function as follows:

<pre><code class="language-javascript">const initFunc = () =&gt; [
  {
      id: id,
      text: "First Item",
      completed: false
    }
]</code></pre>

and then pass it to our `useReducer` hook.

<pre><code class="language-javascript">const [state, dispatch] = useReducer(reducer, initialState, initFunc)</code></pre>

If we do this, the `initFunc` will override the `initialState` we provided and the initial state will be calculated lazily.

## The `useContext` Hook

The React Context API provides a way to share states or data throughout the React component tree. The API has been available in React, as an experimental feature, for a while but it became safe to use in React 16.3.0. The API makes data sharing between components easy while eliminating prop drilling.

While you can apply the React Context to your entire application, it is also possible to apply it to part of the application.

To use the hook, you need to first create a context using `React.createContext` and this context can then be passed to the hook.

To demonstrate the use of the `useContext` hook, let’s create a simple app that will increase font size throughout our application.

Let’s create our context in `context.js` file.

<pre><code class="language-javascript">import { createContext } from "react";

//Here, we set the initial fontSize as 16.
const fontSizeContext = createContext(16);
export default fontSizeContext;</code></pre>

Here, we created a context and passed an initial value of `16` to it, and then exported the context. Next, let’s connect our context to our application.

<pre><code class="language-javascript">import FontSizeContext from "./context";
import { useState } from "react";
import PageOne from "./PageOne";
import PageTwo from "./PageTwo";
const App = () =&gt; {
  const [size, setSize] = useState(16);
  return (
    &lt;FontSizeContext.Provider value={size}&gt;
      &lt;PageOne /&gt;
      &lt;PageTwo /&gt;
      &lt;button onClick={() =&gt; setSize(size + 5)}&gt;Increase font&lt;/button&gt;
      &lt;button
        onClick={() =&gt;
          setSize((prevSize) =&gt; Math.min(11, prevSize - 5))
        }
      &gt;
        Decrease font
      &lt;/button&gt;
    &lt;/FontSizeContext.Provider&gt;
  );
};
export default App;</code></pre>

In the above code, we wrapped our entire component tree with `FontSizeContext.Provider` and passed `size` to its value prop. Here, `size` is a state-created with the `useState` hook. This allows us to change the value prop whenever the `size` state changes. By wrapping the entire component with the `Provider`, we can access the context anywhere in our application.

For instance, we accessed the context in `<PageOne />` and `<PageTwo />`. As a result of this, the font size will increase across these two components when we increase it from the `App.js` file. We can increase or decrease the font size from the buttons as shown above and once we do, the font size changes throughout the application.

<pre><code class="language-javascript">import { useContext } from "react";
import context from "./context";
const PageOne = () =&gt; {
  const size = useContext(context);
  return &lt;p style={{ fontSize: `${size}px` }}&gt;Content from the first page&lt;/p&gt;;
};
export default PageOne;</code></pre>

Here, we accessed the context using the `useContext` hook from our `PageOne` component. We then used this context to set our font-size property. A similar procedure applies to the `PageTwo.js` file.

Themes or other higher-order app-level configurations are good candidates for contexts.

### Using `useContext` And `useReducer`

When used with the `useReducer` hook, `useContext` allows us to create our own state management system. We can create global states and easily manage them in our application.

Let’s improve our to-do application using the context API.

As usual, we need to create a `todoContext` in the `todoContext.js` file.

<pre><code class="language-javascript">import { createContext } from "react";
const initialState = [];
export default createContext(initialState);</code></pre>

Here we created the context, passing an initial value of an empty array. Then we exported the context.

Let’s refactor our `App.js` file by separating the to-do list and items.

<pre><code class="language-javascript">import { useReducer, useState } from "react";
import "./styles.css";
import todoReducer, { ADD_TODO } from "./todoReducer";
import TodoContext from "./todoContext";
import TodoList from "./TodoList";

export default function App() {
  const [id, setId] = useState(0);
  const [text, setText] = useState("");
  const initialState = [];
  const [todoState, todoDispatch] = useReducer(todoReducer, initialState);

  const addTodoItem = (e) =&gt; {
    e.preventDefault();
    const newId = id + 1;
    setId(newId);
    todoDispatch({
      type: ADD_TODO,
      id: newId,
      text: text
    });
    setText("");
  };
  return (
    &lt;TodoContext.Provider value={[todoState, todoDispatch]}&gt;
        &lt;div className="app"&gt;
          &lt;h1&gt;Todo Example&lt;/h1&gt;
          &lt;form className="input" onSubmit={addTodoItem}&gt;
            &lt;input value={text} onChange={(e) =&gt; setText(e.target.value)} /&gt;
            &lt;button disabled={text.length === 0} type="submit"&gt;
              +
            &lt;/button&gt;
          &lt;/form&gt;
          &lt;TodoList /&gt;
        &lt;/div&gt;
    &lt;/TodoContext.Provider&gt;
  );
}</code></pre>

Here, we wrapped our `App.js` file with the `TodoContext.Provider` then we passed the return values of our `todoReducer` to it. This makes the reducer’s state and `dispatch` function to be accessible throughout our application.

We then separated the to-do display into a component `TodoList`. We did this without prop drilling, thanks to the Context API. Let’s take a look at the `TodoList.js` file.

<pre><code class="language-javascript">import React, { useContext } from "react";
import TodoContext from "./todoContext";
import Todo from "./Todo";
const TodoList = () =&gt; {
  const [state] = useContext(TodoContext);
  return (
    &lt;div className="todos"&gt;
      {state.map((todo) =&gt; (
        &lt;Todo key={todo.id} todo={todo} /&gt;
      ))}
    &lt;/div&gt;
  );
};
export default TodoList;</code></pre>

Using array destructuring, we can access the state (leaving the dispatch function) from the context using the `useContext` hook. We can then map through the state and display the to-do items. We still extracted this in a `Todo` component. The ES6+ map function requires us to pass a unique key and since we need the specific to-do, we pass it alongside as well.

Let’s take a look at the `Todo` component.

<pre><code class="language-javascript">import React, { useContext } from "react";
import TodoContext from "./todoContext";
import { REMOVE_TODO, COMPLETE_TODO } from "./todoReducer";
const Todo = ({ todo }) =&gt; {
  const [, dispatch] = useContext(TodoContext);
  const removeTodo = (id) =&gt; {
    dispatch({ type: REMOVE_TODO, id });
  };
  const completeTodo = (id) =&gt; {
    dispatch({ type: COMPLETE_TODO, id });
  };
  return (
    &lt;div className="todoItem"&gt;
      &lt;p className={todo.completed ? "strikethrough" : "nostrikes"}&gt;
        {todo.text}
      &lt;/p&gt;
      &lt;span onClick={() =&gt; removeTodo(todo.id)}&gt;&#10005;&lt;/span&gt;
      &lt;span onClick={() =&gt; completeTodo(todo.id)}&gt;&#10003;&lt;/span&gt;
    &lt;/div&gt;
  );
};
export default Todo;</code></pre>

Again using array destructuring, we accessed the dispatch function from the context. This allows us to define the `completeTodo` and `removeTodo` function as already discussed in the `useReducer` section. With the `todo` prop passed from `todoList.js` we can display a to-do item. We can also mark it as completed and remove the to-do as we deem fit.

It is also possible to nest more than one context provider in the root of our application. This means that we can use more than one context to perform different functions in an application.

To demonstrate this, let’s add theming to the to-do example.

Here’s what we’ll be building.

{{< vimeo id="617978634" breakout="true" >}}

<iframe src="https://codesandbox.io/embed/cold-glitter-3ipz4?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="cold-glitter-3ipz4"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

Again, we have to create `themeContext`. To do this, create a `themeContext.js` file and add the following codes.

<pre><code class="language-javascript">import { createContext } from "react";
import colors from "./colors";
export default createContext(colors.light);</code></pre>

Here, we created a context and passed `colors.light` as the initial value. Let’s define the colors with this property in the `colors.js` file.

<pre><code class="language-javascript">const colors = {
  light: {
    backgroundColor: "#fff",
    color: "#000"
  },
  dark: {
    backgroundColor: "#000",
    color: "#fff"
  }
};
export default colors;</code></pre>

In the code above, we created a `colors` object containing light and dark properties. Each property has `backgroundColor` and `color` object.

Next, we create the `themeReducer` to handle the theme states.

<pre><code class="language-javascript">import Colors from "./colors";
export const LIGHT = "LIGHT";
export const DARK = "DARK";
const themeReducer = (state, action) =&gt; {
  switch (action.type) {
    case LIGHT:
      return {
        ...Colors.light
      };
    case DARK:
      return {
        ...Colors.dark
      };
    default:
      return state;
  }
};
export default themeReducer;</code></pre>

Like all reducers, the `themeReducer` takes the state and the action. It then uses the `switch` statement to determine the current action. If it’s of type `LIGHT`, we simply assign `Colors.light` props and if it’s of type `DARK`, we display `Colors.dark` props. We could have easily done this with the `useState` hook but we choose `useReducer` to drive the point home.

Having set up the `themeReducer`, we can then integrate it in our `App.js` file.

<pre><code class="language-javascript">import { useReducer, useState, useCallback } from "react";
import "./styles.css";
import todoReducer, { ADD_TODO } from "./todoReducer";
import TodoContext from "./todoContext";
import ThemeContext from "./themeContext";
import TodoList from "./TodoList";
import themeReducer, { DARK, LIGHT } from "./themeReducer";
import Colors from "./colors";
import ThemeToggler from "./ThemeToggler";

const themeSetter = useCallback(
      theme =&gt; themeDispatch({type: theme}, 
    [themeDispatch]);

export default function App() {
  const [id, setId] = useState(0);
  const [text, setText] = useState("");
  const initialState = [];
  const [todoState, todoDispatch] = useReducer(todoReducer, initialState);
  const [themeState, themeDispatch] = useReducer(themeReducer, Colors.light);
  const themeSetter = useCallback(
    (theme) =&gt; {
      themeDispatch({ type: theme });
    },
    [themeDispatch]
  );
  const addTodoItem = (e) =&gt; {
    e.preventDefault();
    const newId = id + 1;
    setId(newId);
    todoDispatch({
      type: ADD_TODO,
      id: newId,
      text: text
    });
    setText("");
  };

  return (
    &lt;TodoContext.Provider value={[todoState, todoDispatch]}&gt;
      &lt;ThemeContext.Provider
        value={[
          themeState,
          themeSetter
        ]}
      &gt;
        &lt;div className="app" style={{ ...themeState }}&gt;
          &lt;ThemeToggler /&gt;
          &lt;h1&gt;Todo Example&lt;/h1&gt;
          &lt;form className="input" onSubmit={addTodoItem}&gt;
            &lt;input value={text} onChange={(e) =&gt; setText(e.target.value)} /&gt;
            &lt;button disabled={text.length === 0} type="submit"&gt;
              +
            &lt;/button&gt;
          &lt;/form&gt;
          &lt;TodoList /&gt;
        &lt;/div&gt;
      &lt;/ThemeContext.Provider&gt;
    &lt;/TodoContext.Provider&gt;
  );
}</code></pre>

In the above code, we added a few things to our already existing to-do application. We began by importing the `ThemeContext`, `themeReducer`, `ThemeToggler`, and `Colors`. We created a reducer using the `useReducer` hook, passing the `themeReducer` and an initial value of `Colors.light` to it. This returned the `themeState` and `themeDispatch` to us.

We then nested our component with the provider function from the `ThemeContext`, passing the `themeState` and the `dispatch` functions to it. We also added theme styles to it by spreading out the `themeStates`. This works because the `colors` object already defined properties similar to what the JSX styles will accept.

However, the actual theme toggling happens in the `ThemeToggler` component. Let’s take a look at it.

<pre><code class="language-javascript">import ThemeContext from "./themeContext";
import { useContext, useState } from "react";
import { DARK, LIGHT } from "./themeReducer";
const ThemeToggler = () =&gt; {
  const [showLight, setShowLight] = useState(true);
  const [themeState, themeSetter] = useContext(ThemeContext);
  const dispatchDarkTheme = () =&gt; themeSetter(DARK);
  const dispatchLightTheme = () =&gt; themeSetter(LIGHT);
  const toggleTheme = () =&gt; {
    showLight ? dispatchDarkTheme() : dispatchLightTheme();
    setShowLight(!showLight);
  };
  console.log(themeState);
  return (
    &lt;div&gt;
      &lt;button onClick={toggleTheme}&gt;
        {showLight ? "Change to Dark Theme" : "Change to Light Theme"}
      &lt;/button&gt;
    &lt;/div&gt;
  );
};
export default ThemeToggler;</code></pre>

In this component, we used the `useContext` hook to retrieve the values we passed to the `ThemeContext.Provider` from our `App.js` file. As shown above, these values include the `ThemeState`, dispatch function for the light theme, and dispatch function for the dark theme. Thereafter, we simply called the dispatch functions to toggle the themes. We also created a state `showLight` to determine the current theme. This allows us to easily change the button text depending on the current theme.

{{% ad-panel-leaderboard %}}

## The `useMemo` Hook

The `useMemo` hook is designed to memoize expensive computations. Memoization simply means caching. It caches the computation result with respect to the dependency values so that when the same values are passed, `useMemo` will just spit out the already computed value without recomputing it again. This can significantly improve performance when done correctly. 

The hook can be used as follows:

<pre><code class="language-javascript">const memoizedResult = useMemo(() => expensiveComputation(a, b), [a, b])</code></pre>

Let’s consider three cases of the `useMemo` hook.

1. **When the dependency values, a and b remain the same.**  
  The `useMemo` hook will return the already computed memoized value without recomputation.
2. **When the dependency values, a and b change.**  
  The hook will recompute the value.
3. **When no dependency value is passed.**  
  The hook will recompute the value.

Let’s take a look at an example to demonstrate this concept.

In the example below, we’ll be computing the **PAYE** and **Income after PAYE** of a company’s employees with fake data from JSONPlaceholder.

The calculation will be based on the personal income tax calculation procedure for Nigeria providers by PricewaterhouseCoopers available [here](https://taxsummaries.pwc.com/nigeria/individual/sample-personal-income-tax-calculation).

This is shown in the sandbox below.

<iframe src="https://codesandbox.io/embed/sparkling-water-fludc?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="sparkling-water-fludc"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

First, we queried the API to get the employees’ data. We also get data for each employee (with respect to their employee id).

<pre><code class="language-javascript">const [employee, setEmployee] = useState({});
  const [employees, setEmployees] = useState([]);
  const [num, setNum] = useState(1);
  const endPoint =
    "https://my-json-server.typicode.com/ifeanyidike/jsondata/employees";
  useEffect(() =&gt; {
    const getEmployee = async () =&gt; {
      const { data } = await axios.get(`${endPoint}/${num}`);
      setEmployee(data);
    };
    getEmployee();
  }, [num]);
  useEffect(() =&gt; {
    axios.get(endPoint).then(({ data }) =&gt; setEmployees(data));
  }, [num]);</code></pre>

We used `axios` and the `async/await` method in the first `useEffect` and then the dot then syntax in the second. These two approaches work in the same way.

Next, using the employee data we got from above, let’s calculate the relief variables:

<pre><code class="language-javascript">const taxVariablesCompute = useMemo(() =&gt; {
    const { income, noOfChildren, noOfDependentRelatives } = employee;
    
    //supposedly complex calculation
    //tax relief computations for relief Allowance, children relief, 
    // relatives relief and pension relief

    const reliefs =
      reliefAllowance1 +
      reliefAllowance2 +
      childrenRelief +
      relativesRelief +
      pensionRelief;
    return reliefs;
  }, [employee]);</code></pre>

This is a fairly complex calculation and so we had to wrap it in a `useMemo` hook to memoize or optimize it. Memoizing it this way will ensure that the calculation will not be recomputed if we tried to access the same employee again. 

Furthermore, using the tax relief values obtained above, we’d like to calculate the PAYE and income after PAYE.

<pre><code class="language-javascript">const taxCalculation = useMemo(() =&gt; {
    const { income } = employee;
    let taxableIncome = income - taxVariablesCompute;
    let PAYE = 0;
    
    //supposedly complex calculation
    //computation to compute the PAYE based on the taxable income and tax endpoints
    
    const netIncome = income - PAYE;
    return { PAYE, netIncome };
  }, [employee, taxVariablesCompute]);</code></pre>

We performed tax calculation (a fairly complex calculation) using the above-computed tax variables and then memoized it with the `useMemo` hook.

The complete code is available on [here](https://gist.github.com/ifeanyidike/bc008cf6a28140199aeb74d7ecd90261).

This follows the tax calculation procedure given [here](https://taxsummaries.pwc.com/nigeria/individual/sample-personal-income-tax-calculation). We first computed the tax relief considering income, number of children, and number of dependent relatives. Then, we multiplied the taxable income by the PIT rates in steps. While the calculation in question is not entirely necessary for this tutorial, it is provided to show us why `useMemo` may be necessary. This is also a fairly complex calculation and so we may need to memorize it with `useMemo` as shown above.

After calculating the values, we simply displayed the result.

Note the following about the `useMemo` hook.

- `useMemo` should be used only when it is necessary to optimize the computation. In other words, when recomputation is expensive.
- It is advisable to first write the calculation without memorization and only memorize it if it is causing performance issues.
- Unnecessary and irrelevant use of the `useMemo` hook may even compound the performance issues.
- Sometimes, too much memoization can also cause performance issues.

## The `useCallback` Hook

`useCallback` serves the same purpose as `useMemo` but it returns a memoized callback instead of a memoized value. In other words, `useCallback` is the same as passing `useMemo` without a function call.

For instance, consider the following codes below.

<pre><code class="language-javascript">import React, {useCallback, useMemo} from 'react'

const MemoizationExample = () =&gt; {
  const a = 5
  const b = 7
  
  const memoResult = useMemo(() =&gt; a + b, [a, b])
  const callbackResult = useCallback(a + b, [a, b])

  console.log(memoResult)
  console.log(callbackResult)

  return(
    &lt;div&gt;
      ...
    &lt;/div&gt;
  ) 
}

export default MemoizationExample</code></pre>

In the above example, both `memoResult` and `callbackResult` will give the same value of `12`. Here, `useCallback` will return a memoized value. However, we could also make it return a memoized callback by passing it as a function.

The `useCallback` below will return a memoized callback.

<pre><code class="language-javascript">...
  const callbackResult = useCallback(() =&gt; a + b, [a, b])
...</code></pre>

We can then trigger the callback when an action is performed or in a `useEffect` hook.

<pre><code class="language-javascript">import {useCallback, useEffect} from 'react'
const memoizationExample = () =&gt; {
  const a = 5
  const b = 7
  const callbackResult = useCallback(() =&gt; a + b, [a, b])
  useEffect(() =&gt; {
    const callback = callbackResult()
    console.log(callback)   
  })

  return (
    &lt;div&gt;
      &lt;button onClick= {() =&gt; console.log(callbackResult())}&gt;
        Trigger Callback
      &lt;/button&gt;
    &lt;/div&gt;
  )
} 
export default memoizationExample</code></pre>

In the above code, we defined a callback function using the `useCallback` hook. We then called the callback in a `useEffect` hook when the component mounts and also when a button is clicked.

Both the `useEffect` and the button click yield the same result.

Note that the concepts, do’s, and don’ts that apply to the `useMemo` hook also apply to the `useCallback` hook. We can recreate the `useMemo` example with `useCallback`. 

## The `useRef` Hook

`useRef` returns an object that can persist in an application. The hook has only one property, `current`, and we can easily pass an argument to it.

It serves the same purpose a `createRef` used in class-based components. We can create a reference with this hook as follows:

<pre><code class="language-javascript">const newRef = useRef('')</code></pre>

Here we created a new ref called `newRef` and passed an empty string to it.

This hook is used mainly for two purposes:

1. Accessing or manipulating the DOM, and
2. Storing mutable states &mdash; this is useful when we don’t want the component to rerender when a value change.

### Manipulating the DOM

When passed to a DOM element, the ref object points to that element and can be used to access its DOM attributes and properties.

Here is a very simple example to demonstrate this concept.

<pre><code class="language-javascript">import React, {useRef, useEffect} from 'react'

const RefExample = () =&gt; {
  const headingRef = useRef('')
  console.log(headingRef)
  return(
    &lt;div&gt;
      &lt;h1 className='topheading' ref={headingRef}&gt;This is a h1 element&lt;/h1&gt;
    &lt;/div&gt;
  )
}
export default RefExample</code></pre>

In the example above, we defined `headingRef` using the `useRef` hook passing an empty string. We then set the ref in the `h1` tag by passing `ref  = {headingRef}`. By setting this ref, we have asked the `headingRef` to point to our `h1` element. This means that we can access the properties of our `h1` element from the ref.

To see this, if we check the value of `console.log(headingRef)`, we’ll get `{current: HTMLHeadingElement}` or `{current: h1}` and we can assess all the properties or attributes of the element. A similar thing applies to any other HTML element.

For instance, we could make the text italic when the component mounts.

<pre><code class="language-javascript">useEffect(() =&gt; {
  headingRef.current.style.fontStyle = "italic";
}, []);</code></pre>

We can even change the text to something else.

<pre><code class="language-javascript">...
    headingRef.current.innerHTML = "A Changed H1 Element";
...</code></pre>

We can even change the background color of the parent container as well.

<pre><code class="language-javascript">...
    headingRef.current.parentNode.style.backgroundColor = "red";
...</code></pre>

Any kind of DOM manipulation can be done here. Observe that `headingRef.current` can be read in the same way as  `document.querySelector('.topheading')`. 

One interesting use case of the `useRef` hook in manipulating the DOM element is to focus the cursor on the input element. Let’s quickly run through it.

<pre><code class="language-javascript">import {useRef, useEffect} from 'react'

const inputRefExample = () =&gt; {
  const inputRef = useRef(null)
  useEffect(() =&gt; {
    inputRef.current.focus()
  }, [])
  
  return(
    &lt;div&gt;
      &lt;input ref={inputRef} /&gt;
      &lt;button onClick = {() =&gt; inputRef.current.focus()}&gt;Focus on Input &lt;/button&gt;
    &lt;/div&gt;
  )
}
export default inputRefExample</code></pre>

In the above code, we created `inputRef` using the `useRef` hook and then asked it to point to the input element. We then made the cursor focus on the input ref when the component loads and when the button is clicked using `inputRef.current.focus()`. This is possible because `focus()` is an attribute of input elements and so the ref will be able to assess the methods.

Refs created in a parent component can be assessed at the child component by forwarding it using `React.forwardRef()`. Let’s take a look at it.

Let’s first create another component `NewInput.js` and add the following codes to it.

<pre><code class="language-javascript">import { useRef, forwardRef } from "react";
const NewInput = forwardRef((props, ref) =&gt; {
  return &lt;input placeholder={props.val} ref={ref} /&gt;;
});
export default NewInput;</code></pre>

This component accepts `props` and `ref`. We passed the ref to its ref prop and `props.val` to its placeholder prop. Regular React components do not take a `ref` attribute. This attribute is available only when we wrap it with `React.forwardRef` as shown above.

We can then easily call this in the parent component.

<pre><code class="language-javascript">...
&lt;NewInput val="Just an example" ref={inputRef} /&gt;
...</code></pre>

### Storing The Mutable States

Refs are not just used to manipulate DOM elements, they can also be used to store mutable values without re-rendering the entire component.

The following example will detect the number of times a button is clicked without re-rendering the component.

<pre><code class="language-javascript">import { useRef } from "react";

export default function App() {
  const countRef = useRef(0);
  const increment = () =&gt; {
    countRef.current++;
    console.log(countRef);
  };
  return (
    &lt;div className="App"&gt;
      &lt;button onClick={increment}&gt;Increment &lt;/button&gt;
    &lt;/div&gt;
  );
}</code></pre>

In the code above, we incremented the `countRef` when the button is clicked and then logged it to the console. Although the value is incremented as shown in the console, we won’t be able to see any change if we try to assess it directly in our component. It will only update in the component when it re-renders.

Note that while `useState` is asynchronous, `useRef` is synchronous. In other words, the value is available immediately after it is updated.

## The `useLayoutEffect` Hook

Like the `useEffect` hook, `useLayoutEffect` is called after the component is mounted and rendered. This hook fires after DOM mutation and it does so synchronously. Apart from getting called synchronously after DOM mutation, `useLayoutEffect` does the same thing as `useEffect`. 

`useLayoutEffect` should only be used for performing DOM mutation or DOM-related measurement, otherwise, you should use the `useEffect` hook. Using the `useEffect` hook for DOM mutation functions may cause some performance issues such as flickering but `useLayoutEffect` handles them perfectly as it runs after the mutations have occurred.

Let’s take a look at some examples to demonstrate this concept.

1. We’ll be getting the width and height of the window on resize.

<pre><code class="language-javascript">import {useState, useLayoutEffect} from 'react'

const ResizeExample = () =&gt;{
  const [windowSize, setWindowSize] = useState({width: 0, height: 0})
  useLayoutEffect(() =&gt; {
    const resizeWindow = () =&gt; setWindowSize({
      width: window.innerWidth,
      height: window.innerHeight
    })
    window.addEventListener('resize', resizeWindow)
    return () =&gt; window.removeEventListener('resize', resizeWindow)
  }, [])

  return (
    &lt;div&gt;
      &lt;p&gt;width: {windowSize.width}&lt;/p&gt;
      &lt;p&gt;height: {windowSize.height}&lt;/p&gt;
    &lt;/div&gt;
  )
}
export default ResizeExample</code></pre>

In the above code, we created a state `windowSize` with width and height properties. Then we set the state to the current window’s width and height respectively when the window is resized. We also cleaned up the code when it unmounts. The clean-up process is essential in `useLayoutEffect` to clean up the DOM manipulation and improve efficiency.

2. Let’s blur a text with `useLayoutEffect`.

<pre><code class="language-javascript">import { useRef, useState, useLayoutEffect } from "react";

export default function App() {
  const paragraphRef = useRef("");

  useLayoutEffect(() =&gt; {
    const { current } = paragraphRef;
    const blurredEffect = () =&gt; {
      current.style.color = "transparent";
      current.style.textShadow = "0 0 5px rgba(0,0,0,0.5)";
    };
    current.addEventListener("click", blurredEffect);
    return () =&gt; current.removeEventListener("click", blurredEffect);
  }, []);

  return (
    &lt;div className="App"&gt;
      &lt;p ref={paragraphRef}&gt;This is the text to blur&lt;/p&gt;
    &lt;/div&gt;
  );
}</code></pre>

We used `useRef` and `useLayoutEffect` together in the above code. We first created a ref, `paragraphRef` to point to our paragraph. Then we created an on-click event listener to monitor when the paragraph is clicked and then blurred it using the style properties we defined. Finally, we cleaned up the event listener using `removeEventListener`.

## The `useDispatch` And `useSelector` Hooks

`useDispatch` is a Redux hook for dispatching (triggering) actions in an application. It takes an action object as an argument and invokes the action. `useDispatch` is the hook’s equivalence to `mapDispatchToProps`. 

On the other hand, `useSelector` is a Redux hook for assessing Redux states. It takes a function to select the exact Redux reducer from the store and then returns the corresponding states.

Once our Redux store is connected to a React application through the Redux provider, we can invoke the actions with `useDispatch` and access the states with `useSelector`. Every Redux action and state can be assessed with these two hooks. 

Note that these states ship with React Redux (a package that makes assessing the Redux store easy in a React application). They are not available in the core Redux library.

These hooks are very simple to use. First, we have to declare the dispatch function and then trigger it.

<pre><code class="language-javascript">import {useDispatch, useSelector} from 'react-redux'
import {useEffect} from 'react'
const myaction from '...'

const ReduxHooksExample = () =&gt;{
  const dispatch = useDispatch()
  useEffect(() =&gt; {
    dispatch(myaction());
    //alternatively, we can do this
    dispatch({type: 'MY_ACTION_TYPE'})
  }, [])       
  
  const mystate = useSelector(state =&gt; state.myReducerstate)
  
  return(
    ...
  )
}
export default ReduxHooksExample</code></pre>

In the above code, we imported `useDispatch` and `useSelector` from `react-redux`. Then, in a `useEffect` hook, we dispatched the action. We could define the action in another file and then call it here or we could define it directly as shown in the `useEffect` call. 

Once we have dispatched the actions, our states will be available. We can then retrieve the state using the `useSelector` hook as shown. The states can be used in the same way we would use states from the `useState` hook.

Let’s take a look at an example to demonstrate these two hooks.

To demonstrate this concept, we have to create a Redux store, reducer, and actions. To simplify things here, we’ll be using the Redux Toolkit library with our fake database from JSONPlaceholder.

We need to install the following packages to get started. Run the following bash commands.

<pre><code class="language-bash">npm i redux @reduxjs/toolkit react-redux axios</code></pre>

First, let’s create the `employeesSlice.js` to handle the reducer and action for our employees’ API.

<pre><code class="language-javascript">import { createAsyncThunk, createSlice } from "@reduxjs/toolkit";
import axios from "axios";
const endPoint = "https://my-json-server.typicode.com/ifeanyidike/jsondata/employees";

export const fetchEmployees = createAsyncThunk("employees/fetchAll", async () =&gt; {
    const { data } = await axios.get(endPoint);
    return data;
});

const employeesSlice = createSlice({
  name: "employees",
  initialState: { employees: [], loading: false, error: "" },
  reducers: {},
  extraReducers: {
    [fetchEmployees.pending]: (state, action) =&gt; {
      state.status = "loading";
    },
    [fetchEmployees.fulfilled]: (state, action) =&gt; {
      state.status = "success";
      state.employees = action.payload;
    },
    [fetchEmployees.rejected]: (state, action) =&gt; {
      state.status = "error";
      state.error = action.error.message;
    }
  }
});
export default employeesSlice.reducer;</code></pre>

This is the standard setup for the Redux toolkit. We used the `createAsyncThunk` to access the `Thunk` middleware to perform async actions. This allowed us to fetch the list of employees from the API. We then created the `employeesSlice` and returned, “loading”, “error”, and the employees’ data depending on the action types.

Redux toolkit also makes setting up the store easy. Here is the store.

<pre><code class="language-javascript">import { configureStore } from "@reduxjs/toolkit";
import { combineReducers } from "redux";
import employeesReducer from "./employeesSlice";

const reducer = combineReducers({
  employees: employeesReducer
});

export default configureStore({ reducer });;</code></pre>

Here, we used `combineReducers` to bundle the reducers and the `configureStore` function provided by Redux toolkit to set up the store.

Let’s proceed to use this in our application.

First, we need to connect Redux to our React application. Ideally, this should be done at the root of our application. I like to do it in the `index.js` file.

<pre><code class="language-javascript">import React, { StrictMode } from "react";
import ReactDOM from "react-dom";
import store from "./redux/store";
import { Provider } from "react-redux";
import App from "./App";
const rootElement = document.getElementById("root");
ReactDOM.render(
  &lt;Provider store={store}&gt;
    &lt;StrictMode&gt;
      &lt;App /&gt;
    &lt;/StrictMode&gt;
  &lt;/Provider&gt;,
  rootElement
);</code></pre>

Here, I’ve imported the store I created above and also `Provider` from `react-redux`.

Then, I wrapped the entire application with the `Provider` function, passing the store to it. This makes the store accessible throughout our application.

We can then proceed to use the `useDispatch` and `useSelector` hooks to fetch the data.

Let’s do this in our `App.js` file.

<pre><code class="language-javascript">import { useDispatch, useSelector } from "react-redux";
import { fetchEmployees } from "./redux/employeesSlice";
import { useEffect } from "react";

export default function App() {
  const dispatch = useDispatch();
  useEffect(() =&gt; {
    dispatch(fetchEmployees());
  }, [dispatch]);
  const employeesState = useSelector((state) =&gt; state.employees);
  const { employees, loading, error } = employeesState;

  return (
    &lt;div className="App"&gt;
      {loading ? (
        "Loading..."
      ) : error ? (
        &lt;div&gt;{error}&lt;/div&gt;
      ) : (
        &lt;&gt;
          &lt;h1&gt;List of Employees&lt;/h1&gt;
          {employees.map((employee) =&gt; (
            &lt;div key={employee.id}&gt;
              &lt;h3&gt;{`${employee.firstName} ${employee.lastName}`}&lt;/h3&gt;
            &lt;/div&gt;
          ))}
        &lt;/&gt;
      )}
    &lt;/div&gt;
  );
}</code></pre>

In the above code, we used the `useDispatch` hook to invoke the `fetchEmployees` action created in the `employeesSlice.js` file. This makes the employees state to be available in our application. Then, we used the `useSelector` hook to get the states. Thereafter, we displayed the results by mapping through the `employees`.

## The `useHistory` Hook

Navigation is very important in a React application. While you could achieve this in a couple of ways, React Router provides a simple, efficient and popular way to achieve dynamic routing in a React application. Furthermore, React Router provides a couple of hooks for assessing the state of the router and performing navigation on the browser but to use them, you need to first set up your application properly.

To use any React Router hook, we should first wrap our application with `BrowserRouter`. We can then nest the routes with `Switch` and `Route`.

But first, we have to install the package by running the following commands.

<pre><code class="language-bash">npm install react-router-dom</code></pre>

Then, we need to set up our application as follows. I like to do this in my `App.js` file.

<pre><code class="language-javascript">import { BrowserRouter as Router, Switch, Route } from "react-router-dom";
import Employees from "./components/Employees";
export default function App() {
  return (
    &lt;div className="App"&gt;
      &lt;Router&gt;
        &lt;Switch&gt;
          &lt;Route path='/'&gt;
            &lt;Employees /&gt;
          &lt;/Route&gt;
          ...
        &lt;/Switch&gt;
      &lt;/Router&gt;
    &lt;/div&gt;
  );
}</code></pre>

We could have as many Routes as possible depending on the number of components we wish to render. Here, we have rendered only the `Employees` component. The `path` attribute tells React Router DOM the path of the component and can be assessed with query string or various other methods.

The order matters here. The root route should be placed below the child route and so forth. To override this order, you need to include the `exact` keyword on the root route.

<pre><code class="language-javascript">&lt;Route path='/' exact &gt;
  &lt;Employees /&gt;
&lt;/Route&gt;</code></pre>

Now that we have set up the router, we can then use the `useHistory` hook and other React Router hooks in our application.

To use the `useHistory` hook, we need to first declare it as follows.

<pre><code class="language-javascript">import {useHistory} from 'history'
import {useHistory} from 'react-router-dom'

const Employees = () =&gt;{
  const history = useHistory()
  ...
}</code></pre>

If we log history to the console, we’ll see several properties associated with it. These include `block`, `createHref`, `go`, `goBack`, `goForward`, `length`, `listen`, `location`, `push`, `replace`. While all these properties are useful, you will most likely use `history.push` and `history.replace` more often than other properties.

Let’s use this property to move from one page to another.

Assuming we want to fetch data about a particular employee when we click on their names. We can use the `useHistory` hook to navigate to the new page where the employee’s information will be displayed.

<pre><code class="language-javascript">function moveToPage = (id) =&gt;{
  history.push(`/employees/${id}`)
}</code></pre>

We can implement this in our `Employee.js` file by adding the following.

<pre><code class="language-javascript">import { useEffect } from "react";
import { Link, useHistory, useLocation } from "react-router-dom";

export default function Employees() {
  const history = useHistory();

  function pushToPage = (id) =&gt; {
    history.push(`/employees/${id}`)
  }
  ...
  return (
    &lt;div&gt;
     ...
        &lt;h1&gt;List of Employees&lt;/h1&gt;
        {employees.map((employee) =&gt; (
          &lt;div key={employee.id}&gt;
            &lt;span&gt;{`${employee.firstName} ${employee.lastName} `}&lt;/span&gt;
            &lt;button onClick={pushToPage(employee.id)}&gt; &raquo; &lt;/button&gt;
          &lt;/div&gt;
        ))}
  &lt;/div&gt;
  );
}</code></pre>

In the `pushToPage` function, we used `history` from the `useHistory` hook to navigate to the employee’s page and pass the employee id alongside.

## The `useLocation` Hook

This hook also ships with React Router DOM. It is a very popular hook used to work with the query string parameter. This hook is similar to the `window.location` in the browser.

<pre><code class="language-javascript">import {useLocation} from 'react'

const LocationExample = () =&gt;{
  const location = useLocation()
  return (
    ...
  )
}
export default LocationExample</code></pre>

The `useLocation` hook returns the `pathname`, `search` parameter, `hash` and `state`. The most commonly used parameters include the `pathname` and `search` but you could equally use `hash`, and `state` a lot in your application.

The location `pathname` property will return the path we set in our `Route` set up. While `search` will return the query search parameter if any. For instance, if we pass `'http://mywebsite.com/employee/?id=1'` to our query, the `pathname` would be `/employee` and the `search` would be `?id=1`.

We can then retrieve the various search parameters using packages like query-string or by coding them.

## The `useParams` Hook

If we set up our Route with a URL parameter in its path attribute, we can assess those parameters as key/value pairs with the `useParams` hook.

For instance, let’s assume that we have the following Route.

<pre><code class="language-javascript">&lt;Route path='/employees/:id' &gt;
  &lt;Employees /&gt;
&lt;/Route&gt;</code></pre>

The Route will be expecting a dynamic id in place of `:id`.

With the `useParams` hook, we can assess the id passed by the user, if any.

For instance, assuming the user passes the following in function with `history.push`, 

<pre><code class="language-javascript">function goToPage = () =&gt; {
  history.push(`/employee/3`)
}</code></pre>

We can use the `useParams` hook to access this URL parameter as follows.

<pre><code class="language-javascript">import {useParams} from 'react-router-dom'

const ParamsExample = () =&gt;{
  const params = useParams()
  console.log(params)  

  return(
    &lt;div&gt;
      ...
    &lt;/div&gt;
  )
}
export default ParamsExample</code></pre>

If we log `params` to the console, we’ll get the following object `{id: "3"}`. 

## The `useRouteMatch` Hook

This hook provides access to the match object. It returns the closest match to a component if no argument is supplied to it.

The match object returns several parameters including the `path` (the same as the path specified in Route), the `URL`, `params` object, and `isExact`.

For instance, we can use `useRouteMatch` to return components based on the route.

<pre><code class="language-javascript">import { useRouteMatch } from "react-router-dom";
import Employees from "...";
import Admin from "..."

const CustomRoute = () =&gt; {
  const match = useRouteMatch("/employees/:id");
  return match ? (
    &lt;Employee /&gt; 
  ) : (
    &lt;Admin /&gt;
  );
};
export default CustomRoute;</code></pre>

In the above code, we set a route’s path with `useRouteMatch` and then rendered the `<Employee />` or `<Admin />` component depending on the route selected by the user.

For this to work, we still need to add the route to our `App.js` file.

<pre><code class="language-javascript">...
  &lt;Route&gt;
    &lt;CustomRoute /&gt;
  &lt;/Route&gt;
...</code></pre>

## Building A Custom Hook

According to the React documentation, [building a custom hook allows us to extract a logic into a reusable function](https://reactjs.org/docs/hooks-custom.html). However, you need to make sure that all the rules that apply to React hooks apply to your custom hook. Check the rules of React hook at the top of this tutorial and ensure that your custom hook complies with each of them.

Custom hooks allow us to write functions once and reuse them whenever they are needed and hence obeying the DRY principle. 

For instance, we could create a custom hook to get the scroll position on our page as follows.

<pre><code class="language-javascript">import { useLayoutEffect, useState } from "react";

export const useScrollPos = () =&gt; {
  const [scrollPos, setScrollPos] = useState({
    x: 0,
    y: 0
  });
  useLayoutEffect(() =&gt; {
    const getScrollPos = () =&gt;
      setScrollPos({
        x: window.pageXOffset,
        y: window.pageYOffset
      });
    window.addEventListener("scroll", getScrollPos);
    return () =&gt; window.removeEventListener("scroll", getScrollPos);
  }, []);
  return scrollPos;
};
</code></pre>

Here, we defined a custom hook to determine the scroll position on a page. To achieve this, we first created a state, `scrollPos`, to store the scroll position. Since this will be modifying the DOM, we need to use `useLayoutEffect` instead of `useEffect`. We added a scroll event listener to capture the x and y scroll positions and then cleaned up the event listener. Finally, we returned to the scroll position.

We can use this custom hook anywhere in our application by calling it and using it just as we would use any other state.

<pre><code class="language-javascript">import {useScrollPos} from './Scroll'

const App = () =&gt;{
  const scrollPos = useScrollPos()
  console.log(scrollPos.x, scrollPos.y)
  return (
    ...
  )
}
export default App</code></pre>

Here, we imported the custom hook `useScrollPos` we created above. Then we initialized it and then logged the value to our console. If we scroll on the page, the hook will show us the scroll position at every step of the scroll.

We can create custom hooks to do just about anything we can imagine in our app. As you can see, we simply need to use the inbuilt React hook to perform some functions. We can also use third-party libraries to create custom hooks but if we do so, we will have to install that library to be able to use the hook.

## Conclusion

In this tutorial, we took a good look at some useful React hooks you will be using in most of your applications. We examined what they present and how to use them in your application. We also looked at several code examples to help you understand these hooks and apply them to your application.

I encourage you to try these hooks in your own application to understand them more.

### Resources From The React Docs

- [Hooks FAQ](https://reactjs.org/docs/hooks-faq.html)
- [Redux Toolkit](https://redux-toolkit.js.org/api/createAsyncThunk)
- [Using the State Hook](https://reactjs.org/docs/hooks-state.html)
- [Using the Effect Hook](https://reactjs.org/docs/hooks-effect.html)
- [Hooks API Reference](https://reactjs.org/docs/hooks-reference.html)
- [React Redux Hooks](https://react-redux.js.org/api/hooks)
- [React Router Hooks](https://reactrouter.com/web/api/Hooks)

{{< signature "ks, vf, yk, il" >}}

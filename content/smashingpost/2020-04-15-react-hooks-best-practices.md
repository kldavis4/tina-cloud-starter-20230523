---
title: 'Best Practices With React Hooks'
slug: react-hooks-best-practices
author: adeneye-david-abiodun
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/be317534-1fa3-4811-b6ad-386148770f0a/react-hooks-best-practices.png
date: 2020-04-15T11:00:00.000Z
summary: >-
  This article covers the rules of React Hooks and how to effectively start using them in your projects. Please note that in order to follow this article in detail, you will need to know [how to use React Hooks](https://reactjs.org/docs/hooks-intro.html).
description: >-
  This article covers the rules of React Hooks and how to effectively start using them in your projects. Please note that in order to follow this article in detail, you will need to know [how to use React Hooks](https://reactjs.org/docs/hooks-intro.html).
categories:
  - React
  - React Hooks
  - Tools
  - Techniques
---

React Hooks are a new addition in React 16.8 that let you use state and other React features without writing a `class` component. In other words, [Hooks](https://reactjs.org/docs/hooks-intro.html) are functions that let you “hook into” React state and lifecycle features from function components. (They do not work inside `class` components.)

React provides a few built-in Hooks like `useState`. You can also create your own Hooks to reuse stateful behavior between different components. The example below shows a counter whose state is managed using the `useState()` hook. Each time you click on the button, we make use of `setCount()` to update the value of `count` by `1`.

{{< codepen height="480" theme_id="light" slug_hash="QWbXMyM" default_tab="result" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [React Hook example with Counter](https://codepen.io/smashingmag/pen/QWbXMyM) by <a href="https://codepen.io/adeneye-abiodun-david">Adeneye Abiodun David</a>.{{< /codepen >}}

This example renders a counter with a value of `0`. When you click the button, it increments the value by `1`. The initial value of the component is defined using `useState`.

<pre><code class="language-javascript">const [count, setCount] = useState(0)</code></pre>

As you can see, we set that to be `0`. Then we use the `onClick()` method to call `setCount` when we want to increment the value.

<pre><code class="language-javascript">&lt;button onClick={() => setCount(count + 1)}&gt;
  Click me
&lt;/button&gt;</code></pre>

Before the release of React Hooks, this example would have used more lines of code, as we’d have had to make use of a `class` component.

{{% feature-panel %}}

## Rules Of React Hooks

Before we dive deep into the best practices, we need to understand the rules of React Hooks which are also some of the fundamental concepts of the practices presented in this article.

React Hooks are JavaScript functions, but you need to follow two rules when using them.

<ol>
  <li><a href="#call-hooks-top-level">Call Hooks at the top level</a>;</li>
  <li><a href="#call-hooks-react-components">Only call Hooks from React components</a>.</li>
</ol>

**Note**: *These two rules were introduced in React Hooks, as opposed to being part of JavaScript itself.*

Let’s look at these rules in more detail.

## Call Hooks At The Top Level

Don’t call Hooks inside loops, conditions, or nested functions. Always use Hooks at the top level of your React function. By following this rule, you ensure that Hooks are called in the same order each time a component renders. That’s what allows React to correctly preserve the state of Hooks between multiple `useState` and `useEffect` calls.

Let’s make a `Form` component which will have two states:

- `accountName`
- `accountDetail`

These states will have default values, we’ll make use of the `useEffect` hook to persist the state to either the local storage of our browser or to the title of our document.

Now, this component will be maybe to successfully manage its state if it remains the same between multiple calls of `useState` and `useEffect`.

<div class="break-out">

<pre><code class="language-javascript">function Form() {
  // 1. Use the accountName state variable
  const [accountName, setAccountName] = useState('David');

  // 2. Use an effect for persisting the form
  useEffect(function persistForm() {
    localStorage.setItem('formData', accountName);
  });

  // 3. Use the accountDetail state variable
  const [accountDetail, setAccountDetail] = useState('Active');

  // 4. Use an effect for updating the title
  useEffect(function updateStatus() {
    document.title = accountName + ' ' + accountDetail;
  });

  // ...
}</code></pre>
</div>

If the order of our Hooks changes (which can be possible when they are called in loops or conditionals), React will have a hard time figuring out how to preserve the state of our component.

<div class="break-out">

<pre><code class="language-javascript">// ------------
useState('David')           // 1. Initialize the accountName state variable with 'David'
useEffect(persistForm)     // 2. Add an effect for persisting the form
useState('Active')        // 3. Initialize the accountdetail state variable with 'Active'
useEffect(updateStatus)     // 4. Add an effect for updating the status

// -------------
// Second render
// -------------
useState('David')           // 1. Read the accountName state variable (argument is ignored)
useEffect(persistForm)     // 2. Replace the effect for persisting the form
useState('Active')        // 3. Read the accountDetail state variable (argument is ignored)
useEffect(updateStatus)     // 4. Replace the effect for updating the status

// ...</code></pre>
</div>

That’s the order React follows to call our hooks. Since the order remains the same, it will be able to preserve the state of our component. But what happens if we put a Hook call inside a condition?

<div class="break-out">

<pre><code class="language-javascript">// 🔴 We're breaking the first rule by using a Hook in a condition
  if (accountName !== '') {
    useEffect(function persistForm() {
      localStorage.setItem('formData', accountName);
    });
  }</code></pre>
</div>

The `accountName  !==  ''` condition is `true` on the first render, so we run this Hook. However, on the next render the user might clear the form, making the condition `false`. Now that we skip this Hook during rendering, the order of the Hook calls becomes different:

<div class="break-out">

<pre><code class="language-javascript">useState('David')           // 1. Read the accountName state variable (argument is ignored)
// useEffect(persistForm)  // 🔴 This Hook was skipped!
useState('Active')        // 🔴 2 (but was 3). Fail to read the accountDetails state variable
useEffect(updateStatus)     // 🔴 3 (but was 4). Fail to replace the effect</code></pre>
</div>

React wouldn’t know what to return for the second `useState` Hook call. React expected that the second Hook call in this component corresponds to the `persistForm` effect, just like during the previous render &mdash; but it doesn’t anymore. From that point on, every next `Hook` call after the one we skipped would also shift by one &mdash; leading to bugs.

This is why Hooks must be called on the top level of our components. If we want to run an effect conditionally, we can put that condition *inside* our Hook.

**Note**: *Check out the [React Hook docs](https://reactjs.org/docs/hooks-rules.html) to read more on this topic.*

{{% ad-panel-leaderboard %}}

## Only Call Hooks From React Components

Don’t call Hooks from regular JavaScript functions. Instead, you can call Hooks from React function components. Let’s take look at the difference between JavaScript function and React component below:

#### JavaScript Function
 

<pre><code class="language-javascript">import { useState } = "react";

function toCelsius(fahrenheit) {
  const [name, setName] = useState("David");
  return (5/9) * (fahrenheit-32);
}
document.getElementById("demo").innerHTML = toCelsius;</code></pre>

Here we import the `useState` hook from the React package, and then declared our function. But this is invalid as it is not a React component.

#### React Function

<div class="break-out">

<pre><code class="language-javascript">
import React, { useState} from "react";
import ReactDOM from "react-dom";

function Account(props) {
  const [name, setName] = useState("David");
  return &lt;p&gt;Hello, {name}! The price is &lt;b&gt;{props.total}&lt;/b&gt; and the total amount is &lt;b&gt;{props.amount}&lt;/b&gt;&lt;/p&gt;
}
ReactDom.render(
  &lt;Account total={20} amount={5000} /&gt;,
  document.getElementById('root')
);</code></pre>
</div>

Even though the body of both looks similar, the latter becomes a component when we import React into the file. This is what makes it possible for us to use things like [JSX](https://reactjs.org/docs/introducing-jsx.html) and React hooks inside.

If you happened to import your preferred hook without importing React (which makes it a regular function), you will not be able to make use of the Hook you’ve imported as the Hook is accessible only in React component.

### Call Hooks From Custom Hooks   
    
A custom Hook is a JavaScript function whose name starts with `use` and that may call other Hooks. For example, `useUserName` is used below a custom Hook that calls the `useState` and `useEffect` hooks. It fetches data from an API, loops through the data, and calls `setIsPresent()` if the specific username it received is present in the API data.

<pre><code class="language-javascript">export default function useUserName(userName) {
  const [isPresent, setIsPresent] = useState(false);
  
  useEffect(() => {
    const data = MockedApi.fetchData();
    data.then((res) => {
      res.forEach((e) => {
        if (e.name === userName) {
          setIsPresent(true);
        }
     });
    });
  });
    
  return isPresent;
}</code></pre>

We can then go on to reuse the functionality of this hook in other places where we need such in our application. In such places, except when needed, we don’t have to call `useState` or `useEffect` anymore.

By following this rule, you ensure that all stateful logic in a component is clearly visible from its source code.

### ESLint Plugin

ESLint plugin called [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) enforces the rules above. This comes in handy in enforcing the rules when working on a project. I suggest you make use of this plugin when working on your project, especially when working with others. You can add this plugin to your project if you’d like to try it:

<div class="break-out">

<pre><code class="language-javascript">// Your ESLint configuration
{
  "plugins": [
    // ...
    "react-hooks"
  ],
  "rules": {
    // ...
    "react-hooks/rules-of-hooks": "error", // Checks rules of Hooks
    "react-hooks/exhaustive-deps": "warn" // Checks effect dependencies
  }
}</code></pre>
</div>

This plugin is included by default in [Create React App](https://reactjs.org/docs/create-a-new-react-app.html#create-react-app). So you don’t need to add it if you bootstrap your React applications using Create-React-App.


## Thinking In Hooks

Let’s take a brief look at `class` components and functional components (with Hooks), before diving into the few Hooks best practices.

The simplest way to define a component in React is to write a JavaScript function that returns a React element:

<pre><code class="language-javascript">function Welcome(props) {
  return &lt;h1&gt;Hello, {props.name}&lt;/h1&gt;;
}</code></pre>

The `Welcome` component accepts `props` which is an object that contains data and returns a React element. We can then import and render this component in another component.

The `class` component uses a programming methodology called **Encapsulation** which basically means that everything relevant to the class component will live within it. Life-cycle methods (`constructors`, `componentDidMount()`, `render`, and so on) give components a predictable structure.

Encapsulation is one of the fundamentals of OOP (**O**bject-**O**riented **P**rogramming). It refers to the bundling of data within the methods that operate on that data, and is used to hide the values or state of a structured data object inside a class &mdash; preventing unauthorized parties’ direct access to them.

With Hooks, the composition of a component changes from being a combination of life-cycle Hooks &mdash; to functionalities with some render at the end.

### Function Component

The example below shows how custom Hooks can be used in a functional component (without showcasing what the body is). However, what it does or can do is not limited. It could be instantiating state variables, consuming contexts, subscribing the component to various side effects &mdash; or all of the above if you’re using a custom hook!

<pre><code class="language-javascript">function {
  useHook{...};
  useHook{...};
  useHook{...};
  return (
    <div>...</div>
  );
}</code></pre>

### Class Component

A `class` component requires you to extend from `React.Component` and create a `render` function which returns a React element. This requires more code but will also give you some benefits.

<pre><code class="language-javascript">class {
  constructor(props) {...}
  componentDidMount() {...}
  componentWillUnmount() {...}
  render() {...}
}</code></pre>

There are some benefits you get by using functional components in React:

1. It will get easier to separate container and presentational components because you need to think more about your component’s state if you don’t have access to `setState()` in your component.
2. Functional components are much **easier to read and test** because they are plain JavaScript functions without state or lifecycle-hooks.
3. You end up with **less code.**
4. The React team [mentioned](https://reactjs.org/blog/2015/10/07/react-v0.14.html#stateless-functional-components) that there may be a **performance** boost for functional components in future React versions.

This leads to the first best practice when using React Hooks.

{{% ad-panel-leaderboard %}}

## Hooks Best Practices

### 1. Simplify Your Hooks

Keeping React Hooks simple will give you the power to effectively control and manipulate what goes on in a component throughout its lifetime. **Avoid writing custom Hooks as much as possible**; you can inline a `useState()` or `useEffect()` instead of creating your own hook.

If you find yourself making use of a bunch of custom Hooks that are related in functionality, you can create a custom hook that acts as a wrapper for these. Let’s take a look at two different functional components with hooks below.

#### Functional Component v1

<pre><code class="language-javascript">function {
  useHook(...);
  useHook(...);
  useHook(...);
  return(
    &lt;div&gt;...&lt;/div&gt;
  );
}</code></pre>

#### Functional Component v2

<pre><code class="language-javascript">function {
  useCustomHook(...);
    useHook(...);
    useHook(...);
  return(
    &lt;div&gt;...&lt;/div&gt;
  );
}</code></pre>

v2 is a better version because it keeps the hook simple and all other `useHook`s are inline accordingly. This allows us to create functionality that can be reused across different components and also gives us more power to control and manipulate our components effectively. Instead of adopting v1 in which our components are littered with Hooks, you should make use of v2 which will make debugging easy and your code cleaner.

### 2. Organize And Structure Your Hooks

One of the advantages of React Hooks is the ability to write less code that is easy to read. In some cases, the amount of `useEffect()` and `useState()` can still be confusing. When you keep your component organized it will help in readability and keep the flow of your components consistent and predictable. If your custom Hooks are too complicated, you can always break them down to sub-custom Hooks. Extract the logic of your component to custom Hooks to make your code readable.

### 3. Use React Hooks Snippets

React Hooks Snippets is a Visual Studio Code extension to make React Hooks easier and faster. Currently, five hooks are supported:

- `useState()`
- `useEffect()`
- `useContext()`
- `useCallback()`
- `useMemo()`

Other snippets have also been added. I have tried working with these Hooks and it has been one of the best practices I’ve personally used while working with them.

There are two ways you can add React Hooks snippets to your project:

1. **Command**  
Launch the VS Code Quick open (<kbd>Ctrl</kbd>+<kbd>P</kbd>), paste `ext install ALDuncanson.react-hooks-snippets` and press <kbd>Enter</kbd>.  
2. **Extension Marketplace**  
Launch ‘VS Code Extension Marketplace’ (<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>X</kbd>) and search for ‘React Hook Snippets’. Then, look for the ‘Alduncanson’ icon.

I recommend the first snippet. Read more about the snippets [here](https://marketplace.visualstudio.com/items?itemName=AlDuncanson.react-hooks-snippets) or check for the lastest Hooks snippets [here](https://marketplace.visualstudio.com/).

### 4. Put Hooks Rules Into Consideration

Endeavor to always put the two rules of Hooks we learned earlier into consideration while working with React Hooks. 

- Only call your Hooks at the top level. Don’t call Hooks inside loops, conditions or nested functions.
- Always call Hooks from React function components or from custom Hooks, don’t call Hooks from regular JavaScript functions.

The ESlint plugin called [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) enforces these two rules, you can add this plugin to your project if you’d like it as we explain above in rules of hooks section.

Best practices have not been fully resolved because Hooks are still relatively new. So adoption should be taken with precaution one would take in adopting in any early technology. With that in mind, Hooks are the way for the future of React.

## Conclusion

I hope you enjoyed this tutorial. We’ve learned the two most important rules of React Hooks and how to effectively think in Hooks. We looked at functional components and some best practices in writing Hooks the right and effective way. As brief as the rules are, it’s important to make them your guiding compass when writing rules. If you are prone to forget it, you can make use of the ESLint plugin to enforce it.

I hope you will take all of the lessons learned here in your next React project. Good luck!

### Resources

- “[Introducing Hooks](https://reactjs.org/docs/hooks-intro.html),” React Docs
- “[Functional vs Class-Components In React](https://medium.com/@Zwenza/functional-vs-class-components-in-react-231e3fbd7108),” David Jöch, Medium
- “[Mixins Considered Harmful](https://reactjs.org/blog/2016/07/13/mixins-considered-harmful.html),” Dan Abramov, React Blog
- “[React Hooks: Best Practices And A Shift In Mindset](https://medium.com/@bryanmanuele/react-hooks-best-practices-a-shift-in-mindset-8fd0e58e4b0b),” Bryan Manuele, Medium
- “[React Hooks Snippets For VS Code](https://marketplace.visualstudio.com/items?itemName=antmdvs.vscode-react-hooks-snippets),” Anthony Davis, Visual Code Marketplace

{{< signature "ks, ra, yk, il" >}}

---
title: 'Higher-Order Components In React'
slug: higher-order-components-react
author: shedrack-akintayo
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d4ff5e1d-de3d-4499-9d4e-53a420bc75bb/higher-order-components-react.png
date: 2020-06-08T12:00:00.000Z
summary: >-
  In this tutorial, we are going to learn about higher-order components, the syntax of higher-order components, as well as use cases for them. In the process, we will build a higher-order component from an existing React component. By the end of this tutorial, you will understand the basics of higher-order components and how to build them.
description: >-
  In this tutorial, we are going to learn about higher-order components, the syntax of higher-order components, as well as use cases for them. In the process, we will build a higher-order component from an existing React component.
categories:
  - React
  - Redux
  - Tools
  - JavaScript
---

Higher-order components (HOCs) in React were inspired by higher-order functions in JavaScript. A HOC is an advanced technique for reusing logic in React components. It is a pattern created out of React’s compositional nature.

HOCs basically incorporate the don’t-repeat-yourself (DRY) principle of programming, which you’ve most likely come across at some point in your career as a software developer. It is one of the best-known principles of software development, and observing it is very important when building an application or writing code in general.

In this tutorial, we will learn what a HOC is, its basic structure, some use cases, and finally an example.

**Note:** *Basic knowledge of React and JavaScript will come in handy as you work through this tutorial.*

<div class="c-felix-the-cat">
<h4 class="h3">Best React Practices</h4>
<p>React is a fantastic JavaScript library for building rich user interfaces. It provides a great component abstraction for organizing your interfaces into well-functioning code, and there’s just about anything you can use it for. <a href="https://www.smashingmagazine.com/category/react" class="btn btn--medium btn--blue">Read a related article on React&nbsp;&rarr;</a></p>
</div>

{{% feature-panel %}}

## Higher-Order Functions In JavaScript

Before jumping into HOCs in React, let’s briefly discuss higher-order functions in JavaScript. Understanding them is critical to understanding our topic of focus.

Higher-order functions in JavaScript take some functions as arguments and return another function. They enable us to abstract over **actions**, not just values, They come in several forms, and they help us to write less code when operating on functions and even arrays. 

The most interesting part of using higher-order functions is composition. We can write small functions that handle one piece of logic. Then, we can compose complex functions by using the different small functions we have created. This reduces bugs in our code base and makes our code much easier to read and understand.

JavaScript has some of these functions already built in. Some examples of higher-order functions are the following:

- `.forEach()`  
This iterates over every element in an array with the same code, but does not change or mutate the array, and it returns undefined.
- `.map()`  
This method transforms an array by applying a function to all of its elements, and then building a new array from the returned values.
- `.reduce()`  
This method executes a provided function for each value of the array (from left to right).
- `.filter()`  
This checks every single element in an array to see whether it meets certain criteria as specified in the `filter` method, and then it returns a new array with the elements that match the criteria.

So many higher-order functions are built into JavaScript, and you can make your own custom ones. 

### An Example Of Custom Higher-Order Function

Suppose we are asked to write a function that formats integers as currencies, including some customization of specifying the currency symbol and adding a decimal separator for the currency amount. We can write a higher-other function that takes the currency symbol and also the decimal separator. This same function would then format the value passed to it with the currency symbol and decimal operators. We would name our higher-order function `formatCurrency`.

<pre><code class="language-javascript">const formatCurrency = function( 
    currencySymbol,
    decimalSeparator  ) {
    return function( value ) {
        const wholePart = Math.trunc( value / 100 );
        let fractionalPart = value % 100;
        if ( fractionalPart < 10 ) {
            fractionalPart = '0' + fractionalPart;
        }
        return `${currencySymbol}${wholePart}${decimalSeparator}${fractionalPart}`;
    }
}
</code></pre>

`formatCurrency` returns a function with a fixed currency symbol and decimal separator.

We then pass the formatter a value, and format this value with the function by extracting its whole part and the fractional part. The returned value of this function is constructed by a template literal, concatenating the currency symbol, the whole part, the decimal separator, and the fractional part.

Let’s use this higher-order function by assigning a value to it and seeing the result.

<pre><code class="language-javascript">> getLabel = formatCurrency( '$', '.' );
 
> getLabel( 1999 )
"$19.99" //formatted value
 
> getLabel( 2499 )
"$24.99" //formatted value
</code></pre> 
 
You might have noticed that we created a variable named `getLabel`, then assigned our `formatCurrency` higher-order function, and then passed the currency formatters to the function, which is the currency symbol and a decimal separator.  To make use of the function, we call `getLabel`, which is now a function, and we pass in the value that needs to be formatted. That’s all! We have created a custom higher order of our choice.

## What Is A Higher-Order Component?

A higher-order component (HOC) is an advanced element for reusing logic in React components. Components take one or more components as arguments, and return a new upgraded component. Sounds familiar, right? They are similar to higher-order functions, which take some functions as an argument and produce a new function.

HOCs are commonly used to design components with certain shared behavior in a way that makes them connected differently than normal state-to-props pattern. 

### Facts About HOCs

1. We don’t modify or mutate components. We create new ones.
2. A HOC is used to compose components for code reuse.
3. A HOC is a pure function. It has no side effects, returning only a new component.

Here are some examples of real-world HOCs you might have come across:

<table class="tablesaw" data-tablesaw-mode="stack" data-tablesaw-minimap>
  <tbody>
    <tr>
      <td>react-redux </td>
      <td><code>connect(mapStateToProps, mapDispatchToProps)(UserPage)</code></td>
    </tr>
    <tr>
      <td>react-router</td>
      <td><code>withRouter(UserPage)</code></td>
    </tr>
    <tr>
      <td>material-ui</td>
      <td><code>withStyles(styles)(UserPage)</code></td>
    </tr>
  </tbody>
</table>

## Structure Of A Higher-Order Component

A HOC is structured like a higher-order function:

- It is a component.
- It takes another component as an argument.
- Then, it returns a new component.
- The component it returns can render the original component that was passed to it.

The snippet below shows how a HOC is structured in React:

<pre><code class="language-javascript">
import React from 'react';
// Take in a component as argument WrappedComponent
const higherOrderComponent = (WrappedComponent) =&gt; {
// And return another component
  class HOC extends React.Component {
    render() {
      return &lt;WrappedComponent /&gt;;
    }
  }
  return HOC;
};
</code></pre>

We can see that `higherOrderComponent` takes a component (`WrappedComponent`) and returns another component inside of it. With this technique, whenever we need to reuse a particular component’s logic for something, we can create a HOC out of that component and use it wherever we like.

{{% ad-panel-leaderboard %}}

## Use Cases

In my experience as a front-end engineer who has been writing React for a while now, here are some use cases for HOCs.

**Show a loader while a component waits for data**

Most of the time, when building a web application, we would need to use a loader of some sort that is displayed while a component is waiting for data to be passed to its props. We could easily use an in-component solution to render the loader, which would work, but it wouldn’t be the most elegant solution. Better would be to write a common HOC that can track those props; and while those props haven’t been injected or are in an empty state, it can show a loading state.

To explain this properly, let’s build a list of categories of public APIs, using its open API. We tend to handle list-loading, so that our clients don’t panic when the API we are getting data from takes so much time to respond.

Let’s generate a React app:

<pre><code class="language-bash">npx create-react-app repos-list
</code></pre>

A basic list component can be written as follows: 

<pre><code class="language-javascript">//List.js
import React from 'react';
const List = (props) =&gt; {
  const { repos } = props;
  if (!repos) return null;
  if (!repos.length) return &lt;p&gt;No repos, sorry&lt;/p&gt;;
  return (
    &lt;ul&gt;
      {repos.map((repo) =&gt; {
        return &lt;li key={repo.id}&gt;{repo.full_name}&lt;/li&gt;;
      })}
    &lt;/ul&gt;
  );
};
export default List;
</code></pre> 

The code above is a list component. Let’s break down the code into tiny bits so that we can understand what is happening.

<pre><code class="language-javascript">const List = (props) => {};
</code></pre>

Above, we initialize our functional component, named `List`, and pass props to it.

<pre><code class="language-javascript">const { repos } = props;
</code></pre>

Then, we create a constant, named `repos`, and pass it to our component props, so that it can be used to modify our component.

<pre><code class="language-javascript">if (!repos) return null;
if (!repos.length) return &lt;p&gt;No repos, sorry&lt;/p&gt;;
</code></pre>

Above, we are basically saying that, if after fetching has completed and the `repos` prop is still empty, then it should return `null`. We are also carrying out a conditional render here: If the length of the `repos` prop is still empty, then it should render “No repos, sorry” in our browser.

<pre><code class="language-javascript">return (
    &lt;ul&gt;
      {repos.map((repo) =&gt; {
        return &lt;li key={repo.id}&gt;{repo.full_name}&lt;/li&gt;;
      })}
    &lt;/ul&gt;
  );
</code></pre>

Here, we are basically mapping through the `repos` array and returning a list of repos according to their full names, with a unique key for each entry.

Now, let’s write a HOC that handles loading, to make our users happy.

<pre><code class="language-javascript">//withdLoading.js
import React from 'react';
function WithLoading(Component) {
  return function WihLoadingComponent({ isLoading, ...props }) {
    if (!isLoading) return &lt;Component {...props} /&gt;;
    return &lt;p&gt;Hold on, fetching data might take some time.&lt;/p&gt;;
  };
}
export default WithLoading;
</code></pre>

This would display the text “Hold on, fetching data might take some time” when the app is still fetching data and the props are being injected into state. We make use of `isLoading` to determine whether the component should be rendered.

Now, in your `App.js` file, you could pass the `loading` logic to `WithLoading`, without worrying about it in your `List` .

<pre><code class="language-javascript">import React from 'react';
import List from './components/List.js';
import WithLoading from './components/withLoading.js';
const ListWithLoading = WithLoading(List);
class App extends React.Component {
  state = {
{
  };
  componentDidMount() {
    this.setState({ loading: true });
    fetch(`https://api.github.com/users/hacktivist123/repos`)
      .then((json) => json.json())
      .then((repos) => {
        this.setState({ loading: false, repos: repos });
      });
  }
  render() {
    return (
      &lt;ListWithLoading
        isLoading={this.state.loading}
        repos={this.state.repos}
      /&gt;
    );
  }
}
export default App;
</code></pre>

The code above is our entire app. Let’s break it down to see what is happening.

<pre><code class="language-javascript">class App extends React.Component {
  state = {
    loading: false,
    repos: null,
  };
  componentDidMount() {
    this.setState({ loading: true });
    fetch(`https://api.github.com/users/hacktivist123/repos`)
      .then((json) => json.json())
      .then((repos) => {
        this.setState({ loading: false, repos: repos });
      });
  }
</code></pre>

All we are doing here is creating a class component named `App()`, then initializing state with two properties, `loading: false,` and  `repos: null,`. The initial state of `loading` is `false`, while the initial state of repos is also `null`.

Then, when our component is mounting, we set the state of the `loading` property to `true`, and immediately make a fetch request to the API URL that holds the data we need to populate our `List` component. Once the request is complete, we set the `loading` state to `false` and populate the `repos` state with the data we have pulled from the API request.

<pre><code class="language-javascript">const ListWithLoading = WithLoading(List);
</code></pre>

Here, we create a new component named `ListWithLoading` and pass the `WithLoading` HOC that we created and also the `List` component in it.

<pre><code class="language-javascript">render() {
    return (
      &lt;ListWithLoading
        isLoading={this.state.loading}
        repos={this.state.repos}
      /&gt;
    );
  }
</code></pre>

Above, we render the `ListWithLoading` component, which has been supercharged by the `WithLoading` HOC that we created and also the `List` component in it. Also, we pass the `loading` state’s value and the `repos` state’s value as props to the component.

Because the page is still trying to pull data from the API, our HOC will render the following text in the browser.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2ba009f-0ccd-45ca-8101-d6bde27cc5f9/higher-order-components-react-app-loading-state.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2ba009f-0ccd-45ca-8101-d6bde27cc5f9/higher-order-components-react-app-loading-state.png" sizes="100vw" caption="App loading state (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a2ba009f-0ccd-45ca-8101-d6bde27cc5f9/higher-order-components-react-app-loading-state.png'>Large preview</a>)" alt="" >}}

When loading is done and the props are no longer in an empty state, the repos will be rendered to the screen.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fc19907-0e16-423a-94ac-5025e2a249ff/higher-order-components-react-app-loading-finished-state.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fc19907-0e16-423a-94ac-5025e2a249ff/higher-order-components-react-app-loading-finished-state.png" sizes="100vw" caption="App loading’s finished state (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9fc19907-0e16-423a-94ac-5025e2a249ff/higher-order-components-react-app-loading-finished-state.png'>Large preview</a>)" alt="" >}}

### Conditionally Render Components

Suppose we have a component that needs to be rendered only when a user is authenticated — it is a protected component. We can create a HOC named `WithAuth()` to wrap that protected component, and then do a check in the HOC that will render only that particular component if the user has been authenticated.

A basic `withAuth()` HOC, according to the example above, can be written as follows:

<pre><code class="language-javascript">// withAuth.js
import React from "react";
export function withAuth(Component) {
    return class AuthenticatedComponent extends React.Component {
        isAuthenticated() {
            return this.props.isAuthenticated;
        }

        /**
         * Render
         */
        render() {
            const loginErrorMessage = (
                &lt;div&gt;
                    Please &lt;a href="/login"&gt;login&lt;/a&gt; in order to view this part of the application.
                &lt;/div&gt;
            );

            return (
                &lt;div&gt;
                    { this.isAuthenticated === true ? &lt;Component {...this.props} /&gt; : loginErrorMessage }
                &lt;/div&gt;
            );
        }
    };
}

export default withAuth;
</code></pre>

The code above is a HOC named `withAuth`. It basically takes a component and returns a new component, named `AuthenticatedComponent`, that checks whether the user is authenticated. If the user is not authenticated, it returns the `loginErrorMessage` component; if the user is authenticated, it returns the wrapped component. 

**Note:** `this.props.isAuthenticated` has to be set from your application’s logic. (Or else use react-redux to retrieve it from the global state.)
 
To make use of our HOC in a protected component, we’d use it like so:
 

<pre><code class="language-javascript">// MyProtectedComponent.js
import React from "react";
import {withAuth} from "./withAuth.js";

export class MyProectedComponent extends React.Component {
    /**
     * Render
     */
    render() {
        return (
            &lt;div&gt;
                This is only viewable  by authenticated users.
            &lt;/div&gt;
        );
    }
}

// Now wrap MyPrivateComponent with the requireAuthentication function 
export default withAuth(MyPrivateComponent);
</code></pre>

Here, we create a component that is viewable only by users who are authenticated. We wrap that component in our `withAuth` HOC to protect the component from users who are not authenticated.

### Provide Components With Specific Styling

Continuing the use case above, based on whatever UI state you get from the HOC, you can render specific styles for specific UI states. For example, if the need arises in multiple places for styles like `backgroundColor`, `fontSize` and so on, they can be provided via a HOC by wrapping the component with one that just injects props with the specific `className`.

Take a very simple component that renders “hello” and the name of a person. It takes a `name` prop and some other prop that can affect the rendered JavaScript XML (JSX).

<pre><code class="language-javascript">// A simple component 
const HelloComponent = ({ name, ...otherProps }) =&gt; (
 &lt;div {...otherProps}&gt;Hello {name}!/div&gt;
);
</code></pre>

Let’s create a HOC named `withStyling` that adds some styling to the “hello” text.

<pre><code class="language-javascript">const withStyling = (BaseComponent) =&gt; (props) =&gt; (
  &lt;BaseComponent {...props} style={{ fontWeight: 700, color: 'green' }} /&gt;
);
</code></pre>

In order to make use of the HOC on our `HelloComponent`, we wrap the HOC around the component. We create a pure component, named `EnhancedHello`, and assign the HOC and our `HelloComponent`, like so :

<pre><code class="language-javascript">const EnhancedHello = withStyling(HelloComponent);
</code></pre>

To make a change to our `HelloComponent`, we render the `EnhancedHello` component: 

<pre><code class="language-javascript">&lt;EnhancedHello name='World' /&gt;
</code></pre>

Now, the text in our `HelloComponent` becomes this:

<pre><code class="language-javascript">&lt;div style={{fontWeight: 700, color: 'green' }}&gt;Hello World&lt;/div&gt;
</code></pre>

### Provide A Component With Any Prop You Want

This is a popular use case for HOCs. We can study our code base and note what reusable prop is needed across components. Then, we can have a wrapper HOC to provide those components with the reusable prop.

Let’s use the example above:

<pre><code class="language-javascript">// A simple component 
const HelloComponent = ({ name, ...otherProps }) => (
 &lt;div {...otherProps}&gt;Hello {name}!&lt;/div&gt;
);
</code></pre>

Let’s create a HOC named `withNameChange` that sets a `name` prop on a base component to “New Name”.

<pre><code class="language-javascript">const withNameChange = (BaseComponent) =&gt; (props) =&gt; (
  &lt;BaseComponent {...props} name='New Name' /&gt;
);
</code></pre>

In order to use the HOC on our `HelloComponent`, we wrap the HOC around the component, create a pure component named `EnhancedHello2`, and assign the HOC and our `HelloComponent` like so:

<pre><code class="language-javascript">const EnhancedHello2 = withNameChange(HelloComponent);
</code></pre>

To make a change to our `HelloComponent`, we can render the `EnhancedHello` component like so: 

<pre><code class="language-javascript">&lt;EnhancedHello /&gt;
</code></pre>

Now, the text in our `HelloComponent` becomes this:

<pre><code class="language-javascript">&lt;div&gt;Hello New World&lt;/div&gt;
</code></pre>

To change the `name` prop, all we have to do is this:

<pre><code class="language-javascript">&lt;EnhancedHello name='Shedrack' /&gt;
</code></pre> 

The text in our `HelloComponent` becomes this:

<pre><code class="language-javascript">&lt;div&gt;Hello Shedrack&lt;/div&gt;
</code></pre>

{{% ad-panel-leaderboard %}}

## Let’s Build A Higher-Order Component

In this section, we will build a HOC that takes a component that has a `name` prop, and then we will make use of the `name` prop in our HOC.

So, generate a new React app with  `create-react-app`, like so:

<pre><code class="language-bash">npx create-react-app my-app
</code></pre>

After it is generated, replace the code in your `index.js` file with the following snippet.

<div class="break-out">

 <pre><code class="language-javascript">import React from 'react';
import { render } from 'react-dom';
const Hello = ({ name }) =&gt;
  &lt;h1&gt;
    Hello {name}!
  &lt;/h1&gt;;

function withName(WrappedComponent) {
  return class extends React.Component {
    render() {
      return &lt;WrappedComponent name="Smashing Magazine" {...this.props} /&gt;;
    }
  };
}
const NewComponent = withName(Hello);
const App = () =&gt;
  &lt;div&gt;
    &lt;NewComponent /&gt;
  &lt;/div&gt;;
render(&lt;App /&gt;, document.getElementById('root'));
</code></pre>
</div>

Once you have replaced the code in your `index.js` file, you should see the following on your screen:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e58503d-6d3a-4ea6-b178-d365fb1038ff/higher-order-components-react-react-app.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e58503d-6d3a-4ea6-b178-d365fb1038ff/higher-order-components-react-react-app.png" sizes="100vw" caption="Our React app (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2e58503d-6d3a-4ea6-b178-d365fb1038ff/higher-order-components-react-react-app.png'>Large preview</a>)" alt="" >}}

Let’s go through the snippet bit by bit.

<pre><code class="language-javascript">const Hello = ({ name }) =>
  &lt;h1&gt;
    Hello {name}!
  &lt;/h1&gt;;
</code></pre>

Here, we create a functional component that has a prop called `name`. In this functional component, we render the “Hello” and the value of the `name` prop in an `h1` tag. 

<pre><code class="language-javascript">function withName(WrappedComponent) {
  return class extends React.Component {
    render() {
      return &lt;WrappedComponent name="Smashing Magazine" {...this.props} /&gt;;
    }
  };
}
</code></pre>

Above, we create a higher-order functional component named `withName()`. Then, we return an anonymous class component inside that renders the component wrapped in the HOC. And we assign a value to the prop of the wrapped component. 

<pre><code class="language-javascript">const NewComponent = withName(Hello);
</code></pre>

Here, we create a new component named `NewComponent`. We use the HOC that we created, and assign to it the functional component that we created at the start of the code base, named `hello`.

<pre><code class="language-javascript">const App = () =&gt;
  &lt;div&gt;
    &lt;NewComponent /&gt;
  &lt;/div&gt;;
render(&lt;App /&gt;, document.getElementById('root'));
</code></pre>

All we are doing above is creating another functional component, named `App`. It renders the `NewComponent` that we upgraded with our HOC in a `div`. Then, we use the react-dom function `render` to display the component in the browser.

That’s all we need to do! Our `withName` function takes a component as an argument and returns a HOC. A few months from now, if we decide to change things around, we only have to edit our HOC.

## Conclusion

I hope you’ve enjoyed working through this tutorial. You can read more about higher-order components in the references listed below. If you have any questions, leave them in the comments section below. I’ll be happy to answer every one.

### Resources And References

- “[Higher-Order Functions](https://eloquentjavascript.net/05_higher_order.html)”, Eloquent JavaScript, Marijn Haverbeke
- “[Introduction to Higher-Order Components (HOCs) in React](https://dev.to/ogwurujohnson/introduction-to-higher-order-components-hocs-in-react-273f)”, Johnson Ogwuru
- “[React Higher-Order Components](https://tylermcginnis.com/react-higher-order-components/)”, Tyler McGinnis
- “[Simple Explanation of Higher-Order Components (HOCs)](https://blog.jakoblind.no/simple-explanation-of-higher-order-components-hoc/)”, Jakob Lind
- “[A Quick Intro to React’s Higher-Order Components](https://alligator.io/react/higher-order-components/)”, Patrick Moriarty, Alligator.io
- “[Higher-Order Functions in JavaScript](https://www.zsoltnagy.eu/higher-order-functions-in-javascript/)”, Zslot Nagy

{{< signature "ks, ra, il, al" >}}

---
title: 'Mastering Props And PropTypes In React'
slug: mastering-props-proptypes-react
author: adeneye-david-abiodun
date: 2020-08-17T10:30:00.000Z
summary: >-
  Props and PropTypes are an important mechanism for passing information between React components, and we’re going to look into them in great detail here. This tutorial will introduce you to the details about props, passing and accessing props, and passing information to any component using props. However, it’s always a good practice to validate the data we are getting through props by using PropTypes. So, you will also learn how to integrate PropTypes in React.
description: >-
  Props and PropTypes are an important mechanism for passing information between React components, and in this article, we’re going to look into them in great detail.
categories:
  - React
  - Apps
  - JavaScript
---

Do props and PropTypes confuse you? You’re not alone. I’m going to guide you through everything about props and PropTypes. They can make your life significantly easier when developing React apps. This tutorial will introduce you to the details about props, passing and accessing props, and passing information to any component using props.

Building React applications involves breaking down the UI into several components, which implies that we will need to pass data from one component to another. Props are an important mechanism for passing information between React components, and we’re going to look into them in great detail. This article would be incomplete without looking into PropTypes, because they ensure that components use the correct data type and pass the right data.

It’s always a good practice to validate the data we get as props by using PropTypes. You will also learn about integrating PropTypes in React, typechecking with PropTypes, and using defaultProps. At the end of this tutorial, you will understand how to use props and PropTypes effectively. It is important that you already have basic knowledge of how [React works](https://reactjs.org/docs/thinking-in-react.html).

## Understanding Props

React allows us to pass information to components using things called props (short for properties). Because React comprises several components, props make it possible to share the same data across the components that need them. It makes use of one-directional data flow (parent-to-child components). However, with a callback function, it’s possible to pass props back from a child to a parent component.

These data can come in different forms: numbers, strings, arrays, functions, objects, etc. We can pass props to any component, just as we can declare attributes in any HTML tag. Take a look at the code below:

<pre><code class="language-html">&lt;PostList posts={postsList} /&gt;
</code></pre>

In this snippet, we are passing a prop named `posts` to a component named `PostList`. This prop has a value of `{postsList}`. Let’s break down how to access and pass data.

{{% feature-panel %}}

### Passing and Accessing Props

To make this tutorial interesting,  let’s create an application that shows a list of users’ names and posts. The app demo is shown below:

{{< codepen height="480" theme_id="light" slug_hash="MWyKQpd" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Passing and Accessing Props](https://codepen.io/smashingmag/pen/MWyKQpd) by <a href="https://codepen.io/davidadeneye">David Adeneye</a>.{{< /codepen >}}

The app comprises collections of components: an `App` component, a `PostList` component, and a `Post` component**.**

The list of posts will require data such as the `content` and the `name` of the user. We can construct the data like so:

<pre><code class="language-css">const postsList = [
  {
    id: 1,
    content: "The world will be out of the pandemic soon",
    user: "Lola Lilly",
  },
  {
    id: 2,
    content: "I'm really exited I'm getting married soon",
    user: "Rebecca Smith",
  },
  {
    id: 3,
    content: "What is your take on this pandemic",
    user: "John Doe",
  },
  {
    id: 4,
    content: "Is the world really coming to an end",
    user: "David Mark",
  },
];
</code></pre>

After this, we need the `App` component to pull the data, Here is the basic structure of that component:

<pre><code class="language-html">const App = () =&gt; {
  return (
    &lt;div&gt;
      &lt;PostList posts={postsList} /&gt;
    &lt;/div&gt;
  );
};
</code></pre>

Here, we are passing an array of posts as a prop to the `PostList` (which we’ll create in a bit). The parent component, `PostList`, will access the data in `postsList`, which will be passed as `posts` props to the child component (`Post`). If you’ll remember, our app comprises three components, which we’ll create as we proceed.

Let’s create the `PostList`:

<pre><code class="language-html">class PostList extends React.Component {
  render() {
    return (
      &lt;React.Fragment&gt;
        &lt;h1&gt;Latest Users Posts&lt;/h1&gt;
        &lt;ul&gt;
          {this.props.posts.map((post) =&gt; {
            return (
              &lt;li key={post.id}&gt;
                &lt;Post {...post} /&gt;
              &lt;/li&gt;
            );
          })}
        &lt;/ul&gt;
      &lt;/React.Fragment&gt;
    );
  }
}
</code></pre>

The `PostList` component will receive `posts` as its prop. It will then loop through the `posts` prop, `this.props.posts`, to return each posted item as a `Post` component (which we will model later). Also, note the use of the `key` in the snippet above. For those new to React, a [key](https://reactjs.org/docs/lists-and-keys.html) is a unique identifier assigned to each item in our list, enabling us to distinguish between items. In this case, the key is the `id` of each post. There’s no chance of two items having the same `id`, so it’s a good piece of data to use for this purpose.

Meanwhile, the remaining properties are passed as props to the `Post` component ( `<Post {...post} />` ).

So, let’s create the `Post` component and make use of the props in it:

<pre><code class="language-html">const Post = (props) =&gt; {
  return (
    &lt;div&gt;
      &lt;h2&gt;{props.content}&lt;/h2&gt;
      &lt;h4&gt;username: {props.user}&lt;/h4&gt;
    &lt;/div&gt;
  );
};
</code></pre>

We are constructing the `Post` component as a functional component, rather than defining it as a class component like we did for the `PostList` component. I did this to show you how to access props in a functional component, compared to how we access them in a class component with `this.props`**.** Because this a functional component, we can access the values using `props`**.**

We’ve learned now how to pass and access props, and also how to pass information from one component to the other. Let’s consider now how props work with functions.

{{% ad-panel-leaderboard %}}

### Passing Functions Via Props

In the preceding section, we passed an array of data as props from one component to another. But what if we are working with functions instead? React allows us to pass functions between components. This comes in handy when we want to trigger a state change in a parent component from its child component. Props are supposed to be immutable; you should not attempt to change the value of a prop. You have to do that in the component that passes it down, which is the parent component.

Let’s create a simple demo app that listens to a click event and changes the state of the app. To change the state of the app in a different component, we have to pass down our function to the component whose state needs to change. In this way, we will have a function in our child component that is able to change state.

Sounds a bit complex? I have created a simple React application that changes state with the click of a button and renders a piece of welcome information:

{{< codepen height="480" theme_id="light" slug_hash="WNwrMEY" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Passing Function via Props in React](https://codepen.io/smashingmag/pen/WNwrMEY) by <a href="https://codepen.io/davidadeneye">David Adeneye</a>.{{< /codepen >}}

In the demo above, we have two components. One is the `App` component, which is the parent component that contains the app’s state and the function to set the state. The `ChildComponent` will be the child in this scenario, and its task is to render the welcome information when the state changes.

Let’s break this down into code:

<pre><code class="language-css">class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isShow: true,
    };
  }
  toggleShow = () =&gt; {
    this.setState((state) =&gt; ({ isShow: !state.isShow }));
  };
  render() {
    return (
      &lt;div&gt;
        &lt;ChildComponent isShow={this.state.isShow} clickMe={this.toggleShow} /&gt;
      &lt;/div&gt;
    );
  }
}
</code></pre>

Notice that we’ve set our state to `true`, and the method to change the state is created in the `App` component. In the `render()` function, we pass the state of the app, as the prop `isShow`, to the `ChildComponent` component. We also pass the `toggleShow()` function as a prop named `clickMe`.

We will use this in the `ChildComponent` which looks like this:

<pre><code class="language-css">class ChildComponent extends React.Component {
  clickMe = () =&gt; {
    this.props.clickMe();
  };
  render() {
    const greeting = "Welcome to React Props";
    return (
      &lt;div style={{ textAlign: "center", marginTop: "8rem" }}&gt;
        {this.props.isShow ? (
          &lt;h1 style={{ color: "green", fontSize: "4rem" }}&gt;{greeting}&lt;/h1&gt;
        ) : null}
        &lt;button onClick={this.clickMe}&gt;
          &lt;h3&gt;click Me&lt;/h3&gt;
        &lt;/button&gt;
      &lt;/div&gt;
    );
  }
}
</code></pre>

The most important thing above is that the `App` component passes down a function as a prop to the `ChildComponent`. The function `clickMe()` is used for the click handler in the `ChildComponent`, whereas the `ChildComponent` doesn’t know the logic of the function — it only triggers the function when the button gets clicked. The state is changed when the function is called, and once the state has changed, the state is passed down as a prop again. All affected components, like the child in our case, will render again.

We have to pass the state of the app, `isShow`, as a prop to the `ChildComponent`, because without it, we cannot write the logic above to display `greeting` when the state is updated.

Now that we’ve looked at functions, let’s turn to validation. It’s always a good practice to validate the data we get through props by using PropTypes. Let’s dive into that now.

{{% ad-panel-leaderboard %}}

## What Are PropTypes In React?

PropTypes are a mechanism to ensure that components use the correct data type and pass the right data, and that components use the right type of props, and that receiving components receive the right type of props.

We can think of it like a puppy being delivered to a pet store.  The pet store doesn't want pigs, lions, frogs, or geckos — it wants puppies. PropTypes ensure that the correct data type (puppy) is delivered to the pet store, and not some other kind of animal.

In the section above, we saw how to pass information to any component using props. We passed props directly as an attribute to the component, and we also passed props from outside of the component and used them in that component. But we didn’t check what type of values we are getting in our component through props or that everything still works.

It’s totally upon us whether to validate the data we get in a component through props. But in a complex application, it is always a good practice to validate that data.

### Using PropTypes

To make use of PropTypes, we have to add the package as a dependency to our application through npm or Yarn, by running the following code in the command line. For npm:

<pre><code class="language-bash">npm install --save prop-types
</code></pre>

And for Yarn:

<pre><code class="language-bash">yarn add prop-types
</code></pre>

To use PropTypes, we first need to import PropTypes from the prop-types package:

<pre><code class="language-bash">import PropTypes from 'prop-types';
</code></pre>

Let’s use ProTypes in our app that lists users’ posts. Here is how we will use it for the `Post` component:

<pre><code class="language-css">Post.proptypes = {
  id: PropTypes.number,
  content: PropTypes.string,
  user: PropTypes.string
}
</code></pre>

Here, `PropTypes.string` and `PropTypes.number` are prop validators that can be used to make sure that the props received are of the right type. In the code above, we’re declaring `id` to be a number, while `content` and `user` are to be strings.

Also, PropTypes are useful in catching bugs. And we can enforce passing props by using `isRequired`:

<pre><code class="language-css">Post.proptypes = {
  id: PropTypes.number.isRequired,
  content: PropTypes.string.isRequired,
  user: PropTypes.string.isRequired
}
</code></pre>

PropTypes have a lot of validators. Here are some of the most common ones:

<div class="break-out">

 <pre><code class="language-css">Component.proptypes = {
  stringProp: PropTypes.string,         // The prop should be a string
  numberProp: PropTypes.number,         // The prop should be a number
  anyProp: PropTypes.any,               // The prop can be of any data type
  booleanProp: PropTypes.bool,          // The prop should be a function
  functionProp: PropTypes.func          // The prop should be a function
  arrayProp: PropTypes.array            // The prop should be an array
}
</code></pre>
</div>

More types are available, which you can check in [React’s documentation](https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes)].

### Default Props

If we want to pass some default information to our components using props, React allows us to do so with something called `defaultProps`. In cases where PropTypes are optional (that is, they are not using `isRequired`), we can set `defaultProps`. Default props ensure that props have a value, in case nothing gets passed. Here is an example:

<pre><code class="language-css">Class Profile extends React.Component{

  // Specifies the default values for props
  static defaultProps = {
    name: 'Stranger'
  };

  // Renders "Welcome, Stranger":
  render() {
    return &lt;h2&gt; Welcome, {this.props.name}&lt;h2&gt;
  }
}
</code></pre>

Here, `defaultProps` will be used to ensure that `this.props.name` has a value, in case it is not specified by the parent component. If no name is passed to the class `Profile`, then it will have the default property `Stranger` to fall back on. This prevents any error when no prop is passed. I advise you always to use `defaultProps` for every optional PropType.

## Conclusion

I hope you’ve enjoyed working through this tutorial. Hopefully, it has shown you how important props and propTypes are to building React applications, because without them, we wouldn’t be able to pass data between components when interactions happen. They are a core part of the component-driven and state-management architecture that React is designed around.

PropTypes are a bonus for ensuring that components use the correct data type and pass the right data, and that components use the right type of props, and that receiving components receive the right type of props.

If you have any questions, you can leave them in the comments section below, and I’ll be happy to answer every one and work through any issues with you.

### References

- “[Thinking in React](https://reactjs.org/docs/thinking-in-react.html)”, React Docs
- “[List and Keys](https://reactjs.org/docs/lists-and-keys.html)”, React Docs
- “[Typechecking With PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes)”, React Docs
- “[How to Pass Props to Components in React](https://www.robinwieruch.de/react-pass-props-to-component)”, Robin Wieruch

{{< signature "ks, ra, al, il" >}}
